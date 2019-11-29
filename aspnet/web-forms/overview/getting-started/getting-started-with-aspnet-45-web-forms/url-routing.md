---
uid: web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
title: URL 路由 |Microsoft Docs
author: Erikre
description: 本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 為我們建立 ASP.NET Web Forms 應用程式的基本概念 。
ms.author: riande
ms.date: 09/08/2014
ms.assetid: 4f4bf092-c400-471f-a876-78fda0417890
msc.legacyurl: /web-forms/overview/getting-started/getting-started-with-aspnet-45-web-forms/url-routing
msc.type: authoredcontent
ms.openlocfilehash: 66b727b69ca4f9a3d35b67f492f9a554146e09ef
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590715"
---
# <a name="url-routing"></a><span data-ttu-id="dc946-103">URL 路由</span><span class="sxs-lookup"><span data-stu-id="dc946-103">URL Routing</span></span>

<span data-ttu-id="dc946-104">依[Erik Reitan](https://github.com/Erikre)</span><span class="sxs-lookup"><span data-stu-id="dc946-104">by [Erik Reitan](https://github.com/Erikre)</span></span>

<span data-ttu-id="dc946-105">[下載 Wingtip 玩具範例專案（C#）](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)或[下載電子書（PDF）](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span><span class="sxs-lookup"><span data-stu-id="dc946-105">[Download Wingtip Toys Sample Project (C#)](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) or [Download E-book (PDF)](https://download.microsoft.com/download/0/F/B/0FBFAA46-2BFD-478F-8E56-7BF3C672DF9D/Getting%20Started%20with%20ASP.NET%204.5%20Web%20Forms%20and%20Visual%20Studio%202013.pdf)</span></span>

> <span data-ttu-id="dc946-106">本教學課程系列將教您使用 ASP.NET 4.5 和 Microsoft Visual Studio Express 2013 for Web 建立 ASP.NET Web Forms 應用程式的基本概念。</span><span class="sxs-lookup"><span data-stu-id="dc946-106">This tutorial series will teach you the basics of building an ASP.NET Web Forms application using ASP.NET 4.5 and Microsoft Visual Studio Express 2013 for Web.</span></span> <span data-ttu-id="dc946-107">本教學課程系列隨附有[ C#原始程式碼](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409)的 Visual Studio 2013 專案。</span><span class="sxs-lookup"><span data-stu-id="dc946-107">A Visual Studio 2013 [project with C# source code](https://go.microsoft.com/fwlink/?LinkID=389434&clcid=0x409) is available to accompany this tutorial series.</span></span>

<span data-ttu-id="dc946-108">在本教學課程中，您將修改 Wingtip 玩具範例應用程式以支援 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-108">In this tutorial, you will modify the Wingtip Toys sample application to support URL routing.</span></span> <span data-ttu-id="dc946-109">路由可讓您的 web 應用程式使用易記、容易記住的 Url，並提供更好的搜尋引擎支援。</span><span class="sxs-lookup"><span data-stu-id="dc946-109">Routing enables your web application to use URLs that are friendly, easier to remember, and better supported by search engines.</span></span> <span data-ttu-id="dc946-110">本教學課程是以先前的教學課程「成員資格和系統管理」為基礎，而且是 Wingtip 玩具教學課程系列的一部分。</span><span class="sxs-lookup"><span data-stu-id="dc946-110">This tutorial builds on the previous tutorial "Membership and Administration" and is part of the Wingtip Toys tutorial series.</span></span>

## <a name="what-youll-learn"></a><span data-ttu-id="dc946-111">您將瞭解的內容：</span><span class="sxs-lookup"><span data-stu-id="dc946-111">What you'll learn:</span></span>

- <span data-ttu-id="dc946-112">如何註冊 ASP.NET Web Forms 應用程式的路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-112">How to register routes for an ASP.NET Web Forms application.</span></span>
- <span data-ttu-id="dc946-113">如何將路由加入至網頁。</span><span class="sxs-lookup"><span data-stu-id="dc946-113">How to add routes to a web page.</span></span>
- <span data-ttu-id="dc946-114">如何從資料庫選取資料以支援路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-114">How to select data from a database to support routes.</span></span>

## <a name="aspnet-routing-overview"></a><span data-ttu-id="dc946-115">ASP.NET 路由總覽</span><span class="sxs-lookup"><span data-stu-id="dc946-115">ASP.NET Routing Overview</span></span>

<span data-ttu-id="dc946-116">URL 路由可讓您設定應用程式，以接受未對應至實體檔案的要求 Url。</span><span class="sxs-lookup"><span data-stu-id="dc946-116">URL routing allows you to configure an application to accept request URLs that do not map to physical files.</span></span> <span data-ttu-id="dc946-117">要求 URL 只是使用者在瀏覽器中輸入的 URL，以便在您的網站上尋找頁面。</span><span class="sxs-lookup"><span data-stu-id="dc946-117">A request URL is simply the URL a user enters into their browser to find a page on your web site.</span></span> <span data-ttu-id="dc946-118">您可以使用路由來定義對使用者有意義的 Url，並可協助搜尋引擎優化（SEO）。</span><span class="sxs-lookup"><span data-stu-id="dc946-118">You use routing to define URLs that are semantically meaningful to users and that can help with search-engine optimization (SEO).</span></span>

<span data-ttu-id="dc946-119">根據預設，Web Forms 範本包含[ASP.NET 易記 url](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)。</span><span class="sxs-lookup"><span data-stu-id="dc946-119">By default, the Web Forms template includes [ASP.NET Friendly URLs](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/).</span></span> <span data-ttu-id="dc946-120">大部分的基本路由工作都是使用*易記 url*來執行。</span><span class="sxs-lookup"><span data-stu-id="dc946-120">Much of the basic routing work will be implemented by using *Friendly URLs*.</span></span> <span data-ttu-id="dc946-121">不過，在本教學課程中，您將新增自訂的路由功能。</span><span class="sxs-lookup"><span data-stu-id="dc946-121">However, in this tutorial you will add customized routing capabilities.</span></span>

<span data-ttu-id="dc946-122">在自訂 URL 路由之前，Wingtip 玩具範例應用程式可以使用下列 URL 連結至產品：</span><span class="sxs-lookup"><span data-stu-id="dc946-122">Before customizing URL routing, the Wingtip Toys sample application can link to a product using the following URL:</span></span>

`https://localhost:44300/ProductDetails.aspx?productID=2`

<span data-ttu-id="dc946-123">藉由自訂 URL 路由，Wingtip 玩具範例應用程式會使用更容易閱讀的 URL 來連結至相同的產品：</span><span class="sxs-lookup"><span data-stu-id="dc946-123">By customizing URL routing, the Wingtip Toys sample application will link to the same product using an easier to read URL:</span></span>

`https://localhost:44300/Product/Convertible%20Car`

### <a name="routes"></a><span data-ttu-id="dc946-124">路由</span><span class="sxs-lookup"><span data-stu-id="dc946-124">Routes</span></span>

<span data-ttu-id="dc946-125">路由是對應至處理常式的 URL 模式。</span><span class="sxs-lookup"><span data-stu-id="dc946-125">A route is a URL pattern that is mapped to a handler.</span></span> <span data-ttu-id="dc946-126">處理常式可以是實體檔案，例如 Web Forms 應用程式中的 .aspx 檔案。</span><span class="sxs-lookup"><span data-stu-id="dc946-126">The handler can be a physical file, such as an .aspx file in a Web Forms application.</span></span> <span data-ttu-id="dc946-127">處理常式也可以是處理要求的類別。</span><span class="sxs-lookup"><span data-stu-id="dc946-127">A handler can also be a class that processes the request.</span></span> <span data-ttu-id="dc946-128">若要定義路由，您可以藉由指定 URL 模式、處理常式和選擇性的路由名稱，來建立路由類別的實例。</span><span class="sxs-lookup"><span data-stu-id="dc946-128">To define a route, you create an instance of the Route class by specifying the URL pattern, the handler, and optionally a name for the route.</span></span>

<span data-ttu-id="dc946-129">您可以藉由將 `Route` 物件加入至 `RouteTable` 類別的靜態 `Routes` 屬性，將路由新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc946-129">You add the route to the application by adding the `Route` object to the static `Routes` property of the `RouteTable` class.</span></span> <span data-ttu-id="dc946-130">Route 屬性是一個 `RouteCollection` 物件，它會儲存應用程式的所有路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-130">The Routes property is a `RouteCollection` object that stores all the routes for the application.</span></span>

### <a name="url-patterns"></a><span data-ttu-id="dc946-131">URL 模式</span><span class="sxs-lookup"><span data-stu-id="dc946-131">URL Patterns</span></span>

<span data-ttu-id="dc946-132">URL 模式可以包含常值和變數預留位置（稱為 URL 參數）。</span><span class="sxs-lookup"><span data-stu-id="dc946-132">A URL pattern can contain literal values and variable placeholders (referred to as URL parameters).</span></span> <span data-ttu-id="dc946-133">常值和預留位置位於以斜線（`/`）字元分隔的 URL 區段中。</span><span class="sxs-lookup"><span data-stu-id="dc946-133">The literals and placeholders are located in segments of the URL which are delimited by the slash (`/`) character.</span></span>

<span data-ttu-id="dc946-134">當您對 web 應用程式提出要求時，會將 URL 剖析為區段和預留位置，並將變數值提供給要求處理常式。</span><span class="sxs-lookup"><span data-stu-id="dc946-134">When a request to your web application is made, the URL is parsed into segments and placeholders, and the variable values are provided to the request handler.</span></span> <span data-ttu-id="dc946-135">此程式類似于分析查詢字串中的資料，並將其傳遞給要求處理常式的方式。</span><span class="sxs-lookup"><span data-stu-id="dc946-135">This process is similar to the way the data in a query string is parsed and passed to the request handler.</span></span> <span data-ttu-id="dc946-136">在這兩種情況下，變數資訊都會包含在 URL 中，並以索引鍵/值組的形式傳遞至處理常式。</span><span class="sxs-lookup"><span data-stu-id="dc946-136">In both cases, variable information is included in the URL and passed to the handler in the form of key-value pairs.</span></span> <span data-ttu-id="dc946-137">針對查詢字串，索引鍵和值都在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="dc946-137">For query strings, both the keys and the values are in the URL.</span></span> <span data-ttu-id="dc946-138">針對路由，索引鍵是在 URL 模式中定義的預留位置名稱，而且只有值在 URL 中。</span><span class="sxs-lookup"><span data-stu-id="dc946-138">For routes, the keys are the placeholder names defined in the URL pattern, and only the values are in the URL.</span></span>

<span data-ttu-id="dc946-139">在 URL 模式中，您可以將預留位置括在大括弧（`{` 和 `}`）來定義。</span><span class="sxs-lookup"><span data-stu-id="dc946-139">In a URL pattern, you define placeholders by enclosing them in braces ( `{` and `}` ).</span></span> <span data-ttu-id="dc946-140">您可以在區段中定義一個以上的預留位置，但預留位置必須以常值分隔。</span><span class="sxs-lookup"><span data-stu-id="dc946-140">You can define more than one placeholder in a segment, but the placeholders must be separated by a literal value.</span></span> <span data-ttu-id="dc946-141">例如，`{language}-{country}/{action}` 是有效的路由模式。</span><span class="sxs-lookup"><span data-stu-id="dc946-141">For example, `{language}-{country}/{action}` is a valid route pattern.</span></span> <span data-ttu-id="dc946-142">不過，`{language}{country}/{action}` 不是有效的模式，因為預留位置之間沒有常值或分隔符號。</span><span class="sxs-lookup"><span data-stu-id="dc946-142">However, `{language}{country}/{action}` is not a valid pattern, because there is no literal value or delimiter between the placeholders.</span></span> <span data-ttu-id="dc946-143">因此，路由無法判斷要將 language 預留位置的值與國家/地區預留位置的值分開。</span><span class="sxs-lookup"><span data-stu-id="dc946-143">Therefore, routing cannot determine where to separate the value for the language placeholder from the value for the country placeholder.</span></span>

### <a name="mapping-and-registering-routes"></a><span data-ttu-id="dc946-144">對應和註冊路由</span><span class="sxs-lookup"><span data-stu-id="dc946-144">Mapping and Registering Routes</span></span>

<span data-ttu-id="dc946-145">在您可以將路由包含在 Wingtip 玩具範例應用程式的頁面之前，您必須在應用程式啟動時註冊路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-145">Before you can include routes to pages of the Wingtip Toys sample application, you must register the routes when the application starts.</span></span> <span data-ttu-id="dc946-146">若要註冊路由，您將修改 `Application_Start` 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="dc946-146">To register the routes, you will modify the `Application_Start` event handler.</span></span>

1. <span data-ttu-id="dc946-147">在 Visual Studio 的**方案總管**中，尋找並開啟*Global.asax.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="dc946-147">In **Solution Explorer**of Visual Studio, find and open the *Global.asax.cs* file.</span></span>
2. <span data-ttu-id="dc946-148">將黃色反白顯示的程式碼新增至*Global.asax.cs*檔案，如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc946-148">Add the code highlighted in yellow to the *Global.asax.cs* file as follows:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample1.cs?highlight=30-31,34-46)]

<span data-ttu-id="dc946-149">當 Wingtip 玩具範例應用程式啟動時，它會呼叫 `Application_Start` 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="dc946-149">When the Wingtip Toys sample application starts, it calls the `Application_Start` event handler.</span></span> <span data-ttu-id="dc946-150">在這個事件處理常式的結尾，會呼叫 `RegisterCustomRoutes` 方法。</span><span class="sxs-lookup"><span data-stu-id="dc946-150">At the end of this event handler, the `RegisterCustomRoutes` method is called.</span></span> <span data-ttu-id="dc946-151">`RegisterCustomRoutes` 方法會藉由呼叫 `RouteCollection` 物件的 `MapPageRoute` 方法來新增每個路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-151">The `RegisterCustomRoutes` method adds each route by calling the `MapPageRoute` method of the `RouteCollection` object.</span></span> <span data-ttu-id="dc946-152">路由的定義是使用路由名稱、路由 URL 和實體 URL。</span><span class="sxs-lookup"><span data-stu-id="dc946-152">Routes are defined using a route name, a route URL and a physical URL.</span></span>

<span data-ttu-id="dc946-153">第一個參數（"`ProductsByCategoryRoute`"）是路由名稱。</span><span class="sxs-lookup"><span data-stu-id="dc946-153">The first parameter ("`ProductsByCategoryRoute`") is the route name.</span></span> <span data-ttu-id="dc946-154">它會在需要時用來呼叫路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-154">It is used to call the route when it is needed.</span></span> <span data-ttu-id="dc946-155">第二個參數（"`Category/{categoryName}`"）定義了易記的取代 URL，可以根據程式碼動態地進行。</span><span class="sxs-lookup"><span data-stu-id="dc946-155">The second parameter ("`Category/{categoryName}`") defines the friendly replacement URL that can be dynamic based on code.</span></span> <span data-ttu-id="dc946-156">當您使用以資料為基礎所產生的連結填入資料控制項時，就會用到此路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-156">You use this route when you are populating a data control with links that are generated based on data.</span></span> <span data-ttu-id="dc946-157">路由如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc946-157">A route is shown as follows:</span></span>

[!code-csharp[Main](url-routing/samples/sample2.cs)]

<span data-ttu-id="dc946-158">路由的第二個參數包含以大括弧（`{ }`）指定的動態值。</span><span class="sxs-lookup"><span data-stu-id="dc946-158">The second parameter of the route includes a dynamic value specified by braces (`{ }`).</span></span> <span data-ttu-id="dc946-159">在此情況下，`categoryName` 是用來判斷適當路由路徑的變數。</span><span class="sxs-lookup"><span data-stu-id="dc946-159">In this case, the `categoryName` is a variable that will be used to determine the proper routing path.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="dc946-160">**Optional**</span><span class="sxs-lookup"><span data-stu-id="dc946-160">**Optional**</span></span>
> 
> <span data-ttu-id="dc946-161">藉由將 `RegisterCustomRoutes` 方法移至不同的類別，您可能會發現管理程式碼較容易。</span><span class="sxs-lookup"><span data-stu-id="dc946-161">You might find it easier to manage your code by moving the `RegisterCustomRoutes` method to a separate class.</span></span> <span data-ttu-id="dc946-162">在*邏輯*資料夾中，建立個別的 `RouteActions` 類別。</span><span class="sxs-lookup"><span data-stu-id="dc946-162">In the *Logic* folder, create a separate `RouteActions` class.</span></span> <span data-ttu-id="dc946-163">將上述 `RegisterCustomRoutes` 方法從*Global.asax.cs*檔案移至新的 `RoutesActions` 類別。</span><span class="sxs-lookup"><span data-stu-id="dc946-163">Move the above `RegisterCustomRoutes` method from the *Global.asax.cs* file into the new `RoutesActions` class.</span></span> <span data-ttu-id="dc946-164">使用 `RoleActions` 類別和 `createAdmin` 方法，作為如何從*Global.asax.cs*檔案呼叫 `RegisterCustomRoutes` 方法的範例。</span><span class="sxs-lookup"><span data-stu-id="dc946-164">Use the `RoleActions` class and the `createAdmin` method as an example of how to call the `RegisterCustomRoutes` method from the *Global.asax.cs* file.</span></span>

<span data-ttu-id="dc946-165">您也可能已注意到使用 `Application_Start` 事件處理常式開頭的 `RouteConfig` 物件 `RegisterRoutes` 方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="dc946-165">You may also have noticed the `RegisterRoutes` method call using the `RouteConfig` object at the beginning of the `Application_Start` event handler.</span></span> <span data-ttu-id="dc946-166">此呼叫是用來執行預設路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-166">This call is made to implement default routing.</span></span> <span data-ttu-id="dc946-167">當您使用 Visual Studio 的 Web form 範本建立應用程式時，它會包含為預設程式碼。</span><span class="sxs-lookup"><span data-stu-id="dc946-167">It was included as default code when you created the application using Visual Studio's Web Forms template.</span></span>

## <a name="retrieving-and-using-route-data"></a><span data-ttu-id="dc946-168">正在抓取和使用路由資料</span><span class="sxs-lookup"><span data-stu-id="dc946-168">Retrieving and Using Route Data</span></span>

<span data-ttu-id="dc946-169">如先前所述，您可以定義路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-169">As mentioned above, routes can be defined.</span></span> <span data-ttu-id="dc946-170">您在*Global.asax.cs*檔案中新增至 `Application_Start` 事件處理常式的程式碼會載入可定義的路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-170">The code that you added to the `Application_Start` event handler in the *Global.asax.cs* file loads the definable routes.</span></span>

### <a name="setting-routes"></a><span data-ttu-id="dc946-171">設定路由</span><span class="sxs-lookup"><span data-stu-id="dc946-171">Setting Routes</span></span>

<span data-ttu-id="dc946-172">路由需要您新增額外的程式碼。</span><span class="sxs-lookup"><span data-stu-id="dc946-172">Routes require you to add additional code.</span></span> <span data-ttu-id="dc946-173">在本教學課程中，您將使用模型系結來抓取使用資料控制項的資料產生路由時所使用的 `RouteValueDictionary` 物件。</span><span class="sxs-lookup"><span data-stu-id="dc946-173">In this tutorial, you will use model binding to retrieve a `RouteValueDictionary` object that is used when generating the routes using data from a data control.</span></span> <span data-ttu-id="dc946-174">`RouteValueDictionary` 物件將包含屬於特定產品類別的產品名稱清單。</span><span class="sxs-lookup"><span data-stu-id="dc946-174">The `RouteValueDictionary` object will contain a list of product names that belong to a specific category of products.</span></span> <span data-ttu-id="dc946-175">會根據資料和路線來建立每個產品的連結。</span><span class="sxs-lookup"><span data-stu-id="dc946-175">A link is created for each product based on the data and route.</span></span>

#### <a name="enable-routes-for-categories-and-products"></a><span data-ttu-id="dc946-176">啟用類別和產品的路由</span><span class="sxs-lookup"><span data-stu-id="dc946-176">Enable Routes for Categories and Products</span></span>

<span data-ttu-id="dc946-177">接下來，您將更新應用程式，以使用 `ProductsByCategoryRoute` 來決定要針對每個產品類別連結包含的正確路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-177">Next, you'll update the application to use the `ProductsByCategoryRoute` to determine the correct route to include for each product category link.</span></span> <span data-ttu-id="dc946-178">您也會更新 [ *ProductList* ] 頁面，以包含每個產品的路由連結。</span><span class="sxs-lookup"><span data-stu-id="dc946-178">You'll also update the *ProductList.aspx* page to include a routed link for each product.</span></span> <span data-ttu-id="dc946-179">這些連結會顯示在變更之前，不過連結現在會使用 URL 路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-179">The links will be displayed as they were before the change, however the links will now use URL routing.</span></span>

1. <span data-ttu-id="dc946-180">在**方案總管**中，開啟 [*網站*] 頁面（如果尚未開啟）。</span><span class="sxs-lookup"><span data-stu-id="dc946-180">In **Solution Explorer**, open the *Site.Master* page if it is not already open.</span></span>
2. <span data-ttu-id="dc946-181">將名為 "`categoryList`" 的**ListView**控制項更新為黃色反白顯示的變更，讓標記看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc946-181">Update the **ListView** control named "`categoryList`" with the changes highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample3.aspx?highlight=7-9)]
3. <span data-ttu-id="dc946-182">在**方案總管**中，開啟 [ *ProductList* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="dc946-182">In **Solution Explorer**, open the *ProductList.aspx* page.</span></span>
4. <span data-ttu-id="dc946-183">使用黃色反白顯示的更新來更新*ProductList*的 `ItemTemplate` 專案，讓標記看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="dc946-183">Update the `ItemTemplate` element of the *ProductList.aspx* page with the updates highlighted in yellow, so the markup appears as follows:</span></span>   

    [!code-aspx[Main](url-routing/samples/sample4.aspx?highlight=6-9,14-16)]
5. <span data-ttu-id="dc946-184">開啟*ProductList.aspx.cs*的程式碼後置，並新增下列命名空間（以黃色反白顯示）：</span><span class="sxs-lookup"><span data-stu-id="dc946-184">Open the code-behind of *ProductList.aspx.cs* and add the following namespace as highlighted in yellow:</span></span>  

    [!code-csharp[Main](url-routing/samples/sample5.cs?highlight=9)]
6. <span data-ttu-id="dc946-185">使用下列程式碼取代程式碼後置（*ProductList.aspx.cs*）的 `GetProducts` 方法：</span><span class="sxs-lookup"><span data-stu-id="dc946-185">Replace the `GetProducts` method of the code-behind (*ProductList.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample6.cs)]

#### <a name="add-code-for-product-details"></a><span data-ttu-id="dc946-186">新增產品詳細資料的程式碼</span><span class="sxs-lookup"><span data-stu-id="dc946-186">Add Code for Product Details</span></span>

<span data-ttu-id="dc946-187">現在，更新*ProductDetails*頁面的程式碼後置（*ProductDetails.aspx.cs*），以使用路由資料。</span><span class="sxs-lookup"><span data-stu-id="dc946-187">Now, update the code-behind (*ProductDetails.aspx.cs*) for the *ProductDetails.aspx* page to use route data.</span></span> <span data-ttu-id="dc946-188">請注意，新的 `GetProduct` 方法也會接受查詢字串值，在此案例中，使用者的連結會使用較舊的非易記、非路由 URL。</span><span class="sxs-lookup"><span data-stu-id="dc946-188">Notice that the new `GetProduct` method also accepts a query string value for the case where the user has a link bookmarked that uses the older non-friendly, non-routed URL.</span></span>

1. <span data-ttu-id="dc946-189">使用下列程式碼取代程式碼後置（*ProductDetails.aspx.cs*）的 `GetProduct` 方法：</span><span class="sxs-lookup"><span data-stu-id="dc946-189">Replace the `GetProduct` method of the code-behind (*ProductDetails.aspx.cs*) with the following code:</span></span>   

    [!code-csharp[Main](url-routing/samples/sample7.cs)]

## <a name="running-the-application"></a><span data-ttu-id="dc946-190">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="dc946-190">Running the Application</span></span>

<span data-ttu-id="dc946-191">您可以立即執行應用程式，以查看更新的路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-191">You can run the application now to see the updated routes.</span></span>

1. <span data-ttu-id="dc946-192">按**F5**執行 Wingtip 玩具範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="dc946-192">Press **F5** to run the Wingtip Toys sample application.</span></span>  
 <span data-ttu-id="dc946-193">瀏覽器會開啟並顯示*default.aspx*頁面。</span><span class="sxs-lookup"><span data-stu-id="dc946-193">The browser opens and shows the *Default.aspx* page.</span></span>
2. <span data-ttu-id="dc946-194">按一下頁面頂端的 [**產品**] 連結。</span><span class="sxs-lookup"><span data-stu-id="dc946-194">Click the **Products** link at the top of the page.</span></span>  
 <span data-ttu-id="dc946-195">所有產品都會顯示在 ProductList 的 [ *.aspx* ] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="dc946-195">All products are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="dc946-196">系統會顯示瀏覽器的下列 URL （使用您的埠號碼）：</span><span class="sxs-lookup"><span data-stu-id="dc946-196">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/ProductList`
3. <span data-ttu-id="dc946-197">接下來，按一下靠近頁面頂端的 [ **Cars** ] 類別連結。</span><span class="sxs-lookup"><span data-stu-id="dc946-197">Next, click the **Cars** category link near the top of the page.</span></span>  
 <span data-ttu-id="dc946-198">只有 cars 才會顯示在*ProductList*的 [.aspx] 頁面上。</span><span class="sxs-lookup"><span data-stu-id="dc946-198">Only cars are displayed on the *ProductList.aspx* page.</span></span> <span data-ttu-id="dc946-199">系統會顯示瀏覽器的下列 URL （使用您的埠號碼）：</span><span class="sxs-lookup"><span data-stu-id="dc946-199">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Category/Cars`
4. <span data-ttu-id="dc946-200">按一下包含頁面上所列第一個車輛名稱的連結（「可轉換的**車**」），以顯示產品詳細資料。</span><span class="sxs-lookup"><span data-stu-id="dc946-200">Click the link containing the name of the first car listed on the page ("**Convertible Car**") to display the product details.</span></span>  
 <span data-ttu-id="dc946-201">系統會顯示瀏覽器的下列 URL （使用您的埠號碼）：</span><span class="sxs-lookup"><span data-stu-id="dc946-201">The following URL (using your port number) is displayed for the browser:</span></span>  
    `https://localhost:44300/Product/Convertible%20Car`
5. <span data-ttu-id="dc946-202">接下來，在瀏覽器中輸入下列非路由 URL （使用您的埠號碼）：</span><span class="sxs-lookup"><span data-stu-id="dc946-202">Next, enter the following non-routed URL (using your port number) into the browser:</span></span>  
    `https://localhost:44300/ProductDetails.aspx?productID=2`  
 <span data-ttu-id="dc946-203">程式碼仍會辨識包含查詢字串的 URL，在此情況下，使用者會有已加入書簽的連結。</span><span class="sxs-lookup"><span data-stu-id="dc946-203">The code still recognizes a URL that includes a query string, for the case where a user has a link bookmarked.</span></span>

## <a name="summary"></a><span data-ttu-id="dc946-204">總結</span><span class="sxs-lookup"><span data-stu-id="dc946-204">Summary</span></span>

<span data-ttu-id="dc946-205">在本教學課程中，您已新增類別和產品的路由。</span><span class="sxs-lookup"><span data-stu-id="dc946-205">In this tutorial, you have added routes for categories and products.</span></span> <span data-ttu-id="dc946-206">您已瞭解如何將路由與使用模型系結的資料控制整合。</span><span class="sxs-lookup"><span data-stu-id="dc946-206">You have learned how routes can be integrated with data controls that use model binding.</span></span> <span data-ttu-id="dc946-207">在下一個教學課程中，您將會執行全域錯誤處理。</span><span class="sxs-lookup"><span data-stu-id="dc946-207">In the next tutorial, you will implement global error handling.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="dc946-208">其他資源</span><span class="sxs-lookup"><span data-stu-id="dc946-208">Additional Resources</span></span>

[<span data-ttu-id="dc946-209">ASP.NET 易記 Url</span><span class="sxs-lookup"><span data-stu-id="dc946-209">ASP.NET Friendly URLs</span></span>](http://www.nuget.org/packages/Microsoft.AspNet.FriendlyUrls/)  
[<span data-ttu-id="dc946-210">將具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET Web Forms 應用程式部署至 Azure App Service</span><span class="sxs-lookup"><span data-stu-id="dc946-210">Deploy a Secure ASP.NET Web Forms App with Membership, OAuth, and SQL Database to Azure App Service</span></span>](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-deploy-aspnet-webforms-app-membership-oauth-sql-database/)  
[<span data-ttu-id="dc946-211">Microsoft Azure 免費試用</span><span class="sxs-lookup"><span data-stu-id="dc946-211">Microsoft Azure - Free Trial</span></span>](https://azure.microsoft.com/pricing/free-trial/)

> [!div class="step-by-step"]
> <span data-ttu-id="dc946-212">[上一頁](membership-and-administration.md)
> [下一頁](aspnet-error-handling.md)</span><span class="sxs-lookup"><span data-stu-id="dc946-212">[Previous](membership-and-administration.md)
[Next](aspnet-error-handling.md)</span></span>
