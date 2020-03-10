---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
title: 使用 ASP.NET Web API 2.2 的 OData v4 中的實體關聯 |Microsoft Docs
author: MikeWasson
description: 大部分的資料集會定義實體之間的關聯性：客戶具有訂單;書籍有作者;產品有供應商。 使用 OData 時，用戶端可以流覽 。
ms.author: riande
ms.date: 06/26/2014
ms.assetid: 72657550-ec09-4779-9bfc-2fb15ecd51c7
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v4/entity-relations-in-odata-v4
msc.type: authoredcontent
ms.openlocfilehash: fbafb2b2346689271905db5790cdddeeb809b070
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598690"
---
# <a name="entity-relations-in-odata-v4-using-aspnet-web-api-22"></a><span data-ttu-id="c0bba-104">使用 ASP.NET Web API 2.2 的 OData v4 中的實體關聯</span><span class="sxs-lookup"><span data-stu-id="c0bba-104">Entity Relations in OData v4 Using ASP.NET Web API 2.2</span></span>

<span data-ttu-id="c0bba-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="c0bba-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

> <span data-ttu-id="c0bba-106">大部分的資料集會定義實體之間的關聯性：客戶具有訂單;書籍有作者;產品有供應商。</span><span class="sxs-lookup"><span data-stu-id="c0bba-106">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="c0bba-107">使用 OData 時，用戶端可以流覽實體關聯。</span><span class="sxs-lookup"><span data-stu-id="c0bba-107">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="c0bba-108">提供產品之後，您就可以找到供應商。</span><span class="sxs-lookup"><span data-stu-id="c0bba-108">Given a product, you can find the supplier.</span></span> <span data-ttu-id="c0bba-109">您也可以建立或移除關聯性。</span><span class="sxs-lookup"><span data-stu-id="c0bba-109">You can also create or remove relationships.</span></span> <span data-ttu-id="c0bba-110">例如，您可以設定產品的供應商。</span><span class="sxs-lookup"><span data-stu-id="c0bba-110">For example, you can set the supplier for a product.</span></span>
>
> <span data-ttu-id="c0bba-111">本教學課程說明如何使用 ASP.NET Web API 在 OData v4 中支援這些作業。</span><span class="sxs-lookup"><span data-stu-id="c0bba-111">This tutorial shows how to support these operations in OData v4 using ASP.NET Web API.</span></span> <span data-ttu-id="c0bba-112">本教學課程是[以使用 ASP.NET Web API 2 建立 OData V4 端點](create-an-odata-v4-endpoint.md)教學課程為基礎。</span><span class="sxs-lookup"><span data-stu-id="c0bba-112">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>
>
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="c0bba-113">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="c0bba-113">Software versions used in the tutorial</span></span>
>
> - <span data-ttu-id="c0bba-114">Web API 2。1</span><span class="sxs-lookup"><span data-stu-id="c0bba-114">Web API 2.1</span></span>
> - <span data-ttu-id="c0bba-115">OData v4</span><span class="sxs-lookup"><span data-stu-id="c0bba-115">OData v4</span></span>
> - <span data-ttu-id="c0bba-116">Visual Studio 2013 （[在此](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)下載 Visual Studio 2017）</span><span class="sxs-lookup"><span data-stu-id="c0bba-116">Visual Studio 2013 (download Visual Studio 2017 [here](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017))</span></span>
> - <span data-ttu-id="c0bba-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="c0bba-117">Entity Framework 6</span></span>
> - <span data-ttu-id="c0bba-118">.NET 4.5</span><span class="sxs-lookup"><span data-stu-id="c0bba-118">.NET 4.5</span></span>
>
> ## <a name="tutorial-versions"></a><span data-ttu-id="c0bba-119">教學課程版本</span><span class="sxs-lookup"><span data-stu-id="c0bba-119">Tutorial versions</span></span>
>
> <span data-ttu-id="c0bba-120">針對 OData 第3版，請參閱[支援 odata v3 中的實體](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations)關聯。</span><span class="sxs-lookup"><span data-stu-id="c0bba-120">For the OData Version 3, see [Supporting Entity Relations in OData v3](https://asp.net/web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations).</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="c0bba-121">新增供應商實體</span><span class="sxs-lookup"><span data-stu-id="c0bba-121">Add a Supplier Entity</span></span>

> [!NOTE]
> <span data-ttu-id="c0bba-122">本教學課程是[以使用 ASP.NET Web API 2 建立 OData V4 端點](create-an-odata-v4-endpoint.md)教學課程為基礎。</span><span class="sxs-lookup"><span data-stu-id="c0bba-122">The tutorial builds on the tutorial [Create an OData v4 Endpoint Using ASP.NET Web API 2](create-an-odata-v4-endpoint.md).</span></span>

<span data-ttu-id="c0bba-123">首先，我們需要相關的實體。</span><span class="sxs-lookup"><span data-stu-id="c0bba-123">First, we need a related entity.</span></span> <span data-ttu-id="c0bba-124">在 [模型] 資料夾中，新增名為 `Supplier` 的類別。</span><span class="sxs-lookup"><span data-stu-id="c0bba-124">Add a class named `Supplier` in the Models folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample1.cs)]

