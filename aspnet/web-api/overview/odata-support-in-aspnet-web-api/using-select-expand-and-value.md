---
uid: web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
title: 使用 $select，$expand、 和 $value 中 ASP.NET Web API 2 OData ASP.NET 4.x
author: MikeWasson
description: 展開為 $ 的概觀和程式碼範例，請 $select，和 $value 選項 OData Web API 2 中 ASP.NET 4.x。
ms.author: riande
ms.date: 10/11/2013
ms.custom: seoapril2019
ms.assetid: 43279a80-a96c-4564-b6ea-ad992a2d6828
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/using-select-expand-and-value
msc.type: authoredcontent
ms.openlocfilehash: 8b5d3e87c679a31f1908aa648219ae5c6b701a1f
ms.sourcegitcommit: 0f1119340e4464720cfd16d0ff15764746ea1fea
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 04/09/2019
ms.locfileid: "59400694"
---
# <a name="using-select-expand-and-value-in-aspnet-web-api-2-odata"></a><span data-ttu-id="348d8-103">使用 $select，$expand、 和 ASP.NET Web API 2 OData 中的 $value</span><span class="sxs-lookup"><span data-stu-id="348d8-103">Using $select, $expand, and $value in ASP.NET Web API 2 OData</span></span>

<span data-ttu-id="348d8-104">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="348d8-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="348d8-105">展開為 $ 的概觀和程式碼範例，請 $select，和 $value 選項 OData Web API 2 中 ASP.NET 4.x。</span><span class="sxs-lookup"><span data-stu-id="348d8-105">Overview and code samples for the $expand, $select, and $value options in OData Web API 2 for ASP.NET 4.x.</span></span> <span data-ttu-id="348d8-106">這些選項可讓用戶端來控制它回從伺服器取得的表示法。</span><span class="sxs-lookup"><span data-stu-id="348d8-106">These options allow a client to control the representation that it gets back from the server.</span></span>

- <span data-ttu-id="348d8-107">**$expand**會導致要在回應中的包含的內嵌的相關的實體。</span><span class="sxs-lookup"><span data-stu-id="348d8-107">**$expand** causes related entities to be included inline in the response.</span></span>
- <span data-ttu-id="348d8-108">**$select**選取要包含在回應中的屬性子集。</span><span class="sxs-lookup"><span data-stu-id="348d8-108">**$select** selects a subset of properties to include in the response.</span></span>
- <span data-ttu-id="348d8-109">**$value**取得屬性的原始值。</span><span class="sxs-lookup"><span data-stu-id="348d8-109">**$value** gets the raw value of a property.</span></span>

## <a name="example-schema"></a><span data-ttu-id="348d8-110">範例結構描述</span><span class="sxs-lookup"><span data-stu-id="348d8-110">Example Schema</span></span>

<span data-ttu-id="348d8-111">本文章中，我將使用的 OData 服務，會定義三個實體：產品、 供應商和類別目錄。</span><span class="sxs-lookup"><span data-stu-id="348d8-111">For this article, I'll use an OData service that defines three entities: Product, Supplier, and Category.</span></span> <span data-ttu-id="348d8-112">每個產品都有一個類別目錄和一個供應商。</span><span class="sxs-lookup"><span data-stu-id="348d8-112">Each product has one category and one supplier.</span></span>

![](using-select-expand-and-value/_static/image1.png)

<span data-ttu-id="348d8-113">以下是定義實體模型的 C# 類別：</span><span class="sxs-lookup"><span data-stu-id="348d8-113">Here are the C# classes that define the entity models:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample1.cs)]

<span data-ttu-id="348d8-114">請注意，`Product`類別會定義導覽屬性，如`Supplier`和`Category`。</span><span class="sxs-lookup"><span data-stu-id="348d8-114">Notice that the `Product` class defines navigation properties for the `Supplier` and `Category`.</span></span> <span data-ttu-id="348d8-115">`Category`類別會定義導覽屬性的產品，每個類別中。</span><span class="sxs-lookup"><span data-stu-id="348d8-115">The `Category` class defines a navigation property for the products in each category.</span></span>

