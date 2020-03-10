---
uid: web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
title: ASP.NET Web API 中的路由 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 10/29/2018
ms.assetid: 0675bdc7-282f-4f47-b7f3-7e02133940ca
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/routing-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 85862c094cc54365267b1f21e68d235a15519cda
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557607"
---
# <a name="routing-in-aspnet-web-api"></a><span data-ttu-id="0ba11-102">ASP.NET Web API 中的路由</span><span class="sxs-lookup"><span data-stu-id="0ba11-102">Routing in ASP.NET Web API</span></span>

<span data-ttu-id="0ba11-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="0ba11-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="0ba11-104">本文說明 ASP.NET Web API 如何將 HTTP 要求路由傳送至控制器。</span><span class="sxs-lookup"><span data-stu-id="0ba11-104">This article describes how ASP.NET Web API routes HTTP requests to controllers.</span></span>

> [!NOTE]
> <span data-ttu-id="0ba11-105">如果您熟悉 ASP.NET MVC，Web API 路由與 MVC 路由非常類似。</span><span class="sxs-lookup"><span data-stu-id="0ba11-105">If you are familiar with ASP.NET MVC, Web API routing is very similar to MVC routing.</span></span> <span data-ttu-id="0ba11-106">主要差異在於 Web API 會使用 HTTP 指令動詞，而不是 URI 路徑來選取動作。</span><span class="sxs-lookup"><span data-stu-id="0ba11-106">The main difference is that Web API uses the HTTP verb, not the URI path, to select the action.</span></span> <span data-ttu-id="0ba11-107">您也可以在 Web API 中使用 MVC 樣式的路由。</span><span class="sxs-lookup"><span data-stu-id="0ba11-107">You can also use MVC-style routing in Web API.</span></span> <span data-ttu-id="0ba11-108">本文不會假設您對 ASP.NET MVC 有任何瞭解。</span><span class="sxs-lookup"><span data-stu-id="0ba11-108">This article does not assume any knowledge of ASP.NET MVC.</span></span>

## <a name="routing-tables"></a><span data-ttu-id="0ba11-109">路由表</span><span class="sxs-lookup"><span data-stu-id="0ba11-109">Routing Tables</span></span>

<span data-ttu-id="0ba11-110">在 ASP.NET Web API 中，*控制器*是處理 HTTP 要求的類別。</span><span class="sxs-lookup"><span data-stu-id="0ba11-110">In ASP.NET Web API, a *controller* is a class that handles HTTP requests.</span></span> <span data-ttu-id="0ba11-111">控制器的公用方法稱為*動作方法*或簡單的*動作*。</span><span class="sxs-lookup"><span data-stu-id="0ba11-111">The public methods of the controller are called *action methods* or simply *actions*.</span></span> <span data-ttu-id="0ba11-112">當 Web API 架構收到要求時，它會將要求路由傳送至動作。</span><span class="sxs-lookup"><span data-stu-id="0ba11-112">When the Web API framework receives a request, it routes the request to an action.</span></span>

<span data-ttu-id="0ba11-113">為了判斷要叫用的動作，架構會使用*路由表*。</span><span class="sxs-lookup"><span data-stu-id="0ba11-113">To determine which action to invoke, the framework uses a *routing table*.</span></span> <span data-ttu-id="0ba11-114">Web API 的 Visual Studio 專案範本會建立預設路由：</span><span class="sxs-lookup"><span data-stu-id="0ba11-114">The Visual Studio project template for Web API creates a default route:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="0ba11-115">此路由是在*WebApiConfig.cs*檔案中定義，此檔案會放在*應用程式\_起始*目錄中：</span><span class="sxs-lookup"><span data-stu-id="0ba11-115">This route is defined in the *WebApiConfig.cs* file, which is placed in the *App\_Start* directory:</span></span>

![](routing-in-aspnet-web-api/_static/image1.png)

