---
id: add-image
url: watermark/java/basic-usage/add-image
title: Add image watermarks
weight: 2
description: This article shows how to add an image watermark and save the resultant document. It is capable of adding watermarks to images or documents.
keywords: add image watermark, add image watermark to image, image watermark, java
productName: GroupDocs.Watermark for Java
hideChildren: True
toc: true
---
One of the main features of the GroupDocs.Watermark library is adding image watermarks to documents. You may add watermarks to documents or images from local disks, as well as from streams. For a full list of supported document formats, check [Supported formats]({{< ref "watermark/java/getting-started/supported-document-formats.md" >}}).

To add an image watermark perform the following steps:

1. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#Watermarker-java.lang.String-) an instance of the `Watermarker` class for a local file or file stream;
2. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/imagewatermark/#ImageWatermark-java.lang.String-) an instance of the `ImageWatermark` class from the local image file;
3. (Optionally.) Specify the watermark [horizontal](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setHorizontalAlignment-int-) and [vertical](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermark/#setVerticalAlignment-int-) alignments;
4. Call the [add](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#add-com.groupdocs.watermark.Watermark-) method to apply the watermark to the document;
5. Call the [save](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#save-java.lang.String-) method to store the document in a new location.

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.common.HorizontalAlignment;
import com.groupdocs.watermark.common.VerticalAlignment;
import com.groupdocs.watermark.watermarks.ImageWatermark;

// Specify an absolute or relative path to your document
// and to the desired image.
try (Watermarker watermarker = new Watermarker("C:\\Docs\\contract.docx");
     ImageWatermark watermark = new ImageWatermark("C:\\Docs\\logo.png")) {
    // Specify watermark size, opacity and alignments
    watermark.setWidth(200);
    watermark.setHeight(200);
    watermark.setOpacity(0.5);
    watermark.setHorizontalAlignment(HorizontalAlignment.Center);
    watermark.setVerticalAlignment(VerticalAlignment.Center);
    // Apply the watermark
    watermarker.add(watermark);
    // Save the resulting document
    watermarker.save("C:\\Docs\\img-watermarked-contract.docx");
}
```

Run the program. A new watermarked document will appear in the specified path.

![Adding image watermarks](/watermark/net/images/watermarking/add-image.png)

{{< alert style="info" >}}Both `Watermarker` and [ImageWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/imagewatermark/) implement the `java.io.Closeable` interface. Declare them in a try-with-resources statement, as above, or call their `close()` methods when you are done.{{< /alert >}}

### What's next

GroupDocs.Watermark offers many more capabilities for adding image watermarks. To learn how to add watermarks from streams, use absolute or relative positioning, and so on, see the [Adding image watermarks]({{< ref "watermark/java/developer-guide/advanced-usage/adding-watermarks/adding-image-watermarks.md" >}}) article of the "Advanced usage" section.
