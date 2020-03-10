---
uid: signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
title: 教學課程：使用 ASP.NET SignalR 1.x 的伺服器廣播 |Microsoft Docs
author: bradygaster
description: 本教學課程示範如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供伺服器廣播功能。 伺服器廣播表示 communic 。
ms.author: bradyg
ms.date: 04/10/2013
ms.assetid: ab7b2554-956a-4f6d-b2a0-4ae0c62e8580
msc.legacyurl: /signalr/overview/older-versions/tutorial-server-broadcast-with-aspnet-signalr
msc.type: authoredcontent
ms.openlocfilehash: 68908be34f6b010e512677fe5f5e31bfdefab592
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579405"
---
# <a name="tutorial-server-broadcast-with-aspnet-signalr-1x"></a>教學課程：使用 ASP.NET SignalR 1.x 的伺服器廣播

由一[Fletcher](https://github.com/pfletcher)， [Tom 作者: dykstra](https://github.com/tdykstra)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教學課程示範如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供伺服器廣播功能。 伺服器廣播表示傳送至用戶端的通訊是由伺服器起始。 此案例所需的程式設計方法與對等案例（例如聊天應用程式）不同，而傳送到用戶端的通訊是由一或多個用戶端起始。
> 
> 您在本教學課程中建立的應用程式會模擬股票行情指示器，這是伺服器廣播功能的一般案例。
> 
> 歡迎使用教學課程的批註。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。

## <a name="overview"></a>概觀

[SignalR](http://nuget.org/packages/microsoft.aspnet.signalr.sample) NuGet 套件會在 Visual Studio 專案中安裝範例模擬股票行情指示器應用程式。 在本教學課程的第一個部分中，您將從頭開始建立該應用程式的簡化版本。 在本教學課程的其餘部分中，您將會安裝 NuGet 套件，並檢查它所建立的其他功能和程式碼。

股票行情指示器應用程式是一種即時應用程式的代表，您想要定期「推送」或「廣播」通知，從伺服器到所有連線的用戶端。

您將在本教學課程的第一個部分中建立的應用程式會顯示包含股票資料的方格。

![StockTicker 初始版本](tutorial-server-broadcast-with-aspnet-signalr/_static/image1.png)

伺服器會定期隨機更新股票價格，並將更新推送至所有已連線的用戶端。 在瀏覽器中，[**變更**] 和 [ **%** ] 資料行中的數位和符號會動態變更，以回應來自伺服器的通知。 如果您對相同的 URL 開啟其他瀏覽器，它們會同時顯示相同的資料和相同的資料變更。

本教學課程包含下列各節：

- [必要條件](#prerequisites)
- [建立專案](#createproject)
- [新增 SignalR NuGet 套件](#nugetpackages)
- [設定伺服器程式碼](#server)
- [設定用戶端程式代碼](#client)
- [測試應用程式](#test)
- [啟用記錄](#enablelogging)
- [安裝和查看完整的 StockTicker 範例](#fullsample)
- [後續步驟](#nextsteps)

> [!NOTE]
> 如果您不想要逐步執行建立應用程式的步驟，您可以在新的**空白 ASP.NET Web 應用程式**專案中安裝 SignalR 套件，並閱讀這些步驟來取得程式碼的說明。 本教學課程的第一個部分涵蓋 SignalR 的子集，第二個部分則說明 SignalR 中其他功能的主要功能。

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Prerequisites

開始之前，請確定您已在電腦上安裝 Visual Studio 2012 或 2010 SP1。 如果您沒有 Visual Studio，請參閱[ASP.NET 下載](https://www.asp.net/downloads)以取得免費的 Visual Studio 2012 Express for Web。

如果您有 Visual Studio 2010，請確定已安裝[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 。

<a id="createproject"></a>

## <a name="create-the-project"></a>建立專案

1. 從 [檔案] 功能表，按一下 [新增專案]。
2. 在 [**新增專案**] 對話方塊中， **C#** 展開 [**範本**]，然後選取 [ **Web**]。
3. 選取 [ **ASP.NET 空白 Web 應用程式**] 範本，將專案命名為*SignalR StockTicker*，然後按一下 **[確定]** 。

    ![新增專案對話方塊](tutorial-server-broadcast-with-aspnet-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-nuget-packages"></a>新增 SignalR NuGet 套件

### <a name="add-the-signalr-and-jquery-nuget-packages"></a>新增 SignalR 和 JQuery NuGet 套件

您可以藉由安裝 NuGet 套件，將 SignalR 功能新增至專案。

1. 按一下 [**工具] |NuGet 套件管理員 |套件管理員主控台**。
2. 在 [套件管理員] 中輸入下列命令。

    [!code-powershell[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample1.ps1)]

    SignalR 套件會安裝一些其他 NuGet 套件做為相依性。 當安裝完成時，您會擁有在 ASP.NET 應用程式中使用 SignalR 所需的所有伺服器和用戶端元件。

<a id="server"></a>

## <a name="set-up-the-server-code"></a>設定伺服器程式碼

在本節中，您會設定在伺服器上執行的程式碼。

### <a name="create-the-stock-class"></a>建立 Stock 類別

您一開始會先建立用來儲存和傳送股票資訊的股票模型類別。

1. 在專案資料夾中建立新的類別檔案，將其命名為*Stock.cs*，然後將範本程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample2.cs)]

    您在建立股票時所設定的兩個屬性是符號（例如，MSFT for Microsoft）和價格。 其他屬性則取決於您設定價格的方式和時間。 第一次設定價格時，值會傳播至 DayOpen。 後續設定價格時，會根據 Price 和 DayOpen 之間的差異來計算變更和 PercentChange 屬性值。

### <a name="create-the-stockticker-and-stocktickerhub-classes"></a>建立 StockTicker 和 StockTickerHub 類別

您將使用 SignalR 中樞 API 來處理伺服器對用戶端的互動。 衍生自 SignalR 中樞類別的 StockTickerHub 類別將會處理來自用戶端的接收連接和方法呼叫。 您也需要維護庫存資料，並執行計時器物件，以定期觸發價格更新，而不受用戶端連線影響。 因為中樞實例是暫時性的，所以您無法將這些函數放在中樞類別中。 會針對中樞上的每個作業建立中樞類別實例，例如從用戶端到伺服器的連接和呼叫。 因此，保留股票資料、更新價格，以及廣播價格更新的機制，必須在不同的類別中執行，您將會將其命名為 StockTicker。

![從 StockTicker 廣播](tutorial-server-broadcast-with-aspnet-signalr/_static/image4.png)

您只想要在伺服器上執行一個 StockTicker 類別實例，因此您必須設定每個 StockTickerHub 實例到單一 StockTicker 實例的參考。 StockTicker 類別必須能夠廣播到用戶端，因為它有存貨資料和觸發程式更新，但 StockTicker 不是中樞類別。 因此，StockTicker 類別必須取得 SignalR Hub 連接內容物件的參考。 然後，它可以使用 SignalR 連接內容物件廣播至用戶端。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**加入新專案**]。
2. 如果您有[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=279941)的 Visual Studio 2012，請按一下 [**視覺效果C#**  ] 底下的 [ **Web** ]，然後選取 [ **SignalR 中樞類別**] 專案範本。 否則，請選取 [**類別**] 範本。
3. 將新類別命名為*StockTickerHub.cs*，**然後按一下 [新增]** 。

    ![新增 StockTickerHub.cs](tutorial-server-broadcast-with-aspnet-signalr/_static/image5.png)
4. 使用下列程式碼取代範本程式碼：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample3.cs)]

    [中樞](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hub(v=vs.111).aspx)類別是用來定義用戶端可以在伺服器上呼叫的方法。 您要定義一個方法： `GetAllStocks()`。 當用戶端一開始連線到伺服器時，會呼叫此方法來取得所有股票的清單及其目前的價格。 方法可以同步執行並傳回 `IEnumerable<Stock>`，因為它會從記憶體傳回資料。 如果方法必須藉由執行需要等候的專案（例如資料庫查閱或 web 服務呼叫）來取得資料，您會將 `Task<IEnumerable<Stock>>` 指定為傳回值，以啟用非同步處理。 如需詳細資訊，請參閱[ASP.NET SignalR HUB API Guide-Server-何時以非同步方式執行](index.md)。

    HubName 屬性會指定如何在用戶端上的 JavaScript 程式碼中參考中樞。 如果您不使用這個屬性，則用戶端上的預設名稱是類別名稱的 camel 大小寫版本，在此案例中會是 stockTickerHub。

    您稍後會在建立 StockTicker 類別時看到，會在其靜態實例屬性中建立該類別的單一實例。 不論有多少用戶端連線或中斷連接，StockTicker 的單一實例都會保留在記憶體中，而該實例就是 GetAllStocks 方法用來傳回目前股票資訊的情況。
5. 在專案資料夾中建立新的類別檔案，將其命名為*StockTicker.cs*，然後將範本程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample4.cs)]

    因為多個執行緒將會執行相同的 StockTicker 程式碼實例，所以 StockTicker 類別必須是 threadsafe。

    ### <a name="storing-the-singleton-instance-in-a-static-field"></a>將單一實例儲存在靜態欄位中

    此程式碼會初始化靜態 \_實例欄位，以使用類別的實例來支援實例屬性，而且這是唯一可以建立之類別的實例，因為此函式會標示為私用。 [延遲初始化](https://msdn.microsoft.com/library/dd997286.aspx)會用於 \_實例欄位，而不是基於效能考慮，但可確保實例建立是 threadsafe 的。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample5.cs)]

    每次用戶端連接到伺服器時，在個別執行緒中執行之 StockTickerHub 類別的新實例會從 StockTicker 靜態屬性取得 StockTicker 單一實例，如您稍早在 StockTickerHub 類別中所見。

    ### <a name="storing-stock-data-in-a-concurrentdictionary"></a>將存貨資料儲存在 ConcurrentDictionary 中

    此函式會使用一些範例股票資料來初始化 \_的股票集合，而 GetAllStocks 會傳回股票。 如您稍早所見，這組股票會轉而由 StockTickerHub 傳回。 GetAllStocks，這是用戶端可以呼叫的中樞類別中的伺服器方法。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample6.cs)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample7.cs)]

    股票集合會定義為執行緒安全性的[ConcurrentDictionary](https://msdn.microsoft.com/library/dd287191.aspx)類型。 或者，您可以使用[dictionary](https://msdn.microsoft.com/library/xfhwa508.aspx)物件，並在進行變更時明確地鎖定字典。

    針對此範例應用程式，您可以將應用程式資料儲存在記憶體中，並在處置 StockTicker 實例時遺失資料。 在實際的應用程式中，您會使用後端資料存放區，例如資料庫。

    ### <a name="periodically-updating-stock-prices"></a>定期更新股票價格

    此函式會啟動計時器物件，定期呼叫會隨機更新股票價格的方法。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample8.cs)]

    UpdateStockPrices 是由計時器呼叫，它會在 state 參數中傳遞 null。 更新價格之前，會對 \_updateStockPricesLock 物件採取鎖定。 程式碼會檢查另一個執行緒是否已更新價格，然後在清單中的每個股票上呼叫 TryUpdateStockPrice。 TryUpdateStockPrice 方法會決定是否要變更股票價格，以及要變更的數量。 如果股票價格已變更，則會呼叫 BroadcastStockPrice 以將股票價格變更廣播至所有已連線的用戶端。

    \_updatingStockPrices 旗標會標示為[volatile](https://msdn.microsoft.com/library/x13ttww7.aspx) ，以確保它的存取權是 threadsafe。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample9.cs)]

    在實際的應用程式中，TryUpdateStockPrice 方法會呼叫 web 服務來查閱價格;在此程式碼中，它會使用亂數字產生器來隨機進行變更。

    ### <a name="getting-the-signalr-context-so-that-the-stockticker-class-can-broadcast-to-clients"></a>取得 SignalR 內容，讓 StockTicker 類別可以廣播至用戶端

    因為價格變更的來源是 StockTicker 物件，所以這是需要在所有已連線的用戶端上呼叫 updateStockPrice 方法的物件。 在中樞類別中，您有可呼叫用戶端方法的 API，但 StockTicker 不是衍生自中樞類別，而且沒有任何中樞物件的參考。 因此，為了廣播至已連線的用戶端，StockTicker 類別必須取得 StockTickerHub 類別的 SignalR 內容實例，並使用它來呼叫用戶端上的方法。

    程式碼會在建立單一類別實例時取得 SignalR 內容的參考，將該參考傳遞給此函式，而此函式會將它放在用戶端屬性中。

    當您只想要取得內容一次時，有兩個原因：取得內容是昂貴的作業，而取得它一次可確保傳送至用戶端之訊息的預期順序會保留下來。

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample10.cs)]

    取得內容的用戶端屬性並將它放在 StockTickerClient 屬性中，可讓您撰寫程式碼來呼叫用戶端方法，其外觀與在中樞類別中相同。 比方說，若要廣播至所有用戶端，您可以撰寫用戶端。 updateStockPrice （股票）。

    您在 BroadcastStockPrice 中呼叫的 updateStockPrice 方法尚不存在;稍後當您撰寫在用戶端上執行的程式碼時，您將會新增它。 您可以參考這裡的 updateStockPrice，因為用戶端。全部都是動態的，這表示運算式會在執行時間進行評估。 當這個方法呼叫執行時，SignalR 會將方法名稱和參數值傳送給用戶端，如果用戶端具有名為 updateStockPrice 的方法，就會呼叫該方法，並將參數值傳遞給它。

    用戶端。所有方法皆會傳送至所有用戶端。 SignalR 提供您其他選項來指定要傳送至哪些用戶端或用戶端群組。 如需詳細資訊，請參閱[HubConnectionCoNtext](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubs.hubconnectioncontext(v=vs.111).aspx)。

### <a name="register-the-signalr-route"></a>註冊 SignalR 路由

伺服器必須知道要攔截並直接 SignalR 的 URL。 若要這麼做，請將一些程式碼加入至*global.asax*檔案。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**加入新專案**]。
2. 選取 [**全域應用程式類別**] 專案範本，然後按一下 [**新增**]。

    ![加入 global.asax](tutorial-server-broadcast-with-aspnet-signalr/_static/image6.png)
3. 將 SignalR 路由註冊碼新增至應用程式\_Start 方法：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample11.cs)]

    根據預設，所有 SignalR 流量的基底 URL 為 "/signalr"，而 "/signalr/hubs" 是用來抓取動態產生的 JavaScript 檔案，該檔案會針對您應用程式中的所有中樞定義 proxy。 MapHubs 方法包含多載，可讓您在[HubConfiguration](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.hubconfiguration(v=vs.111).aspx)類別的實例中指定不同的基底 URL 和特定的 SignalR 選項。
4. 在檔案頂端新增 using 語句：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample12.cs)]
5. 儲存並關閉*global.asax*檔案，並建立專案。

