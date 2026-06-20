---
title: "Functions, Limits, and Continuity"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [03-sequence-limits, 07-accumulation-points]
---

# Functions, Limits, and Continuity

## Why this matters

So far we have studied numbers and sequences. Calculus, though, is about
**functions** — and its central qualitative property is *continuity*: a function
with no sudden jumps, the kind you can "draw without lifting your pen." That
slogan is too vague to prove anything with. This lesson gives the rigorous
$`\varepsilon`$–$`\delta`$ definitions of the limit of a function and of continuity,
and connects them to the sequence limits we already understand.

## Definitions

> **Definition (function).** A *function* $`f : D \to \mathbb{R}`$ assigns to each
> $`x`$ in its *domain* $`D \subseteq \mathbb{R}`$ exactly one real value $`f(x)`$.

> **Definition (limit of a function).** Let $`a`$ be an
> [accumulation point](./07-accumulation-points.en.md) of $`D`$. We say
> $`\lim_{x \to a} f(x) = L`$ if:
> ```math
> \text{for every } \varepsilon > 0 \text{ there is } \delta > 0 \text{ such that }
> 0 < |x - a| < \delta,\ x \in D \implies |f(x) - L| < \varepsilon.
> ```

We require $`a`$ to be an accumulation point of $`D`$ so that there are points of $`D`$
arbitrarily near $`a`$ to take the limit through; note $`x = a`$ itself is *excluded*
(the $`0 < |x-a|`$), so the value $`f(a)`$ — if it even exists — is irrelevant to the
limit.

> **Definition (continuity at a point).** $`f`$ is *continuous at* $`a \in D`$ if
> ```math
> \text{for every } \varepsilon > 0 \text{ there is } \delta > 0 \text{ such that }
> |x - a| < \delta,\ x \in D \implies |f(x) - f(a)| < \varepsilon.
> ```
> $`f`$ is *continuous* (on $`D`$) if it is continuous at every point of $`D`$.

When $`a`$ is an accumulation point of $`D`$, continuity at $`a`$ says exactly
$`\lim_{x\to a} f(x) = f(a)`$: the limit exists **and** equals the
function's value. Three things must agree — $`f(a)`$ is defined, the limit exists,
and they are equal.

## The sequential characterization

Function limits and sequence limits are two views of the same idea:

> **Theorem (sequential criterion).** $`\lim_{x\to a} f(x) = L`$ if and
> only if for **every** sequence $`(x_n)`$ in $`D \setminus \{a\}`$ with $`x_n \to a`$,
> we have $`f(x_n) \to L`$. Consequently, $`f`$ is continuous at $`a`$ iff
> $`x_n \to a \Rightarrow f(x_n) \to f(a)`$ for every such sequence.

This bridge lets us import everything we proved about sequences. In particular,
limits respect arithmetic:

> **Theorem (algebra of limits).** If $`\lim_{x\to a} f = L`$ and
> $`\lim_{x\to a} g = M`$, then as $`x \to a`$,
> ```math
> f \pm g \to L \pm M, \qquad fg \to LM, \qquad \frac{f}{g} \to \frac{L}{M}\ (M \neq 0).
> ```

## Building continuous functions

The sequential criterion turns these limit laws into a recipe for *manufacturing*
continuous functions out of simpler ones — each with a one-line proof.

> **Theorem (continuity under arithmetic).** If $`f`$ and $`g`$ are continuous at
> $`a`$, then so are the sum $`f + g`$, the difference $`f - g`$, any constant multiple
> $`cf`$, and the product $`fg`$; and so is the quotient $`f/g`$ provided $`g(a) \neq 0`$.

*Proof.* Take any sequence $`x_n \to a`$ in the common domain. Continuity gives
$`f(x_n) \to f(a)`$ and $`g(x_n) \to g(a)`$, and the algebra of limits **for
sequences** then yields $`f(x_n) \pm g(x_n) \to f(a) \pm g(a)`$, $`c\,f(x_n) \to
c\,f(a)`$, $`f(x_n)\,g(x_n) \to f(a)\,g(a)`$, and — when $`g(a) \neq 0`$, so
$`g(x_n) \neq 0`$ from some point on — $`f(x_n)/g(x_n) \to f(a)/g(a)`$. By the
sequential criterion, each combination is continuous at $`a`$. $`\blacksquare`$

Starting from the two most basic continuous functions — the constant $`x \mapsto c`$
and the identity $`x \mapsto x`$ — this theorem builds every **polynomial** (finitely
many sums and products) and every **rational function**, the latter continuous
wherever its denominator is nonzero.

Composition needs its own argument: it does *not* reduce to the algebra of limits.
(The naive "limit of a composite" can fail when the inner function actually hits
its target value — which is exactly why we state the result for *continuous*
functions, where the value equals the limit.)

> **Theorem (continuity of compositions).** If $`g`$ is continuous at $`a`$ and $`f`$
> is continuous at $`b = g(a)`$, then the composite $`f \circ g`$ is continuous at
> $`a`$.

