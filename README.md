<p align="center">
  <img src="assets/cover.png" alt="econ-paper-reader cover" width="100%">
</p>

<h1 align="center">econ-paper-reader</h1>

<p align="center">
  <strong>A structured skill system for reading, interpreting, and critically analyzing economics papers.</strong>
</p>

<p align="center">
  <a href="README_CN.md">中文说明</a>
  ·
  <a href="#what-this-skill-does">What it does</a>
  ·
  <a href="#architecture">Architecture</a>
  ·
  <a href="#reading-output">Reading output</a>
  ·
  <a href="#usage">Usage</a>
</p>

<p align="center">
  <img alt="Version" src="https://img.shields.io/badge/version-0.6.0-0b4f5c">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-e8ad63">
  <img alt="Domain" src="https://img.shields.io/badge/domain-economics%20papers-234">
  <img alt="Skill" src="https://img.shields.io/badge/type-agent%20skill%20system-5fb2ab">
</p>

---

## What this skill does

Economics papers have a strict narrative logic: every section has a job, every table carries
part of the argument, and every identification strategy rests on assumptions that must be
checked rather than merely summarized.

`econ-paper-reader` teaches an AI agent to read papers the way an economist reads them:
classify the paper type, load the right analytical lenses, reconstruct the research story,
then evaluate whether the design, model, tables, figures, and claims actually support the
paper's conclusion.

The core idea is simple:

> **Reading and writing are inverse processes.**  
> Top-journal writing follows recognizable conventions. By encoding those conventions in
> reverse, the agent knows what to look for when reading.

This is not a generic summarizer. It is a domain-specific reading system for economics papers:
empirical reduced-form work, structural estimation, theory, econometric methods, mixed papers,
surveys, and Chinese CSSCI-style policy research.

## Highlights

| Capability | What the agent learns to inspect |
|---|---|
| **Paper classification** | Empirical RF, structural, theory, methodology, mixed, survey/perspective |
| **Deterministic subskill routing** | Load only the relevant subskills for the paper type, in a fixed order |
| **Research story reconstruction** | Motivation, gap, design, findings, contribution, and significance |
| **Identification critique** | DiD, IV, RDD, synthetic control, matching, event studies, and common threats |
| **Equation-level reading** | Regression equations, model primitives, equilibrium conditions, symbol tables |
| **Tables and figures** | Regression tables, event-study plots, RD plots, balance tables, robustness tables |
| **Policy context** | Policies, reforms, events, institutional background, especially for Chinese papers |
| **Referee-style evaluation** | Strengths, weaknesses, missing robustness, external validity, publishability |
| **Related references** | Select central references from the paper's own bibliography and format them cleanly |

## Architecture

`econ-paper-reader` is a **skill collection**: one main orchestrating skill, eight specialized
subskills, and four reference files.

<details open>
<summary><strong>Repository layout</strong></summary>

```text
econ-paper-reader/
├── SKILL.md                            # Main skill: classify, route, produce report
├── README.md                           # English README
├── README_CN.md                        # Chinese README
├── assets/
│   └── cover.png                       # GitHub README cover image
│
├── subskills/
│   ├── epr-structure/SKILL.md          # Paper anatomy and section expectations
│   ├── epr-empirical/SKILL.md          # Reduced-form and structural empirical papers
│   ├── epr-theory/SKILL.md             # Theory and structural model reading
│   ├── epr-methodology/SKILL.md        # Econometrics and methods papers
│   ├── epr-causal-inference/SKILL.md   # Identification strategies and diagnostics
│   ├── epr-tables-figures/SKILL.md     # Regression tables, event studies, RD plots
│   ├── epr-policy-context/SKILL.md     # Policy, reform, and institutional context
│   └── epr-related-refs/SKILL.md       # Related reference selection and formatting
│
└── references/
    ├── paper-taxonomy.md               # Paper classification taxonomy
    ├── causal-methods-ref.md           # Deep reference for causal inference methods
    ├── theory-components-ref.md        # Model primitives, equilibria, proof reading
    └── chinese-vs-english.md           # Chinese vs. English paper conventions
```

</details>

The `epr-` prefix namespaces all subskills to avoid collisions with other skill sets.

## Routing logic

The skill first classifies the paper, then loads the appropriate subskills. Routing is
deterministic by design: the agent does not guess which files to load after classification.

| Paper type | Load these subskills, in order |
|---|---|
| **Empirical - Reduced Form** | `epr-structure` -> `epr-empirical` -> `epr-causal-inference` -> `epr-tables-figures` |
| **Empirical - Structural** | `epr-structure` -> `epr-empirical` -> `epr-theory` -> `epr-tables-figures` |
| **Theoretical** | `epr-structure` -> `epr-theory` |
| **Methodology** | `epr-structure` -> `epr-methodology` -> `epr-causal-inference` if identification strategies are critiqued |
| **Mixed** | `epr-structure` -> `epr-empirical` -> `epr-theory` -> `epr-causal-inference` -> `epr-tables-figures` |
| **Survey / Perspective** | `epr-structure` |

Additional routing rules:

