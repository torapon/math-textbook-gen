---
title: "The Derivative: Definition and Differentiability"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [03-sequence-limits, 08-functions-and-continuity]
---

# The Derivative: Definition and Differentiability

## Why this matters

Continuity told us a function has no jumps. The **derivative** asks a sharper
question: *how fast* is the function changing, and in *which direction* does its
graph point? The answer is the slope of the tangent line — the best straight-line
approximation to the curve at a point. Averaged over an interval, "slope" is just
rise over run; the derivative is what that average becomes as the interval shrinks
to a single instant. Every later idea — optimization, the mean value theorem,
Taylor approximation — is built on this one limit.

## The difference quotient and the derivative

Fix a point $`a`$ in the domain. Over the interval from $`a`$ to a nearby point, the
**average rate of change** of $`f`$ is the slope of the secant line:
```math
\frac{f(a + h) - f(a)}{h} \qquad (h \neq 0).
```
This is the *difference quotient*. Letting the second point slide toward $`a`$ — that
is, $`h \to 0`$ — turns the secant into the tangent, if the limit exists.

> **Definition (derivative).** $`f`$ is *differentiable at* $`a`$ if the limit
> ```math
> f'(a) = \lim_{h \to 0} \frac{f(a + h) - f(a)}{h}
> ```
> exists (as a finite number). Equivalently, substituting $`x = a + h`$,
> ```math
> f'(a) = \lim_{x \to a} \frac{f(x) - f(a)}{x - a}.
> ```
> The value $`f'(a)`$ is the *derivative* of $`f`$ at $`a`$. If $`f`$ is differentiable
> at every point of an open interval, the rule $`x \mapsto f'(x)`$ is the *derivative
> function* $`f'`$.

Notice the quotient is only ever evaluated for $`h \neq 0`$ (or $`x \neq a`$): we never
divide by zero. The limit, as always, is about what the quotient *approaches*, not
its value at the forbidden point — exactly the situation the
[function-limit definition](./08-functions-and-continuity.en.md) was built for.

> **Notation.** The same derivative is written several ways:
> ```math
> f'(a), \qquad \frac{df}{dx}\bigg|_{x=a}, \qquad \frac{dy}{dx}, \qquad \dot{y}.
> ```
> Lagrange's $`f'`$, Leibniz's $`\tfrac{dy}{dx}`$ (read as a single symbol, not a real
> quotient — though it behaves like one), and Newton's $`\dot y`$ (common for time
> derivatives) all denote the same thing.

## The tangent line and linear approximation

Geometrically, $`f'(a)`$ is the slope of the **tangent line** to the graph at
$`\big(a, f(a)\big)`$:
```math
y = f(a) + f'(a)\,(x - a).
```
Reading this as an approximation gives the single most useful consequence of
differentiability — near $`a`$, the curve is almost its tangent line:
```math
f(x) \approx f(a) + f'(a)\,(x - a) \qquad (x \text{ near } a).
```
"Differentiable" means precisely that such a *linear* approximation exists and is
accurate to first order. This is the seed of Taylor's formula.

## Worked examples

**Example 1 — a power.** Let $`f(x) = x^2`$. Then
```math
\frac{(a+h)^2 - a^2}{h} = \frac{2ah + h^2}{h} = 2a + h \xrightarrow{\ h \to 0\ } 2a,
```
so $`f'(a) = 2a`$. (We could cancel $`h`$ because $`h \neq 0`$ inside the limit.)

**Example 2 — a reciprocal.** Let $`f(x) = \dfrac1x`$ for $`x \neq 0`$. Then
```math
\frac{1}{h}\left(\frac{1}{a+h} - \frac1a\right)
= \frac{1}{h}\cdot\frac{a - (a+h)}{a(a+h)}
= \frac{-1}{a(a+h)} \xrightarrow{\ h \to 0\ } -\frac{1}{a^2}.
```
So $`\dfrac{d}{dx}\,\dfrac1x = -\dfrac{1}{x^2}`$.

## Differentiability implies continuity

Differentiability is a *stronger* condition than continuity — it cannot hold where
the function jumps.

> **Theorem.** If $`f`$ is differentiable at $`a`$, then $`f`$ is continuous at $`a`$.

