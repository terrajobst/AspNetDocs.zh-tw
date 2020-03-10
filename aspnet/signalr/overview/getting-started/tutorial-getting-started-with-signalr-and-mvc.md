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
# <a name="tutorial-real-time-chat-with-signalr-2-and-mvc-5"></a><span data-ttu-id="45018-104">教學課程：使用 SignalR 2 和 MVC 5 進行即時聊天</span><span class="sxs-lookup"><span data-stu-id="45018-104">Tutorial: Real-time chat with SignalR 2 and MVC 5</span></span>

<span data-ttu-id="45018-105">本教學課程說明如何使用 ASP.NET SignalR 2 來建立即時聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="45018-105">This tutorial shows how to use ASP.NET SignalR 2 to create a real-time chat application.</span></span> <span data-ttu-id="45018-106">您會將 SignalR 新增至 MVC 5 應用程式，並建立聊天視圖來傳送和顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="45018-106">You add SignalR to an MVC 5 application and create a chat view to send and display messages.</span></span>

<span data-ttu-id="45018-107">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="45018-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45018-108">設定專案</span><span class="sxs-lookup"><span data-stu-id="45018-108">Set up the project</span></span>
> * <span data-ttu-id="45018-109">執行範例</span><span class="sxs-lookup"><span data-stu-id="45018-109">Run the sample</span></span>
> * <span data-ttu-id="45018-110">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="45018-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="45018-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="45018-111">Prerequisites</span></span>

* <span data-ttu-id="45018-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)，其中包含 **ASP.NET 和 Web 部署**工作負載。</span><span class="sxs-lookup"><span data-stu-id="45018-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="45018-113">設定專案</span><span class="sxs-lookup"><span data-stu-id="45018-113">Set up the Project</span></span>

<span data-ttu-id="45018-114">本節說明如何使用 Visual Studio 2017 和 SignalR 2 來建立空白的 ASP.NET MVC 5 應用程式、新增 SignalR 程式庫，以及建立聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="45018-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET MVC 5 application, add the SignalR library, and create the chat application.</span></span>

1. <span data-ttu-id="45018-115">在 Visual Studio 中，建立C#以 .NET Framework 4.5 為目標的 ASP.NET 應用程式，並將其命名為 SignalRChat，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="45018-115">In Visual Studio, create a C# ASP.NET application that targets .NET Framework 4.5, name it SignalRChat, and click OK.</span></span>

    ![建立 web](tutorial-getting-started-with-signalr-and-mvc/_static/image1.png)

1. <span data-ttu-id="45018-117">在 [**新增 ASP.NET Web 應用程式-SignalRMvcChat**] 中，選取 [ **MVC** ]，然後選取 [**變更驗證**]。</span><span class="sxs-lookup"><span data-stu-id="45018-117">In **New ASP.NET Web Application - SignalRMvcChat**, select **MVC** and then select **Change Authentication**.</span></span>

1. <span data-ttu-id="45018-118">在 [**變更驗證**] 中，選取 [**無驗證**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="45018-118">In **Change Authentication**, select **No Authentication** and click **OK**.</span></span>

    ![選取 [無驗證]](tutorial-getting-started-with-signalr-and-mvc/_static/image2.png)

1. <span data-ttu-id="45018-120">在 [**新增 ASP.NET Web 應用程式-SignalRMvcChat**] 中，選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="45018-120">In **New ASP.NET Web Application - SignalRMvcChat**, select **OK**.</span></span>

1. <span data-ttu-id="45018-121">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="45018-121">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="45018-122">在 **[加入新專案-SignalRChat**] 中，選取 [**已安裝**] >  **C# Visual** > **Web** > **SignalR** ，然後選取 **[SignalR 中樞類別（v2）** ]。</span><span class="sxs-lookup"><span data-stu-id="45018-122">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="45018-123">將類別命名為*ChatHub* ，並將它加入至專案。</span><span class="sxs-lookup"><span data-stu-id="45018-123">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="45018-124">此步驟會建立*ChatHub.cs*類別檔案，並將支援 SignalR 的一組腳本檔案和元件參考加入至專案。</span><span class="sxs-lookup"><span data-stu-id="45018-124">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="45018-125">將新的*ChatHub.cs*類別檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="45018-125">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample1.cs)]

1. <span data-ttu-id="45018-126">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **類別**]。</span><span class="sxs-lookup"><span data-stu-id="45018-126">In **Solution Explorer**, right-click the project and select **Add** > **Class**.</span></span>

