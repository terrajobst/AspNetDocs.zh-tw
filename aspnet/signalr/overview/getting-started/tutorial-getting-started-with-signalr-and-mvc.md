---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
title: 教學課程：與 SignalR 2 和 MVC 5 即時聊天 |Microsoft Docs
author: bradygaster
description: 本教學課程說明如何使用 ASP.NET SignalR 2 來建立即時聊天應用程式。 您會將 SignalR 新增至 MVC 5 應用程式。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: 80bfe5fb-bdfc-41fe-ac43-2132e5d69fac
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr-and-mvc
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: 5671e4f0123ca2b0cb5314336cf4411467feac70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78537041"
---
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a>教學課程：使用 SignalR 2 和 MVC 5 進行即時聊天

本教學課程說明如何使用 ASP.NET SignalR 2 來建立即時聊天應用程式。 您會將 SignalR 新增至 MVC 5 應用程式，並建立聊天視圖來傳送和顯示訊息。

在本教學課程中，您已：

> [!div class="checklist"]
> * 設定專案
> * 執行範例
> * 檢查程式碼

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a>Prerequisites

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)，其中包含 **ASP.NET 和 Web 部署**工作負載。

## <a name="set-up-the-project"></a>設定專案

本節說明如何使用 Visual Studio 2017 和 SignalR 2 來建立空白的 ASP.NET MVC 5 應用程式、新增 SignalR 程式庫，以及建立聊天應用程式。

