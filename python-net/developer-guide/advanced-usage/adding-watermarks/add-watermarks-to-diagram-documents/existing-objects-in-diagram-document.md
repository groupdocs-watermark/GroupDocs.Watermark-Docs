---
id: existing-objects-in-diagram-document
url: watermark/python-net/existing-objects-in-diagram-document
title: Existing objects in diagrams
weight: 1
description: "Find, remove, and modify shapes and headers/footers in Visio documents using Python via .NET."
keywords: watermarks in visio
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Watermarks in Visio documents are usually shapes; sometimes headers and footers also contain text considered as watermark. You can find and remove watermarks of both types.

## Removing watermark from a particular page

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx
import groupdocs.watermark.search.searchcriteria as gws_sc

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    image_criteria = gws_sc.ImageDctHashSearchCriteria("logo.png")
    text_criteria = gws_sc.TextSearchCriteria("Company Name")
    possible = content.pages[0].search(text_criteria.or_(image_criteria))
    possible.clear()
    watermarker.save("diagram.vsdx")
```

## Working with shapes

### Extracting information about all shapes

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    for page in content.pages:
        for shape in page.shapes:
            if shape.image is not None:
                print(shape.image.width)
                print(shape.image.height)
                print(len(shape.image.get_bytes()))
            print(shape.name)
            print(shape.x)
            print(shape.y)
            print(shape.width)
            print(shape.height)
            print(shape.rotate_angle)
            print(shape.text)
            print(shape.id)
```

### Removing a particular shape

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    content.pages[0].shapes.remove_at(0)
    content.pages[0].shapes.remove(content.pages[0].shapes[0])
    watermarker.save("diagram.vsdx")
```

### Removing shapes with particular text formatting

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx
import groupdocs.watermark.watermarks as gww

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    for page in content.pages:
        for i in range(page.shapes.count - 1, -1, -1):
            for fragment in page.shapes[i].formatted_text_fragments:
                if fragment.foreground_color == gww.Color.red and fragment.font.family_name == "Arial":
                    page.shapes.remove_at(i)
                    break
    watermarker.save("diagram.vsdx")
```

### Removing hyperlink associated with a particular shape

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    shape = content.pages[0].shapes[0]
    for i in range(shape.hyperlinks.count - 1, -1, -1):
        if "http://someurl.com" in shape.hyperlinks[i].address:
            shape.hyperlinks.remove_at(i)
    watermarker.save("diagram.vsdx")
```

### Replacing text for particular shapes

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    for shape in content.pages[0].shapes:
        if shape.text and "© Aspose 2016" in shape.text:
            shape.text = "© GroupDocs 2017"
    watermarker.save("diagram.vsdx")
```

### Replacing text for particular shapes with formatted text

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx
import groupdocs.watermark.watermarks as gww

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    for shape in content.pages[0].shapes:
        if shape.text and "© Aspose 2016" in shape.text:
            shape.formatted_text_fragments.clear()
            shape.formatted_text_fragments.add(
                "© GroupDocs 2017", gww.Font("Calibri", 19.0, gww.FontStyle.BOLD), gww.Color.red, gww.Color.aqua
            )
    watermarker.save("diagram.vsdx")
```

### Replacing shape image

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    for shape in content.pages[0].shapes:
        if shape.image is not None:
            with open("test.png", "rb") as f:
                shape.image = gwc_vsdx.DiagramWatermarkableImage(f.read())
    watermarker.save("diagram.vsdx")
```

## Working with headers and footers

### Extracting information about all headers and footers

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    print(content.header_footer.font.family_name)
    print(content.header_footer.font.size)
    print(content.header_footer.font.bold)
    print(content.header_footer.font.italic)
    print(content.header_footer.font.underline)
    print(content.header_footer.font.strikeout)
    print(content.header_footer.header_left)
    print(content.header_footer.header_center)
    print(content.header_footer.header_right)
    print(content.header_footer.footer_left)
    print(content.header_footer.footer_center)
    print(content.header_footer.footer_right)
    print(content.header_footer.text_color.to_argb())
    print(content.header_footer.footer_margin)
    print(content.header_footer.header_margin)
```

### Removing or replacing a particular header and footer

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.diagram as gwc_vsdx
import groupdocs.watermark.watermarks as gww

load_options = gw.DiagramLoadOptions()
with gw.Watermarker("diagram.vsdx", load_options) as watermarker:
    content = watermarker.get_content(gwc_vsdx.DiagramContent)
    content.header_footer.header_center = None
    content.header_footer.footer_center = "Footer center"
    content.header_footer.font.size = 19
    content.header_footer.font.family_name = "Calibri"
    content.header_footer.text_color = gww.Color.red
    watermarker.save("diagram.vsdx")
```


