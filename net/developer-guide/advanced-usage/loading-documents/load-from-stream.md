---
id: load-from-stream
url: watermark/net/load-from-stream
title: Load from stream
linkTitle: From stream
weight: 2
description: "This article explains how to load from stream while using GroupDocs. Watermarks API."
keywords: load from stream
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
The following example demonstrates how to create a [watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/main) for a document stream:

**AdvancedUsage.LoadingDocuments.LoadFromStream**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.docx"
using (Stream document = File.OpenRead("document.docx"))
using (Watermarker watermarker = new Watermarker(document))
{
    // use watermarker methods to manage watermarks
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));
    watermarker.Add(watermark);
    watermarker.Save("document.docx");
}
```

