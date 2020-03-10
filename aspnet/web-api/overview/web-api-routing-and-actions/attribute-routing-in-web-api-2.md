---
uid: web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
title: ASP.NET Web API 2 中的屬性路由 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 01/20/2014
ms.assetid: 979d6c9f-0129-4e5b-ae56-4507b281b86d
msc.legacyurl: /web-api/overview/web-api-routing-and-actions/attribute-routing-in-web-api-2
msc.type: authoredcontent
ms.openlocfilehash: 7da1805d8a7066e82743dc9bd7e024cc9813ee89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78554982"
---
# <a name="attribute-routing-in-aspnet-web-api-2"></a><span data-ttu-id="7646b-102">ASP.NET Web API 2 中的屬性路由</span><span class="sxs-lookup"><span data-stu-id="7646b-102">Attribute Routing in ASP.NET Web API 2</span></span>

<span data-ttu-id="7646b-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7646b-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="7646b-104">*路由*是 Web API 與動作的 URI 相符的方式。</span><span class="sxs-lookup"><span data-stu-id="7646b-104">*Routing* is how Web API matches a URI to an action.</span></span> <span data-ttu-id="7646b-105">Web API 2 支援新類型的路由，稱為*屬性路由*。</span><span class="sxs-lookup"><span data-stu-id="7646b-105">Web API 2 supports a new type of routing, called *attribute routing*.</span></span> <span data-ttu-id="7646b-106">如其名稱所示，屬性路由會使用屬性來定義路由。</span><span class="sxs-lookup"><span data-stu-id="7646b-106">As the name implies, attribute routing uses attributes to define routes.</span></span> <span data-ttu-id="7646b-107">屬性路由可讓您更充分掌控 Web API 中的 Uri。</span><span class="sxs-lookup"><span data-stu-id="7646b-107">Attribute routing gives you more control over the URIs in your web API.</span></span> <span data-ttu-id="7646b-108">例如，您可以輕鬆地建立描述資源階層的 Uri。</span><span class="sxs-lookup"><span data-stu-id="7646b-108">For example, you can easily create URIs that describe hierarchies of resources.</span></span>

<span data-ttu-id="7646b-109">先前的路由樣式（稱為慣例型路由）仍受到完整支援。</span><span class="sxs-lookup"><span data-stu-id="7646b-109">The earlier style of routing, called convention-based routing, is still fully supported.</span></span> <span data-ttu-id="7646b-110">事實上，您可以將這兩種技術結合在同一個專案中。</span><span class="sxs-lookup"><span data-stu-id="7646b-110">In fact, you can combine both techniques in the same project.</span></span>

<span data-ttu-id="7646b-111">本主題說明如何啟用屬性路由，並說明屬性路由的各種選項。</span><span class="sxs-lookup"><span data-stu-id="7646b-111">This topic shows how to enable attribute routing and describes the various options for attribute routing.</span></span> <span data-ttu-id="7646b-112">如需使用屬性路由的端對端教學課程，請參閱[使用 WEB API 2 中的屬性路由建立 REST API](create-a-rest-api-with-attribute-routing.md)。</span><span class="sxs-lookup"><span data-stu-id="7646b-112">For an end-to-end tutorial that uses attribute routing, see [Create a REST API with Attribute Routing in Web API 2](create-a-rest-api-with-attribute-routing.md).</span></span>

## <a name="prerequisites"></a><span data-ttu-id="7646b-113">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="7646b-113">Prerequisites</span></span>

<span data-ttu-id="7646b-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)社區、專業或企業版</span><span class="sxs-lookup"><span data-stu-id="7646b-114">[Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017) Community, Professional, or Enterprise edition</span></span>

<span data-ttu-id="7646b-115">或者，使用 NuGet 套件管理員來安裝必要的套件。</span><span class="sxs-lookup"><span data-stu-id="7646b-115">Alternatively, use NuGet Package Manager to install the necessary packages.</span></span> <span data-ttu-id="7646b-116">從 Visual Studio 的 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="7646b-116">From the **Tools** menu in Visual Studio, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="7646b-117">在 [套件管理員主控台] 視窗中輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="7646b-117">Enter the following command in the Package Manager Console window:</span></span>

`Install-Package Microsoft.AspNet.WebApi.WebHost`

<a id="why"></a>
## <a name="why-attribute-routing"></a><span data-ttu-id="7646b-118">為什麼要進行屬性路由？</span><span class="sxs-lookup"><span data-stu-id="7646b-118">Why Attribute Routing?</span></span>

