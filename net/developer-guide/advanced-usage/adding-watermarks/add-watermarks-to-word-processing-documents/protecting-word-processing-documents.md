---
id: protecting-word-processing-documents
url: watermark/net/protecting-word-processing-documents
title: Protecting word processing documents
weight: 3
description: "This article explains how to protect as well as unprotect the Word documents."
keywords: unprotect the Word documents, Protecting word processing documents
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
Since version 18.6, GroupDocs.Watermark provides a simplified way of protecting the Word documents with the password. The API allows you to protect as well as unprotect the Word documents. The following protection types are supported:

* *AllowOnlyRevisions*: user can only add revision marks to the document.
* *AllowOnlyComments*: user can only modify comments in the document.
* *AllowOnlyFormFields*: user can only enter data in the form fields in the document.
* *ReadOnly*: no changes are allowed to the document.

The protection types are added to the [*WordProcessingProtectionType*](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.wordprocessing/wordprocessingprotectiontype) enum. Following code samples demonstrate how to protect and unprotect Word documents.

## Protecting a document

Following code sample [protects](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.wordprocessing/wordprocessingcontent/methods/protect) a Word document with the password.

**AdvancedUsage.AddingWatermarks.AddWatermarksToWordProcessing.WordProcessingProtectDocument**

```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.docx"
using (Watermarker watermarker = new Watermarker("document.docx", loadOptions))
{
    WordProcessingContent content = watermarker.GetContent<WordProcessingContent>();
    content.Protect(WordProcessingProtectionType.ReadOnly, "7654321");
    watermarker.Save("document.docx");
}
```

## Unprotecting a document

The following code sample shows how to [unprotect](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.wordprocessing/wordprocessingcontent/methods/unprotect) a Word document regardless of password.

**AdvancedUsage.AddingWatermarks.AddWatermarksToWordProcessing.WordProcessingUnProtectDocument**

```csharp
WordProcessingLoadOptions loadOptions = new WordProcessingLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.docx"
using (Watermarker watermarker = new Watermarker("document.docx", loadOptions))
{
    WordProcessingContent content = watermarker.GetContent<WordProcessingContent>();
    content.Unprotect();
    watermarker.Save("document.docx");
}
```

