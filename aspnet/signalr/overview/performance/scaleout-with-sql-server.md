---
uid: signalr/overview/performance/scaleout-with-sql-server
title: 具有 SQL Server 的 SignalR 向外延展 |Microsoft Docs
author: bradygaster
description: 本主題中使用的軟體版本 Visual Studio 2013 .NET 4.5 SignalR 第2版本主題的先前版本，以取得舊版的相關資訊 。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 98358b6e-9139-4239-ba3a-2d7dd74dd664
msc.legacyurl: /signalr/overview/performance/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 709a9ebf8f3396842bee0d87e621c00ae1418ec1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579181"
---
# <a name="signalr-scaleout-with-sql-server"></a><span data-ttu-id="ec6db-103">使用 SQL Server 的向外延展</span><span class="sxs-lookup"><span data-stu-id="ec6db-103">SignalR Scaleout with SQL Server</span></span>

<span data-ttu-id="ec6db-104">由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="ec6db-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="ec6db-105">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="ec6db-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="ec6db-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="ec6db-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="ec6db-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="ec6db-107">.NET 4.5</span></span>
> - <span data-ttu-id="ec6db-108">SignalR 第2版</span><span class="sxs-lookup"><span data-stu-id="ec6db-108">SignalR version 2</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="ec6db-109">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="ec6db-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="ec6db-110">如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="ec6db-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="ec6db-111">問題與意見</span><span class="sxs-lookup"><span data-stu-id="ec6db-111">Questions and comments</span></span>
>
> <span data-ttu-id="ec6db-112">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="ec6db-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="ec6db-113">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="ec6db-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="ec6db-114">在本教學課程中，您將使用 SQL Server 將訊息散發至部署在兩個不同 IIS 實例中的 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec6db-114">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="ec6db-115">您也可以在單一測試電腦上執行本教學課程，但若要取得完整的效果，您必須將 SignalR 應用程式部署到兩部以上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="ec6db-115">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="ec6db-116">您也必須在其中一部伺服器上，或在個別的專用伺服器上安裝 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ec6db-116">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="ec6db-117">另一個選項是使用 Azure 上的 Vm 來執行教學課程。</span><span class="sxs-lookup"><span data-stu-id="ec6db-117">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="ec6db-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="ec6db-118">Prerequisites</span></span>

<span data-ttu-id="ec6db-119">Microsoft SQL Server 2005 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="ec6db-119">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="ec6db-120">背板同時支援桌上型電腦和伺服器版本的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="ec6db-120">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="ec6db-121">它不支援 SQL Server Compact 版本或 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="ec6db-121">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="ec6db-122">（如果您的應用程式裝載在 Azure 上，請考慮改為服務匯流排背板）。</span><span class="sxs-lookup"><span data-stu-id="ec6db-122">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="ec6db-123">概觀</span><span class="sxs-lookup"><span data-stu-id="ec6db-123">Overview</span></span>

