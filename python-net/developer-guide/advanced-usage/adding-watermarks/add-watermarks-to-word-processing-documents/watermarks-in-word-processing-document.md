---
id: watermarks-in-word-processing-document
url: watermark/python-net/watermarks-in-word-processing-document
title: Watermarks in word processing document
weight: 4
description: "Add shape-based watermarks to Word documents with additional options using Python via .NET."
keywords: add watermarks, how to add watermarks
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

When adding a watermark in Microsoft Word, a shape with appropriate content is placed in section headers. GroupDocs.Watermark uses the same approach. When calling `add` on `Watermarker`, a shape is added to the document.

## Using properties of WordProcessingWatermarkBaseOptions

Set additional options like `name` and `alternative_text` when adding a shape watermark.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp
import groupdocs.watermark.common as gwc

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 19.0))
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.rotate_angle = 25.0
    watermark.foreground_color = gww.Color.red
    watermark.opacity = 1.0

    options = gwo_wp.WordProcessingWatermarkSectionOptions()
    options.name = "Shape 1"
    options.alternative_text = "Test watermark"

    watermarker.add(watermark, options)
    watermarker.save("document.docx")
```

## Using WordProcessingTextEffects

Apply text effects to shape watermarks.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp
import groupdocs.watermark.common as gwc

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 19.0))

    effects = gwo_wp.WordProcessingTextEffects()
    effects.line_format.enabled = True
    effects.line_format.color = gww.Color.red
    effects.line_format.dash_style = gwc.OfficeDashStyle.DASH_DOT_DOT
    effects.line_format.line_style = gwc.OfficeLineStyle.TRIPLE
    effects.line_format.weight = 1

    options = gwo_wp.WordProcessingWatermarkSectionOptions()
    options.effects = effects

    watermarker.add(watermark, options)
    watermarker.save("document.docx")
```

## Using WordProcessingImageEffects

Apply image effects to image-based shape watermarks.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    with gww.ImageWatermark("logo.png") as watermark:
        effects = gwo_wp.WordProcessingImageEffects()
        effects.brightness = 0.7
        effects.contrast = 0.6
        effects.chroma_key = gww.Color.red
        effects.border_line_format.enabled = True
        effects.border_line_format.weight = 1

        options = gwo_wp.WordProcessingWatermarkSectionOptions()
        options.effects = effects

        watermarker.add(watermark, options)

    watermarker.save("document.docx")
```


