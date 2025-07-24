---
id: add-watermarks-to-email-attachments
url: watermark/net/add-watermarks-to-email-attachments
title: Add watermarks to email attachments
linkTitle: To email attachments
weight: 4
description: "The API allows you to add watermark to email attachments (all the attachments of supported types in an email message)"
keywords: add watermark, add watermark to email attachments 
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---
The API allows you to add watermark to all the [attachments](https://reference.groupdocs.com/net/watermark/groupdocs.watermark.contents.email/emailcontent/properties/attachments) of supported types in an email message as shown in the following code sample.

**AdvancedUsage.AddingWatermarks.AddWatermarksToEmailAttachments.EmailAddWatermarkToAllAttachments**

```csharp
TextWatermark watermark = new TextWatermark("Test watermark", new Font("Arial", 19));
EmailLoadOptions loadOptions = new EmailLoadOptions();
// Specify an absolute or relative path to your document. Ex: @"C:\Docs\message.msg"
using (Watermarker watermarker = new Watermarker("message.msg", loadOptions))
{
    EmailContent content = watermarker.GetContent<EmailContent>();
    foreach (EmailAttachment attachment in content.Attachments)
    {
        // Check if the attached file is supported by GroupDocs.Watermark
        IDocumentInfo info = attachment.GetDocumentInfo();
        if (info.FileType != FileType.Unknown && !info.IsEncrypted)
        {
            // Load the attached document
            using (Watermarker attachedWatermarker = attachment.CreateWatermarker())
            {
                // Add wateramrk
                attachedWatermarker.Add(watermark);

                // Save changes in the attached file
                attachedWatermarker.Save();
            }
        }
    }

    // Save changes
    watermarker.Save("message.msg");
}
```

## Advanced use cases

* [Email attachments]({{< ref "email-attachments" >}} "Email attachments")
* [Email messages]({{< ref "email-messages" >}} "Email messages")
