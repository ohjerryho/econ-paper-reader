<p align="center">
  <img src="assets/cover.png" alt="econ-paper-reader 封面" width="100%">
</p>

<h1 align="center">econ-paper-reader</h1>

<p align="center">
  <strong>面向经济学文献的结构化 AI 阅读、解释与批判性分析技能系统。</strong>
</p>

<p align="center">
  <a href="README.md">English README</a>
  ·
  <a href="#这个技能可以做什么">这个技能可以做什么</a>
  ·
  <a href="#技能架构">技能架构</a>
  ·
  <a href="#阅读报告">阅读报告</a>
  ·
  <a href="#快速开始">快速开始</a>
  ·
  <a href="#使用方式">使用方式</a>
</p>

<p align="center">
  <img alt="Version" src="https://img.shields.io/badge/version-0.6.1-0b4f5c">
  <img alt="License" src="https://img.shields.io/badge/license-MIT-e8ad63">
  <img alt="Domain" src="https://img.shields.io/badge/domain-economics%20papers-234">
  <img alt="Skill" src="https://img.shields.io/badge/type-agent%20skill%20system-5fb2ab">
</p>

---

## 这个技能可以做什么

经济学论文不是普通信息文本。它有一套相当固定的叙事逻辑：每个章节承担不同任务，每张表格都是论证链的一部分，每一种识别策略都依赖一组需要被检查的假设。

`econ-paper-reader` 的目标，是让 AI agent 更像受过训练的经济学研究者那样读论文：先判断论文类型，再加载相应的分析视角，重构研究故事，最后评估研究设计、模型设定、表图证据和作者主张之间是否真正匹配。

这个技能的核心思想是：

> **阅读与写作互为逆过程。**  
> 顶级期刊写作有稳定的结构规范。把这些写作规范反过来编码成阅读框架，agent 就知道读论文时应该寻找什么、质疑什么、如何组织判断。

它不是通用论文总结器，而是面向经济学论文的领域化阅读系统，覆盖：

- reduced-form 实证论文；
- 结构估计与结构模型；
- 理论模型论文；
- 计量方法论文；
- 理论 + 实证混合型论文；
- 综述 / perspective 类文章；
- 中文 CSSCI 风格的政策与制度研究。

## 功能亮点

| 能力 | agent 会重点检查什么 |
|---|---|
| **论文类型判断** | RF 实证、结构估计、理论、方法、混合型、综述/评论 |
| **确定性子技能路由** | 按论文类型加载对应子技能，不随意多读文件，不靠猜 |
| **研究故事重构** | 背景、文献空白、研究设计、主要发现、贡献与意义 |
| **识别策略评估** | DiD、IV、RDD、合成控制、匹配、事件研究及常见威胁 |
| **方程级阅读** | 回归方程、模型原语、均衡条件、符号说明表 |
| **表格与图形解读** | 回归表、事件研究图、RD 图、平衡性表、稳健性表 |
| **政策与制度背景** | 政策、改革、事件、制度环境，尤其适合中文政策论文 |
| **审稿人式判断** | 亮点、不足、缺失检验、外部有效性、发表或引用价值 |
| **延伸阅读整理** | 从论文参考文献中挑选真正相关的核心文献并规范格式 |

## 技能架构

`econ-paper-reader` 是一个**技能集合**：一个主协调技能，八个专项子技能，以及四个参考文件。

<details open>
<summary><strong>目录结构</strong></summary>

```text
econ-paper-reader/
├── SKILL.md                            # 主技能：分类、路由、产出阅读报告
├── README.md                           # 英文说明
├── README_CN.md                        # 中文说明
├── assets/
│   └── cover.png                       # GitHub README 封面图
│
├── subskills/
│   ├── epr-structural/SKILL.md          # 论文结构：各章节应承担什么任务
│   ├── epr-empirical/SKILL.md          # RF 实证与结构估计论文
│   ├── epr-theoretical/SKILL.md             # 理论模型与结构模型阅读
│   ├── epr-methodology/SKILL.md        # 计量方法与研究方法论文
│   ├── epr-causal-inference/SKILL.md   # 因果识别策略与诊断
│   ├── epr-tables-figures/SKILL.md     # 回归表、事件研究图、RD 图等
│   ├── epr-policy-context/SKILL.md     # 政策、改革和制度背景
│   └── epr-related-refs/SKILL.md       # 延伸阅读文献选择与格式化
│
└── references/
    ├── paper-taxonomy.md               # 经济学论文类型分类体系
    ├── causal-methods-ref.md           # 因果推断方法深度参考
    ├── theory-components-ref.md        # 模型原语、均衡、证明阅读速查
    └── chinese-vs-english.md           # 中英文经济学论文规范差异
```

