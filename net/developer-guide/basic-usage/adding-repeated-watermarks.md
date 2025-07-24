---
id: adding-repeated-watermarks
url: watermark/net/adding-repeated-watermarks
title: Adding repeated watermarks
linkTitle: Repeated watermarks
weight: 3
description: "The GroupDocs.Watermark allows to add repeated or tiled watermarks to documents"
keywords: add repeated watermarks, tiled watermarks
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---

## Rrepeated watermark

Enhance the visual appeal and branding of your documents with the power of repeated or tiled watermarks. This innovative feature allows you to seamlessly integrate patterns of text or images across your pages, creating a professional and cohesive look. Whether you're aiming for subtle branding, artistic expression, or document security, the ability to configure the spacing, rotation, and style of these watermarks provides unparalleled customization. Explore the possibilities and make your documents stand out with the elegance of tiled watermarks.

### Text repeated watermark

The provided code snippet demonstrates how to add a tiled watermark to a document. To configure tiling settings, we can utilize the dedicated class [TileOptions](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/tileoptions). In this example, we set the LineSpacing property, determining the spacing between parallel tiles, to 12 percent of the page size. Additionally, we define the WatermarkSpacing property, which sets the spacing between watermarks in the line, to be 10 percent of the page size. Next image helps to understand the purpose of LineSpacing and WatermarkSpacing settings:
![adding-repeated-watermarks](/watermark/net/images/tilling-options.png)

Furthermore, we apply a watermark rotation of 30 degrees for added customization.

```csharp
    using (Watermarker watermarker = new Watermarker("sample.pdf"))
    {
        // Initialize the font to be used for watermark
        Font font = new Font("Arial", 19, FontStyle.Bold | FontStyle.Italic);

        // Create the watermark object
        var watermark = new TextWatermark("Watermark", font);
        watermark.ForegroundColor = Color.Red;

        // Configure tile options
        watermark.TileOptions = new TileOptions()
        {
            LineSpacing = new MeasureValue()
            {
                MeasureType = TileMeasureType.Percent,
                Value = 12
            },
            WatermarkSpacing = new MeasureValue()
            {
                MeasureType = TileMeasureType.Percent,
                Value = 10
            },
        };

        // Set watermark properties
        watermark.Opacity = 0.2;
        watermark.RotateAngle = -30;

        // Add watermark
        watermarker.Add(watermark);
        watermarker.Save("result.pdf");
    }        
```

The output of the above mentioned code is represented below, showcasing repeated text watermarks:
![text repeated watermarks](/watermark/net/images/tilling-text-30.png)

The common rotation of watermarks on the above image is done relative to the left edge of the document. It's also possible to do the common rotation relative to the bottom left edge of the document. For this need to set property [RotateAroundOrigin](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/tileoptions/rotatearoundorigin/) of the class TileOptions in the true.
```csharp
watermark.TileOptions.RotateAroundOrigin = true;
```
In such case the result of repeated watermark looks like this:
![repeated watermarks rotaion around the center](/watermark/net/images/tilling-text-center.png)

Class TileOptions includes a [TileType](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/tiletype) property, providing the ability to configure the tile template. The default value is Straight mode, but we can change it. For instance, in the previous example, if we add the setting 
```csharp
   watermark.TileOptions.TileType = TileType.Offset
```
it enables the offset style. In the context of watermarks and tiling, the "offset style" refers to a specific arrangement where each tile is positioned with a shift or offset from the previous one. Instead of aligning tiles in a straightforward, parallel manner, the offset style introduces a displacement, creating a more dynamic and visually interesting pattern. This shift can occur horizontally, vertically, or both, depending on the specific settings applied.
In this case, the output will exhibit the following effect:
![adding-repeated-watermarks](/watermark/net/images/tilling-text-30-offset.png)

The TileType enum supports a range of tile templates, including OneThirdOffset and BasketWeave, to accommodate diverse design needs. Setting
```csharp
   watermark.TileOptions.TileType = TileType.BasketWeave
```
It produces the following visual result for the BasketWeave tile watermark pattern in the document:
![adding-repeated-watermarks](/watermark/net/images/basket-weave.png)

### Image repeated watermark

The repeated watermark feature also supports image watermarks. The following C# code demonstrates how to add repeated image watermarks to a PDF document with rotation.

```csharp
    using (Watermarker watermarker = new Watermarker("sample.pdf"))
    {
        // Initialize the font to be used for watermark
        Font font = new Font("Arial", 19, FontStyle.Bold | FontStyle.Italic);

        // Create the image watermark object
        var watermark = new ImageWatermark(imagePath);

        // Configure tile options
        watermark.TileOptions = new TileOptions()
        {
            LineSpacing = new MeasureValue()
            {
                MeasureType = TileMeasureType.Percent,
                Value = 12
            },
            WatermarkSpacing = new MeasureValue()
            {
                MeasureType = TileMeasureType.Percent,
                Value = 10
            },
        };

        // Set watermark properties
        watermark.Opacity = 0.3;
        watermark.RotateAngle = -30;

        // Add watermark
        watermarker.Add(watermark);
        watermarker.Save("result.pdf");
    }        
```

This is the resulting appearance of the document after applying tiled image watermarks:
![adding-repeated-watermarks](/watermark/net/images/tilling-image-30.png)