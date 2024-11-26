---
id: clear
url: watermark/nodejs-java/clear
title: Clear watermarks
weight: 6
description: This article shows how to clear existing text or image watermarks.
keywords: clear text watermark, clear image watermark
productName: GroupDocs.Watermark for Node.js via Java
hideChildren: True
---
Removing existing watermarks is another powerful feature of the GroupDocs.Watermark library. It allows searching and then removing text or image watermarks from a wide range of supported documents. Removing watermarks is possible for some of the supported formats. To learn whether it is available for your format, check [Supported formats]({{< ref "watermark/nodejs-java/getting-started/supported-document-formats.md" >}}).

{{< alert style="info" >}}Updating of watermarks is not allowed in evaluation mode. Please set up a license as described in [Licensing and evaluation]({{< ref "watermark/nodejs-java/getting-started/evaluation-limitations-and-licensing" >}}).{{< /alert >}}

## Deleting text watermarks

To search and remove text watermarks follow next sample:

```js
const groupdocs.watermark = require('@groupdocs/groupdocs.watermark')

function removeTextWatermarks() {
    // Create an instance of Watermarker
    const watermarker = new groupdocsWatermark.Watermarker('sample.pdf');

    // Create a TextSearchCriteria instance
    const criteria = new groupdocsWatermark.TextSearchCriteria('test', false);
    const watermarks = watermarker.search(criteria);

    // Remove found text fragments
    watermarks.clear();

    // Save changes
    watermarker.save('result.pdf');

    // Close watermarker
    watermarker.close();
}
```

## Deleting image watermarks

To search and remove image watermarks within the document:

```js
const groupdocs.watermark = require('@groupdocs/groupdocs.watermark')

function removeImageWatermarks() {
  // Create watermarker
  const watermarker = new groupdocsWatermark.Watermarker('sample.docx');

  // Initialize search criteria with the image
  const imageSearchCriteria = new groupdocsWatermark.ImageDctHashSearchCriteria("logo.png");

  // Set maximum allowed difference between images
  imageSearchCriteria.setMaxDifference(0.9);

  // Search for possible watermarks matching the criteria
  const watermarks = watermarker.search(imageSearchCriteria);

  console.log(`Found ${watermarks.getCount()} possible watermark(s).`);

    // Remove found text fragments
    watermarks.clear();

    // Save changes
    watermarker.save('result.docx');

    // Close watermarker
    watermarker.close();
}

```
Run the program. All found occurrences of image watermarks will be deleted.

