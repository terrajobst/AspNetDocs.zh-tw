---
uid: signalr/overview/getting-started/supported-platforms
title: 支援的平臺 |Microsoft Docs
author: bradygaster
description: 本文說明 SignalR 支援哪些用戶端和伺服器。
ms.author: bradyg
ms.date: 04/18/2018
ms.assetid: eac31beb-0f46-4afa-9def-e80904dea4f0
msc.legacyurl: /signalr/overview/getting-started/supported-platforms
msc.type: authoredcontent
ms.openlocfilehash: 89730e591bb94022d16fe1a78a4350b38e0bf7a4
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558629"
---
# <a name="supported-platforms"></a><span data-ttu-id="ea668-103">支援的平台</span><span class="sxs-lookup"><span data-stu-id="ea668-103">Supported Platforms</span></span>

<span data-ttu-id="ea668-104">由[派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ea668-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="ea668-105">本文說明 SignalR 支援哪些用戶端和伺服器。</span><span class="sxs-lookup"><span data-stu-id="ea668-105">This article describes what clients and servers are supported by SignalR.</span></span> 
> 
> ## <a name="questions-and-comments"></a><span data-ttu-id="ea668-106">問題與意見</span><span class="sxs-lookup"><span data-stu-id="ea668-106">Questions and comments</span></span>
> 
> <span data-ttu-id="ea668-107">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="ea668-107">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ea668-108">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="ea668-108">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="ea668-109">在各種伺服器和用戶端設定下支援 SignalR。</span><span class="sxs-lookup"><span data-stu-id="ea668-109">SignalR is supported under a variety of server and client configurations.</span></span> <span data-ttu-id="ea668-110">此外，每個傳輸選項都有自己的一組需求;如果傳輸的系統需求無法使用，SignalR 會正常地容錯移轉到其他傳輸。</span><span class="sxs-lookup"><span data-stu-id="ea668-110">In addition, each transport option has a set of requirements of its own; if the system requirements for a transport are not available, SignalR will gracefully failover to other transports.</span></span> <span data-ttu-id="ea668-111">如需 SignalR 支援之傳輸的詳細資訊，請參閱[傳輸和回退](introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="ea668-111">For more information on the transports that SignalR supports, see [Transports and Fallbacks](introduction-to-signalr.md#transports).</span></span>

## <a name="server-system-requirements"></a><span data-ttu-id="ea668-112">伺服器系統需求</span><span class="sxs-lookup"><span data-stu-id="ea668-112">Server system requirements</span></span>

<span data-ttu-id="ea668-113">SignalR 伺服器元件可以裝載在各種不同的伺服器設定上。</span><span class="sxs-lookup"><span data-stu-id="ea668-113">The SignalR server component can be hosted on a variety of server configurations.</span></span> <span data-ttu-id="ea668-114">本節說明支援的作業系統版本、.NET framework、網際網路資訊伺服器和其他元件。</span><span class="sxs-lookup"><span data-stu-id="ea668-114">This section describes the supported versions of operating systems, .NET framework, Internet Information Server, and other components.</span></span>

### <a name="supported-server-operating-systems"></a><span data-ttu-id="ea668-115">支援的伺服器作業系統</span><span class="sxs-lookup"><span data-stu-id="ea668-115">Supported server operating systems</span></span>

<span data-ttu-id="ea668-116">SignalR 伺服器元件可以裝載于下列伺服器或用戶端作業系統中。</span><span class="sxs-lookup"><span data-stu-id="ea668-116">The SignalR server component can be hosted in the following server or client operating systems.</span></span> <span data-ttu-id="ea668-117">請注意，若要讓 SignalR 使用 Websocket，必須要有 Windows Server 2012、Windows Server 2016 或 Windows 8 （WebSocket 可用於 Windows Azure 網站，只要網站的 .NET framework 版本設定為4.5，而且網站的[設定] 頁面）。</span><span class="sxs-lookup"><span data-stu-id="ea668-117">Note that for SignalR to use WebSockets, Windows Server 2012, Windows Server 2016, or Windows 8 is required (WebSocket can be used on Windows Azure Web Sites, as long as the site's .NET framework version is set to 4.5, and Web Sockets is enabled in the site's Configuration page).</span></span>

- <span data-ttu-id="ea668-118">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="ea668-118">Windows Server 2016</span></span>
- <span data-ttu-id="ea668-119">Windows Server 2012</span><span class="sxs-lookup"><span data-stu-id="ea668-119">Windows Server 2012</span></span>
- <span data-ttu-id="ea668-120">Windows Server 2008 r2</span><span class="sxs-lookup"><span data-stu-id="ea668-120">Windows Server 2008 r2</span></span>
- <span data-ttu-id="ea668-121">Windows 10</span><span class="sxs-lookup"><span data-stu-id="ea668-121">Windows 10</span></span>
- <span data-ttu-id="ea668-122">Windows 8</span><span class="sxs-lookup"><span data-stu-id="ea668-122">Windows 8</span></span>
- <span data-ttu-id="ea668-123">Windows 7</span><span class="sxs-lookup"><span data-stu-id="ea668-123">Windows 7</span></span>
- <span data-ttu-id="ea668-124">Microsoft Azure</span><span class="sxs-lookup"><span data-stu-id="ea668-124">Windows Azure</span></span>

### <a name="supported-server-net-framework-version"></a><span data-ttu-id="ea668-125">支援的伺服器 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="ea668-125">Supported server .NET Framework version</span></span>

<span data-ttu-id="ea668-126">只有 .NET Framework 4.5 才支援 SignalR 2。</span><span class="sxs-lookup"><span data-stu-id="ea668-126">SignalR 2 is only supported on .NET Framework 4.5.</span></span> <span data-ttu-id="ea668-127">如需增強可靠性、相容性、穩定性和效能的更新，請參閱[建議的更新](#updates)一節。</span><span class="sxs-lookup"><span data-stu-id="ea668-127">See the [Recommended Updates](#updates) section for updates that enhance reliability, compatibility, stability, and performance.</span></span>

### <a name="supported-server-iis-versions"></a><span data-ttu-id="ea668-128">支援的伺服器 IIS 版本</span><span class="sxs-lookup"><span data-stu-id="ea668-128">Supported server IIS versions</span></span>

<span data-ttu-id="ea668-129">當 SignalR 裝載于 IIS 時，會支援下列版本。</span><span class="sxs-lookup"><span data-stu-id="ea668-129">When SignalR is hosted in IIS, the following versions are supported.</span></span> <span data-ttu-id="ea668-130">請注意，如果使用的是用戶端作業系統，例如用於開發（Windows 8 或 Windows 7），則不應使用完整版的 IIS 或 Cassini，因為將會有10個同時連接的限制，這會因為連線而很快到達是暫時性的，經常重新建立，而且不會在不再使用時立即處置。</span><span class="sxs-lookup"><span data-stu-id="ea668-130">Note that if a client operating system is used, such as for development (Windows 8 or Windows 7), full versions of IIS or Cassini should not be used, since there will be a limit of 10 simultaneous connections imposed, which will be reached very quickly since connections are transient, frequently re-established, and are not disposed immediately upon no longer being used.</span></span> <span data-ttu-id="ea668-131">IIS Express 應在用戶端作業系統上使用。</span><span class="sxs-lookup"><span data-stu-id="ea668-131">IIS Express should be used on client operating systems.</span></span>

<span data-ttu-id="ea668-132">另請注意，若要讓 SignalR 使用 WebSocket，必須使用 IIS 8 或 IIS 8 Express，伺服器必須使用 Windows 8、Windows Server 2012 或更新版本，而且必須在 IIS 中啟用 WebSocket。</span><span class="sxs-lookup"><span data-stu-id="ea668-132">Also note that for SignalR to use WebSocket, IIS 8 or IIS 8 Express must be used, the server must be using Windows 8, Windows Server 2012, or later, and WebSocket must be enabled in IIS.</span></span> <span data-ttu-id="ea668-133">如需如何在 IIS 中啟用 WebSocket 的詳細資訊，請參閱[iis 8.0 WebSocket 通訊協定支援](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support)。</span><span class="sxs-lookup"><span data-stu-id="ea668-133">For information on how to enable WebSocket in IIS, see [IIS 8.0 WebSocket Protocol Support](https://www.iis.net/learn/get-started/whats-new-in-iis-8/iis-80-websocket-protocol-support).</span></span>

- <span data-ttu-id="ea668-134">IIS 8 或 IIS 8 Express。</span><span class="sxs-lookup"><span data-stu-id="ea668-134">IIS 8 or IIS 8 Express.</span></span>
- <span data-ttu-id="ea668-135">IIS 7 和7.5。</span><span class="sxs-lookup"><span data-stu-id="ea668-135">IIS 7 and 7.5.</span></span> <span data-ttu-id="ea668-136">需要[無副檔名 url](https://support.microsoft.com/kb/980368)的支援。</span><span class="sxs-lookup"><span data-stu-id="ea668-136">Support for [extensionless URLs](https://support.microsoft.com/kb/980368) is required.</span></span>
- <span data-ttu-id="ea668-137">IIS 必須在整合模式中執行;不支援傳統模式。</span><span class="sxs-lookup"><span data-stu-id="ea668-137">IIS must be running in integrated mode; classic mode is not supported.</span></span> <span data-ttu-id="ea668-138">如果 IIS 是使用伺服器傳送的事件傳輸，在傳統模式中執行，可能會有最多30秒的訊息延遲。</span><span class="sxs-lookup"><span data-stu-id="ea668-138">Message delays of up to 30 seconds may be experienced if IIS is run in classic mode using the Server-Sent Events transport.</span></span>
- <span data-ttu-id="ea668-139">裝載應用程式必須在完全信任模式下執行。</span><span class="sxs-lookup"><span data-stu-id="ea668-139">The hosting application must be running in full trust mode.</span></span>

## <a name="client-system-requirements"></a><span data-ttu-id="ea668-140">用戶端系統需求</span><span class="sxs-lookup"><span data-stu-id="ea668-140">Client system requirements</span></span>

<span data-ttu-id="ea668-141">SignalR 可用於各種不同的用戶端平臺。</span><span class="sxs-lookup"><span data-stu-id="ea668-141">SignalR can be used in a variety of client platforms.</span></span> <span data-ttu-id="ea668-142">本節說明在網頁瀏覽器、Windows 桌面應用程式、Silverlight 應用程式和行動裝置上使用 SignalR 的系統需求。</span><span class="sxs-lookup"><span data-stu-id="ea668-142">This section describes the system requirements for using SignalR in web browsers, Windows desktop applications, Silverlight applications, and mobile devices.</span></span>

### <a name="web-browsers"></a><span data-ttu-id="ea668-143">網頁瀏覽器</span><span class="sxs-lookup"><span data-stu-id="ea668-143">Web browsers</span></span>

<span data-ttu-id="ea668-144">SignalR 可用於各種 web 瀏覽器，但通常僅支援最新的兩個版本。</span><span class="sxs-lookup"><span data-stu-id="ea668-144">SignalR can be used in a variety of web browsers, but typically, only the latest two versions are supported.</span></span>

<span data-ttu-id="ea668-145">在瀏覽器中使用 SignalR 的應用程式必須使用 jQuery 版本1.6.4 或主要的較新版本（例如1.7.2、1.8.2 或1.9.1）。</span><span class="sxs-lookup"><span data-stu-id="ea668-145">Applications that use SignalR in browsers must use jQuery version 1.6.4 or major later versions (such as 1.7.2, 1.8.2, or 1.9.1).</span></span>

<span data-ttu-id="ea668-146">SignalR 可用於下列瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="ea668-146">SignalR can be used in the following browsers:</span></span>

- <span data-ttu-id="ea668-147">Microsoft Internet Explorer 8、9、10和11版。</span><span class="sxs-lookup"><span data-stu-id="ea668-147">Microsoft Internet Explorer versions 8, 9, 10, and 11.</span></span> <span data-ttu-id="ea668-148">支援新式、桌面和行動裝置版。</span><span class="sxs-lookup"><span data-stu-id="ea668-148">Modern, Desktop, and Mobile versions are supported.</span></span>
- <span data-ttu-id="ea668-149">Mozilla Firefox：目前的版本-1，Windows 和 Mac 版本。</span><span class="sxs-lookup"><span data-stu-id="ea668-149">Mozilla Firefox: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="ea668-150">Google Chrome：目前版本-1，Windows 和 Mac 版本。</span><span class="sxs-lookup"><span data-stu-id="ea668-150">Google Chrome: current version - 1, both Windows and Mac versions.</span></span>
- <span data-ttu-id="ea668-151">Safari：目前的版本1，Mac 和 iOS 版本。</span><span class="sxs-lookup"><span data-stu-id="ea668-151">Safari: current version - 1, both Mac and iOS versions.</span></span>
- <span data-ttu-id="ea668-152">Opera：目前的版本-1，僅限 Windows。</span><span class="sxs-lookup"><span data-stu-id="ea668-152">Opera: current version - 1, Windows only.</span></span>
- <span data-ttu-id="ea668-153">Android 瀏覽器</span><span class="sxs-lookup"><span data-stu-id="ea668-153">Android browser</span></span>

<span data-ttu-id="ea668-154">除了需要特定的瀏覽器之外，SignalR 所使用的各種傳輸都有自己的需求。</span><span class="sxs-lookup"><span data-stu-id="ea668-154">In addition to requiring certain browsers, the various transports that SignalR uses have requirements of their own.</span></span> <span data-ttu-id="ea668-155">下列設定支援下列傳輸：</span><span class="sxs-lookup"><span data-stu-id="ea668-155">The following transports are supported under the following configurations:</span></span>

<a id="browser"></a>

<span data-ttu-id="ea668-156">**網頁瀏覽器傳輸需求**</span><span class="sxs-lookup"><span data-stu-id="ea668-156">**Web Browser Transport Requirements**</span></span>

| <span data-ttu-id="ea668-157">Transport</span><span class="sxs-lookup"><span data-stu-id="ea668-157">Transport</span></span> | <span data-ttu-id="ea668-158">Internet Explorer</span><span class="sxs-lookup"><span data-stu-id="ea668-158">Internet Explorer</span></span> | <span data-ttu-id="ea668-159">Chrome （Windows 或 iOS）</span><span class="sxs-lookup"><span data-stu-id="ea668-159">Chrome (Windows or iOS)</span></span> | <span data-ttu-id="ea668-160">Firefox</span><span class="sxs-lookup"><span data-stu-id="ea668-160">Firefox</span></span> | <span data-ttu-id="ea668-161">Safari （OSX 或 iOS）</span><span class="sxs-lookup"><span data-stu-id="ea668-161">Safari (OSX or iOS)</span></span> | <span data-ttu-id="ea668-162">Android</span><span class="sxs-lookup"><span data-stu-id="ea668-162">Android</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="ea668-163">WebSockets</span><span class="sxs-lookup"><span data-stu-id="ea668-163">WebSockets</span></span> | <span data-ttu-id="ea668-164">10 +</span><span class="sxs-lookup"><span data-stu-id="ea668-164">10+</span></span> | <span data-ttu-id="ea668-165">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-165">current - 1</span></span> | <span data-ttu-id="ea668-166">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-166">current - 1</span></span> | <span data-ttu-id="ea668-167">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-167">current - 1</span></span> | <span data-ttu-id="ea668-168">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-168">N/A</span></span> |
| <span data-ttu-id="ea668-169">伺服器傳送的事件</span><span class="sxs-lookup"><span data-stu-id="ea668-169">Server-Sent Events</span></span> | <span data-ttu-id="ea668-170">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-170">N/A</span></span> | <span data-ttu-id="ea668-171">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-171">current - 1</span></span> | <span data-ttu-id="ea668-172">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-172">current - 1</span></span> | <span data-ttu-id="ea668-173">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-173">current - 1</span></span> | <span data-ttu-id="ea668-174">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-174">N/A</span></span> |
| <span data-ttu-id="ea668-175">ForeverFrame</span><span class="sxs-lookup"><span data-stu-id="ea668-175">ForeverFrame</span></span> | <span data-ttu-id="ea668-176">8+</span><span class="sxs-lookup"><span data-stu-id="ea668-176">8+</span></span> | <span data-ttu-id="ea668-177">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-177">N/A</span></span> | <span data-ttu-id="ea668-178">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-178">N/A</span></span> | <span data-ttu-id="ea668-179">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-179">N/A</span></span> | <span data-ttu-id="ea668-180">4.1</span><span class="sxs-lookup"><span data-stu-id="ea668-180">4.1</span></span> |
| <span data-ttu-id="ea668-181">長時間輪詢</span><span class="sxs-lookup"><span data-stu-id="ea668-181">Long Polling</span></span> | <span data-ttu-id="ea668-182">8+</span><span class="sxs-lookup"><span data-stu-id="ea668-182">8+</span></span> | <span data-ttu-id="ea668-183">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-183">current - 1</span></span> | <span data-ttu-id="ea668-184">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-184">current - 1</span></span> | <span data-ttu-id="ea668-185">目前-1</span><span class="sxs-lookup"><span data-stu-id="ea668-185">current - 1</span></span> | <span data-ttu-id="ea668-186">4.1</span><span class="sxs-lookup"><span data-stu-id="ea668-186">4.1</span></span> |

<span data-ttu-id="ea668-187">\*： 6 + 完整功能的必要項。</span><span class="sxs-lookup"><span data-stu-id="ea668-187">\*: 6+ required for full functionality.</span></span>

#### <a name="unsupported-browsers"></a><span data-ttu-id="ea668-188">不支援的瀏覽器</span><span class="sxs-lookup"><span data-stu-id="ea668-188">Unsupported Browsers</span></span>

<span data-ttu-id="ea668-189">雖然在舊版瀏覽器中*可能會*執行 SignalR，而不會有重大問題，但我們並不會主動測試 SignalR，而且通常不會修正可能出現在其中的 bug。</span><span class="sxs-lookup"><span data-stu-id="ea668-189">While SignalR *may* run without major issues in older browser versions, we do not actively test SignalR in them and generally do not fix bugs that may appear in them.</span></span>

### <a name="windows-desktop-and-silverlight-applications"></a><span data-ttu-id="ea668-190">Windows 桌面和 Silverlight 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea668-190">Windows Desktop and Silverlight Applications</span></span>

<span data-ttu-id="ea668-191">除了在網頁瀏覽器中執行之外，SignalR 也可以裝載于獨立的 Windows 用戶端或 Silverlight 應用程式中。</span><span class="sxs-lookup"><span data-stu-id="ea668-191">In addition to running in a web browser, SignalR can be hosted in standalone Windows client or Silverlight applications.</span></span> <span data-ttu-id="ea668-192">Windows 桌面和 Silverlight SignalR 應用程式有下列系統需求。</span><span class="sxs-lookup"><span data-stu-id="ea668-192">Windows Desktop and Silverlight SignalR applications have the following system requirements.</span></span>

- <span data-ttu-id="ea668-193">Windows XP SP3 或更新版本支援使用 .NET 4 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea668-193">Applications using .NET 4 are supported on Windows XP SP3 or later.</span></span>
- <span data-ttu-id="ea668-194">Windows Vista 或更新版本支援使用 .NET Framework 4.5 的應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea668-194">Applications using .NET Framework 4.5 are supported on Windows Vista or later.</span></span>

<span data-ttu-id="ea668-195">除了作業系統和 .NET framework 需求，可供 SignalR 使用的傳輸也具有自己的需求。</span><span class="sxs-lookup"><span data-stu-id="ea668-195">In addition to operating system and .NET framework requirements, the transports available to SignalR have requirements of their own.</span></span> <span data-ttu-id="ea668-196">下列設定支援下列傳輸：</span><span class="sxs-lookup"><span data-stu-id="ea668-196">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="ea668-197">**Windows 桌面和 Silverlight 傳輸需求**</span><span class="sxs-lookup"><span data-stu-id="ea668-197">**Windows Desktop and Silverlight Transport Requirements**</span></span>

| <span data-ttu-id="ea668-198">Transport</span><span class="sxs-lookup"><span data-stu-id="ea668-198">Transport</span></span> | <span data-ttu-id="ea668-199">.NET 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea668-199">.NET application</span></span> | <span data-ttu-id="ea668-200">Silverlight</span><span class="sxs-lookup"><span data-stu-id="ea668-200">Silverlight</span></span> |
| --- | --- | --- |
| <span data-ttu-id="ea668-201">Web 通訊端</span><span class="sxs-lookup"><span data-stu-id="ea668-201">Web Sockets</span></span> | <span data-ttu-id="ea668-202">Windows 8 + 和 .NET 4.5 +</span><span class="sxs-lookup"><span data-stu-id="ea668-202">Windows 8+ and .NET 4.5+</span></span> | <span data-ttu-id="ea668-203">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-203">N/A</span></span> |
| <span data-ttu-id="ea668-204">永久框架</span><span class="sxs-lookup"><span data-stu-id="ea668-204">Forever Frame</span></span> | <span data-ttu-id="ea668-205">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-205">N/A</span></span> | <span data-ttu-id="ea668-206">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-206">N/A</span></span> |
| <span data-ttu-id="ea668-207">伺服器傳送的事件</span><span class="sxs-lookup"><span data-stu-id="ea668-207">Server-Sent Events</span></span> | <span data-ttu-id="ea668-208">.NET 4 +</span><span class="sxs-lookup"><span data-stu-id="ea668-208">.NET 4+</span></span> | <span data-ttu-id="ea668-209">5 +</span><span class="sxs-lookup"><span data-stu-id="ea668-209">5+</span></span> |
| <span data-ttu-id="ea668-210">長時間輪詢</span><span class="sxs-lookup"><span data-stu-id="ea668-210">Long Polling</span></span> | <span data-ttu-id="ea668-211">.NET 4 +</span><span class="sxs-lookup"><span data-stu-id="ea668-211">.NET 4+</span></span> | <span data-ttu-id="ea668-212">5 +</span><span class="sxs-lookup"><span data-stu-id="ea668-212">5+</span></span> |

<a id="android"></a>

### <a name="windows-store-and-windows-phone-applications"></a><span data-ttu-id="ea668-213">Windows 儲存和 Windows Phone 應用程式</span><span class="sxs-lookup"><span data-stu-id="ea668-213">Windows Store and Windows Phone Applications</span></span>

<span data-ttu-id="ea668-214">SignalR 可用於 Windows Store 應用程式和 Windows Phone 8 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ea668-214">SignalR can be used in Windows Store applications and Windows Phone 8 applications.</span></span> <span data-ttu-id="ea668-215">下列設定支援下列傳輸：</span><span class="sxs-lookup"><span data-stu-id="ea668-215">The following transports are supported under the following configurations:</span></span>

<span data-ttu-id="ea668-216">**Windows 儲存和 Windows Phone 傳輸需求**</span><span class="sxs-lookup"><span data-stu-id="ea668-216">**Windows Store and Windows Phone Transport Requirements**</span></span>

| <span data-ttu-id="ea668-217">Transport</span><span class="sxs-lookup"><span data-stu-id="ea668-217">Transport</span></span> | <span data-ttu-id="ea668-218">Windows Store/.NET</span><span class="sxs-lookup"><span data-stu-id="ea668-218">Windows Store/ .NET</span></span> | <span data-ttu-id="ea668-219">Windows Store/JavaScript</span><span class="sxs-lookup"><span data-stu-id="ea668-219">Windows Store/ JavaScript</span></span> | <span data-ttu-id="ea668-220">Windows Phone/IE</span><span class="sxs-lookup"><span data-stu-id="ea668-220">Windows Phone/ IE</span></span> | <span data-ttu-id="ea668-221">Windows Phone/.NET</span><span class="sxs-lookup"><span data-stu-id="ea668-221">Windows Phone/ .NET</span></span> |
| --- | --- | --- | --- | --- |
| <span data-ttu-id="ea668-222">WebSockets</span><span class="sxs-lookup"><span data-stu-id="ea668-222">WebSockets</span></span> | <span data-ttu-id="ea668-223">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-223">N/A</span></span> | <span data-ttu-id="ea668-224">Win8 +</span><span class="sxs-lookup"><span data-stu-id="ea668-224">Win8+</span></span> | <span data-ttu-id="ea668-225">8+</span><span class="sxs-lookup"><span data-stu-id="ea668-225">8+</span></span> | <span data-ttu-id="ea668-226">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-226">N/A</span></span> |
| <span data-ttu-id="ea668-227">永久框架</span><span class="sxs-lookup"><span data-stu-id="ea668-227">Forever Frame</span></span> | <span data-ttu-id="ea668-228">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-228">N/A</span></span> | <span data-ttu-id="ea668-229">Win8 +</span><span class="sxs-lookup"><span data-stu-id="ea668-229">Win8+</span></span> | <span data-ttu-id="ea668-230">7.5+</span><span class="sxs-lookup"><span data-stu-id="ea668-230">7.5+</span></span> | <span data-ttu-id="ea668-231">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-231">N/A</span></span> |
| <span data-ttu-id="ea668-232">伺服器傳送的事件</span><span class="sxs-lookup"><span data-stu-id="ea668-232">Server-Sent Events</span></span> | <span data-ttu-id="ea668-233">Win8 +</span><span class="sxs-lookup"><span data-stu-id="ea668-233">Win8+</span></span> | <span data-ttu-id="ea668-234">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-234">N/A</span></span> | <span data-ttu-id="ea668-235">N/A</span><span class="sxs-lookup"><span data-stu-id="ea668-235">N/A</span></span> | <span data-ttu-id="ea668-236">8+</span><span class="sxs-lookup"><span data-stu-id="ea668-236">8+</span></span> |
| <span data-ttu-id="ea668-237">長時間輪詢</span><span class="sxs-lookup"><span data-stu-id="ea668-237">Long Polling</span></span> | <span data-ttu-id="ea668-238">Win8 +</span><span class="sxs-lookup"><span data-stu-id="ea668-238">Win8+</span></span> | <span data-ttu-id="ea668-239">Win8 +</span><span class="sxs-lookup"><span data-stu-id="ea668-239">Win8+</span></span> | <span data-ttu-id="ea668-240">7.5+</span><span class="sxs-lookup"><span data-stu-id="ea668-240">7.5+</span></span> | <span data-ttu-id="ea668-241">8+</span><span class="sxs-lookup"><span data-stu-id="ea668-241">8+</span></span> |

<a id="updates"></a>

## <a name="recommended-updates"></a><span data-ttu-id="ea668-242">建議的更新</span><span class="sxs-lookup"><span data-stu-id="ea668-242">Recommended Updates</span></span>

<span data-ttu-id="ea668-243">以下是針對 SignalR 伺服器建議的更新：</span><span class="sxs-lookup"><span data-stu-id="ea668-243">The following updates are recommended for SignalR servers:</span></span>

- <span data-ttu-id="ea668-244">您可以在[這裡](https://support.microsoft.com/kb/2750149)取得 .NET Framework 4.5 的更新。</span><span class="sxs-lookup"><span data-stu-id="ea668-244">An update for .NET Framework 4.5 is available [here](https://support.microsoft.com/kb/2750149).</span></span>
- <span data-ttu-id="ea668-245">Microsoft 會定期發行 Qfe 以進行 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="ea668-245">Microsoft will periodically release QFEs for ASP.NET.</span></span> <span data-ttu-id="ea668-246">這些應該套用為 [可用]。</span><span class="sxs-lookup"><span data-stu-id="ea668-246">These should be applied as available.</span></span>
