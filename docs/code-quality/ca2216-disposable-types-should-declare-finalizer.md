---
title: "CA2216: Disposable types should declare finalizer"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "DisposableTypesShouldDeclareFinalizer"
  - "CA2216"
helpviewer_keywords:
  - "CA2216"
  - "DisposableTypesShouldDeclareFinalizer"
ms.assetid: 0cabcc5e-b526-452b-8c2a-0cbe3b93c0ef
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA2216: Disposable types should declare finalizer

|||
|-|-|
|TypeName|DisposableTypesShouldDeclareFinalizer|
|CheckId|CA2216|
|Category|Microsoft.Usage|
|Breaking change|Non-breaking|

## Cause

A type that implements <xref:System.IDisposable?displayProperty=fullName>, and has fields that suggest the use of unmanaged resources, does not implement a finalizer as described by <xref:System.Object.Finalize%2A?displayProperty=fullName>.

## Rule description

A violation of this rule is reported if the disposable type contains fields of the following types:

- <xref:System.IntPtr?displayProperty=fullName>

- <xref:System.UIntPtr?displayProperty=fullName>

- <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName>

## How to fix violations

To fix a violation of this rule, implement a finalizer that calls your <xref:System.IDisposable.Dispose%2A> method.

## When to suppress warnings

It is safe to suppress a warning from this rule if the type does not implement <xref:System.IDisposable> for the purpose of releasing unmanaged resources.

## Example

The following example shows a type that violates this rule.

[!code-csharp[FxCop.Usage.DisposeNoFinalize#1](../code-quality/codesnippet/CSharp/ca2216-disposable-types-should-declare-finalizer_1.cs)]

## Related rules

[CA2115: Call GC.KeepAlive when using native resources](../code-quality/ca2115-call-gc-keepalive-when-using-native-resources.md)

[CA1816: Call GC.SuppressFinalize correctly](../code-quality/ca1816-call-gc-suppressfinalize-correctly.md)

[CA1049: Types that own native resources should be disposable](../code-quality/ca1049-types-that-own-native-resources-should-be-disposable.md)

## See also

- <xref:System.IDisposable?displayProperty=fullName>
- <xref:System.IntPtr?displayProperty=fullName>
- <xref:System.Runtime.InteropServices.HandleRef?displayProperty=fullName>
- <xref:System.UIntPtr?displayProperty=fullName>
- <xref:System.Object.Finalize%2A?displayProperty=fullName>
- [Dispose Pattern](/dotnet/standard/design-guidelines/dispose-pattern)