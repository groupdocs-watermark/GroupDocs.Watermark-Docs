---
id: get-document-info
url: watermark/net/get-document-info
title: Get document info
weight: 6
description: This article explains how to get document information
keywords: GroupDocs.Watermark, watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
GroupDocs.Watermark allows obtaining document information which includes:

* [FileType](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.common/idocumentinfo/properties/filetype)
* [PageCount](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.common/idocumentinfo/properties/pagecount)
* [Size](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.common/idocumentinfo/properties/size)
* [IsEncrypted](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.common/idocumentinfo/properties/isencrypted)

The following code samples demonstrate how to get document information.

## Get document information from a file from local disk

This example demonstrates how to get document information from the local file.

**BasicUsage.GetDocumentInfoForTheFileFromLocalDisk**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\source.docx"
using (Watermarker watermarker = new Watermarker("source.docx"))
{
    IDocumentInfo info = watermarker.GetDocumentInfo();
    Console.WriteLine("File type: {0}", info.FileType);
    Console.WriteLine("Number of pages: {0}", info.PageCount);
    Console.WriteLine("Document size: {0} bytes", info.Size);
}
```

## Get document information from a stream

This example demonstrates how to get document information from the file stream.

**BasicUsage.GetDocumentInfoForTheFileFromStream**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\source.docx"
using (FileStream stream = File.OpenRead("source.docx"))
{
    using (Watermarker watermarker = new Watermarker(stream))
    {
        IDocumentInfo info = watermarker.GetDocumentInfo();
        Console.WriteLine("File type: {0}", info.FileType);
        Console.WriteLine("Number of pages: {0}", info.PageCount);
        Console.WriteLine("Document size: {0} bytes", info.Size);
    }
}
```

## More resources

### Advanced usage topics

To learn more about document watermarking features and get familiar how to manage watermarks and more, please refer to the [advanced usage section]({{< ref "watermark/net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Watermark for .NET examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-.NET)
* [GroupDocs.Watermark for Java examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java)

### Free online document watermarking App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to add watermark to PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Watermarking App](https://products.groupdocs.app/watermark).
