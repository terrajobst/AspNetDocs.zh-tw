---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-net-client
title: ASP.NET SignalR 中樞 API 指南-.NET 用戶端C#（） |Microsoft Docs
author: bradygaster
description: 本檔提供在 .NET 用戶端（例如 Windows Store （WinRT）、WPF、Silverlight 和缺點）中使用中樞 API for SignalR 第2版的簡介 。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 6d02d9f7-94e5-4140-9f51-5a6040f274f6
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-net-client
msc.type: authoredcontent
ms.openlocfilehash: d3536f1c15cd7dad7cd660becf0577e5c131f707
ms.sourcegitcommit: 295cf898a4c87e264b0c35c7254b0fa4169f2278
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/13/2019
ms.locfileid: "74057013"
---
# <a name="aspnet-signalr-hubs-api-guide---net-client-c"></a>ASP.NET SignalR 中樞 API 指南-.NET 用戶端C#（）

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本檔提供在 .NET 用戶端（例如 Windows Store （WinRT）、WPF、Silverlight 和主控台應用程式）中使用適用于 SignalR 第2版之中樞 API 的簡介。
>
> SignalR 中樞 API 可讓您從伺服器對連線的用戶端，以及從用戶端到伺服器進行遠端程序呼叫（Rpc）。 在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。 在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。 SignalR 會為您處理所有的用戶端對伺服器管道。
>
> SignalR 也提供名為「持續連線」的較低層級 API。 如需 SignalR、中樞和持續連線的簡介，或顯示如何建立完整 SignalR 應用程式的教學課程，請參閱[SignalR-消費者入門](../getting-started/index.md)。
>
> ## <a name="software-versions-used-in-this-topic"></a>本主題中使用的軟體版本
>
>
> - [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)
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

## <a name="overview"></a>總覽

本文件包含下列章節：

