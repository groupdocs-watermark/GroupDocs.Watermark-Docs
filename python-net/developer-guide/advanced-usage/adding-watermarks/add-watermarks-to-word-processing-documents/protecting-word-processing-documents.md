---
id: protecting-word-processing-documents
url: watermark/python-net/protecting-word-processing-documents
title: Protecting word processing documents
linkTitle: Protecting documents
weight: 3
description: "Protect and unprotect Word documents with a protection type and password using GroupDocs.Watermark for Python via .NET."
keywords: protect word document, unprotect word document, read only, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Beyond locking an individual watermark, you can protect the whole document. `Watermarker.get_content()` returns a `WordProcessingContent` with `protect()` and `unprotect()` methods.

## Protect a document

The example sets read-only protection with a password.

{{< tabs "code-example-protect-word-document">}}
{{< tab "protect_document.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.word_processing import WordProcessingLoadOptions
from groupdocs.watermark.contents.word_processing import WordProcessingProtectionType

def protect_document():
    with Watermarker("./document.docx", WordProcessingLoadOptions()) as watermarker:
        content = watermarker.get_content()
        content.protect(WordProcessingProtectionType.READ_ONLY, "p@ssw0rd")
        watermarker.save("./output.docx")

if __name__ == "__main__":
    protect_document()
```
{{< /tab >}}
{{< tab "document.docx" >}}  
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 119 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/protecting-word-processing-documents/protect_document/output.docx)
{{< /tab >}}
{{< /tabs >}}

Available `WordProcessingProtectionType` values: `READ_ONLY`, `ALLOW_ONLY_FORM_FIELDS`, `ALLOW_ONLY_COMMENTS`, and `ALLOW_ONLY_REVISIONS`.

## Unprotect a document

{{< tabs "code-example-unprotect-word-document">}}
{{< tab "unprotect_document.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.word_processing import WordProcessingLoadOptions

def unprotect_document():
    with Watermarker("./document.docx", WordProcessingLoadOptions()) as watermarker:
        content = watermarker.get_content()
        content.unprotect()
        watermarker.save("./output.docx")

if __name__ == "__main__":
    unprotect_document()
```
{{< /tab >}}
{{< tab "document.docx" >}}  
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 118 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/protecting-word-processing-documents/unprotect_document/output.docx)
{{< /tab >}}
{{< /tabs >}}
