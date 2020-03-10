---
uid: web-api/overview/advanced/http-message-handlers
title: ASP.NET Web API 中的 HTTP 訊息處理常式-ASP.NET 4。x
author: MikeWasson
description: ASP.NET 4.x 的 ASP.NET Web API 中的 HTTP 訊息處理常式總覽
ms.author: riande
ms.date: 02/13/2012
ms.custom: seoapril2019
ms.assetid: 9002018b-3aa3-4358-bb1c-fbb5bc751d01
msc.legacyurl: /web-api/overview/advanced/http-message-handlers
msc.type: authoredcontent
ms.openlocfilehash: a8e6f1da8df4802e1acf7779a2fc75bfe8ab876f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78622581"
---
# <a name="http-message-handlers-in-aspnet-web-api"></a><span data-ttu-id="757e2-103">ASP.NET Web API 中的 HTTP 訊息處理常式</span><span class="sxs-lookup"><span data-stu-id="757e2-103">HTTP Message Handlers in ASP.NET Web API</span></span>

<span data-ttu-id="757e2-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="757e2-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="757e2-105">*訊息處理常式*是接收 HTTP 要求並傳回 HTTP 回應的類別。</span><span class="sxs-lookup"><span data-stu-id="757e2-105">A *message handler* is a class that receives an HTTP request and returns an HTTP response.</span></span> <span data-ttu-id="757e2-106">訊息處理常式衍生自抽象**HttpMessageHandler**類別。</span><span class="sxs-lookup"><span data-stu-id="757e2-106">Message handlers derive from the abstract **HttpMessageHandler** class.</span></span>

<span data-ttu-id="757e2-107">通常會將一系列的訊息處理常式連結在一起。</span><span class="sxs-lookup"><span data-stu-id="757e2-107">Typically, a series of message handlers are chained together.</span></span> <span data-ttu-id="757e2-108">第一個處理常式會接收 HTTP 要求、進行某些處理，並將要求提供給下一個處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-108">The first handler receives an HTTP request, does some processing, and gives the request to the next handler.</span></span> <span data-ttu-id="757e2-109">在某個時間點，會建立回應，並備份鏈。</span><span class="sxs-lookup"><span data-stu-id="757e2-109">At some point, the response is created and goes back up the chain.</span></span> <span data-ttu-id="757e2-110">這個模式稱為*委派*處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-110">This pattern is called a *delegating* handler.</span></span>

![](http-message-handlers/_static/image1.png)

## <a name="server-side-message-handlers"></a><span data-ttu-id="757e2-111">伺服器端訊息處理常式</span><span class="sxs-lookup"><span data-stu-id="757e2-111">Server-Side Message Handlers</span></span>

<span data-ttu-id="757e2-112">在伺服器端，Web API 管線會使用一些內建的訊息處理常式：</span><span class="sxs-lookup"><span data-stu-id="757e2-112">On the server side, the Web API pipeline uses some built-in message handlers:</span></span>

- <span data-ttu-id="757e2-113">**HttpServer**會從主機取得要求。</span><span class="sxs-lookup"><span data-stu-id="757e2-113">**HttpServer** gets the request from the host.</span></span>
- <span data-ttu-id="757e2-114">**HttpRoutingDispatcher**會根據路由分派要求。</span><span class="sxs-lookup"><span data-stu-id="757e2-114">**HttpRoutingDispatcher** dispatches the request based on the route.</span></span>
- <span data-ttu-id="757e2-115">**System.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**會將要求傳送至 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="757e2-115">**HttpControllerDispatcher** sends the request to a Web API controller.</span></span>

<span data-ttu-id="757e2-116">您可以將自訂處理常式新增至管線。</span><span class="sxs-lookup"><span data-stu-id="757e2-116">You can add custom handlers to the pipeline.</span></span> <span data-ttu-id="757e2-117">訊息處理常式適用于在 HTTP 訊息層級（而不是控制器動作）上運作的跨領域考慮。</span><span class="sxs-lookup"><span data-stu-id="757e2-117">Message handlers are good for cross-cutting concerns that operate at the level of HTTP messages (rather than controller actions).</span></span> <span data-ttu-id="757e2-118">例如，訊息處理常式可能會：</span><span class="sxs-lookup"><span data-stu-id="757e2-118">For example, a message handler might:</span></span>

