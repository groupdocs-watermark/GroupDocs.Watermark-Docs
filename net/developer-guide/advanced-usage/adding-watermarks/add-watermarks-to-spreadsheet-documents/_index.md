---
id: add-watermarks-to-spreadsheet-documents
url: watermark/net/add-watermarks-to-spreadsheet-documents
title: Add watermarks to spreadsheet documents
linkTitle: To spreadsheets
weight: 8
description: "GroupDocs.Watermark provides an easy way to add watermark to the worksheets of any Excel document."
keywords: add watermark, add watermark to the worksheets, Adding watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
## Adding watermark to a particular worksheet

GroupDocs.Watermark provides an easy way to add watermark to the worksheets of any Excel document. Adding watermark to a particular Excel worksheet using GroupDocs.Watermark consists of following steps.

1. Load the document
2. Create and initialize watermark object
3. Set watermark properties
4. Create a [SpreadsheetWatermarkShapeOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkshapeoptions) class and set the [WorksheetIndex](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkshapeoptions/properties/worksheetindex) property
5. Add watermark to the worksheet
6. Save the document

Following code shows how to add watermark to a particular worksheet.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddWatermarkToWorksheet**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    // Add text watermark to the first worksheet
    TextWatermark textWatermark = new TextWatermark("Test watermark", new Font("Arial", 8));
    SpreadsheetWatermarkShapeOptions textWatermarkOptions = new SpreadsheetWatermarkShapeOptions();
    textWatermarkOptions.WorksheetIndex = 0;
    watermarker.Add(textWatermark, textWatermarkOptions);

    // Add image watermark to the second worksheet
    using (ImageWatermark imageWatermark = new ImageWatermark("logo.jpg"))
    {
        SpreadsheetWatermarkShapeOptions imageWatermarkOptions = new SpreadsheetWatermarkShapeOptions();
        imageWatermarkOptions.WorksheetIndex = 1;
        watermarker.Add(imageWatermark, imageWatermarkOptions);
    }

    watermarker.Save("spreadsheet.xlsx");
}
```

## Getting size of content area

If for some reasons you want to use absolute sizing and positioning, you may also need to get the [width](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.spreadsheet/spreadsheetworksheet/properties/contentareawidth) and the [height](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.spreadsheet/spreadsheetworksheet/properties/contentareaheight) of the content area (range of cells which contains data).

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetGetContentAreaDimensions**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    SpreadsheetContent content = watermarker.GetContent<SpreadsheetContent>();

    // Get the size of content area
    Console.WriteLine(content.Worksheets[0].ContentAreaHeight);
    Console.WriteLine(content.Worksheets[0].ContentAreaWidth);

    // Get the size of particular cell
    Console.WriteLine(content.Worksheets[0].GetColumnWidth(0));
    Console.WriteLine(content.Worksheets[0].GetRowHeight(0));
}
```

## Adding watermark to the images from a particular worksheet

Using GroupDocs.Watermark, you can add watermark to the images that belong to a particular worksheet using the [FindImages()](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents/contentpart/methods/findimages) method of the [SpreadsheetWorksheet](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.spreadsheet/spreadsheetworksheet) class.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddWatermarkToWorksheetImages**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    watermark.RotateAngle = 45;
    watermark.SizingType = SizingType.ScaleToParentDimensions;
    watermark.ScaleFactor = 1;

    // Get all images from the first worksheet
    SpreadsheetContent content = watermarker.GetContent<SpreadsheetContent>();
    WatermarkableImageCollection images = content.Worksheets[0].FindImages();

    // Add watermark to all found images
    foreach (WatermarkableImage image in images)
    {
        image.Add(watermark);
    }

    watermarker.Save("spreadsheet.xlsx");
}
```

## Different types of watermark in excel documents

### Shapes

When you're calling [Add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/add/methods/1) method of [Watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker) class with [SpreadsheetWatermarkShapeOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkshapeoptions) parameter, simple shape is added to an Excel document. Besides [SpreadsheetWatermarkShapeOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkshapeoptions) there is [SpreadsheetWatermarkModernWordArtOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkmodernwordartoptions) type which is used only with [TextWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark). Both options add watermark to an Excel document as a shape, however, there are some differences. When [TextWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark) is added with [SpreadsheetWatermarkShapeOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkshapeoptions) there options, it looks and behaves like WordArt object added in Excel'2003, and [SpreadsheetWatermarkModernWordArtOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkmodernwordartoptions) option adds text watermark that looks and behaves like Excel'2013 WordArt object.

The code sample below shows how to add modern WordArt watermark to Excel document worksheet.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddModernWordArdWatermark**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    TextWatermark textWatermark = new TextWatermark("Test watermark", new Font("Arial", 8));
    SpreadsheetWatermarkModernWordArtOptions options = new SpreadsheetWatermarkModernWordArtOptions();
    options.WorksheetIndex = 0;

    watermarker.Add(textWatermark, options);
    watermarker.Save("spreadsheet.xlsx");
}
```

