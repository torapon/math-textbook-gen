---
title: "指数関数と対数関数"
subject: calculus
level: early-undergraduate
lang: ja
prerequisites: [02-supremum-infimum, 04-monotone-convergence, 09-intermediate-value-theorem, 12-derivative-definition]
---

# 指数関数と対数関数

## なぜ重要か

指数関数 $`e^x`$ と、その逆関数である自然対数 $`\ln x`$ は *成長* の関数です — 複利、
人口、減衰、そして（次のレッスンで）自分自身を導関数にもつ唯一の関数です。これらを
公理として仮定はしません。これまで築いてきた基礎 —
[単調収束](./04-monotone-convergence.ja.md)・[完備性](./02-supremum-infimum.ja.md)・
[中間値の定理](./09-intermediate-value-theorem.ja.md) — は、数 $`e`$、関数 $`e^x`$、
そして $`\ln x`$ を厳密に *構成* し、それらの導関数を生む2つの極限を取り出すのに、
ちょうど十分です。

## 数 $`e`$

> **定義.** $`\displaystyle e = \lim_{n \to \infty}\left(1 + \frac1n\right)^{n}.`$

この極限は自明ではありません — 数列 $`a_n = (1 + 1/n)^n`$ が実際に収束することを示す
必要があります。[単調収束定理](./04-monotone-convergence.ja.md)により、$`(a_n)`$ が
**増加** かつ **上に有界** であることを示せば十分です。二項定理で展開します。
```math
a_n = \left(1 + \frac1n\right)^n
= \sum_{k=0}^{n} \frac{1}{k!}\prod_{j=0}^{k-1}\Big(1 - \frac{j}{n}\Big).
```
$`k`$ 個の各因子 $`1 - j/n`$ は $`(0, 1]`$ に属し、これが必要な2つの事実を導きます。

- **増加.** $`n`$ から $`n+1`$ へ移ると、各因子 $`\big(1 - \tfrac{j}{n}\big)`$ は
  $`\big(1 - \tfrac{j}{n+1}\big)`$ へ増え、さらに正の項が1つ加わります。ゆえに
  $`a_{n+1} > a_n`$。
- **有界.** 因子の積は $`\le 1`$ で、$`k! \ge 2^{k-1}`$ なので、
  ```math
  a_n \le \sum_{k=0}^{n}\frac{1}{k!} \le 1 + \sum_{k=1}^{n}\frac{1}{2^{k-1}} < 1 + 2 = 3.
  ```

$`a_1 = 2`$ で数列が増加するので、すべての $`n`$ で $`2 \le a_n < 3`$ であり、極限が
存在して $`2 < e \le 3`$ です。値は $`e = 2.71828\ldots`$ — 無理数であり、実は超越数です。

## 指数関数

$`1`$ を実パラメータ $`x`$ で置き換えると、すべての実数で指数関数が定義されます。

> **定義.** $`x \in \mathbb{R}`$ に対し、
> $`\displaystyle e^{x} = \exp(x) = \lim_{n \to \infty}\left(1 + \frac{x}{n}\right)^{n}.`$

同じ「増加かつ有界」の議論（$`n > |x|`$ で）により、この極限はすべての $`x`$ で存在し、
有理数 $`x`$ では $`e`$ の通常のべきと根に一致します。これが記法 $`e^x`$ を正当化します。
中心的な性質を記録します。

> **命題.** 関数 $`\exp`$ は次を満たす。
> 1. $`\exp(0) = 1`$ かつ すべての $`x`$ で $`\exp(x) > 0`$;
> 2. $`\exp(x + y) = \exp(x)\,\exp(y)`$（*関数等式*）;
> 3. $`\exp`$ は連続かつ狭義単調増加;
> 4. 値域は $`(0, \infty)`$ 全体。

