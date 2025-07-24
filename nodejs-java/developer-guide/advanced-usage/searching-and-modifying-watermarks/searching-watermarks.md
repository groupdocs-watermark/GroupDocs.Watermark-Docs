---
id: searching-watermarks
url: watermark/nodejs-java/searching-watermarks
title: Searching watermarks
weight: 1
description: "This article explains how to search watermarks while using GroupDocs. Watermarks API."
keywords: search watermarks
productName: GroupDocs.Watermark for Node.js via Java
hideChildren: True
toc: true
---
## Searching possible watermarks

GroupDocs.Watermark API allows you to search the possible watermarks placed in any document. You can also search the watermarks that are added using some third-party tool.  The API provides search method to search watermarks in a whole document or in any part of the document. Following code snippet shows how to find and get all possible watermarks in a document.

```js
// Create an instance of Watermarker
const watermarker = new groupdocsWatermark.Watermarker('sample.pdf');

const watermarks = watermarker.search();
  // Iterate through found watermarks
  for (const watermark of watermarks.getInnerList().toArray()) {
    console.log(watermark.getText());
    console.log(watermark.getRotateAngle());
    console.log(watermark.getX());
    console.log(watermark.getY());
    console.log(watermark.getWidth());
    console.log(watermark.getHeight())
  }
```


## Search criteria

You can use search criteria to find objects with some specific parameters.

### Text search criteria

Following code snippet shows how to search for the watermarks that meet a particular text criterion

```js
 // Create watermarker
const watermarker = new groupdocsWatermark.Watermarker('sample.pdf');

// Define search criteria
const searchCriteria = new groupdocsWatermark.TextSearchCriteria("test", false);

// Search for watermarks
const watermarks = watermarker.search(searchCriteria);
console.log(`Found ${watermarks.getCount()} possible watermark(s).`);
```

### Image search criteria

Sometimes a document can contain image watermarks, and it's necessary to find them using sample picture. For example, you may want to find all possible image watermarks that are similar to a company logo. Following sample code searches for image watermarks that resemble with a particular image using.

```js
 // Create watermarker
const watermarker = new groupdocsWatermark.Watermarker('sample.pdf');

// Initialize search criteria with the image
const imageSearchCriteria = new groupdocsWatermark.ImageDctHashSearchCriteria('logo.png');

// Set maximum allowed difference between images
imageSearchCriteria.setMaxDifference(0.9);

// Search for possible watermarks matching the criteria
const possibleWatermarks = watermarker.search(imageSearchCriteria);

console.log(`Found ${possibleWatermarks.getCount()} possible watermark(s).`);
```

MaxDifference property is used to set maximum allowed difference between sample image and possible watermark. The value should be between 0 and 1. The value 0 means that only identical images will be found.
Using of ImageDctHashSearchCriteria is the most efficient way to find image watermark by a sample. This criterion uses DCT (Discrete Cosine Transform) based perceptual hash for image similarity comparison. But there are other image search criteria that are based on other algorithms:

### Combined search criteria

GroupDocs.Watermark API also allows you to search watermarks by a combination of different search criteria. Following sample code shows how to search watermark with the combination of different search criteria.

```js
 // Create watermarker
const watermarker = new groupdocsWatermark.Watermarker('sample.pdf');

  // Define image search criteria
  const imageSearchCriteria = new groupdocsWatermark.ImageDctHashSearchCriteria('logo.png');
  imageSearchCriteria.setMaxDifference(0.9);

  // Define text search criteria
  const textSearchCriteria = new groupdocsWatermark.TextSearchCriteria("Company Name");

  // Define rotate angle search criteria
  const rotateAngleSearchCriteria = new groupdocsWatermark.RotateAngleSearchCriteria(30, 60);

  // Combine search criteria
  const combinedSearchCriteria = imageSearchCriteria.or(textSearchCriteria).and(rotateAngleSearchCriteria);

  // Search for possible watermarks
  const possibleWatermarks = watermarker.search(combinedSearchCriteria);

  // Output the results
  console.log(`Found ${possibleWatermarks.getCount()} possible watermark(s).`);
```