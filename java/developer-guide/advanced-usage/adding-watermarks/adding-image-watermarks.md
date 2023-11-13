---
id: adding-image-watermarks
url: watermark/java/adding-image-watermarks
title: Adding image watermarks
weight: 2
description: ""
keywords: 
productName: GroupDocs.Watermark for Java
hideChildren: False
---
GroupDocs.Watermar API supports adding the following image file types as image watermark:

*   Bmp;
*   Png;
*   Gif;
*   Jpeg.

## Add image watermark from local file

Following code snippet shows how to add [ImageWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark) to a document. If the document consists of multiple parts (pages, worksheets, slides, frames etc), the watermark will be added to all of them.

**advanced\_usage.adding\_image\_watermarks.AddImageWatermark**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx");                                           
                                                                                                                   
// Use path to the image as constructor parameter                                                                  
ImageWatermark watermark = new ImageWatermark("watermark.jpg");                                             
                                                                                                                   
// Add watermark to the document                                                                                   
watermarker.add(watermark);                                                                                        
                                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermark.close();                                                                                                 
watermarker.close();                                                                                             
```

## Add image watermark from stream  

You can also use a stream of the image to initialize [ ImageWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark) instance as shown in below example.

**advanced\_usage.adding\_image\_watermarks.AddImageWatermarkUsingStream**

```java
// Specify an absolute or relative path to the watermark image. Ex: "C:\\Docs\\watermark.jpg"
FileInputStream watermarkStream = new FileInputStream("watermark.jpg");                           
                                                                                                         
Watermarker watermarker = new Watermarker("image.png");                                         
                                                                                                         
// Use stream containing an image as constructor parameter                                               
ImageWatermark watermark = new ImageWatermark(watermarkStream);                                          
                                                                                                         
// Add watermark to the document                                                                         
watermarker.add(watermark);                                                                              
                                                                                                         
watermarker.save("image.png");                                                                 
                                                                                                         
watermark.close();                                                                                       
watermarker.dispose();                                                                                   
watermarkStream.close();                                                                                 
```

{{< alert style="warning" >}}
[ImageWatermark ](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark) class implements [Closable](https://docs.oracle.com/javase/7/docs/api/java/io/Closeable.html) interface. Therefore, it is necessary to call [close()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark#close()) method when you are done working with the watermark. 
{{< /alert >}}

For the advanced use of image watermark properties please check the following article about text watermarks, however, the same techniques will work for image watermarks as well:
*   [Adding Text Watermarks]({{< ref "watermark/java/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}})
