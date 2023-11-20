---
id: save-document-to-the-same-file-or-stream
url: watermark/net/save-document-to-the-same-file-or-stream
title: Save document to the same file or stream
linkTitle: To the same file or stream
weight: 1
description: "This article explains how to save document to the same file or stream while using GroupDocs. Watermarks API."
keywords: save document, save document to the same file
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
Following code shows usage of [Save()](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/save) method.

**AdvancedUsage.SavingDocuments.SaveDocumentToTheSameFileOrStream**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\test.doc"
File.Copy("test-in.doc", "test-out.doc");
using (Watermarker watermarker = new Watermarker("test-out.doc"))
{
    // watermarking goes here
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));
    watermarker.Add(watermark);

    // Saves the document to the underlying source (stream or file)
    watermarker.Save();
}
```
