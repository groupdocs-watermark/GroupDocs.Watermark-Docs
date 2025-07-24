---
id: attachments-in-pdf-document
url: watermark/net/attachments-in-pdf-document
title: Attachments in PDF document
weight: 1
description: "This article explains how to work with PDF attachments while using GroupDocs watermarking API."
keywords: watermarking API, PDF attachments, Extract all attachments
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
## Extract all attachments from PDF document

GroupDocs.Watermark API allows you to extract [attachments](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.pdf/pdfcontent/properties/attachments) in PDF document. Following code performs this functionality.

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfExtractAllAttachments**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    PdfContent pdfContent = watermarker.GetContent<PdfContent>();
    foreach (PdfAttachment attachment in pdfContent.Attachments)
    {
        Console.WriteLine("Name: {0}", attachment.Name);
        Console.WriteLine("Description: {0}", attachment.Description);
        Console.WriteLine("File type: {0}", attachment.GetDocumentInfo().FileType);

        // Save the attached file on disk
        File.WriteAllBytes(Path.Combine("SampleFiles\Output", attachment.Name), attachment.Content);
    }
}
```

## Add an attachment to PDF document

The API also allows you to add attachments to the PDF document. Following code snippet shows how to remove an attachment

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfAddAttachment**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    PdfContent pdfContent = watermarker.GetContent<PdfContent>();

    // Add the attachment
    pdfContent.Attachments.Add(File.ReadAllBytes("sample.docx"), "sample doc", "sample doc as attachment");

    // Save changes
    watermarker.Save("document.pdf");
}
```

## Remove attachment from PDF document

The API also allows you to remove attachments from the PDF document. Following code snippet shows how to remove an attachment.

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfRemoveAttachment**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    PdfContent pdfContent = watermarker.GetContent<PdfContent>();
    for (int i = pdfContent.Attachments.Count - 1; i >= 0; i--)
    {
        PdfAttachment attachment = pdfContent.Attachments[i];

        // Remove all attached pdf files with a particular name
        if (attachment.Name.Contains("sample") && attachment.GetDocumentInfo().FileType == FileType.DOCX)
        {
            pdfContent.Attachments.RemoveAt(i);
        }
    }

    watermarker.Save("document.pdf");
}
```

## Search for images attachments

In case you want to search for all the images attachments in a PDF document, you can use GroupDocs.Watermark. Following code sample shows how to search images attachments of PDF document.

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfSearchImageInAttachment**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    // Consider only the attached images
    watermarker.SearchableObjects.PdfSearchableObjects = PdfSearchableObjects.AttachedImages;

    // Search for similar images
    WatermarkableImageCollection possibleWatermarks = watermarker.GetImages();
    Console.WriteLine("Found {0} image(s).", possibleWatermarks.Count);
}
```
