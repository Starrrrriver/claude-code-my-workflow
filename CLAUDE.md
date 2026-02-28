# CLAUDE.MD -- Academic Project Development with Claude Code

<!-- HOW TO USE: Replace [BRACKETED PLACEHOLDERS] with your project info.
     Customize Beamer environments and CSS classes for your theme.
     Keep this file under ~150 lines — Claude loads it every session.
     See the guide at docs/workflow-guide.html for full documentation. -->

**Project:** HEP Research Papers and Reviewer Responses
**Institution:** [YOUR INSTITUTION]
**Branch:** main

---

## Core Principles

- **Plan first** -- enter plan mode before non-trivial tasks; save plans to `quality_reports/plans/`
- **Verify after** -- compile/render and confirm output at the end of every task
- **Single source of truth** -- Manuscript `.tex` is authoritative; reviewer responses derive from it
- **Quality gates** -- nothing ships below 80/100
- **[LEARN] tags** -- when corrected, save `[LEARN:category] wrong → right` to MEMORY.md

---

## Folder Structure

```
[YOUR-PROJECT]/
├── CLAUDE.MD                    # This file
├── .claude/                     # Rules, skills, agents, hooks
├── Bibliography_base.bib        # Centralized bibliography
├── Figures/                     # Figures and images
├── Preambles/header.tex         # LaTeX headers
├── Slides/                      # Beamer .tex files
├── Quarto/                      # RevealJS .qmd files + theme
├── papers/                      # Per-paper: manuscript/, reviewer_comments/, responses/
├── docs/                        # GitHub Pages (auto-generated)
├── scripts/                     # Utility scripts + R code
├── quality_reports/             # Plans, session logs, merge reports
├── explorations/                # Research sandbox (see rules)
├── templates/                   # Session log, quality report templates
└── master_supporting_docs/      # Papers and existing slides
```

---

## Commands

```bash
# LaTeX (3-pass, XeLaTeX only)
cd Slides && TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
BIBINPUTS=..:$BIBINPUTS bibtex file
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex
TEXINPUTS=../Preambles:$TEXINPUTS xelatex -interaction=nonstopmode file.tex

# Deploy Quarto to GitHub Pages
./scripts/sync_to_docs.sh LectureN

# Quality score
python scripts/quality_score.py Quarto/file.qmd
```

---

## Quality Thresholds

| Score | Gate | Meaning |
|-------|------|---------|
| 80 | Commit | Good enough to save |
| 90 | PR | Ready for deployment |
| 95 | Excellence | Aspirational |

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/compile-latex [file]` | 3-pass XeLaTeX + bibtex |
| `/deploy [LectureN]` | Render Quarto + sync to docs/ |
| `/extract-tikz [LectureN]` | TikZ → PDF → SVG |
| `/proofread [file]` | Grammar/typo/overflow review |
| `/visual-audit [file]` | Slide layout audit |
| `/pedagogy-review [file]` | Narrative, notation, pacing review |
| `/review-r [file]` | R code quality review |
| `/qa-quarto [LectureN]` | Adversarial Quarto vs Beamer QA |
| `/slide-excellence [file]` | Combined multi-agent review |
| `/translate-to-quarto [file]` | Beamer → Quarto translation |
| `/validate-bib` | Cross-reference citations |
| `/devils-advocate` | Challenge slide design |
| `/create-lecture` | Full lecture creation |
| `/commit [msg]` | Stage, commit, PR, merge |
| `/lit-review [topic]` | Literature search + synthesis |
| `/research-ideation [topic]` | Research questions + strategies |
| `/interview-me [topic]` | Interactive research interview |
| `/review-paper [file]` | Manuscript review |
| `/reviewer-response [paper-dir]` | Draft point-by-point reviewer response |
| `/data-analysis [dataset]` | End-to-end R analysis |
| `/learn [skill-name]` | Extract discovery into persistent skill |
| `/context-status` | Show session health + context usage |
| `/deep-audit` | Repository-wide consistency audit |

---

## HEP Conventions Quick Reference

| Convention | Standard | Example |
|------------|----------|---------|
| Kinematics | `p_T`, `\eta` (pseudorapidity), `y` (rapidity) — never conflate | `$p_T > 30~\GeV$, $|\eta| < 2.5$` |
| Uncertainty | `N ± stat ± syst` — always separate; lumi separate | `$12.3 \pm 0.4 \pm 1.1 \pm 0.3~\text{pb}$` |
| Citation keys | INSPIRE format `Author:YYYYid` | `CMS:2023abc`, `Cacciari:2008gp` |
| Required refs | PDG, FastJet, anti-kt, generator papers | See `.claude/rules/hep-paper-standards.md` |
| Jet algorithm | Anti-kt; always state radius parameter | `anti-$k_t$, $R=0.4$` |
| Units | Roman text in math mode; use `hepunits` package | `\GeV`, `\TeV`, `\fb` |
| Limits | Always: 95% CL, CLs method, obs + exp ± 1σ, ± 2σ | — |

---

## Current Project State

| Paper | Directory | Journal | Status |
|-------|-----------|---------|--------|
| *(add papers here)* | `papers/[slug]/` | — | — |
