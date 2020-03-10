---
uid: web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
title: ASP.NET Web API 中的驗證和授權 |Microsoft Docs
author: MikeWasson
description: 提供 ASP.NET Web API 中驗證和授權的一般總覽。
ms.author: riande
ms.date: 11/27/2012
ms.assetid: 6dfb51ea-9f4d-4e70-916c-8ef8344a88d6
msc.legacyurl: /web-api/overview/security/authentication-and-authorization-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 368d2b9456d12b2bb4063a23333e5c8837faa3b8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598641"
---
# <a name="authentication-and-authorization-in-aspnet-web-api"></a><span data-ttu-id="96063-103">ASP.NET Web API 中的驗證和授權</span><span class="sxs-lookup"><span data-stu-id="96063-103">Authentication and Authorization in ASP.NET Web API</span></span>

<span data-ttu-id="96063-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="96063-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="96063-105">您已建立 Web API，但現在您想要控制其存取權。</span><span class="sxs-lookup"><span data-stu-id="96063-105">You've created a web API, but now you want to control access to it.</span></span> <span data-ttu-id="96063-106">在這一系列的文章中，我們將探討一些從未經授權的使用者保護 Web API 的選項。</span><span class="sxs-lookup"><span data-stu-id="96063-106">In this series of articles, we'll look at some options for securing a web API from unauthorized users.</span></span> <span data-ttu-id="96063-107">本系列將涵蓋驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="96063-107">This series will cover both authentication and authorization.</span></span>

- <span data-ttu-id="96063-108">*驗證*會知道使用者的身分識別。</span><span class="sxs-lookup"><span data-stu-id="96063-108">*Authentication* is knowing the identity of the user.</span></span> <span data-ttu-id="96063-109">例如，Alice 以其使用者名稱和密碼登入，而伺服器使用密碼來驗證 Alice。</span><span class="sxs-lookup"><span data-stu-id="96063-109">For example, Alice logs in with her username and password, and the server uses the password to authenticate Alice.</span></span>
- <span data-ttu-id="96063-110">*授權*會決定是否允許使用者執行動作。</span><span class="sxs-lookup"><span data-stu-id="96063-110">*Authorization* is deciding whether a user is allowed to perform an action.</span></span> <span data-ttu-id="96063-111">例如，Alice 具有取得資源的許可權，但無法建立資源。</span><span class="sxs-lookup"><span data-stu-id="96063-111">For example, Alice has permission to get a resource but not create a resource.</span></span>

<span data-ttu-id="96063-112">本系列的第一篇文章提供 ASP.NET Web API 中驗證和授權的一般總覽。</span><span class="sxs-lookup"><span data-stu-id="96063-112">The first article in the series gives a general overview of authentication and authorization in ASP.NET Web API.</span></span> <span data-ttu-id="96063-113">其他主題描述 Web API 的常見驗證案例。</span><span class="sxs-lookup"><span data-stu-id="96063-113">Other topics describe common authentication scenarios for Web API.</span></span>

> [!NOTE]
> <span data-ttu-id="96063-114">感謝審查此系列並提供寶貴意見的人： Rick Anderson、Levi Broderick、Barry Dorrans、Tom 作者: dykstra、Hongmei Ge、David Matson、Daniel Roth、Tim Teebken。</span><span class="sxs-lookup"><span data-stu-id="96063-114">Thanks to the people who reviewed this series and provided valuable feedback: Rick Anderson, Levi Broderick, Barry Dorrans, Tom Dykstra, Hongmei Ge, David Matson, Daniel Roth, Tim Teebken.</span></span>

## <a name="authentication"></a><span data-ttu-id="96063-115">驗證</span><span class="sxs-lookup"><span data-stu-id="96063-115">Authentication</span></span>

<span data-ttu-id="96063-116">Web API 會假設在主機中進行驗證。</span><span class="sxs-lookup"><span data-stu-id="96063-116">Web API assumes that authentication happens in the host.</span></span> <span data-ttu-id="96063-117">若為 web 裝載，則主機是 IIS，它會使用 HTTP 模組進行驗證。</span><span class="sxs-lookup"><span data-stu-id="96063-117">For web-hosting, the host is IIS, which uses HTTP modules for authentication.</span></span> <span data-ttu-id="96063-118">您可以將專案設定為使用 IIS 或 ASP.NET 內建的任何驗證模組，或是撰寫您自己的 HTTP 模組來執行自訂驗證。</span><span class="sxs-lookup"><span data-stu-id="96063-118">You can configure your project to use any of the authentication modules built in to IIS or ASP.NET, or write your own HTTP module to perform custom authentication.</span></span>