您現在已完成伺服器程式碼的設定。 在下一節中，您將設定用戶端。

<a id="client"></a>

## <a name="set-up-the-client-code"></a>設定用戶端程式代碼

1. 在專案資料夾中建立新的 HTML 檔案，並將它命名為*StockTicker*。
2. 使用下列程式碼取代範本程式碼：

    [!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample13.html)]

    HTML 會建立包含5個數據行的資料表、一個標題列，以及一個橫跨所有5個數據行的單一儲存格。 資料列會顯示「正在載入 ...」只有在應用程式啟動時，才會立即顯示和。 JavaScript 程式碼將會移除該資料列，並加入其位置列，其中包含從伺服器抓取的股票資料。

    腳本標記會指定 jQuery 腳本檔案、SignalR core 腳本檔案、SignalR proxy 腳本檔案，以及稍後將建立的 StockTicker 腳本檔案。 SignalR proxy 腳本檔案（指定 "/signalr/hubs" URL）是以動態方式產生，並定義中樞類別上方法的 proxy 方法，在此案例中為 StockTickerHub. GetAllStocks。 如果您想要的話，也可以使用[SignalR 公用程式](http://nuget.org/packages/Microsoft.AspNet.SignalR.Utils/)手動產生此 JavaScript 檔案，並在 MapHubs 方法呼叫中停用動態檔案建立。
3. > [!IMPORTANT]
   > 請確定*StockTicker*中的 JavaScript 檔案參考是正確的。 也就是說，請確定腳本卷*標*（在範例中為1.8.2）中的 jquery 版本與專案 script 資料夾中的 jquery 版本相同，並確定腳本標記中的 SignalR 版本與專案*腳本*資料夾中的 SignalR 版本相同。 必要時，請變更腳本標記中的檔案名。
4. 在**方案總管**中，以滑鼠右鍵按一下 [ *StockTicker*]，然後按一下 [**設定為起始頁**]。
5. 在專案資料夾中建立新的 JavaScript 檔案，並將它命名為*StockTicker*。
6. 使用下列程式碼取代範本程式碼：

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample14.js)]

    $. connection 指的是 SignalR proxy。 程式碼會取得 StockTickerHub 類別之 proxy 的參考，並將它放在「指示器」變數中。 Proxy 名稱是由 [HubName] 屬性所設定的名稱：

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample15.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample16.cs)]

    定義所有變數和函式之後，檔案中的最後一行程式碼會藉由呼叫 SignalR start 函式來初始化 SignalR 連接。 Start 函式會以非同步方式執行並傳回[JQuery 延遲物件](http://api.jquery.com/category/deferred-object/)，這表示您可以呼叫 completed 函式，以指定在非同步作業完成時要呼叫的函式。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample17.js)]

    Init 函數會呼叫伺服器上的 getAllStocks 函數，並使用伺服器傳回的資訊來更新庫存資料表。 請注意，根據預設，您必須在用戶端上使用 camel 大小寫，但在伺服器上，方法名稱是 pascal 大小寫。 Camel 大小寫規則僅適用于方法，而不是物件。 例如，您指的是股票。符號和股票。價格，而不是股票. 符號或股票。價格。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample18.js)]

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample19.cs)]

    如果您想要在用戶端上使用 pascal 大小寫，或如果您想要使用完全不同的方法名稱，您可以使用 HubMethodName 屬性來裝飾中樞方法，方法與使用 HubName 屬性裝飾中樞類別本身的方式相同。

    在 init 方法中，會為從伺服器接收的每個股票物件建立一個資料表資料列的 HTML，方法是呼叫 formatStock 來格式化 stock 物件的屬性，然後呼叫取代（定義于*StockTicker*的頂端），將 rowTemplate 變數中的預留位置取代為 stock 物件屬性值。 產生的 HTML 會附加至股票資料表。

    您可以呼叫 init，方法是將它傳入做為在非同步啟動函數完成後執行的回呼函式。 如果您在呼叫 start 之後將 init 稱為個別的 JavaScript 語句，函式會失敗，因為它會立即執行，而不會等候啟動函式完成建立連接。 在此情況下，init 函數會嘗試在建立伺服器連接之前呼叫 getAllStocks 函式。

    當伺服器變更股票價格時，它會在已連線的用戶端上呼叫 updateStockPrice。 函式會新增至 stockTicker proxy 的用戶端屬性，讓它可供從伺服器呼叫。

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample20.js)]

    UpdateStockPrice 函數會將接收自伺服器的股票物件格式化為資料表資料列，方法與 init 函數相同。 不過，它不會將資料列附加至資料表，而是在資料表中尋找庫存的目前資料列，並將該資料列取代為新的資料列。

