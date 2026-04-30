# AGENTS.md

## What this is

SZTU (深圳技术大学) undergraduate thesis LaTeX template. Single-document project, not a monorepo.

## Rule

- 有任何不确定问题都先和我确认，严格禁止自己臆想
- 编写论文时，尝试使用倒叙、插叙或跳跃式逻辑，增加背景信息的非线性分布，穿插极短句与复杂长句，或其它办法来降低 AI 检测率

## Key files

| File | Role |
|---|---|
| `sztuthesis_main.tex` | **Entry point** — compile this, not content/*.tex |
| `SZTUthesis.cls` | Document class (612 lines). Modifies article class for SZTU formatting. |
| `content/info.tex` | Thesis metadata: title, author, supervisor, department, dates |
| `content/content.tex` | Main body text (chapters) |
| `content/abstractcn.tex` / `abstracten.tex` | Chinese / English abstracts |
| `content/additional.tex` | Acknowledgments, achievements |
| `content/appendix_example.tex` | Appendix example |
| `thesis-references.bib` | Bibliography database |
| `gbt7714-numerical.bst` / `gbt7714.sty` | GB/T 7714 citation style (from CTeX-org/gbt7714-bibtex-style) |
| `STXingkai.ttf` / `STXinwei.ttf` / `STZhongsong.ttf` | Bundled Chinese fonts required by cls |

## Content editing

- All editable content lives in `content/`. Do not modify `sztuthesis_main.tex` unless adding new `\input`/`\include` entries.
- `info.tex` line 1 has `%!TEX root = ../sztuthesis_main.tex` — this tells editors which file is the root.
- Figures go in `images/`; reference them by filename only (e.g., `\includegraphics{sztu.png}`) since the path is configured in cls.
- BibTeX keys go in `thesis-references.bib`; cite with `\cite{key}`.
- The `\lipsum` command in main tex is placeholder text — replace content files, not this macro.

## VS Code / LaTeX Workshop

Configured in `.vscode/settings.json`:
- Root file fixed to `sztuthesis_main.tex`
- Default recipe: `latexmk (xelatex)`
- Formatter: `tex-fmt` (expected at `/root/.cargo/bin/tex-fmt`)
- Auto-build on save is enabled (`"onSave"`)
- BibTeX format: tab-indented

## Gotchas

- Figure/table numbering is per-section (e.g., "图 2-1", "表 3-2") — set via `\numberwithin` in main tex.
- `\blindreviewtrue` in `content/info.tex` toggles blind review mode (hides author/supervisor on cover).
- The `config_example/settings.json` is a legacy VS Code config example — the actual config is `.vscode/settings.json`.
- `texclear.sh` uses `git clean -X` so it only deletes files matching `.gitignore` patterns. Won't delete tracked files or the PDF.
