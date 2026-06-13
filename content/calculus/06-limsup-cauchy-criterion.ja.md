---
title: "上極限とコーシーの判定法"
subject: calculus
level: early-undergraduate
lang: ja
prerequisites: [03-sequence-limits, 04-monotone-convergence]
---

# 上極限とコーシーの判定法

## なぜ重要か

数列の理論には、まだ2つの限界があります。第一に、有界な数列でも極限をもたないことが
あります（$`(-1)^n`$）が、それでも長期的な *最大* と *最小* の値 — **上極限** と
**下極限** — は明確に定まり、これらは常に存在して数列の最終的な振る舞いを教えて
くれます。第二に、$`\varepsilon`$–$`N`$ による収束の定義は *極限を前もって知っている* こと
を要求します。**コーシーの判定法** はこの要求を取り除きます。項どうしが寄り集まる
ことを確かめるだけで、数列の項のみから収束を保証するのです。どちらの考えも、やはり
完備性によって支えられています。

## 上極限・下極限

有界な数列 $`(a_n)`$ に対し、*しっぽの上限・下限* を

```math
s_n = \sup_{k \ge n} a_k, \qquad t_n = \inf_{k \ge n} a_k
```

と定めます。$`n`$ が増えるとしっぽは縮むので、$`(s_n)`$ は減少、$`(t_n)`$ は増加し、ともに
有界です。[単調収束](./04-monotone-convergence.ja.md)によりこれらは収束します。

> **定義（上極限・下極限）.**
> ```math
> \limsup_{n\to\infty} a_n = \lim_{n\to\infty} s_n = \inf_{n} \sup_{k\ge n} a_k,
> \qquad
> \liminf_{n\to\infty} a_n = \lim_{n\to\infty} t_n = \sup_{n} \inf_{k\ge n} a_k.
> ```

これらは有界数列に対して **常に存在** します（非有界なら $`\pm\infty`$ を許す）。常に
$`\liminf a_n \le \limsup a_n`$ であり、これらは通常の収束を特徴づけます。

> **定理.** 有界数列が収束する $`\iff \liminf a_n = \limsup a_n`$ であり、このとき共通の
> 値が $`\lim a_n`$ である。

例えば $`a_n = (-1)^n`$ は $`\limsup = 1`$, $`\liminf = -1`$ で、その差が数列の続く振動の
大きさを測っています。

## コーシーの判定法

> **定義（コーシー列）.** $`(a_n)`$ が *コーシー列* であるとは、
> ```math
> \text{任意の } \varepsilon > 0 \text{ に対し、ある } N \text{ が存在して }
> m, n \ge N \implies |a_m - a_n| < \varepsilon
> ```
> が成り立つことをいいます。

項が最終的に **互いに** $`\varepsilon`$ 以内に収まる、という条件で、極限の値には触れて
いません。

> **定理（コーシーの判定法・完備性）.** 実数の数列が収束する **必要十分条件** は、
> コーシー列であることである。

*証明.*
($`\Rightarrow`$) $`a_n \to L`$ なら、$`m,n \ge N`$ で
$`|a_m - a_n| \le |a_m - L| + |L - a_n| < \tfrac\varepsilon2 + \tfrac\varepsilon2
= \varepsilon`$。

($`\Leftarrow`$) $`(a_n)`$ をコーシー列とします。これは **有界** です（$`\varepsilon = 1`$ を
とると、$`N`$ 以降の項はすべて $`a_N`$ から $`1`$ 以内にあり、それ以前は有限個）。有界
なので $`L = \limsup a_n`$ は有限。$`\varepsilon`$ に対し $`m,n\ge N`$ で
$`|a_m - a_n| < \tfrac\varepsilon2`$ となる $`N`$ をとると、無限個の項が $`L`$ から
$`\tfrac\varepsilon2`$ 以内に来るので、そのうちの1つ $`a_m`$（$`m \ge N`$）は
$`|a_m - L| < \tfrac\varepsilon2`$ を満たし、$`n \ge N`$ なるすべての $`n`$ で
$`|a_n - L| \le |a_n - a_m| + |a_m - L| < \varepsilon`$。ゆえに $`a_n \to L`$。$`\blacksquare`$

