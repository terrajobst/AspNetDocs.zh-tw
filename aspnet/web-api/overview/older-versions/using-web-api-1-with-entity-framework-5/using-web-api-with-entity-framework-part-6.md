---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
title: 第6部分：建立產品和訂單控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 91ee29ee-0689-40ee-914a-e7dd733b6622
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-6
msc.type: authoredcontent
ms.openlocfilehash: e0bf88e3477acbde910cde956042449bc86ce79a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78524987"
---
# <a name="part-6-creating-product-and-order-controllers"></a><span data-ttu-id="02768-102">第6部分：建立產品和訂單控制器</span><span class="sxs-lookup"><span data-stu-id="02768-102">Part 6: Creating Product and Order Controllers</span></span>

<span data-ttu-id="02768-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="02768-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="02768-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="02768-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-a-products-controller"></a><span data-ttu-id="02768-105">新增產品控制器</span><span class="sxs-lookup"><span data-stu-id="02768-105">Add a Products Controller</span></span>

<span data-ttu-id="02768-106">管理控制器是針對具有系統管理員許可權的使用者。</span><span class="sxs-lookup"><span data-stu-id="02768-106">The Admin controller is for users who have administrator privileges.</span></span> <span data-ttu-id="02768-107">另一方面，客戶可以查看產品，但無法建立、更新或刪除它們。</span><span class="sxs-lookup"><span data-stu-id="02768-107">Customers, on the other hand, can view products but cannot create, update, or delete them.</span></span>

<span data-ttu-id="02768-108">我們可以輕鬆地限制對 Post、Put 和 Delete 方法的存取，同時讓 Get 方法保持開啟。</span><span class="sxs-lookup"><span data-stu-id="02768-108">We can easily restrict access to the Post, Put, and Delete methods, while leaving the Get methods open.</span></span> <span data-ttu-id="02768-109">但請查看針對產品所傳回的資料：</span><span class="sxs-lookup"><span data-stu-id="02768-109">But look at the data that is returned for a product:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample1.json?highlight=1)]

<span data-ttu-id="02768-110">客戶應該看不到 `ActualCost` 屬性！</span><span class="sxs-lookup"><span data-stu-id="02768-110">The `ActualCost` property should not be visible to customers!</span></span> <span data-ttu-id="02768-111">解決方法是定義*資料傳輸物件*（DTO），其中包含客戶應看到的屬性子集。</span><span class="sxs-lookup"><span data-stu-id="02768-111">The solution is to define a *data transfer object* (DTO) that includes a subset of properties that should be visible to customers.</span></span> <span data-ttu-id="02768-112">我們將使用 LINQ to project `Product` 實例來 `ProductDTO` 實例。</span><span class="sxs-lookup"><span data-stu-id="02768-112">We will use LINQ to project `Product` instances to `ProductDTO` instances.</span></span>

<span data-ttu-id="02768-113">將名為 `ProductDTO` 的類別新增至 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="02768-113">Add a class named `ProductDTO` to the Models folder.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample2.cs)]

<span data-ttu-id="02768-114">現在新增控制器。</span><span class="sxs-lookup"><span data-stu-id="02768-114">Now add the controller.</span></span> <span data-ttu-id="02768-115">在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="02768-115">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="02768-116">選取 [**新增**]，然後選取 [**控制器**]。</span><span class="sxs-lookup"><span data-stu-id="02768-116">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="02768-117">在 [**新增控制器**] 對話方塊中，將控制器命名為 &quot;productscontroller.cs&quot;。</span><span class="sxs-lookup"><span data-stu-id="02768-117">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="02768-118">在 [**範本**] 底下，選取 [**空的 API 控制器**]。</span><span class="sxs-lookup"><span data-stu-id="02768-118">Under **Template**, select **Empty API controller**.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image1.png)

<span data-ttu-id="02768-119">使用下列程式碼取代原始程式檔中的所有專案：</span><span class="sxs-lookup"><span data-stu-id="02768-119">Replace everything in the source file with the following code:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample3.cs)]