*概略.* (2) は、$`\big(1+\tfrac{x}{n}\big)\big(1+\tfrac{y}{n}\big)`$ と
$`\big(1 + \tfrac{x+y}{n}\big)`$ の比が $`1 + c_n`$（$`c_n = \dfrac{xy/n^2}{1 + (x+y)/n}`$）
となり、$`n\,c_n \to 0`$ なので $`(1 + c_n)^n \to 1`$。$`n`$ 乗して極限をとれば、積
$`\exp(x)\exp(y)`$ が $`\exp(x+y)`$ になります。正値性は $`\exp(x) = \exp(x/2)^2 \ge 0`$
と $`\exp(x)\exp(-x) = \exp(0) = 1 \neq 0`$ から従います。単調性と連続性は下の不等式から、
$`(0,\infty)`$ への全射性は IVT から（$`x \to \infty`$ で $`\exp(x) \to \infty`$、
$`x \to -\infty`$ で $`\exp(x) \to 0`$ だから）従います。$`\blacksquare`$

## 基本不等式

$`\exp`$ に関する定量的なことは、すべて1つの不等式から流れ出ます。それ自体、**ベルヌーイ
の不等式** $`(1 + t)^n \ge 1 + nt`$（$`t \ge -1`$ で成立）の1行の帰結です。

> **補題.** すべての実数 $`x`$ に対し、$`\quad e^{x} \ge 1 + x,\quad`$ 等号は $`x = 0`$
> のときに限る。

*証明.* $`n > |x|`$ のとき $`x/n > -1`$ なので、ベルヌーイより
$`\big(1 + \tfrac{x}{n}\big)^n \ge 1 + n\cdot\tfrac{x}{n} = 1 + x`$。$`n \to \infty`$
とすれば $`e^x \ge 1 + x`$ を得ます。$`\blacksquare`$

$`-x`$ に適用すると、補題は $`e^{-x} \ge 1 - x`$、すなわち
```math
e^{x} \le \frac{1}{1 - x} \qquad (x < 1)
```
という、$`0`$ の近くで対になる上界も与えます。

## 導関数の背後にある極限

これら2つの評価が、$`0`$ における指数関数の振る舞いを正確に固定します — 次のレッスンで
$`e^x`$ が自分自身を導関数にもつ、その鍵です。

> **定理.** $`\displaystyle \lim_{x \to 0} \frac{e^{x} - 1}{x} = 1.`$

*証明.* $`0 < x < 1`$ では、補題の下界から $`e^x - 1 \ge x`$、ゆえに
$`\dfrac{e^x - 1}{x} \ge 1`$。上界から $`e^x - 1 \le \dfrac{x}{1 - x}`$、ゆえに
$`\dfrac{e^x - 1}{x} \le \dfrac{1}{1 - x}`$。よって
```math
1 \le \frac{e^x - 1}{x} \le \frac{1}{1 - x} \xrightarrow{\ x \to 0^+\ } 1,
```
となり、はさみうちの定理から右側極限は $`1`$ です。$`-1 < x < 0`$ では同じ2つの不等式が
役割を入れ替えて反対側からはさみます（あるいは $`x \mapsto -x`$ と置換）。両側極限とも
$`1`$ です。$`\blacksquare`$

## 自然対数

命題により、$`\exp : \mathbb{R} \to (0, \infty)`$ は連続な狭義単調増加の全単射です。
狭義単調増加の連続全単射は、連続で狭義単調増加な逆関数をもちます — その逆関数が
自然対数です。

> **定義.** $`\ln : (0, \infty) \to \mathbb{R}`$ を $`\exp`$ の逆関数とする。
> ```math
> \ln y = x \iff e^{x} = y.
> ```

関数等式を逆にすると、積が和に変わります。
```math
\ln 1 = 0, \quad \ln e = 1, \quad \ln(uv) = \ln u + \ln v, \quad \ln(u^{r}) = r\,\ln u,
```
そして $`\ln`$ は狭義単調増加で、$`y \to \infty`$ で $`\ln y \to \infty`$、$`y \to 0^+`$ で
$`\ln y \to -\infty`$ です。対になる極限は、前の定理から逆数として従います。

> **定理.** $`\displaystyle \lim_{t \to 0} \frac{\ln(1 + t)}{t} = 1.`$

