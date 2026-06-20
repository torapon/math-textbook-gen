---
title: "合成関数の微分（連鎖律）"
subject: calculus
level: early-undergraduate
lang: ja
prerequisites: [12-derivative-definition, 13-differentiation-rules, 15-derivatives-elementary-functions]
---

# 合成関数の微分（連鎖律）

## なぜ重要か

出会う関数のほとんどは **合成** です — $`\sin(x^2)`$, $`e^{-x^2/2}`$,
$`\sqrt{1 + x^3}`$ のように、外側の関数を内側の関数に適用したものです。**連鎖律**
（chain rule）はこれらを微分する法則で、微積分全体で最もよく使われる法則です。その
メッセージは直感的です — $`y`$ が $`u`$ の $`f'`$ 倍の速さで変化し、$`u`$ が $`x`$ の $`g'`$
倍の速さで変化するなら、$`y`$ は $`x`$ の $`f'\cdot g'`$ 倍の速さで変化します。変化率は
鎖に沿って **掛け合わさる** のです。

## 主張

> **定理（連鎖律）.** $`g`$ が $`a`$ で微分可能、$`f`$ が $`b = g(a)`$ で微分可能ならば、
> 合成 $`f \circ g`$ は $`a`$ で微分可能で、
> ```math
> (f \circ g)'(a) = f'\big(g(a)\big)\,\cdot\,g'(a).
> ```

ライプニッツの記法で、$`y = f(u)`$, $`u = g(x)`$ とすると、覚えやすい形
```math
\frac{dy}{dx} = \frac{dy}{du}\cdot\frac{du}{dx}
```
になります。記号はあたかも $`du`$ が約分されるように *振る舞います* — もっとも、いつも
どおり各要素は分数ではなく極限です。

## 丁寧な証明

そそられる1行の証明は、$`g(a+h) - g(a)`$ を掛けて割ります。
```math
\frac{f(g(a+h)) - f(g(a))}{h}
= \frac{f(g(a+h)) - f(g(a))}{g(a+h) - g(a)}\cdot\frac{g(a+h) - g(a)}{h}.
```
これは *ほぼ* 正しいのですが、$`0`$ の近くの $`h`$ で $`g(a+h) = g(a)`$ となると違法です
（最初の分母が消える）。外側の差分商を、$`0`$ でも連続な関数に包むことで修復します。

*証明.* $`b = g(a)`$ とし、
```math
\varphi(k) =
\begin{cases}
\dfrac{f(b + k) - f(b)}{k}, & k \neq 0,\\[6pt]
f'(b), & k = 0
\end{cases}
```
と定義します。$`f`$ は $`b`$ で微分可能なので、$`k \to 0`$ で $`\varphi(k) \to f'(b) =
\varphi(0)`$、すなわち $`\varphi`$ は **$`0`$ で連続** です。さらに、*すべての* $`k`$
（両辺が $`0`$ となる $`k = 0`$ を含む）に対して、
```math
f(b + k) - f(b) = \varphi(k)\,k.
```
ここで $`k = g(a+h) - g(a)`$ とおくと $`b + k = g(a+h)`$。この恒等式を $`h`$ で割ると、
```math
\frac{f(g(a+h)) - f(g(a))}{h} = \varphi\big(g(a+h) - g(a)\big)\cdot\frac{g(a+h) - g(a)}{h}.
```
$`h \to 0`$ とします。$`g`$ は微分可能なので
[連続](./12-derivative-definition.ja.md)であり、$`g(a+h) - g(a) \to 0`$。すると
$`\varphi`$ が $`0`$ で連続なので $`\varphi(g(a+h)-g(a)) \to \varphi(0) = f'(b)`$。第2
因子は $`g'(a)`$ に近づきます。ゆえに積は $`f'(b)\,g'(a) = f'(g(a))\,g'(a)`$ に近づきます。
$`\blacksquare`$

このコツは、素朴な議論を正直にする仕掛けそのものです — $`\varphi`$ が、$`g`$ が一瞬
平らになる厄介な点を越えて値 $`f'(b)`$ を運んでくれるのです。

## 例

