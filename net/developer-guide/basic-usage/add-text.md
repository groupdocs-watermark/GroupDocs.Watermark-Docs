---
id: add-text
url: watermark/net/basic-usage/watermarking/add-text
title: Add text watermarks
weight: 1
description: This article shows how to add a text watermark and save the resultant document. It is capable of adding watermarks to images or documents.
keywords: add text watermark, add text watermark to image, text watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
One of the main features of the GroupDocs.Watermark library is adding text watermarks to documents. You may add watermarks to documents or images from local disks, as well as from streams. For a full list of supported document formats, check [Supported formats]({{< ref "watermark/net/getting-started/supported-document-formats.md" >}}).

To add a text watermark perform the following steps:

1. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) an instance of the `Watermarker` class for a local file or file stream;
2. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark/constructors/main) an instance of the `TextWatermark` class and specify the desired text and font for the watermark;
3. (Optionally.) Specify the watermark [color](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark/properties/foregroundcolor), [horizontal](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermark/properties/horizontalalignment) and [vertical](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermark/properties/verticalalignment) alignments;
4. Call the [Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/add) method to apply the watermark to the document;
5. Call the [Save](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/4) method to store the document in a new location.

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Common;
using GroupDocs.Watermark.Watermarks;

// Specify an absolute or relative path to your document.
using (Watermarker watermarker = new Watermarker("C:\\Docs\\contract.docx"))
{
    // Specify the desired text and font for the watermark
    TextWatermark watermark = new TextWatermark("Contract Draft", new Font("Arial", 60, FontStyle.Bold));
    // Specify font color and text opacity, rotation and alignments
    watermark.ForegroundColor = Color.Red;
    watermark.Opacity = 0.5;
    watermark.RotateAngle = -50;
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    // Apply the watermark
    watermarker.Add(watermark);
    // Save the resulting document
    watermarker.Save("C:\\Docs\\watermarked-contract.docx");
}
```
Run the program. A new watermarked document will appear in the specified path.

![Adding text watermarks](/watermark/net/images/watermarking/add-text.png)

### What's next

GroupDocs.Watermark offers many more capabilities for adding text watermarks. For example, it allows specifying background and foreground colors, formatting, text opacity, use of absolute or relative positioning, and so on. To learn more about this, see the [Adding text watermarks]({{< ref "watermark/net/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}}) article of the "Advanced usage" section.