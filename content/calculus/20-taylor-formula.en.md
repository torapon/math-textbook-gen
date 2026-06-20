---
title: "Taylor's Formula"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [16-chain-rule, 18-mean-value-theorem, 19-higher-order-derivatives]
---

# Taylor's Formula

## Why this matters

The [tangent line](./12-derivative-definition.en.md) approximates a function to
*first* order: $`f(x) \approx f(a) + f'(a)(x-a)`$. **Taylor's formula** is the
systematic upgrade — it uses the higher derivatives at $`a`$ to build the best
polynomial of any degree matching $`f`$ near $`a`$, and, crucially, gives an *exact
expression for the error*. This is how calculators evaluate $`e^x`$, $`\sin x`$, and
$`\ln x`$, and it is the gateway to power series. The formula is, quite literally, the
mean value theorem carried to higher order.

## The Taylor polynomial

> **Definition.** If $`f`$ is $`n`$ times differentiable at $`a`$, its *$`n`$-th Taylor
> polynomial* at $`a`$ is
> ```math
> P_{n}(x) = \sum_{k=0}^{n}\frac{f^{(k)}(a)}{k!}\,(x - a)^{k}
> = f(a) + f'(a)(x-a) + \frac{f''(a)}{2!}(x-a)^2 + \cdots + \frac{f^{(n)}(a)}{n!}(x-a)^n.
> ```

It is built so that $`P_n`$ and $`f`$ agree at $`a`$ through the $`n`$-th derivative:
$`P_n^{(k)}(a) = f^{(k)}(a)`$ for $`k = 0, 1, \dots, n`$. The degree-$`1`$ case
$`P_1(x) = f(a) + f'(a)(x-a)`$ is exactly the tangent-line approximation.

## Taylor's theorem with Lagrange remainder

How good is the approximation? The remainder $`R_n(x) = f(x) - P_n(x)`$ has a clean
closed form that looks like the *next* Taylor term, but with the derivative evaluated
at an unknown intermediate point.

> **Theorem (Taylor, Lagrange form).** Suppose $`f`$ is $`n+1`$ times differentiable on
> an open interval containing $`a`$ and $`x`$. Then there is a point $`\xi`$ strictly
> between $`a`$ and $`x`$ with
> ```math
> f(x) = P_{n}(x) + \frac{f^{(n+1)}(\xi)}{(n+1)!}\,(x - a)^{n+1}.
> ```

For $`n = 0`$ this reads $`f(x) = f(a) + f'(\xi)(x-a)`$ — precisely the
[mean value theorem](./18-mean-value-theorem.en.md). Taylor's theorem is its
higher-order generalization.

## Proof

We need one tool: the MVT for a *pair* of functions.

