---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
title: 設定用於 Web Deploy 發行的 Web 服務器（Web Deploy 處理常式） |Microsoft Docs
author: jrjlee
description: 本主題描述如何設定 Internet Information Services （IIS）網頁伺服器，以支援使用 IIS Web Deploy 漢字的 web 發行和部署 。
ms.author: riande
ms.date: 01/29/2017
ms.assetid: 90ebf911-1c46-4470-b876-1335bd0f590f
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler
msc.type: authoredcontent
ms.openlocfilehash: baaebd32f08d3c6b861572c5c5a16ec0fb70aaf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78568562"
---
# <a name="configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler"></a><span data-ttu-id="9f16a-103">設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)</span><span class="sxs-lookup"><span data-stu-id="9f16a-103">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>

[<span data-ttu-id="9f16a-104">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="9f16a-104">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="9f16a-105">本主題描述如何使用 IIS Web Deploy 處理常式，設定 Internet Information Services （IIS）網頁伺服器，以支援 web 發行和部署。</span><span class="sxs-lookup"><span data-stu-id="9f16a-105">This topic describes how to configure an Internet Information Services (IIS) web server to support web publishing and deployment using the IIS Web Deploy Handler.</span></span>
> 
> <span data-ttu-id="9f16a-106">當您使用 Web Deploy 2.0 或更新版本時，有三種主要方法可用來將您的應用程式或網站放在 Web 服務器上。</span><span class="sxs-lookup"><span data-stu-id="9f16a-106">When you work with Web Deploy 2.0 or later, there are three main approaches you can use to get your applications or sites onto a web server.</span></span> <span data-ttu-id="9f16a-107">您可以：</span><span class="sxs-lookup"><span data-stu-id="9f16a-107">You can:</span></span>
> 
> - <span data-ttu-id="9f16a-108">使用*Web Deploy 的遠端代理程式服務*。</span><span class="sxs-lookup"><span data-stu-id="9f16a-108">Use the *Web Deploy Remote Agent Service*.</span></span> <span data-ttu-id="9f16a-109">這種方法需要較少的 web 伺服器設定，但您必須提供本機伺服器系統管理員的認證，才能將任何專案部署至伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f16a-109">This approach requires less configuration of the web server, but you need to provide the credentials of a local server administrator in order to deploy anything to the server.</span></span>
> - <span data-ttu-id="9f16a-110">使用*Web Deploy 處理常式*。</span><span class="sxs-lookup"><span data-stu-id="9f16a-110">Use the *Web Deploy Handler*.</span></span> <span data-ttu-id="9f16a-111">這種方法比較複雜，而且需要更多的初始工作來設定 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f16a-111">This approach is a lot more complex and requires more initial effort to set up the web server.</span></span> <span data-ttu-id="9f16a-112">不過，當您使用這種方法時，可以設定 IIS 以允許非系統管理員使用者執行部署。</span><span class="sxs-lookup"><span data-stu-id="9f16a-112">However, when you use this approach, you can configure IIS to allow non-administrator users to perform the deployment.</span></span> <span data-ttu-id="9f16a-113">Web Deploy 處理常式僅適用于 IIS 7 版或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9f16a-113">The Web Deploy Handler is only available in IIS version 7 or later.</span></span>
> - <span data-ttu-id="9f16a-114">使用*離線部署*。</span><span class="sxs-lookup"><span data-stu-id="9f16a-114">Use *offline deployment*.</span></span> <span data-ttu-id="9f16a-115">此方法需要最少的 web 伺服器設定，但伺服器管理員必須手動將 web 套件複製到伺服器，並透過 IIS 管理員將其匯入。</span><span class="sxs-lookup"><span data-stu-id="9f16a-115">This approach requires the least configuration of the web server, but a server administrator must manually copy the web package onto the server and import it through IIS Manager.</span></span>
> 
> <span data-ttu-id="9f16a-116">如需這些方法的主要功能、優點和缺點的詳細資訊，請參閱[選擇正確的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-116">For more information on the key features, advantages, and disadvantages of these approaches, see [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md).</span></span>

<span data-ttu-id="9f16a-117">是，如果您想要允許非系統管理員的使用者將內容部署到特定的 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="9f16a-117">Yes, if you want to allow non-administrator users to deploy content to specific IIS websites.</span></span> <span data-ttu-id="9f16a-118">這種方法通常適用于下列類型的案例：</span><span class="sxs-lookup"><span data-stu-id="9f16a-118">This approach is often desirable in these types of scenarios:</span></span>

- <span data-ttu-id="9f16a-119">臨時或生產環境，其中觸發遠端部署的人員或服務帳戶不太可能能夠存取伺服器管理員的認證。</span><span class="sxs-lookup"><span data-stu-id="9f16a-119">Staging or production environments, where the person or service account that triggers the remote deployment is unlikely to have access to the credentials of a server administrator.</span></span>
- <span data-ttu-id="9f16a-120">裝載的環境，您想要讓遠端使用者能夠更新其網站，而不需讓他們完全控制您的 web 伺服器（或存取其他人的網站）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-120">Hosted environments, where you want to give remote users the ability to update their websites without giving them full control of your web servers (or access to anyone else's websites).</span></span>

<span data-ttu-id="9f16a-121">在開發或測試案例中，或小型組織中，使用伺服器管理員認證來部署內容通常較不爭議。</span><span class="sxs-lookup"><span data-stu-id="9f16a-121">In development or test scenarios, or in smaller organizations, deploying content using server administrator credentials is often less contentious.</span></span> <span data-ttu-id="9f16a-122">在這些情況下，使用[Web Deploy 遠端代理程式服務](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)來設定您的 web 伺服器以支援部署，會提供更直接的方法。</span><span class="sxs-lookup"><span data-stu-id="9f16a-122">In these scenarios, configuring your web servers to support deployment using the [Web Deploy Remote Agent Service](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md) offers a more straightforward approach.</span></span>

## <a name="task-overview"></a><span data-ttu-id="9f16a-123">工作總覽</span><span class="sxs-lookup"><span data-stu-id="9f16a-123">Task Overview</span></span>

<span data-ttu-id="9f16a-124">若要使用 Web Deploy 處理常式方法，將 web 伺服器設定為接受及部署遠端電腦上的網頁封裝，您必須：</span><span class="sxs-lookup"><span data-stu-id="9f16a-124">To configure the web server to accept and deploy web packages from a remote computer using the Web Deploy Handler approach, you'll need to:</span></span>

- <span data-ttu-id="9f16a-125">建立或選擇要用來執行部署之認證的網域使用者帳戶（「非系統管理員使用者」）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-125">Create, or choose, a domain user account (the "non-administrator user") whose credentials you'll use to perform deployments.</span></span>
- <span data-ttu-id="9f16a-126">安裝 IIS 7.5，包括 Web 管理服務和基本驗證模組。</span><span class="sxs-lookup"><span data-stu-id="9f16a-126">Install IIS 7.5, including the Web Management Service and the Basic Authentication module.</span></span>
- <span data-ttu-id="9f16a-127">安裝 Web Deploy 2.1 或更新版本。</span><span class="sxs-lookup"><span data-stu-id="9f16a-127">Install Web Deploy 2.1 or later.</span></span>
- <span data-ttu-id="9f16a-128">設定 Web 管理服務以允許遠端連線，並啟動服務。</span><span class="sxs-lookup"><span data-stu-id="9f16a-128">Configure the Web Management Service to allow remote connections, and start the service.</span></span>
- <span data-ttu-id="9f16a-129">建立 IIS 網站來裝載已部署的內容。</span><span class="sxs-lookup"><span data-stu-id="9f16a-129">Create an IIS website to host the deployed content.</span></span>
- <span data-ttu-id="9f16a-130">在 IIS 管理員中，為您的網站授與非系統管理員的使用者許可權。</span><span class="sxs-lookup"><span data-stu-id="9f16a-130">Grant your non-administrator user permissions on your website in IIS Manager.</span></span>
- <span data-ttu-id="9f16a-131">請確定 Web 管理服務委派規則允許服務使用您的非系統管理員使用者帳戶新增和變更網站內容。</span><span class="sxs-lookup"><span data-stu-id="9f16a-131">Ensure that the Web Management Service delegation rules permit the service to add and change website content using your non-administrator user account.</span></span>
- <span data-ttu-id="9f16a-132">設定任何防火牆以允許埠8172上的連入連線。</span><span class="sxs-lookup"><span data-stu-id="9f16a-132">Configure any firewalls to allow incoming connections on port 8172.</span></span>

<span data-ttu-id="9f16a-133">若要特別裝載 ContactManager 範例解決方案，您也需要：</span><span class="sxs-lookup"><span data-stu-id="9f16a-133">To host the ContactManager sample solution specifically, you'll also need to:</span></span>

- <span data-ttu-id="9f16a-134">安裝 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="9f16a-134">Install the .NET Framework 4.0.</span></span>
- <span data-ttu-id="9f16a-135">安裝 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="9f16a-135">Install ASP.NET MVC 3.</span></span>

<span data-ttu-id="9f16a-136">本主題將說明如何執行上述每個程式。</span><span class="sxs-lookup"><span data-stu-id="9f16a-136">This topic will show you how to perform each of these procedures.</span></span> <span data-ttu-id="9f16a-137">本主題中的工作和逐步解說假設您是從執行 Windows Server 2016 的全新伺服器組建開始。</span><span class="sxs-lookup"><span data-stu-id="9f16a-137">The tasks and walkthroughs in this topic assume that you're starting with a clean server build running Windows Server 2016.</span></span> <span data-ttu-id="9f16a-138">在繼續之前，請確定：</span><span class="sxs-lookup"><span data-stu-id="9f16a-138">Before you continue, ensure that:</span></span>

- <span data-ttu-id="9f16a-139">Windows Server 2016</span><span class="sxs-lookup"><span data-stu-id="9f16a-139">Windows Server 2016</span></span>
- <span data-ttu-id="9f16a-140">伺服器已加入網域。</span><span class="sxs-lookup"><span data-stu-id="9f16a-140">The server is domain-joined.</span></span>
- <span data-ttu-id="9f16a-141">伺服器具有靜態 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="9f16a-141">The server has a static IP address.</span></span>

> [!NOTE]
> <span data-ttu-id="9f16a-142">如需將電腦加入網域的詳細資訊，請參閱[將電腦加入網域並登](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx)入。</span><span class="sxs-lookup"><span data-stu-id="9f16a-142">For more information on joining computers to a domain, see [Joining Computers to the Domain and Logging On](https://technet.microsoft.com/library/cc725618(v=WS.10).aspx).</span></span> <span data-ttu-id="9f16a-143">如需設定靜態 IP 位址的詳細資訊，請參閱[設定靜態 Ip 位址](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-143">For more information on configuring static IP addresses, see [Configure a Static IP Address](https://technet.microsoft.com/library/cc754203(v=ws.10).aspx).</span></span>

## <a name="install-products-and-components"></a><span data-ttu-id="9f16a-144">安裝產品和元件</span><span class="sxs-lookup"><span data-stu-id="9f16a-144">Install Products and Components</span></span>

<span data-ttu-id="9f16a-145">本節將引導您在 web 伺服器上安裝必要的產品和元件。</span><span class="sxs-lookup"><span data-stu-id="9f16a-145">This section will guide you through installing the required products and components on the web server.</span></span> <span data-ttu-id="9f16a-146">在開始之前，最好先執行 Windows Update，以確保您的伺服器完全保持在最新狀態。</span><span class="sxs-lookup"><span data-stu-id="9f16a-146">Before you begin, a good practice is to run Windows Update to ensure that your server is fully up to date.</span></span>

<span data-ttu-id="9f16a-147">在此情況下，您需要安裝下列專案：</span><span class="sxs-lookup"><span data-stu-id="9f16a-147">In this case, you need to install these things:</span></span>

- <span data-ttu-id="9f16a-148">**IIS 7 建議**的設定。</span><span class="sxs-lookup"><span data-stu-id="9f16a-148">**IIS 7 Recommended Configuration**.</span></span> <span data-ttu-id="9f16a-149">這會啟用 web 伺服器上的**網頁伺服器（iis）** 角色，並安裝您需要的一組 IIS 模組和元件，才能裝載 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="9f16a-149">This enables the **Web Server (IIS)** role on your web server and installs the set of IIS modules and components that you need in order to host an ASP.NET application.</span></span>
- <span data-ttu-id="9f16a-150">**IIS：管理服務**。</span><span class="sxs-lookup"><span data-stu-id="9f16a-150">**IIS: Management Service**.</span></span> <span data-ttu-id="9f16a-151">這會在 IIS 中安裝 Web 管理服務（WMSvc）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-151">This installs the Web Management Service (WMSvc) in IIS.</span></span> <span data-ttu-id="9f16a-152">這項服務可讓您遠端系統管理 IIS 網站，並將 Web Deploy 處理常式端點公開給用戶端。</span><span class="sxs-lookup"><span data-stu-id="9f16a-152">This service enables remote management of IIS websites and exposes the Web Deploy Handler endpoint to clients.</span></span>
- <span data-ttu-id="9f16a-153">**IIS：基本驗證**。</span><span class="sxs-lookup"><span data-stu-id="9f16a-153">**IIS: Basic Authentication**.</span></span> <span data-ttu-id="9f16a-154">這會安裝 IIS 基本驗證模組。</span><span class="sxs-lookup"><span data-stu-id="9f16a-154">This installs the IIS Basic Authentication module.</span></span> <span data-ttu-id="9f16a-155">這可讓 Web 管理服務（WMSvc）驗證您所提供的認證。</span><span class="sxs-lookup"><span data-stu-id="9f16a-155">This lets the Web Management Service (WMSvc) authenticate the credentials you provide.</span></span>
- <span data-ttu-id="9f16a-156">**Web Deployment Tool 2.1 或更新版本**。</span><span class="sxs-lookup"><span data-stu-id="9f16a-156">**Web Deployment Tool 2.1 or later**.</span></span> <span data-ttu-id="9f16a-157">這會在您的伺服器上安裝 Web Deploy （及其基礎可執行檔，Msdeploy.exe）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-157">This installs Web Deploy (and its underlying executable, MSDeploy.exe) on your server.</span></span> <span data-ttu-id="9f16a-158">在此過程中，它會安裝 Web Deploy 處理常式，並將它與 Web 管理服務整合。</span><span class="sxs-lookup"><span data-stu-id="9f16a-158">As part of this process, it installs the Web Deploy Handler and integrates it with the Web Management Service.</span></span>
- <span data-ttu-id="9f16a-159">**.NET Framework 4.0**。</span><span class="sxs-lookup"><span data-stu-id="9f16a-159">**.NET Framework 4.0**.</span></span> <span data-ttu-id="9f16a-160">這是執行此版本 .NET Framework 所建立之應用程式的必要項。</span><span class="sxs-lookup"><span data-stu-id="9f16a-160">This is required to run applications that were built on this version of the .NET Framework.</span></span>
- <span data-ttu-id="9f16a-161">**ASP.NET MVC 3**。</span><span class="sxs-lookup"><span data-stu-id="9f16a-161">**ASP.NET MVC 3**.</span></span> <span data-ttu-id="9f16a-162">這會安裝執行 MVC 3 應用程式所需的元件。</span><span class="sxs-lookup"><span data-stu-id="9f16a-162">This installs the assemblies you need to run MVC 3 applications.</span></span>

> [!NOTE]
> <span data-ttu-id="9f16a-163">本逐步解說說明如何使用 Web Platform Installer 來安裝和設定各種元件。</span><span class="sxs-lookup"><span data-stu-id="9f16a-163">This walkthrough describes the use of the Web Platform Installer to install and configure various components.</span></span> <span data-ttu-id="9f16a-164">雖然您不需要使用 Web Platform Installer，但它會自動偵測相依性，並確保您一律取得最新的產品版本，藉此簡化安裝程式。</span><span class="sxs-lookup"><span data-stu-id="9f16a-164">Although you don't have to use the Web Platform Installer, it simplifies the installation process by automatically detecting dependencies and ensuring that you always get the latest product versions.</span></span> <span data-ttu-id="9f16a-165">如需詳細資訊，請參閱[Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-165">For more information, see [Microsoft Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>

<span data-ttu-id="9f16a-166">**若要安裝必要的產品和元件**</span><span class="sxs-lookup"><span data-stu-id="9f16a-166">**To install the required products and components**</span></span>

1. <span data-ttu-id="9f16a-167">下載並安裝[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-167">Download and install the [Web Platform Installer](https://go.microsoft.com/?linkid=9805118).</span></span>
2. <span data-ttu-id="9f16a-168">安裝完成時，Web Platform Installer 會自動啟動。</span><span class="sxs-lookup"><span data-stu-id="9f16a-168">When installation is complete, the Web Platform Installer will launch automatically.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9f16a-169">您現在可以隨時從 [**開始**] 功能表啟動 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="9f16a-169">You can now launch the Web Platform Installer at any time from the **Start** menu.</span></span> <span data-ttu-id="9f16a-170">若要這樣做，請在 [**開始**] 功能表上，按一下 [**所有程式**]，然後按一下 [ **Microsoft Web Platform Installer**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-170">To do this, on the **Start** menu, click **All Programs**, and then click **Microsoft Web Platform Installer**.</span></span>
3. <span data-ttu-id="9f16a-171">在 [Web Platform Installer] 視窗的頂端，按一下 [產品]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-171">At the top of the **Web Platform Installer** window, click **Products**.</span></span>
4. <span data-ttu-id="9f16a-172">在視窗左側的流覽窗格中 **，按一下 [** 架構]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-172">On the left side of the window, in the navigation pane, click **Frameworks**.</span></span>
5. <span data-ttu-id="9f16a-173">在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-173">In the **Microsoft .NET Framework 4** row, if the .NET Framework is not already installed, click **Add**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9f16a-174">您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="9f16a-174">You may have already installed the .NET Framework 4.0 through Windows Update.</span></span> <span data-ttu-id="9f16a-175">如果已安裝產品或元件，Web Platform Installer 會以**已安裝**的文字取代 [**新增**] 按鈕來指出這一點。</span><span class="sxs-lookup"><span data-stu-id="9f16a-175">If a product or component is already installed, the Web Platform Installer will indicate this by replacing the **Add** button with the text **Installed**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image1.png)
6. <span data-ttu-id="9f16a-176">在 [ **ASP.NET MVC 3 （Visual Studio 2010）** ] 資料列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-176">In the **ASP.NET MVC 3 (Visual Studio 2010)** row, click **Add**.</span></span>
7. <span data-ttu-id="9f16a-177">在流覽窗格中，按一下 [**伺服器**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-177">In the navigation pane, click **Server**.</span></span>
8. <span data-ttu-id="9f16a-178">在 [ **IIS 7 建議**的設定] 列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-178">In the **IIS 7 Recommended Configuration** row, click **Add**.</span></span>
9. <span data-ttu-id="9f16a-179">在 [ **Web Deployment Tool 2.1** ] 資料列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-179">In the **Web Deployment Tool 2.1** row, click **Add**.</span></span>
10. <span data-ttu-id="9f16a-180">在 [ **IIS：基本驗證**] 資料列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-180">In the **IIS: Basic Authentication** row, click **Add**.</span></span>
11. <span data-ttu-id="9f16a-181">在 [ **IIS：管理服務**] 資料列中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-181">In the **IIS: Management Service** row, click **Add**.</span></span>
12. <span data-ttu-id="9f16a-182">按一下 [安裝]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-182">Click **Install**.</span></span> <span data-ttu-id="9f16a-183">Web Platform Installer 將會顯示一份產品&#x2014;清單，其中包含&#x2014;要安裝的相關聯相依性，並會提示您接受授權條款。</span><span class="sxs-lookup"><span data-stu-id="9f16a-183">The Web Platform Installer will show you a list of products&#x2014;together with any associated dependencies&#x2014;to be installed and will prompt you to accept the license terms.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image2.png)
13. <span data-ttu-id="9f16a-184">請參閱授權條款，如果您同意這些條款，請按一下 [**我接受**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-184">Review the license terms, and if you consent to the terms, click **I Accept**.</span></span>
14. <span data-ttu-id="9f16a-185">當安裝完成時，按一下 **[完成**]，然後關閉 [ **Web Platform Installer** ] 視窗。</span><span class="sxs-lookup"><span data-stu-id="9f16a-185">When the installation is complete, click **Finish**, and then close the **Web Platform Installer** window.</span></span>

<span data-ttu-id="9f16a-186">如果您在安裝 IIS 之前安裝了 .NET Framework 4.0，就必須執行[ASP.NET IIS 註冊工具](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx)（aspnet\_regiis），以向 IIS 註冊最新版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="9f16a-186">If you installed the .NET Framework 4.0 before you installed IIS, you'll need to run the [ASP.NET IIS Registration Tool](https://msdn.microsoft.com/library/k6h9cz8h(v=VS.100).aspx) (aspnet\_regiis.exe) to register the latest version of ASP.NET with IIS.</span></span> <span data-ttu-id="9f16a-187">如果您不這麼做，就會發現 IIS 會提供靜態內容（例如 HTML 檔案），而不會有任何問題，但會傳回**HTTP 錯誤404.0 –** 當您嘗試流覽至 ASP.NET 內容時找不到。</span><span class="sxs-lookup"><span data-stu-id="9f16a-187">If you don't do this, you'll find that IIS will serve static content (like HTML files) without any problems, but it will return **HTTP Error 404.0 – Not Found** when you attempt to browse to ASP.NET content.</span></span> <span data-ttu-id="9f16a-188">您可以使用下一個程式來確保 ASP.NET 4.0 已註冊。</span><span class="sxs-lookup"><span data-stu-id="9f16a-188">You can use the next procedure to ensure that ASP.NET 4.0 is registered.</span></span>

<span data-ttu-id="9f16a-189">**向 IIS 註冊 ASP.NET 4。0**</span><span class="sxs-lookup"><span data-stu-id="9f16a-189">**To register ASP.NET 4.0 with IIS**</span></span>

1. <span data-ttu-id="9f16a-190">按一下 [**開始**]，然後輸入**命令提示**字元。</span><span class="sxs-lookup"><span data-stu-id="9f16a-190">Click **Start**, and then type **Command Prompt**.</span></span>
2. <span data-ttu-id="9f16a-191">在搜尋結果中，以滑鼠右鍵按一下 [**命令提示**字元]，然後按一下 [以**系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-191">In the search results, right-click **Command Prompt**, and then click **Run as administrator**.</span></span>
3. <span data-ttu-id="9f16a-192">在 [命令提示字元] 視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework\v4.0.30319**目錄。</span><span class="sxs-lookup"><span data-stu-id="9f16a-192">In the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework\v4.0.30319** directory.</span></span>
4. <span data-ttu-id="9f16a-193">輸入此命令，然後按 Enter 鍵：</span><span class="sxs-lookup"><span data-stu-id="9f16a-193">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample1.cmd)]
5. <span data-ttu-id="9f16a-194">如果您打算在任何時間點裝載64位的 web 應用程式，您也應該向 IIS 註冊64位版本的 ASP.NET。</span><span class="sxs-lookup"><span data-stu-id="9f16a-194">If you plan to host 64-bit web applications at any point, you should also register the 64-bit version of ASP.NET with IIS.</span></span> <span data-ttu-id="9f16a-195">若要這麼做，請在 [命令提示字元] 視窗中，流覽至 **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319**目錄。</span><span class="sxs-lookup"><span data-stu-id="9f16a-195">To do this, in the Command Prompt window, navigate to the **%WINDIR%\Microsoft.NET\Framework64\v4.0.30319** directory.</span></span>
6. <span data-ttu-id="9f16a-196">輸入此命令，然後按 Enter 鍵：</span><span class="sxs-lookup"><span data-stu-id="9f16a-196">Type this command, and then press Enter:</span></span>

    [!code-console[Main](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/samples/sample2.cmd)]

<span data-ttu-id="9f16a-197">建議的作法是，在此時再次使用 Windows Update，下載並安裝您已安裝之新產品和元件的任何可用更新。</span><span class="sxs-lookup"><span data-stu-id="9f16a-197">As a good practice, use Windows Update again at this point to download and install any available updates for the new products and components you've installed.</span></span>

## <a name="configure-the-web-management-service"></a><span data-ttu-id="9f16a-198">設定 Web 管理服務</span><span class="sxs-lookup"><span data-stu-id="9f16a-198">Configure the Web Management Service</span></span>

<span data-ttu-id="9f16a-199">既然您已安裝所需的所有專案，下一步就是在 IIS 中設定 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="9f16a-199">Now that you've installed everything you need, the next step is to configure the Web Management Service in IIS.</span></span> <span data-ttu-id="9f16a-200">概括而言，您必須完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="9f16a-200">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="9f16a-201">啟用伺服器層級的基本驗證。</span><span class="sxs-lookup"><span data-stu-id="9f16a-201">Enable basic authentication at the server level.</span></span>
- <span data-ttu-id="9f16a-202">設定 Web 管理服務以接受遠端連線。</span><span class="sxs-lookup"><span data-stu-id="9f16a-202">Configure the Web Management Service to accept remote connections.</span></span>
- <span data-ttu-id="9f16a-203">啟動 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="9f16a-203">Start the Web Management Service.</span></span>
- <span data-ttu-id="9f16a-204">檢查必要的 Web 管理服務委派規則是否已就緒。</span><span class="sxs-lookup"><span data-stu-id="9f16a-204">Check that the required Web Management Service delegation rules are in place.</span></span>

<span data-ttu-id="9f16a-205">**若要設定 Web 管理服務**</span><span class="sxs-lookup"><span data-stu-id="9f16a-205">**To configure the Web Management Service**</span></span>

1. <span data-ttu-id="9f16a-206">在 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [ **Internet Information Services （IIS）管理員**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-206">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
2. <span data-ttu-id="9f16a-207">在 **[IIS**管理員] 的 [連線] 窗格中，按一下伺服器節點（例如， **STAGEWEB1**）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-207">In IIS Manager, in the **Connections** pane, click the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image3.png)
3. <span data-ttu-id="9f16a-208">在中央窗格的 [ **IIS**] 底下，按兩下 [**驗證**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-208">In the center pane, under **IIS**, double-click **Authentication**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image20.png)
4. <span data-ttu-id="9f16a-209">以滑鼠右鍵按一下 [**基本驗證**]，然後按一下 [**啟用**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-209">Right-click **Basic Authentication**, and then click **Enable**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image5.png)
5. <span data-ttu-id="9f16a-210">**在 [連線] 窗格**中，再次按一下伺服器節點以返回最上層設定。</span><span class="sxs-lookup"><span data-stu-id="9f16a-210">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
6. <span data-ttu-id="9f16a-211">在中央窗格的 [**管理**] 底下，按兩下 [**管理服務**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-211">In the center pane, under **Management**, double-click **Management Service**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image6.png)
7. <span data-ttu-id="9f16a-212">在中央窗格中，選取 [**啟用遠端連線**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-212">In the center pane, select **Enable remote connections**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9f16a-213">如果 Web 管理服務已在執行中，您必須先將它停止。</span><span class="sxs-lookup"><span data-stu-id="9f16a-213">If the Web Management Service is already running, you'll need to stop it first.</span></span>
8. <span data-ttu-id="9f16a-214">在 [**動作**] 窗格中，按一下 [**啟動**] 以啟動 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="9f16a-214">In the **Actions** pane, click **Start** to start the Web Management Service.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image7.png)
9. <span data-ttu-id="9f16a-215">如果系統提示您儲存設定，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="9f16a-215">If you're prompted to save your settings, click **Yes**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="9f16a-216">您可能也會想要將服務設定為自動啟動。</span><span class="sxs-lookup"><span data-stu-id="9f16a-216">You may also want to configure the service to start automatically.</span></span> <span data-ttu-id="9f16a-217">若要這麼做，請開啟 [服務] 主控台，以滑鼠右鍵按一下 [ **Web 管理服務**]，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-217">To do this, open the Services console, right-click **Web Management Service**, and then click **Properties**.</span></span> <span data-ttu-id="9f16a-218">在 [**啟動類型**] 下拉式清單中，選取 [**自動**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9f16a-218">In the **Startup type** dropdown list, select **Automatic**, and then click **OK**.</span></span>
10. <span data-ttu-id="9f16a-219">**在 [連線] 窗格**中，再次按一下伺服器節點以返回最上層設定。</span><span class="sxs-lookup"><span data-stu-id="9f16a-219">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>
11. <span data-ttu-id="9f16a-220">在中央窗格的 [**管理**] 底下，按兩下 [**管理服務委派**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-220">In the center pane, under **Management**, double-click **Management Service Delegation**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image8.png)
12. <span data-ttu-id="9f16a-221">確認中央窗格包含一組規則。</span><span class="sxs-lookup"><span data-stu-id="9f16a-221">Verify that the center pane contains a set of rules.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image9.png)

    <span data-ttu-id="9f16a-222">這些規則可讓授權的 Web 管理服務使用者使用各種 Web Deploy 提供者。</span><span class="sxs-lookup"><span data-stu-id="9f16a-222">These rules allow authorized Web Management Service users to use various Web Deploy providers.</span></span> <span data-ttu-id="9f16a-223">例如，若要透過 Web Deploy 處理常式將 web 應用程式和內容部署至 IIS，則必須有委派規則，允許所有已驗證的 Web 管理服務使用者使用**contentPath**和**iisApp**提供者（您可以在螢幕擷取畫面中看到的最後一個規則）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-223">For example, to deploy web applications and content to IIS through the Web Deploy Handler, there must be a delegation rule that allows all authenticated Web Management Service users to use the **contentPath** and **iisApp** providers (the last rule that you can see in the screenshot).</span></span>

    <span data-ttu-id="9f16a-224">如果您已依照本主題所述的順序安裝產品和元件，最新版本的 Web Deploy 應該會自動將所有必要的委派規則新增至 Web 管理服務。</span><span class="sxs-lookup"><span data-stu-id="9f16a-224">If you installed products and components in the order described in this topic, the latest version of Web Deploy should automatically add all the required delegation rules to the Web Management Service.</span></span> <span data-ttu-id="9f16a-225">如果 [管理服務委派] 頁面未顯示任何規則，您就必須自行建立。</span><span class="sxs-lookup"><span data-stu-id="9f16a-225">If the Management Service Delegation page does not show any rules, you'll need to create them yourself.</span></span> <span data-ttu-id="9f16a-226">如需如何執行此操作的指示，請參閱[設定 Web 部署處理常式](https://go.microsoft.com/?linkid=9805124)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-226">For instructions on how to do this, see [Configure the Web Deployment Handler](https://go.microsoft.com/?linkid=9805124).</span></span>
13. <span data-ttu-id="9f16a-227">**在 [連線] 窗格**中，再次按一下伺服器節點以返回最上層設定。</span><span class="sxs-lookup"><span data-stu-id="9f16a-227">In the **Connections** pane, click the server node again to return to the top-level settings.</span></span>

## <a name="create-and-configure-an-iis-website"></a><span data-ttu-id="9f16a-228">建立和設定 IIS 網站</span><span class="sxs-lookup"><span data-stu-id="9f16a-228">Create and Configure an IIS Website</span></span>

<span data-ttu-id="9f16a-229">您必須先建立並設定 IIS 網站來裝載內容，才能將 web 內容部署到您的伺服器。</span><span class="sxs-lookup"><span data-stu-id="9f16a-229">Before you can deploy web content to your server, you need to create and configure an IIS website to host the content.</span></span> <span data-ttu-id="9f16a-230">Web Deploy 只能將 web 套件部署到現有的 IIS 網站;它無法為您建立網站。</span><span class="sxs-lookup"><span data-stu-id="9f16a-230">Web Deploy can only deploy web packages to an existing IIS website; it can't create the website for you.</span></span> <span data-ttu-id="9f16a-231">您也需要執行一些額外的設定，以允許您的非系統管理員帳戶從遠端部署內容。</span><span class="sxs-lookup"><span data-stu-id="9f16a-231">You also need to do a little extra configuration to allow your non-administrator account to deploy content remotely.</span></span> <span data-ttu-id="9f16a-232">概括而言，您必須完成下列工作：</span><span class="sxs-lookup"><span data-stu-id="9f16a-232">At a high level, you'll need to complete these tasks:</span></span>

- <span data-ttu-id="9f16a-233">在檔案系統上建立資料夾，以裝載您的內容。</span><span class="sxs-lookup"><span data-stu-id="9f16a-233">Create a folder on the file system to host your content.</span></span>
- <span data-ttu-id="9f16a-234">建立 IIS 網站來提供內容，並將它與本機資料夾產生關聯。</span><span class="sxs-lookup"><span data-stu-id="9f16a-234">Create an IIS website to serve the content, and associate it with the local folder.</span></span>
- <span data-ttu-id="9f16a-235">授與讀取權限給本機資料夾上的應用程式集區身分識別。</span><span class="sxs-lookup"><span data-stu-id="9f16a-235">Grant read permissions to the application pool identity on the local folder.</span></span>
- <span data-ttu-id="9f16a-236">將部署 web 應用程式所需的 IIS 許可權授與網域帳戶。</span><span class="sxs-lookup"><span data-stu-id="9f16a-236">Grant the necessary IIS permissions to the domain account that will deploy your web application.</span></span>

<span data-ttu-id="9f16a-237">雖然沒有任何動作會阻止您將內容部署到 IIS 中的預設網站，但不建議針對測試或示範案例以外的任何專案使用此方法。</span><span class="sxs-lookup"><span data-stu-id="9f16a-237">Although there's nothing stopping you from deploying content to the default website in IIS, this approach is not recommended for anything other than test or demonstration scenarios.</span></span> <span data-ttu-id="9f16a-238">若要模擬生產環境，您應該使用特定于應用程式需求的設定來建立新的 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="9f16a-238">To simulate a production environment, you should create a new IIS website with settings that are specific to the requirements of your application.</span></span>

<span data-ttu-id="9f16a-239">**若要建立 IIS 網站**</span><span class="sxs-lookup"><span data-stu-id="9f16a-239">**To create an IIS website**</span></span>

1. <span data-ttu-id="9f16a-240">在本機檔案系統上，建立用來儲存內容的資料夾（例如， **C:\DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-240">On the local file system, create a folder to store your content (for example, **C:\DemoSite**).</span></span>
2. <span data-ttu-id="9f16a-241">在 [**開始**] 功能表上，指向 [系統**管理工具**]，然後按一下 [ **Internet Information Services （IIS）管理員**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-241">On the **Start** menu, point to **Administrative Tools**, and then click **Internet Information Services (IIS) Manager**.</span></span>
3. <span data-ttu-id="9f16a-242">在 **[IIS**管理員] 的 [連線] 窗格中，展開伺服器節點（例如， **STAGEWEB1**）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-242">In IIS Manager, in the **Connections** pane, expand the server node (for example, **STAGEWEB1**).</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image10.png)
4. <span data-ttu-id="9f16a-243">以滑鼠右鍵按一下 [**網站**] 節點，然後按一下 [**新增**網站]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-243">Right-click the **Sites** node, and then click **Add Web Site**.</span></span>
5. <span data-ttu-id="9f16a-244">在 [**網站名稱**] 方塊中，輸入 IIS 網站的名稱（例如， **DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-244">In the **Site name** box, type a name for the IIS website (for example, **DemoSite**).</span></span>
6. <span data-ttu-id="9f16a-245">在 [**實體路徑**] 方塊中，輸入（或流覽至）本機資料夾的路徑（例如， **C:\DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-245">In the **Physical path** box, type (or browse to) the path to your local folder (for example, **C:\DemoSite**).</span></span>
7. <span data-ttu-id="9f16a-246">在 [**埠**] 方塊中，輸入您要用來裝載網站的埠號碼（例如， **85**）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-246">In the **Port** box, type the port number on which you want to host the website (for example, **85**).</span></span>

    > [!NOTE]
    > <span data-ttu-id="9f16a-247">適用于 HTTP 的標準埠號碼為80，HTTPS 則為443。</span><span class="sxs-lookup"><span data-stu-id="9f16a-247">The standard port numbers are 80 for HTTP and 443 for HTTPS.</span></span> <span data-ttu-id="9f16a-248">不過，如果您在埠80上裝載此網站，則必須先停止預設網站，才能存取您的網站。</span><span class="sxs-lookup"><span data-stu-id="9f16a-248">However, if you host this website on port 80, you'll need to stop the default website before you can access your site.</span></span>
8. <span data-ttu-id="9f16a-249">除非您要設定網站的網域名稱系統（DNS）記錄，否則請將 [**主機名稱**] 方塊保留空白，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9f16a-249">Leave the **Host name** box blank, unless you want to configure a Domain Name System (DNS) record for the website, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image11.png)

    > [!NOTE]
    > <span data-ttu-id="9f16a-250">在生產環境中，您可能會想要在埠80上裝載您的網站，並設定主機標頭和相符的 DNS 記錄。</span><span class="sxs-lookup"><span data-stu-id="9f16a-250">In a production environment, you'll likely want to host your website on port 80 and configure a host header, together with matching DNS records.</span></span> <span data-ttu-id="9f16a-251">如需在 IIS 7 中設定主機標頭的詳細資訊，請參閱[設定網站的主機標頭（iis 7）](https://technet.microsoft.com/library/cc753195(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-251">For more information on configuring host headers in IIS 7, see [Configure a Host Header for a Web Site (IIS 7)](https://technet.microsoft.com/library/cc753195(WS.10).aspx).</span></span> <span data-ttu-id="9f16a-252">如需 Windows Server 中 DNS 伺服器角色的詳細資訊，請參閱[Dns 伺服器總覽](https://technet.microsoft.com/library/cc770392.aspx)和[dns 伺服器](https://technet.microsoft.com/windowsserver/dd448607)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-252">For more information on the DNS Server role in Windows Server, see [DNS Server Overview](https://technet.microsoft.com/library/cc770392.aspx) and [DNS Server](https://technet.microsoft.com/windowsserver/dd448607).</span></span>
9. <span data-ttu-id="9f16a-253">在 [ **動作** ] 窗格的 [ **編輯站台**] 下方，按一下 [ **繫結**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-253">In the **Actions** pane, under **Edit Site**, click **Bindings**.</span></span>
10. <span data-ttu-id="9f16a-254">在 [站台繫結] 對話方塊中，按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-254">In the **Site Bindings** dialog box, click **Add**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image12.png)
11. <span data-ttu-id="9f16a-255">在 [**新增網站**系結] 對話方塊中，將 [ **IP 位址**] 和 [**埠**] 設定為符合您現有的網站設定。</span><span class="sxs-lookup"><span data-stu-id="9f16a-255">In the **Add Site Binding** dialog box, set the **IP address** and **Port** to match your existing site configuration.</span></span>
12. <span data-ttu-id="9f16a-256">在 [**主機名稱**] 方塊中，輸入您的 web 伺服器名稱（例如， **STAGEWEB1**），然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9f16a-256">In the **Host name** box, type the name of your web server (for example, **STAGEWEB1**), and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image13.png)

    > [!NOTE]
    > <span data-ttu-id="9f16a-257">第一個網站系結可讓您使用 IP 位址和埠或 `http://localhost:85`，在本機存取網站。</span><span class="sxs-lookup"><span data-stu-id="9f16a-257">The first site binding allows you to access the site locally using the IP address and port or `http://localhost:85`.</span></span> <span data-ttu-id="9f16a-258">第二個網站系結可讓您使用電腦名稱稱（例如 http://stageweb1:85)，從網域中的其他電腦存取網站。</span><span class="sxs-lookup"><span data-stu-id="9f16a-258">The second site binding allows you to access the site from other computers on the domain using the machine name (for example, http://stageweb1:85).</span></span>
13. <span data-ttu-id="9f16a-259">在 [站台繫結] 對話方塊中，按一下 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-259">In the **Site Bindings** dialog box, click **Close**.</span></span>
14. <span data-ttu-id="9f16a-260">**在 [連線**] 窗格中，按一下 [**應用程式**集區]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-260">In the **Connections** pane, click **Application Pools**.</span></span>
15. <span data-ttu-id="9f16a-261">在 [**應用程式**集區] 窗格中，以滑鼠右鍵按一下應用程式集區的名稱，然後按一下 [**基本設定**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-261">In the **Application Pools** pane, right-click the name of your application pool, and then click **Basic Settings**.</span></span> <span data-ttu-id="9f16a-262">根據預設，您的應用程式集區名稱會與您的網站名稱相符（例如， **DemoSite**）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-262">By default, the name of your application pool will match the name of your website (for example, **DemoSite**).</span></span>
16. <span data-ttu-id="9f16a-263">在 [ **.NET clr 版本**] 清單中，選取 [ **.net Clr v 4.0.30319**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9f16a-263">In the **.NET CLR version** list, select **.NET CLR v4.0.30319**, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image21.png)

    > [!NOTE]
    > <span data-ttu-id="9f16a-264">範例解決方案需要 .NET Framework 4.0。</span><span class="sxs-lookup"><span data-stu-id="9f16a-264">The sample solution requires .NET Framework 4.0.</span></span> <span data-ttu-id="9f16a-265">這不是一般 Web Deploy 的需求。</span><span class="sxs-lookup"><span data-stu-id="9f16a-265">This is not a requirement for Web Deploy in general.</span></span>

<span data-ttu-id="9f16a-266">為了讓您的網站提供內容，應用程式集區識別必須具有儲存內容之本機資料夾的讀取權限。</span><span class="sxs-lookup"><span data-stu-id="9f16a-266">In order for your website to serve content, the application pool identity must have read permissions on the local folder that stores the content.</span></span> <span data-ttu-id="9f16a-267">在 IIS 7.5 中，應用程式集區預設會以唯一的應用程式集區身分識別執行（相較于舊版的 IIS，應用程式集區通常會使用網路服務帳戶來執行）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-267">In IIS 7.5, application pools run with a unique application pool identity by default (in contrast to previous versions of IIS, where application pools would typically run using the Network Service account).</span></span> <span data-ttu-id="9f16a-268">應用程式集區身分識別不是真正的使用者帳戶，也不會顯示在任何使用者或群組&#x2014;清單上，而是在啟動應用程式集區時動態建立的。</span><span class="sxs-lookup"><span data-stu-id="9f16a-268">The application pool identity is not a real user account and does not show up on any lists of users or groups&#x2014;instead, it's created dynamically when the application pool is started.</span></span> <span data-ttu-id="9f16a-269">每個應用程式集區識別都會新增至本機**IIS\_給 iis-iusrs**安全性群組做為隱藏專案。</span><span class="sxs-lookup"><span data-stu-id="9f16a-269">Each application pool identity is added to the local **IIS\_IUSRS** security group as a hidden item.</span></span>

<span data-ttu-id="9f16a-270">若要將許可權授與檔案或資料夾上的應用程式集區身分識別，您有兩個選項：</span><span class="sxs-lookup"><span data-stu-id="9f16a-270">To grant permissions to an application pool identity on a file or folder, you have two options:</span></span>

- <span data-ttu-id="9f16a-271">使用 <strong>IIS AppPool\</strong ><em>[應用程式集區名稱]</em>（例如<strong>iis AppPool\DemoSite</strong>）的格式，直接將許可權指派給應用程式集區身分識別。</span><span class="sxs-lookup"><span data-stu-id="9f16a-271">Assign permissions to the application pool identity directly, using the format <strong>IIS AppPool\</strong><em>[application pool name]</em>(for example, <strong>IIS AppPool\DemoSite</strong>).</span></span>
- <span data-ttu-id="9f16a-272">指派許可權給**IIS\_給 iis-iusrs**群組。</span><span class="sxs-lookup"><span data-stu-id="9f16a-272">Assign permissions to the **IIS\_IUSRS** group.</span></span>

<span data-ttu-id="9f16a-273">最常見的方法是將許可權指派給本機**IIS\_給 iis-iusrs**群組，因為這種方法可讓您變更應用程式集區，而不需要重新設定檔案系統許可權。</span><span class="sxs-lookup"><span data-stu-id="9f16a-273">The most common approach is to assign permissions to the local **IIS\_IUSRS** group, because this approach lets you change application pools without reconfiguring file system permissions.</span></span> <span data-ttu-id="9f16a-274">下一個程式會使用這個以群組為基礎的方法。</span><span class="sxs-lookup"><span data-stu-id="9f16a-274">The next procedure uses this group-based approach.</span></span>

> [!NOTE]
> <span data-ttu-id="9f16a-275">如需 IIS 7.5 中應用程式集區身分識別的詳細資訊，請參閱[應用程式集](https://go.microsoft.com/?linkid=9805123)區身分識別。</span><span class="sxs-lookup"><span data-stu-id="9f16a-275">For more information on application pool identities in IIS 7.5, see [Application Pool Identities](https://go.microsoft.com/?linkid=9805123).</span></span>

<span data-ttu-id="9f16a-276">**設定 IIS 網站的資料夾許可權**</span><span class="sxs-lookup"><span data-stu-id="9f16a-276">**To configure folder permissions for an IIS website**</span></span>

1. <span data-ttu-id="9f16a-277">在 Windows Explorer 中，流覽至本機資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="9f16a-277">In Windows Explorer, browse to the location of your local folder.</span></span>
2. <span data-ttu-id="9f16a-278">以滑鼠右鍵按一下該資料夾，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-278">Right-click the folder, and then click **Properties**.</span></span>
3. <span data-ttu-id="9f16a-279">在 [**Security**] 索引標籤上按一下 [**Edit**]，然後按一下 [**Add**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-279">On the **Security** tab, click **Edit**, and then click **Add**.</span></span>
4. <span data-ttu-id="9f16a-280">按一下 [位置]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-280">Click **Locations**.</span></span> <span data-ttu-id="9f16a-281">在 [**位置**] 對話方塊中，選取本機伺服器，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9f16a-281">In the **Locations** dialog box, select the local server, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image15.png)
5. <span data-ttu-id="9f16a-282">在 [**選取使用者或群組**] 對話方塊中，輸入**IIS\_給 iis-iusrs**，按一下 [**檢查名稱**]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9f16a-282">In the **Select Users or Groups** dialog box, type **IIS\_IUSRS**, click **Check Names**, and then click **OK**.</span></span>
6. <span data-ttu-id="9f16a-283">在<em>[資料夾名稱] 的 [</em> <strong>許可權</strong>] 對話方塊中，請注意，預設會將 [<strong>讀取 &amp; 執行</strong>]、[<strong>列出資料夾內容</strong>] 和 [<strong>讀取</strong>] 許可權指派給新的群組。</span><span class="sxs-lookup"><span data-stu-id="9f16a-283">In the <strong>Permissions for</strong><em>[folder name]</em> dialog box, notice that the new group has been assigned the <strong>Read &amp; execute</strong>, <strong>List folder contents</strong>, and <strong>Read</strong> permissions by default.</span></span> <span data-ttu-id="9f16a-284">保持不變，然後按一下<strong>[確定]</strong>。</span><span class="sxs-lookup"><span data-stu-id="9f16a-284">Leave this unchanged and click <strong>OK</strong>.</span></span>
7. <span data-ttu-id="9f16a-285">按一下 [<strong>確定</strong>] 以關閉<em>[資料夾名稱]</em><strong>屬性</strong>對話方塊。</span><span class="sxs-lookup"><span data-stu-id="9f16a-285">Click <strong>OK</strong> to close the <em>[folder name]</em><strong>Properties</strong> dialog box.</span></span>

<span data-ttu-id="9f16a-286">作為最後一項工作，您必須將適當的許可權授與您將用來部署內容之認證的非系統管理員使用者。</span><span class="sxs-lookup"><span data-stu-id="9f16a-286">As a final task, you must grant the appropriate permissions to the non-administrator user whose credentials you'll use to deploy content.</span></span> <span data-ttu-id="9f16a-287">此使用者需要許可權，才能從遠端將內容部署至您的網站。</span><span class="sxs-lookup"><span data-stu-id="9f16a-287">This user requires the permissions to deploy content remotely to your website.</span></span>

<span data-ttu-id="9f16a-288">**為非系統管理員的網域使用者設定 IIS 網站許可權**</span><span class="sxs-lookup"><span data-stu-id="9f16a-288">**To configure IIS website permissions for a non-administrator domain user**</span></span>

1. <span data-ttu-id="9f16a-289">在 [IIS 管理員] 的 [連線] 窗格中，以滑鼠右鍵按一下**您的網站**節點（例如， **DemoSite**），指向 [**部署**]，然後按一下 [**設定 Web Deploy 發佈**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-289">In IIS Manager, in the **Connections** pane, right-click your website node (for example, **DemoSite**), point to **Deploy**, and then click **Configure Web Deploy Publishing**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image16.png)
2. <span data-ttu-id="9f16a-290">在 [**設定 Web Deploy 發佈**] 對話方塊中，按一下 [**選取要授與發行許可權的使用者**] 清單右邊的省略號按鈕。</span><span class="sxs-lookup"><span data-stu-id="9f16a-290">In the **Configure Web Deploy Publishing** dialog box, to the right of the **Select a user to give publishing permissions** list, click the ellipsis button.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image17.png)
3. <span data-ttu-id="9f16a-291">在 [**允許使用者**] 對話方塊中，輸入您要用來部署內容之帳戶的網域和使用者名稱，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="9f16a-291">In the **Allow User** dialog box, type the domain and user name of the account you want to use to deploy content, and then click **OK**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image18.png)
4. <span data-ttu-id="9f16a-292">在 [**設定 Web Deploy 發佈**] 對話方塊中，按一下 [**設定**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-292">In the **Configure Web Deploy Publishing** dialog box, click **Setup**.</span></span>

    ![](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler/_static/image19.png)

    > [!NOTE]
    > <span data-ttu-id="9f16a-293">這項作業會在一個步驟中執行兩個主要功能。</span><span class="sxs-lookup"><span data-stu-id="9f16a-293">This operation performs two key functions in one step.</span></span> <span data-ttu-id="9f16a-294">首先，它會授與使用者許可權，以便根據您在上一節中檢查的委派規則，透過 Web 管理服務從遠端修改網站。</span><span class="sxs-lookup"><span data-stu-id="9f16a-294">First, it grants the user permission to modify the website remotely through the Web Management Service, according to the delegation rules you examined in the previous section.</span></span> <span data-ttu-id="9f16a-295">第二，它會授與使用者對網站之源資料夾的完整控制權，讓使用者能夠新增、修改及設定網站內容的許可權。</span><span class="sxs-lookup"><span data-stu-id="9f16a-295">Second, it grants the user full control of the source folder for the website, which allows the user to add, modify, and set permissions on the website content.</span></span>
5. <span data-ttu-id="9f16a-296">在 [**設定 Web Deploy 發佈**] 對話方塊中，按一下 [**關閉**]。</span><span class="sxs-lookup"><span data-stu-id="9f16a-296">In the **Configure Web Deploy Publishing** dialog box, click **Close**.</span></span>

## <a name="configure-firewall-exceptions"></a><span data-ttu-id="9f16a-297">設定防火牆例外狀況</span><span class="sxs-lookup"><span data-stu-id="9f16a-297">Configure Firewall Exceptions</span></span>

<span data-ttu-id="9f16a-298">根據預設，IIS Web 管理服務會接聽 TCP 通訊埠8172。</span><span class="sxs-lookup"><span data-stu-id="9f16a-298">By default, the IIS Web Management Service listens on TCP port 8172.</span></span> <span data-ttu-id="9f16a-299">如果您的網頁伺服器上已啟用 Windows 防火牆，您將需要建立新的輸入規則，以允許埠8172上的 TCP 流量（Windows 防火牆預設允許所有輸出流量）。</span><span class="sxs-lookup"><span data-stu-id="9f16a-299">If Windows Firewall is enabled on your web server, you'll need to create a new inbound rule to allow TCP traffic on port 8172 (all outbound traffic is permitted by default in Windows Firewall).</span></span> <span data-ttu-id="9f16a-300">如果您使用協力廠商防火牆，您必須建立規則以允許流量。</span><span class="sxs-lookup"><span data-stu-id="9f16a-300">If you use a third-party firewall, you'll need to create rules to allow traffic.</span></span>

| <span data-ttu-id="9f16a-301">方向</span><span class="sxs-lookup"><span data-stu-id="9f16a-301">Direction</span></span> | <span data-ttu-id="9f16a-302">來源埠</span><span class="sxs-lookup"><span data-stu-id="9f16a-302">From Port</span></span> | <span data-ttu-id="9f16a-303">至埠</span><span class="sxs-lookup"><span data-stu-id="9f16a-303">To Port</span></span> | <span data-ttu-id="9f16a-304">連接埠類型</span><span class="sxs-lookup"><span data-stu-id="9f16a-304">Port Type</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="9f16a-305">輸入</span><span class="sxs-lookup"><span data-stu-id="9f16a-305">Inbound</span></span> | <span data-ttu-id="9f16a-306">Any</span><span class="sxs-lookup"><span data-stu-id="9f16a-306">Any</span></span> | <span data-ttu-id="9f16a-307">8172</span><span class="sxs-lookup"><span data-stu-id="9f16a-307">8172</span></span> | <span data-ttu-id="9f16a-308">TCP</span><span class="sxs-lookup"><span data-stu-id="9f16a-308">TCP</span></span> |
| <span data-ttu-id="9f16a-309">輸出</span><span class="sxs-lookup"><span data-stu-id="9f16a-309">Outbound</span></span> | <span data-ttu-id="9f16a-310">8172</span><span class="sxs-lookup"><span data-stu-id="9f16a-310">8172</span></span> | <span data-ttu-id="9f16a-311">Any</span><span class="sxs-lookup"><span data-stu-id="9f16a-311">Any</span></span> | <span data-ttu-id="9f16a-312">TCP</span><span class="sxs-lookup"><span data-stu-id="9f16a-312">TCP</span></span> |

<span data-ttu-id="9f16a-313">如需在 Windows 防火牆中設定規則的詳細資訊，請參閱設定[防火牆規則](https://technet.microsoft.com/library/dd448559(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-313">For more information on configuring rules in Windows Firewall, see [Configuring Firewall Rules](https://technet.microsoft.com/library/dd448559(WS.10).aspx).</span></span> <span data-ttu-id="9f16a-314">如需協力廠商防火牆，請參閱您的產品檔。</span><span class="sxs-lookup"><span data-stu-id="9f16a-314">For third-party firewalls, please consult your product documentation.</span></span>

## <a name="conclusion"></a><span data-ttu-id="9f16a-315">結論</span><span class="sxs-lookup"><span data-stu-id="9f16a-315">Conclusion</span></span>

<span data-ttu-id="9f16a-316">您的 web 伺服器現在應該已準備好接受透過 Web 管理服務對 Web Deploy 處理常式進行遠端部署。</span><span class="sxs-lookup"><span data-stu-id="9f16a-316">Your web server should now be ready to accept remote deployments to the Web Deploy Handler through the Web Management Service.</span></span> <span data-ttu-id="9f16a-317">嘗試將 web 應用程式部署到伺服器之前，您可能會想要檢查下列重點：</span><span class="sxs-lookup"><span data-stu-id="9f16a-317">Before you attempt to deploy a web application to the server, you may want to check these key points:</span></span>

- <span data-ttu-id="9f16a-318">您是否已在 IIS 的伺服器層級上啟用基本驗證？</span><span class="sxs-lookup"><span data-stu-id="9f16a-318">Have you enabled basic authentication at the server level in IIS?</span></span>
- <span data-ttu-id="9f16a-319">您是否已啟用 Web 管理服務的遠端連線？</span><span class="sxs-lookup"><span data-stu-id="9f16a-319">Have you enabled remote connections to the Web Management Service?</span></span>
- <span data-ttu-id="9f16a-320">您是否已啟動 Web 管理服務？</span><span class="sxs-lookup"><span data-stu-id="9f16a-320">Have you started the Web Management Service?</span></span>
- <span data-ttu-id="9f16a-321">管理服務委派規則是否已就緒？</span><span class="sxs-lookup"><span data-stu-id="9f16a-321">Are there management service delegation rules in place?</span></span>
- <span data-ttu-id="9f16a-322">應用程式集區身分識別對您網站的源資料夾具有讀取權限嗎？</span><span class="sxs-lookup"><span data-stu-id="9f16a-322">Does the application pool identity have read access to the source folder for your website?</span></span>
- <span data-ttu-id="9f16a-323">非系統管理員使用者帳戶是否具有 IIS 中的網站層級許可權？</span><span class="sxs-lookup"><span data-stu-id="9f16a-323">Does the non-administrator user account have site-level permissions in IIS?</span></span>
- <span data-ttu-id="9f16a-324">您的防火牆是否允許連到 TCP 埠8172上的伺服器的連入連線？</span><span class="sxs-lookup"><span data-stu-id="9f16a-324">Does your firewall allow incoming connections to the server on TCP port 8172?</span></span>

## <a name="further-reading"></a><span data-ttu-id="9f16a-325">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="9f16a-325">Further Reading</span></span>

<span data-ttu-id="9f16a-326">如需如何設定自訂 Microsoft Build Engine （MSBuild）專案檔以將 web 封裝部署至 Web Deploy 處理常式的指引，請參閱[設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="9f16a-326">For guidance on how to configure custom Microsoft Build Engine (MSBuild) project files to deploy web packages to the Web Deploy Handler, see [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9f16a-327">[上一頁](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
> [下一頁](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="9f16a-327">[Previous](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)</span></span>
