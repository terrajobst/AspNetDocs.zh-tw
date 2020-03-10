---
uid: aspnet/overview/owin-and-katana/katana-samples
title: Katana 範例 |Microsoft Docs
author: microsoft
description: ''
ms.author: riande
ms.date: 01/17/2014
ms.assetid: bec04f5d-2638-4417-b288-97c58c8d6379
msc.legacyurl: /aspnet/overview/owin-and-katana/katana-samples
msc.type: authoredcontent
ms.openlocfilehash: 1238f7d09492a6856d49dece5de75184ccfa4838
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584557"
---
# <a name="katana-samples"></a><span data-ttu-id="720c2-102">Katana 範例</span><span class="sxs-lookup"><span data-stu-id="720c2-102">Katana Samples</span></span>

<span data-ttu-id="720c2-103">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="720c2-103">by [Microsoft](https://github.com/microsoft)</span></span>

## <a name="katana-samples"></a><span data-ttu-id="720c2-104">Katana 範例</span><span class="sxs-lookup"><span data-stu-id="720c2-104">Katana Samples</span></span>

<span data-ttu-id="720c2-105">**ASP.NET 路由範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span><span class="sxs-lookup"><span data-stu-id="720c2-105">**ASP.NET Routes Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/AspNetRoutes)</span></span>  
<span data-ttu-id="720c2-106">在某些應用程式中，您會想要將 Asp.Net 路由表中的 OWIN 元件與非 OWIN 元件並存。</span><span class="sxs-lookup"><span data-stu-id="720c2-106">In some applications you will want to hook up OWIN components in the Asp.Net route table side by side with non-OWIN components.</span></span> <span data-ttu-id="720c2-107">這個範例示範如何使用 MapOwinPath 和 MapOwinRoute 所提供的 RouteCollection 擴充方法。</span><span class="sxs-lookup"><span data-stu-id="720c2-107">This sample shows how to use the RouteCollection extension methods MapOwinPath and MapOwinRoute provided by Microsoft.Owin.Host.SystemWeb.</span></span>

<span data-ttu-id="720c2-108">**分支管線範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span><span class="sxs-lookup"><span data-stu-id="720c2-108">**Branching Pipelines Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/BranchingPipelines)</span></span>  
<span data-ttu-id="720c2-109">OWIN 要求處理管線不需要是線性的，它們可以透過不同的方式分支以處理要求。</span><span class="sxs-lookup"><span data-stu-id="720c2-109">OWIN request processing pipelines do not need to be linear, they can be branched to process requests in different ways.</span></span> <span data-ttu-id="720c2-110">這個範例示範如何根據要求路徑或其他要求資料（例如標頭）來建立分支管線。</span><span class="sxs-lookup"><span data-stu-id="720c2-110">This sample shows how to construct a branching pipeline based on request paths or other request data such as headers.</span></span> <span data-ttu-id="720c2-111">這些元件可在 Owin nuget 套件中取得。</span><span class="sxs-lookup"><span data-stu-id="720c2-111">These components are available in the Microsoft.Owin.Mapping nuget package.</span></span>

<span data-ttu-id="720c2-112">**自訂伺服器範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span><span class="sxs-lookup"><span data-stu-id="720c2-112">**Custom Server Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/CustomServer) </span></span>  
<span data-ttu-id="720c2-113">顯示如何在自我裝載 OWIN 時使用自訂 OWIN 伺服器。</span><span class="sxs-lookup"><span data-stu-id="720c2-113">Shows how to use a custom OWIN server when self-hosting OWIN.</span></span>

<span data-ttu-id="720c2-114">**內嵌範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span><span class="sxs-lookup"><span data-stu-id="720c2-114">**Embedded Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/Embedded)</span></span>  
<span data-ttu-id="720c2-115">有些 OWIN 伺服器可在您自己的進程中執行（&quot;自我裝載&quot;）。</span><span class="sxs-lookup"><span data-stu-id="720c2-115">Some OWIN servers can be run inside of your own process (&quot;self-hosted&quot;).</span></span> <span data-ttu-id="720c2-116">這個範例示範如何使用 Owin 所提供的工具來啟動 OWIN 應用程式。</span><span class="sxs-lookup"><span data-stu-id="720c2-116">This sample shows how to start an OWIN application using the tools provided by the Microsoft.Owin.Hosting nuget package.</span></span>

