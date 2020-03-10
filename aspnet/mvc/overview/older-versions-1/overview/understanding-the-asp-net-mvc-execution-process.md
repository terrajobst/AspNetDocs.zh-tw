---
uid: mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
title: 瞭解 ASP.NET MVC 執行程式 |Microsoft Docs
author: microsoft
description: 瞭解 ASP.NET MVC 架構如何逐步處理瀏覽器要求。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: d1608db3-660d-4079-8c15-f452ff01f1db
msc.legacyurl: /mvc/overview/older-versions-1/overview/understanding-the-asp-net-mvc-execution-process
msc.type: authoredcontent
ms.openlocfilehash: 28940947253e0af43886cf1231f8aaf4615526cc
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541514"
---
# <a name="understanding-the-aspnet-mvc-execution-process"></a><span data-ttu-id="41295-103">了解 ASP.NET MVC 執行程序</span><span class="sxs-lookup"><span data-stu-id="41295-103">Understanding the ASP.NET MVC Execution Process</span></span>

<span data-ttu-id="41295-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="41295-104">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="41295-105">瞭解 ASP.NET MVC 架構如何逐步處理瀏覽器要求。</span><span class="sxs-lookup"><span data-stu-id="41295-105">Learn how the ASP.NET MVC framework processes a browser request step-by-step.</span></span>

<span data-ttu-id="41295-106">ASP.NET MVC 型 Web 應用程式的要求會先通過**UrlRoutingModule**物件，也就是 HTTP 模組。</span><span class="sxs-lookup"><span data-stu-id="41295-106">Requests to an ASP.NET MVC-based Web application first pass through the **UrlRoutingModule** object, which is an HTTP module.</span></span> <span data-ttu-id="41295-107">此模組會剖析該要求並執行路由選取。</span><span class="sxs-lookup"><span data-stu-id="41295-107">This module parses the request and performs route selection.</span></span> <span data-ttu-id="41295-108">**UrlRoutingModule**物件會選取符合目前要求的第一個路由物件。</span><span class="sxs-lookup"><span data-stu-id="41295-108">The **UrlRoutingModule** object selects the first route object that matches the current request.</span></span> <span data-ttu-id="41295-109">（路由物件是可執行**RouteBase**的類別，通常是**路由**類別的實例）。如果沒有符合的路由， **UrlRoutingModule**物件就不會執行任何工作，而且會讓要求回到一般的 ASP.NET 或 IIS 要求處理。</span><span class="sxs-lookup"><span data-stu-id="41295-109">(A route object is a class that implements **RouteBase**, and is typically an instance of the **Route** class.) If no routes match, the **UrlRoutingModule** object does nothing and lets the request fall back to the regular ASP.NET or IIS request processing.</span></span>

<span data-ttu-id="41295-110">從選取的**路由**物件中， **UrlRoutingModule**物件會取得與**路由**物件相關聯的**IRouteHandler**物件。</span><span class="sxs-lookup"><span data-stu-id="41295-110">From the selected **Route** object, the **UrlRoutingModule** object obtains the **IRouteHandler** object that is associated with the **Route** object.</span></span> <span data-ttu-id="41295-111">一般來說，在 MVC 應用程式中，這會是**MvcRouteHandler**的實例。</span><span class="sxs-lookup"><span data-stu-id="41295-111">Typically, in an MVC application, this will be an instance of **MvcRouteHandler**.</span></span> <span data-ttu-id="41295-112">**IRouteHandler**實例會建立**IHttpHandler**物件，並將它傳遞至**IHttpCoNtext**物件。</span><span class="sxs-lookup"><span data-stu-id="41295-112">The **IRouteHandler** instance creates an **IHttpHandler** object and passes it the **IHttpContext** object.</span></span> <span data-ttu-id="41295-113">根據預設，MVC 的**IHttpHandler**實例是**MvcHandler**物件。</span><span class="sxs-lookup"><span data-stu-id="41295-113">By default, the **IHttpHandler** instance for MVC is the **MvcHandler** object.</span></span> <span data-ttu-id="41295-114">**MvcHandler**物件接著會選取最後會處理要求的控制器。</span><span class="sxs-lookup"><span data-stu-id="41295-114">The **MvcHandler** object then selects the controller that will ultimately handle the request.</span></span>

> [!NOTE]
> <span data-ttu-id="41295-115">當 ASP.NET MVC Web 應用程式在 IIS 7.0 中執行時，MVC 專案不需要副檔名。</span><span class="sxs-lookup"><span data-stu-id="41295-115">When an ASP.NET MVC Web application runs in IIS 7.0, no file name extension is required for MVC projects.</span></span> <span data-ttu-id="41295-116">然而，在 IIS 6.0 中，處理常式需要您將 .mvc 副檔名對應至 ASP.NET ISAPI DLL。</span><span class="sxs-lookup"><span data-stu-id="41295-116">However, in IIS 6.0, the handler requires that you map the .mvc file name extension to the ASP.NET ISAPI DLL.</span></span>

<span data-ttu-id="41295-117">模組和處理常式是 ASP.NET MVC 架構的進入點。</span><span class="sxs-lookup"><span data-stu-id="41295-117">The module and handler are the entry points to the ASP.NET MVC framework.</span></span> <span data-ttu-id="41295-118">它們會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="41295-118">They perform the following actions:</span></span>

