---
id: existing-objects-in-pdf-document
url: watermark/python-net/existing-objects-in-pdf-document
title: Existing objects in PDF document
weight: 2
description: "Remove or modify PDF page objects (XObjects, artifacts, annotations) using Python via .NET."
keywords: Removing watermark, watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Removing watermark from a particular page

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.search.searchcriteria as gws_sc

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    image_criteria = gws_sc.ImageDctHashSearchCriteria("logo.png")
    text_criteria = gws_sc.TextSearchCriteria("Company Name")

    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    possible = pdf_content.pages[0].search(image_criteria.or_(text_criteria))
    for i in range(len(possible) - 1, -1, -1):
        possible.remove_at(i)

    watermarker.save("document.pdf")
```

## Working with XObjects

### Extracting information about all XObjects in PDF document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for page in pdf_content.pages:
        for xobj in page.x_objects:
            if xobj.image is not None:
                print(xobj.image.width)
                print(xobj.image.height)
                print(len(xobj.image.get_bytes()))

            print(xobj.text)
            print(xobj.x)
            print(xobj.y)
            print(xobj.width)
            print(xobj.height)
            print(xobj.rotate_angle)
```

### Removing a particular XObject

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    page = pdf_content.pages[0]
    page.x_objects.remove_at(0)
    page.x_objects.remove(page.x_objects[0])
    watermarker.save("document.pdf")
```

### Removing XObjects containing text with particular text formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for page in pdf_content.pages:
        for i in range(page.x_objects.count - 1, -1, -1):
            for fragment in page.x_objects[i].formatted_text_fragments:
                if fragment.foreground_color == gww.Color.red:
                    page.x_objects.remove_at(i)
                    break

    watermarker.save("document.pdf")
```

### Adding watermark to all image XObjects

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    for page in pdf_content.pages:
        for xobj in page.x_objects:
            if xobj.image is not None:
                xobj.image.add(watermark)

    watermarker.save("document.pdf")
```

### Replacing text for particular XObjects

#### Replacing text

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for xobj in pdf_content.pages[0].x_objects:
        if "Test" in (xobj.text or ""):
            xobj.text = "Passed"

    watermarker.save("document.pdf")
```

#### Replacing text with formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for xobj in pdf_content.pages[0].x_objects:
        if "Test" in (xobj.text or ""):
            xobj.formatted_text_fragments.clear()
            xobj.formatted_text_fragments.add(
                "Passed", gww.Font("Calibri", 19.0, gww.FontStyle.BOLD), gww.Color.red, gww.Color.aqua
            )

    watermarker.save("document.pdf")
```

### Replacing image for particular XObjects

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for xobj in pdf_content.pages[0].x_objects:
        if xobj.image is not None:
            with open("test.png", "rb") as f:
                xobj.image = gwc_pdf.PdfWatermarkableImage(f.read())

    watermarker.save("document.pdf")
```

## Working with artifacts

### Extracting information about all artifacts in PDF document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for page in pdf_content.pages:
        for artifact in page.artifacts:
            print(artifact.artifact_type)
            print(artifact.artifact_subtype)
            if artifact.image is not None:
                print(artifact.image.width)
                print(artifact.image.height)
                print(len(artifact.image.get_bytes()))

            print(artifact.text)
            print(artifact.opacity)
            print(artifact.x)
            print(artifact.y)
            print(artifact.width)
            print(artifact.height)
            print(artifact.rotate_angle)
```

### Removing a particular artifact

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    page = pdf_content.pages[0]
    page.artifacts.remove_at(0)
    page.artifacts.remove(page.artifacts[0])
    watermarker.save("document.pdf")
```

### Removing artifacts containing text with particular text formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for page in pdf_content.pages:
        for i in range(page.artifacts.count - 1, -1, -1):
            for fragment in page.artifacts[i].formatted_text_fragments:
                if fragment.font.size > 42:
                    page.artifacts.remove_at(i)
                    break

    watermarker.save("document.pdf")
```

### Adding watermark to all image artifacts

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    for page in pdf_content.pages:
        for artifact in page.artifacts:
            if artifact.image is not None:
                artifact.image.add(watermark)

    watermarker.save("document.pdf")
```

### Replacing text for particular artifacts

#### Replacing artifact text

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for artifact in pdf_content.pages[0].artifacts:
        if "Test" in (artifact.text or ""):
            artifact.text = "Passed"

    watermarker.save("document.pdf")
```

#### Replacing artifact text with formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for artifact in pdf_content.pages[0].artifacts:
        if "Test" in (artifact.text or ""):
            artifact.formatted_text_fragments.clear()
            artifact.formatted_text_fragments.add(
                "Passed", gww.Font("Calibri", 19.0, gww.FontStyle.BOLD), gww.Color.red, gww.Color.aqua
            )

    watermarker.save("document.pdf")
```

### Replacing image for particular artifacts

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for artifact in pdf_content.pages[0].artifacts:
        if artifact.image is not None:
            with open("test.png", "rb") as f:
                artifact.image = gwc_pdf.PdfWatermarkableImage(f.read())

    watermarker.save("document.pdf")
```

## Working with annotations

### Extracting information about all annotations in PDF document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for page in pdf_content.pages:
        for annotation in page.annotations:
            print(annotation.annotation_type)
            if annotation.image is not None:
                print(annotation.image.width)
                print(annotation.image.height)
                print(len(annotation.image.get_bytes()))

            print(annotation.text)
            print(annotation.x)
            print(annotation.y)
            print(annotation.width)
            print(annotation.height)
            print(annotation.rotate_angle)
```

### Removing a particular annotation

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    page = pdf_content.pages[0]
    page.annotations.remove_at(0)
    page.annotations.remove(page.annotations[0])
    watermarker.save("document.pdf")
```

### Removing annotations containing text with particular text formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for page in pdf_content.pages:
        for i in range(page.annotations.count - 1, -1, -1):
            for fragment in page.annotations[i].formatted_text_fragments:
                if fragment.font.family_name == "Verdana":
                    page.annotations.remove_at(i)
                    break

    watermarker.save("document.pdf")
```

### Adding watermark to all image annotations

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    for page in pdf_content.pages:
        for annotation in page.annotations:
            if annotation.image is not None:
                annotation.image.add(watermark)

    watermarker.save("document.pdf")
```

### Replacing text for particular annotations

#### Replacing annotation text

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for annotation in pdf_content.pages[0].annotations:
        if "Test" in (annotation.text or ""):
            annotation.text = "Passed"

    watermarker.save("document.pdf")
```

#### Replacing annotation text with formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
import groupdocs.watermark.watermarks as gww

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for annotation in pdf_content.pages[0].annotations:
        if "Test" in (annotation.text or ""):
            annotation.formatted_text_fragments.clear()
            annotation.formatted_text_fragments.add(
                "Passed", gww.Font("Calibri", 19.0, gww.FontStyle.BOLD), gww.Color.red, gww.Color.aqua
            )

    watermarker.save("document.pdf")
```

### Replacing image for particular annotations

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for annotation in pdf_content.pages[0].annotations:
        if annotation.image is not None:
            with open("test.png", "rb") as f:
                annotation.image = gwc_pdf.PdfWatermarkableImage(f.read())

    watermarker.save("document.pdf")
```