この同値性は **形を変えた完備性** です。$`\mathbb{Q}`$ 上では、$`\sqrt2`$ を近似する有理数
の列はコーシー列ですが有理数の極限をもちません。コーシーの判定法が成り立つのは、
まさに $`\mathbb{R}`$ にすき間がないからです。

## 例題

**問題.** $`a_n = \displaystyle\sum_{k=1}^{n} \frac{1}{k^2}`$ が、値を計算せずに、
コーシー列であることを確かめて収束することを示しなさい。

$`m > n`$ に対し、

```math
|a_m - a_n| = \sum_{k=n+1}^{m} \frac{1}{k^2}
< \sum_{k=n+1}^{m} \frac{1}{k(k-1)}
= \sum_{k=n+1}^{m}\!\left(\frac{1}{k-1} - \frac{1}{k}\right)
= \frac1n - \frac1m < \frac1n.
```

ここで望遠鏡和の評価 $`\frac{1}{k^2} < \frac{1}{k(k-1)}`$ を用いました。
$`\varepsilon > 0`$ に対し $`N > \tfrac1\varepsilon`$ をとれば、$`m > n \ge N`$ で
$`|a_m - a_n| < \tfrac1n \le \tfrac1N < \varepsilon`$。よって $`(a_n)`$ はコーシー列で、
収束します。

**答え.** 級数 $`\sum 1/k^2`$ は収束します。（その値は $`\pi^2/6`$ ですが、コーシーの
判定法はそれなしに極限の *存在* を証明します。）

## よくある間違い

- **隣り合う項だけを調べる。** $`|a_{n+1} - a_n| \to 0`$ はコーシー列を **意味しません**。
  調和和 $`a_n = \sum_{k=1}^n \tfrac1k`$ は $`a_{n+1}-a_n = \tfrac1{n+1} \to 0`$ でも
  発散します。*すべての* 大きい $`m, n`$ について $`|a_m - a_n|`$ を抑える必要があります。
- **上極限と上限を混同する。** $`\sup_n a_n`$ は数列全体を見ますが、$`\limsup`$ は有限個の
  先頭を無視して長期的な振る舞いだけを捉えます。
- **$`\mathbb{Q}`$ でコーシーの判定法を期待する。** 収束を特徴づけるのは完備な空間に
  おいてだけです。

## 練習問題

1. $`a_n = (-1)^n\!\left(1 + \tfrac1n\right)`$ の $`\limsup`$ と $`\liminf`$ を求めなさい。
2. コーシー列が有界であることを直接証明しなさい。
3. $`a_n = \sum_{k=1}^{n}\tfrac{1}{k}`$ が **コーシー列でない** ことを、$`\varepsilon =
   \tfrac12`$ に対して、どんなに大きい $`N`$ でも $`|a_m - a_n| \ge \tfrac12`$ となる
   $`m,n`$ を示して証明しなさい。*（ヒント：$`a_{2n}`$ と $`a_n`$ を比べる。）*

<details>
<summary>解答</summary>

1. 偶数 $`n`$：$`a_n = 1 + \tfrac1n \downarrow 1`$；奇数 $`n`$：$`a_n = -(1+\tfrac1n)
   \uparrow -1`$。よって $`\limsup = 1`$, $`\liminf = -1`$。
2. $`\varepsilon = 1`$ をとり、$`n \ge N`$ で $`|a_n - a_N| < 1`$ となる $`N`$ を得ると、
   それらは $`(a_N - 1, a_N + 1)`$ に入る。有限個の $`a_1,\dots,a_{N-1}`$ と合わせて
   全体の有界性が出る。
3. $`a_{2n} - a_n = \sum_{k=n+1}^{2n}\tfrac1k \ge n \cdot \tfrac{1}{2n} = \tfrac12`$。
   任意の $`N`$ に対し $`n \ge N`$ と $`m = 2n`$ をとれば $`|a_m - a_n| \ge \tfrac12`$。
   コーシー列でないので発散する。

</details>

## 関連項目

- [有界な単調数列は収束する](./04-monotone-convergence.ja.md)
- [集積点とボルツァーノ・ワイエルシュトラスの定理](./07-accumulation-points.ja.md)
