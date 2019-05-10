---
uid: web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
title: 參數繫結在 ASP.NET Web API-ASP.NET 4.x
author: MikeWasson
description: 描述 Web API 如何繫結參數，以及如何自訂繫結程序，在 ASP.NET 4.x。
ms.author: riande
ms.date: 07/11/2013
ms.custom: seoapril2019
ms.assetid: e42c8388-04ed-4341-9fdb-41b1b4c06320
msc.legacyurl: /web-api/overview/formats-and-model-binding/parameter-binding-in-aspnet-web-api
msc.type: authoredcontent
ms.openlocfilehash: da0b9e12fcbe5cd2bfb5478162b7453d34931edf
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65127514"
---
# <a name="parameter-binding-in-aspnet-web-api"></a><span data-ttu-id="754d4-103">ASP.NET Web API 中繫結的參數</span><span class="sxs-lookup"><span data-stu-id="754d4-103">Parameter Binding in ASP.NET Web API</span></span>

<span data-ttu-id="754d4-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="754d4-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="754d4-105">這篇文章描述 Web API 如何繫結參數，以及如何自訂繫結程序。</span><span class="sxs-lookup"><span data-stu-id="754d4-105">This article describes how Web API binds parameters, and how you can customize the binding process.</span></span> <span data-ttu-id="754d4-106">當 Web API 控制器上呼叫方法時，它必須設定參數的值，這個程序稱為*繫結*。</span><span class="sxs-lookup"><span data-stu-id="754d4-106">When Web API calls a method on a controller, it must set values for the parameters, a process called *binding*.</span></span> 

<span data-ttu-id="754d4-107">根據預設，Web API 會使用下列規則來將參數繫結：</span><span class="sxs-lookup"><span data-stu-id="754d4-107">By default, Web API uses the following rules to bind parameters:</span></span>

- <span data-ttu-id="754d4-108">如果參數是 「 簡單 」 類型，Web API 會嘗試從 URI 取得的值。</span><span class="sxs-lookup"><span data-stu-id="754d4-108">If the parameter is a "simple" type, Web API tries to get the value from the URI.</span></span> <span data-ttu-id="754d4-109">簡單類型包括.NET[基本型別](https://msdn.microsoft.com/library/system.type.isprimitive.aspx)(**int**， **bool**， **double**，依此類推)，再加上**TimeSpan**， **DateTime**， **Guid**， **decimal**，並**字串**，*加上*任何類型從字串可以轉換型別轉換子。</span><span class="sxs-lookup"><span data-stu-id="754d4-109">Simple types include the .NET [primitive types](https://msdn.microsoft.com/library/system.type.isprimitive.aspx) (**int**, **bool**, **double**, and so forth), plus **TimeSpan**, **DateTime**, **Guid**, **decimal**, and **string**, *plus* any type with a type converter that can convert from a string.</span></span> <span data-ttu-id="754d4-110">（深入了解稍後型別轉換子。）</span><span class="sxs-lookup"><span data-stu-id="754d4-110">(More about type converters later.)</span></span>
- <span data-ttu-id="754d4-111">複雜型別，Web API 嘗試讀取訊息主體中的值時，使用[media-type 格式器](media-formatters.md)。</span><span class="sxs-lookup"><span data-stu-id="754d4-111">For complex types, Web API tries to read the value from the message body, using a [media-type formatter](media-formatters.md).</span></span>

<span data-ttu-id="754d4-112">例如，以下是典型的 Web API 控制器方法：</span><span class="sxs-lookup"><span data-stu-id="754d4-112">For example, here is a typical Web API controller method:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample1.cs)]

<span data-ttu-id="754d4-113">*識別碼*參數是&quot;簡單&quot;型別，因此 Web API 會嘗試取得要求 URI 中的值。</span><span class="sxs-lookup"><span data-stu-id="754d4-113">The *id* parameter is a &quot;simple&quot; type, so Web API tries to get the value from the request URI.</span></span> <span data-ttu-id="754d4-114">*項目*參數是複雜類型，因此 Web API 使用的媒體類型格式器來讀取的要求主體中的值。</span><span class="sxs-lookup"><span data-stu-id="754d4-114">The *item* parameter is a complex type, so Web API uses a media-type formatter to read the value from the request body.</span></span>

