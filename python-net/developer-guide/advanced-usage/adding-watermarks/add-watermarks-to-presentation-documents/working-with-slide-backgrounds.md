---
id: working-with-slide-backgrounds
url: watermark/python-net/working-with-slide-backgrounds
title: Working with slide backgrounds
linkTitle: Working with slide backgrounds
weight: 1
description: "Extract, remove, and watermark PowerPoint slide background images using GroupDocs.Watermark for Python via .NET."
keywords: slide background, presentation background image, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

`Watermarker.get_content()` returns a `PresentationContent` whose `slides` each expose an `image_fill_format` with a `background_image`, `tile_as_texture`, and `transparency`. The background image is `None` when the slide has no image fill.

## Extract information about slide backgrounds

{{< tabs "code-example-extract-slide-backgrounds">}}
{{< tab "extract_slide_backgrounds.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.presentation import PresentationLoadOptions

def extract_slide_backgrounds():
    with Watermarker("./presentation.pptx", PresentationLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for i, slide in enumerate(content.slides):
            background = slide.image_fill_format.background_image
            if background is not None:
                print(f"Slide {i}: background {background.width}x{background.height}")
            else:
                print(f"Slide {i}: no background image")

if __name__ == "__main__":
    extract_slide_backgrounds()
```
{{< /tab >}}
{{< tab "presentation.pptx" >}}  
{{< tab-text >}}
`presentation.pptx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/working-with-slide-backgrounds/presentation.pptx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "extract-slide-backgrounds.txt" >}}  
```text
Slide 0: no background image
Slide 1: no background image
Slide 2: no background image
Slide 3: no background image
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/working-with-slide-backgrounds/extract_slide_backgrounds/extract-slide-backgrounds.txt)
{{< /tab >}}
{{< /tabs >}}

## Remove a slide background

Set the `background_image` to `None`:

{{< tabs "code-example-remove-slide-background">}}
{{< tab "remove_slide_background.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.presentation import PresentationLoadOptions

def remove_slide_background():
    with Watermarker("./presentation.pptx", PresentationLoadOptions()) as watermarker:
        content = watermarker.get_content()
        content.slides[0].image_fill_format.background_image = None
        watermarker.save("./output.pptx")

if __name__ == "__main__":
    remove_slide_background()
```
{{< /tab >}}
{{< tab "presentation.pptx" >}}  
{{< tab-text >}}
`presentation.pptx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/working-with-slide-backgrounds/presentation.pptx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pptx" >}}  
```text
Binary file (PPTX, 196 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/working-with-slide-backgrounds/remove_slide_background/output.pptx)
{{< /tab >}}
{{< /tabs >}}

## Watermark existing slide backgrounds

{{< tabs "code-example-watermark-slide-backgrounds">}}
{{< tab "watermark_slide_backgrounds.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.options.presentation import PresentationLoadOptions

def watermark_slide_backgrounds():
    with Watermarker("./presentation.pptx", PresentationLoadOptions()) as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        watermark.foreground_color = Color.red
        content = watermarker.get_content()
        for slide in content.slides:
            if slide.image_fill_format.background_image is not None:
                slide.image_fill_format.background_image.add(watermark)
        watermarker.save("./output.pptx")

if __name__ == "__main__":
    watermark_slide_backgrounds()
```
{{< /tab >}}
{{< tab "presentation.pptx" >}}  
{{< tab-text >}}
`presentation.pptx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/working-with-slide-backgrounds/presentation.pptx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pptx" >}}  
```text
Binary file (PPTX, 196 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/working-with-slide-backgrounds/watermark_slide_backgrounds/output.pptx)
{{< /tab >}}
{{< /tabs >}}

You can also tune `image_fill_format.transparency` (0.0–1.0) and `image_fill_format.tile_as_texture` when setting a background image. The same `image_fill_format` is available on chart objects.
