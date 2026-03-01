---
paths:
  - "papers/**/*.tex"
  - "papers/**/*.md"
  - "scripts/**/*.R"
---

# Quality Gates & Scoring Rubrics

## Thresholds

- **90/100 = Commit** -- publication-ready (high bar for HEP papers)
- **95/100 = Excellence** -- aspirational

## HEP Papers & Responses (papers/**/*.tex, papers/**/*.md)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Physics error in response | -30 |
| Critical | Reviewer point not addressed | -20 |
| Critical | Compilation failure | -100 |
| Critical | Broken citation | -15 |
| Major | Wrong page/line reference | -10 |
| Major | Missing citation | -5 |
| Major | Notation inconsistency | -3 |
| Minor | Typo in response | -2 |
| Minor | Long lines (>100 chars) | -1 (EXCEPT documented math formulas) |

## R Scripts (.R)

| Severity | Issue | Deduction |
|----------|-------|-----------|
| Critical | Syntax errors | -100 |
| Critical | Domain-specific bugs | -30 |
| Critical | Hardcoded absolute paths | -20 |
| Major | Missing set.seed() | -10 |
| Major | Missing figure generation | -5 |

## Enforcement

- **Score < 90:** Block commit. List blocking issues.
- User can override with justification.

## Quality Reports

Generated **only at merge time**. Use `templates/quality-report.md` for format.
Save to `quality_reports/merges/YYYY-MM-DD_[branch-name].md`.

## Tolerance Thresholds (Research)

<!-- Customize for your domain -->

| Quantity | Tolerance | Rationale |
|----------|-----------|-----------|
| Point estimates | [e.g., 1e-6] | [Numerical precision] |
| Standard errors | [e.g., 1e-4] | [MC variability] |
| Coverage rates | [e.g., +/- 0.01] | [MC with B reps] |
