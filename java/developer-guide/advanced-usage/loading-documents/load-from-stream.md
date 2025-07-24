---
id: load-from-stream
url: watermark/java/load-from-stream
title: Load from stream
weight: 2
description: "This article explains how to load from stream while using GroupDocs. Watermarks Java API."
keywords: load from stream
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
The following example democtrates how to create a [watermarker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker) for a document stream:

**advanced\_usage.loading\_documents.LoadFromStream**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
FileInputStream document = new FileInputStream("document.docx");                                   
Watermarker watermarker = new Watermarker(document);                                                        
                                                                                                            
// use watermarker methods to manage watermarks                                                             
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));                       
                                                                                                            
watermarker.add(watermark);                                                                                 
                                                                                                            
watermarker.save("document.docx");                                                                
                                                                                                            
watermarker.close();                                                                                      
document.close();                                                                                           
```

