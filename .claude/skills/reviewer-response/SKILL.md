---
name: reviewer-response
description: Drafts structured "Response to Reviewers" documents for HEP journal submissions. Reads manuscript .tex files and reviewer comment files (.txt, .pdf) in papers/ subdirectory. Use when user says "draft reviewer response", "respond to referee", "write response letter", "address reviewer comments".
argument-hint: "[papers/paper-slug or 'help']"
allowed-tools: ["Read", "Write", "Edit", "Grep", "Glob", "Bash", "Task"]
---

# Reviewer Response Skill

Produce a publication-ready "Response to Reviewers" for a HEP journal submission.
Reads the manuscript source and reviewer comment files; generates a structured
point-by-point Markdown draft; optionally compiles a LaTeX response letter.

**Input:** `$ARGUMENTS` — path to a paper directory (e.g., `papers/bsm-dijets-atlas-2025`)
or the string `help`.

---

## Step 0 — Handle 'help' or missing argument

If `$ARGUMENTS` is empty or equals `help`:

1. Read `papers/README.md` and display the folder convention section.
2. Show a quick-start example:
   ```
   /reviewer-response papers/bsm-dijets-atlas-2025
   ```
3. Exit. Do not proceed to later steps.

---

## Step 1 — Validate paper directory

Set `PAPER_DIR = $ARGUMENTS` (strip trailing slash).

Check that the following exist:
- `$PAPER_DIR/manuscript/` — must contain at least one `.tex` file
- `$PAPER_DIR/reviewer_comments/` — must contain at least one `.txt`, `.pdf`, or `.md` file

If `$PAPER_DIR/README.md` exists, read it to extract:
- Paper title
- Journal (PRL / PRD / JHEP / PLB / EPJC)
- Manuscript number
- Current round (default: round1)

If validation fails, print a clear error explaining what is missing and what the user
should create. Do not proceed.

If `reviewer_comments/` has multiple round subdirectories, use the most recent
(highest-numbered: `round2` > `round1`). Inform the user which round is being used.

---

## Step 2 — Read and understand manuscript

Read all `.tex` files in `$PAPER_DIR/manuscript/`. For large files (>500 lines),
read in sections. Extract:

- **Title** and **abstract**
- **Section structure** (list of section headings)
- **Key physics result** (main measurement, exclusion, observation)
- **Collider and dataset** (LHC Run 2? 13 TeV? X fb⁻¹?)
- **Key kinematic variables** (which observables drive the analysis)
- **Potential weaknesses** (missing systematics discussion? thin theory comparison?)

If `$PAPER_DIR/manuscript/refs.bib` exists, read it for later citation verification in Step 5.

---

## Step 3 — Parse reviewer comments

Glob `$PAPER_DIR/reviewer_comments/**/*.{txt,pdf,md}`.

For each file found:
1. Identify the reviewer number from the filename or content.
2. Parse every distinct concern into a structured point.
3. Classify each point as one of:
   - **MAJOR** — requires new analysis, new figure, or significant revision
   - **CLARIFICATION** — requires added text, explanation, or reference
   - **MINOR** — typo fix, terminology, formatting
   - **POSITIVE** — compliment or no action required

For PDF files: attempt to read directly. If content is not extractable, print:
> "Could not extract text from `[filename]`. Please convert to .txt with
> `pdftotext [filename] [filename].txt` and re-run."
Then continue with remaining files.

**Present the internal parse table to the user before drafting:**

```
## Parsed Reviewer Comments

### Reviewer 1 (N points)
| # | Classification | Summary (≤10 words) |
|---|---------------|---------------------|
| R1.1 | MAJOR | ... |
| R1.2 | CLARIFICATION | ... |

### Reviewer 2 (M points)
| # | Classification | Summary |
|---|---------------|---------|
| R2.1 | MAJOR | ... |

Total: K points across N reviewers
```

Ask: **"Does this parse look correct before I draft the responses?"**
Wait for user confirmation or correction before proceeding to Step 4.

---

## Step 4 — Draft response document

Generate `$PAPER_DIR/responses/response_draft.md` using the structure from
`templates/reviewer-response-template.md` (Part A).

For each parsed point (in order):
1. Use the parsed summary as the subsection heading.
2. Insert the reviewer's verbatim text in a Markdown block quote.
3. Draft a substantive response:
   - For valid criticisms: acknowledge, describe how it is addressed, reference HEP-standard terminology from `.claude/rules/hep-paper-standards.md`
   - For requests for standard information (NLO K-factor, pile-up, jet algorithm): provide a template answer the user can fill with specifics
   - For disagreements: draft a polite, physics-grounded justification template
4. Insert a manuscript change placeholder:
   - Location: `[Section X, page Y, line Z — FILL IN]`
   - Change: `[Description — FILL IN]`
   - New text: `[Paste revised sentence here — FILL IN]`

Generate the complete change log table at the end.

Write the file. Confirm: "Draft saved to `$PAPER_DIR/responses/response_draft.md`."

---

## Step 5 — HEP domain review

Invoke the `hep-domain-reviewer` agent via Task on:
- `$PAPER_DIR/responses/response_draft.md`
- `$PAPER_DIR/manuscript/main.tex` (or primary .tex file)

