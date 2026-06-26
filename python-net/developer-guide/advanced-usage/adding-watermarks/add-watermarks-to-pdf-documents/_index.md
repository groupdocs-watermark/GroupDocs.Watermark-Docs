---
id: add-watermarks-to-pdf-documents
url: watermark/python-net/add-watermarks-to-pdf-documents
title: Add watermarks to PDF documents
linkTitle: To PDF documents
weight: 6
description: "Add watermarks to specific PDF pages, images, and attachments using GroupDocs.Watermark for Python via .NET."
keywords: add watermarks to pdf, pdf watermark, page index, artifact, annotation, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark gives you fine-grained control over watermarks in PDF documents. Open the PDF with `PdfLoadOptions` and pass a PDF-specific watermark option (such as `PdfArtifactWatermarkOptions` or `PdfAnnotationWatermarkOptions`) to `add()` to target a particular page.

## Add a watermark to a particular page

Use `PdfArtifactWatermarkOptions` and set `page_index` (0-based) to place a watermark on a specific page. The example below adds a text watermark to the first page and an image watermark to the second.

{{< tabs "code-example-add-watermark-to-pdf-page">}}
{{< tab "add_watermark_to_page.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, ImageWatermark, Font, Color
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment
from groupdocs.watermark.options.pdf import PdfLoadOptions, PdfArtifactWatermarkOptions

def add_watermark_to_page():
    with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
        # Text watermark on the first page (page_index is 0-based)
        text_watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        text_watermark.foreground_color = Color.red
        text_watermark.horizontal_alignment = HorizontalAlignment.CENTER
        text_watermark.vertical_alignment = VerticalAlignment.CENTER
        text_options = PdfArtifactWatermarkOptions()
        text_options.page_index = 0
        watermarker.add(text_watermark, text_options)

        # Image watermark on the second page
        with ImageWatermark("./logo.png") as image_watermark:
            image_watermark.horizontal_alignment = HorizontalAlignment.RIGHT
            image_watermark.vertical_alignment = VerticalAlignment.TOP
            image_options = PdfArtifactWatermarkOptions()
            image_options.page_index = 1
            watermarker.add(image_watermark, image_options)

        watermarker.save("./output.pdf")

if __name__ == "__main__":
    add_watermark_to_page()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` (two pages) and `logo.png` are the sample files used in this example. Download [document.pdf](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/document.pdf) and [logo.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 221 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/add_watermark_to_page/output.pdf)
{{< /tab >}}
{{< /tabs >}}

`PdfAnnotationWatermarkOptions` works the same way and adds the watermark as a page annotation instead of an artifact; see [Watermarks in PDF document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/watermarks-in-pdf-document.md" >}}).

## Working with existing PDF content

Operations that read or modify the PDF **content tree** — watermarking the existing images on a page, reading a page's size, applying PDF page margins, and working with PDF attachments — are accessed through `Watermarker.get_content()`, which returns a `PdfContent` exposing `pages`, `attachments`, and more.

### Add a watermark to all images of a particular page

```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, SizingType
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment
from groupdocs.watermark.options.pdf import PdfLoadOptions

with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
    watermark = TextWatermark("Protected image", Font("Arial", 8.0))
    watermark.horizontal_alignment = HorizontalAlignment.CENTER
    watermark.vertical_alignment = VerticalAlignment.CENTER
    watermark.sizing_type = SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    pdf_content = watermarker.get_content()
    for image in pdf_content.pages[0].find_images():
        image.add(watermark)
    watermarker.save("./output.pdf")
```

For the full set of PDF content operations — XObjects, artifacts, and annotations; attachments; and rasterization — see the dedicated topics:

- [Watermarks in PDF document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/watermarks-in-pdf-document.md" >}})
- [Existing objects in PDF document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/existing-objects-in-pdf-document.md" >}})
- [Attachments in PDF document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/attachments-in-pdf-document.md" >}})
- [Rasterize document or page]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/rasterize-document-or-page.md" >}})
