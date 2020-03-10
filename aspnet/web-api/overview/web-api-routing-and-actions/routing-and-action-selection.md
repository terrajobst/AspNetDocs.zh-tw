---
uid: web-api/overview/web-api-routing-and-actions/routing-and-action-selection
title: ASP.NET Web API 中的路由和動作選取 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 12/14/2018
ms.assetid: bcf2d223-cb7f-411e-be05-f43e96a14015
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-and-action-selection
msc.type: authoredcontent
ms.openlocfilehash: 62114e56fb29e80c93b82dcb78ce2bc2a123a83b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554884"
---
# <a name="routing-and-action-selection-in-aspnet-web-api"></a><span data-ttu-id="19d1d-102">ASP.NET Web API 中的路由和動作選取</span><span class="sxs-lookup"><span data-stu-id="19d1d-102">Routing and Action Selection in ASP.NET Web API</span></span>

<span data-ttu-id="19d1d-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="19d1d-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="19d1d-104">本文說明 ASP.NET Web API 如何將 HTTP 要求路由至控制器上的特定動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-104">This article describes how ASP.NET Web API routes an HTTP request to a particular action on a controller.</span></span>

> [!NOTE]
> <span data-ttu-id="19d1d-105">如需路由的高階總覽，請參閱[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="19d1d-105">For a high-level overview of routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="19d1d-106">本文將探討路由程式的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="19d1d-106">This article looks at the details of the routing process.</span></span> <span data-ttu-id="19d1d-107">如果您建立 Web API 專案，併發現某些要求不會以您預期的方式路由傳送，希望本文有助。</span><span class="sxs-lookup"><span data-stu-id="19d1d-107">If you create a Web API project and find that some requests don't get routed the way you expect, hopefully this article will help.</span></span>

<span data-ttu-id="19d1d-108">路由有三個主要階段：</span><span class="sxs-lookup"><span data-stu-id="19d1d-108">Routing has three main phases:</span></span>

1. <span data-ttu-id="19d1d-109">符合路由範本的 URI。</span><span class="sxs-lookup"><span data-stu-id="19d1d-109">Matching the URI to a route template.</span></span>
2. <span data-ttu-id="19d1d-110">選取控制器。</span><span class="sxs-lookup"><span data-stu-id="19d1d-110">Selecting a controller.</span></span>
3. <span data-ttu-id="19d1d-111">選取動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-111">Selecting an action.</span></span>

<span data-ttu-id="19d1d-112">您可以使用自己的自訂行為來取代進程的某些部分。</span><span class="sxs-lookup"><span data-stu-id="19d1d-112">You can replace some parts of the process with your own custom behaviors.</span></span> <span data-ttu-id="19d1d-113">在本文中，我將說明預設行為。</span><span class="sxs-lookup"><span data-stu-id="19d1d-113">In this article, I describe the default behavior.</span></span> <span data-ttu-id="19d1d-114">最後，我會注意到您可以自訂行為的地方。</span><span class="sxs-lookup"><span data-stu-id="19d1d-114">At the end, I note the places where you can customize the behavior.</span></span>

## <a name="route-templates"></a><span data-ttu-id="19d1d-115">路由範本</span><span class="sxs-lookup"><span data-stu-id="19d1d-115">Route Templates</span></span>

<span data-ttu-id="19d1d-116">路由範本看起來類似 URI 路徑，但它可以有預留位置值，以大括弧表示：</span><span class="sxs-lookup"><span data-stu-id="19d1d-116">A route template looks similar to a URI path, but it can have placeholder values, indicated with curly braces:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample1.ps1)]

<span data-ttu-id="19d1d-117">當您建立路由時，可以為部分或所有預留位置提供預設值：</span><span class="sxs-lookup"><span data-stu-id="19d1d-117">When you create a route, you can provide default values for some or all of the placeholders:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample2.cs)]

<span data-ttu-id="19d1d-118">您也可以提供條件約束，以限制 URI 區段可以符合預留位置的方式：</span><span class="sxs-lookup"><span data-stu-id="19d1d-118">You can also provide constraints, which restrict how a URI segment can match a placeholder:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample3.js)]

<span data-ttu-id="19d1d-119">架構會嘗試將 URI 路徑中的區段與範本比對。</span><span class="sxs-lookup"><span data-stu-id="19d1d-119">The framework tries to match the segments in the URI path to the template.</span></span> <span data-ttu-id="19d1d-120">範本中的常值必須完全相符。</span><span class="sxs-lookup"><span data-stu-id="19d1d-120">Literals in the template must match exactly.</span></span> <span data-ttu-id="19d1d-121">除非您指定條件約束，否則預留位置會符合任何值。</span><span class="sxs-lookup"><span data-stu-id="19d1d-121">A placeholder matches any value, unless you specify constraints.</span></span> <span data-ttu-id="19d1d-122">架構不符合 URI 的其他部分，例如主機名稱或查詢參數。</span><span class="sxs-lookup"><span data-stu-id="19d1d-122">The framework does not match other parts of the URI, such as the host name or the query parameters.</span></span> <span data-ttu-id="19d1d-123">架構會選取路由表中符合 URI 的第一個路由。</span><span class="sxs-lookup"><span data-stu-id="19d1d-123">The framework selects the first route in the route table that matches the URI.</span></span>