</details>

所有子技能都使用 `epr-` 前缀，避免和其他技能集合发生命名冲突。

## 路由逻辑

主技能会先判断论文类型，然后按固定表格加载子技能。这个设计是刻意的：分类之后，agent 不再临时猜测应该读哪些能力文件。

| 论文类型 | 按顺序加载的子技能 |
|---|---|
| **Empirical - Reduced Form** | `epr-structural` -> `epr-empirical` -> `epr-causal-inference` -> `epr-tables-figures` |
| **Empirical - Structural** | `epr-structural` -> `epr-empirical` -> `epr-theoretical` -> `epr-tables-figures` |
| **Theoretical** | `epr-structural` -> `epr-theoretical` |
| **Methodology** | `epr-structural` -> `epr-methodology`；若涉及识别策略批判，再加载 `epr-causal-inference` |
| **Mixed** | `epr-structural` -> `epr-empirical` -> `epr-theoretical` -> `epr-causal-inference` -> `epr-tables-figures` |
| **Survey / Perspective** | `epr-structural` |

额外规则：

- 如果论文研究政策、事件、改革，或涉及中文制度语境，额外加载 `epr-policy-context`。
- 所有论文类型最后都加载 `epr-related-refs`。
- 深度参考文件只在相关子技能明确要求时加载。

## 阅读报告

标准阅读报告适合用作读书笔记、组会准备、文献综述材料、审稿式评估或研究选题判断。

```text
# [论文标题]

作者 / 来源 / 研究领域 / Paper type

这篇文章讲了个什么故事
  叙事式开篇：现实背景、文献空白、研究思路、主要发现、理论或政策意义

政策与背景
  相关政策 / 事件表 + 制度背景说明

核心问题
  用一句话说明本文回答什么问题

研究设计
  识别策略或理论框架

模型设定
  核心模型方程 + 符号说明表 + 关键假设

实证设计
  回归方程 + 变量说明表 + 设计注意事项

主要发现
  核心结论，实证论文需要给出经济量级

核心贡献
  相对既有文献的新意

亮点
  最有说服力的部分

不足与疑问
  识别威胁、模型缺陷、遗漏的稳健性检验、外部有效性问题

综合评价
  总体判断、可信度与研究价值

延伸阅读
  从论文参考文献列表中选择的关键相关文献
```

## 快速开始

把这个仓库 clone 到你的 agent 技能目录中即可安装。

### Codex

```bash
mkdir -p ~/.codex/skills
git clone https://github.com/ohjerryho/econ-paper-reader.git ~/.codex/skills/econ-paper-reader
```

安装后重启 Codex，让新的技能元信息进入技能列表。

### Claude Code

```bash
mkdir -p ~/.claude/skills
git clone https://github.com/ohjerryho/econ-paper-reader.git ~/.claude/skills/econ-paper-reader
```

安装后重启 Claude Code，让技能生效。

### 更新已有安装

```bash
git -C ~/.codex/skills/econ-paper-reader pull
# 或者，如果你安装在 Claude Code:
git -C ~/.claude/skills/econ-paper-reader pull
```

如果你使用的是其他支持技能目录的 agent runtime，请把本仓库安装为名为
`econ-paper-reader` 的技能文件夹，并确保 `SKILL.md` 位于该文件夹根目录。

## 使用方式

把本目录放到你的 agent 技能加载路径下，例如：

```text
~/.codex/skills/econ-paper-reader/
~/.claude/skills/econ-paper-reader/
```

然后直接用自然语言提问：

```text
帮我读一下这篇论文，识别策略可信吗？
总结这篇 working paper 的主要发现。
帮我理解第三节的理论模型。
表 2 到底说明了什么？
这篇论文适不适合放进我的文献综述？
用审稿人的视角评价这篇文章。
```

### PDF 支持

本技能最好搭配 PDF 阅读能力使用。经济学论文大多以 PDF 发布；如果当前 agent 没有 PDF 解析能力，最好为其配备好相关的 skills 或 MCP。

