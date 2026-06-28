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

When reading any reduced-form paper, the report **MUST** include a dedicated **实证设计 (Empirical Design)** block placed immediately after the 研究设计 section. Every sub-section below is **structured output** — use tables and formatted blocks, never unstructured prose dumps.

```
### 实证设计

**基准回归方程 (Baseline Regression)**

[Reproduce the main estimating equation(s) in LaTeX display math ($$...$$).
Number equations if the paper does. Never paraphrase — show the actual equation.]

**固定效应与标准误 (Fixed Effects & Standard Errors)**

| 固定效应 | 吸收的变异来源 | 选择理由 |
|---------|-------------|---------|
| 个体固定效应 $\alpha_i$ | 个体间不随时间变化的特征 | [Why: e.g., 控制企业不可观测的固有异质性] |
| 年份固定效应 $\lambda_t$ | 宏观共同时间趋势 | [Why: e.g., 排除全国性政策冲击和经济周期] |
| [other FE] | [variation absorbed] | [identification reason] |

标准误聚类：[level] — [why this level matches treatment assignment]

**变量说明 (Variable Definitions)**

| 变量 | 含义 | 构造方式 | 选择动机 |
|------|------|----------|----------|
| $Y_{it}$ | [outcome] | [source + computation] | [why this operationalization] |
| $D_{it}$ | [treatment] | [assignment or measurement] | [why] |
| $X_{it}$ | [controls] | [how computed] | [why included / what omitted variable they address] |

[Log vs. level matters — state it. Include every variable and instrument.]

---

**稳健性与内生性处理 (Robustness & Endogeneity)**

| 检验类型 | 具体做法 | 结论 |
|---------|---------|------|
| 替代规格 | [alternative controls / sample / window] | [robust / sensitive] |
| 安慰剂检验 | [placebo treatment or outcome] | [passes / fails] |
| [other check] | [description] | [result] |

**IV 有效性** *(如使用IV，必填；否则略去)*

| 维度 | 内容 |
|------|------|
| 工具变量 | [name and description of IV] |
| 相关性（Relevance）| [first-stage F-stat or correlation; what the IV predicts and why] |
| 外生性（Exclusion Restriction）| [author's argument for why IV affects Y only through D; any indirect channel concerns] |
| 弱工具检验 | [F ≥ 10? Kleibergen-Paap or Cragg-Donald stat] |

---

**机制分析 (Mechanism Analysis)** *(如有；否则略去)*

[For each hypothesized mechanism:]

**机制 [N]：[mechanism name]**

逻辑：[How does this channel work? What is the intermediate variable M between D and Y?]

$$[机制回归方程，如 M_{it} = \gamma D_{it} + ... 或中介效应设定]$$

| 变量 | 含义 | 构造方式 |
|------|------|----------|
| $M_{it}$ | [mechanism variable] | [how constructed — be specific] |

结果：[coefficient on D in mechanism regression; what it implies about the channel]
结论：[confirmed / ruled out / partially supported]

---

**异质性分析 (Heterogeneity Analysis)** *(如有；否则略去)*

分析维度：[e.g., 地区/行业/规模/时间段]
分组方法：[interaction terms / subgroup regressions / quantile]

| 分组 / 条件 | 核心系数 | 与基准结果的关系 | 含义 |
|-----------|---------|---------------|------|
| [group A] | [β_A (SE)] | [larger/smaller/opposite] | [what this implies about the mechanism or heterogeneity source] |
| [group B] | [β_B (SE)] | [...] | [...] |

核心发现：[What does the heterogeneity pattern tell us? How does it support or complicate the main story?]

---

**进一步分析 (Further Analysis)** *(如有；否则略去)*

[For each additional analysis:]

**分析 [N]：[descriptive title]**

设计逻辑：[Why does the author do this? What additional question does it answer? How does it connect to the baseline?]
实证设定：[equation or method, concisely]
结果：[key finding]
与核心问题的联系：[how this extends, validates, or qualifies the baseline result]

---

**⚠️ 设计注意事项 (Design Flags)**

[Use ⚠️ for EACH flagged issue. Ground every point in specific evidence from the paper — no generic claims.

Two categories, clearly labeled:

**作者自认局限 (Author-acknowledged)**:
⚠️ [Quote or closely paraphrase what the paper itself says about limitations, caveats, or remaining concerns]

**读者独立识别 (Reader-identified)**:
⚠️ [Specific identification threat YOU see that the paper does not fully address — with reasoning]

Cover as relevant: exclusion restriction, anticipation effects, SUTVA, clustering adequacy, parallel trends plausibility, external validity, sample selection, specification sensitivity, publication bias in mechanism results.]
```

**Rule for 亮点 and 不足与疑问 sections** (applies globally, not just to empirical papers):

- **亮点**: Anchor every point to specific features of THIS paper — a particular identification design choice, a novel dataset, an elegant theoretical insight, a surprising finding. Cite specific sections, tables, or methods. Do not use generic phrases like "identification is clean" without saying exactly what makes it clean.
- **不足与疑问**: Start with what the paper explicitly acknowledges as its own limitations (cite section or footnote if possible). Then add reader-identified concerns — but each must be a specific, reasoned argument, not a checklist item. A concern is only worth writing if you can say WHY it matters for THIS paper's specific claims.

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
