---
id: add-image
url: watermark/python-net/add-image
title: Add image watermarks
weight: 2
description: This article shows how to add an image watermark and save the resultant document. It is capable of adding watermarks to images or documents.
keywords: add image watermark, add image watermark to image, image watermark
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
---
One of the main features of the GroupDocs.Watermark library is adding image watermarks to documents. You may add watermarks to documents or images from local disks, as well as from streams. For a full list of supported document formats, check [Supported formats]({{< ref "watermark/python-net/getting-started/supported-document-formats.md" >}}).

To add an image watermark perform the following sample:

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.common as gwс

def run():
  with gw.Watermarker("sample.xlsx") as watermarker:
      watermark = gww.ImageWatermark("logo.png")
      watermark.horizontal_alignment = gwс.HorizontalAlignment.CENTER
      watermark.vertical_alignment = gwс.VerticalAlignment.CENTER

      watermarker.add(watermark)
      watermarker.save(join(output_directory, "result.xlsx"))
```

### What's next

GroupDocs.Watermark offers many more capabilities for adding image watermarks. It's possible  from streams, use absolute or relative positioning, and so on.
