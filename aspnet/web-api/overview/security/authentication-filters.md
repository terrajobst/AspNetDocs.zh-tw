---
uid: web-api/overview/security/authentication-filters
title: ASP.NET Web API 2 中的驗證篩選器 |Microsoft Docs
author: MikeWasson
description: 驗證篩選器是驗證 HTTP 要求的元件。 Web API 2 和 MVC 5 都支援驗證篩選，但它們稍有不同 。
ms.author: riande
ms.date: 09/25/2014
ms.assetid: b9882e53-b3ca-4def-89b0-322846973ccb
msc.legacyurl: /web-api/overview/security/authentication-filters
msc.type: authoredcontent
ms.openlocfilehash: 2ef9e62a6c634237e920b6d7aba2127b835f959d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555885"
---
# <a name="authentication-filters-in-aspnet-web-api-2"></a><span data-ttu-id="797f7-104">ASP.NET Web API 2 中的驗證篩選</span><span class="sxs-lookup"><span data-stu-id="797f7-104">Authentication Filters in ASP.NET Web API 2</span></span>

<span data-ttu-id="797f7-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="797f7-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="797f7-106">驗證篩選器是驗證 HTTP 要求的元件。</span><span class="sxs-lookup"><span data-stu-id="797f7-106">An authentication filter is a component that authenticates an HTTP request.</span></span> <span data-ttu-id="797f7-107">Web API 2 和 MVC 5 都支援驗證篩選，但它們稍有不同，大部分都是在篩選器介面的命名慣例中。</span><span class="sxs-lookup"><span data-stu-id="797f7-107">Web API 2 and MVC 5 both support authentication filters, but they differ slightly, mostly in the naming conventions for the filter interface.</span></span> <span data-ttu-id="797f7-108">本主題描述 Web API 驗證篩選準則。</span><span class="sxs-lookup"><span data-stu-id="797f7-108">This topic describes Web API authentication filters.</span></span>

<span data-ttu-id="797f7-109">驗證篩選器可讓您設定個別控制器或動作的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="797f7-109">Authentication filters let you set an authentication scheme for individual controllers or actions.</span></span> <span data-ttu-id="797f7-110">如此一來，您的應用程式就可以針對不同的 HTTP 資源支援不同的驗證機制。</span><span class="sxs-lookup"><span data-stu-id="797f7-110">That way, your app can support different authentication mechanisms for different HTTP resources.</span></span>

