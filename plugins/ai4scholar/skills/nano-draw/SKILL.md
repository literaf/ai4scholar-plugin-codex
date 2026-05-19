---
name: nano-draw
description: "Generate, edit, and style-transfer scientific figures using AI. Create architecture diagrams, flowcharts, data visualizations, and other research illustrations. Use when the user wants to create or modify scientific figures, diagrams, or illustrations. 当用户想生成、编辑科研图片或进行风格迁移时使用。"
---

# Nano Draw

Use the `ai4scholar` MCP server tools to create and modify scientific figures with AI.

IMPORTANT: Always use the MCP tools listed below via tool calls. Do NOT use other image generation tools. The Nano Draw tools are specialized for scientific figures.

## Available MCP Tools

| MCP Tool Call | Description |
|--------------|-------------|
| `mcp__ai4scholar__nano_generate` | Generate a new scientific figure from text prompt |
| `mcp__ai4scholar__nano_edit` | Edit, style-transfer, or compose images |
| `mcp__ai4scholar__nano_vectorize` | Convert PNG/JPG to vector PDF + PPTX |

## Tool Parameters

### mcp__ai4scholar__nano_generate
- `prompt` (string, required): Image description
- `smart` (bool, optional): AI optimizes prompt, default true
- `model` (string, optional): "flash" (fast) / "flash31" (balanced) / "pro" (best) / "gptimage", default "flash"
- `aspect_ratio` (string, optional): "1:1", "16:9", "4:3", "3:2", default "1:1"
- `image_size` (string, optional): "512px", "1K", "2K", "4K", default "2K"
- `lang` (string, optional): "en" or "zh"

### mcp__ai4scholar__nano_edit
- `prompt` (string, required): Edit instruction
- `images` (list of strings, required): Reference image URLs
- `action` (string, optional): "edit" / "style" / "compose", default "edit"
- `model` (string, optional): Same as above, default "flash"
- `style_preset` (string, optional): For style action: biorender/nature/textbook/sketch/threed/infograph/schematic/electron

### mcp__ai4scholar__nano_vectorize
- `images` (list of strings, required): Image URLs to convert
- `vectorize_mode` (string, optional): "fast" / "standard" / "premium", default "standard"

## Examples

- "Draw a transformer diagram" → call `mcp__ai4scholar__nano_generate` with `{"prompt": "transformer model architecture with multi-head attention", "model": "flash31"}`
- "Make this look like Nature style" → call `mcp__ai4scholar__nano_edit` with `{"prompt": "clean scientific style", "images": ["https://..."], "action": "style", "style_preset": "nature"}`
- "Convert to vector" → call `mcp__ai4scholar__nano_vectorize` with `{"images": ["https://..."]}`
