---
id: removing-found-watermarks
url: watermark/net/removing-found-watermarks
title: Removing found watermarks
weight: 3
description: "This article explains that how to remove found watermarks while using GroupDocs. Watermarks API."
keywords: remove found watermarks
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
## Remove watermark

GroupDocs.Watermark API enables you to easily [find](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/methods/search) and remove a particular [watermark](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search/possiblewatermark) from a document. Following code serves this purpose.

**AdvancedUsage.SearchAndRemoveWatermarks.RemoveWatermark**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    PossibleWatermarkCollection possibleWatermarks = watermarker.Search();

    // Remove possible watermark at the specified index from the document.
    possibleWatermarks.RemoveAt(0);

    // Remove specified possible watermark from the document.
    possibleWatermarks.Remove(possibleWatermarks[0]);

    watermarker.Save("document.pdf");
}
```

## Remove watermark with particular text formatting

GroupDocs.Watermark also enables you to search and remove the watermarks on the basis of some particular [text formatting](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textformattingsearchcriteria). You can provide a search criterion containing [font name](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textformattingsearchcriteria/properties/fontname), size, [color](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search.searchcriteria/textformattingsearchcriteria/properties/foregroundcolorrange) etc and the API will find the watermarks with matching properties. Following code snippet shows how to search and remove watermarks with a particular text formatting.

**AdvancedUsage.SearchAndRemoveWatermarks.RemoveWatermarkWithParticularTextFormatting**

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
    watermarks.Clear();

    watermarker.Save("document.pdf");
}
```

## Remove hyperlink watermarks

GroupDocs.Watermark API allows you to search and remove [hyperlinks](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.search/hyperlinkpossiblewatermark) in a document of any supported format. Following code sample shows how to find and remove hyperlinks with a particular URL from a document.

**AdvancedUsage.SearchAndRemoveWatermarks.RemoveHyperlinksWithParticularUrl**

```csharp
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\document.pdf"
using (Watermarker watermarker = new Watermarker("document.pdf"))
{
    PossibleWatermarkCollection watermarks = watermarker.Search(new TextSearchCriteria(new Regex(@"someurl\.com")));
    for (int i = watermarks.Count - 1; i >= 0; i--)
    {
        // Ensure that only hyperlinks will be removed.
        if (watermarks[i] is HyperlinkPossibleWatermark)
        {
            // Output the full url of the hyperlink
            Console.WriteLine(watermarks[i].Text);

            // Remove hyperlink from the document
            watermarks.RemoveAt(i);
        }
    }

    watermarker.Save("document.pdf");
}
```

## More resources

### GitHub examples

You may easily run the code above and see the feature in action in our GitHub examples:

* [GroupDocs.Watermark for .NET examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-.NET)
* [GroupDocs.Watermark for Java examples](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Java)

### Free online document watermarking App

Along with full featured .NET library we provide simple, but powerful free Apps.

You are welcome to add watermark to PDF, DOC, DOCX, PPT, PPTX, XLS, XLSX, Emails and more with our free online [Free Online Document Watermarking App](https://products.groupdocs.app/watermark).