<span data-ttu-id="797f7-111">在本文中，我將在[https://github.com/aspnet/samples](https://github.com/aspnet/samples)上顯示[基本驗證](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)範例中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="797f7-111">In this article, I'll show code from the [Basic Authentication](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) sample on [https://github.com/aspnet/samples](https://github.com/aspnet/samples).</span></span> <span data-ttu-id="797f7-112">此範例顯示的驗證篩選準則會執行 HTTP 基本存取驗證配置（RFC 2617）。</span><span class="sxs-lookup"><span data-stu-id="797f7-112">The sample shows an authentication filter that implements the HTTP Basic Access Authentication scheme (RFC 2617).</span></span> <span data-ttu-id="797f7-113">此篩選準則會在名為 `IdentityBasicAuthenticationAttribute`的類別中執行。</span><span class="sxs-lookup"><span data-stu-id="797f7-113">The filter is implemented in a class named `IdentityBasicAuthenticationAttribute`.</span></span> <span data-ttu-id="797f7-114">我不會顯示範例中的所有程式碼，只是說明如何撰寫驗證篩選器的元件。</span><span class="sxs-lookup"><span data-stu-id="797f7-114">I won't show all of the code from the sample, just the parts that illustrate how to write an authentication filter.</span></span>

## <a name="setting-an-authentication-filter"></a><span data-ttu-id="797f7-115">設定驗證篩選準則</span><span class="sxs-lookup"><span data-stu-id="797f7-115">Setting an Authentication Filter</span></span>

<span data-ttu-id="797f7-116">就像其他篩選器一樣，驗證篩選器可以套用至每個控制器、每個動作，或全域套用至所有 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="797f7-116">Like other filters, authentication filters can be applied per-controller, per-action, or globally to all Web API controllers.</span></span>

<span data-ttu-id="797f7-117">若要將驗證篩選套用至控制器，請使用 filter 屬性裝飾控制器類別。</span><span class="sxs-lookup"><span data-stu-id="797f7-117">To apply an authentication filter to a controller, decorate the controller class with the filter attribute.</span></span> <span data-ttu-id="797f7-118">下列程式碼會在控制器類別上設定 `[IdentityBasicAuthentication]` 篩選準則，以啟用所有控制器動作的基本驗證。</span><span class="sxs-lookup"><span data-stu-id="797f7-118">The following code sets the `[IdentityBasicAuthentication]` filter on a controller class, which enables Basic Authentication for all of the controller's actions.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample1.cs)]

<span data-ttu-id="797f7-119">若要將篩選套用至一個動作，請使用篩選準則裝飾動作。</span><span class="sxs-lookup"><span data-stu-id="797f7-119">To apply the filter to one action, decorate the action with the filter.</span></span> <span data-ttu-id="797f7-120">下列程式碼會在控制器的 `Post` 方法上設定 `[IdentityBasicAuthentication]` 篩選準則。</span><span class="sxs-lookup"><span data-stu-id="797f7-120">The following code sets the `[IdentityBasicAuthentication]` filter on the controller's `Post` method.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample2.cs)]

<span data-ttu-id="797f7-121">若要將篩選套用至所有 Web API 控制器，請將它新增至**GlobalConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="797f7-121">To apply the filter to all Web API controllers, add it to **GlobalConfiguration.Filters**.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample3.cs)]

## <a name="implementing-a-web-api-authentication-filter"></a><span data-ttu-id="797f7-122">執行 Web API 驗證篩選</span><span class="sxs-lookup"><span data-stu-id="797f7-122">Implementing a Web API Authentication Filter</span></span>

