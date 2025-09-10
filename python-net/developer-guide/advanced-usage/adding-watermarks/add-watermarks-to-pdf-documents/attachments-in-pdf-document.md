---
id: attachments-in-pdf-document
url: watermark/python-net/attachments-in-pdf-document
title: Attachments in PDF document
weight: 1
description: "Work with PDF attachments: extract, add, remove, and search images using Python via .NET."
keywords: watermarking API, PDF attachments, Extract all attachments
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Extract all attachments from PDF document
This sample extracts every embedded file from a PDF, prints basic metadata (name, description, file type), and writes the attachment bytes to an output folder.

```python
import os
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

output_dir = os.path.join("SampleFiles", "Output")
os.makedirs(output_dir, exist_ok=True)

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for attachment in pdf_content.attachments:
        print("Name:", attachment.name)
        print("Description:", attachment.description)
        print("File type:", attachment.get_document_info().file_type)

        with open(os.path.join(output_dir, attachment.name), "wb") as f:
            f.write(attachment.content)
```

## Add an attachment to PDF document
This sample embeds an external file into the PDF as an attachment, assigning a display name and description, and then saves the updated document.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    with open("sample.docx", "rb") as f:
        pdf_content.attachments.add(f.read(), "sample doc", "sample doc as attachment")

    watermarker.save("document.pdf")
```

## Remove attachment from PDF document
This sample finds and removes attachments that match custom criteria (for example, a name containing "sample" and the DOCX file type), and then saves the PDF.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.pdf as gwc_pdf
from groupdocs.watermark.common import FileType

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    pdf_content = watermarker.get_content(gwc_pdf.PdfContent)
    for i in range(pdf_content.attachments.count - 1, -1, -1):
        attachment = pdf_content.attachments[i]
        if ("sample" in attachment.name) and (attachment.get_document_info().file_type == FileType.DOCX):
            pdf_content.attachments.remove_at(i)

    watermarker.save("document.pdf")
```

## Search for images attachments
This sample limits the search scope to images inside attachments and returns the found image collection for further processing or inspection.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.common as gwc

load_options = gw.PdfLoadOptions()
with gw.Watermarker("document.pdf", load_options) as watermarker:
    watermarker.searchable_objects.pdf_searchable_objects = gwc.PdfSearchableObjects.ATTACHED_IMAGES
    images = watermarker.get_images()
    print("Found", images.count, "image(s).")
```


