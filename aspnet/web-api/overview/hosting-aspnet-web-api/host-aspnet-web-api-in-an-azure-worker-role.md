---
uid: web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
title: Azure 背景工作角色中的主機 ASP.NET Web API 2-ASP.NET 4。x
author: MikeWasson
description: 教學課程：使用 OWIN 自我裝載 Web API 架構，在 Azure 背景工作角色中裝載 ASP.NET Web API。
ms.author: riande
ms.date: 04/02/2014
ms.custom: seoapril2019
ms.assetid: 6980ee2e-d6b0-4a08-8fb6-ab96362dd0e3
msc.legacyurl: /web-api/overview/hosting-aspnet-web-api/host-aspnet-web-api-in-an-azure-worker-role
msc.type: authoredcontent
ms.openlocfilehash: ec9904e0bff090be0f504036ae73977cfca0cb31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556627"
---
# <a name="host-aspnet-web-api-2-in-an-azure-worker-role"></a><span data-ttu-id="6a192-103">Azure 背景工作角色中的主機 ASP.NET Web API 2</span><span class="sxs-lookup"><span data-stu-id="6a192-103">Host ASP.NET Web API 2 in an Azure Worker Role</span></span>

<span data-ttu-id="6a192-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="6a192-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="6a192-105">本教學課程說明如何使用 OWIN 自我裝載 Web API 架構，在 Azure 背景工作角色中裝載 ASP.NET Web API。</span><span class="sxs-lookup"><span data-stu-id="6a192-105">This tutorial shows how to host ASP.NET Web API in an Azure Worker Role, using OWIN to self-host the Web API framework.</span></span>
>
> <span data-ttu-id="6a192-106">[Open Web Interface for .net](http://owin.org/) （OWIN）會定義 .net Web 服務器和 Web 應用程式之間的抽象概念。</span><span class="sxs-lookup"><span data-stu-id="6a192-106">[Open Web Interface for .NET](http://owin.org/) (OWIN) defines an abstraction between .NET web servers and web applications.</span></span> <span data-ttu-id="6a192-107">OWIN 會將 web 應用程式與伺服器分離，讓 OWIN 非常適合用於在您自己的進程中自我裝載 web 應用程式（在 IIS 之外），例如在 Azure 背景工作角色中。</span><span class="sxs-lookup"><span data-stu-id="6a192-107">OWIN decouples the web application from the server, which makes OWIN ideal for self-hosting a web application in your own process, outside of IIS–for example, inside an Azure worker role.</span></span>
>
> <span data-ttu-id="6a192-108">在本教學課程中，您將使用 HttpListener 套件，它提供了用於自我裝載 OWIN 應用程式的 HTTP 伺服器。</span><span class="sxs-lookup"><span data-stu-id="6a192-108">In this tutorial, you'll use the Microsoft.Owin.Host.HttpListener package, which provides an HTTP server that be used to self-host OWIN applications.</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="6a192-109">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="6a192-109">Software versions used in the tutorial</span></span>
>
>
> - [<span data-ttu-id="6a192-110">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="6a192-110">Visual Studio 2013</span></span>](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)
> - <span data-ttu-id="6a192-111">Web API 2</span><span class="sxs-lookup"><span data-stu-id="6a192-111">Web API 2</span></span>
> - [<span data-ttu-id="6a192-112">Azure SDK for .NET 2。3</span><span class="sxs-lookup"><span data-stu-id="6a192-112">Azure SDK for .NET 2.3</span></span>](https://azure.microsoft.com/downloads/)

## <a name="create-a-microsoft-azure-project"></a><span data-ttu-id="6a192-113">建立 Microsoft Azure 專案</span><span class="sxs-lookup"><span data-stu-id="6a192-113">Create a Microsoft Azure Project</span></span>

<span data-ttu-id="6a192-114">使用系統管理員許可權啟動 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="6a192-114">Start Visual Studio with administrator privileges.</span></span> <span data-ttu-id="6a192-115">您需要有系統管理員許可權，才能使用 Azure 計算模擬器在本機上進行應用程式的 debug。</span><span class="sxs-lookup"><span data-stu-id="6a192-115">Administrator privileges are needed to debug the application locally, using the Azure compute emulator.</span></span>

<span data-ttu-id="6a192-116">**在 [檔案**] 功能表上，按一下 [**新增**]，然後按一下 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="6a192-116">On the **File** menu, click **New**, then click **Project**.</span></span> <span data-ttu-id="6a192-117">從 **已安裝**的範本C# 的 視覺效果 底下，按一下 **雲端**，然後按一下  **Windows Azure 雲端服務**</span><span class="sxs-lookup"><span data-stu-id="6a192-117">From **Installed Templates**, under Visual C#, click **Cloud** and then click **Windows Azure Cloud Service**.</span></span> <span data-ttu-id="6a192-118">將專案命名為 "Azureapp.java"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="6a192-118">Name the project "AzureApp" and click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image2.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image1.png)

<span data-ttu-id="6a192-119">在 [**新的 Windows Azure 雲端服務**] 對話方塊中，按兩下 [背景**工作角色**]。</span><span class="sxs-lookup"><span data-stu-id="6a192-119">In the **New Windows Azure Cloud Service** dialog, double-click **Worker Role**.</span></span> <span data-ttu-id="6a192-120">保留預設名稱（"WorkerRole1"）。</span><span class="sxs-lookup"><span data-stu-id="6a192-120">Leave the default name ("WorkerRole1").</span></span> <span data-ttu-id="6a192-121">此步驟會將背景工作角色新增至解決方案。</span><span class="sxs-lookup"><span data-stu-id="6a192-121">This step adds a worker role to the solution.</span></span> <span data-ttu-id="6a192-122">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="6a192-122">Click **OK**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image4.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image3.png)

<span data-ttu-id="6a192-123">所建立的 Visual Studio 解決方案包含兩個專案：</span><span class="sxs-lookup"><span data-stu-id="6a192-123">The Visual Studio solution that is created contains two projects:</span></span>

- <span data-ttu-id="6a192-124">&quot;Azureapp.java&quot; 定義 Azure 應用程式的角色和設定。</span><span class="sxs-lookup"><span data-stu-id="6a192-124">&quot;AzureApp&quot; defines the roles and configuration for the Azure application.</span></span>
- <span data-ttu-id="6a192-125">&quot;WorkerRole1&quot; 包含背景工作角色的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6a192-125">&quot;WorkerRole1&quot; contains the code for the worker role.</span></span>

<span data-ttu-id="6a192-126">一般而言，Azure 應用程式可以包含多個角色，雖然本教學課程使用單一角色。</span><span class="sxs-lookup"><span data-stu-id="6a192-126">In general, an Azure application can contain multiple roles, although this tutorial uses a single role.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image5.png)

