---
uid: signalr/overview/getting-started/tutorial-getting-started-with-signalr
title: 教學課程：使用 SignalR 2 的即時聊天 |Microsoft Docs
author: bradygaster
description: 此教學課程會示範如何使用 SignalR 建立即時聊天應用程式。 SignalR 加入空白的 ASP.NET web 應用程式上。
ms.author: bradyg
ms.date: 01/22/2019
ms.assetid: a8b3b778-f009-4369-85c7-e90f9878d8b4
msc.legacyurl: /signalr/overview/getting-started/tutorial-getting-started-with-signalr
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: ecc235454d4b95ce660a4373387f44720826b076
ms.sourcegitcommit: 2d53ed9e4c8b19d3526cbc689bfa8394c9449cec
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/22/2019
ms.locfileid: "59905640"
---
# <a name="tutorial-real-time-chat-with-signalr-2"></a><span data-ttu-id="9340e-104">教學課程：使用 SignalR 2 進行即時聊天</span><span class="sxs-lookup"><span data-stu-id="9340e-104">Tutorial: Real-time chat with SignalR 2</span></span>

<span data-ttu-id="9340e-105">本教學課程會示範如何使用 SignalR 建立即時聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="9340e-105">This tutorial shows you how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="9340e-106">SignalR 加入空白的 ASP.NET web 應用程式，並建立 HTML 網頁來傳送，並顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="9340e-106">You add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

<span data-ttu-id="9340e-107">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="9340e-107">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9340e-108">設定專案</span><span class="sxs-lookup"><span data-stu-id="9340e-108">Set up the project</span></span>
> * <span data-ttu-id="9340e-109">執行範例</span><span class="sxs-lookup"><span data-stu-id="9340e-109">Run the sample</span></span>
> * <span data-ttu-id="9340e-110">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="9340e-110">Examine the code</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

## <a name="prerequisites"></a><span data-ttu-id="9340e-111">必要條件</span><span class="sxs-lookup"><span data-stu-id="9340e-111">Prerequisites</span></span>

* <span data-ttu-id="9340e-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/)具有**ASP.NET 和 web 開發**工作負載。</span><span class="sxs-lookup"><span data-stu-id="9340e-112">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/) with the **ASP.NET and web development** workload.</span></span>

## <a name="set-up-the-project"></a><span data-ttu-id="9340e-113">設定專案</span><span class="sxs-lookup"><span data-stu-id="9340e-113">Set up the Project</span></span>

<span data-ttu-id="9340e-114">本節說明如何使用 Visual Studio 2017 與 SignalR 2 來建立空白的 ASP.NET web 應用程式，SignalR，加上建立交談應用程式。</span><span class="sxs-lookup"><span data-stu-id="9340e-114">This section shows how to use Visual Studio 2017 and SignalR 2 to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

1. <span data-ttu-id="9340e-115">在 Visual Studio 中建立 ASP.NET Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9340e-115">In Visual Studio, create an ASP.NET Web Application.</span></span>

    ![建立 web](tutorial-getting-started-with-signalr/_static/image2.png)

1. <span data-ttu-id="9340e-117">在 [**新的 ASP.NET 專案-SignalRChat** ] 視窗中，保留**空白**，並選取 **[確定]**。</span><span class="sxs-lookup"><span data-stu-id="9340e-117">In the **New ASP.NET Project - SignalRChat** window, leave **Empty** selected and select **OK**.</span></span>

1. <span data-ttu-id="9340e-118">在 **方案總管**，以滑鼠右鍵按一下專案，然後選取**新增** > **新項目**。</span><span class="sxs-lookup"><span data-stu-id="9340e-118">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="9340e-119">在 **加入新項目-SignalRChat**，選取**已安裝** > **Visual C#**   >  **Web**  > **SignalR** ，然後選取**SignalR Hub 類別 (v2)**。</span><span class="sxs-lookup"><span data-stu-id="9340e-119">In **Add New Item - SignalRChat**, select **Installed** > **Visual C#** > **Web** > **SignalR**  and then select **SignalR Hub Class (v2)**.</span></span>

