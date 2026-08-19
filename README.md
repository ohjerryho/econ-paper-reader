<p align="center">
  <img src="assets/cover.png" alt="econ-paper-reader cover" width="100%">
</p>

<h1 align="center">econ-paper-reader</h1>

<p align="center">
  <strong>A structured AI reading skill system for economics papers.</strong>
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
  <a href="#quick-start">Quick start</a>
  ·
  <a href="#usage">Usage</a>
</p>

<p align="center">
  <img alt="Version" src="https://img.shields.io/badge/version-0.9.1-0b4f5c">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-e8ad63">
  <img alt="Domain" src="https://img.shields.io/badge/domain-economics%20papers-234">
  <img alt="Skill" src="https://img.shields.io/badge/type-agent%20skill%20system-5fb2ab">
</p>

---

## What this skill does

Economics papers are not ordinary informational texts. They have a relatively stable narrative
logic: every section has a job, every table carries part of the argument, and every identification
strategy rests on assumptions that must be checked rather than merely summarized.

`econ-paper-reader` is designed to make an AI agent read papers more like a trained economics
researcher: first classify the paper type, then load the right analytical lenses, reconstruct the
research story, and finally evaluate whether the research design, model specification, tables,
figures, and author claims actually fit together.

`econ-paper-reader` is for users who want to quickly grasp the basic logic and key information of
economics papers. It goes beyond generic summary or introductory description: it organizes the
paper structurally around the research question, theoretical mechanism, identification strategy,
data sources, main conclusions, and potential value.

`econ-paper-reader` does not replace real deep reading. It is better used as a literature screening
and pre-reading tool, helping users quickly decide whether a paper matches their research interests
and research needs before investing in close reading.

The core idea is simple:

> **Reading and writing are inverse processes.**  
> Top-journal writing follows recognizable conventions. By encoding those conventions in
> reverse, the agent knows what to look for when reading.

This is not a generic paper summarizer. It is a domain-specific reading system for economics
papers, covering:

- general reduced-form empirical papers;
- structural estimation papers;
- theoretical model papers;
- econometric methods papers;
- theory + empirical mixed papers;
- review articles.

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

## Not meant for

This skill does not replace:

- deep expert-level interpretation;
- actual replication with data and code;
- formal proof verification;
- field-specific expert judgment;
- systematic literature discovery outside the paper's own reference list.

It helps the agent read more like a trained economics researcher. It does not make the paper
true, causal, publishable, or correctly identified by itself.

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
│   ├── epr-structural/SKILL.md         # Paper anatomy and section expectations
│   ├── epr-empirical/SKILL.md          # Reduced-form and structural empirical papers
│   ├── epr-theoretical/SKILL.md        # Theory and structural model reading
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
| **Empirical - Reduced Form** | `epr-structural` -> `epr-empirical` -> `epr-causal-inference` -> `epr-tables-figures` |
| **Empirical - Structural** | `epr-structural` -> `epr-empirical` -> `epr-theoretical` -> `epr-tables-figures` |
| **Theoretical** | `epr-structural` -> `epr-theoretical` |
| **Methodology** | `epr-structural` -> `epr-methodology` -> `epr-causal-inference` if identification strategies are critiqued |
| **Mixed** | `epr-structural` -> `epr-empirical` -> `epr-theoretical` -> `epr-causal-inference` -> `epr-tables-figures` |
| **Survey / Perspective** | `epr-structural` |

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

## Quick start

Install the skill by cloning this repository into the skill directory used by your agent.

### Codex

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/ohjerryho/econ-paper-reader.git ~/.codex/skills/econ-paper-reader
```

Restart Codex after installation so the new skill metadata is loaded.

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/ohjerryho/econ-paper-reader.git ~/.claude/skills/econ-paper-reader
```

Restart Claude Code after installation so the skill becomes available.

### Update an existing install

```bash
git -C ~/.codex/skills/econ-paper-reader pull
# or, for Claude Code:
git -C ~/.claude/skills/econ-paper-reader pull
```

If you use a different agent runtime, install the repository as a skill folder named
`econ-paper-reader`, with `SKILL.md` at the root of that folder.

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
distributed as PDFs; if the current agent does not have PDF parsing capability, it is best
to equip it with the relevant skills or MCP servers.

### Reading modes

| Mode | Best for | Typical output |
|---|---|---|
| **Quick scan** | Triage, citation decisions, first-pass reading | 3-5 sentence summary plus key caveats |
| **Standard read** | Research notes and seminar preparation | Full structured reading report |
| **Referee read** | Deep critique, replication planning, publication judgment | Extended concerns, design threats, verdict |

