---
id: rasterize-document-or-page
url: watermark/python-net/rasterize-document-or-page
title: Rasterize document or page
linkTitle: Rasterize document or page
weight: 3
description: "Rasterize a PDF — convert pages to images — so that watermarks become hard to remove, using GroupDocs.Watermark for Python via .NET."
keywords: rasterize pdf, non-editable watermark, flatten pdf, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Watermarks in PDFs can be removed by third-party tools. If you need watermarks that are very hard to remove, **rasterize** the document: convert its pages to images so the content — including the watermark — becomes non-editable. Access the PDF content tree with `Watermarker.get_content()` and call `rasterize()`.

{{< alert style="warning" >}}
Rasterization is irreversible: the original text and vector content cannot be restored afterwards, and the output file size usually increases.
{{< /alert >}}

## Rasterize the whole document

The example adds a watermark, rasterizes every page to a PNG image at 100 DPI, and saves the result.

{{< tabs "code-example-rasterize-document">}}
{{< tab "rasterize_document.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.options.pdf import PdfLoadOptions
from groupdocs.watermark.contents.pdf import PdfImageConversionFormat

def rasterize_document():
    with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        watermark.foreground_color = Color.red
        watermarker.add(watermark)

        # Rasterize every page at 100x100 DPI to PNG images
        content = watermarker.get_content()
        content.rasterize(100, 100, PdfImageConversionFormat.PNG)

        watermarker.save("./output.pdf")

if __name__ == "__main__":
    rasterize_document()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 1.1 MB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/rasterize-document-or-page/rasterize_document/output.pdf)
{{< /tab >}}
{{< /tabs >}}

## Rasterize a particular page

To rasterize a single page, call `rasterize()` on that page instead of the whole content:

{{< tabs "code-example-rasterize-page">}}
{{< tab "rasterize_page.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.pdf import PdfLoadOptions
from groupdocs.watermark.contents.pdf import PdfImageConversionFormat

def rasterize_page():
    with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
        content = watermarker.get_content()
        content.pages[0].rasterize(100, 100, PdfImageConversionFormat.PNG)
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    rasterize_page()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 570 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/rasterize-document-or-page/rasterize_page/output.pdf)
{{< /tab >}}
{{< /tabs >}}
