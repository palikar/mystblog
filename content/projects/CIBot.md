+++
title = "CIBot"
author = "Stanislav Arnaudov"
description = "CI tool that can connect to MissionControl, issue builds, collect information about them, and generate build reports"
date = 2022-12-27
draft = false
weight = 100
is_project_page = true
+++

## Abstract {#abstract}

As mentioned in [DirectXer]({{< ref "directxer.md" >}}), CIBot is my
Continuous Integration and automation solution. I mainly developed
CIBot because I didn't want to deal with some other CI systems like
Jenkins, GitHub actions, or whatever is popular right now. I wanted
to have a system that is optimized for me, does not waste my time,
has the features I need, and nothing more.

In the spirit of DirectXer, I decided to create this myself. I spend a
week or two working on this project and learn tons of stuff along
the way. In this article, I'll present the main features of CIBot and
how I use them.

## Principles

The core principles I follow and how they apply to CIBot:

* Performance -- everything should happen quickly and smoothly
* Simplicity -- it should just run some commands and present their
  output
* Usability -- it should provide me with the information that I need
  in a convenient manner.

## Notable achievements

* **Integration with MissionControl** -- MissionControl can be started
  in a special Daemo mode where it will start a TCP server and start
  accepting commands through a socket. CIBot can establish a connection
  with this server and start sending commands to be executed. Commands
  include
  * Building a game
  * Building a library
  * Building a tool
  * Building the shaders
  * Building packed assets bundle
    through [AssetBuilder]({{< ref "AssetBuilder.md" >}})
  * Special "perform build" commands that execute a list of predefined steps
  
  {{< figure width=1024px src="/img/cibot_1.png" >}}

* ** Launching predefined simple commands** -- At the root DirectXer
  repository, I have a special `.compile` file that contains a list
  of possible commands for Mission Controle. The file is also used by
  my Emacs to quickly let me choose what I want to compile. CIBot can
  read this command list and execute each command through the
  connected Mission Control. 

  {{< figure width=1024px src="/img/cibot_2.png" >}}
  
* **Issuing complete builds based on predefined builders** -- I have
  special files that are just listings of commands for Mission
  Control. These listings can be executed with a single "build" command
  through Mission Control that CIBot issues. Mission Control
  executes each command and reports the status of each step. 

 {{< figure width=1024px src="/img/cibot_3.png" >}}

* **Reviewing old builds** -- CIBot stores information about all past
  builds in a [SQLite](https://www.sqlite.org/index.html)
  database. Information about previous builds can be displayed in the
  UI so I can quickly see what build has passed and what has not. The
  SQLite integration uses only the official SQLite C library and
  nothing more. Every SQL query is written by hand.
 
 {{< figure width=1024px src="/img/cibot_4.png" >}}
 
* **Build reports generating** -- after each build CIBot can generate
  a summary report of the build in the form of a Markdown file that I
  can inspect through my browser.
  
  {{< figure width=1024px src="/img/cibot_5.png" >}}

## Things that CIBot still lacks

There are a couple of features that CIBot still does not have because
I haven't gotten around to implementing them. These are:

* A way to schedule builds at certain parts of the day
* A way to start automatic builds on a new commit in the DirectXer
  repository

