---
title: "Open and Closed Sets, Interior and Boundary"
subject: calculus
level: early-undergraduate
lang: en
prerequisites: [07-accumulation-points, 08-functions-and-continuity]
---

# Open and Closed Sets, Interior and Boundary

## Why this matters

Everything in this series — limits, continuity, the IVT — is ultimately about how
points sit near a set: *inside* it with room to spare, just *on its edge*, or
safely *outside*. Making this geometric language precise gives us **open sets**,
**closed sets**, and the **boundary**. These notions organize all of analysis
(and are the starting point of topology). This lesson collects the vocabulary and
the structural theorems, tying together the accumulation points of
[Lesson 07](./07-accumulation-points.en.md) with continuity.

## Classifying a point relative to a set

Let $S \subseteq \mathbb{R}$ and $x \in \mathbb{R}$. A *neighborhood* of $x$ is an
open interval $(x - \varepsilon, x + \varepsilon)$. Exactly one of three
descriptions applies to $x$:

> **Definitions.**
> - $x$ is an *interior point* of $S$ if some neighborhood of $x$ lies entirely
>   in $S$.
> - $x$ is an *exterior point* of $S$ if some neighborhood of $x$ lies entirely
>   outside $S$ (i.e. in the complement $S^c$).
> - $x$ is a *boundary point* of $S$ if every neighborhood of $x$ meets **both**
>   $S$ and $S^c$.

The collections are the *interior* $\operatorname{int}(S)$, the *exterior*, and
the *boundary* $\partial S$. They partition the whole line:
$\mathbb{R} = \operatorname{int}(S) \sqcup \partial S \sqcup \operatorname{ext}(S)$.
Interior points belong to $S$; exterior points do not; boundary points may or may
not.

For $S = (0, 1]$: interior $= (0,1)$, boundary $= \{0, 1\}$, exterior
$= (-\infty,0)\cup(1,\infty)$. Here $0 \in \partial S$ but $0 \notin S$, while
$1 \in \partial S$ and $1 \in S$.

## Open and closed sets

> **Definition (open / closed).**
> $S$ is *open* if every point of $S$ is an interior point — equivalently
> $S = \operatorname{int}(S)$, i.e. $S$ contains none of its boundary.
> $S$ is *closed* if it contains all of its boundary points (equivalently, all
> its [accumulation points](./07-accumulation-points.en.md)).

The single most important relationship between the two:

> **Theorem (duality).** $S$ is open $\iff$ its complement $S^c$ is closed.

*Why.* $S$ open means no point of $S$ is on the boundary, so the boundary
$\partial S = \partial S^c$ lies entirely in $S^c$ — which is exactly $S^c$ being
closed. (And $\partial S = \partial S^c$ always.) $\blacksquare$

**"Open" and "closed" are not opposites.** A set can be both, or neither:

| Set | Open? | Closed? |
|:----|:--:|:--:|
| $(0,1)$ | yes | no |
| $[0,1]$ | no | yes |
| $(0,1]$ | no | no |
| $\mathbb{R}$, $\varnothing$ | yes | yes |

Only $\mathbb{R}$ and $\varnothing$ are both open and closed (a fact equivalent to
the *connectedness* of the real line, the same property behind the IVT).

## Structural theorems

> **Theorem.**
> 1. $\mathbb{R}$ and $\varnothing$ are open.
> 2. **Any** union of open sets is open.
> 3. The intersection of **finitely many** open sets is open.
>
> Dually, by taking complements:
> 1. $\mathbb{R}$ and $\varnothing$ are closed.
> 2. **Any** intersection of closed sets is closed.
> 3. The union of **finitely many** closed sets is closed.

The finiteness in (3) is real. Infinitely many open sets can intersect to a
non-open set: $\bigcap_{n\ge1}\left(-\tfrac1n, \tfrac1n\right) = \{0\}$, which is
closed, not open. Dually $\bigcup_{n\ge1}\left[\tfrac1n, 1\right] = (0, 1]$ is
neither.

## Continuity, restated with open sets