## <a name="add-the-web-api-and-owin-packages"></a><span data-ttu-id="6a192-127">新增 Web API 和 OWIN 套件</span><span class="sxs-lookup"><span data-stu-id="6a192-127">Add the Web API and OWIN Packages</span></span>

<span data-ttu-id="6a192-128">從 [**工具**] 功能表中，按一下 [ **NuGet 套件管理員**]，然後按一下 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="6a192-128">From the **Tools** menu, click **NuGet Package Manager**, then click **Package Manager Console**.</span></span>

<span data-ttu-id="6a192-129">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6a192-129">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample1.cmd)]

## <a name="add-an-http-endpoint"></a><span data-ttu-id="6a192-130">新增 HTTP 端點</span><span class="sxs-lookup"><span data-stu-id="6a192-130">Add an HTTP Endpoint</span></span>

<span data-ttu-id="6a192-131">在方案總管中，展開 [Azureapp.java] 專案。</span><span class="sxs-lookup"><span data-stu-id="6a192-131">In Solution Explorer, expand the AzureApp project.</span></span> <span data-ttu-id="6a192-132">展開 [角色] 節點，以滑鼠右鍵按一下 [WorkerRole1]，然後選取 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="6a192-132">Expand the Roles node, right-click WorkerRole1, and select **Properties**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image6.png)

<span data-ttu-id="6a192-133">按一下 **[端點]** ，然後按一下 **[新增端點]** 。</span><span class="sxs-lookup"><span data-stu-id="6a192-133">Click **Endpoints**, and then click **Add Endpoint**.</span></span>

