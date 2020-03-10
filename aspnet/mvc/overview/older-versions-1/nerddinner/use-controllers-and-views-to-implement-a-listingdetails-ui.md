---
uid: mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
title: 使用控制器和 Views 來執行清單/詳細資料 UI |Microsoft Docs
author: microsoft
description: 步驟4顯示如何將控制器新增至應用程式，利用我們的模型為使用者提供資料清單/詳細導覽體驗 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 64116e56-1c9a-4f07-8097-bb36cbb6e57f
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/use-controllers-and-views-to-implement-a-listingdetails-ui
msc.type: authoredcontent
ms.openlocfilehash: 74319fe5ea4c79b50140834349e2fdf86420cfbb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78600741"
---
# <a name="use-controllers-and-views-to-implement-a-listingdetails-ui"></a><span data-ttu-id="d1eca-103">使用控制器和檢視來實作清單/詳細資料 UI</span><span class="sxs-lookup"><span data-stu-id="d1eca-103">Use Controllers and Views to Implement a Listing/Details UI</span></span>

<span data-ttu-id="d1eca-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="d1eca-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="d1eca-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="d1eca-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="d1eca-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟4，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="d1eca-106">This is step 4 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="d1eca-107">步驟4顯示如何將控制器新增至應用程式，以利用我們的模型在我們的 NerdDinner 網站上為使用者提供 dinners 的資料列/詳細導覽體驗。</span><span class="sxs-lookup"><span data-stu-id="d1eca-107">Step 4 shows how to add a Controller to the application that takes advantage of our model to provide users with a data listing/details navigation experience for dinners on our NerdDinner site.</span></span>
> 
> <span data-ttu-id="d1eca-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="d1eca-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-4-controllers-and-views"></a><span data-ttu-id="d1eca-109">NerdDinner 步驟4：控制器和 Views</span><span class="sxs-lookup"><span data-stu-id="d1eca-109">NerdDinner Step 4: Controllers and Views</span></span>

<span data-ttu-id="d1eca-110">使用傳統的 web 架構（傳統 ASP、PHP、ASP.NET Web form 等等）時，連入 Url 通常會對應到磁片上的檔案。</span><span class="sxs-lookup"><span data-stu-id="d1eca-110">With traditional web frameworks (classic ASP, PHP, ASP.NET Web Forms, etc), incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="d1eca-111">例如： "/Products.aspx" 或 "/Products.php" 等 URL 的要求可能會由 "Products" 或 "Products. php" 檔案處理。</span><span class="sxs-lookup"><span data-stu-id="d1eca-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="d1eca-112">以 Web 為基礎的 MVC 架構會以稍有不同的方式將 Url 對應至伺服器程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1eca-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="d1eca-113">與其將傳入 Url 對應至檔案，它們會改為將 Url 對應至類別上的方法。</span><span class="sxs-lookup"><span data-stu-id="d1eca-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="d1eca-114">這些類別稱為「控制器」，負責處理傳入 HTTP 要求、處理使用者輸入、抓取和儲存資料，以及判斷要傳回給用戶端的回應（顯示 HTML、下載檔案、重新導向至不同的URL 等）。</span><span class="sxs-lookup"><span data-stu-id="d1eca-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc).</span></span>

<span data-ttu-id="d1eca-115">既然我們已為 NerdDinner 應用程式建立基本模型，下一步就是將控制器新增至應用程式，利用它來為使用者提供 Dinners 在我們網站上的資料列/詳細導覽體驗。</span><span class="sxs-lookup"><span data-stu-id="d1eca-115">Now that we have built up a basic model for our NerdDinner application, our next step will be to add a Controller to the application that takes advantage of it to provide users with a data listing/details navigation experience for Dinners on our site.</span></span>

### <a name="adding-a-dinnerscontroller-controller"></a><span data-ttu-id="d1eca-116">新增 DinnersController 控制器</span><span class="sxs-lookup"><span data-stu-id="d1eca-116">Adding a DinnersController Controller</span></span>

<span data-ttu-id="d1eca-117">首先，以滑鼠右鍵按一下 Web 專案中的 [控制器] 資料夾，然後選取 [**新增&gt;控制器**] 功能表命令（您也可以輸入 Ctrl-M、ctrl-c 來執行此命令）：</span><span class="sxs-lookup"><span data-stu-id="d1eca-117">We'll begin by right-clicking on the "Controllers" folder within our web project, and then select the **Add-&gt;Controller** menu command (you can also execute this command by typing Ctrl-M, Ctrl-C):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image1.png)

<span data-ttu-id="d1eca-118">這會顯示 [新增控制器] 對話方塊：</span><span class="sxs-lookup"><span data-stu-id="d1eca-118">This will bring up the "Add Controller" dialog:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image2.png)

<span data-ttu-id="d1eca-119">我們會將新的控制器命名為 "DinnersController"，然後按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d1eca-119">We'll name the new controller "DinnersController" and click the "Add" button.</span></span> <span data-ttu-id="d1eca-120">Visual Studio 接著會在 \Controllers 目錄下新增 DinnersController.cs 檔案：</span><span class="sxs-lookup"><span data-stu-id="d1eca-120">Visual Studio will then add a DinnersController.cs file under our \Controllers directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image3.png)

<span data-ttu-id="d1eca-121">它也會在程式碼編輯器中開啟新的 DinnersController 類別。</span><span class="sxs-lookup"><span data-stu-id="d1eca-121">It will also open up the new DinnersController class within the code-editor.</span></span>

### <a name="adding-index-and-details-action-methods-to-the-dinnerscontroller-class"></a><span data-ttu-id="d1eca-122">將 Index （）和 Details （）動作方法加入至 DinnersController 類別</span><span class="sxs-lookup"><span data-stu-id="d1eca-122">Adding Index() and Details() Action Methods to the DinnersController Class</span></span>

<span data-ttu-id="d1eca-123">我們想要讓訪客使用我們的應用程式流覽即將推出的 dinners 清單，並允許他們按一下清單中的任何晚餐，以查看其相關特定的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d1eca-123">We want to enable visitors using our application to browse a list of upcoming dinners, and allow them to click on any Dinner in the list to see specific details about it.</span></span> <span data-ttu-id="d1eca-124">我們將從我們的應用程式發佈下列 Url 來完成這項操作：</span><span class="sxs-lookup"><span data-stu-id="d1eca-124">We'll do this by publishing the following URLs from our application:</span></span>

| <span data-ttu-id="d1eca-125">**URL**</span><span class="sxs-lookup"><span data-stu-id="d1eca-125">**URL**</span></span> | <span data-ttu-id="d1eca-126">**目的**</span><span class="sxs-lookup"><span data-stu-id="d1eca-126">**Purpose**</span></span> |
| --- | --- |
| <span data-ttu-id="d1eca-127">*/Dinners/*</span><span class="sxs-lookup"><span data-stu-id="d1eca-127">*/Dinners/*</span></span> | <span data-ttu-id="d1eca-128">顯示即將推出的 dinners HTML 清單</span><span class="sxs-lookup"><span data-stu-id="d1eca-128">Display an HTML list of upcoming dinners</span></span> |
| <span data-ttu-id="d1eca-129">*/Dinners/Details/[識別碼]*</span><span class="sxs-lookup"><span data-stu-id="d1eca-129">*/Dinners/Details/[id]*</span></span> | <span data-ttu-id="d1eca-130">顯示在 URL 中內嵌的「識別碼」參數所指示之特定晚餐的詳細資料–這會符合資料庫中晚餐的 DinnerID。</span><span class="sxs-lookup"><span data-stu-id="d1eca-130">Display details about a specific dinner indicated by an "id" parameter embedded within the URL – which will match the DinnerID of the dinner in the database.</span></span> <span data-ttu-id="d1eca-131">例如：/Dinners/Details/2 會顯示 HTML 頁面，其中包含其 DinnerID 值為2之晚餐的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d1eca-131">For example: /Dinners/Details/2 would display an HTML page with details about the Dinner whose DinnerID value is 2.</span></span> |

