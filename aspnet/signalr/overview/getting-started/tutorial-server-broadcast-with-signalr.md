---
uid: signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
title: 教學課程：使用 SignalR 2 進行伺服器廣播 |Microsoft Docs
author: tdykstra
description: 本教學課程說明如何建立使用 ASP.NET SignalR 2 來提供伺服器廣播功能的 web 應用程式。
ms.author: bradyg
ms.date: 01/02/2019
ms.topic: tutorial
ms.assetid: 1568247f-60b5-4eca-96e0-e661fbb2b273
msc.legacyurl: /signalr/overview/getting-started/tutorial-server-broadcast-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 14924109fff8db3e537e6bc08b6dc868792ee660
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536600"
---
# <a name="tutorial-server-broadcast-with-signalr-2"></a>教學課程：使用 SignalR 2 進行伺服器廣播

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

本教學課程說明如何建立使用 ASP.NET SignalR 2 來提供伺服器廣播功能的 web 應用程式。 伺服器廣播表示伺服器會啟動傳送到用戶端的通訊。

您在本教學課程中建立的應用程式會模擬股票行情指示器，這是伺服器廣播功能的一般案例。 伺服器會定期更新股票價格，並將更新廣播到所有已連線的用戶端。 在瀏覽器中，[**變更**] 和 [ **%** ] 資料行中的數位和符號會動態變更，以回應來自伺服器的通知。 如果您對相同的 URL 開啟其他瀏覽器，它們會同時顯示相同的資料和相同的資料變更。

![建立 web](tutorial-server-broadcast-with-signalr/_static/image1.png)

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立專案
> * 設定伺服器程式碼
> * 檢查伺服器程式碼
> * 設定用戶端程式代碼
> * 檢查用戶端程式代碼
> * 測試應用程式
> * 啟用記錄

> [!IMPORTANT]
> 如果您不想要逐步執行建立應用程式的步驟，您可以在新的空白 ASP.NET Web 應用程式專案中安裝 SignalR 封裝。 如果您在未執行本教學課程中的步驟的情況下安裝 NuGet 套件，則必須遵循*readme.txt*檔案中的指示。 若要執行封裝，您必須新增 OWIN 啟動類別，以在已安裝的封裝中呼叫 `ConfigureSignalR` 方法。 如果您未新增 OWIN startup 類別，則會收到錯誤。 請參閱本文的[安裝 StockTicker 範例](#install-the-stockticker-sample)一節。

## <a name="prerequisites"></a>Prerequisites

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)，其中包含 **ASP.NET 和 Web 部署**工作負載。

## <a name="create-the-project"></a>建立專案

本節說明如何使用 Visual Studio 2017 來建立空的 ASP.NET Web 應用程式。

1. 在 Visual Studio 中，建立 ASP.NET Web 應用程式。

    ![建立 web](tutorial-server-broadcast-with-signalr/_static/image2.png)

1. 在 [**新增 ASP.NET Web 應用程式-SignalR StockTicker** ] 視窗中，保持選取 [**空白**]，然後選取 **[確定]** 。

## <a name="set-up-the-server-code"></a>設定伺服器程式碼

在本節中，您會設定在伺服器上執行的程式碼。

### <a name="create-the-stock-class"></a>建立 Stock 類別

您一開始會先建立用來儲存和傳送股票資訊的*股票*模型類別。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **類別**]。

1. 將類別命名為*Stock* ，並將其新增至專案。

1. 將*Stock.cs*檔案中的程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample1.cs)]

    您在建立股票時所設定的兩個屬性是 `Symbol` （例如，MSFT for Microsoft）和 `Price`。 其他屬性則取決於您設定 `Price`的方式和時機。 第一次設定 `Price`時，值會傳播至 `DayOpen`。 之後，當您設定 `Price`時，應用程式會根據 `Price` 和 `DayOpen`之間的差異來計算 `Change` 和 `PercentChange` 屬性值。

### <a name="create-the-stocktickerhub-and-stockticker-classes"></a>建立 StockTickerHub 和 StockTicker 類別

