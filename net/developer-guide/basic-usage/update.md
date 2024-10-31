---
id: update
url: watermark/net/basic-usage/update
title: Update watermarks
weight: 5
description: This article shows how to update existing text or image watermarks.
keywords: update text watermark, update image watermark
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
The GroupDocs.Watermark library is also capable of searching the document for any existing text or image watermarks. These can be watermarks added by any third-party tool, not only by GroupDocs.Watermark. Searching watermarks is possible for some of the supported formats. To learn whether it is available for your format, check [Supported formats]({{< ref "watermark/net/getting-started/supported-document-formats.md" >}}). 

Once found you can update those watermarks.

{{< alert style="info" >}}Updating of watermarks is not allowed in evaluation mode. Please set up a license as described in [Licensing and evaluation]({{< ref "watermark/net/getting-started/evaluation-limitations-and-licensing" >}}).{{< /alert >}}

## Updating text watermarks

To search and update text watermarks:
1. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) an instance of the `Watermarker` class for a local file or file stream;
2. Specify the sought-after text of the watermarks. To define criteria use the instance of the [TextSearchCriteria](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.search.searchcriteria/textsearchcriteria/) class. In this example, we will search for a particular string match.
3. Call the [Search](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermarker/search/#search_1) method of the `Watermarker` class to perform the search and obtain a collection of all possible watermarks that meet the search criteria.
4. Iterate through the collection of possible watermarks and update the found text occurrences using the [Text](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.search/possiblewatermark/text/) property.
5. Call the [Save](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/save/methods/4) method to store the document in a new location.

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Search.SearchCriteria;
using GroupDocs.Watermark.Search;

using (Watermarker watermarker = new Watermarker("C:\\Docs\\watermarked-sample.docx"))
{
    // Search watermark matching a particular text
    TextSearchCriteria searchCriteria = new TextSearchCriteria("Contract Draft", false);
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search(searchCriteria);
    Console.WriteLine("Found {0} possible watermark(s).", possibleWatermarks.Count);
    foreach (PossibleWatermark watermark in possibleWatermarks)
    {
        try
        {
            // Update text
            watermark.Text = "Contract is no longer valid";            
        }
        catch (Exception e)
        {
            // Found entity may not support text editing
            // Passed argument can have inappropriate value
            // Process such cases here
        }
    }
    // Save document
    watermarker.Save("C:\\Docs\\updated-sample.docx");
}
```
Run the program. All found occurrences of "Contract Draft" in watermarks will be changed to "Contract is no longer valid".

![Updating text watermarks](/watermark/net/images/watermarking/update-text.png)

### What's next

Text search capabilities of GroupDocs.Watermark are not limited by simple text matches. To learn how to search using regular expressions, or search the watermarks on the basis of some particular text formatting, or update the formatting of found text, see the [Searching watermarks]({{< ref "watermark/net/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks.md" >}}) and [Modifying found watermark properties]({{< ref "watermark/net/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifing-found-watermark-properties.md" >}}) articles of the "Advanced usage" section.

## Updating image watermarks

To search and update text watermarks:
1. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) an instance of the `Watermarker` class for a local file or file stream;
2. Specify the sought-after image of the watermarks. To define criteria use the instance of the [ImageSearchCriteria](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.search.searchcriteria/imagesearchcriteria/) class.
3. Specify the maximum allowed difference between the images using the [MaxDifference](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.search.searchcriteria/imagesearchcriteria/maxdifference/) property. Too strict threshold may fail to detect all needed images, while a very lenient threshold could match dissimilar images.
4. Call the [Search](https://reference.groupdocs.com/watermark/net/groupdocs.watermark/watermarker/search/#search_1) method of the `Watermarker` class to perform the search and obtain a collection of all possible watermarks that meet the search criteria.
5. Iterate through the collection of possible watermarks and update the found image occurrences using the [ImageData](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.search/possiblewatermark/imagedata/) property.
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
    Console.WriteLine("Found {0} possible watermark(s).", possibleWatermarks.Count);
    
    // Read new watermark image
    byte[] imageData = File.ReadAllBytes("C:\\Docs\\new-logo.png");
    foreach (PossibleWatermark watermark in possibleWatermarks)
    {
        try
        {
            // Replace image
            watermark.ImageData = imageData;
        }
        catch (Exception e)
        {
            // Found entity may not support text editing
            // Passed argument can have inappropriate value
            // Process such cases here
        }
    }
    // Save document
    watermarker.Save("C:\\Docs\\updated-sample.docx");    
}
```
Run the program. All found occurrences of image watermarks will be updated.

![Updating image watermarks](/watermark/net/images/watermarking/update-image.png)

### What's next

Searching by images is a way more complex operation that may require finding an appropriate difference threshold or even using other image comparison algorithms. GroupDocs.Watermark offers several image search criteria algorithms. To learn more about them, see the [Searching watermarks]({{< ref "watermark/net/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks.md" >}}) article of the "Advanced usage" section.

