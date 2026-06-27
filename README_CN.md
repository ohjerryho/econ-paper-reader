# econ-paper-reader

> 面向经济学文献的结构化 AI 阅读技能系统。

**作者**: ohjerryho  
**版本**: 0.1.0  
**许可证**: MIT

---

## 这个技能做什么

经济学文献有一套严格的叙事逻辑——每个章节有其职责，每张表格讲述一部分故事，每种识别策略依赖特定的假设。读懂文献，首先要知道每个部分"应该"包含什么。

`econ-paper-reader` 将顶级期刊的写作规范"反转"，从写作惯例倒推阅读框架。结果是：对任意一篇经济学文献的结构化、批判性解读——无论是 AER 实证文章、QJE 理论文章、Econometrica 结构估计，还是中文 CSSCI 政策论文。

---

## 技能结构

这是一个**技能集合**——一个主协调技能，搭配六个专项子技能和四个参考文件。

```
econ-paper-reader/
├── SKILL.md                               ← 主技能：分类 → 路由 → 产出阅读报告
├── README.md                              ← 英文说明
├── README_CN.md                           ← 中文说明（本文件）
│
├── subskills/
│   ├── epr-structure/SKILL.md             ← 论文结构解析（各部分期望内容）
│   ├── epr-empirical/SKILL.md             ← 实证文献（RF回归 + 结构估计）
│   ├── epr-theory/SKILL.md                ← 理论模型（假设、命题、推论）
│   ├── epr-methodology/SKILL.md           ← 计量方法论文（新估计量、识别策略辨析）
│   ├── epr-causal-inference/SKILL.md      ← 因果识别策略（8种）
│   └── epr-tables-figures/SKILL.md        ← 表格与图形解读
│
└── references/
    ├── paper-taxonomy.md                  ← 文献类型分类体系
    ├── causal-methods-ref.md              ← 因果推断方法深度参考
    ├── theory-components-ref.md           ← 理论模型构件速查
    └── chinese-vs-english.md             ← 中英文文献规范差异
```

### 子技能前缀说明

所有子技能以 `epr-` 开头，这是 **econ-paper-reader** 的缩写，用于与其他技能集合中的子技能区分，避免命名冲突。

---

## 技能能做什么

| 任务 | 调用子技能 |
|------|-----------|
| 判断文章类型（实证/理论/结构/计量方法） | `epr-structure` + `paper-taxonomy.md` |
| 产出结构化阅读报告 | 所有相关子技能 |
| 评估识别策略的可信度 | `epr-causal-inference` + `causal-methods-ref.md` |
| 读懂回归表格 | `epr-tables-figures` |
| 解码理论模型的假设和命题 | `epr-theory` + `theory-components-ref.md` |
| 读懂计量方法创新类文章 | `epr-methodology` |
| 审稿人视角的全面评审 | 所有子技能 |
| 阅读中文经济学文献 | `chinese-vs-english.md` |
| 快速扫读，提取要点 | `epr-structure`（快速模式）|

---

## 使用方式

### 在 Claude Code / AWS Kiro 中使用

将本目录放入 `.claude/skills/` 文件夹，或在技能加载器中指向该目录。随后直接提问：

> "帮我读一下这篇文献，识别策略可信吗？"  
> "总结这篇工作论文的主要结论。"  
> "帮我理解第三节的模型。"  
> "表2说明了什么？"  
> "这篇文章方法论有什么问题？"

技能会在涉及经济学文献阅读的任务时自动触发。

### 对 PDF 文献的支持

本技能高度依赖 PDF 阅读能力。建议搭配安装 PDF 阅读工具或技能（如 `/pdf-read`）以获得最佳效果。如未安装，可将论文文本手动粘贴给 agent。

### 阅读深度

**快速扫读**（~5分钟）：摘要 + 引言 + 结论 + 浏览表格。
> "快速读一下这篇文章。"

**标准阅读**：全文阅读，产出结构化报告。
> "读这篇文章，给我一份阅读报告。"

**审稿级阅读**：逐节批判性评估，适合判断发表潜力。
> "像 AER 审稿人一样评审这篇文章。"

---

## 阅读报告格式

