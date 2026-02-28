---
paths:
  - "papers/**"
---

# HEP Paper Standards

Rules automatically loaded when working in `papers/`. Covers physics notation,
uncertainty reporting, citation style, journal formats, reviewer response etiquette,
and LaTeX conventions for High-Energy Physics manuscripts.

---

## 1. Physics Notation

### Kinematics and Vectors
- **Four-vectors:** `p^\mu`, `k^\mu` — always with Greek superscript; metric signature $(+,-,-,-)$
- **Transverse momentum:** `p_T` or `\pT` (macro preferred); NOT `p_t` (lowercase t = top quark)
- **Pseudorapidity vs rapidity:** `\eta` is pseudorapidity (massless limit); `y` is rapidity — do NOT conflate
- **Missing transverse energy:** `E_T^{miss}` or `\MET`; NOT `MET` in math mode
- **Scalar sum of jet pT:** `H_T` or `\HT`
- **Invariant mass:** `m_{jj}`, `m_{\ell\ell}`, `m_{T}` (transverse mass) — always subscript

### Coupling Constants and Parameters
- **Strong coupling:** `\alpha_s` (NOT `\alpha_S`); specify order: `\alpha_s(M_Z)`
- **Electromagnetic coupling:** `\alpha_{\rm em}` or `\alpha`
- **Gauge couplings:** `g_s`, `g`, `g'` — specify gauge group
- **Weak mixing:** `\sin^2\theta_W` or `\sin^2\hat{\theta}_W` (MSbar)

### Particle Naming (PDG conventions)
- **Bosons:** $W^\pm$, $Z$, $H$, $\gamma$ — NOT `W+`, `Z0`, `h`
- **Quarks:** $t$, $b$, $c$, $s$, $u$, $d$ — lowercase italic
- **Leptons:** $e$, $\mu$, $\tau$, $\nu_e$, $\nu_\mu$, $\nu_\tau$
- **BSM particles:** follow PDG naming; define at first use
- **Antiparticles:** $\bar{t}$, $\bar{p}$ — NOT `tbar`

### Cross-sections and Rates
- **Units:** pb, fb, ab — always spell out at first mention (picobarns, femtobarns)
- **Integrated luminosity:** $\mathcal{L} = X~\text{fb}^{-1}$
- **Branching ratios:** $\mathcal{B}(H \to \gamma\gamma)$ — calligraphic B
- **Signal strength:** $\mu = \sigma_{\rm obs}/\sigma_{\rm SM}$

---

## 2. Uncertainty Reporting

### Mandatory Format
```
N ± stat ± syst
```
Always separate statistical and systematic uncertainties. Never combine without
explicit `stat ⊕ syst` notation.

**Examples:**
- $m_t = 172.5 \pm 0.3\,(\text{stat}) \pm 1.2\,(\text{syst})~\text{GeV}$
- Cross-section: $\sigma = 12.3 \pm 0.4\,(\text{stat}) \pm 1.1\,(\text{syst}) \pm 0.3\,(\text{lumi})~\text{pb}$

### Systematic Uncertainty Categories
When listing systematics, use standard HEP categories:

| Category | Symbol | Notes |
|----------|--------|-------|
| Jet energy scale | JES | Quote for leading jet pT threshold |
| Jet energy resolution | JER | Smearing method |
| b-tagging efficiency | b-tag | Per-flavor: b, c, light |
| Pile-up | PU | In-time + out-of-time |
| Luminosity | lumi | Report as ±X% separately |
| PDF uncertainty | PDF | Specify set + eigenvectors |
| Renorm./factor. scales | scale | Quote 7-point or envelope |
| Trigger efficiency | trig | Per-trigger path |
| Lepton ID/isolation | lep ID | Per-flavor, per-year |

### Statistical Significance
- Always quote observed significance AND expected significance
- State confidence level method: CLs, Feldman-Cousins, or asymptotic approximation
- $p$-value for discovery: $p_0$ with conversion to Gaussian $\sigma$
- Exclusion limits: 95% CL unless stated otherwise

---

## 3. Citation Style (INSPIRE-HEP)

### Key Format
```
Author:YYYYidentifier
```
Examples: `CMS:2023abc`, `ATLAS:2022xyz`, `Higgs:1964pj`, `Cacciari:2008gp`

- Large collaborations: `CMS:`, `ATLAS:`, `LHCb:`, `ALICE:`, `Belle:`, `BaBar:`
- Theory papers: `Author1Author2:YYYYid` (first two authors if collaboration is small)

### Mandatory Citations
Every HEP paper must cite:

| Item | Required citation |
|------|------------------|
| PDG values (masses, widths, CKM) | `ParticleDataGroup:2022pth` (update year) |
| MadGraph5_aMC@NLO | `Alwall:2014hca` |
| Pythia 8 | `Bierlich:2022pfr` (Pythia 8.3) or `Sjostrand:2014zea` (8.2) |
| Herwig 7 | `Bellm:2015jjp` |
| Sherpa | `Sherpa:2019gpd` |
| FastJet | `Cacciari:2011ma` |
| anti-kt algorithm | `Cacciari:2008gp` |
| GEANT4 | `GEANT4:2002zbu` |
| PYTHIA 6 (if used) | `Sjostrand:2006za` |