<span data-ttu-id="02768-120">控制器仍然會使用 `OrdersContext` 來查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="02768-120">The controller still uses the `OrdersContext` to query the database.</span></span> <span data-ttu-id="02768-121">但我們不會直接傳回 `Product` 實例，而是呼叫 `MapProducts` 將其投射至 `ProductDTO` 實例：</span><span class="sxs-lookup"><span data-stu-id="02768-121">But instead of returning `Product` instances directly, we call `MapProducts` to project them onto `ProductDTO` instances:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample4.cs?highlight=1)]

<span data-ttu-id="02768-122">`MapProducts` 方法會傳回**IQueryable**，因此我們可以使用其他查詢參數來撰寫結果。</span><span class="sxs-lookup"><span data-stu-id="02768-122">The `MapProducts` method returns an **IQueryable**, so we can compose the result with other query parameters.</span></span> <span data-ttu-id="02768-123">您可以在 `GetProduct` 方法中看到這個，這會在查詢中加入**where**子句：</span><span class="sxs-lookup"><span data-stu-id="02768-123">You can see this in the `GetProduct` method, which adds a **where** clause to the query:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample5.cs?highlight=2)]

## <a name="add-an-orders-controller"></a><span data-ttu-id="02768-124">新增訂單控制器</span><span class="sxs-lookup"><span data-stu-id="02768-124">Add an Orders Controller</span></span>

<span data-ttu-id="02768-125">接下來，新增可讓使用者建立和查看訂單的控制器。</span><span class="sxs-lookup"><span data-stu-id="02768-125">Next, add a controller that lets users create and view orders.</span></span>

<span data-ttu-id="02768-126">我們會從另一個 DTO 開始。</span><span class="sxs-lookup"><span data-stu-id="02768-126">We'll start with another DTO.</span></span> <span data-ttu-id="02768-127">在方案總管中，以滑鼠右鍵按一下 [模型] 資料夾，然後新增名為 `OrderDTO` 的類別使用下列執行：</span><span class="sxs-lookup"><span data-stu-id="02768-127">In Solution Explorer, right-click the Models folder and add a class named `OrderDTO` Use the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample6.cs)]

<span data-ttu-id="02768-128">現在新增控制器。</span><span class="sxs-lookup"><span data-stu-id="02768-128">Now add the controller.</span></span> <span data-ttu-id="02768-129">在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="02768-129">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="02768-130">選取 [**新增**]，然後選取 [**控制器**]。</span><span class="sxs-lookup"><span data-stu-id="02768-130">Select **Add**, then select **Controller**.</span></span> <span data-ttu-id="02768-131">在 [**新增控制器**] 對話方塊中，設定下列選項：</span><span class="sxs-lookup"><span data-stu-id="02768-131">In the **Add Controller** dialog, set the following options:</span></span>

- <span data-ttu-id="02768-132">在 [**控制器名稱**] 下，輸入 "OrdersController"。</span><span class="sxs-lookup"><span data-stu-id="02768-132">Under **Controller Name**, enter "OrdersController".</span></span>
- <span data-ttu-id="02768-133">在 **範本** 底下，選取 具有讀取/寫入動作的 API 控制器，並使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="02768-133">Under **Template**, select "API controller with read/write actions, using Entity Framework".</span></span>
- <span data-ttu-id="02768-134">在 [**模型類別**] 下，選取 [&quot;順序] （ProductStore）&quot;。</span><span class="sxs-lookup"><span data-stu-id="02768-134">Under **Model class**, select &quot;Order (ProductStore.Models)&quot;.</span></span>
- <span data-ttu-id="02768-135">在 [**資料內容類別**] 底下，選取 [&quot;OrdersCoNtext （ProductStore）]&quot;。</span><span class="sxs-lookup"><span data-stu-id="02768-135">Under **Data context class**, select &quot;OrdersContext (ProductStore.Models)&quot;.</span></span>

