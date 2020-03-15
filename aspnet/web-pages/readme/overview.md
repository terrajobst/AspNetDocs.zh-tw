---
uid: web-pages/readme/overview
title: WebMatrix 讀我檔案 |Microsoft Docs
author: rick-anderson
description: WebMatrix 和 ASP.NET Web Pages (Razor) 1.0 版讀我檔案
ms.author: riande
ms.date: 01/06/2011
ms.assetid: 36c5beeb-45a7-48a0-9c30-f82cdf5c5f5f
msc.legacyurl: /web-pages/readme
msc.type: content
ms.openlocfilehash: fac53e935860a90d8f2aa96699d56d66ade3a40f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78563466"
---
# <a name="webmatrix-readme"></a><span data-ttu-id="12f32-103">WebMatrix 讀我檔案</span><span class="sxs-lookup"><span data-stu-id="12f32-103">WebMatrix Readme</span></span>

<span data-ttu-id="12f32-104">2011年1月13日</span><span class="sxs-lookup"><span data-stu-id="12f32-104">13 January 2011</span></span>

## <a name="contents"></a><span data-ttu-id="12f32-105">內容</span><span class="sxs-lookup"><span data-stu-id="12f32-105">Contents</span></span>

> [!NOTE]
> <span data-ttu-id="12f32-106">此讀我檔案適用于1.0 版的 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="12f32-106">This readme applies to the 1.0 release of WebMatrix.</span></span>

