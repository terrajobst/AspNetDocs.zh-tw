---
uid: web-api/overview/getting-started-with-aspnet-web-api/action-results
title: Web API 2-ASP.NET 4.x 中的動作結果
author: MikeWasson
description: 描述 ASP.NET Web API 如何將控制器動作的傳回值轉換成 ASP.NET 4.x 中的 HTTP 回應訊息。
ms.author: riande
ms.date: 02/03/2014
ms.custom: seoapril2019
ms.assetid: 2fc4797c-38ef-4cc7-926c-ca431c4739e8
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/action-results
msc.type: authoredcontent
ms.openlocfilehash: f00ac0db453053e53d6d6942dd1557b409f4167b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557054"
---
# <a name="action-results-in-web-api-2"></a><span data-ttu-id="cd3e3-103">Web API 2 中的動作結果</span><span class="sxs-lookup"><span data-stu-id="cd3e3-103">Action Results in Web API 2</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="cd3e3-104">本主題描述 ASP.NET Web API 如何將控制器動作的傳回值轉換為 HTTP 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-104">This topic describes how ASP.NET Web API converts the return value from a controller action into an HTTP response message.</span></span>

<span data-ttu-id="cd3e3-105">Web API 控制器動作可以傳回下列任何一項：</span><span class="sxs-lookup"><span data-stu-id="cd3e3-105">A Web API controller action can return any of the following:</span></span>

1. <span data-ttu-id="cd3e3-106">void</span><span class="sxs-lookup"><span data-stu-id="cd3e3-106">void</span></span>
2. <span data-ttu-id="cd3e3-107">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="cd3e3-107">**HttpResponseMessage**</span></span>
3. <span data-ttu-id="cd3e3-108">**應傳回 iHTTPactionresult**</span><span class="sxs-lookup"><span data-stu-id="cd3e3-108">**IHttpActionResult**</span></span>
4. <span data-ttu-id="cd3e3-109">其他類型</span><span class="sxs-lookup"><span data-stu-id="cd3e3-109">Some other type</span></span>

<span data-ttu-id="cd3e3-110">根據傳回的是哪一個，Web API 會使用不同的機制來建立 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-110">Depending on which of these is returned, Web API uses a different mechanism to create the HTTP response.</span></span>

| <span data-ttu-id="cd3e3-111">傳回類型</span><span class="sxs-lookup"><span data-stu-id="cd3e3-111">Return type</span></span> | <span data-ttu-id="cd3e3-112">Web API 如何建立回應</span><span class="sxs-lookup"><span data-stu-id="cd3e3-112">How Web API creates the response</span></span> |
| --- | --- |
| <span data-ttu-id="cd3e3-113">void</span><span class="sxs-lookup"><span data-stu-id="cd3e3-113">void</span></span> | <span data-ttu-id="cd3e3-114">傳回空的204（沒有內容）</span><span class="sxs-lookup"><span data-stu-id="cd3e3-114">Return empty 204 (No Content)</span></span> |
| <span data-ttu-id="cd3e3-115">**HttpResponseMessage**</span><span class="sxs-lookup"><span data-stu-id="cd3e3-115">**HttpResponseMessage**</span></span> | <span data-ttu-id="cd3e3-116">直接轉換為 HTTP 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-116">Convert directly to an HTTP response message.</span></span> |
| <span data-ttu-id="cd3e3-117">**應傳回 iHTTPactionresult**</span><span class="sxs-lookup"><span data-stu-id="cd3e3-117">**IHttpActionResult**</span></span> | <span data-ttu-id="cd3e3-118">呼叫**ExecuteAsync**以建立**HttpResponseMessage**，然後轉換為 HTTP 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-118">Call **ExecuteAsync** to create an **HttpResponseMessage**, then convert to an HTTP response message.</span></span> |
| <span data-ttu-id="cd3e3-119">其他類型</span><span class="sxs-lookup"><span data-stu-id="cd3e3-119">Other type</span></span> | <span data-ttu-id="cd3e3-120">將序列化的傳回值寫入回應主體;傳回200（確定）。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-120">Write the serialized return value into the response body; return 200 (OK).</span></span> |

<span data-ttu-id="cd3e3-121">本主題的其餘部分將更詳細地說明每個選項。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-121">The rest of this topic describes each option in more detail.</span></span>

## <a name="void"></a><span data-ttu-id="cd3e3-122">void</span><span class="sxs-lookup"><span data-stu-id="cd3e3-122">void</span></span>

<span data-ttu-id="cd3e3-123">如果傳回型別為 `void`，Web API 只會傳回空的 HTTP 回應，狀態碼為204（沒有內容）。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-123">If the return type is `void`, Web API simply returns an empty HTTP response with status code 204 (No Content).</span></span>

<span data-ttu-id="cd3e3-124">範例控制器：</span><span class="sxs-lookup"><span data-stu-id="cd3e3-124">Example controller:</span></span>

