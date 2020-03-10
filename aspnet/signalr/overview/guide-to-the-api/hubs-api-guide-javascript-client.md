---
uid: signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
title: ASP.NET SignalR 中樞 API 指南-JavaScript 用戶端 |Microsoft Docs
author: bradygaster
description: 本檔介紹如何在 JavaScript 用戶端（例如瀏覽器和 Windows Store （WinJS） applicat）中使用適用于 SignalR 第2版的中樞 API。
ms.author: bradyg
ms.date: 01/15/2019
ms.assetid: a9fd4dc0-1b96-4443-82ca-932a5b4a8ea4
msc.legacyurl: /signalr/overview/guide-to-the-api/hubs-api-guide-javascript-client
msc.type: authoredcontent
ms.openlocfilehash: 8befe133c3627dac1f7d011959c68e2054d345da
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536656"
---
# <a name="aspnet-signalr-hubs-api-guide---javascript-client"></a>ASP.NET SignalR 中樞 API 指南-JavaScript 用戶端

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本檔介紹如何在 JavaScript 用戶端（例如瀏覽器和 Windows Store （WinJS）應用程式）中使用適用于 SignalR 第2版的中樞 API。
>
> SignalR 中樞 API 可讓您從伺服器對連線的用戶端，以及從用戶端到伺服器進行遠端程序呼叫（Rpc）。 在伺服器程式碼中，您會定義可由用戶端呼叫的方法，並呼叫在用戶端上執行的方法。 在用戶端程式代碼中，您可以定義可從伺服器呼叫的方法，並呼叫在伺服器上執行的方法。 SignalR 會為您處理所有的用戶端對伺服器管道。
>
> SignalR 也提供名為「持續連線」的較低層級 API。 如需 SignalR、中樞和持續連線的簡介，請參閱[SignalR 簡介](../getting-started/introduction-to-signalr.md)。
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

本文件包含下列章節：

