---
id: hello-world
url: watermark/python-net/hello-world
title: Hello, World!
second_title: A simple example of how to use GroupDocs.Watermark for Python via .NET
linkTitle: Hello World
weight: 2
keywords: "hello world, example, get started"
description: Get started with GroupDocs.Watermark for Python via .NET by creating and running a minimal example.
productName: GroupDocs.Watermark for Python via .NET
hideChildren: False
toc: True
---

## Introduction
A "Hello, World!" code is often the first simple example to write uisng "GroupDocs.Watermark for Python via .NET", and it can also be used as a sanity test to ensure the software intended to compile or run source code is correctly installed.

## Overview
"GroupDocs.Watermark for Python via .NET" library allows you to add, search and remove watermarks from the documents in various formats. There are many other file formats are [supported](/watermark/python-net/supported-document-formats/).

## Steps to Render a Document
The following steps outline how to render a document to HTML format using the GroupDocs.Watermark for Python via .Net:

1. Import `groupDocs.watermark`.
2. Import `groupDocs.watermark.watermarks` class.
3. Initialize a `Watermarker` object with the path to the sample document.
4. Initialize an `TextWatermark` object with the desired text and font for watermark.
5. Call add() method to add the watermark.

## Code Snippet
Here is a "Hello, World!" example to demonstrate the working of the "GroupDocs.Watermark for Python via .Net" API:

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gwo

def run():
    with gw.Watermarker("sample.docx") as watermarker:
        font = gwo.Font("Arial", 36.0)
        watermark = gwo.TextWatermark("top secret", font)
        watermark.x = 100.0;
        watermark.y = 250.0;

        watermarker.add(watermark)
        watermarker.save("result.docx")
```
## Run the Application
Steps to run the sample application:
1. Download the Sample Application: 
    * [Download Hello World Sample Application](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Python-via-.NET/blob/master/Examples/quick_start/hello_world.py)

2. Run the Application:
    * Navigate to the directory containing the `hello_world.py` script.
    * Run the script:
        ```bash 
        python hello_world.py
        ```

## Expected Output
After running the application, you will find Docx document with added text watermark in the output directory.

## Additional Resources
This demo application references the GroupDocs.Watermark for Python via .Net [code samples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Python-via-.NET).