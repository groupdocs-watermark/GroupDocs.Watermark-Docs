---
id: working-with-slide-backgrounds
url: watermark/net/working-with-slide-backgrounds
title: Working with slide backgrounds
weight: 1
description: "The API allows you to extract information about all the slide backgrounds, Removing a particular background and Adding watermark to all background images"
keywords: Adding watermark, Adding watermark to all background images
productName: GroupDocs.Watermark for .NET
hideChildren: True
---

The API allows you to extract information about all the slide backgrounds, Removing a particular background and Adding watermark to all background images

## Extracting information about all slide backgrounds

The API allows you to extract information about all the slide backgrounds in a PowerPoint document as shown in the following code sample using property [BackgroundImage](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.presentation/presentationimagefillformat/properties/backgroundimage) of [PresentationSlide.ImageFillFormat](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.presentation/presentationbaseslide/properties/imagefillformat).

**AdvancedUsage.AddingWatermarks.AddWatermarksToPresentations.PresentationGetSlideBackgroundsInformation**

```csharp
PresentationLoadOptions loadOptions = new PresentationLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\presentation.pptx"
using (Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions))
{
    PresentationContent content = watermarker.GetContent<PresentationContent>();
    foreach (PresentationSlide slide in content.Slides)
    {
        if (slide.ImageFillFormat.BackgroundImage != null)
        {
            Console.WriteLine(slide.ImageFillFormat.BackgroundImage.Width);
            Console.WriteLine(slide.ImageFillFormat.BackgroundImage.Height);
            Console.WriteLine(slide.ImageFillFormat.BackgroundImage.GetBytes().Length);
        }
    }
}
```

## Removing a particular background

Following code sample shows how to remove the background image of a particular slide setting the property [BackgroundImage](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.presentation/presentationimagefillformat/properties/backgroundimage) to null.

**AdvancedUsage.AddingWatermarks.<WBR>AddWatermarksToPresentations.<WBR>PresentationRemoveSlideBackground**

```csharp
PresentationLoadOptions loadOptions = new PresentationLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\presentation.pptx"
using (Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions))
{
    PresentationContent content = watermarker.GetContent<PresentationContent>();
    content.Slides[0].ImageFillFormat.BackgroundImage = null;

    watermarker.Save("presentation.pptx");
}
```

## Adding watermark to all background images

Using GroupDocs.Watermark, you can also [add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.image/watermarkableimage/methods/add) watermark to the background images that belong to a PowerPoint document as shown in the following code sample.

**AdvancedUsage.AddingWatermarks.<WBR>AddWatermarksToPresentations.<WBR>PresentationAddWatermarkToSlideBackgroundImages**

```csharp
PresentationLoadOptions loadOptions = new PresentationLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\presentation.pptx"
using (Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions))
{
    // Initialize image or text watermark
    TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    watermark.RotateAngle = 45;
    watermark.SizingType = SizingType.ScaleToParentDimensions;
    watermark.ScaleFactor = 1;

    PresentationContent content = watermarker.GetContent<PresentationContent>();
    foreach (PresentationSlide slide in content.Slides)
    {
        if (slide.ImageFillFormat.BackgroundImage != null)
        {
            // Add watermark to the image
            slide.ImageFillFormat.BackgroundImage.Add(watermark);
        }
    }

    watermarker.Save("presentation.pptx");
}
```

## Additional settings for slide background image

GroupDocs.Watermark for .NET also provides the feature that allows you to [tile](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.presentation/presentationimagefillformat/properties/tileastexture) the picture across slide's background. You can also make the image [semi-transparent](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.presentation/presentationimagefillformat/properties/transparency). Following code sample serves this purpose.

**AdvancedUsage.AddingWatermarks.<WBR>AddWatermarksToPresentations.<WBR>PresentationSetTiledSemitransparentBackground**

```csharp
PresentationLoadOptions loadOptions = new PresentationLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\presentation.pptx"
using (Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions))
{
    PresentationContent content = watermarker.GetContent<PresentationContent>();
    PresentationSlide slide = content.Slides[0];
    slide.ImageFillFormat.BackgroundImage = 
        new PresentationWatermarkableImage(File.ReadAllBytes("background.png"));
    slide.ImageFillFormat.TileAsTexture = true;
    slide.ImageFillFormat.Transparency = 0.5;

    watermarker.Save("presentation.pptx");
}
```

## Settings background image for charts

GroupDocs.Watermark for .NET also allows you to set the background image for a chart inside PowerPoint document using [Charts](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.presentation/presentationbaseslide/properties/charts) property. You can use following code sample to achieve this functionality.

**AdvancedUsage.AddingWatermarks.<WBR>AddWatermarksToPresentations.<WBR>PresentationSetBackgroundImageForChart**

```csharp
PresentationLoadOptions loadOptions = new PresentationLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\presentation.pptx"
using (Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions))
{
    PresentationContent content = watermarker.GetContent<PresentationContent>();
    content.Slides[0].Charts[0].ImageFillFormat.BackgroundImage = 
        new PresentationWatermarkableImage(File.ReadAllBytes("test.png"));
    content.Slides[0].Charts[0].ImageFillFormat.Transparency = 0.5;
    content.Slides[0].Charts[0].ImageFillFormat.TileAsTexture = true;

    watermarker.Save("presentation.pptx");
}
```