> **Lemma (Cauchy's generalized MVT).** If $`F, G`$ are continuous on $`[a,x]`$ and
> differentiable on $`(a,x)`$, with $`G' \neq 0`$ there, then for some $`\xi \in (a,x)`$
> ```math
> \frac{F(x) - F(a)}{G(x) - G(a)} = \frac{F'(\xi)}{G'(\xi)}.
> ```

*Proof of the lemma.* Apply [Rolle's theorem](./18-mean-value-theorem.en.md) to
$`\Phi(t) = \big(F(x) - F(a)\big)G(t) - \big(G(x) - G(a)\big)F(t)`$, which satisfies
$`\Phi(a) = \Phi(x) = F(x)G(a) - G(x)F(a)`$. Some $`\xi`$ has $`\Phi'(\xi) = 0`$, which
rearranges to the claim. $`\blacksquare`$

*Proof of the theorem.* Fix $`x`$ and view the Taylor expansion **about the moving
base point $`t`$**: define
```math
F(t) = f(x) - \sum_{k=0}^{n}\frac{f^{(k)}(t)}{k!}\,(x - t)^{k}, \qquad G(t) = (x - t)^{n+1}.
```
At the endpoints, $`F(x) = 0`$ and $`F(a) = f(x) - P_n(x) = R_n(x)`$, while $`G(x) = 0`$
and $`G(a) = (x-a)^{n+1}`$. The sum in $`F`$ **telescopes** when differentiated: every
term's two pieces cancel against neighbors, leaving only
```math
F'(t) = -\frac{f^{(n+1)}(t)}{n!}\,(x - t)^{n}, \qquad G'(t) = -(n+1)(x - t)^{n}.
```
Cauchy's lemma applied to $`F, G`$ gives a $`\xi`$ between $`a`$ and $`x`$ with
```math
\frac{F(a) - F(x)}{G(a) - G(x)} = \frac{F'(\xi)}{G'(\xi)}
= \frac{-\,f^{(n+1)}(\xi)\,(x-\xi)^n/n!}{-(n+1)(x-\xi)^n}
= \frac{f^{(n+1)}(\xi)}{(n+1)!}.
```
The left side is $`\dfrac{R_n(x)}{(x-a)^{n+1}}`$, so $`R_n(x) = \dfrac{f^{(n+1)}(\xi)}
{(n+1)!}(x-a)^{n+1}`$, as claimed. $`\blacksquare`$

## Familiar expansions about $`a = 0`$

Taylor polynomials at $`a = 0`$ (historically *Maclaurin* polynomials) recover the
series every student meets:
```math
e^{x} = 1 + x + \frac{x^2}{2!} + \cdots + \frac{x^n}{n!} + R_n,
\qquad
\sin x = x - \frac{x^3}{3!} + \frac{x^5}{5!} - \cdots,
```
```math
\cos x = 1 - \frac{x^2}{2!} + \frac{x^4}{4!} - \cdots,
\qquad
\ln(1+x) = x - \frac{x^2}{2} + \frac{x^3}{3} - \cdots.
```

## Worked example: approximating $`e^{0.1}`$ with a guaranteed error

Take $`f(x) = e^x`$, $`a = 0`$, $`n = 2`$, so $`P_2(x) = 1 + x + \tfrac{x^2}{2}`$ and
```math
e^{0.1} \approx P_2(0.1) = 1 + 0.1 + 0.005 = 1.105.
```
The remainder is $`R_2 = \dfrac{e^{\xi}}{3!}(0.1)^3`$ for some $`\xi \in (0, 0.1)`$.
Since $`e^{\xi} < e^{0.1} < 1.2`$, we get the rigorous bound
```math
|R_2| < \frac{1.2}{6}(0.001) = 0.0002.
```
So $`e^{0.1} = 1.105 \pm 0.0002`$ — and the true value $`1.10517\ldots`$ indeed lies in
that window. The strength of Taylor's theorem is exactly this: not just an estimate,
but a *certified* one.

## Common mistakes

- **Forgetting the factorials.** The coefficient of $`(x-a)^k`$ is $`f^{(k)}(a)/k!`$,
  not $`f^{(k)}(a)`$.
- **Treating $`\xi`$ as known.** Like the MVT's point, $`\xi`$ exists but is
  unspecified; it is used to *bound* $`R_n`$, by maximizing $`|f^{(n+1)}|`$ over the
  interval — never by "plugging in" a value.
- **Assuming more terms always means more accuracy everywhere.** The remainder must
  actually be shown to shrink; for some functions the Taylor series does not converge
  back to $`f`$ away from $`a`$.
- **Expanding about the wrong point.** All derivatives are evaluated at the base $`a`$;
  approximating near a different point requires re-expanding there.

## Practice

1. Write the degree-$`3`$ Taylor polynomial of $`\sin x`$ at $`a = 0`$.
2. Use the degree-$`1`$ Taylor formula to re-derive $`|\sin x - \sin y| \le |x-y|`$.
3. Approximate $`\sqrt{1.2}`$ using the degree-$`2`$ Taylor polynomial of
   $`\sqrt{1+x}`$ at $`0`$, and bound the error.
4. Show that the degree-$`n`$ Taylor remainder of $`e^x`$ at $`0`$ satisfies $`|R_n(x)|
   \le \dfrac{e^{|x|}\,|x|^{n+1}}{(n+1)!} \to 0`$ as $`n \to \infty`$ for every fixed
   $`x`$.

<details>
<summary>Answers</summary>

1. $`f', f'', f'''`$ at $`0`$ are $`1, 0, -1`$, so $`P_3(x) = x - \dfrac{x^3}{6}`$.
2. With $`n = 0`$ Taylor is the MVT: $`\sin x - \sin y = \cos(\xi)(x - y)`$, and
   $`|\cos\xi| \le 1`$ gives the bound.
3. $`f(x) = (1+x)^{1/2}`$: $`f(0)=1`$, $`f'(0)=\tfrac12`$, $`f''(0) = -\tfrac14`$, so
   $`P_2(x) = 1 + \tfrac{x}{2} - \tfrac{x^2}{8}`$ and $`P_2(0.2) = 1 + 0.1 - 0.005 =
   1.095`$. The remainder uses $`f'''(x) = \tfrac38(1+x)^{-5/2}`$, bounded by
   $`\tfrac38`$ on $`[0,0.2]`$, so $`|R_2| \le \tfrac{3/8}{6}(0.2)^3 = 0.0005`$.
   (True value $`\sqrt{1.2} = 1.0954\ldots`$.)
4. $`f^{(n+1)}(x) = e^x`$, and on the interval between $`0`$ and $`x`$ we have
   $`e^{\xi} \le e^{|x|}`$. Hence $`|R_n(x)| = \dfrac{e^{\xi}}{(n+1)!}|x|^{n+1} \le
   \dfrac{e^{|x|}|x|^{n+1}}{(n+1)!}`$, and the factorial dominates the power, so this
   $`\to 0`$. Thus the Taylor series of $`e^x`$ converges to $`e^x`$ everywhere.

</details>

## See also

- [Rolle's Theorem and the Mean Value Theorem](./18-mean-value-theorem.en.md)
- [Higher-Order Derivatives](./19-higher-order-derivatives.en.md)
- [The Derivative: Definition and Differentiability](./12-derivative-definition.en.md)
