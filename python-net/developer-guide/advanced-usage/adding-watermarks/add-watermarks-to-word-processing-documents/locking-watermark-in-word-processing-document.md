---
id: locking-watermark-in-word-processing-document
url: watermark/python-net/locking-watermark-in-word-processing-document
title: Locking watermark in word processing document
weight: 2
description: "Lock watermarks in a Word document to restrict editing using Python via .NET."
keywords: lock the watermarks, lock the watermarks in a Word document
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

You can lock watermarks in a Word document to restrict editing. GroupDocs.Watermark provides several lock types:

- AllowOnlyRevisions
- AllowOnlyComments
- AllowOnlyFormFields
- ReadOnly
- ReadOnlyWithEditableContent

Use `lock_type` in `WordProcessingWatermarkBaseOptions` (and descendants) to set the lock type.

## Adding watermark to all pages
This sample adds a locked text watermark across all pages using a chosen lock type (and optional password).

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    watermark = gww.TextWatermark("Watermark text", gww.Font("Arial", 19.0))
    watermark.foreground_color = gww.Color.red

    options = gwo_wp.WordProcessingWatermarkPagesOptions()
    options.is_locked = True
    options.lock_type = gwo_wp.WordProcessingLockType.ALLOW_ONLY_FORM_FIELDS
    # options.password = "7654321"

    watermarker.add(watermark, options)
    watermarker.save("document.docx")
```

## Adding watermark to particular pages
This sample applies a locked watermark only to specific pages referenced by their numbers.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    watermark = gww.TextWatermark("Watermark text", gww.Font("Arial", 19.0))
    watermark.foreground_color = gww.Color.red

    options = gwo_wp.WordProcessingWatermarkPagesOptions()
    options.page_numbers = [1, 3]
    options.is_locked = True
    options.lock_type = gwo_wp.WordProcessingLockType.ALLOW_ONLY_COMMENTS
    # options.password = "7654321"

    watermarker.add(watermark, options)
    watermarker.save("document.docx")
```

## Adding watermark to a section
This sample inserts a locked watermark into a specific section, restricting edits according to the lock type.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.wordprocessing as gwo_wp

load_options = gw.WordProcessingLoadOptions()
with gw.Watermarker("document.docx", load_options) as watermarker:
    watermark = gww.TextWatermark("Watermark text", gww.Font("Arial", 19.0))
    watermark.foreground_color = gww.Color.red

    options = gwo_wp.WordProcessingWatermarkSectionOptions()
    options.section_index = 0
    options.is_locked = True
    options.lock_type = gwo_wp.WordProcessingLockType.READ_ONLY_WITH_EDITABLE_CONTENT
    # options.password = "7654321"

    watermarker.add(watermark, options)
    watermarker.save("document.docx")
```