- [產生的 proxy，以及它為您做的工作](#genproxy)

    - [使用產生的 proxy 的時機](#cantusegenproxy)
- [用戶端設定](#clientsetup)

    - [如何參考動態產生的 proxy](#dynamicproxy)
    - [如何為 SignalR 產生的 proxy 建立實體檔案](#manualproxy)
- [如何建立連接](#establishconnection)

    - [$. connection. hub 是 $. hubConnection （）建立的相同物件](#connequivalence)
    - [非同步執行 start 方法](#asyncstart)
- [如何建立跨網域連線](#crossdomain)
- [如何設定連線](#configureconnection)

    - [如何指定查詢字串參數](#querystring)
    - [如何指定傳輸方法](#transport)
- [如何取得中樞類別的 proxy](#getproxy)
- [如何在用戶端上定義伺服器可以呼叫的方法](#callclient)
- [如何從用戶端呼叫伺服器方法](#callserver)
- [如何處理連接存留期事件](#connectionlifetime)
- [如何處理錯誤](#handleerrors)
- [如何啟用用戶端記錄](#logging)

如需如何針對伺服器或 .NET 用戶端進行程式設計的相關檔，請參閱下列資源：

- [SignalR 中樞 API 指南-伺服器](hubs-api-guide-server.md)
- [SignalR 中樞 API 指南-.NET 用戶端](hubs-api-guide-net-client.md)

SignalR 2 伺服器元件僅適用于 .NET 4.5 （但 .NET 4.0 上有適用于 SignalR 2 的 .NET 用戶端）。

<a id="genproxy"></a>

## <a name="the-generated-proxy-and-what-it-does-for-you"></a>產生的 proxy，以及它為您做的工作

您可以將 JavaScript 用戶端程式設計成與 SignalR 服務進行通訊，而不需要 SignalR 為您產生的 proxy。 Proxy 的用途是簡化您用來連接的程式碼語法、撰寫伺服器呼叫的方法，以及在伺服器上呼叫方法。

當您撰寫程式碼來呼叫伺服器方法時，產生的 proxy 可讓您使用看起來像是執列區域函式的語法：您可以撰寫 `serverMethod(arg1, arg2)`，而不是 `invoke('serverMethod', arg1, arg2)`。 如果您拼錯伺服器方法名稱，產生的 proxy 語法也會啟用立即且可理解的用戶端錯誤。 而且，如果您手動建立定義 proxy 的檔案，您也可以取得 IntelliSense 支援來撰寫呼叫伺服器方法的程式碼。

例如，假設您在伺服器上有下列中樞類別：

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample1.cs?highlight=1,3,5)]

下列程式碼範例顯示在伺服器上叫用 `NewContosoChatMessage` 方法，以及從伺服器接收 `addContosoChatMessageToPage` 方法的調用，JavaScript 程式碼的外觀。

**使用產生的 proxy**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample2.js?highlight=1-2,8)]

**沒有產生的 proxy**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample3.js?highlight=2-3,9)]

<a id="cantusegenproxy"></a>

### <a name="when-to-use-the-generated-proxy"></a>使用產生的 proxy 的時機

如果您想要為伺服器呼叫的用戶端方法註冊多個事件處理常式，則無法使用產生的 proxy。 否則，您可以選擇使用產生的 proxy，或不根據編碼喜好設定。 如果您選擇不使用它，就不需要在用戶端程式代碼的 `script` 元素中參考 "signalr/hub" URL。

<a id="clientsetup"></a>

## <a name="client-setup"></a>用戶端設定

JavaScript 用戶端需要參考 jQuery 和 SignalR core JavaScript 檔案。 JQuery 版本必須是1.6.4 或主要的較新版本，例如1.7.2、1.8.2 或1.9.1。 如果您決定使用產生的 proxy，您也需要 SignalR 產生的 proxy JavaScript 檔案的參考。 下列範例顯示在使用所產生之 proxy 的 HTML 頁面中，參考可能看起來的樣子。

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample4.html)]

這些參考必須以下列順序包含： jQuery first、SignalR core after 之後，以及 SignalR proxy last。

<a id="dynamicproxy"></a>

### <a name="how-to-reference-the-dynamically-generated-proxy"></a>如何參考動態產生的 proxy

在上述範例中，SignalR 產生之 proxy 的參考是動態產生的 JavaScript 程式碼，而不是實體檔案。 SignalR 會即時建立 proxy 的 JavaScript 程式碼，並將其提供給用戶端，以回應 "/signalr/hubs" URL。 如果您在 `MapSignalR` 方法中，針對伺服器上的 SignalR 連線指定不同的基底 URL，則動態產生之 proxy 檔案的 URL 就是您的自訂 URL，其中附加了 "/hubs"。

> [!NOTE]
> 若是 Windows 8 （Windows Store） JavaScript 用戶端，請使用實體 proxy 檔案，而不是動態產生的檔案。 如需詳細資訊，請參閱本主題稍後的[如何為 SignalR 產生的 proxy 建立實體](#manualproxy)檔案。

在 ASP.NET MVC 4 或 5 Razor view 中，使用波狀符號來參考 proxy 檔案參考中的應用程式根目錄：

[!code-html[Main](hubs-api-guide-javascript-client/samples/sample5.html)]

如需在 MVC 5 中使用 SignalR 的詳細資訊，請參閱[使用 SignalR 和 MVC 5 的消費者入門](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)。

在 ASP.NET MVC 3 Razor view 中，針對您的 proxy 檔案參考使用 `Url.Content`：

[!code-cshtml[Main](hubs-api-guide-javascript-client/samples/sample6.cshtml)]

在 ASP.NET Web Forms 應用程式中，針對您的 proxy 檔案參考使用 `ResolveClientUrl`，或使用應用程式根目錄相對路徑（以波狀開頭）透過 ScriptManager 進行註冊：

[!code-aspx[Main](hubs-api-guide-javascript-client/samples/sample7.aspx)]

一般的規則是，使用相同的方法來指定用於 CSS 或 JavaScript 檔案的 "/signalr/hubs" URL。 如果您指定 URL 而不使用波狀符號，在某些情況下，當您使用 IIS Express 在 Visual Studio 中測試時，您的應用程式將會正常運作，但當您部署至完整 IIS 時，將會失敗並出現404錯誤。 如需詳細資訊，請參閱 MSDN 網站上的[Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx)中的在 web 伺服器中**解析根層級資源的參考**。

當您以 debug 模式在 Visual Studio 2017 中執行 Web 專案時，如果您使用 Internet Explorer 作為瀏覽器，您可以在 [**腳本**] 底下的**方案總管**中看到 proxy 檔案。

若要查看檔案的內容，請按兩下 [**中樞**]。 如果您不是使用 Visual Studio 2012 或2013及 Internet Explorer，或如果您不是在 [偵錯工具] 模式中，您也可以流覽至 "/signalR/hubs" URL 來取得檔案的內容。 例如，如果您的網站是在 `http://localhost:56699`執行，請在瀏覽器中移至 `http://localhost:56699/SignalR/hubs`。

<a id="manualproxy"></a>

### <a name="how-to-create-a-physical-file-for-the-signalr-generated-proxy"></a>如何為 SignalR 產生的 proxy 建立實體檔案

除了動態產生的 proxy 以外，您還可以建立具有 proxy 程式碼並參考該檔案的實體檔案。 您可能想要這麼做，以控制快取或組合行為，或在編碼呼叫伺服器方法時取得 IntelliSense。

若要建立 proxy 檔案，請執行下列步驟：

1. 安裝[SignalR Utils](https://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/) NuGet 套件。
2. 開啟命令提示字元，並流覽至包含 SignalR 檔案的 [*工具*] 資料夾。 [工具] 資料夾位於下列位置：

    `[your solution folder]\packages\Microsoft.AspNet.SignalR.Utils.2.1.0\tools`
3. 輸入下列命令：

    `signalr ghp /path:[path to the .dll that contains your Hub class]`

    *.Dll*的路徑通常是專案資料夾中的*bin*資料夾。

    此命令會在與*signalr*相同的資料夾中建立名為*node.js*的檔案。
4. 將*server .js*檔案放在專案的適當資料夾中，將它重新命名為適用于您的應用程式，並在其中新增參考以取代 "signalr/hub" 參考。

<a id="establishconnection"></a>

## <a name="how-to-establish-a-connection"></a>如何建立連接

建立連接之前，您必須先建立連線物件、建立 proxy，以及註冊可從伺服器呼叫之方法的事件處理常式。 設定 proxy 和事件處理常式時，藉由呼叫 `start` 方法來建立連接。

如果您使用產生的 proxy，則不需要在自己的程式碼中建立連線物件，因為產生的 proxy 程式碼會為您執行此工作。

<a id="nogenconnection"></a>

**建立連接（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample8.js?highlight=5)]

**建立連接（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample9.js?highlight=1,6)]

範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。 如需有關如何指定不同基底 URL 的詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。

根據預設，中樞位置是目前的伺服器;如果您要連接到不同的伺服器，請在呼叫 `start` 方法之前指定 URL，如下列範例所示：

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample10.js)]

> [!NOTE]
> 通常您會先註冊事件處理常式，然後再呼叫 `start` 方法來建立連接。 如果您想要在建立連接之後註冊一些事件處理常式，可以這麼做，但是在呼叫 `start` 方法之前，必須先註冊至少一個事件處理常式。 其中一個原因是應用程式中可以有許多中樞，但您不想要在每個中樞上觸發 `OnConnected` 事件（若您只打算使用其中一個）。 建立連線時，在中樞的 proxy 上存在用戶端方法，會告訴 SignalR 觸發 `OnConnected` 事件。 如果您未在呼叫 `start` 方法之前註冊任何事件處理常式，則可以在中樞上叫用方法，但不會呼叫中樞的 `OnConnected` 方法，也不會從伺服器叫用任何用戶端方法。

<a id="connequivalence"></a>

### <a name="connectionhub-is-the-same-object-that-hubconnection-creates"></a>$. connection. hub 是 $. hubConnection （）建立的相同物件

如您在範例中所見，當您使用產生的 proxy 時，`$.connection.hub` 會參考連線物件。 當您未使用產生的 proxy 時，您可以藉由呼叫 `$.hubConnection()` 來取得相同的物件。 產生的 proxy 程式碼會藉由執行下列語句，為您建立連接：

![在產生的 proxy 檔案中建立連接](hubs-api-guide-javascript-client/_static/image3.png)

當您使用產生的 proxy 時，您可以使用 `$.connection.hub` 執行任何動作，而當您不使用產生的 proxy 時，可以使用連線物件來執行此作業。

<a id="asyncstart"></a>

### <a name="asynchronous-execution-of-the-start-method"></a>非同步執行 start 方法

`start` 方法會以非同步方式執行。 它會傳回[JQuery 延遲物件](http://api.jquery.com/category/deferred-object/)，這表示您可以藉由呼叫方法（例如 `pipe`、`done`和 `fail`）來加入回呼函數。 如果您有想要在建立連接之後執行的程式碼（例如，呼叫伺服器方法），請將該程式碼放在回呼函式中，或從回呼函數呼叫它。 `.done` 回呼方法是在建立連接之後執行，而且在伺服器上的 `OnConnected` 事件處理常式方法中擁有的任何程式碼完成執行之後。

如果您將上述範例中的「立即連線」語句放在 `start` 方法呼叫之後的下一行程式碼（而不是在 `.done` 回呼中），則會在建立連接之前執行 `console.log` 行，如下列範例所示：

![在建立連接之後執行的程式碼撰寫錯誤的方式](hubs-api-guide-javascript-client/_static/image5.png)

<a id="crossdomain"></a>

## <a name="how-to-establish-a-cross-domain-connection"></a>如何建立跨網域連線

通常，如果瀏覽器從 `http://contoso.com`載入頁面，則 SignalR 連接會位於相同的網域中，`http://contoso.com/signalr`。 如果 `http://contoso.com` 的頁面建立與 `http://fabrikam.com/signalr`的連接，這就是跨網域的連線。 基於安全考慮，預設會停用跨網域連線。

在 SignalR 1.x 中，跨網域要求是由單一 EnableCrossDomain 旗標所控制。 此旗標會同時控制 JSONP 和 CORS 要求。 為了提供更大的彈性，所有 CORS 支援都已從 SignalR 的伺服器元件中移除（如果偵測到瀏覽器支援，JavaScript 用戶端仍會正常使用 CORS），而且已提供新的 OWIN 中介軟體來支援這些案例。

如果用戶端需要 JSONP （以支援舊版瀏覽器中的跨網域要求），則必須將 `HubConfiguration` 物件上的 `EnableJSONP` 設定為 `true`，以明確地啟用它，如下所示。 預設會停用 JSONP，因為它的安全性不如 CORS。

**將 Owin 新增至您的專案：** 若要安裝此程式庫，請在 [套件管理員主控台] 中執行下列命令：

`Install-Package Microsoft.Owin.Cors`

此命令會將套件的2.1.0 版本新增至您的專案。

### <a name="calling-usecors"></a>呼叫 UseCors

 下列程式碼片段示範如何在 SignalR 2 中執行跨網域連接。

**在 SignalR 2 中執行跨網域要求**

下列程式碼示範如何在 SignalR 2 專案中啟用 CORS 或 JSONP。 這個程式碼範例會使用 `Map` 和 `RunSignalR`，而不是 `MapSignalR`，因此 CORS 中介軟體只會針對需要 CORS 支援的 SignalR 要求（而不是在 `MapSignalR`中指定之路徑上的所有流量）執行。對應也可以用於需要針對特定 URL 前置詞執行的任何其他中介軟體，而不是針對整個應用程式。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample11.cs)]

> [!NOTE]
>
> - 請勿在您的程式碼中將 `jQuery.support.cors` 設定為 true。
>
>     ![請勿將 jQuery. 支援 cors 設定為 true](hubs-api-guide-javascript-client/_static/image7.png)
>
>     SignalR 會處理 CORS 的使用。 將 `jQuery.support.cors` 設定為 true 會停用 JSONP，因為它會使 SignalR 假設瀏覽器支援 CORS。
> - 當您連線至 localhost URL 時，Internet Explorer 10 不會將它視為跨網域連線，因此即使您未在伺服器上啟用跨網域連線，應用程式也會在本機使用 IE 10。
> - 如需搭配 Internet Explorer 9 使用跨網域連線的相關資訊，請參閱[此 StackOverflow 執行緒](http://stackoverflow.com/questions/13573397/siganlr-ie9-cross-domain-request-dont-work)。
> - 如需搭配使用跨網域連線與 Chrome 的相關資訊，請參閱[此 StackOverflow 執行緒](http://stackoverflow.com/questions/15467373/signalr-1-0-1-cross-domain-request-cors-with-chrome)。
> - 範例程式碼會使用預設的 "/signalr" URL 來連接到您的 SignalR 服務。 如需有關如何指定不同基底 URL 的詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-Server-/SIGNALR URL](hubs-api-guide-server.md#signalrurl)。

<a id="configureconnection"></a>

## <a name="how-to-configure-the-connection"></a>如何設定連線

建立連接之前，您可以指定查詢字串參數或指定傳輸方法。

<a id="querystring"></a>

### <a name="how-to-specify-query-string-parameters"></a>如何指定查詢字串參數

如果您想要在用戶端連接時將資料傳送到伺服器，您可以將查詢字串參數新增至 connection 物件。 下列範例示範如何在用戶端程式代碼中設定查詢字串參數。

**先設定查詢字串值，再呼叫 start 方法（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample12.js?highlight=1)]

**先設定查詢字串值，再呼叫 start 方法（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample13.js?highlight=2)]

下列範例顯示如何讀取伺服器程式碼中的查詢字串參數。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample14.cs?highlight=5)]

<a id="transport"></a>

### <a name="how-to-specify-the-transport-method"></a>如何指定傳輸方法

在進行連線的過程中，SignalR 用戶端通常會與伺服器協商，以判斷伺服器和用戶端都支援的最佳傳輸。 如果您已經知道您想要使用的傳輸，可以在呼叫 `start` 方法時指定傳輸方法，以略過此協調流程。

**指定傳輸方法的用戶端程式代碼（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample15.js?highlight=1)]

