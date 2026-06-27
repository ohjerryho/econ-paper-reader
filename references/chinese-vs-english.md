---
name: epr-chinese-vs-english
version: 0.1.0
author: ohjerryho
---

# Chinese vs. English Economics Paper Conventions

Economics papers in Chinese and English top journals differ substantially in style, structure,
expectations, and institutional context. This reference helps calibrate reading expectations
when switching between the two.

---

## Structural differences

| Section | English top journal | Chinese CSSCI / top Chinese journal |
|---------|--------------------|------------------------------------|
| **Abstract** | Dense: question + method + result + contribution (150–250 words) | Often looser; may lack quantitative results; sometimes just summarizes sections |
| **Introduction** | Self-contained map of the whole paper; contribution stated explicitly | May be shorter; motivation often institutional/policy-driven; less explicit on "what's new" |
| **Literature review** | Often woven into intro; very selective (10–30 citations) | Usually a standalone 文献综述 section; more comprehensive citation coverage |
| **Data** | Detailed construction notes; precise sample restrictions; summary stats table | Often present but may be less detailed; admin data sources increasingly common in top Chinese journals |
| **Empirical strategy** | Always named explicitly; identifying assumption stated; formal testing | Methodology section present; DiD and IV increasingly common; older papers may rely on OLS |
| **Mechanism** | Increasingly required; must match theory prediction | Often lighter; sometimes replaced with heterogeneity analysis |
| **Policy implications** | Brief and cautious ("consistent with policies that...") | Often a standalone **政策建议** section; concrete recommendations expected |
| **Conclusion** | Summarizes, acknowledges limitations | May be shorter; policy emphasis stronger |

---

## Writing style differences

### English top-journal style
- **Precision over comprehensiveness**: Every claim must be defensible.
- **Contribution first**: Abstract and intro frontload the novel result.
- **Quantitative specificity**: "A 10% increase in X raises Y by 3.2%", not "significantly increases".
- **Active voice, present tense**: "This paper estimates...", "We find..."
- **Minimal hedging on main claims**: Qualifications in robustness, not in the abstract.
- **No flowery language**: Direct, functional prose.

### Chinese CSSCI style
- **Context and motivation emphasized**: Opening often surveys broader policy environment.
- **Contribution may be implicit**: Novelty framed as "filling a gap" in Chinese context rather than explicit "first to do X".
- **Institutional framing**: Often locates the paper within a policy reform, a Five-Year Plan, or a government initiative.
- **Comprehensive literature**: Exhaustive citation of domestic (Chinese-language) literature; less emphasis on positioning against international frontier.
- **Policy recommendation language**: More prescriptive ("建议政府应该..."); treats policy implications as a core deliverable.
- **Parallel structure in section headings**: Chinese papers often use numbered sections (一、二、三) with symmetrically structured subsections.

---

## Identification standards

This is the most important difference for critical reading.

| Standard | English top journal (AER/QJE/JPE/REStud) | Chinese top journal (经济研究/管理世界/世界经济) |
|----------|----------------------------------------|----------------------------------------------|
| **Minimum bar** | Near-experimental variation required; OLS rarely credible for causal claims | Correlational analysis with controls acceptable; DiD increasingly common |
| **Parallel trends test** | Required; event study with confidence intervals standard | Increasingly common in recent papers; may be skipped in older work |
| **IV exclusion** | Economic argument required; scrutinized by referees | Less rigorously scrutinized; sometimes mechanical IVs used |
| **Robustness** | Extensive (10–20 robustness tables common) | Moderate (3–5 robustness checks more typical) |
| **Data quality** | High; admin records, matched employer-employee | Improving; China Household Finance Survey, CFPS, NBS data increasingly used |

**Reading tip**: Apply different priors when reading Chinese vs. English papers. A claim that
would be rejected at AER may still be informative in a Chinese context if the data is unique
or the institutional setting is novel.

---

## Chinese institutional context: essential knowledge

Many Chinese economics papers are unintelligible without knowledge of key institutional
features. These appear constantly:

| Institution / Policy | What it is | Why it matters for empirics |
|--------------------|-----------|---------------------------|
| **户籍制度 (Hukou)** | Residence registration system; restricts migrants' access to local public services | Creates sharp urban/rural divide; used in DiD (hukou reform dates) and RD (eligibility cutoffs) |
| **高考 (Gaokao)** | National college entrance exam; score-based cutoff for university admission | Used in RD designs for returns to college education |
| **国有企业 (SOE) 改革** | State-owned enterprise restructuring (1990s–2000s) | Source of mass layoffs; used as quasi-experimental variation in labor studies |
| **土地制度** | Dual urban/rural land ownership; collective land in rural areas | Key for housing market, migration, and agricultural productivity papers |
| **营改增 (VAT reform)** | Business-to-VAT transition (2012–2016), different industries staggered | Used in DiD for tax policy effects |
| **新农合 (NCMS)** | New Cooperative Medical Scheme for rural residents | Rollout variation used in DiD for health insurance effects |
| **高铁建设** | High-speed rail network expansion (post-2008) | Route assignment used as IV for transportation infrastructure effects |
| **房产税改革** | Property tax pilots in Shanghai and Chongqing (2011) | Used in DiD; only two treated cities limits power |
| **计划生育 (One-Child Policy)** | Fertility restriction; differential enforcement across counties and cohorts | Used in IV (sibling sex composition, policy intensity) for family size effects |

---

## Common patterns in Chinese empirical papers

### The "中国情境" (China context) framing
Many Chinese papers frame their contribution as "applying X methodology to China" or "testing
theory X in the Chinese context". Reading tip: Ask whether the China setting genuinely generates
novel insights (unique institutions, scale, policy variation) or whether the paper is simply
a replication in a new country.

### Policy evaluation papers
Very common in Chinese literature. Structure: describe policy → estimate effect with DiD/IV →
policy recommendation. Reading tip: Check whether the comparison group (did not receive policy)
is truly comparable and whether the policy rollout was as-good-as-random.

### Chinese administrative data
Increasingly available and high-quality: customs data, tax records, ASIF (Annual Survey of
Industrial Firms), NBS surveys. These datasets are powerful but have known issues:
- ASIF: Inconsistent coverage below threshold (above 5 million yuan); frequent firm ID
  changes; possible fabrication in early years (Brandt, Van Biesebroeck, Zhang 2012)
- Export data: Generally high quality; used heavily in Chinese trade literature

---

## Switching between the two languages: reading calibration

When switching from English to Chinese paper (or vice versa):

1. **Adjust identification expectations**: Chinese papers → correlation may be the point;
   English papers → causality claim is non-negotiable.

2. **Look for the policy hook**: Chinese papers almost always have one; it's not a weakness —
   it's a genre convention.

3. **Literature context**: A Chinese paper may cite primarily domestic literature in its
   literature review and position against international literature only briefly. This doesn't
   mean the authors are ignorant of the international frontier — it's an audience convention.

4. **Data uniqueness**: A Chinese paper using confidential Chinese administrative data may
   have a comparative advantage that partially compensates for weaker identification.

5. **Translation of contribution**: When evaluating a Chinese paper for international
   journals, ask: Is the institutional contribution also economically interesting beyond China?
   Does the mechanism operate through forces that would apply in other contexts?
