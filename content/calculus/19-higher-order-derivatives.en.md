---
title: "Higher-Order Derivatives"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [13-differentiation-rules, 16-chain-rule]
---

# Higher-Order Derivatives

## Why this matters

The derivative $`f'`$ is again a function, so we can differentiate it once more — and
again, and again. The **second derivative** measures how the rate of change is itself
changing: acceleration in physics, *concavity* in geometry. Higher derivatives encode
ever finer information about a function's shape, and assembling all of them at a point
is exactly what produces the Taylor approximation of the next lesson.

## Definition and notation

> **Definition.** The *second derivative* of $`f`$ is $`f'' = (f')'`$, and inductively
> the *$`n`$-th derivative* is $`f^{(n)} = \big(f^{(n-1)}\big)'`$, with $`f^{(0)} = f`$.

Common notations for the $`n`$-th derivative:
```math
f^{(n)}(x), \qquad \frac{d^{n} y}{dx^{n}}, \qquad \frac{d^{n}}{dx^{n}}f(x), \qquad \dot{}\,\ddot{}\ \text{(for } n=1,2 \text{ in physics)}.
```
A function with $`n`$ continuous derivatives is called $`C^{n}`$; one differentiable
infinitely often (like $`e^x`$ or $`\sin x`$) is **smooth**, written $`C^{\infty}`$.

## Patterns in the elementary functions

Repeated differentiation often falls into a pattern:

- **Polynomials** lose a degree each time and eventually vanish:
  $`\dfrac{d^{n}}{dx^{n}}x^{m} = 0`$ once $`n > m`$. In general
  $`\dfrac{d^{k}}{dx^{k}}x^{m} = \dfrac{m!}{(m-k)!}x^{m-k}`$ for $`k \le m`$.
- **The exponential** is a fixed point: $`\dfrac{d^{n}}{dx^{n}}e^{x} = e^{x}`$, and
  $`\dfrac{d^{n}}{dx^{n}}e^{ax} = a^{n}e^{ax}`$.
- **Sine and cosine** cycle with period $`4`$:
  ```math
  \frac{d^{n}}{dx^{n}}\sin x = \sin\!\Big(x + \frac{n\pi}{2}\Big),
  ```
  so $`\sin \to \cos \to -\sin \to -\cos \to \sin \to \cdots`$.

## Concavity: what $`f''`$ means

The sign of the second derivative describes the *bending* of the graph.

> If $`f'' > 0`$ on an interval, $`f'`$ is increasing, so the slope steepens and the
> graph is **convex** (curves upward). If $`f'' < 0`$, the graph is **concave** (curves
> downward). A point where the concavity switches is an **inflection point**.

This also sharpens optimization: at a critical point $`c`$ (where $`f'(c) = 0`$), $`f''(c)
> 0`$ signals a local minimum and $`f''(c) < 0`$ a local maximum — the *second
derivative test*.

## The Leibniz rule for products

The product rule iterates into a binomial formula — note the resemblance to
$`(a+b)^n`$.

> **Theorem (Leibniz rule).** If $`f, g`$ are $`n`$ times differentiable, then
> ```math
> (fg)^{(n)} = \sum_{k=0}^{n}\binom{n}{k}\,f^{(k)}\,g^{(n-k)}.
> ```

*Proof sketch.* Induction on $`n`$: differentiate the order-$`n`$ formula once and
collect terms using Pascal's identity $`\binom{n}{k} + \binom{n}{k-1} =
\binom{n+1}{k}`$, exactly as in the binomial theorem. $`\blacksquare`$

## Worked example

**Problem.** Find $`f''`$ for $`f(x) = x\,e^{x}`$, two ways.

*Directly:* $`f' = e^x + x e^x = (1+x)e^x`$, then $`f'' = e^x + (1+x)e^x = (2+x)e^x`$.

*By Leibniz* with $`u = x`$ (so $`u' = 1`$, $`u'' = 0`$) and $`v = e^x`$:
```math
f'' = \binom{2}{0}u\,v'' + \binom{2}{1}u'\,v' + \binom{2}{2}u''\,v
= x e^x + 2 e^x + 0 = (x + 2)e^x.
```
Both give $`f''(x) = (x+2)e^x`$.

## Common mistakes

- **Reading $`f^{(n)}`$ as a power.** $`f^{(3)}`$ is the third *derivative*, not
  $`f^3 = f\cdot f\cdot f`$. The parentheses are what distinguish them.
- **$`(fg)'' = f''g''`$.** False — use the Leibniz rule; the middle term $`2f'g'`$ is
  the one most often forgotten.
- **Confusing the smoothness classes.** $`C^1`$ (one continuous derivative) does not
  imply $`C^2`$. For example $`f(x) = x^2\sin(1/x)`$ (with $`f(0)=0`$) is differentiable
  everywhere but $`f'`$ is not continuous at $`0`$.
- **Assuming a critical point with $`f'' = 0`$ is an inflection.** $`f(x) = x^4`$ has
  $`f''(0) = 0`$ yet a strict minimum there; the test is inconclusive when $`f'' = 0`$.

## Practice

1. Compute the first four derivatives of $`f(x) = \cos x`$ and identify the cycle.
2. Find a general formula for $`\dfrac{d^{n}}{dx^{n}}\,\dfrac{1}{x}`$.
3. Use the Leibniz rule to compute $`(x^2 e^x)^{(n)}`$.
4. Determine the intervals where $`f(x) = x^3 - 3x`$ is convex or concave, and find its
   inflection point.

<details>
<summary>Answers</summary>

1. $`-\sin x,\ -\cos x,\ \sin x,\ \cos x`$ — back to the start after four steps
   (period $`4`$).
2. $`\dfrac{1}{x} = x^{-1}`$, so $`\dfrac{d^n}{dx^n}x^{-1} = (-1)(-2)\cdots(-n)\,x^{-1-n}
   = \dfrac{(-1)^n\,n!}{x^{n+1}}`$.
3. With $`u = x^2`$ ($`u'' = 2`$, higher $`= 0`$) and $`v = e^x`$:
   $`(x^2 e^x)^{(n)} = \big[x^2 + 2nx + n(n-1)\big]e^x`$ (only $`k = 0, 1, 2`$
   contribute).
4. $`f'' = 6x`$: concave on $`(-\infty, 0)`$ ($`f'' < 0`$), convex on $`(0, \infty)`$
   ($`f'' > 0`$), with an inflection point at $`x = 0`$.

</details>

## See also

- [Rules of Differentiation](./13-differentiation-rules.en.md)
- [The Chain Rule](./16-chain-rule.en.md)
