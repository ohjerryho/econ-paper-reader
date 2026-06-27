# econ-paper-reader

> A structured skill system for reading, interpreting, and critically analyzing economics papers.

**Author**: ohjerryho  
**Version**: 0.6.0  
**License**: MIT

---

## What this skill does

Economics papers have a strict narrative logic — every section has a job, every table tells
part of a story, and every identification strategy rests on specific assumptions. Reading well
means knowing what to expect from each piece.

`econ-paper-reader` teaches an AI agent these conventions by reversing the standards of
top-journal writing. The result: structured, critical analysis of any economics paper —
whether it's an AER empirical study, a QJE theory paper, an Econometrica structural model,
or a Chinese CSSCI policy paper.

---

## Skill structure

This is a **skill collection** — a main orchestrating skill plus eight specialized subskills
and four reference files.

```
econ-paper-reader/
├── SKILL.md                            ← Main skill: classify, route, produce reading report
├── README.md                           ← This file
├── README_CN.md                        ← Chinese README
│
├── subskills/
│   ├── epr-structure/SKILL.md          ← Paper anatomy: what each section should contain
│   ├── epr-empirical/SKILL.md          ← Reading empirical papers (RF and structural)
│   ├── epr-theory/SKILL.md             ← Theory and structural model papers
│   ├── epr-methodology/SKILL.md        ← Econometrics/methods papers
│   ├── epr-causal-inference/SKILL.md   ← Identification strategies: DiD, IV, RDD, SC, etc.
│   ├── epr-tables-figures/SKILL.md     ← Reading regression tables, event studies, RD plots
│   ├── epr-policy-context/SKILL.md     ← Extract and organize policy/institutional context
│   └── epr-related-refs/SKILL.md       ← Select & format key related references (ref-format)
│
└── references/
    ├── paper-taxonomy.md               ← Classification system for economics papers
    ├── causal-methods-ref.md           ← Deep reference: CI methods with diagnostics
    ├── theory-components-ref.md        ← Model primitives, equilibria, proof reading
    └── chinese-vs-english.md           ← Chinese vs. English paper conventions
```

The `epr-` prefix namespaces all subskills to avoid conflicts with other skill sets.

Subskill routing is **deterministic by paper type** — once the paper is classified, exactly
the right subskills are loaded. No over-loading, no guessing.

---

## What the skill can do

| Task | Relevant subskill(s) |
|------|---------------------|
| Classify a paper (empirical / theory / structural / mixed) | `epr-structure` + `paper-taxonomy.md` |
| Produce a full structured reading report | All relevant subskills |
| Tell the paper's research story in narrative form | Main SKILL.md (opening section) |
| Extract policy/event context and institutional background | `epr-policy-context` |
| Reproduce and explain key regression or model equations | `epr-empirical` / `epr-theory` |
| Evaluate an identification strategy | `epr-causal-inference` + `causal-methods-ref.md` |
| Read and interpret regression tables | `epr-tables-figures` |
| Decode theory model assumptions and propositions | `epr-theory` + `theory-components-ref.md` |
| Read econometrics / methods papers | `epr-methodology` |
| Assess a paper at referee level | All subskills |
| Read Chinese CSSCI papers | `epr-policy-context` + `chinese-vs-english.md` |
| Recommend key related references | `epr-related-refs` |

---

## How to use

### With Claude Code / AWS Kiro

Place this directory in your `.claude/skills/` folder (or wherever your agent loads skills).
Then simply ask:

> "Read this paper and tell me if the identification is convincing."  
> "Summarize the main findings of this working paper."  
> "Help me understand the model in Section 3."  
> "What does Table 2 show?"

The skill triggers automatically on economics paper reading tasks.

### PDF support

This skill works best alongside a PDF reading tool. Most economics papers are distributed as
PDFs — without PDF reading capability, paste the paper text manually.

### Reading modes

**Quick scan** (~5 min): Abstract + intro + conclusion + skim tables.

**Standard read**: Full paper with structured report.

**Referee read**: Full critical evaluation, section by section.

---

## Token usage

This is a **heavy skill** by design — thoroughness requires reading multiple subskill files
plus the full paper. Expect approximately:

| Paper length | Approximate token cost |
|---|---|
| Short paper / working paper (~20–30 pages) | ~150k–200k tokens |
| Full journal article (~40–50 pages) | ~200k–300k tokens |

These figures are for Opus-class models doing a standard read. Quick-scan mode uses
significantly fewer tokens. Budget accordingly if running at scale.

---

## Reading report format

The skill produces a standardized report with these sections:

```
# [Paper Title]

作者 / 来源 / 研究领域 / Paper type

──────────────────────────────────────────

这篇文章讲了个什么故事
  A full narrative opening: background, gap, approach, findings, significance

政策与背景  [empirical / Chinese-language papers]
  Policy/event table + political/institutional context

核心问题
  One-sentence research question

研究设计
  Identification strategy or model approach

模型设定  [theory / structural papers]
  Core equations in LaTeX + symbol table + ⚠️ key assumptions

实证设计  [reduced-form empirical papers]
  Estimating equations in LaTeX + variable table + ⚠️ design flags

主要发现
  Key results with economic magnitudes

核心贡献
  Novel claims vs. prior literature

亮点
  Strongest aspects of the paper

不足与疑问
  Identification threats, model weaknesses, missing robustness

综合评价
  Overall verdict and publishability assessment

延伸阅读
  Key related references from the paper's reference list (ref-format)
```

---

## Design philosophy

This skill is built on a key insight: **reading and writing are inverses**. Top-journal writing
follows strict conventions — every section has expected content, every identification strategy
has required diagnostics, every theory paper has standard components. By encoding these writing
conventions, the skill knows exactly what to *look for* when reading.

---

## Changelog

### v0.6.0 (2026-06-27)
- Opening section renamed to **这篇文章讲了个什么故事** — full narrative, not a brief summary
- Subskill routing is now **deterministic by paper type** (explicit table, no guessing)
- Added **模型设定** mandatory block for theory/structural papers (equations + symbol table + ⚠️ assumptions)
- `epr-related-refs`: removed forced count — quality over quantity, no padding

### v0.5.0 (2026-06-27)
- Added `epr-policy-context` subskill: policy/event table + political/institutional background
- Added **政策与背景** section to report template (empirical and Chinese-language papers)

### v0.4.1 (2026-06-27)
- Added opening summary section (一句话总结, later renamed in v0.6.0)

### v0.4.0 (2026-06-27)
- Added **实证设计** mandatory block for RF papers: LaTeX equations, variable table, ⚠️ design flags

### v0.3.1 (2026-06-27)
- Section header language consistency rule; README updates

### v0.3.0 (2026-06-27)
- Added `epr-related-refs` subskill with ref-format integration
- Simplified report header; banned internal monologue from output

### v0.2.0 (2026-06-27)
- Added `epr-methodology` subskill; `README_CN.md`

### v0.1.0 (2026-06-27)
- Initial release: 5 subskills + 4 reference files
