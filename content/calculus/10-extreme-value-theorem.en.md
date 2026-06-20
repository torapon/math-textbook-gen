---
title: "The Extreme Value Theorem"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [07-accumulation-points, 08-functions-and-continuity]
---

# The Extreme Value Theorem

## Why this matters

The [intermediate value theorem](./09-intermediate-value-theorem.en.md) says a
continuous function on $`[a,b]`$ misses *no* value between its endpoints. Its
companion, the **extreme value theorem** (EVT), says the function never runs off
to infinity and actually *reaches* its highest and lowest values: there is a point
where it is largest and a point where it is smallest. This is the existence
theorem behind "find the maximum" problems — before you can optimize a continuous
quantity on a closed interval, EVT is what guarantees there is a maximum to find.
Like the IVT, it rests on the **completeness of $`\mathbb{R}`$**, here through the
[Bolzano–Weierstrass theorem](./07-accumulation-points.en.md).

## Key result

> **Theorem (Extreme Value Theorem).** If $`f`$ is continuous on the closed,
> bounded interval $`[a, b]`$, then $`f`$ is **bounded** on $`[a,b]`$ and **attains**
> its maximum and minimum: there exist points $`c, d \in [a, b]`$ with
> ```math
> f(d) \le f(x) \le f(c) \qquad \text{for all } x \in [a, b].
> ```

Two claims are bundled here, and both can fail for badly behaved functions:
*boundedness* (the values do not escape to $`\pm\infty`$) and *attainment* (the
extreme values are achieved, not merely approached). The number $`f(c)`$ is the
**maximum** and $`f(d)`$ the **minimum**; together they are the *extreme values*.

## Proof

Both parts run on the same engine: pick a sequence that chases the behavior we
care about, then use Bolzano–Weierstrass to extract a convergent subsequence and
let continuity finish the job.

**Step 1 — $`f`$ is bounded.** Suppose, for contradiction, that $`f`$ is *not*
bounded above. Then for each $`n`$ there is a point $`x_n \in [a,b]`$ with
$`f(x_n) > n`$. The sequence $`(x_n)`$ lies in $`[a,b]`$, so it is bounded; by
[Bolzano–Weierstrass](./07-accumulation-points.en.md) it has a convergent
subsequence $`x_{n_k} \to c`$. Since $`a \le x_{n_k} \le b`$ for all $`k`$, the limit
satisfies $`a \le c \le b`$ — this is where the interval being **closed** is used.
Continuity at $`c`$ forces $`f(x_{n_k}) \to f(c)`$, a finite number. But
$`f(x_{n_k}) > n_k \to \infty`$, a contradiction. So $`f`$ is bounded above; applying
the same argument to $`-f`$ shows it is bounded below.

**Step 2 — the maximum is attained.** Let
```math
M = \sup\{\, f(x) : x \in [a,b] \,\},
```
which exists and is finite by Step 1 and the
[least-upper-bound property](./02-supremum-infimum.en.md). By the definition of the
supremum, for each $`n`$ the number $`M - \tfrac1n`$ is *not* an upper bound, so
there is $`x_n \in [a,b]`$ with
```math
M - \tfrac1n < f(x_n) \le M, \qquad \text{hence } f(x_n) \to M.
```
Again $`(x_n)`$ lies in $`[a,b]`$; by Bolzano–Weierstrass take $`x_{n_k} \to c \in
[a,b]`$. Continuity gives $`f(x_{n_k}) \to f(c)`$. But $`f(x_{n_k})`$ is a subsequence
of a sequence tending to $`M`$, so $`f(x_{n_k}) \to M`$ as well. Limits are unique,
so $`f(c) = M`$: the supremum is achieved at $`c`$, and is therefore a genuine
maximum. The minimum is the maximum of $`-f`$. $`\blacksquare`$

## All three hypotheses are essential

Drop any one and the conclusion can fail.

- **Closed.** On the half-open interval $`(0, 1]`$, $`f(x) = 1/x`$ is continuous but
  **unbounded** above — boundedness fails. Even when bounded, attainment can fail:
  $`f(x) = x`$ on the open interval $`(0,1)`$ has $`\sup = 1`$ and $`\inf = 0`$, but
  reaches neither.
- **Bounded.** On the closed but *infinite* interval $`[0, \infty)`$, $`f(x) = x`$ is
  continuous and unbounded. And $`f(x) = \arctan x`$ on $`\mathbb{R}`$ is bounded
  (values in $`(-\tfrac\pi2, \tfrac\pi2)`$) yet attains neither bound.
- **Continuous.** On $`[0,1]`$ define $`f(x) = x`$ for $`x < 1`$ and $`f(1) = 0`$. Then
  $`\sup f = 1`$ is approached as $`x \to 1^-`$ but never attained — the single
  discontinuity at $`1`$ destroys the maximum.

