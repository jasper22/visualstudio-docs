---
title: "Test Explorer FAQ | Microsoft Docs"
ms.date: "1/15/2018"
ms.reviewer: ""
ms.suite: ""
ms.technology: vs-devops-test
ms.tgt_pltfrm: ""
ms.topic: "article"
helpviewer_keywords: 
  - "Test Explorer"
  - "Test window"
  - "Visual Studio Test Explorer"
  - "summary line"
  - "unit tests"
  - "Test Explorer FAQ"
ms.author: "kehavens"
ms.workload: 
  - "multiple"
author: "kendrahavens"
manager: ghogen
---
# Visual Studio Test Explorer FAQ

## Test Discovery

### 1. The Test Explorer is not discovering my tests that have theories, custom adapters, custom traits, use #ifdefs, or are dynamically defined. How can I discover these tests?

  Build your project and make sure assembly-based discovery is turned on in **Tools > Options > Test**.

  [Real Time Test Discovery](https://go.microsoft.com/fwlink/?linkid=862824), which is source-based test discovery, can’t discover tests that use theories, custom adapters, custom traits, `#ifdef` statements, or that are dynamically defined in some other way. A build is required for those tests to be accurately discovered. In the 15.6 Previews, assembly-based discovery (the traditional discoverer) runs only after builds. This means Real Time Test Discovery discovers as many tests as it can while you are editing, and assembly-based discovery allows theories (or any dynamically defined tests) to appear after a build. Real Time Test Discovery improves responsiveness, but stills allow you to get complete and accurate results after a build.

### 2. What does the '+' (plus) symbol that appears in the top line of Test Explorer mean?

  The '+' (plus) symbol indicates that more tests may be discovered after a build if assembly-based discovery is turned on. It will appear if dynamically defined tests are detected in your project.

  ![Plus symbol summary line](media/testex-plussymbol.png)

### 3. Assembly-based discovery is no longer working for my project. How do I turn it back on?

  Go to **Tools > Options > Test** and check the box for **Additionally discover tests built from assemblies after builds.**

  ![Assembly-based option](media/testex-toolsoptions.png)

### 4. Tests now appear in Test Explorer while I type, without having to build my project. What changed?

  This feature is called [Real Time Test Discovery](https://go.microsoft.com/fwlink/?linkid=862824). It uses a .NET Complier Platform ("Roslyn") analyzer to discover tests and populate Test Explorer in real time, without requiring you to build your project. See FAQ #1 for more information about test discovery behavior for dynamically defined tests such as theories or custom traits.

### 5. What languages and test frameworks can use Real Time Test Discovery?

  [Real Time Test Discovery](https://go.microsoft.com/fwlink/?linkid=862824) only works for the managed languages (C# and Visual Basic), since it is built using the .NET ("Roslyn") compiler. For now, Real Time Test Discovery only works for the xUnit, NUnit, and MSTest frameworks.

## Features

### How can I turn on feature flags to try out new testing features?

Feature flags are used to ship experimental or unfinished parts of the product to avid users who would like to give feedback before the features ship officially. They may destabilize your IDE experience. It is recommended to use them only in safe development environments, such as virtual machines. Feature flags are always use-at-your-own-risk settings. You can turn on experimental features with the [Feature Flags extension](https://marketplace.visualstudio.com/items?itemName=PaulHarrington.FeatureFlagsExtension), or through the developer command prompt.

![Feature Flag Extension](media/testex-featureflag.png)

To turn on a feature flag through the Visual Studio developer command prompt, use the following command. Change the path to where Visual Studio is installed on your machine, and change the registry key to the desired feature flag.

```shell
vsregedit set “C:\Program Files (x86)\Microsoft Visual Studio\Preview\Enterprise” HKLM FeatureFlags\TestingTools\UnitTesting\HierarchyView Value dword 1
```

> [!NOTE]
> You can turn off the flag with the same command, by using a value of 0 instead of 1 after dword.
  
## See also

<xref:Microsoft.VisualStudio.TestTools.UnitTesting?displayProperty=fullName>  
[Creating and Running Unit Tests for Existing Code](http://msdn.microsoft.com/e8370b93-085b-41c9-8dec-655bd886f173)
[Unit Test Your Code](unit-test-your-code.md)
[Live Unit Testing FAQ](live-unit-testing-faq.md)
