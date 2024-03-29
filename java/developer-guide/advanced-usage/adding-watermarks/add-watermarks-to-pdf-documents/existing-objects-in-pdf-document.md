---
id: existing-objects-in-pdf-document
url: watermark/java/existing-objects-in-pdf-document
title: Existing objects in PDF document
weight: 3
description: Removing watermark from a particular page of PDF document using C#.
keywords: Removing watermark, watermark
productName: GroupDocs.Watermark for Java
hideChildren: False
---
## Removing watermark from a particular page

Removing watermark from a particular page of PDF document using GroupDocs.Watermark consists of following steps.

1.  Load the document 
2.  Create and initialize Image/text search criteria 
3.  Find watermarks
4.  Remove watermarks
5.  Save the document

Following code sample removes watermarks from a particular page.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRemoveWatermark**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                                                    
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"                             
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                                                      
                                                                                                                                      
// Initialize search criteria                                                                                                         
ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("logo.png");                                          
TextSearchCriteria textSearchCriteria = new TextSearchCriteria("Company Name");                                                       
                                                                                                                                      
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                                                     
PossibleWatermarkCollection possibleWatermarks = pdfContent.getPages().get_Item(0).search(imageSearchCriteria.or(textSearchCriteria));
                                                                                                                                      
// Remove all found watermarks                                                                                                        
for (int i = possibleWatermarks.getCount() - 1; i >= 0; i--)                                                                          
{                                                                                                                                     
    possibleWatermarks.removeAt(i);                                                                                                   
}                                                                                                                                     
                                                                                                                                      
watermarker.save("document.pdf");                                                                                           
                                                                                                                                      
watermarker.close();                                                                                                                  
```

[Search()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#search()) method searches watermarks of all mentioned types, but in some cases, it's necessary to analyze only one class of PDF entities. The following articles specifically deal with different types of the watermark objects in a PDF document.

## Working with XObjects

### Extracting information about all XObjects in PDF document

Using GroupDocs.Watermark for .NET, you can extract information about all the [XObjects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfXObject) in a PDF document. Following code sample performs this functionality.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfExtractXObjectInformation**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
for (PdfPage page : pdfContent.getPages())                                                               
{                                                                                                        
    for (PdfXObject xObject : page.getXObjects())                                                        
    {                                                                                                    
        if (xObject.getImage() != null)                                                                  
        {                                                                                                
            System.out.println(xObject.getImage().getWidth());                                           
            System.out.println(xObject.getImage().getHeight());                                          
            System.out.println(xObject.getImage().getBytes().length);                                    
        }                                                                                                
                                                                                                         
        System.out.println(xObject.getText());                                                           
        System.out.println(xObject.getX());                                                              
        System.out.println(xObject.getY());                                                              
        System.out.println(xObject.getWidth());                                                          
        System.out.println(xObject.getHeight());                                                         
        System.out.println(xObject.getRotateAngle());                                                    
    }                                                                                                    
}                                                                                                        
                                                                                                         
watermarker.close();                                                                                     
```

### Removing a particular XObject

You can also remove an XObject from a page using GroupDocs.Watermark. Following code sample removes an XObject from a particular page.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRemoveXObject**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                                  
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"           
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                                    
                                                                                                                    
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                                   
                                                                                                                    
// Remove XObject by index                                                                                          
pdfContent.getPages().get_Item(0).getXObjects().removeAt(0);                                                        
                                                                                                                    
// Remove XObject by reference                                                                                      
pdfContent.getPages().get_Item(0).getXObjects().remove(pdfContent.getPages().get_Item(0).getXObjects().get_Item(0));
                                                                                                                    
watermarker.save("document.pdf");                                                                         
                                                                                                                    
