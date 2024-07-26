---
id: result-of-added-watermarks
url: watermark/net/result-of-added-watermarks
title: Result of added watermarks
linkTitle: Result of added watermarks
weight: 2
description: "GroupDocs.Watermark API returns result with information about added watermarks"
keywords:
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
GroupDocs.Watermark API provides the ability to add watermarks to document, where each added watermark being associated with a unique GUID (Globally Unique Identifier). This functionality not only enhances the security of the watermarked content, but also introduces a range of practical applications, like ability to trace the origin and distribution path of the watermarks, searching and removing specific watermark by id.

## Reviewing the result of added watermarks

The following code snippet shows how to review result [AddWatermarkResult](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks.results/addwatermarkresult/) with information about added watermarks in the document.


```csharp
using (Watermarker watermarker = new Watermarker("sample_2_pages.pdf"))
{
    // Initialize the font to be used for watermark
    Font font = new Font("Arial", 19, FontStyle.Bold | FontStyle.Italic);

    // Create the watermark object
    TextWatermark watermark = new TextWatermark("Test watermark", font);

    // Set watermark properties
    watermark.ForegroundColor = Color.Red;
    watermark.BackgroundColor = Color.Blue;
    watermark.TextAlignment = TextAlignment.Right;
    watermark.Opacity = 0.5;

    // Add watermark
    var result =  watermarker.Add(watermark);
    foreach(var item in  result.Succeeded) 
    {
        Console.WriteLine("WatermarkId: {0}", item.WatermarkId);
        Console.WriteLine("WatermarkType: {0}", item.WatermarkType);
        Console.WriteLine("PageNumber: {0}", item.PageNumber);
        Console.WriteLine("WatermarkPosition: {0}", item.WatermarkPosition);
    }

    watermarker.Save(outputFileName);
}

```

Output will be:

```csharp
WatermarkId: 1a78ef44-d497-451f-8f03-ca08ea537cc8
WatermarkType: Text
PageNumber: 1
WatermarkPosition: Default

WatermarkId: 658179cf-7b6e-472a-8b24-30f845dc2a9a
WatermarkType: Text
PageNumber: 2
WatermarkPosition: Default
```