- <span data-ttu-id="757e2-119">讀取或修改要求標頭。</span><span class="sxs-lookup"><span data-stu-id="757e2-119">Read or modify request headers.</span></span>
- <span data-ttu-id="757e2-120">將回應標頭新增至回應。</span><span class="sxs-lookup"><span data-stu-id="757e2-120">Add a response header to responses.</span></span>
- <span data-ttu-id="757e2-121">先驗證要求，然後再到達控制器。</span><span class="sxs-lookup"><span data-stu-id="757e2-121">Validate requests before they reach the controller.</span></span>

<span data-ttu-id="757e2-122">下圖顯示兩個插入管線的自訂處理常式：</span><span class="sxs-lookup"><span data-stu-id="757e2-122">This diagram shows two custom handlers inserted into the pipeline:</span></span>

![](http-message-handlers/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="757e2-123">在用戶端上，HttpClient 也會使用訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-123">On the client side, HttpClient also uses message handlers.</span></span> <span data-ttu-id="757e2-124">如需詳細資訊，請參閱[HttpClient 訊息處理常式](httpclient-message-handlers.md)。</span><span class="sxs-lookup"><span data-stu-id="757e2-124">For more information, see [HttpClient Message Handlers](httpclient-message-handlers.md).</span></span>

## <a name="custom-message-handlers"></a><span data-ttu-id="757e2-125">自訂訊息處理常式</span><span class="sxs-lookup"><span data-stu-id="757e2-125">Custom Message Handlers</span></span>

<span data-ttu-id="757e2-126">若要撰寫自訂訊息處理常式，請從**DelegatingHandler**衍生，並覆寫**SendAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="757e2-126">To write a custom message handler, derive from **System.Net.Http.DelegatingHandler** and override the **SendAsync** method.</span></span> <span data-ttu-id="757e2-127">此方法具有下列簽章：</span><span class="sxs-lookup"><span data-stu-id="757e2-127">This method has the following signature:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample1.cs)]

<span data-ttu-id="757e2-128">方法會採用**HttpRequestMessage**做為輸入，並以非同步方式傳回**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="757e2-128">The method takes an **HttpRequestMessage** as input and asynchronously returns an **HttpResponseMessage**.</span></span> <span data-ttu-id="757e2-129">一般的執行會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="757e2-129">A typical implementation does the following:</span></span>

1. <span data-ttu-id="757e2-130">處理要求訊息。</span><span class="sxs-lookup"><span data-stu-id="757e2-130">Process the request message.</span></span>
2. <span data-ttu-id="757e2-131">呼叫 `base.SendAsync` 以將要求傳送至內部處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-131">Call `base.SendAsync` to send the request to the inner handler.</span></span>
3. <span data-ttu-id="757e2-132">內部處理常式會傳迴響應消息。</span><span class="sxs-lookup"><span data-stu-id="757e2-132">The inner handler returns a response message.</span></span> <span data-ttu-id="757e2-133">（此步驟是非同步）。</span><span class="sxs-lookup"><span data-stu-id="757e2-133">(This step is asynchronous.)</span></span>
4. <span data-ttu-id="757e2-134">處理回應，並將它傳回給呼叫者。</span><span class="sxs-lookup"><span data-stu-id="757e2-134">Process the response and return it to the caller.</span></span>

<span data-ttu-id="757e2-135">以下是一個簡單的範例：</span><span class="sxs-lookup"><span data-stu-id="757e2-135">Here is a trivial example:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample2.cs)]

> [!NOTE]
> <span data-ttu-id="757e2-136">對 `base.SendAsync` 的呼叫是非同步的。</span><span class="sxs-lookup"><span data-stu-id="757e2-136">The call to `base.SendAsync` is asynchronous.</span></span> <span data-ttu-id="757e2-137">如果處理常式在此呼叫之後執行任何工作，請使用**await**關鍵字，如下所示。</span><span class="sxs-lookup"><span data-stu-id="757e2-137">If the handler does any work after this call, use the **await** keyword, as shown.</span></span>

<span data-ttu-id="757e2-138">委派處理常式也可以略過內部處理常式，並直接建立回應：</span><span class="sxs-lookup"><span data-stu-id="757e2-138">A delegating handler can also skip the inner handler and directly create the response:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample3.cs)]

<span data-ttu-id="757e2-139">如果委派處理常式在沒有呼叫 `base.SendAsync`的情況下建立回應，則要求會略過管線的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="757e2-139">If a delegating handler creates the response without calling `base.SendAsync`, the request skips the rest of the pipeline.</span></span> <span data-ttu-id="757e2-140">這適用于驗證要求的處理常式（建立錯誤回應）。</span><span class="sxs-lookup"><span data-stu-id="757e2-140">This can be useful for a handler that validates the request (creating an error response).</span></span>

