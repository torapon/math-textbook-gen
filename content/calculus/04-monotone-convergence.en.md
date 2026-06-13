---
title: "Monotone Bounded Sequences Converge"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [02-supremum-infimum, 03-sequence-limits]
---

# Monotone Bounded Sequences Converge

## Why this matters

The $`\varepsilon`$–$`N`$ definition tells us how to *check* a limit, but it assumes
we already have a candidate value $`L`$ in hand. Often we don't: we build a number
as the end of a process (a decimal expansion, an iteration, a partial-sum
sequence) and want to know it converges **before** we can name the limit. The
monotone convergence theorem is the first tool that delivers existence of a limit
out of thin air — using only the completeness of $`\mathbb{R}`$.

## Definitions

> **Definition (monotone).** A sequence $`(a_n)`$ is
> *increasing* if $`a_n \le a_{n+1}`$ for all $`n`$, and
> *decreasing* if $`a_n \ge a_{n+1}`$ for all $`n`$.
> It is *monotone* if it is one or the other. (Strict inequalities give
> *strictly* increasing/decreasing.)

## Key result

> **Theorem (Monotone Convergence).** A monotone sequence converges **if and only
> if** it is bounded. More precisely:
> ```math
> (a_n) \text{ increasing and bounded above} \implies \lim_{n\to\infty} a_n = \sup_n a_n,
> ```
> ```math
> (a_n) \text{ decreasing and bounded below} \implies \lim_{n\to\infty} a_n = \inf_n a_n.
> ```

*Proof (increasing case).* Suppose $`(a_n)`$ is increasing and bounded above. The
set $`S = \{a_n : n \ge 1\}`$ is non-empty and bounded above, so by the
[completeness theorem](./02-supremum-infimum.en.md) it has a supremum
$`\alpha = \sup S`$. We show $`a_n \to \alpha`$.

Let $`\varepsilon > 0`$. By the characterization of the supremum, $`\alpha -
\varepsilon`$ is **not** an upper bound, so some term satisfies $`a_N > \alpha -
\varepsilon`$. Because the sequence is increasing, for every $`n \ge N`$,

```math
\alpha - \varepsilon < a_N \le a_n \le \alpha < \alpha + \varepsilon,
```

hence $`|a_n - \alpha| < \varepsilon`$. That is exactly $`a_n \to \alpha`$. The
decreasing case follows by applying this to $`(-a_n)`$. ($`\Leftarrow`$ is the
theorem; $`\Rightarrow`$ holds because every convergent sequence is bounded.) $`\blacksquare`$

The picture: an increasing sequence climbs but is held under a ceiling. The least
ceiling — the supremum — is precisely the value it is forced to approach. It can
never overshoot (monotonicity), and it cannot stall below $`\alpha`$ (or that lower
level would be a smaller ceiling).

## Worked example

**Problem.** Define $`a_1 = \sqrt{2}`$ and $`a_{n+1} = \sqrt{2 + a_n}`$. Show $`(a_n)`$
converges and find its limit.

*Bounded above by $`2`$.* By induction: $`a_1 = \sqrt2 < 2`$, and if $`a_n < 2`$ then
$`a_{n+1} = \sqrt{2 + a_n} < \sqrt{2+2} = 2`$.

*Increasing.* $`a_{n+1} \ge a_n \iff 2 + a_n \ge a_n^2 \iff a_n^2 - a_n - 2 \le 0
\iff (a_n - 2)(a_n + 1) \le 0`$, true since $`0 < a_n < 2`$.

So $`(a_n)`$ is increasing and bounded above; by the theorem it converges to some
$`L`$. Letting $`n \to \infty`$ in $`a_{n+1} = \sqrt{2 + a_n}`$ (both sides have the
same limit) gives $`L = \sqrt{2 + L}`$, i.e. $`L^2 - L - 2 = 0`$, so $`(L-2)(L+1)=0`$.
Since $`L \ge a_1 > 0`$, we take $`L = 2`$.

**Answer.** $`a_n \to 2`$.

Note the two-step pattern: **(1)** prove convergence via monotone + bounded,
**(2)** *then* solve for the limit using the recurrence. Step 2 alone is invalid —
the equation $`L = \sqrt{2+L}`$ also has the root $`-1`$, and without step 1 you
cannot rule out divergence.

## Common mistakes

- **Solving the fixed-point equation without proving convergence first.** A
  divergent sequence has no limit to substitute; the algebra would be meaningless.
- **Assuming monotonicity is automatic.** It must be proved (often by induction),
  not eyeballed from a few terms.
- **Bounded *or* monotone alone.** Bounded but not monotone: $`(-1)^n`$ (diverges).
  Monotone but not bounded: $`a_n = n`$ (diverges to $`+\infty`$). You need both.

## Practice

1. Let $`a_1 = 1`$ and $`a_{n+1} = \tfrac12\!\left(a_n + \tfrac{2}{a_n}\right)`$. Show
   $`(a_n)`$ is decreasing for $`n \ge 1`$ after the first step, bounded below by
   $`\sqrt2`$, and find its limit.
2. Show the sequence $`b_n = \left(1 + \tfrac1n\right)^n`$ is increasing and bounded
   above by $`3`$, hence converges. *(Its limit is the number $`e`$.)*
3. Give an increasing sequence that does **not** converge, and explain which
   hypothesis fails.

<details>
<summary>Answers</summary>

1. (Newton's iteration for $`\sqrt2`$.) For $`a_n > 0`$, AM–GM gives
   $`a_{n+1} = \tfrac12(a_n + \tfrac2{a_n}) \ge \sqrt{a_n \cdot \tfrac2{a_n}} = \sqrt2`$,
   so $`a_n \ge \sqrt2`$ for $`n \ge 2`$. Then
   $`a_{n+1} - a_n = \tfrac12(\tfrac2{a_n} - a_n) = \tfrac{2 - a_n^2}{2a_n} \le 0`$,
   so decreasing and bounded below; the limit $`L`$ solves $`L = \tfrac12(L+\tfrac2L)`$,
   giving $`L = \sqrt2`$.
2. Standard; expand by the binomial theorem and compare term-by-term for
   monotonicity, and bound the sum by a geometric series for the bound $`< 3`$.
   Monotone + bounded $`\Rightarrow`$ converges (to $`e`$).
3. $`a_n = n`$: increasing but not bounded above, so the boundedness hypothesis
   fails and it diverges to $`+\infty`$.

</details>

## See also

- [Supremum, Infimum, and the Completeness of $`\mathbb{R}`$](./02-supremum-infimum.en.md)
- [The Nested Interval Theorem](./05-nested-intervals.en.md)
