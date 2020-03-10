---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
title: 第2部分：建立領域模型 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/03/2012
ms.assetid: fe3ef85f-bdc6-4e10-9768-25aa565c01d0
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-2
msc.type: authoredcontent
ms.openlocfilehash: 7c5ed1bdb4b390c94907b14e208231f16ad42d96
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78621818"
---
# <a name="part-2-creating-the-domain-models"></a><span data-ttu-id="912b5-102">第2部分：建立領域模型</span><span class="sxs-lookup"><span data-stu-id="912b5-102">Part 2: Creating the Domain Models</span></span>

<span data-ttu-id="912b5-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="912b5-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="912b5-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="912b5-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-models"></a><span data-ttu-id="912b5-105">加入模型</span><span class="sxs-lookup"><span data-stu-id="912b5-105">Add Models</span></span>

<span data-ttu-id="912b5-106">有三種方法可以 Entity Framework：</span><span class="sxs-lookup"><span data-stu-id="912b5-106">There are three ways to approach Entity Framework:</span></span>

- <span data-ttu-id="912b5-107">Database-首先：您會開始使用資料庫，而 Entity Framework 會產生程式碼。</span><span class="sxs-lookup"><span data-stu-id="912b5-107">Database-first: You start with a database, and Entity Framework generates the code.</span></span>
- <span data-ttu-id="912b5-108">模型優先：從視覺模型開始，Entity Framework 會產生資料庫和程式碼。</span><span class="sxs-lookup"><span data-stu-id="912b5-108">Model-first: You start with a visual model, and Entity Framework generates both the database and code.</span></span>
- <span data-ttu-id="912b5-109">程式碼優先：開始使用程式碼，Entity Framework 產生資料庫。</span><span class="sxs-lookup"><span data-stu-id="912b5-109">Code-first: You start with code, and Entity Framework generates the database.</span></span>

<span data-ttu-id="912b5-110">我們使用的是程式碼優先方法，因此我們一開始會將網域物件定義為 Poco （純舊的 CLR 物件）。</span><span class="sxs-lookup"><span data-stu-id="912b5-110">We are using the code-first approach, so we start by defining our domain objects as POCOs (plain-old CLR objects).</span></span> <span data-ttu-id="912b5-111">透過程式碼優先方法，網域物件不需要任何額外的程式碼來支援資料庫層，例如交易或持續性。</span><span class="sxs-lookup"><span data-stu-id="912b5-111">With the code-first approach, domain objects don't need any extra code to support the database layer, such as transactions or persistence.</span></span> <span data-ttu-id="912b5-112">（具體而言，它們不需要繼承自[EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx)類別）。您仍然可以使用資料批註來控制 Entity Framework 如何建立資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="912b5-112">(Specifically, they do not need to inherit from the [EntityObject](https://msdn.microsoft.com/library/system.data.objects.dataclasses.entityobject.aspx) class.) You can still use data annotations to control how Entity Framework creates the database schema.</span></span>

<span data-ttu-id="912b5-113">由於 Poco 不會包含任何描述[資料庫狀態](https://msdn.microsoft.com/library/system.data.entitystate.aspx)的額外屬性，因此可以輕鬆地序列化為 JSON 或 XML。</span><span class="sxs-lookup"><span data-stu-id="912b5-113">Because POCOs do not carry any extra properties that describe [database state](https://msdn.microsoft.com/library/system.data.entitystate.aspx), they can easily be serialized to JSON or XML.</span></span> <span data-ttu-id="912b5-114">不過，這並不表示您應該一律將 Entity Framework 模型直接公開給用戶端，如我們稍後在本教學課程中所見。</span><span class="sxs-lookup"><span data-stu-id="912b5-114">However, that does not mean you should always expose your Entity Framework models directly to clients, as we'll see later in the tutorial.</span></span>

<span data-ttu-id="912b5-115">我們將建立下列 Poco：</span><span class="sxs-lookup"><span data-stu-id="912b5-115">We will create the following POCOs:</span></span>

- <span data-ttu-id="912b5-116">Products</span><span class="sxs-lookup"><span data-stu-id="912b5-116">Product</span></span>
- <span data-ttu-id="912b5-117">順序</span><span class="sxs-lookup"><span data-stu-id="912b5-117">Order</span></span>
- <span data-ttu-id="912b5-118">OrderDetail</span><span class="sxs-lookup"><span data-stu-id="912b5-118">OrderDetail</span></span>

<span data-ttu-id="912b5-119">若要建立每個類別，請以滑鼠右鍵按一下方案總管中的 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="912b5-119">To create each class, right-click the Models folder in Solution Explorer.</span></span> <span data-ttu-id="912b5-120">從內容功能表中，選取 [**新增**]，然後選取 [**類別]。**</span><span class="sxs-lookup"><span data-stu-id="912b5-120">From the context menu, select **Add** and then select **Class.**</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image1.png)

