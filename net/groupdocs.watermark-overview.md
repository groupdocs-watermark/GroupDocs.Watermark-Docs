---
id: groupdocs-watermark-overview
url: watermark/net/groupdocs-watermark-overview
title: GroupDocs.Watermark Overview
linkTitle: Product overview
weight: 1
description: "Protect and customize documents with watermarks using GroupDocs.Watermark for .NET. Add, remove, search, and manage visible or invisible watermarks in over 50 document formats including PDF, Word, Excel, PowerPoint, and images."
keywords: 
  - Protect documents with watermarks
  - Add watermark
  - Remove watermark
  - Custom watermark
  - Invisible watermarking
  - Document watermark examples
  - Watermark PDF
  - Watermark Word
  - Watermark Excel
  - Watermark automation
  - Confidential watermark
  - Watermark on document
  - Delete watermark from
  - Add image watermark
  - Add text watermark
  - GroupDocs watermark
  - How to add watermark
  - How to remove watermark
productName: GroupDocs.Watermark for .NET
hideChildren: true,
toc: true
---

## Protect Your Documents with Smart Watermarking

**GroupDocs.Watermark for .NET** is a powerful and flexible API that helps developers **add, search, edit, or remove watermarks** from documents and images across more than 50 file formats.

Whether you need to **add a confidential watermark**, apply **invisible tracking for sensitive content**, or **automate watermarking at scale**, GroupDocs.Watermark offers the features and precision control you need — without relying on external software like Microsoft Office or Adobe Acrobat.

### Supported Formats

- Documents: **PDF, DOCX/DOC, RTF**
- Presentations: **PPTX/PPT**
- Spreadsheets: **XLSX/XLS**
- Images: **JPG, PNG, TIFF, GIF**, and [more] ({{< ref "watermark/net/getting-started/supported-document-formats.md" >}})

---

## Key Features

### Add or Remove Watermarks

- Add **text watermarks** or **image watermarks** to documents or images
- Remove watermarks even if they were added by third-party tools
- Detect and remove watermarks based on text, font, or formatting
- Protect watermarks from editing by locking them in the content structure

### Advanced Customization

- Set **custom font**, color, opacity, and positioning
- Apply watermarks to specific **pages**, **slides**, **sections**, or **frames**
- Align watermark to **bleed box**, **crop box**, **art box**, or **trim box** in PDFs
- Replace existing watermark text with updated formatting

### Invisible & Intelligent Watermarks

- Add **invisible watermarks** that only appear during printing
- Add **tracking watermarks** for audit or copyright protection
- Use OCR-like detection to find obfuscated or hidden text watermarks
- Match image-based watermarks using visual similarity

### Comprehensive Coverage

- Add watermarks to:
  - All **headers and footers**
  - All **attachments** in PDFs or emails
  - All **image shapes** in presentations or Word documents
- Rasterize content to protect watermarks from extraction
- Automatically find and process watermarks in multi-layered or structured content

---

## Real-World Use Cases

> 💡 You can use GroupDocs.Watermark for:

- Adding a **Confidential** watermark before sending internal files
- Protecting content with **invisible watermarks** for IP tracking
- Automating watermarking of **PDF invoices** or **Excel reports**
- **Removing unwanted watermarks** from third-party documents
- Inserting company logos or custom stamps on **Word or PowerPoint slides**

---

## Frequently Asked Questions

### ❓ How can I remove a watermark from a document?

Use the `Watermarker.Remove()` method to delete both visible and invisible watermarks. You can target specific types using watermark search filters.

### ❓ Can I insert a custom watermark on each slide of a presentation?

Yes, you can add text or image watermarks to all slides or selected ones in PPT/PPTX files.

### ❓ How do I add a diagonal watermark?

To add a diagonal watermark, set the desired rotation angle (e.g., 45 degrees) using the `RotationAngle` property. To repeat the watermark across the page, enable tiling with the `TileOptions`. You can also customize the watermark’s position, font, opacity, and size to achieve a polished, professional appearance.

---

## Learn More

- [How to add a watermark to a document] ({{< ref "watermark/net/developer-guide/basic-usage/add-text.md" >}})
- [How to remove watermark from PDF] ({{< ref "watermark/net/developer-guide/advanced-usage/searching-and-modifying-watermarks/removing-found-watermarks.md" >}})
- [Supported File Formats] ({{< ref "watermark/net/basic-usage/supported-document-formats.md" >}})
- [Code Examples Gallery] ({{< ref "watermark/net/basic-usage/how-to-run-examples.md" >}})

---

Start protecting your content today with **GroupDocs.Watermark for .NET** — the complete solution for secure, flexible, and automated document watermarking.

