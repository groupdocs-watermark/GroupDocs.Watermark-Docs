---
id: clear
url: watermark/python-net/basic-usage/clear
title: Clear watermarks
weight: 6
description: "Search and remove existing text or image watermarks using Python via .NET."
keywords: clear text watermark, clear image watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Removing existing watermarks is supported for many formats. Check supported formats to confirm availability.

## Deleting text watermarks

Search for and remove specific text watermarks from documents. You can target them by their text value and clear them in a single step.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("C:\\Docs\\watermarked-sample.docx") as watermarker:
    criteria = gws_sc.TextSearchCriteria("Contract Draft", False)
    possible = watermarker.search(criteria)
    possible.clear()
    watermarker.save("C:\\Docs\\clean-sample.docx")
```
🔹 Use case: Remove outdated labels such as “Draft” or “Internal Use Only” before sharing the document externally.

## Deleting image watermarks

Easily find and delete image watermarks (such as logos, stamps, or backgrounds) using perceptual image matching.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.search.searchcriteria as gws_sc

with gw.Watermarker("watermarked-sample.docx") as watermarker:
    image_criteria = gws_sc.ImageDctHashSearchCriteria("logo.png")
    image_criteria.max_difference = 0.9
    possible = watermarker.search(image_criteria)
    possible.clear()
    watermarker.save("clean-sample.docx")
```

🔹 Use case: Clean up old branding or remove unauthorized third-party logos from documents.
