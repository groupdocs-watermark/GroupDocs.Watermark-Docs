---
id: load-from-local-disk
url: watermark/net/load-from-local-disk
title: Load from local disk
linkTitle: From local disk
weight: 1
description: "This article explains how to load from local disk while using GroupDocs. Watermarks API."
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
The following example demonstrates how to create a [watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) for a local file system document:

**AdvancedUsage.LoadingDocuments.LoadFromLocalDisk**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.docx"
string filePath = "document.docx";
using (Watermarker watermarker = new Watermarker(filePath))
{
    // use watermarker methods to manage watermarks
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));
    watermarker.Add(watermark);
    watermarker.Save("document.docx");
}
```
