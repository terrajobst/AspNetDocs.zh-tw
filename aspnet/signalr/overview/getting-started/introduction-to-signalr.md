---
uid: signalr/overview/getting-started/introduction-to-signalr
title: SignalR 簡介 |Microsoft Docs
author: bradygaster
description: 本文說明 SignalR 是什麼，以及它設計來建立的一些解決方案。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 0fab5e35-8c1f-43d4-8635-b8aba8766a71
msc.legacyurl: /signalr/overview/getting-started/introduction-to-signalr
msc.type: authoredcontent
ms.openlocfilehash: 8dbc31a5c8d59fa55dc5b513c1a51d24d18a685f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536432"
---
# <a name="introduction-to-signalr"></a>SignalR 簡介

由[派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文說明 SignalR 是什麼，以及它設計來建立的一些解決方案。 
> 
> ## <a name="questions-and-comments"></a>問題與意見
> 
> 請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](https://stackoverflow.com/questions/tagged/signalr)。

## <a name="what-is-signalr"></a>什麼是 SignalR？

ASP.NET SignalR 是 ASP.NET 開發人員的程式庫，可簡化將即時 web 功能新增至應用程式的過程。 即時 web 功能能夠讓伺服器程式碼立即將內容推送至已連線的用戶端，因為它可供使用，而不是讓伺服器等待用戶端要求新的資料。

SignalR 可以用來將任何類型的「即時」 web 功能新增至您的 ASP.NET 應用程式。 雖然對話通常是用來做為範例，但您也可以執行更多工作。 每當使用者重新整理網頁以查看新資料，或頁面執行[長時間輪詢](http://en.wikipedia.org/wiki/Push_technology#Long_polling)來取得新資料時，就是使用 SignalR 的候選。 範例包括儀表板和監視應用程式、共同作業應用程式（例如同時編輯檔）、工作進度更新和即時表單。

SignalR 也會啟用全新類型的 web 應用程式，需要伺服器的高頻率更新，例如即時遊戲。

SignalR 提供簡單的 API，可用於建立伺服器對用戶端遠端程序呼叫（RPC），以從伺服器端的 .NET 程式碼呼叫用戶端瀏覽器中的 JavaScript 函式（和其他用戶端平臺）。 SignalR 也包含用於連線管理的 API （例如，連線和中斷線上活動），以及群組連接。

![使用 SignalR 叫用方法](introduction-to-signalr/_static/image1.png)

SignalR 會自動處理連線管理，並可讓您同時將訊息廣播到所有已連接的用戶端，就像聊天室一樣。 您也可以將訊息傳送給特定用戶端。 用戶端與伺服器之間的連接是持續性的，與傳統 HTTP 連線不同，後者會針對每個通訊重新建立。

SignalR 支援「伺服器推播」功能，其中伺服器程式碼可以使用遠端程序呼叫（RPC）來呼叫瀏覽器中的用戶端程式代碼，而不是現今 web 上通用的要求-回應模型。

SignalR 應用程式可以使用內建和協力廠商的向外延展提供者，向外延展至數以千計的用戶端。

內建提供者包括：
* [服務匯流排](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)
* [SQL Server](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
* [Redis](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.Redis)

協力廠商提供者包括：
* [NCache](https://www.alachisoft.com/ncache/asp-net-core-signalr.html)。

SignalR 是開放原始碼，可透過[GitHub](https://github.com/signalr)存取。

## <a name="signalr-and-websocket"></a>SignalR 和 WebSocket

SignalR 會使用新的 WebSocket 傳輸（如果可用），並視需要切換回較舊的傳輸。 雖然您當然可以直接使用 WebSocket 撰寫應用程式，但使用 SignalR 表示您需要執行的許多額外功能已經為您完成。 最重要的是，這表示您可以撰寫應用程式的程式碼來利用 WebSocket，而不必擔心為較舊的用戶端建立個別的程式碼路徑。 SignalR 也會讓您不必擔心 WebSocket 的更新，因為 SignalR 會更新以支援基礎傳輸中的變更，讓您的應用程式在不同的 WebSocket 版本之間提供一致的介面。

<a id="transports"></a>

## <a name="transports-and-fallbacks"></a>傳輸和回退

SignalR 是在用戶端與伺服器之間進行即時工作所需的一些傳輸的抽象概念。 SignalR 連線會以 HTTP 啟動，然後升級至 WebSocket 連線（如果有的話）。 WebSocket 是 SignalR 的理想傳輸，因為它會最有效率地使用伺服器記憶體、具有最低延遲，而且具有最基本的功能（例如用戶端與伺服器之間的全雙工通訊），但它也具有最嚴格的需求： WebSocket 要求伺服器必須使用 Windows Server 2012 或 Windows 8，並 .NET Framework 4.5。 如果不符合這些需求，SignalR 會嘗試使用其他傳輸來建立其連接。

### <a name="html-5-transports"></a>HTML 5 傳輸

這些傳輸取決於[HTML 5](http://en.wikipedia.org/wiki/HTML5)的支援。 如果用戶端瀏覽器不支援 HTML 5 標準，則會使用較舊的傳輸。

- **WebSocket** （如果伺服器和瀏覽器都指出可以支援 WebSocket）。 WebSocket 是唯一可在用戶端與伺服器之間建立真正持續的雙向連接的傳輸。 不過，WebSocket 也具有最嚴格的需求;只有最新版本的 Microsoft Internet Explorer、Google Chrome 和 Mozilla Firefox 才會受到完整支援，而且只有在其他瀏覽器（例如 Opera 和 Safari）中才會有部分執行。
- **伺服器傳送的事件**，也稱為 EventSource （如果瀏覽器支援伺服器傳送的事件，這基本上是 Internet Explorer 以外的所有瀏覽器）。

### <a name="comet-transports"></a>Comet 傳輸

下列傳輸是以[Comet](http://en.wikipedia.org/wiki/Comet_(programming)) web 應用程式模型為基礎，在其中，瀏覽器或其他用戶端會維護長期的 HTTP 要求，而伺服器可以使用它來將資料推送至用戶端，而不需要用戶端特別要求它。

- **永久框架**（僅適用于 Internet Explorer）。 永久框架會建立隱藏的 IFrame，對伺服器上不會完成的端點提出要求。 伺服器接著會持續將腳本傳送至立即執行的用戶端，提供從伺服器到用戶端的單向即時連線。 從用戶端到伺服器的連接會使用與伺服器之間的不同連接，而與標準 HTTP 要求一樣，會針對每個需要傳送的資料片段建立新的連接。
- **Ajax 長輪詢**。 「長時間輪詢」並不會建立持續連線，而是會在伺服器回應時，以保持開啟狀態的要求來輪詢伺服器，此時連接會關閉，並立即要求新的連接。 這可能會在連線重設時導致一些延遲。

如需哪些設定支援哪些傳輸的詳細資訊，請參閱[支援的平臺](supported-platforms.md)。

### <a name="transport-selection-process"></a>傳輸選取進程

下列清單顯示 SignalR 用來決定要使用哪一個傳輸的步驟。

1. 如果瀏覽器是 Internet Explorer 8 或更早的版本，則會使用長時間輪詢。
2. 如果已設定 JSONP （也就是在連線啟動時，`jsonp` 參數設定為 `true`，則會使用長時間輪詢）。
3. 如果正在進行跨網域連線（也就是，如果 SignalR 端點不在裝載頁面所在的相同網域中），則會在符合下列條件時使用 WebSocket：

   - 用戶端支援 CORS （跨原始資源分享）。 如需哪些用戶端支援 CORS 的詳細資訊，請參閱[CORS，網址為 caniuse.com](http://www.caniuse.com/CORS)。
   - 用戶端支援 WebSocket
   - 伺服器支援 WebSocket

     如果不符合上述任何條件，則會使用長時間輪詢。 如需跨網域連線的詳細資訊，請參閱[如何建立跨網域](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)連線。
4. 如果未設定 JSONP，且連線不是跨網域，則當用戶端和伺服器都支援 WebSocket 時，將會使用 WebSocket。
5. 如果用戶端或伺服器不支援 WebSocket，則會使用伺服器傳送的事件（如果有的話）。
6. 如果無法使用伺服器傳送的事件，則會嘗試永久的框架。
7. 如果永久框架失敗，則會使用長時間輪詢。

<a id="MonitoringTransports"></a>
### <a name="monitoring-transports"></a>監視傳輸

您可以在中樞上啟用記錄功能，並在瀏覽器中開啟主控台視窗，以判斷您的應用程式所使用的傳輸。

若要在瀏覽器中啟用中樞事件的記錄，請將下列命令新增至您的用戶端應用程式：

`$.connection.hub.logging = true;`

- 在 Internet Explorer 中，按 F12 開啟開發人員工具，然後按一下 [主控台] 索引標籤。

    ![Microsoft Internet Explorer 中的主控台](introduction-to-signalr/_static/image2.png)
- 在 Chrome 中，按下 Ctrl + Shift + J 來開啟主控台。

    ![Google Chrome 中的主控台](introduction-to-signalr/_static/image3.png)

開啟主控台並啟用記錄功能之後，您將能夠查看 SignalR 正在使用哪個傳輸。

![Internet Explorer 中顯示 WebSocket 傳輸的主控台](introduction-to-signalr/_static/image4.png)

### <a name="specifying-a-transport"></a>指定傳輸

協調傳輸需要一段時間和用戶端/伺服器資源。 如果已知用戶端功能，則可以在用戶端連接啟動時指定傳輸。 下列程式碼片段示範如何使用 Ajax 長輪詢傳輸來啟動連接，如果已知用戶端不支援任何其他通訊協定，就會使用它：

`connection.start({ transport: 'longPolling' });`

如果您想要讓用戶端依序嘗試特定的傳輸，可以指定回溯順序。 下列程式碼片段示範如何嘗試 WebSocket，並失敗，直接進入長時間輪詢。

`connection.start({ transport: ['webSockets','longPolling'] });`

指定傳輸的字串常數定義如下：

- `webSockets`
- `foreverFrame`
- `serverSentEvents`
- `longPolling`

## <a name="connections-and-hubs"></a>連接和中樞

SignalR API 包含兩個可在用戶端和伺服器之間通訊的模型：持續連線和中樞。

連接代表傳送單一收件者、群組或廣播訊息的簡單端點。 持續性連線 API （由 PersistentConnection 類別在 .NET 程式碼中表示）可讓開發人員直接存取 SignalR 所公開的低層級通訊協定。 使用連接型 Api （例如 Windows Communication Foundation）的開發人員將會熟悉使用連線通訊模型。

中樞是以連線 API 為基礎所建立的高階管線，可讓您的用戶端和伺服器直接對彼此呼叫方法。 SignalR 會以神奇的方式處理跨電腦界限的分派，讓用戶端能夠輕鬆地呼叫伺服器上的方法，就像使用本機方法一樣，反之亦然。 使用遠端調用 Api （例如 .NET 遠端處理）的開發人員將會熟悉中樞通訊模型。 使用中樞也可以讓您將強型別參數傳遞至方法，以啟用模型系結。

### <a name="architecture-diagram"></a>架構圖

下圖顯示中樞、持續連線和用於傳輸的基礎技術之間的關聯性。

![顯示 Api、傳輸和用戶端的 SignalR 架構圖](introduction-to-signalr/_static/image5.png)

### <a name="how-hubs-work"></a>中樞的工作方式

當伺服器端程式碼在用戶端上呼叫方法時，會在作用中的傳輸中傳送封包，其中包含要呼叫之方法的名稱和參數（當物件當做方法參數傳送時，會使用 JSON 進行序列化）。 接著，用戶端會將方法名稱與用戶端程式代碼中定義的方法進行比對。 如果相符，則會使用已還原序列化的參數資料來執行用戶端方法。

您可以使用 Fiddler 之類的工具來監視方法呼叫[。](http://fiddler2.com/) 下圖顯示在 Fiddler 的 [記錄] 窗格中，從 SignalR 伺服器傳送至網頁瀏覽器用戶端的方法呼叫。 方法呼叫是從名為 `MoveShapeHub`的中樞傳送，而所叫用的方法則稱為 `updateShape`。

![Fiddler 記錄顯示 SignalR 流量的觀點](introduction-to-signalr/_static/image6.png)

在此範例中，中樞名稱是以 `H` 參數識別;方法名稱是以 `M` 參數識別，而傳送至方法的資料則是以 `A` 參數識別。 產生此訊息的應用程式會在[高頻率即時](tutorial-high-frequency-realtime-with-signalr.md)教學課程中建立。

### <a name="choosing-a-communication-model"></a>選擇通訊模型

大部分的應用程式都應該使用中樞 API。 連接 API 可用於下列情況：

- 必須指定所傳送之實際訊息的格式。
- 開發人員偏好使用訊息處理和分派模型，而不是遠端調用模型。
- 使用訊息模型的現有應用程式會進行移植，以使用 SignalR。
