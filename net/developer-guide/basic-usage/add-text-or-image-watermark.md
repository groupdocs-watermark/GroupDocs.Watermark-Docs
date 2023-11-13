---
id: add-text-or-image-watermark
url: watermark/net/add-text-or-image-watermark
title: Add text or image watermark
weight: 8
description: This article shows how to add a watermark and save the resultant document. GroupDocs.Watermark is capable of adding watermarks to images or documents.
keywords: add watermark, add watermark to image
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
GroupDocs.Watermark allows adding watermarks and saving the resultant document. It is capable of adding watermarks to images or documents. See [Supported formats]({{< ref "watermark/net/getting-started/supported-document-formats.md" >}}) for a full list of supported document formats. You may add text and image watermarks to documents or images from local disks and from streams.

## Add a text watermark

The following example demonstrates how to add a [TextWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark) to a local document:

* [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) an instance of the `Watermarker` class for the local file (line 1);
* [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark/constructors/main) a watermark with text and font (line 3);
* Set the watermark [color](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark/properties/foregroundcolor), [horizontal](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermark/properties/horizontalalignment) and [vertical](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermark/properties/verticalalignment) alignments (lines 4-6);
* [Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/add) the watermark to the document (line 7);
* [Save](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/4) the document to the new file (line 8).

**BasicUsage.AddATextWatermark**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    TextWatermark watermark = new TextWatermark("top secret", new Font("Arial", 36));
    watermark.ForegroundColor = Color.Red;
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    watermarker.Add(watermark);
    watermarker.Save("document.pdf");
}
```

## Add an image watermark

The following example demonstrates how to add an [ImageWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/imagewatermark) to a document from a stream:

* [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/main) an instance of the `Watermarker` class for the file stream (line 1);
* [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/imagewatermark/constructors/1) an image watermark from the local image file (line 3);
* Set the watermark [horizontal](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermark/properties/horizontalalignment) and [vertical](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermark/properties/verticalalignment) alignments (lines 5, 6);
* [Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/add) the watermark to the document (line 7);
* [Save](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/4) the document to the new file (line 10).

**BasicUsage.AddAnImageWatermark**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.xlsx"
using (FileStream stream = File.Open("document.xlsx", FileMode.Open, FileAccess.ReadWrite))
{
    using (Watermarker watermarker = new Watermarker(stream))
    {
        using (ImageWatermark watermark = new ImageWatermark("logo.png"))
        {
            watermark.HorizontalAlignment = HorizontalAlignment.Center;
            watermark.VerticalAlignment = VerticalAlignment.Center;
            watermarker.Add(watermark);
        }

        watermarker.Save("document.xlsx");
    }
}
```

