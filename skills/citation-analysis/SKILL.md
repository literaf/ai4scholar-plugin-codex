---
name: citation-analysis
description: "Explore citation graphs, find citing and referenced papers, discover author networks, and get paper recommendations. Use when the user wants to trace citations, find related work, explore research lineage, or get reading recommendations. 当用户想分析引用关系、追踪引文、发现相关论文或获取推荐时使用。"
---

# Citation Analysis

Use the bundled `ai4scholar` MCP tools to explore citation networks, author graphs, and get paper recommendations.

## Available Tools

| Tool | Description |
|------|-------------|
| `get_semantic_citations` | Get all papers that cite a given paper |
| `get_semantic_references` | Get all papers referenced by a given paper |
| `get_semantic_recommendations` | Recommend papers based on positive/negative examples |
| `get_semantic_recommendations_for_paper` | Recommend similar papers based on a single paper |
| `get_semantic_author_papers` | Get all papers by a specific author |
| `search_semantic_authors` | Find researchers by name |
| `get_pubmed_citations` | Get citing papers from PubMed |
| `get_pubmed_related` | Get related papers from PubMed |

## Workflow

### Citation Tracing

1. Start with a seed paper (user provides ID, DOI, or title).
2. Use `get_semantic_citations` to find papers that cite it (forward citations).
3. Use `get_semantic_references` to find papers it cites (backward references).
4. Identify key papers in the network by frequency of appearance.

### Literature Recommendations

1. Collect a set of papers the user likes (positive examples).
2. Optionally collect papers the user wants to avoid (negative examples).
3. Use `get_semantic_recommendations` with both lists for personalized recommendations.
4. Or use `get_semantic_recommendations_for_paper` for quick similar-paper discovery.

### Author Network

1. Use `search_semantic_authors` to find an author by name.
2. Use `get_semantic_author_papers` to get their publication list.
3. Cross-reference with citations to build a collaboration map.

## Parameters

- `limit`: controls how many results to return (default 100, max 1000 for citations/references).
- `offset`: for pagination through large result sets.
- `pool`: for single-paper recommendations — `"recent"` (default) or `"all-cs"` (all CS papers).

## Tips

- Paper IDs for Semantic Scholar can be SHA, `DOI:<doi>`, `ARXIV:<id>`, `PMID:<id>`, etc.
- Use `limit` and `offset` for pagination when exploring large citation networks.
- Combine citation data with search to build comprehensive literature reviews.
- Present citation analysis as structured summaries: key citing papers, research trends, and influential works.

## Example Workflows

- "What papers cite this work?" → `get_semantic_citations(paper_id="DOI:10.1038/...", limit=50)`
- "Find me papers similar to this one" → `get_semantic_recommendations_for_paper(paper_id="ARXIV:2301.00001")`
- "Build a reading list based on these 3 papers I like" → `get_semantic_recommendations(positive_paper_ids=[...])`
