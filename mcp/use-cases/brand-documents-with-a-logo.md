---
id: mcp-uc-brand-documents-with-a-logo
url: watermark/mcp/use-cases/brand-documents-with-a-logo
title: How to brand documents with a logo watermark using AI
linkTitle: Brand with a logo
weight: 4
description: "Add a logo or stamp as an image watermark with an AI agent over MCP, with opacity and rotation control, across documents and images."
keywords: logo watermark documents AI, brand PDF with logo MCP, image watermark opacity, stamp documents with logo agent
productName: GroupDocs.Watermark MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to brand documents with a logo watermark using AI"
        description: "Add a logo or stamp as an image watermark with an AI agent over MCP, with opacity and rotation control, across documents and images."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Watermark MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Put logo.png on every page of report.pdf at 30% opacity."
---

A logo watermark says where a document came from without anyone having to read a footer. [`add_image_watermark`]({{< ref "watermark/mcp/tools-reference/add-image-watermark.md" >}}) places it, and `opacity` decides whether the result is branding or a mess.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "watermark/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The prompt

> Put logo.png on every page of report.pdf at 30% opacity.

Both the document and the logo are resolved by name from your storage folder, so keep the logo next to the documents — or in the folder you configured — and refer to it by file name.

## Getting it to look right

* **Opacity 0.2-0.4** — visible, still readable underneath. This is the range most people want.
* **Opacity above 0.6** — the logo dominates; useful for a specimen or a sample marking, distracting for a document people must read.
* **Rotation** — 0 for a clean centred mark, `-45` for the diagonal look that matches text watermarks.

Iterate in the conversation rather than guessing:

> That is too strong — redo it at 0.2.

Each attempt writes a new file, so the original is never at risk; delete the rejected copies afterwards.

## Logo and text together

Brand *and* state the status:

> Add the logo at 25% opacity, then add a CONFIDENTIAL text watermark to that result.

Two calls, chained on the produced file — the "to that result" is what keeps both marks.

## Practical notes

* **Use a transparent PNG** where possible: a logo on a white rectangle will show that rectangle over the page.
* **Images are targets too.** Branding a set of product photos works exactly like branding a PDF.
* **Marks can be removed later.** Because the logo is applied as a watermark object, [`remove_watermarks`]({{< ref "watermark/mcp/tools-reference/remove-watermarks.md" >}}) can take it back off when the document is rebranded — one of the practical advantages over pasting a logo into the source file.
* **Check the licence before a brand rollout.** Evaluation-mode output is not distributable: [`get_license_status`]({{< ref "watermark/mcp/tools-reference/get-license-status.md" >}}).
