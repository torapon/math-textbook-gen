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
