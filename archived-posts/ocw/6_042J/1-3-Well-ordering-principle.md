---
title: "1.3 Well Ordering Principle"
excerpt: "Examples of Proof Methods"
last_modified_at: 2017-06-17 10:05:58
mathjax: true
sidebar:
 nav: "ocw_6_042J"
---

{% include video id="fV3v6qQ3w4A" provider="youtube" %}

{% include video id="I1HpgnWQI7I" provider="youtube" %}

{% include video id="hNrtGiCFPGs" provider="youtube" %}

## Lecture Materials

-	[Lecture Slide - 1](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_WellOrdering1.pdf)
-	[Lecture Slide - 2](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_WellOrdering2.pdf)
-	[Lecture Slide - 3](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_WellOrdering3.pdf)
-	[Quiz](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/proofs/tp2-1/vertical-1d9c2a0e507a/)
-	[Lecture Note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/readings/MIT6_042JS15_Session3.pdf)

{% include toc %}

## 1. Theorm

>Every nonempty set of nonnegative integers has a smallest element.

## 2. Usage

A standard way to prove proprosition by using `Well Ordering Principle`

To prove that $\forall{n} \in \Bbb{N}$. $P(n)$ using WOP :

-	Define set of `counterexamples`

$$
	\begin{align*}
		C :: = \{n \in \Bbb{N} \; | \; \rm{NOT}\;P(n)\}
	\end{align*}
$$

-	Assume $C$ is not empty. By WOP, have minimum element $m \in C$
-	Reach a `contradiction` somehow ... or by proving $P(m)$

*[WOP]: Well Ordering Principle