---
id: attachments-in-pdf-document
url: watermark/python-net/attachments-in-pdf-document
title: Attachments in PDF document
linkTitle: Attachments in PDF document
weight: 1
description: "Extract, add, and remove PDF attachments, and watermark them, using GroupDocs.Watermark for Python via .NET."
keywords: pdf attachments, extract attachments, add attachment, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

A PDF can carry embedded file attachments. `Watermarker.get_content()` returns a `PdfContent` whose `attachments` collection lets you add, extract, and remove them — and you can even open an attachment in its own `Watermarker` to watermark it.

## Add an attachment

The example embeds a Word document into the PDF as an attachment.

{{< tabs "code-example-add-pdf-attachment">}}
{{< tab "add_attachment.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.pdf import PdfLoadOptions

def add_attachment():
    with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
        content = watermarker.get_content()
        with open("./sample.docx", "rb") as f:
            data = f.read()
        content.attachments.add(data, "sample.docx", "Attached Word document")
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    add_attachment()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` and `sample.docx` are the sample files used in this example. Download [document.pdf](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/attachments-in-pdf-document/document.pdf) and [sample.docx](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/attachments-in-pdf-document/sample.docx).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 512 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/attachments-in-pdf-document/add_attachment/output.pdf)
{{< /tab >}}
{{< /tabs >}}

## Extract attachments

Iterate the `attachments` collection to read each attachment's metadata and content.

```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.pdf import PdfLoadOptions

with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
    content = watermarker.get_content()
    print("Attachments:", len(content.attachments))
    for attachment in content.attachments:
        info = attachment.get_document_info()
        print(f"- name={attachment.name!r} type={info.file_type} size={len(attachment.content)} bytes")
        # Save the attachment's bytes to disk
        with open(f"./{attachment.name}", "wb") as f:
            f.write(attachment.content)
```

For the example PDF produced above, this prints:

```text
Attachments: 1
- name='sample.docx' type=Docx (.docx) - WordProcessing size=14752 bytes
```

Use `content.attachments.remove_at(index)` or `content.attachments.remove(attachment)` to delete an attachment, and open an attachment in its own `Watermarker` (from its `content` bytes) to add a watermark to the attached document itself.
