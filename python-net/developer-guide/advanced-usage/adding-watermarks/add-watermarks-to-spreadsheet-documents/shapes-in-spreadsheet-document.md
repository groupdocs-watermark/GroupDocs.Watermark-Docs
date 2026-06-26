---
id: shapes-in-spreadsheet-document
url: watermark/python-net/shapes-in-spreadsheet-document
title: Shapes in spreadsheet document
linkTitle: Shapes in spreadsheet document
weight: 1
description: "Inspect, modify, and remove shapes in Excel worksheets using GroupDocs.Watermark for Python via .NET."
keywords: excel shapes, word art, remove shape, replace shape image, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

`Watermarker.get_content()` returns a `SpreadsheetContent` whose `worksheets` each expose a `shapes` collection (along with `charts`, `attachments`, and `background_image`). You can iterate the shapes to read their properties, modify them, or remove them.

## Extract information about shapes

{{< tabs "code-example-spreadsheet-shapes">}}
{{< tab "extract_shapes.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.spreadsheet import SpreadsheetLoadOptions

def extract_shapes():
    with Watermarker("./spreadsheet.xlsx", SpreadsheetLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for i, worksheet in enumerate(content.worksheets):
            print(f"Worksheet {i}: shapes={len(worksheet.shapes)}")
            for shape in worksheet.shapes:
                text = (shape.text or "").strip()
                print(f"  shape text={text!r} size={round(shape.width)}x{round(shape.height)} "
                      f"word_art={shape.is_word_art}")

if __name__ == "__main__":
    extract_shapes()
```
{{< /tab >}}
{{< tab "spreadsheet.xlsx" >}}  
{{< tab-text >}}
`spreadsheet.xlsx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/shapes-in-spreadsheet-document/spreadsheet.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "extract-shapes.txt" >}}  
```text
Worksheet 0: shapes=0
Worksheet 1: shapes=0
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/shapes-in-spreadsheet-document/extract_shapes/extract-shapes.txt)
{{< /tab >}}
{{< /tabs >}}

Each shape exposes `text`, `image`, `name`, `alternative_text`, `x`, `y`, `width`, `height`, `rotate_angle`, and `is_word_art`.

## Remove and modify shapes

The `shapes` collection supports `remove_at(index)` and `remove(shape)`. Iterate in reverse when removing by index:

{{< tabs "code-example-spreadsheet-remove-shapes">}}
{{< tab "remove_and_modify_shapes.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.spreadsheet import SpreadsheetLoadOptions

def remove_and_modify_shapes():
    with Watermarker("./spreadsheet.xlsx", SpreadsheetLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for worksheet in content.worksheets:
            for i in range(len(worksheet.shapes) - 1, -1, -1):
                if worksheet.shapes[i].text == "CONFIDENTIAL":
                    worksheet.shapes.remove_at(i)
        watermarker.save("./output.xlsx")

if __name__ == "__main__":
    remove_and_modify_shapes()
```
{{< /tab >}}
{{< tab "spreadsheet.xlsx" >}}  
{{< tab-text >}}
`spreadsheet.xlsx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/shapes-in-spreadsheet-document/spreadsheet.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.xlsx" >}}  
```text
Binary file (XLSX, 9 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/shapes-in-spreadsheet-document/remove_and_modify_shapes/output.xlsx)
{{< /tab >}}
{{< /tabs >}}

You can replace a shape's text by assigning to `shape.text`, replace its image by assigning a `SpreadsheetWatermarkableImage` to `shape.image`, set a hyperlink via `shape.hyperlink`, and modify its position and size.
