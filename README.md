# 访谈提纲优化专家（Interview Guide Optimizer）

面向质性研究领域的访谈提纲系统化评审与优化技能。支持局部评审（部分问题）和完整评审（完整提纲）两种模式，并可在用户明确要求时接入知识库，从相关文献中提炼问题灵感。

---

## 主要能力

### 1. 双模式评审

| 模式 | 触发条件 | 评审范围 |
|------|---------|---------|
| **局部模式** | 用户仅提交若干条问题（非完整提纲） | 仅检查单条问题的表述合理性（引导性、清晰度、措辞） |
| **完整模式** | 用户提交完整访谈提纲 | 全方位评审：问题表述 → 问题间逻辑 → 与研究目标的对齐 |

技能会自动判断使用哪种模式，无法确定时会询问用户。

### 2. 评审关注点

**完整模式**（12 项关注点，详见 `references/full.md`）：
- **提纲与研究目标对齐**：问题是否覆盖全部研究问题/核心变量，是否存在遗漏或冗余
- **问题引入合理性**：问题是否与受访者经验匹配、是否符合其认知水平
- **问题间逻辑与递进设计**：是否有从事实铺垫→深层体验的合理过渡，是否缺少配套事例追问
- **引导性/预设性提问红线**：措辞是否嵌入研究者偏见，是否默认某类情况必然存在
- **问题表述清晰度**：抽象概念是否有落地场景、是否一题多问
- **措辞与术语规范**：是否避免使用负面词汇、学术术语
- **深层感受类提问准则**：是否先问事实再深挖感受
- **访谈素材产出要求**：每个感受/实践类问题是否配套具体事例追问
- **对比类问题设计规范**：涉及两类事物对比时是否同步覆盖各自优势与短板
- ……更多（详见 `references/full.md`）

**局部模式**（4 项关注点，详见 `references/part.md`）：
- 引导性、预设性提问红线
- 问题表述清晰度规范
- 措辞与术语使用规范
- 深层感受类通用提问准则

### 3. 知识库灵感推荐（可选）

当用户明确要求接入知识库时，技能会：

- 通过 `ima-mcp` 检索用户指定知识库中的相关质性研究论文
- 从每篇论文的**研究问题（RQ）**、**研究发现（Findings）**、**研究局限（Limitations）**中提炼灵感
- 向用户推荐**还可补充的提问方向**，并给出具体的自然语言提问示例

> **核心设计原则**：不要求论文附有访谈提纲，也不直接照搬论文中的提问。而是把论文的 RQ / Findings / Limitations 当作"问题灵感库"，结合用户的实际研究情境进行适配。

### 4. 结构化输出

- **局部模式**：简洁的两部分反馈 —— ① 逐条评价 ② 修改建议（如有）
- **完整模式**：完整的三/四部分反馈 —— ① 总体评价 ② 分点问题清单 ③ 修改建议 ④ 知识库灵感推荐（若启用）

---

## 安装方法

### 方式一：一句话安装

在 WorkBuddy 对话中直接发送：

```
安装技能 https://github.com/charlieliucc/interview-guide-optimizer
```

安装完成后立即生效。

> **使用知识库功能前**，需先完成以下准备：
> 1. 在 WorkBuddy 中开通 **ima 知识库**授权（设置 → 连接器 → ima知识库 → 开启）
> 2. 将相关研究文献（PDF/论文全文）上传至你的 ima 知识库
> 3. 安装完成后，在对话中提到"参考知识库"即可触发知识库灵感推荐功能

### 方式二：手动安装

1. 找到你的 WorkBuddy 技能目录：
   ```
   ~/.workbuddy/skills/
   ```
2. 将 `interview-guide-optimizer/` 整个文件夹复制到该目录下：
   ```
   ~/.workbuddy/skills/interview-guide-optimizer/
   ```
3. 重启 WorkBuddy 或执行 `/skills reload`（若支持）

### 验证安装

在 WorkBuddy 对话中发送：
```
帮我看看这条访谈问题设计得怎么样："你觉得AI对你的工作有帮助吗？"
```

如果技能被触发并返回结构化反馈，说明安装成功。

---

## 使用示例

### 局部评审

```
用户：帮我看看这三条问题：
1. 你觉得平台算法定价对你来说是公平的吗？
2. 你能描述一下你遇到的困难吗？
3. 你认为你的身份认同感受到了挑战吗？
```

→ 触发**局部模式**，逐条检查引导性、清晰度、措辞问题。

### 完整评审

```
用户：这是我完整的访谈提纲，请帮我评审：
[完整提纲文本……]
```

→ 触发**完整模式**，执行 12 项关注点全面检查，输出结构化修改方案。

### 知识库灵感推荐

```
用户：这是我的访谈提纲。另外请参考我的知识库"平台劳动研究"，
     帮我看看还有哪些问题可以补充。
```

→ 执行完整评审 + 检索知识库 → 在输出末尾附加"④ 知识库灵感推荐"部分。

---

## 文件结构

```
interview-guide-optimizer/
├── SKILL.md              # 技能定义文件（WorkBuddy 加载入口）
└── references/
    ├── part.md           # 局部评审关注点（4 项）
    └── full.md           # 完整评审关注点（12 项）
```

---

## 贡献

