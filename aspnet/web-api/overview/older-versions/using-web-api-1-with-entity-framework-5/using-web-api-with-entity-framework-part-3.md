---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
title: 第3部分：建立管理控制器 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 6b9ae3c4-0274-4170-a1bb-9df9c546b2a9
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-3
msc.type: authoredcontent
ms.openlocfilehash: f39be7a84e85db93487d246e9f8cb59c401fe5ce
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556046"
---
# <a name="part-3-creating-an-admin-controller"></a><span data-ttu-id="449f4-102">第3部分：建立管理控制器</span><span class="sxs-lookup"><span data-stu-id="449f4-102">Part 3: Creating an Admin Controller</span></span>

<span data-ttu-id="449f4-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="449f4-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="449f4-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="449f4-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="add-an-admin-controller"></a><span data-ttu-id="449f4-105">新增管理控制器</span><span class="sxs-lookup"><span data-stu-id="449f4-105">Add an Admin Controller</span></span>

<span data-ttu-id="449f4-106">在本節中，我們將新增 Web API 控制器，以支援產品上的 CRUD （建立、讀取、更新和刪除）作業。</span><span class="sxs-lookup"><span data-stu-id="449f4-106">In this section, we'll add a Web API controller that supports CRUD (create, read, update, and delete) operations on products.</span></span> <span data-ttu-id="449f4-107">控制器會使用 Entity Framework 來與資料庫層通訊。</span><span class="sxs-lookup"><span data-stu-id="449f4-107">The controller will use Entity Framework to communicate with the database layer.</span></span> <span data-ttu-id="449f4-108">只有系統管理員可以使用此控制器。</span><span class="sxs-lookup"><span data-stu-id="449f4-108">Only administrators will be able to use this controller.</span></span> <span data-ttu-id="449f4-109">客戶會透過另一個控制器來存取產品。</span><span class="sxs-lookup"><span data-stu-id="449f4-109">Customers will access the products through another controller.</span></span>

<span data-ttu-id="449f4-110">在方案總管中，以滑鼠右鍵按一下 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="449f4-110">In Solution Explorer, right-click the Controllers folder.</span></span> <span data-ttu-id="449f4-111">依序選取 [**新增**] 和 [**控制器**]。</span><span class="sxs-lookup"><span data-stu-id="449f4-111">Select **Add** and then **Controller**.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image1.png)

<span data-ttu-id="449f4-112">在 [**新增控制器**] 對話方塊中，將控制器命名為 `AdminController`。</span><span class="sxs-lookup"><span data-stu-id="449f4-112">In the **Add Controller** dialog, name the controller `AdminController`.</span></span> <span data-ttu-id="449f4-113">在 [**範本**] 下，使用 Entity Framework&quot;選取具有讀取/寫入動作 &quot;API 控制器。</span><span class="sxs-lookup"><span data-stu-id="449f4-113">Under **Template**, select &quot;API controller with read/write actions, using Entity Framework&quot;.</span></span> <span data-ttu-id="449f4-114">在 [**模型類別**] 下，選取 [產品（ProductStore 模型）]。</span><span class="sxs-lookup"><span data-stu-id="449f4-114">Under **Model class**, select "Product (ProductStore.Models)".</span></span> <span data-ttu-id="449f4-115">在 [**資料內容**] 底下，選取 [&lt;新的資料內容&gt;]。</span><span class="sxs-lookup"><span data-stu-id="449f4-115">Under **Data Context**, select "&lt;New Data Context&gt;".</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image2.png)

> [!NOTE]
> <span data-ttu-id="449f4-116">如果 [**模型類別**] 下拉式按鈕沒有顯示任何模型類別，請確定您已編譯專案。</span><span class="sxs-lookup"><span data-stu-id="449f4-116">If the **Model class** drop-down does not show any model classes, make sure you compiled the project.</span></span> <span data-ttu-id="449f4-117">Entity Framework 使用反映，因此需要已編譯的元件。</span><span class="sxs-lookup"><span data-stu-id="449f4-117">Entity Framework uses reflection, so it needs the compiled assembly.</span></span>

<span data-ttu-id="449f4-118">選取 [&lt;新的資料內容&gt;] 將會開啟 [**新增資料內容**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="449f4-118">Selecting "&lt;New Data Context&gt;" will open the **New Data Context** dialog.</span></span> <span data-ttu-id="449f4-119">將資料內容命名 `ProductStore.Models.OrdersContext`。</span><span class="sxs-lookup"><span data-stu-id="449f4-119">Name the data context `ProductStore.Models.OrdersContext`.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image3.png)

