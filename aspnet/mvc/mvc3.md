---
uid: mvc/mvc3
title: ASP.NET MVC 3
author: rick-anderson
description: （包含4月2011工具更新）ASP.NET MVC 3 是一種架構，可讓您使用已妥善建立的設計模式來建立可擴充的標準 web 應用程式 。
ms.author: riande
ms.date: 10/05/2010
ms.assetid: dddc8812-a0bc-49f9-aafb-caf2064c2b8c
msc.legacyurl: /mvc/mvc3
msc.type: content
ms.openlocfilehash: 421a06c89d4dbcb05d4080033813cc6558b7c698
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74586742"
---
# <a name="aspnet-mvc-3"></a><span data-ttu-id="963d5-103">ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="963d5-103">ASP.NET MVC 3</span></span>

> <span data-ttu-id="963d5-104">*（包含4月2011工具更新）*</span><span class="sxs-lookup"><span data-stu-id="963d5-104">*(includes April 2011 Tools Update)*</span></span>
> 
> <span data-ttu-id="963d5-105">ASP.NET MVC 3 是一種架構，可讓您使用妥善建立的設計模式以及 ASP.NET 和 .NET Framework 的強大功能，來建立可擴充且以標準為基礎的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="963d5-105">ASP.NET MVC 3 is a framework for building scalable, standards-based web applications using well-established design patterns and the power of ASP.NET and the .NET Framework.</span></span>
> 
> <span data-ttu-id="963d5-106">它會與 ASP.NET MVC 2 並存安裝，因此現在就開始使用它！</span><span class="sxs-lookup"><span data-stu-id="963d5-106">It installs side-by-side with ASP.NET MVC 2, so get started using it today!</span></span>
> 
> <span data-ttu-id="963d5-107">在[這裡下載安裝程式](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="963d5-107">Download the [installer here](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>

## <a name="top-features"></a><span data-ttu-id="963d5-108">熱門功能</span><span class="sxs-lookup"><span data-stu-id="963d5-108">Top Features</span></span>

- <span data-ttu-id="963d5-109">透過 NuGet 擴充的整合式架構系統</span><span class="sxs-lookup"><span data-stu-id="963d5-109">Integrated Scaffolding system extensible via NuGet</span></span>
- <span data-ttu-id="963d5-110">啟用 HTML 5 的專案範本</span><span class="sxs-lookup"><span data-stu-id="963d5-110">HTML 5 enabled project templates</span></span>
- <span data-ttu-id="963d5-111">表達性視圖，包括新的 Razor View Engine</span><span class="sxs-lookup"><span data-stu-id="963d5-111">Expressive Views including the new Razor View Engine</span></span>
- <span data-ttu-id="963d5-112">具有相依性插入和全域動作篩選器的強大勾點</span><span class="sxs-lookup"><span data-stu-id="963d5-112">Powerful hooks with Dependency Injection and Global Action Filters</span></span>
- <span data-ttu-id="963d5-113">具有不顯眼的 JavaScript、jQuery 驗證和 JSON 系結的豐富 JavaScript 支援</span><span class="sxs-lookup"><span data-stu-id="963d5-113">Rich JavaScript support with unobtrusive JavaScript, jQuery Validation, and JSON binding</span></span>
- <span data-ttu-id="963d5-114">*閱讀[下列](#overview)完整的功能清單*</span><span class="sxs-lookup"><span data-stu-id="963d5-114">*Read the full feature list [below](#overview)*</span></span>

## <a name="top-links"></a><span data-ttu-id="963d5-115">熱門連結</span><span class="sxs-lookup"><span data-stu-id="963d5-115">Top Links</span></span>

<span data-ttu-id="963d5-116">ASP.NET MVC 3 的新功能</span><span class="sxs-lookup"><span data-stu-id="963d5-116">What's New in ASP.NET MVC 3</span></span>

- <span data-ttu-id="963d5-117">Phil Haack： [ASP.NET MVC 3 已發行](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span><span class="sxs-lookup"><span data-stu-id="963d5-117">Phil Haack: [ASP.NET MVC 3 Released](http://haacked.com/archive/2011/01/13/aspnetmvc3-released.aspx)</span></span>
- <span data-ttu-id="963d5-118">Scott Hanselman： [ASP.NET MVC3、WebMatrix、NuGet、IIS Express 和 Orchard 發行-Microsoft 一月 Web 版本的內容](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span><span class="sxs-lookup"><span data-stu-id="963d5-118">Scott Hanselman: [ASP.NET MVC3, WebMatrix, NuGet, IIS Express and Orchard released - The Microsoft January Web Release in Context](http://www.hanselman.com/blog/ASPNETMVC3WebMatrixNuGetIISExpressAndOrchardReleasedTheMicrosoftJanuaryWebReleaseInContext.aspx)</span></span>
- <span data-ttu-id="963d5-119">Scott Guthrie：[宣佈發行 ASP.NET MVC 3、IIS Express、SQL CE 4、Web Farm Framework、Orchard、WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span><span class="sxs-lookup"><span data-stu-id="963d5-119">Scott Guthrie: [Announcing release of ASP.NET MVC 3, IIS Express, SQL CE 4, Web Farm Framework, Orchard, WebMatrix](https://weblogs.asp.net/scottgu/archive/2011/01/13/announcing-release-of-asp-net-mvc-3-iis-express-sql-ce-4-web-farm-framework-orchard-webmatrix.aspx)</span></span>
- [<span data-ttu-id="963d5-120">ASP.NET MVC 3 的版本資訊</span><span class="sxs-lookup"><span data-stu-id="963d5-120">Release Notes for ASP.NET MVC 3</span></span>](../whitepapers/mvc3-release-notes.md)

<span data-ttu-id="963d5-121">安裝與協助</span><span class="sxs-lookup"><span data-stu-id="963d5-121">Installation and Help</span></span>

- <span data-ttu-id="963d5-122">使用 Web Platform Installer 安裝 ASP.NET MVC 3 [（建議選項）](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span><span class="sxs-lookup"><span data-stu-id="963d5-122">Install ASP.NET MVC 3 using the [Web Platform Installer (recommended)](https://www.microsoft.com/web/handlers/webpi.ashx?command=getinstallerredirect&appid=MVC3)</span></span>
- <span data-ttu-id="963d5-123">使用安裝[程式可執行檔](https://go.microsoft.com/fwlink/?LinkID=208140)安裝 ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="963d5-123">Install ASP.NET MVC 3 using the [installer executable](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="963d5-124">安裝[適用于 Visual Studio 11 開發人員預覽的 ASP.NET MVC 3](https://go.microsoft.com/fwlink/?LinkID=208140)</span><span class="sxs-lookup"><span data-stu-id="963d5-124">Install [ASP.NET MVC 3 for Visual Studio 11 Developer Preview](https://go.microsoft.com/fwlink/?LinkID=208140)</span></span>
- <span data-ttu-id="963d5-125">閱讀[ASP.NET MVC 3 簡介教學](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)課程</span><span class="sxs-lookup"><span data-stu-id="963d5-125">Read the [Intro to ASP.NET MVC 3 tutorial](overview/older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)</span></span>
- <span data-ttu-id="963d5-126">取得協助並討論[論壇](https://forums.asp.net/1146.aspx)中的 ASP.NET MVC 3</span><span class="sxs-lookup"><span data-stu-id="963d5-126">Get help and discuss ASP.NET MVC 3 in the [forums](https://forums.asp.net/1146.aspx)</span></span>

<a id="overview"></a>
## <a name="aspnet-mvc-3-overview"></a><span data-ttu-id="963d5-127">ASP.NET MVC 3 概觀 (英文)</span><span class="sxs-lookup"><span data-stu-id="963d5-127">ASP.NET MVC 3 Overview</span></span>

<span data-ttu-id="963d5-128">ASP.NET MVC 3 建置於 ASP.NET MVC 1 和2，加入了可簡化程式碼並允許更深入擴充性的絕佳功能。</span><span class="sxs-lookup"><span data-stu-id="963d5-128">ASP.NET MVC 3 builds on ASP.NET MVC 1 and 2, adding great features that both simplify your code and allow deeper extensibility.</span></span> <span data-ttu-id="963d5-129">本主題概述此版本中包含的許多新功能，並組織成下列各節：</span><span class="sxs-lookup"><span data-stu-id="963d5-129">This topic provides an overview of many of the new features that are included in this release, organized into the following sections:</span></span>

- [<span data-ttu-id="963d5-130">具有 MvcScaffold 整合的可擴充式架構</span><span class="sxs-lookup"><span data-stu-id="963d5-130">Extensible Scaffolding with MvcScaffold integration</span></span>](#BM_MvcScaffolding)
- [<span data-ttu-id="963d5-131">啟用 HTML 5 的專案範本</span><span class="sxs-lookup"><span data-stu-id="963d5-131">HTML 5 enabled project templates</span></span>](#BM_HTML5)
- [<span data-ttu-id="963d5-132">Razor View 引擎</span><span class="sxs-lookup"><span data-stu-id="963d5-132">The Razor View Engine</span></span>](#BM_TheRazorViewEngine)
- [<span data-ttu-id="963d5-133">支援多個視圖引擎</span><span class="sxs-lookup"><span data-stu-id="963d5-133">Support for Multiple View Engines</span></span>](#BM_Support_for_Multiple_View_Engines)
- [<span data-ttu-id="963d5-134">控制器改善</span><span class="sxs-lookup"><span data-stu-id="963d5-134">Controller Improvements</span></span>](#BM_Controller_Improvements)
- [<span data-ttu-id="963d5-135">JavaScript 和 Ajax</span><span class="sxs-lookup"><span data-stu-id="963d5-135">JavaScript and Ajax</span></span>](#BM_JavaScript_and_Ajax_Improvements)
- [<span data-ttu-id="963d5-136">模型驗證改善</span><span class="sxs-lookup"><span data-stu-id="963d5-136">Model Validation Improvements</span></span>](#BM_Model_Validation_Improvements)
- [<span data-ttu-id="963d5-137">相依性插入改良功能</span><span class="sxs-lookup"><span data-stu-id="963d5-137">Dependency Injection Improvements</span></span>](#BM_Dependency_Injection_Improvements)
- [<span data-ttu-id="963d5-138">其他新功能</span><span class="sxs-lookup"><span data-stu-id="963d5-138">Other New Features</span></span>](#BM_Other_New_Features)

<a id="BM_MvcScaffolding"></a>

## <a name="extensible-scaffolding-with-mvcscaffold-integration"></a><span data-ttu-id="963d5-139">具有 MvcScaffold 整合的可擴充式架構</span><span class="sxs-lookup"><span data-stu-id="963d5-139">Extensible Scaffolding with MvcScaffold integration</span></span>

<span data-ttu-id="963d5-140">新的架構系統可讓您更輕鬆地開始使用，並在您剛體驗到 framework 時，將常見的開發工作自動化，並已瞭解您所執行的作業。</span><span class="sxs-lookup"><span data-stu-id="963d5-140">The new Scaffolding system makes it easier to pick up and start using productively if you're entirely new to the framework, and to automate common development tasks if you're experienced and already know what you're doing.</span></span>

<span data-ttu-id="963d5-141">這受到名為**MvcScaffolding**的*新 NuGet 架構*套件支援。</span><span class="sxs-lookup"><span data-stu-id="963d5-141">This is supported by new NuGet *scaffolding* package called **MvcScaffolding**.</span></span> <span data-ttu-id="963d5-142">許多軟體技術都使用「架構」一詞來表示「快速產生軟體的基本大綱，讓您可以編輯和自訂」。</span><span class="sxs-lookup"><span data-stu-id="963d5-142">The term "Scaffolding" is used by many software technologies to mean "quickly generating a basic outline of your software that you can then edit and customize".</span></span> <span data-ttu-id="963d5-143">我們為 ASP.NET MVC 所建立的樣板套件，在數個案例中有很大的好處：</span><span class="sxs-lookup"><span data-stu-id="963d5-143">The scaffolding package we're creating for ASP.NET MVC is greatly beneficial in several scenarios:</span></span>

- <span data-ttu-id="963d5-144">**如果您是第一次學習 ASP.NET MVC**，因為它可讓您快速取得一些有用的工作程式碼，因此您可以根據自己的需求進行編輯和調整。</span><span class="sxs-lookup"><span data-stu-id="963d5-144">**If you're learning ASP.NET MVC for the first time**, because it gives you a fast way to get some useful, working code, that you can then edit and adapt according to your needs.</span></span> <span data-ttu-id="963d5-145">它可以讓您從 trauma 查看空白頁面，而不知道要從何處著手！</span><span class="sxs-lookup"><span data-stu-id="963d5-145">It saves you from the trauma of looking at a blank page and having no idea where to start!</span></span>
- <span data-ttu-id="963d5-146">**如果您知道 ASP.NET MVC，而且現在正在探索一些新的附加元件技術**，例如物件關聯式對應程式、視圖引擎、測試程式庫等，這項技術的建立者也可能會為其建立一個元件套件。</span><span class="sxs-lookup"><span data-stu-id="963d5-146">**If you know ASP.NET MVC well and are now exploring some new add-on technology** such as an object-relational mapper, a view engine, a testing library, etc., because the creator of that technology may have also created a scaffolding package for it.</span></span>
- <span data-ttu-id="963d5-147">**如果您的工作牽涉到重複建立類似的類別或**檔案，這是因為您可以建立自訂鷹架已經，以輸出測試裝置、部署腳本，或任何您所需的其他類型。</span><span class="sxs-lookup"><span data-stu-id="963d5-147">**If your work involves repeatedly creating similar classes or files of some sort**, because you can create custom scaffolders that output test fixtures, deployment scripts, or whatever else you need.</span></span> <span data-ttu-id="963d5-148">小組中的每個人都可以使用您的自訂鷹架已經。</span><span class="sxs-lookup"><span data-stu-id="963d5-148">Everyone on your team can use your custom scaffolders, too.</span></span>

<span data-ttu-id="963d5-149">MvcScaffolding 中的其他功能包括：</span><span class="sxs-lookup"><span data-stu-id="963d5-149">Other features in MvcScaffolding include:</span></span>

- <span data-ttu-id="963d5-150">和 VB C#專案的支援</span><span class="sxs-lookup"><span data-stu-id="963d5-150">Support for C# and VB projects</span></span>
- <span data-ttu-id="963d5-151">Razor 和 ASPX 視圖引擎的支援</span><span class="sxs-lookup"><span data-stu-id="963d5-151">Support for the Razor and ASPX view engines</span></span>
- <span data-ttu-id="963d5-152">支援將樣板 ASP.NET MVC 區域，以及使用自訂視圖配置/主版</span><span class="sxs-lookup"><span data-stu-id="963d5-152">Supports scaffolding into ASP.NET MVC areas and using custom view layouts/masters</span></span>
- <span data-ttu-id="963d5-153">您可以藉由編輯 T4 範本，輕鬆地自訂輸出</span><span class="sxs-lookup"><span data-stu-id="963d5-153">You can easily customize the output by editing T4 templates</span></span>
- <span data-ttu-id="963d5-154">您可以使用自訂的 PowerShell 邏輯和自訂 T4 範本來新增全新的鷹架已經。</span><span class="sxs-lookup"><span data-stu-id="963d5-154">You can add entirely new scaffolders using custom PowerShell logic and custom T4 templates.</span></span> <span data-ttu-id="963d5-155">這些（和您指定的任何自訂參數）會自動顯示在主控台索引標籤-完成清單中。</span><span class="sxs-lookup"><span data-stu-id="963d5-155">These (and any custom parameters you've given them) automatically appear in the console tab-completion list.</span></span>
- <span data-ttu-id="963d5-156">您可以針對不同的技術取得包含其他鷹架已經的 NuGet 套件（例如，目前 LINQ to SQL 的概念證明），並將它們混合在一起</span><span class="sxs-lookup"><span data-stu-id="963d5-156">You can get NuGet packages containing additional scaffolders for different technologies (e.g., there's a proof-of-concept one for LINQ to SQL now) and mix and match them together</span></span>

<span data-ttu-id="963d5-157">ASP.NET MVC 3 工具更新包含此架構系統的絕佳 Visual Studio 支援，例如：</span><span class="sxs-lookup"><span data-stu-id="963d5-157">The ASP.NET MVC 3 Tools Update includes great Visual Studio support for this scaffolding system, such as:</span></span>

- <span data-ttu-id="963d5-158">[新增控制器] 對話方塊現在支援 [建立]、[讀取]、[更新] 和 [刪除控制器動作] 和對應視圖的完整自動架構。</span><span class="sxs-lookup"><span data-stu-id="963d5-158">Add Controller Dialog now supports full automatic scaffolding of Create, Read, Update, and Delete controller actions and corresponding views.</span></span> <span data-ttu-id="963d5-159">根據預設，這會使用 EF Code First scaffold 資料存取程式碼。</span><span class="sxs-lookup"><span data-stu-id="963d5-159">By default, this scaffolds data access code using EF Code First.</span></span>
- <span data-ttu-id="963d5-160">[新增控制器] 對話方塊透過 NuGet 套件（例如*MvcScaffolding*）支援*可擴充的 scaffold* 。</span><span class="sxs-lookup"><span data-stu-id="963d5-160">Add Controller Dialog supports *extensible scaffolds* via NuGet packages such as *MvcScaffolding*.</span></span> <span data-ttu-id="963d5-161">這可讓您將自訂 scaffold 插入對話方塊中，這可讓您針對其他資料存取技術（例如 NHibernate，甚至是使用 ODBCDirect 的 JET）建立 scaffold （如果您這麼做）。</span><span class="sxs-lookup"><span data-stu-id="963d5-161">This allows plugging in custom scaffolds into the dialog which would allow you to create scaffolds for other data access technologies such as NHibernate or even JET with ODBCDirect if you're so inclined!</span></span>

<span data-ttu-id="963d5-162">如需 ASP.NET MVC 3 中之樣板的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="963d5-162">For more information about Scaffolding in ASP.NET MVC 3, see the following resources:</span></span>

- <span data-ttu-id="963d5-163">Steve Sanderson 的文章系列，包括：</span><span class="sxs-lookup"><span data-stu-id="963d5-163">Steve Sanderson's post series, including:</span></span> 

    1. [<span data-ttu-id="963d5-164">簡介：使用 MvcScaffolding 套件 Scaffold 您的 ASP.NET MVC 3 專案</span><span class="sxs-lookup"><span data-stu-id="963d5-164">Introduction: Scaffold your ASP.NET MVC 3 project with the MvcScaffolding package</span></span>](http://blog.stevensanderson.com/2011/01/13/scaffold-your-aspnet-mvc-3-project-with-the-mvcscaffolding-package/)
    2. [<span data-ttu-id="963d5-165">標準使用方式：一般使用案例和選項</span><span class="sxs-lookup"><span data-stu-id="963d5-165">Standard usage: Typical use cases and options</span></span>](http://blog.stevensanderson.com/2011/01/13/mvcscaffolding-standard-usage/)
    3. [<span data-ttu-id="963d5-166">一對多關聯性</span><span class="sxs-lookup"><span data-stu-id="963d5-166">One-to-Many Relationships</span></span>](http://blog.stevensanderson.com/2011/01/28/mvcscaffolding-one-to-many-relationships/)
    4. [<span data-ttu-id="963d5-167">樣板動作和單元測試</span><span class="sxs-lookup"><span data-stu-id="963d5-167">Scaffolding Actions and Unit Tests</span></span>](http://blog.stevensanderson.com/2011/03/28/scaffolding-actions-and-unit-tests-with-mvcscaffolding/)
    5. [<span data-ttu-id="963d5-168">覆寫 T4 範本</span><span class="sxs-lookup"><span data-stu-id="963d5-168">Overriding the T4 templates</span></span>](http://blog.stevensanderson.com/2011/04/06/mvcscaffolding-overriding-the-t4-templates/)
    6. [<span data-ttu-id="963d5-169">這篇文章：建立自訂鷹架已經</span><span class="sxs-lookup"><span data-stu-id="963d5-169">This post: Creating custom scaffolders</span></span>](http://blog.stevensanderson.com/2011/04/07/mvcscaffolding-creating-custom-scaffolders/)
- <span data-ttu-id="963d5-170">Scott Hanselman 在他的 PDC 2010 研討會發表[了 Microsoft 「未命名的 Web 愛套件](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)」的 Blog</span><span class="sxs-lookup"><span data-stu-id="963d5-170">Scott Hanselman's post from his PDC 2010 session [Building a Blog with Microsoft "Unnamed Package of Web Love"](http://www.hanselman.com/blog/PDC10BuildingABlogWithMicrosoftUnnamedPackageOfWebLove.aspx)</span></span>
- [<span data-ttu-id="963d5-171">MVC 3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="963d5-171">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_HTML5"></a>

## <a name="html-5-project-templates"></a><span data-ttu-id="963d5-172">HTML 5 專案範本</span><span class="sxs-lookup"><span data-stu-id="963d5-172">HTML 5 Project Templates</span></span>

<span data-ttu-id="963d5-173">[新增專案] 對話方塊包含 [啟用 HTML 5 版本的專案範本] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="963d5-173">The New Project dialog includes a checkbox enable HTML 5 versions of project templates.</span></span> <span data-ttu-id="963d5-174">這些範本會利用 Modernizr 1.7，為舊版瀏覽器中的 HTML 5 和 CSS 3 提供相容性支援。</span><span class="sxs-lookup"><span data-stu-id="963d5-174">These templates leverage Modernizr 1.7 to provide compatibility support for HTML 5 and CSS 3 in down-level browsers.</span></span>

<a id="BM_TheRazorViewEngine"></a>

## <a name="the-razor-view-engine"></a><span data-ttu-id="963d5-175">Razor View 引擎</span><span class="sxs-lookup"><span data-stu-id="963d5-175">The Razor View Engine</span></span>

<span data-ttu-id="963d5-176">ASP.NET MVC 3 隨附名為 Razor 的新 view engine，可提供下列優點：</span><span class="sxs-lookup"><span data-stu-id="963d5-176">ASP.NET MVC 3 comes with a new view engine named Razor that offers the following benefits:</span></span>

- <span data-ttu-id="963d5-177">Razor 語法很簡潔，而且需要最少的擊鍵數。</span><span class="sxs-lookup"><span data-stu-id="963d5-177">Razor syntax is clean and concise, requiring a minimum number of keystrokes.</span></span>
- <span data-ttu-id="963d5-178">Razor 很容易學習，部分是因為它是以現有的語言（如C#和 Visual Basic）為基礎。</span><span class="sxs-lookup"><span data-stu-id="963d5-178">Razor is easy to learn, in part because it's based on existing languages like C# and Visual Basic.</span></span>
- <span data-ttu-id="963d5-179">Visual Studio 包含 Razor 語法的 IntelliSense 和程式碼顏色標示。</span><span class="sxs-lookup"><span data-stu-id="963d5-179">Visual Studio includes IntelliSense and code colorization for Razor syntax.</span></span>
- <span data-ttu-id="963d5-180">Razor views 可以進行單元測試，而不需要您執行應用程式或啟動 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="963d5-180">Razor views can be unit tested without requiring that you run the application or launch a web server.</span></span>

<span data-ttu-id="963d5-181">一些新的 Razor 功能包括下列各項：</span><span class="sxs-lookup"><span data-stu-id="963d5-181">Some new Razor features include the following:</span></span>

- <span data-ttu-id="963d5-182">`@model` 語法，用於指定要傳遞至視圖的類型。</span><span class="sxs-lookup"><span data-stu-id="963d5-182">`@model` syntax for specifying the type being passed to the view.</span></span>
- <span data-ttu-id="963d5-183">`@* *@` 批註語法。</span><span class="sxs-lookup"><span data-stu-id="963d5-183">`@* *@` comment syntax.</span></span>
- <span data-ttu-id="963d5-184">為整個網站指定預設值（例如 `layoutpage`）的能力。</span><span class="sxs-lookup"><span data-stu-id="963d5-184">The ability to specify defaults (such as `layoutpage`) once for an entire site.</span></span>
- <span data-ttu-id="963d5-185">在不進行 HTML 編碼的情況下顯示文字的 `Html.Raw` 方法。</span><span class="sxs-lookup"><span data-stu-id="963d5-185">The `Html.Raw` method for displaying text without HTML-encoding it.</span></span>
- <span data-ttu-id="963d5-186">支援在多個視圖之間共用程式碼（ *\_viewstart*或 *\_viewstart vbhtml*檔案）。</span><span class="sxs-lookup"><span data-stu-id="963d5-186">Support for sharing code among multiple views (*\_viewstart.cshtml* or *\_viewstart.vbhtml* files).</span></span>

<span data-ttu-id="963d5-187">Razor 也包含新的 HTML 協助程式，如下所示：</span><span class="sxs-lookup"><span data-stu-id="963d5-187">Razor also includes  new HTML helpers, such as the following:</span></span>

- <span data-ttu-id="963d5-188">`Chart`。</span><span class="sxs-lookup"><span data-stu-id="963d5-188">`Chart`.</span></span> <span data-ttu-id="963d5-189">呈現圖表，其提供的功能與 ASP.NET 4 中的 chart 控制項相同。</span><span class="sxs-lookup"><span data-stu-id="963d5-189">Renders a chart, offering the same features as the chart control in ASP.NET 4.</span></span>
- <span data-ttu-id="963d5-190">`WebGrid`。</span><span class="sxs-lookup"><span data-stu-id="963d5-190">`WebGrid`.</span></span> <span data-ttu-id="963d5-191">使用分頁和排序功能來呈現資料方格。</span><span class="sxs-lookup"><span data-stu-id="963d5-191">Renders a data grid, complete with paging and sorting functionality.</span></span>
- <span data-ttu-id="963d5-192">`Crypto`。</span><span class="sxs-lookup"><span data-stu-id="963d5-192">`Crypto`.</span></span> <span data-ttu-id="963d5-193">會使用雜湊演算法來建立適當的 salted 和雜湊密碼。</span><span class="sxs-lookup"><span data-stu-id="963d5-193">Uses hashing algorithms to create properly salted and hashed passwords.</span></span>
- <span data-ttu-id="963d5-194">`WebImage`。</span><span class="sxs-lookup"><span data-stu-id="963d5-194">`WebImage`.</span></span> <span data-ttu-id="963d5-195">呈現影像。</span><span class="sxs-lookup"><span data-stu-id="963d5-195">Renders an image.</span></span>
- <span data-ttu-id="963d5-196">`WebMail`。</span><span class="sxs-lookup"><span data-stu-id="963d5-196">`WebMail`.</span></span> <span data-ttu-id="963d5-197">傳送電子郵件訊息。</span><span class="sxs-lookup"><span data-stu-id="963d5-197">Sends an email message.</span></span>

<span data-ttu-id="963d5-198">如需 Razor 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="963d5-198">For more information about Razor, see the following resources:</span></span>

- [<span data-ttu-id="963d5-199">Scott Guthrie 的文章 Razor 簡介</span><span class="sxs-lookup"><span data-stu-id="963d5-199">Scott Guthrie's blog post introducing Razor</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)
- [<span data-ttu-id="963d5-200">Scott Guthrie 的文章，介紹 @model 關鍵字</span><span class="sxs-lookup"><span data-stu-id="963d5-200">Scott Guthrie's blog post introducing the @model keyword</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/19/asp-net-mvc-3-new-model-directive-support-in-razor.aspx)
- [<span data-ttu-id="963d5-201">Scott Guthrie 的文章 Razor 版面配置簡介</span><span class="sxs-lookup"><span data-stu-id="963d5-201">Scott Guthrie's blog post introducing Razor layouts</span></span>](https://weblogs.asp.net/scottgu/archive/2010/10/22/asp-net-mvc-3-layouts.aspx)
- [<span data-ttu-id="963d5-202">Razor API 快速參考</span><span class="sxs-lookup"><span data-stu-id="963d5-202">Razor API Quick Reference</span></span>](../web-pages/overview/api-reference/asp-net-web-pages-api-reference.md)
- [<span data-ttu-id="963d5-203">MVC 3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="963d5-203">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Support_for_Multiple_View_Engines"></a>

## <a name="support-for-multiple-view-engines"></a><span data-ttu-id="963d5-204">支援多個視圖引擎</span><span class="sxs-lookup"><span data-stu-id="963d5-204">Support for Multiple View Engines</span></span>

<span data-ttu-id="963d5-205">ASP.NET MVC 3 中的 [**加入視圖**] 對話方塊可讓您選擇要使用的視圖引擎，而 [**新增專案**] 對話方塊可讓您指定專案的預設視圖引擎。</span><span class="sxs-lookup"><span data-stu-id="963d5-205">The **Add View** dialog box in ASP.NET MVC 3 lets you choose the view engine you want to work with, and the **New Project** dialog box lets you specify the default view engine for a project.</span></span> <span data-ttu-id="963d5-206">您可以選擇 [Web form view engine （ASPX）]、[Razor] 或開放原始碼視圖引擎（例如[Spark](http://sparkviewengine.com/)、 [NHaml](https://code.google.com/p/nhaml/)或[NDjango](http://ndjango.org/)）。</span><span class="sxs-lookup"><span data-stu-id="963d5-206">You can choose the Web Forms view engine (ASPX), Razor, or an open-source view engine such as [Spark](http://sparkviewengine.com/), [NHaml](https://code.google.com/p/nhaml/), or [NDjango](http://ndjango.org/).</span></span>

<a id="BM_Controller_Improvements"></a>

## <a name="controller-improvements"></a><span data-ttu-id="963d5-207">控制器改善</span><span class="sxs-lookup"><span data-stu-id="963d5-207">Controller Improvements</span></span>

### <a name="global-action-filters"></a><span data-ttu-id="963d5-208">全域動作篩選</span><span class="sxs-lookup"><span data-stu-id="963d5-208">Global Action Filters</span></span>

<span data-ttu-id="963d5-209">有時候，您可能會想要在動作方法執行之前或動作方法執行之後執行邏輯。</span><span class="sxs-lookup"><span data-stu-id="963d5-209">Sometimes you want to perform logic either before an action method runs or after an action method runs.</span></span> <span data-ttu-id="963d5-210">若要支援這種情況，請 ASP.NET MVC 2 提供的動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="963d5-210">To support this, ASP.NET MVC 2 provided action filters.</span></span> <span data-ttu-id="963d5-211">動作篩選器是自訂屬性，可提供宣告式方式，將動作前和動作後的行為新增至特定的控制器動作方法。</span><span class="sxs-lookup"><span data-stu-id="963d5-211">Action filters are custom attributes that provide a declarative means to add pre-action and post-action behavior to specific controller action methods.</span></span> <span data-ttu-id="963d5-212">不過，在某些情況下，您可能會想要指定套用至所有動作方法的前置動作或動作後行為。</span><span class="sxs-lookup"><span data-stu-id="963d5-212">However, in some cases you might want to specify pre-action or post-action behavior that applies to all action methods.</span></span> <span data-ttu-id="963d5-213">MVC 3 可讓您藉由將全域篩選新增至 `GlobalFilters` 集合來指定它們。</span><span class="sxs-lookup"><span data-stu-id="963d5-213">MVC 3 lets you specify global filters by adding them to the `GlobalFilters` collection.</span></span> <span data-ttu-id="963d5-214">如需全域動作篩選器的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="963d5-214">For more information about global action filters, see the following resources:</span></span>

- [<span data-ttu-id="963d5-215">在 MVC 3 Preview 上 Scott Guthrie 的 blog</span><span class="sxs-lookup"><span data-stu-id="963d5-215">Scott Guthrie's blog on the MVC 3 Preview</span></span>](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)
- <span data-ttu-id="963d5-216">[ASP.NET MVC 中的篩選](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span><span class="sxs-lookup"><span data-stu-id="963d5-216">[Filtering in ASP.NET MVC](https://msdn.microsoft.com/library/gg416513(VS.98).aspx)</span></span>

### <a name="new-viewbag-property"></a><span data-ttu-id="963d5-217">新的 "ViewBag" 屬性</span><span class="sxs-lookup"><span data-stu-id="963d5-217">New "ViewBag" Property</span></span>

<span data-ttu-id="963d5-218">MVC 2 控制器支援 `ViewData` 屬性，可讓您使用晚期繫結字典 API 將資料傳遞至視圖範本。</span><span class="sxs-lookup"><span data-stu-id="963d5-218">MVC 2 controllers support a `ViewData` property that enables you to pass data to a view template using a late-bound dictionary API.</span></span> <span data-ttu-id="963d5-219">在 MVC 3 中，您也可以搭配 `ViewBag` 屬性使用稍微簡單的語法，以達成相同的目的。</span><span class="sxs-lookup"><span data-stu-id="963d5-219">In MVC 3, you can also use somewhat simpler syntax with the `ViewBag` property to accomplish the same purpose.</span></span> <span data-ttu-id="963d5-220">例如，您可以撰寫 `ViewBag.Message="text"`，而不是撰寫 `ViewData["Message"]="text"`。</span><span class="sxs-lookup"><span data-stu-id="963d5-220">For example, instead of writing `ViewData["Message"]="text"`, you can write `ViewBag.Message="text"`.</span></span> <span data-ttu-id="963d5-221">您不需要定義任何強型別類別，就可以使用 `ViewBag` 屬性。</span><span class="sxs-lookup"><span data-stu-id="963d5-221">You do not need to define any strongly-typed classes to use the `ViewBag` property.</span></span> <span data-ttu-id="963d5-222">因為它是動態屬性，所以您可以改為取得或設定屬性，而且它會在執行時間動態加以解析。</span><span class="sxs-lookup"><span data-stu-id="963d5-222">Because it is a dynamic property, you can instead just get or set properties and it will resolve them dynamically at run time.</span></span> <span data-ttu-id="963d5-223">就內部而言，`ViewBag` 屬性會以名稱/值組的形式儲存在 `ViewData` 字典中。</span><span class="sxs-lookup"><span data-stu-id="963d5-223">Internally, `ViewBag` properties are stored as name/value pairs in the `ViewData` dictionary.</span></span> <span data-ttu-id="963d5-224">（注意：在 MVC 3 的大部分發行前版本中，`ViewBag` 屬性都是命名為 `ViewModel` 屬性）。</span><span class="sxs-lookup"><span data-stu-id="963d5-224">(Note: in most pre-release versions of MVC 3, the `ViewBag` property was named the `ViewModel` property.)</span></span>

### <a name="new-actionresult-types"></a><span data-ttu-id="963d5-225">新的 "ActionResult" 類型</span><span class="sxs-lookup"><span data-stu-id="963d5-225">New "ActionResult" Types</span></span>

<span data-ttu-id="963d5-226">下列 `ActionResult` 類型和對應的 helper 方法是 MVC 3 中的新功能或增強功能：</span><span class="sxs-lookup"><span data-stu-id="963d5-226">The following `ActionResult` types and corresponding helper methods are new or enhanced in MVC 3:</span></span>

- <span data-ttu-id="963d5-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="963d5-227">[HttpNotFoundResult](https://msdn.microsoft.com/library/system.web.mvc.httpnotfoundresult(v=vs.98).aspx).</span></span> <span data-ttu-id="963d5-228">將 404 HTTP 狀態碼傳回到用戶端。</span><span class="sxs-lookup"><span data-stu-id="963d5-228">Returns a 404 HTTP status code to the client.</span></span>
- <span data-ttu-id="963d5-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="963d5-229">[RedirectResult](https://msdn.microsoft.com/library/system.web.mvc.redirectresult(v=VS.98).aspx).</span></span> <span data-ttu-id="963d5-230">根據布林值參數傳回暫時重新導向（HTTP 302 狀態碼）或永久重新導向（HTTP 301 狀態碼）。</span><span class="sxs-lookup"><span data-stu-id="963d5-230">Returns a temporary redirect (HTTP 302 status code) or a permanent redirect (HTTP 301 status code), depending on a Boolean parameter.</span></span> <span data-ttu-id="963d5-231">結合這項變更，[控制器](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx)類別現在有三種方法可執行永久重新導向： `RedirectPermanent`、`RedirectToRoutePermanent`和 `RedirectToActionPermanent`。</span><span class="sxs-lookup"><span data-stu-id="963d5-231">In conjunction with this change, the [Controller](https://msdn.microsoft.com/library/system.web.mvc.controller(v=VS.98).aspx) class now has three methods for performing permanent redirects: `RedirectPermanent`, `RedirectToRoutePermanent`, and `RedirectToActionPermanent`.</span></span> <span data-ttu-id="963d5-232">這些方法會傳回 `RedirectResult` 的實例，並將 `Permanent` 屬性設定為 `true`。</span><span class="sxs-lookup"><span data-stu-id="963d5-232">These methods return an instance of `RedirectResult` with the `Permanent` property set to `true`.</span></span>
- <span data-ttu-id="963d5-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="963d5-233">[HttpStatusCodeResult](https://msdn.microsoft.com/library/system.web.mvc.httpstatuscoderesult(v=VS.98).aspx).</span></span> <span data-ttu-id="963d5-234">傳回使用者指定的 HTTP 狀態碼。</span><span class="sxs-lookup"><span data-stu-id="963d5-234">Returns a user-specified HTTP status code.</span></span>

<a id="BM_JavaScript_and_Ajax_Improvements"></a>

## <a name="javascript-and-ajax-improvements"></a><span data-ttu-id="963d5-235">JavaScript 和 Ajax 的改良功能</span><span class="sxs-lookup"><span data-stu-id="963d5-235">JavaScript and Ajax Improvements</span></span>

<span data-ttu-id="963d5-236">根據預設，MVC 3 中的 Ajax 和驗證協助程式會使用不顯眼的 JavaScript 方法。</span><span class="sxs-lookup"><span data-stu-id="963d5-236">By default, Ajax and validation helpers in MVC 3 use an unobtrusive JavaScript approach.</span></span> <span data-ttu-id="963d5-237">不顯眼的 JavaScript 可避免將內嵌的 JavaScript 插入 HTML。</span><span class="sxs-lookup"><span data-stu-id="963d5-237">Unobtrusive JavaScript avoids injecting inline JavaScript into HTML.</span></span> <span data-ttu-id="963d5-238">這可讓您的 HTML 變得更小且更不雜亂，並可讓您更輕鬆地交換或自訂 JavaScript 程式庫。</span><span class="sxs-lookup"><span data-stu-id="963d5-238">This makes your HTML smaller and less cluttered, and makes it easier to swap out or customize JavaScript libraries.</span></span> <span data-ttu-id="963d5-239">MVC 3 中的驗證協助程式預設也會使用 `jQueryValidate` 外掛程式。</span><span class="sxs-lookup"><span data-stu-id="963d5-239">Validation helpers in MVC 3 also use the `jQueryValidate` plugin by default.</span></span> <span data-ttu-id="963d5-240">如果您想要 MVC 2 行為，可以*使用 web.config 檔案*設定來停用不顯眼的 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="963d5-240">If you want MVC 2 behavior, you can disable unobtrusive JavaScript using a *web.config* file setting.</span></span> <span data-ttu-id="963d5-241">如需 JavaScript 和 Ajax 改良功能的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="963d5-241">For more information about JavaScript and Ajax improvements, see the following resources:</span></span>

- [<span data-ttu-id="963d5-242">維琪百科網站上不顯眼 JavaScript 的基本簡介</span><span class="sxs-lookup"><span data-stu-id="963d5-242">Basic introduction to unobtrusive JavaScript on the Wikipedia site</span></span>](http://en.wikipedia.org/wiki/Unobtrusive_JavaScript)
- [<span data-ttu-id="963d5-243">Brad Wilson 的不顯眼 JavaScript 貼文</span><span class="sxs-lookup"><span data-stu-id="963d5-243">Brad Wilson's Unobtrusive JavaScript Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-ajax.html)
- [<span data-ttu-id="963d5-244">Brad Wilson 的不顯眼 JavaScript 驗證貼文</span><span class="sxs-lookup"><span data-stu-id="963d5-244">Brad Wilson's Unobtrusive JavaScript Validation Post</span></span>](http://bradwilson.typepad.com/blog/2010/10/mvc3-unobtrusive-validation.html)
- <span data-ttu-id="963d5-245">[使用 Razor 和不顯眼的 JavaScript 建立 MVC 3 應用程式](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md)（ASP.NET 網站上的教學課程）</span><span class="sxs-lookup"><span data-stu-id="963d5-245">[Creating a MVC 3 Application with Razor and Unobtrusive JavaScript](overview/older-versions/creating-a-mvc-3-application-with-razor-and-unobtrusive-javascript.md) (tutorial on the ASP.NET site)</span></span>
- [<span data-ttu-id="963d5-246">MVC 3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="963d5-246">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="client-side-validation-enabled-by-default"></a><span data-ttu-id="963d5-247">預設會啟用用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="963d5-247">Client-Side Validation Enabled by Default</span></span>

<span data-ttu-id="963d5-248">在舊版 MVC 中，您必須從視圖明確呼叫 `Html.EnableClientValidation` 方法，才能啟用用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="963d5-248">In earlier versions of MVC, you need to explicitly call the `Html.EnableClientValidation` method from a view in order to enable client-side validation.</span></span> <span data-ttu-id="963d5-249">在 MVC 3 中，因為預設會啟用用戶端驗證，所以不再需要這項功能。</span><span class="sxs-lookup"><span data-stu-id="963d5-249">In MVC 3 this is no longer required because client-side validation is enabled by default.</span></span> <span data-ttu-id="963d5-250">（您可以*使用 web.config 檔案*中的設定來停用此功能）。</span><span class="sxs-lookup"><span data-stu-id="963d5-250">(You can disable this using a setting in the *web.config* file.)</span></span>

<span data-ttu-id="963d5-251">為了讓用戶端驗證能夠正常執行，您仍然需要在您的網站中參考適當的 jQuery 和 jQuery 驗證程式庫。</span><span class="sxs-lookup"><span data-stu-id="963d5-251">In order for client-side validation to work, you still need to reference the appropriate jQuery and jQuery Validation libraries in your site.</span></span> <span data-ttu-id="963d5-252">您可以在自己的伺服器上裝載這些程式庫，或從 Microsoft 或 Google 的 Cdn 之類的內容傳遞網路（CDN）加以參考。</span><span class="sxs-lookup"><span data-stu-id="963d5-252">You can host those libraries on your own server or reference them from a content delivery network (CDN) like the CDNs from Microsoft or Google.</span></span>

### <a name="remote-validator"></a><span data-ttu-id="963d5-253">遠端驗證程式</span><span class="sxs-lookup"><span data-stu-id="963d5-253">Remote Validator</span></span>

<span data-ttu-id="963d5-254">ASP.NET MVC 3 支援新的[RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx)類別，可讓您利用 jQuery 驗證外掛程式的遠端驗證程式支援。</span><span class="sxs-lookup"><span data-stu-id="963d5-254">ASP.NET MVC 3 supports the new [RemoteAttribute](https://msdn.microsoft.com/library/system.web.mvc.remoteattribute(v=VS.98).aspx) class that enables you to take advantage of the jQuery Validation plug-in's remote validator support.</span></span> <span data-ttu-id="963d5-255">這可讓用戶端驗證程式庫自動呼叫您在伺服器上定義的自訂方法，以便執行只能在伺服器端完成的驗證邏輯。</span><span class="sxs-lookup"><span data-stu-id="963d5-255">This enables the client-side validation library to automatically call a custom method that you define on the server in order to perform validation logic that can only be done server-side.</span></span>

<span data-ttu-id="963d5-256">在下列範例中，`Remote` 屬性會指定用戶端驗證將會在 `UsersController` 類別上呼叫名為 `UserNameAvailable` 的動作，以便驗證 `UserName` 欄位。</span><span class="sxs-lookup"><span data-stu-id="963d5-256">In the following example, the `Remote` attribute specifies that client validation will call an action named `UserNameAvailable` on the `UsersController` class in order to validate the `UserName` field.</span></span>

[!code-csharp[Main](mvc3/samples/sample1.cs)]

<span data-ttu-id="963d5-257">下列範例會顯示對應的控制器。</span><span class="sxs-lookup"><span data-stu-id="963d5-257">The following example shows the corresponding controller.</span></span>

[!code-csharp[Main](mvc3/samples/sample2.cs)]

<span data-ttu-id="963d5-258">如需如何使用 `Remote` 屬性的詳細資訊，請參閱 MSDN library 中的 how [to：在 ASP.NET MVC 中執行遠端驗證](https://msdn.microsoft.com/library/gg508808(VS.98).aspx)。</span><span class="sxs-lookup"><span data-stu-id="963d5-258">For more information about how to use the `Remote` attribute, see [How to: Implement Remote Validation in ASP.NET MVC](https://msdn.microsoft.com/library/gg508808(VS.98).aspx) in the MSDN library.</span></span>

### <a name="json-binding-support"></a><span data-ttu-id="963d5-259">JSON 系結支援</span><span class="sxs-lookup"><span data-stu-id="963d5-259">JSON Binding Support</span></span>

<span data-ttu-id="963d5-260">ASP.NET MVC 3 包含內建的 JSON 系結支援，可讓動作方法接收 JSON 編碼的資料，並將它系結至動作方法參數。</span><span class="sxs-lookup"><span data-stu-id="963d5-260">ASP.NET MVC 3 includes built-in JSON binding support that enables action methods to receive JSON-encoded data and model-bind it to action-method parameters.</span></span> <span data-ttu-id="963d5-261">這項功能在涉及用戶端範本和資料系結的案例中很有用。</span><span class="sxs-lookup"><span data-stu-id="963d5-261">This capability is useful in scenarios involving client templates and data binding.</span></span> <span data-ttu-id="963d5-262">（用戶端範本可讓您使用在用戶端上執行的範本來格式化和顯示單一資料項目或一組資料項目）。MVC 3 可讓您輕鬆地在傳送和接收 JSON 資料的伺服器上，使用動作方法來連接用戶端範本。</span><span class="sxs-lookup"><span data-stu-id="963d5-262">(Client templates enable you to format and display a single data item or set of data items by using templates that execute on the client.) MVC 3 enables you to easily connect client templates with action methods on the server that send and receive JSON data.</span></span> <span data-ttu-id="963d5-263">如需 JSON 系結支援的詳細資訊，請參閱[Scott Guthrie 的 MVC 3 預覽 blog 文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)的**JavaScript 和 AJAX 改善**一節。</span><span class="sxs-lookup"><span data-stu-id="963d5-263">For more information about JSON binding support, see the **JavaScript and AJAX Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span>

<a id="BM_Model_Validation_Improvements"></a>

## <a name="model-validation-improvements"></a><span data-ttu-id="963d5-264">模型驗證改善</span><span class="sxs-lookup"><span data-stu-id="963d5-264">Model Validation Improvements</span></span>

### <a name="dataannotations-metadata-attributes"></a><span data-ttu-id="963d5-265">"DataAnnotations" 中繼資料屬性</span><span class="sxs-lookup"><span data-stu-id="963d5-265">"DataAnnotations" Metadata Attributes</span></span>

<span data-ttu-id="963d5-266">ASP.NET MVC 3 支援 `DataAnnotations` 中繼資料屬性，例如 `DisplayAttribute`。</span><span class="sxs-lookup"><span data-stu-id="963d5-266">ASP.NET MVC 3 supports `DataAnnotations` metadata attributes such as `DisplayAttribute`.</span></span>

### <a name="validationattribute-class"></a><span data-ttu-id="963d5-267">"ValidationAttribute" 類別</span><span class="sxs-lookup"><span data-stu-id="963d5-267">"ValidationAttribute" Class</span></span>

<span data-ttu-id="963d5-268">`ValidationAttribute` 類別已在 .NET Framework 4 中改善，以支援新的 `IsValid` 多載，以提供有關目前驗證內容的詳細資訊，例如要驗證的物件。</span><span class="sxs-lookup"><span data-stu-id="963d5-268">The `ValidationAttribute` class was improved in the .NET Framework 4 to support a new `IsValid` overload that provides more information about the current validation context, such as what object is being validated.</span></span> <span data-ttu-id="963d5-269">這可提供更豐富的案例，讓您可以根據模型的另一個屬性來驗證目前的值。</span><span class="sxs-lookup"><span data-stu-id="963d5-269">This enables richer scenarios where you can validate the current value based on another property of the model.</span></span> <span data-ttu-id="963d5-270">例如，新的 `CompareAttribute` 屬性可讓您比較模型中兩個屬性的值。</span><span class="sxs-lookup"><span data-stu-id="963d5-270">For example, the new `CompareAttribute` attribute lets you compare the values of two properties of a model.</span></span> <span data-ttu-id="963d5-271">在下列範例中，`ComparePassword` 屬性必須符合 `Password` 欄位，才會生效。</span><span class="sxs-lookup"><span data-stu-id="963d5-271">In the following example, the `ComparePassword` property must match the `Password` field in order to be valid.</span></span>

[!code-csharp[Main](mvc3/samples/sample3.cs)]

### <a name="validation-interfaces"></a><span data-ttu-id="963d5-272">驗證介面</span><span class="sxs-lookup"><span data-stu-id="963d5-272">Validation Interfaces</span></span>

<span data-ttu-id="963d5-273">[IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx)介面可讓您執行模型層級的驗證，並可讓您提供整體模型狀態特有的驗證錯誤訊息，或模型內的兩個屬性之間。</span><span class="sxs-lookup"><span data-stu-id="963d5-273">The [IValidatableObject](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.ivalidatableobject.aspx) interface enables you to perform model-level validation, and it enables you to provide validation error messages that are specific to the state of the overall model, or between two properties within the model.</span></span> <span data-ttu-id="963d5-274">在模型系結時，MVC 3 現在會從 `IValidatableObject` 介面中抓取錯誤，並使用內建的 HTML 表單協助程式自動旗標或反白顯示視圖中受影響的欄位。</span><span class="sxs-lookup"><span data-stu-id="963d5-274">MVC 3 now retrieves errors from the `IValidatableObject` interface when model binding, and automatically flags or highlights affected fields within a view using the built-in HTML form helpers.</span></span>

<span data-ttu-id="963d5-275">[IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx)介面可讓 ASP.NET MVC 在執行時間探索驗證程式是否支援用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="963d5-275">The [IClientValidatable](https://msdn.microsoft.com/library/system.web.mvc.iclientvalidatable(v=VS.98).aspx) interface enables ASP.NET MVC to discover at run time whether a validator has support for client validation.</span></span> <span data-ttu-id="963d5-276">這個介面已設計成可與各種不同的驗證架構整合。</span><span class="sxs-lookup"><span data-stu-id="963d5-276">This interface has been designed so that it can be integrated with a variety of validation frameworks.</span></span>

<span data-ttu-id="963d5-277">如需驗證介面的詳細資訊，請參閱[Scott Guthrie 的 MVC 3 預覽 blog 文章](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx)的**模型驗證改善**一節。</span><span class="sxs-lookup"><span data-stu-id="963d5-277">For more information about validation interfaces, see the **Model Validation Improvements** section of [Scott Guthrie's MVC 3 Preview blog post](https://weblogs.asp.net/scottgu/archive/2010/07/27/introducing-asp-net-mvc-3-preview-1.aspx).</span></span> <span data-ttu-id="963d5-278">（不過請注意，在 blog 中，"IValidateObject" 的參考應該是 "IValidatableObject"）。</span><span class="sxs-lookup"><span data-stu-id="963d5-278">(However, note that the reference to "IValidateObject" in the blog should be "IValidatableObject".)</span></span>

<a id="BM_Dependency_Injection_Improvements"></a>

## <a name="dependency-injection-improvements"></a><span data-ttu-id="963d5-279">相依性插入改良功能</span><span class="sxs-lookup"><span data-stu-id="963d5-279">Dependency Injection Improvements</span></span>

<span data-ttu-id="963d5-280">ASP.NET MVC 3 針對套用相依性插入（DI），以及與相依性插入或反轉控制（IOC）容器進行整合，提供更好的支援。</span><span class="sxs-lookup"><span data-stu-id="963d5-280">ASP.NET MVC 3 provides better support for applying Dependency Injection (DI) and for integrating with Dependency Injection or Inversion of Control (IOC) containers.</span></span> <span data-ttu-id="963d5-281">已在下欄區域中新增對 DI 的支援：</span><span class="sxs-lookup"><span data-stu-id="963d5-281">Support for DI has been added in the following areas:</span></span>

- <span data-ttu-id="963d5-282">控制器（註冊和插入控制器工廠，插入控制器）。</span><span class="sxs-lookup"><span data-stu-id="963d5-282">Controllers (registering and injecting controller factories, injecting controllers).</span></span>
- <span data-ttu-id="963d5-283">Views （註冊和插入視圖引擎，將相依性插入至視圖頁面）。</span><span class="sxs-lookup"><span data-stu-id="963d5-283">Views (registering and injecting view engines, injecting dependencies into view pages).</span></span>
- <span data-ttu-id="963d5-284">動作篩選（尋找和插入篩選器）。</span><span class="sxs-lookup"><span data-stu-id="963d5-284">Action filters (locating and injecting filters).</span></span>
- <span data-ttu-id="963d5-285">模型系結器（註冊和插入）。</span><span class="sxs-lookup"><span data-stu-id="963d5-285">Model binders (registering and injecting).</span></span>
- <span data-ttu-id="963d5-286">模型驗證提供者（註冊和插入）。</span><span class="sxs-lookup"><span data-stu-id="963d5-286">Model validation providers (registering and injecting).</span></span>
- <span data-ttu-id="963d5-287">模型中繼資料提供者（註冊和插入）。</span><span class="sxs-lookup"><span data-stu-id="963d5-287">Model metadata providers (registering and injecting).</span></span>
- <span data-ttu-id="963d5-288">值提供者（註冊和插入）。</span><span class="sxs-lookup"><span data-stu-id="963d5-288">Value providers (registering and injecting).</span></span>

<span data-ttu-id="963d5-289">MVC 3 支援[泛型服務定位器](https://github.com/unitycontainer/commonservicelocator)程式庫，以及支援該程式庫之 `IServiceLocator` 介面的任何 DI 容器。</span><span class="sxs-lookup"><span data-stu-id="963d5-289">MVC 3 supports the [Common Service Locator](https://github.com/unitycontainer/commonservicelocator) library and any DI container that supports that library's `IServiceLocator` interface.</span></span> <span data-ttu-id="963d5-290">它也支援新的 `IDependencyResolver` 介面，可讓您更輕鬆地整合 DI 架構。</span><span class="sxs-lookup"><span data-stu-id="963d5-290">It also supports a new `IDependencyResolver` interface that makes it easier to integrate DI frameworks.</span></span>

<span data-ttu-id="963d5-291">如需有關 MVC 3 中 DI 的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="963d5-291">For more information about DI in MVC 3, see the following resources:</span></span>

- [<span data-ttu-id="963d5-292">Brad Wilson 針對服務位置的一系列 blog 文章</span><span class="sxs-lookup"><span data-stu-id="963d5-292">Brad Wilson's series of blog posts on Service Location</span></span>](http://bradwilson.typepad.com/blog/2010/07/service-location-pt1-introduction.html)
- [<span data-ttu-id="963d5-293">MVC 3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="963d5-293">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

<a id="BM_Other_New_Features"></a>

## <a name="other-new-features"></a><span data-ttu-id="963d5-294">其他新功能</span><span class="sxs-lookup"><span data-stu-id="963d5-294">Other New Features</span></span>

### <a name="nuget-integration"></a><span data-ttu-id="963d5-295">NuGet 整合</span><span class="sxs-lookup"><span data-stu-id="963d5-295">NuGet Integration</span></span>

<span data-ttu-id="963d5-296">ASP.NET MVC 3 會在安裝過程中自動安裝並啟用 NuGet。</span><span class="sxs-lookup"><span data-stu-id="963d5-296">ASP.NET MVC 3 automatically installs and enables NuGet as part of its setup.</span></span> <span data-ttu-id="963d5-297">NuGet 是免費的開放原始碼套件管理員，可讓您輕鬆地在專案中尋找、安裝及使用 .NET 程式庫和工具。</span><span class="sxs-lookup"><span data-stu-id="963d5-297">NuGet is a free open-source package manager that makes it easy to find, install, and use .NET libraries and tools in your projects.</span></span> <span data-ttu-id="963d5-298">它適用于所有 Visual Studio 專案類型（包括 ASP.NET Web Forms 和 ASP.NET MVC）。</span><span class="sxs-lookup"><span data-stu-id="963d5-298">It works with all Visual Studio project types (including ASP.NET Web Forms and ASP.NET MVC).</span></span>

<span data-ttu-id="963d5-299">NuGet 可讓維護開放原始碼專案（例如 Moq、NHibernate、Ninject、StructureMap、NUnit、Windsor、RhinoMocks 和 Elmah 等專案）的開發人員封裝其程式庫，並在線上元件庫中註冊。</span><span class="sxs-lookup"><span data-stu-id="963d5-299">NuGet enables developers who maintain open source projects (for example, projects like Moq, NHibernate, Ninject, StructureMap, NUnit, Windsor, RhinoMocks, and Elmah) to package their libraries and register them in an online gallery.</span></span> <span data-ttu-id="963d5-300">然後，想要使用其中一個程式庫來尋找套件，並將它安裝在正在處理的專案中的 .NET 開發人員很容易。</span><span class="sxs-lookup"><span data-stu-id="963d5-300">It is then easy for .NET developers who want to use one of these libraries to find the package and install it in projects they are working on.</span></span>

<span data-ttu-id="963d5-301">透過 ASP.NET 3 工具更新，專案範本包含已預先安裝的 JavaScript 程式庫 NuGet 套件，因此可以透過 NuGet 進行更新。</span><span class="sxs-lookup"><span data-stu-id="963d5-301">With the ASP.NET 3 Tools Update, project templates include JavaScript libraries pre-installed NuGet packages, so they are updatable via NuGet.</span></span> <span data-ttu-id="963d5-302">Entity Framework Code First 也會預先安裝為 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="963d5-302">Entity Framework Code First is also pre-installed as a NuGet package.</span></span>

<span data-ttu-id="963d5-303">如需 NuGet 的詳細資訊，請參閱 [NuGet 文件](https://docs.microsoft.com/nuget/) (英文)。</span><span class="sxs-lookup"><span data-stu-id="963d5-303">For more information about NuGet, see the [NuGet documentation](https://docs.microsoft.com/nuget/).</span></span>

### <a name="partial-page-output-caching"></a><span data-ttu-id="963d5-304">部分頁面輸出快取</span><span class="sxs-lookup"><span data-stu-id="963d5-304">Partial-Page Output Caching</span></span>

<span data-ttu-id="963d5-305">ASP.NET MVC 支援從第1版開始的完整頁面回應輸出快取。</span><span class="sxs-lookup"><span data-stu-id="963d5-305">ASP.NET MVC has supported output caching of full page responses since version 1.</span></span> <span data-ttu-id="963d5-306">MVC 3 也支援部分頁面輸出快取，可讓您輕鬆地快取區域或回應片段。</span><span class="sxs-lookup"><span data-stu-id="963d5-306">MVC 3 also supports partial-page output caching, which allows you to easily cache regions or fragments of a response.</span></span> <span data-ttu-id="963d5-307">如需快取的詳細資訊，請參閱 Scott Guthrie 的「**部分頁面輸出**快取」一節，其位於 mvc [3 發行候選版本](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)和[Mvc 3 版本](../whitepapers/mvc3-release-notes.md)資訊的**子動作輸出**快取一節。</span><span class="sxs-lookup"><span data-stu-id="963d5-307">For more information about caching, see the **Partial Page Output Caching** section of [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx) and the **Child Action Output Caching** section of the [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="granular-control-over-request-validation"></a><span data-ttu-id="963d5-308">對要求驗證的細微控制</span><span class="sxs-lookup"><span data-stu-id="963d5-308">Granular Control over Request Validation</span></span>

<span data-ttu-id="963d5-309">ASP.NET MVC 具有內建的要求驗證，可自動協助防止 XSS 和 HTML 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="963d5-309">ASP.NET MVC has built-in request validation that automatically helps protect against XSS and HTML injection attacks.</span></span> <span data-ttu-id="963d5-310">不過，有時候您會想要明確停用要求驗證，例如，如果您想要讓使用者張貼 HTML 內容（例如，在 blog 專案或 CMS 內容中）。</span><span class="sxs-lookup"><span data-stu-id="963d5-310">However, sometimes you want to explicitly disable request validation, such as if you want to let users post HTML content (for example, in blog entries or CMS content).</span></span> <span data-ttu-id="963d5-311">您現在可以在模型系結期間，將[AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx)屬性新增至模型或視圖模型，以停用每個屬性的要求驗證。</span><span class="sxs-lookup"><span data-stu-id="963d5-311">You can now add an [AllowHtml](https://msdn.microsoft.com/library/system.web.mvc.allowhtmlattribute(v=VS.98).aspx) attribute to models or view models to disable request validation on a per-property basis during model binding.</span></span> <span data-ttu-id="963d5-312">如需要求驗證的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="963d5-312">For more information about request validation, see the following resources:</span></span>

- <span data-ttu-id="963d5-313">[Scott Guthrie 在 MVC 3 發行候選版本的 blog 文章](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx)中，不**顯眼的 JavaScript 和驗證**一節。</span><span class="sxs-lookup"><span data-stu-id="963d5-313">The **Unobtrusive JavaScript and Validation** section in [Scott Guthrie's blog post on the MVC 3 release candidate](https://weblogs.asp.net/scottgu/archive/2010/11/09/announcing-the-asp-net-mvc-3-release-candidate.aspx).</span></span>
- [<span data-ttu-id="963d5-314">MVC 3 版本資訊</span><span class="sxs-lookup"><span data-stu-id="963d5-314">MVC 3 Release Notes</span></span>](../whitepapers/mvc3-release-notes.md)

### <a name="extensible-new-project-dialog-box"></a><span data-ttu-id="963d5-315">可擴充的 [新增專案] 對話方塊</span><span class="sxs-lookup"><span data-stu-id="963d5-315">Extensible "New Project" Dialog Box</span></span>

<span data-ttu-id="963d5-316">在 ASP.NET MVC 3 中，您可以將專案範本、視圖引擎和單元測試專案架構加入至 [**新增專案**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="963d5-316">In ASP.NET MVC 3 you can add project templates, view engines, and unit test project frameworks to the **New Project** dialog box.</span></span>

### <a name="template-scaffolding-improvements"></a><span data-ttu-id="963d5-317">範本樣板的改良功能</span><span class="sxs-lookup"><span data-stu-id="963d5-317">Template Scaffolding Improvements</span></span>

<span data-ttu-id="963d5-318">ASP.NET MVC 3 樣板範本會更妥善地識別模型上的主鍵屬性，並適當地處理它們，而不是使用舊版 MVC。</span><span class="sxs-lookup"><span data-stu-id="963d5-318">ASP.NET MVC 3 scaffolding templates do a better job of identifying primary-key properties on models and handling them appropriately than in earlier versions of MVC.</span></span> <span data-ttu-id="963d5-319">（例如，現在，樣板範本會確保主鍵不會 scaffold 為可編輯的表單欄位）。</span><span class="sxs-lookup"><span data-stu-id="963d5-319">(For example, the scaffolding templates now make sure that the primary key is not scaffolded as an editable form field.)</span></span>

<span data-ttu-id="963d5-320">根據預設，[建立和編輯 scaffold] 現在會使用 `Html.EditorFor` helper，而不是 `Html.TextBoxFor` 協助程式。</span><span class="sxs-lookup"><span data-stu-id="963d5-320">By default, the Create and Edit scaffolds now use the `Html.EditorFor` helper instead of the `Html.TextBoxFor` helper.</span></span> <span data-ttu-id="963d5-321">這會在 [**加入視圖**] 對話方塊產生視圖時，以資料批註屬性的形式改善模型上的中繼資料支援。</span><span class="sxs-lookup"><span data-stu-id="963d5-321">This improves support for metadata on the model in the form of data annotation attributes when the **Add View** dialog box generates a view.</span></span>

### <a name="new-overloads-for-htmllabelfor-and-htmllabelformodel"></a><span data-ttu-id="963d5-322">"LabelFor" 和 "Html. LabelForModel" 的新多載</span><span class="sxs-lookup"><span data-stu-id="963d5-322">New Overloads for "Html.LabelFor" and "Html.LabelForModel"</span></span>

<span data-ttu-id="963d5-323">已為 `LabelFor` 和 `LabelForModel` helper 方法加入新的方法多載。</span><span class="sxs-lookup"><span data-stu-id="963d5-323">New method overloads have been added for the `LabelFor` and `LabelForModel` helper methods.</span></span> <span data-ttu-id="963d5-324">新的多載可讓您指定或覆寫標籤文字。</span><span class="sxs-lookup"><span data-stu-id="963d5-324">The new overloads enable you to specify or override the label text.</span></span>

### <a name="sessionless-controller-support"></a><span data-ttu-id="963d5-325">無會話控制器支援</span><span class="sxs-lookup"><span data-stu-id="963d5-325">Sessionless Controller Support</span></span>

<span data-ttu-id="963d5-326">在 ASP.NET MVC 3 中，您可以指出您是否要讓控制器類別使用會話狀態，如果是，會話狀態應該是讀取/寫入或唯讀。</span><span class="sxs-lookup"><span data-stu-id="963d5-326">In ASP.NET MVC 3 you can indicate whether you want a controller class to use session state, and if so, whether session state should be read/write or read-only.</span></span> <span data-ttu-id="963d5-327">如需無會話控制器支援的詳細資訊，請參閱[MVC 3 版本](../whitepapers/mvc3-release-notes.md)資訊。</span><span class="sxs-lookup"><span data-stu-id="963d5-327">For more information about sessionless controller support, see [MVC 3 Release Notes](../whitepapers/mvc3-release-notes.md).</span></span>

### <a name="new-additionalmetadataattribute-class"></a><span data-ttu-id="963d5-328">新的 "AdditionalMetadataAttribute" 類別</span><span class="sxs-lookup"><span data-stu-id="963d5-328">New "AdditionalMetadataAttribute" Class</span></span>

<span data-ttu-id="963d5-329">您可以使用[AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx)屬性來填入模型屬性的 `ModelMetadata.AdditionalValues` 字典。</span><span class="sxs-lookup"><span data-stu-id="963d5-329">You can use the [AdditionalMetadata](https://msdn.microsoft.com/library/system.web.mvc.additionalmetadataattribute(v=VS.98).aspx) attribute to populate the `ModelMetadata.AdditionalValues` dictionary for a model property.</span></span> <span data-ttu-id="963d5-330">例如，如果視圖模型具有只應顯示給系統管理員的屬性，您可以標注該屬性，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="963d5-330">For example, if a view model has a property that should be displayed only to an administrator, you can annotate that property as shown in the following example:</span></span>

[!code-csharp[Main](mvc3/samples/sample4.cs)]

<span data-ttu-id="963d5-331">當呈現產品視圖模型時，任何顯示或編輯器範本都會提供此中繼資料。</span><span class="sxs-lookup"><span data-stu-id="963d5-331">This metadata is made available to any display or editor template when a product view model is rendered.</span></span> <span data-ttu-id="963d5-332">您可以由您來解讀中繼資料資訊。</span><span class="sxs-lookup"><span data-stu-id="963d5-332">It is up to you to interpret the metadata information.</span></span>

### <a name="accountcontroller-improvements"></a><span data-ttu-id="963d5-333">AccountController 改良功能</span><span class="sxs-lookup"><span data-stu-id="963d5-333">AccountController improvements</span></span>

<span data-ttu-id="963d5-334">網際網路專案範本中的 AccountController 已大幅改善。</span><span class="sxs-lookup"><span data-stu-id="963d5-334">The AccountController in the Internet project template has been greatly improved.</span></span>

### <a name="new-intranet-project-template"></a><span data-ttu-id="963d5-335">新的內部網路專案範本</span><span class="sxs-lookup"><span data-stu-id="963d5-335">New Intranet Project Template</span></span>

<span data-ttu-id="963d5-336">其中包含新的內部網路專案範本，可啟用 Windows 驗證並移除 AccountController。</span><span class="sxs-lookup"><span data-stu-id="963d5-336">A new Intranet Project Template is included which enables Windows Authentication and removes the AccountController.</span></span>
