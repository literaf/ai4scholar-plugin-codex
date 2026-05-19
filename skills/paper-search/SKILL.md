---
name: paper-search
description: "Search academic papers across multiple platforms including arXiv, PubMed, Semantic Scholar, bioRxiv, medRxiv, and Google Scholar. Use when the user wants to find papers by keyword, topic, author, year range, or field. 当用户想搜索、查找、检索学术论文时使用。"
---

# Paper Search

Use the bundled `ai4scholar` MCP tools to search academic papers across six major platforms.

## Available Search Tools

| Tool | Platform | Best For |
|------|----------|----------|
| `search_arxiv` | arXiv | CS, physics, math, quantitative biology preprints |
| `search_pubmed` | PubMed | Biomedical and life sciences |
| `search_semantic` | Semantic Scholar | Cross-disciplinary, supports year filtering |
| `search_biorxiv` | bioRxiv | Biology preprints |
| `search_medrxiv` | medRxiv | Medical and health preprints |
| `search_google_scholar` | Google Scholar | Broadest coverage, citation counts |
| `search_semantic_authors` | Semantic Scholar | Find researchers by name |
| `search_semantic_snippets` | Semantic Scholar | Full-text snippet search |

## Workflow

1. Identify the user's research domain to choose the best platform(s).
2. Use `search_semantic` as the default for cross-disciplinary queries (supports year filtering like `2020-2024`).
3. For biomedical topics, prefer `search_pubmed` (supports date range and sort by relevance/date).
4. For preprints in biology or medicine, use `search_biorxiv` or `search_medrxiv`.
5. For broadest coverage with citation counts, use `search_google_scholar` (supports year_from/year_to).
6. For finding specific researchers, use `search_semantic_authors` then `get_semantic_author_papers`.

## Tips

- Start with a focused query. Refine if too many or too few results.
- Use `max_results` to control output volume (default 10).
- Semantic Scholar supports flexible year filters: `2019`, `2016-2020`, `2010-`, `-2015`.
- PubMed supports `sort="date"` for newest-first results and `min_date`/`max_date` for precise date ranges.
- Google Scholar supports `year_from` and `year_to` integer parameters.
- Present results in a structured format: title, authors, year, abstract snippet, and links.

## Example Queries

- "Search for recent papers on large language models" → `search_semantic(query="large language models", year="2023-")`
- "Find biomedical papers about CRISPR gene editing" → `search_pubmed(query="CRISPR gene editing")`
- "Look for physics preprints on quantum computing" → `search_arxiv(query="quantum computing")`
- "Find papers by Yann LeCun" → `search_semantic_authors(query="Yann LeCun")` then `get_semantic_author_papers`
