---
name: epr-related-refs
description: >
  Select and format the top 3 most relevant references from a paper's reference list.
  Always loaded last in econ-paper-reader. Applies ref-format citation rules.
---

# epr-related-refs

Select up to 3 references from the paper's own reference list for the **延伸阅读** section.

## Selection criteria

Rank candidate references by:

1. **Citation frequency** — how many times is the paper cited in the body text?
2. **Centrality to core argument** — does the paper underpin the main identification strategy, theoretical framework, or key empirical finding?
3. **Title/topic overlap** — does the title suggest direct relevance to this paper's central question?

When unsure about a reference's relevance, a brief web search on the title is acceptable to verify.

## Hard constraints

- **Only from this paper's reference list** — never fabricate or infer references not explicitly listed.
- **Maximum 3** — if fewer than 3 are clearly relevant, list only those that are.
- **No [J]/[R]/[M] markers needed if unclear** — omit the marker rather than guess the reference type.

## Output format

Apply ref-format rules exactly:

### Author rules
- **Chinese**: separate authors with `,` (not 、); no 等
- **English**: `LastName, Initial.` format; separate with `,`; no "and"; no "et al." unless full list unavailable

### Template by type

**Chinese journal** `[J]`:
```
作者. 年份. 标题[J]. 期刊名称, (期号).
作者. 年份. 标题[J]. 期刊名称, 卷号(期号): 页码.
```

**English journal** `[J]`:
```
LastName, I., LastName, I. Year. Title[J]. Journal Name, Volume(Issue): Pages.
```

**Working paper** `[R]`:
```
LastName, I. Year. Title[R]. Institution, Working Paper No. XXXX.
```

**Book** `[M]`:
```
Author. Year. Title[M]. City: Publisher.
```

### Sorting
- Chinese references first (sorted by pinyin of first author's first character)
- English references after (sorted alphabetically by first author's last name)
- Continuous numbering: [1], [2], [3]

### Punctuation
- Year always followed by `.` (e.g., `2023.` not `2023,`)
- Issue in parentheses: `(5)` not `第5期`
- Pages preceded by `:` in English refs

## Example output

```
### 延伸阅读

[1] 黄炜, 刘冲, 潘彬. 2022. 双重差分法的理论基础与应用[J]. 经济研究, (5).
[2] Callaway, B., Sant'Anna, P. H. C. 2021. Difference-in-Differences with Multiple Time Periods[J]. Journal of Econometrics, 225(2): 200-230.
[3] Sun, L., Abraham, S. 2021. Estimating Dynamic Treatment Effects in Event Studies with Heterogeneous Treatment Effects[J]. Journal of Econometrics, 225(2): 175-199.
```
