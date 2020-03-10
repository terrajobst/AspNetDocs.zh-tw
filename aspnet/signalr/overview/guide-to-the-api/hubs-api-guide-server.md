---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-server
title: ASP.NET SignalR 中樞 API 指南-伺服器（C#） |Microsoft Docs
author: bradygaster
description: 本檔介紹如何程式設計 SignalR 第2版 ASP.NET SignalR Hub API 的伺服器端，並提供程式碼範例來示範 。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: b19913e5-cd8a-4e4b-a872-5ac7a858a934
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-server
msc.type: authoredcontent
ms.openlocfilehash: c681b104b15bfc4a04587c7abf685dcf20def2ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536747"
---
# <a name="aspnet-signalr-hubs-api-guide---server-c"></a><span data-ttu-id="5692e-103">ASP.NET SignalR 中樞 API 指南-伺服器（C#）</span><span class="sxs-lookup"><span data-stu-id="5692e-103">ASP.NET SignalR Hubs API Guide - Server (C#)</span></span>

<span data-ttu-id="5692e-104">由一[Fletcher](https://github.com/pfletcher)， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="5692e-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="5692e-105">本檔介紹如何程式設計 SignalR 第2版 ASP.NET SignalR Hub API 的伺服器端，並提供示範常用選項的程式碼範例。</span><span class="sxs-lookup"><span data-stu-id="5692e-105">This document provides an introduction to programming the server side of the ASP.NET SignalR Hubs API for SignalR version 2, with code samples demonstrating common options.</span></span>
> 
> <span data-ttu-id="5692e-106">SignalR 中樞 API 可讓您從伺服器對連線的用戶端，以及從用戶端到伺服器進行遠端程序呼叫（Rpc）。</span><span class="sxs-lookup"><span data-stu-id="5692e-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="5692e-107">在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="5692e-108">在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="5692e-109">SignalR 會為您處理所有的用戶端對伺服器管道。</span><span class="sxs-lookup"><span data-stu-id="5692e-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="5692e-110">SignalR 也提供名為「持續連線」的較低層級 API。</span><span class="sxs-lookup"><span data-stu-id="5692e-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="5692e-111">如需 SignalR、中樞和持續連線的簡介，請參閱[SignalR 2 簡介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="5692e-111">For an introduction to SignalR, Hubs, and Persistent Connections, see [Introduction to SignalR 2](../getting-started/introduction-to-signalr.md).</span></span>
> 
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="5692e-112">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="5692e-112">Software versions used in this topic</span></span>
> 
> 
> - [<span data-ttu-id="5692e-113">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="5692e-113">Visual Studio 2013</span></span>](https://www.microsoft.com/visualstudio/eng/2013-downloads)
> - <span data-ttu-id="5692e-114">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="5692e-114">.NET 4.5</span></span>
> - <span data-ttu-id="5692e-115">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="5692e-115">SignalR version 2</span></span>
>   
> 
> 
> ## <a name="topic-versions"></a><span data-ttu-id="5692e-116">主題版本</span><span class="sxs-lookup"><span data-stu-id="5692e-116">Topic versions</span></span>
> 
> <span data-ttu-id="5692e-117">如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="5692e-117">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="5692e-118">問題與意見</span><span class="sxs-lookup"><span data-stu-id="5692e-118">Questions and comments</span></span>
> 
> <span data-ttu-id="5692e-119">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="5692e-119">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="5692e-120">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="5692e-120">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="5692e-121">概觀</span><span class="sxs-lookup"><span data-stu-id="5692e-121">Overview</span></span>

<span data-ttu-id="5692e-122">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="5692e-122">This document contains the following sections:</span></span>

- [<span data-ttu-id="5692e-123">如何註冊 SignalR 中介軟體</span><span class="sxs-lookup"><span data-stu-id="5692e-123">How to register SignalR middleware</span></span>](#route)

    - [<span data-ttu-id="5692e-124">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="5692e-124">The /signalr URL</span></span>](#signalrurl)
    - [<span data-ttu-id="5692e-125">設定 SignalR 選項</span><span class="sxs-lookup"><span data-stu-id="5692e-125">Configuring SignalR options</span></span>](#options)
- [<span data-ttu-id="5692e-126">如何建立和使用中樞類別</span><span class="sxs-lookup"><span data-stu-id="5692e-126">How to create and use Hub classes</span></span>](#hubclass)

    - [<span data-ttu-id="5692e-127">中樞物件存留期</span><span class="sxs-lookup"><span data-stu-id="5692e-127">Hub object lifetime</span></span>](#transience)
    - [<span data-ttu-id="5692e-128">Camel-JavaScript 用戶端中中樞名稱的大小寫</span><span class="sxs-lookup"><span data-stu-id="5692e-128">Camel-casing of Hub names in JavaScript clients</span></span>](#hubnames)
    - [<span data-ttu-id="5692e-129">多個中樞</span><span class="sxs-lookup"><span data-stu-id="5692e-129">Multiple Hubs</span></span>](#multiplehubs)
    - [<span data-ttu-id="5692e-130">強型別中樞</span><span class="sxs-lookup"><span data-stu-id="5692e-130">Strongly-Typed Hubs</span></span>](#stronglytypedhubs)
- [<span data-ttu-id="5692e-131">如何在中樞類別中定義用戶端可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="5692e-131">How to define methods in the Hub class that clients can call</span></span>](#hubmethods)

    - [<span data-ttu-id="5692e-132">Camel-JavaScript 用戶端中方法名稱的大小寫</span><span class="sxs-lookup"><span data-stu-id="5692e-132">Camel-casing of method names in JavaScript clients</span></span>](#methodnames)
    - [<span data-ttu-id="5692e-133">非同步執行的時機</span><span class="sxs-lookup"><span data-stu-id="5692e-133">When to execute asynchronously</span></span>](#asyncmethods)
    - [<span data-ttu-id="5692e-134">定義多載</span><span class="sxs-lookup"><span data-stu-id="5692e-134">Defining overloads</span></span>](#overloads)
    - [<span data-ttu-id="5692e-135">從中樞方法調用報告進度</span><span class="sxs-lookup"><span data-stu-id="5692e-135">Reporting progress from hub method invocations</span></span>](#progress)
- [<span data-ttu-id="5692e-136">如何從中樞類別呼叫用戶端方法</span><span class="sxs-lookup"><span data-stu-id="5692e-136">How to call client methods from the Hub class</span></span>](#callfromhub)

    - [<span data-ttu-id="5692e-137">選取將接收 RPC 的用戶端</span><span class="sxs-lookup"><span data-stu-id="5692e-137">Selecting which clients will receive the RPC</span></span>](#selectingclients)
    - [<span data-ttu-id="5692e-138">方法名稱沒有編譯時間驗證</span><span class="sxs-lookup"><span data-stu-id="5692e-138">No compile-time validation for method names</span></span>](#dynamicmethodnames)
    - [<span data-ttu-id="5692e-139">不區分大小寫的方法名稱比對</span><span class="sxs-lookup"><span data-stu-id="5692e-139">Case-insensitive method name matching</span></span>](#caseinsensitive)
    - [<span data-ttu-id="5692e-140">非同步執行</span><span class="sxs-lookup"><span data-stu-id="5692e-140">Asynchronous execution</span></span>](#asyncclient)
- [<span data-ttu-id="5692e-141">如何從中樞類別管理群組成員資格</span><span class="sxs-lookup"><span data-stu-id="5692e-141">How to manage group membership from the Hub class</span></span>](#groupsfromhub)

    - [<span data-ttu-id="5692e-142">非同步執行 Add 和 Remove 方法</span><span class="sxs-lookup"><span data-stu-id="5692e-142">Asynchronous execution of Add and Remove methods</span></span>](#asyncgroupmethods)
    - [<span data-ttu-id="5692e-143">群組成員資格持續性</span><span class="sxs-lookup"><span data-stu-id="5692e-143">Group membership persistence</span></span>](#grouppersistence)
    - [<span data-ttu-id="5692e-144">單一使用者群組</span><span class="sxs-lookup"><span data-stu-id="5692e-144">Single-user groups</span></span>](#singleusergroups)
- [<span data-ttu-id="5692e-145">如何處理中樞類別中的連接存留期事件</span><span class="sxs-lookup"><span data-stu-id="5692e-145">How to handle connection lifetime events in the Hub class</span></span>](#connectionlifetime)

    - [<span data-ttu-id="5692e-146">呼叫 OnConnected、OnDisconnected 和 OnReconnected 時</span><span class="sxs-lookup"><span data-stu-id="5692e-146">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>](#onreconnected)
    - [<span data-ttu-id="5692e-147">未填入呼叫者狀態</span><span class="sxs-lookup"><span data-stu-id="5692e-147">Caller state not populated</span></span>](#nocallerstate)
- [<span data-ttu-id="5692e-148">如何從內容屬性取得用戶端的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5692e-148">How to get information about the client from the Context property</span></span>](#contextproperty)
- [<span data-ttu-id="5692e-149">如何在用戶端與中樞類別之間傳遞狀態</span><span class="sxs-lookup"><span data-stu-id="5692e-149">How to pass state between clients and the Hub class</span></span>](#passstate)
- [<span data-ttu-id="5692e-150">如何處理中樞類別中的錯誤</span><span class="sxs-lookup"><span data-stu-id="5692e-150">How to handle errors in the Hub class</span></span>](#handleErrors)
- [<span data-ttu-id="5692e-151">如何從中樞類別外部呼叫用戶端方法和管理群組</span><span class="sxs-lookup"><span data-stu-id="5692e-151">How to call client methods and manage groups from outside the Hub class</span></span>](#callfromoutsidehub)

    - [<span data-ttu-id="5692e-152">呼叫用戶端方法</span><span class="sxs-lookup"><span data-stu-id="5692e-152">Calling client methods</span></span>](#callingclientsoutsidehub)
    - [<span data-ttu-id="5692e-153">管理群組成員資格</span><span class="sxs-lookup"><span data-stu-id="5692e-153">Managing group membership</span></span>](#managinggroupsoutsidehub)
- [<span data-ttu-id="5692e-154">如何啟用追蹤</span><span class="sxs-lookup"><span data-stu-id="5692e-154">How to enable tracing</span></span>](#tracing)
- [<span data-ttu-id="5692e-155">如何自訂中樞管線</span><span class="sxs-lookup"><span data-stu-id="5692e-155">How to customize the Hubs pipeline</span></span>](#hubpipeline)

<span data-ttu-id="5692e-156">如需如何編寫用戶端程式的相關檔，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="5692e-156">For documentation on how to program clients, see the following resources:</span></span>

- [<span data-ttu-id="5692e-157">SignalR 中樞 API 指南-JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="5692e-157">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)
- [<span data-ttu-id="5692e-158">SignalR 中樞 API 指南-.NET 用戶端</span><span class="sxs-lookup"><span data-stu-id="5692e-158">SignalR Hubs API Guide - .NET Client</span></span>](hubs-api-guide-net-client.md)

<span data-ttu-id="5692e-159">SignalR 2 的伺服器元件僅適用于 .NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="5692e-159">The server components for SignalR 2 are only available in .NET 4.5.</span></span> <span data-ttu-id="5692e-160">執行 .NET 4.0 的伺服器必須使用 SignalR v1. x。</span><span class="sxs-lookup"><span data-stu-id="5692e-160">Servers running .NET 4.0 must use SignalR v1.x.</span></span>

<a id="route"></a>

## <a name="how-to-register-signalr-middleware"></a><span data-ttu-id="5692e-161">如何註冊 SignalR 中介軟體</span><span class="sxs-lookup"><span data-stu-id="5692e-161">How to register SignalR middleware</span></span>

<span data-ttu-id="5692e-162">若要定義用戶端將用來連接到您中樞的路由，請在應用程式啟動時呼叫 `MapSignalR` 方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-162">To define the route that clients will use to connect to your Hub, call the `MapSignalR` method when the application starts.</span></span> <span data-ttu-id="5692e-163">`MapSignalR` 是 `OwinExtensions` 類別的[擴充方法](https://msdn.microsoft.com/library/vstudio/bb383977.aspx)。</span><span class="sxs-lookup"><span data-stu-id="5692e-163">`MapSignalR` is an [extension method](https://msdn.microsoft.com/library/vstudio/bb383977.aspx) for the `OwinExtensions` class.</span></span> <span data-ttu-id="5692e-164">下列範例顯示如何使用 OWIN 啟動類別來定義 SignalR 中樞路由。</span><span class="sxs-lookup"><span data-stu-id="5692e-164">The following example shows how to define the SignalR Hubs route using an OWIN startup class.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample1.cs)]

<span data-ttu-id="5692e-165">如果您要將 SignalR 功能新增至 ASP.NET MVC 應用程式，請確定已在其他路由之前新增 SignalR 路由。</span><span class="sxs-lookup"><span data-stu-id="5692e-165">If you are adding SignalR functionality to an ASP.NET MVC application, make sure that the SignalR route is added before the other routes.</span></span> <span data-ttu-id="5692e-166">如需詳細資訊，請參閱[教學課程：使用 SignalR 2 和 MVC 5 的消費者入門](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="5692e-166">For more information, see [Tutorial: Getting Started with SignalR 2 and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<a id="signalrurl"></a>

### <a name="the-signalr-url"></a><span data-ttu-id="5692e-167">/Signalr URL</span><span class="sxs-lookup"><span data-stu-id="5692e-167">The /signalr URL</span></span>

<span data-ttu-id="5692e-168">根據預設，用戶端將用來連線到您中樞的路由 URL 是 "/signalr"。</span><span class="sxs-lookup"><span data-stu-id="5692e-168">By default, the route URL which clients will use to connect to your Hub is "/signalr".</span></span> <span data-ttu-id="5692e-169">（請勿將此 URL 與 "/signalr/hubs" URL 混淆，這適用于自動產生的 JavaScript 檔案。</span><span class="sxs-lookup"><span data-stu-id="5692e-169">(Don't confuse this URL with the "/signalr/hubs" URL, which is for the automatically generated JavaScript file.</span></span> <span data-ttu-id="5692e-170">如需所產生之 proxy 的詳細資訊，請參閱[SignalR HUB API Guide-JavaScript Client-產生的 proxy 和它為您提供的功能](hubs-api-guide-javascript-client.md#genproxy)。）</span><span class="sxs-lookup"><span data-stu-id="5692e-170">For more information about the generated proxy, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).)</span></span>

<span data-ttu-id="5692e-171">在某些情況下，可能會導致此基底 URL 無法用於 SignalR;例如，您的專案中有一個名為*signalr*的資料夾，而且您不想要變更名稱。</span><span class="sxs-lookup"><span data-stu-id="5692e-171">There might be extraordinary circumstances that make this base URL not usable for SignalR; for example, you have a folder in your project named *signalr* and you don't want to change the name.</span></span> <span data-ttu-id="5692e-172">在此情況下，您可以變更基底 URL，如下列範例所示（使用您想要的 URL 取代範例程式碼中的 "/signalr"）。</span><span class="sxs-lookup"><span data-stu-id="5692e-172">In that case, you can change the base URL, as shown in the following examples (replace "/signalr" in the sample code with your desired URL).</span></span>

<span data-ttu-id="5692e-173">**指定 URL 的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="5692e-173">**Server code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample2.cs?highlight=1)]

<span data-ttu-id="5692e-174">**指定 URL 的 JavaScript 用戶端程式代碼（使用產生的 proxy）**</span><span class="sxs-lookup"><span data-stu-id="5692e-174">**JavaScript client code that specifies the URL (with the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample3.js?highlight=1)]

<span data-ttu-id="5692e-175">**指定 URL 的 JavaScript 用戶端程式代碼（不含產生的 proxy）**</span><span class="sxs-lookup"><span data-stu-id="5692e-175">**JavaScript client code that specifies the URL (without the generated proxy)**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample4.js?highlight=1)]

<span data-ttu-id="5692e-176">**指定 URL 的 .NET 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="5692e-176">**.NET client code that specifies the URL**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample5.cs?highlight=1)]

<a id="options"></a>

### <a name="configuring-signalr-options"></a><span data-ttu-id="5692e-177">設定 SignalR 選項</span><span class="sxs-lookup"><span data-stu-id="5692e-177">Configuring SignalR Options</span></span>

<span data-ttu-id="5692e-178">`MapSignalR` 方法的多載可讓您指定自訂 URL、自訂相依性解析程式，以及下列選項：</span><span class="sxs-lookup"><span data-stu-id="5692e-178">Overloads of the `MapSignalR` method enable you to specify a custom URL, a custom dependency resolver, and the following options:</span></span>

- <span data-ttu-id="5692e-179">使用來自瀏覽器用戶端的 CORS 或 JSONP 來啟用跨網域呼叫。</span><span class="sxs-lookup"><span data-stu-id="5692e-179">Enable cross-domain calls using CORS or JSONP from browser clients.</span></span>

    <span data-ttu-id="5692e-180">通常，如果瀏覽器從 `http://contoso.com`載入頁面，則 SignalR 連接會位於相同的網域中，`http://contoso.com/signalr`。</span><span class="sxs-lookup"><span data-stu-id="5692e-180">Typically if the browser loads a page from `http://contoso.com`, the SignalR connection is in the same domain, at `http://contoso.com/signalr`.</span></span> <span data-ttu-id="5692e-181">如果 `http://contoso.com` 的頁面建立與 `http://fabrikam.com/signalr`的連接，這就是跨網域的連線。</span><span class="sxs-lookup"><span data-stu-id="5692e-181">If the page from `http://contoso.com` makes a connection to `http://fabrikam.com/signalr`, that is a cross-domain connection.</span></span> <span data-ttu-id="5692e-182">基於安全考慮，預設會停用跨網域連線。</span><span class="sxs-lookup"><span data-stu-id="5692e-182">For security reasons, cross-domain connections are disabled by default.</span></span> <span data-ttu-id="5692e-183">如需詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-JavaScript 用戶端-如何建立跨網域](hubs-api-guide-javascript-client.md#crossdomain)連線。</span><span class="sxs-lookup"><span data-stu-id="5692e-183">For more information, see [ASP.NET SignalR Hubs API Guide - JavaScript Client - How to establish a cross-domain connection](hubs-api-guide-javascript-client.md#crossdomain).</span></span>
- <span data-ttu-id="5692e-184">啟用詳細的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="5692e-184">Enable detailed error messages.</span></span>

    <span data-ttu-id="5692e-185">發生錯誤時，SignalR 的預設行為是將通知訊息傳送給用戶端，而不會有發生什麼情況的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-185">When errors occur, the default behavior of SignalR is to send to clients a notification message without details about what happened.</span></span> <span data-ttu-id="5692e-186">不建議在生產環境中傳送詳細的錯誤資訊給用戶端，因為惡意使用者可能可以對您的應用程式使用這些資訊。</span><span class="sxs-lookup"><span data-stu-id="5692e-186">Sending detailed error information to clients is not recommended in production, because malicious users might be able to use the information in attacks against your application.</span></span> <span data-ttu-id="5692e-187">若要進行疑難排解，您可以使用此選項暫時啟用更具資訊性的錯誤報表。</span><span class="sxs-lookup"><span data-stu-id="5692e-187">For troubleshooting, you can use this option to temporarily enable more informative error reporting.</span></span>
- <span data-ttu-id="5692e-188">停用自動產生的 JavaScript proxy 檔案。</span><span class="sxs-lookup"><span data-stu-id="5692e-188">Disable automatically generated JavaScript proxy files.</span></span>

    <span data-ttu-id="5692e-189">根據預設，系統會產生一個 JavaScript 檔案，其中包含中樞類別的 proxy，以回應 URL "/signalr/hubs"。</span><span class="sxs-lookup"><span data-stu-id="5692e-189">By default, a JavaScript file with proxies for your Hub classes is generated in response to the URL "/signalr/hubs".</span></span> <span data-ttu-id="5692e-190">如果您不想要使用 JavaScript proxy，或如果您想要手動產生此檔案，並參考用戶端中的實體檔案，則可以使用此選項來停用 proxy 產生。</span><span class="sxs-lookup"><span data-stu-id="5692e-190">If you don't want to use the JavaScript proxies, or if you want to generate this file manually and refer to a physical file in your clients, you can use this option to disable proxy generation.</span></span> <span data-ttu-id="5692e-191">如需詳細資訊，請參閱[SignalR 中樞 API 指南-JavaScript 用戶端-如何為 SignalR 產生的 proxy 建立實體](hubs-api-guide-javascript-client.md#manualproxy)檔案。</span><span class="sxs-lookup"><span data-stu-id="5692e-191">For more information, see [SignalR Hubs API Guide - JavaScript Client - How to create a physical file for the SignalR generated proxy](hubs-api-guide-javascript-client.md#manualproxy).</span></span>

<span data-ttu-id="5692e-192">下列範例示範如何在 `MapSignalR` 方法的呼叫中指定 SignalR 連接 URL 和這些選項。</span><span class="sxs-lookup"><span data-stu-id="5692e-192">The following example shows how to specify the SignalR connection URL and these options in a call to the `MapSignalR` method.</span></span> <span data-ttu-id="5692e-193">若要指定自訂 URL，請將範例中的 "/signalr" 取代為您想要使用的 URL。</span><span class="sxs-lookup"><span data-stu-id="5692e-193">To specify a custom URL, replace "/signalr" in the example with the URL that you want to use.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample6.cs)]

<a id="hubclass"></a>

## <a name="how-to-create-and-use-hub-classes"></a><span data-ttu-id="5692e-194">如何建立和使用中樞類別</span><span class="sxs-lookup"><span data-stu-id="5692e-194">How to create and use Hub classes</span></span>

<span data-ttu-id="5692e-195">若要建立中樞，請建立一個衍生自[Signalr](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)的類別。</span><span class="sxs-lookup"><span data-stu-id="5692e-195">To create a Hub, create a class that derives from [Microsoft.Aspnet.Signalr.Hub](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx).</span></span> <span data-ttu-id="5692e-196">下列範例顯示聊天應用程式的簡單中樞類別。</span><span class="sxs-lookup"><span data-stu-id="5692e-196">The following example shows a simple Hub class for a chat application.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample7.cs)]

<span data-ttu-id="5692e-197">在此範例中，連線的用戶端可以呼叫 `NewContosoChatMessage` 方法，當它這麼做時，收到的資料會廣播到所有連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-197">In this example, a connected client can call the `NewContosoChatMessage` method, and when it does, the data received is broadcasted to all connected clients.</span></span>

<a id="transience"></a>

### <a name="hub-object-lifetime"></a><span data-ttu-id="5692e-198">中樞物件存留期</span><span class="sxs-lookup"><span data-stu-id="5692e-198">Hub object lifetime</span></span>

<span data-ttu-id="5692e-199">您不會在伺服器上具現化中樞類別，或從您自己的程式碼呼叫其方法。SignalR Hub 管線會為您完成這一切。</span><span class="sxs-lookup"><span data-stu-id="5692e-199">You don't instantiate the Hub class or call its methods from your own code on the server; all that is done for you by the SignalR Hubs pipeline.</span></span> <span data-ttu-id="5692e-200">SignalR 會在每次需要處理中樞作業時（例如，當用戶端連接、中斷連線，或對伺服器進行方法呼叫時），建立新的中樞類別實例。</span><span class="sxs-lookup"><span data-stu-id="5692e-200">SignalR creates a new instance of your Hub class each time it needs to handle a Hub operation such as when a client connects, disconnects, or makes a method call to the server.</span></span>

<span data-ttu-id="5692e-201">由於中樞類別的實例是暫時性的，因此您無法使用它們來維護下一個方法呼叫的狀態。</span><span class="sxs-lookup"><span data-stu-id="5692e-201">Because instances of the Hub class are transient, you can't use them to maintain state from one method call to the next.</span></span> <span data-ttu-id="5692e-202">每次伺服器收到來自用戶端的方法呼叫時，中樞類別的新實例就會處理該訊息。</span><span class="sxs-lookup"><span data-stu-id="5692e-202">Each time the server receives a method call from a client, a new instance of your Hub class processes the message.</span></span> <span data-ttu-id="5692e-203">若要透過多個連接和方法呼叫來維護狀態，請使用其他方法（例如資料庫）或中樞類別上的靜態變數，或不是從 `Hub`衍生的不同類別。</span><span class="sxs-lookup"><span data-stu-id="5692e-203">To maintain state through multiple connections and method calls, use some other method such as a database, or a static variable on the Hub class, or a different class that does not derive from `Hub`.</span></span> <span data-ttu-id="5692e-204">如果您將資料保存在記憶體中，在中樞類別上使用靜態變數之類的方法，資料將會在應用程式網域回收時遺失。</span><span class="sxs-lookup"><span data-stu-id="5692e-204">If you persist data in memory, using a method such as a static variable on the Hub class, the data will be lost when the app domain recycles.</span></span>

<span data-ttu-id="5692e-205">如果您想要從您自己的程式碼（在中樞類別外部執行）傳送訊息給用戶端，您無法藉由具現化中樞類別實例來執行此動作，但您可以藉由取得中樞類別之 SignalR 內容物件的參考來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="5692e-205">If you want to send messages to clients from your own code that runs outside the Hub class, you can't do it by instantiating a Hub class instance, but you can do it by getting a reference to the SignalR context object for your Hub class.</span></span> <span data-ttu-id="5692e-206">如需詳細資訊，請參閱本主題稍後[的如何呼叫用戶端方法和從中樞類別外部管理群組](#callfromoutsidehub)。</span><span class="sxs-lookup"><span data-stu-id="5692e-206">For more information, see [How to call client methods and manage groups from outside the Hub class](#callfromoutsidehub) later in this topic.</span></span>

<a id="hubnames"></a>

### <a name="camel-casing-of-hub-names-in-javascript-clients"></a><span data-ttu-id="5692e-207">Camel-JavaScript 用戶端中中樞名稱的大小寫</span><span class="sxs-lookup"><span data-stu-id="5692e-207">Camel-casing of Hub names in JavaScript clients</span></span>

<span data-ttu-id="5692e-208">根據預設，JavaScript 用戶端會使用類別名稱的 camel 大小寫版本來參考中樞。</span><span class="sxs-lookup"><span data-stu-id="5692e-208">By default, JavaScript clients refer to Hubs by using a camel-cased version of the class name.</span></span> <span data-ttu-id="5692e-209">SignalR 會自動進行此變更，使 JavaScript 程式碼可以符合 JavaScript 慣例。</span><span class="sxs-lookup"><span data-stu-id="5692e-209">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span> <span data-ttu-id="5692e-210">先前的範例在 JavaScript 程式碼中稱為 `contosoChatHub`。</span><span class="sxs-lookup"><span data-stu-id="5692e-210">The previous example would be referred to as `contosoChatHub` in JavaScript code.</span></span>

<span data-ttu-id="5692e-211">**Server**</span><span class="sxs-lookup"><span data-stu-id="5692e-211">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample8.cs?highlight=1)]

<span data-ttu-id="5692e-212">**使用產生的 proxy 的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="5692e-212">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample9.js?highlight=1)]

<span data-ttu-id="5692e-213">如果您想要指定不同的名稱供用戶端使用，請新增 `HubName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5692e-213">If you want to specify a different name for clients to use, add the `HubName` attribute.</span></span> <span data-ttu-id="5692e-214">當您使用 `HubName` 屬性時，JavaScript 用戶端上不會有任何名稱變更為 camel 案例。</span><span class="sxs-lookup"><span data-stu-id="5692e-214">When you use a `HubName` attribute, there is no name change to camel case on JavaScript clients.</span></span>

<span data-ttu-id="5692e-215">**Server**</span><span class="sxs-lookup"><span data-stu-id="5692e-215">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample10.cs?highlight=1)]

<span data-ttu-id="5692e-216">**使用產生的 proxy 的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="5692e-216">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample11.js?highlight=1)]

<a id="multiplehubs"></a>

### <a name="multiple-hubs"></a><span data-ttu-id="5692e-217">多個中樞</span><span class="sxs-lookup"><span data-stu-id="5692e-217">Multiple Hubs</span></span>

<span data-ttu-id="5692e-218">您可以在應用程式中定義多個中樞類別。</span><span class="sxs-lookup"><span data-stu-id="5692e-218">You can define multiple Hub classes in an application.</span></span> <span data-ttu-id="5692e-219">當您這麼做時，會共用連線，但群組會分開：</span><span class="sxs-lookup"><span data-stu-id="5692e-219">When you do that, the connection is shared but groups are separate:</span></span>

- <span data-ttu-id="5692e-220">所有用戶端都會使用相同的 URL 來與您的服務建立 SignalR 連線（如果您指定了 "/signalr" 或您的自訂 URL），而且該連線會用於服務所定義的所有中樞。</span><span class="sxs-lookup"><span data-stu-id="5692e-220">All clients will use the same URL to establish a SignalR connection with your service ("/signalr" or your custom URL if you specified one), and that connection is used for all Hubs defined by the service.</span></span>

    <span data-ttu-id="5692e-221">相較于在單一類別中定義所有中樞功能，多個中樞沒有任何效能上的差異。</span><span class="sxs-lookup"><span data-stu-id="5692e-221">There is no performance difference for multiple Hubs compared to defining all Hub functionality in a single class.</span></span>
- <span data-ttu-id="5692e-222">所有中樞都會取得相同的 HTTP 要求資訊。</span><span class="sxs-lookup"><span data-stu-id="5692e-222">All Hubs get the same HTTP request information.</span></span>

    <span data-ttu-id="5692e-223">由於所有中樞共用相同的連線，因此伺服器取得的唯一 HTTP 要求資訊就是建立 SignalR 連接的原始 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="5692e-223">Since all Hubs share the same connection, the only HTTP request information that the server gets is what comes in the original HTTP request that establishes the SignalR connection.</span></span> <span data-ttu-id="5692e-224">如果您使用連線要求，藉由指定查詢字串，將資訊從用戶端傳遞至伺服器，您就無法將不同的查詢字串提供給不同的中樞。</span><span class="sxs-lookup"><span data-stu-id="5692e-224">If you use the connection request to pass information from the client to the server by specifying a query string, you can't provide different query strings to different Hubs.</span></span> <span data-ttu-id="5692e-225">所有中樞都會收到相同的資訊。</span><span class="sxs-lookup"><span data-stu-id="5692e-225">All Hubs will receive the same information.</span></span>
- <span data-ttu-id="5692e-226">產生的 JavaScript proxy 檔案會包含一個檔案中所有中樞的 proxy。</span><span class="sxs-lookup"><span data-stu-id="5692e-226">The generated JavaScript proxies file will contain proxies for all Hubs in one file.</span></span>

    <span data-ttu-id="5692e-227">如需 JavaScript proxy 的相關資訊，請參閱[SignalR HUB API Guide-JavaScript Client-產生的 proxy 和它為您提供的功能](hubs-api-guide-javascript-client.md#genproxy)。</span><span class="sxs-lookup"><span data-stu-id="5692e-227">For information about JavaScript proxies, see [SignalR Hubs API Guide - JavaScript Client - The generated proxy and what it does for you](hubs-api-guide-javascript-client.md#genproxy).</span></span>
- <span data-ttu-id="5692e-228">群組定義于中樞內。</span><span class="sxs-lookup"><span data-stu-id="5692e-228">Groups are defined within Hubs.</span></span>

    <span data-ttu-id="5692e-229">在 SignalR 中，您可以定義要廣播至已連線用戶端子集的命名群組。</span><span class="sxs-lookup"><span data-stu-id="5692e-229">In SignalR you can define named groups to broadcast to subsets of connected clients.</span></span> <span data-ttu-id="5692e-230">群組會分別針對每個中樞進行維護。</span><span class="sxs-lookup"><span data-stu-id="5692e-230">Groups are maintained separately for each Hub.</span></span> <span data-ttu-id="5692e-231">例如，名為「系統管理員」的群組會包含一組 `ContosoChatHub` 類別的用戶端，而相同的組名會參照 `StockTickerHub` 類別的一組不同的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-231">For example, a group named "Administrators" would include one set of clients for your `ContosoChatHub` class, and the same group name would refer to a different set of clients for your `StockTickerHub` class.</span></span>

<a id="stronglytypedhubs"></a>
### <a name="strongly-typed-hubs"></a><span data-ttu-id="5692e-232">強型別中樞</span><span class="sxs-lookup"><span data-stu-id="5692e-232">Strongly-Typed Hubs</span></span>

<span data-ttu-id="5692e-233">若要定義您的中樞方法的介面，讓您的用戶端可以參考（並在您的中樞方法上啟用 Intellisense），請從 `Hub<T>` （在 SignalR 2.1 中引進）衍生您的中樞，而不是 `Hub`：</span><span class="sxs-lookup"><span data-stu-id="5692e-233">To define an interface for your hub methods that your client can reference (and enable Intellisense on your hub methods), derive your hub from `Hub<T>` (introduced in SignalR 2.1) rather than `Hub`:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample12.cs)]

<a id="hubmethods"></a>

## <a name="how-to-define-methods-in-the-hub-class-that-clients-can-call"></a><span data-ttu-id="5692e-234">如何在中樞類別中定義用戶端可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="5692e-234">How to define methods in the Hub class that clients can call</span></span>

<span data-ttu-id="5692e-235">若要在中樞上公開您想要從用戶端呼叫的方法，請宣告公用方法，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5692e-235">To expose a method on the Hub that you want to be callable from the client, declare a public method, as shown in the following examples.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample13.cs?highlight=3)]

[!code-csharp[Main](hubs-api-guide-server/samples/sample14.cs?highlight=3)]

<span data-ttu-id="5692e-236">您可以指定傳回類型和參數，包括複雜類型和陣列，就像在任何C#方法中一樣。</span><span class="sxs-lookup"><span data-stu-id="5692e-236">You can specify a return type and parameters, including complex types and arrays, as you would in any C# method.</span></span> <span data-ttu-id="5692e-237">您在參數中接收或傳回給呼叫者的任何資料都會使用 JSON 在用戶端與伺服器之間進行通訊，而 SignalR 則會自動處理複雜物件和物件陣列的系結。</span><span class="sxs-lookup"><span data-stu-id="5692e-237">Any data that you receive in parameters or return to the caller is communicated between the client and the server by using JSON, and SignalR handles the binding of complex objects and arrays of objects automatically.</span></span>

<a id="methodnames"></a>

### <a name="camel-casing-of-method-names-in-javascript-clients"></a><span data-ttu-id="5692e-238">Camel-JavaScript 用戶端中方法名稱的大小寫</span><span class="sxs-lookup"><span data-stu-id="5692e-238">Camel-casing of method names in JavaScript clients</span></span>

<span data-ttu-id="5692e-239">根據預設，JavaScript 用戶端會使用方法名稱的 camel 大小寫版本來參考中樞方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-239">By default, JavaScript clients refer to Hub methods by using a camel-cased version of the method name.</span></span> <span data-ttu-id="5692e-240">SignalR 會自動進行此變更，使 JavaScript 程式碼可以符合 JavaScript 慣例。</span><span class="sxs-lookup"><span data-stu-id="5692e-240">SignalR automatically makes this change so that JavaScript code can conform to JavaScript conventions.</span></span>

<span data-ttu-id="5692e-241">**Server**</span><span class="sxs-lookup"><span data-stu-id="5692e-241">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample15.cs?highlight=1)]

<span data-ttu-id="5692e-242">**使用產生的 proxy 的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="5692e-242">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample16.js?highlight=1)]

<span data-ttu-id="5692e-243">如果您想要指定不同的名稱供用戶端使用，請新增 `HubMethodName` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5692e-243">If you want to specify a different name for clients to use, add the `HubMethodName` attribute.</span></span>

<span data-ttu-id="5692e-244">**Server**</span><span class="sxs-lookup"><span data-stu-id="5692e-244">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample17.cs?highlight=1)]

<span data-ttu-id="5692e-245">**使用產生的 proxy 的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="5692e-245">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample18.js?highlight=1)]

<a id="asyncmethods"></a>

### <a name="when-to-execute-asynchronously"></a><span data-ttu-id="5692e-246">非同步執行的時機</span><span class="sxs-lookup"><span data-stu-id="5692e-246">When to execute asynchronously</span></span>

<span data-ttu-id="5692e-247">如果此方法將會長時間執行，或必須執行需要等候的工作（例如資料庫查閱或 web 服務呼叫），請傳回[工作（取代](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx)`void` return）或[task&lt;t&gt;](https://msdn.microsoft.com/library/dd321424.aspx)物件（取代 `T` 傳回型別），以將中樞方法設為非同步。</span><span class="sxs-lookup"><span data-stu-id="5692e-247">If the method will be long-running or has to do work that would involve waiting, such as a database lookup or a web service call, make the Hub method asynchronous by returning a [Task](https://msdn.microsoft.com/library/system.threading.tasks.task.aspx) (in place of `void` return) or [Task&lt;T&gt;](https://msdn.microsoft.com/library/dd321424.aspx) object (in place of `T` return type).</span></span> <span data-ttu-id="5692e-248">當您從方法傳回 `Task` 物件時，SignalR 會等候 `Task` 完成，然後將解除包裝的結果傳送回用戶端，因此在用戶端中撰寫方法呼叫程式碼的方式並沒有差異。</span><span class="sxs-lookup"><span data-stu-id="5692e-248">When you return a `Task` object from the method, SignalR waits for the `Task` to complete, and then it sends the unwrapped result back to the client, so there is no difference in how you code the method call in the client.</span></span>

<span data-ttu-id="5692e-249">讓中樞方法非同步可避免在使用 WebSocket 傳輸時封鎖連接。</span><span class="sxs-lookup"><span data-stu-id="5692e-249">Making a Hub method asynchronous avoids blocking the connection when it uses the WebSocket transport.</span></span> <span data-ttu-id="5692e-250">當中樞方法以同步方式執行，且傳輸為 WebSocket 時，在中樞方法完成之前，系統會封鎖從相同用戶端對集線器上的方法進行後續的調用。</span><span class="sxs-lookup"><span data-stu-id="5692e-250">When a Hub method executes synchronously and the transport is WebSocket, subsequent invocations of methods on the Hub from the same client are blocked until the Hub method completes.</span></span>

<span data-ttu-id="5692e-251">下列範例顯示程式碼中，以同步或非同步方式執行的相同方法，接著是可用於呼叫任一版本的 JavaScript 用戶端程式代碼。</span><span class="sxs-lookup"><span data-stu-id="5692e-251">The following example shows the same method coded to run synchronously or asynchronously, followed by JavaScript client code that works for calling either version.</span></span>

<span data-ttu-id="5692e-252">**同步**</span><span class="sxs-lookup"><span data-stu-id="5692e-252">**Synchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample19.cs)]

<span data-ttu-id="5692e-253">**同步**</span><span class="sxs-lookup"><span data-stu-id="5692e-253">**Asynchronous**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample20.cs?highlight=1,7-8)]

<span data-ttu-id="5692e-254">**使用產生的 proxy 的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="5692e-254">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample21.js)]

<span data-ttu-id="5692e-255">如需如何在 ASP.NET 4.5 中使用非同步方法的詳細資訊，請參閱[在 ASP.NET MVC 4 中使用非同步方法](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md)。</span><span class="sxs-lookup"><span data-stu-id="5692e-255">For more information about how to use asynchronous methods in ASP.NET 4.5, see [Using Asynchronous Methods in ASP.NET MVC 4](../../../mvc/overview/performance/using-asynchronous-methods-in-aspnet-mvc-4.md).</span></span>

<a id="overloads"></a>

### <a name="defining-overloads"></a><span data-ttu-id="5692e-256">定義多載</span><span class="sxs-lookup"><span data-stu-id="5692e-256">Defining Overloads</span></span>

<span data-ttu-id="5692e-257">如果您想要為方法定義多載，則每個多載中的參數數目必須不同。</span><span class="sxs-lookup"><span data-stu-id="5692e-257">If you want to define overloads for a method, the number of parameters in each overload must be different.</span></span> <span data-ttu-id="5692e-258">如果您只要指定不同的參數類型來區分多載，則您的中樞類別會進行編譯，但當用戶端嘗試呼叫其中一個多載時，SignalR 服務將會在執行時間擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5692e-258">If you differentiate an overload just by specifying different parameter types, your Hub class will compile but the SignalR service will throw an exception at run time when clients try to call one of the overloads.</span></span>

<a id="progress"></a>
### <a name="reporting-progress-from-hub-method-invocations"></a><span data-ttu-id="5692e-259">從中樞方法調用報告進度</span><span class="sxs-lookup"><span data-stu-id="5692e-259">Reporting progress from hub method invocations</span></span>

<span data-ttu-id="5692e-260">SignalR 2.1 新增了 .NET 4.5 中所引進之[進度報告模式](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx)的支援。</span><span class="sxs-lookup"><span data-stu-id="5692e-260">SignalR 2.1 adds support for the [progress reporting pattern](https://blogs.msdn.com/b/dotnet/archive/2012/06/06/async-in-4-5-enabling-progress-and-cancellation-in-async-apis.aspx) introduced in .NET 4.5.</span></span> <span data-ttu-id="5692e-261">若要執行進度報告，請為您的用戶端可以存取的中樞方法定義 `IProgress<T>` 參數：</span><span class="sxs-lookup"><span data-stu-id="5692e-261">To implement progress reporting, define an `IProgress<T>` parameter for your hub method that your client can access:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample22.cs)]

<span data-ttu-id="5692e-262">撰寫長時間執行的伺服器方法時，請務必使用非同步程式設計模式，例如 Async/Await，而不是封鎖中樞執行緒。</span><span class="sxs-lookup"><span data-stu-id="5692e-262">When writing a long-running server method, it is important to use an asynchronous programming pattern like Async/ Await rather than blocking the hub thread.</span></span>

<a id="callfromhub"></a>

## <a name="how-to-call-client-methods-from-the-hub-class"></a><span data-ttu-id="5692e-263">如何從中樞類別呼叫用戶端方法</span><span class="sxs-lookup"><span data-stu-id="5692e-263">How to call client methods from the Hub class</span></span>

<span data-ttu-id="5692e-264">若要從伺服器呼叫用戶端方法，請在中樞類別的方法中使用 `Clients` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5692e-264">To call client methods from the server, use the `Clients` property in a method in your Hub class.</span></span> <span data-ttu-id="5692e-265">下列範例顯示的伺服器程式碼會呼叫所有已連線用戶端上的 `addNewMessageToPage`，以及在 JavaScript 用戶端中定義方法的用戶端程式代碼。</span><span class="sxs-lookup"><span data-stu-id="5692e-265">The following example shows server code that calls `addNewMessageToPage` on all connected clients, and client code that defines the method in a JavaScript client.</span></span>

<span data-ttu-id="5692e-266">**Server**</span><span class="sxs-lookup"><span data-stu-id="5692e-266">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample23.cs?highlight=5)]

<span data-ttu-id="5692e-267">叫用用戶端方法是非同步作業，並傳回 `Task`。</span><span class="sxs-lookup"><span data-stu-id="5692e-267">Invoking a client method is an asynchronous operation and returns a `Task`.</span></span> <span data-ttu-id="5692e-268">使用 `await`：</span><span class="sxs-lookup"><span data-stu-id="5692e-268">Use `await`:</span></span>

* <span data-ttu-id="5692e-269">以確保訊息會在不發生錯誤的情況下傳送。</span><span class="sxs-lookup"><span data-stu-id="5692e-269">To ensure the message is sent without error.</span></span> 
* <span data-ttu-id="5692e-270">啟用 try-catch 區塊中的攔截和處理錯誤。</span><span class="sxs-lookup"><span data-stu-id="5692e-270">To enable catching and handling errors in a try-catch block.</span></span>

<span data-ttu-id="5692e-271">**使用產生的 proxy 的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="5692e-271">**JavaScript client using generated proxy**</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample24.html?highlight=1)]

<span data-ttu-id="5692e-272">您無法從用戶端方法取得傳回值。`int x = Clients.All.add(1,1)` 之類的語法無法運作。</span><span class="sxs-lookup"><span data-stu-id="5692e-272">You can't get a return value from a client method; syntax such as `int x = Clients.All.add(1,1)` does not work.</span></span>

<span data-ttu-id="5692e-273">您可以針對參數指定複雜的類型和陣列。</span><span class="sxs-lookup"><span data-stu-id="5692e-273">You can specify complex types and arrays for the parameters.</span></span> <span data-ttu-id="5692e-274">下列範例會將複雜型別傳遞至方法參數中的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-274">The following example passes a complex type to the client in a method parameter.</span></span>

<span data-ttu-id="5692e-275">**使用複雜物件呼叫用戶端方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="5692e-275">**Server code that calls a client method using a complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample25.cs?highlight=3)]

<span data-ttu-id="5692e-276">**定義複雜物件的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="5692e-276">**Server code that defines the complex object**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample26.cs?highlight=1)]

<span data-ttu-id="5692e-277">**使用產生的 proxy 的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="5692e-277">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample27.js?highlight=2-3)]

<a id="selectingclients"></a>

### <a name="selecting-which-clients-will-receive-the-rpc"></a><span data-ttu-id="5692e-278">選取將接收 RPC 的用戶端</span><span class="sxs-lookup"><span data-stu-id="5692e-278">Selecting which clients will receive the RPC</span></span>

<span data-ttu-id="5692e-279">[用戶端] 屬性會傳回[HubConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)物件，它會提供數個選項來指定要接收 RPC 的用戶端：</span><span class="sxs-lookup"><span data-stu-id="5692e-279">The Clients property returns a [HubConnectionContext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx) object that provides several options for specifying which clients will receive the RPC:</span></span>

- <span data-ttu-id="5692e-280">所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-280">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample28.cs)]
- <span data-ttu-id="5692e-281">僅呼叫用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-281">Only the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample29.cs)]
- <span data-ttu-id="5692e-282">所有用戶端（呼叫用戶端除外）。</span><span class="sxs-lookup"><span data-stu-id="5692e-282">All clients except the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample30.cs)]
- <span data-ttu-id="5692e-283">連接識別碼所識別的特定用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-283">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample31.css)]

    <span data-ttu-id="5692e-284">這個範例會呼叫呼叫用戶端上的 `addContosoChatMessageToPage`，並與使用 `Clients.Caller`的效果相同。</span><span class="sxs-lookup"><span data-stu-id="5692e-284">This example calls `addContosoChatMessageToPage` on the calling client and has the same effect as using `Clients.Caller`.</span></span>
- <span data-ttu-id="5692e-285">所有已連線的用戶端，但指定的用戶端除外，但由連接識別碼識別。</span><span class="sxs-lookup"><span data-stu-id="5692e-285">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample32.cs)]
- <span data-ttu-id="5692e-286">指定群組中所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-286">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample33.css)]
- <span data-ttu-id="5692e-287">指定群組中所有已連線的用戶端，但指定的用戶端除外，但由連接識別碼識別。</span><span class="sxs-lookup"><span data-stu-id="5692e-287">All connected clients in a specified group except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample34.cs)]
- <span data-ttu-id="5692e-288">指定群組中的所有已連線用戶端（呼叫用戶端除外）。</span><span class="sxs-lookup"><span data-stu-id="5692e-288">All connected clients in a specified group except the calling client.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample35.css)]
- <span data-ttu-id="5692e-289">依 userId 識別的特定使用者。</span><span class="sxs-lookup"><span data-stu-id="5692e-289">A specific user, identified by userId.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample36.cs)]

    <span data-ttu-id="5692e-290">根據預設，這是 `IPrincipal.Identity.Name`的，但可透過向[全域主機註冊 IUserIdProvider 的執行](mapping-users-to-connections.md#IUserIdProvider)來變更。</span><span class="sxs-lookup"><span data-stu-id="5692e-290">By default, this is `IPrincipal.Identity.Name`, but this can be changed by [registering an implementation of IUserIdProvider with the global host](mapping-users-to-connections.md#IUserIdProvider).</span></span>
- <span data-ttu-id="5692e-291">連接識別碼清單中的所有用戶端和群組。</span><span class="sxs-lookup"><span data-stu-id="5692e-291">All clients and groups in a list of connection IDs.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample37.css)]
- <span data-ttu-id="5692e-292">群組的清單。</span><span class="sxs-lookup"><span data-stu-id="5692e-292">A list of groups.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample38.css)]
- <span data-ttu-id="5692e-293">依名稱的使用者。</span><span class="sxs-lookup"><span data-stu-id="5692e-293">A user by name.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample39.cs)]
- <span data-ttu-id="5692e-294">使用者名稱的清單（在 SignalR 2.1 中引進）。</span><span class="sxs-lookup"><span data-stu-id="5692e-294">A list of user names (introduced in SignalR 2.1).</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample40.cs)]

<a id="dynamicmethodnames"></a>

### <a name="no-compile-time-validation-for-method-names"></a><span data-ttu-id="5692e-295">方法名稱沒有編譯時間驗證</span><span class="sxs-lookup"><span data-stu-id="5692e-295">No compile-time validation for method names</span></span>

<span data-ttu-id="5692e-296">您指定的方法名稱會被視為動態物件，這表示沒有任何 IntelliSense 或編譯時間驗證。</span><span class="sxs-lookup"><span data-stu-id="5692e-296">The method name that you specify is interpreted as a dynamic object, which means there is no IntelliSense or compile-time validation for it.</span></span> <span data-ttu-id="5692e-297">運算式會在執行時間進行評估。</span><span class="sxs-lookup"><span data-stu-id="5692e-297">The expression is evaluated at run time.</span></span> <span data-ttu-id="5692e-298">當方法呼叫執行時，SignalR 會將方法名稱和參數值傳送至用戶端，如果用戶端有符合名稱的方法，就會呼叫該方法，並將參數值傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="5692e-298">When the method call executes, SignalR sends the method name and the parameter values to the client, and if the client has a method that matches the name, that method is called and the parameter values are passed to it.</span></span> <span data-ttu-id="5692e-299">如果在用戶端上找不到相符的方法，則不會引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="5692e-299">If no matching method is found on the client, no error is raised.</span></span> <span data-ttu-id="5692e-300">如需當您呼叫用戶端方法時，SignalR 傳輸至用戶端之資料格式的相關資訊，請參閱[SignalR 簡介](../getting-started/introduction-to-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="5692e-300">For information about the format of the data that SignalR transmits to the client behind the scenes when you call a client method, see [Introduction to SignalR](../getting-started/introduction-to-signalr.md).</span></span>

<a id="caseinsensitive"></a>

### <a name="case-insensitive-method-name-matching"></a><span data-ttu-id="5692e-301">不區分大小寫的方法名稱比對</span><span class="sxs-lookup"><span data-stu-id="5692e-301">Case-insensitive method name matching</span></span>

<span data-ttu-id="5692e-302">方法名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="5692e-302">Method name matching is case-insensitive.</span></span> <span data-ttu-id="5692e-303">例如，伺服器上的 `Clients.All.addContosoChatMessageToPage` 將會在用戶端上執行 `AddContosoChatMessageToPage`、`addcontosochatmessagetopage`或 `addContosoChatMessageToPage`。</span><span class="sxs-lookup"><span data-stu-id="5692e-303">For example, `Clients.All.addContosoChatMessageToPage` on the server will execute `AddContosoChatMessageToPage`, `addcontosochatmessagetopage`, or `addContosoChatMessageToPage` on the client.</span></span>

<a id="asyncclient"></a>

### <a name="asynchronous-execution"></a><span data-ttu-id="5692e-304">非同步執行</span><span class="sxs-lookup"><span data-stu-id="5692e-304">Asynchronous execution</span></span>

<span data-ttu-id="5692e-305">您呼叫的方法會以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="5692e-305">The method that you call executes asynchronously.</span></span> <span data-ttu-id="5692e-306">任何在方法呼叫至用戶端之後的程式碼都會立即執行，而不會等候 SignalR 完成將資料傳送至用戶端，除非您指定後續的程式程式碼應該等候方法完成。</span><span class="sxs-lookup"><span data-stu-id="5692e-306">Any code that comes after a method call to a client will execute immediately without waiting for SignalR to finish transmitting data to clients unless you specify that the subsequent lines of code should wait for method completion.</span></span> <span data-ttu-id="5692e-307">下列程式碼範例顯示如何依序執行兩個用戶端方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-307">The following code example shows how to execute two client methods sequentially.</span></span>

<span data-ttu-id="5692e-308">**使用 Await （.NET 4.5）**</span><span class="sxs-lookup"><span data-stu-id="5692e-308">**Using Await (.NET 4.5)**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample41.cs?highlight=1,3)]

<span data-ttu-id="5692e-309">如果您使用 `await` 等待用戶端方法在下一行程式碼執行之前完成，這並不表示用戶端會在下一行程式碼執行之前，實際收到訊息。</span><span class="sxs-lookup"><span data-stu-id="5692e-309">If you use `await` to wait until a client method finishes before the next line of code executes, that does not mean that clients will actually receive the message before the next line of code executes.</span></span> <span data-ttu-id="5692e-310">用戶端方法呼叫的「完成」只表示 SignalR 已完成傳送訊息所需的一切動作。</span><span class="sxs-lookup"><span data-stu-id="5692e-310">"Completion" of a client method call only means that SignalR has done everything necessary to send the message.</span></span> <span data-ttu-id="5692e-311">如果您需要驗證用戶端是否已收到訊息，您必須自行編寫該機制。</span><span class="sxs-lookup"><span data-stu-id="5692e-311">If you need verification that clients received the message, you have to program that mechanism yourself.</span></span> <span data-ttu-id="5692e-312">例如，您可以在中樞上撰寫 `MessageReceived` 方法的程式碼，而在用戶端的 `addContosoChatMessageToPage` 方法中，您可以在執行任何需要在用戶端上執行的工作之後，呼叫 `MessageReceived`。</span><span class="sxs-lookup"><span data-stu-id="5692e-312">For example, you could code a `MessageReceived` method on the Hub, and in the `addContosoChatMessageToPage` method on the client you could call `MessageReceived` after you do whatever work you need to do on the client.</span></span> <span data-ttu-id="5692e-313">在中樞的 `MessageReceived` 中，您可以執行任何工作取決於實際的用戶端接收和原始方法呼叫的處理。</span><span class="sxs-lookup"><span data-stu-id="5692e-313">In `MessageReceived` in the Hub you can do whatever work depends on actual client reception and processing of the original method call.</span></span>

### <a name="how-to-use-a-string-variable-as-the-method-name"></a><span data-ttu-id="5692e-314">如何使用字串變數做為方法名稱</span><span class="sxs-lookup"><span data-stu-id="5692e-314">How to use a string variable as the method name</span></span>

<span data-ttu-id="5692e-315">如果您想要使用字串變數做為方法名稱來叫用用戶端方法，請將 `Clients.All` （或 `Clients.Others`、`Clients.Caller`等）轉換成 `IClientProxy`，然後再呼叫[invoke （方法名稱，args ...）](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="5692e-315">If you want to invoke a client method by using a string variable as the method name, cast `Clients.All` (or `Clients.Others`, `Clients.Caller`, etc.) to `IClientProxy` and then call [Invoke(methodName, args...)](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.iclientproxy.invoke(v=vs.111).aspx).</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample42.cs)]

<a id="groupsfromhub"></a>

## <a name="how-to-manage-group-membership-from-the-hub-class"></a><span data-ttu-id="5692e-316">如何從中樞類別管理群組成員資格</span><span class="sxs-lookup"><span data-stu-id="5692e-316">How to manage group membership from the Hub class</span></span>

<span data-ttu-id="5692e-317">SignalR 中的群組提供一種方法，可將訊息廣播到已連線用戶端的指定子集。</span><span class="sxs-lookup"><span data-stu-id="5692e-317">Groups in SignalR provide a method for broadcasting messages to specified subsets of connected clients.</span></span> <span data-ttu-id="5692e-318">群組可以有任意數目的用戶端，而用戶端可以是任意數目群組的成員。</span><span class="sxs-lookup"><span data-stu-id="5692e-318">A group can have any number of clients, and a client can be a member of any number of groups.</span></span>

<span data-ttu-id="5692e-319">若要管理群組成員資格，請使用中樞類別的 `Groups` 屬性所提供的 [[新增](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx)] 和 [[移除](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx)] 方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-319">To manage group membership, use the [Add](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.add(v=vs.111).aspx) and [Remove](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.igroupmanager.remove(v=vs.111).aspx) methods provided by the `Groups` property of the Hub class.</span></span> <span data-ttu-id="5692e-320">下列範例顯示用戶端程式代碼所呼叫的中樞方法中所使用的 `Groups.Add` 和 `Groups.Remove` 方法，後面接著呼叫它們的 JavaScript 用戶端程式代碼。</span><span class="sxs-lookup"><span data-stu-id="5692e-320">The following example shows the `Groups.Add` and `Groups.Remove` methods used in Hub methods that are called by client code, followed by JavaScript client code that calls them.</span></span>

<span data-ttu-id="5692e-321">**Server**</span><span class="sxs-lookup"><span data-stu-id="5692e-321">**Server**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample43.cs?highlight=5,10)]

<span data-ttu-id="5692e-322">**使用產生的 proxy 的 JavaScript 用戶端**</span><span class="sxs-lookup"><span data-stu-id="5692e-322">**JavaScript client using generated proxy**</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample44.js)]

[!code-javascript[Main](hubs-api-guide-server/samples/sample45.js)]

<span data-ttu-id="5692e-323">您不需要明確建立群組。</span><span class="sxs-lookup"><span data-stu-id="5692e-323">You don't have to explicitly create groups.</span></span> <span data-ttu-id="5692e-324">實際上，群組會在您第一次於 `Groups.Add`的呼叫中指定其名稱時自動建立，而且當您從其中的成員資格移除最後一個連接時，就會將它刪除。</span><span class="sxs-lookup"><span data-stu-id="5692e-324">In effect a group is automatically created the first time you specify its name in a call to `Groups.Add`, and it is deleted when you remove the last connection from membership in it.</span></span>

<span data-ttu-id="5692e-325">沒有 API 可取得群組成員資格清單或群組清單。</span><span class="sxs-lookup"><span data-stu-id="5692e-325">There is no API for getting a group membership list or a list of groups.</span></span> <span data-ttu-id="5692e-326">SignalR 會根據[pub/sub 模型](http://en.wikipedia.org/wiki/Publish/subscribe)將訊息傳送至用戶端和群組，而伺服器不會維護群組或群組成員資格的清單。</span><span class="sxs-lookup"><span data-stu-id="5692e-326">SignalR sends messages to clients and groups based on a [pub/sub model](http://en.wikipedia.org/wiki/Publish/subscribe), and the server does not maintain lists of groups or group memberships.</span></span> <span data-ttu-id="5692e-327">這有助於最大化擴充性，因為每當您將節點加入至 web 伺服陣列時，SignalR 維護的任何狀態都必須傳播到新的節點。</span><span class="sxs-lookup"><span data-stu-id="5692e-327">This helps maximize scalability, because whenever you add a node to a web farm, any state that SignalR maintains has to be propagated to the new node.</span></span>

<a id="asyncgroupmethods"></a>

### <a name="asynchronous-execution-of-add-and-remove-methods"></a><span data-ttu-id="5692e-328">非同步執行 Add 和 Remove 方法</span><span class="sxs-lookup"><span data-stu-id="5692e-328">Asynchronous execution of Add and Remove methods</span></span>

<span data-ttu-id="5692e-329">`Groups.Add` 和 `Groups.Remove` 方法會以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="5692e-329">The `Groups.Add` and `Groups.Remove` methods execute asynchronously.</span></span> <span data-ttu-id="5692e-330">如果您想要將用戶端新增至群組，並使用群組立即將訊息傳送至用戶端，您必須先確定 `Groups.Add` 方法會先完成。</span><span class="sxs-lookup"><span data-stu-id="5692e-330">If you want to add a client to a group and immediately send a message to the client by using the group, you have to make sure that the `Groups.Add` method finishes first.</span></span> <span data-ttu-id="5692e-331">下列程式碼範例顯示如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="5692e-331">The following code example shows how to do that.</span></span>

<span data-ttu-id="5692e-332">**將用戶端新增至群組，然後將用戶端的訊息傳送至**</span><span class="sxs-lookup"><span data-stu-id="5692e-332">**Adding a client to a group and then messaging that client**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample46.cs?highlight=1,3)]

<a id="grouppersistence"></a>

### <a name="group-membership-persistence"></a><span data-ttu-id="5692e-333">群組成員資格持續性</span><span class="sxs-lookup"><span data-stu-id="5692e-333">Group membership persistence</span></span>

<span data-ttu-id="5692e-334">SignalR 會追蹤連接，而不是使用者，因此，如果您希望使用者在每次建立連線時都位於相同的群組中，您必須在每次使用者建立新連線時呼叫 `Groups.Add`。</span><span class="sxs-lookup"><span data-stu-id="5692e-334">SignalR tracks connections, not users, so if you want a user to be in the same group every time the user establishes a connection, you have to call `Groups.Add` every time the user establishes a new connection.</span></span>

<span data-ttu-id="5692e-335">暫時失去連線能力之後，有時 SignalR 就可以自動還原連接。</span><span class="sxs-lookup"><span data-stu-id="5692e-335">After a temporary loss of connectivity, sometimes SignalR can restore the connection automatically.</span></span> <span data-ttu-id="5692e-336">在此情況下，SignalR 會還原相同的連線，而不是建立新的連線，因此會自動還原用戶端的群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="5692e-336">In that case, SignalR is restoring the same connection, not establishing a new connection, and so the client's group membership is automatically restored.</span></span> <span data-ttu-id="5692e-337">即使暫時中斷是伺服器重新開機或失敗的結果，這是可行的，因為每個用戶端的線上狀態（包括群組成員資格）都會對用戶端進行往返。</span><span class="sxs-lookup"><span data-stu-id="5692e-337">This is possible even when the temporary break is the result of a server reboot or failure, because connection state for each client, including group memberships, is round-tripped to the client.</span></span> <span data-ttu-id="5692e-338">如果伺服器停止運作，並在連接逾時之前由新伺服器取代，用戶端就可以自動重新連接到新的伺服器，並重新註冊其所屬群組。</span><span class="sxs-lookup"><span data-stu-id="5692e-338">If a server goes down and is replaced by a new server before the connection times out, a client can reconnect automatically to the new server and re-enroll in groups it is a member of.</span></span>

<span data-ttu-id="5692e-339">當連接中斷或連接逾時，或當用戶端中斷連線時（例如，當瀏覽器導覽至新頁面時）無法自動還原時，群組成員資格會遺失。</span><span class="sxs-lookup"><span data-stu-id="5692e-339">When a connection can't be restored automatically after a loss of connectivity, or when the connection times out, or when the client disconnects (for example, when a browser navigates to a new page), group memberships are lost.</span></span> <span data-ttu-id="5692e-340">下次使用者連接時，將會是新的連線。</span><span class="sxs-lookup"><span data-stu-id="5692e-340">The next time the user connects will be a new connection.</span></span> <span data-ttu-id="5692e-341">若要在相同的使用者建立新連線時維護群組成員資格，您的應用程式必須追蹤使用者與群組之間的關聯，並在每次使用者建立新連線時還原群組成員資格。</span><span class="sxs-lookup"><span data-stu-id="5692e-341">To maintain group memberships when the same user establishes a new connection, your application has to track the associations between users and groups, and restore group memberships each time a user establishes a new connection.</span></span>

<span data-ttu-id="5692e-342">如需連線和重新連接的詳細資訊，請參閱本主題稍後[的如何處理中樞類別中的連接存留期事件](#connectionlifetime)。</span><span class="sxs-lookup"><span data-stu-id="5692e-342">For more information about connections and reconnections, see [How to handle connection lifetime events in the Hub class](#connectionlifetime) later in this topic.</span></span>

<a id="singleusergroups"></a>

### <a name="single-user-groups"></a><span data-ttu-id="5692e-343">單一使用者群組</span><span class="sxs-lookup"><span data-stu-id="5692e-343">Single-user groups</span></span>

<span data-ttu-id="5692e-344">使用 SignalR 的應用程式通常必須追蹤使用者與連線之間的關聯，才能知道哪些使用者已傳送訊息，以及哪些使用者應該接收訊息。</span><span class="sxs-lookup"><span data-stu-id="5692e-344">Applications that use SignalR typically have to keep track of the associations between users and connections in order to know which user has sent a message and which user(s) should be receiving a message.</span></span> <span data-ttu-id="5692e-345">群組是用來進行這兩種常用模式的其中一種。</span><span class="sxs-lookup"><span data-stu-id="5692e-345">Groups are used in one of the two commonly used patterns for doing that.</span></span>

- <span data-ttu-id="5692e-346">單一使用者群組。</span><span class="sxs-lookup"><span data-stu-id="5692e-346">Single-user groups.</span></span>

    <span data-ttu-id="5692e-347">您可以指定使用者名稱做為組名，並在每次使用者連線或重新連線時，將目前的連接識別碼加入至群組。</span><span class="sxs-lookup"><span data-stu-id="5692e-347">You can specify the user name as the group name, and add the current connection ID to the group every time the user connects or reconnects.</span></span> <span data-ttu-id="5692e-348">將訊息傳送給您傳送至群組的使用者。</span><span class="sxs-lookup"><span data-stu-id="5692e-348">To send messages to the user you send to the group.</span></span> <span data-ttu-id="5692e-349">此方法的缺點是，群組不會提供您一種方法來找出使用者是否處於線上或離線狀態。</span><span class="sxs-lookup"><span data-stu-id="5692e-349">A disadvantage of this method is that the group doesn't provide you with a way to find out if the user is online or offline.</span></span>
- <span data-ttu-id="5692e-350">追蹤使用者名稱和連接識別碼之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="5692e-350">Track associations between user names and connection IDs.</span></span>

    <span data-ttu-id="5692e-351">您可以在每個使用者名稱和字典或資料庫中的一個或多個連接識別碼之間儲存關聯，並在每次使用者連接或中斷連線時更新儲存的資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-351">You can store an association between each user name and one or more connection IDs in a dictionary or database, and update the stored data each time the user connects or disconnects.</span></span> <span data-ttu-id="5692e-352">若要將訊息傳送給使用者，您可以指定連接識別碼。</span><span class="sxs-lookup"><span data-stu-id="5692e-352">To send messages to the user you specify the connection IDs.</span></span> <span data-ttu-id="5692e-353">這個方法的缺點是它會佔用更多的記憶體。</span><span class="sxs-lookup"><span data-stu-id="5692e-353">A disadvantage of this method is that it takes more memory.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events-in-the-hub-class"></a><span data-ttu-id="5692e-354">如何處理中樞類別中的連接存留期事件</span><span class="sxs-lookup"><span data-stu-id="5692e-354">How to handle connection lifetime events in the Hub class</span></span>

<span data-ttu-id="5692e-355">處理連接存留期事件的一般原因是追蹤使用者是否已連線，以及追蹤使用者名稱和連接識別碼之間的關聯。</span><span class="sxs-lookup"><span data-stu-id="5692e-355">Typical reasons for handling connection lifetime events are to keep track of whether a user is connected or not, and to keep track of the association between user names and connection IDs.</span></span> <span data-ttu-id="5692e-356">若要在用戶端連接或中斷連線時執行自己的程式碼，請覆寫中樞類別的 `OnConnected`、`OnDisconnected`和 `OnReconnected` 虛擬方法，如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="5692e-356">To run your own code when clients connect or disconnect, override the `OnConnected`, `OnDisconnected`, and `OnReconnected` virtual methods of the Hub class, as shown in the following example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample47.cs?highlight=3,14,22)]

<a id="onreconnected"></a>

### <a name="when-onconnected-ondisconnected-and-onreconnected-are-called"></a><span data-ttu-id="5692e-357">呼叫 OnConnected、OnDisconnected 和 OnReconnected 時</span><span class="sxs-lookup"><span data-stu-id="5692e-357">When OnConnected, OnDisconnected, and OnReconnected are called</span></span>

<span data-ttu-id="5692e-358">每次瀏覽器導覽至新的頁面時，都必須建立新的連接，這表示 SignalR 會執行 `OnDisconnected` 方法，後面接著 `OnConnected` 方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-358">Each time a browser navigates to a new page, a new connection has to be established, which means SignalR will execute the `OnDisconnected` method followed by the `OnConnected` method.</span></span> <span data-ttu-id="5692e-359">建立新的連接時，SignalR 一律會建立新的連線識別碼。</span><span class="sxs-lookup"><span data-stu-id="5692e-359">SignalR always creates a new connection ID when a new connection is established.</span></span>

<span data-ttu-id="5692e-360">當 SignalR 可自動復原的連線中斷時，會呼叫 `OnReconnected` 方法，例如在連接逾時之前，纜線暫時中斷連線並重新連線。當用戶端已中斷連線且 SignalR 無法自動重新連接時（例如當瀏覽器導覽至新頁面時），會呼叫 `OnDisconnected` 方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-360">The `OnReconnected` method is called when there has been a temporary break in connectivity that SignalR can automatically recover from, such as when a cable is temporarily disconnected and reconnected before the connection times out. The `OnDisconnected` method is called when the client is disconnected and SignalR can't automatically reconnect, such as when a browser navigates to a new page.</span></span> <span data-ttu-id="5692e-361">因此，指定用戶端的可能事件順序是 `OnConnected`、`OnReconnected`、`OnDisconnected`;或 `OnConnected`，`OnDisconnected`。</span><span class="sxs-lookup"><span data-stu-id="5692e-361">Therefore, a possible sequence of events for a given client is `OnConnected`, `OnReconnected`, `OnDisconnected`; or `OnConnected`, `OnDisconnected`.</span></span> <span data-ttu-id="5692e-362">您不會看到指定連接的順序 `OnConnected`、`OnDisconnected``OnReconnected`。</span><span class="sxs-lookup"><span data-stu-id="5692e-362">You won't see the sequence `OnConnected`, `OnDisconnected`, `OnReconnected` for a given connection.</span></span>

<span data-ttu-id="5692e-363">在某些情況下，不會呼叫 `OnDisconnected` 方法，例如當伺服器停止運作或回收應用程式域時。</span><span class="sxs-lookup"><span data-stu-id="5692e-363">The `OnDisconnected` method doesn't get called in some scenarios, such as when a server goes down or the App Domain gets recycled.</span></span> <span data-ttu-id="5692e-364">當另一部伺服器開機時，或應用程式域完成其回收時，某些用戶端可能可以重新連線並引發 `OnReconnected` 事件。</span><span class="sxs-lookup"><span data-stu-id="5692e-364">When another server comes on line or the App Domain completes its recycle, some clients may be able to reconnect and fire the `OnReconnected` event.</span></span>

<span data-ttu-id="5692e-365">如需詳細資訊，請參閱[瞭解和處理 SignalR 中的連接存留期事件](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="5692e-365">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="nocallerstate"></a>

### <a name="caller-state-not-populated"></a><span data-ttu-id="5692e-366">未填入呼叫者狀態</span><span class="sxs-lookup"><span data-stu-id="5692e-366">Caller state not populated</span></span>

<span data-ttu-id="5692e-367">系統會從伺服器呼叫連接存留期事件處理常式方法，這表示您放在用戶端上 `state` 物件中的任何狀態，都不會填入伺服器上的 `Caller` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5692e-367">The connection lifetime event handler methods are called from the server, which means that any state that you put in the `state` object on the client will not be populated in the `Caller` property on the server.</span></span> <span data-ttu-id="5692e-368">如需 `state` 物件和 `Caller` 屬性的詳細資訊，請參閱本主題稍後的[如何在用戶端與中樞類別之間傳遞狀態](#passstate)。</span><span class="sxs-lookup"><span data-stu-id="5692e-368">For information about the `state` object and the `Caller` property, see [How to pass state between clients and the Hub class](#passstate) later in this topic.</span></span>

<a id="contextproperty"></a>

## <a name="how-to-get-information-about-the-client-from-the-context-property"></a><span data-ttu-id="5692e-369">如何從內容屬性取得用戶端的相關資訊</span><span class="sxs-lookup"><span data-stu-id="5692e-369">How to get information about the client from the Context property</span></span>

<span data-ttu-id="5692e-370">若要取得用戶端的相關資訊，請使用中樞類別的 `Context` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5692e-370">To get information about the client, use the `Context` property of the Hub class.</span></span> <span data-ttu-id="5692e-371">`Context` 屬性會傳回[HubCallerCoNtext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx)物件，它會提供下列資訊的存取權：</span><span class="sxs-lookup"><span data-stu-id="5692e-371">The `Context` property returns a [HubCallerContext](https://msdn.microsoft.com/library/jj890883(v=vs.111).aspx) object which provides access to the following information:</span></span>

- <span data-ttu-id="5692e-372">呼叫用戶端的連線識別碼。</span><span class="sxs-lookup"><span data-stu-id="5692e-372">The connection ID of the calling client.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample48.cs?highlight=1)]

    <span data-ttu-id="5692e-373">連接識別碼是由 SignalR 指派的 GUID （您無法在自己的程式碼中指定值）。</span><span class="sxs-lookup"><span data-stu-id="5692e-373">The connection ID is a GUID that is assigned by SignalR (you can't specify the value in your own code).</span></span> <span data-ttu-id="5692e-374">每個連線都有一個連線識別碼，如果您的應用程式中有多個中樞，則所有中樞都會使用相同的連線識別碼。</span><span class="sxs-lookup"><span data-stu-id="5692e-374">There is one connection ID for each connection, and the same connection ID is used by all Hubs if you have multiple Hubs in your application.</span></span>
- <span data-ttu-id="5692e-375">HTTP 標頭資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-375">HTTP header data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample49.cs?highlight=1)]

    <span data-ttu-id="5692e-376">您也可以從 `Context.Headers`取得 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="5692e-376">You can also get HTTP headers from `Context.Headers`.</span></span> <span data-ttu-id="5692e-377">有多個參考相同的原因，就是先建立 `Context.Headers`，稍後再加入 `Context.Request` 屬性，並保留 `Context.Headers` 以提供回溯相容性。</span><span class="sxs-lookup"><span data-stu-id="5692e-377">The reason for multiple references to the same thing is that `Context.Headers` was created first, the `Context.Request` property was added later, and `Context.Headers` was retained for backward compatibility.</span></span>
- <span data-ttu-id="5692e-378">查詢字串資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-378">Query string data.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample50.cs?highlight=1)]

    <span data-ttu-id="5692e-379">您也可以從 `Context.QueryString`取得查詢字串資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-379">You can also get query string data from `Context.QueryString`.</span></span>

    <span data-ttu-id="5692e-380">您在此屬性中取得的查詢字串，與建立 SignalR 連接的 HTTP 要求搭配使用。</span><span class="sxs-lookup"><span data-stu-id="5692e-380">The query string that you get in this property is the one that was used with the HTTP request that established the SignalR connection.</span></span> <span data-ttu-id="5692e-381">您可以藉由設定連接，在用戶端中加入查詢字串參數，這是將用戶端的相關資料從用戶端傳遞至伺服器的便利方式。</span><span class="sxs-lookup"><span data-stu-id="5692e-381">You can add query string parameters in the client by configuring the connection, which is a convenient way to pass data about the client from the client to the server.</span></span> <span data-ttu-id="5692e-382">下列範例顯示當您使用產生的 proxy 時，在 JavaScript 用戶端中加入查詢字串的一種方式。</span><span class="sxs-lookup"><span data-stu-id="5692e-382">The following example shows one way to add a query string in a JavaScript client when you use the generated proxy.</span></span>

    [!code-javascript[Main](hubs-api-guide-server/samples/sample51.js?highlight=1)]

    <span data-ttu-id="5692e-383">如需設定查詢字串參數的詳細資訊，請參閱[JavaScript](hubs-api-guide-javascript-client.md)和[.net](hubs-api-guide-net-client.md)用戶端的 API 指南。</span><span class="sxs-lookup"><span data-stu-id="5692e-383">For more information about setting query string parameters, see the API guides for the [JavaScript](hubs-api-guide-javascript-client.md) and [.NET](hubs-api-guide-net-client.md) clients.</span></span>

    <span data-ttu-id="5692e-384">您可以在查詢字串資料中找到用於連接的傳輸方法，以及 SignalR 內部使用的一些其他值：</span><span class="sxs-lookup"><span data-stu-id="5692e-384">You can find the transport method used for the connection in the query string data, along with some other values used internally by SignalR:</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample52.cs)]

    <span data-ttu-id="5692e-385">`transportMethod` 的值將會是 "Websocket"、"serverSentEvents"、"foreverFrame" 或 "longPolling"。</span><span class="sxs-lookup"><span data-stu-id="5692e-385">The value of `transportMethod` will be "webSockets", "serverSentEvents", "foreverFrame" or "longPolling".</span></span> <span data-ttu-id="5692e-386">請注意，如果您在 `OnConnected` 事件處理常式方法中檢查此值，在某些情況下，您可能一開始會取得不是連線的最終協商傳輸方法的傳輸值。</span><span class="sxs-lookup"><span data-stu-id="5692e-386">Note that if you check this value in the `OnConnected` event handler method, in some scenarios you might initially get a transport value that is not the final negotiated transport method for the connection.</span></span> <span data-ttu-id="5692e-387">在這種情況下，方法會擲回例外狀況，稍後當最後一個傳輸方法建立時，將會再次呼叫。</span><span class="sxs-lookup"><span data-stu-id="5692e-387">In that case the method will throw an exception and will be called again later when the final transport method is established.</span></span>
- <span data-ttu-id="5692e-388">Cookie。</span><span class="sxs-lookup"><span data-stu-id="5692e-388">Cookies.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample53.cs?highlight=1)]

    <span data-ttu-id="5692e-389">您也可以從 `Context.RequestCookies`取得 cookie。</span><span class="sxs-lookup"><span data-stu-id="5692e-389">You can also get cookies from `Context.RequestCookies`.</span></span>
- <span data-ttu-id="5692e-390">使用者資訊。</span><span class="sxs-lookup"><span data-stu-id="5692e-390">User information.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample54.cs?highlight=1)]
- <span data-ttu-id="5692e-391">要求的 HttpCoNtext 物件：</span><span class="sxs-lookup"><span data-stu-id="5692e-391">The HttpContext object for the request :</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample55.cs?highlight=1)]

    <span data-ttu-id="5692e-392">使用這個方法，而不是取得 `HttpContext.Current`，以取得 SignalR 連接的 `HttpContext` 物件。</span><span class="sxs-lookup"><span data-stu-id="5692e-392">Use this method instead of getting `HttpContext.Current` to get the `HttpContext` object for the SignalR connection.</span></span>

<a id="passstate"></a>

## <a name="how-to-pass-state-between-clients-and-the-hub-class"></a><span data-ttu-id="5692e-393">如何在用戶端與中樞類別之間傳遞狀態</span><span class="sxs-lookup"><span data-stu-id="5692e-393">How to pass state between clients and the Hub class</span></span>

<span data-ttu-id="5692e-394">用戶端 proxy 會提供一個 `state` 物件，您可以在其中儲存您想要使用每個方法呼叫傳送至伺服器的資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-394">The client proxy provides a `state` object in which you can store data that you want to be transmitted to the server with each method call.</span></span> <span data-ttu-id="5692e-395">在伺服器上，您可以在用戶端所呼叫的中樞方法的 [`Clients.Caller`] 屬性中存取此資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-395">On the server you can access this data in the `Clients.Caller` property in Hub methods that are called by clients.</span></span> <span data-ttu-id="5692e-396">`OnConnected`、`OnDisconnected`和 `OnReconnected`的連接存留期事件處理常式方法，不會填入 `Clients.Caller` 屬性。</span><span class="sxs-lookup"><span data-stu-id="5692e-396">The `Clients.Caller` property is not populated for the connection lifetime event handler methods `OnConnected`, `OnDisconnected`, and `OnReconnected`.</span></span>

<span data-ttu-id="5692e-397">建立或更新 `state` 物件中的資料，而 `Clients.Caller` 屬性則可雙向運作。</span><span class="sxs-lookup"><span data-stu-id="5692e-397">Creating or updating data in the `state` object and the `Clients.Caller` property works in both directions.</span></span> <span data-ttu-id="5692e-398">您可以補救伺服器中的值，並將它們傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-398">You can update values in the server and they are passed back to the client.</span></span>

<span data-ttu-id="5692e-399">下列範例顯示的 JavaScript 用戶端程式代碼會儲存狀態，以便在每次方法呼叫時傳送至伺服器。</span><span class="sxs-lookup"><span data-stu-id="5692e-399">The following example shows JavaScript client code that stores state for transmission to the server with every method call.</span></span>

[!code-javascript[Main](hubs-api-guide-server/samples/sample56.js?highlight=1-2)]

<span data-ttu-id="5692e-400">下列範例會顯示 .NET 用戶端中的對等程式碼。</span><span class="sxs-lookup"><span data-stu-id="5692e-400">The following example shows the equivalent code in a .NET client.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample57.cs?highlight=1-2)]

<span data-ttu-id="5692e-401">在您的中樞類別中，您可以在 `Clients.Caller` 屬性中存取此資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-401">In your Hub class, you can access this data in the `Clients.Caller` property.</span></span> <span data-ttu-id="5692e-402">下列範例顯示的程式碼會抓取上一個範例中所參考的狀態。</span><span class="sxs-lookup"><span data-stu-id="5692e-402">The following example shows code that retrieves the state referred to in the previous example.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample58.cs?highlight=3-4)]

> [!NOTE]
> <span data-ttu-id="5692e-403">這種保存狀態的機制並非適用于大量資料，因為您放入 `state` 或 `Clients.Caller` 屬性中的所有專案都是以每個方法調用來進行迴圈處理。</span><span class="sxs-lookup"><span data-stu-id="5692e-403">This mechanism for persisting state is not intended for large amounts of data, since everything you put in the `state` or `Clients.Caller` property is round-tripped with every method invocation.</span></span> <span data-ttu-id="5692e-404">這適用于較小的專案，例如使用者名稱或計數器。</span><span class="sxs-lookup"><span data-stu-id="5692e-404">It's useful for smaller items such as user names or counters.</span></span>

<span data-ttu-id="5692e-405">在 VB.NET 或強型別中樞中，無法透過 `Clients.Caller`存取呼叫端狀態物件。相反地，請使用 `Clients.CallerState` （在 SignalR 2.1 中引進）：</span><span class="sxs-lookup"><span data-stu-id="5692e-405">In VB.NET or in a strongly-typed hub, the caller state object can't be accessed through `Clients.Caller`; instead, use `Clients.CallerState` (introduced in SignalR 2.1):</span></span>

<span data-ttu-id="5692e-406">**使用中的 CallerStateC#**</span><span class="sxs-lookup"><span data-stu-id="5692e-406">**Using CallerState in C#**</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample59.cs?highlight=3-4)]

<span data-ttu-id="5692e-407">**在 Visual Basic 中使用 CallerState**</span><span class="sxs-lookup"><span data-stu-id="5692e-407">**Using CallerState in Visual Basic**</span></span>

[!code-vb[Main](hubs-api-guide-server/samples/sample60.vb)]

<a id="handleErrors"></a>

## <a name="how-to-handle-errors-in-the-hub-class"></a><span data-ttu-id="5692e-408">如何處理中樞類別中的錯誤</span><span class="sxs-lookup"><span data-stu-id="5692e-408">How to handle errors in the Hub class</span></span>

<span data-ttu-id="5692e-409">若要處理中樞類別方法中發生的錯誤，請先確定您已使用 `await`「觀察」非同步作業的任何例外狀況（例如叫用用戶端方法）。</span><span class="sxs-lookup"><span data-stu-id="5692e-409">To handle errors that occur in your Hub class methods, first ensure you "observe" any exceptions from async operations (such as invoking client methods) by using `await`.</span></span> <span data-ttu-id="5692e-410">然後，使用下列一或多個方法：</span><span class="sxs-lookup"><span data-stu-id="5692e-410">Then use one or more of the following methods:</span></span>

- <span data-ttu-id="5692e-411">在 try-catch 區塊中包裝您的方法程式碼，並記錄例外狀況物件。</span><span class="sxs-lookup"><span data-stu-id="5692e-411">Wrap your method code in try-catch blocks and log the exception object.</span></span> <span data-ttu-id="5692e-412">基於調試目的，您可以將例外狀況傳送給用戶端，但基於安全性考慮，不建議將詳細資訊傳送至生產環境中的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-412">For debugging purposes you can send the exception to the client, but for security reasons sending detailed information to clients in production is not recommended.</span></span>
- <span data-ttu-id="5692e-413">建立中樞管線模組來處理[OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-413">Create a Hubs pipeline module that handles the [OnIncomingError](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubpipelinemodule.onincomingerror(v=vs.111).aspx) method.</span></span> <span data-ttu-id="5692e-414">下列範例顯示的管線模組會記錄錯誤，後面接著 Startup.cs 中的程式碼，將模組插入中樞管線。</span><span class="sxs-lookup"><span data-stu-id="5692e-414">The following example shows a pipeline module that logs errors, followed by code in Startup.cs that injects the module into the Hubs pipeline.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample61.cs)]

    [!code-csharp[Main](hubs-api-guide-server/samples/sample62.cs?highlight=4)]
- <span data-ttu-id="5692e-415">使用 `HubException` 類別（在 SignalR 2 中引進）。</span><span class="sxs-lookup"><span data-stu-id="5692e-415">Use the `HubException` class (introduced in SignalR 2).</span></span> <span data-ttu-id="5692e-416">此錯誤可能會從任何中樞叫用擲回。</span><span class="sxs-lookup"><span data-stu-id="5692e-416">This error can be thrown from any hub invocation.</span></span> <span data-ttu-id="5692e-417">`HubError` 的函式會接受字串訊息，並使用物件來儲存額外的錯誤資料。</span><span class="sxs-lookup"><span data-stu-id="5692e-417">The `HubError` constructor takes a string message, and an object for storing extra error data.</span></span> <span data-ttu-id="5692e-418">SignalR 會自動將例外狀況序列化，並將它傳送至用戶端，其將用來拒絕或失敗中樞方法叫用。</span><span class="sxs-lookup"><span data-stu-id="5692e-418">SignalR will auto-serialize the exception and send it to the client, where it will be used to reject or fail the hub method invocation.</span></span>

    <span data-ttu-id="5692e-419">下列程式碼範例示範如何在中樞叫用期間擲回 `HubException`，以及如何處理 JavaScript 和 .NET 用戶端上的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="5692e-419">The following code samples demonstrate how to throw a `HubException` during a Hub invocation, and how to handle the exception on JavaScript and .NET clients.</span></span>

    <span data-ttu-id="5692e-420">**示範 HubException 類別的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="5692e-420">**Server code demonstrating the HubException class**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample63.cs)]

    <span data-ttu-id="5692e-421">**示範回應以在中樞中擲回 HubException 的 JavaScript 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="5692e-421">**JavaScript client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-html[Main](hubs-api-guide-server/samples/sample64.html)]

    <span data-ttu-id="5692e-422">**示範回應以在中樞中擲回 HubException 的 .NET 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="5692e-422">**.NET client code demonstrating response to throwing a HubException in a hub**</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample65.cs)]

<span data-ttu-id="5692e-423">如需中樞管線模組的詳細資訊，請參閱本主題稍後的[如何自訂中樞管線](#hubpipeline)。</span><span class="sxs-lookup"><span data-stu-id="5692e-423">For more information about Hub pipeline modules, see [How to customize the Hubs pipeline](#hubpipeline) later in this topic.</span></span>

<a id="tracing"></a>

## <a name="how-to-enable-tracing"></a><span data-ttu-id="5692e-424">如何啟用追蹤</span><span class="sxs-lookup"><span data-stu-id="5692e-424">How to enable tracing</span></span>

<span data-ttu-id="5692e-425">若要啟用伺服器端追蹤，請將 system.servicemodel 元素新增至 web.config 檔案，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="5692e-425">To enable server-side tracing, add a system.diagnostics element to your Web.config file, as shown in this example:</span></span>

[!code-html[Main](hubs-api-guide-server/samples/sample66.html?highlight=17-72)]

<span data-ttu-id="5692e-426">當您在 Visual Studio 中執行應用程式時，可以在 [**輸出**] 視窗中查看記錄。</span><span class="sxs-lookup"><span data-stu-id="5692e-426">When you run the application in Visual Studio, you can view the logs in the **Output** window.</span></span>

<a id="callfromoutsidehub"></a>

## <a name="how-to-call-client-methods-and-manage-groups-from-outside-the-hub-class"></a><span data-ttu-id="5692e-427">如何從中樞類別外部呼叫用戶端方法和管理群組</span><span class="sxs-lookup"><span data-stu-id="5692e-427">How to call client methods and manage groups from outside the Hub class</span></span>

<span data-ttu-id="5692e-428">若要從不同于中樞類別的類別呼叫用戶端方法，請取得中樞之 SignalR 內容物件的參考，並使用它來呼叫用戶端上的方法或管理群組。</span><span class="sxs-lookup"><span data-stu-id="5692e-428">To call client methods from a different class than your Hub class, get a reference to the SignalR context object for the Hub and use that to call methods on the client or manage groups.</span></span>

<span data-ttu-id="5692e-429">下列範例 `StockTicker` 類別會取得內容物件、將它儲存在類別的實例中、將類別實例儲存在靜態屬性中，然後使用單一類別實例的內容，在連線到名為 `StockTickerHub`之中樞的用戶端上呼叫 `updateStockPrice` 方法。</span><span class="sxs-lookup"><span data-stu-id="5692e-429">The following sample `StockTicker` class gets the context object, stores it in an instance of the class, stores the class instance in a static property, and uses the context from the singleton class instance to call the `updateStockPrice` method on clients that are connected to a Hub named `StockTickerHub`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample67.cs?highlight=8,24)]

<span data-ttu-id="5692e-430">如果您需要在長時間的物件中多次使用內容，請取得參考一次並加以儲存，而不是每次都重新取得。</span><span class="sxs-lookup"><span data-stu-id="5692e-430">If you need to use the context multiple-times in a long-lived object, get the reference once and save it rather than getting it again each time.</span></span> <span data-ttu-id="5692e-431">取得內容一次，可確保 SignalR 會以中樞方法進行用戶端方法調用的相同順序，將訊息傳送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-431">Getting the context once ensures that SignalR sends messages to clients in the same sequence in which your Hub methods make client method invocations.</span></span> <span data-ttu-id="5692e-432">如需說明如何使用中樞之 SignalR 內容的教學課程，請參閱[使用 ASP.NET SignalR 的伺服器廣播](../getting-started/tutorial-server-broadcast-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="5692e-432">For a tutorial that shows how to use the SignalR context for a Hub, see [Server Broadcast with ASP.NET SignalR](../getting-started/tutorial-server-broadcast-with-signalr.md).</span></span>

<a id="callingclientsoutsidehub"></a>

### <a name="calling-client-methods"></a><span data-ttu-id="5692e-433">呼叫用戶端方法</span><span class="sxs-lookup"><span data-stu-id="5692e-433">Calling client methods</span></span>

<span data-ttu-id="5692e-434">您可以指定要接收 RPC 的用戶端，但是您的選項會比從中樞類別呼叫時少。</span><span class="sxs-lookup"><span data-stu-id="5692e-434">You can specify which clients will receive the RPC, but you have fewer options than when you call from a Hub class.</span></span> <span data-ttu-id="5692e-435">這是因為內容不會與用戶端的特定呼叫相關聯，因此任何需要知道目前連接識別碼（例如 `Clients.Others`或 `Clients.Caller`或 `Clients.OthersInGroup`）的方法都無法使用。</span><span class="sxs-lookup"><span data-stu-id="5692e-435">The reason for this is that the context is not associated with a particular call from a client, so any methods that require knowledge of the current connection ID, such as `Clients.Others`, or `Clients.Caller`, or `Clients.OthersInGroup`, are not available.</span></span> <span data-ttu-id="5692e-436">有下列選項可供使用：</span><span class="sxs-lookup"><span data-stu-id="5692e-436">The following options are available:</span></span>

- <span data-ttu-id="5692e-437">所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-437">All connected clients.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample68.cs)]
- <span data-ttu-id="5692e-438">連接識別碼所識別的特定用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-438">A specific client identified by connection ID.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample69.css)]
- <span data-ttu-id="5692e-439">所有已連線的用戶端，但指定的用戶端除外，但由連接識別碼識別。</span><span class="sxs-lookup"><span data-stu-id="5692e-439">All connected clients except the specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample70.cs)]
- <span data-ttu-id="5692e-440">指定群組中所有已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="5692e-440">All connected clients in a specified group.</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample71.css)]
- <span data-ttu-id="5692e-441">指定群組中的所有已連線用戶端，但指定的用戶端除外，由連接識別碼識別。</span><span class="sxs-lookup"><span data-stu-id="5692e-441">All connected clients in a specified group except specified clients, identified by connection ID.</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample72.cs)]

<span data-ttu-id="5692e-442">如果您是從中樞類別中的方法呼叫非中樞類別，您可以傳入目前的連接識別碼，並搭配 `Clients.Client`、`Clients.AllExcept`或 `Clients.Group` 來模擬 `Clients.Caller`、`Clients.Others`或 `Clients.OthersInGroup`。</span><span class="sxs-lookup"><span data-stu-id="5692e-442">If you are calling into your non-Hub class from methods in your Hub class, you can pass in the current connection ID and use that with `Clients.Client`, `Clients.AllExcept`, or `Clients.Group` to simulate `Clients.Caller`, `Clients.Others`, or `Clients.OthersInGroup`.</span></span> <span data-ttu-id="5692e-443">在下列範例中，`MoveShapeHub` 類別會將連接識別碼傳遞給 `Broadcaster` 類別，讓 `Broadcaster` 類別可以模擬 `Clients.Others`。</span><span class="sxs-lookup"><span data-stu-id="5692e-443">In the following example, the `MoveShapeHub` class passes the connection ID to the `Broadcaster` class so that the `Broadcaster` class can simulate `Clients.Others`.</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample73.cs?highlight=12,36)]

<a id="managinggroupsoutsidehub"></a>

### <a name="managing-group-membership"></a><span data-ttu-id="5692e-444">管理群組成員資格</span><span class="sxs-lookup"><span data-stu-id="5692e-444">Managing group membership</span></span>

<span data-ttu-id="5692e-445">針對管理群組，您擁有的選項與在中樞類別中的相同。</span><span class="sxs-lookup"><span data-stu-id="5692e-445">For managing groups you have the same options as you do in a Hub class.</span></span>

- <span data-ttu-id="5692e-446">將用戶端新增至群組</span><span class="sxs-lookup"><span data-stu-id="5692e-446">Add a client to a group</span></span>

    [!code-csharp[Main](hubs-api-guide-server/samples/sample74.cs)]
- <span data-ttu-id="5692e-447">從群組移除用戶端</span><span class="sxs-lookup"><span data-stu-id="5692e-447">Remove a client from a group</span></span>

    [!code-css[Main](hubs-api-guide-server/samples/sample75.css)]

<a id="hubpipeline"></a>

## <a name="how-to-customize-the-hubs-pipeline"></a><span data-ttu-id="5692e-448">如何自訂中樞管線</span><span class="sxs-lookup"><span data-stu-id="5692e-448">How to customize the Hubs pipeline</span></span>

<span data-ttu-id="5692e-449">SignalR 可讓您將自己的程式碼插入中樞管線。</span><span class="sxs-lookup"><span data-stu-id="5692e-449">SignalR enables you to inject your own code into the Hub pipeline.</span></span> <span data-ttu-id="5692e-450">下列範例顯示的自訂中樞管線模組，會記錄從用戶端接收的每個傳入方法呼叫，以及在用戶端上叫用的傳出方法呼叫：</span><span class="sxs-lookup"><span data-stu-id="5692e-450">The following example shows a custom Hub pipeline module that logs each incoming method call received from the client and outgoing method call invoked on the client:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample76.cs)]

<span data-ttu-id="5692e-451">*Startup.cs*檔案中的下列程式碼會註冊要在中樞管線中執行的模組：</span><span class="sxs-lookup"><span data-stu-id="5692e-451">The following code in the *Startup.cs* file registers the module to run in the Hub pipeline:</span></span>

[!code-csharp[Main](hubs-api-guide-server/samples/sample77.cs?highlight=3)]

<span data-ttu-id="5692e-452">有許多不同的方法可以覆寫。</span><span class="sxs-lookup"><span data-stu-id="5692e-452">There are many different methods that you can override.</span></span> <span data-ttu-id="5692e-453">如需完整清單，請參閱[HubPipelineModule 方法](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="5692e-453">For a complete list, see [HubPipelineModule Methods](https://msdn.microsoft.com/library/jj918633(v=vs.111).aspx).</span></span>