<span data-ttu-id="797f7-123">在 Web API 中，驗證篩選準則會執行[IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx)介面。</span><span class="sxs-lookup"><span data-stu-id="797f7-123">In Web API, authentication filters implement the [System.Web.Http.Filters.IAuthenticationFilter](https://msdn.microsoft.com/library/system.web.http.filters.iauthenticationfilter.aspx) interface.</span></span> <span data-ttu-id="797f7-124">它們也應該繼承自**system.object**，以便套用為屬性。</span><span class="sxs-lookup"><span data-stu-id="797f7-124">They should also inherit from **System.Attribute**, in order to be applied as attributes.</span></span>

<span data-ttu-id="797f7-125">**IAuthenticationFilter**介面有兩個方法：</span><span class="sxs-lookup"><span data-stu-id="797f7-125">The **IAuthenticationFilter** interface has two methods:</span></span>

- <span data-ttu-id="797f7-126">**AuthenticateAsync**會驗證要求中的認證（如果有的話）來驗證要求。</span><span class="sxs-lookup"><span data-stu-id="797f7-126">**AuthenticateAsync** authenticates the request by validating credentials in the request, if present.</span></span>
- <span data-ttu-id="797f7-127">**ChallengeAsync**會視需要將驗證挑戰新增至 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-127">**ChallengeAsync** adds an authentication challenge to the HTTP response, if needed.</span></span>

<span data-ttu-id="797f7-128">這些方法對應于[rfc 2612](http://tools.ietf.org/html/rfc2616)和[rfc 2617](http://tools.ietf.org/html/rfc2617)中定義的驗證流程：</span><span class="sxs-lookup"><span data-stu-id="797f7-128">These methods correspond to the authentication flow defined in [RFC 2612](http://tools.ietf.org/html/rfc2616) and [RFC 2617](http://tools.ietf.org/html/rfc2617):</span></span>

1. <span data-ttu-id="797f7-129">用戶端會在授權標頭中傳送認證。</span><span class="sxs-lookup"><span data-stu-id="797f7-129">The client sends credentials in the Authorization header.</span></span> <span data-ttu-id="797f7-130">這通常是在用戶端從伺服器收到401（未經授權）回應之後發生。</span><span class="sxs-lookup"><span data-stu-id="797f7-130">This typically happens after the client receives a 401 (Unauthorized) response from the server.</span></span> <span data-ttu-id="797f7-131">不過，用戶端可以使用任何要求來傳送認證，而不只是在取得401之後。</span><span class="sxs-lookup"><span data-stu-id="797f7-131">However, a client can send credentials with any request, not just after getting a 401.</span></span>
2. <span data-ttu-id="797f7-132">如果伺服器不接受認證，則會傳回401（未經授權）的回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-132">If the server does not accept the credentials, it returns a 401 (Unauthorized) response.</span></span> <span data-ttu-id="797f7-133">回應包含 Www 驗證標頭，其中包含一或多個挑戰。</span><span class="sxs-lookup"><span data-stu-id="797f7-133">The response includes a Www-Authenticate header that contains one or more challenges.</span></span> <span data-ttu-id="797f7-134">每個挑戰都會指定伺服器所能辨識的驗證配置。</span><span class="sxs-lookup"><span data-stu-id="797f7-134">Each challenge specifies an authentication scheme recognized by the server.</span></span>

<span data-ttu-id="797f7-135">伺服器也可以從匿名要求傳回401。</span><span class="sxs-lookup"><span data-stu-id="797f7-135">The server can also return 401 from an anonymous request.</span></span> <span data-ttu-id="797f7-136">事實上，這通常是驗證程式的起始方式：</span><span class="sxs-lookup"><span data-stu-id="797f7-136">In fact, that's typically how the authentication process is initiated:</span></span>

1. <span data-ttu-id="797f7-137">用戶端會傳送匿名要求。</span><span class="sxs-lookup"><span data-stu-id="797f7-137">The client sends an anonymous request.</span></span>
2. <span data-ttu-id="797f7-138">伺服器會傳回401。</span><span class="sxs-lookup"><span data-stu-id="797f7-138">The server returns 401.</span></span>
3. <span data-ttu-id="797f7-139">用戶端會以認證重新傳送要求。</span><span class="sxs-lookup"><span data-stu-id="797f7-139">The clients resends the request with credentials.</span></span>

<span data-ttu-id="797f7-140">此流程包含*驗證*和*授權*步驟。</span><span class="sxs-lookup"><span data-stu-id="797f7-140">This flow includes both *authentication* and *authorization* steps.</span></span>

- <span data-ttu-id="797f7-141">驗證會證明用戶端的身分識別。</span><span class="sxs-lookup"><span data-stu-id="797f7-141">Authentication proves the identity of the client.</span></span>
- <span data-ttu-id="797f7-142">授權會決定用戶端是否可以存取特定資源。</span><span class="sxs-lookup"><span data-stu-id="797f7-142">Authorization determines whether the client can access a particular resource.</span></span>

<span data-ttu-id="797f7-143">在 Web API 中，驗證篩選器會處理驗證，而不是授權。</span><span class="sxs-lookup"><span data-stu-id="797f7-143">In Web API, authentication filters handle authentication, but not authorization.</span></span> <span data-ttu-id="797f7-144">授權應由授權篩選或在控制器動作內部完成。</span><span class="sxs-lookup"><span data-stu-id="797f7-144">Authorization should be done by an authorization filter or inside the controller action.</span></span>

<span data-ttu-id="797f7-145">以下是 Web API 2 管線中的流程：</span><span class="sxs-lookup"><span data-stu-id="797f7-145">Here is the flow in the Web API 2 pipeline:</span></span>

1. <span data-ttu-id="797f7-146">在叫用動作之前，Web API 會建立該動作的驗證篩選器清單。</span><span class="sxs-lookup"><span data-stu-id="797f7-146">Before invoking an action, Web API creates a list of the authentication filters for that action.</span></span> <span data-ttu-id="797f7-147">這包括具有動作範圍、控制器範圍和全域範圍的篩選準則。</span><span class="sxs-lookup"><span data-stu-id="797f7-147">This includes filters with action scope, controller scope, and global scope.</span></span>
2. <span data-ttu-id="797f7-148">Web API 會針對清單中的每個篩選呼叫**AuthenticateAsync** 。</span><span class="sxs-lookup"><span data-stu-id="797f7-148">Web API calls **AuthenticateAsync** on every filter in the list.</span></span> <span data-ttu-id="797f7-149">每個篩選器都可以驗證要求中的認證。</span><span class="sxs-lookup"><span data-stu-id="797f7-149">Each filter can validate credentials in the request.</span></span> <span data-ttu-id="797f7-150">如果有任何篩選成功驗證認證，篩選準則會建立**IPrincipal** ，並將它附加至要求。</span><span class="sxs-lookup"><span data-stu-id="797f7-150">If any filter successfully validates credentials, the filter creates an **IPrincipal** and attaches it to the request.</span></span> <span data-ttu-id="797f7-151">篩選準則也會在此時觸發錯誤。</span><span class="sxs-lookup"><span data-stu-id="797f7-151">A filter can also trigger an error at this point.</span></span> <span data-ttu-id="797f7-152">若是如此，管線的其餘部分就不會執行。</span><span class="sxs-lookup"><span data-stu-id="797f7-152">If so, the rest of the pipeline does not run.</span></span>
3. <span data-ttu-id="797f7-153">假設沒有發生錯誤，要求會流經管線的其餘部分。</span><span class="sxs-lookup"><span data-stu-id="797f7-153">Assuming there is no error, the request flows through the rest of the pipeline.</span></span>
4. <span data-ttu-id="797f7-154">最後，Web API 會呼叫每個驗證篩選器的**ChallengeAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="797f7-154">Finally, Web API calls every authentication filter's **ChallengeAsync** method.</span></span> <span data-ttu-id="797f7-155">篩選器會使用此方法，視需要將挑戰新增至回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-155">Filters use this method to add a challenge to the response, if needed.</span></span> <span data-ttu-id="797f7-156">通常（但不一定）會發生以回應401錯誤。</span><span class="sxs-lookup"><span data-stu-id="797f7-156">Typically (but not always) that would happen in response to a 401 error.</span></span>

<span data-ttu-id="797f7-157">下圖顯示兩個可能的案例。</span><span class="sxs-lookup"><span data-stu-id="797f7-157">The following diagrams show two possible cases.</span></span> <span data-ttu-id="797f7-158">在第一種情況下，驗證篩選器會成功驗證要求，授權篩選準則會授權要求，而控制器動作會傳回200（確定）。</span><span class="sxs-lookup"><span data-stu-id="797f7-158">In the first, the authentication filter successfully authenticates the request, an authorization filter authorizes the request, and the controller action returns 200 (OK).</span></span>

![](authentication-filters/_static/image1.png)

<span data-ttu-id="797f7-159">在第二個範例中，驗證篩選器會驗證要求，但授權篩選會傳回401（未經授權）。</span><span class="sxs-lookup"><span data-stu-id="797f7-159">In the second example, the authentication filter authenticates the request, but the authorization filter returns 401 (Unauthorized).</span></span> <span data-ttu-id="797f7-160">在此情況下，不會叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="797f7-160">In this case, the controller action is not invoked.</span></span> <span data-ttu-id="797f7-161">驗證篩選準則會將 Www 驗證標頭新增至回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-161">The authentication filter adds a Www-Authenticate header to the response.</span></span>

![](authentication-filters/_static/image2.png)

<span data-ttu-id="797f7-162">其他組合也可能&mdash;例如，如果控制器動作允許匿名要求，您可能會有驗證篩選準則，但沒有授權。</span><span class="sxs-lookup"><span data-stu-id="797f7-162">Other combinations are possible&mdash;for example, if the controller action allows anonymous requests, you might have an authentication filter but no authorization.</span></span>

## <a name="implementing-the-authenticateasync-method"></a><span data-ttu-id="797f7-163">執行 AuthenticateAsync 方法</span><span class="sxs-lookup"><span data-stu-id="797f7-163">Implementing the AuthenticateAsync Method</span></span>

<span data-ttu-id="797f7-164">**AuthenticateAsync**方法會嘗試驗證要求。</span><span class="sxs-lookup"><span data-stu-id="797f7-164">The **AuthenticateAsync** method tries to authenticate the request.</span></span> <span data-ttu-id="797f7-165">以下是方法簽章：</span><span class="sxs-lookup"><span data-stu-id="797f7-165">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample4.cs)]

