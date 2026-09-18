---
id: mcp-uc-find-and-remove-watermarks
url: watermark/mcp/use-cases/find-and-remove-watermarks
title: How to find and remove watermarks with an AI agent
linkTitle: Find and remove watermarks
weight: 3
description: "Find the watermarks a document already carries and remove them with an AI agent over MCP, including filtering by text so only the right mark is removed."
keywords: remove watermark from PDF AI, find watermarks document agent, strip DRAFT watermark MCP, clean watermarked files
productName: GroupDocs.Watermark MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to find and remove watermarks with an AI agent"
        description: "Find the watermarks a document already carries and remove them with an AI agent over MCP, including filtering by text so only the right mark is removed."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Watermark MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Does contract.pdf have a watermark, and what does it say?"
---

"Can you take the DRAFT off?" is a two-call job, and doing it in the right order is what keeps the answer honest.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "watermark/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## 1. Search

> Does contract.pdf have a watermark, and what does it say?

[`search_watermarks`]({{< ref "watermark/mcp/tools-reference/search-watermarks.md" >}}) reports the watermark objects the engine can identify. This step matters because of what it rules out: a document that *looks* watermarked but returns nothing has the mark baked into its content, and no removal call will take it out.

## 2. Remove

> Remove the DRAFT watermark but leave the company logo.

[`remove_watermarks`]({{< ref "watermark/mcp/tools-reference/remove-watermarks.md" >}}) with `textFilter: "DRAFT"` removes only the matching marks and saves `<name>_unwatermarked.<ext>`. Without a filter it removes every watermark it can identify.

## 3. Verify

> Now search the cleaned file and confirm what is left.

A second search on the produced file is the difference between "removed" and "reported as removed". It costs one call and it is the one people skip.

## What will not come out, and why

| The mark is | Removable? |
|---|---|
| A watermark object added by this server or the GroupDocs library | Yes |
| A watermark object added by many common tools | Usually |
| Text drawn into the page content | No — it is content, not a watermark |
| Pixels flattened into a page image | No — nothing distinguishes it from the page |

For the last two, removal is not a watermark problem: covering an area is [redaction]({{< ref "redaction/mcp/_index.md" >}}), and a genuinely clean copy has to come from the source document.

## A word on intent

This tool exists because documents legitimately outlive their marks — a DRAFT becomes final, a template carries an old brand, an internal mark should not reach an archive. Removing a watermark from a document you have no right to redistribute is a different matter, and no API changes that.
