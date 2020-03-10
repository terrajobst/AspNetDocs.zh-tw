---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
title: 使用 Web API 2 支援 OData v3 中的實體關聯 |Microsoft Docs
author: MikeWasson
description: 大部分的資料集會定義實體之間的關聯性：客戶具有訂單;書籍有作者;產品有供應商。 使用 OData 時，用戶端可以流覽 。
ms.author: riande
ms.date: 02/26/2014
ms.assetid: 1e4c2eb4-b6cf-42ff-8a65-4d71ddca0394
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/working-with-entity-relations
msc.type: authoredcontent
ms.openlocfilehash: 726a7d51123805e05f6831ef9cd7eaa84b6c44bd
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598739"
---
# <a name="supporting-entity-relations-in-odata-v3-with-web-api-2"></a><span data-ttu-id="58978-104">使用 Web API 2 支援 OData v3 中的實體關聯</span><span class="sxs-lookup"><span data-stu-id="58978-104">Supporting Entity Relations in OData v3 with Web API 2</span></span>

<span data-ttu-id="58978-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="58978-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="58978-106">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="58978-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="58978-107">大部分的資料集會定義實體之間的關聯性：客戶具有訂單;書籍有作者;產品有供應商。</span><span class="sxs-lookup"><span data-stu-id="58978-107">Most data sets define relations between entities: Customers have orders; books have authors; products have suppliers.</span></span> <span data-ttu-id="58978-108">使用 OData 時，用戶端可以流覽實體關聯。</span><span class="sxs-lookup"><span data-stu-id="58978-108">Using OData, clients can navigate over entity relations.</span></span> <span data-ttu-id="58978-109">提供產品之後，您就可以找到供應商。</span><span class="sxs-lookup"><span data-stu-id="58978-109">Given a product, you can find the supplier.</span></span> <span data-ttu-id="58978-110">您也可以建立或移除關聯性。</span><span class="sxs-lookup"><span data-stu-id="58978-110">You can also create or remove relationships.</span></span> <span data-ttu-id="58978-111">例如，您可以設定產品的供應商。</span><span class="sxs-lookup"><span data-stu-id="58978-111">For example, you can set the supplier for a product.</span></span>
> 
> <span data-ttu-id="58978-112">本教學課程說明如何在 ASP.NET Web API 中支援這些作業。</span><span class="sxs-lookup"><span data-stu-id="58978-112">This tutorial shows how to support these operations in ASP.NET Web API.</span></span> <span data-ttu-id="58978-113">本教學課程是[以使用 WEB API 2 建立 OData V3 端點](creating-an-odata-endpoint.md)教學課程為基礎。</span><span class="sxs-lookup"><span data-stu-id="58978-113">The tutorial builds on the tutorial [Creating an OData v3 Endpoint with Web API 2](creating-an-odata-endpoint.md).</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="58978-114">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="58978-114">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="58978-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="58978-115">Web API 2</span></span>
> - <span data-ttu-id="58978-116">OData 第3版</span><span class="sxs-lookup"><span data-stu-id="58978-116">OData Version 3</span></span>
> - <span data-ttu-id="58978-117">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="58978-117">Entity Framework 6</span></span>

## <a name="add-a-supplier-entity"></a><span data-ttu-id="58978-118">新增供應商實體</span><span class="sxs-lookup"><span data-stu-id="58978-118">Add a Supplier Entity</span></span>

<span data-ttu-id="58978-119">首先，我們需要將新的實體類型新增至我們的 OData 摘要。</span><span class="sxs-lookup"><span data-stu-id="58978-119">First we need to add a new entity type to our OData feed.</span></span> <span data-ttu-id="58978-120">我們會新增 `Supplier` 類別。</span><span class="sxs-lookup"><span data-stu-id="58978-120">We'll add a `Supplier` class.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample1.cs)]

<span data-ttu-id="58978-121">此類別使用實體索引鍵的字串。</span><span class="sxs-lookup"><span data-stu-id="58978-121">This class uses a string for the entity key.</span></span> <span data-ttu-id="58978-122">實際上，這可能比使用整數索引鍵少。</span><span class="sxs-lookup"><span data-stu-id="58978-122">In practice, that might be less common than using an integer key.</span></span> <span data-ttu-id="58978-123">但是，值得一提的是，OData 如何處理其他金鑰類型，但整數除外。</span><span class="sxs-lookup"><span data-stu-id="58978-123">But it's worth seeing how OData handles other key types besides integers.</span></span>

