---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR 中樞 API 指南-.NET 用戶端 (C#) |Microsoft Docs
author: bradygaster
description: 本文件提供使用 signalr.NET 用戶端，例如 Windows 市集 (WinRT)、 WPF、 Silverlight 和優缺點比較的第 2 版的中樞 API 的簡介...
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: df12193b6ba3cc8b080047276ed7174583e7ff8a
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054765"
---
<a name="aspnet-signalr-hubs-api-guide---net-client-c"></a><span data-ttu-id="972d0-103">ASP.NET SignalR 中樞 API 指南-.NET 用戶端 (C#)</span><span class="sxs-lookup"><span data-stu-id="972d0-103">ASP.NET SignalR Hubs API Guide - .NET Client (C#)</span></span>
====================

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="972d0-104">本文件提供使用 signalr 第 2 版，.NET 用戶端，例如 Windows 市集 (WinRT)、 WPF、 Silverlight 和主控台應用程式中的中樞 API 的簡介。</span><span class="sxs-lookup"><span data-stu-id="972d0-104">This document provides an introduction to using the Hubs API for SignalR version 2 in .NET clients, such as Windows Store (WinRT), WPF, Silverlight, and console applications.</span></span>
>
> <span data-ttu-id="972d0-105">SignalR 中樞 API 可讓您從伺服器連線的用戶端和伺服器的用戶端進行遠端程序呼叫 (Rpc)。</span><span class="sxs-lookup"><span data-stu-id="972d0-105">The SignalR Hubs API enables you to make remote procedure calls (RPCs) from a server to connected clients and from clients to the server.</span></span> <span data-ttu-id="972d0-106">在伺服器程式碼中，您定義可由用戶端，呼叫的方法，呼叫用戶端執行的方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-106">In server code, you define methods that can be called by clients, and you call methods that run on the client.</span></span> <span data-ttu-id="972d0-107">在用戶端程式碼中，您定義可以在伺服器上，從呼叫的方法，您呼叫在伺服器執行的方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-107">In client code, you define methods that can be called from the server, and you call methods that run on the server.</span></span> <span data-ttu-id="972d0-108">SignalR 會處理所有為您的用戶端-伺服器配管。</span><span class="sxs-lookup"><span data-stu-id="972d0-108">SignalR takes care of all of the client-to-server plumbing for you.</span></span>
>
> <span data-ttu-id="972d0-109">SignalR 也提供一個名為持續連線的較低層級 API。</span><span class="sxs-lookup"><span data-stu-id="972d0-109">SignalR also offers a lower-level API called Persistent Connections.</span></span> <span data-ttu-id="972d0-110">如需 SignalR、 中樞和持續連線，或該教學課程說明如何建置完整的 SignalR 應用程式，請參閱[SignalR-開始使用](../getting-started/index.md)。</span><span class="sxs-lookup"><span data-stu-id="972d0-110">For an introduction to SignalR, Hubs, and Persistent Connections, or for a tutorial that shows how to build a complete SignalR application, see [SignalR - Getting Started](../getting-started/index.md).</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="972d0-111">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="972d0-111">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="972d0-112">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="972d0-112">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)
> - <span data-ttu-id="972d0-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="972d0-113">.NET 4.5</span></span>
> - <span data-ttu-id="972d0-114">SignalR 第 2 版</span><span class="sxs-lookup"><span data-stu-id="972d0-114">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="972d0-115">本主題的上一個版本</span><span class="sxs-lookup"><span data-stu-id="972d0-115">Previous versions of this topic</span></span>
>
> <span data-ttu-id="972d0-116">如需舊版 SignalR 的資訊，請參閱[SignalR 舊版](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="972d0-116">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="972d0-117">提出問題或意見</span><span class="sxs-lookup"><span data-stu-id="972d0-117">Questions and comments</span></span>
>
> <span data-ttu-id="972d0-118">您喜歡本教學課程中的方式，和我們可以改善在頁面底部的註解中，歡迎留下意見反應。</span><span class="sxs-lookup"><span data-stu-id="972d0-118">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="972d0-119">如果您有不直接相關的教學課程中的問題，您可以張貼他們[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或是[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="972d0-119">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="972d0-120">總覽</span><span class="sxs-lookup"><span data-stu-id="972d0-120">Overview</span></span>

<span data-ttu-id="972d0-121">本文件包含下列章節：</span><span class="sxs-lookup"><span data-stu-id="972d0-121">This document contains the following sections:</span></span>

- [<span data-ttu-id="972d0-122">用戶端安裝程式</span><span class="sxs-lookup"><span data-stu-id="972d0-122">Client Setup</span></span>](#clientsetup)
- [<span data-ttu-id="972d0-123">如何建立連線</span><span class="sxs-lookup"><span data-stu-id="972d0-123">How to establish a connection</span></span>](#establishconnection)

    - [<span data-ttu-id="972d0-124">從 Silverlight 用戶端的跨網域連接</span><span class="sxs-lookup"><span data-stu-id="972d0-124">Cross-domain connections from Silverlight clients</span></span>](#slcrossdomain)
- [<span data-ttu-id="972d0-125">如何設定連線</span><span class="sxs-lookup"><span data-stu-id="972d0-125">How to configure the connection</span></span>](#configureconnection)

    - [<span data-ttu-id="972d0-126">如何在 WPF 用戶端設定的並行連線數目上限</span><span class="sxs-lookup"><span data-stu-id="972d0-126">How to set the maximum number of concurrent connections in WPF clients</span></span>](#maxconnections)
    - [<span data-ttu-id="972d0-127">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="972d0-127">How to specify query string parameters</span></span>](#querystring)
    - [<span data-ttu-id="972d0-128">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="972d0-128">How to specify the transport method</span></span>](#transport)
    - [<span data-ttu-id="972d0-129">如何指定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="972d0-129">How to specify HTTP headers</span></span>](#httpheaders)
    - [<span data-ttu-id="972d0-130">如何指定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="972d0-130">How to specify client certificates</span></span>](#clientcertificate)
- [<span data-ttu-id="972d0-131">如何建立中樞 proxy</span><span class="sxs-lookup"><span data-stu-id="972d0-131">How to create the Hub proxy</span></span>](#proxy)
- [<span data-ttu-id="972d0-132">如何定義伺服器可以呼叫用戶端上的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-132">How to define methods on the client that the server can call</span></span>](#callclient)

    - [<span data-ttu-id="972d0-133">不含參數的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-133">Methods without parameters</span></span>](#clientmethodswithoutparms)
    - [<span data-ttu-id="972d0-134">使用指定的參數型別參數的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-134">Methods with parameters, specifying parameter types</span></span>](#clientmethodswithparmtypes)
    - [<span data-ttu-id="972d0-135">具有參數，指定參數的動態物件的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-135">Methods with parameters, specifying dynamic objects for the parameters</span></span>](#clientmethodswithdynamparms)
    - [<span data-ttu-id="972d0-136">如何移除處理常式</span><span class="sxs-lookup"><span data-stu-id="972d0-136">How to remove a handler</span></span>](#removehandler)
- [<span data-ttu-id="972d0-137">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="972d0-137">How to call server methods from the client</span></span>](#callserver)
- [<span data-ttu-id="972d0-138">如何處理連接的存留期事件</span><span class="sxs-lookup"><span data-stu-id="972d0-138">How to handle connection lifetime events</span></span>](#connectionlifetime)
- [<span data-ttu-id="972d0-139">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="972d0-139">How to handle errors</span></span>](#handleerrors)
- [<span data-ttu-id="972d0-140">如何啟用用戶端記錄</span><span class="sxs-lookup"><span data-stu-id="972d0-140">How to enable client-side logging</span></span>](#logging)
- [<span data-ttu-id="972d0-141">WPF、 Silverlight 和主控台應用程式的程式碼可以呼叫伺服器的用戶端方法的範例</span><span class="sxs-lookup"><span data-stu-id="972d0-141">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>](#wpfsl)

<span data-ttu-id="972d0-142">範例.NET 用戶端專案，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="972d0-142">For a sample .NET client projects, see the following resources:</span></span>

- <span data-ttu-id="972d0-143">[gustavo armenta / SignalR 範例](https://github.com/gustavo-armenta/SignalR-Samples)github.com （WinRT，Silverlight 中的主控台應用程式範例）。</span><span class="sxs-lookup"><span data-stu-id="972d0-143">[gustavo-armenta / SignalR-Samples](https://github.com/gustavo-armenta/SignalR-Samples) on GitHub.com (WinRT, Silverlight, console app examples).</span></span>
- <span data-ttu-id="972d0-144">[DamianEdwards / SignalR MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) github.com （WPF 範例）。</span><span class="sxs-lookup"><span data-stu-id="972d0-144">[DamianEdwards / SignalR-MoveShapeDemo / MoveShape.Desktop](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) on GitHub.com (WPF example).</span></span>
- <span data-ttu-id="972d0-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) github.com （主控台應用程式範例）。</span><span class="sxs-lookup"><span data-stu-id="972d0-145">[SignalR / Microsoft.AspNet.SignalR.Client.Samples](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) on GitHub.com (Console app example).</span></span>

<span data-ttu-id="972d0-146">如需如何撰寫程式的伺服器或 JavaScript 用戶端的文件，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="972d0-146">For documentation on how to program the server or JavaScript clients, see the following resources:</span></span>

- [<span data-ttu-id="972d0-147">SignalR 中樞 API 指南-伺服器</span><span class="sxs-lookup"><span data-stu-id="972d0-147">SignalR Hubs API Guide - Server</span></span>](hubs-api-guide-server.md)
- [<span data-ttu-id="972d0-148">SignalR 中樞 API 指南-JavaScript 用戶端</span><span class="sxs-lookup"><span data-stu-id="972d0-148">SignalR Hubs API Guide - JavaScript Client</span></span>](hubs-api-guide-javascript-client.md)

<span data-ttu-id="972d0-149">API 參考主題的連結是 API 的.NET 4.5 版本。</span><span class="sxs-lookup"><span data-stu-id="972d0-149">Links to API Reference topics are to the .NET 4.5 version of the API.</span></span> <span data-ttu-id="972d0-150">如果您使用.NET 4，請參閱[API 主題的.NET 4 版本](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="972d0-150">If you're using .NET 4, see [the .NET 4 version of the API topics](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx).</span></span>

<a id="clientsetup"></a>

## <a name="client-setup"></a><span data-ttu-id="972d0-151">用戶端安裝程式</span><span class="sxs-lookup"><span data-stu-id="972d0-151">Client setup</span></span>

<span data-ttu-id="972d0-152">安裝[Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet 套件 (不[Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)封裝)。</span><span class="sxs-lookup"><span data-stu-id="972d0-152">Install the [Microsoft.AspNet.SignalR.Client](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client) NuGet package (not the [Microsoft.AspNet.SignalR](http://nuget.org/packages/microsoft.aspnet.signalr) package).</span></span> <span data-ttu-id="972d0-153">此套件支援 WinRT、 Silverlight、 WPF、 主控台應用程式和 Windows Phone 用戶端，.NET 4 和.NET 4.5。</span><span class="sxs-lookup"><span data-stu-id="972d0-153">This package supports WinRT, Silverlight, WPF, console application, and Windows Phone clients, for both .NET 4 and .NET 4.5.</span></span>

<span data-ttu-id="972d0-154">如果您尚未在伺服器的版本不同 SignalR 用戶端上所擁有的版本，SignalR 是通常能夠適應差異。</span><span class="sxs-lookup"><span data-stu-id="972d0-154">If the version of SignalR that you have on the client is different from the version that you have on the server, SignalR is often able to adapt to the difference.</span></span> <span data-ttu-id="972d0-155">例如，具有 1.1.x 安裝用戶端，以及具有版本 2 安裝的用戶端，將支援執行 SignalR 第 2 版的伺服器。</span><span class="sxs-lookup"><span data-stu-id="972d0-155">For example, a server running SignalR version 2 will support clients that have 1.1.x installed as well as clients that have version 2 installed.</span></span> <span data-ttu-id="972d0-156">如果伺服器上的版本與用戶端上的版本之間的差異是太大，或如果用戶端比伺服器更新時，會擲回 SignalR`InvalidOperationException`用戶端會嘗試建立連接時的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="972d0-156">If the difference between the version on the server and the version on the client is too great, or if the client is newer than the server, SignalR throws an `InvalidOperationException` exception when the client tries to establish a connection.</span></span> <span data-ttu-id="972d0-157">錯誤訊息是 「`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`"。</span><span class="sxs-lookup"><span data-stu-id="972d0-157">The error message is "`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`".</span></span>

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a><span data-ttu-id="972d0-158">如何建立連線</span><span class="sxs-lookup"><span data-stu-id="972d0-158">How to establish a connection</span></span>

<span data-ttu-id="972d0-159">您可以建立連線之前，您必須建立`HubConnection`物件，並建立 proxy。</span><span class="sxs-lookup"><span data-stu-id="972d0-159">Before you can establish a connection, you have to create a `HubConnection` object and create a proxy.</span></span> <span data-ttu-id="972d0-160">若要建立連線，呼叫`Start`方法`HubConnection`物件。</span><span class="sxs-lookup"><span data-stu-id="972d0-160">To establish the connection, call the `Start` method on the `HubConnection` object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,4)]

> [!NOTE]
> <span data-ttu-id="972d0-161">您必須註冊至少一個事件處理常式，然後再呼叫 JavaScript 用戶端`Start`方法來建立連線。</span><span class="sxs-lookup"><span data-stu-id="972d0-161">For JavaScript clients you have to register at least one event handler before calling the `Start` method to establish the connection.</span></span> <span data-ttu-id="972d0-162">這是不必要的.NET 用戶端。</span><span class="sxs-lookup"><span data-stu-id="972d0-162">This is not necessary for .NET clients.</span></span> <span data-ttu-id="972d0-163">JavaScript 的用戶端，產生的 proxy 程式碼會自動建立存在的所有主機的 proxy 的伺服器上，以及您該如何指出哪一個中樞註冊的處理常式是您的用戶端想要使用。</span><span class="sxs-lookup"><span data-stu-id="972d0-163">For JavaScript clients, the generated proxy code automatically creates proxies for all Hubs that exist on the server, and registering a handler is how you indicate which Hubs your client intends to use.</span></span> <span data-ttu-id="972d0-164">但.NET 用戶端您中樞 proxy 手動建立，因此 SignalR 假設您將會使用任何中樞所建立的 proxy。</span><span class="sxs-lookup"><span data-stu-id="972d0-164">But for a .NET client you create Hub proxies manually, so SignalR assumes that you will be using any Hub that you create a proxy for.</span></span>


<span data-ttu-id="972d0-165">範例程式碼會使用預設值"/ signalr 」 來連線到您的 SignalR 服務的 URL。</span><span class="sxs-lookup"><span data-stu-id="972d0-165">The sample code uses the default "/signalr" URL to connect to your SignalR service.</span></span> <span data-ttu-id="972d0-166">如需有關如何指定不同的基底 URL 的資訊，請參閱 < [ASP.NET SignalR 中樞 API 指南-Server-/signalr URL](hubs-api-guide-server.md#signalrurl)。</span><span class="sxs-lookup"><span data-stu-id="972d0-166">For information about how to specify a different base URL, see [ASP.NET SignalR Hubs API Guide - Server - The /signalr URL](hubs-api-guide-server.md#signalrurl).</span></span>

<span data-ttu-id="972d0-167">`Start`方法以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="972d0-167">The `Start` method executes asynchronously.</span></span> <span data-ttu-id="972d0-168">若要確定接下來的幾行程式碼不執行直到連線建立之後，請使用`await`在 ASP.NET 4.5 的非同步方法或`.Wait()`同步方法中。</span><span class="sxs-lookup"><span data-stu-id="972d0-168">To make sure that subsequent lines of code don't execute until after the connection is established, use `await` in an ASP.NET 4.5 asynchronous method or `.Wait()` in a synchronous method.</span></span> <span data-ttu-id="972d0-169">請勿使用`.Wait()`WinRT 用戶端中。</span><span class="sxs-lookup"><span data-stu-id="972d0-169">Don't use `.Wait()` in a WinRT client.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a><span data-ttu-id="972d0-170">從 Silverlight 用戶端的跨網域連接</span><span class="sxs-lookup"><span data-stu-id="972d0-170">Cross-domain connections from Silverlight clients</span></span>

<span data-ttu-id="972d0-171">如需如何啟用從 Silverlight 用戶端的跨網域連接資訊，請參閱[讓服務提供跨網域界限](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。</span><span class="sxs-lookup"><span data-stu-id="972d0-171">For information about how to enable cross-domain connections from Silverlight clients, see [Making a Service Available Across Domain Boundaries](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx).</span></span>

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a><span data-ttu-id="972d0-172">如何設定連線</span><span class="sxs-lookup"><span data-stu-id="972d0-172">How to configure the connection</span></span>

<span data-ttu-id="972d0-173">建立連線之前，您可以指定任何下列選項：</span><span class="sxs-lookup"><span data-stu-id="972d0-173">Before you establish a connection, you can specify any of the following options:</span></span>

- <span data-ttu-id="972d0-174">並行連線限制。</span><span class="sxs-lookup"><span data-stu-id="972d0-174">Concurrent connections limit.</span></span>
- <span data-ttu-id="972d0-175">查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="972d0-175">Query string parameters.</span></span>
- <span data-ttu-id="972d0-176">傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-176">The transport method.</span></span>
- <span data-ttu-id="972d0-177">HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="972d0-177">HTTP headers.</span></span>
- <span data-ttu-id="972d0-178">用戶端憑證。</span><span class="sxs-lookup"><span data-stu-id="972d0-178">Client certificates.</span></span>

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a><span data-ttu-id="972d0-179">如何在 WPF 用戶端設定的並行連線數目上限</span><span class="sxs-lookup"><span data-stu-id="972d0-179">How to set the maximum number of concurrent connections in WPF clients</span></span>

<span data-ttu-id="972d0-180">在 WPF 用戶端，您可能增加的預設值為 2 的並行連線數目上限。</span><span class="sxs-lookup"><span data-stu-id="972d0-180">In WPF clients, you might have to increase the maximum number of concurrent connections from its default value of 2.</span></span> <span data-ttu-id="972d0-181">建議的值為 10。</span><span class="sxs-lookup"><span data-stu-id="972d0-181">The recommended value is 10.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=4)]

<span data-ttu-id="972d0-182">如需詳細資訊，請參閱 < [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。</span><span class="sxs-lookup"><span data-stu-id="972d0-182">For more information, see [ServicePointManager.DefaultConnectionLimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx).</span></span>

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a><span data-ttu-id="972d0-183">如何指定查詢字串參數</span><span class="sxs-lookup"><span data-stu-id="972d0-183">How to specify query string parameters</span></span>

<span data-ttu-id="972d0-184">如果您想要將資料傳送至伺服器，用戶端連線時，您可以加入連接物件來查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="972d0-184">If you want to send data to the server when the client connects, you can add query string parameters to the connection object.</span></span> <span data-ttu-id="972d0-185">下列範例會示範如何在用戶端程式碼中設定查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="972d0-185">The following example shows how to set a query string parameter in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

<span data-ttu-id="972d0-186">下列範例示範如何讀取伺服器程式碼中的查詢字串參數。</span><span class="sxs-lookup"><span data-stu-id="972d0-186">The following example shows how to read a query string parameter in server code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a><span data-ttu-id="972d0-187">如何指定傳輸方法</span><span class="sxs-lookup"><span data-stu-id="972d0-187">How to specify the transport method</span></span>

<span data-ttu-id="972d0-188">連接的程序的一部分，通常與伺服器，以判斷最佳傳輸所支援的伺服器和用戶端交涉，SignalR 用戶端。</span><span class="sxs-lookup"><span data-stu-id="972d0-188">As part of the process of connecting, a SignalR client normally negotiates with the server to determine the best transport that is supported by both server and client.</span></span> <span data-ttu-id="972d0-189">如果您已經知道您想要使用哪一個的傳輸，您可以略過此協商處理。</span><span class="sxs-lookup"><span data-stu-id="972d0-189">If you already know which transport you want to use, you can bypass this negotiation process.</span></span> <span data-ttu-id="972d0-190">若要指定的傳輸方法，傳入的傳輸物件的 Start 方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-190">To specify the transport method, pass in a transport object to the Start method.</span></span> <span data-ttu-id="972d0-191">下列範例示範如何在用戶端程式碼中指定的傳輸方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-191">The following example shows how to specify the transport method in client code.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=4)]

<span data-ttu-id="972d0-192">[Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空間包含下列類別可供您指定的傳輸。</span><span class="sxs-lookup"><span data-stu-id="972d0-192">The [Microsoft.AspNet.SignalR.Client.Transports](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx) namespace includes the following classes that you can use to specify the transport.</span></span>

- <span data-ttu-id="972d0-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="972d0-193">[LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="972d0-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span><span class="sxs-lookup"><span data-stu-id="972d0-194">[ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)</span></span>
- <span data-ttu-id="972d0-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) （只有時才能使用伺服器和用戶端使用.NET 4.5。）</span><span class="sxs-lookup"><span data-stu-id="972d0-195">[WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) (Available only when both server and client use .NET 4.5.)</span></span>
- <span data-ttu-id="972d0-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) （會自動選擇最佳用戶端和伺服器所支援的傳輸。</span><span class="sxs-lookup"><span data-stu-id="972d0-196">[AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) (Automatically chooses the best transport that is supported by both the client and the server.</span></span> <span data-ttu-id="972d0-197">這是預設的傳輸。</span><span class="sxs-lookup"><span data-stu-id="972d0-197">This is the default transport.</span></span> <span data-ttu-id="972d0-198">這在以傳遞`Start`方法有相同的效果不傳遞任何項目。)</span><span class="sxs-lookup"><span data-stu-id="972d0-198">Passing this in to the `Start` method has the same effect as not passing in anything.)</span></span>

<span data-ttu-id="972d0-199">ForeverFrame 傳輸不會包含這份清單中，因為它僅供瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="972d0-199">The ForeverFrame transport is not included in this list because it is used only by browsers.</span></span>

<span data-ttu-id="972d0-200">如需如何檢查伺服端程式碼中的傳輸方法的資訊，請參閱[ASP.NET SignalR 中樞 API 指南-Server-如何取得用戶端的資訊，從內容屬性](hubs-api-guide-server.md#contextproperty)。</span><span class="sxs-lookup"><span data-stu-id="972d0-200">For information about how to check the transport method in server code, see [ASP.NET SignalR Hubs API Guide - Server - How to get information about the client from the Context property](hubs-api-guide-server.md#contextproperty).</span></span> <span data-ttu-id="972d0-201">如需有關傳輸與後援的詳細資訊，請參閱[SignalR-傳輸和後援簡介](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="972d0-201">For more information about transports and fallbacks, see [Introduction to SignalR - Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a><span data-ttu-id="972d0-202">如何指定 HTTP 標頭</span><span class="sxs-lookup"><span data-stu-id="972d0-202">How to specify HTTP headers</span></span>

<span data-ttu-id="972d0-203">若要設定 HTTP 標頭，使用`Headers`連線物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="972d0-203">To set HTTP headers, use the `Headers` property on the connection object.</span></span> <span data-ttu-id="972d0-204">下列範例示範如何新增 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="972d0-204">The following example shows how to add an HTTP header.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a><span data-ttu-id="972d0-205">如何指定用戶端憑證</span><span class="sxs-lookup"><span data-stu-id="972d0-205">How to specify client certificates</span></span>

<span data-ttu-id="972d0-206">若要新增用戶端憑證，請使用`AddClientCertificate`連線物件上的方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-206">To add client certificates, use the `AddClientCertificate` method on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a><span data-ttu-id="972d0-207">如何建立中樞 proxy</span><span class="sxs-lookup"><span data-stu-id="972d0-207">How to create the Hub proxy</span></span>

<span data-ttu-id="972d0-208">為了定義中樞可以從伺服器呼叫的用戶端上的方法，並叫用中樞，以在伺服器上的方法，來建立中樞的 proxy 呼叫`CreateHubProxy`連線物件上。</span><span class="sxs-lookup"><span data-stu-id="972d0-208">In order to define methods on the client that a Hub can call from the server, and to invoke methods on a Hub at the server, create a proxy for the Hub by calling `CreateHubProxy` on the connection object.</span></span> <span data-ttu-id="972d0-209">字串您傳遞給`CreateHubProxy`是您的中樞類別名稱或所指定的名稱`HubName`屬性如果在伺服器上使用。</span><span class="sxs-lookup"><span data-stu-id="972d0-209">The string you pass in to `CreateHubProxy` is the name of your Hub class, or the name specified by the `HubName` attribute if one was used on the server.</span></span> <span data-ttu-id="972d0-210">名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="972d0-210">Name matching is case-insensitive.</span></span>

<span data-ttu-id="972d0-211">**在伺服器上的中樞類別**</span><span class="sxs-lookup"><span data-stu-id="972d0-211">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

<span data-ttu-id="972d0-212">**建立中樞類別的用戶端 proxy**</span><span class="sxs-lookup"><span data-stu-id="972d0-212">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=2)]

<span data-ttu-id="972d0-213">如果裝飾您的中樞類別與`HubName`屬性，請使用該名稱。</span><span class="sxs-lookup"><span data-stu-id="972d0-213">If you decorate your Hub class with a `HubName` attribute, use that name.</span></span>

<span data-ttu-id="972d0-214">**在伺服器上的中樞類別**</span><span class="sxs-lookup"><span data-stu-id="972d0-214">**Hub class on server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

<span data-ttu-id="972d0-215">**建立中樞類別的用戶端 proxy**</span><span class="sxs-lookup"><span data-stu-id="972d0-215">**Create client proxy for the Hub class**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=2)]

<span data-ttu-id="972d0-216">如果您呼叫`HubConnection.CreateHubProxy`多次使用相同`hubName`，您得到相同的快取`IHubProxy`物件。</span><span class="sxs-lookup"><span data-stu-id="972d0-216">If you call `HubConnection.CreateHubProxy` multiple times with the same `hubName`, you get the same cached `IHubProxy` object.</span></span>

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a><span data-ttu-id="972d0-217">如何定義伺服器可以呼叫用戶端上的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-217">How to define methods on the client that the server can call</span></span>

<span data-ttu-id="972d0-218">若要定義伺服器可以呼叫的方法，使用 proxy 的`On`方法，以註冊事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="972d0-218">To define a method that the server can call, use the proxy's `On` method to register an event handler.</span></span>

<span data-ttu-id="972d0-219">方法名稱比對不區分大小寫。</span><span class="sxs-lookup"><span data-stu-id="972d0-219">Method name matching is case-insensitive.</span></span> <span data-ttu-id="972d0-220">例如，`Clients.All.UpdateStockPrice`伺服器上將會執行`updateStockPrice`， `updatestockprice`，或`UpdateStockPrice`用戶端上。</span><span class="sxs-lookup"><span data-stu-id="972d0-220">For example, `Clients.All.UpdateStockPrice` on the server will execute `updateStockPrice`, `updatestockprice`, or `UpdateStockPrice` on the client.</span></span>

<span data-ttu-id="972d0-221">不同的用戶端平台有不同撰寫方法的程式碼的方式來更新 UI 的需求。</span><span class="sxs-lookup"><span data-stu-id="972d0-221">Different client platforms have different requirements for how you write method code to update the UI.</span></span> <span data-ttu-id="972d0-222">所顯示的範例適用於 WinRT (Windows 市集.NET) 用戶端。</span><span class="sxs-lookup"><span data-stu-id="972d0-222">The examples shown are for WinRT (Windows Store .NET) clients.</span></span> <span data-ttu-id="972d0-223">WPF、 Silverlight 和主控台應用程式範例中提供[本主題稍後的個別區段](#wpfsl)。</span><span class="sxs-lookup"><span data-stu-id="972d0-223">WPF, Silverlight, and console application examples are provided in [a separate section later in this topic](#wpfsl).</span></span>

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a><span data-ttu-id="972d0-224">不含參數的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-224">Methods without parameters</span></span>

<span data-ttu-id="972d0-225">如果您正在處理的方法沒有參數，使用的非泛型多載`On`方法：</span><span class="sxs-lookup"><span data-stu-id="972d0-225">If the method you're handling does not have parameters, use the non-generic overload of the `On` method:</span></span>

<span data-ttu-id="972d0-226">**伺服端程式碼呼叫不含參數的用戶端方法**</span><span class="sxs-lookup"><span data-stu-id="972d0-226">**Server code calling client method without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

<span data-ttu-id="972d0-227">**WinRT 用戶端程式碼，方法呼叫不含參數的伺服器 ([請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="972d0-227">**WinRT Client code for method called from server without parameters ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="972d0-228">使用指定的參數型別參數的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-228">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="972d0-229">如果您正在處理的方法有參數，則指定的參數類型的泛型型別之`On`方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-229">If the method you're handling has parameters, specify the types of the parameters as the generic types of the `On` method.</span></span> <span data-ttu-id="972d0-230">有泛型多載`On`方法，讓您指定最多 8 個參數 (在 Windows Phone 7 上為 4)。</span><span class="sxs-lookup"><span data-stu-id="972d0-230">There are generic overloads of the `On` method to enable you to specify up to 8 parameters (4 on Windows Phone 7).</span></span> <span data-ttu-id="972d0-231">在下列範例中，有一個參數會傳送至`UpdateStockPrice`方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-231">In the following example, one parameter is sent to the `UpdateStockPrice` method.</span></span>

<span data-ttu-id="972d0-232">**伺服端程式碼呼叫具有參數的用戶端方法**</span><span class="sxs-lookup"><span data-stu-id="972d0-232">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

<span data-ttu-id="972d0-233">**參數所用的庫存類別**</span><span class="sxs-lookup"><span data-stu-id="972d0-233">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

<span data-ttu-id="972d0-234">**來自伺服器的參數呼叫方法的 WinRT 用戶端程式碼 ([請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="972d0-234">**WinRT Client code for a method called from server with a parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="972d0-235">具有參數，指定參數的動態物件的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-235">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="972d0-236">做為泛型類型的指定參數的替代方式為`On`方法中，您可以指定參數作為動態物件：</span><span class="sxs-lookup"><span data-stu-id="972d0-236">As an alternative to specifying parameters as generic types of the `On` method, you can specify parameters as dynamic objects:</span></span>

<span data-ttu-id="972d0-237">**伺服端程式碼呼叫具有參數的用戶端方法**</span><span class="sxs-lookup"><span data-stu-id="972d0-237">**Server code calling client method with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

<span data-ttu-id="972d0-238">**參數所用的庫存類別**</span><span class="sxs-lookup"><span data-stu-id="972d0-238">**The Stock class used for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

<span data-ttu-id="972d0-239">**從伺服器參數，使用動態物件的參數呼叫方法的 WinRT 用戶端程式碼 ([請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl))**</span><span class="sxs-lookup"><span data-stu-id="972d0-239">**WinRT Client code for a method called from server with a parameter, using a dynamic object for the parameter ([see WPF and Silverlight examples later in this topic](#wpfsl))**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a><span data-ttu-id="972d0-240">如何移除處理常式</span><span class="sxs-lookup"><span data-stu-id="972d0-240">How to remove a handler</span></span>

<span data-ttu-id="972d0-241">若要移除的處理常式，呼叫其`Dispose`方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-241">To remove a handler, call its `Dispose` method.</span></span>

<span data-ttu-id="972d0-242">**從伺服器呼叫的方法的用戶端程式碼**</span><span class="sxs-lookup"><span data-stu-id="972d0-242">**Client code for a method called from server**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

<span data-ttu-id="972d0-243">**用戶端程式碼，以移除處理常式**</span><span class="sxs-lookup"><span data-stu-id="972d0-243">**Client code to remove the handler**</span></span>

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a><span data-ttu-id="972d0-244">如何從用戶端呼叫伺服器方法</span><span class="sxs-lookup"><span data-stu-id="972d0-244">How to call server methods from the client</span></span>

<span data-ttu-id="972d0-245">若要在伺服器上呼叫方法，使用`Invoke`中樞 proxy 上的方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-245">To call a method on the server, use the `Invoke` method on the Hub proxy.</span></span>

<span data-ttu-id="972d0-246">如果伺服器方法沒有傳回值，請使用非泛型多載`Invoke`方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-246">If the server method has no return value, use the non-generic overload of the `Invoke` method.</span></span>

<span data-ttu-id="972d0-247">**伺服端程式碼沒有傳回值的方法**</span><span class="sxs-lookup"><span data-stu-id="972d0-247">**Server code for a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

<span data-ttu-id="972d0-248">**用戶端程式碼呼叫的方法沒有傳回值，**</span><span class="sxs-lookup"><span data-stu-id="972d0-248">**Client code calling a method that has no return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

<span data-ttu-id="972d0-249">如果伺服器方法的傳回值，指定傳回類型的泛型型別為`Invoke`方法。</span><span class="sxs-lookup"><span data-stu-id="972d0-249">If the server method has a return value, specify the return type as the generic type of the `Invoke` method.</span></span>

<span data-ttu-id="972d0-250">**伺服端程式碼之方法的傳回值，並採用複雜型別參數**</span><span class="sxs-lookup"><span data-stu-id="972d0-250">**Server code for a method that has a return value and takes a complex type parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

<span data-ttu-id="972d0-251">**用於參數和傳回值的庫存類別**</span><span class="sxs-lookup"><span data-stu-id="972d0-251">**The Stock class used for the parameter and return value**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

<span data-ttu-id="972d0-252">**用戶端程式碼呼叫的方法，傳回的值，並採用 ASP.NET 4.5 非同步方法中的複雜型別參數，**</span><span class="sxs-lookup"><span data-stu-id="972d0-252">**Client code calling a method that has a return value and takes a complex type parameter, in an ASP.NET 4.5 async method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

<span data-ttu-id="972d0-253">**用戶端程式碼呼叫的方法，傳回值和同步方法會採用複雜類型的參數，**</span><span class="sxs-lookup"><span data-stu-id="972d0-253">**Client code calling a method that has a return value and takes a complex type parameter, in a synchronous method**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

<span data-ttu-id="972d0-254">`Invoke`方法以非同步方式執行，並傳回`Task`物件。</span><span class="sxs-lookup"><span data-stu-id="972d0-254">The `Invoke` method executes asynchronously and returns a `Task` object.</span></span> <span data-ttu-id="972d0-255">如果您未指定`await`或`.Wait()`，您可以叫用的方法完成執行之前，將會執行下的一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="972d0-255">If you don't specify `await` or `.Wait()`, the next line of code will execute before the method that you invoke has finished executing.</span></span>

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a><span data-ttu-id="972d0-256">如何處理連接的存留期事件</span><span class="sxs-lookup"><span data-stu-id="972d0-256">How to handle connection lifetime events</span></span>

<span data-ttu-id="972d0-257">SignalR 提供以下連線，您可以處理存留期事件：</span><span class="sxs-lookup"><span data-stu-id="972d0-257">SignalR provides the following connection lifetime events that you can handle:</span></span>

- <span data-ttu-id="972d0-258">`Received`：在此連接上收到任何資料時，就會引發。</span><span class="sxs-lookup"><span data-stu-id="972d0-258">`Received`: Raised when any data is received on the connection.</span></span> <span data-ttu-id="972d0-259">提供已接收的資料。</span><span class="sxs-lookup"><span data-stu-id="972d0-259">Provides the received data.</span></span>
- <span data-ttu-id="972d0-260">`ConnectionSlow`：當用戶端偵測到較慢或經常卸除連接時引發。</span><span class="sxs-lookup"><span data-stu-id="972d0-260">`ConnectionSlow`: Raised when the client detects a slow or frequently dropping connection.</span></span>
- <span data-ttu-id="972d0-261">`Reconnecting`：基礎傳輸可讓您開始重新連線時引發。</span><span class="sxs-lookup"><span data-stu-id="972d0-261">`Reconnecting`: Raised when the underlying transport begins reconnecting.</span></span>
- <span data-ttu-id="972d0-262">`Reconnected`：當基礎傳輸已重新連接時引發。</span><span class="sxs-lookup"><span data-stu-id="972d0-262">`Reconnected`: Raised when the underlying transport has reconnected.</span></span>
- <span data-ttu-id="972d0-263">`StateChanged`：連線狀態變更時引發。</span><span class="sxs-lookup"><span data-stu-id="972d0-263">`StateChanged`: Raised when the connection state changes.</span></span> <span data-ttu-id="972d0-264">提供的舊狀態和新的狀態。</span><span class="sxs-lookup"><span data-stu-id="972d0-264">Provides the old state and the new state.</span></span> <span data-ttu-id="972d0-265">如需連線狀態的值請參閱[ConnectionState 列舉](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。</span><span class="sxs-lookup"><span data-stu-id="972d0-265">For information about connection state values see [ConnectionState Enumeration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx).</span></span>
- <span data-ttu-id="972d0-266">`Closed`：當連接已中斷連線時，就會引發。</span><span class="sxs-lookup"><span data-stu-id="972d0-266">`Closed`: Raised when the connection has disconnected.</span></span>

<span data-ttu-id="972d0-267">例如，如果您想要顯示的錯誤，不嚴重，但會造成間歇性連線問題的警告訊息，例如速度很慢或頻繁的連接，卸除處理`ConnectionSlow`事件。</span><span class="sxs-lookup"><span data-stu-id="972d0-267">For example, if you want to display warning messages for errors that are not fatal but cause intermittent connection problems, such as slowness or frequent dropping of the connection, handle the `ConnectionSlow` event.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

<span data-ttu-id="972d0-268">如需詳細資訊，請參閱 <<c0> [ 了解和處理連線存留期事件 SignalR](handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="972d0-268">For more information, see [Understanding and Handling Connection Lifetime Events in SignalR](handling-connection-lifetime-events.md).</span></span>

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a><span data-ttu-id="972d0-269">如何處理錯誤</span><span class="sxs-lookup"><span data-stu-id="972d0-269">How to handle errors</span></span>

<span data-ttu-id="972d0-270">如果您未明確啟用在伺服器上的詳細的錯誤訊息，SignalR 在發生錯誤之後所傳回的例外狀況物件包含有關錯誤的最少資訊。</span><span class="sxs-lookup"><span data-stu-id="972d0-270">If you don't explicitly enable detailed error messages on the server, the exception object that SignalR returns after an error contains minimal information about the error.</span></span> <span data-ttu-id="972d0-271">例如，如果呼叫`newContosoChatMessage`失敗，錯誤物件中的錯誤訊息包含 「`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`」 傳送詳細的錯誤訊息，以在生產環境中的用戶端不會建議基於安全性理由，但如果您想要啟用的詳細的錯誤訊息疑難排解的目的，在伺服器上使用下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="972d0-271">For example, if a call to `newContosoChatMessage` fails, the error message in the error object contains "`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`" Sending detailed error messages to clients in production is not recommended for security reasons, but if you want to enable detailed error messages for troubleshooting purposes, use the following code on the server.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

<span data-ttu-id="972d0-272">若要處理 SignalR 引發的錯誤，您可以加入的處理常式`Error`連線物件上的事件。</span><span class="sxs-lookup"><span data-stu-id="972d0-272">To handle errors that SignalR raises, you can add a handler for the `Error` event on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

<span data-ttu-id="972d0-273">若要處理來自方法引動過程的錯誤，請將程式碼包裝在 try / catch 區塊中。</span><span class="sxs-lookup"><span data-stu-id="972d0-273">To handle errors from method invocations, wrap the code in a try-catch block.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a><span data-ttu-id="972d0-274">如何啟用用戶端記錄</span><span class="sxs-lookup"><span data-stu-id="972d0-274">How to enable client-side logging</span></span>

<span data-ttu-id="972d0-275">若要啟用用戶端記錄，請設定`TraceLevel`和`TraceWriter`連線物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="972d0-275">To enable client-side logging, set the `TraceLevel` and `TraceWriter` properties on the connection object.</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=2-3)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a><span data-ttu-id="972d0-276">WPF、 Silverlight 和主控台應用程式的程式碼可以呼叫伺服器的用戶端方法的範例</span><span class="sxs-lookup"><span data-stu-id="972d0-276">WPF, Silverlight, and console application code samples for client methods that the server can call</span></span>

<span data-ttu-id="972d0-277">稍早所示來定義伺服器可以呼叫的用戶端方法的程式碼範例會套用至 WinRT 用戶端。</span><span class="sxs-lookup"><span data-stu-id="972d0-277">The code samples shown earlier for defining client methods that the server can call apply to WinRT clients.</span></span> <span data-ttu-id="972d0-278">下列範例顯示 WPF、 Silverlight 和主控台應用程式用戶端的對等的程式碼。</span><span class="sxs-lookup"><span data-stu-id="972d0-278">The following samples show the equivalent code for WPF, Silverlight, and console application clients.</span></span>

### <a name="methods-without-parameters"></a><span data-ttu-id="972d0-279">不含參數的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-279">Methods without parameters</span></span>

<span data-ttu-id="972d0-280">**從伺服器不使用參數呼叫方法的 WPF 用戶端程式碼**</span><span class="sxs-lookup"><span data-stu-id="972d0-280">**WPF client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

<span data-ttu-id="972d0-281">**從伺服器不使用參數呼叫方法的 Silverlight 用戶端程式碼**</span><span class="sxs-lookup"><span data-stu-id="972d0-281">**Silverlight client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

<span data-ttu-id="972d0-282">**方法的主控台應用程式用戶端程式碼呼叫不含參數的伺服器**</span><span class="sxs-lookup"><span data-stu-id="972d0-282">**Console application client code for method called from server without parameters**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a><span data-ttu-id="972d0-283">使用指定的參數型別參數的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-283">Methods with parameters, specifying the parameter types</span></span>

<span data-ttu-id="972d0-284">**從伺服器的參數呼叫方法的 WPF 用戶端程式碼**</span><span class="sxs-lookup"><span data-stu-id="972d0-284">**WPF client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

<span data-ttu-id="972d0-285">**從伺服器的參數呼叫方法的 Silverlight 用戶端程式碼**</span><span class="sxs-lookup"><span data-stu-id="972d0-285">**Silverlight client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

<span data-ttu-id="972d0-286">**從具有參數的伺服器呼叫的方法的主控台應用程式用戶端程式碼**</span><span class="sxs-lookup"><span data-stu-id="972d0-286">**Console application client code for a method called from server with a parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a><span data-ttu-id="972d0-287">具有參數，指定參數的動態物件的方法</span><span class="sxs-lookup"><span data-stu-id="972d0-287">Methods with parameters, specifying dynamic objects for the parameters</span></span>

<span data-ttu-id="972d0-288">**從 伺服器參數，使用動態物件的參數呼叫方法的 WPF 用戶端程式碼**</span><span class="sxs-lookup"><span data-stu-id="972d0-288">**WPF client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

<span data-ttu-id="972d0-289">**從 伺服器參數，使用動態物件的參數呼叫方法的 Silverlight 用戶端程式碼**</span><span class="sxs-lookup"><span data-stu-id="972d0-289">**Silverlight client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

<span data-ttu-id="972d0-290">**主控台應用程式用戶端程式碼，從 伺服器參數，使用動態物件的參數呼叫方法**</span><span class="sxs-lookup"><span data-stu-id="972d0-290">**Console application client code for a method called from server with a parameter, using a dynamic object for the parameter**</span></span>

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
