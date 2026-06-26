---
id: email-attachments
url: watermark/python-net/email-attachments
title: Email attachments
linkTitle: Email attachments
weight: 1
description: "Extract, add, and remove the attachments of an email message using GroupDocs.Watermark for Python via .NET."
keywords: email attachments, msg attachments, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

`EmailContent.attachments` is the collection of files attached to an email message. Each attachment exposes its `name`, `content` (bytes), and `get_document_info()`, and you can add and remove attachments.

## Extract all attachments

{{< tabs "code-example-extract-email-attachments">}}
{{< tab "extract_attachments.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.email import EmailLoadOptions

def extract_attachments():
    with Watermarker("./message.msg", EmailLoadOptions()) as watermarker:
        content = watermarker.get_content()
        print("Attachments:", len(content.attachments))
        for attachment in content.attachments:
            info = attachment.get_document_info()
            print(f"- {attachment.name!r} type={info.file_type}")
            with open(f"./{attachment.name}", "wb") as f:
                f.write(attachment.content)

if __name__ == "__main__":
    extract_attachments()
```
{{< /tab >}}
{{< tab "message.msg" >}}  
{{< tab-text >}}
`message.msg` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-attachments/message.msg) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "sample.docx" >}}  
```text
Binary file (DOCX, 118 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-attachments/extract_attachments/sample.docx)
{{< /tab >}}
{{< /tabs >}}

## Add an attachment

{{< tabs "code-example-add-email-attachment">}}
{{< tab "add_attachment.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.email import EmailLoadOptions

def add_attachment():
    with Watermarker("./message.msg", EmailLoadOptions()) as watermarker:
        content = watermarker.get_content()
        with open("./sample.docx", "rb") as f:
            data = f.read()
        content.attachments.add(data, "sample.docx")
        watermarker.save("./output.msg")

if __name__ == "__main__":
    add_attachment()
```
{{< /tab >}}
{{< tab "message.msg" >}}  
{{< tab-text >}}
`message.msg` and `sample.docx` are the sample files used in this example. Download [message.msg](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-attachments/message.msg) and [sample.docx](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-attachments/sample.docx).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.msg" >}}  
```text
Binary file (MSG, 254 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-attachments/add_attachment/output.msg)
{{< /tab >}}
{{< /tabs >}}

## Remove an attachment

The `attachments` collection supports `remove_at(index)` and `remove(attachment)`. Iterate in reverse when removing by index:

{{< tabs "code-example-remove-email-attachment">}}
{{< tab "remove_attachment.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.email import EmailLoadOptions

def remove_attachment():
    with Watermarker("./message.msg", EmailLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for i in range(len(content.attachments) - 1, -1, -1):
            if "sample" in content.attachments[i].name:
                content.attachments.remove_at(i)
        watermarker.save("./output.msg")

if __name__ == "__main__":
    remove_attachment()
```
{{< /tab >}}
{{< tab "message.msg" >}}  
{{< tab-text >}}
`message.msg` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-attachments/message.msg) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.msg" >}}  
```text
Binary file (MSG, 12 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-attachments/remove_attachment/output.msg)
{{< /tab >}}
{{< /tabs >}}

To watermark an attached document, open `attachment.content` in its own `Watermarker` (via `io.BytesIO`), add the watermark, and write the bytes back — the same pattern shown for [spreadsheet attachments]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/working-with-spreadsheet-document-attachments.md" >}}).
