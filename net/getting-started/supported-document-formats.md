---
id: supported-document-formats
url: watermark/net/supported-document-formats
title: Supported Document Formats
weight: 2
description: It supports DOCX, DOCM, DOC, DOT, DOTM, XLS, XLSX, PDF, PPT, JPG, PNG, HTML, EML and many more.
keywords: DOCX, DOCM, DOC, DOT, DOTM, XLS, XLSX, PDF, PPT, JPG, PNG, HTML, EML 
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---

GroupDocs.Watermark for .NET supports a wide range of file formats for adding, searching, and removing watermarks. Use the search box below to quickly find your format, or browse by category.

<div style="margin: 20px 0; padding: 15px; background: #f8f9fa; border-radius: 8px; border-left: 4px solid #007bff;">
  <div style="margin-bottom: 15px;">
    <input type="text" id="formatSearch" placeholder="🔍 Search for a file format (e.g., docx, pdf, png)..." 
           style="width: 100%; padding: 10px; border: 2px solid #ddd; border-radius: 6px; font-size: 16px;">
  </div>
  <div id="searchResults" style="display: none; margin-top: 15px; padding: 10px; background: white; border-radius: 6px; border: 1px solid #ddd;">
    <strong>Search Results:</strong>
    <div id="resultsList"></div>
  </div>
</div>

## 🚀 Quick Format Lookup

