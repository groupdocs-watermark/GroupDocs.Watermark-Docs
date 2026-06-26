---
id: watermarks-in-pdf-document
url: watermark/python-net/watermarks-in-pdf-document
title: Watermarks in PDF document
linkTitle: Watermarks in PDF document
weight: 4
description: "Add watermarks to a PDF as XObjects, Artifacts, or Annotations — including print-only annotations — using GroupDocs.Watermark for Python via .NET."
keywords: watermarks in pdf, xobject, artifact, annotation, print only, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

A PDF watermark can be added in three different ways, each with its own trade-offs:

- **XObjects** — added to the real page content. They are not removed by simple sanitization, which makes them the hardest to remove.
- **Artifacts** — added as page artifacts. Use `PdfArtifactWatermarkOptions`.
- **Annotations** — added as page annotations. Use `PdfAnnotationWatermarkOptions`; these can be made **print-only** so they appear when the document is printed but are hidden on screen.

## Add artifact and annotation watermarks

The example below adds an artifact text watermark, an annotation text watermark, and a **print-only** annotation image watermark.

{{< tabs "code-example-pdf-watermarks">}}
{{< tab "add_pdf_watermarks.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, ImageWatermark, Font
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment
from groupdocs.watermark.options.pdf import (
    PdfLoadOptions, PdfArtifactWatermarkOptions, PdfAnnotationWatermarkOptions,
)

def add_pdf_watermarks():
    with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
        # Add as an artifact
        artifact_text = TextWatermark("Artifact", Font("Arial", 8.0))
        artifact_text.horizontal_alignment = HorizontalAlignment.RIGHT
        watermarker.add(artifact_text, PdfArtifactWatermarkOptions())

        # Add as an annotation
        annotation_text = TextWatermark("Annotation", Font("Arial", 8.0))
        annotation_text.horizontal_alignment = HorizontalAlignment.LEFT
        annotation_text.vertical_alignment = VerticalAlignment.TOP
        watermarker.add(annotation_text, PdfAnnotationWatermarkOptions())

        # Add a print-only annotation (visible when printed, hidden on screen)
        with ImageWatermark("./logo.png") as image_watermark:
            image_watermark.horizontal_alignment = HorizontalAlignment.RIGHT
            image_watermark.vertical_alignment = VerticalAlignment.TOP
            options = PdfAnnotationWatermarkOptions()
            options.print_only = True
            watermarker.add(image_watermark, options)

        watermarker.save("./output.pdf")

if __name__ == "__main__":
    add_pdf_watermarks()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` and `logo.png` are the sample files used in this example. Download [document.pdf](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/document.pdf) and [logo.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 528 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/watermarks-in-pdf-document/add_pdf_watermarks/output.pdf)
{{< /tab >}}
{{< /tabs >}}

To work with watermarks already present in a PDF — extracting, modifying, or removing existing XObjects, artifacts, and annotations — see [Existing objects in PDF document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/existing-objects-in-pdf-document.md" >}}).
