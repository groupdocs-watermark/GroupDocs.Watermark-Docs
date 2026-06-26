---
id: add-watermarks-to-word-processing-documents
url: watermark/python-net/add-watermarks-to-word-processing-documents
title: Add watermarks to word processing documents
linkTitle: To word-processing documents
weight: 9
description: "Add watermarks to a particular section, page, or the headers and footers of a Word document using GroupDocs.Watermark for Python via .NET."
keywords: add watermark, word watermark, section, headers and footers, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Microsoft Word documents can be divided into multiple sections, and headers and footers are associated with those sections. Open the document with `WordProcessingLoadOptions` and pass a Word-specific watermark option to `add()` to target a particular section or page.

## Add a watermark to a particular section

Use `WordProcessingWatermarkSectionOptions` and set `section_index` to place a watermark in a specific section.

{{< tabs "code-example-add-watermark-to-word-section">}}
{{< tab "add_watermark_to_section.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment
from groupdocs.watermark.options.word_processing import (
    WordProcessingLoadOptions, WordProcessingWatermarkSectionOptions,
)

def add_watermark_to_section():
    with Watermarker("./document.docx", WordProcessingLoadOptions()) as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 36.0))
        watermark.foreground_color = Color.red
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER
        watermark.rotate_angle = 45.0

        options = WordProcessingWatermarkSectionOptions()
        options.section_index = 0
        watermarker.add(watermark, options)

        watermarker.save("./output.docx")

if __name__ == "__main__":
    add_watermark_to_section()
```
{{< /tab >}}
{{< tab "document.docx" >}}  
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 13 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/add_watermark_to_section/output.docx)
{{< /tab >}}
{{< /tabs >}}

To watermark only specific pages, use `WordProcessingWatermarkPagesOptions` and set `page_numbers`.

## Working with existing content

`Watermarker.get_content()` returns a `WordProcessingContent` that exposes the document's `sections`, their shapes, and their headers and footers. For example, to add a watermark to every image inside the first section:

```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font
from groupdocs.watermark.options.word_processing import WordProcessingLoadOptions

with Watermarker("./document.docx", WordProcessingLoadOptions()) as watermarker:
    watermark = TextWatermark("Protected image", Font("Arial", 8.0))
    content = watermarker.get_content()
    for image in content.sections[0].find_images():
        image.add(watermark)
    watermarker.save("./output.docx")
```

For the full set of Word content operations — shape effects, locking, protection, and working with existing shapes and headers/footers — see the dedicated topics:

- [Watermarks in word processing document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/watermarks-in-word-processing-document.md" >}})
- [Existing objects in word processing document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/existing-objects-in-word-processing-document.md" >}})
- [Locking watermark in word processing document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/locking-watermark-in-word-processing-document.md" >}})
- [Protecting word processing documents]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/protecting-word-processing-documents.md" >}})
