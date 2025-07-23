---
id: evaluation-limitations-and-licensing
url: watermark/nodejs-java/evaluation-limitations-and-licensing
title: Licensing
weight: 5
description: "Follow the instructions on this page to configure the license and find out the restrictions when using GroupDocs.Watermark for Node.js via Java without a license (Evaluation Limitations)"
keywords: Licensing, evaluation limitations, set metered license, setting license
productName: GroupDocs.Watermark for Node.js via Java
hideChildren: False
toc: True
structuredData:
  showOrganization: True
  application:
    name: Document Watermark
    description: Adding watermarks with high performance using JavaScript language and GroupDocs.Watermark for Node.js via Java
    productCode: watermark
    productPlatform: nodejs-java
  showVideo: True
  howTo:
    name: How to Setting License in JavaScript
    description: Learn how to Setting License in JavaScript step by step
    steps:
      - name: Create an object
        text: Create an object of license class.
      - name: Set license
        text: Call the setLicense method of your object and put the license path or license file stream parameter.
---

Sometimes, to study the system better, you want to dive into the code as fast as possible. To make this easier, GroupDocs.Watermark provides different purchase plans or offers a Free Trial and a 30-day Temporary License for evaluation.

{{< alert style="info" >}}
Note that there are several general policies and practices that guide you on how to evaluate, properly license, and purchase our products. You can find them in the ["Purchase Policies and FAQ"](https://purchase.groupdocs.com/policies) section.
{{< /alert >}}

## Free Trial or Temporary License

You can try GroupDocs.Watermark without buying a license.

### Free Trial

The evaluation version is the same as the purchased one – the evaluation version simply becomes licensed when you set the license. You can set the license in several ways that are described in the next sections of this article.

The evaluation version comes with the following limitations:

- Only the first 2 pages can be processed.
- Trial badges are placed in the document on the top of each page.

### Temporary License

If you wish to test GroupDocs.Watermark without the limitations of the trial version, you can also request a 30-day Temporary License. For details, see the ["Get a Temporary License"](https://purchase.groupdocs.com/temporary-license) page.

## How to set up a license

{{< alert style="info" >}}

You can find the pricing information on the ["Pricing Information"](https://purchase.groupdocs.com/pricing/watermark/nodejs-java) page.

{{< /alert >}}

After getting the license, you need to set it. This section describes different ways to set the license.

The license should be set:

- Only once per application domain.
- Before using any other GroupDocs.Watermark classes.

{{< alert style="info" >}}

The license can be set multiple times per application domain, but we recommend doing it once since all the subsequent calls to the `setLicense` method except for the first one will just waste processor time.

{{< /alert >}}

### Set License from File

The following code snippet shows how to set a license from a file:

```javascript
const licensePath = "path to the .lic file";
const license = new groupdocs.watermark.License()
await license.setLicense(licensePath); 
```

### Set License from Stream

The following code snippet shows how to set a license from a stream:

```javascript
const java = require('java');
let InputStream = java.import('java.io.FileInputStream');

const licensePath = "path to the .lic file"
try {
  const stream = new InputStream(licensePath)

  const license = new groupdocs.watermark.License()
  await license.setLicense(stream);
  console.log('License set successfully.');
} catch {
  console.log("\nWe do not ship any license with this example. " +
    "\nVisit the GroupDocs site to obtain either a temporary or permanent license. " +
    "\nLearn more about licensing at https://purchase.groupdocs.com/faqs/licensing. " +
    "\nLearn how to request a temporary license at https://purchase.groupdocs.com/temporary-license.");
}
```