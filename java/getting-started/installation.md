---
id: installation
url: watermark/java/installation
title: Installation
weight: 5
description: ""
keywords:
productName: GroupDocs.Watermark for Java
hideChildren: False
---
GroupDocs hosts all Java APIs on [GroupDocs Repository](https://releases.groupdocs.com/java/repo/). You can easily use [GroupDocs.Watermark for Java](https://releases.groupdocs.com/java/repo/com/groupdocs/groupdocs-watermark/) API directly in your Maven projects with simple configurations.

### Specify GroupDocs Repository Configuration

First, you need to specify GroupDocs repository configuration/location in your Maven `pom.xml` as follows: 

```java
<repositories>
	<repository>
		<id>GroupDocsJavaAPI</id>
		<name>GroupDocs Java API</name>
		<url>https://releases.groupdocs.com/java/repo/</url>
	</repository>
</repositories>
```

### Define GroupDocs.Watermark for Java API Dependency

Then define GroupDocs.Watermark for Java API dependency in your `pom.xml` as follows:

```java
<dependencies>
    <dependency>
        <groupId>com.groupdocs</groupId>
        <artifactId>groupdocs-watermark</artifactId>
        <version>20.4</version>
    </dependency>
</dependencies>
```

After performing above-mentioned steps, GroupDocs.Watermark for Java dependency will finally be added to your Maven project.

## Install from official GroupDocs website

You can follow the steps below to reference GroupDocs.Watermark for Java downloaded from official website [Downloads section](https://downloads.groupdocs.com/watermark/java):

1.  Unpack zip archive .
2.  Switch to **lib** folder.
3.  Run **install.bat** (for Windows) or **install.sh** (for Linux) file to install the library in your local maven repository.
4.  After this you should add the GroupDocs.Watermark for Java watermark **dependency** block to your .pom.xml project file.