<span data-ttu-id="96063-119">當主機驗證使用者時，它會建立一個*主體*，這是[IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx)物件，代表執行程式碼的安全性內容。</span><span class="sxs-lookup"><span data-stu-id="96063-119">When the host authenticates the user, it creates a *principal*, which is an [IPrincipal](https://msdn.microsoft.com/library/System.Security.Principal.IPrincipal.aspx) object that represents the security context under which code is running.</span></span> <span data-ttu-id="96063-120">主機會藉由設定**thread.currentprincipal**，將主體附加到目前的執行緒。</span><span class="sxs-lookup"><span data-stu-id="96063-120">The host attaches the principal to the current thread by setting **Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="96063-121">主體包含關聯的身分**識別**物件，其中包含使用者的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="96063-121">The principal contains an associated **Identity** object that contains information about the user.</span></span> <span data-ttu-id="96063-122">如果使用者經過驗證， **IsAuthenticated**屬性會傳回**true**。</span><span class="sxs-lookup"><span data-stu-id="96063-122">If the user is authenticated, the **Identity.IsAuthenticated** property returns **true**.</span></span> <span data-ttu-id="96063-123">若為匿名要求， **IsAuthenticated**會傳回**false**。</span><span class="sxs-lookup"><span data-stu-id="96063-123">For anonymous requests, **IsAuthenticated** returns **false**.</span></span> <span data-ttu-id="96063-124">如需主體的詳細資訊，請參閱以[角色為基礎的安全性](https://msdn.microsoft.com/library/shz8h065.aspx)。</span><span class="sxs-lookup"><span data-stu-id="96063-124">For more information about principals, see [Role-Based Security](https://msdn.microsoft.com/library/shz8h065.aspx).</span></span>

### <a name="http-message-handlers-for-authentication"></a><span data-ttu-id="96063-125">用於驗證的 HTTP 訊息處理常式</span><span class="sxs-lookup"><span data-stu-id="96063-125">HTTP Message Handlers for Authentication</span></span>

<span data-ttu-id="96063-126">您可以將驗證邏輯放入[HTTP 訊息處理常式](../advanced/http-message-handlers.md)中，而不是使用主機進行驗證。</span><span class="sxs-lookup"><span data-stu-id="96063-126">Instead of using the host for authentication, you can put authentication logic into an [HTTP message handler](../advanced/http-message-handlers.md).</span></span> <span data-ttu-id="96063-127">在這種情況下，訊息處理常式會檢查 HTTP 要求並設定主體。</span><span class="sxs-lookup"><span data-stu-id="96063-127">In that case, the message handler examines the HTTP request and sets the principal.</span></span>

<span data-ttu-id="96063-128">何時應該使用訊息處理常式進行驗證？</span><span class="sxs-lookup"><span data-stu-id="96063-128">When should you use message handlers for authentication?</span></span> <span data-ttu-id="96063-129">以下是一些取捨：</span><span class="sxs-lookup"><span data-stu-id="96063-129">Here are some tradeoffs:</span></span>

- <span data-ttu-id="96063-130">HTTP 模組會查看所有經過 ASP.NET 管線的要求。</span><span class="sxs-lookup"><span data-stu-id="96063-130">An HTTP module sees all requests that go through the ASP.NET pipeline.</span></span> <span data-ttu-id="96063-131">訊息處理常式只會看到路由至 Web API 的要求。</span><span class="sxs-lookup"><span data-stu-id="96063-131">A message handler only sees requests that are routed to Web API.</span></span>
- <span data-ttu-id="96063-132">您可以設定每個路由訊息處理常式，讓您將驗證配置套用至特定的路由。</span><span class="sxs-lookup"><span data-stu-id="96063-132">You can set per-route message handlers, which lets you apply an authentication scheme to a specific route.</span></span>
- <span data-ttu-id="96063-133">HTTP 模組是 IIS 特有的。</span><span class="sxs-lookup"><span data-stu-id="96063-133">HTTP modules are specific to IIS.</span></span> <span data-ttu-id="96063-134">訊息處理常式與主機無關，因此可與 web 裝載和自我裝載搭配使用。</span><span class="sxs-lookup"><span data-stu-id="96063-134">Message handlers are host-agnostic, so they can be used with both web-hosting and self-hosting.</span></span>
- <span data-ttu-id="96063-135">HTTP 模組會參與 IIS 記錄、審核等等。</span><span class="sxs-lookup"><span data-stu-id="96063-135">HTTP modules participate in IIS logging, auditing, and so on.</span></span>
- <span data-ttu-id="96063-136">HTTP 模組會在管線中稍早執行。</span><span class="sxs-lookup"><span data-stu-id="96063-136">HTTP modules run earlier in the pipeline.</span></span> <span data-ttu-id="96063-137">如果您在訊息處理常式中處理驗證，則在處理常式執行之前，不會設定主體。</span><span class="sxs-lookup"><span data-stu-id="96063-137">If you handle authentication in a message handler, the principal does not get set until the handler runs.</span></span> <span data-ttu-id="96063-138">此外，當回應離開訊息處理常式時，主體會還原回前一個主體。</span><span class="sxs-lookup"><span data-stu-id="96063-138">Moreover, the principal reverts back to the previous principal when the response leaves the message handler.</span></span>

<span data-ttu-id="96063-139">一般來說，如果您不需要支援自我裝載，HTTP 模組就是較好的選擇。</span><span class="sxs-lookup"><span data-stu-id="96063-139">Generally, if you don't need to support self-hosting, an HTTP module is a better option.</span></span> <span data-ttu-id="96063-140">如果您需要支援自我裝載，請考慮使用訊息處理常式。</span><span class="sxs-lookup"><span data-stu-id="96063-140">If you need to support self-hosting, consider a message handler.</span></span>

### <a name="setting-the-principal"></a><span data-ttu-id="96063-141">設定主體</span><span class="sxs-lookup"><span data-stu-id="96063-141">Setting the Principal</span></span>

<span data-ttu-id="96063-142">如果您的應用程式執行任何自訂驗證邏輯，您必須在兩個地方設定主體：</span><span class="sxs-lookup"><span data-stu-id="96063-142">If your application performs any custom authentication logic, you must set the principal on two places:</span></span>

- <span data-ttu-id="96063-143">**Thread.currentprincipal**。</span><span class="sxs-lookup"><span data-stu-id="96063-143">**Thread.CurrentPrincipal**.</span></span> <span data-ttu-id="96063-144">這個屬性是在 .NET 中設定執行緒主體的標準方式。</span><span class="sxs-lookup"><span data-stu-id="96063-144">This property is the standard way to set the thread's principal in .NET.</span></span>
- <span data-ttu-id="96063-145">**HttpCoNtext。使用者**。</span><span class="sxs-lookup"><span data-stu-id="96063-145">**HttpContext.Current.User**.</span></span> <span data-ttu-id="96063-146">這個屬性是 ASP.NET 特有的。</span><span class="sxs-lookup"><span data-stu-id="96063-146">This property is specific to ASP.NET.</span></span>

<span data-ttu-id="96063-147">下列程式碼顯示如何設定主體：</span><span class="sxs-lookup"><span data-stu-id="96063-147">The following code shows how to set the principal:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="96063-148">若為 web 裝載，您必須在兩個地方設定主體;否則，安全性內容可能會變得不一致。</span><span class="sxs-lookup"><span data-stu-id="96063-148">For web-hosting, you must set the principal in both places; otherwise the security context may become inconsistent.</span></span> <span data-ttu-id="96063-149">不過，如果是自我裝載， **HttpCoNtext**就是 null。</span><span class="sxs-lookup"><span data-stu-id="96063-149">For self-hosting, however, **HttpContext.Current** is null.</span></span> <span data-ttu-id="96063-150">為了確保您的程式碼與主機無關，因此請先檢查是否有 null，再指派給**HttpCoNtext**，如下所示。</span><span class="sxs-lookup"><span data-stu-id="96063-150">To ensure your code is host-agnostic, therefore, check for null before assigning to **HttpContext.Current**, as shown.</span></span>

## <a name="authorization"></a><span data-ttu-id="96063-151">授權</span><span class="sxs-lookup"><span data-stu-id="96063-151">Authorization</span></span>

<span data-ttu-id="96063-152">稍後會在管線中進行授權，接近控制器。</span><span class="sxs-lookup"><span data-stu-id="96063-152">Authorization happens later in the pipeline, closer to the controller.</span></span> <span data-ttu-id="96063-153">這可讓您在授與資源的存取權時，做出更細微的選擇。</span><span class="sxs-lookup"><span data-stu-id="96063-153">That lets you make more granular choices when you grant access to resources.</span></span>

- <span data-ttu-id="96063-154">*授權篩選準則*會在控制器動作之前執行。</span><span class="sxs-lookup"><span data-stu-id="96063-154">*Authorization filters* run before the controller action.</span></span> <span data-ttu-id="96063-155">如果要求未獲授權，篩選準則會傳回錯誤回應，且不會叫用動作。</span><span class="sxs-lookup"><span data-stu-id="96063-155">If the request is not authorized, the filter returns an error response, and the action is not invoked.</span></span>
- <span data-ttu-id="96063-156">在控制器動作中，您可以從**ApiController 的使用者**屬性取得目前的主體。</span><span class="sxs-lookup"><span data-stu-id="96063-156">Within a controller action, you can get the current principal from the **ApiController.User** property.</span></span> <span data-ttu-id="96063-157">例如，您可能會根據使用者名稱篩選資源清單，只傳回屬於該使用者的資源。</span><span class="sxs-lookup"><span data-stu-id="96063-157">For example, you might filter a list of resources based on the user name, returning only those resources that belong to that user.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image1.png)

