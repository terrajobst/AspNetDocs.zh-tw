---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: ASP.NET Web API 中的參數系結-ASP.NET 4。x
author: MikeWasson
description: 描述 Web API 如何系結參數，以及如何在 ASP.NET 4.x 中自訂系結程式。
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: 464cb9b45dc0b62c4da38b7cf612934808854d32
ms.sourcegitcommit: e365196c75ce93cd8967412b1cfdc27121816110
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/07/2020
ms.locfileid: "77074900"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="5c59d-103">ASP.NET Web API 中的參數系結</span><span class="sxs-lookup"><span data-stu-id="5c59d-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="5c59d-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="5c59d-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[!INCLUDE[](~/includes/coreWebAPI.md)]

<span data-ttu-id="5c59d-105">本文說明 Web API 如何系結參數，以及如何自訂系結程式。</span><span class="sxs-lookup"><span data-stu-id="5c59d-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="5c59d-106">當 Web API 呼叫控制器上的方法時，它必須設定參數的值，這是一個稱為*binding*的進程。</span><span class="sxs-lookup"><span data-stu-id="5c59d-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span>

<span data-ttu-id="5c59d-107">根據預設，Web API 會使用下列規則來系結參數：</span><span class="sxs-lookup"><span data-stu-id="5c59d-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="5c59d-108">如果參數是「簡單」類型，Web API 會嘗試從 URI 取得值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="5c59d-109">簡單類型包括 .NET[基本類型](https://msdn.microsoft.com/library/system.type.isprimitive.aspx)（**int**、 **bool**、 **double**等等），加上**TimeSpan**、 **DateTime**、 **Guid**、 **decimal**和**string**，*再加上*具有可從字串轉換之類型轉換器的任何類型。</span><span class="sxs-lookup"><span data-stu-id="5c59d-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="5c59d-110">（稍後會有關于類型轉換器的詳細資訊）。</span><span class="sxs-lookup"><span data-stu-id="5c59d-110">(More about type converters later.)</span></span>
- <span data-ttu-id="5c59d-111">針對複雜類型，Web API 會嘗試使用[媒體類型格式](media-formatters.md)器，從訊息本文中讀取值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="5c59d-112">例如，以下是典型的 Web API 控制器方法：</span><span class="sxs-lookup"><span data-stu-id="5c59d-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="5c59d-113">*Id*參數是 &quot;簡單&quot; 類型，因此 Web API 會嘗試從要求 URI 取得值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="5c59d-114">*Item*參數是複雜型別，因此 Web API 會使用媒體類型格式器來讀取來自要求主體的值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="5c59d-115">為了從 URI 取得值，Web API 會在路由資料和 URI 查詢字串中尋找。</span><span class="sxs-lookup"><span data-stu-id="5c59d-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="5c59d-116">當路由系統剖析 URI 並使其符合路由時，就會填入路由資料。</span><span class="sxs-lookup"><span data-stu-id="5c59d-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="5c59d-117">如需詳細資訊，請參閱[路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="5c59d-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="5c59d-118">在本文的其餘部分，我將示範如何自訂模型系結程式。</span><span class="sxs-lookup"><span data-stu-id="5c59d-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="5c59d-119">不過，如果是複雜類型，請考慮盡可能使用媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="5c59d-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="5c59d-120">HTTP 的主要原則是在訊息本文中傳送資源，使用內容協商來指定資源的標記法。</span><span class="sxs-lookup"><span data-stu-id="5c59d-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="5c59d-121">媒體類型格式器是專為此目的而設計的。</span><span class="sxs-lookup"><span data-stu-id="5c59d-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="5c59d-122">使用 [FromUri]</span><span class="sxs-lookup"><span data-stu-id="5c59d-122">Using [FromUri]</span></span>

