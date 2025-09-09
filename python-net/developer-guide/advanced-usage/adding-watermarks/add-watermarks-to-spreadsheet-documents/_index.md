---
id: add-watermarks-to-spreadsheet-documents
url: watermark/python-net/add-watermarks-to-spreadsheet-documents
title: Add watermarks to spreadsheet documents
linkTitle: To spreadsheets
weight: 8
description: "Add watermarks to worksheets, images, backgrounds, and headers/footers using Python via .NET."
keywords: add watermark, add watermark to the worksheets, Adding watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Adding watermark to a particular worksheet

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    text_watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 8.0))
    text_opts = gwo_xls.SpreadsheetWatermarkShapeOptions()
    text_opts.worksheet_index = 0
    watermarker.add(text_watermark, text_opts)

    with gww.ImageWatermark("logo.jpg") as image_watermark:
        img_opts = gwo_xls.SpreadsheetWatermarkShapeOptions()
        img_opts.worksheet_index = 1
        watermarker.add(image_watermark, img_opts)

    watermarker.save("spreadsheet.xlsx")
```

## Getting size of content area

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    print(content.worksheets[0].content_area_height)
    print(content.worksheets[0].content_area_width)
    print(content.worksheets[0].get_column_width(0))
    print(content.worksheets[0].get_row_height(0))
```

## Adding watermark to the images from a particular worksheet

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    images = content.worksheets[0].find_images()
    for image in images:
        image.add(watermark)
    watermarker.save("spreadsheet.xlsx")
```

## Different types of watermark in Excel documents

### Shapes and WordArt

Use `SpreadsheetWatermarkShapeOptions` or `SpreadsheetWatermarkModernWordArtOptions` when adding shape-based text watermarks.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    text_watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 8.0))
    options = gwo_xls.SpreadsheetWatermarkModernWordArtOptions()
    options.worksheet_index = 0
    watermarker.add(text_watermark, options)
    watermarker.save("spreadsheet.xlsx")
```

### Shape additional options

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Segoe UI", 19.0))
    options = gwo_xls.SpreadsheetWatermarkShapeOptions()
    options.name = "Shape 1"
    options.alternative_text = "Test watermark"
    options.is_locked = True
    watermarker.add(watermark, options)
    watermarker.save("spreadsheet.xlsx")
```

### Text effects

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls
import groupdocs.watermark.common as gwc

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Segoe UI", 19.0))
    effects = gwo_xls.SpreadsheetTextEffects()
    effects.line_format.enabled = True
    effects.line_format.color = gww.Color.red
    effects.line_format.dash_style = gwc.OfficeDashStyle.DASH_DOT_DOT
    effects.line_format.line_style = gwc.OfficeLineStyle.TRIPLE
    effects.line_format.weight = 1
    options = gwo_xls.SpreadsheetWatermarkShapeOptions()
    options.effects = effects
    watermarker.add(watermark, options)
    watermarker.save("spreadsheet.xlsx")
```

### Image effects

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    with gww.ImageWatermark("logo.png") as watermark:
        effects = gwo_xls.SpreadsheetImageEffects()
        effects.brightness = 0.7
        effects.contrast = 0.6
        effects.chroma_key = gww.Color.red
        effects.border_line_format.enabled = True
        effects.border_line_format.weight = 1
        options = gwo_xls.SpreadsheetWatermarkShapeOptions()
        options.effects = effects
        watermarker.add(watermark, options)
    watermarker.save("spreadsheet.xlsx")
```

### Worksheet backgrounds

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    with gww.ImageWatermark("logo.gif") as watermark:
        options = gwo_xls.SpreadsheetBackgroundWatermarkOptions()
        watermarker.add(watermark, options)
    watermarker.save("spreadsheet.xlsx")
```

### Worksheet background image size

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls
import groupdocs.watermark.contents.spreadsheet as gwc_xls
import groupdocs.watermark.common as gwc

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Segoe UI", 19.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 90
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 0.5
    watermark.opacity = 0.5

    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    options = gwo_xls.SpreadsheetBackgroundWatermarkOptions()
    options.background_width = content.worksheets[0].content_area_width_px
    options.background_height = content.worksheets[0].content_area_height_px
    watermarker.add(watermark, options)
    watermarker.save("spreadsheet.xlsx")
```

### Header and footer image watermark

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls
import groupdocs.watermark.common as gwc

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    with gww.ImageWatermark("logo.png") as watermark:
        watermark.vertical_alignment = gwc.VerticalAlignment.TOP
        watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
        watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
        watermark.scale_factor = 1.0
        options = gwo_xls.SpreadsheetWatermarkHeaderFooterOptions()
        options.worksheet_index = 0
        watermarker.add(watermark, options)
    watermarker.save("spreadsheet.xlsx")
```

### Header and footer text watermark

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.spreadsheet as gwo_xls
import groupdocs.watermark.common as gwc

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Segoe UI", 19.0, gww.FontStyle.BOLD))
    watermark.foreground_color = gww.Color.red
    watermark.background_color = gww.Color.aqua
    watermark.vertical_alignment = gwc.VerticalAlignment.TOP
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    options = gwo_xls.SpreadsheetWatermarkHeaderFooterOptions()
    options.worksheet_index = 0
    watermarker.add(watermark, options)
    watermarker.save("spreadsheet.xlsx")
```

## Advanced use cases

- [Shapes in spreadsheet document]({{< ref "shapes-in-spreadsheet-document" >}})
- [Working with spreadsheet document attachments]({{< ref "working-with-spreadsheet-document-attachments" >}})
- [Working with worksheet backgrounds]({{< ref "working-with-worksheet-backgrounds" >}})
- [Working with worksheet headers and footers]({{< ref "working-with-worksheet-headers-and-footers" >}})

