---
id: working-with-slide-backgrounds
url: watermark/java/working-with-slide-backgrounds
title: Working with slide backgrounds
weight: 1
description: ""
keywords: 
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
## Extracting information about all slide backgrounds

The API allows you to extract information about all the slide backgrounds in a PowerPoint document as shown in the following code sample using method [getBackgroundImage()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationImageFillFormat#getBackgroundImage()) of [PresentationSlide](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationSlide).[getImageFillFormat()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationBaseSlide#getImageFillFormat()).

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationGetSlideBackgroundsInformation**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
PresentationContent content = watermarker.getContent(PresentationContent.class);                                   
for (PresentationSlide slide : content.getSlides())                                                                
{                                                                                                                  
    if (slide.getImageFillFormat().getBackgroundImage() != null)                                                   
    {                                                                                                              
        System.out.println(slide.getImageFillFormat().getBackgroundImage().getWidth());                            
        System.out.println(slide.getImageFillFormat().getBackgroundImage().getHeight());                           
        System.out.println(slide.getImageFillFormat().getBackgroundImage().getBytes().length);                     
    }                                                                                                              
}                                                                                                                  
                                                                                                                   
watermarker.close();                                                                                               
```

## Removing a particular background

Following code sample shows how to remove the background image of a particular slide calling the method [setBackgroundImage()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationImageFillFormat#setBackgroundImage(com.groupdocs.watermark.contents.PresentationWatermarkableImage)) with null.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationRemoveSlideBackground**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
PresentationContent content = watermarker.getContent(PresentationContent.class);                                   
content.getSlides().get_Item(0).getImageFillFormat().setBackgroundImage(null);                                     
                                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
```

## Adding watermark to all background Images

Using GroupDocs.Watermark, you can also [add](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WatermarkableImage#add(com.groupdocs.watermark.Watermark)) watermark to the background images that belong to a PowerPoint document as shown in the following code sample.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationAddWatermarkToSlideBackgroundImages**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
// Initialize image or text watermark                                                                              
TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));                              
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                                      
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                          
watermark.setRotateAngle(45);                                                                                      
watermark.setSizingType(SizingType.ScaleToParentDimensions);                                                       
watermark.setScaleFactor(1);                                                                                       
                                                                                                                   
PresentationContent content = watermarker.getContent(PresentationContent.class);                                   
for (PresentationSlide slide : content.getSlides())                                                                
{                                                                                                                  
    if (slide.getImageFillFormat().getBackgroundImage() != null)                                                   
    {                                                                                                              
        // Add watermark to the image                                                                              
        slide.getImageFillFormat().getBackgroundImage().add(watermark);                                            
    }                                                                                                              
}                                                                                                                  
                                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
```

## Additional settings for slide background image

GroupDocs.Watermark for Java also provides the feature that allows you to [tile](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationImageFillFormat#setTileAsTexture(boolean)) the picture across slide's background. You can also make the image [semi-transparent](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationImageFillFormat#setTransparency(double)). Following code sample serves this purpose.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationSetTiledSemitransparentBackground**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
PresentationContent content = watermarker.getContent(PresentationContent.class);                                   
PresentationSlide slide = content.getSlides().get_Item(0);                                                         
                                                                                                                   
File imageFile = new File("background.png");                                                                
byte[] imageBytes = new byte[(int) imageFile.length()];                                                            
InputStream imageInputStream = new FileInputStream(imageFile);                                                     
imageInputStream.read(imageBytes);                                                                                 
imageInputStream.close();                                                                                           
                                                                                                                   
slide.getImageFillFormat().setBackgroundImage(new PresentationWatermarkableImage(imageBytes));                     
slide.getImageFillFormat().setTileAsTexture(true);                                                                 
slide.getImageFillFormat().setTransparency(0.5);                                                                   
                                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
```

## Settings background image for charts

GroupDocs.Watermark for Java also allows you to set the background image for a chart inside PowerPoint document using [getCharts()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationBaseSlide#getCharts()) method. You can use following code sample to achieve this functionality.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationSetBackgroundImageForChart**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                                                             
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"                              
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                                                            
                                                                                                                                                 
PresentationContent content = watermarker.getContent(PresentationContent.class);                                                                 
                                                                                                                                                 
File imageFile = new File("test.png");                                                                                                    
byte[] imageBytes = new byte[(int) imageFile.length()];                                                                                          
InputStream imageInputStream = new FileInputStream(imageFile);                                                                                   
imageInputStream.read(imageBytes);                                                                                                               
imageInputStream.close();                                                                                                                         
                                                                                                                                                 
                                                                                                                                                 
content.getSlides().get_Item(0).getCharts().get_Item(0).getImageFillFormat().setBackgroundImage(new PresentationWatermarkableImage(imageBytes)); 
content.getSlides().get_Item(0).getCharts().get_Item(0).getImageFillFormat().setTransparency(0.5);                                               
content.getSlides().get_Item(0).getCharts().get_Item(0).getImageFillFormat().setTileAsTexture(true);                                             
                                                                                                                                                 
watermarker.save("presentation.pptx");                                                                                                 
                                                                                                                                                 
watermarker.close();                                                                                                                             
```
