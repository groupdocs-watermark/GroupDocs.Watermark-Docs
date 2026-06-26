---
id: home
url: watermark/python-net
title: GroupDocs.Watermark for Python via .NET
weight: 1
description: "Native Python library that adds, searches, and removes text and image watermarks across PDF, Word, Excel, PowerPoint, Visio, email, and image formats on Windows, Linux, and macOS. No Microsoft Office or OpenOffice required."
keywords: GroupDocs.Watermark, Python via .NET, add watermark, remove watermark, search watermark, text watermark, image watermark, PDF, Word, Excel, PowerPoint, on-premise, Windows, Linux, macOS, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: true
toc: True
structuredData:
    showOrganization: true
---

<img src="/logo/128x128/groupdocs-watermark-python.png" width="110" height="110" alt="groupdocs-watermark-python-via-net-home" align="left" style="margin: 0 30px 30px 0"/>

<img src="https://img.shields.io/pypi/v/groupdocs-watermark-net?label=GroupDocs.Watermark%20PyPI" alt="PyPI package">
<img src="https://img.shields.io/pypi/dm/groupdocs-watermark-net?label=pypi%20downloads" alt="PyPI downloads">

{{< button style="primary" link="https://releases.groupdocs.com/watermark/python-net/release-notes/" >}} <svg class="gdoc-icon gdoc-product-doc__btn-icon"><use xlink:href="/img/groupdocs-stack.svg#document"></use></svg> Release notes {{< /button >}}
{{< button style="primary" link="https://pypi.org/project/groupdocs-watermark-net/" >}} {{< icon "gdoc_download" >}} Download from PyPI {{< /button >}}
{{< button style="primary" link="https://products.groupdocs.app/watermark/family" >}} <svg class="gdoc-icon gdoc-product-doc__btn-icon"><use xlink:href="/img/groupdocs-stack.svg#app"></use></svg> Online app {{< /button >}}

[GroupDocs.Watermark for Python via .NET](https://products.groupdocs.com/watermark/python-net/) is a document-watermarking API: add styled text and image watermarks, tile them across a page, lock them, target specific pages or slides, and search for or remove existing watermarks — all through one unified API. It works with Word processing, spreadsheets, presentations, PDF, Visio, email, and image formats, with no MS Office or OpenOffice installation required.

<div style="clear:left"></div>

## Quick example

```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color

# Open a document, add a text watermark, and save the result
with Watermarker("document.pdf") as watermarker:
    watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 48))
    watermark.foreground_color = Color.red
    watermark.opacity = 0.5
    watermarker.add(watermark)
    watermarker.save("watermarked.pdf")
```

## Features

- **Text and image watermarks**: Add styled text or image watermarks with configurable color, opacity, rotation, alignment, and sizing.
- **Multi-format**: PDF, Word processing, spreadsheets, presentations, Visio, email, and images, all behind one API.
- **Format-specific placement**: PDF annotations/artifacts, presentation slides, Visio pages, spreadsheet backgrounds and header/footers, and locked Word watermarks.
- **Search and modify**: Find watermarks by text, image similarity, or formatting; edit their text or remove them.
- **Page targeting and tiling**: Apply watermarks to specific pages or the last page only, or tile them across the whole page.

## Supported File Formats

GroupDocs.Watermark supports a wide range of file formats. For a complete list, see the [full list of supported formats]({{< ref "watermark/python-net/getting-started/supported-document-formats.md" >}}).

- **Word Processing** (DOC, DOCX, DOCM, DOT, DOTX, RTF, ODT)
- **Spreadsheets** (XLS, XLSX, XLSM, XLSB, ODS)
- **Presentations** (PPT, PPTX, PPTM, PPS, PPSX, ODP)
- **Fixed-Layout** (PDF)
- **Diagrams** (VSD, VSDX, VSS, VST, VDX)
- **Email** (MSG, EML, EMLX)
- **Images** (BMP, JPG, JPEG, PNG, GIF, TIFF, WEBP)

## Getting Started

To get started, refer to the [System Requirements]({{< ref "watermark/python-net/getting-started/system-requirements.md" >}}), [Supported Document Formats]({{< ref "watermark/python-net/getting-started/supported-document-formats.md" >}}), [Installation]({{< ref "watermark/python-net/getting-started/installation" >}}), and [Quick Start Guide]({{< ref "watermark/python-net/getting-started/quick-start-guide" >}}) sections for setup instructions.

## Developer Guide

For practical code examples and explanations of the open–add–save workflow across every supported family, see the [Developer Guide]({{< ref "watermark/python-net/developer-guide" >}}) section. It covers adding text and image watermarks, customizing and tiling them, format-specific placement, and searching, modifying, and removing existing watermarks.

## Technical Support

If you experience any issues or have suggestions, please refer to the [Technical Support]({{< ref "watermark/python-net/technical-support" >}}) topic. This topic provides multiple support channels tailored to your needs.
