---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
title: 設定用於 Web Deploy 發佈的 Web 服務器（離線部署） |Microsoft Docs
author: jrjlee
description: 本主題說明如何設定 IIS web 伺服器，以支援離線 web 發行和部署。 當您使用 Internet Information Services （I 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ba92788f-9f03-44b1-b6b2-af8413e6a35d
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment
msc.type: authoredcontent
ms.openlocfilehash: f93cf11085fb19afb97b71aca8f638bd88fe658b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621104"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-offline-deployment"></a><span data-ttu-id="2efa0-104">設定 Web Deploy 發行的網頁伺服器 (離線部署)</span><span class="sxs-lookup"><span data-stu-id="2efa0-104">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>

<span data-ttu-id="2efa0-105">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="2efa0-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="2efa0-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="2efa0-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="2efa0-107">本主題說明如何設定 IIS web 伺服器，以支援離線 web 發行和部署。</span><span class="sxs-lookup"><span data-stu-id="2efa0-107">This topic describes how to configure an IIS web server to support offline web publishing and deployment.</span></span>
> 
> <span data-ttu-id="2efa0-108">當您使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）2.0 或更新版本時，您可以使用三種主要方法，將您的應用程式或網站放在 Web 服務器上。</span><span class="sxs-lookup"><span data-stu-id="2efa0-108">When you work with Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="2efa0-109">您可以：</span><span class="sxs-lookup"><span data-stu-id="2efa0-109">You can:</span></span>
> 
> - <span data-ttu-id="2efa0-110">使用*Web Deploy 的遠端代理程式服務*。</span><span class="sxs-lookup"><span data-stu-id="2efa0-110">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="2efa0-111">這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何專案部署至伺服器。</span><span class="sxs-lookup"><span data-stu-id="2efa0-111">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="2efa0-112">使用*Web Deploy 處理常式*。</span><span class="sxs-lookup"><span data-stu-id="2efa0-112">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="2efa0-113">這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="2efa0-113">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="2efa0-114">不過，當您使用這種方法時，可以設定 IIS 以允許非系統管理員使用者執行部署。</span><span class="sxs-lookup"><span data-stu-id="2efa0-114">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="2efa0-115">Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2efa0-115">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="2efa0-116">使用*離線部署*。</span><span class="sxs-lookup"><span data-stu-id="2efa0-116">Use *offline deployment*.</span></span> <span data-ttu-id="2efa0-117">此方法需要最少的 web 伺服器設定，但伺服器管理員必須手動將 web 套件複製到伺服器，並透過 IIS 管理員將其匯入。</span><span class="sxs-lookup"><span data-stu-id="2efa0-117">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="2efa0-118">如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱[選擇正確的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="2efa0-118">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

<span data-ttu-id="2efa0-119">是，如果您的網路基礎結構或安全性限制阻止遠端部署。</span><span class="sxs-lookup"><span data-stu-id="2efa0-119">Yes, if your network infrastructure or security restrictions prevent remote deployment.</span></span> <span data-ttu-id="2efa0-120">在網際網路對向的生產環境中，這是很可能的情況，其中 web 伺服器會從&#x2014;伺服器基礎結構的其餘部分，&#x2014;實際或由防火牆和子網隔離。</span><span class="sxs-lookup"><span data-stu-id="2efa0-120">This is most likely to be the case in Internet-facing production environments, where the web servers are isolated&#x2014;either physically or by firewalls and subnets&#x2014;from the rest of your server infrastructure.</span></span>

<span data-ttu-id="2efa0-121">很明顯地，如果您的 web 應用程式定期更新，這個方法就會變得較不理想。</span><span class="sxs-lookup"><span data-stu-id="2efa0-121">Obviously, this approach becomes less desirable if your web applications are updated on a regular basis.</span></span> <span data-ttu-id="2efa0-122">如果您的基礎結構允許，您可以考慮使用 Web Deploy 處理常式或 Web Deploy 遠端代理程式服務來啟用遠端部署。</span><span class="sxs-lookup"><span data-stu-id="2efa0-122">If your infrastructure allows it, you may want to consider enabling remote deployment, using either the Web Deploy Handler or the Web Deploy Remote Agent Service.</span></span>

