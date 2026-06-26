---
id: working-with-spreadsheet-document-attachments
url: watermark/python-net/working-with-spreadsheet-document-attachments
title: Working with spreadsheet document attachments
linkTitle: Working with attachments
weight: 2
description: "Extract, add, remove, and watermark the OLE attachments embedded in Excel worksheets using GroupDocs.Watermark for Python via .NET."
keywords: spreadsheet attachments, excel ole objects, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Excel worksheets can embed file attachments (OLE objects). They are available through `SpreadsheetContent.worksheets[i].attachments`. Each attachment exposes `alternative_text`, `is_link`, `source_full_name`, `content`, and `get_document_info()`, and the document it contains can be opened in its own `Watermarker`.

## Extract attachments

{{< tabs "code-example-extract-spreadsheet-attachments">}}
{{< tab "extract_attachments.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.spreadsheet import SpreadsheetLoadOptions

def extract_attachments():
    with Watermarker("./spreadsheet.xlsx", SpreadsheetLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for i, worksheet in enumerate(content.worksheets):
            for attachment in worksheet.attachments:
                info = attachment.get_document_info()
                print(f"Worksheet {i}: {attachment.alternative_text!r} type={info.file_type}")
                with open(f"./{attachment.alternative_text}", "wb") as f:
                    f.write(attachment.content)

if __name__ == "__main__":
    extract_attachments()
```
{{< /tab >}}
{{< tab "spreadsheet.xlsx" >}}  
{{< tab-text >}}
`spreadsheet.xlsx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-spreadsheet-document-attachments/spreadsheet.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< /tabs >}}

## Remove an attachment

The `attachments` collection supports `remove_at(index)` and `remove(attachment)`. Iterate in reverse when removing by index:

{{< tabs "code-example-remove-spreadsheet-attachment">}}
{{< tab "remove_attachment.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.spreadsheet import SpreadsheetLoadOptions

def remove_attachment():
    with Watermarker("./spreadsheet.xlsx", SpreadsheetLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for worksheet in content.worksheets:
            for i in range(len(worksheet.attachments) - 1, -1, -1):
                if worksheet.attachments[i].is_link:
                    worksheet.attachments.remove_at(i)
        watermarker.save("./output.xlsx")

if __name__ == "__main__":
    remove_attachment()
```
{{< /tab >}}
{{< tab "spreadsheet.xlsx" >}}  
{{< tab-text >}}
`spreadsheet.xlsx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-spreadsheet-document-attachments/spreadsheet.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.xlsx" >}}  
```text
Binary file (XLSX, 9 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-spreadsheet-document-attachments/remove_attachment/output.xlsx)
{{< /tab >}}
{{< /tabs >}}

## Watermark the attached documents

Open each attachment's bytes in its own `Watermarker`, add a watermark, and write the result back:

{{< tabs "code-example-watermark-spreadsheet-attachments">}}
{{< tab "watermark_attached_documents.py" >}}  
```python
import io
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.options.spreadsheet import SpreadsheetLoadOptions

def watermark_attached_documents():
    with Watermarker("./spreadsheet.xlsx", SpreadsheetLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for worksheet in content.worksheets:
            for attachment in worksheet.attachments:
                with Watermarker(io.BytesIO(attachment.content)) as inner:
                    wm = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
                    wm.foreground_color = Color.red
                    inner.add(wm)
                    buffer = io.BytesIO()
                    inner.save(buffer)
                # write the watermarked attachment bytes back as needed
        watermarker.save("./output.xlsx")

if __name__ == "__main__":
    watermark_attached_documents()
```
{{< /tab >}}
{{< tab "spreadsheet.xlsx" >}}  
{{< tab-text >}}
`spreadsheet.xlsx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-spreadsheet-document-attachments/spreadsheet.xlsx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.xlsx" >}}  
```text
Binary file (XLSX, 9 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-spreadsheet-document-attachments/watermark_attached_documents/output.xlsx)
{{< /tab >}}
{{< /tabs >}}
