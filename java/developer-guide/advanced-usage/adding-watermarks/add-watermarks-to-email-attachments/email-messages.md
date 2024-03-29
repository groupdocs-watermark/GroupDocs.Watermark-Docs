---
id: email-messages
url: watermark/java/email-messages
title: Email messages
weight: 2
description: Learn how to add watermark in Outlook email messages.
keywords: how to add watermark in outlook email
productName: GroupDocs.Watermark for Java
hideChildren: False
---
## Modifying body and subject of email message

GroupDocs.Watermark also allows you to modify the body and subject of an email message. Below is the code sample to modify [body](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/EmailContent#setBody(java.lang.String)) and [subject](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/EmailContent#setSubject(java.lang.String)) of an email Message:

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailUpdateEmailBody**

```java
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                 
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg"
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                        
                                                                                                       
EmailContent content = watermarker.getContent(EmailContent.class);                                     
                                                                                                       
// Set the plain text body                                                                             
content.setBody("Test plain text body");                                                               
                                                                                                       
// Set the html body                                                                                   
content.setHtmlBody("<html><body>Test html body</body></html>");                                       
                                                                                                       
// Set the email subject                                                                               
content.setSubject("Test subject");                                                                    
                                                                                                       
// Save changes                                                                                        
watermarker.save("message.msg");                                                             
                                                                                                       
watermarker.close();                                                                                   
```

## Embedding image to email message body

GroupDocs.Watermark also provides the feature of embedding images in the body of the email message. Following is the code sample for embedding an image in an email:

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailAddEmbeddedImage**

```java
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                                              
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg"                             
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                                                     
                                                                                                                                    
EmailContent content = watermarker.getContent(EmailContent.class);                                                                  
                                                                                                                                    
File imageFile = new File("sample.jpg");                                                                                     
byte[] imageBytes = new byte[(int) imageFile.length()];                                                                             
InputStream imageInputStream = new FileInputStream(imageFile);                                                                      
imageInputStream.read(imageBytes);                                                                                                  
imageInputStream.close();                                                                                                           
                                                                                                                                    
content.getEmbeddedObjects().add(imageBytes, "sample.jpg");                                                                         
EmailEmbeddedObject embeddedObject = content.getEmbeddedObjects().get_Item(content.getEmbeddedObjects().getCount() - 1);            
content.setHtmlBody("<html><body>This is an embedded image: <img src=\"cid:" + embeddedObject.getContentId() + "\"></body></html>");
watermarker.save("message.msg");                                                                                          
                                                                                                                                    
watermarker.close();                                                                                                                
```

## Removing all embedded images from email message body

You can also remove the embedded images from the body of the email message. Below is the code for removing embedded images:

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailRemoveEmbeddedImages**

```java
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                                
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg"               
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                                       
                                                                                                                      
EmailContent content = watermarker.getContent(EmailContent.class);                                                    
for (int i = content.getEmbeddedObjects().getCount() - 1; i >= 0; i--)                                                
{                                                                                                                     
    if (content.getEmbeddedObjects().get_Item(i).getDocumentInfo().getFileType() == FileType.JPEG)                    
    {                                                                                                                 
        // Remove reference to the image from html body                                                               
        String pattern = "<img[^>]*src=\"cid:" + content.getEmbeddedObjects().get_Item(i).getContentId() + "\"[^>]*>";
        content.setHtmlBody(content.getHtmlBody().replaceAll(pattern, ""));                                           
                                                                                                                      
        // Remove the image                                                                                           
        content.getEmbeddedObjects().removeAt(i);                                                                     
    }                                                                                                                 
}                                                                                                                     
                                                                                                                      
watermarker.save("message.msg");                                                                            
                                                                                                                      
watermarker.close();                                                                                                  
```

## Searching text in email message body or subject

Using GroupDocs.Watermark, you can also search for a text in the subject as well as in the body of the email message. Following is the code sample for searching text in Email Message:

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailSearchTextInBody**

```java
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                                                                               
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg"                                                              
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                                                                                      
                                                                                                                                                                     
SearchCriteria criteria = new TextSearchCriteria("test", false);                                                                                                     
                                                                                                                                                                     
// Specify search locations                                                                                                                                          
watermarker.getSearchableObjects().setEmailSearchableObjects(EmailSearchableObjects.Subject | EmailSearchableObjects.HtmlBody | EmailSearchableObjects.PlainTextBody);
                                                                                                                                                                     
// Note, search is performed only if you pass TextSearchCriteria instance to FindWatermarks method                                                                   
PossibleWatermarkCollection watermarks = watermarker.search(criteria);                                                                                               
                                                                                                                                                                     
// Remove found text fragments                                                                                                                                       
watermarks.clear();                                                                                                                                                  
                                                                                                                                                                     
// Save changes                                                                                                                                                      
watermarker.save("message.msg");                                                                                                                           
                                                                                                                                                                     
watermarker.close();                                                                                                                                                 
```

## Listing all message recipients

GroupDocs.Watermark also allows listing all the message recipients using methods [getTo()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/EmailContent#getTo()), [getCc()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/EmailContent#getCc()) and [getBcc()](https://reference.groupdocs.com/watermark/java/com.groupdocs.watermark.contents/EmailContent#getBcc()) as shown in the following code sample.

**advanced\_usage.add\_watermarks\_to\_email\_attachments.EmailListRecipients**

```java
EmailLoadOptions loadOptions = new EmailLoadOptions();                                                  
// Specify an absolute or relative path to your document. Ex: "C:\\Docs\\message.msg" 
Watermarker watermarker = new Watermarker("message.msg", loadOptions);                         
                                                                                                        
EmailContent content = watermarker.getContent(EmailContent.class);                                      
                                                                                                        
// List all direct recipients                                                                           
for (EmailAddress address : content.getTo())                                                            
{                                                                                                       
    System.out.println(address.getAddress());                                                           
}                                                                                                       
                                                                                                        
// List all CC recipients                                                                               
for (EmailAddress address : content.getCc())                                                            
{                                                                                                       
    System.out.println(address.getAddress());                                                           
}                                                                                                       
                                                                                                        
// List all BCC recipients                                                                              
for (EmailAddress address : content.getBcc())                                                           
{                                                                                                       
    System.out.println(address.getAddress());                                                           
}                                                                                                       
                                                                                                        
watermarker.close();                                                                                    
```
