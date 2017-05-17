---
title: "1.1 Intro to Proofs"
excerpt: "Working..."
last_modified_at: 2017-05-17 08:25:20
mathjax: true
sidebar:
 nav: "ocw_6_042J"
header:
 video:
  id: wIq4CssPoO0
  provider: youtube
---

## Lecture Materials

[Lecture Note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/readings/MIT6_042JS15_Session1.pdf)

{% include toc %}

## What does "discrete" means?

`Discrete` means having unpredictable gaps along values rather than continuous.

## Propositions

`Proposition` is a statement (communication) that is either true or false.

Let

$$
	\begin{align}
		p(n)::= n^2 + n + 41
	\end{align}
$$

### Example 1 

$$
	\begin{align}
		\forall _n \in \Bbb N \quad p(n) \text{ is prime.} 
	\end{align}
$$

$p(n)$ is true until 40. But $p(40) = 40^2 + 40 + 41 = 41 * 41$ is not prime.

The important thing is

>We can't check whether a proposition of infinite set is true by finite set.

### Example 2 - Euler's Conjecture

The equation $a^4 + b^4 + c^4 \neq d^4$ has no solution where a, b, c, d are positive intergers.


In logical notation,

$$
	\begin{align}
		\forall_{a, b, c, d} \in \Bbb Z^+. \quad a^4 + b^4 + c^4 \neq d^4.
	\end{align}
$$

{: .notice--info}
**Note:** The proposition above is also false.

## Predicates

>A `Predicate` can be understood as a proposition whose truth depends on the value of one or more variables.

I have used the predicate delegate in C# a lot but I don't know what is `predicate`. Now, I understand why people call the delegate signature as predicate.

```cs
delegate bool Predicate<T>(T arg);
```

## The Axiomatic Method

The proposition that is regarded as the truth because it is too obvious.

## Proofs

>A proof is a sequence of logical deductions from
axioms and previously proved statements that concludes with the proposition in
question.

-	Important true propositions are called `theorems`.
-	A `lemma` is a preliminary proposition useful for proving later propositions.
-	A `corollary` is a proposition that follows in just a few logical steps from a
theorem.