<span data-ttu-id="0ba11-116">如需 `WebApiConfig` 類別的詳細資訊，請參閱設定[ASP.NET Web API](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba11-116">For more information about the `WebApiConfig` class, see [Configuring ASP.NET Web API](../advanced/configuring-aspnet-web-api.md).</span></span>

<span data-ttu-id="0ba11-117">如果您自行裝載 Web API，您必須直接在 `HttpSelfHostConfiguration` 物件上設定路由表。</span><span class="sxs-lookup"><span data-stu-id="0ba11-117">If you self-host Web API, you must set the routing table directly on the `HttpSelfHostConfiguration` object.</span></span> <span data-ttu-id="0ba11-118">如需詳細資訊，請參閱[自我裝載 WEB API](../older-versions/self-host-a-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="0ba11-118">For more information, see [Self-Host a Web API](../older-versions/self-host-a-web-api.md).</span></span>

<span data-ttu-id="0ba11-119">路由表中的每個專案都包含一個*路由範本*。</span><span class="sxs-lookup"><span data-stu-id="0ba11-119">Each entry in the routing table contains a *route template*.</span></span> <span data-ttu-id="0ba11-120">Web API 的預設路由範本為 &quot;API/{controller}/{id}&quot;。</span><span class="sxs-lookup"><span data-stu-id="0ba11-120">The default route template for Web API is &quot;api/{controller}/{id}&quot;.</span></span> <span data-ttu-id="0ba11-121">在此範本中，&quot;api&quot; 是常值路徑區段，而 {controller} 和 {id} 是預留位置變數。</span><span class="sxs-lookup"><span data-stu-id="0ba11-121">In this template, &quot;api&quot; is a literal path segment, and {controller} and {id} are placeholder variables.</span></span>

<span data-ttu-id="0ba11-122">當 Web API 架構收到 HTTP 要求時，它會嘗試比對路由表中的其中一個路由範本的 URI。</span><span class="sxs-lookup"><span data-stu-id="0ba11-122">When the Web API framework receives an HTTP request, it tries to match the URI against one of the route templates in the routing table.</span></span> <span data-ttu-id="0ba11-123">如果沒有符合的路由，用戶端會收到404錯誤。</span><span class="sxs-lookup"><span data-stu-id="0ba11-123">If no route matches, the client receives a 404 error.</span></span> <span data-ttu-id="0ba11-124">例如，下列 Uri 符合預設路由：</span><span class="sxs-lookup"><span data-stu-id="0ba11-124">For example, the following URIs match the default route:</span></span>

- <span data-ttu-id="0ba11-125">/api/contacts</span><span class="sxs-lookup"><span data-stu-id="0ba11-125">/api/contacts</span></span>
- <span data-ttu-id="0ba11-126">/api/contacts/1</span><span class="sxs-lookup"><span data-stu-id="0ba11-126">/api/contacts/1</span></span>
- <span data-ttu-id="0ba11-127">/api/products/gizmo1</span><span class="sxs-lookup"><span data-stu-id="0ba11-127">/api/products/gizmo1</span></span>

<span data-ttu-id="0ba11-128">不過，下列 URI 不相符，因為它缺少 &quot;api&quot; 區段：</span><span class="sxs-lookup"><span data-stu-id="0ba11-128">However, the following URI does not match, because it lacks the &quot;api&quot; segment:</span></span>

- <span data-ttu-id="0ba11-129">/contacts/1</span><span class="sxs-lookup"><span data-stu-id="0ba11-129">/contacts/1</span></span>

> [!NOTE]
> <span data-ttu-id="0ba11-130">在路由中使用「api」的原因是為了避免與 ASP.NET MVC 路由發生衝突。</span><span class="sxs-lookup"><span data-stu-id="0ba11-130">The reason for using "api" in the route is to avoid collisions with ASP.NET MVC routing.</span></span> <span data-ttu-id="0ba11-131">如此一來，您就可以讓 &quot;/contacts&quot; 移至 MVC 控制器，並 &quot;/api/contacts&quot; 移至 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="0ba11-131">That way, you can have &quot;/contacts&quot; go to an MVC controller, and &quot;/api/contacts&quot; go to a Web API controller.</span></span> <span data-ttu-id="0ba11-132">當然，如果您不喜歡這種慣例，可以變更預設的路由表。</span><span class="sxs-lookup"><span data-stu-id="0ba11-132">Of course, if you don't like this convention, you can change the default route table.</span></span>

<span data-ttu-id="0ba11-133">一旦找到相符的路由，Web API 就會選取控制器和動作：</span><span class="sxs-lookup"><span data-stu-id="0ba11-133">Once a matching route is found, Web API selects the controller and the action:</span></span>

- <span data-ttu-id="0ba11-134">若要尋找控制器，Web API 會將 &quot;控制器&quot; 新增至 *{controller}* 變數的值。</span><span class="sxs-lookup"><span data-stu-id="0ba11-134">To find the controller, Web API adds &quot;Controller&quot; to the value of the *{controller}* variable.</span></span>
- <span data-ttu-id="0ba11-135">若要尋找此動作，Web API 會查看 HTTP 指令動詞，然後尋找名稱開頭為該 HTTP 動詞命令名稱的動作。</span><span class="sxs-lookup"><span data-stu-id="0ba11-135">To find the action, Web API looks at the HTTP verb, and then looks for an action whose name begins with that HTTP verb name.</span></span> <span data-ttu-id="0ba11-136">例如，使用 GET 要求時，Web API 會尋找前面加上 &quot;Get&quot;的動作，例如 &quot;GetContact&quot; 或 &quot;GetAllContacts&quot;。</span><span class="sxs-lookup"><span data-stu-id="0ba11-136">For example, with a GET request, Web API looks for an action prefixed with &quot;Get&quot;, such as &quot;GetContact&quot; or &quot;GetAllContacts&quot;.</span></span> <span data-ttu-id="0ba11-137">此慣例僅適用于 GET、POST、PUT、DELETE、HEAD、OPTIONS 和 PATCH 動詞。</span><span class="sxs-lookup"><span data-stu-id="0ba11-137">This convention applies only to GET, POST, PUT, DELETE, HEAD, OPTIONS, and PATCH verbs.</span></span> <span data-ttu-id="0ba11-138">您可以使用控制器上的屬性來啟用其他 HTTP 動詞命令。</span><span class="sxs-lookup"><span data-stu-id="0ba11-138">You can enable other HTTP verbs by using attributes on your controller.</span></span> <span data-ttu-id="0ba11-139">我們稍後會看到一個範例。</span><span class="sxs-lookup"><span data-stu-id="0ba11-139">We'll see an example of that later.</span></span>
- <span data-ttu-id="0ba11-140">路由範本中的其他預留位置變數（例如 *{id}）* 會對應至動作參數。</span><span class="sxs-lookup"><span data-stu-id="0ba11-140">Other placeholder variables in the route template, such as *{id},* are mapped to action parameters.</span></span>

<span data-ttu-id="0ba11-141">讓我們看看以下範例。</span><span class="sxs-lookup"><span data-stu-id="0ba11-141">Let's look at an example.</span></span> <span data-ttu-id="0ba11-142">假設您定義了下列控制器：</span><span class="sxs-lookup"><span data-stu-id="0ba11-142">Suppose that you define the following controller:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="0ba11-143">以下是一些可能的 HTTP 要求，以及針對每個要求叫用的動作：</span><span class="sxs-lookup"><span data-stu-id="0ba11-143">Here are some possible HTTP requests, along with the action that gets invoked for each:</span></span>

| <span data-ttu-id="0ba11-144">HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="0ba11-144">HTTP Verb</span></span> | <span data-ttu-id="0ba11-145">URI 路徑</span><span class="sxs-lookup"><span data-stu-id="0ba11-145">URI Path</span></span> | <span data-ttu-id="0ba11-146">動作</span><span class="sxs-lookup"><span data-stu-id="0ba11-146">Action</span></span> | <span data-ttu-id="0ba11-147">參數</span><span class="sxs-lookup"><span data-stu-id="0ba11-147">Parameter</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="0ba11-148">GET</span><span class="sxs-lookup"><span data-stu-id="0ba11-148">GET</span></span> | <span data-ttu-id="0ba11-149">api/產品</span><span class="sxs-lookup"><span data-stu-id="0ba11-149">api/products</span></span> | <span data-ttu-id="0ba11-150">Getallproductswithcategories</span><span class="sxs-lookup"><span data-stu-id="0ba11-150">GetAllProducts</span></span> | <span data-ttu-id="0ba11-151">*無*</span><span class="sxs-lookup"><span data-stu-id="0ba11-151">*(none)*</span></span> |
| <span data-ttu-id="0ba11-152">GET</span><span class="sxs-lookup"><span data-stu-id="0ba11-152">GET</span></span> | <span data-ttu-id="0ba11-153">api/產品/4</span><span class="sxs-lookup"><span data-stu-id="0ba11-153">api/products/4</span></span> | <span data-ttu-id="0ba11-154">GetProductById</span><span class="sxs-lookup"><span data-stu-id="0ba11-154">GetProductById</span></span> | <span data-ttu-id="0ba11-155">4</span><span class="sxs-lookup"><span data-stu-id="0ba11-155">4</span></span> |
| <span data-ttu-id="0ba11-156">刪除</span><span class="sxs-lookup"><span data-stu-id="0ba11-156">DELETE</span></span> | <span data-ttu-id="0ba11-157">api/產品/4</span><span class="sxs-lookup"><span data-stu-id="0ba11-157">api/products/4</span></span> | <span data-ttu-id="0ba11-158">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="0ba11-158">DeleteProduct</span></span> | <span data-ttu-id="0ba11-159">4</span><span class="sxs-lookup"><span data-stu-id="0ba11-159">4</span></span> |
| <span data-ttu-id="0ba11-160">POST</span><span class="sxs-lookup"><span data-stu-id="0ba11-160">POST</span></span> | <span data-ttu-id="0ba11-161">api/產品</span><span class="sxs-lookup"><span data-stu-id="0ba11-161">api/products</span></span> | <span data-ttu-id="0ba11-162">*（不符合）*</span><span class="sxs-lookup"><span data-stu-id="0ba11-162">*(no match)*</span></span> |  |

<span data-ttu-id="0ba11-163">請注意，URI 的 *{id}* 區段（如果有的話）會對應至動作的*id*參數。</span><span class="sxs-lookup"><span data-stu-id="0ba11-163">Notice that the *{id}* segment of the URI, if present, is mapped to the *id* parameter of the action.</span></span> <span data-ttu-id="0ba11-164">在此範例中，控制器會定義兩個 GET 方法，一個具有*識別碼*參數，另一個不含參數。</span><span class="sxs-lookup"><span data-stu-id="0ba11-164">In this example, the controller defines two GET methods, one with an *id* parameter and one with no parameters.</span></span>

<span data-ttu-id="0ba11-165">此外，請注意 POST 要求將會失敗，因為控制器不會定義 &quot;Post ...&quot; 方法。</span><span class="sxs-lookup"><span data-stu-id="0ba11-165">Also, note that the POST request will fail, because the controller does not define a &quot;Post...&quot; method.</span></span>

## <a name="routing-variations"></a><span data-ttu-id="0ba11-166">路由變化</span><span class="sxs-lookup"><span data-stu-id="0ba11-166">Routing Variations</span></span>

<span data-ttu-id="0ba11-167">上一節說明了 ASP.NET Web API 的基本路由機制。</span><span class="sxs-lookup"><span data-stu-id="0ba11-167">The previous section described the basic routing mechanism for ASP.NET Web API.</span></span> <span data-ttu-id="0ba11-168">本節說明一些變化。</span><span class="sxs-lookup"><span data-stu-id="0ba11-168">This section describes some variations.</span></span>

### <a name="http-verbs"></a><span data-ttu-id="0ba11-169">HTTP 指令動詞</span><span class="sxs-lookup"><span data-stu-id="0ba11-169">HTTP verbs</span></span>

<span data-ttu-id="0ba11-170">您可以使用下列其中一個屬性來裝飾動作方法，而不是使用 HTTP 指令動詞的命名慣例，以明確指定動作的 HTTP 動詞命令：</span><span class="sxs-lookup"><span data-stu-id="0ba11-170">Instead of using the naming convention for HTTP verbs, you can explicitly specify the HTTP verb for an action by decorating the action method with one of the following attributes:</span></span>

- `[HttpGet]`
- `[HttpPut]`
- `[HttpPost]`
- `[HttpDelete]`
- `[HttpHead]`
- `[HttpOptions]`
- `[HttpPatch]`

<span data-ttu-id="0ba11-171">在下列範例中，`FindProduct` 方法會對應至 GET 要求：</span><span class="sxs-lookup"><span data-stu-id="0ba11-171">In the following example, the `FindProduct` method is mapped to GET requests:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="0ba11-172">若要允許某個動作有多個 HTTP 動詞命令，或允許 GET、PUT、POST、DELETE、HEAD、OPTIONS 和 PATCH 以外的 HTTP 動詞命令，請使用 `[AcceptVerbs]` 屬性，這會接受 HTTP 指令動詞的清單。</span><span class="sxs-lookup"><span data-stu-id="0ba11-172">To allow multiple HTTP verbs for an action, or to allow HTTP verbs other than GET, PUT, POST, DELETE, HEAD, OPTIONS, and PATCH, use the `[AcceptVerbs]` attribute, which takes a list of HTTP verbs.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample4.cs)]