- [<span data-ttu-id="12f32-107">概觀</span><span class="sxs-lookup"><span data-stu-id="12f32-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="12f32-108">安裝</span><span class="sxs-lookup"><span data-stu-id="12f32-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="12f32-109">如何發行應用程式</span><span class="sxs-lookup"><span data-stu-id="12f32-109">How to Publish Applications</span></span>](#InstructionsForPublishingApplications)
- [<span data-ttu-id="12f32-110">變更和問題</span><span class="sxs-lookup"><span data-stu-id="12f32-110">Changes and Issues</span></span>](#ChangesAndIssues)

    - [<span data-ttu-id="12f32-111">WebMatrix 1.0 安裝</span><span class="sxs-lookup"><span data-stu-id="12f32-111">WebMatrix 1.0 Installation</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="12f32-112">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="12f32-112">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="12f32-113">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="12f32-113">WebMatrix</span></span>](#Known_Issues_WebMatrix)
    - [<span data-ttu-id="12f32-114">IIS Express</span><span class="sxs-lookup"><span data-stu-id="12f32-114">IIS Express</span></span>](#Known_Issues_IISExpress)
    - [<span data-ttu-id="12f32-115">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="12f32-115">SQL Server Compact</span></span>](#Known_Issues_SQLServerCompact)
    - [<span data-ttu-id="12f32-116">安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="12f32-116">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="12f32-117">發行應用程式</span><span class="sxs-lookup"><span data-stu-id="12f32-117">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
- [<span data-ttu-id="12f32-118">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="12f32-118">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="12f32-119">概觀</span><span class="sxs-lookup"><span data-stu-id="12f32-119">Overview</span></span>

> <span data-ttu-id="12f32-120">Microsoft WebMatrix 1.0 是一套免費的網頁開發堆疊，只要幾分鐘即可安裝完成。</span><span class="sxs-lookup"><span data-stu-id="12f32-120">Microsoft WebMatrix 1.0 is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="12f32-121">它會將網頁伺服器與資料庫和程式設計架構整合，以便建立單一且整合的使用經驗。</span><span class="sxs-lookup"><span data-stu-id="12f32-121">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="12f32-122">您可以使用 WebMatrix 來簡化編寫程式碼的方式，並且發行您自己的 ASP.NET 或 PHP 網站，也可以使用 WebMatrix 搭配常見的開放原始碼應用程式 (例如 DotNetNuke、Umbraco、WordPress 或 Joomla) 來啟動新的網站。</span><span class="sxs-lookup"><span data-stu-id="12f32-122">You can use WebMatrix to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="12f32-123">WebMatrix 所使用的網頁伺服器、資料庫引擎和架構環境都與您在網際網路上執行網站所使用的項目一樣功能強大，因此可讓您順利且流暢地從開發轉換至實際執行環境。</span><span class="sxs-lookup"><span data-stu-id="12f32-123">WebMatrix uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="12f32-124">安裝</span><span class="sxs-lookup"><span data-stu-id="12f32-124">Installation</span></span>

> <span data-ttu-id="12f32-125">若要安裝 WebMatrix 1.0，您必須先安裝[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="12f32-125">To install WebMatrix 1.0, you must first install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="12f32-126">安裝 Web Platform Installer 之後，您就可以使用它來安裝 WebMatrix。</span><span class="sxs-lookup"><span data-stu-id="12f32-126">After you've installed the Web Platform Installer, you can use it to install WebMatrix.</span></span>
> 
> <span data-ttu-id="12f32-127">如果您在安裝期間遇到問題，請參閱[疑難排解 Microsoft Web Platform Installer 的問題](https://go.microsoft.com/fwlink/?LinkId=196212)。</span><span class="sxs-lookup"><span data-stu-id="12f32-127">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="InstructionsForPublishingApplications"></a>
## <a name="how-to-publish-applications"></a><span data-ttu-id="12f32-128">如何發行應用程式</span><span class="sxs-lookup"><span data-stu-id="12f32-128">How to Publish Applications</span></span>

> <span data-ttu-id="12f32-129">請參閱[發行應用程式的逐步指示](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="12f32-129">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="ChangesAndIssues"></a>

## <a name="changes-and-issues"></a><span data-ttu-id="12f32-130">變更與問題</span><span class="sxs-lookup"><span data-stu-id="12f32-130">Changes and Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-10-installation-issues"></a><span data-ttu-id="12f32-131">WebMatrix 1.0 安裝問題</span><span class="sxs-lookup"><span data-stu-id="12f32-131">WebMatrix 1.0 Installation Issues</span></span>

#### <a name="issue-webmatrix-10-is-available-only-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="12f32-132">問題：WebMatrix 1.0 只能在支援 Microsoft .NET Framework 4 的平台上使用</span><span class="sxs-lookup"><span data-stu-id="12f32-132">Issue: WebMatrix 1.0 is available only on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="12f32-133">.NET Framework 4 版是 WebMatrix 的必要元件。</span><span class="sxs-lookup"><span data-stu-id="12f32-133">The .NET Framework version 4 is required for WebMatrix.</span></span> <span data-ttu-id="12f32-134">在某些情況下，WebMatrix 1.0 安裝程式會讓您嘗試安裝在不屬於受支援組態集的平台上。</span><span class="sxs-lookup"><span data-stu-id="12f32-134">In certain cases, the WebMatrix 1.0 installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="12f32-135">尤其，不包含 SP1 更新的 Windows Vista 會讓您開始安裝 WebMatrix，但是 .NET Framework 4 元件會失敗並封鎖安裝。</span><span class="sxs-lookup"><span data-stu-id="12f32-135">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="12f32-136">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-136">**Workaround**</span></span>  
> <span data-ttu-id="12f32-137">安裝在支援的平台上，包括：</span><span class="sxs-lookup"><span data-stu-id="12f32-137">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="12f32-138">Windows 7</span><span class="sxs-lookup"><span data-stu-id="12f32-138">Windows 7</span></span>
> - <span data-ttu-id="12f32-139">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="12f32-139">Windows Server 2008</span></span>
> - <span data-ttu-id="12f32-140">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="12f32-140">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="12f32-141">Windows Vista SP1 (含) 以後版本</span><span class="sxs-lookup"><span data-stu-id="12f32-141">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="12f32-142">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="12f32-142">Windows XP SP3</span></span>
> - <span data-ttu-id="12f32-143">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="12f32-143">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-10-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="12f32-144">問題：如果已安裝 Microsoft Visual Studio 2008 但並未安裝 Microsoft Visual Studio 2008 SP1，就無法安裝 WebMatrix 1.0</span><span class="sxs-lookup"><span data-stu-id="12f32-144">Issue: Cannot install WebMatrix 1.0 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="12f32-145">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-145">**Workaround**</span></span>  
> <span data-ttu-id="12f32-146">從 Microsoft 下載中心安裝[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 。</span><span class="sxs-lookup"><span data-stu-id="12f32-146">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="12f32-147">問題：SQL Server Compact 4.0 的某些組件不會安裝在 GAC 中</span><span class="sxs-lookup"><span data-stu-id="12f32-147">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="12f32-148">當您在 64 位元電腦上安裝 SQL Server Compact 4.0，而且該電腦只安裝了 .NET Framework 3.5 SP1 Client Profile 時，SQL Server Compact 4.0 的 Managed 組件就不會放置於全域組件快取 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="12f32-148">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="12f32-149">不會安裝在 GAC 中的 Managed 組件包括：</span><span class="sxs-lookup"><span data-stu-id="12f32-149">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="12f32-150">*System.data.sqlserverce .dll* （ADO.NET 提供者）</span><span class="sxs-lookup"><span data-stu-id="12f32-150">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="12f32-151">*System.data.sqlserverce. Entity* .dll （ADO.NET Entity Framework）</span><span class="sxs-lookup"><span data-stu-id="12f32-151">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="12f32-152">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-152">**Workaround**</span></span>  
> <span data-ttu-id="12f32-153">解除安裝 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="12f32-153">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="12f32-154">從下列位置下載並安裝 .NET Framework 3.5 SP1 完整版本：</span><span class="sxs-lookup"><span data-stu-id="12f32-154">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="12f32-155">Microsoft .NET Framework 3.5 Service pack 1 （完整套件）</span><span class="sxs-lookup"><span data-stu-id="12f32-155">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="12f32-156">然後重新安裝 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="12f32-156">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="12f32-157">問題：無法使用命令列解除安裝 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="12f32-157">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="12f32-158">在這個版本中，使用命令列選項解除安裝 SQL Server Compact 沒有作用。</span><span class="sxs-lookup"><span data-stu-id="12f32-158">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="12f32-159">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-159">**Workaround**</span></span>  
> <span data-ttu-id="12f32-160">使用 Windows [控制台] 中的 [*程式和功能*] 卸載 Microsoft SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="12f32-160">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="12f32-161">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="12f32-161">ASP.NET Web Pages</span></span>

<span data-ttu-id="12f32-162">本文件的這一節將描述含有 Razor 語法的 ASP.NET Web Pages 1.0 版的新功能、變更和已知問題。</span><span class="sxs-lookup"><span data-stu-id="12f32-162">This section of the document describes new features, changes, and known issues with the 1.0 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="12f32-163">新功能</span><span class="sxs-lookup"><span data-stu-id="12f32-163">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="12f32-164">變更</span><span class="sxs-lookup"><span data-stu-id="12f32-164">Changes</span></span>](#Changes)
- [<span data-ttu-id="12f32-165">問題</span><span class="sxs-lookup"><span data-stu-id="12f32-165">Issues</span></span>](#Issues)

#### <a id="NewFeatures"></a><span data-ttu-id="12f32-166">新功能</span><span class="sxs-lookup"><span data-stu-id="12f32-166">New Features</span></span>

#### <a name="new-configuration-setting-added-to-disable-the-package-manager"></a><span data-ttu-id="12f32-167">新增：加入了停用封裝管理員的組態設定</span><span class="sxs-lookup"><span data-stu-id="12f32-167">New: Configuration setting added to disable the package manager</span></span>

> <span data-ttu-id="12f32-168">*Web.config*檔案中的 `<appSettings>` 元素可以使用新的 `asp:AdminManagerEnabled` 金鑰，這可讓您完全停用封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="12f32-168">A new `asp:AdminManagerEnabled` key is available for the `<appSettings>` element in the *web.config* file, which lets you completely disable the package manager.</span></span> <span data-ttu-id="12f32-169">這個專案的預設值為 true，這表示如果不包含*在 web.config 檔案*中，則會啟用封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="12f32-169">The default value for this element is true, meaning that if it is not included in the *web.config* file, the package manager is enabled.</span></span> <span data-ttu-id="12f32-170">若要停用封裝管理員，請將下列元素新增*至網站根目錄中的 web.config*檔案：</span><span class="sxs-lookup"><span data-stu-id="12f32-170">To disable the package manager, add the following element to the *web.config* file in the root of the website:</span></span>
> 
> [!code-xml[Main](overview/samples/sample1.xml)]

#### <a id="Changes"></a><span data-ttu-id="12f32-171">變更</span><span class="sxs-lookup"><span data-stu-id="12f32-171">Changes</span></span>

#### <a name="change-webpagesadminfoldervirtualpath-key-renamed-to-aspadminfoldervirtualpath"></a><span data-ttu-id="12f32-172">變更："webPages:AdminFolderVirtualPath" 索引鍵已重新命名為 "asp:AdminFolderVirtualPath"</span><span class="sxs-lookup"><span data-stu-id="12f32-172">Change: "webPages:AdminFolderVirtualPath" key renamed to "asp:AdminFolderVirtualPath"</span></span>

> <span data-ttu-id="12f32-173">可以新增至*web.config*檔案以指定封裝管理員位置的 `webPages:AdminFolderVirtualPath` 金鑰已經重新命名為使用 `asp:` 命名空間，而不是 `webPages` 命名空間。</span><span class="sxs-lookup"><span data-stu-id="12f32-173">The `webPages:AdminFolderVirtualPath` key that can be added to the *web.config* file to specify the location of the package manager has been renamed to use the `asp:` namespace instead of the `webPages` namespace.</span></span> <span data-ttu-id="12f32-174">如果您已經使用此項目，就必須在組態檔中重新命名此項目。</span><span class="sxs-lookup"><span data-stu-id="12f32-174">If you have used this element, you must rename it in the configuration file.</span></span>

#### <a id="Issues"></a> <span data-ttu-id="12f32-175">已知問題</span><span class="sxs-lookup"><span data-stu-id="12f32-175">Known Issues</span></span>

#### <a name="issue-passwords-for-membership-users-no-longer-recognized"></a><span data-ttu-id="12f32-176">問題：無法再辨識成員資格使用者的密碼</span><span class="sxs-lookup"><span data-stu-id="12f32-176">Issue: Passwords for membership users no longer recognized</span></span>

> <span data-ttu-id="12f32-177">用於建立和儲存成員資格 (登入) 密碼的演算法已經變更為更安全的演算法。</span><span class="sxs-lookup"><span data-stu-id="12f32-177">The algorithm for creating and storing membership (login) passwords has been changed to be more secure.</span></span> <span data-ttu-id="12f32-178">因此，系統無法辨識針對 ASP.NET Razor Beta 版中建立之成員 (使用者) 所儲存的密碼。</span><span class="sxs-lookup"><span data-stu-id="12f32-178">As a result, the passwords stored for members (users) created in Beta versions of ASP.NET Razor will not be recognized.</span></span> 
> 
> <span data-ttu-id="12f32-179">因應措施如果網站尚未進入生產環境，請從成員資格資料庫中移除使用者記錄。</span><span class="sxs-lookup"><span data-stu-id="12f32-179">**Workaround** If the site has not yet been put into production, remove the user records from the membership database.</span></span> <span data-ttu-id="12f32-180">如果資料庫已上線，請在成員資格資料庫中以程式設計方式重新產生現有的密碼。</span><span class="sxs-lookup"><span data-stu-id="12f32-180">If database is live, programmatically regenerate existing passwords in the membership database.</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="12f32-181">問題：針對成員資格使用自訂使用者資料表時發生非預期的行為</span><span class="sxs-lookup"><span data-stu-id="12f32-181">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="12f32-182">若要初始化 ASP.NET Razor 網站的成員資格提供者，您可以呼叫 `WebSecurity.InitializeDatabaseConnection` 方法。</span><span class="sxs-lookup"><span data-stu-id="12f32-182">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="12f32-183">（在 WebMatrix 中，入門網站範本會在 *\_AppStart*中包含此方法的呼叫）。如果此方法的 `autoCreateTables` 參數設定為 true （預設會在入門網站範本中設定為 true），而且如果將無法辨識的資料表名稱傳遞給方法（第二個參數），則此方法不會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="12f32-183">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="12f32-184">不過，它會自動產生資料表。</span><span class="sxs-lookup"><span data-stu-id="12f32-184">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="12f32-185">如果您想要使用自訂使用者資料表來取得成員資格，但將錯誤的資料表名稱傳遞給 `WebSecurity.InitializeDatabaseConnection` 方法，這可能會是個問題。</span><span class="sxs-lookup"><span data-stu-id="12f32-185">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="12f32-186">因為如果您所指定的資料表不存在，此方法預設不會引發錯誤，而且因為它會改為建立新的資料表，所以應用程式可能會看似正常運作。</span><span class="sxs-lookup"><span data-stu-id="12f32-186">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="12f32-187">不過，相依於自訂使用者資料表 (以及資料表中的欄位) 的應用程式程式碼最後可能會失敗並發生非預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="12f32-187">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="12f32-188">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-188">**Workaround**</span></span>  
> <span data-ttu-id="12f32-189">請確定在 `InitializeDatabaseConnection` 方法中傳遞的名稱符合成員資格資料庫中的使用者設定檔資料表，或確認 `autoCreateTables` 參數設定為 false。</span><span class="sxs-lookup"><span data-stu-id="12f32-189">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-error-message-the-admin-module-requires-access-to-app_data"></a><span data-ttu-id="12f32-190">問題：「系統管理模組需要存取 ~/App\_資料」錯誤訊息</span><span class="sxs-lookup"><span data-stu-id="12f32-190">Issue: Error message "The Admin Module requires access to ~/App\_Data"</span></span>

> <span data-ttu-id="12f32-191">在某些情況下，嘗試建立使用者或使用 ASP.NET 成員資格系統，可能會導致頁面顯示系統*管理模組需要存取 ~/App\_資料*的錯誤。</span><span class="sxs-lookup"><span data-stu-id="12f32-191">Under some circumstances, trying to create users or otherwise work with the ASP.NET membership system can cause the page to display the error *The Admin Module requires access to ~/App\_Data*.</span></span> <span data-ttu-id="12f32-192">如果執行 IIS 或 IIS Express 的帳戶沒有建立和寫入網站根目錄下之*應用程式\_Data*資料夾的許可權，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="12f32-192">This occurs if the account that IIS or IIS Express is running under does not have permissions to create and write to the *App\_Data* folder under the website root.</span></span> 
> 
> <span data-ttu-id="12f32-193">因應措施為網站手動建立 *\_Data 資料夾的應用程式*。</span><span class="sxs-lookup"><span data-stu-id="12f32-193">**Workaround** Manually create an *App\_Data* folder for the website.</span></span> <span data-ttu-id="12f32-194">然後確定應用程式執行的 Windows 帳戶（通常是 NETWORK SERVICE）擁有應用程式根資料夾和子資料夾（例如應用程式\_資料）的讀取/寫入權限。</span><span class="sxs-lookup"><span data-stu-id="12f32-194">Then make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as App\_Data.</span></span> <span data-ttu-id="12f32-195">如需詳細資訊，請參閱知識庫文章[SQL Server Express 使用者實例和 ASP.net Web 應用程式專案的問題](https://support.microsoft.com/kb/2002980)。</span><span class="sxs-lookup"><span data-stu-id="12f32-195">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="12f32-196">問題：「無法產生 SQL Server 的使用者執行個體」錯誤</span><span class="sxs-lookup"><span data-stu-id="12f32-196">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="12f32-197">如果 WebMatrix Web 應用程式使用了 SQL Server Express 而且正在 Windows 7 或 Windows Server 2008 R2 上執行 IIS 7.5，您可能會看見一則錯誤，表示 SQL Server 無法在執行階段中擷取使用者的本機應用程式路徑。</span><span class="sxs-lookup"><span data-stu-id="12f32-197">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="12f32-198">因應措施確定用來執行應用程式的 Windows 帳戶（通常是 NETWORK SERVICE）擁有應用程式根資料夾和子資料夾（例如*應用程式\_資料*）的讀取/寫入權限。</span><span class="sxs-lookup"><span data-stu-id="12f32-198">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="12f32-199">如需詳細資訊，請參閱知識庫文章[SQL Server Express 使用者實例和 ASP.net Web 應用程式專案的問題](https://support.microsoft.com/kb/2002980)。</span><span class="sxs-lookup"><span data-stu-id="12f32-199">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-files-that-contains-package-manager-resources-or-package-manager-passwords-are-servable-under-iis-60-and-earlier"></a><span data-ttu-id="12f32-200">問題：包含封裝管理員資源或封裝管理員密碼的檔案可在 IIS 6.0 和先前版本底下提供</span><span class="sxs-lookup"><span data-stu-id="12f32-200">Issue: Files that contains package-manager resources or package-manager passwords are servable under IIS 6.0 and earlier</span></span>

> <span data-ttu-id="12f32-201">如果您部署的是使用 RC2 版本建立的 ASP.NET Web Pages （Razor）應用程式，且應用程式在 */App\_Data/admin*底下包含*password .txt*或*packagesources* ，則 IIS 6.0 將會提供檔案（如有要求），可能會公開您的套件管理員實例的密碼。</span><span class="sxs-lookup"><span data-stu-id="12f32-201">If you deploy an ASP.NET Web Pages (Razor) application that was built using the RC2 release, and if the application contains a *password.txt* or *packagesources.txt* file under */App\_Data/admin*, IIS 6.0 will serve the file if requested, potentially exposing the passwords for your package manager instance.</span></span> 
> 
> <span data-ttu-id="12f32-202">因應措施將*密碼 .txt*或*packagesources*重新命名為*config.xml*或*packagesources*。根據預設，IIS 6.0 不會提供副檔名為 *.config*的檔案。</span><span class="sxs-lookup"><span data-stu-id="12f32-202">**Workaround** Rename the *password.txt* or *packagesources.txt* file to *password.config* or *packagesources.config*. By default, IIS 6.0 does not serve files that have the *.config* extension.</span></span> <span data-ttu-id="12f32-203">（在 IIS 7 中，應用程式中不會提供任何檔案 *\_Data*資料夾，因此您不需要重新命名檔案）。</span><span class="sxs-lookup"><span data-stu-id="12f32-203">(In IIS 7, no files in the *App\_Data* folder are served, so you do not need to rename the files.)</span></span>

#### <a name="issue-uninstalling-packages-installed-using-the-beta-3-release-does-not-completely-remove-package-components"></a><span data-ttu-id="12f32-204">問題：解除安裝使用 Beta 3 版本所安裝的封裝並未完全移除封裝元件</span><span class="sxs-lookup"><span data-stu-id="12f32-204">Issue: Uninstalling packages installed using the Beta 3 release does not completely remove package components</span></span>

> <span data-ttu-id="12f32-205">如果您使用 Beta 3 版本中的封裝管理員來安裝某個封裝，然後嘗試使用目前版本來解除安裝該封裝，就無法完全解除安裝該封裝。</span><span class="sxs-lookup"><span data-stu-id="12f32-205">If you installed a package using the package manager in the Beta 3 release and then try to uninstall it using the current release, the package is not completely uninstalled.</span></span> <span data-ttu-id="12f32-206">使用套件管理員的 [**卸載**] 按鈕會移除部分元件，但會保留套件的程式庫程式碼，而且不會更新*package*檔案。</span><span class="sxs-lookup"><span data-stu-id="12f32-206">Using the package manager's **Uninstall** button removes some components, but leaves the package's library code and does not update the *package.config* file.</span></span>
> 
> <span data-ttu-id="12f32-207">因應\*\*措施 \*\*</span><span class="sxs-lookup"><span data-stu-id="12f32-207">**Workaround** </span></span>  
> <span data-ttu-id="12f32-208">執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="12f32-208">Perform these steps:</span></span>  
> 1. <span data-ttu-id="12f32-209">\_Data\packages 資料夾中刪除*應用程式*。</span><span class="sxs-lookup"><span data-stu-id="12f32-209">Delete the *App\_Data\packages* folder.</span></span> <span data-ttu-id="12f32-210">這會移除所有套件。</span><span class="sxs-lookup"><span data-stu-id="12f32-210">This removes all packages.</span></span>   
> 2. <span data-ttu-id="12f32-211">刪除網站根目錄中的*封裝 .config*檔案。</span><span class="sxs-lookup"><span data-stu-id="12f32-211">Delete the *packages.config* file in the root of the website.</span></span>

#### <a name="issue-in-visual-studio-invoking-the-web-based-package-manager-takes-the-application-offline"></a><span data-ttu-id="12f32-212">問題：在 Visual Studio 中，叫用 Web 架構封裝管理員會讓應用程式離線</span><span class="sxs-lookup"><span data-stu-id="12f32-212">Issue: In Visual Studio, invoking the web-based package manager takes the application offline</span></span>

> <span data-ttu-id="12f32-213">如果您在 Visual Studio （非 WebMatrix）中工作，並使用 *\_系統管理員*功能啟動套件管理員，Visual Studio 會讓應用程式離線，並將應用程式 *\_離線*發佈到網站根目錄，這會破壞您使用封裝管理員的能力。</span><span class="sxs-lookup"><span data-stu-id="12f32-213">If you are working in Visual Studio (not WebMatrix) and use the *\_admin* functionality to start the package manager, Visual Studio takes the application offline and posts the *app\_offline.htm* into the website root, which disrupts your ability to use the package manager.</span></span>
> 
> [!NOTE]
> <span data-ttu-id="12f32-214">雖然您通常會在使用以 web 為基礎的套件管理員介面時看到這種行為，但如果您新增、移除或修改應用程式中的任何檔案 *\_Data*資料夾，就會發生相同的行為。</span><span class="sxs-lookup"><span data-stu-id="12f32-214">Although you would most typically see this behavior when using the web-based package manager interface, the same behavior occurs if you add, remove, or modify any files in the *App\_Data* folder.</span></span>
> 
> <span data-ttu-id="12f32-215">因應\*\*措施 \*\*</span><span class="sxs-lookup"><span data-stu-id="12f32-215">**Workaround** </span></span>  
> <span data-ttu-id="12f32-216">若要在 Visual Studio 中使用封裝，請使用 NuGet 延伸模組而非 Web 架構封裝管理員。</span><span class="sxs-lookup"><span data-stu-id="12f32-216">To work with packages in Visual Studio, use the NuGet extension instead of the web-based package manager.</span></span> <span data-ttu-id="12f32-217">如需詳細資訊，請參閱[NuGet 檔](https://docs.microsoft.com/nuget/)。</span><span class="sxs-lookup"><span data-stu-id="12f32-217">For information, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span> <span data-ttu-id="12f32-218">如果您使用應用程式中的其他檔案 *\_Data*資料夾，請考慮將檔案保留在其他位置，以避免發生此問題。</span><span class="sxs-lookup"><span data-stu-id="12f32-218">If you are working with other files in the *App\_Data* folder, consider keeping the files elsewhere to avoid this issue.</span></span> <span data-ttu-id="12f32-219">如果不可行，請以手動方式刪除*應用程式\_離線的 .htm*檔案，或等到網站自動復原上線（預設為30秒之後）。</span><span class="sxs-lookup"><span data-stu-id="12f32-219">If that's not practical, delete the *app\_offline.htm* file manually or wait until the site comes back online automatically (by default, after 30 seconds).</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="12f32-220">問題：Visual Studio IntelliSense 和專案範本只能在 ASP.NET MVC 3 版中使用</span><span class="sxs-lookup"><span data-stu-id="12f32-220">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="12f32-221">安裝 ASP.NET Web Pages 不會一併安裝適用於 Visual Studio 的工具，例如適用於 ASP.NET Web Pages 應用程式的 IntelliSense 和專案範本。</span><span class="sxs-lookup"><span data-stu-id="12f32-221">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="12f32-222">因應措施若要在 Visual Studio 中使用 ASP.NET Web Pages 應用程式的 IntelliSense 和專案範本，請透過 Web Platform Installer 或[獨立安裝程式](https://go.microsoft.com/fwlink/?LinkID=191797)來安裝 ASP.NET MVC 3 RC。</span><span class="sxs-lookup"><span data-stu-id="12f32-222">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="12f32-223">問題：經由 Proxy 伺服器讀取摘要或其他外部資料</span><span class="sxs-lookup"><span data-stu-id="12f32-223">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="12f32-224">如果執行網站的伺服器位於 proxy 伺服器後方，您可能需要*在 web.config 檔案*中設定 proxy 資訊，才能讀取來自網站外部的資訊。</span><span class="sxs-lookup"><span data-stu-id="12f32-224">If the server running the site is behind a proxy server, you might need to configure proxy information in the *web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="12f32-225">例如，如果您使用 `ReCaptcha` 協助程式，則協助專家會與 reCAPTCHA 服務通訊，但您的 proxy 伺服器可能會封鎖它。</span><span class="sxs-lookup"><span data-stu-id="12f32-225">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="12f32-226">同樣地，用於 ASP.NET Web Pages 中的摘要 (例如封裝管理員所使用的摘要) 可能需要 Proxy 組態。</span><span class="sxs-lookup"><span data-stu-id="12f32-226">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="12f32-227">如果您在使用外部服務或使用封裝摘要時遇到問題，請將下列元素放入應用程式*的根 web.config*檔案中：</span><span class="sxs-lookup"><span data-stu-id="12f32-227">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *web.config* file:</span></span>
> 
> [!code-xml[Main](overview/samples/sample2.xml)]
> 
> <span data-ttu-id="12f32-228">如需設定 proxy 伺服器的詳細資訊，請參閱 MSDN 網站上的[&lt;proxy&gt; 元素（網路設定）](https://msdn.microsoft.com/library/sa91de1e.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="12f32-228">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="12f32-229">問題：解除安裝 .NET Framework 4 版就會停用含有 Razor 語法的 ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="12f32-229">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="12f32-230">如果您解除安裝 .NET Framework 4 版，然後重新安裝它，就會停用含有 Razor 語法的 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="12f32-230">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="12f32-231">具有 *. cshtml*副檔名的頁面無法正確執行。</span><span class="sxs-lookup"><span data-stu-id="12f32-231">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="12f32-232">ASP.NET Web Pages 在*電腦根目錄的 web.config 檔案*中註冊元件，移除 .NET Framework 會移除該檔案。</span><span class="sxs-lookup"><span data-stu-id="12f32-232">ASP.NET Web Pages registers an assembly in the machine root *web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="12f32-233">雖然重新安裝 .NET Framework 會安裝新版的組態檔，不過卻不會加入 ASP.NET Web Pages 組件的參考。</span><span class="sxs-lookup"><span data-stu-id="12f32-233">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="12f32-234">因應措施重新安裝 .NET Framework 之後，請使用 Razor 語法重新安裝 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="12f32-234">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="12f32-235">這會將下列專案新增至電腦根目錄*中的 web.config*檔案，此檔案通常位於下列位置：</span><span class="sxs-lookup"><span data-stu-id="12f32-235">This adds the following element to the *web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](overview/samples/sample3.xml)]

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="12f32-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="12f32-236">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="12f32-237">在 IIS 7 或 IIS 7.5 上，URL 如下的要求找不到具有 *. cshtml*或*vbhtml*副檔名的頁面：</span><span class="sxs-lookup"><span data-stu-id="12f32-237">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="12f32-238">因為 IIS 7 或 IIS 7.5 預設不會啟用 URL 重寫，所以會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="12f32-238">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="12f32-239">原因案例是，當您使用 IIS Express 在本機進行測試時，不會看到問題，但是當您將網站部署至主控網站時，就會遇到此問題。</span><span class="sxs-lookup"><span data-stu-id="12f32-239">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="12f32-240">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-240">**Workaround**</span></span>
> 
> - <span data-ttu-id="12f32-241">如果您可以控制伺服器電腦，請在伺服器電腦上安裝更新中所述的更新，[讓特定 IIS 7.0 或 IIS 7.5 處理常式能夠處理其 url 不是以句號結尾的要求](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="12f32-241">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="12f32-242">如果您無法控制伺服器電腦（例如，您要部署至主控網站），請將下列*內容新增至網站的 web.config*檔案：</span><span class="sxs-lookup"><span data-stu-id="12f32-242">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *web.config* file:</span></span> 
> 
>     [!code-xml[Main](overview/samples/sample4.xml)]

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="12f32-243">問題：將應用程式部署到未安裝 SQL Server Compact 的電腦</span><span class="sxs-lookup"><span data-stu-id="12f32-243">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="12f32-244">包含 SQL Server Compact 資料庫的應用程式可以在未安裝 SQL Server Compact 的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="12f32-244">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="12f32-245">Microsoft WebMatrix 1.0 會自動為您複製這些二進位檔，並執行適當的*web.config*檔案轉換。</span><span class="sxs-lookup"><span data-stu-id="12f32-245">Microsoft WebMatrix 1.0 automatically copies these binaries for you and performs the appropriate *web.config* file transforms.</span></span>
> 
> <span data-ttu-id="12f32-246">因應措施如果您需要複製這些檔案，並手動進行*web.config*檔案變更，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="12f32-246">**Workaround** If you need to copy these files and make the *web.config* file changes manually, do the following:</span></span>
> 
> 1. <span data-ttu-id="12f32-247">將資料庫引擎元件複製到目的電腦上應用程式的*Bin*資料夾（和子資料夾）：</span><span class="sxs-lookup"><span data-stu-id="12f32-247">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span>  
> 
>    - <span data-ttu-id="12f32-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span><span class="sxs-lookup"><span data-stu-id="12f32-248">Copy *C:\Program Files\Microsoft SQL Server Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* </span></span>  
>      <span data-ttu-id="12f32-249">**至** *\bin*</span><span class="sxs-lookup"><span data-stu-id="12f32-249">**to** *\Bin*</span></span>
>    - <span data-ttu-id="12f32-250">將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* 複製**到** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="12f32-250">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* **to** *\Bin\x86*</span></span>
>    - <span data-ttu-id="12f32-251">將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* 複製**到** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="12f32-251">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 
> 2. <span data-ttu-id="12f32-252">在網站的根資料夾中，建立或*開啟 web.config 檔案*。</span><span class="sxs-lookup"><span data-stu-id="12f32-252">In the root folder of the website, create or open a *web.config* file.</span></span> <span data-ttu-id="12f32-253">（在 WebMatrix 1.0 中，如果您在 [**選擇檔案類型**] 對話方塊中按一下 [**全部**]，則可以使用此檔案類型）。</span><span class="sxs-lookup"><span data-stu-id="12f32-253">(In WebMatrix 1.0, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="12f32-254">新增下列專案做為 `<configuration>` 專案的子系（不在 `<system.web>` 元素內）：</span><span class="sxs-lookup"><span data-stu-id="12f32-254">Add the following element as a child of the `<configuration>` element (not inside the `<system.web>` element):</span></span>
> 
>     [!code-xml[Main](overview/samples/sample5.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="12f32-255">問題：「資料庫」和「WebGrid」協助程式無法在 Visual Basic 的中度信任中使用</span><span class="sxs-lookup"><span data-stu-id="12f32-255">Issue: "Database" and "WebGrid" helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="12f32-256">如果您使用 Visual Basic （建立*vbhtml*檔案），則當應用程式設定為使用中度信任時，`Database` 和 `WebGrid` helper 將無法使用。</span><span class="sxs-lookup"><span data-stu-id="12f32-256">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="12f32-257">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-257">**Workaround**</span></span>  
> <span data-ttu-id="12f32-258">如果您使用 Visual Studio 2010，您可以藉由安裝 Service Pack 1 版本來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="12f32-258">If you use Visual Studio 2010, you can resolve this problem by installing the Service Pack 1 release.</span></span> <span data-ttu-id="12f32-259">在 SP1 版本的最終版本可供使用之前，您可以從 Microsoft 下載中心的[Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en)版頁面下載 sp1 的搶鮮版（Beta）。</span><span class="sxs-lookup"><span data-stu-id="12f32-259">Until the final version of the SP1 release is available, you can download the Beta version of SP1 from the [Microsoft Visual Studio 2010 Service Pack 1 Beta](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=11ea69cb-cf12-4842-a3d7-b32a1e5642e2&amp;displaylang=en) page on the Microsoft Download Center.</span></span>   
>   
> <span data-ttu-id="12f32-260">如果這不可行，或如果您未使用 Visual Studio 2010，您可以暫時將應用程式設定為使用完全信任。</span><span class="sxs-lookup"><span data-stu-id="12f32-260">If this is not practical, or if you do not use Visual Studio 2010, you can temporarily set the application to use Full Trust.</span></span>

#### <a name="issue-applicationpart-resources-are-externally-accessible"></a><span data-ttu-id="12f32-261">問題：「ApplicationPart」資源可從外部存取</span><span class="sxs-lookup"><span data-stu-id="12f32-261">Issue: "ApplicationPart" resources are externally accessible</span></span>

> <span data-ttu-id="12f32-262">如果元件包含衍生自 `ApplicationPart` 類別的物件，則 `ResourceRouteHandler` 類別會公開該元件的資源。</span><span class="sxs-lookup"><span data-stu-id="12f32-262">If an assembly contains objects that derives from the `ApplicationPart` class, that assembly's resources are exposed by the `ResourceRouteHandler` class.</span></span> <span data-ttu-id="12f32-263">例如，請考慮下列 URL：</span><span class="sxs-lookup"><span data-stu-id="12f32-263">For example, consider the following URL:</span></span>  
>   
> `~/r.ashx/System.Web.WebPages.Administration/Resources/AdminResources.resources`  
>   
> <span data-ttu-id="12f32-264">此要求會下載*system.web. system.web*元件中的所有資源字串。</span><span class="sxs-lookup"><span data-stu-id="12f32-264">This request downloads all of the resource strings in the *System.Web.WebPages.Administration.dll* assembly.</span></span> <span data-ttu-id="12f32-265">會下載所有的內嵌資源（即使是不打算做為靜態內容的資源）。</span><span class="sxs-lookup"><span data-stu-id="12f32-265">All of the embedded resources (even those that are not intended to be served as static content) are downloaded.</span></span> <span data-ttu-id="12f32-266">如果內嵌資源包含敏感性資訊，這可能代表安全性風險。</span><span class="sxs-lookup"><span data-stu-id="12f32-266">If the embedded resources contain sensitive information, this can represent a security risk.</span></span> 
> 
> <span data-ttu-id="12f32-267">因應\*\*措施 \*\*</span><span class="sxs-lookup"><span data-stu-id="12f32-267">**Workaround** </span></span>  
> <span data-ttu-id="12f32-268">如果您建立**ApplicationPart**物件，請確定與該**ApplicationPart**物件的元件相關聯的內嵌資源不包含敏感性資訊。</span><span class="sxs-lookup"><span data-stu-id="12f32-268">If you create an **ApplicationPart** object, make sure that the embedded resources associated with that **ApplicationPart** object's assembly do not contain sensitive information.</span></span>

<a id="Known_Issues_WebMatrix"></a>

### <a name="webmatrix"></a><span data-ttu-id="12f32-269">WebMatrix</span><span class="sxs-lookup"><span data-stu-id="12f32-269">WebMatrix</span></span>

> [!NOTE]
> <span data-ttu-id="12f32-270">如需 WebMatrix 安裝問題的相關資訊，請參閱本檔稍早的[WebMatrix 安裝問題](#Known_Issues_Installation)。</span><span class="sxs-lookup"><span data-stu-id="12f32-270">For information about installation issues for WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

<span data-ttu-id="12f32-271">檔的這一節說明 WebMatrix 開發環境的已知問題。</span><span class="sxs-lookup"><span data-stu-id="12f32-271">This section of the document describes known issues for the WebMatrix development environment.</span></span>

#### <a name="issue-changes-in-the-username-or-password-of-a-database-connection-string-in-a-webconfig-file-are-not-reflected-in-the-databases-workspace"></a><span data-ttu-id="12f32-272">問題： web.config 檔案中資料庫連接字串的使用者名稱或密碼變更，不會反映在 [資料庫] 工作區中</span><span class="sxs-lookup"><span data-stu-id="12f32-272">Issue: Changes in the username or password of a database connection string in a web.config file are not reflected in the Databases workspace</span></span>

> <span data-ttu-id="12f32-273">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-273">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="12f32-274">在 web.config*檔案*中，變更連接字串中的資料庫名稱（例如，在其中加上 "1"）。</span><span class="sxs-lookup"><span data-stu-id="12f32-274">In the *web.config* file, change the database name in the connection string (for example, add "1" to it).</span></span>
> 2. <span data-ttu-id="12f32-275">儲存 web.config*檔案*。</span><span class="sxs-lookup"><span data-stu-id="12f32-275">Save the *web.config* file.</span></span>
> 3. <span data-ttu-id="12f32-276">按一下 [**資料庫**] 和 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="12f32-276">Click **Databases** and refresh.</span></span>
> 4. <span data-ttu-id="12f32-277">將*web.config*檔案之連接字串中的資料庫名稱，變更回原始的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="12f32-277">Change the database name in the connection string in the *web.config* file back to the original database name.</span></span>
> 5. <span data-ttu-id="12f32-278">儲存 web.config*檔案*。</span><span class="sxs-lookup"><span data-stu-id="12f32-278">Save the *web.config* file.</span></span>
> 6. <span data-ttu-id="12f32-279">按一下 [**資料庫**] 和 [重新整理]。</span><span class="sxs-lookup"><span data-stu-id="12f32-279">Click **Databases** and refresh.</span></span>

#### <a name="issue-folders-created-by-webmatrix-cannot-be-deleted"></a><span data-ttu-id="12f32-280">問題：無法刪除 WebMatrix 所建立的資料夾</span><span class="sxs-lookup"><span data-stu-id="12f32-280">Issue: Folders created by WebMatrix cannot be deleted</span></span>

> <span data-ttu-id="12f32-281">如果使用較高的許可權來執行 WebMatrix （也就是您使用 Windows 中的 [**以系統管理員身分執行**] 選項啟動 webmatrix），則無法使用 windows Explorer 刪除 webmatrix 所建立的資料夾。</span><span class="sxs-lookup"><span data-stu-id="12f32-281">If WebMatrix is running using elevated permissions (that is, you started WebMatrix using the **Run as Administrator** option in Windows), folders that are created by WebMatrix cannot be deleted using Windows Explorer.</span></span>
> 
> <span data-ttu-id="12f32-282">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-282">**Workaround**</span></span>  
> <span data-ttu-id="12f32-283">使用較高的許可權執行 Windows Explorer。</span><span class="sxs-lookup"><span data-stu-id="12f32-283">Run Windows Explorer using elevated permissions.</span></span> <span data-ttu-id="12f32-284">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="12f32-284">Follow these steps:</span></span>  
> 
> 1. <span data-ttu-id="12f32-285">在 Windows 中，按一下 [**啟動**]。</span><span class="sxs-lookup"><span data-stu-id="12f32-285">In Windows, click **Start**.</span></span>
> 2. <span data-ttu-id="12f32-286">輸入 "Windows Explorer"，然後以滑鼠右鍵按一下 [ **Windows explorer**] 的專案。</span><span class="sxs-lookup"><span data-stu-id="12f32-286">Enter "Windows Explorer" and right-click the entry for **Windows Explorer**.</span></span>
> 3. <span data-ttu-id="12f32-287">按一下 [**以系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="12f32-287">Click **Run as Administrator**.</span></span> <span data-ttu-id="12f32-288">然後您就可以刪除資料夾。</span><span class="sxs-lookup"><span data-stu-id="12f32-288">You can then delete the folders.</span></span>

#### <a name="issue-webmatrix-10-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="12f32-289">問題： WebMatrix 1.0 無法執行需要提高許可權的特定工作</span><span class="sxs-lookup"><span data-stu-id="12f32-289">Issue: WebMatrix 1.0 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="12f32-290">WebMatrix 1.0 無法執行需要提高許可權的特定工作，例如在下列情況下安裝其他元件：</span><span class="sxs-lookup"><span data-stu-id="12f32-290">WebMatrix 1.0 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="12f32-291">在 Windows Vista 或 Windows 7 上，您使用不具有系統管理許可權的帳戶登入，且使用者帳戶控制（UAC）已停用。</span><span class="sxs-lookup"><span data-stu-id="12f32-291">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="12f32-292">您使用的是 Microsoft Windows XP 或 Microsoft Windows Server 2003。</span><span class="sxs-lookup"><span data-stu-id="12f32-292">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="12f32-293">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-293">**Workaround**</span></span>  
> <span data-ttu-id="12f32-294">WebMatrix 1.0 中大部分的工作都不需要系統管理許可權。</span><span class="sxs-lookup"><span data-stu-id="12f32-294">Most tasks in WebMatrix 1.0 do not require administrative permission.</span></span> <span data-ttu-id="12f32-295">若是這樣做，您可以系統管理員身分執行作業，或遵循下列步驟進行操作：</span><span class="sxs-lookup"><span data-stu-id="12f32-295">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="12f32-296">在 Windows Vista 或 Windows 7 上，啟用 UAC。</span><span class="sxs-lookup"><span data-stu-id="12f32-296">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="12f32-297">在 Windows XP 上，將使用者新增至 [系統管理員] 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="12f32-297">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="12f32-298">問題：「Web 元件庫中的網站」已停用</span><span class="sxs-lookup"><span data-stu-id="12f32-298">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="12f32-299">如果未安裝 Web Platform Installer 3.0，則會停用 [**從 Web 元件庫中的網站**] 選項。</span><span class="sxs-lookup"><span data-stu-id="12f32-299">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="12f32-300">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-300">**Workaround**</span></span>  
> <span data-ttu-id="12f32-301">安裝[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="12f32-301">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="12f32-302">問題： Google Chrome 無法當做執行選項使用</span><span class="sxs-lookup"><span data-stu-id="12f32-302">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="12f32-303">Google Chrome 不會顯示在 [**首頁**] 索引標籤上 [**執行**] 底下的瀏覽器清單中。</span><span class="sxs-lookup"><span data-stu-id="12f32-303">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="12f32-304">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-304">**Workaround**</span></span>  
> <span data-ttu-id="12f32-305">某些版本的 Google Chrome 不會正確地向 Windows 中的 [預設程式] 功能註冊自己。</span><span class="sxs-lookup"><span data-stu-id="12f32-305">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="12f32-306">因應措施是啟動 Google Chrome，按一下 [*自訂和控制 Google chrome* ] 功能表，按一下 [*選項*]，然後按一下 [*將 google Chrome 設為預設瀏覽器*]。</span><span class="sxs-lookup"><span data-stu-id="12f32-306">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="12f32-307">問題： [外鍵] 對話方塊不允許輸入主要金鑰</span><span class="sxs-lookup"><span data-stu-id="12f32-307">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="12f32-308">[**外鍵**] 對話方塊不允許您從主鍵資料表輸入主要金鑰名稱。</span><span class="sxs-lookup"><span data-stu-id="12f32-308">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="12f32-309">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-309">**Workaround**</span></span>  
> <span data-ttu-id="12f32-310">這是故意的。</span><span class="sxs-lookup"><span data-stu-id="12f32-310">This is intentional.</span></span> <span data-ttu-id="12f32-311">您不需要輸入主要索引鍵資料表的主鍵名稱。</span><span class="sxs-lookup"><span data-stu-id="12f32-311">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-intellisense-is-not-available-in-webmatrix-for-razor-syntax-c-or-visual-basic"></a><span data-ttu-id="12f32-312">問題： Razor 語法、 C#或的 WebMatrix 無法使用 IntelliSense Visual Basic</span><span class="sxs-lookup"><span data-stu-id="12f32-312">Issue: IntelliSense is not available in WebMatrix for Razor syntax, C#, or Visual Basic</span></span>

> <span data-ttu-id="12f32-313">HTML 和 CSS 的 WebMatrix 支援 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="12f32-313">IntelliSense is supported in WebMatrix for HTML and CSS.</span></span> <span data-ttu-id="12f32-314">不過，它不適用於其他語言。</span><span class="sxs-lookup"><span data-stu-id="12f32-314">However, it is not available for other languages.</span></span> 
> 
> <span data-ttu-id="12f32-315">因應\*\*措施 \*\*</span><span class="sxs-lookup"><span data-stu-id="12f32-315">**Workaround** </span></span>  
> <span data-ttu-id="12f32-316">無。</span><span class="sxs-lookup"><span data-stu-id="12f32-316">None.</span></span>

#### <a name="issue-intellisense-for-html-and-css-suggests-elements-that-are-not-contextually-appropriate"></a><span data-ttu-id="12f32-317">問題： HTML 和 CSS 的 IntelliSense 建議不適合內容的元素</span><span class="sxs-lookup"><span data-stu-id="12f32-317">Issue: IntelliSense for HTML and CSS suggests elements that are not contextually appropriate</span></span>

> <span data-ttu-id="12f32-318">WebMatrix 中標記的 IntelliSense 支援使用[XHTML 1.0 轉換架構](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional)的 HTML，以及使用[css 2.1 架構](http://www.w3.org/TR/CSS2/)的 css。</span><span class="sxs-lookup"><span data-stu-id="12f32-318">IntelliSense for markup in WebMatrix supports HTML using the [XHTML 1.0 Transitional schema](http://www.w3.org/TR/2002/NOTE-xhtml1-schema-20020902/#xhtml1-transitional) and CSS using the [CSS 2.1 schema](http://www.w3.org/TR/CSS2/).</span></span> <span data-ttu-id="12f32-319">由於 IntelliSense 是以這些特定的架構為基礎，因此可能會建議某些標記、屬性或屬性，而不適合目前的頁面或樣式定義。</span><span class="sxs-lookup"><span data-stu-id="12f32-319">Because IntelliSense is based on these specific schemas, certain tags, attributes, or properties might be suggested that are not appropriate for the current page or style definition.</span></span> <span data-ttu-id="12f32-320">若是 HTML，它也可能會導致內容中的未預期建議，可能會被視為格式不正確的 XHTML （例如，當標記未關閉時）。</span><span class="sxs-lookup"><span data-stu-id="12f32-320">For HTML, it can also lead to unexpected suggestions in content that might be interpreted as malformed XHTML (for example, when tags are not closed).</span></span> <span data-ttu-id="12f32-321">如果插入點位於不完整的標記內，這個問題可能會更明顯;在此情況下，IntelliSense 可能會建議新的開頭標記，或提供其他不正確的建議。</span><span class="sxs-lookup"><span data-stu-id="12f32-321">This issue might be more noticeable if the insertion point is inside an incomplete tag; in that case, IntelliSense might suggest new opening tags or offer other incorrect suggestions.</span></span> 
> 
> <span data-ttu-id="12f32-322">因應\*\*措施 \*\*</span><span class="sxs-lookup"><span data-stu-id="12f32-322">**Workaround** </span></span>  
> <span data-ttu-id="12f32-323">若是 HTML，請確定您是在格式正確的完整 XHTML 頁面中工作。</span><span class="sxs-lookup"><span data-stu-id="12f32-323">For HTML, make sure that you are working within a well-formed, complete XHTML page.</span></span> <span data-ttu-id="12f32-324">針對 CSS，沒有因應措施。</span><span class="sxs-lookup"><span data-stu-id="12f32-324">For CSS, there is no workaround.</span></span>

#### <a name="issue-intellisense-is-not-invoked-while-you-type"></a><span data-ttu-id="12f32-325">問題：當您輸入時，不會叫用 IntelliSense</span><span class="sxs-lookup"><span data-stu-id="12f32-325">Issue: IntelliSense is not invoked while you type</span></span>

> <span data-ttu-id="12f32-326">有時，IntelliSense 可能不會在編輯器中輸入 HTML 或 CSS 時叫用。</span><span class="sxs-lookup"><span data-stu-id="12f32-326">At times, IntelliSense might not be invoked as HTML or CSS is being entered in the editor.</span></span> <span data-ttu-id="12f32-327">特別是，當插入點是直接在另一個專案旁邊或在檔案結尾處時，就可能發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="12f32-327">In particular, this might happen when the insertion point is directly next to another element or at the end of a file.</span></span> 
> 
> <span data-ttu-id="12f32-328">因應\*\*措施 \*\*</span><span class="sxs-lookup"><span data-stu-id="12f32-328">**Workaround** </span></span>  
> <span data-ttu-id="12f32-329">請確定插入點周圍有空白字元，而且插入點不在檔案結尾。</span><span class="sxs-lookup"><span data-stu-id="12f32-329">Make sure that there is whitespace around the insertion point and that the insertion point is not at the end of a file.</span></span> <span data-ttu-id="12f32-330">您也可以按下 Ctrl + 空格鍵，手動叫用 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="12f32-330">You can also invoke IntelliSense manually by pressing Ctrl+Space.</span></span>

#### <a name="issue-no-ui-is-available-for-disabling-intellisense"></a><span data-ttu-id="12f32-331">問題：沒有可用來停用 IntelliSense 的 UI</span><span class="sxs-lookup"><span data-stu-id="12f32-331">Issue: No UI is available for disabling IntelliSense</span></span>

> <span data-ttu-id="12f32-332">WebMatrix 1.0 不提供任何 UI 或手勢來停用 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="12f32-332">WebMatrix 1.0 provides no UI or gesture for disabling IntelliSense.</span></span> 
> 
> <span data-ttu-id="12f32-333">因應\*\*措施 \*\*</span><span class="sxs-lookup"><span data-stu-id="12f32-333">**Workaround** </span></span>  
> <span data-ttu-id="12f32-334">使用下列命令啟動 WebMatrix，其中包括停用 IntelliSense 的交換器：</span><span class="sxs-lookup"><span data-stu-id="12f32-334">Start WebMatrix using the following command, which includes a switch that disables IntelliSense:</span></span>  
>   
> `WebMatrix.exe #ExecuteCommand# EditorIntelliSense off`

<a id="Known_Issues_IISExpress"></a>
### <a name="iis-express"></a><span data-ttu-id="12f32-335">IIS Express</span><span class="sxs-lookup"><span data-stu-id="12f32-335">IIS Express</span></span>

<span data-ttu-id="12f32-336">IIS Express 有自己的讀我檔案，可在下列 URL 取得：</span><span class="sxs-lookup"><span data-stu-id="12f32-336">IIS Express has its own readme file, which is available at the following URL:</span></span>

[<span data-ttu-id="12f32-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp; clcid = 0x409</span><span class="sxs-lookup"><span data-stu-id="12f32-337">https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409</span></span>](https://go.microsoft.com/fwlink/?LinkID=207675&amp;clcid=0x409)

<a id="Known_Issues_SQLServerCompact"></a>

### <a name="sql-server-compact"></a><span data-ttu-id="12f32-338">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="12f32-338">SQL Server Compact</span></span>

<span data-ttu-id="12f32-339">SQL Server Compact 有自己的讀我檔案，可在下列 URL 取得：</span><span class="sxs-lookup"><span data-stu-id="12f32-339">SQL Server Compact has its own readme file, which is available at the following URL:</span></span>

[https://go.microsoft.com/fwlink/?LinkID=208545](https://go.microsoft.com/fwlink/?LinkID=208545&amp;clcid=0x409)

<span data-ttu-id="12f32-340">如需有關在 WebMatrix 中安裝 SQL Server Compact 之問題的詳細資訊，請參閱本檔稍早的[WebMatrix 安裝問題](#Known_Issues_Installation)。</span><span class="sxs-lookup"><span data-stu-id="12f32-340">For information about issues that involve installing SQL Server Compact as part of WebMatrix, see [WebMatrix Installation Issues](#Known_Issues_Installation) earlier in this document.</span></span>

### <a id="Known_Issues_Installing_Applications"></a><span data-ttu-id="12f32-341">安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="12f32-341">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="12f32-342">問題：如果使用者的 [我的文件] 資料夾重新導向到網路共用，則安裝應用程式可能需要很長的時間</span><span class="sxs-lookup"><span data-stu-id="12f32-342">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="12f32-343">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-343">**Workaround**</span></span>  
> <span data-ttu-id="12f32-344">無。</span><span class="sxs-lookup"><span data-stu-id="12f32-344">None.</span></span> <span data-ttu-id="12f32-345">應用程式可能需要一些時間來安裝，但會正確安裝。</span><span class="sxs-lookup"><span data-stu-id="12f32-345">The application might take a while to install, but will install correctly.</span></span>

### <a id="Known_Issues_Publishing_Applications"></a><span data-ttu-id="12f32-346">發行應用程式</span><span class="sxs-lookup"><span data-stu-id="12f32-346">Publishing Applications</span></span>

#### <a name="issue-required-permissions-cannot-be-acquired-error-when-publishing-a-sql-compact-database"></a><span data-ttu-id="12f32-347">問題：發行 SQL Compact 資料庫時發生「無法取得必要許可權」錯誤</span><span class="sxs-lookup"><span data-stu-id="12f32-347">Issue: "Required permissions cannot be acquired" error when publishing a SQL Compact Database</span></span>

> <span data-ttu-id="12f32-348">WebMatrix 並不完全支援使用中度信任設定，將 SQL Server Compact 的支援二進位檔部署至執行 .NET Framework 3.5 版的伺服器。</span><span class="sxs-lookup"><span data-stu-id="12f32-348">WebMatrix does not fully support deploying supporting binaries for SQL Server Compact to a server that is running .NET Framework version 3.5 with a medium trust configuration.</span></span>
> 
> <span data-ttu-id="12f32-349">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-349">**Workaround**</span></span>  
> <span data-ttu-id="12f32-350">慣用的解決方法是在伺服器上安裝 .NET Framework 4。</span><span class="sxs-lookup"><span data-stu-id="12f32-350">The preferred workaround is to install the .NET Framework 4 on the server.</span></span> <span data-ttu-id="12f32-351">或者，執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="12f32-351">Alternatively, do the following:</span></span>
> 
> 1. <span data-ttu-id="12f32-352">將下列元素新增至*Web\_MediumTrust*中的 `SecurityClasses` 區段：</span><span class="sxs-lookup"><span data-stu-id="12f32-352">Add the following elements to the `SecurityClasses` section in *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample6.html)]
> 2. <span data-ttu-id="12f32-353">在*Web\_MediumTrust*中，使用下列必要許可權建立新的許可權集合：</span><span class="sxs-lookup"><span data-stu-id="12f32-353">Create a new permission set in the *Web\_MediumTrust.config* file with the following required permissions:</span></span>
> 
>     [!code-html[Main](overview/samples/sample7.html)]
> 3. <span data-ttu-id="12f32-354">將下列元素放在*Web\_MediumTrust*中，將許可權集合套用至 SQL Server Compact：</span><span class="sxs-lookup"><span data-stu-id="12f32-354">Apply the permission set to SQL Server Compact by putting the following elements in the *Web\_MediumTrust.config* file:</span></span>
> 
>     [!code-html[Main](overview/samples/sample8.html)]

#### <a name="issue-gallery-and-phpbb-web-applications-display-a-service-is-unavailable-error-after-publishing"></a><span data-ttu-id="12f32-355">問題：資源庫和 PhpBB web 應用程式在發佈後顯示「服務無法使用」錯誤</span><span class="sxs-lookup"><span data-stu-id="12f32-355">Issue: Gallery and PhpBB web applications display a "Service is unavailable" error after publishing</span></span>

> <span data-ttu-id="12f32-356">在某些情況下，發行應用程式會導致「服務無法使用」錯誤。</span><span class="sxs-lookup"><span data-stu-id="12f32-356">Under some circumstances, publishing an application causes a "service is unavailable" error.</span></span>
> 
> <span data-ttu-id="12f32-357">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-357">**Workaround**</span></span>  
> <span data-ttu-id="12f32-358">在 WebMatrix 中，于 [**發佈設定**] 視窗中的伺服器名稱結尾新增反斜線（\)，然後再次發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="12f32-358">In WebMatrix, add a backslash (\) to the end of the server name in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-moodle-website-layout-and-links-are-broken-after-publishing"></a><span data-ttu-id="12f32-359">問題： Moodle 網站版面配置和連結在發佈之後中斷</span><span class="sxs-lookup"><span data-stu-id="12f32-359">Issue: Moodle website layout and links are broken after publishing</span></span>

> <span data-ttu-id="12f32-360">在您發佈 Moodle 應用程式之後，應用程式無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="12f32-360">After you publish a Moodle application, the application does not work correctly.</span></span>
> 
> <span data-ttu-id="12f32-361">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-361">**Workaround**</span></span>  
> <span data-ttu-id="12f32-362">在 WebMatrix 中，于 [**發佈設定**] 視窗中的 [**網站名稱**] 欄位結尾加上斜線（/），然後再次發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="12f32-362">In WebMatrix, add a slash (/) to the end of the **Site Name** field in the **Publish Settings** window and then publish the application again.</span></span>

#### <a name="issue-publishing-nopcommerce-fails-with-a-database-error"></a><span data-ttu-id="12f32-363">問題：發行 nopCommerce 失敗，發生資料庫錯誤</span><span class="sxs-lookup"><span data-stu-id="12f32-363">Issue: Publishing nopCommerce fails with a database error</span></span>

> <span data-ttu-id="12f32-364">發行 nopCommerce 失敗並報告資料庫錯誤，例如「插入 nop\_記錄資料表失敗。」</span><span class="sxs-lookup"><span data-stu-id="12f32-364">Publishing nopCommerce fails and reports a database error like "Insert into the nop\_log table failed."</span></span>
> 
> <span data-ttu-id="12f32-365">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-365">**Workaround**</span></span>  
> 
> 1. <span data-ttu-id="12f32-366">在 WebMatrix 中，按一下 [**執行**] 以在本機啟動 nopCommerce。</span><span class="sxs-lookup"><span data-stu-id="12f32-366">In WebMatrix, click **Run** to launch nopCommerce locally.</span></span>
> 2. <span data-ttu-id="12f32-367">登入 [系統管理] 頁面。</span><span class="sxs-lookup"><span data-stu-id="12f32-367">Log into the administration page.</span></span>
> 3. <span data-ttu-id="12f32-368">按一下 [**系統**] 功能表。</span><span class="sxs-lookup"><span data-stu-id="12f32-368">Click the **System** menu.</span></span>
> 4. <span data-ttu-id="12f32-369">按一下 [**記錄**檔] 選項。</span><span class="sxs-lookup"><span data-stu-id="12f32-369">Click the **Log** option.</span></span>
> 5. <span data-ttu-id="12f32-370">按一下 [**清除記錄**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="12f32-370">Click the **Clear Log** button.</span></span>
> 6. <span data-ttu-id="12f32-371">再次發佈 nopCommerce。</span><span class="sxs-lookup"><span data-stu-id="12f32-371">Publish nopCommerce again.</span></span>

#### <a name="issue-silverstripe-cms-displays-a-http-500-php-fcgi-error-when-you-download-a-published-site"></a><span data-ttu-id="12f32-372">問題：當您下載已發佈的網站時，Silverstripe CMS 會顯示「HTTP 500 PHP HANDLER.FCGI 錯誤」</span><span class="sxs-lookup"><span data-stu-id="12f32-372">Issue: Silverstripe CMS displays a "HTTP 500 PHP FCGI Error" when you download a published site</span></span>

> <span data-ttu-id="12f32-373">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-373">**Workaround**</span></span>  
> <span data-ttu-id="12f32-374">按一下 [**下載發佈的網站**] 之後，請略過 [**發行預覽**] 中的 `silverstripe-cache/manifest_main`。</span><span class="sxs-lookup"><span data-stu-id="12f32-374">After you click **Download published site**, skip `silverstripe-cache/manifest_main` in **Publish Preview**.</span></span> <span data-ttu-id="12f32-375">這個檔案是用於快取用途，而且是每部電腦特有的檔案。</span><span class="sxs-lookup"><span data-stu-id="12f32-375">This file is used for caching purposes and is specific to each computer.</span></span>

#### <a name="issue-subtext-displays-server-error-in--application-when-you-download-a-published-site"></a><span data-ttu-id="12f32-376">問題：當您下載發佈的網站時，會顯示「在 '/' 應用程式中發生伺服器錯誤」的子集</span><span class="sxs-lookup"><span data-stu-id="12f32-376">Issue: Subtext displays "Server Error in '/' Application" when you download a published site</span></span>

> <span data-ttu-id="12f32-377">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-377">**Workaround**</span></span>  
> <span data-ttu-id="12f32-378">開啟網站的*web.config*檔案，並以 SQL Server 系統管理員認證（"sa" 認證）取代資料庫連接字串中的使用者識別碼和密碼。</span><span class="sxs-lookup"><span data-stu-id="12f32-378">Open the site's *web.config* file and replace the user ID and password in the database connection string with the SQL Server administrator credentials (the "sa" credentials).</span></span>
> 
> <span data-ttu-id="12f32-379">或者，請遵循下列步驟，將您使用 `db_owner` 許可權登入的使用者帳戶提供給您：</span><span class="sxs-lookup"><span data-stu-id="12f32-379">Alternatively, follow these steps in order to give the user account you are logged in with `db_owner` permissions:</span></span>
> 
> 1. <span data-ttu-id="12f32-380">使用 Web Platform Installer 安裝 SQL Server Management Studio。</span><span class="sxs-lookup"><span data-stu-id="12f32-380">Install SQL Server Management Studio using the Web Platform Installer.</span></span>
> 2. <span data-ttu-id="12f32-381">連接到本機 SQL Server Express 實例（根據預設，`.\SQLEXPRESS`）。</span><span class="sxs-lookup"><span data-stu-id="12f32-381">Connect to the local SQL Server Express instance (by default, `.\SQLEXPRESS`).</span></span>
> 3. <span data-ttu-id="12f32-382">按一下 [資料庫 *] &gt; [LocalSubtextDatabase]* &gt;**安全性**&gt;**使用者**&gt; *[localSubtextUser*] （預設值為 `subtextuser`，按一下滑鼠右鍵，然後按一下 [**屬性**]。</span><span class="sxs-lookup"><span data-stu-id="12f32-382">Click **Databases** &gt; *[localSubtextDatabase]* &gt; **Security** &gt; **Users** &gt; *[localSubtextUser*] (default is `subtextuser`], right-click, and click **Properties**.</span></span>
> 4. <span data-ttu-id="12f32-383">在 [角色成員資格] 區段中選取 [ **db\_擁有**者]。</span><span class="sxs-lookup"><span data-stu-id="12f32-383">Select **db\_owner** in the role membership section.</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="12f32-384">問題：如果 [目的地 URL] 欄位未在前面加上 HTTP://或 HTTPs://，網站在發佈後可能無法正常執行</span><span class="sxs-lookup"><span data-stu-id="12f32-384">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="12f32-385">在 [**發行設定**] 對話方塊中，如果目的地 URL 不是以 `http://` 或 `https://`開頭，則在部署之後，網站可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="12f32-385">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="12f32-386">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-386">**Workaround**</span></span>  
> <span data-ttu-id="12f32-387">在發佈網站之前，請確定 [**發行設定**] 對話方塊中的 [目的地 URL] 開頭為 [`http://`] 或 [`https://`]。</span><span class="sxs-lookup"><span data-stu-id="12f32-387">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="12f32-388">問題：發行 MySQL 資料庫失敗，錯誤為「無法發行資料庫。</span><span class="sxs-lookup"><span data-stu-id="12f32-388">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="12f32-389">如果遠端資料庫無法執行腳本，就會發生這種情況。」</span><span class="sxs-lookup"><span data-stu-id="12f32-389">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="12f32-390">發生此錯誤的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="12f32-390">The error can occur for a number of reasons.</span></span> <span data-ttu-id="12f32-391">您可以看到此錯誤的其中一個原因是，資料庫腳本包含單引號字元（'），而目的地 MySQL 資料庫的預設字元集不是 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="12f32-391">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="12f32-392">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-392">**Workaround**</span></span>  
> <span data-ttu-id="12f32-393">將遠端 MySQL 資料庫的預設字元集設定為 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="12f32-393">Set the default character set for the remote MySQL database to UTF-8.</span></span>

#### <a name="issue-some-links-are-not-visible-in-dotnetnuke-after-publishing-or-downloading-the-site"></a><span data-ttu-id="12f32-394">問題：發佈或下載網站後，在 DotNetNuke 中看不到某些連結</span><span class="sxs-lookup"><span data-stu-id="12f32-394">Issue: Some links are not visible in DotNetNuke after publishing or downloading the site</span></span>

> <span data-ttu-id="12f32-395">如果您發佈或下載 DotNetNuke 網站，您可能需要清除快取，才能讓新連結出現在網站上。</span><span class="sxs-lookup"><span data-stu-id="12f32-395">If you publish or download a DotNetNuke site, you might need to clear the cache to get the new links to appear on the site.</span></span>
> 
> <span data-ttu-id="12f32-396">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-396">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="12f32-397">以「主機」的身分登入。</span><span class="sxs-lookup"><span data-stu-id="12f32-397">Log in as "Host".</span></span>
> 2. <span data-ttu-id="12f32-398">移至 [主機] 功能表並選取 [**主機設定**]。</span><span class="sxs-lookup"><span data-stu-id="12f32-398">Go to the host menu and select **Host Settings**.</span></span>
> 3. <span data-ttu-id="12f32-399">在 [**高級設定**] 底下，展開 [**效能設定**]。</span><span class="sxs-lookup"><span data-stu-id="12f32-399">Scroll down and under **Advanced Settings**, expand **Performance Settings**.</span></span>
> 4. <span data-ttu-id="12f32-400">按一下 [**清除**快取] 連結以取得頁面。</span><span class="sxs-lookup"><span data-stu-id="12f32-400">Click the **Clear Cache** link for pages.</span></span>
> 5. <span data-ttu-id="12f32-401">移至頁面底部，然後重新開機應用程式。</span><span class="sxs-lookup"><span data-stu-id="12f32-401">Go to the bottom of the page and restart the application.</span></span>

#### <a name="issue-some-links-in-atomsite-are-broken-after-you-download-a-published-site"></a><span data-ttu-id="12f32-402">問題： AtomSite 中的某些連結在您下載發佈的網站之後中斷</span><span class="sxs-lookup"><span data-stu-id="12f32-402">Issue: Some links in AtomSite are broken after you download a published site</span></span>

> <span data-ttu-id="12f32-403">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-403">**Workaround**</span></span>  
> <span data-ttu-id="12f32-404">在*app.config*檔案中，*使用者 .config*檔案和所有 *.XML*檔案中，將 URL 字串（例如，`http://myhost.com/atomsite`）取代為本機檔案（例如，`http://localhost:1239`）。</span><span class="sxs-lookup"><span data-stu-id="12f32-404">In the *service.config* file, *users.config* file, and all *.xml* files, replace the URL string (for example, `http://myhost.com/atomsite`) with the local one (for example, `http://localhost:1239`).</span></span>

#### <a name="issue-mysql-based-applications-like-wordpress-fail-to-publish-and-report-a-database-error"></a><span data-ttu-id="12f32-405">問題：以 MySQL 為基礎的應用程式（例如 WordPress）無法發佈和報告資料庫錯誤</span><span class="sxs-lookup"><span data-stu-id="12f32-405">Issue: MySQL-based applications like WordPress fail to publish and report a database error</span></span>

> <span data-ttu-id="12f32-406">根據預設，WebMatrix 會安裝具有 UTF-8 字元集的 MySQL。</span><span class="sxs-lookup"><span data-stu-id="12f32-406">By default, WebMatrix installs MySQL with the UTF-8 character set.</span></span> <span data-ttu-id="12f32-407">如果您自行安裝 MySQL，而字元集不是 UTF-8 （例如，它是採用 latin1-general），則資料庫的發行進程可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="12f32-407">If you install MySQL on your own, and the character set is not UTF-8 (for example, it is Latin1), the publish process for databases might fail.</span></span>
> 
> <span data-ttu-id="12f32-408">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-408">**Workaround**</span></span>
> 
> 1. <span data-ttu-id="12f32-409">將 MySQL 的字元集設定為 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="12f32-409">Change the character set for MySQL to UTF-8.</span></span> <span data-ttu-id="12f32-410">（如需詳細資訊，請參閱 MySQL 網站上的[伺服器字元集和定序](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html)）。</span><span class="sxs-lookup"><span data-stu-id="12f32-410">(For details, see [Server Character Set and Collation](http://dev.mysql.com/doc/refman/5.0/en/charset-server.html) on the MySQL website.)</span></span>
> 2. <span data-ttu-id="12f32-411">重新安裝應用程式。</span><span class="sxs-lookup"><span data-stu-id="12f32-411">Reinstall the application.</span></span>
> 3. <span data-ttu-id="12f32-412">重新發佈應用程式。</span><span class="sxs-lookup"><span data-stu-id="12f32-412">Republish the application.</span></span>

#### <a name="issue-download-published-site-fails-for-applications-that-have-browser-based-setup"></a><span data-ttu-id="12f32-413">問題：如果應用程式具有以瀏覽器為基礎的設定，「下載發佈的網站」會失敗</span><span class="sxs-lookup"><span data-stu-id="12f32-413">Issue: "Download published site" fails for applications that have browser-based setup</span></span>

> <span data-ttu-id="12f32-414">某些應用程式（例如 Kentico CMS）會要求您在瀏覽器中啟動它們，以便執行安裝後的設定，例如建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="12f32-414">Some applications (for example, Kentico CMS) require you to launch them in the browser in order to perform post-installation setup such as creating a database.</span></span> <span data-ttu-id="12f32-415">如果您發佈這類應用程式，但未完成以瀏覽器為基礎的安裝程式，則嘗試從遠端伺服器下載相同的網站將會失敗。</span><span class="sxs-lookup"><span data-stu-id="12f32-415">If you publish an application like this without completing the browser-based setup, attempting to download the same site from a remote server will fail.</span></span>
> 
> <span data-ttu-id="12f32-416">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-416">**Workaround**</span></span>  
> <span data-ttu-id="12f32-417">發行網站之前，請先完成以瀏覽器為基礎的安裝程式。</span><span class="sxs-lookup"><span data-stu-id="12f32-417">Finish browser-based setup before publishing the site.</span></span>

#### <a name="issue-download-published-site-fails-with-a-database-error-for-dotnetnuke-and-kooboo-cms"></a><span data-ttu-id="12f32-418">問題：「下載發佈的網站」失敗並出現資料庫錯誤，DotNetNuke 和 Kooboo CMS</span><span class="sxs-lookup"><span data-stu-id="12f32-418">Issue: "Download published site" fails with a database error for DotNetNuke and Kooboo CMS</span></span>

> <span data-ttu-id="12f32-419">如果您嘗試從伺服器下載應用程式，而且在 [**發行設定**] 對話方塊的資料庫連接字串中具有系統管理員認證，您可能會在發行記錄檔中看到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="12f32-419">If you try to download an application from a server and you have administrator credentials in the database connection string in the **Publish Settings** dialog, you might see the following error in the publish log:</span></span>
> 
> [!code-console[Main](overview/samples/sample9.cmd)]
> 
> <span data-ttu-id="12f32-420">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="12f32-420">**Workaround**</span></span>  
> <span data-ttu-id="12f32-421">如果可行，請使用資料庫的非系統管理員認證重新發佈網站（或已發佈）。</span><span class="sxs-lookup"><span data-stu-id="12f32-421">If practical, republish the site (or have it published) using non-administrator credentials for the database.</span></span>

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="12f32-422">取得更多資訊</span><span class="sxs-lookup"><span data-stu-id="12f32-422">For More Information</span></span>

<span data-ttu-id="12f32-423">如需有關 WebMatrix 1.0 的詳細資訊，請參閱下列網站：</span><span class="sxs-lookup"><span data-stu-id="12f32-423">For more information about WebMatrix 1.0, see the following websites:</span></span>

- [<span data-ttu-id="12f32-424">IIS.net</span><span class="sxs-lookup"><span data-stu-id="12f32-424">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="12f32-425">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="12f32-425">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="12f32-426">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="12f32-426">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

<span data-ttu-id="12f32-427">© 2011 Microsoft Corporation.</span><span class="sxs-lookup"><span data-stu-id="12f32-427">© 2011 Microsoft Corporation.</span></span> <span data-ttu-id="12f32-428">All Rights Reserved.</span><span class="sxs-lookup"><span data-stu-id="12f32-428">All Rights Reserved.</span></span> <span data-ttu-id="12f32-429">[使用條款](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="12f32-429">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
