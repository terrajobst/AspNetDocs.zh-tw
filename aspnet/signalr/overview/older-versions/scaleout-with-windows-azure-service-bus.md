---
uid: signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
title: 具有 Azure 服務匯流排的 SignalR 向外延展（SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 501db899-e68c-49ff-81b2-1dc561bfe908
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-windows-azure-service-bus
msc.type: authoredcontent
ms.openlocfilehash: e64f84db00b571c01ea52f48d1ac1af46698d391
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78558412"
---
# <a name="signalr-scaleout-with-azure-service-bus-signalr-1x"></a><span data-ttu-id="d95d7-102">使用 Azure 服務匯流排的 SignalR 向外延展 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="d95d7-102">SignalR Scaleout with Azure Service Bus (SignalR 1.x)</span></span>

<span data-ttu-id="d95d7-103">由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="d95d7-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="d95d7-104">在本教學課程中，您會將 SignalR 應用程式部署至 Windows Azure Web 角色，使用服務匯流排背板將訊息散發至每個角色實例。</span><span class="sxs-lookup"><span data-stu-id="d95d7-104">In this tutorial, you will deploy a SignalR application to a Windows Azure Web Role, using the Service Bus backplane to distribute messages to each role instance.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image1.png)

<span data-ttu-id="d95d7-105">必要條件：</span><span class="sxs-lookup"><span data-stu-id="d95d7-105">Prerequisites:</span></span>

