---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 使用 Visual Studio ASP.NET Web 部署：部署至測試 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: c45003325832258466a787bc589bf40e844248a2
ms.sourcegitcommit: 4b324a11131e38f920126066b94ff478aa9927f8
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/13/2019
ms.locfileid: "70985848"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a><span data-ttu-id="7966c-103">使用 Visual Studio ASP.NET Web 部署：部署到測試環境</span><span class="sxs-lookup"><span data-stu-id="7966c-103">ASP.NET Web Deployment using Visual Studio: Deploying to Test</span></span>

<span data-ttu-id="7966c-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="7966c-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

<span data-ttu-id="7966c-105">本教學課程系列說明如何使用 Visual Studio 2017，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。</span><span class="sxs-lookup"><span data-stu-id="7966c-105">This tutorial series shows how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider using Visual Studio 2017.</span></span> <span data-ttu-id="7966c-106">如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。</span><span class="sxs-lookup"><span data-stu-id="7966c-106">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

<span data-ttu-id="7966c-107">如需部署至 Azure 的最新版本，請參閱[在 azure 中建立 ASP.NET Core web 應用程式](/azure/app-service/app-service-web-get-started-dotnet)。</span><span class="sxs-lookup"><span data-stu-id="7966c-107">For a current version of deploying to Azure, see [Create an ASP.NET Core web app in Azure](/azure/app-service/app-service-web-get-started-dotnet).</span></span>

## <a name="overview"></a><span data-ttu-id="7966c-108">總覽</span><span class="sxs-lookup"><span data-stu-id="7966c-108">Overview</span></span>

<span data-ttu-id="7966c-109">在本教學課程中，您會將 ASP.NET web 應用程式部署到本機電腦上的 Internet information Server （IIS）。</span><span class="sxs-lookup"><span data-stu-id="7966c-109">In this tutorial, you'll deploy an ASP.NET web application to Internet Information Server (IIS) on your local computer.</span></span>

<span data-ttu-id="7966c-110">一般而言，當您開發應用程式時，您會執行它並在 Visual Studio 中進行測試。</span><span class="sxs-lookup"><span data-stu-id="7966c-110">Generally when you develop an application, you run it and test it in Visual Studio.</span></span> <span data-ttu-id="7966c-111">根據預設，Visual Studio 2017 中的 web 應用程式專案會使用 IIS Express 作為開發 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="7966c-111">By default, web application projects in Visual Studio 2017 use IIS Express as the development web server.</span></span> <span data-ttu-id="7966c-112">IIS Express 的行為比 Visual Studio 程式開發伺服器（也稱為 Cassini）更像是完整的 IIS，Visual Studio 2017 預設使用。</span><span class="sxs-lookup"><span data-stu-id="7966c-112">IIS Express behaves more like full IIS than the Visual Studio Development Server (also known as Cassini), which Visual Studio 2017 uses by default.</span></span> <span data-ttu-id="7966c-113">但這兩種開發 web 伺服器的運作方式都與 IIS 完全一樣。</span><span class="sxs-lookup"><span data-stu-id="7966c-113">But neither development web server works exactly like IIS.</span></span> <span data-ttu-id="7966c-114">因此，應用程式可以在 Visual Studio 中正確執行和測試，但在部署到 IIS 時失敗。</span><span class="sxs-lookup"><span data-stu-id="7966c-114">Consequently, an app could run and test correctly in Visual Studio but fail when it's deployed to IIS.</span></span>

<span data-ttu-id="7966c-115">您可以透過兩種方式可靠地測試您的應用程式：</span><span class="sxs-lookup"><span data-stu-id="7966c-115">You can reliably test your application in two ways:</span></span>

1. <span data-ttu-id="7966c-116">使用您稍後將用來部署至生產環境的相同程式，將您的應用程式部署到開發電腦上的 IIS。</span><span class="sxs-lookup"><span data-stu-id="7966c-116">Deploy your application to IIS on your development computer using the same process that you'll use later to deploy it to your production environment.</span></span>

   <span data-ttu-id="7966c-117">當您執行 Web 專案時，可以將 Visual Studio 設定為使用 IIS，但這樣做並不會測試您的部署流程。</span><span class="sxs-lookup"><span data-stu-id="7966c-117">You can configure Visual Studio to use IIS when you run a web project, but that wouldn't test your deployment process.</span></span> <span data-ttu-id="7966c-118">這個方法會驗證您的部署程式，而且您的應用程式會在 IIS 底下正確執行。</span><span class="sxs-lookup"><span data-stu-id="7966c-118">This method validates your deployment process and that your application runs correctly under IIS.</span></span>

2. <span data-ttu-id="7966c-119">將您的應用程式部署至類似您生產環境的測試環境。</span><span class="sxs-lookup"><span data-stu-id="7966c-119">Deploy your application to a test environment similar to your production environment.</span></span> 
 
   <span data-ttu-id="7966c-120">這些教學課程的生產環境會在 Azure App Service 中 Web Apps。</span><span class="sxs-lookup"><span data-stu-id="7966c-120">The production environment for these tutorials is Web Apps in Azure App Service.</span></span> <span data-ttu-id="7966c-121">理想的測試環境是在 Azure 服務中建立的額外 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7966c-121">The ideal test environment is an additional web app created in the Azure Service.</span></span> <span data-ttu-id="7966c-122">雖然它會以與生產 web 應用程式相同的方式來設定，但您只會使用它來進行測試。</span><span class="sxs-lookup"><span data-stu-id="7966c-122">Though it would be set up the same way as a production web app, you would only use it for testing.</span></span>

<span data-ttu-id="7966c-123">選項2是最可靠的測試方式。</span><span class="sxs-lookup"><span data-stu-id="7966c-123">Option 2 is the most reliable way to test.</span></span> <span data-ttu-id="7966c-124">如果您使用選項2，則不一定需要使用選項1。</span><span class="sxs-lookup"><span data-stu-id="7966c-124">If you use option 2, you don't necessarily need to use option 1.</span></span> <span data-ttu-id="7966c-125">不過，如果您要部署到協力廠商主機服務提供者，選項2可能不可行或成本很高，因此本教學課程系列會顯示這兩種方法。</span><span class="sxs-lookup"><span data-stu-id="7966c-125">However if you're deploying to a third-party hosting provider, option 2 might not be feasible or might be expensive, so this tutorial series shows both methods.</span></span> <span data-ttu-id="7966c-126">[部署至生產環境](deploying-to-production.md)教學課程中提供選項2的指引。</span><span class="sxs-lookup"><span data-stu-id="7966c-126">Guidance for option 2 is provided in the [Deploying to the Production Environment](deploying-to-production.md) tutorial.</span></span>

