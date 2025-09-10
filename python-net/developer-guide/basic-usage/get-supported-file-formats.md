---
id: get-supported-file-formats
url: watermark/python-net/get-supported-file-formats
title: Get supported file formats
weight: 9
description: "List all supported file formats using Python via .NET."
keywords: GroupDocs.Watermark,watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Get the list of all supported file formats.

Quickly retrieve the complete list of file formats supported by GroupDocs.Watermark. This allows Python developers to dynamically check compatibility before processing documents.

```python
from groupdocs.watermark.common import FileType

supported = FileType.get_supported_file_types()
for ft in supported:
    print(ft)
```

🔹 Use case: Build flexible applications that can automatically validate user-uploaded files and inform them if watermarking is supported.

