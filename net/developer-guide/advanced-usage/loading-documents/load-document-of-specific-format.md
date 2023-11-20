---
id: load-document-of-specific-format
url: watermark/net/load-document-of-specific-format
title: Load document of specific format
linkTitle: Of specific format
weight: 3
description: "This article explains how to load document of specific format."
keywords: load document,load document of specific format
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
The constructors [Watermarker(String)](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) and [Watermarker(Stream)](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/main) can load a document of any supported format. When you're loading a document, GroupDocs.Watermark automatically detects its type and creates an instance of the appropriate class. If document format is not supported, constructor throws [UnsupportedFileTypeException](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.exceptions/unsupportedfiletypeexception). If you need specify the format of a document to load, you can use constructors with [LoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options/loadoptions) parameter.

The following example demonstrates how to create a watermarker for the Spreadsheet document:

**AdvancedUsage.LoadingDocuments.LoadingDocumentOfSpecificFormat**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
string filePath = "spreadsheet.xlsx";
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
using (Watermarker watermarker = new Watermarker(filePath, loadOptions))
{
    // use watermarker methods to manage watermarks in the Spreadsheet document
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));
    watermarker.Add(watermark);
    watermarker.Save("spreadsheet.xlsx");
}

```

Any supported format family has the specific [LoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options/loadoptions) descendant:

| Format | LoadOptions descendant |
| --- | --- |
| Diagram | [DiagramLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.diagram/diagramloadoptions) |
| Email | [EmailLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.email/emailloadoptions) |
| Image | [ImageLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.image/imageloadoptions) |
| GIF Image | [GifImageLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.image/gifimageloadoptions) |
| TIFF Image | [TiffImageLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.image/tiffimageloadoptions) |
| PDF | [PdfLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.pdf/pdfloadoptions) |
| Presentation | [PresentationLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.presentation/presentationloadoptions) |
| Spreadsheet | [SpreadsheetLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetloadoptions) |
| WordProcessing | [WordProcessingLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.wordprocessing/wordprocessingloadoptions) |

