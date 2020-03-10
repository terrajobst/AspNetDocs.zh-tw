---
uid: signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
title: ASP.NET SignalR 中樞 API 指南-.NET 用戶端（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本檔提供在 .NET 用戶端（例如 Windows Store （WinRT）、WPF、Silverlight 和缺點）中使用中樞 API for SignalR 第2版的簡介 。
ms.author: bradyg
ms.date: 04/17/2013
ms.assetid: c334adc3-d6dc-44f3-9f06-f7634475aad3
msc.legacyurl: /signalr/overview/older-versions/signalr-1x-hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: 2b22b53c405a865f91b04e677f60b82dd46dbf9b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623799"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-signalr-1x"></a><span data-ttu-id="d1be5-103">ASP.NET SignalR 中樞 API 指南-.NET 用戶端（SignalR 1.x）</span><span class="sxs-lookup"><span data-stu-id="d1be5-103">ASP.NET SignalR Hubs API Guide - .NET Client (SignalR 1.x)</span></span>

<span data-ttu-id="d1be5-104">由一[Fletcher](https://github.com/pfletcher)， [Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="d1be5-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tom Dykstra](https://github.com/tdykstra)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="d1be5-105">本檔提供在 .NET 用戶端（例如 Windows Store （WinRT）、WPF、Silverlight 和主控台應用程式）中使用適用于 SignalR 第2版之中樞 API 的簡介。</span><span class="sxs-lookup"><span data-stu-id="d1be5-105">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
> 
> <span data-ttu-id="d1be5-106">SignalR 中樞 API 可讓您從伺服器對連線的用戶端，以及從用戶端到伺服器進行遠端程序呼叫（Rpc）。</span><span class="sxs-lookup"><span data-stu-id="d1be5-106">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="d1be5-107">在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-107">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="d1be5-108">在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-108">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="d1be5-109">SignalR 會為您處理所有的用戶端對伺服器管道。</span><span class="sxs-lookup"><span data-stu-id="d1be5-109">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
> 
> <span data-ttu-id="d1be5-110">SignalR 也提供名為「持續連線」的較低層級 API。</span><span class="sxs-lookup"><span data-stu-id="d1be5-110">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="d1be5-111">如需 SignalR、中樞和持續連線的簡介，或顯示如何建立完整 SignalR 應用程式的教學課程，請參閱[SignalR-消費者入門](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-111">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>

## <a name="overview"></a><span data-ttu-id="d1be5-112">概觀</span><span class="sxs-lookup"><span data-stu-id="d1be5-112">Overview</span></span>

<span data-ttu-id="d1be5-113">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="d1be5-113">This document contains the following sections:</span></span>

- [<span data-ttu-id="d1be5-114">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="d1be5-114">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="d1be5-115">如何建立連接</span><span class="sxs-lookup"><span data-stu-id="d1be5-115">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="d1be5-116">Silverlight 用戶端的跨網域連線</span><span class="sxs-lookup"><span data-stu-id="d1be5-116">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="d1be5-117">如何設定連線</span><span class="sxs-lookup"><span data-stu-id="d1be5-117">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="d1be5-118">如何設定 WPF 用戶端中的並行連接數目上限</span><span class="sxs-lookup"><span data-stu-id="d1be5-118">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="d1be5-119">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="d1be5-119">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="d1be5-120">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-120">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="d1be5-121">如何指定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="d1be5-121">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="d1be5-122">如何指定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d1be5-122">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="d1be5-123">如何建立中樞 proxy</span><span class="sxs-lookup"><span data-stu-id="d1be5-123">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="d1be5-124">如何在用戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-124">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="d1be5-125">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-125">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="d1be5-126">具有參數的方法，指定參數類型</span><span class="sxs-lookup"><span data-stu-id="d1be5-126">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="d1be5-127">具有參數的方法，指定參數的動態物件</span><span class="sxs-lookup"><span data-stu-id="d1be5-127">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="d1be5-128">如何移除處理常式</span><span class="sxs-lookup"><span data-stu-id="d1be5-128">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="d1be5-129">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-129">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="d1be5-130">如何處理連接存留期事件</span><span class="sxs-lookup"><span data-stu-id="d1be5-130">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="d1be5-131">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="d1be5-131">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="d1be5-132">如何啟用用戶端記錄</span><span class="sxs-lookup"><span data-stu-id="d1be5-132">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="d1be5-133">伺服器可以呼叫之用戶端方法的 WPF、Silverlight 和主控台應用程式程式碼範例</span><span class="sxs-lookup"><span data-stu-id="d1be5-133">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="d1be5-134">如需範例 .NET 用戶端專案，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="d1be5-134">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="d1be5-135">[gustavo-armenta/SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com （WinRT、Silverlight、主控台應用程式範例）上的範例。</span><span class="sxs-lookup"><span data-stu-id="d1be5-135">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="d1be5-136">GitHub.com 上[的 DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) （WPF 範例）。</span><span class="sxs-lookup"><span data-stu-id="d1be5-136">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="d1be5-137">GitHub.com 上的[SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) （主控台應用程式範例）。</span><span class="sxs-lookup"><span data-stu-id="d1be5-137">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="d1be5-138">如需如何撰寫伺服器或 JavaScript 用戶端程式的相關檔，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="d1be5-138">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="d1be5-139">SignalR 中樞 API 指南-伺服器</span><span class="sxs-lookup"><span data-stu-id="d1be5-139">SignalR Hubs API Guide - Server</span></span>](../guide-to-the-api/hubs-api-guide-server.md)
- [<span data-ttu-id="d1be5-140">SignalR 中樞 API 指南-JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="d1be5-140">SignalR Hubs API Guide - JavaScript Client</span></span>](../guide-to-the-api/hubs-api-guide-javascript-client.md)

<span data-ttu-id="d1be5-141">API 參考主題的連結是針對 .NET 4.5 版的 API。</span><span class="sxs-lookup"><span data-stu-id="d1be5-141">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="d1be5-142">如果您使用的是 .NET 4，請參閱[.net 4 版本的 API 主題](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-142">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="d1be5-143">用戶端設定</span><span class="sxs-lookup"><span data-stu-id="d1be5-143">Client setup</span></span>

<span data-ttu-id="d1be5-144">安裝[SignalR。用戶端](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)NuGet 套件（而不是[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)套件）。</span><span class="sxs-lookup"><span data-stu-id="d1be5-144">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="d1be5-145">此套件支援適用于 .NET 4 和 .NET 4.5 的 WinRT、Silverlight、WPF、主控台應用程式和 Windows Phone 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d1be5-145">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="d1be5-146">如果您在用戶端上擁有的 SignalR 版本與伺服器上的版本不同，SignalR 通常可以適應差異。</span><span class="sxs-lookup"><span data-stu-id="d1be5-146">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="d1be5-147">例如，當 SignalR 版本2.0 發行，而且您將它安裝在伺服器上時，伺服器將支援已安裝 1.1. x 的用戶端，以及已安裝2.0 的用戶端。</span><span class="sxs-lookup"><span data-stu-id="d1be5-147">For example, when SignalR version 2.0 is released and you install that on the server, the server will support clients that have 1.1.x installed as well as clients that have 2.0 installed.</span></span> <span data-ttu-id="d1be5-148">如果伺服器上的版本和用戶端上的版本之間的差異太大，則當用戶端嘗試建立連線時，SignalR 會擲回 `InvalidOperationException` 例外狀況。</span><span class="sxs-lookup"><span data-stu-id="d1be5-148">If the difference between the version on the server and the version on the client is too great, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="d1be5-149">錯誤訊息為「`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`」。</span><span class="sxs-lookup"><span data-stu-id="d1be5-149">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="d1be5-150">如何建立連接</span><span class="sxs-lookup"><span data-stu-id="d1be5-150">How to establish a connection</span></span>

<span data-ttu-id="d1be5-151">建立連接之前，您必須先建立 `HubConnection` 物件，並建立 proxy。</span><span class="sxs-lookup"><span data-stu-id="d1be5-151">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="d1be5-152">若要建立連接，請在 `HubConnection` 物件上呼叫 `Start` 方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-152">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="d1be5-153">針對 JavaScript 用戶端，您必須先註冊至少一個事件處理常式，才能呼叫 `Start` 方法來建立連接。</span><span class="sxs-lookup"><span data-stu-id="d1be5-153">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="d1be5-154">這不是 .NET 用戶端的必要動作。</span><span class="sxs-lookup"><span data-stu-id="d1be5-154">This is not necessary for .NET clients.</span></span> <span data-ttu-id="d1be5-155">針對 JavaScript 用戶端，產生的 proxy 程式碼會自動為存在於伺服器上的所有中樞建立 proxy，而註冊處理常式則是您如何指出用戶端想要使用的中樞。</span><span class="sxs-lookup"><span data-stu-id="d1be5-155">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="d1be5-156">但是針對 .NET 用戶端，您可以手動建立中樞 proxy，因此 SignalR 會假設您將使用為其建立 proxy 的任何中樞。</span><span class="sxs-lookup"><span data-stu-id="d1be5-156">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>

<span data-ttu-id="d1be5-157">範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。</span><span class="sxs-lookup"><span data-stu-id="d1be5-157">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="d1be5-158">如需有關如何指定不同基底 URL 的詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-158">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](../guide-to-the-api/hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="d1be5-159">`Start` 方法會以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="d1be5-159">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="d1be5-160">若要確保在建立連接之後才執行後續的程式程式碼，請使用 ASP.NET 4.5 非同步方法中的 `await`，或在同步方法中 `.Wait()`。</span><span class="sxs-lookup"><span data-stu-id="d1be5-160">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="d1be5-161">請勿在 WinRT 用戶端中使用 `.Wait()`。</span><span class="sxs-lookup"><span data-stu-id="d1be5-161">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<span data-ttu-id="d1be5-162">`HubConnection` 類別是安全執行緒。</span><span class="sxs-lookup"><span data-stu-id="d1be5-162">The `HubConnection` class is thread-safe.</span></span>

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="d1be5-163">Silverlight 用戶端的跨網域連線</span><span class="sxs-lookup"><span data-stu-id="d1be5-163">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="d1be5-164">如需有關如何從 Silverlight 用戶端啟用跨網域連線的詳細資訊，請參閱[讓服務可跨網域界限使用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-164">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="d1be5-165">如何設定連線</span><span class="sxs-lookup"><span data-stu-id="d1be5-165">How to configure the connection</span></span>

<span data-ttu-id="d1be5-166">建立連接之前，您可以指定下列任何選項：</span><span class="sxs-lookup"><span data-stu-id="d1be5-166">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="d1be5-167">同時連接限制。</span><span class="sxs-lookup"><span data-stu-id="d1be5-167">Concurrent connections limit.</span></span>
- <span data-ttu-id="d1be5-168">查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="d1be5-168">Query string parameters.</span></span>
- <span data-ttu-id="d1be5-169">傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-169">The transport method.</span></span>
- <span data-ttu-id="d1be5-170">HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="d1be5-170">HTTP headers.</span></span>
- <span data-ttu-id="d1be5-171">用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="d1be5-171">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="d1be5-172">如何設定 WPF 用戶端中的並行連接數目上限</span><span class="sxs-lookup"><span data-stu-id="d1be5-172">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="d1be5-173">在 WPF 用戶端中，您可能必須從預設值2增加並行連接的最大數目。</span><span class="sxs-lookup"><span data-stu-id="d1be5-173">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="d1be5-174">建議的值是10。</span><span class="sxs-lookup"><span data-stu-id="d1be5-174">The recommended value is 10.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="d1be5-175">如需詳細資訊，請參閱[ServicePointManager. servicepointmanager.defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-175">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="d1be5-176">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="d1be5-176">How to specify query string parameters</span></span>

<span data-ttu-id="d1be5-177">如果您想要在用戶端連接時將資料傳送到伺服器，您可以將查詢字串參數新增至 connection 物件。</span><span class="sxs-lookup"><span data-stu-id="d1be5-177">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="d1be5-178">下列範例說明如何在用戶端程式代碼中設定查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="d1be5-178">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="d1be5-179">下列範例顯示如何讀取伺服器程式碼中的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="d1be5-179">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="d1be5-180">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-180">How to specify the transport method</span></span>

<span data-ttu-id="d1be5-181">在進行連線的過程中，SignalR 用戶端通常會與伺服器協商，以判斷伺服器和用戶端都支援的最佳傳輸。</span><span class="sxs-lookup"><span data-stu-id="d1be5-181">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="d1be5-182">如果您已經知道您想要使用的傳輸，可以略過此協調流程。</span><span class="sxs-lookup"><span data-stu-id="d1be5-182">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="d1be5-183">若要指定傳輸方法，請將傳輸物件傳入 Start 方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-183">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="d1be5-184">下列範例顯示如何在用戶端程式代碼中指定傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-184">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="d1be5-185">[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空間包含下列可供您用來指定傳輸的類別。</span><span class="sxs-lookup"><span data-stu-id="d1be5-185">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="d1be5-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="d1be5-186">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="d1be5-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="d1be5-187">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="d1be5-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) （僅適用于伺服器和用戶端都使用 .net 4.5 時）。</span><span class="sxs-lookup"><span data-stu-id="d1be5-188">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="d1be5-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) （自動選擇用戶端和伺服器所支援的最佳傳輸。</span><span class="sxs-lookup"><span data-stu-id="d1be5-189">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="d1be5-190">這是預設的傳輸。</span><span class="sxs-lookup"><span data-stu-id="d1be5-190">This is the default transport.</span></span> <span data-ttu-id="d1be5-191">將此傳遞至 `Start` 方法，其效果與未傳入任何專案相同。）</span><span class="sxs-lookup"><span data-stu-id="d1be5-191">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="d1be5-192">ForeverFrame 傳輸不包含在這份清單中，因為它僅供瀏覽器使用。</span><span class="sxs-lookup"><span data-stu-id="d1be5-192">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="d1be5-193">如需有關如何在伺服器程式碼中檢查傳輸方法的詳細資訊，請參閱[ASP.NET SignalR HUB API 指南-伺服器-如何從內容屬性取得用戶端的相關資訊](../guide-to-the-api/hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-193">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](../guide-to-the-api/hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="d1be5-194">如需傳輸和回退的詳細資訊，請參閱[SignalR-傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-194">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="d1be5-195">如何指定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="d1be5-195">How to specify HTTP headers</span></span>

<span data-ttu-id="d1be5-196">若要設定 HTTP 標頭，請使用 connection 物件上的 `Headers` 屬性。</span><span class="sxs-lookup"><span data-stu-id="d1be5-196">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="d1be5-197">下列範例顯示如何新增 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="d1be5-197">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="d1be5-198">如何指定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="d1be5-198">How to specify client certificates</span></span>

<span data-ttu-id="d1be5-199">若要新增用戶端憑證，請在 connection 物件上使用 `AddClientCertificate` 方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-199">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="d1be5-200">如何建立中樞 proxy</span><span class="sxs-lookup"><span data-stu-id="d1be5-200">How to create the Hub proxy</span></span>

<span data-ttu-id="d1be5-201">若要在用戶端上定義中樞可以從伺服器呼叫的方法，以及在伺服器上叫用中樞上的方法，請在連線物件上呼叫 `CreateHubProxy`，以建立中樞的 proxy。</span><span class="sxs-lookup"><span data-stu-id="d1be5-201">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="d1be5-202">您傳入 `CreateHubProxy` 的字串是中樞類別的名稱，或是 `HubName` 屬性所指定的名稱（如果伺服器上使用了它）。</span><span class="sxs-lookup"><span data-stu-id="d1be5-202">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="d1be5-203">名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="d1be5-203">Name matching is case-insensitive.</span></span>

<span data-ttu-id="d1be5-204">**伺服器上的中樞類別**</span><span class="sxs-lookup"><span data-stu-id="d1be5-204">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="d1be5-205">**建立中樞類別的用戶端 proxy**</span><span class="sxs-lookup"><span data-stu-id="d1be5-205">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="d1be5-206">如果您以 `HubName` 屬性裝飾中樞類別，請使用該名稱。</span><span class="sxs-lookup"><span data-stu-id="d1be5-206">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="d1be5-207">**伺服器上的中樞類別**</span><span class="sxs-lookup"><span data-stu-id="d1be5-207">**Hub class on server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="d1be5-208">**建立中樞類別的用戶端 proxy**</span><span class="sxs-lookup"><span data-stu-id="d1be5-208">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="d1be5-209">Proxy 物件是安全線程。</span><span class="sxs-lookup"><span data-stu-id="d1be5-209">The proxy object is thread-safe.</span></span> <span data-ttu-id="d1be5-210">事實上，如果您使用相同的 `hubName`多次呼叫 `HubConnection.CreateHubProxy`，就會取得相同的快取 `IHubProxy` 物件。</span><span class="sxs-lookup"><span data-stu-id="d1be5-210">In fact, if you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="d1be5-211">如何在用戶端上定義伺服器可以呼叫的方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-211">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="d1be5-212">若要定義伺服器可以呼叫的方法，請使用 proxy 的 `On` 方法來註冊事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="d1be5-212">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="d1be5-213">方法名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="d1be5-213">Method name matching is case-insensitive.</span></span> <span data-ttu-id="d1be5-214">例如，伺服器上的 `Clients.All.UpdateStockPrice` 將會在用戶端上執行 `updateStockPrice`、`updatestockprice`或 `UpdateStockPrice`。</span><span class="sxs-lookup"><span data-stu-id="d1be5-214">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="d1be5-215">不同的用戶端平臺對於您撰寫方法程式碼來更新 UI 的方式有不同的需求。</span><span class="sxs-lookup"><span data-stu-id="d1be5-215">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="d1be5-216">所顯示的範例適用于 WinRT （Windows Store .NET）用戶端。</span><span class="sxs-lookup"><span data-stu-id="d1be5-216">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="d1be5-217">[本主題稍後的個別章節](#wpfsl)會提供 WPF、Silverlight 和主控台應用程式範例。</span><span class="sxs-lookup"><span data-stu-id="d1be5-217">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="d1be5-218">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-218">Methods without parameters</span></span>

<span data-ttu-id="d1be5-219">如果您要處理的方法沒有參數，請使用 `On` 方法的非泛型多載：</span><span class="sxs-lookup"><span data-stu-id="d1be5-219">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="d1be5-220">**不含參數的伺服器程式碼呼叫用戶端方法**</span><span class="sxs-lookup"><span data-stu-id="d1be5-220">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="d1be5-221">**從沒有參數的伺服器呼叫之方法的 WinRT 用戶端程式代碼（[請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="d1be5-221">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="d1be5-222">具有參數的方法，指定參數類型</span><span class="sxs-lookup"><span data-stu-id="d1be5-222">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="d1be5-223">如果您要處理的方法有參數，請將參數的類型指定為 `On` 方法的泛型型別。</span><span class="sxs-lookup"><span data-stu-id="d1be5-223">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="d1be5-224">`On` 方法的泛型多載，可讓您指定最多8個參數（4 Windows Phone 7）。</span><span class="sxs-lookup"><span data-stu-id="d1be5-224">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="d1be5-225">在下列範例中，會將一個參數傳送至 `UpdateStockPrice` 方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-225">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="d1be5-226">**使用參數呼叫用戶端方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-226">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="d1be5-227">**用於參數的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="d1be5-227">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="d1be5-228">**使用參數從伺服器呼叫之方法的 WinRT 用戶端程式代碼（[請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="d1be5-228">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="d1be5-229">具有參數的方法，指定參數的動態物件</span><span class="sxs-lookup"><span data-stu-id="d1be5-229">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="d1be5-230">除了將參數指定為 `On` 方法的泛型型別之外，您還可以將參數指定為動態物件：</span><span class="sxs-lookup"><span data-stu-id="d1be5-230">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="d1be5-231">**使用參數呼叫用戶端方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-231">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="d1be5-232">**用於參數的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="d1be5-232">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="d1be5-233">**使用參數從伺服器呼叫之方法的 WinRT 用戶端程式代碼（[請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)）**</span><span class="sxs-lookup"><span data-stu-id="d1be5-233">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="d1be5-234">如何移除處理常式</span><span class="sxs-lookup"><span data-stu-id="d1be5-234">How to remove a handler</span></span>

<span data-ttu-id="d1be5-235">若要移除處理常式，請呼叫其 `Dispose` 方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-235">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="d1be5-236">**從伺服器呼叫之方法的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-236">**Client code for a method called from server**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="d1be5-237">**移除處理常式的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-237">**Client code to remove the handler**</span></span>

[!code-css[Main](signalr-1x-hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="d1be5-238">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-238">How to call server methods from the client</span></span>

<span data-ttu-id="d1be5-239">若要在伺服器上呼叫方法，請在中樞 proxy 上使用 `Invoke` 方法。</span><span class="sxs-lookup"><span data-stu-id="d1be5-239">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="d1be5-240">如果伺服器方法沒有傳回值，請使用 `Invoke` 方法的非泛型多載。</span><span class="sxs-lookup"><span data-stu-id="d1be5-240">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="d1be5-241">**沒有傳回值之方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-241">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="d1be5-242">**呼叫沒有傳回值之方法的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-242">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="d1be5-243">如果伺服器方法有傳回值，請將傳回型別指定為 `Invoke` 方法的泛型型別。</span><span class="sxs-lookup"><span data-stu-id="d1be5-243">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="d1be5-244">**具有傳回值並接受複雜型別參數之方法的伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-244">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="d1be5-245">**用於參數和傳回值的 Stock 類別**</span><span class="sxs-lookup"><span data-stu-id="d1be5-245">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="d1be5-246">**在 ASP.NET 4.5 非同步方法中呼叫具有傳回值並採用複雜類型參數的方法的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-246">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="d1be5-247">**在同步方法中呼叫具有傳回值並採用複雜型別參數之方法的用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-247">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="d1be5-248">`Invoke` 方法會以非同步方式執行，並傳回 `Task` 物件。</span><span class="sxs-lookup"><span data-stu-id="d1be5-248">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="d1be5-249">如果您未指定 `await` 或 `.Wait()`，則下一行程式碼會在您叫用的方法完成執行之前執行。</span><span class="sxs-lookup"><span data-stu-id="d1be5-249">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="d1be5-250">如何處理連接存留期事件</span><span class="sxs-lookup"><span data-stu-id="d1be5-250">How to handle connection lifetime events</span></span>

<span data-ttu-id="d1be5-251">SignalR 提供您可以處理的下列連接存留期事件：</span><span class="sxs-lookup"><span data-stu-id="d1be5-251">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="d1be5-252">`Received`：在連接上收到任何資料時引發。</span><span class="sxs-lookup"><span data-stu-id="d1be5-252">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="d1be5-253">提供接收的資料。</span><span class="sxs-lookup"><span data-stu-id="d1be5-253">Provides the received data.</span></span>
- <span data-ttu-id="d1be5-254">`ConnectionSlow`：當用戶端偵測到緩慢或經常中斷的連接時引發。</span><span class="sxs-lookup"><span data-stu-id="d1be5-254">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="d1be5-255">`Reconnecting`：當基礎傳輸開始重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="d1be5-255">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="d1be5-256">`Reconnected`：當基礎傳輸已重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="d1be5-256">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="d1be5-257">`StateChanged`：當連接狀態變更時引發。</span><span class="sxs-lookup"><span data-stu-id="d1be5-257">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="d1be5-258">提供舊狀態和新狀態。</span><span class="sxs-lookup"><span data-stu-id="d1be5-258">Provides the old state and the new state.</span></span> <span data-ttu-id="d1be5-259">如需連接狀態值的詳細資訊，請參閱[ConnectionState 列舉](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-259">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="d1be5-260">`Closed`：當連接中斷連線時引發。</span><span class="sxs-lookup"><span data-stu-id="d1be5-260">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="d1be5-261">例如，如果您想要針對不嚴重的錯誤顯示警告訊息，但造成間歇性的連線問題（例如緩慢或經常卸載連接），則會處理 `ConnectionSlow` 事件。</span><span class="sxs-lookup"><span data-stu-id="d1be5-261">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="d1be5-262">如需詳細資訊，請參閱[瞭解和處理 SignalR 中的連接存留期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="d1be5-262">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="d1be5-263">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="d1be5-263">How to handle errors</span></span>

<span data-ttu-id="d1be5-264">如果您未在伺服器上明確啟用詳細的錯誤訊息，則 SignalR 會在錯誤之後傳回的例外狀況物件包含有關錯誤的最少資訊。</span><span class="sxs-lookup"><span data-stu-id="d1be5-264">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="d1be5-265">例如，如果 `newContosoChatMessage` 的呼叫失敗，錯誤物件中的錯誤訊息就會包含「`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`」將詳細的錯誤訊息傳送給生產環境中的用戶端，基於安全性理由，不建議使用此方法，但如果您想要針對疑難排解目的啟用詳細的錯誤訊息，請在伺服器上使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1be5-265">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="d1be5-266">若要處理 SignalR 引發的錯誤，您可以在 connection 物件上加入 `Error` 事件的處理常式。</span><span class="sxs-lookup"><span data-stu-id="d1be5-266">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="d1be5-267">若要處理方法調用中的錯誤，請將程式碼包裝在 try-catch 區塊中。</span><span class="sxs-lookup"><span data-stu-id="d1be5-267">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="d1be5-268">如何啟用用戶端記錄</span><span class="sxs-lookup"><span data-stu-id="d1be5-268">How to enable client-side logging</span></span>

<span data-ttu-id="d1be5-269">若要啟用用戶端記錄，請在 connection 物件上設定 `TraceLevel` 和 `TraceWriter` 屬性。</span><span class="sxs-lookup"><span data-stu-id="d1be5-269">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="d1be5-270">伺服器可以呼叫之用戶端方法的 WPF、Silverlight 和主控台應用程式程式碼範例</span><span class="sxs-lookup"><span data-stu-id="d1be5-270">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="d1be5-271">先前針對定義伺服器可以呼叫之用戶端方法所顯示的程式碼範例，適用于 WinRT 用戶端。</span><span class="sxs-lookup"><span data-stu-id="d1be5-271">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="d1be5-272">下列範例顯示 WPF、Silverlight 和主控台應用程式用戶端的對等程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1be5-272">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="d1be5-273">沒有參數的方法</span><span class="sxs-lookup"><span data-stu-id="d1be5-273">Methods without parameters</span></span>

<span data-ttu-id="d1be5-274">**從沒有參數的伺服器呼叫之方法的 WPF 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-274">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="d1be5-275">**從沒有參數的伺服器呼叫之方法的 Silverlight 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-275">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="d1be5-276">**從沒有參數的伺服器呼叫之方法的主控台應用程式用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-276">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="d1be5-277">具有參數的方法，指定參數類型</span><span class="sxs-lookup"><span data-stu-id="d1be5-277">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="d1be5-278">**使用參數從伺服器呼叫之方法的 WPF 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-278">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="d1be5-279">**使用參數從伺服器呼叫之方法的 Silverlight 用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-279">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="d1be5-280">**使用參數從伺服器呼叫之方法的主控台應用程式用戶端程式代碼**</span><span class="sxs-lookup"><span data-stu-id="d1be5-280">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="d1be5-281">具有參數的方法，指定參數的動態物件</span><span class="sxs-lookup"><span data-stu-id="d1be5-281">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="d1be5-282">**從伺服器使用參數呼叫之方法的 WPF 用戶端程式代碼，使用參數的動態物件**</span><span class="sxs-lookup"><span data-stu-id="d1be5-282">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="d1be5-283">**從伺服器使用參數呼叫之方法的 Silverlight 用戶端程式代碼，使用參數的動態物件**</span><span class="sxs-lookup"><span data-stu-id="d1be5-283">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="d1be5-284">**從伺服器使用參數呼叫之方法的主控台應用程式用戶端程式代碼，使用參數的動態物件**</span><span class="sxs-lookup"><span data-stu-id="d1be5-284">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](signalr-1x-hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
