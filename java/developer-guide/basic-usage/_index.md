---
id: basic-usage
url: watermark/java/basic-usage
title: Basic Usage
weight: 1
description: ""
keywords: 
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
GroupDocs.Watermark library provides the ability to manipulate different watermark types such as [TextWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/TextWatermark), [ImageWatermark](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.watermarks/ImageWatermark). These watermarks could be added to documents, updated, removed, or searched inside already watermarked documents. Our product also provides information about document type and structure - file type, size, page count, etc. and generates document page previews based on provided options.  

Here are the main GroupDocs.Watermark API concepts:

*   [Watermarker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker) is the main class that contains all the required methods for manipulating document watermarks.
    
*   Most part of the methods expect different options to add, update, search, or remove watermarks inside a document.
    
*   [Watermarker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker) class implements the [Closable](https://docs.oracle.com/javase/7/docs/api/java/io/Closeable.html) interface to correctly release used resources - like safely closing document streams when all operations are completed.
    

## Watermarker object definition

The following code shows еру most used code pattern to define [Watermarker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker) object and call its methods.

```java
// Add text watermark to PDF document
Watermarker watermarker = new Watermarker("document.pdf");
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 36, FontStyle.Bold | FontStyle.Italic));
watermarker.add(watermark);
watermarker.save("Watermarked_document.pdf");
watermarker.close(); 
```

Let’s review common usage scenarios when documents and watermarks are stored in a local drive and you want to manage them using GroupDocs.Watermark API:

## More resources

### Advanced usage topics

To learn more about document watermarking features and get familiar how to manage watermarks and more, please refer to the [advanced usage section]({{< ref "/watermark/java/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

*   [GroupDocs.Watermark for .NET examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-.NET)
    
*   [GroupDocs.Watermark for Java examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java)
    

### Free online document watermarking App

Along with a full-featured Java library, we provide simple, but powerful free Apps.

You are welcome to add watermark to PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, emails, and more with our [Free Online Document Watermarking Apps](https://products.groupdocs.app/watermark).
