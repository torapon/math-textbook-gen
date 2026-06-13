---
title: "The Nested Interval Theorem"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [02-supremum-infimum, 04-monotone-convergence]
---

# The Nested Interval Theorem

## Why this matters

Many constructions in analysis trap a number by squeezing it between two bounds
that close in on each other: bisection methods, the binary expansion of a real
number, and the proof of the [intermediate value theorem](./09-intermediate-value-theorem.en.md)
all work this way. The nested interval theorem guarantees that such a squeeze
always catches **exactly one** real number — provided the lengths shrink to zero.
It is yet another face of completeness, and the most geometric one.

## Definitions

> **Definition (nested intervals).** A sequence of closed intervals
> $I_n = [a_n, b_n]$ is *nested* if
> $$
> I_1 \supseteq I_2 \supseteq I_3 \supseteq \cdots,
> \quad\text{i.e.}\quad a_n \le a_{n+1} \le b_{n+1} \le b_n \ \text{ for all } n.
> $$

Each interval sits inside the previous one. We say the lengths *shrink to zero*
if $b_n - a_n \to 0$.

## Key result

> **Theorem (Nested Intervals).** Let $I_n = [a_n, b_n]$ be nested **closed**
> intervals. Then their intersection is non-empty:
> $$
> \bigcap_{n=1}^{\infty} I_n \neq \varnothing.
> $$
> If moreover $b_n - a_n \to 0$, the intersection is a **single point**: there is
> a unique $\xi$ with $\{\xi\} = \bigcap_n I_n$, and $a_n \to \xi$, $b_n \to \xi$.

*Proof.* The left endpoints $(a_n)$ are increasing (nesting) and bounded above by
$b_1$ (since $a_n \le b_n \le b_1$). By the
[monotone convergence theorem](./04-monotone-convergence.en.md) they converge to
$\xi = \sup_n a_n$. Symmetrically $(b_n)$ decreases to $\eta = \inf_n b_n$, and
$a_n \le \xi \le \eta \le b_n$ for every $n$, so $[\xi, \eta] \subseteq I_n$ for
all $n$; thus $[\xi,\eta] \subseteq \bigcap_n I_n$, which is therefore non-empty.

If additionally $b_n - a_n \to 0$, then $0 \le \eta - \xi \le b_n - a_n \to 0$
forces $\eta = \xi$. Any point of the intersection lies in $[a_n, b_n]$ for all
$n$, hence equals $\xi$; so the intersection is exactly $\{\xi\}$. $\blacksquare$

## Two hypotheses you cannot drop

- **Closed.** With open intervals it fails: $J_n = \left(0, \tfrac1n\right)$ are
  nested but $\bigcap_n J_n = \varnothing$ — the would-be limit point $0$ is
  excluded from every interval.
- **Bounded.** With unbounded intervals it fails: $K_n = [n, \infty)$ are nested
  but $\bigcap_n K_n = \varnothing$. (The theorem is stated for finite closed
  intervals $[a_n,b_n]$.)

It also fails over $\mathbb{Q}$: intervals with rational endpoints closing in on
$\sqrt2$ have empty intersection *in $\mathbb{Q}$*. So the theorem, like the
others in this series, is a form of completeness.

## Worked example

**Problem.** Use bisection to locate a root of $f(x) = x^2 - 2$ in $[1, 2]$, and
explain what the nested interval theorem guarantees.

Start with $I_1 = [1,2]$: $f(1) = -1 < 0$, $f(2) = 2 > 0$. Evaluate at the
midpoint and keep the half on which $f$ changes sign:
$$
\begin{aligned}
&f(1.5) = 0.25 > 0 &&\Rightarrow I_2 = [1,\ 1.5]\\
&f(1.25) = -0.4375 < 0 &&\Rightarrow I_3 = [1.25,\ 1.5]\\
&f(1.375) = -0.109\ldots < 0 &&\Rightarrow I_4 = [1.375,\ 1.5]\\
&\vdots
\end{aligned}
$$
Each step halves the length: $b_n - a_n = \dfrac{1}{2^{\,n-1}} \to 0$, and the
intervals are nested and closed. By the theorem the intersection is a single
point $\xi$, with $a_n \to \xi$ and $b_n \to \xi$. Since $f(a_n) \le 0 \le f(b_n)$
and $f$ is continuous, passing to the limit gives $f(\xi) = 0$, i.e.
$\xi = \sqrt2$.

**Answer.** The nested intervals pin down the unique $\xi = \sqrt2 \in [1,2]$;
bisection is a constructive way to compute it to any accuracy.

## Common mistakes

- **Using open or half-open intervals.** Closedness is essential — the limit
  point can escape through a missing endpoint.
- **Forgetting the length condition for uniqueness.** Without $b_n - a_n \to 0$
  the intersection can be a whole interval (e.g. $I_n = [0,1]$ for all $n$ gives
  $\bigcap = [0,1]$).
- **Assuming the common point is rational.** The trapped $\xi$ is generally
  irrational; that is exactly why $\mathbb{Q}$ does not satisfy the theorem.

## Practice

1. Exhibit nested closed intervals with $b_n - a_n \to 0$ whose common point is
   $\tfrac13$, using only intervals with terminating-decimal endpoints.
2. Where does the proof break if the $I_n$ are open? Identify the exact step.
3. Show the nested interval theorem (with the length condition) implies that a
   bounded increasing sequence converges. *(Hint: build intervals from the terms
   and an upper bound.)*

<details>
<summary>Answers</summary>

1. $\tfrac13 = 0.3333\ldots$; take $I_n = [0.\underbrace{3\cdots3}_{n}, \;
   0.\underbrace{3\cdots3}_{n} + 10^{-n}]$, e.g. $[0.3,0.4], [0.33,0.34], \dots$
   Lengths $10^{-n}\to 0$, nested, and $\tfrac13$ lies in each.
2. The endpoints still converge ($a_n\uparrow\xi$, $b_n\downarrow\eta$), but for
   open $(a_n,b_n)$ the common point $\xi=\eta$ need not lie in any $(a_n,b_n)$ —
   the inclusion $[\xi,\eta]\subseteq I_n$ used closed endpoints. So the
   intersection can be empty.
3. Given increasing $(x_n)$ bounded above by $M$, set $I_n = [x_n, M]$… but lengths
   needn't shrink. Better: this direction is more naturally an *equivalence of
   completeness axioms*; a clean route is to bisect $[x_1, M]$, always keeping the
   half that still contains a tail of the sequence, producing nested intervals
   whose unique point is $\sup x_n = \lim x_n$.

</details>

## See also

- [Monotone Bounded Sequences Converge](./04-monotone-convergence.en.md)
- [Limit Superior and the Cauchy Criterion](./06-limsup-cauchy-criterion.en.md)
- [The Intermediate Value Theorem](./09-intermediate-value-theorem.en.md)
