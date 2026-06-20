---
title: "The Exponential and Logarithm"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [02-supremum-infimum, 04-monotone-convergence, 09-intermediate-value-theorem, 12-derivative-definition]
---

# The Exponential and Logarithm

## Why this matters

The exponential $`e^x`$ and its inverse the natural logarithm $`\ln x`$ are the
functions of *growth* — compound interest, populations, decay, and (next lesson)
the one function that is its own derivative. We will not postulate them. The
foundations we have built — [monotone convergence](./04-monotone-convergence.en.md),
[completeness](./02-supremum-infimum.en.md), and the
[intermediate value theorem](./09-intermediate-value-theorem.en.md) — are exactly
enough to *construct* the number $`e`$, the function $`e^x`$, and $`\ln x`$ rigorously,
and to extract the two limits that will produce their derivatives.

## The number $`e`$

> **Definition.** $`\displaystyle e = \lim_{n \to \infty}\left(1 + \frac1n\right)^{n}.`$

This limit is not obvious — we must show the sequence $`a_n = (1 + 1/n)^n`$ actually
converges. By the [monotone convergence theorem](./04-monotone-convergence.en.md) it
suffices to show $`(a_n)`$ is **increasing** and **bounded above**. Expand with the
binomial theorem:
```math
a_n = \left(1 + \frac1n\right)^n
= \sum_{k=0}^{n} \frac{1}{k!}\prod_{j=0}^{k-1}\Big(1 - \frac{j}{n}\Big).
```
Each of the $`k`$ factors $`1 - j/n`$ lies in $`(0, 1]`$, which drives both facts we
need:

- **Increasing.** Passing from $`n`$ to $`n+1`$, every factor $`\big(1 - \tfrac{j}{n}\big)`$
  grows to $`\big(1 - \tfrac{j}{n+1}\big)`$, and an extra positive term is added. So
  $`a_{n+1} > a_n`$.
- **Bounded.** Each product of factors is $`\le 1`$, and $`k! \ge 2^{k-1}`$, so
  ```math
  a_n \le \sum_{k=0}^{n}\frac{1}{k!} \le 1 + \sum_{k=1}^{n}\frac{1}{2^{k-1}} < 1 + 2 = 3.
  ```

Since $`a_1 = 2`$ and the sequence increases, $`2 \le a_n < 3`$ for all $`n`$, and the
limit exists with $`2 < e \le 3`$. Its value is $`e = 2.71828\ldots`$ — irrational,
in fact transcendental.

## The exponential function

Replacing $`1`$ by a real parameter $`x`$ defines the exponential at every real
number.

> **Definition.** For $`x \in \mathbb{R}`$,
> $`\displaystyle e^{x} = \exp(x) = \lim_{n \to \infty}\left(1 + \frac{x}{n}\right)^{n}.`$

The same monotone-and-bounded reasoning (for $`n > |x|`$) shows this limit exists for
every $`x`$, and for rational $`x`$ it agrees with ordinary powers and roots of $`e`$,
which is why the notation $`e^x`$ is justified. We record its core properties.

> **Proposition.** The function $`\exp`$ satisfies:
> 1. $`\exp(0) = 1`$ and $`\exp(x) > 0`$ for all $`x`$;
> 2. $`\exp(x + y) = \exp(x)\,\exp(y)`$ (the *functional equation*);
> 3. $`\exp`$ is continuous and strictly increasing;
> 4. its range is all of $`(0, \infty)`$.

*Sketch.* For (2), the ratio of $`\big(1+\tfrac{x}{n}\big)\big(1+\tfrac{y}{n}\big)`$ to
$`\big(1 + \tfrac{x+y}{n}\big)`$ is $`1 + c_n`$ with $`c_n = \dfrac{xy/n^2}{1 + (x+y)/n}`$,
so $`n\,c_n \to 0`$ and hence $`(1 + c_n)^n \to 1`$; taking $`n`$-th powers and limits
turns the product $`\exp(x)\exp(y)`$ into $`\exp(x+y)`$. Positivity follows from
$`\exp(x) = \exp(x/2)^2 \ge 0`$ together with $`\exp(x)\exp(-x) = \exp(0) = 1 \neq 0`$.
Monotonicity and continuity come from the inequality below, and surjectivity onto
$`(0,\infty)`$ from the IVT, since $`\exp(x) \to \infty`$ as $`x \to \infty`$ and
$`\exp(x) \to 0`$ as $`x \to -\infty`$. $`\blacksquare`$

## The fundamental inequality

Everything quantitative about $`\exp`$ flows from one inequality, itself a one-line
consequence of **Bernoulli's inequality** $`(1 + t)^n \ge 1 + nt`$ (valid for
$`t \ge -1`$).

> **Lemma.** For every real $`x`$, $`\quad e^{x} \ge 1 + x,\quad`$ with equality only at
> $`x = 0`$.

*Proof.* For $`n > |x|`$ we have $`x/n > -1`$, so Bernoulli gives
$`\big(1 + \tfrac{x}{n}\big)^n \ge 1 + n\cdot\tfrac{x}{n} = 1 + x`$. Letting
$`n \to \infty`$ yields $`e^x \ge 1 + x`$. $`\blacksquare`$

Applied to $`-x`$, the lemma also gives $`e^{-x} \ge 1 - x`$, i.e.
```math
e^{x} \le \frac{1}{1 - x} \qquad (x < 1),
```
a matching upper bound near $`0`$.

## The limit behind the derivative

These two bounds pin down the exponential's behavior at $`0`$ exactly — the fact that
makes $`e^x`$ its own derivative next lesson.

> **Theorem.** $`\displaystyle \lim_{x \to 0} \frac{e^{x} - 1}{x} = 1.`$

