---
uid: whitepapers/side-by-side-with-10
title: ASP.NET .NET Framework 1.0 和1.1 的並存執行 |Microsoft Docs
author: rick-anderson
description: 本白皮書說明如何在您的電腦上安裝 .NET 1.0 和 .NET 1.1，讓 ASP.NET Web 應用程式可在任一版本的 fram 上執行 。
ms.author: riande
ms.date: 02/10/2010
ms.assetid: bdea2003-e964-4db5-9092-d56cc7560616
msc.legacyurl: /whitepapers/side-by-side-with-10
msc.type: content
ms.openlocfilehash: c123545099013af71569bce4707f2b3eb732c344
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78632969"
---
# <a name="aspnet-side-by-side-execution-of-net-framework-10-and-11"></a><span data-ttu-id="94249-103">ASP.NET 並存執行 .NET Framework 1.0 與 1.1</span><span class="sxs-lookup"><span data-stu-id="94249-103">ASP.NET Side-by-Side Execution of .NET Framework 1.0 and 1.1</span></span>

> <span data-ttu-id="94249-104">本白皮書說明如何在您的電腦上安裝 .NET 1.0 和 .NET 1.1，讓 ASP.NET Web 應用程式可在任一版本的架構上執行。</span><span class="sxs-lookup"><span data-stu-id="94249-104">This whitepaper describes how to install both .NET 1.0 and .NET 1.1 on your machine, allowing an ASP.NET Web application to run on either version of the framework.</span></span>
> 
> <span data-ttu-id="94249-105">適用于 ASP.NET 1.0 和 ASP.NET 1.1。</span><span class="sxs-lookup"><span data-stu-id="94249-105">Applies to ASP.NET 1.0 and ASP.NET 1.1.</span></span>

<span data-ttu-id="94249-106">在 ASP.NET 中，當應用程式安裝在同一部電腦上，但使用不同版本的 .NET Framework 時，就會被視為並存執行。</span><span class="sxs-lookup"><span data-stu-id="94249-106">In ASP.NET, applications are said to be running side by side when they are installed on the same computer, but use different versions of the .NET Framework.</span></span> <span data-ttu-id="94249-107">下列主題說明如何設定 ASP.NET 應用程式以進行並存執行，並提供詳細的步驟來執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="94249-107">The following topic describes how to configure ASP.NET applications for side-by-side execution and provides detailed steps to:</span></span>