<span data-ttu-id="5c59d-123">若要強制 Web API 從 URI 讀取複雜型別，請將 **[FromUri]** 屬性加入至參數。</span><span class="sxs-lookup"><span data-stu-id="5c59d-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="5c59d-124">下列範例會定義 `GeoPoint` 型別，以及可從 URI 取得 `GeoPoint` 的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="5c59d-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="5c59d-125">用戶端可以將緯度和經度值放在查詢字串中，而 Web API 會使用它們來建立 `GeoPoint`。</span><span class="sxs-lookup"><span data-stu-id="5c59d-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="5c59d-126">例如：</span><span class="sxs-lookup"><span data-stu-id="5c59d-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="5c59d-127">使用 [FromBody]</span><span class="sxs-lookup"><span data-stu-id="5c59d-127">Using [FromBody]</span></span>

<span data-ttu-id="5c59d-128">若要強制 Web API 從要求主體讀取簡單的類型，請將 **[FromBody]** 屬性加入至參數：</span><span class="sxs-lookup"><span data-stu-id="5c59d-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="5c59d-129">在此範例中，Web API 會使用媒體類型格式器來讀取要求主體中的*名稱*值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="5c59d-130">以下是範例用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="5c59d-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="5c59d-131">當參數具有 [FromBody] 時，Web API 會使用 Content-type 標頭來選取格式器。</span><span class="sxs-lookup"><span data-stu-id="5c59d-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="5c59d-132">在此範例中，內容類型為 &quot;application/json&quot;，而要求本文是原始 JSON 字串（而不是 JSON 物件）。</span><span class="sxs-lookup"><span data-stu-id="5c59d-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="5c59d-133">最多隻能有一個參數讀取訊息本文。</span><span class="sxs-lookup"><span data-stu-id="5c59d-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="5c59d-134">這將無法正常執行：</span><span class="sxs-lookup"><span data-stu-id="5c59d-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="5c59d-135">此規則的原因是要求主體可能儲存在只能讀取一次的非緩衝資料流程中。</span><span class="sxs-lookup"><span data-stu-id="5c59d-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="5c59d-136">類型轉換器</span><span class="sxs-lookup"><span data-stu-id="5c59d-136">Type Converters</span></span>

<span data-ttu-id="5c59d-137">您可以藉由建立**TypeConverter**並提供字串轉換，讓 web api 將類別視為簡單類型（因此 web api 會嘗試從 URI 系結）。</span><span class="sxs-lookup"><span data-stu-id="5c59d-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="5c59d-138">下列程式碼顯示代表地理點的 `GeoPoint` 類別，加上從字串轉換成 `GeoPoint` 實例的**TypeConverter** 。</span><span class="sxs-lookup"><span data-stu-id="5c59d-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="5c59d-139">`GeoPoint` 類別會以 **[TypeConverter]** 屬性裝飾，以指定類型轉換器。</span><span class="sxs-lookup"><span data-stu-id="5c59d-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="5c59d-140">（此範例是由 Mike 延遲的 blog 文章所靈感，[如何在 MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)中系結至動作簽章中的自訂物件）。</span><span class="sxs-lookup"><span data-stu-id="5c59d-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="5c59d-141">Web API 現在會將 `GeoPoint` 視為簡單的類型，這表示它會嘗試從 URI 系結 `GeoPoint` 參數。</span><span class="sxs-lookup"><span data-stu-id="5c59d-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="5c59d-142">您不需要在參數上包含 **[FromUri]** 。</span><span class="sxs-lookup"><span data-stu-id="5c59d-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="5c59d-143">用戶端可以使用如下的 URI 叫用方法：</span><span class="sxs-lookup"><span data-stu-id="5c59d-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="5c59d-144">模型繫結器</span><span class="sxs-lookup"><span data-stu-id="5c59d-144">Model Binders</span></span>

