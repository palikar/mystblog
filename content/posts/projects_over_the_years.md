+++
title = "Summary of my personal projects from over the years"
author = "Stanislav Arnaudov"
description = "A list of my personal projects that can be used as reference about what have I done in my career"
date = 2023-06-24
draft = false
weight = 1
+++


## Abstract {#abstract}

This post is meant as an answer to questions of the type "Tell me
about some of your personal projects". I'll go over every major
endeavor that I've undertaken per my own initiative and I'll give a
little bit information on why I've chosen to write it, what has been
the idea, and what I have learned in the process of making it.


## --- AdvancedResouceMenaging ---
[Github Repository](https://github.com/palikar/AdvancedResouceMenaging)

A Java application from my high-school days. The idea was to develop a
software that can create a school schedule for teachers and classes
given how many of each subject every class should have per week.

Algorithmically this was essentially a constraint satisfaction problem
where we must create the schedule for every teacher and class such
that it does not conflict with the schedules of the other teachers and
classes while still fulfilling the subjects per week requirements for
each class.

<img width="512px"
src="https://raw.githubusercontent.com/palikar/AdvancedResouceMenaging/master/screenshots/screen_1.png"
style="display: inline-block"> <img width="512px"
src="https://raw.githubusercontent.com/palikar/AdvancedResouceMenaging/master/screenshots/screen_3.png"
style="display: inline-block">

What I've learned during the development
* algorithmic thinking and design
* Java 8, Java Swing

## --- TicTacMiniMax ---
[Github Repository](https://github.com/palikar/TicTacMiniMax)

A small project from my early university days where the user can play
a game of Tic-Tac-Toe against the computer. The computer is playing
optimally and it is virtually impossible for a human to beat it.

Around this time I was learning about a lot of AI concepts and one of
them was the idea of the MiniMax algorithm. TicTacMiniMax was a
practical way for me to learn and understand the essence of the
algorithm.

![TicTacToe](https://raw.githubusercontent.com/palikar/TicTacMiniMax/master/demo.png)

What I've learned during the development
* a practical use of the Minimax algorithm
* Java 8

## --- python-requirements-installer ---
[Github Repository](https://github.com/palikar/python-requirements-installer)

A very simple [Emacs](https://www.gnu.org/software/emacs/) package
that helps with handling Python `requirements.txt` files. When such a
file is opened, through the package, Emacs reads its content and
highlights the installed packages in green and the not installed ones
in red. The user can also decide to install the missing Python
packages through `pip`.

![RequirementsInstaller](https://raw.githubusercontent.com/palikar/python-requirements-installer/master/screenshot/packages-highlighted.png)

What I've learned during development
* Emacs packages development
* Emacs Lisp

## --- HomeworksSmart ---
[Github Repository](https://github.com/palikar/HomeworksSmart)

This was a web application developed for a course at my
university. The app was meant as a homework and note management tool
where the user can create homework that they have assigned, keep track
of them, and mark them as complete when they are completed. In the
app, there was also not taking section where you can write something
down and refer to it later. There was also a "Productivity Hub" where
the user can do Pomodoro sessions for a certain homework.

<img width="1024px" src="/img/project_summary/smart_homeworks_1.png"
style="display: inline-block"> <img width="1024px"
src="/img/project_summary/smart_homeworks_2.png" style="display:
inline-block">

The whole thing was built as a single-page VueJS application that
stored all relevant data in the browser's local storage.

What I've learned during the development
* HTML/CSS/JavaScript
* Bootstrap, VueJS
* General web development

## --- MandelbrotWorks ---
[Github Repository](https://github.com/palikar/MandelbrotWorks)

Another pure interest project about visualizing
the [Mandelbrot](https://en.wikipedia.org/wiki/Mandelbrot_set) as well
as generating [Buddhabrot](https://en.wikipedia.org/wiki/Buddhabrot)
images. I read about those things on some blog somewhere and decided
that I got to implement something like this. I spend a week
researching and implementing and I managed to generate some
interesting pictures.

What I've learned during the development
* C++, CMake
* A little bit of OpenCV

## --- Evaluating Stochastic Regression Models on the Basis of Heterogenous Sensor Networks ---
[Github Repository](https://github.com/palikar/PollutionDev)

This was my Bachelor's thesis at my university. This thesis aimed to
better understand Bayesian machine learning models and their practical
use on real-world data. We examine two models that incorporate
uncertainty in their predictions – Bayesian Neural Networks and
Mixture Density Networks. The used data comes from air-pollution
sensors. The quality of three of the sensors is known to be high but
for the rest of them, the quality of measurement is unknown. We aim to
build a model that can predict air pollution at some sensor at a given
time. Consideration of the uncertainty in the predicted value is
crucial as it allows the precise evaluation of the generated
models. We compare the models through evaluation with proper scoring
rules. As the quality of the majority of sensors is unknown, we try to
find out which of the sensors are most relevant for the prediction
through a feature importance technique. We leverage the capabilities
of Tensorflow, Edward, and GPFlow as machine learning libraries in
order to build probabilistic regression models that can be further
evaluated.

<img width="1024px"
src="/img/project_summary/pollution_dev_system.png" style="display:
inline-block">

If you want to check the whole
thesis,
[this](https://github.com/palikar/PollutionDev/blob/master/Thesis/thesis.pdf) is
it in its entirety.

What I've learned during the development
* python
* Tensorflow, pandas, numpy, SciKit-learn
* Scientific writing

## --- CodeManager ---
[Github Repository](https://github.com/palikar/code_manager)

A tool I've spent a lot of time tinkering with and using. In my Linux
days I was using a Debian as my distribution and did not have access
to something like
the [AUR (Arch User Repository)](https://aur.archlinux.org/). So, my
solution was to develop a custom tool that helps me pull code from
GitHub, compile it locally and then install it. CodeManager had a
sizable database in the form of a JSON file in which I had numerous
Gibhub repositories (some personal, some not). Through the tool, I was
able to clone and install any of the defined packages.

The application was in the form of a CLI tool build with Python.

![CodeManager](https://raw.githubusercontent.com/palikar/code_manager/master/logo.png)

What I've learned during development
* python
* Automation

## --- Fcontrol ---
[Github Repository](https://github.com/palikar/fcontrol)

A short-lived project built with NodeJS that was able to log into my
Facebook account, intercepts every messenger message and dumps it to a
file on the filesystem. The idea was to have a huge database of all my
messages ever in a convenient form in files.

Turns out Facebook does not like it when you log in from a random JS
scripts and was locking my account when the script was running for a
while.

![FControl](https://raw.githubusercontent.com/palikar/dotfiles/master/screenshots/fcontrol_usage.png)

What I've learned during development
* JavaScript
* NodeJS

## --- My Dotfiles ---
[Github Repository](https://github.com/palikar/dotfiles)

This is a meta-project of sorts. When I was using Linux actively, I
was deep in the weeds with it. I was using a window manager, and
different small utilities to control stuff, and I was writing all of
my scripts myself, and I've spent probably too much time perfecting my
"Linux
Setup". These [Dotfiles](https://wiki.archlinux.org/title/Dotfiles)
are the entire configuration of my Linux system as well as my Emacs
configuration.

![Dotfiles](https://raw.githubusercontent.com/palikar/dotfiles/master/screenshots/work.png)

What I've learned during development
* Shell scripting
* Emacs lisp
* Doing things efficiently, Automation, Minimalism

## --- Projector ---
[Github Repository](https://github.com/palikar/projector)

A small Python CLI utility for creating project files and folder
structures from different templates. The idea was to be able to
quickly spin up a project (C++, python, Latex, among other templates)
and automate the whole folder copying from old projects I've been
usually doing.

![Projector](https://raw.githubusercontent.com/palikar/projector/master/demo_pic.png)

What I've learned during development
* python

## --- RabbitHoler ---
[Github Repository](https://github.com/palikar/rabbitholer)

At my job at [Fraunhofer](https://www.iosb.fraunhofer.de/en.html) we
were often using RabbitMQ (a message broker) for communication between
different systems. I picked up RabbitMQ at home and as a learning
exercise, I created RabbitHoler -- a simple CLI tool that lets you
quickly send or receive messages on a topic. The whole thing was
designed to be as CLI-friendly as possible so that one can pipe input
and output from and out of the tool as necessary.

<img width="1024px" src="/img/project_summary/rabbitholer_usage.png"
style="display: inline-block">

What I've learned during the development
* python
* RabbitMQ

## --- MFlower ---
[Github Repository](https://github.com/palikar/mflower)

A project that never really took off but for a week I was doing some
interesting for my stuff on it. MFlower was meant to be a
Tesnsorflow-type of automatic differentiation engine where one can
define some mathematical expression and the framework itself will
derive its derivative with respect to some parameter. I managed to get
the basics up and running (simple expression and derivative
evaluation) but never committed to this fully.

What I've learned during development
* C++

## --- CTGraph ---
[Github Repository](https://github.com/palikar/ctgraph)

![CTGraph logo](https://raw.githubusercontent.com/palikar/ctgraph/master/logo.png)

A fun little weekend project where I went full "contexpr all the
things". CTGraph is
a [graph](https://en.wikipedia.org/wiki/Graph_(discrete_mathematics))
that can be fully used at compile time. I even implemented different
algorithms that were able to be run at compile time with C++17. Most
of the project is implemented through `template` functions that expand
and compile time and do "some work" while doing so.

What I've learned during the development
* C++ 17
* C++ template metaprogramming

## --- Bringing Together Numerical Methods for Partial Differential Equation and Image Processing ---
[Github Repository](https://github.com/palikar/flow_predict)

This was part of a two-semester university course where we would learn
how to do actual scientific research. My project had to do with trying
to predict fluid flow from images encoding fluid speed and density. I
had to implement and evaluate a deep learning model that would take
one image as an input representing a step in a simulation and try to
predict the next step of the simulation, again represented as an
image. At the end of the project, we had to write scientific papers
describing our research.

The full paper can be
found
[here](https://github.com/palikar/flow_predict/blob/master/paper/paper.pdf).

![Flow Predict screenshot](https://raw.githubusercontent.com/palikar/flow_predict/master/paper/imgs/x_recursive_0_fluid_25.png)

What I've learned during the development
* python
* PyTorch
* large machine models handling, work with computer clusters,
  scientific writing

## --- Gosweeper ---
[Github Repository](https://github.com/palikar/gosweeper)

At some point, I wanted to get into the [Go language](https://go.dev/)
so I decided to recreate the mine sweeper game in it. The project is
nothing special, it was just an opportunity to learn a little bit of
Go programming.

![Sweeper screenshot](https://raw.githubusercontent.com/palikar/gosweeper/master/res/big.png)

What I've learned during the development
* Go

## --- Alisp ---
[Github Repository](https://github.com/palikar/alisp)

Alisp is my own Lisp-based programming language that I've spent half a
year developing. This has been one of my biggest projects and a huge
source of pride for me. During development, I dealt not only with the
language core runtime but also implement things like interpreters, CLI
utilities, different packages written in the language itself, s
standard library, testing system, documentation, and more. At its
peak, the source code of the project was in the neighborhood of
30KLoC.

<img width="502px" src="/img/project_summary/alisp_doc_2.png"
style="display: inline-block"> <img width="502px"
src="/img/project_summary/alisp_doc_1.png" style="display:
inline-block">

What I've learned during the development
* C++
* A huge part of the STD library
* Language design and implementation
* A whole lot of things about software development

## --- Anything ---
[Github Repository](https://github.com/palikar/anything)

*Anything* is my first attempt to create a big game engine where I can
experiment with different rendering techniques. I made a lot of
mistakes with respect to the general architecture of the engine but I
also learned a lot. The engine was written from scratch in C++ with
minimal use of third-party libraries. Most of my general knowledge
about graphics APIs (like OpenGL) comes from this project.

![Anyhting Screenshot](https://raw.githubusercontent.com/palikar/anything/master/screenshots/spheres_lighting.png)

What I've learned during development
* C++
* OpenGL
* A lot of fundamental rendering concepts


## --- Mission Control ---
See the [ DirectXer post]({{< ref "directxer.md" >}})

## --- CIBot ---
See the [ DirectXer post]({{< ref "directxer.md" >}})

## --- AssetBuilder ---
See the [ DirectXer post]({{< ref "directxer.md" >}})

## --- SceneChecker ---
See the [ DirectXer post]({{< ref "directxer.md" >}})

## --- PerfChecker ---
See the [ DirectXer post]({{< ref "directxer.md" >}})

