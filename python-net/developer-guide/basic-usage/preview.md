---
id: preview
url: watermark/python-net/basic-usage/preview
title: Document preview
linkTitle: Document preview
weight: 7
description: "Generate preview images (PNG/JPG/BMP) for document pages using GroupDocs.Watermark for Python via .NET."
keywords: document preview, page preview, render page, thumbnail, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark can render document pages as images so you can show page thumbnails without fully opening a document in a viewer. You drive the render with a `create_page_stream` callback that supplies a writable file stream for each page — the library writes the page image to it and closes it for you.

## Generate a document preview

Set `PreviewOptions` with a `create_page_stream` callback, choose the `preview_format`, and list the `page_numbers` to render.

{{< tabs "code-example-preview">}}
{{< tab "generate_preview.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.options import PreviewOptions, PreviewFormats

def generate_preview():
    # Supply a writable file stream for each page to render
    def create_page_stream(page_number):
        return open(f"./output-page-{page_number}.png", "wb")

    with Watermarker("./sample.pdf") as watermarker:
        options = PreviewOptions(create_page_stream)
        options.preview_format = PreviewFormats.PNG
        options.page_numbers = [1, 2]
        watermarker.generate_preview(options)

if __name__ == "__main__":
    generate_preview()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}  
{{< tab-text >}}
`sample.pdf` is the two-page sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/basic-usage/preview/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "generate-preview-outputs.zip" >}}  
```text
output-page-1.png (600 KB)
output-page-2.png (94 KB)
```
[Download full output](/watermark/python-net/_output_files/developer-guide/basic-usage/preview/generate_preview/generate-preview-outputs.zip)
{{< /tab >}}
{{< /tabs >}}

The page images are written to the current directory — one PNG per requested page. Use `PreviewFormats.JPEG` or `PreviewFormats.BMP` for other formats, and set `options.width` / `options.height` to control the rendered size.

{{< alert style="info" >}}
The library closes each file `create_page_stream` returns once the page is written. To act on a page as soon as it is ready, pass a second callback: `PreviewOptions(create_page_stream, release_page_stream)` calls `release_page_stream(page_number, stream)` with the object `create_page_stream` returned for that page, after the whole image is in it. A one-argument `release_page_stream(page_number)` works too. `create_page_stream` may also return an `io.BytesIO`: it stays open, and holds the page image by the time `release_page_stream` gets it.
{{< /alert >}}

{{< alert style="info" >}}
**Use case:** Generate page previews to display in a web app, dashboard, or document-management system without requiring users to download the full file.
{{< /alert >}}
