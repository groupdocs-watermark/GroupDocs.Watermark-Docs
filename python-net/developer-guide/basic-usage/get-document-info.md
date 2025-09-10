---
id: get-document-info
url: watermark/python-net/get-document-info
title: Get document info
weight: 8
description: "Retrieve file type, page count, size, and encryption using Python via .NET."
keywords: GroupDocs.Watermark, watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark can obtain document information:

- FileType
- PageCount
- Size
- IsEncrypted

## Get document information from a file from local disk

GroupDocs.Watermark lets you extract key details about a document before working with it. You can check its format, size, number of pages, and encryption status either from a file on disk or directly from a stream.

```python
import groupdocs.watermark as gw

with gw.Watermarker("source.docx") as watermarker:
    info = watermarker.get_document_info()
    print("File type:", info.file_type)
    print("Number of pages:", info.page_count)
    print("Document size:", info.size)
```

## Get document information from a stream

```python
import io
import groupdocs.watermark as gw

with open("source.docx", "rb") as f:
    stream = io.BytesIO(f.read())

with gw.Watermarker(stream) as watermarker:
    info = watermarker.get_document_info()
    print("File type:", info.file_type)
    print("Number of pages:", info.page_count)
    print("Document size:", info.size)
```

🔹 Use case: Validate documents before processing (e.g., reject encrypted files, check page limits, or confirm file type).
