---
uid: web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
title: 在 ASP.NET Web API 2 中支援 OData 動作 |Microsoft Docs
author: MikeWasson
description: 在 OData 中，動作是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。 動作的某些用途包括： [執行]
ms.author: riande
ms.date: 02/25/2014
ms.assetid: 2d7b3aa2-aa47-4e6e-b0ce-3d65a1c6fe02
msc.legacyurl: /web-api/overview/odata-support-in-aspnet-web-api/odata-v3/odata-actions
msc.type: authoredcontent
ms.openlocfilehash: ae8b23f0868f992cb2bbbf14ee3f7ac848501515
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556354"
---
# <a name="supporting-odata-actions-in-aspnet-web-api-2"></a><span data-ttu-id="e7798-104">在 ASP.NET Web API 2 中支援 OData 動作</span><span class="sxs-lookup"><span data-stu-id="e7798-104">Supporting OData Actions in ASP.NET Web API 2</span></span>

<span data-ttu-id="e7798-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="e7798-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="e7798-106">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="e7798-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASPNET-Web-API-OData-cecdb524)

> <span data-ttu-id="e7798-107">在 OData 中，*動作*是一種新增伺服器端行為的方法，不容易定義為實體上的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="e7798-107">In OData, *actions* are a way to add server-side behaviors that are not easily defined as CRUD operations on entities.</span></span> <span data-ttu-id="e7798-108">某些動作的用途包括：</span><span class="sxs-lookup"><span data-stu-id="e7798-108">Some uses for actions include:</span></span>
> 
> - <span data-ttu-id="e7798-109">執行複雜交易。</span><span class="sxs-lookup"><span data-stu-id="e7798-109">Implementing complex transactions.</span></span>
> - <span data-ttu-id="e7798-110">一次處理數個實體。</span><span class="sxs-lookup"><span data-stu-id="e7798-110">Manipulating several entities at once.</span></span>
> - <span data-ttu-id="e7798-111">僅允許更新實體的特定屬性。</span><span class="sxs-lookup"><span data-stu-id="e7798-111">Allowing updates only to certain properties of an entity.</span></span>
> - <span data-ttu-id="e7798-112">將資訊傳送至未定義于實體中的伺服器。</span><span class="sxs-lookup"><span data-stu-id="e7798-112">Sending information to the server that is not defined in an entity.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="e7798-113">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="e7798-113">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="e7798-114">Web API 2</span><span class="sxs-lookup"><span data-stu-id="e7798-114">Web API 2</span></span>
> - <span data-ttu-id="e7798-115">OData 第3版</span><span class="sxs-lookup"><span data-stu-id="e7798-115">OData Version 3</span></span>
> - <span data-ttu-id="e7798-116">Entity Framework 6</span><span class="sxs-lookup"><span data-stu-id="e7798-116">Entity Framework 6</span></span>

## <a name="example-rating-a-product"></a><span data-ttu-id="e7798-117">範例：評等產品</span><span class="sxs-lookup"><span data-stu-id="e7798-117">Example: Rating a Product</span></span>

<span data-ttu-id="e7798-118">在此範例中，我們想要讓使用者對產品進行評分，然後公開每個產品的平均評等。</span><span class="sxs-lookup"><span data-stu-id="e7798-118">In this example, we want to let users rate products, and then expose the average ratings for each product.</span></span> <span data-ttu-id="e7798-119">在資料庫上，我們將會儲存評等的清單，並將其加入產品中。</span><span class="sxs-lookup"><span data-stu-id="e7798-119">On the database, we will store a list of ratings, keyed to products.</span></span>

<span data-ttu-id="e7798-120">以下是我們可能用來代表 Entity Framework 中的評等的模型：</span><span class="sxs-lookup"><span data-stu-id="e7798-120">Here is the model we might use to represent the ratings in Entity Framework:</span></span>

[!code-csharp[Main](odata-actions/samples/sample1.cs)]

