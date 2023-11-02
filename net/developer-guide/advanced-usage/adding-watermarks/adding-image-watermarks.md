---
id: adding-image-watermarks
url: watermark/net/adding-image-watermarks
title: Adding image watermarks
linkTitle: Image watermarks
weight: 1
description: "GroupDocs.Watermark API supports adding the following image file types as image watermark"
keywords: image watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
GroupDocs.Watermark API supports adding the following image file types as image watermark:

* BMP;
* PNG;
* GIF;
* JPEG.

## Add image watermark from local file

The following code snippet shows how to add [ImageWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/imagewatermark) to a document. If the document consists of multiple parts (pages, worksheets, slides, frames, etc.), the watermark will be added to each of them.

**AdvancedUsage.AddingImageWatermarks.AddImageWatermark**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\presentation.pptx"
using (Watermarker watermarker = new Watermarker("presentation.pptx"))
{
    // Use path to the image as constructor parameter
    using (ImageWatermark watermark = new ImageWatermark("watermark.jpg"))
    {
        // Add watermark to the document
        watermarker.Add(watermark);

        watermarker.Save("presentation.pptx");
    }
}
```

## Add image watermark from stream  

You can also use a stream of the image to initialize [ImageWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/imagewatermark) instance as shown in below example.

**AdvancedUsage.AddingImageWatermarks.AddImageWatermarkUsingStream**

```csharp
// Specify an absolute or relative path to the watermark image. Ex: @"C:\Docs\watermark.jpg"
using (Stream watermarkStream = File.OpenRead("watermark.jpg"))
{
    using (Watermarker watermarker = new Watermarker("image.png"))
    {
        // Use stream containing an image as constructor parameter
        using (ImageWatermark watermark = new ImageWatermark(watermarkStream))
        {
            // Add watermark to the document
            watermarker.Add(watermark);

            watermarker.Save("image.png");
        }
    }
}
```

{{< alert style="warning" >}}
The [ImageWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/imagewatermark) class implements an [IDisposable](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable) interface. Therefore, it is necessary to call the [Dispose](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable.dispose) method when you are done working with the watermark. Alternatively, you can use the [using](https://docs.microsoft.com/en-us/dotnet/csharp/language-reference/keywords/using-statement) statement.
{{< /alert >}}

For the advanced use of image watermark properties please check the following article about text watermarks, however same techniques will work for image watermark as well:

* [Adding Text Watermarks]({{< ref "watermark/net/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}})

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Watermark for .NET examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-.NET)
* [GroupDocs.Watermark for Java examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java)

### Free online document watermarking App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to add watermark to PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Watermarking App](https://products.groupdocs.app/watermark).
