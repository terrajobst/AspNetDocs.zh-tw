---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr
title: 教學課程：使用 SignalR 1.x 的消費者入門 |Microsoft Docs
author: bradygaster
description: 使用 ASP.NET SignalR 在 HTML 網頁中建立即時聊天應用程式。
ms.author: bradyg
ms.date: 02/18/2013
ms.assetid: fdc3599a-5217-44c1-951f-0eec9812dce7
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.openlocfilehash: 87a90b47ae30bee43e0b0c1e078597db54b8e67d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78623540"
---
# <a name="tutorial-getting-started-with-signalr-1x"></a>教學課程：使用 SignalR 1.x 消費者入門

[Fletcher](https://github.com/pfletcher)的[Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 此教學課程會示範如何使用 SignalR 建立即時聊天應用程式。 您會將 SignalR 新增至空白的 ASP.NET web 應用程式，並建立用來傳送和顯示訊息的 HTML 頁面。

## <a name="overview"></a>概觀

本教學課程會示範如何建立以瀏覽器為基礎的簡單交談應用程式，以介紹 SignalR 開發。 您會將 SignalR 程式庫新增至空白的 ASP.NET web 應用程式、建立可將訊息傳送至用戶端的中樞類別，以及建立可讓使用者傳送及接收聊天訊息的 HTML 網頁。 如需示範如何使用 MVC 視圖在 MVC 4 中建立聊天應用程式的類似教學課程，請參閱[使用 SignalR 和 MVC 4 的消費者入門](index.md)。

> [!NOTE]
> 本教學課程使用 release （1.x）版的 SignalR。 如需 SignalR 1.x 與2.0 之間變更的詳細資訊，請參閱[升級 SignalR 1.X 專案](../releases/upgrading-signalr-1x-projects-to-20.md)。

SignalR 是一個開放原始碼 .NET 程式庫，用於建立需要即時使用者互動或即時資料更新的 web 應用程式。 範例包括社交應用程式、多使用者遊戲、商務共同作業，以及新聞、天氣或金融更新應用程式。 這些通常稱為即時應用程式。

SignalR 簡化了建立即時應用程式的流程。 其中包含 ASP.NET 伺服器程式庫和 JavaScript 用戶端程式庫，可讓您更輕鬆地管理用戶端伺服器連線，以及將內容更新推送至用戶端。 您可以將 SignalR 程式庫新增至現有的 ASP.NET 應用程式，以取得即時功能。

本教學課程會示範下列 SignalR 開發工作：

- 將 SignalR 程式庫新增至 ASP.NET web 應用程式。
- 建立中樞類別以將內容推送至用戶端。
- 使用網頁中的 SignalR jQuery 程式庫來傳送訊息，並從中樞顯示更新。

下列螢幕擷取畫面顯示在瀏覽器中執行的聊天應用程式。 每個新的使用者都可以張貼留言，並在使用者加入聊天之後，看到新增的批註。

![聊天實例](tutorial-getting-started-with-signalr/_static/image1.png)

各節

- [設定專案](#setup)
- [執行範例](#run)
- [檢查程式碼](#code)
- [後續步驟](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>設定專案

本節說明如何建立空白的 ASP.NET web 應用程式、新增 SignalR，以及建立聊天應用程式。

必要條件：

- Visual Studio 2010 SP1 或2012。 如果您沒有 Visual Studio，請參閱[ASP.NET 下載](https://www.asp.net/downloads)以取得免費的 Visual Studio 2012 Express 開發工具。
- [Microsoft ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941)。 針對 Visual Studio 2012，此安裝程式會將新的 ASP.NET 功能（包括 SignalR 範本）新增至 Visual Studio。 針對 Visual Studio 2010 SP1，安裝程式無法使用，但您可以安裝 SignalR NuGet 套件（如設定步驟中所述）來完成本教學課程。

下列步驟會使用 Visual Studio 2012 來建立 ASP.NET 空白 Web 應用程式，並新增 SignalR 程式庫：

1. 在 Visual Studio 建立 ASP.NET 空白 Web 應用程式。

    ![建立空的 web](tutorial-getting-started-with-signalr/_static/image2.png)
2. 選取 [工具]，開啟 [**套件管理員主控台**] **|NuGet 套件管理員 |套件管理員主控台**。 在主控台視窗中輸入下列命令：

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    此命令會安裝最新版本的 SignalR 1.x。
3. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增] |類別**。 將新類別命名為**ChatHub**。
4. 在**方案總管**展開 [腳本] 節點。 JQuery 和 SignalR 的腳本程式庫會顯示在專案中。

    ![程式庫參考](tutorial-getting-started-with-signalr/_static/image3.png)
5. 將**ChatHub**類別中的程式碼取代為下列程式碼。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. 在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**新增] |新專案**。 在 [**加入新專案**] 對話方塊中，選取 [**全域應用程式類別**]，然後按一下 [**新增**]。

    ![加入全域](tutorial-getting-started-with-signalr/_static/image4.png)
7. 在 Global.asax.cs 類別中提供的 `using` 語句之後，新增下列 `using` 語句。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. 在全域類別的 `Application_Start` 方法中新增下列程式程式碼，以註冊 SignalR 中樞的預設路由。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. 在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**新增] |新專案**。 在 [**加入新專案**] 對話方塊中，選取 [Html 網頁]，然後按一下 [**新增**]。
10. 在**方案總管**中，以滑鼠右鍵按一下您剛建立的 HTML 網頁，然後按一下 [**設定為起始頁**]。
11. 將 HTML 網頁中的預設程式碼取代為下列程式碼。

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. **全部儲存**專案。

<a id="run"></a>

## <a name="run-the-sample"></a>執行範例

1. 按 F5 以在 [調試] 模式中執行專案。 HTML 頁面會在瀏覽器實例中載入，並提示您輸入使用者名稱。

    ![輸入使用者名稱](tutorial-getting-started-with-signalr/_static/image5.png)
2. 輸入使用者稱。
3. 從瀏覽器的位址行複製 URL，並用它來開啟兩個以上的瀏覽器實例。 在每個瀏覽器實例中，輸入唯一的使用者名稱。
4. 在每個瀏覽器實例中新增批註，然後按一下 [**傳送**]。 批註應該會顯示在所有瀏覽器實例中。

    > [!NOTE]
    > 這個簡單的聊天應用程式不會維護伺服器上的討論內容。 中樞會將批註廣播給所有目前的使用者。 稍後加入交談的使用者會看到從他們加入的時間新增的訊息。

    下列螢幕擷取畫面顯示在三個瀏覽器實例中執行的聊天應用程式，其中的每個實例都會在傳送訊息時進行更新：

    ![聊天瀏覽器](tutorial-getting-started-with-signalr/_static/image6.png)
5. 在**方案總管**中，檢查執行中應用程式的 [**指令檔**] 節點。 有一個名為**hub**的腳本檔案，SignalR 程式庫會在執行時間動態產生此檔案。 這個檔案會管理 jQuery 腳本與伺服器端程式碼之間的通訊。

    ![產生的中樞腳本](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a>檢查程式碼

SignalR chat 應用程式會示範兩個基本的 SignalR 開發工作：建立中樞做為伺服器上的主要協調物件，以及使用 SignalR jQuery 程式庫來傳送和接收訊息。

### <a name="signalr-hubs"></a>SignalR 中樞

在程式碼範例中， **ChatHub**類別衍生自**SignalR**類別。 從**中樞**類別衍生的是建立 SignalR 應用程式的實用方式。 您可以在中樞類別上建立公用方法，然後從網頁中的 jQuery 腳本呼叫這些方法來存取這些方法。

在聊天程式碼中，用戶端會呼叫**ChatHub** ，以傳送新的訊息。 接著，中樞會藉由呼叫**broadcastMessage**，將訊息傳送至所有用戶端。

**Send**方法會示範數個中樞概念：

- 在中樞上宣告公用方法，讓用戶端可以呼叫它們。
- 使用**SignalR**動態屬性來存取連線至此中樞的所有用戶端。
- 呼叫用戶端上的 jQuery 函式（例如 `broadcastMessage` 函數）來更新用戶端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 和 jQuery

程式碼範例中的 HTML 網頁會示範如何使用 SignalR jQuery 程式庫來與 SignalR 中樞進行通訊。 程式碼中的基本工作是宣告 proxy 來參考中樞、宣告伺服器可以呼叫的函式，將內容推送至用戶端，以及啟動連線以將訊息傳送至中樞。

下列程式碼會宣告中樞的 proxy。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> 在 jQuery 中，伺服器類別及其成員的參考是 camel 大小寫。 此程式碼範例會C#將 jQuery 中的**ChatHub**類別參考為**ChatHub**。

下列程式碼是您在腳本中建立回呼函數的方式。 伺服器上的中樞類別會呼叫此函式，將內容更新推送至每個用戶端。 在顯示內容之前進行 HTML 編碼的兩行程式碼是選擇性的，而且會顯示一個簡單的方法來防止腳本插入。

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

下列程式碼顯示如何開啟與中樞的連線。 程式碼會啟動連接，然後將函式傳遞給它，以處理 HTML 網頁中 [**傳送**] 按鈕上的 click 事件。

> [!NOTE]
> 這個方法可確保在事件處理常式執行之前就已建立連接。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>後續步驟

您已瞭解 SignalR 是用來建立即時 web 應用程式的架構。 您也學到幾個 SignalR 的開發工作：如何將 SignalR 新增至 ASP.NET 應用程式、如何建立中樞類別，以及如何從中樞傳送和接收訊息。

您可以透過將範例應用程式部署至主機服務提供者，在本教學課程或透過網際網路提供的其他 SignalR 應用程式中進行。 Microsoft 在免費的[Windows Azure 試用帳戶](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中，最多可為10個網站提供免費的 web 主機。 如需如何部署範例 SignalR 應用程式的逐步解說，請參閱[將 SignalR 消費者入門範例發佈為 Windows Azure 網站](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)。 如需如何將 Visual Studio Web 專案部署至 Windows Azure 網站的詳細資訊，請參閱將[ASP.NET 應用程式部署至 Windows azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)網站。 （注意：目前不支援 Windows Azure 網站的 WebSocket 傳輸。 當 WebSocket 傳輸無法使用時，SignalR 會使用其他可用的傳輸，如[SignalR 簡介主題](index.md)的傳輸一節中所述）。

若要深入瞭解更先進的 SignalR 開發概念，請造訪下列網站以取得 SignalR 原始程式碼和資源：

- [SignalR 專案](http://signalr.net)
- [SignalR Github 和範例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