<a id="auth3"></a>
### <a name="using-the-authorize-attribute"></a><span data-ttu-id="96063-158">使用 [授權] 屬性</span><span class="sxs-lookup"><span data-stu-id="96063-158">Using the [Authorize] Attribute</span></span>

<span data-ttu-id="96063-159">Web API 提供內建的授權篩選準則[AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx)。</span><span class="sxs-lookup"><span data-stu-id="96063-159">Web API provides a built-in authorization filter, [AuthorizeAttribute](https://msdn.microsoft.com/library/system.web.http.authorizeattribute.aspx).</span></span> <span data-ttu-id="96063-160">此篩選準則會檢查使用者是否經過驗證。</span><span class="sxs-lookup"><span data-stu-id="96063-160">This filter checks whether the user is authenticated.</span></span> <span data-ttu-id="96063-161">如果不是，則會傳回 HTTP 狀態碼401（未經授權），而不會叫用動作。</span><span class="sxs-lookup"><span data-stu-id="96063-161">If not, it returns HTTP status code 401 (Unauthorized), without invoking the action.</span></span>

<span data-ttu-id="96063-162">您可以在控制器層級或個別動作層級，全域套用篩選準則。</span><span class="sxs-lookup"><span data-stu-id="96063-162">You can apply the filter globally, at the controller level, or at the level of individual actions.</span></span>

<span data-ttu-id="96063-163">**全域**：若要限制每個 Web API 控制器的存取，請將**AuthorizeAttribute**篩選器新增至全域篩選清單：</span><span class="sxs-lookup"><span data-stu-id="96063-163">**Globally**: To restrict access for every Web API controller, add the **AuthorizeAttribute** filter to the global filter list:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="96063-164">**控制器**：若要限制特定控制器的存取，請將篩選器新增為控制器的屬性：</span><span class="sxs-lookup"><span data-stu-id="96063-164">**Controller**: To restrict access for a specific controller, add the filter as an attribute to the controller:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="96063-165">**動作**：若要限制特定動作的存取權，請將屬性新增至動作方法：</span><span class="sxs-lookup"><span data-stu-id="96063-165">**Action**: To restrict access for specific actions, add the attribute to the action method:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample4.cs)]

