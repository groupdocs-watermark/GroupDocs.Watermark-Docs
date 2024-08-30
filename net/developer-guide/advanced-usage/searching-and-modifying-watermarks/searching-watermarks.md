---
id: searching-watermarks
url: watermark/net/searching-watermarks
title: Searching watermarks
weight: 1
description: "This article explains how to search watermarks while using GroupDocs. Watermarks API."
keywords: search watermarks
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
## Searching possible watermarks

GroupDocs.Watermark API allows you to search the possible watermarks placed in any document. You can also search the watermarks that are added using some third-party tool. The API provides [Search](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/search) method to search watermarks in a whole document or in any part of the document. Following code snippet shows how to find and get all possible watermarks in a document.

**AdvancedUsage.SearchAndRemoveWatermarks.SearchWatermark**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search();
    foreach (PossibleWatermark possibleWatermark in possibleWatermarks)
    {
        if (possibleWatermark.ImageData != null)
        {
            Console.WriteLine(possibleWatermark.ImageData.Length);
        }

        Console.WriteLine($"Text {possibleWatermark.Text}");
        Console.WriteLine($"X {possibleWatermark.X}");
        Console.WriteLine($"Y {possibleWatermark.Y}");
        Console.WriteLine($"RotateAngle {possibleWatermark.RotateAngle}");
        Console.WriteLine($"Width {possibleWatermark.Width}");
        Console.WriteLine($"Height {possibleWatermark.Height}");
        Console.WriteLine($"PageNumber {possibleWatermark.PageNumber}");
        Console.WriteLine("");
    }
}
```

## Search criteria

Usually, large documents may contain too many objects which can be considered as watermarks. Parameterless overload of [Search](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/search) method returns only some of them, e.g. backgrounds or floating objects which could have been added during document post-processing. You can use [search criteria](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/) to find objects with some specific parameters.

### Text search criteria

Following code snippet shows how to search for the watermarks that meet a particular [text criterion](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textsearchcriteria).

**AdvancedUsage.SearchAndRemoveWatermarks.SearchWatermarkWithSearchString**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    // Search by exact string
    TextSearchCriteria textSearchCriteria = new TextSearchCriteria("Â© 2017");
    // Find all possible watermarks containing some specific text
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search(textSearchCriteria);
    Console.WriteLine("Found {0} possible watermark(s)", possibleWatermarks.Count);
}
```

### Regular expression search criteria  

Regular expressions are also supported by [TextSearchCriteria](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textsearchcriteria). The below sample code uses a regular expression to search for watermarks.

**AdvancedUsage.SearchAndRemoveWatermarks.SearchWatermarkWithRegularExpression**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    Regex regex = new Regex(@"^Â© \d{4}$");
    // Search by regular expression
    TextSearchCriteria textSearchCriteria = new TextSearchCriteria(regex);
    // Find possible watermarks using regular expression
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search(textSearchCriteria);
    Console.WriteLine("Found {0} possible watermark(s).", possibleWatermarks.Count);
}
```

{{< alert style="info" >}}
What happens when the user is passing [TextSearchCriteria](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textsearchcriteria) instance to the method?

1. It searches fragments of document's main text which match regular expression (or contain exact search string)
2. It checks text of other objects (shapes, XObjects, annotations etc.) if they match regular expression (or contain exact search string)

Search in the main text of a document is performed only if you pass [TextSearchCriteria](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textsearchcriteria) instance to [Search](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.watermarker/search/methods/1) method.
{{< /alert >}}

### Image search criteria

Sometimes a document can contain image watermarks, and it's necessary to find them using sample picture. For example, you may want to find all possible image watermarks that are similar to a company logo. Following sample code searches for image watermarks that resemble with a particular image using.

**AdvancedUsage.SearchAndRemoveWatermarks.SearchImageWatermark**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    // Initialize criteria with the image
    ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("watermark.jpg");
    //Set maximum allowed difference between images
    imageSearchCriteria.MaxDifference = 0.9;
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search(imageSearchCriteria);
    Console.WriteLine("Found {0} possible watermark(s).", possibleWatermarks.Count);
}
```

[MaxDifference](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/imagesearchcriteria/properties/maxdifference) property is used to set maximum allowed difference between sample image and possible watermark. The value should be between 0 and 1. The value 0 means that only identical images will be found.
Using of [ImageDctHashSearchCriteria](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/imagedcthashsearchcriteria) is the most efficient way to find image watermark by a sample. This criterion uses DCT (Discrete Cosine Transform) based perceptual hash for image similarity comparison. But there are other image search criteria that are based on other algorithms:

* [ImageColorHistogramSearchCriteria](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/imagecolorhistogramsearchcriteria) uses image color histograms for calculating image similarity. This criterion is invariant to rotation, scaling, and translation of the image.
* [ImageThumbnailSearchCriteria](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/imagethumbnailsearchcriteria) uses image binarized thumbnail for calculating image similarity. This criterion is invariant to rotation, scaling and insignificant changes of the color palette.

### Combined search criteria

