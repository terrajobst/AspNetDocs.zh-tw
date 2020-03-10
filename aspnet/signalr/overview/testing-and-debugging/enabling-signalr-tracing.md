---
uid: signalr/overview/testing-and-debugging/enabling-signalr-tracing
title: 啟用 SignalR 追蹤 |Microsoft Docs
author: bradygaster
description: 本檔說明如何啟用及設定 SignalR 伺服器和用戶端的追蹤。 追蹤可讓您查看事件的相關診斷資訊 。
ms.author: bradyg
ms.date: 08/08/2014
ms.assetid: 30060acb-be3e-4347-996f-3870f0c37829
msc.legacyurl: /signalr/overview/testing-and-debugging/enabling-signalr-tracing
msc.type: authoredcontent
ms.openlocfilehash: 34fe2cdb10c4b41a6e8cac7fb1741d53c02dfc80
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578831"
---
# <a name="enabling-signalr-tracing"></a><span data-ttu-id="b64c7-104">啟用 SignalR 追蹤</span><span class="sxs-lookup"><span data-stu-id="b64c7-104">Enabling SignalR Tracing</span></span>

<span data-ttu-id="b64c7-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b64c7-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="b64c7-106">本檔說明如何啟用及設定 SignalR 伺服器和用戶端的追蹤。</span><span class="sxs-lookup"><span data-stu-id="b64c7-106">This document describes how to enable and configure tracing for SignalR servers and clients.</span></span> <span data-ttu-id="b64c7-107">追蹤可讓您在 SignalR 應用程式中，查看事件的相關診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="b64c7-107">Tracing enables you to view diagnostic information about events in your SignalR application.</span></span>
>
> <span data-ttu-id="b64c7-108">本主題原本是由一 Fletcher 的一節所撰寫。</span><span class="sxs-lookup"><span data-stu-id="b64c7-108">This topic was originally written by Patrick Fletcher.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b64c7-109">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="b64c7-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="b64c7-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="b64c7-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="b64c7-111">.NET Framework 4.5</span><span class="sxs-lookup"><span data-stu-id="b64c7-111">.NET Framework 4.5</span></span>
> - <span data-ttu-id="b64c7-112">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="b64c7-112">SignalR version 2</span></span>
>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="b64c7-113">問題與意見</span><span class="sxs-lookup"><span data-stu-id="b64c7-113">Questions and comments</span></span>
>
> <span data-ttu-id="b64c7-114">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="b64c7-114">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="b64c7-115">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="b64c7-115">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="b64c7-116">啟用追蹤時，SignalR 應用程式會建立事件的記錄專案。</span><span class="sxs-lookup"><span data-stu-id="b64c7-116">When tracing is enabled, a SignalR application creates log entries for events.</span></span> <span data-ttu-id="b64c7-117">您可以從用戶端和伺服器記錄事件。</span><span class="sxs-lookup"><span data-stu-id="b64c7-117">You can log events from both the client and the server.</span></span> <span data-ttu-id="b64c7-118">伺服器上的追蹤會記錄連接、向外延展提供者和訊息匯流排事件。</span><span class="sxs-lookup"><span data-stu-id="b64c7-118">Tracing on the server logs connection, scaleout provider, and message bus events.</span></span> <span data-ttu-id="b64c7-119">在用戶端上追蹤記錄連接事件。</span><span class="sxs-lookup"><span data-stu-id="b64c7-119">Tracing on the client logs connection events.</span></span> <span data-ttu-id="b64c7-120">在 SignalR 2.1 和更新版本中，用戶端上的追蹤會記錄中樞調用訊息的完整內容。</span><span class="sxs-lookup"><span data-stu-id="b64c7-120">In SignalR 2.1 and later, tracing on the client logs the full content of hub invocation messages.</span></span>

## <a name="contents"></a><span data-ttu-id="b64c7-121">內容</span><span class="sxs-lookup"><span data-stu-id="b64c7-121">Contents</span></span>