<span data-ttu-id="96063-166">或者，您可以使用 `[AllowAnonymous]` 屬性來限制控制器，然後允許匿名存取特定的動作。</span><span class="sxs-lookup"><span data-stu-id="96063-166">Alternatively, you can restrict the controller and then allow anonymous access to specific actions, by using the `[AllowAnonymous]` attribute.</span></span> <span data-ttu-id="96063-167">在下列範例中，`Post` 方法是受限制的，但 `Get` 方法允許匿名存取。</span><span class="sxs-lookup"><span data-stu-id="96063-167">In the following example, the `Post` method is restricted, but the `Get` method allows anonymous access.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="96063-168">在先前的範例中，篩選準則可讓任何已驗證的使用者存取受限制的方法。只會保留匿名使用者。您也可以限制特定使用者或特定角色使用者的存取權：</span><span class="sxs-lookup"><span data-stu-id="96063-168">In the previous examples, the filter allows any authenticated user to access the restricted methods; only anonymous users are kept out. You can also limit access to specific users or to users in specific roles:</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample6.cs)]

> [!NOTE]
> <span data-ttu-id="96063-169">Web API 控制器的**AuthorizeAttribute**篩選器位於**system.web. Http**命名空間中。</span><span class="sxs-lookup"><span data-stu-id="96063-169">The **AuthorizeAttribute** filter for Web API controllers is located in the **System.Web.Http** namespace.</span></span> <span data-ttu-id="96063-170">**System.web**命名空間中的 MVC 控制器有類似的篩選，這與 web API 控制器不相容。</span><span class="sxs-lookup"><span data-stu-id="96063-170">There is a similar filter for MVC controllers in the **System.Web.Mvc** namespace, which is not compatible with Web API controllers.</span></span>

