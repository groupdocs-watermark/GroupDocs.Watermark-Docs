---
id: add-text-or-image-watermark
url: watermark/java/add-text-or-image-watermark
title: Add text or image watermark
weight: 3
description: This article shows how to add watermark and save resultant document. It is capable to add watermark to image or documents.
keywords: add watermark, add watermark to image
productName: GroupDocs.Watermark for Java
hideChildren: False
---
GroupDocs.Watermark allows adding watermarks and saving the resultant documents. The full list of supported document formats can be found [here]({{< ref "watermark/java/getting-started/supported-document-formats.md" >}}). You may add text and image watermarks to the documents from the local disk and from streams.

## Add a text watermark

The following example demonstrates how to add a [TextWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/TextWatermark) to a local document:

*   [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#Watermarker(java.lang.String)) a watermarker for the local file (line 2);
*   [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/TextWatermark#TextWatermark(java.lang.String,%20com.groupdocs.watermark.watermarks.Font)) a watermark with text and font (line 4);
*   Set the watermark [color](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/TextWatermark#setForegroundColor(com.groupdocs.watermark.watermarks.Color)), [horizontal](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermark#setHorizontalAlignment(int)) and [vertical](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermark#setVerticalAlignment(int)) alignments (lines 5-7);
*   [Add](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#add(com.groupdocs.watermark.Watermark)) the watermark to the document (line 9);
*   [Save](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#save(java.lang.String)) the document to the new file (line 10).
*   [Close](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#close()) the watermarker and free its resources (line 12).

**basic\_usage.AddATextWatermark**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
TextWatermark watermark = new TextWatermark("top secret", new Font("Arial", 36));                        
watermark.setForegroundColor(Color.getRed());                                                            
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                            
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                
                                                                                                         
watermarker.add(watermark);                                                                              
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                   
```

## Add an Image Watermark

The following example demonstrates how to add an [ImageWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark) to a document from a stream:

*   [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#Watermarker(java.lang.String)) a watermarker for the file stream (line 4);
*   [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark#ImageWatermark(java.lang.String)) an image watermark from the local image file (line 6);
*   Set the watermark [horizontal](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermark#setHorizontalAlignment(int)) and [vertical](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermark#setVerticalAlignment(int)) alignments (lines 7, 8);
*   [Add](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#add(com.groupdocs.watermark.Watermark)) the watermark to the document (line 9);
*   [Save](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#save(java.lang.String)) the document to the new file (line 11).
*   [Close](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark#close()) the watermark and free its resources (line 13);
*   [Close](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#close()) the watermarker and free its resources (line 14).

**basic\_usage.AddAnImageWatermark**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.xlsx" 
FileInputStream stream = new FileInputStream("document.xlsx");                                     
                                                                                                            
Watermarker watermarker = new Watermarker(stream);                                                          
                                                                                                            
ImageWatermark watermark = new ImageWatermark("logo.png");                                           
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                               
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                   
watermarker.add(watermark);                                                                                 
                                                                                                            
watermarker.save("document.xlsx");                                                                
                                                                                                            
watermark.close();                                                                                          
watermarker.close();                                                                                      
stream.close();                                                                                             
```