<span data-ttu-id="19d1d-124">有兩個特殊的預留位置： "{controller}" 和 "{action}"。</span><span class="sxs-lookup"><span data-stu-id="19d1d-124">There are two special placeholders: "{controller}" and "{action}".</span></span>

- <span data-ttu-id="19d1d-125">"{controller}" 提供控制器的名稱。</span><span class="sxs-lookup"><span data-stu-id="19d1d-125">"{controller}" provides the name of the controller.</span></span>
- <span data-ttu-id="19d1d-126">"{action}" 提供動作的名稱。</span><span class="sxs-lookup"><span data-stu-id="19d1d-126">"{action}" provides the name of the action.</span></span> <span data-ttu-id="19d1d-127">在 Web API 中，一般的慣例是省略 "{action}"。</span><span class="sxs-lookup"><span data-stu-id="19d1d-127">In Web API, the usual convention is to omit "{action}".</span></span>

### <a name="defaults"></a><span data-ttu-id="19d1d-128">預設值</span><span class="sxs-lookup"><span data-stu-id="19d1d-128">Defaults</span></span>

<span data-ttu-id="19d1d-129">如果您提供預設值，則路由會符合遺漏這些區段的 URI。</span><span class="sxs-lookup"><span data-stu-id="19d1d-129">If you provide defaults, the route will match a URI that is missing those segments.</span></span> <span data-ttu-id="19d1d-130">例如:</span><span class="sxs-lookup"><span data-stu-id="19d1d-130">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample4.cs)]

<span data-ttu-id="19d1d-131">Uri `http://localhost/api/products/all`，`http://localhost/api/products` 符合先前的路由。</span><span class="sxs-lookup"><span data-stu-id="19d1d-131">The URIs `http://localhost/api/products/all` and `http://localhost/api/products` match the preceding route.</span></span> <span data-ttu-id="19d1d-132">在後面的 URI 中，遺漏的 `{category}` 區段會被指派預設值 `all`。</span><span class="sxs-lookup"><span data-stu-id="19d1d-132">In the latter URI, the missing `{category}` segment is assigned the default value `all`.</span></span>

### <a name="route-dictionary"></a><span data-ttu-id="19d1d-133">路由字典</span><span class="sxs-lookup"><span data-stu-id="19d1d-133">Route Dictionary</span></span>

<span data-ttu-id="19d1d-134">如果架構找到 URI 的相符項，它會建立一個包含每個預留位置值的字典。</span><span class="sxs-lookup"><span data-stu-id="19d1d-134">If the framework finds a match for a URI, it creates a dictionary that contains the value for each placeholder.</span></span> <span data-ttu-id="19d1d-135">這些索引鍵是預留位置名稱，不包含大括弧。</span><span class="sxs-lookup"><span data-stu-id="19d1d-135">The keys are the placeholder names, not including the curly braces.</span></span> <span data-ttu-id="19d1d-136">值取自 URI 路徑，或來自預設值。</span><span class="sxs-lookup"><span data-stu-id="19d1d-136">The values are taken from the URI path or from the defaults.</span></span> <span data-ttu-id="19d1d-137">字典會儲存在**IHttpRouteData**物件中。</span><span class="sxs-lookup"><span data-stu-id="19d1d-137">The dictionary is stored in the **IHttpRouteData** object.</span></span>

<span data-ttu-id="19d1d-138">在此路由比對階段期間，特殊的 "{controller}" 和 "{action}" 預留位置的處理方式就像其他預留位置一樣。</span><span class="sxs-lookup"><span data-stu-id="19d1d-138">During this route-matching phase, the special "{controller}" and "{action}" placeholders are treated just like the other placeholders.</span></span> <span data-ttu-id="19d1d-139">它們只會與其他值一起儲存在字典中。</span><span class="sxs-lookup"><span data-stu-id="19d1d-139">They are simply stored in the dictionary with the other values.</span></span>

<span data-ttu-id="19d1d-140">預設值可以是選擇性的**RouteParameter**。</span><span class="sxs-lookup"><span data-stu-id="19d1d-140">A default can have the special value **RouteParameter.Optional**.</span></span> <span data-ttu-id="19d1d-141">如果將此值指派給預留位置，此值就不會加入至路由字典。</span><span class="sxs-lookup"><span data-stu-id="19d1d-141">If a placeholder gets assigned this value, the value is not added to the route dictionary.</span></span> <span data-ttu-id="19d1d-142">例如:</span><span class="sxs-lookup"><span data-stu-id="19d1d-142">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample5.cs)]

<span data-ttu-id="19d1d-143">對於 URI 路徑「api/產品」，路由字典會包含：</span><span class="sxs-lookup"><span data-stu-id="19d1d-143">For the URI path "api/products", the route dictionary will contain:</span></span>

- <span data-ttu-id="19d1d-144">控制器：「產品」</span><span class="sxs-lookup"><span data-stu-id="19d1d-144">controller: "products"</span></span>
- <span data-ttu-id="19d1d-145">類別：「全部」</span><span class="sxs-lookup"><span data-stu-id="19d1d-145">category: "all"</span></span>

