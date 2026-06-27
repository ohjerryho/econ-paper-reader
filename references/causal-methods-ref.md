---
name: epr-causal-methods-ref
version: 0.1.0
author: ohjerryho
---

# Causal Methods Quick Reference

Concise reference for the major identification strategies used in economics. Each entry:
key assumption, diagnostic tests to find in the paper, and common threats.

Distilled from Cunningham (2021) *Causal Inference: The Mixtape* and applied micro practice.

---

## OLS (Ordinary Least Squares)

**When it's causal**: Only when treatment is randomly assigned, or when selection on
observables is credibly satisfied.

**Key assumption**: E[ε|D, X] = 0 (no unobserved confounders conditional on X)

**Typical use**: Correlational baseline before an identification strategy; "kitchen sink"
robustness.

**Threats**: Omitted variable bias, reverse causality, measurement error in D.

**Diagnostic**: Adding more controls changes β materially → omitted variable concerns.

---

## Difference-in-Differences (DiD)

**Key assumption**: Parallel trends — absent treatment, treated units would have followed
the same trend as control units.

**Estimating equation**:
`Y = β(Post × Treat) + α_i + λ_t + X'γ + ε`

**Diagnostics**:
- Pre-treatment event study: β at t=−2, t=−3 should be ≈ 0
- Balance on pre-treatment observables
- Placebo test: Fake treatment date

**Staggered DiD**: Use robust estimators (CS, SA, or dCdH) — standard TWFE can produce
negative weights under heterogeneous treatment effects (Goodman-Bacon decomposition).

**Estimand**: ATT (average treatment effect on the treated)

**Common threats**:
- Anticipation effects (units change behavior before official treatment date)
- SUTVA violation (spillovers from treated to control)
- Pre-existing trend differences
- Collider / selection into treatment correlated with time trend

---

## Instrumental Variables (IV / 2SLS)

**Key assumptions**:
1. Relevance: Cov(Z, D) ≠ 0 — tested by F-statistic in first stage (threshold: F > 10 or F > 20)
2. Exclusion: Z → Y only through D — economic argument required, not testable
3. Independence: Z ⊥ potential outcomes (conditional on X)

**2SLS procedure**:
- Stage 1: D̂ = π_0 + π_1 Z + X'π + v
- Stage 2: Y = β D̂ + X'γ + ε

**Diagnostics**:
- First-stage F-statistic (in table or in text)
- Anderson-Rubin test (robust to weak instruments)
- Over-identification test if multiple instruments (J-statistic, though exclusion for each instrument is still a judgment call)
- Reduced form: Is Z directly predictive of Y? Direction consistent with β × π̂?

**Estimand**: LATE for the complier subpopulation (units moved by Z from D=0 to D=1).

**Common threats**:
- Weak instrument (F < 10): Inflated CIs, potential bias toward OLS
- Exclusion restriction violated (Z → Y directly)
- Z correlated with other treatments (instrument contamination)
- Non-monotone first stage (defiers)

---

## Regression Discontinuity (RD)

**Sharp RD**: D = 1[X ≥ c]
**Fuzzy RD**: P(D=1 | X) jumps at c — use as IV

**Key assumption**: Continuity of E[Y(0)|X] and E[Y(1)|X] at the cutoff c. Equivalently:
no manipulation of X around c.

**Diagnostics**:
- McCrary (2008) / Cattaneo-Jansson-Ma density test: No spike in density of X at c
- Covariate balance: Pre-determined covariates smooth through c
- Placebo cutoffs: No discontinuity at other values of X
- Donut RD: Excluding observations very close to c (tests for bunching/manipulation)
- Bandwidth sensitivity: Results stable across CCT optimal, half, and double bandwidth

**Estimation**: Local linear regression (preferred over global polynomial). CCT data-driven bandwidth (Calonico-Cattaneo-Titiunik).

**Estimand**: LATE at the cutoff — local effect, may not generalize.

**Common threats**:
- Manipulation of X to be just above/below cutoff
- Discrete running variable (imprecise specification)
- Very small samples near cutoff
- Functional form misspecification (bandwidth too wide, polynomial too high)

---

## Synthetic Control

