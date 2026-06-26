---
id: clear
url: watermark/python-net/basic-usage/clear
title: Clear watermarks
linkTitle: Clear watermarks
weight: 6
description: "Search for and remove existing text or image watermarks using GroupDocs.Watermark for Python via .NET."
keywords: clear text watermark, clear image watermark, remove watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

You can search a document for existing watermarks and remove them. The example below finds a "CONFIDENTIAL" text watermark and removes it, producing a clean document.

## Remove text watermarks

Iterate the search results in reverse so removing an item does not shift the indexes still to visit, and call `remove()` for each match.

{{< tabs "code-example-clear">}}
{{< tab "clear_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

def clear_watermark():
    with Watermarker("./watermarked-document.pdf") as watermarker:
        possible = watermarker.search(TextSearchCriteria("CONFIDENTIAL"))
        # Remove in reverse so indexes stay valid as items are deleted
        for i in range(len(possible) - 1, -1, -1):
            watermarker.remove(possible[i])
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    clear_watermark()
```
{{< /tab >}}
{{< tab "watermarked-document.pdf" >}}  
{{< tab-text >}}
`watermarked-document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/basic-usage/clear/watermarked-document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 394 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/clear/clear_watermark/output.pdf)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="info" >}}
**Use case:** Remove outdated labels such as "Draft" or "Internal Use Only" before sharing a document externally.
{{< /alert >}}

## Remove image watermarks

Image watermarks can be found with perceptual hashing and removed the same way:

{{< tabs "code-example-clear-image">}}
{{< tab "clear_image_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import ImageDctHashSearchCriteria

def clear_image_watermark():
    with Watermarker("./watermarked-document.docx") as watermarker:
        criteria = ImageDctHashSearchCriteria("./logo.png")
        criteria.max_difference = 0.9
        possible = watermarker.search(criteria)
        # Remove in reverse so indexes stay valid as items are deleted
        for i in range(len(possible) - 1, -1, -1):
            watermarker.remove(possible[i])
        watermarker.save("./output.docx")

if __name__ == "__main__":
    clear_image_watermark()
```
{{< /tab >}}
{{< tab "watermarked-document.docx" >}}  
{{< tab-text >}}
`watermarked-document.docx` and `logo.png` are the sample files used in this example. Download [watermarked-document.docx](/watermark/python-net/_sample_files/developer-guide/basic-usage/clear/watermarked-document.docx) and [logo.png](/watermark/python-net/_sample_files/developer-guide/basic-usage/clear/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 12 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/clear/clear_image_watermark/output.docx)
{{< /tab >}}
{{< /tabs >}}
