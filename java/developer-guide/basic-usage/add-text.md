---
id: add-text
url: watermark/java/basic-usage/add-text
title: Add text watermarks
weight: 1
description: This article shows how to add a text watermark and save the resultant document. It is capable of adding watermarks to images or documents.
keywords: add text watermark, add text watermark to image, text watermark, java
productName: GroupDocs.Watermark for Java
hideChildren: True
toc: true
aliases:
    - /watermark/java/add-text-or-image-watermark/
---
One of the main features of the GroupDocs.Watermark library is adding text watermarks to documents. You may add watermarks to documents or images from local disks, as well as from streams. For a full list of supported document formats, check [Supported formats]({{< ref "watermark/java/getting-started/supported-document-formats.md" >}}).

To add a text watermark perform the following steps:

1. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#Watermarker-java.lang.String-) an instance of the `Watermarker` class for a local file or file stream;
2. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/textwatermark/#TextWatermark-java.lang.String-com.groupdocs.watermark.watermarks.Font-) an instance of the `TextWatermark` class and specify the desired text and font for the watermark;
3. (Optionally.) Specify the watermark [color](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/textwatermark/#setForegroundColor-com.groupdocs.watermark.watermarks.Color-), [horizontal](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setHorizontalAlignment-int-) and [vertical](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setVerticalAlignment-int-) alignments;
4. Call the [add](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#add-com.groupdocs.watermark.Watermark-) method to apply the watermark to the document;
5. Call the [save](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#save-java.lang.String-) method to store the document in a new location.

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.common.HorizontalAlignment;
import com.groupdocs.watermark.common.VerticalAlignment;
import com.groupdocs.watermark.watermarks.Color;
import com.groupdocs.watermark.watermarks.Font;
import com.groupdocs.watermark.watermarks.FontStyle;
import com.groupdocs.watermark.watermarks.TextWatermark;

// Specify an absolute or relative path to your document.
try (Watermarker watermarker = new Watermarker("C:\\Docs\\contract.docx")) {
    // Specify the desired text and font for the watermark
    TextWatermark watermark = new TextWatermark("Contract Draft",
            new Font("Arial", 60, FontStyle.Bold));
    // Specify font color, text opacity and alignments
    watermark.setForegroundColor(Color.getDarkGreen());
    watermark.setOpacity(0.5);
    watermark.setHorizontalAlignment(HorizontalAlignment.Center);
    watermark.setVerticalAlignment(VerticalAlignment.Center);
    // Apply the watermark
    watermarker.add(watermark);
    // Save the resulting document
    watermarker.save("C:\\Docs\\watermarked-contract.docx");
}
```

Run the program. A new watermarked document will appear in the specified path.

![Adding text watermarks](/watermark/net/images/watermarking/add-text.png)

### What's next

GroupDocs.Watermark offers many more capabilities for adding text watermarks. For example, it allows specifying background and foreground colors, formatting, text opacity, use of absolute or relative positioning, custom fonts, and so on. To learn more about this, see the [Adding text watermarks]({{< ref "watermark/java/developer-guide/advanced-usage/adding-watermarks/adding-text-watermarks.md" >}}) article of the "Advanced usage" section.