<span data-ttu-id="797f7-166">**AuthenticateAsync**方法必須執行下列其中一項動作：</span><span class="sxs-lookup"><span data-stu-id="797f7-166">The **AuthenticateAsync** method must do one of the following:</span></span>

1. <span data-ttu-id="797f7-167">無（無 op）。</span><span class="sxs-lookup"><span data-stu-id="797f7-167">Nothing (no-op).</span></span>
2. <span data-ttu-id="797f7-168">建立**IPrincipal** ，並在要求上設定它。</span><span class="sxs-lookup"><span data-stu-id="797f7-168">Create an **IPrincipal** and set it on the request.</span></span>
3. <span data-ttu-id="797f7-169">設定錯誤結果。</span><span class="sxs-lookup"><span data-stu-id="797f7-169">Set an error result.</span></span>

<span data-ttu-id="797f7-170">選項（1）表示要求沒有篩選器所瞭解的任何認證。</span><span class="sxs-lookup"><span data-stu-id="797f7-170">Option (1) means the request did not have any credentials that the filter understands.</span></span> <span data-ttu-id="797f7-171">選項（2）表示篩選已成功驗證要求。</span><span class="sxs-lookup"><span data-stu-id="797f7-171">Option (2) means the filter successfully authenticated the request.</span></span> <span data-ttu-id="797f7-172">選項（3）表示要求具有不正確認證（例如錯誤的密碼），這會觸發錯誤回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-172">Option (3) means the request had invalid credentials (like the wrong password), which triggers an error response.</span></span>