<span data-ttu-id="754d4-115">若要從 URI 取得值，Web API 看起來的路由資料和 URI 查詢字串中。</span><span class="sxs-lookup"><span data-stu-id="754d4-115">To get a value from the URI, Web API looks in the route data and the URI query string.</span></span> <span data-ttu-id="754d4-116">當路由系統會剖析的 URI，並進行比對路由，則會填入的路由資料。</span><span class="sxs-lookup"><span data-stu-id="754d4-116">The route data is populated when the routing system parses the URI and matches it to a route.</span></span> <span data-ttu-id="754d4-117">如需詳細資訊，請參閱 <<c0> [ 路由和動作選取](../web-api-routing-and-actions/routing-and-action-selection.md)。</span><span class="sxs-lookup"><span data-stu-id="754d4-117">For more information, see [Routing and Action Selection](../web-api-routing-and-actions/routing-and-action-selection.md).</span></span>

<span data-ttu-id="754d4-118">在這篇文章的其餘部分，我將示範如何自訂模型繫結程序。</span><span class="sxs-lookup"><span data-stu-id="754d4-118">In the rest of this article, I'll show how you can customize the model binding process.</span></span> <span data-ttu-id="754d4-119">複雜型別，不過，請考慮使用盡可能的媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="754d4-119">For complex types, however, consider using media-type formatters whenever possible.</span></span> <span data-ttu-id="754d4-120">HTTP 的主要原則是資源會在訊息主體中，使用內容交涉，以指定資源的表示法。</span><span class="sxs-lookup"><span data-stu-id="754d4-120">A key principle of HTTP is that resources are sent in the message body, using content negotiation to specify the representation of the resource.</span></span> <span data-ttu-id="754d4-121">針對完全此用途所設計的媒體類型格式器。</span><span class="sxs-lookup"><span data-stu-id="754d4-121">Media-type formatters were designed for exactly this purpose.</span></span>

## <a name="using-fromuri"></a><span data-ttu-id="754d4-122">使用 [FromUri]</span><span class="sxs-lookup"><span data-stu-id="754d4-122">Using [FromUri]</span></span>

<span data-ttu-id="754d4-123">若要強制 Web API，可讀取的 URI 中的複雜型別，請新增 **[FromUri]** 屬性至參數。</span><span class="sxs-lookup"><span data-stu-id="754d4-123">To force Web API to read a complex type from the URI, add the **[FromUri]** attribute to the parameter.</span></span> <span data-ttu-id="754d4-124">下列範例會定義`GeoPoint`型別，以及取得控制器方法`GeoPoint`從 URI。</span><span class="sxs-lookup"><span data-stu-id="754d4-124">The following example defines a `GeoPoint` type, along with a controller method that gets the `GeoPoint` from the URI.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample2.cs)]

<span data-ttu-id="754d4-125">用戶端可以將緯度和經度值放在查詢字串和 Web API 會使用這些來建構`GeoPoint`。</span><span class="sxs-lookup"><span data-stu-id="754d4-125">The client can put the Latitude and Longitude values in the query string and Web API will use them to construct a `GeoPoint`.</span></span> <span data-ttu-id="754d4-126">例如: </span><span class="sxs-lookup"><span data-stu-id="754d4-126">For example:</span></span>

`http://localhost/api/values/?Latitude=47.678558&Longitude=-122.130989`

## <a name="using-frombody"></a><span data-ttu-id="754d4-127">使用 [FromBody]</span><span class="sxs-lookup"><span data-stu-id="754d4-127">Using [FromBody]</span></span>

<span data-ttu-id="754d4-128">若要強制 Web API，可讀取的要求主體中的簡單類型，新增 **[FromBody]** 屬性至參數：</span><span class="sxs-lookup"><span data-stu-id="754d4-128">To force Web API to read a simple type from the request body, add the **[FromBody]** attribute to the parameter:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample3.cs)]

<span data-ttu-id="754d4-129">在此範例中，Web API 會讀取的值使用的媒體類型格式器*名稱*從要求主體。</span><span class="sxs-lookup"><span data-stu-id="754d4-129">In this example, Web API will use a media-type formatter to read the value of *name* from the request body.</span></span> <span data-ttu-id="754d4-130">以下是範例用戶端要求。</span><span class="sxs-lookup"><span data-stu-id="754d4-130">Here is an example client request.</span></span>

[!code-console[Main](parameter-binding-in-aspnet-web-api/samples/sample4.cmd)]

