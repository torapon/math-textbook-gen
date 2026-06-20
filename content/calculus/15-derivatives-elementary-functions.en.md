---
title: "Derivatives of the Elementary Functions"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [13-differentiation-rules, 14-exponential-and-logarithm]
---

# Derivatives of the Elementary Functions

## Why this matters

With the [rules of differentiation](./13-differentiation-rules.en.md) in hand, we
only need the derivatives of a few *building-block* functions; everything else is
assembled from them. This lesson proves the derivatives of the exponential, the
logarithm, and the trigonometric functions. Each proof reduces — via a difference
quotient — to a single limit we have already secured: $`\tfrac{e^h-1}{h} \to 1`$,
$`\tfrac{\ln(1+t)}{t} \to 1`$, or the geometric limit $`\tfrac{\sin x}{x} \to 1`$.

## The exponential is its own derivative

> **Theorem.** $`\dfrac{d}{dx}\,e^{x} = e^{x}.`$

*Proof.* Factor $`e^x`$ out of the difference quotient and use the functional
equation $`e^{x+h} = e^x e^h`$:
```math
\begin{aligned}
\frac{e^{x+h} - e^{x}}{h}
&= e^{x}\,\frac{e^{h} - 1}{h}
\xrightarrow{\ h \to 0\ } e^{x}\cdot 1 = e^{x},
\end{aligned}
```
by the [exponential limit](./14-exponential-and-logarithm.en.md). $`\blacksquare`$

This is the property that singles out $`e`$: among all bases, $`e^x`$ is the unique
exponential whose graph has slope exactly equal to its height.

## The logarithm

> **Theorem.** For $`x > 0`$, $`\dfrac{d}{dx}\,\ln x = \dfrac1x.`$

*Proof.* Write the difference quotient and substitute $`t = h/x`$ (so $`t \to 0`$ as
$`h \to 0`$):
```math
\frac{\ln(x+h) - \ln x}{h} = \frac1h\,\ln\!\left(1 + \frac{h}{x}\right)
= \frac1x\cdot\frac{\ln(1 + t)}{t} \xrightarrow{\ h \to 0\ } \frac1x\cdot 1 = \frac1x,
```
using $`\ln(x+h) - \ln x = \ln\frac{x+h}{x} = \ln(1+t)`$ and the
[logarithm limit](./14-exponential-and-logarithm.en.md). $`\blacksquare`$

(For $`x < 0`$ the same formula holds for $`\ln|x|`$: $`\dfrac{d}{dx}\ln|x| =
\dfrac1x`$ on $`x \neq 0`$.)

## The key trigonometric limit

The trigonometric derivatives all rest on one geometric fact. Take $`x`$ in
**radians** (this is the entire reason radians are the natural angle measure for
calculus). Comparing, on the unit circle, the areas of a triangle, a circular
sector, and a larger triangle gives, for $`0 < x < \tfrac\pi2`$,
```math
\sin x \le x \le \tan x.
```
Dividing by $`\sin x > 0`$ and inverting yields $`\cos x \le \dfrac{\sin x}{x} \le 1`$.
Since $`\cos x \to 1`$ as $`x \to 0`$, the squeeze theorem gives the limit (it is even
in $`x`$, so both sides agree):

> **Lemma.** $`\lim_{x \to 0}\frac{\sin x}{x} = 1`$, and consequently
> $`\lim_{x \to 0}\frac{1 - \cos x}{x} = 0.`$

*The second limit* follows by rationalizing:
```math
\begin{aligned}
\frac{1 - \cos x}{x}
&= \frac{1 - \cos^2 x}{x\,(1 + \cos x)} \\
&= \frac{\sin x}{x}\cdot\frac{\sin x}{1 + \cos x}
\to 1 \cdot \frac{0}{2} = 0.
\end{aligned}
```

## Sine and cosine

> **Theorem.** $`\dfrac{d}{dx}\,\sin x = \cos x`$ and $`\dfrac{d}{dx}\,\cos x = -\sin x.`$

