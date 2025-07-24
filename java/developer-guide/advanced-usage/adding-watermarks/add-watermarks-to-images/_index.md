---
id: add-watermarks-to-images
url: watermark/java/add-watermarks-to-images
title: Add watermarks to images
weight: 5
description: Add watermark to photos or multi-framed images using Java.
keywords: Add watermark to photos, Add watermarks to images, java
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
## Adding watermark to multi-framed image 

When you are working with an animated gif or multi-frame tiff images, you may want to add watermark to some particular frame(s) using the method [setFrameIndex()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/MultiframeImageWatermarkOptions#setFrameIndex(int)) of [TiffImageWatermarkOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/TiffImageWatermarkOptions) or [GifImageWatermarkOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/GifImageWatermarkOptions).

**advanced\_usage.add\_watermarks\_to\_images.AddWatermarkToImage**

```java
// Specify an absolute or relative path to your image. Ex: "C:\\Docs\\image.tiff"
TiffImageLoadOptions loadOptions = new TiffImageLoadOptions();                                       
Watermarker watermarker = new Watermarker("image.tiff", loadOptions);                       
                                                                                                     
// Initialize text or image watermark                                                                
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));                
                                                                                                     
// Add watermark to the first frame                                                                  
TiffImageWatermarkOptions options = new TiffImageWatermarkOptions();                                 
options.setFrameIndex(0);                                                                            
                                                                                                     
watermarker.add(watermark, options);                                                                 
watermarker.save("image.tiff");                                                            
                                                                                                     
watermarker.close();                                                                                 
```
