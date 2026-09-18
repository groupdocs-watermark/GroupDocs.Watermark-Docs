---
id: mcp-supported-formats
url: watermark/mcp/supported-formats
title: Supported formats
weight: 4
description: "The MCP server exposes the full GroupDocs.Watermark engine: PDF, Word, Excel, PowerPoint, images, diagrams and 50+ more formats can be watermarked, searched, and cleaned."
keywords: MCP server supported formats, watermark pdf MCP, watermark docx MCP, watermark images MCP
productName: GroupDocs.Watermark MCP Server
toc: True
---

The MCP server exposes the **full GroupDocs.Watermark engine**: every format the .NET library can watermark — 50+ document, spreadsheet, presentation, image, and diagram formats — is available to your AI agent. The canonical matrix lives in the library documentation: [supported document formats]({{< ref "watermark/net/getting-started/supported-document-formats.md" >}}).

What agents are asked for most:

* **PDF** — the distribution format, and the one where *CONFIDENTIAL* and *DRAFT* marks earn their keep.
* **DOCX / XLSX / PPTX** — mark a document while it is still being worked on, in its own format.
* **Images (PNG, JPG, TIFF)** — both as **targets** and as the **source** of an image watermark.

**Watermark sources**: an image watermark can be a PNG, JPG, or similar file resolved from your storage folder by name, exactly like the document.

**What can be removed** depends on how the mark was applied. Watermarks added as watermark objects — by this server, by the GroupDocs library, or by many common tools — can be found and removed. A mark flattened into a page image, or drawn as ordinary content, cannot: [`search_watermarks`]({{< ref "watermark/mcp/tools-reference/search-watermarks.md" >}}) tells you which you are dealing with.
