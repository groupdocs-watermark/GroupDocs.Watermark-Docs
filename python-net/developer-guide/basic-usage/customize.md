---
id: rotate
url: watermark/python-net/basic-usage/customize
title: Customize watermarks
weight: 4
description: "Adjust text or image watermark appearance and position using Python via .NET."
keywords: rotate watermark, position watermark, move watermark, scale watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark lets you control how a watermark looks and where it appears.

## Customizing text watermarks

GroupDocs.Watermark lets you fully control the look and position of text watermarks. Adjust color, font, alignment, rotation, opacity, and scaling to match your document’s style.

Use `TextWatermark` properties like `foreground_color`, `opacity`, `rotate_angle`, `sizing_type`, `scale_factor`, `horizontal_alignment`, `vertical_alignment`, `x`, `y`, `width`, `height`, and `consider_parent_margins`.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

with gw.Watermarker("C:\\Docs\\sample.docx") as watermarker:
    watermark = gww.TextWatermark("Customized watermark.", gww.Font("Arial", 24.0, gww.FontStyle.BOLD))
    watermark.foreground_color = gww.Color.dark_orange
    watermark.consider_parent_margins = True
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.TOP
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.rotate_angle = 45
    watermark.scale_factor = 0.7
    watermarker.add(watermark)
    watermarker.save("C:\\Docs\\watermarked-sample.docx")
```
🔹 Use case: Apply branded or legal disclaimers in a consistent style across pages (e.g., “Confidential – Do Not Distribute”).

## Customizing image watermarks

You can also personalize image watermarks by adjusting their alignment, rotation, opacity, and layering. This allows you to place logos, stamps, or seals exactly where needed.

Use `ImageWatermark` with similar properties for position, rotation, background/foreground layering, and opacity.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

with gw.Watermarker("C:\\Docs\\seagull.jpg") as watermarker:
    watermark = gww.ImageWatermark("C:\\Docs\\greetings-stamp.png")
    watermark.horizontal_alignment = gwc.HorizontalAlignment.RIGHT
    watermark.vertical_alignment = gwc.VerticalAlignment.TOP
    watermark.rotate_angle = 15
    watermark.is_background = False
    watermark.opacity = 0.8
    watermarker.add(watermark)
    watermarker.save("C:\\Docs\\custom-image-watermark.jpg")
```
🔹 Use case: Place a semi-transparent company logo in the corner of each page, or overlay a stamp image for approvals and certifications.

