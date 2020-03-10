---
uid: signalr/overview/performance/signalr-performance
title: SignalR 效能 |Microsoft Docs
author: bradygaster
description: SignalR 效能
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 3751f5e7-59db-4be0-a290-50abc24e5c84
msc.legacyurl: /signalr/overview/performance/signalr-performance
msc.type: authoredcontent
ms.openlocfilehash: b8a44f4c924c94cdfff1ce7630539b45fe269bbf
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558321"
---
# <a name="signalr-performance"></a><span data-ttu-id="f74ef-103">SignalR 效能</span><span class="sxs-lookup"><span data-stu-id="f74ef-103">SignalR Performance</span></span>

<span data-ttu-id="f74ef-104">由[派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="f74ef-104">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="f74ef-105">本主題描述如何在 SignalR 應用程式中設計、測量和改善效能。</span><span class="sxs-lookup"><span data-stu-id="f74ef-105">This topic describes how to design for, measure, and improve performance in a SignalR application.</span></span>
>
> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="f74ef-106">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="f74ef-106">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="f74ef-107">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f74ef-107">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="f74ef-108">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f74ef-108">.NET 4.5</span></span>
> - <span data-ttu-id="f74ef-109">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="f74ef-109">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="f74ef-110">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="f74ef-110">Previous versions of this topic</span></span>
>
> <span data-ttu-id="f74ef-111">如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-111">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="f74ef-112">問題與意見</span><span class="sxs-lookup"><span data-stu-id="f74ef-112">Questions and comments</span></span>
>
> <span data-ttu-id="f74ef-113">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="f74ef-113">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="f74ef-114">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-114">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="f74ef-115">如需 SignalR 效能和調整的最新簡報，請參閱[使用 ASP.NET SignalR 調整即時 Web](https://channel9.msdn.com/Events/Build/2013/3-502)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-115">For a recent presentation on SignalR performance and scaling, see [Scaling the Real-time Web with ASP.NET SignalR](https://channel9.msdn.com/Events/Build/2013/3-502).</span></span>

<span data-ttu-id="f74ef-116">本主題包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="f74ef-116">This topic contains the following sections:</span></span>

- [<span data-ttu-id="f74ef-117">設計考量</span><span class="sxs-lookup"><span data-stu-id="f74ef-117">Design considerations</span></span>](#design)
- [<span data-ttu-id="f74ef-118">調整 SignalR 伺服器的效能</span><span class="sxs-lookup"><span data-stu-id="f74ef-118">Tuning your SignalR server for performance</span></span>](#tuning)
- [<span data-ttu-id="f74ef-119">針對效能問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f74ef-119">Troubleshooting performance issues</span></span>](#troubleshooting)
- [<span data-ttu-id="f74ef-120">使用 SignalR 效能計數器</span><span class="sxs-lookup"><span data-stu-id="f74ef-120">Using SignalR performance counters</span></span>](#perfcounters)
- [<span data-ttu-id="f74ef-121">使用其他效能計數器</span><span class="sxs-lookup"><span data-stu-id="f74ef-121">Using other performance counters</span></span>](#othercounters)
- [<span data-ttu-id="f74ef-122">其他資源</span><span class="sxs-lookup"><span data-stu-id="f74ef-122">Other resources</span></span>](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a><span data-ttu-id="f74ef-123">設計考量</span><span class="sxs-lookup"><span data-stu-id="f74ef-123">Design considerations</span></span>

<span data-ttu-id="f74ef-124">本節說明可在 SignalR 應用程式設計期間實行的模式，以確保不會產生不必要的網路流量來妨礙運作效能。</span><span class="sxs-lookup"><span data-stu-id="f74ef-124">This section describes patterns that can be implemented during the design of a SignalR application, to ensure that performance is not being hindered by generating unnecessary network traffic.</span></span>

### <a name="throttling-message-frequency"></a><span data-ttu-id="f74ef-125">節流訊息頻率</span><span class="sxs-lookup"><span data-stu-id="f74ef-125">Throttling message frequency</span></span>

<span data-ttu-id="f74ef-126">即使是在以較高頻率（例如即時遊戲應用程式）傳送訊息的應用程式中，大部分的應用程式都不需要一次傳送超過幾個訊息。</span><span class="sxs-lookup"><span data-stu-id="f74ef-126">Even in an application that sends out messages at a high frequency (such as a realtime gaming application), most applications don't need to send more than a few messages a second.</span></span> <span data-ttu-id="f74ef-127">若要減少每個用戶端產生的流量量，可以將訊息迴圈實作為佇列，並將訊息送出的頻率不會超過固定速率（也就是每秒傳送的訊息數上限，如果當時的訊息位於要傳送的 terval）。</span><span class="sxs-lookup"><span data-stu-id="f74ef-127">To reduce the amount of traffic that each client generates, a message loop can be implemented that queues and sends out messages no more frequently than a fixed rate (that is, up to a certain number of messages will be sent every second, if there are messages in that time interval to be sent).</span></span> <span data-ttu-id="f74ef-128">如需將訊息節流為特定速率（來自用戶端和伺服器）的範例應用程式，請參閱[使用 SignalR 的高頻率即時](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-128">For a sample application that throttles messages to a certain rate (from both client and server), see [High-Frequency Realtime with SignalR](../getting-started/tutorial-high-frequency-realtime-with-signalr.md).</span></span>

### <a name="reducing-message-size"></a><span data-ttu-id="f74ef-129">減少訊息大小</span><span class="sxs-lookup"><span data-stu-id="f74ef-129">Reducing message size</span></span>

<span data-ttu-id="f74ef-130">您可以減少已序列化物件的大小，以減少 SignalR 訊息的大小。</span><span class="sxs-lookup"><span data-stu-id="f74ef-130">You can reduce the size of a SignalR message by reducing the size of your serialized objects.</span></span> <span data-ttu-id="f74ef-131">在伺服器程式碼中，如果您要傳送的物件包含不需要傳輸的屬性，請使用 `JsonIgnore` 屬性來避免序列化這些屬性。</span><span class="sxs-lookup"><span data-stu-id="f74ef-131">In server code, if you're sending an object that contains properties that don't need to be transmitted, prevent those properties from being serialized by using the `JsonIgnore` attribute.</span></span> <span data-ttu-id="f74ef-132">屬性的名稱也會儲存在訊息中;您可以使用 `JsonProperty` 屬性來縮短屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="f74ef-132">The names of properties are also stored in the message; the names of properties can be shortened using the `JsonProperty` attribute.</span></span> <span data-ttu-id="f74ef-133">下列程式碼範例示範如何排除將屬性傳送至用戶端的方法，以及如何縮短屬性名稱：</span><span class="sxs-lookup"><span data-stu-id="f74ef-133">The following code sample demonstrates how to exclude a property from being sent to the client, and how to shorten property names:</span></span>

<span data-ttu-id="f74ef-134">**.NET server 程式碼，它會示範 JsonIgnore 屬性來排除要傳送至用戶端的資料，以及用來減少訊息大小的 JsonProperty 屬性**</span><span class="sxs-lookup"><span data-stu-id="f74ef-134">**.NET server code that demonstrates the JsonIgnore attribute to exclude data from being sent to the client, and the JsonProperty attribute to reduce message size**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

<span data-ttu-id="f74ef-135">為了在用戶端程式代碼中保留可讀性/可維護性，可以在收到訊息之後，將縮寫的屬性名稱重新對應至易記名稱。</span><span class="sxs-lookup"><span data-stu-id="f74ef-135">In order to retain readability/ maintainability in the client code, the abbreviated property names can be remapped to human-friendly names after the message is received.</span></span> <span data-ttu-id="f74ef-136">下列程式碼範例示範一種可能的方式，藉由定義訊息合約（對應）來重新對應較長的名稱，並使用 `reMap` 函式將合約套用到優化的訊息類別：</span><span class="sxs-lookup"><span data-stu-id="f74ef-136">The following code sample demonstrates one possible way of remapping shortened names to longer ones, by defining a message contract (mapping), and using the `reMap` function to apply the contract to the optimized message class:</span></span>

<span data-ttu-id="f74ef-137">**將縮短的屬性名稱重新對應到人類可讀名稱的用戶端 JavaScript 程式碼**</span><span class="sxs-lookup"><span data-stu-id="f74ef-137">**Client-side JavaScript code that remaps shortened property names to human-readable names**</span></span>

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

<span data-ttu-id="f74ef-138">也可以使用相同的方法，從用戶端到伺服器的訊息中縮短名稱。</span><span class="sxs-lookup"><span data-stu-id="f74ef-138">Names can be shortened in messages from the client to the server as well, using the same method.</span></span>

<span data-ttu-id="f74ef-139">減少 message 物件的記憶體使用量（也就是訊息使用的記憶體數量）也可以改善效能。</span><span class="sxs-lookup"><span data-stu-id="f74ef-139">Reducing the memory footprint (that is, the amount of memory used for the message) of the message object can also improve performance.</span></span> <span data-ttu-id="f74ef-140">例如，如果不需要 `int` 的完整範圍，就可以改用 `short` 或 `byte`。</span><span class="sxs-lookup"><span data-stu-id="f74ef-140">For example, if the full range of an `int` is not needed, a `short` or `byte` can be used instead.</span></span>

<span data-ttu-id="f74ef-141">由於訊息會儲存在伺服器記憶體的訊息匯流排中，因此減少訊息的大小也可以解決伺服器記憶體的問題。</span><span class="sxs-lookup"><span data-stu-id="f74ef-141">Since messages are stored in the message bus in server memory, reducing the size of messages can also address server memory issues.</span></span>

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a><span data-ttu-id="f74ef-142">調整 SignalR 伺服器的效能</span><span class="sxs-lookup"><span data-stu-id="f74ef-142">Tuning your SignalR server for performance</span></span>

<span data-ttu-id="f74ef-143">下列設定可用於微調伺服器，以在 SignalR 應用程式中獲得更佳的效能。</span><span class="sxs-lookup"><span data-stu-id="f74ef-143">The following configuration settings can be used to tune your server for better performance in a SignalR application.</span></span> <span data-ttu-id="f74ef-144">如需如何在 ASP.NET 應用程式中改善效能的一般資訊，請參閱[改善 ASP.NET 效能](https://msdn.microsoft.com/library/ff647787.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-144">For general information on how to improve performance in an ASP.NET application, see [Improving ASP.NET Performance](https://msdn.microsoft.com/library/ff647787.aspx).</span></span>

<span data-ttu-id="f74ef-145">**SignalR 設定**</span><span class="sxs-lookup"><span data-stu-id="f74ef-145">**SignalR configuration settings**</span></span>

- <span data-ttu-id="f74ef-146">**DefaultMessageBufferSize**：根據預設，SignalR 會每個連線在每個中樞的記憶體中保留1000訊息。</span><span class="sxs-lookup"><span data-stu-id="f74ef-146">**DefaultMessageBufferSize**: By default, SignalR retains 1000 messages in memory per hub per connection.</span></span> <span data-ttu-id="f74ef-147">如果使用的是大型訊息，這可能會造成記憶體問題，藉由減少此值來緩解。</span><span class="sxs-lookup"><span data-stu-id="f74ef-147">If large messages are being used, this may create memory issues which can be alleviated by reducing this value.</span></span> <span data-ttu-id="f74ef-148">這項設定可在 ASP.NET 應用程式的 `Application_Start` 事件處理常式中設定，或在自我裝載應用程式中 OWIN 啟動類別的 `Configuration` 方法中設定。</span><span class="sxs-lookup"><span data-stu-id="f74ef-148">This setting can be set in the `Application_Start` event handler in an ASP.NET application, or in the `Configuration` method of an OWIN startup class in a self-hosted application.</span></span> <span data-ttu-id="f74ef-149">下列範例示範如何減少此值，以減少應用程式的記憶體使用量，以減少使用的伺服器記憶體量：</span><span class="sxs-lookup"><span data-stu-id="f74ef-149">The following sample demonstrates how to reduce this value in order to reduce the memory footprint of your application in order to reduce the amount of server memory used:</span></span>

    <span data-ttu-id="f74ef-150">**Startup.cs 中的 .NET 伺服器程式碼，以減少預設的訊息緩衝區大小**</span><span class="sxs-lookup"><span data-stu-id="f74ef-150">**.NET server code in Startup.cs for decreasing default message buffer size**</span></span>

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

<span data-ttu-id="f74ef-151">**IIS 設定**</span><span class="sxs-lookup"><span data-stu-id="f74ef-151">**IIS configuration settings**</span></span>

- <span data-ttu-id="f74ef-152">**每個應用程式的並行要求數上限**：增加同時 IIS 要求的數目會增加可用來提供要求的伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="f74ef-152">**Max concurrent requests per application**: Increasing the number of concurrent IIS requests will increase server resources available for serving requests.</span></span> <span data-ttu-id="f74ef-153">預設值為 5000;若要增加這項設定，請在提升許可權的命令提示字元中執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f74ef-153">The default value is 5000; to increase this setting, execute the following commands in an elevated command prompt:</span></span>

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- <span data-ttu-id="f74ef-154">**ApplicationPool QueueLength**：這是應用程式集區之 HTTP.sys 佇列的最大要求數目。</span><span class="sxs-lookup"><span data-stu-id="f74ef-154">**ApplicationPool QueueLength**: This is the maximum number of requests that Http.sys queues for the application pool.</span></span> <span data-ttu-id="f74ef-155">當佇列已滿時，新的要求會收到503「服務無法使用」的回應。</span><span class="sxs-lookup"><span data-stu-id="f74ef-155">When the queue is full, new requests receive a 503 "Service Unavailable" response.</span></span> <span data-ttu-id="f74ef-156">預設值為 1000。</span><span class="sxs-lookup"><span data-stu-id="f74ef-156">The default value is 1000.</span></span>

    <span data-ttu-id="f74ef-157">縮短裝載應用程式之應用程式集區中工作者進程的佇列長度，將可節省記憶體資源。</span><span class="sxs-lookup"><span data-stu-id="f74ef-157">Shortening the queue length for the worker process in the application pool hosting your application will conserve memory resources.</span></span> <span data-ttu-id="f74ef-158">如需詳細資訊，請參閱[管理、調整和設定應用程式](https://technet.microsoft.com/library/cc745955.aspx)集區。</span><span class="sxs-lookup"><span data-stu-id="f74ef-158">For more information, see [Managing, Tuning, and Configuring Application Pools](https://technet.microsoft.com/library/cc745955.aspx).</span></span>

<span data-ttu-id="f74ef-159">**ASP.NET 設定**</span><span class="sxs-lookup"><span data-stu-id="f74ef-159">**ASP.NET configuration settings**</span></span>

<span data-ttu-id="f74ef-160">本節包含可以在 `aspnet.config` 檔案中設定的配置設定。</span><span class="sxs-lookup"><span data-stu-id="f74ef-160">This section includes configuration settings that can be set in the `aspnet.config` file.</span></span> <span data-ttu-id="f74ef-161">此檔案可在下列兩個位置的其中一個找到，視平臺而定：</span><span class="sxs-lookup"><span data-stu-id="f74ef-161">This file is found in one of two locations, depending on platform:</span></span>

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

<span data-ttu-id="f74ef-162">可能會改善 SignalR 效能的 ASP.NET 設定包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="f74ef-162">ASP.NET settings that may improve SignalR performance include the following:</span></span>

- <span data-ttu-id="f74ef-163">**每一 CPU 的並行要求數上限**：增加此設定可減輕效能瓶頸。</span><span class="sxs-lookup"><span data-stu-id="f74ef-163">**Maximum concurrent requests per CPU**: Increasing this setting may alleviate performance bottlenecks.</span></span> <span data-ttu-id="f74ef-164">若要增加此設定，請將下列設定新增至 `aspnet.config` 檔案：</span><span class="sxs-lookup"><span data-stu-id="f74ef-164">To increase this setting, add the following configuration setting to the `aspnet.config` file:</span></span>

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- <span data-ttu-id="f74ef-165">**要求佇列限制**：當連線總數超過 `maxConcurrentRequestsPerCPU` 設定時，ASP.NET 會開始使用佇列來節流要求。</span><span class="sxs-lookup"><span data-stu-id="f74ef-165">**Request Queue Limit**: When the total number of connections exceeds the `maxConcurrentRequestsPerCPU` setting, ASP.NET will start throttling requests using a queue.</span></span> <span data-ttu-id="f74ef-166">若要增加佇列的大小，您可以增加 [`requestQueueLimit`] 設定。</span><span class="sxs-lookup"><span data-stu-id="f74ef-166">To increase the size of the queue, you can increase the `requestQueueLimit` setting.</span></span> <span data-ttu-id="f74ef-167">若要這麼做，請將下列設定設為 `config/machine.config` 中的 `processModel` 節點（而不是 `aspnet.config`）：</span><span class="sxs-lookup"><span data-stu-id="f74ef-167">To do this, add the following configuration setting to the `processModel` node in `config/machine.config` (rather than `aspnet.config`):</span></span>

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a><span data-ttu-id="f74ef-168">針對效能問題進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="f74ef-168">Troubleshooting performance issues</span></span>

<span data-ttu-id="f74ef-169">本節說明在您的應用程式中找出效能瓶頸的方式。</span><span class="sxs-lookup"><span data-stu-id="f74ef-169">This section describes ways to find performance bottlenecks in your application.</span></span>

### <a name="verifying-that-websocket-is-being-used"></a><span data-ttu-id="f74ef-170">正在驗證是否正在使用 WebSocket</span><span class="sxs-lookup"><span data-stu-id="f74ef-170">Verifying that WebSocket is being used</span></span>

<span data-ttu-id="f74ef-171">雖然 SignalR 可以使用各種傳輸來進行用戶端與伺服器之間的通訊，但 WebSocket 提供了顯著的效能優勢，如果用戶端和伺服器支援，則應使用它們。</span><span class="sxs-lookup"><span data-stu-id="f74ef-171">While SignalR can use a variety of transports for communication between client and server, WebSocket offers a significant performance advantage, and should be used if the client and server support it.</span></span> <span data-ttu-id="f74ef-172">若要判斷您的用戶端和伺服器是否符合 WebSocket 的需求，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-172">To determine if your client and server meet the requirements for WebSocket, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span> <span data-ttu-id="f74ef-173">若要判斷應用程式中所使用的傳輸為何，您可以使用瀏覽器開發人員工具，並檢查記錄檔，以查看連接所使用的傳輸。</span><span class="sxs-lookup"><span data-stu-id="f74ef-173">To determine what transport is being used in your application, you can use the browser developer tools, and examine the logs to see what transport is being used for the connection.</span></span> <span data-ttu-id="f74ef-174">如需在 Internet Explorer 和 Chrome 中使用瀏覽器開發工具的相關資訊，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-174">For information on using the browser development tools in Internet Explorer and Chrome, see [Transports and Fallbacks](../getting-started/introduction-to-signalr.md#transports).</span></span>

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a><span data-ttu-id="f74ef-175">使用 SignalR 效能計數器</span><span class="sxs-lookup"><span data-stu-id="f74ef-175">Using SignalR performance counters</span></span>

<span data-ttu-id="f74ef-176">本節說明如何啟用和使用 `Microsoft.AspNet.SignalR.Utils` 封裝中找到的 SignalR 效能計數器。</span><span class="sxs-lookup"><span data-stu-id="f74ef-176">This section describes how to enable and use SignalR performance counters, found in the `Microsoft.AspNet.SignalR.Utils` package.</span></span>

### <a name="installing-signalrexe"></a><span data-ttu-id="f74ef-177">安裝 signalr</span><span class="sxs-lookup"><span data-stu-id="f74ef-177">Installing signalr.exe</span></span>

<span data-ttu-id="f74ef-178">您可以使用稱為 SignalR 的公用程式，將效能計數器新增至伺服器。</span><span class="sxs-lookup"><span data-stu-id="f74ef-178">Performance counters can be added to the server using a utility called SignalR.exe.</span></span> <span data-ttu-id="f74ef-179">若要安裝此公用程式，請遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="f74ef-179">To install this utility, follow these steps:</span></span>

1. <span data-ttu-id="f74ef-180">在 Visual Studio 中，選取 [**工具**] [ > **nuget 套件管理員**] > [**管理解決方案的 nuget 套件**]</span><span class="sxs-lookup"><span data-stu-id="f74ef-180">In Visual Studio, select **Tools** > **NuGet Package Manager** > **Manage NuGet Packages for Solution**</span></span>
2. <span data-ttu-id="f74ef-181">搜尋**signalr utils**，然後選取 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="f74ef-181">Search for **signalr.utils**, and select Install.</span></span>

    ![](signalr-performance/_static/image1.png)
3. <span data-ttu-id="f74ef-182">接受授權合約以安裝套件。</span><span class="sxs-lookup"><span data-stu-id="f74ef-182">Accept the license agreement to install the package.</span></span>
4. <span data-ttu-id="f74ef-183">SignalR 會安裝到 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`。</span><span class="sxs-lookup"><span data-stu-id="f74ef-183">SignalR.exe will be installed to `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`.</span></span>

### <a name="installing-performance-counters-with-signalrexe"></a><span data-ttu-id="f74ef-184">使用 SignalR 安裝效能計數器</span><span class="sxs-lookup"><span data-stu-id="f74ef-184">Installing performance counters with SignalR.exe</span></span>

<span data-ttu-id="f74ef-185">若要安裝 SignalR 效能計數器，請在提升許可權的命令提示字元中，使用下列參數執行 SignalR：</span><span class="sxs-lookup"><span data-stu-id="f74ef-185">To install SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

<span data-ttu-id="f74ef-186">若要移除 SignalR 效能計數器，請在提升許可權的命令提示字元中，使用下列參數執行 SignalR：</span><span class="sxs-lookup"><span data-stu-id="f74ef-186">To remove SignalR performance counters, run SignalR.exe in an elevated command prompt with the following parameter:</span></span>

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a><span data-ttu-id="f74ef-187">SignalR 效能計數器</span><span class="sxs-lookup"><span data-stu-id="f74ef-187">SignalR Performance counters</span></span>

<span data-ttu-id="f74ef-188">公用程式套件會安裝下列效能計數器。</span><span class="sxs-lookup"><span data-stu-id="f74ef-188">The utilities package installs the following performance counters.</span></span> <span data-ttu-id="f74ef-189">「總計」計數器會測量自上一個應用程式集區或伺服器重新開機之後的事件數目。</span><span class="sxs-lookup"><span data-stu-id="f74ef-189">The "Total" counters measure the number of events since the last application pool or server restart.</span></span>

<span data-ttu-id="f74ef-190">**連接計量**</span><span class="sxs-lookup"><span data-stu-id="f74ef-190">**Connection metrics**</span></span>

<span data-ttu-id="f74ef-191">下列計量會測量發生的連線存留期事件。</span><span class="sxs-lookup"><span data-stu-id="f74ef-191">The following metrics measure the connection lifetime events that occur.</span></span> <span data-ttu-id="f74ef-192">如需詳細資訊，請參閱[瞭解和處理連接存留期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-192">For more information, see [Understanding and Handling Connection Lifetime Events](../guide-to-the-api/handling-connection-lifetime-events.md).</span></span>

- <span data-ttu-id="f74ef-193">**連接的連線**</span><span class="sxs-lookup"><span data-stu-id="f74ef-193">**Connections Connected**</span></span>
- <span data-ttu-id="f74ef-194">**連接重新連接**</span><span class="sxs-lookup"><span data-stu-id="f74ef-194">**Connections Reconnected**</span></span>
- <span data-ttu-id="f74ef-195">**連線中斷連接**</span><span class="sxs-lookup"><span data-stu-id="f74ef-195">**Connections Disconnected**</span></span>
- <span data-ttu-id="f74ef-196">**目前的連線數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-196">**Connections Current**</span></span>

<span data-ttu-id="f74ef-197">**訊息計量**</span><span class="sxs-lookup"><span data-stu-id="f74ef-197">**Message metrics**</span></span>

<span data-ttu-id="f74ef-198">下列計量會測量 SignalR 所產生的訊息流量。</span><span class="sxs-lookup"><span data-stu-id="f74ef-198">The following metrics measure the message traffic generated by SignalR.</span></span>

- <span data-ttu-id="f74ef-199">**已接收的連接訊息總數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-199">**Connection Messages Received Total**</span></span>
- <span data-ttu-id="f74ef-200">**已傳送的連接訊息總數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-200">**Connection Messages Sent Total**</span></span>
- <span data-ttu-id="f74ef-201">**接收的連接訊息數/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-201">**Connection Messages Received/Sec**</span></span>
- <span data-ttu-id="f74ef-202">**傳送的連接訊息數/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-202">**Connection Messages Sent/Sec**</span></span>

<span data-ttu-id="f74ef-203">**訊息匯流排計量**</span><span class="sxs-lookup"><span data-stu-id="f74ef-203">**Message bus metrics**</span></span>

<span data-ttu-id="f74ef-204">下列計量會測量透過內部 SignalR 訊息匯流排的流量，這是放置所有傳入和傳出 SignalR 訊息的佇列。</span><span class="sxs-lookup"><span data-stu-id="f74ef-204">The following metrics measure traffic through the internal SignalR message bus, the queue in which all incoming and outgoing SignalR messages are placed.</span></span> <span data-ttu-id="f74ef-205">訊息會在傳送或廣播時**發行**。</span><span class="sxs-lookup"><span data-stu-id="f74ef-205">A message is **Published** when it is sent or broadcast.</span></span> <span data-ttu-id="f74ef-206">此內容中的**訂閱者**是訊息匯流排上的訂用帳戶;這應該等於用戶端的數目加上伺服器本身。</span><span class="sxs-lookup"><span data-stu-id="f74ef-206">A **Subscriber** in this context is a subscription on the message bus; this should equal the number of clients plus the server itself.</span></span> <span data-ttu-id="f74ef-207">配置的背景**工作**是將資料傳送至使用中連線的元件;**忙碌的工作者**就是主動傳送訊息的背景工作。</span><span class="sxs-lookup"><span data-stu-id="f74ef-207">An **Allocated Worker** is a component that sends data to active connections; a **Busy Worker** is one that is actively sending a message.</span></span>

- <span data-ttu-id="f74ef-208">**訊息匯流排接收的訊息總數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-208">**Message Bus Messages Received Total**</span></span>
- <span data-ttu-id="f74ef-209">**訊息匯流排接收訊息數/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-209">**Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="f74ef-210">**訊息匯流排訊息已發佈總數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-210">**Message Bus Messages Published Total**</span></span>
- <span data-ttu-id="f74ef-211">**已發佈的訊息匯流排訊息數/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-211">**Message Bus Messages Published/Sec**</span></span>
- <span data-ttu-id="f74ef-212">**訊息匯流排訂閱者目前**</span><span class="sxs-lookup"><span data-stu-id="f74ef-212">**Message Bus Subscribers Current**</span></span>
- <span data-ttu-id="f74ef-213">**訊息匯流排訂閱者總數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-213">**Message Bus Subscribers Total**</span></span>
- <span data-ttu-id="f74ef-214">**訊息匯流排訂閱者/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-214">**Message Bus Subscribers/Sec**</span></span>
- <span data-ttu-id="f74ef-215">**訊息匯流排配置的背景工作**</span><span class="sxs-lookup"><span data-stu-id="f74ef-215">**Message Bus Allocated Workers**</span></span>
- <span data-ttu-id="f74ef-216">**訊息匯流排忙碌工作者**</span><span class="sxs-lookup"><span data-stu-id="f74ef-216">**Message Bus Busy Workers**</span></span>
- <span data-ttu-id="f74ef-217">**訊息匯流排主題目前**</span><span class="sxs-lookup"><span data-stu-id="f74ef-217">**Message Bus Topics Current**</span></span>

<span data-ttu-id="f74ef-218">**錯誤計量**</span><span class="sxs-lookup"><span data-stu-id="f74ef-218">**Error metrics**</span></span>

<span data-ttu-id="f74ef-219">下列計量會測量 SignalR 訊息流量所產生的錯誤。</span><span class="sxs-lookup"><span data-stu-id="f74ef-219">The following metrics measure errors generated by SignalR message traffic.</span></span> <span data-ttu-id="f74ef-220">無法解析中樞或中樞方法時，會發生**中樞解析**錯誤。</span><span class="sxs-lookup"><span data-stu-id="f74ef-220">**Hub Resolution** errors occur when a hub or hub method cannot be resolved.</span></span> <span data-ttu-id="f74ef-221">**中樞調用**錯誤是叫用中樞方法時擲回的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="f74ef-221">**Hub Invocation** errors are exceptions thrown while invoking a hub method.</span></span> <span data-ttu-id="f74ef-222">**傳輸**錯誤是在 HTTP 要求或回應期間擲回的連接錯誤。</span><span class="sxs-lookup"><span data-stu-id="f74ef-222">**Transport** errors are connection errors thrown during an HTTP request or response.</span></span>

- <span data-ttu-id="f74ef-223">**錯誤：所有總計**</span><span class="sxs-lookup"><span data-stu-id="f74ef-223">**Errors: All Total**</span></span>
- <span data-ttu-id="f74ef-224">**錯誤：全部/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-224">**Errors: All/Sec**</span></span>
- <span data-ttu-id="f74ef-225">**錯誤：中樞解析總計**</span><span class="sxs-lookup"><span data-stu-id="f74ef-225">**Errors: Hub Resolution Total**</span></span>
- <span data-ttu-id="f74ef-226">**錯誤：中樞解析/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-226">**Errors: Hub Resolution/Sec**</span></span>
- <span data-ttu-id="f74ef-227">**錯誤：中樞調用總數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-227">**Errors: Hub Invocation Total**</span></span>
- <span data-ttu-id="f74ef-228">**錯誤：中樞調用/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-228">**Errors: Hub Invocation/Sec**</span></span>
- <span data-ttu-id="f74ef-229">**錯誤：傳輸總數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-229">**Errors: Transport Total**</span></span>
- <span data-ttu-id="f74ef-230">**錯誤：傳輸/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-230">**Errors: Transport/Sec**</span></span>

<a id="scaleout_metrics"></a>

<span data-ttu-id="f74ef-231">**向外延展計量**</span><span class="sxs-lookup"><span data-stu-id="f74ef-231">**Scaleout metrics**</span></span>

<span data-ttu-id="f74ef-232">下列計量會測量向外延展提供者所產生的流量和錯誤。</span><span class="sxs-lookup"><span data-stu-id="f74ef-232">The following metrics measure traffic and errors generated by the scaleout provider.</span></span> <span data-ttu-id="f74ef-233">此內容中的**資料流程**是向外延展提供者所使用的縮放單位;這是使用 SQL Server 時的資料表、使用服務匯流排的主題，以及使用 Redis 的訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="f74ef-233">A **Stream** in this context is a scale unit used by the scaleout provider; this is a table if SQL Server is used, a Topic if Service Bus is used, and a Subscription if Redis is used.</span></span> <span data-ttu-id="f74ef-234">每個資料流程都會確保已排序的讀取和寫入作業;單一資料流程是潛在的調整瓶頸，因此可以增加串流數，以協助降低瓶頸。</span><span class="sxs-lookup"><span data-stu-id="f74ef-234">Each stream ensures ordered read and write operations; a single stream is a potential scale bottleneck, so the number of streams can be increased to help reduce that bottleneck.</span></span> <span data-ttu-id="f74ef-235">如果使用多個資料流程，SignalR 會以確保從任何指定的連線傳送訊息的方式，自動在這些資料流程之間散發（分區）訊息。</span><span class="sxs-lookup"><span data-stu-id="f74ef-235">If multiple streams are used, SignalR will automatically distribute (shard) messages across these streams in a way that ensures messages sent from any given connection are in order.</span></span>

<span data-ttu-id="f74ef-236">[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)設定會控制 SignalR 所維護的向外延展傳送佇列長度。</span><span class="sxs-lookup"><span data-stu-id="f74ef-236">The [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx) setting controls the length of the scaleout send queue maintained by SignalR.</span></span> <span data-ttu-id="f74ef-237">將它設定為大於0的值，會將傳送佇列中的所有訊息一次傳送至設定的訊息後擋板。</span><span class="sxs-lookup"><span data-stu-id="f74ef-237">Setting it to a value greater than 0 will place all messages in a send queue to be sent one at a time to the configured messaging backplane.</span></span> <span data-ttu-id="f74ef-238">如果佇列的大小超過設定的長度，後續的傳送呼叫將會立即失敗，並傳回[InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ，直到佇列中的訊息數目小於設定。</span><span class="sxs-lookup"><span data-stu-id="f74ef-238">If the size of the queue goes above the configured length, subsequent calls to send will fail immediately with an [InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) until the number of messages in the queue is less than the setting again.</span></span> <span data-ttu-id="f74ef-239">預設會停用佇列，因為實作的背板通常會有自己的佇列或流量控制。</span><span class="sxs-lookup"><span data-stu-id="f74ef-239">Queueing is disabled by default because the implemented backplanes generally have their own queuing or flow-control in place.</span></span> <span data-ttu-id="f74ef-240">在 SQL Server 的情況下，連接共用會有效限制一次傳入的傳送數目。</span><span class="sxs-lookup"><span data-stu-id="f74ef-240">In the case of SQL Server, connection pooling effectively limits the number of sends going on at any one time.</span></span>

<span data-ttu-id="f74ef-241">根據預設，只有一個資料流程會用於 SQL Server 和 Redis，而五個串流用於服務匯流排，而佇列已停用，但您可以透過 SQL Server 和服務匯流排上的設定來變更這些設定：</span><span class="sxs-lookup"><span data-stu-id="f74ef-241">By default, only one stream is used for SQL Server and Redis, five streams are used for Service Bus, and queueing is disabled, but these settings can be changed through configuration on SQL Server and Service Bus:</span></span>

<span data-ttu-id="f74ef-242">**用於設定 SQL Server 背板之資料表計數和佇列長度的 .NET 伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="f74ef-242">**.NET Server Code for configuring table count and queue length for SQL Server backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

<span data-ttu-id="f74ef-243">**用於設定服務匯流排背板之主題計數和佇列長度的 .NET 伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="f74ef-243">**.NET Server Code for configuring topic count and queue length for Service Bus backplane**</span></span>

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

<span data-ttu-id="f74ef-244">**緩衝**資料流程是進入錯誤狀態的一個，當資料流程處於「錯誤」狀態時，所有傳送至後擋板的訊息都會立即失敗，直到資料流程不再出錯為止。</span><span class="sxs-lookup"><span data-stu-id="f74ef-244">A **Buffering** stream is one that has entered a faulted state; when the stream is in the faulted state, all messages sent to the backplane will fail immediately until the stream is no longer faulting.</span></span> <span data-ttu-id="f74ef-245">**傳送佇列長度**是已張貼但尚未傳送的郵件數目。</span><span class="sxs-lookup"><span data-stu-id="f74ef-245">The **Send Queue Length** is the number of messages that have been posted but not yet sent.</span></span>

- <span data-ttu-id="f74ef-246">**向外延展接收的訊息匯流排訊息數/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-246">**Scaleout Message Bus Messages Received/Sec**</span></span>
- <span data-ttu-id="f74ef-247">**向外延展資料流程總計**</span><span class="sxs-lookup"><span data-stu-id="f74ef-247">**Scaleout Streams Total**</span></span>
- <span data-ttu-id="f74ef-248">**開啟的向外延展資料流程**</span><span class="sxs-lookup"><span data-stu-id="f74ef-248">**Scaleout Streams Open**</span></span>
- <span data-ttu-id="f74ef-249">**向外延展串流緩衝處理**</span><span class="sxs-lookup"><span data-stu-id="f74ef-249">**Scaleout Streams Buffering**</span></span>
- <span data-ttu-id="f74ef-250">**向外延展錯誤總數**</span><span class="sxs-lookup"><span data-stu-id="f74ef-250">**Scaleout Errors Total**</span></span>
- <span data-ttu-id="f74ef-251">**向外延展錯誤數/秒**</span><span class="sxs-lookup"><span data-stu-id="f74ef-251">**Scaleout Errors/Sec**</span></span>
- <span data-ttu-id="f74ef-252">**向外延展傳送佇列長度**</span><span class="sxs-lookup"><span data-stu-id="f74ef-252">**Scaleout Send Queue Length**</span></span>

<span data-ttu-id="f74ef-253">如需這些計數器測量之內容的詳細資訊，請參閱[SignalR 向外延展 with Azure 服務匯流排](scaleout-with-windows-azure-service-bus.md)。</span><span class="sxs-lookup"><span data-stu-id="f74ef-253">For more information on what these counters are measuring, see [SignalR Scaleout with Azure Service Bus](scaleout-with-windows-azure-service-bus.md).</span></span>

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a><span data-ttu-id="f74ef-254">使用其他效能計數器</span><span class="sxs-lookup"><span data-stu-id="f74ef-254">Using other performance counters</span></span>

<span data-ttu-id="f74ef-255">下列效能計數器可能也有助於監視應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="f74ef-255">The following performance counters may also be useful in monitoring your application's performance.</span></span>

<span data-ttu-id="f74ef-256">**記憶體**</span><span class="sxs-lookup"><span data-stu-id="f74ef-256">**Memory**</span></span>

- <span data-ttu-id="f74ef-257">.NET CLR 記憶體\\所有堆積中的 # 個位元組（適用于 w3wp.exe）</span><span class="sxs-lookup"><span data-stu-id="f74ef-257">.NET CLR Memory\\# bytes in all Heaps (for w3wp)</span></span>

<span data-ttu-id="f74ef-258">**ASP.NET**</span><span class="sxs-lookup"><span data-stu-id="f74ef-258">**ASP.NET**</span></span>

- <span data-ttu-id="f74ef-259">ASP. NET\Requests Current</span><span class="sxs-lookup"><span data-stu-id="f74ef-259">ASP.NET\Requests Current</span></span>
- <span data-ttu-id="f74ef-260">ASP. NET\Queued</span><span class="sxs-lookup"><span data-stu-id="f74ef-260">ASP.NET\Queued</span></span>
- <span data-ttu-id="f74ef-261">ASP. NET\Rejected</span><span class="sxs-lookup"><span data-stu-id="f74ef-261">ASP.NET\Rejected</span></span>

<span data-ttu-id="f74ef-262">**CPU**</span><span class="sxs-lookup"><span data-stu-id="f74ef-262">**CPU**</span></span>

- <span data-ttu-id="f74ef-263">處理器 Information\Processor 時間</span><span class="sxs-lookup"><span data-stu-id="f74ef-263">Processor Information\Processor Time</span></span>

<span data-ttu-id="f74ef-264">**TCP/IP**</span><span class="sxs-lookup"><span data-stu-id="f74ef-264">**TCP/IP**</span></span>

- <span data-ttu-id="f74ef-265">已建立 TCPv6/Connections</span><span class="sxs-lookup"><span data-stu-id="f74ef-265">TCPv6/Connections Established</span></span>
- <span data-ttu-id="f74ef-266">已建立 Tcpv4 已/Connections</span><span class="sxs-lookup"><span data-stu-id="f74ef-266">TCPv4/Connections Established</span></span>

<span data-ttu-id="f74ef-267">**Web 服務**</span><span class="sxs-lookup"><span data-stu-id="f74ef-267">**Web Service**</span></span>

- <span data-ttu-id="f74ef-268">Web Service\current connections 連接</span><span class="sxs-lookup"><span data-stu-id="f74ef-268">Web Service\Current Connections</span></span>
- <span data-ttu-id="f74ef-269">Web Service\Maximum 連接</span><span class="sxs-lookup"><span data-stu-id="f74ef-269">Web Service\Maximum Connections</span></span>

<span data-ttu-id="f74ef-270">**執行緒處理**</span><span class="sxs-lookup"><span data-stu-id="f74ef-270">**Threading**</span></span>

- <span data-ttu-id="f74ef-271">.NET CLR 鎖定和執行緒\\# 個目前的邏輯執行緒</span><span class="sxs-lookup"><span data-stu-id="f74ef-271">.NET CLR Locks And Threads\\# of current logical Threads</span></span>
- <span data-ttu-id="f74ef-272">.NET CLR 鎖定和執行緒\\目前的實體執行緒數目</span><span class="sxs-lookup"><span data-stu-id="f74ef-272">.NET CLR Locks And Threads\\# of current physical Threads</span></span>

<a id="otherresources"></a>

## <a name="other-resources"></a><span data-ttu-id="f74ef-273">其他資源</span><span class="sxs-lookup"><span data-stu-id="f74ef-273">Other Resources</span></span>

<span data-ttu-id="f74ef-274">如需有關 ASP.NET 效能監視和微調的詳細資訊，請參閱下列主題：</span><span class="sxs-lookup"><span data-stu-id="f74ef-274">For more information on ASP.NET performance monitoring and tuning, see the following topics:</span></span>

- <span data-ttu-id="f74ef-275">[ASP.NET 效能概觀](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span><span class="sxs-lookup"><span data-stu-id="f74ef-275">[ASP.NET Performance Overview](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)</span></span>
- [<span data-ttu-id="f74ef-276">在 IIS 7.5、IIS 7.0 和 IIS 6.0 上 ASP.NET 執行緒使用方式</span><span class="sxs-lookup"><span data-stu-id="f74ef-276">ASP.NET Thread Usage on IIS 7.5, IIS 7.0, and IIS 6.0</span></span>](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [<span data-ttu-id="f74ef-277">&lt;applicationPool&gt; 元素（Web 設定）</span><span class="sxs-lookup"><span data-stu-id="f74ef-277">&lt;applicationPool&gt; Element (Web Settings)</span></span>](https://msdn.microsoft.com/library/dd560842.aspx)