- <span data-ttu-id="d95d7-106">Windows Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="d95d7-106">A Windows Azure account.</span></span>
- <span data-ttu-id="d95d7-107">[Windows AZURE SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409)。</span><span class="sxs-lookup"><span data-stu-id="d95d7-107">The [Windows Azure SDK](https://go.microsoft.com/fwlink/?linkid=254364&amp;clcid=0x409).</span></span>
- <span data-ttu-id="d95d7-108">Visual Studio 2012。</span><span class="sxs-lookup"><span data-stu-id="d95d7-108">Visual Studio 2012.</span></span>

<span data-ttu-id="d95d7-109">服務匯流排背板也與[Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx)1.1 版的服務匯流排相容。</span><span class="sxs-lookup"><span data-stu-id="d95d7-109">The service bus backplane is also compatible with [Service Bus for Windows Server](https://msdn.microsoft.com/library/windowsazure/dn282144.aspx), version 1.1.</span></span> <span data-ttu-id="d95d7-110">不過，它與 Windows Server 的1.0 版服務匯流排不相容。</span><span class="sxs-lookup"><span data-stu-id="d95d7-110">However, it is not compatible with version 1.0 of Service Bus for Windows Server.</span></span>

## <a name="pricing"></a><span data-ttu-id="d95d7-111">定價</span><span class="sxs-lookup"><span data-stu-id="d95d7-111">Pricing</span></span>

<span data-ttu-id="d95d7-112">服務匯流排的背板會使用主題來傳送訊息。</span><span class="sxs-lookup"><span data-stu-id="d95d7-112">The Service Bus backplane uses topics to send messages.</span></span> <span data-ttu-id="d95d7-113">如需最新的定價資訊，請參閱[服務匯流排](https://azure.microsoft.com/pricing/details/service-bus/)。</span><span class="sxs-lookup"><span data-stu-id="d95d7-113">For the latest pricing information, see [Service Bus](https://azure.microsoft.com/pricing/details/service-bus/).</span></span> <span data-ttu-id="d95d7-114">在撰寫本文時，您可以針對小於 $1 的每月傳送1000000訊息。</span><span class="sxs-lookup"><span data-stu-id="d95d7-114">At the time of this writing, you can send 1,000,000 messages per month for less than $1.</span></span> <span data-ttu-id="d95d7-115">背板會針對 SignalR 中樞方法的每個調用傳送服務匯流排訊息。</span><span class="sxs-lookup"><span data-stu-id="d95d7-115">The backplane sends a service bus message for each invocation of a SignalR hub method.</span></span> <span data-ttu-id="d95d7-116">還有一些控制訊息可用於連接、中斷連線、加入或離開群組等等。</span><span class="sxs-lookup"><span data-stu-id="d95d7-116">There are also some control messages for connections, disconnections, joining or leaving groups, and so forth.</span></span> <span data-ttu-id="d95d7-117">在大部分的應用程式中，大部分的訊息流量都會是中樞方法調用。</span><span class="sxs-lookup"><span data-stu-id="d95d7-117">In most applications, the majority of the message traffic will be hub method invocations.</span></span>

## <a name="overview"></a><span data-ttu-id="d95d7-118">概觀</span><span class="sxs-lookup"><span data-stu-id="d95d7-118">Overview</span></span>

<span data-ttu-id="d95d7-119">在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。</span><span class="sxs-lookup"><span data-stu-id="d95d7-119">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="d95d7-120">使用 Windows Azure 入口網站建立新的服務匯流排命名空間。</span><span class="sxs-lookup"><span data-stu-id="d95d7-120">Use the Windows Azure portal to create a new Service Bus namespace.</span></span>
2. <span data-ttu-id="d95d7-121">將下列 NuGet 套件新增至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="d95d7-121">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="d95d7-122">SignalR</span><span class="sxs-lookup"><span data-stu-id="d95d7-122">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="d95d7-123">SignalR。</span><span class="sxs-lookup"><span data-stu-id="d95d7-123">Microsoft.AspNet.SignalR.ServiceBus</span></span>](http://www.nuget.org/packages/SignalR.WindowsAzureServiceBus)
3. <span data-ttu-id="d95d7-124">建立 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d95d7-124">Create a SignalR application.</span></span>
4. <span data-ttu-id="d95d7-125">將下列程式碼新增至 global.asax 以設定背板：</span><span class="sxs-lookup"><span data-stu-id="d95d7-125">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample1.cs)]

<span data-ttu-id="d95d7-126">針對每個應用程式，挑選不同的 "YourAppName" 值。</span><span class="sxs-lookup"><span data-stu-id="d95d7-126">For each application, pick a different value for "YourAppName".</span></span> <span data-ttu-id="d95d7-127">請勿在多個應用程式中使用相同的值。</span><span class="sxs-lookup"><span data-stu-id="d95d7-127">Do not use the same value across multiple applications.</span></span>

## <a name="create-the-azure-services"></a><span data-ttu-id="d95d7-128">建立 Azure 服務</span><span class="sxs-lookup"><span data-stu-id="d95d7-128">Create the Azure Services</span></span>

<span data-ttu-id="d95d7-129">如[如何建立和部署雲端服務](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy)中所述，建立雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d95d7-129">Create a Cloud Service, as described in [How to Create and Deploy a Cloud Service](https://docs.microsoft.com/azure/cloud-services/cloud-services-how-to-create-deploy).</span></span> <span data-ttu-id="d95d7-130">依照「如何：使用快速建立來建立雲端服務」一節中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="d95d7-130">Follow the steps in the section "How to: Create a cloud service using Quick Create".</span></span> <span data-ttu-id="d95d7-131">在本教學課程中，您不需要上傳憑證。</span><span class="sxs-lookup"><span data-stu-id="d95d7-131">For this tutorial, you do not need to upload a certificate.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image2.png)

<span data-ttu-id="d95d7-132">建立新的服務匯流排命名空間，如[如何使用服務匯流排主題/訂用](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions)帳戶中所述。</span><span class="sxs-lookup"><span data-stu-id="d95d7-132">Create a new Service Bus namespace, as described in [How to Use Service Bus Topics/Subscriptions](https://docs.microsoft.com/azure/service-bus-messaging/service-bus-dotnet-how-to-use-topics-subscriptions).</span></span> <span data-ttu-id="d95d7-133">依照「建立服務命名空間」一節中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="d95d7-133">Follow the steps in the section "Create a Service Namespace".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="d95d7-134">請務必為雲端服務和服務匯流排命名空間選取相同的區域。</span><span class="sxs-lookup"><span data-stu-id="d95d7-134">Make sure to select the same region for the cloud service and the Service Bus namespace.</span></span>

## <a name="create-the-visual-studio-project"></a><span data-ttu-id="d95d7-135">建立 Visual Studio 專案</span><span class="sxs-lookup"><span data-stu-id="d95d7-135">Create the Visual Studio Project</span></span>

<span data-ttu-id="d95d7-136">啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="d95d7-136">Start Visual Studio.</span></span> <span data-ttu-id="d95d7-137">從 [檔案] 功能表，按一下 [新增專案]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-137">From the **File** menu, click **New Project**.</span></span>

<span data-ttu-id="d95d7-138">在 [**新增專案**] 對話方塊中，展開 [**視覺效果C#** ]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-138">In the **New Project** dialog box, expand **Visual C#**.</span></span> <span data-ttu-id="d95d7-139">在 [**已安裝的範本**] 底下選取 [**雲端**]，然後選取 [ **Windows Azure 雲端服務**]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-139">Under **Installed Templates**, select **Cloud** and then select **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="d95d7-140">保留預設值 .NET Framework 4.5。</span><span class="sxs-lookup"><span data-stu-id="d95d7-140">Keep the default .NET Framework 4.5.</span></span> <span data-ttu-id="d95d7-141">將應用程式命名為 ChatService，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="d95d7-141">Name the application ChatService and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image4.png)

<span data-ttu-id="d95d7-142">在 [**新的 Windows Azure 雲端服務**] 對話方塊中，選取 [ASP.NET MVC 4 Web 角色]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-142">In the **New Windows Azure Cloud Service** dialog, select ASP.NET MVC 4 Web Role.</span></span> <span data-ttu-id="d95d7-143">按一下向右箭號按鈕（ **&gt;** ），將角色新增至您的方案。</span><span class="sxs-lookup"><span data-stu-id="d95d7-143">Click the right-arrow button (**&gt;**) to add the role to your solution.</span></span>

<span data-ttu-id="d95d7-144">將滑鼠游標移到新的角色上方，使鉛筆圖示可見。</span><span class="sxs-lookup"><span data-stu-id="d95d7-144">Hover the mouse over the new role, so the pencil icon visible.</span></span> <span data-ttu-id="d95d7-145">按一下此圖示以重新命名角色。</span><span class="sxs-lookup"><span data-stu-id="d95d7-145">Click this icon to rename the role.</span></span> <span data-ttu-id="d95d7-146">將角色命名為 "SignalRChat"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="d95d7-146">Name the role "SignalRChat" and click **OK**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image5.png)

<span data-ttu-id="d95d7-147">在 [**新增 ASP.NET MVC 4 專案**] 中，選取 [**網際網路應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-147">In the **New ASP.NET MVC 4 Project** wizard, select **Internet Application**.</span></span> <span data-ttu-id="d95d7-148">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-148">Click **OK**.</span></span> <span data-ttu-id="d95d7-149">[專案] wizard 會建立兩個專案：</span><span class="sxs-lookup"><span data-stu-id="d95d7-149">The project wizard creates two projects:</span></span>

- <span data-ttu-id="d95d7-150">ChatService：此專案是 Windows Azure 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d95d7-150">ChatService: This project is the Windows Azure application.</span></span> <span data-ttu-id="d95d7-151">它會定義 Azure 角色和其他設定選項。</span><span class="sxs-lookup"><span data-stu-id="d95d7-151">It defines the Azure roles and other configuration options.</span></span>
- <span data-ttu-id="d95d7-152">SignalRChat：此專案是您的 ASP.NET MVC 4 專案。</span><span class="sxs-lookup"><span data-stu-id="d95d7-152">SignalRChat: This project is your ASP.NET MVC 4 project.</span></span>

## <a name="create-the-signalr-chat-application"></a><span data-ttu-id="d95d7-153">建立 SignalR Chat 應用程式</span><span class="sxs-lookup"><span data-stu-id="d95d7-153">Create the SignalR Chat Application</span></span>

<span data-ttu-id="d95d7-154">若要建立聊天應用程式，請依照教學課程[消費者入門使用 SignalR 和 MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md)中的步驟進行。</span><span class="sxs-lookup"><span data-stu-id="d95d7-154">To create the chat application, follow the steps in the tutorial [Getting Started with SignalR and MVC 4](tutorial-getting-started-with-signalr-and-mvc-4.md).</span></span>

<span data-ttu-id="d95d7-155">使用 NuGet 來安裝所需的程式庫。</span><span class="sxs-lookup"><span data-stu-id="d95d7-155">Use NuGet to install the required libraries.</span></span> <span data-ttu-id="d95d7-156">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-156">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="d95d7-157">在 [**套件管理員主控台**] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="d95d7-157">In the **Package Manager Console** window, enter the following commands:</span></span>

[!code-powershell[Main](scaleout-with-windows-azure-service-bus/samples/sample2.ps1)]

<span data-ttu-id="d95d7-158">使用 [`-ProjectName`] 選項，將套件安裝至 ASP.NET MVC 專案，而不是 Windows Azure 專案。</span><span class="sxs-lookup"><span data-stu-id="d95d7-158">Use the `-ProjectName` option to install the packages to the ASP.NET MVC project, rather than the Windows Azure project.</span></span>

## <a name="configure-the-backplane"></a><span data-ttu-id="d95d7-159">設定背板</span><span class="sxs-lookup"><span data-stu-id="d95d7-159">Configure the Backplane</span></span>

<span data-ttu-id="d95d7-160">在您應用程式的 global.asax 檔案中，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="d95d7-160">In your application's Global.asax file, add the following code:</span></span>

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample3.cs)]

<span data-ttu-id="d95d7-161">現在您需要取得服務匯流排連接字串。</span><span class="sxs-lookup"><span data-stu-id="d95d7-161">Now you need to get your service bus connection string.</span></span> <span data-ttu-id="d95d7-162">在 Azure 入口網站中，選取您所建立的服務匯流排命名空間，然後按一下 存取金鑰 圖示。</span><span class="sxs-lookup"><span data-stu-id="d95d7-162">In the Azure portal, select the service bus namespace that you created and click the Access Key icon.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image6.png)

