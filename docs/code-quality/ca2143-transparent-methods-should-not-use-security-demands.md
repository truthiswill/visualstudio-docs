---
title: "CA2143: Transparent methods should not use security demands"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA2143"
ms.assetid: 5d3923d7-cf40-4512-bc5c-0db0e0d6e25a
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA2143: Transparent methods should not use security demands

|||
|-|-|
|TypeName|TransparentMethodsShouldNotDemand|
|CheckId|CA2143|
|Category|Microsoft.Security|
|Breaking change|Breaking|

## Cause
A tranparent type or method is declaratively marked with a <xref:System.Security.Permissions.SecurityAction?displayProperty=fullName>`.Demand` demand or the method calls the <xref:System.Security.CodeAccessPermission.Demand%2A?displayProperty=fullName> method.

## Rule description
Security transparent code should not be responsible for verifying the security of an operation, and therefore should not demand permissions. Security transparent code should use full demands to make security decisions and safe-critical code should not rely on transparent code to have made the full demand. Any code that performs security checks, such as security demands, should be safe-critical instead.

## How to fix violations
In general, to fix a violation of this rule, mark the method with the <xref:System.Security.SecuritySafeCriticalAttribute> attribute. You can also remove the demand.

## When to suppress warnings
Do not suppress a warning from this rule.

## Example
The rule files on the following code because a transparent method makes a declarative security demand.

[!code-csharp[FxCop.Security.CA2143.TransparentMethodsShouldNotDemand#1](../code-quality/codesnippet/CSharp/ca2143-transparent-methods-should-not-use-security-demands_1.cs)]

## See also
[CA2142: Transparent code should not be protected with LinkDemands](../code-quality/ca2142-transparent-code-should-not-be-protected-with-linkdemands.md)