---
title				: 프로젝트 개요
excerpt				: "Setup the project for a game engine"
last_modified_at	: 2019-04-28

toc 				: true
toc_sticky			: true

categories:
 - Astro
 - Engine
---

## 프로젝트 소개

**엔진 스펙**

- 타겟 플랫폼 : Windows, Linux, Android
- 개발 언어   : C++

**개발 환경**

- OS : Windows 10, Arch linux
- Development process : Test driven development
- Source Control : Git (hosted by Github)
- Unit Test Framework : Catch2
- Make : CMake
- Compiler : MSVC, clang/LLVM

**개발 목적**

게임 엔진에 대한 이해도를 높이고 다양한 개발 문제에 대하여 대처할 수 있는 능력을 기르기 위하여 개발하였다.

## 엔진 레이어

일반적인 게임 엔진의 구조를 최대한 간추리면 다음과 같다.

-----------------------------------------
|                  Game                 |
|           Gameplay Foundation         |
|                 Engine                |
|              Core Systems             |
|   PAL(Platform Abstraction Layer)     |
|           3rd Party Library           |
|                   OS                  |
-----------------------------------------

**OS Layer**

좀 더 세분화하자면 하드웨어와 드라이버 그리고 OS 종속적인 SDK들이 있다.
OS에 따라 사용할 수 있는 컴파일러를 선정하고 이를 고려해야한다.
더 자세한 내용은 **PAL Layer**에서 다룬다.

**3rd Party Library**

DRY(Don't repeat yourself)의 원칙에 따라 엔진을 개발할 때에는 다른 개발자의 작업을 사용하는 것이 바람직하다.
엔진의 개발에 필요한 기능은 매우 다양하고 분야별로 파고들어가면 끝도 없기 때문이다.
이를 보완하고 개발 속도를 높이기 위하여 [Open source Project]들을 도입할 것이다.
라이브러리 선정의 중요한 점은 다음의 세가지다.

1. 크로스 플랫폼을 지원하기 위해 다른 OS에서 빌드가 가능한가?
2. 꾸준히 관리되어 왔는가? 
3. 시스템의 안정성이 확보되어 있는가?

다음은 각 분야별 C++ 라이브러리 및 프레임워크 목록이다.
OS 종속적인 라이브러리의 경우에는 괄호로 표기하였다.

- General : Boost
- Graphycs : SDL/SDL2[0], OpenGL, DirectX[1]
- Physics : Box2D, PhysX, Bullet, ...
- Unit Test Framework : xUnit series, Google Test, Boost.Test, Catch, ...

[0] C Library
[1] Windows dependant.

**PAL**

Platform Abstraction Layer로 혹은 정확히는 같은 의미는 아니지만 HAL(Hardware abstraction layer)를 포함한다.
기본적인 구조는 각 OS에 공통적인 기능들을 추상화하여 인터페이스로 노출하고 Preprocessor를 통하여 이를 제어한다.

1. [Platform detection via Preprocessor](https://blog.kowalczyk.info/article/j/guide-to-predefined-macros-in-c-compilers-gcc-clang-msvc-etc..html)

컴파일러 마다 OS에 기본적으로 define들을 검사하여 플랫폼을 결정한다.

''cpp
// --------------- Platform detection --------------- //
#ifdef _WIN64
	#define PLATFORM_WINDOWS
#endif

#ifdef __gnu_linux__
    #define PLATFORM_LINUX
#endif

#ifdef __ANDROID__
    #define PLATFORM_ANDROID
#endif
''

2. Includes platform dependent header files ex) windows.h

1에서 검출된 플랫폼에 따라 해당되는 플랫폼의 종속적인 라이브러리를 프로젝트에 포함한다.

3. Abstraction

2에서 포함한 라이브러리에 대하여 엔진에 필요한 기능을 추상화한 인터페이스를 정의하고 OS에 종속적인 모든 기능은 이를 통하여 사용한다.

필요한 세부적인 기능들을 대략적으로 살펴보면 다음과 같다.

- Platform detection
- Data type definition
- Collections
- Algorithm
- File system
- High resolution timer
- Threading
- Low level Graphics(GDIs) : 주로 OpenGL과 DirectX를 추상화한 랩핑작업을 한다. 
- Physics : 주로 3rd Party 라이브러리를 랩핑한다.

**Core Systems**

주 역할은 엔진에 필수적인 기능과 3rd Party library의 추상화이다.

- Assertion, Debugging and logging
- Math : Linear algebra 가 가장 핵심적인 기능이다.
- Unit Testing
- Memory Allocation
- String
- Guid
- Serialization
- RNG (Random number generator)
- Parsers : XML, Json, CSV, ...
- Asset management
- Module management

**Engine**

- GUI, HUD
- IO handling
- Profiling
- Audio
- Animation
- GDI interface

**Gameplay Foundation**

엔진에 대한 아키텍쳐에 따른 게임플레이 제작에 필요한 기능들이 들어간다.
현재 많이 사용하는 게임 엔진 아키텍쳐의 종류로는 Component based system 과 Entity Component System가 있다.

- Scripting system
- High level funtionalities for games
- Camera
- Physics API
- AI

**Game**

사용자가 엔진을 사용하여 그 위에 게임을 제작한다.