### <a name="custom-authorization-filters"></a><span data-ttu-id="96063-171">自訂授權篩選</span><span class="sxs-lookup"><span data-stu-id="96063-171">Custom Authorization Filters</span></span>

<span data-ttu-id="96063-172">若要撰寫自訂授權篩選，請從下列其中一種類型衍生：</span><span class="sxs-lookup"><span data-stu-id="96063-172">To write a custom authorization filter, derive from one of these types:</span></span>

- <span data-ttu-id="96063-173">**AuthorizeAttribute**。</span><span class="sxs-lookup"><span data-stu-id="96063-173">**AuthorizeAttribute**.</span></span> <span data-ttu-id="96063-174">擴充此類別，以根據目前的使用者和使用者的角色來執行授權邏輯。</span><span class="sxs-lookup"><span data-stu-id="96063-174">Extend this class to perform authorization logic based on the current user and the user's roles.</span></span>
- <span data-ttu-id="96063-175">**AuthorizationFilterAttribute**。</span><span class="sxs-lookup"><span data-stu-id="96063-175">**AuthorizationFilterAttribute**.</span></span> <span data-ttu-id="96063-176">擴充這個類別，以執行不一定是根據目前使用者或角色的同步授權邏輯。</span><span class="sxs-lookup"><span data-stu-id="96063-176">Extend this class to perform synchronous authorization logic that is not necessarily based on the current user or role.</span></span>
- <span data-ttu-id="96063-177">**IAuthorizationFilter**。</span><span class="sxs-lookup"><span data-stu-id="96063-177">**IAuthorizationFilter**.</span></span> <span data-ttu-id="96063-178">執行此介面來執行非同步授權邏輯;例如，如果您的授權邏輯會進行非同步 i/o 或網路呼叫。</span><span class="sxs-lookup"><span data-stu-id="96063-178">Implement this interface to perform asynchronous authorization logic; for example, if your authorization logic makes asynchronous I/O or network calls.</span></span> <span data-ttu-id="96063-179">（如果您的授權邏輯是 CPU 界限，則從**AuthorizationFilterAttribute**衍生會比較簡單，因為您不需要撰寫非同步方法）。</span><span class="sxs-lookup"><span data-stu-id="96063-179">(If your authorization logic is CPU-bound, it is simpler to derive from **AuthorizationFilterAttribute**, because then you don't need to write an asynchronous method.)</span></span>

<span data-ttu-id="96063-180">下圖顯示**AuthorizeAttribute**類別的類別階層。</span><span class="sxs-lookup"><span data-stu-id="96063-180">The following diagram shows the class hierarchy for the **AuthorizeAttribute** class.</span></span>

![](authentication-and-authorization-in-aspnet-web-api/_static/image2.png)

### <a name="authorization-inside-a-controller-action"></a><span data-ttu-id="96063-181">控制器動作內的授權</span><span class="sxs-lookup"><span data-stu-id="96063-181">Authorization Inside a Controller Action</span></span>

<span data-ttu-id="96063-182">在某些情況下，您可能會允許要求繼續進行，但根據主體變更行為。</span><span class="sxs-lookup"><span data-stu-id="96063-182">In some cases, you might allow a request to proceed, but change the behavior based on the principal.</span></span> <span data-ttu-id="96063-183">例如，您傳回的資訊可能會根據使用者的角色而變更。</span><span class="sxs-lookup"><span data-stu-id="96063-183">For example, the information that you return might change depending on the user's role.</span></span> <span data-ttu-id="96063-184">在控制器方法中，您可以從**ApiController**屬性取得目前的主體。</span><span class="sxs-lookup"><span data-stu-id="96063-184">Within a controller method, you can get the current principal from the **ApiController.User** property.</span></span>

[!code-csharp[Main](authentication-and-authorization-in-aspnet-web-api/samples/sample7.cs)]
