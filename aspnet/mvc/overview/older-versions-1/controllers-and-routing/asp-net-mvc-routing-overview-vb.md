---
uid: mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
title: ASP.NET MVC 路由總覽（VB） |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 會說明 ASP.NET MVC 架構如何將瀏覽器要求對應至控制器動作。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: 4bc8d19a-80f1-44b4-adbf-95ed22d691ca
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/asp-net-mvc-routing-overview-vb
msc.type: authoredcontent
ms.openlocfilehash: ed043d76b89ce31945cf3423b0c5afca9383cc21
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601532"
---
# <a name="aspnet-mvc-routing-overview-vb"></a><span data-ttu-id="3dc1a-103">ASP.NET MVC 路由概觀 (VB)</span><span class="sxs-lookup"><span data-stu-id="3dc1a-103">ASP.NET MVC Routing Overview (VB)</span></span>

<span data-ttu-id="3dc1a-104">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="3dc1a-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="3dc1a-105">在本教學課程中，Stephen Walther 會說明 ASP.NET MVC 架構如何將瀏覽器要求對應至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-105">In this tutorial, Stephen Walther shows how the ASP.NET MVC framework maps browser requests to controller actions.</span></span>

<span data-ttu-id="3dc1a-106">在本教學課程中，您會在每個名為*ASP.NET 路由*的 ASP.NET MVC 應用程式中引進一項重要功能。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-106">In this tutorial, you are introduced to an important feature of every ASP.NET MVC application called *ASP.NET Routing*.</span></span> <span data-ttu-id="3dc1a-107">ASP.NET 路由模組負責將傳入瀏覽器要求對應至特定的 MVC 控制器動作。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-107">The ASP.NET Routing module is responsible for mapping incoming browser requests to particular MVC controller actions.</span></span> <span data-ttu-id="3dc1a-108">本教學課程結束時，您將瞭解標準路由表如何將要求對應至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-108">By the end of this tutorial, you will understand how the standard route table maps requests to controller actions.</span></span>

## <a name="using-the-default-route-table"></a><span data-ttu-id="3dc1a-109">使用預設路由表</span><span class="sxs-lookup"><span data-stu-id="3dc1a-109">Using the Default Route Table</span></span>

<span data-ttu-id="3dc1a-110">當您建立新的 ASP.NET MVC 應用程式時，應用程式已設定為使用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-110">When you create a new ASP.NET MVC application, the application is already configured to use ASP.NET Routing.</span></span> <span data-ttu-id="3dc1a-111">ASP.NET 路由會在兩個地方設定。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-111">ASP.NET Routing is setup in two places.</span></span>

<span data-ttu-id="3dc1a-112">首先，會在應用程式的 Web 設定檔案（Web.config 檔案）中啟用 ASP.NET 路由。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-112">First, ASP.NET Routing is enabled in your application's Web configuration file (Web.config file).</span></span> <span data-ttu-id="3dc1a-113">與路由相關的設定檔中有四個區段： system.web. HTTPHandlers 區段、system.webserver 和 system.web 區段，以及 system.webserver. web. web. web.config 區段和 system.servicemodel。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-113">There are four sections in the configuration file that are relevant to routing: the system.web.httpModules section, the system.web.httpHandlers section, the system.webserver.modules section, and the system.webserver.handlers section.</span></span> <span data-ttu-id="3dc1a-114">請小心不要刪除這些區段，因為如果沒有這些區段，路由將不再有效。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-114">Be careful not to delete these sections because without these sections routing will no longer work.</span></span>

<span data-ttu-id="3dc1a-115">其次，更重要的是，在應用程式的 global.asax 檔案中建立路由表。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-115">Second, and more importantly, a route table is created in the application's Global.asax file.</span></span> <span data-ttu-id="3dc1a-116">Global.asax 檔案是特殊的檔案，其中包含 ASP.NET 應用程式週期事件的事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-116">The Global.asax file is a special file that contains event handlers for ASP.NET application lifecycle events.</span></span> <span data-ttu-id="3dc1a-117">在應用程式啟動事件期間，會建立路由表。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-117">The route table is created during the Application Start event.</span></span>

<span data-ttu-id="3dc1a-118">[清單 1] 中的檔案包含 ASP.NET MVC 應用程式的預設 global.asax 檔案。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-118">The file in Listing 1 contains the default Global.asax file for an ASP.NET MVC application.</span></span>

<span data-ttu-id="3dc1a-119">**清單 1-global.asax .vb**</span><span class="sxs-lookup"><span data-stu-id="3dc1a-119">**Listing 1 - Global.asax.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample1.vb)]

<span data-ttu-id="3dc1a-120">當 MVC 應用程式第一次啟動時，會呼叫應用程式\_Start （）方法。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-120">When an MVC application first starts, the Application\_Start() method is called.</span></span> <span data-ttu-id="3dc1a-121">這個方法接著會呼叫 RegisterRoutes （）方法。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-121">This method, in turn, calls the RegisterRoutes() method.</span></span> <span data-ttu-id="3dc1a-122">RegisterRoutes （）方法會建立路由表。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-122">The RegisterRoutes() method creates the route table.</span></span>

