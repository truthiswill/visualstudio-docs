---
title: "CA2001: Avoid calling problematic methods"
ms.date: 11/04/2016
ms.topic: reference
f1_keywords:
  - "CA2001"
  - "AvoidCallingProblematicMethods"
helpviewer_keywords:
  - "CA2001"
  - "AvoidCallingProblematicMethods"
ms.assetid: 19db8edb-31ce-441c-b0de-a0f2746155b7
author: gewarren
ms.author: gewarren
manager: jillfra
ms.workload:
  - "multiple"
---
# CA2001: Avoid calling problematic methods

|||
|-|-|
|TypeName|AvoidCallingProblematicMethods|
|CheckId|CA2001|
|Category|Microsoft.Reliability|
|Breaking change|Non-breaking|

## Cause

A member calls a potentially dangerous or problematic method.

## Rule description

Avoid making unnecessary and potentially dangerous method calls. A violation of this rule occurs when a member calls one of the following methods:

|Method|Description|
|------------|-----------------|
|<xref:System.GC.Collect%2A?displayProperty=fullName>|Calling GC.Collect can significantly affect application performance and is rarely necessary. For more information, see [Rico Mariani's Performance Tidbits](http://go.microsoft.com/fwlink/?LinkId=169256) blog entry on MSDN.|
|<xref:System.Threading.Thread.Resume%2A?displayProperty=fullName><br /><br /> <xref:System.Threading.Thread.Suspend%2A?displayProperty=fullName>|Thread.Suspend and Thread.Resume have been deprecated because of their unpredictable behavior.  Use other classes in the <xref:System.Threading> namespace, such as <xref:System.Threading.Monitor>, <xref:System.Threading.Mutex>, and <xref:System.Threading.Semaphore>, to synchronize threads or protect resources.|
|<xref:System.Runtime.InteropServices.SafeHandle.DangerousGetHandle%2A?displayProperty=fullName>|The DangerousGetHandle method poses a security risk because it can return a handle that is not valid. See the <xref:System.Runtime.InteropServices.SafeHandle.DangerousAddRef%2A> and the <xref:System.Runtime.InteropServices.SafeHandle.DangerousRelease%2A> methods for more information about how to use the DangerousGetHandle method safely.|
|<xref:System.Reflection.Assembly.LoadFrom%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadFile%2A?displayProperty=fullName><br /><br /> <xref:System.Reflection.Assembly.LoadWithPartialName%2A?displayProperty=fullName>|These methods can load assemblies from unexpected locations. For example, see Suzanne Cook's .NET CLR Notes blog posts [LoadFile vs. LoadFrom](http://go.microsoft.com/fwlink/?LinkId=164450) and [Choosing a Binding Context](http://go.microsoft.com/fwlink/?LinkId=164451) for information about methods that load assemblies.|
|[CoSetProxyBlanket](http://go.microsoft.com/fwlink/?LinkID=169250) (Ole32)<br /><br /> [CoInitializeSecurity](http://go.microsoft.com/fwlink/?LinkId=169255) (Ole32)|By the time the user code starts executing in a managed process, it is too late to reliably call CoSetProxyBlanket. The common language runtime (CLR) takes initialization actions that may prevent the users P/Invoke from succeeding.<br /><br /> If you do have to call CoSetProxyBlanket for a managed application, we recommend that you start the process by using a native code (C++) executable, call CoSetProxyBlanket in the native code, and then start your managed code application in process. (Be sure to specify a runtime version number.)|

## How to fix violations

To fix a violation of this rule, remove or replace the call to the dangerous or problematic method.

## When to suppress warnings

You should suppress messages from this rule only when no alternatives to the problematic method are available.

## See also

- [Reliability Warnings](../code-quality/reliability-warnings.md)