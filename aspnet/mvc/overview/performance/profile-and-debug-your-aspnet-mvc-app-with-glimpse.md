---
uid: mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
title: 使用粗略的分析和 ASP.NET MVC 應用程式Microsoft Docs
author: Rick-Anderson
description: 「一覽」是一系列蓬勃發展且持續成長的開放原始碼 NuGet 套件，提供詳細的效能、偵錯工具和診斷資訊，讓您 ASP.NET 。
ms.author: riande
ms.date: 03/26/2015
ms.assetid: c205805f-efdd-4fa7-9616-f26eab180611
msc.legacyurl: /mvc/overview/performance/profile-and-debug-your-aspnet-mvc-app-with-glimpse
msc.type: authoredcontent
ms.openlocfilehash: d3689147a3bc3aa1f4180c377d2483a94bdd95a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78538532"
---
# <a name="profile-and-debug-your-aspnet-mvc-app-with-glimpse"></a><span data-ttu-id="19425-103">使用 Glimpse 分析 ASP.NET MVC 應用程式以對其進行偵錯</span><span class="sxs-lookup"><span data-stu-id="19425-103">Profile and debug your ASP.NET MVC app with Glimpse</span></span>

<span data-ttu-id="19425-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="19425-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="19425-105">「一覽」是蓬勃發展且持續成長的開放原始碼 NuGet 套件系列，提供 ASP.NET 應用程式的詳細效能、偵錯工具和診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="19425-105">Glimpse is a thriving and growing family of open source NuGet packages that provides detailed performance, debugging and diagnostic information for ASP.NET apps.</span></span> <span data-ttu-id="19425-106">在每一頁的底部，安裝、輕量、超高，並顯示關鍵效能計量是很簡單的。</span><span class="sxs-lookup"><span data-stu-id="19425-106">It's trivial to install, lightweight, ultra-fast, and displays key performance metrics at the bottom of every page.</span></span> <span data-ttu-id="19425-107">當您需要瞭解伺服器上的狀況時，它可讓您向下切入至您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="19425-107">It allows you to drill down into your app when you need to find out what's going on at the server.</span></span> <span data-ttu-id="19425-108">我們建議您在整個開發週期（包括您的 Azure 測試環境）中使用它，以提供非常重要的資訊。</span><span class="sxs-lookup"><span data-stu-id="19425-108">Glimpse provides so much valuable information we recommend you use it throughout your development cycle, including your Azure test environment.</span></span> <span data-ttu-id="19425-109">雖然[Fiddler](http://www.telerik.com/fiddler)和[F-12 開發工具](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx)提供用戶端視圖，但還是會從伺服器提供詳細的觀點。</span><span class="sxs-lookup"><span data-stu-id="19425-109">While [Fiddler](http://www.telerik.com/fiddler) and the [F-12 development tools](https://msdn.microsoft.com/library/ie/gg589512(v=vs.85).aspx) provide a client side view, Glimpse provides a detailed view from the server.</span></span> <span data-ttu-id="19425-110">本教學課程將著重于使用 ASP.NET MVC 和 EF 封裝，但有許多其他套件可供使用。</span><span class="sxs-lookup"><span data-stu-id="19425-110">This tutorial will focus on using the Glimpse ASP.NET MVC and EF packages, but many other packages are available.</span></span> <span data-ttu-id="19425-111">在可能的情況下，我會連結到適當的[粗略](http://getglimpse.com/Docs/)檔，協助維護。</span><span class="sxs-lookup"><span data-stu-id="19425-111">Where possible I will link to the appropriate [Glimpse docs](http://getglimpse.com/Docs/) which I help maintain.</span></span> <span data-ttu-id="19425-112">「一覽」是一個開放原始碼專案，您也可以參與原始程式碼和檔。</span><span class="sxs-lookup"><span data-stu-id="19425-112">Glimpse is an open source project, you too can contribute to the source code and the docs.</span></span>

- [<span data-ttu-id="19425-113">安裝一覽</span><span class="sxs-lookup"><span data-stu-id="19425-113">Installing Glimpse</span></span>](#ig)
- [<span data-ttu-id="19425-114">啟用對 localhost 的粗略</span><span class="sxs-lookup"><span data-stu-id="19425-114">Enable Glimpse for localhost</span></span>](#eg)
- <span data-ttu-id="19425-115">[[時間軸] 索引標籤](#Time)</span><span class="sxs-lookup"><span data-stu-id="19425-115">[The Timeline tab](#Time)</span></span>
- [<span data-ttu-id="19425-116">模型繫結</span><span class="sxs-lookup"><span data-stu-id="19425-116">Model Binding</span></span>](#mb)
- [<span data-ttu-id="19425-117">路由</span><span class="sxs-lookup"><span data-stu-id="19425-117">Routes</span></span>](#route)
- [<span data-ttu-id="19425-118">使用 Azure 上的粗略操作</span><span class="sxs-lookup"><span data-stu-id="19425-118">Using Glimpse on Azure</span></span>](#da)
- [<span data-ttu-id="19425-119">其他資源</span><span class="sxs-lookup"><span data-stu-id="19425-119">Additional Resources</span></span>](#addRes)

<a id="ig"></a>
## <a name="installing-glimpse"></a><span data-ttu-id="19425-120">安裝一覽</span><span class="sxs-lookup"><span data-stu-id="19425-120">Installing Glimpse</span></span>

<span data-ttu-id="19425-121">您可以從 NuGet 套件管理員主控台，或從 [**管理 NuGet 套件**] 主控台安裝。</span><span class="sxs-lookup"><span data-stu-id="19425-121">You can install Glimpse from the NuGet package manager console or from the **Manage NuGet Packages** console.</span></span> <span data-ttu-id="19425-122">在此示範中，我將安裝 Mvc5 和 EF6 套件：</span><span class="sxs-lookup"><span data-stu-id="19425-122">For this demo, I'll install the Mvc5 and EF6 packages:</span></span>

![從 NuGet Dlg 安裝一覽](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image1.png)

<span data-ttu-id="19425-124">搜尋*粗略的 EF*</span><span class="sxs-lookup"><span data-stu-id="19425-124">Search for *Glimpse.EF*</span></span>

![從 NuGet 安裝 dlg 的 EF](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image2.png)

<span data-ttu-id="19425-126">藉由選取 [**已安裝的套件**]，您可以看到已安裝的「粗略相依模組」：</span><span class="sxs-lookup"><span data-stu-id="19425-126">By selecting **Installed packages**, you can see the Glimpse dependent modules installed:</span></span>

![已安裝從 DLg 開始進行封裝](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image3.png)

<span data-ttu-id="19425-128">下列命令會從套件管理員主控台安裝 MVC5 和 EF6 模組：</span><span class="sxs-lookup"><span data-stu-id="19425-128">The following commands install Glimpse MVC5 and EF6 modules from the package manager console:</span></span>

[!code-console[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample1.cmd)]

<a id="eg"></a>
## <a name="enable-glimpse-for-localhost"></a><span data-ttu-id="19425-129">啟用對 localhost 的粗略</span><span class="sxs-lookup"><span data-stu-id="19425-129">Enable Glimpse for localhost</span></span>

<span data-ttu-id="19425-130">流覽至 http://localhost:&lt;p 埠 o #&gt;/glimpse.axd，然後按一下 [<strong>開啟</strong>] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="19425-130">Navigate to http://localhost:&lt;port #&gt;/glimpse.axd and click the <strong>Turn Glimpse On</strong> button.</span></span>

![粗略頁面](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image4.png)

<span data-ttu-id="19425-132">如果您有顯示 [我的最愛] 列，您可以拖放 [粗略] 按鈕，並將其新增為 bookmarklets：</span><span class="sxs-lookup"><span data-stu-id="19425-132">If you have your favorites bar displayed, you can drag and drop the Glimpse buttons and add them as bookmarklets:</span></span>

![熟悉 bookmarklets 的 IE](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image5.png)

<span data-ttu-id="19425-134">您現在可以流覽您的應用程式，並在頁面底部顯示**標題顯示**（抬頭顯示器）。</span><span class="sxs-lookup"><span data-stu-id="19425-134">You can now navigate your app, and the **Heads Up Display** (HUD) is shown at the bottom of the page.</span></span>

![具有抬頭顯示器的連絡人管理員頁面](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image6.png)

<span data-ttu-id="19425-136">[一覽[抬頭顯示器] 頁面](http://getglimpse.com/Docs/Heads-up-Display)會詳細說明上面顯示的計時資訊。</span><span class="sxs-lookup"><span data-stu-id="19425-136">The [Glimpse HUD page](http://getglimpse.com/Docs/Heads-up-Display) details the timing information shown above.</span></span> <span data-ttu-id="19425-137">抬頭顯示器所顯示的不顯眼效能資料，可以立即通知您問題，然後才進入測試週期。</span><span class="sxs-lookup"><span data-stu-id="19425-137">The unobtrusive performance data the HUD displays can notify you of a problem immediately - before you get to the test cycle.</span></span> <span data-ttu-id="19425-138">按一下右下角的 &quot;g&quot; 會顯示 [一覽] 面板：</span><span class="sxs-lookup"><span data-stu-id="19425-138">Clicking on the &quot;g&quot; in the lower right corner brings up the Glimpse panel:</span></span>

![一覽面板](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image7.png)

<span data-ttu-id="19425-140">在上圖中，已選取 [[執行]](http://getglimpse.com/Docs/Execution-Tab)索引標籤，它會顯示管線中動作和篩選準則的計時詳細資料。</span><span class="sxs-lookup"><span data-stu-id="19425-140">In the image above, the [Execution tab](http://getglimpse.com/Docs/Execution-Tab) is selected, which shows timing details of the actions and filters in the pipeline.</span></span> <span data-ttu-id="19425-141">您可以看到我的[停止監看篩選計時器](http://www.nuget.org/packages/StopWatch/)在管線的第6階段開始。</span><span class="sxs-lookup"><span data-stu-id="19425-141">You can see my [Stop Watch filter timer](http://www.nuget.org/packages/StopWatch/) start at stage 6 of the pipeline.</span></span> <span data-ttu-id="19425-142">雖然我的輕量計時器可以提供有用的設定檔/時間資料，但它卻遺漏了授權和呈現視圖所花費的所有時間。</span><span class="sxs-lookup"><span data-stu-id="19425-142">While my light weight timer can provide useful profile/timing data, it misses all the time spent in authorization and rendering the view.</span></span> <span data-ttu-id="19425-143">您可以在設定檔中閱讀關於我[的計時器，以及將 ASP.NET MVC 應用程式一直到 Azure 的時間](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx)。</span><span class="sxs-lookup"><span data-stu-id="19425-143">You can read about my timer at [Profile and Time your ASP.NET MVC app all the way to Azure](https://blogs.msdn.com/b/webdev/archive/2014/07/29/profile-and-time-your-asp-net-mvc-app-all-the-way-to-azure.aspx).</span></span> <span data-ttu-id="19425-144">[索引標籤] 頁面會提供每個索引標籤上詳細[資訊的連結](http://getglimpse.com/Docs/Tabs)。</span><span class="sxs-lookup"><span data-stu-id="19425-144">The [Tabs](http://getglimpse.com/Docs/Tabs) page provides links to detailed information on each tab.</span></span>

<a id="Time"></a>
## <a name="the-timeline-tab"></a><span data-ttu-id="19425-145">[時間軸] 索引標籤</span><span class="sxs-lookup"><span data-stu-id="19425-145">The Timeline tab</span></span>

<span data-ttu-id="19425-146">我已修改 Tom 作者: dykstra 的未完成[EF 6/MVC 5 教學](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程，並將下列程式碼變更為講師控制器：</span><span class="sxs-lookup"><span data-stu-id="19425-146">I've modified Tom Dykstra's outstanding [EF 6/MVC 5 tutorial](../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) with the following code change to the instructors controller:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample2.cs?highlight=1,20-31)]

<span data-ttu-id="19425-147">上述程式碼可讓我傳入查詢字串（`eager`），以控制資料的積極式或明確載入。</span><span class="sxs-lookup"><span data-stu-id="19425-147">The code above allows me to pass in query string (`eager`) to control eager or explicit loading of data.</span></span> <span data-ttu-id="19425-148">在下圖中，會使用明確載入，而 [計時] 頁面會顯示在 `Index` 動作方法中載入的每個註冊：</span><span class="sxs-lookup"><span data-stu-id="19425-148">In the image below, explicit loading is used and the timing page shows each enrollment loaded in the `Index` action method:</span></span>

![Explicit Loading - 明確載入](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image8.png)

<span data-ttu-id="19425-150">在下列程式碼中，會指定 [積極]，並在呼叫 `Index` view 之後提取每個註冊：</span><span class="sxs-lookup"><span data-stu-id="19425-150">In the following code, eager is specified, and each enrollment is fetched after the `Index` view is called:</span></span>

![指定了積極的](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image9.png)

<span data-ttu-id="19425-152">您可以將滑鼠停留在某個時間區段上，以取得詳細的計時資訊：</span><span class="sxs-lookup"><span data-stu-id="19425-152">You can hover over a time segment to get detailed timing information:</span></span>

![將滑鼠暫留以查看詳細計時](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image10.png)

<a id="mb"></a>
## <a name="model-binding"></a><span data-ttu-id="19425-154">模型繫結</span><span class="sxs-lookup"><span data-stu-id="19425-154">Model Binding</span></span>

<span data-ttu-id="19425-155">[[模型](http://getglimpse.com/Docs/Model-Binding-Tab)系結] 索引標籤可提供豐富的資訊，協助您瞭解如何系結表單變數，以及為何某些不會如預期般系結。</span><span class="sxs-lookup"><span data-stu-id="19425-155">The [model binding tab](http://getglimpse.com/Docs/Model-Binding-Tab) provides a wealth of information to help you understand how your form variables are bound and why some are not bound as would expect.</span></span> <span data-ttu-id="19425-156">下圖顯示 **？**</span><span class="sxs-lookup"><span data-stu-id="19425-156">The image below shows the **?**</span></span> <span data-ttu-id="19425-157">圖示，您可以按一下它來顯示該功能的粗略說明頁面。</span><span class="sxs-lookup"><span data-stu-id="19425-157">icon, which you can click on to bring up the glimpse help page for that feature.</span></span>

![查看模型系結視圖](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image11.png)

<a id="route"></a>
## <a name="routes"></a><span data-ttu-id="19425-159">路由</span><span class="sxs-lookup"><span data-stu-id="19425-159">Routes</span></span>

 <span data-ttu-id="19425-160">[粗略路由] 索引標籤可協助您進行調試和瞭解路由。</span><span class="sxs-lookup"><span data-stu-id="19425-160">The Glimpse Routes tab will can help you debug and understand routing.</span></span> <span data-ttu-id="19425-161">在下圖中，已選取 [產品路線] （並以綠色顯示「一覽」慣例）。</span><span class="sxs-lookup"><span data-stu-id="19425-161">In the image below, the product route is selected (and it shows in green, a Glimpse convention).</span></span> <span data-ttu-id="19425-162">![選取的產品名稱](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) 路由條件約束、區域和資料權杖也會顯示。</span><span class="sxs-lookup"><span data-stu-id="19425-162">![product name selected](profile-and-debug-your-aspnet-mvc-app-with-glimpse/_static/image12.png) Route constraints, Areas and data tokens are also displayed.</span></span> <span data-ttu-id="19425-163">如需詳細資訊，請參閱[在 ASP.NET MVC 5 中](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx)查看[路由](http://getglimpse.com/Docs/Routes-Tab)和屬性路由。</span><span class="sxs-lookup"><span data-stu-id="19425-163">See [Glimpse Routes](http://getglimpse.com/Docs/Routes-Tab) and [Attribute Routing in ASP.NET MVC 5](https://blogs.msdn.com/b/webdev/archive/2013/10/17/attribute-routing-in-asp-net-mvc-5.aspx) for more information.</span></span> 

<a id="da"></a>
## <a name="using-glimpse-on-azure"></a><span data-ttu-id="19425-164">使用 Azure 上的粗略操作</span><span class="sxs-lookup"><span data-stu-id="19425-164">Using Glimpse on Azure</span></span>

<span data-ttu-id="19425-165">[粗略的預設安全性原則] 只允許從本機主機顯示資料。</span><span class="sxs-lookup"><span data-stu-id="19425-165">The Glimpse default security policy only allows Glimpse data to be displayed from local host.</span></span> <span data-ttu-id="19425-166">您可以變更此安全性原則，讓您可以在遠端伺服器（例如 Azure 上的 web 應用程式）上查看此資料。</span><span class="sxs-lookup"><span data-stu-id="19425-166">You can change this security policy so you can view this data on a remote server (such as a web app on Azure).</span></span> <span data-ttu-id="19425-167">針對 Azure 上的測試環境，請在*web.config*檔案底部新增反白顯示的標記，以讓您大致瞭解：</span><span class="sxs-lookup"><span data-stu-id="19425-167">For test environments on Azure, add the highlighted mark up to the bottom of the *web.config* file to enable Glimpse:</span></span>

[!code-xml[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample3.xml?highlight=2-6)]

<span data-ttu-id="19425-168">透過這種變更，任何使用者都可以在遠端網站上看到您的資料。</span><span class="sxs-lookup"><span data-stu-id="19425-168">With this change alone, any user can see your Glimpse data on a remote site.</span></span> <span data-ttu-id="19425-169">請考慮將上述標記新增至發行設定檔，使它只會在您使用該發行設定檔（例如，您的 Azure 測試組態檔）時部署。為了限制流覽資料，我們會新增 `canViewGlimpseData` 角色，而且只允許此角色中的使用者查看資料的外觀。</span><span class="sxs-lookup"><span data-stu-id="19425-169">Consider adding the markup above to a publish profile so it's only deployed an applied when you use that publish profile (for example, your Azure test profile.) To restrict Glimpse data, we will add the `canViewGlimpseData` role and only allow users in this role to view Glimpse data.</span></span>

<span data-ttu-id="19425-170">移除*GlimpseSecurityPolicy.cs*檔案中的批註，並將[IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx)呼叫從 `Administrator` 變更為 `canViewGlimpseData` 角色：</span><span class="sxs-lookup"><span data-stu-id="19425-170">Remove the comments from the *GlimpseSecurityPolicy.cs* file and change the [IsInRole](https://msdn.microsoft.com/library/system.security.principal.iprincipal.isinrole(v=vs.110).aspx) call from `Administrator` to the `canViewGlimpseData` role:</span></span>

[!code-csharp[Main](profile-and-debug-your-aspnet-mvc-app-with-glimpse/samples/sample4.cs?highlight=6)]

> [!WARNING]
> <span data-ttu-id="19425-171">安全性-所提供的豐富資料可以公開應用程式的安全性。</span><span class="sxs-lookup"><span data-stu-id="19425-171">Security - The rich data provided by Glimpse could expose the security of your app.</span></span> <span data-ttu-id="19425-172">Microsoft 尚未執行「粗略」的安全性審核，以用於生產應用程式。</span><span class="sxs-lookup"><span data-stu-id="19425-172">Microsoft has not performed a security audit of Glimpse for use on productions apps.</span></span>

<span data-ttu-id="19425-173">如需新增角色的相關資訊，請參閱我的[部署具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 5 web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)教學課程。</span><span class="sxs-lookup"><span data-stu-id="19425-173">For information on adding roles, see my [Deploy a Secure ASP.NET MVC 5 web app with Membership, OAuth, and SQL Database to Azure](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/) tutorial.</span></span>

<a id="addRes"></a>
## <a name="additional-resources"></a><span data-ttu-id="19425-174">其他資源</span><span class="sxs-lookup"><span data-stu-id="19425-174">Additional Resources</span></span>

- [<span data-ttu-id="19425-175">將具有成員資格、OAuth 和 SQL Database 的 Secure ASP.NET MVC 5 應用程式部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="19425-175">Deploy a Secure ASP.NET MVC 5 app with Membership, OAuth, and SQL Database to Azure</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-mvc-app-membership-oauth-sql-database/)
- <span data-ttu-id="19425-176">[一覽設定]-設定索引標籤、執行時間原則、記錄[等的檔](http://getglimpse.com/Docs/Configuration)頁面。</span><span class="sxs-lookup"><span data-stu-id="19425-176">[Glimpse Configuration](http://getglimpse.com/Docs/Configuration) - Doc page on configuring tabs, runtime policy, logging and more.</span></span>
