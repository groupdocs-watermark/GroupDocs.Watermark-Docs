---
id: mcp-tool-search-watermarks
url: watermark/mcp/tools-reference/search-watermarks
title: search_watermarks
weight: 3
description: "The search_watermarks MCP tool finds watermarks already present in a document and returns their details as JSON."
keywords: search_watermarks MCP tool, find watermarks in PDF, detect watermark AI agent, check if document watermarked
productName: GroupDocs.Watermark MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`search_watermarks` reports the watermarks a document already carries. It is the call to make **before** promising to remove anything — it distinguishes a real watermark object from text baked into the page. Example prompt: *"Does this document have a watermark, and what does it say?"*

**Tool description (as the AI agent sees it):**

> Searches for watermarks in a document and returns their details as JSON. Supports PDF, DOCX, XLSX, PPTX, PNG, JPG, and 50+ more document and image formats. Call this tool immediately whenever the user asks to search for watermarks, find watermarks, list watermarks, or check if a document has watermarks. Do NOT pre-check whether files exist — just pass the filename the user provided. Returns a JSON object with fields `count` (number of watermarks found) and `watermarks` (array with `type` ("text"|"image"), `text`, `page`, `x`, `y`, `width`, `height`, `rotateAngle` per watermark). On failure, the response text starts with 'Search failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "watermark/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "search_watermarks",
  "arguments": {
    "file": {
      "filePath": "contract.pdf"
    }
  }
}
```

## Result

A JSON array describing each watermark the engine can identify.

An empty result on a document that visibly shows "DRAFT" is informative, not a failure: it means the mark is part of the page content rather than a watermark object, and [`remove_watermarks`]({{< ref "watermark/mcp/tools-reference/remove-watermarks.md" >}}) will not be able to take it out.

On failure the text starts with `Watermark search failed for`, followed by the exception type and message.

## Example prompts

* *"Does this document have a watermark?"*
* *"What do the watermarks on these files say?"*
* *"Check which of these are still marked DRAFT."*

See it used end-to-end: [Find and remove watermarks]({{< ref "watermark/mcp/use-cases/find-and-remove-watermarks.md" >}}).
