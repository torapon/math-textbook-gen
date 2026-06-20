---
title: "Rules of Differentiation"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [08-functions-and-continuity, 12-derivative-definition]
---

# Rules of Differentiation

## Why this matters

Computing every derivative from the limit definition is exhausting and
unnecessary. Derivatives obey a small set of **algebraic rules** — for sums,
constant multiples, products, and quotients — that let us differentiate any
combination of known functions mechanically. This lesson states the four rules
and *proves* each one directly from the definition, so the machinery rests on
solid ground rather than memorized formulas.

Throughout, assume $`f`$ and $`g`$ are differentiable at $`a`$, and let $`c`$ be a
constant.

## Linearity: sums and constant multiples

> **Theorem (linearity).** $`f + g`$ and $`cf`$ are differentiable at $`a`$, with
> ```math
> (f + g)'(a) = f'(a) + g'(a), \qquad (cf)'(a) = c\,f'(a).
> ```

*Proof.* Split the difference quotient and pass to the limit:
```math
\frac{(f+g)(a+h) - (f+g)(a)}{h}
= \frac{f(a+h) - f(a)}{h} + \frac{g(a+h) - g(a)}{h}
\to f'(a) + g'(a),
```
using the [algebra of limits](./08-functions-and-continuity.en.md). The constant
multiple is identical: $`\dfrac{cf(a+h) - cf(a)}{h} = c\,\dfrac{f(a+h)-f(a)}{h} \to
c\,f'(a)`$. $`\blacksquare`$

Together these say differentiation is a *linear* operation: $`(\alpha f + \beta g)'
= \alpha f' + \beta g'`$.

## The product rule

The derivative of a product is **not** the product of the derivatives. The correct
rule mixes each function with the other's derivative.

> **Theorem (product rule).** $`fg`$ is differentiable at $`a`$, with
> ```math
> (fg)'(a) = f'(a)\,g(a) + f(a)\,g'(a).
> ```

*Proof.* The trick is to add and subtract $`f(a+h)\,g(a)`$ in the numerator so each
piece becomes a difference quotient:
```math
\begin{aligned}
\frac{f(a+h)g(a+h) - f(a)g(a)}{h}
&= \frac{f(a+h)\big[g(a+h) - g(a)\big] + g(a)\big[f(a+h) - f(a)\big]}{h} \\[2pt]
&= f(a+h)\,\frac{g(a+h) - g(a)}{h} + g(a)\,\frac{f(a+h) - f(a)}{h}.
\end{aligned}
```
Now let $`h \to 0`$. The quotients tend to $`g'(a)`$ and $`f'(a)`$; the factor
$`f(a+h) \to f(a)`$ because $`f`$, being differentiable, is
[continuous at $`a`$](./12-derivative-definition.en.md). The limit is therefore
$`f(a)g'(a) + g(a)f'(a)`$. $`\blacksquare`$

That callback matters: the product rule *needs* "differentiable $`\Rightarrow$
continuous" to know $`f(a+h) \to f(a)`$.

## The reciprocal and quotient rules

> **Theorem (reciprocal rule).** If $`g(a) \neq 0`$, then $`1/g`$ is differentiable at
> $`a`$, with
> ```math
> \left(\frac1g\right)'(a) = -\,\frac{g'(a)}{g(a)^2}.
> ```

*Proof.* Since $`g`$ is continuous and $`g(a) \neq 0`$, $`g`$ stays nonzero near $`a`$,
so the quotient below is defined for small $`h`$:
```math
\frac1h\left(\frac{1}{g(a+h)} - \frac{1}{g(a)}\right)
= -\,\frac{g(a+h) - g(a)}{h}\cdot\frac{1}{g(a+h)\,g(a)}
\to -\,g'(a)\cdot\frac{1}{g(a)^2},
```
using $`g(a+h) \to g(a)`$. $`\blacksquare`$

Writing $`f/g = f \cdot (1/g)`$ and combining the product and reciprocal rules gives
the quotient rule:

> **Theorem (quotient rule).** If $`g(a) \neq 0`$, then $`f/g`$ is differentiable at
> $`a`$, with
> ```math
> \left(\frac{f}{g}\right)'(a) = \frac{f'(a)\,g(a) - f(a)\,g'(a)}{g(a)^2}.
> ```

*Proof.*
```math
\left(\frac{f}{g}\right)' = f'\cdot\frac1g + f\cdot\left(-\frac{g'}{g^2}\right)
= \frac{f'}{g} - \frac{f g'}{g^2} = \frac{f'g - f g'}{g^2}. \qquad \blacksquare
```
The numerator order matters — it is "derivative of top times bottom *minus* top
times derivative of bottom," not the reverse.

