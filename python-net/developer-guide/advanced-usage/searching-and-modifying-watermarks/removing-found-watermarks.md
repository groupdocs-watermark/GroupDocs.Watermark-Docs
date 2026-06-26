---
id: removing-found-watermarks
url: watermark/python-net/removing-found-watermarks
title: Removing found watermarks
linkTitle: Removing found watermarks
weight: 3
description: "Find and remove text, image, and hyperlink watermarks using GroupDocs.Watermark for Python via .NET."
keywords: remove watermark, clear watermarks, remove hyperlink watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Search for the watermarks already present in a document — including those added by third-party tools — and remove them. Iterate the results in reverse so that removing an item does not shift the indexes still to visit.

## Remove watermarks

The example below finds every possible watermark in a document and removes them all.

{{< tabs "code-example-remove-watermark">}}
{{< tab "remove_watermark.py" >}}  
```python
from groupdocs.watermark import Watermarker

def remove_watermark():
    with Watermarker("./document.pdf") as watermarker:
        possible = watermarker.search()
        for i in range(len(possible) - 1, -1, -1):
            watermarker.remove(possible[i])
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    remove_watermark()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 394 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks/remove_watermark/output.pdf)
{{< /tab >}}
{{< /tabs >}}

## Remove watermarks with particular text formatting

Search by color and size, then remove every match.

{{< tabs "code-example-remove-watermark-formatting">}}
{{< tab "remove_watermark_with_formatting.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextFormattingSearchCriteria, ColorRange

def remove_watermark_with_formatting():
    with Watermarker("./document.pdf") as watermarker:
        criteria = TextFormattingSearchCriteria()
        criteria.foreground_color_range = ColorRange()
        criteria.foreground_color_range.min_hue = -15
        criteria.foreground_color_range.max_hue = 15
        criteria.foreground_color_range.min_brightness = 0.01
        criteria.foreground_color_range.max_brightness = 0.99
        criteria.min_font_size = 19
        criteria.max_font_size = 42

        possible = watermarker.search(criteria)
        for i in range(len(possible) - 1, -1, -1):
            watermarker.remove(possible[i])
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    remove_watermark_with_formatting()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 394 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks/remove_watermark_with_formatting/output.pdf)
{{< /tab >}}
{{< /tabs >}}

## Remove hyperlink watermarks

Find hyperlinks with a particular URL using a regular expression, and remove only the entities that are hyperlinks.

{{< tabs "code-example-remove-hyperlink-watermarks">}}
{{< tab "remove_hyperlink_watermarks.py" >}}  
```python
import re
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search import HyperlinkPossibleWatermark
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

def remove_hyperlink_watermarks():
    with Watermarker("./document.pdf") as watermarker:
        possible = watermarker.search(TextSearchCriteria(re.compile(r"someurl\.com")))
        for i in range(len(possible) - 1, -1, -1):
            if isinstance(possible[i], HyperlinkPossibleWatermark):
                print(possible[i].text)
                watermarker.remove(possible[i])
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    remove_hyperlink_watermarks()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 395 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks/remove_hyperlink_watermarks/output.pdf)
{{< /tab >}}
{{< /tabs >}}
