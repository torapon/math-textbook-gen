---
title: "Rolle's Theorem and the Mean Value Theorem"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [10-extreme-value-theorem, 12-derivative-definition]
---

# Rolle's Theorem and the Mean Value Theorem

## Why this matters

The derivative is defined *pointwise*, yet we constantly use it to draw *global*
conclusions: "$`f' > 0`$, so $`f`$ increases," "$`f' = 0`$, so $`f`$ is constant." The
bridge from local slope to global behavior is the **mean value theorem** (MVT).
Everything downstream — monotonicity tests, error bounds, Taylor's theorem — crosses
this bridge. We build it in three steps: an interior-extremum lemma, Rolle's
theorem, and then the MVT.

## Fermat's interior extremum lemma

> **Lemma (Fermat).** If $`f`$ has a local maximum or minimum at an *interior* point
> $`c`$ and is differentiable there, then $`f'(c) = 0`$.

*Proof.* Suppose $`c`$ is a local maximum, so $`f(c + h) \le f(c)`$ for all small $`h`$.
For $`h > 0`$ the difference quotient $`\dfrac{f(c+h) - f(c)}{h} \le 0`$, so taking the
limit, $`f'(c) \le 0`$. For $`h < 0`$ the quotient is $`\ge 0`$ (a non-positive numerator
over a negative denominator), so $`f'(c) \ge 0`$. Both hold, hence $`f'(c) = 0`$. (A
minimum is the same argument with inequalities reversed.) $`\blacksquare`$

Geometrically: at an interior peak or valley the tangent is horizontal. The word
*interior* is essential — at an endpoint only one side exists, and the slope need not
vanish.

## Rolle's theorem

> **Theorem (Rolle).** If $`f`$ is continuous on $`[a, b]`$, differentiable on
> $`(a, b)`$, and $`f(a) = f(b)`$, then there is a point $`c \in (a, b)`$ with
> $`f'(c) = 0`$.

*Proof.* By the [extreme value theorem](./10-extreme-value-theorem.en.md), $`f`$
attains a maximum and a minimum on $`[a, b]`$. If **both** are attained at the
endpoints, then — since $`f(a) = f(b)`$ — the maximum equals the minimum, so $`f`$ is
constant and $`f'(c) = 0`$ at every $`c \in (a,b)`$. Otherwise some extremum is attained
at an interior point $`c \in (a, b)`$; there $`f`$ is differentiable, so Fermat's lemma
gives $`f'(c) = 0`$. $`\blacksquare`$

## The mean value theorem

Rolle's theorem is the special case of a horizontal chord. Tilting it gives the
general statement: somewhere the tangent is parallel to the secant.

> **Theorem (Mean Value Theorem).** If $`f`$ is continuous on $`[a, b]`$ and
> differentiable on $`(a, b)`$, then there is a point $`c \in (a, b)`$ with
> ```math
> f'(c) = \frac{f(b) - f(a)}{b - a}.
> ```

*Proof.* Subtract off the secant line. Define
```math
h(x) = f(x) - f(a) - \frac{f(b) - f(a)}{b - a}\,(x - a),
```
which is continuous on $`[a,b]`$ and differentiable on $`(a,b)`$. A quick check gives
$`h(a) = 0`$ and $`h(b) = f(b) - f(a) - (f(b) - f(a)) = 0`$, so $`h(a) = h(b)`$. By
Rolle's theorem there is $`c \in (a,b)`$ with $`h'(c) = 0`$, that is,
```math
0 = h'(c) = f'(c) - \frac{f(b) - f(a)}{b - a}. \qquad \blacksquare
```

The quantity $`\dfrac{f(b)-f(a)}{b-a}`$ is the *average* rate of change over $`[a,b]`$;
the MVT says this average is achieved as an *instantaneous* rate at some interior
point.

## Consequences: from $`f'`$ back to $`f`$

These corollaries are why the MVT matters — they convert sign information about $`f'`$
into shape information about $`f`$. Throughout, $`f`$ is differentiable on an interval.

