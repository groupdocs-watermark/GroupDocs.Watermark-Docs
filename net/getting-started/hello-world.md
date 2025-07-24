---
id: hello-world
url: watermark/net/hello-world
title: Hello, world!
weight: 8
description: Get started with GroupDocs.Watermark for .NET by creating and running a minimal example.
keywords: creating a text watermark, adding text watermark to document, C# 
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
In this article, you will learn how to create a simple C# application that appends a text watermark using the GroupDocs.Watermark API. 

{{% alert color="primary" %}} 
We assume that you already have a basic knowledge of **Microsoft Visual Studio** and **C#**.
{{% /alert %}}

## Requirements

- A [compatible]({{< ref "watermark/net/getting-started/system-requirements.md" >}}) system with Microsoft Visual Studio installed. As an individual developer, you can use a free Visual Studio Community Edition.
- **5 minutes** of your spare time.

## Preparing

1. Open Visual Studio and go to **File** -> **New** -> **Project**.
2. Select the **Console App** project type.
3. [Install]({{< ref "watermark/net/getting-started/installation.md" >}}) **GroupDocs.Watermark** NuGet package to the project.

## Coding

1. Create an instance of the `Watermarker` class for the local document. You can specify an absolute or relative path:
   ```csharp
   Watermarker watermarker = new Watermarker("C:\\Docs\\sample.docx")
   ```
2. Create an instance of the `TextWatermark` class and specify the desired text and font for the watermark:
   ```csharp
   TextWatermark watermark = new TextWatermark("Hello, world!", new Font("Arial", 36));
   ```
3. Apply the watermark:
   ```csharp
   watermarker.Add(watermark);
   ```
4. Save the resulting document:
   ```csharp
   watermarker.Save("C:\\Docs\\watermarked-sample.docx");
   ```

Full code:

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Watermarks;

// Specify an absolute or relative path to your document.
using (Watermarker watermarker = new Watermarker("C:\\Docs\\sample.docx"))
{
   // Specify the desired text and font for the watermark
   TextWatermark watermark = new TextWatermark("Test watermark", 
      new Font("Arial", 36, FontStyle.Bold | FontStyle.Italic));
      
   watermark.HorizontalAlignment = HorizontalAlignment.Center;
   watermark.VerticalAlignment = VerticalAlignment.Center;

   watermark.Opacity = 0.4;
   watermark.RotateAngle = 45;
   watermark.ForegroundColor = Color.Red;

    // Apply the watermark
    watermarker.Add(watermark);
    // Save the resulting document
    watermarker.Save("C:\\Docs\\watermarked-sample.docx");
}
```

Additionally, if you are certain about your file extension or know the document type in advance, you can specify the FileType through the LoadOptions class. Specifying it eliminates the need for format detection, enabling faster and more efficient document processing:

```csharp

var filePath = "C:\\Docs\\sample.docx";
var loadOptions = new LoadOptions()
{
    FileType = FileType.FromExtension(Path.GetExtension(filePath))
};

// Or set the FormatFamily property directly when using a stream, for example:
loadOptions.FormatFamily = FormatFamily.WordProcessing;

using (var watermarker = new Watermarker(filePath, loadOptions))
{ .... }

```

## Running

Run the program. A new watermarked document will appear in the specified path.

!["Hello, world!" example](/watermark/net/images/hello-world.png)

## What's next

Congratulations! You have added a simple text watermark to a document. Read the [Developer guide]({{< ref "watermark/net/developer-guide" >}}) and [API reference](https://reference.groupdocs.com/watermark/net/) to learn how to customize text watermarks, add images as watermarks, search documents for existing watermarks, and much more.
