---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 教學課程：與 SignalR 2 的即時聊天 |Microsoft Docs
author: bradygaster
description: 此教學課程會示範如何使用 SignalR 建立即時聊天應用程式。 您會將 SignalR 新增至空白的 ASP.NET web 應用程式。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: bc4ef190b6e36812b6fe7ca4e16eb763431e0e82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536978"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a>教學課程：與 SignalR 的即時交談2

本教學課程說明如何使用 SignalR 來建立即時聊天應用程式。 您會將 SignalR 新增至空白的 ASP.NET web 應用程式，並建立可傳送和顯示訊息的 HTML 頁面。

在本教學課程中，您已：

> [!div class="checklist"]
> * 設定專案
> * 執行範例
> * 檢查程式碼

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Prerequisites

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)，其中包含 **ASP.NET 和 Web 部署**工作負載。

## <a name="set-up-the-project"></a>設定專案

本節說明如何使用 Visual Studio 2017 和 SignalR 2 來建立空的 ASP.NET web 應用程式、新增 SignalR，以及建立聊天應用程式。

1. 在 Visual Studio 中，建立 ASP.NET Web 應用程式。

    ![建立 web](tutorial-getting-started-with-signalr/_static/image2.png)

1. 在 [**新增 ASP.NET 專案-SignalRChat** ] 視窗中，保持選取 [**空白**]，然後選取 **[確定]** 。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。

1. 在 **[加入新專案-SignalRChat**] 中，選取 [**已安裝**] >  **C# Visual** > **Web** > **SignalR** ，然後選取 **[SignalR 中樞類別（v2）** ]。

1. 將類別命名為*ChatHub* ，並將它加入至專案。

    此步驟會建立*ChatHub.cs*類別檔案，並將支援 SignalR 的一組腳本檔案和元件參考加入至專案。

1. 將新的*ChatHub.cs*類別檔案中的程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。

1. 在 [**加入新專案-SignalRChat** ] 中，選取 [**已安裝** > **Visual C#**  > **Web** ]，然後選取 [ **OWIN 啟動類別**]。

1. 將類別命名為*Startup* ，並將它加入至專案。

1. 將*Startup*類別中的預設程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **HTML 網頁**]。

1. 將新的頁面*索引*命名為，然後選取 **[確定]** 。

1. 在**方案總管**中，以滑鼠右鍵按一下您所建立的 HTML 網頁，然後選取 [**設定為起始頁**]。

1. 將 HTML 網頁中的預設程式碼取代為下列程式碼：

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. 在**方案總管**中，展開 [**腳本**]。

    JQuery 和 SignalR 的腳本程式庫會顯示在專案中。

    > [!IMPORTANT]
    > 封裝管理員可能已安裝較新版本的 SignalR 腳本。

1. 檢查程式碼區塊中的腳本參考是否對應到專案中的腳本檔案版本。

    來自原始程式碼區塊的腳本參考：

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. 如果兩者不相符，請更新 *.html*檔案。

1. 從功能表列中 **，選取 [** 檔案] > [**全部儲存**]。

## <a name="run-the-sample"></a>執行範例

1. 在工具列中，開啟 [**腳本調試**]，然後選取 [播放] 按鈕，以在 Debug 模式中執行範例。

    ![輸入使用者名稱](tutorial-getting-started-with-signalr/_static/image3.png)

1. 當瀏覽器開啟時，輸入聊天識別的名稱。

1. 從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到網址列中。

1. 在每個瀏覽器中，輸入唯一的名稱。

1. 現在，新增批註，然後選取 [**傳送**]。 在其他瀏覽器中重複此動作。 批註會即時出現。

    > [!NOTE]
    > 這個簡單的聊天應用程式不會維護伺服器上的討論內容。 中樞會將批註廣播給所有目前的使用者。 稍後加入交談的使用者會看到從他們加入的時間新增的訊息。

    瞭解聊天應用程式如何在三個不同的瀏覽器中執行。 當 Tom、Anand 和 Susan 傳送訊息時，所有瀏覽器都會即時更新：

    ![這三個瀏覽器都會顯示相同的聊天記錄](tutorial-getting-started-with-signalr/_static/image4.png)

1. 在**方案總管**中，檢查執行中應用程式的 [**指令檔**] 節點。 有一個名為*hub*的腳本檔案，SignalR 程式庫會在執行時間產生此檔案。 這個檔案會管理 jQuery 腳本與伺服器端程式碼之間的通訊。

    ![[指令檔] 節點中自動產生的中樞腳本](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a>檢查程式碼

SignalRChat 應用程式會示範兩個基本的 SignalR 開發工作。 它會說明如何建立中樞。 伺服器會使用該中樞作為主要的協調物件。 中樞會使用 SignalR jQuery 程式庫來傳送和接收訊息。

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs 中的 SignalR 中樞

在上述程式碼範例中，`ChatHub` 類別衍生自 `Microsoft.AspNet.SignalR.Hub` 類別。 衍生自 `Hub` 類別是建立 SignalR 應用程式的實用方式。 您可以在中樞類別上建立公用方法，然後在網頁的腳本中呼叫這些方法，藉此使用它們。

在聊天程式碼中，用戶端會呼叫 `ChatHub.Send` 方法，以傳送新的訊息。 然後，中樞會藉由呼叫 `Clients.All.broadcastMessage`，將訊息傳送至所有用戶端。

`Send` 方法會示範數個中樞概念：

* 在中樞上宣告公用方法，讓用戶端可以呼叫它們。

* 使用 `Microsoft.AspNet.SignalR.Hub.Clients` 動態屬性，與連線至此中樞的所有用戶端進行通訊。

* 呼叫用戶端上的函式（例如 `broadcastMessage` 函數）來更新用戶端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a>SignalR 和 jQuery 中的索引 .html

程式碼範例中的 [ *.html* ] 頁面會顯示如何使用 SignalR jQuery 程式庫與 SignalR 中樞進行通訊。 程式碼會執行許多重要的工作。 它會宣告一個 proxy 來參考中樞、宣告一個函式，讓伺服器可以呼叫它來將內容推送至用戶端，並啟動連線以將訊息傳送至中樞。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> 在 JavaScript 中，伺服器類別及其成員的參考必須是 camelCase。 程式碼範例會將C# JavaScript 中的*ChatHub*類別參考為 `chatHub`。

在此程式碼區塊中，您會在腳本中建立回呼函數。

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

伺服器上的中樞類別會呼叫此函式，將內容更新推送至每個用戶端。 在顯示內容之前進行 HTML 編碼的兩行程式碼是選擇性的，並顯示可防止腳本插入的好方法。

此程式碼會開啟與中樞的連接。

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> 這種方法可確保程式碼會在事件處理常式執行之前建立連接。

程式碼會啟動連接，然後將函式傳遞給它，以處理 HTML 網頁中 [**傳送**] 按鈕上的 click 事件。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a>其他資源

如需 SignalR 的詳細資訊，請參閱下列資源：

* [SignalR 專案](http://signalr.net)

* [SignalR Github 和範例](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您將：

> [!div class="checklist"]
> * 設定專案
> * 執行範例
> * 檢查程式碼

前進到下一篇文章，以瞭解如何使用 SignalR 和 MVC 5。
> [!div class="nextstepaction"]
> [SignalR 2 和 MVC 5](tutorial-getting-started-with-signalr-and-mvc.md)