<span data-ttu-id="c0bba-125">將導覽屬性新增至 `Product` 類別：</span><span class="sxs-lookup"><span data-stu-id="c0bba-125">Add a navigation property to the `Product` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample2.cs?highlight=13-15)]

<span data-ttu-id="c0bba-126">將新的**DbSet**加入 `ProductsContext` 類別，使 Entity Framework 將在資料庫中包含供應商資料表。</span><span class="sxs-lookup"><span data-stu-id="c0bba-126">Add a new **DbSet** to the `ProductsContext` class, so that Entity Framework will include the Supplier table in the database.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample3.cs?highlight=10)]

<span data-ttu-id="c0bba-127">在 WebApiConfig.cs 中，將 &quot;供應商&quot; 實體集新增至實體資料模型：</span><span class="sxs-lookup"><span data-stu-id="c0bba-127">In WebApiConfig.cs, add a &quot;Suppliers&quot; entity set to the entity data model:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample4.cs?highlight=6)]

## <a name="add-a-suppliers-controller"></a><span data-ttu-id="c0bba-128">新增供應商控制器</span><span class="sxs-lookup"><span data-stu-id="c0bba-128">Add a Suppliers Controller</span></span>

<span data-ttu-id="c0bba-129">將 `SuppliersController` 類別新增至 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="c0bba-129">Add a `SuppliersController` class to the Controllers folder.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample5.cs)]

<span data-ttu-id="c0bba-130">我不會示範如何新增此控制器的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="c0bba-130">I won't show how to add CRUD operations for this controller.</span></span> <span data-ttu-id="c0bba-131">這些步驟與產品控制器相同（請參閱[建立 OData V4 端點](create-an-odata-v4-endpoint.md)）。</span><span class="sxs-lookup"><span data-stu-id="c0bba-131">The steps are the same as for the Products controller (see [Create an OData v4 Endpoint](create-an-odata-v4-endpoint.md)).</span></span>

## <a name="getting-related-entities"></a><span data-ttu-id="c0bba-132">取得相關實體</span><span class="sxs-lookup"><span data-stu-id="c0bba-132">Getting Related Entities</span></span>

<span data-ttu-id="c0bba-133">若要取得產品的供應商，用戶端會傳送 GET 要求：</span><span class="sxs-lookup"><span data-stu-id="c0bba-133">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample6.cmd)]

<span data-ttu-id="c0bba-134">若要支援此要求，請將下列方法新增至 `ProductsController` 類別：</span><span class="sxs-lookup"><span data-stu-id="c0bba-134">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample7.cs)]

