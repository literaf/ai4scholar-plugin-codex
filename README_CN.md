# AI4Scholar Codex 插件

[English](README.md) | **中文**

为 [OpenAI Codex](https://openai.com/codex) 提供学术论文搜索、阅读、引用分析、自动标注引用和 AI 科研绘图能力的插件。

基于 [ai4scholar-mcp](https://github.com/literaf/ai4s-mcp) —— 覆盖 arXiv、PubMed、Semantic Scholar、bioRxiv、medRxiv 和 Google Scholar 的 28 个工具。

![License](https://img.shields.io/badge/license-MIT-blue.svg) ![Python](https://img.shields.io/badge/python-3.10+-blue.svg)

---

## Skills（技能）

| 技能 | 描述 |
|------|------|
| **paper-search** | 跨 6 个平台搜索论文，支持年份/日期/作者过滤 |
| **paper-reading** | 下载 PDF 并提取全文用于总结分析 |
| **citation-analysis** | 探索引用图谱、作者网络，获取论文推荐 |
| **auto-cite** | 自动为学术文本标注引用和参考文献 |
| **nano-draw** | AI 生成、编辑、矢量化科研图片 |

---

## 快速开始

### 前提条件

- 一个 AI4Scholar API 密钥，前往 [ai4scholar.net](https://ai4scholar.net) 获取
- **默认 SSE 模式无需安装任何 Python 包**

### 在 Codex 中安装

**方式一：本地插件（推荐）**

克隆此仓库，注册为 Codex 本地插件：

```bash
git clone https://github.com/literaf/ai4scholar-plugin-codex.git
```

编辑 `.mcp.json`，将 `<your-ai4scholar-api-key>` 替换为你的实际 API 密钥。

创建或编辑 `~/.agents/plugins/marketplace.json`：

```json
{
  "name": "local-plugins",
  "plugins": [
    {
      "name": "ai4scholar",
      "source": {
        "source": "local",
        "path": "/path/to/ai4scholar-plugin-codex"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_INSTALL"
      },
      "category": "Research"
    }
  ]
}
```

重启 Codex，在插件目录中安装即可。

**方式二：仓库级插件**

将插件复制到你的项目中：

```bash
cp -R /path/to/ai4scholar-plugin-codex ./plugins/ai4scholar
```

添加到 `$REPO_ROOT/.agents/plugins/marketplace.json`：

```json
{
  "name": "repo-plugins",
  "plugins": [
    {
      "name": "ai4scholar",
      "source": {
        "source": "local",
        "path": "./plugins/ai4scholar"
      },
      "policy": {
        "installation": "AVAILABLE",
        "authentication": "ON_INSTALL"
      },
      "category": "Research"
    }
  ]
}
```

### 在 Claude Code 中安装

**SSE 模式（无需安装）：**

```bash
claude mcp add ai4scholar --transport sse --url https://mcp.ai4scholar.net/sse --header "Authorization: Bearer <your-api-key>"
```

**本地模式（需要 pip install）：**

```bash
pip install ai4scholar-mcp
claude mcp add ai4scholar -- python -m ai4scholar_mcp.server
```

或使用 `.claude-plugin/plugin.json` 配置。

---

## 配置

### 默认：远程 SSE 模式（零安装）

插件默认使用托管的 SSE 服务器。只需编辑 `.mcp.json`，将 `<your-ai4scholar-api-key>` 替换为你从 [ai4scholar.net](https://ai4scholar.net) 获取的 API 密钥：

```json
{
  "mcpServers": {
    "ai4scholar": {
      "type": "sse",
      "url": "https://mcp.ai4scholar.net/sse",
      "headers": {
        "Authorization": "Bearer <your-ai4scholar-api-key>"
      }
    }
  }
}
```

开箱即用——不需要 Python、不需要 pip、不需要任何本地配置。

### 可选：本地模式（完整功能）

如需 PDF 下载功能（在校园网环境下可利用机构权限下载付费论文），切换到本地 stdio 模式：

```bash
pip install ai4scholar-mcp
```

然后编辑 `.mcp.json`：

```json
{
  "mcpServers": {
    "ai4scholar": {
      "type": "stdio",
      "command": "python",
      "args": ["-m", "ai4scholar_mcp.server"],
      "env": {
        "AI4SCHOLAR_API_KEY": "your-api-key"
      }
    }
  }
}
```

> **注意：** PDF 下载工具（`download_*`、`download_pdf_by_doi`）仅在本地模式（stdio）下可用。SSE 模式支持搜索、文本提取、自动引用和科研绘图。

---

## 工具（28 个）

| 平台 | 工具 | 能力 |
|------|------|------|
| **arXiv** | `search_arxiv`, `download_arxiv`, `read_arxiv_paper` | 搜索、下载 PDF、提取全文 |
| **PubMed** | `search_pubmed`, `get_pubmed_paper_detail`, `get_pubmed_citations`, `get_pubmed_related` | 搜索、详情、引用、相关论文 |
| **Semantic Scholar** | `search_semantic`, `download_semantic`, `read_semantic_paper`, `get_semantic_citations`, `get_semantic_references`, `search_semantic_authors`, `get_semantic_author_papers`, `get_semantic_recommendations`, `get_semantic_recommendations_for_paper`, `search_semantic_snippets` | 完整引用图谱和推荐 |
| **Google Scholar** | `search_google_scholar` | 广泛搜索，支持年份过滤 |
| **bioRxiv** | `search_biorxiv`, `download_biorxiv`, `read_biorxiv_paper` | 生物学预印本 |
| **medRxiv** | `search_medrxiv`, `download_medrxiv`, `read_medrxiv_paper` | 医学预印本 |
| **通用** | `download_pdf_by_doi` | 通过 DOI 下载任意论文 |
| **Auto-Cite** | `auto_cite` | AI 引用标注 |
| **Nano Draw** | `nano_generate`, `nano_edit`, `nano_vectorize` | AI 科研绘图和编辑 |

---

## 使用示例

```text
搜索最近关于大语言模型的论文。
阅读并总结 arXiv 论文 2301.00001。
哪些论文引用了 DOI:10.1038/s41586-024-07487-w？
为我的引言段落自动添加 IEEE 格式引用。
生成一个 Transformer 架构的示意图。
```

---

## 许可证

MIT 许可证。详见 [LICENSE](https://github.com/literaf/ai4s-mcp/blob/main/LICENSE)。
