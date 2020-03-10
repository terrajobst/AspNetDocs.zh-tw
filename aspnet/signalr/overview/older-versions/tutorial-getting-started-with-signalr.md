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
# <a name="tutorial-getting-started-with-signalr-1x"></a><span data-ttu-id="cc086-103">教學課程：使用 SignalR 1.x 消費者入門</span><span class="sxs-lookup"><span data-stu-id="cc086-103">Tutorial: Getting Started with SignalR 1.x</span></span>

<span data-ttu-id="cc086-104">[Fletcher](https://github.com/pfletcher)的[Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="cc086-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="cc086-105">此教學課程會示範如何使用 SignalR 建立即時聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc086-105">This tutorial shows how to use SignalR to create a real-time chat application.</span></span> <span data-ttu-id="cc086-106">您會將 SignalR 新增至空白的 ASP.NET web 應用程式，並建立用來傳送和顯示訊息的 HTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="cc086-106">You will add SignalR to an empty ASP.NET web application and create an HTML page to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="cc086-107">概觀</span><span class="sxs-lookup"><span data-stu-id="cc086-107">Overview</span></span>

<span data-ttu-id="cc086-108">本教學課程會示範如何建立以瀏覽器為基礎的簡單交談應用程式，以介紹 SignalR 開發。</span><span class="sxs-lookup"><span data-stu-id="cc086-108">This tutorial introduces SignalR development by showing how to build a simple browser-based chat application.</span></span> <span data-ttu-id="cc086-109">您會將 SignalR 程式庫新增至空白的 ASP.NET web 應用程式、建立可將訊息傳送至用戶端的中樞類別，以及建立可讓使用者傳送及接收聊天訊息的 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="cc086-109">You will add the SignalR library to an empty ASP.NET web application, create a hub class for sending messages to clients, and create an HTML page that lets users send and receive chat messages.</span></span> <span data-ttu-id="cc086-110">如需示範如何使用 MVC 視圖在 MVC 4 中建立聊天應用程式的類似教學課程，請參閱[使用 SignalR 和 MVC 4 的消費者入門](index.md)。</span><span class="sxs-lookup"><span data-stu-id="cc086-110">For a similar tutorial that shows how to create a chat application in MVC 4 using an MVC view, see [Getting Started with SignalR and MVC 4](index.md).</span></span>

> [!NOTE]
> <span data-ttu-id="cc086-111">本教學課程使用 release （1.x）版的 SignalR。</span><span class="sxs-lookup"><span data-stu-id="cc086-111">This tutorial uses the release (1.x) version of SignalR.</span></span> <span data-ttu-id="cc086-112">如需 SignalR 1.x 與2.0 之間變更的詳細資訊，請參閱[升級 SignalR 1.X 專案](../releases/upgrading-signalr-1x-projects-to-20.md)。</span><span class="sxs-lookup"><span data-stu-id="cc086-112">For details on changes between SignalR 1.x and 2.0, see [Upgrading SignalR 1.x Projects](../releases/upgrading-signalr-1x-projects-to-20.md).</span></span>

<span data-ttu-id="cc086-113">SignalR 是一個開放原始碼 .NET 程式庫，用於建立需要即時使用者互動或即時資料更新的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc086-113">SignalR is an open-source .NET library for building web applications that require live user interaction or real-time data updates.</span></span> <span data-ttu-id="cc086-114">範例包括社交應用程式、多使用者遊戲、商務共同作業，以及新聞、天氣或金融更新應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc086-114">Examples include social applications, multiuser games, business collaboration, and news, weather, or financial update applications.</span></span> <span data-ttu-id="cc086-115">這些通常稱為即時應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc086-115">These are often called real-time applications.</span></span>

<span data-ttu-id="cc086-116">SignalR 簡化了建立即時應用程式的流程。</span><span class="sxs-lookup"><span data-stu-id="cc086-116">SignalR simplifies the process of building real-time applications.</span></span> <span data-ttu-id="cc086-117">其中包含 ASP.NET 伺服器程式庫和 JavaScript 用戶端程式庫，可讓您更輕鬆地管理用戶端伺服器連線，以及將內容更新推送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="cc086-117">It includes an ASP.NET server library and a JavaScript client library to make it easier to manage client-server connections and push content updates to clients.</span></span> <span data-ttu-id="cc086-118">您可以將 SignalR 程式庫新增至現有的 ASP.NET 應用程式，以取得即時功能。</span><span class="sxs-lookup"><span data-stu-id="cc086-118">You can add the SignalR library to an existing ASP.NET application to gain real-time functionality.</span></span>

<span data-ttu-id="cc086-119">本教學課程會示範下列 SignalR 開發工作：</span><span class="sxs-lookup"><span data-stu-id="cc086-119">The tutorial demonstrates the following SignalR development tasks:</span></span>

- <span data-ttu-id="cc086-120">將 SignalR 程式庫新增至 ASP.NET web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc086-120">Adding the SignalR library to an ASP.NET web application.</span></span>
- <span data-ttu-id="cc086-121">建立中樞類別以將內容推送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="cc086-121">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="cc086-122">使用網頁中的 SignalR jQuery 程式庫來傳送訊息，並從中樞顯示更新。</span><span class="sxs-lookup"><span data-stu-id="cc086-122">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="cc086-123">下列螢幕擷取畫面顯示在瀏覽器中執行的聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc086-123">The following screen shot shows the chat application running in a browser.</span></span> <span data-ttu-id="cc086-124">每個新的使用者都可以張貼留言，並在使用者加入聊天之後，看到新增的批註。</span><span class="sxs-lookup"><span data-stu-id="cc086-124">Each new user can post comments and see comments added after the user joins the chat.</span></span>

![聊天實例](tutorial-getting-started-with-signalr/_static/image1.png)

<span data-ttu-id="cc086-126">各節</span><span class="sxs-lookup"><span data-stu-id="cc086-126">Sections:</span></span>

- [<span data-ttu-id="cc086-127">設定專案</span><span class="sxs-lookup"><span data-stu-id="cc086-127">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="cc086-128">執行範例</span><span class="sxs-lookup"><span data-stu-id="cc086-128">Run the Sample</span></span>](#run)
- [<span data-ttu-id="cc086-129">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="cc086-129">Examine the Code</span></span>](#code)
- [<span data-ttu-id="cc086-130">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc086-130">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="cc086-131">設定專案</span><span class="sxs-lookup"><span data-stu-id="cc086-131">Set up the Project</span></span>

<span data-ttu-id="cc086-132">本節說明如何建立空白的 ASP.NET web 應用程式、新增 SignalR，以及建立聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc086-132">This section shows how to create an empty ASP.NET web application, add SignalR, and create the chat application.</span></span>

<span data-ttu-id="cc086-133">必要條件：</span><span class="sxs-lookup"><span data-stu-id="cc086-133">Prerequisites:</span></span>

- <span data-ttu-id="cc086-134">Visual Studio 2010 SP1 或2012。</span><span class="sxs-lookup"><span data-stu-id="cc086-134">Visual Studio 2010 SP1 or 2012.</span></span> <span data-ttu-id="cc086-135">如果您沒有 Visual Studio，請參閱[ASP.NET 下載](https://www.asp.net/downloads)以取得免費的 Visual Studio 2012 Express 開發工具。</span><span class="sxs-lookup"><span data-stu-id="cc086-135">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="cc086-136">[Microsoft ASP.NET 和 Web 工具 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941)。</span><span class="sxs-lookup"><span data-stu-id="cc086-136">[Microsoft ASP.NET and Web Tools 2012.2](https://go.microsoft.com/fwlink/?LinkId=279941).</span></span> <span data-ttu-id="cc086-137">針對 Visual Studio 2012，此安裝程式會將新的 ASP.NET 功能（包括 SignalR 範本）新增至 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="cc086-137">For Visual Studio 2012, this installer adds new ASP.NET features including SignalR templates to Visual Studio.</span></span> <span data-ttu-id="cc086-138">針對 Visual Studio 2010 SP1，安裝程式無法使用，但您可以安裝 SignalR NuGet 套件（如設定步驟中所述）來完成本教學課程。</span><span class="sxs-lookup"><span data-stu-id="cc086-138">For Visual Studio 2010 SP1, an installer is not available but you can complete the tutorial by installing the SignalR NuGet package as described in the setup steps.</span></span>

<span data-ttu-id="cc086-139">下列步驟會使用 Visual Studio 2012 來建立 ASP.NET 空白 Web 應用程式，並新增 SignalR 程式庫：</span><span class="sxs-lookup"><span data-stu-id="cc086-139">The following steps use Visual Studio 2012 to create an ASP.NET Empty Web Application and add the SignalR library:</span></span>

1. <span data-ttu-id="cc086-140">在 Visual Studio 建立 ASP.NET 空白 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc086-140">In Visual Studio create an ASP.NET Empty Web Application.</span></span>

    ![建立空的 web](tutorial-getting-started-with-signalr/_static/image2.png)
2. <span data-ttu-id="cc086-142">選取 [工具]，開啟 [**套件管理員主控台**] **|NuGet 套件管理員 |套件管理員主控台**。</span><span class="sxs-lookup"><span data-stu-id="cc086-142">Open the **Package Manager Console** by selecting **Tools | NuGet Package Manager | Package Manager Console**.</span></span> <span data-ttu-id="cc086-143">在主控台視窗中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="cc086-143">Enter the following command into the console window:</span></span>

    `Install-Package Microsoft.AspNet.SignalR -Version 1.1.3`

    <span data-ttu-id="cc086-144">此命令會安裝最新版本的 SignalR 1.x。</span><span class="sxs-lookup"><span data-stu-id="cc086-144">This command installs the latest version of SignalR 1.x.</span></span>
3. <span data-ttu-id="cc086-145">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增] |類別**。</span><span class="sxs-lookup"><span data-stu-id="cc086-145">In **Solution Explorer**, right-click the project, select **Add | Class**.</span></span> <span data-ttu-id="cc086-146">將新類別命名為**ChatHub**。</span><span class="sxs-lookup"><span data-stu-id="cc086-146">Name the new class **ChatHub**.</span></span>
4. <span data-ttu-id="cc086-147">在**方案總管**展開 [腳本] 節點。</span><span class="sxs-lookup"><span data-stu-id="cc086-147">In **Solution Explorer** expand the Scripts node.</span></span> <span data-ttu-id="cc086-148">JQuery 和 SignalR 的腳本程式庫會顯示在專案中。</span><span class="sxs-lookup"><span data-stu-id="cc086-148">Script libraries for jQuery and SignalR are visible in the project.</span></span>

    ![程式庫參考](tutorial-getting-started-with-signalr/_static/image3.png)
5. <span data-ttu-id="cc086-150">將**ChatHub**類別中的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="cc086-150">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample1.cs)]
6. <span data-ttu-id="cc086-151">在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**新增] |新專案**。</span><span class="sxs-lookup"><span data-stu-id="cc086-151">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="cc086-152">在 [**加入新專案**] 對話方塊中，選取 [**全域應用程式類別**]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="cc086-152">In the **Add New Item** dialog, select **Global Application Class** and click **Add**.</span></span>

    ![加入全域](tutorial-getting-started-with-signalr/_static/image4.png)
7. <span data-ttu-id="cc086-154">在 Global.asax.cs 類別中提供的 `using` 語句之後，新增下列 `using` 語句。</span><span class="sxs-lookup"><span data-stu-id="cc086-154">Add the following `using` statements after the provided `using` statements in the Global.asax.cs class.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample2.cs)]
8. <span data-ttu-id="cc086-155">在全域類別的 `Application_Start` 方法中新增下列程式程式碼，以註冊 SignalR 中樞的預設路由。</span><span class="sxs-lookup"><span data-stu-id="cc086-155">Add the following line of code in the `Application_Start` method of the Global class to register the default route for SignalR hubs.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample3.cs)]
9. <span data-ttu-id="cc086-156">在**方案總管**中，以滑鼠右鍵按一下專案，然後按一下 [**新增] |新專案**。</span><span class="sxs-lookup"><span data-stu-id="cc086-156">In **Solution Explorer**, right-click the project, then click **Add | New Item**.</span></span> <span data-ttu-id="cc086-157">在 [**加入新專案**] 對話方塊中，選取 [Html 網頁]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="cc086-157">In the **Add New Item** dialog, select Html Page and click **Add**.</span></span>
10. <span data-ttu-id="cc086-158">在**方案總管**中，以滑鼠右鍵按一下您剛建立的 HTML 網頁，然後按一下 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="cc086-158">In **Solution Explorer**, right-click the HTML page you just created and click **Set as Start Page**.</span></span>
11. <span data-ttu-id="cc086-159">將 HTML 網頁中的預設程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="cc086-159">Replace the default code in the HTML page with the following code.</span></span>

    [!code-html[Main](tutorial-getting-started-with-signalr/samples/sample4.html)]
