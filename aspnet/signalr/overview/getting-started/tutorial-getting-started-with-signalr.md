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
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600461"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="4ef84-104">教學課程：與 SignalR 的即時交談2</span><span class="sxs-lookup"><span data-stu-id="4ef84-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="4ef84-105">本教學課程說明如何使用 SignalR 來建立即時聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ef84-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="4ef84-106">您會將 SignalR 新增至空白的 ASP.NET web 應用程式，並建立可傳送和顯示訊息的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="4ef84-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="4ef84-107">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="4ef84-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4ef84-108">設定專案</span><span class="sxs-lookup"><span data-stu-id="4ef84-108">Set up the project</span></span>
> * <span data-ttu-id="4ef84-109">執行範例</span><span class="sxs-lookup"><span data-stu-id="4ef84-109">Run the sample</span></span>
> * <span data-ttu-id="4ef84-110">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="4ef84-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="4ef84-111">必要條件：</span><span class="sxs-lookup"><span data-stu-id="4ef84-111">Prerequisites</span></span>

* <span data-ttu-id="4ef84-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)搭配**ASP.NET 和 網頁程式開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="4ef84-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="4ef84-113">設定專案</span><span class="sxs-lookup"><span data-stu-id="4ef84-113">Set up the Project</span></span>

<span data-ttu-id="4ef84-114">本節說明如何使用 Visual Studio 2017 和 SignalR 2 來建立空的 ASP.NET web 應用程式、新增 SignalR，以及建立聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ef84-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="4ef84-115">在 Visual Studio 中，建立 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="4ef84-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![建立 web](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="4ef84-117">在 [**新增 ASP.NET 專案-SignalRChat** ] 視窗中，保持選取 [**空白**]，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="4ef84-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="4ef84-118">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="4ef84-119">在 **[加入新專案-SignalRChat**] 中，選取 [**已安裝**] >  **C# Visual** > **Web** > **SignalR** ，然後選取 **[SignalR 中樞類別（v2）** ]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="4ef84-120">將類別命名為*ChatHub* ，並將它加入至專案。</span><span class="sxs-lookup"><span data-stu-id="4ef84-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="4ef84-121">此步驟會建立*ChatHub.cs*類別檔案，並將支援 SignalR 的一組腳本檔案和元件參考加入至專案。</span><span class="sxs-lookup"><span data-stu-id="4ef84-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="4ef84-122">將新的*ChatHub.cs*類別檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="4ef84-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="4ef84-123">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**加入** > **新專案**]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="4ef84-124">在 [**加入新專案-SignalRChat** ] 中，選取 [**已安裝** > **Visual C#**  > **Web** ]，然後選取 [ **OWIN 啟動類別**]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="4ef84-125">將類別命名為*Startup* ，並將它加入至專案。</span><span class="sxs-lookup"><span data-stu-id="4ef84-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="4ef84-126">將*Startup*類別中的預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="4ef84-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="4ef84-127">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增** > **HTML 網頁**]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="4ef84-128">將新的頁面*索引*命名為，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="4ef84-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="4ef84-129">在**方案總管**中，以滑鼠右鍵按一下您所建立的 HTML 網頁，然後選取 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="4ef84-130">將 HTML 網頁中的預設程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="4ef84-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="4ef84-131">在**方案總管**中，展開 [**腳本**]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="4ef84-132">JQuery 和 SignalR 的腳本程式庫會顯示在專案中。</span><span class="sxs-lookup"><span data-stu-id="4ef84-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="4ef84-133">封裝管理員可能已安裝較新版本的 SignalR 腳本。</span><span class="sxs-lookup"><span data-stu-id="4ef84-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="4ef84-134">檢查程式碼區塊中的腳本參考是否對應到專案中的腳本檔案版本。</span><span class="sxs-lookup"><span data-stu-id="4ef84-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="4ef84-135">來自原始程式碼區塊的腳本參考：</span><span class="sxs-lookup"><span data-stu-id="4ef84-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="4ef84-136">如果兩者不相符，請更新 *.html*檔案。</span><span class="sxs-lookup"><span data-stu-id="4ef84-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="4ef84-137">從功能表列中 **，選取 [** 檔案] > [**全部儲存**]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="4ef84-138">執行範例</span><span class="sxs-lookup"><span data-stu-id="4ef84-138">Run the Sample</span></span>