### 阅读深度

| 模式 | 适合场景 | 典型输出 |
|---|---|---|
| **快速扫读** | 初筛文献、判断是否值得细读或引用 | 3-5 句摘要 + 核心 caveat |
| **标准阅读** | 组会准备、读书笔记、文献综述 | 完整结构化阅读报告 |
| **审稿级阅读** | 深度批判、复现准备、发表价值判断 | 扩展版问题清单、设计威胁、总体 verdict |

## 适合用在什么任务

适合在这些场景触发：

- 想理解一篇经济学论文的论证逻辑，而不只是要摘要；
- 想判断识别策略是否可信；
- 需要读懂回归表、事件研究图、RD 图或稳健性检验；
- 需要梳理理论模型的假设、命题、均衡和比较静态；
- 需要从实证论文或中文政策论文中提取政策 / 制度背景；
- 需要判断一篇论文是否值得引用、放进综述、作为选题基础或用于 replication。

## 不适合替代什么

这个技能不能替代：

- 真实的数据和代码复现；
- 严格的数学证明检查；
- 领域专家的最终判断；
- PDF parser、OCR 或图表识别工具；
- 论文参考文献之外的系统性文献发现。

它的作用是让 agent 的阅读方式更接近经济学研究训练，而不是保证论文本身一定正确、因果识别一定成立、或结论一定可发表。

## Token 消耗

这是一个**重量级技能**。完整阅读一篇经济学论文时，通常需要加载多个子技能文件，再读取论文全文。

| 文献长度 | 大致 token 消耗 |
|---|---:|
| 短篇论文 / working paper，约 20-30 页 | 150k-200k tokens |
| 完整期刊论文，约 40-50 页 | 200k-300k tokens |

快速扫读模式会显著更省，因为它只加载最少上下文并选择性阅读。

## 设计原则

1. **读论证，而不是只读信息。**  
   经济学论文的主线通常是：动机 -> 设计/模型 -> 证据 -> 贡献。

2. **把识别策略视为实证论文的脊梁。**  
   核心问题不是“作者估计了什么”，而是“为什么我们应该相信这是因果关系”。

3. **重要方程必须显性化。**  
   关键回归方程、模型条件和符号说明应以 LaTeX 和表格形式呈现，而不是被口头概括掉。

4. **系数要有经济量级解释。**  
   显著性不等于经济意义。需要追问：这个效应到底有多大？

5. **区分作者主张和读者判断。**  
   报告既要还原作者如何论证，也要评价这个论证是否站得住。

## 元信息

| 字段 | 内容 |
|---|---|
| 作者 | `ohjerryho` |
| 仓库 | `github.com/ohjerryho/econ-paper-reader` |
| 版本 | `0.6.1` |
| 许可证 | `MIT` |

## 更新日志

<details>
<summary><strong>v0.6.1 及以前</strong></summary>

### v0.6.1（2026-06-28）

- 新增快速安装说明，覆盖 Codex、Claude Code 和通用 agent runtime。
- 新增已有本地安装的更新命令。
- 更新 README 展示方式，加入项目封面图并完善中英文文档。

### v0.6.0（2026-06-27）

- 开篇章节改为**“这篇文章讲了个什么故事”**：完整叙事，而不是简短摘要。
- 子技能路由改为按论文类型确定性触发。
- 新增理论 / 结构估计论文的**模型设定**强制输出块。
- `epr-related-refs` 不再强制凑够固定数量的参考文献。

### v0.5.0（2026-06-27）

- 新增 `epr-policy-context`：政策 / 事件表 + 政治与制度背景。
- 阅读报告模板新增**政策与背景**章节。

### v0.4.1（2026-06-27）

- 新增开篇概括节，后来在 v0.6.0 中升级为叙事式开篇。

### v0.4.0（2026-06-27）

- RF 实证论文新增**实证设计**强制输出块。

### v0.3.1（2026-06-27）

- 新增章节标题语言一致性规则。

### v0.3.0（2026-06-27）

- 新增 `epr-related-refs`，整合 `ref-format` 格式规范。
- 简化报告头部，并禁止在输出中写内部处理独白。

### v0.2.0（2026-06-27）

- 新增 `epr-methodology`。
- 新增 `README_CN.md`。

### v0.1.0（2026-06-27）

- 初始版本：5 个子技能 + 4 个参考文件。

</details>
