---
id: get-document-info
url: watermark/python-net/get-document-info
title: Get document info
linkTitle: Get document info
weight: 8
description: "Retrieve file type, page count, and size of a document using GroupDocs.Watermark for Python via .NET."
keywords: GroupDocs.Watermark, document info, file type, page count, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark can obtain a document's basic information — file type, page count, and size — before you process it. The `get_document_info()` method works on a `Watermarker` opened from either a file path or a stream.

## Get document information from a file

{{< tabs "code-example-get-document-info">}}
{{< tab "get_document_info.py" >}}  
```python
from groupdocs.watermark import Watermarker

def get_document_info():
    with Watermarker("./sample.docx") as watermarker:
        info = watermarker.get_document_info()
        print("File type:", info.file_type)
        print("Pages:", info.page_count)
        print("Size, bytes:", info.size)

if __name__ == "__main__":
    get_document_info()
```
{{< /tab >}}
{{< tab "sample.docx" >}}  
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/basic-usage/get-document-info/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "get-document-info.txt" >}}  
```text
File type: Docx (.docx) - WordProcessing
Pages: 3
Size, bytes: 121298
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/get-document-info/get_document_info/get-document-info.txt)
{{< /tab >}}
{{< /tabs >}}

## Get document information from a stream

A document can also be opened from any readable stream:

{{< tabs "code-example-get-document-info-stream">}}
{{< tab "get_document_info_from_stream.py" >}}  
```python
import io
from groupdocs.watermark import Watermarker

def get_document_info_from_stream():
    with open("./sample.docx", "rb") as f:
        stream = io.BytesIO(f.read())

    with Watermarker(stream) as watermarker:
        info = watermarker.get_document_info()
        print("File type:", info.file_type)
        print("Pages:", info.page_count)
        print("Size, bytes:", info.size)

if __name__ == "__main__":
    get_document_info_from_stream()
```
{{< /tab >}}
{{< tab "sample.docx" >}}  
{{< tab-text >}}
`sample.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/basic-usage/get-document-info/sample.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "get-document-info-from-stream.txt" >}}  
```text
File type: Docx (.docx) - WordProcessing
Pages: 3
Size, bytes: 121298
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/get-document-info/get_document_info_from_stream/get-document-info-from-stream.txt)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="info" >}}
**Use case:** Validate documents before processing — for example, reject unsupported file types or confirm page limits.
{{< /alert >}}
