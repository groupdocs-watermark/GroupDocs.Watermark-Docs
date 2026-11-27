---
id: customize
url: watermark/java/basic-usage/customize
title: Customize watermarks
weight: 4
description: This article shows how to adjust text or image watermarks to your needs.
keywords: rotate watermark, position watermark, move watermark, scale watermark, java
productName: GroupDocs.Watermark for Java
hideChildren: True
toc: true
---
GroupDocs.Watermark offers many capabilities to customize how the watermark would look and where it will be positioned within the document.

## Customizing text watermarks

To adjust a text watermark to your needs, use the methods of the [`TextWatermark`](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/textwatermark/) class and of its base class [`Watermark`](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/).

The following options could be set:

| Method | Description |
|--------|-------------|
|**[setBackgroundColor](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/textwatermark/#setBackgroundColor-com.groupdocs.watermark.watermarks.Color-)** | Specifies the background color of the text. |
|**[setConsiderParentMargins](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setConsiderParentMargins-boolean-)** | Whether to take into account the existing page margins of the document when calculating the watermark's size and coordinates. Default: false. |
|**[setFont](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/textwatermark/#setFont-com.groupdocs.watermark.watermarks.Font-)** | Specifies the current font of the text watermark. |
|**[setForegroundColor](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/textwatermark/#setForegroundColor-com.groupdocs.watermark.watermarks.Color-)** | Specifies the foreground color of the text. |
|**[setHeight](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setHeight-double-)** | Specifies the desired height of the watermark. |
|**[setHorizontalAlignment](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setHorizontalAlignment-int-)** | Specifies the horizontal alignment of the watermark. Takes a `HorizontalAlignment` constant: `None` (default), `Left`, `Center`, or `Right`. |
|**[setBackground](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setBackground-boolean-)** | Whether to place the watermark below (true) or above (false) the main content. Default: false. |
|**[setMargins](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setMargins-com.groupdocs.watermark.watermarks.Margins-)** | Specifies the watermark margins. |
|**[setOpacity](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setOpacity-double-)** | Defines the opacity of the watermark as a value ranging from 0 (fully transparent) to 1 (solid filling). Default: 1. |
|**[setRotateAngle](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setRotateAngle-double-)** | Defines the rotation angle of the watermark. A positive value corresponds to a clockwise rotation angle, negative - to a counterclockwise rotation angle. |
|**[setScaleFactor](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setScaleFactor-double-)** | Specifies how the watermark size depends on the size of a parent document. |
|**[setSizingType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setSizingType-int-)** | Specifies a way the watermark should be sized. Takes a `SizingType` constant: `Auto` (default), `Absolute`, `ScaleToParentDimensions`, or `ScaleToParentArea`. |
|**[setText](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/textwatermark/#setText-java.lang.String-)** | Defines the text of the watermark. |
|**[setTextAlignment](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/textwatermark/#setTextAlignment-int-)** | Specifies the alignment of text. Takes a `TextAlignment` constant: `Left` (default), `Center`, `Right`, or `Justify`. |
|**`setTileOptions`** | Repeats the watermark across the page. See [Adding repeated watermarks]({{< ref "watermark/java/developer-guide/basic-usage/adding-repeated-watermarks.md" >}}). |
|**[setVerticalAlignment](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setVerticalAlignment-int-)** | Specifies the vertical alignment of the watermark. Takes a `VerticalAlignment` constant: `None` (default), `Top`, `Center`, or `Bottom`. |
|**[setWidth](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setWidth-double-)** | Specifies the desired width of the watermark. |
|**[setX](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setX-double-)** | Specifies the horizontal coordinate of the watermark within the parent document. |
|**[setY](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setY-double-)** | Specifies the vertical coordinate of the watermark within the parent document. |

The code below demonstrates how to specify the desired watermark appearance and position before applying it to the document:

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.common.HorizontalAlignment;
import com.groupdocs.watermark.common.VerticalAlignment;
import com.groupdocs.watermark.watermarks.Color;
import com.groupdocs.watermark.watermarks.Font;
import com.groupdocs.watermark.watermarks.FontStyle;
import com.groupdocs.watermark.watermarks.SizingType;
import com.groupdocs.watermark.watermarks.TextWatermark;

// Specify an absolute or relative path to your document.
try (Watermarker watermarker = new Watermarker("C:\\Docs\\sample.docx")) {
    // Specify the desired text and font for the watermark
    TextWatermark watermark = new TextWatermark("Customized watermark.",
            new Font("Arial", 24, FontStyle.Bold));
    // Specify the appearance and the position of the watermark
    watermark.setForegroundColor(Color.getDarkOrange());
    watermark.setConsiderParentMargins(true);
    watermark.setHorizontalAlignment(HorizontalAlignment.Center);
    watermark.setVerticalAlignment(VerticalAlignment.Top);
    watermark.setSizingType(SizingType.ScaleToParentDimensions);
    watermark.setRotateAngle(45);
    watermark.setScaleFactor(0.7);
    // Apply the watermark
    watermarker.add(watermark);
    // Save the resulting document
    watermarker.save("C:\\Docs\\watermarked-sample.docx");
}
```

Run the program. A watermark will be added at a specified position and will have the specified look.

![Customized text watermark](/watermark/net/images/watermarking/custom-text-watermark.png)

## Customizing image watermarks

Image watermarks have similar settings that affect their look and position. To adjust an image watermark, use the methods that the [`ImageWatermark`](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/imagewatermark/) class inherits from the [`Watermark`](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/) class.

The following options could be set:

| Method | Description |
|--------|-------------|
|**[setConsiderParentMargins](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setConsiderParentMargins-boolean-)** | Whether to take into account the existing page margins of the document when calculating the watermark's size and coordinates. Default: false. |
|**[setHeight](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setHeight-double-)** | Specifies the desired height of the watermark. |
|**[setHorizontalAlignment](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setHorizontalAlignment-int-)** | Specifies the horizontal alignment of the watermark. Takes a `HorizontalAlignment` constant: `None` (default), `Left`, `Center`, or `Right`. |
|**[setBackground](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setBackground-boolean-)** | Whether to place the watermark below (true) or above (false) the main content. Default: false. |
|**[setMargins](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setMargins-com.groupdocs.watermark.watermarks.Margins-)** | Specifies the watermark margins. |
|**[setOpacity](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setOpacity-double-)** | Defines the opacity of the watermark as a value ranging from 0 (fully transparent) to 1 (solid filling). Default: 1. |
|**[setRotateAngle](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setRotateAngle-double-)** | Defines the rotation angle of the watermark. A positive value corresponds to a clockwise rotation angle, negative - to a counterclockwise rotation angle. |
|**[setScaleFactor](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setScaleFactor-double-)** | Specifies how the watermark size depends on the size of a parent document. |
|**[setSizingType](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setSizingType-int-)** | Specifies a way the watermark should be sized. Takes a `SizingType` constant: `Auto` (default), `Absolute`, `ScaleToParentDimensions`, or `ScaleToParentArea`. |
|**`setTileOptions`** | Repeats the watermark across the page. See [Adding repeated watermarks]({{< ref "watermark/java/developer-guide/basic-usage/adding-repeated-watermarks.md" >}}). |
|**[setVerticalAlignment](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setVerticalAlignment-int-)** | Specifies the vertical alignment of the watermark. Takes a `VerticalAlignment` constant: `None` (default), `Top`, `Center`, or `Bottom`. |
|**[setWidth](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setWidth-double-)** | Specifies the desired width of the watermark. |
|**[setX](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setX-double-)** | Specifies the horizontal coordinate of the watermark within the parent document. |
|**[setY](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setY-double-)** | Specifies the vertical coordinate of the watermark within the parent document. |

The code below demonstrates how to specify the desired watermark appearance and position before applying it to the document:

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.common.HorizontalAlignment;
import com.groupdocs.watermark.common.VerticalAlignment;
import com.groupdocs.watermark.watermarks.ImageWatermark;

// Specify an absolute or relative path to your document
// and to the watermark image.
try (Watermarker watermarker = new Watermarker("C:\\Docs\\seagull.jpg");
     ImageWatermark watermark = new ImageWatermark("C:\\Docs\\greetings-stamp.png")) {
    // Specify watermark position, rotation and opacity
    watermark.setHorizontalAlignment(HorizontalAlignment.Right);
    watermark.setVerticalAlignment(VerticalAlignment.Top);
    watermark.setRotateAngle(15);
    watermark.setBackground(false);
    watermark.setOpacity(0.8);
    // Apply the watermark
    watermarker.add(watermark);
    // Save the resulting document
    watermarker.save("C:\\Docs\\custom-image-watermark.jpg");
}
```

Run the program. An image watermark will be added at a specified position.

![Customized image watermark](/watermark/net/images/watermarking/custom-image-watermark.jpg)
