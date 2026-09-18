---
id: mcp-tools-reference
url: watermark/mcp/tools-reference
title: Tools reference
weight: 2
description: "Complete reference of every tool the GroupDocs.Watermark MCP server exposes to AI agents, with parameters, example prompts, and results."
keywords: MCP tools list watermarking, add_watermark MCP tool, remove_watermarks MCP, search watermarks agent, MCP tools reference
productName: GroupDocs.Watermark MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

Complete reference of every tool the GroupDocs.Watermark MCP server exposes to AI agents, with parameters, example prompts, and results. Captured from a live `tools/list` call against server version **26.9.0** (raw capture: `tools-list.generated.json` in this section's source).

| Tool | What it does |
|---|---|
| [`add_watermark`]({{< ref "watermark/mcp/tools-reference/add-watermark.md" >}}) | Adds a text watermark with optional size and rotation |
| [`add_image_watermark`]({{< ref "watermark/mcp/tools-reference/add-image-watermark.md" >}}) | Adds an image watermark — logo, stamp, signature scan — with opacity and rotation |
| [`search_watermarks`]({{< ref "watermark/mcp/tools-reference/search-watermarks.md" >}}) | Finds watermarks already in a document and returns their details |
| [`remove_watermarks`]({{< ref "watermark/mcp/tools-reference/remove-watermarks.md" >}}) | Removes watermarks, optionally only those matching a text filter |
| [`get_document_info`]({{< ref "watermark/mcp/tools-reference/get-document-info.md" >}}) | Returns file type, page count, and format-specific properties |
| [`get_license_status`]({{< ref "watermark/mcp/tools-reference/get-license-status.md" >}}) | Reports the active licensing mode and, under metered licensing, consumption |

## The FileInput shape

Every tool takes its document through the same `file` object — pass **either** a name from your storage folder **or** inline content:

```json
{ "file": { "filePath": "contract.pdf" } }
```

| Field | Type | Description |
|---|---|---|
| `filePath` | string | File path or name in the configured storage folder |
| `fileContent` | string | Base64-encoded file content (alternative to `filePath`) |
| `fileName` | string | Original filename with extension — required with `fileContent`. Since **26.9.0** it also works on its own, resolved from the storage folder exactly like `filePath` |

You rarely write this JSON yourself: the AI agent does, from your plain-language prompt. Missing files are not an error to fear — the tool responds with the list of available files so the agent can correct itself.