<span data-ttu-id="797f7-173">以下是執行**AuthenticateAsync**的一般大綱。</span><span class="sxs-lookup"><span data-stu-id="797f7-173">Here is a general outline for implementing **AuthenticateAsync**.</span></span>

1. <span data-ttu-id="797f7-174">在要求中尋找認證。</span><span class="sxs-lookup"><span data-stu-id="797f7-174">Look for credentials in the request.</span></span>
2. <span data-ttu-id="797f7-175">如果沒有任何認證，則不執行任何動作，也不會傳回（無 op）。</span><span class="sxs-lookup"><span data-stu-id="797f7-175">If there are no credentials, do nothing and return (no-op).</span></span>
3. <span data-ttu-id="797f7-176">如果有認證，但篩選準則無法辨識驗證配置，則不執行任何動作，也不會傳回（無 op）。</span><span class="sxs-lookup"><span data-stu-id="797f7-176">If there are credentials but the filter does not recognize the authentication scheme, do nothing and return (no-op).</span></span> <span data-ttu-id="797f7-177">管線中的另一個篩選器可能會瞭解配置。</span><span class="sxs-lookup"><span data-stu-id="797f7-177">Another filter in the pipeline might understand the scheme.</span></span>
4. <span data-ttu-id="797f7-178">如果有篩選器瞭解的認證，請嘗試進行驗證。</span><span class="sxs-lookup"><span data-stu-id="797f7-178">If there are credentials that the filter understands, try to authenticate them.</span></span>
5. <span data-ttu-id="797f7-179">如果認證不正確，請設定 `context.ErrorResult`以傳回401。</span><span class="sxs-lookup"><span data-stu-id="797f7-179">If the credentials are bad, return 401 by setting `context.ErrorResult`.</span></span>
6. <span data-ttu-id="797f7-180">如果認證有效，請建立**IPrincipal** ，並設定 `context.Principal`。</span><span class="sxs-lookup"><span data-stu-id="797f7-180">If the credentials are valid, create an **IPrincipal** and set `context.Principal`.</span></span>

