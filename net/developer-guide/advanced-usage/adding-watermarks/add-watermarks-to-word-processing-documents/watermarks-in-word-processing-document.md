---
id: watermarks-in-word-processing-document
url: watermark/net/watermarks-in-word-processing-document
title: Watermarks in word processing document
weight: 4
description: "This article explains how to add watermarks in word processing document."
keywords: add watermarks, how to add watermarks
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
When adding watermark in Microsoft Word application, it places a shape with appropriate content in section headers. GroupDocs.Watermark API uses the same approach. When calling *[Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/add)* method of *[Watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker)* class, the shape is added to a document.

## Using properties of [WordProcessingWatermarkBaseOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.wordprocessing/wordprocessingwatermarkbaseoptions)

You can also set some additional options ([Name](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.wordprocessing/wordprocessingwatermarkbaseoptions/properties/name) or [AlternativeText](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.wordprocessing/wordprocessingwatermarkbaseoptions/properties/alternativetext)) when adding shape watermark to a Word document using GroupDocs.Watermark. Following code samples demonstrates it.

**AdvancedUsage.AddingWatermarks.AddWatermarksToWordProcessing.WordProcessingAddWatermarkWithShapeSettings**

```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.docx"
using (Watermarker watermarker = new Watermarker("document.docx", loadOptions))
{
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));

    //Some settings for watermark
    watermark.VerticalAlignment = VerticalAlignment.Center;
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.RotateAngle = 25.0;
    watermark.ForegroundColor = Color.Red;
    watermark.Opacity = 1.0;

    WordProcessingWatermarkSectionOptions options = new WordProcessingWatermarkSectionOptions();

    // Set the shape name
    options.Name = "Shape 1";

    // Set the descriptive (alternative) text that will be associated with the shape
    options.AlternativeText = "Test watermark";

    watermarker.Add(watermark, options);
    watermarker.Save("document.docx");
}
```

## Using [WordProcessingTextEffects](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.wordprocessing/wordprocessingtexteffects)

You can also apply some text effects to the shape watermarks as shown in the below code.

**AdvancedUsage.AddingWatermarks.AddWatermarksToWordProcessing.WordProcessingAddWatermarkWithTextEffects**

```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.docx"
using (Watermarker watermarker = new Watermarker("document.docx", loadOptions))
{
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));

    WordProcessingTextEffects effects = new WordProcessingTextEffects();
    effects.LineFormat.Enabled = true;
    effects.LineFormat.Color = Color.Red;
    effects.LineFormat.DashStyle = OfficeDashStyle.DashDotDot;
    effects.LineFormat.LineStyle = OfficeLineStyle.Triple;
    effects.LineFormat.Weight = 1;

    WordProcessingWatermarkSectionOptions options = new WordProcessingWatermarkSectionOptions();
    options.Effects = effects;

    watermarker.Add(watermark, options);
    watermarker.Save("document.docx");
}
```

## Using [WordProcessingImageEffects](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.wordprocessing/wordprocessingimageeffects)

GroupDocs.Watermark also provides the facility to apply image effects to the shape watermarks.

**AdvancedUsage.AddingWatermarks.AddWatermarksToWordProcessing.WordProcessingAddWatermarkWithImageEffects**

```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.docx"
using (Watermarker watermarker = new Watermarker("document.docx", loadOptions))
{
    using (ImageWatermark watermark = new ImageWatermark("logo.png"))
    {
        WordProcessingImageEffects effects = new WordProcessingImageEffects();
        effects.Brightness = 0.7;
        effects.Contrast = 0.6;
        effects.ChromaKey = Color.Red;
        effects.BorderLineFormat.Enabled = true;
        effects.BorderLineFormat.Weight = 1;

        WordProcessingWatermarkSectionOptions options = new WordProcessingWatermarkSectionOptions();
        options.Effects = effects;

        watermarker.Add(watermark, options);
    }

    watermarker.Save("document.docx");
}
```
