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
# <a name="enabling-signalr-tracing"></a>啟用 SignalR 追蹤

由[Tom FitzMacken](https://github.com/tfitzmac)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本檔說明如何啟用及設定 SignalR 伺服器和用戶端的追蹤。 追蹤可讓您在 SignalR 應用程式中，查看事件的相關診斷資訊。
>
> 本主題原本是由一 Fletcher 的一節所撰寫。
>
> ## <a name="software-versions-used-in-the-tutorial"></a>教學課程中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET Framework 4.5
> - SignalR 第2版
>
>
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

啟用追蹤時，SignalR 應用程式會建立事件的記錄專案。 您可以從用戶端和伺服器記錄事件。 伺服器上的追蹤會記錄連接、向外延展提供者和訊息匯流排事件。 在用戶端上追蹤記錄連接事件。 在 SignalR 2.1 和更新版本中，用戶端上的追蹤會記錄中樞調用訊息的完整內容。

## <a name="contents"></a>內容

- [在伺服器上啟用追蹤](#server)

    - [將伺服器事件記錄到文字檔](#server_text)
    - [將伺服器事件記錄到事件記錄檔](#server_eventlog)
- [在 .NET 用戶端中啟用追蹤（Windows 桌面應用程式）](#net_client)

    - [將桌面用戶端事件記錄到主控台](#desktop_console)
    - [將桌面用戶端事件記錄到文字檔](#desktop_text)
- [在 Windows Phone 8 用戶端中啟用追蹤](#phone)

    - [將 Windows Phone 用戶端事件記錄至 UI](#phone_ui)
    - [將 Windows Phone 用戶端事件記錄到調試主控台](#phone_debug)
- [在 JavaScript 用戶端中啟用追蹤](#javascript)

<a id="server"></a>
## <a name="enabling-tracing-on-the-server"></a>在伺服器上啟用追蹤

您會在應用程式的設定檔（App.config 或 web.config，視專案類型而定）中啟用伺服器上的追蹤。您可以指定要記錄的事件類別。 在設定檔中，您也可以指定是否要使用[TraceListener](https://msdn.microsoft.com/library/system.diagnostics.tracelistener(v=vs.110).aspx)的執行，將事件記錄到文字檔、Windows 事件記錄檔或自訂記錄檔。

伺服器事件類別目錄包含下列各種訊息：

| 原始程式檔 | 訊息 |
| --- | --- |
| SignalR. SqlMessageBus | SQL 訊息匯流排向外延展提供者安裝程式、資料庫作業、錯誤和超時事件 |
| SignalR. ServiceBusMessageBus | 服務匯流排向外延展提供者主題建立和訂用帳戶、錯誤和訊息事件 |
| SignalR. RedisMessageBus | Redis 向外延展提供者連線、中斷連接和錯誤事件 |
| SignalR. ScaleoutMessageBus | 向外延展訊息事件 |
| SignalR. WebSocketTransport | WebSocket 傳輸連線、中斷連線、訊息和錯誤事件 |
| SignalR. ServerSentEventsTransport | ServerSentEvents 傳輸連接、中斷連線、訊息和錯誤事件 |
| SignalR. ForeverFrameTransport | ForeverFrame 傳輸連接、中斷連線、訊息和錯誤事件 |
| SignalR. LongPollingTransport | LongPolling 傳輸連接、中斷連線、訊息和錯誤事件 |
| SignalR. TransportHeartBeat | 傳輸連線、中斷連接和 keepalive 事件 |
| SignalR. ReflectedHubDescriptorProvider | 中樞探索事件 |

<a id="server_text"></a>
### <a name="logging-server-events-to-text-files"></a>將伺服器事件記錄到文字檔

下列程式碼示範如何為每個事件類別目錄啟用追蹤。 這個範例會將應用程式設定為將事件記錄到文字檔。

**用於啟用追蹤的 XML 伺服器程式碼**

[!code-html[Main](enabling-signalr-tracing/samples/sample1.html)]

在上述程式碼中，`SignalRSwitch` 專案會指定用於傳送至指定記錄之事件的[TraceLevel](https://msdn.microsoft.com/library/system.diagnostics.tracelevel(v=vs.110).aspx) 。 在此情況下，它會設定為 `Verbose` 這表示會記錄所有的調試和追蹤訊息。

下列輸出會顯示使用上述設定檔之應用程式的 `transports.log.txt` 檔案中的專案。 它會顯示新的連接、已移除的連接，以及傳輸的事件。

[!code-console[Main](enabling-signalr-tracing/samples/sample2.cmd)]

<a id="server_eventlog"></a>
### <a name="logging-server-events-to-the-event-log"></a>將伺服器事件記錄到事件記錄檔

若要將事件記錄到事件記錄檔，而不是文字檔，請變更 [`sharedListeners`] 節點中專案的值。 下列程式碼顯示如何將伺服器事件記錄到事件記錄檔：

**將事件記錄到事件記錄檔的 XML 伺服器程式碼**

[!code-xml[Main](enabling-signalr-tracing/samples/sample3.xml)]

事件會記錄在應用程式記錄檔中，並可透過事件檢視器取得，如下所示：

![顯示 SignalR 記錄的事件檢視器](enabling-signalr-tracing/_static/image1.png)

> [!NOTE]
> 使用事件記錄檔時，請將**TraceLevel**設定為**Error** ，以保持可管理的訊息數目。

<a id="net_client"></a>
## <a name="enabling-tracing-in-the-net-client-windows-desktop-apps"></a>在 .NET 用戶端中啟用追蹤（Windows 桌面應用程式）

.NET 用戶端可以將事件記錄到主控台、文字檔，或使用執行[檔的實](https://msdn.microsoft.com/library/system.io.textwriter.aspx)作為自訂記錄檔。

若要在 .NET 用戶端中啟用記錄，請將連接的 `TraceLevel` 屬性設定為[TraceLevels](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.tracelevels(v=vs.118).aspx)值，並將 `TraceWriter` 屬性設[為有效的](https://msdn.microsoft.com/library/system.io.textwriter.aspx)[無效] 實例。

<a id="desktop_console"></a>
### <a name="logging-desktop-client-events-to-the-console"></a>將桌面用戶端事件記錄到主控台

下列C#程式碼說明如何將 .net 用戶端中的事件記錄到主控台：

[!code-csharp[Main](enabling-signalr-tracing/samples/sample4.cs?highlight=2-3)]

<a id="desktop_text"></a>
### <a name="logging-desktop-client-events-to-a-text-file"></a>將桌面用戶端事件記錄到文字檔

下列C#程式碼顯示如何將 .net 用戶端中的事件記錄到文字檔：

[!code-csharp[Main](enabling-signalr-tracing/samples/sample5.cs?highlight=4-5)]

下列輸出會顯示使用上述設定檔之應用程式的 `ClientLog.txt` 檔案中的專案。 它會顯示連接到伺服器的用戶端，而中樞會叫用名為 `addMessage`的用戶端方法：

[!code-console[Main](enabling-signalr-tracing/samples/sample6.cmd)]

<a id="phone"></a>
## <a name="enabling-tracing-in-windows-phone-8-clients"></a>在 Windows Phone 8 用戶端中啟用追蹤

Windows Phone 應用程式的 SignalR 應用程式會使用與桌面應用程式相同的 .NET 用戶端，但不提供使用[StreamWriter](https://msdn.microsoft.com/library/system.io.streamwriter(v=vs.110).aspx)的[檔案和寫入](https://msdn.microsoft.com/library/system.console.out(v=vs.110).aspx)檔案的功能。 相反地，您需要為追蹤建立一個自[定義的執行](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)。

<a id="phone_ui"></a>
### <a name="logging-windows-phone-client-events-to-the-ui"></a>將 Windows Phone 用戶端事件記錄至 UI

[SignalR 程式碼基](https://github.com/SignalR/SignalR/archive/master.zip)底包含 Windows Phone 範例，其會使用稱為 `TextBlockWriter`[的自訂](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)的執行身分叫用將追蹤輸出寫入至[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) 。 您可以在**samples/SignalR. WP8 範例**專案中找到這個類別。 建立 `TextBlockWriter`的實例時，傳入目前的[SynchronizationCoNtext](https://msdn.microsoft.com/library/system.threading.synchronizationcontext(v=vs.110).aspx)和[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx) ，其中會建立用於追蹤輸出的[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) ：

[!code-csharp[Main](enabling-signalr-tracing/samples/sample7.cs)]

然後追蹤輸出會寫入至您傳入的[StackPanel](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.stackpanel.aspx)中建立的新[TextBlock](https://msdn.microsoft.com/library/windows/apps/windows.ui.xaml.controls.textblock.aspx) ：

![](enabling-signalr-tracing/_static/image2.png)

<a id="phone_debug"></a>
### <a name="logging-windows-phone-client-events-to-the-debug-console"></a>將 Windows Phone 用戶端事件記錄到調試主控台

若要將輸出傳送至偵錯工具主控台，而不是 UI，請建立會寫入至 [debug] 視窗，並將它指派給您的連接[TraceWriter](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connection.tracewriter(v=vs.118).aspx) [屬性的 [](https://msdn.microsoft.com/library/system.io.textwriter(v=vs.110).aspx)執行器]：

[!code-csharp[Main](enabling-signalr-tracing/samples/sample8.cs)]

接著，追蹤資訊會寫入 Visual Studio 中的 [debug] 視窗：

![](enabling-signalr-tracing/_static/image3.png)

<a id="javascript"></a>
## <a name="enabling-tracing-in-the-javascript-client"></a>在 JavaScript 用戶端中啟用追蹤

若要在連接上啟用用戶端記錄，請先在連線物件上設定 `logging` 屬性，再呼叫 `start` 方法來建立連接。

**用來啟用瀏覽器主控台追蹤的用戶端 JavaScript 程式碼（使用產生的 proxy）**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample9.js?highlight=1)]

**用來啟用瀏覽器主控台追蹤的用戶端 JavaScript 程式碼（不含產生的 proxy）**

[!code-javascript[Main](enabling-signalr-tracing/samples/sample10.js?highlight=2)]

啟用追蹤時，JavaScript 用戶端會將事件記錄到瀏覽器主控台。 若要存取瀏覽器主控台，請參閱[監視傳輸](../getting-started/introduction-to-signalr.md#MonitoringTransports)。

下列螢幕擷取畫面顯示已啟用追蹤的 SignalR JavaScript 用戶端。 它會在瀏覽器主控台中顯示連線和中樞呼叫事件：

![在瀏覽器主控台中 SignalR 追蹤事件](enabling-signalr-tracing/_static/image4.png)
