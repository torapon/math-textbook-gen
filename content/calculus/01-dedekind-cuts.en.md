---
title: "Dedekind Cuts and the Continuity of the Real Numbers"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: []
---

# Dedekind Cuts and the Continuity of the Real Numbers

## Why this matters

The rational numbers $`\mathbb{Q}`$ look densely packed: between any two rationals
there is always another. Yet they are full of invisible **gaps**. There is no
rational number whose square is $`2`$, even though we can find rationals whose
squares are as close to $`2`$ as we like. If we try to do calculus on $`\mathbb{Q}`$,
limits that "should" exist fall through these gaps.

The real numbers $`\mathbb{R}`$ are built precisely to have *no gaps*. Making that
idea exact is the goal of this lesson. Dedekind's insight was to describe a
number not by a decimal expansion, but by **the way it splits the rationals into
a left part and a right part**.

## Definitions

> **Definition (cut).** A *cut* of $`\mathbb{Q}`$ is a pair $`(A, B)`$ of sets of
> rational numbers such that
>
> 1. $`A`$ and $`B`$ are both non-empty, and together they make up all of
>    $`\mathbb{Q}`$: $`\; A \cup B = \mathbb{Q}`$, $`\; A \cap B = \varnothing`$;
> 2. every element of $`A`$ is less than every element of $`B`$: if $`a \in A`$ and
>    $`b \in B`$ then $`a < b`$.

We call $`A`$ the *lower class* and $`B`$ the *upper class*. Intuitively a cut marks
a single place on the number line: everything to the left goes into $`A`$,
everything to the right into $`B`$.

## The three types of a cut

First, two terms we will lean on. The *greatest element* of a set is a member
that belongs to the set **and** is $`\ge`$ every other member; the *least element*
is a member that belongs to the set and is $`\le`$ every other member. A finite set
always has both, but an infinite set need **not**: for example
$`\{x \in \mathbb{Q} : x < 1\}`$ has no greatest element — whatever member you pick,
another member sits between it and $`1`$. This "may or may not exist" is exactly
what distinguishes the types below.

Because $`\mathbb{Q}`$ is **densely ordered** (between any two rationals lies a
third), one logical possibility is ruled out immediately: $`A`$ cannot have a
greatest element $`a^{*}`$ *and* $`B`$ a least element $`b^{*}`$ at the same time —
otherwise the rational $`\frac{a^{*} + b^{*}}{2}`$ would belong to neither class.
That leaves exactly three types:

| Type | Lower class $`A`$ | Upper class $`B`$ | Meaning |
|:----:|:----------------|:----------------|:--------|
| I  | has a greatest element | has **no** least element | the cut is *at* a rational |
| II | has **no** greatest element | has a least element | the cut is *at* a rational |
| III | has **no** greatest element | has **no** least element | the cut sits in a **gap** |

Types I and II both pin the cut to a specific rational number (the boundary
element). Type III is the interesting case: the cut points to a location where
**no rational number exists**. Each such gap is what we will call an *irrational
number*.

## Worked example: the cut that defines $`\sqrt{2}`$

**Problem.** Show that

```math
A = \{\, x \in \mathbb{Q} : x \le 0 \ \text{or}\ x^2 < 2 \,\}, \qquad
B = \{\, x \in \mathbb{Q} : x > 0 \ \text{and}\ x^2 > 2 \,\}
```

is a cut of $`\mathbb{Q}`$ of **Type III**.

First, $`(A,B)`$ really is a cut: every positive rational has $`x^2 < 2`$, $`x^2 = 2`$,
or $`x^2 > 2`$; since no rational satisfies $`x^2 = 2`$, every rational lands in
exactly one of $`A, B`$, and any $`a \in A`$ is smaller than any $`b \in B`$.

Now we show $`A`$ has **no greatest** element. Take any $`a \in A`$ with $`a > 0`$ (so
$`a^2 < 2`$) and look for a slightly larger rational still in $`A`$. Put

```math
a' = a + \frac{2 - a^2}{a + 2}\,= \frac{2a+2}{a+2}.
```

Then $`a' > a`$, and a short computation gives

```math
a'^2 - 2 = \frac{(2a+2)^2 - 2(a+2)^2}{(a+2)^2}
        = \frac{2(a^2 - 2)}{(a+2)^2} < 0,
```

so $`a'^2 < 2`$, i.e. $`a' \in A`$. Thus every element of $`A`$ is beaten by a larger
one — $`A`$ has no maximum. A symmetric argument shows $`B`$ has **no least**
element. Hence the cut is of Type III: it marks the gap we name $`\sqrt{2}`$. $`\blacksquare`$

## The continuity of $`\mathbb{R}`$

Real numbers are *defined* so that this gap problem disappears. The decisive
property is:

> **Dedekind's Theorem (continuity / completeness of $`\mathbb{R}`$).**
> For every cut $`(A, B)`$ of the **real** numbers there is exactly one real number
> $`\alpha`$ that produces it — that is, either $`\alpha`$ is the greatest element of
> $`A`$, or $`\alpha`$ is the least element of $`B`$. **No cut of $`\mathbb{R}`$ is of
> Type III.**

In words: the real line has no gaps. Every way of slicing $`\mathbb{R}`$ into a
left part and a right part is realized by an actual number sitting exactly at the
cut. This single statement — that there are no Type III cuts — is what we mean by
the **continuity of the real numbers**, and it is the foundation on which every
limit theorem in analysis ultimately rests.

## Proof of Dedekind's Theorem

From the standpoint that **constructs** the reals as cuts of $`\mathbb{Q}`$, this
theorem can be proved straight from the definition. The key idea is to **build the
number at the gap directly out of rationals**.