watermarker.close();                                                                                                
```

### Removing XObjects containing text with particular text formatting

You can also find and remove all XObjects containing [text with a particular formatting](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#getFormattedTextFragments()) from a PDF document as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRemoveXObjectWithParticularTextFormatting**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
for (PdfPage page : pdfContent.getPages())                                                               
{                                                                                                        
    for (int i = page.getXObjects().getCount() - 1; i >= 0; i--)                                         
    {                                                                                                    
        for (FormattedTextFragment fragment : page.getXObjects().get_Item(i).getFormattedTextFragments())
        {                                                                                                
            if (fragment.getForegroundColor().equals(Color.getRed()))                                    
            {                                                                                            
                page.getXObjects().removeAt(i);                                                          
                break;                                                                                   
            }                                                                                            
        }                                                                                                
    }                                                                                                    
}                                                                                                        
                                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

### Adding watermark to all image XObjects

GroupDocs.Watermark API allows you to add watermark to all [image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#getImage()) XObjects in a PDF document. Following code sample serves this purpose.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfAddWatermarkToXObjects**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
                                                                                                         
// Initialize image or text watermark                                                                    
TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));                    
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                            
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                
watermark.setRotateAngle(45);                                                                            
watermark.setSizingType(SizingType.ScaleToParentDimensions);                                             
watermark.setScaleFactor(1);                                                                             
                                                                                                         
for (PdfPage page : pdfContent.getPages())                                                               
{                                                                                                        
    for (PdfXObject xObject : page.getXObjects())                                                        
    {                                                                                                    
        if (xObject.getImage() != null)                                                                  
        {                                                                                                
            // Add watermark to the image                                                                
            xObject.getImage().add(watermark);                                                           
        }                                                                                                
    }                                                                                                    
}                                                                                                        
                                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

### Replacing text for particular XObjects

GroupDocs.Watermark allows you to edit and replace the text of the particular XObject. You can also replace XObject's [text](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#setText(java.lang.String)) with formatting as shown in the below code samples.

#### Replacing text

**advanced\_usage.add\_watermarks\_to\_pdf.PdfReplaceTextForParticularXObject**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
for (PdfXObject xObject : pdfContent.getPages().get_Item(0).getXObjects())                               
{                                                                                                        
    // Replace text                                                                                      
    if (xObject.getText().contains("Test"))                                                              
    {                                                                                                    
        xObject.setText("Passed");                                                                       
    }                                                                                                    
}                                                                                                        
                                                                                                         
// Save document                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

#### Replacing text with formatting

**advanced\_usage.add\_watermarks\_to\_pdf.ReplaceTextForParticularXObjectWithFormatting**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                                                  
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"                           
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                                                    
                                                                                                                                    
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                                                   
for (PdfXObject xObject : pdfContent.getPages().get_Item(0).getXObjects())                                                          
{                                                                                                                                   
    // Replace text                                                                                                                 
    if (xObject.getText().contains("Test"))                                                                                         
    {                                                                                                                               
        xObject.getFormattedTextFragments().clear();                                                                                
        xObject.getFormattedTextFragments().add("Passed", new Font("Calibri", 19, FontStyle.Bold), Color.getRed(), Color.getAqua());
    }                                                                                                                               
}                                                                                                                                   
                                                                                                                                    
// Save document                                                                                                                    
watermarker.save("document.pdf");                                                                                         
                                                                                                                                    
watermarker.close();                                                                                                                
```

### Replacing image for particular XObjects

