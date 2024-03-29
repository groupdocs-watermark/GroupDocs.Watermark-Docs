---
id: add-watermarks-to-diagram-documents
url: watermark/java/add-watermarks-to-diagram-documents
title: Add watermarks to diagram documents
weight: 3
description: ""
keywords: 
productName: GroupDocs.Watermark for Java
hideChildren: False
---
## Adding watermark to all pages of a particular type

Using GroupDocs.Watermark, you can add watermark to all pages of a particular type in a document. It consists of following steps.

1.  Load the document
2.  Create and initialize watermark object
3.  Set watermark properties
4.  Add watermark by specifying page type using [setPlacementType()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/DiagramShapeWatermarkOptions#setPlacementType(int)) method of [DiagramShapeWatermarkOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/DiagramShapeWatermarkOptions)
5.  Save the document

Following code shows how to add watermark to a particular type of the pages.

**advanced\_usage.add\_watermarks\_to\_diagrams.DiagramAddWatermarkToAllPagesOfParticularType**

```java
DiagramLoadOptions loadOptions = new DiagramLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\diagram.vsdx"
Watermarker watermarker = new Watermarker("diagram.vsdx", loadOptions);                         
                                                                                                         
// Initialize text watermark                                                                             
TextWatermark textWatermark = new TextWatermark("Test watermark 1", new Font("Calibri", 19));            
                                                                                                         
DiagramShapeWatermarkOptions textWatermarkOptions = new DiagramShapeWatermarkOptions();                  
textWatermarkOptions.setPlacementType(DiagramWatermarkPlacementType.BackgroundPages);                    
                                                                                                         
// Add text watermark to all background pages                                                            
watermarker.add(textWatermark, textWatermarkOptions);                                                    
                                                                                                         
// Initialize image watermark                                                                            
ImageWatermark imageWatermark = new ImageWatermark("logo.jpg");                                   
                                                                                                         
DiagramShapeWatermarkOptions imageWatermarkOptions = new DiagramShapeWatermarkOptions();                 
imageWatermarkOptions.setPlacementType(DiagramWatermarkPlacementType.ForegroundPages);                   
                                                                                                         
// Add image watermark to all foreground pages                                                           
watermarker.add(imageWatermark, imageWatermarkOptions);                                                  
                                                                                                         
watermarker.save("diagram.vsdx");                                                              
imageWatermark.close();                                                                                  
watermarker.close();                                                                                   
```

## Adding watermark on separate background page

In some cases, you may want to place the watermark on separate newly created background pages. In this case, use below code.

**advanced\_usage.add\_watermarks\_to\_diagrams.DiagramAddWatermarkToSeparateBackgroundPage**

```java
DiagramLoadOptions loadOptions = new DiagramLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\diagram.vsdx"
Watermarker watermarker = new Watermarker("diagram.vsdx", loadOptions);                         
                                                                                                         
// Initialize watermark of any supported type                                                            
TextWatermark textWatermark = new TextWatermark("Test watermark 1", new Font("Calibri", 19));            
                                                                                                         
DiagramShapeWatermarkOptions options = new DiagramShapeWatermarkOptions();                               
options.setPlacementType(DiagramWatermarkPlacementType.SeparateBackgrounds);                             
                                                                                                         
// Create separate background for each page where it is not set. Add watermark to it.                    
watermarker.add(textWatermark, options);                                                                 
                                                                                                         
watermarker.save("diagram.vsdx");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

## Add watermark to a particular page

GroupDocs.Watermark allows you to add watermark to a particular page of the document using [setPageIndex()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/DiagramPageWatermarkOptions#setPageIndex(int)) of [DiagramPageWatermarkOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/DiagramPageWatermarkOptions) as shown in below example.

**advanced\_usage.add\_watermarks\_to\_diagrams.DiagramAddWatermarkToParticularPage**

```java
DiagramLoadOptions loadOptions = new DiagramLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\diagram.vsdx"
Watermarker watermarker = new Watermarker("diagram.vsdx", loadOptions);                         
                                                                                                         
TextWatermark textWatermark = new TextWatermark("Test watermark", new Font("Calibri", 19));              
                                                                                                         
DiagramPageWatermarkOptions textWatermarkOptions = new DiagramPageWatermarkOptions();                    
textWatermarkOptions.setPageIndex(0);                                                                    
                                                                                                         
// Add text watermark to the first page                                                                  
watermarker.add(textWatermark, textWatermarkOptions);                                                    
                                                                                                         
ImageWatermark imageWatermark = new ImageWatermark("logo.jpg");                                   
                                                                                                         
DiagramPageWatermarkOptions imageWatermarkOptions = new DiagramPageWatermarkOptions();                   
imageWatermarkOptions.setPageIndex(1);                                                                   
                                                                                                         
// Add image watermark to the second page                                                                
watermarker.add(imageWatermark, imageWatermarkOptions);                                                  
                                                                                                         
watermarker.save("diagram.vsdx");                                                              
                                                                                                         
watermarker.close();                                                                                     
imageWatermark.close();                                                                                  
```

## Lock watermark

When you're calling [*add()*](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#add(com.groupdocs.watermark.Watermark)) method of *[Watermaker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker)* object created for the Diagram document, simple shape is added to the document. There is no difference between added watermark and Visio shapes that are used to create diagrams.

GroupDocs.Watermark allows you to protect watermark from editing in MS Visio by calling [setLocked()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/DiagramWatermarkOptions#setLocked(boolean)) method of [DiagramShapeWatermarkOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/DiagramShapeWatermarkOptions) (as shown in the following example).

**advanced\_usage.add\_watermarks\_to\_diagrams.DiagramLockWatermarkShape**

```java
DiagramLoadOptions loadOptions = new DiagramLoadOptions();                                                
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\diagram.vsdx" 
Watermarker watermarker = new Watermarker("diagram.vsdx", loadOptions);                          
                                                                                                          
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));                     
                                                                                                          
DiagramShapeWatermarkOptions options = new DiagramShapeWatermarkOptions();                                
options.setLocked(true);                                                                                  
                                                                                                          
// Editing of the shape in Visio is forbidden                                                             
watermarker.add(watermark, options);                                                                      
                                                                                                          
watermarker.save("diagram.vsdx");                                                               
                                                                                                          
watermarker.close();                                                                                      
```

