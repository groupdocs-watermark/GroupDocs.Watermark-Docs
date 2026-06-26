---
id: add-image
url: watermark/python-net/add-image
title: Add image watermarks
linkTitle: Add image watermarks
weight: 2
description: "This article shows how to add an image watermark to a document and save the result with GroupDocs.Watermark for Python via .NET."
keywords: add image watermark, add image watermark to image, image watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

One of the main features of GroupDocs.Watermark is adding image watermarks to documents. You can add watermarks to documents or images from a local path, as well as from a stream. For a full list of supported formats, check [Supported document formats]({{< ref "watermark/python-net/getting-started/supported-document-formats.md" >}}).

## Add an image watermark

To add an image watermark, follow these steps:

1. Open the document by passing its path (or a stream) to the `Watermarker` class.
2. Create an `ImageWatermark` from the watermark image file (or a stream).
3. Position the watermark — for example, set `horizontal_alignment`, `vertical_alignment`, and `opacity`.
4. Call `add()` to apply the watermark and `save()` to write the result.

{{< tabs "code-example-add-image">}}
{{< tab "add_image_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import ImageWatermark
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment

def add_image_watermark():
    with Watermarker("./sample.docx") as watermarker:
        # Build an image watermark from a logo file and center it
        watermark = ImageWatermark("./logo.png")
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER
        watermark.opacity = 0.7

        watermarker.add(watermark)
        watermarker.save("./output.docx")

if __name__ == "__main__":
    add_image_watermark()
```
{{< /tab >}}
{{< tab "sample.docx" >}}  
{{< tab-text >}}
`sample.docx` and `logo.png` are the sample files used in this example. Download [sample.docx](/watermark/python-net/_sample_files/developer-guide/basic-usage/add-image/sample.docx) and [logo.png](/watermark/python-net/_sample_files/developer-guide/basic-usage/add-image/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 125 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/add-image/add_image_watermark/output.docx)
{{< /tab >}}
{{< /tabs >}}

## What's next

GroupDocs.Watermark offers more capabilities for image watermarks — loading from streams, scaling, tiling, and absolute or relative positioning. See [Adding image watermarks]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks.md" >}}) in the advanced guide.
