---
title				: Dependency management
excerpt				: "Brief talk about dependency management in C++"
last_modified_at	: 2019-04-30

toc 				: true
toc_sticky			: false

categories:
 - Game engine
---

{: .notice--info}
**NOTICE:** I'm junior developer. Thus content may be inaccurate.

First things first. Let's setup project

## Create repository

1. Make a repository with nice engine name.
2. Shoping appropriate .gitignore from [Git Ignore Template](https://github.com/github/gitignore)

Now you have clean start repository!

## Brief talk about dependency management

On linux, there is no problem. But when you work with third party libraries on Windows system.
Because there is no package manaer like pacman, apt, npm.
It is very hard to manage all third party dependencies by hand.
I introduce some techniques available.

**NuGet package**

This tool is handy when you work with Visual studio. 
But I gonna use CMake and also it is not avilable on other operating systems.

**Git submodule**

[Git Submodule](https://git-scm.com/docs/git-submodule) is subtool of git. And we can leverage this git submodule as long as third party library is available on git.
And also it doesn't space your git repository. It creates kind of symlink to target repository.
One problem is that we should build library by hand.

**Vcpkg**

[Vcpkg](https://github.com/microsoft/vcpkg) is cross platform package manager by Microsoft. 
It automatically build requested library. It is also open source and sources are on git.
One problem is not every git repository is registered to vcpkg.

**So which one should we use?**
We mix git submodule and vcpkg!
Most of third party libraries are available on the vcpkg.
Next step will show you how to manage dependencies with CMake.

I found this clever idea from [Bootstrapping a vcpkg-based cmake project in Visual Studio](http://cpptruths.blogspot.com/2019/03/bootstrapping-vcpkg-based-cmake-project.html).
I recommend check it out.

## First CMakeLists

```bash
# Minimum engine development environment
# CPU Architecture : x64 
# Platform         : Windows 8 above, Linux
# CMake            : 3.12.4 above
# Git              : Required

# Check minimum version of cmake
# To use vcpkg, 3.12.4 or higher version of cmake is required.
# See https://github.com/Microsoft/vcpkg
cmake_minimum_required(VERSION 3.12.4)

# CMake modules
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/CMake)

include(FindVcpkg) # Vcpkg !Important: It should be placed before project()
include(CheckDependencies) # Module to check third party denpencies

# Top-level project
set(MAIN_PROJECT_NAME Astro)
project(${MAIN_PROJECT_NAME} C CXX)

# Global properties
set(ENGINE_INCLUDE_DIR 
    ${CMAKE_CURRENT_SOURCE_DIR}/Source/Runtime
    ${CMAKE_CURRENT_SOURCE_DIR}/Source/Runtime/Core
    ${CMAKE_CURRENT_SOURCE_DIR}/Source/ThirdParty
    )

set(CMAKE_RUNTIME_OUTPUT_DIRECTORY ../Binaries)
set(CMAKE_ARCHIVE_OUTPUT_DIRECTORY ../Binaries)
set(CMAKE_LIBRARY_OUTPUT_DIRECTORY ../Binaries)

# Generates projects
message(STATUS "Generates runtime project")
add_subdirectory(Source/Runtime Engine)
```

This is typical CMakeLists for top-level project. The important part is including custom cmake modules.

```bash
# CMake modules
list(APPEND CMAKE_MODULE_PATH ${CMAKE_CURRENT_SOURCE_DIR}/CMake)

include(FindVcpkg) # Vcpkg !Important: It should be placed before project()
include(CheckDependencies) # Module to check third party denpencies
```

FindVcpkg and CheckDependencies are custom modules modified from [Bootstrapping a vcpkg-based cmake project in Visual Studio](http://cpptruths.blogspot.com/2019/03/bootstrapping-vcpkg-based-cmake-project.html).

Usage this script is like this.

```bash
set(FOO_PROJECT_NAME FOO)
project(${FOO_PROJECT_NAME} C CXX)

# Add required dependencies
set(FOO_DEPENDENCIES
    celero
    )

# check_depencies is function included in CheckDependencies
check_dependcies(${FOO_DEPENDENCIES})

find_package(celero REQUIRED)

# Helper macro to produce single executable for each benchmark
add_executable(${FOO_PROJECT_NAME} ${FOO_HEADER} ${FOO_SOURCE})

target_link_libraries(${FOO_PROJECT_NAME}
                        PRIVATE 
                        ${FOO_DEPENDENCIES}
                        )
```

{: .notice--warning}
**IMPORTANT!** You should use [tool chain file provided from vcpkg](https://github.com/microsoft/vcpkg/blob/master/docs/examples/installing-and-using-packages.md#cmake)

We gonna stick to this strategy until the dependent package is not available on [Vcpkg](https://github.com/microsoft/vcpkg).

## References

- [Git Submodule](https://git-scm.com/docs/git-submodule)
- [Vcpkg](https://github.com/microsoft/vcpkg)
- [Bootstrapping a vcpkg-based cmake project in Visual Studio](http://cpptruths.blogspot.com/2019/03/bootstrapping-vcpkg-based-cmake-project.html).