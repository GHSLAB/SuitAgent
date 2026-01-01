---
description: "SuitAgent Agent与目录映射配置 - 单一真实源，定义所有Agent的输出目录映射关系"
category: "agent-mappings"
version: "1.0"
---

# SuitAgent Agent与目录映射配置

本文件定义了SuitAgent系统中所有10个Agent的输出目录映射关系，按四层架构组织。

## 📊 Agent分层架构映射

### 📥 输入层 (Input Layer) - 文档数据采集

#### DocAnalyzer
- **主要输出目录**：`02 - 📄 案件分析`
- **次要输出目录**：
  - `04 - 📤 客户提供`
  - `07 - 📥 对方提交`
  - `08 - 🏛️ 法院送达`
  - `09 - 🎯 庭审笔录`
- **功能说明**：分析各类法律文档，提取结构化信息

#### EvidenceAnalyzer
- **主要输出目录**：`05 - 📎 证据材料`
- **次要输出目录**：`07 - 📥 对方提交`
- **功能说明**：深度分析证据材料，评估证明力

### 🔍 分析层 (Analysis Layer) - 智能分析与研究

#### IssueIdentifier
- **主要输出目录**：`03 - 🔍 法律研究`
- **功能说明**：识别和归类争议焦点

#### Researcher
- **主要输出目录**：`03 - 🔍 法律研究`
- **次要输出目录**：`11 - 📚 参考文件`
- **功能说明**：法条解读、判例检索、法律适用研究

#### Strategist
- **主要输出目录**：`02 - 📄 案件分析`
- **功能说明**：SWOT分析、策略制定、风险评估

### 📝 输出层 (Output Layer) - 文书生成与报告

#### Writer
- **主要输出目录**：`06 - 📝 法律文书`
- **次要输出目录**：`01 - 🤝 委托材料`
- **功能说明**：起草各类法律文书

#### Reporter
- **主要输出目录**：`10 - 📊 综合报告`
- **功能说明**：整合所有内容，生成综合报告

#### Summarizer
- **主要输出目录**：`10 - 📊 综合报告`
- **次要输出目录**：`09 - 🎯 庭审笔录`
- **功能说明**：生成各类摘要和简报

### ⚙️ 支持层 (Support Layer) - 质量保证与辅助

#### Scheduler
- **主要输出目录**：`00 - 📅 日程管理`
- **次要输出目录**：`08 - 🏛️ 法院送达`
- **功能说明**：期限管理、工时统计

#### Reviewer
- **主要输出目录**：无（不直接输出文件）
- **功能说明**：智能审查器，质量把关专家

## 🔄 目录反向映射（目录 → Agent）

| 目录 | 输出Agent |
|------|----------|
| **00 - 📅 日程管理** | Scheduler |
| **01 - 🤝 委托材料** | Writer |
| **02 - 📄 案件分析** | DocAnalyzer, Strategist |
| **03 - 🔍 法律研究** | IssueIdentifier, Researcher |
| **04 - 📤 客户提供** | DocAnalyzer |
| **05 - 📎 证据材料** | EvidenceAnalyzer |
| **06 - 📝 法律文书** | Writer |
| **07 - 📥 对方提交** | DocAnalyzer, EvidenceAnalyzer |
| **08 - 🏛️ 法院送达** | DocAnalyzer, Scheduler |
| **09 - 🎯 庭审笔录** | DocAnalyzer, Summarizer |
| **10 - 📊 综合报告** | Summarizer, Reporter |
| **11 - 📚 参考文件** | Researcher |

## 📝 使用说明

### 映射规则
- **primary**：主要输出目录
- **secondary**：次要输出目录（可选，列表）
- **note**：特殊说明（可选）

### 目录层级对应
```
输入层 (Input Layer) → 02, 04, 05, 07, 08, 09
分析层 (Analysis Layer) → 02, 03, 11
输出层 (Output Layer) → 01, 06, 10
支持层 (Support Layer) → 00, 08
```

## 🔄 变更历史

| 版本 | 日期 | 更新内容 |
| :--- | :--- | :--- |
| v1.0 | 2026-01-01 | 迁移到Claude Code Rules架构，从YAML配置文件转换为Markdown格式，保持所有Agent映射关系不变 |

---

*本文档是SuitAgent Agent与目录映射的核心配置文件，自动加载到项目记忆中。*