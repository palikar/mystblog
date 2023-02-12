+++
title = "Mission Control"
author = "Stanislav Arnaudov"
description = "A build tool that I use to build my other applications and libraries"
date = 2022-12-26
draft = false
weight = 100
is_project_page = true
+++

.## Abstract {#abstract}

Mission Control is the product of my frustration with MSBuild and
Visual Studio. Everything happens super slow in Visual Studio, if I
want to make something happen, I always end up battling MSBuild
configurations in the UI, things are not obvious, and all of this eats
my time without giving me any deeper knowledge of... anything really.

This led to me spending a week or two developing and fleshing out
Mission Control -- tool written in C-styled C++ that uses nothing but
Win32 libraries to do everything that it needs to. And it does not need
to do much. For the most part, Mission Control accepts some sort of
"command" and generates and executes a `.bat` file that "executes"
this command. The BAT file usually contains calls to `cl.exe` with the
appropriate flags to build my projects. In the beginning, this was all
Mission Control was capable of. Now I use it for various build commands
in DirectXer.


## Principles

The core principles I follow and how they apply to Mission Control:

* Performance -- it should do very little and it should do it fast
* Near zero dependencies -- it should compile on its own and depend
  only on system libraries that come with windows
* Simplicity -- changing something should be trivial and itss inner
  workings should be obvious to understand.
  
  
## Notable achievements

Currently, I use Mission Control for:

* Building my sample games
* Building my auxiliary tools like CIBot, AssetBuilder, PerfChecker
  and SceneChecker.
* Compiling my HLSL shaders to C++ header files.
* Creating certain soft links in the DirectXer repository because some
  applications expect certain things to be in certain places
* Build all the third-party libraries I use
  --
  [freetype](http://freetype.org/),
  [ImGui](https://github.com/ocornut/imgui),
  [Opticks](https://github.com/bombomby/optick)
  [Stb](https://github.com/nothings/stb)
  
  
Some other nice features of Mission Control that make my life easier:

* Can build games with Clang and enable build instrumentation for build
  performance investigations.
* Can build in Release and Debug modes
* Can insert extra C pre-processor defines for build passes as command line arguments
* Can checkout git revisions
* Can be started in daemon mode where it will accept commands though
  sockets and execute them.
  
Some of these are specifically there for nice integration with
the [CIBot]({{< ref "CIBot.md" >}})
