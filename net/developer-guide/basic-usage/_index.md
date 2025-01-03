---
id: basic-usage
url: watermark/net/basic-usage
title: Basic usage
weight: 1
description: ""
keywords: 
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
GroupDocs.Watermark library provides the ability to manipulate different watermark types such as [TextWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/textwatermark), [ImageWatermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarks/imagewatermark). These watermarks could be added to documents, updated, removed, or searched inside already watermarked documents. Our product also provides information about document type and structure - file type, size, page count, etc. and generates document page previews based on provided options.  

Here are the main concepts of the GroupDocs.Watermark API:

* [Watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker) is the main class that contains all the required methods for manipulating document watermarks.
* Most part of the methods expect different options to add, update, search or remove watermarks inside a document.
* The [Watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker) class implements an [IDisposable](https://docs.microsoft.com/en-us/dotnet/api/system.idisposable) interface to correctly release used resources - like safely closing document streams when all operations are completed.

## Articles in this section

* [Add text watermarks]({{< ref "add-text" >}} "Add text watermarks")
* [Add image watermarks]({{< ref "add-image" >}} "Add image watermarks")
* [Adding repeated watermarks]({{< ref "adding-repeated-watermarks" >}} "Adding repeated watermarks")
* [Customize watermarks]({{< ref "customize" >}} "Customize watermarks")
* [Update watermarks]({{< ref "update" >}} "Update watermarks")
* [Clear watermarks]({{< ref "clear" >}} "Clear watermarks")
* [Get supported file formats]({{< ref "get-supported-file-formats" >}} "Get supported file formats")
* [Get document info]({{< ref "get-document-info" >}} "Get document info")

## Referencing required namespaces

The following code shows how to include the required namespaces for all code examples.  

```csharp
using GroupDocs.Watermark;
using GroupDocs.Watermark.Common;
using GroupDocs.Watermark.Contents;
using GroupDocs.Watermark.Options;
using GroupDocs.Watermark.Search;
using GroupDocs.Watermark.Watermarks;
```

## Watermarker object definition

The following code shows the most used code pattern to define the [Watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker) object and call its methods.

```csharp
// Add text watermark to PDF document
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 36, FontStyle.Bold | FontStyle.Italic));
    watermarker.Add(watermark);
    watermarker.Save("Watermarked_document.pdf");
}
```

Let’s review common usage scenarios when documents and watermarks are stored in a local drive and you want to manage them using GroupDocs.Watermark API:

## More resources

### Advanced usage topics

To learn more about document watermarking features and learn how to manage watermarks and more, please refer to the [advanced usage section]({{< ref "watermark/net/developer-guide/advanced-usage/_index.md" >}}).

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Watermark for .NET examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-.NET)
* [GroupDocs.Watermark for Java examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java)

### Free online document watermarking App

Along with a full-featured .NET library, we provide simple, but powerful free Apps.

You are welcome to add watermark to PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, emails, and more with our [Free Online Document Watermarking Apps](https://products.groupdocs.app/watermark).
