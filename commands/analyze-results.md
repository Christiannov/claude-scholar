---
name: analyze-results
description: Analyze experimental results and generate a strict analysis bundle with rigorous statistics, real scientific figures, and figure interpretation guidance. Triggers data-analyst agent to perform academic-grade analysis.
args:
  - name: data_path
    description: Path to experimental results (CSV, JSON, logs, or directory)
    required: false
  - name: analysis_type
    description: Type of analysis (full, comparison, ablation, visualization)
    required: false
    default: full
tags: [Research, Analysis, Statistics, Visualization]
---

# Analyze Results Command

快速启动 **strict analysis bundle** 生成流程。

## 目标

此命令用于生成：
- 严谨统计分析
- 真实科研图
- 图表说明与 interpretation checklist
- 可供后续 `results-report` 复用的分析底座

此命令**不负责**生成论文 `Results` 草稿。

## 使用方法

### 基本用法

```bash
/analyze-results
```

### 指定数据路径

```bash
/analyze-results path/to/results.csv
```

### 指定分析类型

```bash
/analyze-results path/to/results/ comparison
```

## 分析类型

| 类型 | 说明 | 输出 |
|------|------|------|
| `full` | 完整严格分析（默认） | analysis report + stats appendix + figure catalog + real figures |
| `comparison` | 模型对比 | 主对比图 + 显著性检验 + effect size |
| `ablation` | 消融实验 | 组件贡献分析 + supporting figure |
| `visualization` | 图表优先 | 实图生成 + caption/interpretation requirements |

## 工作流程

1. **数据定位** - 找到实验结果文件、日志与比较对象
2. **数据验证** - 检查 comparability、样本单位、缺失项
3. **严格统计** - 执行假设检查、显著性检验、effect size、多重比较校正
4. **生成真实图表** - 优先生成实际科研图，而不是只写 specs
5. **输出分析 bundle** - 写出分析报告、统计附录、图表目录
6. **显式报告 blocker** - 输入不完整时必须指出原因

## 输出文件

命令执行后默认生成：

```text
analysis-output/
├── analysis-report.md      # 关键发现、比较结论、限制
├── stats-appendix.md       # 完整统计附录
├── figure-catalog.md       # 每张图的用途、caption要求、解释清单
└── figures/                # 真实科研图
```

## 示例

### 示例 1：分析单个实验结果目录

```bash
/analyze-results experiments/model_family/
```

**输出**：
- 主指标的 descriptive + inferential analysis
- 至少一张主图
- 统计附录
- figure catalog

### 示例 2：对比多个模型

```bash
/analyze-results experiments/comparison/ comparison
```

**输出**：
- 多模型性能对比图
- 显著性检验（含 correction）
- effect size
- 图后 interpretation checklist

### 示例 3：消融实验分析

```bash
/analyze-results experiments/ablation/ ablation
```

**输出**：
- 各组件贡献分析
- supporting ablation figure
- 稳定性 / 解释边界

## 集成说明

此命令触发 **data-analyst agent**，该 agent 会：
1. 使用 **results-analysis skill** 的方法论
2. 优先生成真实科研图
3. 保持统计完整性与可复现性
4. 为后续 `results-report` 提供可信输入

## 注意事项

- 至少提供可比较的原始指标或 seed-level 结果
- 对多组比较需显式处理 multiple comparisons
- 若无法生成真实图表，必须说明缺失字段或阻塞点
- 该命令不会产出 `results-draft.md`

## 相关资源

- **Skill**: `results-analysis`
- **Agent**: `data-analyst`
- **Follow-up Skill**: `results-report`
