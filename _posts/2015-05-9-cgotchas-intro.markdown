---
layout: post
title: Cgo(tchas)
categories: [tutorials]
tags: [Go, Cgo, C, Lisp]
description: Exploring tricky Cgo situations when working with a simple C library
---

When working an existing C library into a [Go](http://golang.org/) project using [Cgo](http://golang.org/cmd/cgo/),
there are some C language features that are tricky to handle.
This post will work through several examples,
the highlights involving Cgo's handling of C unions and variadic arguments.

Background
----------

With both [LambdaConf](http://www.degoesconsulting.com/lambdaconf-2015/)
and [Gophercon](http://gophercon.com/) being held in Colorado for another year,
I wanted to embark on a project that would combine the ideas of functional programming with Go.
Eventually, I decided on working through the book [Build Your Own Lisp](http://www.buildyourownlisp.com/),
using the Go programming language.
Because the material was written using the C programming language as a base,
I thought translating the examples into Go would be an interesting test of Go's reputation as a modern C. (As a C/C++ user during the day, the idea of Go as a replacement for C seemed a bit unusual given some of Go's design decisions, but that is a discussion for another day.)
The exercise involved a few technical speed bumps that led to the impetus for this series:

The book makes use of a [Micro Parsers Combinators](https://github.com/orangeduck/mpc) library
to define and parse a grammar for a Lisp-like language.
Because this library was created with C,
there was an opportunity to use Cgo to integrate it into my Go-based project.
While working with the API provided by mpc,
I ran into a few C code examples that were unexpectedly tricky to handle for Cgo.
Hopefully such examples will provide some useful tips for working with C and Go interoperability.


Function calls (and Go/C String conversions)
-----------------
Suppose after reading through the [parsing chapter of Build Your Own Lisp](http://www.buildyourownlisp.com/chapter6_parsing),
you want to integrate mpc into a Go program that creates a parser for a polish notation grammar.
The first steps involve initializing the individual parsers for numbers, operators and expressions,
which will be combined to create the overall "Lispy" parser.

We'll need to use the following C API:
{% highlight c %}
mpc_parser_t *mpc_new(const char *name);
{% endhighlight %}

... which is a function that takes in name string, and returns a pointer:
{% highlight go %}
mpc_parser_t* Number = mpc_new("number");
{% endhighlight %}

To start the project,
let's create a main program loop (main.go) in the same directory that the mpc.h and mpc.c files are copied to.

As usual, start off with the package declaration:
{% highlight go %}
package main
{% endhighlight %}

... followed by a block of Cgo-related code to import the header for mpc:
{% highlight go %}
/*
#cgo LDFLAGS: -lm
#include "mpc.h"
*/
import "C"
{% endhighlight %}

The #cgo directive includes a compiler flag -lm that brings in some math functionality used by mpc in its internal workings.
This line is optional on some setups, but not on others.
For example, Travic CI will [fail](https://travis-ci.org/sunzenshen/go-build-your-own-lisp/builds/54618585)
until that dependency is [resolved](https://travis-ci.org/sunzenshen/go-build-your-own-lisp/builds/54650990),
while my local environment is indifferent to this setting.

To make use of the mpc_new function, we need to convert a Go string into a C type that is compatible with the input parameter:
{% highlight go %}
name := "Name of parser defined"
cName := C.CString(name)
defer C.free(unsafe.Pointer(cName))
return C.mpc_new(cName)
{% endhighlight %}
Because C has no garbage collection, and Cgo allocates the memory on the C heap,
we need to remember to clean up that memory,
with defer simplifying the question of when.

As we'll be using the function mpc_new several times,
wrapping the above pattern into a function will save keystrokes in the long run:
{% highlight go %}
func mpcNew(name string) *C.mpc_parser_t {
	cName := C.CString(name)
	defer C.free(unsafe.Pointer(cName))
	return C.mpc_new(cName)
}
{% endhighlight %}

By this point, we can now initialize a pointer to an mpc parser.
[(example)](https://github.com/sunzenshen/cgotchas/blob/2cb05c3b1b474fd0a42ff12955319131f3a38e28/main.go)


Abstracting Cgo usage (Undefined symbols when linking with "go run")
---------------------

If the previous example is run with "go run main.go", you may run into issues getting the C compiler to link the mpc files:

{% highlight bash %}
> go run main.go
# command-line-arguments
Undefined symbols for architecture x86_64:
  "_mpc_new", referenced from:
      __cgo_2ab80fd5553f_Cfunc_mpc_new in main.cgo2.o
     (maybe you meant: __cgo_2ab80fd5553f_Cfunc_mpc_new)
ld: symbol(s) not found for architecture x86_64
clang: error: linker command failed with exit code 1 (use -v to see invocation)
{% endhighlight %}

Instead, you can try building an executable first, before running it:
{% highlight bash %}
> go build
> ./cgotchas
{% endhighlight %}

We can actually get "go run" working again by moving our Cgo code into its own package,
which can then be imported into a main program loop.
This also has the advantage of providing a generic interface to the mpc library, that we can use in other Go projects.

Here's a rough outline of the steps:

* Move the mpc header and source files into their own package location (perhaps into a folder called "mpc").

* Declare the name of the Go package.

* [Export](http://golang.org/ref/spec#Exported_identifiers) any functions or types to be used outside the package.


The goal of the last step is to minimize the amount of direct contact with Cgo.
For example, instead of passing around a *C.mpc_parser_t around the code base,
we could declare a new type that hides the Cgo usage:
{% highlight go %}
type Parser *C.mpc_parser_t
func New(name string) Parser {
     // return a parser with the given name
}
{% endhighlight %}

Then after importing our new package:
{% highlight go %}
import "github.com/<github_username>/cgotchas/mpc"
{% endhighlight %}

We are now able to call the mpc types and functions defined:
{% highlight go %}
var number mpc.Parser
number = mpc.New("number")
{% endhighlight %}

In fact, now that the mpc-related Cgo code has been isolated into its own package, "go run main.go" will now work.
I ought to look into why this organization fixes the linker error,
but I would guess that there is some building of the Cgo code before it is imported into another context.
 
By now, we should be ready to continue building up the interface to mpc,
while minimizing exposure to C code with the rest of the project.
[(example)](https://github.com/sunzenshen/cgotchas/tree/mpc_isolation)


Memory Cleanup (Handling variadic-argument functions from C)
------------------------------------------------------------
Because C does not manage memory automatically,
take care when calling any C code that may allocate memory on the heap.
The mpc_new function from our library is a convenient example of this memory allocation,
and has a corresponding utility function that frees the resources taken:
{% highlight c %}
void mpc_cleanup(int n, ...);
{% endhighlight %}

Go has support for variadic argument functions too,
so we may try something along these lines:
{% highlight go %}
func Cleanup(p Parser) {
	C.mpc_cleanup(1, p)
}
{% endhighlight %}

But that would result in this compilation error:
{% highlight bash %}
mpc/mpc.go:22:2: unexpected type: ...
{% endhighlight %}

While Go has support for variadic arguments,
Cgo does not appear to support handling variadic arguments from C (if it does, please let me know!).
In order to use mpc_cleanup,
we will need to create our own wrapper in C to call that function with a fixed number of arguments.

Let's create a new C header file,
called [mpc_interface.h](https://github.com/sunzenshen/cgotchas/blob/mpc_cleanup_1/mpc/mpc_interface.h),
with a wrapper function:
{% highlight c %}
#include "mpc.h"

inline void mpc_cleanup_if(mpc_parser_t* parser) {
  mpc_cleanup(1, parser);
}
{% endhighlight %}

We'll also need to edit the mpc.go file to include this new header:
{% highlight go %}
/*
#cgo LDFLAGS: -lm
#include "mpc_interface.h"
*/
import "C"
{% endhighlight %}

Because mpc_interface.h already includes mpc.h, we don't need to include the latter again.

Finally, we can make use of our new wrapper:
{% highlight go %}
package main

import "github.com/sunzenshen/cgotchas/mpc"

func main() {
	var number mpc.Parser
	number = mpc.New("number")
	mpc.Cleanup(number)
}
{% endhighlight %}

The project now has a way to call mpc_cleanup with 1 argument.
[(example)](https://github.com/sunzenshen/cgotchas/tree/mpc_cleanup_1)

If any C programmers in the audience are getting agitated about a critical and missing protection, hold on a second:

C macro guards
--------------
When importing our new header file,
we need to watch for accidentally duplicating the contents of that file through multiple inclusion.
For example, if we import the header file twice:
{% highlight go %}
/*
#cgo LDFLAGS: -lm
#include "mpc_interface.h"
#include "mpc_interface.h"
*/
import "C"
{% endhighlight %}

My example as is would result in the following perplexing error:
{% highlight bash %}
In file included from mpc/mpc.go:6:
./mpc_interface.h:3:13: error: redefinition of 'mpc_cleanup_if'
inline void mpc_cleanup_if(mpc_parser_t* parser) {
            ^
./mpc_interface.h:3:13: note: previous definition is here
inline void mpc_cleanup_if(mpc_parser_t* parser) {
            ^
1 error generated.
{% endhighlight %}

While your code may return a slightly different error depending on the ordering of your function definitions,
the key highlight is on the redefinition of a function... at the same place it was originally defined.

The (partially inaccurate to spec) way I like to think of this scenario is to consider C code
as being manipulated by another set of instructions focused on the text processing of C source files.
These instructions are the C preprocessor commands, indicated by the #-symbol:
{% highlight c %}
#cgo LDFLAGS: -lm
#include "mpc_interface.h"
{% endhighlight %}

Some preprocessor commands, like the #cgo directive, are instructions for the compiler,
and my metaphor doesn't accurately describe them.

But the #include command be be thought of as instruction as saying:

* This is a text function

* That takes a "local" header name as an argument

* And then inserts the entire contents of that file at this location


These instructions work towards the end goal of creating a single source listing of all the C code for a program.
That is, the separation of source files is only an abstraction that helps organize a C project,
but everything ends up in a single location.

(Ignoring the differences between static and dynamic linking. This story is getting shakier by the second!)

This creation of a single source file is the reason why
"[warning : No new line at end of file](http://stackoverflow.com/questions/72271/no-newline-at-end-of-file-compiler-warning)"
is a thing in C, because if two different #include(s) were placed right next to each other,
there's a risk that the first instruction of the second header would be pasted on the same line of the
last line of the first header.

Back to the error example of stacking the same #include directive,
doing so caused the source code for "mpc_interface.h" to be inserted twice in a row.
This led to the duplication of definition that was reported.

We can use C preprocessor commands to avoid this duplication:
[(example)](https://github.com/sunzenshen/cgotchas/commit/a58fd1ef9e756794428442b9886655f3b7b3a657)
{% highlight c %}
#ifndef MPC_INTERFACE_H
#define MPC_INTERFACE_H

// The rest of the contents in mpc_interface.h

#endif
{% endhighlight %}

Let's break down the preprocessor commands:

* \#ifndef

\#ifndef looks for a definition of a processor symbol MPC_INTERFACE_H.
If a definition is found, skip over this entire code block terminated by #endif.
Otherwise, if a definition was not found, read in the next lines of code...

* \#define

\#define in a sense, takes in 2 arguments, a symbol name, and what that symbol represents.

This is how constants are often created in C,
where every place that symbol is seen, the contents are replaced by the second argument.
{% highlight c %}
#define ANSWER 42
// Any instance of ANSWER is this file will now be replaced with 42...
{% endhighlight %}
A common convention is to make symbol names all capitalized,
but this is not enforced by the C compiler.
The relative lack of all caps in conventional variable names makes such a naming scheme safer to use with the preprocessor.

In our example, this defines a symbol MPC_INTERFACE_H that is defined to be nothing.
If we had used MPC_INTERFACE_H anywhere in the C code, that text would essentially be deleted.
Preprocessor symbols are persistent until #undef are called on them (especially when reading/re-reading files),
so the next time #ifndef reads this symbol, the condition will be false.

* \#endif

As mentioned earlier, #endif closes the conditional block initiated by #ifndef.
If that condition evaluates to false, file reading will skip to after this line.

These commands avoid the error of the repeated #include instructions with the following behavior:

\#include "mpc_interface.h"

* Begin reading mpc_interface.h

* Look up symbol MPC_INTERFACE_H

* Symbol MPC_INTERFACE_H was not found

* Continue reading the incoming lines

* define symbol MPC_INTERFACE_H with nothing

* continue reading in the rest of the lines until end of file

\#include "mpc_interface.h" (second pass)

* Begin reading mpc_interface.h

* Look up symbol MPC_INTERFACE_H

* MPC_INTERFACE_H is defined

* Skip until #endif

* continue reading in the rest of the lines until end of file


Maintaining wrappers for C variadic arguments
-----------------------------------------

There's a major inefficiency with this approach of creating C wrappers,
as new wrapper functions need to be defined for different numbers of arguments.
For example, let's revisit the other parsers needed for the project:
{% highlight go %}
number := mpc.New("number")
operator := mpc.New("operator")
expr := mpc.New("expr")
lispy := mpc.New("lispy")
{% endhighlight %}

To handle 4 parsers with the mpc_cleanup function, another wrapper is needed:
{% highlight c %}
inline void mpc_cleanup_if
(
  mpc_parser_t* p1,
  mpc_parser_t* p2,
  mpc_parser_t* p3,
  mpc_parser_t* p4
)
{
  mpc_cleanup(4, p1, p2, p3, p4);
}
{% endhighlight %}

As well as a way to call it in Go:
{% highlight go %}
func Cleanup(p1, p2, p3, p4 Parser) {
	C.mpc_cleanup_if(p1, p2, p3, p4)
}
{% endhighlight %}

This plumbing work was not that tedious for this project,
as C variadic function uses were not so numerous and required only infrequent updates,
much like this [example](https://github.com/sunzenshen/cgotchas/commit/26465d067777c19b513ed664a7951cbacfc58dcb).


Intermission (Hand waving turns to hand flailing)
--------------------------------------
Next I would like to cover how Go handles C's union feature,
but good chunk of additional work is needed to get to that point.

Specifically, we need to define the grammar for our parser as this C example demonstrates:
{% highlight c %}
mpca_lang(MPCA_LANG_DEFAULT,
  "                                                     \
    number   : /-?[0-9]+/ ;                             \
    operator : '+' | '-' | '*' | '/' ;                  \
    expr     : <number> | '(' <operator> <expr>+ ')' ;  \
    lispy    : /^/ <operator> <expr>+ /$/ ;             \
  ",
  Number, Operator, Expr, Lispy);
{% endhighlight %}

Making use of that interface involves a number of steps similar to those covered earlier.
For now, I'll leave the adaptation to Go as an exercise for the reader,
as well as provide an [example](https://github.com/sunzenshen/cgotchas/tree/grammar_definition)
of such [work](https://github.com/sunzenshen/cgotchas/commit/d66b33eb65d774f1e5e532de90b9c64edb02ab91).
If you would like me to expand on this section,
feel free to let me know.


Accessing the fruits of labor (from a C union)
----------------------------------------------
At some point, we'll have successfully used the mpc library to extract a structured result into the following C union:
{% highlight c %}
typedef union {
  mpc_err_t *error;
  mpc_val_t *output; // void pointer, interpreted as a mpc_ast_t
} mpc_result_t;
{% endhighlight %}

... where depending on the result of mpc's parsing functions, mpc_result_t is either a struct containing error information, or a struct containing the parsing output.

Normally, the fields of C unions are accessed in this manner:
{% highlight c %}
mpc_result_t r;
// attempt to fill out the mpc result "r" with parsed output
if (mpc_parse("<stdin>", input, Lispy, &r)) { 
  // Do something with: r.output
} else {
  // Do something with: r.error
}
{% endhighlight %}

However, Go does not support such syntax,
and if the above syntax is emulated, the compiler reports the following error:
{% highlight bash %}
r.output undefined (type C.mpc_result_t has no field or method output)
{% endhighlight %}

Instead, the contents of the union need to be accessed through casting of the pointer:
{% highlight go %}
// Assuming that we have a mpc result:
var result C.result *C.mpc_result_t
// Accessing the error field
errorPointer := (**C.mpc_err_t)(unsafe.Pointer(result))
// Remember that mpc_val_t is a void pointer, reinterpreted as an AST
astPointer := (**C.mpc_ast_t)(unsafe.Pointer(result))
{% endhighlight %}

Why does this work?  In Cgo, C unions are represented as an array of bytes,
with the size aligned to the largest member of the union.

For example, in the following union:
{% highlight c %}
union foo {
    char   c;
    int    i;
    double d;
};
{% endhighlight %}

... the double variable accounts for an 8 byte allocation with my machine.

Print that C union, and Go will print something like this:
{% highlight go %}
// Minimum value
&[0 0 0 0 0 0 0 0]
// Maximum value
&[255 255 255 255 255 255 255 255]
{% endhighlight %}

Meanwhile this union is sized based on the int variable, at 4 bytes:
{% highlight c %}
union foo {
    char   c;
    int    i;
};
{% endhighlight %}

It's also worth pointing out that the number of members does not affect the size of the byte array representing the union.

An example demonstrating union access in a project can be found [here](https://github.com/sunzenshen/cgotchas/tree/print_ast).


Final thoughts
--------------
By this point, the chapter has been completed using Go,
and the rest of the book can be tackled using the approaches we just covered.

Have thoughts or feedback regarding the explanations?
Could a particular section be expanded?
If so, feel free to contact me @sunzenshen on Twitter, or sunzenshen @ Gmail.


Additional References
----------

* [C? Go? Cgo!](http://blog.golang.org/c-go-cgo)
* [Stack Overflow: Golang Cgo Convering union field to go type](http://stackoverflow.com/questions/14581063/golang-cgo-converting-union-field-to-go-type)
* [Stack Overflow: cgo : Undefined symbols for architecture x86_64](http://stackoverflow.com/questions/28593574/cgo-undefined-symbols-for-architecture-x86-64)
* [golang-nuts: cgo and varargs](https://groups.google.com/forum/#!topic/golang-nuts/cl1i2ZVUZqk)
* [Slides from a talk I gave on this same topic](https://github.com/sunzenshen/go-build-your-own-lisp/tree/talk_cgotchas/slides)
* [Make a Lisp, another useful resource for implementing your own lisp](https://github.com/kanaka/mal)