<span data-ttu-id="7646b-119">第一版的 Web API 使用以*慣例為基礎*的路由。</span><span class="sxs-lookup"><span data-stu-id="7646b-119">The first release of Web API used *convention-based* routing.</span></span> <span data-ttu-id="7646b-120">在該類型的路由中，您會定義一或多個路由範本，基本上就是參數化字串。</span><span class="sxs-lookup"><span data-stu-id="7646b-120">In that type of routing, you define one or more route templates, which are basically parameterized strings.</span></span> <span data-ttu-id="7646b-121">當架構收到要求時，它會比對路由範本的 URI。</span><span class="sxs-lookup"><span data-stu-id="7646b-121">When the framework receives a request, it matches the URI against the route template.</span></span> <span data-ttu-id="7646b-122">（如需以慣例為基礎之路由的詳細資訊，請參閱[ASP.NET Web API 中的路由](routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="7646b-122">(For more information about convention-based routing, see [Routing in ASP.NET Web API](routing-in-aspnet-web-api.md).</span></span>

<span data-ttu-id="7646b-123">以慣例為基礎的路由的優點之一，是在單一位置定義範本，並在所有控制器上一致地套用路由規則。</span><span class="sxs-lookup"><span data-stu-id="7646b-123">One advantage of convention-based routing is that templates are defined in a single place, and the routing rules are applied consistently across all controllers.</span></span> <span data-ttu-id="7646b-124">可惜的是，以慣例為基礎的路由，讓您難以支援 RESTful Api 中常見的特定 URI 模式。</span><span class="sxs-lookup"><span data-stu-id="7646b-124">Unfortunately, convention-based routing makes it hard to support certain URI patterns that are common in RESTful APIs.</span></span> <span data-ttu-id="7646b-125">例如，資源通常包含子資源：客戶有訂單、電影具有執行者、書籍有作者等等。</span><span class="sxs-lookup"><span data-stu-id="7646b-125">For example, resources often contain child resources: Customers have orders, movies have actors, books have authors, and so forth.</span></span> <span data-ttu-id="7646b-126">建立反映這些關聯性的 Uri 是很自然的：</span><span class="sxs-lookup"><span data-stu-id="7646b-126">It's natural to create URIs that reflect these relations:</span></span>

`/customers/1/orders`

<span data-ttu-id="7646b-127">這種類型的 URI 很容易使用以慣例為基礎的路由來建立。</span><span class="sxs-lookup"><span data-stu-id="7646b-127">This type of URI is difficult to create using convention-based routing.</span></span> <span data-ttu-id="7646b-128">雖然可以完成，但如果您有許多控制器或資源類型，則結果無法妥善調整。</span><span class="sxs-lookup"><span data-stu-id="7646b-128">Although it can be done, the results don't scale well if you have many controllers or resource types.</span></span>

<span data-ttu-id="7646b-129">使用屬性路由，為此 URI 定義路由是很簡單的。</span><span class="sxs-lookup"><span data-stu-id="7646b-129">With attribute routing, it's trivial to define a route for this URI.</span></span> <span data-ttu-id="7646b-130">您只需將屬性新增至控制器動作：</span><span class="sxs-lookup"><span data-stu-id="7646b-130">You simply add an attribute to the controller action:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample1.cs)]

<span data-ttu-id="7646b-131">以下是一些屬性路由變得很容易的其他模式。</span><span class="sxs-lookup"><span data-stu-id="7646b-131">Here are some other patterns that attribute routing makes easy.</span></span>

<span data-ttu-id="7646b-132">**API 版本控制**</span><span class="sxs-lookup"><span data-stu-id="7646b-132">**API versioning**</span></span>

<span data-ttu-id="7646b-133">在此範例中，"/api/v1/products" 會路由傳送至不同的控制器，而不是 "/api/v2/products"。</span><span class="sxs-lookup"><span data-stu-id="7646b-133">In this example, "/api/v1/products" would be routed to a different controller than "/api/v2/products".</span></span>

`/api/v1/products`
`/api/v2/products`

<span data-ttu-id="7646b-134">**多載 URI 區段**</span><span class="sxs-lookup"><span data-stu-id="7646b-134">**Overloaded URI segments**</span></span>

<span data-ttu-id="7646b-135">在此範例中，"1" 是訂單號碼，但 "pending" 對應至集合。</span><span class="sxs-lookup"><span data-stu-id="7646b-135">In this example, "1" is an order number, but "pending" maps to a collection.</span></span>

`/orders/1`
`/orders/pending`

<span data-ttu-id="7646b-136">**多個參數類型**</span><span class="sxs-lookup"><span data-stu-id="7646b-136">**Multiple parameter types**</span></span>

<span data-ttu-id="7646b-137">在此範例中，"1" 是訂單號碼，但 "2013/06/16" 指定日期。</span><span class="sxs-lookup"><span data-stu-id="7646b-137">In this example, "1" is an order number, but "2013/06/16" specifies a date.</span></span>

`/orders/1`
`/orders/2013/06/16`

<a id="enable"></a>
## <a name="enabling-attribute-routing"></a><span data-ttu-id="7646b-138">啟用屬性路由</span><span class="sxs-lookup"><span data-stu-id="7646b-138">Enabling Attribute Routing</span></span>

<span data-ttu-id="7646b-139">若要啟用屬性路由，請在設定期間呼叫**MapHttpAttributeRoutes** 。</span><span class="sxs-lookup"><span data-stu-id="7646b-139">To enable attribute routing, call **MapHttpAttributeRoutes** during configuration.</span></span> <span data-ttu-id="7646b-140">這個擴充方法是在**HttpConfigurationExtensions**類別中定義。</span><span class="sxs-lookup"><span data-stu-id="7646b-140">This extension method is defined in the **System.Web.Http.HttpConfigurationExtensions** class.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample2.cs)]

<span data-ttu-id="7646b-141">屬性路由可以與以[慣例為基礎](routing-in-aspnet-web-api.md)的路由結合。</span><span class="sxs-lookup"><span data-stu-id="7646b-141">Attribute routing can be combined with [convention-based](routing-in-aspnet-web-api.md) routing.</span></span> <span data-ttu-id="7646b-142">若要定義以慣例為基礎的路由，請呼叫**MapHttpRoute**方法。</span><span class="sxs-lookup"><span data-stu-id="7646b-142">To define convention-based routes, call the **MapHttpRoute** method.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample3.cs)]

