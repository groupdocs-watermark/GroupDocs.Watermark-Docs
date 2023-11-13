---
id: save-document-to-the-specified-stream
url: watermark/java/save-document-to-the-specified-stream
title: Save document to the specified stream
weight: 2
description: "This article explains how to save document to the specified stream while using GroupDocs.Watermarks Java API."
keywords: save document to the specified stream, save document 
productName: GroupDocs.Watermark for Java
hideChildren: False
---
Following code shows usage of [save(OutputStream)](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#save(java.io.OutputStream)) method.

**advanced\_usage.saving\_documents.SaveDocumentToTheSpecifiedStream**

```java
ByteArrayOutputStream outputStream = new ByteArrayOutputStream();                                
                                                                                                 
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\test.doc"
Watermarker watermarker = new Watermarker("test.doc");                                  
                                                                                                 
// watermarking goes here                                                                        
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));            
watermarker.add(watermark);                                                                      
                                                                                                 
// Saves the document to the specified stream                                                    
watermarker.save(outputStream);                                                                  
                                                                                                 
watermarker.close();                                                                             
outputStream.close();                                                                            
```

