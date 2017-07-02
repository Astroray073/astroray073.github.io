---
title: "3 String Manipulation, Guess and Check, Approximation, Bisection"
excerpt: "Learning about vairous techniques to solve problems"
last_modified_at: 2017-06-21 16:35:11
mathjax: true
sidebar:
 nav: "ocw_6_0001"
---

{% include video id="SE4P7IVCunE" provider="youtube" %}

## Lecture Materials

-	[Lecture Note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/lecture-slides-code/MIT6_0001F16_Lec3.pdf)
-	[Quiz](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/in-class-questions-and-video-solutions/lecture-3/)

{% include toc %}

## String Manipulation

### Indexer

```python
s = "abc"
len(s) # evaluates to 3

s[-1] # c
s[-2] # b
s[-3] # a
```

### Substring

We can get substring by using syntax [start:stop:step]. `Step`'s default value is 1.

```python
s = "abcdefgh"

s[3:6] # "def"
s[::-1] # "hgfedcba"
```

### Immutability

Strings are immutable. `s[0] = 'y'` is not allowed.

## Guess and Check

Exhausting iteration method. Iterating all possiblity to get the answer.

```python
cube = 8
for guess in range(cube+1):
	if guess**3 >= abs(cube):
		break
	if guess**3 != abs(cube):
		print(cube, "is not a perfect cube!")
	else:
		if cube < 0:
			guess = -guess
		print("Cube root of " + str(cube) + " is " + str(guess))
```

## Approximation

Getting good enough solution. The key is setting up reasonable epsilon and increment per each steps.

```python
cube = 27
epsilon = 0.01
guess = 0.0
increment = 0.0001
num_guesses = 0

while abs(guess**3 - cube) >= epsilon:
	guess += increment
	num_gess += 1
	print("num_guesses =", num_guesses)
	if abs(guess**3 - cube) >= epsilon:
		print("Failed on cube root of", cube)
	else:
		print(guess, "is close to the cube root of", cube);
```

## Bisection

Searches the answer by halving the search area. Time complexity of this algorithm for searching the answer is $O(\log{N})$.

```python
cube = 27
epsilon = 0.01
num_guesses = 0
low = 0
high = cube
guess = (high + low) / 2.0

while abs(guess**3 - cube) >= epsilon:
	if guess**3 < cube:
		low = guess
	else:
		high = guess
	guess = (high + low) / 2.0
	num_guesses += 1
print("num_guesses = ", num_guesses)
print(guess, "is close to the cube root of", cube)
```