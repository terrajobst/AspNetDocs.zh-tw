---
uid: signalr/overview/older-versions/scaleout-with-sql-server
title: 具有 SQL Server 的 SignalR 向外延展（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 1dca7967-8296-444a-9533-837eb284e78c
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-sql-server
msc.type: authoredcontent
ms.openlocfilehash: 8674b06a2a751c9a7b1c6c9b19782974d0602a62
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536467"
---
# <a name="signalr-scaleout-with-sql-server-signalr-1x"></a><span data-ttu-id="7d82f-102">使用 SQL Server 的向外延展 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="7d82f-102">SignalR Scaleout with SQL Server (SignalR 1.x)</span></span>

<span data-ttu-id="7d82f-103">由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="7d82f-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="7d82f-104">在本教學課程中，您將使用 SQL Server 將訊息散發至部署在兩個不同 IIS 實例中的 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d82f-104">In this tutorial, you will use SQL Server to distribute messages across a SignalR application that is deployed in two separate IIS instances.</span></span> <span data-ttu-id="7d82f-105">您也可以在單一測試電腦上執行本教學課程，但若要取得完整的效果，您必須將 SignalR 應用程式部署到兩部以上的伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d82f-105">You can also run this tutorial on a single test machine, but to get the full effect, you need to deploy the SignalR application to two or more servers.</span></span> <span data-ttu-id="7d82f-106">您也必須在其中一部伺服器上，或在個別的專用伺服器上安裝 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="7d82f-106">You must also install SQL Server on one of the servers, or on a separate dedicated server.</span></span> <span data-ttu-id="7d82f-107">另一個選項是使用 Azure 上的 Vm 來執行教學課程。</span><span class="sxs-lookup"><span data-stu-id="7d82f-107">Another option is to run the tutorial using VMs on Azure.</span></span>

![](scaleout-with-sql-server/_static/image1.png)

## <a name="prerequisites"></a><span data-ttu-id="7d82f-108">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7d82f-108">Prerequisites</span></span>

<span data-ttu-id="7d82f-109">Microsoft SQL Server 2005 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="7d82f-109">Microsoft SQL Server 2005 or later.</span></span> <span data-ttu-id="7d82f-110">背板同時支援桌上型電腦和伺服器版本的 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="7d82f-110">The backplane supports both desktop and server editions of SQL Server.</span></span> <span data-ttu-id="7d82f-111">它不支援 SQL Server Compact 版本或 Azure SQL Database。</span><span class="sxs-lookup"><span data-stu-id="7d82f-111">It does not support SQL Server Compact Edition or Azure SQL Database.</span></span> <span data-ttu-id="7d82f-112">（如果您的應用程式裝載在 Azure 上，請考慮改為服務匯流排背板）。</span><span class="sxs-lookup"><span data-stu-id="7d82f-112">(If your application is hosted on Azure, consider the Service Bus backplane instead.)</span></span>

## <a name="overview"></a><span data-ttu-id="7d82f-113">概觀</span><span class="sxs-lookup"><span data-stu-id="7d82f-113">Overview</span></span>

<span data-ttu-id="7d82f-114">在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。</span><span class="sxs-lookup"><span data-stu-id="7d82f-114">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="7d82f-115">建立新的空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d82f-115">Create a new empty database.</span></span> <span data-ttu-id="7d82f-116">背板會在此資料庫中建立必要的資料表。</span><span class="sxs-lookup"><span data-stu-id="7d82f-116">The backplane will create the necessary tables in this database.</span></span>
2. <span data-ttu-id="7d82f-117">將下列 NuGet 套件新增至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="7d82f-117">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="7d82f-118">SignalR</span><span class="sxs-lookup"><span data-stu-id="7d82f-118">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="7d82f-119">SignalR SqlServer</span><span class="sxs-lookup"><span data-stu-id="7d82f-119">Microsoft.AspNet.SignalR.SqlServer</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.SqlServer)
3. <span data-ttu-id="7d82f-120">建立 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d82f-120">Create a SignalR application.</span></span>
4. <span data-ttu-id="7d82f-121">將下列程式碼新增至 global.asax 以設定背板：</span><span class="sxs-lookup"><span data-stu-id="7d82f-121">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-sql-server/samples/sample1.cs)]

## <a name="configure-the-database"></a><span data-ttu-id="7d82f-122">設定資料庫</span><span class="sxs-lookup"><span data-stu-id="7d82f-122">Configure the Database</span></span>