![](http-message-handlers/_static/image3.png)

## <a name="adding-a-handler-to-the-pipeline"></a><span data-ttu-id="757e2-141">將處理常式新增至管線</span><span class="sxs-lookup"><span data-stu-id="757e2-141">Adding a Handler to the Pipeline</span></span>

<span data-ttu-id="757e2-142">若要在伺服器端加入訊息處理常式，請將處理常式加入至**HttpConfiguration. MessageHandlers**集合。</span><span class="sxs-lookup"><span data-stu-id="757e2-142">To add a message handler on the server side, add the handler to the **HttpConfiguration.MessageHandlers** collection.</span></span> <span data-ttu-id="757e2-143">如果您使用「ASP.NET MVC 4 Web 應用程式」範本來建立專案，您可以在**WebApiConfig**類別內執行此動作：</span><span class="sxs-lookup"><span data-stu-id="757e2-143">If you used the "ASP.NET MVC 4 Web Application" template to create the project, you can do this inside the **WebApiConfig** class:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample4.cs)]

<span data-ttu-id="757e2-144">訊息處理常式的呼叫順序，會與它們出現在**MessageHandlers**收集中的順序相同。</span><span class="sxs-lookup"><span data-stu-id="757e2-144">Message handlers are called in the same order that they appear in **MessageHandlers** collection.</span></span> <span data-ttu-id="757e2-145">因為它們是嵌套的，回應訊息會以另一個方向移動。</span><span class="sxs-lookup"><span data-stu-id="757e2-145">Because they are nested, the response message travels in the other direction.</span></span> <span data-ttu-id="757e2-146">也就是，最後一個處理常式是取得回應訊息的第一個。</span><span class="sxs-lookup"><span data-stu-id="757e2-146">That is, the last handler is the first to get the response message.</span></span>

<span data-ttu-id="757e2-147">請注意，您不需要設定內部處理常式;Web API 架構會自動連接訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-147">Notice that you don't need to set the inner handlers; the Web API framework automatically connects the message handlers.</span></span>

<span data-ttu-id="757e2-148">如果您是[自我裝載](../older-versions/self-host-a-web-api.md)，請建立**HttpSelfHostConfiguration**類別的實例，並將處理常式新增至**MessageHandlers**集合。</span><span class="sxs-lookup"><span data-stu-id="757e2-148">If you are [self-hosting](../older-versions/self-host-a-web-api.md), create an instance of the **HttpSelfHostConfiguration** class and add the handlers to the **MessageHandlers** collection.</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample5.cs)]

<span data-ttu-id="757e2-149">現在讓我們來看一些自訂訊息處理常式的範例。</span><span class="sxs-lookup"><span data-stu-id="757e2-149">Now let's look at some examples of custom message handlers.</span></span>

## <a name="example-x-http-method-override"></a><span data-ttu-id="757e2-150">範例： X-HTTP-方法-覆寫</span><span class="sxs-lookup"><span data-stu-id="757e2-150">Example: X-HTTP-Method-Override</span></span>

<span data-ttu-id="757e2-151">X-HTTP-方法-覆寫是非標準的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="757e2-151">X-HTTP-Method-Override is a non-standard HTTP header.</span></span> <span data-ttu-id="757e2-152">它是針對無法傳送特定 HTTP 要求類型的用戶端所設計，例如 PUT 或 DELETE。</span><span class="sxs-lookup"><span data-stu-id="757e2-152">It is designed for clients that cannot send certain HTTP request types, such as PUT or DELETE.</span></span> <span data-ttu-id="757e2-153">相反地，用戶端會傳送 POST 要求，並將 X-HTTP 方法覆寫標頭設定為所需的方法。</span><span class="sxs-lookup"><span data-stu-id="757e2-153">Instead, the client sends a POST request and sets the X-HTTP-Method-Override header to the desired method.</span></span> <span data-ttu-id="757e2-154">例如:</span><span class="sxs-lookup"><span data-stu-id="757e2-154">For example:</span></span>

[!code-console[Main](http-message-handlers/samples/sample6.cmd)]

<span data-ttu-id="757e2-155">以下是新增 X-HTTP 方法覆寫支援的訊息處理常式：</span><span class="sxs-lookup"><span data-stu-id="757e2-155">Here is a message handler that adds support for X-HTTP-Method-Override:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample7.cs)]