您將使用 SignalR 中樞 API 來處理伺服器對用戶端的互動。 衍生自 SignalR `Hub` 類別的 `StockTickerHub` 類別將會處理來自用戶端的接收連接和方法呼叫。 您也需要維護庫存資料，並執行 `Timer` 物件。 `Timer` 物件將定期觸發與用戶端連接無關的價格更新。 您無法將這些函數放在 `Hub` 類別中，因為中樞是暫時性的。 應用程式會為中樞上的每個工作建立一個 `Hub` 類別實例，例如從用戶端到伺服器的連接和呼叫。 因此，保留股票資料、更新價格，以及廣播價格更新的機制，必須在不同的類別中執行。 您會將類別命名為 `StockTicker`。

![從 StockTicker 廣播](tutorial-server-broadcast-with-signalr/_static/image3.png)

您只想要在伺服器上執行 `StockTicker` 類別的一個實例，因此您必須設定從每個 `StockTickerHub` 實例到單一 `StockTicker` 實例的參考。 `StockTicker` 類別必須廣播至用戶端，因為它有存貨資料和觸發程式更新，但 `StockTicker` 不是 `Hub` 類別。 `StockTicker` 類別必須取得 SignalR Hub 連接內容物件的參考。 然後，它可以使用 SignalR 連接內容物件廣播至用戶端。

#### <a name="create-stocktickerhubcs"></a>建立 StockTickerHub.cs

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。

1. 在 **[加入新專案-SignalR**] 中，選取 [**已安裝**] >  **C# Visual** > **Web** > **SignalR** ，然後選取 **[SignalR 中樞類別（v2）** ]。

1. 將類別命名為*StockTickerHub* ，並將它加入至專案。

    此步驟會建立*StockTickerHub.cs*類別檔案。 同時，它會將支援 SignalR 的一組腳本檔案和元件參考加入至專案。

1. 將*StockTickerHub.cs*檔案中的程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample2.cs)]

1. 儲存檔案。

應用程式會使用[中樞](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)類別來定義用戶端可以在伺服器上呼叫的方法。 您要定義一個方法： `GetAllStocks()`。 當用戶端一開始連線到伺服器時，會呼叫此方法來取得所有股票的清單及其目前的價格。 方法可以同步執行並傳回 `IEnumerable<Stock>`，因為它會從記憶體傳回資料。

如果方法必須藉由執行需要等候的專案（例如資料庫查閱或 web 服務呼叫）來取得資料，您會將 `Task<IEnumerable<Stock>>` 指定為傳回值，以啟用非同步處理。 如需詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-Server-何時以非同步方式執行](../guide-to-the-api/hubs-api-guide-server.md#asyncmethods)。

`HubName` 屬性會指定應用程式將如何在用戶端上參考 JavaScript 程式碼中的中樞。 如果您不使用這個屬性，用戶端上的預設名稱會是類別名稱的 camelCase 版本，在此情況下 `stockTickerHub`。

您稍後會在建立 `StockTicker` 類別時看到，應用程式會在其靜態 `Instance` 屬性中建立該類別的單一實例。 無論有多少用戶端連線或中斷連接，`StockTicker` 的單一實例都在記憶體中。 該實例是 `GetAllStocks()` 方法用來傳回目前股票資訊的內容。

#### <a name="create-stocktickercs"></a>建立 StockTicker.cs

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **類別**]。

1. 將類別命名為*StockTicker* ，並將它加入至專案。

1. 將*StockTicker.cs*檔案中的程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample3.cs)]

由於所有線程都會執行相同的 StockTicker 程式碼實例，因此 StockTicker 類別必須是安全線程。

### <a name="examine-the-server-code"></a>檢查伺服器程式碼

如果您檢查伺服器程式碼，它會協助您瞭解應用程式的運作方式。

#### <a name="storing-the-singleton-instance-in-a-static-field"></a>將單一實例儲存在靜態欄位中

程式碼會初始化靜態 `_instance` 欄位，以使用類別的實例來支援 `Instance` 屬性。 因為此函式是私用的，所以它是應用程式可以建立之類別的唯一實例。 應用程式會針對 `_instance` 欄位使用[延遲初始化](/dotnet/framework/performance/lazy-initialization)。 基於效能的考慮，這並不適用。 這是為了確保實例建立是安全線程。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample4.cs)]

每次用戶端連接到伺服器時，在個別執行緒中執行之 StockTickerHub 類別的新實例會從 `StockTicker.Instance` 靜態屬性取得 StockTicker 單一實例，如您稍早在 `StockTickerHub` 類別中所見。

