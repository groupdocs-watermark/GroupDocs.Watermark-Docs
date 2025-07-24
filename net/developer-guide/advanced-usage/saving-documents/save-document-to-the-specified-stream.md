---
id: save-document-to-the-specified-stream
url: watermark/net/save-document-to-the-specified-stream
title: Save document to the specified stream
linkTitle: To the specified stream
weight: 3
description: "This article explains how to save document to the specified stream while using GroupDocs. Watermarks API."
keywords: save document to the specified stream, save document 
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
Following code shows usage of [Save(Stream)](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/2) method.

**AdvancedUsage.SavingDocuments.SaveDocumentToTheSpecifiedStream**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\test.doc"
using (Watermarker watermarker = new Watermarker("test.doc"))
{
    // watermarking goes here
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));
    watermarker.Add(watermark);

    // Saves the document to the specified stream
    watermarker.Save(stream);
}
```