<span data-ttu-id="7646b-143">如需設定 Web API 的詳細資訊，請參閱設定[ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="7646b-143">For more information about configuring Web API, see [Configuring ASP.NET Web API 2](../advanced/configuring-aspnet-web-api.md).</span></span>

<a id="config"></a>
### <a name="note-migrating-from-web-api-1"></a><span data-ttu-id="7646b-144">注意：從 Web API 1 進行遷移</span><span class="sxs-lookup"><span data-stu-id="7646b-144">Note: Migrating From Web API 1</span></span>

<span data-ttu-id="7646b-145">在 Web API 2 之前，Web API 專案範本會產生如下的程式碼：</span><span class="sxs-lookup"><span data-stu-id="7646b-145">Prior to Web API 2, the Web API project templates generated code like this:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample4.cs)]

<span data-ttu-id="7646b-146">如果已啟用屬性路由，此程式碼將會擲回例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7646b-146">If attribute routing is enabled, this code will throw an exception.</span></span> <span data-ttu-id="7646b-147">如果您將現有的 Web API 專案升級為使用屬性路由，請務必將此設定程式碼更新為下列內容：</span><span class="sxs-lookup"><span data-stu-id="7646b-147">If you upgrade an existing Web API project to use attribute routing, make sure to update this configuration code to the following:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample5.cs?highlight=4)]

> [!NOTE]
> <span data-ttu-id="7646b-148">如需詳細資訊，請參閱[使用 ASP.NET 裝載來設定 WEB API](../advanced/configuring-aspnet-web-api.md#webhost)。</span><span class="sxs-lookup"><span data-stu-id="7646b-148">For more information, see [Configuring Web API with ASP.NET Hosting](../advanced/configuring-aspnet-web-api.md#webhost).</span></span>

<a id="add-routes"></a>
## <a name="adding-route-attributes"></a><span data-ttu-id="7646b-149">新增路由屬性</span><span class="sxs-lookup"><span data-stu-id="7646b-149">Adding Route Attributes</span></span>

<span data-ttu-id="7646b-150">以下是使用屬性定義的路由範例：</span><span class="sxs-lookup"><span data-stu-id="7646b-150">Here is an example of a route defined using an attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample6.cs)]

<span data-ttu-id="7646b-151">客戶/{customerId}/訂單&quot; &quot;字串是路由的 URI 範本。</span><span class="sxs-lookup"><span data-stu-id="7646b-151">The string &quot;customers/{customerId}/orders&quot; is the URI template for the route.</span></span> <span data-ttu-id="7646b-152">Web API 會嘗試將要求 URI 與範本比對。</span><span class="sxs-lookup"><span data-stu-id="7646b-152">Web API tries to match the request URI to the template.</span></span> <span data-ttu-id="7646b-153">在此範例中，「客戶」和「訂單」是常值區段，而「{customerId}」則是變數參數。</span><span class="sxs-lookup"><span data-stu-id="7646b-153">In this example, "customers" and "orders" are literal segments, and "{customerId}" is a variable parameter.</span></span> <span data-ttu-id="7646b-154">下列 Uri 會符合此範本：</span><span class="sxs-lookup"><span data-stu-id="7646b-154">The following URIs would match this template:</span></span>

- `http://localhost/customers/1/orders`
- `http://localhost/customers/bob/orders`
- `http://localhost/customers/1234-5678/orders`

<span data-ttu-id="7646b-155">您可以使用[條件約束](#constraints)來限制比對，如本主題稍後所述。</span><span class="sxs-lookup"><span data-stu-id="7646b-155">You can restrict the matching by using [constraints](#constraints), described later in this topic.</span></span>

<span data-ttu-id="7646b-156">請注意，路由範本中的 &quot;{customerId}&quot; 參數符合方法中*customerId*參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="7646b-156">Notice that the &quot;{customerId}&quot; parameter in the route template matches the name of the *customerId* parameter in the method.</span></span> <span data-ttu-id="7646b-157">當 Web API 叫用控制器動作時，它會嘗試系結路由參數。</span><span class="sxs-lookup"><span data-stu-id="7646b-157">When Web API invokes the controller action, it tries to bind the route parameters.</span></span> <span data-ttu-id="7646b-158">例如，如果 URI 為 `http://example.com/customers/1/orders`，Web API 會嘗試將值 "1" 系結至動作中的*customerId*參數。</span><span class="sxs-lookup"><span data-stu-id="7646b-158">For example, if the URI is `http://example.com/customers/1/orders`, Web API tries to bind the value "1" to the *customerId* parameter in the action.</span></span>

<span data-ttu-id="7646b-159">URI 範本可以有數個參數：</span><span class="sxs-lookup"><span data-stu-id="7646b-159">A URI template can have several parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample7.cs)]

<span data-ttu-id="7646b-160">任何沒有路由屬性的控制器方法都會使用以慣例為基礎的路由。</span><span class="sxs-lookup"><span data-stu-id="7646b-160">Any controller methods that do not have a route attribute use convention-based routing.</span></span> <span data-ttu-id="7646b-161">如此一來，您就可以將這兩種類型的路由結合在相同的專案中。</span><span class="sxs-lookup"><span data-stu-id="7646b-161">That way, you can combine both types of routing in the same project.</span></span>

## <a name="http-methods"></a><span data-ttu-id="7646b-162">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="7646b-162">HTTP Methods</span></span>