<span data-ttu-id="348d8-116">若要建立此結構描述的 OData 端點，使用 Visual Studio 2013 scaffolding，如中所述[建立 ASP.NET Web API 中的 OData 端點](odata-v3/creating-an-odata-endpoint.md)。</span><span class="sxs-lookup"><span data-stu-id="348d8-116">To create an OData endpoint for this schema, use the Visual Studio 2013 scaffolding, as described in [Creating an OData Endpoint in ASP.NET Web API](odata-v3/creating-an-odata-endpoint.md).</span></span> <span data-ttu-id="348d8-117">新增個別的控制站的產品、 類別和供應商。</span><span class="sxs-lookup"><span data-stu-id="348d8-117">Add separate controllers for Product, Category, and Supplier.</span></span>

## <a name="enabling-expand-and-select"></a><span data-ttu-id="348d8-118">啟用 $展開和 $select</span><span class="sxs-lookup"><span data-stu-id="348d8-118">Enabling $expand and $select</span></span>

<span data-ttu-id="348d8-119">在 Visual Studio 2013 中的 Web API OData 樣板會先建立一個控制站，來自動支援 $expand 與 $select。</span><span class="sxs-lookup"><span data-stu-id="348d8-119">In Visual Studio 2013, the Web API OData scaffolding creates a controller that automatically supports $expand and $select.</span></span> <span data-ttu-id="348d8-120">如需參考，以下是支援 $ 需求展開和 $select 控制器中的。</span><span class="sxs-lookup"><span data-stu-id="348d8-120">For reference, here are the requirements to support $expand and $select in a controller.</span></span>

<span data-ttu-id="348d8-121">對於集合，控制站的`Get`方法必須傳回**IQueryable**。</span><span class="sxs-lookup"><span data-stu-id="348d8-121">For collections, the controller's `Get` method must return an **IQueryable**.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample2.cs)]

<span data-ttu-id="348d8-122">對於單一實體，會傳回**SingleResult&lt;T&gt;**，其中 T 是**IQueryable**包含零個或一個實體。</span><span class="sxs-lookup"><span data-stu-id="348d8-122">For single entities, return a **SingleResult&lt;T&gt;**, where T is an **IQueryable** that contains zero or one entities.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample3.cs)]

<span data-ttu-id="348d8-123">此外，裝飾您`Get`方法具有 **[Queryable]** 屬性，如先前的程式碼片段所示。</span><span class="sxs-lookup"><span data-stu-id="348d8-123">Also, decorate your `Get` methods with the **[Queryable]** attribute, as shown in the previous code snippets.</span></span> <span data-ttu-id="348d8-124">或者，呼叫**EnableQuerySupport**上**HttpConfiguration**在啟動的物件。</span><span class="sxs-lookup"><span data-stu-id="348d8-124">Alternatively, call **EnableQuerySupport** on the **HttpConfiguration** object at startup.</span></span> <span data-ttu-id="348d8-125">(如需詳細資訊，請參閱 <<c0> [ 啟用 OData 查詢選項](supporting-odata-query-options.md#enable)。)</span><span class="sxs-lookup"><span data-stu-id="348d8-125">(For more information, see [Enabling OData Query Options](supporting-odata-query-options.md#enable).)</span></span>

## <a name="using-expand"></a><span data-ttu-id="348d8-126">使用 $expand</span><span class="sxs-lookup"><span data-stu-id="348d8-126">Using $expand</span></span>

<span data-ttu-id="348d8-127">當您查詢之 OData 實體或集合時，預設回應不包含相關的實體。</span><span class="sxs-lookup"><span data-stu-id="348d8-127">When you query an OData entity or collection, the default response does not include related entities.</span></span> <span data-ttu-id="348d8-128">例如，以下是分類實體集的預設回應：</span><span class="sxs-lookup"><span data-stu-id="348d8-128">For example, here is the default response for the Categories entity set:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample4.cmd)]

<span data-ttu-id="348d8-129">如您所見，回應不包含任何產品，即使 Category 實體具有產品導覽連結。</span><span class="sxs-lookup"><span data-stu-id="348d8-129">As you can see, the response does not include any products, even though the Category entity has a Products navigation link.</span></span> <span data-ttu-id="348d8-130">不過，用戶端可以使用 $展開每個類別目錄中取得的產品清單。</span><span class="sxs-lookup"><span data-stu-id="348d8-130">However, the client can use $expand to get the list of products for each category.</span></span> <span data-ttu-id="348d8-131">$Expand 選項會要求查詢字串中：</span><span class="sxs-lookup"><span data-stu-id="348d8-131">The $expand option goes in the query string of the request:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample5.cmd)]