#### <a name="storing-stock-data-in-a-concurrentdictionary"></a>將存貨資料儲存在 ConcurrentDictionary 中

此函式會使用一些範例股票資料來初始化 `_stocks` 集合，而 `GetAllStocks` 會傳回股票。 如您稍早所見，這組股票會由 `StockTickerHub.GetAllStocks`傳回，這是用戶端可以呼叫 `Hub` 類別中的伺服器方法。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample5.cs)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample6.cs)]

股票集合會定義為執行緒安全性的[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)類型。 或者，您可以使用[dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)物件，並在進行變更時明確地鎖定字典。

針對此範例應用程式，您可以將應用程式資料儲存在記憶體中，並在應用程式處置 `StockTicker` 實例時遺失資料。 在實際的應用程式中，您可以使用資料庫之類的後端資料存放區。

#### <a name="periodically-updating-stock-prices"></a>定期更新股票價格

此函式會啟動一個 `Timer` 物件，定期呼叫會隨機更新股票價格的方法。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample7.cs)]

 `Timer` 會呼叫 `UpdateStockPrices`，這會在 state 參數中傳遞 null。 更新價格之前，應用程式會在 `_updateStockPricesLock` 物件上取得鎖定。 程式碼會檢查另一個執行緒是否已更新價格，然後在清單中的每個股票上呼叫 `TryUpdateStockPrice`。 `TryUpdateStockPrice` 方法會決定是否要變更股票價格，以及要變更的數量。 如果股票價格變更，應用程式會呼叫 `BroadcastStockPrice`，以廣播所有已連線用戶端的股票價格變更。

指定為[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx)的 `_updatingStockPrices` 旗標，以確保它是安全線程。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample8.cs)]

在實際的應用程式中，`TryUpdateStockPrice` 方法會呼叫 web 服務來查閱價格。 在此程式碼中，應用程式會使用亂數字產生器來隨機進行變更。

#### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>取得 SignalR 內容，讓 StockTicker 類別可以廣播至用戶端

因為價格變更會在 `StockTicker` 物件中產生，所以必須在所有已連線的用戶端上呼叫 `updateStockPrice` 方法的物件。 在 `Hub` 類別中，您有可呼叫用戶端方法的 API，但 `StockTicker` 不是衍生自 `Hub` 類別，而且沒有任何 `Hub` 物件的參考。 若要廣播至已連線的用戶端，`StockTicker` 類別必須取得 `StockTickerHub` 類別的 SignalR 內容實例，並使用它來呼叫用戶端上的方法。

程式碼會在建立單一類別實例時取得 SignalR 內容的參考，將該參考傳遞給此函式，而此函式會將它放在 `Clients` 屬性中。

當您只想要取得內容一次時，有兩個原因：取得內容是一項昂貴的工作，而且只要取得，就能確保應用程式保留傳送給用戶端的預期訊息順序。

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample9.cs)]

取得內容的 `Clients` 屬性，並將它放在 `StockTickerClient` 屬性中，可讓您撰寫程式碼來呼叫用戶端方法，其外觀與在 `Hub` 類別中相同。 比方說，若要廣播至所有用戶端，您可以 `Clients.All.updateStockPrice(stock)`寫入。

您在 `BroadcastStockPrice` 中呼叫的 `updateStockPrice` 方法尚不存在。 稍後當您撰寫在用戶端上執行的程式碼時，您將會新增它。 您可以參考這裡的 `updateStockPrice`，因為 `Clients.All` 是動態的，這表示應用程式會在執行時間評估運算式。 當這個方法呼叫執行時，SignalR 會將方法名稱和參數值傳送給用戶端，如果用戶端具有名為 `updateStockPrice`的方法，應用程式將會呼叫該方法，並將參數值傳遞給它。

`Clients.All` 表示傳送至所有用戶端。 SignalR 提供您其他選項來指定要傳送至哪些用戶端或用戶端群組。 如需詳細資訊，請參閱[HubConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。

### <a name="register-the-signalr-route"></a>註冊 SignalR 路由

伺服器必須知道要攔截並直接 SignalR 的 URL。 若要這麼做，請新增 OWIN 啟動類別：

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。

1. 在 **加入新專案-SignalR**  中，選取 **已安裝** > **Visual C#**  > **Web** ，然後選取  **OWIN 啟動類別**。

1. 將類別命名為*Startup* ，然後選取 **[確定]** 。

1. 使用下列程式碼取代*Startup.cs*檔案中的預設程式碼：

    [!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample10.cs)]

