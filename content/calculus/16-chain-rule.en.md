---
title: "The Chain Rule"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [12-derivative-definition, 13-differentiation-rules, 15-derivatives-elementary-functions]
---

# The Chain Rule

## Why this matters

Most functions we meet are **composites** — $`\sin(x^2)`$, $`e^{-x^2/2}`$,
$`\sqrt{1 + x^3}`$ — an outer function applied to an inner one. The **chain rule**
differentiates them, and it is the single most-used rule in all of calculus. Its
message is intuitive: if $`y`$ changes $`f'`$ times as fast as $`u`$, and $`u`$ changes
$`g'`$ times as fast as $`x`$, then $`y`$ changes $`f'\cdot g'`$ times as fast as $`x`$ —
rates of change **multiply** along the chain.

## Statement

> **Theorem (chain rule).** If $`g`$ is differentiable at $`a`$ and $`f`$ is
> differentiable at $`b = g(a)`$, then the composite $`f \circ g`$ is differentiable
> at $`a`$, with
> ```math
> (f \circ g)'(a) = f'\big(g(a)\big)\,\cdot\,g'(a).
> ```

In Leibniz notation, with $`y = f(u)`$ and $`u = g(x)`$, this is the memorable
```math
\frac{dy}{dx} = \frac{dy}{du}\cdot\frac{du}{dx},
```
where the symbols *behave* as if $`du`$ cancels — though, as always, each piece is a
limit, not a fraction.

## A careful proof

The tempting one-line proof multiplies and divides by $`g(a+h) - g(a)`$:
```math
\frac{f(g(a+h)) - f(g(a))}{h}
= \frac{f(g(a+h)) - f(g(a))}{g(a+h) - g(a)}\cdot\frac{g(a+h) - g(a)}{h}.
```
This is *almost* right but illegal when $`g(a+h) = g(a)`$ for $`h`$ near $`0`$ (the
first denominator vanishes). We repair it by packaging the outer difference quotient
into a function that is continuous even at $`0`$.

*Proof.* Let $`b = g(a)`$ and define
```math
\varphi(k) =
\begin{cases}
\dfrac{f(b + k) - f(b)}{k}, & k \neq 0,\\[6pt]
f'(b), & k = 0.
\end{cases}
```
Because $`f`$ is differentiable at $`b`$, $`\varphi(k) \to f'(b) = \varphi(0)`$ as
$`k \to 0`$, so $`\varphi`$ is **continuous at $`0`$**. Moreover, for *every* $`k`$
(including $`k = 0`$, where both sides are $`0`$),
```math
f(b + k) - f(b) = \varphi(k)\,k.
```
Now set $`k = g(a+h) - g(a)`$, so $`b + k = g(a+h)`$. Dividing the displayed identity
by $`h`$,
```math
\begin{aligned}
\frac{f(g(a+h)) - f(g(a))}{h}
&= \varphi\big(g(a+h) - g(a)\big)\cdot\frac{g(a+h) - g(a)}{h}.
\end{aligned}
```
Let $`h \to 0`$. Since $`g`$ is differentiable, it is
[continuous](./12-derivative-definition.en.md), so $`g(a+h) - g(a) \to 0`$; then
$`\varphi`$ being continuous at $`0`$ gives $`\varphi(g(a+h)-g(a)) \to \varphi(0) =
f'(b)`$. The second factor tends to $`g'(a)`$. Hence the product tends to
$`f'(b)\,g'(a) = f'(g(a))\,g'(a)`$. $`\blacksquare`$

The trick is exactly the device that makes the naive argument honest: $`\varphi`$
carries the value $`f'(b)`$ across the troublesome points where $`g`$ is momentarily
flat.

## Examples