12. <span data-ttu-id="cc086-160">**全部儲存**專案。</span><span class="sxs-lookup"><span data-stu-id="cc086-160">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="cc086-161">執行範例</span><span class="sxs-lookup"><span data-stu-id="cc086-161">Run the Sample</span></span>

1. <span data-ttu-id="cc086-162">按 F5 以在 [調試] 模式中執行專案。</span><span class="sxs-lookup"><span data-stu-id="cc086-162">Press F5 to run the project in debug mode.</span></span> <span data-ttu-id="cc086-163">HTML 頁面會在瀏覽器實例中載入，並提示您輸入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="cc086-163">The HTML page loads in a browser instance and prompts for a user name.</span></span>

    ![輸入使用者名稱](tutorial-getting-started-with-signalr/_static/image5.png)
2. <span data-ttu-id="cc086-165">輸入使用者稱。</span><span class="sxs-lookup"><span data-stu-id="cc086-165">Enter a user name.</span></span>
3. <span data-ttu-id="cc086-166">從瀏覽器的位址行複製 URL，並用它來開啟兩個以上的瀏覽器實例。</span><span class="sxs-lookup"><span data-stu-id="cc086-166">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="cc086-167">在每個瀏覽器實例中，輸入唯一的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="cc086-167">In each browser instance, enter a unique user name.</span></span>
4. <span data-ttu-id="cc086-168">在每個瀏覽器實例中新增批註，然後按一下 [**傳送**]。</span><span class="sxs-lookup"><span data-stu-id="cc086-168">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="cc086-169">批註應該會顯示在所有瀏覽器實例中。</span><span class="sxs-lookup"><span data-stu-id="cc086-169">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="cc086-170">這個簡單的聊天應用程式不會維護伺服器上的討論內容。</span><span class="sxs-lookup"><span data-stu-id="cc086-170">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="cc086-171">中樞會將批註廣播給所有目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="cc086-171">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="cc086-172">稍後加入交談的使用者會看到從他們加入的時間新增的訊息。</span><span class="sxs-lookup"><span data-stu-id="cc086-172">Users who join the chat later will see messages added from the time they join.</span></span>

    <span data-ttu-id="cc086-173">下列螢幕擷取畫面顯示在三個瀏覽器實例中執行的聊天應用程式，其中的每個實例都會在傳送訊息時進行更新：</span><span class="sxs-lookup"><span data-stu-id="cc086-173">The following screen shot shows the chat application running in three browser instances, all of which are updated when one instance sends a message:</span></span>

    ![聊天瀏覽器](tutorial-getting-started-with-signalr/_static/image6.png)
