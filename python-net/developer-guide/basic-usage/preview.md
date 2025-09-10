---
id: preview
url: watermark/python-net/basic-usage/preview
title: Document preview
weight: 7
description: "Generate preview images (PNG/JPG/BMP) for document pages using Python via .NET."
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

Generate preview images for document pages.

Easily render document pages as images for preview purposes. With Python, you can generate page thumbnails (e.g., PNG or JPG) to display documents without fully opening them in a viewer.

## Generate document preview

```python
import os
import io
import groupdocs.watermark as gw
import groupdocs.watermark.options as gwo

output_directory = os.path.join(os.getcwd(), "preview")
os.makedirs(output_directory, exist_ok=True)

def create_page_stream(number: int):
    path = os.path.join(output_directory, f"page{number}.png")
    return open(path, "wb")

def release_page_stream(number: int, stream):
    stream.close()

with gw.Watermarker("sample.pdf") as watermarker:
    preview_options = gwo.PreviewOptions(create_page_stream, release_page_stream)
    preview_options.preview_format = gwo.PreviewOptions.PreviewFormats.PNG
    preview_options.page_numbers = [1, 2]
    watermarker.generate_preview(preview_options)
```

The images will be created in the specified output directory.

🔹 Use case: Generate page previews for displaying in a web app, dashboard, or document management system without requiring end users to download the full file.