1. <span data-ttu-id="9340e-120">將類別命名為*ChatHub*並將它新增至專案。</span><span class="sxs-lookup"><span data-stu-id="9340e-120">Name the class *ChatHub* and add it to the project.</span></span>

    <span data-ttu-id="9340e-121">這個步驟會建立*ChatHub.cs*類別檔案，以及新增一組指令碼檔案和專案支援 SignalR 的組件參考。</span><span class="sxs-lookup"><span data-stu-id="9340e-121">This step creates the *ChatHub.cs* class file and adds a set of script files and assembly references that support SignalR to the project.</span></span>

1. <span data-ttu-id="9340e-122">在新程式碼取代*ChatHub.cs*類別檔案，以下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="9340e-122">Replace the code in the new *ChatHub.cs* class file with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]

1. <span data-ttu-id="9340e-123">在 **方案總管**，以滑鼠右鍵按一下專案，然後選取**新增** > **新項目**。</span><span class="sxs-lookup"><span data-stu-id="9340e-123">In **Solution Explorer**, right-click the project and select **Add** > **New Item**.</span></span>

1. <span data-ttu-id="9340e-124">在 **加入新項目-SignalRChat**選取**已安裝** > **Visual C#**   >  **Web** ，然後選取  **OWIN 啟動類別**。</span><span class="sxs-lookup"><span data-stu-id="9340e-124">In **Add New Item - SignalRChat** select **Installed** > **Visual C#** > **Web**  and then select **OWIN Startup Class**.</span></span>

1. <span data-ttu-id="9340e-125">將類別命名為*啟動*並將它新增至專案。</span><span class="sxs-lookup"><span data-stu-id="9340e-125">Name the class *Startup* and add it to the project.</span></span>

1. <span data-ttu-id="9340e-126">取代預設的程式碼中*啟動*以下列程式碼的類別：</span><span class="sxs-lookup"><span data-stu-id="9340e-126">Replace the default code in *Startup* class with this code:</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]

1. <span data-ttu-id="9340e-127">在 **方案總管**，以滑鼠右鍵按一下專案，然後選取**新增** > **HTML 網頁**。</span><span class="sxs-lookup"><span data-stu-id="9340e-127">In **Solution Explorer**, right-click the project and select **Add** > **HTML Page**.</span></span>

1. <span data-ttu-id="9340e-128">將新頁面命名*index* ，然後選取**確定**。</span><span class="sxs-lookup"><span data-stu-id="9340e-128">Name the new page *index* and select **OK**.</span></span>

1. <span data-ttu-id="9340e-129">在 **方案總管**，以滑鼠右鍵按一下您建立的 HTML 頁面，然後選取**設定為起始頁**。</span><span class="sxs-lookup"><span data-stu-id="9340e-129">In **Solution Explorer**, right-click the HTML page you created and select **Set as Start Page**.</span></span>

1. <span data-ttu-id="9340e-130">HTML 網頁中的預設程式碼取代此程式碼：</span><span class="sxs-lookup"><span data-stu-id="9340e-130">Replace the default code in the HTML page with this code:</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample3.html)]

1. <span data-ttu-id="9340e-131">在 **方案總管**，展開**指令碼**。</span><span class="sxs-lookup"><span data-stu-id="9340e-131">In **Solution Explorer**, expand **Scripts**.</span></span>

    <span data-ttu-id="9340e-132">JQuery 和 SignalR 的指令碼程式庫會顯示在專案中。</span><span class="sxs-lookup"><span data-stu-id="9340e-132">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="9340e-133">封裝管理員可能已安裝較新版 SignalR 指令碼。</span><span class="sxs-lookup"><span data-stu-id="9340e-133">The package manager may have installed a later version of the SignalR scripts.</span></span>

1. <span data-ttu-id="9340e-134">請檢查程式碼區塊中的指令碼參考對應至專案中的指令碼檔案的版本。</span><span class="sxs-lookup"><span data-stu-id="9340e-134">Check that the script references in the code block correspond to the versions of the script files in the project.</span></span>

    <span data-ttu-id="9340e-135">從原始的程式碼區塊的指令碼參考：</span><span class="sxs-lookup"><span data-stu-id="9340e-135">Script references from the original code block:</span></span>

    ```html
    <!--Script references. -->
    <!--Reference the jQuery library. -->
    <script src="Scripts/jquery-3.1.1.min.js" ></script>
    <!--Reference the SignalR library. -->
    <script src="Scripts/jquery.signalR-2.2.1.min.js"></script>
    ```

