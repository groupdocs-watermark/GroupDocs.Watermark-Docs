---
id: update
url: watermark/java/basic-usage/update
title: Update watermarks
weight: 5
description: This article shows how to update existing text or image watermarks.
keywords: update text watermark, update image watermark, java
productName: GroupDocs.Watermark for Java
hideChildren: True
toc: true
---
The GroupDocs.Watermark library is also capable of searching the document for any existing text or image watermarks. These can be watermarks added by any third-party tool, not only by GroupDocs.Watermark. Searching watermarks is possible for some of the supported formats. To learn whether it is available for your format, check [Supported formats]({{< ref "watermark/java/getting-started/supported-document-formats.md" >}}).

Once found you can update those watermarks.

## Updating text watermarks

To search and update text watermarks:
1. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#Watermarker-java.lang.String-) an instance of the `Watermarker` class for a local file or file stream;
2. Specify the sought-after text of the watermarks. To define criteria use the instance of the [TextSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/textsearchcriteria/) class. In this example, we will search for a particular string match.
3. Call the [search](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#search-com.groupdocs.watermark.search.SearchCriteria-) method of the `Watermarker` class to perform the search and obtain a collection of all possible watermarks that meet the search criteria.
4. Iterate through the collection of possible watermarks and update the found text occurrences using the [setText](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/possiblewatermark/#setText-java.lang.String-) method.
5. Call the [save](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#save-java.lang.String-) method to store the document in a new location.

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.search.PossibleWatermark;
import com.groupdocs.watermark.search.PossibleWatermarkCollection;
import com.groupdocs.watermark.search.TextSearchCriteria;

try (Watermarker watermarker = new Watermarker("C:\\Docs\\watermarked-sample.docx")) {
    // Search watermark matching a particular text
    TextSearchCriteria searchCriteria = new TextSearchCriteria("Contract Draft", false);
    PossibleWatermarkCollection possibleWatermarks = watermarker.search(searchCriteria);
    System.out.println("Found " + possibleWatermarks.getCount() + " possible watermark(s).");
    for (PossibleWatermark watermark : possibleWatermarks) {
        try {
            // Update text
            watermark.setText("Contract is no longer valid");
        } catch (Exception e) {
            // Found entity may not support text editing
            // Passed argument can have inappropriate value
            // Process such cases here
        }
    }
    // Save document
    watermarker.save("C:\\Docs\\updated-sample.docx");
}
```

Run the program. All found occurrences of "Contract Draft" in watermarks will be changed to "Contract is no longer valid".

![Updating text watermarks](/watermark/net/images/watermarking/update-text.png)

### What's next

Text search capabilities of GroupDocs.Watermark are not limited by simple text matches. To learn how to search using regular expressions, or search the watermarks on the basis of some particular text formatting, or update the formatting of found text, see the [Searching watermarks]({{< ref "watermark/java/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks.md" >}}) and [Modifying found watermark properties]({{< ref "watermark/java/developer-guide/advanced-usage/searching-and-modifying-watermarks/modifying-found-watermark-properties.md" >}}) articles of the "Advanced usage" section.

## Updating image watermarks

To search and update image watermarks:
1. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#Watermarker-java.lang.String-) an instance of the `Watermarker` class for a local file or file stream;
2. Specify the sought-after image of the watermarks. To define criteria use the instance of the [ImageSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/imagesearchcriteria/) class.
3. Specify the maximum allowed difference between the images using the [setMaxDifference](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/imagesearchcriteria/#setMaxDifference-double-) method. Too strict threshold may fail to detect all needed images, while a very lenient threshold could match dissimilar images.
4. Call the [search](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#search-com.groupdocs.watermark.search.SearchCriteria-) method of the `Watermarker` class to perform the search and obtain a collection of all possible watermarks that meet the search criteria.
5. Iterate through the collection of possible watermarks and update the found image occurrences using the [setImageData](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/possiblewatermark/#setImageData-byte---) method.
6. Call the [save](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#save-java.lang.String-) method to store the document in a new location.

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.search.ImageDctHashSearchCriteria;
import com.groupdocs.watermark.search.ImageSearchCriteria;
import com.groupdocs.watermark.search.PossibleWatermark;
import com.groupdocs.watermark.search.PossibleWatermarkCollection;

import java.nio.file.Files;
import java.nio.file.Paths;

// Files.readAllBytes throws IOException: declare it in the enclosing method or catch it.
try (Watermarker watermarker = new Watermarker("C:\\Docs\\watermarked-sample.docx")) {
    // Initialize criteria with the image
    ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("C:\\Docs\\logo.png");
    // Set maximum allowed difference between images
    imageSearchCriteria.setMaxDifference(0.9);
    PossibleWatermarkCollection possibleWatermarks = watermarker.search(imageSearchCriteria);
    System.out.println("Found " + possibleWatermarks.getCount() + " possible watermark(s).");

    // Read new watermark image
    byte[] imageData = Files.readAllBytes(Paths.get("C:\\Docs\\new-logo.png"));
    for (PossibleWatermark watermark : possibleWatermarks) {
        try {
            // Replace image
            watermark.setImageData(imageData);
        } catch (Exception e) {
            // Found entity may not support image replacement
            // Passed image can have inappropriate format
            // Process such cases here
        }
    }
    // Save document
    watermarker.save("C:\\Docs\\updated-sample.docx");
}
```

Run the program. All found occurrences of image watermarks will be updated.

![Updating image watermarks](/watermark/net/images/watermarking/update-image.png)

### What's next

Searching by images is a way more complex operation that may require finding an appropriate difference threshold or even using other image comparison algorithms. GroupDocs.Watermark offers several image search criteria algorithms. To learn more about them, see the [Searching watermarks]({{< ref "watermark/java/developer-guide/advanced-usage/searching-and-modifying-watermarks/searching-watermarks.md" >}}) article of the "Advanced usage" section.
