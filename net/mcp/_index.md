---
id: mcp-net
url: watermark/net/mcp
title: MCP server for .NET
linkTitle: MCP Server
weight: 7
description: "Install and configure the GroupDocs.Watermark MCP server for .NET — one-click install links for VS Code and Cursor, per-OS setup for Windows, Linux, and macOS, and the full environment-variable reference."
keywords: GroupDocs.Watermark MCP .NET, install MCP server dnx, MCP server Docker image, MCP server configuration, Model Context Protocol .NET
productName: GroupDocs.Watermark MCP Server for .NET
hideChildren: True
toc: True
---

Everything needed to **install and run** the GroupDocs.Watermark MCP server on the .NET platform. What the server *does* — its tools, use cases, and licensing model — is platform-independent and lives in the [MCP server section]({{< ref "watermark/mcp/_index.md" >}}).

| The .NET build at a glance | |
|---|---|
| Package | [`GroupDocs.Watermark.Mcp`](https://www.nuget.org/packages/GroupDocs.Watermark.Mcp) (current **26.9.0**) |
| One-command run | `dnx GroupDocs.Watermark.Mcp --yes` |
| Container images | `ghcr.io/groupdocs-watermark/watermark-net-mcp` · `groupdocs/watermark-net-mcp` |
| Prerequisites | [.NET 10 SDK](https://dotnet.microsoft.com/download/dotnet/10.0) for the NuGet channel, or Docker |
| Source | [GroupDocs.Watermark.Mcp on GitHub](https://github.com/groupdocs-watermark/GroupDocs.Watermark.Mcp) |
| Release notes | [changelog](https://github.com/groupdocs-watermark/GroupDocs.Watermark.Mcp/tree/master/changelog) · [GitHub releases](https://github.com/groupdocs-watermark/GroupDocs.Watermark.Mcp/releases) |

## Start here

1. **Install** for your operating system — [Windows]({{< ref "watermark/net/mcp/windows-installation.md" >}}) · [Linux]({{< ref "watermark/net/mcp/linux-installation.md" >}}) · [macOS]({{< ref "watermark/net/mcp/macos-installation.md" >}})
2. **Register it in your AI client** — [one-click links and per-client configs]({{< ref "watermark/net/mcp/install-in-ai-clients.md" >}})
3. **Point it at your documents** — [configuration]({{< ref "watermark/net/mcp/configuration.md" >}})
4. **License it** — evaluation, a license file, or metered keys: [Licensing]({{< ref "watermark/mcp/getting-started/licensing.md" >}})

## In this section

* [Install on Windows]({{< ref "watermark/net/mcp/windows-installation.md" >}})
* [Install on Linux]({{< ref "watermark/net/mcp/linux-installation.md" >}})
* [Install on macOS]({{< ref "watermark/net/mcp/macos-installation.md" >}})
* [Register in AI clients]({{< ref "watermark/net/mcp/install-in-ai-clients.md" >}}) — VS Code, Cursor, Claude, Visual Studio, Windsurf, Cline, Codex, Rider
* [Configuration]({{< ref "watermark/net/mcp/configuration.md" >}}) — storage, output, license, metered keys
* [System requirements]({{< ref "watermark/net/mcp/system-requirements.md" >}})
* [Troubleshooting (.NET)]({{< ref "watermark/net/mcp/troubleshooting.md" >}}) — `dnx`, native libraries, Docker daemon

## Platform-independent reference

* [Tools reference]({{< ref "watermark/mcp/tools-reference/_index.md" >}}) — `add_watermark`, `add_image_watermark`, `search_watermarks`, `remove_watermarks`, `get_document_info`, `get_license_status`
* [Use cases]({{< ref "watermark/mcp/use-cases/_index.md" >}}) · [Supported formats]({{< ref "watermark/mcp/supported-formats.md" >}}) · [Troubleshooting & FAQ]({{< ref "watermark/mcp/troubleshooting-faq.md" >}})