<span data-ttu-id="7646b-163">Web API 也會根據要求的 HTTP 方法（GET、POST 等等）來選取動作。</span><span class="sxs-lookup"><span data-stu-id="7646b-163">Web API also selects actions based on the HTTP method of the request (GET, POST, etc).</span></span> <span data-ttu-id="7646b-164">根據預設，Web API 會使用控制器方法名稱的開頭，尋找不區分大小寫的相符。</span><span class="sxs-lookup"><span data-stu-id="7646b-164">By default, Web API looks for a case-insensitive match with the start of the controller method name.</span></span> <span data-ttu-id="7646b-165">例如，名為 `PutCustomers` 的控制器方法會符合 HTTP PUT 要求。</span><span class="sxs-lookup"><span data-stu-id="7646b-165">For example, a controller method named `PutCustomers` matches an HTTP PUT request.</span></span>

<span data-ttu-id="7646b-166">您可以使用下列任何屬性來裝飾方法，以覆寫此慣例：</span><span class="sxs-lookup"><span data-stu-id="7646b-166">You can override this convention by decorating the method with any the following attributes:</span></span>

- <span data-ttu-id="7646b-167">**HttpDelete**</span><span class="sxs-lookup"><span data-stu-id="7646b-167">**[HttpDelete]**</span></span>
- <span data-ttu-id="7646b-168">**[HttpGet]**</span><span class="sxs-lookup"><span data-stu-id="7646b-168">**[HttpGet]**</span></span>
- <span data-ttu-id="7646b-169">**[HttpHead]**</span><span class="sxs-lookup"><span data-stu-id="7646b-169">**[HttpHead]**</span></span>
- <span data-ttu-id="7646b-170">**HttpOptions**</span><span class="sxs-lookup"><span data-stu-id="7646b-170">**[HttpOptions]**</span></span>
- <span data-ttu-id="7646b-171">**[HttpPatch]**</span><span class="sxs-lookup"><span data-stu-id="7646b-171">**[HttpPatch]**</span></span>
- <span data-ttu-id="7646b-172">**HttpPost**</span><span class="sxs-lookup"><span data-stu-id="7646b-172">**[HttpPost]**</span></span>
- <span data-ttu-id="7646b-173">**HttpPut**</span><span class="sxs-lookup"><span data-stu-id="7646b-173">**[HttpPut]**</span></span>

<span data-ttu-id="7646b-174">下列範例會將 CreateBook 方法對應至 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="7646b-174">The following example maps the CreateBook method to HTTP POST requests.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample8.cs)]

<span data-ttu-id="7646b-175">針對所有其他 HTTP 方法，包括非標準方法，請使用**AcceptVerbs**屬性，這會接受 HTTP 方法的清單。</span><span class="sxs-lookup"><span data-stu-id="7646b-175">For all other HTTP methods, including non-standard methods, use the **AcceptVerbs** attribute, which takes a list of HTTP methods.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample9.cs)]

<a id="prefixes"></a>
## <a name="route-prefixes"></a><span data-ttu-id="7646b-176">路由首碼</span><span class="sxs-lookup"><span data-stu-id="7646b-176">Route Prefixes</span></span>

<span data-ttu-id="7646b-177">通常，控制器中的路由都是以相同的前置詞開頭。</span><span class="sxs-lookup"><span data-stu-id="7646b-177">Often, the routes in a controller all start with the same prefix.</span></span> <span data-ttu-id="7646b-178">例如:</span><span class="sxs-lookup"><span data-stu-id="7646b-178">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample10.cs)]

<span data-ttu-id="7646b-179">您可以使用 **[RoutePrefix]** 屬性來設定整個控制器的通用前置詞：</span><span class="sxs-lookup"><span data-stu-id="7646b-179">You can set a common prefix for an entire controller by using the **[RoutePrefix]** attribute:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample11.cs)]

<span data-ttu-id="7646b-180">在 method 屬性上使用波狀符號（~）來覆寫路由前置詞：</span><span class="sxs-lookup"><span data-stu-id="7646b-180">Use a tilde (~) on the method attribute to override the route prefix:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample12.cs)]

<span data-ttu-id="7646b-181">路由前置詞可以包含參數：</span><span class="sxs-lookup"><span data-stu-id="7646b-181">The route prefix can include parameters:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample13.cs)]

<a id="constraints"></a>
## <a name="route-constraints"></a><span data-ttu-id="7646b-182">路由條件約束</span><span class="sxs-lookup"><span data-stu-id="7646b-182">Route Constraints</span></span>

<span data-ttu-id="7646b-183">路由條件約束可讓您限制路由範本中的參數相符的方式。</span><span class="sxs-lookup"><span data-stu-id="7646b-183">Route constraints let you restrict how the parameters in the route template are matched.</span></span> <span data-ttu-id="7646b-184">一般語法為 &quot;{parameter： constraint}&quot;。</span><span class="sxs-lookup"><span data-stu-id="7646b-184">The general syntax is &quot;{parameter:constraint}&quot;.</span></span> <span data-ttu-id="7646b-185">例如:</span><span class="sxs-lookup"><span data-stu-id="7646b-185">For example:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample14.cs)]

