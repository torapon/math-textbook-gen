# Conventions for generating math lessons

This project produces bilingual (English / 日本語) math documentation at the
high-school to early-undergraduate level. Follow these conventions when
creating or editing content.

## Audience & tone

- Level: high school through early university. Assume motivated learners, not experts.
- Explain *why*, not just *how*. Build intuition before formalism.
- Define notation the first time it appears. Don't assume prior topics unless linked.
- Keep prose concise; prefer worked examples over long paragraphs.

## File layout

- Content lives under `content/<subject>/<topic>.<lang>.md` where `<lang>` is `en` or `ja`.
- Subjects: `algebra`, `geometry`, `trigonometry`, `functions`, `calculus`,
  `linear-algebra`, `probability-statistics`, `discrete-math`.
- Pair every lesson: create both `.en.md` and `.ja.md` unless the user asks for one language.
- The two language versions must cover the **same content, structure, and equations** —
  translate the prose, keep the math identical.
- Use a kebab-case topic slug shared across languages (e.g. `quadratic-equations`).

## Math formatting

- Inline math: wrap in backtick-shielded dollars — `` $`...`$ `` (e.g. `` $`a_n \to L`$ ``).
  GitHub's inline `$...$` runs Markdown's emphasis parser over the contents first, so
  a `_` (subscript) or `*` collides with `_emphasis_`/`*emphasis*` and the math fails
  to render. The backticks protect the contents while GitHub still renders them as math.
- Display math: use a fenced ` ```math ` block, **not** `$$ ... $$`. GitHub
  Markdown-escapes the contents of a `$$` block (turning `\{`→`{`, `\,`→`,`, etc.)
  before the math is rendered, which silently breaks set braces, spacing, and the
  like. A ` ```math ` fence is left verbatim and renders reliably. For example:
  ~~~
  ```math
  \begin{aligned}
  x &= \frac{-b \pm \sqrt{b^2 - 4ac}}{2a} \\
    &= \dots
  \end{aligned}
  ```
  ~~~
- Use standard LaTeX. Prefer `\frac`, `\sqrt`, `\cdot`, `\times`, `\le`, `\ge`, `\neq`.
- Align multi-step derivations with `aligned` inside the ` ```math ` fence (see above).
- Do **not** use `\(`, `\)`, `\[`, `\]`. Inline is `` $`...`$ ``; display is ` ```math `.
- Do **not** fake a display equation with inline `` $`\displaystyle ...`$ ``. GitHub
  wraps an oversized inline element in a horizontally-scrolling box. For a standalone
  centered equation use a ` ```math ` fence (blockquoted as `> ```math` when it is the
  body of a definition/theorem box); keep inline math in normal style (no
  `\displaystyle`), which renders compactly (`\lim`, `\sum` with side-set limits).
  (For Pandoc export, normalize both back to `$...$`/`$$...$$` first; see the README.)
- Do **not** backslash-escape punctuation inside math (`\*`, `\%`, etc.). Markdown
  escaping does not apply in math mode; `\*` is an undefined KaTeX control sequence
  and breaks rendering on GitHub. For a literal star use `^{*}` / `{*}`.
- Do **not** use `\operatorname{...}`. GitHub's math allowlist rejects it ("The
  following macros are not allowed: operatorname"). For an upright multi-letter
  operator name (`int`, `ext`, `sign`, etc.) use `\mathrm{...}` instead.
- Keep display equations from overflowing their box (GitHub adds a horizontal
  scrollbar when a line is too wide). Break long equality chains across lines with
  an `aligned` block (`&=` at each break), prefer compact forms (`\prod`,
  `\sum`) over spelled-out products, and move long `\text{...}` annotations or
  domain conditions into the surrounding prose rather than onto the math line.
- Number equations only when later referenced; otherwise leave them unnumbered.

## Lesson structure

Follow `templates/lesson-template.en.md` / `templates/lesson-template.ja.md`. In order:

1. **Frontmatter** — YAML with `title`, `subject`, `level`, `lang`, `prerequisites`.
2. **Intuition / motivation** — why this matters, a concrete hook.
3. **Definitions / theory** — formal statements, clearly set off.
4. **Worked examples** — at least one or two, fully stepped out.
5. **Common mistakes / pitfalls** — what learners get wrong.
6. **Practice problems** — with answers in a collapsed `<details>` block.
7. **See also** — links to related lessons.

## Language-specific notes

- Japanese: use です・ます調 (polite form) for explanatory prose. Use 全角 punctuation
  （。、）in prose, but keep math, code, and LaTeX in 半角 (ASCII).
- Keep technical terms with their English equivalent on first use, e.g.
  「判別式 (discriminant)」.
- English: US spelling, Oxford comma.

## Assets

- Diagrams/images go in `assets/` and are referenced with relative paths.
- Prefer generating diagrams as TikZ/LaTeX or describing them so they can be reproduced;
  avoid committing large binaries when a text-based figure works.