<a id="test"></a>

## <a name="test-the-application"></a>測試應用程式

1. 按 F5 以在偵錯模式中執行應用程式。

    股票資料表一開始會顯示「正在載入 ...」行，然後在短暫延遲之後顯示初始股票資料，然後再開始變更股票價格。

    ![正在載入](tutorial-server-broadcast-with-aspnet-signalr/_static/image7.png)

    ![初始股票表](tutorial-server-broadcast-with-aspnet-signalr/_static/image8.png)

    ![從伺服器接收變更的存貨資料表](tutorial-server-broadcast-with-aspnet-signalr/_static/image9.png)
2. 複製瀏覽器網址列中的 URL，並將它貼到一個或多個新的瀏覽器視窗中。

    初始股票顯示與第一個瀏覽器相同，而且會同時進行變更。
3. 關閉所有瀏覽器並開啟新的瀏覽器，然後移至相同的 URL。

    StockTicker singleton 物件已繼續在伺服器中執行，因此股票資料表顯示會顯示股票已繼續變更。 （您看不到具有零變更圖形的初始資料表）。
4. 關閉瀏覽器。

<a id="enablelogging"></a>

## <a name="enable-logging"></a>啟用記錄

SignalR 具有內建的記錄功能，可讓您在用戶端上啟用以協助進行疑難排解。 在本節中，您會啟用記錄並查看範例，以顯示記錄如何告訴您 SignalR 使用下列哪一個傳輸方法：

