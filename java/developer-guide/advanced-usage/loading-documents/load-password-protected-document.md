---
id: load-password-protected-document
url: watermark/java/load-password-protected-document
title: Load password-protected document
weight: 4
description: "This article explains how to load password-protected document while using GroupDocs. Watermarks Java API."
keywords: load password-protected document
productName: GroupDocs.Watermark for Java
hideChildren: False
---
Some document formats also support content encryption. To load these type of documents you will have to provide the password. GroupDocs.Watermark API allows you to load content of these documents to manage watermark.

## Load password-protected document of any supported format

The following example demonstrates how to load an encrypted document of any supported format using the password. If the password is incorrect, [InvalidPasswordException](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.exceptions/InvalidPasswordException) is thrown.

**advanced\_usage.loading\_documents.LoadPasswordProtectedDocument**

```java
LoadOptions loadOptions = new LoadOptions();                                                                                   
loadOptions.setPassword("P@$$w0rd");                                                                                           
// Specify an absolute or relative path to your document. Ex: @"C:\\Docs\\protected-document.docx"
String filePath = "protected-document.docx";                                                                           
Watermarker watermarker = new Watermarker(filePath, loadOptions);                                                              
                                                                                                                               
// use watermarker methods to manage watermarks in the document                                                                
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));                                          
                                                                                                                               
watermarker.add(watermark);                                                                                                    
                                                                                                                               
watermarker.save("protected-document.docx");                                                                          
                                                                                                                               
watermarker.close();                                                                                                         
```

## Load password-protected word processing document

The following example demontrates how to load an encrypted word processing document (DOC, DOCX etc) using the password.

**advanced\_usage.loading\_documents.LoadPasswordProtectedWordProcessingDocument**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                                       
loadOptions.setPassword("P@$$w0rd");                                                                                           
// Specify an absolute or relative path to your document. Ex: @"C:\\Docs\\protected-document.docx"
String filePath = "protected-document.docx";                                                                           
Watermarker watermarker = new Watermarker(filePath, loadOptions);                                                              
                                                                                                                               
// use watermarker methods to manage watermarks in the WordProcessing document                                                 
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));                                          
                                                                                                                               
watermarker.add(watermark);                                                                                                    
                                                                                                                               
watermarker.save("protected-document.docx");                                                                          
                                                                                                                               
watermarker.close();                                                                                                         

```

The following [LoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/LoadOptions) descendants use [setPassword](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/LoadOptions#setPassword(java.lang.String)) method:

*   [DiagramLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/DiagramLoadOptions)
*   [PdfLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PdfLoadOptions)
*   [PresentationLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationLoadOptions)
*   [SpreadsheetLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/SpreadsheetLoadOptions)
*   [WordProcessingLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingLoadOptions)

