---
id: save-document-to-the-specified-location
url: watermark/java/save-document-to-the-specified-location
title: Save document to the specified location
weight: 1
description: "This article explains how to save document to the specified location while using GroupDocs. Watermarks Java API."
keywords: save document to the specified location, save document
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
Following code shows usage of [save(String)](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#save(java.lang.String)) method.

**advanced\_usage.saving\_documents.SaveDocumentToTheSpecifiedLocation**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\test.doc"
Watermarker watermarker = new Watermarker("test.doc");                                  
                                                                                                 
// watermarking goes here                                                                        
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));            
watermarker.add(watermark);                                                                      
                                                                                                 
// Saves the document to the specified location                                                  
watermarker.save("test.doc");                                                          
                                                                                                 
watermarker.close();                                                                             
```