- [Websocket](http://en.wikipedia.org/wiki/WebSocket)（由 IIS 8 和目前的瀏覽器支援）。
- [伺服器傳送的事件](http://en.wikipedia.org/wiki/Server-sent_events)，由 Internet Explorer 以外的瀏覽器所支援。
- Internet Explorer 所支援的[永久框架](http://en.wikipedia.org/wiki/Comet_(programming)#Hidden_iframe)。
- 所有瀏覽器都支援[Ajax 長輪詢](http://en.wikipedia.org/wiki/Comet_(programming)#Ajax_with_long_polling)。

針對任何指定的連接，SignalR 會選擇伺服器和用戶端支援的最佳傳輸方法。

1. 開啟*StockTicker* ，並新增一行程式碼，以便在檔案結尾初始化連接的程式碼之前立即啟用記錄：

    [!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample21.js)]
2. 按 F5 執行專案。
3. 開啟瀏覽器的 [開發人員工具] 視窗，然後選取主控台以查看記錄。 您可能必須重新整理頁面，才能查看 Signalr 的記錄，以協調新連接的傳輸方法。

    如果您是在 Windows 8 （IIS 8）上執行 Internet Explorer 10，傳輸方法是 Websocket。

    ![IE 10 IIS 8 主控台](tutorial-server-broadcast-with-aspnet-signalr/_static/image10.png)

    如果您是在 Windows 7 （IIS 7.5）上執行 Internet Explorer 10，則傳輸方法是 iframe。

    ![IE 10 主控台，IIS 7。5](tutorial-server-broadcast-with-aspnet-signalr/_static/image11.png)

    在 Firefox 中，安裝 Firebug 增益集以取得主控台視窗。 如果您是在 Windows 8 （IIS 8）上執行 Firefox 19，傳輸方法是 Websocket。

    ![Firefox 19 IIS 8 Websocket](tutorial-server-broadcast-with-aspnet-signalr/_static/image12.png)

    如果您在 Windows 7 （IIS 7.5）上執行 Firefox 19，傳輸方法就是伺服器傳送的事件。

    ![Firefox 19 IIS 7.5 主控台](tutorial-server-broadcast-with-aspnet-signalr/_static/image13.png)

<a id="fullsample"></a>

## <a name="install-and-review-the-full-stockticker-sample"></a>安裝和查看完整的 StockTicker 範例

[SignalR 範例](http://nuget.org/packages/microsoft.aspnet.signalr.sample)所安裝的 StockTicker 應用程式所包含的功能，比您剛從頭建立的簡化版本還多。 在本教學課程的這一節中，您會安裝 NuGet 套件，並檢查新功能及其執行的程式碼。

### <a name="install-the-signalrsample-nuget-package"></a>安裝 SignalR NuGet 套件

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**管理 NuGet 套件**]。
2. 在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**線上**]，在 [**線上搜尋**] 方塊中輸入*SignalR* ，然後按一下**SignalR 範例**套件中的 [**安裝**]。

    ![安裝 SignalR。範例套件](tutorial-server-broadcast-with-aspnet-signalr/_static/image14.png)
3. 在*global.asax*檔案中，將 RouteTable 標記為批註 MapHubs （）;您稍早在應用程式中新增的行\_Start 方法。

    已不再需要*global.asax*中的程式碼，因為 SignalR 套件會在 App 中註冊 SignalR 路由 *\_啟動/RegisterHubs .cs*檔案：

    [!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample22.cs)]

    元件屬性所參考的 WebActivator 類別包含在 WebActivatorEx NuGet 封裝中，該套件會安裝為 SignalR 套件的相依性。
4. 在**方案總管**中，展開安裝 SignalR 範例所建立的*SignalR*資料夾。
5. 在 [ *SignalR* ] 資料夾中，以滑鼠右鍵按一下 [ *StockTicker*]，然後按一下 [**設定為起始頁**]。

    > [!NOTE]
    > 安裝 SignalR 時，NuGet 套件可能會變更您在 [*腳本*] 資料夾中的 jQuery 版本。 封裝安裝在*SignalR*中的新*StockTicker*檔案會與封裝所安裝的 jQuery 版本同步，但如果您想要再次執行原始的*StockTicker .html*檔案，您可能必須先更新腳本標記中的 jquery 參考。

### <a name="run-the-application"></a>執行應用程式

1. 按 F5 執行應用程式。

    除了您稍早看到的方格外，「全庫存指示器」應用程式會顯示水準滾動視窗，顯示相同的股票資料。 當您第一次執行應用程式時，「市場」會是「已關閉」，而您會看到不會滾動的靜態方格和「捲軸」視窗。

    ![StockTicker 畫面啟動](tutorial-server-broadcast-with-aspnet-signalr/_static/image15.png)

    當您按一下 [**開啟市場**] 時，[**即時股票行情**] 方塊會開始水準滾動，而伺服器會開始定期廣播股價變更。 每次股票價格變更時，就會更新 [**即時股票] 資料表**方格和 [**即時股票行情**] 方塊。 當股票價格變更為正面時，股票會以綠色背景顯示，而當變更為負值時，股票會以紅色背景顯示。

    ![StockTicker 應用程式，市場開放](tutorial-server-broadcast-with-aspnet-signalr/_static/image16.png)

    [**關閉市場**] 按鈕會停止變更並停止捲軸，而且 [**重設**] 按鈕會在價格變更開始之前，將所有存貨資料重設為初始狀態。 如果您開啟其他瀏覽器視窗並移至相同的 URL，您會看到相同的資料在每個瀏覽器中同時動態更新。 當您按一下其中一個按鈕時，所有瀏覽器會同時以相同的方式回應。

### <a name="live-stock-ticker-display"></a>即時股票行情顯示

**即時股票行情**指示器顯示是 div 元素中的未排序清單，會透過 CSS 樣式格式化成單行。 此指示器會以與資料表相同的方式進行初始化和更新：藉由取代 &lt;li&gt; 範本字串中的預留位置，並動態地將 &lt;li&gt; 專案新增至 &lt;ul&gt; 元素。 使用 jQuery 動畫函式來執行滾動，會改變 div 內未排序清單的左邊界。

股票行情指示器 HTML：

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample23.html)]

