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
# <a name="tutorial-getting-started-with-signalr-1x-and-mvc-4"></a><span data-ttu-id="80b87-103">教學課程：使用 SignalR 1.x 和 MVC 4 消費者入門</span><span class="sxs-lookup"><span data-stu-id="80b87-103">Tutorial: Getting Started with SignalR 1.x and MVC 4</span></span>

<span data-ttu-id="80b87-104">[Fletcher](https://github.com/pfletcher)的[Tim Teebken](https://github.com/timlt)</span><span class="sxs-lookup"><span data-stu-id="80b87-104">by [Patrick Fletcher](https://github.com/pfletcher), [Tim Teebken](https://github.com/timlt)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> <span data-ttu-id="80b87-105">本教學課程說明如何使用 ASP.NET SignalR 來建立即時聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="80b87-105">This tutorial shows how to use ASP.NET SignalR to create a real-time chat application.</span></span> <span data-ttu-id="80b87-106">您會將 SignalR 新增至 MVC 4 應用程式，並建立聊天視圖來傳送和顯示訊息。</span><span class="sxs-lookup"><span data-stu-id="80b87-106">You will add SignalR to an MVC 4 application and create a chat view to send and display messages.</span></span>

## <a name="overview"></a><span data-ttu-id="80b87-107">概觀</span><span class="sxs-lookup"><span data-stu-id="80b87-107">Overview</span></span>

<span data-ttu-id="80b87-108">本教學課程將為您介紹如何使用 ASP.NET SignalR 和 ASP.NET MVC 4 進行即時 web 應用程式開發。</span><span class="sxs-lookup"><span data-stu-id="80b87-108">This tutorial introduces you to real-time web application development with ASP.NET SignalR and ASP.NET MVC 4.</span></span> <span data-ttu-id="80b87-109">本教學課程使用與[SignalR 消費者入門教學](tutorial-getting-started-with-signalr.md)課程相同的聊天應用程式代碼，但會示範如何將它新增至以網際網路範本為基礎的 MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="80b87-109">The tutorial uses the same chat application code as the [SignalR Getting Started tutorial](tutorial-getting-started-with-signalr.md), but shows how to add it to an MVC 4 application based on the Internet template.</span></span>

<span data-ttu-id="80b87-110">在本主題中，您將瞭解下列 SignalR 開發工作：</span><span class="sxs-lookup"><span data-stu-id="80b87-110">In this topic you will learn the following SignalR development tasks:</span></span>

- <span data-ttu-id="80b87-111">將 SignalR 程式庫新增至 MVC 4 應用程式。</span><span class="sxs-lookup"><span data-stu-id="80b87-111">Adding the SignalR library to an MVC 4 application.</span></span>
- <span data-ttu-id="80b87-112">建立中樞類別以將內容推送至用戶端。</span><span class="sxs-lookup"><span data-stu-id="80b87-112">Creating a hub class to push content to clients.</span></span>
- <span data-ttu-id="80b87-113">使用網頁中的 SignalR jQuery 程式庫來傳送訊息，並從中樞顯示更新。</span><span class="sxs-lookup"><span data-stu-id="80b87-113">Using the SignalR jQuery library in a web page to send messages and display updates from the hub.</span></span>

<span data-ttu-id="80b87-114">下列螢幕擷取畫面顯示在瀏覽器中執行的已完成聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="80b87-114">The following screen shot shows the completed chat application running in a browser.</span></span>

![聊天實例](tutorial-getting-started-with-signalr-and-mvc-4/_static/image2.png)

<span data-ttu-id="80b87-116">各節</span><span class="sxs-lookup"><span data-stu-id="80b87-116">Sections:</span></span>

- [<span data-ttu-id="80b87-117">設定專案</span><span class="sxs-lookup"><span data-stu-id="80b87-117">Set up the Project</span></span>](#setup)
- [<span data-ttu-id="80b87-118">執行範例</span><span class="sxs-lookup"><span data-stu-id="80b87-118">Run the Sample</span></span>](#run)
- [<span data-ttu-id="80b87-119">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="80b87-119">Examine the Code</span></span>](#code)
- [<span data-ttu-id="80b87-120">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80b87-120">Next Steps</span></span>](#next)

<a id="setup"></a>

## <a name="set-up-the-project"></a><span data-ttu-id="80b87-121">設定專案</span><span class="sxs-lookup"><span data-stu-id="80b87-121">Set up the Project</span></span>

<span data-ttu-id="80b87-122">必要條件：</span><span class="sxs-lookup"><span data-stu-id="80b87-122">Prerequisites:</span></span>

- <span data-ttu-id="80b87-123">Visual Studio 2010 SP1、Visual Studio 2012 或 Visual Studio 2012 Express。</span><span class="sxs-lookup"><span data-stu-id="80b87-123">Visual Studio 2010 SP1, Visual Studio 2012, or Visual Studio 2012 Express.</span></span> <span data-ttu-id="80b87-124">如果您沒有 Visual Studio，請參閱[ASP.NET 下載](https://www.asp.net/downloads)以取得免費的 Visual Studio 2012 Express 開發工具。</span><span class="sxs-lookup"><span data-stu-id="80b87-124">If you do not have Visual Studio, see [ASP.NET Downloads](https://www.asp.net/downloads) to get the free Visual Studio 2012 Express Development Tool.</span></span>
- <span data-ttu-id="80b87-125">針對 Visual Studio 2010，請安裝[ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683)。</span><span class="sxs-lookup"><span data-stu-id="80b87-125">For Visual Studio 2010, install [ASP.NET MVC 4](https://www.microsoft.com/download/details.aspx?id=30683).</span></span>

<span data-ttu-id="80b87-126">本節說明如何建立 ASP.NET MVC 4 應用程式、新增 SignalR 程式庫，以及建立聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="80b87-126">This section shows how to create an ASP.NET MVC 4 application, add the SignalR library, and create the chat application.</span></span>

1. 1. <span data-ttu-id="80b87-127">在 Visual Studio 建立 ASP.NET MVC 4 應用程式，將其命名為 SignalRChat，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="80b87-127">In Visual Studio create an ASP.NET MVC 4 application, name it SignalRChat, and click OK.</span></span>

        > [!NOTE]
        > <span data-ttu-id="80b87-128">在 VS 2010 中，選取 [Framework 版本] 下拉式控制項中的 [ **.NET Framework 4** ]。</span><span class="sxs-lookup"><span data-stu-id="80b87-128">In VS 2010, select **.NET Framework 4** in the Framework version dropdown control.</span></span> <span data-ttu-id="80b87-129">SignalR 程式碼會在 .NET Framework 版本4和4.5 上執行。</span><span class="sxs-lookup"><span data-stu-id="80b87-129">SignalR code runs on .NET Framework versions 4 and 4.5.</span></span>

        ![建立 mvc web](tutorial-getting-started-with-signalr-and-mvc-4/_static/image3.png)
      2. <span data-ttu-id="80b87-131">選取 [網際網路應用程式] 範本，清除 [**建立單元測試專案**] 選項，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="80b87-131">Select the Internet Application template, clear the option to **Create a unit test project**, and click OK.</span></span>

         ![建立 mvc 網際網路網站](tutorial-getting-started-with-signalr-and-mvc-4/_static/image4.png)
      3. <span data-ttu-id="80b87-133">開啟 [**工具] > NuGet 套件管理員 > [套件管理員主控台**]，然後執行下列命令。</span><span class="sxs-lookup"><span data-stu-id="80b87-133">Open the **Tools > NuGet Package Manager > Package Manager Console** and run the following command.</span></span> <span data-ttu-id="80b87-134">此步驟會將一組腳本檔案和元件參考加入至專案，以啟用 SignalR 功能。</span><span class="sxs-lookup"><span data-stu-id="80b87-134">This step adds to the project a set of script files and assembly references that enable SignalR functionality.</span></span>

         `install-package Microsoft.AspNet.SignalR -Version 1.1.3`
      4. <span data-ttu-id="80b87-135">在**方案總管**展開 [腳本] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="80b87-135">In **Solution Explorer** expand the Scripts folder.</span></span> <span data-ttu-id="80b87-136">請注意，SignalR 的腳本程式庫已加入至專案。</span><span class="sxs-lookup"><span data-stu-id="80b87-136">Note that script libraries for SignalR have been added to the project.</span></span>

         ![程式庫參考](tutorial-getting-started-with-signalr-and-mvc-4/_static/image6.png)
      5. <span data-ttu-id="80b87-138">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增] |新增資料夾**，然後新增名為**hub**的新資料夾。</span><span class="sxs-lookup"><span data-stu-id="80b87-138">In **Solution Explorer**, right-click the project, select **Add | New Folder**, and add a new folder named **Hubs**.</span></span>
      6. <span data-ttu-id="80b87-139">以滑鼠右鍵按一下 [**中樞**] 資料夾，然後按一下 [**新增] |類別**，並建立名為C# **ChatHub.cs**的新類別。</span><span class="sxs-lookup"><span data-stu-id="80b87-139">Right-click the **Hubs** folder, click **Add | Class**, and create a new C# class named **ChatHub.cs**.</span></span> <span data-ttu-id="80b87-140">您將使用此類別做為 SignalR 伺服器中樞，以將訊息傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="80b87-140">You will use this class as a SignalR server hub that sends messages to all clients.</span></span>

> [!NOTE]
> <span data-ttu-id="80b87-141">如果您使用 Visual Studio 2012，並已安裝[ASP.NET 和 Web 工具2012.2 更新](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation)，您可以使用 [新增 SignalR 專案] 範本來建立中樞類別。</span><span class="sxs-lookup"><span data-stu-id="80b87-141">If you use Visual Studio 2012 and have installed the [ASP.NET and Web Tools 2012.2 update](../../../visual-studio/overview/2012/aspnet-and-web-tools-20122-release-notes-rtw.md#_Installation), you can use the new SignalR item template to create the hub class.</span></span> <span data-ttu-id="80b87-142">若要這麼做，請以滑鼠右鍵按一下 **中樞** 資料夾，然後按一下 **新增 |新增專案**，選取  **SignalR Hub Class （v1）** ，並將類別命名為**ChatHub.cs**。</span><span class="sxs-lookup"><span data-stu-id="80b87-142">To do that, right-click the **Hubs** folder, click **Add | New Item**, select **SignalR Hub Class (v1)**, and name the class **ChatHub.cs**.</span></span>

1. <span data-ttu-id="80b87-143">將**ChatHub**類別中的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="80b87-143">Replace the code in the **ChatHub** class with the following code.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample1.cs)]
2. <span data-ttu-id="80b87-144">開啟專案的**global.asax**檔案，並將呼叫新增至方法 `RouteTable.Routes.MapHubs();` 做為 `Application_Start` 方法中的第一行程式碼。</span><span class="sxs-lookup"><span data-stu-id="80b87-144">Open the **Global.asax** file for the project, and add a call to the method `RouteTable.Routes.MapHubs();` as the first line of code in the `Application_Start` method.</span></span> <span data-ttu-id="80b87-145">此程式碼會註冊 SignalR 中樞的預設路由，而且必須在註冊任何其他路由之前呼叫。</span><span class="sxs-lookup"><span data-stu-id="80b87-145">This code registers the default route for SignalR hubs and must be called before you register any other routes.</span></span> <span data-ttu-id="80b87-146">完成的 `Application_Start` 方法如下列範例所示。</span><span class="sxs-lookup"><span data-stu-id="80b87-146">The completed `Application_Start` method looks like the following example.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample2.cs)]
3. <span data-ttu-id="80b87-147">編輯在 controller **/HomeController**中找到的 `HomeController` 類別，並將下列方法新增至類別。</span><span class="sxs-lookup"><span data-stu-id="80b87-147">Edit the `HomeController` class found in **Controllers/HomeController.cs** and add the following method to the class.</span></span> <span data-ttu-id="80b87-148">這個方法會傳回您將在稍後步驟中建立的**聊天**視圖。</span><span class="sxs-lookup"><span data-stu-id="80b87-148">This method returns the **Chat** view that you will create in a later step.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample3.cs)]
4. <span data-ttu-id="80b87-149">以滑鼠右鍵按一下您剛才建立的 `Chat` 方法，然後按一下 [**新增視圖**] 以建立新的視圖檔案。</span><span class="sxs-lookup"><span data-stu-id="80b87-149">Right-click within the `Chat` method you just created, and click **Add View** to create a new view file.</span></span>
5. <span data-ttu-id="80b87-150">在 [**加入視圖**] 對話方塊中，確定已選取核取方塊以**使用版面配置或主版頁面**（清除其他核取方塊），然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="80b87-150">In the **Add View** dialog, make sure the check box is selected to **Use a layout or master page** (clear the other check boxes), and then click **Add**.</span></span>

    ![新增檢視](tutorial-getting-started-with-signalr-and-mvc-4/_static/image8.png)
6. <span data-ttu-id="80b87-152">編輯名為**Chat**的新視圖檔案。</span><span class="sxs-lookup"><span data-stu-id="80b87-152">Edit the new view file named **Chat.cshtml**.</span></span> <span data-ttu-id="80b87-153">在 &lt;h2&gt; 標記之後，將下列 &lt;div&gt; 區段和 `@section scripts` 程式碼區塊貼到頁面中。</span><span class="sxs-lookup"><span data-stu-id="80b87-153">After the &lt;h2&gt; tag, paste the following &lt;div&gt; section and `@section scripts` code block into the page.</span></span> <span data-ttu-id="80b87-154">此腳本可讓頁面傳送聊天訊息，並顯示來自伺服器的訊息。</span><span class="sxs-lookup"><span data-stu-id="80b87-154">This script enables the page to send chat messages and display messages from the server.</span></span> <span data-ttu-id="80b87-155">聊天視圖的完整程式碼會出現在下列程式碼區塊中。</span><span class="sxs-lookup"><span data-stu-id="80b87-155">The complete code for the chat view appears in the following code block.</span></span>

    > [!IMPORTANT]
    > <span data-ttu-id="80b87-156">當您將 SignalR 和其他腳本程式庫加入 Visual Studio 專案時，封裝管理員可能會安裝比本主題中所示版本還新的腳本版本。</span><span class="sxs-lookup"><span data-stu-id="80b87-156">When you add SignalR and other script libraries to your Visual Studio project, the Package Manager might install versions of the scripts that are more recent than the versions shown in this topic.</span></span> <span data-ttu-id="80b87-157">請確定程式碼中的腳本參考，符合您的專案中所安裝的腳本程式庫版本。</span><span class="sxs-lookup"><span data-stu-id="80b87-157">Make sure that the script references in your code match the versions of the script libraries installed in your project.</span></span>

    [!code-cshtml[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample4.cshtml)]
7. <span data-ttu-id="80b87-158">**全部儲存**專案。</span><span class="sxs-lookup"><span data-stu-id="80b87-158">**Save All** for the project.</span></span>

<a id="run"></a>

## <a name="run-the-sample"></a><span data-ttu-id="80b87-159">執行範例</span><span class="sxs-lookup"><span data-stu-id="80b87-159">Run the Sample</span></span>

1. <span data-ttu-id="80b87-160">按 F5 以在 [調試] 模式中執行專案。</span><span class="sxs-lookup"><span data-stu-id="80b87-160">Press F5 to run the project in debug mode.</span></span>
2. <span data-ttu-id="80b87-161">在瀏覽器位址行中，將 **/home/chat**附加至專案的預設頁面 URL。</span><span class="sxs-lookup"><span data-stu-id="80b87-161">In the browser address line, append **/home/chat** to the URL of the default page for the project.</span></span> <span data-ttu-id="80b87-162">聊天頁面會在瀏覽器實例中載入，並提示您輸入使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="80b87-162">The Chat page loads in a browser instance and prompts for a user name.</span></span>

    ![輸入使用者名稱](tutorial-getting-started-with-signalr-and-mvc-4/_static/image9.png)
3. <span data-ttu-id="80b87-164">輸入使用者稱。</span><span class="sxs-lookup"><span data-stu-id="80b87-164">Enter a user name.</span></span>
4. <span data-ttu-id="80b87-165">從瀏覽器的位址行複製 URL，並用它來開啟兩個以上的瀏覽器實例。</span><span class="sxs-lookup"><span data-stu-id="80b87-165">Copy the URL from the address line of the browser and use it to open two more browser instances.</span></span> <span data-ttu-id="80b87-166">在每個瀏覽器實例中，輸入唯一的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="80b87-166">In each browser instance, enter a unique user name.</span></span>
5. <span data-ttu-id="80b87-167">在每個瀏覽器實例中新增批註，然後按一下 [**傳送**]。</span><span class="sxs-lookup"><span data-stu-id="80b87-167">In each browser instance, add a comment and click **Send**.</span></span> <span data-ttu-id="80b87-168">批註應該會顯示在所有瀏覽器實例中。</span><span class="sxs-lookup"><span data-stu-id="80b87-168">The comments should display in all browser instances.</span></span>

    > [!NOTE]
    > <span data-ttu-id="80b87-169">這個簡單的聊天應用程式不會維護伺服器上的討論內容。</span><span class="sxs-lookup"><span data-stu-id="80b87-169">This simple chat application does not maintain the discussion context on the server.</span></span> <span data-ttu-id="80b87-170">中樞會將批註廣播給所有目前的使用者。</span><span class="sxs-lookup"><span data-stu-id="80b87-170">The hub broadcasts comments to all current users.</span></span> <span data-ttu-id="80b87-171">稍後加入交談的使用者會看到從他們加入的時間新增的訊息。</span><span class="sxs-lookup"><span data-stu-id="80b87-171">Users who join the chat later will see messages added from the time they join.</span></span>
6. <span data-ttu-id="80b87-172">下列螢幕擷取畫面顯示在瀏覽器中執行的聊天應用程式。</span><span class="sxs-lookup"><span data-stu-id="80b87-172">The following screen shot shows the chat application running in a browser.</span></span>

    ![聊天瀏覽器](tutorial-getting-started-with-signalr-and-mvc-4/_static/image11.png)
7. <span data-ttu-id="80b87-174">在**方案總管**中，檢查執行中應用程式的 [**指令檔**] 節點。</span><span class="sxs-lookup"><span data-stu-id="80b87-174">In **Solution Explorer**, inspect the **Script Documents** node for the running application.</span></span> <span data-ttu-id="80b87-175">如果您使用 Internet Explorer 作為瀏覽器，此節點會顯示在 [偵錯工具] 模式中。</span><span class="sxs-lookup"><span data-stu-id="80b87-175">This node is visible in debug mode if you are using Internet Explorer as your browser.</span></span> <span data-ttu-id="80b87-176">有一個名為**hub**的腳本檔案，SignalR 程式庫會在執行時間動態產生此檔案。</span><span class="sxs-lookup"><span data-stu-id="80b87-176">There is a script file named **hubs** that the SignalR library dynamically generates at runtime.</span></span> <span data-ttu-id="80b87-177">這個檔案會管理 jQuery 腳本與伺服器端程式碼之間的通訊。</span><span class="sxs-lookup"><span data-stu-id="80b87-177">This file manages the communication between jQuery script and server-side code.</span></span> <span data-ttu-id="80b87-178">如果您使用 Internet Explorer 以外的瀏覽器，您也可以直接流覽至動態**中樞**檔案（例如 http://mywebsite/signalr/hubs）來存取該檔案。</span><span class="sxs-lookup"><span data-stu-id="80b87-178">If you use a browser other than Internet Explorer, you can also access the dynamic **hubs** file by browsing to it directly, for example http://mywebsite/signalr/hubs.</span></span>

    ![產生的中樞腳本](tutorial-getting-started-with-signalr-and-mvc-4/_static/image13.png)

<a id="code"></a>

## <a name="examine-the-code"></a><span data-ttu-id="80b87-180">檢查程式碼</span><span class="sxs-lookup"><span data-stu-id="80b87-180">Examine the Code</span></span>

<span data-ttu-id="80b87-181">SignalR chat 應用程式會示範兩個基本的 SignalR 開發工作：建立中樞做為伺服器上的主要協調物件，以及使用 SignalR jQuery 程式庫來傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="80b87-181">The SignalR chat application demonstrates two basic SignalR development tasks: creating a hub as the main coordination object on the server, and using the SignalR jQuery library to send and receive messages.</span></span>

### <a name="signalr-hubs"></a><span data-ttu-id="80b87-182">SignalR 中樞</span><span class="sxs-lookup"><span data-stu-id="80b87-182">SignalR Hubs</span></span>

<span data-ttu-id="80b87-183">在程式碼範例中， **ChatHub**類別衍生自**SignalR**類別。</span><span class="sxs-lookup"><span data-stu-id="80b87-183">In the code sample the **ChatHub** class derives from the **Microsoft.AspNet.SignalR.Hub** class.</span></span> <span data-ttu-id="80b87-184">從**中樞**類別衍生的是建立 SignalR 應用程式的實用方式。</span><span class="sxs-lookup"><span data-stu-id="80b87-184">Deriving from the **Hub** class is a useful way to build a SignalR application.</span></span> <span data-ttu-id="80b87-185">您可以在中樞類別上建立公用方法，然後從網頁中的 jQuery 腳本呼叫這些方法來存取這些方法。</span><span class="sxs-lookup"><span data-stu-id="80b87-185">You can create public methods on your hub class and then access those methods by calling them from jQuery scripts in a web page.</span></span>

<span data-ttu-id="80b87-186">在聊天程式碼中，用戶端會呼叫**ChatHub** ，以傳送新的訊息。</span><span class="sxs-lookup"><span data-stu-id="80b87-186">In the chat code, clients call the **ChatHub.Send** method to send a new message.</span></span> <span data-ttu-id="80b87-187">接著，中樞會藉由呼叫**addNewMessageToPage**，將訊息傳送至所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="80b87-187">The hub in turn sends the message to all clients by calling **Clients.All.addNewMessageToPage**.</span></span>

<span data-ttu-id="80b87-188">**Send**方法會示範數個中樞概念：</span><span class="sxs-lookup"><span data-stu-id="80b87-188">The **Send** method demonstrates several hub concepts :</span></span>

- <span data-ttu-id="80b87-189">在中樞上宣告公用方法，讓用戶端可以呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="80b87-189">Declare public methods on a hub so that clients can call them.</span></span>
- <span data-ttu-id="80b87-190">使用**SignalR**來存取連線到此中樞的所有用戶端。</span><span class="sxs-lookup"><span data-stu-id="80b87-190">Use the **Microsoft.AspNet.SignalR.Hub.Clients** property to access all clients connected to this hub.</span></span>
- <span data-ttu-id="80b87-191">呼叫用戶端上的 jQuery 函式（例如 `addNewMessageToPage` 函數）來更新用戶端。</span><span class="sxs-lookup"><span data-stu-id="80b87-191">Call a jQuery function on the client (such as the `addNewMessageToPage` function) to update clients.</span></span>

    [!code-csharp[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample5.cs)]

### <a name="signalr-and-jquery"></a><span data-ttu-id="80b87-192">SignalR 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="80b87-192">SignalR and jQuery</span></span>

<span data-ttu-id="80b87-193">程式碼範例中的**Chat**視圖檔示範如何使用 SignalR jQuery 程式庫與 SignalR 中樞進行通訊。</span><span class="sxs-lookup"><span data-stu-id="80b87-193">The **Chat.cshtml** view file in the code sample shows how to use the SignalR jQuery library to communicate with a SignalR hub.</span></span> <span data-ttu-id="80b87-194">程式碼中的必要工作是建立中樞自動產生的 proxy 參考、宣告伺服器可以呼叫的函式以將內容推送至用戶端，以及啟動連線以將訊息傳送至中樞。</span><span class="sxs-lookup"><span data-stu-id="80b87-194">The essential tasks in the code are creating a reference to the auto-generated proxy for the hub, declaring a function that the server can call to push content to clients, and starting a connection to send messages to the hub.</span></span>

<span data-ttu-id="80b87-195">下列程式碼會宣告中樞的 proxy。</span><span class="sxs-lookup"><span data-stu-id="80b87-195">The following code declares a proxy for a hub.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample6.js)]

