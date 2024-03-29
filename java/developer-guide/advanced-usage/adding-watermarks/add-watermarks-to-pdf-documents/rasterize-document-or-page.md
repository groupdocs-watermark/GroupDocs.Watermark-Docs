---
id: rasterize-document-or-page
url: watermark/java/rasterize-document-or-page
title: Rasterize document or page
weight: 2
description:  The watermark can be removed from the PDF documents using third-party tools. However, if you want to remove a watermark that is almost impossible to remove, you can rasterize pdf documents. GroupDocs.Watermark provides the feature to convert all the pages of a PDF document to raster images with only one line of code.
keywords: remove a watermark, watermark, rasterize pdf
productName: GroupDocs.Watermark for Java
hideChildren: False
---
## How to remove a watermark from a pdf 
The watermark can be removed from the PDF documents using third-party tools. However, if you want to get a watermark that is almost impossible to remove, you can consider PDF document rasterization. GroupDocs.Watermark provides the feature to convert all the pages of a PDF document to raster images with only one line of code.

## Rasterize PDF document

Following code snippet is used to [rasterize](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfContent#rasterize(int,%20int,%20int)) the PDF document to protect added watermarks.  

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRasterizeDocument**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
// Initialize image or text watermark                                                                    
TextWatermark watermark = new TextWatermark("Do not copy", new Font("Arial", 8));                        
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                            
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                
watermark.setRotateAngle(45);                                                                            
watermark.setSizingType(SizingType.ScaleToParentDimensions);                                             
watermark.setScaleFactor(1);                                                                             
watermark.setOpacity(0.5);                                                                               
                                                                                                         
// Add watermark of any type first                                                                       
watermarker.add(watermark);                                                                              
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
                                                                                                         
// Rasterize all pages                                                                                   
pdfContent.rasterize(100, 100, PdfImageConversionFormat.Png);                                            
                                                                                                         
// Content of all pages is replaced with raster images                                                   
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

{{< alert style="warning" >}}You can't restore document content after saving the document. Rasterization significantly increases the size of the resultant PDF file.{{< /alert >}}

## Rasterize particular page of the PDF document

The API also allows you to [rasterize](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfPage#rasterize(int,%20int,%20int)) any particular page of the PDF document. Following code snippet is used to rasterize a page of the PDF document.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRasterizePage**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
// Initialize image or text watermark                                                                    
TextWatermark watermark = new TextWatermark("Do not copy", new Font("Arial", 8));                        
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                            
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                
watermark.setRotateAngle(45);                                                                            
watermark.setSizingType(SizingType.ScaleToParentDimensions);                                             
watermark.setScaleFactor(1);                                                                             
watermark.setOpacity(0.5);                                                                               
                                                                                                         
// Add watermark of any type first                                                                       
PdfArtifactWatermarkOptions options = new PdfArtifactWatermarkOptions();                                 
options.setPageIndex(0);                                                                                 
watermarker.add(watermark, options);                                                                     
                                                                                                         
// Rasterize the first page                                                                              
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
pdfContent.getPages().get_Item(0).rasterize(100, 100, PdfImageConversionFormat.Png);                     
                                                                                                         
// Content of the first page is replaced with raster image                                               
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```
