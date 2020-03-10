---
uid: signalr/overview/guide-to-the-api/handling-connection-lifetime-events
title: 瞭解和處理 SignalR 中的連接存留期事件 |Microsoft Docs
author: bradygaster
description: 本文說明如何使用中樞 API 所公開的事件。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: 03960de2-8d95-4444-9169-4426dcc64913
msc.legacyurl: /signalr/overview/guide-to-the-api/handling-connection-lifetime-events
msc.type: authoredcontent
ms.openlocfilehash: 5bdf20549fccab5d644e35fdf4ce351540c8620d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78578810"
---
# <a name="understanding-and-handling-connection-lifetime-events-in-signalr"></a>了解及處理 SignalR 的連線存留期事件

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本文概要說明您可以處理的 SignalR 連線、重新連線和中斷線上活動，以及您可以設定的 timeout 和 keepalive 設定。
>
> 本文假設您已經瞭解 SignalR 和連線存留期事件。 如需 SignalR 的簡介，請參閱[SignalR 簡介](../getting-started/introduction-to-signalr.md)。 如需連線存留期事件的清單，請參閱下列資源：
>
> - [如何處理中樞類別中的連接存留期事件](hubs-api-guide-server.md#connectionlifetime)
> - [如何處理 JavaScript 用戶端中的連接存留期事件](hubs-api-guide-javascript-client.md#connectionlifetime)
> - [如何處理 .NET 用戶端中的連接存留期事件](hubs-api-guide-net-client.md#connectionlifetime)
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

## <a name="overview"></a>概觀

本文包含下列章節：

- [連線存留期術語和案例](#terminology)

    - [SignalR 連線、傳輸連線和實體連接](#signalrvstransport)
    - [傳輸中斷連接案例](#transportdisconnect)
    - [用戶端中斷連接案例](#clientdisconnect)
    - [伺服器中斷連接案例](#serverdisconnect)
- [Timeout 和 keepalive 設定](#timeoutkeepalive)

    - [ConnectionTimeout](#connectiontimeout)
    - [DisconnectTimeout](#disconnecttimeout)
    - [保](#keepalive)
    - [如何變更 timeout 和 keepalive 設定](#changetimeout)
- [如何通知使用者中斷連線](#notifydisconnect)
- [如何持續重新連線](#continuousreconnect)
- [如何中斷用戶端與伺服器程式碼的連線](#disconnectclientfromserver)
- [偵測中斷連接的原因](#detectingreasonfordisconnection)

API 參考主題的連結是針對 .NET 4.5 版的 API。 如果您使用的是 .NET 4，請參閱[.net 4 版本的 API 主題](https://msdn.microsoft.com/library/jj891075(v=vs.100).aspx)。

<a id="terminology"></a>

## <a name="connection-lifetime-terminology-and-scenarios"></a>連線存留期術語和案例

SignalR 中樞內的 `OnReconnected` 事件處理常式可以在 `OnConnected` 之後直接執行，而不是在指定的用戶端 `OnDisconnected` 之後。 您可以在沒有中斷連線的情況下進行重新連線的原因，就是在 SignalR 中使用「連線」這個字的幾種方式。

<a id="signalrvstransport"></a>

### <a name="signalr-connections-transport-connections-and-physical-connections"></a>SignalR 連線、傳輸連線和實體連接

本文將區別*SignalR 連接*、*傳輸*連線和*實體*連線：

- **SignalR**連線是指用戶端和伺服器 URL 之間的邏輯關聯性，由 SignalR API 維護，並由連接識別碼唯一識別。 此關聯性的相關資料是由 SignalR 維護，用來建立傳輸連接。 當用戶端呼叫 `Stop` 方法，或當 SignalR 嘗試重新建立遺失的傳輸連線時，當到達時，關聯性會結束並 SignalR 處置資料。
- **傳輸**連線指的是用戶端與伺服器之間的邏輯關聯性，由四個傳輸 api 的其中一個來維護： websocket、伺服器傳送事件、永久框架或長時間輪詢。 SignalR 使用傳輸 API 來建立傳輸連線，而傳輸 API 則取決於實體網路連線是否存在，以建立傳輸連接。 當 SignalR 終止時，或當傳輸 API 偵測到實體連接中斷時，傳輸連接就會結束。
- **實體**連線指的是實體網路連結（有線、無線信號、路由器等），可協助用戶端電腦和伺服器電腦之間的通訊。 必須要有實體連接，才能建立傳輸連線，而且必須建立傳輸連線，才能建立 SignalR 連接。 不過，中斷實體連接並不一定會立即結束傳輸連線或 SignalR 連線，如本主題稍後所述。

在下圖中，SignalR 連線是由中樞 API 和 PersistentConnection API SignalR 層代表，傳輸連接是以傳輸層來表示，而實體連接則是由伺服器之間的程式程式碼來表示。和用戶端。

![SignalR 架構圖](handling-connection-lifetime-events/_static/image1.png)

當您在 SignalR 用戶端中呼叫 `Start` 方法時，您會提供 SignalR 用戶端程式代碼，以及建立與伺服器的實體連接時所需的所有資訊。 SignalR 用戶端程式代碼會使用這項資訊來提出 HTTP 要求，並建立使用四種傳輸方法之一的實體連接。 如果傳輸連線失敗或伺服器失敗，則 SignalR 連線不會立即消失，因為用戶端仍具有自動重新建立連線到相同 SignalR URL 的新傳輸連接所需的資訊。 在此案例中，不涉及使用者應用程式的介入，而且當 SignalR 用戶端程式代碼建立新的傳輸連線時，並不會啟動新的 SignalR 連接。 SignalR 連接的持續性會反映在您呼叫 `Start` 方法時所建立的連線識別碼不會變更的事實中。

當傳輸連線在遺失後自動重新建立時，中樞上的 `OnReconnected` 事件處理常式就會執行。 `OnDisconnected` 事件處理常式會在 SignalR 連接結束時執行。 SignalR 連接可以下列任何一種方式結束：

- 如果用戶端呼叫 `Stop` 方法，就會將停止訊息傳送至伺服器，而且用戶端和伺服器都會立即結束 SignalR 連線。
- 在用戶端與伺服器之間的連線中斷之後，用戶端會嘗試重新連接，而伺服器會等待用戶端重新連線。 如果嘗試重新連線失敗，而中斷連線超時期間結束，則用戶端和伺服器都會結束 SignalR 連線。 用戶端會停止嘗試重新連線，而伺服器會處置其 SignalR 連接的表示。
- 如果用戶端在沒有機會呼叫 `Stop` 方法的情況下停止執行，伺服器會等待用戶端重新連線，然後在中斷連線超時時間之後結束 SignalR 連線。
- 如果伺服器停止執行，用戶端會嘗試重新連線（重新建立傳輸連線），然後在中斷連線超時時間之後結束 SignalR 連接。

當沒有連線問題時，如果使用者應用程式藉由呼叫 `Stop` 方法來結束 SignalR 連接，則 SignalR 連接和傳輸連接會在大約相同的時間開始和結束。 下列各節將更詳細地說明其他案例。

<a id="transportdisconnect"></a>

### <a name="transport-disconnection-scenarios"></a>傳輸中斷連接案例

實體連接可能很慢，或連線中斷。 視停機時間長度的因素而定，傳輸連接可能會被捨棄。 SignalR 接著會嘗試重新建立傳輸連接。 有時傳輸連線 API 會偵測中斷並卸載傳輸連線，而 SignalR 會立即發現連線已中斷。 在其他情況下，傳輸連線 API 和 SignalR 都不會立即得知連線是否已中斷。 對於長時間輪詢以外的所有傳輸，SignalR 用戶端會使用名為*keepalive*的函數來檢查傳輸 API 無法偵測到的連線中斷。 如需長時間輪詢連接的詳細資訊，請參閱本主題稍後的[Timeout 和 keepalive 設定](#timeoutkeepalive)。

當連接處於非作用中狀態時，伺服器會定期將 keepalive 封包傳送至用戶端。 在撰寫本文的日期起，預設頻率為每10秒一次。 藉由接聽這些封包，用戶端可以判斷是否有連線問題。 如果預期不會收到 keepalive 封包，則在短暫的時間之後，用戶端會假設有連線問題，例如緩慢或中斷。 如果在較長的時間之後仍未收到 keepalive，用戶端會假設已卸載連接，並開始嘗試重新連線。

下圖說明當傳輸 API 無法立即辨識實體連線問題時，在一般案例中引發的用戶端和伺服器事件。 圖表適用于下列情況：

- 傳輸是 Websocket、永久框架或伺服器傳送事件。
- 實體網路連線有不同的中斷期間。
- 傳輸 API 不會察覺中斷，因此 SignalR 會依賴 keepalive 功能來偵測它們。

![傳輸中斷連線](handling-connection-lifetime-events/_static/image2.png)

如果用戶端進入重新連線模式，但無法在中斷連線超時限制內建立傳輸連線，伺服器就會終止 SignalR 連接。 發生這種情況時，伺服器會執行中樞的 `OnDisconnected` 方法，並將中斷連線訊息排入佇列，以在用戶端管理以供稍後連線時傳送至用戶端。 如果用戶端接著重新連接，它會接收 disconnect 命令並呼叫 `Stop` 方法。 在此案例中，當用戶端重新連接時，不會執行 `OnReconnected`，而且當用戶端呼叫 `Stop`時，不會執行 `OnDisconnected`。 下圖說明此案例。

![傳輸中斷-伺服器超時](handling-connection-lifetime-events/_static/image3.png)

可能在用戶端上引發的 SignalR 連接存留期事件如下：

- `ConnectionSlow` 用戶端事件。

    當 keepalive 超時期間的預設比例在收到最後一則訊息或 keepalive ping 之後引發。 預設的 keepalive 超時警告期間為2/3 的 keepalive 時間。 Keepalive 超時時間為20秒，因此警告大約會在13秒內發生。

    根據預設，伺服器每隔10秒會傳送 keepalive ping，而且用戶端會每隔2秒檢查一次 keepalive ping （keepalive 超時值與 keepalive 超時警告值之間的差異三分之一）。

    如果傳輸 API 會察覺中斷連線，則在 keepalive 超時警告期間通過之前，SignalR 可能會收到中斷連線的通知。 在此情況下，將不會引發 `ConnectionSlow` 事件，而 SignalR 會直接進入 `Reconnecting` 事件。
- `Reconnecting` 用戶端事件。

    當（a）傳輸 API 偵測到連接遺失時引發，或（b）在收到最後一則訊息或 keepalive ping 之後已經過。 SignalR 用戶端程式代碼會開始嘗試重新連線。 如果您想要讓應用程式在傳輸連接中斷時採取某種動作，可以處理這個事件。 預設的 keepalive 超時時間目前為20秒。

    如果您的用戶端程式代碼在 SignalR 處於重新連線模式時嘗試呼叫中樞方法，SignalR 會嘗試傳送命令。 在大部分的情況下，這類嘗試會失敗，但在某些情況下，可能會成功。 對於伺服器傳送的事件、永遠的框架和長輪詢傳輸，SignalR 會使用兩個通道，其中一個是用戶端用來傳送訊息的通道，另一個則是用來接收訊息。 用來接收的通道是永久開啟的通道，這是實體連接中斷時所關閉的通道。 用於傳送的通道仍可供使用，因此，如果還原實體連線，從用戶端到伺服器的方法呼叫可能會在接收通道重新建立之前成功。 在 SignalR 重新開啟用來接收的通道之前，不會收到傳回值。
- `Reconnected` 用戶端事件。

    重新建立傳輸連接時引發。 中樞內的 `OnReconnected` 事件處理常式會執行。
- `Closed` 用戶端事件（JavaScript 中的`disconnected` 事件）。

    當 SignalR 用戶端程式代碼在失去傳輸連線後嘗試重新連線時，當中斷連線超時期間過期時引發。 預設的中斷連線超時時間為30秒。 （當連接因為呼叫 `Stop` 方法而結束時，也會引發這個事件）。

傳輸 API 不會偵測到傳輸連線中斷，而且不會延遲從伺服器接收 keepalive ping 的時間超過 keepalive 超時警告期間，可能不會導致任何連線存留期事件引發。

有些網路環境故意關閉閒置連線，而 keepalive 封包的另一個功能是讓這些網路知道 SignalR 連線正在使用中，藉此避免這種情況。 在極端情況下，keepalive ping 的預設頻率可能不足以防止關閉的連接。 在此情況下，您可以設定讓 keepalive ping 更頻繁地傳送。 如需詳細資訊，請參閱本主題稍後的[Timeout 和 keepalive 設定](#timeoutkeepalive)。

> [!NOTE]
>
> **重要**事項：不保證此處所述的事件順序。 SignalR 會根據此配置，以可預測的方式讓每次嘗試引發連線存留期事件，但有許多網路事件的變化，還有許多方法，例如傳輸 Api 處理它們的基礎通訊架構。 例如，當用戶端重新連線時，可能不會引發 `Reconnected` 事件，或者當嘗試建立連線失敗時，伺服器上的 `OnConnected` 處理常式可能會執行。 本主題僅說明某些一般情況下通常會產生的效果。

<a id="clientdisconnect"></a>

### <a name="client-disconnection-scenarios"></a>用戶端中斷連接案例

在瀏覽器用戶端中，維護 SignalR 連接的 SignalR 用戶端程式代碼會在網頁的 JavaScript 內容中執行。 這就是為什麼當您從一頁流覽到另一個頁面時，SignalR 連線必須結束，這就是為什麼當您從多個瀏覽器視窗或索引標籤連接時，如果您有多個連接識別碼的連接，就會有 當使用者關閉瀏覽器視窗或索引標籤，或流覽至新頁面或重新整理頁面時，SignalR 連接會立即結束，因為 SignalR 用戶端程式代碼會為您處理該瀏覽器事件，並呼叫 `Stop` 方法。 在這些情況下，或在任何用戶端平臺中，當您的應用程式呼叫 `Stop` 方法時，`OnDisconnected` 事件處理常式會在伺服器上立即執行，而用戶端會引發 `Closed` 事件（此事件在 JavaScript 中會命名為 `disconnected`）。

如果用戶端應用程式或其執行所在的電腦損毀或進入睡眠狀態（例如，當使用者關閉膝上型電腦時），伺服器就不會收到發生什麼情況的通知。 只要伺服器知道，遺失用戶端可能是因為連線中斷，而且用戶端可能嘗試重新連線。 因此，在這些案例中，伺服器會等待讓用戶端有機會重新連線，而且 `OnDisconnected` 在中斷連線超時期間（預設為大約30秒）後才會執行。 下圖說明此案例。

![用戶端電腦失敗](handling-connection-lifetime-events/_static/image4.png)

<a id="serverdisconnect"></a>

### <a name="server-disconnection-scenarios"></a>伺服器中斷連接案例

當伺服器離線時--它會重新開機、失敗、應用程式網域回收等等。--結果可能類似于連線中斷，或傳輸 API 和 SignalR 可能會立即得知伺服器已消失，而 SignalR 可能會開始嘗試重新連線，而不會引發 `ConnectionSlow` 事件。 如果用戶端進入重新連線模式，且伺服器復原或重新開機，或是新的伺服器在中斷連接逾時期限到期之前上線，用戶端就會重新連接到已還原或新的伺服器。 在此情況下，SignalR 連接會繼續在用戶端上執行，並引發 `Reconnected` 事件。 在第一部伺服器上，一律不會執行 `OnDisconnected`，而在新的伺服器上，`OnReconnected` 會執行，但在之前，該伺服器上的該用戶端從未執行過 `OnConnected`。 （如果用戶端在重新開機或應用程式域回收後重新連線到相同的伺服器，效果就會相同，因為當伺服器重新開機時，它沒有任何記憶體的先前連線活動）。下圖假設傳輸 API 會立即察覺遺失的連線，因此不會引發 `ConnectionSlow` 事件。

![伺服器失敗和重新連接](handling-connection-lifetime-events/_static/image5.png)

如果伺服器在中斷連線超時時間內無法使用，SignalR 連接就會結束。 在此案例中，`Closed` 事件（在 JavaScript 用戶端中`disconnected`）會在用戶端上引發，但伺服器上永遠不會呼叫 `OnDisconnected`。 下圖假設傳輸 API 不會察覺到連線中斷，因此 SignalR keepalive 功能會偵測到該連接，並引發 `ConnectionSlow` 事件。

![伺服器失敗和超時](handling-connection-lifetime-events/_static/image6.png)

<a id="timeoutkeepalive"></a>

## <a name="timeout-and-keepalive-settings"></a>Timeout 和 keepalive 設定

預設 `ConnectionTimeout`、`DisconnectTimeout`和 `KeepAlive` 值適用于大部分的案例，但如果您的環境有特殊需求，則可加以變更。 例如，如果您的網路環境關閉閒置5秒的連線，您可能必須減少 keepalive 值。

<a id="connectiontimeout"></a>

### <a name="connectiontimeout"></a>ConnectionTimeout

這項設定代表在關閉傳輸連線並等候回應，然後開啟新的連線時，所需的時間量。 預設值為110秒。

此設定僅適用于停用 keepalive 功能時，這通常只適用于長時間輪詢傳輸。 下圖說明此設定在長輪詢傳輸連接上的效果。

![長時間輪詢傳輸連接](handling-connection-lifetime-events/_static/image7.png)

<a id="disconnecttimeout"></a>

### <a name="disconnecttimeout"></a>DisconnectTimeout

此設定代表在引發 `Disconnected` 事件之前，傳輸連線中斷後所要等待的時間量。 預設值為 30 秒。 當您設定 `DisconnectTimeout`時，`KeepAlive` 會自動設定為1/3 的 `DisconnectTimeout` 值。

<a id="keepalive"></a>

### <a name="keepalive"></a>KeepAlive

此設定代表透過閒置連線傳送 keepalive 封包之前要等待的時間量。 預設值為 10 秒。 此值不得超過1/3 的 `DisconnectTimeout` 值。

如果您想要同時設定 `DisconnectTimeout` 和 `KeepAlive`，請在 `DisconnectTimeout`之後設定 `KeepAlive`。 否則，當 `DisconnectTimeout` 自動將 `KeepAlive` 設定為 timeout 值的1/3 時，將會覆寫您的 `KeepAlive` 設定。

如果您想要停用 keepalive 功能，請將 `KeepAlive` 設定為 null。 長期輪詢傳輸會自動停用 Keepalive 功能。

<a id="changetimeout"></a>

### <a name="how-to-change-timeout-and-keepalive-settings"></a>如何變更 timeout 和 keepalive 設定

若要變更這些設定的預設值，請在*global.asax*檔案的 `Application_Start` 中設定它們，如下列範例所示。 範例程式碼中所顯示的值與預設值相同。

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample1.cs)]

<a id="notifydisconnect"></a>

## <a name="how-to-notify-the-user-about-disconnections"></a>如何通知使用者中斷連線

在某些應用程式中，當發生連線問題時，您可能會想要向使用者顯示訊息。 您有數個選項可用於執行此動作的方式和時機。 下列程式碼範例適用于使用所產生之 proxy 的 JavaScript 用戶端。

- 處理 `connectionSlow` 事件，以便在 SignalR 知道連線問題，然後進入重新連接模式之前，立即顯示訊息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample2.js)]
- 處理 `reconnecting` 事件，以在 SignalR 感知中斷連線且進入重新連接模式時顯示訊息。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample3.js)]
- 處理 `disconnected` 事件，以在嘗試重新連線時顯示訊息。在此案例中，重新建立與伺服器之連線的唯一方法是，藉由呼叫 `Start` 方法來重新開機 SignalR 連接，這會建立新的連線識別碼。 下列程式碼範例會使用旗標，確保您只會在重新連接的超時時間之後發出通知，而不是在正常結束後，透過呼叫 `Stop` 方法所造成的 SignalR 連接。

    [!code-javascript[Main](handling-connection-lifetime-events/samples/sample4.js)]

<a id="continuousreconnect"></a>

## <a name="how-to-continuously-reconnect"></a>如何持續重新連線

在某些應用程式中，您可能會想要在連線中斷之後自動重新建立連線，而重新連接的嘗試已超時。若要這麼做，您可以從 `Closed` 事件處理常式（JavaScript 用戶端上的`disconnected` 事件處理常式）呼叫 `Start` 方法。 在呼叫 `Start` 之前，您可能會想要等待一段時間，以避免在伺服器或實體連接無法使用時，過於頻繁地這麼做。 下列程式碼範例適用于使用所產生之 proxy 的 JavaScript 用戶端。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample5.js)]

在行動用戶端中必須注意的一個潛在問題是，當伺服器或實體連線無法使用時，連續重新連線嘗試可能會造成不必要的電池耗盡。

<a id="disconnectclientfromserver"></a>

## <a name="how-to-disconnect-a-client-in-server-code"></a>如何中斷用戶端與伺服器程式碼的連線

SignalR 第2版沒有內建的伺服器 API 可中斷用戶端的連線。 未來會有[新增這項功能的計畫](https://github.com/SignalR/SignalR/issues/2101)。 在目前的 SignalR 版本中，將用戶端與伺服器中斷連線的最簡單方式，就是在用戶端上執行 disconnect 方法，並從伺服器呼叫該方法。 下列程式碼範例會使用產生的 proxy，顯示 JavaScript 用戶端的中斷連接方法。

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample6.js)]

> [!WARNING]
> 安全性-這不是用來中斷用戶端連線的這種方法，也不是建議的內建 API，會解決因為用戶端可能會重新連線，或遭到駭客攻擊的程式碼可能會移除 `stopClient` 方法或變更其用途的攻擊。 執行具狀態的拒絕服務（DOS）保護的適當位置不在架構或伺服器層中，而是在前端基礎結構中。

<a id="detectingreasonfordisconnection"></a>
## <a name="detecting-the-reason-for-a-disconnection"></a>偵測中斷連接的原因

SignalR 2.1 會將多載加入伺服器 `OnDisconnect` 事件，以指出用戶端是否刻意中斷連接，而不是計時。如果用戶端明確關閉連接，`StopCalled` 參數為 true。 在 JavaScript 中，如果伺服器錯誤導致用戶端中斷連線，錯誤資訊會以 `$.connection.hub.lastError`的形式傳遞給用戶端。

**C#伺服器程式碼： `stopCalled` 參數**

[!code-csharp[Main](handling-connection-lifetime-events/samples/sample7.cs?highlight=1,3)]

**JavaScript 用戶端程式代碼：存取 `disconnect` 事件中的 `lastError`。**

[!code-javascript[Main](handling-connection-lifetime-events/samples/sample8.js?highlight=2-3)]
