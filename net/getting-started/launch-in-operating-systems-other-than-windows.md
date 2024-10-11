---
id: launch-in-operating-systems-other-than-windows
url: watermark/net/launch-in-operating-systems-other-than-windows
title: Launch in operating systems other than windows
weight: 7
description: ""
keywords: 
productName: GroupDocs.Watermark for .NET
hideChildren: True
---
## Limitations

1. Because of the lack of Windows fonts in target OS (Android, macOS, Linux, etc), fonts used in documents are substituted with available fonts, this might lead to inaccurate document layout when rendering the document to PNG, JPG, and PDF.
2. If GroupDocs.Watermark for .NET Standard is intended to be used in a Linux environment, an additional NuGet package should be referenced to make it work correctly with graphics: [SkiaSharp.NativeAssets.Linux](https://www.nuget.org/packages/SkiaSharp.NativeAssets.Linux) for Ubuntu (it also should work on most Debian-based Linux distributions) or [Goelze.SkiaSharp.NativeAssets.AlpineLinux](https://www.nuget.org/packages/Goelze.SkiaSharp.NativeAssets.AlpineLinux) for Alpine Linux.

## Recommendations

When using GroupDocs.Watermark in a non-Windows environment, the following packages should be installed to improve rendering results and prevent possible runtime errors:

1. libgdiplus - is the Mono library that provides a GDI+-compatible API on non-Windows operating systems.
2. libc6-dev - package contains the symlinks, headers, and object files needed to compile and link programs which use the standard C library.
3. ttf-mscorefonts-installer - package with Microsoft compatible fonts.

To install packages on Debian-based Linux distributions use [apt-get](https://wiki.debian.org/apt-get) utility:

1. sudo apt-get install libgdiplus
2. sudo apt-get install libc6-dev
3. sudo apt-get install ttf-mscorefonts-installer

## How to run .net GroupDocs.Watermark in the Docker

Running GroupDocs.Watermark in Docker is straightforward. All you need to do is add the installation of the packages described in the previous paragraph to the docker file. An example beginning of the Dockerfile might look like this:

```Dockerfile
FROM mcr.microsoft.com/dotnet/aspnet:6.0 AS base
WORKDIR /app
EXPOSE 80

# Add libgdiplus, libc6-dev
RUN apt-get update && apt-get install -y apt-utils libgdiplus libc6-dev

# Add `contrib` archive area to package sources list
RUN sed -i'.bak' 's/$/ contrib/' /etc/apt/sources.list
# Add fonts
RUN apt-get update; apt-get install -y ttf-mscorefonts-installer fontconfig
RUN fc-cache -f -v

# etc
```

**fontconfig:** This library configures and customizes font access.

**ttf-mscorefonts-installer:** This package provides Microsoft TrueType core fonts. It's available in the [contrib](https://www.debian.org/doc/debian-policy/ch-archive#s-contrib) archive area. (Note: Using non-free fonts may have licensing implications, so be sure to check the license terms.)