<span data-ttu-id="5c59d-145">比類型轉換器更有彈性的選項是建立自訂模型系結器。</span><span class="sxs-lookup"><span data-stu-id="5c59d-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="5c59d-146">使用模型系結器時，您可以存取來自路由資料的 HTTP 要求、動作描述和原始值等專案。</span><span class="sxs-lookup"><span data-stu-id="5c59d-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="5c59d-147">若要建立模型系結器，請執行**IModelBinder**介面。</span><span class="sxs-lookup"><span data-stu-id="5c59d-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="5c59d-148">這個介面會定義單一方法**BindModel**：</span><span class="sxs-lookup"><span data-stu-id="5c59d-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="5c59d-149">以下是 `GeoPoint` 物件的模型系結器。</span><span class="sxs-lookup"><span data-stu-id="5c59d-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="5c59d-150">模型系結器會從*值提供者*取得原始輸入值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="5c59d-151">這種設計會分隔兩個不同的功能：</span><span class="sxs-lookup"><span data-stu-id="5c59d-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="5c59d-152">值提供者會接受 HTTP 要求，並填入索引鍵/值組的字典。</span><span class="sxs-lookup"><span data-stu-id="5c59d-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="5c59d-153">模型系結器會使用這個字典來填入模型。</span><span class="sxs-lookup"><span data-stu-id="5c59d-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="5c59d-154">Web API 中的預設值提供者會從路由資料和查詢字串中取得值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="5c59d-155">例如，如果 URI 為 `http://localhost/api/values/1?location=48,-122`，則值提供者會建立下列機碼值組：</span><span class="sxs-lookup"><span data-stu-id="5c59d-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="5c59d-156">識別碼 = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="5c59d-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="5c59d-157">location = &quot;48122&quot;</span><span class="sxs-lookup"><span data-stu-id="5c59d-157">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="5c59d-158">（我假設預設路由範本，也就是 &quot;api/{controller}/{id}&quot;）。</span><span class="sxs-lookup"><span data-stu-id="5c59d-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="5c59d-159">要系結的參數名稱會儲存在**ModelBindingCoNtext. ModelName**屬性中。</span><span class="sxs-lookup"><span data-stu-id="5c59d-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="5c59d-160">模型系結器會在字典中尋找具有此值的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="5c59d-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="5c59d-161">如果值存在，而且可以轉換成 `GeoPoint`，則模型系結器會將系結值指派給**ModelBindingCoNtext 模型**屬性。</span><span class="sxs-lookup"><span data-stu-id="5c59d-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="5c59d-162">請注意，模型系結器並不限於簡單的類型轉換。</span><span class="sxs-lookup"><span data-stu-id="5c59d-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="5c59d-163">在此範例中，模型系結器會先在已知位置的資料表中尋找，如果失敗，則會使用類型轉換。</span><span class="sxs-lookup"><span data-stu-id="5c59d-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="5c59d-164">**設定模型系結器**</span><span class="sxs-lookup"><span data-stu-id="5c59d-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="5c59d-165">有數種方式可以設定模型系結器。</span><span class="sxs-lookup"><span data-stu-id="5c59d-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="5c59d-166">首先，您可以將 **[ModelBinder]** 屬性加入至參數。</span><span class="sxs-lookup"><span data-stu-id="5c59d-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="5c59d-167">您也可以將 **[ModelBinder]** 屬性加入至類型。</span><span class="sxs-lookup"><span data-stu-id="5c59d-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="5c59d-168">Web API 會針對該類型的所有參數使用指定的模型系結器。</span><span class="sxs-lookup"><span data-stu-id="5c59d-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="5c59d-169">最後，您可以將模型系結器提供者加入至**HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="5c59d-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="5c59d-170">模型系結器提供者只是建立模型系結器的 factory 類別。</span><span class="sxs-lookup"><span data-stu-id="5c59d-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="5c59d-171">您可以藉由衍生自[ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx)類別來建立提供者。</span><span class="sxs-lookup"><span data-stu-id="5c59d-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="5c59d-172">不過，如果您的模型系結器會處理單一型別，則使用專為此用途而設計的內建**SimpleModelBinderProvider**會比較容易。</span><span class="sxs-lookup"><span data-stu-id="5c59d-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="5c59d-173">下列程式碼示範如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="5c59d-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="5c59d-174">使用模型系結提供者時，您仍然需要將 **[ModelBinder]** 屬性加入至參數，以告知 Web API 應該使用模型系結器，而不是媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="5c59d-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="5c59d-175">但現在您不需要在屬性中指定模型系結器的類型：</span><span class="sxs-lookup"><span data-stu-id="5c59d-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="5c59d-176">值提供者</span><span class="sxs-lookup"><span data-stu-id="5c59d-176">Value Providers</span></span>

