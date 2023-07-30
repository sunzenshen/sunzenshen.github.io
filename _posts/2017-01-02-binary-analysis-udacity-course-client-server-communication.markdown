---
layout: post
title: What's In A Binary? Udacity - Client-Server Communication
categories: [lab_notes]
tags: [binary_analysis, Go]
description: Discovering useful open source libraries through string browsing of a Go binary file
---

Recently, I took Udacity's short and free [Client-Server Communication](https://www.udacity.com/course/client-server-communication--ud897) course to review HTTP concepts.
When working through the interactive labs, it struck me as a bit funny that they ask you to casually execute binary files to run each of the localhost servers for each exercise.
I actually trust Udacity/Google not to do anything suspicious, but was curious to see if I could get any insights about how the binaries were made.

The notes below involve the "devtools_mac_amd64" binary included in "L1-DevTools.zip" from the "Quiz: DevTools Quiz" section of the course.

Step 1: Totally fail to use radare2
-----------------------------------
To start, I thought it would be fun to follow Sushant's [An Introduction to radare2](http://sushant94.me/2015/05/31/Introduction_to_radare2/) as a first trial of radare2.
I was able to load the binary with ```r2 ./devtools_mac_amd64```, but then immediately noticed that a [Go](https://golang.org/) library was in use:

![Where to start...]({{ site.images }}radare2_VV_sym.github.com_GeertJohan_go.rice_embedded.png)

This gave me a hint that trying to examine the assembly code would be a bit too much for someone who hasn't fully Read The * Manual yet,
but this also gave me the idea of looking at the strings in the file.

strings
-------
I recalled seeing a way to filter [strings](http://manpages.ubuntu.com/manpages/zesty/en/man1/strings.1posix.html)
from a LiveOverflow video about [finding the license key in a naive key check implementation](https://www.youtube.com/watch?v=3NTXFUxcKPc&feature=youtu.be&t=2m43s).

How many results would the default arguments output?

```
> strings devtools_mac_amd64 | wc -l
   65861
```

Okay, so maybe manually inspecting all those results might not be the best use of time.
How about searching for GitHub urls like from the radare2 output above?

```
> strings devtools_mac_amd64 | grep github | wc -l
     638
```

From that list, the list of included libraries emerges:

* [github.com/GeertJohan/go.rice](https://github.com/GeertJohan/go.rice)
* [github.com/daaku/go%2ezipexe.OpenCloser](https://github.com/daaku/go.zipexe)
* [github.com/kardianos/osext.Executable](https://github.com/kardianos/osext)

... oh, hey, is that a directory listing of the instructor's Go sources?

```
/Users/surma/src/github.com/kardianos/osext/osext_sysctl.go
/Users/surma/src/github.com/kardianos/osext/osext.go
/Users/surma/src/github.com/daaku/go.zipexe/zipexe.go
/Users/surma/src/github.com/GeertJohan/go.rice/walk.go
/Users/surma/src/github.com/GeertJohan/go.rice/virtual.go
/Users/surma/src/github.com/GeertJohan/go.rice/sort.go
/Users/surma/src/github.com/GeertJohan/go.rice/http.go
/Users/surma/src/github.com/GeertJohan/go.rice/file.go
/Users/surma/src/github.com/GeertJohan/go.rice/embedded.go
/Users/surma/src/github.com/GeertJohan/go.rice/box.go
/Users/surma/src/github.com/GeertJohan/go.rice/appended.go
/Users/surma/src/github.com/GeertJohan/go.rice/embedded/embedded.go
/Users/surma/src/github.com/udacity/ud897-client-server-communication/devtools/main.go
/Users/surma/src/github.com/udacity/ud897-client-server-communication/devtools/assets.rice-box.go
/Users/surma/src/github.com/udacity/ud897-client-server-communication/devtools/assets.rice-box.go
/Users/surma/src/github.com/udacity/ud897-client-server-communication/devtools/main.go
/Users/surma/src/github.com/GeertJohan/go.rice/embedded/embedded.go
/Users/surma/src/github.com/GeertJohan/go.rice/appended.go
/Users/surma/src/github.com/GeertJohan/go.rice/box.go
/Users/surma/src/github.com/GeertJohan/go.rice/embedded.go
/Users/surma/src/github.com/GeertJohan/go.rice/file.go
/Users/surma/src/github.com/GeertJohan/go.rice/http.go
/Users/surma/src/github.com/GeertJohan/go.rice/sort.go
/Users/surma/src/github.com/GeertJohan/go.rice/virtual.go
/Users/surma/src/github.com/GeertJohan/go.rice/walk.go
/Users/surma/src/github.com/daaku/go.zipexe/zipexe.go
/Users/surma/src/github.com/kardianos/osext/osext.go
/Users/surma/src/github.com/kardianos/osext/osext_sysctl.go
/Users/surma/src/github.com/udacity/ud897-client-server-communication
```

?

```
/Users/surma/src/github.com/udacity/ud897-client-server-communication
```

[https://github.com/udacity/ud897-client-server-communication](https://github.com/udacity/ud897-client-server-communication) /facepalm

So it turns out that I totally forgot to search around on GitHub/Google for the course source code, before embarking on this wild goose chase.
At least now we know where to see how Surma implemented each of the exercise binaries.
I suppose one could wear some tin-foil and wonder if the compiled binaries match, but I'm not nearly paranoid enough to consider that a realistic concern.

Now wondering how much information the binary leaks about the user's setup, I alter the query to search the instructor's username:

```
> strings devtools_mac_amd64 | grep surma
/Users/surma/.homebrew/Cellar/go/1.6.2/libexec
...
```

From this, I'm guessing that the binaries were built using Go 1.6.2 on an OSX setup involving [Homebrew](http://brew.sh/).
Thankfully, it looks like all the list entries are related to the Go libraries used in the project,
so I don't need to worry about too much about my directory info being leaked should I distribute Go binaries myself.

Now curious about my own Go projects, I pull a copy of the code for my [toy lisp project](https://github.com/sunzenshen/go-build-your-own-lisp):

```
> go build
> strings go-build-your-own-lisp | grep /Users/
/Users/MAWS/go/src/github.com/sunzenshen/go-build-your-own-lisp/mpc/mpc_interface.go
/Users/MAWS/go/src/github.com/sunzenshen/go-build-your-own-lisp/mpc/
/Users/MAWS/go/src/github.com/sunzenshen/go-build-your-own-lisp/lispy/lval.go
/Users/MAWS/go/src/github.com/sunzenshen/go-build-your-own-lisp/lispy/lispy.go
/Users/MAWS/go/src/github.com/sunzenshen/go-build-your-own-lisp/lispy/lenv.go
/Users/MAWS/go/src/github.com/sunzenshen/go-build-your-own-lisp/lispy/builtin.go
/Users/MAWS/go/src/github.com/sunzenshen/go-build-your-own-lisp/main.go
```

Neat, so if I send a binary to someone, they could learn that I keep my Go source files in ```/Users/MAWS/go/src/github.com/sunzenshen/```,
and that I named my OSX account after an obscure [Neotokyo](http://www.neotokyohq.com/) [reference](https://neotokyohq.com/map_large_maws.html).
After feeling a bit slimy looking up Surma's /Users/ directory, may as well out myself too.

So what did we learn here?
--------------------------

* Where to find the source code for the Client-Server Communication exercise binaries.
* A way to determine which libraries a Go binary uses. (usually redundant given the open source culture of the language community)
* That you can get a little formation about the binary creator's directory structure for Go projects.

I'm hopeful that the last item is not a big concern, given the prevalence of screencasts showing such information.
That said, if you think looking up such information is in bad taste, feel free to caps-lock at me on Twitter and the usual channels.
