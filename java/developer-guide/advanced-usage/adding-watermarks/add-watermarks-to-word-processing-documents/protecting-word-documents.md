---
id: protecting-word-documents
url: watermark/java/protecting-word-documents
title: Protecting Word documents
weight: 4
description: "This article explains how to protect as well as unprotect the Word documents in Java."
keywords: unprotect the Word documents, Protecting word processing documents
productName: GroupDocs.Watermark for Java
hideChildren: False
---
Since version 18.6, GroupDocs.Watermark provides a simplified way of protecting the Word documents with the password. The API allows you to protect as well as unprotect the Word documents. The following protection types are supported:

*   *AllowOnlyRevisions*: user can only add revision marks to the document.
    
*   *AllowOnlyComments*: user can only modify comments in the document.
    
*   *AllowOnlyFormFields*: user can only enter data in the form fields in the document.
    
*   ReadOnly: no changes are allowed to the document.
    

The protection types are added to the [WordProcessingProtectionType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingProtectionType) enum. Following code samples demonstrate how to protect and unprotect Word documents.

## Protecting a document

Following code sample [protects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingContent#protect(int,%20java.lang.String)) a Word document with the password.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingProtectDocument**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                       
                                                                                                           
content.protect(WordProcessingProtectionType.ReadOnly, "7654321");                                         
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

## Unprotecting a document

The following code sample shows how to [unprotect](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WordProcessingContent#unprotect()) a Word document regardless of password.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingUnProtectDocument**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
WordProcessingContent content = watermarker.getContent(WordProcessingContent.class);                       
                                                                                                           
content.unprotect();                                                                                       
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```
