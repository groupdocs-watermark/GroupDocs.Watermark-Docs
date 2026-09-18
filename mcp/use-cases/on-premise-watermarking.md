---
id: mcp-uc-on-premise-watermarking
url: watermark/mcp/use-cases/on-premise-watermarking
title: "Running GroupDocs MCP servers on-premise: architecture and security model"
linkTitle: On-premise deployment
weight: 5
description: "Run watermarking for AI agents fully on-premise: local stdio transport, no external endpoints, no inbound ports, no telemetry."
keywords: on-premise MCP server, air-gapped watermarking, MCP security model, local document processing AI
productName: GroupDocs.Watermark MCP Server
toc: True
structuredData:
    showOrganization: True
    howTo:
        name: "Running GroupDocs MCP servers on-premise: architecture and security model"
        description: "Run watermarking for AI agents fully on-premise: local stdio transport, no external endpoints, no inbound ports, no telemetry."
        steps:
        - name: "Run the pinned image inside the perimeter"
          text: "Start the GroupDocs.Watermark MCP server from its versioned Docker image as a child process of the AI client."
        - name: "Mount only the folders the agent may reach"
          text: "Map the document folder read-write and the license folder read-only."
        - name: "Choose the license mode"
          text: "Use a license file for fully offline operation; metered licensing needs outbound egress for usage reports."
---

Run watermarking for AI agents **fully on-premise**: the GroupDocs.Watermark MCP server uses local stdio transport with **no external endpoints, no inbound ports, and no telemetry**. This page is the one to send your security reviewer.

{{< alert style="info" >}}
The commands and config snippets on this page are for the **.NET** build of the server — the only platform available today. Installation and client setup: [MCP server for .NET]({{< ref "watermark/net/mcp/_index.md" >}}). Other platforms will expose the same tools with their own launch command; everything else on this page applies unchanged.
{{< /alert >}}

## The architecture in one picture

```text
+--------------+          +--------------------+         +------------------+
|  AI client   |  stdio   | MCP server process | reads / | local filesystem |
| (Claude, VS  | <----->  | (GroupDocs engine) | <-----> | storage / output |
| Code, agent) | JSON-RPC |   child process    |  writes |     folders      |
+--------------+          +--------------------+         +------------------+
```

* **Transport:** the AI client *starts the server as a child process* and communicates over standard input/output. The server never listens on a network socket.
* **Data path:** agent → local server → local filesystem. Documents, logos, and watermarked copies are read and written in the folders you configure; no content is transmitted anywhere.
* **Network use:** only at install time (nuget.org or ghcr.io/docker.io). At runtime the server makes no outbound calls. Air-gapped: pre-pull the image or pre-cache the package and pin the version.
* **Telemetry:** none. The engine processes documents in-process.

The documents being marked are, almost by definition, the ones that must not circulate freely — that is why they are being stamped CONFIDENTIAL. Uploading them to a cloud service to have the stamp applied would be an odd way to keep them contained.

## Docker deployment inside the perimeter

```bash
docker run --rm -i \
  -v /srv/documents:/data \
  -v /srv/licenses:/license:ro \
  -e GROUPDOCS_MCP_STORAGE_PATH=/data \
  -e GROUPDOCS_LICENSE_PATH=/license/GroupDocs.Watermark.lic \
  ghcr.io/groupdocs-watermark/watermark-net-mcp:26.9.0
```

* Pin the tag (`:26.9.0`, not `:latest`).
* Licence read-only; mount only the folders the agent should reach — including wherever the logo lives.
* Multi-arch images (linux/amd64 + linux/arm64) with all native dependencies included.

## License management

* **License file** — read from local disk by the local process. Fully offline; the right answer for air-gapped deployments.
* **Metered (pay-per-use)** — reports *usage* to GroupDocs servers, so it needs outbound egress. Document content is never part of that report.

Both are covered in [Licensing]({{< ref "watermark/mcp/getting-started/licensing.md" >}}).

## What this fits — honestly

**A good fit:** marking documents before distribution, branding deliverables, stripping obsolete marks after approval, and doing all of it inside a network that does not allow document uploads.

**Not what this is:** access control or copy protection. A watermark is visible provenance, not a barrier — see the note on the [section landing page]({{< ref "watermark/mcp/_index.md" >}}). And it is not a shared service: one stdio server, one client, one machine.

## FAQ

**Does any document content leave the machine?** Not from the server. Only what the agent says back to you travels to your model provider.

**Does it need internet at runtime?** No — only at install, and when metered licensing is enabled.

**Can I run it air-gapped?** Yes: pre-pull the image, use a license file, pin the version.

**What ports does it open?** None. stdio only.

**How do I prove that?** The [verification script]({{< ref "watermark/net/mcp/troubleshooting.md" >}}#verifying-an-installation-end-to-end) performs a real handshake and a real engine call so you can watch exactly what happens.
