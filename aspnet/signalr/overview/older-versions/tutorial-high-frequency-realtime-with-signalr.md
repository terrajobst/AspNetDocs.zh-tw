---
uid: signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
title: 具有 SignalR 1.x 的高頻率即時 |Microsoft Docs
author: bradygaster
description: 本教學課程說明如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供高頻率的訊息功能。 中的高頻率訊息 。
ms.author: bradyg
ms.date: 04/16/2013
ms.assetid: ad2a5da5-2e79-40ea-bc84-028d327f5982
msc.legacyurl: /signalr/overview/older-versions/tutorial-high-frequency-realtime-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: e37e63a410952ec170cbbaadeeb54eae7e82b3b5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623498"
---
# <a name="high-frequency-realtime-with-signalr-1x"></a>使用 SignalR 1.x 進行高頻率即時聊天

由[派翠克 Fletcher](https://github.com/pfletcher)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教學課程說明如何建立使用 ASP.NET SignalR 的 web 應用程式，以提供高頻率的訊息功能。 在此情況下，高頻率訊息表示以固定速率傳送的更新;在此應用程式的案例中，每秒最多10個訊息。
> 
> 您在本教學課程中建立的應用程式會顯示使用者可以拖曳的圖形。 接著，所有其他已連接的瀏覽器中的圖形位置都會更新，以符合使用計時更新所拖曳之圖形的位置。
> 
> 本教學課程中引進的概念，具有即時遊戲和其他模擬應用程式中的應用程式。
> 
> 歡迎使用教學課程的批註。 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com)。

## <a name="overview"></a>概觀

本教學課程示範如何建立應用程式，以與其他瀏覽器即時共用物件的狀態。 我們將建立的應用程式稱為 MoveShape。 [MoveShape] 頁面會顯示使用者可以拖曳的 HTML Div 元素;當使用者拖曳 Div 時，其新位置將會傳送至伺服器，然後通知所有其他已連線的用戶端更新圖形的位置以符合。

![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image1.png)

