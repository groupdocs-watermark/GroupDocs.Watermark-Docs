---
id: locking-watermark-in-word-processing-document
url: watermark/python-net/locking-watermark-in-word-processing-document
title: Locking watermark in word processing document
linkTitle: Locking watermark
weight: 2
description: "Lock a watermark in a Word document to restrict editing, optionally with a password, using GroupDocs.Watermark for Python via .NET."
keywords: lock watermark, protect watermark, word, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

To make a watermark harder to remove, you can lock it by setting `is_locked` and a `lock_type` on the watermark option (`WordProcessingWatermarkSectionOptions` or `WordProcessingWatermarkPagesOptions`). An optional `password` is also supported.

## Add a locked watermark

{{< tabs "code-example-add-locked-word-watermark">}}
{{< tab "add_locked_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.options.word_processing import (
    WordProcessingLoadOptions, WordProcessingWatermarkSectionOptions, WordProcessingLockType,
)

def add_locked_watermark():
    with Watermarker("./document.docx", WordProcessingLoadOptions()) as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        watermark.foreground_color = Color.red

        options = WordProcessingWatermarkSectionOptions()
        options.is_locked = True
        options.lock_type = WordProcessingLockType.ALLOW_ONLY_FORM_FIELDS
        # options.password = "p@ssw0rd"   # optional
        watermarker.add(watermark, options)

        watermarker.save("./output.docx")

if __name__ == "__main__":
    add_locked_watermark()
```
{{< /tab >}}
{{< tab "document.docx" >}}  
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 125 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/locking-watermark-in-word-processing-document/add_locked_watermark/output.docx)
{{< /tab >}}
{{< /tabs >}}

Available `WordProcessingLockType` values: `ALLOW_ONLY_FORM_FIELDS`, `ALLOW_ONLY_COMMENTS`, `ALLOW_ONLY_REVISIONS`, `READ_ONLY`, `READ_ONLY_WITH_EDITABLE_CONTENT`, and `NO_LOCK`.