<span data-ttu-id="d1eca-132">我們會將兩個公用的「動作方法」新增至我們的 DinnersController 類別，以發佈這些 Url 的初始執行，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1eca-132">We will publish initial implementations of these URLs by adding two public "action methods" to our DinnersController class like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample1.cs)]

<span data-ttu-id="d1eca-133">接著，我們會執行 NerdDinner 應用程式，並使用我們的瀏覽器來叫用它們。</span><span class="sxs-lookup"><span data-stu-id="d1eca-133">We'll then run the NerdDinner application and use our browser to invoke them.</span></span> <span data-ttu-id="d1eca-134">在 *"/Dinners/"* URL 中輸入會導致我們的*Index （）* 方法執行，並傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="d1eca-134">Typing in the *"/Dinners/"* URL will cause our *Index()* method to run, and it will send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image4.png)

<span data-ttu-id="d1eca-135">輸入 *"/Dinners/Details/2"* URL 會導致我們的*Details （）* 方法執行，並傳回下列回應：</span><span class="sxs-lookup"><span data-stu-id="d1eca-135">Typing in the *"/Dinners/Details/2"* URL will cause our *Details()* method to run, and send back the following response:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image5.png)

<span data-ttu-id="d1eca-136">您可能會想： ASP.NET MVC 如何知道如何建立 DinnersController 類別並叫用這些方法？</span><span class="sxs-lookup"><span data-stu-id="d1eca-136">You might be wondering - how did ASP.NET MVC know to create our DinnersController class and invoke those methods?</span></span> <span data-ttu-id="d1eca-137">若要瞭解這一點，讓我們快速查看路由的運作方式。</span><span class="sxs-lookup"><span data-stu-id="d1eca-137">To understand that let's take a quick look at how routing works.</span></span>

### <a name="understanding-aspnet-mvc-routing"></a><span data-ttu-id="d1eca-138">瞭解 ASP.NET MVC 路由</span><span class="sxs-lookup"><span data-stu-id="d1eca-138">Understanding ASP.NET MVC Routing</span></span>

<span data-ttu-id="d1eca-139">ASP.NET MVC 包含強大的 URL 路由引擎，可提供很大的彈性來控制 Url 對應至控制器類別的方式。</span><span class="sxs-lookup"><span data-stu-id="d1eca-139">ASP.NET MVC includes a powerful URL routing engine that provides a lot of flexibility in controlling how URLs are mapped to controller classes.</span></span> <span data-ttu-id="d1eca-140">它可讓我們完全自訂 ASP.NET MVC 如何選擇要建立的控制器類別、要在其上叫用的方法，以及設定變數可以從 URL/Querystring 自動剖析並當做參數引數傳遞至方法的不同方式。</span><span class="sxs-lookup"><span data-stu-id="d1eca-140">It allows us to completely customize how ASP.NET MVC chooses which controller class to create, which method to invoke on it, as well as configure different ways that variables can be automatically parsed from the URL/Querystring and passed to the method as parameter arguments.</span></span> <span data-ttu-id="d1eca-141">它提供彈性來完全優化 SEO 的網站（搜尋引擎優化），並從應用程式發佈所需的任何 URL 結構。</span><span class="sxs-lookup"><span data-stu-id="d1eca-141">It delivers the flexibility to totally optimize a site for SEO (search engine optimization) as well as publish any URL structure we want from an application.</span></span>

<span data-ttu-id="d1eca-142">根據預設，新的 ASP.NET MVC 專案會隨附一組預先設定的 URL 路由規則已註冊。</span><span class="sxs-lookup"><span data-stu-id="d1eca-142">By default, new ASP.NET MVC projects come with a preconfigured set of URL routing rules already registered.</span></span> <span data-ttu-id="d1eca-143">這可讓我們輕鬆地開始使用應用程式，而不需要明確地設定任何專案。</span><span class="sxs-lookup"><span data-stu-id="d1eca-143">This enables us to easily get started on an application without having to explicitly configure anything.</span></span> <span data-ttu-id="d1eca-144">您可以在專案的 [應用程式] 類別中找到預設的路由規則註冊，我們可以按兩下專案根目錄中的 "global.asax" 檔案來開啟它：</span><span class="sxs-lookup"><span data-stu-id="d1eca-144">The default routing rule registrations can be found within the "Application" class of our projects – which we can open by double-clicking the "Global.asax" file in the root of our project:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image6.png)

<span data-ttu-id="d1eca-145">預設 ASP.NET MVC 路由規則會在此類別的 "RegisterRoutes" 方法中註冊：</span><span class="sxs-lookup"><span data-stu-id="d1eca-145">The default ASP.NET MVC routing rules are registered within the "RegisterRoutes" method of this class:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample2.cs)]

<span data-ttu-id="d1eca-146">「路由」。上述的 Maproute.html （） "方法呼叫會註冊預設路由規則，其會使用 URL 格式將傳入 Url 對應至控制器類別："/{controller}/{action}/{id} "–其中" controller "是要具現化的控制器類別名稱，" action "是要在其上叫用之公用方法的名稱，而" id "是內嵌在 URL 內的選擇性參數，可當做引數傳遞給方法。</span><span class="sxs-lookup"><span data-stu-id="d1eca-146">The "routes.MapRoute()" method call above registers a default routing rule that maps incoming URLs to controller classes using the URL format: "/{controller}/{action}/{id}" – where "controller" is the name of the controller class to instantiate, "action" is the name of a public method to invoke on it, and "id" is an optional parameter embedded within the URL that can be passed as an argument to the method.</span></span> <span data-ttu-id="d1eca-147">傳遞至 "Maproute.html （）" 方法呼叫的第三個參數是一組預設值，如果它們不存在於 URL 中（控制器 = "Home"，Action = "Index"，Id = ""），就會在控制器/動作/識別碼的值中使用。</span><span class="sxs-lookup"><span data-stu-id="d1eca-147">The third parameter passed to the "MapRoute()" method call is a set of default values to use for the controller/action/id values in the event that they are not present in the URL (Controller = "Home", Action="Index", Id="").</span></span>

<span data-ttu-id="d1eca-148">以下表格示範如何使用預設的 "<em>/{controllers}/{action}/{id}"</em>路由規則來對應各種 url：</span><span class="sxs-lookup"><span data-stu-id="d1eca-148">Below is a table that demonstrates how a variety of URLs are mapped using the default "<em>/{controllers}/{action}/{id}"</em>route rule:</span></span>

