---
id: adding-repeated-watermarks
url: watermark/java/adding-repeated-watermarks
title: Adding repeated watermarks
linkTitle: Repeated watermarks
weight: 3
description: "GroupDocs.Watermark for Java allows to add repeated or tiled watermarks to documents"
keywords: add repeated watermarks, tiled watermarks, java
productName: GroupDocs.Watermark for Java
hideChildren: True
toc: true
---

## Repeated watermark

A repeated (tiled) watermark fills the whole page with copies of a text or an image. Such a pattern is much harder to crop out or cover than a single watermark, so it suits both branding and document security. You can configure the spacing between the copies, their rotation and the layout of the pattern.

### Text repeated watermark

The code snippet below demonstrates how to add a tiled watermark to a document. To configure tiling, use the `TileOptions` class and pass it to the `setTileOptions` method of the watermark. In this example, the line spacing (the spacing between parallel rows of tiles) is 12 percent of the page size, and the watermark spacing (the spacing between watermarks in a row) is 10 percent of the page size. Both values are `MeasureValue` objects. The following image explains the purpose of the line spacing and watermark spacing settings:
![adding-repeated-watermarks](/watermark/net/images/tilling-options.png)

The watermark is also rotated by 30 degrees counterclockwise (a negative angle).

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.watermarks.Color;
import com.groupdocs.watermark.watermarks.Font;
import com.groupdocs.watermark.watermarks.FontStyle;
import com.groupdocs.watermark.watermarks.MeasureValue;
import com.groupdocs.watermark.watermarks.TextWatermark;
import com.groupdocs.watermark.watermarks.TileMeasureType;
import com.groupdocs.watermark.watermarks.TileOptions;

try (Watermarker watermarker = new Watermarker("sample.pdf")) {
    // Initialize the font to be used for watermark
    Font font = new Font("Arial", 19, FontStyle.Bold | FontStyle.Italic);

    // Create the watermark object
    TextWatermark watermark = new TextWatermark("Watermark", font);
    watermark.setForegroundColor(Color.getRed());

    // Configure tile options
    MeasureValue lineSpacing = new MeasureValue();
    lineSpacing.setMeasureType(TileMeasureType.Percent);
    lineSpacing.setValue(12);

    MeasureValue watermarkSpacing = new MeasureValue();
    watermarkSpacing.setMeasureType(TileMeasureType.Percent);
    watermarkSpacing.setValue(10);

    TileOptions tileOptions = new TileOptions();
    tileOptions.setLineSpacing(lineSpacing);
    tileOptions.setWatermarkSpacing(watermarkSpacing);
    watermark.setTileOptions(tileOptions);

    // Set watermark properties
    watermark.setOpacity(0.2);
    watermark.setRotateAngle(-30);

    // Add watermark
    watermarker.add(watermark);
    watermarker.save("result.pdf");
}
```

The output of the code above shows repeated text watermarks:
![text repeated watermarks](/watermark/net/images/tilling-text-30.png)

`TileMeasureType` sets the unit of a `MeasureValue`: `Pixel`, `Percent` (of the page size) or `Points`. The value must be greater than 0; `setValue` throws an exception with the message "Value must be greater than 0." for zero and negative values.

#### Rotation around the origin

In the image above, each row of tiles is rotated relative to the left edge of the document. You can rotate the whole pattern around the bottom left corner of the document instead. To do this, set `setRotateAroundOrigin` of the `TileOptions` class to `true`:

```java
watermark.getTileOptions().setRotateAroundOrigin(true);
```

In this case, the repeated watermark looks like this:
![repeated watermarks rotation around the origin](/watermark/net/images/tilling-text-center.png)

{{< alert style="info" >}}`setRotateAroundOrigin` was added in version 26.11. It replaces `setRotateAroundCenter`, which is deprecated and calls the new method.{{< /alert >}}

#### Tile patterns

The `setTileType` method of the `TileOptions` class sets the tile pattern. It takes one of the constants of the `com.groupdocs.watermark.watermarks.TileType` class:

| Constant | Pattern |
|----------|---------|
| `TileType.Straight` | The default. Rows of tiles are aligned with each other. |
| `TileType.Offset` | Every second row is shifted by a half of the tile step. |
| `TileType.OneThirdOffset` | Every second row is shifted by two thirds of the tile step. |
| `TileType.BasketWeave` | Tiles are laid out in alternating groups of three horizontal and three vertical watermarks. The rotation angle of the watermark is ignored. |

For example, add the following line to the previous example to enable the offset pattern:

```java
watermark.getTileOptions().setTileType(TileType.Offset);
```

With the offset pattern, each row of tiles is shifted relative to the previous one. Instead of a strict grid, the watermarks form a more dynamic pattern that is harder to remove:
![adding-repeated-watermarks](/watermark/net/images/tilling-text-30-offset.png)

The following line enables the basket weave pattern:

```java
watermark.getTileOptions().setTileType(TileType.BasketWeave);
```

It produces the following result:
![adding-repeated-watermarks](/watermark/net/images/basket-weave.png)

{{< alert style="info" >}}`TileType.OneThirdOffset` and `TileType.BasketWeave` are available since version 26.11.{{< /alert >}}

### Image repeated watermark

Repeated watermarks also work with images. The following code adds rotated repeated image watermarks to a PDF document.

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.watermarks.ImageWatermark;
import com.groupdocs.watermark.watermarks.MeasureValue;
import com.groupdocs.watermark.watermarks.TileMeasureType;
import com.groupdocs.watermark.watermarks.TileOptions;

try (Watermarker watermarker = new Watermarker("sample.pdf");
     // Create the image watermark object
     ImageWatermark watermark = new ImageWatermark("logo.png")) {

    // Configure tile options
    MeasureValue lineSpacing = new MeasureValue();
    lineSpacing.setMeasureType(TileMeasureType.Percent);
    lineSpacing.setValue(12);

    MeasureValue watermarkSpacing = new MeasureValue();
    watermarkSpacing.setMeasureType(TileMeasureType.Percent);
    watermarkSpacing.setValue(10);

    TileOptions tileOptions = new TileOptions();
    tileOptions.setLineSpacing(lineSpacing);
    tileOptions.setWatermarkSpacing(watermarkSpacing);
    watermark.setTileOptions(tileOptions);

    // Set watermark properties
    watermark.setOpacity(0.3);
    watermark.setRotateAngle(-30);

    // Add watermark
    watermarker.add(watermark);
    watermarker.save("result.pdf");
}
```

This is the resulting appearance of the document after applying tiled image watermarks:
![adding-repeated-watermarks](/watermark/net/images/tilling-image-30.png)

### More examples

The [GroupDocs.Watermark for Java examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java) repository contains runnable tiled watermark examples: `basic_usage.AddTextTiledWatermark` and `basic_usage.AddImageTiledWatermark`.
