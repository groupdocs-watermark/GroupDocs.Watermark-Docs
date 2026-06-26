---
id: adding-image-watermarks
url: watermark/python-net/adding-image-watermarks
title: Adding image watermarks
linkTitle: Image watermarks
weight: 2
description: "Add image watermarks from a file or a stream using GroupDocs.Watermark for Python via .NET."
keywords: image watermark, add image watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark supports adding the following image formats as watermarks:

- BMP
- PNG
- GIF
- JPEG

## Add an image watermark from a local file

The following example adds an `ImageWatermark` to a document. If the document consists of multiple parts (pages, worksheets, slides, frames, etc.), the watermark is added to each of them.

{{< tabs "code-example-adding-image-watermarks">}}
{{< tab "add_image_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import ImageWatermark, SizingType
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment

def add_image_watermark():
    with Watermarker("./sample.docx") as watermarker:
        with ImageWatermark("./logo.png") as watermark:
            watermark.horizontal_alignment = HorizontalAlignment.CENTER
            watermark.vertical_alignment = VerticalAlignment.CENTER
            watermark.sizing_type = SizingType.SCALE_TO_PARENT_DIMENSIONS
            watermark.scale_factor = 0.5
            watermark.opacity = 0.7
            watermarker.add(watermark)
        watermarker.save("./output.docx")

if __name__ == "__main__":
    add_image_watermark()
```
{{< /tab >}}
{{< tab "sample.docx" >}}  
{{< tab-text >}}
`sample.docx` and `logo.png` are the sample files used in this example. Download [sample.docx](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks/sample.docx) and [logo.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 125 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks/add_image_watermark/output.docx)
{{< /tab >}}
{{< /tabs >}}

## Add an image watermark from a stream

You can also initialize an `ImageWatermark` from a stream — pass it as the `stream` argument.

{{< tabs "code-example-adding-image-watermarks-stream">}}
{{< tab "add_image_watermark_from_stream.py" >}}  
```python
import io
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import ImageWatermark

def add_image_watermark_from_stream():
    with open("./logo.png", "rb") as f:
        data = f.read()

    with Watermarker("./sample.docx") as watermarker:
        with ImageWatermark(stream=io.BytesIO(data)) as watermark:
            watermarker.add(watermark)
        watermarker.save("./output.docx")

if __name__ == "__main__":
    add_image_watermark_from_stream()
```
{{< /tab >}}
{{< tab "sample.docx" >}}  
{{< tab-text >}}
`sample.docx` and `logo.png` are the sample files used in this example. Download [sample.docx](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks/sample.docx) and [logo.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 120 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks/add_image_watermark_from_stream/output.docx)
{{< /tab >}}
{{< /tabs >}}

For advanced watermark properties (tiling, alignment, sizing, rotation, and margins), the same techniques shown for text watermarks apply to image watermarks. See [Adding text watermarks]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}}).