<span data-ttu-id="e7798-121">但是，我們不希望用戶端將 `ProductRating` 物件張貼到「評等」集合。</span><span class="sxs-lookup"><span data-stu-id="e7798-121">But we don't want clients to POST a `ProductRating` object to a "Ratings" collection.</span></span> <span data-ttu-id="e7798-122">就直覺而言，評等與 Products 集合相關聯，而且用戶端應該只需要公佈評等值。</span><span class="sxs-lookup"><span data-stu-id="e7798-122">Intuitively, the rating is associated with the Products collection, and the client should only need to post the rating value.</span></span>

<span data-ttu-id="e7798-123">因此，我們不會使用一般 CRUD 作業，而是定義用戶端可以在產品上叫用的動作。</span><span class="sxs-lookup"><span data-stu-id="e7798-123">Therefore, instead of using the normal CRUD operations, we define an action that a client can invoke on a Product.</span></span> <span data-ttu-id="e7798-124">在 OData 術語中，*動作會系*結至 Product 實體。</span><span class="sxs-lookup"><span data-stu-id="e7798-124">In OData terminology, the action is *bound* to Product entities.</span></span>

><span data-ttu-id="e7798-125">動作在伺服器上有副作用。</span><span class="sxs-lookup"><span data-stu-id="e7798-125">Actions have side-effects on the server.</span></span> <span data-ttu-id="e7798-126">基於這個理由，系統會使用 HTTP POST 要求來叫用它們。</span><span class="sxs-lookup"><span data-stu-id="e7798-126">For this reason, they are invoked using HTTP POST requests.</span></span> <span data-ttu-id="e7798-127">動作可以有參數和傳回型別，如服務中繼資料中所述。</span><span class="sxs-lookup"><span data-stu-id="e7798-127">Actions can have parameters and return types, which are described in the service metadata.</span></span> <span data-ttu-id="e7798-128">用戶端會在要求主體中傳送參數，而伺服器會在回應本文中傳送傳回值。</span><span class="sxs-lookup"><span data-stu-id="e7798-128">The client sends the parameters in the request body, and the server sends the return value in the response body.</span></span> <span data-ttu-id="e7798-129">為了叫用「速率產品」動作，用戶端會將 POST 傳送至 URI，如下所示：</span><span class="sxs-lookup"><span data-stu-id="e7798-129">To invoke the "Rate Product" action, the client sends a POST to a URI like the following:</span></span>

[!code-console[Main](odata-actions/samples/sample2.cmd)]

<span data-ttu-id="e7798-130">POST 要求中的資料只是產品分級：</span><span class="sxs-lookup"><span data-stu-id="e7798-130">The data in the POST request is simply the product rating:</span></span>

[!code-console[Main](odata-actions/samples/sample3.cmd)]

## <a name="declare-the-action-in-the-entity-data-model"></a><span data-ttu-id="e7798-131">在實體資料模型中宣告動作</span><span class="sxs-lookup"><span data-stu-id="e7798-131">Declare the Action in the Entity Data Model</span></span>

<span data-ttu-id="e7798-132">在您的 Web API 設定中，將動作新增至 entity data model （EDM）：</span><span class="sxs-lookup"><span data-stu-id="e7798-132">In your Web API configuration, add the action to the entity data model (EDM):</span></span>

[!code-csharp[Main](odata-actions/samples/sample4.cs)]

<span data-ttu-id="e7798-133">此程式碼會將 "RateProduct" 定義為可在產品實體上執行的動作。</span><span class="sxs-lookup"><span data-stu-id="e7798-133">This code defines "RateProduct" as an action that can be performed on Product entities.</span></span> <span data-ttu-id="e7798-134">它也會宣告動作接受名為「評等」的**int**參數，並傳回**int**值。</span><span class="sxs-lookup"><span data-stu-id="e7798-134">It also declares that the action takes an **int** parameter named "Rating", and returns an **int** value.</span></span>

## <a name="add-the-action-to-the-controller"></a><span data-ttu-id="e7798-135">將動作新增至控制器</span><span class="sxs-lookup"><span data-stu-id="e7798-135">Add the Action to the Controller</span></span>