Using GroupDocs.Watermark, you can also replace the image of a particular XObject. GroupDocs.Watermark allows you to loop through all the [XObjects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfPage#getXObjects()) of a particular page and you can replace the [image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#setImage(com.groupdocs.watermark.contents.PdfWatermarkableImage)) of particular XObjects using some condition as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfReplaceImageForParticularXObject**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
                                                                                                         
File imageFile = new File("test.png");                                                            
byte[] imageBytes = new byte[(int) imageFile.length()];                                                  
InputStream imageStream = new FileInputStream(imageFile);                                                
imageStream.read(imageBytes);                                                                            
imageStream.close();                                                                                     
                                                                                                         
// Replace image                                                                                         
for (PdfXObject xObject : pdfContent.getPages().get_Item(0).getXObjects())                               
{                                                                                                        
    if (xObject.getImage() != null)                                                                      
    {                                                                                                    
        xObject.setImage(new PdfWatermarkableImage(imageBytes));                                         
    }                                                                                                    
}                                                                                                        
                                                                                                         
// Save document                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

## Working with artifacts

### Extracting information about all artifacts in PDF document

GroupDocs.Watermark enables you to extract the information about the [artifacts](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfPage#getArtifacts()) in a PDF document as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfExtractArtifactInformation**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
for (PdfPage page : pdfContent.getPages())                                                               
{                                                                                                        
    for (PdfArtifact artifact : page.getArtifacts())                                                     
    {                                                                                                    
        System.out.println(artifact.getArtifactType());                                                  
        System.out.println(artifact.getArtifactSubtype());                                               
        if (artifact.getImage() != null)                                                                 
        {                                                                                                
            System.out.println(artifact.getImage().getWidth());                                          
            System.out.println(artifact.getImage().getHeight());                                         
            System.out.println(artifact.getImage().getBytes().length);                                   
        }                                                                                                
                                                                                                         
        System.out.println(artifact.getText());                                                          
        System.out.println(artifact.getOpacity());                                                       
        System.out.println(artifact.getX());                                                             
        System.out.println(artifact.getY());                                                             
        System.out.println(artifact.getWidth());                                                         
        System.out.println(artifact.getHeight());                                                        
        System.out.println(artifact.getRotateAngle());                                                   
    }                                                                                                    
}                                                                                                        
                                                                                                         
watermarker.close();                                                                                     
```

### Removing a particular artifact

Following code sample shows how to remove an [artifact](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfArtifact) from a particular page of the PDF document.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRemoveArtifact**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                                    
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"             
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                                      
                                                                                                                      
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                                     
                                                                                                                      
// Remove Artifact by index                                                                                           
pdfContent.getPages().get_Item(0).getArtifacts().removeAt(0);                                                         
                                                                                                                      
// Remove Artifact by reference                                                                                       
pdfContent.getPages().get_Item(0).getArtifacts().remove(pdfContent.getPages().get_Item(0).getArtifacts().get_Item(0));
                                                                                                                      
watermarker.save("document.pdf");                                                                           
                                                                                                                      
watermarker.close();                                                                                                  
```

### Removing artifacts containing text with particular text formatting

You can also find and remove all artifacts containing [text with a particular formatting](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#getFormattedTextFragments()) from a PDF document as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRemoveArtifactsWithParticularTextFormatting**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                        
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf" 
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                          
                                                                                                          
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                         
for (PdfPage page : pdfContent.getPages())                                                                
{                                                                                                         
    for (int i = page.getArtifacts().getCount() - 1; i >= 0; i--)                                         
    {                                                                                                     
        for (FormattedTextFragment fragment : page.getArtifacts().get_Item(i).getFormattedTextFragments())
        {                                                                                                 
            if (fragment.getFont().getSize() > 42)                                                        
            {                                                                                             
                page.getArtifacts().removeAt(i);                                                          
                break;                                                                                    
            }                                                                                             
        }                                                                                                 
    }                                                                                                     
}                                                                                                         
                                                                                                          
watermarker.save("document.pdf");                                                               
                                                                                                          
watermarker.close();                                                                                      
```

### Adding watermark to all image artifacts

GroupDocs.Watermark API also provides the feature of adding watermark to all image artifacts in a PDF document. Following code sample adds watermark to all [image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#getImage()) artifacts.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfAddWatermarkToImageArtifacts**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
                                                                                                         
// Initialize image or text watermark                                                                    
TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));                    
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                            
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                
watermark.setRotateAngle(45);                                                                            
watermark.setSizingType(SizingType.ScaleToParentDimensions);                                             
watermark.setScaleFactor(1);                                                                             
                                                                                                         
for (PdfPage page : pdfContent.getPages())                                                               
{                                                                                                        
    for (PdfArtifact artifact : page.getArtifacts())                                                     
    {                                                                                                    
        if (artifact.getImage() != null)                                                                 
        {                                                                                                
            // Add watermark to the image                                                                
            artifact.getImage().add(watermark);                                                          
        }                                                                                                
    }                                                                                                    
}                                                                                                        
                                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

### Replacing text for particular artifacts

GroupDocs.Watermark allows you to edit and replace the [text](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfArtifact#setText(java.lang.String)) of the particular artifacts. You can also replace artifact's [text with formatting](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#getFormattedTextFragments()) as shown in the below code samples.

#### Replacing text

**advanced\_usage.add\_watermarks\_to\_pdf.PdfReplaceTextForParticularArtifact**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
for (PdfArtifact artifact : pdfContent.getPages().get_Item(0).getArtifacts())                            
{                                                                                                        
    // Replace text                                                                                      
    if (artifact.getText().contains("Test"))                                                             
    {                                                                                                    
        artifact.setText("Passed");                                                                      
    }                                                                                                    
}                                                                                                        
                                                                                                         
// Save document                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

#### Replacing text with formatting

**advanced\_usage.add\_watermarks\_to\_pdf.PdfReplaceTextForParticularArtifactWithFormatting**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"                            
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                                                     
                                                                                                                                     
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                                                    
for (PdfArtifact artifact : pdfContent.getPages().get_Item(0).getArtifacts())                                                        
{                                                                                                                                    
    // Replace text                                                                                                                  
    if (artifact.getText().contains("Test"))                                                                                         
    {                                                                                                                                
        artifact.getFormattedTextFragments().clear();                                                                                
        artifact.getFormattedTextFragments().add("Passed", new Font("Calibri", 19, FontStyle.Bold), Color.getRed(), Color.getAqua());
    }                                                                                                                                
}                                                                                                                                    
                                                                                                                                     
// Save document                                                                                                                     
watermarker.save("document.pdf");                                                                                          
                                                                                                                                     
watermarker.close();                                                                                                                 
```

### Replacing image for particular artifacts

Using GroupDocs.Watermark, you can also replace the image of a particular artifact. GroupDocs.Watermark allows you to loop through all the [artifacts](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfPage#getArtifacts()) of a particular page and you can replace the [image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#setImage(com.groupdocs.watermark.contents.PdfWatermarkableImage)) of particular artifacts using some condition as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfReplaceImageForParticularArtifact**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
                                                                                                         
File imageFile = new File("test.png");                                                            
byte[] imageBytes = new byte[(int) imageFile.length()];                                                  
InputStream imageStream = new FileInputStream(imageFile);                                                
imageStream.read(imageBytes);                                                                            
imageStream.close();                                                                                     
                                                                                                         
// Replace image                                                                                         
for (PdfArtifact artifact : pdfContent.getPages().get_Item(0).getArtifacts())                            
{                                                                                                        
    if (artifact.getImage() != null)                                                                     
    {                                                                                                    
        artifact.setImage(new PdfWatermarkableImage(imageBytes));                                        
    }                                                                                                    
}                                                                                                        
                                                                                                         
// Save document                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

## Working with annotations

### Extracting information about all annotations in PDF document

You can also extract information about all the [annotations](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfPage#getAnnotations()) in a PDF document using GroupDocs.Watermark as shown in below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfExtractAnnotationInformation**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
for (PdfPage page : pdfContent.getPages())                                                               
{                                                                                                        
    for (PdfAnnotation annotation : page.getAnnotations())                                               
    {                                                                                                    
        System.out.println(annotation.getAnnotationType());                                              
        if (annotation.getImage() != null)                                                               
        {                                                                                                
            System.out.println(annotation.getImage().getWidth());                                        
            System.out.println(annotation.getImage().getHeight());                                       
            System.out.println(annotation.getImage().getBytes().length);                                 
        }                                                                                                
                                                                                                         
        System.out.println(annotation.getText());                                                        
        System.out.println(annotation.getX());                                                           
        System.out.println(annotation.getY());                                                           
        System.out.println(annotation.getWidth());                                                       
        System.out.println(annotation.getHeight());                                                      
        System.out.println(annotation.getRotateAngle());                                                 
    }                                                                                                    
}                                                                                                        
                                                                                                         
watermarker.close();                                                                                     
```

### Removing a particular annotation

Following code sample can be used to remove a particular [annotation](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfAnnotation) from a PDF document.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRemoveAnnotation**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                                        
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"                 
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                                          
                                                                                                                          
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                                         
                                                                                                                          
// Remove Annotation by index                                                                                             
pdfContent.getPages().get_Item(0).getAnnotations().removeAt(0);                                                           
                                                                                                                          
// Remove Annotation by reference                                                                                         
pdfContent.getPages().get_Item(0).getAnnotations().remove(pdfContent.getPages().get_Item(0).getAnnotations().get_Item(0));
                                                                                                                          
watermarker.save("document.pdf");                                                                               
                                                                                                                          
watermarker.close();                                                                                                      
```

### Removing annotations containing text with particular text formatting

You can also find and remove all annotations containing [text with a particular formatting](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#getFormattedTextFragments()) from a PDF document as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRemoveAnnotationsWithParticularTextFormatting**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                          
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"   
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                            
                                                                                                            
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                           
for (PdfPage page : pdfContent.getPages())                                                                  
{                                                                                                           
    for (int i = page.getAnnotations().getCount() - 1; i >= 0; i--)                                         
    {                                                                                                       
        for (FormattedTextFragment fragment : page.getAnnotations().get_Item(i).getFormattedTextFragments())
        {                                                                                                   
            if (fragment.getFont().getFamilyName() == "Verdana")                                            
            {                                                                                               
                page.getAnnotations().removeAt(i);                                                          
                break;                                                                                      
            }                                                                                               
        }                                                                                                   
    }                                                                                                       
}                                                                                                           
                                                                                                            
watermarker.save("document.pdf");                                                                 
                                                                                                            
watermarker.close();                                                                                        
```

### Adding watermark to all image annotations 

Similar to the other types, the watermark can be added to [image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#getImage()) annotations in PDF documents as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfAddWatermarkToAnnotationImages**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
                                                                                                         
// Initialize image or text watermark                                                                    
TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));                    
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                            
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                
watermark.setRotateAngle(45);                                                                            
watermark.setSizingType(SizingType.ScaleToParentDimensions);                                             
watermark.setScaleFactor(1);                                                                             
                                                                                                         
for (PdfPage page : pdfContent.getPages())                                                               
{                                                                                                        
    for (PdfAnnotation annotation : page.getAnnotations())                                               
    {                                                                                                    
        if (annotation.getImage() != null)                                                               
        {                                                                                                
            // Add watermark to the image                                                                
            annotation.getImage().add(watermark);                                                        
        }                                                                                                
    }                                                                                                    
}                                                                                                        
                                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

### Replacing text for particular annotations

GroupDocs.Watermark allows you to edit and replace the [text](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#setText(java.lang.String)) of the particular annotations. You can also replace annotation's [text with formatting](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#getFormattedTextFragments()) as shown in the below code samples.

#### Replacing text

**advanced\_usage.add\_watermarks\_to\_pdf.PdfReplaceTextForParticularAnnotation**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
for (PdfAnnotation annotation : pdfContent.getPages().get_Item(0).getAnnotations())                      
{                                                                                                        
    // Replace text                                                                                      
    if (annotation.getText().contains("Test"))                                                           
    {                                                                                                    
        annotation.setText("Passed");                                                                    
    }                                                                                                    
}                                                                                                        
                                                                                                         
// Save document                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

#### Replacing text with formatting

**advanced\_usage.add\_watermarks\_to\_pdf.PdfReplaceTextForParticularAnnotationWithFormatting**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                                                     
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"                              
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                                                       
                                                                                                                                       
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                                                      
for (PdfAnnotation annotation : pdfContent.getPages().get_Item(0).getAnnotations())                                                    
{                                                                                                                                      
    // Replace text                                                                                                                    
    if (annotation.getText().contains("Test"))                                                                                         
    {                                                                                                                                  
        annotation.getFormattedTextFragments().clear();                                                                                
        annotation.getFormattedTextFragments().add("Passed", new Font("Calibri", 19, FontStyle.Bold), Color.getRed(), Color.getAqua());
    }                                                                                                                                  
}                                                                                                                                      
                                                                                                                                       
// Save document                                                                                                                       
watermarker.save("document.pdf");                                                                                            
                                                                                                                                       
watermarker.close();                                                                                                                   
```

### Replacing image for particular annotations

Using GroupDocs.Watermark, you can also replace the image of a particular annotation. GroupDocs.Watermark allows you to loop through all the annotations of a particular page and you can replace the [image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfShape#setImage(com.groupdocs.watermark.contents.PdfWatermarkableImage)) of particular annotations using some condition as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfReplaceImageForParticularAnnotation**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
                                                                                                         
File imageFile = new File("test.png");                                                            
byte[] imageBytes = new byte[(int) imageFile.length()];                                                  
InputStream imageStream = new FileInputStream(imageFile);                                                
imageStream.read(imageBytes);                                                                            
imageStream.close();                                                                                     
                                                                                                         
// Replace image                                                                                         
for (PdfAnnotation annotation : pdfContent.getPages().get_Item(0).getAnnotations())                      
{                                                                                                        
    if (annotation.getImage() != null)                                                                   
    {                                                                                                    
        annotation.setImage(new PdfWatermarkableImage(imageBytes));                                      
    }                                                                                                    
}                                                                                                        
                                                                                                         
// Save document                                                                                         
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```