<span data-ttu-id="7d82f-123">決定應用程式是否會使用 Windows 驗證或 SQL Server 驗證來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d82f-123">Decide whether the application will use Windows authentication or SQL Server authentication to access the database.</span></span> <span data-ttu-id="7d82f-124">無論如何，請確定資料庫使用者具有登入、建立架構和建立資料表的許可權。</span><span class="sxs-lookup"><span data-stu-id="7d82f-124">Regardless, make sure the database user has permissions to log in, create schemas, and create tables.</span></span>

<span data-ttu-id="7d82f-125">建立新的資料庫，讓背板使用。</span><span class="sxs-lookup"><span data-stu-id="7d82f-125">Create a new database for the backplane to use.</span></span> <span data-ttu-id="7d82f-126">您可以為資料庫提供任何名稱。</span><span class="sxs-lookup"><span data-stu-id="7d82f-126">You can give the database any name.</span></span> <span data-ttu-id="7d82f-127">您不需要在資料庫中建立任何資料表;背板會建立所需的資料表。</span><span class="sxs-lookup"><span data-stu-id="7d82f-127">You don't need to create any tables in the database; the backplane will create the necessary tables.</span></span>

![](scaleout-with-sql-server/_static/image2.png)

## <a name="enable-service-broker"></a><span data-ttu-id="7d82f-128">啟用 Service Broker</span><span class="sxs-lookup"><span data-stu-id="7d82f-128">Enable Service Broker</span></span>

<span data-ttu-id="7d82f-129">建議您啟用背板資料庫的 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="7d82f-129">It is recommended to enable Service Broker for the backplane database.</span></span> <span data-ttu-id="7d82f-130">Service Broker 在 SQL Server 中提供訊息和佇列的原生支援，讓背板更有效率地接收更新。</span><span class="sxs-lookup"><span data-stu-id="7d82f-130">Service Broker provides native support for messaging and queuing in SQL Server, which lets the backplane receive updates more efficiently.</span></span> <span data-ttu-id="7d82f-131">（不過，背板也可以運作，而不 Service Broker）。</span><span class="sxs-lookup"><span data-stu-id="7d82f-131">(However, the backplane also works without Service Broker.)</span></span>

<span data-ttu-id="7d82f-132">若要檢查是否已啟用 Service Broker，請查詢**sys.databases**目錄檢視中 **\_Broker\_enabled**資料行。</span><span class="sxs-lookup"><span data-stu-id="7d82f-132">To check whether Service Broker is enabled, query the **is\_broker\_enabled** column in the **sys.databases** catalog view.</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample2.sql)]

![](scaleout-with-sql-server/_static/image3.png)

<span data-ttu-id="7d82f-133">若要啟用 Service Broker，請使用下列 SQL 查詢：</span><span class="sxs-lookup"><span data-stu-id="7d82f-133">To enable Service Broker, use the following SQL query:</span></span>

[!code-sql[Main](scaleout-with-sql-server/samples/sample3.sql)]

> [!NOTE]
> <span data-ttu-id="7d82f-134">如果此查詢出現鎖死，請確定沒有任何應用程式連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="7d82f-134">If this query appears to deadlock, make sure there are no applications connected to the DB.</span></span>

<span data-ttu-id="7d82f-135">如果您已啟用追蹤，追蹤也會顯示是否已啟用 Service Broker。</span><span class="sxs-lookup"><span data-stu-id="7d82f-135">If you have enabled tracing, the traces will also show whether Service Broker is enabled.</span></span>

## <a name="create-a-signalr-application"></a><span data-ttu-id="7d82f-136">建立 SignalR 應用程式</span><span class="sxs-lookup"><span data-stu-id="7d82f-136">Create a SignalR Application</span></span>

<span data-ttu-id="7d82f-137">遵循下列其中一個教學課程來建立 SignalR 應用程式：</span><span class="sxs-lookup"><span data-stu-id="7d82f-137">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="7d82f-138">使用 SignalR 消費者入門</span><span class="sxs-lookup"><span data-stu-id="7d82f-138">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="7d82f-139">使用 SignalR 和 MVC 4 的消費者入門</span><span class="sxs-lookup"><span data-stu-id="7d82f-139">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="7d82f-140">接下來，我們將修改聊天應用程式，以支援 SQL Server 的向外延展。</span><span class="sxs-lookup"><span data-stu-id="7d82f-140">Next, we'll modify the chat application to support scaleout with SQL Server.</span></span> <span data-ttu-id="7d82f-141">首先，將 SignalR NuGet 套件新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="7d82f-141">First, add the SignalR.SqlServer NuGet package to your project.</span></span> <span data-ttu-id="7d82f-142">在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="7d82f-142">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7d82f-143">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="7d82f-143">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-sql-server/samples/sample4.ps1)]

