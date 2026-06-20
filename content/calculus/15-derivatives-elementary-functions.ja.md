---
title: "初等関数の微分"
subject: calculus
level: early-undergraduate
lang: ja
prerequisites: [13-differentiation-rules, 14-exponential-and-logarithm]
---

# 初等関数の微分

## なぜ重要か

[微分の法則](./13-differentiation-rules.ja.md)が手に入った今、必要なのは少数の
*基本部品* となる関数の導関数だけです。それ以外はすべてそこから組み立てられます。本
レッスンでは、指数関数・対数関数・三角関数の導関数を証明します。どの証明も — 差分商を
通じて — すでに確保した1つの極限に帰着します。$`\tfrac{e^h-1}{h} \to 1`$、
$`\tfrac{\ln(1+t)}{t} \to 1`$、または幾何的極限 $`\tfrac{\sin x}{x} \to 1`$ です。

## 指数関数は自分自身が導関数

> **定理.** $`\dfrac{d}{dx}\,e^{x} = e^{x}.`$

*証明.* 差分商から $`e^x`$ をくくり出し、関数等式 $`e^{x+h} = e^x e^h`$ を使います。
```math
\begin{aligned}
\frac{e^{x+h} - e^{x}}{h}
&= e^{x}\,\frac{e^{h} - 1}{h}
\xrightarrow{\ h \to 0\ } e^{x}\cdot 1 = e^{x},
\end{aligned}
```
ここで[指数関数の極限](./14-exponential-and-logarithm.ja.md)を用いました。$`\blacksquare`$

これこそ $`e`$ を特別にする性質です — あらゆる底の中で、$`e^x`$ はグラフの傾きがちょうど
その高さに等しい唯一の指数関数です。

## 対数関数

> **定理.** $`x > 0`$ に対し、$`\dfrac{d}{dx}\,\ln x = \dfrac1x.`$

*証明.* 差分商を書き、$`t = h/x`$ と置換します（$`h \to 0`$ で $`t \to 0`$）。
```math
\frac{\ln(x+h) - \ln x}{h} = \frac1h\,\ln\!\left(1 + \frac{h}{x}\right)
= \frac1x\cdot\frac{\ln(1 + t)}{t} \xrightarrow{\ h \to 0\ } \frac1x\cdot 1 = \frac1x,
```
ここで $`\ln(x+h) - \ln x = \ln\frac{x+h}{x} = \ln(1+t)`$ と
[対数関数の極限](./14-exponential-and-logarithm.ja.md)を使いました。$`\blacksquare`$

（$`x < 0`$ では $`\ln|x|`$ について同じ式が成り立ちます。$`x \neq 0`$ で
$`\dfrac{d}{dx}\ln|x| = \dfrac1x`$。）

## 三角関数の鍵となる極限

三角関数の導関数はすべて、1つの幾何的事実に依拠します。$`x`$ を **ラジアン** でとります
（これが、微積分でラジアンが自然な角度の単位である理由のすべてです）。単位円上で、
三角形・扇形・より大きい三角形の面積を比べると、$`0 < x < \tfrac\pi2`$ に対して
```math
\sin x \le x \le \tan x
```
が得られます。$`\sin x > 0`$ で割って逆数をとると $`\cos x \le \dfrac{\sin x}{x} \le 1`$。
$`x \to 0`$ で $`\cos x \to 1`$ なので、はさみうちの定理から極限が得られます（$`x`$ の
偶関数なので両側が一致します）。

> **補題.** $`\lim_{x \to 0}\frac{\sin x}{x} = 1`$、したがって
> $`\lim_{x \to 0}\frac{1 - \cos x}{x} = 0.`$

*2つ目の極限* は有理化で従います。
```math
\begin{aligned}
\frac{1 - \cos x}{x}
&= \frac{1 - \cos^2 x}{x\,(1 + \cos x)} \\
&= \frac{\sin x}{x}\cdot\frac{\sin x}{1 + \cos x}
\to 1 \cdot \frac{0}{2} = 0.
\end{aligned}
```

## 正弦と余弦

> **定理.** $`\dfrac{d}{dx}\,\sin x = \cos x`$ かつ $`\dfrac{d}{dx}\,\cos x = -\sin x.`$

