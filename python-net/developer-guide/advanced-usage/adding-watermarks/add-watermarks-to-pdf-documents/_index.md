---
id: add-watermarks-to-pdf-documents
url: watermark/python-net/add-watermarks-to-pdf-documents
title: Add watermarks to PDF documents
linkTitle: To PDF documents
weight: 6
description: "Add watermarks to PDF pages, images, and attachments using Python via .NET."
keywords: add watermarks to pdf, watermarking API, adding watermarks
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Add watermarks to PDF documents
Add watermarks to a particular page or to all images/attachments on a page.

### Adding watermark to a particular page

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.pdf as gwo_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    text_watermark = gww.TextWatermark("This is a test watermark", gww.Font("Arial", 8.0))
    text_opts = gwo_pdf.PdfArtifactWatermarkOptions()
    text_opts.page_index = 0
    watermarker.add(text_watermark, text_opts)

    with gww.ImageWatermark("protect.jpg") as img_wm:
        img_opts = gwo_pdf.PdfArtifactWatermarkOptions()
        img_opts.page_index = 1
        watermarker.add(img_wm, img_opts)

    watermarker.save("document.pdf")
```

### Adding watermark to all images of a particular page

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    images = pdf_content.pages[0].find_images()
    for image in images:
        image.add(watermark)
    watermarker.save("document.pdf")
```

### Getting page size

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    print(pdf_content.pages[0].width)
    print(pdf_content.pages[0].height)
```

### Page margins in PDF document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 42.0))
    watermark.horizontal_alignment = gww.HorizontalAlignment.RIGHT if hasattr(gww, 'HorizontalAlignment') else 0
    watermark.vertical_alignment = gww.VerticalAlignment.TOP if hasattr(gww, 'VerticalAlignment') else 0
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    pdf_content.page_margin_type = gwc_pdf.PdfPageMarginType.BLEED_BOX
    watermark.consider_parent_margins = True

    watermarker.add(watermark)
    watermarker.save("document.pdf")
```

### Add watermark to all attachments

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww
from groupdocs.watermark.common import FileType

watermark = gww.TextWatermark("This is WaterMark on Attachment", gww.Font("Arial", 19.0))

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for attachment in pdf_content.attachments:
        info = attachment.get_document_info()
        if info.file_type != FileType.UNKNOWN and not info.is_encrypted:
            with attachment.create_watermarker() as attached:
                attached.add(watermark)
                attached.save()
    watermarker.save("document.pdf")
```

### Advanced use cases

- [Attachments in PDF document]({{< ref "attachments-in-pdf-document" >}})
- [Existing objects in PDF document]({{< ref "existing-objects-in-pdf-document" >}})
- [Rasterize document or page]({{< ref "rasterize-document-or-page" >}})
- [Watermarks in PDF document]({{< ref "watermarks-in-pdf-document" >}})


