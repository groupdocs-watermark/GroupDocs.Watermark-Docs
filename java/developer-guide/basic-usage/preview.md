---
id: preview
url: watermark/java/basic-usage/preview
title: Document preview
weight: 7
description: This article shows how to generate preview images of document pages.
keywords: document preview, page preview, generate preview, java
productName: GroupDocs.Watermark for Java
hideChildren: True
toc: true
---

GroupDocs.Watermark can generate a preview image for every page of a document. Use previews to show the pages to a user, for example to check a watermark before or after you save the document.

## Generate document preview

To create document preview:
1. [Create](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#Watermarker-java.lang.String-) an instance of the `Watermarker` class for a local file or file stream;

2. Instantiate the [PreviewOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/previewoptions/) object with an implementation of the [ICreatePageStream](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/icreatepagestream/) interface. It returns the output stream for each page image.
If you need to close the page streams yourself, also pass an implementation of the [IReleasePageStream](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/ireleasepagestream/) interface.

3. Specify the [preview format](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/previewoptions/#setPreviewFormat-int-) - `PreviewOptions.PreviewFormats.PNG`, `JPEG`, or `BMP` - and other options like the [page numbers](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/previewoptions/#setPageNumbers-int---) for which you want to generate the preview. For most document types, you can also use a format-specific subclass of `PreviewOptions`, like [PdfPreviewOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/pdfpreviewoptions/) or [SpreadsheetPreviewOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/spreadsheetpreviewoptions/), which allows you to set the resolution of the generated images in dots per inch.

4. Call the [generatePreview](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/watermarker/#generatePreview-com.groupdocs.watermark.options.PreviewOptions-) method of the `Watermarker` object and pass `PreviewOptions` to it.

`ICreatePageStream` and `IReleasePageStream` have a single method each, so you can implement them with lambda expressions:

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.options.ICreatePageStream;
import com.groupdocs.watermark.options.IReleasePageStream;
import com.groupdocs.watermark.options.PreviewOptions;

import java.io.File;
import java.io.FileNotFoundException;
import java.io.FileOutputStream;
import java.io.IOException;

String outputDirectory = "C:\\Docs\\preview";

try (Watermarker watermarker = new Watermarker("sample.pdf")) {
    ICreatePageStream createPageStream = pageNumber -> {
        File previewImageFile = new File(outputDirectory, "page" + pageNumber + ".png");
        try {
            return new FileOutputStream(previewImageFile);
        } catch (FileNotFoundException e) {
            throw new RuntimeException(e);
        }
    };

    IReleasePageStream releasePageStream = (pageNumber, pageStream) -> {
        try {
            pageStream.close();
        } catch (IOException e) {
            throw new RuntimeException(e);
        }
    };

    PreviewOptions previewOptions = new PreviewOptions(createPageStream, releasePageStream);
    previewOptions.setPreviewFormat(PreviewOptions.PreviewFormats.PNG);
    previewOptions.setPageNumbers(new int[] { 1, 2 });

    watermarker.generatePreview(previewOptions);
}
```

Run the program. It will create images in the `outputDirectory` folder corresponding to the pages of the document.

The [GroupDocs.Watermark for Java examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java) repository contains a runnable preview example, `basic_usage.GenerateDocumentPreview`, that implements the interfaces with classes.
