---
name: auto-cite
description: "Automatically annotate academic text with citations and generate formatted reference lists. Use when the user has a draft paragraph or section that needs proper academic citations added. 当用户想为学术文本自动添加引用标注和参考文献列表时使用。"
---

# Auto-Cite

Use the `auto_cite` tool to automatically find and insert academic citations into text.

## Tool

| Tool | Description |
|------|-------------|
| `auto_cite` | AI-powered citation annotation — identifies citation points, searches for matching papers, outputs annotated text with formatted references |

## Workflow

1. Receive academic text from the user (100–10,000 characters).
2. Choose mode:
   - `auto`: AI identifies where citations are needed.
   - `manual`: User marks positions with `[CITE]` or `[CITE:hint]` in their text.
3. Configure citation style and filtering preferences.
4. Call `auto_cite` and present the annotated text with reference list.

## Parameters

| Parameter | Description | Default |
|-----------|-------------|---------|
| `text` | Academic text to annotate (100–10,000 chars) | required |
| `mode` | `"auto"` or `"manual"` | `"auto"` |
| `min_citations` | Minimum number of citations in auto mode | 10 |
| `citation_style` | Format: ieee/apa/nature/vancouver/mla/chicago/harvard/acs/ama/acm/gbt7714 | `"ieee"` |
| `max_references` | Maximum references to return | none |
| `preferred_venues` | Priority journals (e.g., `["Nature", "Science", "CVPR"]`) | none |
| `field` | Research field (e.g., `"computer science"`) | none |
| `year_preference` | Prefer papers near this year | none |
| `exclude_preprints` | Exclude arXiv and other preprints | false |
| `exclude_conferences` | Exclude conference papers | false |

## Tips

- For Chinese academic writing, use `citation_style="gbt7714"` (GB/T 7714 国标格式).
- Set `field` to help the AI find more relevant citations for niche topics.
- Use `preferred_venues` to bias towards top-tier venues in your field.
- Use `year_preference` to prioritize recent or seminal (older) works.
- In `manual` mode, `[CITE:transformer architecture]` gives the AI a hint about what to cite.

## Example Workflows

- "Add citations to my introduction paragraph" → `auto_cite(text="...", mode="auto", citation_style="ieee")`
- "I marked citation spots with [CITE], fill them in" → `auto_cite(text="...[CITE]...", mode="manual")`
- "Cite this in Nature style with recent ML papers" → `auto_cite(text="...", citation_style="nature", field="machine learning", year_preference=2024)`