- [<span data-ttu-id="b64c7-122">在伺服器上啟用追蹤</span><span class="sxs-lookup"><span data-stu-id="b64c7-122">Enabling tracing on the server</span></span>](#server)

    - [<span data-ttu-id="b64c7-123">將伺服器事件記錄到文字檔</span><span class="sxs-lookup"><span data-stu-id="b64c7-123">Logging server events to text files</span></span>](#server_text)
    - [<span data-ttu-id="b64c7-124">將伺服器事件記錄到事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="b64c7-124">Logging server events to the event log</span></span>](#server_eventlog)
- [<span data-ttu-id="b64c7-125">在 .NET 用戶端中啟用追蹤（Windows 桌面應用程式）</span><span class="sxs-lookup"><span data-stu-id="b64c7-125">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>](#net_client)

    - [<span data-ttu-id="b64c7-126">將桌面用戶端事件記錄到主控台</span><span class="sxs-lookup"><span data-stu-id="b64c7-126">Logging Desktop client events to the console</span></span>](#desktop_console)
    - [<span data-ttu-id="b64c7-127">將桌面用戶端事件記錄到文字檔</span><span class="sxs-lookup"><span data-stu-id="b64c7-127">Logging Desktop client events to a text file</span></span>](#desktop_text)
- [<span data-ttu-id="b64c7-128">在 Windows Phone 8 用戶端中啟用追蹤</span><span class="sxs-lookup"><span data-stu-id="b64c7-128">Enabling tracing in Windows Phone 8 clients</span></span>](#phone)

    - [<span data-ttu-id="b64c7-129">將 Windows Phone 用戶端事件記錄至 UI</span><span class="sxs-lookup"><span data-stu-id="b64c7-129">Logging Windows Phone client events to the UI</span></span>](#phone_ui)
    - [<span data-ttu-id="b64c7-130">將 Windows Phone 用戶端事件記錄到調試主控台</span><span class="sxs-lookup"><span data-stu-id="b64c7-130">Logging Windows Phone client events to the debug console</span></span>](#phone_debug)
- [<span data-ttu-id="b64c7-131">在 JavaScript 用戶端中啟用追蹤</span><span class="sxs-lookup"><span data-stu-id="b64c7-131">Enabling tracing in the JavaScript client</span></span>](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a><span data-ttu-id="b64c7-132">在伺服器上啟用追蹤</span><span class="sxs-lookup"><span data-stu-id="b64c7-132">Enabling tracing on the server</span></span>

<span data-ttu-id="b64c7-133">您會在應用程式的設定檔（App.config 或 web.config，視專案類型而定）中啟用伺服器上的追蹤。您可以指定要記錄的事件類別。</span><span class="sxs-lookup"><span data-stu-id="b64c7-133">You enable tracing on the server within the application's configuration file (either App.config or Web.config depending on the type of project.) You specify which categories of events you want to log.</span></span> <span data-ttu-id="b64c7-134">在設定檔中，您也可以指定是否要使用[TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)的執行，將事件記錄到文字檔、Windows 事件記錄檔或自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b64c7-134">In the configuration file, you also specify whether to log the events to a text file, the Windows event log, or a custom log using an implementation of [TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx).</span></span>

<span data-ttu-id="b64c7-135">伺服器事件類別目錄包含下列各種訊息：</span><span class="sxs-lookup"><span data-stu-id="b64c7-135">The server event categories include the following sorts of messages:</span></span>

| <span data-ttu-id="b64c7-136">原始程式檔</span><span class="sxs-lookup"><span data-stu-id="b64c7-136">Source</span></span> | <span data-ttu-id="b64c7-137">訊息</span><span class="sxs-lookup"><span data-stu-id="b64c7-137">Messages</span></span> |
| --- | --- |
| <span data-ttu-id="b64c7-138">SignalR. SqlMessageBus</span><span class="sxs-lookup"><span data-stu-id="b64c7-138">SignalR.SqlMessageBus</span></span> | <span data-ttu-id="b64c7-139">SQL 訊息匯流排向外延展提供者安裝程式、資料庫作業、錯誤和超時事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-139">SQL Message Bus scaleout provider setup, database operation, error, and timeout events</span></span> |
| <span data-ttu-id="b64c7-140">SignalR. ServiceBusMessageBus</span><span class="sxs-lookup"><span data-stu-id="b64c7-140">SignalR.ServiceBusMessageBus</span></span> | <span data-ttu-id="b64c7-141">服務匯流排向外延展提供者主題建立和訂用帳戶、錯誤和訊息事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-141">Service bus scaleout provider topic creation and subscription, error, and messaging events</span></span> |
| <span data-ttu-id="b64c7-142">SignalR. RedisMessageBus</span><span class="sxs-lookup"><span data-stu-id="b64c7-142">SignalR.RedisMessageBus</span></span> | <span data-ttu-id="b64c7-143">Redis 向外延展提供者連線、中斷連接和錯誤事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-143">Redis scaleout provider connection, disconnection, and error events</span></span> |
| <span data-ttu-id="b64c7-144">SignalR. ScaleoutMessageBus</span><span class="sxs-lookup"><span data-stu-id="b64c7-144">SignalR.ScaleoutMessageBus</span></span> | <span data-ttu-id="b64c7-145">向外延展訊息事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-145">Scaleout messaging events</span></span> |
| <span data-ttu-id="b64c7-146">SignalR. WebSocketTransport</span><span class="sxs-lookup"><span data-stu-id="b64c7-146">SignalR.Transports.WebSocketTransport</span></span> | <span data-ttu-id="b64c7-147">WebSocket 傳輸連線、中斷連線、訊息和錯誤事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-147">WebSocket transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="b64c7-148">SignalR. ServerSentEventsTransport</span><span class="sxs-lookup"><span data-stu-id="b64c7-148">SignalR.Transports.ServerSentEventsTransport</span></span> | <span data-ttu-id="b64c7-149">ServerSentEvents 傳輸連接、中斷連線、訊息和錯誤事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-149">ServerSentEvents transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="b64c7-150">SignalR. ForeverFrameTransport</span><span class="sxs-lookup"><span data-stu-id="b64c7-150">SignalR.Transports.ForeverFrameTransport</span></span> | <span data-ttu-id="b64c7-151">ForeverFrame 傳輸連接、中斷連線、訊息和錯誤事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-151">ForeverFrame transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="b64c7-152">SignalR. LongPollingTransport</span><span class="sxs-lookup"><span data-stu-id="b64c7-152">SignalR.Transports.LongPollingTransport</span></span> | <span data-ttu-id="b64c7-153">LongPolling 傳輸連接、中斷連線、訊息和錯誤事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-153">LongPolling transport connection, disconnection, messaging, and error events</span></span> |
| <span data-ttu-id="b64c7-154">SignalR. TransportHeartBeat</span><span class="sxs-lookup"><span data-stu-id="b64c7-154">SignalR.Transports.TransportHeartBeat</span></span> | <span data-ttu-id="b64c7-155">傳輸連線、中斷連接和 keepalive 事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-155">Transport connection, disconnection, and keepalive events</span></span> |
| <span data-ttu-id="b64c7-156">SignalR. ReflectedHubDescriptorProvider</span><span class="sxs-lookup"><span data-stu-id="b64c7-156">SignalR.ReflectedHubDescriptorProvider</span></span> | <span data-ttu-id="b64c7-157">中樞探索事件</span><span class="sxs-lookup"><span data-stu-id="b64c7-157">Hub discovery events</span></span> |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a><span data-ttu-id="b64c7-158">將伺服器事件記錄到文字檔</span><span class="sxs-lookup"><span data-stu-id="b64c7-158">Logging server events to text files</span></span>

<span data-ttu-id="b64c7-159">下列程式碼示範如何為每個事件類別目錄啟用追蹤。</span><span class="sxs-lookup"><span data-stu-id="b64c7-159">The following code shows how to enable tracing for each category of event.</span></span> <span data-ttu-id="b64c7-160">這個範例會將應用程式設定為將事件記錄到文字檔。</span><span class="sxs-lookup"><span data-stu-id="b64c7-160">This sample configures the application to log events to text files.</span></span>

<span data-ttu-id="b64c7-161">**用於啟用追蹤的 XML 伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="b64c7-161">**XML server code for enabling tracing**</span></span>

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

<span data-ttu-id="b64c7-162">在上述程式碼中，`SignalRSwitch` 專案會指定用於傳送至指定記錄之事件的[TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) 。</span><span class="sxs-lookup"><span data-stu-id="b64c7-162">In the code above, the `SignalRSwitch` entry specifies the [TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) used for events sent to the specified log.</span></span> <span data-ttu-id="b64c7-163">在此情況下，它會設定為 `Verbose` 這表示會記錄所有的調試和追蹤訊息。</span><span class="sxs-lookup"><span data-stu-id="b64c7-163">In this case, it is set to `Verbose` which means all debugging and tracing messages are logged.</span></span>

<span data-ttu-id="b64c7-164">下列輸出會顯示使用上述設定檔之應用程式的 `transports.log.txt` 檔案中的專案。</span><span class="sxs-lookup"><span data-stu-id="b64c7-164">The following output shows entries from the `transports.log.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="b64c7-165">它會顯示新的連接、已移除的連接，以及傳輸的事件。</span><span class="sxs-lookup"><span data-stu-id="b64c7-165">It shows a new connection, a removed connection, and transport heartbeat events.</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a><span data-ttu-id="b64c7-166">將伺服器事件記錄到事件記錄檔</span><span class="sxs-lookup"><span data-stu-id="b64c7-166">Logging server events to the event log</span></span>

<span data-ttu-id="b64c7-167">若要將事件記錄到事件記錄檔，而不是文字檔，請變更 [`sharedListeners`] 節點中專案的值。</span><span class="sxs-lookup"><span data-stu-id="b64c7-167">To log events to the event log rather than a text file, change the values for the entries in the `sharedListeners` node.</span></span> <span data-ttu-id="b64c7-168">下列程式碼顯示如何將伺服器事件記錄到事件記錄檔：</span><span class="sxs-lookup"><span data-stu-id="b64c7-168">The following code shows how to log server events to the event log:</span></span>

<span data-ttu-id="b64c7-169">**將事件記錄到事件記錄檔的 XML 伺服器程式碼**</span><span class="sxs-lookup"><span data-stu-id="b64c7-169">**XML server code for logging events to the event log**</span></span>

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

<span data-ttu-id="b64c7-170">事件會記錄在應用程式記錄檔中，並可透過事件檢視器取得，如下所示：</span><span class="sxs-lookup"><span data-stu-id="b64c7-170">The events are logged in the Application log, and are available through the Event Viewer, as shown below:</span></span>

![顯示 SignalR 記錄的事件檢視器](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> <span data-ttu-id="b64c7-172">使用事件記錄檔時，請將**TraceLevel**設定為**Error** ，以保持可管理的訊息數目。</span><span class="sxs-lookup"><span data-stu-id="b64c7-172">When using the event log, set the **TraceLevel** to **Error** to keep the number of messages manageable.</span></span>

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a><span data-ttu-id="b64c7-173">在 .NET 用戶端中啟用追蹤（Windows 桌面應用程式）</span><span class="sxs-lookup"><span data-stu-id="b64c7-173">Enabling tracing in the .NET client (Windows Desktop apps)</span></span>

<span data-ttu-id="b64c7-174">.NET 用戶端可以將事件記錄到主控台、文字檔，或使用執行[檔的實](https://msdn.microsoft.com/library/system.io.textwriter.aspx)作為自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="b64c7-174">The .NET client can log events to the console, a text file, or to a custom log using an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx).</span></span>

<span data-ttu-id="b64c7-175">若要在 .NET 用戶端中啟用記錄，請將連接的 `TraceLevel` 屬性設定為[TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx)值，並將 `TraceWriter` 屬性設[為有效的](https://msdn.microsoft.com/library/system.io.textwriter.aspx)[無效] 實例。</span><span class="sxs-lookup"><span data-stu-id="b64c7-175">To enable logging in the .NET client, set the connection's `TraceLevel` property to a [TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx) value, and the `TraceWriter` property to a valid [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter.aspx) instance.</span></span>

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a><span data-ttu-id="b64c7-176">將桌面用戶端事件記錄到主控台</span><span class="sxs-lookup"><span data-stu-id="b64c7-176">Logging Desktop client events to the console</span></span>

<span data-ttu-id="b64c7-177">下列C#程式碼說明如何將 .net 用戶端中的事件記錄到主控台：</span><span class="sxs-lookup"><span data-stu-id="b64c7-177">The following C# code shows how to log events in the .NET client to the console:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a><span data-ttu-id="b64c7-178">將桌面用戶端事件記錄到文字檔</span><span class="sxs-lookup"><span data-stu-id="b64c7-178">Logging Desktop client events to a text file</span></span>

<span data-ttu-id="b64c7-179">下列C#程式碼顯示如何將 .net 用戶端中的事件記錄到文字檔：</span><span class="sxs-lookup"><span data-stu-id="b64c7-179">The following C# code shows how to log events in the .NET client to a text file:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

<span data-ttu-id="b64c7-180">下列輸出會顯示使用上述設定檔之應用程式的 `ClientLog.txt` 檔案中的專案。</span><span class="sxs-lookup"><span data-stu-id="b64c7-180">The following output shows entries from the `ClientLog.txt` file for an application using the above configuration file.</span></span> <span data-ttu-id="b64c7-181">它會顯示連接到伺服器的用戶端，而中樞會叫用名為 `addMessage`的用戶端方法：</span><span class="sxs-lookup"><span data-stu-id="b64c7-181">It shows the client connecting to the server, and the hub invoking a client method called `addMessage`:</span></span>

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a><span data-ttu-id="b64c7-182">在 Windows Phone 8 用戶端中啟用追蹤</span><span class="sxs-lookup"><span data-stu-id="b64c7-182">Enabling tracing in Windows Phone 8 clients</span></span>

<span data-ttu-id="b64c7-183">Windows Phone 應用程式的 SignalR 應用程式會使用與桌面應用程式相同的 .NET 用戶端，但不提供使用[StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)的[檔案和寫入](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx)檔案的功能。</span><span class="sxs-lookup"><span data-stu-id="b64c7-183">SignalR applications for Windows Phone apps use the same .NET client as desktop apps, but [Console.Out](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx) and writing to a file with [StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx) are not available.</span></span> <span data-ttu-id="b64c7-184">相反地，您需要為追蹤建立一個自[定義的執行](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="b64c7-184">Instead, you need to create a custom implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) for tracing.</span></span>

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a><span data-ttu-id="b64c7-185">將 Windows Phone 用戶端事件記錄至 UI</span><span class="sxs-lookup"><span data-stu-id="b64c7-185">Logging Windows Phone client events to the UI</span></span>

<span data-ttu-id="b64c7-186">[SignalR 程式碼基](https://github.com/SignalR/SignalR/archive/master.zip)底包含 Windows Phone 範例，其會使用稱為 `TextBlockWriter`[的自訂](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)的執行身分叫用將追蹤輸出寫入至[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="b64c7-186">The [SignalR codebase](https://github.com/SignalR/SignalR/archive/master.zip) includes a Windows Phone sample that writes trace output to a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) using a custom [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) implementation called `TextBlockWriter`.</span></span> <span data-ttu-id="b64c7-187">您可以在**samples/SignalR. WP8 範例**專案中找到這個類別。</span><span class="sxs-lookup"><span data-stu-id="b64c7-187">This class can be found in the **samples/Microsoft.AspNet.SignalR.Client.WP8.Samples** project.</span></span> <span data-ttu-id="b64c7-188">建立 `TextBlockWriter`的實例時，傳入目前的[SynchronizationCoNtext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)和[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) ，其中會建立用於追蹤輸出的[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) ：</span><span class="sxs-lookup"><span data-stu-id="b64c7-188">When creating an instance of `TextBlockWriter`, pass in the current [SynchronizationContext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx), and a [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) where it will create a [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) to use for trace output:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

<span data-ttu-id="b64c7-189">然後追蹤輸出會寫入至您傳入的[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)中建立的新[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) ：</span><span class="sxs-lookup"><span data-stu-id="b64c7-189">The trace output will then be written to a new [TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) created in the [StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) you passed in:</span></span>

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a><span data-ttu-id="b64c7-190">將 Windows Phone 用戶端事件記錄到調試主控台</span><span class="sxs-lookup"><span data-stu-id="b64c7-190">Logging Windows Phone client events to the debug console</span></span>

<span data-ttu-id="b64c7-191">若要將輸出傳送至偵錯工具主控台，而不是 UI，請建立會寫入至 [debug] 視窗，並將它指派給您的連接[TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) [屬性的 [](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)執行器]：</span><span class="sxs-lookup"><span data-stu-id="b64c7-191">To send output to the debug console rather than the UI, create an implementation of [TextWriter](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx) that writes to the debug window, and assign it to your connection's [TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) property:</span></span>

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

<span data-ttu-id="b64c7-192">接著，追蹤資訊會寫入 Visual Studio 中的 [debug] 視窗：</span><span class="sxs-lookup"><span data-stu-id="b64c7-192">Trace information will then be written to the debug window in Visual Studio:</span></span>

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a><span data-ttu-id="b64c7-193">在 JavaScript 用戶端中啟用追蹤</span><span class="sxs-lookup"><span data-stu-id="b64c7-193">Enabling tracing in the JavaScript client</span></span>

<span data-ttu-id="b64c7-194">若要在連接上啟用用戶端記錄，請先在連線物件上設定 `logging` 屬性，再呼叫 `start` 方法來建立連接。</span><span class="sxs-lookup"><span data-stu-id="b64c7-194">To enable client-side logging on a connection, set the `logging` property on the connection object before you call the `start` method to establish the connection.</span></span>

<span data-ttu-id="b64c7-195">**用來啟用瀏覽器主控台追蹤的用戶端 JavaScript 程式碼（使用產生的 proxy）**</span><span class="sxs-lookup"><span data-stu-id="b64c7-195">**Client JavaScript code for enabling tracing to the browser console (with the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

<span data-ttu-id="b64c7-196">**用來啟用瀏覽器主控台追蹤的用戶端 JavaScript 程式碼（不含產生的 proxy）**</span><span class="sxs-lookup"><span data-stu-id="b64c7-196">**Client JavaScript code for enabling tracing to the browser console (without the generated proxy)**</span></span>

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

<span data-ttu-id="b64c7-197">啟用追蹤時，JavaScript 用戶端會將事件記錄到瀏覽器主控台。</span><span class="sxs-lookup"><span data-stu-id="b64c7-197">When tracing is enabled, the JavaScript client logs events to the browser console.</span></span> <span data-ttu-id="b64c7-198">若要存取瀏覽器主控台，請參閱[監視傳輸](../getting-started/introduction-to-signalr.md#MonitoringTransports)。</span><span class="sxs-lookup"><span data-stu-id="b64c7-198">To access the browser console, see [Monitoring Transports](../getting-started/introduction-to-signalr.md#MonitoringTransports).</span></span>

<span data-ttu-id="b64c7-199">下列螢幕擷取畫面顯示已啟用追蹤的 SignalR JavaScript 用戶端。</span><span class="sxs-lookup"><span data-stu-id="b64c7-199">The following screenshot shows a SignalR JavaScript client with tracing enabled.</span></span> <span data-ttu-id="b64c7-200">它會在瀏覽器主控台中顯示連線和中樞呼叫事件：</span><span class="sxs-lookup"><span data-stu-id="b64c7-200">It shows connection and hub invocation events in the browser console:</span></span>

![在瀏覽器主控台中 SignalR 追蹤事件](enabling-signalr-tracing/_static/image4.png)
