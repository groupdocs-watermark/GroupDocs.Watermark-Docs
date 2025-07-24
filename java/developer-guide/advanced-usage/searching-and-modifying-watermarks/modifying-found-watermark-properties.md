---
id: modifying-found-watermark-properties
url: watermark/java/modifying-found-watermark-properties
title: Modifying found watermark properties
weight: 3
description: "This article explains how to modify found watermark properties while using GroupDocs.Watermarks Java API."
keywords: modify found watermark properties
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
GroupDocs.Watermark also allows you to replace text and image in the found possible watermarks. Following sections will show you how to replace text and image of a found watermark.

## Replacing text

To replace text of the found watermarks, loop through the possible watermarks in the [watermark collection](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/PossibleWatermarkCollection) and call [setText()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/PossibleWatermark#setText(java.lang.String)) method as shown in the following code sample.

**advanced\_usage.searching\_and\_modifying\_watermarks.EditTextInFoundWatermarks**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
TextSearchCriteria searchCriteria = new TextSearchCriteria("test", false);                               
PossibleWatermarkCollection watermarks = watermarker.search(searchCriteria);                             
for (PossibleWatermark watermark : watermarks)                                                           
{                                                                                                        
    try                                                                                                  
    {                                                                                                    
        // Edit text                                                                                     
        watermark.setText("passed");                                                                     
    }                                                                                                    
    catch (Exception e)                                                                                  
    {                                                                                                    
        // Found entity may not support text editing                                                     
        // Passed argument can have inappropriate value                                                  
        // Process such cases here                                                                       
    }                                                                                                    
}                                                                                                        
                                                                                                         
// Save document                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

## Replacing text with formatting

You can also replace the watermark's text with [formatting](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/PossibleWatermark#getFormattedTextFragments()) as shown in the below code sample.

**advanced\_usage.searching\_and\_modifying\_watermarks.EditTextWithFormattingInFoundWatermarks**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"                             
Watermarker watermarker = new Watermarker("document.pdf");                                                                   
                                                                                                                                      
TextSearchCriteria searchCriteria = new TextSearchCriteria("test", false);                                                            
PossibleWatermarkCollection watermarks = watermarker.search(searchCriteria);                                                          
for (PossibleWatermark watermark : watermarks)                                                                                        
{                                                                                                                                     
    try                                                                                                                               
    {                                                                                                                                 
        // Edit text                                                                                                                  
        watermark.getFormattedTextFragments().clear();                                                                                
        watermark.getFormattedTextFragments().add("passed", new Font("Calibri", 19, FontStyle.Bold), Color.getRed(), Color.getAqua());
    }                                                                                                                                 
    catch (Exception e)                                                                                                               
    {                                                                                                                                 
        // Found entity may not support text editing                                                                                  
        // Passed arguments can have inappropriate value                                                                              
        // Process such cases here                                                                                                    
    }                                                                                                                                 
}                                                                                                                                     
                                                                                                                                      
// Save document                                                                                                                      
watermarker.save("document.pdf");                                                                                           
                                                                                                                                      
watermarker.close();                                                                                                                  
```

## Replacing image

Following code sample shows how to replace the image of the found watermarks using GroupDocs.Watermark.

**advanced\_usage.searching\_and\_modifying\_watermarks.ReplacesImageInFoundWatermarks**

```java
File imageFile = new File("image.png");                                                           
byte[] imageData = new byte[(int) imageFile.length()];                                                   
InputStream imageInputStream = new FileInputStream(imageFile);                                           
imageInputStream.read(imageData);                                                                        
imageInputStream.close();                                                                                
                                                                                                         
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
// Search watermark matching a particular image                                                          
SearchCriteria searchCriteria = new ImageDctHashSearchCriteria("logo.bmp");                       
PossibleWatermarkCollection watermarks = watermarker.search(searchCriteria);                             
for (PossibleWatermark watermark : watermarks)                                                           
{                                                                                                        
    try                                                                                                  
    {                                                                                                    
        // Replace image                                                                                 
        watermark.setImageData(imageData);                                                               
    }                                                                                                    
    catch (Exception e)                                                                                  
    {                                                                                                    
        // Found entity may not support image replacement                                                
        // Passed image can have inappropriate format                                                    
        // Process such cases here                                                                       
    }                                                                                                    
}                                                                                                        
                                                                                                         
// Save document                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

