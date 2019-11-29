---
uid: web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
title: 在 ASP.NET Web API 1-ASP.NET 4.x 中啟用 CRUD 作業
author: MikeWasson
description: 教學課程說明如何使用 ASP.NET 4.x 的 ASP.NET Web API，在 HTTP 服務中支援 CRUD 作業。
ms.author: riande
ms.date: 01/28/2012
ms.custom: seoapril2019
ms.assetid: c125ca47-606a-4d6f-a1fc-1fc62928af93
msc.legacyurl: /web-api/overview/older-versions/creating-a-web-api-that-supports-crud-operations
msc.type: authoredcontent
ms.openlocfilehash: a096fd1c54df33b40115907a5c2517b2e3fec5b8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74600343"
---
# <a name="enabling-crud-operations-in-aspnet-web-api-1"></a><span data-ttu-id="7b46a-103">啟用 ASP.NET Web API 1 中的 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="7b46a-103">Enabling CRUD Operations in ASP.NET Web API 1</span></span>

<span data-ttu-id="7b46a-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="7b46a-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="7b46a-105">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="7b46a-105">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-Tutorial-c4761894)

> <span data-ttu-id="7b46a-106">本教學課程說明如何使用 ASP.NET 4.x 的 ASP.NET Web API，支援 HTTP 服務中的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="7b46a-106">This tutorial shows how to support CRUD operations in an HTTP service using ASP.NET Web API for ASP.NET 4.x.</span></span>
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="7b46a-107">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="7b46a-107">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="7b46a-108">Visual Studio 2012</span><span class="sxs-lookup"><span data-stu-id="7b46a-108">Visual Studio 2012</span></span>
> - <span data-ttu-id="7b46a-109">Web API 1 （也適用于 Web API 2）</span><span class="sxs-lookup"><span data-stu-id="7b46a-109">Web API 1 (also works with Web API 2)</span></span>

<span data-ttu-id="7b46a-110">CRUD 代表 &quot;建立、讀取、更新和刪除，&quot; 這四種基本資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="7b46a-110">CRUD stands for &quot;Create, Read, Update, and Delete,&quot; which are the four basic database operations.</span></span> <span data-ttu-id="7b46a-111">許多 HTTP 服務也會透過 REST 或 REST 之類的 Api 來建立 CRUD 作業的模型。</span><span class="sxs-lookup"><span data-stu-id="7b46a-111">Many HTTP services also model CRUD operations through REST or REST-like APIs.</span></span>

<span data-ttu-id="7b46a-112">在本教學課程中，您將建立一個非常簡單的 Web API 來管理產品清單。</span><span class="sxs-lookup"><span data-stu-id="7b46a-112">In this tutorial, you will build a very simple web API to manage a list of products.</span></span> <span data-ttu-id="7b46a-113">每項產品都會包含名稱、價格及類別（例如 &quot;玩具&quot; 或 &quot;硬體&quot;），加上產品識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b46a-113">Each product will contain a name, price, and category (such as &quot;toys&quot; or &quot;hardware&quot;), plus a product ID.</span></span>

<span data-ttu-id="7b46a-114">產品 API 將會公開下列方法。</span><span class="sxs-lookup"><span data-stu-id="7b46a-114">The products API will expose following methods.</span></span>