- [用戶端設定](#clientsetup)
- [如何建立連接](#establishconnection)

    - [Silverlight 用戶端的跨網域連線](#slcrossdomain)
- [如何設定連線](#configureconnection)

    - [如何設定 WPF 用戶端中的並行連接數目上限](#maxconnections)
    - [如何指定查詢字串參數](#querystring)
    - [如何指定傳輸方法](#transport)
    - [如何指定 HTTP 標頭](#httpheaders)
    - [如何指定用戶端憑證](#clientcertificate)
- [如何建立中樞 proxy](#proxy)
- [如何在用戶端上定義伺服器可以呼叫的方法](#callclient)

    - [沒有參數的方法](#clientmethodswithoutparms)
    - [具有參數的方法，指定參數類型](#clientmethodswithparmtypes)
    - [具有參數的方法，指定參數的動態物件](#clientmethodswithdynamparms)
    - [如何移除處理常式](#removehandler)
- [如何從用戶端呼叫伺服器方法](#callserver)
- [如何處理連接存留期事件](#connectionlifetime)
- [如何處理錯誤](#handleerrors)
- [如何啟用用戶端記錄](#logging)
- [伺服器可以呼叫之用戶端方法的 WPF、Silverlight 和主控台應用程式程式碼範例](#wpfsl)

如需範例 .NET 用戶端專案，請參閱下列資源：

- [gustavo-armenta/SignalR-](https://github.com/gustavo-armenta/SignalR-Samples) GitHub.com （WinRT、Silverlight、主控台應用程式範例）上的範例。
- GitHub.com 上[的 DamianEdwards/SignalR-MoveShapeDemo/MoveShape](https://github.com/DamianEdwards/SignalR-MoveShapeDemo/tree/master/MoveShape/MoveShape.Desktop) （WPF 範例）。
- GitHub.com 上的[SignalR/SignalR](https://github.com/SignalR/SignalR/tree/master/samples/Microsoft.AspNet.SignalR.Client.Samples) （主控台應用程式範例）。

如需如何撰寫伺服器或 JavaScript 用戶端程式的相關檔，請參閱下列資源：

- [SignalR 中樞 API 指南-伺服器](hubs-api-guide-server.md)
- [SignalR 中樞 API 指南-JavaScript 用戶端](hubs-api-guide-javascript-client.md)

API 參考主題的連結是針對 .NET 4.5 版的 API。 如果您使用的是 .NET 4，請參閱[.net 4 版本的 API 主題](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="clientsetup"></a>

## <a name="client-setup"></a>用戶端設定

安裝[SignalR。用戶端](http://nuget.org/packages/Microsoft.AspNet.SignalR.Client)NuGet 套件（而不是[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr)套件）。 此套件支援適用于 .NET 4 和 .NET 4.5 的 WinRT、Silverlight、WPF、主控台應用程式和 Windows Phone 用戶端。

如果您在用戶端上擁有的 SignalR 版本與伺服器上的版本不同，SignalR 通常可以適應差異。 例如，執行 SignalR 第2版的伺服器將支援已安裝 1.1. x 的用戶端，以及安裝了第2版的用戶端。 如果伺服器上的版本和用戶端上的版本之間的差異太大，或者用戶端比伺服器新，則當用戶端嘗試建立連線時，SignalR 會擲回 `InvalidOperationException` 例外狀況。 錯誤訊息為「`You are using a version of the client that isn't compatible with the server. Client version X.X, server version X.X`」。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立連接

建立連接之前，您必須先建立 `HubConnection` 物件，並建立 proxy。 若要建立連接，請在 `HubConnection` 物件上呼叫 `Start` 方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample1.cs?highlight=1,5)]

> [!NOTE]
> 針對 JavaScript 用戶端，您必須先註冊至少一個事件處理常式，才能呼叫 `Start` 方法來建立連接。 這不是 .NET 用戶端的必要動作。 針對 JavaScript 用戶端，產生的 proxy 程式碼會自動為存在於伺服器上的所有中樞建立 proxy，而註冊處理常式則是您如何指出用戶端想要使用的中樞。 但是針對 .NET 用戶端，您可以手動建立中樞 proxy，因此 SignalR 會假設您將使用為其建立 proxy 的任何中樞。

範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。 如需有關如何指定不同基底 URL 的詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。

`Start` 方法會以非同步方式執行。 若要確保在建立連接之後才執行後續的程式程式碼，請使用 ASP.NET 4.5 非同步方法中的 `await`，或在同步方法中 `.Wait()`。 請勿在 WinRT 用戶端中使用 `.Wait()`。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample2.cs?highlight=1)]

[!code-css[Main](hubs-api-guide-net-client/samples/sample3.css?highlight=1)]

<a id="slcrossdomain"></a>

### <a name="cross-domain-connections-from-silverlight-clients"></a>Silverlight 用戶端的跨網域連線

如需有關如何從 Silverlight 用戶端啟用跨網域連線的詳細資訊，請參閱[讓服務可跨網域界限使用](https://msdn.microsoft.com/library/cc197955(v=vs.95).aspx)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何設定連線

建立連接之前，您可以指定下列任何選項：

- 同時連接限制。
- 查詢字串參數。
- 傳輸方法。
- HTTP 標頭。
- 用戶端憑證。

<a id="maxconnections"></a>

### <a name="how-to-set-the-maximum-number-of-concurrent-connections-in-wpf-clients"></a>如何設定 WPF 用戶端中的並行連接數目上限

在 WPF 用戶端中，您可能必須從預設值2增加並行連接的最大數目。 建議的值是10。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample4.cs?highlight=5)]

如需詳細資訊，請參閱[ServicePointManager. servicepointmanager.defaultconnectionlimit](https://msdn.microsoft.com/library/system.net.servicepointmanager.defaultconnectionlimit.aspx)。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查詢字串參數

如果您想要在用戶端連接時將資料傳送到伺服器，您可以將查詢字串參數新增至 connection 物件。 下列範例說明如何在用戶端程式代碼中設定查詢字串參數。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample5.cs)]

下列範例顯示如何讀取伺服器程式碼中的查詢字串參數。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample6.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定傳輸方法

在進行連線的過程中，SignalR 用戶端通常會與伺服器協商，以判斷伺服器和用戶端都支援的最佳傳輸。 如果您已經知道您想要使用的傳輸，可以略過此協調流程。 若要指定傳輸方法，請將傳輸物件傳入 Start 方法。 下列範例顯示如何在用戶端程式代碼中指定傳輸方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample7.cs?highlight=5)]

[SignalR](https://msdn.microsoft.com/library/jj918090(v=vs.111).aspx)命名空間包含下列可供您用來指定傳輸的類別。

- [LongPollingTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.longpollingtransport(v=vs.111).aspx)
- [ServerSentEventsTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.serversenteventstransport(v=vs.111).aspx)
- [WebSocketTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.websockettransport(v=vs.111).aspx) （僅適用于伺服器和用戶端都使用 .net 4.5 時）。
- [AutoTransport](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.transports.autotransport(v=vs.111).aspx) （自動選擇用戶端和伺服器所支援的最佳傳輸。 這是預設的傳輸。 將此傳遞至 `Start` 方法，其效果與未傳入任何專案相同。）

ForeverFrame 傳輸不包含在這份清單中，因為它僅供瀏覽器使用。

如需有關如何在伺服器程式碼中檢查傳輸方法的詳細資訊，請參閱[ASP.NET SignalR HUB API 指南-伺服器-如何從內容屬性取得用戶端的相關資訊](hubs-api-guide-server.md#contextproperty)。 如需傳輸和回退的詳細資訊，請參閱[SignalR-傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。

<a id="httpheaders"></a>

### <a name="how-to-specify-http-headers"></a>如何指定 HTTP 標頭

若要設定 HTTP 標頭，請使用 connection 物件上的 `Headers` 屬性。 下列範例顯示如何新增 HTTP 標頭。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample8.cs?highlight=2)]

<a id="clientcertificate"></a>

### <a name="how-to-specify-client-certificates"></a>如何指定用戶端憑證

若要新增用戶端憑證，請在 connection 物件上使用 `AddClientCertificate` 方法。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample9.cs?highlight=2)]

<a id="proxy"></a>

## <a name="how-to-create-the-hub-proxy"></a>如何建立中樞 proxy

若要在用戶端上定義中樞可以從伺服器呼叫的方法，以及在伺服器上叫用中樞上的方法，請在連線物件上呼叫 `CreateHubProxy`，以建立中樞的 proxy。 您傳入 `CreateHubProxy` 的字串是中樞類別的名稱，或是 `HubName` 屬性所指定的名稱（如果伺服器上使用了它）。 名稱比對不區分大小寫。

**伺服器上的中樞類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample10.cs?highlight=1)]

**建立中樞類別的用戶端 proxy**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample11.cs?highlight=3)]

如果您以 `HubName` 屬性裝飾中樞類別，請使用該名稱。

**伺服器上的中樞類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample12.cs)]

**建立中樞類別的用戶端 proxy**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample13.cs?highlight=3)]

如果您使用相同的 `hubName`多次呼叫 `HubConnection.CreateHubProxy`，則會取得相同的快取 `IHubProxy` 物件。

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在用戶端上定義伺服器可以呼叫的方法

若要定義伺服器可以呼叫的方法，請使用 proxy 的 `On` 方法來註冊事件處理常式。

方法名稱比對不區分大小寫。 例如，伺服器上的 `Clients.All.UpdateStockPrice` 將會在用戶端上執行 `updateStockPrice`、`updatestockprice`或 `UpdateStockPrice`。

不同的用戶端平臺對於您撰寫方法程式碼來更新 UI 的方式有不同的需求。 所顯示的範例適用于 WinRT （Windows Store .NET）用戶端。 [本主題稍後的個別章節](#wpfsl)會提供 WPF、Silverlight 和主控台應用程式範例。

<a id="clientmethodswithoutparms"></a>

### <a name="methods-without-parameters"></a>沒有參數的方法

如果您要處理的方法沒有參數，請使用 `On` 方法的非泛型多載：

**不含參數的伺服器程式碼呼叫用戶端方法**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample14.cs?highlight=5)]

**從沒有參數的伺服器呼叫之方法的 WinRT 用戶端程式代碼（[請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)）**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample15.cs)]

<a id="clientmethodswithparmtypes"></a>

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>具有參數的方法，指定參數類型

如果您要處理的方法有參數，請將參數的類型指定為 `On` 方法的泛型型別。 `On` 方法的泛型多載，可讓您指定最多8個參數（4 Windows Phone 7）。 在下列範例中，會將一個參數傳送至 `UpdateStockPrice` 方法。

**使用參數呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample16.cs?highlight=3)]

**用於參數的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample17.cs)]

