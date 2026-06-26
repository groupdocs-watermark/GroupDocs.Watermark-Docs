---
id: existing-objects-in-diagram-document
url: watermark/python-net/existing-objects-in-diagram-document
title: Existing objects in diagrams
linkTitle: Existing objects in diagrams
weight: 1
description: "Inspect, modify, and remove shapes and headers/footers in Visio diagrams using GroupDocs.Watermark for Python via .NET."
keywords: visio shapes, diagram watermark, remove shape, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

`Watermarker.get_content()` returns a `DiagramContent` whose `pages` expose the diagram's `shapes` and headers/footers. You can iterate the shapes to read their properties, modify them, or remove them.

## Extract information about shapes

The example reports the shapes on the first page of a Visio diagram.

{{< tabs "code-example-diagram-existing-objects">}}
{{< tab "extract_shapes.py" >}}  
```python
from groupdocs.watermark import Watermarker

def extract_shapes():
    with Watermarker("./diagram.vsdx") as watermarker:
        content = watermarker.get_content()
        page = content.pages[0]
        print(f"Pages: {len(content.pages)}; page 1 shapes: {len(page.shapes)}")
        for shape in page.shapes:
            text = (shape.text or "").strip()
            print(f"  shape name={shape.name!r} text={text!r} "
                  f"size={round(shape.width)}x{round(shape.height)}")

if __name__ == "__main__":
    extract_shapes()
```
{{< /tab >}}
{{< tab "diagram.vsdx" >}}  
{{< tab-text >}}
`diagram.vsdx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/existing-objects-in-diagram-document/diagram.vsdx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "extract-shapes.txt" >}}  
```text
Pages: 2; page 1 shapes: 12
  shape name='Rectangle' text='' size=108x72
  shape name='Circle' text='' size=108x108
  shape name='Square' text='' size=108x108
  shape name='Octagon' text='' size=108x108
  shape name='Sheet.20' text='' size=216x63
  shape name='Sheet.21' text='' size=216x54
  shape name='Triangle' text='' size=108x94
  shape name='Sheet.33' text='' size=85x0
  shape name='Sheet.34' text='' size=108x0
[TRUNCATED]
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-diagram-documents/existing-objects-in-diagram-document/extract_shapes/extract-shapes.txt)
{{< /tab >}}
{{< /tabs >}}

Each shape exposes `name`, `text`, `image`, `x`, `y`, `width`, `height`, and `rotate_angle`.

## Remove and modify shapes

The `shapes` collection supports `remove_at(index)` and `remove(shape)`. Iterate in reverse when removing by index:

{{< tabs "code-example-diagram-remove-shapes">}}
{{< tab "remove_and_modify_shapes.py" >}}  
```python
from groupdocs.watermark import Watermarker

def remove_and_modify_shapes():
    with Watermarker("./diagram.vsdx") as watermarker:
        content = watermarker.get_content()
        for page in content.pages:
            for i in range(len(page.shapes) - 1, -1, -1):
                if page.shapes[i].name == "Rectangle":
                    page.shapes.remove_at(i)
        watermarker.save("./output.vsdx")

if __name__ == "__main__":
    remove_and_modify_shapes()
```
{{< /tab >}}
{{< tab "diagram.vsdx" >}}  
{{< tab-text >}}
`diagram.vsdx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/existing-objects-in-diagram-document/diagram.vsdx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.vsdx" >}}  
```text
Binary file (VSDX, 29 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-diagram-documents/existing-objects-in-diagram-document/remove_and_modify_shapes/output.vsdx)
{{< /tab >}}
{{< /tabs >}}

You can replace a shape's text by assigning to `shape.text`, replace its image by assigning a `DiagramWatermarkableImage` to `shape.image`, and modify its position and size through `x`, `y`, `width`, `height`, and `rotate_angle`.