<span data-ttu-id="d95d7-163">將連接字串複製到剪貼簿，然後將它貼到*connectionString*變數中。</span><span class="sxs-lookup"><span data-stu-id="d95d7-163">Copy the connection string to the clipboard, then paste it into the *connectionString* variable.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image7.png)

[!code-csharp[Main](scaleout-with-windows-azure-service-bus/samples/sample4.cs)]

## <a name="deploy-to-azure"></a><span data-ttu-id="d95d7-164">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="d95d7-164">Deploy to Azure</span></span>

<span data-ttu-id="d95d7-165">在方案總管中，展開 ChatService 專案內的 [**角色**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="d95d7-165">In Solution Explorer, expand the **Roles** folder inside the ChatService project.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image8.png)

<span data-ttu-id="d95d7-166">以滑鼠右鍵按一下 [SignalRChat] 角色，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-166">Right-click the SignalRChat role and select **Properties**.</span></span> <span data-ttu-id="d95d7-167">選取 [**設定**] 索引標籤。在 [**實例**] 下選取 [2]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-167">Select the **Configuration** tab. Under **Instances** select 2.</span></span> <span data-ttu-id="d95d7-168">您也可以將 VM 大小設定為 **[超小型]。**</span><span class="sxs-lookup"><span data-stu-id="d95d7-168">You can also set the VM size to **Extra Small**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image9.png)

