---
title: "Supremum, Infimum, and the Completeness of $`\\mathbb{R}`$"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [01-dedekind-cuts]
---

# Supremum, Infimum, and the Completeness of $`\mathbb{R}`$

## Why this matters

The continuity of the real numbers ([Dedekind's theorem](./01-dedekind-cuts.en.md))
says the real line has no gaps. That abstract statement has an enormously useful
working form: **any non-empty set of reals that does not run off to infinity has a
least upper bound.** This is the tool we actually use to prove that limits exist —
that monotone sequences converge, that continuous functions attain their maxima,
that the intermediate value theorem holds. This lesson introduces the vocabulary
of bounds and states that key theorem.

## Definitions

Let $`S \subseteq \mathbb{R}`$ be a set of real numbers.

> **Definition (bounds).**
> A number $`M`$ is an *upper bound* of $`S`$ if $`x \le M`$ for every $`x \in S`$.
> A number $`m`$ is a *lower bound* of $`S`$ if $`m \le x`$ for every $`x \in S`$.
> $`S`$ is *bounded above* if it has an upper bound, *bounded below* if it has a
> lower bound, and *bounded* if both.

> **Definition (supremum / infimum).**
> The *supremum* (least upper bound) of $`S`$, written $`\sup S`$, is an upper bound
> $`\alpha`$ of $`S`$ such that no smaller number is an upper bound. The *infimum*
> (greatest lower bound), $`\inf S`$, is a lower bound that no larger number beats.

Concretely, $`\alpha = \sup S`$ is characterized by two conditions:

$$
\textbf{(i)}\quad x \le \alpha \ \text{ for all } x \in S;
\qquad
\textbf{(ii)}\quad \text{for every } \varepsilon > 0 \text{ there is } x \in S
\text{ with } x > \alpha - \varepsilon.
$$

Condition (i) says $`\alpha`$ is an upper bound; (ii) says nothing smaller than
$`\alpha`$ is — you can always find an element of $`S`$ within $`\varepsilon`$ of
$`\alpha`$.

Note $`\sup S`$ need not belong to $`S`$. For $`S = \{x : 0 \le x < 1\}`$ we have
$`\sup S = 1 \notin S`$. When the supremum *does* belong to $`S`$, it is the maximum.

## Key result

> **Theorem (Weierstrass / completeness of $`\mathbb{R}`$).**
> Every non-empty subset of $`\mathbb{R}`$ that is bounded above has a supremum in
> $`\mathbb{R}`$. Likewise, every non-empty subset bounded below has an infimum.

*Why it is true (sketch).* This is just Dedekind continuity rephrased. Given a
non-empty $`S`$ bounded above, split $`\mathbb{R}`$ into
$$
B = \{\, b \in \mathbb{R} : b \text{ is an upper bound of } S \,\},
\qquad
A = \mathbb{R} \setminus B.
$$
Both are non-empty ($`S`$ is bounded above so $`B \neq \varnothing`$; $`S`$ is
non-empty so some number lies below an element of $`S`$, giving $`A \neq \varnothing`$),
and every element of $`A`$ is less than every element of $`B`$. So $`(A, B)`$ is a cut
of $`\mathbb{R}`$. By Dedekind's theorem the cut is realized by a single real
number $`\alpha`$, and one checks that $`\alpha`$ is exactly the least upper bound of
$`S`$. The infimum statement follows by applying this to $`-S = \{-x : x \in S\}`$. $`\blacksquare`$

The completeness theorem and Dedekind continuity are **logically equivalent**;
either can be taken as *the* axiom that distinguishes $`\mathbb{R}`$ from
$`\mathbb{Q}`$. (Over $`\mathbb{Q}`$ the theorem fails: $`\{x \in \mathbb{Q} : x^2 < 2\}`$
is bounded above but has no rational supremum.)

## Worked example

**Problem.** Let $`S = \left\{\, 1 - \dfrac{1}{n} : n = 1, 2, 3, \dots \right\}`$.
Find $`\sup S`$ and $`\inf S`$, and say which (if either) belongs to $`S`$.

The elements are $`0, \tfrac12, \tfrac23, \tfrac34, \dots`$, increasing toward $`1`$.

- *Lower bound.* The smallest element is $`1 - \tfrac11 = 0`$ (at $`n=1`$), and every
  term is $`\ge 0`$. So $`0`$ is a lower bound and $`0 \in S`$; hence
  $`\inf S = 0`$, and it **is** attained (it is the minimum).
- *Upper bound.* Each term $`1 - \tfrac1n < 1`$, so $`1`$ is an upper bound. Is
  anything smaller an upper bound? For any $`\varepsilon > 0`$, choosing $`n`$ with
  $`\tfrac1n < \varepsilon`$ gives $`1 - \tfrac1n > 1 - \varepsilon`$. So no number
  below $`1`$ bounds $`S`$; by characterization (i)–(ii), $`\sup S = 1`$. It is
  **not** attained, so $`S`$ has no maximum.

**Answer.** $`\inf S = 0 \in S`$ (a minimum); $`\sup S = 1 \notin S`$ (no maximum).

## Common mistakes

- **Confusing supremum with maximum.** Every maximum is a supremum, but a
  supremum need not be attained. "$`\sup`$ exists" is far weaker — and far more
  often true — than "$`\max`$ exists."
- **Dropping non-emptiness.** The empty set has *every* real number as an upper
  bound, so it has no *least* one; the theorem genuinely needs $`S \neq \varnothing`$.
- **Expecting it over $`\mathbb{Q}`$.** Least upper bounds can fail to exist in
  $`\mathbb{Q}`$. Completeness is special to $`\mathbb{R}`$.
- **Forgetting condition (ii).** Showing $`\alpha`$ is *an* upper bound is only half
  the job; you must also show nothing smaller works.

## Practice

1. Find $`\sup`$ and $`\inf`$ of $`T = \left\{\, \dfrac{(-1)^n}{n} : n \ge 1 \right\}`$,
   and state whether each is attained.
2. Prove: if $`\alpha = \sup S`$ and $`\alpha \notin S`$, then for every
   $`\varepsilon > 0`$ the interval $`(\alpha - \varepsilon, \alpha)`$ contains
   infinitely many points of $`S`$.
3. Let $`A, B`$ be non-empty and bounded above with $`A \subseteq B`$. Show
   $`\sup A \le \sup B`$.

<details>
<summary>Answers</summary>

1. Terms: $`-1, \tfrac12, -\tfrac13, \tfrac14, \dots`$ The largest is
   $`\tfrac12`$ (at $`n=2`$), so $`\sup T = \tfrac12 \in T`$ (attained). The smallest is
   $`-1`$ (at $`n=1`$), so $`\inf T = -1 \in T`$ (attained).
2. If only finitely many points lay in $`(\alpha-\varepsilon,\alpha)`$ for some
   $`\varepsilon`$, the largest of them — together with the bound $`\alpha`$ on the
   rest — would give an upper bound below $`\alpha`$, contradicting (ii). (Since
   $`\alpha \notin S`$, no point equals $`\alpha`$.)
3. Any upper bound of $`B`$ bounds $`A`$ too (as $`A \subseteq B`$); in particular
   $`\sup B`$ is an upper bound of $`A`$, so the *least* upper bound of $`A`$ satisfies
   $`\sup A \le \sup B`$.

</details>

## See also

- [Dedekind Cuts and the Continuity of the Real Numbers](./01-dedekind-cuts.en.md)
- [Sequences and Their Limits](./03-sequence-limits.en.md)