<span data-ttu-id="19d1d-146">不過，對於「api/產品/玩具/123」，路由字典將包含：</span><span class="sxs-lookup"><span data-stu-id="19d1d-146">For "api/products/toys/123", however, the route dictionary will contain:</span></span>

- <span data-ttu-id="19d1d-147">控制器：「產品」</span><span class="sxs-lookup"><span data-stu-id="19d1d-147">controller: "products"</span></span>
- <span data-ttu-id="19d1d-148">類別：「玩具」</span><span class="sxs-lookup"><span data-stu-id="19d1d-148">category: "toys"</span></span>
- <span data-ttu-id="19d1d-149">識別碼： "123"</span><span class="sxs-lookup"><span data-stu-id="19d1d-149">id: "123"</span></span>

<span data-ttu-id="19d1d-150">預設值也可以包含不會出現在路由範本中任何位置的值。</span><span class="sxs-lookup"><span data-stu-id="19d1d-150">The defaults can also include a value that does not appear anywhere in the route template.</span></span> <span data-ttu-id="19d1d-151">如果路由符合，該值會儲存在字典中。</span><span class="sxs-lookup"><span data-stu-id="19d1d-151">If the route matches, that value is stored in the dictionary.</span></span> <span data-ttu-id="19d1d-152">例如:</span><span class="sxs-lookup"><span data-stu-id="19d1d-152">For example:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample6.cs)]

<span data-ttu-id="19d1d-153">如果 URI 路徑為 "api/root/8"，則字典會包含兩個值：</span><span class="sxs-lookup"><span data-stu-id="19d1d-153">If the URI path is "api/root/8", the dictionary will contain two values:</span></span>

- <span data-ttu-id="19d1d-154">控制器：「客戶」</span><span class="sxs-lookup"><span data-stu-id="19d1d-154">controller: "customers"</span></span>
- <span data-ttu-id="19d1d-155">識別碼： "8"</span><span class="sxs-lookup"><span data-stu-id="19d1d-155">id: "8"</span></span>

## <a name="selecting-a-controller"></a><span data-ttu-id="19d1d-156">選取控制器</span><span class="sxs-lookup"><span data-stu-id="19d1d-156">Selecting a Controller</span></span>

<span data-ttu-id="19d1d-157">控制器選取會由**IHttpControllerSelector. SelectController**方法處理。</span><span class="sxs-lookup"><span data-stu-id="19d1d-157">Controller selection is handled by the **IHttpControllerSelector.SelectController** method.</span></span> <span data-ttu-id="19d1d-158">這個方法會採用**HttpRequestMessage**實例，並傳回**HttpControllerDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="19d1d-158">This method takes an **HttpRequestMessage** instance and returns an **HttpControllerDescriptor**.</span></span> <span data-ttu-id="19d1d-159">預設的執行是由**DefaultHttpControllerSelector**類別所提供。</span><span class="sxs-lookup"><span data-stu-id="19d1d-159">The default implementation is provided by the **DefaultHttpControllerSelector** class.</span></span> <span data-ttu-id="19d1d-160">這個類別會使用簡單的演算法：</span><span class="sxs-lookup"><span data-stu-id="19d1d-160">This class uses a straightforward algorithm:</span></span>

1. <span data-ttu-id="19d1d-161">查看索引鍵 "controller" 的路由字典。</span><span class="sxs-lookup"><span data-stu-id="19d1d-161">Look in the route dictionary for the key "controller".</span></span>
2. <span data-ttu-id="19d1d-162">取得此索引鍵的值，然後附加字串 "Controller" 以取得控制器類型名稱。</span><span class="sxs-lookup"><span data-stu-id="19d1d-162">Take the value for this key and append the string "Controller" to get the controller type name.</span></span>
3. <span data-ttu-id="19d1d-163">尋找此類型名稱為的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="19d1d-163">Look for a Web API controller with this type name.</span></span>

<span data-ttu-id="19d1d-164">例如，如果路由字典包含機碼值組 "controller" = "products"，則控制器類型為 "Productscontroller.cs"。</span><span class="sxs-lookup"><span data-stu-id="19d1d-164">For example, if the route dictionary contains the key-value pair "controller" = "products", then the controller type is "ProductsController".</span></span> <span data-ttu-id="19d1d-165">如果沒有相符的類型或多個相符專案，架構會將錯誤傳回給用戶端。</span><span class="sxs-lookup"><span data-stu-id="19d1d-165">If there is no matching type, or multiple matches, the framework returns an error to the client.</span></span>

<span data-ttu-id="19d1d-166">在步驟3中， **DefaultHttpControllerSelector**會使用**IHttpControllerTypeResolver**介面來取得 Web API 控制器類型的清單。</span><span class="sxs-lookup"><span data-stu-id="19d1d-166">For step 3, **DefaultHttpControllerSelector** uses the **IHttpControllerTypeResolver** interface to get the list of Web API controller types.</span></span> <span data-ttu-id="19d1d-167">**IHttpControllerTypeResolver**的預設執行會傳回（a）實**IHttpController**的所有公用類別，（b）不是抽象的，而（c）的名稱會以 "Controller" 結尾。</span><span class="sxs-lookup"><span data-stu-id="19d1d-167">The default implementation of **IHttpControllerTypeResolver** returns all public classes that (a) implement **IHttpController**, (b) are not abstract, and (c) have a name that ends in "Controller".</span></span>