## <a name="task-overview"></a><span data-ttu-id="2efa0-123">工作總覽</span><span class="sxs-lookup"><span data-stu-id="2efa0-123">Task Overview</span></span>

<span data-ttu-id="2efa0-124">若要將網頁伺服器設定為支援離線匯入和部署 web 套件，您必須：</span><span class="sxs-lookup"><span data-stu-id="2efa0-124">To configure the web server to support offline import and deployment of web packages, you'll need to:</span></span>

- <span data-ttu-id="2efa0-125">安裝 IIS 7.5 和 IIS 7 建議的設定。</span><span class="sxs-lookup"><span data-stu-id="2efa0-125">Install IIS 7.5 and the IIS 7 recommended configuration.</span></span>
- <span data-ttu-id="2efa0-126">安裝 Web Deploy 2.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="2efa0-126">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="2efa0-127">建立 IIS 網站來裝載已部署的內容。</span><span class="sxs-lookup"><span data-stu-id="2efa0-127">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="2efa0-128">停用 Web Deployment Agent 服務。</span><span class="sxs-lookup"><span data-stu-id="2efa0-128">Disable the Web Deployment Agent Service.</span></span>

<span data-ttu-id="2efa0-129">若要明確裝載範例解決方案，您也需要：</span><span class="sxs-lookup"><span data-stu-id="2efa0-129">To host the sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="2efa0-130">安裝 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="2efa0-130">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="2efa0-131">安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="2efa0-131">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="2efa0-132">本主題將說明如何執行上述每個程式。</span><span class="sxs-lookup"><span data-stu-id="2efa0-132">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="2efa0-133">本主題中的工作和逐步解說假設您是從執行 Windows Server 2008 R2 的全新伺服器組建開始。</span><span class="sxs-lookup"><span data-stu-id="2efa0-133">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2008 R2.</span></span> <span data-ttu-id="2efa0-134">在繼續之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="2efa0-134">Before you continue, ensure that:</span></span>

