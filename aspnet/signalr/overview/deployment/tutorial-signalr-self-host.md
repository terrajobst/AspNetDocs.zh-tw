---
uid: signalr/overview/deployment/tutorial-signalr-self-host
title: 教學課程： SignalR 自我裝載 |Microsoft Docs
author: bradygaster
description: 本教學課程說明如何建立自我裝載的 SignalR 2 伺服器，以及如何使用 JavaScript 用戶端連接到它。 教學課程中使用的軟體版本 。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 400db427-27af-4f2f-abf0-5486d5e024b5
msc.legacyurl: /signalr/overview/deployment/tutorial-signalr-self-host
msc.type: authoredcontent
ms.openlocfilehash: 41c8c3803923e76ef238a5c5937cbe7f81e6aa82
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558678"
---
# <a name="tutorial-signalr-self-host"></a><span data-ttu-id="f997d-104">教學課程： SignalR 自我裝載</span><span class="sxs-lookup"><span data-stu-id="f997d-104">Tutorial: SignalR Self-Host</span></span>

<span data-ttu-id="f997d-105">由[派翠克 Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="f997d-105">by [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

[<span data-ttu-id="f997d-106">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="f997d-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/SignalR-Self-Host-Sample-6da0f383)

> <span data-ttu-id="f997d-107">本教學課程說明如何建立自我裝載的 SignalR 2 伺服器，以及如何使用 JavaScript 用戶端連接到它。</span><span class="sxs-lookup"><span data-stu-id="f997d-107">This tutorial shows how to create a self-hosted SignalR 2 server, and how to connect to it with a JavaScript client.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="f997d-108">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="f997d-108">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="f997d-109">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="f997d-109">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="f997d-110">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="f997d-110">.NET 4.5</span></span>
> - <span data-ttu-id="f997d-111">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="f997d-111">SignalR version 2</span></span>
>
>
>
> ## <a name="using-visual-studio-2012-with-this-tutorial"></a><span data-ttu-id="f997d-112">在本教學課程中使用 Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="f997d-112">Using Visual Studio 2012 with this tutorial</span></span>
>
>
> <span data-ttu-id="f997d-113">若要在本教學課程中使用 Visual Studio 2012，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="f997d-113">To use Visual Studio 2012 with this tutorial, do the following:</span></span>
>
> - <span data-ttu-id="f997d-114">將您的[套件管理員](http://docs.nuget.org/docs/start-here/installing-nuget)更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="f997d-114">Update your [Package Manager](http://docs.nuget.org/docs/start-here/installing-nuget) to the latest version.</span></span>
> - <span data-ttu-id="f997d-115">安裝[Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f997d-115">Install the [Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx).</span></span>
> - <span data-ttu-id="f997d-116">在 Web Platform Installer 中，搜尋並安裝**適用于 Visual Studio 2012 的 ASP.NET 和 Web 工具 2013.1**。</span><span class="sxs-lookup"><span data-stu-id="f997d-116">In the Web Platform Installer, search for and install **ASP.NET and Web Tools 2013.1 for Visual Studio 2012**.</span></span> <span data-ttu-id="f997d-117">這會為 SignalR 類別（例如**中樞**）安裝 Visual Studio 範本。</span><span class="sxs-lookup"><span data-stu-id="f997d-117">This will install Visual Studio templates for SignalR classes such as **Hub**.</span></span>
> - <span data-ttu-id="f997d-118">有些範本（例如**OWIN Startup 類別**）將無法使用;為此，請改用類別檔案。</span><span class="sxs-lookup"><span data-stu-id="f997d-118">Some templates (such as **OWIN Startup Class**) will not be available; for these, use a Class file instead.</span></span>
>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="f997d-119">問題與意見</span><span class="sxs-lookup"><span data-stu-id="f997d-119">Questions and comments</span></span>
>
> <span data-ttu-id="f997d-120">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="f997d-120">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="f997d-121">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="f997d-121">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

## <a name="overview"></a><span data-ttu-id="f997d-122">概觀</span><span class="sxs-lookup"><span data-stu-id="f997d-122">Overview</span></span>

<span data-ttu-id="f997d-123">SignalR 伺服器通常裝載于 IIS 中的 ASP.NET 應用程式中，但也可以使用自我裝載程式庫自我裝載（例如主控台應用程式或 Windows 服務）。</span><span class="sxs-lookup"><span data-stu-id="f997d-123">A SignalR server is usually hosted in an ASP.NET application in IIS, but it can also be self-hosted (such as in a console application or Windows service) using the self-host library.</span></span> <span data-ttu-id="f997d-124">此程式庫（例如所有的 SignalR 2）是以 OWIN （[開放式 Web 介面 for .net](http://owin.org)）為基礎。</span><span class="sxs-lookup"><span data-stu-id="f997d-124">This library, like all of SignalR 2, is built on OWIN ([Open Web Interface for .NET](http://owin.org)).</span></span> <span data-ttu-id="f997d-125">OWIN 會定義 .NET web 伺服器和 web 應用程式之間的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="f997d-125">OWIN defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="f997d-126">OWIN 會將 web 應用程式與伺服器分離，讓 OWIN 非常適合在 IIS 以外的進程中自我裝載 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f997d-126">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS.</span></span>

<span data-ttu-id="f997d-127">未在 IIS 中裝載的原因包括：</span><span class="sxs-lookup"><span data-stu-id="f997d-127">Reasons for not hosting in IIS include:</span></span>

- <span data-ttu-id="f997d-128">無法使用或不需要 IIS 的環境，例如不含 IIS 的現有伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="f997d-128">Environments where IIS is not available or desirable, such as an existing server farm without IIS.</span></span>
- <span data-ttu-id="f997d-129">必須避免 IIS 的效能負擔。</span><span class="sxs-lookup"><span data-stu-id="f997d-129">The performance overhead of IIS needs to be avoided.</span></span>
- <span data-ttu-id="f997d-130">SignalR 功能會新增至在 Windows 服務、Azure 背景工作角色或其他進程中執行的現有應用程式。</span><span class="sxs-lookup"><span data-stu-id="f997d-130">SignalR functionality is to be added to an existing application that runs in a Windows Service, Azure worker role, or other process.</span></span>

<span data-ttu-id="f997d-131">如果基於效能考慮，將解決方案開發為自我裝載，建議您也測試裝載于 IIS 中的應用程式，以判斷效能的優勢。</span><span class="sxs-lookup"><span data-stu-id="f997d-131">If a solution is being developed as self-host for performance reasons, it's recommended to also test the application hosted in IIS to determine the performance benefit.</span></span>

<span data-ttu-id="f997d-132">本教學課程包含下列各節：</span><span class="sxs-lookup"><span data-stu-id="f997d-132">This tutorial contains the following sections:</span></span>

- [<span data-ttu-id="f997d-133">建立伺服器</span><span class="sxs-lookup"><span data-stu-id="f997d-133">Creating the server</span></span>](#server)
- [<span data-ttu-id="f997d-134">使用 JavaScript 用戶端存取伺服器</span><span class="sxs-lookup"><span data-stu-id="f997d-134">Accessing the server with a JavaScript client</span></span>](#js)

<a id="server"></a>

## <a name="creating-the-server"></a><span data-ttu-id="f997d-135">建立伺服器</span><span class="sxs-lookup"><span data-stu-id="f997d-135">Creating the server</span></span>

<span data-ttu-id="f997d-136">在本教學課程中，您將建立裝載于主控台應用程式中的伺服器，但伺服器可以裝載于任何類型的進程，例如 Windows 服務或 Azure 背景工作角色。</span><span class="sxs-lookup"><span data-stu-id="f997d-136">In this tutorial, you'll create a server that's hosted in a console application, but the server can be hosted in any sort of process, such as a Windows service or Azure worker role.</span></span> <span data-ttu-id="f997d-137">如需在 Windows 服務中裝載 SignalR 伺服器的範例程式碼，請參閱[Windows 服務中的自我裝載 SignalR](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3)。</span><span class="sxs-lookup"><span data-stu-id="f997d-137">For sample code for hosting a SignalR server in a Windows Service, see [Self-Hosting SignalR in a Windows Service](https://code.msdn.microsoft.com/SignalR-self-hosted-in-6ff7e6c3).</span></span>

1. <span data-ttu-id="f997d-138">以系統管理員許可權開啟 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="f997d-138">Open Visual Studio 2013 with administrator privileges.</span></span> <span data-ttu-id="f997d-139">選取 **[** 檔案]、[**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="f997d-139">Select **File**, **New Project**.</span></span> <span data-ttu-id="f997d-140">在 [**範本**] 窗格中的 [**視覺效果C#**  ] 節點底下選取 [ **Windows** ]，然後選取 [**主控台應用程式**] 範本。</span><span class="sxs-lookup"><span data-stu-id="f997d-140">Select **Windows** under the **Visual C#** node in the **Templates** pane, and select the **Console Application** template.</span></span> <span data-ttu-id="f997d-141">將新專案命名為 "SignalRSelfHost"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="f997d-141">Name the new project "SignalRSelfHost" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image1.png)
2. <span data-ttu-id="f997d-142">選取 **工具** > **nuget 套件管理員** > **套件管理員主控台**，以開啟 nuget 套件管理員主控台。</span><span class="sxs-lookup"><span data-stu-id="f997d-142">Open the NuGet package manager console by selecting **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
3. <span data-ttu-id="f997d-143">在 [套件管理員主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="f997d-143">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample1.ps1)]

    <span data-ttu-id="f997d-144">此命令會將 SignalR 2 自我裝載程式庫新增至專案。</span><span class="sxs-lookup"><span data-stu-id="f997d-144">This command adds the SignalR 2 Self-Host libraries to the project.</span></span>
4. <span data-ttu-id="f997d-145">在 [套件管理員主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="f997d-145">In the package manager console, enter the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample2.ps1)]

    <span data-ttu-id="f997d-146">此命令會將 Owin 程式庫新增至專案。</span><span class="sxs-lookup"><span data-stu-id="f997d-146">This command adds the Microsoft.Owin.Cors library to the project.</span></span> <span data-ttu-id="f997d-147">此程式庫將用於跨網域支援，這對於裝載 SignalR 的應用程式和不同網域中的網頁用戶端而言是必要的。</span><span class="sxs-lookup"><span data-stu-id="f997d-147">This library will be used for cross-domain support, which is required for applications that host SignalR and a web page client in different domains.</span></span> <span data-ttu-id="f997d-148">因為您將在不同的埠上裝載 SignalR 伺服器和 web 用戶端，這表示必須啟用跨網域，才能在這些元件之間進行通訊。</span><span class="sxs-lookup"><span data-stu-id="f997d-148">Since you'll be hosting the SignalR server and the web client on different ports, this means that cross-domain must be enabled for communication between these components.</span></span>
5. <span data-ttu-id="f997d-149">以下列程式碼取代 Program.cs 的內容。</span><span class="sxs-lookup"><span data-stu-id="f997d-149">Replace the contents of Program.cs with the following code.</span></span>

    [!code-csharp[Main](tutorial-signalr-self-host/samples/sample3.cs)]

    <span data-ttu-id="f997d-150">上述程式碼包含三個類別：</span><span class="sxs-lookup"><span data-stu-id="f997d-150">The above code includes three classes:</span></span>

    - <span data-ttu-id="f997d-151">**程式**，包括定義執行主要路徑的**Main**方法。</span><span class="sxs-lookup"><span data-stu-id="f997d-151">**Program**, including the **Main** method defining the primary path of execution.</span></span> <span data-ttu-id="f997d-152">在此方法中，**啟動**類型的 web 應用程式會在指定的 URL （`http://localhost:8080`）啟動。</span><span class="sxs-lookup"><span data-stu-id="f997d-152">In this method, a web application of type **Startup** is started at the specified URL (`http://localhost:8080`).</span></span> <span data-ttu-id="f997d-153">如果端點上需要安全性，則可以執行 SSL。</span><span class="sxs-lookup"><span data-stu-id="f997d-153">If security is required on the endpoint, SSL can be implemented.</span></span> <span data-ttu-id="f997d-154">如需詳細資訊，請參閱[如何：使用 SSL 憑證設定埠](https://msdn.microsoft.com/library/ms733791.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f997d-154">See [How to: Configure a Port with an SSL Certificate](https://msdn.microsoft.com/library/ms733791.aspx) for more information.</span></span>
    - <span data-ttu-id="f997d-155">**啟動**，此類別包含 SignalR 伺服器的設定（本教學課程使用的唯一設定是呼叫 `UseCors`），而呼叫 `MapSignalR`，它會為專案中的任何中樞物件建立路由。</span><span class="sxs-lookup"><span data-stu-id="f997d-155">**Startup**, the class containing the configuration for the SignalR server (the only configuration this tutorial uses is the call to `UseCors`), and the call to `MapSignalR`, which creates routes for any Hub objects in the project.</span></span>
    - <span data-ttu-id="f997d-156">**MyHub**，這是應用程式將提供給用戶端的 SignalR 中樞類別。</span><span class="sxs-lookup"><span data-stu-id="f997d-156">**MyHub**, the SignalR Hub class that the application will provide to clients.</span></span> <span data-ttu-id="f997d-157">此類別具有單一方法**Send**，用戶端會呼叫來將訊息廣播給所有其他已連線的用戶端。</span><span class="sxs-lookup"><span data-stu-id="f997d-157">This class has a single method, **Send**, that clients will call to broadcast a message to all other connected clients.</span></span>
6. <span data-ttu-id="f997d-158">編譯並執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f997d-158">Compile and run the application.</span></span> <span data-ttu-id="f997d-159">伺服器正在執行的位址應該會顯示在主控台視窗中。</span><span class="sxs-lookup"><span data-stu-id="f997d-159">The address that the server is running should show in a console window.</span></span>

    ![](tutorial-signalr-self-host/_static/image2.png)
7. <span data-ttu-id="f997d-160">如果執行因例外狀況 `System.Reflection.TargetInvocationException was unhandled`而失敗，您將需要以系統管理員許可權重新開機 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="f997d-160">If execution fails with the exception `System.Reflection.TargetInvocationException was unhandled`, you will need to restart Visual Studio with administrator privileges.</span></span>
8. <span data-ttu-id="f997d-161">請先停止應用程式，再繼續進行下一節。</span><span class="sxs-lookup"><span data-stu-id="f997d-161">Stop the application before proceeding to the next section.</span></span>

<a id="js"></a>

## <a name="accessing-the-server-with-a-javascript-client"></a><span data-ttu-id="f997d-162">使用 JavaScript 用戶端存取伺服器</span><span class="sxs-lookup"><span data-stu-id="f997d-162">Accessing the server with a JavaScript client</span></span>

<span data-ttu-id="f997d-163">在本節中，您將使用[消費者入門教學](../getting-started/tutorial-getting-started-with-signalr.md)課程中的相同 JavaScript 用戶端。</span><span class="sxs-lookup"><span data-stu-id="f997d-163">In this section, you'll use the same JavaScript client from the [Getting Started tutorial](../getting-started/tutorial-getting-started-with-signalr.md).</span></span> <span data-ttu-id="f997d-164">我們只會對用戶端進行一項修改，也就是明確定義中樞 URL。</span><span class="sxs-lookup"><span data-stu-id="f997d-164">We'll only make one modification to the client, which is to explicitly define the hub URL.</span></span> <span data-ttu-id="f997d-165">使用自我裝載的應用程式時，伺服器可能不一定會與連線 URL 位於相同的位址（因為反向 proxy 和負載平衡器），因此必須明確定義 URL。</span><span class="sxs-lookup"><span data-stu-id="f997d-165">With a self-hosted application, the server may not necessarily be at the same address as the connection URL (due to reverse proxies and load balancers), so the URL needs to be defined explicitly.</span></span>

1. <span data-ttu-id="f997d-166">在**方案總管**中，以滑鼠右鍵按一下方案，然後選取 [**加入**]、[**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="f997d-166">In **Solution Explorer**, right-click on the solution and select **Add**, **New Project**.</span></span> <span data-ttu-id="f997d-167">選取 [ **web** ] 節點，然後選取 [ **ASP.NET web 應用程式**] 範本。</span><span class="sxs-lookup"><span data-stu-id="f997d-167">Select the **Web** node, and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="f997d-168">將專案命名為 "JAVAscriptClient"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="f997d-168">Name the project "JavascriptClient" and click **OK**.</span></span>

    ![](tutorial-signalr-self-host/_static/image3.png)
2. <span data-ttu-id="f997d-169">選取 [**空白**] 範本，並將其餘選項保留為未選取狀態。</span><span class="sxs-lookup"><span data-stu-id="f997d-169">Select the **Empty** template, and leave the remaining options unselected.</span></span> <span data-ttu-id="f997d-170">選取 [**建立專案**]。</span><span class="sxs-lookup"><span data-stu-id="f997d-170">Select **Create Project**.</span></span>

    ![](tutorial-signalr-self-host/_static/image4.png)
3. <span data-ttu-id="f997d-171">在 [套件管理員主控台] 中，選取 [**預設專案**] 下拉式集中的 "JAVAscriptClient" 專案，然後執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="f997d-171">In the package manager console, select the "JavascriptClient" project in the **Default project** drop-down, and execute the following command:</span></span>

    [!code-powershell[Main](tutorial-signalr-self-host/samples/sample4.ps1)]

    <span data-ttu-id="f997d-172">此命令會安裝用戶端中所需的 SignalR 和 JQuery 程式庫。</span><span class="sxs-lookup"><span data-stu-id="f997d-172">This command installs the SignalR and JQuery libraries that you'll need in the client.</span></span>
4. <span data-ttu-id="f997d-173">以滑鼠右鍵按一下您的專案，然後選取 [**加入**]、[**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="f997d-173">Right-click on your project and select **Add**, **New Item**.</span></span> <span data-ttu-id="f997d-174">選取 [ **Web** ] 節點，然後選取 [HTML 網頁]。</span><span class="sxs-lookup"><span data-stu-id="f997d-174">Select the **Web** node, and select HTML Page.</span></span> <span data-ttu-id="f997d-175">將頁面命名為**Default .html**。</span><span class="sxs-lookup"><span data-stu-id="f997d-175">Name the page **Default.html**.</span></span>

    ![](tutorial-signalr-self-host/_static/image5.png)
5. <span data-ttu-id="f997d-176">將新 HTML 網頁的內容取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="f997d-176">Replace the contents of the new HTML page with the following code.</span></span> <span data-ttu-id="f997d-177">確認此處的腳本參考符合專案的 Scripts 資料夾中的腳本。</span><span class="sxs-lookup"><span data-stu-id="f997d-177">Verify that the script references here match the scripts in the Scripts folder of the project.</span></span>

    [!code-html[Main](tutorial-signalr-self-host/samples/sample5.html?highlight=31-32)]

    <span data-ttu-id="f997d-178">下列程式碼（在上述程式碼範例中反白顯示）是您對取得開始教學課程中所使用之用戶端的新增功能（除了將程式碼升級至 SignalR 第2版 Beta 版以外）。</span><span class="sxs-lookup"><span data-stu-id="f997d-178">The following code (highlighted in the code sample above) is the addition that you've made to the client used in the Getting Stared tutorial (in addition to upgrading the code to SignalR version 2 beta).</span></span> <span data-ttu-id="f997d-179">這行程式碼會在伺服器上明確設定 SignalR 的基底連接 URL。</span><span class="sxs-lookup"><span data-stu-id="f997d-179">This line of code explicitly sets the base connection URL for SignalR on the server.</span></span>

    [!code-javascript[Main](tutorial-signalr-self-host/samples/sample6.js)]
6. <span data-ttu-id="f997d-180">以滑鼠右鍵按一下方案，然後選取 [**設定啟始專案**...]。選取 [**多個啟始專案**] 選項按鈕，並將兩個專案的 [**動作**] 設定為 [**啟動**]。</span><span class="sxs-lookup"><span data-stu-id="f997d-180">Right-click on the solution, and select **Set Startup Projects...**. Select the **Multiple startup projects** radio button, and set both projects' **Action** to **Start**.</span></span>

    ![](tutorial-signalr-self-host/_static/image6.png)
7. <span data-ttu-id="f997d-181">以滑鼠右鍵按一下 [預設的 .html]，然後選取 [**設定為起始頁**]。</span><span class="sxs-lookup"><span data-stu-id="f997d-181">Right-click on "Default.html" and select **Set As Start Page**.</span></span>
8. <span data-ttu-id="f997d-182">執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f997d-182">Run the application.</span></span> <span data-ttu-id="f997d-183">隨即會啟動伺服器和頁面。</span><span class="sxs-lookup"><span data-stu-id="f997d-183">The server and page will launch.</span></span> <span data-ttu-id="f997d-184">如果在伺服器啟動之前載入頁面，您可能需要重載網頁（或選取偵錯工具中的 [**繼續**]）。</span><span class="sxs-lookup"><span data-stu-id="f997d-184">You may need to reload the web page (or select **Continue** in the debugger) if the page loads before the server is started.</span></span>
9. <span data-ttu-id="f997d-185">在瀏覽器中，于出現提示時提供使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f997d-185">In the browser, provide a username when prompted.</span></span> <span data-ttu-id="f997d-186">將頁面的 URL 複製到另一個瀏覽器索引標籤或視窗中，並提供不同的使用者名稱。</span><span class="sxs-lookup"><span data-stu-id="f997d-186">Copy the page's URL into another browser tab or window and provide a different username.</span></span> <span data-ttu-id="f997d-187">如消費者入門教學課程所示，您可以將訊息從一個瀏覽器窗格傳送到另一個。</span><span class="sxs-lookup"><span data-stu-id="f997d-187">You will be able to send messages from one browser pane to the other, as in the Getting Started tutorial.</span></span>