<span data-ttu-id="797f7-181">下列程式碼顯示[基本驗證](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication)範例中的**AuthenticateAsync**方法。</span><span class="sxs-lookup"><span data-stu-id="797f7-181">The follow code shows the **AuthenticateAsync** method from the [Basic Authentication](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/BasicAuthentication) sample.</span></span> <span data-ttu-id="797f7-182">批註會指出每個步驟。</span><span class="sxs-lookup"><span data-stu-id="797f7-182">The comments indicate each step.</span></span> <span data-ttu-id="797f7-183">程式碼會顯示數種類型的錯誤：沒有認證的授權標頭、認證格式不正確，以及使用者名稱/密碼不正確。</span><span class="sxs-lookup"><span data-stu-id="797f7-183">The code shows several types of error: An Authorization header with no credentials, malformed credentials, and bad username/password.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample5.cs)]

## <a name="setting-an-error-result"></a><span data-ttu-id="797f7-184">設定錯誤結果</span><span class="sxs-lookup"><span data-stu-id="797f7-184">Setting an Error Result</span></span>

<span data-ttu-id="797f7-185">如果認證無效，則篩選準則必須將 `context.ErrorResult` 設定為會建立錯誤回應的**應傳回 iHTTPactionresult** 。</span><span class="sxs-lookup"><span data-stu-id="797f7-185">If the credentials are invalid, the filter must set `context.ErrorResult` to an **IHttpActionResult** that creates an error response.</span></span> <span data-ttu-id="797f7-186">如需**應傳回 iHTTPactionresult**的詳細資訊，請參閱[Web API 2 中的動作結果](../getting-started-with-aspnet-web-api/action-results.md)。</span><span class="sxs-lookup"><span data-stu-id="797f7-186">For more information about **IHttpActionResult**, see [Action Results in Web API 2](../getting-started-with-aspnet-web-api/action-results.md).</span></span>

<span data-ttu-id="797f7-187">基本驗證範例包含適用于此用途的 `AuthenticationFailureResult` 類別。</span><span class="sxs-lookup"><span data-stu-id="797f7-187">The Basic Authentication sample includes an `AuthenticationFailureResult` class that is suitable for this purpose.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample6.cs)]

## <a name="implementing-challengeasync"></a><span data-ttu-id="797f7-188">執行 ChallengeAsync</span><span class="sxs-lookup"><span data-stu-id="797f7-188">Implementing ChallengeAsync</span></span>

<span data-ttu-id="797f7-189">**ChallengeAsync**方法的目的是要在需要時，將驗證挑戰新增至回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-189">The purpose of the **ChallengeAsync** method is to add authentication challenges to the response, if needed.</span></span> <span data-ttu-id="797f7-190">以下是方法簽章：</span><span class="sxs-lookup"><span data-stu-id="797f7-190">Here is the method signature:</span></span>

[!code-csharp[Main](authentication-filters/samples/sample7.cs)]

<span data-ttu-id="797f7-191">方法是在要求管線中的每個驗證篩選準則上呼叫。</span><span class="sxs-lookup"><span data-stu-id="797f7-191">The method is called on every authentication filter in the request pipeline.</span></span>

