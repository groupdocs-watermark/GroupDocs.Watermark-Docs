---
id: email-attachments
url: watermark/java/email-attachments
title: Email attachments
weight: 1
description: "This article shows how to get the information about the attachments."
keywords: Email attachments
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---
## Extracting all attachments from email message

GroupDocs.Watermark allows you to get the information about the [attachments](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/EmailContent#getAttachments()) in an email message. Below is the code snippet for extracting attachments from Email.

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailExtractAllAttachments**

```java
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                       
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg"      
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                              
                                                                                                             
EmailContent content = watermarker.getContent(EmailContent.class);                                           
for (EmailAttachment attachment : content.getAttachments())                                                  
{                                                                                                            
    System.out.println("Name: " + attachment.getName());                                                     
    System.out.println("File format: " + attachment.getDocumentInfo().getFileType());                        
                                                                                                             
    FileOutputStream outputStream = new FileOutputStream("SampleFiles\\Output" + "\\" + attachment.getName());
    outputStream.write(attachment.getContent());                                                             
    outputStream.close();                                                                                    
}                                                                                                            
                                                                                                             
watermarker.close();                                                                                         
```

## Removing particular attachment from email message

Using GroupDocs.Watermark, you can [remove](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.common/RemoveOnlyListBase#remove(T)) any particular attachment from an email message. Below is the code for removing specific attachment:

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailRemoveAttachment**

```java
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                         
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg"        
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                                
                                                                                                               
EmailContent content = watermarker.getContent(EmailContent.class);                                             
for (int i = content.getAttachments().getCount() - 1; i >= 0; i--)                                             
{                                                                                                              
    EmailAttachment attachment = content.getAttachments().get_Item(i);                                         
                                                                                                               
    // Remove all attached files with a particular name and format                                             
    if (attachment.getName().contains("sample") && attachment.getDocumentInfo().getFileType() == FileType.DOCX)
    {                                                                                                          
        content.getAttachments().removeAt(i);                                                                  
    }                                                                                                          
}                                                                                                              
                                                                                                               
// Save changes                                                                                                
watermarker.save("message.msg");                                                                     
                                                                                                               
watermarker.close();                                                                                           
```

## Adding attachment to email message

You can also add attachments to the email messages using GroupDocs.Watermark. Following is the code sample for adding an attachment:

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailAddAttachment**

```java
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                 
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg"
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                        
                                                                                                       
EmailContent content = watermarker.getContent(EmailContent.class);                                     
                                                                                                       
File attachmentFile = new File("sample.msg");                                                 
byte[] attachmentBytes = new byte[(int) attachmentFile.length()];                                      
InputStream attachmentInputStream = new FileInputStream(attachmentFile);                               
attachmentInputStream.read(attachmentBytes);                                                           
attachmentInputStream.close();                                                                         
                                                                                                       
content.getAttachments().add(attachmentBytes, "sample.msg");                                           
                                                                                                       
// Save changes                                                                                        
watermarker.save("message.msg");                                                             
                                                                                                       
watermarker.close();                                                                                   
```
