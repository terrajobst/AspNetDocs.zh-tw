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
# <a name="signalr-performance"></a>SignalR 效能

由[派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本主題描述如何在 SignalR 應用程式中設計、測量和改善效能。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - .NET 4.5
> - SignalR 第2版
>
>
>
> ## <a name="previous-versions-of-this-topic"></a>本主題的先前版本
>
> 如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。
>
> ## <a name="questions-and-comments"></a>問題與意見
>
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。

如需 SignalR 效能和調整的最新簡報，請參閱[使用 ASP.NET SignalR 調整即時 Web](https://channel9.msdn.com/Events/Build/2013/3-502)。

本主題包含下列各節：

- [設計考量](#design)
- [調整 SignalR 伺服器的效能](#tuning)
- [針對效能問題進行疑難排解](#troubleshooting)
- [使用 SignalR 效能計數器](#perfcounters)
- [使用其他效能計數器](#othercounters)
- [其他資源](#otherresources)

<a id="design"></a>

## <a name="design-considerations"></a>設計考量

本節說明可在 SignalR 應用程式設計期間實行的模式，以確保不會產生不必要的網路流量來妨礙運作效能。

### <a name="throttling-message-frequency"></a>節流訊息頻率

即使是在以較高頻率（例如即時遊戲應用程式）傳送訊息的應用程式中，大部分的應用程式都不需要一次傳送超過幾個訊息。 若要減少每個用戶端產生的流量量，可以將訊息迴圈實作為佇列，並將訊息送出的頻率不會超過固定速率（也就是每秒傳送的訊息數上限，如果當時的訊息位於要傳送的 terval）。 如需將訊息節流為特定速率（來自用戶端和伺服器）的範例應用程式，請參閱[使用 SignalR 的高頻率即時](../getting-started/tutorial-high-frequency-realtime-with-signalr.md)。

### <a name="reducing-message-size"></a>減少訊息大小

您可以減少已序列化物件的大小，以減少 SignalR 訊息的大小。 在伺服器程式碼中，如果您要傳送的物件包含不需要傳輸的屬性，請使用 `JsonIgnore` 屬性來避免序列化這些屬性。 屬性的名稱也會儲存在訊息中;您可以使用 `JsonProperty` 屬性來縮短屬性的名稱。 下列程式碼範例示範如何排除將屬性傳送至用戶端的方法，以及如何縮短屬性名稱：

**.NET server 程式碼，它會示範 JsonIgnore 屬性來排除要傳送至用戶端的資料，以及用來減少訊息大小的 JsonProperty 屬性**

[!code-csharp[Main](signalr-performance/samples/sample1.cs?highlight=5,7,10)]

為了在用戶端程式代碼中保留可讀性/可維護性，可以在收到訊息之後，將縮寫的屬性名稱重新對應至易記名稱。 下列程式碼範例示範一種可能的方式，藉由定義訊息合約（對應）來重新對應較長的名稱，並使用 `reMap` 函式將合約套用到優化的訊息類別：

**將縮短的屬性名稱重新對應到人類可讀名稱的用戶端 JavaScript 程式碼**

[!code-javascript[Main](signalr-performance/samples/sample2.js)]

也可以使用相同的方法，從用戶端到伺服器的訊息中縮短名稱。

減少 message 物件的記憶體使用量（也就是訊息使用的記憶體數量）也可以改善效能。 例如，如果不需要 `int` 的完整範圍，就可以改用 `short` 或 `byte`。

由於訊息會儲存在伺服器記憶體的訊息匯流排中，因此減少訊息的大小也可以解決伺服器記憶體的問題。

<a id="tuning"></a>

### <a name="tuning-your-signalr-server-for-performance"></a>調整 SignalR 伺服器的效能

下列設定可用於微調伺服器，以在 SignalR 應用程式中獲得更佳的效能。 如需如何在 ASP.NET 應用程式中改善效能的一般資訊，請參閱[改善 ASP.NET 效能](https://msdn.microsoft.com/library/ff647787.aspx)。

**SignalR 設定**

- **DefaultMessageBufferSize**：根據預設，SignalR 會每個連線在每個中樞的記憶體中保留1000訊息。 如果使用的是大型訊息，這可能會造成記憶體問題，藉由減少此值來緩解。 這項設定可在 ASP.NET 應用程式的 `Application_Start` 事件處理常式中設定，或在自我裝載應用程式中 OWIN 啟動類別的 `Configuration` 方法中設定。 下列範例示範如何減少此值，以減少應用程式的記憶體使用量，以減少使用的伺服器記憶體量：

    **Startup.cs 中的 .NET 伺服器程式碼，以減少預設的訊息緩衝區大小**

    [!code-csharp[Main](signalr-performance/samples/sample3.cs)]

**IIS 設定**

- **每個應用程式的並行要求數上限**：增加同時 IIS 要求的數目會增加可用來提供要求的伺服器資源。 預設值為 5000;若要增加這項設定，請在提升許可權的命令提示字元中執行下列命令：

    [!code-console[Main](signalr-performance/samples/sample4.cmd)]
- **ApplicationPool QueueLength**：這是應用程式集區之 HTTP.sys 佇列的最大要求數目。 當佇列已滿時，新的要求會收到503「服務無法使用」的回應。 預設值為 1000。

    縮短裝載應用程式之應用程式集區中工作者進程的佇列長度，將可節省記憶體資源。 如需詳細資訊，請參閱[管理、調整和設定應用程式](https://technet.microsoft.com/library/cc745955.aspx)集區。

**ASP.NET 設定**

本節包含可以在 `aspnet.config` 檔案中設定的配置設定。 此檔案可在下列兩個位置的其中一個找到，視平臺而定：

- `%windir%\Microsoft.NET\Framework\v4.0.30319\aspnet.config`
- `%windir%\Microsoft.NET\Framework64\v4.0.30319\aspnet.config`

可能會改善 SignalR 效能的 ASP.NET 設定包括下列各項：

- **每一 CPU 的並行要求數上限**：增加此設定可減輕效能瓶頸。 若要增加此設定，請將下列設定新增至 `aspnet.config` 檔案：

    [!code-xml[Main](signalr-performance/samples/sample5.xml?highlight=4)]
- **要求佇列限制**：當連線總數超過 `maxConcurrentRequestsPerCPU` 設定時，ASP.NET 會開始使用佇列來節流要求。 若要增加佇列的大小，您可以增加 [`requestQueueLimit`] 設定。 若要這麼做，請將下列設定設為 `config/machine.config` 中的 `processModel` 節點（而不是 `aspnet.config`）：

    [!code-xml[Main](signalr-performance/samples/sample6.xml)]

<a id="troubleshooting"></a>

## <a name="troubleshooting-performance-issues"></a>針對效能問題進行疑難排解

本節說明在您的應用程式中找出效能瓶頸的方式。

### <a name="verifying-that-websocket-is-being-used"></a>正在驗證是否正在使用 WebSocket

雖然 SignalR 可以使用各種傳輸來進行用戶端與伺服器之間的通訊，但 WebSocket 提供了顯著的效能優勢，如果用戶端和伺服器支援，則應使用它們。 若要判斷您的用戶端和伺服器是否符合 WebSocket 的需求，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。 若要判斷應用程式中所使用的傳輸為何，您可以使用瀏覽器開發人員工具，並檢查記錄檔，以查看連接所使用的傳輸。 如需在 Internet Explorer 和 Chrome 中使用瀏覽器開發工具的相關資訊，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。

<a id="perfcounters"></a>

## <a name="using-signalr-performance-counters"></a>使用 SignalR 效能計數器

本節說明如何啟用和使用 `Microsoft.AspNet.SignalR.Utils` 封裝中找到的 SignalR 效能計數器。

### <a name="installing-signalrexe"></a>安裝 signalr

您可以使用稱為 SignalR 的公用程式，將效能計數器新增至伺服器。 若要安裝此公用程式，請遵循下列步驟：

1. 在 Visual Studio 中，選取 [**工具**] [ > **nuget 套件管理員**] > [**管理解決方案的 nuget 套件**]
2. 搜尋**signalr utils**，然後選取 [安裝]。

    ![](signalr-performance/_static/image1.png)
3. 接受授權合約以安裝套件。
4. SignalR 會安裝到 `<project folder>/packages/Microsoft.AspNet.SignalR.Utils.<version>/tools`。

### <a name="installing-performance-counters-with-signalrexe"></a>使用 SignalR 安裝效能計數器

若要安裝 SignalR 效能計數器，請在提升許可權的命令提示字元中，使用下列參數執行 SignalR：

[!code-console[Main](signalr-performance/samples/sample7.cmd)]

若要移除 SignalR 效能計數器，請在提升許可權的命令提示字元中，使用下列參數執行 SignalR：

[!code-console[Main](signalr-performance/samples/sample8.cmd)]

### <a name="signalr-performance-counters"></a>SignalR 效能計數器

公用程式套件會安裝下列效能計數器。 「總計」計數器會測量自上一個應用程式集區或伺服器重新開機之後的事件數目。

**連接計量**

下列計量會測量發生的連線存留期事件。 如需詳細資訊，請參閱[瞭解和處理連接存留期事件](../guide-to-the-api/handling-connection-lifetime-events.md)。

- **連接的連線**
- **連接重新連接**
- **連線中斷連接**
- **目前的連線數**

**訊息計量**

下列計量會測量 SignalR 所產生的訊息流量。

- **已接收的連接訊息總數**
- **已傳送的連接訊息總數**
- **接收的連接訊息數/秒**
- **傳送的連接訊息數/秒**

**訊息匯流排計量**

下列計量會測量透過內部 SignalR 訊息匯流排的流量，這是放置所有傳入和傳出 SignalR 訊息的佇列。 訊息會在傳送或廣播時**發行**。 此內容中的**訂閱者**是訊息匯流排上的訂用帳戶;這應該等於用戶端的數目加上伺服器本身。 配置的背景**工作**是將資料傳送至使用中連線的元件;**忙碌的工作者**就是主動傳送訊息的背景工作。

- **訊息匯流排接收的訊息總數**
- **訊息匯流排接收訊息數/秒**
- **訊息匯流排訊息已發佈總數**
- **已發佈的訊息匯流排訊息數/秒**
- **訊息匯流排訂閱者目前**
- **訊息匯流排訂閱者總數**
- **訊息匯流排訂閱者/秒**
- **訊息匯流排配置的背景工作**
- **訊息匯流排忙碌工作者**
- **訊息匯流排主題目前**

**錯誤計量**

下列計量會測量 SignalR 訊息流量所產生的錯誤。 無法解析中樞或中樞方法時，會發生**中樞解析**錯誤。 **中樞調用**錯誤是叫用中樞方法時擲回的例外狀況。 **傳輸**錯誤是在 HTTP 要求或回應期間擲回的連接錯誤。

- **錯誤：所有總計**
- **錯誤：全部/秒**
- **錯誤：中樞解析總計**
- **錯誤：中樞解析/秒**
- **錯誤：中樞調用總數**
- **錯誤：中樞調用/秒**
- **錯誤：傳輸總數**
- **錯誤：傳輸/秒**

<a id="scaleout_metrics"></a>

**向外延展計量**

下列計量會測量向外延展提供者所產生的流量和錯誤。 此內容中的**資料流程**是向外延展提供者所使用的縮放單位;這是使用 SQL Server 時的資料表、使用服務匯流排的主題，以及使用 Redis 的訂用帳戶。 每個資料流程都會確保已排序的讀取和寫入作業;單一資料流程是潛在的調整瓶頸，因此可以增加串流數，以協助降低瓶頸。 如果使用多個資料流程，SignalR 會以確保從任何指定的連線傳送訊息的方式，自動在這些資料流程之間散發（分區）訊息。

[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)設定會控制 SignalR 所維護的向外延展傳送佇列長度。 將它設定為大於0的值，會將傳送佇列中的所有訊息一次傳送至設定的訊息後擋板。 如果佇列的大小超過設定的長度，後續的傳送呼叫將會立即失敗，並傳回[InvalidOperationException](https://msdn.microsoft.com/library/system.invalidoperationexception(v=vs.118).aspx) ，直到佇列中的訊息數目小於設定。 預設會停用佇列，因為實作的背板通常會有自己的佇列或流量控制。 在 SQL Server 的情況下，連接共用會有效限制一次傳入的傳送數目。

根據預設，只有一個資料流程會用於 SQL Server 和 Redis，而五個串流用於服務匯流排，而佇列已停用，但您可以透過 SQL Server 和服務匯流排上的設定來變更這些設定：

**用於設定 SQL Server 背板之資料表計數和佇列長度的 .NET 伺服器程式碼**

[!code-csharp[Main](signalr-performance/samples/sample9.cs)]

**用於設定服務匯流排背板之主題計數和佇列長度的 .NET 伺服器程式碼**

[!code-csharp[Main](signalr-performance/samples/sample10.cs)]

**緩衝**資料流程是進入錯誤狀態的一個，當資料流程處於「錯誤」狀態時，所有傳送至後擋板的訊息都會立即失敗，直到資料流程不再出錯為止。 **傳送佇列長度**是已張貼但尚未傳送的郵件數目。

- **向外延展接收的訊息匯流排訊息數/秒**
- **向外延展資料流程總計**
- **開啟的向外延展資料流程**
- **向外延展串流緩衝處理**
- **向外延展錯誤總數**
- **向外延展錯誤數/秒**
- **向外延展傳送佇列長度**

如需這些計數器測量之內容的詳細資訊，請參閱[SignalR 向外延展 with Azure 服務匯流排](scaleout-with-windows-azure-service-bus.md)。

<a id="othercounters"></a>

## <a name="using-other-performance-counters"></a>使用其他效能計數器

下列效能計數器可能也有助於監視應用程式的效能。

**記憶體**

- .NET CLR 記憶體\\所有堆積中的 # 個位元組（適用于 w3wp.exe）

**ASP.NET**

- ASP. NET\Requests Current
- ASP. NET\Queued
- ASP. NET\Rejected

**CPU**

- 處理器 Information\Processor 時間

**TCP/IP**

- 已建立 TCPv6/Connections
- 已建立 Tcpv4 已/Connections

**Web 服務**

- Web Service\current connections 連接
- Web Service\Maximum 連接

**執行緒處理**

- .NET CLR 鎖定和執行緒\\# 個目前的邏輯執行緒
- .NET CLR 鎖定和執行緒\\目前的實體執行緒數目

<a id="otherresources"></a>

## <a name="other-resources"></a>其他資源

如需有關 ASP.NET 效能監視和微調的詳細資訊，請參閱下列主題：

- [ASP.NET 效能概觀](https://msdn.microsoft.com/library/cc668225(v=vs.100).aspx)
- [在 IIS 7.5、IIS 7.0 和 IIS 6.0 上 ASP.NET 執行緒使用方式](https://blogs.msdn.com/b/tmarq/archive/2007/07/21/asp-net-thread-usage-on-iis-7-0-and-6-0.aspx)
- [&lt;applicationPool&gt; 元素（Web 設定）](https://msdn.microsoft.com/library/dd560842.aspx)
