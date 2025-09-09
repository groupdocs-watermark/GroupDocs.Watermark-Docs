---
id: watermarks-in-pdf-document
url: watermark/python-net/watermarks-in-pdf-document
title: Watermarks in PDF document
weight: 4
description: "Add watermarks as XObjects, Artifacts, and Annotations using Python via .NET."
keywords: Watermarks in PDF, watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Learn the ways GroupDocs.Watermark adds watermarks in PDF documents.

## XObjects

When `add` on `Watermarker` is called, a simple XObject is added to the PDF.

Image XObject and Form XObject are used to add `ImageWatermark` and `TextWatermark` respectively. XObjects are page real content and are not removed by Adobe Acrobat sanitization.

## Artifacts

Watermarks can be represented by artifacts. Add an artifact watermark using `PdfArtifactWatermarkOptions`.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.options.pdf as gwo_pdf
import groupdocs.watermark.common as gwc

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    options = gwo_pdf.PdfArtifactWatermarkOptions()

    text_watermark = gww.TextWatermark("This is an artifact watermark", gww.Font("Arial", 8.0))
    text_watermark.horizontal_alignment = gwc.HorizontalAlignment.RIGHT
    watermarker.add(text_watermark, options)

    with gww.ImageWatermark("logo.bmp") as image_watermark:
        watermarker.add(image_watermark, options)

    watermarker.save("document.pdf")
```

## Annotations

Add annotation watermarks using `PdfAnnotationWatermarkOptions`.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.options.pdf as gwo_pdf
import groupdocs.watermark.common as gwc

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    options = gwo_pdf.PdfAnnotationWatermarkOptions()

    text_watermark = gww.TextWatermark("This is a annotation watermark", gww.Font("Arial", 8.0))
    text_watermark.horizontal_alignment = gwc.HorizontalAlignment.LEFT
    text_watermark.vertical_alignment = gwc.VerticalAlignment.TOP
    watermarker.add(text_watermark, options)

    with gww.ImageWatermark("protect.jpg") as image_watermark:
        image_watermark.horizontal_alignment = gwc.HorizontalAlignment.RIGHT
        image_watermark.vertical_alignment = gwc.VerticalAlignment.TOP
        watermarker.add(image_watermark, options)

    watermarker.save("document.pdf")
```

## Print-only annotations

Make an annotation print-only using `print_only`.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.pdf as gwo_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    text_watermark = gww.TextWatermark(
        "This is a print only test watermark. It won't appear in view mode.",
        gww.Font("Arial", 8.0),
    )

    options = gwo_pdf.PdfAnnotationWatermarkOptions()
    options.page_index = 0
    options.print_only = True

    watermarker.add(text_watermark, options)
    watermarker.save("document.pdf")
```


