---
id: shapes-in-spreadsheet-document
url: watermark/python-net/shapes-in-spreadsheet-document
title: Shapes in spreadsheet document
weight: 1
description: "Inspect, modify, and remove shapes in Excel documents using Python via .NET."
keywords: extracting information about all shapes, Removing a particular shape, Replacing shape image
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Extracting information about all shapes in an Excel document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for worksheet in content.worksheets:
        for shape in worksheet.shapes:
            print(shape.auto_shape_type)
            print(shape.mso_drawing_type)
            print(shape.text)
            if shape.image is not None:
                print(shape.image.width)
                print(shape.image.height)
                print(len(shape.image.get_bytes())))

            print(shape.id)
            print(shape.alternative_text)
            print(shape.x)
            print(shape.y)
            print(shape.width)
            print(shape.height)
            print(shape.rotate_angle)
            print(shape.is_word_art)
            print(shape.name)
```

## Removing a particular shape

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    content.worksheets[0].shapes.remove_at(0)
    content.worksheets[0].shapes.remove(content.worksheets[0].shapes[0])
    watermarker.save("spreadsheet.xlsx")
```

## Removing shapes with particular text formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls
import groupdocs.watermark.watermarks as gww

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for worksheet in content.worksheets:
        for i in range(worksheet.shapes.count - 1, -1, -1):
            for fragment in worksheet.shapes[i].formatted_text_fragments:
                if fragment.foreground_color == gww.Color.red and fragment.font.family_name == "Arial":
                    worksheet.shapes.remove_at(i)
                    break
    watermarker.save("spreadsheet.xlsx")
```

## Removing/replacing hyperlink associated with a particular shape

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    content.worksheets[0].charts[0].hyperlink = "https://www.aspose.com/"
    content.worksheets[0].shapes[0].hyperlink = "https://www.groupdocs.com/"
    content.worksheets[1].charts[0].hyperlink = None
    content.worksheets[1].shapes[0].hyperlink = None
    watermarker.save("spreadsheet.xlsx")
```

## Replacing text for particular shapes

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for shape in content.worksheets[0].shapes:
        if shape.text == "© Aspose 2016":
            shape.text = "© GroupDocs 2017"
    watermarker.save("spreadsheet.xlsx")
```

## Replacing text for particular shapes with formatted text

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls
import groupdocs.watermark.watermarks as gww

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for shape in content.worksheets[0].shapes:
        if shape.text == "© Aspose 2016":
            shape.formatted_text_fragments.clear()
            shape.formatted_text_fragments.add(
                "© GroupDocs 2017",
                gww.Font("Calibri", 19.0, gww.FontStyle.BOLD),
                gww.Color.red,
                gww.Color.aqua,
            )
    watermarker.save("spreadsheet.xlsx")
```

## Replacing shape image

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for shape in content.worksheets[0].shapes:
        if shape.image is not None:
            with open("test.png", "rb") as f:
                shape.image = gwc_xls.SpreadsheetWatermarkableImage(f.read())
    watermarker.save("spreadsheet.xlsx")
```

## Setting background image for particular shapes

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for shape in content.worksheets[0].shapes:
        if shape.text == "© Aspose 2016":
            with open("test.png", "rb") as f:
                shape.image_fill_format.background_image = gwc_xls.SpreadsheetWatermarkableImage(f.read())
            shape.image_fill_format.transparency = 0.5
            shape.image_fill_format.tile_as_texture = True
    watermarker.save("spreadsheet.xlsx")
```

## Updating shape properties

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for shape in content.worksheets[0].shapes:
        if shape.text == "© Aspose 2019":
            shape.alternative_text = "watermark"
            shape.rotate_angle = 30
            shape.x = 200
            shape.y = 200
            shape.width = 400
            shape.height = 100
    watermarker.save("spreadsheet.xlsx")
```