<span data-ttu-id="797f7-192">請務必瞭解， **ChallengeAsync**是在建立 HTTP 回應*之前*呼叫，甚至可能在控制器動作執行之前進行。</span><span class="sxs-lookup"><span data-stu-id="797f7-192">It's important to understand that **ChallengeAsync** is called *before* the HTTP response is created, and possibly even before the controller action runs.</span></span> <span data-ttu-id="797f7-193">呼叫**ChallengeAsync**時，`context.Result` 包含**應傳回 iHTTPactionresult**，稍後用來建立 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-193">When **ChallengeAsync** is called, `context.Result` contains an **IHttpActionResult**, which is used later to create the HTTP response.</span></span> <span data-ttu-id="797f7-194">因此，在呼叫**ChallengeAsync**時，您還不知道 HTTP 回應的任何內容。</span><span class="sxs-lookup"><span data-stu-id="797f7-194">So when **ChallengeAsync** is called, you don't know anything about the HTTP response yet.</span></span> <span data-ttu-id="797f7-195">**ChallengeAsync**方法應該以新的**應傳回 iHTTPactionresult**取代 `context.Result` 的原始值。</span><span class="sxs-lookup"><span data-stu-id="797f7-195">The **ChallengeAsync** method should replace the original value of `context.Result` with a new **IHttpActionResult**.</span></span> <span data-ttu-id="797f7-196">此**應傳回 iHTTPactionresult**必須包裝原始 `context.Result`。</span><span class="sxs-lookup"><span data-stu-id="797f7-196">This **IHttpActionResult** must wrap the original `context.Result`.</span></span>

![](authentication-filters/_static/image3.png)

<span data-ttu-id="797f7-197">我會呼叫*內部結果*的原始**應傳回 iHTTPactionresult** ，而新的會**應傳回 iHTTPactionresult** *外部結果*。</span><span class="sxs-lookup"><span data-stu-id="797f7-197">I'll call the original **IHttpActionResult** the *inner result*, and the new **IHttpActionResult** the *outer result*.</span></span> <span data-ttu-id="797f7-198">外部結果必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="797f7-198">The outer result must do the following:</span></span>

1. <span data-ttu-id="797f7-199">叫用內部結果以建立 HTTP 回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-199">Invoke the inner result to create the HTTP response.</span></span>
2. <span data-ttu-id="797f7-200">檢查回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-200">Examine the response.</span></span>
3. <span data-ttu-id="797f7-201">如有需要，請將驗證挑戰新增至回應。</span><span class="sxs-lookup"><span data-stu-id="797f7-201">Add an authentication challenge to the response, if needed.</span></span>

<span data-ttu-id="797f7-202">下列範例取自基本驗證範例。</span><span class="sxs-lookup"><span data-stu-id="797f7-202">The following example is taken from the Basic Authentication sample.</span></span> <span data-ttu-id="797f7-203">它會定義外部結果的**應傳回 iHTTPactionresult** 。</span><span class="sxs-lookup"><span data-stu-id="797f7-203">It defines an **IHttpActionResult** for the outer result.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample8.cs)]

<span data-ttu-id="797f7-204">`InnerResult` 屬性會保存內部**應傳回 iHTTPactionresult**。</span><span class="sxs-lookup"><span data-stu-id="797f7-204">The `InnerResult` property holds the inner **IHttpActionResult**.</span></span> <span data-ttu-id="797f7-205">`Challenge` 屬性代表 Www 驗證標頭。</span><span class="sxs-lookup"><span data-stu-id="797f7-205">The `Challenge` property represents a Www-Authentication header.</span></span> <span data-ttu-id="797f7-206">請注意， **ExecuteAsync**會先呼叫 `InnerResult.ExecuteAsync` 來建立 HTTP 回應，然後視需要新增挑戰。</span><span class="sxs-lookup"><span data-stu-id="797f7-206">Notice that **ExecuteAsync** first calls `InnerResult.ExecuteAsync` to create the HTTP response, and then adds the challenge if needed.</span></span>

