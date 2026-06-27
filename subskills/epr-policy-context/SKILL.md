---
name: epr-policy-context
version: 0.1.0
author: ohjerryho
description: >
  Extract and organize policy information from economics papers. Captures the policy or
  event being studied, its institutional context, and — for Chinese-language or China-focused
  papers — the broader political and regulatory background (key speeches, party meetings,
  important economic documents). Always load for empirical and mixed papers; skip for
  pure theory or pure methodology papers with no policy content.
---

# epr-policy-context — 政策与背景提取

Economics papers frequently study the effects of real-world events and policies. This subskill
systematically extracts that policy information so readers can quickly grasp what happened,
when, and in what institutional context — without reading the entire paper.

## When to load

Load this subskill for:
- Empirical papers where a policy, regulation, reform, or event is the main shock
- Papers that use policy variation as an instrument
- Any paper that discusses Chinese government policies, plans, or directives
- Papers where institutional context is necessary to understand the identification strategy

Skip for: pure theory papers, pure methods papers, and papers with no real-world event content.

## Required output block: 政策与背景

Place this section **immediately after 一句话总结** in the reading report.

```
### 政策与背景

**核心政策 / 事件**

| 名称 | 时间 | 发布方 / 级别 | 主要内容 | 在文中的作用 |
|------|------|--------------|---------|------------|
| [policy name] | [year or date range] | [ministry / state council / local gov / etc.] | [what it does in 1–2 sentences] | [treatment shock / instrument / background / motivation] |

[Add one row per distinct policy or event. If the paper studies multiple reforms or a policy sequence, list each.]

**政治与制度背景** *(中文文献或涉及中国政策的文献必填；其他文献有重要制度背景时填写)*

[Describe the broader political and institutional setting the reader needs to understand the paper.
For Chinese papers, include as applicable:
- Party Congress / Plenary Session decisions directly relevant to the policy (e.g., 十八届三中全会)
- Key leadership speeches or directives that motivated the policy (e.g., 习近平关于XX的重要论述)
- Five-Year Plan targets or industrial policy documents (e.g., 中国制造2025、十四五规划)
- Regulatory milestones or landmark laws (e.g., 劳动合同法2008、增值税改革)

Write in plain prose. Be concise but specific — include the document name, year, and why it matters
for understanding this paper. Do not invent documents; only include what appears in the paper.]
```

## Extraction guidelines

**What counts as a "policy or event"**:
- Laws, regulations, reforms (e.g., minimum wage increases, trade liberalization)
- Administrative policies (e.g., hukou reform, one-child policy relaxation)
- Infrastructure or investment programs (e.g., high-speed rail expansion, broadband rollout)
- Natural experiments tied to institutional rules (e.g., age cutoffs, geographic boundaries)
- Financial events (e.g., exchange rate reforms, capital account opening)
- Trade policy changes (e.g., WTO accession, tariff reductions)

**Role in the paper** (pick the most accurate):
- `主要冲击` — the policy IS the treatment variable
- `工具变量` — policy variation is used as an instrument for an endogenous variable
- `外生分组依据` — policy assigns units to treatment/control groups
- `背景与动机` — policy motivates the research question but is not directly estimated
- `机制渠道` — policy is one of several mechanisms the paper investigates

**Critical rule**: Only include policies and documents that are explicitly mentioned in the paper.
Never add context from general knowledge unless it directly explains something the paper refers to.
