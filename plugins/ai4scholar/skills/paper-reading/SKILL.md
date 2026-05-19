---
name: paper-reading
description: "Download and read full-text academic papers from arXiv, Semantic Scholar, bioRxiv, and medRxiv. Extract text content for summarization and analysis. Use when the user wants to read, summarize, or analyze the content of a specific paper. 当用户想阅读、总结、分析论文全文内容时使用。"
---

# Paper Reading

Use the `ai4scholar` MCP server tools to download and extract full-text content from academic papers. These tools are available as MCP tool calls with the `mcp__ai4scholar__` prefix.

IMPORTANT: Always use the MCP tools listed below via tool calls. Do NOT use web search or manually fetch PDFs. The MCP server handles download and text extraction automatically.

## Available MCP Tools

| MCP Tool Call | Description |
|--------------|-------------|
| `mcp__ai4scholar__read_arxiv_paper` | Extract full text from arXiv paper |
| `mcp__ai4scholar__read_semantic_paper` | Extract full text from Semantic Scholar paper |
| `mcp__ai4scholar__read_biorxiv_paper` | Extract full text from bioRxiv paper |
| `mcp__ai4scholar__read_medrxiv_paper` | Extract full text from medRxiv paper |
| `mcp__ai4scholar__download_arxiv` | Download arXiv PDF locally |
| `mcp__ai4scholar__download_semantic` | Download Semantic Scholar PDF locally |
| `mcp__ai4scholar__download_biorxiv` | Download bioRxiv PDF locally |
| `mcp__ai4scholar__download_medrxiv` | Download medRxiv PDF locally |
| `mcp__ai4scholar__download_pdf_by_doi` | Download any paper by DOI |
| `mcp__ai4scholar__get_pubmed_paper_detail` | Get detailed PubMed paper metadata |

## Workflow

1. Identify the paper source and ID from the user's request.
2. Call the appropriate `read_*` MCP tool to extract full text.
3. After extraction, summarize key findings, methodology, and conclusions.

## Tool Parameters

### mcp__ai4scholar__read_arxiv_paper
- `paper_id` (string, required): arXiv ID, e.g. "2301.00001"

### mcp__ai4scholar__read_semantic_paper
- `paper_id` (string, required): Supports multiple formats:
  - SHA hash: "649def34f8be52c8b66281af98ae884c09aef38b"
  - "DOI:10.18653/v1/N18-3011"
  - "ARXIV:2106.15928"
  - "PMID:19872477"
  - "URL:https://arxiv.org/abs/2106.15928v1"

### mcp__ai4scholar__read_biorxiv_paper / read_medrxiv_paper
- `paper_id` (string, required): DOI, e.g. "10.1101/2024.01.01.123456"

### mcp__ai4scholar__get_pubmed_paper_detail
- `pmid` (string, required): PubMed ID, e.g. "39575807"

## Examples

- "Read arXiv paper 2301.00001" → call `mcp__ai4scholar__read_arxiv_paper` with `{"paper_id": "2301.00001"}`
- "Summarize DOI:10.1038/s41586-024-07487-w" → call `mcp__ai4scholar__read_semantic_paper` with `{"paper_id": "DOI:10.1038/s41586-024-07487-w"}`