1. <span data-ttu-id="45018-127">將新類別命名為*Startup* ，並將其新增至專案。</span><span class="sxs-lookup"><span data-stu-id="45018-127">Name the new class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="45018-128">將*Startup.cs*類別檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="45018-128">Replace the code in the *Startup.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample2.cs)]

1. <span data-ttu-id="45018-129">在**方案總管**中，選取 [**控制器** > **HomeController.cs**]。</span><span class="sxs-lookup"><span data-stu-id="45018-129">In **Solution Explorer**, select **Controllers** > **HomeController.cs**.</span></span>

1. <span data-ttu-id="45018-130">將此方法新增至*HomeController.cs*。</span><span class="sxs-lookup"><span data-stu-id="45018-130">Add this method to the *HomeController.cs*.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample3.cs)]

    <span data-ttu-id="45018-131">這個方法會傳回您在稍後步驟中建立的**聊天**視圖。</span><span class="sxs-lookup"><span data-stu-id="45018-131">This method returns the **Chat** view that you create in a later step.</span></span>

1. <span data-ttu-id="45018-132">在**方案總管**中，以滑鼠右鍵按一下  **Views**  > **Home**，然後選取 **新增** >  **視圖**。</span><span class="sxs-lookup"><span data-stu-id="45018-132">In **Solution Explorer**, right-click **Views** > **Home**, and select **Add** >  **View**.</span></span>

1. <span data-ttu-id="45018-133">在 [新增**視圖**] 中，將新的觀看**交談**命名為，**然後選取 [新增]** 。</span><span class="sxs-lookup"><span data-stu-id="45018-133">In **Add View**, name the new view **Chat** and select **Add**.</span></span>

1. <span data-ttu-id="45018-134">將**Chat**的內容取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="45018-134">Replace the contents of **Chat.cshtml** with this code:</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample4.cshtml)]

1. <span data-ttu-id="45018-135">在**方案總管**中，展開 [**腳本**]。</span><span class="sxs-lookup"><span data-stu-id="45018-135">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="45018-136">JQuery 和 SignalR 的腳本程式庫會顯示在專案中。</span><span class="sxs-lookup"><span data-stu-id="45018-136">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="45018-137">封裝管理員可能已安裝較新版本的 SignalR 腳本。</span><span class="sxs-lookup"><span data-stu-id="45018-137">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="45018-138">檢查程式碼區塊中的腳本參考是否對應到專案中的腳本檔案版本。</span><span class="sxs-lookup"><span data-stu-id="45018-138">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="45018-139">來自原始程式碼區塊的腳本參考：</span><span class="sxs-lookup"><span data-stu-id="45018-139">Script references from the original code block:</span></span>

    ```cshtml
    <!--Script references. -->
    <!--The jQuery library is required and is referenced by default in _Layout.cshtml. -->
    <!--Reference the SignalR library. -->
    <script src="~/Scripts/jquery.signalR-2.1.0.min.js"></script>
    ```

1. <span data-ttu-id="45018-140">如果兩者不相符，請更新*cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="45018-140">If they don't match, update the *.cshtml* file.</span></span>

1. <span data-ttu-id="45018-141">從功能表列中 **，選取 [** 檔案] > [**全部儲存**]。</span><span class="sxs-lookup"><span data-stu-id="45018-141">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="45018-142">執行範例</span><span class="sxs-lookup"><span data-stu-id="45018-142">Run the Sample</span></span>

1. <span data-ttu-id="45018-143">在工具列中，開啟 [**腳本調試**]，然後選取 [播放] 按鈕，以在 Debug 模式中執行範例。</span><span class="sxs-lookup"><span data-stu-id="45018-143">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![輸入使用者名稱](tutorial-getting-started-with-signalr-and-mvc/_static/image3.png)