### Shape additional options

The API also provides the feature to set some additional options ([Name](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkbaseoptions/properties/name), [AlternativeText](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkbaseoptions/properties/alternativetext) and [IsLocked](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkbaseoptions/properties/islocked)) when adding shape watermark to Excel worksheet (as shown in the below sample).

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddWatermarkUsingShapeSettings**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Segoe UI", 19));
    SpreadsheetWatermarkShapeOptions options = new SpreadsheetWatermarkShapeOptions();

    // Set the shape name
    options.Name = "Shape 1";

    // Set the descriptive (alternative) text that will be associated with the shape
    options.AlternativeText = "Test watermark";

    // Editing of the shape in Excel is forbidden
    options.IsLocked = true;

    watermarker.Add(watermark, options);
    watermarker.Save("spreadsheet.xlsx");
}
```

### Text effects

You can also apply [text effects](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheettexteffects) when adding shape watermark in Excel worksheet as shown in below code sample.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddWatermarkWithTextEffects**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Segoe UI", 19));

    SpreadsheetTextEffects effects = new SpreadsheetTextEffects();
    effects.LineFormat.Enabled = true;
    effects.LineFormat.Color = Color.Red;
    effects.LineFormat.DashStyle = OfficeDashStyle.DashDotDot;
    effects.LineFormat.LineStyle = OfficeLineStyle.Triple;
    effects.LineFormat.Weight = 1;

    SpreadsheetWatermarkShapeOptions options = new SpreadsheetWatermarkShapeOptions();
    options.Effects = effects;

    watermarker.Add(watermark, options);
    watermarker.Save("spreadsheet.xlsx");
}
```

### Image effects

The API also allows you to apply [image effects](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetimageeffects) to the shape watermark using below code sample.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddWatermarkWithImageEffects**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    using (ImageWatermark watermark = new ImageWatermark("logo.png"))
    {
        SpreadsheetImageEffects effects = new SpreadsheetImageEffects();
        effects.Brightness = 0.7;
        effects.Contrast = 0.6;
        effects.ChromaKey = Color.Red;
        effects.BorderLineFormat.Enabled = true;
        effects.BorderLineFormat.Weight = 1;

        SpreadsheetWatermarkShapeOptions options = new SpreadsheetWatermarkShapeOptions();
        options.Effects = effects;

        watermarker.Add(watermark, options);
    }

    watermarker.Save("spreadsheet.xlsx");
}
```

### Worksheet backgrounds

[Microsoft Office documentation](https://support.office.com/en-us/article/Add-a-watermark-in-Excel-a372182a-d733-484e-825c-18ddf3edf009?ui=en-US&rs=en-US&ad=US&fromAR=1) says that Excel does not support adding of watermarks, however, it offers some workarounds. [One of them](https://support.office.com/en-us/article/Add-a-watermark-in-Excel-a372182a-d733-484e-825c-18ddf3edf009?ui=en-US&rs=en-US&ad=US&fromAR=1#odh_background) is using worksheet background images as watermarks.

Use the following code sample to add [background watermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetbackgroundwatermarkoptions) to all worksheets of Excel document.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddWatermarkAsBackground**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    using (ImageWatermark watermark = new ImageWatermark("logo.gif"))
    {
        SpreadsheetBackgroundWatermarkOptions options = new SpreadsheetBackgroundWatermarkOptions();
        watermarker.Add(watermark, options);
    }

    watermarker.Save("spreadsheet.xlsx");
}
```

{{< alert style="info" >}}Backgrounds are viewable in Normal View in the worksheet and are invisible in Page Layout mode. The image is automatically tiled on the background of the worksheet. Excel formats don't support background image customization. Using properties of image watermark (size, rotation etc) will cause image redrawing. This may lead to the decrease in performance.{{< /alert >}}

### Worksheet background image size

