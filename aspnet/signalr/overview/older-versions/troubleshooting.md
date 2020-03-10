---
uid: signalr/overview/older-versions/troubleshooting
title: SignalR 疑難排解（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: 本文說明開發 SignalR 應用程式的常見問題。
ms.author: bradyg
ms.date: 06/05/2013
ms.assetid: 347210ba-c452-4feb-886f-b51d89f58971
msc.legacyurl: /signalr/overview/older-versions/troubleshooting
msc.type: authoredcontent
ms.openlocfilehash: 3dbf091ac2daa4da477b405852bb4d1316584fcd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579601"
---
# <a name="signalr-troubleshooting-signalr-1x"></a>SignalR 疑難排解 (SignalR 1.x)

由[派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本檔說明 SignalR 的常見疑難排解問題。

本檔包含下列各節。

- [在用戶端與伺服器之間呼叫方法無訊息失敗](#connection)
- [其他連接問題](#other)
- [編譯和伺服器端錯誤](#server)
- [Visual Studio 問題](#vs)
- [Internet Information Services 問題](#iis)
- [Azure 問題](#azure)

<a id="connection"></a>

## <a name="calling-methods-between-the-client-and-server-silently-fails"></a>在用戶端與伺服器之間呼叫方法無訊息失敗

本節描述用戶端和伺服器之間方法呼叫失敗的可能原因，而不會有有意義的錯誤訊息。 在 SignalR 應用程式中，伺服器不會有用戶端所執行之方法的相關資訊;當伺服器叫用用戶端方法時，方法名稱和參數資料會傳送至用戶端，而且只有在該方法是以伺服器指定的格式存在時，才會執行它。 如果在用戶端上找不到相符的方法，就不會發生任何事，也不會在伺服器上引發錯誤訊息。

若要進一步調查不會呼叫的用戶端方法，您可以在呼叫中樞上的啟動方法之前開啟記錄功能，以查看來自伺服器的呼叫。 若要在 JavaScript 應用程式中啟用記錄，請參閱[如何啟用用戶端記錄（JavaScript 用戶端版本）](../guide-to-the-api/hubs-api-guide-javascript-client.md#logging)。 若要在 .NET 用戶端應用程式中啟用記錄，請參閱[如何啟用用戶端記錄（.Net 用戶端版本）](../guide-to-the-api/hubs-api-guide-net-client.md#logging)。

### <a name="misspelled-method-incorrect-method-signature-or-incorrect-hub-name"></a>拼錯的方法、不正確的方法簽章或不正確的中樞名稱

如果所呼叫方法的名稱或簽章不完全符合用戶端上的適當方法，則呼叫將會失敗。 確認伺服器所呼叫的方法名稱符合用戶端上的方法名稱。 此外，SignalR 會使用 camel 大小寫方法建立中樞 proxy，如同在 JavaScript 中適用，因此會在用戶端 proxy 中呼叫在伺服器上 `SendMessage` 的方法 `sendMessage`。 如果您在伺服器端程式碼中使用 `HubName` 屬性，請確認所使用的名稱符合用來在用戶端上建立中樞的名稱。 如果您未使用 `HubName` 屬性，請確認 JavaScript 用戶端中的中樞名稱為 camel 大小寫，例如 chatHub，而不是 ChatHub。

### <a name="duplicate-method-name-on-client"></a>用戶端上重複的方法名稱

請確認您的用戶端上沒有重複的方法，只有大小寫不同。 如果您的用戶端應用程式有一個稱為 `sendMessage`的方法，請確認也沒有稱為 `SendMessage` 的方法。

### <a name="missing-json-parser-on-the-client"></a>用戶端上缺少 JSON 剖析器

SignalR 需要有 JSON 剖析器，才能序列化伺服器和用戶端之間的呼叫。 如果您的用戶端沒有內建的 JSON 剖析器（例如 Internet Explorer 7），您必須在應用程式中包含一個。 您可以在[這裡](http://nuget.org/packages/json2)下載 JSON 剖析器。

### <a name="mixing-hub-and-persistentconnection-syntax"></a>混合中樞和 PersistentConnection 語法

SignalR 使用兩種通訊模型：中樞和 PersistentConnections。 在用戶端程式代碼中呼叫這兩種通訊模型的語法不同。 如果您已在伺服器程式碼中新增中樞，請確認您的所有用戶端程式代碼都使用適當的中樞語法。

**在 JavaScript 用戶端中建立 PersistentConnection 的 JavaScript 用戶端程式代碼**

[!code-javascript[Main](troubleshooting/samples/sample1.js)]

**在 JAVAscript 用戶端中建立中樞 Proxy 的 JavaScript 用戶端程式代碼**

[!code-javascript[Main](troubleshooting/samples/sample2.js)]

**C#將路由對應至 PersistentConnection 的伺服器程式碼**

[!code-csharp[Main](troubleshooting/samples/sample3.cs)]

**C#將路由對應至中樞的伺服器程式碼，如果您有多個應用程式，則為多個中樞**

[!code-csharp[Main](troubleshooting/samples/sample4.cs)]

### <a name="connection-started-before-subscriptions-are-added"></a>在新增訂閱之前啟動連線

如果在可以從伺服器呼叫的方法加入至 proxy 之前，中樞的連線已啟動，則不會收到訊息。 下列 JavaScript 程式碼不會正確啟動中樞：

**不正確的 JavaScript 用戶端程式代碼將不允許接收中樞訊息**

[!code-javascript[Main](troubleshooting/samples/sample5.js)]

請改為在呼叫 Start 之前新增方法訂閱：

**將訂用帳戶正確新增至中樞的 JavaScript 用戶端程式代碼**

[!code-javascript[Main](troubleshooting/samples/sample6.js)]

### <a name="missing-method-name-on-the-hub-proxy"></a>中樞 proxy 上缺少方法名稱

確認伺服器上定義的方法已在用戶端上訂閱。 即使伺服器定義方法，仍然必須將它加入至用戶端 proxy。 方法可以透過下列方式新增至用戶端 proxy （請注意，方法會新增至中樞的 `client` 成員，而不是直接加入中樞）：

**將方法新增至中樞 proxy 的 JavaScript 用戶端程式代碼**

[!code-javascript[Main](troubleshooting/samples/sample7.js)]

### <a name="hub-or-hub-methods-not-declared-as-public"></a>中樞或中樞方法未宣告為公用

若要在用戶端上顯示，中樞的執行和方法必須宣告為 `public`。

### <a name="accessing-hub-from-a-different-application"></a>從不同的應用程式存取中樞

SignalR Hub 只能透過執行 SignalR 用戶端的應用程式來存取。 SignalR 無法與其他通訊庫（例如 SOAP 或 WCF web 服務）相交互操作。如果您的目標平臺沒有可用的 SignalR 用戶端，您就無法直接存取伺服器的端點。

### <a name="manually-serializing-data"></a>手動序列化資料

SignalR 會自動使用 JSON 來序列化您的方法參數，而不需要自行執行此動作。

### <a name="remote-hub-method-not-executed-on-client-in-ondisconnected-function"></a>遠端中樞方法未在 OnDisconnected 函式的用戶端上執行

這是設計的行為。 呼叫 `OnDisconnected` 時，中樞已經進入 `Disconnected` 狀態，這不允許呼叫進一步的中樞方法。

**C#在 OnDisconnected 事件中正確執行程式碼的伺服器程式碼**

[!code-csharp[Main](troubleshooting/samples/sample8.cs)]

### <a name="connection-limit-reached"></a>已達到連接限制

在 Windows 7 之類的用戶端作業系統上使用完整版的 IIS 時，會強加10個連線限制。 使用用戶端 OS 時，請改用 IIS Express 以避免此限制。

### <a name="cross-domain-connection-not-set-up-properly"></a>未正確設定跨網域連線

如果跨網域連線（SignalR URL 與主控頁面不在相同網域中的連線）未正確設定，則連接可能會失敗，且不會出現錯誤訊息。 如需如何啟用跨網域通訊的相關資訊，請參閱[如何建立跨網域](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)連線。

### <a name="connection-using-ntlm-active-directory-not-working-in-net-client"></a>使用 NTLM （Active Directory）的連接在 .NET 用戶端中無法運作

如果連接未正確設定，在 .NET 用戶端應用程式中使用網域安全性的連接可能會失敗。 若要在網域環境中使用 SignalR，請設定必要的連接屬性，如下所示：

**C#執行連接認證的用戶端程式代碼**

[!code-csharp[Main](troubleshooting/samples/sample9.cs)]

<a id="other"></a>

## <a name="other-connection-issues"></a>其他連接問題

本節說明連線期間所發生之特定徵兆或錯誤訊息的原因和解決方案。

### <a name="start-must-be-called-before-data-can-be-sent-error"></a>「必須在可以傳送資料之前呼叫啟動」錯誤

如果在啟動連接之前，程式碼參考 SignalR 物件，通常會出現此錯誤。 在連接完成之後，必須新增處理常式的裝設，以及將呼叫在伺服器上定義之方法的 like。 請注意，`Start` 的呼叫是非同步，因此呼叫之後的程式碼可能會在完成之前執行。 在連接完全啟動之後加入處理常式的最佳方式，是將它們放入回呼函式，並以參數的形式傳遞給 start 方法：

**可正確加入參考 SignalR 物件之事件處理常式的 JavaScript 用戶端程式代碼**

[!code-javascript[Main](troubleshooting/samples/sample10.js?highlight=1)]

如果在仍在參考 SignalR 物件的情況下，連接停止，也會出現此錯誤。

### <a name="301-moved-permanently-or-302-moved-temporarily-error"></a>「已永久移動301」或「已暫時移動302」錯誤

如果專案包含名為 SignalR 的資料夾，這會干擾自動建立的 proxy，可能會出現此錯誤。 若要避免這個錯誤，請不要在應用程式中使用名為 `SignalR` 的資料夾，或關閉自動產生 proxy。 如需更多詳細資料，請參閱[產生的 Proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。

### <a name="403-forbidden-error-in-net-or-silverlight-client"></a>.NET 或 Silverlight 用戶端發生「403禁止」錯誤

跨網域的環境中，如果未正確啟用跨網域通訊，則可能會發生此錯誤。 如需如何啟用跨網域通訊的相關資訊，請參閱[如何建立跨網域](../guide-to-the-api/hubs-api-guide-javascript-client.md#crossdomain)連線。 若要在 Silverlight 用戶端中建立跨網域連接，請參閱[silverlight 用戶端的跨網域](../guide-to-the-api/hubs-api-guide-net-client.md#slcrossdomain)連線。

### <a name="404-not-found-error"></a>「找不到404」錯誤

發生此問題的原因有好幾個。 確認下列所有事項：

- **中樞 proxy 位址參考的格式不正確：** 如果所產生之中樞 proxy 位址的參考格式不正確，通常會出現此錯誤。 確認已正確地對中樞位址進行參考。 如需詳細資訊，請參閱[如何參考動態產生的 proxy](../guide-to-the-api/hubs-api-guide-javascript-client.md#dynamicproxy) 。
- 新增**路由至應用程式，再新增中樞路由：** 如果您的應用程式使用其他路由，請確認新增的第一個路由是 `MapHubs`的呼叫。

### <a name="500-internal-server-error"></a>「500內部伺服器錯誤」

這是一個非常一般的錯誤，可能會有各種不同的原因。 錯誤的詳細資料應該會出現在伺服器的事件記錄檔中，或透過偵測伺服器來找到。 藉由開啟伺服器上的詳細錯誤，可取得更詳細的錯誤資訊。 如需詳細資訊，請參閱[如何處理中樞類別中的錯誤](../guide-to-the-api/hubs-api-guide-server.md#handleErrors)。

### <a name="typeerror-lthubtypegt-is-undefined-error"></a>「TypeError： &lt;hubType&gt; 未定義」錯誤

如果未正確呼叫 `MapHubs`，將會產生此錯誤。 如需詳細資訊，請參閱[如何註冊 SignalR 路由和設定 SignalR 選項](../guide-to-the-api/hubs-api-guide-server.md#route)。

### <a name="jsonserializationexception-was-unhandled-by-user-code"></a>JsonSerializationException 已由使用者程式碼未處理

確認您傳送至方法的參數不包含非可序列化的類型（例如檔案控制代碼或資料庫連接）。 如果您需要在不想要傳送至用戶端的伺服器端物件上使用成員（基於安全性或序列化的原因），請使用 `JSONIgnore` 屬性。

### <a name="protocol-error-unknown-transport-error"></a>「通訊協定錯誤：未知的傳輸」錯誤

如果用戶端不支援 SignalR 所使用的傳輸，則可能會發生此錯誤。 如需可與 SignalR 搭配使用之瀏覽器的相關資訊，請參閱[傳輸和回退](../getting-started/introduction-to-signalr.md#transports)。

### <a name="javascript-hub-proxy-generation-has-been-disabled"></a>「JavaScript 中樞 proxy 產生已停用。」

如果設定了 `DisableJavaScriptProxies`，同時包含 `signalr/hubs`上動態產生之 proxy 的參考，就會發生這個錯誤。 如需手動建立 proxy 的詳細資訊，請參閱[產生的 proxy 和它為您提供的功能](../guide-to-the-api/hubs-api-guide-javascript-client.md#genproxy)。

### <a name="the-connection-id-is-in-the-incorrect-format-or-the-user-identity-cannot-change-during-an-active-signalr-connection-error"></a>「連線識別碼的格式不正確」或「使用者識別在使用中的 SignalR 連接期間無法變更」錯誤

如果正在使用驗證，而且在連線停止之前，用戶端已登出，可能會出現此錯誤。 解決方法是在登出用戶端之前，先停止 SignalR 連接。

### <a name="uncaught-error-signalr-jquery-not-found-please-ensure-jquery-is-referenced-before-the-signalrjs-file-error"></a>「未攔截的錯誤： SignalR：找不到 jQuery。 請確定已在 SignalR .js 檔案之前參考 jQuery」錯誤

SignalR JavaScript 用戶端需要 jQuery 才能執行。 請確認您對 jQuery 的參考是否正確、使用的路徑是否有效，以及 jQuery 的參考是否在 SignalR 的參考之前。

### <a name="uncaught-typeerror-cannot-read-property-ltpropertygt-of-undefined-error"></a>「未攔截的 TypeError：無法讀取屬性 '&lt;屬性&gt;' 未定義」錯誤

此錯誤的結果是未正確參考 jQuery 或中樞 proxy。 請確認您對 jQuery 和中樞 proxy 的參考是否正確、使用的路徑是否有效，以及 jQuery 的參考是否在中樞 proxy 的參考之前。 中樞 proxy 的預設參考看起來應該如下所示：

**正確參考中樞 proxy 的 HTML 用戶端程式代碼**

[!code-html[Main](troubleshooting/samples/sample11.html)]

### <a name="runtimebinderexception-was-unhandled-by-user-code-error"></a>「RuntimeBinderException 由使用者程式碼未處理」錯誤

使用不正確的 `Hub.On` 多載時，可能會發生此錯誤。 如果方法有傳回值，則傳回型別必須指定為泛型型別參數：

**在用戶端上定義的方法（不含產生的 proxy）**

[!code-html[Main](troubleshooting/samples/sample12.html?highlight=1)]

### <a name="connection-id-is-inconsistent-or-connection-breaks-between-page-loads"></a>連接識別碼不一致，或頁面載入之間的連接中斷

這是設計的行為。 由於中樞物件裝載于 page 物件中，因此當頁面重新整理時，中樞會遭到終結。 多頁應用程式必須維護使用者與連接識別碼之間的關聯，以便在頁面載入之間保持一致。 連接識別碼可以儲存在伺服器上的 `ConcurrentDictionary` 物件或資料庫中。

### <a name="value-cannot-be-null-error"></a>「值不能為 null」錯誤

目前不支援具有選擇性參數的伺服器端方法;如果省略了選擇性參數，方法將會失敗。 如需詳細資訊，請參閱[選擇性參數](https://github.com/SignalR/SignalR/issues/324)。

### <a name="firefox-cant-establish-a-connection-to-the-server-at-ltaddressgt-error-in-firebug"></a>「Firefox 無法在 Firebug 時建立與伺服器的連接，&lt;位址&gt;」錯誤

如果 WebSocket 傳輸的協商失敗，而改用另一個傳輸，則會在 Firebug 中看到此錯誤訊息。 這是設計的行為。

### <a name="the-remote-certificate-is-invalid-according-to-the-validation-procedure-error-in-net-client-application"></a>.NET 用戶端應用程式中的「根據驗證程式，遠端憑證無效」錯誤

如果您的伺服器需要自訂用戶端憑證，您可以在提出要求之前，將 x509certificate 新增至連接。 使用 `Connection.AddClientCertificate`將憑證新增至連接。

### <a name="connection-drops-after-authentication-times-out"></a>驗證超時之後中斷連接

這是設計的行為。 當連接啟用時，無法修改驗證認證;若要重新整理認證，必須停止並重新啟動連接。

### <a name="onconnected-gets-called-twice-when-using-jquery-mobile"></a>使用 jQuery Mobile 時，會呼叫 OnConnected 兩次

jQuery Mobile 的 `initializePage` 函式會強制重新執行每個頁面中的腳本，因此會建立第二個連接。 此問題的解決方案包括：

- 在您的 JavaScript 檔案之前包含 jQuery Mobile 的參考。
- 藉由設定 `$.mobile.autoInitializePage = false`來停用 `initializePage` 函數。
- 等候頁面完成初始化，再開始連接。

### <a name="messages-are-delayed-in-silverlight-applications-using-server-sent-events"></a>使用伺服器傳送事件的 Silverlight 應用程式中的訊息延遲

在 Silverlight 上使用伺服器傳送事件時，會延遲訊息。 若要改為強制使用長輪詢，請在啟動連線時使用下列內容：

[!code-css[Main](troubleshooting/samples/sample13.css)]

### <a name="permission-denied-using-forever-frame-protocol"></a>「拒絕許可權」使用永久框架通訊協定

這是已知的問題，如[這裡](https://github.com/SignalR/SignalR/issues/1963)所述。 您可以使用最新的 JQuery 程式庫看到此徵兆;因應措施是將您的應用程式降級至 JQuery 1.8.2。

<a id="server"></a>

## <a name="compilation-and-server-side-errors"></a>編譯和伺服器端錯誤

 下一節包含編譯器和伺服器端執行時間錯誤的可能解決方案。 

### <a name="reference-to-hub-instance-is-null"></a>中樞實例的參考為 null

由於會針對每個連接建立中樞實例，因此您無法自行在程式碼中建立中樞的實例。 若要從中樞本身外部呼叫中樞上的方法，請參閱[如何從中樞類別外部呼叫用戶端方法和管理群組](../guide-to-the-api/hubs-api-guide-server.md#callfromoutsidehub)，以瞭解如何取得中樞內容的參考。

### <a name="httpcontextcurrentsession-is-null"></a>HTTPCoNtext。會話為 null

這是設計的行為。 SignalR 不支援 ASP.NET 會話狀態，因為啟用會話狀態會中斷雙工訊息。

### <a name="no-suitable-method-to-override"></a>沒有適合的覆寫方法

如果您使用舊版檔或 blog 中的程式碼，可能會看到此錯誤。 請確認您未參考已變更或已淘汰之方法的名稱（例如 `OnConnectedAsync`）。

### <a name="hostcontextextensionswebsocketserverurl-is-null"></a>HostCoNtextExtensions. WebSocketServerUrl 為 null

這是設計的行為。 這個成員已被取代，不應使用。

### <a name="a-route-named-signalrhubs-is-already-in-the-route-collection-error"></a>「路由集合中已有名為 ' signalr ' 的路由」錯誤

如果您的應用程式呼叫了兩次 `MapHubs`，就會出現此錯誤。 某些範例應用程式會直接呼叫全域應用程式檔中的 `MapHubs`;其他則會在包裝函式類別中進行呼叫。 請確定您的應用程式不會同時執行這兩項操作。

<a id="vs"></a>

## <a name="visual-studio-issues"></a>Visual Studio 問題

本節說明 Visual Studio 中遇到的問題。

### <a name="script-documents-node-does-not-appear-in-solution-explorer"></a>[指令檔] 節點不會出現在方案總管

我們的一些教學課程會在進行調試時，將您導向方案總管中的 [指令檔] 節點。 這個節點是由 JavaScript 偵錯工具所產生，而且只會在在 Internet Explorer 中進行瀏覽器用戶端的偵測時出現;如果使用 Chrome 或 Firefox，節點將不會出現。 如果另一個用戶端偵錯工具正在執行（例如 Silverlight 偵錯工具），JavaScript 偵錯工具也不會執行。

### <a name="signalr-does-not-work-on-visual-studio-2008-or-earlier"></a>SignalR 無法在 Visual Studio 2008 或更早版本上運作

這是設計的行為。 SignalR 需要 .NET Framework 4 或更新版本;這需要在 Visual Studio 2010 或更新版本中開發 SignalR 應用程式。

<a id="iis"></a>

## <a name="iis-issues"></a>IIS 問題

本節包含 Internet Information Services 的問題。

### <a name="web-site-crashes-after-maphubs-call"></a>MapHubs 呼叫後網站損毀

此問題已在最新版本的 SignalR 中修正。 使用 NuGet 更新安裝，以確認您使用的是最新發行版本的 SignalR。

<a id="azure"></a>

## <a name="azure-issues"></a>Azure 問題

本節包含 Microsoft Azure 的問題。

### <a name="messages-are-not-received-through-the-azure-backplane-after-altering-topic-names"></a>修改主題名稱之後，不會透過 Azure 後擋板接收訊息

Azure 背板所使用的主題不適合用來進行使用者可設定。
