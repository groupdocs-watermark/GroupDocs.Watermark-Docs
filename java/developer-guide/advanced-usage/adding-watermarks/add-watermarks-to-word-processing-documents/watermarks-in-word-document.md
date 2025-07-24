---
id: watermarks-in-word-document
url: watermark/java/watermarks-in-word-document
title: Watermarks in Word document
weight: 2
description: "This article explains how to add watermarks in word processing document in Java."
keywords: add watermarks, how to add watermarks
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
When adding watermark in Microsoft Word application, it places a shape with appropriate content in section headers. GroupDocs.Watermark API uses the same approach. When calling [add()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#add(com.groupdocs.watermark.Watermark)) method of [Watermarker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker) class, the shape is added to a document.

## Using properties of [WordProcessingWatermarkBaseOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkBaseOptions)

You can also set some additional options ([setName()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkBaseOptions#setName(java.lang.String)) or [setAlternativeText()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkBaseOptions#setAlternativeText(java.lang.String))) when adding shape watermark to a Word document using GroupDocs.Watermark. Following code samples demonstrates it.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingAddWatermarkWithShapeSettings**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));                      
                                                                                                           
//Some settings for watermark                                                                              
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                  
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                              
watermark.setRotateAngle(25.0);                                                                            
watermark.setForegroundColor(Color.getRed());                                                              
watermark.setOpacity(1.0);                                                                                 
                                                                                                           
WordProcessingWatermarkSectionOptions options = new WordProcessingWatermarkSectionOptions();               
                                                                                                           
// Set the shape name                                                                                      
options.setName("Shape 1");                                                                                
                                                                                                           
// Set the descriptive (alternative) text that will be associated with the shape                           
options.setAlternativeText("Test watermark");                                                              
                                                                                                           
watermarker.add(watermark, options);                                                                       
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

## Using [WordProcessingTextEffects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingTextEffects)

You can also apply some text effects to the shape watermarks as shown in the below code.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingAddWatermarkWithTextEffects**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));                      
                                                                                                           
WordProcessingTextEffects effects = new WordProcessingTextEffects();                                       
effects.getLineFormat().setEnabled(true);                                                                  
effects.getLineFormat().setColor(Color.getRed());                                                          
effects.getLineFormat().setDashStyle(OfficeDashStyle.DashDotDot);                                          
effects.getLineFormat().setLineStyle(OfficeLineStyle.Triple);                                              
effects.getLineFormat().setWeight(1);                                                                      
                                                                                                           
WordProcessingWatermarkSectionOptions options = new WordProcessingWatermarkSectionOptions();               
options.setEffects(effects);                                                                               
                                                                                                           
watermarker.add(watermark, options);                                                                       
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

## Using [WordProcessingImageEffects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingImageEffects)

GroupDocs.Watermark also provides the facility to apply image effects to the shape watermarks.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingAddWatermarkWithImageEffects**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
ImageWatermark watermark = new ImageWatermark("logo.png");                                          
                                                                                                           
WordProcessingImageEffects effects = new WordProcessingImageEffects();                                     
effects.setBrightness(0.7);                                                                                
effects.setContrast(0.6);                                                                                  
effects.setChromaKey(Color.getRed());                                                                      
effects.getBorderLineFormat().setEnabled(true);                                                            
effects.getBorderLineFormat().setWeight(1);                                                                
                                                                                                           
WordProcessingWatermarkSectionOptions options = new WordProcessingWatermarkSectionOptions();               
options.setEffects(effects);                                                                               
                                                                                                           
watermarker.add(watermark, options);                                                                       
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

