---
id: preview
url: watermark/net/basic-usage/preview
title: Document preview
weight: 7
description: This article shows how to get document preview.
keywords: 
productName: GroupDocs.Watermark for .NET
hideChildren: True
---

GroupDocs.Watermark library equipped with the capability to generate preview images for every page of your documents, simplifying your workflow and enhancing efficiency. With this feature, users can  effortlessly preview their documents with a glance, enabling swift navigation and ensuring seamless accessibility to crucial content. 

## Generate document preview

To create document preview:
1. [Create](https://reference.groupdocs.com/net/watermark/groupdocs.watermark/watermarker/constructors/4) an instance of the `Watermarker` class for a local file or file stream;

2. Instantiate the [PreviewOptions](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.options/previewoptions/) object with the delegate for stream creation (see event handler [CreatePageStream](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.options/createpagestream/));
If you need to implement custom image preview stream disposing you have to pass additional argument [ReleasePageStream](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.options/releasepagestream/) to clean up resources.  

3. Specify [PreviewFormat](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.options/previewoptions.previewformats/) - PNG / JPG / BMP, and other properties like PageNumbers for which you want to generate preview. Additionaly for most of documents you can use specific PreviewOptions overloads, like [PdfPreviewOptions](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.options.pdf/pdfpreviewoptions/), [SpreadsheetPreviewOptions](https://reference.groupdocs.com/watermark/net/groupdocs.watermark.options.spreadsheet/spreadsheetpreviewoptions/) which allows to configure the resolution for the generated images in dots per inch.

4. Call method GeneratePreview method of the Watermarker object and pass PreviewOptions to it.


```csharp
string outputDirectory = Constants.GetOutputDirectoryPath();

using (Watermarker watermarker = new Watermarker("sample.pdf"))
{
    CreatePageStream createPageStreamDelegate = delegate(int number)
    {
        string previewImageFileName = Path.Combine(outputDirectory, 
            string.Format("page{0}.png", number));
        return File.OpenWrite(previewImageFileName);
    };

    ReleasePageStream releasePageStreamDelegate = delegate(int number, Stream stream)
    {
        stream.Close();
    };

    PreviewOptions previewOptions = new PreviewOptions(createPageStreamDelegate,
        releasePageStreamDelegate)
    {
        PreviewFormat = PreviewOptions.PreviewFormats.PNG,
        PageNumbers = new []{1, 2}
    };
    
    watermarker.GeneratePreview(previewOptions);
}
```
Run the program. It will create images in the outputDirectory corresponding to the pages of the document.

