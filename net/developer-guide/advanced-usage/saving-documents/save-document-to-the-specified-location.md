---
id: save-document-to-the-specified-location
url: watermark/net/save-document-to-the-specified-location
title: Save document to the specified location
linkTitle: To the specified location
weight: 2
description: "This article explains how to save document to the specified location while using GroupDocs. Watermarks API."
keywords: save document to the specified location, save document
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
Following code shows usage of [Save(string)](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/4) method.

**AdvancedUsage.SavingDocuments.SaveDocumentToTheSpecifiedLocation**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\test.doc"
using (Watermarker watermarker = new Watermarker("test.doc"))
{
    // watermarking goes here
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));
    watermarker.Add(watermark);

    // Saves the document to the specified location
    watermarker.Save("test.doc");
}
```