**指定傳輸方法的用戶端程式代碼（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample16.js?highlight=2)]

或者，您也可以指定多個傳輸方法，依您想要讓 SignalR 嘗試它們的順序來進行：

**指定自訂傳輸回退配置的用戶端程式代碼（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample17.js?highlight=1)]

**指定自訂傳輸回退配置的用戶端程式代碼（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample18.js?highlight=2)]

您可以使用下列值來指定傳輸方法：

- Websocket
- "foreverFrame"
- "serverSentEvents"
- "longPolling"

下列範例示範如何找出連接所使用的傳輸方法。

**顯示連接所使用之傳輸方法的用戶端程式代碼（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample19.js?highlight=2)]

**顯示連接所使用之傳輸方法的用戶端程式代碼（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample20.js?highlight=3)]

如需有關如何在伺服器程式碼中檢查傳輸方法的詳細資訊，請參閱[ASP.NET SignalR HUB API 指南-伺服器-如何從內容屬性取得用戶端的相關資訊](hubs-api-guide-server.md#contextproperty)。 如需傳輸和回退的詳細資訊，請參閱[SignalR-傳輸和回退簡介](../getting-started/introduction-to-signalr.md#transports)。

<a id="getproxy"></a>

## <a name="how-to-get-a-proxy-for-a-hub-class"></a>如何取得中樞類別的 proxy

您所建立的每個連線物件都會封裝包含一或多個中樞類別之 SignalR 服務連線的相關資訊。 若要與中樞類別通訊，請使用您自行建立的 proxy 物件（如果您不是使用產生的 proxy），或為您產生。

在用戶端上，proxy 名稱是中樞類別名稱的 camel 大小寫版本。 SignalR 會自動進行此變更，使 JavaScript 程式碼可以符合 JavaScript 慣例。

**伺服器上的中樞類別**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample21.cs?highlight=1)]

