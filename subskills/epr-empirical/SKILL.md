---
name: epr-empirical
version: 0.1.0
author: ohjerryho
description: >
  Subskill for reading empirical economics papers, covering both reduced-form and structural
  estimation approaches. Part of the econ-paper-reader skill set.
---

# epr-empirical — Reading Empirical Economics Papers

Empirical economics papers make causal (or at minimum, correlational) claims supported by data.
There are two paradigms that require different reading strategies.

## The two empirical paradigms

### Reduced-form (RF) papers

The dominant paradigm in modern applied economics. Key features:
- Exploit **quasi-random variation** in a treatment variable
- Estimate effect using linear-in-parameters regression
- Identification strategy usually named explicitly (DiD, IV, RDD, SC...)
- Results: regression coefficients with confidence intervals
- Goal: clean identification of one well-defined estimand

The reading question: *Is the variation truly exogenous?*

### Structural estimation papers

Estimate parameters of an explicitly specified economic model. Key features:
- Model primitives written out formally (utility function, production function, etc.)
- Equilibrium derived analytically
- Estimation: GMM, MLE, SMM, or Bayesian methods
- Results: structural parameters + counterfactual simulations
- Goal: estimate parameters that are policy-invariant (Lucas critique proof)

The reading question: *Do the model assumptions and the identification strategy jointly justify
the structural parameters?*

---

## Mandatory output block for reduced-form papers

When reading any reduced-form paper, the report **MUST** include a dedicated **实证设计 (Empirical Design)** block placed immediately after the 研究设计 section. This block is the heart of the report for empirical papers — give it full depth. Use this exact structure:

```
### 实证设计

**基准回归方程 (Baseline Regression)**

[Reproduce the main estimating equation(s) in LaTeX display math ($$...$$).
Number equations if the paper does. Never paraphrase — show the actual equation.]

固定效应（Fixed Effects）：[list all FE included, e.g., 个体固定效应 + 年份固定效应]
标准误聚类（Clustering）：[level at which SE are clustered, e.g., 企业层面 / 县级 / 个人层面]

**变量说明 (Variable Definitions)**

| 变量 | 含义 | 构造方式 | 选择动机 |
|------|------|----------|----------|
| $Y_{it}$ | [outcome: what it measures] | [data source + computation] | [why this outcome] |
| $D_{it}$ | [treatment] | [how assigned or measured] | [why this operationalization] |
| $X_{it}$ | [key controls] | [how computed] | [why included] |
| $\alpha_i$, $\lambda_t$ | [fixed effects] | [unit/time dimension] | [variation absorbed] |

[Include every variable and instrument. Log vs. level matters — state it explicitly.]

**稳健性与内生性处理 (Robustness & Endogeneity)**

[Describe ALL robustness checks and endogeneity solutions the paper reports:
- Alternative specifications (different controls, samples, time windows)
- Placebo tests (fake treatments, pre-period outcomes)
- Addressing endogeneity: IV strategy, matching, PSM, synthetic control robustness
- Inference concerns: alternative clustering levels, wild bootstrap
State WHAT was done and WHAT the result shows (robust / partially robust / sensitive).]

**机制分析 (Mechanism Analysis)** *(if present; skip if absent)*

[If the paper conducts mechanism analysis:
- What mechanisms does the author hypothesize?
- What is the empirical strategy to test each mechanism? (mediation, subgroup, auxiliary outcome)
- What do the results show — which mechanism is confirmed, which is ruled out?
This section is common in Chinese-language empirical papers; less universal in top English journals.]

**异质性分析 (Heterogeneity Analysis)** *(if present; skip if absent)*

[If the paper conducts heterogeneity analysis:
- What dimensions of heterogeneity are examined? (industry, region, firm size, time period, etc.)
- How is heterogeneity identified? (interaction terms, subgroup regressions)
- What is the main pattern in the heterogeneous treatment effects?]

**进一步分析 (Further Analysis)** *(if present; skip if absent)*

[Any additional analyses beyond the baseline: welfare calculations, back-of-envelope cost-benefit,
general equilibrium exercises, policy simulation using estimated parameters, etc.]

**⚠️ 设计注意事项 (Design Flags)**

[Use ⚠️ for each flagged issue. Include BOTH:
(a) issues the authors themselves explicitly acknowledge
(b) issues you identify as a critical reader

Cover: exclusion restriction, anticipation, SUTVA, clustering level adequacy,
parallel trends plausibility, external validity, sample selection, specification sensitivity.]
```

---