1. <span data-ttu-id="9340e-136">如果兩者不符，更新 *.html*檔案。</span><span class="sxs-lookup"><span data-stu-id="9340e-136">If they don't match, update the *.html* file.</span></span>

1. <span data-ttu-id="9340e-137">從功能表列中，選取**檔案** > **全部儲存**。</span><span class="sxs-lookup"><span data-stu-id="9340e-137">From the menu bar, select **File** > **Save All**.</span></span>

## <a name="run-the-sample"></a><span data-ttu-id="9340e-138">執行範例</span><span class="sxs-lookup"><span data-stu-id="9340e-138">Run the Sample</span></span>

1. <span data-ttu-id="9340e-139">在工具列中，開啟**指令碼偵錯**，然後選取 偵錯模式中執行範例的 播放 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9340e-139">In the toolbar, turn on **Script Debugging** and then select the play button to run the sample in Debug mode.</span></span>

    ![輸入使用者名稱](tutorial-getting-started-with-signalr/_static/image3.png)

1. <span data-ttu-id="9340e-141">瀏覽器開啟時，輸入您的對談身分識別的名稱。</span><span class="sxs-lookup"><span data-stu-id="9340e-141">When the browser opens, enter a name for your chat identity.</span></span>

1. <span data-ttu-id="9340e-142">從瀏覽器複製 URL，開啟兩個其他瀏覽器，並將 Url 貼到 位址列。</span><span class="sxs-lookup"><span data-stu-id="9340e-142">Copy the URL from the browser, open two other browsers, and paste the URLs into the address bars.</span></span>

1. <span data-ttu-id="9340e-143">在每個瀏覽器中，輸入唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="9340e-143">In each browser, enter a unique name.</span></span>

1. <span data-ttu-id="9340e-144">現在，加入 註解，然後選取**傳送**。</span><span class="sxs-lookup"><span data-stu-id="9340e-144">Now, add a comment and select **Send**.</span></span> <span data-ttu-id="9340e-145">您可以重複，在其他瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="9340e-145">Repeat that in the other browsers.</span></span> <span data-ttu-id="9340e-146">註解會出現在 即時。</span><span class="sxs-lookup"><span data-stu-id="9340e-146">The comments appear in real-time.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9340e-147">這個簡單的聊天應用程式不會維護伺服器上的討論內容。</span><span class="sxs-lookup"><span data-stu-id="9340e-147">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="9340e-148">中樞會廣播到所有目前使用者的註解。</span><span class="sxs-lookup"><span data-stu-id="9340e-148">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="9340e-149">稍後加入聊天室使用者會看到訊息的時間加入它們加入。</span><span class="sxs-lookup"><span data-stu-id="9340e-149">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="9340e-150">了解交談應用程式在三個不同的瀏覽器中執行時。</span><span class="sxs-lookup"><span data-stu-id="9340e-150">See how the chat application runs in three different browsers.</span></span> <span data-ttu-id="9340e-151">當 Tom、 Anand 和 Susan 傳送訊息時，即時更新所有瀏覽器：</span><span class="sxs-lookup"><span data-stu-id="9340e-151">When Tom, Anand, and Susan send messages, all browsers update in real time:</span></span>

    ![所有的三個瀏覽器會顯示相同的交談記錄](tutorial-getting-started-with-signalr/_static/image4.png)

1. <span data-ttu-id="9340e-153">在 **方案總管**，檢查**指令碼文件**節點執行的應用程式。</span><span class="sxs-lookup"><span data-stu-id="9340e-153">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="9340e-154">沒有名為的指令碼檔案*中樞*SignalR 程式庫產生在執行階段。</span><span class="sxs-lookup"><span data-stu-id="9340e-154">There's a script file named *hubs* that the SignalR library generates at runtime.</span></span> <span data-ttu-id="9340e-155">此檔案會管理 jQuery 指令碼和伺服器端程式碼之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="9340e-155">This file manages the communication between jQuery script and server-side code.</span></span>

    ![在 [指令碼文件] 節點中的自動產生中樞指令碼](tutorial-getting-started-with-signalr/_static/image5.png)

## <a name="examine-the-code"></a><span data-ttu-id="9340e-157">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="9340e-157">Examine the Code</span></span>

