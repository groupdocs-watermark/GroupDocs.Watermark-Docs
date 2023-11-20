---
id: load-from-local-disk
url: watermark/java/load-from-local-disk
title: Load from local disk
weight: 1
description: "This article explains how to load from local disk while using GroupDocs. Watermarks Java API."
keywords: 
productName: GroupDocs.Watermark for Java
hideChildren: False
---
The folowing example demontrates how to create a [watermarker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker) for a local filesystem document:

**advanced\_usage.loading\_documents.LoadFromLocalDisk**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
String filePath = "document.docx";                                                                 
Watermarker watermarker = new Watermarker(filePath);                                                        
// use watermarker methods to manage watermarks                                                             
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));                       
                                                                                                            
watermarker.add(watermark);                                                                                 
watermarker.save("document.docx");                                                                
watermarker.close();                                                                                      
```