<span data-ttu-id="449f4-120">按一下 **[確定]** 以關閉 [**新增資料內容**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="449f4-120">Click **OK** to dismiss the **New Data Context** dialog.</span></span> <span data-ttu-id="449f4-121">在 [**新增控制器**] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="449f4-121">In the **Add Controller** dialog, click **Add**.</span></span>

<span data-ttu-id="449f4-122">以下是已新增至專案的內容：</span><span class="sxs-lookup"><span data-stu-id="449f4-122">Here's what got added to the project:</span></span>

- <span data-ttu-id="449f4-123">衍生自**DbCoNtext**的類別，名為 `OrdersContext`。</span><span class="sxs-lookup"><span data-stu-id="449f4-123">A class named `OrdersContext` that derives from **DbContext**.</span></span> <span data-ttu-id="449f4-124">這個類別會提供 POCO 模型與資料庫之間的粘連。</span><span class="sxs-lookup"><span data-stu-id="449f4-124">This class provides the glue between the POCO models and the database.</span></span>
- <span data-ttu-id="449f4-125">名為 `AdminController`的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="449f4-125">A Web API controller named `AdminController`.</span></span> <span data-ttu-id="449f4-126">此控制器支援 `Product` 實例上的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="449f4-126">This controller supports CRUD operations on `Product` instances.</span></span> <span data-ttu-id="449f4-127">它會使用 `OrdersContext` 類別來與 Entity Framework 通訊。</span><span class="sxs-lookup"><span data-stu-id="449f4-127">It uses the `OrdersContext` class to communicate with Entity Framework.</span></span>
- <span data-ttu-id="449f4-128">Web.config 檔案中的新資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="449f4-128">A new database connection string in the Web.config file.</span></span>

![](using-web-api-with-entity-framework-part-3/_static/image4.png)

<span data-ttu-id="449f4-129">開啟 OrdersCoNtext.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="449f4-129">Open the OrdersContext.cs file.</span></span> <span data-ttu-id="449f4-130">請注意，此函式會指定資料庫連接字串的名稱。</span><span class="sxs-lookup"><span data-stu-id="449f4-130">Notice that the constructor specifies the name of the database connection string.</span></span> <span data-ttu-id="449f4-131">這個名稱會參考已加入至 web.config 的連接字串。</span><span class="sxs-lookup"><span data-stu-id="449f4-131">This name refers to the connection string that was added to Web.config.</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample1.cs)]

<span data-ttu-id="449f4-132">將下列屬性新增至 `OrdersContext` 類別：</span><span class="sxs-lookup"><span data-stu-id="449f4-132">Add the following properties to the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample2.cs)]

<span data-ttu-id="449f4-133">**DbSet**代表一組可以查詢的實體。</span><span class="sxs-lookup"><span data-stu-id="449f4-133">A **DbSet** represents a set of entities that can be queried.</span></span> <span data-ttu-id="449f4-134">以下是 `OrdersContext` 類別的完整清單：</span><span class="sxs-lookup"><span data-stu-id="449f4-134">Here is the complete listing for the `OrdersContext` class:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample3.cs)]

<span data-ttu-id="449f4-135">`AdminController` 類別會定義用來執行基本 CRUD 功能的五種方法。</span><span class="sxs-lookup"><span data-stu-id="449f4-135">The `AdminController` class defines five methods that implement basic CRUD functionality.</span></span> <span data-ttu-id="449f4-136">每個方法都會對應至用戶端可以叫用的 URI：</span><span class="sxs-lookup"><span data-stu-id="449f4-136">Each method corresponds to a URI that the client can invoke:</span></span>