在本教學課程中建立的應用程式是以 Damian Edwards 的示範為基礎。 您可以在[這裡](https://channel9.msdn.com/Series/Building-Web-Apps-with-ASP-NET-Jump-Start/Building-Web-Apps-with-ASPNET-Jump-Start-08-Real-time-Communication-with-SignalR)看到包含此示範的影片。

本教學課程一開始會示範如何從每個引發的事件中，將 SignalR 訊息傳送至拖曳的圖形。 每次已連線的用戶端都會在收到訊息時，更新局部版本的圖形位置。

雖然應用程式會使用此方法運作，但這不是建議的程式設計模型，因為傳送的訊息數目沒有上限，因此用戶端和伺服器可能會因為訊息而變得很龐大，而且效能會降低. 在用戶端上顯示的動畫也會脫離，因為圖形會立即由每個方法移動，而不會順暢地移至每個新位置。 本教學課程的後續章節將示範如何建立計時器函式，以限制用戶端或伺服器傳送訊息的最大速率，以及如何在位置之間順暢地移動圖形。 您可以從程式[代碼庫](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)下載本教學課程中所建立的最終應用程式版本。

本教學課程包含下列各節：

- [必要條件](#prerequisites)
- [建立專案](#createtheproject)
- [新增 ASP.NET SignalR 和 JQuery. UI NuGet 套件](#nugetpackages)
- [建立基底應用程式](#baseapp)
- [新增用戶端迴圈](#clientloop)
- [新增伺服器迴圈](#serverloop)
- [在用戶端上新增平滑動畫](#animation)
- [進一步的步驟](#furthersteps)

<a id="prerequisites"></a>

## <a name="prerequisites"></a>Prerequisites

本教學課程需要 Visual Studio 2012 或 Visual Studio 2010。 如果使用 Visual Studio 2010，專案將會使用 .NET Framework 4，而不是 .NET Framework 4.5。

如果您使用 Visual Studio 2012，建議您安裝[ASP.NET 和 Web 工具2012.2 更新](https://go.microsoft.com/fwlink/?LinkId=282650)。 此更新包含新功能，例如發佈、新功能和新範本的增強功能。

如果您有 Visual Studio 2010，請確定已安裝[NuGet](https://visualstudiogallery.msdn.microsoft.com/27077b70-9dad-4c64-adcf-c7cf6bc9970c) 。

<a id="createtheproject"></a>

## <a name="create-the-project"></a>建立專案

在本節中，我們將在 Visual Studio 中建立專案。

1. 從 [檔案] 功能表，按一下 [新增專案]。
2. 在 [**新增專案**] 對話方塊中， **C#** 展開 [**範本**]，然後選取 [ **Web**]。
3. 選取 [ **ASP.NET 空白 Web 應用程式**] 範本，將專案命名為*MoveShapeDemo*，然後按一下 **[確定]** 。

    ![建立新專案](tutorial-high-frequency-realtime-with-signalr/_static/image2.png)

<a id="nugetpackages"></a>

## <a name="add-the-signalr-and-jqueryui-nuget-packages"></a>新增 SignalR 和 JQuery。 UI NuGet 套件

您可以藉由安裝 NuGet 套件，將 SignalR 功能新增至專案。 本教學課程也會使用 JQuery. UI 封裝，讓圖形得以拖曳和動畫。

1. 按一下 [**工具] |NuGet 套件管理員 |套件管理員主控台**。
2. 在 [套件管理員] 中輸入下列命令。

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample1.ps1)]

    SignalR 套件會安裝一些其他 NuGet 套件做為相依性。 當安裝完成時，您會擁有在 ASP.NET 應用程式中使用 SignalR 所需的所有伺服器和用戶端元件。
3. 在 [套件管理員主控台] 中輸入下列命令，以安裝 JQuery 和 JQuery. UI 封裝。

    [!code-powershell[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample2.ps1)]

<a id="baseapp"></a>

## <a name="create-the-base-application"></a>建立基底應用程式

在本節中，我們將建立瀏覽器應用程式，以便在每個滑鼠移動事件期間，將圖形的位置傳送至伺服器。 接著，伺服器會將此資訊廣播到所有其他已連線的用戶端。 我們將在稍後的章節中展開此應用程式。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增**]、[**類別**...]。將類別命名為**MoveShapeHub** ，然後按一下 [**新增**]。
2. 將新的**MoveShapeHub**類別中的程式碼取代為下列程式碼。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample3.cs)]

    上述 `MoveShapeHub` 類別是 SignalR 中樞的執行。 如同在[消費者入門 With SignalR](index.md)教學課程中，中樞具有一種方法，可讓用戶端直接呼叫。 在此情況下，用戶端會將包含圖形新 X 和 Y 座標的物件傳送至伺服器，然後再將其廣播至所有其他已連線的用戶端。 SignalR 會使用 JSON 自動序列化此物件。

    將傳送至用戶端的物件（`ShapeModel`）包含用來儲存圖形位置的成員。 伺服器上的物件版本也包含成員，以追蹤正在儲存的用戶端資料，讓指定的用戶端不會傳送自己的資料。 這個成員會使用 `JsonIgnore` 屬性，讓它不被序列化並傳送到用戶端。
3. 接下來，我們會在應用程式啟動時設定中樞。 在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**新增] |全域應用程式類別**。 接受*全域*的預設名稱，然後按一下 **[確定]** 。

    ![新增全域應用程式類別](tutorial-high-frequency-realtime-with-signalr/_static/image3.png)
4. 在 Global.asax.cs 類別中提供的**using**語句之後，新增下列 `using` 語句。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample4.cs)]
5. 在全域類別的 `Application_Start` 方法中新增下列程式程式碼，以註冊 SignalR 的預設路由。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample5.cs)]

    您的 global.asax 檔案看起來應該如下所示：

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample6.cs)]
6. 接下來，我們要新增用戶端。 在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**新增] |新專案**。 在 [**加入新專案**] 對話方塊中，選取 [ **Html 網頁**]。 為頁面指定適當的名稱（例如 [ **.html**]），然後按一下 [**新增**]。
7. 在**方案總管**中，以滑鼠右鍵按一下您剛建立的頁面，然後按一下 [**設定為起始頁**]。
8. 將 HTML 網頁中的預設程式碼取代為下列程式碼片段。

    > [!NOTE]
    > 確認下列腳本參考符合在 [腳本] 資料夾中新增至專案的套件。 在 Visual Studio 2010 中，加入至專案的 JQuery 和 SignalR 版本可能與下列版本號碼不相符。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample7.html)]

    上述 HTML 和 JavaScript 程式碼會建立稱為 Shape 的紅色 Div，使用 jQuery 程式庫啟用圖形的拖曳行為，並使用圖形的 `drag` 事件將圖形的位置傳送至伺服器。
9. 按 F5 啟動應用程式。 複製頁面的 URL，並將它貼入第二個瀏覽器視窗。 將圖形拖曳到其中一個瀏覽器視窗中;另一個瀏覽器視窗中的圖形應該會移動。

    ![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image4.png)

<a id="clientloop"></a>

## <a name="add-the-client-loop"></a>新增用戶端迴圈

由於在每個滑鼠移動事件上傳送圖形的位置，將會產生不必要的網路流量量，因此來自用戶端的訊息必須進行節流。 我們將使用 javascript `setInterval` 函數來設定迴圈，以固定速率將新的位置資訊傳送至伺服器。 這個迴圈是一個非常基本的「遊戲迴圈」標記法，這是一種重複呼叫的函式，可驅動遊戲或其他模擬的所有功能。

