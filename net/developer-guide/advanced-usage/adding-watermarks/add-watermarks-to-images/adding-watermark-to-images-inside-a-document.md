---
id: adding-watermark-to-images-inside-a-document
url: watermark/net/adding-watermark-to-images-inside-a-document
title: Adding watermark to images inside a document
linkTitle: To images inside a document
weight: 1
description: This article will help, if you want to add watermark to images inside a document then it can be possible using GroupDocs.Watermark.
keywords: Adding watermark, add watermark to images
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
The most of the document formats allow you to place images inside a document. If you want to add watermark to images inside a document then it can be possible using GroupDocs.Watermark. Following are the steps to add watermark to the images of any document.

1. Load the document
2. Create and initialize watermark object
3. Set watermark properties
4. [Find](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/getimages) images in the document
5. [Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.image/watermarkableimage/methods/add) watermark to all found images
6. Save the document

**AdvancedUsage.AddingWatermarks.AddWatermarksToImages.AddWatermarkToImagesInsideDocument**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    // Initialize text watermark
    TextWatermark textWatermark = new TextWatermark("Protected image", new Font("Arial", 8));
    textWatermark.HorizontalAlignment = HorizontalAlignment.Center;
    textWatermark.VerticalAlignment = VerticalAlignment.Center;
    textWatermark.RotateAngle = 45;
    textWatermark.SizingType = SizingType.ScaleToParentDimensions;
    textWatermark.ScaleFactor = 1;

    // Initialize image watermark
    using (ImageWatermark imageWatermark = new ImageWatermark("protect.jpg"))
    {
        imageWatermark.HorizontalAlignment = HorizontalAlignment.Center;
        imageWatermark.VerticalAlignment = VerticalAlignment.Center;
        imageWatermark.RotateAngle = -45;
        imageWatermark.SizingType = SizingType.ScaleToParentDimensions;
        imageWatermark.ScaleFactor = 1;

        // Find all images in a document
        WatermarkableImageCollection images = watermarker.GetImages();
        for (int i = 0; i < images.Count; i++)
        {
            if (images[i].Width > 100 && images[i].Height > 100)
            {
                if (i % 2 == 0)
                {
                    images[i].Add(textWatermark);
                }
                else
                {
                    images[i].Add(imageWatermark);
                }
            }
        }
    }

    watermarker.Save("document.pdf");
}
```
