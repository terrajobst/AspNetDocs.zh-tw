---
uid: webhooks/receiving/dependencies
title: ASP.NET Webhook 接收器相依性 |Microsoft Docs
author: rick-anderson
description: ASP.NET Webhook 中的接收者相依性和相依性插入。
ms.author: riande
ms.date: 01/17/2012
ms.assetid: 5125e483-c2bb-435b-8cd1-21d3499bfaaf
ms.openlocfilehash: 477b8828209d0da1d485ef883b0f99b4e1b9b5bf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637281"
---
# <a name="aspnet-webhooks-receiver-dependencies"></a><span data-ttu-id="c528f-103">ASP.NET Webhook 接收器相依性</span><span class="sxs-lookup"><span data-stu-id="c528f-103">ASP.NET WebHooks receiver dependencies</span></span>

<span data-ttu-id="c528f-104">Microsoft ASP.NET Webhook 的設計是要記住相依性插入。</span><span class="sxs-lookup"><span data-stu-id="c528f-104">Microsoft ASP.NET WebHooks is designed with dependency injection in mind.</span></span> <span data-ttu-id="c528f-105">系統中大部分的相依性都可以使用相依性插入引擎取代為替代的執行方式。</span><span class="sxs-lookup"><span data-stu-id="c528f-105">Most dependencies in the system can be replaced with alternative implementations using a dependency injection engine.</span></span>

<span data-ttu-id="c528f-106">如需接收者相依性的清單，請參閱[DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) 。</span><span class="sxs-lookup"><span data-stu-id="c528f-106">See [DependencyScopeExtensions](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Extensions/DependencyScopeExtensions.cs) for a list of receiver dependencies.</span></span> <span data-ttu-id="c528f-107">如果未註冊任何相依性，則會使用預設的實作為。</span><span class="sxs-lookup"><span data-stu-id="c528f-107">If no dependency has been registered, a default implementation is used.</span></span> <span data-ttu-id="c528f-108">如需預設實值的清單，請參閱[ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) 。</span><span class="sxs-lookup"><span data-stu-id="c528f-108">See [ReceiverServices](https://github.com/aspnet/aspnetWebHooks/blob/master/src/Microsoft.AspNet.WebHooks.Receivers/Services/ReceiverServices.cs) for a list of default implementations.</span></span>
