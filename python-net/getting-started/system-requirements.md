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
GroupDocs.Watermark for Python via .NET ships as a self-contained wheel that bundles the .NET runtime it needs. No Microsoft Office, third-party document editor, .NET install or Mono install is required. On Linux and macOS a few system packages are needed; see [Platform Dependencies](#platform-dependencies). To install the library, follow the steps in the [Installation]({{< ref "watermark/python-net/getting-started/installation" >}}) guide.
{{< /alert >}}

## Supported Operating Systems

GroupDocs.Watermark for Python via .NET runs on Windows, Linux, and macOS. The package ships as a platform-specific `.whl` on PyPI and `pip` picks the correct one automatically.

### Windows

* Microsoft Windows 10 (x64)
* Microsoft Windows 11 (x64)
* Microsoft Windows Server 2016 and later

The Windows wheel is 64-bit only: use a 64-bit Python.

### Linux

* Any **x86-64** distribution with **glibc 2.27 or newer** — for example Ubuntu 18.04+, Debian 10+, RHEL 8+. The embedded .NET runtime needs glibc 2.27, and the wheel's `manylinux_2_27_x86_64` tag says so, so pip refuses an older system.

### macOS

* macOS 12 (Monterey) and later — Intel and Apple Silicon (M-series). Every binary of the embedded .NET runtime requires macOS 12, and the wheels are tagged `macosx_12_0_*` accordingly. Microsoft supports .NET 10 on macOS 14 and later.

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
| Linux x64 (glibc) | `py3-none-manylinux_2_27_x86_64.whl` |
| macOS Apple Silicon | `py3-none-macosx_12_0_arm64.whl` |
| macOS Intel | `py3-none-macosx_12_0_x86_64.whl` |

`pip` 20.3 or newer picks the right wheel for your platform; older versions do not recognise these tags, so upgrade with `python -m pip install --upgrade pip` (on Python 3.5, `python -m pip install "pip==20.3.4"`). On an Intel Mac, a Python built against a pre-11 macOS SDK reports its system as macOS 10.16 — there use pip 24.1 or newer, or run `SYSTEM_VERSION_COMPAT=0 pip install groupdocs-watermark-net`.

## Platform Dependencies

### Linux

Install **ICU**, **fontconfig**, **`libgdiplus`** and the **Microsoft core fonts**:

```bash
# Debian: enable the contrib component first (ttf-mscorefonts-installer lives there)
sudo sed -i '/^Components:/s/main/main contrib/' /etc/apt/sources.list.d/debian.sources
echo ttf-mscorefonts-installer msttcorefonts/accepted-mscorefonts-eula select true | sudo debconf-set-selections
sudo apt-get update
sudo apt-get install -y libicu-dev libfontconfig1 libgdiplus ttf-mscorefonts-installer fontconfig
sudo fc-cache -f

# Ubuntu: the same packages; ttf-mscorefonts-installer is in multiverse
sudo add-apt-repository -y multiverse
sudo apt-get install -y libicu-dev libfontconfig1 libgdiplus ttf-mscorefonts-installer fontconfig
```

What each package is for, measured on the 26.9 engine:

- **ICU** (`libicu-dev`, any version your distribution ships) — without it the runtime cannot start: the first call aborts the Python process with "Couldn't find a valid ICU package". Do not set `DOTNET_SYSTEM_GLOBALIZATION_INVARIANT=1` to work around it.
- **fontconfig** — the bundled SkiaSharp library loads `libfontconfig.so.1`.
- **`libgdiplus`** — needed for text watermarks on Word, Excel, PowerPoint, Visio and image files, for text watermarks on PDF files that set `sizing_type`, and for image watermarks, removal and previews on PowerPoint files. Without it these fail with "The type initializer for 'Gdip' threw an exception" (for PowerPoint text watermarks, a `NullReferenceException`). Everything else on PDF works without it, and so do image watermarks on Word, Excel, Visio and image files.
- **Microsoft core fonts** — a text watermark on a PDF file looks its font up by name and fails with `FontNotFoundException` when that font is not installed. Metric-compatible substitutes such as Liberation are not picked up; alternatively, use a font that is installed.

PowerPoint page previews do not work on Linux and macOS, even with `libgdiplus`: the engine renders slides through a GDI+ call that `libgdiplus` does not implement, and `generate_preview` raises "Not implemented.". Generate PowerPoint previews on Windows; previews of every other format work.

### macOS

Install `mono-libgdiplus` using [Homebrew](https://brew.sh/), for the same features as on Linux:

```bash
brew install mono-libgdiplus
```

If you see a `DllNotFoundException: libSkiaSharp` error after upgrading, an older system copy of SkiaSharp is shadowing the one bundled with the wheel. Rename it so the bundled copy wins:

```bash
sudo mv /usr/local/lib/libSkiaSharp.dylib /usr/local/lib/libSkiaSharp.dylib.bak
```

### Windows

No extra dependencies — the wheel is self-contained.
