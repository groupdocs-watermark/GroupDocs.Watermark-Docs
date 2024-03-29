---
id: add-watermarks-to-diagram-documents
url: watermark/net/add-watermarks-to-diagram-documents
title: Add watermarks to diagram documents
linkTitle: To diagrams
weight: 3
description: "Using GroupDocs.Watermark, you can add watermark to all pages of a particular type in a document. It consists of following steps."
keywords: add watermark, add watermark to all pages
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
## Adding watermark to all pages of a particular type

Using GroupDocs.Watermark, you can add watermark to all pages of a particular type in a document. It consists of following steps.

1. Load the document
2. Create and initialize watermark object
3. Set watermark properties
4. Add watermark by specifying page type using [PlacementType](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.diagram/diagramshapewatermarkoptions/properties/placementtype) of [DiagramShapeWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.diagram/diagramshapewatermarkoptions)
5. Save the document

Following code shows how to add watermark to a particular type of the pages.

**AdvancedUsage.AddingWatermarks.AdWatermarksToDiagrams.DiagramAddWatermarkToAllPagesOfParticularType**

```csharp
DiagramLoadOptions loadOptions = new DiagramLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\diagram.vsdx"
using (Watermarker watermarker = new Watermarker("diagram.vsdx", loadOptions))
{
    // Initialize text watermark
    TextWatermark textWatermark = new TextWatermark("Test watermark 1", new Font("Calibri", 19));
    DiagramShapeWatermarkOptions textWatermarkOptions = new DiagramShapeWatermarkOptions();
    textWatermarkOptions.PlacementType = DiagramWatermarkPlacementType.BackgroundPages;

    // Add text watermark to all background pages
    watermarker.Add(textWatermark, textWatermarkOptions);

    // Initialize image watermark
    using (ImageWatermark imageWatermark = new ImageWatermark("logo.jpg"))
    {
        DiagramShapeWatermarkOptions imageWatermarkOptions = new DiagramShapeWatermarkOptions();
        imageWatermarkOptions.PlacementType = DiagramWatermarkPlacementType.ForegroundPages;

        // Add image watermark to all foreground pages
        watermarker.Add(imageWatermark, imageWatermarkOptions);
    }

    watermarker.Save("diagram.vsdx");
}
```

## Adding watermark on separate background page

In some cases, you may want to place the watermark on separate newly created background pages. In this case, use below code.

**AdvancedUsage.AddingWatermarks.AddWatermarksToDiagrams.DiagramAddWatermarkToSeparateBackgroundPage**

```csharp
DiagramLoadOptions loadOptions = new DiagramLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\diagram.vsdx"
using (Watermarker watermarker = new Watermarker("diagram.vsdx", loadOptions))
{
    // Initialize watermark of any supported type
    TextWatermark textWatermark = new TextWatermark("Test watermark 1", new Font("Calibri", 19));

    DiagramShapeWatermarkOptions options = new DiagramShapeWatermarkOptions();
    options.PlacementType = DiagramWatermarkPlacementType.SeparateBackgrounds;

    // Create separate background for each page where it is not set. Add watermark to it.
    watermarker.Add(textWatermark, options);
    watermarker.Save("diagram.vsdx");
}
```

## Add watermark to a particular page

GroupDocs.Watermark allows you to add watermark to a particular page of the document using [PageIndex](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.diagram/diagrampagewatermarkoptions/properties/pageindex) of [DiagramPageWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.diagram/diagrampagewatermarkoptions) as shown in below example.

**AdvancedUsage.AddingWatermarks.AddWatermarksToDiagrams.DiagramAddWatermarkToParticularPage**

```csharp
DiagramLoadOptions loadOptions = new DiagramLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\diagram.vsdx"
using (Watermarker watermarker = new Watermarker("diagram.vsdx", loadOptions))
{
    TextWatermark textWatermark = new TextWatermark("Test watermark", new Font("Calibri", 19));
    DiagramPageWatermarkOptions textWatermarkOptions = new DiagramPageWatermarkOptions();
    textWatermarkOptions.PageIndex = 0;

    // Add text watermark to the first page
    watermarker.Add(textWatermark, textWatermarkOptions);
    using (ImageWatermark imageWatermark = new ImageWatermark("logo.jpg"))
    {
        DiagramPageWatermarkOptions imageWatermarkOptions = new DiagramPageWatermarkOptions();
        imageWatermarkOptions.PageIndex = 1;
        // Add image watermark to the second page
        watermarker.Add(imageWatermark, imageWatermarkOptions);
    }

    watermarker.Save("diagram.vsdx");
}
```

## Lock watermark

When you're calling [Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/add/methods/1) method of [Watermaker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker) object created for the Diagram document, simple shape is added to the document. There is no difference between added watermark and Visio shapes that are used to create diagrams.

GroupDocs.Watermark allows you to protect watermark from editing in MS Visio by setting [IsLocked](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.diagram/diagramwatermarkoptions/properties/islocked) property of [DiagramShapeWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.diagram/diagramshapewatermarkoptions) (as shown in the following example).

**AdvancedUsage.AddingWatermarks.AddWatermarksToDiagrams.DiagramLockWatermarkShape**

```csharp
DiagramLoadOptions loadOptions = new DiagramLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\diagram.vsdx"
using (Watermarker watermarker = new Watermarker("diagram.vsdx", loadOptions))
{
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));

    DiagramShapeWatermarkOptions options = new DiagramShapeWatermarkOptions();
    options.IsLocked = true;

    // Editing of the shape in Visio is forbidden
    watermarker.Add(watermark, options);

    watermarker.Save("diagram.vsdx");
}
```

## Advanced use cases

* [Existing objects in diagram document]({{< ref "existing-objects-in-diagram-document" >}} "Existing objects in diagram document")
