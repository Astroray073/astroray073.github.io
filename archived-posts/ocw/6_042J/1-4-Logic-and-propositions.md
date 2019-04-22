---
title: "1.4 Logic & Propositions"
excerpt: "Examples of Proof Methods"
last_modified_at: 2017-06-17 11:41:04
mathjax: true
sidebar:
 nav: "ocw_6_042J"
---

{% include video id="0exBzsexUoI" provider="youtube" %}

{% include video id="eMWG-jTh-GE" provider="youtube" %}

{% include video id="_3WDzxt5p8c" provider="youtube" %}

## Lecture Materials

-	[Propositional Operators](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_PropositOper.pdf)
-	[Digital Logic](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_DigitalLogic.pdf)
-	[Truth Tables](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_TruthTables.pdf)
-	[Implies](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_Implies.pdf)
-	[Propositional Logic](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_PropositLogic.pdf)

{% include toc %}

## Propositional Logic

1.	True
2.	False
3.	AND
4.	OR
5.	XOR
6.	NOT

## Truth Table

**OR:** The value of (P or Q) is T iff P is T, or Q is T, or both are T.

|P|Q|P OR Q|
|T|T|T|
|T|F|T|
|F|T|T|
|F|F|F|

**XOR:** The value of (P xor Q) is T iff exactly one of P and Q is T.

|P|Q|P XOR Q|
|T|T|F|
|T|F|T|
|F|T|T|
|F|F|F|

**AND:** The value of (P and Q) is T iff both P and are T.

|P|Q|P AND Q|
|T|T|T|
|T|F|F|
|F|T|F|
|F|F|F|

**NOT:** The value of NOT(P) if T iff the value of P is F.

|P|NOT(P)|
|T|F|
|F|T|

## Binary addition circuit

![Binary Addition Circuit]({{ site.url }}{{ site.imgurl }}OCW/6_042J/binary-addition-circuit.png){: .align-center}

### Half Adder

![Half Adder]({{ site.url }}{{ site.imgurl }}OCW/6_042J/half-adder.png){: .align-center}

### Full Adder

![Full Adder]({{ site.url }}{{ site.imgurl }}OCW/6_042J/full-adder.png){: .align-center}

### Ripple Carry formulas

$$
	\begin{align*}
		s_i ::= a_i \; \rm{XOR} \; b_i
	\end{align*}
$$

$$
	\begin{align*}
		d_i ::= c_{i - 1} \; \rm{XOR} \; s_i
	\end{align*}
$$

$$
	\begin{align*}
		c_i ::= (c_{i-1} \; \rm{AND} \; s_i) \; \rm{OR} \; (a_i \; \rm{AND} \; b_i)
	\end{align*}
$$

## Truth Table

### DeMorgan's Law

NOT(P OR Q) is equivalent to NOT(P) AND NOT(Q).

### IFF

The value of (P IFF Q) is T iff P and Q have the same truth value.

|P|Q|P IFF Q|
|T|T|T|
|T|F|F|
|F|T|F|
|F|F|T|

### Satisfiability & Validity

>A formula is **satisfiable** iff it is true in some environment.

>A formula is **valid** iff it is true in all environments.

G and H are equivalent exactly when (G iff H) is valid.

### P = NP?

This question is equivalent to asking if there is an "efficient" procedure to check satisfiablility. (polynomial rather than exponential time).