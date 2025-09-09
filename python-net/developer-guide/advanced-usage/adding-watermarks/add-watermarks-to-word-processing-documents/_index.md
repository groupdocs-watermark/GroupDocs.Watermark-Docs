---
id: add-watermarks-to-word-processing-documents
url: watermark/python-net/add-watermarks-to-word-processing-documents
title: Add watermarks to word processing documents
linkTitle: To word-processing documents
weight: 9
description: "Add watermarks in headers and footers of any section using Python via .NET."
keywords: add watermark, add watermark in headers and footers
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Microsoft Word documents can be divided into multiple sections. Headers and footers are associated with sections and are commonly used to display text or graphics across pages. You can add watermarks into headers/footers of a particular section or target specific pages.

## Adding watermark to a particular section

Steps:

1. Load the document
2. Create and initialize watermark object
3. Set watermark properties
4. Create `WordProcessingWatermarkSectionOptions` and set `section_index`
5. Add watermark to the section
6. Save the document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 19.0))

    options = gwo_wp.WordProcessingWatermarkSectionOptions()
    options.section_index = 0

    watermarker.add(watermark, options)
    watermarker.save("document.docx")
```

## Getting page size

Get page setup of a section when using absolute positioning/sizing.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    print(content.sections[0].page_setup.width)
    print(content.sections[0].page_setup.height)
    print(content.sections[0].page_setup.top_margin)
    print(content.sections[0].page_setup.right_margin)
    print(content.sections[0].page_setup.bottom_margin)
    print(content.sections[0].page_setup.left_margin)
```

## Adding watermark to the images inside a particular section

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    images = content.sections[0].find_images()
    for image in images:
        image.add(watermark)

    watermarker.save("document.docx")
```

## Adding watermark to the image shapes in a word document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for section in content.sections:
        for shape in section.shapes:
            if shape.header_footer is None and shape.image is not None:
                shape.image.add(watermark)

    watermarker.save("document.docx")
```

## Adding watermark to a particular page of word document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    text_watermark = gww.TextWatermark("DRAFT", gww.Font("Arial", 42.0))

    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    options = gwo_wp.WordProcessingWatermarkPagesOptions()
    options.page_numbers = [content.page_count]

    watermarker.add(text_watermark, options)
    watermarker.save("document.docx")
```

## Working with headers and footers

### Linking headers and footers

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp
import groupdocs.watermark.common as gwc

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    content.sections[1].headers_footers[gwc.OfficeHeaderFooterType.FOOTER_EVEN].is_linked_to_previous = True
    watermarker.save("document.docx")
```

### Linking all headers and footers

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for i in range(1, content.sections.count):
        content.sections[i].headers_footers.link_to_previous(True)
    watermarker.save("document.docx")
```

### Add watermark to headers and footers with linking

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    with gww.ImageWatermark("large.png") as watermark:
        options = gwo_wp.WordProcessingWatermarkSectionOptions()
        options.section_index = 0
        watermarker.add(watermark, options)

    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    for i in range(1, content.sections.count):
        content.sections[i].headers_footers.link_to_previous(True)

    watermarker.save("document.docx")
```

### Setting different headers or footers

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.wordprocessing as gwc_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    content = watermarker.get_content(gwc_wp.WordProcessingContent)
    content.sections[0].page_setup.different_first_page_header_footer = True
    content.sections[0].page_setup.odd_and_even_pages_header_footer = True
    watermarker.save("document.docx")
```

## Advanced use cases

- [Existing objects in word processing document]({{< ref "existing-objects-in-word-processing-document" >}})
- [Locking watermark in word processing document]({{< ref "locking-watermark-in-word-processing-document" >}})
- [Protecting word processing documents]({{< ref "protecting-word-processing-documents" >}})
- [Watermarks in word processing document]({{< ref "watermarks-in-word-processing-document" >}})


