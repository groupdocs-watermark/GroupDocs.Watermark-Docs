---
id: get-supported-file-formats
url: watermark/python-net/get-supported-file-formats
title: Get supported file formats
linkTitle: Get supported file formats
weight: 9
description: "List all file formats supported by GroupDocs.Watermark for Python via .NET."
keywords: GroupDocs.Watermark, supported file formats, file types, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Quickly retrieve the complete list of file formats supported by GroupDocs.Watermark. This lets your application check compatibility dynamically before processing a document — for example, to validate user-uploaded files.

## List supported file formats

`FileType.get_supported_file_types()` returns every supported file type. Each item exposes its `extension` and a friendly description.

{{< tabs "code-example-get-supported-file-formats">}}
{{< tab "list_supported_formats.py" >}}  
```python
from groupdocs.watermark.common import FileType

def list_supported_formats():
    # Enumerate every file type the library can open
    supported_file_types = FileType.get_supported_file_types()
    for file_type in sorted(supported_file_types, key=lambda x: x.extension):
        print(file_type)

if __name__ == "__main__":
    list_supported_formats()
```
{{< /tab >}}
{{< tab "list-supported-formats.txt" >}}  
```text
Bmp (.bmp) - Image
Doc (.doc) - WordProcessing
Docm (.docm) - WordProcessing
Docx (.docx) - WordProcessing
Dot (.dot) - WordProcessing
Dotm (.dotm) - WordProcessing
Dotx (.dotx) - WordProcessing
Eml (.eml) - Email
Emlx (.emlx) - Email
Gif (.gif) - Image
[TRUNCATED]
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/get-supported-file-formats/list_supported_formats/list-supported-formats.txt)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="info" >}}
**Use case:** Build flexible applications that validate user-uploaded files and tell the user whether watermarking is supported.
{{< /alert >}}
