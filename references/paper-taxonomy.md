---
name: epr-paper-taxonomy
version: 0.1.0
author: ohjerryho
---

# Paper Taxonomy

A classification system for economics papers. Use this when you're unsure how to categorize a paper.

## Primary classification axis: Empirical vs. Theoretical

### Pure empirical (reduced form)
- Uses observational or quasi-experimental data
- Identification strategy is explicit (DiD, IV, RDD, SC, matching)
- No formal model required
- Typical venues: JPE, QJE, AER, REStud, Journal of Labor Economics, Journal of Public Economics
- **Signal**: Abstract mentions "natural experiment", "exploits variation in", "difference-in-differences"

### Pure empirical (structural)
- Writes down a formal model
- Estimates structural parameters (GMM, MLE, SMM)
- Uses estimates for counterfactual policy analysis
- Typical venues: Econometrica, JPE, REStud, RAND Journal of Economics, Journal of Finance
- **Signal**: Abstract mentions "structural model", "counterfactual", "welfare analysis", "equilibrium"

### Pure theory
- No data, no calibration (or minimal illustration)
- Contribution = set of propositions/theorems
- Typical venues: Econometrica, JPE, Theoretical Economics, Journal of Economic Theory, Games and Economic Behavior
- **Signal**: Abstract mentions "characterize", "necessary and sufficient conditions", "equilibrium exists", "show that"

### Applied theory / theory with calibration
- Formal model + calibrated to aggregate moments
- Counterfactual simulations
- Typical venues: AER, Econometrica, Journal of Monetary Economics, Journal of Finance
- **Signal**: Abstract mentions "calibrated to match", "model moments", "aggregate data"

### Mixed (most common in top journals)
- Theoretical model motivates or guides empirical strategy
- OR: empirical evidence motivates/validates the model
- **Subtypes**:
  - *Theory-led*: Model first, empirics confirm model predictions
  - *Empirics-led*: Stylized facts first, model rationalizes them
  - *Sufficient statistics*: Model derives formula; empirics estimate key parameters in formula

### Survey / literature review
- Maps a literature, synthesizes findings
- No primary identification or new model
- Typical venues: Journal of Economic Literature, Journal of Economic Perspectives, Annual Review of Economics
- **Signal**: Extensive literature references, section structure around themes, invited articles

---

## Secondary classification axis: Subfield

| Subfield | Common methods | Common data sources |
|----------|---------------|---------------------|
| Labor economics | DiD, IV, RDD, matching | CPS, NLSY, admin payroll records |
| Public economics | DiD, bunching, RDD, structural | Tax records, SIPP, ACS |
| Development economics | RCT, IV, DiD, structural | LSMS, DHS, village surveys |
| IO (Industrial Organization) | Structural (BLP, merger simulation), DiD | Nielsen, Compustat, patents |
| Macroeconomics | Structural, calibration, local projection | FRED, national accounts, Compustat |
| Finance | Event study, IV, structural | CRSP, Compustat, OptionMetrics |
| Trade | Gravity, structural (Armington/EK), shift-share | UN Comtrade, customs records |
| Health economics | DiD, IV, RDD, structural | MEPS, CMS, hospital records |
| Urban / Housing | RD, hedonic, DiD, structural | Census, MLS, Zillow |
| Political economy | RD, IV, natural experiments | Election data, congressional records |

---

## Chinese economics paper conventions

Chinese-language economics papers warrant special classification note. See `references/chinese-vs-english.md` for detailed reading guide. Key classification adjustments:

| Dimension | Top English journal | Chinese CSSCI paper |
|-----------|--------------------|--------------------|
| Identification standard | Near-experimental required for top journals | Descriptive/correlational more accepted |
| Theory model | Often required in top journals | Optional; many descriptive papers lack formal model |
| Policy section | Brief implications | Often a standalone 政策建议 section |
| Contribution claim | "This paper is first to..." explicit | Often implicit or institutional focus |
| Chinese institutional context | Often generic | Often requires knowledge of specific Chinese policies (hukou, SOE reform, tax law) |

---

## Quick-classification heuristic

Read the abstract. Ask:
1. Is there a dataset? → Empirical component
2. Is there an identification strategy named? → Reduced form
3. Is there "structural model" / "equilibrium" / "counterfactual"? → Structural
4. Are there propositions / theorems? → Theory component
5. Is the dataset Chinese administrative or survey data? → Chinese institutional context matters
