---
id: add-image
url: watermark/nodejs-java/add-image
title: Add image watermarks
weight: 2
description: This article shows how to add an image watermark and save the resultant document. It is capable of adding watermarks to images or documents.
keywords: add image watermark, add image watermark to image, image watermark
productName: GroupDocs.Watermark for Node.js via Java
hideChildren: True
toc: true
---
One of the main features of the GroupDocs.Watermark library is adding image watermarks to documents. You may add watermarks to documents or images from local disks, as well as from streams. For a full list of supported document formats, check [Supported formats]({{< ref "watermark/net/getting-started/supported-document-formats.md" >}}).

To add an image watermark perform the following sample:

```javascript
const groupdocs.watermark = require('@groupdocs/groupdocs.watermark')

function addAnImageWatermark() {
  const watermarker = new groupdocs.watermark.Watermarker("sample.pdf");

  const imageWatermark = new groupdocs.watermark.ImageWatermark("sample.png");
  imageWatermark.setHorizontalAlignment(groupdocs.watermark.HorizontalAlignment.Center);
  imageWatermark.setVerticalAlignment(groupdocs.watermark.VerticalAlignment.Center);

  watermarker.add(imageWatermark);
  watermarker.save("sample.pdf");
  watermarker.close();
  console.log('Image watermark added and document saved successfully.');
}
```

### What's next

GroupDocs.Watermark offers many more capabilities for adding image watermarks. It's possible  from streams, use absolute or relative positioning, and so on.
