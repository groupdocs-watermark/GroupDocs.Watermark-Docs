---
id: adding-text-watermarks
url: watermark/python-net/adding-text-watermarks
title: Adding text watermarks
linkTitle: Text watermarks
weight: 1
description: "Add text watermarks to pages, worksheets, slides or frames using Python via .NET."
keywords: add text watermarks, text watermarks
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Using text watermarks is an effective way to protect document content. By overlaying sensitive documents with watermarks such as "Confidential" or "Draft", you can deter unauthorized distribution and reinforce data security.

The following example shows how to add a text watermark to a document.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

with gw.Watermarker("sample.pdf") as watermarker:
    font = gww.Font("Arial", 19.0, gww.FontStyle.BOLD | gww.FontStyle.ITALIC)
    watermark = gww.TextWatermark("Test watermark", font)

    watermark.foreground_color = gww.Color.red
    watermark.background_color = gww.Color.blue
    watermark.text_alignment = gww.TextAlignment.RIGHT
    watermark.opacity = 0.5

    watermarker.add(watermark)
    watermarker.save("output.pdf")
```

If a document consists of multiple parts (pages, worksheets, slides, frames, etc.), the watermark will be added to each of them. You can configure this behavior via the `PagesSetup` property:

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww

with gw.Watermarker("sample.pdf") as watermarker:
    font = gww.Font("Arial", 19.0)
    watermark = gww.TextWatermark("Test watermark", font)

    watermark.pages_setup = gww.PagesSetup()
    watermark.pages_setup.pages = [1, 3]

    watermarker.add(watermark)
    watermarker.save("output.pdf")
```

## Sizing and positioning of watermark

### Absolute watermark positioning

You can add a watermark to an absolute position by setting `x`, `y`, `width`, and `height`. Values are measured in default document units.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww

with gw.Watermarker("image.png") as watermarker:
    font = gww.Font("Times New Roman", 8.0)
    watermark = gww.TextWatermark("Test watermark", font)

    watermark.x = 10
    watermark.y = 20
    watermark.width = 100
    watermark.height = 40

    watermarker.add(watermark)
    watermarker.save("image.png")
```

Note: the origin of coordinates may differ between formats (relative positioning has no such specifics and can be used as a unified approach).

### Relative watermark positioning

Instead of exact coordinates, use parent-relative alignment and set offsets with `margins`.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

with gw.Watermarker("image.png") as watermarker:
    font = gww.Font("Calibri", 12.0)
    watermark = gww.TextWatermark("Test watermark", font)
    watermark.horizontal_alignment = gwc.HorizontalAlignment.RIGHT
    watermark.vertical_alignment = gwc.VerticalAlignment.BOTTOM

    watermark.margins.right = 10
    watermark.margins.bottom = 5

    watermarker.add(watermark)
    watermarker.save("image.png")
```

### Using the MarginType property

Set relative margins using `MarginType`, where values are interpreted as a portion of the parent size (0.0–1.0).

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

with gw.Watermarker("image.png") as watermarker:
    font = gww.Font("Calibri", 12.0)
    watermark = gww.TextWatermark("Test watermark", font)
    watermark.horizontal_alignment = gwc.HorizontalAlignment.RIGHT
    watermark.vertical_alignment = gwc.VerticalAlignment.BOTTOM

    watermark.margins.margin_type = gww.MarginType.RELATIVE_TO_PARENT_DIMENSIONS
    watermark.margins.right = 0.1
    watermark.margins.bottom = 0.2

    watermarker.add(watermark)
    watermarker.save("image.png")
```

### Size types

Scale watermark depending on the parent size using `sizing_type` and `scale_factor`.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww

with gw.Watermarker("image.png") as watermarker:
    font = gww.Font("Calibri", 12.0)
    watermark = gww.TextWatermark("This is a test watermark", font)

    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 0.5

    watermarker.add(watermark)
    watermarker.save("image.png")
```

### Watermark rotation

Rotate watermark by setting `rotate_angle` in degrees. Positive values mean clockwise.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

with gw.Watermarker("test.docx") as watermarker:
    font = gww.Font("Calibri", 8.0)
    watermark = gww.TextWatermark("Test watermark", font)
    watermark.horizontal_alignment = gwc.HorizontalAlignment.RIGHT
    watermark.vertical_alignment = gwc.VerticalAlignment.TOP
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 0.5
    watermark.rotate_angle = 45

    watermarker.add(watermark)
    watermarker.save("test.docx")
```

### Using custom fonts

You can use custom TrueType fonts by specifying a folder path in the `Font` constructor.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww

fonts_folder = r"c:\\CustomFonts\\"
with gw.Watermarker("test.pdf") as watermarker:
    font = gww.Font("CustomFontName", fonts_folder, 36.0)
    watermark = gww.TextWatermark("Test watermark", font)

    watermark.foreground_color = gww.Color.blue
    watermark.opacity = 0.5
    watermark.x = 10
    watermark.y = 10

    watermarker.add(watermark)
    watermarker.save("result.pdf")
```

### Considering parent margins

By default, page margins are ignored and the maximum available space is used. To align with page margins, set `consider_parent_margins` to `True`.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

with gw.Watermarker("input.vsdx") as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 42.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.RIGHT
    watermark.vertical_alignment = gwc.VerticalAlignment.TOP
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0
    watermark.rotate_angle = 45
    watermark.foreground_color = gww.Color.red
    watermark.background_color = gww.Color.aqua
    watermark.consider_parent_margins = True

    watermarker.add(watermark)
    watermarker.save("input.vsdx")
```

## Watermark in documents of different types

Watermarks are represented by different objects in different formats. Some properties may not be supported for specific formats (for example, background color for WordArt in Word documents). See [Features Overview]({{< ref "watermark/python-net/getting-started/features-overview.md" >}}) for details.