1. <span data-ttu-id="45018-145">當瀏覽器開啟時，輸入聊天識別的名稱。</span><span class="sxs-lookup"><span data-stu-id="45018-145">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="45018-146">從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到網址列中。</span><span class="sxs-lookup"><span data-stu-id="45018-146">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="45018-147">在每個瀏覽器中，輸入唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="45018-147">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="45018-148">現在，新增批註，然後選取 [**傳送**]。</span><span class="sxs-lookup"><span data-stu-id="45018-148">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="45018-149">在其他瀏覽器中重複此動作。</span><span class="sxs-lookup"><span data-stu-id="45018-149">Repeat that in the other browsers.</span></span> <span data-ttu-id="45018-150">批註會即時出現。</span><span class="sxs-lookup"><span data-stu-id="45018-150">The comments appear in real time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="45018-151">這個簡單的聊天應用程式不會維護伺服器上的討論內容。</span><span class="sxs-lookup"><span data-stu-id="45018-151">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="45018-152">中樞會將批註廣播給所有目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="45018-152">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="45018-153">稍後加入交談的使用者會看到從他們加入的時間新增的訊息。</span><span class="sxs-lookup"><span data-stu-id="45018-153">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="45018-154">瞭解聊天應用程式如何在三個不同的瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="45018-154">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="45018-155">當 Tom、Anand 和 Susan 傳送訊息時，所有瀏覽器都會即時更新：</span><span class="sxs-lookup"><span data-stu-id="45018-155">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![這三個瀏覽器都會顯示相同的聊天記錄](tutorial-getting-started-with-signalr-and-mvc/_static/image4.png)

1. <span data-ttu-id="45018-157">在**方案總管**中，檢查執行中應用程式的 [**指令檔**] 節點。</span><span class="sxs-lookup"><span data-stu-id="45018-157">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="45018-158">有一個名為*hub*的腳本檔案，SignalR 程式庫會在執行時間產生此檔案。</span><span class="sxs-lookup"><span data-stu-id="45018-158">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="45018-159">這個檔案會管理 jQuery 腳本與伺服器端程式碼之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="45018-159">This file manages the communication between jQuery script and server-side code.</span></span>

    ![[指令檔] 節點中自動產生的中樞腳本](tutorial-getting-started-with-signalr-and-mvc/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="45018-161">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="45018-161">Examine the Code</span></span>

<span data-ttu-id="45018-162">SignalR chat 應用程式會示範兩個基本的 SignalR 開發工作。</span><span class="sxs-lookup"><span data-stu-id="45018-162">The SignalR chat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="45018-163">它會說明如何建立中樞。</span><span class="sxs-lookup"><span data-stu-id="45018-163">It shows you how to create a hub.</span></span> <span data-ttu-id="45018-164">伺服器會使用該中樞作為主要的協調物件。</span><span class="sxs-lookup"><span data-stu-id="45018-164">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="45018-165">中樞會使用 SignalR jQuery 程式庫來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="45018-165">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="45018-166">ChatHub.cs 中的 SignalR 中樞</span><span class="sxs-lookup"><span data-stu-id="45018-166">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="45018-167">在程式碼範例中，`ChatHub` 類別衍生自 `Microsoft.AspNet.SignalR.Hub` 類別。</span><span class="sxs-lookup"><span data-stu-id="45018-167">In the code sample, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="45018-168">衍生自 `Hub` 類別是建立 SignalR 應用程式的實用方式。</span><span class="sxs-lookup"><span data-stu-id="45018-168">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="45018-169">您可以在中樞類別上建立公用方法，然後從網頁中的腳本呼叫這些方法來存取這些方法。</span><span class="sxs-lookup"><span data-stu-id="45018-169">You can create public methods on your hub class and then access those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="45018-170">在聊天程式碼中，用戶端會呼叫 `ChatHub.Send` 方法，以傳送新的訊息。</span><span class="sxs-lookup"><span data-stu-id="45018-170">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="45018-171">接著，中樞會藉由呼叫 `Clients.All.addNewMessageToPage`，將訊息傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="45018-171">The hub in turn sends the message to all clients by calling `Clients.All.addNewMessageToPage`.</span></span>

<span data-ttu-id="45018-172">`Send` 方法會示範數個中樞概念：</span><span class="sxs-lookup"><span data-stu-id="45018-172">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="45018-173">在中樞上宣告公用方法，讓用戶端可以呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="45018-173">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="45018-174">使用 `Microsoft.AspNet.SignalR.Hub.Clients` 動態屬性，與連線至此中樞的所有用戶端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="45018-174">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="45018-175">呼叫用戶端上的函式（例如 `addNewMessageToPage` 函數）來更新用戶端。</span><span class="sxs-lookup"><span data-stu-id="45018-175">Call a function on the client (like the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample5.cs)]

### <a name="signalr-and-jquery-chatcshtml"></a><span data-ttu-id="45018-176">SignalR 和 jQuery 聊天. cshtml</span><span class="sxs-lookup"><span data-stu-id="45018-176">SignalR and jQuery Chat.cshtml</span></span>