<span data-ttu-id="c0bba-135">這個方法會使用預設的命名慣例</span><span class="sxs-lookup"><span data-stu-id="c0bba-135">This method uses a default naming convention</span></span>

- <span data-ttu-id="c0bba-136">方法名稱： GetX，其中 X 是導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="c0bba-136">Method name: GetX, where X is the navigation property.</span></span>
- <span data-ttu-id="c0bba-137">參數名稱：*金鑰*</span><span class="sxs-lookup"><span data-stu-id="c0bba-137">Parameter name: *key*</span></span>

<span data-ttu-id="c0bba-138">如果您遵循此命名慣例，Web API 會自動將 HTTP 要求對應至控制器方法。</span><span class="sxs-lookup"><span data-stu-id="c0bba-138">If you follow this naming convention, Web API automatically maps the HTTP request to the controller method.</span></span>

<span data-ttu-id="c0bba-139">範例 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="c0bba-139">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample8.cmd)]

<span data-ttu-id="c0bba-140">範例 HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="c0bba-140">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample9.cmd)]

### <a name="getting-a-related-collection"></a><span data-ttu-id="c0bba-141">取得相關集合</span><span class="sxs-lookup"><span data-stu-id="c0bba-141">Getting a related collection</span></span>

<span data-ttu-id="c0bba-142">在上述範例中，產品有一個供應商。</span><span class="sxs-lookup"><span data-stu-id="c0bba-142">In the previous example, a product has one supplier.</span></span> <span data-ttu-id="c0bba-143">導覽屬性也可以傳回集合。</span><span class="sxs-lookup"><span data-stu-id="c0bba-143">A navigation property can also return a collection.</span></span> <span data-ttu-id="c0bba-144">下列程式碼會取得供應商的產品：</span><span class="sxs-lookup"><span data-stu-id="c0bba-144">The following code gets the products for a supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample10.cs)]

<span data-ttu-id="c0bba-145">在此情況下，方法會傳回**IQueryable** ，而不是**SingleResult&lt;t&gt;**</span><span class="sxs-lookup"><span data-stu-id="c0bba-145">In this case, the method returns an **IQueryable** instead of a **SingleResult&lt;T&gt;**</span></span>

<span data-ttu-id="c0bba-146">範例 HTTP 要求：</span><span class="sxs-lookup"><span data-stu-id="c0bba-146">Example HTTP request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample11.cmd)]

<span data-ttu-id="c0bba-147">範例 HTTP 回應：</span><span class="sxs-lookup"><span data-stu-id="c0bba-147">Example HTTP response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample12.cmd)]

## <a name="creating-a-relationship-between-entities"></a><span data-ttu-id="c0bba-148">建立實體之間的關聯性</span><span class="sxs-lookup"><span data-stu-id="c0bba-148">Creating a Relationship Between Entities</span></span>

<span data-ttu-id="c0bba-149">OData 支援建立或移除兩個現有實體之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="c0bba-149">OData supports creating or removing relationships between two existing entities.</span></span> <span data-ttu-id="c0bba-150">在 OData v4 術語中，關聯性是 &quot;的參考&quot;。</span><span class="sxs-lookup"><span data-stu-id="c0bba-150">In OData v4 terminology, the relationship is a &quot;reference&quot;.</span></span> <span data-ttu-id="c0bba-151">（在 OData v3 中，關聯性稱為「*連結*」。</span><span class="sxs-lookup"><span data-stu-id="c0bba-151">(In OData v3, the relationship was called a *link*.</span></span> <span data-ttu-id="c0bba-152">此教學課程的通訊協定差異並不重要）。</span><span class="sxs-lookup"><span data-stu-id="c0bba-152">The protocol differences don't matter for this tutorial.)</span></span>

<span data-ttu-id="c0bba-153">參考有自己的 URI，格式為 `/Entity/NavigationProperty/$ref`。</span><span class="sxs-lookup"><span data-stu-id="c0bba-153">A reference has its own URI, with the form `/Entity/NavigationProperty/$ref`.</span></span> <span data-ttu-id="c0bba-154">例如，以下是用來處理產品和其供應商之間參考的 URI：</span><span class="sxs-lookup"><span data-stu-id="c0bba-154">For example, here is the URI to address the reference between a product and its supplier:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample13.cmd)]

