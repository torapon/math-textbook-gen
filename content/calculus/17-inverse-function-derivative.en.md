---
title: "The Derivative of an Inverse Function"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [09-intermediate-value-theorem, 12-derivative-definition, 16-chain-rule]
---

# The Derivative of an Inverse Function

## Why this matters

Many functions are defined as **inverses** of ones we already understand:
$`\sqrt{x}`$ undoes squaring, $`\ln x`$ undoes $`e^x`$, and $`\arcsin`$, $`\arctan`$
undo the trigonometric functions. Rather than differentiate each from scratch, one
clean rule gives the derivative of *any* inverse in terms of the original. The
geometry is vivid: the graph of $`f^{-1}`$ is the mirror image of the graph of $`f`$
across the line $`y = x`$, and reflection turns a slope into its **reciprocal**.

## When does an inverse exist?

First, recall when the inverse is even a function. A function that is **continuous
and strictly monotone** on an interval $`I`$ is injective, and by the
[intermediate value theorem](./09-intermediate-value-theorem.en.md) its image is an
interval $`J`$; so it has an inverse $`f^{-1} : J \to I`$, which is itself continuous
and strictly monotone. (This is exactly how $`\ln`$ arose as the inverse of $`e^x`$.)
With existence settled, we differentiate.

## The rule

> **Theorem (inverse function derivative).** Let $`f`$ be continuous and strictly
> monotone on an interval, differentiable at $`a`$ with $`f'(a) \neq 0`$, and let
> $`g = f^{-1}`$. Then $`g`$ is differentiable at $`b = f(a)`$, with
> ```math
> g'(b) = \frac{1}{f'(a)} = \frac{1}{f'\big(g(b)\big)}.
> ```

In Leibniz notation this is simply $`\dfrac{dx}{dy} = \dfrac{1}{\,dy/dx\,}`$ — the
derivative of the inverse is the reciprocal of the derivative.

*Proof.* Take $`k \neq 0`$ and set $`y = b + k`$, $`x = g(y)`$, so $`a = g(b)`$ and
$`f(x) = y`$, $`f(a) = b`$. Because $`g`$ is injective, $`y \neq b`$ forces $`x \neq a`$,
and because $`g`$ is continuous, $`x \to a`$ as $`k \to 0`$. Now flip the difference
quotient:
```math
\frac{g(b+k) - g(b)}{k} = \frac{x - a}{f(x) - f(a)} = \left(\frac{f(x) - f(a)}{x - a}\right)^{-1}.
```
As $`k \to 0`$ we have $`x \to a`$, so the inner quotient tends to $`f'(a) \neq 0`$, and
its reciprocal tends to $`1/f'(a)`$. $`\blacksquare`$

There is also a one-line *mnemonic* once you know $`g`$ is differentiable: apply the
[chain rule](./16-chain-rule.en.md) to the identity $`f(g(y)) = y`$, getting
$`f'(g(y))\,g'(y) = 1`$, hence $`g'(y) = 1/f'(g(y))`$. The proof above is what
*justifies* differentiating in the first place.

**Where it fails.** If $`f'(a) = 0`$, the tangent to $`f`$ is horizontal, so the
reflected tangent to $`g`$ is *vertical* and $`g`$ is not differentiable at $`b`$.
Example: $`f(x) = x^3`$ has $`f'(0) = 0`$, and its inverse $`g(y) = y^{1/3}`$ has a
vertical tangent at $`0`$.

## Examples

**Square root.** $`g(x) = \sqrt{x}`$ inverts $`f(x) = x^2`$ on $`[0,\infty)`$, where
$`f'(x) = 2x`$. So for $`x > 0`$,
```math
g'(x) = \frac{1}{f'(g(x))} = \frac{1}{2\sqrt{x}},
```
matching the power rule $`\tfrac{d}{dx}x^{1/2} = \tfrac12 x^{-1/2}`$.

**Logarithm, revisited.** $`\ln`$ inverts $`f(x) = e^x`$ with $`f' = e^x`$. Hence
```math
(\ln)'(y) = \frac{1}{e^{\ln y}} = \frac1y,
```
the same answer as before, now obtained purely from the inverse rule.