Each example keeps two hypotheses and violates the third, so all three are doing
real work. (The pattern "closed **and** bounded" is the property called
*compactness*, the true home of this theorem; see the
[next lesson](./11-open-and-closed-sets.en.md).)

## Worked example

**Problem.** Let $`f`$ be continuous on $`[a,b]`$ with $`f(x) > 0`$ for every $`x`$.
Show there is a constant $`\delta > 0`$ with $`f(x) \ge \delta`$ for all $`x \in
[a,b]`$ — a *uniform* positive lower bound, not just positivity point by point.

By EVT, $`f`$ attains its minimum at some $`d \in [a,b]`$: $`f(x) \ge f(d)`$ for all
$`x`$. Since $`d \in [a,b]`$, the hypothesis gives $`f(d) > 0`$. Put $`\delta = f(d) >
0`$; then $`f(x) \ge \delta`$ everywhere on $`[a,b]`$.

**Answer.** Such a $`\delta`$ exists. (The closed interval is crucial: on $`(0,1]`$
the positive function $`f(x) = x`$ has *no* positive lower bound, since its values
shrink to $`0`$. The conclusion also makes $`1/f`$ bounded on $`[a,b]`$ — a fact used
constantly when dividing by a continuous nonzero function.)

## A capstone: combining IVT and EVT

Put the two great theorems together. On $`[a,b]`$ a continuous $`f`$ attains a
minimum $`m = f(d)`$ and a maximum $`M = f(c)`$ (EVT), and by the IVT it takes
*every* value between $`f(d)`$ and $`f(c)`$. Hence the image is exactly the closed
interval
```math
f\big([a,b]\big) = [\,m,\ M\,].
```
**The continuous image of a closed bounded interval is again a closed bounded
interval** — a clean statement that neither theorem gives alone.

## Common mistakes

- **Confusing "bounded" with "attains its bound."** $`\arctan`$ on $`\mathbb{R}`$ is
  bounded yet has no maximum. EVT needs a closed *bounded* interval to deliver
  attainment, not just boundedness.
- **Forgetting the interval must be closed *and* bounded.** Either failure alone
  can sink the conclusion, as the counterexamples show.
- **Expecting the location of $`c`$ or $`d`$.** Like the IVT, EVT is an *existence*
  theorem; it names no point. Locating the extremum is the job of differentiation
  (critical points) in later lessons.
- **Assuming the max occurs in the interior.** It may sit at an endpoint — e.g. an
  increasing function on $`[a,b]`$ is maximal at $`b`$.

## Practice

1. Show that a continuous function on $`[a,b]`$ is bounded, *without* assuming the
   attainment part — i.e. reprove Step 1 in your own words.
2. Give a continuous function on the open interval $`(0,1)`$ that is bounded but
   attains neither its supremum nor its infimum.
3. Let $`f`$ be continuous on $`[a,b]`$. Show the *range* $`f([a,b])`$ is a bounded
   set and that $`\sup f([a,b])`$ and $`\inf f([a,b])`$ both belong to it.
4. True or false: if $`f`$ is continuous on the *closed* but unbounded interval
   $`[0,\infty)`$ and is bounded, it must attain its supremum. Justify.

<details>
<summary>Answers</summary>

1. If $`f`$ were unbounded above, choose $`x_n \in [a,b]`$ with $`f(x_n) > n`$. By
   Bolzano–Weierstrass a subsequence $`x_{n_k} \to c \in [a,b]`$ (closedness keeps
   $`c`$ in range); continuity gives $`f(x_{n_k}) \to f(c)`$ finite, contradicting
   $`f(x_{n_k}) > n_k \to \infty`$. Same for below.
2. $`f(x) = x`$ on $`(0,1)`$: $`\sup = 1`$, $`\inf = 0`$, and since the endpoints are
   excluded, neither value is taken. (Or $`f(x) = 2x - 1`$, range $`(-1,1)`$.)
3. Boundedness of the range is exactly Step 1. For the suprema: by EVT there is
   $`c`$ with $`f(c) = M := \sup f([a,b])`$, so $`M \in f([a,b])`$; likewise the
   infimum is attained. Thus both lie in the range.
4. **False.** $`f(x) = \arctan x`$ on $`[0,\infty)`$ is continuous and bounded above
   by $`\tfrac\pi2`$, with $`\sup = \tfrac\pi2`$ never attained. Boundedness of the
   *interval* — not just of $`f`$ — is what EVT requires.

</details>

## See also

- [Accumulation Points and the Bolzano–Weierstrass Theorem](./07-accumulation-points.en.md)
- [Functions, Limits, and Continuity](./08-functions-and-continuity.en.md)
- [The Intermediate Value Theorem](./09-intermediate-value-theorem.en.md)
- [Open and Closed Sets, Interior and Boundary](./11-open-and-closed-sets.en.md)
