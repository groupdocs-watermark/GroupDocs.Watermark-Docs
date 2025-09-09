---
id: working-with-worksheet-backgrounds
url: watermark/python-net/working-with-worksheet-backgrounds
title: Working with worksheet backgrounds
linkTitle: Working with backgrounds
weight: 3
description: "Extract, remove, and watermark worksheet backgrounds using Python via .NET."
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Extracting information about all worksheet backgrounds in an Excel document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for worksheet in content.worksheets:
        if worksheet.background_image is not None:
            print(worksheet.background_image.width)
            print(worksheet.background_image.height)
            print(len(worksheet.background_image.get_bytes()))
```

## Removing a particular background

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    content.worksheets[0].background_image = None
    watermarker.save("spreadsheet.xlsx")
```

## Adding watermark to all backgrounds in an Excel worksheet

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for worksheet in content.worksheets:
        if worksheet.background_image is not None:
            worksheet.background_image.add(watermark)
    watermarker.save("spreadsheet.xlsx")
```

## Settings background image for charts

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    with open("test.png", "rb") as f:
        content.worksheets[0].charts[0].image_fill_format.background_image = \
            gwc_xls.SpreadsheetWatermarkableImage(f.read())
    content.worksheets[0].charts[0].image_fill_format.transparency = 0.5
    content.worksheets[0].charts[0].image_fill_format.tile_as_texture = True
    watermarker.save("spreadsheet.xlsx")
```


