---
id: existing-objects-in-word-document
url: watermark/java/existing-objects-in-word-document
title: Existing objects in Word document
weight: 3
description: "This article explains how to remove shape of any type from any level of document structure while using GroupDocs watermarking Java API"
keywords: document structure, remove shape
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
Watermarks in Word documents are usually represented by shapes. Using GroupDocs.Watermark API you can easily remove shape of any type from any level of document structure.

## Removing watermark from a particular section

Removing watermark from a particular section of a Word document using GroupDocs.Watermark consists of following steps.

1.  Load the document 
2.  Create and initialize [image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/ImageSearchCriteria) or [text](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/TextSearchCriteria) search criteria  
3.  Find possible watermarks
4.  Remove found watermarks 
5.  Save the document

Following code sample shows how to remove watermark from a particular section.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingRemoveWatermarkFromSection**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                                              
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"                           
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                                                     
                                                                                                                                      
// Initialize search criteria                                                                                                         
ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("logo.png");                                          
TextSearchCriteria textSearchCriteria = new TextSearchCriteria("Company Name");                                                       
                                                                                                                                      
// Call Search method for the section                                                                                                 
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                                                  
PossibleWatermarkCollection possibleWatermarks = content.getSections().get_Item(0).search(textSearchCriteria.or(imageSearchCriteria));
                                                                                                                                      
// Remove all found watermarks                                                                                                        
for (int i = possibleWatermarks.getCount() - 1; i >= 0; i--)                                                                          
{                                                                                                                                     
    possibleWatermarks.removeAt(i);                                                                                                   
}                                                                                                                                     
                                                                                                                                      
watermarker.save("document.docx");                                                                                          
                                                                                                                                      
watermarker.close();                                                                                                                  
```

### Search for particular header or footer  

You can also call [search()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/ContentPart#search()) method for a particular [header or footer](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingHeaderFooter) as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingFindWatermarkInHeaderFooter**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
// Initialize search criteria                                                                              
ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("logo.png");               
TextSearchCriteria textSearchCriteria = new TextSearchCriteria("Company Name");                            
                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                       
PossibleWatermarkCollection possibleWatermarks = content                                                   
        .getSections().get_Item(0)                                                                         
        .getHeadersFooters().getByOfficeHeaderFooterType(OfficeHeaderFooterType.HeaderPrimary)             
        .search(textSearchCriteria.or(imageSearchCriteria));                                               
                                                                                                           
// Remove all found watermarks                                                                             
for (int i = possibleWatermarks.getCount() - 1; i >= 0; i--)                                               
{                                                                                                          
    possibleWatermarks.removeAt(i);                                                                        
}                                                                                                          
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

## Extracting information about all shapes in a Word document

[search()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/ContentPart#search()) method returns a collection of [PossibleWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/PossibleWatermark) instances for all document types. But in some cases, it's necessary to get more information about Word shapes than common API offers. GroupDocs.Watermark enables you to extract the information about all the [shapes](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingSection#getShapes()) as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingGetShapesInformation**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                       
for (WordProcessingSection section : content.getSections())                                                
{                                                                                                          
    for (WordProcessingShape shape : section.getShapes())                                                  
    {                                                                                                      
        if (shape.getHeaderFooter() != null)                                                               
        {                                                                                                  
            System.out.println("In header/footer");                                                        
        }                                                                                                  
                                                                                                           
        System.out.println(shape.getShapeType());                                                          
        System.out.println(shape.getWidth());                                                              
        System.out.println(shape.getHeight());                                                             
        System.out.println(shape.isWordArt());                                                             
        System.out.println(shape.getRotateAngle());                                                        
        System.out.println(shape.getAlternativeText());                                                    
        System.out.println(shape.getName());                                                               
        System.out.println(shape.getX());                                                                  
        System.out.println(shape.getY());                                                                  
        System.out.println(shape.getText());                                                               
        if (shape.getImage() != null)                                                                      
        {                                                                                                  
            System.out.println(shape.getImage().getWidth());                                               
            System.out.println(shape.getImage().getHeight());                                              
            System.out.println(shape.getImage().getBytes().length);                                        
        }                                                                                                  
                                                                                                           
        System.out.println(shape.getHorizontalAlignment());                                                
        System.out.println(shape.getVerticalAlignment());                                                  
        System.out.println(shape.getRelativeHorizontalPosition());                                         
        System.out.println(shape.getRelativeVerticalPosition());                                           
    }                                                                                                      
}                                                                                                          
                                                                                                           
watermarker.close();                                                                                       
```