<span data-ttu-id="797f7-207">請檢查回應碼，然後再新增挑戰。</span><span class="sxs-lookup"><span data-stu-id="797f7-207">Check the response code before adding the challenge.</span></span> <span data-ttu-id="797f7-208">如果回應為401，大部分的驗證配置只會新增挑戰，如下所示。</span><span class="sxs-lookup"><span data-stu-id="797f7-208">Most authentication schemes only add a challenge if the response is 401, as shown here.</span></span> <span data-ttu-id="797f7-209">不過，某些驗證配置會對成功回應新增挑戰。</span><span class="sxs-lookup"><span data-stu-id="797f7-209">However, some authentication schemes do add a challenge to a success response.</span></span> <span data-ttu-id="797f7-210">例如，請參閱[Negotiate](http://tools.ietf.org/html/rfc4559#section-5) （RFC 4559）。</span><span class="sxs-lookup"><span data-stu-id="797f7-210">For example, see [Negotiate](http://tools.ietf.org/html/rfc4559#section-5) (RFC 4559).</span></span>

<span data-ttu-id="797f7-211">假設有 `AddChallengeOnUnauthorizedResult` 類別，則**ChallengeAsync**中的實際程式碼很簡單。</span><span class="sxs-lookup"><span data-stu-id="797f7-211">Given the `AddChallengeOnUnauthorizedResult` class, the actual code in **ChallengeAsync** is simple.</span></span> <span data-ttu-id="797f7-212">您只需建立結果，並將其附加至 `context.Result`。</span><span class="sxs-lookup"><span data-stu-id="797f7-212">You just create the result and attach it to `context.Result`.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample9.cs)]

<span data-ttu-id="797f7-213">注意：基本驗證範例會將此邏輯一併放在擴充方法中，藉此將它抽象化。</span><span class="sxs-lookup"><span data-stu-id="797f7-213">Note: The Basic Authentication sample abstracts this logic a bit, by placing it in an extension method.</span></span>

## <a name="combining-authentication-filters-with-host-level-authentication"></a><span data-ttu-id="797f7-214">將驗證篩選器與主機層級驗證結合</span><span class="sxs-lookup"><span data-stu-id="797f7-214">Combining Authentication Filters with Host-Level Authentication</span></span>

<span data-ttu-id="797f7-215">「主機層級驗證」是由主機（例如 IIS）執行的驗證，在要求到達 Web API 架構之前。</span><span class="sxs-lookup"><span data-stu-id="797f7-215">"Host-level authentication" is authentication performed by the host (such as IIS), before the request reaches the Web API framework.</span></span>

<span data-ttu-id="797f7-216">通常，您可能會想要為應用程式的其餘部分啟用主機層級驗證，但請將它停用於您的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="797f7-216">Often, you may want to enable host-level authentication for the rest of your application, but disable it for your Web API controllers.</span></span> <span data-ttu-id="797f7-217">例如，典型的案例是在主機層級啟用表單驗證，但針對 Web API 使用權杖型驗證。</span><span class="sxs-lookup"><span data-stu-id="797f7-217">For example, a typical scenario is to enable Forms Authentication at the host level, but use token-based authentication for Web API.</span></span>

<span data-ttu-id="797f7-218">若要在 Web API 管線內停用主機層級驗證，請在您的設定中呼叫 `config.SuppressHostPrincipal()`。</span><span class="sxs-lookup"><span data-stu-id="797f7-218">To disable host-level authentication inside the Web API pipeline, call `config.SuppressHostPrincipal()` in your configuration.</span></span> <span data-ttu-id="797f7-219">這會導致 Web API 從輸入 Web API 管線的任何要求中移除**IPrincipal** 。</span><span class="sxs-lookup"><span data-stu-id="797f7-219">This causes Web API to remove the **IPrincipal** from any request that enters the Web API pipeline.</span></span> <span data-ttu-id="797f7-220">實際上，它 &quot;取消驗證要求&quot;。</span><span class="sxs-lookup"><span data-stu-id="797f7-220">Effectively, it &quot;un-authenticates&quot; the request.</span></span>

[!code-csharp[Main](authentication-filters/samples/sample10.cs)]

## <a name="additional-resources"></a><span data-ttu-id="797f7-221">其他資源</span><span class="sxs-lookup"><span data-stu-id="797f7-221">Additional Resources</span></span>

<span data-ttu-id="797f7-222">[ASP.NET Web API 安全性篩選](https://msdn.microsoft.com/magazine/dn781361.aspx)（MSDN 雜誌）</span><span class="sxs-lookup"><span data-stu-id="797f7-222">[ASP.NET Web API Security Filters](https://msdn.microsoft.com/magazine/dn781361.aspx) (MSDN Magazine)</span></span>
