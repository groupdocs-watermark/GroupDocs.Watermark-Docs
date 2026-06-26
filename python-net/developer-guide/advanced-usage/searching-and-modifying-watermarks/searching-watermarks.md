---
id: searching-watermarks
url: watermark/python-net/searching-watermarks
title: Searching watermarks
linkTitle: Searching watermarks
weight: 1
description: "Find possible text and image watermarks with powerful criteria — text, regex, image similarity, formatting, and combined criteria — using GroupDocs.Watermark for Python via .NET."
keywords: search watermarks, text search, regex search, image search, combined search, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Use `Watermarker.search()` to scan a document for objects that can be treated as watermarks — including watermarks added by third-party tools. Without criteria, `search()` returns a subset such as backgrounds and floating objects; pass a criteria object to narrow the results.

## Search for possible watermarks

The example below searches a watermarked PDF and prints the text, page, and size of each possible watermark.

{{< tabs "code-example-searching-watermarks">}}
{{< tab "search_watermarks.py" >}}  
```python
from groupdocs.watermark import Watermarker

def search_watermarks():
    with Watermarker("./document.pdf") as watermarker:
        possible = watermarker.search()
        print(f"Found {len(possible)} possible watermark(s).")
        for wm in possible:
            text = (wm.text or "").strip()
            print(f"- page={wm.page_number} text={text!r} size={round(wm.width)}x{round(wm.height)}")

if __name__ == "__main__":
    search_watermarks()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-watermarks.txt" >}}  
```text
Found 8 possible watermark(s).
- page=1 text='CONFIDENTIAL' size=268x36
- page=1 text='' size=230x69
- page=1 text='' size=460x287
- page=2 text='CONFIDENTIAL' size=268x36
- page=3 text='CONFIDENTIAL' size=268x36
- page=None text='https://auroravisuals.example/legal/msa' size=128x14
- page=None text='https://auroravisuals.example/legal/licensing' size=173x14
- page=None text='https://auroravisuals.example/portfolio' size=76x14
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_watermarks/search-watermarks.txt)
{{< /tab >}}
{{< /tabs >}}

Each possible watermark exposes `text`, `image_data`, `x`, `y`, `width`, `height`, `rotate_angle`, and `page_number`.

## Search criteria

Large documents may contain many candidates. Use dedicated criteria to find exactly what you need.

### Text search criteria

Find watermarks by exact text.

