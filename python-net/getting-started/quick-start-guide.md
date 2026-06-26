---
id: quick-start-guide
url: watermark/python-net/quick-start-guide
title: Quick Start Guide
linkTitle: Quick Start Guide
second_title: A simple example of how to use GroupDocs.Watermark for Python via .NET
weight: 4
keywords: quick start, hello world, get started, first watermark, add watermark, image watermark, document info, pip install, venv, virtual environment, GroupDocs.Watermark, python
description: "Set up a virtual environment, install groupdocs-watermark-net, and run three minimal examples — add a text watermark, add an image watermark, and read document info — in under five minutes."
productName: GroupDocs.Watermark for Python via .NET
hideChildren: False
toc: True
---

This guide provides a quick overview of how to set up and start using GroupDocs.Watermark for Python via .NET. The library opens a document, lets you add text or image watermarks, search for or remove existing ones, and saves the result back to the original format.

## Prerequisites

To proceed, make sure you have:

1. **Configured** environment as described in the [System Requirements]({{< ref "watermark/python-net/getting-started/system-requirements.md" >}}) topic.
2. **Optionally** you may [Get a Temporary License](https://purchase.groupdocs.com/temporary-license/) to test all the product features.

## Set Up Your Development Environment

For best practices, use a virtual environment to manage dependencies in Python applications. Learn more about virtual environments at the [Create and Use Virtual Environments](https://packaging.python.org/en/latest/guides/installing-using-pip-and-virtual-environments/#create-and-use-virtual-environments) documentation topic.

### Create and Activate a Virtual Environment

Create a virtual environment:

{{< tabs "example1">}}
{{< tab "Windows" >}}
```ps
py -m venv .venv
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m venv .venv
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m venv .venv
```
{{< /tab >}}
{{< /tabs >}}

Activate a virtual environment:

{{< tabs "example2">}}
{{< tab "Windows" >}}
```ps
.venv\Scripts\activate
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
source .venv/bin/activate
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
source .venv/bin/activate
```
{{< /tab >}}
{{< /tabs >}}

### Install `groupdocs-watermark-net` Package

After activating the virtual environment, run the following command in your terminal to install the latest version of the package:

{{< tabs "example3">}}
{{< tab "Windows" >}}
```ps
py -m pip install groupdocs-watermark-net
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 -m pip install groupdocs-watermark-net
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 -m pip install groupdocs-watermark-net
```
{{< /tab >}}
{{< /tabs >}}

Ensure the package is installed successfully. You should see the message

```bash
Successfully installed groupdocs-watermark-net-*
```

## Example 1: Add a text watermark

To quickly test the library, let's open a PDF, add a diagonal "CONFIDENTIAL" text watermark, and save the result.

{{< tabs "demo_app_add_text_watermark">}}
{{< tab "add_text_watermark.py" >}}  
```python
import os
from groupdocs.watermark import Watermarker, License
from groupdocs.watermark.watermarks import TextWatermark, Font, Color

def add_text_watermark():
    # Optionally set a license
    license_path = os.path.abspath("./GroupDocs.Watermark.lic")
    if os.path.exists(license_path):
        License().set_license(license_path)

    # Open the document, add a text watermark, and save the result
    with Watermarker("./sample.pdf") as watermarker:
        watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 48))
        watermark.foreground_color = Color.red
        watermark.opacity = 0.5
        watermark.rotate_angle = 45.0
        watermarker.add(watermark)
        watermarker.save("./watermarked.pdf")

if __name__ == "__main__":
    add_text_watermark()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}  
{{< tab-text >}}
`sample.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/getting-started/quick-start-guide/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "watermarked.pdf" >}}  
```text
Binary file (PDF, 351 KB)
```
[Download full output](/watermark/python-net/_output_files/getting-started/quick-start-guide/add_text_watermark/watermarked.pdf)
{{< /tab >}}
{{< /tabs >}}

Your folder tree should look similar to the following directory structure:

```Directory
📂 demo-app
 ├──add_text_watermark.py
 ├──sample.pdf
 └──GroupDocs.Watermark.lic (Optionally)
```

### Run the App

{{< tabs "run_the_app_add_text_watermark">}}
{{< tab "Windows" >}}
```ps
py add_text_watermark.py
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 add_text_watermark.py
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 add_text_watermark.py
```
{{< /tab >}}
{{< /tabs >}}

After running the app you can deactivate the virtual environment by executing `deactivate` or closing your shell.

### Explanation
- `Watermarker("./sample.pdf")`: Opens the document. Used as a context manager so the native document handle is released.
- `TextWatermark("CONFIDENTIAL", Font("Arial", 48))`: Builds a text watermark and its font.
- `watermark.foreground_color` / `opacity` / `rotate_angle`: Style the watermark (red, half-transparent, rotated 45°).
- `watermarker.add(watermark)` then `watermarker.save("./watermarked.pdf")`: Applies the watermark and writes the result.

