---
uid: signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
title: 教學課程：使用 SignalR 2 建立高頻率即時應用程式 |Microsoft Docs
author: bradygaster
description: 本教學課程說明如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供高頻率的訊息功能。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 9f969dda-78ea-4329-b1e3-e51c02210a2b
msc.legacyurl: /signalr/overview/getting-started/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 2503e90735d6cfa445ee08c9e43f8443aa106096
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600460"
---
# <a name="tutorial-create-high-frequency-real-time-app-with-signalr-2"></a>教學課程：使用 SignalR 2 建立高頻率即時應用程式

本教學課程示範如何建立使用 ASP.NET SignalR 2 的 web 應用程式，以提供高頻率的訊息功能。 在此情況下，「高頻率訊息」表示伺服器會以固定的速率傳送更新。 您每秒最多傳送10則訊息。

您所建立的應用程式會顯示使用者可以拖曳的圖形。 伺服器會在所有連接的瀏覽器中更新圖形的位置，以符合使用計時更新所拖曳之圖形的位置。

本教學課程中引進的概念，具有即時遊戲和其他模擬應用程式中的應用程式。

在本教學課程中，您已：

> [!div class="checklist"]
> * 設定專案
> * 建立基底應用程式
> * 在應用程式啟動時對應至中樞
> * 新增用戶端
> * 執行應用程式
> * 新增用戶端迴圈
> * 新增伺服器迴圈
> * 新增平滑動畫

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>必要條件：

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)搭配**ASP.NET 和 網頁程式開發**工作負載。

## <a name="set-up-the-project"></a>設定專案

在本節中，您會在 Visual Studio 2017 中建立專案。

本節說明如何使用 Visual Studio 2017 來建立空的 ASP.NET Web 應用程式，並新增 SignalR 和 jQuery UI 程式庫。

1. 在 Visual Studio 中，建立 ASP.NET Web 應用程式。

    ![建立 web](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

1. 在 [**新增 ASP.NET Web 應用程式-MoveShapeDemo** ] 視窗中，保持選取 [**空白**]，然後選取 **[確定]** 。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。

1. 在 **[加入新專案-MoveShapeDemo**] 中，選取 [**已安裝**] >  **C# Visual** > **Web** > **SignalR** ，然後選取 **[SignalR 中樞類別（v2）** ]。

1. 將類別命名為*MoveShapeHub* ，並將它加入至專案。

    此步驟會建立*MoveShapeHub.cs*類別檔案。 同時，它會加入一組腳本檔案和元件參考，以支援 SignalR 至專案。

1. 選取 **工具** > **NuGet 套件管理員** > **套件管理員主控台**。

1. 在 [**套件管理員主控台**] 中，執行下列命令：

    ```console
    Install-Package jQuery.UI.Combined
    ```

    命令會安裝 jQuery UI 程式庫。 您可以使用它來建立圖形的動畫。

1. 在**方案總管**中，展開 [腳本] 節點。

    ![腳本程式庫參考](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

    JQuery、jQueryUI 和 SignalR 的腳本程式庫會顯示在專案中。

## <a name="create-the-base-application"></a>建立基底應用程式

在本節中，您會建立瀏覽器應用程式。 應用程式會在每個滑鼠移動事件期間，將圖形位置傳送至伺服器。 伺服器會即時將這項資訊廣播給所有其他已連線的用戶端。 您可以在稍後的章節中深入瞭解此應用程式。

1. 開啟*MoveShapeHub.cs*檔案。

1. 將*MoveShapeHub.cs*檔案中的程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.cs)]

1. 儲存檔案。

`MoveShapeHub` 類別是 SignalR 中樞的執行。 如同在[消費者入門 With SignalR](tutorial-getting-started-with-signalr.md)教學課程中，中樞具有用戶端直接呼叫的方法。 在此情況下，用戶端會將具有圖形的新 X 和 Y 座標的物件傳送至伺服器。 這些座標會被廣播到所有其他已連線的用戶端。 SignalR 會使用 JSON 自動序列化此物件。

應用程式會將 `ShapeModel` 物件傳送至用戶端。 它具有可儲存圖形位置的成員。 伺服器上的物件版本也具有成員，可以追蹤正在儲存的用戶端資料。 此物件可防止伺服器將用戶端的資料傳送回其本身。 這個成員會使用 `JsonIgnore` 屬性，以防止應用程式將資料序列化，並將其傳回用戶端。

