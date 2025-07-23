---
id: get-supported-file-formats
url: watermark/java/get-supported-file-formats
title: Get supported file formats
weight: 2
description: This article explains how to get the list of all supported file formats.
keywords: GroupDocs.Watermark,watermark
productName: GroupDocs.Watermark for Java
hideChildren: False
---
GroupDocs.Watermark allows to get the [list of all supported file formats]({{< ref "/watermark/java/getting-started/supported-document-formats.md" >}}) by following the below steps:

*   Call [getSupportedFileTypes](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/FileType#getSupportedFileTypes()) of [FileType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/FileType) class;
*   Enumerate through the collection of [FileType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/FileType) objects*.*

The following code sample demonstrates how to get a supported file formats list.

**basic\_usage.GetSupportedFileFormats**

```java
FileType[] fileTypes = FileType.getSupportedFileTypes();
for(FileType fileType : fileTypes) {                    
    System.out.println(fileType);                       
}                                                       
```
