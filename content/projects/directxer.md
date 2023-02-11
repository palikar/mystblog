+++
title = "DirectXer"
author = "Stanislav Arnaudov"
description = "Playground for game engine ideas and experiments"
date = 2022-12-25
draft = false
weight = 100
is_project_page = true
important_post = true
+++

## Abstract {#abstract}


[DirectXer](https://github.com/palikar/DirectXer) started as a way for
me
learn
[DirectX11](https://learn.microsoft.com/en-us/windows/win32/direct3d11/atoc-dx-graphics-direct3d-11). Up
until some point I was familiar only with OpenGL and I wanted to learn
THE main stream API for graphics programming. DirectXer was the
project where I was experimenting and figuring things out about doing
real-time rendering.

Over the time, however, DirectXer evolved into my primary "code base"
where I was doing everything, again in experimental fashion. I was
doing things like figuring out what memory management solution works
best, how to do 3D and 2D rendreing on the GPU, how to load my assets
quicky, what is a good approach to doing UI in video games, and much
more.

Right now, DirectXer is again more like a platform or like a suit of
functionality where I am still figuring things out about game
developement.

## Principles

Almost for the entirety of the developement of DirectXer I have been
trying to follow my core principles
from
[my software philosophy article]({{< ref "software_philosophy.md" >}}). For
this project I've left every "modern" practice I've been taught in my
university nad throught watching CppCon talks and started exploring
and seeing what works well myself. In this sense, I am much more
following the approach
of [Casey Muratori in Handmade Hero](https://handmadehero.org/)

With that, the guiding principles for almost everything in DirectXer are:
* Simplicity
* Performance
* Stability
* Doing less in code while still solving the actual problem
* Making and figuring architecture questions yourself rather than following dogma
* Minimal reliance on Third Party libraries

## Notable applications

Part of DirectXer are:

* [Mission Control]({{< ref "MissionControl.md">}}) -- my custom buidl
  system type of application. At some point I gor frustureated with
  MSBuild and Visual Studio 2022 so much that I decided to quit them
  and for a week I ended up writing *Mission Control* in my spare
  time. Currently the project is quit mature and can compile my games,
  tools, and that-party libraries that I use. It's written in C styled
  C++, has no ependecies, and is compiled with simple BAT script by
  dirrectly calling `cl.exe` (Microsoft's C++ compiler)

* [CIBot]({{< ref "CIBot.md.md">}})Bot -- At my work place
  almost everyone has always be frustrated with our CI build system
  (it's [BuildBot](https://buildbot.net/) btw). The CI has been doing
  it'S job mostly fine but at some moments, the introduced complexity
  was taking it's toll. At one point I started asking myself "Why is
  this so hard? I just need my CI that run some commands on the
  console. Why can't I have just this?". Then, predictably, I started
  working on a CI solution for my persoanl projects and after a week
  or two of spare time developing, I had my CIBot -- a simple
  application that can connect to Mission Controll (started in daemonq
  mod) and execute commands/build through it.

* [AssetBuilder]({{< ref "AssetBuilder.md">}}) -- as I am primarly
  focused on game programming, I want my assets to be loaded as quick
  as possible, without doing any extra work that I don't have to
  do. Hence, I all the assets (images, models, animations, textures,
  etc.) are packed in a custom file format from which the game runtime
  can quickly load everything necessary. *AssetBuilder* is the
  application that processes and packs the needed assets in this optimized
  file.
  
* **SceneChecker** -- as I do a lot of rendering related things, it's
  foten really important to know if I've accedently broken something
  while programming and suddently things don't visually look the way
  they should. At my workplace we also have similar concerns and there
  we have several systems that run certain scenes and compare the
  rendered output against a refrence one. *SceneChecker* is my attempt
  to have such system. Currently the application can run 2D/3D scenes,
  save outputs as reference and then run the same scenes to verify the
  visual output. The while program is designed to be as performant as
  possible so the tests can be run in a matter of seconds.

* **PerfChecker** -- this is my tools that helps my track performance
  of the example 2D and 3D scenes that I have. *PerfChecker* is very
  similar to SceneChecker but its only job is to create reports of the
  telemetry data gatherd during the running of the scenes.

## Notable achievements

* PBR Rendering

* Shadow mapping

* Bloom filtering

* Water rendering

* Mesh Skinning and Animations

* UI Rendering

* ImGui integrations

* 2D Rendering API

* Fast Unit Builds -- every application in DirectXer is compiled in
  three to four `.cpp` files. I don't use incremental builds and the
  whole application I am woking on is compiled every time I make a
  change to some file. Build times genrally vary in the range ~2-5
  seconds while sometimes they go as low as 1.8 seconds. This is stark
  contrast when working on large code bases with Visual Studio where
  the MSBuild needs around 5 seconds to only start compiling the
  changed files. I thought that compiling everything eevry single time
  will be annoying but this hasn't relly been the case as 2-3 seconds
  of build time do not get in my way when programming.

## Scenes 2D



## Scenes 3D
