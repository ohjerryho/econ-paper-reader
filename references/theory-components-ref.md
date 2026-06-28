---
name: epr-theoretical-components-ref
version: 0.1.0
author: ohjerryho
---

# Theory Model Components Reference

A reference guide for reading theoretical models in economics. Covers model primitives,
equilibrium concepts, common model architectures, and proof reading techniques.

Informed by the benchmark model library in pAI-Econ-claude (Chen Zhu, Xiaolu Wang, Weilong Zhang).

---

## Model primitives: a universal map

Every economic model, regardless of complexity, is built from these components:

### 1. Agents
- Who makes decisions? (consumers, firms, workers, government, planner, intermediaries)
- How many? (finite set {1...N}, continuum [0,1], representative agent)
- Are they identical (representative agent) or heterogeneous (indexed by type θ)?

### 2. Preferences / Objectives
- **Consumers**: Utility function U(c, l, ...) over consumption, leisure, etc.
- **Firms**: Profit function π = pq − c(q)
- **Workers**: Value function over wages, working conditions, job match
- **Planner**: Social welfare function (utilitarian = sum of utilities, Rawlsian = min utility)
- **Time preferences**: Discount factor β ∈ (0,1) in dynamic models

### 3. Technology / Production
- Production function F(K, L, ...) — typically CRS (constant returns to scale) in competitive models
- Matching function M(u, v) in search models
- Information technology: signal precision σ², Bayesian updating

### 4. Endowments / Resources
- Initial wealth w_0, time endowment T
- Human capital h, skills θ (often drawn from distribution F(θ))
- In general equilibrium: factor endowments L̄, K̄

### 5. Information structure
- **Full information**: All agents observe all relevant variables
- **Private information**: Agents observe their own type θ; others don't (adverse selection)
- **Moral hazard**: Actions unobservable; outcomes observed
- **Rational expectations**: Agents know the model; learn from equilibrium prices

### 6. Timing / Sequence of events
The timing section defines causality within the model. Read it carefully.
Example: "(1) Nature draws θ. (2) Principal offers contract. (3) Agent accepts/rejects.
(4) Agent chooses effort. (5) Output realized. (6) Wages paid."

---

## Equilibrium concepts

| Concept | Description | Used in |
|---------|-------------|---------|
| **Competitive equilibrium** | Prices clear markets; agents are price-takers | Macro, trade, partial equilibrium |
| **Nash equilibrium** | Each player plays best response to others' strategies | IO, game theory |
| **Subgame perfect NE (SPE)** | Nash equilibrium in every subgame; backward induction | Dynamic games |
| **Bayesian Nash equilibrium** | Nash with private information; update beliefs via Bayes | Auctions, contracting |
| **Perfect Bayesian equilibrium (PBE)** | SPE + consistent beliefs | Signaling, dynamic contracting |
| **Rational expectations equilibrium** | Agents' beliefs consistent with equilibrium outcomes | Finance, macro |
| **Stable matching** | No blocking pairs; no couple can jointly deviate | Labor markets, marriage |
| **Mechanism** | Designer sets rules to implement social objective | Taxation, auctions, regulation |

**Reading tip**: The equilibrium concept is a modeling *assumption*, not a result. Ask whether
it's appropriate for the agents and setting being described.

---

## Common model architectures

### Search and matching models (e.g., Mortensen-Pissarides)
- **Signature**: Matching function M(u,v); Beveridge curve; Nash wage bargaining
- **Key parameters**: Matching efficiency, workers' bargaining power η, job destruction rate δ
- **Equilibrium**: Free-entry condition pins down job creation; wage bargaining splits surplus
- **Benchmark papers**: Mortensen-Pissarides (1994), Diamond (1982)
- **Reading focus**: Is the matching function microfounded? What determines surplus division?

### Human capital models (e.g., Mincer, Becker)
- **Signature**: Returns to education, Ben-Porath investment model
- **Key parameters**: Rate of return to human capital, depreciation, complementarity with technology
- **Benchmark papers**: Becker (1964), Ben-Porath (1967), Mincer (1958)
- **Reading focus**: What determines the human capital investment decision? On-the-job vs. schooling?