**取得針對中樞所產生之用戶端 proxy 的參考**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample22.js?highlight=1)]

**建立中樞類別的用戶端 proxy （不含產生的 proxy）**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample23.cs?highlight=1)]

如果您以 `HubName` 屬性裝飾您的中樞類別，請使用正確的名稱，而不需要變更大小寫。

**伺服器上具有 HubName 屬性的中樞類別**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample24.cs?highlight=1)]

**取得針對中樞所產生之用戶端 proxy 的參考**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample25.js?highlight=1)]

**建立中樞類別的用戶端 proxy （不含產生的 proxy）**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample26.cs?highlight=1)]

<a id="callclient"></a>

## <a name="how-to-define-methods-on-the-client-that-the-server-can-call"></a>如何在用戶端上定義伺服器可以呼叫的方法

若要定義伺服器可以從中樞呼叫的方法，請使用所產生之 proxy 的 `client` 屬性，將事件處理常式新增至中樞 proxy，如果您不是使用所產生的 proxy，請呼叫 `on` 方法。 參數可以是複雜的物件。

請先加入事件處理常式，然後再呼叫 `start` 方法來建立連接。 （如果您想要在呼叫 `start` 方法之後加入事件處理常式，請參閱本檔稍早[如何建立連接](#establishconnection)中的附注，並使用顯示的語法來定義方法，而不使用產生的 proxy）。

方法名稱比對不區分大小寫。 例如，伺服器上的 `Clients.All.addContosoChatMessageToPage` 將會在用戶端上執行 `AddContosoChatMessageToPage`、`addContosoChatMessageToPage`或 `addcontosochatmessagetopage`。

**在用戶端上定義方法（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample27.js?highlight=2)]