<span data-ttu-id="720c2-117">**HelloWorld 範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span><span class="sxs-lookup"><span data-stu-id="720c2-117">**HelloWorld Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorld)</span></span>  
<span data-ttu-id="720c2-118">OWIN 是一種 HTTP 伺服器 API 抽象概念，可讓您跨各種伺服器進行應用程式可攜性。</span><span class="sxs-lookup"><span data-stu-id="720c2-118">OWIN is a HTTP server API abstraction that enables application portability across various servers.</span></span> <span data-ttu-id="720c2-119">這個範例會示範如何使用一些**簡單的包裝**函式來撰寫 Hello World 的應用程式，並在原始的 OWIN 抽象概念上執行，並在類似 ASP.NET 的 web 伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="720c2-119">This sample demonstrates how to write a Hello World application using some **simple wrappers** around the raw OWIN abstraction and run it on a web server like ASP.NET.</span></span>

<span data-ttu-id="720c2-120">**Hello World 原始 OWIN 範例** | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span><span class="sxs-lookup"><span data-stu-id="720c2-120">**Hello World Raw OWIN Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/HelloWorldRawOwin)</span></span>  
<span data-ttu-id="720c2-121">這個範例會示範如何使用**原始**OWIN 抽象來撰寫 Hello World 應用程式，並在類似 Asp.Net 的 web 伺服器上執行。</span><span class="sxs-lookup"><span data-stu-id="720c2-121">This sample demonstrates how to write a Hello World application using the **raw** OWIN abstraction and run it on a web server like Asp.Net.</span></span>

<span data-ttu-id="720c2-122">**SignalR 範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span><span class="sxs-lookup"><span data-stu-id="720c2-122">**SignalR Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/SignalR)</span></span>  
<span data-ttu-id="720c2-123">說明如何使用 OWIN/Katana 自我裝載 SignalR。</span><span class="sxs-lookup"><span data-stu-id="720c2-123">Shows how to self-host SignalR using OWIN / Katana.</span></span> <span data-ttu-id="720c2-124">如需自我裝載 SignalR 的詳細資訊，請參閱[教學課程： SignalR 自我裝載](../../../signalr/overview/deployment/tutorial-signalr-self-host.md)。</span><span class="sxs-lookup"><span data-stu-id="720c2-124">For more info about self-hosting SignalR, see [Tutorial: SignalR Self-Host](../../../signalr/overview/deployment/tutorial-signalr-self-host.md).</span></span>

<span data-ttu-id="720c2-125">**靜態檔案範例** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span><span class="sxs-lookup"><span data-stu-id="720c2-125">**Static Files Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/StaticFilesSample) </span></span>  
<span data-ttu-id="720c2-126">示範如何使用 OWIN/Katana 支援靜態檔案的 HTTP 要求。</span><span class="sxs-lookup"><span data-stu-id="720c2-126">Shows how to support HTTP requests for static files using OWIN / Katana.</span></span>

<span data-ttu-id="720c2-127">**WEB API** | [原始碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span><span class="sxs-lookup"><span data-stu-id="720c2-127">**Web API** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebApi) </span></span>  
<span data-ttu-id="720c2-128">這個範例示範如何在 IIS 中裝載 OWIN，以及如何將 Web API 新增至 OWIN 管線。</span><span class="sxs-lookup"><span data-stu-id="720c2-128">This sample shows how to host OWIN in IIS and add Web API to the OWIN pipeline.</span></span>

<span data-ttu-id="720c2-129"> | [原始程式碼](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample)的**Web 通訊端範例** </span><span class="sxs-lookup"><span data-stu-id="720c2-129">**Web Socket Sample** | [Source Code](https://github.com/aspnet/samples/tree/master/samples/aspnet/Katana/WebSocketSample) </span></span>  
<span data-ttu-id="720c2-130">示範如何使用[系統的 .net](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) websocket 類別，在 OWIN 中支援 Web 通訊端。</span><span class="sxs-lookup"><span data-stu-id="720c2-130">Shows how to support Web Sockets in OWIN by using the [System.Net.WebSockets.WebSocket](https://msdn.microsoft.com/library/system.net.websockets.websocket(v=vs.110).aspx) class.</span></span>
