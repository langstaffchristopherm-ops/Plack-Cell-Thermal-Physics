# Minimal Publishing Template

Use `main_template.tex` as your starting point. It wires front matter in this order:

1. Title page
2. (Optional) Epigraph — `other_tex/epigraph.tex`
3. (Optional) **Dedication** (before Abstract) — `other_tex/dedication.tex`
4. **Abstract** (its own page) — `other_tex/abstract.tex`
5. Acknowledgements
6. Statements: Competing interests, Author contributions, Funding, Data availability, Disclosure
7. Table of contents (and optional lists of figures/tables)
8. Main body
9. (Optional) Glossary (only printed if the `glossaries` package is actually loaded)
10. Bibliography (BibTeX by default, using `bibliography.bib`)

## Compile

With TeX Live:
```bash
pdflatex main_template.tex
bibtex main_template
pdflatex main_template.tex
pdflatex main_template.tex
```

If you prefer `biblatex/biber`, switch the bibliography block at the bottom of `main_template.tex` and ensure `biber` is installed.

## Customization

- Author and title macros come from `other_tex/format_macros.tex` and `release.tex` (if present).
- Keep all custom packages inside `other_tex/format_macros.tex`.
