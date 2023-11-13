---
id: get-document-info
url: watermark/java/get-document-info
title: Get document Info
weight: 1
description: This artcle explains how to get document information
keywords: GroupDocs.Watermark, watermark
productName: GroupDocs.Watermark for Java
hideChildren: False
---
GroupDocs.Watermark allows to get document information which includes:

*   [FileType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/IDocumentInfo#getFileType())
*   [PageCount](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/IDocumentInfo#getPageCount())
*   [FileSize](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/IDocumentInfo#getSize())
*   [IsEncrypted](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/IDocumentInfo#isEncrypted())

The following code samples demonstrate how to get document information.

## Get document information from a file from local disk

This example demostrates how to get document information from the local file.

**basic\_usage.GetDocumentInfoForTheFileFromLocalDisk**

```java
// Specify an absolute or relative path to your document. Ex.: "C:\\Docs\\source.docx"
Watermarker watermarker = new Watermarker("source.docx");                                      
IDocumentInfo info = watermarker.getDocumentInfo();                                                 
System.out.println("File type: " + info.getFileType());                                             
System.out.println("Number of pages: " + info.getPageCount());                                      
System.out.println("Document size: " + info.getSize() + " bytes");
watermarker.dispose();
```

## Get document information from a stream

This example demonstrates how to get document information from the file stream.

**basic\_usage.GetDocumentInfoForTheFileFromStream**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\source.docx"
FileInputStream stream = new FileInputStream("source.docx");                                  
Watermarker watermarker = new Watermarker(stream);                                                     
IDocumentInfo info = watermarker.getDocumentInfo();                                                    
System.out.println("File type: " + info.getFileType());                                                
System.out.println("Number of pages: " + info.getPageCount());                                         
System.out.println("Document size: " + info.getSize() + " bytes");
watermarker.dispose();
stream.close();
```
