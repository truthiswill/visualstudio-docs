---
title: "CA1053: Static holder types should not have constructors"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "StaticHolderTypesShouldNotHaveConstructors"
  - "CA1053"
helpviewer_keywords:
  - "CA1053"
  - "StaticHolderTypesShouldNotHaveConstructors"
ms.assetid: 10302b9a-fa5e-4935-a06a-513d9600f613
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA1053: Static holder types should not have default constructors

|||
|-|-|
|TypeName|StaticHolderTypesShouldNotHaveConstructors|
|CheckId|CA1053|
|Category|Microsoft.Design|
|Breaking change|Breaking|

> [!NOTE]
> Rule CA1053 is combined into [CA1052: Static holder types should be sealed](ca1052-static-holder-types-should-be-sealed.md) in [FxCop analyzers](fxcop-analyzers.yml).

## Cause

A public or nested public type declares only static members and has a default constructor.

## Rule description

The default constructor is unnecessary because calling static members does not require an instance of the type. Also, because the type does not have non-static members, creating an instance does not provide access to any of the type's members.

## How to fix violations

To fix a violation of this rule, remove the default constructor.

## When to suppress warnings

Do not suppress a warning from this rule. The presence of the default constructor suggests that the type is not a static type.