---
title               : "Spyder 설치"
excerpt             : "ArchLinux에서 Python IDE인 Spyder를 설치하는 방법입니다."
last_modified_at    : 2017-05-21 16:08:03

toc 				: true
toc_sticky			: true

categories:
 - Python
---

ArchLinux에서 Python IDE인 `Spyder`를 설치하는 방법입니다.

## pip 설치

`Python` 패키지 관리자인 `pip`을 설치합니다.

```
# sudo pacman -S python-pip
```

## Spyder 종속 패키지 설치

`Spyder`만 설치할 경우 실행이 되지 않습니다. PyQt5가 종속 패키지인데 자동으로 찾아주지 않습니다.

```
# sudo pip install pyqt5
# sudo pip install spyder
```

설치가 끝나면 앱 아이콘이나 `spyder3` 명령어를 통해 실행할 수 있습니다.