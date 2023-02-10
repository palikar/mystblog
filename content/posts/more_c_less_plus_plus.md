+++
title = "More C Less ++"
author = "Stanislav Arnaudov"
description = "A meditation on trying to attempt to remedy the C++ madness"
date = "2022-12-30"
draft = false
weight = 100
important_post = true
+++

## Abstract {#abstract}
Recently I have moved in the direction of being a "C++ bad" person. I
have learned C++ through watching [CppCon](https://cppcon.org/) talks
so it's not like I don't understand the language. There was even a
time when I fully bought into its philosophy. This time has
passed. In recent years I've experimented with just how little I can
use C++ and still be able to write performant, good, and easy-to-understand code. I've also thought about real hard about the dogmatic
parts of C++ and whether those are necessary. These are my
thoughts on the matter.

## Observations bout modern C++

* **{{< color "#e34b4b">}}RAII is not that neccesary{{< /color>}}**

One of C++'s greatest features has said to be the "}" (closing
bracket). In C++, on every closing bracket, we can implicitly execute
code thanks to some object going out of scope and its destructor being
invoked. The pattern that emerges is
* take some resources in the constructor of an object
* release these resources in the destructor
* the semantics of the language **guarantee** that the destructor will
be executed when the object goes out of scope
* this way you cannot forget to release the resources This is what we
call RAII.

In my experience from the last two years, not using extensively RAII
has not been a problem and my code hasn't suffered at all. The reasons
for this:
* If you properly set things up, there is not that much "taking some
  resources". Things are usually part of bigger overarching systems
  and I rarely (if at all) need to take-release something on a scope
  granularity. This is a stark difference to modern C++ practices
  where something trivial as a string object can be allocating memory
  when create and deallocating it when destroyed at the end of the
  scope. This leads to massive amounts of implicit code being executed
  at the end of most closing braces. Code that really shouldn't there
* The implicit nature of the execution hides what is actually
  happening and allows you to forget about it. I understand that this
  is the main idea but I find it deeply unsettling that there is code
  in my programs that is being executed at the end of each scope that
  I cannot see or reason about it. It makes optimizing hard, hides
  details about your program from you, and it encourages you not to
  think about what is actually going on in a function/scope, even when
  you are looking at it.
  
In my current code base, I use RAII for only two things:
1. To implement a convenient `Defer` macro which lets me execute a
given block of code at the end of the enclosing scope. So something
like

```c++ MyResorucee res; Init(res); Defer { Destroy(res); } ```
2. To create "time blocks" which take performance measurements of the
time spent in a given scope.

For these two use cases, RAII is undoubtedly useful. For everything
else that the C++ people tell you to use RAII, I think I am doing just
fine without it.