<span data-ttu-id="6a192-134">在 [**通訊協定**] 下拉式清單中，選取 [HTTP]。</span><span class="sxs-lookup"><span data-stu-id="6a192-134">In the **Protocol** dropdown list, select "http".</span></span> <span data-ttu-id="6a192-135">在 [**公用埠**] 和 [**私人埠**] 中，輸入80。</span><span class="sxs-lookup"><span data-stu-id="6a192-135">In **Public Port** and **Private Port**, type 80.</span></span> <span data-ttu-id="6a192-136">這些連接埠號碼可以不同。</span><span class="sxs-lookup"><span data-stu-id="6a192-136">These port numbers can be different.</span></span> <span data-ttu-id="6a192-137">公用埠是用戶端將要求傳送至角色時所使用的。</span><span class="sxs-lookup"><span data-stu-id="6a192-137">The public port is what clients use when they send a request to the role.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image8.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image7.png)

## <a name="configure-web-api-for-self-host"></a><span data-ttu-id="6a192-138">設定適用于自我裝載的 Web API</span><span class="sxs-lookup"><span data-stu-id="6a192-138">Configure Web API for Self-Host</span></span>

<span data-ttu-id="6a192-139">在方案總管中，以滑鼠右鍵按一下 WorkerRole1 專案，然後選取 [**新增** / **類別**] 以加入新的類別。</span><span class="sxs-lookup"><span data-stu-id="6a192-139">In Solution Explorer, right click the WorkerRole1 project and select **Add** / **Class** to add a new class.</span></span> <span data-ttu-id="6a192-140">將類別命名為 `Startup`。</span><span class="sxs-lookup"><span data-stu-id="6a192-140">Name the class `Startup`.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image9.png)

<span data-ttu-id="6a192-141">以下列內容取代此檔案中的所有重複使用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="6a192-141">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample2.cs)]

## <a name="add-a-web-api-controller"></a><span data-ttu-id="6a192-142">新增 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="6a192-142">Add a Web API Controller</span></span>

<span data-ttu-id="6a192-143">接下來，新增 Web API 控制器類別。</span><span class="sxs-lookup"><span data-stu-id="6a192-143">Next, add a Web API controller class.</span></span> <span data-ttu-id="6a192-144">以滑鼠右鍵按一下 [WorkerRole1] 專案，然後選取 [**新增** / **類別**]。</span><span class="sxs-lookup"><span data-stu-id="6a192-144">Right-click the WorkerRole1 project and select **Add** / **Class**.</span></span> <span data-ttu-id="6a192-145">將類別命名為 TestController。</span><span class="sxs-lookup"><span data-stu-id="6a192-145">Name the class TestController.</span></span> <span data-ttu-id="6a192-146">以下列內容取代此檔案中的所有重複使用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="6a192-146">Replace all of the boilerplate code in this file with the following:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample3.cs)]

<span data-ttu-id="6a192-147">為了簡單起見，此控制器只會定義兩個會傳回純文字的 GET 方法。</span><span class="sxs-lookup"><span data-stu-id="6a192-147">For simplicity, this controller just defines two GET methods that return plain text.</span></span>

## <a name="start-the-owin-host"></a><span data-ttu-id="6a192-148">啟動 OWIN 主機</span><span class="sxs-lookup"><span data-stu-id="6a192-148">Start the OWIN Host</span></span>

<span data-ttu-id="6a192-149">開啟 WorkerRole.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="6a192-149">Open the WorkerRole.cs file.</span></span> <span data-ttu-id="6a192-150">這個類別會定義背景工作角色啟動和停止時所執行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6a192-150">This class defines the code that runs when the worker role is started and stopped.</span></span>

<span data-ttu-id="6a192-151">加入下列 using 陳述式：</span><span class="sxs-lookup"><span data-stu-id="6a192-151">Add the following using statement:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample4.cs)]

<span data-ttu-id="6a192-152">將**IDisposable**成員新增至 `WorkerRole` 類別：</span><span class="sxs-lookup"><span data-stu-id="6a192-152">Add an **IDisposable** member to the `WorkerRole` class:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample5.cs)]

<span data-ttu-id="6a192-153">在 `OnStart` 方法中，新增下列程式碼以啟動主機：</span><span class="sxs-lookup"><span data-stu-id="6a192-153">In the `OnStart` method, add the following code to start the host:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample6.cs?highlight=5)]