**在用戶端上定義方法的替代方式（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample28.js?highlight=1-2)]

**在用戶端上定義方法（不含產生的 proxy，或在呼叫 start 方法之後加入）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample29.js?highlight=3)]

**呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample30.cs?highlight=5)]

下列範例包含當做方法參數的複雜物件。

**在接受複雜物件的用戶端上定義方法（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample31.js?highlight=2-3)]

**在接受複雜物件的用戶端上定義方法（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample32.js?highlight=3-4)]

**定義複雜物件的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample33.cs?highlight=1)]

**使用複雜物件呼叫用戶端方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample34.cs?highlight=3)]

<a id="callserver"></a>

## <a name="how-to-call-server-methods-from-the-client"></a>如何從用戶端呼叫伺服器方法

若要從用戶端呼叫伺服器方法，請在中樞 proxy 上使用所產生之 proxy 或 `invoke` 方法的 `server` 屬性（如果您不是使用所產生的 proxy）。 傳回值或參數可以是複雜的物件。

在中樞上傳入方法名稱的 camel 大小寫版本。 SignalR 會自動進行此變更，使 JavaScript 程式碼可以符合 JavaScript 慣例。

下列範例示範如何呼叫沒有傳回值的伺服器方法，以及如何呼叫具有傳回值的伺服器方法。