<span data-ttu-id="3dc1a-123">預設路由表包含單一路由（名為 Default）。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-123">The default route table contains a single route (named Default).</span></span> <span data-ttu-id="3dc1a-124">預設路由會將 URL 的第一個區段對應至控制器名稱、控制器動作 URL 的第二個區段，以及第三個區段到名為**id**的參數。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-124">The Default route maps the first segment of a URL to a controller name, the second segment of a URL to a controller action, and the third segment to a parameter named **id**.</span></span>

<span data-ttu-id="3dc1a-125">假設您在網頁瀏覽器的網址列中輸入下列 URL：</span><span class="sxs-lookup"><span data-stu-id="3dc1a-125">Imagine that you enter the following URL into your web browser's address bar:</span></span>

<span data-ttu-id="3dc1a-126">/Home/Index/3</span><span class="sxs-lookup"><span data-stu-id="3dc1a-126">/Home/Index/3</span></span>

<span data-ttu-id="3dc1a-127">預設路由會將此 URL 對應至下列參數：</span><span class="sxs-lookup"><span data-stu-id="3dc1a-127">The Default route maps this URL to the following parameters:</span></span>

- <span data-ttu-id="3dc1a-128">控制器 = 首頁</span><span class="sxs-lookup"><span data-stu-id="3dc1a-128">controller = Home</span></span>

- <span data-ttu-id="3dc1a-129">action = 索引</span><span class="sxs-lookup"><span data-stu-id="3dc1a-129">action = Index</span></span>

- <span data-ttu-id="3dc1a-130">識別碼 = 3</span><span class="sxs-lookup"><span data-stu-id="3dc1a-130">id = 3</span></span>

<span data-ttu-id="3dc1a-131">當您要求 URL/Home/Index/3 時，會執行下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="3dc1a-131">When you request the URL /Home/Index/3, the following code is executed:</span></span>

<span data-ttu-id="3dc1a-132">HomeController。 Index （3）</span><span class="sxs-lookup"><span data-stu-id="3dc1a-132">HomeController.Index(3)</span></span>

<span data-ttu-id="3dc1a-133">預設路由會包含所有三個參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-133">The Default route includes defaults for all three parameters.</span></span> <span data-ttu-id="3dc1a-134">如果您未提供控制器，則控制器參數的預設值為**Home**。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-134">If you don't supply a controller, then the controller parameter defaults to the value **Home**.</span></span> <span data-ttu-id="3dc1a-135">如果您未提供動作，動作參數會預設為值**索引**。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-135">If you don't supply an action, the action parameter defaults to the value **Index**.</span></span> <span data-ttu-id="3dc1a-136">最後，如果您未提供識別碼，則 id 參數會預設為空字串。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-136">Finally, if you don't supply an id, the id parameter defaults to an empty string.</span></span>

<span data-ttu-id="3dc1a-137">讓我們看看一些範例，說明預設路由如何將 Url 對應至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-137">Let's look at a few examples of how the Default route maps URLs to controller actions.</span></span> <span data-ttu-id="3dc1a-138">假設您在瀏覽器網址列中輸入下列 URL：</span><span class="sxs-lookup"><span data-stu-id="3dc1a-138">Imagine that you enter the following URL into your browser address bar:</span></span>

<span data-ttu-id="3dc1a-139">/Home</span><span class="sxs-lookup"><span data-stu-id="3dc1a-139">/Home</span></span>

<span data-ttu-id="3dc1a-140">基於預設路由參數預設值，輸入此 URL 將會呼叫 [清單 2] 中 HomeController 類別的 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-140">Because of the Default route parameter defaults, entering this URL will cause the Index() method of the HomeController class in Listing 2 to be called.</span></span>

<span data-ttu-id="3dc1a-141">**清單 2-HomeController .vb**</span><span class="sxs-lookup"><span data-stu-id="3dc1a-141">**Listing 2 - HomeController.vb**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample2.vb)]

<span data-ttu-id="3dc1a-142">在 [清單 2] 中，HomeController 類別包含名為 Index （）的方法，它會接受名為 Id 的單一參數。URL/Home 會使 Index （）方法以值「無」做為 Id 參數的值來呼叫。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-142">In Listing 2, the HomeController class includes a method named Index() that accepts a single parameter named Id. The URL /Home causes the Index() method to be called with the value Nothing as the value of the Id parameter.</span></span>

<span data-ttu-id="3dc1a-143">由於 MVC 架構會叫用控制器動作的方式，因此 URL/Home 也會符合 [清單 3] 中 HomeController 類別的 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-143">Because of the way that the MVC framework invokes controller actions, the URL /Home also matches the Index() method of the HomeController class in Listing 3.</span></span>

