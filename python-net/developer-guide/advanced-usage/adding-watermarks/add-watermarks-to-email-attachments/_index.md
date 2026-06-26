---
id: add-watermarks-to-email-attachments
url: watermark/python-net/add-watermarks-to-email-attachments
title: Add watermarks to email messages and attachments
linkTitle: Email messages and attachments
weight: 20
description: "Modify email message bodies and subjects, embed and remove images, and watermark email attachments using GroupDocs.Watermark for Python via .NET."
keywords: email watermark, msg, eml, attachments, embedded images, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: False
toc: true
---

GroupDocs.Watermark works with email messages (MSG, EML, EMLX) through their content tree. Open the message and call `Watermarker.get_content()` to obtain an `EmailContent`, which exposes the message body and subject, embedded objects, recipients, and attachments. From there you can modify the body and subject, embed or remove images, search the message text, and watermark the attached documents.

This section covers:

- [Email messages]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-messages.md" >}}) — modify the body and subject, embed and remove images, search the message text, and list recipients.
- [Email attachments]({{< ref "watermark/python-net/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/email-attachments.md" >}}) — extract, add, remove, and watermark the documents attached to a message.
