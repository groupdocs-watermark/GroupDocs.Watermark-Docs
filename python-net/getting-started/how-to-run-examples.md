---
id: how-to-run-examples
url: watermark/python-net/how-to-run-examples
title: How to run examples
weight: 7
description: "How to clone, set up, and run the GroupDocs.Watermark for Python via .NET example suite — locally, with a license, or in Docker."
keywords: "groupdocs watermark python, examples, docker, ci"
productName: GroupDocs.Watermark for Python via .NET
hideChildren: False
toc: True
---

The complete project [GroupDocs.Watermark for Python via .NET](https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Python-via-.NET) with code examples and sample files is hosted on GitHub.

## Prerequisites

- [Python 3.5–3.14](https://www.python.org/downloads/).
- On Linux, ICU, fontconfig, `libgdiplus` and the Microsoft core fonts (`libicu-dev libfontconfig1 libgdiplus ttf-mscorefonts-installer`). On macOS: `mono-libgdiplus` (via Homebrew). See [System Requirements]({{< ref "watermark/python-net/getting-started/system-requirements.md" >}}) for what each one is needed for.

## Get the code

```bash
git clone https://github.com/groupdocs-watermark/GroupDocs.Watermark-for-Python-via-.NET.git
cd ./GroupDocs.Watermark-for-Python-via-.NET/Examples
```

## Project structure

```
Examples/
├── run_all_examples.py     # Runs every example and prints a pass/fail summary
├── _run_example.py         # Per-example wrapper (applies the license, reports evaluation and font errors)
├── requirements.txt
├── licensing/              # Set a license from a file, a stream, or a metered key
├── getting-started/
│   └── hello-world/        # Minimal add-a-watermark example
└── developer-guide/
    ├── basic-usage/        # Add text/image/custom-font/tile watermarks, document info, formats
    └── advanced-usage/     # Loading options, format-specific placement, search & modify
```

## Set up

```bash
pip install -r requirements.txt
```

To run the examples with the full feature set, apply a license. The simplest way is the `GROUPDOCS_LIC_PATH` environment variable, which the package applies automatically at import:

{{< tabs "set-license" >}}
{{< tab "Windows" >}}
```batch
set GROUPDOCS_LIC_PATH=C:\path\to\GroupDocs.Watermark.lic
```
{{< /tab >}}
{{< tab "Linux / macOS" >}}
```bash
export GROUPDOCS_LIC_PATH=/path/to/GroupDocs.Watermark.lic
```
{{< /tab >}}
{{< /tabs >}}

Without a license the suite still runs, in evaluation mode: each document an example saves carries an evaluation mark. Each example runs in its own subprocess.

## Run the examples

Run the full suite, which prints a pass/fail summary at the end:

```bash
python run_all_examples.py
```

You can also run any single example by navigating to its folder and running the script directly — each example uses paths relative to its own folder, and writes its result next to the script as `output.*`:

```bash
cd getting-started/hello-world
python hello_world.py
```

## Run with Docker

The repository ships a `Dockerfile` that builds a Linux image with Python 3.13, the system packages the library needs on Linux (ICU, fontconfig, `libgdiplus` and the Microsoft core fonts), and the package preinstalled.

```bash
# Build the image
docker build -t watermark-examples .

# Run unlicensed (evaluation mode)
docker run --rm watermark-examples

# Run with a license mounted from the host
docker run --rm \
    -v /path/to/license:/lic:ro \
    -e GROUPDOCS_LIC_PATH=/lic/your-license.lic \
    watermark-examples
```

## Continuous integration

The `.github/workflows/` directory contains a workflow that runs the full example suite on every push, on `ubuntu-latest` with Python 3.13. The same matrix is reproducible locally via the `Dockerfile` above.

## Troubleshooting

- **"The type initializer for 'Gdip' threw an exception"** or **`DllNotFoundException: libgdiplus`** (Linux/macOS) — install the GDI+ library: `sudo apt install libgdiplus` (Linux) or `brew install mono-libgdiplus` (macOS). Text watermarks on Word, Excel, PowerPoint, Visio and image files, PDF text watermarks that set `sizing_type`, and image watermarks, removal and previews on PowerPoint files need it.
- **`FontNotFoundException`** when adding a text watermark to a PDF (Linux) — install the font the watermark names; for Arial and the other Microsoft fonts: `sudo apt install ttf-mscorefonts-installer fontconfig && sudo fc-cache -f` (on Debian, enable the `contrib` component first). Liberation fonts are not substituted.
- **"Not implemented."** from a PowerPoint preview example (Linux/macOS) — PowerPoint previews need a GDI+ feature `libgdiplus` lacks; run them on Windows.
- **"Couldn't find a valid ICU package"**, with the Python process ending abruptly — install ICU (`libicu-dev` on Debian and Ubuntu).
- **Evaluation marks in the output** — "Evaluation only. Created with GroupDocs.Watermark." on PDF and image files, "Created with evaluation version of GroupDocs.Watermark" on Word, PowerPoint and Visio files, an "Evaluation Warning" worksheet in Excel files. Apply a license (see above) to remove them; a free 30-day [temporary license](https://purchase.groupdocs.com/temporary-license) is available.

## Contribute

If you would like to add or improve an example, we encourage you to contribute to the project. All examples in this repository are open source and can be freely used in your own applications. Fork the repository, edit the source code, and open a pull request.