## Working with shape types

You can extract information about the existing shapes of particular types. The [WordProcessingShapeType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShapeType) enum is available to check the types possibly available shapes.

The following code snippet demonstrates the usage of [WordProcessingShapeType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShapeType) enum.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingShapeTypeUsage**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                                                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"                                                
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                                                                          
                                                                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                                                                       
for (WordProcessingSection section : content.getSections())                                                                                                
{                                                                                                                                                          
    for (WordProcessingShape shape : section.getShapes())                                                                                                  
    {                                                                                                                                                      
        //Check for Diagonal Corners Rounded shapes                                                                                                        
        if (shape.getShapeType() == WordProcessingShapeType.DiagonalCornersRounded)                                                                        
        {                                                                                                                                                  
            System.out.println("Diagonal Corners Rounded shape found");                                                                                    
                                                                                                                                                           
            //Write text on all Diagonal Corners Rounded shapes                                                                                            
            shape.getFormattedTextFragments().add("I am Diagonal Corner Rounded", new Font("Calibri", 8, FontStyle.Bold), Color.getRed(), Color.getAqua());
        }                                                                                                                                                  
    }                                                                                                                                                      
}                                                                                                                                                          
                                                                                                                                                           
watermarker.save("document.docx");                                                                                                               
                                                                                                                                                           
watermarker.close();                                                                                                                                       
```

## Removing a particular shape

You can also remove a particular [shape](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape) from a Word document as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingRemoveShape**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                        
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"     
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                               
                                                                                                                
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                            
                                                                                                                
// Remove shape by index                                                                                        
content.getSections().get_Item(0).getShapes().removeAt(0);                                                      
                                                                                                                
// Remove shape by reference                                                                                    
content.getSections().get_Item(0).getShapes().remove(content.getSections().get_Item(0).getShapes().get_Item(0));
                                                                                                                
watermarker.save("document.docx");                                                                    
                                                                                                                
watermarker.close();                                                                                            
```

## Removing shapes with particular text formatting