**Key assumption**: The weighted combination of control units (donor pool) provides a good
counterfactual for the treated unit.

**Diagnostics**:
- Pre-treatment RMSPE (root mean square prediction error): How well does SC fit pre-treatment?
- Permutation / in-space placebo: Run SC for all control units; treated unit should produce
  a larger post-treatment gap than most control units
- Leave-one-out: Results robust to removing one donor unit?
- In-time placebo: No effect when fake treatment date is used

**When to use**: Single treated unit (a country, a state, a firm); enough pre-periods to
construct a good match.

**Common threats**:
- Poor pre-treatment fit
- Few donor units
- Extrapolation (treated unit requires weights outside [0,1])

---

## Matching / PSM

**Key assumption**: Selection on observables — conditional on X, treatment is as-good-as-random.

**Reading note**: This assumption is strong and generally untestable. PSM is best viewed as
a robustness check, not a primary identification strategy. If PSM is the only claim to
causality, be skeptical.

**Diagnostics**:
- Common support: Trimming proportion
- Post-matching balance: Standardized mean differences < 0.1 for key covariates
- Sensitivity analysis (Rosenbaum bounds)

**Common threats**:
- Unobservable confounders (the assumption literally says this isn't a problem, but we can't verify)
- Propensity score model misspecification
- Lack of common support in high dimensions

---

## Shift-Share / Bartik

**The instrument**: Z_l = Σ_k s_{lk} * g_k
where s_{lk} = local industry k's initial share in location l
and g_k = national (leave-one-out) growth of industry k

**Two valid identification approaches**:
1. **Borusyak et al. (2022)**: Exogeneity of shocks g_k (conditional on shares as controls)
2. **Goldsmith-Pinkham et al. (2020)**: Exogeneity of initial shares s_{lk} (each industry instruments separately)

**Key diagnostics**:
- Rotemberg weights: Which industry k dominates identification? Is that industry's shock plausible?
- Pre-trend test: Bartik instrument uncorrelated with pre-period outcomes
- Overidentification across industries (GPG approach)

**Common threats**:
- National shock g_k is endogenous to local conditions (if local economy is large)
- Initial shares correlated with local time trends
- Few dominant industries carry all the identification weight

---

## RCT / Field Experiments

**When it's causal**: Treatment is randomly assigned → selection bias = 0 by design.

**Still check**:
- Balance table: Are treatment and control groups similar on observables?
- Attrition: Is dropout differential? (ITT vs. LATE distinction)
- SUTVA: Spillovers between treatment and control arms
- Compliance: Perfect vs. imperfect; use randomization as IV for intent-to-treat
- External validity: LATE (effect on compliers) ≠ ATE; specific context may not generalize

---

## Bunching Estimators

**Design**: Exploit the clustering of agents at a kink or notch in a budget set
(e.g., a tax threshold, income cutoff, regulatory threshold).

**Key papers**: Saez (2010), Chetty et al. (2011), Kleven & Waseem (2013).

**What to look for**:
- Distribution of the running variable showing excess mass at the notch/kink
- Counterfactual distribution (smooth polynomial fit away from notch)
- Elasticity estimate derived from bunching mass

**Common threats**: Optimization frictions (bunching may understate elasticity), manipulation
at the notch for other reasons.

---

## Local Projections (Jordà 2005)

**Design**: Estimate impulse response functions by regressing future outcomes on current shocks.

**Versus VARs**: More robust to misspecification; can handle non-linear responses.

**What to look for**:
- Identification of the shock (is it truly exogenous?)
- Horizon length (how many periods ahead are plotted?)
- Confidence bands that account for serial correlation

---

## Key concepts cheat sheet

| Term | Meaning |
|------|---------|
| ATE | Average treatment effect (over full population) |
| ATT | Average treatment effect on the treated |
| LATE | Local average treatment effect (for compliers) |
| ITT | Intent-to-treat (effect of assignment, not receipt) |
| SUTVA | Stable unit treatment value assumption (no spillovers, no multiple versions of treatment) |
| Compliers | Units induced to take treatment by the instrument |
| Never-takers | Units who never take treatment regardless of instrument |
| Always-takers | Units who always take treatment regardless of instrument |
