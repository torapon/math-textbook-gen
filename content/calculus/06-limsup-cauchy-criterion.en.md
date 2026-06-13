---
title: "Limit Superior and the Cauchy Criterion"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [03-sequence-limits, 04-monotone-convergence]
---

# Limit Superior and the Cauchy Criterion

## Why this matters

Two limitations remain in our theory of sequences. First, a bounded sequence may
fail to have a limit ($`(-1)^n`$), yet it still has a well-defined *largest* and
*smallest* long-run value — the **limit superior** and **limit inferior** — which
always exist and tell us how the sequence eventually behaves. Second, the
$`\varepsilon`$–$`N`$ definition of convergence requires *knowing the limit in
advance*. The **Cauchy criterion** removes that requirement: it certifies
convergence using only the terms of the sequence, by checking that they bunch
together. Both ideas are, once again, powered by completeness.

## Limit superior and inferior

For a bounded sequence $`(a_n)`$, define the *tail suprema* and *tail infima*

```math
s_n = \sup_{k \ge n} a_k, \qquad t_n = \inf_{k \ge n} a_k.
```

As $`n`$ grows the tail shrinks, so $`(s_n)`$ is decreasing and $`(t_n)`$ is increasing,
and both are bounded; by [monotone convergence](./04-monotone-convergence.en.md)
they converge.

> **Definition (limsup / liminf).**
> ```math
> \limsup_{n\to\infty} a_n = \lim_{n\to\infty} s_n = \inf_{n} \sup_{k\ge n} a_k,
> \qquad
> \liminf_{n\to\infty} a_n = \lim_{n\to\infty} t_n = \sup_{n} \inf_{k\ge n} a_k.
> ```

These **always exist** for a bounded sequence (allow $`\pm\infty`$ for unbounded
ones). Always $`\liminf a_n \le \limsup a_n`$, and they pin down ordinary
convergence:

> **Theorem.** A bounded sequence converges $`\iff \liminf a_n = \limsup a_n`$, and
> then the common value is $`\lim a_n`$.

For example $`a_n = (-1)^n`$ has $`\limsup = 1`$, $`\liminf = -1`$: the gap between them
measures the sequence's persistent oscillation.

## The Cauchy criterion

> **Definition (Cauchy sequence).** $`(a_n)`$ is a *Cauchy sequence* if
> ```math
> \text{for every } \varepsilon > 0 \text{ there is } N \text{ such that }
> m, n \ge N \implies |a_m - a_n| < \varepsilon.
> ```

The terms eventually lie within $`\varepsilon`$ of **one another** — no limit value
is mentioned.

> **Theorem (Cauchy criterion / completeness).** A sequence of real numbers
> converges **if and only if** it is a Cauchy sequence.

*Proof.*
($`\Rightarrow`$) If $`a_n \to L`$, then for $`m,n \ge N`$ we have
$`|a_m - a_n| \le |a_m - L| + |L - a_n| < \tfrac\varepsilon2 + \tfrac\varepsilon2
= \varepsilon`$.

($`\Leftarrow`$) Suppose $`(a_n)`$ is Cauchy. It is **bounded** (take
$`\varepsilon = 1`$: all terms past $`N`$ lie within $`1`$ of $`a_N`$, and finitely many
precede it). A bounded sequence has finite $`L = \limsup a_n`$. Given $`\varepsilon`$,
pick $`N`$ with $`|a_m - a_n| < \tfrac\varepsilon2`$ for $`m,n\ge N`$; since infinitely
many terms come within $`\tfrac\varepsilon2`$ of $`L`$, one of them, $`a_m`$ with
$`m \ge N`$, has $`|a_m - L| < \tfrac\varepsilon2`$, whence for all $`n \ge N`$,
$`|a_n - L| \le |a_n - a_m| + |a_m - L| < \varepsilon`$. So $`a_n \to L`$. $`\blacksquare`$

