---
id: hello-world
url: watermark/java/hello-world
title: Hello, world!
weight: 8
description: Get started with GroupDocs.Watermark for Java by creating and running a minimal example.
keywords: creating a text watermark, adding text watermark to document, Java
productName: GroupDocs.Watermark for Java
hideChildren: True
toc: true
---
In this article, you will learn how to create a simple Java application that appends a text watermark using the GroupDocs.Watermark API.

{{% alert color="primary" %}}
We assume that you already have a basic knowledge of **Java** and **Maven**.
{{% /alert %}}

## Requirements

- A [compatible]({{< ref "watermark/java/getting-started/system-requirements.md" >}}) system with a JDK installed, and Maven or an IDE that works with Maven projects, such as IntelliJ IDEA or Eclipse.
- **5 minutes** of your spare time.

## Preparing

1. Create a new Maven project.
2. [Add]({{< ref "watermark/java/getting-started/installation.md" >}}) the GroupDocs repository and the **groupdocs-watermark** dependency to the `pom.xml` file of the project.
3. Create a class with a `main` method.

## Coding

1. Create an instance of the `Watermarker` class for the local document. You can specify an absolute or relative path:
   ```java
   Watermarker watermarker = new Watermarker("C:\\Docs\\sample.docx");
   ```
2. Create an instance of the `TextWatermark` class and specify the desired text and font for the watermark:
   ```java
   TextWatermark watermark = new TextWatermark("Hello, world!", new Font("Arial", 36));
   ```
3. Apply the watermark:
   ```java
   watermarker.add(watermark);
   ```
4. Save the resulting document:
   ```java
   watermarker.save("C:\\Docs\\watermarked-sample.docx");
   ```
5. Close the watermarker to release the document:
   ```java
   watermarker.close();
   ```

Full code:

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.common.HorizontalAlignment;
import com.groupdocs.watermark.common.VerticalAlignment;
import com.groupdocs.watermark.watermarks.Color;
import com.groupdocs.watermark.watermarks.Font;
import com.groupdocs.watermark.watermarks.FontStyle;
import com.groupdocs.watermark.watermarks.TextWatermark;

public class HelloWorld {
    public static void main(String[] args) {
        // Specify an absolute or relative path to your document.
        try (Watermarker watermarker = new Watermarker("C:\\Docs\\sample.docx")) {
            // Specify the desired text and font for the watermark
            TextWatermark watermark = new TextWatermark("Test watermark",
                    new Font("Arial", 36, FontStyle.Bold | FontStyle.Italic));

            watermark.setHorizontalAlignment(HorizontalAlignment.Center);
            watermark.setVerticalAlignment(VerticalAlignment.Center);

            watermark.setOpacity(0.4);
            watermark.setRotateAngle(45);
            watermark.setForegroundColor(Color.getRed());

            // Apply the watermark
            watermarker.add(watermark);
            // Save the resulting document
            watermarker.save("C:\\Docs\\watermarked-sample.docx");
        }
    }
}
```

`Watermarker` implements `java.io.Closeable`, so the try-with-resources statement closes it for you.

Additionally, if you are certain about your file extension or know the document type in advance, you can specify the file type through the [LoadOptions](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.options/loadoptions/) class. Specifying it eliminates the need for format detection, enabling faster and more efficient document processing:

```java
import com.groupdocs.watermark.Watermarker;
import com.groupdocs.watermark.common.FileType;
import com.groupdocs.watermark.common.FormatFamily;
import com.groupdocs.watermark.options.LoadOptions;

String filePath = "C:\\Docs\\sample.docx";
LoadOptions loadOptions = new LoadOptions();
// FileType.fromExtension expects the extension with the period, for example ".docx"
loadOptions.setFileType(FileType.fromExtension(filePath.substring(filePath.lastIndexOf('.'))));

// Or set the format family directly when you load a document from a stream, for example:
// loadOptions.setFormatFamily(FormatFamily.WordProcessing);

try (Watermarker watermarker = new Watermarker(filePath, loadOptions)) {
    // ....
}
```

## Running

Run the program. A new watermarked document will appear in the specified path.

!["Hello, world!" example](/watermark/net/images/hello-world.png)

## What's next

Congratulations! You have added a simple text watermark to a document. Read the [Developer guide]({{< ref "watermark/java/developer-guide" >}}) and [API reference](https://reference.groupdocs.com/watermark/java/) to learn how to customize text watermarks, add images as watermarks, search documents for existing watermarks, and much more.