## The power rule for positive integers

> **Corollary.** For every integer $`n \ge 1`$, $`\dfrac{d}{dx}\,x^n = n\,x^{n-1}`$.

*Proof (induction on $`n`$).* For $`n = 1`$, $`\dfrac{d}{dx}\,x = 1 = 1\cdot x^0`$.
Assuming $`\dfrac{d}{dx}\,x^n = n x^{n-1}`$, the product rule on $`x^{n+1} = x \cdot
x^n`$ gives
```math
\frac{d}{dx}\,x^{n+1} = 1\cdot x^n + x\cdot n x^{n-1} = x^n + n x^n = (n+1)\,x^n.
\qquad \blacksquare
```
With linearity, this differentiates **every polynomial** term by term. (The rule in
fact holds for all real exponents; we prove the general case once exponentials are
available.)

## Worked examples

**Example 1 — a polynomial.** For $`p(x) = 3x^4 - 5x^2 + 2x - 7`$, linearity and the
power rule give
```math
p'(x) = 3\cdot 4x^3 - 5\cdot 2x + 2 = 12x^3 - 10x + 2.
```
(The constant $`-7`$ contributes $`0`$.)

**Example 2 — a quotient.** For $`f(x) = \dfrac{x^2 - 1}{x^2 + 1}`$, the quotient rule
with top $`u = x^2-1`$, bottom $`v = x^2+1`$ gives
```math
f'(x) = \frac{(2x)(x^2+1) - (x^2-1)(2x)}{(x^2+1)^2}
= \frac{2x\big[(x^2+1) - (x^2-1)\big]}{(x^2+1)^2}
= \frac{4x}{(x^2+1)^2}.
```

## Common mistakes

- **$`(fg)' = f'g'`$.** False. Use $`f'g + fg'`$; the cross terms are essential.
- **Wrong sign or order in the quotient rule.** It is $`f'g - fg'`$ over $`g^2`$, not
  $`fg' - f'g`$. Mixing the order flips the sign of every answer.
- **Dropping the $`g^2`$.** The quotient and reciprocal rules divide by the *square*
  of the denominator.
- **Differentiating a constant to anything but $`0`$.** A constant has zero rate of
  change; $`c' = 0`$.
- **Forgetting continuity is doing work.** The product and reciprocal proofs rely on
  $`f(a+h) \to f(a)`$ and $`g(a+h) \to g(a)`$ — i.e. on differentiable $`\Rightarrow$
  continuous.

## Practice

1. Differentiate $`(2x^3 - x)(x^2 + 4)`$ two ways — by the product rule and by
   expanding first — and check the answers agree.
2. Differentiate $`\dfrac{x}{x^2 + 1}`$.
3. Use the reciprocal rule to differentiate $`\dfrac{1}{x^2 + 1}`$, then confirm via
   the quotient rule.
4. Derive the quotient rule's denominator power: explain why $`g^2`$, not $`g`$,
   appears.

<details>
<summary>Answers</summary>

1. Product rule: $`(6x^2 - 1)(x^2+4) + (2x^3 - x)(2x) = 6x^4 + 24x^2 - x^2 - 4 +
   4x^4 - 2x^2 = 10x^4 + 21x^2 - 4`$. Expanding first: $`2x^5 + 8x^3 - x^3 - 4x =
   2x^5 + 7x^3 - 4x`$, whose derivative is $`10x^4 + 21x^2 - 4`$. They match.
2. $`\dfrac{(1)(x^2+1) - x(2x)}{(x^2+1)^2} = \dfrac{1 - x^2}{(x^2+1)^2}`$.
3. Reciprocal: $`-\dfrac{2x}{(x^2+1)^2}`$. Quotient with top $`1`$ (derivative $`0`$):
   $`\dfrac{0\cdot(x^2+1) - 1\cdot 2x}{(x^2+1)^2} = -\dfrac{2x}{(x^2+1)^2}`$. Same.
4. From $`f/g = f\cdot(1/g)`$ and $`(1/g)' = -g'/g^2`$, the $`g^2`$ is inherited from
   the reciprocal rule, where it arises as $`\tfrac{1}{g(a+h)\,g(a)} \to \tfrac1{g^2}`$.

</details>

## See also

- [The Derivative: Definition and Differentiability](./12-derivative-definition.en.md)
- [Functions, Limits, and Continuity](./08-functions-and-continuity.en.md)
