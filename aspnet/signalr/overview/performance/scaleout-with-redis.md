---
uid: signalr/overview/performance/scaleout-with-redis
title: 具有 Redis 的 SignalR 向外延展 |Microsoft Docs
author: bradygaster
description: 本主題中使用的軟體版本 Visual Studio 2013 .NET 4.5 SignalR 第2版本主題的先前版本，以取得舊版的相關資訊 。
ms.author: bradyg
ms.date: 06/10/2014
ms.assetid: 6ecd08c1-e364-4cd7-ad4c-806521911585
msc.legacyurl: /signalr/overview/performance/scaleout-with-redis
msc.type: authoredcontent
ms.openlocfilehash: 58a7affa1769523955adc76455a1c33be6f49751
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78579223"
---
# <a name="signalr-scaleout-with-redis"></a><span data-ttu-id="2c0a8-103">使用 Redis 的 SignalR 向外延展</span><span class="sxs-lookup"><span data-stu-id="2c0a8-103">SignalR Scaleout with Redis</span></span>

<span data-ttu-id="2c0a8-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="2c0a8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE [Consider ASP.NET Core SignalR](~/includes/signalr/signalr-version-disambiguation.md)]

> ## <a name="software-versions-used-in-this-topic"></a><span data-ttu-id="2c0a8-105">本主題中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="2c0a8-105">Software versions used in this topic</span></span>
>
>
> - [<span data-ttu-id="2c0a8-106">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="2c0a8-106">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="2c0a8-107">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="2c0a8-107">.NET 4.5</span></span>
> - <span data-ttu-id="2c0a8-108">SignalR 版本2。4</span><span class="sxs-lookup"><span data-stu-id="2c0a8-108">SignalR version 2.4</span></span>
>
>
>
> ## <a name="previous-versions-of-this-topic"></a><span data-ttu-id="2c0a8-109">本主題的先前版本</span><span class="sxs-lookup"><span data-stu-id="2c0a8-109">Previous versions of this topic</span></span>
>
> <span data-ttu-id="2c0a8-110">如需舊版 SignalR 的詳細資訊，請參閱[SignalR 較舊的版本](../older-versions/index.md)。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-110">For information about earlier versions of SignalR, see [SignalR Older Versions](../older-versions/index.md).</span></span>
>
> ## <a name="questions-and-comments"></a><span data-ttu-id="2c0a8-111">問題與意見</span><span class="sxs-lookup"><span data-stu-id="2c0a8-111">Questions and comments</span></span>
>
> <span data-ttu-id="2c0a8-112">請留下有關您喜歡本教學課程的意見反應，以及我們可以在頁面底部的批註中改進的內容。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-112">Please leave feedback on how you liked this tutorial and what we could improve in the comments at the bottom of the page.</span></span> <span data-ttu-id="2c0a8-113">如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET SignalR 論壇](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR)或[StackOverflow.com](http://stackoverflow.com/)。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-113">If you have questions that are not directly related to the tutorial, you can post them to the [ASP.NET SignalR forum](https://forums.asp.net/1254.aspx/1?ASP+NET+SignalR) or [StackOverflow.com](http://stackoverflow.com/).</span></span>

<span data-ttu-id="2c0a8-114">在本教學課程中，您將使用[Redis](http://redis.io/) ，將訊息散發至部署在兩個不同 IIS 實例上的 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-114">In this tutorial, you will use [Redis](http://redis.io/) to distribute messages across a SignalR application that is deployed on two separate IIS instances.</span></span>

<span data-ttu-id="2c0a8-115">Redis 是記憶體中的索引鍵/值存放區。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-115">Redis is an in-memory key-value store.</span></span> <span data-ttu-id="2c0a8-116">它也支援具有發行/訂閱模型的訊息系統。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-116">It also supports a messaging system with a publish/subscribe model.</span></span> <span data-ttu-id="2c0a8-117">SignalR Redis 背板會使用 pub/sub 功能將訊息轉送至其他伺服器。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-117">The SignalR Redis backplane uses the pub/sub feature to forward messages to other servers.</span></span>

![](scaleout-with-redis/_static/image1.png)

<span data-ttu-id="2c0a8-118">在本教學課程中，您將使用三部伺服器：</span><span class="sxs-lookup"><span data-stu-id="2c0a8-118">For this tutorial, you will use three servers:</span></span>

- <span data-ttu-id="2c0a8-119">兩部執行 Windows 的伺服器，您將用它來部署 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-119">Two servers running Windows, which you will use to deploy a SignalR application.</span></span>
- <span data-ttu-id="2c0a8-120">一部執行 Linux 的伺服器，您將使用它來執行 Redis。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-120">One server running Linux, which you will use to run Redis.</span></span> <span data-ttu-id="2c0a8-121">在本教學課程的螢幕擷取畫面中，我使用了 Ubuntu 12.04 TLS。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-121">For the screenshots in this tutorial, I used Ubuntu 12.04 TLS.</span></span>

<span data-ttu-id="2c0a8-122">如果您沒有三個要使用的實體伺服器，您可以在 Hyper-v 上建立 Vm。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-122">If you don't have three physical servers to use, you can create VMs on Hyper-V.</span></span> <span data-ttu-id="2c0a8-123">另一個選項是在 Azure 上建立 Vm。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-123">Another option is to create VMs on Azure.</span></span>

<span data-ttu-id="2c0a8-124">雖然本教學課程使用官方 Redis 實，但也有 MSOpenTech 的[Windows 埠 Redis](https://github.com/MSOpenTech/redis) 。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-124">Although this tutorial uses the official Redis implementation, there is also a [Windows port of Redis](https://github.com/MSOpenTech/redis) from MSOpenTech.</span></span> <span data-ttu-id="2c0a8-125">安裝程式和設定不同，但步驟相同。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-125">Setup and configuration are different, but otherwise the steps are the same.</span></span>

> [!NOTE]
>
> <span data-ttu-id="2c0a8-126">具有 Redis 的 SignalR 向外延展不支援 Redis 叢集。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-126">SignalR scaleout with Redis does not support Redis clusters.</span></span>

## <a name="overview"></a><span data-ttu-id="2c0a8-127">概觀</span><span class="sxs-lookup"><span data-stu-id="2c0a8-127">Overview</span></span>

<span data-ttu-id="2c0a8-128">在我們開始進行詳細的教學課程之前，請先快速瞭解您將執行的動作。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-128">Before we get to the detailed tutorial, here is a quick overview of what you will do.</span></span>

1. <span data-ttu-id="2c0a8-129">安裝 Redis 並啟動 Redis 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-129">Install Redis and start the Redis server.</span></span>
2. <span data-ttu-id="2c0a8-130">將下列 NuGet 套件新增至您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="2c0a8-130">Add these NuGet packages to your application:</span></span>

    - [<span data-ttu-id="2c0a8-131">SignalR</span><span class="sxs-lookup"><span data-stu-id="2c0a8-131">Microsoft.AspNet.SignalR</span></span>](http://nuget.org/packages/Microsoft.AspNet.SignalR)
    - [<span data-ttu-id="2c0a8-132">SignalR. StackExchangeRedis</span><span class="sxs-lookup"><span data-stu-id="2c0a8-132">Microsoft.AspNet.SignalR.StackExchangeRedis</span></span>](https://www.nuget.org/packages/Microsoft.AspNet.SignalR.StackExchangeRedis)
    
3. <span data-ttu-id="2c0a8-133">建立 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-133">Create a SignalR application.</span></span>
4. <span data-ttu-id="2c0a8-134">將下列程式碼新增至 Startup.cs 以設定背板：</span><span class="sxs-lookup"><span data-stu-id="2c0a8-134">Add the following code to Startup.cs to configure the backplane:</span></span>

    [!code-csharp[Main](scaleout-with-redis/samples/sample1.cs)]

## <a name="ubuntu-on-hyper-v"></a><span data-ttu-id="2c0a8-135">Hyper-v 上的 Ubuntu</span><span class="sxs-lookup"><span data-stu-id="2c0a8-135">Ubuntu on Hyper-V</span></span>

<span data-ttu-id="2c0a8-136">您可以使用 Windows Hyper-v，輕鬆地在 Windows Server 上建立 Ubuntu VM。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-136">Using Windows Hyper-V, you can easily create an Ubuntu VM on Windows Server.</span></span>

<span data-ttu-id="2c0a8-137">從[http://www.ubuntu.com](http://www.ubuntu.com/)下載 Ubuntu ISO。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-137">Download the Ubuntu ISO from [http://www.ubuntu.com](http://www.ubuntu.com/).</span></span>

<span data-ttu-id="2c0a8-138">在 Hyper-v 中，新增 VM。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-138">In Hyper-V, add a new VM.</span></span> <span data-ttu-id="2c0a8-139">在 [**連接虛擬硬碟]** 步驟中，選取 [**建立虛擬硬碟**]。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-139">In the **Connect Virtual Hard Disk** step, select **Create a virtual hard disk**.</span></span>

![](scaleout-with-redis/_static/image2.png)

<span data-ttu-id="2c0a8-140">在 [**安裝選項**] 步驟中，選取 [**影像檔案（.iso）** ]，按一下 **[流覽]** ，然後流覽至 Ubuntu 安裝 iso。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-140">In the **Installation Options** step, select **Image file (.iso)**, click **Browse**, and browse to the Ubuntu installation ISO.</span></span>

![](scaleout-with-redis/_static/image3.png)

## <a name="install-redis"></a><span data-ttu-id="2c0a8-141">安裝 Redis</span><span class="sxs-lookup"><span data-stu-id="2c0a8-141">Install Redis</span></span>

<span data-ttu-id="2c0a8-142">遵循[http://redis.io/download](http://redis.io/download)的步驟，下載並建立 Redis。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-142">Follow the steps at [http://redis.io/download](http://redis.io/download) to download and build Redis.</span></span>

[!code-console[Main](scaleout-with-redis/samples/sample2.cmd)]

<span data-ttu-id="2c0a8-143">這會在 `src` 目錄中建立 Redis 二進位檔。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-143">This builds the Redis binaries in the `src` directory.</span></span>

<span data-ttu-id="2c0a8-144">根據預設，Redis 不需要密碼。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-144">By default, Redis does not require a password.</span></span> <span data-ttu-id="2c0a8-145">若要設定密碼，請編輯位於原始程式碼根目錄中的 `redis.conf` 檔案。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-145">To set a password, edit the `redis.conf` file, which is located in the root directory of the source code.</span></span> <span data-ttu-id="2c0a8-146">（您必須先製作檔案的備份副本，然後再進行編輯！）將下列指示詞新增至 `redis.conf`：</span><span class="sxs-lookup"><span data-stu-id="2c0a8-146">(Make a backup copy of the file before you edit it!) Add the following directive to `redis.conf`:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample3.ps1)]

<span data-ttu-id="2c0a8-147">現在啟動 Redis 伺服器：</span><span class="sxs-lookup"><span data-stu-id="2c0a8-147">Now start the Redis server:</span></span>

[!code-css[Main](scaleout-with-redis/samples/sample4.css)]

![](scaleout-with-redis/_static/image4.png)

<span data-ttu-id="2c0a8-148">開啟埠6379，這是 Redis 接聽的預設埠。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-148">Open port 6379, which is the default port that Redis listens on.</span></span> <span data-ttu-id="2c0a8-149">（您可以變更設定檔案中的埠號碼）。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-149">(You can change the port number in the configuration file.)</span></span>

## <a name="create-the-signalr-application"></a><span data-ttu-id="2c0a8-150">建立 SignalR 應用程式</span><span class="sxs-lookup"><span data-stu-id="2c0a8-150">Create the SignalR Application</span></span>

<span data-ttu-id="2c0a8-151">遵循下列其中一個教學課程來建立 SignalR 應用程式：</span><span class="sxs-lookup"><span data-stu-id="2c0a8-151">Create a SignalR application by following either of these tutorials:</span></span>

- [<span data-ttu-id="2c0a8-152">使用 SignalR 2.0 的消費者入門</span><span class="sxs-lookup"><span data-stu-id="2c0a8-152">Getting Started with SignalR 2.0</span></span>](../getting-started/tutorial-getting-started-with-signalr.md)
- [<span data-ttu-id="2c0a8-153">使用 SignalR 2.0 和 MVC 5 的消費者入門</span><span class="sxs-lookup"><span data-stu-id="2c0a8-153">Getting Started with SignalR 2.0 and MVC 5</span></span>](../getting-started/tutorial-getting-started-with-signalr-and-mvc.md)

<span data-ttu-id="2c0a8-154">接下來，我們將修改聊天應用程式，以支援使用 Redis 的向外延展。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-154">Next, we'll modify the chat application to support scaleout with Redis.</span></span> <span data-ttu-id="2c0a8-155">首先，將 `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet 封裝新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-155">First, add the `Microsoft.AspNet.SignalR.StackExchangeRedis` NuGet package to your project.</span></span> <span data-ttu-id="2c0a8-156">在 Visual Studio 中，從 [**工具**] 功能表選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-156">In Visual Studio, from the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="2c0a8-157">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="2c0a8-157">In the Package Manager Console window, enter the following command:</span></span>

[!code-powershell[Main](scaleout-with-redis/samples/sample5.ps1)]

<span data-ttu-id="2c0a8-158">接下來，開啟 Startup.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-158">Next, open the Startup.cs file.</span></span> <span data-ttu-id="2c0a8-159">將下列程式碼新增至**Configuration**方法：</span><span class="sxs-lookup"><span data-stu-id="2c0a8-159">Add the following code to the **Configuration** method:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample6.cs)]

- <span data-ttu-id="2c0a8-160">「伺服器」是正在執行 Redis 的伺服器名稱。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-160">"server" is the name of the server that is running Redis.</span></span>
- <span data-ttu-id="2c0a8-161">*port*是埠號碼</span><span class="sxs-lookup"><span data-stu-id="2c0a8-161">*port* is the port number</span></span>
- <span data-ttu-id="2c0a8-162">「密碼」是您在 redis 檔案中定義的密碼。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-162">"password" is the password that you defined in the redis.conf file.</span></span>
- <span data-ttu-id="2c0a8-163">"AppName" 為任何字串。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-163">"AppName" is any string.</span></span> <span data-ttu-id="2c0a8-164">SignalR 會使用此名稱建立 Redis pub/sub 通道。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-164">SignalR creates a Redis pub/sub channel with this name.</span></span>

<span data-ttu-id="2c0a8-165">例如:</span><span class="sxs-lookup"><span data-stu-id="2c0a8-165">For example:</span></span>

[!code-csharp[Main](scaleout-with-redis/samples/sample7.cs)]

## <a name="deploy-and-run-the-application"></a><span data-ttu-id="2c0a8-166">部署和執行應用程式</span><span class="sxs-lookup"><span data-stu-id="2c0a8-166">Deploy and Run the Application</span></span>

<span data-ttu-id="2c0a8-167">準備您的 Windows Server 實例以部署 SignalR 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-167">Prepare your Windows Server instances to deploy the SignalR application.</span></span>

<span data-ttu-id="2c0a8-168">新增 IIS 角色。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-168">Add the IIS role.</span></span> <span data-ttu-id="2c0a8-169">包含「應用程式開發」功能，包括 WebSocket 通訊協定。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-169">Include "Application Development" features, including the WebSocket Protocol.</span></span>

![](scaleout-with-redis/_static/image5.png)

<span data-ttu-id="2c0a8-170">也請包含管理服務（列在 [管理工具] 底下）。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-170">Also include the Management Service (listed under "Management Tools").</span></span>

![](scaleout-with-redis/_static/image6.png)

<span data-ttu-id="2c0a8-171">**安裝 Web Deploy 3.0。**</span><span class="sxs-lookup"><span data-stu-id="2c0a8-171">**Install Web Deploy 3.0.**</span></span> <span data-ttu-id="2c0a8-172">當您執行 IIS 管理員時，它會提示您安裝 Microsoft Web Platform，或者您可以[下載安裝程式](https://go.microsoft.com/fwlink/?LinkId=255386)。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-172">When you run IIS Manager, it will prompt you to install Microsoft Web Platform, or you can [download the installer](https://go.microsoft.com/fwlink/?LinkId=255386).</span></span> <span data-ttu-id="2c0a8-173">在平臺安裝程式中，搜尋 Web Deploy 並安裝 Web Deploy 3。0</span><span class="sxs-lookup"><span data-stu-id="2c0a8-173">In the Platform Installer, search for Web Deploy and install Web Deploy 3.0</span></span>

![](scaleout-with-redis/_static/image7.png)

<span data-ttu-id="2c0a8-174">檢查 Web 管理服務是否正在執行。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-174">Check that the Web Management Service is running.</span></span> <span data-ttu-id="2c0a8-175">如果沒有，請啟動服務。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-175">If not, start the service.</span></span> <span data-ttu-id="2c0a8-176">（如果您在 Windows 服務清單中看不到 [Web 管理服務]，請確定您已在新增 IIS 角色時安裝管理服務）。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-176">(If you don't see Web Management Service in the list of Windows services, make sure that you installed the Management Service when you added the IIS role.)</span></span>

<span data-ttu-id="2c0a8-177">根據預設，Web 管理服務會接聽 TCP 通訊埠8172。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-177">By default, the Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="2c0a8-178">在 Windows 防火牆中，建立新的輸入規則，以允許埠8172上的 TCP 流量。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-178">In Windows Firewall, create a new inbound rule to allow TCP traffic on port 8172.</span></span> <span data-ttu-id="2c0a8-179">如需詳細資訊，請參閱設定[防火牆規則](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-179">For more information, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="2c0a8-180">（如果您要在 Azure 上裝載 Vm，您可以直接在 Azure 入口網站中執行此動作。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-180">(If you are hosting the VMs on Azure, you can do this directly in the Azure portal.</span></span> <span data-ttu-id="2c0a8-181">請參閱[如何設定虛擬機器的端點](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/)。）</span><span class="sxs-lookup"><span data-stu-id="2c0a8-181">See [How to Set Up Endpoints to a Virtual Machine](https://azure.microsoft.com/documentation/articles/virtual-machines-set-up-endpoints/).)</span></span>

<span data-ttu-id="2c0a8-182">現在您已準備好從開發電腦將 Visual Studio 專案部署到伺服器。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-182">Now you are ready to deploy the Visual Studio project from your development machine to the server.</span></span> <span data-ttu-id="2c0a8-183">在方案總管中，以滑鼠右鍵按一下方案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-183">In Solution Explorer, right-click the solution and click **Publish**.</span></span>

<span data-ttu-id="2c0a8-184">如需 web 部署的詳細檔，請參閱[Visual Studio 和 ASP.NET 的 Web 部署內容對應](../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-184">For more detailed documentation about web deployment, see [Web Deployment Content Map for Visual Studio and ASP.NET](../../../whitepapers/aspnet-web-deployment-content-map.md).</span></span>

<span data-ttu-id="2c0a8-185">如果您將應用程式部署至兩部伺服器，您可以在另一個瀏覽器視窗中開啟每個實例，並查看每個實例都會收到來自另一個的 SignalR 訊息。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-185">If you deploy the application to two servers, you can open each instance in a separate browser window and see that they each receive SignalR messages from the other.</span></span> <span data-ttu-id="2c0a8-186">（當然，在生產環境中，這兩部伺服器會位於負載平衡器後方）。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-186">(Of course, in a production environment, the two servers would sit behind a load balancer.)</span></span>

![](scaleout-with-redis/_static/image8.png)

<span data-ttu-id="2c0a8-187">如果您想要查看傳送至 Redis 的訊息，可以使用**Redis cli**用戶端，它會與 Redis 一起安裝。</span><span class="sxs-lookup"><span data-stu-id="2c0a8-187">If you're curious to see the messages that are sent to Redis, you can use the **redis-cli** client, which installs with Redis.</span></span>

[!code-xml[Main](scaleout-with-redis/samples/sample8.xml)]

![](scaleout-with-redis/_static/image9.png)