您現在已完成伺服器程式碼的設定。 在下一節中，您將設定用戶端。

## <a name="set-up-the-client-code"></a>設定用戶端程式代碼

在本節中，您會設定在用戶端上執行的程式碼。

### <a name="create-the-html-page-and-javascript-file"></a>建立 HTML 網頁和 JavaScript 檔案

HTML 網頁會顯示資料，而 JavaScript 檔案會組織資料。

#### <a name="create-stocktickerhtml"></a>建立 StockTicker

首先，您要加入 HTML 用戶端。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **HTML 網頁**]。

1. 將檔案命名為*StockTicker* ，然後選取 **[確定]** 。

1. 將*StockTicker*中的預設程式碼取代為下列程式碼：

    [!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample11.html?highlight=40-43)]

    HTML 會建立具有五個數據行的資料表、一個標題列，以及一個橫跨所有五個數據行的單一儲存格。 資料列顯示「正在載入 ...」當應用程式啟動時，很快就會發生。 JavaScript 程式碼將會移除該資料列，並加入其位置列，其中包含從伺服器抓取的股票資料。

    腳本標記會指定：

    * JQuery 腳本檔案。

    * SignalR 核心腳本檔案。

    * SignalR proxy 腳本檔案。

    * 稍後將建立的 StockTicker 腳本檔案。

    應用程式會動態產生 SignalR proxy 腳本檔案。 它會指定 "/signalr/hubs" URL，並為中樞類別上的方法定義 proxy 方法，在此案例中為 `StockTickerHub.GetAllStocks`。 如果您想要的話，也可以使用[SignalR 公用程式](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)，以手動方式產生此 JavaScript 檔案。 別忘了在 `MapHubs` 方法呼叫中停用動態檔案建立。

1. 在**方案總管**中，展開 [**腳本**]。

    JQuery 和 SignalR 的腳本程式庫會顯示在專案中。

    > [!IMPORTANT]
    > 封裝管理員將會安裝較新版本的 SignalR 腳本。

1. 更新程式碼區塊中的腳本參考，以對應至專案中的腳本檔案版本。

1. 在**方案總管**中，以滑鼠右鍵按一下 [ *StockTicker*]，然後選取 [**設定為起始頁**]。

#### <a name="create-stocktickerjs"></a>建立 StockTicker

現在建立 JavaScript 檔案。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **JavaScript**檔案]。

1. 將檔案命名為*StockTicker* ，然後選取 **[確定]** 。

1. 將下列程式碼新增至*StockTicker*檔案：

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample12.js)]

### <a name="examine-the-client-code"></a>檢查用戶端程式代碼

如果您檢查用戶端程式代碼，它會協助您瞭解用戶端程式代碼如何與伺服器程式碼互動，以讓應用程式正常執行。

#### <a name="starting-the-connection"></a>啟動連接

`$.connection` 是指 SignalR proxy。 程式碼會取得 `StockTickerHub` 類別之 proxy 的參考，並將它放在 `ticker` 變數中。 Proxy 名稱是 `HubName` 屬性所設定的名稱：

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample13.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample14.cs)]

定義所有變數和函數之後，檔案中的最後一行程式碼會藉由呼叫 SignalR `start` 函式來初始化 SignalR 連接。 `start` 函式會以非同步方式執行，並傳回[JQuery 延遲物件](http://api.jquery.com/category/deferred-object/)。 您可以呼叫完成函式，以指定當應用程式完成非同步動作時所要呼叫的函式。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample15.js)]

#### <a name="getting-all-the-stocks"></a>取得所有股票

`init` 函式會在伺服器上呼叫 `getAllStocks` 函數，並使用伺服器傳回的資訊來更新庫存資料表。 請注意，根據預設，您必須在用戶端上使用 camelCasing，即使伺服器上的方法名稱是 pascal 大小寫也一樣。 CamelCasing 規則僅適用于方法，而不是物件。 例如，您指的是 `stock.Symbol` 和 `stock.Price`，而不是 `stock.symbol` 或 `stock.price`。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample16.js)]

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample17.cs)]

