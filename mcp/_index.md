---
id: mcp
url: watermark/mcp
title: GroupDocs.Watermark MCP Server
weight: 6
description: "GroupDocs.Watermark MCP server lets AI agents like Claude, Cursor, and Copilot add, find, and remove watermarks in documents and images — locally on your machine."
keywords: watermark MCP server, add watermark with AI agent, remove watermark MCP, brand documents AI, Claude watermark PDF
productName: GroupDocs.Watermark MCP Server
hideChildren: True
toc: True
---

**GroupDocs.Watermark MCP server** lets AI agents like Claude, Cursor, and Copilot **add, find, and remove watermarks** in documents and images — PDF, Word, Excel, PowerPoint, images and 50+ more formats — **locally on your machine**. 

Run it with one command. The Docker image is self-contained — the runtime and every native dependency the engine needs are inside it:

```bash
docker run --rm -i -v $(pwd)/documents:/data \
  ghcr.io/groupdocs-watermark/watermark-net-mcp:latest
```

With the .NET 10 SDK installed, the same server also runs without Docker:

```bash
dnx GroupDocs.Watermark.Mcp --yes
```

Both are the **.NET** build of the server and run on Windows, Linux, and macOS. Other platforms will each get their own launcher — see [Install for your platform](#install-for-your-platform).

Or use the [guided installer]({{< ref "watermark/mcp/getting-started/_index.md" >}}) to register the server in your AI client, verify the setup, and configure shared folders in one pass.

## What you can do

Six tools (full details in the [tools reference]({{< ref "watermark/mcp/tools-reference/_index.md" >}})):

* **[`add_watermark`]({{< ref "watermark/mcp/tools-reference/add-watermark.md" >}})** — a text watermark with font size and rotation.
* **[`add_image_watermark`]({{< ref "watermark/mcp/tools-reference/add-image-watermark.md" >}})** — a logo, stamp, or scanned signature, with opacity.
* **[`search_watermarks`]({{< ref "watermark/mcp/tools-reference/search-watermarks.md" >}})** — what a document already carries.
* **[`remove_watermarks`]({{< ref "watermark/mcp/tools-reference/remove-watermarks.md" >}})** — all of them, or only those matching a text filter.
* **[`get_document_info`]({{< ref "watermark/mcp/tools-reference/get-document-info.md" >}})** — type, pages, structure.
* **[`get_license_status`]({{< ref "watermark/mcp/tools-reference/get-license-status.md" >}})** — active licensing mode and metered consumption.

Ask in plain language — *"stamp DRAFT across this deck"*, *"take the old watermark off these"* — and the agent picks the tools.

## Install for your platform

Installation, prerequisites, and client configuration are platform-specific; the tools and licensing model below are the same everywhere.

| Platform | Status | Install and setup |
|---|---|---|
| .NET | **Available** | [MCP server for .NET]({{< ref "watermark/net/mcp/_index.md" >}}) |
| Java | Planned | [Tell us you need it](https://forum.groupdocs.com/c/watermark/19) |
| Python | Planned | [Tell us you need it](https://forum.groupdocs.com/c/watermark/19) |
| Node.js | Planned | [Tell us you need it](https://forum.groupdocs.com/c/watermark/19) |

## A watermark is a deterrent, not a control

Worth being clear, because agents will do exactly what you ask: a watermark makes provenance visible and casual reuse awkward. It does not prevent copying, does not protect the text underneath, and can be removed by someone who wants to. If you need the document to be *unreadable* to the wrong people, control access; to be *tamper-evident*, use a [digital signature](/signature/mcp/); to have content *permanently gone*, use [redaction](/redaction/mcp/).

## Supported AI clients

| Client | How it connects |
|---|---|
| Claude Desktop | `claude_desktop_config.json` |
| Claude Code | `claude mcp add` CLI |
| VS Code / GitHub Copilot | user-level or workspace `mcp.json` |
| Visual Studio 2022 (17.14+) | `.mcp.json` in the solution root |
| Cursor | `~/.cursor/mcp.json` |
| Windsurf | `~/.codeium/windsurf/mcp_config.json` |
| Cline | Cline MCP settings |
| Codex CLI | `codex mcp add` CLI |
| JetBrains Rider | manual registration (Settings → AI Assistant → MCP) |

Exact config blocks for every client: [Register in AI clients]({{< ref "watermark/net/mcp/install-in-ai-clients.md" >}}).

## Delivery channels

| | Docker (recommended) | NuGet (`dnx`) |
|---|---|---|
| Prerequisites | Docker only | .NET 10 SDK (+ `libgdiplus` on Linux/macOS) |
| Native dependencies | bundled in the image | installed by you (or the setup script) |
| Package | `ghcr.io/groupdocs-watermark/watermark-net-mcp` | `GroupDocs.Watermark.Mcp` on NuGet |
| Architectures | linux/amd64 + linux/arm64 (Apple Silicon native) | any OS with .NET 10 |

## How it works

The server uses MCP's **local stdio transport**: your AI client starts the server as a child process and talks to it over standard input/output. No inbound ports, no external endpoints, no telemetry — the data path is *agent → local server → local filesystem*. Details: [On-premise architecture]({{< ref "watermark/mcp/use-cases/on-premise-watermarking.md" >}}).

## When you need more than a "add watermark" checkbox

Office and PDF tools can stamp their own format, by hand. Choose this server when you need: **one model across 50+ formats** including images; watermarks as **objects you can later find and remove**, not pixels baked into a page; batch marking driven from a prompt; image watermarks with opacity control; and the fidelity of the commercial GroupDocs engine trusted by enterprise teams for over a decade.

## Resources

* [Quick start]({{< ref "watermark/mcp/getting-started/_index.md" >}}) · [Use cases]({{< ref "watermark/mcp/use-cases/_index.md" >}}) · [Troubleshooting & FAQ]({{< ref "watermark/mcp/troubleshooting-faq.md" >}})
* GitHub: [server source](https://github.com/groupdocs-watermark/GroupDocs.Watermark.Mcp) · [installer](https://github.com/groupdocs/GroupDocs.Mcp.Installer) · [integration tests](https://github.com/groupdocs-watermark/GroupDocs.Watermark.Mcp.Tests)
* [NuGet package](https://www.nuget.org/packages/GroupDocs.Watermark.Mcp) · [Docker image](https://github.com/orgs/groupdocs-watermark/packages/container/package/watermark-net-mcp) · [MCP Registry](https://registry.modelcontextprotocol.io/v0/servers?search=io.github.groupdocs-watermark/groupdocs-watermark-mcp)
* Questions: [Watermark forum](https://forum.groupdocs.com/c/watermark/19)
