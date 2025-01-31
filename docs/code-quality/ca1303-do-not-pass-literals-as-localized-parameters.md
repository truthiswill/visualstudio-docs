---
title: "CA1303: Do not pass literals as localized parameters"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "Do not pass literals as localized parameters"
  - "DoNotPassLiteralsAsLocalizedParameters"
  - "CA1303"
helpviewer_keywords:
  - "DoNotPassLiteralsAsLocalizedParameters"
  - "CA1303"
ms.assetid: 904d284e-76d0-4b8f-a4df-0094de8d7aac
author: gewarren
ms.author: gewarren
manager: jillfra
dev_langs:
 - CPP
 - CSharp
 - VB
ms.workload:
  - "multiple"
---
# CA1303: Do not pass literals as localized parameters

|||
|-|-|
|TypeName|DoNotPassLiteralsAsLocalizedParameters|
|CheckId|CA1303|
|Category|Microsoft.Globalization|
|Breaking change|Non-breaking|

## Cause

A method passes a string literal as a parameter to a .NET constructor or method and that string should be localizable.

This warning is raised when a literal string is passed as a value to a parameter or property and one or more of the following cases is true:

- The <xref:System.ComponentModel.LocalizableAttribute> attribute of the parameter or property is set to true.

- The parameter or property name contains "Text", "Message", or "Caption".

- The name of the string parameter that is passed to a Console.Write or Console.WriteLine method is either "value" or "format".

## Rule description

String literals that are embedded in source code are difficult to localize.

## How to fix violations

To fix a violation of this rule, replace the string literal with a string retrieved through an instance of the <xref:System.Resources.ResourceManager> class.

## When to suppress warnings

It is safe to suppress a warning from this rule if the code library will not be localized or if the string is not exposed to the end user or a developer using the code library.

Users can eliminate noise against methods that should not be passed localized strings by either renaming the parameter or property, or by marking these items as conditional.

## Example

The following example shows a method that throws an exception when either of its two arguments are out of range. For the first argument, the exception constructor is passed a literal string, which violates this rule. For the second argument, the constructor is correctly passed a string retrieved through a <xref:System.Resources.ResourceManager>.

[!code-cpp[FxCop.Globalization.DoNotPassLiterals#1](../code-quality/codesnippet/CPP/ca1303-do-not-pass-literals-as-localized-parameters_1.cpp)]
[!code-vb[FxCop.Globalization.DoNotPassLiterals#1](../code-quality/codesnippet/VisualBasic/ca1303-do-not-pass-literals-as-localized-parameters_1.vb)]
[!code-csharp[FxCop.Globalization.DoNotPassLiterals#1](../code-quality/codesnippet/CSharp/ca1303-do-not-pass-literals-as-localized-parameters_1.cs)]

## See also

- [Resources in desktop apps](/dotnet/framework/resources/index)