<span data-ttu-id="348d8-132">現在伺服器會包含每個類別與類別的內嵌產品。</span><span class="sxs-lookup"><span data-stu-id="348d8-132">Now the server will include the products for each category, inline with the categories.</span></span> <span data-ttu-id="348d8-133">以下是回應承載：</span><span class="sxs-lookup"><span data-stu-id="348d8-133">Here is the response payload:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample6.cmd)]

<span data-ttu-id="348d8-134">請注意每個項目"value"陣列中的包含的產品清單。</span><span class="sxs-lookup"><span data-stu-id="348d8-134">Notice that each entry in the "value" array contains a Products list.</span></span>

<span data-ttu-id="348d8-135">$ Expand 選項會採用以逗號分隔清單，以展開的導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="348d8-135">The $expand option takes a comma-separated list of navigation properties to expand.</span></span> <span data-ttu-id="348d8-136">下列要求會展開分類和產品的供應商。</span><span class="sxs-lookup"><span data-stu-id="348d8-136">The following request expands both the category and the supplier for a product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample7.cmd)]

<span data-ttu-id="348d8-137">以下是回應主體：</span><span class="sxs-lookup"><span data-stu-id="348d8-137">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample8.cmd)]

<span data-ttu-id="348d8-138">您可以展開導覽屬性的多個層的級。</span><span class="sxs-lookup"><span data-stu-id="348d8-138">You can expand more than one level of navigation property.</span></span> <span data-ttu-id="348d8-139">下列範例會加入分類的所有產品以及每項產品的供應商。</span><span class="sxs-lookup"><span data-stu-id="348d8-139">The following example includes all the products for a category and also the supplier for each product.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample9.cmd)]

<span data-ttu-id="348d8-140">以下是回應主體：</span><span class="sxs-lookup"><span data-stu-id="348d8-140">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample10.cmd)]

<span data-ttu-id="348d8-141">根據預設，Web API 會限制為 2 的最大展開深度。</span><span class="sxs-lookup"><span data-stu-id="348d8-141">By default, Web API limits the maximum expansion depth to 2.</span></span> <span data-ttu-id="348d8-142">這樣可防止用戶端傳送複雜的要求，例如`$expand=Orders/OrderDetails/Product/Supplier/Region`，這可能會沒有效率，來查詢及建立大型的回應。</span><span class="sxs-lookup"><span data-stu-id="348d8-142">That prevents the client from sending complex requests like `$expand=Orders/OrderDetails/Product/Supplier/Region`, which might be inefficient to query and create large responses.</span></span> <span data-ttu-id="348d8-143">若要覆寫預設值，請設定**MaxExpansionDepth**屬性上的 **[Queryable]** 屬性。</span><span class="sxs-lookup"><span data-stu-id="348d8-143">To override the default, set the **MaxExpansionDepth** property on the **[Queryable]** attribute.</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample11.cs)]

<span data-ttu-id="348d8-144">如需有關 $expand 選項，請參閱 < [Expand 系統查詢選項 ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand)官方的 OData 文件中。</span><span class="sxs-lookup"><span data-stu-id="348d8-144">For more information about the $expand option, see [Expand System Query Option ($expand)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#46_Expand_System_Query_Option_expand) in the official OData documentation.</span></span>

## <a name="using-select"></a><span data-ttu-id="348d8-145">使用 $select</span><span class="sxs-lookup"><span data-stu-id="348d8-145">Using $select</span></span>

<span data-ttu-id="348d8-146">$Select 選項指定要包含在回應主體中的屬性子集。</span><span class="sxs-lookup"><span data-stu-id="348d8-146">The $select option specifies a subset of properties to include in the response body.</span></span> <span data-ttu-id="348d8-147">例如，若要取得只有名稱和每個產品的價格，請使用下列查詢：</span><span class="sxs-lookup"><span data-stu-id="348d8-147">For example, to get only the name and price of each product, use the following query:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample12.cmd)]

<span data-ttu-id="348d8-148">以下是回應主體：</span><span class="sxs-lookup"><span data-stu-id="348d8-148">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample13.cmd)]