[!code-csharp[Main](action-results/samples/sample1.cs)]

<span data-ttu-id="cd3e3-125">HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="cd3e3-125">HTTP response:</span></span>

[!code-console[Main](action-results/samples/sample2.cmd)]

## <a name="httpresponsemessage"></a><span data-ttu-id="cd3e3-126">HTTPResponseMessage</span><span class="sxs-lookup"><span data-stu-id="cd3e3-126">HttpResponseMessage</span></span>

<span data-ttu-id="cd3e3-127">如果動作傳回[HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx)，Web API 會使用**HttpResponseMessage**物件的屬性來填入回應，將傳回值直接轉換為 HTTP 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-127">If the action returns an [HttpResponseMessage](https://msdn.microsoft.com/library/system.net.http.httpresponsemessage.aspx), Web API converts the return value directly into an HTTP response message, using the properties of the **HttpResponseMessage** object to populate the response.</span></span>

<span data-ttu-id="cd3e3-128">此選項可讓您對回應訊息有很大的控制權。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-128">This option gives you a lot of control over the response message.</span></span> <span data-ttu-id="cd3e3-129">例如，下列控制器動作會設定快取控制標頭。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-129">For example, the following controller action sets the Cache-Control header.</span></span>

[!code-csharp[Main](action-results/samples/sample3.cs)]

<span data-ttu-id="cd3e3-130">回應：</span><span class="sxs-lookup"><span data-stu-id="cd3e3-130">Response:</span></span>

[!code-console[Main](action-results/samples/sample4.cmd?highlight=2)]

<span data-ttu-id="cd3e3-131">如果您將領域模型傳遞至**CreateResponse**方法，Web API 會使用[媒體格式](../formats-and-model-binding/media-formatters.md)器將序列化的模型寫入回應主體。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-131">If you pass a domain model to the **CreateResponse** method, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to write the serialized model into the response body.</span></span>

[!code-csharp[Main](action-results/samples/sample5.cs)]

<span data-ttu-id="cd3e3-132">Web API 會在要求中使用 Accept 標頭來選擇格式器。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-132">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="cd3e3-133">如需詳細資訊，請參閱[內容協商](../formats-and-model-binding/content-negotiation.md)。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-133">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

## <a name="ihttpactionresult"></a><span data-ttu-id="cd3e3-134">應傳回 iHTTPactionresult</span><span class="sxs-lookup"><span data-stu-id="cd3e3-134">IHttpActionResult</span></span>

<span data-ttu-id="cd3e3-135">**應傳回 iHTTPactionresult**介面是在 Web API 2 中引進。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-135">The **IHttpActionResult** interface was introduced in Web API 2.</span></span> <span data-ttu-id="cd3e3-136">基本上，它會定義**HttpResponseMessage** factory。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-136">Essentially, it defines an **HttpResponseMessage** factory.</span></span> <span data-ttu-id="cd3e3-137">以下是使用**應傳回 iHTTPactionresult**介面的一些優點：</span><span class="sxs-lookup"><span data-stu-id="cd3e3-137">Here are some advantages of using the **IHttpActionResult** interface:</span></span>

