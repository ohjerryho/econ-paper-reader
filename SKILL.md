---
name: econ-paper-reader
version: 0.3.0
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
subskills/epr-related-refs/SKILL.md     ← always load last; selects and formats top-3 related references
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

**CRITICAL output rules**:
1. Begin the report immediately with the paper title. Never write processing notes, progress summaries, or internal comments such as "Now I have enough material…", "Based on my reading…", or any similar meta-commentary before or after the report body. The report is the only output.
2. Section headers must be **consistent in language throughout the report** — either all Chinese or all English. Never mix. Parenthetical translation is allowed (e.g., "核心问题 (Core Question)" or "Key Results（主要发现）"). Choose the language that matches the main body language of the report.

```
# [论文标题 / Paper Title]

**作者**: [Authors]
**来源**: [Journal / Source, Year]
**研究领域**: [e.g., 国际贸易、产业组织、劳动经济学]
**Paper type**: [e.g., Empirical-RF / Theory / Mixed / Methodology]

---

### 核心问题

[一句话：本文回答什么问题？]

### 研究设计

[如何回答？简述识别策略或理论框架。]

### 主要发现

- [发现1——实证类请给出经济量级]
- [发现2]
- [发现3（如有）]

### 核心贡献

[作者主张的创新点是什么？如何与既有文献区分？]

### 亮点

[最有说服力之处：识别策略干净、模型优雅、数据丰富、叙事清晰等]

### 不足与疑问

[核心假设是否承压、识别威胁、机制逻辑漏洞、缺失的稳健性检验、系数解读是否合理等]

### 综合评价

[是否令人信服？为何？如有必要，粗略评估发表价值或引用价值。]

---

### 延伸阅读

[Top 3 most relevant references from this paper's reference list.
Follow epr-related-refs subskill for selection criteria and ref-format formatting rules.
If fewer than 3 clearly relevant references exist in the paper's reference list, only list those that are genuinely relevant — never fabricate or guess.]
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
