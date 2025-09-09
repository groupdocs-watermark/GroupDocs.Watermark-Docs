---
id: working-with-slide-backgrounds
url: watermark/python-net/working-with-slide-backgrounds
title: Working with slide backgrounds
weight: 1
description: "Extract, remove, and watermark slide background images using Python via .NET."
keywords: Adding watermark, Adding watermark to all background images
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

The API allows you to extract information about all slide backgrounds, remove a particular background, and add watermark to all background images.

## Extracting information about all slide backgrounds

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.presentation as gwc_ppt

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    content = watermarker.get_content(gwc_ppt.PresentationContent)
    for slide in content.slides:
        if slide.image_fill_format.background_image is not None:
            print(slide.image_fill_format.background_image.width)
            print(slide.image_fill_format.background_image.height)
            print(len(slide.image_fill_format.background_image.get_bytes()))
```

## Removing a particular background

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.presentation as gwc_ppt

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    content = watermarker.get_content(gwc_ppt.PresentationContent)
    content.slides[0].image_fill_format.background_image = None
    watermarker.save("presentation.pptx")
```

## Adding watermark to all background images

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.presentation as gwc_ppt
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwc

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    watermark = gww.TextWatermark("Protected image", gww.Font("Arial", 8.0))
    watermark.horizontal_alignment = gwc.HorizontalAlignment.CENTER
    watermark.vertical_alignment = gwc.VerticalAlignment.CENTER
    watermark.rotate_angle = 45
    watermark.sizing_type = gww.SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 1.0

    content = watermarker.get_content(gwc_ppt.PresentationContent)
    for slide in content.slides:
        if slide.image_fill_format.background_image is not None:
            slide.image_fill_format.background_image.add(watermark)

    watermarker.save("presentation.pptx")
```

## Additional settings for slide background image

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.presentation as gwc_ppt

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    content = watermarker.get_content(gwc_ppt.PresentationContent)
    slide = content.slides[0]
    with open("background.png", "rb") as f:
        slide.image_fill_format.background_image = gwc_ppt.PresentationWatermarkableImage(f.read())
    slide.image_fill_format.tile_as_texture = True
    slide.image_fill_format.transparency = 0.5
    watermarker.save("presentation.pptx")
```

## Settings background image for charts

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.presentation as gwc_ppt

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    content = watermarker.get_content(gwc_ppt.PresentationContent)
    with open("test.png", "rb") as f:
        content.slides[0].charts[0].image_fill_format.background_image = \
            gwc_ppt.PresentationWatermarkableImage(f.read())
    content.slides[0].charts[0].image_fill_format.transparency = 0.5
    content.slides[0].charts[0].image_fill_format.tile_as_texture = True
    watermarker.save("presentation.pptx")
```


