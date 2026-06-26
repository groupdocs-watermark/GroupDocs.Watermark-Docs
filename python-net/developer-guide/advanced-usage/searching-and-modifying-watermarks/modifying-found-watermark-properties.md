---
id: modifying-found-watermark-properties
url: watermark/python-net/modifying-found-watermark-properties
title: Modifying found watermark properties
linkTitle: Modifying found watermark properties
weight: 2
description: "Search for existing watermarks and update their text, formatted text, or image using GroupDocs.Watermark for Python via .NET."
keywords: modify watermark text, replace watermark image, formatted text fragments, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark lets you replace the text or image of watermarks that already exist in a document. Search for the watermarks first, then assign a new value to each match.

## Replace text

The example below opens a document that contains a "CONFIDENTIAL" watermark, finds it, and replaces the text with "APPROVED".

{{< tabs "code-example-modify-watermark">}}
{{< tab "modify_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

def modify_watermark():
    with Watermarker("./watermarked-document.pdf") as watermarker:
        possible = watermarker.search(TextSearchCriteria("CONFIDENTIAL"))
        for wm in possible:
            try:
                wm.text = "APPROVED"
            except Exception:
                # The entity may not support text editing, or the value is invalid
                pass
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    modify_watermark()
```
{{< /tab >}}
{{< tab "watermarked-document.pdf" >}}  
{{< tab-text >}}
`watermarked-document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties/watermarked-document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 479 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties/modify_watermark/output.pdf)
{{< /tab >}}
{{< /tabs >}}

## Replace text with formatting

Use `formatted_text_fragments` to replace the text with styled fragments — choose the font, foreground color, and background color.

{{< tabs "code-example-modify-watermark-formatting">}}
{{< tab "modify_watermark_with_formatting.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import Font, FontStyle, Color
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

def modify_watermark_with_formatting():
    with Watermarker("./watermarked-document.pdf") as watermarker:
        possible = watermarker.search(TextSearchCriteria("CONFIDENTIAL"))
        for wm in possible:
            try:
                wm.formatted_text_fragments.clear()
                wm.formatted_text_fragments.add(
                    "APPROVED",
                    Font("Calibri", 19.0, FontStyle.BOLD),
                    Color.red,
                    Color.aqua,
                )
            except Exception:
                # The entity may not support formatted text, or values may be invalid
                pass
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    modify_watermark_with_formatting()
```
{{< /tab >}}
{{< tab "watermarked-document.pdf" >}}  
{{< tab-text >}}
`watermarked-document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties/watermarked-document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 662 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties/modify_watermark_with_formatting/output.pdf)
{{< /tab >}}
{{< /tabs >}}

## Replace image

Swap the image data of matched watermarks by assigning new bytes to `image_data`.

{{< tabs "code-example-replace-watermark-image">}}
{{< tab "replace_watermark_image.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import ImageDctHashSearchCriteria

def replace_watermark_image():
    with open("./stamp.png", "rb") as f:
        image_data = f.read()

    with Watermarker("./watermarked-document.docx") as watermarker:
        criteria = ImageDctHashSearchCriteria("./logo.png")
        criteria.max_difference = 0.9
        possible = watermarker.search(criteria)
        for wm in possible:
            try:
                wm.image_data = image_data
            except Exception:
                # The entity may not support image replacement, or the image format is invalid
                pass
        watermarker.save("./output.docx")

if __name__ == "__main__":
    replace_watermark_image()
```
{{< /tab >}}
{{< tab "watermarked-document.docx" >}}  
{{< tab-text >}}
`watermarked-document.docx`, `logo.png`, and `stamp.png` are the sample files used in this example. Download [watermarked-document.docx](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties/watermarked-document.docx), [logo.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties/logo.png), and [stamp.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties/stamp.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 18 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties/replace_watermark_image/output.docx)
{{< /tab >}}
{{< /tabs >}}
