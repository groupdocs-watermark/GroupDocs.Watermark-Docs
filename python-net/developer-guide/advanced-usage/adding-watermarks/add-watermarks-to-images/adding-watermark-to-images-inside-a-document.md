---
id: adding-watermark-to-images-inside-a-document
url: watermark/python-net/adding-watermark-to-images-inside-a-document
title: Adding watermark to images inside a document
linkTitle: To images inside a document
weight: 1
description: "Add a watermark to the images embedded inside a document using GroupDocs.Watermark for Python via .NET."
keywords: watermark embedded images, get_images, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Beyond watermarking a document's pages, you can watermark the **images embedded inside** it. `Watermarker.get_images()` returns a collection of every raster image in the document, regardless of format, and each image accepts its own watermark via `add()`.

## Watermark every embedded image

The example finds all embedded images, watermarks the larger ones (over 100×100), and saves the result.

{{< tabs "code-example-watermark-images-inside">}}
{{< tab "watermark_images_inside.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color, SizingType
from groupdocs.watermark.options.pdf import PdfLoadOptions

def watermark_images_inside():
    with Watermarker("./document.pdf", PdfLoadOptions()) as watermarker:
        watermark = TextWatermark("PROTECTED", Font("Arial", 8.0))
        watermark.foreground_color = Color.red
        watermark.sizing_type = SizingType.SCALE_TO_PARENT_DIMENSIONS
        watermark.scale_factor = 1.0

        # Every raster image embedded in the document
        for image in watermarker.get_images():
            # Skip tiny images such as icons or bullets
            if image.width > 100 and image.height > 100:
                image.add(watermark)

        watermarker.save("./output.pdf")

if __name__ == "__main__":
    watermark_images_inside()
```
{{< /tab >}}
{{< tab "document.pdf" >}}  
{{< tab-text >}}
`document.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/adding-watermark-to-images-inside-a-document/document.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "output.pdf" >}}  
```text
Binary file (PDF, 1596 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/adding-watermark-to-images-inside-a-document/watermark_images_inside/output.pdf)
{{< /tab >}}
{{< /tabs >}}

For the example document (10 embedded images), 8 images larger than 100×100 are watermarked. `get_images()` works the same way for Word, Excel, PowerPoint, and other formats — open the document and iterate the returned collection. You can also pass an `ImageWatermark` to `image.add(...)` to stamp a logo onto each embedded image.
