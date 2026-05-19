---
name: citation-analysis
description: "Explore citation graphs, find citing and referenced papers, discover author networks, and get paper recommendations. Use when the user wants to trace citations, find related work, explore research lineage, or get reading recommendations. 当用户想分析引用关系、追踪引文、发现相关论文或获取推荐时使用。"
---

# Citation Analysis

Use the `ai4scholar` MCP server tools to explore citation networks and get recommendations. These tools are available as MCP tool calls with the `mcp__ai4scholar__` prefix.

IMPORTANT: Always use the MCP tools listed below via tool calls. Do NOT use web search. The MCP server provides structured citation data directly.

## Available MCP Tools

| MCP Tool Call | Description |
|--------------|-------------|
| `mcp__ai4scholar__get_semantic_citations` | Get papers that cite a given paper |
| `mcp__ai4scholar__get_semantic_references` | Get papers referenced by a given paper |
| `mcp__ai4scholar__get_semantic_recommendations` | Recommend papers based on positive/negative examples |
| `mcp__ai4scholar__get_semantic_recommendations_for_paper` | Recommend similar papers from a single paper |
| `mcp__ai4scholar__get_semantic_author_papers` | Get all papers by an author |
| `mcp__ai4scholar__search_semantic_authors` | Find researchers by name |
| `mcp__ai4scholar__get_pubmed_citations` | Get citing papers from PubMed |
| `mcp__ai4scholar__get_pubmed_related` | Get related PubMed papers |

## Tool Parameters

### mcp__ai4scholar__get_semantic_citations / get_semantic_references
- `paper_id` (string, required): Paper ID (SHA, DOI:<doi>, ARXIV:<id>, PMID:<id>, etc.)
- `limit` (int, optional): Max results, default 100, max 1000
- `offset` (int, optional): Pagination offset, default 0

### mcp__ai4scholar__get_semantic_recommendations
- `positive_paper_ids` (list of strings, required): Papers the user likes
- `negative_paper_ids` (list of strings, optional): Papers to avoid
- `limit` (int, optional): Max recommendations, default 100

### mcp__ai4scholar__get_semantic_recommendations_for_paper
- `paper_id` (string, required): Paper identifier
- `limit` (int, optional): Max recommendations, default 100
- `pool` (string, optional): "recent" or "all-cs", default "recent"

## Examples

- "What papers cite this?" → call `mcp__ai4scholar__get_semantic_citations` with `{"paper_id": "DOI:10.1038/...", "limit": 50}`
- "Find similar papers" → call `mcp__ai4scholar__get_semantic_recommendations_for_paper` with `{"paper_id": "ARXIV:2301.00001"}`
- "Build a reading list from these papers" → call `mcp__ai4scholar__get_semantic_recommendations` with `{"positive_paper_ids": [...]}`
