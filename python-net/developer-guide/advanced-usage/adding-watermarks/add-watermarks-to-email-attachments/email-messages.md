---
id: email-messages
url: watermark/python-net/email-messages
title: Email messages
linkTitle: Email messages
weight: 2
description: "Modify an email message body and subject, embed and remove images, search text, and list recipients using GroupDocs.Watermark for Python via .NET."
keywords: email watermark, msg, eml, embed image, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

`Watermarker.get_content()` returns an `EmailContent` for an email message (MSG, EML, EMLX). It exposes the message `body`, `html_body`, and `subject`, the `embedded_objects` (inline images), the recipient lists (`to`, `cc`, `bcc`), and the `attachments`.

## Modify the body and subject

{{< tabs "code-example-modify-email-message">}}
{{< tab "modify_message.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.email import EmailLoadOptions

def modify_message():
    with Watermarker("./message.msg", EmailLoadOptions()) as watermarker:
        content = watermarker.get_content()
        content.subject = content.subject + " [CONFIDENTIAL]"
        content.body = content.body + "\n\nThis message is confidential."
        watermarker.save("./output.msg")

if __name__ == "__main__":
    modify_message()
```
{{< /tab >}}
{{< tab "message.msg" >}}  
{{< tab-text >}}
`message.msg` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/message.msg) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.msg" >}}  
```text
Binary file (MSG, 134 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/modify_message/output.msg)
{{< /tab >}}
{{< /tabs >}}

## Embed an image into the body

Add the image to `embedded_objects`, then reference it from the HTML body by its content id:

{{< tabs "code-example-embed-email-image">}}
{{< tab "embed_image.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.email import EmailLoadOptions

def embed_image():
    with Watermarker("./message.msg", EmailLoadOptions()) as watermarker:
        content = watermarker.get_content()
        with open("./logo.png", "rb") as f:
            data = f.read()
        content.embedded_objects.add(data, "logo.png")
        embedded = content.embedded_objects[len(content.embedded_objects) - 1]
        content.html_body = content.html_body.replace(
            "</body>", f'<img src="cid:{embedded.content_id}"/></body>')
        watermarker.save("./output.msg")

if __name__ == "__main__":
    embed_image()
```
{{< /tab >}}
{{< tab "message.msg" >}}  
{{< tab-text >}}
`message.msg` and `logo.png` are the sample files used in this example. Download [message.msg](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/message.msg) and [logo.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.msg" >}}  
```text
Binary file (MSG, 142 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/embed_image/output.msg)
{{< /tab >}}
{{< /tabs >}}

## Search the message text

Limit the search to the subject and body, then search with a `TextSearchCriteria`:

{{< tabs "code-example-search-email-text">}}
{{< tab "search_message_text.py" >}}  
```python
from groupdocs.watermark import Watermarker, WatermarkerSettings
from groupdocs.watermark.search.search_criteria import TextSearchCriteria
from groupdocs.watermark.search.objects import SearchableObjects, EmailSearchableObjects

def search_message_text():
    settings = WatermarkerSettings()
    settings.searchable_objects = SearchableObjects(
        email_searchable_objects=EmailSearchableObjects.SUBJECT | EmailSearchableObjects.PLAIN_TEXT_BODY)

    with Watermarker("./message.msg", settings) as watermarker:
        possible = watermarker.search(TextSearchCriteria("confidential"))
        print("Found", len(possible), "match(es)")

if __name__ == "__main__":
    search_message_text()
```
{{< /tab >}}
{{< tab "message.msg" >}}  
{{< tab-text >}}
`message.msg` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/message.msg) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-message-text.txt" >}}  
```text
Found 0 match(es)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/search_message_text/search-message-text.txt)
{{< /tab >}}
{{< /tabs >}}

## List recipients

{{< tabs "code-example-list-recipients">}}
{{< tab "list_recipients.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.email import EmailLoadOptions

def list_recipients():
    with Watermarker("./message.msg", EmailLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for recipient in list(content.to) + list(content.cc) + list(content.bcc):
            print(recipient.address)

if __name__ == "__main__":
    list_recipients()
```
{{< /tab >}}
{{< tab "message.msg" >}}  
{{< tab-text >}}
`message.msg` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/message.msg) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "list-recipients.txt" >}}  
```text
alex.chen@northwind.example
tomas.reyes@auroravisuals.example
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages/list_recipients/list-recipients.txt)
{{< /tab >}}
{{< /tabs >}}
