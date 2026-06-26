---
id: existing-objects-in-pdf-document
url: watermark/python-net/existing-objects-in-pdf-document
title: Existing objects in PDF document
linkTitle: Existing objects in PDF document
weight: 2
description: "Inspect, modify, and remove existing PDF page objects — XObjects, artifacts, and annotations — using GroupDocs.Watermark for Python via .NET."
keywords: pdf xobjects, artifacts, annotations, remove watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

`Watermarker.get_content()` returns a `PdfContent` whose `pages` expose three collections of existing objects: `xobjects`, `artifacts`, and `annotations`. You can iterate them to read their properties, modify them, or remove them.

## Extract information about page objects

The example below reports the objects on the first page of a watermarked PDF.

{{< tabs "code-example-pdf-existing-objects">}}
{{< tab "extract_objects.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.pdf import PdfLoadOptions

def extract_objects():
    with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
        content = watermarker.get_content()
        page = content.pages[0]
        print(f"Page 1: xobjects={len(page.xobjects)} "
              f"artifacts={len(page.artifacts)} annotations={len(page.annotations)}")
        for artifact in page.artifacts:
            text = (artifact.text or "").strip()
            print(f"  artifact text={text!r} size={round(artifact.width)}x{round(artifact.height)}")
        for annotation in page.annotations:
            text = (annotation.text or "").strip()
            print(f"  annotation text={text!r} size={round(annotation.width)}x{round(annotation.height)}")

if __name__ == "__main__":
    extract_objects()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/existing-objects-in-pdf-document/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "extract-objects.txt" >}}  
```text
Page 1: xobjects=2 artifacts=2 annotations=0
  artifact text='CONFIDENTIAL' size=268x36
  artifact text='' size=135x40
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/existing-objects-in-pdf-document/extract_objects/extract-objects.txt)
{{< /tab >}}
{{< /tabs >}}

Each object exposes `text`, `image`, `x`, `y`, `width`, `height`, and `rotate_angle` (artifacts also expose `opacity`, `artifact_type`, and `artifact_subtype`).

## Remove and modify objects

Each collection supports `remove_at(index)` and `remove(object)`. Iterate in reverse when removing by index:

{{< tabs "code-example-pdf-remove-objects">}}
{{< tab "remove_and_modify_objects.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options.pdf import PdfLoadOptions

def remove_and_modify_objects():
    with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
        content = watermarker.get_content()
        for page in content.pages:
            for i in range(len(page.artifacts) - 1, -1, -1):
                if page.artifacts[i].text and "watermark" in page.artifacts[i].text.lower():
                    page.artifacts.remove_at(i)
        watermarker.save("./output.pdf")

if __name__ == "__main__":
    remove_and_modify_objects()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/existing-objects-in-pdf-document/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 394 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/existing-objects-in-pdf-document/remove_and_modify_objects/output.pdf)
{{< /tab >}}
{{< /tabs >}}

You can replace an object's text by assigning to `obj.text`, replace its image by assigning bytes to `obj.image_data`, and add a watermark to an image object via `image.add(watermark)` after locating it with `page.find_images()`.