1. <span data-ttu-id="4ef84-139">在工具列中，開啟 [**腳本調試**]，然後選取 [播放] 按鈕，以在 Debug 模式中執行範例。</span><span class="sxs-lookup"><span data-stu-id="4ef84-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![輸入使用者名稱](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="4ef84-141">當瀏覽器開啟時，輸入聊天識別的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ef84-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="4ef84-142">從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到網址列中。</span><span class="sxs-lookup"><span data-stu-id="4ef84-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="4ef84-143">在每個瀏覽器中，輸入唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ef84-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="4ef84-144">現在，新增批註，然後選取 [**傳送**]。</span><span class="sxs-lookup"><span data-stu-id="4ef84-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="4ef84-145">在其他瀏覽器中重複此動作。</span><span class="sxs-lookup"><span data-stu-id="4ef84-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="4ef84-146">批註會即時出現。</span><span class="sxs-lookup"><span data-stu-id="4ef84-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="4ef84-147">這個簡單的聊天應用程式不會維護伺服器上的討論內容。</span><span class="sxs-lookup"><span data-stu-id="4ef84-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="4ef84-148">中樞會將批註廣播給所有目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="4ef84-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="4ef84-149">稍後加入交談的使用者會看到從他們加入的時間新增的訊息。</span><span class="sxs-lookup"><span data-stu-id="4ef84-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="4ef84-150">瞭解聊天應用程式如何在三個不同的瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="4ef84-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="4ef84-151">當 Tom、Anand 和 Susan 傳送訊息時，所有瀏覽器都會即時更新：</span><span class="sxs-lookup"><span data-stu-id="4ef84-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![這三個瀏覽器都會顯示相同的聊天記錄](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="4ef84-153">在**方案總管**中，檢查執行中應用程式的 [**指令檔**] 節點。</span><span class="sxs-lookup"><span data-stu-id="4ef84-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="4ef84-154">有一個名為*hub*的腳本檔案，SignalR 程式庫會在執行時間產生此檔案。</span><span class="sxs-lookup"><span data-stu-id="4ef84-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="4ef84-155">這個檔案會管理 jQuery 腳本與伺服器端程式碼之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="4ef84-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![[指令檔] 節點中自動產生的中樞腳本](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="4ef84-157">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="4ef84-157">Examine the Code</span></span>

<span data-ttu-id="4ef84-158">SignalRChat 應用程式會示範兩個基本的 SignalR 開發工作。</span><span class="sxs-lookup"><span data-stu-id="4ef84-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="4ef84-159">它會說明如何建立中樞。</span><span class="sxs-lookup"><span data-stu-id="4ef84-159">It shows you how to create a hub.</span></span> <span data-ttu-id="4ef84-160">伺服器會使用該中樞作為主要的協調物件。</span><span class="sxs-lookup"><span data-stu-id="4ef84-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="4ef84-161">中樞會使用 SignalR jQuery 程式庫來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="4ef84-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="4ef84-162">ChatHub.cs 中的 SignalR 中樞</span><span class="sxs-lookup"><span data-stu-id="4ef84-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="4ef84-163">在上述程式碼範例中，`ChatHub` 類別衍生自 `Microsoft.AspNet.SignalR.Hub` 類別。</span><span class="sxs-lookup"><span data-stu-id="4ef84-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="4ef84-164">衍生自 `Hub` 類別是建立 SignalR 應用程式的實用方式。</span><span class="sxs-lookup"><span data-stu-id="4ef84-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="4ef84-165">您可以在中樞類別上建立公用方法，然後在網頁的腳本中呼叫這些方法，藉此使用它們。</span><span class="sxs-lookup"><span data-stu-id="4ef84-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="4ef84-166">在聊天程式碼中，用戶端會呼叫 `ChatHub.Send` 方法，以傳送新的訊息。</span><span class="sxs-lookup"><span data-stu-id="4ef84-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="4ef84-167">然後，中樞會藉由呼叫 `Clients.All.broadcastMessage`，將訊息傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="4ef84-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="4ef84-168">`Send` 方法會示範數個中樞概念：</span><span class="sxs-lookup"><span data-stu-id="4ef84-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="4ef84-169">在中樞上宣告公用方法，讓用戶端可以呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="4ef84-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="4ef84-170">使用 `Microsoft.AspNet.SignalR.Hub.Clients` 動態屬性，與連線至此中樞的所有用戶端進行通訊。</span><span class="sxs-lookup"><span data-stu-id="4ef84-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="4ef84-171">呼叫用戶端上的函式（例如 `broadcastMessage` 函數）來更新用戶端。</span><span class="sxs-lookup"><span data-stu-id="4ef84-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="4ef84-172">SignalR 和 jQuery 中的索引 .html</span><span class="sxs-lookup"><span data-stu-id="4ef84-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="4ef84-173">程式碼範例中的 [ *.html* ] 頁面會顯示如何使用 SignalR jQuery 程式庫與 SignalR 中樞進行通訊。</span><span class="sxs-lookup"><span data-stu-id="4ef84-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="4ef84-174">程式碼會執行許多重要的工作。</span><span class="sxs-lookup"><span data-stu-id="4ef84-174">The code carries out many important tasks.</span></span> <span data-ttu-id="4ef84-175">它會宣告一個 proxy 來參考中樞、宣告一個函式，讓伺服器可以呼叫它來將內容推送至用戶端，並啟動連線以將訊息傳送至中樞。</span><span class="sxs-lookup"><span data-stu-id="4ef84-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="4ef84-176">在 JavaScript 中，伺服器類別及其成員的參考必須是 camelCase。</span><span class="sxs-lookup"><span data-stu-id="4ef84-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="4ef84-177">程式碼範例會將C# JavaScript 中的*ChatHub*類別參考為 `chatHub`。</span><span class="sxs-lookup"><span data-stu-id="4ef84-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="4ef84-178">在此程式碼區塊中，您會在腳本中建立回呼函數。</span><span class="sxs-lookup"><span data-stu-id="4ef84-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="4ef84-179">伺服器上的中樞類別會呼叫此函式，將內容更新推送至每個用戶端。</span><span class="sxs-lookup"><span data-stu-id="4ef84-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="4ef84-180">在顯示內容之前進行 HTML 編碼的兩行程式碼是選擇性的，並顯示可防止腳本插入的好方法。</span><span class="sxs-lookup"><span data-stu-id="4ef84-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="4ef84-181">此程式碼會開啟與中樞的連接。</span><span class="sxs-lookup"><span data-stu-id="4ef84-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="4ef84-182">這種方法可確保程式碼會在事件處理常式執行之前建立連接。</span><span class="sxs-lookup"><span data-stu-id="4ef84-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="4ef84-183">程式碼會啟動連接，然後將函式傳遞給它，以處理 HTML 網頁中 [**傳送**] 按鈕上的 click 事件。</span><span class="sxs-lookup"><span data-stu-id="4ef84-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="4ef84-184">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="4ef84-184">Get the code</span></span>

[<span data-ttu-id="4ef84-185">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="4ef84-185">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="4ef84-186">其他資源</span><span class="sxs-lookup"><span data-stu-id="4ef84-186">Additional resources</span></span>

<span data-ttu-id="4ef84-187">如需 SignalR 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="4ef84-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="4ef84-188">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="4ef84-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="4ef84-189">SignalR Github 和範例</span><span class="sxs-lookup"><span data-stu-id="4ef84-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="4ef84-190">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="4ef84-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="4ef84-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="4ef84-191">Next steps</span></span>

<span data-ttu-id="4ef84-192">在本教學課程中，您將：</span><span class="sxs-lookup"><span data-stu-id="4ef84-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="4ef84-193">設定專案</span><span class="sxs-lookup"><span data-stu-id="4ef84-193">Set up the project</span></span>
> * <span data-ttu-id="4ef84-194">執行範例</span><span class="sxs-lookup"><span data-stu-id="4ef84-194">Ran the sample</span></span>
> * <span data-ttu-id="4ef84-195">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="4ef84-195">Examined the code</span></span>

<span data-ttu-id="4ef84-196">前進到下一篇文章，以瞭解如何使用 SignalR 和 MVC 5。</span><span class="sxs-lookup"><span data-stu-id="4ef84-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="4ef84-197">SignalR 2 和 MVC 5</span><span class="sxs-lookup"><span data-stu-id="4ef84-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)