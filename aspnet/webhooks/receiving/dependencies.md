---
uid: webhooks/receiving/dependencies
title: ASP.NET Webhook 接收器相依性 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 中的接收者相依性和相依性插入。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: 6f0e10e4ca61a1e5534b09c655fd35cdc6886c8a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/27/2019
ms.locfileid: "74564863"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a>ASP.NET Webhook 接收器相依性

Microsoft ASP.NET Webhook 的設計是要記住相依性插入。 系統中大部分的相依性都可以使用相依性插入引擎取代為替代的執行方式。

如需接收者相依性的清單，請參閱[DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 。 如果未註冊任何相依性，則會使用預設的實作為。 如需預設實值的清單，請參閱[ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 。
