---
id: mcp-tool-add-watermark
url: watermark/mcp/tools-reference/add-watermark
title: add_watermark
weight: 1
description: "The add_watermark MCP tool adds a text watermark to a document with optional font size and rotation, and saves the watermarked file."
keywords: add_watermark MCP tool, add CONFIDENTIAL watermark AI, watermark PDF agent, stamp text on document MCP
productName: GroupDocs.Watermark MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`add_watermark` stamps a **text watermark** across a document and saves a watermarked copy. `fontSize` and `rotation` control how it looks — a diagonal *CONFIDENTIAL* is `rotation: -45`. Example prompt: *"Add a diagonal DRAFT watermark to this contract"*.

**Tool description (as the AI agent sees it):**

> Adds a text watermark to a document and saves the watermarked file to storage. Supports PDF, DOCX, XLSX, PPTX, PNG, JPG, and 50+ more document and image formats. Call this tool immediately whenever the user asks to add a watermark, stamp text onto a document, or mark a document as draft/confidential. Do NOT pre-check whether files exist — just pass the filename the user provided. Returns a saved-path message ('Added text watermark "<text>" to "<file>"') and the download URL or storage path. On failure, the response text starts with 'Watermarking failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "watermark/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `text` | string | yes | Watermark text to add |
| `fontSize` | integer | no | Font size (default 36) |
| `rotation` | integer | no | Rotation angle in degrees (default -45) |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "add_watermark",
  "arguments": {
    "file": {
      "filePath": "contract.pdf"
    },
    "text": "CONFIDENTIAL",
    "fontSize": 48,
    "rotation": -45
  }
}
```

## Result

A saved-path message naming the watermarked file in your output folder; the original is left alone.

The watermark is applied to the document as a watermark object — which is what makes it findable by [`search_watermarks`]({{< ref "watermark/mcp/tools-reference/search-watermarks.md" >}}) and removable by [`remove_watermarks`]({{< ref "watermark/mcp/tools-reference/remove-watermarks.md" >}}) later.

On failure the text starts with `Watermark failed for`, followed by the exception type and message.

## Example prompts

* *"Add a diagonal CONFIDENTIAL watermark to contract.pdf."*
* *"Stamp DRAFT across every page of this deck."*
* *"Watermark these files with today's date and the client name."*

See it used end-to-end: [Watermark documents with AI agents]({{< ref "watermark/mcp/use-cases/watermark-documents-with-ai-agents.md" >}}).