* **{{< color "#e34b4b">}}Move semantics are an artifact of culture,
  not necessity {{< /color>}}** -- the current dogma goes as follows: We
  initialize resources in the constructor (like allocating memory) and
  then we dispose of them in the destructor (like deallocating
  memory). Also, when the copy constructor is invoked, we copy the
  resources (e.g. allocate them again). Move semantics (by having
  the concept of a move constructor) allows us to avoid copying in
  certain cases. In these cases, the new object can take ownership of
  the resources and we don't need to create them again. The current
  best practice tips are to be predominantly in situations where we
  move-construct and not copy-construct.
  
  I posit that this whole spiel is unnecessary. Here is why:
  1. Even before C++11 (pre-move-semantics) we had only constructors,
     copy constructors, and destructors. The basic idea of allocating in
     the constructor and deallocating in the destructor was still
     prevalent. I think this is the root problem. The idea that we
     have to use constructors and destructors like that. In my
     experience, when things are properly set up, no object has to
     "take ownership" of anything. "Resources" are usually part of
     some bigger system and individual objects do not have to burden
     themselves with such management. And yes, I have the same
     considerations for memory allocations. In this sense, I don't
     worry about constructors and destructors. No object releases
     resources when it dies. As a consequence, for me copy-construct =
     move-construct = memcpy.
  2. Move-constructing is essentially a memcpy with extra "marking"
     the old object as empty (usually setting something to
     `nullptr`). Move-constructing is there because it allows us to do
     the naive thing (memcpy) without having to worry that two objects
     can hold the same resource. The C++ people say that we should
     mostly move. So like... we should mostly do `memcpy` + marking
     empty objects. Ok, if that's the case, why not go all the way and
     say. We should always `memcpy`. Also, do we really need the
     marking, I don't think so.
  3. If (that's a big if) there are cases when you actually want a
     true copy of an object, we could simply have something like
     `MyClass::Clone` method. We agreed that we are mostly moving, so
     the edge case is copying, so it should not be a problem to have to
     call a method manually.
	 
 I have practiced all of this for some time and, for me, I don't miss
 anything, things are great, things are simpler, and I don't have a
 bunch of code executed on each closing bracket. I consider these
 things worth it.

* **{{< color "#e34b4b">}} Template magic seems to be unnecessary use
case {{< /color>}}** At some point I heard the statement "People
invent problems to solve with templates" and since then I cannot stop
thinking about it. I've noticed that most of the time I've written
some template-heavy code it has essentially been for the reason of
"wouldn't it be cool, if...". I guess it is cool, but also not
necessary. Sometimes templates allow you to create more intuitive API
but most of the time this quickly devolves into a huge unmaintainable
mess that can't even be debugged properly. Also, again build times
suffer greatly without having something that justifies the cost. I've
opted for very limited use of templates and I have not noticed me
wanting to go back. To be clear, I still think that templates make
sense for
* simple containers -- maps and vectors
* some math utilities
* handling variadic arguments in a typesafe way

* **{{< color "#e34b4b">}} The std is bad for any concrete software
  use case {{< /color>}}** -- even the C++ people agree that "STD is a
  general use library that fits the needs of the general user of
  C++". My problem with this is that I strive to write to write
  "non-general" software. I write concrete software that solves
  concrete problems. And this concrete software has very concrete
  specifications where a lot of assumptions are made. In this sense, I
  don't want a general library that does everything. I want a very
  concrete piece of functionality which, generally, I have written to
  solve my hyper-concrete problem.
  
  My other gripe with the STD is its total disregard for memory
  allocations. I want to write code that allocates as little as
  possible (even not at all). This is simply not possible if you use
  the STD. Using the STD, it's very easy to have lines that allocate
  several times just to deallocate at the end of the scope (or when
  some temporary is destroyed). I really want to avoid that.
  
  Finally, build times. Heavy usage of STD slows by build with
  a noticeable amount of sends. Build times can increase with 10+ seconds
  if a good amount of std headers are included. For reference, my build
  times are ~3-5 seconds (that's for a full non-incremental build ).
  
  Again, I have been not using STD for some time now and things are
  going great. Sometimes I have to do a bit of extra work but I feel
  it's worth it and my code runs faster.

* **{{< color "#e34b4b">}} C++ style type casts are the oposite of
  syntactic sugar{{< /color>}}** -- not much to say here. I don't use
  them because I don't want to type some big ugly thing. I have been
  using C-styled casts and things have not been falling apart.

## Rules for C++ live
To summarize my current attitudes toward C++, here is a list of
things I do and do not do when working on my projects using C++.

* No constructors -- I don't use "resource acquisition" on the object level;
  I don't want to execute code for every object on the stack;
* No destructors -- I don't want to execute code on every closing
  bracket
* No RAII -- I use only `Defer { ... };` and that seems to be enough
* Move = Copy = memcpy -- I don't use "resource acquisition" on object
  level
* No exceptions -- exceptions are slow and are often abused
* No STD headers -- bloated, allocates unpredictably, compile times
  suffer
* No virtual functions -- I don't need that much of a heavy mechanism
  for dynamic dispatch, a function pointer is enough
* No heavy templates -- compile times suffer; the problems being
  solved with templates are generally non-problems
* No use of `private` -- getters and setters are annoying
* Limited use of `const` -- it's just annoying
* Limited use of operator overloading -- not knowing what given piece
  of code executes makes it hard to reason about
* No storage of pointers to things -- use indices instead,
  serialization theen becomes trivial
* No use of `malloc`/`free` or `new`/`delete` -- malloc is slow and my goal is zero allocations/deallocations past initialization