*Proof.* Let $`x_n \to a`$. Continuity of $`g`$ at $`a`$ gives $`g(x_n) \to g(a) = b`$;
then continuity of $`f`$ at $`b`$ gives $`f\big(g(x_n)\big) \to f(b) = f\big(g(a)\big)`$.
By the sequential criterion, $`f \circ g`$ is continuous at $`a`$. $`\blacksquare`$

For instance $`x \mapsto \sqrt{x^2 + 1}`$ is continuous everywhere — it is the
(continuous) square-root function composed with the polynomial $`x^2 + 1`$, whose
values stay positive.

The sequential criterion is also the easiest way to prove a limit *does not*
exist: find two sequences $`x_n \to a`$ and $`x_n' \to a`$ along which $`f`$ tends to
different values.

## Worked example

**Problem.** Show that $`f(x) = x^2`$ is continuous at every $`a \in \mathbb{R}`$,
directly from the $`\varepsilon`$–$`\delta`$ definition.

We must bound $`|x^2 - a^2| = |x - a|\,|x + a|`$. Restrict attention to
$`|x - a| < 1`$; then $`|x| < |a| + 1`$, so $`|x + a| \le |x| + |a| < 2|a| + 1`$. Hence

```math
|x^2 - a^2| = |x-a|\,|x+a| < (2|a| + 1)\,|x - a|.
```

Given $`\varepsilon > 0`$, choose
$`\delta = \min\!\left(1,\ \dfrac{\varepsilon}{2|a| + 1}\right)`$. Then
$`|x - a| < \delta`$ gives $`|x^2 - a^2| < (2|a|+1)\cdot \dfrac{\varepsilon}{2|a|+1}
= \varepsilon`$.

**Answer.** $`f`$ is continuous at $`a`$. (The trick — first cap $`\delta \le 1`$ to
control the "extra" factor $`|x+a|`$, then shrink it further to hit $`\varepsilon`$ —
is the standard pattern for products.)

## A famous discontinuity

The function $`g(x) = \sin(1/x)`$ for $`x \neq 0`$ has **no limit** as $`x \to 0`$:
along $`x_n = \tfrac{1}{n\pi}`$ we get $`g(x_n) = 0`$, but along
$`x_n' = \tfrac{1}{2\pi n + \pi/2}`$ we get $`g(x_n') = 1`$. Two sequences approaching
$`0`$ produce different limits, so by the sequential criterion no limit exists — no
choice of $`g(0)`$ can make it continuous there.

## Common mistakes

- **Letting $`x = a`$ into the limit.** The limit deliberately ignores $`x = a`$;
  $`\lim_{x\to a} f`$ can exist even if $`f(a)`$ is undefined or has a different value.
- **Order of quantifiers again.** $`\delta`$ may depend on both $`\varepsilon`$ and
  $`a`$. (When one $`\delta`$ works for all $`a`$ at once, $`f`$ is *uniformly* continuous
  — a stronger notion for a later lesson.)
- **Proving a limit exists by trying one sequence.** One sequence can only
  *disprove*. Existence needs the full $`\varepsilon`$–$`\delta`$ condition (or all
  sequences).
- **Assuming "no lifting the pen" is a proof.** The pictorial idea guides
  intuition but is not an argument; reach for $`\varepsilon`$–$`\delta`$ or the
  sequential criterion.

## Practice

1. Prove from the definition that $`f(x) = 3x - 4`$ is continuous at every $`a`$.
2. Show $`\lim_{x\to 0}\dfrac{|x|}{x}`$ does not exist using the sequential
   criterion.
3. Let $`f(x) = x`$ if $`x \in \mathbb{Q}`$ and $`f(x) = 0`$ if $`x \notin \mathbb{Q}`$.
   At which points is $`f`$ continuous?

<details>
<summary>Answers</summary>

1. $`|f(x)-f(a)| = 3|x-a| < \varepsilon`$ when $`|x-a| < \tfrac\varepsilon3`$; take
   $`\delta = \tfrac\varepsilon3`$ (independent of $`a`$, so $`f`$ is even uniformly
   continuous).
2. Along $`x_n = \tfrac1n \to 0^+`$, the ratio is $`+1`$; along $`x_n = -\tfrac1n \to
   0^-`$, it is $`-1`$. Different limits $`\Rightarrow`$ no limit.
3. Only at $`a = 0`$. For any $`x`$, $`|f(x)| \le |x|`$, so $`f(x) \to 0 = f(0)`$ as
   $`x \to 0`$. For $`a \neq 0`$, rationals near $`a`$ give values near $`a`$ while
   irrationals give $`0`$; the two disagree, so $`f`$ is discontinuous there.

</details>

## See also

- [Sequences and Their Limits](./03-sequence-limits.en.md)
- [Accumulation Points and the Bolzano–Weierstrass Theorem](./07-accumulation-points.en.md)
- [The Intermediate Value Theorem](./09-intermediate-value-theorem.en.md)
- [The Extreme Value Theorem](./10-extreme-value-theorem.en.md)