<span data-ttu-id="754d4-131">參數會有 [FromBody]，Web API 會使用 Content-type 標頭來選取格式器。</span><span class="sxs-lookup"><span data-stu-id="754d4-131">When a parameter has [FromBody], Web API uses the Content-Type header to select a formatter.</span></span> <span data-ttu-id="754d4-132">在此範例中，內容類型是&quot;application/json&quot;和要求主體是原始的 JSON 字串 （而不是 JSON 物件）。</span><span class="sxs-lookup"><span data-stu-id="754d4-132">In this example, the content type is &quot;application/json&quot; and the request body is a raw JSON string (not a JSON object).</span></span>

<span data-ttu-id="754d4-133">最多一個參數可以讀取訊息主體。</span><span class="sxs-lookup"><span data-stu-id="754d4-133">At most one parameter is allowed to read from the message body.</span></span> <span data-ttu-id="754d4-134">因此，這不適用：</span><span class="sxs-lookup"><span data-stu-id="754d4-134">So this will not work:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample5.cs)]

<span data-ttu-id="754d4-135">此規則的原因是，可能只讀取一次的非緩衝處理資料流中儲存的要求主體。</span><span class="sxs-lookup"><span data-stu-id="754d4-135">The reason for this rule is that the request body might be stored in a non-buffered stream that can only be read once.</span></span>

## <a name="type-converters"></a><span data-ttu-id="754d4-136">類型轉換器</span><span class="sxs-lookup"><span data-stu-id="754d4-136">Type Converters</span></span>

<span data-ttu-id="754d4-137">您可以讓類別視為簡單型別 （以便讓 Web API 會嘗試將它繫結從 URI） 的 Web API 建立**TypeConverter**並提供字串轉換。</span><span class="sxs-lookup"><span data-stu-id="754d4-137">You can make Web API treat a class as a simple type (so that Web API will try to bind it from the URI) by creating a **TypeConverter** and providing a string conversion.</span></span>

<span data-ttu-id="754d4-138">下列程式碼示範`GeoPoint`類別，表示地理的點，再加上**TypeConverter**可將字串的轉換`GeoPoint`執行個體。</span><span class="sxs-lookup"><span data-stu-id="754d4-138">The following code shows a `GeoPoint` class that represents a geographical point, plus a **TypeConverter** that converts from strings to `GeoPoint` instances.</span></span> <span data-ttu-id="754d4-139">`GeoPoint`類別以裝飾 **[TypeConverter]** 屬性來指定型別轉換子。</span><span class="sxs-lookup"><span data-stu-id="754d4-139">The `GeoPoint` class is decorated with a **[TypeConverter]** attribute to specify the type converter.</span></span> <span data-ttu-id="754d4-140">(此範例由 Mike Stall 的部落格文章啟發[如何繫結至 MVC/WebAPI 中的動作簽章中的自訂物件](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)。)</span><span class="sxs-lookup"><span data-stu-id="754d4-140">(This example was inspired by Mike Stall's blog post [How to bind to custom objects in action signatures in MVC/WebAPI](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx).)</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample6.cs)]

<span data-ttu-id="754d4-141">現在會將 Web API`GeoPoint`為簡單型別，亦即它會嘗試繫結`GeoPoint`來自 URI 的參數。</span><span class="sxs-lookup"><span data-stu-id="754d4-141">Now Web API will treat `GeoPoint` as a simple type, meaning it will try to bind `GeoPoint` parameters from the URI.</span></span> <span data-ttu-id="754d4-142">您不需要包含 **[FromUri]** 參數上。</span><span class="sxs-lookup"><span data-stu-id="754d4-142">You don't need to include **[FromUri]** on the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample7.cs)]

<span data-ttu-id="754d4-143">用戶端可以叫用的方法，就像這樣的 uri:</span><span class="sxs-lookup"><span data-stu-id="754d4-143">The client can invoke the method with a URI like this:</span></span>

`http://localhost/api/values/?location=47.678558,-122.130989`

## <a name="model-binders"></a><span data-ttu-id="754d4-144">模型繫結器</span><span class="sxs-lookup"><span data-stu-id="754d4-144">Model Binders</span></span>

<span data-ttu-id="754d4-145">型別轉換子比更有彈性的選項是建立自訂模型繫結。</span><span class="sxs-lookup"><span data-stu-id="754d4-145">A more flexible option than a type converter is to create a custom model binder.</span></span> <span data-ttu-id="754d4-146">使用模型繫結，您必須存取 HTTP 要求、 動作描述，以及原始值等項目從路由資料。</span><span class="sxs-lookup"><span data-stu-id="754d4-146">With a model binder, you have access to things like the HTTP request, the action description, and the raw values from the route data.</span></span>

<span data-ttu-id="754d4-147">若要建立的模型繫結器，實作**IModelBinder**介面。</span><span class="sxs-lookup"><span data-stu-id="754d4-147">To create a model binder, implement the **IModelBinder** interface.</span></span> <span data-ttu-id="754d4-148">這個介面會定義單一方法**BindModel**:</span><span class="sxs-lookup"><span data-stu-id="754d4-148">This interface defines a single method, **BindModel**:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample8.cs)]