## <a name="map-to-the-hub-when-app-starts"></a>在應用程式啟動時對應至中樞

接下來，您會在應用程式啟動時設定與中樞的對應。 在 SignalR 2 中，新增 OWIN 啟動類別會建立對應。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。

1. 在 [**加入新專案-MoveShapeDemo** ] 中，選取 [**已安裝** > **Visual C#**  > **Web** ]，然後選取 [ **OWIN 啟動類別**]。

1. 將類別命名為*Startup* ，然後選取 **[確定]** 。

1. 使用下列程式碼取代*Startup.cs*檔案中的預設程式碼：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.cs)]

OWIN 啟動類別會在應用程式執行 `Configuration` 方法時呼叫 `MapSignalR`。 應用程式會使用 `OwinStartup` 元件屬性，將類別新增至 OWIN 的啟動進程。

## <a name="add-the-client"></a>新增用戶端

新增用戶端的 HTML 頁面。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **HTML 網頁**]。

1. 將頁面命名為**預設值**，然後選取 **[確定]** 。

1. 在**方案總管**中，以滑鼠右鍵按一下 [*預設的 .html* ]，然後選取 [**設定為起始頁**]。

1. 使用下列程式碼取代*預設 .html*檔案中的預設程式碼：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.html?highlight=14-16)]

1. 在**方案總管**中，展開 [**腳本**]。

    JQuery 和 SignalR 的腳本程式庫會顯示在專案中。

    > [!IMPORTANT]
    > 封裝管理員會安裝較新版本的 SignalR 腳本。

1. 更新程式碼區塊中的腳本參考，以對應至專案中的腳本檔案版本。

此 HTML 和 JavaScript 程式碼會建立稱為 `shape`的紅色 `div`。 它會使用 jQuery 程式庫來啟用圖形的拖曳行為，並使用 `drag` 事件將圖形的位置傳送至伺服器。

## <a name="run-the-app"></a>執行應用程式

您可以執行應用程式來 se'e 其運作。 當您將圖形拖曳至瀏覽器視窗時，圖形也會移到其他瀏覽器中。

1. 在工具列中，開啟 [**腳本調試**程式]，然後選取 [播放] 按鈕，以在 [偵測模式] 中執行應用程式。

    ![使用者開啟偵錯模式和選取 [播放] 的螢幕擷取畫面。](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)

    瀏覽器視窗隨即開啟，並在右上角出現紅色形狀。

1. 複製頁面的 URL。

1. 開啟另一個瀏覽器，並將 URL 貼到網址列中。

1. 將圖形拖曳到其中一個瀏覽器視窗中。 另一個瀏覽器視窗中的圖形如下所示。

雖然應用程式會使用這個方法來運作，但它並不是建議的程式設計模型。 傳送的訊息數目沒有上限。 因此，用戶端和伺服器會因為訊息和效能降低而變得非常龐大。 此外，應用程式會在用戶端上顯示脫離的動畫。 因為圖形會立即透過每個方法移動，所以會發生這個無法停用的動畫。 如果圖形順暢地移到每個新位置，這會更好。 接下來，您將瞭解如何修正這些問題。

## <a name="add-the-client-loop"></a>新增用戶端迴圈

在每個滑鼠移動事件上傳送圖形的位置，會建立不必要的網路流量量。 應用程式需要對用戶端的訊息進行節流處理。

使用 javascript `setInterval` 函數來設定迴圈，以固定速率將新的位置資訊傳送至伺服器。 這個迴圈是「遊戲迴圈」的基本標記法。 它是重複呼叫的函式，它會驅動遊戲的所有功能。

1. 將*預設 .html*檔案中的用戶端程式代碼取代為下列程式碼：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.html?highlight=14-16)]

    > [!IMPORTANT]
    > 您必須再次取代腳本參考。 它們必須符合專案中的腳本版本。

    這個新的程式碼會加入 `updateServerModel` 函式。 它會以固定頻率呼叫。 每當 `moved` 旗標指出有要傳送的新位置資料時，函數就會將位置資料傳送至伺服器。

1. 選取 [播放] 按鈕以啟動應用程式

1. 複製頁面的 URL。

