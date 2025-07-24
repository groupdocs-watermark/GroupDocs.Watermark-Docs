---
id: add-watermarks-to-images
url: watermark/net/add-watermarks-to-images
title: Add watermarks to images
linkTitle: To images
weight: 5
description: Add watermark to photos or multi-framed images using c#.
keywords: Add watermark to photos, Add watermarks to images
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
## Add watermark to photos or multi-framed images

When you are working with an animated GIF or multi-frame TIFF images, you may want to add watermark to some particular frame(s) using the property [FrameIndex](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.image/multiframeimagewatermarkoptions/properties/frameindex) of [TiffImageWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.image/tiffimagewatermarkoptions) or [GifImageWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.image/gifimagewatermarkoptions).

**AdvancedUsage.AddingWatermarks.AddWatermarksToImages.AddWatermarkToImage**

```csharp
TiffImageLoadOptions loadOptions = new TiffImageLoadOptions();
// Specify an absolute or relative path to your image. Ex: @"C:\Docs\image.tiff"
using (Watermarker watermarker = new Watermarker("image.tiff", loadOptions))
{
    // Initialize text or image watermark
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));

    // Add watermark to the first frame
    TiffImageWatermarkOptions options = new TiffImageWatermarkOptions();
    options.FrameIndex = 0;

    watermarker.Add(watermark, options);
    watermarker.Save("image.tiff");
}
```

## Advanced use cases

* [Adding watermark to images inside a document]({{< ref "adding-watermark-to-images-inside-a-document" >}} "Adding watermark to images inside a document")

