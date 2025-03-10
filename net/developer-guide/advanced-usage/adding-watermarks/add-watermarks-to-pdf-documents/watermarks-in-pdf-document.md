---
id: watermarks-in-pdf-document
url: watermark/net/watermarks-in-pdf-document
title: Watermarks in PDF document
weight: 4
description: Learn about how many ways the Groupdocs.watermark can add watermarks in PDF documents.
keywords: Watermarks in PDF, watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---

Learn about how many ways the Groupdocs.watermark can add watermarks in PDF documents.

## XObjects

When *[Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/add)* method of *[Watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker)* class is called, simple XObject is added to a PDF document.

{{< alert style="info" >}}
**PDF Reference 1.7**  

An external object (commonly called an XObject) is a graphics object whose contents are defined by a self-contained content stream, separate from the content stream in which it is used. There are three types of external objects:

* An image XObject represents a sampled visual image such as a photograph.
* A form XObject is a self-contained description of an arbitrary sequence of graphics objects.
* A PostScript XObject contains a fragment of code expressed in the PostScript page description language. PostScript XObjects are no longer recommended.
{{< /alert >}}

Image XObject and Form XObject are used by GroupDocs.Watermark API to add [ImageWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/imagewatermark) and [TextWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark) respectively. XObjects are considered as a page real content, therefore, they are not removed by Adobe Acrobat during document sanitization.

## Artifacts

{{< alert style="info" >}}
**PDF Reference 1.7**
The graphics objects in a document can be divided into two classes:

* The real content of a document comprises objects representing material originally introduced by the document’s author.
* Artifacts are graphics objects that are typically not part of the author’s original content but rather are generated by the PDF producer application in the course of pagination, layout, or other strictly mechanical processes. Artifacts may also be used to describe areas of the document where the author uses a graphical background, with the goal of enhancing the visual experience. In such a case, the background is not required for understanding the content.
{{< /alert >}}

According to artifact definition, the watermark can be represented by an artifact in a PDF document. The following example shows how artifact watermark can be added to a document with GroupDocs.Watermark using [PdfArtifactWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.pdf/pdfartifactwatermarkoptions).

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfAddArtifactWatermark**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    PdfArtifactWatermarkOptions options = new PdfArtifactWatermarkOptions();
    // Add text watermark
    TextWatermark textWatermark = new TextWatermark("This is an artifact watermark", 
        new Font("Arial", 8));
    textWatermark.HorizontalAlignment = HorizontalAlignment.Right;
    watermarker.Add(textWatermark, options);
    // Add image watermark
    using (ImageWatermark imageWatermark = new ImageWatermark("logo.bmp"))
    {
        watermarker.Add(imageWatermark, options);
    }
    watermarker.Save("document.pdf");
}
```

## Annotations

{{< alert style="info" >}}
**PDF Reference 1.7**
An annotation associates an object such as a note, sound, or movie with a location on a page of a PDF document, or provides a way to interact with the user by means of the mouse and keyboard. PDF includes a wide variety of standard annotation types.
A watermark annotation (PDF 1.6) is used to represent graphics that are expected to be printed at a fixed size and position on a page, regardless of the dimensions of the printed page.
{{< /alert >}}

Annotation is the third type of PDF entities by which a watermark can be represented. Use the following code snippet to add watermark annotation to a PDF document using [PdfAnnotationWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.pdf/pdfannotationwatermarkoptions).

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfAddAnnotationWatermark**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    PdfAnnotationWatermarkOptions options = new PdfAnnotationWatermarkOptions();
    // Add text watermark
    TextWatermark textWatermark = new TextWatermark("This is a annotation watermark", 
        new Font("Arial", 8));
    textWatermark.HorizontalAlignment = HorizontalAlignment.Left;
    textWatermark.VerticalAlignment = VerticalAlignment.Top;
    watermarker.Add(textWatermark, options);
    // Add image watermark
    using (ImageWatermark imageWatermark = new ImageWatermark("protect.jpg"))
    {
        imageWatermark.HorizontalAlignment = HorizontalAlignment.Right;
        imageWatermark.VerticalAlignment = VerticalAlignment.Top;
        watermarker.Add(imageWatermark, options);
    }

    watermarker.Save("document.pdf");
}
```

## Print-only annotations  

You can also add print only annotation watermark to the document setting [PrintOnly](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.pdf/pdfannotationwatermarkoptions/properties/printonly) property of [PdfAnnotationWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.pdf/pdfannotationwatermarkoptions). The following code demonstrates this approach.

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfAddPrintOnlyAnnotationWatermark**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    TextWatermark textWatermark = new TextWatermark("This is a print only test watermark. It won't appear in view mode.", new Font("Arial", 8));
    bool isPrintOnly = true;

    // Annotation will be printed, but not displayed in pdf viewing application
    PdfAnnotationWatermarkOptions options = new PdfAnnotationWatermarkOptions();
    options.PageIndex = 0;
    options.PrintOnly = isPrintOnly;

    watermarker.Add(textWatermark, options);
    watermarker.Save("document.pdf");
}
```