You can also find and remove the shapes with a particular [text formatting](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#getFormattedTextFragments()) from a Word document as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingRemoveShapesWithParticularTextFormatting**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                              
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"           
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                                     
                                                                                                                      
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                                  
for (WordProcessingSection section : content.getSections())                                                           
{                                                                                                                     
    for (int i = section.getShapes().getCount() - 1; i >= 0; i--)                                                     
    {                                                                                                                 
        for (FormattedTextFragment fragment : section.getShapes().get_Item(i).getFormattedTextFragments())            
        {                                                                                                             
            if (fragment.getForegroundColor().equals(Color.getRed()) && fragment.getFont().getFamilyName() == "Arial")
            {                                                                                                         
                section.getShapes().removeAt(i);                                                                      
                break;                                                                                                
            }                                                                                                         
        }                                                                                                             
    }                                                                                                                 
}                                                                                                                     
                                                                                                                      
watermarker.save("document.docx");                                                                          
                                                                                                                      
watermarker.close();                                                                                                  
```

## Removing or replacing hyperlink associated with a particular shape

Using GroupDocs.Watermark for Java, you can also remove or replace [hyperlink](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setHyperlink(java.lang.String)) associated with a particular shape inside a Word document. Use following code sample to achieve this functionality.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingRemoveHyperlinks**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                       
                                                                                                           
// Replace hyperlink                                                                                       
content.getSections().get_Item(0).getShapes().get_Item(0).setHyperlink("https://www.groupdocs.com/");      
                                                                                                           
// Remove hyperlink                                                                                        
content.getSections().get_Item(0).getShapes().get_Item(1).setHyperlink(null);                              
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

## Replacing text for particular shapes

### Replacing shape's text

GroupDocs.Watermark supports replacing [text](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setText(java.lang.String)) for particular shapes in a Word document. Following code sample shows the usage of this feature.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingReplaceTextForParticularShape**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                       
                                                                                                           
// Set shape's text                                                                                        
for (WordProcessingShape shape : content.getSections().get_Item(0).getShapes())                            
{                                                                                                          
    if (shape.getText().contains("Some text"))                                                             
    {                                                                                                      
        shape.setText("Another text");                                                                     
    }                                                                                                      
}                                                                                                          
                                                                                                           
// Save document                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

### Replacing shape's text with formatted text

You can also replace the [text](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setText(java.lang.String)) of the shapes with [formatted text](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#getFormattedTextFragments()) as shown in the following code sample.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingReplaceShapeTextWithFormattedText**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                                                
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"                             
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                                                       
                                                                                                                                        
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                                                    
                                                                                                                                        
// Set shape's text                                                                                                                     
for (WordProcessingShape shape : content.getSections().get_Item(0).getShapes())                                                         
{                                                                                                                                       
    if (shape.getText().contains("Some text"))                                                                                          
    {                                                                                                                                   
        shape.getFormattedTextFragments().clear();                                                                                      
        shape.getFormattedTextFragments().add("Another text", new Font("Calibri", 19, FontStyle.Bold), Color.getRed(), Color.getAqua());
    }                                                                                                                                   
}                                                                                                                                       
                                                                                                                                        
// Save document                                                                                                                        
watermarker.save("document.docx");                                                                                            
                                                                                                                                        
watermarker.close();                                                                                                                    
```

## Replacing shape's image

GroupDocs.Watermark also allows you to replace the [image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setImage(com.groupdocs.watermark.contents.WordProcessingWatermarkableImage)) of the particular shapes in a Word document as shown in the following code sample.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingReplaceShapeImage**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                       
                                                                                                           
File imageFile = new File("test.png");                                                              
byte[] imageBytes = new byte[(int) imageFile.length()];                                                    
InputStream imageInputStream = new FileInputStream(imageFile);                                             
imageInputStream.read(imageBytes);                                                                         
imageInputStream.close();                                                                                  
                                                                                                           
// Set shape image                                                                                         
for (WordProcessingShape shape : content.getSections().get_Item(0).getShapes())                            
{                                                                                                          
    if (shape.getImage() != null)                                                                          
    {                                                                                                      
        shape.setImage(new WordProcessingWatermarkableImage(imageBytes));                                  
    }                                                                                                      
}                                                                                                          
                                                                                                           
// Save document                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

## Modifying shape properties

GroupDocs.Watermark also provides the feature of modifying properties ([setAlternativeText()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setAlternativeText(java.lang.String)), [setRotateAngle()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setRotateAngle(double)), [setX()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setX(double)), [setY()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setY(double)), [setHeight()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setHeight(double)), [setWidth()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setWidth(double)) or [setBehindText()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingShape#setBehindText(boolean))) of particular shapes in a Word document. Following code sample shows how to use this feature.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingModifyShapeProperties**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                       
                                                                                                           
// Change shape properties                                                                                 
for (WordProcessingShape shape : content.getSections().get_Item(0).getShapes())                            
{                                                                                                          
    if (shape.getText().contains("Some text"))                                                             
    {                                                                                                      
        shape.setAlternativeText("watermark");                                                             
        shape.setRotateAngle(30);                                                                          
        shape.setX(200);                                                                                   
        shape.setY(200);                                                                                   
        shape.setHeight(100);                                                                              
        shape.setWidth(400);                                                                               
        shape.setBehindText(false);                                                                        
    }                                                                                                      
}                                                                                                          
                                                                                                           
// Save document                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```