股票行情指示器 CSS：

[!code-html[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample24.html)]

使其滾動的 jQuery 程式碼：

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample25.js)]

### <a name="additional-methods-on-the-server-that-the-client-can-call"></a>用戶端可以呼叫之伺服器上的其他方法

StockTickerHub 類別定義了用戶端可以呼叫的四個額外方法：

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample26.cs)]

系統會呼叫 OpenMarket、CloseMarket 和 Reset，以回應頁面頂端的按鈕。 它們會示範一個用戶端的模式，其中觸發的狀態變更會立即傳播至所有用戶端。 這些方法中的每一個都會呼叫 StockTicker 類別中的方法，以影響市場狀態變更，然後廣播新的狀態。

在 StockTicker 類別中，市場的狀態是由傳回 MarketState 列舉值的 MarketState 屬性所維護：

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample27.cs)]

每個變更市場狀態的方法都會在鎖定區塊內這麼做，因為 StockTicker 類別必須是 threadsafe：

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample28.cs)]

為確保此程式碼為 threadsafe，支援 MarketState 屬性的 \_marketState 欄位會標示為 volatile，

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample29.cs)]

BroadcastMarketStateChange 和 BroadcastMarketReset 方法類似于您已看到的 BroadcastStockPrice 方法，不同的是，它們會呼叫用戶端上定義的不同方法：