**使用參數從伺服器呼叫之方法的 WinRT 用戶端程式代碼（[請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)）**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample18.cs?highlight=1,5)]

<a id="clientmethodswithdynamparms"></a>

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>具有參數的方法，指定參數的動態物件

除了將參數指定為 `On` 方法的泛型型別之外，您還可以將參數指定為動態物件：

**使用參數呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample19.cs?highlight=3)]

**用於參數的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample20.cs)]

**使用參數從伺服器呼叫之方法的 WinRT 用戶端程式代碼（[請參閱本主題稍後的 WPF 和 Silverlight 範例](#wpfsl)）**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample21.cs?highlight=1,5)]

<a id="removehandler"></a>

### <a name="how-to-remove-a-handler"></a>如何移除處理常式

若要移除處理常式，請呼叫其 `Dispose` 方法。

**從伺服器呼叫之方法的用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample22.cs?highlight=1)]

**移除處理常式的用戶端程式代碼**

[!code-css[Main](hubs-api-guide-net-client/samples/sample23.css?highlight=1)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何從用戶端呼叫伺服器方法

若要在伺服器上呼叫方法，請在中樞 proxy 上使用 `Invoke` 方法。

如果伺服器方法沒有傳回值，請使用 `Invoke` 方法的非泛型多載。

**沒有傳回值之方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample24.cs?highlight=3)]

**呼叫沒有傳回值之方法的用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample25.cs?highlight=1)]

如果伺服器方法有傳回值，請將傳回型別指定為 `Invoke` 方法的泛型型別。

