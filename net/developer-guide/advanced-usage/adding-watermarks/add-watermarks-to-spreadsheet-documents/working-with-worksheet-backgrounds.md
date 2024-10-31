---
id: working-with-worksheet-backgrounds
url: watermark/net/working-with-worksheet-backgrounds
title: Working with worksheet backgrounds
linkTitle: Working with backgrounds
weight: 3
description: "This article explains how to work with worksheet backgrounds while using GroupDocs watermarking API"
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
## Extracting information about all worksheet backgrounds in an excel document

The API allows you to extract [information](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.spreadsheet/spreadsheetworksheet/properties/backgroundimage) about all the worksheet backgrounds in an Excel document as shown in the following code sample.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetGetInformationOfWorksheetBackgrounds**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    SpreadsheetContent content = watermarker.GetContent<SpreadsheetContent>();
    foreach (SpreadsheetWorksheet worksheet in content.Worksheets)
    {
        if (worksheet.BackgroundImage != null)
        {
            Console.WriteLine(worksheet.BackgroundImage.Width);
            Console.WriteLine(worksheet.BackgroundImage.Height);
            Console.WriteLine(worksheet.BackgroundImage.GetBytes().Length);
        }
    }
}
```

## Removing a particular background

Following code sample can be used to remove the [background](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.spreadsheet/spreadsheetworksheet/properties/backgroundimage) of a particular worksheet.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetRemoveWorksheetBackground**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    SpreadsheetContent content = watermarker.GetContent<SpreadsheetContent>();
    content.Worksheets[0].BackgroundImage = null;

    watermarker.Save("spreadsheet.xlsx");
}
```

## Adding watermark to all backgrounds in an excel worksheet

You can [add](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.image/watermarkableimage/methods/add) watermark to the background images that belong to an Excel document as shown in the below code sample.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetAddWatermarkToBackgroundImages**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    // Initialize image or text watermark
    TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Center;
    watermark.RotateAngle = 45;
    watermark.SizingType = SizingType.ScaleToParentDimensions;
    watermark.ScaleFactor = 1;

    SpreadsheetContent content = watermarker.GetContent<SpreadsheetContent>();
    foreach (SpreadsheetWorksheet worksheet in content.Worksheets)
    {
        if (worksheet.BackgroundImage != null)
        {
            // Add watermark to the image
            worksheet.BackgroundImage.Add(watermark);
        }
    }

    watermarker.Save("spreadsheet.xlsx");
}
```

## Settings background image for charts

GroupDocs.Watermark for .NET also allows you to set the [background image](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.spreadsheet/spreadsheetchart/properties/imagefillformat) for a chart inside an Excel document. Following code sample shows how to achieve this functionality.

**AdvancedUsage.AddingWatermarks.AddWatermarksToSpreadsheets.SpreadsheetSetBackgroundImageForChart**

```csharp
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\spreadsheet.xlsx"
using (Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions))
{
    SpreadsheetContent content = watermarker.GetContent<SpreadsheetContent>();
    content.Worksheets[0].Charts[0].ImageFillFormat.BackgroundImage = 
        new SpreadsheetWatermarkableImage(File.ReadAllBytes("test.png"));
    content.Worksheets[0].Charts[0].ImageFillFormat.Transparency = 0.5;
    content.Worksheets[0].Charts[0].ImageFillFormat.TileAsTexture = true;

    watermarker.Save("spreadsheet.xlsx");
}
```

