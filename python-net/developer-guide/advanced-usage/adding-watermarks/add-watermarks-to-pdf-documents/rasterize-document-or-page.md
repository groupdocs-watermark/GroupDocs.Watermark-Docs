---
id: rasterize-document-or-page
url: watermark/python-net/rasterize-document-or-page
title: Rasterize document or page
weight: 3
description: "Rasterize a PDF to make watermarks hard to remove using Python via .NET."
keywords: remove a watermark, watermark, rasterize pdf
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## How to remove a watermark from a PDF
Watermarks in PDFs can be removed by third-party tools. If you need watermarks that are very hard to remove, rasterize the document: convert pages to images so content becomes non-editable.

## Rasterize PDF document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    watermark = gww.TextWatermark("Do not copy", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0
    watermark.opacity = 0.5

    watermarker.add(watermark)
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    pdf_content.rasterize(100, 100, gwc_pdf.PdfImageConversionFormat.PNG)
    watermarker.save("document.pdf")
```

Note: You cannot restore document content after saving; rasterization increases file size.

## Rasterize particular page of the PDF document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc
import groupdocs.watermark.options.pdf as gwo_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    watermark = gww.TextWatermark("Do not copy", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0
    watermark.opacity = 0.5

    options = gwo_pdf.PdfArtifactWatermarkOptions()
    options.page_index = 0
    watermarker.add(watermark, options)

    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    pdf_content.pages[0].rasterize(100, 100, gwc_pdf.PdfImageConversionFormat.PNG)
    watermarker.save("document.pdf")
```


