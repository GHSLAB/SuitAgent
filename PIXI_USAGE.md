# Pixi 依赖管理指南

本指南说明如何使用 Pixi 来管理 SuitAgent 项目的 Python 依赖。

## 🎯 Pixi 简介

Pixi 是一个现代化的 Python 包管理工具，提供以下优势：
- **快速安装**: 比 pip 快 3-10 倍
- **环境隔离**: 自动创建和管理虚拟环境
- **锁定依赖**: 自动生成 `pixi.lock` 文件，确保环境一致性
- **多平台支持**: 自动处理不同操作系统的依赖
- **系统依赖管理**: 支持管理系统和编译依赖

## 📦 安装 Pixi

### macOS
```bash
brew install pixi
```

### Windows
```powershell
powershell -c "irm https://pixi.sh/install.ps1 | iex"
```

### Linux
```bash
curl -fsSL https://pixi.sh/install.sh | sh
```

## 🚀 快速开始

### 1. 初始化项目
```bash
# 在项目根目录执行
pixi init
```

### 2. 安装依赖
```bash
# 安装生产依赖
pixi add pypdf>=3.17.0 pdfplumber>=0.10.0 reportlab>=4.0.0 pdf2image>=1.17.0

# 安装 OCR 依赖
pixi add pytesseract>=0.3.10

# 安装文档处理依赖
pixi add python-docx>=1.1.0 python-pptx>=0.6.21 openpyxl>=3.1.2

# 安装图像处理依赖
pixi add Pillow>=10.0.0

# 安装 XML/HTML 处理依赖
pixi add defusedxml>=0.7.1 lxml>=4.9.0

# 安装数据处理依赖
pixi add pandas>=2.0.0 PyYAML>=6.0.0

# 安装文档格式转换依赖
pixi add markdown>=3.5.0 html2text>=2020.1.16 markitdown>=0.2.0

# 安装开发依赖 (可选)
pixi add --dev pytest>=7.4.0 pytest-cov>=4.1.0 black>=23.0.0 flake8>=6.0.0 mypy>=1.5.0
```

### 3. 激活环境并运行
```bash
# 激活环境
pixi shell

# 运行 Python 脚本
python main.py

# 或直接运行命令 (自动激活环境)
pixi run python main.py
```

## 📋 依赖分类管理

### 按功能分组安装

```bash
# 1. PDF 处理组
pixi add "pypdf>=3.17.0" "pdfplumber>=0.10.0" "reportlab>=4.0.0" "pdf2image>=1.17.0"

# 2. OCR 识别组
pixi add "pytesseract>=0.3.10"

# 3. 文档处理组
pixi add "python-docx>=1.1.0" "python-pptx>=0.6.21" "openpyxl>=3.1.2"

# 4. 图像处理组
pixi add "Pillow>=10.0.0"

# 5. 数据处理组
pixi add "pandas>=2.0.0" "PyYAML>=6.0.0"

# 6. 格式转换组
pixi add "markdown>=3.5.0" "html2text>=2020.1.16" "markitdown>=0.2.0"
```

## 🔧 常用命令

### 环境管理
```bash
# 查看环境信息
pixi info

# 列出已安装的包
pixi list

# 更新所有包
pixi update

# 移除包
pixi remove <package-name>

# 清理环境
pixi clean
```

### 开发工作流
```bash
# 安装开发依赖
pixi add --dev black flake8 pytest

# 运行代码格式化
pixi run black .

# 运行代码检查
pixi run flake8 .

# 运行测试
pixi run pytest

# 运行类型检查
pixi run mypy .
```

### 锁定依赖
```bash
# 锁定当前依赖版本 (自动生成 pixi.lock)
pixi lock

# 更新锁文件
pixi update
```

## 📁 项目文件结构

使用 Pixi 后，项目结构如下：

```
suitagent/
├── pyproject.toml          # 项目配置和依赖
├── pixi.lock              # 锁定依赖版本 (自动生成)
├── .pixi/                 # Pixi 环境目录 (自动生成)
│   ├── manifest.toml      # 依赖清单
│   └── lock.toml          # 锁文件
├── src/                   # 源代码
├── tests/                 # 测试代码
└── docs/                  # 文档
```

## 🔗 系统依赖安装

Pixi 会自动处理 Python 包的依赖，但系统级依赖需要手动安装：

### macOS
```bash
# 安装 Tesseract OCR
brew install tesseract

# 安装 Poppler
brew install poppler

# 安装 Pandoc
brew install pandoc

# 安装 LibreOffice (可选)
brew install --cask libreoffice
```

### Ubuntu/Debian
```bash
sudo apt-get update
sudo apt-get install tesseract-ocr poppler-utils pandoc libreoffice
```

### Windows
1. 下载并安装 [Tesseract OCR](https://github.com/UB-Mannheim/tesseract/wiki)
2. 下载并安装 [Poppler](https://blog.alivate.com.au/install-poppler-windows/)
3. 下载并安装 [Pandoc](https://pandoc.org/installing.html)
4. 下载并安装 [LibreOffice](https://www.libreoffice.org/download/)

## 📊 性能对比

| 操作 | pip | pixi |
|------|-----|------|
| 首次安装 | ~5-10分钟 | ~1-3分钟 |
| 依赖解析 | 慢 | 快 |
| 环境切换 | 需要激活/取消激活 | 即时切换 |
| 锁文件 | 无 | 自动生成 |
| 多平台支持 | 需要额外配置 | 自动支持 |

## 🚀 高级功能

### 1. 自定义环境
```bash
# 创建开发环境
pixi env create --name dev

# 激活特定环境
pixi shell --name dev
```

### 2. 导出依赖
```bash
# 导出 requirements.txt
pixi export requirements

# 导出 conda 环境
pixi export conda
```

### 3. 任务自动化
```bash
# 运行自定义任务 (需要在 pyproject.toml 中配置)
pixi run test
pixi run lint
pixi run build
```

## 🔄 从 requirements.txt 迁移

如果你之前使用 `requirements.txt`，可以按以下步骤迁移：

1. **安装 Pixi** (见上方)
2. **初始化项目**
   ```bash
   pixi init
   ```
3. **从 requirements.txt 安装**
   ```bash
   pixi add -r requirements.txt
   ```
4. **更新代码** (如果需要)
   - 更新导入路径 (如果使用 src 布局)
   - 运行测试确保一切正常

## 🛠️ 故障排除

### 常见问题

1. **权限错误**
   ```bash
   # 如果遇到权限问题，尝试
   sudo chown -R $USER:$USER ~/.pixi
   ```

2. **依赖冲突**
   ```bash
   # 强制重新锁定依赖
   pixi lock --force
   ```

3. **环境损坏**
   ```bash
   # 重新创建环境
   pixi env create --force
   ```

### 获取帮助
```bash
# 查看所有可用命令
pixi --help

# 查看特定命令帮助
pixi add --help
pixi run --help
```

## 📚 资源链接

- [Pixi 官方文档](https://pixi.sh/)
- [Pixi GitHub 仓库](https://github.com/prefix-dev/pixi)
- [Pixi 社区讨论](https://github.com/prefix-dev/pixi/discussions)

---

使用 Pixi 可以大大提升 Python 项目的依赖管理效率！🚀