<a id="routing_by_action_name"></a>
### <a name="routing-by-action-name"></a><span data-ttu-id="0ba11-173">依動作名稱路由</span><span class="sxs-lookup"><span data-stu-id="0ba11-173">Routing by Action Name</span></span>

<span data-ttu-id="0ba11-174">使用預設路由範本時，Web API 會使用 HTTP 指令動詞來選取動作。</span><span class="sxs-lookup"><span data-stu-id="0ba11-174">With the default routing template, Web API uses the HTTP verb to select the action.</span></span> <span data-ttu-id="0ba11-175">不過，您也可以建立路由，其中動作名稱會包含在 URI 中：</span><span class="sxs-lookup"><span data-stu-id="0ba11-175">However, you can also create a route where the action name is included in the URI:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="0ba11-176">在此路由範本中， *{action}* 參數會在控制器上命名動作方法。</span><span class="sxs-lookup"><span data-stu-id="0ba11-176">In this route template, the *{action}* parameter names the action method on the controller.</span></span> <span data-ttu-id="0ba11-177">使用這種路由模式時，請使用屬性來指定允許的 HTTP 動詞命令。</span><span class="sxs-lookup"><span data-stu-id="0ba11-177">With this style of routing, use attributes to specify the allowed HTTP verbs.</span></span> <span data-ttu-id="0ba11-178">例如，假設您的控制器具有下列方法：</span><span class="sxs-lookup"><span data-stu-id="0ba11-178">For example, suppose your controller has the following method:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="0ba11-179">在此情況下，「api/產品/詳細資料/1」的 GET 要求會對應至 `Details` 方法。</span><span class="sxs-lookup"><span data-stu-id="0ba11-179">In this case, a GET request for "api/products/details/1" would map to the `Details` method.</span></span> <span data-ttu-id="0ba11-180">這種路由樣式類似于 ASP.NET MVC，而且可能適用于 RPC 樣式的 API。</span><span class="sxs-lookup"><span data-stu-id="0ba11-180">This style of routing is similar to ASP.NET MVC, and may be appropriate for an RPC-style API.</span></span>