GroupDocs.Watermark API also allows you to search watermarks by a combination ([And](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/andsearchcriteria), [Or](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/orsearchcriteria), [Not](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/notsearchcriteria)) of different search criteria. Following sample code shows how to search watermark with the combination of different search criteria.

**AdvancedUsage.SearchAndRemoveWatermarks.SearchWatermarkWithCombinedSearch**

```csharp
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("logo.png");
    imageSearchCriteria.MaxDifference = 0.9;
    TextSearchCriteria textSearchCriteria = new TextSearchCriteria("Company Name");
    RotateAngleSearchCriteria rotateAngleSearchCriteria = new RotateAngleSearchCriteria(30, 60);
    SearchCriteria combinedSearchCriteria = imageSearchCriteria.Or(textSearchCriteria).And(rotateAngleSearchCriteria);
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search(combinedSearchCriteria);
    Console.WriteLine("Found {0} possible watermark(s).", possibleWatermarks.Count);
}
```

### Text formatting search criteria

GroupDocs.Watermark also enables you to search the watermarks on the basis of some particular text formatting. You can provide a search criterion containing font name, size, color etc and the API will find the watermarks with matching properties. Following code snippet shows how to search watermark with a particular [text formatting](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textformattingsearchcriteria).

**AdvancedUsage.SearchAndRemoveWatermarks.SearchWatermarkWithParticularTextFormatting**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    TextFormattingSearchCriteria criteria = new TextFormattingSearchCriteria();
    criteria.ForegroundColorRange = new ColorRange();
    criteria.ForegroundColorRange.MinHue = -5;
    criteria.ForegroundColorRange.MaxHue = 10;
    criteria.ForegroundColorRange.MinBrightness = 0.01f;
    criteria.ForegroundColorRange.MaxBrightness = 0.99f;
    criteria.BackgroundColorRange = new ColorRange();
    criteria.BackgroundColorRange.IsEmpty = true;
    criteria.FontName = "Arial";
    criteria.MinFontSize = 19;
    criteria.MaxFontSize = 42;
    criteria.FontBold = true;

    PossibleWatermarkCollection watermarks = watermarker.Search(criteria);

    // The code for working with found watermarks goes here.
    Console.WriteLine("Found {0} possible watermark(s).", watermarks.Count);
}
```

## Searching watermarks in particular objects

This feature allows you to specify which objects should be included in watermark search. Restricting searchable objects, you can significantly increase search performance. Following sample code shows how to set [searchable objects](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarkersettings/properties/searchableobjects) globally (for all documents that will be created after that).

**AdvancedUsage.SearchAndRemoveWatermarks.SearchWatermarkInParticularObjectsAllInstances**

```csharp
WatermarkerSettings settings = new WatermarkerSettings();
settings.SearchableObjects = new SearchableObjects
                             {
                                 WordProcessingSearchableObjects = WordProcessingSearchableObjects.Hyperlinks | WordProcessingSearchableObjects.Text,
                                 SpreadsheetSearchableObjects = SpreadsheetSearchableObjects.HeadersFooters,
                                 PresentationSearchableObjects = PresentationSearchableObjects.SlidesBackgrounds | PresentationSearchableObjects.Shapes,
                                 DiagramSearchableObjects = DiagramSearchableObjects.None,
                                 PdfSearchableObjects = PdfSearchableObjects.All
                             };
string[] files = { "document.docx", "spreadsheet.xlsx", "presentation.pptx",
                   "diagram.vsdx", "document.pdf" };
foreach (string file in files)
{
    using (Watermarker watermarker = new Watermarker(file, settings))
    {
        PossibleWatermarkCollection watermarks = watermarker.Search();

        // The code for working with found watermarks goes here.
        Console.WriteLine("In {0} found {1} possible watermark(s).", Path.GetFileName(file), watermarks.Count);
    }
}
```

### Searching for hyperlink watermarks  

You can also set [searchable objects](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/properties/searchableobjects) for a particular [Watermarker](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker) instance as shown in the sample code below.

**AdvancedUsage.SearchAndRemoveWatermarks.SearchWatermarkInParticularObjectsForParticularDocument**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    // Search for hyperlinks only.
    watermarker.SearchableObjects.PdfSearchableObjects = PdfSearchableObjects.Hyperlinks;
    PossibleWatermarkCollection watermarks = watermarker.Search();

    // The code for working with found watermarks goes here.
    Console.WriteLine("Found {0} hyperlink watermark(s).", watermarks.Count);
}
```

## Searching text watermark skipping unreadable characters

This feature allows finding text watermark even if it contains unreadable characters between the letters. The following code sample shows how to [skip unreadable characters](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textsearchcriteria/properties/skipunreadablecharacters) when searching for the watermark.

**AdvancedUsage.SearchAndRemoveWatermarks.SearchTextWatermarkSkippingUnreadableCharacters**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    string watermarkText = "Company name";
    TextSearchCriteria criterion = new TextSearchCriteria(watermarkText);

    // Enable skipping of unreadable characters
    criterion.SkipUnreadableCharacters = true;
    PossibleWatermarkCollection result = watermarker.Search(criterion);

    // ...
    Console.WriteLine("Found {0} possible watermark(s).", result.Count);
}
```