**沒有 HubMethodName 屬性的伺服器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample35.cs?highlight=3)]

**定義在參數中傳遞之複雜物件的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample36.cs)]

**叫用伺服器方法的用戶端程式代碼（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample37.js?highlight=1)]

**叫用伺服器方法的用戶端程式代碼（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample38.js?highlight=1)]

如果您以 `HubMethodName` 屬性裝飾中樞方法，請使用該名稱，而不需要變更大小寫。

具有 HubMethodName 屬性的**伺服器方法**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample39.cs?highlight=3)]

**叫用伺服器方法的用戶端程式代碼（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample40.js?highlight=1)]

**叫用伺服器方法的用戶端程式代碼（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample41.js?highlight=1)]

上述範例示範如何呼叫沒有傳回值的伺服器方法。 下列範例示範如何呼叫具有傳回值的伺服器方法。

**具有傳回值之方法的伺服器程式碼**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample42.cs?highlight=3)]

用於傳回值的**Stock 類別**

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample43.cs?highlight=1)]

**叫用伺服器方法的用戶端程式代碼（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample44.js?highlight=2,4-5)]

**叫用伺服器方法的用戶端程式代碼（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample45.js?highlight=2,4-5)]

<a id="connectionlifetime"></a>