本技能基于质性研究（焦点小组/深度访谈提纲设计）的实际指导反馈开发。如果你有新的评审关注点建议或对现有内容的改进意见，欢迎提 Issue 或 PR。

---

## 许可证

MIT

---

<br>

---

<br>

# Interview Guide Optimizer

A WorkBuddy skill for systematic review and optimization of interview guides in qualitative research. It detects wording flaws, logical gaps, and alignment issues against research goals — then produces structured, actionable revision suggestions.

---

## Key Capabilities

### 1. Dual Review Modes

| Mode | When to Use | Scope |
|------|------------|-------|
| **Partial review** | User submits a few questions (not a full guide) | Checks each question for wording clarity, leadingness, and terminology — no structural analysis |
| **Full review** | User submits a complete interview guide | Comprehensive review: wording → question logic → alignment with research objectives |

The skill auto-detects which mode to use, or asks the user if unclear.

### 2. Review Criteria

**Full mode** (12 criteria, see `references/full.md`):
- **Alignment with research goals**: Does the guide cover all research questions / core variables?
- **Question appropriateness**: Are questions matched to the interviewee's experience and cognitive level?
- **Logical flow & progression**: Is there proper transition from factual warm-up → deeper experience → reflection? Are concrete example prompts included?
- **Leadingness red flags**: Does the wording embed researcher bias or presuppose answers?
- **Clarity**: Are abstract concepts grounded in concrete scenarios? Is each question single-focused?
- **Wording & terminology**: Are negative/extreme words avoided? Is academic jargon kept out of interviewee-facing text?
- **Deep-feeling question norms**: Are feeling-based questions properly preceded by behavioral fact questions?
- **Case-prompting requirement**: Does every feeling/practice question have a companion prompt asking for a concrete example?
- **Comparative question design**: Are both advantages and shortcomings covered when comparing two subjects?
- ...and more (see `references/full.md`)

**Partial mode** (4 simplified criteria, see `references/part.md`):
- Leadingness & presupposition red flags
- Question clarity norms
- Wording & terminology norms
- Deep-feeling question guidelines

### 3. Knowledge Base Inspiration (Optional)

When the user explicitly asks to reference a knowledge base, the skill:

- Searches the user's connected knowledge base (via `ima-mcp`) for relevant qualitative research papers
- Extracts inspiration from each paper's **Research Questions**, **Findings**, and **Limitations**
- Recommends **new question directions** the user may not have considered — with concrete natural-language question examples

> **Key design principle**: The skill does NOT copy questions from papers. It treats papers as an "idea library" and adapts suggestions to the user's actual research context.

### 4. Structured Output

- **Partial mode**: Concise 2-section feedback — ① Per-question evaluation ② Revision suggestions (if any)
- **Full mode**: Comprehensive 3- or 4-section feedback — ① Overall assessment ② Point-by-point problem list ③ Detailed revision suggestions ④ Knowledge base inspiration (if enabled)

---

## Installation

### Method 1: One-Line Install

In a WorkBuddy conversation, simply send:

```
install skill https://github.com/charlieliucc/interview-guide-optimizer
```

The skill takes effect immediately after installation.

> **Before using the knowledge base feature**, complete the following setup:
> 1. Enable **ima Knowledge Base** authorization in WorkBuddy (Settings → Connectors → ima Knowledge Base → Enable)
> 2. Upload relevant research papers (PDF/full text) to your ima knowledge base
> 3. Once done, mention "参考知识库" (reference knowledge base) in your conversation to trigger the knowledge base inspiration feature

### Method 2: Manual Install

1. Locate your WorkBuddy skills directory:
   ```
   ~/.workbuddy/skills/
   ```
2. Copy the entire `interview-guide-optimizer/` folder into it:
   ```
   ~/.workbuddy/skills/interview-guide-optimizer/
   ```
3. Restart WorkBuddy or run `/skills reload` (if supported)

### Verify Installation

In a WorkBuddy conversation, send:
```
帮我看看这条访谈问题设计得怎么样："你觉得AI对你的工作有帮助吗？"
```

If the skill triggers and returns structured feedback, the installation was successful.

---

## Usage Examples

### Partial Review

```
User: 帮我看看这三条问题：
1. 你觉得平台算法定价对你来说是公平的吗？
2. 你能描述一下你遇到的困难吗？
3. 你认为你的身份认同感受到了挑战吗？
```

→ Triggers **partial mode**, checks each question for leadingness, clarity, and wording.

### Full Review

```
User: 这是我完整的访谈提纲，请帮我评审：
[full guide text...]
```

→ Triggers **full mode**, runs the complete 12-criteria checklist, outputs structured revision plan.

### Knowledge Base Inspiration

```
User: 这是我的访谈提纲。另外请参考我的知识库"平台劳动研究"，帮我看看还有哪些问题可以补充。
```

→ Runs full review + searches the knowledge base → appends a "④ Knowledge Base Inspiration" section to the output.

---

## File Structure

```
interview-guide-optimizer/
├── SKILL.md              # Skill definition (loaded by WorkBuddy)
└── references/
    ├── part.md           # Partial review criteria (4 criteria)
    └── full.md           # Full review criteria (12 criteria)
```

---

## Contributing

This skill was developed based on real qualitative research supervision feedback (focus group / in-depth interview guide design). If you have suggestions for new review criteria or improvements to existing ones, feel free to open an issue or PR.

---

## License

MIT
