---
name: auto-cite
description: "Automatically annotate academic text with citations and generate formatted reference lists. Use when the user has a draft paragraph or section that needs proper academic citations added. 当用户想为学术文本自动添加引用标注和参考文献列表时使用。"
---

# Auto-Cite

Use the `ai4scholar` MCP server tool to automatically annotate academic text with citations.

IMPORTANT: Always use the MCP tool below via a direct tool call. Do NOT manually search for papers, use shell commands, or format citations yourself. The MCP server is pre-configured with authentication — just call the tool directly. Do NOT run shell commands to read config files, parse tokens, curl endpoints, or set up connections. Simply invoke the tool call and it will work.

## MCP Tool

| MCP Tool Call | Description |
|--------------|-------------|
| `mcp__ai4scholar__auto_cite` | AI-powered citation annotation with formatted references |

## Tool Parameters

### mcp__ai4scholar__auto_cite
- `text` (string, required): Academic text to annotate, 100-10000 characters
- `mode` (string, optional): "auto" (AI finds citation points) or "manual" (user marks with [CITE]), default "auto"
- `min_citations` (int, optional): Minimum citations in auto mode, default 10
- `citation_style` (string, optional): ieee/apa/nature/vancouver/mla/chicago/harvard/acs/ama/acm/gbt7714, default "ieee"
- `max_references` (int, optional): Max references to return
- `preferred_venues` (list of strings, optional): Priority journals, e.g. ["Nature", "Science"]
- `field` (string, optional): Research field, e.g. "computer science"
- `year_preference` (int, optional): Prefer papers near this year
- `exclude_preprints` (bool, optional): Exclude arXiv etc., default false
- `exclude_conferences` (bool, optional): Exclude conference papers, default false

## Examples

- "Add citations to my paragraph" → call `mcp__ai4scholar__auto_cite` with `{"text": "...", "mode": "auto", "citation_style": "ieee"}`
- "Cite in Nature style" → call `mcp__ai4scholar__auto_cite` with `{"text": "...", "citation_style": "nature", "field": "machine learning"}`
- "Fill in my [CITE] markers" → call `mcp__ai4scholar__auto_cite` with `{"text": "...[CITE]...", "mode": "manual"}`
