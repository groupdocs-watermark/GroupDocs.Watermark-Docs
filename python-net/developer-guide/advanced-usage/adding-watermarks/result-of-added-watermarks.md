---
id: result-of-added-watermarks
url: watermark/python-net/result-of-added-watermarks
title: Result of added watermarks
linkTitle: Result of added watermarks
weight: 3
description: "Review the AddWatermarkResult returned by add() — the count and per-watermark details such as id, type, page number, and position — using GroupDocs.Watermark for Python via .NET."
keywords: AddWatermarkResult, added watermark id, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

`Watermarker.add()` returns an `AddWatermarkResult` describing what was added. It exposes `number_applied_watermarks` and a `succeeded` collection; each succeeded item carries a unique identifier (`watermark_id`), the `watermark_type`, the `page_number`, the `watermark_position`, and the placed geometry (`left`, `top`, `width`, `height`). This enables tracing, searching, and removing specific watermarks later.

## Review the result of added watermarks

The example below adds a text watermark to a two-page PDF and prints the result for each applied watermark.

{{< tabs "code-example-result-of-added-watermarks">}}
{{< tab "get_add_result.py" >}}  
```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font
from groupdocs.watermark.common import HorizontalAlignment, VerticalAlignment

def get_add_result():
    with Watermarker("./sample.pdf") as watermarker:
        watermark = TextWatermark("Test watermark", Font("Arial", 19.0))
        watermark.horizontal_alignment = HorizontalAlignment.CENTER
        watermark.vertical_alignment = VerticalAlignment.CENTER

        result = watermarker.add(watermark)
        print("Applied watermarks:", result.number_applied_watermarks)
        for item in result.succeeded:
            print(f"- id={item.watermark_id} type={item.watermark_type} "
                  f"page={item.page_number} position={item.watermark_position}")

if __name__ == "__main__":
    get_add_result()
```
{{< /tab >}}
{{< tab "sample.pdf" >}}  
{{< tab-text >}}
`sample.pdf` is the two-page sample file used in this example. Click [here](/watermark/python-net/_sample_files/developer-guide/advanced-usage/adding-watermarks/result-of-added-watermarks/sample.pdf) to download it.
{{< /tab-text >}}
{{< /tab >}}
{{< tab "get-add-result.txt" >}}  
```text
Applied watermarks: 3
- id=655b60a3-9c9e-4a6a-9f84-d78100469157 type=0 page=1 position=1
- id=f72574bf-306a-4b4b-8c71-3634a6080c6c type=0 page=2 position=1
- id=d3cd2017-3b63-4ae1-8e8c-c625c294f58a type=0 page=3 position=1
```
[Download full output](/watermark/python-net/_output_files/developer-guide/advanced-usage/adding-watermarks/result-of-added-watermarks/get_add_result/get-add-result.txt)
{{< /tab >}}
{{< /tabs >}}

The watermark was added to both pages, so `succeeded` contains two items, each with its own `watermark_id`. The `watermark_type` and `watermark_position` are enum values (here `type=0` corresponds to a text watermark). The `watermark_id` GUIDs let you locate and remove these exact watermarks in a later session.
