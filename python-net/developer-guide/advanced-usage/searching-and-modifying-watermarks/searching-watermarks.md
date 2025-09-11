---
id: searching-watermarks
url: watermark/python-net/searching-watermarks
title: Searching watermarks
weight: 1
description: "Find possible text and image watermarks using Python via .NET, with powerful criteria."
keywords: search watermarks, text search, regex search, image search, combined search
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Searching possible watermarks

Use `Watermarker.search()` to scan a document for objects that can be treated as watermarks. This includes watermarks added by third‑party tools.

```python
import groupdocs.watermark as gw

with gw.Watermarker("document.pdf") as watermarker:
    possible = watermarker.search()
    for wm in possible:
        if wm.image_data is not None:
            print(len(wm.image_data))

        print("Text", wm.text)
        print("X", wm.x)
        print("Y", wm.y)
        print("RotateAngle", wm.rotate_angle)
        print("Width", wm.width)
        print("Height", wm.height)
        print("PageNumber", wm.page_number)
        print("")
```

## Search criteria

Large documents may contain many candidates. Without parameters, `search()` returns a subset such as backgrounds or floating objects. Use dedicated criteria to narrow results.

### Text search criteria

Find watermarks by exact text.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("document.pdf") as watermarker:
    text_criteria = gws_sc.TextSearchCriteria("© 2017")
    possible = watermarker.search(text_criteria)
    print("Found", possible.count, "possible watermark(s)")
```

### Regular expression search criteria

Use regex with `TextSearchCriteria`.

```python
import re
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("document.pdf") as watermarker:
    regex = re.compile(r"^© \d{4}$")
    text_criteria = gws_sc.TextSearchCriteria(regex)
    possible = watermarker.search(text_criteria)
    print("Found", possible.count, "possible watermark(s)")
```

{{< alert style="info" >}}
When `TextSearchCriteria` is provided, the API also scans the main document text along with shapes, XObjects, annotations, and other objects.
{{< /alert >}}

### Image search criteria

Find image watermarks that are visually similar to a sample image using perceptual hashing (DCT hash). Control sensitivity with `max_difference` (0–1).

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("document.pdf") as watermarker:
    image_criteria = gws_sc.ImageDctHashSearchCriteria("watermark.jpg")
    image_criteria.max_difference = 0.9
    possible = watermarker.search(image_criteria)
    print("Found", possible.count, "possible watermark(s)")
```

Other image criteria:

- `ImageColorHistogramSearchCriteria`: robust to rotation, scaling, translation.
- `ImageThumbnailSearchCriteria`: robust to rotation, scaling, minor color changes.

### Combined search criteria

Combine multiple criteria with logical And/Or/Not.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("document.pdf") as watermarker:
    image_criteria = gws_sc.ImageDctHashSearchCriteria("logo.png")
    image_criteria.max_difference = 0.9
    text_criteria = gws_sc.TextSearchCriteria("Company Name")
    angle_criteria = gws_sc.RotateAngleSearchCriteria(30, 60)

    combined = image_criteria.or_(text_criteria).and_(angle_criteria)
    possible = watermarker.search(combined)
    print("Found", possible.count, "possible watermark(s)")
```

### Text formatting search criteria

Find watermarks by text formatting such as font, size, and color ranges.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("document.pdf") as watermarker:
    criteria = gws_sc.TextFormattingSearchCriteria()
    criteria.foreground_color_range = gws_sc.ColorRange()
    criteria.foreground_color_range.min_hue = -5
    criteria.foreground_color_range.max_hue = 10
    criteria.foreground_color_range.min_brightness = 0.01
    criteria.foreground_color_range.max_brightness = 0.99
    criteria.background_color_range = gws_sc.ColorRange()
    criteria.background_color_range.is_empty = True
    criteria.font_name = "Arial"
    criteria.min_font_size = 19
    criteria.max_font_size = 42
    criteria.font_bold = True

    possible = watermarker.search(criteria)
    print("Found", possible.count, "possible watermark(s)")
```

## Searching watermarks in particular objects

Limit search to specific object types to improve performance, either globally via `WatermarkerSettings.searchable_objects` or per instance via `Watermarker.searchable_objects`.

```python
import os
import groupdocs.watermark as gw
import groupdocs.watermark.search as gws

settings = gw.WatermarkerSettings()
settings.searchable_objects = gws.SearchableObjects(
    word_processing_searchable_objects=gws.WordProcessingSearchableObjects.HYPERLINKS | gws.WordProcessingSearchableObjects.TEXT,
    spreadsheet_searchable_objects=gws.SpreadsheetSearchableObjects.HEADERS_FOOTERS,
    presentation_searchable_objects=gws.PresentationSearchableObjects.SLIDES_BACKGROUNDS | gws.PresentationSearchableObjects.SHAPES,
    diagram_searchable_objects=gws.DiagramSearchableObjects.NONE,
    pdf_searchable_objects=gws.PdfSearchableObjects.ALL,
)

files = ["document.docx", "spreadsheet.xlsx", "presentation.pptx", "diagram.vsdx", "document.pdf"]
for file in files:
    with gw.Watermarker(file, settings) as watermarker:
        possible = watermarker.search()
        print(f"In {os.path.basename(file)} found {possible.count} possible watermark(s).")
```

### Searching for hyperlink watermarks

Restrict search to hyperlinks for a specific `Watermarker` instance.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search as gws

with gw.Watermarker("document.pdf") as watermarker:
    watermarker.searchable_objects.pdf_searchable_objects = gws.PdfSearchableObjects.HYPERLINKS
    possible = watermarker.search()
    print("Found", possible.count, "hyperlink watermark(s)")
```

## Searching text watermark while skipping unreadable characters

Enable tolerant matching when text contains unreadable characters between letters.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("document.pdf") as watermarker:
    criterion = gws_sc.TextSearchCriteria("Company name")
    criterion.skip_unreadable_characters = True
    result = watermarker.search(criterion)
    print("Found", result.count, "possible watermark(s)")
```


