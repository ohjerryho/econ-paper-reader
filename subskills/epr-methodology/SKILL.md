---
name: epr-methodology
version: 0.1.0
author: ohjerryho
description: >
  Subskill for reading econometrics and research methods papers — papers that propose
  new estimators, prove asymptotic properties, provide Monte Carlo simulations, or
  clarify when and how to apply existing identification strategies. Part of the
  econ-paper-reader skill set.
---

# epr-methodology — Reading Econometrics & Methods Papers

Methods papers are a distinct genre within economics: they contribute to *how* we answer
questions, not directly *what* the answers are. They are theoretical in structure (proofs,
assumptions, theorems) but applied in motivation (they solve a concrete problem faced by
empirical researchers).

## Types of methods papers

### New estimator / procedure papers
Propose a new econometric estimator or testing procedure.
- *Examples*: Callaway-Sant'Anna (2021) on staggered DiD; Calonico-Cattaneo-Titiunik (2014)
  on optimal RD bandwidth; Sun-Abraham (2021) on heterogeneous treatment effect DiD.
- **Core contribution**: A new formula or algorithm that improves on existing approaches.
- **Reading focus**: What problem with existing methods motivates this? What are the new
  estimator's properties (consistency, efficiency, robustness)?

### Identification critique / clarification papers
Show that a widely-used method has problems, and explain under what conditions it fails.
- *Examples*: Goodman-Bacon (2021) on TWFE negative weights; Bertrand-Duflo-Mullainathan (2004)
  on DiD standard errors; de Chaisemartin & D'Haultfoeuille (2020) on heterogeneous DiD.
- **Core contribution**: Diagnosis of a failure mode in existing practice.
- **Reading focus**: Under what conditions does the standard approach fail? How severe is
  the problem in practice? What is recommended instead?

### Survey / synthesis of methods
Review and compare a family of methods; often appear in Journal of Economic Perspectives,
Annual Review of Economics, or as handbook chapters.
- **Reading focus**: What is the taxonomy of methods? Which method fits which setting?
  What are the authors' practical recommendations?

### Application + methods paper
Introduces a new method through an empirical application; the method and application are
co-developed.
- **Reading focus**: Is the method's value added demonstrated clearly in the application?
  Could you use the method on a different dataset?

---

## Reading structure for methods papers

### 1. The motivating problem (Introduction)

Every methods paper starts with a concrete problem: "Researchers do X, but X is wrong / inefficient
/ not identified when Y holds." Read the introduction to extract:

- **The status quo**: What is the standard practice being critiqued or extended?
- **The failure mode**: Under what conditions does the status quo fail?
- **The proposed fix**: One-sentence statement of the new method.
- **The gain**: What improves — consistency, efficiency, power, robustness?

### 2. Setup and assumptions

Methods papers have a model just like theory papers, but the "agents" are data-generating
processes, not economic agents.

Identify:
- **DGP (Data Generating Process)**: What is the assumed model for the data?
- **Key assumptions**: What is required for the new estimator to be valid?
- **Comparison assumptions**: Are the new assumptions weaker or stronger than the status quo?

### 3. Main result: the estimator or test statistic

The equivalent of a "proposition" in theory is the estimator formula or testing procedure.

For a new estimator, find:
- **The formula**: Written out explicitly (e.g., a weighted average of period-specific DiD estimates)
- **Consistency**: Does it converge to the right thing as n → ∞?
- **Asymptotic distribution**: Is it asymptotically normal? At what rate does it converge?
- **Variance estimation**: How are standard errors computed?

For a new test, find:
- **The null hypothesis** and **alternative hypothesis**
- **The test statistic** and its null distribution
- **Size and power**: Is the test well-sized? Does it have power against the relevant alternatives?

### 4. Monte Carlo simulations

Nearly all methods papers include simulation evidence. This is the experimental validation
of the theoretical results.

Reading checklist:
- **DGP of the simulation**: Does it match real data features? Is it too clean?
- **Comparison**: Simulated new method vs. status quo — does new method win?
- **Failure cases**: Does the paper show where the new method also fails? (Honest papers do this.)
- **Sample sizes**: Are the simulation sample sizes realistic for typical applications?

### 5. Empirical application

Usually one or two real-data examples showing the method in action.

Reading focus:
- Does the new method change the substantive conclusion relative to the old approach?
  (If results are identical, the paper has a weaker "so what".)
- Is the application the paper's main selling point, or just illustrative?

---

## Key papers by method (reference)

| Method area | Seminal methods papers |
|-------------|----------------------|
| Staggered DiD | Goodman-Bacon (2021); Callaway-Sant'Anna (2021); Sun-Abraham (2021); de Chaisemartin & D'Haultfoeuille (2020) |
| Event study | Schmidheiny-Siegloch (2023); 张子尧 (2022 JQTM); 黄炜 (2022 JQTM) |
| DiD standard errors | Bertrand-Duflo-Mullainathan (2004); Cameron-Gelbach-Miller (2008); MacKinnon-Webb (2017) |
| RD design | Hahn-Todd-Van der Klaauw (2001); Imbens-Lemieux (2008); Calonico-Cattaneo-Titiunik (2014); Cattaneo-Idrobo-Titiunik (2020 guide) |
| Shift-share IV | Goldsmith-Pinkham et al. (2020); Borusyak-Hull-Jaravel (2022) |
| Weak instruments | Staiger-Stock (1997); Stock-Yogo (2005); Andrews-Stock-Sun (2019) |
| Bunching | Saez (2010); Chetty et al. (2011); Kleven (2016 review) |
| Machine learning in econ | Chernozhukov et al. (2018) Double ML; Athey-Imbens (2019 review) |

---

## Reading quality signals

| Green flags | Red flags |
|------------|-----------|
| Motivating failure is demonstrated with a clear example | Failure mode only shown in contrived DGPs |
| New assumptions explicitly stated and compared to status quo | Assumptions buried or not compared |
| Simulation covers realistic sample sizes and DGPs | Simulations only show the best case for the new method |
| Software implementation provided | Method proposed with no implementation guidance |
| Guidance on when to use the new method (and when not to) | Paper claims new method always dominates |
| Empirical application changes substantive conclusion | "Robustness" application leaves all conclusions unchanged |

---

## Chinese methods papers

The Chinese econometrics literature has produced a genre of "methods introduction" papers that:
- Explain an international method to Chinese readers (e.g., 黄炜's event study guide)
- Provide Stata/R implementation code
- Apply the method to a Chinese dataset as illustration

These should be read primarily as **pedagogical resources**, not novel methodological contributions.
The key reading question is: *Is the exposition clear and accurate? Is the implementation guidance trustworthy?*