| <span data-ttu-id="449f4-137">控制器方法</span><span class="sxs-lookup"><span data-stu-id="449f4-137">Controller Method</span></span> | <span data-ttu-id="449f4-138">說明</span><span class="sxs-lookup"><span data-stu-id="449f4-138">Description</span></span> | <span data-ttu-id="449f4-139">URI</span><span class="sxs-lookup"><span data-stu-id="449f4-139">URI</span></span> | <span data-ttu-id="449f4-140">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="449f4-140">HTTP Method</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="449f4-141">GetProducts</span><span class="sxs-lookup"><span data-stu-id="449f4-141">GetProducts</span></span> | <span data-ttu-id="449f4-142">取得所有產品。</span><span class="sxs-lookup"><span data-stu-id="449f4-142">Gets all products.</span></span> | <span data-ttu-id="449f4-143">api/產品</span><span class="sxs-lookup"><span data-stu-id="449f4-143">api/products</span></span> | <span data-ttu-id="449f4-144">GET</span><span class="sxs-lookup"><span data-stu-id="449f4-144">GET</span></span> |
| <span data-ttu-id="449f4-145">GetProduct</span><span class="sxs-lookup"><span data-stu-id="449f4-145">GetProduct</span></span> | <span data-ttu-id="449f4-146">依識別碼尋找產品。</span><span class="sxs-lookup"><span data-stu-id="449f4-146">Finds a product by ID.</span></span> | <span data-ttu-id="449f4-147">api/產品/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="449f4-147">api/products/*id*</span></span> | <span data-ttu-id="449f4-148">GET</span><span class="sxs-lookup"><span data-stu-id="449f4-148">GET</span></span> |
| <span data-ttu-id="449f4-149">PutProduct</span><span class="sxs-lookup"><span data-stu-id="449f4-149">PutProduct</span></span> | <span data-ttu-id="449f4-150">更新產品。</span><span class="sxs-lookup"><span data-stu-id="449f4-150">Updates a product.</span></span> | <span data-ttu-id="449f4-151">api/產品/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="449f4-151">api/products/*id*</span></span> | <span data-ttu-id="449f4-152">PUT</span><span class="sxs-lookup"><span data-stu-id="449f4-152">PUT</span></span> |
| <span data-ttu-id="449f4-153">PostProduct</span><span class="sxs-lookup"><span data-stu-id="449f4-153">PostProduct</span></span> | <span data-ttu-id="449f4-154">建立新的產品。</span><span class="sxs-lookup"><span data-stu-id="449f4-154">Creates a new product.</span></span> | <span data-ttu-id="449f4-155">api/產品</span><span class="sxs-lookup"><span data-stu-id="449f4-155">api/products</span></span> | <span data-ttu-id="449f4-156">POST</span><span class="sxs-lookup"><span data-stu-id="449f4-156">POST</span></span> |
| <span data-ttu-id="449f4-157">DeleteProduct</span><span class="sxs-lookup"><span data-stu-id="449f4-157">DeleteProduct</span></span> | <span data-ttu-id="449f4-158">刪除產品。</span><span class="sxs-lookup"><span data-stu-id="449f4-158">Deletes a product.</span></span> | <span data-ttu-id="449f4-159">api/產品/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="449f4-159">api/products/*id*</span></span> | <span data-ttu-id="449f4-160">刪除</span><span class="sxs-lookup"><span data-stu-id="449f4-160">DELETE</span></span> |

<span data-ttu-id="449f4-161">每個方法都會呼叫 `OrdersContext` 來查詢資料庫。</span><span class="sxs-lookup"><span data-stu-id="449f4-161">Each method calls into `OrdersContext` to query the database.</span></span> <span data-ttu-id="449f4-162">修改集合（PUT、POST 和 DELETE）呼叫 `db.SaveChanges` 的方法會將變更保存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="449f4-162">The methods that modify the collection (PUT, POST, and DELETE) call `db.SaveChanges` to persist the changes to the database.</span></span> <span data-ttu-id="449f4-163">系統會針對每個 HTTP 要求建立控制器，然後加以處置，因此必須在方法傳回之前保存變更。</span><span class="sxs-lookup"><span data-stu-id="449f4-163">Controllers are created per HTTP request and then disposed, so it is necessary to persist changes before a method returns.</span></span>

## <a name="add-a-database-initializer"></a><span data-ttu-id="449f4-164">加入資料庫初始化運算式</span><span class="sxs-lookup"><span data-stu-id="449f4-164">Add a Database Initializer</span></span>

<span data-ttu-id="449f4-165">Entity Framework 有一個很好的功能，可讓您在啟動時填入資料庫，並在每次模型變更時自動重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="449f4-165">Entity Framework has a nice feature that lets you populate the database on startup, and automatically recreate the database whenever the models change.</span></span> <span data-ttu-id="449f4-166">這項功能在開發期間很有用，因為您一律會有一些測試資料，即使您變更模型也一樣。</span><span class="sxs-lookup"><span data-stu-id="449f4-166">This feature is useful during development, because you always have some test data, even if you change the models.</span></span>

<span data-ttu-id="449f4-167">在方案總管中，以滑鼠右鍵按一下 [模型] 資料夾，然後建立名為 `OrdersContextInitializer`的新類別。</span><span class="sxs-lookup"><span data-stu-id="449f4-167">In Solution Explorer, right-click the Models folder and create a new class named `OrdersContextInitializer`.</span></span> <span data-ttu-id="449f4-168">貼上下列實作方式：</span><span class="sxs-lookup"><span data-stu-id="449f4-168">Paste in the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample4.cs)]

<span data-ttu-id="449f4-169">藉由繼承自**DropCreateDatabaseIfModelChanges**類別，我們會在我們每次修改模型類別時，告訴 Entity Framework 卸載資料庫。</span><span class="sxs-lookup"><span data-stu-id="449f4-169">By inheriting from the **DropCreateDatabaseIfModelChanges** class, we are telling Entity Framework to drop the database whenever we modify the model classes.</span></span> <span data-ttu-id="449f4-170">當 Entity Framework 建立（或重新建立）資料庫時，它會呼叫**Seed**方法來填入資料表。</span><span class="sxs-lookup"><span data-stu-id="449f4-170">When Entity Framework creates (or recreates) the database, it calls the **Seed** method to populate the tables.</span></span> <span data-ttu-id="449f4-171">我們使用**種子**方法來新增一些範例產品，加上範例訂單。</span><span class="sxs-lookup"><span data-stu-id="449f4-171">We use the **Seed** method to add some example products plus an example order.</span></span>

<span data-ttu-id="449f4-172">這項功能非常適合用來測試，但請勿在生產環境中使用**DropCreateDatabaseIfModelChanges**類別，因為如果有人變更了模型類別，您可能會遺失資料。</span><span class="sxs-lookup"><span data-stu-id="449f4-172">This feature is great for testing, but don't use the **DropCreateDatabaseIfModelChanges** class in production,, because you could lose your data if someone changes a model class.</span></span>

<span data-ttu-id="449f4-173">接下來，開啟 global.asax，然後將下列程式碼新增至**應用程式\_Start**方法：</span><span class="sxs-lookup"><span data-stu-id="449f4-173">Next, open Global.asax and add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-entity-framework-part-3/samples/sample5.cs)]

## <a name="send-a-request-to-the-controller"></a><span data-ttu-id="449f4-174">將要求傳送至控制器</span><span class="sxs-lookup"><span data-stu-id="449f4-174">Send a Request to the Controller</span></span>

<span data-ttu-id="449f4-175">此時，我們尚未撰寫任何用戶端程式代碼，但您可以使用網頁瀏覽器或 HTTP 偵錯工具（例如[Fiddler](http://www.fiddler2.com/fiddler2/)）來叫用 Web API。</span><span class="sxs-lookup"><span data-stu-id="449f4-175">At this point, we haven't written any client code, but you can invoke the web API using a web browser or an HTTP debugging tool such as [Fiddler](http://www.fiddler2.com/fiddler2/).</span></span> <span data-ttu-id="449f4-176">在 Visual Studio 中，按 F5 開始進行調試。</span><span class="sxs-lookup"><span data-stu-id="449f4-176">In Visual Studio, press F5 to start debugging.</span></span> <span data-ttu-id="449f4-177">您的網頁瀏覽器將會開啟 `http://localhost:*portnum*/`，其中*portnum*是一些埠號碼。</span><span class="sxs-lookup"><span data-stu-id="449f4-177">Your web browser will open to `http://localhost:*portnum*/`, where *portnum* is some port number.</span></span>

<span data-ttu-id="449f4-178">將 HTTP 要求傳送至 "`http://localhost:*portnum*/api/admin`。</span><span class="sxs-lookup"><span data-stu-id="449f4-178">Send an HTTP request to "`http://localhost:*portnum*/api/admin`.</span></span> <span data-ttu-id="449f4-179">第一個要求可能會很慢而無法完成，因為 Entity Framework 需要建立和植入資料庫。</span><span class="sxs-lookup"><span data-stu-id="449f4-179">The first request may be slow to complete, because Entity Framework needs to create and seed the database.</span></span> <span data-ttu-id="449f4-180">回應應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="449f4-180">The response should something similar to the following:</span></span>

[!code-console[Main](using-web-api-with-entity-framework-part-3/samples/sample6.cmd)]

> [!div class="step-by-step"]
> <span data-ttu-id="449f4-181">[上一頁](using-web-api-with-entity-framework-part-2.md)
> [下一頁](using-web-api-with-entity-framework-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="449f4-181">[Previous](using-web-api-with-entity-framework-part-2.md)
[Next](using-web-api-with-entity-framework-part-4.md)</span></span>