<span data-ttu-id="45018-177">程式碼範例中的*Chat*視圖檔示範如何使用 SignalR jQuery 程式庫與 SignalR 中樞進行通訊。</span><span class="sxs-lookup"><span data-stu-id="45018-177">The *Chat.cshtml* view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span>  <span data-ttu-id="45018-178">程式碼會執行許多重要的工作。</span><span class="sxs-lookup"><span data-stu-id="45018-178">The code carries out many important tasks.</span></span> <span data-ttu-id="45018-179">它會為中樞建立自動產生的 proxy 參考、宣告一個函式，讓伺服器可以呼叫它來將內容推送至用戶端，並啟動連線以將訊息傳送至中樞。</span><span class="sxs-lookup"><span data-stu-id="45018-179">It creates a reference to the autogenerated proxy for the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="45018-180">在 JavaScript 中，伺服器類別及其成員的參考是在 camelCase 中。</span><span class="sxs-lookup"><span data-stu-id="45018-180">In JavaScript, the reference to the server class and its members is in camelCase.</span></span> <span data-ttu-id="45018-181">此程式碼範例會C#將 JavaScript 中的 `ChatHub` 類別當做 `chatHub`參考。</span><span class="sxs-lookup"><span data-stu-id="45018-181">The code sample references the C# `ChatHub` class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="45018-182">在此程式碼區塊中，您會在腳本中建立回呼函數。</span><span class="sxs-lookup"><span data-stu-id="45018-182">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample7.html)]

<span data-ttu-id="45018-183">伺服器上的中樞類別會呼叫此函式，將內容更新推送至每個用戶端。</span><span class="sxs-lookup"><span data-stu-id="45018-183">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="45018-184">`htmlEncode` 函式的選擇性呼叫會顯示在頁面中顯示訊息內容之前，對其進行 HTML 編碼的方式。</span><span class="sxs-lookup"><span data-stu-id="45018-184">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page.</span></span> <span data-ttu-id="45018-185">這是防止腳本插入的方式。</span><span class="sxs-lookup"><span data-stu-id="45018-185">It's a way to prevent script injection.</span></span>

<span data-ttu-id="45018-186">此程式碼會開啟與中樞的連接。</span><span class="sxs-lookup"><span data-stu-id="45018-186">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc/samples/sample8.js)]

> [!NOTE]
> <span data-ttu-id="45018-187">這種方法可確保您在事件處理常式執行之前建立連接。</span><span class="sxs-lookup"><span data-stu-id="45018-187">This approach ensures that you establish a connection before the event handler executes.</span></span>

<span data-ttu-id="45018-188">程式碼會啟動連線，然後將函式傳遞至聊天頁面中 [**傳送**] 按鈕上的 [按一下] 事件。</span><span class="sxs-lookup"><span data-stu-id="45018-188">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="45018-189">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="45018-189">Get the code</span></span>

[<span data-ttu-id="45018-190">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="45018-190">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Getting-Started-with-c366b2f3)

## <a name="additional-resources"></a><span data-ttu-id="45018-191">其他資源</span><span class="sxs-lookup"><span data-stu-id="45018-191">Additional resources</span></span>

<span data-ttu-id="45018-192">如需 SignalR 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="45018-192">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="45018-193">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="45018-193">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="45018-194">SignalR GitHub 和範例</span><span class="sxs-lookup"><span data-stu-id="45018-194">SignalR GitHub and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="45018-195">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="45018-195">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="45018-196">後續步驟</span><span class="sxs-lookup"><span data-stu-id="45018-196">Next steps</span></span>

<span data-ttu-id="45018-197">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="45018-197">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="45018-198">設定專案</span><span class="sxs-lookup"><span data-stu-id="45018-198">Set up the project</span></span>
> * <span data-ttu-id="45018-199">執行範例</span><span class="sxs-lookup"><span data-stu-id="45018-199">Ran the sample</span></span>
> * <span data-ttu-id="45018-200">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="45018-200">Examined the code</span></span>

<span data-ttu-id="45018-201">前往下一篇文章，以瞭解如何建立使用 ASP.NET SignalR 2 的 web 應用程式，以提供高頻率的訊息功能。</span><span class="sxs-lookup"><span data-stu-id="45018-201">Advance to the next article to learn how to create a web application that uses ASP.NET SignalR 2 to provide high-frequency messaging functionality.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="45018-202">具有高頻率訊息的 Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="45018-202">Web app with high-frequency messaging</span></span>](tutorial-high-frequency-realtime-with-signalr.md)