<span data-ttu-id="5c59d-177">我說過，模型系結器會從值提供者取得值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="5c59d-178">若要撰寫自訂值提供者，請執行**IValueProvider**介面。</span><span class="sxs-lookup"><span data-stu-id="5c59d-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="5c59d-179">以下是從要求中的 cookie 提取值的範例：</span><span class="sxs-lookup"><span data-stu-id="5c59d-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="5c59d-180">您也必須藉由衍生自**ValueProviderFactory**類別，來建立值提供者 factory。</span><span class="sxs-lookup"><span data-stu-id="5c59d-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="5c59d-181">將值提供者 factory 新增至**HttpConfiguration** ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="5c59d-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="5c59d-182">Web API 會撰寫所有的值提供者，因此當模型系結器呼叫**ValueProvider**時，模型系結器會從第一個值提供者接收能夠產生它的值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="5c59d-183">或者，您可以使用**ValueProvider**屬性，在參數層級設定值提供者 factory，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5c59d-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="5c59d-184">這會告知 Web API 使用模型系結搭配指定的值提供者 factory，而不是使用任何其他已註冊的值提供者。</span><span class="sxs-lookup"><span data-stu-id="5c59d-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="5c59d-185">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="5c59d-185">HttpParameterBinding</span></span>

<span data-ttu-id="5c59d-186">模型系結器是較通用機制的特定實例。</span><span class="sxs-lookup"><span data-stu-id="5c59d-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="5c59d-187">如果您查看 **[ModelBinder]** 屬性，您會看到它衍生自抽象的**ParameterBindingAttribute**類別。</span><span class="sxs-lookup"><span data-stu-id="5c59d-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="5c59d-188">這個類別會定義單一方法**getbindingexpression**，它會傳回**HttpParameterBinding**物件：</span><span class="sxs-lookup"><span data-stu-id="5c59d-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="5c59d-189">**HttpParameterBinding**會負責將參數系結至值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="5c59d-190">在 **[ModelBinder]** 的案例中，屬性會傳回使用**IModelBinder**執行實際系結的**HttpParameterBinding**實值。</span><span class="sxs-lookup"><span data-stu-id="5c59d-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="5c59d-191">您也可以執行自己的**HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="5c59d-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="5c59d-192">例如，假設您想要從 `if-match` 取得 Etag，並在要求中 `if-none-match` 標頭。</span><span class="sxs-lookup"><span data-stu-id="5c59d-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="5c59d-193">首先，我們會定義一個類別來代表 Etag。</span><span class="sxs-lookup"><span data-stu-id="5c59d-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="5c59d-194">我們也會定義列舉，指出是否要從 `if-match` 標頭或 `if-none-match` 標頭取得 ETag。</span><span class="sxs-lookup"><span data-stu-id="5c59d-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="5c59d-195">以下**HttpParameterBinding**會從所需的標頭取得 ETag，並將其系結至 etag 類型的參數：</span><span class="sxs-lookup"><span data-stu-id="5c59d-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="5c59d-196">**ExecuteBindingAsync**方法會執行系結。</span><span class="sxs-lookup"><span data-stu-id="5c59d-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="5c59d-197">在此方法中，將系結參數值新增至**HttpActionCoNtext**中的**ActionArgument**字典。</span><span class="sxs-lookup"><span data-stu-id="5c59d-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="5c59d-198">如果您的**ExecuteBindingAsync**方法會讀取要求訊息的主體，請覆寫**WillReadBody**屬性以傳回 true。</span><span class="sxs-lookup"><span data-stu-id="5c59d-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="5c59d-199">要求主體可能是只能讀取一次的未緩衝資料流程，因此 Web API 會強制執行一個規則，其中最多隻能有一個系結讀取訊息本文。</span><span class="sxs-lookup"><span data-stu-id="5c59d-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>

