---
id: add-watermarks-to-presentation-documents
url: watermark/python-net/add-watermarks-to-presentation-documents
title: Add watermarks to PowerPoint presentations
linkTitle: To presentations
weight: 7
description: "Add watermarks to a particular slide, master, layout, or notes slide using GroupDocs.Watermark for Python via .NET."
keywords: add watermark, presentation watermark, slide, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Open a presentation with `PresentationLoadOptions` and pass a presentation-specific watermark option to `add()` to target a particular slide.

## Add a watermark to a particular slide

Use `PresentationWatermarkSlideOptions` and set `slide_index` (0-based) to add the watermark to a specific slide.

{{< tabs "code-example-add-watermark-to-slide">}}
{{< tab "add_watermark_to_slide.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment
from groupdocs.watermark.options.presentation import (
    PresentationLoadOptions, PresentationWatermarkSlideOptions,
)

def add_watermark_to_slide():
    with Watermarker("./presentation.pptx", PresentationLoadOptions()) as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        watermark.foreground_color = Color.red
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER

        options = PresentationWatermarkSlideOptions()
        options.slide_index = 0
        watermarker.add(watermark, options)

        watermarker.save("./output.pptx")

if __name__ == "__main__":
    add_watermark_to_slide()
```
{{< /tab >}}
{{< tab "presentation.pptx" >}}  
{{< tab-text >}}
`presentation.pptx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/presentation.pptx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pptx" >}}  
```text
Binary file (PPTX, 241 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/add_watermark_to_slide/output.pptx)
{{< /tab >}}
{{< /tabs >}}

You can also add watermarks to master, layout, and notes slides with `PresentationWatermarkMasterSlideOptions`, `PresentationWatermarkLayoutSlideOptions`, and `PresentationWatermarkNoteSlideOptions`. `Watermarker.get_content()` returns a `PresentationContent` exposing each slide and its background.

For working with slide backgrounds and charts, see [Working with slide backgrounds]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/working-with-slide-backgrounds.md" >}}).