| <span data-ttu-id="d1eca-149">**URL**</span><span class="sxs-lookup"><span data-stu-id="d1eca-149">**URL**</span></span> | <span data-ttu-id="d1eca-150">**控制器類別**</span><span class="sxs-lookup"><span data-stu-id="d1eca-150">**Controller Class**</span></span> | <span data-ttu-id="d1eca-151">**動作方法**</span><span class="sxs-lookup"><span data-stu-id="d1eca-151">**Action Method**</span></span> | <span data-ttu-id="d1eca-152">**傳遞的參數**</span><span class="sxs-lookup"><span data-stu-id="d1eca-152">**Parameters Passed**</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="d1eca-153">*/Dinners/Details/2*</span><span class="sxs-lookup"><span data-stu-id="d1eca-153">*/Dinners/Details/2*</span></span> | <span data-ttu-id="d1eca-154">DinnersController</span><span class="sxs-lookup"><span data-stu-id="d1eca-154">DinnersController</span></span> | <span data-ttu-id="d1eca-155">詳細資料（識別碼）</span><span class="sxs-lookup"><span data-stu-id="d1eca-155">Details(id)</span></span> | <span data-ttu-id="d1eca-156">識別碼 = 2</span><span class="sxs-lookup"><span data-stu-id="d1eca-156">id=2</span></span> |
| <span data-ttu-id="d1eca-157">*/Dinners/Edit/5*</span><span class="sxs-lookup"><span data-stu-id="d1eca-157">*/Dinners/Edit/5*</span></span> | <span data-ttu-id="d1eca-158">DinnersController</span><span class="sxs-lookup"><span data-stu-id="d1eca-158">DinnersController</span></span> | <span data-ttu-id="d1eca-159">編輯（id）</span><span class="sxs-lookup"><span data-stu-id="d1eca-159">Edit(id)</span></span> | <span data-ttu-id="d1eca-160">識別碼 = 5</span><span class="sxs-lookup"><span data-stu-id="d1eca-160">id=5</span></span> |
| <span data-ttu-id="d1eca-161">*/Dinners/Create*</span><span class="sxs-lookup"><span data-stu-id="d1eca-161">*/Dinners/Create*</span></span> | <span data-ttu-id="d1eca-162">DinnersController</span><span class="sxs-lookup"><span data-stu-id="d1eca-162">DinnersController</span></span> | <span data-ttu-id="d1eca-163">Create()</span><span class="sxs-lookup"><span data-stu-id="d1eca-163">Create()</span></span> | <span data-ttu-id="d1eca-164">N/A</span><span class="sxs-lookup"><span data-stu-id="d1eca-164">N/A</span></span> |
| <span data-ttu-id="d1eca-165">*/Dinners*</span><span class="sxs-lookup"><span data-stu-id="d1eca-165">*/Dinners*</span></span> | <span data-ttu-id="d1eca-166">DinnersController</span><span class="sxs-lookup"><span data-stu-id="d1eca-166">DinnersController</span></span> | <span data-ttu-id="d1eca-167">Index （）</span><span class="sxs-lookup"><span data-stu-id="d1eca-167">Index()</span></span> | <span data-ttu-id="d1eca-168">N/A</span><span class="sxs-lookup"><span data-stu-id="d1eca-168">N/A</span></span> |
| <span data-ttu-id="d1eca-169">*/Home*</span><span class="sxs-lookup"><span data-stu-id="d1eca-169">*/Home*</span></span> | <span data-ttu-id="d1eca-170">HomeController</span><span class="sxs-lookup"><span data-stu-id="d1eca-170">HomeController</span></span> | <span data-ttu-id="d1eca-171">Index （）</span><span class="sxs-lookup"><span data-stu-id="d1eca-171">Index()</span></span> | <span data-ttu-id="d1eca-172">N/A</span><span class="sxs-lookup"><span data-stu-id="d1eca-172">N/A</span></span> |
| */* | <span data-ttu-id="d1eca-173">HomeController</span><span class="sxs-lookup"><span data-stu-id="d1eca-173">HomeController</span></span> | <span data-ttu-id="d1eca-174">Index （）</span><span class="sxs-lookup"><span data-stu-id="d1eca-174">Index()</span></span> | <span data-ttu-id="d1eca-175">N/A</span><span class="sxs-lookup"><span data-stu-id="d1eca-175">N/A</span></span> |

<span data-ttu-id="d1eca-176">最後三個數據列會顯示使用的預設值（控制器 = Home，Action = Index，Id = ""）。</span><span class="sxs-lookup"><span data-stu-id="d1eca-176">The last three rows show the default values (Controller = Home, Action = Index, Id = "") being used.</span></span> <span data-ttu-id="d1eca-177">因為 "Index" 方法已註冊為預設動作名稱（如果未指定），所以 "/Dinners" 和 "/Home" Url 會使 Index （）動作方法在其控制器類別上叫用。</span><span class="sxs-lookup"><span data-stu-id="d1eca-177">Because the "Index" method is registered as the default action name if one isn't specified, the "/Dinners" and "/Home" URLs cause the Index() action method to be invoked on their Controller classes.</span></span> <span data-ttu-id="d1eca-178">因為 "Home" 控制器已註冊為預設控制器（如果未指定），所以 "/" URL 會導致建立 HomeController，並在其上叫用 Index （）動作方法。</span><span class="sxs-lookup"><span data-stu-id="d1eca-178">Because the "Home" controller is registered as the default controller if one isn't specified, the "/" URL causes the HomeController to be created, and the Index() action method on it to be invoked.</span></span>

<span data-ttu-id="d1eca-179">如果您不喜歡這些預設的 URL 路由規則，好消息是可以輕鬆地進行變更，只要在上面的 RegisterRoutes 方法中編輯它們即可。</span><span class="sxs-lookup"><span data-stu-id="d1eca-179">If you don't like these default URL routing rules, the good news is that they are easy to change - just edit them within the RegisterRoutes method above.</span></span> <span data-ttu-id="d1eca-180">不過，針對我們的 NerdDinner 應用程式，我們不會變更任何預設的 URL 路由規則，而是改為直接使用它們。</span><span class="sxs-lookup"><span data-stu-id="d1eca-180">For our NerdDinner application, though, we aren't going to change any of the default URL routing rules – instead we'll just use them as-is.</span></span>

### <a name="using-the-dinnerrepository-from-our-dinnerscontroller"></a><span data-ttu-id="d1eca-181">從我們的 DinnersController 使用 DinnerRepository</span><span class="sxs-lookup"><span data-stu-id="d1eca-181">Using the DinnerRepository from our DinnersController</span></span>

<span data-ttu-id="d1eca-182">現在讓我們將 DinnersController 的 Index （）和 Details （）動作方法的目前執行，取代為使用我們模型的程式。</span><span class="sxs-lookup"><span data-stu-id="d1eca-182">Let's now replace our current implementation of the DinnersController's Index() and Details() action methods with implementations that use our model.</span></span>

<span data-ttu-id="d1eca-183">我們將使用稍早建立的 DinnerRepository 類別來執行此行為。</span><span class="sxs-lookup"><span data-stu-id="d1eca-183">We'll use the DinnerRepository class we built earlier to implement the behavior.</span></span> <span data-ttu-id="d1eca-184">首先，我們會新增一個參考 "NerdDinner" 命名空間的 "using" 語句，然後在 DinnerController 類別上宣告 DinnerRepository 的實例作為欄位。</span><span class="sxs-lookup"><span data-stu-id="d1eca-184">We'll begin by adding a "using" statement that references the "NerdDinner.Models" namespace, and then declare an instance of our DinnerRepository as a field on our DinnerController class.</span></span>

<span data-ttu-id="d1eca-185">我們將在本章稍後介紹「相依性插入」的概念，並顯示另一種方式，讓我們的控制器取得對 DinnerRepository 的參考，以進行更好的單元測試，但現在我們只會建立 DinnerRepository 的實例。內嵌，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d1eca-185">Later in this chapter we'll introduce the concept of "Dependency Injection" and show another way for our Controllers to obtain a reference to a DinnerRepository that enables better unit testing – but for right now we'll just create an instance of our DinnerRepository inline like below.</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample3.cs)]

<span data-ttu-id="d1eca-186">現在，我們已準備好使用我們抓取的資料模型物件來產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="d1eca-186">Now we are ready to generate a HTML response back using our retrieved data model objects.</span></span>

### <a name="using-views-with-our-controller"></a><span data-ttu-id="d1eca-187">搭配我們的控制器使用 Views</span><span class="sxs-lookup"><span data-stu-id="d1eca-187">Using Views with our Controller</span></span>

<span data-ttu-id="d1eca-188">雖然您可以在動作方法中撰寫程式碼來組合 HTML，然後使用*Response （）* helper 方法將它傳回給用戶端，但該方法會變得相當難以處理。</span><span class="sxs-lookup"><span data-stu-id="d1eca-188">While it is possible to write code within our action methods to assemble HTML and then use the *Response.Write()* helper method to send it back to the client, that approach becomes fairly unwieldy quickly.</span></span> <span data-ttu-id="d1eca-189">更好的方法是讓我們只在 DinnersController 動作方法內執行應用程式和資料邏輯，然後將呈現 HTML 回應所需的資料傳遞至個別的「view」範本，以負責輸出 HTML 標記法其中的。</span><span class="sxs-lookup"><span data-stu-id="d1eca-189">A much better approach is for us to only perform application and data logic inside our DinnersController action methods, and to then pass the data needed to render a HTML response to a separate "view" template that is responsible for outputting the HTML representation of it.</span></span> <span data-ttu-id="d1eca-190">如我們稍後所見，「view」範本是一個文字檔，通常包含 HTML 標籤和內嵌呈現程式碼的組合。</span><span class="sxs-lookup"><span data-stu-id="d1eca-190">As we'll see in a moment, a "view" template is a text file that typically contains a combination of HTML markup and embedded rendering code.</span></span>

<span data-ttu-id="d1eca-191">將我們的控制器邏輯與我們的視圖轉譯分開，可提供數個大優勢。</span><span class="sxs-lookup"><span data-stu-id="d1eca-191">Separating our controller logic from our view rendering brings several big benefits.</span></span> <span data-ttu-id="d1eca-192">特別是，這有助於在應用程式代碼和 UI 格式設定/轉譯程式碼之間，強制執行明確的「關注點分離」。</span><span class="sxs-lookup"><span data-stu-id="d1eca-192">In particular it helps enforce a clear "separation of concerns" between the application code and UI formatting/rendering code.</span></span> <span data-ttu-id="d1eca-193">這可讓您更輕鬆地對應用程式邏輯進行單元測試，而不受 UI 轉譯邏輯的隔離。</span><span class="sxs-lookup"><span data-stu-id="d1eca-193">This makes it much easier to unit-test application logic in isolation from UI rendering logic.</span></span> <span data-ttu-id="d1eca-194">這可讓您更輕鬆地修改 UI 轉譯範本，而不需要變更應用程式程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1eca-194">It makes it easier to later modify the UI rendering templates without having to make application code changes.</span></span> <span data-ttu-id="d1eca-195">而且它可以讓開發人員和設計人員更輕鬆地在專案上共同作業。</span><span class="sxs-lookup"><span data-stu-id="d1eca-195">And it can make it easier for developers and designers to collaborate together on projects.</span></span>

<span data-ttu-id="d1eca-196">我們可以更新 DinnersController 類別，以指出我們想要使用視圖範本來傳回 HTML UI 回應，方法是變更兩個動作方法的方法簽章，使其傳回型別為 "void"，而改用 "ActionResult" 的傳回型別。</span><span class="sxs-lookup"><span data-stu-id="d1eca-196">We can update our DinnersController class to indicate that we want to use a view template to send back an HTML UI response by changing the method signatures of our two action methods from having a return type of "void" to instead have a return type of "ActionResult".</span></span> <span data-ttu-id="d1eca-197">然後，我們可以在控制器基類上呼叫*View （）* helper 方法，傳回 "ViewResult" 物件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1eca-197">We can then call the *View()* helper method on the Controller base class to return back a "ViewResult" object like below:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample4.cs)]

<span data-ttu-id="d1eca-198">我們在上面使用的*View （）* helper 方法的簽章如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1eca-198">The signature of the *View()* helper method we are using above looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image7.png)

<span data-ttu-id="d1eca-199">*View （）* helper 方法的第一個參數是我們想要用來呈現 HTML 回應的視圖範本檔案名。</span><span class="sxs-lookup"><span data-stu-id="d1eca-199">The first parameter to the *View()* helper method is the name of the view template file we want to use to render the HTML response.</span></span> <span data-ttu-id="d1eca-200">第二個參數是模型物件，其中包含視圖範本所需的資料，以便呈現 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="d1eca-200">The second parameter is a model object that contains the data that the view template needs in order to render the HTML response.</span></span>

<span data-ttu-id="d1eca-201">在我們的 Index （）動作方法中，我們會呼叫*View （）* helper 方法，並指出我們想要使用「索引」視圖範本來呈現 DINNERS 的 HTML 清單。</span><span class="sxs-lookup"><span data-stu-id="d1eca-201">Within our Index() action method we are calling the *View()* helper method and indicating that we want to render an HTML listing of dinners using an "Index" view template.</span></span> <span data-ttu-id="d1eca-202">我們會傳遞一個晚餐物件序列給此視圖範本，以產生下列清單：</span><span class="sxs-lookup"><span data-stu-id="d1eca-202">We are passing the view template a sequence of Dinner objects to generate the list from:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample5.cs)]

<span data-ttu-id="d1eca-203">在我們的 Details （）動作方法中，我們嘗試使用 URL 中提供的識別碼來抓取晚餐物件。</span><span class="sxs-lookup"><span data-stu-id="d1eca-203">Within our Details() action method we attempt to retrieve a Dinner object using the id provided within the URL.</span></span> <span data-ttu-id="d1eca-204">如果找到有效的晚餐，我們會呼叫*View （）* 協助程式方法，表示我們想要使用「詳細資料」視圖範本來呈現抓取的晚餐物件。</span><span class="sxs-lookup"><span data-stu-id="d1eca-204">If a valid Dinner is found we call the *View()* helper method, indicating we want to use a "Details" view template to render the retrieved Dinner object.</span></span> <span data-ttu-id="d1eca-205">如果要求的晚餐無效，我們會轉譯一個有用的錯誤訊息，指出晚餐不是使用 "NotFound" view 範本（和只接受範本名稱的*view （）* helper 方法的多載版本）：</span><span class="sxs-lookup"><span data-stu-id="d1eca-205">If an invalid dinner is requested, we render a helpful error message that indicates that the Dinner doesn't exist using a "NotFound" view template (and an overloaded version of the *View()* helper method that just takes the template name):</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample6.cs)]

<span data-ttu-id="d1eca-206">現在讓我們來執行「NotFound」、「Details」和「Index」視圖範本。</span><span class="sxs-lookup"><span data-stu-id="d1eca-206">Let's now implement the "NotFound", "Details", and "Index" view templates.</span></span>

### <a name="implementing-the-notfound-view-template"></a><span data-ttu-id="d1eca-207">執行 "NotFound" View 範本</span><span class="sxs-lookup"><span data-stu-id="d1eca-207">Implementing the "NotFound" View Template</span></span>

<span data-ttu-id="d1eca-208">我們一開始會先執行「NotFound」視圖範本，這會顯示一個易記的錯誤訊息，指出找不到所要求的晚餐。</span><span class="sxs-lookup"><span data-stu-id="d1eca-208">We'll begin by implementing the "NotFound" view template – which displays a friendly error message indicating that the requested dinner can't be found.</span></span>

<span data-ttu-id="d1eca-209">我們會建立新的 view 範本，方法是將文字游標放在控制器動作方法中，然後以滑鼠右鍵按一下並選擇 [新增視圖] 功能表命令（我們也可以輸入 Ctrl-M、Ctrl-c 來執行此命令）：</span><span class="sxs-lookup"><span data-stu-id="d1eca-209">We'll create a new view template by positioning our text cursor within a controller action method, and then right click and choose the "Add View" menu command (we can also execute this command by typing Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image8.png)

<span data-ttu-id="d1eca-210">這會顯示 [新增視圖] 對話方塊，如下所示。</span><span class="sxs-lookup"><span data-stu-id="d1eca-210">This will bring up an "Add View" dialog like below.</span></span> <span data-ttu-id="d1eca-211">根據預設，對話方塊會預先填入要建立的視圖名稱，以符合在啟動對話時游標所在的動作方法名稱（在此案例中為「詳細資料」）。</span><span class="sxs-lookup"><span data-stu-id="d1eca-211">By default the dialog will pre-populate the name of the view to create to match the name of the action method the cursor was in when the dialog was launched (in this case "Details").</span></span> <span data-ttu-id="d1eca-212">因為我們想要先執行「NotFound」範本，所以我們將覆寫此視圖名稱，並將它設定為「NotFound」：</span><span class="sxs-lookup"><span data-stu-id="d1eca-212">Because we want to first implement the "NotFound" template, we'll override this view name and set it to instead be "NotFound":</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image9.png)

<span data-ttu-id="d1eca-213">當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們建立新的 "NotFound" 視圖範本（如果目錄不存在，也會建立）：</span><span class="sxs-lookup"><span data-stu-id="d1eca-213">When we click the "Add" button, Visual Studio will create a new "NotFound.aspx" view template for us within the "\Views\Dinners" directory (which it will also create if the directory doesn't already exist):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image10.png)

<span data-ttu-id="d1eca-214">它也會在程式碼編輯器中開啟新的「NotFound .aspx」視圖範本：</span><span class="sxs-lookup"><span data-stu-id="d1eca-214">It will also open up our new "NotFound.aspx" view template within the code-editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image11.png)

<span data-ttu-id="d1eca-215">根據預設，視圖範本有兩個「內容區域」，我們可以在其中新增內容和程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1eca-215">View templates by default have two "content regions" where we can add content and code.</span></span> <span data-ttu-id="d1eca-216">第一個可讓我們自訂送回之 HTML 網頁的「標題」。</span><span class="sxs-lookup"><span data-stu-id="d1eca-216">The first allows us to customize the "title" of the HTML page sent back.</span></span> <span data-ttu-id="d1eca-217">第二個可讓我們自訂送回之 HTML 網頁的「主要內容」。</span><span class="sxs-lookup"><span data-stu-id="d1eca-217">The second allows us to customize the "main content" of the HTML page sent back.</span></span>

<span data-ttu-id="d1eca-218">若要執行我們的「NotFound」視圖範本，我們將新增一些基本內容：</span><span class="sxs-lookup"><span data-stu-id="d1eca-218">To implement our "NotFound" view template we'll add some basic content:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample7.aspx)]

<span data-ttu-id="d1eca-219">然後，我們可以在瀏覽器內試用它。</span><span class="sxs-lookup"><span data-stu-id="d1eca-219">We can then try it out within the browser.</span></span> <span data-ttu-id="d1eca-220">若要這麼做，讓我們要求 *"/Dinners/Details/9999"* URL。</span><span class="sxs-lookup"><span data-stu-id="d1eca-220">To do this let's request the *"/Dinners/Details/9999"* URL.</span></span> <span data-ttu-id="d1eca-221">這會參考目前不存在於資料庫中的晚餐，並會導致我們的 DinnersController （）動作方法呈現我們的 "NotFound" 視圖範本：</span><span class="sxs-lookup"><span data-stu-id="d1eca-221">This will refer to a dinner that doesn't currently exist in the database, and will cause our DinnersController.Details() action method to render our "NotFound" view template:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image12.png)

<span data-ttu-id="d1eca-222">您在上面的螢幕擷取畫面中會注意到的一件事，就是我們的「基本觀點」範本繼承了一堆圍繞螢幕上主要內容的 HTML。</span><span class="sxs-lookup"><span data-stu-id="d1eca-222">One thing you'll notice in the screen-shot above is that our basic view template has inherited a bunch of HTML that surrounds the main content on the screen.</span></span> <span data-ttu-id="d1eca-223">這是因為我們的視圖範本使用「主版頁面」範本，可讓我們在網站上的所有視圖中套用一致的版面配置。</span><span class="sxs-lookup"><span data-stu-id="d1eca-223">This is because our view-template is using a "master page" template that enables us to apply a consistent layout across all views on the site.</span></span> <span data-ttu-id="d1eca-224">我們將在本教學課程稍後的部分討論主版頁面的工作方式。</span><span class="sxs-lookup"><span data-stu-id="d1eca-224">We'll discuss how master pages work more in a later part of this tutorial.</span></span>

### <a name="implementing-the-details-view-template"></a><span data-ttu-id="d1eca-225">執行「詳細資料」視圖範本</span><span class="sxs-lookup"><span data-stu-id="d1eca-225">Implementing the "Details" View Template</span></span>

<span data-ttu-id="d1eca-226">現在，讓我們來執行「詳細資料」視圖範本，這會針對單一晚餐模型產生 HTML。</span><span class="sxs-lookup"><span data-stu-id="d1eca-226">Let's now implement the "Details" view template – which will generate HTML for a single Dinner model.</span></span>

<span data-ttu-id="d1eca-227">若要這麼做，請將文字游標放在詳細資料動作方法中，然後以滑鼠右鍵按一下並選擇 [加入視圖] 功能表命令（或按下 Ctrl-M、Ctrl + V）：</span><span class="sxs-lookup"><span data-stu-id="d1eca-227">We'll do this by positioning our text cursor within the Details action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image13.png)

<span data-ttu-id="d1eca-228">這會顯示 [新增視圖] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="d1eca-228">This will bring up the "Add View" dialog.</span></span> <span data-ttu-id="d1eca-229">我們會保留預設的視圖名稱（「詳細資料」）。</span><span class="sxs-lookup"><span data-stu-id="d1eca-229">We'll keep the default view name ("Details").</span></span> <span data-ttu-id="d1eca-230">我們也會選取對話方塊中的 [建立強型別視圖] 核取方塊，然後選取（使用 combobox 下拉式清單）我們從控制器傳遞至視圖的模型類型名稱。</span><span class="sxs-lookup"><span data-stu-id="d1eca-230">We'll also select the "Create a strongly-typed View" checkbox in the dialog and select (using the combobox dropdown) the name of the model type we are passing from the Controller to the View.</span></span> <span data-ttu-id="d1eca-231">在此視圖中，我們會傳遞晚餐物件（此類型的完整名稱為： "NerdDinner"）：</span><span class="sxs-lookup"><span data-stu-id="d1eca-231">For this view we are passing a Dinner object (the fully qualified name for this type is: "NerdDinner.Models.Dinner"):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image14.png)

<span data-ttu-id="d1eca-232">不同于先前的範本，我們選擇建立「空的視圖」，這次我們會選擇使用「詳細資料」範本自動「scaffold」此視圖。</span><span class="sxs-lookup"><span data-stu-id="d1eca-232">Unlike the previous template, where we chose to create an "Empty View", this time we will choose to automatically "scaffold" the view using a "Details" template.</span></span> <span data-ttu-id="d1eca-233">我們可以藉由變更上述對話方塊中的 [視圖內容] 下拉式功能表來指出這一點。</span><span class="sxs-lookup"><span data-stu-id="d1eca-233">We can indicate this by changing the "View content" drop-down in the dialog above.</span></span>

<span data-ttu-id="d1eca-234">「架構」會根據我們要傳遞給它的晚餐物件，產生詳細資料檢視範本的初始執行。</span><span class="sxs-lookup"><span data-stu-id="d1eca-234">"Scaffolding" will generate an initial implementation of our details view template based on the Dinner object we are passing to it.</span></span> <span data-ttu-id="d1eca-235">這可讓我們快速地開始使用我們的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="d1eca-235">This provides an easy way for us to quickly get started on our view template implementation.</span></span>

<span data-ttu-id="d1eca-236">當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們建立新的 "default.aspx" view 範本檔案：</span><span class="sxs-lookup"><span data-stu-id="d1eca-236">When we click the "Add" button, Visual Studio will create a new "Details.aspx" view template file for us within our "\Views\Dinners" directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image15.png)

<span data-ttu-id="d1eca-237">它也會在程式碼編輯器中開啟新的「詳細資料 .aspx」視圖範本。</span><span class="sxs-lookup"><span data-stu-id="d1eca-237">It will also open up our new "Details.aspx" view template within the code-editor.</span></span> <span data-ttu-id="d1eca-238">它將包含以晚餐模型為基礎之詳細資料檢視的初始 scaffold 執行。</span><span class="sxs-lookup"><span data-stu-id="d1eca-238">It will contain an initial scaffold implementation of a details view based on a Dinner model.</span></span> <span data-ttu-id="d1eca-239">此樣板引擎會使用 .NET 反映來查看傳遞給它的類別所公開的公用屬性，並根據它找到的每個類型來新增適當的內容：</span><span class="sxs-lookup"><span data-stu-id="d1eca-239">The scaffolding engine uses .NET reflection to look at the public properties exposed on the class passed it, and will add appropriate content based on each type it finds:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample8.aspx)]

<span data-ttu-id="d1eca-240">我們可以要求 *"/Dinners/Details/1"* URL，以查看此「詳細資料」 scaffold 在瀏覽器中的執行外觀。</span><span class="sxs-lookup"><span data-stu-id="d1eca-240">We can request the *"/Dinners/Details/1"* URL to see what this "details" scaffold implementation looks like in the browser.</span></span> <span data-ttu-id="d1eca-241">使用此 URL 時，將會顯示我們在第一次建立資料庫時，手動新增至資料庫的其中一個 dinners：</span><span class="sxs-lookup"><span data-stu-id="d1eca-241">Using this URL will display one of the dinners we manually added to our database when we first created it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image16.png)

<span data-ttu-id="d1eca-242">這會讓我們快速啟動並執行，並為我們提供詳細資料 .aspx 視圖的初始程式。</span><span class="sxs-lookup"><span data-stu-id="d1eca-242">This gets us up and running quickly, and provides us with an initial implementation of our Details.aspx view.</span></span> <span data-ttu-id="d1eca-243">然後我們可以調整它，以自訂 UI 以符合我們的滿意度。</span><span class="sxs-lookup"><span data-stu-id="d1eca-243">We can then go and tweak it to customize the UI to our satisfaction.</span></span>

<span data-ttu-id="d1eca-244">當我們更仔細查看 default.aspx 範本時，我們會發現它包含靜態 HTML 和內嵌的轉譯程式碼。</span><span class="sxs-lookup"><span data-stu-id="d1eca-244">When we look at the Details.aspx template more closely, we'll find that it contains static HTML as well as embedded rendering code.</span></span> <span data-ttu-id="d1eca-245">&lt;%%&gt; 程式碼區塊會在視圖範本呈現時執行程式碼，而 &lt;% =%&gt; 程式碼區塊執行其中包含的程式碼，然後將結果轉譯為範本的輸出資料流程。</span><span class="sxs-lookup"><span data-stu-id="d1eca-245">&lt;% %&gt; code nuggets execute code when the view template renders, and &lt;%= %&gt; code nuggets execute the code contained within them and then render the result to the output stream of the template.</span></span>

<span data-ttu-id="d1eca-246">我們可以在我們的觀點中撰寫程式碼，以存取使用強型別「模型」屬性從我們的控制器傳遞的「晚餐」模型物件。</span><span class="sxs-lookup"><span data-stu-id="d1eca-246">We can write code within our View that accesses the "Dinner" model object that was passed from our controller using a strongly-typed "Model" property.</span></span> <span data-ttu-id="d1eca-247">Visual Studio 在編輯器中存取此 "Model" 屬性時，會提供完整的程式碼 intellisense：</span><span class="sxs-lookup"><span data-stu-id="d1eca-247">Visual Studio provides us with full code-intellisense when accessing this "Model" property within the editor:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image17.png)

<span data-ttu-id="d1eca-248">讓我們進行一些調整，讓最終詳細資料檢視範本的來源看起來如下：</span><span class="sxs-lookup"><span data-stu-id="d1eca-248">Let's make some tweaks so that the source for our final Details view template looks like below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample9.aspx)]

<span data-ttu-id="d1eca-249">當我們再次存取 *"/Dinners/Details/1"* URL 時，它現在會呈現如下：</span><span class="sxs-lookup"><span data-stu-id="d1eca-249">When we access the *"/Dinners/Details/1"* URL again it will now render like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image18.png)

### <a name="implementing-the-index-view-template"></a><span data-ttu-id="d1eca-250">執行「索引」視圖範本</span><span class="sxs-lookup"><span data-stu-id="d1eca-250">Implementing the "Index" View Template</span></span>

<span data-ttu-id="d1eca-251">現在讓我們來執行「Index」 view 範本，這會產生即將推出的 Dinners 清單。</span><span class="sxs-lookup"><span data-stu-id="d1eca-251">Let's now implement the "Index" view template – which will generate a listing of upcoming Dinners.</span></span> <span data-ttu-id="d1eca-252">為此，我們會將文字游標放在索引動作方法內，然後以滑鼠右鍵按一下並選擇 [加入視圖] 功能表命令（或按 Ctrl-M、Ctrl + V）。</span><span class="sxs-lookup"><span data-stu-id="d1eca-252">To-do this we'll position our text cursor within the Index action method, and then right click and choose the "Add View" menu command (or press Ctrl-M, Ctrl-V).</span></span>

<span data-ttu-id="d1eca-253">在 [加入視圖] 對話方塊中，我們會保留名為 "Index" 的視圖範本，然後選取 [建立強型別的視圖] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="d1eca-253">Within the "Add View" dialog we'll keep the view template named "Index" and select the "Create a strongly-typed view" checkbox.</span></span> <span data-ttu-id="d1eca-254">這次我們會選擇自動產生「清單」視圖範本，並選取「NerdDinner」作為模型類型傳遞至「視圖」（因為我們指出我們要建立「清單」 scaffold 會使 [加入視圖] 對話方塊假設我們是將一系列的晚餐物件從我們的控制器傳遞至視圖）：</span><span class="sxs-lookup"><span data-stu-id="d1eca-254">This time we will choose to automatically generate a "List" view template, and select "NerdDinner.Models.Dinner" as the model type passed to the view (which because we have indicated we are creating a "List" scaffold will cause the Add View dialog to assume we are passing a sequence of Dinner objects from our Controller to the View):</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image19.png)

<span data-ttu-id="d1eca-255">當我們按一下 [新增] 按鈕時，Visual Studio 會在 "\Views\Dinners" 目錄中為我們建立新的 "Index .aspx" view 範本檔案。</span><span class="sxs-lookup"><span data-stu-id="d1eca-255">When we click the "Add" button, Visual Studio will create a new "Index.aspx" view template file for us within our "\Views\Dinners" directory.</span></span> <span data-ttu-id="d1eca-256">它會「scaffold」它在其中的初始執行，它會提供一個 HTML 資料表，列出我們傳遞給視圖的 Dinners。</span><span class="sxs-lookup"><span data-stu-id="d1eca-256">It will "scaffold" an initial implementation within it that provides an HTML table listing of the Dinners we pass to the view.</span></span>

<span data-ttu-id="d1eca-257">當我們執行應用程式並存取 *"/Dinners/"* URL 時，它會轉譯我們的 Dinners 清單，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1eca-257">When we run the application and access the *"/Dinners/"* URL it will render our list of dinners like so:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image20.png)

<span data-ttu-id="d1eca-258">上述資料表解決方案提供我們晚餐資料的類似方格版面配置，這不是我們想要取用者面向晚餐的清單。</span><span class="sxs-lookup"><span data-stu-id="d1eca-258">The table solution above gives us a grid-like layout of our Dinner data – which isn't quite what we want for our consumer facing Dinner listing.</span></span> <span data-ttu-id="d1eca-259">我們可以更新 default.aspx view 範本並加以修改，以列出較少的資料行，並使用 &lt;的 ul&gt; 元素來轉譯它們，而不是使用下列程式碼來呈現資料表：</span><span class="sxs-lookup"><span data-stu-id="d1eca-259">We can update the Index.aspx view template and modify it to list fewer columns of data, and use a &lt;ul&gt; element to render them instead of a table using the code below:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample10.aspx)]

<span data-ttu-id="d1eca-260">我們使用上述 foreach 語句內的 "var" 關鍵字，因為我們會在我們的模型中迴圈處理每個晚餐。</span><span class="sxs-lookup"><span data-stu-id="d1eca-260">We are using the "var" keyword within the above foreach statement as we loop over each dinner in our Model.</span></span> <span data-ttu-id="d1eca-261">不熟悉C# 3.0 的人可能會認為使用「var」表示晚餐物件是晚期繫結。</span><span class="sxs-lookup"><span data-stu-id="d1eca-261">Those unfamiliar with C# 3.0 might think that using "var" means that the dinner object is late-bound.</span></span> <span data-ttu-id="d1eca-262">相反地，編譯器會針對強型別 "Model" 屬性（其型別為 "IEnumerable&lt;晚餐&gt;"）使用類型推斷，並將當地的「晚餐」變數編譯為晚餐類型，這表示我們會在程式碼區塊內取得完整的 intellisense 和編譯時間檢查：</span><span class="sxs-lookup"><span data-stu-id="d1eca-262">It instead means that the compiler is using type-inference against the strongly typed "Model" property (which is of type "IEnumerable&lt;Dinner&gt;") and compiling the local "dinner" variable as a Dinner type – which means we get full intellisense and compile-time checking for it within code blocks:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image21.png)

<span data-ttu-id="d1eca-263">當我們在瀏覽器中按下 */Dinners* URL 的重新整理時，我們的更新視圖現在如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1eca-263">When we hit refresh on the */Dinners* URL in our browser our updated view now looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image22.png)

