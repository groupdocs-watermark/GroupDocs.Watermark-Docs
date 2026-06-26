---
id: licensing-and-evaluation
url: watermark/python-net/licensing-and-evaluation
title: Licensing and evaluation
weight: 5
keywords: free, free trial, subscription, evaluation, groupdocs watermark python
description: "GroupDocs.Watermark for Python via .NET offers flexible licensing options, including a Free Trial and a 30-day Temporary License for evaluation purposes."
productName: GroupDocs.Watermark for Python via .NET
hideChildren: False
toc: True
aliases:
    - /watermark/python-net/licensing-and-subscription/
---

To explore the system effectively, you may want immediate access to the API. GroupDocs.Watermark simplifies this by offering various purchase plans, along with a Free Trial and a 30-day Temporary License for evaluation.

{{< alert style="info" >}}

To learn more about licensing options, purchasing, and evaluation policies, refer to the [Purchase Policies and FAQ](https://purchase.groupdocs.com/policies) section.

{{< /alert >}}

## Purchased License

After purchasing GroupDocs.Watermark for Python via .NET, you will receive a license file that unlocks the full functionality of the API. A few rules apply:

- Apply the license **only once** per process, in your start-up code.
- Apply it **before** constructing any `Watermarker` or other GroupDocs.Watermark object.
- A license can be applied from a file path, from a binary stream (handy when the license is an embedded resource), or as a [Metered License](https://purchase.groupdocs.com/faqs/licensing/metered/) that bills by usage.

Use the [set_license](https://reference.groupdocs.com/watermark/python-net/) method to license the component. Calling it more than once is harmless — it simply wastes a little processor time.

### Set a license from a file

The example below applies a license from a file path. It reads the path from the `GROUPDOCS_LIC_PATH` environment variable and falls back to a local `GroupDocs.Watermark.lic` file:

{{< tabs "code-example-set-license-from-file" >}}
{{< tab "set_license_from_file.py" >}}
```python
import os
from groupdocs.watermark import License

def set_license_from_file():
    # Resolve the license path from the environment, with a local fallback
    license_path = os.environ.get("GROUPDOCS_LIC_PATH", "./GroupDocs.Watermark.lic")

    # Apply the license before using any watermarking features
    if os.path.exists(license_path):
        License().set_license(license_path)
        print("License set successfully.")
    else:
        print("License file not found. Running in evaluation mode.")

if __name__ == "__main__":
    set_license_from_file()
```
{{< /tab >}}
{{< /tabs >}}

### Set a license from a stream

You can also apply a license from any readable binary stream — useful when the license ships as an embedded resource:

{{< tabs "code-example-set-license-from-stream" >}}
{{< tab "set_license_from_stream.py" >}}
```python
import os
from groupdocs.watermark import License

def set_license_from_stream():
    # Resolve the license path from the environment, with a local fallback
    license_path = os.environ.get("GROUPDOCS_LIC_PATH", "./GroupDocs.Watermark.lic")

    # Apply the license from an open binary stream
    if os.path.exists(license_path):
        with open(license_path, "rb") as stream:
            License().set_license(stream)
        print("License set successfully.")
    else:
        print("License file not found. Running in evaluation mode.")

if __name__ == "__main__":
    set_license_from_stream()
```
{{< /tab >}}
{{< /tabs >}}

### Set a metered license

A Metered License lets you pay for what you use. Set the public and private keys with [set_metered_key](https://reference.groupdocs.com/watermark/python-net/) before using the API:

{{< tabs "code-example-set-metered-license" >}}
{{< tab "set_metered_license.py" >}}
```python
from groupdocs.watermark import Metered

def set_metered_license():
    # Replace these placeholders with your real metered public/private keys
    public_key = "*****"
    private_key = "*****"

    # Skip the call until real keys are supplied (placeholder keys are rejected)
    if "*" in public_key or "*" in private_key:
        print("Provide real metered keys to enable metered licensing.")
        return

    # Apply the metered keys before using any watermarking features
    Metered().set_metered_key(public_key, private_key)
    print("Metered license set successfully.")

if __name__ == "__main__":
    set_metered_license()
```
{{< /tab >}}
{{< /tabs >}}

### Changing the license file name

You are not required to keep the license file name as `GroupDocs.Watermark.lic`. You can rename it to any preferred name and use that name when applying the license in your application.

### "Cannot find license filename" exception

When you download the license from the GroupDocs website it is saved as `GroupDocs.Watermark.lic`. However, some web browsers may automatically append `.xml`, resulting in `GroupDocs.Watermark.lic.xml`.

If your Windows settings are configured to hide file extensions (the default), the file may still appear as `GroupDocs.Watermark.lic` in File Explorer even though the actual name is `GroupDocs.Watermark.lic.xml`. This discrepancy can cause `set_license` to throw an exception. To fix it, manually rename the file to remove the `.xml` extension, or disable "Hide extensions for known file types" in Windows.

## How to evaluate GroupDocs.Watermark

You can evaluate GroupDocs.Watermark for Python via .NET without purchasing a license by using one of the following options.

### Free Trial

The evaluation version is identical to the purchased one; it becomes fully licensed once you set a license. Without a license the Free Trial gives you access to the API's features, but with some limitations:

- A maximum of **10 documents** can be loaded per application run.
- Only **one watermark** can be added to a document per editing session.
- The output document carries an **evaluation watermark** stamp.

### Temporary License

To experience the complete features of GroupDocs.Watermark without the limitations of the Free Trial, you can request a 30-day ["Temporary License"](https://purchase.groupdocs.com/temporary-license).