「外側を先に、それから内側の導関数を掛ける」と微分します。
```math
\frac{d}{dx}(x^2 + 1)^{10} = 10(x^2+1)^9\cdot 2x = 20x\,(x^2+1)^9,
```
```math
\frac{d}{dx}\,e^{x^2} = e^{x^2}\cdot 2x, \qquad
\frac{d}{dx}\,\sin(3x) = \cos(3x)\cdot 3, \qquad
\frac{d}{dx}\,\ln(\cos x) = \frac{1}{\cos x}\cdot(-\sin x) = -\tan x.
```
より長い鎖では法則が反復されます — 例えば3連結なら、
```math
\frac{d}{dx}\,e^{\sin(x^2)} = e^{\sin(x^2)}\cdot\cos(x^2)\cdot 2x.
```

## 応用：一般のべきの法則

連鎖律を $`x^r = e^{r\ln x}`$（$`x > 0`$ で有効）と組み合わせると、ついに **すべての
実数の指数** $`r`$ に対するべきの法則が証明されます — 正の整数だけではありません。
```math
\frac{d}{dx}\,x^{r} = \frac{d}{dx}\,e^{r\ln x} = e^{r\ln x}\cdot\frac{r}{x}
= x^{r}\cdot\frac{r}{x} = r\,x^{r-1}.
```
ゆえに $`\tfrac{d}{dx}\sqrt{x} = \tfrac12 x^{-1/2}`$ や $`\tfrac{d}{dx}\,x^{-1} =
-x^{-2}`$ も、$`x^2`$ の場合と同じ法則です。

## 応用：一般の底

同様に $`a^{x} = e^{x\ln a}`$（$`a > 0`$）から、
```math
\frac{d}{dx}\,a^{x} = e^{x\ln a}\cdot\ln a = a^{x}\,\ln a,
\qquad\text{および}\qquad
\frac{d}{dx}\,\log_a x = \frac{d}{dx}\,\frac{\ln x}{\ln a} = \frac{1}{x\,\ln a}.
```
係数 $`\ln a`$ は $`a = e`$ のときちょうど消えるもので — 底 $`e`$ が自然である理由の
もう1つの見方です。

## よくある間違い

- **内側の導関数を忘れる.** $`\dfrac{d}{dx}\sin(3x) = 3\cos(3x)`$ であって
  $`\cos(3x)`$ ではありません。因子 $`g'`$ こそが核心です。
- **外側と内側を同じ引数で微分する.** $`f'`$ は $`a`$ ではなく $`g(a)`$ で評価します。
  $`\dfrac{d}{dx}e^{x^2} = e^{x^2}\cdot 2x`$ であって、決して $`e^{2x}\cdot 2x`$ では
  ありません。
- **2連結で止める.** 各層が因子を寄与します。$`x`$ に届くまで続けます。
- **$`du`$ を文字どおり約分する.** $`\tfrac{dy}{du}\tfrac{du}{dx}`$ は極限についての
  定理であって、分数の代数ではありません — 約分のように見えても。

## 練習問題

1. $`\sqrt{1 + x^3}`$ を微分しなさい。
2. $`e^{-x^2/2}`$ を微分しなさい。
3. $`\ln(1 + e^x)`$ を微分しなさい。
4. 定数 $`n`$ に対し $`\big(\sin x\big)^{n}`$ を、また $`\cos(\cos x)`$ を微分しなさい。

<details>
<summary>解答</summary>

1. $`(1+x^3)^{1/2}`$：$`\tfrac12(1+x^3)^{-1/2}\cdot 3x^2 = \dfrac{3x^2}{2\sqrt{1+x^3}}`$。
2. $`e^{-x^2/2}\cdot(-x) = -x\,e^{-x^2/2}`$。
3. $`\dfrac{1}{1+e^x}\cdot e^x = \dfrac{e^x}{1+e^x}`$。
4. $`\dfrac{d}{dx}(\sin x)^n = n(\sin x)^{n-1}\cos x`$;
   $`\dfrac{d}{dx}\cos(\cos x) = -\sin(\cos x)\cdot(-\sin x) = \sin x\,\sin(\cos x)`$。

</details>

## 関連項目

- [微分の法則](./13-differentiation-rules.ja.md)
- [初等関数の微分](./15-derivatives-elementary-functions.ja.md)
- [指数関数と対数関数](./14-exponential-and-logarithm.ja.md)