<span data-ttu-id="0ba11-181">您可以使用 `[ActionName]` 屬性來覆寫動作名稱。</span><span class="sxs-lookup"><span data-stu-id="0ba11-181">You can override the action name by using the `[ActionName]` attribute.</span></span> <span data-ttu-id="0ba11-182">在下列範例中，有兩個動作會對應至 &quot;api/產品/縮圖/*識別碼*。其中一個支援 GET，另一個支援 POST：</span><span class="sxs-lookup"><span data-stu-id="0ba11-182">In the following example, there are two actions that map to &quot;api/products/thumbnail/*id*. One supports GET and the other supports POST:</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample7.cs)]

### <a name="non-actions"></a><span data-ttu-id="0ba11-183">非動作</span><span class="sxs-lookup"><span data-stu-id="0ba11-183">Non-Actions</span></span>

<span data-ttu-id="0ba11-184">若要防止方法被叫用為動作，請使用 `[NonAction]` 屬性。</span><span class="sxs-lookup"><span data-stu-id="0ba11-184">To prevent a method from getting invoked as an action, use the `[NonAction]` attribute.</span></span> <span data-ttu-id="0ba11-185">這會向架構指出方法不是動作，即使它會符合路由規則也一樣。</span><span class="sxs-lookup"><span data-stu-id="0ba11-185">This signals to the framework that the method is not an action, even if it would otherwise match the routing rules.</span></span>

[!code-csharp[Main](routing-in-aspnet-web-api/samples/sample8.cs)]

## <a name="further-reading"></a><span data-ttu-id="0ba11-186">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="0ba11-186">Further Reading</span></span>

<span data-ttu-id="0ba11-187">本主題提供路由的高階觀點。</span><span class="sxs-lookup"><span data-stu-id="0ba11-187">This topic provided a high-level view of routing.</span></span> <span data-ttu-id="0ba11-188">如需詳細資訊，請參閱[路由和動作選取](routing-and-action-selection.md)，其中描述架構如何比對路由的 URI、選取控制器，然後選取要叫用的動作。</span><span class="sxs-lookup"><span data-stu-id="0ba11-188">For more detail, see [Routing and Action Selection](routing-and-action-selection.md), which describes exactly how the framework matches a URI to a route, selects a controller, and then selects the action to invoke.</span></span>