<span data-ttu-id="e7798-136">"RateProduct" 動作會系結至 Product 實體。</span><span class="sxs-lookup"><span data-stu-id="e7798-136">The "RateProduct" action is bound to Product entities.</span></span> <span data-ttu-id="e7798-137">若要執行此動作，請將名為 `RateProduct` 的方法新增至 Products controller：</span><span class="sxs-lookup"><span data-stu-id="e7798-137">To implement the action, add a method named `RateProduct` to the Products controller:</span></span>

[!code-csharp[Main](odata-actions/samples/sample5.cs)]

<span data-ttu-id="e7798-138">請注意，方法名稱與 EDM 中的動作名稱相符。</span><span class="sxs-lookup"><span data-stu-id="e7798-138">Notice that the method name matches the name of the action in the EDM.</span></span> <span data-ttu-id="e7798-139">此方法有兩個參數：</span><span class="sxs-lookup"><span data-stu-id="e7798-139">The method has two parameters:</span></span>

- <span data-ttu-id="e7798-140">*金鑰*：要分級之產品的金鑰。</span><span class="sxs-lookup"><span data-stu-id="e7798-140">*key*: The key for the product to rate.</span></span>
- <span data-ttu-id="e7798-141">*parameters*：動作參數值的字典。</span><span class="sxs-lookup"><span data-stu-id="e7798-141">*parameters*: A dictionary of action parameter values.</span></span>

<span data-ttu-id="e7798-142">如果您使用預設路由慣例，則金鑰參數必須命名為 "key"。</span><span class="sxs-lookup"><span data-stu-id="e7798-142">If you are using the default routing conventions, the key parameter must be named "key".</span></span> <span data-ttu-id="e7798-143">也請務必包含 **[FromOdataUri]** 屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="e7798-143">It is also important to include the **[FromOdataUri]** attribute, as shown.</span></span> <span data-ttu-id="e7798-144">這個屬性會告知 Web API 在從要求 URI 剖析金鑰時，使用 OData 語法規則。</span><span class="sxs-lookup"><span data-stu-id="e7798-144">This attribute tells Web API to use OData syntax rules when it parses the key from the request URI.</span></span>

<span data-ttu-id="e7798-145">使用*parameters*字典來取得動作參數：</span><span class="sxs-lookup"><span data-stu-id="e7798-145">Use the *parameters* dictionary to get the action parameters:</span></span>

[!code-csharp[Main](odata-actions/samples/sample6.cs)]

<span data-ttu-id="e7798-146">如果用戶端以正確的格式傳送動作參數， **ModelState**的值就是 true。</span><span class="sxs-lookup"><span data-stu-id="e7798-146">If the client sends the action parameters in the correct format, the value of **ModelState.IsValid** is true.</span></span> <span data-ttu-id="e7798-147">在這種情況下，您可以使用**ODataActionParameters**字典來取得參數值。</span><span class="sxs-lookup"><span data-stu-id="e7798-147">In that case, you can use the **ODataActionParameters** dictionary to get the parameter values.</span></span> <span data-ttu-id="e7798-148">在此範例中，`RateProduct` 動作會接受名為「評等」的單一參數。</span><span class="sxs-lookup"><span data-stu-id="e7798-148">In this example, the `RateProduct` action takes a single parameter named "Rating".</span></span>

## <a name="action-metadata"></a><span data-ttu-id="e7798-149">動作中繼資料</span><span class="sxs-lookup"><span data-stu-id="e7798-149">Action Metadata</span></span>

<span data-ttu-id="e7798-150">若要查看服務中繼資料，請將 GET 要求傳送至/odata/$metadata。</span><span class="sxs-lookup"><span data-stu-id="e7798-150">To view the service metadata, send a GET request to /odata/$metadata.</span></span> <span data-ttu-id="e7798-151">以下是宣告 `RateProduct` 動作的中繼資料部分：</span><span class="sxs-lookup"><span data-stu-id="e7798-151">Here is the portion of the metadata that declares the `RateProduct` action:</span></span>

[!code-xml[Main](odata-actions/samples/sample7.xml)]

