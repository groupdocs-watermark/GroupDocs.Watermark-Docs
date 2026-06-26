---
id: add-text
url: watermark/python-net/add-text
title: Add text watermarks
linkTitle: Add text watermarks
weight: 1
description: "This article shows how to add a text watermark to a document and save the result with GroupDocs.Watermark for Python via .NET."
keywords: add text watermark, add text watermark to image, text watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

One of the main features of GroupDocs.Watermark is adding text watermarks to documents. You can add watermarks to documents or images from a local path, as well as from a stream. For a full list of supported formats, check [Supported document formats]({{< ref "watermark/python-net/getting-started/supported-document-formats.md" >}}).

## Add a text watermark

To add a text watermark, follow these steps:

1. Open the document by passing its path (or a stream) to the [Watermarker](https://reference.groupdocs.com/watermark/python-net/) class, using a `with` block so the document is released automatically.
2. Create a `TextWatermark` with the desired text and `Font`.
3. Style the watermark — for example, set `foreground_color` and alignment.
4. Call `add()` to apply the watermark and `save()` to write the result.

{{< tabs "code-example-add-text">}}
{{< tab "add_text_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment

def add_text_watermark():
    with Watermarker("./sample.pdf") as watermarker:
        # Build the text watermark and style it
        watermark = TextWatermark("Top Secret", Font("Arial", 36.0))
        watermark.foreground_color = Color.red
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER
        watermark.rotate_angle = 45.0
        watermark.opacity = 0.4

        watermarker.add(watermark)
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    add_text_watermark()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}  
{{< tab-text >}}
`sample.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/basic-usage/add-text/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 352 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/add-text/add_text_watermark/output.pdf)
{{< /tab >}}
{{< /tabs >}}

Run the program. A new watermarked document appears at the specified path.

## What's next

GroupDocs.Watermark offers many more capabilities for text watermarks — background and foreground colors, custom fonts, opacity, rotation, tiling, and absolute or relative positioning. See [Adding text watermarks]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}}) in the advanced guide.