**Arcsine.** $`y = \arcsin x`$ means $`x = \sin y`$ with $`y \in [-\tfrac\pi2,
\tfrac\pi2]`$, where $`\cos y \ge 0`$. Since $`\sin' = \cos`$,
```math
\frac{d}{dx}\arcsin x = \frac{1}{\cos y} = \frac{1}{\sqrt{1 - \sin^2 y}} = \frac{1}{\sqrt{1 - x^2}}
\qquad (-1 < x < 1).
```

**Arctangent.** $`y = \arctan x`$ means $`x = \tan y`$; with $`\tan' = \sec^2 = 1 +
\tan^2`$,
```math
\frac{d}{dx}\arctan x = \frac{1}{\sec^2 y} = \frac{1}{1 + \tan^2 y} = \frac{1}{1 + x^2}.
```

## Common mistakes

- **Using the rule where $`f'(a) = 0`$.** A horizontal tangent reflects to a vertical
  one; the inverse is not differentiable there.
- **Evaluating $`f'`$ at the wrong point.** The reciprocal is $`1/f'(g(b))`$ — plug the
  inverse's *output* back into $`f'`$, not $`b`$ itself.
- **Confusing $`(f^{-1})'`$ with $`(1/f)'`$.** The derivative of the inverse function
  is not the derivative of the reciprocal $`1/f`$. They are unrelated.
- **Dropping the domain restriction.** $`\arcsin'`$ holds on $`(-1,1)`$;
  $`\arcsin`$ itself is defined on $`[-1,1]`$ but not differentiable at the endpoints.

## Practice

1. Using $`f(x) = x^n`$, derive $`\dfrac{d}{dx}x^{1/n} = \dfrac1n x^{1/n - 1}`$ for
   $`x > 0`$.
2. Find $`\dfrac{d}{dx}\arccos x`$ and compare it with $`\dfrac{d}{dx}\arcsin x`$.
3. Let $`f(x) = x + e^x`$. Show $`f`$ has a differentiable inverse $`g`$, and compute
   $`g'(1)`$. *(Hint: $`f(0) = 1`$.)*
4. Where is the inverse of $`f(x) = x^3 - 3x`$ non-differentiable? *(Hint: solve
   $`f'(x) = 0`$.)*

<details>
<summary>Answers</summary>

1. $`f'(x) = n x^{n-1}`$, $`g(x) = x^{1/n}`$, so $`g'(x) = \dfrac{1}{n\,(x^{1/n})^{n-1}}
   = \dfrac1n x^{-(n-1)/n} = \dfrac1n x^{1/n - 1}`$.
2. $`y = \arccos x`$, $`x = \cos y`$, $`\cos' = -\sin`$, and $`\sin y \ge 0`$ on
   $`[0,\pi]`$, so $`\dfrac{d}{dx}\arccos x = \dfrac{1}{-\sin y} = -\dfrac{1}{\sqrt{1-x^2}}`$
   — the negative of $`\arcsin'`$. (Indeed $`\arcsin x + \arccos x = \tfrac\pi2`$.)
3. $`f'(x) = 1 + e^x > 0`$, so $`f`$ is strictly increasing and continuous, hence
   invertible with a differentiable inverse where $`f' \neq 0`$ — that is, everywhere.
   Since $`f(0) = 1`$, $`g(1) = 0`$ and $`g'(1) = 1/f'(0) = 1/(1 + 1) = \tfrac12`$.
4. $`f'(x) = 3x^2 - 3 = 0`$ at $`x = \pm 1`$, giving points $`f(\pm 1) = \mp 2`$. The
   inverse has vertical tangents (is non-differentiable) at $`y = \mp 2`$. (Note $`f`$
   is not globally invertible here; restrict to a monotone piece.)

</details>

## See also

- [The Chain Rule](./16-chain-rule.en.md)
- [The Exponential and Logarithm](./14-exponential-and-logarithm.en.md)
- [The Intermediate Value Theorem](./09-intermediate-value-theorem.en.md)
