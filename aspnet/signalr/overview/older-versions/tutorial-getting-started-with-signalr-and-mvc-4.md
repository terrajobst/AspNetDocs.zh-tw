---
uid: signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
title: 教學課程：使用 SignalR 1.x 和 MVC 4 的消費者入門 |Microsoft Docs
author: bradygaster
description: 使用 ASP.NET SignalR 和 ASP.NET MVC 4 來建立即時聊天應用程式。
ms.author: bradyg
ms.date: 03/29/2013
ms.assetid: eeef9f73-6de3-49f9-b50b-9af22108f2ce
msc.legacyurl: /signalr/overview/older-versions/tutorial-getting-started-with-signalr-and-mvc-4
msc.type: authoredcontent
ms.openlocfilehash: 9186915df6d5de6bc20dfc0adabc54056d2f3a8c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579566"
---
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a>教學課程：使用 SignalR 1.x 和 MVC 4 消費者入門

[Fletcher](https://github.com/pfletcher)的[Tim Teebken](https://github.com/timlt)

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> 本教學課程說明如何使用 ASP.NET SignalR 來建立即時聊天應用程式。 您會將 SignalR 新增至 MVC 4 應用程式，並建立聊天視圖來傳送和顯示訊息。

## <a name="overview"></a>概觀

本教學課程將為您介紹如何使用 ASP.NET SignalR 和 ASP.NET MVC 4 進行即時 web 應用程式開發。 本教學課程使用與[SignalR 消費者入門教學](tutorial-getting-started-with-signalr.md)課程相同的聊天應用程式代碼，但會示範如何將它新增至以網際網路範本為基礎的 MVC 4 應用程式。

在本主題中，您將瞭解下列 SignalR 開發工作：

- 將 SignalR 程式庫新增至 MVC 4 應用程式。
- 建立中樞類別以將內容推送至用戶端。
- 使用網頁中的 SignalR jQuery 程式庫來傳送訊息，並從中樞顯示更新。

下列螢幕擷取畫面顯示在瀏覽器中執行的已完成聊天應用程式。

![聊天實例](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

各節

- [設定專案](#setup)
- [執行範例](#run)
- [檢查程式碼](#code)
- [後續步驟](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a>設定專案

必要條件：

- Visual Studio 2010 SP1、Visual Studio 2012 或 Visual Studio 2012 Express。 如果您沒有 Visual Studio，請參閱[ASP.NET 下載](https://www.asp.net/downloads)以取得免費的 Visual Studio 2012 Express 開發工具。
- 針對 Visual Studio 2010，請安裝[ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)。

本節說明如何建立 ASP.NET MVC 4 應用程式、新增 SignalR 程式庫，以及建立聊天應用程式。

1. 1. 在 Visual Studio 建立 ASP.NET MVC 4 應用程式，將其命名為 SignalRChat，然後按一下 [確定]。

        > [!NOTE]
        > 在 VS 2010 中，選取 [Framework 版本] 下拉式控制項中的 [ **.NET Framework 4** ]。 SignalR 程式碼會在 .NET Framework 版本4和4.5 上執行。

        ![建立 mvc web](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. 選取 [網際網路應用程式] 範本，清除 [**建立單元測試專案**] 選項，然後按一下 [確定]。

         ![建立 mvc 網際網路網站](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. 開啟 [**工具] > NuGet 套件管理員 > [套件管理員主控台**]，然後執行下列命令。 此步驟會將一組腳本檔案和元件參考加入至專案，以啟用 SignalR 功能。

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. 在**方案總管**展開 [腳本] 資料夾。 請注意，SignalR 的腳本程式庫已加入至專案。

         ![程式庫參考](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增] |新增資料夾**，然後新增名為**hub**的新資料夾。
      6. 以滑鼠右鍵按一下 [**中樞**] 資料夾，然後按一下 [**新增] |類別**，並建立名為C# **ChatHub.cs**的新類別。 您將使用此類別做為 SignalR 伺服器中樞，以將訊息傳送至所有用戶端。

> [!NOTE]
> 如果您使用 Visual Studio 2012，並已安裝[ASP.NET 和 Web 工具2012.2 更新](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)，您可以使用 [新增 SignalR 專案] 範本來建立中樞類別。 若要這麼做，請以滑鼠右鍵按一下 **中樞** 資料夾，然後按一下 **新增 |新增專案**，選取  **SignalR Hub Class （v1）** ，並將類別命名為**ChatHub.cs**。

1. 將**ChatHub**類別中的程式碼取代為下列程式碼。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. 開啟專案的**global.asax**檔案，並將呼叫新增至方法 `RouteTable.Routes.MapHubs();` 做為 `Application_Start` 方法中的第一行程式碼。 此程式碼會註冊 SignalR 中樞的預設路由，而且必須在註冊任何其他路由之前呼叫。 完成的 `Application_Start` 方法如下列範例所示。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. 編輯在 controller **/HomeController**中找到的 `HomeController` 類別，並將下列方法新增至類別。 這個方法會傳回您將在稍後步驟中建立的**聊天**視圖。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. 以滑鼠右鍵按一下您剛才建立的 `Chat` 方法，然後按一下 [**新增視圖**] 以建立新的視圖檔案。
5. 在 [**加入視圖**] 對話方塊中，確定已選取核取方塊以**使用版面配置或主版頁面**（清除其他核取方塊），然後按一下 [**新增**]。

    ![新增檢視](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. 編輯名為**Chat**的新視圖檔案。 在 &lt;h2&gt; 標記之後，將下列 &lt;div&gt; 區段和 `@section scripts` 程式碼區塊貼到頁面中。 此腳本可讓頁面傳送聊天訊息，並顯示來自伺服器的訊息。 聊天視圖的完整程式碼會出現在下列程式碼區塊中。

    > [!IMPORTANT]
    > 當您將 SignalR 和其他腳本程式庫加入 Visual Studio 專案時，封裝管理員可能會安裝比本主題中所示版本還新的腳本版本。 請確定程式碼中的腳本參考，符合您的專案中所安裝的腳本程式庫版本。

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. **全部儲存**專案。

<a id="run"></a>

## <a name="run-the-sample"></a>執行範例

1. 按 F5 以在 [調試] 模式中執行專案。
2. 在瀏覽器位址行中，將 **/home/chat**附加至專案的預設頁面 URL。 聊天頁面會在瀏覽器實例中載入，並提示您輸入使用者名稱。

    ![輸入使用者名稱](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. 輸入使用者稱。
4. 從瀏覽器的位址行複製 URL，並用它來開啟兩個以上的瀏覽器實例。 在每個瀏覽器實例中，輸入唯一的使用者名稱。
5. 在每個瀏覽器實例中新增批註，然後按一下 [**傳送**]。 批註應該會顯示在所有瀏覽器實例中。

    > [!NOTE]
    > 這個簡單的聊天應用程式不會維護伺服器上的討論內容。 中樞會將批註廣播給所有目前的使用者。 稍後加入交談的使用者會看到從他們加入的時間新增的訊息。
6. 下列螢幕擷取畫面顯示在瀏覽器中執行的聊天應用程式。

    ![聊天瀏覽器](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. 在**方案總管**中，檢查執行中應用程式的 [**指令檔**] 節點。 如果您使用 Internet Explorer 作為瀏覽器，此節點會顯示在 [偵錯工具] 模式中。 有一個名為**hub**的腳本檔案，SignalR 程式庫會在執行時間動態產生此檔案。 這個檔案會管理 jQuery 腳本與伺服器端程式碼之間的通訊。 如果您使用 Internet Explorer 以外的瀏覽器，您也可以直接流覽至動態**中樞**檔案（例如 http://mywebsite/signalr/hubs）來存取該檔案。

    ![產生的中樞腳本](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a>檢查程式碼

SignalR chat 應用程式會示範兩個基本的 SignalR 開發工作：建立中樞做為伺服器上的主要協調物件，以及使用 SignalR jQuery 程式庫來傳送和接收訊息。

### <a name="signalr-hubs"></a>SignalR 中樞

在程式碼範例中， **ChatHub**類別衍生自**SignalR**類別。 從**中樞**類別衍生的是建立 SignalR 應用程式的實用方式。 您可以在中樞類別上建立公用方法，然後從網頁中的 jQuery 腳本呼叫這些方法來存取這些方法。

在聊天程式碼中，用戶端會呼叫**ChatHub** ，以傳送新的訊息。 接著，中樞會藉由呼叫**addNewMessageToPage**，將訊息傳送至所有用戶端。

**Send**方法會示範數個中樞概念：

- 在中樞上宣告公用方法，讓用戶端可以呼叫它們。
- 使用**SignalR**來存取連線到此中樞的所有用戶端。
- 呼叫用戶端上的 jQuery 函式（例如 `addNewMessageToPage` 函數）來更新用戶端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a>SignalR 和 jQuery

程式碼範例中的**Chat**視圖檔示範如何使用 SignalR jQuery 程式庫與 SignalR 中樞進行通訊。 程式碼中的必要工作是建立中樞自動產生的 proxy 參考、宣告伺服器可以呼叫的函式以將內容推送至用戶端，以及啟動連線以將訊息傳送至中樞。

下列程式碼會宣告中樞的 proxy。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> 在 jQuery 中，伺服器類別及其成員的參考是 camel 大小寫。 此程式碼範例會C#將 jQuery 中的**ChatHub**類別參考為**ChatHub**。 如果您想要使用傳統 Pascal 大小寫來參考 jQuery 中的 `ChatHub` 類別C#，請編輯 ChatHub.cs 類別檔案。 加入 `using` 語句，以參考 `Microsoft.AspNet.SignalR.Hubs` 命名空間。 然後將 `HubName` 屬性加入 `ChatHub` 類別，例如 `[HubName("ChatHub")]`。 最後，將您的 jQuery 參考更新為 `ChatHub` 類別。

下列程式碼示範如何在腳本中建立回呼函數。 伺服器上的中樞類別會呼叫此函式，將內容更新推送至每個用戶端。 `htmlEncode` 函式的選擇性呼叫會顯示在頁面中顯示訊息內容的 HTML 編碼方式，以防止腳本插入。

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

下列程式碼顯示如何開啟與中樞的連線。 程式碼會啟動連線，然後將函式傳遞至聊天頁面中 [**傳送**] 按鈕上的 [按一下] 事件。

> [!NOTE]
> 這種方法可確保在事件處理常式執行之前就已建立連接。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a>後續步驟

您已瞭解 SignalR 是用來建立即時 web 應用程式的架構。 您也學到幾個 SignalR 的開發工作：如何將 SignalR 新增至 ASP.NET 應用程式、如何建立中樞類別，以及如何從中樞傳送和接收訊息。

若要深入瞭解更先進的 SignalR 開發概念，請造訪下列網站以取得 SignalR 原始程式碼和資源：

- [SignalR 專案](http://signalr.net)
- [SignalR Github 和範例](https://github.com/SignalR/SignalR)
- [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)
