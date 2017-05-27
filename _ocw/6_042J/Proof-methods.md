---
title: "1.2 Proof Methods"
excerpt: "Examples of Proof Methods"
last_modified_at: 2017-05-27 15:23:27
mathjax: true
sidebar:
 nav: "ocw_6_042J"
---

{% include video id="CpW0ZJ7i0oc" provider="youtube" %}

{% include video id="vzpFQ3uNyPo" provider="youtube" %}

## Lecture Materials

-	[Lecture Slide](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/lecture-slides/MIT6_042JS16_ProofContrad.pdf)
-	[Quiz](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/proofs/tp1-2/vertical-2835de2f30b6)
-	[Lecture Note](https://ocw.mit.edu/courses/electrical-engineering-and-computer-science/6-042j-mathematics-for-computer-science-spring-2015/readings/MIT6_042JS15_Session2.pdf)

{% include toc %}

## 1. Proof by Contradiction

This method is making the contrapositive of the proposition to proof the proposition.

>In a *proof by contradiction, or indirect proof*, you show that if a proposition were false, then some flase fact would be true.

1.	Write, "We use proof by contradiction."
2.	Write, "Suppose $P$ is false."
3.	Deduce something known to be false (a logical contradiction).
4.	Write, "This is a contradiction. Therefore, $P$ must be true." 

### Example

**Proposition:** 

$\sqrt{2}$ is irrational.

**Proof:**

We use proof by contradiction. Suppose the claim is false, and $\sqrt 2$ is rational.
Then we can write $\sqrt 2$ as a fraction $n/d$ in lowest terms.

$$
	\sqrt 2 = {n \over d}
$$

Squaring both sides gives 

$$
	2 = {n^2 \over d^2}
	\\
	2d^2 = n^2
$$

This implies that $n$ is a multiple of 2 (see Problems 1.10 and 1.11). Therefore $n^2$ must be a multiple of 4. But since $2d^2 = n^2$, we know $2d^2$ is a multiple of 4 and so $d^2$ is a multiple of 2. This implies that $d$ is a multiple of 2.

So, the numerator and denominator have 2 as a common factor, which contradicts
the fact that $n/d$ is in lowest terms. Thus, 2 must be irrational.

## 2. Proof by Cases

Proofs a proprosition by spliting it into small cases that we can handle more easily.

### Example

**Proposition:**

Do following two expressions behave the same output

```cs
// Expression 1
if (x > 0 || x <= 0 && y > 100)

// Expression 2
if (x > 0 || y > 100)
```

**Proof:**

This proof is by case analysis. There are two cases.

**Case 1, $x \gt 0$:**

They omit the same output because `or` operator check expressions in order.

**Case 2, $x \leq 0$:**

Both failed first expression, `$x \gt 0$`, but omit the same output because `$x \leq 0$` is always true in the case.

**QED.** The claim therefore holds in both cases.

## 3. Good Proofs in Practice

1.	**State your game plan.** A good proof begins by explaining the general line of reasoning, for example, “We use case analysis” or “We argue by contradiction.”

2.	**Keep a linear flow.** Sometimes proofs are written like mathematical mosaics, with juicy tidbits of independent reasoning sprinkled throughout. This is not good. The steps of an argument should follow one another in an intelligible order.

3.	**A proof is an essay, not a calculation.** Many students initially write proofs the way they compute integrals. The result is a long sequence of expressions without explanation, making it very hard to follow. This is bad. A good proof usually looks like an essay with some equations thrown in. Use complete sentences.

4.	**Avoid excessive symbolism.** Your reader is probably good at understanding words, but much less skilled at reading arcane mathematical symbols. Use words where you reasonably can.

5.	**Revise and simplify.** Your readers will be grateful.

6.	**Introduce notation thoughtfully.** Sometimes an argument can be greatly simpli-fied by introducing a variable, devising a special notation, or defining a new term. But do this sparingly, since you’re requiring the reader to remember
all that new stuff. And remember to actually define the meanings of new variables, terms, or notations; don’t just start using them!

7.	**Structure long proofs.** Long programs are usually broken into a hierarchy of smaller procedures. Long proofs are much the same. When your proof needed facts that are easily stated, but not readily proved, those fact are best pulled out as preliminary `lemmas`. Also, if you are repeating essentially the same argument over and over, try to capture that argument in a general `lemma`, which you can cite repeatedly instead.

8.	**Be wary of the “obvious.”** When familiar or truly obvious facts are needed in a proof, it’s OK to label them as such and to not prove them. But remember that what’s obvious to you may not be—and typically is not—obvious to
your reader. Most especially, don’t use phrases like “clearly” or “obviously” in an attempt to bully the reader into accepting something you’re having trouble proving. Also, go on the alert whenever you see one of these phrases in someone else’s proof.

9.	**Finish.** At some point in a proof, you’ll have established all the essential facts you need. Resist the temptation to quit and leave the reader to draw the “obvious” conclusion. Instead, tie everything together yourself and explain why the original claim follows.