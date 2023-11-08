---
id: rotate
url: watermark/net/basic-usage/watermarking/rotate
title: Rotate watermarks
weight: 3
description: This article shows how to rotate text or image watermarks.
keywords: rotate text watermark, rotate image watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
When adding watermarks, their orientation is not limited to horizontal only. You can specify whichever rotation angle you want. 

To rotate text or image watermark, set the desired angle using the [Watermark.RotateAngle](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/rotateangle/) property:

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Watermarks;

// Specify an absolute or relative path to your document.
using (Watermarker watermarker = new Watermarker("C:\\Docs\\sample.docx"))
{
    // Specify the desired text and font for the watermark
    TextWatermark watermark = new TextWatermark("Top secret", new Font("Courier New", 14));
    // Specify font color
    watermark.ForegroundColor = Color.Red;    
    // Set rotation angle
    watermark.RotateAngle = 35;
    // Apply the watermark
    watermarker.Add(watermark);
    // Save the resulting document
    watermarker.Save("C:\\Docs\\watermarked-sample.docx");
}
```
Run the program. A watermark will be added at a specified angle.

![Rotating watermarks](/watermark/net/images/watermarking/angled-watermark.png)

### What's next

GroupDocs.Watermark offers many more capabilities for adding text watermarks. For example, it allows specifying background and foreground colors, formatting, text opacity, use of absolute or relative positioning, and so on. To learn more about this, see the [Adding text watermarks]({{< ref "watermark/net/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}}) article of the "Advanced usage" section.