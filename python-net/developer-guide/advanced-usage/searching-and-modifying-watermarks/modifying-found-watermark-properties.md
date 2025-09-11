---
id: modifying-found-watermark-properties
url: watermark/python-net/modifying-found-watermark-properties
title: Modifying found watermark properties
weight: 2
description: "Search and update existing text or image watermarks using Python via .NET."
keywords: modify watermark text, replace watermark image, formatted text fragments
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark lets you replace text or images in watermarks that already exist in a document.

## Replacing text

Loop through found watermarks and set the `text` property.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("document.pdf") as watermarker:
    criteria = gws_sc.TextSearchCriteria("test", False)
    possible = watermarker.search(criteria)
    for wm in possible:
        try:
            wm.text = "passed"
        except Exception:
            # Entity may not support text editing or the value is invalid
            pass
    watermarker.save("document.pdf")
```

## Replacing text with formatting

Use `formatted_text_fragments` to set styled text.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc
import groupdocs.watermark.watermarks as gww

with gw.Watermarker("document.pdf") as watermarker:
    criteria = gws_sc.TextSearchCriteria("test", False)
    possible = watermarker.search(criteria)
    for wm in possible:
        try:
            wm.formatted_text_fragments.clear()
            wm.formatted_text_fragments.add(
                "passed",
                gww.Font("Calibri", 19.0, gww.FontStyle.BOLD),
                gww.Color.red,
                gww.Color.aqua,
            )
        except Exception:
            # Entity may not support formatted text or values may be invalid
            pass
    watermarker.save("document.pdf")
```

## Replacing image

Swap the image data of matched watermarks.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with open("image.png", "rb") as f:
    image_data = f.read()

with gw.Watermarker("document.pdf") as watermarker:
    criteria = gws_sc.ImageDctHashSearchCriteria("logo.bmp")
    possible = watermarker.search(criteria)
    for wm in possible:
        try:
            wm.image_data = image_data
        except Exception:
            # Entity may not support image replacement or image format is invalid
            pass
    watermarker.save("document.pdf")
```


