---
title: Jekyll 블로그 만들기 (Windows)
excerpt: "웹상의 여러 글들을 참고하여 이번에 Jekyll 블로그를 개설하면서 겪은 시행착오를 바탕으로 Jekyll로 블로그를 만드는 방법에 대하여 설명합니다."
last_modified_at: 2017-05-16 00:51:36

categories:
 - Jekyll
---

{% include nav_list nav="jekyll" %}

{% include toc %}

앞으로 블로그에 공부한 내용들을 정리를 해볼까하여 블로그에 대해 알아보게 되었습니다.
저의 경우 콘텐츠에 주로 수학이나 코드를 수록할 일이 많기때문에 다음과 같은 조건을 가지고 알아보았습니다.

1.	호스팅 비용 무료
2.	심플한 디자인
3.	코드 블록 하이라이트 지원
4.	수식 입력 지원
5.	카테고리별 분류 기능

알아보던 중 위의 조건에 적합한 블로그로 Jekyll을 사용하여 GitHub Pages로 호스팅하는 블로그를 개설하는 법에 대하여 찾아보았습니다. 웹상의 여러 글들을 참고하여 이번에 Jekyll 블로그를 개설하면서 겪은 시행착오를 바탕으로 Jekyll로 블로그를 만드는 방법에 대하여 설명합니다.
기본적으로 [Jekyll 설치하기](https://nesoy.github.io/articles/2016-12/Install-Jekyll) 의 내용과 같습니다.

## Jekyll 이란?

다음은 [Jekyll 공식 홈페이지](https://jekyllrb-ko.github.io/docs/home/)로부터의 설명입니다.

>Jekyll 은 아주 심플하고 블로그 지향적인 정적 사이트 생성기입니다. Jekyll 은 다양한 포맷의 원본 텍스트 파일을 템플릿 디렉토리로부터 읽어서, (Markdown 등의) 변환기와 Liquid 렌더러를 통해 가공하여, 당신이 즐겨 사용하는 웹 서버에 곧바로 게시할 수 있는, 완성된 정적 웹사이트를 만들어냅니다. 그리고 Jekyll 은 GitHub Pages 의 내부 엔진이기도 합니다. 다시 말해, Jekyll 을 사용하면 자신의 프로젝트 페이지나 블로그, 웹사이트를 무료로 GitHub 에 호스팅 할 수 있다는 뜻입니다.

현재의 웹환경은 다양한 반응형 웹들로 가득차 있지만 정작 일반인인 우리들에게는 그러한 기능이 많이 필요치 않습니다. 우린 그저 나만의 글을 나만의 저장소에 저장하고 살펴볼 수 있으면 좋으니까요. 분명 소통도 가능하다면 좋겠지요. 여기서 <a>정적</a>이란 말은 런타임시 아무런 변화가 일어나지 않음을 뜻합니다. 다시말하면, 웹환경에서의 정적이란 서버로부터 어떠한 요청에 의해 HTML을 생성하여 보여주는 방식이 아니라 이미 해당 페이지에 대하여 모든 HTML이 빌드가 되어 있어 이를 요청시 그저 보여주기만 한다는 뜻입니다.

## 블로그 개설 환경 구축

<dl>
	<dt>1.	블로그 개설 목표는 Jekyll을 활용하여 GitHub Pages로 호스팅을 하는 것입니다.</dt>
	<dd>부가적으로 테마는 현재 사용하고 있는 테마인 <a href="https://github.com/mmistakes/minimal-mistakes">Minimal-Mistakes</a>를 사용할 것입니다.</dd>
	<dt>2.	로컬 테스팅이 가능한 개발환경을 목표로 합니다.</dt>
	<dd>매번 결과물을 확인하기위해서 Git으로 push해서 확인하긴 어렵기 때문입니다. 기본적으로 <a>Git</a>으로 push 후 바로 되는 경우도 있지만 반영되기까지 어느 정도 시간이 걸릴 수 있습니다.</dd>
</dl>

블로그를 개설하기 위해서 필요한 어플리케이션들은 다음과 같습니다.

* Git 		 : GitHub에 올릴 것이므로 편한 Git 클라이언트를 사용하시면 됩니다. 본 글에서는 Console를 이용합니다.
* Python 	 : 웹쪽은 전문이 아니기때문에 잘 모르겠지만 Pip 관련해서 설치하는 것 같습니다.
* Ruby 		 : Jekyll의 기반이 되는 언어입니다.
* RubyDevkit : 경험해보니 Json 플러그인을 받을 때 네이티브 빌드를 위해 설치하는 것 같습니다.
* Jekyll 	 : Jekyll를 로컬에서 프리뷰 용도로 사용하기 위함입니다.
* Bundler 	 : Ruby에서 사용하는 패키지 관리자입니다.

## Git 설치

1.	[Git Homepage](https://git-scm.com/)로 이동하여 자신에게 맞는 OS환경에 맞는 버전을 받습니다.
2.	설치합니다.
3.	Global config를 설정합니다.

```
$ git config --global user.name "USER_NAME"
$ git config --global user.email "EMAIL"

// 저장된 내용을 리스트로 확인
$ git config --global --list
```

## Python 설치

1.	[Python 2.7.13 Installer](https://www.python.org/ftp/python/2.7.13/python-2.7.13.msi)을 받아서 실행합니다.
2.	설치 후 **시스템 환경변수 Path** 에 다음의 디렉토리를 추가시켜줍니다.
	*	C:\Python27
	*	C:\Python27\Scripts

{: .notice--info}
**Note:** Default 디렉토리 설정의 경우입니다.

## Ruby 설치

1.	[Ruby Installer(x64)](https://dl.bintray.com/oneclick/rubyinstaller/rubyinstaller-2.3.3-x64.exe)를 받아서 실행합니다.
2.	설치중 `Add Ruby executables to your PATH` 옵션을 활성화시켜줍니다.
3.	[RubyDevkit](https://dl.bintray.com/oneclick/rubyinstaller/DevKit-mingw64-64-4.7.2-20130224-1432-sfx.exe)를 받아서 `C:\RubyDevkit`에 압축을 풉니다.
4.	다음과 같은 명령어를 입력합니다.

```
$ ruby dk.rb init
[INFO] found RubyInstaller v2.3.3 at C:/Ruby23-x64

Initialization complete! Please review and modify the auto-gener
'config.yml' file to ensure it contains the root directories to
of the installed Rubies you want enhanced by the DevKit.
$ ruby dk.rb install
[INFO] Updating convenience notice gem override for 'C:/Ruby23-x
[INFO] Installing 'C:/Ruby23-x64/lib/ruby/site_ruby/devkit.rb'
```

{: .notice--info}
**Note:** Devkit 디렉토리는 원하는 곳으로 해도 무방합니다.

## Jekyll 설치

```
$ gem install bundler
$ gem install jekyll
```

## 테마 적용

1.	[Minimal-Mistakes]("https://github.com/mmistakes/minimal-mistakes") 테마를 fork 하거나 zip으로 받습니다.
2.	자신에 맞게 `_config.yml` 파일을 수정합니다.
3.	`bundle install`을 입력하여 관련된 패키지를 설치합니다.
4.	`jekyll s`를 입력하여 로컬에서 테스트를 해볼 수 있습니다. (port: 4000)

{: .notice--info }
**Note:** [Minimal-Mistakes Quick start guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)에 가시면 상세한 정보를 얻으실 수 있습니다.

## References

-	[Jekyll](https://jekyllrb-ko.github.io/docs/home/)
-	[Jekyll 설치하기](https://nesoy.github.io/articles/2016-12/Install-Jekyll)
-	[Jekyll Document](https://jekyllrb.com/docs/home/)
-	[Minimal-Mistakes Quick start guide](https://mmistakes.github.io/minimal-mistakes/docs/quick-start-guide/)

*[HTML]: Hyper Text Markup Language