---
name: paper-caption-polish
description: 将中文论文图标题、表标题译成简洁规范的英文，或优化已有英文图表标题。适用于图题/表题翻译、caption polishing、标题大小写与 LaTeX 特殊字符规范化；不用于论文主标题、正文润色或图表绘制。
---

# 论文图表标题优化

以学术编辑的标准，将用户提供的中文描述或已有英文图表标题改写为准确、简洁、可直接用于论文的英文标题。统一处理图标题与表标题，默认遵循下面的大小写和 LaTeX 规则；用户指定的会议、期刊模板或输出格式优先。

## 内容与措辞

- 根据用户说明或上下文识别图题或表题。类型不明但不影响措辞时直接处理；只有缺失信息会改变含义时才提问。
- 忠实保留研究对象、比较关系、实验条件、指标、数据集、方法名与数值。术语有上下文时沿用上下文，不添加未提供的结果、因果关系、优越性或统计显著性。
- 默认优先使用自然的名词性短语；完整句子更适合表达原意时保留句子，不为缩短标题而损失必要信息。
- 删除 `The figure shows`、`This diagram illustrates`、`This table presents` 等冗余引导，直接描述内容。使用平实、常见、准确的词，避免 `showcase`、`depict` 等装饰性表达；确需动词时优先考虑 `show`、`compare`、`present`。
- 图标题可按内容使用 `Architecture of`、`Overview of`、`Performance comparison`、`Visualization of` 等表达。
- 表标题可按内容使用 `Comparison with`（与某对象比较）、`Comparison of`（比较多个对象）、`Ablation study on`、`Results on` 等表达。仅在含义相符时采用，不机械套用句式。

## 大小写与句末标点

先判断最终英文是名词性短语还是完整句子，再应用对应规则。

- **名词性短语：Title Case，末尾不加句号。** 首尾词及实词（名词、代词、动词、形容词、副词）首字母大写；非首尾的冠词、并列连词、介词通常小写，例如 `a`、`an`、`the`、`and`、`or`、`of`、`on`、`with`。连字符连接的实词分别大写，例如 `Cross-Dataset Evaluation`。
- **完整句子：Sentence case，末尾加句号。** 仅句首词首字母大写，其余使用正常句中大小写；保留专有名词、缩写和大小写敏感标识符，例如 `ImageNet`、`BERT`、`mAP`、`ResNet-50`。不得把它们强制小写。
- 标题含有 `of`、`with` 等介词或动名词，并不等于完整句子；按实际语法判断。例如 `Comparison of Model Accuracy` 是名词性短语，`Model accuracy improves with more training data.` 是完整句子。

## LaTeX 字符与数学公式

默认输出可粘贴到 LaTeX `\caption{...}` 中的内容，但不包裹 `\caption{}`。

- **先保护数学片段，再处理普通文本。** 保持 `$...$`、`$$...$$`、`\(...\)`、`\[...\]` 中的公式及定界符原样，包括其中的大小写、空格、下划线、百分号和 LaTeX 命令。不得翻译、改写或转义公式内部字符。
- 普通文本中的未转义特殊字符按 LaTeX 规则处理：`%` → `\%`，`_` → `\_`，`&` → `\&`，`#` → `\#`，字面量 `{`、`}` → `\{`、`\}`；字面量 `$` → `\$`，`~` → `\textasciitilde{}`，`^` → `\textasciicircum{}`，字面量反斜杠 → `\textbackslash{}`。
- 已有的 `\%`、`\_`、`\&` 等转义及有效 LaTeX 命令保持原样，避免重复转义。命令参数中的普通文本可润色，命令名和结构保留。
- 若用户明确要求纯文本、Word 或其他非 LaTeX 格式，按指定格式输出，不额外插入 LaTeX 转义。

## 输出

- 默认只输出一个最终英文标题，不附解释、备选项、引号、Markdown 包装或代码块。
- 删除 `Figure 1:`、`Fig. 1.`、`Table 1:` 等编号前缀，只输出标题内容；保留具有实际含义的子图说明。
- 批量输入时按原顺序逐行输出，每个标题一行；仅在用户明确要求时提供编号、对照、多个版本或解释。
- 输出前检查：含义准确、术语一致、语法分类正确、大小写与句末标点匹配、普通文本转义完整、数学片段未改动。无需为普通标题优化联网检索。

## 示例

以下示例展示转换规则，实际回复只包含对应的英文标题。

输入（图）：所提方法的整体架构

输出：Overall Architecture of the Proposed Method

输入（表）：在 CIFAR-10 上与基线方法的比较

输出：Comparison with Baseline Methods on CIFAR-10

输入（表）：注意力模块的消融实验

输出：Ablation Study on the Attention Module

输入（图）：随着训练数据增加，模型准确率提高。

输出：Model accuracy improves with more training data.

输入（表）：当 $r=10\%$ 时，model_v2 与 A&B 的准确率对比

输出：Accuracy Comparison of model\_v2 and A\&B at $r=10\%$

输入（图）：在 10% 标签噪声下，$\alpha_i$ 对准确率的影响

输出：Effect of $\alpha_i$ on Accuracy under 10\% Label Noise