<span data-ttu-id="d1eca-264">這看起來更好，但尚未完成。</span><span class="sxs-lookup"><span data-stu-id="d1eca-264">This is looking better – but isn't entirely there yet.</span></span> <span data-ttu-id="d1eca-265">最後一個步驟是讓使用者按一下清單中的個別 Dinners，並查看其相關詳細資料。</span><span class="sxs-lookup"><span data-stu-id="d1eca-265">Our last step is to enable end-users to click individual Dinners in the list and see details about them.</span></span> <span data-ttu-id="d1eca-266">我們會藉由呈現連結至 DinnersController 上 Details 動作方法的 HTML 超連結元素，來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="d1eca-266">We'll implement this by rendering HTML hyperlink elements that link to the Details action method on our DinnersController.</span></span>

<span data-ttu-id="d1eca-267">我們可以透過兩種方式的其中一種，在索引視圖內產生這些超連結。</span><span class="sxs-lookup"><span data-stu-id="d1eca-267">We can generate these hyperlinks within our Index view in one of two ways.</span></span> <span data-ttu-id="d1eca-268">第一個是手動建立 HTML &lt;如下所示的&gt; 元素，我們會在 &lt;HTML 專案中內嵌 &lt;%%&gt; 區塊：&gt;</span><span class="sxs-lookup"><span data-stu-id="d1eca-268">The first is to manually create HTML &lt;a&gt; elements like below, where we embed &lt;% %&gt; blocks within the &lt;a&gt; HTML element:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image23.png)