<span data-ttu-id="7966c-127">如需在 Visual Studio 中使用 web 伺服器的詳細資訊，請參閱[Visual Studio 中 ASP.NET Web 專案的 Web 服務器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7966c-127">For more information about using web servers in Visual Studio, see [Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>

<span data-ttu-id="7966c-128">一下如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="7966c-128">Reminder: If you receive an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="download-the-contoso-university-starter-project"></a><span data-ttu-id="7966c-129">下載 Contoso 大學入門專案</span><span class="sxs-lookup"><span data-stu-id="7966c-129">Download the Contoso University starter project</span></span>

<span data-ttu-id="7966c-130">下載並安裝 Contoso 大學 Visual Studio starter 解決方案和專案。</span><span class="sxs-lookup"><span data-stu-id="7966c-130">Download and install the Contoso University Visual Studio starter solution and project.</span></span> <span data-ttu-id="7966c-131">此解決方案包含已完成的教學課程。</span><span class="sxs-lookup"><span data-stu-id="7966c-131">This solution contains the completed tutorial.</span></span> 

[<span data-ttu-id="7966c-132">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="7966c-132">Download Starter Project</span></span>](http://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a><span data-ttu-id="7966c-133">安裝 IIS</span><span class="sxs-lookup"><span data-stu-id="7966c-133">Install IIS</span></span>

<span data-ttu-id="7966c-134">若要部署至開發電腦上的 IIS，請確認已安裝 IIS 和 Web Deploy。</span><span class="sxs-lookup"><span data-stu-id="7966c-134">To deploy to IIS on your development computer, confirm that IIS and Web Deploy are installed.</span></span> <span data-ttu-id="7966c-135">根據預設，Visual Studio 會安裝 Web Deploy，但 IIS 並未包含在預設的 Windows 10、Windows 8 或 Windows 7 設定中。</span><span class="sxs-lookup"><span data-stu-id="7966c-135">By default, Visual Studio installs Web Deploy, but IIS isn't included in the default Windows 10, Windows 8, or Windows 7 configuration.</span></span> <span data-ttu-id="7966c-136">如果您已經安裝 IIS，而且預設應用程式集區已設定為 .NET 4，請跳到[下一節](#sqlexpress)。</span><span class="sxs-lookup"><span data-stu-id="7966c-136">If you've already installed IIS and the default application pool is already set to .NET 4, skip to [the next section](#sqlexpress).</span></span>

1. <span data-ttu-id="7966c-137">建議您使用[Web Platform Installer （download-wpi）](https://www.microsoft.com/web/downloads/platform.aspx)來安裝 IIS 和 Web Deploy。</span><span class="sxs-lookup"><span data-stu-id="7966c-137">It's recommended you use the [Web Platform Installer (WPI)](https://www.microsoft.com/web/downloads/platform.aspx) to install IIS and Web Deploy.</span></span> <span data-ttu-id="7966c-138">DOWNLOAD-WPI 會安裝建議的 IIS 設定，其中包含 IIS 並在必要時 Web Deploy 必要條件。</span><span class="sxs-lookup"><span data-stu-id="7966c-138">WPI installs a recommended IIS configuration that includes IIS and Web Deploy prerequisites if necessary.</span></span>

   <span data-ttu-id="7966c-139">如果您已安裝 IIS、Web Deploy 或其任何必要的元件，DOWNLOAD-WPI 只會安裝遺失的內容。</span><span class="sxs-lookup"><span data-stu-id="7966c-139">If you've already installed IIS, Web Deploy, or any of their required components, the WPI installs only what is missing.</span></span>

   * <span data-ttu-id="7966c-140">使用 Web Platform Installer 來安裝 IIS 和 Web Deploy：</span><span class="sxs-lookup"><span data-stu-id="7966c-140">Use the Web Platform Installer to install IIS and Web Deploy:</span></span>
    
     ![使用 DOWNLOAD-WPI 安裝 IIS](deploying-to-iis/_static/image30.png)

     ![使用 DOWNLOAD-WPI 安裝 Web Deploy](deploying-to-iis/_static/image31.png)

     <span data-ttu-id="7966c-143">您會看到指出將會安裝 IIS 7 的訊息。</span><span class="sxs-lookup"><span data-stu-id="7966c-143">You'll see messages indicating that IIS 7 will be installed.</span></span> <span data-ttu-id="7966c-144">此連結適用于 Windows 8 中的 IIS 8;但是對於 Windows 8 和更新版本，請執行下列步驟，以確定已安裝 ASP.NET 4.7：</span><span class="sxs-lookup"><span data-stu-id="7966c-144">The link works for IIS 8 in Windows 8; but for Windows 8 and later, go through the following steps to make sure that ASP.NET 4.7 is installed:</span></span>

   * <span data-ttu-id="7966c-145">開啟 [**控制台** >   > ] [程式] [程式和功能] [開啟或關閉 Windows 功能]。 > </span><span class="sxs-lookup"><span data-stu-id="7966c-145">Open **Control Panel** > **Programs** > **Programs and Features** > **Turn Windows features on or off**.</span></span>

   * <span data-ttu-id="7966c-146">展開 [ **Internet Information Services**]、[ **World Wide Web 服務**] 和 [**應用程式開發] 功能**。</span><span class="sxs-lookup"><span data-stu-id="7966c-146">Expand **Internet Information Services**, **World Wide Web Services**, and **Application Development Features**.</span></span>
   
   * <span data-ttu-id="7966c-147">確認已選取 [ **ASP.NET 4.7** ]。</span><span class="sxs-lookup"><span data-stu-id="7966c-147">Confirm that **ASP.NET 4.7** is selected.</span></span>

     ![選取 ASP.NET 4。7](deploying-to-iis/_static/image1a.png)

   * <span data-ttu-id="7966c-149">確認已選取 [ **World Wide Web 服務**] 和 [ **IIS 管理主控台**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-149">Confirm that **World Wide Web Services** and **IIS Management Console** is selected.</span></span> <span data-ttu-id="7966c-150">這會安裝 IIS 和 IIS 管理員。</span><span class="sxs-lookup"><span data-stu-id="7966c-150">This installs IIS and IIS Manager.</span></span>
    
     ![選取 World Wide Web 服務](deploying-to-iis/_static/image24.png)    
  
   * <span data-ttu-id="7966c-152">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7966c-152">Select **OK**.</span></span> <span data-ttu-id="7966c-153">指出已進行安裝的對話方塊訊息隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7966c-153">Dialog box messages indicating installation is taking place appear.</span></span>

<span data-ttu-id="7966c-154">安裝 IIS 之後，請執行**Iis 管理員**，以確定 .NET Framework 第4版已指派給預設的應用程式集區。</span><span class="sxs-lookup"><span data-stu-id="7966c-154">After installing IIS, run **IIS Manager** to make sure that the .NET Framework version 4 is assigned to the default application pool.</span></span>

1. <span data-ttu-id="7966c-155">按 WINDOWS + R，以開啟 [**執行**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="7966c-155">Press WINDOWS+R to open the **Run** dialog box.</span></span>

   <span data-ttu-id="7966c-156">（在 Windows 8 或更新版本上，在 [**開始**] 頁面上輸入 "run"。</span><span class="sxs-lookup"><span data-stu-id="7966c-156">(On Windows 8 or later, enter "run" on the **Start** page.</span></span> <span data-ttu-id="7966c-157">在 Windows 7 中，從 [**開始**] 功能表選取 [**執行**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-157">In Windows 7, select **Run** from the **Start** menu.</span></span> <span data-ttu-id="7966c-158">如果 [**執行**] 不在 [**開始**] 功能表中，請以滑鼠右鍵按一下工作列，然後依序選取 [**屬性**]、[**開始] 功能表**索引標籤、[**自訂**] 和 [**執行命令**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-158">If **Run** isn't in the **Start** menu, right-click the taskbar, select **Properties**, select the **Start Menu** tab, select **Customize**, and select **Run command**.)</span></span>

2. <span data-ttu-id="7966c-159">輸入 "inetmgr"，然後選取 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="7966c-159">Enter "inetmgr" and select **OK**.</span></span>

3. <span data-ttu-id="7966c-160">在 [**連線] 窗格**中，展開伺服器節點，然後選取 [**應用程式**集區]。</span><span class="sxs-lookup"><span data-stu-id="7966c-160">In the **Connections** pane, expand the server node and select **Application Pools**.</span></span> <span data-ttu-id="7966c-161">在 [**應用程式**集區] 窗格中，如果**DefaultAppPool**已指派給 .net framework 第4版（如下圖所示），請跳至下一節。</span><span class="sxs-lookup"><span data-stu-id="7966c-161">In the **Application Pools** pane if **DefaultAppPool** is assigned to the .NET framework version 4 as in the following illustration, skip to the next section.</span></span>

   ![Inetmgr_showing_4.0_app_pools](deploying-to-iis/_static/image5a.png)

4. <span data-ttu-id="7966c-163">如果您只看到兩個應用程式集區，且兩者都設定為 .NET Framework 2.0，請在 IIS 中安裝 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="7966c-163">If you see only two application pools and both are set to .NET Framework 2.0, install ASP.NET 4 in IIS.</span></span>

   <span data-ttu-id="7966c-164">針對 Windows 8 或更新版本，請參閱上一節的指示，以確定已安裝 ASP.NET 4.7，或參閱[如何在 windows 8 和 Windows Server 2012 上安裝 ASP.NET 4.5](https://support.microsoft.com/kb/2736284)。</span><span class="sxs-lookup"><span data-stu-id="7966c-164">For Windows 8 or later, see the previous section's instructions for making sure that ASP.NET 4.7 is installed or see [How to install ASP.NET 4.5 on Windows 8 and Windows Server 2012](https://support.microsoft.com/kb/2736284).</span></span> <span data-ttu-id="7966c-165">若是 Windows 7，請以滑鼠右鍵按一下 Windows [**開始**] 功能表中的 [**命令提示**字元]，然後選取 [以**系統管理員身分執行**]，開啟命令提示字元視窗</span><span class="sxs-lookup"><span data-stu-id="7966c-165">For Windows 7, open a command prompt window by right-clicking **Command Prompt** in the Windows **Start** menu and selecting **Run as Administrator**.</span></span> <span data-ttu-id="7966c-166">執行[aspnet\_regiis](https://msdn.microsoft.com/library/k6h9cz8h.aspx) ，使用下列命令在 IIS 中安裝 ASP.NET 4。</span><span class="sxs-lookup"><span data-stu-id="7966c-166">Run [aspnet\_regiis.exe](https://msdn.microsoft.com/library/k6h9cz8h.aspx) to install ASP.NET 4 in IIS using the following commands.</span></span> <span data-ttu-id="7966c-167">（在32位系統中，將 "Framework64" 取代為 "Framework"）。</span><span class="sxs-lookup"><span data-stu-id="7966c-167">(In 32-bit systems, replace "Framework64" with "Framework".)</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   <span data-ttu-id="7966c-168">此命令會建立 .NET Framework 4 的新應用程式集區，但預設的應用程式集區仍會設定為2.0。</span><span class="sxs-lookup"><span data-stu-id="7966c-168">This command creates new application pools for the .NET Framework 4, but the default application pool will remain set to 2.0.</span></span> <span data-ttu-id="7966c-169">您要將以 .NET 4 為目標的應用程式部署到該應用程式集區，因此請將應用程式集區變更為 .NET 4。</span><span class="sxs-lookup"><span data-stu-id="7966c-169">You're deploying an application that targets .NET 4 to that application pool, so change the application pool to .NET 4.</span></span>

5. <span data-ttu-id="7966c-170">如果您關閉了 [ **IIS 管理員**]，請再次執行它，展開伺服器節點，然後選取 [**應用程式**集區]。</span><span class="sxs-lookup"><span data-stu-id="7966c-170">If you closed **IIS Manager**, run it again, expand the server node, and select **Application Pools**.</span></span>

6. <span data-ttu-id="7966c-171">在 [**應用程式**集區] 窗格中，選取 [ **DefaultAppPool**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-171">In the **Application Pools** pane, select **DefaultAppPool**.</span></span> <span data-ttu-id="7966c-172">在 [**動作**] 窗格中，選取 [**基本設定**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-172">In the **Actions** pane, select **Basic Settings**.</span></span>

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. <span data-ttu-id="7966c-174">在 [**編輯應用程式集**區] 對話方塊中，將 [ **.net clr 版本**] 變更為 [ **.net clr v 4.0.30319**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-174">In the **Edit Application Pool** dialog box, change the **.NET CLR version** to **.NET CLR v4.0.30319**.</span></span> <span data-ttu-id="7966c-175">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7966c-175">Select **OK**.</span></span>

   ![Selecting_.NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

<span data-ttu-id="7966c-177">您現在已準備好將 web 應用程式發佈至 IIS。</span><span class="sxs-lookup"><span data-stu-id="7966c-177">You're now ready to publish a web application to IIS.</span></span> <span data-ttu-id="7966c-178">不過，首先要建立資料庫來進行測試。</span><span class="sxs-lookup"><span data-stu-id="7966c-178">First, however, create databases for testing.</span></span>

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a><span data-ttu-id="7966c-179">安裝 SQL Server Express</span><span class="sxs-lookup"><span data-stu-id="7966c-179">Install SQL Server Express</span></span>

<span data-ttu-id="7966c-180">LocalDB 並非設計成在 IIS 中工作，因此您的測試環境必須安裝 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="7966c-180">LocalDB isn't designed to work in IIS, so your test environment has to have SQL Server Express installed.</span></span> <span data-ttu-id="7966c-181">如果您使用 Visual Studio 2010 SQL Server Express，則預設已安裝。</span><span class="sxs-lookup"><span data-stu-id="7966c-181">If you're using Visual Studio 2010 SQL Server Express, it's already installed by default.</span></span> <span data-ttu-id="7966c-182">如果您使用的是 Visual Studio 2012 或更新版本，請安裝 SQL Server Express。</span><span class="sxs-lookup"><span data-stu-id="7966c-182">If you're using Visual Studio 2012 or later, install SQL Server Express.</span></span>

<span data-ttu-id="7966c-183">若要安裝 SQL Server Express，請從[下載中心下載並安裝：Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express)。</span><span class="sxs-lookup"><span data-stu-id="7966c-183">To install SQL Server Express, download and install it from [Download Center: Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express).</span></span> 

<span data-ttu-id="7966c-184">在 SQL Server 安裝中心 的第一頁上，選取 新增  **SQL Server 獨立安裝 或 將功能新增至現有安裝**，並依照指示接受預設選項。</span><span class="sxs-lookup"><span data-stu-id="7966c-184">On the first page of the SQL Server Installation Center, select **New SQL Server stand-alone installation or add features to an existing installation** and follow the instructions accepting the default choices.</span></span> <span data-ttu-id="7966c-185">在安裝精靈中，接受預設設定。</span><span class="sxs-lookup"><span data-stu-id="7966c-185">In the installation wizard, accept the default settings.</span></span> <span data-ttu-id="7966c-186">如需安裝選項的詳細資訊，請參閱[從安裝精靈安裝 SQL Server （安裝程式）](https://msdn.microsoft.com/library/ms143219.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7966c-186">For more information about installation options, see [Install SQL Server from the Installation Wizard (Setup)](https://msdn.microsoft.com/library/ms143219.aspx).</span></span>

## <a name="create-sql-server-express-databases-for-the-test-environment"></a><span data-ttu-id="7966c-187">建立測試環境的 SQL Server Express 資料庫</span><span class="sxs-lookup"><span data-stu-id="7966c-187">Create SQL Server Express databases for the test environment</span></span>

<span data-ttu-id="7966c-188">Contoso 大學應用程式有兩個資料庫：</span><span class="sxs-lookup"><span data-stu-id="7966c-188">The Contoso University application has two databases:</span></span> 

1. <span data-ttu-id="7966c-189">成員資格資料庫</span><span class="sxs-lookup"><span data-stu-id="7966c-189">Membership database</span></span> 
2. <span data-ttu-id="7966c-190">應用程式資料庫</span><span class="sxs-lookup"><span data-stu-id="7966c-190">Application database</span></span> 

<span data-ttu-id="7966c-191">您可以將這些資料庫部署到兩個不同的資料庫或單一資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-191">You can deploy these databases to two separate databases or to a single database.</span></span> <span data-ttu-id="7966c-192">結合它們可讓它們之間的資料庫聯結變得更容易。</span><span class="sxs-lookup"><span data-stu-id="7966c-192">Combining them makes database joins between them easier.</span></span> 

<span data-ttu-id="7966c-193">如果您要部署到協力廠商主機服務提供者，您的主控方案可能也會讓您有理由加以結合。</span><span class="sxs-lookup"><span data-stu-id="7966c-193">If you're deploying to a third-party hosting provider, your hosting plan might also give you a reason to combine them.</span></span> <span data-ttu-id="7966c-194">例如，提供者可能會對多個資料庫收取更多費用，或甚至不允許一個以上的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-194">For example, the provider might charge more for multiple databases or might not even allow more than one database.</span></span>

<span data-ttu-id="7966c-195">在本教學課程中，您會在測試環境中部署至兩個資料庫，並在預備和生產環境中部署到一個資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-195">In this tutorial, you'll deploy to two databases in the test environment and to one database in the staging and production environments.</span></span>

<span data-ttu-id="7966c-196">從 Visual Studio 的 [ **View** ] 功能表中，選取 [**伺服器總管**（Visual Web Developer 中的**資料庫總管**）]。</span><span class="sxs-lookup"><span data-stu-id="7966c-196">From the **View** menu in Visual Studio, select **Server Explorer** (**Database Explorer** in Visual Web Developer).</span></span> <span data-ttu-id="7966c-197">以滑鼠右鍵按一下 [**資料連線**]，然後選取 [**建立新的 SQL Server 資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-197">Right-click **Data Connections** and select **Create New SQL Server Database**.</span></span>

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

<span data-ttu-id="7966c-199">在 [**建立新的 SQL Server 資料庫**] 對話方塊中，于 [**伺服器名稱**] 方塊中輸入 ".\SQLExpress"，並在 [**新資料庫名稱**] 方塊中輸入 "aspnet-ContosoUniversity"。</span><span class="sxs-lookup"><span data-stu-id="7966c-199">In the **Create New SQL Server Database** dialog box, enter ".\SQLExpress" in the **Server name** box and "aspnet-ContosoUniversity" in the **New database name** box.</span></span> <span data-ttu-id="7966c-200">選取 [確定]。</span><span class="sxs-lookup"><span data-stu-id="7966c-200">Select **OK**.</span></span>

![建立 aspnet-ContosoUniversity](deploying-to-iis/_static/image9.png)

<span data-ttu-id="7966c-202">遵循相同的程式，建立名為`ContosoUniversity`的新 SQL Server Express School 資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-202">Follow the same procedure to create a new SQL Server Express School database named `ContosoUniversity`.</span></span>

<span data-ttu-id="7966c-203">**伺服器總管**會顯示兩個新的資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-203">**Server Explorer** shows the two new databases.</span></span>

![伺服器總管中的新資料庫](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a><span data-ttu-id="7966c-205">建立新資料庫的授與腳本</span><span class="sxs-lookup"><span data-stu-id="7966c-205">Create a grant script for the new databases</span></span>

<span data-ttu-id="7966c-206">當應用程式在開發電腦上的 IIS 中執行時，應用程式會使用預設應用程式集區的認證來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-206">When the application runs in IIS on your development computer, the application uses the default application pool's credentials to access the database.</span></span> <span data-ttu-id="7966c-207">不過，根據預設，應用程式集區沒有開啟資料庫的許可權。</span><span class="sxs-lookup"><span data-stu-id="7966c-207">However, by default, the application pool doesn't have permission to open the databases.</span></span> <span data-ttu-id="7966c-208">這表示您需要執行腳本以授與該許可權。</span><span class="sxs-lookup"><span data-stu-id="7966c-208">This means you need to run a script to grant that permission.</span></span> <span data-ttu-id="7966c-209">在本節中，您將建立該腳本並于稍後執行，以確保應用程式可以在 IIS 中執行時開啟資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-209">In this section, you'll create that script and run it later to make sure that the application can open the databases when it runs in IIS.</span></span>

<span data-ttu-id="7966c-210">在文字編輯器中，將下列 SQL 命令複製到新的檔案，並將它儲存為*Grant. SQL*。</span><span class="sxs-lookup"><span data-stu-id="7966c-210">In a text editor, copy the following SQL commands into a new file and save it as *Grant.sql*.</span></span> 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

<span data-ttu-id="7966c-211">在 Visual Studio 中，開啟 [Contoso 大學] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="7966c-211">In Visual Studio, open the Contoso University solution.</span></span> <span data-ttu-id="7966c-212">以滑鼠右鍵按一下方案（不是其中一個專案），然後選取 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-212">Right-click the solution (not one of the projects), and select **Add**.</span></span> <span data-ttu-id="7966c-213">選取 [**現有專案**]，流覽至 *[授與 .sql*]，然後開啟它。</span><span class="sxs-lookup"><span data-stu-id="7966c-213">Select **Existing Item**, browse to *Grant.sql*, and open it.</span></span>

> [!NOTE]
> <span data-ttu-id="7966c-214">此腳本是設計用來搭配 SQL Server Express 2012 或更新版本，以及在本教學課程中指定的 Windows 10、Windows 8 或 Windows 7 中的 IIS 設定。</span><span class="sxs-lookup"><span data-stu-id="7966c-214">This script is designed to work with SQL Server Express 2012 or later and with the IIS settings in Windows 10, Windows 8, or Windows 7 as they are specified in this tutorial.</span></span> <span data-ttu-id="7966c-215">如果您使用的是不同版本的 SQL Server 或 Windows，或如果您在電腦上以不同的方式設定 IIS，可能就需要變更此腳本。</span><span class="sxs-lookup"><span data-stu-id="7966c-215">If you're using a different version of SQL Server or Windows, or if you set up IIS on your computer differently, changes to this script might be required.</span></span> <span data-ttu-id="7966c-216">如需 SQL Server 腳本的詳細資訊，請參閱[SQL Server 線上叢書](https://go.microsoft.com/fwlink/?LinkId=132511)。</span><span class="sxs-lookup"><span data-stu-id="7966c-216">For more information about SQL Server scripts, see [SQL Server Books Online](https://go.microsoft.com/fwlink/?LinkId=132511).</span></span>

> [!NOTE] 
> <span data-ttu-id="7966c-217">**安全性注意事項**此腳本`db_owner`會將許可權授與在執行時間存取資料庫的使用者，這就是您在生產環境中擁有的功能。</span><span class="sxs-lookup"><span data-stu-id="7966c-217">**Security Note** This script gives `db_owner` permissions to the user that accesses the database at run time, which is what you'll have in the production environment.</span></span> <span data-ttu-id="7966c-218">在某些情況下，您可能會想要指定具有完整資料庫架構更新許可權的使用者，僅供部署之用，並為執行時間指定僅具有讀取和寫入資料許可權的其他使用者。</span><span class="sxs-lookup"><span data-stu-id="7966c-218">In some scenarios, you might want to specify a user that has full database schema update permissions only for deployment and specify for run time a different user that has permissions only to read and write data.</span></span> <span data-ttu-id="7966c-219">如需詳細資訊，請參閱本教學課程稍後的 <<c0>檢查自動的 Web.config 變更 Code First 移轉。</span><span class="sxs-lookup"><span data-stu-id="7966c-219">For more information, see [Reviewing the Automatic Web.config Changes for Code First Migrations](#reviewingmigrations) later in this tutorial.</span></span>

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a><span data-ttu-id="7966c-220">在應用程式資料庫中執行 grant 腳本</span><span class="sxs-lookup"><span data-stu-id="7966c-220">Run the grant script in the application database</span></span>

<span data-ttu-id="7966c-221">您可以將發行設定檔設定為在部署期間于成員資格資料庫中執行授與腳本，因為該資料庫部署會使用[dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing)提供者。</span><span class="sxs-lookup"><span data-stu-id="7966c-221">You can configure the publish profile to run the grant script in the membership database during deployment because that database deployment uses the [dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing) provider.</span></span> <span data-ttu-id="7966c-222">您無法在 Code First 移轉部署期間執行腳本，這就是部署應用程式資料庫的方式。</span><span class="sxs-lookup"><span data-stu-id="7966c-222">You can't run scripts during Code First Migrations deployment, which is how you're deploying the application database.</span></span> <span data-ttu-id="7966c-223">這表示您必須在應用程式資料庫中部署之前，手動執行腳本。</span><span class="sxs-lookup"><span data-stu-id="7966c-223">This means you have to manually run the script before deployment in the application database.</span></span>

1. <span data-ttu-id="7966c-224">在 Visual Studio 中，開啟您稍早建立的*Grant .sql*檔案。</span><span class="sxs-lookup"><span data-stu-id="7966c-224">In Visual Studio, open the *Grant.sql* file that you created earlier.</span></span>

2. <span data-ttu-id="7966c-225">選取 **[連線]** 。</span><span class="sxs-lookup"><span data-stu-id="7966c-225">Select **Connect**.</span></span> 

    ![[連線] 按鈕](deploying-to-iis/_static/image11.png)

3. <span data-ttu-id="7966c-227">在 [**連接到伺服器**] 對話方塊中，輸入 *.\SQLExpress*做為**伺服器名稱**。</span><span class="sxs-lookup"><span data-stu-id="7966c-227">In the **Connect to Server** dialog box, enter *.\SQLExpress* as the **Server Name**.</span></span> <span data-ttu-id="7966c-228">選取 **[連線]** 。</span><span class="sxs-lookup"><span data-stu-id="7966c-228">Select **Connect**.</span></span>

4. <span data-ttu-id="7966c-229">在 [資料庫] 下拉式清單中，選取 [ **ContosoUniversity**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-229">In the database drop-down list select **ContosoUniversity**.</span></span> <span data-ttu-id="7966c-230">選取 [**執行**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-230">Select **Execute**.</span></span> 

   ![](deploying-to-iis/_static/image12.png)

<span data-ttu-id="7966c-231">預設應用程式集區身分識別現在在應用程式資料庫中有足夠的許可權，可供 Code First 移轉在應用程式執行時建立資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="7966c-231">The default application pool identity now has sufficient permissions in the application database for Code First Migrations to create the database tables when the application runs.</span></span>

## <a name="publish-to-iis"></a><span data-ttu-id="7966c-232">發佈至 IIS</span><span class="sxs-lookup"><span data-stu-id="7966c-232">Publish to IIS</span></span>

<span data-ttu-id="7966c-233">有數種方式可供您使用 Visual Studio 和 Web Deploy 部署到 IIS：</span><span class="sxs-lookup"><span data-stu-id="7966c-233">There are several ways you can deploy to IIS using Visual Studio and Web Deploy:</span></span>

* <span data-ttu-id="7966c-234">使用 Visual Studio 單鍵發行。</span><span class="sxs-lookup"><span data-stu-id="7966c-234">Use Visual Studio one-click publish.</span></span>
* <span data-ttu-id="7966c-235">從命令列發佈。</span><span class="sxs-lookup"><span data-stu-id="7966c-235">Publish from the command line.</span></span>
* <span data-ttu-id="7966c-236">建立部署套件，並使用 IIS 管理員進行安裝。</span><span class="sxs-lookup"><span data-stu-id="7966c-236">Create a deployment package and install it using IIS Manager.</span></span> <span data-ttu-id="7966c-237">封裝有一個 .zip 檔案，其中包含在 IIS 中安裝網站所需的所有檔案和中繼資料。</span><span class="sxs-lookup"><span data-stu-id="7966c-237">The package has a .zip file with all the files and metadata required to install a site in IIS.</span></span>
* <span data-ttu-id="7966c-238">建立部署套件，並使用命令列進行安裝。</span><span class="sxs-lookup"><span data-stu-id="7966c-238">Create a deployment package and install it using the command line.</span></span>

<span data-ttu-id="7966c-239">您在先前的教學課程中完成以設定 Visual Studio 來自動化部署工作的程式，適用于所有這些方法。</span><span class="sxs-lookup"><span data-stu-id="7966c-239">The process you went through in the previous tutorials to set up Visual Studio to automate deployment tasks applies to all of these methods.</span></span> <span data-ttu-id="7966c-240">在這些教學課程中，您將使用前兩個方法。</span><span class="sxs-lookup"><span data-stu-id="7966c-240">In these tutorials, you'll use the first two methods.</span></span> <span data-ttu-id="7966c-241">如需使用部署套件的詳細資訊，請參閱 Visual Studio 和 ASP.NET 的 Web 部署內容對應中[建立和安裝 web 部署套件，以部署 web 應用程式](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)。</span><span class="sxs-lookup"><span data-stu-id="7966c-241">For information about using deployment packages, see [Deploying a web application by creating and installing a web deployment package](https://go.microsoft.com/fwlink/p/?LinkId=282413#package) in the Web Deployment Content Map for Visual Studio and ASP.NET.</span></span>

<span data-ttu-id="7966c-242">在發佈之前，請確定您是以系統管理員模式執行 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7966c-242">Before publishing, make sure that you're running Visual Studio in administrator mode.</span></span> <span data-ttu-id="7966c-243">如果您在標題列中沒有看到 **（系統管理員）** ，請關閉 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="7966c-243">If you don't see **(Administrator)** in the title bar, close Visual Studio.</span></span> <span data-ttu-id="7966c-244">在 Windows 8 （或更新版本）**起始**頁或 windows 7 **開始** 功能表中，以滑鼠右鍵按一下 Visual Studio 圖示，然後選取 以**系統管理員身分執行**。</span><span class="sxs-lookup"><span data-stu-id="7966c-244">In the Windows 8 (or later) **Start** page or the Windows 7 **Start** menu, right-click the Visual Studio icon and select **Run as Administrator**.</span></span> <span data-ttu-id="7966c-245">只有當您要發行到本機電腦上的 IIS 時，才需要系統管理員模式。</span><span class="sxs-lookup"><span data-stu-id="7966c-245">Administrator mode is only required for publishing when you're publishing to IIS on the local computer.</span></span>

### <a name="create-the-publish-profile"></a><span data-ttu-id="7966c-246">建立發行設定檔</span><span class="sxs-lookup"><span data-stu-id="7966c-246">Create the publish profile</span></span>

1. <span data-ttu-id="7966c-247">在**方案總管**中，以滑鼠右鍵按一下**ContosoUniversity**專案（而非**ContosoUniversity**專案）。</span><span class="sxs-lookup"><span data-stu-id="7966c-247">In **Solution Explorer**, right-click the **ContosoUniversity** project (not the **ContosoUniversity.DAL** project).</span></span> <span data-ttu-id="7966c-248">選取 [發行]。</span><span class="sxs-lookup"><span data-stu-id="7966c-248">Select **Publish**.</span></span> <span data-ttu-id="7966c-249">[**發行**] 頁面隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7966c-249">The **Publish** page appears.</span></span>

2. <span data-ttu-id="7966c-250">選取 [**新增設定檔**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-250">Select **New Profile**.</span></span> <span data-ttu-id="7966c-251">[**挑選發行目標**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7966c-251">The **Pick a publish target** dialog box appears.</span></span>

3. <span data-ttu-id="7966c-252">選取 [ **IIS]、[FTP] 等等**。選取 [建立設定檔]。</span><span class="sxs-lookup"><span data-stu-id="7966c-252">Select **IIS, FTP, etc**. Select **Create Profile**.</span></span> <span data-ttu-id="7966c-253">[**發行**嚮導] 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="7966c-253">The **Publish** wizard appears.</span></span>

   ![[發行 Web wizard 設定檔] 索引標籤](deploying-to-iis/_static/image26.png)

4. <span data-ttu-id="7966c-255">從 [**發行方法**] 下拉式功能表中，選取 [ **Web Deploy**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-255">From the **Publish method** drop-down menu, select **Web Deploy**.</span></span>

5. <span data-ttu-id="7966c-256">針對 [**伺服器**]，輸入*localhost*。</span><span class="sxs-lookup"><span data-stu-id="7966c-256">For **Server**, enter *localhost*.</span></span>

6. <span data-ttu-id="7966c-257">在 [**網站名稱**] 中，輸入*Default Web Site/ContosoUniversity*。</span><span class="sxs-lookup"><span data-stu-id="7966c-257">For **Site name**, enter *Default Web Site/ContosoUniversity*.</span></span>

7. <span data-ttu-id="7966c-258">針對 [**目的地 URL**] *http://localhost/ContosoUniversity* ，輸入。</span><span class="sxs-lookup"><span data-stu-id="7966c-258">For **Destination URL**, enter *http://localhost/ContosoUniversity*.</span></span>

   <span data-ttu-id="7966c-259">不需要 [**目的地 URL** ] 設定。</span><span class="sxs-lookup"><span data-stu-id="7966c-259">The **Destination URL** setting isn't required.</span></span> <span data-ttu-id="7966c-260">當 Visual Studio 完成部署應用程式時，它會自動開啟此 URL 的預設瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="7966c-260">When Visual Studio finishes deploying the application, it automatically opens your default browser to this URL.</span></span> <span data-ttu-id="7966c-261">如果您不想要在部署後自動開啟瀏覽器，請將此方塊保留空白。</span><span class="sxs-lookup"><span data-stu-id="7966c-261">If you don't want the browser to open automatically after deployment, leave this box blank.</span></span>

8. <span data-ttu-id="7966c-262">選取 [**驗證連接**]，確認設定正確，而且您可以連接到本機電腦上的 IIS。</span><span class="sxs-lookup"><span data-stu-id="7966c-262">Select **Validate Connection** to verify that the settings are correct and you can connect to IIS on the local computer.</span></span>

   <span data-ttu-id="7966c-263">綠色核取記號會確認連接是否成功。</span><span class="sxs-lookup"><span data-stu-id="7966c-263">A green check mark verifies that the connection is successful.</span></span>

   ![[發佈 Web wizard 連接] 索引標籤](deploying-to-iis/_static/image27.png)

9. <span data-ttu-id="7966c-265">選取 **[下一步**] 前進至 [**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="7966c-265">Select **Next** to advance to the **Settings** tab.</span></span>

10. <span data-ttu-id="7966c-266">[設定] 下拉式方塊會指定要**部署的組建**設定。</span><span class="sxs-lookup"><span data-stu-id="7966c-266">The **Configuration** drop-down box specifies the build configuration to deploy.</span></span> <span data-ttu-id="7966c-267">將它設定為預設值 [**發行**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-267">Leave it set to the default value of **Release**.</span></span> <span data-ttu-id="7966c-268">在本教學課程中，您將不會部署 Debug build。</span><span class="sxs-lookup"><span data-stu-id="7966c-268">You won't be deploying Debug builds in this tutorial.</span></span>

11. <span data-ttu-id="7966c-269">展開 [檔案] [**發行選項**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-269">Expand **File Publish Options**.</span></span> <span data-ttu-id="7966c-270">**從 [應用程式\_資料] 資料夾中選取 [排除**檔案]。</span><span class="sxs-lookup"><span data-stu-id="7966c-270">Select **Exclude files from the App\_Data folder**.</span></span>

    <span data-ttu-id="7966c-271">在測試環境中，應用程式會存取您在本機 SQL Server Express 實例中建立的資料庫，而不是 *\_應用程式 Data*資料夾中的 .mdf 檔案。</span><span class="sxs-lookup"><span data-stu-id="7966c-271">In the test environment, the application accesses the databases that you created in the local SQL Server Express instance, not the .mdf files in the *App\_Data* folder.</span></span>

12. <span data-ttu-id="7966c-272">在 [**發行**及**移除目的地的其他**檔案] 核取方塊中，保留預先編譯的狀態。</span><span class="sxs-lookup"><span data-stu-id="7966c-272">Leave the **Precompile during publishing** and **Remove additional files at destination** check boxes cleared.</span></span>

    ![[設定] 索引標籤中的檔案發佈選項](deploying-to-iis/_static/image15a.png)

    <span data-ttu-id="7966c-274">先行編譯是適用于大型網站的選項。</span><span class="sxs-lookup"><span data-stu-id="7966c-274">Precompiling is an option that is useful mainly for large sites.</span></span> <span data-ttu-id="7966c-275">在網站發佈之後，第一次要求頁面時，它可以減少啟動時間。</span><span class="sxs-lookup"><span data-stu-id="7966c-275">It can reduce startup time the first time a page is requested after the site is published.</span></span>

    <span data-ttu-id="7966c-276">您不需要移除其他檔案，因為這是您的第一個部署，而且目的地資料夾中還沒有任何檔案。</span><span class="sxs-lookup"><span data-stu-id="7966c-276">You don't need to remove additional files since this is your first deployment and there won't be any files in the destination folder yet.</span></span>

    > [!NOTE] 
    > <span data-ttu-id="7966c-277">如果您選取 [**移除目的地的其他**檔案] 以進行後續部署到相同的網站，請確定您使用的是預覽功能，如此一來，您就會事先看到哪些檔案將在部署之前刪除。</span><span class="sxs-lookup"><span data-stu-id="7966c-277">If you select **Remove additional files at destination** for a subsequent deployment to the same site, make sure that you use the preview feature so that you see in advance which files will be deleted before you deploy.</span></span> <span data-ttu-id="7966c-278">預期的行為是 Web Deploy 會刪除您在專案中已刪除之目的地伺服器上的檔案。</span><span class="sxs-lookup"><span data-stu-id="7966c-278">The expected behavior is that Web Deploy will delete files on the destination server that you have deleted in your project.</span></span> <span data-ttu-id="7966c-279">不過，會比較來源和目的地資料夾下的整個資料夾結構。而在某些情況下，Web Deploy 可能會刪除您不想要刪除的檔案。</span><span class="sxs-lookup"><span data-stu-id="7966c-279">However, the entire folder structure under the source and destination folders is compared; and in some scenarios, Web Deploy might delete files you don't want to delete.</span></span>
    > 
    > <span data-ttu-id="7966c-280">例如，如果您在伺服器上的子資料夾中有 web 應用程式，當您將專案部署至根資料夾時，將會刪除子資料夾。</span><span class="sxs-lookup"><span data-stu-id="7966c-280">For example if you have a web application in a subfolder on the server when you deploy a project to the root folder, the subfolder will be deleted.</span></span> <span data-ttu-id="7966c-281">您在 contoso.com 的主要網站可能會有一個專案，而 contoso.com/blog 的另一個專案則適用于 blog。</span><span class="sxs-lookup"><span data-stu-id="7966c-281">You might have one project for the main site at contoso.com and another project for a blog at contoso.com/blog.</span></span> <span data-ttu-id="7966c-282">Blog 應用程式位於子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="7966c-282">The blog application is in a subfolder.</span></span> <span data-ttu-id="7966c-283">如果您在部署主要網站時選取 [**移除目的地的其他**檔案]，則會刪除 blog 應用程式。</span><span class="sxs-lookup"><span data-stu-id="7966c-283">If you select **Remove additional files at destination** when you deploy the main site, the blog application will be deleted.</span></span>
    > 
    > <span data-ttu-id="7966c-284">若是另一個範例，您\_的應用程式資料檔案夾可能會意外刪除。</span><span class="sxs-lookup"><span data-stu-id="7966c-284">For another example, your App\_Data folder might get deleted unexpectedly.</span></span> <span data-ttu-id="7966c-285">某些資料庫（例如 SQL Server Compact 會將資料庫檔案儲存在\_App Data 資料夾中）。</span><span class="sxs-lookup"><span data-stu-id="7966c-285">Certain databases such as SQL Server Compact store database files in the App\_Data folder.</span></span> <span data-ttu-id="7966c-286">在初始部署之後，您不想要在後續部署中繼續複製資料庫檔案，因此您可以選取 [封裝/發行 Web] 索引標籤上的 [**排除應用程式\_資料**]。執行此動作之後，如果您已選取 [**移除目的地的其他**檔案]，則下次發行\_時，將會刪除您的資料庫檔案和應用程式資料檔案夾本身。</span><span class="sxs-lookup"><span data-stu-id="7966c-286">After the initial deployment, you don't want to keep copying the database files in subsequent deployments, so you select  **Exclude App\_Data** on the Package/Publish Web tab. After you do that if you have **Remove additional files at destination** selected, your database files and the App\_Data folder itself will be deleted the next time you publish.</span></span>

### <a name="configure-deployment-for-the-membership-database"></a><span data-ttu-id="7966c-287">設定成員資格資料庫的部署</span><span class="sxs-lookup"><span data-stu-id="7966c-287">Configure deployment for the membership database</span></span>

<span data-ttu-id="7966c-288">下列步驟適用于對話方塊的 [**資料庫**] 區段中的**DefaultConnection**資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-288">The following steps apply to the **DefaultConnection** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="7966c-289">在 [**遠端連線字串**] 方塊中，輸入指向新 SQL Server Express 成員資格資料庫的下列連接字串。</span><span class="sxs-lookup"><span data-stu-id="7966c-289">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express membership database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   <span data-ttu-id="7966c-290">部署程式會將此連接字串放在已部署的 Web.config 檔案中，因為已選取 [**在執行時間使用此連接字串**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-290">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

    <span data-ttu-id="7966c-291">您也可以從**伺服器總管**取得連接字串。</span><span class="sxs-lookup"><span data-stu-id="7966c-291">You can also get the connection string from **Server Explorer**.</span></span> <span data-ttu-id="7966c-292">在**伺服器總管**中，展開 [**資料連線**]  **&lt;並&gt;選取 machinename \sqlexpress.aspnet-ContosoUniversity**資料庫，然後從 [**屬性**] 視窗複製**連接字串**值。</span><span class="sxs-lookup"><span data-stu-id="7966c-292">In **Server Explorer**, expand **Data Connections** and select the **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity** database, then from the **Properties** window copy the **Connection String** value.</span></span> <span data-ttu-id="7966c-293">該連接字串將會有一個您可以刪除的額外設定`Pooling=False`：。</span><span class="sxs-lookup"><span data-stu-id="7966c-293">That connection string will have one additional setting that you can delete: `Pooling=False`.</span></span>

2. <span data-ttu-id="7966c-294">選取 [**更新資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-294">Select **Update database**.</span></span>

   <span data-ttu-id="7966c-295">這會導致在部署期間，于目的地資料庫中建立資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="7966c-295">This causes the database schema to be created in the destination database during deployment.</span></span> <span data-ttu-id="7966c-296">在接下來的步驟中，您會指定需要執行的其他腳本：一個用來授與資料庫存取權給預設的應用程式集區，另一個則用來部署資料。</span><span class="sxs-lookup"><span data-stu-id="7966c-296">In next steps, you specify the additional scripts that you need to run: one to grant database access to the default application pool and one to deploy data.</span></span>

3. <span data-ttu-id="7966c-297">選取 [**設定資料庫更新**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-297">Select **Configure database updates**.</span></span>
 
4. <span data-ttu-id="7966c-298">在 [**設定資料庫更新**] 對話方塊中，選取 [**加入 SQL 腳本**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-298">In the **Configure Database Updates** dialog box, select **Add SQL Script**.</span></span> <span data-ttu-id="7966c-299">流覽至您稍早在 [方案] 資料夾中儲存的*Grant. sql*腳本。</span><span class="sxs-lookup"><span data-stu-id="7966c-299">Navigate to the *Grant.sql* script that you saved earlier in the solution folder.</span></span>

5. <span data-ttu-id="7966c-300">重複此程式以新增*aspnet-data-dev*腳本。</span><span class="sxs-lookup"><span data-stu-id="7966c-300">Repeat the process to add the *aspnet-data-dev.sql* script.</span></span>

   ![設定成員資格資料庫的資料庫更新](deploying-to-iis/_static/image16.png)

6. <span data-ttu-id="7966c-302">選取 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="7966c-302">Select **Close**.</span></span>

### <a name="configure-deployment-for-the-application-database"></a><span data-ttu-id="7966c-303">設定應用程式資料庫的部署</span><span class="sxs-lookup"><span data-stu-id="7966c-303">Configure deployment for the application database</span></span>

<span data-ttu-id="7966c-304">當 Visual Studio 偵測到 Entity Framework `DbContext`類別時，它會在 [**資料庫**] 區段中建立具有 [**執行 Code First 移轉**] 核取方塊的專案，而不是 [**更新資料庫**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7966c-304">When Visual Studio detects an Entity Framework `DbContext` class, it creates an entry in the **Databases** section that has an **Execute Code First Migrations** check box instead of an **Update Database** check box.</span></span> <span data-ttu-id="7966c-305">在本教學課程中，您將使用該核取方塊來指定 Code First 移轉部署。</span><span class="sxs-lookup"><span data-stu-id="7966c-305">For this tutorial, you'll use that check box to specify Code First Migrations deployment.</span></span>

<span data-ttu-id="7966c-306">在某些情況下，您可能會使用`DbContext`資料庫，但是您想要使用 dbDacFx 提供者而不是遷移來部署資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-306">In some scenarios, you might be using a `DbContext` database but you want to use the dbDacFx provider instead of Migrations to deploy the database.</span></span> <span data-ttu-id="7966c-307">在此情況下，請參閱 MSDN 上的 ASP.NET Web 部署常見問題中的[如何? 部署 Code First 資料庫而不進行遷移？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 。</span><span class="sxs-lookup"><span data-stu-id="7966c-307">In that case, see [How do I deploy a Code First database without Migrations?](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) in the ASP.NET Web Deployment FAQ on MSDN.</span></span>

<span data-ttu-id="7966c-308">下列步驟適用于對話方塊的 [**資料庫**] 區段中的**SchoolCoNtext**資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-308">The following steps apply to the **SchoolContext** database in the dialog box's **Databases** section.</span></span>

1. <span data-ttu-id="7966c-309">在 [**遠端連線字串**] 方塊中，輸入指向新 SQL Server Express 應用程式資料庫的下列連接字串。</span><span class="sxs-lookup"><span data-stu-id="7966c-309">In the **Remote connection string** box, enter the following connection string that points to the new SQL Server Express application database.</span></span>

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   <span data-ttu-id="7966c-310">部署程式會將此連接字串放在已部署的 Web.config 檔案中，因為已選取 [**在執行時間使用此連接字串**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-310">The deployment process puts this connection string in the deployed Web.config file because **Use this connection string at runtime** is selected.</span></span>

   <span data-ttu-id="7966c-311">您也可以利用取得成員資格資料庫連接字串的相同方式，從**伺服器總管**取得應用程式資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="7966c-311">You can also get the application database connection string from **Server Explorer** in the same way you got the membership database connection string.</span></span>

2. <span data-ttu-id="7966c-312">選取**執行 Code First 移轉（在應用程式啟動時執行）** 。</span><span class="sxs-lookup"><span data-stu-id="7966c-312">Select **Execute Code First Migrations (runs on application start)**.</span></span>

   <span data-ttu-id="7966c-313">此選項會讓部署程式`MigrateDatabaseToLatestVersion`設定已部署的 web.config 檔案，以指定初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="7966c-313">This option causes the deployment process to configure the deployed Web.config file to specify the `MigrateDatabaseToLatestVersion` initializer.</span></span> <span data-ttu-id="7966c-314">當應用程式在部署後第一次存取資料庫時，這個初始化運算式會自動將資料庫更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="7966c-314">This initializer automatically updates the database to the latest version when the application accesses the database for the first time after deployment.</span></span>

### <a name="configure-publish-profile-transforms"></a><span data-ttu-id="7966c-315">設定發行設定檔轉換</span><span class="sxs-lookup"><span data-stu-id="7966c-315">Configure publish profile transforms</span></span>

1. <span data-ttu-id="7966c-316">選取 [關閉]。</span><span class="sxs-lookup"><span data-stu-id="7966c-316">Select **Close**.</span></span> <span data-ttu-id="7966c-317">當系統詢問您是否要儲存變更時，請選取 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="7966c-317">Select **Yes** when you are asked if you want to save changes.</span></span>

2. <span data-ttu-id="7966c-318">在**方案總管**中，依序展開 [**屬性**] 和 [ **PublishProfiles**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-318">In **Solution Explorer**, expand **Properties**, expand **PublishProfiles**.</span></span>

3. <span data-ttu-id="7966c-319">以滑鼠右鍵按一下*CustomProfile .pubxml* ，然後將它重新命名為 *.pubxml*。</span><span class="sxs-lookup"><span data-stu-id="7966c-319">Right-click *CustomProfile.pubxml* and rename it *Test.pubxml*.</span></span>

4. <span data-ttu-id="7966c-320">以滑鼠右鍵按一下 [ *.pubxml*]。</span><span class="sxs-lookup"><span data-stu-id="7966c-320">Right-click *Test.pubxml*.</span></span> <span data-ttu-id="7966c-321">選取 [**新增設定轉換**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-321">Select **Add Config Transform**.</span></span>

   ![[新增設定轉換] 功能表](deploying-to-iis/_static/image17.png)

   <span data-ttu-id="7966c-323">Visual Studio 建立 web.config*轉換檔案*並開啟它。</span><span class="sxs-lookup"><span data-stu-id="7966c-323">Visual Studio creates the *Web.Test.config* transform file and opens it.</span></span>

5. <span data-ttu-id="7966c-324">*在 web.config 轉換檔案*中，將下列程式碼插入緊接在開啟設定標記之後。</span><span class="sxs-lookup"><span data-stu-id="7966c-324">In the *Web.Test.config* transform file, insert the following code immediately after the opening configuration tag.</span></span>

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    <span data-ttu-id="7966c-325">當您使用測試發行設定檔時，這種轉換會將環境指標設定為「測試」。</span><span class="sxs-lookup"><span data-stu-id="7966c-325">When you use the Test publish profile, this transform sets the environment indicator to "Test".</span></span> <span data-ttu-id="7966c-326">在部署的網站中，您會在 "Contoso 大學" H1 標題之後看到 "（Test）"。</span><span class="sxs-lookup"><span data-stu-id="7966c-326">In the deployed site, you'll see "(Test)" after the "Contoso University" H1 heading.</span></span>

6. <span data-ttu-id="7966c-327">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="7966c-327">Save and close the file.</span></span>

7. <span data-ttu-id="7966c-328">以滑鼠右鍵按一下*web.config*檔案，然後選取 [**預覽轉換**]，以確定您編碼的轉換會產生預期的變更。</span><span class="sxs-lookup"><span data-stu-id="7966c-328">Right-click the *Web.Test.config* file and select **Preview Transform** to make sure that the transform you coded produces the expected changes.</span></span>

    <span data-ttu-id="7966c-329">[Web.config**預覽**] 視窗會顯示套用*web.config* *轉換和 web.config 轉換時*所產生的結果。</span><span class="sxs-lookup"><span data-stu-id="7966c-329">The **Web.config Preview** window shows the result of applying both the *Web.Release.config* transforms and the *Web.Test.config* transforms.</span></span>

### <a name="preview-the-deployment-updates"></a><span data-ttu-id="7966c-330">預覽部署更新</span><span class="sxs-lookup"><span data-stu-id="7966c-330">Preview the deployment updates</span></span>

1. <span data-ttu-id="7966c-331">再次開啟 [**發行 Web** wizard] （以滑鼠右鍵按一下 ContosoUniversity 專案，然後依序選取 [**發佈**] 和 [**預覽**]）。</span><span class="sxs-lookup"><span data-stu-id="7966c-331">Open the **Publish Web** wizard again (right-click the ContosoUniversity project, select **Publish**, then **Preview**).</span></span>

2. <span data-ttu-id="7966c-332">在 [**預覽**] 對話方塊中，選取 [**開始預覽**] 以查看將複製的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="7966c-332">In the **Preview** dialog box, select **Start Preview** to see a list of the files that will be copied.</span></span> 

   ![發行預覽](deploying-to-iis/_static/image29.png)

   <span data-ttu-id="7966c-334">您也可以選取 [**預覽資料庫**] 連結，以查看將在成員資格資料庫中執行的腳本。</span><span class="sxs-lookup"><span data-stu-id="7966c-334">You can also select the **Preview database** link to see the scripts that will run in the membership database.</span></span> <span data-ttu-id="7966c-335">（不會針對 Code First 移轉部署執行任何腳本，因此不會為應用程式資料庫預覽任何內容）。</span><span class="sxs-lookup"><span data-stu-id="7966c-335">(No scripts are run for Code First Migrations deployment, so there's nothing to preview for the application database.)</span></span>

3. <span data-ttu-id="7966c-336">選取 [發行]。</span><span class="sxs-lookup"><span data-stu-id="7966c-336">Select **Publish**.</span></span>

   <span data-ttu-id="7966c-337">如果 Visual Studio 不是在系統管理員模式中，您可能會收到許可權錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="7966c-337">If Visual Studio is not in administrator mode, you might get a permissions error message.</span></span> <span data-ttu-id="7966c-338">在此情況下，請關閉 Visual Studio，在系統管理員模式中開啟它，然後再次嘗試發佈。</span><span class="sxs-lookup"><span data-stu-id="7966c-338">In that case, close Visual Studio, open it in administrator mode, and try to publish again.</span></span>

   <span data-ttu-id="7966c-339">如果 Visual Studio 處於系統管理員模式，[**輸出**] 視窗會報告 [成功的組建] 和 [發行]。</span><span class="sxs-lookup"><span data-stu-id="7966c-339">If Visual Studio is in administrator mode, the **Output** window reports successful build and publish.</span></span>

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   <span data-ttu-id="7966c-341">如果您在 [**發行設定檔**連線] 索引標籤的 [**目的地 URL** ] 方塊中輸入 URL，瀏覽器會自動開啟至您電腦上的 IIS 中執行的 Contoso 大學首頁。</span><span class="sxs-lookup"><span data-stu-id="7966c-341">If you entered the URL in the **Destination URL** box on the publish profile **Connection** tab, the browser automatically opens to the Contoso University Home page running in IIS on your computer.</span></span>

## <a name="test-in-the-test-environment"></a><span data-ttu-id="7966c-342">在測試環境中測試</span><span class="sxs-lookup"><span data-stu-id="7966c-342">Test in the test environment</span></span>

<span data-ttu-id="7966c-343">請注意，環境指標會顯示「（測試）」而不是「（Dev）」，這表示環境指標的*web.config 轉換成功*。</span><span class="sxs-lookup"><span data-stu-id="7966c-343">Notice that the environment indicator shows "(Test)" instead of "(Dev)," which shows that the *Web.config* transformation for the environment indicator was successful.</span></span>

<span data-ttu-id="7966c-344">執行 [**講師**] 頁面，確認 Code First 以講師資料植入資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-344">Run the **Instructors** page to verify that Code First seeded the database with instructor data.</span></span> <span data-ttu-id="7966c-345">當您選取此頁面時，可能需要幾分鐘的時間才能載入，因為 Code First 會建立資料庫，然後`Seed`執行方法。</span><span class="sxs-lookup"><span data-stu-id="7966c-345">When you select this page, it may take a few minutes to load because Code First creates the database and then runs the `Seed` method.</span></span> <span data-ttu-id="7966c-346">（因為應用程式尚未嘗試存取資料庫，所以不會在首頁上這麼做。）</span><span class="sxs-lookup"><span data-stu-id="7966c-346">(It didn't do that when you were on the home page because the application didn't try to access the database yet.)</span></span>

<span data-ttu-id="7966c-347">選取 [**學生**] 索引標籤，確認已部署的資料庫沒有任何學生。</span><span class="sxs-lookup"><span data-stu-id="7966c-347">Select the **Students** tab to verify that the deployed database has no students.</span></span>

<span data-ttu-id="7966c-348">從 [**學生**] 功能表中選取 [**新增學生**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-348">Select **Add Students** from the **Students** menu.</span></span> <span data-ttu-id="7966c-349">新增學生，然後在 [**學生**] 頁面中查看新學生。</span><span class="sxs-lookup"><span data-stu-id="7966c-349">Add a student, and then view the new student in the **Students** page.</span></span> <span data-ttu-id="7966c-350">這會驗證您是否可以成功寫入資料庫。</span><span class="sxs-lookup"><span data-stu-id="7966c-350">This verifies that you can successfully write to the database.</span></span>

<span data-ttu-id="7966c-351">從 [**課程**] 功能表中，選取 [**更新信用額度**]。</span><span class="sxs-lookup"><span data-stu-id="7966c-351">From the **Courses** menu, select **Update Credits**.</span></span> <span data-ttu-id="7966c-352">[**更新信用額度**] 頁面需要系統管理員許可權，因此會顯示 [**登入**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="7966c-352">The **Update Credits** page requires administrator permissions, so the **Log In** page is displayed.</span></span> <span data-ttu-id="7966c-353">輸入您稍早建立的系統管理員帳號憑證（"admin" 和 "devpwd"）。</span><span class="sxs-lookup"><span data-stu-id="7966c-353">Enter the administrator account credentials that you created earlier ("admin" and "devpwd").</span></span> <span data-ttu-id="7966c-354">[**更新信用額度**] 頁面隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="7966c-354">The **Update Credits** page is displayed.</span></span> <span data-ttu-id="7966c-355">這會確認您在上一個教學課程中建立的系統管理員帳戶已正確部署到測試環境。</span><span class="sxs-lookup"><span data-stu-id="7966c-355">This verifies that the administrator account that you created in the previous tutorial was correctly deployed to the test environment.</span></span>

<span data-ttu-id="7966c-356">確認*c:\inetpub\wwwroot\ContosoUniversity*資料夾中有一個只有預留位置檔案的*ELMAH*資料夾。</span><span class="sxs-lookup"><span data-stu-id="7966c-356">Verify that an *ELMAH* folder exists in the *c:\inetpub\wwwroot\ContosoUniversity* folder with only the placeholder file in it.</span></span>

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a><span data-ttu-id="7966c-357">檢查 Code First 移轉的自動 web.config 變更</span><span class="sxs-lookup"><span data-stu-id="7966c-357">Review the automatic Web.config changes for Code First Migrations</span></span>

<span data-ttu-id="7966c-358">在*C:\inetpub\wwwroot\ContosoUniversity*的已部署應用程式中開啟*web.config*檔案，您可以看到部署程式設定 Code First 移轉自動將資料庫更新為最新版本。</span><span class="sxs-lookup"><span data-stu-id="7966c-358">Open the *Web.config* file in the deployed application at *C:\inetpub\wwwroot\ContosoUniversity* and you can see where the deployment process configured Code First Migrations to automatically update the database to the latest version.</span></span>

![](deploying-to-iis/_static/image21.png)

<span data-ttu-id="7966c-359">部署程式也會為 Code First 移轉建立新的連接字串，以獨佔用來更新資料庫架構：</span><span class="sxs-lookup"><span data-stu-id="7966c-359">The deployment process also created a new connection string for Code First Migrations to use exclusively for updating the database schema:</span></span>

![Database_Publish 連接字串](deploying-to-iis/_static/image22.png)

<span data-ttu-id="7966c-361">這個額外的連接字串可讓您指定資料庫架構更新的一個使用者帳戶，以及不同的使用者帳戶來存取應用程式資料。</span><span class="sxs-lookup"><span data-stu-id="7966c-361">This additional connection string enables you to specify one user account for database schema updates and a different user account for application data access.</span></span> <span data-ttu-id="7966c-362">例如，您可以將**資料庫\_擁有**者角色指派 **\_** 給 Code First 移轉，並將 db datareader 與**db\_資料寫入元**角色指派給應用程式。</span><span class="sxs-lookup"><span data-stu-id="7966c-362">For example, you could assign the **db\_owner** role to Code First Migrations and **db\_datareader** with **db\_datawriter** roles to the application.</span></span> <span data-ttu-id="7966c-363">這是常見的深度防禦模式，可防止應用程式中可能的惡意程式碼變更資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="7966c-363">This is a common defense-in-depth pattern that prevents potentially malicious code in the application from changing the database schema.</span></span> <span data-ttu-id="7966c-364">（例如，這可能會發生在成功的 SQL 插入式攻擊中）。這些教學課程不會使用此模式。</span><span class="sxs-lookup"><span data-stu-id="7966c-364">(For example, this might happen in a successful SQL injection attack.) These tutorials don't use this pattern.</span></span> <span data-ttu-id="7966c-365">若要在您的案例中執行此模式，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="7966c-365">To implement this pattern in your scenario, take these steps:</span></span>

1. <span data-ttu-id="7966c-366">在 [**發行 Web** wizard] 的 [**設定**] 索引標籤下，輸入指定具有完整資料庫架構更新許可權之使用者的連接字串。</span><span class="sxs-lookup"><span data-stu-id="7966c-366">In the **Publish Web** wizard under the **Settings** tab, enter the connection string that specifies a user with full database schema update permissions.</span></span> <span data-ttu-id="7966c-367">清除 [**在執行時間使用此連接字串**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="7966c-367">Clear the **Use this connection string at runtime** check box.</span></span> <span data-ttu-id="7966c-368">在已部署的 web.config 檔案中，這會變成`DatabasePublish`連接字串。</span><span class="sxs-lookup"><span data-stu-id="7966c-368">In the deployed Web.config file, this becomes the `DatabasePublish` connection string.</span></span>

2. <span data-ttu-id="7966c-369">針對您希望應用程式在執行時間使用的連接字串，建立 Web.config 檔案轉換。</span><span class="sxs-lookup"><span data-stu-id="7966c-369">Create a Web.config file transformation for the connection string that you want the application to use at run time.</span></span>

## <a name="summary"></a><span data-ttu-id="7966c-370">總結</span><span class="sxs-lookup"><span data-stu-id="7966c-370">Summary</span></span>

<span data-ttu-id="7966c-371">您現在已將應用程式部署至開發電腦上的 IIS，並在該處進行測試。</span><span class="sxs-lookup"><span data-stu-id="7966c-371">You've now deployed your application to IIS on your development computer and tested it there.</span></span>

![測試中的首頁](deploying-to-iis/_static/image23.png)

<span data-ttu-id="7966c-373">這會驗證部署程式是否已將應用程式的內容複寫到正確的位置（不包括您不想要部署的檔案），以及在部署期間，Web Deploy 正確設定 IIS。</span><span class="sxs-lookup"><span data-stu-id="7966c-373">This verifies that the deployment process copied the application's content to the right location (excluding the files that you did not want to deploy) and also that Web Deploy configured IIS correctly during deployment.</span></span> <span data-ttu-id="7966c-374">在下一個教學課程中，您將執行一項測試，尋找尚未完成的部署工作：在 [*榆樹 ah* ] 資料夾上設定資料夾許可權。</span><span class="sxs-lookup"><span data-stu-id="7966c-374">In the next tutorial, you'll run one more test that finds a deployment task that has not yet been done: setting folder permissions on the *Elm ah* folder.</span></span>

## <a name="more-information"></a><span data-ttu-id="7966c-375">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="7966c-375">More information</span></span>

<span data-ttu-id="7966c-376">如需在 Visual Studio 中執行 IIS 或 IIS Express 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="7966c-376">For information about running IIS or IIS Express in Visual Studio, see the following resources:</span></span>

- <span data-ttu-id="7966c-377">[IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 網站上的總覽。</span><span class="sxs-lookup"><span data-stu-id="7966c-377">[IIS Express Overview](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) on the IIS.net site.</span></span>
- <span data-ttu-id="7966c-378">[簡介 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie 的 blog。</span><span class="sxs-lookup"><span data-stu-id="7966c-378">[Introducing IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) on Scott Guthrie's blog.</span></span>
- <span data-ttu-id="7966c-379">[Visual Studio 中用於 ASP.NET Web 專案的 Web 服務器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7966c-379">[Web Servers in Visual Studio for ASP.NET Web Projects](https://msdn.microsoft.com/library/58wxa9w5.aspx).</span></span>
- <span data-ttu-id="7966c-380">[IIS 與 ASP.NET 網站上的 ASP.NET 程式開發伺服器之間的核心差異](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。</span><span class="sxs-lookup"><span data-stu-id="7966c-380">[Core Differences Between IIS and the ASP.NET Development Server](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md) on the ASP.NET site.</span></span>

<span data-ttu-id="7966c-381">如需在您的應用程式以中度信任執行時可能會發生哪些問題的詳細資訊，請參閱 Rolla 網站的四位專家的[中級信任中的 ASP.NET 應用程式裝載](http://www.4guysfromrolla.com/articles/100307-1.aspx)。</span><span class="sxs-lookup"><span data-stu-id="7966c-381">For information about what issues might arise when your application runs in medium trust, see [Hosting ASP.NET Applications in Medium Trust](http://www.4guysfromrolla.com/articles/100307-1.aspx) on the four Guys from Rolla site.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="7966c-382">[上一頁](project-properties.md)
> [下一頁](setting-folder-permissions.md)</span><span class="sxs-lookup"><span data-stu-id="7966c-382">[Previous](project-properties.md)
[Next](setting-folder-permissions.md)</span></span>
