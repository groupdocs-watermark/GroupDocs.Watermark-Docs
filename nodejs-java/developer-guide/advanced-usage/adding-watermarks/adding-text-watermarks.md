---
id: adding-text-watermarks
url: watermark/nodejs-java/adding-text-watermarks
title: Adding text watermarks
linkTitle: Text watermarks
weight: 1
description: "The GroupDocs.Watermark allows to add text watermarks to documents which may consists of pages, worksheets, slides or frames."
keywords: add text watermarks, text watermarks
productName: GroupDocs.Watermark for Node.js via Java
hideChildren: True
---

Using text watermarks is an effective way to protect the integrity of document content. By marking sensitive documents with watermarks like "Confidential" or "Draft," organizations can discourage unauthorized sharing and strengthen data security measures. This visual indicator acts as a continual reminder of the document's restricted status, encouraging careful handling by anyone who views it.

The following code snippet shows how to add text watermark to a document. 

```js
const watermarker = new groupdocsWatermark.Watermarker('sample.pdf');
const watermark = new groupdocsWatermark.TextWatermark('Test watermark', new 
    groupdocsWatermark.Font('Arial', 36, groupdocsWatermark.FontStyle.Bold));

watermark.setTextAlignment(groupdocsWatermark.TextAlignment.Right);
watermark.setOpacity(0.4);
watermark.setForegroundColor(groupdocsWatermark.Color.getRed());
watermark.setBackgroundColor(groupdocsWatermark.Color.getBlue());

watermarker.add(watermark);

watermarker.save("result.pdf");
watermarker.close();
```

If the document consists of multiple parts (pages, worksheets, slides, frames, etc.), the watermark will be added to each of them. You can configure this behaivior through the [PagesSetup](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.watermarks/pagessetup/) property:

```js

  const pagesSetup = new groupdocsWatermark.PagesSetup();
  pagesSetup.setFirstPage(true);
  pagesSetup.setOddPages(true);

  watermark.setPagesSetup(pagesSetup);

```

## Sizing and positioning of watermark

### Absolute watermark positioning

Using GroupDocs.Watermark, you can also add watermark to some absolute position in the document. Following example shows how to add a text watermark with absolute positioning using properties X, Y, Width and Height. The values of all properties for absolute sizing and positioning are measured in default document units.

```js
const watermarker = new groupdocsWatermark.Watermarker('sample.pdf');
const watermark = new groupdocsWatermark.TextWatermark('Test watermark', new 
    groupdocsWatermark.Font('Arial', 36, groupdocsWatermark.FontStyle.Bold));

watermark.setX(10.0);
watermark.setY(20.0);

watermark.setWidth(100.0);
watermark.setHeight(40.0);

watermarker.add(watermark);
watermarker.save("result.pdf");
watermarker.close();
```

### Using the MarginType property

In the example above, absolute margin values are used. This means that margins are measured in document units. But you can set relative margins for a watermark as well (as shown in below example), using the MarginType property

```js
const watermarker = new groupdocsWatermark.Watermarker('image.png');
const watermark = new groupdocsWatermark.TextWatermark('Test watermark', new 
    groupdocsWatermark.Font('Calibri', 32));

watermark.Margins.setMarginType(groupdocsWatermark.MarginType.RelativeToParentDimensions);
watermark.Margins.setRight(0.1);
watermark.Margins.setBottom(0.2);

watermarker.add(watermark);
watermarker.save("result.png");
watermarker.close();
```

### Watermark rotation

GroupDocs.Watermark API also supports rotation of the watermark. You can use [RotateAngle] property to define watermark rotation angle in degrees. A positive value means clockwise rotation.

```js
const watermarker = new groupdocsWatermark.Watermarker('test.docx');
const watermark = new groupdocsWatermark.TextWatermark('Test watermark', new 
    groupdocsWatermark.Font('Calibri', 32));

watermark.setHorizontalAlignment(groupdocsWatermark.HorizontalAlignment.Right);
watermark.setVerticalAlignment(groupdocsWatermark.VerticalAlignment.Top);
watermark.setSizingType(groupdocsWatermark.SizingType.ScaleToParentDimensions);
watermark.setScaleFactor(0.5);

// Set rotation angle
watermark.setRotateAngle(45.0);

watermarker.add(watermark);
watermarker.save("result.docx");
watermarker.close();
```


If rotation angle is set, it is assumed that watermark size is equal to axis-aligned bounding box size. The following picture illustrates what is the watermark bounding box and how it is used for sizing and positioning. The picture shows a result of execution of the above code snippet. The actual watermark bounds are colored in blue and the bounding box is colored in red. As you can see, the bounding box size is used to calculate watermark relative size.

![adding-text-watermarks](/watermark/net/images/adding-text-watermarks.png)

### Using custom fonts

GroupDocs.Watermark API provides ability to use custom TrueType fonts. For this you can configure FolderPath property through the Font class constructor with a folder path which contains fonts files.

```js
const watermarker = new groupdocsWatermark.Watermarker('test.pdf');

var fontsFolder = @"c:\CustomFonts\";
// Initialize the font to be used for watermark and folder with it
var font = new groupdocsWatermark.Font("OT Chekharda Bold Italic", fontsFolder, 36)
const watermark = new groupdocsWatermark.TextWatermark('top secret', font);

watermark.setForegroundColor(groupdocsWatermark.Color.getRed());
watermark.setX(10);
watermark.setY(100);
watermark.setOpacity(0.4);

watermarker.add(watermark);
watermarker.save(outputFilePath);
watermarker.close();
```