<span data-ttu-id="7d82f-144">接下來，開啟 global.asax 檔案。</span><span class="sxs-lookup"><span data-stu-id="7d82f-144">Next, open the Global.asax file.</span></span> <span data-ttu-id="7d82f-145">將下列程式碼新增至**應用程式\_Start**方法：</span><span class="sxs-lookup"><span data-stu-id="7d82f-145">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-sql-server/samples/sample5.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="7d82f-146">部署和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="7d82f-146">Deploy and Run the Application</span></span>

<span data-ttu-id="7d82f-147">準備您的 Windows Server 實例以部署 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7d82f-147">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="7d82f-148">新增 IIS 角色。</span><span class="sxs-lookup"><span data-stu-id="7d82f-148">Add the IIS role.</span></span> <span data-ttu-id="7d82f-149">包含「應用程式開發」功能，包括 WebSocket 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="7d82f-149">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-sql-server/_static/image4.png)

<span data-ttu-id="7d82f-150">也請包含管理服務（列在 [管理工具] 底下）。</span><span class="sxs-lookup"><span data-stu-id="7d82f-150">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-sql-server/_static/image5.png)

<span data-ttu-id="7d82f-151">**安裝 Web Deploy 3.0。**</span><span class="sxs-lookup"><span data-stu-id="7d82f-151">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="7d82f-152">當您執行 IIS 管理員時，它會提示您安裝 Microsoft Web Platform，或者您可以[下載安裝程式](https://go.microsoft.com/fwlink/?LinkId=255386)。</span><span class="sxs-lookup"><span data-stu-id="7d82f-152">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="7d82f-153">在平臺安裝程式中，搜尋 Web Deploy 並安裝 Web Deploy 3。0</span><span class="sxs-lookup"><span data-stu-id="7d82f-153">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-sql-server/_static/image6.png)

<span data-ttu-id="7d82f-154">檢查 Web 管理服務是否正在執行。</span><span class="sxs-lookup"><span data-stu-id="7d82f-154">Check that the Web Management Service is running.</span></span> <span data-ttu-id="7d82f-155">如果沒有，請啟動服務。</span><span class="sxs-lookup"><span data-stu-id="7d82f-155">If not, start the service.</span></span> <span data-ttu-id="7d82f-156">（如果您在 Windows 服務清單中看不到 [Web 管理服務]，請確定您已在新增 IIS 角色時安裝管理服務）。</span><span class="sxs-lookup"><span data-stu-id="7d82f-156">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="7d82f-157">最後，針對 TCP 開啟埠8172。</span><span class="sxs-lookup"><span data-stu-id="7d82f-157">Finally, open port 8172 for TCP.</span></span> <span data-ttu-id="7d82f-158">這是 Web Deploy 工具所使用的埠。</span><span class="sxs-lookup"><span data-stu-id="7d82f-158">This is the port that the Web Deploy tool uses.</span></span>

<span data-ttu-id="7d82f-159">現在您已準備好從開發電腦將 Visual Studio 專案部署到伺服器。</span><span class="sxs-lookup"><span data-stu-id="7d82f-159">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="7d82f-160">在方案總管中，以滑鼠右鍵按一下方案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="7d82f-160">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="7d82f-161">如需 web 部署的詳細檔，請參閱[Visual Studio 和 ASP.NET 的 Web 部署內容對應](../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="7d82f-161">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="7d82f-162">如果您將應用程式部署至兩部伺服器，您可以在另一個瀏覽器視窗中開啟每個實例，並查看每個實例都會收到來自另一個的 SignalR 訊息。</span><span class="sxs-lookup"><span data-stu-id="7d82f-162">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="7d82f-163">（當然，在生產環境中，這兩部伺服器會位於負載平衡器後方）。</span><span class="sxs-lookup"><span data-stu-id="7d82f-163">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-sql-server/_static/image7.png)

<span data-ttu-id="7d82f-164">執行應用程式之後，您可以看到 SignalR 已自動在資料庫中建立資料表：</span><span class="sxs-lookup"><span data-stu-id="7d82f-164">After you run the application, you can see that SignalR has automatically created tables in the database:</span></span>

![](scaleout-with-sql-server/_static/image8.png)

<span data-ttu-id="7d82f-165">SignalR 管理資料表。</span><span class="sxs-lookup"><span data-stu-id="7d82f-165">SignalR manages the tables.</span></span> <span data-ttu-id="7d82f-166">只要您的應用程式已部署，就不要刪除資料列、修改資料表等等。</span><span class="sxs-lookup"><span data-stu-id="7d82f-166">As long as your application is deployed, don't delete rows, modify the table, and so forth.</span></span>