*Proof.* For $`0 < x < 1`$, the lemma's lower bound gives $`e^x - 1 \ge x`$, so
$`\dfrac{e^x - 1}{x} \ge 1`$; the upper bound gives $`e^x - 1 \le \dfrac{x}{1 - x}`$, so
$`\dfrac{e^x - 1}{x} \le \dfrac{1}{1 - x}`$. Hence
```math
1 \le \frac{e^x - 1}{x} \le \frac{1}{1 - x} \xrightarrow{\ x \to 0^+\ } 1,
```
and the squeeze theorem forces the right-hand limit to be $`1`$. For $`-1 < x < 0`$ the
same two inequalities reverse the roles and squeeze from the other side (or
substitute $`x \mapsto -x`$). Both one-sided limits equal $`1`$. $`\blacksquare`$

## The natural logarithm

By the Proposition, $`\exp : \mathbb{R} \to (0, \infty)`$ is a continuous, strictly
increasing bijection. A strictly increasing continuous bijection has a continuous,
strictly increasing inverse — that inverse is the natural logarithm.

> **Definition.** $`\ln : (0, \infty) \to \mathbb{R}`$ is the inverse of $`\exp`$:
> ```math
> \ln y = x \iff e^{x} = y.
> ```

Inverting the functional equation turns products into sums:
```math
\ln 1 = 0, \quad \ln e = 1, \quad \ln(uv) = \ln u + \ln v, \quad \ln(u^{r}) = r\,\ln u,
```
and $`\ln`$ is strictly increasing with $`\ln y \to \infty`$ as $`y \to \infty`$,
$`\ln y \to -\infty`$ as $`y \to 0^+`$. The companion limit follows from the last
theorem by reciprocals.

> **Theorem.** $`\displaystyle \lim_{t \to 0} \frac{\ln(1 + t)}{t} = 1.`$

*Proof.* Put $`x = \ln(1 + t)`$, so $`t = e^{x} - 1`$, and by continuity of $`\ln`$
and $`\exp`$ we have $`t \to 0 \iff x \to 0`$. Then
```math
\frac{\ln(1 + t)}{t} = \frac{x}{e^{x} - 1} = \left(\frac{e^x - 1}{x}\right)^{-1}
\xrightarrow{\ x \to 0\ } 1^{-1} = 1. \qquad \blacksquare
```

## Worked example

**Problem.** Evaluate $`\displaystyle \lim_{x \to 0} \frac{e^{3x} - 1}{x}`$.

Write $`u = 3x`$, so $`u \to 0`$ as $`x \to 0`$ and
```math
\frac{e^{3x} - 1}{x} = 3\cdot\frac{e^{u} - 1}{u} \xrightarrow{\ x \to 0\ } 3 \cdot 1 = 3.
```
**Answer.** $`3`$. (More generally $`\lim_{x\to0}\dfrac{e^{ax}-1}{x} = a`$ — already a
hint that $`\dfrac{d}{dx}e^{ax} = a\,e^{ax}`$.)

## Common mistakes

- **Treating $`e`$ as merely "$`\approx 2.718`$".** Its *definition* is the limit
  $`(1+1/n)^n`$; the decimal is a consequence.
- **$`e^{x+y} = e^x + e^y`$.** No — exponentials turn **sums into products**:
  $`e^{x+y} = e^x e^y`$.
- **$`\ln(a + b) = \ln a + \ln b`$.** Also false; the log identity is
  $`\ln(ab) = \ln a + \ln b`$.
- **Taking $`\ln`$ of a non-positive number.** The domain of $`\ln`$ is $`(0,\infty)`$.
- **Confusing the two limits.** $`\dfrac{e^x-1}{x}`$ and $`\dfrac{\ln(1+t)}{t}`$ both
  tend to $`1`$ because they are reciprocals along $`t = e^x - 1`$.

## Practice

1. Show $`2 \le (1 + 1/n)^n < 3`$ for every $`n \ge 1`$.
2. From $`e^x \ge 1 + x`$ (all real $`x`$), deduce $`e^x \le \dfrac{1}{1-x}`$ for
   $`x < 1`$.
3. Evaluate $`\displaystyle\lim_{x \to 0}\frac{e^{ax} - 1}{x}`$ for a constant $`a`$.
4. Prove $`\ln(uv) = \ln u + \ln v`$ for $`u, v > 0`$ using $`e^{s+t} = e^s e^t`$.

<details>
<summary>Answers</summary>

1. Increasing with $`a_1 = 2`$ gives the lower bound; $`a_n \le \sum_{k=0}^n
   \tfrac1{k!} < 1 + \sum_{k\ge1} 2^{-(k-1)} = 3`$ gives the upper bound.
2. Apply the inequality to $`-x`$: $`e^{-x} \ge 1 - x`$. For $`x < 1`$ the right side is
   positive, so taking reciprocals (which reverses the inequality) gives $`e^{x} =
   1/e^{-x} \le 1/(1-x)`$.
3. Let $`u = ax`$: $`\dfrac{e^{ax}-1}{x} = a\cdot\dfrac{e^u - 1}{u} \to a`$. (For
   $`a = 0`$ the expression is identically $`0`$, consistent with the limit $`0`$.)
4. Let $`s = \ln u`$, $`t = \ln v`$, so $`e^s = u`$, $`e^t = v`$. Then $`uv = e^s e^t =
   e^{s+t}`$, so by definition $`\ln(uv) = s + t = \ln u + \ln v`$.

</details>

## See also

- [Monotone Bounded Sequences Converge](./04-monotone-convergence.en.md)
- [Supremum, Infimum, and Completeness](./02-supremum-infimum.en.md)
- [The Intermediate Value Theorem](./09-intermediate-value-theorem.en.md)
- [The Derivative: Definition and Differentiability](./12-derivative-definition.en.md)
