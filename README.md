# econ-paper-reader

> A structured skill system for reading, interpreting, and critically analyzing economics papers.

**Author**: ohjerryho  
**Version**: 0.1.0  
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

This is a **skill collection** — a main orchestrating skill plus five specialized subskills
and four reference files.

```
econ-paper-reader/
├── SKILL.md                          ← Main skill: classify, route, produce reading report
├── README.md                         ← This file
│
├── subskills/
│   ├── epr-structure/SKILL.md        ← Paper anatomy: what each section should contain
│   ├── epr-empirical/SKILL.md        ← Reading empirical papers (RF and structural)
│   ├── epr-theory/SKILL.md           ← Reading theoretical model papers
│   ├── epr-causal-inference/SKILL.md ← Identification strategies: DiD, IV, RDD, SC, etc.
│   └── epr-tables-figures/SKILL.md   ← Reading regression tables, event studies, RD plots
│
└── references/
    ├── paper-taxonomy.md             ← Classification system for economics papers
    ├── causal-methods-ref.md         ← Deep reference: 10 CI methods with diagnostics
    ├── theory-components-ref.md      ← Model primitives, equilibria, proof reading
    └── chinese-vs-english.md         ← Chinese vs. English paper conventions
```

---

## What the skill can do

| Task | Relevant subskill(s) |
|------|---------------------|
| Classify a paper (empirical / theory / structural / mixed) | `epr-structure` + `paper-taxonomy.md` |
| Produce a structured reading report | All relevant subskills |
| Evaluate an identification strategy | `epr-causal-inference` + `causal-methods-ref.md` |
| Read and interpret a regression table | `epr-tables-figures` |
| Decode a theory model's assumptions and propositions | `epr-theory` + `theory-components-ref.md` |
| Assess a paper at referee level | All subskills |
| Read Chinese-language economics papers | `chinese-vs-english.md` |
| Quick-scan a paper for key takeaways | `epr-structure` (quick mode) |

---

## How to use

### With Claude Code / AWS Kiro

Place this directory in your `.claude/skills/` folder, or point your skill loader at it.
Then simply ask:

> "Read this paper and tell me if the identification is convincing."  
> "Summarize the main findings of this working paper."  
> "Help me understand the model in Section 3."  
> "What does Table 2 show?"

The skill triggers automatically on economics paper reading tasks.

### Reading modes

**Quick scan** (~5 min): Abstract + intro + conclusion + skim tables.
> "Quick read this paper for me."

**Standard read**: Full paper with structured report.
> "Read this paper and give me a reading report."

**Referee read**: Full critical evaluation, section by section.
> "Review this paper like a referee for the AER."

---

## Paper types supported

| Type | Coverage |
|------|---------|
| Empirical — Reduced Form | ✅ Full (DiD, IV, RDD, SC, RCT, Matching, Bunching) |
| Empirical — Structural | ✅ Full (BLP, dynamic, contracting) |
| Theoretical | ✅ Full (all standard model architectures) |
| Mixed (theory + empirics) | ✅ Full |
| Survey / Review papers | ✅ Basic |
| English top journals | ✅ AER, QJE, JPE, REStud, Econometrica, etc. |
| Chinese CSSCI journals | ✅ With dedicated Chinese conventions guide |
| Working papers | ✅ |

---

## Reading report format

The skill produces a standardized report:

```
## Reading Report: [Paper Title]

Citation: Authors (Year). "Title." Journal.
Paper type: [Empirical-RF / Theory / Mixed / etc.]
Style: [English top-journal / Chinese CSSCI / Working paper]

Core question       — What the paper asks
Research design     — How it answers the question
Key results         — 2–4 findings with economic magnitudes
Stated contribution — What the authors claim is novel
What works well     — Strongest aspects
Concerns            — Threats to identification / model weaknesses
Overall verdict     — Convincing? Publishable? Why?
```

---

## Background and design philosophy

This skill was designed around a key insight: **reading and writing are inverses**. Top-journal
writing follows strict conventions — every section has expected content, every identification
strategy has required diagnostics, every theory paper has standard components. By encoding
these writing conventions, the skill knows exactly what to *look for* when reading.

Source material drawn from:
- **Writing conventions**: AER-Skills, econ-writing-skill (synthesis of 50+ top economist guides), research-writing-skill
- **Causal inference**: Cunningham (2021) *Causal Inference: The Mixtape* + Codex Stata for Economists
- **Theory models**: pAI-Econ-claude model library (Chen Zhu, Xiaolu Wang, Weilong Zhang; CAU / Cambridge)
- **Chinese economics conventions**: Institutional knowledge of Chinese CSSCI standards and data sources

---

## Development and contributing

This skill is under active development. Planned additions:
- `epr-welfare`: Reading welfare analysis and sufficient statistics papers
- `epr-heterogeneity`: Reading CATE / distributional analysis sections
- `epr-replication`: Assessing reproducibility and replication potential
- Expanded Chinese institutional context (more policy events)

To contribute or report issues, open an issue or PR at the GitHub repository.

---

## Changelog

### v0.1.0 (2026-06-27)
- Initial release
- 5 subskills: epr-structure, epr-empirical, epr-theory, epr-causal-inference, epr-tables-figures
- 4 reference files: paper-taxonomy, causal-methods-ref, theory-components-ref, chinese-vs-english