*証明.* 加法定理 $`\sin(x+h) = \sin x \cos h + \cos x \sin h`$ を使います。
```math
\frac{\sin(x+h) - \sin x}{h}
= \sin x\,\frac{\cos h - 1}{h} + \cos x\,\frac{\sin h}{h}
\xrightarrow{\ h \to 0\ } \sin x\cdot 0 + \cos x\cdot 1 = \cos x,
```
上の2つの極限によります。余弦も $`\cos(x+h) = \cos x \cos h - \sin x \sin h`$ で同様です。
```math
\frac{\cos(x+h) - \cos x}{h} = \cos x\,\frac{\cos h - 1}{h} - \sin x\,\frac{\sin h}{h}
\to -\sin x. \qquad \blacksquare
```

## 正接

正弦と余弦がわかれば、商の法則が三角関数の残りを仕上げます。$`\cos x \neq 0`$ に対し、
```math
\frac{d}{dx}\,\tan x = \frac{d}{dx}\,\frac{\sin x}{\cos x}
= \frac{\cos x \cos x - \sin x(-\sin x)}{\cos^2 x}
= \frac{\cos^2 x + \sin^2 x}{\cos^2 x} = \frac{1}{\cos^2 x} = \sec^2 x.
```

## まとめ

| $`f(x)`$ | $`e^x`$ | $`\ln x`$ | $`\sin x`$ | $`\cos x`$ | $`\tan x`$ |
|---|---|---|---|---|---|
| $`f'(x)`$ | $`e^x`$ | $`1/x`$ | $`\cos x`$ | $`-\sin x`$ | $`\sec^2 x`$ |

（実数 $`r`$ に対する一般のべきの法則 $`\tfrac{d}{dx}x^r = r x^{r-1}`$ と
$`\tfrac{d}{dx}a^x = a^x \ln a`$ は連鎖律を要し、次のレッスンで証明します。）

## 例題

**問題.** $`f(x) = x^2 \ln x`$ と $`g(x) = e^x \sin x`$ を微分しなさい。

積の法則により、
```math
f'(x) = 2x\,\ln x + x^2\cdot\frac1x = 2x\ln x + x, \qquad
g'(x) = e^x \sin x + e^x \cos x = e^x(\sin x + \cos x).
```

## よくある間違い

- **$`\dfrac{d}{dx}e^x = x e^{x-1}`$.** 違います — これは *べき* の法則の誤用です。指数が
  変数なので $`\dfrac{d}{dx}e^x = e^x`$。
- **$`\sin x`$ を度数法で微分する.** きれいな法則 $`\sin' = \cos`$ は **ラジアン** でのみ
  成り立ちます。度数法では係数 $`\pi/180`$ が入ります。
- **$`\ln`$ の定義域を忘れる.** $`\tfrac{d}{dx}\ln x = 1/x`$ は $`x > 0`$ で（$`x \neq 0`$
  なら $`\ln|x|`$ を使う）。
- **$`\cos`$ の符号の取りこぼし.** $`\dfrac{d}{dx}\cos x = -\sin x`$ — マイナスを落とし
  がちです。

## 練習問題

1. $`\dfrac{\ln x}{x}`$ を微分しなさい。
2. $`\dfrac{1}{\cos x}`$（すなわち $`\sec x`$）を微分し、簡単にしなさい。
3. $`\dfrac{d}{dx}\big(e^x \cos x\big)`$ を求めなさい。
4. 極限 $`\tfrac{\sin x}{x}\to 1`$ から、$`\lim_{x\to0}\frac{\sin 5x}{\sin 2x}`$ を求めなさい。

<details>
<summary>解答</summary>

1. 商の法則：$`\dfrac{(1/x)\,x - \ln x\cdot 1}{x^2} = \dfrac{1 - \ln x}{x^2}`$。
2. $`\dfrac{d}{dx}(\cos x)^{-1} = -\dfrac{-\sin x}{\cos^2 x} = \dfrac{\sin x}{\cos^2 x}
   = \sec x \tan x`$。
3. $`e^x \cos x + e^x(-\sin x) = e^x(\cos x - \sin x)`$。
4. $`\dfrac{\sin 5x}{\sin 2x} = \dfrac{\sin 5x}{5x}\cdot\dfrac{2x}{\sin 2x}\cdot\dfrac{5x}{2x}
   \to 1\cdot 1\cdot \dfrac52 = \dfrac52`$。

</details>

## 関連項目

- [微分の法則](./13-differentiation-rules.ja.md)
- [指数関数と対数関数](./14-exponential-and-logarithm.ja.md)