<span data-ttu-id="58978-124">接下來，我們將藉由將 `Supplier` 屬性新增至 `Product` 類別來建立關聯性：</span><span class="sxs-lookup"><span data-stu-id="58978-124">Next, we'll create a relation by adding a `Supplier` property to the `Product` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample2.cs)]

<span data-ttu-id="58978-125">將新的**DbSet**加入 `ProductServiceContext` 類別，使 Entity Framework 將在資料庫中包含 `Supplier` 資料表。</span><span class="sxs-lookup"><span data-stu-id="58978-125">Add a new **DbSet** to the `ProductServiceContext` class, so that Entity Framework will include the `Supplier` table in the database.</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample3.cs?highlight=9)]

<span data-ttu-id="58978-126">在 WebApiConfig.cs 中，將「供應商」實體新增至 EDM 模型：</span><span class="sxs-lookup"><span data-stu-id="58978-126">In WebApiConfig.cs, add a "Suppliers" entity to the EDM model:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample4.cs?highlight=4)]

## <a name="navigation-properties"></a><span data-ttu-id="58978-127">導覽屬性</span><span class="sxs-lookup"><span data-stu-id="58978-127">Navigation Properties</span></span>

<span data-ttu-id="58978-128">若要取得產品的供應商，用戶端會傳送 GET 要求：</span><span class="sxs-lookup"><span data-stu-id="58978-128">To get the supplier for a product, the client sends a GET request:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample5.cmd)]

<span data-ttu-id="58978-129">這裡的「供應商」是 `Product` 類型的導覽屬性。</span><span class="sxs-lookup"><span data-stu-id="58978-129">Here "Supplier" is a navigation property on the `Product` type.</span></span> <span data-ttu-id="58978-130">在此情況下，`Supplier` 指的是單一專案，但導覽屬性也可以傳回集合（一對多或多對多關聯性）。</span><span class="sxs-lookup"><span data-stu-id="58978-130">In this case, `Supplier` refers to a single item, but a navigation property can also return a collection (one-to-many or many-to-many relation).</span></span>

<span data-ttu-id="58978-131">若要支援此要求，請將下列方法新增至 `ProductsController` 類別：</span><span class="sxs-lookup"><span data-stu-id="58978-131">To support this request, add the following method to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample6.cs)]

<span data-ttu-id="58978-132">*金鑰*參數是產品的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="58978-132">The *key* parameter is the key of the product.</span></span> <span data-ttu-id="58978-133">此方法會傳回相關實體&#8212;，在此案例中為 `Supplier` 實例。</span><span class="sxs-lookup"><span data-stu-id="58978-133">The method returns the related entity&#8212;in this case, a `Supplier` instance.</span></span> <span data-ttu-id="58978-134">方法名稱和參數名稱都很重要。</span><span class="sxs-lookup"><span data-stu-id="58978-134">The method name and parameter name are both important.</span></span> <span data-ttu-id="58978-135">一般而言，如果導覽屬性的名稱為 "X"，您就必須加入名為 "GetX" 的方法。</span><span class="sxs-lookup"><span data-stu-id="58978-135">In general, if the navigation property is named "X", you need to add a method named "GetX".</span></span> <span data-ttu-id="58978-136">此方法必須採用名為 "*key*" 的參數，以符合父系索引鍵的資料類型。</span><span class="sxs-lookup"><span data-stu-id="58978-136">The method must take a parameter named "*key*" that matches the data type of the parent's key.</span></span>

<span data-ttu-id="58978-137">此外，在*key*參數中包含 **[FromOdataUri]** 屬性也很重要。</span><span class="sxs-lookup"><span data-stu-id="58978-137">It is also important to include the **[FromOdataUri]** attribute in the *key* parameter.</span></span> <span data-ttu-id="58978-138">這個屬性會告知 Web API 在從要求 URI 剖析金鑰時，使用 OData 語法規則。</span><span class="sxs-lookup"><span data-stu-id="58978-138">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

## <a name="creating-and-deleting-links"></a><span data-ttu-id="58978-139">建立和刪除連結</span><span class="sxs-lookup"><span data-stu-id="58978-139">Creating and Deleting Links</span></span>