*Proof.* For $`x \neq a`$ write the identity
```math
f(x) - f(a) = \frac{f(x) - f(a)}{x - a}\,\cdot\,(x - a).
```
As $`x \to a`$ the first factor tends to $`f'(a)`$ (a finite number, since $`f`$ is
differentiable) and the second tends to $`0`$. By the
[algebra of limits](./08-functions-and-continuity.en.md), the product tends to
$`f'(a) \cdot 0 = 0`$. Hence $`f(x) - f(a) \to 0`$, i.e. $`f(x) \to f(a)`$, which is
continuity at $`a`$. $`\blacksquare`$

## The converse is false

Continuity does **not** imply differentiability. The standard example is the
absolute value $`f(x) = |x|`$ at $`a = 0`$. Its difference quotient is
```math
\frac{|0 + h| - |0|}{h} = \frac{|h|}{h} = \mathrm{sign}(h),
```
which equals $`+1`$ for $`h > 0`$ and $`-1`$ for $`h < 0`$. The right- and left-hand
limits disagree, so the limit does not exist: $`|x|`$ is continuous everywhere but
not differentiable at $`0`$. Geometrically the graph has a **corner** — there is no
single tangent line. (Far more dramatically, Weierstrass exhibited a function that
is continuous at *every* point yet differentiable at *none*; continuity is genuinely
weaker.)

## Common mistakes

- **Assuming continuous $`\Rightarrow`$ differentiable.** A corner like $`|x|`$ is
  continuous but has no derivative there. The implication only runs one way.
- **Forgetting both one-sided limits must agree.** The derivative exists only when
  the difference quotient has the *same* limit from both sides.
- **Confusing $`f'(a)`$ with $`f'`$.** $`f'(a)`$ is a number (a slope at one point);
  $`f'`$ is the function assembling those slopes.
- **Worrying about division by zero.** The quotient is taken at $`h \neq 0`$; the
  limit then handles $`h \to 0`$. Cancel freely before passing to the limit.
- **Reading $`\tfrac{dy}{dx}`$ as a fraction.** It is one symbol for a limit. (It is
  often *manipulated* like a fraction — the chain rule is why — but it is not one.)

## Practice

1. From the definition, show $`f(x) = x^3`$ has $`f'(a) = 3a^2`$.
2. From the definition, show $`f(x) = \sqrt{x}`$ has $`f'(a) = \dfrac{1}{2\sqrt a}`$
   for $`a > 0`$.
3. Show $`f(x) = x\,|x|`$ is differentiable at $`0`$ and find $`f'(0)`$, even though
   the formula changes sign at $`0`$.
4. At which points is $`f(x) = |x^2 - 1|`$ not differentiable? Explain.

<details>
<summary>Answers</summary>

1. $`\dfrac{(a+h)^3 - a^3}{h} = \dfrac{3a^2 h + 3a h^2 + h^3}{h} = 3a^2 + 3ah + h^2
   \to 3a^2`$.
2. $`\dfrac{\sqrt{a+h} - \sqrt a}{h} = \dfrac{(a+h) - a}{h\big(\sqrt{a+h} + \sqrt a\big)}
   = \dfrac{1}{\sqrt{a+h} + \sqrt a} \to \dfrac{1}{2\sqrt a}`$ (rationalizing the
   numerator).
3. $`\dfrac{h\,|h| - 0}{h} = |h| \to 0`$, so $`f'(0) = 0`$. (In fact $`f(x) = x|x|`$ is
   differentiable everywhere with $`f'(x) = 2|x|`$; at $`0`$ the two one-sided slopes
   both equal $`0`$, so there is no corner.)
4. At $`x = \pm 1`$. There $`x^2 - 1`$ crosses zero, so $`|x^2 - 1|`$ reflects and forms
   a corner (one-sided slopes $`\mp 2`$ and $`\pm 2`$ disagree). Elsewhere $`f`$ is a
   smooth piece of $`\pm(x^2 - 1)`$ and is differentiable.

</details>

## See also

- [Functions, Limits, and Continuity](./08-functions-and-continuity.en.md)
- [Rules of Differentiation](./13-differentiation-rules.en.md)