**具有傳回值並接受複雜型別參數之方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample26.cs?highlight=1)]

**用於參數和傳回值的 Stock 類別**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample27.cs)]

**在 ASP.NET 4.5 非同步方法中呼叫具有傳回值並採用複雜類型參數的方法的用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample28.cs?highlight=1-2)]

**在同步方法中呼叫具有傳回值並採用複雜型別參數之方法的用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample29.cs?highlight=1-2)]

`Invoke` 方法會以非同步方式執行，並傳回 `Task` 物件。 如果您未指定 `await` 或 `.Wait()`，則下一行程式碼會在您叫用的方法完成執行之前執行。

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何處理連接存留期事件

SignalR 提供您可以處理的下列連接存留期事件：

- `Received`：在連接上收到任何資料時引發。 提供接收的資料。
- `ConnectionSlow`：當用戶端偵測到緩慢或經常中斷的連接時引發。
- `Reconnecting`：當基礎傳輸開始重新連接時引發。
- `Reconnected`：當基礎傳輸已重新連接時引發。
- `StateChanged`：當連接狀態變更時引發。 提供舊狀態和新狀態。 如需連接狀態值的詳細資訊，請參閱[ConnectionState 列舉](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.client.connectionstate(v=vs.111).aspx)。
- `Closed`：當連接中斷連線時引發。

例如，如果您想要針對不嚴重的錯誤顯示警告訊息，但造成間歇性的連線問題（例如緩慢或經常卸載連接），則會處理 `ConnectionSlow` 事件。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample30.cs)]

如需詳細資訊，請參閱[瞭解和處理 SignalR 中的連接存留期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何處理錯誤

如果您未在伺服器上明確啟用詳細的錯誤訊息，則 SignalR 會在錯誤之後傳回的例外狀況物件包含有關錯誤的最少資訊。 例如，如果 `newContosoChatMessage` 的呼叫失敗，錯誤物件中的錯誤訊息就會包含「`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`」將詳細的錯誤訊息傳送給生產環境中的用戶端，基於安全性理由，不建議使用此方法，但如果您想要針對疑難排解目的啟用詳細的錯誤訊息，請在伺服器上使用下列程式碼。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample31.cs?highlight=2)]

<a id="handleerrors"></a>

若要處理 SignalR 引發的錯誤，您可以在 connection 物件上加入 `Error` 事件的處理常式。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample32.cs)]

若要處理方法調用中的錯誤，請將程式碼包裝在 try-catch 區塊中。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample33.cs)]

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何啟用用戶端記錄

若要啟用用戶端記錄，請在 connection 物件上設定 `TraceLevel` 和 `TraceWriter` 屬性。

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample34.cs?highlight=3-4)]

<a id="wpfsl"></a>

## <a name="wpf-silverlight-and-console-application-code-samples-for-client-methods-that-the-server-can-call"></a>伺服器可以呼叫之用戶端方法的 WPF、Silverlight 和主控台應用程式程式碼範例

先前針對定義伺服器可以呼叫之用戶端方法所顯示的程式碼範例，適用于 WinRT 用戶端。 下列範例顯示 WPF、Silverlight 和主控台應用程式用戶端的對等程式碼。

### <a name="methods-without-parameters"></a>沒有參數的方法

**從沒有參數的伺服器呼叫之方法的 WPF 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample35.cs?highlight=1)]

**從沒有參數的伺服器呼叫之方法的 Silverlight 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample36.cs?highlight=1)]

**從沒有參數的伺服器呼叫之方法的主控台應用程式用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample37.cs?highlight=1)]

### <a name="methods-with-parameters-specifying-the-parameter-types"></a>具有參數的方法，指定參數類型

**使用參數從伺服器呼叫之方法的 WPF 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample38.cs?highlight=1,4)]

**使用參數從伺服器呼叫之方法的 Silverlight 用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample39.cs?highlight=1,5)]

**使用參數從伺服器呼叫之方法的主控台應用程式用戶端程式代碼**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample40.cs?highlight=1-2)]

### <a name="methods-with-parameters-specifying-dynamic-objects-for-the-parameters"></a>具有參數的方法，指定參數的動態物件

**從伺服器使用參數呼叫之方法的 WPF 用戶端程式代碼，使用參數的動態物件**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample41.cs?highlight=1,4)]

**從伺服器使用參數呼叫之方法的 Silverlight 用戶端程式代碼，使用參數的動態物件**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample42.cs?highlight=1,5)]

**從伺服器使用參數呼叫之方法的主控台應用程式用戶端程式代碼，使用參數的動態物件**

[!code-csharp[Main](hubs-api-guide-net-client/samples/sample43.cs?highlight=1-2)]
