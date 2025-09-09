---
id: email-attachments
url: watermark/python-net/email-attachments
title: Email attachments
weight: 1
description: "Extract, add, and remove attachments in email messages using Python via .NET."
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Extracting all attachments from email message

```python
import os
import groupdocs.watermark as gw
import groupdocs.watermark.contents.email as gwc_email

output_dir = os.path.join("SampleFiles", "Output")
os.makedirs(output_dir, exist_ok=True)

load_options = gw.EmailLoadOptions()
with gw.Watermarker("message.msg", load_options) as watermarker:
    content = watermarker.get_content(gwc_email.EmailContent)
    for attachment in content.attachments:
        print("Name:", attachment.name)
        print("File format:", attachment.get_document_info().file_type)
        with open(os.path.join(output_dir, attachment.name), "wb") as f:
            f.write(attachment.content)
```

## Removing particular attachment from email message

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.email as gwc_email
from groupdocs.watermark.common import FileType

load_options = gw.EmailLoadOptions()
with gw.Watermarker("message.msg", load_options) as watermarker:
    content = watermarker.get_content(gwc_email.EmailContent)
    for i in range(content.attachments.count - 1, -1, -1):
        attachment = content.attachments[i]
        if ("sample" in attachment.name) and (attachment.get_document_info().file_type == FileType.DOCX):
            content.attachments.remove_at(i)
    watermarker.save("message.msg")
```

## Adding attachment to email message

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.email as gwc_email

load_options = gw.EmailLoadOptions()
with gw.Watermarker("message.msg", load_options) as watermarker:
    content = watermarker.get_content(gwc_email.EmailContent)
    with open("sample.msg", "rb") as f:
        content.attachments.add(f.read(), "sample.msg")
    watermarker.save("message.msg")
```