<span data-ttu-id="754d4-149">以下是模型繫結器`GeoPoint`物件。</span><span class="sxs-lookup"><span data-stu-id="754d4-149">Here is a model binder for `GeoPoint` objects.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample9.cs)]

<span data-ttu-id="754d4-150">模型繫結取得未經處理輸入的值從*值提供者*。</span><span class="sxs-lookup"><span data-stu-id="754d4-150">A model binder gets raw input values from a *value provider*.</span></span> <span data-ttu-id="754d4-151">這項設計會分隔兩個不同的功能：</span><span class="sxs-lookup"><span data-stu-id="754d4-151">This design separates two distinct functions:</span></span>

- <span data-ttu-id="754d4-152">值提供者會接受 HTTP 要求，並於其中填入索引鍵 / 值組的字典。</span><span class="sxs-lookup"><span data-stu-id="754d4-152">The value provider takes the HTTP request and populates a dictionary of key-value pairs.</span></span>
- <span data-ttu-id="754d4-153">模型繫結會使用此字典，來擴展模型。</span><span class="sxs-lookup"><span data-stu-id="754d4-153">The model binder uses this dictionary to populate the model.</span></span>

<span data-ttu-id="754d4-154">在 Web API 中的預設值提供者會取得值，從路由資料和查詢字串。</span><span class="sxs-lookup"><span data-stu-id="754d4-154">The default value provider in Web API gets values from the route data and the query string.</span></span> <span data-ttu-id="754d4-155">比方說，如果 URI 為`http://localhost/api/values/1?location=48,-122`，值提供者會建立下列機碼值組：</span><span class="sxs-lookup"><span data-stu-id="754d4-155">For example, if the URI is `http://localhost/api/values/1?location=48,-122`, the value provider creates the following key-value pairs:</span></span>

- <span data-ttu-id="754d4-156">id = &quot;1&quot;</span><span class="sxs-lookup"><span data-stu-id="754d4-156">id = &quot;1&quot;</span></span>
- <span data-ttu-id="754d4-157">位置 = &quot;48,122&quot;</span><span class="sxs-lookup"><span data-stu-id="754d4-157">location = &quot;48,122&quot;</span></span>

<span data-ttu-id="754d4-158">(我假設是預設的路由範本，也就是&quot;api / {controller} / {id}&quot;。)</span><span class="sxs-lookup"><span data-stu-id="754d4-158">(I'm assuming the default route template, which is &quot;api/{controller}/{id}&quot;.)</span></span>

<span data-ttu-id="754d4-159">要繫結參數的名稱會儲存在**ModelBindingContext.ModelName**屬性。</span><span class="sxs-lookup"><span data-stu-id="754d4-159">The name of the parameter to bind is stored in the **ModelBindingContext.ModelName** property.</span></span> <span data-ttu-id="754d4-160">模型繫結會尋找與這個字典中值的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="754d4-160">The model binder looks for a key with this value in the dictionary.</span></span> <span data-ttu-id="754d4-161">如果該值存在，而且可以轉換成`GeoPoint`，模型繫結器繫結將值指派給**ModelBindingContext.Model**屬性。</span><span class="sxs-lookup"><span data-stu-id="754d4-161">If the value exists and can be converted into a `GeoPoint`, the model binder assigns the bound value to the **ModelBindingContext.Model** property.</span></span>

<span data-ttu-id="754d4-162">請注意，模型繫結並不會限制為簡單的型別轉換。</span><span class="sxs-lookup"><span data-stu-id="754d4-162">Notice that the model binder is not limited to a simple type conversion.</span></span> <span data-ttu-id="754d4-163">在此範例中，模型繫結器會先尋找已知的位置，資料表中，如果失敗，它會使用型別轉換。</span><span class="sxs-lookup"><span data-stu-id="754d4-163">In this example, the model binder first looks in a table of known locations, and if that fails, it uses type conversion.</span></span>

<span data-ttu-id="754d4-164">**設定模型繫結**</span><span class="sxs-lookup"><span data-stu-id="754d4-164">**Setting the Model Binder**</span></span>

<span data-ttu-id="754d4-165">有數種方式可設定的模型繫結器。</span><span class="sxs-lookup"><span data-stu-id="754d4-165">There are several ways to set a model binder.</span></span> <span data-ttu-id="754d4-166">首先，您可以在其中加入 **[ModelBinder]** 屬性至參數。</span><span class="sxs-lookup"><span data-stu-id="754d4-166">First, you can add a **[ModelBinder]** attribute to the parameter.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample10.cs)]

