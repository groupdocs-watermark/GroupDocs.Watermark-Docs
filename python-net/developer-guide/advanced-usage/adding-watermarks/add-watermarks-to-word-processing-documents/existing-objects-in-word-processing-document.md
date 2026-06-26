---
id: existing-objects-in-word-processing-document
url: watermark/python-net/existing-objects-in-word-processing-document
title: Existing objects in word processing document
linkTitle: Existing objects in word processing document
weight: 1
description: "Inspect, modify, and remove existing shapes (potential watermarks) in Word documents using GroupDocs.Watermark for Python via .NET."
keywords: word shapes, remove shape, replace shape text, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

`Watermarker.get_content()` returns a `WordProcessingContent` whose `sections` each expose a `shapes` collection. Watermarks added to a Word document are shapes, so this is how you find, modify, and remove watermarks that already exist in a document.

## Extract information about shapes

{{< tabs "code-example-word-existing-objects">}}
{{< tab "extract_shapes.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.word_processing import WordProcessingLoadOptions

def extract_shapes():
    with Watermarker("./document.docx", WordProcessingLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for i, section in enumerate(content.sections):
            print(f"Section {i}: shapes={len(section.shapes)}")
            for shape in section.shapes:
                text = (shape.text or "").strip()
                print(f"  shape text={text!r} size={round(shape.width)}x{round(shape.height)} name={shape.name!r}")

if __name__ == "__main__":
    extract_shapes()
```
{{< /tab >}}
{{< tab "document.docx" >}}  
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/existing-objects-in-word-processing-document/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "extract-shapes.txt" >}}  
```text
Section 0: shapes=3
  shape text='' size=230x69 name=''
  shape text='' size=90x3 name='Rectangle 100004'
  shape text='' size=460x287 name=''
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/existing-objects-in-word-processing-document/extract_shapes/extract-shapes.txt)
{{< /tab >}}
{{< /tabs >}}

Each shape exposes `text`, `image`, `name`, `alternative_text`, `x`, `y`, `width`, `height`, `rotate_angle`, `is_word_art`, and `behind_text`.

## Remove and modify shapes

The `shapes` collection supports `remove_at(index)` and `remove(shape)`. Iterate in reverse when removing by index:

{{< tabs "code-example-word-remove-shapes">}}
{{< tab "remove_and_modify_shapes.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.word_processing import WordProcessingLoadOptions

def remove_and_modify_shapes():
    with Watermarker("./document.docx", WordProcessingLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for section in content.sections:
            for i in range(len(section.shapes) - 1, -1, -1):
                if section.shapes[i].text == "CONFIDENTIAL":
                    section.shapes.remove_at(i)
        watermarker.save("./output.docx")

if __name__ == "__main__":
    remove_and_modify_shapes()
```
{{< /tab >}}
{{< tab "document.docx" >}}  
{{< tab-text >}}
`document.docx` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/existing-objects-in-word-processing-document/document.docx) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.docx" >}}  
```text
Binary file (DOCX, 118 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/existing-objects-in-word-processing-document/remove_and_modify_shapes/output.docx)
{{< /tab >}}
{{< /tabs >}}

You can replace a shape's text by assigning to `shape.text`, replace its image by assigning a `WordProcessingWatermarkableImage` to `shape.image`, set or clear a hyperlink via `shape.hyperlink`, and modify its position, size, and `rotate_angle`. Headers and footers are available through `section.headers_footers`.
