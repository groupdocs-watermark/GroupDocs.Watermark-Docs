---
id: update
url: watermark/python-net/basic-usage/update
title: Update watermarks
linkTitle: Update watermarks
weight: 5
description: "Search for existing text or image watermarks and update them using GroupDocs.Watermark for Python via .NET."
keywords: update text watermark, update image watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

You can search a document for existing watermarks and modify them in place — for example, replace the text of a text watermark or swap the image of an image watermark.

## Update text watermarks

Search for a watermark by its text content, then assign a new value to each match. The example below opens a document that already contains a "CONFIDENTIAL" watermark and replaces it with "APPROVED".

{{< tabs "code-example-update">}}
{{< tab "update_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

def update_watermark():
    with Watermarker("./watermarked-document.pdf") as watermarker:
        # Find the watermarks whose text matches the criteria
        possible = watermarker.search(TextSearchCriteria("CONFIDENTIAL"))
        print("Found", len(possible), "possible watermark(s).")
        for watermark in possible:
            try:
                watermark.text = "APPROVED"
            except Exception:
                # Some found entities do not support text editing — skip them
                pass
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    update_watermark()
```
{{< /tab >}}
{{< tab "watermarked-document.pdf" >}}  
{{< tab-text >}}
`watermarked-document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/basic-usage/update/watermarked-document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 479 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/update/update_watermark/output.pdf)
{{< /tab >}}
{{< /tabs >}}

## Update image watermarks

Image watermarks can be found with perceptual hashing (`ImageDctHashSearchCriteria`) and updated by assigning new bytes to `image_data`. The example below finds the logo watermark and replaces it with an "APPROVED" stamp:

{{< tabs "code-example-update-image">}}
{{< tab "update_image_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import ImageDctHashSearchCriteria

def update_image_watermark():
    with Watermarker("./watermarked-document.docx") as watermarker:
        criteria = ImageDctHashSearchCriteria("./logo.png")
        criteria.max_difference = 0.9
        possible = watermarker.search(criteria)
        with open("./stamp.png", "rb") as f:
            image_data = f.read()
        for watermark in possible:
            try:
                watermark.image_data = image_data
            except Exception:
                # Some found entities do not support image editing — skip them
                pass
        watermarker.save("./output.docx")

if __name__ == "__main__":
    update_image_watermark()
```
{{< /tab >}}
{{< tab "watermarked-document.docx" >}}  
{{< tab-text >}}
`watermarked-document.docx`, `logo.png`, and `stamp.png` are the sample files used in this example. Download [watermarked-document.docx](/watermark/python-net/_sample_files/developer-guide/basic-usage/update/watermarked-document.docx), [logo.png](/watermark/python-net/_sample_files/developer-guide/basic-usage/update/logo.png), and [stamp.png](/watermark/python-net/_sample_files/developer-guide/basic-usage/update/stamp.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 18 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/update/update_image_watermark/output.docx)
{{< /tab >}}
{{< /tabs >}}
