---
title: "4 Decomposition, Abstraction and Functions"
excerpt: ""
last_modified_at: 2017-07-02 08:55:57
mathjax: true
sidebar:
 nav: "ocw_6_0001"
---

{% include video id="MjbuarJ7SE0" provider="youtube" %}

## Lecture Materials

-	[Lecture Note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/lecture-slides-code/MIT6_0001F16_Lec4.pdf)
-	[Quiz](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/in-class-questions-and-video-solutions/lecture-4/)

{% include toc %}

## Abstraction

**Abstraction** is hiding details. Because we don't need to know how sommething works to use it.

-	cannot see details
-	do not need to see details
-	do not want to see details
-	hide tedious coding details

## Decomposition

**Decomposition** is that different segments works together to get the result.

-	are **self-contained**
-	used to **break up** code
-	**reusable**
-	**organized**
-	**coherenent**

## Functions

**Functions** is code chunk called or invoked in a program

-	name
-	parameters
-	docstring
-	body
-	returns

```python
def is_even(i):
	"""
	input: i, a positive int
	Returns True if i is even, otherwise False
	"""
	print("inside is even")
	return i % 2 == 0

is_even(3) # invoke function
```

## Scope

**Scope** is separate environment from a program.

```python
def f(x):
	x = x + 1
	return x

x = 3
z = f(x)
```

|Global scope|f(x) scope|
|f = some code|x = 3|
|x = 3|x = 4|
|z = x as 4| |