- <span data-ttu-id="2efa0-135">Windows Server 2008 R2 Service Pack 1 和所有可用的更新都已安裝。</span><span class="sxs-lookup"><span data-stu-id="2efa0-135">Windows Server 2008 R2 Service Pack 1 and all available updates are installed.</span></span>
- <span data-ttu-id="2efa0-136">伺服器已加入網域。</span><span class="sxs-lookup"><span data-stu-id="2efa0-136">The server is domain-joined.</span></span>
- <span data-ttu-id="2efa0-137">伺服器具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="2efa0-137">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="2efa0-138">如需將電腦加入網域的詳細資訊，請參閱[將電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。</span><span class="sxs-lookup"><span data-stu-id="2efa0-138">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="2efa0-139">如需設定靜態 IP 位址的詳細資訊，請參閱[設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2efa0-139">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="2efa0-140">安裝產品和元件</span><span class="sxs-lookup"><span data-stu-id="2efa0-140">Install Products and Components</span></span>

<span data-ttu-id="2efa0-141">本節將引導您在 web 伺服器上安裝必要的產品和元件。</span><span class="sxs-lookup"><span data-stu-id="2efa0-141">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="2efa0-142">在開始之前，最好先執行 Windows Update，以確保您的伺服器完全保持在最新狀態。</span><span class="sxs-lookup"><span data-stu-id="2efa0-142">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="2efa0-143">在此情況下，您需要安裝下列專案：</span><span class="sxs-lookup"><span data-stu-id="2efa0-143">In this case, you need to install these things:</span></span>

- <span data-ttu-id="2efa0-144">**IIS 7 建議**的設定。</span><span class="sxs-lookup"><span data-stu-id="2efa0-144">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="2efa0-145">這會啟用 web 伺服器上的**網頁伺服器（iis）** 角色，並安裝您需要的一組 IIS 模組和元件，才能裝載 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="2efa0-145">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="2efa0-146">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="2efa0-146">**.NET Framework 4.0**.</span></span> <span data-ttu-id="2efa0-147">這是執行此版本 .NET Framework 所建立之應用程式的必要項。</span><span class="sxs-lookup"><span data-stu-id="2efa0-147">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="2efa0-148">**Web Deployment Tool 2.1 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="2efa0-148">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="2efa0-149">這會在您的伺服器上安裝 Web Deploy （及其基礎可執行檔，Msdeploy.exe）。</span><span class="sxs-lookup"><span data-stu-id="2efa0-149">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="2efa0-150">Web Deploy 與 IIS 整合，並可讓您匯入和匯出 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="2efa0-150">Web Deploy integrates with IIS and lets you import and export web packages.</span></span>
- <span data-ttu-id="2efa0-151">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="2efa0-151">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="2efa0-152">這會安裝執行 MVC 3 應用程式所需的元件。</span><span class="sxs-lookup"><span data-stu-id="2efa0-152">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="2efa0-153">本逐步解說說明如何使用 Web Platform Installer 來安裝和設定各種元件。</span><span class="sxs-lookup"><span data-stu-id="2efa0-153">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="2efa0-154">雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。</span><span class="sxs-lookup"><span data-stu-id="2efa0-154">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="2efa0-155">如需詳細資訊，請參閱[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="2efa0-155">For more information, see [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="2efa0-156">**若要安裝必要的產品和元件**</span><span class="sxs-lookup"><span data-stu-id="2efa0-156">**To install the required products and components**</span></span>

1. <span data-ttu-id="2efa0-157">下載並安裝[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="2efa0-157">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="2efa0-158">安裝完成時，Web Platform Installer 會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="2efa0-158">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2efa0-159">您現在可以隨時從 [**開始**] 功能表啟動 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="2efa0-159">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="2efa0-160">若要這樣做，請在 [**開始**] 功能表上，按一下 [**所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-160">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="2efa0-161">在 [ **Web Platform Installer 3.0** ] 視窗頂端，按一下 [**產品**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-161">At the top of the **Web Platform Installer 3.0** window, click **Products**.</span></span>
4. <span data-ttu-id="2efa0-162">在視窗左側的流覽窗格中 **，按一下 [** 架構]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-162">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="2efa0-163">在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-163">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="2efa0-164">您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="2efa0-164">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="2efa0-165">如果已安裝產品或元件，Web Platform Installer 會以**已安裝**的文字取代 [**新增**] 按鈕來指出這一點。</span><span class="sxs-lookup"><span data-stu-id="2efa0-165">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image1.png)
6. <span data-ttu-id="2efa0-166">在 [ **ASP.NET MVC 3 （Visual Studio 2010）** ] 資料列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-166">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="2efa0-167">在流覽窗格中，按一下 [**伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-167">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="2efa0-168">在 [ **IIS 7 建議**的設定] 列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-168">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="2efa0-169">在 [ **Web Deployment Tool 2.1** ] 資料列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-169">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="2efa0-170">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-170">Click **Install**.</span></span> <span data-ttu-id="2efa0-171">Web Platform Installer 將會顯示一份產品&#x2014;清單，其中包含&#x2014;要安裝的相關聯相依性，並會提示您接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="2efa0-171">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image2.png)
11. <span data-ttu-id="2efa0-172">請參閱授權條款，如果您同意這些條款，請按一下 [**我接受**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-172">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
12. <span data-ttu-id="2efa0-173">當安裝完成時，按一下 **[完成]** ，然後關閉 [ **Web Platform Installer 3.0** ] 視窗。</span><span class="sxs-lookup"><span data-stu-id="2efa0-173">When the installation is complete, click **Finish**, and then close the **Web Platform Installer 3.0** window.</span></span>

<span data-ttu-id="2efa0-174">如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，就必須執行[ASP.NET IIS 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)（aspnet\_regiis），以向 IIS 註冊最新版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="2efa0-174">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="2efa0-175">如果您不這麼做，就會發現 IIS 會提供靜態內容（例如 HTML 檔案），而不會有任何問題，但會傳回**HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時找不到。</span><span class="sxs-lookup"><span data-stu-id="2efa0-175">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="2efa0-176">您可以使用下一個程式來確保 ASP.NET 4.0 已註冊。</span><span class="sxs-lookup"><span data-stu-id="2efa0-176">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="2efa0-177">**向 IIS 註冊 ASP.NET 4。0**</span><span class="sxs-lookup"><span data-stu-id="2efa0-177">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="2efa0-178">按一下 [**開始**]，然後輸入**命令提示**字元。</span><span class="sxs-lookup"><span data-stu-id="2efa0-178">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="2efa0-179">在搜尋結果中，以滑鼠右鍵按一下 [**命令提示**字元]，然後按一下 [以**系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-179">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="2efa0-180">在 [命令提示字元] 視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319**目錄。</span><span class="sxs-lookup"><span data-stu-id="2efa0-180">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="2efa0-181">輸入此命令，然後按 Enter 鍵：</span><span class="sxs-lookup"><span data-stu-id="2efa0-181">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample1.cmd)]
5. <span data-ttu-id="2efa0-182">如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="2efa0-182">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="2efa0-183">若要這麼做，請在 [命令提示字元] 視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319**目錄。</span><span class="sxs-lookup"><span data-stu-id="2efa0-183">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="2efa0-184">輸入此命令，然後按 Enter 鍵：</span><span class="sxs-lookup"><span data-stu-id="2efa0-184">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/samples/sample2.cmd)]

<span data-ttu-id="2efa0-185">建議的作法是，在此時再次使用 Windows Update，下載並安裝您已安裝之新產品和元件的任何可用更新。</span><span class="sxs-lookup"><span data-stu-id="2efa0-185">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-iis-website"></a><span data-ttu-id="2efa0-186">設定 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="2efa0-186">Configure the IIS Website</span></span>

<span data-ttu-id="2efa0-187">您必須先建立並設定 IIS 網站來裝載內容，才能將 web 內容部署到您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="2efa0-187">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="2efa0-188">Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。</span><span class="sxs-lookup"><span data-stu-id="2efa0-188">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="2efa0-189">概括而言，您必須完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="2efa0-189">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="2efa0-190">在檔案系統上建立資料夾，以裝載您的內容。</span><span class="sxs-lookup"><span data-stu-id="2efa0-190">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="2efa0-191">建立 IIS 網站來提供內容，並將它與本機資料夾產生關聯。</span><span class="sxs-lookup"><span data-stu-id="2efa0-191">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="2efa0-192">授與讀取權限給本機資料夾上的應用程式集區身分識別。</span><span class="sxs-lookup"><span data-stu-id="2efa0-192">Grant read permissions to the application pool identity on the local folder.</span></span>

<span data-ttu-id="2efa0-193">雖然沒有任何動作會阻止您將內容部署到 IIS 中的預設網站，但不建議針對測試或示範案例以外的任何專案使用此方法。</span><span class="sxs-lookup"><span data-stu-id="2efa0-193">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="2efa0-194">若要模擬生產環境，您應該使用特定于應用程式需求的設定來建立新的 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="2efa0-194">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="2efa0-195">**建立和設定 IIS 網站**</span><span class="sxs-lookup"><span data-stu-id="2efa0-195">**To create and configure an IIS website**</span></span>

1. <span data-ttu-id="2efa0-196">在本機檔案系統上，建立用來儲存內容的資料夾（例如， **C:\DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="2efa0-196">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="2efa0-197">在 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [ **Internet Information Services （IIS）管理員**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-197">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="2efa0-198">在 **[IIS**管理員] 的 [連線] 窗格中，展開伺服器節點（例如， **PROWEB1**）。</span><span class="sxs-lookup"><span data-stu-id="2efa0-198">In IIS Manager, in the **Connections** pane, expand the server node (for example, **PROWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image3.png)
4. <span data-ttu-id="2efa0-199">以滑鼠右鍵按一下 [**網站**] 節點，然後按一下 [**新增**網站]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-199">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="2efa0-200">在 [**網站名稱**] 方塊中，輸入 IIS 網站的名稱（例如， **DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="2efa0-200">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="2efa0-201">在 [**實體路徑**] 方塊中，輸入（或流覽至）本機資料夾的路徑（例如， **C:\DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="2efa0-201">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="2efa0-202">在 [**埠**] 方塊中，輸入您要用來裝載網站的埠號碼（例如， **85**）。</span><span class="sxs-lookup"><span data-stu-id="2efa0-202">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="2efa0-203">適用于 HTTP 的標準埠號碼為80，HTTPS 則為443。</span><span class="sxs-lookup"><span data-stu-id="2efa0-203">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="2efa0-204">不過，如果您在埠80上裝載此網站，則必須先停止預設網站，才能存取您的網站。</span><span class="sxs-lookup"><span data-stu-id="2efa0-204">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="2efa0-205">除非您要設定網站的網域名稱系統（DNS）記錄，否則請將 [**主機名稱**] 方塊保留空白，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2efa0-205">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="2efa0-206">在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="2efa0-206">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="2efa0-207">如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱[設定網站的主機標頭（iis 7）](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="2efa0-207">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="2efa0-208">如需有關 Windows Server 2008 R2 中 DNS 伺服器角色的詳細資訊，請參閱[Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx)和[dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="2efa0-208">For more information on the DNS Server role in Windows Server 2008 R2, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="2efa0-209">在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-209">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="2efa0-210">在 [**網站**系結] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-210">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image5.png)
11. <span data-ttu-id="2efa0-211">在 [**新增網站**系結] 對話方塊中，將 [ **IP 位址**] 和 [**埠**] 設定為符合您現有的網站設定。</span><span class="sxs-lookup"><span data-stu-id="2efa0-211">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="2efa0-212">在 [**主機名稱**] 方塊中，輸入您的 web 伺服器名稱（例如， **PROWEB1**），然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2efa0-212">In the **Host name** box, type the name of your web server (for example, **PROWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="2efa0-213">第一個網站系結可讓您使用 IP 位址和埠或 `http://localhost:85`，在本機存取網站。</span><span class="sxs-lookup"><span data-stu-id="2efa0-213">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="2efa0-214">第二個網站系結可讓您使用電腦名稱稱（例如 http://proweb1:85) ，從網域中的其他電腦存取網站。</span><span class="sxs-lookup"><span data-stu-id="2efa0-214">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://proweb1:85).</span></span>
13. <span data-ttu-id="2efa0-215">在 [**網站**系結] 對話方塊中，按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-215">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="2efa0-216">**在 [連線**] 窗格中，按一下 [**應用程式**集區]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-216">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="2efa0-217">在 [**應用程式**集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [**基本設定**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-217">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="2efa0-218">根據預設，您的應用程式集區名稱會與您的網站名稱相符（例如， **DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="2efa0-218">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="2efa0-219">在 [ **.NET Framework 版本**] 清單中，選取 [ **.NET Framework v 4.0.30319**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2efa0-219">In the **.NET Framework version** list, select **.NET Framework v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image7.png)

    > [!NOTE]
    > <span data-ttu-id="2efa0-220">範例解決方案需要 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="2efa0-220">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="2efa0-221">這不是一般 Web Deploy 的需求。</span><span class="sxs-lookup"><span data-stu-id="2efa0-221">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="2efa0-222">為了讓您的網站提供內容，應用程式集區識別必須具有儲存內容之本機資料夾的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="2efa0-222">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="2efa0-223">在 IIS 7.5 中，應用程式集區預設會以唯一的應用程式集區身分識別執行（相較于舊版的 IIS，應用程式集區通常會使用網路服務帳戶來執行）。</span><span class="sxs-lookup"><span data-stu-id="2efa0-223">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="2efa0-224">應用程式集區身分識別不是真正的使用者帳戶，也不會顯示在任何使用者或群組&#x2014;清單上，而是在啟動應用程式集區時動態建立的。</span><span class="sxs-lookup"><span data-stu-id="2efa0-224">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="2efa0-225">每個應用程式集區識別都會新增至本機**IIS\_給 iis-iusrs**安全性群組做為隱藏專案。</span><span class="sxs-lookup"><span data-stu-id="2efa0-225">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="2efa0-226">若要將許可權授與檔案或資料夾上的應用程式集區身分識別，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="2efa0-226">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="2efa0-227">使用 <strong>IIS AppPool\</strong ><em>[應用程式集區名稱]</em>（例如<strong>iis AppPool\DemoSite</strong>）的格式，直接將許可權指派給應用程式集區身分識別。</span><span class="sxs-lookup"><span data-stu-id="2efa0-227">Assign permissions to the application pool identity directly, using the format <strong>IIS AppPool\</strong><em>[application pool name]</em>(for example, <strong>IIS AppPool\DemoSite</strong>).</span></span>
- <span data-ttu-id="2efa0-228">指派許可權給**IIS\_給 iis-iusrs**群組。</span><span class="sxs-lookup"><span data-stu-id="2efa0-228">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="2efa0-229">最常見的方法是將許可權指派給本機**IIS\_給 iis-iusrs**群組，因為這種方法可讓您變更應用程式集區，而不需要重新設定檔案系統許可權。</span><span class="sxs-lookup"><span data-stu-id="2efa0-229">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="2efa0-230">下一個程式會使用這個以群組為基礎的方法。</span><span class="sxs-lookup"><span data-stu-id="2efa0-230">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="2efa0-231">如需 IIS 7.5 中應用程式集區身分識別的詳細資訊，請參閱[應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。</span><span class="sxs-lookup"><span data-stu-id="2efa0-231">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="2efa0-232">**設定 IIS 網站的資料夾許可權**</span><span class="sxs-lookup"><span data-stu-id="2efa0-232">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="2efa0-233">在 Windows Explorer 中，流覽至本機資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="2efa0-233">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="2efa0-234">以滑鼠右鍵按一下該資料夾，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-234">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="2efa0-235">在 [**安全性**] 索引標籤上，按一下 [**編輯**]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-235">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="2efa0-236">按一下 [**位置**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-236">Click **Locations**.</span></span> <span data-ttu-id="2efa0-237">在 [**位置**] 對話方塊中，選取本機伺服器，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2efa0-237">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image8.png)
5. <span data-ttu-id="2efa0-238">在 [**選取使用者或群組**] 對話方塊中，輸入**IIS\_給 iis-iusrs**，按一下 [**檢查名稱**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2efa0-238">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="2efa0-239">在<em>[資料夾名稱] 的 [</em> <strong>許可權</strong>] 對話方塊中，請注意，預設會將 [<strong>讀取 &amp; 執行</strong>]、[<strong>列出資料夾內容</strong>] 和 [<strong>讀取</strong>] 許可權指派給新的群組。</span><span class="sxs-lookup"><span data-stu-id="2efa0-239">In the <strong>Permissions for</strong><em>[folder name]</em> dialog box, notice that the new group has been assigned the <strong>Read &amp; execute</strong>, <strong>List folder contents</strong>, and <strong>Read</strong> permissions by default.</span></span> <span data-ttu-id="2efa0-240">保持不變，然後按一下<strong>[確定]</strong>。</span><span class="sxs-lookup"><span data-stu-id="2efa0-240">Leave this unchanged and click <strong>OK</strong>.</span></span>
7. <span data-ttu-id="2efa0-241">按一下 [<strong>確定</strong>] 以關閉<em>[資料夾名稱]</em><strong>屬性</strong>對話方塊。</span><span class="sxs-lookup"><span data-stu-id="2efa0-241">Click <strong>OK</strong> to close the <em>[folder name]</em><strong>Properties</strong> dialog box.</span></span>

## <a name="disable-the-remote-agent-service"></a><span data-ttu-id="2efa0-242">停用遠端代理程式服務</span><span class="sxs-lookup"><span data-stu-id="2efa0-242">Disable the Remote Agent Service</span></span>

<span data-ttu-id="2efa0-243">當您安裝 Web Deploy 時，會自動安裝及啟動 Web Deployment Agent 服務。</span><span class="sxs-lookup"><span data-stu-id="2efa0-243">When you install Web Deploy, the Web Deployment Agent Service is installed and started automatically.</span></span> <span data-ttu-id="2efa0-244">此服務可讓您從遠端位置部署和發佈 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="2efa0-244">This service allows you to deploy and publish web packages from a remote location.</span></span> <span data-ttu-id="2efa0-245">在此案例中，您將不會使用遠端部署功能，因此您應該停止並停用服務。</span><span class="sxs-lookup"><span data-stu-id="2efa0-245">You won't be using the remote deployment capability in this scenario, so you should stop and disable the service.</span></span>

> [!NOTE]
> <span data-ttu-id="2efa0-246">您不需要停止遠端代理程式服務，就可以手動匯入和部署 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="2efa0-246">You don't need to stop the remote agent service in order to import and deploy a web package manually.</span></span> <span data-ttu-id="2efa0-247">不過，如果您不打算使用服務，最好是停止並停用它。</span><span class="sxs-lookup"><span data-stu-id="2efa0-247">However, it's a good practice to stop and disable the service if you don't plan to use it.</span></span>

<span data-ttu-id="2efa0-248">您可以使用各種命令列公用程式或 Windows PowerShell Cmdlet，以多種方式停止及停用服務。</span><span class="sxs-lookup"><span data-stu-id="2efa0-248">You can stop and disable a service in multiple ways, using various command-line utilities or Windows PowerShell cmdlets.</span></span> <span data-ttu-id="2efa0-249">此程式描述以 UI 為基礎的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="2efa0-249">This procedure describes a straightforward UI-based approach.</span></span>

<span data-ttu-id="2efa0-250">**停止和停用遠端代理程式服務**</span><span class="sxs-lookup"><span data-stu-id="2efa0-250">**To stop and disable the remote agent service**</span></span>

1. <span data-ttu-id="2efa0-251">在 [開始] 功能表上，指向 [系統管理工具]，然後按一下 [服務]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-251">On the **Start** menu, point to **Administrative Tools**, and then click **Services**.</span></span>
2. <span data-ttu-id="2efa0-252">在 [服務] 主控台中，找出 [ **Web Deployment Agent 服務**] 資料列。</span><span class="sxs-lookup"><span data-stu-id="2efa0-252">In the Services console, locate the **Web Deployment Agent Service** row.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image9.png)
3. <span data-ttu-id="2efa0-253">以滑鼠右鍵按一下 [ **Web Deployment Agent 服務**]，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-253">Right-click **Web Deployment Agent Service**, and then click **Properties**.</span></span>
4. <span data-ttu-id="2efa0-254">在 [ **Web Deployment Agent 服務屬性**] 對話方塊中，按一下 [**停止**]。</span><span class="sxs-lookup"><span data-stu-id="2efa0-254">In the **Web Deployment Agent Service Properties** dialog box, click **Stop**.</span></span>
5. <span data-ttu-id="2efa0-255">在 [**啟動類型**] 清單中，選取 [**停用**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="2efa0-255">In the **Startup type** list, select **Disabled**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-offline-deployment/_static/image10.png)

## <a name="conclusion"></a><span data-ttu-id="2efa0-256">結論</span><span class="sxs-lookup"><span data-stu-id="2efa0-256">Conclusion</span></span>

<span data-ttu-id="2efa0-257">此時，您的 web 伺服器已準備好進行離線 web 套件部署。</span><span class="sxs-lookup"><span data-stu-id="2efa0-257">At this point, your web server is ready for offline web package deployment.</span></span> <span data-ttu-id="2efa0-258">嘗試將 web 封裝匯入 IIS 網站之前，您可能會想要檢查下列重點：</span><span class="sxs-lookup"><span data-stu-id="2efa0-258">Before you attempt to import web packages to an IIS website, you may want to check these key points:</span></span>

- <span data-ttu-id="2efa0-259">您是否已向 IIS 註冊 ASP.NET 4.0？</span><span class="sxs-lookup"><span data-stu-id="2efa0-259">Have you registered ASP.NET 4.0 with IIS?</span></span>
- <span data-ttu-id="2efa0-260">應用程式集區身分識別對您網站的源資料夾具有讀取權限嗎？</span><span class="sxs-lookup"><span data-stu-id="2efa0-260">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="2efa0-261">您已停止 Web Deployment Agent 服務嗎？</span><span class="sxs-lookup"><span data-stu-id="2efa0-261">Have you stopped the Web Deployment Agent Service?</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="2efa0-262">[上一頁](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
> [下一頁](configuring-a-database-server-for-web-deploy-publishing.md)</span><span class="sxs-lookup"><span data-stu-id="2efa0-262">[Previous](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
[Next](configuring-a-database-server-for-web-deploy-publishing.md)</span></span>