### Principal-agent / contracting models
- **Signature**: Incentive compatibility (IC) constraint, participation (IR) constraint, optimal contract
- **Setup**: Principal maximizes profit subject to agent's IC and IR constraints
- **First best**: No information asymmetry → efficient allocation
- **Second best**: Private information → information rent, distorted effort/allocation
- **Benchmark papers**: Mirrlees (1971), Holmstrom (1979), Hart-Moore (1988)
- **Reading focus**: Which constraint binds? What's the distortion relative to first best?

### Dynamic programming models
- **Signature**: Bellman equation V(s) = max_{a} {u(s,a) + β E[V(s')]}
- **State variable** s: Sufficient statistic for future
- **Policy function**: a*(s) = argmax of Bellman
- **Solution**: Value function iteration, policy function iteration
- **Reading focus**: Is the state space tractable? What's being approximated?

### Mechanism design / optimal taxation
- **Signature**: Types θ ∈ Θ; revelation principle → direct mechanism; IC + IR constraints
- **Mirrlees optimal tax**: Type = productivity; instrument = income; information rent → marginal rate distortion
- **Reading focus**: What is the policy instrument? What is the social objective? Which constraints bind?

### General equilibrium (GE) models
- **Signature**: Market clearing conditions, Walras' law, existence via fixed point theorem
- **Key check**: Is GE actually needed, or would partial equilibrium be sufficient?
- **Reading focus**: What general equilibrium channels are quantitatively important? Is GE an improvement over PE in magnitude?

### IO models (imperfect competition)
- **BLP (Berry-Levinsohn-Pakes)**: Demand estimation with product differentiation and endogenous prices
- **Cournot / Bertrand**: Quantity vs. price competition
- **Signature**: First-order conditions from profit maximization; Nash-in-prices or -quantities
- **Reading focus**: What competition mode is assumed? Symmetric or asymmetric firms?

---

## Reading propositions and proofs

### Proposition structure
```
Proposition X: Under Assumptions A1 and A2, [result R] holds.
Proof: [see Appendix A / in text]
```

**Reading strategy**:
1. State A1 and A2 in plain English
2. State R in plain English
3. Ask: Is R surprising given A1 and A2? If obvious, why is it a proposition?
4. Ask: Which assumption is doing the most work?
5. Ask: What happens if A1 is relaxed?

### Common proof techniques

| Technique | When used | Reading tip |
|-----------|-----------|-------------|
| First-order conditions (FOC) | Optimization problems | Interior solution assumed — check boundary conditions |
| Envelope theorem | Derivatives with respect to parameters | Used in comparative statics — trace the effect of a parameter change |
| Implicit function theorem | Showing equilibrium exists and is differentiable | Conditions for Jacobian to be invertible at equilibrium |
| Contraction mapping / Banach fixed point | Existence and uniqueness | Verify the discount factor β < 1 or the contraction condition |
| Revealed preference | Choice-based arguments | No maximization assumed — weaker than utility-based |
| Proof by contradiction | Assume not-R → derive contradiction | Track the chain of inequalities carefully |
| Mathematical induction | Dynamic / recursive settings | Check base case and inductive step |

### Corollaries and remarks

- **Corollary**: A result that follows immediately from a proposition, usually a special case.
  Reading tip: Corollaries often contain the economic intuition more clearly than the main proposition.
- **Remark**: An interpretive comment — not a formal result. Read all remarks; they often
  contain the author's actual intuition.
- **Lemma**: A technical result used in proving the main proposition. Usually less economically
  interesting; skim unless you're verifying the proof.

---

## Comparative statics quick guide

Most theory papers deliver comparative statics: how equilibrium Y changes when parameter θ changes.

**Reading approach**:
1. Identify what moves: ∂Y/∂θ > 0? < 0? Non-monotone?
2. Identify the mechanism: through which channel does θ affect Y?
3. Does the result match economic intuition? If not, what's the subtle mechanism?
4. Is the result monotone everywhere, or only locally?
5. For welfare comparisons: is the planner's optimum the same direction as the equilibrium response?

**Non-monotone results** (often the most interesting): a higher θ increases Y up to a threshold,
then decreases it. Usually driven by competing effects (substitution vs. income; direct effect
vs. equilibrium response). Look for the exact threshold and its economic interpretation.