> [!NOTE]
> <span data-ttu-id="80b87-196">在 jQuery 中，伺服器類別及其成員的參考是 camel 大小寫。</span><span class="sxs-lookup"><span data-stu-id="80b87-196">In jQuery the reference to the server class and its members is in camel case.</span></span> <span data-ttu-id="80b87-197">此程式碼範例會C#將 jQuery 中的**ChatHub**類別參考為**ChatHub**。</span><span class="sxs-lookup"><span data-stu-id="80b87-197">The code sample references the C# **ChatHub** class in jQuery as **chatHub**.</span></span> <span data-ttu-id="80b87-198">如果您想要使用傳統 Pascal 大小寫來參考 jQuery 中的 `ChatHub` 類別C#，請編輯 ChatHub.cs 類別檔案。</span><span class="sxs-lookup"><span data-stu-id="80b87-198">If you want to reference the `ChatHub` class in jQuery with conventional Pascal casing as you would in C#, edit the ChatHub.cs class file.</span></span> <span data-ttu-id="80b87-199">加入 `using` 語句，以參考 `Microsoft.AspNet.SignalR.Hubs` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="80b87-199">Add a `using` statement to reference the `Microsoft.AspNet.SignalR.Hubs` namespace.</span></span> <span data-ttu-id="80b87-200">然後將 `HubName` 屬性加入 `ChatHub` 類別，例如 `[HubName("ChatHub")]`。</span><span class="sxs-lookup"><span data-stu-id="80b87-200">Then add the `HubName` attribute to the `ChatHub` class, for example `[HubName("ChatHub")]`.</span></span> <span data-ttu-id="80b87-201">最後，將您的 jQuery 參考更新為 `ChatHub` 類別。</span><span class="sxs-lookup"><span data-stu-id="80b87-201">Finally, update your jQuery reference to the `ChatHub` class.</span></span>

