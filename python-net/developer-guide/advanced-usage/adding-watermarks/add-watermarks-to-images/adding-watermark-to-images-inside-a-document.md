---
id: adding-watermark-to-images-inside-a-document
url: watermark/python-net/adding-watermark-to-images-inside-a-document
title: Adding watermark to images inside a document
linkTitle: To images inside a document
weight: 1
description: "Add text or image watermarks to images embedded in documents using Python via .NET."
keywords: Adding watermark, add watermark to images
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Many document formats allow embedding images. To add watermarks to images inside a document, follow these steps:

1. Load the document
2. Create and initialize watermark object
3. Set watermark properties
4. Find images in the document
5. Add watermark to all found images
6. Save the document

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

with gw.Watermarker("document.pdf") as watermarker:
    text_watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    text_watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    text_watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    text_watermark.rotate_angle = 45
    text_watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    text_watermark.scale_factor = 1.0

    with gww.ImageWatermark("protect.jpg") as image_watermark:
        image_watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
        image_watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
        image_watermark.rotate_angle = -45
        image_watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
        image_watermark.scale_factor = 1.0

        images = watermarker.get_images()
        for i in range(images.count):
            if images[i].width > 100 and images[i].height > 100:
                if i % 2 == 0:
                    images[i].add(text_watermark)
                else:
                    images[i].add(image_watermark)

    watermarker.save("document.pdf")
```


