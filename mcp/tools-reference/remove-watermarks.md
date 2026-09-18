---
id: mcp-tool-remove-watermarks
url: watermark/mcp/tools-reference/remove-watermarks
title: remove_watermarks
weight: 4
description: "The remove_watermarks MCP tool removes watermarks from a document — all of them, or only those matching a text filter — and saves a cleaned copy."
keywords: remove_watermarks MCP tool, remove watermark from PDF AI, strip DRAFT watermark, clean watermarked document
productName: GroupDocs.Watermark MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`remove_watermarks` removes watermarks and saves the result as `<name>_unwatermarked.<ext>`. Pass `textFilter` to remove only the ones containing given text — *"remove the DRAFT mark but keep the logo"*. Example prompt: *"Remove the DRAFT watermark now that it is approved"*.

**Tool description (as the AI agent sees it):**

> Removes existing watermarks from a document and saves the cleaned copy as '<name>_unwatermarked.<ext>'. Supports PDF, DOCX, XLSX, PPTX, PNG, JPG, and 50+ more document and image formats. Call this tool whenever the user asks to remove / strip / clean / delete watermarks from a document. If `textFilter` is supplied, only watermarks whose text contains that substring (case-insensitive) are removed; otherwise ALL watermarks are removed. Do NOT pre-check whether the file exists — just pass the filename the user provided. Returns a saved-path message ('Removed <N> watermark(s) from "<file>"') and the download URL or storage path. If no matching watermarks are found, the original document is saved unchanged with a message starting 'No matching watermarks found in'. On failure, the response text starts with 'Watermark removal failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "watermark/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `textFilter` | string | no | Optional case-insensitive substring filter — only watermarks whose text contains this string are removed. Omit to remove ALL watermarks. |
| `password` | string | no | Password for protected documents |

## Example call

```json
{
  "name": "remove_watermarks",
  "arguments": {
    "file": {
      "filePath": "contract.pdf"
    },
    "textFilter": "DRAFT"
  }
}
```

## Result

A saved-path message naming the cleaned file.

What comes out is what the engine can identify as a watermark object. Content that merely looks like a watermark — flattened into an image, or drawn as ordinary page text — stays. Run [`search_watermarks`]({{< ref "watermark/mcp/tools-reference/search-watermarks.md" >}}) first if the answer matters.

On failure the text starts with `Watermark removal failed for`, followed by the exception type and message.

## Example prompts

* *"Remove the DRAFT watermark now that this is approved."*
* *"Strip every watermark from these files."*
* *"Take out the old logo watermark but leave the confidentiality mark."*

See it used end-to-end: [Find and remove watermarks]({{< ref "watermark/mcp/use-cases/find-and-remove-watermarks.md" >}}).
