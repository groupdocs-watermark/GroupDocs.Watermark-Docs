---
id: result-of-added-watermarks
url: watermark/python-net/result-of-added-watermarks
title: Result of added watermarks
linkTitle: Result of added watermarks
weight: 3
description: "Review AddWatermarkResult with information about added watermarks using Python via .NET."
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark can return details about each added watermark, including a unique identifier (GUID), type, page number, and position. This enables scenarios such as tracing, searching, and removing specific watermarks by ID.

## Reviewing the result of added watermarks

The following example shows how to review `AddWatermarkResult` with information about added watermarks in a document.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww

with gw.Watermarker("sample_2_pages.pdf") as watermarker:
    font = gww.Font("Arial", 19.0, gww.FontStyle.BOLD | gww.FontStyle.ITALIC)
    watermark = gww.TextWatermark("Test watermark", font)

    watermark.foreground_color = gww.Color.red
    watermark.background_color = gww.Color.blue
    watermark.text_alignment = gww.TextAlignment.RIGHT
    watermark.opacity = 0.5

    result = watermarker.add(watermark)

    for item in result.succeeded:
        print("WatermarkId:", item.watermark_id)
        print("WatermarkType:", item.watermark_type)
        print("PageNumber:", item.page_number)
        print("WatermarkPosition:", item.watermark_position)

    watermarker.save("output.pdf")
```

Example output:

```text
WatermarkId: 1a78ef44-d497-451f-8f03-ca08ea537cc8
WatermarkType: Text
PageNumber: 1
WatermarkPosition: Default

WatermarkId: 658179cf-7b6e-472a-8b24-30f845dc2a9a
WatermarkType: Text
PageNumber: 2
WatermarkPosition: Default
```