<span data-ttu-id="e7798-152">**FunctionImport**元素會宣告動作。</span><span class="sxs-lookup"><span data-stu-id="e7798-152">The **FunctionImport** element declares the action.</span></span> <span data-ttu-id="e7798-153">大部分的欄位都是一目了然的，但有兩個值得注意的：</span><span class="sxs-lookup"><span data-stu-id="e7798-153">Most of the fields are self-explanatory, but two are worth noting:</span></span>

- <span data-ttu-id="e7798-154">**Isbindable 時**表示可在目標實體上叫用此動作，至少必須有一些時間。</span><span class="sxs-lookup"><span data-stu-id="e7798-154">**IsBindable** means the action can be invoked on the target entity, at least some of the time.</span></span>
- <span data-ttu-id="e7798-155">**IsAlwaysBindable**表示動作一律可在目標實體上叫用。</span><span class="sxs-lookup"><span data-stu-id="e7798-155">**IsAlwaysBindable** means the action can always be invoked on the target entity.</span></span>

<span data-ttu-id="e7798-156">差別在於某些動作一律可供用戶端使用，但其他動作則可能取決於實體的狀態。</span><span class="sxs-lookup"><span data-stu-id="e7798-156">The difference is that some actions are always available to clients, but other actions might depend on the state of the entity.</span></span> <span data-ttu-id="e7798-157">例如，假設您定義了「購買」動作。</span><span class="sxs-lookup"><span data-stu-id="e7798-157">For example, suppose you define a "Purchase" action.</span></span> <span data-ttu-id="e7798-158">您只能購買庫存中的專案。</span><span class="sxs-lookup"><span data-stu-id="e7798-158">You can only purchase an item that is in stock.</span></span> <span data-ttu-id="e7798-159">如果專案已脫銷，用戶端就無法叫用該動作。</span><span class="sxs-lookup"><span data-stu-id="e7798-159">If the item is out of stock, a client cannot invoke that action.</span></span>

<span data-ttu-id="e7798-160">當您定義 EDM 時，**動作**方法會建立永遠可系結的動作：</span><span class="sxs-lookup"><span data-stu-id="e7798-160">When you define the EDM, the **Action** method creates an always-bindable action:</span></span>

[!code-csharp[Main](odata-actions/samples/sample8.cs?highlight=1)]

<span data-ttu-id="e7798-161">我將在本主題稍後討論不一定可系結的動作（也稱為*暫時性*動作）。</span><span class="sxs-lookup"><span data-stu-id="e7798-161">I'll talk about not-always-bindable actions (also called *transient* actions) later in this topic.</span></span>

## <a name="invoking-the-action"></a><span data-ttu-id="e7798-162">叫用動作</span><span class="sxs-lookup"><span data-stu-id="e7798-162">Invoking the Action</span></span>

<span data-ttu-id="e7798-163">現在讓我們來看看用戶端叫用此動作的方式。</span><span class="sxs-lookup"><span data-stu-id="e7798-163">Now let's see how a client would invoke this action.</span></span> <span data-ttu-id="e7798-164">假設用戶端想要為識別碼為4的產品提供2的評等。</span><span class="sxs-lookup"><span data-stu-id="e7798-164">Suppose the client wants to give a rating of 2 to the product with ID = 4.</span></span> <span data-ttu-id="e7798-165">以下是範例要求訊息，其中使用 JSON 格式的要求本文：</span><span class="sxs-lookup"><span data-stu-id="e7798-165">Here is an example request message, using JSON format for the request body:</span></span>

[!code-console[Main](odata-actions/samples/sample9.cmd)]

<span data-ttu-id="e7798-166">以下是回應訊息：</span><span class="sxs-lookup"><span data-stu-id="e7798-166">Here is the response message:</span></span>

[!code-console[Main](odata-actions/samples/sample10.cmd)]

## <a name="binding-an-action-to-an-entity-set"></a><span data-ttu-id="e7798-167">將動作系結至實體集</span><span class="sxs-lookup"><span data-stu-id="e7798-167">Binding an Action to an Entity Set</span></span>

