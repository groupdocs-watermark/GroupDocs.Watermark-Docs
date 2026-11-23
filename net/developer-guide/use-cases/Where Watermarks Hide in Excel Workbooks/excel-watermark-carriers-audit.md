---
id: excel-watermark-carriers-audit
url: watermark/net/excel-watermark-carriers-audit
title: Where Watermarks Hide in Excel Workbooks - 4 Carriers Compared
weight: 10
description: "Find, stamp and clear marks in XLSX with GroupDocs.Watermark for .NET. Compare the four carriers - header pictures, worksheet backgrounds, shape images and OLE attachments - and learn which ones a reader never sees."
keywords: excel watermark, xlsx watermark, worksheet background, header footer image, spreadsheet shapes, ole attachment, remove watermark excel, document audit, .NET watermark
productName: GroupDocs.Watermark for .NET
structuredData:
    showOrganization: True
toc: true
draft: false
---

{{< alert style="info" >}} The complete source code for this use case is available on GitHub: [groupdocs-watermark/audit-hidden-watermarks-in-excel-workbooks-dotnet](https://github.com/groupdocs-watermark/audit-hidden-watermarks-in-excel-workbooks-dotnet).{{< /alert >}}

## Introduction

"Does this workbook have a watermark?" has no single answer in Excel, because
Excel has no watermark feature. What it has instead are four separate places
where a mark can live: header and footer sections, the worksheet background,
shapes drawn on the sheet, and files embedded as OLE attachments. A workbook
can use all four at once, and three of them are invisible in the normal
editing view.

That invisibility cuts both ways. Workbooks go out believing they are marked
when the only mark sits in a header nobody reads on screen. Workbooks arrive
from clients and get reused internally, carrying the client's logo and
confidentiality notice into reports that were never meant to have them.

This guide compares the four carriers in GroupDocs.Watermark for .NET - how to
find each one, how to mark it, how to clear it, and how visible each is to
the person who opens the file.

## What This Guide Covers

- The four carriers a mark can occupy in an `.xlsx` workbook
- An inventory pass that reports what a workbook holds before you change it
- Marking images in place with `SpreadsheetWatermarkableImage.Add`
- Clearing headers, footers and backgrounds for external distribution
- Why a watermark on the workbook never reaches inside an attachment

## Choosing Where to Look

Start from what you need. To learn what a workbook already carries, run the
inventory pass - it reads all four carriers in one load. For a mark that
prints on every page, the header or footer is the only reliable choice, since
Excel does not print worksheet backgrounds. For a mark the reader cannot click
away, the background is sturdier than any shape. When the picture itself is
the asset and may be copied into another document, mark the shape image. And
whatever else you do, check the attachments: that count tells you whether a
whole file is travelling inside the workbook.

## Method Comparison Overview

Each carrier is reached through its own member of `SpreadsheetWorksheet`:
`HeadersFooters` for header and footer sections, `BackgroundImage` for the
tiled picture behind the cells, `Shapes` for drawn objects, and `Attachments`
for embedded files. They differ sharply in how visible they are. A header is
seen only in print preview and removed through Page Setup; a background shows
behind the cells and is removed through Page Layout; a shape is immediately
visible and deletes in a single click, as does an attachment icon.

## Detailed Method Analysis

### Carrier 1: Headers and footers

#### Overview

Every worksheet has six header/footer objects - primary, even and first, each
as header and footer - and each has left, centre and right sections. That is
eighteen slots per sheet, every one able to hold text in `Script` and a
picture in `Image`.

```csharp
foreach (SpreadsheetHeaderFooter headerFooter in worksheet.HeadersFooters)
{
    foreach (SpreadsheetHeaderFooterSection section in headerFooter.Sections)
    {
        if (!string.IsNullOrEmpty(section.Script)) headerTexts++;
        if (section.Image != null) headerImages++;
    }
}
```

#### When to Use

When the mark must appear on printed and exported copies. It is the standard
place for "CONFIDENTIAL" notices and for a company logo, precisely because it
repeats on every page without occupying a cell.

**Pros:**

- Prints on every page automatically
- Survives row and column edits entirely
- Holds both text and a picture per section

**Cons:**

- Invisible in the normal editing view, so it is easy to forget it is there
- Eighteen slots per sheet means checking one header proves nothing
- Removable through Page Setup by anyone who thinks to look

### Carrier 2: Worksheet background

#### Overview

A background is a picture tiled behind the cells, set through Page Layout.
`BackgroundImage` is null on sheets without one, which is most of them.

```csharp
foreach (SpreadsheetWorksheet worksheet in content.Worksheets)
{
    if (worksheet.BackgroundImage != null)
    {
        worksheet.BackgroundImage.Add(watermark);
        stamped++;
    }
}
```

#### When to Use

When the mark should be hard for a reader to remove casually. Unlike a shape
there is nothing to select and delete on the sheet itself - removing it means
knowing where the setting lives.

**Pros:**

- Cannot be selected or deleted on the sheet
- Tiles across the whole used range
- Reads as part of the document rather than an object placed on it

**Cons:**

- Does not print by default in Excel, so it protects the screen copy only
- Easy to miss when auditing - it renders behind data and scrolls with it
- One per worksheet; no per-range control

### Carrier 3: Shapes

#### Overview

Shapes are the visible layer: logos, callouts, pasted charts. Those carrying a
picture expose it through `Image`, and marking that image writes into the
picture data rather than adding another object.

```csharp
foreach (SpreadsheetShape shape in worksheet.Shapes)
{
    if (shape.Image != null)
    {
        shape.Image.Add(watermark);
        stamped++;
    }
}
```

#### When to Use

When the asset worth protecting is the picture itself - a chart or diagram
that would be valuable extracted from the workbook. A mark burned into the
image travels with it into whatever document it is pasted into.

**Pros:**

- Survives the picture being copied out of the workbook
- Immediately visible, so it communicates as well as protects
- Rich metadata (`Id`, `Name`, `AlternativeText`) for locating shapes later

**Cons:**

- The shape itself deletes in one click
- Only pictures can be marked; text boxes and autoshapes have a null `Image`
- Re-encodes the picture, so test the result where fidelity matters

### Carrier 4: Attachments

#### Overview

An OLE attachment is a whole file living inside the workbook. It is the
carrier most audits overlook, and the one where watermarking the workbook
achieves nothing at all.

```csharp
foreach (SpreadsheetAttachment attachment in worksheet.Attachments)
{
    Console.WriteLine($"  attachment: {attachment.SourceFullName} "
        + $"({attachment.Content.Length} bytes)");
    found++;
}
```

#### When to Use

Always check it, even when you do not intend to add one. The count answering
non-zero changes what "this workbook is marked" means: the attached file keeps
whatever marking it had when it was embedded.

**Pros:**

- `SourceFullName` and `Content` are enough for an audit report
- `AddAttachment` can embed a file with a preview image and frame rectangle
- Nothing needs extracting to disk to inspect it

**Cons:**

- A workbook-level watermark never reaches inside the attached file
- Shown only as an icon, so readers rarely notice it is there
- Marking the content means processing the attached file separately

## Side-by-Side Feature Comparison

| Capability | Header/footer | Background | Shape | Attachment |
|---|---|---|---|---|
| Holds text | Yes | No | Yes | n/a |
| Holds a picture | Yes | Yes | Yes | n/a |
| Image can be watermarked | Yes | Yes | Yes | No |
| Prints by default | Yes | No | Yes | No |
| Deletable in one click | No | No | Yes | Yes |
| Can hide an entire file | No | No | No | Yes |

## Real-World Use Cases

### Use Case 1: Pre-flight check before a data room upload

**Challenge:** Dozens of workbooks go into a diligence data room. Every one
must carry the deal's confidentiality marking, and none may carry leftovers
from earlier deals.

**Solution:** Run the inventory pass across the set, then mark what is missing
and clear what does not belong.

**Result:** A list of exactly which workbooks were already marked and where,
instead of a blanket re-marking that leaves stale notices in place.

### Use Case 2: Client workbook reused internally

**Challenge:** A model arrives from a client with their logo in the header and
a background marked INTERNAL. It becomes the basis for your own reporting, and
the markings must not survive.

**Solution:** Clear header and footer sections, then drop the worksheet
backgrounds.

**Result:** The structure and formulas are kept, and the other organisation's
branding and confidentiality notices are gone.

### Use Case 3: Charts lifted out of published workbooks

**Challenge:** Charts from a published workbook are being reused elsewhere
without attribution. A header mark does not follow a copied picture.

**Solution:** Mark the shape images, so the attribution is in the picture data.

**Result:** The mark travels with the chart wherever it is pasted.

## Best Practices and Recommendations

### Inventory first

Counting what a workbook already holds costs one load and no save. It is the
difference between "add a watermark" and knowing whether one is already there,
in a place nobody checked.

### Null-check every carrier

`BackgroundImage`, `section.Image` and `shape.Image` are null far more often
than not. The null checks are not defensive clutter; they are what keeps the
counts truthful.

### Return counts, not void

A pass that stamps nothing and a pass that stamps three images produce files
that look equally valid. Returning the count is what distinguishes them.

### Treat attachments as a separate problem

The workbook-level watermark stops at the attachment boundary. Extract, mark
and re-embed if the attached content genuinely needs marking.

## Common Pitfalls and How to Avoid Them

| Pitfall | Why it happens | Avoid it by |
|---|---|---|
| "The workbook has no watermark" | Only the editing view was checked | Running the inventory pass |
| Checking the primary header alone | Six header/footer types exist per sheet | Iterating `HeadersFooters` fully |
| Background mark missing from print | Excel does not print backgrounds | Using a header for printed copies |
| Attachment carries an unmarked copy | Workbook watermarks stop at the boundary | Checking the attachment count |
| Cleanup reports inflated numbers | Empty sections counted as cleared | Guarding on existing content |
| `shape.Image` throws | Text boxes and autoshapes hold no picture | Null-checking before `Add` |

## FAQ

**Why does my watermark not appear when printing?**

Worksheet backgrounds are screen-only in Excel; they are not printed. For a
mark that appears on paper and in PDF exports, use a header or footer, or
mark the shape images.

**How many header and footer slots does a worksheet really have?**

Eighteen: six `SpreadsheetHeaderFooter` objects - primary, even and first, as
header and footer - each with left, centre and right sections.

**Does watermarking the workbook mark its attachments?**

No. An attachment is a separate file stored inside the workbook, and it keeps
whatever marking it had when embedded. Check `Attachments` explicitly.

**Can I remove a watermark someone else added?**

Yes, for the carriers shown here: set `Script` and `Image` to null on header
sections, and `BackgroundImage` to null on the worksheet. A mark rasterised
into a picture cannot be undone - the original pixels are gone.

**Why mark the image instead of the sheet?**

Because a mark in the picture data survives the picture being copied into
another document, while anything placed on the sheet does not travel with it.

## Conclusion

The useful question about an Excel workbook is not whether it has a watermark
but which of the four carriers it uses. Headers print but hide on screen;
backgrounds show on screen but do not print; shapes are visible and deletable;
attachments are whole files that workbook-level marking never touches.

Start with the inventory pass. It takes one load, changes nothing, and
replaces an assumption with a list.

## See Also

- [Working with worksheet headers and footers](https://docs.groupdocs.com/watermark/net/working-with-worksheet-headers-and-footers/)
- [Working with worksheet backgrounds](https://docs.groupdocs.com/watermark/net/working-with-worksheet-backgrounds/)
- [Shapes in spreadsheet document](https://docs.groupdocs.com/watermark/net/shapes-in-spreadsheet-document/)
- [API Reference](https://reference.groupdocs.com/watermark/net/)
