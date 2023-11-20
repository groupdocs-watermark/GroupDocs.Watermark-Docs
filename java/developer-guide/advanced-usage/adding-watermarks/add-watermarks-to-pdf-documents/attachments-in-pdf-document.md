---
id: attachments-in-pdf-document
url: watermark/java/attachments-in-pdf-document
title: Attachments in PDF document
weight: 4
description: "This article explains how to work with PDF attachments while using GroupDocs watermarking Java API."
keywords: watermarking, API, PDF attachments, Extract all attachments
productName: GroupDocs.Watermark for Java
hideChildren: False
---


## Extract all attachments from PDF document 

GroupDocs.Watermark API allows you to extract [attachments](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/PdfContent#getAttachments()) in PDF document. Following code performs this functionality.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfExtractAllAttachments**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                           
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"    
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                             
                                                                                                             
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                            
for (PdfAttachment attachment : pdfContent.getAttachments())                                                 
{                                                                                                            
    System.out.println("Name: " + attachment.getName());                                                     
    System.out.println("Description: " + attachment.getDescription());                                       
    System.out.println("File type: " + attachment.getDocumentInfo().getFileType());                          
                                                                                                             
    // Save the attached file on disk                                                                        
    FileOutputStream outputStream = new FileOutputStream("SampleFiles\\Output" + "\\" + attachment.getName());
    outputStream.write(attachment.getContent());                                                             
    outputStream.close();                                                                                    
}                                                                                                            
                                                                                                             
watermarker.close();                                                                                         
```

## Add an attachment to PDF document

The API also allows you to add attachments to the PDF document. Following code snippet shows how to remove an attachment

**advanced\_usage.add\_watermarks\_to\_pdf.PdfAddAttachment**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                        
                                                                                                         
File file = new File("sample.docx");                                                            
byte[] attachmentBytes = new byte[(int) file.length()];                                                  
InputStream inputStream = new FileInputStream(file);                                                     
inputStream.read(attachmentBytes);                                                                       
inputStream.close();                                                                                     
                                                                                                         
// Add the attachment                                                                                    
pdfContent.getAttachments().add(attachmentBytes, "sample doc", "sample doc as attachment");              
                                                                                                         
// Save changes                                                                                          
watermarker.save("document.pdf");                                                              
                                                                                                         
watermarker.close();                                                                                     
```

## Remove attachment from PDF document

The API also allows you to remove attachments from the PDF document. Following code snippet shows how to remove an attachment.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfRemoveAttachment**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                             
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"      
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                               
                                                                                                               
PdfContent pdfContent = watermarker.getContent(PdfContent.class);                                              
for (int i = pdfContent.getAttachments().getCount() - 1; i >= 0; i--)                                          
{                                                                                                              
    PdfAttachment attachment = pdfContent.getAttachments().get_Item(i);                                        
                                                                                                               
    // Remove all attached pdf files with a particular name                                                    
    if (attachment.getName().contains("sample") && attachment.getDocumentInfo().getFileType() == FileType.DOCX)
    {                                                                                                          
        pdfContent.getAttachments().removeAt(i);                                                               
    }                                                                                                          
}                                                                                                              
                                                                                                               
watermarker.save("document.pdf");                                                                    
                                                                                                               
watermarker.close();                                                                                           
```

## Search for images attachments

In case you want to search for all the images attachments in a PDF document, you can use GroupDocs.Watermark. Following code sample shows how to search images attachments of PDF document.

**advanced\_usage.add\_watermarks\_to\_pdf.PdfSearchImageInAttachment**

```java
PdfLoadOptions loadOptions = new PdfLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf", loadOptions);                         
                                                                                                         
// Consider only the attached images                                                                     
watermarker.getSearchableObjects().setPdfSearchableObjects(PdfSearchableObjects.AttachedImages);         
                                                                                                         
// Search for similar images                                                                             
WatermarkableImageCollection possibleWatermarks = watermarker.getImages();                               
                                                                                                         
System.out.println("Found " + possibleWatermarks.getCount() + " image(s).");                             
                                                                                                         
watermarker.close();                                                                                     
```