<span data-ttu-id="5c59d-200">若要套用自訂**HttpParameterBinding**，您可以定義衍生自**ParameterBindingAttribute**的屬性。</span><span class="sxs-lookup"><span data-stu-id="5c59d-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="5c59d-201">針對 `ETagParameterBinding`，我們將定義兩個屬性，一個用於 `if-match` 標頭，另一個用於 `if-none-match` 標頭。</span><span class="sxs-lookup"><span data-stu-id="5c59d-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="5c59d-202">兩者都是衍生自抽象基類。</span><span class="sxs-lookup"><span data-stu-id="5c59d-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="5c59d-203">以下是使用 `[IfNoneMatch]` 屬性的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="5c59d-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="5c59d-204">除了**ParameterBindingAttribute**之外，還有另一個加入自訂**HttpParameterBinding**的勾點。</span><span class="sxs-lookup"><span data-stu-id="5c59d-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="5c59d-205">在**HttpConfiguration**物件上， **ParameterBindingRules**屬性是類型（**HttpParameterDescriptor** -&gt; **HttpParameterBinding**）之匿名函式的集合。</span><span class="sxs-lookup"><span data-stu-id="5c59d-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="5c59d-206">例如，您可以新增規則，GET 方法上的任何 ETag 參數都會使用 `ETagParameterBinding` 搭配 `if-none-match`：</span><span class="sxs-lookup"><span data-stu-id="5c59d-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="5c59d-207">函式應該會針對不適用系結的參數傳回 `null`。</span><span class="sxs-lookup"><span data-stu-id="5c59d-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="5c59d-208">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="5c59d-208">IActionValueBinder</span></span>

<span data-ttu-id="5c59d-209">整個參數系結程式是由可插入的服務（ **IActionValueBinder**）所控制。</span><span class="sxs-lookup"><span data-stu-id="5c59d-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="5c59d-210">**IActionValueBinder**的預設執行會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="5c59d-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="5c59d-211">在參數上尋找**ParameterBindingAttribute** 。</span><span class="sxs-lookup"><span data-stu-id="5c59d-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="5c59d-212">這包括 **[FromBody]** 、 **[FromUri]** 和 **[ModelBinder]** ，或自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="5c59d-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="5c59d-213">否則，請針對傳回非 null **HttpParameterBinding**的函式，尋找**HttpConfiguration. ParameterBindingRules** 。</span><span class="sxs-lookup"><span data-stu-id="5c59d-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="5c59d-214">否則，請使用我先前所述的預設規則。</span><span class="sxs-lookup"><span data-stu-id="5c59d-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="5c59d-215">如果參數類型為 "simple" 或具有類型轉換器，請從 URI 進行系結。</span><span class="sxs-lookup"><span data-stu-id="5c59d-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="5c59d-216">這相當於將 **[FromUri]** 屬性放在參數上。</span><span class="sxs-lookup"><span data-stu-id="5c59d-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="5c59d-217">否則，請嘗試從訊息本文中讀取參數。</span><span class="sxs-lookup"><span data-stu-id="5c59d-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="5c59d-218">這相當於將 **[FromBody]** 放在參數上。</span><span class="sxs-lookup"><span data-stu-id="5c59d-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="5c59d-219">如有需要，您可以將整個**IActionValueBinder**服務取代為自訂的執行。</span><span class="sxs-lookup"><span data-stu-id="5c59d-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="5c59d-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="5c59d-220">Additional Resources</span></span>

[<span data-ttu-id="5c59d-221">自訂參數系結範例</span><span class="sxs-lookup"><span data-stu-id="5c59d-221">Custom Parameter Binding Sample</span></span>](https://github.com/aspnet/samples/tree/master/samples/aspnet/WebApi/CustomParameterBinding)

<span data-ttu-id="5c59d-222">Mike 的停止寫了一系列有關 Web API 參數系結的絕佳 blog 文章：</span><span class="sxs-lookup"><span data-stu-id="5c59d-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="5c59d-223">Web API 如何進行參數系結</span><span class="sxs-lookup"><span data-stu-id="5c59d-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="5c59d-224">Web API 的 MVC 樣式參數系結</span><span class="sxs-lookup"><span data-stu-id="5c59d-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="5c59d-225">如何在 MVC/Web API 中系結至動作簽章中的自訂物件</span><span class="sxs-lookup"><span data-stu-id="5c59d-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="5c59d-226">如何在 Web API 中建立自訂值提供者</span><span class="sxs-lookup"><span data-stu-id="5c59d-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="5c59d-227">幕後的 Web API 參數系結</span><span class="sxs-lookup"><span data-stu-id="5c59d-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