<span data-ttu-id="7646b-186">在這裡，只有在 URI 的 &quot;識別碼&quot; 區段是整數時，才會選取第一個路由。</span><span class="sxs-lookup"><span data-stu-id="7646b-186">Here, the first route will only be selected if the &quot;id&quot; segment of the URI is an integer.</span></span> <span data-ttu-id="7646b-187">否則，將會選擇第二個路由。</span><span class="sxs-lookup"><span data-stu-id="7646b-187">Otherwise, the second route will be chosen.</span></span>

<span data-ttu-id="7646b-188">下表列出支援的條件約束。</span><span class="sxs-lookup"><span data-stu-id="7646b-188">The following table lists the constraints that are supported.</span></span>

| <span data-ttu-id="7646b-189">條件約束</span><span class="sxs-lookup"><span data-stu-id="7646b-189">Constraint</span></span> | <span data-ttu-id="7646b-190">說明</span><span class="sxs-lookup"><span data-stu-id="7646b-190">Description</span></span> | <span data-ttu-id="7646b-191">範例</span><span class="sxs-lookup"><span data-stu-id="7646b-191">Example</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7646b-192">Alpha</span><span class="sxs-lookup"><span data-stu-id="7646b-192">alpha</span></span> | <span data-ttu-id="7646b-193">符合大寫或小寫拉丁字母字元（a-z、a-z）</span><span class="sxs-lookup"><span data-stu-id="7646b-193">Matches uppercase or lowercase Latin alphabet characters (a-z, A-Z)</span></span> | <span data-ttu-id="7646b-194">{x:Alpha}</span><span class="sxs-lookup"><span data-stu-id="7646b-194">{x:alpha}</span></span> |
| <span data-ttu-id="7646b-195">bool</span><span class="sxs-lookup"><span data-stu-id="7646b-195">bool</span></span> | <span data-ttu-id="7646b-196">符合布林值。</span><span class="sxs-lookup"><span data-stu-id="7646b-196">Matches a Boolean value.</span></span> | <span data-ttu-id="7646b-197">{x:bool}</span><span class="sxs-lookup"><span data-stu-id="7646b-197">{x:bool}</span></span> |
| <span data-ttu-id="7646b-198">datetime</span><span class="sxs-lookup"><span data-stu-id="7646b-198">datetime</span></span> | <span data-ttu-id="7646b-199">符合**日期時間**值。</span><span class="sxs-lookup"><span data-stu-id="7646b-199">Matches a **DateTime** value.</span></span> | <span data-ttu-id="7646b-200">{x:datetime}</span><span class="sxs-lookup"><span data-stu-id="7646b-200">{x:datetime}</span></span> |
| <span data-ttu-id="7646b-201">decimal</span><span class="sxs-lookup"><span data-stu-id="7646b-201">decimal</span></span> | <span data-ttu-id="7646b-202">符合十進位值。</span><span class="sxs-lookup"><span data-stu-id="7646b-202">Matches a decimal value.</span></span> | <span data-ttu-id="7646b-203">{x:decimal}</span><span class="sxs-lookup"><span data-stu-id="7646b-203">{x:decimal}</span></span> |
| <span data-ttu-id="7646b-204">雙線</span><span class="sxs-lookup"><span data-stu-id="7646b-204">double</span></span> | <span data-ttu-id="7646b-205">符合64位的浮點值。</span><span class="sxs-lookup"><span data-stu-id="7646b-205">Matches a 64-bit floating-point value.</span></span> | <span data-ttu-id="7646b-206">x：double</span><span class="sxs-lookup"><span data-stu-id="7646b-206">{x:double}</span></span> |
| <span data-ttu-id="7646b-207">FLOAT</span><span class="sxs-lookup"><span data-stu-id="7646b-207">float</span></span> | <span data-ttu-id="7646b-208">符合32位的浮點值。</span><span class="sxs-lookup"><span data-stu-id="7646b-208">Matches a 32-bit floating-point value.</span></span> | <span data-ttu-id="7646b-209">{x:float}</span><span class="sxs-lookup"><span data-stu-id="7646b-209">{x:float}</span></span> |
| <span data-ttu-id="7646b-210">guid</span><span class="sxs-lookup"><span data-stu-id="7646b-210">guid</span></span> | <span data-ttu-id="7646b-211">符合 GUID 值。</span><span class="sxs-lookup"><span data-stu-id="7646b-211">Matches a GUID value.</span></span> | <span data-ttu-id="7646b-212">{x:guid}</span><span class="sxs-lookup"><span data-stu-id="7646b-212">{x:guid}</span></span> |
| <span data-ttu-id="7646b-213">int</span><span class="sxs-lookup"><span data-stu-id="7646b-213">int</span></span> | <span data-ttu-id="7646b-214">符合32位的整數值。</span><span class="sxs-lookup"><span data-stu-id="7646b-214">Matches a 32-bit integer value.</span></span> | <span data-ttu-id="7646b-215">{x:int}</span><span class="sxs-lookup"><span data-stu-id="7646b-215">{x:int}</span></span> |
| <span data-ttu-id="7646b-216">長度</span><span class="sxs-lookup"><span data-stu-id="7646b-216">length</span></span> | <span data-ttu-id="7646b-217">符合指定長度或指定長度範圍內的字串。</span><span class="sxs-lookup"><span data-stu-id="7646b-217">Matches a string with the specified length or within a specified range of lengths.</span></span> | <span data-ttu-id="7646b-218">{x:length （6）}{x:length （1，20）}</span><span class="sxs-lookup"><span data-stu-id="7646b-218">{x:length(6)} {x:length(1,20)}</span></span> |
| <span data-ttu-id="7646b-219">long</span><span class="sxs-lookup"><span data-stu-id="7646b-219">long</span></span> | <span data-ttu-id="7646b-220">符合64位的整數值。</span><span class="sxs-lookup"><span data-stu-id="7646b-220">Matches a 64-bit integer value.</span></span> | <span data-ttu-id="7646b-221">{x:long}</span><span class="sxs-lookup"><span data-stu-id="7646b-221">{x:long}</span></span> |
| <span data-ttu-id="7646b-222">max</span><span class="sxs-lookup"><span data-stu-id="7646b-222">max</span></span> | <span data-ttu-id="7646b-223">符合具有最大值的整數。</span><span class="sxs-lookup"><span data-stu-id="7646b-223">Matches an integer with a maximum value.</span></span> | <span data-ttu-id="7646b-224">{x:max （10）}</span><span class="sxs-lookup"><span data-stu-id="7646b-224">{x:max(10)}</span></span> |
| <span data-ttu-id="7646b-225">長度</span><span class="sxs-lookup"><span data-stu-id="7646b-225">maxlength</span></span> | <span data-ttu-id="7646b-226">符合長度上限的字串。</span><span class="sxs-lookup"><span data-stu-id="7646b-226">Matches a string with a maximum length.</span></span> | <span data-ttu-id="7646b-227">{x:maxlength （10）}</span><span class="sxs-lookup"><span data-stu-id="7646b-227">{x:maxlength(10)}</span></span> |
| <span data-ttu-id="7646b-228">min</span><span class="sxs-lookup"><span data-stu-id="7646b-228">min</span></span> | <span data-ttu-id="7646b-229">符合最小值的整數。</span><span class="sxs-lookup"><span data-stu-id="7646b-229">Matches an integer with a minimum value.</span></span> | <span data-ttu-id="7646b-230">{x:min （10）}</span><span class="sxs-lookup"><span data-stu-id="7646b-230">{x:min(10)}</span></span> |
| <span data-ttu-id="7646b-231">minlength</span><span class="sxs-lookup"><span data-stu-id="7646b-231">minlength</span></span> | <span data-ttu-id="7646b-232">符合長度最小的字串。</span><span class="sxs-lookup"><span data-stu-id="7646b-232">Matches a string with a minimum length.</span></span> | <span data-ttu-id="7646b-233">{x:minlength （10）}</span><span class="sxs-lookup"><span data-stu-id="7646b-233">{x:minlength(10)}</span></span> |
| <span data-ttu-id="7646b-234">range</span><span class="sxs-lookup"><span data-stu-id="7646b-234">range</span></span> | <span data-ttu-id="7646b-235">符合某個值範圍內的整數。</span><span class="sxs-lookup"><span data-stu-id="7646b-235">Matches an integer within a range of values.</span></span> | <span data-ttu-id="7646b-236">{x:range （10，50）}</span><span class="sxs-lookup"><span data-stu-id="7646b-236">{x:range(10,50)}</span></span> |
| <span data-ttu-id="7646b-237">regex</span><span class="sxs-lookup"><span data-stu-id="7646b-237">regex</span></span> | <span data-ttu-id="7646b-238">符合正則運算式。</span><span class="sxs-lookup"><span data-stu-id="7646b-238">Matches a regular expression.</span></span> | <span data-ttu-id="7646b-239">{x:RegEx （^ \d{3}-\d{3}-\d{4}$）}</span><span class="sxs-lookup"><span data-stu-id="7646b-239">{x:regex(^\d{3}-\d{3}-\d{4}$)}</span></span> |