Differentiate "outer first, then times the inner derivative":
```math
\frac{d}{dx}(x^2 + 1)^{10} = 10(x^2+1)^9\cdot 2x = 20x\,(x^2+1)^9,
```
```math
\frac{d}{dx}\,e^{x^2} = e^{x^2}\cdot 2x, \qquad
\frac{d}{dx}\,\sin(3x) = \cos(3x)\cdot 3, \qquad
\frac{d}{dx}\,\ln(\cos x) = \frac{1}{\cos x}\cdot(-\sin x) = -\tan x.
```
For longer chains the rule iterates — e.g. with three links,
```math
\frac{d}{dx}\,e^{\sin(x^2)} = e^{\sin(x^2)}\cdot\cos(x^2)\cdot 2x.
```

## Application: the general power rule

The chain rule, combined with $`x^r = e^{r\ln x}`$ (valid for $`x > 0`$), finally
proves the power rule for **every real exponent** $`r`$ — not just positive integers:
```math
\frac{d}{dx}\,x^{r} = \frac{d}{dx}\,e^{r\ln x} = e^{r\ln x}\cdot\frac{r}{x}
= x^{r}\cdot\frac{r}{x} = r\,x^{r-1}.
```
So $`\tfrac{d}{dx}\sqrt{x} = \tfrac12 x^{-1/2}`$ and $`\tfrac{d}{dx}\,x^{-1} =
-x^{-2}`$ are the same rule as for $`x^2`$.

## Application: a general base

Likewise $`a^{x} = e^{x\ln a}`$ (for $`a > 0`$) gives
```math
\frac{d}{dx}\,a^{x} = e^{x\ln a}\cdot\ln a = a^{x}\,\ln a,
\qquad\text{and}\qquad
\frac{d}{dx}\,\log_a x = \frac{d}{dx}\,\frac{\ln x}{\ln a} = \frac{1}{x\,\ln a}.
```
The factor $`\ln a`$ is exactly what disappears when $`a = e`$ — another way to see
why base $`e`$ is the natural one.

## Common mistakes

- **Forgetting the inner derivative.** $`\dfrac{d}{dx}\sin(3x) = 3\cos(3x)`$, *not*
  $`\cos(3x)`$. The factor $`g'`$ is the whole point.
- **Differentiating outer and inner at the same argument.** Evaluate $`f'`$ at
  $`g(a)`$, not at $`a`$: $`\dfrac{d}{dx}e^{x^2} = e^{x^2}\cdot 2x`$, never $`e^{2x}\cdot
  2x`$.
- **Stopping after two links.** Each layer contributes a factor; keep going until you
  reach $`x`$.
- **Cancelling $`du`$ literally.** $`\tfrac{dy}{du}\tfrac{du}{dx}`$ is a theorem about
  limits, not algebra on fractions — even though it looks like cancellation.

## Practice

1. Differentiate $`\sqrt{1 + x^3}`$.
2. Differentiate $`e^{-x^2/2}`$.
3. Differentiate $`\ln(1 + e^x)`$.
4. Differentiate $`\big(\sin x\big)^{n}`$ for a constant $`n`$, and $`\cos(\cos x)`$.

<details>
<summary>Answers</summary>

1. $`(1+x^3)^{1/2}`$: $`\tfrac12(1+x^3)^{-1/2}\cdot 3x^2 = \dfrac{3x^2}{2\sqrt{1+x^3}}`$.
2. $`e^{-x^2/2}\cdot(-x) = -x\,e^{-x^2/2}`$.
3. $`\dfrac{1}{1+e^x}\cdot e^x = \dfrac{e^x}{1+e^x}`$.
4. $`\dfrac{d}{dx}(\sin x)^n = n(\sin x)^{n-1}\cos x`$;
   $`\dfrac{d}{dx}\cos(\cos x) = -\sin(\cos x)\cdot(-\sin x) = \sin x\,\sin(\cos x)`$.

</details>

## See also

- [Rules of Differentiation](./13-differentiation-rules.en.md)
- [Derivatives of the Elementary Functions](./15-derivatives-elementary-functions.en.md)
- [The Exponential and Logarithm](./14-exponential-and-logarithm.en.md)
