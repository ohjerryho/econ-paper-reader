---
name: epr-theory
version: 0.1.0
author: ohjerryho
description: >
  Subskill for reading theoretical economics papers — formal models with assumptions,
  propositions, proofs, and comparative statics. Part of the econ-paper-reader skill set.
---

# epr-theory — Reading Theory Papers

Theoretical economics papers use mathematics to derive logical implications of assumptions
about economic behavior. The math is the language; the economic intuition is the content.
Reading theory well means extracting the intuition without getting lost in the notation.

## The structure of a theory paper

A theory paper typically follows this spine:

```
Economic question / puzzle
    ↓
Model environment (primitives)
    ↓
Equilibrium characterization
    ↓
Main results (propositions / theorems)
    ↓
Economic interpretation
    ↓
Extensions / comparative statics
    ↓
(Optional) Empirical implications or calibration
```

## Model primitives — what to identify

Every model has the same building blocks, even if the notation differs:

| Primitive | What to look for | Typical notation |
|-----------|-----------------|-----------------|
| **Agents** | Who makes decisions? (households, firms, workers, planner) | indexed by i, j, or continuous measure |
| **Preferences** | What do they maximize? | utility U(·), profit π(·), value function V(·) |
| **Technology** | Production or matching technology | F(K,L), matching function M(u,v) |
| **Endowments** | What are they endowed with? | wealth w, time T, skills θ |
| **Information** | What do agents observe? | private θ, public signal s, full information |
| **Timing** | In what order do things happen? | period-by-period or "stages" |
| **Prices / wages** | How are they determined? | competitive, Nash bargaining, posted |

Reading tip: Write these down as you read the model setup. This map is your guide through
the rest of the paper.

## Mandatory output block for theory and structural papers

When reading any theory or structural paper, the report **MUST** include a dedicated **模型设定 (Model Setup)** block placed immediately after the 研究设计 section (and after 实证设计 if it also exists). Use this exact structure:

```
### 模型设定

**核心方程**

[Reproduce ALL key model equations in LaTeX display math ($$...$$).
Include: objective functions, equilibrium conditions, key FOCs, law of motion, structural estimating equations.
Number equations if the paper does. Never paraphrase — show the actual equations.]

**符号说明**

| 符号 | 含义 | 约束 / 假设 | 作用 |
|------|------|------------|------|
| $\theta$ | [parameter name] | [domain, e.g., θ ∈ (0,1)] | [what it drives in the model] |
| $Y_t$ | [variable name] | [endogenous / exogenous] | [role in equilibrium] |

[Include every symbol appearing in the key equations above: parameters, state variables, choice variables, equilibrium objects.]

**⚠️ 关键假设与模型局限**

[List the assumptions that DRIVE the main results — the ones the conclusions would not hold without.
Also flag assumptions that seem strong or empirically questionable.
Examples: functional form restrictions (CES, Cobb-Douglas), market structure (perfect competition, monopoly), information assumptions (full information, rational expectations), exogeneity of certain parameters.]
```

## Equilibrium concept

The equilibrium concept defines what "solution" means. Common concepts:

| Concept | Papers that use it |
|---------|-------------------|
| **Competitive equilibrium** | Trade, growth, most macro models |
| **Nash equilibrium** | IO, game theory |
| **Subgame perfect NE** | Dynamic games, contracting |
| **Rational expectations equilibrium** | Finance, macro with uncertainty |
| **Stable matching** | Labor markets, marriage markets |
| **Mechanism / Planner's problem** | Optimal taxation, auction theory |

Reading tip: The equilibrium concept tells you what behavioral assumptions are embedded in
the model. Competitive equilibrium assumes price-taking; Nash assumes strategic interaction.
These are not neutral choices — they matter for what the model can and can't say.

## Reading propositions and theorems

A proposition/theorem is a logical statement of the form: *Under assumptions A1–Ak, result R holds.*

To read a proposition:
1. **Identify the assumptions** (often referenced as "A1", "Assumption 1", etc.)
2. **State the result in plain English** — What does R say, in words?
3. **Understand the mechanism** — *Why* does R follow from A1–Ak?
4. **Identify the binding constraint** — Which assumption is doing the heavy lifting?
5. **Ask what breaks R** — If you relax Ai, does R fail? The paper often tells you.

