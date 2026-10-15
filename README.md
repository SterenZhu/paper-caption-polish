# paper-caption-polish

将中文论文图题、表题翻译成简洁规范的英文，或润色已有英文标题。适合论文写作时处理架构图、方法概览、性能比较、消融实验等图表标题。

## 功能

- **翻译与润色**：保留研究对象、比较关系、实验条件、指标、方法名和数值，精简冗余措辞。
- **大小写与标点**：名词性短语使用 Title Case，末尾不加句号；完整句子使用 Sentence case，末尾加句号。
- **LaTeX 处理**：转义普通文本中的特殊字符，保留数学公式、已有转义及有效命令。
- **批量处理**：按输入顺序逐行返回英文标题。
- **按需调整格式**：用户指定的期刊、会议模板和输出格式优先；可要求纯文本或 Word 格式。

默认只输出最终英文标题，不附解释或备选项，也不保留 `Figure 1:`、`Table 1:` 等编号前缀。

## 安装

将本仓库作为 `paper-caption-polish` 文件夹放入本地 Codex Skills 目录，使目录结构如下：

```text
~/.codex/skills/paper-caption-polish/
├── SKILL.md
└── agents/
    └── openai.yaml
```

Windows PowerShell 示例（目标目录尚不存在时）：

```powershell
git clone https://github.com/SterenZhu/paper-caption-polish.git "$env:USERPROFILE\.codex\skills\paper-caption-polish"
```

也可以下载仓库 ZIP，解压后将包含 `SKILL.md` 的文件夹命名为 `paper-caption-polish`，放入上述目录。若已安装，请在替换前保留自己的修改。

## 使用

在对话中明确调用 Skill，并给出图表类型和标题：

```text
使用 $paper-caption-polish 翻译这个图标题：所提方法的整体架构
```

输出：

```text
Overall Architecture of the Proposed Method
```

批量处理时，每行提供一个标题：

```text
使用 $paper-caption-polish，按原顺序逐行输出：
图：所提方法的整体架构
表：在 CIFAR-10 上与基线方法的比较
表：注意力模块的消融实验
```

如需特定格式，可直接补充要求，例如“输出纯文本，用于 Word”或“按目标期刊要求，所有标题使用 sentence case”。

## 示例

| 输入 | 输出 |
| --- | --- |
| 图：所提方法的整体架构 | Overall Architecture of the Proposed Method |
| 表：在 CIFAR-10 上与基线方法的比较 | Comparison with Baseline Methods on CIFAR-10 |
| 表：注意力模块的消融实验 | Ablation Study on the Attention Module |
| 图：随着训练数据增加，模型准确率提高。 | Model accuracy improves with more training data. |

包含数学公式和特殊字符时：

输入：

```text
图：在 10% 标签噪声下，$\alpha_i$ 对准确率的影响
```

输出：

```latex
Effect of $\alpha_i$ on Accuracy under 10\% Label Noise
```

默认输出的是可放入 `\caption{...}` 内的内容，不包含外层命令。公式中的字符保持原样；普通文本中的 `%`、`_`、`&` 等按 LaTeX 规则转义，已有转义不会重复处理。

## 适用范围

本 Skill 专注于论文图题和表题的语言与格式处理。论文主标题、正文润色及图表绘制不在其范围内。标题优化以输入内容为依据，不添加未提供的实验结果、因果关系、优越性或统计显著性。

完整规则见 [SKILL.md](SKILL.md)，Codex 界面配置见 [agents/openai.yaml](agents/openai.yaml)。

## 参考与致谢

本 Skill 的提示词参考了 [Leey21/awesome-ai-research-writing](https://github.com/Leey21/awesome-ai-research-writing) 项目中的提示词，感谢原作者的整理与分享。