Open sets give a strikingly clean restatement of continuity that needs no
$\varepsilon$ or $\delta$:

> **Theorem (topological continuity).** A function $f : \mathbb{R} \to \mathbb{R}$
> is continuous **if and only if** the preimage $f^{-1}(U)$ of every open set $U$
> is open.

This is the definition continuity takes in general topology. It says continuity is
not really about distances at all — only about which sets are open.

## Worked example

**Problem.** For $S = \{ \tfrac1n : n \ge 1 \}$, find
$\operatorname{int}(S)$, $\partial S$, and decide whether $S$ is open or closed.

- *Interior.* Each $\tfrac1n$ is isolated: a small enough neighborhood contains no
  *other* point of $S$, so it cannot lie inside $S$. Thus
  $\operatorname{int}(S) = \varnothing$ — $S$ has **no** interior points, so it is
  **not open**.
- *Boundary.* Every point $\tfrac1n$ is a boundary point (its neighborhoods meet
  $S$ at $\tfrac1n$ and meet $S^c$ in between). Also $0$ is a boundary point:
  every neighborhood of $0$ contains some $\tfrac1n \in S$ and also points not in
  $S$. So $\partial S = S \cup \{0\}$.
- *Closed?* The only accumulation point is $0$, and $0 \notin S$, so $S$ does not
  contain all its boundary — $S$ is **not closed**.

**Answer.** $\operatorname{int}(S) = \varnothing$,
$\partial S = \{0\} \cup \{\tfrac1n\}$; $S$ is neither open nor closed. (Adding the
point $0$ makes $S \cup \{0\}$ closed.)

## Common mistakes

- **Treating open and closed as opposites.** They are dual via complements, not
  negations; sets can be both or neither.
- **Putting boundary points in the interior.** An endpoint like $1 \in [0,1]$ is
  in the set but is a boundary point, not an interior point.
- **Intersecting infinitely many open sets and expecting open.** Only *finite*
  intersections stay open.
- **Confusing "boundary point of $S$" with "point of $S$."** A boundary point may
  lie outside $S$ (e.g. $0$ for $(0,1]$).

## Practice

1. Determine the interior, boundary, open-ness and closed-ness of $\mathbb{Q}$.
2. Show that $\operatorname{int}(S)$ is always open and that $\partial S$ is always
   closed.
3. Using the topological criterion, show $f(x) = x^2$ is continuous by describing
   $f^{-1}\big((a,b)\big)$ for $0 \le a < b$ and checking it is open.

<details>
<summary>Answers</summary>

1. Every neighborhood of any real contains both rationals and irrationals, so
   $\operatorname{int}(\mathbb{Q}) = \varnothing$ and
   $\partial \mathbb{Q} = \mathbb{R}$. Thus $\mathbb{Q}$ is neither open (empty
   interior, yet non-empty) nor closed (its accumulation points are all of
   $\mathbb{R}$).
2. If $x \in \operatorname{int}(S)$, some $(x-\varepsilon,x+\varepsilon)\subseteq S$;
   every point of that interval is also interior, so $\operatorname{int}(S)$ is
   open. $\partial S = \overline{S}\cap\overline{S^c}$ is an intersection of two
   closed sets (closures), hence closed. (Equivalently $(\partial S)^c =
   \operatorname{int}(S)\cup\operatorname{ext}(S)$ is a union of open sets, so
   open.)
3. For $0\le a<b$, $f^{-1}((a,b)) = (-\sqrt b,-\sqrt a)\cup(\sqrt a,\sqrt b)$ (with
   the convention $\sqrt a = 0$ when $a=0$, giving a single interval
   $(-\sqrt b,\sqrt b)$). Each piece is an open interval, so the preimage is open;
   preimages of general open sets are unions of such, hence open. So $f$ is
   continuous.

</details>

## See also

- [Accumulation Points and the Bolzano–Weierstrass Theorem](./07-accumulation-points.en.md)
- [Functions, Limits, and Continuity](./08-functions-and-continuity.en.md)
- [The Intermediate Value Theorem](./09-intermediate-value-theorem.en.md)