## <a name="how-to-handle-connection-lifetime-events"></a>如何處理連接存留期事件

SignalR 提供您可以處理的下列連接存留期事件：

- `starting`：在透過連接傳送任何資料之前引發。
- `received`：在連接上收到任何資料時引發。 提供接收的資料。
- `connectionSlow`：當用戶端偵測到緩慢或經常中斷的連接時引發。
- `reconnecting`：當基礎傳輸開始重新連接時引發。
- `reconnected`：當基礎傳輸已重新連接時引發。
- `stateChanged`：當連接狀態變更時引發。 提供舊狀態和新狀態（連接、連線、重新連接或中斷連接）。
- `disconnected`：當連接中斷連線時引發。

例如，如果您想要在發生可能會造成顯著延遲的連接問題時顯示警告訊息，請處理 `connectionSlow` 事件。

**處理 connectionSlow 事件（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample46.js?highlight=1)]

**處理 connectionSlow 事件（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample47.js?highlight=2)]

如需詳細資訊，請參閱[瞭解和處理 SignalR 中的連接存留期事件](handling-connection-lifetime-events.md)。

<a id="handleerrors"></a>

## <a name="how-to-handle-errors"></a>如何處理錯誤

SignalR JavaScript 用戶端會提供一個 `error` 事件，您可以在其中加入的處理常式。 您也可以使用 fail 方法，針對由伺服器方法調用所產生的錯誤來加入處理常式。

如果您未在伺服器上明確啟用詳細的錯誤訊息，則 SignalR 會在錯誤之後傳回的例外狀況物件包含有關錯誤的最少資訊。 例如，如果 `newContosoChatMessage` 的呼叫失敗，錯誤物件中的錯誤訊息就會包含「`There was an error invoking Hub method 'contosoChatHub.newContosoChatMessage'.`」將詳細的錯誤訊息傳送給生產環境中的用戶端，基於安全性理由，不建議使用此方法，但如果您想要針對疑難排解目的啟用詳細的錯誤訊息，請在伺服器上使用下列程式碼。

[!code-csharp[Main](hubs-api-guide-javascript-client/samples/sample48.cs?highlight=2)]

下列範例顯示如何加入錯誤事件的處理常式。

**新增錯誤處理常式（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample49.js?highlight=1)]

**新增錯誤處理常式（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample50.js?highlight=2)]

下列範例示範如何從方法調用中處理錯誤。

**處理方法調用中的錯誤（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample51.js?highlight=2)]

**處理方法調用中的錯誤（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample52.js?highlight=2)]

如果方法調用失敗，也會引發 `error` 事件，因此 `error` 方法處理常式中和 `.fail` 方法回呼中的程式碼會執行。

<a id="logging"></a>

## <a name="how-to-enable-client-side-logging"></a>如何啟用用戶端記錄

若要在連接上啟用用戶端記錄，請先在連線物件上設定 `logging` 屬性，再呼叫 `start` 方法來建立連接。

**啟用記錄（使用產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample53.js?highlight=1)]

**啟用記錄（不含產生的 proxy）**

[!code-javascript[Main](hubs-api-guide-javascript-client/samples/sample54.js?highlight=2)]

若要查看記錄，請開啟瀏覽器的開發人員工具，並移至 [主控台] 索引標籤。如需示範如何執行這項操作的逐步指示和螢幕擷取畫面的教學課程，請參閱[使用 ASP.NET Signalr 進行伺服器廣播-啟用記錄](../getting-started/tutorial-server-broadcast-with-signalr.md#enable-logging)。