*Proof.* Use the angle-addition formula $`\sin(x+h) = \sin x \cos h + \cos x \sin h`$:
```math
\frac{\sin(x+h) - \sin x}{h}
= \sin x\,\frac{\cos h - 1}{h} + \cos x\,\frac{\sin h}{h}
\xrightarrow{\ h \to 0\ } \sin x\cdot 0 + \cos x\cdot 1 = \cos x,
```
by the two limits above. The cosine is identical with $`\cos(x+h) = \cos x \cos h -
\sin x \sin h`$:
```math
\frac{\cos(x+h) - \cos x}{h} = \cos x\,\frac{\cos h - 1}{h} - \sin x\,\frac{\sin h}{h}
\to -\sin x. \qquad \blacksquare
```

## The tangent

With sine and cosine known, the quotient rule finishes the rest of the
trigonometric family. For $`\cos x \neq 0`$,
```math
\frac{d}{dx}\,\tan x = \frac{d}{dx}\,\frac{\sin x}{\cos x}
= \frac{\cos x \cos x - \sin x(-\sin x)}{\cos^2 x}
= \frac{\cos^2 x + \sin^2 x}{\cos^2 x} = \frac{1}{\cos^2 x} = \sec^2 x.
```

## Summary

| $`f(x)`$ | $`e^x`$ | $`\ln x`$ | $`\sin x`$ | $`\cos x`$ | $`\tan x`$ |
|---|---|---|---|---|---|
| $`f'(x)`$ | $`e^x`$ | $`1/x`$ | $`\cos x`$ | $`-\sin x`$ | $`\sec^2 x`$ |

(The general power rule $`\tfrac{d}{dx}x^r = r x^{r-1}`$ for *real* $`r`$, and
$`\tfrac{d}{dx}a^x = a^x \ln a`$, need the chain rule and are proved in the next
lesson.)

## Worked example

**Problem.** Differentiate $`f(x) = x^2 \ln x`$ and $`g(x) = e^x \sin x`$.

By the product rule,
```math
f'(x) = 2x\,\ln x + x^2\cdot\frac1x = 2x\ln x + x, \qquad
g'(x) = e^x \sin x + e^x \cos x = e^x(\sin x + \cos x).
```

## Common mistakes

- **$`\dfrac{d}{dx}e^x = x e^{x-1}`$.** No — that is the *power* rule misapplied. The
  exponent is the variable; $`\dfrac{d}{dx}e^x = e^x`$.
- **Differentiating $`\sin x`$ in degrees.** The clean rule $`\sin' = \cos`$ holds
  only in **radians**; degrees insert a factor $`\pi/180`$.
- **Forgetting the domain of $`\ln`$.** $`\tfrac{d}{dx}\ln x = 1/x`$ is for $`x > 0`$
  (or use $`\ln|x|`$ for $`x \neq 0`$).
- **Sign slip on $`\cos`$.** $`\dfrac{d}{dx}\cos x = -\sin x`$ — the minus is easy to
  drop.

## Practice

1. Differentiate $`\dfrac{\ln x}{x}`$.
2. Differentiate $`\dfrac{1}{\cos x}`$ (i.e. $`\sec x`$) and simplify.
3. Find $`\dfrac{d}{dx}\big(e^x \cos x\big)`$.
4. From the limit $`\tfrac{\sin x}{x}\to 1`$, evaluate $`\lim_{x\to0}\frac{\sin 5x}{\sin 2x}`$.

<details>
<summary>Answers</summary>

1. Quotient rule: $`\dfrac{(1/x)\,x - \ln x\cdot 1}{x^2} = \dfrac{1 - \ln x}{x^2}`$.
2. $`\dfrac{d}{dx}(\cos x)^{-1} = -\dfrac{-\sin x}{\cos^2 x} = \dfrac{\sin x}{\cos^2 x}
   = \sec x \tan x`$.
3. $`e^x \cos x + e^x(-\sin x) = e^x(\cos x - \sin x)`$.
4. $`\dfrac{\sin 5x}{\sin 2x} = \dfrac{\sin 5x}{5x}\cdot\dfrac{2x}{\sin 2x}\cdot\dfrac{5x}{2x}
   \to 1\cdot 1\cdot \dfrac52 = \dfrac52`$.

</details>

## See also

- [Rules of Differentiation](./13-differentiation-rules.en.md)
- [The Exponential and Logarithm](./14-exponential-and-logarithm.en.md)
