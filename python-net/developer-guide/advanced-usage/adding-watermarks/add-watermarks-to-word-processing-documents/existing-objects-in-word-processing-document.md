---
id: existing-objects-in-word-processing-document
url: watermark/python-net/existing-objects-in-word-processing-document
title: Existing objects in word processing document
weight: 1
description: "Remove, inspect, and modify shapes (potential watermarks) in Word documents using Python via .NET."
keywords: document structure, remove shape
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Watermarks in Word documents are usually represented by shapes. Using GroupDocs.Watermark you can remove shapes of any type from any level of the document structure, or inspect and modify them.

## Removing watermark from a particular section

Steps:

1. Load the document
2. Create and initialize image or text search criteria
3. Find possible watermarks
4. Remove found watermarks
5. Save the document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp
import groupdocs.watermark.search.searchcriteria as gws_sc

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    image_criteria = gws_sc.ImageDctHashSearchCriteria("logo.png")
    text_criteria = gws_sc.TextSearchCriteria("Company Name")

    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    possible = content.sections[0].search(text_criteria.or_(image_criteria))

    for i in range(len(possible) - 1, -1, -1):
        possible.remove_at(i)

    watermarker.save("document.docx")
```

### Search for particular header or footer

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp
import groupdocs.watermark.search.searchcriteria as gws_sc
import groupdocs.watermark.common as gwc

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    image_criteria = gws_sc.ImageDctHashSearchCriteria("logo.png")
    text_criteria = gws_sc.TextSearchCriteria("Company Name")

    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    header_footer = content.sections[0].headers_footers[gwc.OfficeHeaderFooterType.HEADER_PRIMARY]
    possible = header_footer.search(text_criteria.or_(image_criteria))

    for i in range(len(possible) - 1, -1, -1):
        possible.remove_at(i)

    watermarker.save("document.docx")
```

## Extracting information about all shapes in a Word document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for section in content.sections:
        for shape in section.shapes:
            if shape.header_footer is not None:
                print("In header/footer")

            print(shape.shape_type)
            print(shape.width)
            print(shape.height)
            print(shape.is_word_art)
            print(shape.rotate_angle)
            print(shape.alternative_text)
            print(shape.name)
            print(shape.x)
            print(shape.y)
            print(shape.text)

            if shape.image is not None:
                print(shape.image.width)
                print(shape.image.height)
                print(len(shape.image.get_bytes()))

            print(shape.horizontal_alignment)
            print(shape.vertical_alignment)
            print(shape.relative_horizontal_position)
            print(shape.relative_vertical_position)
```

## Working with shape types

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for section in content.sections:
        for shape in section.shapes:
            if shape.shape_type == gwc_wp.WordProcessingShapeType.DIAGONAL_CORNERS_ROUNDED:
                print("Diagonal Corners Rounded shape found")
                shape.formatted_text_fragments.add(
                    "I am Diagonal Corner Rounded",
                    gww.Font("Calibri", 8.0, gww.FontStyle.BOLD),
                    gww.Color.red,
                    gww.Color.aqua,
                )

    watermarker.save("document.docx")
```

## Removing a particular shape

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)

    # Remove shape by index
    content.sections[0].shapes.remove_at(0)

    # Remove shape by reference
    shp = content.sections[0].shapes[0]
    content.sections[0].shapes.remove(shp)

    watermarker.save("document.docx")
```

## Removing shapes with particular text formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp
import groupdocs.watermark.watermarks as gww

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for section in content.sections:
        for i in range(section.shapes.count - 1, -1, -1):
            for fragment in section.shapes[i].formatted_text_fragments:
                if fragment.foreground_color == gww.Color.red and fragment.font.family_name == "Arial":
                    section.shapes.remove_at(i)
                    break

    watermarker.save("document.docx")
```

## Removing or replacing hyperlink associated with a particular shape

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)

    # Replace hyperlink
    content.sections[0].shapes[0].hyperlink = "https://www.groupdocs.com/"

    # Remove hyperlink
    content.sections[0].shapes[1].hyperlink = None

    watermarker.save("document.docx")
```

## Replacing text for particular shapes

### Replacing shape's text

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for shape in content.sections[0].shapes:
        if "Some text" in (shape.text or ""):
            shape.text = "Another text"

    watermarker.save("document.docx")
```

### Replacing shape's text with formatted text

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp
import groupdocs.watermark.watermarks as gww

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for shape in content.sections[0].shapes:
        if "Some text" in (shape.text or ""):
            shape.formatted_text_fragments.clear()
            shape.formatted_text_fragments.add(
                "Another text",
                gww.Font("Calibri", 19.0, gww.FontStyle.BOLD),
                gww.Color.red,
                gww.Color.aqua,
            )

    watermarker.save("document.docx")
```

## Replacing shape's image

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for shape in content.sections[0].shapes:
        if shape.image is not None:
            with open("test.png", "rb") as f:
                img_bytes = f.read()
            shape.image = gwc_wp.WordProcessingWatermarkableImage(img_bytes)

    watermarker.save("document.docx")
```

## Modifying shape properties

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for shape in content.sections[0].shapes:
        if "Some text" in (shape.text or ""):
            shape.alternative_text = "watermark"
            shape.rotate_angle = 30
            shape.x = 200
            shape.y = 200
            shape.height = 100
            shape.width = 400
            shape.behind_text = False

    watermarker.save("document.docx")
```