```
## 阅读报告：[论文标题]

引用：作者（年份）。"题目。"《期刊》。
文章类型：[实证-简约式 / 理论 / 实证-结构 / 混合 / 计量方法 / 综述]
风格：[英文顶刊 / 中文CSSCI / 工作论文]

核心问题    — 这篇文章研究什么问题？
研究设计    — 如何回答这个问题？（识别策略或模型方法）
主要结论    — 2–4个核心发现，含经济意义量化
贡献声明    — 作者声称的创新是什么？
优点        — 设计的最强之处
疑虑/弱点   — 识别假设的威胁、模型缺陷、遗漏稳健性检验
总体评价    — 是否可信？发表潜力如何？
```

---

## 支持的文章类型

| 类型 | 支持程度 |
|------|---------|
| 实证 — 简约式（Reduced Form） | ✅ 完整（DiD/IV/RDD/SC/RCT/Matching等） |
| 实证 — 结构估计 | ✅ 完整 |
| 理论模型 | ✅ 完整 |
| 计量方法论文 | ✅ 完整（包含新估计量与方法辨析） |
| 混合（理论+实证） | ✅ 完整 |
| 综述/前沿介绍 | ✅ 基础支持 |
| 英文顶刊（AER/QJE/JPE/REStud/Econometrica等） | ✅ |
| 中文CSSCI（经济研究/管理世界/世界经济等） | ✅ 含专项中文规范指南 |
| 工作论文（NBER/CEPR/SSRNl等） | ✅ |

---

## 致谢

本技能的参考资料来源于以下开源仓库，感谢原作者：

**写作与投稿规范**

| 仓库 | 作者/组织 | 用途 |
|------|----------|------|
| [AER-Skills](https://github.com/brycewang-stanford/AER-Skills) | brycewang-stanford | AER 投稿流程与各节写作标准 |
| [econ-TopJournal-writing-Skill](https://github.com/juliaError/econ-TopJournal-writing-Skill) | juliaError | 顶刊写作技能（含中文顶刊） |
| [econ-writing-skill](https://github.com/hanlulong/econ-writing-skill) | hanlulong | 综合经济学写作原则 |
| [journal-adapt-writing-skill](https://github.com/WantongC/journal-adapt-writing-skill) | WantongC | 期刊适配写作技能 |
| [research-writing-skill](https://github.com/Norman-bury/research-writing-skill) | Norman-bury | 研究写作综合框架 |

**因果推断与计量**

| 仓库 | 作者/组织 | 用途 |
|------|----------|------|
| [causal-inference-mixtape](https://github.com/Jill0099/causal-inference-mixtape) | Jill0099 | 基于 Cunningham《Causal Inference: The Mixtape》的识别策略技能 |
| [codex-stata-for-economists](https://github.com/maxwell2732/codex-stata-for-economists) | maxwell2732 | Stata 经济学工具箱（含 review-paper、lit-review 等技能） |

**理论模型**

| 仓库 | 作者/组织 | 用途 |
|------|----------|------|
| [pAI-Econ-claude](https://github.com/maxwell2732/pAI-Econ-claude) | maxwell2732，原作者：Chen Zhu、Xiaolu Wang（中国农业大学）、Weilong Zhang（剑桥大学） | 理论经济学模型库，含28+基准模型参考文献 |

**综合工具**

| 仓库 | 作者/组织 | 用途 |
|------|----------|------|
| [AcademicForge](https://github.com/HughYau/AcademicForge) | HughYau | 学术研究综合工具 |
| [Auto-Empirical-Research-Skills](https://github.com/brycewang-stanford/Auto-Empirical-Research-Skills) | brycewang-stanford | 实证研究自动化技能集 |
| [awesome-ai-for-economists](https://github.com/hanlulong/awesome-ai-for-economists) | hanlulong | AI 经济学工具资源列表 |
| [awesome-econ-ai-stuff](https://github.com/meleantonio/awesome-econ-ai-stuff) | meleantonio | AI 经济学相关技能与资源 |

---

## 更新日志

### v0.1.0（2026-06-27）
- 初始版本
- 6个子技能：epr-structure / epr-empirical / epr-theory / epr-methodology / epr-causal-inference / epr-tables-figures
- 4个参考文件：paper-taxonomy / causal-methods-ref / theory-components-ref / chinese-vs-english
