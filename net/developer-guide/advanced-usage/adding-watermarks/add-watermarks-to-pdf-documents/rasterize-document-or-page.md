---
id: rasterize-document-or-page
url: watermark/net/rasterize-document-or-page
title: Rasterize document or page
weight: 3
description: The watermark can be removed from the PDF documents using third-party tools. However, if you want to remove a watermark that is almost impossible to remove, you can rasterize pdf documents. GroupDocs.Watermark provides the feature to convert all the pages of a PDF document to raster images with only one line of code.
keywords: remove a watermark, watermark, rasterize pdf
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
## How to remove a watermark from a pdf 
The watermark can be removed from the PDF documents using third-party tools. However, if you want to remove a watermark that is almost impossible to remove, you can rasterize pdf documents. GroupDocs.Watermark provides the feature to convert all the pages of a PDF document to raster images with only one line of code.

## Rasterize PDF document

Following code snippet is used to [rasterize](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.pdf/pdfcontent/methods/rasterize) the PDF document to protect added watermarks.  

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfRasterizeDocument**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    // Initialize image or text watermark
    TextWatermark watermark = new TextWatermark("Do not copy", new Font("Arial", 8));
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    watermark.RotateAngle = 45;
    watermark.SizingType = SizingType.ScaleToParentDimensions;
    watermark.ScaleFactor = 1;
    watermark.Opacity = 0.5;

    // Add watermark of any type first
    watermarker.Add(watermark);
    PdfContent pdfContent = watermarker.GetContent<PdfContent>();

    // Rasterize all pages
    pdfContent.Rasterize(100, 100, PdfImageConversionFormat.Png);

    // Content of all pages is replaced with raster images
    watermarker.Save("document.pdf");
}
```

{{< alert style="warning" >}}You can't restore document content after saving the document. Rasterization significantly increases the size of the resultant PDF file.{{< /alert >}}

## Rasterize particular page of the PDF document

The API also allows you to [rasterize](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.pdf/pdfpage/methods/rasterize) any particular page of the PDF document. Following code snippet is used to rasterize a page of the PDF document.

**AdvancedUsage.AddingWatermarks.AddWatermarksToPdf.PdfRasterizePage**

```csharp
PdfLoadOptions loadOptions = new PdfLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf", loadOptions))
{
    // Initialize image or text watermark
    TextWatermark watermark = new TextWatermark("Do not copy", new Font("Arial", 8));
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    watermark.RotateAngle = 45;
    watermark.SizingType = SizingType.ScaleToParentDimensions;
    watermark.ScaleFactor = 1;
    watermark.Opacity = 0.5;

    // Add watermark of any type first
    PdfArtifactWatermarkOptions options = new PdfArtifactWatermarkOptions();
    options.PageIndex = 0;
    watermarker.Add(watermark, options);

    // Rasterize the first page
    PdfContent pdfContent = watermarker.GetContent<PdfContent>();
    pdfContent.Pages[0].Rasterize(100, 100, PdfImageConversionFormat.Png);

    // Content of the first page is replaced with raster image
    watermarker.Save("document.pdf");
}
```

