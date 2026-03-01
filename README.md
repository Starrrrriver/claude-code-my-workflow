# HEP Reviewer Response Workflow with Claude Code

> **Work in progress.** This is a fork of pedrohcgs/claude-code-my-workflow adapted for **HEP (High Energy Physics) research papers and reviewer response drafting**. The original workflow was designed for lecture slides; this version focuses on publication-ready "Response to Reviewers" documents for journals like PRL, JHEP, PRD, PLB, and EPJC.

**Last Updated:** 2026-03-01

A ready-to-fork foundation for AI-assisted HEP paper workflows. You describe what you need — draft a reviewer response, review a manuscript, validate citations — and Claude plans the approach, runs specialized agents, fixes issues, verifies quality, and presents results. Like a contractor who handles the entire job.

---

## Quick Start (5 minutes)

### 1. Fork & Clone

```bash
# Fork this repo on GitHub (click "Fork" on the repo page), then:
git clone https://github.com/YOUR_USERNAME/claude-code-my-workflow.git my-project
cd my-project
```

Replace `YOUR_USERNAME` with your GitHub username.

### 2. Start Claude Code and Paste This Prompt

```bash
claude
```

**Using VS Code?** Open the Claude Code panel instead. Everything works the same — see the [full guide](https://psantanna.com/claude-code-my-workflow/workflow-guide.html#sec-setup) for details.

Then paste the [starter prompt](https://psantanna.com/claude-code-my-workflow/workflow-guide.html#sec-first-session) from the guide, filling in your project details:

> I am starting to work on **[PAPER NAME]** in this repo. **[Describe your HEP paper in 2–3 sentences: experiment, analysis, journal target.]** I've set up the Claude Code HEP workflow... Please read the configuration files and adapt them for my project. Enter plan mode and start.

The [full guide](https://psantanna.com/claude-code-my-workflow/workflow-guide.html#sec-first-session) has the complete starter prompt with all the details.

**What this does:** Claude reads all the configuration files, fills in your project name, institution, and preferences, then enters contractor mode — planning, implementing, reviewing, and verifying autonomously. You approve the plan and Claude handles the rest.

---

## How It Works

### Contractor Mode

You describe a task. For complex or ambiguous requests, Claude first creates a requirements specification with MUST/SHOULD/MAY priorities and clarity status (CLEAR/ASSUMED/BLOCKED). You approve the spec, then Claude plans the approach, implements it, runs specialized review agents, fixes issues, re-verifies, and scores against quality gates — all autonomously. You see a summary when the work meets quality standards. Say "just do it" and it auto-commits too.

### Specialized Agents

Instead of one general-purpose reviewer, focused agents each check one dimension:

- **hep-domain-reviewer** — HEP-specific physics correctness, citation completeness, claim-evidence alignment
- **proofreader** — grammar/typos
- **r-reviewer** — R code quality (for data analysis)
- **tikz-reviewer** — TikZ diagram visual critique (for figures)

Each is better at its narrow task than a generalist would be. The same pattern extends to any academic artifact — manuscripts, data pipelines, proposals.

### Adversarial QA

The **hep-domain-reviewer** agent provides substantive review of physics correctness, assumption transparency, citation completeness, and claim-evidence alignment. It catches errors that single-pass review misses.

### Quality Gates

Every file gets a score (0–100). Scores below threshold block the action:
- **90** — commit threshold (high bar for publication-ready responses)
- **95** — excellence (aspirational)

### Context Survival

Plans, specifications, and session logs survive auto-compression and session boundaries. The PreCompact hook saves a context snapshot before Claude's auto-compression triggers, ensuring critical decisions are never lost. MEMORY.md accumulates learning across sessions, so patterns discovered in one session inform future work.

---

## The Guide

For a comprehensive walkthrough, read the **[full guide](https://psantanna.com/claude-code-my-workflow/workflow-guide.html)** (or see the [source](guide/workflow-guide.qmd)).

It covers:
1. **Why This Workflow Exists** — the problem and the vision
2. **Getting Started** — fork, paste one prompt, and Claude sets up the rest
3. **The System in Action** — specialized agents, adversarial QA, quality scoring
4. **The Building Blocks** — CLAUDE.md, rules, skills, agents, hooks, memory
5. **Workflow Patterns** — slides, research, reproducibility, presentation rhetoric, and more
6. **The Ecosystem** — extensions by clo-author, claudeblattman, MixtapeTools, and others
7. **Customizing for Your Domain** — creating your own reviewers and knowledge bases

---

## Use Cases

| Academic Task | How This Workflow Helps |
|---------------|----------------------|
| Reviewer responses | Point-by-point response drafting with HEP-specific review |
| Research papers | Manuscript review, citation validation, physics correctness |
| Data analysis | End-to-end R pipelines, replication verification, publication-ready output |
| Literature review | Structured search, synthesis, and gap identification |
| Research proposals | Structured drafting with adversarial critique |

---

## What's Included

<details>
<summary><strong>6 agents, 14 skills, 15 rules, 7 hooks</strong> (click to expand)</summary>

### Agents (`.claude/agents/`)

| Agent | What It Does |
|-------|-------------|
| `hep-domain-reviewer` | HEP-specialized domain reviewer for manuscripts and responses |
| `proofreader` | Grammar, typos, overflow, consistency review |
| `r-reviewer` | R code quality, reproducibility, and domain correctness |
| `tikz-reviewer` | Merciless TikZ diagram visual critique |
| `verifier` | End-to-end task completion verification |
| `domain-reviewer` | **Template** for your field-specific substance reviewer |

### Skills (`.claude/skills/`)

| Skill | What It Does |
|-------|-------------|
| `/reviewer-response` | Draft point-by-point reviewer response for HEP papers |
| `/review-paper` | Manuscript review: structure, physics, referee objections |
| `/validate-bib` | Cross-reference citations against bibliography |
| `/proofread` | Launch proofreader on a file |
| `/compile-latex` | 3-pass pdflatex compilation with bibtex |
| `/review-r` | Launch R code reviewer |
| `/commit` | Stage, commit, create PR, and merge to main |
| `/lit-review` | Literature search, synthesis, and gap identification |
| `/research-ideation` | Generate research questions and empirical strategies |
| `/interview-me` | Interactive interview to formalize a research idea |
| `/data-analysis` | End-to-end R analysis with publication-ready output |
| `/learn` | Extract non-obvious discoveries into persistent skills |
| `/context-status` | Show session health and context usage |
| `/deep-audit` | Repository-wide consistency audit |

### Research Workflow

| Feature | What It Does |
|---------|-------------|
| Exploration folder | Structured `explorations/` sandbox with graduate/archive lifecycle |
| Fast-track workflow | 60/100 quality threshold for rapid prototyping |
| Simplified orchestrator | implement → verify → score → done (no multi-round reviews) |
| Enhanced session logging | Structured tables for changes, decisions, verification |
| Merge-only reporting | Quality reports at merge time only |
| Math line-length exception | Long lines acceptable for documented formulas |
| Workflow quick reference | One-page cheat sheet at `.claude/WORKFLOW_QUICK_REF.md` |

### Rules (`.claude/rules/`)

Rules use path-scoped loading: **always-on** rules load every session (~100 lines total); **path-scoped** rules load only when Claude works on matching files. Claude follows ~150 instructions reliably, so less is more.

**Always-on** (no `paths:` frontmatter — load every session):

| Rule | What It Enforces |
|------|-----------------|
| `plan-first-workflow` | Plan mode for non-trivial tasks + context preservation |
| `orchestrator-protocol` | Contractor mode: implement → verify → review → fix → score |
| `session-logging` | Three logging triggers: post-plan, incremental, end-of-session |
| `meta-governance` | Template vs. working project distinctions |

**Path-scoped** (load only when working on matching files):

| Rule | Triggers On | What It Enforces |
|------|------------|-----------------|
| `verification-protocol` | `papers/**`, `docs/` | Task completion checklist for HEP papers |
| `single-source-of-truth` | `Figures/`, `papers/**` | Manuscript is authoritative; responses are read-only |
| `quality-gates` | `papers/**/*.tex`, `papers/**/*.md`, `*.R` | 90/95 scoring for publication-ready work |
| `hep-paper-standards` | `papers/**` | HEP conventions: INSPIRE citations, uncertainty reporting, jet algorithms |
| `r-code-conventions` | `*.R` | R coding standards + math line-length exception |
| `tikz-visual-quality` | `.tex` | TikZ diagram visual standards |
| `pdf-processing` | `master_supporting_docs/` | Safe large PDF handling |
| `proofreading-protocol` | `.tex`, `.md`, `quality_reports/` | Propose-first, then apply with approval |
| `replication-protocol` | `*.R` | Replicate original results before extending |
| `knowledge-base-template` | `.tex`, `*.R` | Notation/application registry template |
| `orchestrator-research` | `*.R`, `explorations/` | Simple orchestrator for research (no multi-round reviews) |
| `exploration-folder-protocol` | `explorations/` | Structured sandbox for experimental work |
| `exploration-fast-track` | `explorations/` | Lightweight exploration workflow (60/100 threshold) |

### Templates (`templates/`)

| Template | What It Does |
|----------|-------------|
| `session-log.md` | Structured session logging format |
| `quality-report.md` | Merge-time quality report format |
| `requirements-spec.md` | MUST/SHOULD/MAY requirements framework with clarity status |
| `constitutional-governance.md` | Template for defining non-negotiable principles vs. preferences |
| `skill-template.md` | Academic skill creation template with domain-specific examples |
| `reviewer-response-template.md` | HEP-aware reviewer response template |

</details>

---

## Prerequisites

| Tool | Required For | Install |
|------|-------------|---------|
| [Claude Code](https://code.claude.com/docs/en/overview) | Everything | `npm install -g @anthropic-ai/claude-code` |
| pdflatex | LaTeX compilation | [TeX Live](https://tug.org/texlive/) or [MacTeX](https://tug.org/mactex/) |
| R | Data analysis | [r-project.org](https://www.r-project.org/) |
| [gh CLI](https://cli.github.com/) | PR workflow | `brew install gh` (macOS) |

Not all tools are needed — install only what your project uses. Claude Code is the only hard requirement.

---

## Adapting for Your Field

1. **Fill in the knowledge base** (`.claude/rules/knowledge-base-template.md`) with your notation, applications, and design principles
2. **Customize the domain reviewer** (`.claude/agents/domain-reviewer.md`) with review lenses specific to your field (or use `hep-domain-reviewer.md` as a model)
3. **Add field-specific conventions** to `.claude/rules/hep-paper-standards.md` (or create your own standards file)
4. **Add field-specific R pitfalls** to `.claude/rules/r-code-conventions.md`
5. **Customize the workflow quick reference** (`.claude/WORKFLOW_QUICK_REF.md`) with your non-negotiables and preferences
6. **Set up the exploration folder** (`explorations/`) for experimental work

---

## Additional Resources

- [Claude Code Documentation](https://code.claude.com/docs/en/overview)
- [Writing a Good CLAUDE.md](https://code.claude.com/docs/en/memory) — official guidance on project memory

---

## Origin

This infrastructure is a fork of **[pedrohcgs/claude-code-my-workflow](https://github.com/pedrohcgs/claude-code-my-workflow)**, originally developed for lecture slides and extended for HEP research papers and reviewer response drafting. The original workflow was extracted from Econ 730: Causal Panel Data at Emory University. This fork adapts the multi-agent workflow for HEP paper workflows, focusing on publication-ready "Response to Reviewers" documents for journals like PRL, JHEP, PRD, PLB, and EPJC.

---

## Community & Extensions

This repo is the foundation. Others have extended it for specific workflows:

- **[clo-author](https://github.com/hsantanna88/clo-author)** by Hugo Sant'Anna (UAB) — Paper-centric research workflows with 15 adversarial worker-critic agent pairs, simulated blind peer review, AEA replication compliance, and full research lifecycle management
- **[claudeblattman](https://github.com/chrisblattman/claudeblattman)** by Chris Blattman (U Chicago) — Comprehensive guide for non-technical academics: executive assistant workflows, proposal writing, agent debates, and self-improving configuration
- **[MixtapeTools](https://github.com/scunning1975/MixtapeTools)** by Scott Cunningham (Baylor) — The Rhetoric of Decks: philosophy and practice of beautiful, rhetorically effective academic presentations

See the [guide's ecosystem section](https://psantanna.com/claude-code-my-workflow/workflow-guide.html#sec-ecosystem) for detailed descriptions, design principles, and more resources.

---

## License

MIT License. See [LICENSE](LICENSE).