5. <span data-ttu-id="cc086-175">在**方案總管**中，檢查執行中應用程式的 [**指令檔**] 節點。</span><span class="sxs-lookup"><span data-stu-id="cc086-175">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="cc086-176">有一個名為**hub**的腳本檔案，SignalR 程式庫會在執行時間動態產生此檔案。</span><span class="sxs-lookup"><span data-stu-id="cc086-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="cc086-177">這個檔案會管理 jQuery 腳本與伺服器端程式碼之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="cc086-177">This file manages the communication between jQuery script and server-side code.</span></span>

    ![產生的中樞腳本](tutorial-getting-started-with-signalr/_static/image7.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="cc086-179">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="cc086-179">Examine the Code</span></span>

<span data-ttu-id="cc086-180">SignalR chat 應用程式會示範兩個基本的 SignalR 開發工作：建立中樞做為伺服器上的主要協調物件，以及使用 SignalR jQuery 程式庫來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="cc086-180">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="cc086-181">SignalR 中樞</span><span class="sxs-lookup"><span data-stu-id="cc086-181">SignalR Hubs</span></span>

<span data-ttu-id="cc086-182">在程式碼範例中， **ChatHub**類別衍生自**SignalR**類別。</span><span class="sxs-lookup"><span data-stu-id="cc086-182">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="cc086-183">從**中樞**類別衍生的是建立 SignalR 應用程式的實用方式。</span><span class="sxs-lookup"><span data-stu-id="cc086-183">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="cc086-184">您可以在中樞類別上建立公用方法，然後從網頁中的 jQuery 腳本呼叫這些方法來存取這些方法。</span><span class="sxs-lookup"><span data-stu-id="cc086-184">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="cc086-185">在聊天程式碼中，用戶端會呼叫**ChatHub** ，以傳送新的訊息。</span><span class="sxs-lookup"><span data-stu-id="cc086-185">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="cc086-186">接著，中樞會藉由呼叫**broadcastMessage**，將訊息傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="cc086-186">The hub in turn sends the message to all clients by calling **Clients.All.broadcastMessage**.</span></span>

<span data-ttu-id="cc086-187">**Send**方法會示範數個中樞概念：</span><span class="sxs-lookup"><span data-stu-id="cc086-187">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="cc086-188">在中樞上宣告公用方法，讓用戶端可以呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="cc086-188">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="cc086-189">使用**SignalR**動態屬性來存取連線至此中樞的所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="cc086-189">Use the **Microsoft.AspNet.SignalR.Hub.Clients** dynamic property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="cc086-190">呼叫用戶端上的 jQuery 函式（例如 `broadcastMessage` 函數）來更新用戶端。</span><span class="sxs-lookup"><span data-stu-id="cc086-190">Call a jQuery function on the client (such as the `broadcastMessage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="cc086-191">SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="cc086-191">SignalR and jQuery</span></span>

<span data-ttu-id="cc086-192">程式碼範例中的 HTML 網頁會示範如何使用 SignalR jQuery 程式庫來與 SignalR 中樞進行通訊。</span><span class="sxs-lookup"><span data-stu-id="cc086-192">The HTML page in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="cc086-193">程式碼中的基本工作是宣告 proxy 來參考中樞、宣告伺服器可以呼叫的函式，將內容推送至用戶端，以及啟動連線以將訊息傳送至中樞。</span><span class="sxs-lookup"><span data-stu-id="cc086-193">The essential tasks in the code are declaring a proxy to reference the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="cc086-194">下列程式碼會宣告中樞的 proxy。</span><span class="sxs-lookup"><span data-stu-id="cc086-194">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="cc086-195">在 jQuery 中，伺服器類別及其成員的參考是 camel 大小寫。</span><span class="sxs-lookup"><span data-stu-id="cc086-195">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="cc086-196">此程式碼範例會C#將 jQuery 中的**ChatHub**類別參考為**ChatHub**。</span><span class="sxs-lookup"><span data-stu-id="cc086-196">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span>

<span data-ttu-id="cc086-197">下列程式碼是您在腳本中建立回呼函數的方式。</span><span class="sxs-lookup"><span data-stu-id="cc086-197">The following code is how you create a callback function in the script.</span></span> <span data-ttu-id="cc086-198">伺服器上的中樞類別會呼叫此函式，將內容更新推送至每個用戶端。</span><span class="sxs-lookup"><span data-stu-id="cc086-198">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="cc086-199">在顯示內容之前進行 HTML 編碼的兩行程式碼是選擇性的，而且會顯示一個簡單的方法來防止腳本插入。</span><span class="sxs-lookup"><span data-stu-id="cc086-199">The two lines that HTML encode the content before displaying it are optional and show a simple way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr/samples/sample7.html)]

<span data-ttu-id="cc086-200">下列程式碼顯示如何開啟與中樞的連線。</span><span class="sxs-lookup"><span data-stu-id="cc086-200">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="cc086-201">程式碼會啟動連接，然後將函式傳遞給它，以處理 HTML 網頁中 [**傳送**] 按鈕上的 click 事件。</span><span class="sxs-lookup"><span data-stu-id="cc086-201">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the HTML page.</span></span>

> [!NOTE]
> <span data-ttu-id="cc086-202">這個方法可確保在事件處理常式執行之前就已建立連接。</span><span class="sxs-lookup"><span data-stu-id="cc086-202">This approach insures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="cc086-203">後續步驟</span><span class="sxs-lookup"><span data-stu-id="cc086-203">Next Steps</span></span>

<span data-ttu-id="cc086-204">您已瞭解 SignalR 是用來建立即時 web 應用程式的架構。</span><span class="sxs-lookup"><span data-stu-id="cc086-204">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="cc086-205">您也學到幾個 SignalR 的開發工作：如何將 SignalR 新增至 ASP.NET 應用程式、如何建立中樞類別，以及如何從中樞傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="cc086-205">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="cc086-206">您可以透過將範例應用程式部署至主機服務提供者，在本教學課程或透過網際網路提供的其他 SignalR 應用程式中進行。</span><span class="sxs-lookup"><span data-stu-id="cc086-206">You can make the sample application in this tutorial or other SignalR applications available over the Internet by deploying them to a hosting provider.</span></span> <span data-ttu-id="cc086-207">Microsoft 在免費的[Windows Azure 試用帳戶](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604)中，最多可為10個網站提供免費的 web 主機。</span><span class="sxs-lookup"><span data-stu-id="cc086-207">Microsoft offers free web hosting for up to 10 web sites in a free [Windows Azure trial account](https://www.windowsazure.com/pricing/free-trial/?WT.mc_id=A443DD604).</span></span> <span data-ttu-id="cc086-208">如需如何部署範例 SignalR 應用程式的逐步解說，請參閱[將 SignalR 消費者入門範例發佈為 Windows Azure 網站](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx)。</span><span class="sxs-lookup"><span data-stu-id="cc086-208">For a walkthrough on how to deploy the sample SignalR application, see [Publish the SignalR Getting Started Sample as a Windows Azure Web Site](https://blogs.msdn.com/b/timlee/archive/2013/02/27/deploy-the-signalr-getting-started-sample-as-a-windows-azure-web-site.aspx).</span></span> <span data-ttu-id="cc086-209">如需如何將 Visual Studio Web 專案部署至 Windows Azure 網站的詳細資訊，請參閱將[ASP.NET 應用程式部署至 Windows azure](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet)網站。</span><span class="sxs-lookup"><span data-stu-id="cc086-209">For detailed information about how to deploy a Visual Studio web project to a Windows Azure Web Site, see [Deploying an ASP.NET Application to a Windows Azure Web Site](https://docs.microsoft.com/azure/app-service-web/app-service-web-get-started-dotnet).</span></span> <span data-ttu-id="cc086-210">（注意：目前不支援 Windows Azure 網站的 WebSocket 傳輸。</span><span class="sxs-lookup"><span data-stu-id="cc086-210">(Note: The WebSocket transport is not currently supported for Windows Azure Web Sites.</span></span> <span data-ttu-id="cc086-211">當 WebSocket 傳輸無法使用時，SignalR 會使用其他可用的傳輸，如[SignalR 簡介主題](index.md)的傳輸一節中所述）。</span><span class="sxs-lookup"><span data-stu-id="cc086-211">When WebSocket transport is not available, SignalR uses the other available transports as described in the Transports section of the [Introduction to SignalR topic](index.md).)</span></span>

<span data-ttu-id="cc086-212">若要深入瞭解更先進的 SignalR 開發概念，請造訪下列網站以取得 SignalR 原始程式碼和資源：</span><span class="sxs-lookup"><span data-stu-id="cc086-212">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources:</span></span>

- [<span data-ttu-id="cc086-213">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="cc086-213">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="cc086-214">SignalR Github 和範例</span><span class="sxs-lookup"><span data-stu-id="cc086-214">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="cc086-215">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="cc086-215">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
