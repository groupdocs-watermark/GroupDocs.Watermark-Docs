---
id: supported-document-formats
url: watermark/java/supported-document-formats
title: Supported Document Formats
weight: 2
description: It supports DOCX, DOCM, DOC, DOT, DOTM, XLS, XLSX, PDF, PPT, JPG, PNG, HTML, EML and many more.
keywords: DOCX, DOCM, DOC, DOT, DOTM, XLS, XLSX, PDF, PPT, JPG, PNG, HTML, EML 
productName: GroupDocs.Watermark for Java
hideChildren: False
toc: true
---

GroupDocs.Watermark for Java supports a wide range of file formats for adding, searching, and removing watermarks. Use the search box below to quickly find your format, or browse by category.

<style>
/* Theme-aware format search — colors come from the geekdoc theme variables,
   so the widget follows light/dark mode (manual toggle and prefers-color-scheme). */
.gd-format-search { margin: 24px 0; }
.gd-format-search__box { position: relative; display: flex; align-items: center; }
.gd-format-search__icon {
  position: absolute; left: 14px; width: 18px; height: 18px;
  color: var(--body-text-font-color); opacity: .75; pointer-events: none;
}
.gd-format-search__input {
  width: 100%; box-sizing: border-box;
  padding: 12px 44px 12px 42px;
  font-size: 16px; line-height: 1.4;
  color: var(--body-font-color);
  background: var(--code-background);
  border: 1px solid var(--border-color);
  border-radius: 10px; outline: none;
  -webkit-appearance: none; appearance: none;
  transition: border-color .15s ease, box-shadow .15s ease, background .15s ease;
}
.gd-format-search__input::placeholder { color: var(--body-text-font-color); opacity: .85; }
.gd-format-search__input:hover { border-color: var(--alt-border-color); }
.gd-format-search__input:focus {
  border-color: var(--link-color);
  box-shadow: 0 0 0 3px var(--link-border-color);
  background: var(--body-background);
}
.gd-format-search__clear {
  position: absolute; right: 10px;
  display: flex; align-items: center; justify-content: center;
  width: 26px; height: 26px; padding: 0;
  font-size: 20px; line-height: 1;
  color: var(--body-text-font-color);
  background: transparent; border: 0; border-radius: 50%; cursor: pointer;
  transition: background .15s ease, color .15s ease;
}
.gd-format-search__clear:hover { background: var(--accent-color); color: var(--body-font-color); }
.gd-format-search__results {
  margin-top: 10px;
  background: var(--body-background);
  border: 1px solid var(--border-color);
  border-radius: 10px; overflow: hidden;
}
.gd-format-search__results-head {
  padding: 9px 14px;
  font-size: 13px; font-weight: 600;
  color: var(--body-text-font-color);
  background: var(--accent-color);
  border-bottom: 1px solid var(--border-color);
}
.gd-format-search__list { max-height: 320px; overflow-y: auto; }
.gd-format-search__item {
  padding: 10px 14px;
  border-left: 3px solid var(--link-color);
  border-bottom: 1px solid var(--border-color);
}
.gd-format-search__item:last-child { border-bottom: 0; }
.gd-format-search__item-title { color: var(--body-font-color); }
.gd-format-search__item-ext { font-weight: 700; }
.gd-format-search__item-meta {
  display: block; margin-top: 3px;
  font-size: 12.5px; color: var(--body-text-font-color);
}
.gd-format-search__badge {
  display: inline-block; margin-left: 4px;
  padding: 1px 8px; border-radius: 999px;
  font-size: 11px; font-weight: 600; color: #fff; vertical-align: middle;
}
.gd-format-search__badge.is-full { background: var(--tip-color); }
.gd-format-search__badge.is-partial { background: var(--warning-color); }
.gd-format-search__badge.is-add { background: var(--info-color); }
.gd-format-search__badge.is-none { background: var(--danger-color); }
.gd-format-search__hl { background: var(--mark-color); color: #1b1b1e; border-radius: 2px; padding: 0 1px; }
.gd-format-search__empty { padding: 14px; color: var(--body-text-font-color); }
</style>

<div class="gd-format-search">
  <div class="gd-format-search__box">
    <svg class="gd-format-search__icon" viewBox="0 0 24 24" fill="none" stroke="currentColor" stroke-width="2" stroke-linecap="round" stroke-linejoin="round" aria-hidden="true">
      <circle cx="11" cy="11" r="7"></circle>
      <line x1="21" y1="21" x2="16.65" y2="16.65"></line>
    </svg>
    <input type="text" id="formatSearch" class="gd-format-search__input" autocomplete="off"
           placeholder="Search for a file format (e.g., docx, pdf, png)…"
           aria-label="Search supported file formats">
    <button type="button" id="formatSearchClear" class="gd-format-search__clear" aria-label="Clear search" hidden>&times;</button>
  </div>
  <div id="searchResults" class="gd-format-search__results" hidden>
    <div class="gd-format-search__results-head" id="resultsCount"></div>
    <div id="resultsList" class="gd-format-search__list"></div>
  </div>
</div>

## 🚀 Quick Format Lookup

**Popular Formats:** [.docx](#-microsoft-word-formats) | [.pdf](#-pdf-formats) | [.xlsx](#-microsoft-excel-formats) | [.pptx](#-microsoft-powerpoint-formats) | [.png](#-image-formats) | [.jpg](#-image-formats)

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

📘 See examples for [Word]({{< ref "/watermark/java/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-word-processing-documents/_index.md" >}}) formats

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

📘 Excel watermarking [examples]({{< ref "/watermark/java/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-spreadsheet-documents/_index.md" >}})

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

📘 PowerPoint watermarking [examples]({{< ref "/watermark/java/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-presentation-documents/_index.md" >}})

---

## 🧾 PDF Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.pdf` | PDF (Adobe Portable Document) format | ✅ | ✅ | ✅ | ✅ | ✅ | Watermark searching and removing is not available for rasterized pages |

📘 Add watermark to [PDF]({{< ref "/watermark/java/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-pdf-documents/_index.md" >}})

---

## ✉️ Email Formats

| Format | Description | Load | Save | Add | Search | Remove | Remarks |
|--------|-------------|------|------|-----|--------|--------|---------|
| `.eml` | Email Message Format | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | Watermark management is available for attached documents and images |
| `.emlx` | Apple Mail Message | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | Watermark management is available for attached documents and images |
| `.oft` | Microsoft Outlook Email Template | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | Watermark management is available for attached documents and images |
| `.msg` | Outlook Email Message Format | ✅ | ✅ | ⚠️ | ⚠️ | ⚠️ | Watermark management is available for attached documents and images |

📘 Add watermark to MSG [files]({{< ref "/watermark/java/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-email-attachments/_index.md" >}})

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

📘 Image watermarking [examples]({{< ref "/watermark/java/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-images/_index.md" >}})

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

📘 Visio watermarking [examples]({{< ref "/watermark/java/developer-guide/advanced-usage/adding-watermarks/add-watermarks-to-diagram-documents/_index.md" >}})

---

## ℹ️ Notes

- Watermarking capabilities may vary depending on the document content and structure.
- For email formats, watermark operations are limited to attached documents and images within the email.
- For image formats, search and remove operations are not supported - only adding watermarks is available.
- PDF watermark searching and removing is not available for rasterized pages.
- For the latest updates, refer to the [Changelog](https://docs.groupdocs.com/watermark/java/release-notes/).
- If a format you need is not listed, feel free to [contact support](https://forum.groupdocs.com/).

---

{{< alert style="tip" >}}

**Can't find your file format?**

We're here to help! Please post a request on our [Free Support Forum](https://forum.groupdocs.com/c/watermark/19), and our team will assist you.

{{< /alert >}}


<script>
document.addEventListener('DOMContentLoaded', function() {
    const searchInput = document.getElementById('formatSearch');
    const searchResults = document.getElementById('searchResults');
    const resultsList = document.getElementById('resultsList');
    
    // Format database for search (Java version)
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
    
    const clearButton = document.getElementById('formatSearchClear');
    const resultsCount = document.getElementById('resultsCount');

    const SUPPORT_META = {
        'Full':     { label: 'Full',          cls: 'is-full' },
        'Full*':    { label: 'Full*',         cls: 'is-full' },
        'Partial':  { label: 'Partial',       cls: 'is-partial' },
        'Add Only': { label: 'Add only',      cls: 'is-add' }
    };

    function escapeHtml(text) {
        return text.replace(/[&<>"']/g, ch => ({
            '&': '&amp;', '<': '&lt;', '>': '&gt;', '"': '&quot;', "'": '&#39;'
        }[ch]));
    }

    function escapeRegExp(text) {
        return text.replace(/[.*+?^${}()|[\]\\]/g, '\\$&');
    }

    function highlight(text, query) {
        const safe = escapeHtml(text);
        if (!query) return safe;
        const re = new RegExp('(' + escapeRegExp(escapeHtml(query)) + ')', 'ig');
        return safe.replace(re, '<span class="gd-format-search__hl">$1</span>');
    }

    function badge(support) {
        const meta = SUPPORT_META[support] || { label: support || 'None', cls: 'is-none' };
        return '<span class="gd-format-search__badge ' + meta.cls + '">' + escapeHtml(meta.label) + '</span>';
    }

    function showResults(open) {
        searchResults.hidden = !open;
    }

    function performSearch(rawQuery) {
        const query = (rawQuery || '').trim();
        clearButton.hidden = query.length === 0;

        if (query.length < 2) {
            showResults(false);
            return;
        }

        const needle = query.toLowerCase();
        const matches = formats.filter(format =>
            format.ext.toLowerCase().includes(needle) ||
            format.name.toLowerCase().includes(needle) ||
            format.category.toLowerCase().includes(needle)
        );

        if (matches.length > 0) {
            resultsCount.textContent = matches.length + (matches.length === 1 ? ' format' : ' formats') + ' found';
            resultsList.innerHTML = matches.map(match => `
                <div class="gd-format-search__item">
                    <span class="gd-format-search__item-title">
                        <span class="gd-format-search__item-ext">${highlight(match.ext, query)}</span>
                        &mdash; ${highlight(match.name, query)}
                    </span>
                    <small class="gd-format-search__item-meta">
                        ${highlight(match.category, query)} &middot; ${badge(match.support)}
                    </small>
                </div>
            `).join('');
        } else {
            resultsCount.textContent = 'No matches';
            resultsList.innerHTML = '<div class="gd-format-search__empty">No formats found matching &ldquo;' + escapeHtml(query) + '&rdquo;.</div>';
        }
        showResults(true);
    }

    function clearSearch() {
        searchInput.value = '';
        performSearch('');
        searchInput.focus();
    }

    searchInput.addEventListener('input', function(e) {
        performSearch(e.target.value);
    });

    searchInput.addEventListener('keydown', function(e) {
        if (e.key === 'Escape') {
            clearSearch();
        }
    });

    clearButton.addEventListener('click', clearSearch);

    // Re-open results when focusing a non-empty field
    searchInput.addEventListener('focus', function(e) {
        if (e.target.value.trim().length >= 2) {
            performSearch(e.target.value);
        }
    });

    // Hide results when clicking outside the widget
    document.addEventListener('click', function(e) {
        if (!e.target.closest('.gd-format-search')) {
            showResults(false);
        }
    });
});
</script>