The agent will save its report to `$PAPER_DIR/responses/hep_review_[date].md`.

After the agent completes, present a summary of its findings:
- Overall assessment (SOUND / MINOR / MAJOR / CRITICAL)
- Any CRITICAL or MAJOR issues requiring attention before submission
- Location of the full report

---

## Step 6 — Offer LaTeX compilation

Ask the user:
> "Would you like me to also generate `response_letter.tex` and attempt to compile it?
> This produces a PDF formatted for [journal] submission."

If **yes**:
1. Read `templates/reviewer-response-template.md` Part B.
2. Determine document class from journal:
   - **PRL or PRD** → use `revtex4-2` with `[aps,prl,reprint]` or `[aps,prd,reprint]`
   - **JHEP / PLB / EPJC** → use standard `letter` class (12pt, letterpaper)
3. Generate `$PAPER_DIR/responses/response_letter.tex` with:
   - Paper title, journal, manuscript number from Step 1
   - All reviewer points from Step 4 in LaTeX format
   - `\reviewerquote{}` macros for verbatim quotes
   - `\change{}{}{}` macros for manuscript change descriptions
4. Attempt compilation:
   ```bash
   cd $PAPER_DIR/responses && pdflatex response_letter.tex 2>&1 | tail -20
   ```
   If compilation succeeds: "Compiled successfully → `response_letter.pdf`"
   If it fails: show the relevant error lines; save `.tex` anyway with note:
   > "LaTeX compilation failed. The .tex file has been saved — compile locally to diagnose."

If **no**: skip and proceed to Step 7.

---

## Step 7 — Present summary

Print a structured summary:

```
## Reviewer Response Draft Complete

**Paper:** [Title]
**Journal:** [Journal] | **Manuscript #:** [Number]
**Round:** [N] | **Date:** [YYYY-MM-DD]

### Files Generated
- `$PAPER_DIR/responses/response_draft.md` — Markdown draft (primary output)
- `$PAPER_DIR/responses/hep_review_[date].md` — HEP domain review report
- `$PAPER_DIR/responses/response_letter.tex` — LaTeX letter [if generated]
- `$PAPER_DIR/responses/response_letter.pdf` — Compiled PDF [if successful]

### Reviewer Points Summary
- Total points addressed: K (Reviewer 1: N, Reviewer 2: M, ...)
- MAJOR: X | CLARIFICATION: Y | MINOR: Z | POSITIVE: W

### HEP Domain Review
- Overall: [SOUND / MINOR / MAJOR / CRITICAL]
- [Any CRITICAL/MAJOR issues flagged]

### Action Required From You
The following placeholders need your input before submission:
1. Page/line/equation numbers for each manuscript change (marked `[FILL IN]`)
2. Actual revised text for each new sentence (marked `[FILL IN]`)
3. [Any specific physics details flagged by the domain reviewer]
```

---

## Examples

### Example 1: First-round PRL response

```
/reviewer-response papers/higgs-ggf-cms-2025
```

Directory has:
- `manuscript/main.tex` (Higgs ggF measurement, 13 TeV, 138 fb⁻¹)
- `reviewer_comments/round1/reviewer1.txt` (4 points: NLO K-factor, jet veto, signal region definition, comparison with ATLAS)
- `reviewer_comments/round1/reviewer2.txt` (3 points: PDF uncertainty, figure clarity, one typo)

Skill parses 7 points across 2 reviewers, drafts `response_draft.md` with 7 structured responses, runs HEP domain review, offers LaTeX compilation with `revtex4-2 [aps,prl]` class.

### Example 2: Help mode

```
/reviewer-response help
```

Displays the folder convention from `papers/README.md`, shows how to set up a paper directory, and exits.

### Example 3: Missing reviewer_comments/ directory

```
/reviewer-response papers/bsm-dijets-atlas-2025
```

If `reviewer_comments/` is missing:

> "Error: `papers/bsm-dijets-atlas-2025/reviewer_comments/` not found.
>
> Create this directory and add the referee reports:
> ```bash
> mkdir -p papers/bsm-dijets-atlas-2025/reviewer_comments/round1
> cp /path/to/referee_report.txt papers/bsm-dijets-atlas-2025/reviewer_comments/round1/reviewer1.txt
> ```
> Then re-run `/reviewer-response papers/bsm-dijets-atlas-2025`."

---

## Troubleshooting

| Problem | Action |
|---------|--------|
| No `.tex` files in `manuscript/` | Search one level up in `$PAPER_DIR/`; if found, inform user of non-standard location and proceed |
| PDF comment files unreadable | Ask user to convert with `pdftotext`; continue with other files |
| Reviewer numbering ambiguous | Default to sequential numbering (Reviewer 1, Reviewer 2, ...); inform user |
| `pdflatex` not available | Save `.tex` with note: "Compile locally with `pdflatex response_letter.tex`" |
| Multiple `.tex` files in `manuscript/` | Look for `main.tex`; if absent, look for `\begin{document}` to identify primary file |
| Reviewer quoted text is very long (>500 words) | Truncate in draft with `[...excerpt...]` and note that full quote is in the comment file |