1. 開啟另一個瀏覽器，並將 URL 貼到網址列中。

1. 將圖形拖曳到其中一個瀏覽器視窗中。 另一個瀏覽器視窗中的圖形如下所示。

由於應用程式會節流傳送至伺服器的訊息數目，因此，動畫一開始不會顯示為平滑。

## <a name="add-the-server-loop"></a>新增伺服器迴圈

在目前的應用程式中，從伺服器傳送到用戶端的訊息會在收到時經常消失。 這種網路流量呈現的問題與在用戶端上看到的類似。

應用程式可以傳送的訊息頻率會高於所需。 如此一來，連接可能會變得很溢。 本章節描述如何補救伺服器，以新增計時器來限制外寄訊息的速率。

1. 將 `MoveShapeHub.cs` 的內容取代為下列程式碼：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

1. 選取 [播放] 按鈕以啟動應用程式。

1. 複製頁面的 URL。

1. 開啟另一個瀏覽器，並將 URL 貼到網址列中。

1. 將圖形拖曳到其中一個瀏覽器視窗中。

此程式碼會擴充用戶端，以加入 `Broadcaster` 類別。 新類別會使用 .NET framework 中的 `Timer` 類別來節流外寄訊息。

瞭解中樞本身是暫時性的，是很好的。 它會在每次需要時建立。 因此，應用程式會建立 `Broadcaster` 做為單一實例。 它會使用延遲初始化來延遲 `Broadcaster`的建立，直到需要它為止。 這可確保應用程式在啟動計時器之前完全建立第一個中樞實例。

然後，對用戶端的 `UpdateShape` 函式的呼叫會移出中樞的 `UpdateModel` 方法。 每當應用程式收到傳入訊息時，就不會再立即呼叫它。 相反地，應用程式會以每秒25次呼叫的速率，將訊息傳送給用戶端。 進程是由 `Broadcaster` 類別內的 `_broadcastLoop` 計時器所管理。

最後，`Broadcaster` 類別不會直接從中樞呼叫用戶端方法，而是需要取得目前操作 `_hubContext` 中樞的參考。 它會取得 `GlobalHost`的參考。

## <a name="add-smooth-animation"></a>新增平滑動畫

應用程式幾乎已經完成，但我們可以改善一個。 應用程式會在用戶端上移動圖形，以回應伺服器消息。 請使用 JQuery UI 程式庫的 `animate` 函式，而不是將圖形的位置設定為伺服器所指定的新位置。 它可以在其目前和新位置之間順暢地移動圖形。

1. 更新*預設 .html*檔案中用戶端的 `updateShape` 方法，看起來像反白顯示的程式碼：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.html?highlight=33-40)]

1. 選取 [播放] 按鈕以啟動應用程式。

1. 複製頁面的 URL。

1. 開啟另一個瀏覽器，並將 URL 貼到網址列中。

1. 將圖形拖曳到其中一個瀏覽器視窗中。

在另一個視窗中的圖形移動會顯示較不停的。 應用程式會在一段時間內插補其移動，而不是針對每個傳入訊息設定一次。

此程式碼會將圖形從舊位置移至新位置。 伺服器會在動畫間隔的過程中提供圖形的位置。 在此情況下，這是100毫秒。 應用程式會在新的動畫開始之前，清除在圖形上執行的任何先前動畫。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://code.msdn.microsoft.com/SignalR-20-MoveShape-Demo-6285b83a)

## <a name="additional-resources"></a>其他資源

您剛學到的溝通架構，對於開發線上遊戲和其他模擬很有用，例如[使用 SignalR 所建立的 ShootR 遊戲](https://shootr.azurewebsites.net/)。

如需 SignalR 的詳細資訊，請參閱下列資源：

* [SignalR 專案](http://signalr.net)

* [SignalR GitHub 和範例](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 設定專案
> * 建立基底應用程式
> * 在應用程式啟動時對應至中樞
> * 新增用戶端
> * 執行應用程式
> * 新增用戶端迴圈
> * 已新增伺服器迴圈
> * 已新增平滑動畫

前進到下一篇文章，以瞭解如何建立使用 ASP.NET SignalR 2 來提供伺服器廣播功能的 web 應用程式。
> [!div class="nextstepaction"]
> [SignalR 2 和伺服器廣播](tutorial-server-broadcast-with-signalr.md)