在 `init` 方法中，應用程式會藉由呼叫 `formatStock` 來格式化 `stock` 物件的屬性，然後呼叫 `supplant` 將 `rowTemplate` 變數中的預留位置取代為 `stock` 物件屬性值，為每個從伺服器接收的股票物件建立 HTML。 產生的 HTML 會附加至股票資料表。

> [!NOTE]
> 您可以呼叫 `init`，方法是將它傳入做為 `callback` 函式，該函式會在非同步 `start` 函數完成後執行。 如果您在呼叫 `start`之後，以個別的 JavaScript 語句來呼叫 `init`，此函式會失敗，因為它會立即執行，而不會等候啟動函數完成建立連接。 在此情況下，`init` 函式會先嘗試呼叫 `getAllStocks` 函式，應用程式才會建立伺服器連接。

#### <a name="getting-updated-stock-prices"></a>取得更新的股票價格

當伺服器變更股票價格時，它會在已連線的用戶端上呼叫 `updateStockPrice`。 應用程式會將函式新增至 `stockTicker` proxy 的用戶端屬性，使其可供從伺服器呼叫。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample18.js)]

`updateStockPrice` 函數會依照 `init` 函數中的相同方式，將從伺服器接收的股票物件格式化為資料表資料列。 它不會將資料列附加至資料表，而是在資料表中尋找庫存的目前資料列，並將該資料列取代為新的資料列。

## <a name="test-the-application"></a>測試應用程式

您可以測試應用程式以確定其運作正常。 您會看到所有的瀏覽器視窗都會顯示股票價格變動的即時股票資料表。

1. 在工具列中，開啟 [**腳本調試**程式]，然後選取 [播放] 按鈕，以在 [偵測模式] 中執行應用程式。

    ![使用者開啟偵錯模式和選取 [播放] 的螢幕擷取畫面。](tutorial-server-broadcast-with-signalr/_static/image4.png)

    瀏覽器視窗隨即開啟，並顯示 [**即時股票] 資料表**。 Stock 資料表一開始會顯示「正在載入 ...」一行之後，應用程式就會顯示初始股票資料，然後再開始變更股票價格。

1. 從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到網址列中。

    初始股票顯示與第一個瀏覽器相同，而且會同時進行變更。

1. 關閉所有瀏覽器，開啟新的瀏覽器，然後移至相同的 URL。

    StockTicker singleton 物件會繼續在伺服器中執行。 [ **Live Stock] 資料表**顯示股票已繼續變更。 您看不到具有零變更圖形的初始資料表。

1. 關閉瀏覽器。

## <a name="enable-logging"></a>啟用記錄

SignalR 具有內建的記錄功能，可讓您在用戶端上啟用以協助進行疑難排解。 在本節中，您會啟用記錄功能，並查看說明記錄如何告訴您 SignalR 使用下列哪一個傳輸方法的範例：