<span data-ttu-id="c0bba-155">若要加入關聯性，用戶端會將 POST 或 PUT 要求傳送至這個位址。</span><span class="sxs-lookup"><span data-stu-id="c0bba-155">To add a relationship, the client sends a POST or PUT request to this address.</span></span>

- <span data-ttu-id="c0bba-156">如果導覽屬性是單一實體（例如 `Product.Supplier`），則 PUT。</span><span class="sxs-lookup"><span data-stu-id="c0bba-156">PUT if the navigation property is a single entity, such as `Product.Supplier`.</span></span>
- <span data-ttu-id="c0bba-157">如果導覽屬性是集合（例如 `Supplier.Products`），則為 POST。</span><span class="sxs-lookup"><span data-stu-id="c0bba-157">POST if the navigation property is a collection, such as `Supplier.Products`.</span></span>

<span data-ttu-id="c0bba-158">要求的主體包含關聯性中其他實體的 URI。</span><span class="sxs-lookup"><span data-stu-id="c0bba-158">The body of the request contains the URI of the other entity in the relation.</span></span> <span data-ttu-id="c0bba-159">以下是範例要求：</span><span class="sxs-lookup"><span data-stu-id="c0bba-159">Here is an example request:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample14.cmd)]

<span data-ttu-id="c0bba-160">在此範例中，用戶端會將 PUT 要求傳送至 `/Products(6)/Supplier/$ref`，這是識別碼 = 6 之產品 `Supplier` 的 $ref URI。</span><span class="sxs-lookup"><span data-stu-id="c0bba-160">In this example, the client sends a PUT request to `/Products(6)/Supplier/$ref`, which is the $ref URI for the `Supplier` of the product with ID = 6.</span></span> <span data-ttu-id="c0bba-161">如果要求成功，伺服器會傳送204（沒有內容）回應：</span><span class="sxs-lookup"><span data-stu-id="c0bba-161">If the request succeeds, the server sends a 204 (No Content) response:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample15.cmd)]

<span data-ttu-id="c0bba-162">以下是將關聯性新增至 `Product`的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="c0bba-162">Here is the controller method to add a relationship to a `Product`:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample16.cs)]

<span data-ttu-id="c0bba-163">*NavigationProperty*參數會指定要設定的關聯性。</span><span class="sxs-lookup"><span data-stu-id="c0bba-163">The *navigationProperty* parameter specifies which relationship to set.</span></span> <span data-ttu-id="c0bba-164">（如果實體上有一個以上的導覽屬性，您可以加入更多 `case` 語句）。</span><span class="sxs-lookup"><span data-stu-id="c0bba-164">(If there is more than one navigation property on the entity, you can add more `case` statements.)</span></span>

<span data-ttu-id="c0bba-165">*連結*參數包含供應商的 URI。</span><span class="sxs-lookup"><span data-stu-id="c0bba-165">The *link* parameter contains the URI of the supplier.</span></span> <span data-ttu-id="c0bba-166">Web API 會自動剖析要求主體，以取得此參數的值。</span><span class="sxs-lookup"><span data-stu-id="c0bba-166">Web API automatically parses the request body to get the value for this parameter.</span></span>

<span data-ttu-id="c0bba-167">若要查閱供應商，我們需要識別碼（或金鑰），這是*連結*參數的一部分。</span><span class="sxs-lookup"><span data-stu-id="c0bba-167">To look up the supplier, we need the ID (or key), which is part of the *link* parameter.</span></span> <span data-ttu-id="c0bba-168">若要這麼做，請使用下列 helper 方法：</span><span class="sxs-lookup"><span data-stu-id="c0bba-168">To do this, use the following helper method:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample17.cs)]