<span data-ttu-id="d1eca-269">我們可以使用的替代方法，是利用 ASP.NET MVC 中的內建 "Html.actionlink （）" helper 方法，以程式設計方式建立 HTML &lt;&gt; 元素，該專案會連結至控制器上的另一個動作方法：</span><span class="sxs-lookup"><span data-stu-id="d1eca-269">An alternative approach we can use is to take advantage of the built-in "Html.ActionLink()" helper method within ASP.NET MVC that supports programmatically creating an HTML &lt;a&gt; element that links to another action method on a Controller:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample11.aspx)]

<span data-ttu-id="d1eca-270">Html 的第一個參數。 Html.actionlink （） helper 方法是要顯示的連結文字（在此案例中為晚餐的標題），第二個參數是我們想要產生連結的控制器動作名稱（在此案例中為 Details 方法），而第三個參數是要傳送至動作的一組參數（實作為具有屬性名稱/值的匿名型別）。</span><span class="sxs-lookup"><span data-stu-id="d1eca-270">The first parameter to the Html.ActionLink() helper method is the link-text to display (in this case the title of the dinner), the second parameter is the Controller action name we want to generate the link to (in this case the Details method), and the third parameter is a set of parameters to send to the action (implemented as an anonymous type with property name/values).</span></span> <span data-ttu-id="d1eca-271">在此情況下，我們會指定我們想要連結的晚餐的「識別碼」參數，而且因為 ASP.NET MVC 中的預設 URL 路由規則是 "{Controller}/{Action}/{id}"，所以 .Html （） helper 方法會產生下列輸出：</span><span class="sxs-lookup"><span data-stu-id="d1eca-271">In this case we are specifying the "id" parameter of the dinner we want to link to, and because the default URL routing rule in ASP.NET MVC is "{Controller}/{Action}/{id}" the Html.ActionLink() helper method will generate the following output:</span></span>

