# ============ build_scripts/latex/Makefile — PDF only ============
# Usage:
#   make pdf
#   make clean
#   make distclean

TEX  := ../../main.tex   # main.tex at repo root
PDF  := ../../main.pdf
RUNS := ../../runs

.PHONY: pdf clean distclean

pdf:
	latexmk -pdf -interaction=nonstopmode -halt-on-error $(TEX)

clean:
	latexmk -c -outdir=$(RUNS) $(TEX) || latexmk -c $(TEX)
	@rm -f $(RUNS)/*.auxlock 2>/dev/null || true

distclean: clean
	latexmk -C -outdir=$(RUNS) $(TEX) || latexmk -C $(TEX)
	@rm -rf $(RUNS) 2>/dev/null || true
	@rm -f $(PDF) 2>/dev/null || true
