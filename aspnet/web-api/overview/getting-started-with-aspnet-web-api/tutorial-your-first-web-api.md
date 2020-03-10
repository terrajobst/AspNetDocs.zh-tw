---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: 開始使用 ASP.NET Web API 2 （C#）-ASP.NET 4。x
author: MikeWasson
description: 教學課程與程式碼。 使用 ASP.NET Web API 建立可傳回產品清單的 Web API。
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556795"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="39a48-104">開始使用 ASP.NET Web API 2 （C#）</span><span class="sxs-lookup"><span data-stu-id="39a48-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="39a48-105">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="39a48-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="39a48-106">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="39a48-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="39a48-107">在本教學課程中，您將使用 ASP.NET Web API 來建立可傳回產品清單的 Web API。</span><span class="sxs-lookup"><span data-stu-id="39a48-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="39a48-108">HTTP 並不只是用來提供網頁。</span><span class="sxs-lookup"><span data-stu-id="39a48-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="39a48-109">HTTP 也是一個功能強大的平臺，可用於建立公開服務和資料的 Api。</span><span class="sxs-lookup"><span data-stu-id="39a48-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="39a48-110">HTTP 既簡單、有彈性，而且十分普遍。</span><span class="sxs-lookup"><span data-stu-id="39a48-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="39a48-111">幾乎任何您可以想到的平臺都有 HTTP 程式庫，因此 HTTP 服務可以連線到各種用戶端，包括瀏覽器、行動裝置和傳統桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="39a48-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="39a48-112">ASP.NET Web API 是在 .NET Framework 之上建立 Web Api 的架構。</span><span class="sxs-lookup"><span data-stu-id="39a48-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="39a48-113">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="39a48-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="39a48-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="39a48-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="39a48-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="39a48-115">Web API 2</span></span>

<span data-ttu-id="39a48-116">如需本教學課程的較新版本，請參閱[使用適用于 Windows 的 ASP.NET Core 和 Visual Studio 建立 Web API](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) 。</span><span class="sxs-lookup"><span data-stu-id="39a48-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="39a48-117">建立 Web API 專案</span><span class="sxs-lookup"><span data-stu-id="39a48-117">Create a Web API Project</span></span>