[!code-html[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample12.html)]

<span data-ttu-id="d1eca-272">針對我們的 Index .aspx view，我們將使用 Html.actionlink （） helper 方法方法，並將清單中的每個晚餐連結至適當的詳細資料 URL：</span><span class="sxs-lookup"><span data-stu-id="d1eca-272">For our Index.aspx view we'll use the Html.ActionLink() helper method approach and have each dinner in the list link to the appropriate details URL:</span></span>

[!code-aspx[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample13.aspx)]

<span data-ttu-id="d1eca-273">現在當我們達到 */Dinners* URL 時，我們的晚餐清單如下所示：</span><span class="sxs-lookup"><span data-stu-id="d1eca-273">And now when we hit the */Dinners* URL our dinner list looks like below:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image24.png)

<span data-ttu-id="d1eca-274">當我們按一下清單中的任何 Dinners 時，我們會流覽以查看其詳細資料：</span><span class="sxs-lookup"><span data-stu-id="d1eca-274">When we click any of the Dinners in the list we'll navigate to see details about it:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image25.png)

### <a name="convention-based-naming-and-the-views-directory-structure"></a><span data-ttu-id="d1eca-275">以慣例為基礎的命名和 \Views 目錄結構</span><span class="sxs-lookup"><span data-stu-id="d1eca-275">Convention-based naming and the \Views directory structure</span></span>

