---
title: "Problem Set 0"
excerpt: "Solving problem set 0"
last_modified_at: 2017-05-21 16:54:31
sidebar:
 nav: "ocw_6_0001"
---

{% include toc %}

## Spyder 설치

[Spyder 설치](/2017-05-21-Archlinux-spyder/)를 참고해주세요.

강의에 사용되는 python 패키지들을 추가적으로 설치합니다.

```bash
# sudo pip install numpy
# sudo pip install matplotlib
```

## Problem

[Problem Download](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/assignments/ps0.zip)

Write a program that does the following in order:

1. Asks the user to enter a number “x”
2. Asks the user to enter a number “y”
3. Prints out number “x”, raised to the power “y”.
4. Prints out the log (base 2) of “x”.

## Solve

`Python`은 처음 사용해보는데 한가지 특이한 점이 있다면,

1.	`;`을 안쳐도 된다는 점.
2.	타입을 지정을 안한다는 점.

이 두가지가 눈에 띄는 특징인 것 같다. 문제에 관한 풀이는 기본적인 것으로 중요한 내용은 없다.

```python
import math;

x = input("Enter number x: ");
y = input("Enter number y: ");

print("X**y = ", float(x)**float(y));
print("log(x) = ", math.log2(float(x)));
```

{: notice--info}
**Note:** `input` 함수의 리턴값은 `string`이기때문에 이를 숫자로 사용할 때 `캐스팅`을 해주어야한다.

## References

-	Guttag, John. Introduction to Computation and Programming Using Python: With Application to Understanding Data Second Edition. MIT Press, 2016. ISBN: 9780262529624.