[!code-csharp[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample30.cs)]

### <a name="additional-functions-on-the-client-that-the-server-can-call"></a>伺服器可以呼叫之用戶端上的其他函數

UpdateStockPrice 函式現在會同時處理方格和捲軸顯示，並使用 jQuery. 色彩來閃爍紅色和綠色色彩。

*SignalR*中的新函式會根據市場狀態來啟用和停用按鈕，並停止或啟動 [捲軸] 視窗水準滾動。 因為有多個函式會新增至「指示器」，所以會使用[jQuery extend 函數](http://api.jquery.com/jQuery.extend/)來新增它們。

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample31.js)]

### <a name="additional-client-setup-after-establishing-the-connection"></a>建立連線後的其他用戶端設定

用戶端建立連線之後，會有一些額外的工作需要執行：找出市場是否已開啟或已關閉，以呼叫適當的 marketOpened 或 marketClosed 函式，並將伺服器方法呼叫附加至按鈕。

[!code-javascript[Main](tutorial-server-broadcast-with-aspnet-signalr/samples/sample32.js)]

在建立連接之後，伺服器方法不會連線到按鈕，因此程式碼無法在可用之前嘗試呼叫伺服器方法。

<a id="nextsteps"></a>

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已瞭解如何設計 SignalR 應用程式，將訊息從伺服器廣播到所有已連線的用戶端，並定期並回應來自任何用戶端的通知。 使用多執行緒單一實例來維護伺服器狀態的模式也可以在多玩家線上遊戲案例中使用。 如需範例，請參閱以[SignalR 為基礎的 ShootR 遊戲](https://github.com/NTaylorMullen/ShootR)。

如需顯示點對點通訊案例的教學課程，請參閱[使用 SignalR](index.md)和[使用 SignalR 進行即時更新](index.md)的消費者入門。

若要深入瞭解更先進的 SignalR 開發概念，請造訪下列網站以取得 SignalR 原始程式碼和資源：

- [ASP.NET SignalR](https://asp.net/signalr/)
- [SignalR 專案](http://signalr.net/)
- [SignalR Github 和範例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
