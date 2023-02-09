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
Recently I have moving in the direction of being a "C++ bad" person. I
have learned C++ through watching CppCon so it's not like I don't
understand the language. There were even a time when I was fulyl
bought in in its philosphy. This time has passes. In recent years I've
experiemented with just how little I can use of C++ and still be able
to write performant, good, and easy to understand code. I've also
thought about real hard about the dogmatic parts of C++ and whether
those are really neccesary. These are my thoughts on the matter.

## Observations bout modern C++

* **{{< color "#e34b4b">}}RAII is not that neccesary{{< /color>}}**

* **{{< color "#e34b4b">}}Move semantics are artifacacts of culture
  not neccessity {{< /color>}}** -- the current dogma goes as : We
  initialize resources in the constructor (like allocating memory) and
  then we dispose of them in the destructor (like deallocating
  memory). Also, when the copy construcotr is invoked, we copy the
  resources (e.g. allocate them again). Move semantics (by having
  concept of move constructor) allows us to avoid the copying in
  certain cases. In these cases, the new object can take ownership of
  the resoruces and we don't need to create them again. The current
  best practice tips are to be prodominatly in situations where we
  move-construct and not copy-construct.
  
  I posit that this whole spiel in unneccery. Why?
  1. Even before C++11 (pre move-semantics) we had only constructors,
     copy constructors, and desturctors. The basic idea of allocate in
     constructor and deallocate in the destructore was still
     prevelant. I think this is the root problem. The idea that we
     have to use construcotrs and destructors like that. In my
     experience, when things are properly set up, no object has to
     "take ownership" of anything. "Resources" are usually part of
     some bigger system and individual objects do not have to burden
     themselves with such management. And yes, I have the same
     considerations for memory allocations. In this sense, I don't
     worry about constructors and destrucotrs. No object releases
     resources when it dies. As a consequence, for me copy-construct =
     move-construct = memcpy.
  2. Move-constructing is essentially a memcpy with extra "marking"
     the old object as empty (usuall setting something to
     `nullptr`). Move-constructing is there because it allows us to do
     the naive thing (memcpy) without having to worry that two objects
     can hold the same resource. The C++ people say that we should
     mostly move. So like... we should mosty do `memcpy` + marking
     empty objects. Ok, if that's the case, why not go all the way and
     say. We should always `memcpy`. Also, do we really need the
     marking, I don't think so.
  3. If (that's a big if) there are cases when you actually want a
     true copy of an object, we could simply have something like
     `MyClass::Clone` method. We agreed that we are mostly moving, so
     the edge case is copying, so it should not be a problem having to
     call a method manually.
	 
 I have practive all of this for some time and, for me, I don't miss
 anything, things are great, things are simpler, and I don't have a
 bunch of code executed on each closing bracket. I consider these
 things worth it.

* Template magic seems to be unnecceary

* **{{< color "#e34b4b">}} The std is bad for any concrete software
  use case {{< /color>}}** -- even the C++ people agree that "STD is a
  general use library that fits the needs of the genral user of
  C++". My problem with this is that I strive to write to write
  "non-general" software. I write concrete sofware that solves
  concrete problem. I this concrete software has very concrete
  specifications where a lot assumptions are made. In this sense, I
  don't want a general library that does everything. I want very
  concreate piece of functionality which, generally, I have written to
  soleve my hyper-concrete problem.
  
  My other grife with the STD is its total disregard for memoy
  allocations. I want to write code that allocates as little as
  possible (even not at all). This is simply not possible if you use
  the STD. Using the STD, it's very easy to have lines that allocate
  several times just to deallocate at the end of the scope (or when
  some temporary is destroyed). I really want to avoid that.
  
  Finally, build times. Heavy usage of STD slows by build with
  noticable amount of sends. Build times can increase with 10+ seconds
  if good amount of std headers are included. For reference, my build
  times are ~3-5 seconds.
  
  Again, I have been not using STD for some time now and things are
  going great. Sometimes I have to do a bit of extra work but I feel
  it's worth it and my code runs faster.

*  **{{< color "#e34b4b">}}The burden of having lots of features{{<
   /color>}}**

* **{{< color "#e34b4b">}} C++ style type casts are the oposite of
  syntactic sugar{{< /color>}}** -- not much to say here. I don't use
  them because I don't want to type some big ugly thing. I have been
  using C-styled casts and things have not been falling apart.

## Rules for C++ live
To summerize my current attitudes towards C++, here is a list of
things I do and not do when working on my projects using C++.

* No constructors -- I don't use "resource aqusition" on object level;
  I don't want to execute code for every object on the stack;
* No desctructors -- I don't want to execute code on every closing
  bracket
* No RAII -- I use only `Defer { ... };` and that seems to be enough
* Move = Copy = memcpy -- I don't use "resource aqusition" on object
  level
* No exceptions -- exceptions are slow and are often abused
* No STD headers -- bloated, allocates unpredictably, compile times
  suffer
* No virtual functions -- I don't need that much of heavy mechanism
  for dynamic dispatch, function pointer is enough
* No heavy templates -- compile times suffer; the problems being
  solved with templates are generally non-problems
* No use of `private` -- getters and setters are annyoing
* Limited use of `const` -- it's just anoying
* Limited use of operator overloading -- not knowing what given piece
  of code executes makes it hard to reason about
* No storage of pointers to things -- use indexes instead,
  serializations becomes trivial
* No use of `malloc`/`free` or `new`/`delete` -- malloc is slow
