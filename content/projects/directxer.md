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

Part of DirectXer ares:

* [Mission Control]({{< ref "MissionControl.md">}}) -- my custom buidl
  system type of application. At some point I gor frustureated with
  MSBuild and Visual Studio 2022 so much that I decided to quit them
  and for a week I ended up writing *Mission Control* in my spare
  time. Currently the project is quit mature and can compile my games,
  tools, and that-party libraries that I use. It's written in C styled
  C++, has no ependecies, and is compiled with simple BAT script by
  dirrectly calling `cl.exe` (Microsoft's C++ compiler)

* CIBot --

* AssetBuilder --

## Notable achievements

* PBR Rendering

* Shadow mapping

* Bloom filtering

* Water rendering

* Mesh Skinning and Animations

* UI Rendering

* ImGui integrations

* 2D Rendering API

## Scenes 2D



## Scenes 3D