{{< tabs "code-example-search-by-text">}}
{{< tab "search_by_text.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

def search_by_text():
    with Watermarker("./document.pdf") as watermarker:
        possible = watermarker.search(TextSearchCriteria("CONFIDENTIAL"))
        print("Found", len(possible), "possible watermark(s)")

if __name__ == "__main__":
    search_by_text()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-by-text.txt" >}}  
```text
Found 6 possible watermark(s)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_by_text/search-by-text.txt)
{{< /tab >}}
{{< /tabs >}}

### Regular expression search criteria

Pass a compiled regular expression to `TextSearchCriteria`.

{{< tabs "code-example-search-by-regex">}}
{{< tab "search_by_regex.py" >}}  
```python
import re
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

def search_by_regex():
    with Watermarker("./document.pdf") as watermarker:
        possible = watermarker.search(TextSearchCriteria(re.compile(r"^CONFIDENTIAL$")))
        print("Found", len(possible), "possible watermark(s)")

if __name__ == "__main__":
    search_by_regex()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-by-regex.txt" >}}  
```text
Found 6 possible watermark(s)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_by_regex/search-by-regex.txt)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="info" >}}
When a `TextSearchCriteria` is provided, the API also scans the main document text along with shapes, XObjects, annotations, and other objects.
{{< /alert >}}

### Image search criteria

Find image watermarks that are visually similar to a sample image using perceptual hashing (DCT hash). Control sensitivity with `max_difference` (0–1).

{{< tabs "code-example-search-by-image">}}
{{< tab "search_by_image.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import ImageDctHashSearchCriteria

def search_by_image():
    with Watermarker("./document.pdf") as watermarker:
        criteria = ImageDctHashSearchCriteria("./logo.png")
        criteria.max_difference = 0.9
        possible = watermarker.search(criteria)
        print("Found", len(possible), "possible watermark(s)")

if __name__ == "__main__":
    search_by_image()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` and `logo.png` are the sample files used in this example. Download [document.pdf](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) and [logo.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-by-image.txt" >}}  
```text
Found 2 possible watermark(s)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_by_image/search-by-image.txt)
{{< /tab >}}
{{< /tabs >}}

Other image criteria:

- `ImageColorHistogramSearchCriteria` — robust to rotation, scaling, and translation.
- `ImageThumbnailSearchCriteria` — robust to rotation, scaling, and minor color changes.

### Combined search criteria

Combine criteria with `and_()`, `or_()`, and `not_()`.

{{< tabs "code-example-search-combined">}}
{{< tab "search_combined.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import (
    ImageDctHashSearchCriteria, TextSearchCriteria, RotateAngleSearchCriteria,
)

def search_combined():
    with Watermarker("./document.pdf") as watermarker:
        image_criteria = ImageDctHashSearchCriteria("./logo.png")
        image_criteria.max_difference = 0.9
        text_criteria = TextSearchCriteria("CONFIDENTIAL")
        angle_criteria = RotateAngleSearchCriteria(30, 60)

        combined = image_criteria.or_(text_criteria).and_(angle_criteria)
        possible = watermarker.search(combined)
        print("Found", len(possible), "possible watermark(s)")

if __name__ == "__main__":
    search_combined()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` and `logo.png` are the sample files used in this example. Download [document.pdf](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) and [logo.png](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-combined.txt" >}}  
```text
Found 3 possible watermark(s)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_combined/search-combined.txt)
{{< /tab >}}
{{< /tabs >}}

### Text formatting search criteria

Find watermarks by text formatting such as font, size, and color ranges.

{{< tabs "code-example-search-by-formatting">}}
{{< tab "search_by_formatting.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextFormattingSearchCriteria, ColorRange

def search_by_formatting():
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
        print("Found", len(possible), "possible watermark(s)")

if __name__ == "__main__":
    search_by_formatting()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-by-formatting.txt" >}}  
```text
Found 3 possible watermark(s)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_by_formatting/search-by-formatting.txt)
{{< /tab >}}
{{< /tabs >}}

{{< alert style="info" >}}
Searching by **color and size** is the most robust way to match a text watermark. You can
also constrain `font_name` and `font_bold`, but bold fonts are often embedded under a fused
subset name (for example `ArialBold`) rather than `Arial` with a separate bold flag, so a
`font_name = "Arial"` filter may miss them.
{{< /alert >}}

## Search watermarks in particular objects

Limit the search to specific object types to improve performance — either globally via `WatermarkerSettings.searchable_objects`, or per instance via `Watermarker.searchable_objects`. The flags live in `groupdocs.watermark.search.objects`.

{{< tabs "code-example-search-in-objects">}}
{{< tab "search_in_objects.py" >}}  
```python
from groupdocs.watermark import Watermarker, WatermarkerSettings
from groupdocs.watermark.search.objects import (
    SearchableObjects, WordProcessingSearchableObjects, PdfSearchableObjects,
)

def search_in_objects():
    settings = WatermarkerSettings()
    settings.searchable_objects = SearchableObjects(
        word_processing_searchable_objects=WordProcessingSearchableObjects.HYPERLINKS | WordProcessingSearchableObjects.TEXT,
        pdf_searchable_objects=PdfSearchableObjects.ALL,
    )

    with Watermarker("./document.pdf", settings) as watermarker:
        possible = watermarker.search()
        print("Found", len(possible), "possible watermark(s)")

if __name__ == "__main__":
    search_in_objects()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-in-objects.txt" >}}  
```text
Found 8 possible watermark(s)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_in_objects/search-in-objects.txt)
{{< /tab >}}
{{< /tabs >}}

### Search for hyperlink watermarks

Restrict the search to hyperlinks for a single `Watermarker` instance:

{{< tabs "code-example-search-hyperlinks">}}
{{< tab "search_hyperlinks.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.objects import PdfSearchableObjects

def search_hyperlinks():
    with Watermarker("./document.pdf") as watermarker:
        watermarker.searchable_objects.pdf_searchable_objects = PdfSearchableObjects.HYPERLINKS
        possible = watermarker.search()
        print("Found", len(possible), "hyperlink watermark(s)")

if __name__ == "__main__":
    search_hyperlinks()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-hyperlinks.txt" >}}  
```text
Found 3 hyperlink watermark(s)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_hyperlinks/search-hyperlinks.txt)
{{< /tab >}}
{{< /tabs >}}

## Search text while skipping unreadable characters

Enable tolerant matching when text contains unreadable characters between letters.

{{< tabs "code-example-search-skip-unreadable">}}
{{< tab "search_skip_unreadable.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

def search_skip_unreadable():
    with Watermarker("./document.pdf") as watermarker:
        criterion = TextSearchCriteria("CONFIDENTIAL")
        criterion.skip_unreadable_characters = True
        possible = watermarker.search(criterion)
        print("Found", len(possible), "possible watermark(s)")

if __name__ == "__main__":
    search_skip_unreadable()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "search-skip-unreadable.txt" >}}  
```text
Found 6 possible watermark(s)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks/search_skip_unreadable/search-skip-unreadable.txt)
{{< /tab >}}
{{< /tabs >}}
