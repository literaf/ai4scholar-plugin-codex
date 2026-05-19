---
name: paper-search
description: "Search academic papers across multiple platforms including arXiv, PubMed, Semantic Scholar, bioRxiv, medRxiv, and Google Scholar. Use when the user wants to find papers by keyword, topic, author, year range, or field. 当用户想搜索、查找、检索学术论文时使用。"
---

# Paper Search

Use the `ai4scholar` MCP server tools to search academic papers. These tools are available as MCP tool calls with the `mcp__ai4scholar__` prefix.

IMPORTANT: Always use the MCP tools listed below via tool calls. Do NOT use web search or manually call APIs. The MCP server handles authentication and API access automatically.

## Available MCP Tools

| MCP Tool Call | Platform | Best For |
|--------------|----------|----------|
| `mcp__ai4scholar__search_arxiv` | arXiv | CS, physics, math preprints |
| `mcp__ai4scholar__search_pubmed` | PubMed | Biomedical and life sciences |
| `mcp__ai4scholar__search_semantic` | Semantic Scholar | Cross-disciplinary, year filtering |
| `mcp__ai4scholar__search_biorxiv` | bioRxiv | Biology preprints |
| `mcp__ai4scholar__search_medrxiv` | medRxiv | Medical and health preprints |
| `mcp__ai4scholar__search_google_scholar` | Google Scholar | Broadest coverage, citation counts |
| `mcp__ai4scholar__search_semantic_authors` | Semantic Scholar | Find researchers by name |
| `mcp__ai4scholar__search_semantic_snippets` | Semantic Scholar | Full-text snippet search |

## Workflow

1. Identify the user's research domain to choose the best platform(s).
2. Call the appropriate MCP tool directly. Do NOT fall back to web search.
3. Use `mcp__ai4scholar__search_semantic` as the default for cross-disciplinary queries.
4. For biomedical topics, prefer `mcp__ai4scholar__search_pubmed`.
5. For preprints in biology or medicine, use `mcp__ai4scholar__search_biorxiv` or `mcp__ai4scholar__search_medrxiv`.
6. For broadest coverage with citation counts, use `mcp__ai4scholar__search_google_scholar`.
7. For finding specific researchers, use `mcp__ai4scholar__search_semantic_authors` then `mcp__ai4scholar__get_semantic_author_papers`.

## Tool Parameters

### mcp__ai4scholar__search_semantic
- `query` (string, required): Search keywords
- `year` (string, optional): Year filter, e.g. "2019", "2016-2020", "2010-", "-2015"
- `max_results` (int, optional): Max papers to return, default 10

### mcp__ai4scholar__search_arxiv
- `query` (string, required): Search keywords
- `max_results` (int, optional): Max papers to return, default 10

### mcp__ai4scholar__search_pubmed
- `query` (string, required): Search keywords
- `max_results` (int, optional): Max papers to return, default 10
- `sort` (string, optional): "relevance" or "date"
- `min_date` (string, optional): Format YYYY/MM/DD
- `max_date` (string, optional): Format YYYY/MM/DD

### mcp__ai4scholar__search_google_scholar
- `query` (string, required): Search keywords
- `max_results` (int, optional): Max papers to return, default 10
- `year_from` (int, optional): Start year
- `year_to` (int, optional): End year

## Examples

- "Search for recent papers on large language models" → call `mcp__ai4scholar__search_semantic` with `{"query": "large language models", "year": "2023-"}`
- "Find biomedical papers about CRISPR" → call `mcp__ai4scholar__search_pubmed` with `{"query": "CRISPR gene editing"}`
- "Look for physics preprints on quantum computing" → call `mcp__ai4scholar__search_arxiv` with `{"query": "quantum computing"}`
- "Find papers by Yann LeCun" → call `mcp__ai4scholar__search_semantic_authors` with `{"query": "Yann LeCun"}`
