# Math Textbook Generator / 数学教材ジェネレーター

Bilingual (English / 日本語) math documentation at the **high-school to early-undergraduate** level.

数学教材を **高校〜大学初年度** レベルで、**英語と日本語の両方** で作成するプロジェクトです。

## Format / 形式

Content is written in **Markdown with LaTeX math**:

- Inline math: `` $`...`$ `` → $`a^2 + b^2 = c^2`$
- Display math: a fenced ` ```math ` block

Both forms are chosen for reliable **GitHub** rendering:

- GitHub runs its Markdown parser over the *contents* of bare `$...$` / `$$...$$`,
  which corrupts the LaTeX — subscripts (`_`) and stars (`*`) collide with emphasis
  inline, and `\{`, `\,`, etc. get escaped in display blocks. Shielding inline math
  with backticks (`` $`...`$ ``) and writing display math as a ` ```math ` fence keeps
  the LaTeX verbatim so GitHub renders it correctly.

### Export to PDF / HTML via [Pandoc](https://pandoc.org/)

Pandoc wants plain `$...$` / `$$...$$`, so normalize the GitHub-specific forms first
(strip inline backticks; turn ` ```math ` fences into `$$`):

```sh
# GitHub forms  ->  plain $...$ / $$...$$
normalize() {
  sed -E 's/\$`/$/g; s/`\$/$/g; s/^```math$/$$/; s/^```$/$$/' "$1"
}

# Single lesson → PDF
normalize content/calculus/01-dedekind-cuts.en.md | pandoc -o dedekind-cuts.pdf

# → standalone HTML with MathJax
normalize content/calculus/01-dedekind-cuts.en.md | pandoc -s --mathjax -o dedekind-cuts.html
```

(The second `s/^```$/$$/` closes the fence; it assumes lessons use ` ``` ` fences
only for math, which is the convention here.)

## Structure / 構成

```
content/
  algebra/                  代数
  geometry/                 幾何
  trigonometry/             三角法
  functions/                関数 (precalculus)
  calculus/                 微積分
  linear-algebra/           線形代数
  probability-statistics/   確率・統計
  discrete-math/            離散数学
templates/                  Lesson templates / 雛形
assets/                     Images, diagrams / 画像・図
```

Each topic exists as a paired set of files so the two languages stay in sync:

```
content/algebra/quadratic-equations.en.md
content/algebra/quadratic-equations.ja.md
```

## Conventions / 規約

Writing and formatting conventions for generated lessons live in [`CLAUDE.md`](./CLAUDE.md).
生成される教材の執筆・書式規約は [`CLAUDE.md`](./CLAUDE.md) を参照してください。

## How to request content / 依頼の仕方

Just describe the topic and level in **English or Japanese**, e.g.:

- "Write a lesson on the quadratic formula."
- 「微分の定義について、高校生向けの教材を作って。」

By default both `.en.md` and `.ja.md` versions are produced unless you ask for one language.
特に指定がなければ、英語版と日本語版の両方を作成します。
