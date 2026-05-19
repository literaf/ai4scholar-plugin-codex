---
name: nano-draw
description: "Generate, edit, and style-transfer scientific figures using AI. Create architecture diagrams, flowcharts, data visualizations, and other research illustrations. Use when the user wants to create or modify scientific figures, diagrams, or illustrations. 当用户想生成、编辑科研图片或进行风格迁移时使用。"
---

# Nano Draw

Use the `nano_generate`, `nano_edit`, and `nano_vectorize` tools to create and modify scientific figures with AI.

## Available Tools

| Tool | Description |
|------|-------------|
| `nano_generate` | Generate a new scientific figure from a text prompt |
| `nano_edit` | Edit, style-transfer, or compose multiple images |
| `nano_vectorize` | Convert PNG/JPG to vector format (PDF + PPTX) |

## Workflow

### Generate a New Figure

1. Understand what the user wants to illustrate.
2. Craft a descriptive prompt (in English for best results).
3. Choose model based on quality needs: `flash` (fast), `flash31` (balanced), `pro` (best quality), `gptimage` (GPT Image).
4. Call `nano_generate` and return the image URL.

### Edit an Existing Figure

1. Get the image URL(s) from the user.
2. Determine the action: `edit` (modify), `style` (style transfer), or `compose` (merge multiple images).
3. Call `nano_edit` with the appropriate action and prompt.

### Vectorize a Figure

1. Get the raster image URL from the user.
2. Choose mode: `fast`, `standard`, or `premium`.
3. Call `nano_vectorize` to get PDF and PPTX outputs.

## Parameters

### nano_generate

| Parameter | Description | Default |
|-----------|-------------|---------|
| `prompt` | Image description | required |
| `smart` | AI optimizes the prompt automatically | true |
| `model` | `flash` (1.5x) / `flash31` (2x) / `pro` (4x) / `gptimage` (1x) | `"flash"` |
| `aspect_ratio` | `1:1`, `16:9`, `4:3`, `3:2` | `"1:1"` |
| `image_size` | `512px`, `1K`, `2K`, `4K` | `"2K"` |
| `lang` | `en` or `zh` (affects prompt optimization and labels) | none |

### nano_edit

| Parameter | Description | Default |
|-----------|-------------|---------|
| `prompt` | Edit instruction | required |
| `images` | Reference image URL list | required |
| `action` | `edit` / `style` / `compose` | `"edit"` |
| `model` | same as above | `"flash"` |
| `style_preset` | For style action: biorender/nature/textbook/sketch/threed/infograph/schematic/electron | none |

### nano_vectorize

| Parameter | Description | Default |
|-----------|-------------|---------|
| `images` | Image URL list to convert | required |
| `vectorize_mode` | `fast` / `standard` / `premium` | `"standard"` |

## Tips

- Use `smart=true` (default) to let AI enhance your prompt for better results.
- For publication-quality figures, use `model="pro"` and `image_size="4K"`.
- Style presets for `nano_edit` with `action="style"`:
  - `biorender`: BioRender-style biology illustrations
  - `nature`: Nature journal style
  - `textbook`: Clean textbook diagrams
  - `sketch`: Hand-drawn sketch style
  - `threed`: 3D rendered style
  - `schematic`: Technical schematic style
- Use `nano_vectorize` to convert raster figures to editable vector format for papers.
- Set `lang="en"` to ensure English labels in generated figures.

## Example Workflows

- "Draw a transformer architecture diagram" → `nano_generate(prompt="transformer model architecture with multi-head attention, feed-forward layers, and residual connections", model="flash31")`
- "Make this figure look like a Nature paper" → `nano_edit(prompt="clean scientific style", images=["https://..."], action="style", style_preset="nature")`
- "Convert my figure to vector format" → `nano_vectorize(images=["https://..."], vectorize_mode="standard")`
