---
id: add-watermarks-to-email-attachments
url: watermark/java/add-watermarks-to-email-attachments
title: Add watermarks to email attachments
weight: 4
description: ""
keywords: 
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
The API allows you to add watermark to all the [attachments](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/EmailContent#getAttachments()) of supported types in an email message as shown in the following code sample.

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailAddWatermarkToAllAttachments**

```java
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));                  
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                 
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg"
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                        
                                                                                                       
EmailContent content = watermarker.getContent(EmailContent.class);                                     
for (EmailAttachment attachment : content.getAttachments())                                            
{                                                                                                      
    // Check if the attached file is supported by GroupDocs.Watermark                                  
    IDocumentInfo info = attachment.getDocumentInfo();                                                 
    if (info.getFileType() != FileType.Unknown && !info.isEncrypted())                                 
    {                                                                                                  
        // Load the attached document                                                                  
        Watermarker attachedWatermarker = attachment.createWatermarker();                              
                                                                                                       
        // Add watermark                                                                               
        attachedWatermarker.add(watermark);                                                            
                                                                                                       
        // Save changes in the attached file                                                           
        attachment.updateContent(attachedWatermarker);                                                 
                                                                                                       
        attachedWatermarker.close();                                                                   
    }                                                                                                  
}                                                                                                      
                                                                                                       
// Save changes                                                                                        
watermarker.save("message.msg");                                                             
                                                                                                       
watermarker.close();                                                                                   
```