<span data-ttu-id="80b87-202">下列程式碼示範如何在腳本中建立回呼函數。</span><span class="sxs-lookup"><span data-stu-id="80b87-202">The following code shows how to create a callback function in the script.</span></span> <span data-ttu-id="80b87-203">伺服器上的中樞類別會呼叫此函式，將內容更新推送至每個用戶端。</span><span class="sxs-lookup"><span data-stu-id="80b87-203">The hub class on the server calls this function to push content updates to each client.</span></span> <span data-ttu-id="80b87-204">`htmlEncode` 函式的選擇性呼叫會顯示在頁面中顯示訊息內容的 HTML 編碼方式，以防止腳本插入。</span><span class="sxs-lookup"><span data-stu-id="80b87-204">The optional call to the `htmlEncode` function shows a way to HTML encode the message content before displaying it in the page, as a way to prevent script injection.</span></span>

[!code-html[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample7.html)]

<span data-ttu-id="80b87-205">下列程式碼顯示如何開啟與中樞的連線。</span><span class="sxs-lookup"><span data-stu-id="80b87-205">The following code shows how to open a connection with the hub.</span></span> <span data-ttu-id="80b87-206">程式碼會啟動連線，然後將函式傳遞至聊天頁面中 [**傳送**] 按鈕上的 [按一下] 事件。</span><span class="sxs-lookup"><span data-stu-id="80b87-206">The code starts the connection and then passes it a function to handle the click event on the **Send** button in the Chat page.</span></span>