<span data-ttu-id="3dc1a-144">**清單 3-HomeController （不含參數的索引動作）**</span><span class="sxs-lookup"><span data-stu-id="3dc1a-144">**Listing 3 - HomeController.vb (Index action with no parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample3.vb)]

<span data-ttu-id="3dc1a-145">[清單 3] 中的 Index （）方法不接受任何參數。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-145">The Index() method in Listing 3 does not accept any parameters.</span></span> <span data-ttu-id="3dc1a-146">URL/Home 會導致呼叫這個 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-146">The URL /Home will cause this Index() method to be called.</span></span> <span data-ttu-id="3dc1a-147">URL/Home/Index/3 也會叫用這個方法（忽略識別碼）。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-147">The URL /Home/Index/3 also invokes this method (the Id is ignored).</span></span>

<span data-ttu-id="3dc1a-148">URL/Home 也符合清單4中 HomeController 類別的 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-148">The URL /Home also matches the Index() method of the HomeController class in Listing 4.</span></span>

<span data-ttu-id="3dc1a-149">**清單 4-HomeController （具有可為 null 參數的索引動作）**</span><span class="sxs-lookup"><span data-stu-id="3dc1a-149">**Listing 4 - HomeController.vb (Index action with nullable parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample4.vb)]

<span data-ttu-id="3dc1a-150">在 [清單 4] 中，Index （）方法有一個整數參數。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-150">In Listing 4, the Index() method has one Integer parameter.</span></span> <span data-ttu-id="3dc1a-151">因為參數是可為 null 的參數（可以有值「無」），所以可以呼叫索引（），而不會引發錯誤。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-151">Because the parameter is a nullable parameter (can have the value Nothing), the Index() can be called without raising an error.</span></span>

<span data-ttu-id="3dc1a-152">最後，使用 URL/Home 叫用清單5中的 Index （）方法會造成例外狀況，因為 Id 參數*不是*可為 null 的參數。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-152">Finally, invoking the Index() method in Listing 5 with the URL /Home causes an exception since the Id parameter *is not* a nullable parameter.</span></span> <span data-ttu-id="3dc1a-153">如果您嘗試叫用 Index （）方法，就會得到 [圖 1] 所示的錯誤。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-153">If you attempt to invoke the Index() method then you get the error displayed in Figure 1.</span></span>

<span data-ttu-id="3dc1a-154">**清單 5-HomeController （識別碼參數的索引動作）**</span><span class="sxs-lookup"><span data-stu-id="3dc1a-154">**Listing 5 - HomeController.vb (Index action with Id parameter)**</span></span>

[!code-vb[Main](asp-net-mvc-routing-overview-vb/samples/sample5.vb)]

<span data-ttu-id="3dc1a-155">[![叫用需要參數值的控制器動作](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3dc1a-155">[![Invoking a controller action that expects a parameter value](asp-net-mvc-routing-overview-vb/_static/image1.jpg)](asp-net-mvc-routing-overview-vb/_static/image1.png)</span></span>

<span data-ttu-id="3dc1a-156">**圖 01**：叫用需要參數值的控制器動作（[按一下以查看完整大小的影像](asp-net-mvc-routing-overview-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="3dc1a-156">**Figure 01**: Invoking a controller action that expects a parameter value ([Click to view full-size image](asp-net-mvc-routing-overview-vb/_static/image2.png))</span></span>

<span data-ttu-id="3dc1a-157">另一方面，URL/Home/Index/3 的運作方式與 [清單 5] 中的索引控制器動作沒什麼關係。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-157">The URL /Home/Index/3, on the other hand, works just fine with the Index controller action in Listing 5.</span></span> <span data-ttu-id="3dc1a-158">要求/Home/Index/3 會導致使用值3的 Id 參數來呼叫 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-158">The request /Home/Index/3 causes the Index() method to be called with an Id parameter that has the value 3.</span></span>

## <a name="summary"></a><span data-ttu-id="3dc1a-159">總結</span><span class="sxs-lookup"><span data-stu-id="3dc1a-159">Summary</span></span>

<span data-ttu-id="3dc1a-160">本教學課程的目的是為您提供 ASP.NET 路由的簡介。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-160">The goal of this tutorial was to provide you with a brief introduction to ASP.NET Routing.</span></span> <span data-ttu-id="3dc1a-161">我們檢查了您使用新的 ASP.NET MVC 應用程式取得的預設路由表。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-161">We examined the default route table that you get with a new ASP.NET MVC application.</span></span> <span data-ttu-id="3dc1a-162">您已瞭解預設路由如何將 Url 對應至控制器動作。</span><span class="sxs-lookup"><span data-stu-id="3dc1a-162">You learned how the default route maps URLs to controller actions.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3dc1a-163">[上一頁](creating-an-action-cs.md)
> [下一頁](understanding-action-filters-vb.md)</span><span class="sxs-lookup"><span data-stu-id="3dc1a-163">[Previous](creating-an-action-cs.md)
[Next](understanding-action-filters-vb.md)</span></span>
