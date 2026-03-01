---
paths:
  - "papers/**"
  - "docs/**"
---

# Task Completion Verification Protocol

**At the end of EVERY task, Claude MUST verify the output works correctly.** This is non-negotiable.

## For HEP Papers & Responses (papers/**):
1. Compile response_letter.tex successfully: `cd papers/[slug]/responses && pdflatex response_letter.tex`
2. Verify all reviewer points addressed (count matches)
3. Check all manuscript change references are correct (page/line/equation numbers)
4. Run hep-domain-reviewer agent for substantive review
5. Verify bibliography citations resolve
6. Open PDF to verify formatting: `open response_letter.pdf` (macOS) or `xdg-open` (Linux)
7. Report verification results

## For TikZ Diagrams in Papers:
1. Compile TikZ to PDF: `pdflatex diagram.tex`
2. Convert to SVG if needed for web: `pdf2svg input.pdf output.svg`
3. **NEVER use PNG for diagrams** — PNG is raster and looks blurry
4. Verify SVG files contain valid XML/SVG markup
5. Copy to Figures/ directory

## For R Scripts:
1. Run `Rscript scripts/R/filename.R`
2. Verify output files (PDF, RDS) were created with non-zero size
3. Spot-check estimates for reasonable magnitude

## Common Pitfalls:
- **Missing reviewer points**: Always count and verify all points addressed
- **Wrong references**: Page/line/equation numbers must match manuscript exactly
- **Broken citations**: Verify all INSPIRE keys resolve
- **Assuming success**: Always verify output files exist AND contain correct content

## Verification Checklist:
```
[ ] Output file created successfully
[ ] No compilation/render errors
[ ] Images/figures display correctly
[ ] Paths resolve in deployment location (docs/)
[ ] Opened in browser/viewer to confirm visual appearance
[ ] Reported results to user
```