**Popular Formats:** [.docx](#-microsoft-word-formats) | [.pdf](#-pdf-formats) | [.xlsx](#-microsoft-excel-formats) | [.pptx](#-microsoft-powerpoint-formats) | [.png](#️-image-formats) | [.jpg](#️-image-formats)

Each format may support different watermarking capabilities:
- ✅ Full support (Add / Search / Remove)
- ⚠️ Partial support (some limitations)
- ❌ Not supported

---

## 📄 Microsoft Word Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.doc` | Microsoft Word 97 - 2007 Document | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.dot` | Microsoft Word 97 - 2007 Template | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.docx` | Office Open XML WordprocessingML Document (macro-free) | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.docm` | Office Open XML WordprocessingML Macro-Enabled Document | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.dotx` | Office Open XML WordprocessingML Template (macro-free) | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.dotm` | Word Open XML Macro-Enabled Document | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.rtf` | Rich Text Format File | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.odt` | ODF Text Document | ✅ | ✅ | ✅ | ✅ | ✅ | |

📘 [See examples for Word formats](https://docs.groupdocs.com/watermark/net/add-watermark-to-word-document/)

---

## 📊 Microsoft Excel Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.xlsx` | OOXML 2007-2010 | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.xlsm` | OOXML Macro Enabled Workbook | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.xltm` | OOXML Macro Enabled Workbook Template | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.xlt` | Microsoft Excel Template File | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.xltx` | Excel Open XML Spreadsheet Template | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.xls` | Excel Workbook 97-2003 | ✅ | ✅ | ✅ | ✅ | ✅ | |

📘 [Excel watermarking examples](https://docs.groupdocs.com/watermark/net/add-watermark-to-excel/)

---

## 📈 Microsoft PowerPoint Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.pptx` | OOXML Presentation | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.pptm` | OOXML Macro Enabled Presentation | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.ppsx` | OOXML SlideShow | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.ppsm` | OOXML Macros Enabled Presentation | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.potx` | OOXML Presentation Template | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.potm` | OOXML Macro Enabled Presentation Template | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.ppt` | PowerPoint Presentation 97-2003 | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.pps` | PowerPoint SlideShow 97-2003 | ✅ | ✅ | ✅ | ✅ | ✅ | |

📘 [PowerPoint watermarking examples](https://docs.groupdocs.com/watermark/net/add-watermark-to-powerpoint/)

---

## 🧾 PDF Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.pdf` | PDF (Adobe Portable Document) format | ✅ | ✅ | ✅ | ✅ | ✅ | Watermark searching and removing is not available for rasterized pages |

📘 [Add watermark to PDF](https://docs.groupdocs.com/watermark/net/add-watermark-to-pdf/)

---

## ✉️ Email Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.eml` | Email Message Format | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | Watermark management is available for attached documents and images |
| `.emlx` | Apple Mail Message | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | Watermark management is available for attached documents and images |
| `.oft` | Microsoft Outlook Email Template | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | Watermark management is available for attached documents and images |
| `.msg` | Outlook Email Message Format | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | Watermark management is available for attached documents and images |

📘 [Add watermark to MSG files](https://docs.groupdocs.com/watermark/net/add-watermark-to-email-message/)

---

## 🖼️ Image Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.bmp` | Bitmap Picture (BMP) | ✅ | ✅ | ✅ | ❌ | ❌ | |
| `.gif` | Graphics Interchange Format (GIF) | ✅ | ✅ | ✅ | ❌ | ❌ | |
| `.jpg` / `.jpeg` / `.jpe` | Joint Photographic Experts Group (JPEG) | ✅ | ✅ | ✅ | ❌ | ❌ | |
| `.jp2` | JPEG2000 Core Image File | ✅ | ✅ | ✅ | ❌ | ❌ | |
| `.png` | Portable Network Graphics (PNG) | ✅ | ✅ | ✅ | ❌ | ❌ | |
| `.tiff` | Tagged Image File Format (TIFF) | ✅ | ✅ | ✅ | ❌ | ❌ | |
| `.webp` | WebP Image | ✅ | ✅ | ✅ | ❌ | ❌ | |

📘 [Image watermarking examples](https://docs.groupdocs.com/watermark/net/add-watermark-to-image/)

---

## 🎨 Microsoft Visio Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.vsd` | Microsoft Visio 2003-2010 Drawing | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vdx` | Microsoft Visio 2003-2010 XML Drawing | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vsdx` | Microsoft Visio Drawing | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vstx` | Microsoft Visio File Format | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vss` | Microsoft Visio 2003-2010 Stencil | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vssx` | Visio Stencil File Format | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vsdm` | Visio Macro-Enabled Drawing | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vssm` | Microsoft Visio Macro Enabled File Format | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vstm` | Visio Macro-Enabled Drawing Template | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vtx` | VTX Chiptune File | ✅ | ✅ | ✅ | ✅ | ✅ | |
| `.vsx` | Microsoft Visio 2003-2010 XML Stencil | ✅ | ✅ | ✅ | ✅ | ✅ | |

📘 [Visio watermarking examples](https://docs.groupdocs.com/watermark/net/add-watermark-to-visio/)

---

## ℹ️ Notes

- Watermarking capabilities may vary depending on the document content and structure.
- For email formats, watermark operations are limited to attached documents and images within the email.
- For image formats, search and remove operations are not supported - only adding watermarks is available.
- PDF watermark searching and removing is not available for rasterized pages.
- For the latest updates, refer to the [Changelog](https://docs.groupdocs.com/watermark/net/release-notes/).
- If a format you need is not listed, feel free to [contact support](https://forum.groupdocs.com/).

---

## How to Get Supported File Types Programmatically

GroupDocs.Watermark also allows you to retrieve the list of all supported file formats programmatically using the `GetSupportedFileTypes()` method of the `FileType` class.

### Example

```csharp
IEnumerable<FileType> supportedFileTypes = FileType.GetSupportedFileTypes();
foreach (FileType fileType in supportedFileTypes)
{
    Console.WriteLine(fileType);
}
```

{{< alert style="tip" >}}

**Can’t find your file format?**

We’re here to help! Please post a request on our [Free Support Forum](https://forum.groupdocs.com/c/watermark/19), and our team will assist you.

{{< /alert >}}


<script>
document.addEventListener('DOMContentLoaded', function() {
    const searchInput = document.getElementById('formatSearch');
    const searchResults = document.getElementById('searchResults');
    const resultsList = document.getElementById('resultsList');
    
    // Format database for search
    const formats = [
        { ext: '.doc', name: 'Microsoft Word 97-2007 Document', category: 'Word', support: 'Full' },
        { ext: '.docx', name: 'Office Open XML WordprocessingML Document', category: 'Word', support: 'Full' },
        { ext: '.docm', name: 'Office Open XML WordprocessingML Macro-Enabled Document', category: 'Word', support: 'Full' },
        { ext: '.dot', name: 'Microsoft Word 97-2007 Template', category: 'Word', support: 'Full' },
        { ext: '.dotx', name: 'Office Open XML WordprocessingML Template', category: 'Word', support: 'Full' },
        { ext: '.dotm', name: 'Word Open XML Macro-Enabled Document', category: 'Word', support: 'Full' },
        { ext: '.rtf', name: 'Rich Text Format File', category: 'Word', support: 'Full' },
        { ext: '.odt', name: 'ODF Text Document', category: 'Word', support: 'Full' },
        
        { ext: '.xlsx', name: 'OOXML 2007-2010', category: 'Excel', support: 'Full' },
        { ext: '.xlsm', name: 'OOXML Macro Enabled Workbook', category: 'Excel', support: 'Full' },
        { ext: '.xltm', name: 'OOXML Macro Enabled Workbook Template', category: 'Excel', support: 'Full' },
        { ext: '.xlt', name: 'Microsoft Excel Template File', category: 'Excel', support: 'Full' },
        { ext: '.xltx', name: 'Excel Open XML Spreadsheet Template', category: 'Excel', support: 'Full' },
        { ext: '.xls', name: 'Excel Workbook 97-2003', category: 'Excel', support: 'Full' },
        
        { ext: '.pptx', name: 'OOXML Presentation', category: 'PowerPoint', support: 'Full' },
        { ext: '.pptm', name: 'OOXML Macro Enabled Presentation', category: 'PowerPoint', support: 'Full' },
        { ext: '.ppsx', name: 'OOXML SlideShow', category: 'PowerPoint', support: 'Full' },
        { ext: '.ppsm', name: 'OOXML Macros Enabled Presentation', category: 'PowerPoint', support: 'Full' },
        { ext: '.potx', name: 'OOXML Presentation Template', category: 'PowerPoint', support: 'Full' },
        { ext: '.potm', name: 'OOXML Macro Enabled Presentation Template', category: 'PowerPoint', support: 'Full' },
        { ext: '.ppt', name: 'PowerPoint Presentation 97-2003', category: 'PowerPoint', support: 'Full' },
        { ext: '.pps', name: 'PowerPoint SlideShow 97-2003', category: 'PowerPoint', support: 'Full' },
        
        { ext: '.pdf', name: 'PDF (Adobe Portable Document) format', category: 'PDF', support: 'Full*' },
        
        { ext: '.eml', name: 'Email Message Format', category: 'Email', support: 'Partial' },
        { ext: '.emlx', name: 'Apple Mail Message', category: 'Email', support: 'Partial' },
        { ext: '.oft', name: 'Microsoft Outlook Email Template', category: 'Email', support: 'Partial' },
        { ext: '.msg', name: 'Outlook Email Message Format', category: 'Email', support: 'Partial' },
        
        { ext: '.bmp', name: 'Bitmap Picture', category: 'Image', support: 'Add Only' },
        { ext: '.gif', name: 'Graphics Interchange Format', category: 'Image', support: 'Add Only' },
        { ext: '.jpg', name: 'Joint Photographic Experts Group', category: 'Image', support: 'Add Only' },
        { ext: '.jpeg', name: 'Joint Photographic Experts Group', category: 'Image', support: 'Add Only' },
        { ext: '.jpe', name: 'Joint Photographic Experts Group', category: 'Image', support: 'Add Only' },
        { ext: '.jp2', name: 'JPEG2000 Core Image File', category: 'Image', support: 'Add Only' },
        { ext: '.png', name: 'Portable Network Graphics', category: 'Image', support: 'Add Only' },
        { ext: '.tiff', name: 'Tagged Image File Format', category: 'Image', support: 'Add Only' },
        { ext: '.webp', name: 'WebP Image', category: 'Image', support: 'Add Only' },
        
        { ext: '.vsd', name: 'Microsoft Visio 2003-2010 Drawing', category: 'Visio', support: 'Full' },
        { ext: '.vdx', name: 'Microsoft Visio 2003-2010 XML Drawing', category: 'Visio', support: 'Full' },
        { ext: '.vsdx', name: 'Microsoft Visio Drawing', category: 'Visio', support: 'Full' },
        { ext: '.vstx', name: 'Microsoft Visio File Format', category: 'Visio', support: 'Full' },
        { ext: '.vss', name: 'Microsoft Visio 2003-2010 Stencil', category: 'Visio', support: 'Full' },
        { ext: '.vssx', name: 'Visio Stencil File Format', category: 'Visio', support: 'Full' },
        { ext: '.vsdm', name: 'Visio Macro-Enabled Drawing', category: 'Visio', support: 'Full' },
        { ext: '.vssm', name: 'Microsoft Visio Macro Enabled File Format', category: 'Visio', support: 'Full' },
        { ext: '.vstm', name: 'Visio Macro-Enabled Drawing Template', category: 'Visio', support: 'Full' },
        { ext: '.vtx', name: 'VTX Chiptune File', category: 'Visio', support: 'Full' },
        { ext: '.vsx', name: 'Microsoft Visio 2003-2010 XML Stencil', category: 'Visio', support: 'Full' }
    ];
    
    function getSupportIcon(support) {
        switch(support) {
            case 'Full': return '✅';
            case 'Full*': return '✅*';
            case 'Partial': return '⚠️';
            case 'Add Only': return '🔸';
            default: return '❌';
        }
    }
    
    function performSearch(query) {
        if (!query || query.length < 2) {
            searchResults.style.display = 'none';
            return;
        }
        
        query = query.toLowerCase();
        const matches = formats.filter(format => 
            format.ext.toLowerCase().includes(query) || 
            format.name.toLowerCase().includes(query) ||
            format.category.toLowerCase().includes(query)
        );
        
        if (matches.length > 0) {
            resultsList.innerHTML = matches.map(match => `
                <div style="padding: 8px; margin: 5px 0; background: #f0f8ff; border-left: 3px solid #007bff; border-radius: 4px;">
                    <strong>${match.ext}</strong> - ${match.name}
                    <br><small>Category: ${match.category} | Support: ${getSupportIcon(match.support)} ${match.support}</small>
                </div>
            `).join('');
            searchResults.style.display = 'block';
        } else {
            resultsList.innerHTML = '<div style="padding: 8px; color: #666;">No formats found matching your search.</div>';
            searchResults.style.display = 'block';
        }
    }
    
    searchInput.addEventListener('input', function(e) {
        performSearch(e.target.value);
    });
    
    searchInput.addEventListener('keydown', function(e) {
        if (e.key === 'Escape') {
            searchResults.style.display = 'none';
            searchInput.value = '';
        }
    });
    
    // Hide search results when clicking outside
    document.addEventListener('click', function(e) {
        if (!e.target.closest('#formatSearch') && !e.target.closest('#searchResults')) {
            searchResults.style.display = 'none';
        }
    });
});
</script>