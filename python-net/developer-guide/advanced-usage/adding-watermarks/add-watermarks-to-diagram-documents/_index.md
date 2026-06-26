---
id: add-watermarks-to-diagram-documents
url: watermark/python-net/add-watermarks-to-diagram-documents
title: Add watermarks to Diagram documents
linkTitle: Diagram documents
weight: 10
description: "Add watermarks to Visio/diagram pages using GroupDocs.Watermark for Python via .NET."
keywords: add watermark, visio watermark, diagram, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: False
toc: true
---

GroupDocs.Watermark adds watermarks to Visio diagrams as shapes placed on the background or foreground of the pages. Open the diagram and pass a `DiagramShapeWatermarkOptions` to `add()` with the desired `placement_type`.

{{< alert style="info" >}}
Open Visio files with format auto-detection — `Watermarker("diagram.vsdx")` — rather than passing `DiagramLoadOptions()` to the constructor.
{{< /alert >}}

## Add a watermark to a diagram

{{< tabs "code-example-add-watermark-to-diagram">}}
{{< tab "add_watermark_to_diagram.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment
from groupdocs.watermark.options.diagram import DiagramShapeWatermarkOptions
from groupdocs.watermark.contents.diagram import DiagramWatermarkPlacementType

def add_watermark_to_diagram():
    with Watermarker("./diagram.vsdx") as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 19.0))
        watermark.foreground_color = Color.red
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER

        # Place the watermark on the background of every page
        options = DiagramShapeWatermarkOptions()
        options.placement_type = DiagramWatermarkPlacementType.BACKGROUND_PAGES
        watermarker.add(watermark, options)

        watermarker.save("./output.vsdx")

if __name__ == "__main__":
    add_watermark_to_diagram()
```
{{< /tab >}}
{{< tab "diagram.vsdx" >}}  
{{< tab-text >}}
`diagram.vsdx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-diagram-documents/diagram.vsdx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.vsdx" >}}  
```text
Binary file (VSDX, 29 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-diagram-documents/add_watermark_to_diagram/output.vsdx)
{{< /tab >}}
{{< /tabs >}}

Use `DiagramWatermarkPlacementType.FOREGROUND_PAGES` to place the watermark in front of the page content instead. `Watermarker.get_content()` returns a `DiagramContent` exposing each page's shapes and headers/footers — see [Existing objects in diagrams]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-diagram-documents/existing-objects-in-diagram-document.md" >}}).