## Example 2: Add an image watermark

In this example we stamp a logo image onto a Word document.

{{< tabs "demo_app_add_image_watermark">}}
{{< tab "add_image_watermark.py" >}}  
```python
import os
from groupdocs.watermark import Watermarker, License
from groupdocs.watermark.watermarks import ImageWatermark

def add_image_watermark():
    # Optionally set a license
    license_path = os.path.abspath("./GroupDocs.Watermark.lic")
    if os.path.exists(license_path):
        License().set_license(license_path)

    # Open the document, add an image watermark, and save the result
    with Watermarker("./sample.docx") as watermarker:
        watermark = ImageWatermark("./logo.png")
        watermark.opacity = 0.5
        watermarker.add(watermark)
        watermarker.save("./watermarked.docx")

if __name__ == "__main__":
    add_image_watermark()
```
{{< /tab >}}
{{< tab "sample.docx" >}}  
{{< tab-text >}}
`sample.docx` and `logo.png` are the sample files used in this example. Download [sample.docx](/watermark/python-net/_sample_files/getting-started/quick-start-guide/sample.docx) and [logo.png](/watermark/python-net/_sample_files/getting-started/quick-start-guide/logo.png).
{{< /tab-text >}}
{{< /tab >}}
{{< tab "watermarked.docx" >}}  
```text
Binary file (DOCX, 125 KB)
```
[Download full output](/watermark/python-net/_output_files/getting-started/quick-start-guide/add_image_watermark/watermarked.docx)
{{< /tab >}}
{{< /tabs >}}

### Run the App

{{< tabs "run_the_app_add_image_watermark">}}
{{< tab "Windows" >}}
```ps
py add_image_watermark.py
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 add_image_watermark.py
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 add_image_watermark.py
```
{{< /tab >}}
{{< /tabs >}}

### Explanation
- `ImageWatermark("./logo.png")`: Builds an image watermark from a logo file. You can also pass a stream.
- `watermark.opacity = 0.5`: Makes the logo half-transparent so the underlying content stays readable.
- `watermarker.add(watermark)` then `watermarker.save("./watermarked.docx")`: Applies the watermark and writes the result.

## Example 3: Read document information

Sometimes you only need a document's metadata. `get_document_info()` returns the file type, page count, and size without modifying the document.

{{< tabs "demo_app_get_document_info">}}
{{< tab "get_document_info.py" >}}  
```python
import os
from groupdocs.watermark import Watermarker, License

def get_document_info():
    # Optionally set a license
    license_path = os.path.abspath("./GroupDocs.Watermark.lic")
    if os.path.exists(license_path):
        License().set_license(license_path)

    # Open the document and read its metadata
    with Watermarker("./sample.pdf") as watermarker:
        info = watermarker.get_document_info()

        print("File type:", info.file_type)
        print("Pages:", info.page_count)
        print("Size, bytes:", info.size)

if __name__ == "__main__":
    get_document_info()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}  
{{< tab-text >}}
`sample.pdf` is the sample file used in this example. Click [here](/watermark/python-net/_sample_files/getting-started/quick-start-guide/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "get-document-info.txt" >}}  
```text
File type: Pdf (.pdf) - Pdf
Pages: 3
Size, bytes: 271889
```
[Download full output](/watermark/python-net/_output_files/getting-started/quick-start-guide/get_document_info/get-document-info.txt)
{{< /tab >}}
{{< /tabs >}}

### Run the App

{{< tabs "run_the_app_get_document_info">}}
{{< tab "Windows" >}}
```ps
py get_document_info.py
```
{{< /tab >}}
{{< tab "Linux" >}}
```bash
python3 get_document_info.py
```
{{< /tab >}}
{{< tab "macOS" >}}
```bash
python3 get_document_info.py
```
{{< /tab >}}
{{< /tabs >}}

### Explanation
- `watermarker.get_document_info()`: Returns an `IDocumentInfo` with the document's `file_type`, `page_count`, and `size`.

## Next Steps

After completing the basics, explore additional resources to enhance your usage:
- [Supported Document Formats]({{< ref "watermark/python-net/getting-started/supported-document-formats.md" >}}): Review the full list of supported file types.
- [Licensing and Subscription]({{< ref "watermark/python-net/getting-started/licensing-and-subscription.md" >}}): Check details on licensing and evaluation.
- [Developer Guide]({{< ref "watermark/python-net/developer-guide" >}}): Dive into adding, searching, modifying, and removing watermarks across every supported family.
- [Technical Support]({{< ref "watermark/python-net/technical-support" >}}): Contact support for assistance if you encounter issues.
