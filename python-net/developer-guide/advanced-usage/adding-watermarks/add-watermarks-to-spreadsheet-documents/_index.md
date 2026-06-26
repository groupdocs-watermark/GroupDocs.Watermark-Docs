---
id: add-watermarks-to-spreadsheet-documents
url: watermark/python-net/add-watermarks-to-spreadsheet-documents
title: Add watermarks to spreadsheet documents
linkTitle: To spreadsheets
weight: 8
description: "Add watermarks to a particular worksheet, and work with shapes, backgrounds, and headers/footers using GroupDocs.Watermark for Python via .NET."
keywords: add watermark, spreadsheet watermark, worksheet, background, headers and footers, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Open a spreadsheet with `SpreadsheetLoadOptions` and pass a spreadsheet-specific watermark option to `add()` to target a particular worksheet, a background, or a header/footer.

## Add a watermark to a particular worksheet

Use `SpreadsheetWatermarkShapeOptions` and set `worksheet_index` to add the watermark as a shape on a specific worksheet.

{{< tabs "code-example-add-watermark-to-worksheet">}}
{{< tab "add_watermark_to_worksheet.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment
from groupdocs.watermark.options.spreadsheet import (
    SpreadsheetLoadOptions, SpreadsheetWatermarkShapeOptions,
)

def add_watermark_to_worksheet():
    with Watermarker("./spreadsheet.xlsx", SpreadsheetLoadOptions()) as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        watermark.foreground_color = Color.red
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER

        options = SpreadsheetWatermarkShapeOptions()
        options.worksheet_index = 0
        watermarker.add(watermark, options)

        watermarker.save("./output.xlsx")

if __name__ == "__main__":
    add_watermark_to_worksheet()
```
{{< /tab >}}
{{< tab "spreadsheet.xlsx" >}}  
{{< tab-text >}}
`spreadsheet.xlsx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/spreadsheet.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.xlsx" >}}  
```text
Binary file (XLSX, 48 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/add_watermark_to_worksheet/output.xlsx)
{{< /tab >}}
{{< /tabs >}}

Other worksheet placements are available through dedicated options — `SpreadsheetBackgroundWatermarkOptions` (worksheet background) and `SpreadsheetWatermarkHeaderFooterOptions` (header/footer). `Watermarker.get_content()` returns a `SpreadsheetContent` exposing each worksheet's shapes, charts, backgrounds, headers/footers, and attachments.

For the full set of spreadsheet content operations, see the dedicated topics:

- [Shapes in spreadsheet document]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/shapes-in-spreadsheet-document.md" >}})
- [Working with spreadsheet document attachments]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-spreadsheet-document-attachments.md" >}})
- [Working with worksheet backgrounds]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-worksheet-backgrounds.md" >}})
- [Working with worksheet headers and footers]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-worksheet-headers-and-footers.md" >}})
