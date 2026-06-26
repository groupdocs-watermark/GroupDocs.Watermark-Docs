---
id: adding-repeated-watermarks
url: watermark/python-net/adding-repeated-watermarks
title: Adding repeated watermarks
linkTitle: Repeated watermarks
weight: 3
description: "Add repeated (tiled) text or image watermarks with spacing, rotation, and patterns using GroupDocs.Watermark for Python via .NET."
keywords: add repeated watermarks, tiled watermarks, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Repeated (tiled) watermarks let you cover entire pages with a pattern of text or images. You can control spacing, rotation, offsets, and choose different tiling templates by setting `tile_options` on the watermark.

## Add a repeated text watermark

The example below tiles a diagonal text watermark across the whole page. The `line_spacing` and `watermark_spacing` are expressed as a percentage of the page, and `tile_type` selects the tiling template.

{{< tabs "code-example-adding-repeated-watermarks">}}
{{< tab "add_repeated_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import (
    TextWatermark, Font, Color, TextAlignment,
    TileOptions, TileType, MeasureValue, TileMeasureType,
)

def add_repeated_watermark():
    with Watermarker("./sample.pdf") as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        watermark.foreground_color = Color.gray
        watermark.opacity = 0.3
        watermark.rotate_angle = -45.0
        watermark.text_alignment = TextAlignment.CENTER

        # Spacing between lines and between repeated watermarks, as a percentage of the page
        line_spacing = MeasureValue()
        line_spacing.measure_type = TileMeasureType.PERCENT
        line_spacing.value = 12.0
        watermark_spacing = MeasureValue()
        watermark_spacing.measure_type = TileMeasureType.PERCENT
        watermark_spacing.value = 10.0

        # Tile the watermark across the whole page
        tile_options = TileOptions()
        tile_options.tile_type = TileType.ONE_THIRD_OFFSET
        tile_options.line_spacing = line_spacing
        tile_options.watermark_spacing = watermark_spacing
        watermark.tile_options = tile_options

        watermarker.add(watermark)
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    add_repeated_watermark()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}  
{{< tab-text >}}
`sample.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/basic-usage/adding-repeated-watermarks/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 401 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/adding-repeated-watermarks/add_repeated_watermark/output.pdf)
{{< /tab >}}
{{< /tabs >}}

You can replace the `TextWatermark` with an `ImageWatermark` to tile a logo or seal across the page in the same way — set the same `tile_options` on the image watermark.

{{< alert style="info" >}}
**Use case:** Protect sensitive PDFs by overlaying a tiled "Confidential" text across every page, or reinforce branding by repeating a logo in the background.
{{< /alert >}}