<span data-ttu-id="754d4-167">您也可以加入 **[ModelBinder]** 屬性型別。</span><span class="sxs-lookup"><span data-stu-id="754d4-167">You can also add a **[ModelBinder]** attribute to the type.</span></span> <span data-ttu-id="754d4-168">Web API 會使用指定的模型繫結，該類型的所有參數。</span><span class="sxs-lookup"><span data-stu-id="754d4-168">Web API will use the specified model binder for all parameters of that type.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample11.cs)]

<span data-ttu-id="754d4-169">最後，您可以在其中新增模型繫結器提供者**HttpConfiguration**。</span><span class="sxs-lookup"><span data-stu-id="754d4-169">Finally, you can add a model-binder provider to the **HttpConfiguration**.</span></span> <span data-ttu-id="754d4-170">模型繫結器提供者是只建立的模型繫結器的 factory 類別。</span><span class="sxs-lookup"><span data-stu-id="754d4-170">A model-binder provider is simply a factory class that creates a model binder.</span></span> <span data-ttu-id="754d4-171">您可以建立提供者透過衍生自[ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx)類別。</span><span class="sxs-lookup"><span data-stu-id="754d4-171">You can create a provider by deriving from the [ModelBinderProvider](https://msdn.microsoft.com/library/system.web.http.modelbinding.modelbinderprovider.aspx) class.</span></span> <span data-ttu-id="754d4-172">不過，如果您的模型繫結器會處理單一的類型，它是使用內建的工作變得更容易**SimpleModelBinderProvider**，這針對此用途而設計。</span><span class="sxs-lookup"><span data-stu-id="754d4-172">However, if your model binder handles a single type, it's easier to use the built-in **SimpleModelBinderProvider**, which is designed for this purpose.</span></span> <span data-ttu-id="754d4-173">下列程式碼示範如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="754d4-173">The following code shows how to do this.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample12.cs)]

<span data-ttu-id="754d4-174">使用模型繫結提供者，您仍然需要新增 **[ModelBinder]** 屬性至參數，來告訴 Web API，它應該使用模型繫結和未 media-type 格式器。</span><span class="sxs-lookup"><span data-stu-id="754d4-174">With a model-binding provider, you still need to add the **[ModelBinder]** attribute to the parameter, to tell Web API that it should use a model binder and not a media-type formatter.</span></span> <span data-ttu-id="754d4-175">但現在，您不必在屬性中指定的模型繫結器類型：</span><span class="sxs-lookup"><span data-stu-id="754d4-175">But now you don't need to specify the type of model binder in the attribute:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample13.cs)]

## <a name="value-providers"></a><span data-ttu-id="754d4-176">值提供者</span><span class="sxs-lookup"><span data-stu-id="754d4-176">Value Providers</span></span>

<span data-ttu-id="754d4-177">我說過的模型繫結器取得值，來自值提供者。</span><span class="sxs-lookup"><span data-stu-id="754d4-177">I mentioned that a model binder gets values from a value provider.</span></span> <span data-ttu-id="754d4-178">若要撰寫的自訂值提供者，實作**IValueProvider**介面。</span><span class="sxs-lookup"><span data-stu-id="754d4-178">To write a custom value provider, implement the **IValueProvider** interface.</span></span> <span data-ttu-id="754d4-179">提取要求中的 cookie 中的值範例如下：</span><span class="sxs-lookup"><span data-stu-id="754d4-179">Here is an example that pulls values from the cookies in the request:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample14.cs)]

<span data-ttu-id="754d4-180">您也需要建立值提供者 factory 藉由衍生自**ValueProviderFactory**類別。</span><span class="sxs-lookup"><span data-stu-id="754d4-180">You also need to create a value provider factory by deriving from the **ValueProviderFactory** class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample15.cs)]

<span data-ttu-id="754d4-181">新增至值提供者處理站**HttpConfiguration** ，如下所示。</span><span class="sxs-lookup"><span data-stu-id="754d4-181">Add the value provider factory to the **HttpConfiguration** as follows.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample16.cs)]

