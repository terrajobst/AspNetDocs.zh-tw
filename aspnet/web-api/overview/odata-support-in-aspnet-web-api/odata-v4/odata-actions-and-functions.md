---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
title: 使用 ASP.NET Web API 2.2 的 OData v4 中的動作和函式 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，動作和函式是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。 本教學課程顯示如何 。
ms.author: riande
ms.date: 06/27/2014
ms.assetid: 0e6fb03c-b16d-4bb0-ab0b-552bd2b6ece1
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/odata-actions-and-functions
msc.type: authoredcontent
ms.openlocfilehash: f5af94e93e5b7f2351d40febbf1a468d635c9db1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556221"
---
# <a name="actions-and-functions-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="4b158-104">使用 ASP.NET Web API 2.2 的 OData v4 中的動作和函式</span><span class="sxs-lookup"><span data-stu-id="4b158-104">Actions and Functions in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="4b158-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="4b158-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="4b158-106">在 OData 中，動作和函式是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="4b158-106">In OData, actions and functions are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="4b158-107">本教學課程說明如何使用 Web API 2.2，將動作和函式加入至 OData v4 端點。</span><span class="sxs-lookup"><span data-stu-id="4b158-107">This tutorial shows how to add actions and functions to an OData v4 endpoint, using Web API 2.2.</span></span> <span data-ttu-id="4b158-108">本教學課程是[以使用 ASP.NET Web API 2 建立 OData V4 端點](create-an-odata-v4-endpoint.md)教學課程為基礎</span><span class="sxs-lookup"><span data-stu-id="4b158-108">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="4b158-109">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="4b158-109">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="4b158-110">Web API 2。2</span><span class="sxs-lookup"><span data-stu-id="4b158-110">Web API 2.2</span></span>
> - <span data-ttu-id="4b158-111">OData v4</span><span class="sxs-lookup"><span data-stu-id="4b158-111">OData v4</span></span>
> - <span data-ttu-id="4b158-112">Visual Studio 2013 （[在此](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下載 Visual Studio 2017）</span><span class="sxs-lookup"><span data-stu-id="4b158-112">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="4b158-113">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="4b158-113">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="4b158-114">教學課程版本</span><span class="sxs-lookup"><span data-stu-id="4b158-114">Tutorial versions</span></span>
>
> <span data-ttu-id="4b158-115">針對 OData 第3版，請參閱[ASP.NET Web API 2 中的 Odata 動作](../odata-v3/odata-actions.md)。</span><span class="sxs-lookup"><span data-stu-id="4b158-115">For OData Version 3, see [OData Actions in ASP.NET Web API 2](../odata-v3/odata-actions.md).</span></span>

<span data-ttu-id="4b158-116">*動作*和函式之間的差異在於動作可以有副作用，而函式則*不會。*</span><span class="sxs-lookup"><span data-stu-id="4b158-116">The difference between *actions* and *functions* is that actions can have side effects, and functions do not.</span></span> <span data-ttu-id="4b158-117">動作和函數都可以傳回資料。</span><span class="sxs-lookup"><span data-stu-id="4b158-117">Both actions and functions can return data.</span></span> <span data-ttu-id="4b158-118">某些動作的用途包括：</span><span class="sxs-lookup"><span data-stu-id="4b158-118">Some uses for actions include:</span></span>

- <span data-ttu-id="4b158-119">複雜交易。</span><span class="sxs-lookup"><span data-stu-id="4b158-119">Complex transactions.</span></span>
- <span data-ttu-id="4b158-120">一次處理數個實體。</span><span class="sxs-lookup"><span data-stu-id="4b158-120">Manipulating several entities at once.</span></span>
- <span data-ttu-id="4b158-121">僅允許更新實體的特定屬性。</span><span class="sxs-lookup"><span data-stu-id="4b158-121">Allowing updates only to certain properties of an entity.</span></span>
- <span data-ttu-id="4b158-122">傳送不是實體的資料。</span><span class="sxs-lookup"><span data-stu-id="4b158-122">Sending data that is not an entity.</span></span>

<span data-ttu-id="4b158-123">函數適用于傳回未直接對應至實體或集合的資訊。</span><span class="sxs-lookup"><span data-stu-id="4b158-123">Functions are useful for returning information that does not correspond directly to an entity or collection.</span></span>

<span data-ttu-id="4b158-124">動作（或函式）可以將單一實體或集合設為目標。</span><span class="sxs-lookup"><span data-stu-id="4b158-124">An action (or function) can target a single entity or a collection.</span></span> <span data-ttu-id="4b158-125">在 OData 術語中，這是系*結。*</span><span class="sxs-lookup"><span data-stu-id="4b158-125">In OData terminology, this is the *binding*.</span></span> <span data-ttu-id="4b158-126">您也可以將 &quot;未系結的&quot; 動作/函式，稱為服務上的靜態作業。</span><span class="sxs-lookup"><span data-stu-id="4b158-126">You can also have &quot;unbound&quot; actions/functions, which are called as static operations on the service.</span></span>

## <a name="example-adding-an-action"></a><span data-ttu-id="4b158-127">範例：新增動作</span><span class="sxs-lookup"><span data-stu-id="4b158-127">Example: Adding an Action</span></span>

<span data-ttu-id="4b158-128">讓我們定義一個動作來為產品評分。</span><span class="sxs-lookup"><span data-stu-id="4b158-128">Let's define an action to rate a product.</span></span>

> [!NOTE]
> <span data-ttu-id="4b158-129">本教學課程是[以使用 ASP.NET Web API 2 建立 OData V4 端點](create-an-odata-v4-endpoint.md)教學課程為基礎</span><span class="sxs-lookup"><span data-stu-id="4b158-129">This tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md)</span></span>