<span data-ttu-id="348d8-149">您可以結合 $select 及 $expand 中相同的查詢。</span><span class="sxs-lookup"><span data-stu-id="348d8-149">You can combine $select and $expand in the same query.</span></span> <span data-ttu-id="348d8-150">請確定已展開的屬性納入 $select 選項。</span><span class="sxs-lookup"><span data-stu-id="348d8-150">Make sure to include the expanded property in the $select option.</span></span> <span data-ttu-id="348d8-151">例如，下列要求會取得供應商與產品名稱。</span><span class="sxs-lookup"><span data-stu-id="348d8-151">For example, the following request gets the product name and supplier.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample14.cmd)]

<span data-ttu-id="348d8-152">以下是回應主體：</span><span class="sxs-lookup"><span data-stu-id="348d8-152">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample15.cmd)]

<span data-ttu-id="348d8-153">您也可以選取內展開屬性的屬性。</span><span class="sxs-lookup"><span data-stu-id="348d8-153">You can also select the properties within an expanded property.</span></span> <span data-ttu-id="348d8-154">下列要求會展開產品，並選取類別目錄名稱加上產品名稱。</span><span class="sxs-lookup"><span data-stu-id="348d8-154">The following request expands Products and selects category name plus product name.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample16.cmd)]

<span data-ttu-id="348d8-155">以下是回應主體：</span><span class="sxs-lookup"><span data-stu-id="348d8-155">Here is the response body:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample17.cmd)]

<span data-ttu-id="348d8-156">如需有關 $select 選項的詳細資訊，請參閱[Select 系統查詢選項 ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select)官方的 OData 文件中。</span><span class="sxs-lookup"><span data-stu-id="348d8-156">For more information about the $select option, see [Select System Query Option ($select)](http://www.odata.org/documentation/odata-v2-documentation/uri-conventions/#48_Select_System_Query_Option_select) in the official OData documentation.</span></span>

## <a name="getting-individual-properties-of-an-entity-value"></a><span data-ttu-id="348d8-157">取得實體 ($value) 的個別屬性</span><span class="sxs-lookup"><span data-stu-id="348d8-157">Getting Individual Properties of an Entity ($value)</span></span>

<span data-ttu-id="348d8-158">有兩種方式，從實體取得的個別屬性的 OData 用戶端。</span><span class="sxs-lookup"><span data-stu-id="348d8-158">There are two ways for an OData client to get an individual property from an entity.</span></span> <span data-ttu-id="348d8-159">用戶端可以取得 OData 格式的值，或取得屬性的原始值。</span><span class="sxs-lookup"><span data-stu-id="348d8-159">The client can either get the value in OData format, or get the raw value of the property.</span></span>

<span data-ttu-id="348d8-160">下列要求會取得 OData 格式的屬性。</span><span class="sxs-lookup"><span data-stu-id="348d8-160">The following request gets a property in OData format.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample18.cmd)]

<span data-ttu-id="348d8-161">以下是 JSON 格式的範例回應：</span><span class="sxs-lookup"><span data-stu-id="348d8-161">Here is an example response in JSON format:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample19.cmd)]

<span data-ttu-id="348d8-162">若要取得原始值的屬性，附加到 URI 的 $value:</span><span class="sxs-lookup"><span data-stu-id="348d8-162">To get the raw value of the property, append $value to the URI:</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample20.cmd)]

<span data-ttu-id="348d8-163">以下是回應。</span><span class="sxs-lookup"><span data-stu-id="348d8-163">Here is the response.</span></span> <span data-ttu-id="348d8-164">請注意，內容類型"text/plain"不是 JSON。</span><span class="sxs-lookup"><span data-stu-id="348d8-164">Notice that the content type is "text/plain", not JSON.</span></span>

[!code-console[Main](using-select-expand-and-value/samples/sample21.cmd)]

<span data-ttu-id="348d8-165">若要支援這些查詢 OData 控制器中，新增名為`GetProperty`，其中`Property`是屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="348d8-165">To support these queries in your OData controller, add a method named `GetProperty`, where `Property` is the name of the property.</span></span> <span data-ttu-id="348d8-166">比方說，要取得 Name 屬性的方法就會命名為`GetName`。</span><span class="sxs-lookup"><span data-stu-id="348d8-166">For example, the method to get the Name property would be named `GetName`.</span></span> <span data-ttu-id="348d8-167">這個方法應傳回該屬性的值：</span><span class="sxs-lookup"><span data-stu-id="348d8-167">The method should return the value of that property:</span></span>

[!code-csharp[Main](using-select-expand-and-value/samples/sample22.cs)]
