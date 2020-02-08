---
uid: single-page-application/overview/templates/hottowel-template
title: 熱門紙巾範本 |Microsoft Docs
author: madskristensen
description: HotTowel 範本
ms.author: riande
ms.date: 02/09/2013
ms.assetid: 75af2e17-6ed3-4d24-8ea1-bc340027c318
msc.legacyurl: /single-page-application/overview/templates/hottowel-template
msc.type: authoredcontent
ms.openlocfilehash: eeab69e75546791978bb09d7823d95caf9dca1a0
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/07/2020
ms.locfileid: "77075056"
---
# <a name="hot-towel-template"></a><span data-ttu-id="cbe81-103">Hot Towel 範本</span><span class="sxs-lookup"><span data-stu-id="cbe81-103">Hot Towel template</span></span>

<span data-ttu-id="cbe81-104">依[Mads Kristensen](https://github.com/madskristensen)</span><span class="sxs-lookup"><span data-stu-id="cbe81-104">by [Mads Kristensen](https://github.com/madskristensen)</span></span>

> <span data-ttu-id="cbe81-105">「熱門紙巾」 MVC 範本是由 John Papa 所撰寫</span><span class="sxs-lookup"><span data-stu-id="cbe81-105">The Hot Towel MVC Template is written by John Papa</span></span>
> 
> <span data-ttu-id="cbe81-106">選擇要下載的版本：</span><span class="sxs-lookup"><span data-stu-id="cbe81-106">Choose which version to download:</span></span>
> 
> [<span data-ttu-id="cbe81-107">Visual Studio 2012 的熱門紙巾 MVC 範本</span><span class="sxs-lookup"><span data-stu-id="cbe81-107">Hot Towel MVC Template for Visual Studio 2012</span></span>](https://visualstudiogallery.msdn.microsoft.com/1f68fbe8-b4e9-4968-9fd3-ddc7cbc52dca)
> 
> [<span data-ttu-id="cbe81-108">Visual Studio 2013 的熱門紙巾 MVC 範本</span><span class="sxs-lookup"><span data-stu-id="cbe81-108">Hot Towel MVC Template for Visual Studio 2013</span></span>](https://visualstudiogallery.msdn.microsoft.com/1eb8780d-d522-4dcf-bf56-56f0eab305c2)
> 
> 
> <span data-ttu-id="cbe81-109">熱紙巾：因為您不想要移至 SPA，而不需要一個！</span><span class="sxs-lookup"><span data-stu-id="cbe81-109">Hot Towel: Because you don't want to go to the SPA without one!</span></span>

<span data-ttu-id="cbe81-110">想要建立 SPA，但無法決定要從何處開始？</span><span class="sxs-lookup"><span data-stu-id="cbe81-110">Want to build a SPA but can't decide where to start?</span></span> <span data-ttu-id="cbe81-111">使用最熱門的紙巾，而在幾秒內，您就會有 SPA 和您需要建立的所有工具！</span><span class="sxs-lookup"><span data-stu-id="cbe81-111">Use Hot Towel and in seconds you'll have a SPA and all the tools you need to build on it!</span></span>

<span data-ttu-id="cbe81-112">最棒的是使用 ASP.NET 建立單一頁面應用程式（SPA）的絕佳起點。</span><span class="sxs-lookup"><span data-stu-id="cbe81-112">Hot Towel creates a great starting point for building a Single Page Application (SPA) with ASP.NET.</span></span> <span data-ttu-id="cbe81-113">現成可用來為您的程式碼提供模組化結構、視圖導覽、資料系結、豐富的資料管理，以及簡單但簡潔的樣式。</span><span class="sxs-lookup"><span data-stu-id="cbe81-113">Out of the box you it provides a modular structure for your code, view navigation, data binding, rich data management and simple but elegant styling.</span></span> <span data-ttu-id="cbe81-114">「熱門的紙巾」提供您建立 SPA 所需的所有專案，因此您可以專注于應用程式，而不是「配管」。</span><span class="sxs-lookup"><span data-stu-id="cbe81-114">Hot Towel provides everything you need to build a SPA, so you can focus on your app, not the plumbing.</span></span>

> <span data-ttu-id="cbe81-115">深入瞭解如何從[John Papa 的影片、教學課程和 Pluralsight 課程](http://johnpapa.net/spa?vsix)建立 SPA。</span><span class="sxs-lookup"><span data-stu-id="cbe81-115">Learn more about building a SPA from [John Papa's videos, tutorials and Pluralsight courses](http://johnpapa.net/spa?vsix).</span></span>

## <a name="application-structure"></a><span data-ttu-id="cbe81-116">應用程式結構</span><span class="sxs-lookup"><span data-stu-id="cbe81-116">Application Structure</span></span>

<span data-ttu-id="cbe81-117">「熱門的紙巾 SPA」提供應用程式資料夾，其中包含定義應用程式的 JavaScript 和 HTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="cbe81-117">Hot Towel SPA provides an App folder which contains the JavaScript and HTML files that define your application.</span></span>

<span data-ttu-id="cbe81-118">在應用程式資料夾內：</span><span class="sxs-lookup"><span data-stu-id="cbe81-118">Inside the App folder:</span></span>

- <span data-ttu-id="cbe81-119">durandal 等架構</span><span class="sxs-lookup"><span data-stu-id="cbe81-119">durandal</span></span>
- <span data-ttu-id="cbe81-120">服務</span><span class="sxs-lookup"><span data-stu-id="cbe81-120">services</span></span>
- <span data-ttu-id="cbe81-121">viewmodel</span><span class="sxs-lookup"><span data-stu-id="cbe81-121">viewmodels</span></span>
- <span data-ttu-id="cbe81-122">檢視</span><span class="sxs-lookup"><span data-stu-id="cbe81-122">views</span></span>

<span data-ttu-id="cbe81-123">應用程式資料夾包含模組的集合。</span><span class="sxs-lookup"><span data-stu-id="cbe81-123">The App folder contains a collection of modules.</span></span> <span data-ttu-id="cbe81-124">這些模組會封裝功能，並宣告其他模組的相依性。</span><span class="sxs-lookup"><span data-stu-id="cbe81-124">These modules encapsulate functionality and declare dependencies on other modules.</span></span> <span data-ttu-id="cbe81-125">Views 資料夾包含您應用程式的 HTML，而 viewmodel 資料夾包含 views 的呈現邏輯（通用 MVVM 模式）。</span><span class="sxs-lookup"><span data-stu-id="cbe81-125">The views folder contains the HTML for your application and the viewmodels folder contains the presentation logic for the views (a common MVVM pattern).</span></span> <span data-ttu-id="cbe81-126">[服務] 資料夾非常適合用來存放應用程式可能需要的任何一般服務，例如 HTTP 資料抓取或本機儲存體互動。</span><span class="sxs-lookup"><span data-stu-id="cbe81-126">The services folder is ideal for housing any common services that your application may need such as HTTP data retrieval or local storage interaction.</span></span> <span data-ttu-id="cbe81-127">多個 viewmodel 通常會從服務模組重複使用程式碼。</span><span class="sxs-lookup"><span data-stu-id="cbe81-127">It is common for multiple viewmodels to re-use code from the service modules.</span></span>

## <a name="aspnet-mvc-server-side-application-structure"></a><span data-ttu-id="cbe81-128">ASP.NET MVC 伺服器端應用程式結構</span><span class="sxs-lookup"><span data-stu-id="cbe81-128">ASP.NET MVC Server Side Application Structure</span></span>

<span data-ttu-id="cbe81-129">熱門的紙巾建基於熟悉且功能強大的 ASP.NET MVC 結構。</span><span class="sxs-lookup"><span data-stu-id="cbe81-129">Hot Towel builds on the familiar and powerful ASP.NET MVC structure.</span></span>

- <span data-ttu-id="cbe81-130">應用程式\_啟動</span><span class="sxs-lookup"><span data-stu-id="cbe81-130">App\_Start</span></span>
- <span data-ttu-id="cbe81-131">內容</span><span class="sxs-lookup"><span data-stu-id="cbe81-131">Content</span></span>
- <span data-ttu-id="cbe81-132">Controllers</span><span class="sxs-lookup"><span data-stu-id="cbe81-132">Controllers</span></span>
- <span data-ttu-id="cbe81-133">模型</span><span class="sxs-lookup"><span data-stu-id="cbe81-133">Models</span></span>
- <span data-ttu-id="cbe81-134">指令碼</span><span class="sxs-lookup"><span data-stu-id="cbe81-134">Scripts</span></span>
- <span data-ttu-id="cbe81-135">檢視</span><span class="sxs-lookup"><span data-stu-id="cbe81-135">Views</span></span>

## <a name="featured-libraries"></a><span data-ttu-id="cbe81-136">精選程式庫</span><span class="sxs-lookup"><span data-stu-id="cbe81-136">Featured Libraries</span></span>

- <span data-ttu-id="cbe81-137">ASP.NET MVC</span><span class="sxs-lookup"><span data-stu-id="cbe81-137">ASP.NET MVC</span></span>
- <span data-ttu-id="cbe81-138">ASP.NET Web API</span><span class="sxs-lookup"><span data-stu-id="cbe81-138">ASP.NET Web API</span></span>
- <span data-ttu-id="cbe81-139">ASP.NET Web 優化-捆綁和縮制</span><span class="sxs-lookup"><span data-stu-id="cbe81-139">ASP.NET Web Optimization - bundling and minification</span></span>
- <span data-ttu-id="cbe81-140">[輕鬆的 .js](http://Breezejs.com) -豐富資料管理</span><span class="sxs-lookup"><span data-stu-id="cbe81-140">[Breeze.js](http://Breezejs.com) - rich data management</span></span>
- <span data-ttu-id="cbe81-141">[Durandal 等架構 .js](http://Durandaljs.com) -導覽和視圖撰寫</span><span class="sxs-lookup"><span data-stu-id="cbe81-141">[Durandal.js](http://Durandaljs.com) - navigation and View composition</span></span>
- <span data-ttu-id="cbe81-142">[挖式 .js](http://Knockoutjs.com) -資料系結</span><span class="sxs-lookup"><span data-stu-id="cbe81-142">[Knockout.js](http://Knockoutjs.com) - data bindings</span></span>
- <span data-ttu-id="cbe81-143">[需要 .js](http://requirejs.org) -具有 AMD 和優化的模組化</span><span class="sxs-lookup"><span data-stu-id="cbe81-143">[Require.js](http://requirejs.org) - Modularity with AMD and optimization</span></span>
- <span data-ttu-id="cbe81-144">[Toastr](http://jpapa.me/c7toastr) -快顯視窗訊息</span><span class="sxs-lookup"><span data-stu-id="cbe81-144">[Toastr.js](http://jpapa.me/c7toastr) - pop-up messages</span></span>
- <span data-ttu-id="cbe81-145">[Twitter 啟動](https://twitter.github.com/bootstrap/)程式-健全的 CSS 樣式</span><span class="sxs-lookup"><span data-stu-id="cbe81-145">[Twitter Bootstrap](https://twitter.github.com/bootstrap/) - robust CSS styling</span></span>

## <a name="installing-via-the-visual-studio-2012-hot-towel-spa-template"></a><span data-ttu-id="cbe81-146">透過 Visual Studio 2012 的熱門紙巾 SPA 範本進行安裝</span><span class="sxs-lookup"><span data-stu-id="cbe81-146">Installing via the Visual Studio 2012 Hot Towel SPA Template</span></span>

<span data-ttu-id="cbe81-147">熱門的紙巾可以安裝為 Visual Studio 2012 範本。</span><span class="sxs-lookup"><span data-stu-id="cbe81-147">Hot Towel can be installed as a Visual Studio 2012 template.</span></span> <span data-ttu-id="cbe81-148">只要按一下 `File` | `New Project`，然後選擇 [`ASP.NET MVC 4 Web Application`]。</span><span class="sxs-lookup"><span data-stu-id="cbe81-148">Just click `File` | `New Project` and choose `ASP.NET MVC 4 Web Application`.</span></span> <span data-ttu-id="cbe81-149">然後選取 [熱門的紙巾單一頁面應用程式] 範本並執行！</span><span class="sxs-lookup"><span data-stu-id="cbe81-149">Then select the 'Hot Towel Single Page Application" template and run!</span></span>

## <a name="installing-via-the-nuget-package"></a><span data-ttu-id="cbe81-150">透過 NuGet 套件安裝</span><span class="sxs-lookup"><span data-stu-id="cbe81-150">Installing via the NuGet Package</span></span>

<span data-ttu-id="cbe81-151">熱門的紙巾也是可增強現有空白 ASP.NET MVC 專案的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="cbe81-151">Hot Towel is also a NuGet package that augments an existing empty ASP.NET MVC project.</span></span> <span data-ttu-id="cbe81-152">只要使用 Nuget 進行安裝，然後執行！</span><span class="sxs-lookup"><span data-stu-id="cbe81-152">Just install using Nuget and then run!</span></span>

[!code-powershell[Main](hottowel-template/samples/sample1.ps1)]

## <a name="how-do-i-build-on-hot-towel"></a><span data-ttu-id="cbe81-153">我該如何建立在熱門的紙巾上？</span><span class="sxs-lookup"><span data-stu-id="cbe81-153">How Do I Build On Hot Towel?</span></span>

<span data-ttu-id="cbe81-154">只要開始加入程式碼！</span><span class="sxs-lookup"><span data-stu-id="cbe81-154">Simply start adding code!</span></span>

1. <span data-ttu-id="cbe81-155">新增您自己的伺服器端程式碼，最好是 Entity Framework 和 WebAPI （這其實是使用簡單的 .js）</span><span class="sxs-lookup"><span data-stu-id="cbe81-155">Add your own server-side code, preferably Entity Framework and WebAPI (which really shine with Breeze.js)</span></span>
2. <span data-ttu-id="cbe81-156">將 views 新增至 `App/views` 資料夾</span><span class="sxs-lookup"><span data-stu-id="cbe81-156">Add views to the `App/views` folder</span></span>
3. <span data-ttu-id="cbe81-157">將 viewmodel 新增至 `App/viewmodels` 資料夾</span><span class="sxs-lookup"><span data-stu-id="cbe81-157">Add viewmodels to the `App/viewmodels` folder</span></span>
4. <span data-ttu-id="cbe81-158">將 HTML 和挖的資料系結新增至新的視圖</span><span class="sxs-lookup"><span data-stu-id="cbe81-158">Add HTML and Knockout data bindings to your new views</span></span>
5. <span data-ttu-id="cbe81-159">更新 `shell.js` 中的導覽路由</span><span class="sxs-lookup"><span data-stu-id="cbe81-159">Update the navigation routes in `shell.js`</span></span>

## <a name="walkthrough-of-the-htmljavascript"></a><span data-ttu-id="cbe81-160">HTML/JavaScript 的逐步解說</span><span class="sxs-lookup"><span data-stu-id="cbe81-160">Walkthrough of the HTML/JavaScript</span></span>

### <a name="viewshottowelindexcshtml"></a><span data-ttu-id="cbe81-161">Views/HotTowel/index. cshtml</span><span class="sxs-lookup"><span data-stu-id="cbe81-161">Views/HotTowel/index.cshtml</span></span>

<span data-ttu-id="cbe81-162">[index] 是 MVC 應用程式的起始路由和視圖。</span><span class="sxs-lookup"><span data-stu-id="cbe81-162">index.cshtml is the starting route and view for the MVC application.</span></span> <span data-ttu-id="cbe81-163">其中包含您預期的所有標準中繼標記、css 連結和 JavaScript 參考。</span><span class="sxs-lookup"><span data-stu-id="cbe81-163">It contains all the standard meta tags, css links, and JavaScript references you would expect.</span></span> <span data-ttu-id="cbe81-164">本文包含單一 `<div>`，這是要求所有內容（您的視圖）時將放置的位置。</span><span class="sxs-lookup"><span data-stu-id="cbe81-164">The body contains a single `<div>` which is where all of the content (your views) will be placed when they are requested.</span></span> <span data-ttu-id="cbe81-165">`@Scripts.Render` 使用需要 .js 來執行應用程式程式碼的進入點，其包含在 `main.js` 檔案中。</span><span class="sxs-lookup"><span data-stu-id="cbe81-165">The `@Scripts.Render` uses Require.js to run the entrance point for the application's code, which is contained in the `main.js` file.</span></span> <span data-ttu-id="cbe81-166">系統會提供啟動顯示畫面，示範如何在應用程式載入時建立啟動顯示畫面。</span><span class="sxs-lookup"><span data-stu-id="cbe81-166">A splash screen is provided to demonstrate how to create a splash screen while your app loads.</span></span>

[!code-cshtml[Main](hottowel-template/samples/sample2.cshtml)]

### <a name="appmainjs"></a><span data-ttu-id="cbe81-167">App/main .js</span><span class="sxs-lookup"><span data-stu-id="cbe81-167">App/main.js</span></span>

<span data-ttu-id="cbe81-168">`main.js` 檔案包含的程式碼，會在您的應用程式載入時立即執行。</span><span class="sxs-lookup"><span data-stu-id="cbe81-168">The `main.js` file contains the code that will run as soon as your app is loaded.</span></span> <span data-ttu-id="cbe81-169">這是您要定義流覽路由的位置、設定啟動視圖，以及執行任何安裝/啟動程式，例如預備應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="cbe81-169">This is where you want to define your navigation routes, set your start up views, and perform any setup/bootstrapping such as priming your application's data.</span></span>

<span data-ttu-id="cbe81-170">`main.js` 檔案會定義數個 durandal 等架構的模組，以協助應用程式開始進行。</span><span class="sxs-lookup"><span data-stu-id="cbe81-170">The `main.js` file defines several of durandal's modules to help the application kick start.</span></span> <span data-ttu-id="cbe81-171">Define 語句有助於解析模組相依性，使其可供函式使用。</span><span class="sxs-lookup"><span data-stu-id="cbe81-171">The define statement helps resolve the modules dependencies so they are available for the function.</span></span> <span data-ttu-id="cbe81-172">首先會啟用偵錯工具訊息，這會將應用程式正在執行之事件的相關訊息傳送至主控台視窗。</span><span class="sxs-lookup"><span data-stu-id="cbe81-172">First the debugging messages are enabled, which send messages about what events the application is performing to the console window.</span></span> <span data-ttu-id="cbe81-173">應用程式. 啟動程式碼會指示 durandal 等架構架構啟動應用程式。</span><span class="sxs-lookup"><span data-stu-id="cbe81-173">The app.start code tells durandal framework to start the application.</span></span> <span data-ttu-id="cbe81-174">系統會設定慣例，讓 durandal 等架構知道所有 views 和 viewmodel 分別包含在相同的命名資料夾中。</span><span class="sxs-lookup"><span data-stu-id="cbe81-174">The conventions are set so that durandal knows all views and viewmodels are contained in the same named folders, respectively.</span></span> <span data-ttu-id="cbe81-175">最後，`app.setRoot` 啟動會使用預先定義的 `entrance` 動畫來載入 `shell`。</span><span class="sxs-lookup"><span data-stu-id="cbe81-175">Finally, the `app.setRoot` kicks loads the `shell` using a predefined `entrance` animation.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample3.js)]

## <a name="views"></a><span data-ttu-id="cbe81-176">檢視</span><span class="sxs-lookup"><span data-stu-id="cbe81-176">Views</span></span>

<span data-ttu-id="cbe81-177">Views 可以在 `App/views` 資料夾中找到。</span><span class="sxs-lookup"><span data-stu-id="cbe81-177">Views are found in the `App/views` folder.</span></span>

### <a name="shellhtml"></a><span data-ttu-id="cbe81-178">shell .html</span><span class="sxs-lookup"><span data-stu-id="cbe81-178">shell.html</span></span>

<span data-ttu-id="cbe81-179">`shell.html` 包含您的 HTML 的主要版面配置。</span><span class="sxs-lookup"><span data-stu-id="cbe81-179">The `shell.html` contains the master layout for your HTML.</span></span> <span data-ttu-id="cbe81-180">所有其他的視圖都會在 `shell` 視圖的某處組成。</span><span class="sxs-lookup"><span data-stu-id="cbe81-180">All of your other views will be composed somewhere in side of your `shell` view.</span></span> <span data-ttu-id="cbe81-181">「經常性存取」提供具有三種這類區域的 `shell`：標題、內容區域和頁尾。</span><span class="sxs-lookup"><span data-stu-id="cbe81-181">Hot Towel provides a `shell` with three such regions: a header, a content area, and a footer.</span></span> <span data-ttu-id="cbe81-182">當要求時，每個區域都會以其他視圖的內容形式載入。</span><span class="sxs-lookup"><span data-stu-id="cbe81-182">Each of these regions is loaded with contents form other views when requested.</span></span>

<span data-ttu-id="cbe81-183">頁首和頁尾的 `compose` 系結在「熱紙巾」中硬式編碼，分別指向 [`nav`] 和 [`footer`] views。</span><span class="sxs-lookup"><span data-stu-id="cbe81-183">The `compose` bindings for the header and footer are hard coded in Hot Towel to point to the `nav` and `footer` views, respectively.</span></span> <span data-ttu-id="cbe81-184">區段 `#content` 的撰寫系結系結至 `router` 模組的現用專案。</span><span class="sxs-lookup"><span data-stu-id="cbe81-184">The compose binding for the section `#content` is bound to the `router` module's active item.</span></span> <span data-ttu-id="cbe81-185">換句話說，當您按一下導覽連結時，它會在此區域中載入對應的 view。</span><span class="sxs-lookup"><span data-stu-id="cbe81-185">In other words, when you click a navigation link it's corresponding view is loaded in this area.</span></span>

[!code-html[Main](hottowel-template/samples/sample4.html)]

### <a name="navhtml"></a><span data-ttu-id="cbe81-186">nav .html</span><span class="sxs-lookup"><span data-stu-id="cbe81-186">nav.html</span></span>

<span data-ttu-id="cbe81-187">`nav.html` 包含 SPA 的流覽連結。</span><span class="sxs-lookup"><span data-stu-id="cbe81-187">The `nav.html` contains the navigation links for the SPA.</span></span> <span data-ttu-id="cbe81-188">例如，您可以在這裡放置功能表結構。</span><span class="sxs-lookup"><span data-stu-id="cbe81-188">This is where the menu structure can be placed, for example.</span></span> <span data-ttu-id="cbe81-189">這通常是資料系結（使用挖式）至 `router` 模組，以顯示您在 `shell.js`中定義的導覽。</span><span class="sxs-lookup"><span data-stu-id="cbe81-189">Often this is data bound (using Knockout) to the `router` module to display the navigation you defined in the `shell.js`.</span></span> <span data-ttu-id="cbe81-190">挖起來會尋找資料系結屬性，並將其系結至 `shell` viewmodel 以顯示導覽路線，並在 `router` 模組正從一個視圖流覽至另一個時顯示 progressbar （使用 Twitter 啟動程式）（請參閱 `router.isNavigating`）。</span><span class="sxs-lookup"><span data-stu-id="cbe81-190">Knockout looks for the data-bind attributes and binds those to the `shell` viewmodel to display the navigation routes and to show a progressbar (using Twitter Bootstrap) if the `router` module is in the middle of navigating from one view to another (see `router.isNavigating`).</span></span>

[!code-html[Main](hottowel-template/samples/sample5.html)]

### <a name="homehtml-and-detailshtml"></a><span data-ttu-id="cbe81-191">首頁 .html 和詳細資料 .html</span><span class="sxs-lookup"><span data-stu-id="cbe81-191">home.html and details.html</span></span>

<span data-ttu-id="cbe81-192">這些 views 包含自訂視圖的 HTML。</span><span class="sxs-lookup"><span data-stu-id="cbe81-192">These views contain HTML for custom views.</span></span> <span data-ttu-id="cbe81-193">按一下 [`nav`] 視圖功能表中的 [`home`] 連結時，`home` 視圖會放在 [`shell`] 視圖的 [內容] 區域中。</span><span class="sxs-lookup"><span data-stu-id="cbe81-193">When the `home` link in the `nav` view's menu is clicked, the `home` view will be placed in the content area of the `shell` view.</span></span> <span data-ttu-id="cbe81-194">您可以使用自己的自訂視圖來增強或取代這些視圖。</span><span class="sxs-lookup"><span data-stu-id="cbe81-194">These views can be augmented or replaced with your own custom views.</span></span>

### <a name="footerhtml"></a><span data-ttu-id="cbe81-195">頁尾 .html</span><span class="sxs-lookup"><span data-stu-id="cbe81-195">footer.html</span></span>

<span data-ttu-id="cbe81-196">`footer.html` 包含出現在頁尾中的 HTML，位於 [`shell`] 視圖的底部。</span><span class="sxs-lookup"><span data-stu-id="cbe81-196">The `footer.html` contains HTML that appears in the footer, at the bottom of the `shell` view.</span></span>

## <a name="viewmodels"></a><span data-ttu-id="cbe81-197">ViewModels</span><span class="sxs-lookup"><span data-stu-id="cbe81-197">ViewModels</span></span>

<span data-ttu-id="cbe81-198">Viewmodel 可在 `App/viewmodels` 資料夾中找到。</span><span class="sxs-lookup"><span data-stu-id="cbe81-198">ViewModels are found in the `App/viewmodels` folder.</span></span>

### <a name="shelljs"></a><span data-ttu-id="cbe81-199">shell .js</span><span class="sxs-lookup"><span data-stu-id="cbe81-199">shell.js</span></span>

<span data-ttu-id="cbe81-200">`shell` viewmodel 包含系結至 `shell` 視圖的屬性和函式。</span><span class="sxs-lookup"><span data-stu-id="cbe81-200">The `shell` viewmodel contains properties and functions that are bound to the `shell` view.</span></span> <span data-ttu-id="cbe81-201">通常這是找到功能表導覽系結的位置（請參閱 `router.mapNav` 邏輯）。</span><span class="sxs-lookup"><span data-stu-id="cbe81-201">Often this is where the menu navigation bindings are found (see the `router.mapNav` logic).</span></span>

[!code-javascript[Main](hottowel-template/samples/sample6.js)]

### <a name="homejs-and-detailsjs"></a><span data-ttu-id="cbe81-202">首頁和詳細資訊 .js</span><span class="sxs-lookup"><span data-stu-id="cbe81-202">home.js and details.js</span></span>

<span data-ttu-id="cbe81-203">這些 viewmodel 包含系結至 `home` 視圖的屬性和函數。</span><span class="sxs-lookup"><span data-stu-id="cbe81-203">These viewmodels contain the properties and functions that are bound to the `home` view.</span></span> <span data-ttu-id="cbe81-204">它也包含視圖的呈現邏輯，而是資料和視圖之間的粘連。</span><span class="sxs-lookup"><span data-stu-id="cbe81-204">it also contains the presentation logic for the view, and is the glue between the data and the view.</span></span>

[!code-javascript[Main](hottowel-template/samples/sample7.js)]

## <a name="services"></a><span data-ttu-id="cbe81-205">服務</span><span class="sxs-lookup"><span data-stu-id="cbe81-205">Services</span></span>

<span data-ttu-id="cbe81-206">服務可在 [應用程式/服務] 資料夾中找到。</span><span class="sxs-lookup"><span data-stu-id="cbe81-206">Services are found in the App/services folder.</span></span> <span data-ttu-id="cbe81-207">最理想的情況是，您未來的服務（例如 dataservice 模組），負責取得和張貼遠端資料。</span><span class="sxs-lookup"><span data-stu-id="cbe81-207">Ideally your future services such as a dataservice module, that is responsible for getting and posting remote data, could be placed.</span></span>

### <a name="loggerjs"></a><span data-ttu-id="cbe81-208">記錄器 .js</span><span class="sxs-lookup"><span data-stu-id="cbe81-208">logger.js</span></span>

<span data-ttu-id="cbe81-209">熱紙巾會在 [服務] 資料夾中提供 `logger` 模組。</span><span class="sxs-lookup"><span data-stu-id="cbe81-209">Hot Towel provides a `logger` module in the services folder.</span></span> <span data-ttu-id="cbe81-210">`logger` 模組適合用來將訊息記錄到主控台和快顯快顯通知中的使用者。</span><span class="sxs-lookup"><span data-stu-id="cbe81-210">The `logger` module is ideal for logging messages to the console and to the user in pop up toasts.</span></span>
