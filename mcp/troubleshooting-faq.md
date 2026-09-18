---
id: mcp-troubleshooting-faq
url: watermark/mcp/troubleshooting-faq
title: Troubleshooting & FAQ
weight: 5
description: "Solutions to the most common GroupDocs.Watermark MCP server issues — server not appearing in the client, startup failures, missing native dependencies, and first-launch timeouts."
keywords: MCP server not showing up in Claude Desktop, Claude can't see MCP tools, MCP server failed to start, dnx command not found, libgdiplus not found error, add watermark AI agent, remove watermark MCP, find watermarks in PDF, batch watermark documents
productName: GroupDocs.Watermark MCP Server
toc: True
---

Solutions to the most common GroupDocs.Watermark MCP server issues — server not appearing in the client, startup failures, missing native dependencies, and first-launch timeouts.

{{< alert style="info" >}}
**Platform-specific troubleshooting:** runtime problems depend on which build you run. For the `dnx` runner, native graphics libraries, and the Docker channel, see [Troubleshooting (.NET)]({{< ref "watermark/net/mcp/troubleshooting.md" >}}). The issues on this page apply to every platform.
{{< /alert >}}

## Why is my MCP server not showing up in Claude Desktop?

1. **Restart the client** — every client reads its MCP config only at startup.
2. Check the config file location for your OS ([per-client reference]({{< ref "watermark/net/mcp/install-in-ai-clients.md" >}})) and that the entry sits under the right root key (`mcpServers` for Claude Desktop/Cursor/Windsurf, `servers` for VS Code/VS 2022).
3. Validate the JSON — a trailing comma silently breaks the whole file. If you used the [installer](https://github.com/groupdocs/GroupDocs.Mcp.Installer), a timestamped `.bak` of your previous config sits next to the file for comparison.

## The first tool call is slow or fails once, then works

A **cold cache**: on the very first use the server's package or image is still downloading while the client is already waiting on the connection. Warming it once fixes it for good — the exact command depends on your build: [.NET]({{< ref "watermark/net/mcp/troubleshooting.md" >}}#the-first-tool-call-is-slow-or-fails-once-and-then-works).

## The server fails to start, or a runtime dependency is missing

These are properties of the build you run rather than of MCP, so the fixes live with the platform:

| Symptom | Where the fix is |
|---|---|
| `dnx: command not found` | [.NET troubleshooting]({{< ref "watermark/net/mcp/troubleshooting.md" >}}#dnx-command-not-found) — `dnx` ships inside the .NET 10 SDK |
| `DllNotFoundException: libgdiplus` on Linux/macOS | [.NET troubleshooting]({{< ref "watermark/net/mcp/troubleshooting.md" >}}#dllnotfoundexception-libgdiplus) — install the native graphics libraries, or use the Docker image |
| "docker daemon not reachable" | [.NET troubleshooting]({{< ref "watermark/net/mcp/troubleshooting.md" >}}#docker-daemon-not-reachable) — start Docker Desktop or `dockerd` |

## The agent says a file does not exist

Pass the **file name**, not a full path from your machine: the server resolves names inside its configured storage folder. When a name is not found the tool responds with the list of files it can see, so the agent can correct itself — check that list against [`GROUPDOCS_MCP_STORAGE_PATH`]({{< ref "watermark/net/mcp/configuration.md" >}}).

## Can it remove any watermark?

It removes watermarks the engine can **identify as watermark objects** — including ones added by this or other GroupDocs tools, and many produced by common applications. A "watermark" that was flattened into the page image, or that is simply text drawn into the content, is not a separable object and will not come out. [`search_watermarks`]({{< ref "watermark/mcp/tools-reference/search-watermarks.md" >}}) tells you which case you are in before you promise anyone a clean copy.

## Is a watermark security?

No. It is a **deterrent and a provenance mark** — visible, removable by someone determined, and no barrier to copying the text underneath. For confidentiality, control access to the file; for tamper-evidence, use a [digital signature]({{< ref "signature/mcp/_index.md" >}}); for permanently removing content, use [redaction]({{< ref "redaction/mcp/_index.md" >}}).

## Which file does the agent write to?

A new one. Adding writes a watermarked copy; removing writes `<name>_unwatermarked.<ext>`. Your original is never modified — so in a chain (watermark, then something else) the agent must pass the produced file forward.

## Can I watermark images as well as documents?

Yes — PDF, Office formats, and image formats are all supported targets, and an image watermark can be a PNG, JPG, or similar. Details: [Supported formats]({{< ref "watermark/mcp/supported-formats.md" >}}).

## Can it place the watermark in a specific corner?

The MCP tools expose text, font size, rotation, and opacity (for image watermarks). Fine-grained positioning and per-section placement are library-level features not surfaced as tool parameters today; if you need them through MCP, say so in the [forum](https://forum.groupdocs.com/c/watermark/19).

## Verifying an installation end-to-end

Ask your agent *"list your GroupDocs watermark tools and the license status"* — it should name `add_watermark`, `add_image_watermark`, `search_watermarks`, `remove_watermarks`, `get_document_info`, `get_license_status`. For a scripted check that performs the real MCP handshake and a live call through the engine, see [verifying a .NET installation]({{< ref "watermark/net/mcp/troubleshooting.md" >}}#verifying-an-installation-end-to-end).

## Still stuck?

Post your config (redact license paths) and the client name in the [Watermark forum](https://forum.groupdocs.com/c/watermark/19) — we answer MCP questions daily. Bugs: [GitHub issues](https://github.com/groupdocs-watermark/GroupDocs.Watermark.Mcp/issues).