<span data-ttu-id="d1eca-276">在解析視圖範本時，預設會 ASP.NET MVC 應用程式使用以慣例為基礎的目錄命名結構。</span><span class="sxs-lookup"><span data-stu-id="d1eca-276">ASP.NET MVC applications by default use a convention-based directory naming structure when resolving view templates.</span></span> <span data-ttu-id="d1eca-277">這可讓開發人員在參考控制器類別內的視圖時，避免必須完整限定位置路徑。</span><span class="sxs-lookup"><span data-stu-id="d1eca-277">This allows developers to avoid having to fully-qualify a location path when referencing views from within a Controller class.</span></span> <span data-ttu-id="d1eca-278">根據預設，ASP.NET MVC 會在應用程式底下的 \* \Views\[ControllerName]\* 目錄中尋找視圖範本檔案。</span><span class="sxs-lookup"><span data-stu-id="d1eca-278">By default ASP.NET MVC will look for the view template file within the \*\Views\[ControllerName]\* directory underneath the application.</span></span>

<span data-ttu-id="d1eca-279">例如，我們一直在處理 DinnersController 類別，它會明確參考三個視圖範本：「索引」、「詳細資料」和「NotFound」。</span><span class="sxs-lookup"><span data-stu-id="d1eca-279">For example, we've been working on the DinnersController class – which explicitly references three view templates: "Index", "Details" and "NotFound".</span></span> <span data-ttu-id="d1eca-280">ASP.NET MVC 預設會在應用程式根目錄底下的 *\Views\Dinners*目錄中尋找這些 views：</span><span class="sxs-lookup"><span data-stu-id="d1eca-280">ASP.NET MVC will by default look for these views within the *\Views\Dinners* directory underneath our application root directory:</span></span>

