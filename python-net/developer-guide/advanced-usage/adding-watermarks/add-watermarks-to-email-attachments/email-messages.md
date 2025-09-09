---
id: email-messages
url: watermark/python-net/email-messages
title: Email messages
weight: 2
description: "Modify message body/subject, embed/remove images, search text, and list recipients using Python via .NET."
keywords: how to add watermark in outlook email, add watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Modifying body and subject of email message

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.email as gwc_email

load_options = gw.EmailLoadOptions()
with gw.Watermarker("message.msg", load_options) as watermarker:
    content = watermarker.get_content(gwc_email.EmailContent)
    content.body = "Test plain text body"
    content.html_body = "<html><body>Test html body</body></html>"
    content.subject = "Test subject"
    watermarker.save("message.msg")
```

## Embedding image to email message body

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.email as gwc_email

load_options = gw.EmailLoadOptions()
with gw.Watermarker("message.msg", load_options) as watermarker:
    content = watermarker.get_content(gwc_email.EmailContent)
    with open("sample.jpg", "rb") as f:
        content.embedded_objects.add(f.read(), "sample.jpg")
    embedded_object = content.embedded_objects[content.embedded_objects.count - 1]
    content.html_body = f"<html><body>This is an embedded image: <img src=\"cid:{embedded_object.content_id}\"></body></html>"
    watermarker.save("message.msg")
```

## Removing all embedded images from email message body

```python
import re
import groupdocs.watermark as gw
import groupdocs.watermark.contents.email as gwc_email
from groupdocs.watermark.common import FileType

load_options = gw.EmailLoadOptions()
with gw.Watermarker("message.msg", load_options) as watermarker:
    content = watermarker.get_content(gwc_email.EmailContent)
    for i in range(content.embedded_objects.count - 1, -1, -1):
        if content.embedded_objects[i].get_document_info().file_type == FileType.JPEG:
            pattern = rf"<img[^>]*src=\"cid:{re.escape(content.embedded_objects[i].content_id)}\"[^>]*>"
            content.html_body = re.sub(pattern, "", content.html_body)
            content.embedded_objects.remove_at(i)
    watermarker.save("message.msg")
```

## Searching text in email message body or subject

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.email as gwc_email
import groupdocs.watermark.search.searchcriteria as gws_sc
import groupdocs.watermark.search.objects as gws_objs

load_options = gw.EmailLoadOptions()
with gw.Watermarker("message.msg", load_options) as watermarker:
    criteria = gws_sc.TextSearchCriteria("test", False)
    watermarker.searchable_objects.email_searchable_objects = (
        gws_objs.EmailSearchableObjects.SUBJECT
        | gws_objs.EmailSearchableObjects.HTML_BODY
        | gws_objs.EmailSearchableObjects.PLAIN_TEXT_BODY
    )
    watermarks = watermarker.search(criteria)
    watermarks.clear()
    watermarker.save("message.msg")
```

## Listing all message recipients

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.email as gwc_email

load_options = gw.EmailLoadOptions()
with gw.Watermarker("message.msg", load_options) as watermarker:
    content = watermarker.get_content(gwc_email.EmailContent)
    for address in content.to:
        print(address.address)
    for address in content.cc:
        print(address.address)
    for address in content.bcc:
        print(address.address)
```


