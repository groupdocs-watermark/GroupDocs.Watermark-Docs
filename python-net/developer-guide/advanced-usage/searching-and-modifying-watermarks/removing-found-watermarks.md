---
id: removing-found-watermarks
url: watermark/python-net/removing-found-watermarks
title: Removing found watermarks
weight: 3
description: "Find and remove text, image, and hyperlink watermarks using Python via .NET."
keywords: remove watermark, clear watermarks, remove hyperlink watermark, text formatting criteria
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Remove watermark

Search for possible watermarks and remove them from the document.

```python
import groupdocs.watermark as gw

with gw.Watermarker("document.pdf") as watermarker:
    possible = watermarker.search()

    # Remove watermark at the specified index
    possible.remove_at(0)

    # Remove a specific watermark instance
    if possible.count > 0:
        possible.remove(possible[0])

    watermarker.save("document.pdf")
```

## Remove watermark with particular text formatting

Search and clear watermarks that match font and color parameters.

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
    possible.clear()

    watermarker.save("document.pdf")
```

## Remove hyperlink watermarks

Find and remove hyperlinks with a particular URL using a regex. Ensure only hyperlinks are cleared.

```python
import re
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc
import groupdocs.watermark.search as gws

with gw.Watermarker("document.pdf") as watermarker:
    possible = watermarker.search(gws_sc.TextSearchCriteria(re.compile(r"someurl\.com")))
    # iterate backwards when removing by index
    for i in range(possible.count - 1, -1, -1):
        if isinstance(possible[i], gws.HyperlinkPossibleWatermark):
            print(possible[i].text)
            possible.remove_at(i)

    watermarker.save("document.pdf")
```


