---
id: searching-watermarks
url: watermark/java/searching-watermarks
title: Searching watermarks
weight: 1
description: "This article explains how to search watermarks while using GroupDocs. Watermarks Java API."
keywords: search watermarks
productName: GroupDocs.Watermark for Java
hideChildren: False
---
## Searching possible watermarks 

GroupDocs.Watermark API allows you to search the possible watermarks placed in any document. You can also search the watermarks that are added using some third-party tool. The API provides [search()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#search()) method to search watermarks in a whole document or in any part of the document. Following code snippet shows how to find and get all possible watermarks in a document.

**advanced\_usage.searching\_and\_modifying\_watermarks.SearchWatermark**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
PossibleWatermarkCollection possibleWatermarks = watermarker.search();                                   
for (PossibleWatermark possibleWatermark : possibleWatermarks)                                           
{                                                                                                        
    if (possibleWatermark.getImageData() != null)                                                        
    {                                                                                                    
        System.out.println(possibleWatermark.getImageData().length);                                     
    }                                                                                                    
                                                                                                         
    System.out.println(possibleWatermark.getText());                                                     
    System.out.println(possibleWatermark.getX());                                                        
    System.out.println(possibleWatermark.getY());                                                        
    System.out.println(possibleWatermark.getRotateAngle());                                              
    System.out.println(possibleWatermark.getWidth());                                                    
    System.out.println(possibleWatermark.getHeight());                                                   
}                                                                                                        
                                                                                                         
watermarker.close();                                                                                     
```

## Search criteria

Usually, large documents may contain too many objects which can be considered as watermarks. Parameterless overload of [search()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#search()) method returns only some of them, e.g. backgrounds or floating objects which could have been added during document post-processing. You can use [search criteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/SearchCriteria) to find objects with some specific parameters.

### Text search criteria

Following code snippet shows how to search for the watermarks that meet a particular [text criterion](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/TextSearchCriteria).

**advanced\_usage.searching\_and\_modifying\_watermarks.SearchWatermarkWithSearchString**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
// Search by exact string                                                                                
TextSearchCriteria textSearchCriteria = new TextSearchCriteria("© 2017");                                
                                                                                                         
// Find all possible watermarks containing some specific text                                            
PossibleWatermarkCollection possibleWatermarks = watermarker.search(textSearchCriteria);                 
                                                                                                         
System.out.println("Found " + possibleWatermarks.getCount() + " possible watermark(s)");                 
                                                                                                         
watermarker.close();                                                                                     
```

### Regular expression search criteria  

Regular expressions are also supported by [TextSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/TextSearchCriteria). The below sample code uses a regular expression to search for watermarks.

**advanced\_usage.searching\_and\_modifying\_watermarks.SearchWatermarkWithRegularExpression**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
Pattern pattern = Pattern.compile("© \\d{4}$");                                                          
                                                                                                         
// Search by regular expression                                                                          
TextSearchCriteria textSearchCriteria = new TextSearchCriteria(pattern);                                 
                                                                                                         
// Find possible watermarks using regular expression                                                     
PossibleWatermarkCollection possibleWatermarks = watermarker.search(textSearchCriteria);                 
                                                                                                         
System.out.println("Found " + possibleWatermarks.getCount() + " possible watermark(s).");                
                                                                                                         
watermarker.close();                                                                                     
```

{{< alert style="info" >}}
What happens when the user is passing [TextSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/TextSearchCriteria) instance to the method?
1. It searches fragments of document's main text which match regular expression (or contain exact search string)
2. It checks text of other objects (shapes, XObjects, annotations etc.) if they match regular expression (or contain exact search string)
  
Search in the main text of a document is performed only if you pass [TextSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/TextSearchCriteria) instance to [search()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#search(com.groupdocs.watermark.search.SearchCriteria)) method.
{{< /alert >}}

### Image search criteria
Sometimes a document can contain image watermarks, and it's necessary to find them using sample picture. For example, you may want to find all possible image watermarks that are similar to a company logo. Following sample code searches for image watermarks that resemble with a particular image.
**advanced\_usage.searching\_and\_modifying\_watermarks.SearchImageWatermark**
```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
// Initialize criteria with the image                                                                    
ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("watermark.jpg");        
                                                                                                         
//Set maximum allowed difference between images                                                          
imageSearchCriteria.setMaxDifference(0.9);                                                               
                                                                                                         
PossibleWatermarkCollection possibleWatermarks = watermarker.search(imageSearchCriteria);                
                                                                                                         
System.out.println("Found " + possibleWatermarks.getCount() + " possible watermark(s).");                
                                                                                                         
watermarker.close();                                                                                     
```

[setMaxDifference()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/ImageSearchCriteria#setMaxDifference(double)) method is used to set maximum allowed difference between sample image and possible watermark. The value should be between 0 and 1. The value 0 means that only identical images will be found.

Using of [ImageDctHashSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/ImageDctHashSearchCriteria) is the most efficient way to find image watermark by a sample. This criterion uses DCT (Discrete Cosine Transform) based perceptual hash for image similarity comparison. But there are other image search criteria that are based on other algorithms:

*   [ImageColorHistogramSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/ImageColorHistogramSearchCriteria) uses image color histograms for calculating image similarity. This criterion is invariant to rotation, scaling, and translation of the image.
*   [ImageThumbnailSearchCriteria](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/ImageThumbnailSearchCriteria) uses image binarized thumbnail for calculating image similarity. This criterion is invariant to rotation, scaling and insignificant changes of the color palette.

### Combined search criteria

GroupDocs.Watermark API also allows you to search watermarks by a combination ([And](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/AndSearchCriteria), [Or](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/OrSearchCriteria), [Not](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/NotSearchCriteria)) of different search criteria. Following sample code shows how to search watermark with the combination of different search criteria.

**advanced\_usage.searching\_and\_modifying\_watermarks.SearchWatermarkWithCombinedSearch**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
ImageSearchCriteria imageSearchCriteria = new ImageDctHashSearchCriteria("logo.png");             
imageSearchCriteria.setMaxDifference(0.9);                                                               
                                                                                                         
TextSearchCriteria textSearchCriteria = new TextSearchCriteria("Company Name");                          
                                                                                                         
RotateAngleSearchCriteria rotateAngleSearchCriteria = new RotateAngleSearchCriteria(30, 60);             
                                                                                                         
SearchCriteria combinedSearchCriteria = imageSearchCriteria.or(textSearchCriteria)                       
                                                           .and(rotateAngleSearchCriteria);              
PossibleWatermarkCollection possibleWatermarks = watermarker.search(combinedSearchCriteria);             
                                                                                                         
System.out.println("Found " + possibleWatermarks.getCount() + " possible watermark(s).");                
                                                                                                         
watermarker.close();                                                                                     
```

### Text formatting search criteria

GroupDocs.Watermark also enables you to search the watermarks on the basis of some particular text formatting. You can provide a search criterion containing font name, size, color etc and the API will find the watermarks with matching properties. Following code snippet shows how to search watermark with a particular [text formatting](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/TextFormattingSearchCriteria).

**advanced\_usage.searching\_and\_modifying\_watermarks.SearchWatermarkWithParticularTextFormatting**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
TextFormattingSearchCriteria criteria = new TextFormattingSearchCriteria();                              
criteria.setForegroundColorRange(new ColorRange());                                                      
criteria.getForegroundColorRange().setMinHue(-5);                                                        
criteria.getForegroundColorRange().setMaxHue(10);                                                        
criteria.getForegroundColorRange().setMinBrightness(0.01f);                                              
criteria.getForegroundColorRange().setMaxBrightness(0.99f);                                              
criteria.setBackgroundColorRange(new ColorRange());                                                      
criteria.getBackgroundColorRange().setEmpty(true);                                                       
criteria.setFontName("Arial");                                                                           
criteria.setMinFontSize(19);                                                                             
criteria.setMaxFontSize(42);                                                                             
criteria.setFontBold(true);                                                                              
                                                                                                         
PossibleWatermarkCollection watermarks = watermarker.search(criteria);                                   
// The code for working with found watermarks goes here.                                                 
                                                                                                         
System.out.println("Found " + watermarks.getCount() + " possible watermark(s).");                        
                                                                                                         
watermarker.close();                                                                                     
```

## Searching watermarks in particular objects

This feature allows you to specify which objects should be included in watermark search. Restricting searchable objects, you can significantly increase search performance. Following sample code shows how to set [searchable objects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/WatermarkerSettings#setSearchableObjects(com.groupdocs.watermark.search.SearchableObjects)) globally (for all documents that will be created after that).

**advanced\_usage.searching\_and\_modifying\_watermarks.SearchWatermarkInParticularObjectsAllInstances**

```java
WatermarkerSettings settings = new WatermarkerSettings();                                                                                                
settings.setSearchableObjects(new SearchableObjects());                                                                                                  
settings.getSearchableObjects().setWordProcessingSearchableObjects(WordProcessingSearchableObjects.Hyperlinks | WordProcessingSearchableObjects.Text);   
settings.getSearchableObjects().setSpreadsheetSearchableObjects(SpreadsheetSearchableObjects.HeadersFooters);                                            
settings.getSearchableObjects().setPresentationSearchableObjects(PresentationSearchableObjects.SlidesBackgrounds | PresentationSearchableObjects.Shapes);
settings.getSearchableObjects().setDiagramSearchableObjects(DiagramSearchableObjects.None);                                                              
settings.getSearchableObjects().setPdfSearchableObjects(PdfSearchableObjects.All);                                                                       
                                                                                                                                                         
String[] files = { "document.docx",                                                                                                             
                   "spreadsheet.xlsx",                                                                                                          
                   "presentation.pptx",                                                                                                         
                   "diagram.vsdx",                                                                                                              
                   "document.pdf" };                                                                                                            
                                                                                                                                                         
for (String file : files)                                                                                                                                
{                                                                                                                                                        
    Watermarker watermarker = new Watermarker(file, settings);                                                                                           
                                                                                                                                                         
    PossibleWatermarkCollection watermarks = watermarker.search();                                                                                       
                                                                                                                                                         
    // The code for working with found watermarks goes here.                                                                                             
                                                                                                                                                         
    System.out.println("In " + new File(file).getName() + " found " + watermarks.getCount() + " possible watermark(s).");                                
                                                                                                                                                         
    watermarker.close();                                                                                                                                 
}                                                                                                                                                        
```

### Searching for hyperlink watermarks  

You can also set [searchable objects](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker#setSearchableObjects(com.groupdocs.watermark.search.SearchableObjects)) for a particular [Watermarker](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark/Watermarker) instance as shown in the sample code below.

**advanced\_usage.searching\_and\_modifying\_watermarks.SearchWatermarkInParticularObjectsForParticularDocument**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
// Search for hyperlinks only.                                                                           
watermarker.getSearchableObjects().setPdfSearchableObjects(PdfSearchableObjects.Hyperlinks);             
PossibleWatermarkCollection watermarks = watermarker.search();                                           
                                                                                                         
// The code for working with found watermarks goes here.                                                 
                                                                                                         
System.out.println("Found " + watermarks.getCount() + " possible watermark(s).");                        
                                                                                                         
watermarker.close();                                                                                     
```

## Searching text watermark skipping unreadable characters

This feature allows finding text watermark even if it contains unreadable characters between the letters. The following code sample shows how to [skip unreadable characters](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.search/TextSearchCriteria#setSkipUnreadableCharacters(boolean)) when searching for the watermark.

**advanced\_usage.searching\_and\_modifying\_watermarks.SearchTextWatermarkSkippingUnreadableCharacters**

```java
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\document.pdf"
Watermarker watermarker = new Watermarker("document.pdf");                                      
                                                                                                         
String watermarkText = "Company name";                                                                   
TextSearchCriteria criterion = new TextSearchCriteria(watermarkText);                                    
                                                                                                         
// Enable skipping of unreadable characters                                                              
criterion.setSkipUnreadableCharacters(true);                                                             
                                                                                                         
PossibleWatermarkCollection result = watermarker.search(criterion);                                      
                                                                                                         
// ...                                                                                                   
                                                                                                         
System.out.println("Found " + result.getCount() + " possible watermark(s).");                            
                                                                                                         
watermarker.close();                                                                                     
```

