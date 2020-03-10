---
uid: web-pages/readme/beta3
title: Web Matrix 和 ASP.NET Web Pages （Razor） Beta 3 版本讀我檔案 |Microsoft Docs
author: rick-anderson
description: Web Matrix 與 ASP.NET Web Pages (Razor) 搶鮮版 (Beta) 3 讀我檔案
ms.author: riande
ms.date: 01/10/2011
ms.assetid: ffa3d5c9-91e5-4da3-b409-560b0c7fbbf0
msc.legacyurl: /web-pages/readme/beta3
msc.type: content
ms.openlocfilehash: dc1d9237c04a7fcdbf4db6ccc8c36d255f6de003
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628895"
---
# <a name="web-matrix-and-aspnet-web-pages-razor-beta-3-release-readme"></a><span data-ttu-id="4aafc-103">Web Matrix 與 ASP.NET Web Pages (Razor) 搶鮮版 (Beta) 3 讀我檔案</span><span class="sxs-lookup"><span data-stu-id="4aafc-103">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

> <span data-ttu-id="4aafc-104">Web Matrix 與 ASP.NET Web Pages (Razor) 搶鮮版 (Beta) 3 讀我檔案</span><span class="sxs-lookup"><span data-stu-id="4aafc-104">Web Matrix and ASP.NET Web Pages (Razor) Beta 3 Release Readme</span></span>

<span data-ttu-id="4aafc-105">2010年11月9日</span><span class="sxs-lookup"><span data-stu-id="4aafc-105">9 November 2010</span></span>

## <a name="contents"></a><span data-ttu-id="4aafc-106">內容</span><span class="sxs-lookup"><span data-stu-id="4aafc-106">Contents</span></span>