<span data-ttu-id="7646b-240">請注意，某些條件約束（例如 &quot;min&quot;）接受括弧中的引數。</span><span class="sxs-lookup"><span data-stu-id="7646b-240">Notice that some of the constraints, such as &quot;min&quot;, take arguments in parentheses.</span></span> <span data-ttu-id="7646b-241">您可以將多個條件約束套用至參數，並以冒號分隔。</span><span class="sxs-lookup"><span data-stu-id="7646b-241">You can apply multiple constraints to a parameter, separated by a colon.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample15.cs)]

### <a name="custom-route-constraints"></a><span data-ttu-id="7646b-242">自訂路由限制式</span><span class="sxs-lookup"><span data-stu-id="7646b-242">Custom Route Constraints</span></span>

<span data-ttu-id="7646b-243">您可以藉由執行**IHttpRouteConstraint**介面來建立自訂路由條件約束。</span><span class="sxs-lookup"><span data-stu-id="7646b-243">You can create custom route constraints by implementing the **IHttpRouteConstraint** interface.</span></span> <span data-ttu-id="7646b-244">例如，下列條件約束會將參數限制為非零的整數值。</span><span class="sxs-lookup"><span data-stu-id="7646b-244">For example, the following constraint restricts a parameter to a non-zero integer value.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample16.cs)]

<span data-ttu-id="7646b-245">下列程式碼顯示如何註冊條件約束：</span><span class="sxs-lookup"><span data-stu-id="7646b-245">The following code shows how to register the constraint:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample17.cs)]

<span data-ttu-id="7646b-246">現在您可以在路由中套用條件約束：</span><span class="sxs-lookup"><span data-stu-id="7646b-246">Now you can apply the constraint in your routes:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample18.cs)]

