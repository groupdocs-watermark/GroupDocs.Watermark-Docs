---
id: clear
url: watermark/java/basic-usage/clear
title: Clear watermarks
weight: 6
description: This article shows how to clear existing text or image watermarks.
keywords: clear text watermark, clear image watermark, remove watermark, java
productName: GroupDocs.Watermark for Java
hideChildren: True
toc: true
---
Removing existing watermarks is another powerful feature of the GroupDocs.Watermark library. It allows searching and then removing text or image watermarks from a wide range of supported documents. Removing watermarks is possible for some of the supported formats. To learn whether it is available for your format, check [Supported formats]({{< ref "watermark/java/getting-started/supported-document-formats.md" >}}).

## Deleting text watermarks

To search and remove text watermarks:
1. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#Watermarker-java.lang.String-) an instance of the `Watermarker` class for a local file or file stream;
2. Specify the sought-after text of the watermark. To define criteria use the instance of the [TextSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/textsearchcriteria/) class. In this example, we will search for a particular string match.
3. Call the [search](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#search-com.groupdocs.watermark.search.SearchCriteria-) method of the `Watermarker` class to perform the search and obtain a collection of all possible watermarks that meet the search criteria.
4. Use the [clear](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/removeonlylistbase/#clear--) method of the `PossibleWatermarkCollection` class to remove all found watermarks.
5. Call the [save](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#save-java.lang.String-) method to store the document in a new location.

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.search.PossibleWatermarkCollection;
import com.groupdocs.watermark.search.TextSearchCriteria;

try (Watermarker watermarker = new Watermarker("C:\\Docs\\watermarked-sample.docx")) {
    // Search watermark matching a particular text
    TextSearchCriteria searchCriteria = new TextSearchCriteria("Contract Draft", false);
    PossibleWatermarkCollection possibleWatermarks = watermarker.search(searchCriteria);
    // Clear all found watermarks
    possibleWatermarks.clear();
    // Save document
    watermarker.save("C:\\Docs\\clean-sample.docx");
}
```

Run the program. All found occurrences of "Contract Draft" in watermarks will be removed.

![Cleaning text watermarks](/watermark/net/images/watermarking/clean-text.png)

## Deleting image watermarks

To search and remove image watermarks within the document:
1. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#Watermarker-java.lang.String-) an instance of the `Watermarker` class for a local file or file stream;
2. Specify the sought-after image of the watermarks. To define criteria use the instance of the [ImageSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/imagesearchcriteria/) class.
3. (Optionally.) Specify the maximum allowed difference between the images using the [setMaxDifference](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/imagesearchcriteria/#setMaxDifference-double-) method. Too strict threshold may fail to detect all needed images, while a very lenient threshold could match dissimilar images.
4. Call the [search](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#search-com.groupdocs.watermark.search.SearchCriteria-) method of the `Watermarker` class to perform the search and obtain a collection of all possible watermarks that meet the search criteria.
5. Use the [clear](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/removeonlylistbase/#clear--) method of the `PossibleWatermarkCollection` class to remove all found watermarks.
6. Call the [save](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#save-java.lang.String-) method to store the document in a new location.

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.search.ImageDctHashSearchCriteria;
import com.groupdocs.watermark.search.ImageSearchCriteria;
import com.groupdocs.watermark.search.PossibleWatermarkCollection;

try (Watermarker watermarker = new Watermarker("watermarked-sample.docx")) {
    // Initialize criteria with the image
    ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("logo.png");
    // Set maximum allowed difference between images
    imageSearchCriteria.setMaxDifference(0.9);
    PossibleWatermarkCollection possibleWatermarks = watermarker.search(imageSearchCriteria);
    // Clear all found watermarks
    possibleWatermarks.clear();
    // Save document
    watermarker.save("clean-sample.docx");
}
```

Run the program. All found occurrences of image watermarks will be deleted.

![Cleaning image watermarks](/watermark/net/images/watermarking/clean-image.png)

### What's next

To remove a single found watermark, remove watermarks with a particular text formatting, or remove hyperlinks, see the [Removing found watermarks]({{< ref "watermark/java/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks.md" >}}) article of the "Advanced usage" section.