- **Zero derivative $`\Rightarrow`$ constant.** If $`f' = 0`$ everywhere, then for any
  $`x < y`$, MVT gives $`f(y) - f(x) = f'(c)(y - x) = 0`$, so $`f`$ is constant.
- **Equal derivatives $`\Rightarrow`$ differ by a constant.** If $`f' = g'`$, apply the
  above to $`f - g`$. (This is the uniqueness behind antiderivatives.)
- **Sign of $`f'`$ controls monotonicity.** If $`f' > 0`$ on the interval then $`f`$ is
  strictly increasing, since $`f(y) - f(x) = f'(c)(y - x) > 0`$ for $`x < y`$; likewise
  $`f' < 0`$ gives strictly decreasing, and $`f' \ge 0`$ gives non-decreasing.

## Worked example

**Problem.** Show $`|\sin x - \sin y| \le |x - y|`$ for all real $`x, y`$.

Apply the MVT to $`\sin`$ on the interval with endpoints $`x`$ and $`y`$: there is a
$`c`$ between them with
```math
\sin x - \sin y = \cos(c)\,(x - y).
```
Since $`|\cos c| \le 1`$, taking absolute values gives $`|\sin x - \sin y| =
|\cos c|\,|x - y| \le |x - y|`$.

**Answer.** The inequality holds — $`\sin`$ is *Lipschitz* with constant $`1`$. (The
same template turns any bound $`|f'| \le M`$ into $`|f(x) - f(y)| \le M|x - y|`$.)

## Common mistakes

- **Dropping a hypothesis.** The chord example $`f(x) = |x|`$ on $`[-1, 1]`$ has
  $`f(-1) = f(1)`$ but *no* interior zero of $`f'`$ — because $`f`$ is not differentiable
  at $`0`$. Rolle and the MVT need differentiability on the *whole* open interval.
- **Expecting a unique or located $`c`$.** The theorems assert *existence*; there may
  be several such $`c`$, and they give no formula.
- **Confusing the two intervals.** Continuity is required on the *closed* $`[a,b]`$
  (endpoints included), differentiability only on the *open* $`(a,b)`$.
- **Reading the conclusion backwards.** $`f' > 0`$ gives increasing; "increasing" does
  *not* give $`f' > 0`$ everywhere ($`f(x) = x^3`$ increases but $`f'(0) = 0`$).

## Practice

1. Verify Rolle's theorem for $`f(x) = x^2 - 2x`$ on $`[0, 2]`$: find the point $`c`$.
2. Use the MVT to prove $`\ln(1 + x) < x`$ for all $`x > 0`$.
3. Prove that if $`f'(x) = 0`$ for all $`x`$ in an interval, then $`f`$ is constant
   there.
4. Show $`|\arctan a - \arctan b| \le |a - b|`$.

<details>
<summary>Answers</summary>

1. $`f(0) = 0 = f(2)`$ and $`f'(x) = 2x - 2 = 0`$ at $`c = 1 \in (0,2)`$.
2. Apply the MVT to $`g(t) = \ln(1+t)`$ on $`[0, x]`$: $`\ln(1+x) - 0 = \dfrac{1}{1+c}\,x`$
   for some $`c \in (0, x)`$. Since $`c > 0`$, $`\dfrac{1}{1+c} < 1`$, so $`\ln(1+x) < x`$.
3. For any $`x < y`$ in the interval, MVT gives $`f(y) - f(x) = f'(c)(y - x) = 0`$, so
   $`f(y) = f(x)`$; the common value is the constant.
4. By the MVT, $`\arctan a - \arctan b = \dfrac{1}{1 + c^2}(a - b)`$ for some $`c`$.
   Since $`\dfrac{1}{1+c^2} \le 1`$, the absolute values give $`\le |a - b|`$.

</details>

## See also

- [The Extreme Value Theorem](./10-extreme-value-theorem.en.md)
- [The Derivative: Definition and Differentiability](./12-derivative-definition.en.md)