<span data-ttu-id="7646b-247">您也可以藉由執行**IInlineConstraintResolver**介面來取代整個**DefaultInlineConstraintResolver**類別。</span><span class="sxs-lookup"><span data-stu-id="7646b-247">You can also replace the entire **DefaultInlineConstraintResolver** class by implementing the **IInlineConstraintResolver** interface.</span></span> <span data-ttu-id="7646b-248">這麼做會取代所有內建的條件約束，除非您的**IInlineConstraintResolver**特別加入它們。</span><span class="sxs-lookup"><span data-stu-id="7646b-248">Doing so will replace all of the built-in constraints, unless your implementation of **IInlineConstraintResolver** specifically adds them.</span></span>

<a id="optional"></a>
## <a name="optional-uri-parameters-and-default-values"></a><span data-ttu-id="7646b-249">選擇性的 URI 參數和預設值</span><span class="sxs-lookup"><span data-stu-id="7646b-249">Optional URI Parameters and Default Values</span></span>

<span data-ttu-id="7646b-250">您可以藉由將問號新增至 route 參數，將 URI 參數設為選擇性。</span><span class="sxs-lookup"><span data-stu-id="7646b-250">You can make a URI parameter optional by adding a question mark to the route parameter.</span></span> <span data-ttu-id="7646b-251">如果路由參數是選擇性的，您必須定義 method 參數的預設值。</span><span class="sxs-lookup"><span data-stu-id="7646b-251">If a route parameter is optional, you must define a default value for the method parameter.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample19.cs)]

<span data-ttu-id="7646b-252">在此範例中，`/api/books/locale/1033` 和 `/api/books/locale` 會傳回相同的資源。</span><span class="sxs-lookup"><span data-stu-id="7646b-252">In this example, `/api/books/locale/1033` and `/api/books/locale` return the same resource.</span></span>

<span data-ttu-id="7646b-253">或者，您也可以在路由範本中指定預設值，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7646b-253">Alternatively, you can specify a default value inside the route template, as follows:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample20.cs)]

<span data-ttu-id="7646b-254">這幾乎與上一個範例相同，但套用預設值時，行為稍有不同。</span><span class="sxs-lookup"><span data-stu-id="7646b-254">This is almost the same as the previous example, but there is a slight difference of behavior when the default value is applied.</span></span>

- <span data-ttu-id="7646b-255">在第一個範例（"{lcid： int？}"）中，1033的預設值會直接指派給方法參數，因此參數會有這個確切的值。</span><span class="sxs-lookup"><span data-stu-id="7646b-255">In the first example ("{lcid:int?}"), the default value of 1033 is assigned directly to the method parameter, so the parameter will have this exact value.</span></span>
- <span data-ttu-id="7646b-256">在第二個範例（"{lcid： int = 1033}"）中，"1033" 的預設值會經過模型系結程式。</span><span class="sxs-lookup"><span data-stu-id="7646b-256">In the second example ("{lcid:int=1033}"), the default value of "1033" goes through the model-binding process.</span></span> <span data-ttu-id="7646b-257">預設的模型系結器會將 "1033" 轉換為數值1033。</span><span class="sxs-lookup"><span data-stu-id="7646b-257">The default model-binder will convert "1033" to the numeric value 1033.</span></span> <span data-ttu-id="7646b-258">不過，您可以插入自訂模型系結器，這可能會執行一些不同的動作。</span><span class="sxs-lookup"><span data-stu-id="7646b-258">However, you could plug in a custom model binder, which might do something different.</span></span>

<span data-ttu-id="7646b-259">（在大部分的情況下，除非您的管線中有自訂模型系結器，否則這兩種形式會是相等的）。</span><span class="sxs-lookup"><span data-stu-id="7646b-259">(In most cases, unless you have custom model binders in your pipeline, the two forms will be equivalent.)</span></span>

<a id="route-names"></a>
## <a name="route-names"></a><span data-ttu-id="7646b-260">路由名稱</span><span class="sxs-lookup"><span data-stu-id="7646b-260">Route Names</span></span>

<span data-ttu-id="7646b-261">在 Web API 中，每個路由都有一個名稱。</span><span class="sxs-lookup"><span data-stu-id="7646b-261">In Web API, every route has a name.</span></span> <span data-ttu-id="7646b-262">路由名稱適用于產生連結，因此您可以在 HTTP 回應中包含連結。</span><span class="sxs-lookup"><span data-stu-id="7646b-262">Route names are useful for generating links, so that you can include a link in an HTTP response.</span></span>

<span data-ttu-id="7646b-263">若要指定路由名稱，請在屬性上設定**name**屬性。</span><span class="sxs-lookup"><span data-stu-id="7646b-263">To specify the route name, set the **Name** property on the attribute.</span></span> <span data-ttu-id="7646b-264">下列範例顯示如何設定路由名稱，以及如何在產生連結時使用路由名稱。</span><span class="sxs-lookup"><span data-stu-id="7646b-264">The following example shows how to set the route name, and also how to use the route name when generating a link.</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample21.cs)]

<a id="order"></a>
## <a name="route-order"></a><span data-ttu-id="7646b-265">路由順序</span><span class="sxs-lookup"><span data-stu-id="7646b-265">Route Order</span></span>

