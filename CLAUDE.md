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
- **Quality gates** -- nothing ships below 90/100 (high bar for publication)
- **[LEARN] tags** -- when corrected, save `[LEARN:category] wrong → right` to MEMORY.md

---

## Folder Structure

```
[YOUR-PROJECT]/
├── CLAUDE.MD                    # This file
├── .claude/                     # Rules, skills, agents, hooks
├── Bibliography_base.bib        # Centralized bibliography (optional)
├── Figures/                     # Figures and images
├── papers/                      # Per-paper: manuscript/, reviewer_comments/, responses/
├── docs/                        # GitHub Pages (preprints, documentation)
├── scripts/                     # Utility scripts + R code
├── quality_reports/             # Plans, session logs, merge reports
├── explorations/                # Research sandbox (see rules)
├── templates/                   # Session log, quality report templates
└── master_supporting_docs/      # Reference papers and materials
```

---

## Commands

```bash
# Compile manuscript (pdflatex, 3-pass + bibtex)
cd papers/[slug]/manuscript && pdflatex main.tex
bibtex main
pdflatex main.tex
pdflatex main.tex

# Compile response letter
cd papers/[slug]/responses && pdflatex response_letter.tex

# Draft reviewer response
/reviewer-response papers/[slug]

# Validate bibliography
/validate-bib

# Quality score
python scripts/quality_score.py papers/[slug]/responses/response_draft.md
```

---

## Quality Thresholds

| Score | Gate | Meaning |
|-------|------|---------|
| 90 | Commit | Publication-ready (high bar) |
| 95 | Excellence | Aspirational |

---

## Skills Quick Reference

| Command | What It Does |
|---------|-------------|
| `/reviewer-response [paper-dir]` | Draft point-by-point reviewer response |
| `/review-paper [file]` | Manuscript review |
| `/validate-bib` | Cross-reference citations |
| `/proofread [file]` | Grammar/typo/overflow review |
| `/lit-review [topic]` | Literature search + synthesis |
| `/research-ideation [topic]` | Research questions + strategies |
| `/interview-me [topic]` | Interactive research interview |
| `/data-analysis [dataset]` | End-to-end R analysis |
| `/review-r [file]` | R code quality review |
| `/compile-latex [file]` | 3-pass pdflatex + bibtex |
| `/commit [msg]` | Stage, commit, PR, merge |
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