## <a name="action-selection"></a><span data-ttu-id="19d1d-168">動作選取</span><span class="sxs-lookup"><span data-stu-id="19d1d-168">Action Selection</span></span>

<span data-ttu-id="19d1d-169">選取控制器之後，架構會藉由呼叫**IHttpActionSelector. SelectAction**方法來選取動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-169">After selecting the controller, the framework selects the action by calling the **IHttpActionSelector.SelectAction** method.</span></span> <span data-ttu-id="19d1d-170">這個方法會採用**system.web.HTTP.controllers.HTTPcontrollercoNtext** ，並傳回**HttpActionDescriptor**。</span><span class="sxs-lookup"><span data-stu-id="19d1d-170">This method takes an **HttpControllerContext** and returns an **HttpActionDescriptor**.</span></span>

<span data-ttu-id="19d1d-171">預設的執行是由**ApiControllerActionSelector**類別所提供。</span><span class="sxs-lookup"><span data-stu-id="19d1d-171">The default implementation is provided by the **ApiControllerActionSelector** class.</span></span> <span data-ttu-id="19d1d-172">若要選取動作，它會查看下列內容：</span><span class="sxs-lookup"><span data-stu-id="19d1d-172">To select an action, it looks at the following:</span></span>

- <span data-ttu-id="19d1d-173">要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="19d1d-173">The HTTP method of the request.</span></span>
- <span data-ttu-id="19d1d-174">路由範本中的 "{action}" 預留位置（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="19d1d-174">The "{action}" placeholder in the route template, if present.</span></span>
- <span data-ttu-id="19d1d-175">控制器上動作的參數。</span><span class="sxs-lookup"><span data-stu-id="19d1d-175">The parameters of the actions on the controller.</span></span>

<span data-ttu-id="19d1d-176">在查看選取演算法之前，我們必須先瞭解控制器動作的一些相關事項。</span><span class="sxs-lookup"><span data-stu-id="19d1d-176">Before looking at the selection algorithm, we need to understand some things about controller actions.</span></span>

