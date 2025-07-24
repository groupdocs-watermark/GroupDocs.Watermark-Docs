---
id: installation
url: watermark/net/installation
title: Installation
weight: 4
description: ""
keywords: 
productName: GroupDocs.Watermark for .NET
hideChildren: True
toc: true
---


This guide helps you quickly install GroupDocs.Watermark for .NET, a powerful library to add, edit, or remove watermarks from PDF, Word, Excel, PowerPoint, Visio, and image formats. Choose your preferred method below.

### Install via NuGet (Recommended)

Follow these steps to reference GroupDocs.Watermark using Package Manager GUI:

* Open your solution/project in Visual Studio.
* Click **Tools** -> **NuGet Package Manager** -> **Manage NuGet Packages for Solution**. You can also access the same option through the Solution Explorer. Right-click the solution or project and select **Manage NuGet Packages** from the context menu
* Select **Browse** tab and type "GroupDocs.Watermark" in the search text box.
* Click the **Install** button to install the latest version of the API into your project as shown in the following screenshot.

![installation](/watermark/net/images/installation.png)

### Using the package manager console

You can follow the steps below to reference GroupDocs.Watermark using the Package Manager Console:

* Open your solution/project in Visual Studio.
* Select **Tools** -> **NuGet Package Manager** -> **Package Manager Console** from the menu to open the package manager console.
* Type the command "Install-Package GroupDocs.Watermark" and press enter to install the latest release into your application.
* After successful installation, GroupDocs.Watermark will be referenced in your application.

![installation_1](/watermark/net/images/installation_1.png)

## Install from the official GroupDocs website

You can follow the steps below to reference GroupDocs.Watermark for .NET downloaded from official website [Downloads section](https://downloads.groupdocs.com/watermark/net):

1. Unpack the ZIP archive or follow MSI install wizard instructions.
2. In the Solution Explorer, expand the project node you want to add a reference to.
3. Right-click the **References** node for the project and select **Add Reference** from the menu.
4. In the Add Reference dialog box, select the **.NET** tab (it's usually selected by default).
5. If you have used the MSI installer to install GroupDocs.Watermark, you will see GroupDocs.Watermark in the top pane. Select it and then click the **Select** button.
6. If you have downloaded and unpacked the DLL only, click the **Browse** button and locate the GroupDocs.Watermark.dll file. You have referenced GroupDocs.Watermark and it should appear in the **Selected Components** pane of the dialog box.
7. Click **OK**.
8. GroupDocs.Watermark reference appears under the **References** node of the project.

Note that .NET Standard 2.0 version has external references:

| Package | Version |
| --- | --- |
| System.Drawing.Common | 5.0.3 |
| System.Text.Encoding.CodePages | 7.0.0 |
| SkiaSharp | 3.119.0 |
