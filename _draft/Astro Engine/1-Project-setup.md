---
title				: 프로젝트 설정
excerpt				: "Setup the project for a game engine"
last_modified_at	: 2019-04-29

toc 				: true
toc_sticky			: true

categories:
 - Astro
 - Engine
---

## 개발환경

각자 원하는 에디터와 컴파일러 등을 사용하면 되지만 궁금한 이들을 위해 필자의 개발환경을 적어둔다.

- OS                  : Windows(major)
- Text Editor         : VSCode
- Unit Test Framework : Catch2
- Package Manager     : Git submodule

3rd Party 관리를 Git submodule 과 CMake를 사용하여 관리한다.

## Git repository 생성

1. 원하는 곳에 Repository를 생성하여 클론한다.
2. gitignore 항목과 License 항목을 작성한다.
3. README 파일도 만들어 두면 좋다.

## Project structure layout

- Build          : CMake가 생성하는 프로젝트 파일을 담아둔다.
- Engine         : 엔진 라이브러리 프로젝트 
- Tests          : 유닛 테스트 프로젝트
- .gitIgnore     : Git 무시 목록
- CMakeLists.txt : 메인 CMake project file
- LICENSE        : 라이센스 명시

## 빌드 테스트

먼저 빌드가 되는 환경을 구축하기 위해서 간단한 테스트 코드를 작성한다.
Tests/Source에 Factorial.cpp 를 작성해본다.
Catch2의 샘플을 가져왔다.

''cpp
#define CATCH_CONFIG_MAIN  // This tells Catch to provide a main() - only do this in one cpp file
#include "Catch2/single_include/catch2/catch.hpp"

unsigned int Factorial( unsigned int number ) {
    return number <= 1 ? number : Factorial(number-1)*number;
}

TEST_CASE( "Factorials are computed", "[factorial]" ) {
    REQUIRE( Factorial(1) == 1 );
    REQUIRE( Factorial(2) == 2 );
    REQUIRE( Factorial(3) == 6 );
    REQUIRE( Factorial(10) == 3628800 );
}
''

아직 Catch2 Header를 받지 않았기 때문에 빌드되진 않는다.

1. Tests/Source/ThirdParty 에 Catch2 를 Git submodule 로 추가해준다.

''bash
git submodule add https://github.com/catchorg/Catch2.git Tests/Source/ThirdParty
''

추가가 되면 다음과 같은 .gitmoudles 파일이 생성되어 있을 것이다.

''txt
[submodule "Tests/Source/ThirdParty/Catch2"]
	path = Tests/Source/ThirdParty/Catch2
	url = https://github.com/catchorg/Catch2.git
``

Include 를 간략화하기 위해서 타겟에 ThirdParty 디렉토리를 추가해준다.

''cmake
set(TEST_SOURCE_DIR ${ASTRO_ROOT_DIR}/Tests/Source)

add_executable(${TEST_PROJECT_NAME} ${TEST_HEADER} ${TEST_SOURCE})
target_link_libraries(${TEST_PROJECT_NAME} Astro)
target_include_directories(${TEST_PROJECT_NAME} 
                           PRIVATE ${ASTRO_ENGINE_SOURCE_DIR}
                           PRIVATE ${TEST_SOURCE_DIR}/ThirdParty)
''