<span data-ttu-id="ec6db-124">在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。</span><span class="sxs-lookup"><span data-stu-id="ec6db-124">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="ec6db-125">建立新的空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="ec6db-125">Create a new empty database.</span></span> <span data-ttu-id="ec6db-126">背板會在此資料庫中建立必要的資料表。</span><span class="sxs-lookup"><span data-stu-id="ec6db-126">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="ec6db-127">將下列 NuGet 套件新增至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="ec6db-127">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="ec6db-128">SignalR</span><span class="sxs-lookup"><span data-stu-id="ec6db-128">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="ec6db-129">SignalR SqlServer</span><span class="sxs-lookup"><span data-stu-id="ec6db-129">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="ec6db-130">建立 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec6db-130">Create a SignalR application.</span></span>
4. <span data-ttu-id="ec6db-131">將下列程式碼新增至 Startup.cs 以設定背板：</span><span class="sxs-lookup"><span data-stu-id="ec6db-131">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

   <span data-ttu-id="ec6db-132">這段程式碼會使用[TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx)和[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)的預設值來設定背板。</span><span class="sxs-lookup"><span data-stu-id="ec6db-132">This code configures the backplane with the default values for [TableCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.sqlscaleoutconfiguration.tablecount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="ec6db-133">如需變更這些值的相關資訊，請參閱[SignalR Performance：向外延展計量](signalr-performance.md#scaleout_metrics)。</span><span class="sxs-lookup"><span data-stu-id="ec6db-133">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

## <a name="configure-the-database"></a><span data-ttu-id="ec6db-134">設定資料庫</span><span class="sxs-lookup"><span data-stu-id="ec6db-134">Configure the Database</span></span>

<span data-ttu-id="ec6db-135">決定應用程式是否會使用 Windows 驗證或 SQL Server 驗證來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="ec6db-135">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="ec6db-136">無論如何，請確定資料庫使用者具有登入、建立架構和建立資料表的許可權。</span><span class="sxs-lookup"><span data-stu-id="ec6db-136">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="ec6db-137">建立新的資料庫，讓背板使用。</span><span class="sxs-lookup"><span data-stu-id="ec6db-137">Create a new database for the backplane to use.</span></span> <span data-ttu-id="ec6db-138">您可以為資料庫提供任何名稱。</span><span class="sxs-lookup"><span data-stu-id="ec6db-138">You can give the database any name.</span></span> <span data-ttu-id="ec6db-139">您不需要在資料庫中建立任何資料表;背板會建立所需的資料表。</span><span class="sxs-lookup"><span data-stu-id="ec6db-139">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="ec6db-140">啟用 Service Broker</span><span class="sxs-lookup"><span data-stu-id="ec6db-140">Enable Service Broker</span></span>

<span data-ttu-id="ec6db-141">建議您啟用背板資料庫的 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="ec6db-141">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="ec6db-142">Service Broker 在 SQL Server 中提供訊息和佇列的原生支援，讓背板更有效率地接收更新。</span><span class="sxs-lookup"><span data-stu-id="ec6db-142">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="ec6db-143">（不過，背板也可以運作，而不 Service Broker）。</span><span class="sxs-lookup"><span data-stu-id="ec6db-143">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="ec6db-144">若要檢查是否已啟用 Service Broker，請查詢**sys.databases**目錄檢視中 **\_Broker\_enabled**資料行。</span><span class="sxs-lookup"><span data-stu-id="ec6db-144">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="ec6db-145">若要啟用 Service Broker，請使用下列 SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="ec6db-145">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="ec6db-146">如果此查詢出現鎖死，請確定沒有任何應用程式連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="ec6db-146">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="ec6db-147">如果您已啟用追蹤，追蹤也會顯示是否已啟用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="ec6db-147">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="ec6db-148">建立 SignalR 應用程式</span><span class="sxs-lookup"><span data-stu-id="ec6db-148">Create a SignalR Application</span></span>

<span data-ttu-id="ec6db-149">遵循下列其中一個教學課程來建立 SignalR 應用程式：</span><span class="sxs-lookup"><span data-stu-id="ec6db-149">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="ec6db-150">使用 SignalR 2.0 的消費者入門</span><span class="sxs-lookup"><span data-stu-id="ec6db-150">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="ec6db-151">使用 SignalR 2.0 和 MVC 5 的消費者入門</span><span class="sxs-lookup"><span data-stu-id="ec6db-151">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="ec6db-152">接下來，我們將修改聊天應用程式，以支援 SQL Server 的向外延展。</span><span class="sxs-lookup"><span data-stu-id="ec6db-152">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="ec6db-153">首先，將 SignalR NuGet 套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="ec6db-153">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="ec6db-154">在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="ec6db-154">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="ec6db-155">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="ec6db-155">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="ec6db-156">接下來，開啟 Startup.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="ec6db-156">Next, open the Startup.cs file.</span></span> <span data-ttu-id="ec6db-157">將下列程式碼新增至**Configure**方法：</span><span class="sxs-lookup"><span data-stu-id="ec6db-157">Add the following code to the **Configure** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="ec6db-158">部署和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="ec6db-158">Deploy and Run the Application</span></span>

<span data-ttu-id="ec6db-159">準備您的 Windows Server 實例以部署 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="ec6db-159">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="ec6db-160">新增 IIS 角色。</span><span class="sxs-lookup"><span data-stu-id="ec6db-160">Add the IIS role.</span></span> <span data-ttu-id="ec6db-161">包含「應用程式開發」功能，包括 WebSocket 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="ec6db-161">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="ec6db-162">也請包含管理服務（列在 [管理工具] 底下）。</span><span class="sxs-lookup"><span data-stu-id="ec6db-162">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="ec6db-163">**安裝 Web Deploy 3.0。**</span><span class="sxs-lookup"><span data-stu-id="ec6db-163">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="ec6db-164">當您執行 IIS 管理員時，它會提示您安裝 Microsoft Web Platform，或者您可以[下載安裝程式](https://go.microsoft.com/fwlink/?LinkId=255386)。</span><span class="sxs-lookup"><span data-stu-id="ec6db-164">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="ec6db-165">在平臺安裝程式中，搜尋 Web Deploy 並安裝 Web Deploy 3。0</span><span class="sxs-lookup"><span data-stu-id="ec6db-165">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="ec6db-166">檢查 Web 管理服務是否正在執行。</span><span class="sxs-lookup"><span data-stu-id="ec6db-166">Check that the Web Management Service is running.</span></span> <span data-ttu-id="ec6db-167">如果沒有，請啟動服務。</span><span class="sxs-lookup"><span data-stu-id="ec6db-167">If not, start the service.</span></span> <span data-ttu-id="ec6db-168">（如果您在 Windows 服務清單中看不到 [Web 管理服務]，請確定您已在新增 IIS 角色時安裝管理服務）。</span><span class="sxs-lookup"><span data-stu-id="ec6db-168">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="ec6db-169">最後，針對 TCP 開啟埠8172。</span><span class="sxs-lookup"><span data-stu-id="ec6db-169">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="ec6db-170">這是 Web Deploy 工具所使用的埠。</span><span class="sxs-lookup"><span data-stu-id="ec6db-170">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="ec6db-171">現在您已準備好從開發電腦將 Visual Studio 專案部署到伺服器。</span><span class="sxs-lookup"><span data-stu-id="ec6db-171">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="ec6db-172">在方案總管中，以滑鼠右鍵按一下方案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="ec6db-172">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="ec6db-173">如需 web 部署的詳細檔，請參閱[Visual Studio 和 ASP.NET 的 Web 部署內容對應](../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="ec6db-173">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="ec6db-174">如果您將應用程式部署至兩部伺服器，您可以在另一個瀏覽器視窗中開啟每個實例，並查看每個實例都會收到來自另一個的 SignalR 訊息。</span><span class="sxs-lookup"><span data-stu-id="ec6db-174">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="ec6db-175">（當然，在生產環境中，這兩部伺服器會位於負載平衡器後方）。</span><span class="sxs-lookup"><span data-stu-id="ec6db-175">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="ec6db-176">執行應用程式之後，您可以看到 SignalR 已自動在資料庫中建立資料表：</span><span class="sxs-lookup"><span data-stu-id="ec6db-176">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="ec6db-177">SignalR 管理資料表。</span><span class="sxs-lookup"><span data-stu-id="ec6db-177">SignalR manages the tables.</span></span> <span data-ttu-id="ec6db-178">只要您的應用程式已部署，就不要刪除資料列、修改資料表等等。</span><span class="sxs-lookup"><span data-stu-id="ec6db-178">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