<span data-ttu-id="6a192-154">**WebApp**方法啟動 OWIN 主機。</span><span class="sxs-lookup"><span data-stu-id="6a192-154">The **WebApp.Start** method starts the OWIN host.</span></span> <span data-ttu-id="6a192-155">`Startup` 類別的名稱是方法的型別參數。</span><span class="sxs-lookup"><span data-stu-id="6a192-155">The name of the `Startup` class is a type parameter to the method.</span></span> <span data-ttu-id="6a192-156">依照慣例，主機會呼叫這個類別的 `Configure` 方法。</span><span class="sxs-lookup"><span data-stu-id="6a192-156">By convention, the host will call the `Configure` method of this class.</span></span>

<span data-ttu-id="6a192-157">覆寫 `OnStop` 以處置 *\_應用程式*實例：</span><span class="sxs-lookup"><span data-stu-id="6a192-157">Override the `OnStop` to dispose of the *\_app* instance:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample7.cs)]

<span data-ttu-id="6a192-158">以下是 WorkerRole.cs 的完整程式碼：</span><span class="sxs-lookup"><span data-stu-id="6a192-158">Here is the complete code for WorkerRole.cs:</span></span>

[!code-csharp[Main](host-aspnet-web-api-in-an-azure-worker-role/samples/sample8.cs)]

<span data-ttu-id="6a192-159">建立解決方案，然後按 F5 在 Azure 計算模擬器中本機執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6a192-159">Build the solution, and press F5 to run the application locally in the Azure Compute Emulator.</span></span> <span data-ttu-id="6a192-160">根據您的防火牆設定，您可能需要允許模擬器通過防火牆。</span><span class="sxs-lookup"><span data-stu-id="6a192-160">Depending on your firewall settings, you might need to allow the emulator through your firewall.</span></span>

> [!NOTE]
> <span data-ttu-id="6a192-161">如果您收到類似下面的例外狀況，請參閱[這篇 blog 文章](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx)以取得因應措施。</span><span class="sxs-lookup"><span data-stu-id="6a192-161">If you get an exception like the following, please see [this blog post](https://blogs.msdn.com/b/praburaj/archive/2013/11/20/fileloadexception-on-microsoft-owin-when-running-on-worker-role.aspx) for a workaround.</span></span> <span data-ttu-id="6a192-162">「無法載入檔案或元件 ' Owin，Version = 2.0.2.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35 ' 或其相依性的其中之一。</span><span class="sxs-lookup"><span data-stu-id="6a192-162">"Could not load file or assembly 'Microsoft.Owin, Version=2.0.2.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35' or one of its dependencies.</span></span> <span data-ttu-id="6a192-163">找不到元件的資訊清單定義與元件參考不符。</span><span class="sxs-lookup"><span data-stu-id="6a192-163">The located assembly's manifest definition does not match the assembly reference.</span></span> <span data-ttu-id="6a192-164">（來自 HRESULT 的例外狀況：0x80131040）」</span><span class="sxs-lookup"><span data-stu-id="6a192-164">(Exception from HRESULT: 0x80131040)"</span></span>

<span data-ttu-id="6a192-165">計算模擬器會將本機 IP 位址指派給端點。</span><span class="sxs-lookup"><span data-stu-id="6a192-165">The compute emulator assigns a local IP address to the endpoint.</span></span> <span data-ttu-id="6a192-166">您可以藉由查看計算模擬器 UI 來尋找 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6a192-166">You can find the IP address by viewing the Compute Emulator UI.</span></span> <span data-ttu-id="6a192-167">以滑鼠右鍵按一下工作列通知區域中的模擬器圖示，然後選取 [**顯示計算模擬器 UI**]。</span><span class="sxs-lookup"><span data-stu-id="6a192-167">Right-click the emulator icon in the task bar notification area, and select **Show Compute Emulator UI**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image11.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image10.png)

<span data-ttu-id="6a192-168">尋找 [服務部署]、[部署 [識別碼]]、[服務詳細資料] 底下的 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="6a192-168">Find the IP address under Service Deployments, deployment [id], Service Details.</span></span> <span data-ttu-id="6a192-169">開啟網頁瀏覽器並流覽至 HTTP://<em>address</em>/test/1，其中<em>address</em>是計算模擬器所指派的 IP 位址;例如，`http://127.0.0.1:80/test/1`。</span><span class="sxs-lookup"><span data-stu-id="6a192-169">Open a web browser and navigate to http://<em>address</em>/test/1, where <em>address</em> is the IP address assigned by the compute emulator; for example, `http://127.0.0.1:80/test/1`.</span></span> <span data-ttu-id="6a192-170">您應該會看到來自 Web API 控制器的回應：</span><span class="sxs-lookup"><span data-stu-id="6a192-170">You should see the response from the Web API controller:</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image12.png)

## <a name="deploy-to-azure"></a><span data-ttu-id="6a192-171">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="6a192-171">Deploy to Azure</span></span>

<span data-ttu-id="6a192-172">在此步驟中，您必須擁有 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a192-172">For this step, you must have an Azure account.</span></span> <span data-ttu-id="6a192-173">如果您還沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。</span><span class="sxs-lookup"><span data-stu-id="6a192-173">If you don't already have one, you can create a free trial account in just a couple of minutes.</span></span> <span data-ttu-id="6a192-174">如需詳細資訊，請參閱[Microsoft Azure 免費試用](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F)。</span><span class="sxs-lookup"><span data-stu-id="6a192-174">For details, see [Microsoft Azure Free Trial](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A261C142F).</span></span>

<span data-ttu-id="6a192-175">在方案總管中，以滑鼠右鍵按一下 [Azureapp.java] 專案。</span><span class="sxs-lookup"><span data-stu-id="6a192-175">In Solution Explorer, right-click the AzureApp project.</span></span> <span data-ttu-id="6a192-176">選取 [發行]。</span><span class="sxs-lookup"><span data-stu-id="6a192-176">Select **Publish**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image13.png)