<span data-ttu-id="4b158-130">首先，加入 `ProductRating` 模型來代表評等。</span><span class="sxs-lookup"><span data-stu-id="4b158-130">First, add a `ProductRating` model to represent the ratings.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample1.cs)]

<span data-ttu-id="4b158-131">此外，也請將**DbSet**新增至 `ProductsContext` 類別，以便 EF 在資料庫中建立評等資料表。</span><span class="sxs-lookup"><span data-stu-id="4b158-131">Also add a **DbSet** to the `ProductsContext` class, so that EF will create a Ratings table in the database.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample2.cs)]

### <a name="add-the-action-to-the-edm"></a><span data-ttu-id="4b158-132">將動作新增至 EDM</span><span class="sxs-lookup"><span data-stu-id="4b158-132">Add the Action to the EDM</span></span>

<span data-ttu-id="4b158-133">在 WebApiConfig.cs 中，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="4b158-133">In WebApiConfig.cs, add the following code:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample3.cs)]

<span data-ttu-id="4b158-134">**EntityTypeConfiguration**方法會將動作加入至 entity data MODEL （EDM）。</span><span class="sxs-lookup"><span data-stu-id="4b158-134">The **EntityTypeConfiguration.Action** method adds an action to the entity data model (EDM).</span></span> <span data-ttu-id="4b158-135">**參數**方法會為動作指定具類型的參數。</span><span class="sxs-lookup"><span data-stu-id="4b158-135">The **Parameter** method specifies a typed parameter for the action.</span></span>

<span data-ttu-id="4b158-136">此程式碼也會設定 EDM 的命名空間。</span><span class="sxs-lookup"><span data-stu-id="4b158-136">This code also sets the namespace for the EDM.</span></span> <span data-ttu-id="4b158-137">命名空間很重要，因為動作的 URI 包含完整的動作名稱：</span><span class="sxs-lookup"><span data-stu-id="4b158-137">The namespace matters because the URI for the action includes the fully-qualified action name:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample4.cmd)]

> [!NOTE]
> <span data-ttu-id="4b158-138">在一般的 IIS 設定中，此 URL 中的點會導致 IIS 傳回錯誤404。</span><span class="sxs-lookup"><span data-stu-id="4b158-138">In a typical IIS configuration, the dot in this URL will cause IIS to return error 404.</span></span> <span data-ttu-id="4b158-139">您可以藉由將下列區段新增至 web.config 檔案來解決此問題：</span><span class="sxs-lookup"><span data-stu-id="4b158-139">You can resolve this by adding the following section to your Web.Config file:</span></span>

[!code-xml[Main](odata-actions-and-functions/samples/sample5.xml)]

