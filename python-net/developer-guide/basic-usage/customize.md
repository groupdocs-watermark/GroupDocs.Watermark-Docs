---
id: customize
url: watermark/python-net/basic-usage/customize
title: Customize watermarks
linkTitle: Customize watermarks
weight: 4
description: "Adjust text or image watermark appearance and position — color, font, rotation, opacity, sizing, and alignment — using GroupDocs.Watermark for Python via .NET."
keywords: rotate watermark, position watermark, move watermark, scale watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark lets you control how a watermark looks and where it appears. Adjust color, font, alignment, rotation, opacity, and scaling to match your document's style.

## Customize text watermarks

Use `TextWatermark` properties such as `foreground_color`, `opacity`, `rotate_angle`, `sizing_type`, `scale_factor`, `horizontal_alignment`, `vertical_alignment`, `x`, `y`, `width`, `height`, and `consider_parent_margins`. The example below scales a "DRAFT" watermark to the page, rotates it 45°, and makes it half-transparent.

{{< tabs "code-example-customize">}}
{{< tab "customize_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color, SizingType
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment

def customize_watermark():
    with Watermarker("./sample.pdf") as watermarker:
        watermark = TextWatermark("DRAFT", Font("Arial", 42.0))
        watermark.foreground_color = Color.dark_orange
        # Scale the watermark relative to the page and rotate it
        watermark.sizing_type = SizingType.SCALE_TO_PARENT_DIMENSIONS
        watermark.scale_factor = 0.7
        watermark.rotate_angle = 45.0
        watermark.opacity = 0.5
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER

        watermarker.add(watermark)
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    customize_watermark()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}  
{{< tab-text >}}
`sample.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/basic-usage/customize/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 351 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/customize/customize_watermark/output.pdf)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="info" >}}
**Use case:** Apply branded or legal disclaimers in a consistent style across pages (for example, "Confidential – Do Not Distribute").
{{< /alert >}}

## Customize image watermarks

Image watermarks support the same positioning, rotation, and opacity properties. Place a logo, stamp, or seal exactly where you need it:

{{< tabs "code-example-customize-image">}}
{{< tab "customize_image_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import ImageWatermark
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment

def customize_image_watermark():
    with Watermarker("./sample.pdf") as watermarker:
        with ImageWatermark("./stamp.png") as watermark:
            watermark.horizontal_alignment = HorizontalAlignment.RIGHT
            watermark.vertical_alignment = VerticalAlignment.TOP
            watermark.rotate_angle = 15.0
            watermark.opacity = 0.8
            watermarker.add(watermark)
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    customize_image_watermark()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}  
{{< tab-text >}}
`sample.pdf` and `stamp.png` are the sample files used in this example. Download [sample.pdf](/watermark/python-net/_sample_files/developer-guide/basic-usage/customize/sample.pdf) and [stamp.png](/watermark/python-net/_sample_files/developer-guide/basic-usage/customize/stamp.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 307 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/customize/customize_image_watermark/output.pdf)
{{< /tab >}}
{{< /tabs >}}
