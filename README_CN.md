<p align="center">
  <img src="plugins/ai4scholar/assets/logo.svg" width="120" alt="AI4Scholar Logo">
</p>

# AI4Scholar Codex 插件

[English](README.md) | **中文**

为 [OpenAI Codex](https://openai.com/codex) 提供学术论文搜索、阅读、引用分析、自动标注引用和 AI 科研绘图能力的插件。

基于 [ai4scholar-mcp](https://github.com/literaf/ai4s-mcp) —— 覆盖 arXiv、PubMed、Semantic Scholar、bioRxiv、medRxiv 和 Google Scholar 的 28 个工具。

![License](https://img.shields.io/badge/license-MIT-blue.svg)

---

## 快速开始（3 步完成）

### 前提条件

- 一个 AI4Scholar API 密钥，前往 [ai4scholar.net](https://ai4scholar.net) 获取
- **无需安装 Python** —— 插件直接连接远程托管服务器

### 第 1 步：添加 Marketplace

在 Codex 中添加插件市场。可以：

- 通过 Codex UI：设置 → 插件 → 添加 Marketplace → 粘贴 `https://github.com/literaf/ai4scholar-plugin-codex.git`
- 或手动编辑 `~/.codex/config.toml`：

```toml
[marketplaces.ai4scholar-plugins]
source_type = "git"
source = "https://github.com/literaf/ai4scholar-plugin-codex.git"
```

### 第 2 步：启用插件

通过 Codex UI 启用（设置 → 插件 → AI4Scholar → 启用），或添加到 `~/.codex/config.toml`：

```toml
[plugins."ai4scholar@ai4scholar-plugins"]
enabled = true
```

### 第 3 步：配置 API 密钥

在 `~/.codex/config.toml` 中添加：

```toml
[plugins."ai4scholar@ai4scholar-plugins".mcp_servers.ai4scholar]
enabled = true
default_tools_approval_mode = "auto"

[plugins."ai4scholar@ai4scholar-plugins".mcp_servers.ai4scholar.env]
AI4SCHOLAR_API_KEY = "sk-user-你的密钥"
```

重启 Codex 即可。插件会出现在 `/plugins` 中，使用 `@ai4scholar` 调用。

---

## 技能

| 技能 | 描述 |
|------|------|
| **paper-search** | 跨 6 个平台搜索论文，支持年份/日期/作者过滤 |
| **paper-reading** | 下载 PDF 并提取全文用于总结分析 |
| **citation-analysis** | 探索引用图谱、作者网络，获取论文推荐 |
| **auto-cite** | 自动为学术文本标注引用和参考文献 |
| **nano-draw** | AI 生成、编辑、矢量化科研图片 |

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

## 也支持 Claude Code

```bash
claude mcp add ai4scholar --transport sse --url https://mcp.ai4scholar.net/sse --header "Authorization: Bearer <your-api-key>"
```

---

## 许可证

MIT 许可证。详见 [LICENSE](https://github.com/literaf/ai4s-mcp/blob/main/LICENSE)。