### <a name="add-a-controller-method-for-the-action"></a><span data-ttu-id="4b158-140">新增動作的控制器方法</span><span class="sxs-lookup"><span data-stu-id="4b158-140">Add a Controller Method for the Action</span></span>

<span data-ttu-id="4b158-141">若要啟用 &quot;速率&quot; 動作，請將下列方法新增至 `ProductsController`：</span><span class="sxs-lookup"><span data-stu-id="4b158-141">To enable the &quot;Rate&quot; action, add the following method to `ProductsController`:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample6.cs)]

<span data-ttu-id="4b158-142">請注意，方法名稱符合動作名稱。</span><span class="sxs-lookup"><span data-stu-id="4b158-142">Notice that the method name matches the action name.</span></span> <span data-ttu-id="4b158-143">**[HttpPost]** 屬性會指定方法是 HTTP POST 方法。</span><span class="sxs-lookup"><span data-stu-id="4b158-143">The **[HttpPost]** attribute specifies the method is an HTTP POST method.</span></span>

<span data-ttu-id="4b158-144">若要叫用動作，用戶端會傳送 HTTP POST 要求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4b158-144">To invoke the action, the client sends an HTTP POST request like the following:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample7.cmd)]

<span data-ttu-id="4b158-145">&quot;速率&quot; 動作會系結至產品實例，因此動作的 URI 是附加至實體 URI 的完整動作名稱。</span><span class="sxs-lookup"><span data-stu-id="4b158-145">The &quot;Rate&quot; action is bound to Product instances, so the URI for the action is the fully-qualified action name appended to the entity URI.</span></span> <span data-ttu-id="4b158-146">（回想一下，我們將 EDM 命名空間設定為 &quot;ProductService&quot;，因此完整的動作名稱 &quot;ProductService。速率&quot;）。</span><span class="sxs-lookup"><span data-stu-id="4b158-146">(Recall that we set the EDM namespace to &quot;ProductService&quot;, so the fully-qualified action name is &quot;ProductService.Rate&quot;.)</span></span>

<span data-ttu-id="4b158-147">要求的主體會將動作參數包含為 JSON 承載。</span><span class="sxs-lookup"><span data-stu-id="4b158-147">The body of the request contains the action parameters as a JSON payload.</span></span> <span data-ttu-id="4b158-148">Web API 會自動將 JSON 承載轉換成**ODataActionParameters**物件，這只是參數值的字典。</span><span class="sxs-lookup"><span data-stu-id="4b158-148">Web API automatically converts the JSON payload to an **ODataActionParameters** object, which is just a dictionary of parameter values.</span></span> <span data-ttu-id="4b158-149">使用此字典來存取控制器方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="4b158-149">Use this dictionary to access the parameters in your controller method.</span></span>

<span data-ttu-id="4b158-150">如果用戶端以錯誤的格式傳送動作參數， **ModelState**的值就是 false。</span><span class="sxs-lookup"><span data-stu-id="4b158-150">If the client sends the action parameters in the wrong format, the value of **ModelState.IsValid** is false.</span></span> <span data-ttu-id="4b158-151">請在控制器方法中檢查此旗標，並在 [ **IsValid** ] 為 false 時傳回錯誤。</span><span class="sxs-lookup"><span data-stu-id="4b158-151">Check this flag in your controller method and return an error if **IsValid** is false.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample8.cs)]

## <a name="example-adding-a-function"></a><span data-ttu-id="4b158-152">範例：新增函式</span><span class="sxs-lookup"><span data-stu-id="4b158-152">Example: Adding a Function</span></span>

<span data-ttu-id="4b158-153">現在讓我們加入 OData 函式，以傳回成本最高的產品。</span><span class="sxs-lookup"><span data-stu-id="4b158-153">Now let's add an OData function that returns the most expensive product.</span></span> <span data-ttu-id="4b158-154">如先前所述，第一個步驟是將函式新增至 EDM。</span><span class="sxs-lookup"><span data-stu-id="4b158-154">As before, the first step is adding the function to the EDM.</span></span> <span data-ttu-id="4b158-155">在 WebApiConfig.cs 中，新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="4b158-155">In WebApiConfig.cs, add the following code.</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample9.cs)]

