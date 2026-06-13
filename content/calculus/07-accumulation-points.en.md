---
title: "Accumulation Points and the Bolzano–Weierstrass Theorem"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [03-sequence-limits, 05-nested-intervals]
---

# Accumulation Points and the Bolzano–Weierstrass Theorem

## Why this matters

A bounded sequence need not converge, but it can never wander off to infinity, so
its terms must pile up somewhere. The points where they pile up are
*accumulation points*, and the Bolzano–Weierstrass theorem makes the intuition
precise: **every bounded infinite set of reals has at least one accumulation
point.** This is the existence theorem behind convergent subsequences, the
extreme value theorem, and compactness. It also gives us the right language for
*closed sets* — the sets that contain all their own limit points.

## Definitions

Let $S \subseteq \mathbb{R}$.

> **Definition (accumulation point).** A point $x \in \mathbb{R}$ is an
> *accumulation point* (or *limit point*) of $S$ if every neighborhood of $x$
> contains a point of $S$ **other than $x$ itself**: for every $\varepsilon > 0$,
> $$
> \big( (x - \varepsilon,\ x + \varepsilon) \setminus \{x\} \big) \cap S \neq \varnothing.
> $$

Equivalently, there is a sequence of points of $S$, all different from $x$,
converging to $x$. Intuitively $S$ "accumulates" arbitrarily close to $x$.

A point of $S$ that is *not* an accumulation point is an **isolated point**: it
has a neighborhood meeting $S$ only at itself. Note an accumulation point need
not belong to $S$ (e.g. $0$ for $S = \{\tfrac1n\}$), and a point of $S$ need not
be an accumulation point.

## Key result

> **Theorem (Bolzano–Weierstrass).** Every bounded infinite subset of
> $\mathbb{R}$ has at least one accumulation point. Equivalently, every bounded
> sequence of reals has a convergent subsequence.

*Proof (bisection).* Let $S$ be infinite and contained in $[a, b]$. Bisect:
at least one of the two halves contains infinitely many points of $S$; call it
$[a_1, b_1]$. Bisect again, always keeping a half with infinitely many points of
$S$, producing nested closed intervals $[a_n, b_n]$ with
$b_n - a_n = \dfrac{b - a}{2^n} \to 0$. By the
[nested interval theorem](./05-nested-intervals.en.md) they share a single point
$\xi$. Every neighborhood of $\xi$ contains some $[a_n, b_n]$, hence infinitely
many points of $S$ — so $\xi$ is an accumulation point. $\blacksquare$

For the subsequence form: from a bounded sequence pick terms lying in successive
$[a_n,b_n]$ with increasing indices; they converge to $\xi$.

## Closed sets

> **Definition (closed set).** A set $F \subseteq \mathbb{R}$ is *closed* if it
> contains all of its accumulation points.

Equivalently, $F$ is closed iff every convergent sequence of points of $F$ has
its limit in $F$ — closed sets are "sealed" under taking limits.

| Set | Accumulation points | Closed? |
|:----|:----|:--:|
| $[0,1]$ | all of $[0,1]$ | yes |
| $(0,1]$ | all of $[0,1]$ | no ($0$ is missing) |
| $\{\tfrac1n : n \ge 1\}$ | $\{0\}$ | no ($0$ is missing) |
| $\{0\} \cup \{\tfrac1n\}$ | $\{0\}$ | yes |
| $\mathbb{Z}$ | none | yes (vacuously) |

A finite set has no accumulation points, so it is closed automatically. The
deeper structural facts (arbitrary intersections and finite unions of closed sets
are closed; closed $=$ complement of open) are developed in the
[final lesson](./10-open-and-closed-sets.en.md).

## Worked example

**Problem.** Find all accumulation points of
$S = \left\{\, \dfrac1m + \dfrac1n : m, n \ge 1 \,\right\}$, and decide whether
$S$ is closed.

Fix $m$ and let $n \to \infty$: $\tfrac1m + \tfrac1n \to \tfrac1m$, so each
$\tfrac1m$ is an accumulation point. Letting $m \to \infty$ as well,
$\tfrac1m + \tfrac1n \to 0$, so $0$ is an accumulation point too. No other point
$c$ qualifies: if $c \notin \{0\} \cup \{\tfrac1m\}$, one checks a small
neighborhood of $c$ meets $S$ in only finitely many points.

So the accumulation points are $\{0\} \cup \{\tfrac1m : m \ge 1\}$. Now $0 \notin S$
(a sum of two positive terms is $> 0$, and the infimum $0$ is never attained), so
$S$ is **missing the accumulation point $0$**.

**Answer.** Accumulation points: $\{0\} \cup \{\tfrac1m : m\ge1\}$; $S$ is **not**
closed because $0 \notin S$.

## Common mistakes

- **"Other than $x$ itself" matters.** Without excluding $x$, every point of $S$
  would trivially qualify. An isolated point of $S$ is *not* an accumulation point.
- **Confusing accumulation point with point of the set.** Neither implies the
  other: $0$ accumulates $\{\tfrac1n\}$ but isn't in it; each $\tfrac1n$ is in the
  set but is isolated.
- **Thinking finite sets need checking.** A finite (or any set with no
  accumulation points) is closed for free.
- **Requiring boundedness for closedness.** Closed and bounded are independent;
  $\mathbb{Z}$ is closed and unbounded, $(0,1)$ is bounded and not closed.

## Practice

1. Find the accumulation points of $\mathbb{Q} \cap [0,1]$. Is this set closed?
2. Show that a set with no accumulation points is closed, and give an unbounded
   example.
3. Prove the subsequence form of Bolzano–Weierstrass from the
   accumulation-point form. *(Hint: choose indices $n_1 < n_2 < \cdots$ with
   $a_{n_k}$ within $\tfrac1k$ of an accumulation point.)*

<details>
<summary>Answers</summary>

1. Every point of $[0,1]$ is a limit of rationals in $[0,1]$, so the set of
   accumulation points is all of $[0,1]$. Since irrationals in $[0,1]$ are
   accumulation points not in $\mathbb{Q}\cap[0,1]$, the set is **not** closed.
2. If there are no accumulation points, the condition "contains all its
   accumulation points" is vacuously true, so the set is closed. Example:
   $\mathbb{Z}$.
3. Let $\xi$ be an accumulation point. Pick $n_1$ with $|a_{n_1}-\xi|<1$; having
   chosen $n_{k-1}$, infinitely many terms lie within $\tfrac1k$ of $\xi$, so pick
   $n_k > n_{k-1}$ with $|a_{n_k}-\xi|<\tfrac1k$. Then $a_{n_k}\to\xi$.

</details>

## See also

- [The Nested Interval Theorem](./05-nested-intervals.en.md)
- [Functions, Limits, and Continuity](./08-functions-and-continuity.en.md)
- [Open and Closed Sets](./10-open-and-closed-sets.en.md)