- <span data-ttu-id="cd3e3-138">簡化控制器的[單元測試](../testing-and-debugging/unit-testing-controllers-in-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-138">Simplifies [unit testing](../testing-and-debugging/unit-testing-controllers-in-web-api.md) your controllers.</span></span>
- <span data-ttu-id="cd3e3-139">將建立 HTTP 回應的常見邏輯移至不同的類別。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-139">Moves common logic for creating HTTP responses into separate classes.</span></span>
- <span data-ttu-id="cd3e3-140">藉由隱藏用來建立回應的低層級詳細資料，讓控制器動作的意圖更清楚。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-140">Makes the intent of the controller action clearer, by hiding the low-level details of constructing the response.</span></span>

<span data-ttu-id="cd3e3-141">**應傳回 iHTTPactionresult**包含單一方法**ExecuteAsync**，它會以非同步方式建立**HttpResponseMessage**實例。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-141">**IHttpActionResult** contains a single method, **ExecuteAsync**, which asynchronously creates an **HttpResponseMessage** instance.</span></span>

[!code-csharp[Main](action-results/samples/sample6.cs)]

<span data-ttu-id="cd3e3-142">如果控制器動作傳回**應傳回 iHTTPactionresult**，Web API 會呼叫**ExecuteAsync**方法來建立**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-142">If a controller action returns an **IHttpActionResult**, Web API calls the **ExecuteAsync** method to create an **HttpResponseMessage**.</span></span> <span data-ttu-id="cd3e3-143">然後，它會將**HttpResponseMessage**轉換為 HTTP 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-143">Then it converts the **HttpResponseMessage** into an HTTP response message.</span></span>

<span data-ttu-id="cd3e3-144">以下是簡單的**應傳回 iHTTPactionresult**執行，可建立純文字回應：</span><span class="sxs-lookup"><span data-stu-id="cd3e3-144">Here is a simple implementation of **IHttpActionResult** that creates a plain text response:</span></span>

[!code-csharp[Main](action-results/samples/sample7.cs)]

<span data-ttu-id="cd3e3-145">範例控制器動作：</span><span class="sxs-lookup"><span data-stu-id="cd3e3-145">Example controller action:</span></span>

[!code-csharp[Main](action-results/samples/sample8.cs)]

<span data-ttu-id="cd3e3-146">回應：</span><span class="sxs-lookup"><span data-stu-id="cd3e3-146">Response:</span></span>

[!code-console[Main](action-results/samples/sample9.cmd)]

<span data-ttu-id="cd3e3-147">通常，您會使用在 **[system.web. HTTP.sys](https://msdn.microsoft.com/library/system.web.http.results.aspx)** 命名空間中定義的**應傳回 iHTTPactionresult**部署。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-147">More often, you use the **IHttpActionResult** implementations defined in the **[System.Web.Http.Results](https://msdn.microsoft.com/library/system.web.http.results.aspx)** namespace.</span></span> <span data-ttu-id="cd3e3-148">**ApiController**類別會定義可傳回這些內建動作結果的 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-148">The **ApiController** class defines helper methods that return these built-in action results.</span></span>

<span data-ttu-id="cd3e3-149">在下列範例中，如果要求不符合現有的產品識別碼，則控制器會呼叫[ApiController NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx)以建立404（找不到）回應。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-149">In the following example, if the request does not match an existing product ID, the controller calls [ApiController.NotFound](https://msdn.microsoft.com/library/system.web.http.apicontroller.notfound.aspx) to create a 404 (Not Found) response.</span></span> <span data-ttu-id="cd3e3-150">否則，控制器會呼叫[ApiController](https://msdn.microsoft.com/library/dn314591.aspx)，這會建立包含產品的200（確定）回應。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-150">Otherwise, the controller calls [ApiController.OK](https://msdn.microsoft.com/library/dn314591.aspx), which creates a 200 (OK) response that contains the product.</span></span>

[!code-csharp[Main](action-results/samples/sample10.cs)]

## <a name="other-return-types"></a><span data-ttu-id="cd3e3-151">其他傳回類型</span><span class="sxs-lookup"><span data-stu-id="cd3e3-151">Other Return Types</span></span>

<span data-ttu-id="cd3e3-152">針對所有其他傳回類型，Web API 會使用[媒體格式](../formats-and-model-binding/media-formatters.md)器來序列化傳回值。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-152">For all other return types, Web API uses a [media formatter](../formats-and-model-binding/media-formatters.md) to serialize the return value.</span></span> <span data-ttu-id="cd3e3-153">Web API 會將序列化的值寫入回應主體。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-153">Web API writes the serialized value into the response body.</span></span> <span data-ttu-id="cd3e3-154">回應狀態碼為200（確定）。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-154">The response status code is 200 (OK).</span></span>

[!code-csharp[Main](action-results/samples/sample11.cs)]

<span data-ttu-id="cd3e3-155">這種方法的缺點是您無法直接傳回錯誤碼，例如404。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-155">A disadvantage of this approach is that you cannot directly return an error code, such as 404.</span></span> <span data-ttu-id="cd3e3-156">不過，您可以擲回錯誤碼的**HttpResponseException** 。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-156">However, you can throw an **HttpResponseException** for error codes.</span></span> <span data-ttu-id="cd3e3-157">如需詳細資訊，請參閱[ASP.NET Web API 中的例外狀況處理](../error-handling/exception-handling.md)。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-157">For more information, see [Exception Handling in ASP.NET Web API](../error-handling/exception-handling.md).</span></span>

<span data-ttu-id="cd3e3-158">Web API 會在要求中使用 Accept 標頭來選擇格式器。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-158">Web API uses the Accept header in the request to choose the formatter.</span></span> <span data-ttu-id="cd3e3-159">如需詳細資訊，請參閱[內容協商](../formats-and-model-binding/content-negotiation.md)。</span><span class="sxs-lookup"><span data-stu-id="cd3e3-159">For more information, see [Content Negotiation](../formats-and-model-binding/content-negotiation.md).</span></span>

<span data-ttu-id="cd3e3-160">範例要求</span><span class="sxs-lookup"><span data-stu-id="cd3e3-160">Example request</span></span>

[!code-console[Main](action-results/samples/sample12.cmd)]

<span data-ttu-id="cd3e3-161">範例回應</span><span class="sxs-lookup"><span data-stu-id="cd3e3-161">Example response</span></span>

[!code-console[Main](action-results/samples/sample13.cmd)]