![](using-web-api-with-entity-framework-part-6/_static/image2.png)

<span data-ttu-id="02768-136">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="02768-136">Click **Add**.</span></span> <span data-ttu-id="02768-137">這會新增名為 OrdersController.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="02768-137">This adds a file named OrdersController.cs.</span></span> <span data-ttu-id="02768-138">接下來，我們需要修改控制器的預設執行。</span><span class="sxs-lookup"><span data-stu-id="02768-138">Next, we need to modify the default implementation of the controller.</span></span>

<span data-ttu-id="02768-139">首先，刪除 `PutOrder` 和 `DeleteOrder` 方法。</span><span class="sxs-lookup"><span data-stu-id="02768-139">First, delete the `PutOrder` and `DeleteOrder` methods.</span></span> <span data-ttu-id="02768-140">在此範例中，客戶無法修改或刪除現有的訂單。</span><span class="sxs-lookup"><span data-stu-id="02768-140">For this sample, customers cannot modify or delete existing orders.</span></span> <span data-ttu-id="02768-141">在實際的應用程式中，您需要許多後端邏輯來處理這些情況。</span><span class="sxs-lookup"><span data-stu-id="02768-141">In a real application, you would need lots of back-end logic to handle these cases.</span></span> <span data-ttu-id="02768-142">（例如，訂單是否已出貨？）</span><span class="sxs-lookup"><span data-stu-id="02768-142">(For example, was the order already shipped?)</span></span>

<span data-ttu-id="02768-143">變更 `GetOrders` 方法，只傳回屬於使用者的訂單：</span><span class="sxs-lookup"><span data-stu-id="02768-143">Change the `GetOrders` method to return just the orders that belong to the user:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample7.cs)]

<span data-ttu-id="02768-144">變更 `GetOrder` 方法，如下所示：</span><span class="sxs-lookup"><span data-stu-id="02768-144">Change the `GetOrder` method as follows:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample8.cs)]

<span data-ttu-id="02768-145">以下是我們對方法所做的變更：</span><span class="sxs-lookup"><span data-stu-id="02768-145">Here are the changes that we made to the method:</span></span>

- <span data-ttu-id="02768-146">傳回值是 `OrderDTO` 實例，而不是 `Order`。</span><span class="sxs-lookup"><span data-stu-id="02768-146">The return value is an `OrderDTO` instance, instead of an `Order`.</span></span>
- <span data-ttu-id="02768-147">當我們查詢資料庫的順序時，我們會使用[DbQuery](https://msdn.microsoft.com/library/gg696395)方法來提取相關的 `OrderDetail` 和 `Product` 實體。</span><span class="sxs-lookup"><span data-stu-id="02768-147">When we query the database for the order, we use the [DbQuery.Include](https://msdn.microsoft.com/library/gg696395) method to fetch the related `OrderDetail` and `Product` entities.</span></span>
- <span data-ttu-id="02768-148">我們使用投射來壓平合併結果。</span><span class="sxs-lookup"><span data-stu-id="02768-148">We flatten the result by using a projection.</span></span>

<span data-ttu-id="02768-149">HTTP 回應會包含具有數量的產品陣列：</span><span class="sxs-lookup"><span data-stu-id="02768-149">The HTTP response will contain an array of products with quantities:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample9.json)]

<span data-ttu-id="02768-150">此格式比原始物件圖形更容易取用，其包含嵌套的實體（順序、詳細資料和產品）。</span><span class="sxs-lookup"><span data-stu-id="02768-150">This format is easier for clients to consume than the original object graph, which contains nested entities (order, details, and products).</span></span>

