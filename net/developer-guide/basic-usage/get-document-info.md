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

