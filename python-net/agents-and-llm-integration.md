---
id: agents-and-llm-integration
url: watermark/python-net/agents-and-llm-integration
title: AI agents and LLM integration
linkTitle: Agents and LLMs
weight: 6
description: "Use GroupDocs.Watermark for Python via .NET with AI coding assistants and LLMs — the bundled AGENTS.md reference, the GroupDocs MCP server, and machine-readable documentation."
keywords: AI agents, LLM, AGENTS.md, MCP, Claude, Cursor, Copilot, watermark, python
productName: GroupDocs.Watermark for Python via .NET
hideChildren: False
toc: True
---

GroupDocs.Watermark for Python via .NET is designed to work smoothly with AI coding assistants such as Claude Code, Cursor, and GitHub Copilot in agent mode.

## Built into the package

The `groupdocs-watermark-net` wheel ships a bundled `AGENTS.md` reference. Once the package is installed, AI tools discover it automatically at `groupdocs/watermark/AGENTS.md`. It covers the canonical imports, the open → add → save workflow, per-operation recipes, licensing, the full API-surface tables, and troubleshooting — everything an agent needs to write correct watermarking code without guessing.

## MCP server

For on-demand documentation lookups, point your AI tool at the GroupDocs MCP server:

```json
{
  "mcpServers": {
    "groupdocs-docs": {
      "url": "https://docs.groupdocs.com/mcp"
    }
  }
}
```

This works with Claude Code (`~/.claude/settings.json`), Cursor (`.cursor/mcp.json`), VS Code Copilot (`.vscode/mcp.json`), and any MCP-compatible client.

## Machine-readable documentation

