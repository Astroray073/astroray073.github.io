---
title: Jekyll 블로그 만들기 (Windows)
description: "앞으로 블로그에 공부한 내용들을 정리를 해볼까하여 블로그에 대해 알아보게 되었습니다. 저의 경우 주로 기술적인 문서(특히 코드)를 작업할 예정이므로 다음과 같은 조건을 가지고 알아보았습니다. 알아보던 중 위의 조건에 적합한 블로그로 Jekyll을 사용하여 GitHub Pages로 호스팅하는 블로그를 개설하는 법에 대하여 찾아보았습니다. 웹상의 여러 글들을 참고하여 이번에 개설하면서 겪은 시행착오를 바탕으로 Jekyll로 블로그를 만드는 방법에 대하여 설명합니다."
categories:
 - Jekyll
tags:
 - Jekyll
---

앞으로 블로그에 공부한 내용들을 정리를 해볼까하여 블로그에 대해 알아보게 되었습니다.
저의 경우 콘텐츠에 주로 수학이나 코드를 수록할 일이 많기때문에 다음과 같은 조건을 가지고 알아보았습니다.

1.	호스팅 비용 무료
2.	심플한 디자인
3.	코드 블록 하이라이트 지원
4.	수식 입력 지원
5.	<del>카테고리별 분류 기능</del>[^1]

알아보던 중 위의 조건에 적합한 블로그로 Jekyll을 사용하여 GitHub Pages로 호스팅하는 블로그를 개설하는 법에 대하여 찾아보았습니다. 웹상의 여러 글들을 참고하여 이번에 개설하면서 겪은 시행착오를 바탕으로 Jekyll로 블로그를 만드는 방법에 대하여 설명합니다.
기본적으로 [Jekyll 설치하기](https://nesoy.github.io/articles/2016-12/Install-Jekyll) 의 내용과 같습니다.

## 블로그 개설 환경 구축

Jekyll을 활용하여 GitHub로 호스팅을 할 것이고, 테마는 Lanyon 기반으로 된 Lanyon-plus 테마를 사용할 것 입니다.
이 둘의 가장 큰 차이점은 Lanyon-plus 의 경우 Jekyll 3.0 이상 버전을 지원한다는 점입니다.
블로그 개설만을 위한다면 더 쉬운 방법이 있으나 테마를 사용하고 로컬에서 프리뷰가 필요하다면 추가적으로 개발 환경의 구축이 필요합니다.
블로그를 개설하기 위해서 필요한 어플리케이션들은 다음과 같습니다.

* Python : pip 관련해서 설치하는 것 같은데 웹쪽은 전문이 아니기때문에 왜 설치하는 지는 잘 모르겠습니다.
* Ruby : Jekyll의 기반이 되는 언어입니다.
* RubyDevkit : Lanyon-plus 테마의 종속 패키지를 설치시 필요합니다.
* Jekyll : Jekyll를 로컬에서 프리뷰 용도로 사용하기 위함입니다.

### Python 설치

1.	[Python 2.7.13 Installer](https://www.python.org/ftp/python/2.7.13/python-2.7.13.msi)을 받아서 실행합니다.
2.	설치 후 **시스템 환경변수 Path** 에 다음의 디렉토리를 추가시켜줍니다. (Default 디렉토리 설정의 경우)
	*	C:\Python27
	*	C:\Python27\Scripts

### Ruby 설치

1.	[Ruby Installer(x64)](https://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.3.3-x64.exe)를 받아서 실행합니다.
2.	설치중 `Add Ruby executables to your PATH` 옵션을 활성화시켜줍니다.
3.	[RubyDevkit](https://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe)를 받아서 `C:\RubyDevkit`에 압축을 풉니다.[^2]
4.	Command prompt를 열어 다음과 같은 명령어를 입력합니다.

~~~
C:\rubydevkit> ruby dk.rb init
[INFO] found RubyInstaller v2.3.3 at C:/Ruby23-x64

Initialization complete! Please review and modify the auto-gener
'config.yml' file to ensure it contains the root directories to
of the installed Rubies you want enhanced by the DevKit.
C:\rubydevkit> ruby dk.rb install
[INFO] Updating convenience notice gem override for 'C:/Ruby23-x
[INFO] Installing 'C:/Ruby23-x64/lib/ruby/site_ruby/devkit.rb'
~~~

### Jekyll 설정
1.	Command prompt에서 `gem install bundler`를 입력하여 bundler 패키지를 설치합니다.
	bundler는 루비에서의 패키지 관리자입니다.
2.	Command prompt에서 `gem install jekyll`을 입력하여 jekyll을 설치합니다.

### 테마 적용
1.	[Lanyon-plus](https://github.com/dyndna/lanyon-plus) 테마를 clone 하거나 zip으로 받습니다.
2.	자신에 맞게 `_config.yml` 파일을 수정합니다.[^3]
3.	Command prompt에서 블로그 DIRECTORY에 이동하여 `bundle install`을 입력하여 관련된 패키지를 설치합니다.
4.	`bundle exec jekyll s`를 입력하여 로컬에서 테스트를 해볼 수 있습니다.[^4]

#### 다음글에서는 테마를 로컬에서 커스터마이징하고 웹에 올려서 확인해보도록 하겠습니다.

### References
1.	[Jekyll 설치하기](https://nesoy.github.io/articles/2016-12/Install-Jekyll)
2.	[Jekyll Document](https://jekyllrb.com/docs/home/)
3.	[Lanyon plus theme](https://github.com/dyndna/lanyon-plus)

### Comments

[^1]: 결국 커스터마이징을 통해서 해결했습니다.
[^2]: 디렉토리는 원하는 곳에 설치해도 무방합니다.
[^3]: 가장 중요한건 `url`, `baseurl`, `urlimg` 이 세가지 항목에 대해서 수정해야 웹사이트 빌드가 가능합니다.
[^4]: 기본값은 `http://localhost:4000` 입니다.

*[Jekyll]: Jekyll이란 정적 사이트 생성기로 현재 GitHub내에서 GitHub Pages의 웹페이지 생성기로 사용하고 있습니다. (2017-05 기준)