<span data-ttu-id="912b5-121">新增具有下列執行的 `Product` 類別：</span><span class="sxs-lookup"><span data-stu-id="912b5-121">Add a `Product` class with the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample1.cs)]

<span data-ttu-id="912b5-122">依照慣例，Entity Framework 會使用 `Id` 屬性作為主要索引鍵，並將它對應至資料庫資料表中的識別欄位。</span><span class="sxs-lookup"><span data-stu-id="912b5-122">By convention, Entity Framework uses the `Id` property as the primary key and maps it to an identity column in the database table.</span></span> <span data-ttu-id="912b5-123">當您建立新的 `Product` 實例時，您不會設定 `Id`的值，因為資料庫會產生值。</span><span class="sxs-lookup"><span data-stu-id="912b5-123">When you create a new `Product` instance, you won't set a value for `Id`, because the database generates the value.</span></span>

<span data-ttu-id="912b5-124">**ScaffoldColumn**屬性會在產生編輯器表單時，告訴 ASP.NET MVC 略過 `Id` 屬性。</span><span class="sxs-lookup"><span data-stu-id="912b5-124">The **ScaffoldColumn** attribute tells ASP.NET MVC to skip the `Id` property when generating an editor form.</span></span> <span data-ttu-id="912b5-125">**必要**的屬性是用來驗證模型。</span><span class="sxs-lookup"><span data-stu-id="912b5-125">The **Required** attribute is used to validate the model.</span></span> <span data-ttu-id="912b5-126">它會指定 `Name` 屬性必須是非空白字串。</span><span class="sxs-lookup"><span data-stu-id="912b5-126">It specifies that the `Name` property must be a non-empty string.</span></span>

<span data-ttu-id="912b5-127">新增 `Order` 類別：</span><span class="sxs-lookup"><span data-stu-id="912b5-127">Add the `Order` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample2.cs)]

<span data-ttu-id="912b5-128">新增 `OrderDetail` 類別：</span><span class="sxs-lookup"><span data-stu-id="912b5-128">Add the `OrderDetail` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample3.cs)]

## <a name="foreign-key-relations"></a><span data-ttu-id="912b5-129">外鍵關聯性</span><span class="sxs-lookup"><span data-stu-id="912b5-129">Foreign Key Relations</span></span>

<span data-ttu-id="912b5-130">訂單包含許多訂單明細，而每個訂單詳細資料則是指單一產品。</span><span class="sxs-lookup"><span data-stu-id="912b5-130">An order contains many order details, and each order detail refers to a single product.</span></span> <span data-ttu-id="912b5-131">為了表示這些關聯性，`OrderDetail` 類別會定義名為 `OrderId` 和 `ProductId`的屬性。</span><span class="sxs-lookup"><span data-stu-id="912b5-131">To represent these relations, the `OrderDetail` class defines properties named `OrderId` and `ProductId`.</span></span> <span data-ttu-id="912b5-132">Entity Framework 會推斷這些屬性代表外鍵，而且會將外鍵條件約束加入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="912b5-132">Entity Framework will infer that these properties represent foreign keys, and will add foreign-key constraints to the database.</span></span>

![](using-web-api-with-entity-framework-part-2/_static/image2.png)

<span data-ttu-id="912b5-133">`Order` 和 `OrderDetail` 類別也包含 "導覽" 屬性，其中包含相關物件的參考。</span><span class="sxs-lookup"><span data-stu-id="912b5-133">The `Order` and `OrderDetail` classes also include "navigation" properties, which contain references to the related objects.</span></span> <span data-ttu-id="912b5-134">根據您的順序，您可以遵循導覽屬性，流覽至訂單中的產品。</span><span class="sxs-lookup"><span data-stu-id="912b5-134">Given an order, you can navigate to the products in the order by following the navigation properties.</span></span>