1. 在 Visual Studio 中，建立C#以 .NET Framework 4.5 為目標的 ASP.NET 應用程式，並將其命名為 SignalRChat，然後按一下 [確定]。

    ![建立 web](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. 在 [**新增 ASP.NET Web 應用程式-SignalRMvcChat**] 中，選取 [ **MVC** ]，然後選取 [**變更驗證**]。

1. 在 [**變更驗證**] 中，選取 [**無驗證**]，然後按一下 **[確定]** 。

    ![選取 [無驗證]](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. 在 [**新增 ASP.NET Web 應用程式-SignalRMvcChat**] 中，選取 **[確定]** 。

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。

1. 在 **[加入新專案-SignalRChat**] 中，選取 [**已安裝**] >  **C# Visual** > **Web** > **SignalR** ，然後選取 **[SignalR 中樞類別（v2）** ]。

1. 將類別命名為*ChatHub* ，並將它加入至專案。

    此步驟會建立*ChatHub.cs*類別檔案，並將支援 SignalR 的一組腳本檔案和元件參考加入至專案。

1. 將新的*ChatHub.cs*類別檔案中的程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. 在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **類別**]。

1. 將新類別命名為*Startup* ，並將其新增至專案。

1. 將*Startup.cs*類別檔案中的程式碼取代為下列程式碼：

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. 在**方案總管**中，選取 [**控制器** > **HomeController.cs**]。

1. 將此方法新增至*HomeController.cs*。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    這個方法會傳回您在稍後步驟中建立的**聊天**視圖。

1. 在**方案總管**中，以滑鼠右鍵按一下  **Views**  > **Home**，然後選取 **新增** >  **視圖**。

1. 在 [新增**視圖**] 中，將新的觀看**交談**命名為，**然後選取 [新增]** 。

1. 將**Chat**的內容取代為下列程式碼：

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. 在**方案總管**中，展開 [**腳本**]。

    JQuery 和 SignalR 的腳本程式庫會顯示在專案中。

    > [!IMPORTANT]
    > 封裝管理員可能已安裝較新版本的 SignalR 腳本。

1. 檢查程式碼區塊中的腳本參考是否對應到專案中的腳本檔案版本。

    來自原始程式碼區塊的腳本參考：

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. 如果兩者不相符，請更新*cshtml*檔案。

1. 從功能表列中 **，選取 [** 檔案] > [**全部儲存**]。

## <a name="run-the-sample"></a>執行範例

1. 在工具列中，開啟 [**腳本調試**]，然後選取 [播放] 按鈕，以在 Debug 模式中執行範例。

    ![輸入使用者名稱](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. 當瀏覽器開啟時，輸入聊天識別的名稱。

1. 從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到網址列中。

1. 在每個瀏覽器中，輸入唯一的名稱。

1. 現在，新增批註，然後選取 [**傳送**]。 在其他瀏覽器中重複此動作。 批註會即時出現。

    > [!NOTE]
    > 這個簡單的聊天應用程式不會維護伺服器上的討論內容。 中樞會將批註廣播給所有目前的使用者。 稍後加入交談的使用者會看到從他們加入的時間新增的訊息。

    瞭解聊天應用程式如何在三個不同的瀏覽器中執行。 當 Tom、Anand 和 Susan 傳送訊息時，所有瀏覽器都會即時更新：

    ![這三個瀏覽器都會顯示相同的聊天記錄](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. 在**方案總管**中，檢查執行中應用程式的 [**指令檔**] 節點。 有一個名為*hub*的腳本檔案，SignalR 程式庫會在執行時間產生此檔案。 這個檔案會管理 jQuery 腳本與伺服器端程式碼之間的通訊。

    ![[指令檔] 節點中自動產生的中樞腳本](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a>檢查程式碼

SignalR chat 應用程式會示範兩個基本的 SignalR 開發工作。 它會說明如何建立中樞。 伺服器會使用該中樞作為主要的協調物件。 中樞會使用 SignalR jQuery 程式庫來傳送和接收訊息。

### <a name="signalr-hubs-in-the-chathubcs"></a>ChatHub.cs 中的 SignalR 中樞

在程式碼範例中，`ChatHub` 類別衍生自 `Microsoft.AspNet.SignalR.Hub` 類別。 衍生自 `Hub` 類別是建立 SignalR 應用程式的實用方式。 您可以在中樞類別上建立公用方法，然後從網頁中的腳本呼叫這些方法來存取這些方法。

在聊天程式碼中，用戶端會呼叫 `ChatHub.Send` 方法，以傳送新的訊息。 接著，中樞會藉由呼叫 `Clients.All.addNewMessageToPage`，將訊息傳送至所有用戶端。

`Send` 方法會示範數個中樞概念：

* 在中樞上宣告公用方法，讓用戶端可以呼叫它們。

* 使用 `Microsoft.AspNet.SignalR.Hub.Clients` 動態屬性，與連線至此中樞的所有用戶端進行通訊。

* 呼叫用戶端上的函式（例如 `addNewMessageToPage` 函數）來更新用戶端。

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a>SignalR 和 jQuery 聊天. cshtml

程式碼範例中的*Chat*視圖檔示範如何使用 SignalR jQuery 程式庫與 SignalR 中樞進行通訊。  程式碼會執行許多重要的工作。 它會為中樞建立自動產生的 proxy 參考、宣告一個函式，讓伺服器可以呼叫它來將內容推送至用戶端，並啟動連線以將訊息傳送至中樞。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> 在 JavaScript 中，伺服器類別及其成員的參考是在 camelCase 中。 此程式碼範例會C#將 JavaScript 中的 `ChatHub` 類別當做 `chatHub`參考。

在此程式碼區塊中，您會在腳本中建立回呼函數。

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

伺服器上的中樞類別會呼叫此函式，將內容更新推送至每個用戶端。 `htmlEncode` 函式的選擇性呼叫會顯示在頁面中顯示訊息內容之前，對其進行 HTML 編碼的方式。 這是防止腳本插入的方式。

此程式碼會開啟與中樞的連接。

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> 這種方法可確保您在事件處理常式執行之前建立連接。

程式碼會啟動連線，然後將函式傳遞至聊天頁面中 [**傳送**] 按鈕上的 [按一下] 事件。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a>其他資源

如需 SignalR 的詳細資訊，請參閱下列資源：

* [SignalR 專案](http://signalr.net)

* [SignalR GitHub 和範例](https://github.com/SignalR/SignalR)

* [SignalR Wiki](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 設定專案
> * 執行範例
> * 檢查程式碼

前往下一篇文章，以瞭解如何建立使用 ASP.NET SignalR 2 的 web 應用程式，以提供高頻率的訊息功能。
> [!div class="nextstepaction"]
> [具有高頻率訊息的 Web 應用程式](tutorial-high-frequency-realtime-with-signalr.md)