<span data-ttu-id="19d1d-177">**控制器上的哪些方法會被視為「動作」？**</span><span class="sxs-lookup"><span data-stu-id="19d1d-177">**Which methods on the controller are considered "actions"?**</span></span> <span data-ttu-id="19d1d-178">選取動作時，架構只會查看控制器上的公用實例方法。</span><span class="sxs-lookup"><span data-stu-id="19d1d-178">When selecting an action, the framework only looks at public instance methods on the controller.</span></span> <span data-ttu-id="19d1d-179">此外，它也排除了「[特殊名稱](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname)」方法（例如，多載、事件、運算子多載等等），以及繼承自**ApiController**類別的方法。</span><span class="sxs-lookup"><span data-stu-id="19d1d-179">Also, it excludes ["special name"](https://msdn.microsoft.com/library/system.reflection.methodbase.isspecialname) methods (constructors, events, operator overloads, and so forth), and methods inherited from the **ApiController** class.</span></span>

<span data-ttu-id="19d1d-180">**HTTP 方法。**</span><span class="sxs-lookup"><span data-stu-id="19d1d-180">**HTTP Methods.**</span></span> <span data-ttu-id="19d1d-181">架構只會選擇符合要求之 HTTP 方法的動作，如下所示：</span><span class="sxs-lookup"><span data-stu-id="19d1d-181">The framework only chooses actions that match the HTTP method of the request, determined as follows:</span></span>

1. <span data-ttu-id="19d1d-182">您可以使用屬性指定 HTTP 方法： **AcceptVerbs**、 **HttpDelete**、 **HttpGet**、 **HttpHead**、 **HttpOptions**、 **HttpPatch**、 **HttpPost**或**HttpPut**。</span><span class="sxs-lookup"><span data-stu-id="19d1d-182">You can specify the HTTP method with an attribute: **AcceptVerbs**, **HttpDelete**, **HttpGet**, **HttpHead**, **HttpOptions**, **HttpPatch**, **HttpPost**, or **HttpPut**.</span></span>
2. <span data-ttu-id="19d1d-183">否則，如果控制器方法的名稱開頭為 "Get"、"Post"、"Put"、"Delete"、"Head"、"Options" 或 "Patch"，則依照慣例，動作會支援該 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="19d1d-183">Otherwise, if the name of the controller method starts with "Get", "Post", "Put", "Delete", "Head", "Options", or "Patch", then by convention the action supports that HTTP method.</span></span>
3. <span data-ttu-id="19d1d-184">如果以上皆非，則方法支援 POST。</span><span class="sxs-lookup"><span data-stu-id="19d1d-184">If none of the above, the method supports POST.</span></span>

<span data-ttu-id="19d1d-185">**參數系結。**</span><span class="sxs-lookup"><span data-stu-id="19d1d-185">**Parameter Bindings.**</span></span> <span data-ttu-id="19d1d-186">參數系結是 Web API 為參數建立值的方式。</span><span class="sxs-lookup"><span data-stu-id="19d1d-186">A parameter binding is how Web API creates a value for a parameter.</span></span> <span data-ttu-id="19d1d-187">以下是參數系結的預設規則：</span><span class="sxs-lookup"><span data-stu-id="19d1d-187">Here is the default rule for parameter binding:</span></span>

- <span data-ttu-id="19d1d-188">簡單類型取自 URI。</span><span class="sxs-lookup"><span data-stu-id="19d1d-188">Simple types are taken from the URI.</span></span>
- <span data-ttu-id="19d1d-189">複雜型別取自要求主體。</span><span class="sxs-lookup"><span data-stu-id="19d1d-189">Complex types are taken from the request body.</span></span>

<span data-ttu-id="19d1d-190">簡單類型包括所有[.NET Framework](https://msdn.microsoft.com/library/system.type.isprimitive)基本型別，加上**DateTime**、 **Decimal**、 **Guid**、 **String**和**TimeSpan**。</span><span class="sxs-lookup"><span data-stu-id="19d1d-190">Simple types include all of the [.NET Framework primitive types](https://msdn.microsoft.com/library/system.type.isprimitive), plus **DateTime**, **Decimal**, **Guid**, **String**, and **TimeSpan**.</span></span> <span data-ttu-id="19d1d-191">針對每個動作，最多隻能有一個參數讀取要求主體。</span><span class="sxs-lookup"><span data-stu-id="19d1d-191">For each action, at most one parameter can read the request body.</span></span>

> [!NOTE]
> <span data-ttu-id="19d1d-192">您可以覆寫預設的系結規則。</span><span class="sxs-lookup"><span data-stu-id="19d1d-192">It is possible to override the default binding rules.</span></span> <span data-ttu-id="19d1d-193">請參閱幕後[的 WebAPI 參數](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)系結。</span><span class="sxs-lookup"><span data-stu-id="19d1d-193">See [WebAPI Parameter binding under the hood](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx).</span></span>

<span data-ttu-id="19d1d-194">在該背景中，以下是動作選取演算法。</span><span class="sxs-lookup"><span data-stu-id="19d1d-194">With that background, here is the action selection algorithm.</span></span>

1. <span data-ttu-id="19d1d-195">在控制器上建立符合 HTTP 要求方法的所有動作清單。</span><span class="sxs-lookup"><span data-stu-id="19d1d-195">Create a list of all actions on the controller that match the HTTP request method.</span></span>
2. <span data-ttu-id="19d1d-196">如果路由字典有「動作」專案，請移除名稱不符合此值的動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-196">If the route dictionary has an "action" entry, remove actions whose name does not match this value.</span></span>
3. <span data-ttu-id="19d1d-197">請嘗試比對動作參數與 URI，如下所示：</span><span class="sxs-lookup"><span data-stu-id="19d1d-197">Try to match action parameters to the URI, as follows:</span></span> 

    1. <span data-ttu-id="19d1d-198">針對每個動作，取得簡單類型的參數清單，其中系結會從 URI 取得參數。</span><span class="sxs-lookup"><span data-stu-id="19d1d-198">For each action, get a list of the parameters that are a simple type, where the binding gets the parameter from the URI.</span></span> <span data-ttu-id="19d1d-199">排除選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="19d1d-199">Exclude optional parameters.</span></span>
    2. <span data-ttu-id="19d1d-200">從這份清單中，嘗試尋找每個參數名稱的相符項，不論是在路由字典中，或在 URI 查詢字串中。</span><span class="sxs-lookup"><span data-stu-id="19d1d-200">From this list, try to find a match for each parameter name, either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="19d1d-201">相符專案不區分大小寫，且不會相依于參數順序。</span><span class="sxs-lookup"><span data-stu-id="19d1d-201">Matches are case insensitive and do not depend on the parameter order.</span></span>
    3. <span data-ttu-id="19d1d-202">選取動作，其中清單中的每個參數在 URI 中都有相符的。</span><span class="sxs-lookup"><span data-stu-id="19d1d-202">Select an action where every parameter in the list has a match in the URI.</span></span>
    4. <span data-ttu-id="19d1d-203">如果有更多動作符合這些準則，請挑選其中一個包含最多參數的相符專案。</span><span class="sxs-lookup"><span data-stu-id="19d1d-203">If more that one action meets these criteria, pick the one with the most parameter matches.</span></span>
4. <span data-ttu-id="19d1d-204">忽略具有 **[請以 nonaction]** 屬性的動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-204">Ignore actions with the **[NonAction]** attribute.</span></span>

<span data-ttu-id="19d1d-205">步驟 #3 可能是最令人困惑的。</span><span class="sxs-lookup"><span data-stu-id="19d1d-205">Step #3 is probably the most confusing.</span></span> <span data-ttu-id="19d1d-206">基本概念是，參數可以從 URI、要求主體或自訂系結取得其值。</span><span class="sxs-lookup"><span data-stu-id="19d1d-206">The basic idea is that a parameter can get its value either from the URI, from the request body, or from a custom binding.</span></span> <span data-ttu-id="19d1d-207">對於來自 URI 的參數，我們想要確保 URI 實際上包含該參數的值，不論是在路徑中（透過路由字典）或是在查詢字串中。</span><span class="sxs-lookup"><span data-stu-id="19d1d-207">For parameters that come from the URI, we want to ensure that the URI actually contains a value for that parameter, either in the path (via the route dictionary) or in the query string.</span></span>

<span data-ttu-id="19d1d-208">例如，請考慮下列動作：</span><span class="sxs-lookup"><span data-stu-id="19d1d-208">For example, consider the following action:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample7.cs)]

