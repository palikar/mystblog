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
until some point, I was familiar only with OpenGL and I wanted to
learn THE mainstream API for graphics programming. DirectXer was the a
project where I was experimenting and figuring things out about doing
real-time rendering.

Over time, however, DirectXer evolved into my primary "code base"
where I was doing everything, again in an experimental fashion. I was
doing things like figuring out what memory management solution works
best, how to do 3D and 2D rendering on the GPU, how to load my assets
quicky, what is a good approach to doing UI in video games, and much
more.

Right now, DirectXer is again more like a platform or like a suit of
functionality where I am still figuring things out about the game
development in general.

## Principles

Almost for the entirety of the development of DirectXer, I have been
trying to follow my core principles
from
[my software philosophy article]({{< ref "software_philosophy.md" >}}). For
this project I've left every "modern" practice I've been taught in my
university and through watching CppCon talks and started exploring and
seeing what works well for me. In this sense, I am much more following
the approach
of [Casey Muratori in Handmade Hero](https://handmadehero.org/)

With that, the guiding principles for almost everything in DirectXer
are:
* Simplicity
* Performance
* Stability
* Doing less in code while still solving the actual problem
* Making and figuring out architecture questions yourself rather than
  following dogma
* Minimal reliance on Third Party Libraries

## Notable applications

Part of DirectXer are:

* [Mission Control]({{< ref "MissionControl.md">}}) -- my custom buidl
  system type of application. At some point, I got frustrated with
  MSBuild and Visual Studio 2022 so much that I decided to quit them
  and for a week I ended up writing *Mission Control* in my spare
  time. Currently, the project is quite mature and can compile sample
  games, tools, and that-party libraries that I use. It's written in C
  styled C++ has no dependencies and is compiled with a simple BAT
  script by directly calling `cl.exe` (Microsoft's C++ compiler)

	{{< figure width=1024px src="/img/mission_control_demo.png" >}}
	
* [CIBot]({{< ref "CIBot.md">}})Bot -- At my workplace, almost
  everyone has always been frustrated with our CI build system
  (it's [BuildBot](https://buildbot.net/) btw). The CI has been doing
  its job mostly fine but at some moments, the introduced complexity
  was taking its toll. At one point I started asking myself "Why is
  this so hard? I just need my CI that runs some commands on the
  console. Why can't I have just this?". Then, predictably, I started
  working on a CI solution for my personal projects and after a week
  or two of spare time developing, I had my CIBot -- a simple
  application that can connect to Mission Control (started in daemon
  mod) and execute commands/build through it.
  
	{{< figure width=1024px src="/img/cibot_demo.png">}}

* [AssetBuilder]({{< ref "AssetBuilder.md">}}) -- as I am primarily
  focused on game programming, I want my assets to be loaded as
  quickly as possible, without doing any extra work that I don't have
  to do. Hence, all the assets (images, models, animations, textures,
  etc.) are packed in a custom file format from which the game runtime
  can quickly load everything necessary. *AssetBuilder* is the
  application that processes and packs the needed assets in this
  optimized file.
  
  {{< figure width=1024px src="/img/asset_builder_demo.png">}}
  
* **SceneChecker** -- as I do a lot of rendering-related things, it's
  often really important to know if I've accidentally broken something
  while programming and suddenly things don't visually look the way
  they should. At my workplace, we also have similar concerns and
  there we have several systems that run certain scenes and compare
  the rendered output against a reference one. *SceneChecker* is my
  attempt to have such a system. Currently, the application can run
  2D/3D scenes, save outputs as a reference and then run the same
  scenes to verify the visual output. The whole program is designed to
  be as performant as possible so the tests can be run in a matter of
  seconds. The tool also can generate an HTML page summarizing the
  results of the visual tests.
  
  {{< figure width=1024px src="/img/scene_checker_demo.png" >}}

* **PerfChecker** -- this is the tool that helps me track the
  performance of the example 2D and 3D scenes that I
  have. *PerfChecker* is very similar to SceneChecker but its only job
  is to create reports of the telemetry data gathered during the
  running of the scenes.
  
  {{< figure width=1024px src="/img/perf_checker_demo.png" >}}

## Notable achievements

Here is a list of some random stuff that I've implemented in DirectXer
and that I am proud of. By no means this is an exhaustive list but I
don't want to get into every small implementation detail I've dealt
with in the past two years. The major things are:

* PBR Rendering -- I wanted to learn and see how every modern game
  does its PBR (Physically based rendering) materials so I spend some
  time figuring this aspect out. My current implementation of PBR
  rendering also includes IBL (Image based lighting) for getting
  ambient diffuse and specular reflections.

* **Shadow mapping** -- I've always wanted to implement shadow mapping and
  at some point, I got to it. Now my 3D scenes can be rendered with up
  to 4 shadow maps for different parts of the view frustum
  
  {{< figure width=1024px src="/img/shadows_demo.gif" >}}

* **Bloom filter** -- no modern game can be complete without the nice
  glowing effects that the bloom filter provides so I decided to see
  if I can implement it for myself. My implementation is fully done
  with compute shaders and it's the
  "Standard"
  [state of the art one](http://www.iryoku.com/next-generation-post-processing-in-call-of-duty-advanced-warfare).
  
  {{< figure width=1024px src="/img/bloom_demo.png" >}}

* **Water rendering** -- probably not exactly what you would expect for
  water rendering but I really like the low poly style water from
  the [ThimMatrix](https://www.youtube.com/watch?v=5yhDb9dzJ58). I
  remember being in high school watching this low poly water tutorial
  and now I finally felt confident to pretty much do it myself... so I
  did it.
  
  {{< figure width=1024px src="/img/water_scene_demo.gif" >}}

* **Mesh Skinning and Animations** -- obviously animations are a big part
  of any game so I couldn't have this. My current system does bone
  transformation calculations and the mesh skinning entirely in
  compute shaders.
  
  {{< figure width=1024px src="/img/animation_demo.gif" >}}

* **BUI* and UI Rendering* -- at my day job at Coherent Labs, we are
  developing a game UI library that can render HTML/CSS/JS in a
  performance-oriented way suitable for games. Based on that, I have
  some experience with the Web standard, the problems with it, and the
  parts that make performance optimizations hard. This is why for
  several months I spent time developing my own custom UI rendering
  solution -- *BUI* (Beter UI, yes, not very imaginative). It's a
  custom HTML/CSS-like syntax that allows you to place elements on the
  screen and lay them out. It's nothing special but I don't think I
  need something special to make a good enough UI so it does the job.

* **ImGui integrations** -- not exactly a selling point but I do use ImGui
  extensively for debugging/editor stuff and I wanted to mention
  it. Also, the UI of CIBot is entirely ImGui.

* **2D Rendering API** -- I've talked about 3D Rendering but the 2D
  rendering in DirectXer is also something I've spent a large time
  on. Currently, my 2D renderer is quite capable and can draw simple
  shapes, images, supports transformations, can draw text, and can
  apply simple effects such as blur, saturation, and brightness.

* **Fast Unit Builds** -- every application in DirectXer is compiled in
  three to four `.cpp` files. I don't use incremental builds and the
  whole application I am working on is compiled every time I make a
  change to some file. Build times generally vary in the range of ~2-5
  seconds while sometimes they go as low as 1.8 seconds. This is in
  stark contrast when working on large code bases with Visual Studio
  where MSBuild needs around 5 seconds to only start compiling the
  changed files. I thought that compiling everything every single time
  will be annoying but this hasn't really been the case as 2-3 seconds
  of build time do not get in my way when programming.
