---
id: groupdocs-watermark-for-net-22-12-release-notes
url: watermark/net/groupdocs-watermark-for-net-22-12-release-notes
title: GroupDocs.Watermark for .NET 22.12 Release Notes
weight: 2
description: ""
keywords: 
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
{{< alert style="info" >}}This page contains release notes for GroupDocs.Watermark for .NET 22.12{{< /alert >}}

## Major features

There are the following enhancements in this release:

* Implemented Padding property in TextWatermark class for image files
* Implement support for .NET 6.0

## Full List of Issues Covering all Changes in this Release

| Key | Summary | Issue Type |
| --- | --- | --- |
| WATERMARKNET-1392 | Implemented Padding property in TextWatermark class for image files | Enhancement |
| WATERMARKNET-1380 | Implement support for .NET 6.0 | Enhancement |

## Public API and Backward Incompatible Changes

{{< alert style="info" >}}This section lists public API changes that were introduced in GroupDocs.Watermark for .NET 22.12.
It includes not only new and obsoleted public methods, but also a description of any changes in the behavior behind the scenes in GroupDocs.Watermark which may affect existing code.
Any behavior introduced that could be seen as a regression and modifies existing behavior is especially important and is documented here.{{< /alert >}}

### Implemented Padding property in TextWatermark class for image files

This enhancement allows you to set the paddings of text watermarks, separately on the left, top, right and bottom when adding to images.
Also the enhancement provides a method to calculate the paddings automatically so that the top and bottom margins are visually equal.

##### Public API changes

Class **Thickness** has been added to **GroupDocs.Watermark.Watermarks** namespace.  
Property **Double Bottom** has been added to **GroupDocs.Watermark.Watermarks.Thickness** class.  
Property **Double Left** has been added to **GroupDocs.Watermark.Watermarks.Thickness** class.  
Property **Double Right** has been added to **GroupDocs.Watermark.Watermarks.Thickness** class.  
Property **Double Top** has been added to **GroupDocs.Watermark.Watermarks.Thickness** class.  
Constructor **Thickness(Double, Double, Double, Double)** has been added to **GroupDocs.Watermark.Watermarks.Thickness** class.  
Constructor **Thickness(Double)** has been added to **GroupDocs.Watermark.Watermarks.Thickness** class.

Property **GroupDocs.Watermark.Watermarks.Thickness Padding** has been added to **GroupDocs.Watermark.Watermarks.TextWatermark** class.

##### Use cases

The following example demonstrates the use of padding.

```csharp
string inputFilePath = "InputImage.jpg";
string outputFilePath = "OutputImage.jpg";
string watermarkText = "TOP SECRET";

using (Watermarker watermarker = new Watermarker(File.OpenRead(inputFilePath)))
{
    TextWatermark textWatermark = new TextWatermark(watermarkText, new Font("Arial", 81));
    textWatermark.X = 500;
    textWatermark.Y = 200;
    textWatermark.Width = 300;
    textWatermark.Height = 50;
    textWatermark.BackgroundColor = Color.White;
    textWatermark.Opacity = 0.6;
    textWatermark.SizingType = SizingType.Absolute;
    textWatermark.Padding = new Thickness(0, 0, 4, 0);

    watermarker.Add(textWatermark);
    watermarker.Save(outputFilePath);
}
```

### Implement support for .NET 6.0

This enhancement implements the ability to use the library and API on the .NET 6.0 platform.

##### Public API changes

None

##### Use cases

None
