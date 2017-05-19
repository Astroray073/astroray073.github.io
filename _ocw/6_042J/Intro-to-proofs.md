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

{: .notice--info}
**Note:** Following contents are from the reading material.

## 1. Propositions

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

## 2. Predicates

>A `Predicate` can be understood as a proposition whose truth depends on the value of one or more variables.

I have used the predicate delegate in C# a lot but I don't know what is `predicate`. Now, I understand why people call the delegate signature as predicate.

```cs
delegate bool Predicate<T>(T arg);
```

## 3. The Axiomatic Method

The proposition that is regarded as the truth because it is too obvious.

>A proof is a sequence of logical deductions from
axioms and previously proved statements that concludes with the proposition in
question.

-	Important true propositions are called `theorems`.
-	A `lemma` is a preliminary proposition useful for proving later propositions.
-	A `corollary` is a proposition that follows in just a few logical steps from a
theorem.

## 4. Our Axioms

>The ZFC axioms are important in studying and justifying the foundations of mathematics, but for practical purposes, they are much too primitive.

### 4.1. Logical Deductions

>Logicla deductions, or `inference rulse`, are used to proce new propositions using previously proved ones. A fundamental inference ruls is `modus ponens`. This rule says that a proof of $P$ together with a proof that $P$ IMPLIES $Q$ is a proof of $Q$.

**The basic rule:**

$$
	\begin{align*}
		\text{antecedents} \over{\text{consequent}}
	\end{align*}
$$

**`modus ponens`:**

$$
	\begin{align*}
		P, \; P \; \mathrm{\text{IMPLIES}} \; Q \over{Q}
	\end{align*}
$$

**Other inference rules:**

$$
	\begin{align*}
		P \; \mathrm{\text{IMPLIES}} \; Q, \quad Q \; \mathrm{\text{IMPLIES}} \; R \over{P \; \mathrm{\text{IMPLIES}} \; P}
	\end{align*}
$$

$$
	\begin{align*}
		\mathrm{NOT} (P) \; \mathrm{\text{IMPLIES}} \; \mathrm{NOT} (Q) \over{Q \; \mathrm{\text{IMPLIES}} \; P}
	\end{align*}
$$

**Non-Rule:**

$$
	\begin{align*}
		\mathrm{NOT} (P) \; \mathrm{\text{IMPLIES}} \; \mathrm{NOT} (Q) \over{P \; \mathrm{\text{IMPLIES}} \; Q}
	\end{align*}
$$

## 5. Proving an Implication

### If $P$, then $Q$

**Proving Method**

1.	Write, "Assume $P$".
2.	Show that $Q$ logically follows.

**Proposition:**

{: .text-center }
If $0 \le x \le 2$, then $-x^3 + 4x + 1 \gt 0$

**Proof:**

Assume $0 \le x \le 2$. Then $x$, $2-x$, and $2 + x$ are all nonnegative. Therefore,
the product of these terms is also nonnegative. Adding 1 to this product gives a
positive number, so:

$$
	x(2 - x)(2 + x) + 1 \gt 0
$$

Multiplying out on the left side proves that

$$
	-x^3 + 4x + 1 \gt 0
$$

as claimed.	

**Tips**

*	You’ll often need to do some scratchwork while you’re trying to figure out
the logical steps of a proof. Your scratchwork can be as disorganized as you
like—full of dead-ends, strange diagrams, obscene words, whatever. But
keep your scratchwork separate from your final proof, which should be clear
and concise.

*	Proofs typically begin with the word “Proof” and end with some sort of delimiter
like ㅁ or “QED.” The only purpose for these conventions is to clarify
where proofs begin and end.

### NOT($Q$) IMPLIES NOT($P$)

**Proving Method**

1.	 Write, "We prove the contrapositive:" and then state the contrapositive.
2.	Proceed as in Method #1.

**Proposition:**

{: .text-center }
If $r$ is irrational, then $\sqrt{r}$ is also irrational.

**Proof:**

We proove the contrapositive: if $\sqrt{r}$ is rational, then $r$ is rational.

Assume that $\sqrt{r}$ is rational. Then there exist integers $m$ and $n$ such that:

$$ \sqrt{r} = {m \over{n}} $$

Squaring both sides gives:

$$ r = {m^2 \over{n^2}} $$

Since $m^2$ and $n^2$ are integers, $r$ is also rational.

## 6. Proving an "If and Only IF"

{: .notice--info}
**Note:** "If and Only IF" can be expessed as IFF

### Prove Each STatement Implies the Other

The statement “P IFF Q” is equivalent to the two statements “P IMPLIES Q” and
“Q IMPLIES P.” So you can prove an “iff” by proving two implications:

1.	Write, “We prove P implies Q and vice-versa.”
2.	Write, “First, we show P implies Q.” Do this by one of the methods in
`Section 5`.
3.	Write, “Now, we show Q implies P.” Again, do this by one of the methods
in `Section 5`.

### Construct a Chain of Iffs

In order to prove that P is true iff Q is true:

1.	Write, “We construct a chain of if-and-only-if implications.”
2.	Prove P is equivalent to a second statement which is equivalent to a third
statement and so forth until you reach Q.

>This method sometimes requires more ingenuity than the first, but the result can be
a short, elegant proof.

*[ZFC]: Zermelo-Fraenkel with Choice axioms