---
id: clear
url: watermark/net/basic-usage/watermarking/clear
title: Clear watermarks
weight: 5
description: This article shows how to clear existing text or image watermarks.
keywords: clear text watermark, clear image watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
Removing existing watermarks is another powerful feature of the GroupDocs.Watermark library. It allows searching and then removing text or image watermarks from a wide range of supported documents.

{{< alert style="info" >}}Updating of watermarks is not allowed in evaluation mode. Please set up a license as described in [Licensing and evaluation]({{< ref "watermark/net/getting-started/evaluation-limitations-and-licensing" >}}).{{< /alert >}}

## Deleting text watermarks

To search and remove text watermarks:
1. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) an instance of the `Watermarker` class for a local file or file stream;
2. Specify the sought-after text of the watermark. To define criteria use the instance of the [TextSearchCriteria](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.search.searchcriteria/textsearchcriteria/) class. In this example, we will search for a particular string match.
3. Call the [Search](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermarker/search/#search_1) method of the `Watermarker` class to perform the search and obtain a collection of all possible watermarks that meet the search criteria.
4. Use the [Clear](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.common/removeonlylistbase-1/clear/) method of the `PossibleWatermarkCollection` class to remove all found watermarks.
5. Call the [Save](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/4) method to store the document in a new location.

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Search.SearchCriteria;
using GroupDocs.Watermark.Search;

using (Watermarker watermarker = new Watermarker("C:\\Docs\\watermarked-sample.docx"))
{
    // Search watermark matching a particular text
    TextSearchCriteria searchCriteria = new TextSearchCriteria("Top secret", false);
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search(searchCriteria);    
    // Clear all found watermarks
    possibleWatermarks.Clear();
    // Save document
    watermarker.Save("C:\\Docs\\clean-sample.docx");
}
```
Run the program. All found occurrences of "Top secret" in watermarks will be removed.
![Cleaning text watermarks](/watermark/net/images/watermarking/clean-text.png)

## Deleting image watermarks

To search and remove image watermarks within the document:
1. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) an instance of the `Watermarker` class for a local file or file stream;
2. Specify the sought-after image of the watermarks. To define criteria use the instance of the [ImageSearchCriteria](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.search.searchcriteria/imagesearchcriteria/) class.
3. (Optionally.) Specify the maximum allowed difference between the images using the [MaxDifference](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.search.searchcriteria/imagesearchcriteria/maxdifference/) property. Too strict threshold may fail to detect all needed images, while a very lenient threshold could match dissimilar images.
4. Call the [Search](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermarker/search/#search_1) method of the `Watermarker` class to perform the search and obtain a collection of all possible watermarks that meet the search criteria.
5. Use the [Clear](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.common/removeonlylistbase-1/clear/) method of the `PossibleWatermarkCollection` class to remove all found watermarks.
6. Call the [Save](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/4) method to store the document in a new location.

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Search.SearchCriteria;
using GroupDocs.Watermark.Search;

using (Watermarker watermarker = new Watermarker("C:\\Docs\\watermarked-sample.docx"))

{
    // Initialize criteria with the image    
    ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("C:\\Docs\\logo.png");
    //Set maximum allowed difference between images
    imageSearchCriteria.MaxDifference = 0.9;
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search(imageSearchCriteria);
    // Clear all found watermarks
    possibleWatermarks.Clear();
    // Save document
    watermarker.Save("C:\\Docs\\clean-sample.docx");
}
```
Run the program. All found occurrences of image watermarks will be deleted.

![Cleaning image watermarks](/watermark/net/images/watermarking/clean-image.png)

