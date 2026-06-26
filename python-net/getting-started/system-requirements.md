---
id: system-requirements
url: watermark/python-net/system-requirements
title: System Requirements
linkTitle: System Requirements
weight: 3
description: "System requirements for GroupDocs.Watermark for Python via .NET — supported operating systems, Python versions, and optional platform dependencies."
keywords: GroupDocs.Watermark for Python via .NET, system requirements, Windows, Linux, Python 3.5
productName: GroupDocs.Watermark for Python via .NET
hideChildren: false
toc: true
---

{{< alert style="info" >}}
GroupDocs.Watermark for Python via .NET does not require any external software such as Microsoft Office or third-party document editors. To install the library, follow the steps in the [Installation]({{< ref "watermark/python-net/getting-started/installation" >}}) guide.
{{< /alert >}}

## Supported Operating Systems

GroupDocs.Watermark for Python via .NET runs on Windows, Linux, and macOS. The package ships as a platform-specific `.whl` on PyPI and `pip` picks the correct one automatically.

### Windows

* Microsoft Windows 10 (x64)
* Microsoft Windows 11 (x64)
* Microsoft Windows Server 2016 and later

### Linux

* Ubuntu 20.04+, Debian 11+, CentOS 8+, Fedora 36+ (glibc-based distributions)

### macOS

* macOS 12 (Monterey) and later — Intel and Apple Silicon (M-series)

## Python Version

GroupDocs.Watermark for Python via .NET supports **Python 3.5 through 3.14**. The wheel uses the `py3-none-{platform}` tag, meaning it works with any Python 3.x version in that range without per-version rebuilds.

| Python Version | Supported |
| --- | :---: |
| 3.5  | Yes |
| 3.6  | Yes |
| 3.7  | Yes |
| 3.8  | Yes |
| 3.9  | Yes |
| 3.10 | Yes |
| 3.11 | Yes |
| 3.12 | Yes |
| 3.13 | Yes |
| 3.14 | Yes |

## Package Manager

GroupDocs.Watermark for Python via .NET is distributed via [PyPI](https://pypi.org/project/groupdocs-watermark-net/):

```bash
pip install groupdocs-watermark-net
```

The PyPI index hosts one wheel per platform:

| Platform | Wheel suffix |
| --- | --- |
| Windows 64-bit | `py3-none-win_amd64.whl` |
| Linux x64 (glibc) | `py3-none-manylinux1_x86_64.whl` |
| macOS Apple Silicon | `py3-none-macosx_11_0_arm64.whl` |
| macOS Intel | `py3-none-macosx_10_14_x86_64.whl` |

## Optional Platform Dependencies

GroupDocs.Watermark uses `libgdiplus` for drawing routines when a document contains images or rasterized output is produced. On Windows no extra setup is required. On Linux install `libgdiplus` and a minimal font set so that image-bearing documents render correctly.

### Linux

Install the following packages on Debian / Ubuntu derivatives:

```bash
sudo apt-get update
sudo apt-get install -y libgdiplus libfontconfig1 libicu-dev ttf-mscorefonts-installer
```

- **libgdiplus** — Mono library providing a GDI+-compatible API on non-Windows operating systems.
- **libfontconfig1** — needed for drawing functions (image and font rendering).
- **libicu-dev** — required by the .NET runtime. Do **not** set `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT`, as it disables culture-sensitive operations.
- **ttf-mscorefonts-installer** — Microsoft-compatible fonts used by many Office-format documents. If it is not available, add the `contrib` component to your apt sources and re-run `apt-get update`.

### macOS

Install `libgdiplus` using [Homebrew](https://brew.sh/):

```bash
brew install mono-libgdiplus
```

If you see a `DllNotFoundException: libSkiaSharp` error after upgrading, an older system copy of SkiaSharp is shadowing the one bundled with the wheel. Rename it so the bundled copy wins:

```bash
sudo mv /usr/local/lib/libSkiaSharp.dylib /usr/local/lib/libSkiaSharp.dylib.bak
```

### Windows

No extra dependencies — the wheel is self-contained.