1. 更新 HTML 網頁中的用戶端程式代碼，以符合下列程式碼片段。

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample8.html)]

    上述更新會新增 `updateServerModel` 函式，此函式會以固定頻率呼叫。 每當 `moved` 旗標指出有要傳送的新位置資料時，此函數就會將位置資料傳送至伺服器。
2. 按 F5 啟動應用程式。 複製頁面的 URL，並將它貼入第二個瀏覽器視窗。 將圖形拖曳到其中一個瀏覽器視窗中;另一個瀏覽器視窗中的圖形應該會移動。 因為傳送至伺服器的訊息數目將會受到節流，所以動畫不會像上一節一樣平滑。

    ![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image5.png)

<a id="serverloop"></a>

## <a name="add-the-server-loop"></a>新增伺服器迴圈

在目前的應用程式中，從伺服器傳送到用戶端的訊息會在收到時經常消失。 這會呈現在用戶端上看到的類似問題;訊息的傳送頻率可能比所需的還多，而且連接可能會變得太大。 本節說明如何補救伺服器，以執行會節流傳出訊息速率的計時器。

1. 將 `MoveShapeHub.cs` 的內容取代為下列程式碼片段。

    [!code-csharp[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample9.cs)]

    上述程式碼會擴充用戶端，以加入 `Broadcaster` 類別，這會使用 .NET framework 中的 `Timer` 類別來節流外寄訊息。

    由於中樞本身是暫時性的（每次需要時都會建立），因此 `Broadcaster` 將會建立為單一實例。 延遲初始化（在 .NET 4 中引進）是用來延遲其建立，直到需要它為止，確保在啟動計時器之前，會完全建立第一個中樞實例。

    接著，對用戶端的 `UpdateShape` 函式的呼叫會移出中樞的 `UpdateModel` 方法，如此一來，只要收到傳入訊息，就不會再立即呼叫該函數。 相反地，用戶端的訊息會以每秒25次呼叫的速率傳送，由 `Broadcaster` 類別內的 `_broadcastLoop` 計時器管理。

    最後，`Broadcaster` 類別不會直接從中樞呼叫用戶端方法，而是必須使用 `GlobalHost`取得目前操作中樞（`_hubContext`）的參考。
2. 按 F5 啟動應用程式。 複製頁面的 URL，並將它貼入第二個瀏覽器視窗。 將圖形拖曳到其中一個瀏覽器視窗中;另一個瀏覽器視窗中的圖形應該會移動。 上一節的瀏覽器中不會有明顯的差異，但傳送至用戶端的訊息數目將會受到節流。

    ![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image6.png)

<a id="animation"></a>

## <a name="add-smooth-animation-on-the-client"></a>在用戶端上新增平滑動畫

應用程式幾乎已完成，但我們可以在用戶端的圖形移動時，將其移至回應伺服器消息時，改善一個更好的改良。 我們會使用 JQuery UI 程式庫的 `animate` 函式，在其目前和新位置之間順暢地移動圖形，而不是將圖形的位置設定為伺服器所指定的新位置。

1. 更新用戶端的 `updateShape` 方法，讓它看起來像下面的反白顯示的程式碼：

    [!code-html[Main](tutorial-high-frequency-realtime-with-signalr/samples/sample10.html?highlight=35-42)]

    上述程式碼會在動畫間隔（在此案例中為100毫秒）的過程中，將圖形從舊位置移至伺服器提供的新位置。 在新動畫開始之前，會先清除在圖形上執行的任何先前動畫。
2. 按 F5 啟動應用程式。 複製頁面的 URL，並將它貼入第二個瀏覽器視窗。 將圖形拖曳到其中一個瀏覽器視窗中;另一個瀏覽器視窗中的圖形應該會移動。 在另一個視窗中，圖形的移動應該顯示得比較少，因為它會在一段時間內插補，而不是針對每個傳入訊息設定一次。

    ![應用程式視窗](tutorial-high-frequency-realtime-with-signalr/_static/image7.png)

<a id="furthersteps"></a>

## <a name="further-steps"></a>進一步的步驟

在本教學課程中，您已瞭解如何針對在用戶端與伺服器之間傳送高頻率訊息的 SignalR 應用程式進行程式設計。 此通訊範例適用于開發線上遊戲和其他模擬，例如[使用 SignalR 建立的 ShootR 遊戲](http://shootr.signalr.net)。

您可以從程式[代碼庫](https://code.msdn.microsoft.com/SignalR-MoveShape-demo-3366dac6)下載本教學課程中建立的完整應用程式。

若要深入瞭解 SignalR 開發概念，請造訪下列網站以取得 SignalR 原始程式碼和資源：

- [SignalR 專案](http://signalr.net)
- [SignalR Github 和範例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