<span data-ttu-id="754d4-182">Web API 撰寫所有值提供者，因此當模型繫結呼叫**ValueProvider.GetValue**，模型繫結會從第一個能夠產生它的值提供者收到的值。</span><span class="sxs-lookup"><span data-stu-id="754d4-182">Web API composes all of the value providers, so when a model binder calls **ValueProvider.GetValue**, the model binder receives the value from the first value provider that is able to produce it.</span></span>

<span data-ttu-id="754d4-183">或者，使用參數層級設定值提供者 factory **ValueProvider**屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="754d4-183">Alternatively, you can set the value provider factory at the parameter level by using the **ValueProvider** attribute, as follows:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample17.cs)]

<span data-ttu-id="754d4-184">這會告知模型繫結使用指定的值提供者處理站，且不使用任何其他已註冊的值提供者的 Web API。</span><span class="sxs-lookup"><span data-stu-id="754d4-184">This tells Web API to use model binding with the specified value provider factory, and not to use any of the other registered value providers.</span></span>

## <a name="httpparameterbinding"></a><span data-ttu-id="754d4-185">HttpParameterBinding</span><span class="sxs-lookup"><span data-stu-id="754d4-185">HttpParameterBinding</span></span>

<span data-ttu-id="754d4-186">模型繫結器的較通用的機制的特定執行個體。</span><span class="sxs-lookup"><span data-stu-id="754d4-186">Model binders are a specific instance of a more general mechanism.</span></span> <span data-ttu-id="754d4-187">如果您看一下 **[ModelBinder]** 屬性，您會看到它會衍生自抽象**ParameterBindingAttribute**類別。</span><span class="sxs-lookup"><span data-stu-id="754d4-187">If you look at the **[ModelBinder]** attribute, you will see that it derives from the abstract **ParameterBindingAttribute** class.</span></span> <span data-ttu-id="754d4-188">這個類別會定義單一方法**GetBinding**，以傳回**HttpParameterBinding**物件：</span><span class="sxs-lookup"><span data-stu-id="754d4-188">This class defines a single method, **GetBinding**, which returns an **HttpParameterBinding** object:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample18.cs)]

<span data-ttu-id="754d4-189">**HttpParameterBinding**會負責將參數繫結的值。</span><span class="sxs-lookup"><span data-stu-id="754d4-189">An **HttpParameterBinding** is responsible for binding a parameter to a value.</span></span> <span data-ttu-id="754d4-190">若是 **[ModelBinder]**，屬性會傳回**HttpParameterBinding**實作會使用**IModelBinder**執行實際的繫結。</span><span class="sxs-lookup"><span data-stu-id="754d4-190">In the case of **[ModelBinder]**, the attribute returns an **HttpParameterBinding** implementation that uses an **IModelBinder** to perform the actual binding.</span></span> <span data-ttu-id="754d4-191">您也可以實作您自己**HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="754d4-191">You can also implement your own **HttpParameterBinding**.</span></span>

<span data-ttu-id="754d4-192">例如，假設您想要取得從 Etag`if-match`和`if-none-match`要求中的標頭。</span><span class="sxs-lookup"><span data-stu-id="754d4-192">For example, suppose you want to get ETags from `if-match` and `if-none-match` headers in the request.</span></span> <span data-ttu-id="754d4-193">我們一開始先定義一個類別來表示 Etag。</span><span class="sxs-lookup"><span data-stu-id="754d4-193">We'll start by defining a class to represent ETags.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample19.cs)]

<span data-ttu-id="754d4-194">我們也會定義列舉，指出要取得所產生的 ETag`if-match`標頭或`if-none-match`標頭。</span><span class="sxs-lookup"><span data-stu-id="754d4-194">We'll also define an enumeration to indicate whether to get the ETag from the `if-match` header or the `if-none-match` header.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample20.cs)]

<span data-ttu-id="754d4-195">以下是**HttpParameterBinding** ，取得所需的標頭的 ETag，並將它繫結至類型參數的 ETag:</span><span class="sxs-lookup"><span data-stu-id="754d4-195">Here is an **HttpParameterBinding** that gets the ETag from the desired header and binds it to a parameter of type ETag:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample21.cs)]