### Citation Verification
- Check all INSPIRE keys resolve to the correct paper before submission
- For preprints, prefer published version keys if available
- Competing experiment results must be cited when claiming "first observation" or "most precise"
- NLO/NNLO theory calculations must cite the specific code or paper providing the prediction

---

## 4. Journal Format Standards

| Journal | Publisher | Page limit | Columns | Notes |
|---------|-----------|-----------|---------|-------|
| PRL | APS | 4 pages | 1 | Tight; no subsections in intro; long author list in supplement |
| PRD | APS | Open | 2 | Full systematic tables; detailed appendices |
| JHEP | SISSA/Springer | Open | 2 | Appendices for lengthy derivations; JHEP style file |
| PLB | Elsevier | ~6 pages | 2 | Brief letters format; key plots only |
| EPJC | Springer | Open | 2 | Full paper; HEP community standard for many theory papers |

### PRL-Specific Rules
- Abstract: ≤600 characters
- No `\subsection` in Introduction
- Supplemental Material is separate document; label all Supplemental refs as "S[N]"
- Use `letter` class or `revtex4-2` with `[aps,prl,reprint]` options

### Figure and Table Requirements
- Every figure/table must be self-contained: axis labels with units, caption with full description
- Figures: minimum 300 dpi; vector formats (PDF, EPS) strongly preferred
- Tables: statistical and systematic uncertainties in separate columns
- Error bars: quote 68% CL (1σ) unless specified; label if 95% CL bands shown

---

## 5. Reviewer Response Etiquette

### Opening Formula (required)
Begin the response letter with:
> "We thank the editor and the reviewers for their careful reading of our manuscript
> and their constructive comments. We have revised the manuscript accordingly and
> address each point in detail below."

### Per-Point Protocol
1. **Paraphrase** the reviewer concern in ≤10 words as a subsection heading
2. **Quote verbatim** the reviewer's exact text in a block quote
3. **Respond substantively** — acknowledge valid criticisms; never be dismissive
4. **Justify disagreements** with physics arguments, literature references, or statistics
5. **Give exact refs** for every manuscript change: Section X, page Y, line Z, Eq. (N)
6. **Never skip a point** — if a concern is trivial, still acknowledge and explain briefly

### Common HEP Reviewer Concerns (Know These)
Reviewers at PRL/JHEP/PRD typically ask about:

| Topic | Typical request |
|-------|----------------|
| NLO corrections | "Are QCD corrections included? What is the K-factor?" |
| Pile-up treatment | "How are pile-up jets suppressed? JVT/PUPPI?" |
| Jet algorithm | "Which jet algorithm and radius parameter?" |
| Luminosity uncertainty | "Is lumi uncertainty included in the limit?" |
| PDF uncertainty | "Which PDF set? Are PDF uncertainties evaluated?" |
| BSM comparison | "Compare with existing exclusion contours from X" |
| MC generator | "Which version of Pythia/Herwig? What tune?" |
| Trigger efficiency | "Is trigger efficiency measured in data or simulation?" |
| Signal contamination | "Is signal contamination in control regions checked?" |
| Statistical method | "Is the CLs or Bayesian method used for limits?" |

### Tone Guidelines
- Professional and collegial — reviewers volunteer their time
- Genuine corrections: "We thank the reviewer for this important observation..."
- Justified disagreements: "We respectfully disagree because..."
- Never: "The reviewer has misunderstood...", "As we clearly stated..."
- Include complete **change log table** at end of response

---

## 6. HEP LaTeX Conventions

### Required Packages
```latex
\usepackage{amsmath}      % Core math
\usepackage{amssymb}      % Math symbols
\usepackage{slashed}      % Feynman slash: \slashed{p}
\usepackage{hepunits}     % SI units: \GeV, \TeV, \fb, \pb
\usepackage{hepnames}     % Particle names: \Pep, \Pem, \PZ
\usepackage{booktabs}     % Professional tables: \toprule, \midrule, \bottomrule
\usepackage{siunitx}      % Consistent number formatting
```

### Standard Macros (define in macros.tex)
```latex
\newcommand{\MET}{E_T^{\mathrm{miss}}}
\newcommand{\pT}{p_{\mathrm{T}}}
\newcommand{\HT}{H_{\mathrm{T}}}
\newcommand{\mll}{m_{\ell\ell}}
\newcommand{\mjj}{m_{jj}}
\newcommand{\GeV}{\,\text{GeV}}
\newcommand{\TeV}{\,\text{TeV}}
\newcommand{\fb}{\,\text{fb}^{-1}}
\newcommand{\pb}{\,\text{pb}^{-1}}
\newcommand{\as}{\alpha_s}
\newcommand{\CLs}{\text{CL}_s}
```

### Number Formatting
- Large numbers: use `\num{12345}` from siunitx (adds thin spaces: 12 345)
- Units always in roman (upright): `\text{GeV}`, not `GeV` in math mode
- Ranges: `$100 < m_{jj} < 200~\GeV$` — use `<` not dash in physics ranges
- Percentages: `20\%` in text, `20\,\%` in math

### Equation Numbering
- Number all equations that are referenced; suppress others with `equation*`
- Cross-reference as `Eq.~(\ref{eq:label})` — always `Eq.` not `equation`
- Multi-line equations: use `align` environment, not `eqnarray`
