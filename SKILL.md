---
name: spreadsheet-ops
description: Spreadsheet processing and analysis for CSV/Excel; trigger when users ask to merge/clean tabular data, run statistics, add/edit Excel formulas, apply formatting, generate charts, or force workbook recalculation.
license: MIT
skill-author: AIPOCH
---

## When to Use

- You need to merge multiple CSV/Excel files into a single dataset and align columns.
- You need to clean tabular data (normalize headers, deduplicate rows, resolve conflicts) before downstream use.
- You need to perform data analysis/statistics on CSV/Excel (summaries, distributions, group-by metrics).
- You need to add or edit formulas in an Excel workbook (including applying formulas across ranges).
- You need to apply Excel formatting (including conditional formatting), generate charts, or force formula recalculation.

## Key Features

- **CSV/Excel merge & cleaning**: combine files, normalize column names, deduplicate, and resolve conflicts.
- **CSV/Excel analysis**: compute descriptive statistics and analysis reports.
- **Excel-only formula operations**: create/edit formulas and apply them to specified ranges.
- **Excel-only formatting**: apply cell styles and conditional formatting rules.
- **Excel-only visualization**: build charts from worksheet ranges.
- **Excel-only recalculation**: set workbook to full recalculation (recalc flag) to ensure formulas update.

## Dependencies

- Python **3.x**
- Project Python dependencies are defined by the repository environment (e.g., `requirements.txt` / lockfile if present).  
  *(No explicit versions were provided in the source document.)*

## Example Usage

> The following commands assume you are in the repository root and have a Python environment available.

### 1) Merge files (CSV/Excel)

```bash
python scripts/merge_files.py
```

### 2) Analyze data (CSV/Excel)

```bash
python scripts/analyze_data.py
```

### 3) Apply formulas (Excel only)

```bash
python scripts/apply_formulas.py
```

### 4) Apply formatting (Excel only)

```bash
python scripts/apply_formatting.py
```

### 5) Build charts (Excel only)

```bash
python scripts/build_charts.py
```

### 6) Force workbook recalculation (Excel only)

```bash
python scripts/recalc_workbook.py
```

## Implementation Details

- **Workflow**
  1. Confirm inputs/outputs: file paths, file formats (CSV vs Excel), worksheet names, and target ranges.
  2. Choose the task type: merge, analysis, formula, formatting, chart, or recalculation.
  3. Run the corresponding script and configure parameters in `CONFIG` (as used by the scripts).
  4. Produce output files and any generated reports.

- **Task boundaries**
  - **CSV/Excel supported**: merging/cleaning, data analysis.
  - **Excel only**: formula creation/editing, formatting, chart visualization, and recalculation.

- **Key parameters to clarify (priority)**
  - Input type: CSV or Excel; single file or multiple files.
  - Worksheet names and cell ranges to operate on (Excel).
  - Whether formulas/formatting/charts must preserve original styles.
  - Desired output format: CSV / Excel / JSON / Parquet.

- **Standards / constraints**
  - Python file I/O must explicitly specify `encoding='utf-8'`.
  - `json.dump(...)` must set `ensure_ascii=False`.

- **Reference documentation (optional)**
  - Column name matching & normalization: `references/column-matching.md`
  - Deduplication & conflict resolution: `references/dedup-conflict.md`
  - Large files & performance: `references/large-files.md`
  - Formula design & ranges: `references/formulas.md`
  - Formatting & conditional formatting: `references/formatting.md`
  - Data analysis & statistics: `references/analysis.md`
  - Charts & visualization: `references/visualization.md`
  - Formula recalculation: `references/recalc.md`

## When Not to Use

- 缺少完成任务所必需的输入文件、标识符、参数或上下文时，不要继续，先要求用户补充。
- 用户要求超出本 skill 已声明范围的推断、外部操作或权限时，不要自行假设具备这些能力。
- 需要覆盖已有结果、执行高成本批量操作或扩大任务范围时，不要直接继续，先和用户确认。

## Required Inputs

| 字段 | 必填 | 格式/来源 | 示例 | 缺失时处理 |
|---|---|---|---|---|
| 用户任务说明 | 是 | 文本 | 研究问题、写作目标、分析目标 | 缺失时停止并要求补充 |
| 主要输入材料 | 视任务而定 | 文本、文件路径、ID、表格或文献 | PMID、PDF、CSV、DOCX、主题词等 | 明确指出缺少哪类材料 |
| 输出偏好 | 否 | 文本 | 语言、格式、目标期刊、模板 | 未提供时采用 skill 默认格式 |

## Output Contract

- 主输出：与本 skill 目标一致的结构化结果或目标文件。
- 可选输出：中间检查说明、问题清单、补充建议或生成文件路径。
- 格式要求：除非用户另有要求，优先返回稳定、可复核的 Markdown 或 JSON；若 skill 自带脚本要求固定格式，则按该格式输出。
- 若为部分完成：必须显式标注 PARTIAL，并说明哪些步骤已完成、哪些步骤未完成。

## Failure Handling

- 缺少关键输入时：明确指出缺少的字段、文件或标识符，并暂停继续。
- 脚本、模板或资源执行失败时：报告失败步骤、可能原因和恢复建议，不要静默降级。
- 只能部分完成时：先返回已验证部分，再列出剩余阻塞项和建议的下一步。

## User Checkpoints

- 在执行批量处理、覆盖文件、长耗时检索或多阶段生成前，先向用户确认范围和输出格式。
- 在关键判断存在歧义、证据不足或需要进入下一阶段前，先向用户确认是否继续。

## Quick Validation

- 检查本 skill 依赖的关键脚本、模板或参考资料路径是否存在。
- 检查最终输出是否包含本任务约定的核心字段、章节或文件。
- 检查结果中是否清楚标注假设、限制和未完成项。
