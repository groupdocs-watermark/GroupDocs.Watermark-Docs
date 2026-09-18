---
id: mcp-uc-batch-watermark-a-folder
url: watermark/mcp/use-cases/batch-watermark-a-folder
title: How to batch-watermark a folder of documents with an AI agent
linkTitle: Batch-watermark a folder
weight: 2
description: "Watermark many documents in one prompt with an AI agent over MCP: the agent iterates the folder, applies the same mark to each file, and reports what it produced."
keywords: batch watermark documents, watermark folder AI agent, bulk watermark PDF MCP, mark documents before distribution
productName: GroupDocs.Watermark MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "How to batch-watermark a folder of documents with an AI agent"
        description: "Watermark many documents in one prompt with an AI agent over MCP: the agent iterates the folder, applies the same mark to each file, and reports what it produced."
        steps:
        - name: "Install the server"
          text: "Run the GroupDocs.Watermark MCP server with Docker or dnx and register it in your AI client."
        - name: "Put the documents in the storage folder"
          text: "Point GROUPDOCS_MCP_STORAGE_PATH at the folder that holds the files the agent should use."
        - name: "Ask the agent"
          text: "Add a diagonal CONFIDENTIAL watermark to every PDF in my documents folder, then list the files you produced."
---

Distribution sets arrive as folders, and marking them one by one is the kind of work that gets skipped under deadline. One prompt covers it.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "watermark/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## Setup

Point `GROUPDOCS_MCP_STORAGE_PATH` at the folder ([configuration]({{< ref "watermark/net/mcp/configuration.md" >}})). Files are resolved by name, so the agent passes `proposal-01.pdf`, not a path from your machine.

## The prompt

> Add a diagonal CONFIDENTIAL watermark to every PDF in my documents folder, then list the files you produced.

The agent calls [`add_watermark`]({{< ref "watermark/mcp/tools-reference/add-watermark.md" >}}) per file. Each produces a new watermarked copy; the originals stay as they are.

## Variations that come up

> Watermark each file with the client name and today's date.
> Put the logo on the slide decks and a text mark on the PDFs.
> Mark everything except the ones that already have a watermark.

The last one is worth spelling out: the agent runs [`search_watermarks`]({{< ref "watermark/mcp/tools-reference/search-watermarks.md" >}}) first and skips the files that already carry one — which is how you avoid a document with *CONFIDENTIAL* stamped twice at different angles.

## Keep it honest and cheap

* **Ask for the list of produced files.** A batch that reports only "done" leaves you guessing which copies to ship.
* **Watch the failures.** A mixed folder may contain a format the engine cannot watermark; the call fails with a message rather than silently skipping, so ask for failures to be listed explicitly.
* **Mind metered usage.** Under [metered licensing]({{< ref "watermark/mcp/getting-started/licensing.md" >}}#metered-pay-per-use-licensing) each file is billed processing.
* **Check the licence first.** Evaluation-mode output carries evaluation limitations — a whole folder of them is a wasted run.

## The unmark pass

Approval flips the requirement. Same folder, opposite prompt:

> Remove the DRAFT watermark from every file in this folder and keep the rest of the marks.

That is [`remove_watermarks`]({{< ref "watermark/mcp/tools-reference/remove-watermarks.md" >}}) with a `textFilter` — see [Find and remove watermarks]({{< ref "watermark/mcp/use-cases/find-and-remove-watermarks.md" >}}).