<span data-ttu-id="754d4-196">**ExecuteBindingAsync**方法會繫結。</span><span class="sxs-lookup"><span data-stu-id="754d4-196">The **ExecuteBindingAsync** method does the binding.</span></span> <span data-ttu-id="754d4-197">在此方法中，加入繫結的參數值**ActionArgument**中的字典**HttpActionContext**。</span><span class="sxs-lookup"><span data-stu-id="754d4-197">Within this method, add the bound parameter value to the **ActionArgument** dictionary in the **HttpActionContext**.</span></span>

> [!NOTE]
> <span data-ttu-id="754d4-198">如果您**ExecuteBindingAsync**方法會讀取要求訊息的本文中，覆寫**WillReadBody**屬性傳回 true。</span><span class="sxs-lookup"><span data-stu-id="754d4-198">If your **ExecuteBindingAsync** method reads the body of the request message, override the **WillReadBody** property to return true.</span></span> <span data-ttu-id="754d4-199">要求主體可能只能讀取一次，讓 Web API 會強制執行規則，最多一個繫結的緩衝資料流可讀取訊息主體。</span><span class="sxs-lookup"><span data-stu-id="754d4-199">The request body might be an unbuffered stream that can only be read once, so Web API enforces a rule that at most one binding can read the message body.</span></span>

<span data-ttu-id="754d4-200">若要套用自訂**HttpParameterBinding**，您可以定義屬性衍生自**ParameterBindingAttribute**。</span><span class="sxs-lookup"><span data-stu-id="754d4-200">To apply a custom **HttpParameterBinding**, you can define an attribute that derives from **ParameterBindingAttribute**.</span></span> <span data-ttu-id="754d4-201">針對`ETagParameterBinding`，我們會定義兩個屬性，一個用於`if-match`標頭，另一個用於`if-none-match`標頭。</span><span class="sxs-lookup"><span data-stu-id="754d4-201">For `ETagParameterBinding`, we'll define two attributes, one for `if-match` headers and one for `if-none-match` headers.</span></span> <span data-ttu-id="754d4-202">都是衍生自抽象基底類別。</span><span class="sxs-lookup"><span data-stu-id="754d4-202">Both derive from an abstract base class.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample22.cs)]

<span data-ttu-id="754d4-203">以下是使用控制器方法`[IfNoneMatch]`屬性。</span><span class="sxs-lookup"><span data-stu-id="754d4-203">Here is a controller method that uses the `[IfNoneMatch]` attribute.</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample23.cs)]

<span data-ttu-id="754d4-204">除了**ParameterBindingAttribute**，沒有新增自訂的另一個攔截**HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="754d4-204">Besides **ParameterBindingAttribute**, there is another hook for adding a custom **HttpParameterBinding**.</span></span> <span data-ttu-id="754d4-205">在  **HttpConfiguration**物件， **ParameterBindingRules**屬性是類型的匿名函式的集合 (**HttpParameterDescriptor**  - &gt; **HttpParameterBinding**)。</span><span class="sxs-lookup"><span data-stu-id="754d4-205">On the **HttpConfiguration** object, the **ParameterBindingRules** property is a collection of anonymous functions of type (**HttpParameterDescriptor** -&gt; **HttpParameterBinding**).</span></span> <span data-ttu-id="754d4-206">比方說，您可以在其中新增任何的 GET 方法上的 ETag 參數使用的規則`ETagParameterBinding`與`if-none-match`:</span><span class="sxs-lookup"><span data-stu-id="754d4-206">For example, you could add a rule that any ETag parameter on a GET method uses `ETagParameterBinding` with `if-none-match`:</span></span>

[!code-csharp[Main](parameter-binding-in-aspnet-web-api/samples/sample24.cs)]

<span data-ttu-id="754d4-207">函式應傳回`null`繫結不適用的參數。</span><span class="sxs-lookup"><span data-stu-id="754d4-207">The function should return `null` for parameters where the binding is not applicable.</span></span>

## <a name="iactionvaluebinder"></a><span data-ttu-id="754d4-208">IActionValueBinder</span><span class="sxs-lookup"><span data-stu-id="754d4-208">IActionValueBinder</span></span>

<span data-ttu-id="754d4-209">整個參數繫結程序由隨插即用的服務，控制**IActionValueBinder**。</span><span class="sxs-lookup"><span data-stu-id="754d4-209">The entire parameter-binding process is controlled by a pluggable service, **IActionValueBinder**.</span></span> <span data-ttu-id="754d4-210">預設實作**IActionValueBinder**會進行下列作業：</span><span class="sxs-lookup"><span data-stu-id="754d4-210">The default implementation of **IActionValueBinder** does the following:</span></span>

