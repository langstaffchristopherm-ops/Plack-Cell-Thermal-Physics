# ============ build_scripts/release/Makefile — Unified Release ============
# Usage (requires BOTH TAG and DOI):
#   make release TAG=v0.1.0 DOI=10.5281/zenodo.1234567 PUB_TYPE=preprint
#
# Assumes:
#   - format_macros.tex defines \PaperTitleMain (placeholder supported)
#   - format_macros.tex contains: \IfFileExists{release.tex}{\input{release.tex}}{}
#   - .zenodo.json present at repo root (will be updated)
#   - build_scripts/latex/Makefile exists (pdf build)
#   - gh CLI authenticated (optional; comment out gh-release if not used)

SHELL := /bin/bash

TAG      ?=
DOI      ?=
PUB_TYPE ?=

.PHONY: release guard-req guard-clean sync-meta build-pdf commit-tag push gh-release

release: guard-req guard-clean sync-meta build-pdf commit-tag push gh-release
	@echo
	@echo "Release $(TAG) complete. GitHub Release created and main.pdf attached."

guard-req:
	@[ -n "$(TAG)" ] || (echo "ERROR: Pass TAG=vX.Y.Z" >&2; exit 2)
	@[ -n "$(DOI)" ] || (echo "ERROR: Pass DOI=10.5281/zenodo.NNNNNNN" >&2; exit 2)

guard-clean:
	@git diff --quiet || (echo "ERROR: Uncommitted changes present. Commit/stash first." >&2; exit 3)

sync-meta:
	@python3 - <<'PY'
import re, json, pathlib, sys, os, subprocess
TAG = os.environ["TAG"].strip()
DOI = os.environ["DOI"].strip()
PUB_TYPE = os.environ.get("PUB_TYPE","").strip()

fmt_p = pathlib.Path("format_macros.tex")
zen_p = pathlib.Path(".zenodo.json")
if not fmt_p.exists():
    print("ERROR: format_macros.tex not found", file=sys.stderr); sys.exit(4)
if not zen_p.exists():
    print("ERROR: .zenodo.json not found", file=sys.stderr); sys.exit(5)

fmt = fmt_p.read_text(encoding="utf-8")

# Extract PaperTitleMain (fallback to placeholder if not set)
m = re.search(r"\\(?:providecommand|newcommand)\\PaperTitleMain\{(.+?)\}", fmt, re.S)
if not m:
    print("ERROR: \\PaperTitleMain{...} not found in format_macros.tex", file=sys.stderr); sys.exit(6)
title = re.sub(r"\s+", " ", m.group(1)).strip()

# Update .zenodo.json
data = json.loads(zen_p.read_text(encoding="utf-8"))
data.setdefault("upload_type", "publication")
if PUB_TYPE:
    data["publication_type"] = PUB_TYPE
else:
    data.setdefault("publication_type", "preprint")
data["title"] = title
zen_p.write_text(json.dumps(data, ensure_ascii=False, indent=2)+"\n", encoding="utf-8")
print(f".zenodo.json: title='{title}'; publication_type='{data['publication_type']}'")

# Write/overwrite release.tex at repo root
commit = "(unknown)"
try:
    commit = subprocess.check_output(["git","rev-parse","--short","HEAD"], text=True).strip()
except Exception:
    pass

rel = "\\n".join([
    f"\\newcommand\\PaperVersion{{{TAG}}}",
    f"\\newcommand\\RepoDOI{{{DOI}}}",
    f"\\newcommand\\RepoCommit{{{commit}}}",
    ""
])
pathlib.Path("release.tex").write_text(rel, encoding="utf-8")
print("release.tex written with PaperVersion, RepoDOI, RepoCommit")
PY

build-pdf:
	$(MAKE) -C ../latex pdf

commit-tag:
	git add -A
	git commit -m "Release $(TAG): sync meta + PDF + release.tex" || true
	git tag -a $(TAG) -m "$(TAG)"

push:
	git push origin HEAD --follow-tags

gh-release:
	@command -v gh >/dev/null 2>&1 || { echo "NOTE: gh CLI not found; skipping GitHub release automation." >&2; exit 0; }
	@gh release create "$(TAG)" --notes "Release $(TAG)" || true
	@gh release upload "$(TAG)" "main.pdf" --clobber
