# AI4Scholar Codex Plugin

**English** | [中文](README_CN.md)

A Codex plugin that brings academic paper search, reading, citation analysis, auto-citation, and AI scientific figure generation into [OpenAI Codex](https://openai.com/codex).

Powered by [ai4scholar-mcp](https://github.com/literaf/ai4s-mcp) — 28 tools across arXiv, PubMed, Semantic Scholar, bioRxiv, medRxiv, and Google Scholar.

![License](https://img.shields.io/badge/license-MIT-blue.svg) ![Python](https://img.shields.io/badge/python-3.10+-blue.svg)

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

## Quick Start

### Prerequisites

- An AI4Scholar API key from [ai4scholar.net](https://ai4scholar.net)
- **No Python installation required** — the plugin connects to the hosted SSE server

### Install in Codex

**Step 1: Clone the plugin**

```bash
git clone https://github.com/literaf/ai4scholar-plugin-codex.git ~/.codex/plugins/ai4scholar-plugin-codex
```

**Step 2: Register the marketplace in `~/.codex/config.toml`**

Add the following to your Codex config file:

```toml
[marketplaces.ai4scholar-local]
source_type = "local"
source = "~/.codex/plugins/ai4scholar-plugin-codex"

[plugins."ai4scholar@ai4scholar-local"]
enabled = true

[plugins."ai4scholar@ai4scholar-local".mcp_servers.ai4scholar]
enabled = true
```

**Step 3: Configure your API key**

Add the MCP server config with your API key to `~/.codex/config.toml`:

```toml
[mcp_servers.ai4scholar]
enabled = true
url = "https://mcp.ai4scholar.net/sse"

[mcp_servers.ai4scholar.http_headers]
Authorization = "Bearer <your-ai4scholar-api-key>"
```

**Step 4: Restart Codex**

The plugin should now appear in `/plugins`. You can use `@ai4scholar` or describe your task directly.

### Install in Claude Code

**SSE mode (no installation):**

```bash
claude mcp add ai4scholar --transport sse --url https://mcp.ai4scholar.net/sse --header "Authorization: Bearer <your-api-key>"
```

**Local mode (requires pip install):**

```bash
pip install ai4scholar-mcp
claude mcp add ai4scholar -- python -m ai4scholar_mcp.server
```

---

## Configuration

### Default: Remote SSE Mode (Zero Installation)

The plugin uses the hosted SSE server by default. Just edit `.mcp.json` and replace `<your-ai4scholar-api-key>` with your API key from [ai4scholar.net](https://ai4scholar.net):

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

This works out of the box — no Python, no pip, no local setup needed.

### Optional: Local Mode (Full Features)

For PDF download support (especially useful on campus networks with institutional access), switch to local stdio mode:

```bash
pip install ai4scholar-mcp
```

Then edit `.mcp.json`:

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

> **Note:** PDF download tools (`download_*`, `download_pdf_by_doi`) are only available in local/stdio mode. SSE mode supports search, text extraction, auto-cite, and nano-draw.

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

## License

MIT License. See [LICENSE](https://github.com/literaf/ai4s-mcp/blob/main/LICENSE) for details.
