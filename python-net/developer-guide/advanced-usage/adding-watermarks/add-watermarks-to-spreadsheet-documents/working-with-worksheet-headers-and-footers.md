---
id: working-with-worksheet-headers-and-footers
url: watermark/python-net/working-with-worksheet-headers-and-footers
title: Working with worksheet headers and footers
linkTitle: Working with headers and footers
weight: 4
description: "Inspect, clear, and watermark images in headers and footers using Python via .NET."
keywords:  worksheet headers and footers
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Extracting information about all headers and footers in an Excel document
This sample enumerates all headers/footers and prints section details, including image stats and script content.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for worksheet in content.worksheets:
        for header_footer in worksheet.headers_footers:
            print(header_footer.header_footer_type)
            for section in header_footer.sections:
                print(section.section_type)
                if section.image is not None:
                    print(section.image.width)
                    print(section.image.height)
                    print(len(section.image.get_bytes()))
                print(section.script)
```

## Clearing a particular header or footer
This sample clears both text and image content from a chosen header or footer type on a worksheet.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls
import groupdocs.watermark.common as gwc

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for section in content.worksheets[0].headers_footers[gwc.OfficeHeaderFooterType.HEADER_PRIMARY].sections:
        section.script = None
        section.image = None
    watermarker.save("spreadsheet.xlsx")
```

## Clearing a particular section of header or footer
This sample targets a specific header/footer section and clears its image and script.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls
import groupdocs.watermark.common as gwc

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    section = content.worksheets[0].headers_footers[gwc.OfficeHeaderFooterType.HEADER_EVEN].sections[gwc_xls.SpreadsheetHeaderFooterSectionType.LEFT]
    section.image = None
    section.script = None
    watermarker.save("spreadsheet.xlsx")
```

## Adding watermark to all images in header and footer
This sample applies a centered, rotated text watermark over all header/footer images across worksheets.

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
        for header_footer in worksheet.headers_footers:
            for section in header_footer.sections:
                if section.image is not None:
                    section.image.add(watermark)
    watermarker.save("spreadsheet.xlsx")
```