- Add `epr-policy-context` when the paper studies a policy, event, reform, or Chinese-language institutional setting.
- Add `epr-related-refs` last for every paper type.
- Load deep reference files only when the relevant subskill instructs it.

## Reading output

The standard report is designed to be useful for research notes, seminar preparation, referee
thinking, and literature review work.

```text
# [Paper Title]

作者 / 来源 / 研究领域 / Paper type

这篇文章讲了个什么故事
  A narrative opening: background, gap, approach, findings, significance

政策与背景
  Policy/event table + institutional context when relevant

核心问题
  One-sentence research question

研究设计
  Identification strategy or theoretical framework

模型设定
  Core model equations + symbol table + key assumptions

实证设计
  Regression equations + variable table + design warnings

主要发现
  Main results with economic magnitudes when applicable

核心贡献
  Novelty relative to prior literature

亮点
  Strongest parts of the paper

不足与疑问
  Identification threats, model weaknesses, missing robustness

综合评价
  Overall judgment and research value

延伸阅读
  Key references selected from the paper's own bibliography
```

## Usage

Place this directory where your agent loads skills, for example:

```text
~/.codex/skills/econ-paper-reader/
~/.claude/skills/econ-paper-reader/
```

Then ask natural questions such as:

```text
Read this paper and tell me if the identification is convincing.
Summarize the main findings of this working paper.
Help me understand the model in Section 3.
What does Table 2 show?
Is this paper worth citing for my literature review?
Give me a referee-style evaluation of this paper.
```

### PDF support

This skill is meant to work alongside a PDF-reading capability. Most economics papers are
distributed as PDFs; without PDF access, paste the paper text or relevant sections manually.

### Reading modes

| Mode | Best for | Typical output |
|---|---|---|
| **Quick scan** | Triage, citation decisions, first-pass reading | 3-5 sentence summary plus key caveats |
| **Standard read** | Research notes and seminar preparation | Full structured reading report |
| **Referee read** | Deep critique, replication planning, publication judgment | Extended concerns, design threats, verdict |

## Good fits

Use this skill when you need to:

- understand the logic of an economics paper rather than merely summarize it;
- evaluate whether an identification strategy is credible;
- decode regression tables, event-study figures, RD plots, or robustness checks;
- reconstruct model assumptions, propositions, equilibrium conditions, and comparative statics;
- extract policy or institutional context from empirical and Chinese-language papers;
- decide whether a paper is useful for a literature review, proposal, referee report, or replication plan.

## Not meant for

This skill does not replace:

- actual replication with data and code;
- formal proof verification;
- field-specific expert judgment;
- a PDF parser or OCR system;
- citation discovery outside the paper's own reference list.

It helps the agent read more like a trained economics researcher. It does not make the paper
true, causal, publishable, or correctly identified by itself.

## Token usage

This is a **heavy skill** by design. A thorough economics-paper reading task may require loading
multiple subskill files plus the paper itself.

| Paper length | Approximate token cost |
|---|---:|
| Short paper / working paper, about 20-30 pages | 150k-200k tokens |
| Full journal article, about 40-50 pages | 200k-300k tokens |

Quick-scan mode is much cheaper because it loads less context and reads selectively.

## Design principles

1. **Read for argument, not just content.**  
   Economics papers make claims through a sequence: motivation -> design/model -> evidence -> contribution.

2. **Treat identification as the spine of empirical work.**  
   The central question is not "what did the authors estimate?" but "why should we believe it is causal?"

3. **Keep equations visible.**  
   Important regressions and models should be reproduced in LaTeX rather than paraphrased away.

4. **Interpret magnitudes economically.**  
   A significant coefficient is not necessarily a meaningful effect.

5. **Separate author claims from reader judgment.**  
   The report should state what the authors argue and then assess whether the argument holds.

## Metadata

| Field | Value |
|---|---|
| Author | `ohjerryho` |
| Repository | `github.com/ohjerryho/econ-paper-reader` |
| Version | `0.6.0` |
| License | `MIT` |

## Changelog

<details>
<summary><strong>v0.6.0 and earlier</strong></summary>

### v0.6.0 (2026-06-27)

- Opening section renamed to **这篇文章讲了个什么故事**: full narrative, not a brief summary.
- Subskill routing is now deterministic by paper type.
- Added mandatory **模型设定** block for theory and structural papers.
- `epr-related-refs` no longer forces a fixed number of references.

### v0.5.0 (2026-06-27)

- Added `epr-policy-context`: policy/event table plus political and institutional background.
- Added **政策与背景** section to the report template.

### v0.4.1 (2026-06-27)

- Added the opening summary section, later upgraded in v0.6.0.

### v0.4.0 (2026-06-27)

- Added mandatory **实证设计** block for reduced-form papers.

### v0.3.1 (2026-06-27)

- Added section-header language consistency rule.

### v0.3.0 (2026-06-27)

- Added `epr-related-refs` with `ref-format` integration.
- Simplified report header and banned internal monologue from output.

### v0.2.0 (2026-06-27)

- Added `epr-methodology`.
- Added `README_CN.md`.

### v0.1.0 (2026-06-27)

- Initial release: 5 subskills and 4 reference files.

</details>