- [<span data-ttu-id="94249-108">在安裝期間維護 Web 應用程式與 .NET Framework 版本1.0 的對應</span><span class="sxs-lookup"><span data-stu-id="94249-108">Maintain your Web application's mapping to .NET Framework version 1.0 during installation</span></span>](#1)
- [<span data-ttu-id="94249-109">將 Web 應用程式對應至特定版本的 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="94249-109">Map a Web application to a specific version of the .NET Framework</span></span>](#2)
- [<span data-ttu-id="94249-110">找出網站所使用的 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="94249-110">Find the version of the .NET Framework that a Web site is using</span></span>](#3)

<span data-ttu-id="94249-111">傳統上，當元件或應用程式在電腦上更新時，會移除較舊的版本，並取代為較新的版本。</span><span class="sxs-lookup"><span data-stu-id="94249-111">Traditionally, when a component or application is updated on a computer, the older version is removed and replaced with the newer version.</span></span> <span data-ttu-id="94249-112">如果新版本與先前的版本不相容，這通常會中斷使用元件或應用程式的其他應用程式。</span><span class="sxs-lookup"><span data-stu-id="94249-112">If the new version is not compatible with the previous version, this usually breaks other applications that use the component or application.</span></span> <span data-ttu-id="94249-113">.NET Framework 提供並存執行的支援，允許在同一部電腦上同時安裝多個版本的元件或應用程式。</span><span class="sxs-lookup"><span data-stu-id="94249-113">The .NET Framework provides support for side-by-side execution, which allows multiple versions of an assembly or application to be installed on the same computer at the same time.</span></span> <span data-ttu-id="94249-114">因為可以同時安裝多個版本，所以受控應用程式可以選擇要使用的版本，而不會影響使用不同版本的應用程式。</span><span class="sxs-lookup"><span data-stu-id="94249-114">Because multiple versions can be installed simultaneously, managed applications can select which version to use without affecting applications that use a different version.</span></span>

<span data-ttu-id="94249-115">根據預設，在安裝 .NET Framework 版本1.1 期間，所有現有的 ASP.NET 應用程式都會自動重新設定為使用最新版本的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="94249-115">By default, during the installation of the .NET Framework version 1.1, all existing ASP.NET applications are automatically reconfigured to use the latest version of the .NET Framework.</span></span> <span data-ttu-id="94249-116">如果您不想讓 ASP.NET 應用程式預設為 .NET Framework 1.1，請按一下[這裡](#1)以瞭解如何在安裝期間避免這種情況。</span><span class="sxs-lookup"><span data-stu-id="94249-116">If you do not want your ASP.NET applications to default to .NET Framework 1.1, click [here](#1) to learn how to prevent this during installation.</span></span>

<span data-ttu-id="94249-117">如果您將 Web 服務器更新為 .NET Framework 1.1，而且想要在 .NET Framework 1.0 中執行一或多個 Web 應用程式，則需要更新 Internet Information Services （IIS）腳本對應。</span><span class="sxs-lookup"><span data-stu-id="94249-117">If you update your Web server to .NET Framework 1.1 and want one or more Web applications to run .NET Framework 1.0, you need to update the Internet Information Services (IIS) Script Map.</span></span> <span data-ttu-id="94249-118">腳本對應是將特定 Web 應用程式的 .aspx 副檔名對應至 .NET Framework 版本的機制。</span><span class="sxs-lookup"><span data-stu-id="94249-118">The script mapping is the mechanism to map the .aspx file extension for a specific Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="94249-119">按一下[這裡](#2)以瞭解如何將 Web 應用程式對應至特定版本的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="94249-119">Click [here](#2) to learn how to map a Web application to a specific version of the .NET Framework.</span></span>

<span data-ttu-id="94249-120">您可以使用 Internet Information manager 或 ASP.NET IIS 註冊工具（Aspnet\_regiis）來尋找哪個 .NET Framework 版本正在執行特定的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="94249-120">You can use the Internet Information Manger or the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe) to find which .NET Framework version is running a particular Web application.</span></span> <span data-ttu-id="94249-121">按一下[這裡](#3)以瞭解如何找出網站所使用的 .NET Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="94249-121">Click [here](#3) to learn how to find the version of the .NET Framework that a Web site is using.</span></span>

<span data-ttu-id="94249-122">遷移至 .NET Framework 1.1 時，一個匯入考慮是 .NET Framework 的每個版本都使用它自己的 Machine.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="94249-122">One import consideration when migrating to .NET Framework 1.1 is that each version of the .NET Framework uses its own Machine.config file.</span></span> <span data-ttu-id="94249-123">因此，如果 Web 管理員對 Machine.config 檔案進行了變更，這些變更就必須遷移到 .NET Framework 1.1 Machine.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="94249-123">As a result, if a Web administrator has made changes to the Machine.config file, those changes must be migrated to the .NET Framework 1.1 Machine.config file.</span></span>

<a id="1"></a>

## <a name="maintaining-your-web-applications-mapping-to-net-framework-10-during-installation"></a><span data-ttu-id="94249-124">在安裝期間維護 Web 應用程式與 .NET Framework 1.0 的對應</span><span class="sxs-lookup"><span data-stu-id="94249-124">Maintaining your Web application's mapping to .NET Framework 1.0 during installation</span></span>

<span data-ttu-id="94249-125">根據預設，所有現有的 ASP.NET 應用程式會在安裝期間自動重新設定，以使用較新版本的 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="94249-125">By default, all existing ASP.NET applications are automatically reconfigured during installation to use the newer version of the .NET Framework.</span></span> <span data-ttu-id="94249-126">使用較新版本的 .NET Framework，應用程式可以充分利用新版本中所包含的改良功能和新功能。</span><span class="sxs-lookup"><span data-stu-id="94249-126">Using the newer version of the .NET Framework, applications can take full advantage of improvements and new features included in the new release.</span></span> <span data-ttu-id="94249-127">同時，若 Web 管理員可能想要更精確地控制哪些應用程式已更新，則在安裝 .NET Framework 時，可能會導致無法自動重新對應所有現有的 ASP.NET 應用程式。</span><span class="sxs-lookup"><span data-stu-id="94249-127">At the same time, the Web administrator, who might want granular control over which applications are updated, can prevent the automatic remapping of all existing ASP.NET applications during installation of the .NET Framework.</span></span>

<span data-ttu-id="94249-128">為避免將整個 ASP.NET 應用程式自動重新對應到較新版本的 .NET Framework，Web 管理員可以使用/noaspupgrade 命令列選項搭配 Dotnetfx.exe 安裝程式。</span><span class="sxs-lookup"><span data-stu-id="94249-128">To prevent the automatic remapping of the entire ASP.NET application to the newer version of the .NET Framework, the Web administrator can use the /noaspupgrade command-line option with the Dotnetfx.exe setup program.</span></span>

<span data-ttu-id="94249-129">**防止 ASP.NET 應用程式重新對應到較新的版本**</span><span class="sxs-lookup"><span data-stu-id="94249-129">**To prevent total remapping of ASP.NET application to newer version**</span></span>

1. <span data-ttu-id="94249-130">移至 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="94249-130">Go to **Start**.</span></span>
2. <span data-ttu-id="94249-131">按一下 [**執行**]。</span><span class="sxs-lookup"><span data-stu-id="94249-131">Click on **run**.</span></span>
3. <span data-ttu-id="94249-132">輸入 **cmd**。</span><span class="sxs-lookup"><span data-stu-id="94249-132">Type **cmd**.</span></span>
4. <span data-ttu-id="94249-133">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="94249-133">Click **OK**.</span></span>  
  
    ![](side-by-side-with-10/_static/image1.gif)
5. <span data-ttu-id="94249-134">從命令提示字元輸入下列程式程式碼，以開始安裝 .NET Framework： **dotnetfx.exe/c： "install/noaspupgrade？"** 。</span><span class="sxs-lookup"><span data-stu-id="94249-134">From the command prompt, type the following line to start the installation of the .NET Framework: **Dotnetfx.exe /c:"install /noaspupgrade?**.</span></span>  
  
    ![](side-by-side-with-10/_static/image2.gif)
6. <span data-ttu-id="94249-135">在 Microsoft .NET Framework 1.1 安裝程式中按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="94249-135">Click **Yes** in the Microsoft .NET Framework 1.1 Setup.</span></span> <span data-ttu-id="94249-136">這會啟動 .NET Framework 1.1 的設定程式。</span><span class="sxs-lookup"><span data-stu-id="94249-136">This will start the setup process of the .NET Framework 1.1.</span></span>  
  
    ![](side-by-side-with-10/_static/image3.gif)

<a id="2"></a>

## <a name="map-a-web-application-to-a-specific-version-of-the-net-framework"></a><span data-ttu-id="94249-137">將 Web 應用程式對應至特定版本的 .NET Framework</span><span class="sxs-lookup"><span data-stu-id="94249-137">Map a Web application to a specific version of the .NET Framework</span></span>

<span data-ttu-id="94249-138">.NET Framework 的每個版本都包含一個版本的 ASP.NET IIS 註冊工具（Aspnet\_regiis）。</span><span class="sxs-lookup"><span data-stu-id="94249-138">Each version of the .NET Framework includes a version of the ASP.NET IIS Registration Tool (Aspnet\_regiis.exe).</span></span> <span data-ttu-id="94249-139">這項工具可讓系統管理員指定在特定版本的 .NET Framework 下執行 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="94249-139">This tool enables administrators to specify that a Web application be run under a particular version of the .NET Framework.</span></span> <span data-ttu-id="94249-140">這稱為將 Web 應用程式對應至 .NET Framework 的版本。</span><span class="sxs-lookup"><span data-stu-id="94249-140">This is referred to as mapping a Web application to a version of the .NET Framework.</span></span> <span data-ttu-id="94249-141">系統管理員必須選取對應至將與 Web 應用程式相關聯之 .NET Framework 版本的 Aspnet\_regiis。</span><span class="sxs-lookup"><span data-stu-id="94249-141">Administrators must select the Aspnet\_regiis.exe that corresponds to the version of the .NET Framework that will be associated with the Web application.</span></span> <span data-ttu-id="94249-142">例如，想要指定網站使用 .NET Framework 1.1 的系統管理員，必須使用 .NET Framework 1.1 隨附的 Aspnet\_regiis。</span><span class="sxs-lookup"><span data-stu-id="94249-142">For example, an administrator who wants to specify that a Web site use .NET Framework 1.1 must use the Aspnet\_regiis.exe that comes with .NET Framework 1.1.</span></span>

<span data-ttu-id="94249-143">1\.0 版的 Aspnet\_regiis 位於：</span><span class="sxs-lookup"><span data-stu-id="94249-143">The Aspnet\_regiis.exe for version 1.0 is located at:</span></span>

- <span data-ttu-id="94249-144">C:\WINDOWS\Microsoft.NET\Framework\\**v v1.0.3705**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="94249-144">C:\WINDOWS\Microsoft.NET\Framework\\**v1.0.3705**\aspnet\_regiis</span></span>

<span data-ttu-id="94249-145">第1版的 Aspnet\_regiis，1位於：</span><span class="sxs-lookup"><span data-stu-id="94249-145">The Aspnet\_regiis.exe for version 1,1 is located at:</span></span>

- <span data-ttu-id="94249-146">C:\WINDOWS\Microsoft.NET\Framework\\**v 1.1.4322**\aspnet\_regiis</span><span class="sxs-lookup"><span data-stu-id="94249-146">C:\WINDOWS\Microsoft.NET\Framework\\**v1.1.4322**\aspnet\_regiis</span></span>

<span data-ttu-id="94249-147">Aspnet\_regiis 提供兩個選項來對應 Web 應用程式的腳本：</span><span class="sxs-lookup"><span data-stu-id="94249-147">The Aspnet\_regiis.exe provides two options for script mapping a Web application:</span></span>

- <span data-ttu-id="94249-148">**-s**會在路徑和其子目錄中設定腳本對應。</span><span class="sxs-lookup"><span data-stu-id="94249-148">**-s** sets the script map in the path and in its child directories.</span></span>
- <span data-ttu-id="94249-149">**-sn**只會在路徑中設定腳本對應。</span><span class="sxs-lookup"><span data-stu-id="94249-149">**-sn** sets the script map in the path only.</span></span>

<span data-ttu-id="94249-150">路徑會定義 Web 應用程式 IIS 中繼資料路徑，其定義格式為 W3SVC/ROOT/{WebSiteNumber}/{應用程式\_名稱}。</span><span class="sxs-lookup"><span data-stu-id="94249-150">The path defines the Web application IIS metadata path, which is defined in the form of W3SVC/ROOT/{WebSiteNumber}/{Application\_Name}.</span></span> <span data-ttu-id="94249-151">例如，對於名為入口網站的 Web 應用程式，位於 [預設的網站] 底下，則元資料庫路徑為 W3SVC/1/ROOT/Portal。</span><span class="sxs-lookup"><span data-stu-id="94249-151">For example, for a Web application called Portal located under the default Web site, the metabase path is W3SVC/1/ROOT/Portal.</span></span>

![](side-by-side-with-10/_static/image4.gif)

<span data-ttu-id="94249-152">注意：您也可以使用稱為「元資料庫編輯器」的工具來取得元資料庫路徑。</span><span class="sxs-lookup"><span data-stu-id="94249-152">Note You can also use a tool called the Metabase Editor to get the metabase path.</span></span> <span data-ttu-id="94249-153">您可以從 Microsoft 支援服務網站下載此工具，網址為[https://support.microsoft.com/default.aspx?scid=kb; en-us; 232068。](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span><span class="sxs-lookup"><span data-stu-id="94249-153">You can download this tool from the Microsoft Support site at [https://support.microsoft.com/default.aspx?scid=kb;en-us;232068.](https://support.microsoft.com/default.aspx?scid=kb;en-us;232068)</span></span>

- <span data-ttu-id="94249-154">執行 Aspnet\_regiis-s W3SVC/1/ROOT/Portal，以更新入口網站 IIS 腳本對應和其 subapplication。</span><span class="sxs-lookup"><span data-stu-id="94249-154">Run Aspnet\_regiis.exe -s W3SVC/1/ROOT/Portal to update the portal IIS script map and its subapplication.</span></span>  
  
    ![](side-by-side-with-10/_static/image5.gif)

- <span data-ttu-id="94249-155">執行 Aspnet\_regiis，以更新入口網站 IIS 腳本對應，而不會影響入口網站子目錄中的應用程式。</span><span class="sxs-lookup"><span data-stu-id="94249-155">Run Aspnet\_regiis.exe -sn W3SVC/1/ROOT/Portal to update the portal IIS script map, without affecting applications in the portal?s subdirectories.</span></span>  
  
    ![](side-by-side-with-10/_static/image6.gif)

<a id="3"></a>

## <a name="find-the-net-framework-version-that-a-web-application-is-using"></a><span data-ttu-id="94249-156">尋找 Web 應用程式正在使用的 .NET Framework 版本</span><span class="sxs-lookup"><span data-stu-id="94249-156">Find the .NET Framework version that a Web application is using</span></span>

<span data-ttu-id="94249-157">系統管理員可以使用網際網路 Service Manager 來尋找哪個版本的 .NET Framework 會執行網站。</span><span class="sxs-lookup"><span data-stu-id="94249-157">An administrator can use the Internet Service Manager to find which version of the .NET Framework runs a Web site.</span></span> <span data-ttu-id="94249-158">不同的作業系統版本會以不同的方式啟動網際網路 Service Manager。</span><span class="sxs-lookup"><span data-stu-id="94249-158">Different operating system versions launch the Internet Service Manager differently.</span></span> <span data-ttu-id="94249-159">若要啟動服務管理員，請遵循下列步驟。</span><span class="sxs-lookup"><span data-stu-id="94249-159">To start the service manager, follow the steps listed below.</span></span>

<span data-ttu-id="94249-160">**若要啟動網際網路 Service Manager**</span><span class="sxs-lookup"><span data-stu-id="94249-160">**To start Internet Service Manager**</span></span>

1. <span data-ttu-id="94249-161">移至 [啟動]。</span><span class="sxs-lookup"><span data-stu-id="94249-161">Go to **Start**.</span></span>
2. <span data-ttu-id="94249-162">按一下 [**執行**]。</span><span class="sxs-lookup"><span data-stu-id="94249-162">Click on **run**.</span></span>
3. <span data-ttu-id="94249-163">輸入**inetmgr**。</span><span class="sxs-lookup"><span data-stu-id="94249-163">Type **inetmgr**.</span></span>  
  
    ![](side-by-side-with-10/_static/image7.gif)
4. <span data-ttu-id="94249-164">從 [網際網路] Service Manager 中，選取您想要知道其版本 .NET Framework 的 Web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="94249-164">From the Internet Service Manager, select the Web application whose version of the .NET Framework you want to know.</span></span>  
  
    ![](side-by-side-with-10/_static/image8.gif)
5. <span data-ttu-id="94249-165">以滑鼠右鍵按一下 Web 應用程式，然後按一下 [**屬性]。**</span><span class="sxs-lookup"><span data-stu-id="94249-165">Right-click on the Web application, and click on **Properties.**</span></span>  
  
    ![](side-by-side-with-10/_static/image9.gif)
6. <span data-ttu-id="94249-166">從 [屬性] 視窗中，選取 [設定] **。**</span><span class="sxs-lookup"><span data-stu-id="94249-166">From the Property window, select **Configuration.**</span></span>  
  
    ![](side-by-side-with-10/_static/image10.gif)
7. <span data-ttu-id="94249-167">從 [應用程式對應] 資料表中，選取 [ **.aspx**]，然後按一下 [**編輯**]。</span><span class="sxs-lookup"><span data-stu-id="94249-167">From the application mapping table, select **.aspx**, and click **Edit**.</span></span>  
  
    ![](side-by-side-with-10/_static/image11.gif)
8. <span data-ttu-id="94249-168">從 [**可執行檔**] 文字方塊中，藉由滾動來查看版本目錄。</span><span class="sxs-lookup"><span data-stu-id="94249-168">From the **Executable** text box, look at the version directory by scrolling.</span></span> <span data-ttu-id="94249-169">如果版本目錄是1.1.4322，應用程式會對應到 .NET Framework 1.1。</span><span class="sxs-lookup"><span data-stu-id="94249-169">If the version directory is v.1.1.4322, the application is mapped to .NET Framework 1.1.</span></span> <span data-ttu-id="94249-170">相反地，如果版本目錄是 v v1.0.3705，應用程式會對應到 .NET Framework 1.0。</span><span class="sxs-lookup"><span data-stu-id="94249-170">Conversely, if the version directory is v1.0.3705, the application is mapped to .NET Framework 1.0.</span></span>  
  
    ![](side-by-side-with-10/_static/image12.gif)
