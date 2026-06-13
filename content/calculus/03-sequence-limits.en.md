---
title: "Sequences and Their Limits"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [02-supremum-infimum]
---

# Sequences and Their Limits

## Why this matters

Almost every object in analysis — a derivative, an integral, the number $e$, the
sum of an infinite series — is secretly a **limit of a sequence**. Before we can
work with any of them rigorously, we need an airtight definition of what it means
for a list of numbers $a_1, a_2, a_3, \dots$ to "approach" a value $L$. The
intuitive phrase *"the terms get close to $L$"* is too vague: close how, and for
how long? The $\varepsilon$–$N$ definition makes it precise.

## Definitions

> **Definition (sequence).** A *sequence* of real numbers is a function
> $a : \mathbb{N} \to \mathbb{R}$, written $(a_n)_{n\ge 1}$ or just $(a_n)$, whose
> value at $n$ is the $n$-th *term* $a_n$.

> **Definition (limit / convergence).** A sequence $(a_n)$ *converges* to a real
> number $L$ if:
> $$
> \text{for every } \varepsilon > 0 \text{ there exists } N \in \mathbb{N}
> \text{ such that } \; n \ge N \implies |a_n - L| < \varepsilon.
> $$
> We then write $\displaystyle \lim_{n\to\infty} a_n = L$, or $a_n \to L$, and
> call $L$ the *limit*. If no such $L$ exists, $(a_n)$ *diverges*.

Read it as a challenge–response game. An adversary names a tolerance
$\varepsilon > 0$ (how close you must get). You must produce a threshold $N$ (a
point in the sequence) beyond which **every** term lies within $\varepsilon$ of
$L$. If you can always answer, no matter how tiny $\varepsilon$ is, the sequence
converges to $L$. The condition $|a_n - L| < \varepsilon$ means
$L - \varepsilon < a_n < L + \varepsilon$: from term $N$ on, the whole tail sits
inside the band of half-width $\varepsilon$ around $L$.

## Two basic facts

> **Theorem (uniqueness of limits).** A sequence has at most one limit.

*Proof.* Suppose $a_n \to L$ and $a_n \to L'$ with $L \neq L'$. Put
$\varepsilon = \tfrac{|L - L'|}{2} > 0$. For large $n$ we would need both
$|a_n - L| < \varepsilon$ and $|a_n - L'| < \varepsilon$, giving
$|L - L'| \le |L - a_n| + |a_n - L'| < 2\varepsilon = |L - L'|$, a contradiction.
$\blacksquare$

> **Theorem (convergent $\Rightarrow$ bounded).** Every convergent sequence is
> bounded.

*Proof.* If $a_n \to L$, take $\varepsilon = 1$: there is $N$ with $|a_n - L| < 1$
for $n \ge N$, so those terms lie in $(L-1, L+1)$. The finitely many earlier
terms $a_1, \dots, a_{N-1}$ are bounded too. Taking the largest and smallest of
all the bounds shows $(a_n)$ is bounded. $\blacksquare$

The converse fails — $a_n = (-1)^n$ is bounded but does not converge — so
boundedness alone is not enough. (The extra ingredient that rescues it,
monotonicity, is the subject of the [next lesson](./04-monotone-convergence.en.md).)

## Worked example

**Problem.** Prove directly from the definition that
$\displaystyle \lim_{n\to\infty} \frac{n+2}{2n+1} = \frac12$.

We estimate the gap to the candidate limit $L = \tfrac12$:
$$
\left| \frac{n+2}{2n+1} - \frac12 \right|
= \left| \frac{2(n+2) - (2n+1)}{2(2n+1)} \right|
= \frac{3}{2(2n+1)} < \frac{3}{4n}.
$$
Given $\varepsilon > 0$, this is $< \varepsilon$ as soon as $\frac{3}{4n} < \varepsilon$,
i.e. $n > \frac{3}{4\varepsilon}$. So choose any integer $N > \frac{3}{4\varepsilon}$.
Then for all $n \ge N$,
$$
\left| \frac{n+2}{2n+1} - \frac12 \right| < \frac{3}{4n} \le \frac{3}{4N} < \varepsilon.
$$
By the definition, the limit is $\tfrac12$. $\blacksquare$

Notice the strategy: bound $|a_n - L|$ above by a **simpler** expression
($\tfrac{3}{4n}$), then solve that for $n$. You never need the smallest valid $N$ —
any $N$ that works will do.

## Common mistakes

- **Swapping the quantifiers.** The order is "for all $\varepsilon$, there is
  $N$." $N$ is allowed to depend on $\varepsilon$ (smaller $\varepsilon$ usually
  needs larger $N$). Demanding one $N$ for all $\varepsilon$ is a different,
  much stronger condition.
- **Requiring $|a_n - L| < \varepsilon$ for *some* $n$.** It must hold for **all**
  $n \ge N$ — the entire tail, not a single lucky term.
- **Assuming bounded means convergent.** It does not; see $(-1)^n$.
- **Hunting for the optimal $N$.** Wasteful. Over-estimating $|a_n - L|$ by
  something simpler is the standard, fully rigorous shortcut.

## Practice

1. Using the definition, prove $\displaystyle \lim_{n\to\infty} \frac{1}{n^2} = 0$.
2. Prove that $a_n = (-1)^n$ diverges. *(Hint: suppose $a_n \to L$ and take
   $\varepsilon = 1$.)*
3. Show that if $a_n \to L$ and $a_n \ge 0$ for all $n$, then $L \ge 0$.

<details>
<summary>Answers</summary>

1. $\left|\frac{1}{n^2} - 0\right| = \frac{1}{n^2} \le \frac1n < \varepsilon$ when
   $n > \frac1\varepsilon$; take $N > \frac1\varepsilon$.
2. If $a_n \to L$, then for $\varepsilon = 1$ and large $n$ both $|1 - L| < 1$ and
   $|-1 - L| < 1$, so $|1-(-1)| = 2 \le |1-L| + |{-1}-L| < 2$, impossible.
3. If $L < 0$, take $\varepsilon = -L > 0$; for large $n$, $a_n < L + \varepsilon = 0$,
   contradicting $a_n \ge 0$. Hence $L \ge 0$. (Note strict $a_n > 0$ still only
   gives $L \ge 0$, e.g. $a_n = \frac1n$.)

</details>

## See also

- [Supremum, Infimum, and the Completeness of $\mathbb{R}$](./02-supremum-infimum.en.md)
- [Monotone Bounded Sequences Converge](./04-monotone-convergence.en.md)
