---
id: update
url: watermark/python-net/basic-usage/update
title: Update watermarks
weight: 5
description: "Search and update existing text or image watermarks using Python via .NET."
keywords: update text watermark, update image watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Search for existing watermarks and update them.

## Updating text watermarks

Easily find and modify existing text watermarks in documents. With Python, you can search for a watermark by its text content and update it with a new value.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("C:\\Docs\\watermarked-sample.docx") as watermarker:
    criteria = gws_sc.TextSearchCriteria("Contract Draft", False)
    possible = watermarker.search(criteria)
    print("Found", possible.count, "possible watermark(s).")
    for wm in possible:
        try:
            wm.text = "Contract is no longer valid"
        except Exception:
            pass
    watermarker.save("C:\\Docs\\updated-sample.docx")
```

## Updating image watermarks

Quickly replace old or incorrect image watermarks with new ones. Python developers can search for an image watermark using perceptual hashing and swap it with an updated logo or graphic.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("C:\\Docs\\watermarked-sample.docx") as watermarker:
    image_criteria = gws_sc.ImageDctHashSearchCriteria("C:\\Docs\\logo.png")
    image_criteria.max_difference = 0.9
    possible = watermarker.search(image_criteria)
    print("Found", possible.count, "possible watermark(s).")
    with open("C:\\Docs\\new-logo.png", "rb") as f:
        image_data = f.read()
    for wm in possible:
        try:
            wm.image_data = image_data
        except Exception:
            pass
    watermarker.save("C:\\Docs\\updated-sample.docx")
```


