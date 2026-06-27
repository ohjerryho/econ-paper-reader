---
name: epr-tables-figures
version: 0.1.0
author: ohjerryho
description: >
  Subskill for interpreting tables and figures in economics papers — regression tables,
  event study plots, RD plots, model fit tables, and standard graphical outputs.
  Part of the econ-paper-reader skill set.
---

# epr-tables-figures — Reading Tables and Figures

Tables and figures in economics papers encode the empirical evidence. Knowing their anatomy
lets you extract the evidence efficiently and critically.

---

## Regression tables

The standard workhorse of empirical economics. Anatomy of a typical regression table:

```
                    (1)        (2)        (3)
Outcome variable:   Y          Y          Y

Treatment (D)      0.234**    0.198**    0.201**
                  (0.089)    (0.082)    (0.085)

Controls              N          Y          Y
FE: Industry          N          N          Y
Observations       5,420      5,420      4,891
R-squared          0.12       0.31       0.44
Clusters            342        342        289
```

**What each element tells you:**

| Element | What it means | What to ask |
|---------|--------------|-------------|
| Point estimate (0.234) | Effect of D on Y in the units of Y | What's the economic magnitude? |
| Standard error (0.089) | Precision of estimate | Clustered at what level? Should match treatment level |
| Stars (**, *) | Statistical significance | Is the result robust, or just barely significant? |
| N changes across columns | Sample changes when FE added | Why? Selection concern? |
| R² | Fraction of variance explained | Low R² is fine — variation in Y is expected |
| Cluster count | How many independent groups | Fewer than ~30 clusters → SE unreliable |

**Reading sequence:**
1. Read the column headers first — what's the outcome, what specification?
2. Column (1) is usually the baseline. Focus here first.
3. Moving right: are controls being added? Does β change materially? (If β drops a lot when controls are added, suggests omitted variable bias.)
4. Compare last column to first column: How much do results change with full specification?
5. Check the N: Does it drop? If so, why?

**Significance conventions in economics:**
- *** p < 0.01, ** p < 0.05, * p < 0.10 (most common)
- Some papers report 95% confidence intervals rather than stars
- "Marginally significant" (p < 0.10) requires more scrutiny — especially for headline results

**Computing economic magnitude (essential):**

From summary statistics + coefficient:
- If Y is log-transformed: coefficient ≈ % change in Y per unit change in D
- If D is binary and Y is continuous: coefficient = mean difference in Y
- Effect size relative to baseline: β / mean(Y)
- If both Y and D are in logs: coefficient = elasticity

---

## Balance / summary statistics tables

Usually Table 1. Shows pre-treatment characteristics or descriptive statistics.

**What to check:**
- Control vs. treated group means: Are they similar? (Randomization balance)
- Standard deviations: Do they give a sense of variation?
- P-values on treatment-control differences: Should be large (no significant differences) for balanced designs
- Variable definitions: Sometimes the only place variable names are defined

---

## Event study plots

Shows treatment effects across time relative to event date. X-axis: periods relative to
treatment (−3, −2, −1, 0, 1, 2, 3...). Y-axis: estimated DiD coefficient for each period.

**Reading an event study plot:**

```
β
|          ●——●
|     ●——●/
|  ●——●/
|—●——●————————————  (baseline, normalized to 0 at t=-1)
|       ↑
|    treatment
0  -3  -2  -1  0  +1  +2  +3    time
```

**What to look for:**
1. **Pre-trends**: Coefficients before t=0 should be statistically and economically close to zero. If they're trending, parallel trends assumption is violated.
2. **Event date jump**: Sharp discontinuity at t=0 or t=1.
3. **Persistence**: Does the effect persist or fade? Important for mechanism.
4. **Confidence intervals**: Should be shown. Wide CIs in pre-period can mask pre-trends.
5. **Omitted period**: Typically t=−1. This is the normalization — its coefficient is zero by construction, not evidence.

**Red flags:**
- Pre-trend visually upward/downward before treatment (claimed to be "noise")
- No confidence intervals shown
- Only post-treatment periods plotted (hiding pre-trend)
- Results driven by one or two periods

---

## RD (Regression Discontinuity) plots

Shows the relationship between the running variable X and the outcome Y, with a discontinuity
at the cutoff.

**Reading an RD plot:**
1. **Visual jump at the cutoff**: Is there a clear discontinuity? How large?
2. **Scatter vs. binned averages**: Good RD plots show binned means (not raw data) to visualize the jump cleanly.
3. **Functional form**: What polynomial fits on each side? Linear? Quadratic? Local linear is preferred.
4. **Bandwidth**: How wide is the window around the cutoff? Narrower = more credible but less precise.
5. **Density plot** (companion to main plot): Should show no spike in density at the cutoff (no manipulation).

---

## Heterogeneity / subgroup tables

Shows treatment effects for different subgroups (by gender, income quintile, region, etc.).

**What to look for:**
- Do subgroup effects line up with theoretical predictions? (A priori heterogeneity is more convincing than data-mining)
- Are the subgroup estimates significantly *different from each other*, not just from zero? (Need an interaction test)
- How many subgroups? (More subgroups → multiple testing concern)

---

## Model fit tables (structural papers)

Shows data moments vs. model-predicted moments (e.g., "Table 3: Data and Model Moments").

**What to look for:**
- Which moments are targeted (used in estimation) vs. untargeted (out-of-sample)?
- Model fit on untargeted moments is much more convincing
- Large misfit on certain moments → which assumptions drive those moments?

---

## Coefficient plots (dot-and-whisker plots)

Visualize multiple regression coefficients with confidence intervals. Used for heterogeneity
analysis or comparison across specifications.

**Reading:**
- Dot = point estimate, line = confidence interval (usually 95%)
- Does CI cross zero? (Statistical significance)
- Are estimates in the same direction and similar magnitude? (Consistency)
- Compare to reference category (if there is one)

---

## Common figure types and how to read them

| Figure type | Key questions |
|-------------|--------------|
| Event study plot | Pre-trends flat? Sharp change at t=0? |
| RD plot | Visual jump? Correct functional form? |
| CDF / distribution plots | Stochastic dominance? Which quantiles differ? |
| Binscatter | Non-linearities in the relationship? |
| Map | Geographic clustering? Selection into treatment by location? |
| Mechanism diagram / DAG | Is the proposed mechanism visually encoded? |

---

## Quick diagnosis: Does the figure support the claim?

For every key figure, ask:
1. What claim does the text make about this figure?
2. Does the figure actually support that claim, or just not contradict it?
3. Could a different interpretation of the same figure undermine the paper's argument?