* [Websocket](http://en.wikipedia.org/wiki/WebSocket)（由 IIS 8 和目前的瀏覽器支援）。

* [伺服器傳送的事件](http://en.wikipedia.org/wiki/Server-sent_events)，由 Internet Explorer 以外的瀏覽器所支援。

* Internet Explorer 所支援的[永久框架](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。

* 所有瀏覽器都支援[Ajax 長輪詢](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)。

針對任何指定的連接，SignalR 會選擇伺服器和用戶端支援的最佳傳輸方法。

1. 開啟*StockTicker*。

1. 新增這個反白顯示的程式程式碼，以便在檔案結尾初始化連接的程式碼之前立即啟用記錄：

    [!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample19.js?highlight=2)]

1. 按 **F5** 執行專案。

1. 開啟瀏覽器的 [開發人員工具] 視窗，然後選取主控台以查看記錄。 您可能必須重新整理頁面，才能查看 SignalR 的記錄，以協調新連接的傳輸方法。

    * 如果您是在 Windows 8 （IIS 8）上執行 Internet Explorer 10，傳輸方法是**websocket**。

    * 如果您是在 Windows 7 （IIS 7.5）上執行 Internet Explorer 10，則傳輸方法是**iframe**。

    * 如果您是在 Windows 8 （IIS 8）上執行 Firefox 19，傳輸方法是**websocket**。

        > [!TIP]
        > 在 Firefox 中，安裝 Firebug 增益集以取得主控台視窗。

    * 如果您是在 Windows 7 （IIS 7.5）上執行 Firefox 19，傳輸方法就是**伺服器傳送**的事件。

## <a name="install-the-stockticker-sample"></a>安裝 StockTicker 範例

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample)會安裝 StockTicker 應用程式。 NuGet 套件包含的功能比您從頭建立的簡化版本還多。 在本教學課程的這一節中，您會安裝 NuGet 套件，並檢查新功能及其執行的程式碼。

> [!IMPORTANT]
> 如果您在未執行本教學課程的先前步驟的情況下安裝套件，您必須將 OWIN 啟動類別新增至您的專案。 此 NuGet 套件的 readme.txt 檔案會說明此步驟。

### <a name="install-the-signalrsample-nuget-package"></a>安裝 SignalR NuGet 套件

1. 在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取 [管理 NuGet 套件]。

1. 在**NuGet 套件管理員中： SignalR. StockTicker**，選取 **[流覽]** 。

1. 在 [**套件來源**] 中，選取 [ **nuget.org**]。

1. 在搜尋方塊中輸入*SignalR* ，然後選取 [ **SignalR. 範例** > **安裝**]。

1. 在**方案總管**中，展開 [ *SignalR* ] 資料夾。

    安裝 SignalR 套件時，會建立資料夾及其內容。

1. 在 [ *SignalR* ] 資料夾中，以滑鼠右鍵按一下 [ *StockTicker*]，然後選取 [**設定為起始頁**]。

    > [!NOTE]
    > 安裝 SignalR 時，NuGet 套件可能會變更您在 [*腳本*] 資料夾中的 jQuery 版本。 封裝安裝在*SignalR*中的新*StockTicker*檔案會與封裝所安裝的 jQuery 版本同步，但如果您想要再次執行原始的*StockTicker .html*檔案，您可能必須先更新腳本標記中的 jquery 參考。

### <a name="run-the-application"></a>執行應用程式

 您在第一個應用程式中看到的資料表具有有用的功能。 「全庫存指示器」應用程式會顯示新功能：顯示股票資料的水準滾動視窗，以及變更色彩隨著上升和落的股票。

1. 按下 **F5** 即可執行應用程式。

     當您第一次執行應用程式時，「市場」會是「已關閉」，而您會看到靜態資料表和不會滾動的「捲軸」視窗。

1. 選取 [**開放市場**]。

    ![即時報價的螢幕擷取畫面。](tutorial-server-broadcast-with-signalr/_static/image5.png)

    * [**即時股票行情**] 方塊會開始水準滾動，而伺服器會開始定期廣播股價變更。

    * 每次股票價格變更時，應用程式都會更新**即時股票資料表**和**即時股票行情**指示器。

    * 當股票價格變更為正面時，應用程式會以綠色背景顯示股票。

    * 當變更為負值時，應用程式會以紅色背景顯示股票。

1. 選取 [**關閉市場**]。

    * 資料表更新會停止。

    * 此指示器會停止滾動。

1. 選取 [**重設**]。

    * 所有的存貨資料都會重設。

    * 應用程式會在價格變更開始前，先還原初始狀態。

1. 從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到網址列中。

1. 您會看到相同的資料在每個瀏覽器中同時動態更新。

1. 當您選取任何控制項時，所有瀏覽器會同時以相同的方式回應。

### <a name="live-stock-ticker-display"></a>即時股票行情顯示

**即時股票行情**指示器顯示是在 `<div>` 專案中，以 CSS 樣式格式化成單行的未排序清單。 應用程式會使用與資料表相同的方式來初始化和更新「滾動框」：藉由取代 `<li>` 範本字串中的預留位置，並動態地將 `<li>` 元素新增至 `<ul>` 元素。 應用程式包含使用 jQuery `animate` 函式的滾動，來改變 `<div>`內未排序清單的左邊界。

#### <a name="signalrsample-stocktickerhtml"></a>SignalR. Sample StockTicker .html

股票行情指示器 HTML 程式碼：

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample20.html)]

#### <a name="signalrsample-stocktickercss"></a>SignalR. Sample StockTicker .css

股票行情指示器 CSS 程式碼：

[!code-html[Main](tutorial-server-broadcast-with-signalr/samples/sample21.html)]