![](use-controllers-and-views-to-implement-a-listingdetails-ui/_static/image26.png)

<span data-ttu-id="d1eca-281">請注意，專案中目前有三個控制器類別（DinnersController、HomeController 和 AccountController –在建立專案時，預設會新增最後兩個），而且有三個子目錄（每個目錄各有一個）控制器），在 \Views 目錄中。</span><span class="sxs-lookup"><span data-stu-id="d1eca-281">Notice above how there are currently three controller classes within the project (DinnersController, HomeController and AccountController – the last two were added by default when we created the project), and there are three sub-directories (one for each controller) within the \Views directory.</span></span>

<span data-ttu-id="d1eca-282">從 Home 和 Accounts 控制器參考的視圖，會自動從個別的 *\Views\Home*和 *\Views\Account*目錄解析其視圖範本。</span><span class="sxs-lookup"><span data-stu-id="d1eca-282">Views referenced from the Home and Accounts controllers will automatically resolve their view templates from the respective *\Views\Home* and *\Views\Account* directories.</span></span> <span data-ttu-id="d1eca-283">*\Views\Shared*子目錄提供了一種方式，可以儲存跨應用程式內多個控制器重複使用的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="d1eca-283">The *\Views\Shared* sub-directory provides a way to store view templates that are re-used across multiple controllers within the application.</span></span> <span data-ttu-id="d1eca-284">當 ASP.NET MVC 嘗試解析視圖範本時，它會先在 *\Views\[Controller]* 特定目錄內進行檢查，如果找不到 view 範本，它會在 *\Views\Shared*目錄中尋找。</span><span class="sxs-lookup"><span data-stu-id="d1eca-284">When ASP.NET MVC attempts to resolve a view template, it will first check within the *\Views\[Controller]* specific directory, and if it can't find the view template there it will look within the *\Views\Shared* directory.</span></span>

<span data-ttu-id="d1eca-285">在命名個別的視圖範本時，建議的指引是讓視圖範本共用與造成它呈現的動作方法相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="d1eca-285">When it comes to naming individual view templates, the recommended guidance is to have the view template share the same name as the action method that caused it to render.</span></span> <span data-ttu-id="d1eca-286">例如，上面的「索引」動作方法會使用「索引」視圖來轉譯視圖結果，而「詳細資料」動作方法會使用「詳細資料」視圖來呈現其結果。</span><span class="sxs-lookup"><span data-stu-id="d1eca-286">For example, above our "Index" action method is using the "Index" view to render the view result, and the "Details" action method is using the "Details" view to render its results.</span></span> <span data-ttu-id="d1eca-287">這可讓您輕鬆地快速查看與每個動作相關聯的範本。</span><span class="sxs-lookup"><span data-stu-id="d1eca-287">This makes it easy to quickly see which template is associated with each action.</span></span>

<span data-ttu-id="d1eca-288">當視圖範本的名稱與在控制器上叫用的動作方法相同時，開發人員不需要明確指定視圖範本名稱。</span><span class="sxs-lookup"><span data-stu-id="d1eca-288">Developers do not need to explicitly specify the view template name when the view template has the same name as the action method being invoked on the controller.</span></span> <span data-ttu-id="d1eca-289">我們可以改為只將模型物件傳遞給 "View （）" 協助程式方法（不指定視圖名稱），而 ASP.NET MVC 會自動推斷要使用磁片上的 *\Views\[ControllerName]\[ActionName]* View 範本來呈現它。</span><span class="sxs-lookup"><span data-stu-id="d1eca-289">We can instead just pass the model object to the "View()" helper method (without specifying the view name), and ASP.NET MVC will automatically infer that we want to use the *\Views\[ControllerName]\[ActionName]* view template on disk to render it.</span></span>

<span data-ttu-id="d1eca-290">這可讓我們稍微清理我們的控制器程式碼，並避免在我們的程式碼中重複此名稱兩次：</span><span class="sxs-lookup"><span data-stu-id="d1eca-290">This allows us to clean up our controller code a little, and avoid duplicating the name twice in our code:</span></span>

[!code-csharp[Main](use-controllers-and-views-to-implement-a-listingdetails-ui/samples/sample14.cs)]

<span data-ttu-id="d1eca-291">上述程式碼就是為網站實現絕佳晚餐清單/詳細資料體驗所需的一切。</span><span class="sxs-lookup"><span data-stu-id="d1eca-291">The above code is all that is needed to implement a nice Dinner listing/details experience for the site.</span></span>

#### <a name="next-step"></a><span data-ttu-id="d1eca-292">後續步驟</span><span class="sxs-lookup"><span data-stu-id="d1eca-292">Next Step</span></span>

<span data-ttu-id="d1eca-293">我們現在已建立好的晚餐流覽體驗。</span><span class="sxs-lookup"><span data-stu-id="d1eca-293">We now have a nice Dinner browsing experience built.</span></span>

<span data-ttu-id="d1eca-294">現在讓我們啟用 CRUD （建立、讀取、更新、刪除）資料表單編輯支援。</span><span class="sxs-lookup"><span data-stu-id="d1eca-294">Let's now enable CRUD (Create, Read, Update, Delete) data form editing support.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="d1eca-295">[上一頁](build-a-model-with-business-rule-validations.md)
> [下一頁](provide-crud-create-read-update-delete-data-form-entry-support.md)</span><span class="sxs-lookup"><span data-stu-id="d1eca-295">[Previous](build-a-model-with-business-rule-validations.md)
[Next](provide-crud-create-read-update-delete-data-form-entry-support.md)</span></span>
