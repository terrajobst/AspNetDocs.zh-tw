---
uid: signalr/overview/older-versions/scaleout-with-redis
title: SignalR 向外延展 with Redis （SignalR 1.x） |Microsoft Docs
author: bradygaster
description: ''
ms.author: bradyg
ms.date: 05/01/2013
ms.assetid: 6abecf80-8ffa-41ba-b0d9-1d9edbe7687b
msc.legacyurl: /signalr/overview/older-versions/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 5079cf3fa773faeac911eddc75dc66e94ad98bb0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78536558"
---
# <a name="signalr-scaleout-with-redis-signalr-1x"></a><span data-ttu-id="347c5-102">使用 Redis 的 SignalR 向外延展 (SignalR 1.x)</span><span class="sxs-lookup"><span data-stu-id="347c5-102">SignalR Scaleout with Redis (SignalR 1.x)</span></span>

<span data-ttu-id="347c5-103">由[Mike Wasson](https://github.com/MikeWasson)， [Fletcher](https://github.com/pfletcher)</span><span class="sxs-lookup"><span data-stu-id="347c5-103">by [Mike Wasson](https://github.com/MikeWasson), [Patrick Fletcher](https://github.com/pfletcher)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

<span data-ttu-id="347c5-104">在本教學課程中，您將使用[Redis](http://redis.io/) ，將訊息散發至部署在兩個不同 IIS 實例上的 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="347c5-104">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="347c5-105">Redis 是記憶體中的索引鍵/值存放區。</span><span class="sxs-lookup"><span data-stu-id="347c5-105">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="347c5-106">它也支援具有發行/訂閱模型的訊息系統。</span><span class="sxs-lookup"><span data-stu-id="347c5-106">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="347c5-107">SignalR Redis 背板會使用 pub/sub 功能將訊息轉送至其他伺服器。</span><span class="sxs-lookup"><span data-stu-id="347c5-107">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="347c5-108">在本教學課程中，您將使用三部伺服器：</span><span class="sxs-lookup"><span data-stu-id="347c5-108">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="347c5-109">兩部執行 Windows 的伺服器，您將用它來部署 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="347c5-109">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="347c5-110">一部執行 Linux 的伺服器，您將使用它來執行 Redis。</span><span class="sxs-lookup"><span data-stu-id="347c5-110">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="347c5-111">在本教學課程的螢幕擷取畫面中，我使用了 Ubuntu 12.04 TLS。</span><span class="sxs-lookup"><span data-stu-id="347c5-111">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="347c5-112">如果您沒有三個要使用的實體伺服器，您可以在 Hyper-v 上建立 Vm。</span><span class="sxs-lookup"><span data-stu-id="347c5-112">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="347c5-113">另一個選項是在 Azure 上建立 Vm。</span><span class="sxs-lookup"><span data-stu-id="347c5-113">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="347c5-114">雖然本教學課程使用官方 Redis 實，但也有 MSOpenTech 的[Windows 埠 Redis](https://github.com/MSOpenTech/redis) 。</span><span class="sxs-lookup"><span data-stu-id="347c5-114">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="347c5-115">安裝程式和設定不同，但步驟相同。</span><span class="sxs-lookup"><span data-stu-id="347c5-115">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="347c5-116">具有 Redis 的 SignalR 向外延展不支援 Redis 叢集。</span><span class="sxs-lookup"><span data-stu-id="347c5-116">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="347c5-117">概觀</span><span class="sxs-lookup"><span data-stu-id="347c5-117">Overview</span></span>

<span data-ttu-id="347c5-118">在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。</span><span class="sxs-lookup"><span data-stu-id="347c5-118">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="347c5-119">安裝 Redis 並啟動 Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="347c5-119">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="347c5-120">將下列 NuGet 套件新增至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="347c5-120">Add these NuGet packages to your application:</span></span> 

    - [<span data-ttu-id="347c5-121">SignalR</span><span class="sxs-lookup"><span data-stu-id="347c5-121">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="347c5-122">SignalR. Redis</span><span class="sxs-lookup"><span data-stu-id="347c5-122">Microsoft.AspNet.SignalR.Redis</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR.Redis)
3. <span data-ttu-id="347c5-123">建立 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="347c5-123">Create a SignalR application.</span></span>
4. <span data-ttu-id="347c5-124">將下列程式碼新增至 global.asax 以設定背板：</span><span class="sxs-lookup"><span data-stu-id="347c5-124">Add the following code to Global.asax to configure the backplane:</span></span> 

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="347c5-125">Hyper-v 上的 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="347c5-125">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="347c5-126">您可以使用 Windows Hyper-v，輕鬆地在 Windows Server 上建立 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="347c5-126">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="347c5-127">從[http://www.ubuntu.com](http://www.ubuntu.com/)下載 Ubuntu ISO。</span><span class="sxs-lookup"><span data-stu-id="347c5-127">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="347c5-128">在 Hyper-v 中，新增 VM。</span><span class="sxs-lookup"><span data-stu-id="347c5-128">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="347c5-129">在 [**連接虛擬硬碟]** 步驟中，選取 [**建立虛擬硬碟**]。</span><span class="sxs-lookup"><span data-stu-id="347c5-129">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="347c5-130">在 [**安裝選項**] 步驟中，選取 [**影像檔案（.iso）** ]，按一下 **[流覽]** ，然後流覽至 Ubuntu 安裝 iso。</span><span class="sxs-lookup"><span data-stu-id="347c5-130">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="347c5-131">安裝 Redis</span><span class="sxs-lookup"><span data-stu-id="347c5-131">Install Redis</span></span>

<span data-ttu-id="347c5-132">遵循[http://redis.io/download](http://redis.io/download)的步驟，下載並建立 Redis。</span><span class="sxs-lookup"><span data-stu-id="347c5-132">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="347c5-133">這會在 `src` 目錄中建立 Redis 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="347c5-133">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="347c5-134">根據預設，Redis 不需要密碼。</span><span class="sxs-lookup"><span data-stu-id="347c5-134">By default, Redis does not require a password.</span></span> <span data-ttu-id="347c5-135">若要設定密碼，請編輯位於原始程式碼根目錄中的 `redis.conf` 檔案。</span><span class="sxs-lookup"><span data-stu-id="347c5-135">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="347c5-136">（您必須先製作檔案的備份副本，然後再進行編輯！）將下列指示詞新增至 `redis.conf`：</span><span class="sxs-lookup"><span data-stu-id="347c5-136">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="347c5-137">現在啟動 Redis 伺服器：</span><span class="sxs-lookup"><span data-stu-id="347c5-137">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="347c5-138">開啟埠6379，這是 Redis 接聽的預設埠。</span><span class="sxs-lookup"><span data-stu-id="347c5-138">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="347c5-139">（您可以變更設定檔案中的埠號碼）。</span><span class="sxs-lookup"><span data-stu-id="347c5-139">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="347c5-140">建立 SignalR 應用程式</span><span class="sxs-lookup"><span data-stu-id="347c5-140">Create the SignalR Application</span></span>

<span data-ttu-id="347c5-141">遵循下列其中一個教學課程來建立 SignalR 應用程式：</span><span class="sxs-lookup"><span data-stu-id="347c5-141">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="347c5-142">使用 SignalR 消費者入門</span><span class="sxs-lookup"><span data-stu-id="347c5-142">Getting Started with SignalR</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="347c5-143">使用 SignalR 和 MVC 4 的消費者入門</span><span class="sxs-lookup"><span data-stu-id="347c5-143">Getting Started with SignalR and MVC 4</span></span>](tutorial-getting-started-with-signalr-and-mvc-4.md)

<span data-ttu-id="347c5-144">接下來，我們將修改聊天應用程式，以支援使用 Redis 的向外延展。</span><span class="sxs-lookup"><span data-stu-id="347c5-144">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="347c5-145">首先，將 SignalR Redis NuGet 封裝新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="347c5-145">First, add the SignalR.Redis NuGet package to your project.</span></span> <span data-ttu-id="347c5-146">在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="347c5-146">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="347c5-147">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="347c5-147">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="347c5-148">接下來，開啟 global.asax 檔案。</span><span class="sxs-lookup"><span data-stu-id="347c5-148">Next, open the Global.asax file.</span></span> <span data-ttu-id="347c5-149">將下列程式碼新增至**應用程式\_Start**方法：</span><span class="sxs-lookup"><span data-stu-id="347c5-149">Add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="347c5-150">「伺服器」是正在執行 Redis 的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="347c5-150">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="347c5-151">*port*是埠號碼</span><span class="sxs-lookup"><span data-stu-id="347c5-151">*port* is the port number</span></span>
- <span data-ttu-id="347c5-152">「密碼」是您在 redis 檔案中定義的密碼。</span><span class="sxs-lookup"><span data-stu-id="347c5-152">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="347c5-153">"AppName" 為任何字串。</span><span class="sxs-lookup"><span data-stu-id="347c5-153">"AppName" is any string.</span></span> <span data-ttu-id="347c5-154">SignalR 會使用此名稱建立 Redis pub/sub 通道。</span><span class="sxs-lookup"><span data-stu-id="347c5-154">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="347c5-155">例如:</span><span class="sxs-lookup"><span data-stu-id="347c5-155">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="347c5-156">部署和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="347c5-156">Deploy and Run the Application</span></span>

<span data-ttu-id="347c5-157">準備您的 Windows Server 實例以部署 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="347c5-157">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="347c5-158">新增 IIS 角色。</span><span class="sxs-lookup"><span data-stu-id="347c5-158">Add the IIS role.</span></span> <span data-ttu-id="347c5-159">包含「應用程式開發」功能，包括 WebSocket 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="347c5-159">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="347c5-160">也請包含管理服務（列在 [管理工具] 底下）。</span><span class="sxs-lookup"><span data-stu-id="347c5-160">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="347c5-161">**安裝 Web Deploy 3.0。**</span><span class="sxs-lookup"><span data-stu-id="347c5-161">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="347c5-162">當您執行 IIS 管理員時，它會提示您安裝 Microsoft Web Platform，或者您可以[下載安裝程式](https://go.microsoft.com/fwlink/?LinkId=255386)。</span><span class="sxs-lookup"><span data-stu-id="347c5-162">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="347c5-163">在平臺安裝程式中，搜尋 Web Deploy 並安裝 Web Deploy 3。0</span><span class="sxs-lookup"><span data-stu-id="347c5-163">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="347c5-164">檢查 Web 管理服務是否正在執行。</span><span class="sxs-lookup"><span data-stu-id="347c5-164">Check that the Web Management Service is running.</span></span> <span data-ttu-id="347c5-165">如果沒有，請啟動服務。</span><span class="sxs-lookup"><span data-stu-id="347c5-165">If not, start the service.</span></span> <span data-ttu-id="347c5-166">（如果您在 Windows 服務清單中看不到 [Web 管理服務]，請確定您已在新增 IIS 角色時安裝管理服務）。</span><span class="sxs-lookup"><span data-stu-id="347c5-166">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="347c5-167">根據預設，Web 管理服務會接聽 TCP 通訊埠8172。</span><span class="sxs-lookup"><span data-stu-id="347c5-167">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="347c5-168">在 Windows 防火牆中，建立新的輸入規則，以允許埠8172上的 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="347c5-168">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="347c5-169">如需詳細資訊，請參閱設定[防火牆規則](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="347c5-169">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="347c5-170">（如果您要在 Azure 上裝載 Vm，您可以直接在 Azure 入口網站中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="347c5-170">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="347c5-171">請參閱[如何設定虛擬機器的端點](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)。）</span><span class="sxs-lookup"><span data-stu-id="347c5-171">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="347c5-172">現在您已準備好從開發電腦將 Visual Studio 專案部署到伺服器。</span><span class="sxs-lookup"><span data-stu-id="347c5-172">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="347c5-173">在方案總管中，以滑鼠右鍵按一下方案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="347c5-173">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="347c5-174">如需 web 部署的詳細檔，請參閱[Visual Studio 和 ASP.NET 的 Web 部署內容對應](../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="347c5-174">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="347c5-175">如果您將應用程式部署至兩部伺服器，您可以在另一個瀏覽器視窗中開啟每個實例，並查看每個實例都會收到來自另一個的 SignalR 訊息。</span><span class="sxs-lookup"><span data-stu-id="347c5-175">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="347c5-176">（當然，在生產環境中，這兩部伺服器會位於負載平衡器後方）。</span><span class="sxs-lookup"><span data-stu-id="347c5-176">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="347c5-177">如果您想要查看傳送至 Redis 的訊息，可以使用**Redis cli**用戶端，它會與 Redis 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="347c5-177">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
