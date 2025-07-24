---
id: modifing-found-watermark-properties
url: watermark/net/modifing-found-watermark-properties
title: Modifying found watermark properties
weight: 2
description: "This article explains how to modify found watermark properties while using GroupDocs. Watermarks API."
keywords: modify found watermark properties
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
GroupDocs.Watermark also allows you to replace text and image in the found possible watermarks. Following sections will show you how to replace text and image of a found watermark.

## Replacing text

To replace text of the found watermarks, loop through the possible watermarks in the [watermark collection](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search/possiblewatermarkcollection) and replace [Text](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search/possiblewatermark/properties/text) property as shown in the following code sample.

**AdvancedUsage.SearchAndRemoveWatermarks.EditTextInFoundWatermarks**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    TextSearchCriteria searchCriteria = new TextSearchCriteria("test", false);
    PossibleWatermarkCollection watermarks = watermarker.Search(searchCriteria);
    foreach (PossibleWatermark watermark in watermarks)
    {
        try
        {
            // Edit text
            watermark.Text = "passed";
        }
        catch (Exception e)
        {
            // Found entity may not support text editing
            // Passed argument can have inappropriate value
            // Process such cases here
        }
    }

    // Save document
    watermarker.Save("document.pdf");
}
```

## Replacing text with formatting

You can also replace the watermark's text with [formatting](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search/possiblewatermark/properties/formattedtextfragments) as shown in the below code sample.

**AdvancedUsage.SearchAndRemoveWatermarks.EditTextWithFormattingInFoundWatermarks**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    TextSearchCriteria searchCriteria = new TextSearchCriteria("test", false);
    PossibleWatermarkCollection watermarks = watermarker.Search(searchCriteria);
    foreach (PossibleWatermark watermark in watermarks)
    {
        try
        {
            // Edit text
            watermark.FormattedTextFragments.Clear();
            watermark.FormattedTextFragments.Add("passed", new Font("Calibri", 19, FontStyle.Bold), Color.Red, Color.Aqua);
        }
        catch (Exception e)
        {
            // Found entity may not support text editing
            // Passed arguments can have inappropriate value
            // Process such cases here
        }
    }

    // Save document
    watermarker.Save("document.pdf");
}
```

## Replacing image

Following code sample shows how to replace the [image](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search/possiblewatermark/properties/imagedata) of the found watermarks using GroupDocs.Watermark.

**AdvancedUsage.SearchAndRemoveWatermarks.ReplacesImageInFoundWatermarks**

```csharp
byte[] imageData = File.ReadAllBytes("image.png");

// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    // Search watermark matching a particular image
    SearchCriteria searchCriteria = new ImageDctHashSearchCriteria("logo.bmp");
    PossibleWatermarkCollection watermarks = watermarker.Search(searchCriteria);
    foreach (PossibleWatermark watermark in watermarks)
    {
        try
        {
            // Replace image
            watermark.ImageData = imageData;
        }
        catch (Exception e)
        {
            // Found entity may not support image replacment
            // Passed image can have inappropriate format
            // Process such cases here
        }
    }

    // Save document
    watermarker.Save("document.pdf");
}
```

