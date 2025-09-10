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
This sample searches a specific page for objects matching image or text criteria and removes the found items.

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
These samples read and modify XObjects (reusable content) on PDF pages, including extracting info, deleting, watermarking images, and replacing text or images.

### Extracting information about all XObjects in PDF document
This sample iterates through all XObjects on all pages and prints basic image, text, position, size, and rotation details.

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
This sample removes XObjects by index and by reference from a selected page and then saves the document.

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
This sample scans XObjects for formatted text fragments and removes those that match a specific formatting condition (e.g., red foreground color).

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
This sample overlays a centered, rotated text watermark onto every image contained inside XObjects across all pages.

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
These samples demonstrate updating XObject text content, either plain replacement or with custom font and colors.

#### Replacing text
This sample finds XObjects whose text contains a target substring and replaces it with new plain text.

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
This sample clears existing formatted fragments and inserts new text with specific font, style, and colors.

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
This sample replaces the image content of XObjects with a new image loaded from disk.

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
These samples operate on PDF artifacts (headers, footers, watermarks, etc.), allowing extraction, deletion, conditional removal, watermarking, and content replacement.

### Extracting information about all artifacts in PDF document
This sample iterates all artifacts on all pages and prints type, image details, text, opacity, position, size, and rotation.

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
This sample removes artifacts by index and reference from a given page and saves the result.

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
This sample deletes artifacts that contain text fragments satisfying a formatting rule (for example, font size greater than a threshold).

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
This sample applies a centered, rotated text watermark to every artifact that contains an image.

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
These samples show how to replace artifact text directly or recreate it with custom formatting.

#### Replacing artifact text
This sample replaces plain artifact text when it contains a target substring.

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
This sample clears existing formatted text and adds new text with chosen font, style, and colors.

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
This sample replaces the image of matching artifacts with a new image loaded from disk.

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
These samples work with PDF annotations: extracting details, removing, conditionally deleting, watermarking images, and replacing text or images.

### Extracting information about all annotations in PDF document
This sample walks through all annotations on all pages and prints image stats, text, position, size, and rotation.

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
This sample removes annotations from a page using index and reference methods and saves the document.

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
This sample deletes annotations whose formatted text fragments meet a specific condition (e.g., a particular font family).

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
This sample places a centered, rotated text watermark over every annotation image in the document.

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
These samples demonstrate replacing annotation text, either plain or with full formatting control.

#### Replacing annotation text
This sample replaces plain annotation text when it contains a target substring.

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
This sample clears existing formatted annotation text and adds new formatted content with specific font and colors.

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
This sample replaces the image within annotations with a new image read from disk.

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


