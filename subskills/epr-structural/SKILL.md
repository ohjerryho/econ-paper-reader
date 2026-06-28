---
name: epr-structural
version: 0.1.0
author: ohjerryho
description: >
  Paper anatomy subskill for econ-paper-reader. Teaches the expected content and logic of
  each section of an economics paper, derived from top-journal writing conventions in reverse.
  Load this as the first step whenever reading any economics paper.
---

# epr-structural — Paper Anatomy

Top-journal papers follow a predictable architecture. Each section has a job to do. Reading
well means knowing what each section *should* contain — so you can recognize when it delivers
and when it falls short.

## Abstract (150–250 words)

A well-written abstract is the whole paper in four moves:
1. **Motivation**: Why does the question matter?
2. **What we do**: Research design in one sentence.
3. **Main result**: The key finding, with magnitude if quantitative.
4. **Contribution / So what**: Why this advances knowledge.

Reading tip: If the abstract is vague about the identification strategy or the main result,
that's a yellow flag — either the paper is genuinely exploratory, or the authors are hedging.

## Introduction (~10% of paper length)

The introduction is the most important section. A top-journal introduction follows this arc:

1. **Hook / Motivating fact** — One striking fact or puzzle that opens the question.
2. **Research question** — Precisely stated.
3. **What this paper does** — Preview of the research design in 2–3 sentences.
4. **Main results** — Key findings, stated quantitatively where applicable.
5. **Contribution** — "This paper contributes to X literature by doing Y." Often explicit.
6. **Related literature** — Brief positioning (or full section if the paper has a lit review).
7. **Roadmap** — Section outline (Section 2 describes data, Section 3 presents the model...).

Reading tip: The intro makes promises. Read the conclusion to check how well they were kept.
If the intro says "we find X" but the results section only finds X with caveats, note that gap.

## Literature Review / Related Work

Positions the paper along 2–4 strands of existing literature. In top-journal English papers,
this is often woven into the introduction rather than a standalone section. In Chinese papers,
a standalone 文献综述 section is more common.

Reading tip: Literature review reveals what the authors consider the paper's predecessors.
Ask: Is the most directly competing paper included? How does this paper differ from it?

## Data Section

Describes the dataset(s) used. Should contain:
- Data source, time period, level of observation (firm/worker/county/individual)
- Sample construction and selection criteria (and any restrictions to worry about)
- Summary statistics table (mean, SD, min, max by key variables)
- Variable definitions (especially the main outcome and treatment variables)

Reading tip: Sample restrictions are where selection bias hides. Check footnotes carefully.
The summary statistics table tells you the scale of variation — essential for interpreting
coefficient magnitudes later.

## Theoretical Model / Model Setup

When present, the model section establishes:
- **Primitives**: agents, preferences, technology, endowments, information structure
- **Timing**: the sequence of decisions
- **Equilibrium concept**: Nash, competitive equilibrium, mechanism, etc.
- **Key predictions**: propositions or comparative statics that motivate the empirics

Reading tip: Don't get lost in math. Identify the 1–2 core mechanisms the model is trying
to capture. The rest is usually technical scaffolding. For theory papers, see `epr-theoretical`.

## Empirical Strategy / Identification Section

The core of an empirical paper. Should clearly state:
- Estimating equation (often displayed prominently)
- Source of identifying variation (what makes the treatment "as-good-as-random")
- Key identifying assumptions (stated explicitly or implicitly)
- Threats to identification and how they're addressed

Reading tip: This is where you should be most skeptical. Ask: Is the variation truly
exogenous? Is there a plausible mechanism for the exclusion restriction? Load `epr-causal-inference`
for method-specific reading guides.

## Results Section

Presents the main findings, usually organized around one or more key tables or figures.

Structure in reduced form papers:
1. Main specification (baseline result)
2. Controls robustness (adding covariates)
3. Heterogeneity analysis (subgroup effects)
4. Mechanism tests (why does the effect exist?)

Structure in structural papers:
1. First-stage / selection model estimates
2. Structural parameters
3. Model fit (does the model match data moments?)
4. Counterfactuals

Reading tip: Focus on Column (1) first — that's often the author's preferred specification.
Then read the other columns as sensitivity checks. Load `epr-tables-figures` for help reading
regression tables.

## Robustness Section

Shows the main results survive alternative specifications, samples, and assumptions. Common checks:
- Alternative outcome definitions
- Alternative sample restrictions
- Controlling for different covariates
- Placebo tests
- Bounding exercises (sensitivity to violation of key assumptions)

Reading tip: What's **not** in the robustness section is as informative as what is. If an
obvious threat isn't addressed, either the authors don't consider it a threat (ask why) or
they couldn't rule it out.

## Mechanism / Heterogeneity Analysis

Answers "why?" and "for whom?". This is increasingly required in top journals.

- **Mechanism channels**: intermediate outcomes consistent with the proposed mechanism
- **Heterogeneity by group**: subgroup analysis revealing who is affected and when
- **Theory-guided predictions**: heterogeneity patterns the theory predicts should be present

Reading tip: This section is often thinner than it should be. A result is more convincing
when we understand the mechanism. Weak mechanism evidence is a common referee complaint.

## Conclusion

Summarizes findings and discusses implications. Often contains:
- One-paragraph summary of the paper
- Policy implications (especially in applied work)
- Limitations and caveats
- Future research directions

Reading tip: Compare the conclusion's claims to the evidence actually presented. Good papers
are honest about what their design can and cannot identify.

## Appendix

Contains what didn't fit in the main text:
- Detailed proofs (for theory papers)
- Data construction details
- Additional robustness tables
- Online appendix (often as extensive as the main paper)

Reading tip: For credibility concerns, the appendix is often where the key robustness tests
live. If a reviewer found a gap, the authors may have addressed it here.

---

## Section quality signals

| Green flags | Red flags |
|------------|-----------|
| Research question stated precisely in intro | Vague contribution claim ("we add to the literature") |
| Identification assumption stated explicitly | Identification section absent or buried |
| Economic magnitude interpreted in text | Only statistical significance reported |
| Robustness section addresses most obvious threats | Robustness checks only confirm already-robust specs |
| Mechanism analysis consistent with the theory | Mechanism section tests convenient, not core, channels |
| Summary statistics enable coefficient interpretation | Summary stats missing or incomplete |
