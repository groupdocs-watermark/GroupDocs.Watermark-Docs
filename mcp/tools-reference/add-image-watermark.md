---
id: mcp-tool-add-image-watermark
url: watermark/mcp/tools-reference/add-image-watermark
title: add_image_watermark
weight: 2
description: "The add_image_watermark MCP tool adds an image watermark — logo, stamp, or signature scan — to a document with opacity and rotation control."
keywords: add_image_watermark MCP tool, logo watermark PDF AI, stamp image on document, brand documents agent
productName: GroupDocs.Watermark MCP Server
generated: true
serverVersion: 26.9.0
toc: True
---

`add_image_watermark` places an **image** — a logo, a stamp, a scanned signature — onto the document, with `opacity` and `rotation`. The watermark source can be PNG, JPG, and similar. Example prompt: *"Put our logo on every page at 30% opacity"*.

**Tool description (as the AI agent sees it):**

> Adds an image watermark (e.g. company logo, signature scan, stamp) to a document and saves the watermarked file. Supports PDF, DOCX, XLSX, PPTX, PNG, JPG, and 50+ more document and image formats as the target. The watermark source image can be PNG, JPG, BMP, or TIFF, resolved from the same storage as the target. Call this tool whenever the user asks to add an image / logo / stamp watermark, or to overlay an image on a document. Do NOT pre-check whether files exist — just pass the filenames the user provided. Returns a saved-path message ('Added image watermark from "<image>" to "<file>"') and the download URL or storage path. On failure, the response text starts with 'Image watermarking failed for' followed by the underlying exception type, message, and inner-exception chain.

## Parameters

| Name | Type | Required | Description |
|---|---|---|---|
| `file` | object | yes |  — [FileInput shape]({{< ref "watermark/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `watermarkImage` | object | yes | Image file to use as the watermark — resolved from the same storage as `file`. — [FileInput shape]({{< ref "watermark/mcp/tools-reference/_index.md#the-fileinput-shape" >}}) |
| `opacity` | number | no | Opacity 0.0 (fully transparent) to 1.0 (opaque). Default 0.5. |
| `rotation` | integer | no | Rotation angle in degrees (default 0) |
| `password` | string | no | Password for protected target documents |

## Example call

```json
{
  "name": "add_image_watermark",
  "arguments": {
    "file": {
      "filePath": "report.pdf"
    },
    "watermarkImage": {
      "filePath": "logo.png"
    },
    "opacity": 0.3
  }
}
```

## Result

A saved-path message naming the watermarked file.

`opacity` is the parameter that decides whether this reads as branding or as vandalism: low values (0.2-0.4) sit behind the content; high values dominate the page. Both the document and the watermark image are resolved from your storage folder by name, like any other [FileInput]({{< ref "watermark/mcp/tools-reference/_index.md#the-fileinput-shape" >}}).

On failure the text starts with `Image watermark failed for`, followed by the exception type and message.

## Example prompts

* *"Put our logo on every page of this report at 30% opacity."*
* *"Add the approved stamp image to the signed contract."*
* *"Brand these slides with the company mark."*
