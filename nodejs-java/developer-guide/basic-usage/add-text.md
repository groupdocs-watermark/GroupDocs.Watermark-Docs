---
id: add-text
url: watermark/nodejs-java/add-text
title: Add text watermarks
weight: 1
description: This article shows how to add a text watermark and save the resultant document. It is capable of adding watermarks to images or documents.
keywords: add text watermark, add text watermark to image, text watermark
productName: GroupDocs.Watermark for Node.js via Java
hideChildren: True
toc: true
---
One of the main features of the GroupDocs.Watermark library is adding text watermarks to documents. You may add watermarks to documents or images from local disks, as well as from streams. For a full list of supported document formats, check [Supported formats]({{< ref "watermark/net/getting-started/supported-document-formats.md" >}}).

To add a text watermark perform follow next code sample:


```js
const groupdocs.watermark = require('@groupdocs/groupdocs.watermark')

function addATextWatermark() {
  const watermarker = new groupdocs.watermark.Watermarker("sample.docx");

  const watermark = new groupdocs.watermark.TextWatermark('top secret', new groupdocs.watermark.Font('Arial', 36));
  watermark.setForegroundColor(groupdocs.watermark.Color.getRed());
  watermark.setHorizontalAlignment(groupdocs.watermark.HorizontalAlignment.Center);
  watermark.setVerticalAlignment(groupdocs.watermark.VerticalAlignment.Center);

  watermarker.add(watermark);
  watermarker.save("sample.docx");
  watermarker.close();
}
```

Run the program. A new watermarked document will appear in the specified path.

### What's next

GroupDocs.Watermark offers many more capabilities for adding text watermarks. For example, it allows specifying background and foreground colors, formatting, text opacity, use of absolute or relative positioning, and so on.