<span data-ttu-id="39a48-118">在本教學課程中，您將使用 ASP.NET Web API 來建立可傳回產品清單的 Web API。</span><span class="sxs-lookup"><span data-stu-id="39a48-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="39a48-119">前端網頁會使用 jQuery 來顯示結果。</span><span class="sxs-lookup"><span data-stu-id="39a48-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="39a48-120">啟動 Visual Studio，然後從 [**開始**] 頁面選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="39a48-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="39a48-121">或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="39a48-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="39a48-122">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。</span><span class="sxs-lookup"><span data-stu-id="39a48-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="39a48-123">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="39a48-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="39a48-124">在專案範本清單中，選取 [ **ASP.NET Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="39a48-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="39a48-125">將專案命名為 "ProductsApp"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="39a48-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="39a48-126">在 [**新增 ASP.NET 專案**] 對話方塊中，選取 [**空白**] 範本。</span><span class="sxs-lookup"><span data-stu-id="39a48-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="39a48-127">在 [&quot;新增&quot;的資料夾和核心參考] 底下，檢查 [ **WEB API**]。</span><span class="sxs-lookup"><span data-stu-id="39a48-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="39a48-128">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="39a48-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="39a48-129">您也可以使用 &quot;Web API&quot; 範本來建立 Web API 專案。</span><span class="sxs-lookup"><span data-stu-id="39a48-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="39a48-130">Web API 範本會使用 ASP.NET MVC 來提供 API 說明頁面。</span><span class="sxs-lookup"><span data-stu-id="39a48-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="39a48-131">我在本教學課程中使用空白範本，因為我想要顯示不含 MVC 的 Web API。</span><span class="sxs-lookup"><span data-stu-id="39a48-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="39a48-132">一般來說，您不需要知道 ASP.NET MVC 就能使用 Web API。</span><span class="sxs-lookup"><span data-stu-id="39a48-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="39a48-133">新增模型</span><span class="sxs-lookup"><span data-stu-id="39a48-133">Adding a Model</span></span>

<span data-ttu-id="39a48-134">「模型」是代表應用程式中資料的物件。</span><span class="sxs-lookup"><span data-stu-id="39a48-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="39a48-135">ASP.NET Web API 可以自動將您的模型序列化為 JSON、XML 或其他格式，然後將序列化資料寫入 HTTP 回應訊息的本文中。</span><span class="sxs-lookup"><span data-stu-id="39a48-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="39a48-136">只要用戶端可以讀取序列化格式，它就可以還原序列化物件。</span><span class="sxs-lookup"><span data-stu-id="39a48-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="39a48-137">大部分的用戶端都可以剖析 XML 或 JSON。</span><span class="sxs-lookup"><span data-stu-id="39a48-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="39a48-138">此外，用戶端可以藉由設定 HTTP 要求訊息中的 Accept 標頭，來指出所要的格式。</span><span class="sxs-lookup"><span data-stu-id="39a48-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="39a48-139">讓我們從建立代表產品的簡單模型開始。</span><span class="sxs-lookup"><span data-stu-id="39a48-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="39a48-140">如果沒有顯示 [方案總管]，請按一下 [檢視] 功能表，然後選取 [方案總管]。</span><span class="sxs-lookup"><span data-stu-id="39a48-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="39a48-141">在 [方案總管] 中，於 Models 資料夾上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="39a48-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="39a48-142">從操作功能表中，選取 [新增]，然後選取 [類別]。</span><span class="sxs-lookup"><span data-stu-id="39a48-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="39a48-143">將類別命名為 &quot;產品&quot;。</span><span class="sxs-lookup"><span data-stu-id="39a48-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="39a48-144">將下列屬性新增至 `Product` 類別。</span><span class="sxs-lookup"><span data-stu-id="39a48-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="39a48-145">新增控制器</span><span class="sxs-lookup"><span data-stu-id="39a48-145">Adding a Controller</span></span>

<span data-ttu-id="39a48-146">在 Web API 中，*控制器*是處理 HTTP 要求的物件。</span><span class="sxs-lookup"><span data-stu-id="39a48-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="39a48-147">我們會新增可傳回產品清單的控制器，或由識別碼所指定的單一產品。</span><span class="sxs-lookup"><span data-stu-id="39a48-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="39a48-148">如果您已使用 ASP.NET MVC，則您已經熟悉控制器。</span><span class="sxs-lookup"><span data-stu-id="39a48-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="39a48-149">Web API 控制器類似于 MVC 控制器，但會繼承**ApiController**類別，而不是**控制器**類別。</span><span class="sxs-lookup"><span data-stu-id="39a48-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="39a48-150">在 [方案總管] 中，於 Controllers 資料夾上按一下滑鼠右鍵。</span><span class="sxs-lookup"><span data-stu-id="39a48-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="39a48-151">選取 [新增]，然後選取 [控制器]。</span><span class="sxs-lookup"><span data-stu-id="39a48-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="39a48-152">在 [新增 Scaffold] 對話方塊中，選取 [Web API 控制器 - 空白]。</span><span class="sxs-lookup"><span data-stu-id="39a48-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="39a48-153">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="39a48-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="39a48-154">在 [**新增控制器**] 對話方塊中，將控制器命名為 &quot;productscontroller.cs&quot;。</span><span class="sxs-lookup"><span data-stu-id="39a48-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="39a48-155">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="39a48-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="39a48-156">此樣板會在 [控制器] 資料夾中建立名為 ProductsController.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="39a48-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="39a48-157">您不需要將控制器放入名為 [控制器] 的資料夾。</span><span class="sxs-lookup"><span data-stu-id="39a48-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="39a48-158">資料夾名稱只是組織原始程式檔的便利方式。</span><span class="sxs-lookup"><span data-stu-id="39a48-158">The folder name is just a convenient way to organize your source files.</span></span>

<span data-ttu-id="39a48-159">如果此檔案尚未開啟，請按兩下檔案將它開啟。</span><span class="sxs-lookup"><span data-stu-id="39a48-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="39a48-160">將此檔案中的程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="39a48-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="39a48-161">為了讓範例保持簡單，產品會儲存在控制器類別內的固定陣列中。</span><span class="sxs-lookup"><span data-stu-id="39a48-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="39a48-162">當然，在實際的應用程式中，您會查詢資料庫或使用其他外部資料源。</span><span class="sxs-lookup"><span data-stu-id="39a48-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="39a48-163">控制器會定義兩個傳回產品的方法：</span><span class="sxs-lookup"><span data-stu-id="39a48-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="39a48-164">`GetAllProducts` 方法會傳回完整的產品清單，做為**IEnumerable&lt;產品&gt;** 類型。</span><span class="sxs-lookup"><span data-stu-id="39a48-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="39a48-165">`GetProduct` 方法會依識別碼查閱單一產品。</span><span class="sxs-lookup"><span data-stu-id="39a48-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="39a48-166">就這麼容易！</span><span class="sxs-lookup"><span data-stu-id="39a48-166">That's it!</span></span> <span data-ttu-id="39a48-167">您有一個可運作的 Web API。</span><span class="sxs-lookup"><span data-stu-id="39a48-167">You have a working web API.</span></span> <span data-ttu-id="39a48-168">控制器上的每個方法都會對應至一或多個 Uri：</span><span class="sxs-lookup"><span data-stu-id="39a48-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="39a48-169">控制器方法</span><span class="sxs-lookup"><span data-stu-id="39a48-169">Controller Method</span></span> | <span data-ttu-id="39a48-170">URI</span><span class="sxs-lookup"><span data-stu-id="39a48-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="39a48-171">Getallproductswithcategories</span><span class="sxs-lookup"><span data-stu-id="39a48-171">GetAllProducts</span></span> | <span data-ttu-id="39a48-172">/api/products</span><span class="sxs-lookup"><span data-stu-id="39a48-172">/api/products</span></span> |
| <span data-ttu-id="39a48-173">GetProduct</span><span class="sxs-lookup"><span data-stu-id="39a48-173">GetProduct</span></span> | <span data-ttu-id="39a48-174">/api/products/*識別碼*</span><span class="sxs-lookup"><span data-stu-id="39a48-174">/api/products/*id*</span></span> |

<span data-ttu-id="39a48-175">針對 `GetProduct` 方法，URI 中的*識別碼*是預留位置。</span><span class="sxs-lookup"><span data-stu-id="39a48-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="39a48-176">例如，若要取得識別碼為5的產品，則 URI 為 `api/products/5`。</span><span class="sxs-lookup"><span data-stu-id="39a48-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="39a48-177">如需 Web API 如何將 HTTP 要求路由傳送至控制器方法的詳細資訊，請參閱[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="39a48-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="39a48-178">使用 JAVAscript 和 jQuery 呼叫 Web API</span><span class="sxs-lookup"><span data-stu-id="39a48-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="39a48-179">在本節中，我們將新增使用 AJAX 呼叫 Web API 的 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="39a48-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="39a48-180">我們將使用 jQuery 來進行 AJAX 呼叫，並以結果更新頁面。</span><span class="sxs-lookup"><span data-stu-id="39a48-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="39a48-181">在方案總管中，以滑鼠右鍵按一下專案並選取 [**加入**]，然後選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="39a48-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="39a48-182">在 [**加入新專案**] 對話方塊中，選取 [**視覺效果C#** ] 底下的 [ **Web** ] 節點，然後選取 [ **HTML] 頁面**專案。</span><span class="sxs-lookup"><span data-stu-id="39a48-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="39a48-183">將頁面命名為 &quot;index .html&quot;。</span><span class="sxs-lookup"><span data-stu-id="39a48-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="39a48-184">以下列內容取代此檔案中的所有專案：</span><span class="sxs-lookup"><span data-stu-id="39a48-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="39a48-185">您可以使用幾種方式來取得 jQuery。</span><span class="sxs-lookup"><span data-stu-id="39a48-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="39a48-186">在此範例中，我使用了[Microsoft AJAX CDN](../../../ajax/cdn/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="39a48-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="39a48-187">您也可以從[http://jquery.com/](http://jquery.com/)下載，而 ASP.NET 的「Web API」專案範本也包含 jQuery。</span><span class="sxs-lookup"><span data-stu-id="39a48-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="39a48-188">取得產品清單</span><span class="sxs-lookup"><span data-stu-id="39a48-188">Getting a List of Products</span></span>

<span data-ttu-id="39a48-189">若要取得產品清單，請將 HTTP GET 要求傳送至 &quot;/api/products&quot;。</span><span class="sxs-lookup"><span data-stu-id="39a48-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="39a48-190">JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/)函數會傳送 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="39a48-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="39a48-191">For response 包含 JSON 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="39a48-191">For response contains array of JSON objects.</span></span> <span data-ttu-id="39a48-192">`done` 函式會指定要求成功時所呼叫的回呼。</span><span class="sxs-lookup"><span data-stu-id="39a48-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="39a48-193">在回呼中，我們會使用產品資訊來更新 DOM。</span><span class="sxs-lookup"><span data-stu-id="39a48-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="39a48-194">依識別碼取得產品</span><span class="sxs-lookup"><span data-stu-id="39a48-194">Getting a Product By ID</span></span>

<span data-ttu-id="39a48-195">若要依識別碼取得產品，請將 HTTP GET 要求傳送至 &quot;/api/products/*id*&quot;，其中*ID*是產品識別碼。</span><span class="sxs-lookup"><span data-stu-id="39a48-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="39a48-196">我們仍然會呼叫 `getJSON` 來傳送 AJAX 要求，但這次我們將識別碼放在要求 URI 中。</span><span class="sxs-lookup"><span data-stu-id="39a48-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="39a48-197">此要求的回應是單一產品的 JSON 標記法。</span><span class="sxs-lookup"><span data-stu-id="39a48-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="39a48-198">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="39a48-198">Running the Application</span></span>

<span data-ttu-id="39a48-199">按 F5 開始對應用程式進行偵錯。</span><span class="sxs-lookup"><span data-stu-id="39a48-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="39a48-200">網頁看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="39a48-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="39a48-201">若要依識別碼取得產品，請輸入識別碼，然後按一下 [搜尋]：</span><span class="sxs-lookup"><span data-stu-id="39a48-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="39a48-202">如果您輸入不正確識別碼，伺服器會傳回 HTTP 錯誤：</span><span class="sxs-lookup"><span data-stu-id="39a48-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="39a48-203">使用 F12 來查看 HTTP 要求和回應</span><span class="sxs-lookup"><span data-stu-id="39a48-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="39a48-204">當您使用 HTTP 服務時，查看 HTTP 要求和要求訊息會非常有用。</span><span class="sxs-lookup"><span data-stu-id="39a48-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="39a48-205">您可以使用 Internet Explorer 9 中的 F12 開發人員工具來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="39a48-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="39a48-206">從 Internet Explorer 9，按**F12**開啟工具。</span><span class="sxs-lookup"><span data-stu-id="39a48-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="39a48-207">按一下 [**網路**] 索引標籤，然後按 [**開始捕獲**]。</span><span class="sxs-lookup"><span data-stu-id="39a48-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="39a48-208">現在請回到網頁，然後按**F5**重載網頁。</span><span class="sxs-lookup"><span data-stu-id="39a48-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="39a48-209">Internet Explorer 將會在瀏覽器與 web 伺服器之間捕捉 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="39a48-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="39a48-210">[摘要] 視圖會顯示頁面的所有網路流量：</span><span class="sxs-lookup"><span data-stu-id="39a48-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="39a48-211">找出相對 URI "api/products/" 的專案。</span><span class="sxs-lookup"><span data-stu-id="39a48-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="39a48-212">選取此專案，然後按一下 [**移至詳細視圖**]。</span><span class="sxs-lookup"><span data-stu-id="39a48-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="39a48-213">在 [詳細資料] 視圖中，有一些索引標籤可供您查看要求和回應標頭和主體。</span><span class="sxs-lookup"><span data-stu-id="39a48-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="39a48-214">例如，如果您按一下 [**要求標頭**] 索引標籤，您可以看到用戶端要求的 &quot;application/json&quot; 在 Accept 標頭中。</span><span class="sxs-lookup"><span data-stu-id="39a48-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="39a48-215">如果您按一下 [回應主體] 索引標籤，您可以看到產品清單如何序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="39a48-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="39a48-216">其他瀏覽器具有類似的功能。</span><span class="sxs-lookup"><span data-stu-id="39a48-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="39a48-217">另一個有用的工具是[Fiddler](http://www.fiddler2.com/fiddler2/)，也就是 web 調試的 proxy。</span><span class="sxs-lookup"><span data-stu-id="39a48-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="39a48-218">您可以使用 Fiddler 來查看您的 HTTP 流量，並撰寫 HTTP 要求，讓您完全掌控要求中的 HTTP 標頭。</span><span class="sxs-lookup"><span data-stu-id="39a48-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="39a48-219">請參閱此應用程式在 Azure 上執行</span><span class="sxs-lookup"><span data-stu-id="39a48-219">See this App Running on Azure</span></span>

<span data-ttu-id="39a48-220">您是否想要查看已完成的網站以即時 web 應用程式的形式執行？</span><span class="sxs-lookup"><span data-stu-id="39a48-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="39a48-221">只要按一下下列按鈕，您就可以將應用程式的完整版本部署至您的 Azure 帳戶。</span><span class="sxs-lookup"><span data-stu-id="39a48-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="39a48-222">您需要 Azure 帳戶，才能將此解決方案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="39a48-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="39a48-223">如果您還沒有帳戶，您可以使用下列選項：</span><span class="sxs-lookup"><span data-stu-id="39a48-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="39a48-224">[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-您將取得可試用付費 azure 服務的額度，且即使在用完後，您仍可保留帳戶，並使用免費的 azure 服務。</span><span class="sxs-lookup"><span data-stu-id="39a48-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="39a48-225">[啟用 msdn 訂閱者權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-您的 msdn 訂用帳戶每月會提供您額度，供您用於付費 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="39a48-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="39a48-226">後續步驟</span><span class="sxs-lookup"><span data-stu-id="39a48-226">Next Steps</span></span>

- <span data-ttu-id="39a48-227">如需可支援 POST、PUT 和 DELETE 動作及寫入至資料庫之 HTTP 服務的更完整範例，請參閱搭配[使用 WEB API 2 與 Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="39a48-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="39a48-228">如需有關在 HTTP 服務上建立流暢且回應式 web 應用程式的詳細資訊，請參閱[ASP.NET 單一頁面應用程式](../../../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="39a48-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="39a48-229">如需如何將 Visual Studio Web 專案部署至 Azure App Service 的詳細資訊，請參閱[在 Azure App Service 中建立 ASP.NET web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="39a48-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