<span data-ttu-id="7646b-266">當架構嘗試比對 URI 與路由時，會以特定順序評估路由。</span><span class="sxs-lookup"><span data-stu-id="7646b-266">When the framework tries to match a URI with a route, it evaluates the routes in a particular order.</span></span> <span data-ttu-id="7646b-267">若要指定順序，請設定 route 屬性的**order**屬性。</span><span class="sxs-lookup"><span data-stu-id="7646b-267">To specify the order, set the **Order** property on the route attribute.</span></span> <span data-ttu-id="7646b-268">較低的值會先進行評估。</span><span class="sxs-lookup"><span data-stu-id="7646b-268">Lower values are evaluated first.</span></span> <span data-ttu-id="7646b-269">預設順序值為零。</span><span class="sxs-lookup"><span data-stu-id="7646b-269">The default order value is zero.</span></span>

<span data-ttu-id="7646b-270">以下是決定總計順序的方式：</span><span class="sxs-lookup"><span data-stu-id="7646b-270">Here is how the total ordering is determined:</span></span>

1. <span data-ttu-id="7646b-271">比較 route 屬性的**Order**屬性。</span><span class="sxs-lookup"><span data-stu-id="7646b-271">Compare the **Order** property of the route attribute.</span></span>
2. <span data-ttu-id="7646b-272">查看路由範本中的每個 URI 區段。</span><span class="sxs-lookup"><span data-stu-id="7646b-272">Look at each URI segment in the route template.</span></span> <span data-ttu-id="7646b-273">針對每個區段，順序如下：</span><span class="sxs-lookup"><span data-stu-id="7646b-273">For each segment, order as follows:</span></span>

    1. <span data-ttu-id="7646b-274">常值區段。</span><span class="sxs-lookup"><span data-stu-id="7646b-274">Literal segments.</span></span>
    2. <span data-ttu-id="7646b-275">具有條件約束的路由參數。</span><span class="sxs-lookup"><span data-stu-id="7646b-275">Route parameters with constraints.</span></span>
    3. <span data-ttu-id="7646b-276">沒有條件約束的路由參數。</span><span class="sxs-lookup"><span data-stu-id="7646b-276">Route parameters without constraints.</span></span>
    4. <span data-ttu-id="7646b-277">具有條件約束的萬用字元參數區段。</span><span class="sxs-lookup"><span data-stu-id="7646b-277">Wildcard parameter segments with constraints.</span></span>
    5. <span data-ttu-id="7646b-278">沒有條件約束的萬用字元參數區段。</span><span class="sxs-lookup"><span data-stu-id="7646b-278">Wildcard parameter segments without constraints.</span></span>
3. <span data-ttu-id="7646b-279">如果是系結，路由會依路由範本的不區分大小寫序數位串比較（[OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)）排序。</span><span class="sxs-lookup"><span data-stu-id="7646b-279">In the case of a tie, routes are ordered by a case-insensitive ordinal string comparison ([OrdinalIgnoreCase](https://msdn.microsoft.com/library/system.stringcomparer.ordinalignorecase.aspx)) of the route template.</span></span>

<span data-ttu-id="7646b-280">以下是一個範例。</span><span class="sxs-lookup"><span data-stu-id="7646b-280">Here is an example.</span></span> <span data-ttu-id="7646b-281">假設您定義下列控制器：</span><span class="sxs-lookup"><span data-stu-id="7646b-281">Suppose you define the following controller:</span></span>

[!code-csharp[Main](attribute-routing-in-web-api-2/samples/sample22.cs)]

<span data-ttu-id="7646b-282">這些路由的順序如下所示。</span><span class="sxs-lookup"><span data-stu-id="7646b-282">These routes are ordered as follows.</span></span>

1. <span data-ttu-id="7646b-283">訂單/詳細資料</span><span class="sxs-lookup"><span data-stu-id="7646b-283">orders/details</span></span>
2. <span data-ttu-id="7646b-284">訂單/{id}</span><span class="sxs-lookup"><span data-stu-id="7646b-284">orders/{id}</span></span>
3. <span data-ttu-id="7646b-285">orders/{customerName}</span><span class="sxs-lookup"><span data-stu-id="7646b-285">orders/{customerName}</span></span>
4. <span data-ttu-id="7646b-286">訂單/{\*日期}</span><span class="sxs-lookup"><span data-stu-id="7646b-286">orders/{\*date}</span></span>
5. <span data-ttu-id="7646b-287">訂單/暫止</span><span class="sxs-lookup"><span data-stu-id="7646b-287">orders/pending</span></span>

<span data-ttu-id="7646b-288">請注意，「詳細資料」是常值區段，而且會出現在 "{id}" 之前，但 "pending" 最後會出現，因為**Order**屬性是1。</span><span class="sxs-lookup"><span data-stu-id="7646b-288">Notice that "details" is a literal segment and appears before "{id}", but "pending" appears last because the **Order** property is 1.</span></span> <span data-ttu-id="7646b-289">（此範例假設沒有名為「詳細資料」或「擱置」的客戶。</span><span class="sxs-lookup"><span data-stu-id="7646b-289">(This example assumes there are no customers named "details" or "pending".</span></span> <span data-ttu-id="7646b-290">一般來說，請嘗試避免不明確的路由。</span><span class="sxs-lookup"><span data-stu-id="7646b-290">In general, try to avoid ambiguous routes.</span></span> <span data-ttu-id="7646b-291">在此範例中，`GetByCustomer` 的較佳路由範本是 "customers/{customerName}"）</span><span class="sxs-lookup"><span data-stu-id="7646b-291">In this example, a better route template for `GetByCustomer` is "customers/{customerName}" )</span></span>
