---
name: epr-causal-inference
version: 0.1.0
author: ohjerryho
description: >
  Subskill for reading causal inference sections in economics papers. Covers the major
  identification strategies (DiD, IV, RDD, SC, Matching, etc.) with reading guides for
  each. Part of the econ-paper-reader skill set.
---

# epr-causal-inference — Reading Causal Identification

The central challenge of empirical economics is establishing causality from observational data.
This subskill provides reading guides for the major identification strategies. For each
strategy, know: what variation is exploited, what assumption enables causality, and what
diagnostic tests should appear in the paper.

## The fundamental problem

The ideal experiment compares the same unit under treatment and control simultaneously — which
is impossible. Every identification strategy is an attempt to construct a credible counterfactual.

The key assumption in all non-experimental designs: *the untreated units tell us what the
treated units would have looked like in the absence of treatment.*

---

## 1. Difference-in-Differences (DiD)

**The design**: Compare treated and control units before and after treatment.

**Key assumption**: **Parallel trends** — in the absence of treatment, treated and control
units would have followed the same trend.

**What to look for in the paper:**
- Pre-treatment parallel trends test (event study plot — see `epr-tables-figures`)
- Choice of control group: Is it plausible they share the same trend?
- Anticipation effects: Did treated units change behavior before treatment?
- Spillovers: Did treatment affect the control group?

**Red flags:**
- No pre-trend test
- Pre-trends shown but visually non-parallel, dismissed without formal test
- Control group chosen post-hoc from many possible controls
- Single post-period result without dynamic effects

**Staggered DiD (increasingly common):**
Treatment rollout at different times for different units. Key concern: heterogeneous
treatment effects can cause the two-way FE estimator to be a weighted average with negative
weights (Goodman-Bacon decomposition). Look for whether the paper uses robust estimators
(Callaway-Sant'Anna, Sun-Abraham, de Chaisemartin-D'Haultfoeuille, or similar).

---

## 2. Instrumental Variables (IV / 2SLS)

**The design**: Use instrument Z to isolate exogenous variation in treatment D.

**Key assumptions:**
1. **Relevance**: Z affects D (testable — F-statistic in first stage, rule of thumb F > 10)
2. **Exclusion**: Z affects Y *only through* D (not directly testable — requires economic argument)
3. **Independence**: Z is as good as randomly assigned (conditional on controls)

**What to look for in the paper:**
- First-stage regression and F-statistic
- Economic argument for exclusion restriction (this is the most important thing to evaluate)
- LATE interpretation: IV estimates effect only for *compliers* (those induced by Z)
- Over-identification tests if multiple instruments (Sargan-Hansen J-statistic)

**Red flags:**
- Weak instrument (F < 10, or even F < 20 for conservative standards)
- Exclusion restriction justified only by intuition, no formal argument
- Instrument itself plausibly affects outcome directly
- No acknowledgment of LATE interpretation when treatment is heterogeneous

**Economic interpretation of LATE**: The IV estimate is the treatment effect for compliers —
units who take up treatment because of Z. If compliers differ from the full population, the
estimate may not generalize.

---

## 3. Regression Discontinuity (RD)

**The design**: Compare units just above and just below a cutoff in a running variable X.

**Types:**
- **Sharp RD**: Treatment is a deterministic function of crossing the cutoff (D = 1[X ≥ c])
- **Fuzzy RD**: Crossing the cutoff increases probability of treatment (use as IV)

**Key assumption**: **Continuity** — potential outcomes are continuous at the cutoff. No
manipulation of the running variable to be on one side.

**What to look for in the paper:**
- RD plot: Visual jump at the cutoff in both Y and D
- McCrary (2008) density test for manipulation of the running variable
- Bandwidth choice (local linear vs. polynomial, CCT optimal bandwidth)
- Placebo cutoffs: No discontinuity at other values of X
- Covariate balance at the cutoff: Pre-determined covariates should not jump

**Red flags:**
- No density test for manipulation
- Polynomial of degree > 2 globally fitted (should use local methods near cutoff)
- Results sensitive to bandwidth choice with no discussion
- Only a few dozen observations near the cutoff

**Interpretation**: RD estimates a local average treatment effect (LATE) at the cutoff.
Extrapolation beyond the cutoff requires additional assumptions.

---

## 4. Synthetic Control

**The design**: Construct a weighted average of control units to match the treated unit's
pre-treatment trajectory, then compare post-treatment.

**Key assumption**: The pre-treatment match is good enough to serve as counterfactual.

**What to look for in the paper:**
- Pre-treatment fit plot: How well does the synthetic control track the treated unit?
- Donor pool: What units are available as potential controls?
- Predictor variables used in matching
- Permutation / placebo inference (run SC for all control units — treated unit should stand out)

**Red flags:**
- Poor pre-treatment fit
- Few units in the donor pool
- Large weights on a single control unit
- Only one or two post-treatment periods

---

## 5. Event Study

Not a standalone identification strategy — it's a way to display DiD or IV estimates
dynamically, showing treatment effects in each time period before and after treatment.

**What to look for:**
- Flat / near-zero pre-treatment coefficients (pre-trend test)
- Sharp change at the event date (period 0 or 1)
- Whether confidence intervals are shown (not just point estimates)
- Omitted period (usually t = −1 as normalization)

See `epr-tables-figures` for detailed guidance on reading event study plots.

---

## 6. Matching / Propensity Score Matching (PSM)

**The design**: Match treated and control units on observable characteristics to construct a
comparable control group.

**Key assumption**: **Conditional independence** (selection on observables) — conditional on
observed X, treatment is as good as random.

**Reading concern**: This assumption is strong and untestable. PSM is best viewed as a
robustness check to OLS, not a primary identification strategy. If a paper's *only* claim to
causality is PSM, be skeptical.

**What to look for:**
- Common support: Distribution of propensity scores overlaps for treated and control
- Covariate balance after matching
- Trimming: What fraction of treated units are dropped due to lack of common support?

---

## 7. Shift-Share (Bartik) Instruments

**The design**: Instrument = national industry growth rates × local industry composition.
Local exposure to national shocks provides "exogenous" variation.

**Key assumptions (Borusyak et al. 2022 vs. Goldsmith-Pinkham et al. 2020):**
- Shift assumption: National industry shocks are exogenous (Borusyak-style)
- Share assumption: Initial industry shares are exogenous (Goldsmith-Pinkham-style)

**What to look for:**
- Which exogeneity assumption is being made? (Not always stated clearly)
- Rotemberg weights: Which industry/shock pair dominates? Are those shocks plausible?
- Placebo tests on the identifying shocks
- Overidentification test across industries/shocks

---

## 8. Randomized Controlled Trials (RCT) / Field Experiments

**The design**: Randomized treatment assignment eliminates selection bias by construction.

**Still need to check:**
- Balance table: Are control and treatment groups similar on pre-determined characteristics?
- Attrition: Is dropout from the sample differential by treatment?
- Compliance: Is there imperfect compliance? (Use IV with random assignment as instrument)
- Spillovers / SUTVA: Did control units interact with treated units?
- External validity: Does the sample / context generalize?

---

## General reading heuristic

When reading any identification section, ask these questions in order:

1. *What variation in the treatment variable is being exploited?*
2. *Why is that variation plausibly exogenous?*
3. *What would make the identifying assumption fail?*
4. *Does the paper test the assumption where testable?*
5. *What is the exact estimand — LATE, ATT, ATE? For whom?*
6. *How would the finding change if the key assumption were violated?*

For deep reference on specific methods → `references/causal-methods-ref.md`