<span data-ttu-id="e7798-168">在上述範例中，動作會系結至單一實體：用戶端會對單一產品進行速率。</span><span class="sxs-lookup"><span data-stu-id="e7798-168">In the previous example, the action is bound to a single entity: The client rates a single product.</span></span> <span data-ttu-id="e7798-169">您也可以將動作系結至實體的集合。</span><span class="sxs-lookup"><span data-stu-id="e7798-169">You can also bind an action to a collection of entities.</span></span> <span data-ttu-id="e7798-170">只要進行下列變更：</span><span class="sxs-lookup"><span data-stu-id="e7798-170">Just make the following changes:</span></span>

<span data-ttu-id="e7798-171">在 EDM 中，將動作加入至實體的**集合**屬性。</span><span class="sxs-lookup"><span data-stu-id="e7798-171">In the EDM, add the action to the entity's **Collection** property.</span></span>

[!code-csharp[Main](odata-actions/samples/sample11.cs?highlight=1)]

<span data-ttu-id="e7798-172">在控制器方法中，省略*key*參數。</span><span class="sxs-lookup"><span data-stu-id="e7798-172">In the controller method, omit the *key* parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample12.cs)]

<span data-ttu-id="e7798-173">現在，用戶端會叫用 Products 實體集上的動作：</span><span class="sxs-lookup"><span data-stu-id="e7798-173">Now the client invokes the action on the Products entity set:</span></span>

[!code-console[Main](odata-actions/samples/sample13.cmd)]

## <a name="actions-with-collection-parameters"></a><span data-ttu-id="e7798-174">具有集合參數的動作</span><span class="sxs-lookup"><span data-stu-id="e7798-174">Actions with Collection Parameters</span></span>

<span data-ttu-id="e7798-175">動作可以具有接受值集合的參數。</span><span class="sxs-lookup"><span data-stu-id="e7798-175">Actions can have parameters that take a collection of values.</span></span> <span data-ttu-id="e7798-176">在 EDM 中，使用**CollectionParameter&lt;t&gt;** 來宣告參數。</span><span class="sxs-lookup"><span data-stu-id="e7798-176">In the EDM, use **CollectionParameter&lt;T&gt;** to declare the parameter.</span></span>

[!code-csharp[Main](odata-actions/samples/sample14.cs)]

<span data-ttu-id="e7798-177">這會宣告名為「評等」的參數，其接受**int**值的集合。</span><span class="sxs-lookup"><span data-stu-id="e7798-177">This declares a parameter named "Ratings" that takes a collection of **int** values.</span></span> <span data-ttu-id="e7798-178">在控制器方法中，您仍然會從**ODataActionParameters**物件取得參數值，但現在的值是**ICollection&lt;int&gt;** 值：</span><span class="sxs-lookup"><span data-stu-id="e7798-178">In the controller method, you still get the parameter value from the **ODataActionParameters** object, but now the value is an **ICollection&lt;int&gt;** value:</span></span>

[!code-csharp[Main](odata-actions/samples/sample15.cs)]

## <a name="transient-actions"></a><span data-ttu-id="e7798-179">暫時性動作</span><span class="sxs-lookup"><span data-stu-id="e7798-179">Transient Actions</span></span>

<span data-ttu-id="e7798-180">在 "RateProduct" 範例中，使用者一律可以對產品進行評分，因此此動作一律可供使用。</span><span class="sxs-lookup"><span data-stu-id="e7798-180">In the "RateProduct" example, users can always rate a product, so the action is always available.</span></span> <span data-ttu-id="e7798-181">但某些動作取決於實體的狀態。</span><span class="sxs-lookup"><span data-stu-id="e7798-181">But some actions depend on the state of the entity.</span></span> <span data-ttu-id="e7798-182">例如，在影片出租服務中，「結帳」動作不一定可供使用。</span><span class="sxs-lookup"><span data-stu-id="e7798-182">For example, in a video rental service, the "CheckOut" action is not always available.</span></span> <span data-ttu-id="e7798-183">（這取決於該影片的複本是否可供使用。）這種類型的動作稱為「*暫時性*動作」。</span><span class="sxs-lookup"><span data-stu-id="e7798-183">(It depends whether a copy of that video is available.) This type of action is called a *transient* action.</span></span>

