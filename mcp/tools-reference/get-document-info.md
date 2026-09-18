---
id: mcp-tool-get-document-info
url: watermark/mcp/tools-reference/get-document-info
title: get_document_info
weight: 5
description: "The get_document_info MCP tool returns file type, page count, and format-specific properties for a document without modifying it."
keywords: get_document_info MCP, page count before watermarking, document structure check MCP, inspect file agent
productName: GroupDocs.Watermark MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`get_document_info` returns the file type, page count, and format-specific structure without changing anything — the sensible check before watermarking a batch. Example prompt: *"How many pages will this watermark cover?"*

**Tool description (as the AI agent sees it):**

> Returns the file type, page count, and format-specific properties of a document as JSON. Supports PDF, DOCX, XLSX, PPTX, PNG, JPG, and 50+ more document and image formats. Call this tool whenever the user asks about the structure of a document — page count, dimensions, file type — without modifying it. Useful as a precondition check before AddWatermark / SearchWatermarks (e.g. 'how many pages does this PDF have?'). Do NOT pre-check whether the file exists — just pass the filename the user provided. Returns a JSON object with fields `fileType` (engine-reported format name), `fileFormat` (extension), `size` (bytes), `pageCount`, and `pages` (array of `{ number, width, height }` per page). On failure, the response text starts with 'Document-info lookup failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "watermark/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "get_document_info",
  "arguments": {
    "file": {
      "filePath": "contract.pdf"
    }
  }
}
```

## Result

A JSON object with the file type, page count, and format-specific properties.

On failure the text starts with `Document-info lookup failed for`, followed by the exception type and message.

## Example prompts

* *"How many pages does this document have?"*
* *"What format is this file?"*
* *"Check the structure before I watermark the folder."*