This equivalence is **completeness in disguise**: over $`\mathbb{Q}`$ a sequence of
rationals approximating $`\sqrt2`$ is Cauchy but has no rational limit. The Cauchy
criterion holds precisely because $`\mathbb{R}`$ has no gaps.

## Worked example

**Problem.** Show $`a_n = \displaystyle\sum_{k=1}^{n} \frac{1}{k^2}`$ converges,
without computing its value, by verifying it is Cauchy.

For $`m > n`$,

```math
|a_m - a_n| = \sum_{k=n+1}^{m} \frac{1}{k^2}
< \sum_{k=n+1}^{m} \frac{1}{k(k-1)}
= \sum_{k=n+1}^{m}\!\left(\frac{1}{k-1} - \frac{1}{k}\right)
= \frac1n - \frac1m < \frac1n,
```

using the telescoping bound $`\frac{1}{k^2} < \frac{1}{k(k-1)}`$. Given
$`\varepsilon > 0`$, choose $`N > \tfrac1\varepsilon`$; then for $`m > n \ge N`$,
$`|a_m - a_n| < \tfrac1n \le \tfrac1N < \varepsilon`$. So $`(a_n)`$ is Cauchy, hence
converges.

**Answer.** The series $`\sum 1/k^2`$ converges. (Its value is $`\pi^2/6`$, but the
Cauchy criterion proves *existence* of the limit without it.)

## Common mistakes

- **Checking only adjacent terms.** $`|a_{n+1} - a_n| \to 0`$ does **not** imply
  Cauchy. The harmonic sums $`a_n = \sum_{k=1}^n \tfrac1k`$ have
  $`a_{n+1}-a_n = \tfrac1{n+1} \to 0`$ yet diverge. You must control $`|a_m - a_n|`$
  for *all* large $`m, n`$.
- **Confusing limsup with sup.** $`\sup_n a_n`$ looks at the whole sequence;
  $`\limsup`$ ignores any finite head and captures only long-run behavior.
- **Expecting the Cauchy criterion in $`\mathbb{Q}`$.** It characterizes
  convergence only in a complete space.

## Practice

1. Compute $`\limsup`$ and $`\liminf`$ of $`a_n = (-1)^n\!\left(1 + \tfrac1n\right)`$.
2. Prove directly that a Cauchy sequence is bounded.
3. Show $`a_n = \sum_{k=1}^{n}\tfrac{1}{k}`$ is **not** Cauchy by exhibiting, for
   $`\varepsilon = \tfrac12`$, indices $`m,n`$ with $`|a_m - a_n| \ge \tfrac12`$ no
   matter how large $`N`$ is. *(Hint: compare $`a_{2n}`$ and $`a_n`$.)*

<details>
<summary>Answers</summary>

1. Even $`n`$: $`a_n = 1 + \tfrac1n \downarrow 1`$; odd $`n`$: $`a_n = -(1+\tfrac1n)
   \uparrow -1`$. So $`\limsup = 1`$, $`\liminf = -1`$.
2. Take $`\varepsilon = 1`$, get $`N`$ with $`|a_n - a_N| < 1`$ for $`n \ge N`$, so those
   terms lie in $`(a_N - 1, a_N + 1)`$; combine with the finitely many
   $`a_1,\dots,a_{N-1}`$ to get a global bound.
3. $`a_{2n} - a_n = \sum_{k=n+1}^{2n}\tfrac1k \ge n \cdot \tfrac{1}{2n} = \tfrac12`$.
   For any $`N`$, pick $`n \ge N`$ and $`m = 2n`$: $`|a_m - a_n| \ge \tfrac12`$. Not
   Cauchy, so it diverges.

</details>

## See also

- [Monotone Bounded Sequences Converge](./04-monotone-convergence.en.md)
- [Accumulation Points and the Bolzano–Weierstrass Theorem](./07-accumulation-points.en.md)