<span data-ttu-id="757e2-156">在**SendAsync**方法中，處理常式會檢查要求訊息是否為 POST 要求，以及它是否包含 X-HTTP 方法覆寫標頭。</span><span class="sxs-lookup"><span data-stu-id="757e2-156">In the **SendAsync** method, the handler checks whether the request message is a POST request, and whether it contains the X-HTTP-Method-Override header.</span></span> <span data-ttu-id="757e2-157">若是如此，它會驗證標頭值，然後修改要求方法。</span><span class="sxs-lookup"><span data-stu-id="757e2-157">If so, it validates the header value, and then modifies the request method.</span></span> <span data-ttu-id="757e2-158">最後，處理常式會呼叫 `base.SendAsync`，將訊息傳遞至下一個處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-158">Finally, the handler calls `base.SendAsync` to pass the message to the next handler.</span></span>

<span data-ttu-id="757e2-159">當要求到達**system.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**類別時， **system.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**會根據更新的要求方法來路由傳送要求。</span><span class="sxs-lookup"><span data-stu-id="757e2-159">When the request reaches the **HttpControllerDispatcher** class, **HttpControllerDispatcher** will route the request based on the updated request method.</span></span>

## <a name="example-adding-a-custom-response-header"></a><span data-ttu-id="757e2-160">範例：新增自訂回應標頭</span><span class="sxs-lookup"><span data-stu-id="757e2-160">Example: Adding a Custom Response Header</span></span>

<span data-ttu-id="757e2-161">以下是將自訂標頭新增至每個回應訊息的訊息處理常式：</span><span class="sxs-lookup"><span data-stu-id="757e2-161">Here is a message handler that adds a custom header to every response message:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample8.cs)]

<span data-ttu-id="757e2-162">首先，處理常式會呼叫 `base.SendAsync`，將要求傳遞至內部訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-162">First, the handler calls `base.SendAsync` to pass the request to the inner message handler.</span></span> <span data-ttu-id="757e2-163">內部處理常式會傳迴響應消息，但它會使用工作 **&lt;t&gt;** 物件以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="757e2-163">The inner handler returns a response message, but it does so asynchronously using a **Task&lt;T&gt;** object.</span></span> <span data-ttu-id="757e2-164">除非 `base.SendAsync` 非同步完成，否則無法使用回應訊息。</span><span class="sxs-lookup"><span data-stu-id="757e2-164">The response message is not available until `base.SendAsync` completes asynchronously.</span></span>

<span data-ttu-id="757e2-165">這個範例會使用**await**關鍵字，在 `SendAsync` 完成後以非同步方式執行工作。</span><span class="sxs-lookup"><span data-stu-id="757e2-165">This example uses the **await** keyword to perform work asynchronously after `SendAsync` completes.</span></span> <span data-ttu-id="757e2-166">如果您的目標是 .NET Framework 4.0，請**使用&lt;t**&gt;的工作 **。System.threading.tasks.task.continuewith**方法：</span><span class="sxs-lookup"><span data-stu-id="757e2-166">If you are targeting .NET Framework 4.0, use the **Task**&lt;T&gt;**.ContinueWith** method:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample9.cs)]

## <a name="example-checking-for-an-api-key"></a><span data-ttu-id="757e2-167">範例：檢查 API 金鑰</span><span class="sxs-lookup"><span data-stu-id="757e2-167">Example: Checking for an API Key</span></span>

<span data-ttu-id="757e2-168">某些 web 服務要求用戶端在其要求中包含 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="757e2-168">Some web services require clients to include an API key in their request.</span></span> <span data-ttu-id="757e2-169">下列範例會顯示訊息處理常式如何檢查有效 API 金鑰的要求：</span><span class="sxs-lookup"><span data-stu-id="757e2-169">The following example shows how a message handler can check requests for a valid API key:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample10.cs)]

