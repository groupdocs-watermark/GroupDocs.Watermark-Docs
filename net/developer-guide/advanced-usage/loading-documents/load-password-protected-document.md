---
id: load-password-protected-document
url: watermark/net/load-password-protected-document
title: Load password-protected document
linkTitle: Password-protected document
weight: 4
description: "This article explains how to load password-protected document while using GroupDocs. Watermarks API."
keywords: load password-protected document
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
Some document formats also support content encryption. To load these type of documents you will have to provide the password. GroupDocs.Watermark API allows you to load content of these documents to manage watermark.

## Load password-protected document of any supported format

The following example demonstrates how to load an encrypted document of any supported format using the password. If the password is incorrect, [InvalidPasswordException](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.exceptions/invalidpasswordexception)is thrown.

**AdvancedUsage.LoadingDocuments.LoadPasswordProtectedDocument**

```csharp
LoadOptions loadOptions = new LoadOptions();
loadOptions.Password = "P@$$w0rd";
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\protected-document.docx"
string filePath = "protected-document.docx";
using (Watermarker watermarker = new Watermarker(filePath, loadOptions))
{
    // use watermarker methods to manage watermarks in the document
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));

    watermarker.Add(watermark);

    watermarker.Save("protected-document.docx");
}
```

## Load password-protected word processing document

The following example demontrates how to load an encrypted word processing document (DOC, DOCX etc) using the password.

**AdvancedUsage.LoadingDocuments.LoadPasswordProtectedWordProcessingDocument**

```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
loadOptions.Password = "P@$$w0rd";
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\protected-document.docx"
string filePath = "protected-document.docx";
using (Watermarker watermarker = new Watermarker(filePath, loadOptions))
{
    // use watermarker methods to manage watermarks in the WordProcessing document
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 12));
    watermarker.Add(watermark);
    watermarker.Save("protected-document.docx");
}

```

The following [LoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options/loadoptions) descendants use [Password](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options/loadoptions/properties/password) property:

* [DiagramLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.diagram/diagramloadoptions)
* [PdfLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.pdf/pdfloadoptions)
* [PresentationLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.presentation/presentationloadoptions)
* [SpreadsheetLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetloadoptions)
* [WordProcessingLoadOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.wordprocessing/wordprocessingloadoptions)
