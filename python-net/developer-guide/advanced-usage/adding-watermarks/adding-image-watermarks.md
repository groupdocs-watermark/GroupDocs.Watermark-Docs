---
id: adding-image-watermarks
url: watermark/python-net/adding-image-watermarks
title: Adding image watermarks
linkTitle: Image watermarks
weight: 2
description: "Add image watermarks from file or stream using GroupDocs.Watermark for Python via .NET."
keywords: image watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark supports adding the following image formats as watermarks:

- BMP
- PNG
- GIF
- JPEG

## Add image watermark from local file

The following example shows how to add an `ImageWatermark` to a document. If the document consists of multiple parts (pages, worksheets, slides, frames, etc.), the watermark will be added to each of them.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww

with gw.Watermarker("presentation.pptx") as watermarker:
    with gww.ImageWatermark("watermark.jpg") as watermark:
        watermarker.add(watermark)
        watermarker.save("presentation.pptx")
```

## Add image watermark from stream

You can also use a stream of the image to initialize an `ImageWatermark` instance.

```python
import io
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww

with open("watermark.jpg", "rb") as f:
    data = f.read()

with gw.Watermarker("image.png") as watermarker:
    with gww.ImageWatermark(io.BytesIO(data)) as watermark:
        watermarker.add(watermark)
        watermarker.save("image.png")
```

For advanced usage of watermark properties (tiling, alignment, sizing, rotation, margins), see the text watermark article; the same techniques apply to image watermarks as well:

- [Adding Text Watermarks]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}})