#### <a name="signalrsample-signalrstocktickerjs"></a>SignalR. Sample SignalR. StockTicker .js

使其滾動的 jQuery 程式碼：

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample22.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>用戶端可以呼叫之伺服器上的其他方法

為了增加應用程式的彈性，應用程式可以呼叫其他方法。

#### <a name="signalrsample-stocktickerhubcs"></a>SignalR. Sample StockTickerHub.cs

`StockTickerHub` 類別定義了用戶端可以呼叫的四個額外方法：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample23.cs)]

應用程式會呼叫 `OpenMarket`、`CloseMarket`和 `Reset`，以回應頁面頂端的按鈕。 它們會示範一個用戶端的模式，觸發狀態變更立即傳播至所有用戶端。 這些方法中的每一個都會呼叫 `StockTicker` 類別中的方法，這會導致市場狀態變更，然後廣播新的狀態。

#### <a name="signalrsample-stocktickercs"></a>SignalR. Sample StockTicker.cs

在 `StockTicker` 類別中，應用程式會以傳回 `MarketState` 列舉值的 `MarketState` 屬性，來維護市場的狀態：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample24.cs)]

每個變更市場狀態的方法都會在鎖定區塊內這麼做，因為 `StockTicker` 類別必須是安全線程：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample25.cs)]

為確保此程式碼為安全線程，`_marketState` 欄位會支援指定 `volatile`的 `MarketState` 屬性：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample26.cs)]

`BroadcastMarketStateChange` 和 `BroadcastMarketReset` 方法與您已見過的 BroadcastStockPrice 方法類似，不同之處在于它們會呼叫用戶端上定義的不同方法：

[!code-csharp[Main](tutorial-server-broadcast-with-signalr/samples/sample27.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>伺服器可以呼叫之用戶端上的其他函數

`updateStockPrice` 函式現在會同時處理資料表和捲軸顯示，並使用 `jQuery.Color` 來閃爍紅色和綠色色彩。

*SignalR. StockTicker*中的新函式會根據市場狀態來啟用和停用按鈕。 他們也會停止或啟動**即時股票**指示器水準滾動。 由於有許多函式會新增至 `ticker.client`，因此應用程式會使用[jQuery extend](http://api.jquery.com/jQuery.extend/)函式來新增這些函數。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample28.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>建立連線後的其他用戶端設定

用戶端建立連線之後，還有一些額外的工作要執行：

* 找出市場是否已開啟或已關閉，以呼叫適當的 `marketOpened` 或 `marketClosed` 函數。

* 將伺服器方法呼叫附加至按鈕。

[!code-javascript[Main](tutorial-server-broadcast-with-signalr/samples/sample29.js)]

直到應用程式建立連線之後，伺服器方法才會連接到按鈕。 這是為了讓程式碼無法在可用之前呼叫伺服器方法。

## <a name="additional-resources"></a>其他資源

在本教學課程中，您已瞭解如何設計 SignalR 應用程式，以將訊息從伺服器廣播到所有已連線的用戶端。 現在您可以定期廣播訊息，並回應來自任何用戶端的通知。 您可以使用多執行緒單一實例的概念，在多玩家的線上遊戲案例中維護伺服器狀態。 如需範例，請參閱以[SignalR 為基礎的 ShootR 遊戲](https://github.com/NTaylorMullen/ShootR)。

如需顯示點對點通訊案例的教學課程，請參閱[使用 SignalR](introduction-to-signalr.md)和[使用 SignalR 進行即時更新](tutorial-high-frequency-realtime-with-signalr.md)的消費者入門。

如需 SignalR 的詳細資訊，請參閱下列資源：

* [ASP.NET SignalR](../../index.md)
* [SignalR 專案](http://signalr.net/)
* [SignalR GitHub 和範例](https://github.com/SignalR/SignalR)
* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立專案
> * 設定伺服器程式碼
> * 檢查伺服器程式碼
> * 設定用戶端程式代碼
> * 檢查用戶端程式代碼
> * 測試應用程式
> * 啟用記錄

前進到下一篇文章，以瞭解如何建立使用 ASP.NET SignalR 2 的即時 web 應用程式。
> [!div class="nextstepaction"]
> [使用 SignalR 建立即時 web 應用程式](real-time-web-applications-with-signalr.md)
