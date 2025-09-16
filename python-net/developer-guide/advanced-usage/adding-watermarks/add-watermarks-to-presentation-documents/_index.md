---
id: add-watermarks-to-presentation-documents
url: watermark/python-net/add-watermarks-to-presentation-documents
title: Add watermarks to PowerPoint presentations
linkTitle: To presentations
weight: 7
description: "Add watermarks to slides with simple or advanced settings using Python via .NET."
productName: GroupDocs.Watermark for Python via .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark allows you to add watermarks to slides, master slides, layout slides, notes, and background images in PowerPoint presentations.

## Adding watermark to a particular slide

Apply text or image watermarks to specific slides by targeting them with PresentationWatermarkSlideOptions.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.presentation as gwo_ppt

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    text_wm = gww.TextWatermark("Test watermark", gww.Font("Arial", 8.0))
    text_opts = gwo_ppt.PresentationWatermarkSlideOptions()
    text_opts.slide_index = 0
    watermarker.add(text_wm, text_opts)

    with gww.ImageWatermark("logo.jpg") as img_wm:
        img_opts = gwo_ppt.PresentationWatermarkSlideOptions()
        img_opts.slide_index = 1
        watermarker.add(img_wm, img_opts)
    watermarker.save("presentation.pptx")
```
🔹 Use case: Place a disclaimer on the title slide and a logo on the second slide.

## Protecting watermark using unreadable characters

You can lock watermarks so that users cannot edit or remove them easily.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.presentation as gwo_ppt

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    watermark = gww.TextWatermark("Watermark text", gww.Font("Arial", 19.0))
    options = gwo_ppt.PresentationWatermarkSlideOptions()
    options.is_locked = True
    options.protect_with_unreadable_characters = True
    watermarker.add(watermark, options)
    watermarker.save("presentation.pptx")
```

🔹 Use case: Protect sensitive slides by embedding non-removable watermarks.

## Getting slide dimensions

Retrieve slide width and height programmatically.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.contents.presentation as gwc_ppt

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    content = watermarker.get_content(gwc_ppt.PresentationContent)
    print(content.slide_width)
    print(content.slide_height)
```
🔹 Use case: Dynamically size watermarks to match slide proportions.

## Working with masters, layouts, and notes

You can add watermarks to master slides, layout slides, notes, and handouts.

```python
import groupdocs.watermark as gw
import groupdocs.watermark.watermarks as gww
import groupdocs.watermark.options.presentation as gwo_ppt
import groupdocs.watermark.contents.presentation as gwc_ppt

load_options = gw.PresentationLoadOptions()
with gw.Watermarker("presentation.pptx", load_options) as watermarker:
    watermark = gww.TextWatermark("Test watermark", gww.Font("Arial", 8.0))
    content = watermarker.get_content(gwc_ppt.PresentationContent)

    master_opts = gwo_ppt.PresentationWatermarkMasterSlideOptions()
    master_opts.master_slide_index = -1
    watermarker.add(watermark, master_opts)

    if content.layout_slides is not None:
        layout_opts = gwo_ppt.PresentationWatermarkLayoutSlideOptions()
        layout_opts.layout_slide_index = -1
        watermarker.add(watermark, layout_opts)

    for i in range(content.slides.count):
        if content.slides[i].notes_slide is not None:
            note_opts = gwo_ppt.PresentationWatermarkNoteSlideOptions()
            note_opts.slide_index = i
            watermarker.add(watermark, note_opts)

    if content.master_handout_slide is not None:
        handout_opts = gwo_ppt.PresentationWatermarkMasterHandoutSlideOptions()
        watermarker.add(watermark, handout_opts)

    if content.master_notes_slide is not None:
        notes_opts = gwo_ppt.PresentationWatermarkMasterNotesSlideOptions()
        watermarker.add(watermark, notes_opts)

    watermarker.save("presentation.pptx")
```
🔹 Use case: Apply a company logo watermark across all slides, notes, and handouts to enforce consistent branding.

## Advanced use cases

- [Working with slide backgrounds]({{< ref "working-with-slide-backgrounds" >}})


