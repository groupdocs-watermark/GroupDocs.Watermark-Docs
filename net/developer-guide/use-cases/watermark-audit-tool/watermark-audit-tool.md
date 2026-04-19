---
id: watermark-audit-compliance
url: watermark/net/watermark-audit-compliance
title: Watermark Auditing for PDF Compliance with GroupDocs.Watermark for .NET
weight: 10
description: "Automate PDF watermark compliance checks using GroupDocs.Watermark for .NET."
keywords: "GroupDocs.Watermark, .NET, PDF, watermark audit, compliance, branding, document security, automation"
productName: "GroupDocs.Watermark for .NET"
structuredData:
    showOrganization: True
toc: true
hideChildren: false
draft: true
---

{{< alert style="info" >}} The complete source code for this use case is available on GitHub: [groupdocs-watermark/watermark-audit-tool-dotnet](https://github.com/groupdocs-watermark/watermark-audit-tool-dotnet).{{< /alert >}}

## Overview

Enterprises that distribute PDF contracts, marketing collateral, or technical manuals often embed watermarks to protect intellectual property and enforce branding rules. Manually opening each file to verify that a specific text watermark (e.g., "Confidential") appears on every page is error-prone, especially when thousands of documents are involved. This use-case shows how to automate a full-document audit using `Watermarker` and `TextSearchCriteria`, confirm that the required watermark exists on every page, verify formatting rules, and produce a concise compliance report.

## Prerequisites

- **.NET runtime** 6.0 or newer.
- **GroupDocs.Watermark** NuGet package (`GroupDocs.Watermark`).
- A temporary or permanent GroupDocs.Watermark license key (optional for evaluation).
- PDF files located in a local folder that you want to audit.

## Installation

Add the Watermark package to your project with the .NET CLI:

```bash
dotnet add package GroupDocs.Watermark
```

## Repository Structure

```
watermark-audit-tool/
│
├── WatermarkAuditTool/
│   ├── Program.cs
│   ├── WatermarkAuditTool.csproj
│   ├── Resources/
│   │   ├── Logos/
│   │   │   └── expected-logo.png
│   │   └── SampleDocs/
│   │       ├── sample-draft.pdf
│   │       └── sample-watermarked.pdf
│   └── Results/
```

## Usage Example

Below is a step-by-step guide based on the actual `Program.cs` in the sample repository.

### 1. Scan a document for all existing watermarks

Use the parameterless `Search()` method on a `Watermarker` instance to enumerate every watermark, including text, position, rotation, and image data:

```csharp
using (Watermarker watermarker = new Watermarker(filePath))
{
    PossibleWatermarkCollection watermarks = watermarker.Search();

    foreach (PossibleWatermark wm in watermarks)
    {
        Console.WriteLine($"  Text: {wm.Text ?? "(image)"}");
        Console.WriteLine($"  Position: X={wm.X}, Y={wm.Y}");
        Console.WriteLine($"  Rotation: {wm.RotateAngle} degrees");
        Console.WriteLine($"  Page: {wm.PageNumber}");
    }
}
```

### 2. Verify required text watermark is present

Build a `TextSearchCriteria` with `SkipUnreadableCharacters` enabled to detect obfuscated or fragmented watermarks. The search returns a PASS/FAIL flag:

```csharp
using (Watermarker watermarker = new Watermarker(filePath))
{
    TextSearchCriteria criteria =
        new TextSearchCriteria(expectedText);
    criteria.SkipUnreadableCharacters = true;

    PossibleWatermarkCollection found = watermarker.Search(criteria);
    bool passed = found.Count > 0;

    Console.WriteLine($"  [{(passed ? "PASS" : "FAIL")}] " +
        $"expected '{expectedText}', " +
        $"found {found.Count} match(es)");
}
```

### 3. Run a multi-rule compliance report

Combine `TextSearchCriteria` with `TextFormattingSearchCriteria` using the `.And()` operator to check font, size, and bold style in addition to text presence:

```csharp
var textCriteria = new TextSearchCriteria(expectedText);

// Check text + font name
var fontCriteria = new TextFormattingSearchCriteria
    { FontName = "Arial" };
CheckRule(watermarker, textCriteria.And(fontCriteria),
    "Font 'Arial'", ref passed, ref failed);

// Check text + minimum font size
var sizeCriteria = new TextFormattingSearchCriteria
    { MinFontSize = 15 };
CheckRule(watermarker, textCriteria.And(sizeCriteria),
    "Min font size >= 15", ref passed, ref failed);
```

A separate helper verifies page coverage by collecting watermarked page numbers and comparing against the total page count. The final verdict is COMPLIANT or NON-COMPLIANT.

### 4. Replace outdated watermark text

Locate watermarks by old text, clear their `FormattedTextFragments`, and add new text with updated font and color:

```csharp
using (Watermarker watermarker = new Watermarker(filePath))
{
    var criteria = new TextSearchCriteria(oldText, false);
    var watermarks = watermarker.Search(criteria);

    foreach (PossibleWatermark wm in watermarks)
    {
        wm.FormattedTextFragments.Clear();
        wm.FormattedTextFragments.Add(
            newText,
            new Font("Arial", 19, FontStyle.Bold),
            Color.DarkBlue,
            Color.Transparent);
    }

    watermarker.Save(outputPath);
}
```

The screenshot below shows the result — the old watermark text has been replaced with the new text, font, and color:

![Text replacement result](watermark/net/images/text-replaced-example.png)

{{< alert style="info" >}} The sample project also demonstrates adding invisible tracking watermarks for leak detection and recovering them with regex-based `TextSearchCriteria`. See `AddTrackingWatermark` and `DetectTrackingWatermark` in `Program.cs`.{{< /alert >}}

The `RemoveWatermarksByCriteria` method in the sample project demonstrates targeted removal — only watermarks matching both text and formatting criteria are deleted:

![Watermark removal result](watermark/net/images/watermarks-removed-example.png)

## Notes

- The sample works with any document format supported by GroupDocs.Watermark (DOCX, PPTX, etc.). Replace the `*.pdf` filter with `*.*` to audit a mixed folder.
- For large collections, consider processing files in parallel (`Parallel.ForEach`) — the Watermark SDK is thread-safe when each thread uses its own `Watermarker` instance.
- If you need to audit encrypted PDFs, pass the password to `Watermarker` via the constructor overload.
- The free evaluation license limits the number of processed pages; acquire a full license for production workloads.

## See Also

- [GroupDocs.Watermark .NET Documentation](https://docs.groupdocs.com/watermark/net/)
- [GroupDocs.Watermark .NET API Reference](https://reference.groupdocs.com/watermark/net/)
- [Get a Temporary License](https://purchase.groupdocs.com/temp-license/100354)
- [GroupDocs.Watermark Forum](https://forum.groupdocs.com/c/watermark/19)
