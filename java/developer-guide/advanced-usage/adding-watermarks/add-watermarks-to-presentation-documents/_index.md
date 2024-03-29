---
id: add-watermarks-to-presentation-documents
url: watermark/java/add-watermarks-to-presentation-documents
title: Add watermarks to presentation documents
weight: 7
description: ""
keywords: 
productName: GroupDocs.Watermark for Java
hideChildren: False
---
## Adding watermark to a particular slide

Using GroupDocs.Watermark, you can add watermark to a particular slide of a PowerPoint presentation in a simplified way. Adding watermark to a particular PowerPoint slide using GroupDocs.Watermark consists of following steps.

1.  Load the document
2.  Create and initialize watermark object
3.  Set watermark properties
4.  Call [setSlideIndex()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationWatermarkSlideOptions#setSlideIndex(int)) of [PresentationWatermarkSlideOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationWatermarkSlideOptions)
5.  Add watermark to the document
6.  Save the document

Following code shows how to add [TextWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/TextWatermark) to the first slide and [ImageWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark) to the second slide.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationAddWatermarkToSlide**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
// Add text watermark to the first slide                                                                           
TextWatermark textWatermark = new TextWatermark("Test watermark", new Font("Arial", 8));                           
PresentationWatermarkSlideOptions textWatermarkOptions = new PresentationWatermarkSlideOptions();                  
textWatermarkOptions.setSlideIndex(0);                                                                             
watermarker.add(textWatermark, textWatermarkOptions);                                                              
                                                                                                                   
// Add image watermark to the second slide                                                                         
ImageWatermark imageWatermark = new ImageWatermark("logo.jpg");                                             
                                                                                                                   
PresentationWatermarkSlideOptions imageWatermarkOptions = new PresentationWatermarkSlideOptions();                 
imageWatermarkOptions.setSlideIndex(1);                                                                            
watermarker.add(imageWatermark, imageWatermarkOptions);                                                            
                                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
imageWatermark.close();                                                                                            
```

## Protecting watermark using unreadable characters

This feature allows strengthening the protection of text watermark. Using unreadable characters in the watermark text forbids the modification using Find and Replace dialog. The following code sample shows how to include unreadable characters in watermark text using methods [setLocked()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationWatermarkBaseSlideOptions#setLocked(boolean)) and [setProtectWithUnreadableCharacters()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationWatermarkBaseSlideOptions#setProtectWithUnreadableCharacters(boolean)) of [PresentationWatermarkSlideOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationWatermarkSlideOptions).

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationProtectWatermarkUsingUnreadableCharacters**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
TextWatermark watermark = new TextWatermark("Watermark text", new Font("Arial", 19));                              
                                                                                                                   
PresentationWatermarkSlideOptions options = new PresentationWatermarkSlideOptions();                               
options.setLocked(true);                                                                                           
options.setProtectWithUnreadableCharacters(true);                                                                  
                                                                                                                   
// Add watermark                                                                                                   
watermarker.add(watermark, options);                                                                               
                                                                                                                   
// Save document                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
```

## Getting slide dimensions

If for some reasons you want to use absolute sizing and positioning, you may also need to get the [width](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationContent#getSlideWidth()) and [height](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationContent#getSlideHeight()) of the slide. Use below code to get the dimensions of a particular slide.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationGetSlideDimensions**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
PresentationContent content = watermarker.getContent(PresentationContent.class);                                   
                                                                                                                   
System.out.println(content.getSlideWidth());                                                                       
System.out.println(content.getSlideHeight());                                                                      
                                                                                                                   
watermarker.close();                                                                                               
```

## Add watermark to all images inside a particular slide

GroupDocs.Watermark allows you to add watermark to the images inside a particular PowerPoint slide using [add()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WatermarkableImage#add(com.groupdocs.watermark.Watermark)) method as shown in below example.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationAddWatermarkToSlideImages**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));                              
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                                      
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                          
watermark.setRotateAngle(45);                                                                                      
watermark.setSizingType(SizingType.ScaleToParentDimensions);                                                       
watermark.setScaleFactor(1);                                                                                       
                                                                                                                   
// Get all images from the first slide                                                                             
PresentationContent content = watermarker.getContent(PresentationContent.class);                                   
WatermarkableImageCollection images = content.getSlides().get_Item(0).findImages();                                
                                                                                                                   
// Add watermark to all found images                                                                               
for (WatermarkableImage image : images)                                                                            
{                                                                                                                  
    image.add(watermark);                                                                                          
}                                                                                                                  
                                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
```

## Working with masters, layouts, and notes

GroupDocs.Watermark enables you to access all types of the service slides in a PowerPoint presentation. Following methods of [PresentationContent](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationContent) allows access to the coresponding slide types using the API

*   [getMasterSlides()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationContent#getMasterSlides())
*   [getLayoutSlides()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationContent#getLayoutSlides())
*   [getMasterHandoutSlide()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationContent#getMasterHandoutSlide())
*   [getMasterNotesSlide()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationContent#getMasterNotesSlide())
*   [getNotesSlide()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationSlide#getNotesSlide()) (the method of [PresentationSlide](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PresentationSlide))

Following code shows how to access each type of the slides in a PowerPoint presentation.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationAddWatermarkToAllSlideTypes**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                                          
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"           
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                                         
                                                                                                                              
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 8));                                          
                                                                                                                              
PresentationContent content = watermarker.getContent(PresentationContent.class);                                              
                                                                                                                              
// Add watermark to all master slides                                                                                         
PresentationWatermarkMasterSlideOptions masterSlideOptions = new PresentationWatermarkMasterSlideOptions();                   
masterSlideOptions.setMasterSlideIndex(-1);                                                                                   
watermarker.add(watermark, masterSlideOptions);                                                                               
                                                                                                                              
// Add watermark to all layout slides                                                                                         
if (content.getLayoutSlides() != null)                                                                                        
{                                                                                                                             
    PresentationWatermarkLayoutSlideOptions layoutSlideOptions = new PresentationWatermarkLayoutSlideOptions();               
    layoutSlideOptions.setLayoutSlideIndex(-1);                                                                               
    watermarker.add(watermark, masterSlideOptions);                                                                           
}                                                                                                                             
                                                                                                                              
// Add watermark to all notes slides                                                                                          
for (int i = 0; i < content.getSlides().getCount(); i++)                                                                      
{                                                                                                                             
    if (content.getSlides().get_Item(i).getNotesSlide() != null)                                                              
    {                                                                                                                         
        PresentationWatermarkNoteSlideOptions noteSlideOptions = new PresentationWatermarkNoteSlideOptions();                 
        noteSlideOptions.setSlideIndex(i);                                                                                    
        watermarker.add(watermark, noteSlideOptions);                                                                         
    }                                                                                                                         
}                                                                                                                             
                                                                                                                              
// Add watermark to handout master                                                                                            
if (content.getMasterHandoutSlide() != null)                                                                                  
{                                                                                                                             
    PresentationWatermarkMasterHandoutSlideOptions handoutSlideOptions = new PresentationWatermarkMasterHandoutSlideOptions();
    watermarker.add(watermark, handoutSlideOptions);                                                                          
}                                                                                                                             
                                                                                                                              
// Add watermark to notes master                                                                                              
if (content.getMasterNotesSlide() != null)                                                                                    
{                                                                                                                             
    PresentationWatermarkMasterNotesSlideOptions masterNotesSlideOptions = new PresentationWatermarkMasterNotesSlideOptions();
    watermarker.add(watermark, masterNotesSlideOptions);                                                                      
}                                                                                                                             
                                                                                                                              
watermarker.save("presentation.pptx");                                                                              
                                                                                                                              
watermarker.close();                                                                                                          
```

## What is watermark in PowerPoint

When you're calling [add()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#add(com.groupdocs.watermark.Watermark)) method of [Watermarker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker) class with loaded presentation document, simple shape is added to a PowerPoint document. GroupDocs.Watermark provides some additional options when adding a shape watermark. Use [PresentationWatermarkBaseSlideOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationWatermarkBaseSlideOptions) descendant classes to set these options as shown in below example.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationAddWatermarkWithSlidesShapeSettings**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));                              
watermark.setBackground(true);                                                                                     
                                                                                                                   
PresentationWatermarkSlideOptions options = new PresentationWatermarkSlideOptions();                               
                                                                                                                   
// Set the shape name                                                                                              
options.setName("Shape 1");                                                                                        
                                                                                                                   
// Set the descriptive (alternative) text that will be associated with the shape                                   
options.setAlternativeText("Test watermark");                                                                      
                                                                                                                   
// Editing of the shape in PowerPoint is forbidden                                                                 
options.setLocked(true);                                                                                           
                                                                                                                   
watermarker.add(watermark, options);                                                                               
                                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
```

### Applying text effects 

You can also apply [text effects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationTextEffects) when adding shape watermark to a PowerPoint slide.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationAddWatermarkWithTextEffects**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Segoe UI", 19));                           
                                                                                                                   
PresentationTextEffects effects = new PresentationTextEffects();                                                   
effects.getLineFormat().setEnabled(true);                                                                          
effects.getLineFormat().setColor(Color.getRed());                                                                  
effects.getLineFormat().setDashStyle(OfficeDashStyle.DashDotDot);                                                  
effects.getLineFormat().setLineStyle(OfficeLineStyle.Triple);                                                      
effects.getLineFormat().setWeight(1);                                                                              
                                                                                                                   
PresentationWatermarkSlideOptions options = new PresentationWatermarkSlideOptions();                               
options.setEffects(effects);                                                                                       
                                                                                                                   
watermarker.add(watermark, options);                                                                               
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
```

{{< alert style="warning" >}}Line format settings are not supported for Ppt presentations at this moment.{{< /alert >}}

### Applying image effects 

The API also allows you to apply [image effects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationImageEffects) to the shape watermark using below code.

**advanced\_usage.add\_watermarks\_to\_presentations.PresentationAddWatermarkWithImageEffects**

```java
PresentationLoadOptions loadOptions = new PresentationLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\presentation.pptx"
Watermarker watermarker = new Watermarker("presentation.pptx", loadOptions);                              
                                                                                                                   
ImageWatermark watermark = new ImageWatermark("logo.png");                                                  
                                                                                                                   
PresentationImageEffects effects = new PresentationImageEffects();                                                 
effects.setBrightness(0.7);                                                                                        
effects.setContrast(0.6);                                                                                          
effects.setChromaKey(Color.getRed());                                                                              
effects.getBorderLineFormat().setEnabled(true);                                                                    
effects.getBorderLineFormat().setWeight(1);                                                                        
                                                                                                                   
PresentationWatermarkSlideOptions options = new PresentationWatermarkSlideOptions();                               
options.setEffects(effects);                                                                                       
                                                                                                                   
watermarker.add(watermark, options);                                                                               
                                                                                                                   
watermarker.save("presentation.pptx");                                                                   
                                                                                                                   
watermarker.close();                                                                                               
watermark.close();                                                                                                 
```
