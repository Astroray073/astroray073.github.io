---
title				: Introduction to game engine development
excerpt				: "First article about game engine development"
last_modified_at	: 2019-04-28

toc 				: true
toc_sticky			: false

categories:
 - Game engine
---

{: .notice--info}
**NOTICE:** I'm junior developer. Thus content may be inaccurate.

## Motivation

As game developer, there is the tempting moment to dream about developing own game engine.
But a lot of peopel says **"Don't make the wheel again" and that is very true!**
There are plenty of production level game engines out there such as Unreal 4, Unity, Orge ... and so on.

Even though why making own game engine? When I develop a game with a game engine. A lot of questions come up and doesn't go away.
How they build to various platform? What about memory handling? How they make such a fluent UI Frameworks?
I want deep understanding the voodoo magics behind the scene.

So the motivation are...

- I want to know how game engine works.
- Studying various aspects about game engine makes me better developer.
- Test myself how far I can handle complex system.
- Improving the reading ability to understand other people's code.
- Cross platform development experience.
- Acknowledge low-level systems to make better high-level experience.
- And of course, for fun.

## Game engine architecture

Before starting this journey, Let's figure out basic game engine architecture.
I've already do some research. Simple modified version of game engine architecture looks like this.

|                  Game                 | Product built on top from engine      |
|           Gameplay Foundation         | Engine Paradigm. CBS, ECS...          |
|                 Engine                | High-level support                    |
|              Core Systems             | Low-level support systems             |
|   PAL(Platform Abstraction Layer)     | Platform indepent layer               |
|           3rd Party Library           | Libraries to boost our development    |
|                   OS                  | Platform dependent library            |

This structure is very simplified version. To know about more details please see [the reference](#references).

### OS Layer

OS Layer consists of platform(Windows, Linux, OSX...) dependent code.
To make cross platform system, we cannot use directly this code bases.
We need to warp these functionalites to use in the engine system.
That's why PAL exists.

*[PAL]: Platform Abstraction Layer

### 3rd Party Library

We cannot build Everything. There are plenty open source projects to make our life easy.
We gonna make our own system but also utilize other projects. So the question comes out. "Build by hand or bring other library?"

First, We avoid to platform specific techniques as much as possible.
But when these technique is important then we gonna import that library.
For example, We cannot and will not make graphics library such as OpenGL.

Second, if the required feature is important to understand the engine archtecture, then we gonna make it.
We will make custom memory management system which can boost the performance but not too fancy.

In conclusion, we should make a choice to build such a system or not in the development process.

### PAL (Platform Abstract Layer)

PAL is all about the Multiplatform compilation. The basic process is as below.

- Defines features to work with OS.

This includes memory management, string, filesystem, process and so on.

- Defines common functionality across platforms.

Defines plaform independent features. It is usaualy standard c library functionality used in OS.
You can find about deatils on [Unreal Engine's generic platfom](https://github.com/EpicGames/UnrealEngine/tree/release/Engine/Source/Runtime/Core/Public/GenericPlatform).

- Defines platfom specific features which we need.

Make interfaces to communicate OS.
The interface will call platform dependent function or common c library function to do the job.

- Includes only needed headers via predefined preprocessor macros.

### Core systems

Core systems is collection of general purpose componenets to build development environment such as memory management, math, containers, etc.
We gonna make `most of this part  by ourself.

### Engine

Game Engine is collection of tools to assist the game development process.
Major categories of Engine parts are Resource management system, Graphics, Physics, Audio, Animation, Game components and ton of them.
Every single part is very huge to deal with. So we gonna aggressively import other 3rd party frameworks.

### Gameplay Foundation

This part is where game engine paradigm comes. Most widely using game engine paradigms are Component Based System and Entity-Component-System.
CBS is the most governing paradigm in game industry. CBS defines peice of functionality as Component and attach Components to the object called Game object.
It prefers Composition to Inheritance.

ECS is more data-driven development paradigm. Entity is collection of Components. Component in ECS doesn't have any feature. 
It is pure data structure. The features will be handled by the Systems.

I worked with CBS based engines like Unreal and Unity.
Actually Unity is going to move its system to ECS. Anyway, because I have no experience dealing with ECS I will take a chance to develop it.

*[CBS]: Component Based System
*[ECS]: Entity Component System

## Engine specification

We briefly look around the architecture of game engine. Now it is the time to set our scope.

- Development platform  : Windows, Linux
- Build target platform : Windows, Linux, Android(Optional)
- Language              : C++

**Development environment**

- OS                    : Windows 10, Arch linux
- CPU Architecture      : x64, ARM64(Optional)
- Development process   : Test driven development
- Source Control        : Git (hosted by Github)
- Unit Test Framework   : Catch2
- Make                  : CMake
- Compiler              : MSVC, clang/LLVM

## References

- [Game Engine Architecture](https://www.gameenginebook.com/)
- [Unreal Engine](https://github.com/EpicGames/UnrealEngine)