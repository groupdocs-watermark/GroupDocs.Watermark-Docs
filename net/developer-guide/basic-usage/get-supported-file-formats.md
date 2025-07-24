---
id: get-supported-file-formats
url: watermark/net/get-supported-file-formats
title: Get supported file formats
weight: 9
description: This article explains how to get the list of all supported file formats.
keywords: GroupDocs.Watermark,watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
GroupDocs.Watermark allows to get the [list of all supported file formats]({{< ref "watermark/net/getting-started/supported-document-formats.md" >}}) by following the below steps:

* Call the [GetSupportedFileTypes](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.common/filetype/methods/getsupportedfiletypes) method of the [FileType](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.common/filetype) class;
* Enumerate through the collection of [FileType](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.common/filetype) objects.

The following code sample demonstrates how to get a supported file formats list.

**BasicUsage.GetSupportedFileFormats**

```csharp
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes();
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType);
}
```
