---
id: rotate
url: watermark/net/basic-usage/customize
title: Customize watermarks
weight: 4
description: This article shows how to adjust text or image watermarks to your needs.
keywords: rotate watermark, position watermark, move watermark, scale watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
GroupDocs.Watermark offers many capabilities to customize how the watermark would look and where it will be positioned within the document.

## Customizing text watermarks

To adjust a text watermark to your needs, use the properties of the [`TextWatermark`](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/textwatermark/#properties) class. 

The following options could be set:
| Option | Description |
|--------|-------------|
|**[BackgroundColor](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/textwatermark/backgroundcolor)** | Specifies the background color of the text. |
|**[ConsiderParentMargins](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/considerparentmargins)** | Whether to take into account the existing page margins of the document when calculating the watermark's size and coordinates. Default: false.|
|**[Font](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/textwatermark/font)** | Specifies the current font of the text watermark. |
|**[ForegroundColor](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/textwatermark/foregroundcolor)** | Specifies the foreground color of the text. |
|**[Height](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/height)** | Specifies the desired height of the watermark. |
|**[HorizontalAlignment](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/horizontalalignment)** | Specifies the horizontal alignment of the watermark. Possible values are `None` (default), `Left`, `Center`, and `Right`.|
|**[IsBackground](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/isbackground)** | Whether to place the watermark below (true) or above (true) the main content. Default: false. |
|**[Margins](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/margins)** | Specifies the watermark margins. |
|**[Opacity](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/opacity)** | Defines the opacity of the watermark as a value ranging from 0 (fully transparent) to 1 (solid filling). |
|**[RotateAngle](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/rotateangle/)** | Defines the rotation angle of the watermark. A positive value corresponds to a clockwise rotation angle, negative - to a counterclockwise rotation angle. |
|**[ScaleFactor](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/scalefactor)** | Specifies how the watermark size depends on the size of a parent document. |
|**[SizingType](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/sizingtype)** | Specifies a way the watermark should be sized. Possible values are `Auto` (default), `Absolute`, `ScaleToParentDimensions`, and `ScaleToParentArea`. |
|**[Text](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/textwatermark/text)** | Defines the text of the watermark. |
|**[TextAlignment](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/textwatermark/textalignment)** | Specifies the alignment of text. Possible values are `Left` (default), `Center`, `Right`, and `Justify`.  |
|**[VerticalAlignment](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/verticalalignment)** | Specifies the vertical alignment of the watermark. Possible values are `None` (default), `Left`, `Center`, and `Bottom`. |
|**[Width](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/width)** | Specifies the desired width of the watermark. |
|**[X](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/x)** | Specifies the horizontal coordinate of the watermark within the parent document. |
|**[Y](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/y)** | Specifies the vertical coordinate of the watermark within the parent document. |


The code below demonstrates how to specify the desired watermark appearance and position before applying it to the document:

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Common;
using GroupDocs.Watermark.Watermarks;

// Specify an absolute or relative path to your document.
using (Watermarker watermarker = new Watermarker("C:\\Docs\\sample.docx"))
{
    // Specify the desired text and font for the watermark
    TextWatermark watermark = new TextWatermark("Customized watermark.", 
        new Font("Arial", 24, FontStyle.Bold));
    // Specify the appearance and the position of the watermark
    watermark.ForegroundColor = Color.DarkOrange;
    watermark.ConsiderParentMargins = true;
    watermark.HorizontalAlignment = HorizontalAlignment.Center;
    watermark.VerticalAlignment = VerticalAlignment.Top;
    watermark.SizingType = SizingType.ScaleToParentDimensions;
    watermark.RotateAngle = 45;
    watermark.ScaleFactor = 0.7;
    // Apply the watermark
    watermarker.Add(watermark);
    // Save the resulting document
    watermarker.Save("C:\\Docs\\watermarked-sample.docx");
}
```
Run the program. A watermark will be added at a specified position and will have the specified look.

![Customized text watermark](/watermark/net/images/watermarking/custom-text-watermark.png)

## Customizing image watermarks

Image watermarks have similar settings that affect their look and position. To adjust an image watermark, use the properties of the [`ImageWatermark`](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/imagewatermark/#properties) class. 

The following options could be set:
| Option | Description |
|--------|-------------|
|**[ConsiderParentMargins](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/considerparentmargins)** | Whether to take into account the existing page margins of the document when calculating the watermark's size and coordinates. Default: false.|
|**[Height](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/height)** | Specifies the desired height of the watermark. |
|**[HorizontalAlignment](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/horizontalalignment)** | Specifies the horizontal alignment of the watermark. Possible values are `None` (default), `Left`, `Center`, and `Right`.|
|**[IsBackground](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/isbackground)** | Whether to place the watermark below (true) or above (true) the main content. Default: false. |
|**[Margins](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/margins)** | Specifies the watermark margins. |
|**[Opacity](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/opacity)** | Defines the opacity of the watermark as a value ranging from 0 (fully transparent) to 1 (solid filling). |
|**[RotateAngle](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/rotateangle/)** | Defines the rotation angle of the watermark. A positive value corresponds to a clockwise rotation angle, negative - to a counterclockwise rotation angle. |
|**[ScaleFactor](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/scalefactor)** | Specifies how the watermark size depends on the size of a parent document. |
|**[SizingType](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/sizingtype)** | Specifies a way the watermark should be sized. Possible values are `Auto` (default), `Absolute`, `ScaleToParentDimensions`, and `ScaleToParentArea`. |
|**[VerticalAlignment](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/verticalalignment)** | Specifies the vertical alignment of the watermark. Possible values are `None` (default), `Left`, `Center`, and `Bottom`. |
|**[Width](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/width)** | Specifies the desired width of the watermark. |
|**[X](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/x)** | Specifies the horizontal coordinate of the watermark within the parent document. |
|**[Y](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermark/y)** | Specifies the vertical coordinate of the watermark within the parent document. |


The code below demonstrates how to specify the desired watermark appearance and position before applying it to the document:

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Common;
using GroupDocs.Watermark.Watermarks;

// Specify an absolute or relative path to your document.
using (Watermarker watermarker = new Watermarker("C:\\Docs\\seagull.jpg"))
{
    // Specify the desired text and font for the watermark
    ImageWatermark watermark = new ImageWatermark("C:\\Docs\\greetings-stamp.png");
    // Specify watermark position, rotation and opacity
    watermark.HorizontalAlignment = HorizontalAlignment.Right;
    watermark.VerticalAlignment = VerticalAlignment.Top;
    watermark.RotateAngle = 15;
    watermark.IsBackground = false;
    watermark.Opacity = 0.8;
    // Apply the watermark
    watermarker.Add(watermark);
    // Save the resulting document
    watermarker.Save("C:\\Docs\\custom-image-watermark.jpg");
}
```
Run the program. An image watermark will be added at a specified position.

![Customized image watermark](/watermark/net/images/watermarking/custom-image-watermark.jpg)