<span data-ttu-id="757e2-170">此處理程式會在 URI 查詢字串中尋找 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="757e2-170">This handler looks for the API key in the URI query string.</span></span> <span data-ttu-id="757e2-171">（在此範例中，我們假設金鑰是靜態字串。</span><span class="sxs-lookup"><span data-stu-id="757e2-171">(For this example, we assume that the key is a static string.</span></span> <span data-ttu-id="757e2-172">實際的執行可能會使用更複雜的驗證。）如果查詢字串包含索引鍵，則處理常式會將要求傳遞給內部處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-172">A real implementation would probably use more complex validation.) If the query string contains the key, the handler passes the request to the inner handler.</span></span>

<span data-ttu-id="757e2-173">如果要求沒有有效的索引鍵，則處理常式會建立狀態為403、禁止的回應訊息。</span><span class="sxs-lookup"><span data-stu-id="757e2-173">If the request does not have a valid key, the handler creates a response message with status 403, Forbidden.</span></span> <span data-ttu-id="757e2-174">在此情況下，處理常式不會呼叫 `base.SendAsync`，因此內部處理常式永遠不會接收要求，也不會執行控制器。</span><span class="sxs-lookup"><span data-stu-id="757e2-174">In this case, the handler does not call `base.SendAsync`, so the inner handler never receives the request, nor does the controller.</span></span> <span data-ttu-id="757e2-175">因此，控制器可以假設所有連入要求都具有有效的 API 金鑰。</span><span class="sxs-lookup"><span data-stu-id="757e2-175">Therefore, the controller can assume that all incoming requests have a valid API key.</span></span>

> [!NOTE]
> <span data-ttu-id="757e2-176">如果 API 金鑰僅適用于特定的控制器動作，請考慮使用動作篩選，而不是訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="757e2-176">If the API key applies only to certain controller actions, consider using an action filter instead of a message handler.</span></span> <span data-ttu-id="757e2-177">動作篩選準則會在 URI 路由執行之後執行。</span><span class="sxs-lookup"><span data-stu-id="757e2-177">Action filters run after URI routing is performed.</span></span>

## <a name="per-route-message-handlers"></a><span data-ttu-id="757e2-178">每個路由訊息處理常式</span><span class="sxs-lookup"><span data-stu-id="757e2-178">Per-Route Message Handlers</span></span>

<span data-ttu-id="757e2-179">**HttpConfiguration. MessageHandlers**集合中的處理常式會全域套用。</span><span class="sxs-lookup"><span data-stu-id="757e2-179">Handlers in the **HttpConfiguration.MessageHandlers** collection apply globally.</span></span>

<span data-ttu-id="757e2-180">或者，您可以在定義路由時，將訊息處理常式新增至特定的路由：</span><span class="sxs-lookup"><span data-stu-id="757e2-180">Alternatively, you can add a message handler to a specific route when you define the route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample11.cs?highlight=16)]

<span data-ttu-id="757e2-181">在此範例中，如果要求 URI 符合 "Route2"，則會將要求分派給 `MessageHandler2`。</span><span class="sxs-lookup"><span data-stu-id="757e2-181">In this example, if the request URI matches "Route2", the request is dispatched to `MessageHandler2`.</span></span> <span data-ttu-id="757e2-182">下圖顯示這兩個路由的管線：</span><span class="sxs-lookup"><span data-stu-id="757e2-182">The following diagram shows the pipeline for these two routes:</span></span>

![](http-message-handlers/_static/image4.png)

<span data-ttu-id="757e2-183">請注意，`MessageHandler2` 取代預設的**system.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**。</span><span class="sxs-lookup"><span data-stu-id="757e2-183">Notice that `MessageHandler2` replaces the default **HttpControllerDispatcher**.</span></span> <span data-ttu-id="757e2-184">在此範例中，`MessageHandler2` 會建立回應，且符合 "Route2" 的要求永遠不會移至控制器。</span><span class="sxs-lookup"><span data-stu-id="757e2-184">In this example, `MessageHandler2` creates the response, and requests that match "Route2" never go to a controller.</span></span> <span data-ttu-id="757e2-185">這可讓您將整個 Web API 控制器機制取代為您自己的自訂端點。</span><span class="sxs-lookup"><span data-stu-id="757e2-185">This lets you replace the entire Web API controller mechanism with your own custom endpoint.</span></span>

<span data-ttu-id="757e2-186">或者，每個路由的訊息處理常式可以委派給**system.web.HTTP.exceptionhandling.exceptioncatchblocks.HTTPcontrollerdispatcher.sendasync**，然後再分派給控制器。</span><span class="sxs-lookup"><span data-stu-id="757e2-186">Alternatively, a per-route message handler can delegate to **HttpControllerDispatcher**, which then dispatches to a controller.</span></span>

![](http-message-handlers/_static/image5.png)

<span data-ttu-id="757e2-187">下列程式碼顯示如何設定此路由：</span><span class="sxs-lookup"><span data-stu-id="757e2-187">The following code shows how to configure this route:</span></span>

[!code-csharp[Main](http-message-handlers/samples/sample12.cs)]