LLM-optimized documentation for retrieval-augmented generation and context loading is available at [`https://docs.groupdocs.com/watermark/python-net/llms-full.txt`](https://docs.groupdocs.com/watermark/python-net/llms-full.txt).

## AGENTS.md reference

The complete reference bundled inside the wheel is reproduced below.

````markdown
# GroupDocs.Watermark for Python via .NET -- AGENTS.md

> Instructions for AI agents working with this package.

Add, search, and remove text and image watermarks across PDF, Word, Excel, PowerPoint, Visio, email, and image formats through one unified API -- with no MS Office or other external software installed.

## Install

```bash
pip install groupdocs-watermark-net
```

**Python**: 3.5 - 3.14 (pip 20.3+) | **Platforms**: Windows x64, Linux x64, macOS x64/ARM64 -- 64-bit only

## Resources

| Resource | URL |
|---|---|
| Documentation | https://docs.groupdocs.com/watermark/python-net/ |
| LLM-optimized docs | https://docs.groupdocs.com/watermark/python-net/llms-full.txt |
| API reference | https://reference.groupdocs.com/watermark/python-net/ |
| Code examples | https://docs.groupdocs.com/watermark/python-net/developer-guide/ |
| Release notes | https://releases.groupdocs.com/watermark/python-net/release-notes/ |
| PyPI | https://pypi.org/project/groupdocs-watermark-net/ |
| Free support forum | https://forum.groupdocs.com/c/watermark/ |
| Temporary license | https://purchase.groupdocs.com/temporary-license |

## MCP Server

If your environment has MCP configured, you can connect your AI tool to the GroupDocs documentation server for on-demand API lookups:

```json
{
  "mcpServers": {
    "groupdocs-docs": {
      "url": "https://docs.groupdocs.com/mcp"
    }
  }
}
```

Works with Claude Code (`~/.claude/settings.json`), Cursor (`.cursor/mcp.json`), VS Code Copilot (`.vscode/mcp.json`), and any MCP-compatible client. If MCP is unavailable, fall back to the LLM-optimized docs URL above and this file -- both are shipped inside the wheel.

## Imports

```python
from groupdocs.watermark import License, Metered, Watermarker, WatermarkerSettings, UnitOfMeasurement
from groupdocs.watermark.common import Attachment, AttachmentWatermarkableImage, Dimension, FileType, FormatFamily, HorizontalAlignment, VerticalAlignment, IDocumentInfo, PageInfo, Point, Rectangle
from groupdocs.watermark.options import LoadOptions, OoxmlLoadOptions, SaveOptions, WatermarkOptions, PreviewOptions, PreviewFormats, CreatePageStream, ReleasePageStream
from groupdocs.watermark.watermarks import TextWatermark, ImageWatermark, Color, Font, FontStyle, TextAlignment, SizingType, MarginType, Margins, TileOptions, Thickness
from groupdocs.watermark.watermarks.results import AddWatermarkResult, ImageWatermarkResult, TextWatermarkResult, WatermarkPosition, WatermarkType
from groupdocs.watermark.search import PossibleWatermark, PossibleWatermarkCollection, FormattedTextFragment, FormattedTextFragmentCollection
from groupdocs.watermark.search.search_criteria import TextSearchCriteria, ImageSearchCriteria, ColorRange, SizeSearchCriteria, RotateAngleSearchCriteria
```

> Format-specific content/options live under sub-namespaces: `groupdocs.watermark.contents.{pdf,word_processing,spreadsheet,presentation,diagram,email,image}` and `groupdocs.watermark.options.{...}` mirror them. Import these only when you need format-specific shape/content access.

## Add Text Watermark

```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import TextWatermark, Font, Color

with Watermarker("document.pdf") as watermarker:
    watermark = TextWatermark("CONFIDENTIAL", Font("Arial", 48))
    watermark.foreground_color = Color.red
    watermark.opacity = 0.5
    watermarker.add(watermark)
    watermarker.save("watermarked.pdf")
```

## Add Image Watermark

```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.watermarks import ImageWatermark, SizingType

with Watermarker("document.docx") as watermarker:
    watermark = ImageWatermark("logo.png")
    watermark.sizing_type = SizingType.SCALE_TO_PARENT_DIMENSIONS
    watermark.scale_factor = 0.5
    watermark.opacity = 0.7
    watermarker.add(watermark)
    watermarker.save("watermarked.docx")
```

## Search and Remove Watermarks

```python
from groupdocs.watermark import Watermarker
from groupdocs.watermark.search.search_criteria import TextSearchCriteria

with Watermarker("watermarked.pdf") as watermarker:
    criteria = TextSearchCriteria("CONFIDENTIAL")     # also: ImageSearchCriteria(...)
    possible = watermarker.search(criteria)
    for wm in possible:
        print(wm.text, wm.x, wm.y)
    watermarker.remove(possible)                       # remove the whole collection
    watermarker.save("clean.pdf")
```

## Callbacks: pass Python functions and objects

Wherever the engine takes a callback type, pass plain Python:

| .NET type | Pass |
|---|---|
| `CreatePageStream` / `ReleasePageStream` (`PreviewOptions(create, release)`) | `create(page_number) -> stream`, `release(page_number, stream)` |
| `ILogger` (`WatermarkerSettings.logger`) | an object with `trace(message)`, `warning(message)`, `error(message, exception)` -- or a function `fn(level, message, exception)` |

- A create callback returns a writable file object (`open(path, "wb")`), an `io.BytesIO`, or a .NET `Stream`.
- The release callback gets back **the same object** create returned. The bytes are already complete by then: a file is closed and a `BytesIO` is filled.
- A `release` taking one argument (`release(page_number)`) is accepted too. `PreviewOptions(create)` alone works as well; the engine then closes each stream itself.
- The engine logs a `trace` when it opens a file and an `error` (with the .NET exception's text) when it cannot load one. Failures inside release and logger callbacks are ignored, so cleanup and logging cannot break watermarking.

```python
from groupdocs.watermark import Watermarker, WatermarkerSettings
from groupdocs.watermark.options import PreviewOptions, PreviewFormats

class PrintLogger(object):
    def trace(self, message):
        print("trace:", message)

    def warning(self, message):
        print("warning:", message)

    def error(self, message, exception):
        print("error:", message, exception)

def create_page_stream(page_number):
    return open("page-%d.png" % page_number, "wb")

def release_page_stream(page_number, stream):
    stream.close()

settings = WatermarkerSettings()
settings.logger = PrintLogger()
with Watermarker("document.pdf", settings) as watermarker:
    options = PreviewOptions(create_page_stream, release_page_stream)
    options.preview_format = PreviewFormats.PNG
    options.page_numbers = [1]
    watermarker.generate_preview(options)
```

## Upgrading from 26.6

- `release(page_number, stream)` now gets the stream `create` returned; 26.6 passed `None`.
- Previews written through a release callback are complete, and `BytesIO` pages are filled; 26.6 could truncate a spreadsheet page and left `BytesIO` pages empty.
- `WatermarkerSettings.logger` takes a Python object or function (26.6 raised `TypeError: cannot wrap`).
- Assigning an attribute a class does not have raises `AttributeError` with a suggestion; 26.6 stored it silently, so a misspelled property changed nothing.
- Python 3.5 - 3.7 work (26.6 failed to import on 3.5/3.6 and on first use on 3.7).
- Evaluation mode allows several watermarks per document, search, and removal (engine 26.9).

## Licensing

```python
from groupdocs.watermark import License

# From file
License().set_license("path/to/license.lic")

# From stream
with open("license.lic", "rb") as f:
    License().set_license(f)
```

Or auto-apply: `export GROUPDOCS_LIC_PATH="path/to/license.lic"`

**Evaluation vs licensed** (measured on engine 26.9). Without a license every feature runs -- several watermarks per document, search and removal included -- and there is no document-count cap, but each saved document carries an evaluation mark: the line "Evaluation only. Created with GroupDocs.Watermark." on PDF and image files, "Created with evaluation version of GroupDocs.Watermark" on Word, PowerPoint and Visio files, and an extra "Evaluation Warning" worksheet in Excel files. Search reports the PDF, PowerPoint and Visio lines as possible watermarks. Set `GROUPDOCS_LIC_PATH` (or call `License().set_license(...)`) and re-run to clear them. A 30-day full license is free: https://purchase.groupdocs.com/temporary-license

## Supported Formats

| Category | Formats |
|---|---|
| **Word Processing** | DOC, DOCX, DOCM, DOT, DOTX, RTF, ODT, OTT |
| **Spreadsheets** | XLS, XLSX, XLSM, XLSB, ODS |
| **Presentations** | PPT, PPTX, PPTM, PPS, PPSX, ODP |
| **Fixed-Layout** | PDF |
| **Diagrams** | VSD, VSDX, VSS, VST, VDX |
| **Email** | MSG, EML, EMLX |
| **Images** | BMP, JPG, JPEG, PNG, GIF, TIFF, WEBP |

## API Reference

### Watermarker

| Method | Returns | Description |
|---|---|---|
| `Watermarker(file_path)` | | Open a document (path, or a file-like stream) |
| `get_document_info()` | `IDocumentInfo` | Format, page count, per-page dimensions |
| `add(watermark)` | `AddWatermarkResult` | Add a text or image watermark |
| `search(search_criteria=None)` | `PossibleWatermarkCollection` | Find existing watermarks (optionally filtered) |
| `remove(possible_watermark)` | `None` | Remove a watermark or a whole collection |
| `get_images(search_criteria=None)` | `WatermarkableImageCollection` | Enumerate raster images in the document |
| `generate_preview(preview_options)` | `None` | Render pages to images via a page-stream callback |
| `get_content()` | `Content` | Format-specific content tree (advanced) |
| `save(file_path)` | `WatermarkResult` | Save to a path, or a file-like stream |
| `dispose()` | `None` | Release the document (or use a `with` block) |

### Watermark types

- `TextWatermark(text, font)` — `foreground_color`, `background_color`, `opacity`, `rotate_angle`, `sizing_type`, `text_alignment`, `horizontal_alignment`, `vertical_alignment`, `margins`, `tile_options`.
- `ImageWatermark(file_path)` or `ImageWatermark(stream=...)` — `opacity`, `scale_factor`, `sizing_type`, `rotate_angle`, alignment + margins as above.

## Key Patterns

- **Properties**: use `snake_case` -- auto-mapped to .NET `PascalCase`
- **Context managers**: `with Watermarker(...) as x:` ensures resources are released
- **Streams**: pass `open("file", "rb")` or `io.BytesIO(data)` where .NET expects Stream
- **Stream write-back**: `BytesIO` objects are updated after .NET writes to them
- **Colors**: `Color.red`, `Color(255, 0, 0)`, `Color.from_argb(...)`, or `"#RRGGBB"` strings (see `groupdocs.watermark.watermarks.Color`)
- **Enums**: case-insensitive, lazy-loaded (e.g., `FileType.DOCX`, `SizingType.SCALE_TO_PARENT_DIMENSIONS`)
- **Collections**: `for item in result` and `len(result)` work on .NET collections (e.g. `search()` results)
- **Attribute names**: assigning an attribute a class does not have raises `AttributeError` with a "Did you mean" hint (`watermark.opactiy = 0.5` -> `opacity`)

## Platform Requirements

| Platform | Requirements |
|---|---|
| Windows x64 | None |
| Linux x64 (glibc 2.27+: Ubuntu 18.04+, Debian 10+, RHEL 8+) | `apt install libicu-dev libfontconfig1 libgdiplus ttf-mscorefonts-installer` (Debian: enable `contrib` first) |
| macOS 12+ (x64, ARM64) | `brew install mono-libgdiplus` |

What each one is for, measured on the 26.9 engine:
- **libgdiplus** -- text watermarks on Word, Excel, PowerPoint, Visio and image files, text watermarks on PDF files that set `sizing_type` (anything but the default `SizingType.AUTO`), and image watermarks, removal and previews on PowerPoint files. The rest of PDF needs none of it; image watermarks on Word, Excel, Visio and image files work without it.
- **Microsoft core fonts** -- text watermarks on PDF files, which look their font up by name (`Font("Arial", ...)`). Metric-compatible substitutes (Liberation) are not picked up.

The wheel tags state the OS floors (`manylinux_2_27_x86_64`, `macosx_12_0_x86_64`, `macosx_12_0_arm64`), so pip 20.3+ refuses an older OS up front.

## Troubleshooting

**`The type initializer for 'Gdip' threw an exception` / `DllNotFoundException: libgdiplus` when adding a watermark** (Linux/macOS) -- install libgdiplus: `sudo apt install libgdiplus` (Linux) / `brew install mono-libgdiplus` (macOS). Only the features listed under Platform Requirements need it; `import` and almost everything on PDF work without it

**`FontNotFoundException` when adding a text watermark to a PDF** (Linux) -- install the font the watermark names; for Arial and the other Microsoft fonts: `sudo apt install ttf-mscorefonts-installer fontconfig && sudo fc-cache -f` (Debian: enable `contrib`)

**`Not implemented.` from `generate_preview` on a PowerPoint file** (Linux/macOS) -- the PowerPoint preview path needs a GDI+ feature libgdiplus does not implement; generate PowerPoint previews on Windows. Previews of the other formats work

**`DllNotFoundException: libSkiaSharp`** -- stale system copy conflicts with bundled version. Rename it: `sudo mv /usr/local/lib/libSkiaSharp.dylib /usr/local/lib/libSkiaSharp.dylib.bak`

**The process aborts on first use with `Couldn't find a valid ICU package`** (Linux; exit code 134, no Python exception) -- install ICU: `sudo apt install libicu-dev`, and do NOT set `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT`

**`TypeLoadException`** -- reinstall: `pip install --force-reinstall groupdocs-watermark-net`

**Still stuck?** Post your question at https://forum.groupdocs.com/c/watermark/ -- the development team responds directly.
````