<span data-ttu-id="9340e-158">SignalRChat 應用程式會示範兩個基本的 SignalR 開發工作。</span><span class="sxs-lookup"><span data-stu-id="9340e-158">The SignalRChat application demonstrates two basic SignalR development tasks.</span></span> <span data-ttu-id="9340e-159">它說明如何建立中樞。</span><span class="sxs-lookup"><span data-stu-id="9340e-159">It shows you how to create a hub.</span></span> <span data-ttu-id="9340e-160">伺服器會使用該中樞做為主要協調物件。</span><span class="sxs-lookup"><span data-stu-id="9340e-160">The server uses that hub as the main coordination object.</span></span> <span data-ttu-id="9340e-161">中樞會使用 SignalR jQuery 程式庫，來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="9340e-161">The hub uses the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs-in-the-chathubcs"></a><span data-ttu-id="9340e-162">在 ChatHub.cs SignalR 中樞</span><span class="sxs-lookup"><span data-stu-id="9340e-162">SignalR Hubs in the ChatHub.cs</span></span>

<span data-ttu-id="9340e-163">在上述程式碼範例`ChatHub`類別衍生自`Microsoft.AspNet.SignalR.Hub`類別。</span><span class="sxs-lookup"><span data-stu-id="9340e-163">In the code sample above, the `ChatHub` class derives from the `Microsoft.AspNet.SignalR.Hub` class.</span></span> <span data-ttu-id="9340e-164">衍生自`Hub`類別是實用的方式，來建置 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9340e-164">Deriving from the `Hub` class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="9340e-165">您可以建立中樞類別上的公用方法和呼叫它們從網頁中的指令碼，以使用這些方法。</span><span class="sxs-lookup"><span data-stu-id="9340e-165">You can create public methods on your hub class and then use those methods by calling them from scripts in a web page.</span></span>

<span data-ttu-id="9340e-166">在對談程式碼中，用戶端呼叫`ChatHub.Send`方法以傳送新訊息。</span><span class="sxs-lookup"><span data-stu-id="9340e-166">In the chat code, clients call the `ChatHub.Send` method to send a new message.</span></span> <span data-ttu-id="9340e-167">中樞然後將訊息傳送至所有用戶端藉由呼叫`Clients.All.broadcastMessage`。</span><span class="sxs-lookup"><span data-stu-id="9340e-167">The hub then sends the message to all clients by calling `Clients.All.broadcastMessage`.</span></span>

<span data-ttu-id="9340e-168">`Send`方法將示範數個中樞概念：</span><span class="sxs-lookup"><span data-stu-id="9340e-168">The `Send` method demonstrates several hub concepts:</span></span>

* <span data-ttu-id="9340e-169">可讓用戶端呼叫，則請在中樞中宣告的公用方法。</span><span class="sxs-lookup"><span data-stu-id="9340e-169">Declare public methods on a hub so that clients can call them.</span></span>

* <span data-ttu-id="9340e-170">使用`Microsoft.AspNet.SignalR.Hub.Clients`此中樞的連線與所有的用戶端通訊的動態屬性。</span><span class="sxs-lookup"><span data-stu-id="9340e-170">Use the `Microsoft.AspNet.SignalR.Hub.Clients` dynamic property to communicate with all clients connected to this hub.</span></span>

* <span data-ttu-id="9340e-171">在用戶端上呼叫的函式 (例如`broadcastMessage`函式) 來更新用戶端。</span><span class="sxs-lookup"><span data-stu-id="9340e-171">Call a function on the client (like the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample4.cs)]

### <a name="signalr-and-jquery-in-the-indexhtml"></a><span data-ttu-id="9340e-172">SignalR 和 jQuery 在 index.html 中</span><span class="sxs-lookup"><span data-stu-id="9340e-172">SignalR and jQuery in the index.html</span></span>

<span data-ttu-id="9340e-173">*Index.html*頁面中的程式碼範例示範如何使用 SignalR jQuery 程式庫與 SignalR 中樞進行通訊。</span><span class="sxs-lookup"><span data-stu-id="9340e-173">The *index.html* page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="9340e-174">程式碼會執行許多重要的工作。</span><span class="sxs-lookup"><span data-stu-id="9340e-174">The code carries out many important tasks.</span></span> <span data-ttu-id="9340e-175">它會宣告來參考中樞 proxy、 宣告函式推播內容給用戶端，可以呼叫的伺服器，並開始將訊息傳送至中樞的連接。</span><span class="sxs-lookup"><span data-stu-id="9340e-175">It declares a proxy to reference the hub, declares a function that the server can call to push content to clients, and it starts a connection to send messages to the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample5.js)]

