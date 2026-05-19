<p align="center">
  <img src="plugins/ai4scholar/assets/logo.svg" width="120" alt="AI4Scholar Logo">
</p>

# AI4Scholar Codex Plugin

**English** | [中文](README_CN.md)

A Codex plugin that brings academic paper search, reading, citation analysis, auto-citation, and AI scientific figure generation into [OpenAI Codex](https://openai.com/codex).

Powered by [ai4scholar-mcp](https://github.com/literaf/ai4s-mcp) — 28 tools across arXiv, PubMed, Semantic Scholar, bioRxiv, medRxiv, and Google Scholar.

![License](https://img.shields.io/badge/license-MIT-blue.svg)

---

## Quick Start (3 Steps)

### Prerequisites

- An AI4Scholar API key from [ai4scholar.net](https://ai4scholar.net)
- No Python installation required — the plugin connects to the hosted remote server

### Step 1: Add Marketplace

In Codex, add the plugin marketplace. You can either:

- Use the Codex UI: Settings → Plugins → Add Marketplace → paste `https://github.com/literaf/ai4scholar-plugin-codex.git`
- Or manually add to `~/.codex/config.toml`:

```toml
[marketplaces.ai4scholar-plugins]
source_type = "git"
source = "https://github.com/literaf/ai4scholar-plugin-codex.git"
```

### Step 2: Enable the Plugin

Enable it via Codex UI (Settings → Plugins → AI4Scholar → Enable), or add to `~/.codex/config.toml`:

```toml
[plugins."ai4scholar@ai4scholar-plugins"]
enabled = true
```

### Step 3: Configure Your API Key

Add your API key to `~/.codex/config.toml`:

```toml
[plugins."ai4scholar@ai4scholar-plugins".mcp_servers.ai4scholar]
enabled = true
default_tools_approval_mode = "auto"

[plugins."ai4scholar@ai4scholar-plugins".mcp_servers.ai4scholar.env]
AI4SCHOLAR_API_KEY = "sk-user-your-api-key-here"
```

Then restart Codex. The plugin will appear in `/plugins` and you can use `@ai4scholar` to invoke it.

---

## Skills

| Skill | Description |
|-------|-------------|
| **paper-search** | Search papers across 6 platforms with year/date/author filtering |
| **paper-reading** | Download PDFs and extract full text for summarization |
| **citation-analysis** | Explore citation graphs, author networks, and get recommendations |
| **auto-cite** | Automatically annotate academic text with citations and references |
| **nano-draw** | Generate, edit, and vectorize scientific figures with AI |

---

## Tools (28)

| Platform | Tools | Capabilities |
|----------|-------|-------------|
| **arXiv** | `search_arxiv`, `download_arxiv`, `read_arxiv_paper` | Search, download PDF, extract text |
| **PubMed** | `search_pubmed`, `get_pubmed_paper_detail`, `get_pubmed_citations`, `get_pubmed_related` | Search, detail, citations, related |
| **Semantic Scholar** | `search_semantic`, `download_semantic`, `read_semantic_paper`, `get_semantic_citations`, `get_semantic_references`, `search_semantic_authors`, `get_semantic_author_papers`, `get_semantic_recommendations`, `get_semantic_recommendations_for_paper`, `search_semantic_snippets` | Full citation graph and recommendations |
| **Google Scholar** | `search_google_scholar` | Broad search with year filtering |
| **bioRxiv** | `search_biorxiv`, `download_biorxiv`, `read_biorxiv_paper` | Biology preprints |
| **medRxiv** | `search_medrxiv`, `download_medrxiv`, `read_medrxiv_paper` | Medical preprints |
| **General** | `download_pdf_by_doi` | Download any paper by DOI |
| **Auto-Cite** | `auto_cite` | AI citation annotation |
| **Nano Draw** | `nano_generate`, `nano_edit`, `nano_vectorize` | AI figure generation and editing |

---

## Usage Examples

```text
Search for recent papers on large language models.
Read and summarize arXiv paper 2301.00001.
What papers cite DOI:10.1038/s41586-024-07487-w?
Auto-cite my introduction paragraph with IEEE references.
Generate a diagram showing transformer architecture.
```

---

## Also Works With Claude Code

```bash
claude mcp add ai4scholar --transport sse --url https://mcp.ai4scholar.net/sse --header "Authorization: Bearer <your-api-key>"
```

---

## License

MIT License. See [LICENSE](https://github.com/literaf/ai4s-mcp/blob/main/LICENSE) for details.