- [<span data-ttu-id="4aafc-107">概觀</span><span class="sxs-lookup"><span data-stu-id="4aafc-107">Overview</span></span>](#Overview)
- [<span data-ttu-id="4aafc-108">安裝</span><span class="sxs-lookup"><span data-stu-id="4aafc-108">Installation</span></span>](#Installation_Notes)
- [<span data-ttu-id="4aafc-109">Beta 3 版本中的新功能、變更和已知問題</span><span class="sxs-lookup"><span data-stu-id="4aafc-109">New Features, Changes, and Known Issues in the Beta 3 release</span></span>](#Known_Issues)

    - [<span data-ttu-id="4aafc-110">WebMatrix 安裝問題</span><span class="sxs-lookup"><span data-stu-id="4aafc-110">WebMatrix Installation Issues</span></span>](#Known_Issues_Installation)
    - [<span data-ttu-id="4aafc-111">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="4aafc-111">ASP.NET Web Pages</span></span>](#Known_Issues_ASPNET)
    - [<span data-ttu-id="4aafc-112">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="4aafc-112">SQL Server Compact</span></span>](#Known_Issues_SQL_Server_Compact)
    - [<span data-ttu-id="4aafc-113">安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="4aafc-113">Installing Applications</span></span>](#Known_Issues_Installing_Applications)
    - [<span data-ttu-id="4aafc-114">發行應用程式</span><span class="sxs-lookup"><span data-stu-id="4aafc-114">Publishing Applications</span></span>](#Known_Issues_Publishing_Applications)
    - [<span data-ttu-id="4aafc-115">其他問題</span><span class="sxs-lookup"><span data-stu-id="4aafc-115">Other Issues</span></span>](#Known_Issues_Other_Issues)
- [<span data-ttu-id="4aafc-116">詳細資訊</span><span class="sxs-lookup"><span data-stu-id="4aafc-116">For More Information</span></span>](#More_Info)

<a id="Overview"></a>

## <a name="overview"></a><span data-ttu-id="4aafc-117">概觀</span><span class="sxs-lookup"><span data-stu-id="4aafc-117">Overview</span></span>

> <span data-ttu-id="4aafc-118">Microsoft WebMatrix Beta 是免費的 網頁程式開發堆疊，會在幾分鐘內安裝。</span><span class="sxs-lookup"><span data-stu-id="4aafc-118">Microsoft WebMatrix Beta is a free web development stack that installs in minutes.</span></span> <span data-ttu-id="4aafc-119">它會將網頁伺服器與資料庫和程式設計架構整合，以便建立單一且整合的使用經驗。</span><span class="sxs-lookup"><span data-stu-id="4aafc-119">It integrates a web server with database and programming frameworks to create a single, integrated experience.</span></span> <span data-ttu-id="4aafc-120">您可以使用 WebMatrix 搶鮮版（Beta）來簡化撰寫程式碼、測試及發佈自己的 ASP.NET 或 PHP 網站的方式，或者您可以使用 WebMatrix Beta 版，使用熱門的開放原始碼應用程式（例如 DotNetNuke、Umbraco、WordPress 或 Joomla）來啟動新的網站。</span><span class="sxs-lookup"><span data-stu-id="4aafc-120">You can use WebMatrix Beta to streamline the way you code, test, and publish your own ASP.NET or PHP website, or you can use WebMatrix Beta to start a new website using popular open-source apps like DotNetNuke, Umbraco, WordPress, or Joomla.</span></span> <span data-ttu-id="4aafc-121">WebMatrix 搶鮮版（Beta）使用的功能強大的 web 伺服器、資料庫引擎和架構環境，會在網際網路上執行您的網站，這使得從開發到生產環境的轉換順暢且順暢。</span><span class="sxs-lookup"><span data-stu-id="4aafc-121">WebMatrix Beta uses the same powerful web server, database engine, and frameworks environment that will run your website on the internet, which makes the transition from development to production smooth and seamless.</span></span>

<a id="Installation_Notes"></a>

## <a name="installation"></a><span data-ttu-id="4aafc-122">安裝</span><span class="sxs-lookup"><span data-stu-id="4aafc-122">Installation</span></span>

> <span data-ttu-id="4aafc-123">若要安裝 WebMatrix Beta 3，請使用[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="4aafc-123">To install WebMatrix Beta 3, you use [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span> <span data-ttu-id="4aafc-124">安裝 Web Platform Installer 之後，您就可以使用它來安裝 WebMatrix Beta 3。</span><span class="sxs-lookup"><span data-stu-id="4aafc-124">After you've installed the Web Platform Installer, you can use it to install WebMatrix Beta 3.</span></span>
> 
> <span data-ttu-id="4aafc-125">如果您在安裝期間遇到問題，請參閱[疑難排解 Microsoft Web Platform Installer 的問題](https://go.microsoft.com/fwlink/?LinkId=196212)。</span><span class="sxs-lookup"><span data-stu-id="4aafc-125">If you have problems during installation, refer to [Troubleshooting Problems with Microsoft Web Platform Installer](https://go.microsoft.com/fwlink/?LinkId=196212).</span></span>

<a id="Installation_Notes0"></a>

## <a name="instructions-for-publishing-applications"></a><span data-ttu-id="4aafc-126">發行應用程式的指示</span><span class="sxs-lookup"><span data-stu-id="4aafc-126">Instructions for Publishing Applications</span></span>

> <span data-ttu-id="4aafc-127">請參閱[發行應用程式的逐步指示](https://go.microsoft.com/fwlink/?LinkID=196149)</span><span class="sxs-lookup"><span data-stu-id="4aafc-127">See [Step-by-Step Instructions for Publishing Applications](https://go.microsoft.com/fwlink/?LinkID=196149)</span></span>

<a id="Known_Issues"></a>

## <a name="new-features-changes-andknown-issues"></a><span data-ttu-id="4aafc-128">新功能、變更、andKnown 問題</span><span class="sxs-lookup"><span data-stu-id="4aafc-128">New Features, Changes, andKnown Issues</span></span>

<a id="Known_Issues_Installation"></a>

### <a name="webmatrix-beta-3-installation"></a><span data-ttu-id="4aafc-129">WebMatrix Beta 3 安裝</span><span class="sxs-lookup"><span data-stu-id="4aafc-129">WebMatrix Beta 3 Installation</span></span>

#### <a name="issue-webmatrix-beta-3-is-only-available-on-platforms-that-support-microsoft-net-framework-4"></a><span data-ttu-id="4aafc-130">問題： WebMatrix 搶鮮版（Beta）3僅適用于支援 Microsoft .NET Framework 4 的平臺</span><span class="sxs-lookup"><span data-stu-id="4aafc-130">Issue: WebMatrix Beta 3 is only available on platforms that support Microsoft .NET Framework 4</span></span>

> <span data-ttu-id="4aafc-131">WebMatrix 搶鮮版（Beta）需要 .NET Framework 第4版。</span><span class="sxs-lookup"><span data-stu-id="4aafc-131">The .NET Framework version 4 is required for WebMatrix Beta.</span></span> <span data-ttu-id="4aafc-132">在某些情況下，WebMatrix 搶鮮版（Beta）安裝程式可讓您嘗試在不屬於受支援設定集的平臺上安裝。</span><span class="sxs-lookup"><span data-stu-id="4aafc-132">In certain cases, the WebMatrix Beta installer will let you try to install on a platform that is not part of the supported configuration set.</span></span> <span data-ttu-id="4aafc-133">特別是，沒有 SP1 更新的 Windows Vista 可讓您開始安裝 WebMatrix Beta，但 .NET Framework 4 元件將會失敗，並封鎖您的安裝。</span><span class="sxs-lookup"><span data-stu-id="4aafc-133">In particular, Windows Vista without the SP1 update will let you begin the installation of WebMatrix Beta, but the .NET Framework 4 component will fail and block your installation.</span></span>
> 
> <span data-ttu-id="4aafc-134">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-134">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-135">安裝在支援的平台上，包括：</span><span class="sxs-lookup"><span data-stu-id="4aafc-135">Install on a supported platform, which includes:</span></span>
> 
> - <span data-ttu-id="4aafc-136">Windows 7</span><span class="sxs-lookup"><span data-stu-id="4aafc-136">Windows 7</span></span>
> - <span data-ttu-id="4aafc-137">Windows Server 2008</span><span class="sxs-lookup"><span data-stu-id="4aafc-137">Windows Server 2008</span></span>
> - <span data-ttu-id="4aafc-138">Windows Server 2008 R2</span><span class="sxs-lookup"><span data-stu-id="4aafc-138">Windows Server 2008 R2</span></span>
> - <span data-ttu-id="4aafc-139">Windows Vista SP1 (含) 以後版本</span><span class="sxs-lookup"><span data-stu-id="4aafc-139">Windows Vista SP1 or later</span></span>
> - <span data-ttu-id="4aafc-140">Windows XP SP3</span><span class="sxs-lookup"><span data-stu-id="4aafc-140">Windows XP SP3</span></span>
> - <span data-ttu-id="4aafc-141">Windows Server 2003 SP2</span><span class="sxs-lookup"><span data-stu-id="4aafc-141">Windows Server 2003 SP2</span></span>

#### <a name="issue-cannot-install-webmatrix-beta-3-if-microsoft-visual-studio-2008-is-installed-without-microsoft-visual-studio-2008-sp1"></a><span data-ttu-id="4aafc-142">問題：如果安裝 Microsoft Visual Studio 2008 但未 Microsoft Visual Studio 2008 SP1，就無法安裝 WebMatrix Beta 3</span><span class="sxs-lookup"><span data-stu-id="4aafc-142">Issue: Cannot install WebMatrix Beta 3 if Microsoft Visual Studio 2008 is installed without Microsoft Visual Studio 2008 SP1</span></span>

> <span data-ttu-id="4aafc-143">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-143">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-144">從 Microsoft 下載中心安裝[Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) 。</span><span class="sxs-lookup"><span data-stu-id="4aafc-144">Install [Microsoft Visual Studio 2008 SP1](https://www.microsoft.com/downloads/details.aspx?FamilyId=FBEE1648-7106-44A7-9649-6D9F6D58056E&amp;displaylang=en) from the Microsoft Download Center.</span></span>

#### <a name="issue-some-assemblies-for-sql-server-compact-40-are-not-installed-in-the-gac"></a><span data-ttu-id="4aafc-145">問題：SQL Server Compact 4.0 的某些組件不會安裝在 GAC 中</span><span class="sxs-lookup"><span data-stu-id="4aafc-145">Issue: Some assemblies for SQL Server Compact 4.0 are not installed in the GAC</span></span>

> <span data-ttu-id="4aafc-146">當您在 64 位元電腦上安裝 SQL Server Compact 4.0，而且該電腦只安裝了 .NET Framework 3.5 SP1 Client Profile 時，SQL Server Compact 4.0 的 Managed 組件就不會放置於全域組件快取 (GAC) 中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-146">The managed assemblies for SQL Server Compact 4.0 are not placed in the global assembly cache (GAC) when you install SQL Server Compact 4.0 on a 64-bit computer and the computer has only the .NET Framework 3.5 SP1 Client Profile installed.</span></span> <span data-ttu-id="4aafc-147">不會安裝在 GAC 中的 Managed 組件包括：</span><span class="sxs-lookup"><span data-stu-id="4aafc-147">The managed assemblies that are not installed in the GAC are:</span></span>
> 
> - <span data-ttu-id="4aafc-148">*System.data.sqlserverce .dll* （ADO.NET 提供者）</span><span class="sxs-lookup"><span data-stu-id="4aafc-148">*System.Data.SqlServerCe.dll* (ADO.NET provider)</span></span>
> - <span data-ttu-id="4aafc-149">*System.data.sqlserverce. Entity* .dll （ADO.NET Entity Framework）</span><span class="sxs-lookup"><span data-stu-id="4aafc-149">*System.Data.SqlServerCe.Entity.dll* (ADO.NET Entity Framework )</span></span>
> 
> <span data-ttu-id="4aafc-150">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-150">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-151">解除安裝 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="4aafc-151">Uninstall SQL Server Compact 4.0.</span></span> <span data-ttu-id="4aafc-152">從下列位置下載並安裝 .NET Framework 3.5 SP1 完整版本：</span><span class="sxs-lookup"><span data-stu-id="4aafc-152">Download and install the full version of .NET Framework 3.5 SP1 from the following location:</span></span>  
>   
> [<span data-ttu-id="4aafc-153">Microsoft .NET Framework 3.5 Service pack 1 （完整套件）</span><span class="sxs-lookup"><span data-stu-id="4aafc-153">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
>   
> <span data-ttu-id="4aafc-154">然後重新安裝 SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="4aafc-154">Then reinstall SQL Server Compact 4.0.</span></span>

#### <a name="issue-cannot-uninstall-sql-server-compact-using-the-command-line"></a><span data-ttu-id="4aafc-155">問題：無法使用命令列解除安裝 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="4aafc-155">Issue: Cannot uninstall SQL Server Compact using the command line</span></span>

> <span data-ttu-id="4aafc-156">在這個版本中，使用命令列選項解除安裝 SQL Server Compact 沒有作用。</span><span class="sxs-lookup"><span data-stu-id="4aafc-156">Uninstallation of SQL Server Compact using command-line options does not work in this release.</span></span>
> 
> <span data-ttu-id="4aafc-157">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-157">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-158">使用 Windows [控制台] 中的 [*程式和功能*] 卸載 Microsoft SQL Server Compact 4.0。</span><span class="sxs-lookup"><span data-stu-id="4aafc-158">Use *Programs and Features* in the Windows Control Panel to uninstall Microsoft SQL Server Compact 4.0.</span></span>

<a id="Known_Issues_ASPNET"></a>

### <a name="aspnet-web-pages"></a><span data-ttu-id="4aafc-159">ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="4aafc-159">ASP.NET Web Pages</span></span>

<span data-ttu-id="4aafc-160">本檔的這一節描述具有 Razor 語法之 ASP.NET Web Pages Beta 3 版本的新功能、變更和已知問題。</span><span class="sxs-lookup"><span data-stu-id="4aafc-160">This section of the document describes new features, changes, and known issues with the Beta 3 release of ASP.NET Web Pages with Razor syntax.</span></span>

- [<span data-ttu-id="4aafc-161">新功能</span><span class="sxs-lookup"><span data-stu-id="4aafc-161">New features</span></span>](#NewFeatures)
- [<span data-ttu-id="4aafc-162">變更</span><span class="sxs-lookup"><span data-stu-id="4aafc-162">Changes</span></span>](#Changes)
- [<span data-ttu-id="4aafc-163">問題</span><span class="sxs-lookup"><span data-stu-id="4aafc-163">Issues</span></span>](#Issues)

<a id="NewFeatures"></a>

#### <a name="new-features-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="4aafc-164">Beta 3 的新功能，適用于使用 Razor 語法的 ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="4aafc-164">New Features in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="new-htmlraw-method-renders-unencoded-markup"></a><span data-ttu-id="4aafc-165">New： ".Html" 方法會轉譯未編碼的標記</span><span class="sxs-lookup"><span data-stu-id="4aafc-165">New: "Html.Raw" method renders unencoded markup</span></span>

> <span data-ttu-id="4aafc-166">新的 `Html.Raw` 方法可讓您將 HTML 標籤呈現為標記，而不是轉譯編碼的輸出。</span><span class="sxs-lookup"><span data-stu-id="4aafc-166">The new `Html.Raw` method lets you render HTML markup as markup instead of rendering encoded output.</span></span> <span data-ttu-id="4aafc-167">（根據預設，ASP.NET Razor 會先編碼字串，再進行轉譯）。語法為：</span><span class="sxs-lookup"><span data-stu-id="4aafc-167">(By default, ASP.NET Razor encodes strings before rendering them.) The syntax is:</span></span>
> 
> `Html.Raw(value)`
> 
> <span data-ttu-id="4aafc-168">下列範例顯示如何使用 `Html.Raw`：</span><span class="sxs-lookup"><span data-stu-id="4aafc-168">The following example shows how to use `Html.Raw`:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample1.cshtml)]

<a id="Changes"></a>

#### <a name="changes-in-beta-3-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="4aafc-169">Beta 3 中使用 Razor 語法進行 ASP.NET Web Pages 的變更</span><span class="sxs-lookup"><span data-stu-id="4aafc-169">Changes in Beta 3 for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="change-hrefattribute-method-removed"></a><span data-ttu-id="4aafc-170">變更：已移除 "HrefAttribute" 方法</span><span class="sxs-lookup"><span data-stu-id="4aafc-170">Change: "HrefAttribute" method removed</span></span>

> <span data-ttu-id="4aafc-171">已移除 `WebPage` 類別的 `HrefAttribute` 方法。</span><span class="sxs-lookup"><span data-stu-id="4aafc-171">The `HrefAttribute` method of the `WebPage` class has been removed.</span></span> <span data-ttu-id="4aafc-172">此 helper 是用來編碼 Url 中的不安全字元。</span><span class="sxs-lookup"><span data-stu-id="4aafc-172">This helper was used to encode unsafe characters in URLs.</span></span> <span data-ttu-id="4aafc-173">已不再需要它，因為 ASP.NET Razor 會自動將字串編碼。</span><span class="sxs-lookup"><span data-stu-id="4aafc-173">It is no longer required because ASP.NET Razor automatically encodes strings.</span></span> <span data-ttu-id="4aafc-174">（使用新的 `Html.Raw` 方法來呈現未編碼的字串）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-174">(Use the new `Html.Raw` method to render unencoded strings.)</span></span>

#### <a name="change-syntax-for-declarative-helper-helpers-changed"></a><span data-ttu-id="4aafc-175">變更：宣告式 "@helper" 協助程式的語法已變更</span><span class="sxs-lookup"><span data-stu-id="4aafc-175">Change: Syntax for declarative "@helper" helpers changed</span></span>

> <span data-ttu-id="4aafc-176">在 Beta 3 版本中，ASP.NET 會變更如何剖析使用 `@helper` 語法所建立的協助程式。</span><span class="sxs-lookup"><span data-stu-id="4aafc-176">In the Beta 3 release, ASP.NET changes how it parses helpers that are created using the `@helper` syntax.</span></span> <span data-ttu-id="4aafc-177">基本上，`@helper` 語法現在會剖析為程式碼區塊，而不是會剖析為可包含程式碼的標記區塊。</span><span class="sxs-lookup"><span data-stu-id="4aafc-177">In essence, the `@helper` syntax is now parsed as a code block instead of as a block of markup that can include code.</span></span> <span data-ttu-id="4aafc-178">因此，helper 內的程式碼不需要括在 `@{ }` 區塊中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-178">Therefore, code inside the helper does not need to be enclosed in `@{ }` blocks.</span></span> <span data-ttu-id="4aafc-179">相反地，helper 內的標記必須明確包含在 HTML 元素中，或 ASP.NET Razor `<text></text>` 標籤中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-179">Conversely, markup inside the helper has to be explicitly included in HTML elements or in ASP.NET Razor `<text></text>` tags.</span></span>
> 
> <span data-ttu-id="4aafc-180">例如，下列 `@helper` 語法適用于 Beta 3 版：</span><span class="sxs-lookup"><span data-stu-id="4aafc-180">For example, the following `@helper` syntax works in the Beta 3 release:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample2.cshtml)]
> 
> <span data-ttu-id="4aafc-181">在 Beta 3 版本中，此協助程式必須變更，看起來如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="4aafc-181">In the Beta 3 release, this helper must be changed to look like the following example:</span></span>
> 
> [!code-cshtml[Main](beta3/samples/sample3.cshtml)]
> 
> <span data-ttu-id="4aafc-182">請注意，已不再使用 helper 中初始程式碼周圍的 `@{ }` 字元。</span><span class="sxs-lookup"><span data-stu-id="4aafc-182">Notice that the `@{ }` characters around the initial code in the helper is no longer used.</span></span> <span data-ttu-id="4aafc-183">這是因為根據預設，系統會將 helper 的內容視為程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="4aafc-183">This is because the contents of the helpers are treated as a code block by default.</span></span> <span data-ttu-id="4aafc-184">協助程式呈現標記，其開頭為開啟的 `<a>` 標記。</span><span class="sxs-lookup"><span data-stu-id="4aafc-184">The helper renders markup, which starts with the opening `<a>` tag.</span></span> <span data-ttu-id="4aafc-185">如果 helper 必須轉譯純文字或不含結束記號的標記（例如，`<meta>` 標記），則要轉譯的內容必須在 `<text></text>` 標記中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-185">If the helper must render plain text or tags that do not include a closing tag (for example, `<meta>` tags), the content to be rendered must be in `<text></text>` tags.</span></span>

#### <a name="change-webpagecontexthttpcontext-removed"></a><span data-ttu-id="4aafc-186">變更：已移除 "WebPageCoNtext"</span><span class="sxs-lookup"><span data-stu-id="4aafc-186">Change: "WebPageContext.HttpContext" removed</span></span>

> <span data-ttu-id="4aafc-187">`WebPageContext.HttpContext` 屬性已經移除。</span><span class="sxs-lookup"><span data-stu-id="4aafc-187">The `WebPageContext.HttpContext` property has been removed.</span></span> <span data-ttu-id="4aafc-188">請改用 `HttpContext.Current`。</span><span class="sxs-lookup"><span data-stu-id="4aafc-188">Use `HttpContext.Current` instead.</span></span> <span data-ttu-id="4aafc-189">（`WebPageContext.HttpContext` 屬性只會包裝此內容）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-189">(The `WebPageContext.HttpContext` property simply wrapped this.)</span></span>

#### <a name="change-facebook-helper-moved-to-new-package"></a><span data-ttu-id="4aafc-190">變更： "Facebook" helper 已移至新套件</span><span class="sxs-lookup"><span data-stu-id="4aafc-190">Change: "Facebook" helper moved to new package</span></span>

> <span data-ttu-id="4aafc-191">`Facebook` helper 已移至*Facebook. helper*程式庫，其中包含 `Facebook` 協助程式和其他功能。</span><span class="sxs-lookup"><span data-stu-id="4aafc-191">The `Facebook` helper has been moved to the *Facebook.Helper* library, which includes the `Facebook` helper and additional functionality.</span></span> <span data-ttu-id="4aafc-192">您必須將此程式庫安裝為個別套件，如 < 使用封裝管理員安裝協助程式[ASP.NET 網頁](https://go.microsoft.com/fwlink/?LinkId=202889)中的教學課程消費者入門中所述。</span><span class="sxs-lookup"><span data-stu-id="4aafc-192">You must install this library as a separate package, as described in "Installing Helpers with Package Manager" in the tutorial [Getting Started with ASP.NET Pages](https://go.microsoft.com/fwlink/?LinkId=202889).</span></span>

#### <a name="change-membership-role-and-security-types-moves-to-new-assembly"></a><span data-ttu-id="4aafc-193">變更：成員資格、角色和安全性類型會移至新的元件</span><span class="sxs-lookup"><span data-stu-id="4aafc-193">Change: Membership, Role, and Security types moves to new assembly</span></span>

> <span data-ttu-id="4aafc-194">下列類型已移至 `WebMatrix.WebData` 元件：</span><span class="sxs-lookup"><span data-stu-id="4aafc-194">The following types were moved to the `WebMatrix.WebData` assembly:</span></span>
> 
> - `ExtendedMembershipProvider`
> - `SimpleMembershipProvider`
> - `SimpleRoleProvider`
> - `WebSecurity`

#### <a name="change-tagbuilder-class-moved-to-systemwebwebpagesdll-assembly"></a><span data-ttu-id="4aafc-195">變更：已將 "TagBuilder" 類別移至 System.web 元件</span><span class="sxs-lookup"><span data-stu-id="4aafc-195">Change: "TagBuilder" class moved to System.Web.WebPages.dll assembly</span></span>

> <span data-ttu-id="4aafc-196">`TagBuilde` r 類別已移至 System.web .dll 元件。</span><span class="sxs-lookup"><span data-stu-id="4aafc-196">The `TagBuilde` r class has been moved to the System.Web.WebPages.dll assembly.</span></span> <span data-ttu-id="4aafc-197">先前，這是在屬於 ASP.NET MVC 的元件中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-197">Previously, this was in an assembly that was part of ASP.NET MVC.</span></span> <span data-ttu-id="4aafc-198">這項變更表示您不需要安裝 ASP.NET MVC，即可使用 `TagBuilder` 類別。</span><span class="sxs-lookup"><span data-stu-id="4aafc-198">This change means that you do not have to install ASP.NET MVC in order to use the `TagBuilder` class.</span></span>
> 
> <span data-ttu-id="4aafc-199">不過，類別仍在 `System.Web.Mvc` 命名空間中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-199">However, the class is still in the `System.Web.Mvc` namespace.</span></span> <span data-ttu-id="4aafc-200">若要使用 `TagBuilder` 類別（例如，在自訂的 ASP.NET Razor helper 中），您必須參考命名空間（例如，藉由將 `@using System.Web.Mvc` 新增至您的程式碼）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-200">In order to use the `TagBuilder` class (for example, in a custom ASP.NET Razor helper), you must reference the namespace (for example, by adding `@using System.Web.Mvc` to your code).</span></span>

#### <a name="change-request-validation-syntax-changed-validation-class-removed"></a><span data-ttu-id="4aafc-201">變更：要求驗證語法已變更;已移除 "驗證" 類別</span><span class="sxs-lookup"><span data-stu-id="4aafc-201">Change: Request validation syntax changed; "Validation" class removed</span></span>

> <span data-ttu-id="4aafc-202">在 Beta 3 版本中，若要停用個別欄位或一組欄位的驗證，您可以呼叫 `Validation.Exclude` 方法，傳入要從驗證排除之欄位的名稱或名稱。</span><span class="sxs-lookup"><span data-stu-id="4aafc-202">In the Beta 3 release, to disable validation for an individual field or set of fields, you can call the `Validation.Exclude` method, passing in the name or names of the fields to exclude from validation.</span></span> <span data-ttu-id="4aafc-203">Beta 3 版本提供新的語法，以略過驗證。</span><span class="sxs-lookup"><span data-stu-id="4aafc-203">A new syntax is available in the Beta 3 release for bypassing validation.</span></span> <span data-ttu-id="4aafc-204">搶鮮版（Beta）3中使用的 `Validation` 方法已經移除。</span><span class="sxs-lookup"><span data-stu-id="4aafc-204">The `Validation` method used in Beta 3 has been removed.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="4aafc-205">如果您未停用要求驗證，如果使用者嘗試上傳 HTML 標籤（例如，藉由在頁面上使用 rtf 編輯器），網站將會報告錯誤，例如*潛在危險的要求。從用戶端偵測到表單值*，而且不接受使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="4aafc-205">If you do not disable request validation, if users try to upload HTML markup (for example, by using a rich text editor on a page), the website will report an error like *A potentially dangerous Request.Form value was detected from the client* and the user input is not accepted.</span></span> <span data-ttu-id="4aafc-206">如果您停用要求驗證，則必須手動檢查使用者輸入，以確定它不包含可能有害的標記或腳本，其使用的是[Microsoft 反跨網站腳本程式庫 v4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651)。</span><span class="sxs-lookup"><span data-stu-id="4aafc-206">If you disable request validation, you must manually check user input to make sure that it does not contain potentially dangerous markup or script using something like the [Microsoft Anti-Cross Site Scripting Library V4.0](https://www.microsoft.com/downloads/en/details.aspx?FamilyID=f4cd231b-7e06-445b-bec7-343e5884e651).</span></span>
> 
> 
> <span data-ttu-id="4aafc-207">若要停用自動要求驗證，請呼叫 `Request.Unvalidated` 方法，將您想要略過要求驗證的欄位或其他 post 物件的名稱傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="4aafc-207">To disable automatic request validation, call the `Request.Unvalidated` method, passing it the name of the field or other post object that you want to bypass request validation for.</span></span> <span data-ttu-id="4aafc-208">您可以使用這個方法，略過 `Form`、`QueryString`、`Cookies`和 `ServerVariables` 集合中任何專案的驗證。</span><span class="sxs-lookup"><span data-stu-id="4aafc-208">You can use this method to bypass validation for any items in the `Form`, `QueryString`, `Cookies`, and `ServerVariables` collections.</span></span> <span data-ttu-id="4aafc-209">下列範例示範如何使用 `Unvalidated` 方法：</span><span class="sxs-lookup"><span data-stu-id="4aafc-209">The following examples show how to use the `Unvalidated` method:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample4.cs)]

<a id="Issues"></a>

#### <a name="known-issues-for-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="4aafc-210">使用 Razor 語法 ASP.NET Web Pages 的已知問題</span><span class="sxs-lookup"><span data-stu-id="4aafc-210">Known Issues for ASP.NET Web Pages with Razor Syntax</span></span>

#### <a name="issue-unexpected-behavior-when-using-a-custom-user-table-for-membership"></a><span data-ttu-id="4aafc-211">問題：針對成員資格使用自訂使用者資料表時發生非預期的行為</span><span class="sxs-lookup"><span data-stu-id="4aafc-211">Issue: Unexpected behavior when using a custom user table for membership</span></span>

> <span data-ttu-id="4aafc-212">若要初始化 ASP.NET Razor 網站的成員資格提供者，您可以呼叫 `WebSecurity.InitializeDatabaseConnection` 方法。</span><span class="sxs-lookup"><span data-stu-id="4aafc-212">To initialize the membership provider for an ASP.NET Razor website, you call the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="4aafc-213">（在 WebMatrix 中，入門網站範本會在 *\_AppStart*中包含此方法的呼叫）。如果此方法的 `autoCreateTables` 參數設定為 true （預設會在入門網站範本中設定為 true），而且如果將無法辨識的資料表名稱傳遞給方法（第二個參數），則此方法不會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="4aafc-213">(In WebMatrix, the Starter Site template includes a call to this method in the *\_AppStart.cshtml* file.) If the `autoCreateTables` parameter of this method is set to true (by default, it is set to true in the Starter Site template), and if an unrecognized table name is passed to the method (the second parameter), the method does not throw an error.</span></span> <span data-ttu-id="4aafc-214">不過，它會自動產生資料表。</span><span class="sxs-lookup"><span data-stu-id="4aafc-214">Instead, it automatically creates the table.</span></span>
> 
> <span data-ttu-id="4aafc-215">如果您想要使用自訂使用者資料表來取得成員資格，但將錯誤的資料表名稱傳遞給 `WebSecurity.InitializeDatabaseConnection` 方法，這可能會是個問題。</span><span class="sxs-lookup"><span data-stu-id="4aafc-215">This can be a problem if you intend to use a custom user table for membership but pass the wrong table name to the `WebSecurity.InitializeDatabaseConnection` method.</span></span> <span data-ttu-id="4aafc-216">因為如果您所指定的資料表不存在，此方法預設不會引發錯誤，而且因為它會改為建立新的資料表，所以應用程式可能會看似正常運作。</span><span class="sxs-lookup"><span data-stu-id="4aafc-216">Because the method does not by default raise an error if the table you specify does not exist, and because it instead creates a new table, the application can appear to be working.</span></span> <span data-ttu-id="4aafc-217">不過，相依於自訂使用者資料表 (以及資料表中的欄位) 的應用程式程式碼最後可能會失敗並發生非預期的錯誤。</span><span class="sxs-lookup"><span data-stu-id="4aafc-217">However, application code that relies on your custom user table (and on fields in it) can eventually fail with unexpected errors.</span></span>
> 
> <span data-ttu-id="4aafc-218">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-218">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-219">請確定在 `InitializeDatabaseConnection` 方法中傳遞的名稱符合成員資格資料庫中的使用者設定檔資料表，或確認 `autoCreateTables` 參數設定為 false。</span><span class="sxs-lookup"><span data-stu-id="4aafc-219">Make sure that the name passed in the `InitializeDatabaseConnection` method matches the user profile table in the membership database, or make sure that the `autoCreateTables` parameter is set to false.</span></span>

#### <a name="issue-failed-to-generate-a-user-instance-of-sql-server-error"></a><span data-ttu-id="4aafc-220">問題：「無法產生 SQL Server 的使用者執行個體」錯誤</span><span class="sxs-lookup"><span data-stu-id="4aafc-220">Issue: "Failed to generate a user instance of SQL Server" error</span></span>

> <span data-ttu-id="4aafc-221">如果 WebMatrix Web 應用程式使用了 SQL Server Express 而且正在 Windows 7 或 Windows Server 2008 R2 上執行 IIS 7.5，您可能會看見一則錯誤，表示 SQL Server 無法在執行階段中擷取使用者的本機應用程式路徑。</span><span class="sxs-lookup"><span data-stu-id="4aafc-221">If a WebMatrix Web application uses SQL Server Express and is running IIS 7.5 on Windows 7 or Windows Server 2008 R2, you might see an error that indicates that SQL Server cannot retrieve the user's local application path at run time.</span></span>
> 
> <span data-ttu-id="4aafc-222">因應措施確定用來執行應用程式的 Windows 帳戶（通常是 NETWORK SERVICE）擁有應用程式根資料夾和子資料夾（例如*應用程式\_資料*）的讀取/寫入權限。</span><span class="sxs-lookup"><span data-stu-id="4aafc-222">**Workaround** Make sure that the Windows account that the application runs under (typically NETWORK SERVICE) has read/write permissions for root folders of the application and for subfolders such as *App\_Data*.</span></span> <span data-ttu-id="4aafc-223">如需詳細資訊，請參閱知識庫文章[SQL Server Express 使用者實例和 ASP.net Web 應用程式專案的問題](https://support.microsoft.com/kb/2002980)。</span><span class="sxs-lookup"><span data-stu-id="4aafc-223">More detailed information is available in the KnowledgeBase article [Problems with SQL Server Express user instancing and ASP.net Web Application Projects](https://support.microsoft.com/kb/2002980).</span></span>

#### <a name="issue-in-visual-studio-namespaces-for-custom-assemblies-dlls-are-not-imported-automatically"></a><span data-ttu-id="4aafc-224">問題：在 Visual Studio 中，不會自動匯入自訂群組件（Dll）的命名空間</span><span class="sxs-lookup"><span data-stu-id="4aafc-224">Issue: In Visual Studio, namespaces for custom assemblies (DLLs) are not imported automatically</span></span>

> <span data-ttu-id="4aafc-225">如果您在 Visual Studio 的專案中使用自訂群組件，則這些元件中宣告的命名空間不會在設計階段自動匯入。</span><span class="sxs-lookup"><span data-stu-id="4aafc-225">If you use custom assemblies in a project in Visual Studio, the namespaces declared in those assemblies are not automatically imported at design time.</span></span> <span data-ttu-id="4aafc-226">因此，在設計階段可能無法辨識自訂類型的參考，並在 Visual Studio 中將其標示為無法辨識（使用「波浪線」）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-226">As a result, references to custom types might not be recognized at design time and are marked as not recognized in Visual Studio (using a "squiggle").</span></span> <span data-ttu-id="4aafc-227">這個問題只會發生在 Visual Studio 的設計階段;應用程式本身會正常執行。</span><span class="sxs-lookup"><span data-stu-id="4aafc-227">This problem occurs only at design time in Visual Studio; the application itself runs properly.</span></span>
> 
> <span data-ttu-id="4aafc-228">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-228">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-229">包含 `using` 語句（Visual Basic 中的`imports`），其參考在設計階段無法辨識的實體。</span><span class="sxs-lookup"><span data-stu-id="4aafc-229">Include a `using` statement (`imports` in Visual Basic) that references the entities that are not recognized at design time.</span></span>

#### <a name="issue-visual-studio-intellisense-and-project-templates-available-only-in-aspnet-mvc-version-3"></a><span data-ttu-id="4aafc-230">問題：Visual Studio IntelliSense 和專案範本只能在 ASP.NET MVC 3 版中使用</span><span class="sxs-lookup"><span data-stu-id="4aafc-230">Issue: Visual Studio IntelliSense and project templates available only in ASP.NET MVC version 3</span></span>

> <span data-ttu-id="4aafc-231">安裝 ASP.NET Web Pages 不會一併安裝適用於 Visual Studio 的工具，例如適用於 ASP.NET Web Pages 應用程式的 IntelliSense 和專案範本。</span><span class="sxs-lookup"><span data-stu-id="4aafc-231">Installing ASP.NET Web Pages does not also install tools for Visual Studio such as IntelliSense and project templates for ASP.NET Web Pages applications.</span></span>
> 
> <span data-ttu-id="4aafc-232">因應措施若要在 Visual Studio 中使用 ASP.NET Web Pages 應用程式的 IntelliSense 和專案範本，請透過 Web Platform Installer 或[獨立安裝程式](https://go.microsoft.com/fwlink/?LinkID=191797)來安裝 ASP.NET MVC 3 RC。</span><span class="sxs-lookup"><span data-stu-id="4aafc-232">**Workaround** To use IntelliSense and project templates for ASP.NET Web Pages applications in Visual Studio, install ASP.NET MVC 3 RC either through the Web Platform Installer or the [stand-alone installer](https://go.microsoft.com/fwlink/?LinkID=191797).</span></span>

#### <a name="issue-lthelpergt-class-cannot-be-found-error"></a><span data-ttu-id="4aafc-233">問題：「找不到&lt;helper&gt; 類別」錯誤</span><span class="sxs-lookup"><span data-stu-id="4aafc-233">Issue: "&lt;helper&gt; class cannot be found" error</span></span>

> <span data-ttu-id="4aafc-234">升級至 Beta 3 之後，您可能會看到錯誤，指出找不到 helper 類別（例如，`Facebook` 類別）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-234">After you upgrade to Beta 3, you might see an error that a helper class (for example, the `Facebook` class) cannot not be found.</span></span> <span data-ttu-id="4aafc-235">從 Beta 2 開始並繼續 Beta 3，協助程式已移至您必須明確安裝的套件。</span><span class="sxs-lookup"><span data-stu-id="4aafc-235">Starting in Beta 2 and continuing in Beta 3, helpers have been moved to packages that you must explicitly install.</span></span> <span data-ttu-id="4aafc-236">現有的網站不會升級為包含這些套件;這包括 [ *\My Documents\IISExpress* ] 或 [ *\My documents\ 我 Web sites* ] 資料夾中的網站。</span><span class="sxs-lookup"><span data-stu-id="4aafc-236">Existing sites are not upgraded to include these packages; this includes sites in the *\My Documents\IISExpress* or *\My Documents\My Web Sites* folders.</span></span> <span data-ttu-id="4aafc-237">特別的是，如果您在 [*我的網站*] （WebSite1）中使用預設網站（其中包含 `Twitter` helper 的參考），就會看到此錯誤。</span><span class="sxs-lookup"><span data-stu-id="4aafc-237">In particular, you will see this error if you use the default site in *My Sites* (WebSite1), which includes a reference to the `Twitter` helper.</span></span>
> 
> <span data-ttu-id="4aafc-238">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-238">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-239">將呼叫批註至網站中的任何協助程式，執行 [ *\_管理員*] 頁面，並安裝包含您要使用之 helper 的封裝。</span><span class="sxs-lookup"><span data-stu-id="4aafc-239">Comment out calls to any helpers in the site, run the *\_Admin* page, and install the package or packages that include the helpers that you want to use.</span></span> <span data-ttu-id="4aafc-240">安裝封裝之後，您可以取消批註參考 helper 的程式列。</span><span class="sxs-lookup"><span data-stu-id="4aafc-240">After you've installed the package, you can uncomment the lines that reference helpers.</span></span>

#### <a name="issue-deploying-beta-3-aspnet-razor-assemblies-to-the-bin-folder-might-not-work-on-hosting-sites"></a><span data-ttu-id="4aafc-241">問題：將搶鮮版（Beta 3） ASP.NET Razor 元件部署到 Bin 資料夾可能無法在主控網站上運作</span><span class="sxs-lookup"><span data-stu-id="4aafc-241">Issue: Deploying Beta 3 ASP.NET Razor assemblies to the Bin folder might not work on hosting sites</span></span>

> <span data-ttu-id="4aafc-242">如果您將 ASP.NET Web Pages 網站部署至主控網站，而且將 ASP.NET Razor Beta 3 元件部署到網站的*Bin*資料夾，您可能會遇到錯誤，包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="4aafc-242">If you deploy an ASP.NET Web Pages website to a hosting site, and if you deploy the ASP.NET Razor Beta 3 assemblies to the site's *Bin* folder, you might experience errors, including the following:</span></span>
> 
> `Could not load type 'Microsoft.Web.Infrastructure.DynamicModuleHelper.DynamicModuleUtility' from assembly 'Microsoft.Web.Infrastructure, Version=1.0.0.0, Culture=neutral, PublicKeyToken=31bf3856ad364e35'.`
> 
> <span data-ttu-id="4aafc-243">如果主控提供者已將 ASP.NET Web Pages Beta 1 元件安裝到伺服器的全域應用程式快取（GAC）中，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="4aafc-243">This can happen if the hosting provider has installed the ASP.NET Web Pages Beta 1 assemblies into the server's global application cache (GAC).</span></span> <span data-ttu-id="4aafc-244">GAC 中的元件優先于*Bin*資料夾中本機安裝的元件。</span><span class="sxs-lookup"><span data-stu-id="4aafc-244">Assemblies in the GAC get precedence over assemblies installed locally in the *Bin* folder.</span></span>
> 
> <span data-ttu-id="4aafc-245">因應措施請洽詢您的主控提供者，以確認您看到的錯誤是由提供者版本的元件與您的衝突所造成。</span><span class="sxs-lookup"><span data-stu-id="4aafc-245">**Workaround** Contact your hosting provider to confirm that the errors you are seeing are due to a conflict between the provider's versions of the assemblies and yours.</span></span> <span data-ttu-id="4aafc-246">若是如此，請要求主控提供者補救伺服器 GAC 中的元件。</span><span class="sxs-lookup"><span data-stu-id="4aafc-246">If so, request that the hosting provider update the assemblies in the server's GAC.</span></span>

#### <a name="issue-reading-feeds-or-other-external-data-via-a-proxy-server"></a><span data-ttu-id="4aafc-247">問題：經由 Proxy 伺服器讀取摘要或其他外部資料</span><span class="sxs-lookup"><span data-stu-id="4aafc-247">Issue: Reading feeds or other external data via a proxy server</span></span>

> <span data-ttu-id="4aafc-248">如果執行網站的伺服器位於 proxy 伺服器後方，您可能需要*在 web.config 檔案*中設定 proxy 資訊，才能讀取來自網站外部的資訊。</span><span class="sxs-lookup"><span data-stu-id="4aafc-248">If the server running the site is behind a proxy server, you might need to configure proxy information in the *Web.config* file in order to be able to read information that comes from outside your site.</span></span> <span data-ttu-id="4aafc-249">例如，如果您使用 `ReCaptcha` 協助程式，則協助專家會與 reCAPTCHA 服務通訊，但您的 proxy 伺服器可能會封鎖它。</span><span class="sxs-lookup"><span data-stu-id="4aafc-249">For example, if you use the `ReCaptcha` helper, the helper communicates with the reCAPTCHA service, but might be blocked by your proxy server.</span></span> <span data-ttu-id="4aafc-250">同樣地，用於 ASP.NET Web Pages 中的摘要 (例如封裝管理員所使用的摘要) 可能需要 Proxy 組態。</span><span class="sxs-lookup"><span data-stu-id="4aafc-250">Similarly, feeds that are used in ASP.NET Web Pages, such as the feed used by the package manager, might require proxy configuration.</span></span>
> 
> <span data-ttu-id="4aafc-251">如果您在使用外部服務或使用封裝摘要時遇到問題，請將下列元素放入應用程式*的根 web.config*檔案中：</span><span class="sxs-lookup"><span data-stu-id="4aafc-251">If you experience problems in working with an external service or working with the package feed, put the following elements into your application's root *Web.config* file:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample5.xml)]
> 
> <span data-ttu-id="4aafc-252">如需設定 proxy 伺服器的詳細資訊，請參閱 MSDN 網站上的[&lt;proxy&gt; 元素（網路設定）](https://msdn.microsoft.com/library/sa91de1e.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="4aafc-252">For more information about configuring a proxy server, see [&lt;proxy&gt; Element (Network Settings)](https://msdn.microsoft.com/library/sa91de1e.aspx) on the MSDN Web site.</span></span>

#### <a name="issue-microsoftwebinfrastructuredll-cannot-be-loaded-error"></a><span data-ttu-id="4aafc-253">問題：「無法載入 Microsoft Web .dll .dll」錯誤</span><span class="sxs-lookup"><span data-stu-id="4aafc-253">Issue: "Microsoft.Web.Infrastructure.dll cannot be loaded" error</span></span>

> <span data-ttu-id="4aafc-254">如果您先前已使用 Razor 語法安裝 Beta 1 版的 ASP.NET Web Pages，然後再安裝 Beta 3 版，則所有適當的元件都會安裝在 GAC 中，但不包括*Microsoft. Web. 基礎結構 .dll*。</span><span class="sxs-lookup"><span data-stu-id="4aafc-254">If you previously installed the Beta 1 version of ASP.NET Web Pages with Razor syntax and then install the Beta 3 version, all appropriate assemblies are installed in the GAC except *Microsoft.Web.Infrastructure.dll*.</span></span> <span data-ttu-id="4aafc-255">因此，當您執行 ASP.NET Razor pages 時，您會看到錯誤訊息，*指出無法載入*[node.js]。</span><span class="sxs-lookup"><span data-stu-id="4aafc-255">As a consequence, when you run ASP.NET Razor pages, you see an error that indicates that *Microsoft.Web.Infrastructure.dll* could not be loaded.</span></span>
> 
> <span data-ttu-id="4aafc-256">如果您在乾淨的電腦上載入 Beta 3 版本，就不會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="4aafc-256">This issue does not occur if you loaded the Beta 3 release on a clean computer.</span></span>
> 
> <span data-ttu-id="4aafc-257">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-257">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-258">在 [控制台] 中，卸載 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="4aafc-258">In Control Panel, uninstall ASP.NET Web Pages.</span></span> <span data-ttu-id="4aafc-259">然後重新安裝 Beta 3 版。</span><span class="sxs-lookup"><span data-stu-id="4aafc-259">Then reinstall the Beta 3 release.</span></span>

#### <a name="issue-uninstalling-the-net-framework-version-4-disables-aspnet-web-pages-with-razor-syntax"></a><span data-ttu-id="4aafc-260">問題：解除安裝 .NET Framework 4 版就會停用含有 Razor 語法的 ASP.NET Web Pages</span><span class="sxs-lookup"><span data-stu-id="4aafc-260">Issue: Uninstalling the .NET Framework version 4 disables ASP.NET Web Pages with Razor Syntax</span></span>

> <span data-ttu-id="4aafc-261">如果您解除安裝 .NET Framework 4 版，然後重新安裝它，就會停用含有 Razor 語法的 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="4aafc-261">If you uninstall the .NET Framework version 4 and then reinstall it, ASP.NET Web Pages with Razor syntax is disabled.</span></span> <span data-ttu-id="4aafc-262">具有 *. cshtml*副檔名的頁面無法正確執行。</span><span class="sxs-lookup"><span data-stu-id="4aafc-262">Pages with the *.cshtml* extension do not run correctly.</span></span> <span data-ttu-id="4aafc-263">ASP.NET Web Pages 在*電腦根目錄的 web.config 檔案*中註冊元件，移除 .NET Framework 會移除該檔案。</span><span class="sxs-lookup"><span data-stu-id="4aafc-263">ASP.NET Web Pages registers an assembly in the machine root *Web.config* file, and removing the .NET Framework removes that file.</span></span> <span data-ttu-id="4aafc-264">雖然重新安裝 .NET Framework 會安裝新版的組態檔，不過卻不會加入 ASP.NET Web Pages 組件的參考。</span><span class="sxs-lookup"><span data-stu-id="4aafc-264">Reinstalling the .NET Framework installs a new version of the configuration file, but does not add the reference for the ASP.NET Web Pages assembly.</span></span>
> 
> <span data-ttu-id="4aafc-265">因應措施重新安裝 .NET Framework 之後，請使用 Razor 語法重新安裝 ASP.NET Web Pages。</span><span class="sxs-lookup"><span data-stu-id="4aafc-265">**Workaround** After reinstalling the .NET Framework, reinstall ASP.NET Web Pages with Razor syntax.</span></span> <span data-ttu-id="4aafc-266">這會將下列專案新增至電腦根目錄*中的 web.config*檔案，此檔案通常位於下列位置：</span><span class="sxs-lookup"><span data-stu-id="4aafc-266">This adds the following element to the *Web.config* file in the machine root, which is typically in the following location:</span></span>  
> 
> `C:\Windows\Microsoft.NET\Framework\v4.0.30319\Config (32-bit)`  
> 
> `C:\Windows\Microsoft.NET\Framework64\v4.0.30319\Config (64-bit)`
> 
> [!code-xml[Main](beta3/samples/sample6.xml)]

#### <a name="issue-applications-previously-deployed-with-aspnet-assemblies-in-the-bin-folder-experience-errors"></a><span data-ttu-id="4aafc-267">問題：先前使用 Bin 資料夾中的 ASP.NET 元件部署的應用程式發生錯誤</span><span class="sxs-lookup"><span data-stu-id="4aafc-267">Issue: Applications previously deployed with ASP.NET assemblies in the Bin folder experience errors</span></span>

> <span data-ttu-id="4aafc-268">在部署期間，ASP.NET Web Pages 元件（例如， *Microsoft. .dll*）的複本會複製到伺服器上網站的*Bin*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-268">During deployment, copies of the ASP.NET Web Pages assemblies (for example, *Microsoft.WebPages.dll*) to the *Bin* folder of the website on the server.</span></span> <span data-ttu-id="4aafc-269">（這可能會在部署期間自動發生，或因為開發人員已明確複製元件）。不過，在安裝 Beta 3 版本時，會發生錯誤，例如找不到特定類型的錯誤。</span><span class="sxs-lookup"><span data-stu-id="4aafc-269">(This might have happened automatically during deployment or because the developer explicitly copied the assemblies.) However, when the Beta 3 release is installed, errors occurs, such as errors that certain types cannot be found.</span></span> <span data-ttu-id="4aafc-270">這是因為在 Beta 3 版本中，有一些 ASP.NET Web Pages 類型已移至不同的命名空間。</span><span class="sxs-lookup"><span data-stu-id="4aafc-270">This occurs because a number of ASP.NET Web Pages types were moved into different namespaces for the Beta 3 release.</span></span>
> 
> <span data-ttu-id="4aafc-271">因應\*\*措施 \*\*</span><span class="sxs-lookup"><span data-stu-id="4aafc-271">**Workaround** </span></span>  
> <span data-ttu-id="4aafc-272">清除已部署應用程式的*Bin*資料夾，將新的元件複製到資料夾（或重新部署應用程式），然後重新開機應用程式。</span><span class="sxs-lookup"><span data-stu-id="4aafc-272">Clear the *Bin* folder of the deployed application, copy the new assemblies to the folder (or redeploy the application), and then restart the application.</span></span>

#### <a name="issue-extensionless-urls-do-not-find-cshtmlvbhtml-files-on-iis-7-or-iis-75"></a><span data-ttu-id="4aafc-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span><span class="sxs-lookup"><span data-stu-id="4aafc-273">Issue: Extensionless URLs do not find .cshtml/.vbhtml files on IIS 7 or IIS 7.5</span></span>

> <span data-ttu-id="4aafc-274">在 IIS 7 或 IIS 7.5 上，URL 如下的要求找不到具有 *. cshtml*或*vbhtml*副檔名的頁面：</span><span class="sxs-lookup"><span data-stu-id="4aafc-274">On IIS 7 or IIS 7.5, requests with a URL like the following are not able to find pages that have the *.cshtml* or *.vbhtml* extension:</span></span>  
> 
> `http://www.example.com/ExampleSite/ExampleFile`  
> 
> <span data-ttu-id="4aafc-275">因為 IIS 7 或 IIS 7.5 預設不會啟用 URL 重寫，所以會發生此問題。</span><span class="sxs-lookup"><span data-stu-id="4aafc-275">The issue arises because URL rewriting is not enabled by default for IIS 7 or IIS 7.5.</span></span> <span data-ttu-id="4aafc-276">原因案例是，當您使用 IIS Express 在本機進行測試時，不會看到問題，但是當您將網站部署至主控網站時，就會遇到此問題。</span><span class="sxs-lookup"><span data-stu-id="4aafc-276">The likeliest scenario is that you do not see the problem when testing locally using IIS Express, but you experience it when you deploy your website to a hosting website.</span></span>
> 
> <span data-ttu-id="4aafc-277">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-277">**Workaround**</span></span>
> 
> - <span data-ttu-id="4aafc-278">如果您可以控制伺服器電腦，請在伺服器電腦上安裝更新中所述的更新，[讓特定 IIS 7.0 或 IIS 7.5 處理常式能夠處理其 url 不是以句號結尾的要求](https://support.microsoft.com/kb/980368)。</span><span class="sxs-lookup"><span data-stu-id="4aafc-278">If you have control over the server computer, on the server computer install the update that is described in [A update is available that enables certain IIS 7.0 or IIS 7.5 handlers to handle requests whose URLs do not end with a period](https://support.microsoft.com/kb/980368).</span></span>
> - <span data-ttu-id="4aafc-279">如果您無法控制伺服器電腦（例如，您要部署至主控網站），請將下列*內容新增至網站的 web.config*檔案：</span><span class="sxs-lookup"><span data-stu-id="4aafc-279">If you do not have control over the server computer (for example, you are deploying to a hosting website), add the following to the website's *Web.config* file:</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample7.xml)]

#### <a name="issue-using-web-application-project-or-aspnet-mvc-and-aspnet-web-pages-in-the-same-application"></a><span data-ttu-id="4aafc-280">問題：在相同的應用程式中使用 Web 應用程式專案或 ASP.NET MVC 和 ASP.NET Web pages</span><span class="sxs-lookup"><span data-stu-id="4aafc-280">Issue: Using Web Application Project or ASP.NET MVC and ASP.NET Web pages in the same application</span></span>

> <span data-ttu-id="4aafc-281">如果您在 Web 應用程式專案或 ASP.NET MVC 應用程式中使用 ASP.NET Web Pages，您可能會看到*WebPageHttpApplication*找不到的錯誤。</span><span class="sxs-lookup"><span data-stu-id="4aafc-281">If you were using ASP.NET Web Pages in a Web Application project or ASP.NET MVC application, you might see an error that *WebPageHttpApplication* cannot be found.</span></span>
> 
> <span data-ttu-id="4aafc-282">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-282">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-283">如果您收到此錯誤，請變更應用程式衍生的基類。</span><span class="sxs-lookup"><span data-stu-id="4aafc-283">If you get this error, change the base class from which the application derives.</span></span> <span data-ttu-id="4aafc-284">在*global.asax*檔案中，變更下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="4aafc-284">In the *Global.asax* file, change the following line:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample8.cs)]
> 
> <span data-ttu-id="4aafc-285">為此值：</span><span class="sxs-lookup"><span data-stu-id="4aafc-285">To this:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample9.cs)]
> 
> <span data-ttu-id="4aafc-286">這實際上會反轉 ASP.NET Web Pages 的 Beta 1 版本所引進的變更與 Razor 語法。</span><span class="sxs-lookup"><span data-stu-id="4aafc-286">This in effect reverses a change that was introduced for the Beta 1 release of ASP.NET Web Pages with Razor syntax.</span></span>

#### <a name="issue-deploying-an-application-to-a-computer-that-does-not-have-sql-server-compact-installed"></a><span data-ttu-id="4aafc-287">問題：將應用程式部署到未安裝 SQL Server Compact 的電腦</span><span class="sxs-lookup"><span data-stu-id="4aafc-287">Issue: Deploying an application to a computer that does not have SQL Server Compact installed</span></span>

> <span data-ttu-id="4aafc-288">包含 SQL Server Compact 資料庫的應用程式可以在未安裝 SQL Server Compact 的電腦上執行。</span><span class="sxs-lookup"><span data-stu-id="4aafc-288">Applications that include SQL Server Compact databases can run on a computer where SQL Server Compact is not installed.</span></span> <span data-ttu-id="4aafc-289">Microsoft WebMatrix Beta 3 會自動為您複製這些二進位檔，並執行適當的*web.config*檔案轉換。</span><span class="sxs-lookup"><span data-stu-id="4aafc-289">Microsoft WebMatrix Beta 3 automatically copies these binaries for you and performs the appropriate *Web.config* file transforms.</span></span>
> 
> <span data-ttu-id="4aafc-290">因應措施如果您需要複製這些檔案，並手動進行*web.config*檔案變更，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="4aafc-290">**Workaround** If you need to copy these files and make the *Web.config* file changes manually, do the following :</span></span>
> 
> 1. <span data-ttu-id="4aafc-291">將資料庫引擎元件複製到目的電腦上應用程式的*Bin*資料夾（和子資料夾）：</span><span class="sxs-lookup"><span data-stu-id="4aafc-291">Copy the database engine assemblies to the *Bin* folder (and subfolders) of the application on the target computer:</span></span> 
> 
>     - <span data-ttu-id="4aafc-292">將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll*複製**到** *\bin*</span><span class="sxs-lookup"><span data-stu-id="4aafc-292">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Desktop\System.Data.SqlServerCe.dll* **to** *\Bin*</span></span>
>     - <span data-ttu-id="4aafc-293">將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\* \* 複製**到** *\Bin\x86*</span><span class="sxs-lookup"><span data-stu-id="4aafc-293">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\x86\\*\* **to** *\Bin\x86*</span></span>
>     - <span data-ttu-id="4aafc-294">將*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\* \* 複製**到** *\Bin\amd64*</span><span class="sxs-lookup"><span data-stu-id="4aafc-294">Copy *C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private\amd64\\*\* **to** *\Bin\amd64*</span></span>
> 2. <span data-ttu-id="4aafc-295">在網站的根資料夾中，建立或*開啟 web.config 檔案*。</span><span class="sxs-lookup"><span data-stu-id="4aafc-295">In the root folder of the website, create or open a *Web.config* file.</span></span> <span data-ttu-id="4aafc-296">（在 WebMatrix 搶鮮版（Beta 3）中，如果您在 [**選擇檔案類型**] 對話方塊中按一下 [**全部**]，則可以使用此檔案類型）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-296">(In WebMatrix Beta 3, this file type is available if you click **All** in the **Choose a File Type** dialog box.)</span></span>
> 3. <span data-ttu-id="4aafc-297">新增下列專案做為 **&lt;configuration&gt;** 專案的子系（而不是在 **&lt;system.web&gt;** 專案中）：</span><span class="sxs-lookup"><span data-stu-id="4aafc-297">Add the following element as a child of the **&lt;configuration&gt;** element (not inside the **&lt;system.web&gt;** element):</span></span>
> 
> 
> [!code-xml[Main](beta3/samples/sample10.xml)]

#### <a name="issue-database-and-webgrid-helpers-do-not-work-in-medium-trust-in-visual-basic"></a><span data-ttu-id="4aafc-298">問題：資料庫和 WebGrid 協助程式在 Visual Basic 中的中度信任無法正常操作</span><span class="sxs-lookup"><span data-stu-id="4aafc-298">Issue: Database and WebGrid helpers do not work in Medium Trust in Visual Basic</span></span>

> <span data-ttu-id="4aafc-299">如果您使用 Visual Basic （建立*vbhtml*檔案），則當應用程式設定為使用中度信任時，`Database` 和 `WebGrid` helper 將無法使用。</span><span class="sxs-lookup"><span data-stu-id="4aafc-299">If you are using Visual Basic (creating *.vbhtml* files), the `Database` and `WebGrid` helpers will not work if the application is set to use Medium Trust.</span></span>
> 
> <span data-ttu-id="4aafc-300">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-300">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-301">暫時將應用程式設定為使用完全信任。</span><span class="sxs-lookup"><span data-stu-id="4aafc-301">Temporarily set the application to use Full Trust.</span></span>

<a id="Known_Issues_SQL_Server_Compact"></a>
### <a name="sql-server-compact"></a><span data-ttu-id="4aafc-302">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="4aafc-302">SQL Server Compact</span></span>

#### <a name="issue-encrypt-property-is-not-recognized"></a><span data-ttu-id="4aafc-303">問題：無法辨識「加密」屬性</span><span class="sxs-lookup"><span data-stu-id="4aafc-303">Issue: "Encrypt" property is not recognized</span></span>

> <span data-ttu-id="4aafc-304">SQL Server Compact 4.0 無法辨識 `SqlCeConnection` 類別的 `Encrypt` 屬性。</span><span class="sxs-lookup"><span data-stu-id="4aafc-304">SQL Server Compact 4.0 does not recognize the `Encrypt` property of the `SqlCeConnection` class.</span></span> <span data-ttu-id="4aafc-305">您不應該使用這個屬性來加密資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="4aafc-305">You should not use this property to encrypt database files.</span></span> <span data-ttu-id="4aafc-306">`Encrypt` 屬性在 SQL Server Compact 3.5 版本中已被取代，而且只為了回溯相容性而保留。</span><span class="sxs-lookup"><span data-stu-id="4aafc-306">The `Encrypt` property was deprecated in SQL Server Compact 3.5 release and was retained only for backward compatibility.</span></span> 
> 
> <span data-ttu-id="4aafc-307">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-307">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-308">使用 `SqlCeConnection` 類別的 `Encryption Mode` 屬性來加密 SQL Server Compact 4.0 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="4aafc-308">Use the `Encryption Mode` property of the `SqlCeConnection` class to encrypt SQL Server Compact 4.0 database files.</span></span> <span data-ttu-id="4aafc-309">下列範例示範如何使用 `Encryption Mode` 屬性來建立加密的 SQL Server Compact 4.0 資料庫：</span><span class="sxs-lookup"><span data-stu-id="4aafc-309">The following example shows how to create an encrypted SQL Server Compact 4.0 database using the `Encryption Mode` property:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample11.cs)]
> 
> [!code-vb[Main](beta3/samples/sample12.vb)]
> 
> <span data-ttu-id="4aafc-310">若要變更現有 SQL Server Compact 4.0 資料庫的加密模式，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="4aafc-310">To change the encryption mode of an existing SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample13.cs)]
> 
> [!code-vb[Main](beta3/samples/sample14.vb)]
> 
> <span data-ttu-id="4aafc-311">若要加密未加密的 SQL Server Compact 4.0 資料庫，請執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="4aafc-311">To encrypt an unencrypted SQL Server Compact 4.0 database, do the following:</span></span>
> 
> [!code-csharp[Main](beta3/samples/sample15.cs)]
> 
> [!code-vb[Main](beta3/samples/sample16.vb)]

#### <a name="issue-microsoft-visual-c-2008-runtime-libraries-are-required"></a><span data-ttu-id="4aafc-312">問題：需要 Microsoft C++ Visual 2008 執行時間程式庫</span><span class="sxs-lookup"><span data-stu-id="4aafc-312">Issue: Microsoft Visual C++ 2008 runtime libraries are required</span></span>

> <span data-ttu-id="4aafc-313">SQL Server Compact 4.0 的原生 Dll 需要 Microsoft Visual C++ 2008 執行時間程式庫（X86、IA64 和 X64） Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="4aafc-313">The native DLLs of SQL Server Compact 4.0 need the Microsoft Visual C++ 2008 Runtime Libraries (x86, IA64, and x64), Service Pack 1.</span></span>
> 
> <span data-ttu-id="4aafc-314">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-314">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-315">安裝 .NET Framework 3.5 SP1。</span><span class="sxs-lookup"><span data-stu-id="4aafc-315">Install the .NET Framework 3.5 SP1.</span></span> <span data-ttu-id="4aafc-316">這也會安裝 Visual C++ 2008 執行時間程式庫 SP1。</span><span class="sxs-lookup"><span data-stu-id="4aafc-316">This also installs the Visual C++ 2008 Runtime Libraries SP1.</span></span> <span data-ttu-id="4aafc-317">您可以從下列位置下載程式庫：</span><span class="sxs-lookup"><span data-stu-id="4aafc-317">You can download the libraries from the following location:</span></span>   
>   
> [<span data-ttu-id="4aafc-318">Microsoft Visual C++ 2008 Service Pack 1 可轉散發套件 ATL 安全性更新</span><span class="sxs-lookup"><span data-stu-id="4aafc-318">Microsoft Visual C++ 2008 Service Pack 1 Redistributable Package ATL Security Update</span></span>](https://go.microsoft.com/fwlink/?LinkId=194827)
> 
> [!NOTE]
> <span data-ttu-id="4aafc-319">請注意，安裝 .NET Framework 2.0、3.0 或*4 並不*會安裝 Visual C++ 2008 執行時間程式庫 SP1。</span><span class="sxs-lookup"><span data-stu-id="4aafc-319">Note that installing the .NET Framework 2.0, 3.0, or 4 does *not* install the Visual C++ 2008 Runtime Libraries SP1.</span></span>

#### <a name="issue-if-sql-server-compact-is-installed-prior-to-installing-net-framework-on-the-computer-its-provider-invariant-name-is-not-registered-in-the-net-framework-machineconfig-file"></a><span data-ttu-id="4aafc-320">問題：如果在電腦上安裝 .NET Framework 之前已安裝 SQL Server Compact，則其提供者不變名稱不會在 .NET Framework machine.config 檔案中註冊</span><span class="sxs-lookup"><span data-stu-id="4aafc-320">Issue: If SQL Server Compact is installed prior to installing .NET Framework on the computer, its provider invariant name is not registered in the .NET Framework machine.config file</span></span>

> <span data-ttu-id="4aafc-321">SQL Server Compact 可以安裝在未安裝 .NET Framework 的電腦上，因為 SQL Server Compact 需要 .NET Framework。</span><span class="sxs-lookup"><span data-stu-id="4aafc-321">SQL Server Compact can be installed on a machine that does not have .NET Framework installed because SQL Server Compact does require the .NET framework.</span></span> <span data-ttu-id="4aafc-322">如果在安裝 SQL Server Compact 之前都未安裝 .NET Framework 版本3.5 或4，SQL Server Compact 安裝程式不會在*machine.config*檔案中註冊其提供者不變名稱。</span><span class="sxs-lookup"><span data-stu-id="4aafc-322">If neither .NET Framework version 3.5 nor 4 is installed before you install SQL Server Compact, the SQL Server Compact Setup does not register its provider invariant name in the *machine.config* file.</span></span> <span data-ttu-id="4aafc-323">依賴*machine.config*檔案中 SQL Server Compact 專案的任何應用程式都會失敗。</span><span class="sxs-lookup"><span data-stu-id="4aafc-323">Any application that relies on the SQL Server Compact entry in the *machine.config* file will fail.</span></span> <span data-ttu-id="4aafc-324">*Machine.config*中的非變異名稱註冊專案如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="4aafc-324">The invariant name registration entry in *machine.config* looks like the following example:</span></span>
> 
> [!code-xml[Main](beta3/samples/sample17.xml)]
> 
> <span data-ttu-id="4aafc-325">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-325">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-326">卸載 SQL Server Compact 4.0 CTP1。</span><span class="sxs-lookup"><span data-stu-id="4aafc-326">Uninstall SQL Server Compact 4.0 CTP1.</span></span> <span data-ttu-id="4aafc-327">從下列位置下載並安裝完整版的 .NET Framework：</span><span class="sxs-lookup"><span data-stu-id="4aafc-327">Download and install the full versions of the .NET Framework from the following location:</span></span>
> 
> [<span data-ttu-id="4aafc-328">Microsoft .NET Framework 3.5 Service pack 1 （完整套件）</span><span class="sxs-lookup"><span data-stu-id="4aafc-328">Microsoft .NET Framework 3.5 Service pack 1 (Full Package)</span></span>](https://go.microsoft.com/fwlink/?LinkId=194828)  
> [<span data-ttu-id="4aafc-329">Microsoft .NET Framework 4.0 版本（完整套件）</span><span class="sxs-lookup"><span data-stu-id="4aafc-329">Microsoft .NET Framework 4.0 Release (Full Package)</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyID=9cfb2d51-5ff4-4491-b0e5-b386f32c0992&amp;displaylang=en)
> 
> <span data-ttu-id="4aafc-330">然後重新安裝[SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en)。</span><span class="sxs-lookup"><span data-stu-id="4aafc-330">Then reinstall [SQL Server Compact 4.0 CTP1](https://www.microsoft.com/downloads/details.aspx?FamilyID=0d2357ea-324f-46fd-88fc-7364c80e4fdb&amp;displaylang=en).</span></span>

<a id="Known_Issues_Installing_Applications"></a>

### <a name="installing-applications"></a><span data-ttu-id="4aafc-331">安裝應用程式</span><span class="sxs-lookup"><span data-stu-id="4aafc-331">Installing Applications</span></span>

#### <a name="issue-installing-an-application-can-take-a-long-time-if-the-users-my-documents-folder-is-redirected-to-a-network-share"></a><span data-ttu-id="4aafc-332">問題：如果使用者的 [我的文件] 資料夾重新導向到網路共用，則安裝應用程式可能需要很長的時間</span><span class="sxs-lookup"><span data-stu-id="4aafc-332">Issue: Installing an application can take a long time if the user's My Documents folder is redirected to a network share</span></span>

> <span data-ttu-id="4aafc-333">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-333">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-334">無。</span><span class="sxs-lookup"><span data-stu-id="4aafc-334">None.</span></span> <span data-ttu-id="4aafc-335">應用程式可能需要一些時間來安裝，但會正確安裝。</span><span class="sxs-lookup"><span data-stu-id="4aafc-335">The application might take a while to install, but will install correctly.</span></span>

<a id="Known_Issues_Publishing_Applications"></a>

### <a name="publishing-applications"></a><span data-ttu-id="4aafc-336">發行應用程式</span><span class="sxs-lookup"><span data-stu-id="4aafc-336">Publishing Applications</span></span>

#### <a name="issue-site-might-not-work-after-publishing-if-the-destination-url-field-is-not-prefixed-with-http-or-https"></a><span data-ttu-id="4aafc-337">問題：如果 [目的地 URL] 欄位未在前面加上 HTTP://或 HTTPs://，網站在發佈後可能無法正常執行</span><span class="sxs-lookup"><span data-stu-id="4aafc-337">Issue: Site might not work after publishing if the "Destination URL" field is not prefixed with http:// or https://</span></span>

> <span data-ttu-id="4aafc-338">在 [**發行設定**] 對話方塊中，如果目的地 URL 不是以 `http://` 或 `https://`開頭，則在部署之後，網站可能無法運作。</span><span class="sxs-lookup"><span data-stu-id="4aafc-338">In the **Publishing Settings** dialog box, if the destination URL does not begin with `http://` or `https://`, the site might not work after deployment.</span></span>
> 
> <span data-ttu-id="4aafc-339">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-339">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-340">在發佈網站之前，請確定 [**發行設定**] 對話方塊中的 [目的地 URL] 開頭為 [`http://`] 或 [`https://`]。</span><span class="sxs-lookup"><span data-stu-id="4aafc-340">Make sure that before you publish a site, the destination URL in the **Publish Settings** dialog box starts with `http://` or `https://`.</span></span>

#### <a name="issue-publishing-a-mysql-database-fails-with-the-error-failed-to-publish-the-database-this-can-happen-if-the-remote-database-cannot-run-the-script"></a><span data-ttu-id="4aafc-341">問題：發行 MySQL 資料庫失敗，錯誤為「無法發行資料庫。</span><span class="sxs-lookup"><span data-stu-id="4aafc-341">Issue: Publishing a MySQL database fails with the error "Failed to publish the database.</span></span> <span data-ttu-id="4aafc-342">如果遠端資料庫無法執行腳本，就會發生這種情況。」</span><span class="sxs-lookup"><span data-stu-id="4aafc-342">This can happen if the remote database cannot run the script."</span></span>

> <span data-ttu-id="4aafc-343">發生此錯誤的原因有很多。</span><span class="sxs-lookup"><span data-stu-id="4aafc-343">The error can occur for a number of reasons.</span></span> <span data-ttu-id="4aafc-344">您可以看到此錯誤的其中一個原因是，資料庫腳本包含單引號字元（'），而目的地 MySQL 資料庫的預設字元集不是 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="4aafc-344">One reason you can see this error is if the database script contains a single quotation character (') and the destination MySQL database's default character set is not to UTF-8.</span></span>
> 
> <span data-ttu-id="4aafc-345">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-345">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-346">將遠端 MySQL 資料庫的預設字元集設定為 UTF-8。</span><span class="sxs-lookup"><span data-stu-id="4aafc-346">Set the default character set for the remote MySQL database to UTF-8.</span></span>

<a id="Known_Issues_Other_Issues"></a>

### <a name="other-issues"></a><span data-ttu-id="4aafc-347">其他問題</span><span class="sxs-lookup"><span data-stu-id="4aafc-347">Other Issues</span></span>

#### <a name="issue-searchfilter-does-not-work-in-reports-for-group-by-issue-type"></a><span data-ttu-id="4aafc-348">問題：在 [群組依據] 的報表中，搜尋/篩選無法運作：問題類型</span><span class="sxs-lookup"><span data-stu-id="4aafc-348">Issue: Search/Filter does not work in Reports for Group By: Issue Type</span></span>

> <span data-ttu-id="4aafc-349">當您執行網站的報表時，如果您在 [*依 URL 篩選*] 方塊中輸入文字，然後按一下 [*搜尋*]，就不會發生任何事。</span><span class="sxs-lookup"><span data-stu-id="4aafc-349">When you run a report for a site, if you enter text in the *Filter by URL* box and click *Search*, nothing happens.</span></span> <span data-ttu-id="4aafc-350">這是因為當報表的 [*群組依據*] 狀態設定為 [*問題類型*] （預設值）時，此控制項無法正常運作。</span><span class="sxs-lookup"><span data-stu-id="4aafc-350">This is because this control is not functional while the *Group By* state of the report is set to *Issue Type*, which is the default.</span></span>
> 
> <span data-ttu-id="4aafc-351">因應措施在功能區的 [*分組方式*] 索引標籤中，按一下 [ *URL* ]，依據專案的來源 URL 來分組專案。</span><span class="sxs-lookup"><span data-stu-id="4aafc-351">**Workaround** In the *Group By* tab of ribbon, click *URL* to group the entries by their source URL.</span></span> <span data-ttu-id="4aafc-352">在此狀態下，用來篩選項目的文字方塊和按鈕會有作用。</span><span class="sxs-lookup"><span data-stu-id="4aafc-352">The text box and button to filter the entries are functional while in this state.</span></span>

#### <a name="issue-wcf-applications-fail-to-run-with-iis-express"></a><span data-ttu-id="4aafc-353">問題： WCF 應用程式無法使用 IIS Express 執行</span><span class="sxs-lookup"><span data-stu-id="4aafc-353">Issue: WCF applications fail to run with IIS Express</span></span>

> <span data-ttu-id="4aafc-354">流覽 WCF 應用程式會產生類似下列的錯誤：</span><span class="sxs-lookup"><span data-stu-id="4aafc-354">Browsing to a WCF application results in an error like the following one:</span></span>
> 
> <span data-ttu-id="4aafc-355">*無法載入檔案或元件 ' 7.0.0.0，Culture = 中性，PublicKeyToken = 31bf3856ad364e35 ' 或其相依性的其中之一。系統找不到指定的檔案。*</span><span class="sxs-lookup"><span data-stu-id="4aafc-355">*Could not load file or assembly 'Microsoft.Web.Administration, Version=7.0.0.0, Culture=neutral,PublicKeyToken=31bf3856ad364e35' or one of its dependencies. The system cannot find the file specified.*</span></span>
> 
> <span data-ttu-id="4aafc-356">之所以會發生這種情況，是因為 IIS Express 的 Beta 版預設不支援 WCF。</span><span class="sxs-lookup"><span data-stu-id="4aafc-356">This occurs because IIS Express Beta release doesn't support WCF by default.</span></span>
> 
> <span data-ttu-id="4aafc-357">因應措施使用下列任何一個因應措施（因應措施 #2 需要 Microsoft Windows Vista 或更高版本）：</span><span class="sxs-lookup"><span data-stu-id="4aafc-357">**Workaround** Use any one of the following workarounds (workaround #2 requires Microsoft Windows Vista or higher):</span></span>
> 
> 
> 1. <span data-ttu-id="4aafc-358">從 WebMatrix 安裝位置將*system.web*和*microsoft. web.config*元件複製到 WCF 應用程式的*bin*目錄。</span><span class="sxs-lookup"><span data-stu-id="4aafc-358">Copy the *Microsoft.Web.dll* and *Microsoft.Web.Administration.dll* assemblies from the WebMatrix installation location to the *bin* directory of the WCF application.</span></span> <span data-ttu-id="4aafc-359">根據預設，WebMatrix 會安裝在系統 [ *Program Files* ] 資料夾下的 [ *Microsoft WebMatrix* ] 子資料夾中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-359">By default, WebMatrix is installed in the *Microsoft WebMatrix* subfolder under the system's *Program Files* folder.</span></span>
> 2. <span data-ttu-id="4aafc-360">在 Microsoft Windows Vista 或更高版本上，使用下列命令建立*bin*目錄中元件的符號連結。</span><span class="sxs-lookup"><span data-stu-id="4aafc-360">On Microsoft Windows Vista or higher, create a symlink to the assemblies in the *bin* directory using the following commands.</span></span> <span data-ttu-id="4aafc-361">（這種方法的優點是它不會建立元件的複本）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-361">(This approach has the advantage that it does not create a copy of the assemblies.)</span></span>
> 
>     [!code-console[Main](beta3/samples/sample18.cmd)]
> 3. <span data-ttu-id="4aafc-362">在 GAC 中安裝這兩個元件。</span><span class="sxs-lookup"><span data-stu-id="4aafc-362">Install the two assemblies in the GAC.</span></span> <span data-ttu-id="4aafc-363">從提高許可權的提示字元中，執行下列命令：</span><span class="sxs-lookup"><span data-stu-id="4aafc-363">From an elevated prompt, run the following commands:</span></span>
> 
>     [!code-console[Main](beta3/samples/sample19.cmd)]

#### <a name="issue-webmatrix-beta-3-is-unable-to-perform-certain-tasks-that-require-elevation"></a><span data-ttu-id="4aafc-364">問題： WebMatrix Beta 3 無法執行某些需要提高許可權的工作</span><span class="sxs-lookup"><span data-stu-id="4aafc-364">Issue: WebMatrix Beta 3 is unable to perform certain tasks that require elevation</span></span>

> <span data-ttu-id="4aafc-365">WebMatrix Beta 3 無法執行需要提高許可權的特定工作，例如在下列情況下安裝其他元件：</span><span class="sxs-lookup"><span data-stu-id="4aafc-365">WebMatrix Beta 3 is unable to perform certain tasks that require elevation, such as installing additional components in the following situations:</span></span>
> 
> - <span data-ttu-id="4aafc-366">在 Windows Vista 或 Windows 7 上，您使用不具有系統管理許可權的帳戶登入，且使用者帳戶控制（UAC）已停用。</span><span class="sxs-lookup"><span data-stu-id="4aafc-366">On Windows Vista or Windows 7, you are logged in with an account that does not have administrative privileges and User Account Control (UAC) is disabled.</span></span>
> - <span data-ttu-id="4aafc-367">您使用的是 Microsoft Windows XP 或 Microsoft Windows Server 2003。</span><span class="sxs-lookup"><span data-stu-id="4aafc-367">You are using Microsoft Windows XP or Microsoft Windows Server 2003.</span></span>
> 
> <span data-ttu-id="4aafc-368">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-368">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-369">WebMatrix Beta 3 中的大部分工作都不需要系統管理許可權。</span><span class="sxs-lookup"><span data-stu-id="4aafc-369">Most tasks in WebMatrix Beta 3 do not require administrative permission.</span></span> <span data-ttu-id="4aafc-370">若是這樣做，您可以系統管理員身分執行作業，或遵循下列步驟進行操作：</span><span class="sxs-lookup"><span data-stu-id="4aafc-370">For those that do, you can perform the operation as an administrator, or follow these steps:</span></span>
> 
> - <span data-ttu-id="4aafc-371">在 Windows Vista 或 Windows 7 上，啟用 UAC。</span><span class="sxs-lookup"><span data-stu-id="4aafc-371">On Windows Vista or Windows 7, enable UAC.</span></span>
> - <span data-ttu-id="4aafc-372">在 Windows XP 上，將使用者新增至 [系統管理員] 安全性群組。</span><span class="sxs-lookup"><span data-stu-id="4aafc-372">On Windows XP, add the user to the Administrators security group.</span></span>

#### <a name="issue-site-from-web-gallery-is-disabled"></a><span data-ttu-id="4aafc-373">問題：「Web 元件庫中的網站」已停用</span><span class="sxs-lookup"><span data-stu-id="4aafc-373">Issue: "Site from Web Gallery" is disabled</span></span>

> <span data-ttu-id="4aafc-374">如果未安裝 Web Platform Installer 3.0，則會停用 [**從 Web 元件庫中的網站**] 選項。</span><span class="sxs-lookup"><span data-stu-id="4aafc-374">The **Site from Web Gallery** option is disabled if the Web Platform Installer 3.0 is not installed.</span></span>
> 
> <span data-ttu-id="4aafc-375">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-375">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-376">安裝[Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638)。</span><span class="sxs-lookup"><span data-stu-id="4aafc-376">Install the [Microsoft Web Platform Installer 3.0](https://go.microsoft.com/fwlink/?LinkID=194638).</span></span>

#### <a name="issue-on-windows-server-2003-iis-express-does-not-start-for-a-non-administrative-user"></a><span data-ttu-id="4aafc-377">問題：在 Windows Server 2003 上，不會為非系統管理使用者啟動 IIS Express</span><span class="sxs-lookup"><span data-stu-id="4aafc-377">Issue: On Windows Server 2003, IIS Express does not start for a non-administrative user</span></span>

> <span data-ttu-id="4aafc-378">在 Windows Server 2003 上，當您啟動頁面或開始 IIS Express 時，IIS Express 不會啟動。</span><span class="sxs-lookup"><span data-stu-id="4aafc-378">On Windows Server 2003, when you launch a page or start IIS Express, IIS Express does not start.</span></span> <span data-ttu-id="4aafc-379">若為網頁，則會顯示錯誤，指出應用程式已由非系統管理使用者啟動。</span><span class="sxs-lookup"><span data-stu-id="4aafc-379">For Web pages, an error is displayed that indicates that the application has been started by a non-administrative user.</span></span>
> 
> <span data-ttu-id="4aafc-380">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-380">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-381">以系統管理使用者身分啟動 WebMatrix 搶鮮版（Beta 3）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-381">Start WebMatrix Beta 3 as an administrative user.</span></span> <span data-ttu-id="4aafc-382">如需詳細資訊，請參閱下列知識庫文章：</span><span class="sxs-lookup"><span data-stu-id="4aafc-382">For more details, see the following KnowledgeBase article:</span></span>  
>   
> [<span data-ttu-id="4aafc-383">非系統管理使用者所啟動的應用程式無法接聽在 Windows Vista、Windows Server 2003 或 Windows XP 中執行應用程式之電腦的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="4aafc-383">An application that is started by a non-administrative user cannot listen to the HTTP traffic of the computer on which the application is running in Windows Vista, Windows Server 2003, or Windows XP.</span></span>](https://support.microsoft.com/kb/939786)

#### <a name="issue-google-chrome-is-not-available-as-a-run-option"></a><span data-ttu-id="4aafc-384">問題： Google Chrome 無法當做執行選項使用</span><span class="sxs-lookup"><span data-stu-id="4aafc-384">Issue: Google Chrome is not available as a Run option</span></span>

> <span data-ttu-id="4aafc-385">Google Chrome 不會顯示在 [**首頁**] 索引標籤上 [**執行**] 底下的瀏覽器清單中。</span><span class="sxs-lookup"><span data-stu-id="4aafc-385">Google Chrome is not displayed in the list of browsers under **Run** on the **Home** tab.</span></span>
> 
> <span data-ttu-id="4aafc-386">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-386">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-387">某些版本的 Google Chrome 不會正確地向 Windows 中的 [預設程式] 功能註冊自己。</span><span class="sxs-lookup"><span data-stu-id="4aafc-387">Some versions of Google Chrome do not register themselves correctly with the Default Programs feature in Windows.</span></span> <span data-ttu-id="4aafc-388">因應措施是啟動 Google Chrome，按一下 [*自訂和控制 Google chrome* ] 功能表，按一下 [*選項*]，然後按一下 [*將 google Chrome 設為預設瀏覽器*]。</span><span class="sxs-lookup"><span data-stu-id="4aafc-388">As a workaround, start Google Chrome, click the *Customize and control Google Chrome* menu, click *Options*, and then click *Make Google Chrome my default browser*.</span></span>

#### <a name="issue-the-foreign-key-dialog-box-doesnt-allow-entering-a-primary-key"></a><span data-ttu-id="4aafc-389">問題： [外鍵] 對話方塊不允許輸入主要金鑰</span><span class="sxs-lookup"><span data-stu-id="4aafc-389">Issue: The "Foreign Key" dialog box doesn't allow entering a primary key</span></span>

> <span data-ttu-id="4aafc-390">[**外鍵**] 對話方塊不允許您從主鍵資料表輸入主要金鑰名稱。</span><span class="sxs-lookup"><span data-stu-id="4aafc-390">The **Foreign Key** dialog box does not allow you to enter the primary key name from the primary key table.</span></span>
> 
> <span data-ttu-id="4aafc-391">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-391">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-392">這是故意的。</span><span class="sxs-lookup"><span data-stu-id="4aafc-392">This is intentional.</span></span> <span data-ttu-id="4aafc-393">您不需要輸入主要索引鍵資料表的主鍵名稱。</span><span class="sxs-lookup"><span data-stu-id="4aafc-393">You do not need to enter the name of the primary key from the primary key table.</span></span>

#### <a name="issue-the-relationships-button-is-disabled"></a><span data-ttu-id="4aafc-394">問題： [關聯性] 按鈕已停用</span><span class="sxs-lookup"><span data-stu-id="4aafc-394">Issue: The "Relationships" button is disabled</span></span>

> <span data-ttu-id="4aafc-395">[**資料庫**] 工作區中 [**資料表**] 索引標籤下的 [**關聯**性] 按鈕會停用 SQL Server Compact 資料庫。</span><span class="sxs-lookup"><span data-stu-id="4aafc-395">The **Relationships** button under the **Table** tab in the **Databases** workspace is disabled for SQL Server Compact databases.</span></span>
> 
> <span data-ttu-id="4aafc-396">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-396">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-397">無。</span><span class="sxs-lookup"><span data-stu-id="4aafc-397">None.</span></span> <span data-ttu-id="4aafc-398">SQL Server Compact 不支援資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="4aafc-398">SQL Server Compact does not support relationships between tables.</span></span>

#### <a name="issue-parameterized-sql-queries-throw-exceptions"></a><span data-ttu-id="4aafc-399">問題：參數化 SQL 查詢會擲回例外狀況</span><span class="sxs-lookup"><span data-stu-id="4aafc-399">Issue: Parameterized SQL queries throw exceptions</span></span>

> <span data-ttu-id="4aafc-400">在 SQL Server Compact 4.0 中，如果您未在參數化查詢中指定參數的資料類型（例如 `SqlDbType` 或 `DbType`），當查詢執行時，就會擲回例外狀況（exception）。</span><span class="sxs-lookup"><span data-stu-id="4aafc-400">In SQL Server Compact 4.0, if you do not specify a data type such as `SqlDbType` or `DbType` for parameters in parameterized queries, an exception is thrown when the query runs.</span></span>
> 
> <span data-ttu-id="4aafc-401">**因應措施**</span><span class="sxs-lookup"><span data-stu-id="4aafc-401">**Workaround**</span></span>  
> <span data-ttu-id="4aafc-402">明確設定參數的資料類型，例如 `SqlDbType` 或 `DbType`。</span><span class="sxs-lookup"><span data-stu-id="4aafc-402">Explicitly set the data type for parameters such as `SqlDbType` or `DbType`.</span></span> <span data-ttu-id="4aafc-403">這在 BLOB 資料類型（`image` 和 `ntext`）的情況下是不可或缺的。</span><span class="sxs-lookup"><span data-stu-id="4aafc-403">This is critical in the case of BLOB data types (`image` and `ntext`).</span></span> <span data-ttu-id="4aafc-404">使用如下所示的程式碼：</span><span class="sxs-lookup"><span data-stu-id="4aafc-404">Use code like the following:</span></span>
> 
> [!code-sql[Main](beta3/samples/sample20.sql)]
> 
> [!code-vb[Main](beta3/samples/sample21.vb)]

<a id="More_Info"></a>

## <a name="for-more-information"></a><span data-ttu-id="4aafc-405">取得更多資訊</span><span class="sxs-lookup"><span data-stu-id="4aafc-405">For More Information</span></span>

<span data-ttu-id="4aafc-406">如需 WebMatrix Beta 3 的詳細資訊，請參閱下列網站：</span><span class="sxs-lookup"><span data-stu-id="4aafc-406">For more information about WebMatrix Beta 3, see the following websites:</span></span>

- [<span data-ttu-id="4aafc-407">IIS.net</span><span class="sxs-lookup"><span data-stu-id="4aafc-407">IIS.net</span></span>](http://iis.net/)
- [<span data-ttu-id="4aafc-408">ASP.NET</span><span class="sxs-lookup"><span data-stu-id="4aafc-408">ASP.NET</span></span>](https://asp.net/webmatrix)
- [<span data-ttu-id="4aafc-409">Microsoft.com/web</span><span class="sxs-lookup"><span data-stu-id="4aafc-409">Microsoft.com/web</span></span>](https://www.microsoft.com/web)

---

<span data-ttu-id="4aafc-410">© 2010 Microsoft Corporation。</span><span class="sxs-lookup"><span data-stu-id="4aafc-410">© 2010 Microsoft Corporation.</span></span> <span data-ttu-id="4aafc-411">All Rights Reserved.</span><span class="sxs-lookup"><span data-stu-id="4aafc-411">All Rights Reserved.</span></span> <span data-ttu-id="4aafc-412">[使用條款](https://msdn.microsoft.cos/cc300389.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4aafc-412">[Terms of Use](https://msdn.microsoft.cos/cc300389.aspx).</span></span>