<span data-ttu-id="912b5-135">立即編譯專案。</span><span class="sxs-lookup"><span data-stu-id="912b5-135">Compile the project now.</span></span> <span data-ttu-id="912b5-136">Entity Framework 會使用反映來探索模型的屬性，因此需要已編譯的元件來建立資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="912b5-136">Entity Framework uses reflection to discover the properties of the models, so it requires a compiled assembly to create the database schema.</span></span>

## <a name="configure-the-media-type-formatters"></a><span data-ttu-id="912b5-137">設定媒體類型格式器</span><span class="sxs-lookup"><span data-stu-id="912b5-137">Configure the Media-Type Formatters</span></span>

<span data-ttu-id="912b5-138">[媒體類型格式](../../formats-and-model-binding/media-formatters.md)器是一種物件，可在 Web API 寫入 HTTP 回應本文時，將您的資料序列化。</span><span class="sxs-lookup"><span data-stu-id="912b5-138">A [media-type formatter](../../formats-and-model-binding/media-formatters.md) is an object that serializes your data when Web API writes the HTTP response body.</span></span> <span data-ttu-id="912b5-139">內建的格式器支援 JSON 和 XML 輸出。</span><span class="sxs-lookup"><span data-stu-id="912b5-139">The built-in formatters support JSON and XML output.</span></span> <span data-ttu-id="912b5-140">根據預設，這兩個格式子都會以傳值方式序列化所有物件。</span><span class="sxs-lookup"><span data-stu-id="912b5-140">By default, both of these formatters serialize all objects by value.</span></span>

<span data-ttu-id="912b5-141">如果物件圖形包含迴圈參考，依值序列化會產生問題。</span><span class="sxs-lookup"><span data-stu-id="912b5-141">Serialization by value creates a problem if an object graph contains circular references.</span></span> <span data-ttu-id="912b5-142">這就是 `Order` 和 `OrderDetail` 類別的情況，因為每個類別都有另一個參考。</span><span class="sxs-lookup"><span data-stu-id="912b5-142">That's exactly the case with the `Order` and `OrderDetail` classes, because each holds a reference to the other.</span></span> <span data-ttu-id="912b5-143">格式器會遵循參考、以傳值方式寫入每個物件，然後進入圓圈。</span><span class="sxs-lookup"><span data-stu-id="912b5-143">The formatter will follow the references, writing each object by value, and go in circles.</span></span> <span data-ttu-id="912b5-144">因此，我們需要變更預設行為。</span><span class="sxs-lookup"><span data-stu-id="912b5-144">Therefore, we need to change the default behavior.</span></span>

<span data-ttu-id="912b5-145">在方案總管中，展開應用程式\_開始 資料夾，然後開啟名為 WebApiConfig.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="912b5-145">In Solution Explorer, expand the App\_Start folder and open the file named WebApiConfig.cs.</span></span> <span data-ttu-id="912b5-146">將下列程式碼加入 `WebApiConfig` 類別：</span><span class="sxs-lookup"><span data-stu-id="912b5-146">Add the following code to the `WebApiConfig` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-2/samples/sample4.cs?highlight=11)]

<span data-ttu-id="912b5-147">這段程式碼會設定 JSON 格式器來保留物件參考，並從管線中移除 XML 格式器。</span><span class="sxs-lookup"><span data-stu-id="912b5-147">This code sets the JSON formatter to preserve object references, and removes the XML formatter from the pipeline entirely.</span></span> <span data-ttu-id="912b5-148">（您可以設定 XML 格式器來保留物件參考，但這是比較好的工作，而且我們只需要此應用程式的 JSON。</span><span class="sxs-lookup"><span data-stu-id="912b5-148">(You can configure the XML formatter to preserve object references, but it's a little more work, and we only need JSON for this application.</span></span> <span data-ttu-id="912b5-149">如需詳細資訊，請參閱[處理迴圈物件參考](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references)。）</span><span class="sxs-lookup"><span data-stu-id="912b5-149">For more information, see [Handling Circular Object References](../../formats-and-model-binding/json-and-xml-serialization.md#handling_circular_object_references).)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="912b5-150">[上一頁](using-web-api-with-entity-framework-part-1.md)
> [下一頁](using-web-api-with-entity-framework-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="912b5-150">[Previous](using-web-api-with-entity-framework-part-1.md)
[Next](using-web-api-with-entity-framework-part-3.md)</span></span>
