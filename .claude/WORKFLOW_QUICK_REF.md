# Workflow Quick Reference

**Model:** Contractor (you direct, Claude orchestrates)

---

## The Loop

```
Your instruction
    ↓
[PLAN] (if multi-file or unclear) → Show plan → Your approval
    ↓
[EXECUTE] Implement, verify, done
    ↓
[REPORT] Summary + what's ready
    ↓
Repeat
```

---

## I Ask You When

- **Design forks:** "Option A (fast) vs. Option B (robust). Which?"
- **Code ambiguity:** "Spec unclear on X. Assume Y?"
- **Replication edge case:** "Just missed tolerance. Investigate?"
- **Scope question:** "Also refactor Y while here, or focus on X?"

---

## I Just Execute When

- Code fix is obvious (bug, pattern application)
- Verification (tolerance checks, tests, compilation)
- Documentation (logs, commits)
- Plotting (per established standards)
- Deployment (after you approve, I ship automatically)

---

## Quality Gates (No Exceptions)

| Score | Action |
|-------|--------|
| >= 90 | Ready to commit (high bar for publication) |
| < 90  | Fix blocking issues |

---

## Non-Negotiables (HEP Conventions)

<!-- HEP-specific conventions — see .claude/rules/hep-paper-standards.md -->

- **INSPIRE citation format:** `Author:YYYYidentifier` (e.g., `CMS:2023abc`, `Cacciari:2008gp`)
- **Uncertainty reporting:** `N ± stat ± syst` — always separate; luminosity separate
- **Manuscript is authoritative:** Read-only for responses; never modify during response drafting
- **All reviewer points addressed:** No skipping; count must match
- **Page/line/equation references:** Must be exact; verify against PDF
- **Jet algorithm:** Anti-kt; always state radius parameter (e.g., `anti-$k_t$, $R=0.4$`)
- **Units:** Roman text in math mode; use `hepunits` package (`\GeV`, `\TeV`, `\fb`)
- **Limits:** Always 95% CL, CLs method, obs + exp ± 1σ, ± 2σ

---

## Preferences

<!-- Fill in as you discover your working style -->

**Response tone:** Professional and collegial
**Citation verification:** Always check INSPIRE keys resolve
**Change log:** Complete table at end of response
**Reporting:** [Concise bullets? Detailed prose? Details on request?]
**Session logs:** Always (post-plan, incremental, end-of-session)
**Replication:** [How strict? Flag near-misses?]

---

## Exploration Mode

For experimental work, use the **Fast-Track** workflow:
- Work in `explorations/` folder
- 60/100 quality threshold (vs. 80/100 for production)
- No plan needed — just a research value check (2 min)
- See `.claude/rules/exploration-fast-track.md`

---

## Next Step

You provide task → I plan (if needed) → Your approval → Execute → Done.