- <span data-ttu-id="41295-119">選取 MVC Web 應用程式中適當的控制器。</span><span class="sxs-lookup"><span data-stu-id="41295-119">Select the appropriate controller in an MVC Web application.</span></span>
- <span data-ttu-id="41295-120">取得特定控制器執行個體。</span><span class="sxs-lookup"><span data-stu-id="41295-120">Obtain a specific controller instance.</span></span>
- <span data-ttu-id="41295-121">呼叫控制器的**Execute**方法。</span><span class="sxs-lookup"><span data-stu-id="41295-121">Call the controller's **Execute** method.</span></span>

<span data-ttu-id="41295-122">下列列出 MVC Web 專案的執行階段：</span><span class="sxs-lookup"><span data-stu-id="41295-122">The following lists the stages of execution for an MVC Web project:</span></span>

- <span data-ttu-id="41295-123">接收應用程式的第一個要求</span><span class="sxs-lookup"><span data-stu-id="41295-123">Receive first request for the application</span></span> 

    - <span data-ttu-id="41295-124">在 global.asax 檔案中，**路由**物件會新增至**RouteTable**物件。</span><span class="sxs-lookup"><span data-stu-id="41295-124">In the Global.asax file, **Route** objects are added to the **RouteTable** object.</span></span>
- <span data-ttu-id="41295-125">執行路由</span><span class="sxs-lookup"><span data-stu-id="41295-125">Perform routing</span></span> 

    - <span data-ttu-id="41295-126">**UrlRoutingModule**模組會使用**RouteTable**集合中的第一個相符**路由**物件來建立**RouteData**物件，然後用它來建立**RequestCoNtext** （**IHttpCoNtext**）物件。</span><span class="sxs-lookup"><span data-stu-id="41295-126">The **UrlRoutingModule** module uses the first matching **Route** object in the **RouteTable** collection to create the **RouteData** object, which it then uses to create a **RequestContext** (**IHttpContext**) object.</span></span>
- <span data-ttu-id="41295-127">建立 MVC 要求處理常式</span><span class="sxs-lookup"><span data-stu-id="41295-127">Create MVC request handler</span></span> 

    - <span data-ttu-id="41295-128">**MvcRouteHandler**物件會建立**MvcHandler**類別的實例，並將它傳遞至**RequestCoNtext**實例。</span><span class="sxs-lookup"><span data-stu-id="41295-128">The **MvcRouteHandler** object creates an instance of the **MvcHandler** class and passes it the **RequestContext** instance.</span></span>
- <span data-ttu-id="41295-129">建立控制器</span><span class="sxs-lookup"><span data-stu-id="41295-129">Create controller</span></span> 

    - <span data-ttu-id="41295-130">**MvcHandler**物件會使用**RequestCoNtext**實例來識別**IControllerFactory**物件（通常是**DefaultControllerFactory**類別的實例），以使用建立控制器實例。</span><span class="sxs-lookup"><span data-stu-id="41295-130">The **MvcHandler** object uses the **RequestContext** instance to identify the **IControllerFactory** object (typically an instance of the **DefaultControllerFactory** class) to create the controller instance with.</span></span>
- <span data-ttu-id="41295-131">執行控制器- **MvcHandler**實例會呼叫控制器 s**執行**方法。</span><span class="sxs-lookup"><span data-stu-id="41295-131">Execute controller - The **MvcHandler** instance calls the controller s **Execute** method.</span></span> |
- <span data-ttu-id="41295-132">叫用動作</span><span class="sxs-lookup"><span data-stu-id="41295-132">Invoke action</span></span> 

    - <span data-ttu-id="41295-133">大部分的控制器會繼承自**控制器**基類。</span><span class="sxs-lookup"><span data-stu-id="41295-133">Most controllers inherit from the **Controller** base class.</span></span> <span data-ttu-id="41295-134">對於執行這項操作的控制器而言，與控制器相關聯的**ControllerActionInvoker**物件會決定要呼叫控制器類別的哪一個動作方法，然後再呼叫該方法。</span><span class="sxs-lookup"><span data-stu-id="41295-134">For controllers that do so, the **ControllerActionInvoker** object that is associated with the controller determines which action method of the controller class to call, and then calls that method.</span></span>
- <span data-ttu-id="41295-135">執行結果</span><span class="sxs-lookup"><span data-stu-id="41295-135">Execute result</span></span> 

    - <span data-ttu-id="41295-136">一般動作方法可能會接收使用者輸入、準備適當的回應資料，然後藉由傳回結果類型來執行結果。</span><span class="sxs-lookup"><span data-stu-id="41295-136">A typical action method might receive user input, prepare the appropriate response data, and then execute the result by returning a result type.</span></span> <span data-ttu-id="41295-137">可以執行的內建結果類型包括下列各項： **ViewResult** （它會轉譯視圖，而是最常用的結果類型）、 **RedirectToRouteResult**、 **RedirectResult**、 **ContentResult**、 **JsonResult**和**EmptyResult**。</span><span class="sxs-lookup"><span data-stu-id="41295-137">The built-in result types that can be executed include the following: **ViewResult** (which renders a view and is the most-often used result type), **RedirectToRouteResult**, **RedirectResult**, **ContentResult**, **JsonResult**, and **EmptyResult**.</span></span>
