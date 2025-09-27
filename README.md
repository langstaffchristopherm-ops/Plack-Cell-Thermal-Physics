# Planck-Cell Program — Thermal Physics Chapter

This repository contains the LaTeX sources for **“Thermal Physics in the Planck-Cell Medium”**, 
which develops thermodynamics in the S/t (Planck-Cell) framework and integrates with the earlier 
kinematics, mass, and gravity layers.

## Build

Recommended toolchain:
- `pdflatex main.tex`
- `bibtex main`
- `pdflatex main.tex` (twice)

> Tip: If you see overfull/underfull boxes, the document includes boxed summary and display math
> variants designed to minimize those warnings. They can be toggled with the provided snippets.

## Structure (top-level; depth ≤ 3)

```
- .github/
  - .github/.gitkeep
  - .github/workflows/
    - .github/workflows/.gitkeep
- .zenodo.json
- README_TEMPLATE.md
- bibliography.bib
- build_scripts/
  - build_scripts/latex/
    - build_scripts/latex/Makefile
  - build_scripts/release/
    - build_scripts/release/Makefile
- data/
  - data/.gitkeep
- figs/
  - figs/.gitkeep
- latexmkrc
- main.tex
- other_tex/
  - other_tex/abstract.tex
  - other_tex/acknowledgments.tex
  - other_tex/authors_contributions.tex
  - other_tex/competing_interests.tex
  - other_tex/data_accessibility.tex
  - other_tex/dedication.tex
  - other_tex/disclosure.tex
  - other_tex/epigraph.tex
  - other_tex/format_macros.tex
  - other_tex/funding.tex
  - other_tex/math.tex
  - other_tex/theorems.tex
- runs/
  - runs/.gitkeep
- scripts/
  - scripts/.gitkeep
- src/
  - src/.gitkeep
```

Key files:
- `main.tex` — primary entry point.
- `bibliography.bib` — curated references (thermo/stat mech, blackbody, cosmology, constants, and the author’s related works).
- `other_tex/` — shared macros, math layers, theorem environments, and optional sections (acknowledgments, etc.).

## Citing

- Thermodynamics/stat mech foundations: Callen (1985), Boltzmann (1872), Clausius (1879), Shannon (1948).
- Blackbody/relativity: Planck (1901), Einstein (1905).
- Cosmological scalar tilt: Peebles (1993); Planck Collaboration (2018/2020) for modern constraints.
- Constants: CODATA (2018), Allen's Astrophysical Quantities, CRC Handbook.
- Author’s program: Temporal Relativity; Planck-Cell Kinematics; Planck-Cell Mass; Planck-Cell — Gravity.

## License

Unless otherwise noted, the text and code are provided by the author. Add your license of choice here
(e.g., CC-BY 4.0 for text; MIT for code snippets).

---
_This README was auto-added on 2025-09-27._
