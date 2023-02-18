+++
title = "How DRY maybe hurting you"
author = "Stanislav Arnaudov"
description = "A meditation on the pitfals of code reuse"
date = 2023-02-18
draft = false
weight = 1
+++


## Abstract {#abstract}

The current culture of software development puts a huge emphasis on
the
[SOLID](https://www.dotnettricks.com/learn/designpatterns/different-types-of-software-design-principles) principles. In
universities, in boot camps, and crash courses young developers are
being told to follow these principles and this will eventually lead
them to produce "good software". Young developers, being young, follow
the principles dogmatically, often without stopping to think why are
they actually doing it and what the downstream consequences might be
of their design/approach choices. In this article, I want to consider
what might happen if one of these principles is taken too much at face
value.

## The DRY

One of the SOLID principles is DRY -- Don't Repeat Yourself. This is
mostly is viewed as:
* extract small pieces of functionality into functions
* extract big pieces of functionality into modules/packages
* more generally -- abstract commonalities between pieces of your
  program and let the individual pieces use the same abstract base

The overarching idea of course is that we can write some piece of code
once and use it in a variety of places, given that the code is at the
the right level of abstraction.
* Abstract enough to fit it in different places in different contexts
* Concrete enough so that it still does useful work.

This allows us to have easily maintainable software because we have to
work on one small piece of code at a time, not having to bother with
every other part of the program.

## The antithesis

All of this, I believe, is
the [Steel Man](https://constantrenewal.com/steel-man) case for DRY
(even though I've been mostly brief). I posit, **DRY can potentially
slow your growth as a developer**. By trying to abstract things away
and write them only once, you lose the chance to do something several
times and with that to explore what works well and what does not. The
core principles I would appeal to:

* Skills and knowledge come with practice
* Repetition solidifies your knowledge and skills and allows you to do
  things are slightly (or not slightly) different each time
* The process of interactive learning boils down to:
  - Perform action
  - Observe the results
  - Reflect on what went well and what can be improved
  - Consider how you would make things differently the next time you
    have the opportunity to perform a similar action
  - Do things differently the next time

In my experience, learning software development is not that different
from learning every other skill. You program stuff, you scale them,
you see the flaws in your code/design you've made along the way, you
experiment with other decisions, and you for the next time.


I've particularly found a great amount of value in exploring different
options for doing the same thing. Rarely I've written a system and
gotten it right the first time. An eye-opening moment was one of the
first episodes of [HandmadeHero](https://handmadehero.org/) where
Casey said, "I have a good idea of what I want from my platform layer
because I've done it 11 times". This simple statement made me think
about several things:
1. Of course! It's obvious. The more you do one thing, the better you
   get at it. The more you expose yourself to a problem in software
   development and the more ways you tackle this problem, the more you
   understand how to solve it.
2. You don't know what all of the constraints of a problem are before
   you've dealt with the problem for a while
3. Having encountered the same problem in different contexts exposes
   you to a variety of possible solutions


The fixation on DRY often makes you forget about all of these
considerations I've laid out. A lot of times I hear things along the
lines of
* "Let's design this system well and then we'll be able to use it all
  over the place"
* "System X solves problems related/close to our current
  problem. Let's modify System X slightly so that it also solves the
  current problem. This way we won't have two systems that are doing
  the same thing"
* "System X is not generic enough. We are not able to use it for
  anything else. Let's unify it with System Y so that we can use it in
  a variety of contexts"
* "We don't have unified handling of objects X, Y, Z. Let's create a a
  system that handles the commonalities between the objects."

The common factor among these is the desire to write/design something
once and then to not worry about it. The reality is that 99% of the
time you still end up modifying your reusable components to make the
useable for your next current problem for which you think "I have a a
component that almost solves this, we can reuse it here!".

This process puts much less emphasis on the exploration of what the
correct level of abstraction is and how to solve a given class of
problems in the best way. By trying to not repeat yourself from the
beginning, you lock yourself into the way you've implemented something
the first time you've encountered the problem. And this is bad. You
probably don't want to constrain yourself to some design before you've
understood the problem. And you understand the problem by solving it
in multiples ways in different manners, seeing what works and does
not.


Things that **I am not saying**:
* Introducing functions being called from different places is bad
* Having large pieces of code for some shared functionality is bad
* Having reusable components/subsystems is bad

Not following DRY dogmatically is as bad as obsessing over it. I am
not in favor of any extreme application of both sides of the
argument. I am only inviting you to consider how repeating yourself
from time to time presents opportunities for improvement.


## More concrete examples

All I've said so far is somewhat abstract. Here are a few examples
from my projects that illustrate what I am trying to convey.

In [DirectXer]({{< ref "directxer.md" >}}) I've had a lot of
applications where I've experimented with rendering, UI and UI layout
stuff, materials,
and [BVH](https://en.wikipedia.org/wiki/Bounding_volume_hierarchy)
traversals. Throughout the development of these applications some
"common functionalities" have started to emerge but I've always
delayed the "abstracting things away" step to the last possible time.

### ImGui panels

Multiple different applications have had very similar ImGui panels for
displaying/controlling various stuff -- telemetry information,
controlling the rendering, controlling parameters of some
subsystems. There was a time when I had three different applications
using almost the same ImGui panels but each had some quirk that had to
be considered separately. Things got extra annoying as I had to modify
the panel for controlling the renderer three times if I wanted the
same tweakable in the three applications. At this point, I decided
I've seen enough and I opted to unify all the application's panels so
that they use the same code. This gave me an opportunity to setup
things up in a way that I knew will cover all relevant use cases.

### Resource loading

Different applications were each loading resources in different
ways. For each application, I experimented with a slightly different
way of doing the loading. In the end when I thought I had enough
understanding of what the problem is, where things get annoying to
maintain, and what are the important constraints, I decided to pull
the trigger and create a unified system for asset loading that can be
used throughout DirectXer.


### Platform layers

The most frustrating part of setting up my applications has been to
figure out how to have the Win32 platform layer so that it is isolated
from the rest of the game/app. I've done it in a few ways now and I
have it somewhat figured out. Currently, all my example games use the
same platform layer base which is responsible for opening windows,
starting some worker threads, driving the game loop, etc. I've been
able to do this cleanly only because I've done it in a few different
ways for my other applications. During this exploration, I've kept a
lot of notes on what have been the problems with each approach so that
I can know better for the future. And I now know better. And that's
good.
