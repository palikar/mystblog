+++
title = "Software development philosophy"
author = "Stanislav Arnaudov"
description = "A statement on how I like to do software developement"
date = "2022-12-25"
draft = false
weight = 100
important_post = true
+++

In the last couple of years, I've had a major shift in the way I view
the whole process of "software development". In this post, I want to
share my current views and clearly state what I (currently) believe
about programming, what my priorities are, and what I am thinking
about when starting a new software project.

## My shift in perspective

Several factors made me reconsider what I believe bout software
development. I'll summarize them here while giving a short explanation
of why has each been relevant to me.


* **{{< color "#e34b4b">}}Getting exposed to performance-oriented
  software{{< /color>}}** -- The people I can thank for that
  are [Jonathan Blow](https://en.wikipedia.org/wiki/Jonathan_Blow)
  and [Casey Muratori](https://caseymuratori.com/). On Blow's side --
  he has a stream where he programs his compiler for
  the
  [Jai Programming language](https://github.com/BSVino/JaiPrimer/blob/master/JaiPrimer.md).
  The compiler is famous for its speed and Blow has claimed that he
  thinks the compiler can reach about **1 million** lines of code per
  second. The moment I saw how Blow compiles a ~30,000 LOC game
  written in Jai for less than 1 second, my immediate thought was
  "Wait, this is possible?!?! I want everything I make to be this
  fast".
  
  The other person that influenced me -- Muratori -- has a series of
  streams where he develops [HandmadeHero](https://handmadehero.org/)
  -- a complete game written from scratch. I've played with the game's
  source code for a while and I am amazed about how smoothly
  everything runs and everything loads instantly. On the other hand, I
  was amazed how during his streams Muratori does not present some
  wild concepts about how to write code, how to design the
  architecture, or what language feature (of C++) to use. He just
  "types the code" and creates as few moving parts as possible. This
  was a stark contrast to what [CppCon](https://cppcon.org/) would
  have me believe about developing something with C++. The clarity and
  simplicity of the code coupled with its performance is what earned
  my admiration and me wanting to delve deeper into this style of
  programming/development.

* **{{< color "#e34b4b">}}Modern software development demanding an
  ever-increasing metal strain{{< /color>}}** -- Writing software
  these days bring a lot of what we can call "artificial complexity"
  with it. There is always some library to be used weirdly, some tool
  that needs complex setup, some language feature that claims to solve
  a problem that is only introduced by another language feature that
  we've told ourselves we want to use. Earlier in my life as a
  developer, I almost enjoyed this complexity as it made be think that
  I was doing something exciting (I mean, it's complex so it HAS to be
  important and worthwhile, right?).
  
  This was keeping me going for some time but at some point, I started
  wanting something "more". I was already sold on the idea of
  *minimalism* (through my experience with Linux) so it was only a
  matter of time for this to seep in in my programming. At some point
  I started forcing myself to use fewer and fewer c++ features, fewer
  std headers, fewer libraries, and fewer everything. And so I
  discovered that I don't actually need the vast majority of things I
  thought I needed to make a functional program run. Based on this, it
  seems rather obvious that if I can achieve more with less, there is
  no reason to ever go back to "using more".
  
  Right now, I am at a point where glorifying complexity seems simply
  nonsensical. I do not want to be burdened with all of the
  complexities introduced by language features, third-party code, and
  frameworks that dictate how I should structure my program or
  cumbersome tools with questionable value added.

* **{{< color "#e34b4b">}}Seeing and experiencing the results of not
  doing things "the modern way"{{< /color>}}** -- This is closely
  related to the other two factors, but the focus here is on the
  results of not doing things the way my university, CppCon, and every
  book on modern software developer practices. For the most part, I
  was astonished at just how much value can "simply typing the code"
  can bring.
  
  Up to some point, I had the perspective that starting a new project
  always begins with some big planning/design step where you lay out
  the core components of the system you want to build. You think
  everything over, you discuss the design with yourself and
  others. You try to predict what problems are to be solved and you
  solve them before they are even actual problems. When it comes time
  to write the code, you maximize the use of language features, you
  use the standard library, and follow the best practices dictated by
  the gurus. At some point, you realized that you've built a bloated
  and overly complex mess that runs slowly, has bugs, and you have no
  idea how it works. At this point is however too late to change it
  now, you tell yourself that you'll do better on your next
  project. This experience is repeated for every new project.
  
  I thought this was what software development was all about. I
  accepted that this is why people say that programming is hard. I
  thought there was no other way of doing programming. Spoiler alert
  -- there is. Turns out, things I thought were not the only way of
  getting work done. I tried some other things, I discovered stuff for
  myself, and I listen to people who have been developing software
  since forever.
  
   * Questions about architecture and their answers become clearer
  once you know the domain of the problem. And the domain is only
  knowledgable through doing some exploratory programming experiments.
   
   * Not using libraries keeps your compile times low. And having
     quick feedback from your compiler. And having quick feedback
     makes the developing experience that much more pleasant.
   
   * Staying in your code avoids the insanity you go through when
  wanting to use some poorly documented third party. And dealing with
  this insanity is solving a problem that is not actually there.
  
These together with some other observations made me solidify my
opinion that the "modern" dogma is something to be avoided.

## My Core values

* **{{< color "#e34b4b">}}CPUs and computers are fast, so should be
  software{{< /color>}}**. In this day and age, there's no reason why
  any newly developed software should be slow. CPUs can run millions
  of instructions per second so any slowness that is introduced comes
  at the software level. This should not be the case and every
  developer should be obsessed with the performance of their
  product. This is very often not the case and we have taught
  ourselves to put the performance question on the backburner in favor
  of more abstract goals like "clean code", "good design", and
  "understandable architecture". As far as I am concerned, the primary
  reason for all of these should be to facilitate performant
  software. It is shame that these days users expect the software that
  they use to be slow and don't even question if something can be done
  about this. Something can be done about this and there is a way to
  make useful software that does not feel sluggish.

* **{{< color "#e34b4b">}}Polishing software is developing software{{<
  /color>}}**. There is this perception that when hunting and clearing
  up bugs in your software, you are not really doing exciting
  work. This should not be the case. Every solved bug is a measurable
  improvement of your product and it guarantees that the users of the
  product won't hit that bug. Having a great experience with a
  software product means not encountering bugs and weird
  behaviors. Cleaning up bugs and weird behavior is thus of the most
  importance for the health and perception of your product. Having a
  few features that function well and without problems brings a much
  better experience than having a bloated mess of half-baked features
  where every other user hits a crash. Because of this polishing and
  making sure that the existing features work as intended should take
  precedence over adding new functionality for the sake of "having
  something new to show".

* **{{< color "#e34b4b">}}If there is no obvious reason for having
  complexity, then complexity is bad{{< /color>}}**. Complexity, more
  often than not, **kills** software by introducing (usually) slow and
  hard-to-maintain code. Having high complexity in your system ensures
  that at some point no one will know how your software
  works. Debugging will be hard. Adding new features will be breaking
  things you didn't expect. Your confidence that your product works as
  intended will be low. No one should ever want this. Reducing
  complexity should be always on your mind when developing. Abstract
  promises of "how to manage complexity" should be taken with a grain
  of salt. Not having the complexity in the first place is almost
  always the preferable thing.
  

* **{{< color "#e34b4b">}}Writing your code is easier than using
  someone else's{{< /color>}}**. There are two major modes I am in
  when writing software.
   1. I am developing the code for my program and I am solving the
         problem at hand through the code.
   2. I am trying to integrate some libraries into my code or use some
      API. The problem at hand here is the integration itself. I am
      not doing any real work, I'm merely trying to get to a state
      where I would be able to do real work once the library is
      integrated with my own code.
  
  Doing number 1 feels great -- I feel creative, I experiment and
  discover things, and I figure out new ways of doing things. Number 2
  is horrible and can be absolutely torturous. Given this, I want to
  avoid number 2 and I strive to stay completely in number 1.
  
  Also, rarely do I need the whole of the functionality that a library
  provides. I most often need a small piece of functionality. If this
  is the case, why not simply write this small piece of functionality
  myself, gain the knowledge of how to do it, and avoid the pain of
  using a third-party library? The time investment is often comparable
  to integrating the library, and if it is not, I am ok with it.


* **{{< color "#e34b4b">}}OOP sells you a promise that is yet to be
  fulfilled{{< /color>}}**. *Object Oriented Programming* is the
  defacto way we teach programming these days. Since my early
  high-school days of programming, through university, and past work
  environment, the prevailing idea seems to be that your program
  should be this collection of objects, and if you manage to set up
  these objects in the right way with the correct relationships
  between them, you'll have *clean*, easy to maintain and modify
  software, that everyone can understand. This simply hasn't been the
  case for anything of medium complexity that I've written. I know all
  the design patterns, I've applied them all, and I've followed the
  instructions, but still to no avail. The resulting software is slow,
  bug-prone, and hard to understand and reason about.
  
  The killer question that got me to actively start moving away from
  OOP -- "Can you give me one example of a software project that is
  well designed and it uses OOP?"

* **{{< color "#e34b4b">}} All programs solve problems about data {{<
  /color>}}** Moving away from OOP has led me to Data-Oriented
  Design. There are many ways to (not) describe what DOD is but the
  core principles I've identified are:
  * Objects are not carriers of behaviour but rather of data
  * The data and how you transform it into other data is the problem
  * Procedures transform one set of data into another
  
  I want to think about how I access my data, how I iterate on it, and
  what happens in the memory of the computer when I do so. This leads
  to software that respects its inputs and the hardware it's running
  on.
  
------------------- Yes, some of these (if not all) sound obvious. Any
developer should be able to recognize where the virtue of these points
lies and every point should seem non-controversial nor
profound. Still, I found it useful to state exactly what I believe.

## Meaning of believe

It is often however the case that we as developers forget to practice
the things we hold to be true. Having the right values is great but
ultimately useless if you don't live them out in your day-to-day
live. Therefore I think it is necessary to not only state what you
believe in but also to s have something actionable that puts your
beliefs and ideals in the real world.

For me, *practice* is the way I live up to the aforementioned core
values. Practicing means a very specific thing and it goes as follows:

*  **{{< color "#e34b4b">}}Picking a task that is slightly above my
  current skill level{{< /color>}}** -- so that I can learn something
  from the whole endeavour

* **{{< color "#e34b4b">}}Solving the task under the constraints of my
  core values{{< /color>}}** -- so that I can actually put my ideals
  in the real world

* **{{< color "#e34b4b">}}Relfecting on what went well and what did
  not{{< /color>}}** -- so that I have more knowledge for the future
  
* **{{< color "#e34b4b">}}Adjusting my ideas and expectations for the
  future{{< /color>}}** -- so that I can now make more educated
  guesses for any future tasks\projects

* **{{< color "#e34b4b">}}Repeat{{< /color>}}** -- so that I
  constantly learn something new, develop my skillset and knowladge
  base, live out my values and having actual real things that I can
  point to when I have to show that my beliefs work in the real world
  and are not merely "theories" about how software development should
  be done.

* ... -- ???


* {{< color "#e34b4b">}} Profit {{< /color>}}