<span data-ttu-id="e7798-184">在服務中繼資料中，暫時性動作的**IsAlwaysBindable**等於 false。</span><span class="sxs-lookup"><span data-stu-id="e7798-184">In the service metadata, a transient action has **IsAlwaysBindable** equal to false.</span></span> <span data-ttu-id="e7798-185">這實際上是預設值，因此中繼資料看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="e7798-185">That's actually the default value, so the metadata will look like this:</span></span>

[!code-xml[Main](odata-actions/samples/sample16.xml)]

<span data-ttu-id="e7798-186">這就是為什麼這是很重要的原因：如果某個動作是暫時性的，伺服器就必須在有動作可用時告訴用戶端。</span><span class="sxs-lookup"><span data-stu-id="e7798-186">Here's why this matters: If an action is transient, the server needs to tell the client when the action is available.</span></span> <span data-ttu-id="e7798-187">其方式是在實體中包含動作的連結。</span><span class="sxs-lookup"><span data-stu-id="e7798-187">It does this by including a link to the action in the entity.</span></span> <span data-ttu-id="e7798-188">以下是 Movie 實體的範例：</span><span class="sxs-lookup"><span data-stu-id="e7798-188">Here is an example for a Movie entity:</span></span>

[!code-console[Main](odata-actions/samples/sample17.cmd)]

<span data-ttu-id="e7798-189">"#CheckOut" 屬性包含 [簽出] 動作的連結。</span><span class="sxs-lookup"><span data-stu-id="e7798-189">The "#CheckOut" property contains a link to the CheckOut action.</span></span> <span data-ttu-id="e7798-190">如果動作無法使用，伺服器就會省略連結。</span><span class="sxs-lookup"><span data-stu-id="e7798-190">If the action is not available, the server omits the link.</span></span>

<span data-ttu-id="e7798-191">若要在 EDM 中宣告暫時性動作，請呼叫**TransientAction**方法：</span><span class="sxs-lookup"><span data-stu-id="e7798-191">To declare a transient action in the EDM, call the **TransientAction** method:</span></span>

[!code-csharp[Main](odata-actions/samples/sample18.cs)]

<span data-ttu-id="e7798-192">此外，您還必須提供函式，以傳回指定實體的動作連結。</span><span class="sxs-lookup"><span data-stu-id="e7798-192">Also, you must provide a function that returns an action link for a given entity.</span></span> <span data-ttu-id="e7798-193">藉由呼叫**HasActionLink**來設定此函式。</span><span class="sxs-lookup"><span data-stu-id="e7798-193">Set this function by calling **HasActionLink**.</span></span> <span data-ttu-id="e7798-194">您可以撰寫函式做為 lambda 運算式：</span><span class="sxs-lookup"><span data-stu-id="e7798-194">You can write the function as a lambda expression:</span></span>

[!code-csharp[Main](odata-actions/samples/sample19.cs)]

<span data-ttu-id="e7798-195">如果動作可供使用，lambda 運算式會傳回動作的連結。</span><span class="sxs-lookup"><span data-stu-id="e7798-195">If the action is available, the lambda expression returns a link to the action.</span></span> <span data-ttu-id="e7798-196">OData 序列化程式會在序列化實體時包含此連結。</span><span class="sxs-lookup"><span data-stu-id="e7798-196">The OData serializer includes this link when it serializes the entity.</span></span> <span data-ttu-id="e7798-197">當動作無法使用時，函數會傳回 `null`。</span><span class="sxs-lookup"><span data-stu-id="e7798-197">When the action is not available, the function returns `null`.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="e7798-198">其他資源</span><span class="sxs-lookup"><span data-stu-id="e7798-198">Additional Resources</span></span>

[<span data-ttu-id="e7798-199">OData 動作範例</span><span class="sxs-lookup"><span data-stu-id="e7798-199">OData Actions Sample</span></span>](http://aspnet.codeplex.com/sourcecontrol/latest#Samples/WebApi/OData/v3/ODataActionsSample/)