*証明.* $`x = \ln(1 + t)`$ とおくと $`t = e^{x} - 1`$ であり、$`\ln`$ と $`\exp`$ の連続性に
より $`t \to 0 \iff x \to 0`$。よって
```math
\frac{\ln(1 + t)}{t} = \frac{x}{e^{x} - 1} = \left(\frac{e^x - 1}{x}\right)^{-1}
\xrightarrow{\ x \to 0\ } 1^{-1} = 1. \qquad \blacksquare
```

## 例題

**問題.** $`\displaystyle \lim_{x \to 0} \frac{e^{3x} - 1}{x}`$ を求めなさい。

$`u = 3x`$ とおくと $`x \to 0`$ で $`u \to 0`$ となり、
```math
\frac{e^{3x} - 1}{x} = 3\cdot\frac{e^{u} - 1}{u} \xrightarrow{\ x \to 0\ } 3 \cdot 1 = 3.
```
**答え.** $`3`$。（より一般に $`\lim_{x\to0}\dfrac{e^{ax}-1}{x} = a`$ — すでに
$`\dfrac{d}{dx}e^{ax} = a\,e^{ax}`$ の予兆です。）

## よくある間違い

- **$`e`$ を単に「$`\approx 2.718`$」と扱う.** その *定義* は極限 $`(1+1/n)^n`$ であり、
  小数はその帰結です。
- **$`e^{x+y} = e^x + e^y`$.** 違います — 指数関数は **和を積に** 変えます:
  $`e^{x+y} = e^x e^y`$。
- **$`\ln(a + b) = \ln a + \ln b`$.** これも誤り。対数の等式は $`\ln(ab) = \ln a +
  \ln b`$ です。
- **非正の数の $`\ln`$ をとる.** $`\ln`$ の定義域は $`(0,\infty)`$ です。
- **2つの極限を混同する.** $`\dfrac{e^x-1}{x}`$ と $`\dfrac{\ln(1+t)}{t}`$ がともに
  $`1`$ に近づくのは、$`t = e^x - 1`$ に沿って互いに逆数だからです。

## 練習問題

1. すべての $`n \ge 1`$ で $`2 \le (1 + 1/n)^n < 3`$ を示しなさい。
2. $`e^x \ge 1 + x`$（すべての実数 $`x`$）から、$`x < 1`$ で $`e^x \le \dfrac{1}{1-x}`$ を
   導きなさい。
3. 定数 $`a`$ に対し、$`\displaystyle\lim_{x \to 0}\frac{e^{ax} - 1}{x}`$ を求めなさい。
4. $`e^{s+t} = e^s e^t`$ を用いて、$`u, v > 0`$ に対し $`\ln(uv) = \ln u + \ln v`$ を
   証明しなさい。

<details>
<summary>解答</summary>

1. 増加で $`a_1 = 2`$ より下界。$`a_n \le \sum_{k=0}^n \tfrac1{k!} < 1 + \sum_{k\ge1}
   2^{-(k-1)} = 3`$ より上界。
2. 不等式を $`-x`$ に適用：$`e^{-x} \ge 1 - x`$。$`x < 1`$ では右辺が正なので、逆数を
   とると（不等号が反転して）$`e^{x} = 1/e^{-x} \le 1/(1-x)`$。
3. $`u = ax`$ とおく：$`\dfrac{e^{ax}-1}{x} = a\cdot\dfrac{e^u - 1}{u} \to a`$。
   （$`a = 0`$ では式は恒等的に $`0`$ で、極限 $`0`$ と整合。）
4. $`s = \ln u`$, $`t = \ln v`$ とおくと $`e^s = u`$, $`e^t = v`$。すると $`uv = e^s e^t
   = e^{s+t}`$ なので、定義により $`\ln(uv) = s + t = \ln u + \ln v`$。

</details>

## 関連項目

- [有界な単調数列は収束する](./04-monotone-convergence.ja.md)
- [上限・下限と実数の完備性](./02-supremum-infimum.ja.md)
- [中間値の定理](./09-intermediate-value-theorem.ja.md)
- [導関数：定義と微分可能性](./12-derivative-definition.ja.md)