<span data-ttu-id="d95d7-169">儲存變更。</span><span class="sxs-lookup"><span data-stu-id="d95d7-169">Save the changes.</span></span>

<span data-ttu-id="d95d7-170">在方案總管中，以滑鼠右鍵按一下 [ChatService] 專案。</span><span class="sxs-lookup"><span data-stu-id="d95d7-170">In Solution Explorer, right-click the ChatService project.</span></span> <span data-ttu-id="d95d7-171">選取 [發行]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-171">Select **Publish**.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image10.png)

<span data-ttu-id="d95d7-172">如果這是您第一次發行至 Windows Azure，您必須下載您的認證。</span><span class="sxs-lookup"><span data-stu-id="d95d7-172">If this is your first time publishing to Windows Azure, you must download your credentials.</span></span> <span data-ttu-id="d95d7-173">在 [**發行**嚮導] 中，按一下 [登入以下載認證]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-173">In the **Publish** wizard, click "Sign in to download credentials".</span></span> <span data-ttu-id="d95d7-174">這會提示您登入 Windows Azure 入口網站並下載發佈設定檔案。</span><span class="sxs-lookup"><span data-stu-id="d95d7-174">This will prompt you to sign into the Windows Azure portal and download a publish settings file.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image11.png)

<span data-ttu-id="d95d7-175">按一下 [匯**入**]，然後選取您已下載的發佈設定檔案。</span><span class="sxs-lookup"><span data-stu-id="d95d7-175">Click **Import** and select the publish settings file that you downloaded.</span></span>