<span data-ttu-id="4b158-156">在此情況下，函數會系結至 Products 集合，而不是個別的產品實例。</span><span class="sxs-lookup"><span data-stu-id="4b158-156">In this case, the function is bound to the Products collection, rather than individual Product instances.</span></span> <span data-ttu-id="4b158-157">用戶端會藉由傳送 GET 要求來叫用函式：</span><span class="sxs-lookup"><span data-stu-id="4b158-157">Clients invoke the function by sending a GET request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample10.cmd)]

<span data-ttu-id="4b158-158">以下是此函式的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="4b158-158">Here is the controller method for this function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample11.cs)]

<span data-ttu-id="4b158-159">請注意，方法名稱符合函數名稱。</span><span class="sxs-lookup"><span data-stu-id="4b158-159">Notice that the method name matches the function name.</span></span> <span data-ttu-id="4b158-160">**[HttpGet]** 屬性會指定方法是 HTTP GET 方法。</span><span class="sxs-lookup"><span data-stu-id="4b158-160">The **[HttpGet]** attribute specifies the method is an HTTP GET method.</span></span>

<span data-ttu-id="4b158-161">以下是 HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="4b158-161">Here is the HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample12.cmd)]

## <a name="example-adding-an-unbound-function"></a><span data-ttu-id="4b158-162">範例：加入未系結的函式</span><span class="sxs-lookup"><span data-stu-id="4b158-162">Example: Adding an Unbound Function</span></span>

<span data-ttu-id="4b158-163">上一個範例是系結至集合的函式。</span><span class="sxs-lookup"><span data-stu-id="4b158-163">The previous example was a function bound to a collection.</span></span> <span data-ttu-id="4b158-164">在下一個範例中，我們將建立*未*系結的函式。</span><span class="sxs-lookup"><span data-stu-id="4b158-164">In this next example, we'll create an *unbound* function.</span></span> <span data-ttu-id="4b158-165">未系結的函式會在服務上呼叫為靜態作業。</span><span class="sxs-lookup"><span data-stu-id="4b158-165">Unbound functions are called as static operations on the service.</span></span> <span data-ttu-id="4b158-166">此範例中的函式會傳回指定郵遞區號的銷售稅額。</span><span class="sxs-lookup"><span data-stu-id="4b158-166">The function in this example will return the sales tax for a given postal code.</span></span>

<span data-ttu-id="4b158-167">在 WebApiConfig 檔案中，將函式新增至 EDM：</span><span class="sxs-lookup"><span data-stu-id="4b158-167">In the WebApiConfig file, add the function to the EDM:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample13.cs)]

<span data-ttu-id="4b158-168">請注意，我們會直接在**用**上呼叫**函數**，而不是實體類型或集合。</span><span class="sxs-lookup"><span data-stu-id="4b158-168">Notice that we are calling **Function** directly on the **ODataModelBuilder**, instead of the entity type or collection.</span></span> <span data-ttu-id="4b158-169">這會告知模型產生器函式已解除系結。</span><span class="sxs-lookup"><span data-stu-id="4b158-169">This tells the model builder that the function is unbound.</span></span>

<span data-ttu-id="4b158-170">以下是可實作用函式的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="4b158-170">Here is the controller method that implements the function:</span></span>

[!code-csharp[Main](odata-actions-and-functions/samples/sample14.cs)]

<span data-ttu-id="4b158-171">您放置此方法的 Web API 控制器並不重要。</span><span class="sxs-lookup"><span data-stu-id="4b158-171">It does not matter which Web API controller you place this method in.</span></span> <span data-ttu-id="4b158-172">您可以將它放在 `ProductsController`中，或定義個別的控制器。</span><span class="sxs-lookup"><span data-stu-id="4b158-172">You could put it in `ProductsController`, or define a separate controller.</span></span> <span data-ttu-id="4b158-173">**[ODataRoute]** 屬性會定義函式的 URI 範本。</span><span class="sxs-lookup"><span data-stu-id="4b158-173">The **[ODataRoute]** attribute defines the URI template for the function.</span></span>

<span data-ttu-id="4b158-174">以下是用戶端要求範例：</span><span class="sxs-lookup"><span data-stu-id="4b158-174">Here is an example client request:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample15.cmd)]

<span data-ttu-id="4b158-175">HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="4b158-175">The HTTP response:</span></span>

[!code-console[Main](odata-actions-and-functions/samples/sample16.cmd)]
