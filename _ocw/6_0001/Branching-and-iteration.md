---
title: "2\\. Branching and Iteration"
excerpt: ""
last_modified_at: 2017-05-23 17:48:31
mathjax: true
sidebar:
 nav: "ocw_6_0001"
---

{% include video id="0jljZRnHwOI" provider="youtube" %}

## Lecture Materials

[Lecture Note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/lecture-slides-code/MIT6_0001F16_Lec2.pdf)

{% include toc %}

## String

`String` is a sequence of characters.

```python
# Assignment
hi = "hello there"

# Concatenate
name = "ana"
greet = hi + name # hello thereana
greeting = hi + " " + name # hello there ana
silly = hi + " " + name * 3 # hi anaanaana
```

## print

```python
print("Message: ", value) # Message: value
```

## input

The type of return value of input function is string.

```python
intValue = int(input("x = ")) # This way can get the value whose type is what we want.
```

## Flow control

The indentation is important!

### if

```python
if <condition>:
	<expression>
elseif: <condition>:
	<expression>
else:
	<expression>
```

### while

```python
while <condition>:
	<expression>
```

### for

```python
# range(start, stop, step)
for n in range(5):
	<expression>
```
