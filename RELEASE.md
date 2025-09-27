# Release Notes

## v0.1.0 — Initial thermal physics chapter (2025-09-27)

**Highlights**
- Integrates “Thermal Physics in the Planck-Cell Medium” into the LaTeX project.
- Adds improved Planck-units checkpoint (aligned equations, units).
- Reworks “Summary box” into a wrapped, breakable layout to avoid overfull boxes.
- Normalizes notation and prevents double-subscript issues (e.g., `\dot{S}_{\mathrm{phys,rad}}`).
- Aligns citations with curated `bibliography.bib` (Callen, Boltzmann, Clausius, Shannon, Planck, Einstein, Zeh, Peebles, Planck 2018, CODATA, Allen, CRC).
- Adds “Other Works by the Author” section with Zenodo DOIs (Temporal Relativity; Planck-Cell Kinematics; Planck-Cell Mass; Planck-Cell — Gravity).

**Build**
```
pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex
```

**Known issues**
- Depending on your LaTeX class/margins, boxed summaries may still need slight width tweaks
  (see `\fboxsep`, `\fboxrule`, and minipage width). The provided defaults are conservative.
- If both `README.md` and/or `RELEASE.md` existed already, this process saved additional files as
  `README_ADDED.md` / `RELEASE_ADDED.md` to avoid overwriting.

**Next steps**
- Optional: consolidate macro definitions for information-theoretic quantities in `other_tex/format_macros.tex` (e.g., `\newcommand{\Sbits}{S_{\mathrm{bits}}}`).
- Extend dynamics sections to connect thermal layer to field dynamics in subsequent articles.

https://doi.org/10.5281/zenodo.17211721