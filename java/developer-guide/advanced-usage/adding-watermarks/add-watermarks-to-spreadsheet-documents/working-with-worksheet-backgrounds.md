---
id: working-with-worksheet-backgrounds
url: watermark/java/working-with-worksheet-backgrounds
title: Working with worksheet backgrounds
weight: 1
description: "This article explains how to work with worksheet backgrounds while using GroupDocs watermarking Java API"
productName: GroupDocs.Watermark for Java
hideChildren: False
---
## Extracting information about all worksheet backgrounds in an Excel document

The API allows you to extract [information](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/SpreadsheetWorksheet#getBackgroundImage()) about all the worksheet backgrounds in an Excel document as shown in the following code sample.

**advanced\_usage.add\_watermarks\_to\_spreadsheets.SpreadsheetGetInformationOfWorksheetBackgrounds**

```java
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\spreadsheet.xlsx"
Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions);                             
                                                                                                                 
SpreadsheetContent content = watermarker.getContent(SpreadsheetContent.class);                                   
for (SpreadsheetWorksheet worksheet : content.getWorksheets())                                                   
{                                                                                                                
    if (worksheet.getBackgroundImage() != null)                                                                  
    {                                                                                                            
        System.out.println(worksheet.getBackgroundImage().getWidth());                                           
        System.out.println(worksheet.getBackgroundImage().getHeight());                                          
        System.out.println(worksheet.getBackgroundImage().getBytes().length);                                    
    }                                                                                                            
}                                                                                                                
                                                                                                                 
watermarker.close();                                                                                             
```

## Removing a particular background

Following code sample can be used to remove the [background](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/SpreadsheetWorksheet#getBackgroundImage()) of a particular worksheet.

**advanced\_usage.add\_watermarks\_to\_spreadsheets.SpreadsheetRemoveWorksheetBackground**

```java
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\spreadsheet.xlsx"
Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions);                             
                                                                                                                 
SpreadsheetContent content = watermarker.getContent(SpreadsheetContent.class);                                   
content.getWorksheets().get_Item(0).setBackgroundImage(null);                                                    
                                                                                                                 
watermarker.save("spreadsheet.xlsx");                                                                  
                                                                                                                 
watermarker.close();                                                                                             
```

## Adding watermark to all backgrounds in an Excel worksheet

You can [add](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/WatermarkableImage#add(com.groupdocs.watermark.Watermark)) watermark to the background images that belong to an Excel document as shown in the below code sample.

**advanced\_usage.add\_watermarks\_to\_spreadsheets.SpreadsheetAddWatermarkToBackgroundImages**

```java
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\spreadsheet.xlsx"
Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions);                             
                                                                                                                 
// Initialize image or text watermark                                                                            
TextWatermark watermark = new TextWatermark("Protected image", new Font("Arial", 8));                            
watermark.setHorizontalAlignment(HorizontalAlignment.Center);                                                    
watermark.setVerticalAlignment(VerticalAlignment.Center);                                                        
watermark.setRotateAngle(45);                                                                                    
watermark.setSizingType(SizingType.ScaleToParentDimensions);                                                     
watermark.setScaleFactor(1);                                                                                     
                                                                                                                 
SpreadsheetContent content = watermarker.getContent(SpreadsheetContent.class);                                   
for (SpreadsheetWorksheet worksheet : content.getWorksheets())                                                   
{                                                                                                                
    if (worksheet.getBackgroundImage() != null)                                                                  
    {                                                                                                            
        // Add watermark to the image                                                                            
        worksheet.getBackgroundImage().add(watermark);                                                           
    }                                                                                                            
}                                                                                                                
                                                                                                                 
watermarker.save("spreadsheet.xlsx");                                                                  
                                                                                                                 
watermarker.close();                                                                                             
```

## Settings background image for charts

GroupDocs.Watermark for Java also allows you to set the [background image](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/SpreadsheetChart#getImageFillFormat()) for a chart inside an Excel document. Following code sample shows how to achieve this functionality.

**advanced\_usage.add\_watermarks\_to\_spreadsheets.SpreadsheetSetBackgroundImageForChart**

```java
SpreadsheetLoadOptions loadOptions = new SpreadsheetLoadOptions();                                                                                 
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\spreadsheet.xlsx"                                  
Watermarker watermarker = new Watermarker("spreadsheet.xlsx", loadOptions);                                                               
                                                                                                                                                   
SpreadsheetContent content = watermarker.getContent(SpreadsheetContent.class);                                                                     
                                                                                                                                                   
File imageFile = new File("test.png");                                                                                                      
byte[] imageBytes = new byte[(int) imageFile.length()];                                                                                            
InputStream imageInputStream = new FileInputStream(imageFile);                                                                                     
imageInputStream.read(imageBytes);                                                                                                                 
imageInputStream.close();                                                                                                                          
                                                                                                                                                   
content.getWorksheets().get_Item(0).getCharts().get_Item(0).getImageFillFormat().setBackgroundImage(new SpreadsheetWatermarkableImage(imageBytes));
content.getWorksheets().get_Item(0).getCharts().get_Item(0).getImageFillFormat().setTransparency(0.5);                                             
content.getWorksheets().get_Item(0).getCharts().get_Item(0).getImageFillFormat().setTileAsTexture(true);                                           
                                                                                                                                                   
watermarker.save("spreadsheet.xlsx");                                                                                                    
                                                                                                                                                   
watermarker.close();                                                                                                                               
```
