---
layout: post
title: How I Start - C# on Mac OS X
categories: [tutorials]
tags: [C#]
description: How to get started with solving C# exercism.io exercises with Xamarin Studio on Mac OS X.
---

While working on the C# exercises from [exercism.io](http://exercism.io/),
I noticed that the [getting started documentation](http://help.exercism.io/getting-started-with-csharp.html)
was light on specific setup procedures for Xamarin Studio and OS X
(at least compared to the adjacent set of Visual Studio instructions).
Here is a workflow that works for me:

Installing Xamarin Studio
-------------------------
Follow the link from the
[getting started guide](http://help.exercism.io/getting-started-with-csharp.html)
to download [Xamarin Studio](http://xamarin.com/download) .
The default options of the installation wizard are sufficient for installing the app.

Creating A New Solution
-----------------------
After starting up Xamarin Studio, there is a dialog for creating a "New Solution...".
The following template settings will work with the NUnit tests provided by each exercism.io exercise:

* Other > .NET
* General > NUnit Library Project (C#)

Next, these were the settings I used in "Configure your new Project":

* Project Name: leap
* Solution Name: csharp 
* Location: [your path here]/exercism 
* [Enabled] Create a project within the solution directory 

This will create a project directory inside the "exercism" folder which mimics the directory structure of exercism/csharp.
Along these lines, the initial project "leap" corresponds with the first C# exercise.
Subsequent exercises are then managed as additional projects under this same "csharp" solution.

Note that the "Version Control" settings optional here.
I personally use the GitHub desktop client to manage the source code for my
[submissions](https://github.com/sunzenshen/exercism-submissions/tree/master/csharp),
and the example .gitignore file was useful for that setup.
I also prefer to place the Xamarin project in a separate location from my exercism install,
to allow rolling back any unsuccessful experiments with the project setup.

Working With The First Exercise
-------------------------------
By this point, a solution called "csharp" will have been created,
with an initial project called "leap".
To initiate the exercise,
I copy over the "LeapTest.cs" unit tests from exercism to my "leap" project folder.
I also add the file's location to the "leap" project:

* Right click on the "leap" project under the "csharp" solution explorer.
* Add > Add Files ...
* Select "LeapTest.cs"

At this point, you can also remove the unused "Test.cs" unit test file from the project.

If you hit the "Run All" button under the "Unit Tests" menu,
you should see failing test cases because of the missing implementation code.
In response, these were the options I chose for creating a "New File...":

* General > Empty Class (C#)
* Name: Leap

This creates a file called "Leap.cs" where the exercise implementation can be written.

Creating Projects For The Next Exercises
----------------------------------------

After submitting the solution for the "leap" exercise,
the "bob" exercise is fetched next from exercism.
To create the corresponding project under the "csharp" solution:

* Right click on "csharp" under the solution explorer
* Add > Add New Project...
* Other > .NET
* General > NUnit Library Project (C#)

Under "Configure your new project", the "Project Name:" can be set to the name of the next exercise (bob).

This process of copying over the unit tests, creating an implementation file, and solving the exercise can then be repeated for as many exercises attempted.

Discussion
----------
> Like this post, or would like to discuss it on some sort of forum?
> Feel free to post it on your favorite social media site (HN, Reddit, Lobste.rs, etc), and to send me the link!
> I promise to relink the discussion thread from this post, and to upvote your submission.
> It'll be win-win: you'll rake in the sweet-sweet karma/points/upvotes,
> and I won't need to worry about hunting spam-bots in an otherwise empty Disqus thread.