<span data-ttu-id="6a192-177">如果您未登入您的 Azure 帳戶，請按一下 [登**入**]。</span><span class="sxs-lookup"><span data-stu-id="6a192-177">If you are not signed in to your Azure account, click **Sign In**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image15.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image14.png)

<span data-ttu-id="6a192-178">登入之後，請選擇訂用帳戶，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="6a192-178">After you are signed in, choose a subscription and click **Next**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image17.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image16.png)

<span data-ttu-id="6a192-179">輸入雲端服務的名稱，然後選擇 [區域]。</span><span class="sxs-lookup"><span data-stu-id="6a192-179">Enter a name for the cloud service and choose a region.</span></span> <span data-ttu-id="6a192-180">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="6a192-180">Click **Create**.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image18.png)

<span data-ttu-id="6a192-181">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="6a192-181">Click **Publish**.</span></span>

[![](host-aspnet-web-api-in-an-azure-worker-role/_static/image20.png)](host-aspnet-web-api-in-an-azure-worker-role/_static/image19.png)

<span data-ttu-id="6a192-182">[Azure 活動記錄] 視窗會顯示部署的進度。</span><span class="sxs-lookup"><span data-stu-id="6a192-182">The Azure Activity Log window shows the progress of the deployment.</span></span> <span data-ttu-id="6a192-183">部署應用程式時，請流覽至 http://appname.cloudapp.net/test/1。</span><span class="sxs-lookup"><span data-stu-id="6a192-183">When the app is deployed, browse to http://appname.cloudapp.net/test/1.</span></span>

![](host-aspnet-web-api-in-an-azure-worker-role/_static/image21.png)

## <a name="additional-resources"></a><span data-ttu-id="6a192-184">其他資源</span><span class="sxs-lookup"><span data-stu-id="6a192-184">Additional Resources</span></span>

- [<span data-ttu-id="6a192-185">Katana 專案概觀</span><span class="sxs-lookup"><span data-stu-id="6a192-185">An Overview of Project Katana</span></span>](../../../aspnet/overview/owin-and-katana/an-overview-of-project-katana.md)
- [<span data-ttu-id="6a192-186">GitHub 上的 Katana 專案</span><span class="sxs-lookup"><span data-stu-id="6a192-186">Katana Project on GitHub</span></span>](https://github.com/aspnet/AspNetKatana)
