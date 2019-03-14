---
title: 裝載模型的 razor 元件
author: guardrex
description: 了解用戶端 Blazor 和裝載模型的伺服器端 ASP.NET Core Razor 元件。
monikerRange: '>= aspnetcore-3.0'
ms.author: riande
ms.custom: mvc
ms.date: 01/29/2019
uid: razor-components/hosting-models
ms.openlocfilehash: d1e0c472d7d10eeb4cef0da735cf703c98dd1645
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57042435"
---
# <a name="razor-components-hosting-models"></a><span data-ttu-id="6e8c4-103">裝載模型的 razor 元件</span><span class="sxs-lookup"><span data-stu-id="6e8c4-103">Razor Components hosting models</span></span>

<span data-ttu-id="6e8c4-104">藉由[Daniel Roth](https://github.com/danroth27)</span><span class="sxs-lookup"><span data-stu-id="6e8c4-104">By [Daniel Roth](https://github.com/danroth27)</span></span>

<span data-ttu-id="6e8c4-105">Razor 元件是設計用來執行用戶端的 web 架構 WebAssembly 為基礎的.NET 執行階段上的瀏覽器中 (*Blazor*) 或 ASP.NET Core 中的伺服器端 (*ASP.NET Core Razor 元件*)。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-105">Razor Components is a web framework designed to run client-side in the browser on a WebAssembly-based .NET runtime (*Blazor*) or server-side in ASP.NET Core (*ASP.NET Core Razor Components*).</span></span> <span data-ttu-id="6e8c4-106">無論裝載模型、 應用程式和元件模型*維持不變*。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-106">Regardless of the hosting model, the app and component models *remain the same*.</span></span> <span data-ttu-id="6e8c4-107">這篇文章會討論可用的裝載模型。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-107">This article discusses the available hosting models.</span></span>

## <a name="client-side-hosting-model"></a><span data-ttu-id="6e8c4-108">用戶端裝載模型</span><span class="sxs-lookup"><span data-stu-id="6e8c4-108">Client-side hosting model</span></span>

[!INCLUDE[](~/includes/razor-components-preview-notice.md)]

<span data-ttu-id="6e8c4-109">Blazor 的主要裝載模型是在瀏覽器中的執行用戶端。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-109">The principal hosting model for Blazor is running client-side in the browser.</span></span> <span data-ttu-id="6e8c4-110">在此模型中，Blazor 應用程式、 其相依性，以及.NET 執行階段會下載至瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-110">In this model, the Blazor app, its dependencies, and the .NET runtime are downloaded to the browser.</span></span> <span data-ttu-id="6e8c4-111">應用程式會直接在瀏覽器 UI 執行緒上執行。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-111">The app is executed directly on the browser UI thread.</span></span> <span data-ttu-id="6e8c4-112">所有的 UI 更新及事件處理會發生相同的程序中。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-112">All UI updates and event handling happens within the same process.</span></span> <span data-ttu-id="6e8c4-113">應用程式資產可部署為使用任何網頁伺服器慣用的靜態檔案 (請參閱[主機和部署](xref:host-and-deploy/razor-components/index))。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-113">The app assets can be deployed as static files using whatever web server is preferred (see [Host and deploy](xref:host-and-deploy/razor-components/index)).</span></span>

![Blazor 用戶端：Blazor 應用程式會在瀏覽器 UI 執行緒上執行。](hosting-models/_static/client-side.png)

<span data-ttu-id="6e8c4-115">若要建立一個使用的用戶端的裝載模型的 Blazor 應用程式，請使用**Blazor**或 **（ASP.NET Core 裝載） 的 Blazor**專案範本 (`blazor`或`blazorhosted`範本時使用[dotnet 新](/dotnet/core/tools/dotnet-new)命令在命令提示字元)。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-115">To create a Blazor app using the client-side hosting model, use the **Blazor** or **Blazor (ASP.NET Core Hosted)** project templates (`blazor` or `blazorhosted` template when using the [dotnet new](/dotnet/core/tools/dotnet-new) command at a command prompt).</span></span> <span data-ttu-id="6e8c4-116">包含*blazor.webassembly.js*指令碼處理：</span><span class="sxs-lookup"><span data-stu-id="6e8c4-116">The included *blazor.webassembly.js* script handles:</span></span>

* <span data-ttu-id="6e8c4-117">下載.NET 執行階段、 應用程式和其相依性。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-117">Downloading the .NET runtime, the app, and its dependencies.</span></span>
* <span data-ttu-id="6e8c4-118">要執行應用程式的執行階段初始化。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-118">Initialization of the runtime to run the app.</span></span>

<span data-ttu-id="6e8c4-119">用戶端的裝載模型提供幾項優點。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-119">The client-side hosting model offers several benefits.</span></span> <span data-ttu-id="6e8c4-120">用戶端 Blazor:</span><span class="sxs-lookup"><span data-stu-id="6e8c4-120">Client-side Blazor:</span></span>

* <span data-ttu-id="6e8c4-121">有任何的.NET 伺服器端相依性。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-121">Has no .NET server-side dependency.</span></span>
* <span data-ttu-id="6e8c4-122">有豐富的互動式 UI。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-122">Has a rich interactive UI.</span></span>
* <span data-ttu-id="6e8c4-123">充分利用用戶端資源和功能。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-123">Fully leverages client resources and capabilities.</span></span>
* <span data-ttu-id="6e8c4-124">卸載工作從伺服器到用戶端。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-124">Offloads work from the server to the client.</span></span>
* <span data-ttu-id="6e8c4-125">支援離線案例。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-125">Supports offline scenarios.</span></span>

<span data-ttu-id="6e8c4-126">有裝載用戶端的缺點。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-126">There are downsides to client-side hosting.</span></span> <span data-ttu-id="6e8c4-127">用戶端 Blazor:</span><span class="sxs-lookup"><span data-stu-id="6e8c4-127">Client-side Blazor:</span></span>

* <span data-ttu-id="6e8c4-128">將應用程式限制的瀏覽器的功能。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-128">Restricts the app to the capabilities of the browser.</span></span>
* <span data-ttu-id="6e8c4-129">需要支援用戶端硬體和軟體 （例如 WebAssembly 支援）。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-129">Requires capable client hardware and software (for example, WebAssembly support).</span></span>
* <span data-ttu-id="6e8c4-130">具有較大的下載大小和較長載入時間的應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-130">Has a larger download size and longer app load time.</span></span>
* <span data-ttu-id="6e8c4-131">具有較少成熟的.NET 執行階段和工具支援 （例如，.NET Standard 的支援和偵錯的限制）。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-131">Has less mature .NET runtime and tooling support (for example, limitations in .NET Standard support and debugging).</span></span>

<span data-ttu-id="6e8c4-132">Visual Studio 包含**Blazor (裝載 ASP.NET Core)** 建立 Blazor 應用程式執行 WebAssembly，而且裝載 ASP.NET Core 伺服器上的專案範本。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-132">Visual Studio includes the **Blazor (ASP.NET Core hosted)** project template for creating a Blazor app that runs on WebAssembly and is hosted on an ASP.NET Core server.</span></span> <span data-ttu-id="6e8c4-133">ASP.NET Core 應用程式提供給用戶端 Blazor 應用程式，但因不同的處理序。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-133">The ASP.NET Core app serves the Blazor app to clients but is otherwise a separate process.</span></span> <span data-ttu-id="6e8c4-134">用戶端 Blazor 應用程式可以透過使用 Web API 呼叫或 SignalR 連線的網路來與伺服器互動。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-134">The client-side Blazor app can interact with the server over the network using Web API calls or SignalR connections.</span></span>

> [!IMPORTANT]
> <span data-ttu-id="6e8c4-135">如果用戶端 Blazor 應用程式由裝載為 IIS 子應用程式的 ASP.NET Core 應用程式，停用繼承的 ASP.NET Core 模組處理常式。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-135">If a client-side Blazor app is served by an ASP.NET Core app hosted as an IIS sub-app, disable the inherited ASP.NET Core Module handler.</span></span> <span data-ttu-id="6e8c4-136">Blazor 應用程式中設定的應用程式的基底路徑*index.html*檔案，以在 IIS 中設定子應用程式時使用的 IIS 別名。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-136">Set the app base path in the Blazor app's *index.html* file to the IIS alias used when configuring the sub-app in IIS.</span></span>
>
> <span data-ttu-id="6e8c4-137">如需詳細資訊，請參閱 <<c0> [ 應用程式基底路徑](xref:host-and-deploy/razor-components/index#app-base-path)。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-137">For more information, see [App base path](xref:host-and-deploy/razor-components/index#app-base-path).</span></span>

## <a name="server-side-hosting-model"></a><span data-ttu-id="6e8c4-138">伺服器端裝載模型</span><span class="sxs-lookup"><span data-stu-id="6e8c4-138">Server-side hosting model</span></span>

<span data-ttu-id="6e8c4-139">在 ASP.NET Core Razor 元件伺服器端裝載模型中，從 ASP.NET Core 應用程式中的伺服器上執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-139">In the ASP.NET Core Razor Components server-side hosting model, the app is executed on the server from within an ASP.NET Core app.</span></span> <span data-ttu-id="6e8c4-140">UI 更新、事件處理及 JavaScript 呼叫會透過 SignalR 連線處理。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-140">UI updates, event handling, and JavaScript calls are handled over a SignalR connection.</span></span>

![ASP.NET Core Razor 元件伺服器端：瀏覽器互動 （裝載 ASP.NET Core 應用程式內） 的應用程式伺服器上透過 SignalR 的連線。](hosting-models/_static/server-side.png)

<span data-ttu-id="6e8c4-142">若要建立一個使用的伺服器端的主控模型的 Razor 元件應用程式，請使用**Blazor （伺服器端 ASP.NET Core 中）** 範本 (`blazorserver`使用時[dotnet 新](/dotnet/core/tools/dotnet-new)在命令提示字元)。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-142">To create a Razor Components app using the server-side hosting model, use the **Blazor (Server-side in ASP.NET Core)** template (`blazorserver` when using [dotnet new](/dotnet/core/tools/dotnet-new) at a command prompt).</span></span> <span data-ttu-id="6e8c4-143">將 ASP.NET Core 應用程式裝載 Razor 元件伺服器端應用程式，並設定 SignalR 端點的用戶端連線的位置。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-143">An ASP.NET Core app hosts the Razor Components server-side app and sets up the SignalR endpoint where clients connect.</span></span> <span data-ttu-id="6e8c4-144">ASP.NET Core 應用程式參考應用程式的`Startup`来加入類別：</span><span class="sxs-lookup"><span data-stu-id="6e8c4-144">The ASP.NET Core app references the app's `Startup` class to add:</span></span>

* <span data-ttu-id="6e8c4-145">伺服器端 Razor 元件服務。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-145">Server-side Razor Components services.</span></span>
* <span data-ttu-id="6e8c4-146">應用程式，以在要求處理管線。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-146">The app to the request handling pipeline.</span></span>

[!code-csharp[](hosting-models/samples_snapshot/Startup.cs?highlight=5,27)]

<span data-ttu-id="6e8c4-147">*Blazor.server.js*指令碼&dagger;會建立用戶端連線。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-147">The *blazor.server.js* script&dagger; establishes the client connection.</span></span> <span data-ttu-id="6e8c4-148">它是保存和還原應用程式狀態為 必要 （例如，如果遺失的網路連線） 的應用程式的責任。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-148">It's the app's responsibility to persist and restore app state as required (for example, in the event of a lost network connection).</span></span>

<span data-ttu-id="6e8c4-149">伺服器端的主控模型會提供數個優點：</span><span class="sxs-lookup"><span data-stu-id="6e8c4-149">The server-side hosting model offers several benefits:</span></span>

* <span data-ttu-id="6e8c4-150">可讓您撰寫您的整個應用程式使用.NET 和C#使用的元件模型。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-150">Allows you to write your entire app with .NET and C# using the component model.</span></span>
* <span data-ttu-id="6e8c4-151">提供豐富的互動式風格，並避免不必要的頁面重新整理。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-151">Provides a rich interactive feel and avoids unnecessary page refreshes.</span></span>
* <span data-ttu-id="6e8c4-152">具有大幅縮小應用程式大小比用戶端 Blazor 應用程式，且速度更快載入。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-152">Has a significantly smaller app size than a client-side Blazor app and loads much faster.</span></span>
* <span data-ttu-id="6e8c4-153">元件的邏輯可以充分利用 server 功能，包括使用任何.NET Core 相容的 Api。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-153">Component logic can take full advantage of server capabilities, including using any .NET Core compatible APIs.</span></span>
* <span data-ttu-id="6e8c4-154">在.NET Core 上的伺服器上執行，讓現有的.NET 工具，例如偵錯時，如預期運作。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-154">Runs on .NET Core on the server, so existing .NET tooling, such as debugging, works as expected.</span></span>
* <span data-ttu-id="6e8c4-155">使用精簡型用戶端 （例如，不支援 WebAssembly 和資源的瀏覽器受限的裝置）。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-155">Works with thin clients (for example, browsers that don't support WebAssembly and resource constrained devices).</span></span>

<span data-ttu-id="6e8c4-156">有伺服器端裝載的缺點：</span><span class="sxs-lookup"><span data-stu-id="6e8c4-156">There are downsides to server-side hosting:</span></span>

* <span data-ttu-id="6e8c4-157">具有較高的延遲：每個使用者互動牽涉到的網路躍點。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-157">Has higher latency: Every user interaction involves a network hop.</span></span>
* <span data-ttu-id="6e8c4-158">提供任何離線的支援：如果用戶端連線失敗，應用程式會停止運作。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-158">Offers no offline support: If the client connection fails, the app stops working.</span></span>
* <span data-ttu-id="6e8c4-159">降低延展性：伺服器必須管理多個用戶端連線，並處理用戶端狀態。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-159">Has reduced scalability: The server must manage multiple client connections and handle client state.</span></span>
* <span data-ttu-id="6e8c4-160">需要 ASP.NET Core 伺服器以提供應用程式。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-160">Requires an ASP.NET Core server to serve the app.</span></span> <span data-ttu-id="6e8c4-161">不使用伺服器 （例如，從 CDN) 的部署不可行。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-161">Deployment without a server (for example, from a CDN) isn't possible.</span></span>

<span data-ttu-id="6e8c4-162">&dagger;*Blazor.server.js*指令碼發行至下列路徑： *bin / {偵錯 |發行} / {目標 FRAMEWORK} /publish/ {應用程式名稱}。應用程式/dist/架構 （_f)*。</span><span class="sxs-lookup"><span data-stu-id="6e8c4-162">&dagger;The *blazor.server.js* script is published to the following path: *bin/{Debug|Release}/{TARGET FRAMEWORK}/publish/{APPLICATION NAME}.App/dist/_framework*.</span></span>
