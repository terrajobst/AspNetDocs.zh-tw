---
uid: signalr/overview/performance/scaleout-with-windows-azure-service-bus
title: 具有 Azure 服務匯流排的 SignalR 向外延展 |Microsoft Docs
author: bradygaster
description: 本主題中使用的軟體版本 Visual Studio 2013 .NET 4.5 SignalR 第2版本主題 SignalR 1.x 版的本主題的先前版本,。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: ce1305f9-30fd-49e3-bf38-d0a78dfb06c3
msc.legacyurl: /signalr/overview/performance/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: 73ed95c5027f57c7e390069dcb36b18a3714973f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579174"
---
# <a name="signalr-scaleout-with-azure-service-bus"></a><span data-ttu-id="c585a-103">使用 Azure 服務匯流排的 SignalR 向外延展</span><span class="sxs-lookup"><span data-stu-id="c585a-103">SignalR Scaleout with Azure Service Bus</span></span>

<span data-ttu-id="c585a-104">由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="c585a-104">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="c585a-105">在本教學課程中，您會將 SignalR 應用程式部署至 Windows Azure Web 角色，使用服務匯流排背板將訊息散發至每個角色實例。</span><span class="sxs-lookup"><span data-stu-id="c585a-105">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span> <span data-ttu-id="c585a-106">（您也可以[在 Azure App Service 中搭配 web apps](https://docs.microsoft.com/azure/app-service-web/)使用服務匯流排背板）。</span><span class="sxs-lookup"><span data-stu-id="c585a-106">(You can also use the Service Bus backplane with [web apps in Azure App Service](https://docs.microsoft.com/azure/app-service-web/).)</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="c585a-107">必要條件：</span><span class="sxs-lookup"><span data-stu-id="c585a-107">Prerequisites:</span></span>

- <span data-ttu-id="c585a-108">Windows Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="c585a-108">A Windows Azure account.</span></span>
- <span data-ttu-id="c585a-109">[Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="c585a-109">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="c585a-110">Visual Studio 2012 或 2013。</span><span class="sxs-lookup"><span data-stu-id="c585a-110">Visual Studio 2012 or 2013.</span></span>

<span data-ttu-id="c585a-111">服務匯流排背板也與[Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)1.1 版的服務匯流排相容。</span><span class="sxs-lookup"><span data-stu-id="c585a-111">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="c585a-112">不過，它與 Windows Server 的1.0 版服務匯流排不相容。</span><span class="sxs-lookup"><span data-stu-id="c585a-112">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="c585a-113">定價</span><span class="sxs-lookup"><span data-stu-id="c585a-113">Pricing</span></span>

<span data-ttu-id="c585a-114">服務匯流排的背板會使用主題來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="c585a-114">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="c585a-115">如需最新的定價資訊，請參閱[服務匯流排](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="c585a-115">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="c585a-116">在撰寫本文時，您可以針對小於 $1 的每月傳送1000000訊息。</span><span class="sxs-lookup"><span data-stu-id="c585a-116">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="c585a-117">背板會針對 SignalR 中樞方法的每個調用傳送服務匯流排訊息。</span><span class="sxs-lookup"><span data-stu-id="c585a-117">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="c585a-118">還有一些控制訊息可用於連接、中斷連線、加入或離開群組等等。</span><span class="sxs-lookup"><span data-stu-id="c585a-118">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="c585a-119">在大部分的應用程式中，大部分的訊息流量都會是中樞方法調用。</span><span class="sxs-lookup"><span data-stu-id="c585a-119">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="c585a-120">概觀</span><span class="sxs-lookup"><span data-stu-id="c585a-120">Overview</span></span>

<span data-ttu-id="c585a-121">在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。</span><span class="sxs-lookup"><span data-stu-id="c585a-121">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="c585a-122">使用 Windows Azure 入口網站建立新的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="c585a-122">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="c585a-123">將下列 NuGet 套件新增至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="c585a-123">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="c585a-124">SignalR</span><span class="sxs-lookup"><span data-stu-id="c585a-124">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - <span data-ttu-id="c585a-125">[SignalR. ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3)或[SignalR 的。](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span><span class="sxs-lookup"><span data-stu-id="c585a-125">[Microsoft.AspNet.SignalR.ServiceBus3](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus3) or [Microsoft.AspNet.SignalR.ServiceBus](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.ServiceBus)</span></span>
3. <span data-ttu-id="c585a-126">建立 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c585a-126">Create a SignalR application.</span></span>
4. <span data-ttu-id="c585a-127">將下列程式碼新增至 Startup.cs 以設定背板：</span><span class="sxs-lookup"><span data-stu-id="c585a-127">Add the following code to Startup.cs to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="c585a-128">這段程式碼會使用[TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx)和[MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx)的預設值來設定背板。</span><span class="sxs-lookup"><span data-stu-id="c585a-128">This code configures the backplane with the default values for [TopicCount](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.servicebusscaleoutconfiguration.topiccount(v=vs.118).aspx) and [MaxQueueLength](https://msdn.microsoft.com/library/microsoft.aspnet.signalr.messaging.scaleoutconfiguration.maxqueuelength(v=vs.118).aspx).</span></span> <span data-ttu-id="c585a-129">如需變更這些值的相關資訊，請參閱[SignalR Performance：向外延展計量](signalr-performance.md#scaleout_metrics)。</span><span class="sxs-lookup"><span data-stu-id="c585a-129">For information on changing these values, see [SignalR Performance: Scaleout Metrics](signalr-performance.md#scaleout_metrics).</span></span>

<span data-ttu-id="c585a-130">針對每個應用程式，挑選不同的 "YourAppName" 值。</span><span class="sxs-lookup"><span data-stu-id="c585a-130">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="c585a-131">請勿在多個應用程式中使用相同的值。</span><span class="sxs-lookup"><span data-stu-id="c585a-131">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="c585a-132">建立 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="c585a-132">Create the Azure Services</span></span>

<span data-ttu-id="c585a-133">如[如何建立和部署雲端服務](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)中所述，建立雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c585a-133">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="c585a-134">依照「如何：使用快速建立來建立雲端服務」一節中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="c585a-134">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="c585a-135">在本教學課程中，您不需要上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="c585a-135">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="c585a-136">建立新的服務匯流排命名空間，如[如何使用服務匯流排主題/訂用](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)帳戶中所述。</span><span class="sxs-lookup"><span data-stu-id="c585a-136">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="c585a-137">依照「建立服務命名空間」一節中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="c585a-137">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="c585a-138">請務必為雲端服務和服務匯流排命名空間選取相同的區域。</span><span class="sxs-lookup"><span data-stu-id="c585a-138">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="c585a-139">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="c585a-139">Create the Visual Studio Project</span></span>

<span data-ttu-id="c585a-140">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="c585a-140">Start Visual Studio.</span></span> <span data-ttu-id="c585a-141">從 [檔案] 功能表，按一下 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="c585a-141">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="c585a-142">在 [**新增專案**] 對話方塊中，展開 [**視覺效果C#** ]。</span><span class="sxs-lookup"><span data-stu-id="c585a-142">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="c585a-143">在 [**已安裝的範本**] 底下選取 [**雲端**]，然後選取 [ **Windows Azure 雲端服務**]。</span><span class="sxs-lookup"><span data-stu-id="c585a-143">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="c585a-144">保留預設值 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="c585a-144">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="c585a-145">將應用程式命名為 ChatService，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="c585a-145">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="c585a-146">在 [**新的 Windows Azure 雲端服務**] 對話方塊中，選取 [ASP.NET Web 角色]。</span><span class="sxs-lookup"><span data-stu-id="c585a-146">In the **New Windows Azure Cloud Service** dialog, select ASP.NET Web Role.</span></span> <span data-ttu-id="c585a-147">按一下向右箭號按鈕（ **&gt;** ），將角色新增至您的方案。</span><span class="sxs-lookup"><span data-stu-id="c585a-147">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="c585a-148">將滑鼠游標移到新的角色上方，使鉛筆圖示可見。</span><span class="sxs-lookup"><span data-stu-id="c585a-148">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="c585a-149">按一下此圖示以重新命名角色。</span><span class="sxs-lookup"><span data-stu-id="c585a-149">Click this icon to rename the role.</span></span> <span data-ttu-id="c585a-150">將角色命名為 "SignalRChat"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="c585a-150">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="c585a-151">在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [ **MVC**]，然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c585a-151">In the **New ASP.NET Project** dialog, select **MVC**, and click OK.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="c585a-152">[專案] wizard 會建立兩個專案：</span><span class="sxs-lookup"><span data-stu-id="c585a-152">The project wizard creates two projects:</span></span>

- <span data-ttu-id="c585a-153">ChatService：此專案是 Windows Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c585a-153">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="c585a-154">它會定義 Azure 角色和其他設定選項。</span><span class="sxs-lookup"><span data-stu-id="c585a-154">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="c585a-155">SignalRChat：此專案是您的 ASP.NET MVC 5 專案。</span><span class="sxs-lookup"><span data-stu-id="c585a-155">SignalRChat: This project is your ASP.NET MVC 5 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="c585a-156">建立 SignalR Chat 應用程式</span><span class="sxs-lookup"><span data-stu-id="c585a-156">Create the SignalR Chat Application</span></span>

<span data-ttu-id="c585a-157">若要建立聊天應用程式，請依照教學課程[消費者入門使用 SignalR 和 MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="c585a-157">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 5](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md).</span></span>

<span data-ttu-id="c585a-158">使用 NuGet 來安裝所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="c585a-158">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="c585a-159">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="c585a-159">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="c585a-160">在 [**套件管理員主控台**] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="c585a-160">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="c585a-161">使用 [`-ProjectName`] 選項，將套件安裝至 ASP.NET MVC 專案，而不是 Windows Azure 專案。</span><span class="sxs-lookup"><span data-stu-id="c585a-161">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="c585a-162">設定背板</span><span class="sxs-lookup"><span data-stu-id="c585a-162">Configure the Backplane</span></span>

<span data-ttu-id="c585a-163">在您應用程式的 Startup.cs 檔案中，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="c585a-163">In your application's Startup.cs file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="c585a-164">現在您需要取得服務匯流排連接字串。</span><span class="sxs-lookup"><span data-stu-id="c585a-164">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="c585a-165">在 Azure 入口網站中，選取您所建立的服務匯流排命名空間，然後按一下 存取金鑰 圖示。</span><span class="sxs-lookup"><span data-stu-id="c585a-165">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

<span data-ttu-id="c585a-166">將連接字串複製到剪貼簿，然後將它貼到*connectionString*變數中。</span><span class="sxs-lookup"><span data-stu-id="c585a-166">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="c585a-167">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="c585a-167">Deploy to Azure</span></span>

<span data-ttu-id="c585a-168">在方案總管中，展開 ChatService 專案內的 [**角色**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c585a-168">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="c585a-169">以滑鼠右鍵按一下 [SignalRChat] 角色，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="c585a-169">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="c585a-170">選取 [**設定**] 索引標籤。在 [**實例**] 下選取 [2]。</span><span class="sxs-lookup"><span data-stu-id="c585a-170">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="c585a-171">您也可以將 VM 大小設定為 **[超小型]。**</span><span class="sxs-lookup"><span data-stu-id="c585a-171">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="c585a-172">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="c585a-172">Save the changes.</span></span>

<span data-ttu-id="c585a-173">在方案總管中，以滑鼠右鍵按一下 [ChatService] 專案。</span><span class="sxs-lookup"><span data-stu-id="c585a-173">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="c585a-174">選取 [發行]。</span><span class="sxs-lookup"><span data-stu-id="c585a-174">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="c585a-175">如果這是您第一次發行至 Windows Azure，您必須下載您的認證。</span><span class="sxs-lookup"><span data-stu-id="c585a-175">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="c585a-176">在 [**發行**嚮導] 中，按一下 [登入以下載認證]。</span><span class="sxs-lookup"><span data-stu-id="c585a-176">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="c585a-177">這會提示您登入 Windows Azure 入口網站並下載發佈設定檔案。</span><span class="sxs-lookup"><span data-stu-id="c585a-177">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="c585a-178">按一下 [匯**入**]，然後選取您已下載的發佈設定檔案。</span><span class="sxs-lookup"><span data-stu-id="c585a-178">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="c585a-179">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="c585a-179">Click **Next**.</span></span> <span data-ttu-id="c585a-180">在 [**發行設定**] 對話方塊的 [**雲端服務**] 底下，選取您稍早建立的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="c585a-180">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="c585a-181">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="c585a-181">Click **Publish**.</span></span> <span data-ttu-id="c585a-182">部署應用程式並啟動 Vm 可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="c585a-182">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="c585a-183">現在當您執行聊天應用程式時，角色實例會使用服務匯流排主題，透過 Azure 服務匯流排進行通訊。</span><span class="sxs-lookup"><span data-stu-id="c585a-183">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="c585a-184">主題是允許多個訂閱者的訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="c585a-184">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="c585a-185">背板會自動建立主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="c585a-185">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="c585a-186">若要查看 [訂用帳戶] 和 [訊息] 活動，請開啟 Azure 入口網站，選取服務匯流排命名空間，然後按一下 [主題]。</span><span class="sxs-lookup"><span data-stu-id="c585a-186">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="c585a-187">這需要幾分鐘的時間，訊息活動才會顯示在儀表板中。</span><span class="sxs-lookup"><span data-stu-id="c585a-187">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image15.png)

<span data-ttu-id="c585a-188">SignalR 會管理主題的存留期。</span><span class="sxs-lookup"><span data-stu-id="c585a-188">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="c585a-189">只要您的應用程式已部署，請不要嘗試手動刪除主題或變更設定。</span><span class="sxs-lookup"><span data-stu-id="c585a-189">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>

## <a name="troubleshooting"></a><span data-ttu-id="c585a-190">疑難排解</span><span class="sxs-lookup"><span data-stu-id="c585a-190">Troubleshooting</span></span>

<span data-ttu-id="c585a-191">**InvalidOperationException 「唯一支援的 IsolationLevel 是 ' IsolationLevel。 Serializable '」。**</span><span class="sxs-lookup"><span data-stu-id="c585a-191">**System.InvalidOperationException "The only supported IsolationLevel is 'IsolationLevel.Serializable'."**</span></span>

<span data-ttu-id="c585a-192">如果作業的交易層級設定為 `Serializable`以外的某個專案，就會發生這個錯誤。</span><span class="sxs-lookup"><span data-stu-id="c585a-192">This error can occur if the transaction level for an operation is set to something other than `Serializable`.</span></span> <span data-ttu-id="c585a-193">確認沒有任何作業正在執行其他交易層級。</span><span class="sxs-lookup"><span data-stu-id="c585a-193">Verify that no operations are being performed with other transaction levels.</span></span>
