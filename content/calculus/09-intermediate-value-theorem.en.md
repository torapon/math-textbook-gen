---
title: "The Intermediate Value Theorem"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [05-nested-intervals, 08-functions-and-continuity]
---

# The Intermediate Value Theorem

## Why this matters

The intermediate value theorem (IVT) is the precise statement of the intuition
that a continuous graph cannot get from below a level to above it without
crossing it. It is the workhorse existence theorem of elementary analysis: it
proves equations have solutions ($`x^2 = 2`$, $`\cos x = x`$), guarantees roots of
odd-degree polynomials, and underlies the bisection method. Crucially, it is
where **continuity meets completeness** — the theorem is false without either.

## Key result

> **Theorem (Intermediate Value Theorem).** Let $`f`$ be continuous on the closed
> interval $`[a, b]`$, and let $`y`$ be any value between $`f(a)`$ and $`f(b)`$. Then
> there exists $`c \in [a, b]`$ with $`f(c) = y`$.

Equivalently (the most-used special case): if $`f`$ is continuous on $`[a,b]`$ and
$`f(a)`$ and $`f(b)`$ have **opposite signs**, then $`f`$ has a root in $`(a, b)`$.

*Proof (bisection / nested intervals).* By replacing $`f`$ with $`f - y`$ (or with
$`-f`$) we may assume $`f(a) < 0 < f(b)`$ and seek a root. Set $`a_0 = a`$, $`b_0 = b`$
and repeatedly bisect: with midpoint $`m = \tfrac{a_n + b_n}{2}`$,

```math
\text{if } f(m) \le 0,\ \text{set } [a_{n+1}, b_{n+1}] = [m,\ b_n];
\qquad
\text{if } f(m) > 0,\ \text{set } [a_{n+1}, b_{n+1}] = [a_n,\ m].
```

At every stage $`f(a_n) \le 0 \le f(b_n)`$, the intervals are nested and closed,
and $`b_n - a_n = \dfrac{b-a}{2^n} \to 0`$. By the
[nested interval theorem](./05-nested-intervals.en.md) they share a single point
$`c`$, and $`a_n \to c`$, $`b_n \to c`$. Continuity gives $`f(a_n) \to f(c)`$ and
$`f(b_n) \to f(c)`$; since $`f(a_n) \le 0`$ we get $`f(c) \le 0`$, and since
$`f(b_n) \ge 0`$ we get $`f(c) \ge 0`$. Hence $`f(c) = 0`$. $`\blacksquare`$

The proof shows the two pillars at work: **continuity** transfers the sign
information across the limit, and **completeness** (via nested intervals)
guarantees the limit point $`c`$ actually exists.

## Both hypotheses are essential

- **Continuity cannot be dropped.** On $`[-1, 1]`$ the function $`f(x) = -1`$ for
  $`x < 0`$, $`f(x) = 1`$ for $`x \ge 0`$ jumps from $`-1`$ to $`1`$ but never equals $`0`$.
- **Completeness cannot be dropped.** Over $`\mathbb{Q}`$, $`f(x) = x^2 - 2`$ is
  continuous with $`f(1) < 0 < f(2)`$, yet has **no rational root** — the crossing
  point $`\sqrt2`$ is a gap. IVT genuinely needs $`\mathbb{R}`$.

IVT gives *existence*, not uniqueness or a formula: there may be many such $`c`$,
and the theorem names none of them. (Bisection, however, computes one to any
precision.)

## Worked example

**Problem.** Show that $`\cos x = x`$ has a solution in $`[0, 1]`$.

Let $`f(x) = \cos x - x`$, continuous everywhere. At the endpoints,

```math
f(0) = \cos 0 - 0 = 1 > 0, \qquad
f(1) = \cos 1 - 1 \approx 0.540 - 1 = -0.460 < 0.
```

Since $`f`$ is continuous on $`[0,1]`$ and changes sign, IVT gives $`c \in (0,1)`$ with
$`f(c) = 0`$, i.e. $`\cos c = c`$.

**Answer.** A solution exists in $`(0,1)`$. (It is the *Dottie number*
$`c \approx 0.739`$, but IVT only asserts existence — finding the value needs
further work, e.g. iterating $`x \mapsto \cos x`$ or bisection.)

A useful corollary: **every odd-degree polynomial has a real root**, since
$`p(x) \to +\infty`$ at one end and $`-\infty`$ at the other, so $`p`$ changes sign.

## Common mistakes

- **Forgetting continuity must hold on the *whole* interval.** A single jump
  anywhere in $`[a,b]`$ can defeat the conclusion.
- **Reading existence as uniqueness.** IVT says *at least one* $`c`$; there can be
  several.
- **Using an open interval at the wrong place.** The hypothesis needs the closed
  interval $`[a,b]`$ (so endpoints exist); the root is located in the open
  $`(a,b)`$ in the sign-change form.
- **Expecting a formula for $`c`$.** IVT is non-constructive in itself; pair it with
  bisection if you need the number.

## Practice

1. Show that $`x^3 - x - 1 = 0`$ has a real root, and locate it within an interval
   of length $`1`$.
2. Prove that any continuous $`f : [0,1] \to [0,1]`$ has a *fixed point*: some
   $`c`$ with $`f(c) = c`$. *(Hint: apply IVT to $`g(x) = f(x) - x`$.)*
3. Give a continuous function on $`(0,1]`$ (note: not closed) for which the
   sign-change conclusion of IVT fails, or explain why none can.

<details>
<summary>Answers</summary>

1. $`p(x) = x^3 - x - 1`$: $`p(1) = -1 < 0`$, $`p(2) = 5 > 0`$, so a root lies in
   $`(1,2)`$.
2. $`g(x) = f(x) - x`$ is continuous, $`g(0) = f(0) \ge 0`$ and $`g(1) = f(1) - 1 \le 0`$.
   By IVT some $`c`$ has $`g(c) = 0`$, i.e. $`f(c) = c`$. (If either inequality is an
   equality, that endpoint is already a fixed point.)
3. The conclusion is about sign-change *between two endpoints*; on $`(0,1]`$ there is
   no left endpoint to compare, but IVT still applies to any closed subinterval
   $`[a,b]\subset(0,1]`$ where $`f`$ changes sign. The interval being non-closed only
   removes the endpoint $`0`$ from consideration; continuity on a closed subinterval
   is what matters.

</details>

## See also

- [The Nested Interval Theorem](./05-nested-intervals.en.md)
- [Functions, Limits, and Continuity](./08-functions-and-continuity.en.md)
- [Open and Closed Sets](./10-open-and-closed-sets.en.md)