<span data-ttu-id="19d1d-209">*Id*參數會系結至 URI。</span><span class="sxs-lookup"><span data-stu-id="19d1d-209">The *id* parameter binds to the URI.</span></span> <span data-ttu-id="19d1d-210">因此，此動作只能符合在路由字典或查詢字串中包含 "id" 值的 URI。</span><span class="sxs-lookup"><span data-stu-id="19d1d-210">Therefore, this action can only match a URI that contains a value for "id", either in the route dictionary or in the query string.</span></span>

<span data-ttu-id="19d1d-211">選擇性參數是例外狀況，因為它們是選擇性的。</span><span class="sxs-lookup"><span data-stu-id="19d1d-211">Optional parameters are an exception, because they are optional.</span></span> <span data-ttu-id="19d1d-212">對於選擇性參數，如果系結無法從 URI 取得值，則為 OK。</span><span class="sxs-lookup"><span data-stu-id="19d1d-212">For an optional parameter, it's OK if the binding can't get the value from the URI.</span></span>

<span data-ttu-id="19d1d-213">複雜類型是因不同原因而產生的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="19d1d-213">Complex types are an exception for a different reason.</span></span> <span data-ttu-id="19d1d-214">複雜型別只能透過自訂系結系結至 URI。</span><span class="sxs-lookup"><span data-stu-id="19d1d-214">A complex type can only bind to the URI through a custom binding.</span></span> <span data-ttu-id="19d1d-215">但是在這種情況下，架構無法事先知道參數是否會系結至特定的 URI。</span><span class="sxs-lookup"><span data-stu-id="19d1d-215">But in that case, the framework cannot know in advance whether the parameter would bind to a particular URI.</span></span> <span data-ttu-id="19d1d-216">若要找出，必須叫用系結。</span><span class="sxs-lookup"><span data-stu-id="19d1d-216">To find out, it would need to invoke the binding.</span></span> <span data-ttu-id="19d1d-217">選取演算法的目標是在叫用任何系結之前，從靜態描述中選取動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-217">The goal of the selection algorithm is to select an action from the static description, before invoking any bindings.</span></span> <span data-ttu-id="19d1d-218">因此，複雜類型會從比對演算法中排除。</span><span class="sxs-lookup"><span data-stu-id="19d1d-218">Therefore, complex types are excluded from the matching algorithm.</span></span>

<span data-ttu-id="19d1d-219">選取動作之後，就會叫用所有參數系結。</span><span class="sxs-lookup"><span data-stu-id="19d1d-219">After the action is selected, all parameter bindings are invoked.</span></span>

<span data-ttu-id="19d1d-220">摘要:</span><span class="sxs-lookup"><span data-stu-id="19d1d-220">Summary:</span></span>

- <span data-ttu-id="19d1d-221">動作必須符合要求的 HTTP 方法。</span><span class="sxs-lookup"><span data-stu-id="19d1d-221">The action must match the HTTP method of the request.</span></span>
- <span data-ttu-id="19d1d-222">動作名稱必須符合路由字典中的「動作」專案（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="19d1d-222">The action name must match the "action" entry in the route dictionary, if present.</span></span>
- <span data-ttu-id="19d1d-223">對於動作的每個參數，如果從 URI 取得參數，則必須在路由字典或 URI 查詢字串中找到參數名稱。</span><span class="sxs-lookup"><span data-stu-id="19d1d-223">For every parameter of the action, if the parameter is taken from the URI, then the parameter name must be found either in the route dictionary or in the URI query string.</span></span> <span data-ttu-id="19d1d-224">（已排除具有複雜類型的選擇性參數和參數）。</span><span class="sxs-lookup"><span data-stu-id="19d1d-224">(Optional parameters and parameters with complex types are excluded.)</span></span>
- <span data-ttu-id="19d1d-225">嘗試比對最多的參數數目。</span><span class="sxs-lookup"><span data-stu-id="19d1d-225">Try to match the most number of parameters.</span></span> <span data-ttu-id="19d1d-226">最佳比對可能是沒有參數的方法。</span><span class="sxs-lookup"><span data-stu-id="19d1d-226">The best match might be a method with no parameters.</span></span>

## <a name="extended-example"></a><span data-ttu-id="19d1d-227">擴充範例</span><span class="sxs-lookup"><span data-stu-id="19d1d-227">Extended Example</span></span>