> [!NOTE]
> <span data-ttu-id="80b87-207">這種方法可確保在事件處理常式執行之前就已建立連接。</span><span class="sxs-lookup"><span data-stu-id="80b87-207">This approach ensures that the connection is established before the event handler executes.</span></span>

[!code-javascript[Main](tutorial-getting-started-with-signalr-and-mvc-4/samples/sample8.js)]

<a id="next"></a>

## <a name="next-steps"></a><span data-ttu-id="80b87-208">後續步驟</span><span class="sxs-lookup"><span data-stu-id="80b87-208">Next Steps</span></span>

<span data-ttu-id="80b87-209">您已瞭解 SignalR 是用來建立即時 web 應用程式的架構。</span><span class="sxs-lookup"><span data-stu-id="80b87-209">You learned that SignalR is a framework for building real-time web applications.</span></span> <span data-ttu-id="80b87-210">您也學到幾個 SignalR 的開發工作：如何將 SignalR 新增至 ASP.NET 應用程式、如何建立中樞類別，以及如何從中樞傳送和接收訊息。</span><span class="sxs-lookup"><span data-stu-id="80b87-210">You also learned several SignalR development tasks: how to add SignalR to an ASP.NET application, how to create a hub class, and how to send and receive messages from the hub.</span></span>

<span data-ttu-id="80b87-211">若要深入瞭解更先進的 SignalR 開發概念，請造訪下列網站以取得 SignalR 原始程式碼和資源：</span><span class="sxs-lookup"><span data-stu-id="80b87-211">To learn more advanced SignalR developments concepts, visit the following sites for SignalR source code and resources :</span></span>

- [<span data-ttu-id="80b87-212">SignalR 專案</span><span class="sxs-lookup"><span data-stu-id="80b87-212">SignalR Project</span></span>](http://signalr.net)
- [<span data-ttu-id="80b87-213">SignalR Github 和範例</span><span class="sxs-lookup"><span data-stu-id="80b87-213">SignalR Github and Samples</span></span>](https://github.com/SignalR/SignalR)
- [<span data-ttu-id="80b87-214">SignalR Wiki</span><span class="sxs-lookup"><span data-stu-id="80b87-214">SignalR Wiki</span></span>](https://github.com/SignalR/SignalR/wiki)
