---
id: locking-watermark-in-word-processing-document
url: watermark/java/locking-watermark-in-word-processing-document
title: Locking watermark in word processing document
weight: 1
description: "This article explains how to lock the watermarks in a Word document to restrict the editing in Java."
keywords: lock the watermarks, lock the watermarks in a Word document
productName: GroupDocs.Watermark for Java
hideChildren: False
---
There might be the case when you need to lock the watermarks in a Word document to restrict the editing. To deal with such cases, GroupDocs.Watermark provides 5 variants of locking Word document when adding watermark.

*   **AllowOnlyRevisions**: user can only add revision marks to the document.
*   **AllowOnlyComments**: user can only modify comments in the document.
*   **AllowOnlyFormFields**: the document is split into one-page sections and locked section with watermark is added between each two adjacent document sections.
*   **ReadOnly**: the entire document is read-only.
*   **ReadOnlyWithEditableContent**: the document is read-only, but all the content except the watermark is marked as editable.

[setLockType()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkBaseOptions#setLockType(int)) method has been added to [WordProcessingWatermarkBaseOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkBaseOptions) class (and all descendants) to set any of the above-mentioned lock types. [WordProcessingLockType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingLockType) enum is used to define the lock type. The following code samples show how to lock watermark in different scenarios.

## Adding watermark to all pages

This example uses [WordProcessingWatermarkPagesOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkPagesOptions) with empty setPageNumbers().

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingAddLockedWatermarkToAllPages**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
TextWatermark watermark = new TextWatermark("Watermark text", new Font("Arial", 19));                      
watermark.setForegroundColor(Color.getRed());                                                              
                                                                                                           
WordProcessingWatermarkPagesOptions options = new WordProcessingWatermarkPagesOptions();                   
options.setLocked(true);                                                                                   
options.setLockType(WordProcessingLockType.AllowOnlyFormFields);                                           
                                                                                                           
// To protect with password                                                                                
//options.setPassword("7654321");                                                                          
                                                                                                           
watermarker.add(watermark, options);                                                                       
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

## Adding watermark to particular pages

This example uses [WordProcessingWatermarkPagesOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkPagesOptions) calling setPageNumbers() with numbers of two pages.

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingAddLockedWatermarkToParticularPages**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
TextWatermark watermark = new TextWatermark("Watermark text", new Font("Arial", 19));                      
watermark.setForegroundColor(Color.getRed());                                                              
                                                                                                           
WordProcessingWatermarkPagesOptions options = new WordProcessingWatermarkPagesOptions();                   
options.setPageNumbers(new int[] { 1, 3 });                                                                
options.setLocked(true);                                                                                   
options.setLockType(WordProcessingLockType.AllowOnlyComments);                                             
                                                                                                           
// To protect with password                                                                                
//options.Password = "7654321";                                                                            
                                                                                                           
watermarker.add(watermark, options);                                                                       
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```

## Adding watermark to a section

This example uses [WordProcessingWatermarkSectionOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkSectionOptions) calling [setSectionIndex()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingWatermarkSectionOptions#setSectionIndex(int)).

**advanced\_usage.add\_watermarks\_to\_word\_processing.WordProcessingAddLockedWatermarkToSection**

```java
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();                                   
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.docx"
Watermarker watermarker = new Watermarker("document.docx", loadOptions);                          
                                                                                                           
TextWatermark watermark = new TextWatermark("Watermark text", new Font("Arial", 19));                      
watermark.setForegroundColor(Color.getRed());                                                              
                                                                                                           
WordProcessingWatermarkSectionOptions options = new WordProcessingWatermarkSectionOptions();               
options.setSectionIndex(0);                                                                                
options.setLocked(true);                                                                                   
options.setLockType(WordProcessingLockType.ReadOnlyWithEditableContent);                                   
                                                                                                           
// To protect with password                                                                                
//options.setPassword("7654321");                                                                          
                                                                                                           
watermarker.add(watermark, options);                                                                       
                                                                                                           
watermarker.save("document.docx");                                                               
                                                                                                           
watermarker.close();                                                                                       
```
