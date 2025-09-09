---
id: add-watermarks-to-images
url: watermark/python-net/add-watermarks-to-images
title: Add watermarks to images
linkTitle: To images
weight: 5
description: "Add watermarks to photos or multi-framed images using Python via .NET."
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

## Add watermark to photos or multi-framed images

For animated GIF or multi-frame TIFF images, add watermarks to specific frames using `frame_index` in `TiffImageWatermarkOptions` or `GifImageWatermarkOptions`.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.image as gwo_img

load_options = gw.TiffImageLoadOptions()
with gw.Watermarker("image.tiff", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 19.0))
    options = gwo_img.TiffImageWatermarkOptions()
    options.frame_index = 0
    watermarker.add(watermark, options)
    watermarker.save("image.tiff")
```

## Advanced use cases

- [Adding watermark to images inside a document]({{< ref "adding-watermark-to-images-inside-a-document" >}})