<span data-ttu-id="19d1d-228">料</span><span class="sxs-lookup"><span data-stu-id="19d1d-228">Routes:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample8.cs)]

<span data-ttu-id="19d1d-229">控制器:</span><span class="sxs-lookup"><span data-stu-id="19d1d-229">Controller:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample9.cs)]

<span data-ttu-id="19d1d-230">HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="19d1d-230">HTTP request:</span></span>

[!code-console[Main](routing-and-action-selection/samples/sample10.cmd)]

### <a name="route-matching"></a><span data-ttu-id="19d1d-231">路由符合</span><span class="sxs-lookup"><span data-stu-id="19d1d-231">Route Matching</span></span>

<span data-ttu-id="19d1d-232">URI 符合名為 "DefaultApi" 的路由。</span><span class="sxs-lookup"><span data-stu-id="19d1d-232">The URI matches the route named "DefaultApi".</span></span> <span data-ttu-id="19d1d-233">路由字典包含下列專案：</span><span class="sxs-lookup"><span data-stu-id="19d1d-233">The route dictionary contains the following entries:</span></span>

- <span data-ttu-id="19d1d-234">控制器：「產品」</span><span class="sxs-lookup"><span data-stu-id="19d1d-234">controller: "products"</span></span>
- <span data-ttu-id="19d1d-235">識別碼： "1"</span><span class="sxs-lookup"><span data-stu-id="19d1d-235">id: "1"</span></span>

<span data-ttu-id="19d1d-236">路由字典不包含查詢字串參數 "version" 和 "details"，但是在動作選取期間仍會考慮這些專案。</span><span class="sxs-lookup"><span data-stu-id="19d1d-236">The route dictionary does not contain the query string parameters, "version" and "details", but these will still be considered during action selection.</span></span>

### <a name="controller-selection"></a><span data-ttu-id="19d1d-237">控制器選取</span><span class="sxs-lookup"><span data-stu-id="19d1d-237">Controller Selection</span></span>

<span data-ttu-id="19d1d-238">從路由字典中的「控制器」專案，控制器類型為 `ProductsController`。</span><span class="sxs-lookup"><span data-stu-id="19d1d-238">From the "controller" entry in the route dictionary, the controller type is `ProductsController`.</span></span>

### <a name="action-selection"></a><span data-ttu-id="19d1d-239">動作選取</span><span class="sxs-lookup"><span data-stu-id="19d1d-239">Action Selection</span></span>

<span data-ttu-id="19d1d-240">HTTP 要求是 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="19d1d-240">The HTTP request is a GET request.</span></span> <span data-ttu-id="19d1d-241">支援 GET 的控制器動作包括 `GetAll`、`GetById`和 `FindProductsByName`。</span><span class="sxs-lookup"><span data-stu-id="19d1d-241">The controller actions that support GET are `GetAll`, `GetById`, and `FindProductsByName`.</span></span> <span data-ttu-id="19d1d-242">路由字典未包含 "action" 的專案，因此不需要符合動作名稱。</span><span class="sxs-lookup"><span data-stu-id="19d1d-242">The route dictionary does not contain an entry for "action", so we don't need to match the action name.</span></span>

<span data-ttu-id="19d1d-243">接下來，我們會嘗試比對動作的參數名稱，只查看 [取得] 動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-243">Next, we try to match parameter names for the actions, looking only at the GET actions.</span></span>

| <span data-ttu-id="19d1d-244">動作</span><span class="sxs-lookup"><span data-stu-id="19d1d-244">Action</span></span> | <span data-ttu-id="19d1d-245">要比對的參數</span><span class="sxs-lookup"><span data-stu-id="19d1d-245">Parameters to Match</span></span> |
| --- | --- |
| `GetAll` | <span data-ttu-id="19d1d-246">無</span><span class="sxs-lookup"><span data-stu-id="19d1d-246">none</span></span> |
| `GetById` | <span data-ttu-id="19d1d-247">"id"</span><span class="sxs-lookup"><span data-stu-id="19d1d-247">"id"</span></span> |
| `FindProductsByName` | <span data-ttu-id="19d1d-248">檔案名</span><span class="sxs-lookup"><span data-stu-id="19d1d-248">"name"</span></span> |

<span data-ttu-id="19d1d-249">請注意，不會考慮 `GetById` 的*version*參數，因為它是選擇性參數。</span><span class="sxs-lookup"><span data-stu-id="19d1d-249">Notice that the *version* parameter of `GetById` is not considered, because it is an optional parameter.</span></span>

<span data-ttu-id="19d1d-250">`GetAll` 的方法符合完整。</span><span class="sxs-lookup"><span data-stu-id="19d1d-250">The `GetAll` method matches trivially.</span></span> <span data-ttu-id="19d1d-251">`GetById` 方法也會符合，因為路由字典包含 "id"。</span><span class="sxs-lookup"><span data-stu-id="19d1d-251">The `GetById` method also matches, because the route dictionary contains "id".</span></span> <span data-ttu-id="19d1d-252">`FindProductsByName` 的方法不相符。</span><span class="sxs-lookup"><span data-stu-id="19d1d-252">The `FindProductsByName` method does not match.</span></span>