> [!NOTE]
> <span data-ttu-id="9340e-176">在 JavaScript 中必須是 camelCase 伺服器類別和其成員的參考。</span><span class="sxs-lookup"><span data-stu-id="9340e-176">In JavaScript the reference to the server class and its members has to be camelCase.</span></span> <span data-ttu-id="9340e-177">程式碼範例參考C# *ChatHub*類別，以做為 JavaScript `chatHub`。</span><span class="sxs-lookup"><span data-stu-id="9340e-177">The code sample references the C# *ChatHub* class in JavaScript as `chatHub`.</span></span>

<span data-ttu-id="9340e-178">在此程式碼區塊中，您可以建立指令碼中的回呼函式。</span><span class="sxs-lookup"><span data-stu-id="9340e-178">In this code block, you create a callback function in the script.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample6.html)]

<span data-ttu-id="9340e-179">在伺服器上的中樞類別會呼叫此函式可將內容更新推送至每個用戶端。</span><span class="sxs-lookup"><span data-stu-id="9340e-179">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="9340e-180">兩個線條的 HTML 編碼內容，然後再顯示它是選擇性的顯示阻止指令碼資料隱碼的好方法。</span><span class="sxs-lookup"><span data-stu-id="9340e-180">The two lines that HTML-encode the content before displaying it are optional and show a good way to prevent script injection.</span></span>

<span data-ttu-id="9340e-181">此程式碼與中樞開啟的連接。</span><span class="sxs-lookup"><span data-stu-id="9340e-181">This code opens a connection with the hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample7.js)]

> [!NOTE]
> <span data-ttu-id="9340e-182">這個方法可確保程式碼在事件處理常式執行之前，會建立連接。</span><span class="sxs-lookup"><span data-stu-id="9340e-182">This approach ensures that the code establishes a connection before the event handler executes.</span></span>

<span data-ttu-id="9340e-183">程式碼啟動連線並再將它傳遞至 click 事件處理函式**傳送**HTML 網頁中的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9340e-183">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="9340e-184">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="9340e-184">Get the code</span></span>

[<span data-ttu-id="9340e-185">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="9340e-185">Download Completed Project</span></span>](http://code.msdn.microsoft.com/SignalR-Getting-Started-b9d18aa9)

## <a name="additional-resources"></a><span data-ttu-id="9340e-186">其他資源</span><span class="sxs-lookup"><span data-stu-id="9340e-186">Additional resources</span></span>

<span data-ttu-id="9340e-187">如需 SignalR 相關資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="9340e-187">For more about SignalR, see the following resources:</span></span>

* [<span data-ttu-id="9340e-188">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="9340e-188">SignalR Project</span></span>](http://signalr.net)

* [<span data-ttu-id="9340e-189">SignalR Github 和範例</span><span class="sxs-lookup"><span data-stu-id="9340e-189">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)

* [<span data-ttu-id="9340e-190">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="9340e-190">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)

## <a name="next-steps"></a><span data-ttu-id="9340e-191">後續步驟</span><span class="sxs-lookup"><span data-stu-id="9340e-191">Next steps</span></span>

<span data-ttu-id="9340e-192">在本教學課程中您：</span><span class="sxs-lookup"><span data-stu-id="9340e-192">In this tutorial you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="9340e-193">設定專案</span><span class="sxs-lookup"><span data-stu-id="9340e-193">Set up the project</span></span>
> * <span data-ttu-id="9340e-194">執行範例</span><span class="sxs-lookup"><span data-stu-id="9340e-194">Ran the sample</span></span>
> * <span data-ttu-id="9340e-195">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="9340e-195">Examined the code</span></span>

<span data-ttu-id="9340e-196">請前往下一篇文章，以了解如何使用 SignalR 和 MVC 5。</span><span class="sxs-lookup"><span data-stu-id="9340e-196">Advance to the next article to learn how to use SignalR and MVC 5.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="9340e-197">SignalR 2 及 MVC 5</span><span class="sxs-lookup"><span data-stu-id="9340e-197">SignalR 2 and MVC 5</span></span>](tutorial-getting-started-with-signalr-and-mvc.md)