---
id: save-document-to-the-specified-stream
url: watermark/net/save-document-to-the-specified-stream
title: Save document to the specified stream
weight: 3
description: "This article explains that how to save document to the specified stream while using GroupDocs. Watermarks API."
keywords: save document to the specified stream, save document 
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
Following code shows usage of [Save(Stream)](https://apireference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/2) method.

**AdvancedUsage.SavingDocuments.SaveDocumentToTheSpecifiedStream**

```csharp
// Constants.InTestDoc is an absolute or relative path to your document. Ex: @"C:\Docs\test.doc"
using (Watermarker watermarker = new Watermarker(Constants.InTestDoc))
{
    // watermarking goes here
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));
    watermarker.Add(watermark);

    // Saves the document to the specified stream
    watermarker.Save(stream);
}
```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Watermark for .NET examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-.NET)
* [GroupDocs.Watermark for Java examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java)

### Free online document watermarking App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to add watermark to PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Watermarking App](https://products.groupdocs.app/watermark).