<span data-ttu-id="19d1d-253">`GetById` 方法會勝出，因為它符合一個參數，而不是 `GetAll`的參數。</span><span class="sxs-lookup"><span data-stu-id="19d1d-253">The `GetById` method wins, because it matches one parameter, versus no parameters for `GetAll`.</span></span> <span data-ttu-id="19d1d-254">使用下列參數值叫用方法：</span><span class="sxs-lookup"><span data-stu-id="19d1d-254">The method is invoked with the following parameter values:</span></span>

- <span data-ttu-id="19d1d-255">*識別碼*= 1</span><span class="sxs-lookup"><span data-stu-id="19d1d-255">*id* = 1</span></span>
- <span data-ttu-id="19d1d-256">*版本*= 1。5</span><span class="sxs-lookup"><span data-stu-id="19d1d-256">*version* = 1.5</span></span>

<span data-ttu-id="19d1d-257">請注意，即使*版本*不是用在選取演算法中，參數的值還是來自 URI 查詢字串。</span><span class="sxs-lookup"><span data-stu-id="19d1d-257">Notice that even though *version* was not used in the selection algorithm, the value of the parameter comes from the URI query string.</span></span>

## <a name="extension-points"></a><span data-ttu-id="19d1d-258">擴充點</span><span class="sxs-lookup"><span data-stu-id="19d1d-258">Extension Points</span></span>

<span data-ttu-id="19d1d-259">Web API 會為路由程式的某些部分提供延伸模組點。</span><span class="sxs-lookup"><span data-stu-id="19d1d-259">Web API provides extension points for some parts of the routing process.</span></span>

| <span data-ttu-id="19d1d-260">介面</span><span class="sxs-lookup"><span data-stu-id="19d1d-260">Interface</span></span> | <span data-ttu-id="19d1d-261">說明</span><span class="sxs-lookup"><span data-stu-id="19d1d-261">Description</span></span> |
| --- | --- |
| <span data-ttu-id="19d1d-262">**IHttpControllerSelector**</span><span class="sxs-lookup"><span data-stu-id="19d1d-262">**IHttpControllerSelector**</span></span> | <span data-ttu-id="19d1d-263">選取控制器。</span><span class="sxs-lookup"><span data-stu-id="19d1d-263">Selects the controller.</span></span> |
| <span data-ttu-id="19d1d-264">**IHttpControllerTypeResolver**</span><span class="sxs-lookup"><span data-stu-id="19d1d-264">**IHttpControllerTypeResolver**</span></span> | <span data-ttu-id="19d1d-265">取得控制器類型的清單。</span><span class="sxs-lookup"><span data-stu-id="19d1d-265">Gets the list of controller types.</span></span> <span data-ttu-id="19d1d-266">**DefaultHttpControllerSelector**會從這份清單中選擇控制器類型。</span><span class="sxs-lookup"><span data-stu-id="19d1d-266">The **DefaultHttpControllerSelector** chooses the controller type from this list.</span></span> |
| <span data-ttu-id="19d1d-267">**IAssembliesResolver**</span><span class="sxs-lookup"><span data-stu-id="19d1d-267">**IAssembliesResolver**</span></span> | <span data-ttu-id="19d1d-268">取得專案元件的清單。</span><span class="sxs-lookup"><span data-stu-id="19d1d-268">Gets the list of project assemblies.</span></span> <span data-ttu-id="19d1d-269">**IHttpControllerTypeResolver**介面會使用這份清單來尋找控制器類型。</span><span class="sxs-lookup"><span data-stu-id="19d1d-269">The **IHttpControllerTypeResolver** interface uses this list to find the controller types.</span></span> |
| <span data-ttu-id="19d1d-270">**IHttpControllerActivator**</span><span class="sxs-lookup"><span data-stu-id="19d1d-270">**IHttpControllerActivator**</span></span> | <span data-ttu-id="19d1d-271">建立新的控制器實例。</span><span class="sxs-lookup"><span data-stu-id="19d1d-271">Creates new controller instances.</span></span> |
| <span data-ttu-id="19d1d-272">**IHttpActionSelector**</span><span class="sxs-lookup"><span data-stu-id="19d1d-272">**IHttpActionSelector**</span></span> | <span data-ttu-id="19d1d-273">選取動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-273">Selects the action.</span></span> |
| <span data-ttu-id="19d1d-274">**IHttpActionInvoker**</span><span class="sxs-lookup"><span data-stu-id="19d1d-274">**IHttpActionInvoker**</span></span> | <span data-ttu-id="19d1d-275">叫用動作。</span><span class="sxs-lookup"><span data-stu-id="19d1d-275">Invokes the action.</span></span> |

<span data-ttu-id="19d1d-276">若要為上述任何介面提供您自己的執行，請在**HttpConfiguration**物件上使用**Services**集合：</span><span class="sxs-lookup"><span data-stu-id="19d1d-276">To provide your own implementation for any of these interfaces, use the **Services** collection on the **HttpConfiguration** object:</span></span>

[!code-csharp[Main](routing-and-action-selection/samples/sample11.cs)]