<span data-ttu-id="58978-140">OData 支援建立或移除兩個實體之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="58978-140">OData supports creating or removing relationships between two entities.</span></span> <span data-ttu-id="58978-141">在 OData 術語中，關聯性是「連結」。</span><span class="sxs-lookup"><span data-stu-id="58978-141">In OData terminology, the relationship is a "link."</span></span> <span data-ttu-id="58978-142">每個連結都有一個具有*entity*/$links/*實體*格式的 URI。</span><span class="sxs-lookup"><span data-stu-id="58978-142">Each link has a URI with the form *entity*/$links/*entity*.</span></span> <span data-ttu-id="58978-143">例如，從產品到供應商的連結看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="58978-143">For example, the link from product to supplier looks like this:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample7.cmd)]

<span data-ttu-id="58978-144">若要建立新的連結，用戶端會將 POST 要求傳送至連結 URI。</span><span class="sxs-lookup"><span data-stu-id="58978-144">To create a new link, the client sends a POST request to the link URI.</span></span> <span data-ttu-id="58978-145">要求的主體是目標實體的 URI。</span><span class="sxs-lookup"><span data-stu-id="58978-145">The body of the request is the URI of the target entity.</span></span> <span data-ttu-id="58978-146">例如，假設有一個具有索引鍵 "CTSO" 的供應商。</span><span class="sxs-lookup"><span data-stu-id="58978-146">For example, suppose there is a supplier with the key "CTSO".</span></span> <span data-ttu-id="58978-147">若要建立從「產品（1）」到「供應商（' CTSO '）」的連結，用戶端會傳送如下所示的要求：</span><span class="sxs-lookup"><span data-stu-id="58978-147">To create a link from "Product(1)" to "Supplier('CTSO')", the client sends a request like the following:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample8.cmd)]

<span data-ttu-id="58978-148">若要刪除連結，用戶端會將刪除要求傳送至連結 URI。</span><span class="sxs-lookup"><span data-stu-id="58978-148">To delete a link, the client sends a DELETE request to the link URI.</span></span>

<span data-ttu-id="58978-149">**建立連結**</span><span class="sxs-lookup"><span data-stu-id="58978-149">**Creating Links**</span></span>

<span data-ttu-id="58978-150">若要讓用戶端建立產品供應商連結，請將下列程式碼新增至 `ProductsController` 類別：</span><span class="sxs-lookup"><span data-stu-id="58978-150">To enable a client to create product-supplier links, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample9.cs)]

<span data-ttu-id="58978-151">此方法採用三個參數：</span><span class="sxs-lookup"><span data-stu-id="58978-151">This method takes three parameters:</span></span>

- <span data-ttu-id="58978-152">*金鑰*：父實體的金鑰（產品）</span><span class="sxs-lookup"><span data-stu-id="58978-152">*key*: The key to the parent entity (the product)</span></span>
- <span data-ttu-id="58978-153">*navigationProperty*：導覽屬性的名稱。</span><span class="sxs-lookup"><span data-stu-id="58978-153">*navigationProperty*: The name of the navigation property.</span></span> <span data-ttu-id="58978-154">在此範例中，唯一有效的導覽屬性是「供應商」。</span><span class="sxs-lookup"><span data-stu-id="58978-154">In this example, the only valid navigation property is "Supplier".</span></span>
- <span data-ttu-id="58978-155">*連結*：相關實體的 OData URI。</span><span class="sxs-lookup"><span data-stu-id="58978-155">*link*: The OData URI of the related entity.</span></span> <span data-ttu-id="58978-156">此值取自要求主體。</span><span class="sxs-lookup"><span data-stu-id="58978-156">This value is taken from the request body.</span></span> <span data-ttu-id="58978-157">例如，連結 URI 可能是 "`http://localhost/odata/Suppliers('CTSO')`，表示識別碼 = ' CTSO ' 的供應商。</span><span class="sxs-lookup"><span data-stu-id="58978-157">For example, the link URI might be "`http://localhost/odata/Suppliers('CTSO')`, meaning the supplier with ID = ‘CTSO'.</span></span>

<span data-ttu-id="58978-158">方法會使用連結來查閱供應商。</span><span class="sxs-lookup"><span data-stu-id="58978-158">The method uses the link to look up the supplier.</span></span> <span data-ttu-id="58978-159">如果找到相符的供應商，方法會設定 `Product.Supplier` 屬性，並將結果儲存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="58978-159">If the matching supplier is found, the method sets the `Product.Supplier` property and saves the result to the database.</span></span>

<span data-ttu-id="58978-160">最困難的部分是剖析連結 URI。</span><span class="sxs-lookup"><span data-stu-id="58978-160">The hardest part is parsing the link URI.</span></span> <span data-ttu-id="58978-161">基本上，您需要模擬將 GET 要求傳送至該 URI 的結果。</span><span class="sxs-lookup"><span data-stu-id="58978-161">Basically, you need to simulate the result of sending a GET request to that URI.</span></span> <span data-ttu-id="58978-162">下列 helper 方法說明如何執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="58978-162">The following helper method shows how to do this.</span></span> <span data-ttu-id="58978-163">方法會叫用 Web API 路由進程，並取得代表已剖析 OData 路徑的**ODataPath**實例。</span><span class="sxs-lookup"><span data-stu-id="58978-163">The method invokes the Web API routing process and gets back an **ODataPath** instance that represents the parsed OData path.</span></span> <span data-ttu-id="58978-164">若為連結 URI，其中一個區段應該是實體索引鍵。</span><span class="sxs-lookup"><span data-stu-id="58978-164">For a link URI, one of the segments should be the entity key.</span></span> <span data-ttu-id="58978-165">（如果不是，用戶端傳送了錯誤的 URI）。</span><span class="sxs-lookup"><span data-stu-id="58978-165">(If not, the client sent a bad URI.)</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample10.cs)]

<span data-ttu-id="58978-166">**刪除連結**</span><span class="sxs-lookup"><span data-stu-id="58978-166">**Deleting Links**</span></span>

<span data-ttu-id="58978-167">若要刪除連結，請將下列程式碼新增至 `ProductsController` 類別：</span><span class="sxs-lookup"><span data-stu-id="58978-167">To delete a link, add the following code to the `ProductsController` class:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample11.cs)]

<span data-ttu-id="58978-168">在此範例中，導覽屬性是單一 `Supplier` 實體。</span><span class="sxs-lookup"><span data-stu-id="58978-168">In this example, the navigation property is a single `Supplier` entity.</span></span> <span data-ttu-id="58978-169">如果導覽屬性是集合，則要刪除連結的 URI 必須包含相關實體的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="58978-169">If the navigation property is a collection, the URI to delete a link must include a key for the related entity.</span></span> <span data-ttu-id="58978-170">例如:</span><span class="sxs-lookup"><span data-stu-id="58978-170">For example:</span></span>

[!code-console[Main](working-with-entity-relations/samples/sample12.cmd)]

<span data-ttu-id="58978-171">此要求會移除客戶1的訂單1。</span><span class="sxs-lookup"><span data-stu-id="58978-171">This request removes order 1 from customer 1.</span></span> <span data-ttu-id="58978-172">在此情況下，DeleteLink 方法會具有下列簽章：</span><span class="sxs-lookup"><span data-stu-id="58978-172">In this case, the DeleteLink method will have the following signature:</span></span>

[!code-csharp[Main](working-with-entity-relations/samples/sample13.cs)]

<span data-ttu-id="58978-173">*RelatedKey*參數會提供相關實體的索引鍵。</span><span class="sxs-lookup"><span data-stu-id="58978-173">The *relatedKey* parameter gives the key for the related entity.</span></span> <span data-ttu-id="58978-174">因此，在您的 `DeleteLink` 方法中，請依索引*鍵*參數查閱主要實體、依*relatedKey*參數尋找相關實體，然後移除關聯。</span><span class="sxs-lookup"><span data-stu-id="58978-174">So in your `DeleteLink` method, look up the primary entity by the *key* parameter, find the related entity by the *relatedKey* parameter, and then remove the association.</span></span> <span data-ttu-id="58978-175">根據您的資料模型，您可能需要同時執行這兩個版本的 `DeleteLink`。</span><span class="sxs-lookup"><span data-stu-id="58978-175">Depending on your data model, you might need to implement both versions of `DeleteLink`.</span></span> <span data-ttu-id="58978-176">Web API 會根據要求 URI 來呼叫正確的版本。</span><span class="sxs-lookup"><span data-stu-id="58978-176">Web API will call the correct version based on the request URI.</span></span>