1. <span data-ttu-id="754d4-211">尋求**ParameterBindingAttribute**參數上。</span><span class="sxs-lookup"><span data-stu-id="754d4-211">Look for a **ParameterBindingAttribute** on the parameter.</span></span> <span data-ttu-id="754d4-212">這包括 **[FromBody]**， **[FromUri]**，並 **[ModelBinder]**，或自訂屬性。</span><span class="sxs-lookup"><span data-stu-id="754d4-212">This includes **[FromBody]**, **[FromUri]**, and **[ModelBinder]**, or custom attributes.</span></span>
2. <span data-ttu-id="754d4-213">否則，請查看**HttpConfiguration.ParameterBindingRules**函式會傳回非 null **HttpParameterBinding**。</span><span class="sxs-lookup"><span data-stu-id="754d4-213">Otherwise, look in **HttpConfiguration.ParameterBindingRules** for a function that returns a non-null **HttpParameterBinding**.</span></span>
3. <span data-ttu-id="754d4-214">否則，請使用先前所述的預設規則。</span><span class="sxs-lookup"><span data-stu-id="754d4-214">Otherwise, use the default rules that I described previously.</span></span> 

    - <span data-ttu-id="754d4-215">如果參數類型為 「 簡單 」，或具有型別轉換子，從 URI 繫結。</span><span class="sxs-lookup"><span data-stu-id="754d4-215">If the parameter type is "simple"or has a type converter, bind from the URI.</span></span> <span data-ttu-id="754d4-216">這相當於將放 **[FromUri]** 參數上的屬性。</span><span class="sxs-lookup"><span data-stu-id="754d4-216">This is equivalent to putting the **[FromUri]** attribute on the parameter.</span></span>
    - <span data-ttu-id="754d4-217">否則，嘗試讀取訊息主體中的參數。</span><span class="sxs-lookup"><span data-stu-id="754d4-217">Otherwise, try to read the parameter from the message body.</span></span> <span data-ttu-id="754d4-218">這相當於將放 **[FromBody]** 參數上。</span><span class="sxs-lookup"><span data-stu-id="754d4-218">This is equivalent to putting **[FromBody]** on the parameter.</span></span>

<span data-ttu-id="754d4-219">如果您想，您可以取代整個**IActionValueBinder**服務的自訂實作。</span><span class="sxs-lookup"><span data-stu-id="754d4-219">If you wanted, you could replace the entire **IActionValueBinder** service with a custom implementation.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="754d4-220">其他資源</span><span class="sxs-lookup"><span data-stu-id="754d4-220">Additional Resources</span></span>

[<span data-ttu-id="754d4-221">自訂參數繫結範例</span><span class="sxs-lookup"><span data-stu-id="754d4-221">Custom Parameter Binding Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/CustomParameterBinding/ReadMe.txt)

<span data-ttu-id="754d4-222">Mike Stall 撰寫有關 Web API 的參數繫結的良好的一連串的部落格文章：</span><span class="sxs-lookup"><span data-stu-id="754d4-222">Mike Stall wrote a good series of blog posts about Web API parameter binding:</span></span>

- [<span data-ttu-id="754d4-223">Web API 是怎麼參數繫結</span><span class="sxs-lookup"><span data-stu-id="754d4-223">How Web API does Parameter Binding</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/16/how-webapi-does-parameter-binding.aspx)
- [<span data-ttu-id="754d4-224">Web API 的 MVC 樣式參數繫結</span><span class="sxs-lookup"><span data-stu-id="754d4-224">MVC Style parameter binding for Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/18/mvc-style-parameter-binding-for-webapi.aspx)
- [<span data-ttu-id="754d4-225">如何繫結至 MVC/Web API 中的動作簽章中的自訂物件</span><span class="sxs-lookup"><span data-stu-id="754d4-225">How to bind to custom objects in action signatures in MVC/Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/20/how-to-bind-to-custom-objects-in-action-signatures-in-mvc-webapi.aspx)
- [<span data-ttu-id="754d4-226">如何在 Web API 中建立的自訂值提供者</span><span class="sxs-lookup"><span data-stu-id="754d4-226">How to create a custom value provider in Web API</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/04/23/how-to-create-a-custom-value-provider-in-webapi.aspx)
- [<span data-ttu-id="754d4-227">背後原理的 web API 參數繫結</span><span class="sxs-lookup"><span data-stu-id="754d4-227">Web API Parameter binding under the hood</span></span>](https://blogs.msdn.com/b/jmstall/archive/2012/05/11/webapi-parameter-binding-under-the-hood.aspx)
