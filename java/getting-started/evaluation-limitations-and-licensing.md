---
id: evaluation-limitations-and-licensing
url: watermark/java/evaluation-limitations-and-licensing
title: Evaluation Limitations and Licensing
weight: 6
description: The free evaluation version of GroupDocs.Watermark for Java works like the licensed one, but adds an evaluation message to the saved documents.
keywords: free watermark,license,watermark,api,evaluation,metered license,java
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
{{< alert style="info" >}}You can use GroupDocs.Watermark without a license. The evaluation version provides the same features as the licensed one; the only difference is an evaluation message in the saved documents.{{< /alert >}}

# Evaluation version limitations

You can easily download GroupDocs.Watermark for evaluation. The evaluation download is the same as the purchased download. The evaluation version simply becomes licensed when you add a few lines of code to apply the license. You will face the following limitation while using the API without a license.

| API Feature | Limitation |
| --- | --- |
| Document saving | An evaluation message is added to every saved document: "Created with evaluation version of GroupDocs.Watermark © Aspose Pty Ltd 2001-2026. All Rights Reserved." The year is the release year of the library. |

Where the evaluation message appears depends on the document format:

| Document format | Evaluation message |
| --- | --- |
| PDF | A watermark on every page. |
| Word processing | A paragraph or a watermark. |
| Spreadsheet | A locked shape and a footer. |
| Presentation | A locked shape on the slides. |
| Diagram (Visio) | A locked shape on the pages and a header. |
| Email | The subject of the message. |
| Image | A watermark on the image. |

Since version 26.11, evaluation mode has no other limits: you can load any number of documents, add any number of watermarks to a document, and add or remove document parts, such as found watermarks, attachments and hyperlinks.

## Licensing

The license file contains details such as the product name, number of developers it is licensed to, subscription expiry date and so on. It contains the digital signature, so don't modify the file. Even inadvertent addition of an extra line break into the file will invalidate it. You need to set a license before utilizing GroupDocs.Watermark API if you want to avoid its evaluation limitations.

The license can be loaded from a file or stream object. The `License` and `Metered` classes are in the `com.groupdocs.watermark.licenses` package.

### Setting license from file

The code below shows how to set the product license from a file.

```java
// For complete examples and data files, please go to https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java
import com.groupdocs.watermark.licenses.License;

// Initialize License
License license = new License();

// Set license
license.setLicense("C:\\Licenses\\GroupDocs.Watermark.lic");
```

{{< alert style="info" >}}Pass an absolute path to `setLicense(String)`. A relative file name is looked up in the folder of the GroupDocs.Watermark jar, not in the working directory. To set a license from a path relative to the working directory, use the `setLicense(java.nio.file.Path)` overload, for example `license.setLicense(Paths.get("GroupDocs.Watermark.lic"))`.{{< /alert >}}

### Setting license from stream

The following example shows how to load a license from a stream.

```java
// For complete examples and data files, please go to https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java
import com.groupdocs.watermark.licenses.License;

import java.io.FileInputStream;
import java.io.IOException;
import java.io.InputStream;

try (InputStream stream = new FileInputStream("GroupDocs.Watermark.lic")) {
    License license = new License();
    license.setLicense(stream);
} catch (IOException e) {
    System.out.println(e.getMessage());
}
```

{{< alert style="info" >}}
Calling `License.setLicense` multiple times is not harmful but simply wastes processor time. Call `License.setLicense` once in your startup code, before using GroupDocs.Watermark classes. To check whether a license is set, call the static `License.isValidLicense()` method.
{{< /alert >}}

### Setting metered license

You can also set a metered license as an alternative to the license file. It is a licensing mechanism that is used along with the existing licensing method. It is useful for the customers who want to be billed based on the usage of the API features. For more details, please refer to the [Metered Licensing FAQ](https://purchase.groupdocs.com/faqs/licensing/metered) section.

Here are the simple steps to use the `Metered` class:
* Create an instance of the `Metered` class.
* Pass the public and private keys to the `setMeteredKey` method.
* Do processing (perform task).
* Call the static `Metered.getConsumptionQuantity()` method. It returns the amount of data (in MB) processed so far.
* Call the static `Metered.getConsumptionCredit()` method. It returns the number of credits consumed so far.

Following is the sample code demonstrating how to set metered public and private keys.

```java
// For complete examples and data files, please go to https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java
import com.groupdocs.watermark.licenses.Metered;

String publicKey = ""; // Your public license key
String privateKey = ""; // Your private license key

Metered metered = new Metered();
metered.setMeteredKey(publicKey, privateKey);

// Get amount (MB) consumed
double amountConsumed = Metered.getConsumptionQuantity();

// Get count of credits consumed
double creditsConsumed = Metered.getConsumptionCredit();
```