<span data-ttu-id="02768-151">要將它視為 `PostOrder`的最後一個方法。</span><span class="sxs-lookup"><span data-stu-id="02768-151">The last method to consider it `PostOrder`.</span></span> <span data-ttu-id="02768-152">現在，這個方法會採用 `Order` 實例。</span><span class="sxs-lookup"><span data-stu-id="02768-152">Right now, this method takes an `Order` instance.</span></span> <span data-ttu-id="02768-153">但是，請考慮用戶端傳送要求本文時所發生的狀況，如下所示：</span><span class="sxs-lookup"><span data-stu-id="02768-153">But consider what happens if a client sends a request body like this:</span></span>

[!code-json[Main](using-web-api-with-entity-framework-part-6/samples/sample10.json)]

<span data-ttu-id="02768-154">這是結構良好的順序，Entity Framework 會很高興地將它插入資料庫中。</span><span class="sxs-lookup"><span data-stu-id="02768-154">This is a well-structured order, and Entity Framework will happily insert it into the database.</span></span> <span data-ttu-id="02768-155">但它包含先前不存在的產品實體。</span><span class="sxs-lookup"><span data-stu-id="02768-155">But it contains a Product entity that did not exist previously.</span></span> <span data-ttu-id="02768-156">用戶端剛剛在資料庫中建立了新的產品！</span><span class="sxs-lookup"><span data-stu-id="02768-156">The client just created a new product in our database!</span></span> <span data-ttu-id="02768-157">當訂單履行部門看到 koala 的人的訂單時，這會很驚訝。</span><span class="sxs-lookup"><span data-stu-id="02768-157">This will be a surprise to the order fulfillment department, when they see an order for koala bears.</span></span> <span data-ttu-id="02768-158">值得注意的是，您在 POST 或 PUT 要求中所接受的資料非常謹慎。</span><span class="sxs-lookup"><span data-stu-id="02768-158">The moral is, be really careful about the data you accept in a POST or PUT request.</span></span>

<span data-ttu-id="02768-159">若要避免這個問題，請將 `PostOrder` 方法變更為採用 `OrderDTO` 實例。</span><span class="sxs-lookup"><span data-stu-id="02768-159">To avoid this problem, change the `PostOrder` method to take an `OrderDTO` instance.</span></span> <span data-ttu-id="02768-160">使用 `OrderDTO` 來建立 `Order`。</span><span class="sxs-lookup"><span data-stu-id="02768-160">Use the `OrderDTO` to create the `Order`.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample11.cs)]

<span data-ttu-id="02768-161">請注意，我們會使用 `ProductID` 和 `Quantity` 屬性，而我們會忽略用戶端針對產品名稱或價格所傳送的任何值。</span><span class="sxs-lookup"><span data-stu-id="02768-161">Notice that we use the `ProductID` and `Quantity` properties, and we ignore any values that the client sent for either product name or price.</span></span> <span data-ttu-id="02768-162">如果產品識別碼無效，它會違反資料庫中的外鍵條件約束，而插入將會失敗，如其所示。</span><span class="sxs-lookup"><span data-stu-id="02768-162">If the product ID is not valid, it will violate the foreign key constraint in the database, and the insert will fail, as it should.</span></span>

<span data-ttu-id="02768-163">以下是完整的 `PostOrder` 方法：</span><span class="sxs-lookup"><span data-stu-id="02768-163">Here is the complete `PostOrder` method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample12.cs)]

<span data-ttu-id="02768-164">最後，將**授權**屬性新增至控制器：</span><span class="sxs-lookup"><span data-stu-id="02768-164">Finally, add the **Authorize** attribute to the controller:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-6/samples/sample13.cs)]

<span data-ttu-id="02768-165">現在只有已註冊的使用者可以建立或查看訂單。</span><span class="sxs-lookup"><span data-stu-id="02768-165">Now only registered users can create or view orders.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="02768-166">[上一頁](using-web-api-with-entity-framework-part-5.md)
> [下一頁](using-web-api-with-entity-framework-part-7.md)</span><span class="sxs-lookup"><span data-stu-id="02768-166">[Previous](using-web-api-with-entity-framework-part-5.md)
[Next](using-web-api-with-entity-framework-part-7.md)</span></span>