Fix one way to represent a real number. For each real $`\alpha`$, let

```math
\ell(\alpha) = \{\, q \in \mathbb{Q} : q < \alpha \,\}
```

be the set of all rationals below it — its *lower class*. In Dedekind's
construction we identify the real number $`\alpha`$ with this very set. Each
$`\ell(\alpha)`$ is non-empty, is not all of $`\mathbb{Q}`$, is downward closed (if
$`q \in \ell(\alpha)`$ and $`q' < q`$ then $`q' \in \ell(\alpha)`$), and has no greatest
element. Moreover, for a rational $`q`$ we have $`q \in \ell(\alpha) \iff q < \alpha`$,
and $`\alpha \le \beta \iff \ell(\alpha) \subseteq \ell(\beta)`$.

Now take any cut $`(A, B)`$ of $`\mathbb{R}`$ (here $`A, B`$ are sets of **real**
numbers). Form the set of rationals

```math
U = \bigcup_{\alpha \in A} \ell(\alpha),
```

the overlay of the lower classes of all the reals in $`A`$.

**$`U`$ defines a single real number.** We check that $`U`$ is a lower class with
the four properties above. Since $`A \neq \varnothing`$ and each
$`\ell(\alpha) \neq \varnothing`$, we get $`U \neq \varnothing`$. Pick $`\beta \in B`$; for
every $`\alpha \in A`$ we have $`\alpha < \beta`$, so $`\ell(\alpha) \subseteq \ell(\beta)`$,
giving $`U \subseteq \ell(\beta) \neq \mathbb{Q}`$; hence $`U \neq \mathbb{Q}`$. Downward
closure and the absence of a greatest element pass from each $`\ell(\alpha)`$ to the
union directly. So $`U = \ell(\gamma)`$ for a unique real $`\gamma`$. Note that **this
$`\gamma`$ — the number the cut points to — was built as a union of rationals,
without assuming completeness.**

**$`\gamma`$ is the boundary.** For each $`\alpha \in A`$, $`\ell(\alpha) \subseteq U = \ell(\gamma)`$,
so $`\alpha \le \gamma`$. For each $`\beta \in B`$, $`U \subseteq \ell(\beta)`$, i.e.
$`\ell(\gamma) \subseteq \ell(\beta)`$, so $`\gamma \le \beta`$.

**Conclusion.** Since $`A \cup B = \mathbb{R}`$, the real number $`\gamma`$ lies in
exactly one of $`A, B`$.

- If $`\gamma \in A`$: every $`\alpha \in A`$ has $`\alpha \le \gamma`$ and $`\gamma \in A`$,
  so $`\gamma = \max A`$ (Type I).
- If $`\gamma \in B`$: every $`\beta \in B`$ has $`\gamma \le \beta`$ and $`\gamma \in B`$,
  so $`\gamma = \min B`$ (Type II).

Either way a boundary element exists, so Type III cannot occur. $`\blacksquare`$

A Type III cut arose for $`\mathbb{Q}`$ (the $`\sqrt{2}`$ example) precisely because the
boundary $`\gamma`$ fell *outside* $`\mathbb{Q}`$, so neither class could catch it. Over
$`\mathbb{R}`$ the number $`\gamma`$ can always be constructed as a set of rationals, so
this never happens.

## Common mistakes

- **Requiring $`A`$ to have a maximum.** A cut need not have a boundary element in
  $`A`$; whether it does is exactly what distinguishes the types.
- **Thinking a Type III cut is "missing a number" in $`\mathbb{R}`$.** In
  $`\mathbb{Q}`$ it is; in $`\mathbb{R}`$ the gap is filled by definition. Type III
  cuts exist for $`\mathbb{Q}`$, never for $`\mathbb{R}`$.
- **Forgetting density.** The reason the "$`A`$ has a max and $`B`$ has a min" case
  is impossible is precisely the density of the order — drop density and the
  classification changes.

## Practice

1. Describe the cut of $`\mathbb{Q}`$ that corresponds to the rational number $`3`$.
   Which type is it — and is the *other* description of $`3`$ (max of $`A`$ vs. min
   of $`B`$) also a valid cut?
2. Explain why there is no Type III cut whose gap is the number $`1`$.
3. Let $`(A,B)`$ be the cut for $`\sqrt{2}`$ above. Show that for every $`\varepsilon > 0`$
   there are $`a \in A`$ and $`b \in B`$ with $`b - a < \varepsilon`$.

<details>
<summary>Answers</summary>

1. Either $`A = \{x : x < 3\},\, B = \{x : x \ge 3\}`$ (Type II, $`\min B = 3`$) or
   $`A = \{x : x \le 3\},\, B = \{x : x > 3\}`$ (Type I, $`\max A = 3`$). Both are
   valid; a single rational gives rise to a Type I and a Type II description, and
   we identify them as the same number $`3`$.
2. $`1`$ is rational, so it serves as $`\max A`$ (or $`\min B`$); the cut is Type I/II,
   not III. A gap exists only where no rational sits.
3. From the example, for $`a \in A,\ b \in B`$ both positive, $`a^2 < 2 < b^2`$, so
   $`b - a < \frac{b^2 - a^2}{a+b} = \frac{(b^2-2)+(2-a^2)}{a+b}`$. Choosing $`a, b`$
   with $`a^2, b^2`$ within $`\delta`$ of $`2`$ makes $`b-a`$ as small as desired.

</details>

## See also

- [Supremum, Infimum, and the Completeness of $`\mathbb{R}`$](./02-supremum-infimum.en.md)