<span data-ttu-id="d95d7-176">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-176">Click **Next**.</span></span> <span data-ttu-id="d95d7-177">在 [**發行設定**] 對話方塊的 [**雲端服務**] 底下，選取您稍早建立的雲端服務。</span><span class="sxs-lookup"><span data-stu-id="d95d7-177">In the **Publish Settings** dialog, under **Cloud Service**, select the cloud service that you created earlier.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image12.png)

<span data-ttu-id="d95d7-178">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-178">Click **Publish**.</span></span> <span data-ttu-id="d95d7-179">部署應用程式並啟動 Vm 可能需要幾分鐘的時間。</span><span class="sxs-lookup"><span data-stu-id="d95d7-179">It can take a few minutes to deploy the application and start the VMs.</span></span>

<span data-ttu-id="d95d7-180">現在當您執行聊天應用程式時，角色實例會使用服務匯流排主題，透過 Azure 服務匯流排進行通訊。</span><span class="sxs-lookup"><span data-stu-id="d95d7-180">Now when you run the chat application, the role instances communicate through Azure Service Bus, using a Service Bus topic.</span></span> <span data-ttu-id="d95d7-181">主題是允許多個訂閱者的訊息佇列。</span><span class="sxs-lookup"><span data-stu-id="d95d7-181">A topic is a message queue that allows multiple subscribers.</span></span>

<span data-ttu-id="d95d7-182">背板會自動建立主題和訂用帳戶。</span><span class="sxs-lookup"><span data-stu-id="d95d7-182">The backplane automatically creates the topic and the subscriptions.</span></span> <span data-ttu-id="d95d7-183">若要查看 [訂用帳戶] 和 [訊息] 活動，請開啟 Azure 入口網站，選取服務匯流排命名空間，然後按一下 [主題]。</span><span class="sxs-lookup"><span data-stu-id="d95d7-183">To see the subscriptions and message activity, open the Azure portal, select the Service Bus namespace, and click on "Topics".</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image13.png)

<span data-ttu-id="d95d7-184">這需要幾分鐘的時間，訊息活動才會顯示在儀表板中。</span><span class="sxs-lookup"><span data-stu-id="d95d7-184">It make take a few minutes for the message activity to show up in the dashboard.</span></span>

![](scaleout-with-windows-azure-service-bus/_static/image14.png)

<span data-ttu-id="d95d7-185">SignalR 會管理主題的存留期。</span><span class="sxs-lookup"><span data-stu-id="d95d7-185">SignalR manages the topic lifetime.</span></span> <span data-ttu-id="d95d7-186">只要您的應用程式已部署，請不要嘗試手動刪除主題或變更設定。</span><span class="sxs-lookup"><span data-stu-id="d95d7-186">As long as your application is deployed, don't try to manually delete topics or change settings on the topic.</span></span>
