---
id: add-watermarks-to-images
url: watermark/python-net/add-watermarks-to-images
title: Add watermarks to images
linkTitle: To images
weight: 5
description: "Add watermarks to single or multi-framed images (such as TIFF and GIF) using GroupDocs.Watermark for Python via .NET."
keywords: add watermark, image watermark, tiff, gif, frame, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark adds watermarks to raster images, including multi-frame formats such as TIFF and GIF. For multi-frame images, open the file with the format-specific load options and target a frame with the matching watermark option.

## Add a watermark to a particular frame

Open a TIFF with `TiffImageLoadOptions` and use `TiffImageWatermarkOptions` with `frame_index` to watermark a specific frame.

{{< tabs "code-example-add-watermark-to-image">}}
{{< tab "add_watermark_to_image.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment
from groupdocs.watermark.options.image import TiffImageLoadOptions, TiffImageWatermarkOptions

def add_watermark_to_image():
    with Watermarker("./image.tiff", TiffImageLoadOptions()) as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        watermark.foreground_color = Color.red
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER

        options = TiffImageWatermarkOptions()
        options.frame_index = 0
        watermarker.add(watermark, options)

        watermarker.save("./output.tiff")

if __name__ == "__main__":
    add_watermark_to_image()
```
{{< /tab >}}
{{< tab "image.tiff" >}}  
{{< tab-text >}}
`image.tiff` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-images/image.tiff) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.tiff" >}}  
```text
Binary file (TIFF, 364 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-images/add_watermark_to_image/output.tiff)
{{< /tab >}}
{{< /tabs >}}

For a single-frame image (BMP, PNG, JPEG), open it directly with `Watermarker("photo.png")` and add the watermark without frame options. To watermark the images embedded **inside** a document, see [Adding watermark to images inside a document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-images/adding-watermark-to-images-inside-a-document.md" >}}).
