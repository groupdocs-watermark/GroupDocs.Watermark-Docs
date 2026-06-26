---
id: product-overview
url: watermark/python-net/product-overview
title: GroupDocs.Watermark for Python via .NET Overview
linkTitle: Product overview
weight: 1
description: "GroupDocs.Watermark for Python via .NET adds, searches, and removes text and image watermarks across PDF, Word, Excel, PowerPoint, Visio, email, and image formats — with format-specific placement, tiling, locking, and content-tree access — on-premise, with no Microsoft Office required."
keywords: watermark, add watermark, remove watermark, search watermark, PDF, DOCX, XLSX, PPTX, image, python
productName: GroupDocs.Watermark for Python via .NET
toc: True
---

## What is GroupDocs.Watermark?

GroupDocs.Watermark for Python via .NET is a native Python library that adds, searches, and removes **text and image watermarks** across PDF, Word, Excel, PowerPoint, Visio, email, and image formats. It runs entirely on-premise, requires no Microsoft Office installation, and ships as a pre-built wheel for Windows, Linux, and macOS.

Typical uses include:

- **Document security** — stamp every file in a pipeline with a "Confidential" or "Draft" mark that is hard to remove with third-party tools.
- **Branding** — overlay a logo or seal on documents and on the images embedded inside them.
- **Cleanup and migration** — find and remove outdated labels or third-party watermarks before sharing or re-publishing.
- **Compliance and tamper-resistance** — lock watermarks, add print-only PDF annotations, or rasterize pages so the watermark cannot be edited out.
- **Auditing** — search documents for existing watermarks by text, image similarity, or formatting, and report or modify them.

## Key Capabilities

| Capability | Description |
|---|---|
| **Text and image watermarks** | [Add styled text or image watermarks]({{< ref "watermark/python-net/developer-guide/basic-usage/add-text.md" >}}) with color, opacity, rotation, alignment, and sizing. |
| **Customize and tile** | [Customize]({{< ref "watermark/python-net/developer-guide/basic-usage/customize.md" >}}) appearance and position, or [tile a watermark]({{< ref "watermark/python-net/developer-guide/basic-usage/adding-repeated-watermarks.md" >}}) across the whole page. |
| **Advanced positioning** | [Absolute and relative positioning, margins, sizing, and rotation]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}}). |
| **Format-specific placement** | PDF [artifacts/annotations]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/watermarks-in-pdf-document.md" >}}), [presentation slides]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents" >}}), [worksheets]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents" >}}), [Visio pages]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-diagram-documents" >}}), and [Word sections]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents" >}}). |
| **Search and modify** | [Find watermarks by text, image, or formatting]({{< ref "watermark/python-net/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks.md" >}}), then [modify]({{< ref "watermark/python-net/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties.md" >}}) or [remove]({{< ref "watermark/python-net/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks.md" >}}) them. |
| **Content-tree access** | Work with existing shapes, attachments, backgrounds, and headers/footers via `get_content()`. |
| **Images inside documents** | [Watermark the images embedded inside a document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-images/adding-watermark-to-images-inside-a-document.md" >}}). |
| **Tamper resistance** | [Lock watermarks]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/locking-watermark-in-word-processing-document.md" >}}), protect documents, and [rasterize PDF pages]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/rasterize-document-or-page.md" >}}). |
| **Document inspection** | [Read file type, page count, and size]({{< ref "watermark/python-net/developer-guide/basic-usage/get-document-info.md" >}}) without modifying the document. |
| **Streams** | Load input from file-like objects — handy for cloud blobs and HTTP bodies. |
| **On-premise** | No cloud calls, no Microsoft Office install, no network traffic. |

## Quick Example

Add a text watermark to a document and save the result with just a few lines of code:

{{< tabs "product-overview-add-watermark" >}}
{{< tab "quick_example.py" >}}
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color

def quick_example():
    # Open the document, add a text watermark, and save the result
    with Watermarker("./document.docx") as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 36))
        watermark.foreground_color = Color.red
        watermark.opacity = 0.5
        watermarker.add(watermark)
        watermarker.save("./watermarked.docx")

if __name__ == "__main__":
    quick_example()
```
{{< /tab >}}
{{< tab "document.docx" >}}
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/product-overview/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "watermarked.docx" >}}  
```text
Binary file (DOCX, 13 KB)
```
[Download full output](/watermark/python-net/_output_files/product-overview/quick_example/watermarked.docx)
{{< /tab >}}
{{< /tabs >}}

For finer control, scale, rotate, and center the watermark:

{{< tabs "product-overview-add-watermark-options" >}}
{{< tab "watermark_with_options.py" >}}
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color, SizingType
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment

def watermark_with_options():
    with Watermarker("./document.docx") as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 36))
        watermark.foreground_color = Color.red
        watermark.opacity = 0.5
        watermark.rotate_angle = 45.0
        # Scale the watermark relative to the page and center it
        watermark.sizing_type = SizingType.SCALE_TO_PARENT_DIMENSIONS
        watermark.scale_factor = 0.8
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER
        watermarker.add(watermark)
        watermarker.save("./watermarked.docx")

if __name__ == "__main__":
    watermark_with_options()
```
{{< /tab >}}
{{< tab "document.docx" >}}
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/product-overview/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "watermarked.docx" >}}  
```text
Binary file (DOCX, 13 KB)
```
[Download full output](/watermark/python-net/_output_files/product-overview/watermark_with_options/watermarked.docx)
{{< /tab >}}
{{< /tabs >}}

## Where to next

1. **Install the package** — [Installation]({{< ref "watermark/python-net/getting-started/installation" >}}) walks through PyPI and offline wheel installation for Windows, Linux, and macOS.
2. **Add your first watermark** — [Quick Start Guide]({{< ref "watermark/python-net/getting-started/quick-start-guide" >}}) stamps a document in five minutes.
3. **Explore the examples** — [How to Run Examples]({{< ref "watermark/python-net/getting-started/how-to-run-examples.md" >}}) clones the runnable repository and runs every documented scenario locally or in Docker.
4. **Use it in depth** — the [Developer Guide]({{< ref "watermark/python-net/developer-guide" >}}) covers adding, customizing, searching, modifying, and removing watermarks across every supported format.
5. **Licensing** — [Licensing and Subscription]({{< ref "watermark/python-net/getting-started/licensing-and-subscription.md" >}}) explains evaluation mode and how to apply a license.
