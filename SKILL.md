---
name: econ-paper-reader
version: 0.1.0
author: ohjerryho
description: >
  Systematic reading, interpretation, and critical analysis of economics papers — empirical,
  theoretical, structural, or mixed; English top-journal or Chinese CSSCI style. Use this skill
  whenever the user needs to read, summarize, analyze, critique, or understand an economics
  paper. Trigger on phrases like: "read this paper", "help me understand this paper", "what's
  the identification strategy", "explain this model", "is this paper convincing", "what does
  this table show", "summarize the findings", "what's the contribution", "how does the theory
  work", "is this identification valid", "what are the main assumptions", "should I cite this",
  "analyze this working paper", "help me understand the econometrics", "what's the story here".
---

# econ-paper-reader

Economics papers communicate through a strict narrative logic — understanding that logic is the
key to reading them well. This skill reverses the conventions of top-journal writing to decode
what each section is *supposed* to contain, then reads accordingly.

## Step 1: Classify the paper

Before reading in depth, determine the paper's dominant mode:

| Type | Defining signals |
|------|-----------------|
| **Empirical — Reduced Form** | Identification section, regression tables, DiD/IV/RDD/SC design, robustness checks |
| **Empirical — Structural** | Model primitives → equilibrium → estimation (GMM/MLE/SMM), counterfactual simulations |
| **Theoretical** | Formal assumptions, propositions, proofs, corollaries, comparative statics |
| **Mixed** | Theory motivates empirics, or empirics validate a structural model |
| **Methodology** | New estimator/test, asymptotic theory, Monte Carlo simulations, methods critique, "how to do X" guide |
| **Survey / Perspective** | Literature mapping, broad citations, no primary identification, often invited |

Most serious papers are **Mixed**. The dominant mode determines which subskill leads; load
additional subskills for supporting sections.

For detailed taxonomy and edge cases → `references/paper-taxonomy.md`

## Step 2: Route to subskills

Load subskills based on the paper type. **Always start with `epr-structure`.**

```
subskills/epr-structure/SKILL.md        ← always load first
subskills/epr-empirical/SKILL.md        ← if empirical sections present
subskills/epr-theory/SKILL.md           ← if theoretical model sections present
subskills/epr-methodology/SKILL.md      ← if paper proposes/critiques an econometric method
subskills/epr-causal-inference/SKILL.md ← if identification strategy is central
subskills/epr-tables-figures/SKILL.md   ← when interpreting tables or figures
```

Additional reference files:
```
references/causal-methods-ref.md        ← deep reference on 10 CI methods
references/theory-components-ref.md     ← model primitives, equilibria, proof reading
references/chinese-vs-english.md        ← when reading Chinese-language papers
```

## Step 3: Read with purpose

Choose reading depth based on the user's goal:

**Quick scan** (5 min): Abstract → Introduction → Conclusion → skim tables.
Activate: `epr-structure` only. Output: 3–5 sentence summary.

**Standard read**: Full paper. All relevant subskills.
Output: Full reading report (format below).

**Referee read**: All subskills + section-by-section critical evaluation.
Output: Reading report with extended Concerns section and a verdict.

## Reading report format

Always produce a structured report. Depth scales with reading mode.

```
## Reading Report: [Short Title]

**Citation**: Authors (Year). "Title." *Journal/Source*.
**Paper type**: [e.g., Empirical-RF / Theory / Mixed / Survey]
**Style**: [English top-journal / Chinese CSSCI / Working paper]

---

### Core question
[One sentence: what question does this paper answer?]

### Research design
[How does the paper answer it? State identification strategy or model approach concisely.]

### Key results
- [Finding 1 — include economic magnitude if empirical]
- [Finding 2]
- [Finding 3, if any]

### Stated contribution
[What does the paper claim is its novel contribution? How does it position against prior work?]

### What works well
[Strongest aspects: clean identification, elegant model, rich data, compelling narrative]

### Concerns / Weaknesses
[Key assumptions under pressure, threats to identification, gaps in mechanism logic,
missing robustness, questionable interpretation of coefficients]

### Overall verdict
[Convincing? Why? Rough assessment of publishability/citation worthiness if relevant.]
```

## Core reading principles

Economics papers tell a **story with logic**, not just a sequence of results. Read to
understand the argument, not just collect findings.

- **Introduction as a map**: A well-written intro contains the whole paper in miniature —
  motivation, gap, research design, main results, contribution. Read it twice: once at the
  start to orient, once at the end to assess whether the paper delivered its promise.

- **Follow the identification logic**: In empirical papers, the central question is always
  "why should we believe this is causal?" The identification section is the paper's spine.
  If it's weak, everything downstream is weakened.

- **Model ≠ empirics**: In mixed papers, the theory model and the empirical section often
  make different claims. Check whether they actually connect — does the theory generate
  testable predictions that the empirics test, or do they run in parallel?

- **Coefficients need economic interpretation**: A statistically significant coefficient
  only matters if the economic magnitude is meaningful. Always ask: "How big is this in
  real-world terms?"

- **Robustness tells you about the authors' confidence**: The choice of robustness checks
  reveals what threats the authors are most worried about. Note what's *missing* from the
  robustness section as much as what's present.