You can also define the size ([width](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetbackgroundwatermarkoptions/properties/backgroundwidth) and [height](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetbackgroundwatermarkoptions/properties/backgroundheight)) of the background image on which your watermark will be drawn. This feature allows you to mimic watermark relative size and position.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddWatermarkAsBackgroundWithRelativeSizeAndPosition**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    using (ImageWatermark watermark = new ImageWatermark("logo.gif"))
    {
        watermark.HorizontalAlignment = HorizontalAlignment.Center;
        watermark.VerticalAlignment = VerticalAlignment.Center;
        watermark.RotateAngle = 90;
        watermark.SizingType = SizingType.ScaleToParentDimensions;
        watermark.ScaleFactor = 0.5;

        SpreadsheetContent content = watermarker.GetContent<SpreadsheetContent>();
        SpreadsheetBackgroundWatermarkOptions options = new SpreadsheetBackgroundWatermarkOptions();
        options.BackgroundWidth = content.Worksheets[0].ContentAreaWidthPx; /* set background width */
        options.BackgroundHeight = content.Worksheets[0].ContentAreaHeightPx; /* set background height */

        watermarker.Add(watermark, options);
    }

    watermarker.Save("spreadsheet.xlsx");
}
```

{{< alert style="warning" >}}This method assumes that watermark absolute coordinates and size are measured in pixels (if they are assigned).{{< /alert >}}

### [TextWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark) as background

Excel does not support text backgrounds but you still can pass [TextWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark) instance with the [SpreadsheetBackgroundWatermarkOptions](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetbackgroundwatermarkoptions) option. The text will be converted to image preserving formatting. The following code sample demonstrates this feature.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddTextWatermarkAsBackground**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Segoe UI", 19));
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    watermark.RotateAngle = 45;
    watermark.SizingType = SizingType.ScaleToParentDimensions;
    watermark.ScaleFactor = 0.5;
    watermark.Opacity = 0.5;

    SpreadsheetContent content = watermarker.GetContent<SpreadsheetContent>();

    SpreadsheetBackgroundWatermarkOptions options = new SpreadsheetBackgroundWatermarkOptions();
    options.BackgroundWidth = content.Worksheets[0].ContentAreaWidthPx; /* set background width */
    options.BackgroundHeight = content.Worksheets[0].ContentAreaHeightPx; /* set background height */

    watermarker.Add(watermark, options);
    watermarker.Save("spreadsheet.xlsx");
}
```

### Header and footer image watermark

Another way to mimic watermark in Excel is to [use Headers and Footers](https://support.office.com/en-us/article/Add-a-watermark-in-Excel-a372182a-d733-484e-825c-18ddf3edf009?ui=en-US&rs=en-US&ad=US&fromAR=1). You can [add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.options.spreadsheet/spreadsheetwatermarkheaderfooteroptions) watermark to worksheet's header or footer using below code sample.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddImageWatermarkIntoHeaderFooter**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    using (ImageWatermark watermark = new ImageWatermark("logo.png"))
    {
        watermark.VerticalAlignment = VerticalAlignment.Top;
        watermark.HorizontalAlignment = HorizontalAlignment.Center;
        watermark.SizingType = SizingType.ScaleToParentDimensions;
        watermark.ScaleFactor = 1;

        SpreadsheetWatermarkHeaderFooterOptions options = new SpreadsheetWatermarkHeaderFooterOptions();
        options.WorksheetIndex = 0;

        watermarker.Add(watermark, options);
    }

    watermarker.Save("spreadsheet.xlsx");
}
```

### Header and footer text watermark

You can also add [text watermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark) in header or footer as shown in the below code sample.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddTextWatermarkIntoHeaderFooter**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Segoe UI", 19, FontStyle.Bold));
    watermark.ForegroundColor = Color.Red;
    watermark.BackgroundColor = Color.Aqua;
    watermark.VerticalAlignment = VerticalAlignment.Top;
    watermark.HorizontalAlignment = HorizontalAlignment.Center;

    SpreadsheetWatermarkHeaderFooterOptions options = new SpreadsheetWatermarkHeaderFooterOptions();
    options.WorksheetIndex = 0;

    watermarker.Add(watermark, options);
    watermarker.Save("spreadsheet.xlsx");
}
```

{{< alert style="warning" >}}You’ll see the watermark in Excel only when you’re in Page Layout view or Print Preview.{{< /alert >}}{{< alert style="warning" >}}Excel Headersand footers are not designed for watermarking, so, some features don't work for header and footer watermarks.{{< /alert >}}

## Advanced use cases

* [Shapes in spreadsheet document]({{< ref "shapes-in-spreadsheet-document" >}} "Shapes in spreadsheet document")
* [Working with spreadsheet document attachments]({{< ref "working-with-spreadsheet-document-attachments" >}} "Working with spreadsheet document attachments")
* [Working with worksheet backgrounds]({{< ref "working-with-worksheet-backgrounds" >}} "Working with worksheet backgrounds")
* [Working with worksheet headers and footers]({{< ref "working-with-worksheet-headers-and-footers" >}} "Working with worksheet headers and footers")