<span data-ttu-id="c0bba-169">基本上，這個方法會使用 OData 程式庫，將 URI 路徑分割成區段，找出包含索引鍵的區段，然後將索引鍵轉換成正確的型別。</span><span class="sxs-lookup"><span data-stu-id="c0bba-169">Basically, this method uses the OData library to split the URI path into segments, find the segment that contains the key, and convert the key into the correct type.</span></span>

## <a name="deleting-a-relationship-between-entities"></a><span data-ttu-id="c0bba-170">刪除實體之間的關聯性</span><span class="sxs-lookup"><span data-stu-id="c0bba-170">Deleting a Relationship Between Entities</span></span>

<span data-ttu-id="c0bba-171">若要刪除關聯性，用戶端會將 HTTP DELETE 要求傳送至 $ref URI：</span><span class="sxs-lookup"><span data-stu-id="c0bba-171">To delete a relationship, the client sends an HTTP DELETE request to the $ref URI:</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample18.cmd)]

<span data-ttu-id="c0bba-172">以下是用來刪除產品與供應商之間關聯性的控制器方法：</span><span class="sxs-lookup"><span data-stu-id="c0bba-172">Here is the controller method to delete the relationship between a Product and a Supplier:</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample19.cs)]

<span data-ttu-id="c0bba-173">在此情況下，`Product.Supplier` 是一對多關聯的 &quot;1&quot; 端，因此您只需將 `Product.Supplier` 設定為 [`null`]，即可移除關聯性。</span><span class="sxs-lookup"><span data-stu-id="c0bba-173">In this case, `Product.Supplier` is the &quot;1&quot; end of a 1-to-many relation, so you can remove the relationship just by setting `Product.Supplier` to `null`.</span></span>

<span data-ttu-id="c0bba-174">在 &quot;關聯性的許多&quot; 端，用戶端必須指定要移除的相關實體。</span><span class="sxs-lookup"><span data-stu-id="c0bba-174">In the &quot;many&quot; end of a relationship, the client must specify which related entity to remove.</span></span> <span data-ttu-id="c0bba-175">若要這樣做，用戶端會在要求的查詢字串中傳送相關實體的 URI。</span><span class="sxs-lookup"><span data-stu-id="c0bba-175">To do so, the client sends the URI of the related entity in the query string of the request.</span></span> <span data-ttu-id="c0bba-176">例如，若要從「供應商1」移除「產品1」：</span><span class="sxs-lookup"><span data-stu-id="c0bba-176">For example, to remove "Product 1" from "Supplier 1":</span></span>

[!code-console[Main](entity-relations-in-odata-v4/samples/sample20.cmd?highlight=1)]

<span data-ttu-id="c0bba-177">若要在 Web API 中支援這項功能，我們必須在 `DeleteRef` 方法中包含額外的參數。</span><span class="sxs-lookup"><span data-stu-id="c0bba-177">To support this in Web API, we need to include an extra parameter in the `DeleteRef` method.</span></span> <span data-ttu-id="c0bba-178">以下是從 `Supplier.Products` 關聯移除產品的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="c0bba-178">Here is the controller method to remove a product from the `Supplier.Products` relation.</span></span>

[!code-csharp[Main](entity-relations-in-odata-v4/samples/sample21.cs)]

<span data-ttu-id="c0bba-179">*金鑰*參數是供應商的金鑰，而*relatedKey*參數則是要從 `Products` 關聯性中移除之產品的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="c0bba-179">The *key* parameter is the key for the supplier, and the *relatedKey* parameter is the key for the product to remove from the `Products` relationship.</span></span> <span data-ttu-id="c0bba-180">請注意，Web API 會自動從查詢字串取得金鑰。</span><span class="sxs-lookup"><span data-stu-id="c0bba-180">Note that Web API automatically gets the key from the query string.</span></span>