## Token usage

This is not a **lightweight skill**. A complete economics-paper reading task usually involves PDF
extraction, table/figure inspection, subskill loading, section rereading, report drafting, and
revision. The table below gives tested **end-to-end workflow** budget estimates.

| Paper length / type | Budget |
|---|---:|
| Short paper, about 20-30 pages | 150k-200k tokens |
| Full journal article, about 40-50 pages | 200k-300k tokens |

## Changelog

### v0.9.1 (2026-08-19)
- **理论基础 field**: report header gains a **理论基础** metadata field listing every theoretical branch the paper belongs to, sourced strictly from the author's own statements in the introduction or literature review ("this paper contributes to the literature on X"). Format: `理论名称 (Anchor reference, year)`. If no explicit author self-statement is found, the field is left blank — no inference.

### v0.9.0 (2026-08-19)
- **Data sources block**: `epr-empirical` now opens the 实证设计 section with a mandatory **数据说明 (Data Sources & Coverage)** table listing every dataset used — name, provider, observation level, time span, sample size, and accessibility (public / restricted / proprietary). Merge logic and sample selection criteria are noted when present.
- **Variable table extended**: the 变量说明 table gains a **数据来源** column so every variable's origin is visible at a glance. Cross-references the数据说明 table; a single-dataset note at the header may substitute when all variables share one source.
- **Mechanism variable table extended**: the per-mechanism variable table also gains a **数据来源** column, flagging any new dataset not in the main数据说明.
- **Inline source notes for robustness / heterogeneity / further analysis**: instructions added to note new data sources in-place when those sections introduce datasets beyond the main数据说明 table.

### v0.8.2 (2026-06-29)
- **LaTeX rule strengthened**: isolated math symbols and Greek letters in running text must also use `$...$`; backtick inline code (`` `x_i` ``) for math is now explicitly banned
- **研究设计 template**: now explains the bridge from real-world question → model variables/equations → analysis dimensions (mechanism, heterogeneity, etc.)
- **epr-empirical**: mechanism analysis and further analysis follow the paper's own logical structure (narrative + equations); rigid table format only required for robustness and heterogeneity

### v0.8.1 (2026-06-29)
- Moved **亮点 / 不足 grounding rule** from `epr-empirical` to main `SKILL.md` — now applies to ALL paper types, not just empirical papers

### v0.8.0 (2026-06-29)
- **epr-empirical**: Full rewrite of mandatory output block — all sections now use structured tables, not prose dumps
  - Fixed effects table includes a **rationale column** (what variation each FE absorbs and why)
  - New **IV validity block**: relevance (first-stage F / correlation), exclusion restriction argument, weak instrument test
  - **Mechanism analysis**: regression equation in LaTeX + variable construction table + channel role + result per mechanism
  - **Heterogeneity analysis**: structured table (group → coefficient → relation to baseline → implication)
  - **Further analysis**: design logic + empirical setup + result + link to core question, per analysis
  - **亮点 / 不足 rules**: every point must be grounded in THIS paper's specifics; author-acknowledged limitations labeled separately from reader-identified concerns

### v0.7.1 (2026-06-28)
- Renamed subskills for consistent adjective-form naming: `epr-structural` → `epr-structural`, `epr-theoretical` → `epr-theoretical`, `epr-review` → `epr-review`
- All internal references updated accordingly
- Clarified token-usage guidance: workflow budget vs. static context payload

### v0.7.0 (2026-06-28)
- **epr-empirical**: Expanded mandatory 实证设计 block — baseline FE/clustering spec, robustness/endogeneity, mechanism analysis, heterogeneity analysis, further analysis
- **epr-theoretical**: Added mandatory 校准与参数设定 block for structural/calibration papers
- **New epr-review subskill**: Field development timeline, benchmark papers table, literature logic diagram (Mermaid), unlimited 延伸阅读 for benchmark papers
- **epr-related-refs**: Survey paper override — no cap on references when paper type is review/survey
- Routing table updated to route Survey/Perspective to `epr-structural → epr-review`

<details>
<summary><strong>v0.6.1 and earlier</strong></summary>

### v0.6.1 (2026-06-28)

- Added Quick start installation instructions for Codex, Claude Code, and generic agent runtimes.
- Added update commands for existing local installs.
- Refreshed README presentation with a project cover image and bilingual documentation.

### v0.6.0 (2026-06-28)

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
