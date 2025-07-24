---
id: add-image
url: watermark/net/basic-usage/add-image
title: Add image watermarks
weight: 2
description: This article shows how to add an image watermark and save the resultant document. It is capable of adding watermarks to images or documents.
keywords: add image watermark, add image watermark to image, image watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
One of the main features of the GroupDocs.Watermark library is adding image watermarks to documents. You may add watermarks to documents or images from local disks, as well as from streams. For a full list of supported document formats, check [Supported formats]({{< ref "watermark/net/getting-started/supported-document-formats.md" >}}).

To add an image watermark perform the following steps:

1. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) an instance of the `Watermarker` class for a local file or file stream;
2. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/imagewatermark/constructors/1) an instance of the `ImageWatermark` class from the local image file;
3. (Optionally.) Specify the watermark [horizontal](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermark/properties/horizontalalignment) and [vertical](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermark/properties/verticalalignment) alignments;
4. Call the [Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/add) method to apply the watermark to the document;
5. Call the [Save](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/4) method to store the document in a new location.

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Common;
using GroupDocs.Watermark.Watermarks;

// Specify an absolute or relative path to your document.
using (Watermarker watermarker = new Watermarker("C:\\Docs\\contract.docx"))
{
    // Specify an absolute or relative path to the desired image
    ImageWatermark watermark = new ImageWatermark("C:\\Docs\\logo.png");
    // Specify watermark size, opacity and alignments
    watermark.Width = 200;
    watermark.Height = 200;
    watermark.Opacity = 0.5;
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    // Apply the watermark
    watermarker.Add(watermark);
    // Save the resulting document
    watermarker.Save("C:\\Docs\\img-watermarked-contract.docx");
}
```
Run the program. A new watermarked image will appear in the specified path.

![Adding image watermarks](/watermark/net/images/watermarking/add-image.png)

### What's next

GroupDocs.Watermark offers many more capabilities for adding image watermarks. To learn how to add watermarks from streams, use absolute or relative positioning, and so on, see the [Adding image watermarks]({{< ref "watermark/net/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks.md" >}}) article of the "Advanced usage" section.
