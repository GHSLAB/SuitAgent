# 文档处理强制规范

**版本**: 1.0
**状态**: 生效中
**最后更新**: 2025-11-20

## 📖 目的

本文档规定了SuitAgent系统中所有文档处理任务的强制执行标准，确保MCP工具的正确使用和输出文件的规范性。

## 🚨 核心原则

### 1. MCP工具使用原则

**绝对禁止**：
- ❌ **严禁绕过MCP直接编写Python脚本**
- ❌ **严禁绕过MCP直接调用API**
- ❌ **严禁绕过MCP使用第三方工具**

**必须遵循**：
- ✅ **必须通过Claude Code的MCP工具调用**
- ✅ **必须使用已配置的MCP服务**
- ✅ **必须遵循MCP通信协议**

### 2. 文档处理流程

所有文档处理必须通过对应的Agent执行：

| 文档类型 | 强制执行Agent | MCP工具 | 输出格式 |
|----------|---------------|---------|----------|
| **PDF文档** | DocAnalyzer | mineru.parse_documents | Markdown |
| **图片文件** | DocAnalyzer | mineru.parse_documents | Markdown |
| **Word文档** | DocAnalyzer | mineru.parse_documents | Markdown |
| **其他文档** | DocAnalyzer | mineru.parse_documents | Markdown |

## 📁 输出文件规范

### 严格要求

**必须生成**：
- ✅ **一个同名Markdown文件**（与原文档同名，扩展名为.md）

**严禁生成**：
- ❌ **JSON文件**（包括结构化数据、配置文件等）
- ❌ **图片目录**（包括提取的图片文件夹）
- ❌ **布局信息文件**（layout.json等）
- ❌ **内容列表文件**（content_list.json等）
- ❌ **处理报告文件**
- ❌ **临时文件或缓存文件**

### 输出位置规范

```
输入文件: /path/to/document.pdf
输出文件: /path/to/document.md （同目录，同名）
```

**命名规则**：
- 保持原始文件名不变
- 仅修改扩展名为 `.md`
- 不得添加任何前缀或后缀

### Markdown文件内容规范

**标准模板**：

```markdown
# [文件名] 解析结果

## 关键信息提取
- 字段1: 值1
- 字段2: 值2
- ...（根据文档类型提取结构化信息）
```

**重要**：
- ✅ **只包含结构化信息**
- ❌ **不要包含原始OCR文本**
- ❌ **不要包含技术说明**
- ❌ **不要包含其他无关内容**

## 🔧 MCP配置要求

### mineru MCP配置

当前系统中mineru的配置：

```json
{
  "mcpServers": {
    "mineru": {
      "command": "~/Library/Python/3.13/bin/mineru-mcp",
      "env": {
        "MINERU_API_KEY": "已配置的有效密钥",
        "MINERU_API_BASE": "https://mineru.net",
        "OUTPUT_DIR": "./",
        "OUTPUT_IN_SAME_DIR": "true",
        "KEEP_FILENAME": "true"
      }
    }
  }
}
```

**配置说明**：
- `OUTPUT_IN_SAME_DIR`: "true" - 在原文件同目录输出
- `KEEP_FILENAME`: "true" - 保持原文件名，仅改扩展名

## ⚙️ 执行标准

### Agent调用规范

**DocAnalyzer Agent工作流**：

1. **接收文档路径**
2. **调用mineru MCP工具**：
   - 工具：`mineru.parse_documents`
   - 参数：`enable_ocr=true`, `language="ch"`
3. **接收解析结果**
4. **生成标准Markdown文件**
5. **清理临时文件**
6. **返回完成状态**

**严禁操作**：
- 不得在Agent中编写Python调用代码
- 不得直接使用mineru API
- 不得生成额外格式的输出文件

### 错误处理

**失败处理流程**：
1. 记录错误信息
2. 保持原始文件不变
3. 报告具体的失败原因
4. 建议替代方案

## 📋 质量检查清单

每次文档处理后必须验证：

**文件检查**：
- [ ] 只生成了一个Markdown文件
- [ ] 文件名与原文档一致（扩展名为.md）
- [ ] 文件位置在原文件同目录

**内容检查**：
- [ ] 包含结构化的关键信息
- [ ] 包含原始OCR文本
- [ ] 包含技术说明信息
- [ ] 内容完整可读

**规范检查**：
- [ ] 没有生成JSON文件
- [ ] 没有生成图片目录
- [ ] 没有生成布局文件
- [ ] 没有生成其他格式文件

## 🚫 违规后果

**违规行为**：
- 绕过MCP直接调用API
- 生成多余的文件格式
- 不遵循输出规范
- 创建复杂的处理流程

**处理措施**：
1. 立即停止违规操作
2. 清理所有违规生成的文件
3. 重新按照规范执行
4. 记录违规行为以避免重复

## 📞 支持与维护

**相关文档**：
- [MinerU MCP配置](../mcp/mineru/README.md)
- [MinerU官方文档](../mcp/mineru/OFFICIAL_DOCUMENTATION.md)
- [系统架构文档](../../../docs/ARCHITECTURE.md)

**配置文件**：
- MCP配置：`.claude/mcp.json`
- MinerU配置：`.claude/mcp/mineru/`

---

**注**：本规范为强制执行标准，所有SuitAgent系统中的文档处理任务必须严格遵守。