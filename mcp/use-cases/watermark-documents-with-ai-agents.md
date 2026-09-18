---
id: mcp-uc-watermark-documents-with-ai-agents
url: watermark/mcp/use-cases/watermark-documents-with-ai-agents
title: How to watermark documents with AI agents using MCP
linkTitle: Watermark with AI agents
weight: 1
description: "Add text and image watermarks to documents with an AI agent over MCP: locally, in any of 50+ formats, with the original file left untouched."
keywords: watermark documents with AI agent, MCP watermarking, Claude add watermark PDF, stamp documents AI
productName: GroupDocs.Watermark MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to watermark documents with AI agents using MCP"
        description: "Add text and image watermarks to documents with an AI agent over MCP: locally, in any of 50+ formats, with the original file left untouched."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Watermark MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Add the logo at 30% opacity, then add a DRAFT text watermark to that result."
---

Watermarking through an agent is the small task nobody schedules and everybody needs: mark this before it goes out, brand these before the client sees them, stamp DRAFT until it is approved.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "watermark/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The pattern

1. Put the document in the storage folder the server can see.
2. Ask: *"Add a diagonal CONFIDENTIAL watermark to contract.pdf."*
3. The agent calls [`add_watermark`]({{< ref "watermark/mcp/tools-reference/add-watermark.md" >}}) with the text, a font size, and a rotation.
4. A watermarked copy appears in your output folder; the original is untouched.

## Text or image

| You want | Tool | Key parameters |
|---|---|---|
| CONFIDENTIAL / DRAFT / a date | [`add_watermark`]({{< ref "watermark/mcp/tools-reference/add-watermark.md" >}}) | `text`, `fontSize`, `rotation` |
| A logo, stamp, or signature scan | [`add_image_watermark`]({{< ref "watermark/mcp/tools-reference/add-image-watermark.md" >}}) | `watermarkImage`, `opacity`, `rotation` |

`rotation: -45` gives the classic diagonal. For image watermarks, `opacity` between 0.2 and 0.4 usually reads as branding rather than as an obstruction.

## Chaining

Every call writes a **new file**. To put a logo *and* a text mark on the same document, the second call must take the file the first one produced:

> Add the logo at 30% opacity, then add a DRAFT text watermark to that result.

Without "to that result", the second call starts from the original and only the DRAFT survives.

## Check the licence before a batch

Unlicensed output carries evaluation limitations — which on a watermarking tool means the copies you were about to distribute are not distributable. One call to [`get_license_status`]({{< ref "watermark/mcp/tools-reference/get-license-status.md" >}}) settles it; see [Licensing]({{< ref "watermark/mcp/getting-started/licensing.md" >}}).

## Setup

```bash
dnx GroupDocs.Watermark.Mcp --yes
```

with `GROUPDOCS_MCP_STORAGE_PATH` pointing at your documents folder — [per-client config]({{< ref "watermark/net/mcp/install-in-ai-clients.md" >}}) or the [installer]({{< ref "watermark/mcp/getting-started/_index.md" >}}).

## Where to go next

* [Batch-watermark a folder]({{< ref "watermark/mcp/use-cases/batch-watermark-a-folder.md" >}}) — the whole distribution set in one prompt.
* [Find and remove watermarks]({{< ref "watermark/mcp/use-cases/find-and-remove-watermarks.md" >}}) — and what cannot be removed.
* [Brand documents with a logo]({{< ref "watermark/mcp/use-cases/brand-documents-with-a-logo.md" >}}) — opacity, placement, and taste.
* [On-premise architecture]({{< ref "watermark/mcp/use-cases/on-premise-watermarking.md" >}}) — nothing leaves the machine.
