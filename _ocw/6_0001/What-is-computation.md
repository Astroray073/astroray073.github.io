---
title: "What is Computation?"
excerpt: "The computer is a machine to help people to calculate something. A Computer can calculate and memorize a lot of things beyond the human ability."
last_modified_at: 2017-05-17 08:25:20
mathjax: true
sidebar:
 nav: "ocw_6_0001"
---

{% include video id="ytpJdnlu9ug" provider="youtube" %}

## Lecture Materials

[Lecture Note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/lecture-slides-code/MIT6_0001F16_Lec1.pdf)

{% include toc %}

## Introduction

The computer is a machine to help people to calculate something. A Computer can calculate and memorize a lot of things beyond the human ability.

But the important thing is

>Computer can do what people say to do.

That is the reason why programmers exists today. Computer do nothing without a programmer. In these days, some people may argue about the technology of meta-programming or artificial intelligence but the all of these are implemented to the hardware by human.

<!--more-->

## Types of knowledge

We can solve a problem using computer. To do so, we should know about the two types of knowledge.

*	<a>Declarative knowledge</a>: The truth for some problem.
*	<a>Imperative knowledge</a>: How to solve a problem.

**Declarative knowledge** is the truth that we can use solving a problem.
**Imperative knowledge** is the description how to solve a problem with the Decalartive knowledge.

{: .notice--info}
**Note:** Dr.Ana shows very fun example using python. Here is the code below.

```python
import random
random.randint(16, 272)
```

If we have the truth $y^2 = x$ (obviously!) and try to solve $y$ where $y = 16$.
Following **Imperative Knowledge** is

1.	Guess $g$.
2.	If $g^2$ is close enough to $x$, then stop and choose $g$ as the answer.
3.	If not, choose the next guess as the average of $g$ and $x/g$.
4.	Using the new guess, iterates until the condition 2 is satisfied.

|$g$|$g^2$|$x/g$|$(g + x/g)/2$|
|---|---|---|---|
|3|9|16/3|4.17|
|4.17|17.36|3.837|4.0035|
|4.0035|16.0027|3.997|4.000002|

{: .notice--info}
**Note:** Can be proved by using [Newton's method](https://en.wikipedia.org/wiki/Newton%27s_method).

We generally call this kind of Imperative Knowledge as <a>Algorithm</a>

Let's try to define what **algorithm** is
<br>
By controlling the flow of instructions, decide when to finish the task to get the answer of a problem.

## Two types of computer

*	Fixed program computer : Only do one thing `e.g. a simple calculator`
*	Stored program : Sequence of instructions -> do a lot of tasks. `e.g. Today's computer`

## Basic machine architecture

![Basic machine architecture]({{ site.url }}{{ site.imgurl }}OCW/6_0001/bma.png){: .align-center}

<a>Memory</a> contains data & sequence of <ins>primitive</ins> instructions.

1. Program counter starts to execute the sequence of primitive instructions in order.
2. During the execution if some instruction has a task, then it passes the instruction to ALU.
3. When the seqeunce of instruction is finished, the computer emits the output.

>Turning suggested that only 6 instructions are enough to compute anything. Those are 'Move left', 'Move right', 'Read", 'Write", 'Scan' and 'Do nothing'

That results in that if something can be computed in a particular language then other languages can do the same thing.

## Aspects of languages

1.	<a>Syntactically valid</a> : Phrases should be correctly.
2.	<a>Static semantics</a> : Phrases should have meaningful expression.
3.	<a>Unintentional error</a> : The error which is not intended by the programmer.

Case 1 and 2 are caught by compiler but third one is hard to detect.

## Objects

*	<a>Scalar (primities):</a> Primitive types `e.g. float, bool, int, ...`
*	<a>Non-scalar:</a> Custom or complex types which have data structure. `e.g. Vector, List, ...`

~~~python
# How to know the type of an object
type(5)
int

# How to prints a value
print(3 + 2) 
5
~~~

## Operators

*	i + j : Summation
*	i - j : Substarct
*	i * j : Multiply
*	i / j : Division
*	i % j : Remainder
*	i ** j : Power
*	pi_approx = 22/7 : Assignment

{: .notice--info}
**Note:** $22/7 = 3.1428571428571428571428571428571$

## Changing bindings

![Changing bindings]({{ site.url }}{{ site.imgurl }}OCW/6_0001/binding.png){: .align-center}

~~~python
pi = 3.14
radius = 2.2
area = pi*(radius**2)  # Pointer moves
radius = radius+1      # We lose previous handle and replace the value as new.
~~~

## References

1.	[Lecture note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-0001-introduction-to-computer-science-and-programming-in-python-fall-2016/lecture-slides-code/MIT6_0001F16_Lec1.pdf)
