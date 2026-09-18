---
id: mcp-getting-started
url: watermark/mcp/getting-started
title: Quick start
weight: 1
description: "Install and register the GroupDocs.Watermark MCP server in Claude Desktop, VS Code, Cursor, or any MCP client in three commands using the guided installer — then verify the setup automatically."
keywords: how to install MCP server, set up document MCP server, add MCP server to Claude Desktop, MCP server quick start
productName: GroupDocs.Watermark MCP Server
hideChildren: True
toc: True
---

{{< alert style="info" >}}
These steps install the **.NET** build of the server — the only platform available today. Java, Python, and Node.js builds are planned; each will get its own install section under its platform. Platform-independent material (tools, use cases, licensing) lives here and applies to all of them.
{{< /alert >}}

Install and register the GroupDocs.Watermark MCP server in Claude Desktop, VS Code, Cursor, or any MCP client in three commands with the guided [installer](https://github.com/groupdocs/GroupDocs.Mcp.Installer) — then verify the setup automatically:

```powershell
git clone https://github.com/groupdocs/GroupDocs.Mcp.Installer.git
cd GroupDocs.Mcp.Installer

# wizard: products, channel, clients, folders, license
./install-groupdocs-mcp.ps1 -Interactive
# preview - prints everything, changes nothing
./install-groupdocs-mcp.ps1 -DryRun
# apply + warm caches + verify the setup in one go
./install-groupdocs-mcp.ps1 -Verify
```

Then **restart your AI client** (Claude Desktop, VS Code, Cursor, …) so it picks up the new server.

## Your first prompt

Put a document to protect (say `contract.pdf`) into the storage folder you chose, then ask your agent:

> Add a diagonal CONFIDENTIAL watermark to contract.pdf

The agent calls `add_watermark` with the text and a rotation, and saves the watermarked copy to your output folder. The original is untouched and nothing is uploaded.

## Where to go next

* **Fresh machine?** Follow your OS page — it includes the prerequisite bootstrap:
  [Windows]({{< ref "watermark/net/mcp/windows-installation.md" >}}) · [Linux]({{< ref "watermark/net/mcp/linux-installation.md" >}}) · [macOS]({{< ref "watermark/net/mcp/macos-installation.md" >}})
* **Manual or single-client install** (exact JSON per client): [Register in AI clients]({{< ref "watermark/net/mcp/install-in-ai-clients.md" >}})
* **Docker-only shop:** run `./install-groupdocs-mcp.ps1 -EmitCompose -Clients @()` to generate a `docker-compose.yml` instead of client registration — see [Configuration]({{< ref "watermark/net/mcp/configuration.md" >}}).
* **Licensing:** the server works in evaluation mode out of the box; your existing GroupDocs.Watermark license applies — [Licensing]({{< ref "watermark/mcp/getting-started/licensing.md" >}}).
