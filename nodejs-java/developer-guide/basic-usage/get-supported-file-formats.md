---
id: get-supported-document-formats
url: watermark/nodejs-java/get-supported-document-formats
title: Get supported file formats
weight: 1
description: "This article explains how to obtain supported file formats list when viewing documents with GroupDocs.Watermark within your Java applications."
keywords: Get file info, Get File Type, Page count, File size
productName: GroupDocs.Watermark for Node.js via Java
hideChildren: False
toc: True
structuredData:
  showOrganization: True
  application:
    name: Document Watermark
    description: Compare documents natively with high performance using JavaScript language and GroupDocs.Watermark for Node.js via Java
    productCode: watermark
    productPlatform: nodejs-java
  showVideo: True
  howTo:
    name: Get file formats supported by Watermark in JavaScriptScript
    description: Get file formats supported by Watermark Java step by step
    steps:
      - name: Get an array of supported file types
        text: Call the GetSupportedFileTypes method of the FileType object. Additionally, the OrderBy method can sort the resulting array, using lambda expression as the parameter. The result is a collection of a FileType data type, with the possibility of iteration.
      - name: Output the supported file types
        text: Iterate through the collection, to output the supported data types, for example, to the console.
---

[GroupDocs.Watermark](https://products.groupdocs.com/watermark/nodejs-java) allows you to get the list of all [supported file formats]({{< ref "watermark/nodejs-java/getting-started/supported-document-formats.md" >}}). To do this, follow these steps:

1. Call the `getSupportedFileTypes`<!--](https://reference.groupdocs.com/watermark/nodejs-java/com.groupdocs.watermark.result/filetype/#getSupportedFileTypes- -)--> method of the `FileType`<!--](https://reference.groupdocs.com/watermark/nodejs-java/com.groupdocs.watermark.result/filetype/)--> class.
2. Enumerate through the collection of the `FileType`<!--](https://reference.groupdocs.com/watermark/nodejs-java/com.groupdocs.watermark.result/filetype/)--> objects.

The following code snippet shows how to obtain a list of supported file formats:


```javascript
const supportedFileTypes = groupdocs.watermark.FileType.getSupportedFileTypes();
supportedFileTypes.forEach(fileType => {
  console.log(fileType.toString());
});
```