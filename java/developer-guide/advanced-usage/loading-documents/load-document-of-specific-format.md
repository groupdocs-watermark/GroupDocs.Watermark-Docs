---
id: load-document-of-specific-format
url: watermark/java/load-document-of-specific-format
title: Load document of specific format
weight: 3
description: "This article explains how to load document of specific format."
keywords: load document,load document of specific format
productName: GroupDocs.Watermark for Java
hideChildren: False
---
The constructors [Watermarker(String)](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#Watermarker(java.lang.String)) and [Watermarker(InputStream)](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#Watermarker(java.io.InputStream)) can load a document of any supported format. When you're loading a document, GroupDocs.Watermark automatically detects its type and creates an instance of the appropriate class. If document format is not supported, constructor throws [UnsupportedFileTypeException](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.exceptions/UnsupportedFileTypeException). If you need specify the format of a document to load, you can use constructors with [LoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/LoadOptions) parameter.

The following examle demonstrates how to create a watermarker for the Spreadsheet document:

**advanced\_usage.loading\_documents.LoadingDocumentOfSpecificFormat**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\spreadsheet.xlsx"
String filePath = "spreadsheet.xlsx";                                                                    
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();                                                
Watermarker watermarker = new Watermarker(filePath, loadOptions);                                                 
                                                                                                                  
// use watermarker methods to manage watermarks in the Spreadsheet document                                       
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));                             
                                                                                                                  
watermarker.add(watermark);                                                                                       
                                                                                                                  
watermarker.save("spreadsheet.xlsx");                                                                   
                                                                                                                  
watermarker.close();                                                                                            

```

Any supported format family has the specific [LoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/LoadOptions) descendant:

| Format | LoadOptions descendant |
| --- | --- |
| Diagram | [DiagramLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/DiagramLoadOptions) |
| Email | [EmailLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/EmailLoadOptions) |
| Image | [ImageLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/ImageLoadOptions) |
| GifImage | [GifImageLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/GifImageLoadOptions) |
| TiffImage | [TiffImageLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/TiffImageLoadOptions) |
| PDF | [PdfLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PdfLoadOptions) |
| Presentation | [PresentationLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/PresentationLoadOptions) |
| Spreadsheet | [SpreadsheetLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/SpreadsheetLoadOptions) |
| WordProcessing | [WordProcessingLoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/WordProcessingLoadOptions) |