## Reading a reduced-form paper

### The estimating equation

Look for the main regression equation, usually displayed prominently:

```
Y_{it} = β * D_{it} + X'_{it}γ + α_i + λ_t + ε_{it}
```

Identify:
- **Y**: What is the outcome variable? (Level, log, growth rate?)
- **D**: What is the treatment? (Binary, continuous, intensity?)
- **β**: This is the coefficient of interest. Its economic meaning is your priority.
- **X**: What controls are included? Why?
- **α_i, λ_t**: Fixed effects. What variation do they absorb?
- **ε**: Standard errors clustered at what level? (Should match treatment assignment level.)

### Identification section

This is the core of the paper. Ask:
1. What is the source of variation in D?
2. Why should this variation be uncorrelated with ε (the identifying assumption)?
3. What would make the assumption fail? (Confounders, anticipation, spillovers)
4. Does the paper test the assumption where testable? (Pre-trends, balance tests, placebo)

Load `epr-causal-inference` for method-specific guidance (DiD, IV, RDD, etc.).

### Results table reading

Each column in a results table is a specification. Read them as a sequence:
- Column 1: Baseline result (usually no controls or minimal controls)
- Subsequent columns: Adding controls, fixed effects, alternative samples
- Watch for: Does β change a lot when controls are added? (Suggests potential confounding)
- Watch for: Does SE cluster level change? (Affects inference)

The point of multiple columns is to show the result is **not an artifact** of one specific
specification. If the coefficient varies dramatically across columns, that's a concern.

### Economic magnitude

A statistically significant coefficient means nothing without economic interpretation.
Always compute: *What does this coefficient mean in real-world units?*

Examples:
- "A 10% increase in X raises Y by β × 10 percentage points" (log-linear)
- "Moving from control to treatment changes Y by β, which is β/mean(Y) × 100% of the baseline mean"
- Compare to: policy cost, prior literature magnitudes, descriptive variation in Y

If the paper doesn't provide this interpretation in the text, compute it yourself from the
summary statistics and the coefficient estimate.

### Robustness checks to look for

| Threat | Robustness check |
|--------|----------------|
| Selection into treatment | Balance table, pre-treatment trends |
| Concurrent events | Placebo treatments, event-by-event results |
| Sample restrictions | Alternative sample definitions |
| Functional form | Non-parametric specifications |
| Spillovers | Donut RD, excluding adjacent areas |
| Mismeasurement | Alternative variable definitions |

---

## Reading a structural paper

Structural papers are harder to read because you need to understand both the model and the
estimation strategy simultaneously.

### Model setup

Read the model section to identify:
1. **Who are the agents?** (consumers, firms, workers, governments)
2. **What do they maximize?** (utility function, profit function — written out explicitly)
3. **What are the constraints?** (budget, technology, information)
4. **What is the equilibrium concept?** (competitive, Nash, mechanism, social optimum)
5. **What are the key parameters?** (usually Greek letters — σ, η, β, γ — that the paper will estimate)

### Equilibrium and first-order conditions

The model is "solved" by deriving equilibrium conditions (usually first-order conditions or
fixed-point equations). These become the **estimating equations** in structural work.

Look for: "In equilibrium, the following condition holds..." followed by an equation that
relates observables to structural parameters.

### Identification in structural models

Structural identification is about whether the model parameters are uniquely determined by
the data moments. Questions to ask:
- What moments in the data identify which parameters?
- Is there a clear mapping from parameters to observable predictions?
- Would a different model (with different assumptions) fit the same data equally well?

### Counterfactual analysis

The payoff of structural estimation: you can ask "what if?" The model allows simulation
of policy changes that never happened.

Reading checklist:
- Is the counterfactual policy change well-defined in the model?
- Are the counterfactual results sensitive to specific parameter values?
- Does the paper report confidence intervals on the counterfactual?

### Model fit

A well-written structural paper shows the model fits the data it wasn't estimated on (out-of-sample).
Look for moments tables: "Data moments vs. model-predicted moments."

---

## Mixed papers: theory + empirics

Many serious papers use a simplified model to:
1. **Derive testable predictions** → then test them with RF methods
2. **Provide sufficient statistics** → express welfare in terms of estimable elasticities
3. **Motivate the structural form** of a regression equation

Reading strategy: Ask whether the theory and empirics actually connect.
- Does the model generate a specific prediction that the empirics test?
- Or are the theory and empirics two separate arguments that happen to reach the same conclusion?
- Is the model's key parameter actually estimated? Or is it just illustrative?
