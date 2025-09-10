---
id: working-with-spreadsheet-document-attachments
url: watermark/python-net/working-with-spreadsheet-document-attachments
title: Working with spreadsheet document attachments
linkTitle: Working with attachments
weight: 2
description: "Extract, add, remove, search, and watermark spreadsheet attachments using Python via .NET."
keywords: watermarking API, spreadsheet attachments, Extract all attachments
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Extract all attachments from Excel document
This sample walks worksheets and lists metadata for each attachment, including placement, preview image size, and file details.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for worksheet in content.worksheets:
        for attachment in worksheet.attachments:
            print("Alternative text:", attachment.alternative_text)
            print("Attachment frame x-coordinate:", attachment.x)
            print("Attachment frame y-coordinate:", attachment.y)
            print("Attachment frame width:", attachment.width)
            print("Attachment frame height:", attachment.height)
            print("Preview image size:", len(attachment.preview_image_content) if attachment.preview_image_content else 0)
            if attachment.is_link:
                print("Full path to the attached file:", attachment.source_full_name)
            else:
                info = attachment.get_document_info()
                print("File type:", info.file_type)
                print("Name of the source file:", attachment.source_full_name)
                print("File size:", len(attachment.content))
```

## Add an attachment to Excel document
This sample embeds a file into a worksheet with a preview image and frame coordinates/sizes.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    worksheet = content.worksheets[0]
    with open("document.docx", "rb") as f_doc, open("document_preview.png", "rb") as f_prev:
        worksheet.attachments.add_attachment(
            f_doc.read(),
            "sample document.docx",
            f_prev.read(),
            50,
            100,
            200,
            400,
        )
    watermarker.save("spreadsheet.xlsx")
```

## Add linked attachment to Excel document
This sample adds a link to an external file with a preview image and placement settings.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    worksheet = content.worksheets[0]
    with open("document_preview.png", "rb") as f_prev:
        worksheet.attachments.add_link(
            "document.docx",
            f_prev.read(),
            50,
            100,
            200,
            400,
        )
    watermarker.save("spreadsheet.xlsx")
```

## Remove attachment from Excel document
This sample removes attachments based on conditions (e.g., broken link paths or encrypted files).

```python
import os
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for worksheet in content.worksheets:
        for i in range(worksheet.attachments.count - 1, -1, -1):
            attachment = worksheet.attachments[i]
            if (attachment.is_link and not os.path.exists(attachment.source_full_name)) or \
               attachment.get_document_info().is_encrypted:
                worksheet.attachments.remove_at(i)
    watermarker.save("spreadsheet.xlsx")
```

## Add watermark to all attachments
This sample opens each non-encrypted attached file and applies a text watermark in-place.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.spreadsheet as gwc_xls
import groupdocs.watermark.watermarks as gww
from groupdocs.watermark.common import FileType

watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 19.0))

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options) as watermarker:
    content = watermarker.get_content(gwc_xls.SpreadsheetContent)
    for worksheet in content.worksheets:
        for attachment in worksheet.attachments:
            info = attachment.get_document_info()
            if info.file_type != FileType.UNKNOWN and not info.is_encrypted:
                with attachment.create_watermarker() as attached_watermarker:
                    attached_watermarker.add(watermark)
                    attached_watermarker.save()
    watermarker.save("spreadsheet.xlsx")
```

## Search for images in attached files
This sample searches inside attached files for image watermarks using DCT hash matching and reports findings.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.objects as gws_objs
import groupdocs.watermark.search.searchcriteria as gws_sc

settings = gw.WatermarkerSettings()
settings.searchable_objects.spreadsheet_searchable_objects = gws_objs.SpreadsheetSearchableObjects.ATTACHED_IMAGES

load_options = gw.SpreadsheetLoadOptions()
with gw.Watermarker("spreadsheet.xlsx", load_options, settings) as watermarker:
    criteria = gws_sc.ImageDctHashSearchCriteria("attachment.png")
    possible = watermarker.search(criteria)
    print("Found", possible.count, "possible watermark(s).")
```


