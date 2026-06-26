---
id: working-with-worksheet-headers-and-footers
url: watermark/python-net/working-with-worksheet-headers-and-footers
title: Working with worksheet headers and footers
linkTitle: Working with headers and footers
weight: 4
description: "Inspect, clear, and watermark the images in Excel worksheet headers and footers using GroupDocs.Watermark for Python via .NET."
keywords: worksheet headers and footers, excel, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Each worksheet has a collection of header/footer slots, available through `SpreadsheetContent.worksheets[i].headers_footers`. Each slot has a `header_footer_type` and three `sections` (left, center, right), and each section can carry a `script` (text) or an `image`.

## Extract information about headers and footers

{{< tabs "code-example-worksheet-headers-footers">}}
{{< tab "extract_headers_footers.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.spreadsheet import SpreadsheetLoadOptions

def extract_headers_footers():
    with Watermarker("./spreadsheet.xlsx", SpreadsheetLoadOptions()) as watermarker:
        content = watermarker.get_content()
        worksheet = content.worksheets[0]
        print(f"Worksheet 0 header/footer slots: {len(worksheet.headers_footers)}")
        for header_footer in worksheet.headers_footers:
            sections = list(header_footer.sections)
            with_content = [s for s in sections if s.image is not None or s.script]
            print(f"  type={header_footer.header_footer_type} "
                  f"sections={len(sections)} with_content={len(with_content)}")

if __name__ == "__main__":
    extract_headers_footers()
```
{{< /tab >}}
{{< tab "spreadsheet.xlsx" >}}  
{{< tab-text >}}
`spreadsheet.xlsx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/working-with-worksheet-headers-and-footers/spreadsheet.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "extract-headers-footers.txt" >}}  
```text
Worksheet 0 header/footer slots: 6
  type=0 sections=3 with_content=0
  type=1 sections=3 with_content=0
  type=2 sections=3 with_content=0
  type=3 sections=3 with_content=0
  type=4 sections=3 with_content=0
  type=5 sections=3 with_content=0
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-worksheet-headers-and-footers/extract_headers_footers/extract-headers-footers.txt)
{{< /tab >}}
{{< /tabs >}}

## Clear and watermark header/footer content

To clear a section, set its `image` and `script` to `None`. To watermark the existing header/footer images, add a watermark to each non-empty `image`:

{{< tabs "code-example-worksheet-headers-footers-watermark">}}
{{< tab "watermark_headers_footers.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font
from groupdocs.watermark.options.spreadsheet import SpreadsheetLoadOptions

def watermark_headers_footers():
    with Watermarker("./spreadsheet.xlsx", SpreadsheetLoadOptions()) as watermarker:
        watermark = TextWatermark("Protected", Font("Arial", 8.0))
        content = watermarker.get_content()
        for worksheet in content.worksheets:
            for header_footer in worksheet.headers_footers:
                for section in header_footer.sections:
                    if section.image is not None:
                        section.image.add(watermark)
        watermarker.save("./output.xlsx")

if __name__ == "__main__":
    watermark_headers_footers()
```
{{< /tab >}}
{{< tab "spreadsheet.xlsx" >}}  
{{< tab-text >}}
`spreadsheet.xlsx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/working-with-worksheet-headers-and-footers/spreadsheet.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.xlsx" >}}  
```text
Binary file (XLSX, 9 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-worksheet-headers-and-footers/watermark_headers_footers/output.xlsx)
{{< /tab >}}
{{< /tabs >}}

To add a fresh header/footer watermark instead, use `SpreadsheetWatermarkHeaderFooterOptions` (see the [section index]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents" >}})).
