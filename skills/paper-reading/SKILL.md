---
name: paper-reading
description: "Download and read full-text academic papers from arXiv, Semantic Scholar, bioRxiv, and medRxiv. Extract text content for summarization and analysis. Use when the user wants to read, summarize, or analyze the content of a specific paper. 当用户想阅读、总结、分析论文全文内容时使用。"
---

# Paper Reading

Use the bundled `ai4scholar` MCP tools to download PDFs and extract full-text content from academic papers.

## Available Tools

| Tool | Platform | Input |
|------|----------|-------|
| `read_arxiv_paper` | arXiv | paper_id (e.g., `2301.00001`) |
| `read_semantic_paper` | Semantic Scholar | paper_id (SHA, DOI:, ARXIV:, PMID:, URL:) |
| `read_biorxiv_paper` | bioRxiv | paper DOI |
| `read_medrxiv_paper` | medRxiv | paper DOI |
| `download_arxiv` | arXiv | paper_id → saves PDF locally |
| `download_semantic` | Semantic Scholar | paper_id → saves PDF locally |
| `download_biorxiv` | bioRxiv | paper DOI → saves PDF locally |
| `download_medrxiv` | medRxiv | paper DOI → saves PDF locally |
| `download_pdf_by_doi` | Any (via DOI) | DOI → saves PDF locally |
| `get_pubmed_paper_detail` | PubMed | PMID → detailed metadata |

## Workflow

1. Identify the paper source and ID from the user's request.
2. For reading full text, use `read_*` tools which download and extract text automatically.
3. For saving PDFs locally, use `download_*` tools (only available in local/stdio mode).
4. For PubMed papers (no full-text download), use `get_pubmed_paper_detail` for metadata.
5. After extraction, summarize key findings, methodology, and conclusions.

## Paper ID Formats

- **arXiv**: `2301.00001` or `2106.12345`
- **Semantic Scholar**: supports multiple formats:
  - SHA hash: `649def34f8be52c8b66281af98ae884c09aef38b`
  - `DOI:10.18653/v1/N18-3011`
  - `ARXIV:2106.15928`
  - `PMID:19872477`
  - `URL:https://arxiv.org/abs/2106.15928v1`
- **bioRxiv/medRxiv**: DOI (e.g., `10.1101/2024.01.01.123456`)

## Tips

- `read_*` tools return extracted plain text — ideal for summarization.
- `download_*` tools save the PDF file — only works in local mode (stdio), not in SSE mode.
- `download_pdf_by_doi` tries Unpaywall first, then publisher direct download. Works best on campus networks with institutional access.
- If a paper is behind a paywall, suggest the user run in local mode on a campus network.

## Example Workflows

- "Read this arXiv paper 2301.00001" → `read_arxiv_paper(paper_id="2301.00001")`
- "Summarize this paper DOI:10.1038/s41586-024-07487-w" → `read_semantic_paper(paper_id="DOI:10.1038/s41586-024-07487-w")`
- "Download this paper for me" → `download_pdf_by_doi(doi="10.1038/...")` (local mode only)