Reading proofs: You don't need to verify every proof step. Focus on the *proof strategy*:
- By contradiction? By construction? By induction?
- What lemma does the main result rest on?
- Is the proof in the appendix? (Read appendix proofs for main results if you're doing a deep read)

## Comparative statics

Comparative statics ask: *How does the equilibrium change when a parameter changes?*

These are usually stated as: "A higher θ leads to higher / lower / non-monotone Y."

Reading strategy:
1. Identify what is being varied (the parameter)
2. Identify what is being traced (the equilibrium outcome)
3. Understand the direction and (if stated) the magnitude
4. Connect to the economic mechanism: *Why* does Y move this way when θ increases?

Comparative statics are often the paper's main economic contribution. They generate
testable predictions for empirical work.

## Types of theory papers

### Pure theory

Only a model. No calibration, no empirics. Contribution is the set of propositions.
Reading focus: Are the assumptions reasonable? Are the results surprising? Is the
mechanism novel or is this a known result in new clothing?

### Theory + calibration

Estimates parameters using aggregate moments (not micro-identification). Then simulates
counterfactuals. Weaker identification than structural estimation, but tractable for
complex general-equilibrium models.
Reading focus: Are the calibrated parameters within the range of prior estimates?
How sensitive are the counterfactual results to the calibrated parameters?

**Mandatory calibration block** for theory+calibration and structural papers:

```
### 校准与参数设定 (Calibration)

**校准方法 (Calibration Method)**
[Describe the method: GMM / SMM / MLE / method of moments / direct targeting of data moments.
What data moments are matched? (e.g., labor share, trade elasticity, firm size distribution)]

**预设参数 (Preset Parameters)**

| 参数 | 含义 | 设定值 | 来源 / 依据 |
|------|------|--------|------------|
| $\beta$ | discount factor | 0.96 | standard in macro literature |
| $\sigma$ | elasticity of substitution | 4.0 | Broda & Weinstein (2006) |

[List every parameter taken from prior literature or set by assumption rather than estimated.
These are the "free" inputs to the model — sensitivity to them matters.]

**估计/校准结果 (Estimated Parameters)**

| 参数 | 含义 | 估计值 | 解读 |
|------|------|--------|------|
| $\theta$ | matching efficiency | 0.72 | implies X% of vacancies filled per quarter |

[For each estimated parameter: what does the value imply economically?
How does it compare to prior literature? Are there implausible values?]

**模型拟合 (Model Fit)**
[Does the model replicate the targeted moments? Any notable misfit?
Any non-targeted moments that the model matches or misses?]

**反事实分析 (Counterfactual)**
[What policy or shock is simulated? What do the counterfactual results show?
How sensitive are the counterfactual results to key calibrated parameters?]
```

### Theory with empirical application

The model generates predictions that are tested in a companion empirical section.
Reading focus: Does the model's prediction map cleanly to the empirical test?
Is the empirical test actually capable of rejecting the model?

## Common model types in economics

For detailed reference on specific model architectures → `references/theory-components-ref.md`

| Type | Signature features | Common papers |
|------|--------------------|--------------|
| Search & matching | UE/EU transition rates, matching function, bargaining | Labor, housing markets |
| Incomplete contracts | Non-verifiable actions/investments, hold-up problem | Firm boundaries, finance |
| Adverse selection / moral hazard | Private information, screening, principal-agent | Insurance, contracts |
| Dynamic programming | Bellman equation, value function iteration | Macro, IO |
| General equilibrium | Market-clearing, budget constraints bind, prices endogenous | Trade, macro |
| Mechanism design | Social planner, incentive compatibility, individual rationality | Taxation, auctions |
| Game theory / IO | Strategic interaction, best response functions | Industrial organization |

## Economic intuition extraction

The most valuable thing you can do when reading theory is extract the **economic mechanism**
in one paragraph — no math.

Template: *"The key insight is that when [condition], agents do [behavior A] rather than
[behavior B], because [incentive]. This leads to [equilibrium outcome], which means
[economic implication]."*

If you can't write this paragraph, you haven't fully understood the paper yet.

## Theory paper quality signals

| Green flags | Red flags |
|------------|-----------|
| Assumptions stated at the start of each section | Assumptions scattered or implicit |
| Economic intuition provided after each proposition | Results stated without interpretation |
| Special cases / limiting cases shown | Model only works in one parameterization |
| Robustness to relaxing key assumptions discussed | No sensitivity to assumptions |
| Connection to empirical evidence | "Stylized facts" loosely connected to model |
| Model nests prior literature as special case | Claims novelty without showing what's different |