| <span data-ttu-id="7b46a-115">動作</span><span class="sxs-lookup"><span data-stu-id="7b46a-115">Action</span></span> | <span data-ttu-id="7b46a-116">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="7b46a-116">HTTP method</span></span> | <span data-ttu-id="7b46a-117">相對 URI</span><span class="sxs-lookup"><span data-stu-id="7b46a-117">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b46a-118">取得所有產品的清單</span><span class="sxs-lookup"><span data-stu-id="7b46a-118">Get a list of all products</span></span> | <span data-ttu-id="7b46a-119">GET</span><span class="sxs-lookup"><span data-stu-id="7b46a-119">GET</span></span> | <span data-ttu-id="7b46a-120">/api/products</span><span class="sxs-lookup"><span data-stu-id="7b46a-120">/api/products</span></span> |
| <span data-ttu-id="7b46a-121">依識別碼取得產品</span><span class="sxs-lookup"><span data-stu-id="7b46a-121">Get a product by ID</span></span> | <span data-ttu-id="7b46a-122">GET</span><span class="sxs-lookup"><span data-stu-id="7b46a-122">GET</span></span> | <span data-ttu-id="7b46a-123">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="7b46a-123">/api/products/*id*</span></span> |
| <span data-ttu-id="7b46a-124">依類別取得產品</span><span class="sxs-lookup"><span data-stu-id="7b46a-124">Get a product by category</span></span> | <span data-ttu-id="7b46a-125">GET</span><span class="sxs-lookup"><span data-stu-id="7b46a-125">GET</span></span> | <span data-ttu-id="7b46a-126">/api/products？ category =*category*</span><span class="sxs-lookup"><span data-stu-id="7b46a-126">/api/products?category=*category*</span></span> |
| <span data-ttu-id="7b46a-127">建立新的產品</span><span class="sxs-lookup"><span data-stu-id="7b46a-127">Create a new product</span></span> | <span data-ttu-id="7b46a-128">POST</span><span class="sxs-lookup"><span data-stu-id="7b46a-128">POST</span></span> | <span data-ttu-id="7b46a-129">/api/products</span><span class="sxs-lookup"><span data-stu-id="7b46a-129">/api/products</span></span> |
| <span data-ttu-id="7b46a-130">更新產品</span><span class="sxs-lookup"><span data-stu-id="7b46a-130">Update a product</span></span> | <span data-ttu-id="7b46a-131">PUT</span><span class="sxs-lookup"><span data-stu-id="7b46a-131">PUT</span></span> | <span data-ttu-id="7b46a-132">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="7b46a-132">/api/products/*id*</span></span> |
| <span data-ttu-id="7b46a-133">刪除產品</span><span class="sxs-lookup"><span data-stu-id="7b46a-133">Delete a product</span></span> | <span data-ttu-id="7b46a-134">Delete</span><span class="sxs-lookup"><span data-stu-id="7b46a-134">DELETE</span></span> | <span data-ttu-id="7b46a-135">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="7b46a-135">/api/products/*id*</span></span> |

<span data-ttu-id="7b46a-136">請注意，部分 Uri 會在 path 中包含產品識別碼。</span><span class="sxs-lookup"><span data-stu-id="7b46a-136">Notice that some of the URIs include the product ID in path.</span></span> <span data-ttu-id="7b46a-137">例如，若要取得識別碼為28的產品，用戶端會傳送 `http://hostname/api/products/28`的 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="7b46a-137">For example, to get the product whose ID is 28, the client sends a GET request for `http://hostname/api/products/28`.</span></span>

### <a name="resources"></a><span data-ttu-id="7b46a-138">資源</span><span class="sxs-lookup"><span data-stu-id="7b46a-138">Resources</span></span>

<span data-ttu-id="7b46a-139">產品 API 會定義兩個資源類型的 Uri：</span><span class="sxs-lookup"><span data-stu-id="7b46a-139">The products API defines URIs for two resource types:</span></span>

| <span data-ttu-id="7b46a-140">資源</span><span class="sxs-lookup"><span data-stu-id="7b46a-140">Resource</span></span> | <span data-ttu-id="7b46a-141">URI</span><span class="sxs-lookup"><span data-stu-id="7b46a-141">URI</span></span> |
| --- | --- |
| <span data-ttu-id="7b46a-142">所有產品的清單。</span><span class="sxs-lookup"><span data-stu-id="7b46a-142">The list of all the products.</span></span> | <span data-ttu-id="7b46a-143">/api/products</span><span class="sxs-lookup"><span data-stu-id="7b46a-143">/api/products</span></span> |
| <span data-ttu-id="7b46a-144">個別產品。</span><span class="sxs-lookup"><span data-stu-id="7b46a-144">An individual product.</span></span> | <span data-ttu-id="7b46a-145">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="7b46a-145">/api/products/*id*</span></span> |

### <a name="methods"></a><span data-ttu-id="7b46a-146">方法</span><span class="sxs-lookup"><span data-stu-id="7b46a-146">Methods</span></span>

<span data-ttu-id="7b46a-147">四個主要的 HTTP 方法（GET、PUT、POST 和 DELETE）可以對應至 CRUD 作業，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7b46a-147">The four main HTTP methods (GET, PUT, POST, and DELETE) can be mapped to CRUD operations as follows:</span></span>

- <span data-ttu-id="7b46a-148">GET 會在指定的 URI 上抓取資源的表示。</span><span class="sxs-lookup"><span data-stu-id="7b46a-148">GET retrieves the representation of the resource at a specified URI.</span></span> <span data-ttu-id="7b46a-149">GET 在伺服器上應該沒有任何副作用。</span><span class="sxs-lookup"><span data-stu-id="7b46a-149">GET should have no side effects on the server.</span></span>
- <span data-ttu-id="7b46a-150">PUT 會將資源更新為指定的 URI。</span><span class="sxs-lookup"><span data-stu-id="7b46a-150">PUT updates a resource at a specified URI.</span></span> <span data-ttu-id="7b46a-151">如果伺服器允許用戶端指定新的 Uri，PUT 也可以用來在指定的 URI 建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="7b46a-151">PUT can also be used to create a new resource at a specified URI, if the server allows clients to specify new URIs.</span></span> <span data-ttu-id="7b46a-152">在本教學課程中，API 將不支援透過 PUT 建立。</span><span class="sxs-lookup"><span data-stu-id="7b46a-152">For this tutorial, the API will not support creation through PUT.</span></span>
- <span data-ttu-id="7b46a-153">POST 會建立新的資源。</span><span class="sxs-lookup"><span data-stu-id="7b46a-153">POST creates a new resource.</span></span> <span data-ttu-id="7b46a-154">伺服器會指派新物件的 URI，並在回應訊息中傳回此 URI。</span><span class="sxs-lookup"><span data-stu-id="7b46a-154">The server assigns the URI for the new object and returns this URI as part of the response message.</span></span>
- <span data-ttu-id="7b46a-155">DELETE 刪除指定 URI 的資源。</span><span class="sxs-lookup"><span data-stu-id="7b46a-155">DELETE deletes a resource at a specified URI.</span></span>

<span data-ttu-id="7b46a-156">注意： PUT 方法會取代整個 product 實體。</span><span class="sxs-lookup"><span data-stu-id="7b46a-156">Note: The PUT method replaces the entire product entity.</span></span> <span data-ttu-id="7b46a-157">也就是說，用戶端預期會傳送已更新產品的完整標記法。</span><span class="sxs-lookup"><span data-stu-id="7b46a-157">That is, the client is expected to send a complete representation of the updated product.</span></span> <span data-ttu-id="7b46a-158">如果您想要支援部分更新，建議您選擇 PATCH 方法。</span><span class="sxs-lookup"><span data-stu-id="7b46a-158">If you want to support partial updates, the PATCH method is preferred.</span></span> <span data-ttu-id="7b46a-159">本教學課程不會執行修補程式。</span><span class="sxs-lookup"><span data-stu-id="7b46a-159">This tutorial does not implement PATCH.</span></span>

## <a name="create-a-new-web-api-project"></a><span data-ttu-id="7b46a-160">建立新的 Web API 專案</span><span class="sxs-lookup"><span data-stu-id="7b46a-160">Create a New Web API Project</span></span>

<span data-ttu-id="7b46a-161">從執行 Visual Studio 開始，然後從 [**開始**] 頁面選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-161">Start by running Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="7b46a-162">或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-162">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="7b46a-163">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。</span><span class="sxs-lookup"><span data-stu-id="7b46a-163">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="7b46a-164">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-164">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="7b46a-165">在專案範本清單中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-165">In the list of project templates, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="7b46a-166">將專案命名為 &quot;ProductStore&quot; 然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="7b46a-166">Name the project &quot;ProductStore&quot; and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image1.png)

<span data-ttu-id="7b46a-167">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [ **Web API** ]，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="7b46a-167">In the **New ASP.NET MVC 4 Project** dialog, select **Web API** and click **OK**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image2.png)

## <a name="adding-a-model"></a><span data-ttu-id="7b46a-168">新增模型</span><span class="sxs-lookup"><span data-stu-id="7b46a-168">Adding a Model</span></span>

<span data-ttu-id="7b46a-169">「模型」是代表應用程式中資料的物件。</span><span class="sxs-lookup"><span data-stu-id="7b46a-169">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="7b46a-170">在 ASP.NET Web API 中，您可以使用強型別 CLR 物件做為模型，而且它們會自動序列化為用戶端的 XML 或 JSON。</span><span class="sxs-lookup"><span data-stu-id="7b46a-170">In ASP.NET Web API, you can use strongly typed CLR objects as models, and they will automatically be serialized to XML or JSON for the client.</span></span>

<span data-ttu-id="7b46a-171">針對 ProductStore API，我們的資料是由產品所組成，因此我們將建立名為 `Product`的新類別。</span><span class="sxs-lookup"><span data-stu-id="7b46a-171">For the ProductStore API, our data consists of products, so we'll create a new class named `Product`.</span></span>

<span data-ttu-id="7b46a-172">如果方案總管尚未顯示，請按一下 [ **View** ] 功能表，然後選取 [**方案總管**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-172">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="7b46a-173">在方案總管中，以滑鼠右鍵按一下 [**模型**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b46a-173">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="7b46a-174">從內容功能表中，選取 [**新增**]，然後選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-174">From the context menu, select **Add**, then select **Class**.</span></span> <span data-ttu-id="7b46a-175">將類別命名為 &quot;產品&quot;。</span><span class="sxs-lookup"><span data-stu-id="7b46a-175">Name the class &quot;Product&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image3.png)

<span data-ttu-id="7b46a-176">將下列屬性新增至 `Product` 類別。</span><span class="sxs-lookup"><span data-stu-id="7b46a-176">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample1.cs)]

## <a name="adding-a-repository"></a><span data-ttu-id="7b46a-177">加入儲存機制</span><span class="sxs-lookup"><span data-stu-id="7b46a-177">Adding a Repository</span></span>

<span data-ttu-id="7b46a-178">我們需要儲存一系列產品。</span><span class="sxs-lookup"><span data-stu-id="7b46a-178">We need to store a collection of products.</span></span> <span data-ttu-id="7b46a-179">將集合與我們的服務實作為區隔是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="7b46a-179">It's a good idea to separate the collection from our service implementation.</span></span> <span data-ttu-id="7b46a-180">如此一來，我們就可以變更備份存放區，而不需要重寫服務類別。</span><span class="sxs-lookup"><span data-stu-id="7b46a-180">That way, we can change the backing store without rewriting the service class.</span></span> <span data-ttu-id="7b46a-181">這種設計稱為「*儲存*機制」模式。</span><span class="sxs-lookup"><span data-stu-id="7b46a-181">This type of design is called the *repository* pattern.</span></span> <span data-ttu-id="7b46a-182">一開始請先定義存放庫的泛型介面。</span><span class="sxs-lookup"><span data-stu-id="7b46a-182">Start by defining a generic interface for the repository.</span></span>

<span data-ttu-id="7b46a-183">在方案總管中，以滑鼠右鍵按一下 [**模型**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b46a-183">In Solution Explorer, right-click the **Models** folder.</span></span> <span data-ttu-id="7b46a-184">選取 [**加入**]，然後選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-184">Select **Add**, then select **New Item**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image4.png)

<span data-ttu-id="7b46a-185">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開C#節點。</span><span class="sxs-lookup"><span data-stu-id="7b46a-185">In the **Templates** pane, select **Installed Templates** and expand the C# node.</span></span> <span data-ttu-id="7b46a-186">在C#底下選取 [程式**代碼**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-186">Under C#, select **Code**.</span></span> <span data-ttu-id="7b46a-187">在程式碼範本清單中，選取 [**介面**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-187">In the list of code templates, select **Interface**.</span></span> <span data-ttu-id="7b46a-188">將介面命名 &quot;IProductRepository&quot;。</span><span class="sxs-lookup"><span data-stu-id="7b46a-188">Name the interface &quot;IProductRepository&quot;.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image5.png)

<span data-ttu-id="7b46a-189">新增下列執行：</span><span class="sxs-lookup"><span data-stu-id="7b46a-189">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample2.cs)]

<span data-ttu-id="7b46a-190">現在將另一個類別新增至 [模型] 資料夾，名為 &quot;ProductRepository。&quot; 這個類別將會執行 `IProductRepository` 介面。</span><span class="sxs-lookup"><span data-stu-id="7b46a-190">Now add another class to the Models folder, named &quot;ProductRepository.&quot; This class will implement the `IProductRepository` interface.</span></span> <span data-ttu-id="7b46a-191">新增下列執行：</span><span class="sxs-lookup"><span data-stu-id="7b46a-191">Add the following implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample3.cs)]

<span data-ttu-id="7b46a-192">存放庫會將清單保留在本機記憶體中。</span><span class="sxs-lookup"><span data-stu-id="7b46a-192">The repository keeps the list in local memory.</span></span> <span data-ttu-id="7b46a-193">這在教學課程中是正常的，但在實際的應用程式中，您會將資料儲存在外部，也就是資料庫或雲端儲存體。</span><span class="sxs-lookup"><span data-stu-id="7b46a-193">This is OK for a tutorial, but in a real application, you would store the data externally, either a database or in cloud storage.</span></span> <span data-ttu-id="7b46a-194">儲存機制模式可讓您稍後更輕鬆地變更執行。</span><span class="sxs-lookup"><span data-stu-id="7b46a-194">The repository pattern will make it easier to change the implementation later.</span></span>

## <a name="adding-a-web-api-controller"></a><span data-ttu-id="7b46a-195">新增 Web API 控制器</span><span class="sxs-lookup"><span data-stu-id="7b46a-195">Adding a Web API Controller</span></span>

<span data-ttu-id="7b46a-196">如果您曾經使用過 ASP.NET MVC，則您已經熟悉控制器。</span><span class="sxs-lookup"><span data-stu-id="7b46a-196">If you have worked with ASP.NET MVC, then you are already familiar with controllers.</span></span> <span data-ttu-id="7b46a-197">在 ASP.NET Web API 中，*控制器*是處理來自用戶端之 HTTP 要求的類別。</span><span class="sxs-lookup"><span data-stu-id="7b46a-197">In ASP.NET Web API, a *controller* is a class that handles HTTP requests from the client.</span></span> <span data-ttu-id="7b46a-198">[新增專案] wizard 會在建立專案時，為您建立兩個控制器。</span><span class="sxs-lookup"><span data-stu-id="7b46a-198">The New Project wizard created two controllers for you when it created the project.</span></span> <span data-ttu-id="7b46a-199">若要查看它們，請展開方案總管中的 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b46a-199">To see them, expand the Controllers folder in Solution Explorer.</span></span>

- <span data-ttu-id="7b46a-200">HomeController 是傳統的 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="7b46a-200">HomeController is a traditional ASP.NET MVC controller.</span></span> <span data-ttu-id="7b46a-201">它負責為網站提供 HTML 網頁，而不是與我們的 Web API 直接相關。</span><span class="sxs-lookup"><span data-stu-id="7b46a-201">It is responsible for serving HTML pages for the site, and is not directly related to our web API.</span></span>
- <span data-ttu-id="7b46a-202">ValuesController 是 WebAPI 控制器的範例。</span><span class="sxs-lookup"><span data-stu-id="7b46a-202">ValuesController is an example WebAPI controller.</span></span>

<span data-ttu-id="7b46a-203">繼續並刪除 ValuesController，方法是以滑鼠右鍵按一下方案總管中的檔案，然後選取 [**刪除]。**</span><span class="sxs-lookup"><span data-stu-id="7b46a-203">Go ahead and delete ValuesController, by right-clicking the file in Solution Explorer and selecting **Delete.**</span></span> <span data-ttu-id="7b46a-204">現在加入新的控制器，如下所示：</span><span class="sxs-lookup"><span data-stu-id="7b46a-204">Now add a new controller, as follows:</span></span>

<span data-ttu-id="7b46a-205">在**方案總管**中，以滑鼠右鍵按一下 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b46a-205">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="7b46a-206">選取 [**新增**]，然後選取 [**控制器**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-206">Select **Add** and then select **Controller**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image6.png)

<span data-ttu-id="7b46a-207">在 [**新增控制器**嚮導] 中，將控制器命名為 &quot;productscontroller.cs&quot;。</span><span class="sxs-lookup"><span data-stu-id="7b46a-207">In the **Add Controller** wizard, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="7b46a-208">在 [**範本**] 下拉式清單中，選取 [**空的 API 控制器**]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-208">In the **Template** drop-down list, select **Empty API Controller**.</span></span> <span data-ttu-id="7b46a-209">然後按一下 [加入]。</span><span class="sxs-lookup"><span data-stu-id="7b46a-209">Then click **Add**.</span></span>

![](creating-a-web-api-that-supports-crud-operations/_static/image7.png)

> [!NOTE]
> <span data-ttu-id="7b46a-210">您不需要將控制器放入名為 [控制器] 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="7b46a-210">It is not necessary to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="7b46a-211">資料夾名稱並不重要;這只是一個方便的方式來組織您的來源檔案。</span><span class="sxs-lookup"><span data-stu-id="7b46a-211">The folder name is not important; it is simply a convenient way to organize your source files.</span></span>

<span data-ttu-id="7b46a-212">「**新增控制器**」 wizard 會在 [控制器] 資料夾中建立名為 ProductsController.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="7b46a-212">The **Add Controller** wizard will create a file named ProductsController.cs in the Controllers folder.</span></span> <span data-ttu-id="7b46a-213">如果此檔案尚未開啟，請按兩下檔案將其開啟。</span><span class="sxs-lookup"><span data-stu-id="7b46a-213">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="7b46a-214">新增下列**using**語句：</span><span class="sxs-lookup"><span data-stu-id="7b46a-214">Add the following **using** statement:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample4.cs)]

<span data-ttu-id="7b46a-215">新增保存**IProductRepository**實例的欄位。</span><span class="sxs-lookup"><span data-stu-id="7b46a-215">Add a field that holds an **IProductRepository** instance.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample5.cs)]

> [!NOTE]
> <span data-ttu-id="7b46a-216">在控制器中呼叫 `new ProductRepository()` 並不是最佳設計，因為它會將控制器系結至特定的 `IProductRepository`執行。</span><span class="sxs-lookup"><span data-stu-id="7b46a-216">Calling `new ProductRepository()` in the controller is not the best design, because it ties the controller to a particular implementation of `IProductRepository`.</span></span> <span data-ttu-id="7b46a-217">如需更好的方法，請參閱[使用 WEB API 相依性解析程式](../advanced/dependency-injection.md)。</span><span class="sxs-lookup"><span data-stu-id="7b46a-217">For a better approach, see [Using the Web API Dependency Resolver](../advanced/dependency-injection.md).</span></span>

## <a name="getting-a-resource"></a><span data-ttu-id="7b46a-218">取得資源</span><span class="sxs-lookup"><span data-stu-id="7b46a-218">Getting a Resource</span></span>

<span data-ttu-id="7b46a-219">ProductStore API 會公開數個 &quot;讀取&quot; 動作作為 HTTP GET 方法。</span><span class="sxs-lookup"><span data-stu-id="7b46a-219">The ProductStore API will expose several &quot;read&quot; actions as HTTP GET methods.</span></span> <span data-ttu-id="7b46a-220">每個動作都會對應至 `ProductsController` 類別中的方法。</span><span class="sxs-lookup"><span data-stu-id="7b46a-220">Each action will correspond to a method in the `ProductsController` class.</span></span>

| <span data-ttu-id="7b46a-221">動作</span><span class="sxs-lookup"><span data-stu-id="7b46a-221">Action</span></span> | <span data-ttu-id="7b46a-222">HTTP 方法</span><span class="sxs-lookup"><span data-stu-id="7b46a-222">HTTP method</span></span> | <span data-ttu-id="7b46a-223">相對 URI</span><span class="sxs-lookup"><span data-stu-id="7b46a-223">Relative URI</span></span> |
| --- | --- | --- |
| <span data-ttu-id="7b46a-224">取得所有產品的清單</span><span class="sxs-lookup"><span data-stu-id="7b46a-224">Get a list of all products</span></span> | <span data-ttu-id="7b46a-225">GET</span><span class="sxs-lookup"><span data-stu-id="7b46a-225">GET</span></span> | <span data-ttu-id="7b46a-226">/api/products</span><span class="sxs-lookup"><span data-stu-id="7b46a-226">/api/products</span></span> |
| <span data-ttu-id="7b46a-227">依識別碼取得產品</span><span class="sxs-lookup"><span data-stu-id="7b46a-227">Get a product by ID</span></span> | <span data-ttu-id="7b46a-228">GET</span><span class="sxs-lookup"><span data-stu-id="7b46a-228">GET</span></span> | <span data-ttu-id="7b46a-229">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="7b46a-229">/api/products/*id*</span></span> |
| <span data-ttu-id="7b46a-230">依類別取得產品</span><span class="sxs-lookup"><span data-stu-id="7b46a-230">Get a product by category</span></span> | <span data-ttu-id="7b46a-231">GET</span><span class="sxs-lookup"><span data-stu-id="7b46a-231">GET</span></span> | <span data-ttu-id="7b46a-232">/api/products？ category =*category*</span><span class="sxs-lookup"><span data-stu-id="7b46a-232">/api/products?category=*category*</span></span> |

<span data-ttu-id="7b46a-233">若要取得所有產品的清單，請將下列方法新增至 `ProductsController` 類別：</span><span class="sxs-lookup"><span data-stu-id="7b46a-233">To get the list of all products, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample6.cs)]

<span data-ttu-id="7b46a-234">方法名稱的開頭為 &quot;取得&quot;，因此依照慣例，它會對應至 GET 要求。</span><span class="sxs-lookup"><span data-stu-id="7b46a-234">The method name starts with &quot;Get&quot;, so by convention it maps to GET requests.</span></span> <span data-ttu-id="7b46a-235">此外，因為方法沒有參數，所以它會對應到路徑中不包含 *&quot;識別碼&quot;* 區段的 URI。</span><span class="sxs-lookup"><span data-stu-id="7b46a-235">Also, because the method has no parameters, it maps to a URI that does not contain an *&quot;id&quot;* segment in the path.</span></span>

<span data-ttu-id="7b46a-236">若要依識別碼取得產品，請將下列方法新增至 `ProductsController` 類別：</span><span class="sxs-lookup"><span data-stu-id="7b46a-236">To get a product by ID, add this method to the `ProductsController` class:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample7.cs)]

<span data-ttu-id="7b46a-237">這個方法名稱也是以 &quot;Get&quot;開頭，但方法具有名為*id*的參數。這個參數會對應至 URI 路徑的 &quot;識別碼&quot; 區段。</span><span class="sxs-lookup"><span data-stu-id="7b46a-237">This method name also starts with &quot;Get&quot;, but the method has a parameter named *id*. This parameter is mapped to the &quot;id&quot; segment of the URI path.</span></span> <span data-ttu-id="7b46a-238">ASP.NET Web API 架構會自動將識別碼轉換為參數的正確資料類型（**int**）。</span><span class="sxs-lookup"><span data-stu-id="7b46a-238">The ASP.NET Web API framework automatically converts the ID to the correct data type (**int**) for the parameter.</span></span>

<span data-ttu-id="7b46a-239">如果*識別碼*無效，GetProduct 方法會擲回**HttpResponseException**類型的例外狀況。</span><span class="sxs-lookup"><span data-stu-id="7b46a-239">The GetProduct method throws an exception of type **HttpResponseException** if *id* is not valid.</span></span> <span data-ttu-id="7b46a-240">架構會將此例外狀況轉譯為404（找不到）錯誤。</span><span class="sxs-lookup"><span data-stu-id="7b46a-240">This exception will be translated by the framework into a 404 (Not Found) error.</span></span>

<span data-ttu-id="7b46a-241">最後，新增方法以依類別尋找產品：</span><span class="sxs-lookup"><span data-stu-id="7b46a-241">Finally, add a method to find products by category:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample8.cs)]

<span data-ttu-id="7b46a-242">如果要求 URI 有查詢字串，Web API 會嘗試將查詢參數與控制器方法上的參數比對。</span><span class="sxs-lookup"><span data-stu-id="7b46a-242">If the request URI has a query string, Web API tries to match the query parameters to parameters on the controller method.</span></span> <span data-ttu-id="7b46a-243">因此，"api/products？ category =*category*" 格式的 URI 會對應至此方法。</span><span class="sxs-lookup"><span data-stu-id="7b46a-243">Therefore, a URI of the form "api/products?category=*category*" will map to this method.</span></span>

## <a name="creating-a-resource"></a><span data-ttu-id="7b46a-244">建立資源</span><span class="sxs-lookup"><span data-stu-id="7b46a-244">Creating a Resource</span></span>

<span data-ttu-id="7b46a-245">接下來，我們會將方法新增至 `ProductsController` 類別，以建立新的產品。</span><span class="sxs-lookup"><span data-stu-id="7b46a-245">Next, we'll add a method to the `ProductsController` class to create a new product.</span></span> <span data-ttu-id="7b46a-246">以下是方法的簡單執行：</span><span class="sxs-lookup"><span data-stu-id="7b46a-246">Here is a simple implementation of the method:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample9.cs)]

<span data-ttu-id="7b46a-247">請注意這種方法的兩個相關事項：</span><span class="sxs-lookup"><span data-stu-id="7b46a-247">Note two things about this method:</span></span>

- <span data-ttu-id="7b46a-248">方法名稱是以 &quot;Post ...&quot;開頭。</span><span class="sxs-lookup"><span data-stu-id="7b46a-248">The method name starts with &quot;Post...&quot;.</span></span> <span data-ttu-id="7b46a-249">若要建立新的產品，用戶端會傳送 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="7b46a-249">To create a new product, the client sends an HTTP POST request.</span></span>
- <span data-ttu-id="7b46a-250">方法會使用產品類型的參數。</span><span class="sxs-lookup"><span data-stu-id="7b46a-250">The method takes a parameter of type Product.</span></span> <span data-ttu-id="7b46a-251">在 Web API 中，具有複雜類型的參數會從要求主體還原序列化。</span><span class="sxs-lookup"><span data-stu-id="7b46a-251">In Web API, parameters with complex types are deserialized from the request body.</span></span> <span data-ttu-id="7b46a-252">因此，我們預期用戶端會以 XML 或 JSON 格式傳送產品物件的序列化標記法。</span><span class="sxs-lookup"><span data-stu-id="7b46a-252">Therefore, we expect the client to send a serialized representation of a product object, in either XML or JSON format.</span></span>

<span data-ttu-id="7b46a-253">此實作為可行的，但不是完全一樣。</span><span class="sxs-lookup"><span data-stu-id="7b46a-253">This implementation will work, but it is not quite complete.</span></span> <span data-ttu-id="7b46a-254">在理想的情況下，我們希望 HTTP 回應包含下列內容：</span><span class="sxs-lookup"><span data-stu-id="7b46a-254">Ideally, we would like the HTTP response to include the following:</span></span>

- <span data-ttu-id="7b46a-255">**回應碼：** 根據預設，Web API 架構會將回應狀態碼設定為200（確定）。</span><span class="sxs-lookup"><span data-stu-id="7b46a-255">**Response code:** By default, the Web API framework sets the response status code to 200 (OK).</span></span> <span data-ttu-id="7b46a-256">但是根據 HTTP/1.1 通訊協定，當 POST 要求導致資源的建立時，伺服器應該會回復狀態201（已建立）。</span><span class="sxs-lookup"><span data-stu-id="7b46a-256">But according to the HTTP/1.1 protocol, when a POST request results in the creation of a resource, the server should reply with status 201 (Created).</span></span>
- <span data-ttu-id="7b46a-257">**位置：** 當伺服器建立資源時，它應該在回應的位置標頭中包含新資源的 URI。</span><span class="sxs-lookup"><span data-stu-id="7b46a-257">**Location:** When the server creates a resource, it should include the URI of the new resource in the Location header of the response.</span></span>

<span data-ttu-id="7b46a-258">ASP.NET Web API 可讓您輕鬆地操作 HTTP 回應訊息。</span><span class="sxs-lookup"><span data-stu-id="7b46a-258">ASP.NET Web API makes it easy to manipulate the HTTP response message.</span></span> <span data-ttu-id="7b46a-259">以下是改良的執行：</span><span class="sxs-lookup"><span data-stu-id="7b46a-259">Here is the improved implementation:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample10.cs)]

<span data-ttu-id="7b46a-260">請注意，方法傳回類型現在是**HttpResponseMessage**。</span><span class="sxs-lookup"><span data-stu-id="7b46a-260">Notice that the method return type is now **HttpResponseMessage**.</span></span> <span data-ttu-id="7b46a-261">藉由傳回**HttpResponseMessage**而不是產品，我們可以控制 HTTP 回應訊息的詳細資料，包括狀態碼和位置標頭。</span><span class="sxs-lookup"><span data-stu-id="7b46a-261">By returning an **HttpResponseMessage** instead of a Product, we can control the details of the HTTP response message, including the status code and the Location header.</span></span>

<span data-ttu-id="7b46a-262">**CreateResponse**方法會建立**HttpResponseMessage** ，並自動將產品物件的序列化表示寫入回應訊息的本文中。</span><span class="sxs-lookup"><span data-stu-id="7b46a-262">The **CreateResponse** method creates an **HttpResponseMessage** and automatically writes a serialized representation of the Product object into the body fo the response message.</span></span>

> [!NOTE]
> <span data-ttu-id="7b46a-263">這個範例不會驗證 `Product`。</span><span class="sxs-lookup"><span data-stu-id="7b46a-263">This example does not validate the `Product`.</span></span> <span data-ttu-id="7b46a-264">如需模型驗證的相關資訊，請參閱[ASP.NET Web API 中的模型驗證](../formats-and-model-binding/model-validation-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="7b46a-264">For information about model validation, see [Model Validation in ASP.NET Web API](../formats-and-model-binding/model-validation-in-aspnet-web-api.md).</span></span>

## <a name="updating-a-resource"></a><span data-ttu-id="7b46a-265">更新資源</span><span class="sxs-lookup"><span data-stu-id="7b46a-265">Updating a Resource</span></span>

<span data-ttu-id="7b46a-266">使用 PUT 來更新產品非常簡單：</span><span class="sxs-lookup"><span data-stu-id="7b46a-266">Updating a product with PUT is straightforward:</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample11.cs)]

<span data-ttu-id="7b46a-267">方法名稱是以 &quot;Put ...&quot;開頭，因此 Web API 會與它相符以提出要求。</span><span class="sxs-lookup"><span data-stu-id="7b46a-267">The method name starts with &quot;Put...&quot;, so Web API matches it to PUT requests.</span></span> <span data-ttu-id="7b46a-268">方法會採用兩個參數：產品識別碼和更新的產品。</span><span class="sxs-lookup"><span data-stu-id="7b46a-268">The method takes two parameters, the product ID and the updated product.</span></span> <span data-ttu-id="7b46a-269">*識別碼*參數取自 URI 路徑，而*product*參數則會從要求主體還原序列化。</span><span class="sxs-lookup"><span data-stu-id="7b46a-269">The *id* parameter is taken from the URI path, and the *product* parameter is deserialized from the request body.</span></span> <span data-ttu-id="7b46a-270">根據預設，ASP.NET Web API 架構會從要求主體中的路由和複雜類型取得簡單的參數類型。</span><span class="sxs-lookup"><span data-stu-id="7b46a-270">By default, the ASP.NET Web API framework takes simple parameter types from the route and complex types from the request body.</span></span>

## <a name="deleting-a-resource"></a><span data-ttu-id="7b46a-271">刪除資源</span><span class="sxs-lookup"><span data-stu-id="7b46a-271">Deleting a Resource</span></span>

<span data-ttu-id="7b46a-272">若要刪除資源，請定義「刪除 ...」方法.</span><span class="sxs-lookup"><span data-stu-id="7b46a-272">To delete a resource, define a "Delete..." method.</span></span>

[!code-csharp[Main](creating-a-web-api-that-supports-crud-operations/samples/sample12.cs)]

<span data-ttu-id="7b46a-273">如果 DELETE 要求成功，它會傳回狀態200（確定）與描述狀態的實體主體。狀態202（已接受），如果刪除仍待決;或沒有實體主體的狀態204（沒有內容）。</span><span class="sxs-lookup"><span data-stu-id="7b46a-273">If a DELETE request succeeds, it can return status 200 (OK) with an entity-body that describes the status; status 202 (Accepted) if the deletion is still pending; or status 204 (No Content) with no entity body.</span></span> <span data-ttu-id="7b46a-274">在此情況下，`DeleteProduct` 方法會有 `void` 傳回型別，因此 ASP.NET Web API 會自動將此轉譯為狀態碼204（沒有內容）。</span><span class="sxs-lookup"><span data-stu-id="7b46a-274">In this case, the `DeleteProduct` method has a `void` return type, so ASP.NET Web API automatically translates this into status code 204 (No Content).</span></span>
