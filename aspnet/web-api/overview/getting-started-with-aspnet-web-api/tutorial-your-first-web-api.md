---
uid: web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
title: 開始使用 ASP.NET Web API 2 (C#)-ASP.NET 4.x
author: MikeWasson
description: 使用程式碼的教學課程。 您可以使用 ASP.NET Web API 來建立 web API 會傳回一份產品。
ms.author: riande
ms.date: 11/28/2017
ms.custom: seoapril2019
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/tutorial-your-first-web-api
msc.type: authoredcontent
ms.openlocfilehash: 3e35c2bc0e46dfdb4544b772775eddd533f27be3
ms.sourcegitcommit: 51b01b6ff8edde57d8243e4da28c9f1e7f1962b2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 05/06/2019
ms.locfileid: "65125230"
---
# <a name="get-started-with-aspnet-web-api-2-c"></a><span data-ttu-id="216e9-104">開始使用 ASP.NET Web API 2 (C#)</span><span class="sxs-lookup"><span data-stu-id="216e9-104">Get Started with ASP.NET Web API 2 (C#)</span></span>

<span data-ttu-id="216e9-105">藉由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="216e9-105">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="216e9-106">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="216e9-106">Download Completed Project</span></span>](https://code.msdn.microsoft.com/Sample-code-of-Getting-c56ccb28)

<span data-ttu-id="216e9-107">在本教學課程中，您將使用 ASP.NET Web API 來建立 web API 會傳回一份產品。</span><span class="sxs-lookup"><span data-stu-id="216e9-107">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span>

<span data-ttu-id="216e9-108">HTTP 不只是提供 web 頁面。</span><span class="sxs-lookup"><span data-stu-id="216e9-108">HTTP is not just for serving up web pages.</span></span> <span data-ttu-id="216e9-109">HTTP 也是強大的平台，建置公開 （expose) 服務和資料的 Api。</span><span class="sxs-lookup"><span data-stu-id="216e9-109">HTTP is also a powerful platform for building APIs that expose services and data.</span></span> <span data-ttu-id="216e9-110">HTTP 是簡單、 彈性且無所不在。</span><span class="sxs-lookup"><span data-stu-id="216e9-110">HTTP is simple, flexible, and ubiquitous.</span></span> <span data-ttu-id="216e9-111">您可以將幾乎任何平台會有 HTTP 程式庫，因此 HTTP 服務可以連線到各種用戶端，包括瀏覽器、 行動裝置，以及傳統桌面應用程式。</span><span class="sxs-lookup"><span data-stu-id="216e9-111">Almost any platform that you can think of has an HTTP library, so HTTP services can reach a broad range of clients, including browsers, mobile devices, and traditional desktop applications.</span></span>

<span data-ttu-id="216e9-112">ASP.NET Web API 是用於建置 web Api 在.NET framework 的架構。</span><span class="sxs-lookup"><span data-stu-id="216e9-112">ASP.NET Web API is a framework for building web APIs on top of the .NET Framework.</span></span> 

## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="216e9-113">在本教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="216e9-113">Software versions used in the tutorial</span></span>

- [<span data-ttu-id="216e9-114">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="216e9-114">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)
- <span data-ttu-id="216e9-115">Web API 2</span><span class="sxs-lookup"><span data-stu-id="216e9-115">Web API 2</span></span>

<span data-ttu-id="216e9-116">請參閱[使用 ASP.NET Core 和 Visual Studio for Windows 建立 web API](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api)本教學課程的較新版本。</span><span class="sxs-lookup"><span data-stu-id="216e9-116">See [Create a web API with ASP.NET Core and Visual Studio for Windows](https://docs.microsoft.com/aspnet/core/tutorials/first-web-api) for a newer version of this tutorial.</span></span>

## <a name="create-a-web-api-project"></a><span data-ttu-id="216e9-117">建立 Web API 專案</span><span class="sxs-lookup"><span data-stu-id="216e9-117">Create a Web API Project</span></span>

<span data-ttu-id="216e9-118">在本教學課程中，您將使用 ASP.NET Web API 來建立 web API 會傳回一份產品。</span><span class="sxs-lookup"><span data-stu-id="216e9-118">In this tutorial, you will use ASP.NET Web API to create a web API that returns a list of products.</span></span> <span data-ttu-id="216e9-119">前端的 web 網頁會使用 jQuery 來顯示結果。</span><span class="sxs-lookup"><span data-stu-id="216e9-119">The front-end web page uses jQuery to display the results.</span></span>

![](tutorial-your-first-web-api/_static/image1.png)

<span data-ttu-id="216e9-120">啟動 Visual Studio，然後選取**新的專案**從**開始**頁面。</span><span class="sxs-lookup"><span data-stu-id="216e9-120">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="216e9-121">或從**檔案**功能表上，選取**新增**，然後**專案**。</span><span class="sxs-lookup"><span data-stu-id="216e9-121">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="216e9-122">在 **範本**窗格中，選取**已安裝的範本**展開**Visual C#** 節點。</span><span class="sxs-lookup"><span data-stu-id="216e9-122">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="216e9-123">底下**Visual C#**，選取**Web**。</span><span class="sxs-lookup"><span data-stu-id="216e9-123">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="216e9-124">在專案範本清單中，選取**ASP.NET Web 應用程式**。</span><span class="sxs-lookup"><span data-stu-id="216e9-124">In the list of project templates, select **ASP.NET Web Application**.</span></span> <span data-ttu-id="216e9-125">將專案命名為"ProductsApp 」，然後按一下**確定**。</span><span class="sxs-lookup"><span data-stu-id="216e9-125">Name the project "ProductsApp" and click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image2.png)

<span data-ttu-id="216e9-126">在 **新的 ASP.NET 專案**對話方塊中，選取**空白**範本。</span><span class="sxs-lookup"><span data-stu-id="216e9-126">In the **New ASP.NET Project** dialog, select the **Empty** template.</span></span> <span data-ttu-id="216e9-127">底下&quot;新增的資料夾和核心參考&quot;，檢查**Web API**。</span><span class="sxs-lookup"><span data-stu-id="216e9-127">Under &quot;Add folders and core references for&quot;, check **Web API**.</span></span> <span data-ttu-id="216e9-128">按一下 [確定] 。</span><span class="sxs-lookup"><span data-stu-id="216e9-128">Click **OK**.</span></span>

![](tutorial-your-first-web-api/_static/image3.png)

> [!NOTE]
> <span data-ttu-id="216e9-129">您也可以建立使用 Web API 專案&quot;Web API&quot;範本。</span><span class="sxs-lookup"><span data-stu-id="216e9-129">You can also create a Web API project using the &quot;Web API&quot; template.</span></span> <span data-ttu-id="216e9-130">Web API 範本會使用 ASP.NET MVC 提供 API 說明頁面。</span><span class="sxs-lookup"><span data-stu-id="216e9-130">The Web API template uses ASP.NET MVC to provide API help pages.</span></span> <span data-ttu-id="216e9-131">我正在使用空白範本本教學課程中，因為我想要顯示沒有 MVC 的 Web API。</span><span class="sxs-lookup"><span data-stu-id="216e9-131">I'm using the Empty template for this tutorial because I want to show Web API without MVC.</span></span> <span data-ttu-id="216e9-132">一般情況下，您不需要知道要使用 Web API 的 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="216e9-132">In general, you don't need to know ASP.NET MVC to use Web API.</span></span>

## <a name="adding-a-model"></a><span data-ttu-id="216e9-133">新增模型</span><span class="sxs-lookup"><span data-stu-id="216e9-133">Adding a Model</span></span>

<span data-ttu-id="216e9-134">「模型」是代表應用程式中資料的物件。</span><span class="sxs-lookup"><span data-stu-id="216e9-134">A *model* is an object that represents the data in your application.</span></span> <span data-ttu-id="216e9-135">ASP.NET Web API 可以自動序列化至 JSON、 XML 或某些其他格式，您的模型，然後將序列化的資料寫入 HTTP 回應訊息的本文。</span><span class="sxs-lookup"><span data-stu-id="216e9-135">ASP.NET Web API can automatically serialize your model to JSON, XML, or some other format, and then write the serialized data into the body of the HTTP response message.</span></span> <span data-ttu-id="216e9-136">只要用戶端可以讀取序列化格式，它可以還原序列化物件。</span><span class="sxs-lookup"><span data-stu-id="216e9-136">As long as a client can read the serialization format, it can deserialize the object.</span></span> <span data-ttu-id="216e9-137">大部分的用戶端可以剖析 XML 或 JSON。</span><span class="sxs-lookup"><span data-stu-id="216e9-137">Most clients can parse either XML or JSON.</span></span> <span data-ttu-id="216e9-138">此外，用戶端可以指定它想要藉由設定 Accept 標頭在 HTTP 要求訊息中的哪一種格式。</span><span class="sxs-lookup"><span data-stu-id="216e9-138">Moreover, the client can indicate which format it wants by setting the Accept header in the HTTP request message.</span></span>

<span data-ttu-id="216e9-139">讓我們開始建立簡單的模型，代表產品。</span><span class="sxs-lookup"><span data-stu-id="216e9-139">Let's start by creating a simple model that represents a product.</span></span>

<span data-ttu-id="216e9-140">如果沒有顯示 [方案總管] 中，按一下**檢視**功能表，然後選取**方案總管 中**。</span><span class="sxs-lookup"><span data-stu-id="216e9-140">If Solution Explorer is not already visible, click the **View** menu and select **Solution Explorer**.</span></span> <span data-ttu-id="216e9-141">在 [方案總管] 中，以滑鼠右鍵按一下 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="216e9-141">In Solution Explorer, right-click the Models folder.</span></span> <span data-ttu-id="216e9-142">從操作功能表中，選取**新增**然後選取**類別**。</span><span class="sxs-lookup"><span data-stu-id="216e9-142">From the context menu, select **Add** then select **Class**.</span></span>

![](tutorial-your-first-web-api/_static/image4.png)

<span data-ttu-id="216e9-143">將類別命名為&quot;產品&quot;。</span><span class="sxs-lookup"><span data-stu-id="216e9-143">Name the class &quot;Product&quot;.</span></span> <span data-ttu-id="216e9-144">新增下列屬性以`Product`類別。</span><span class="sxs-lookup"><span data-stu-id="216e9-144">Add the following properties to the `Product` class.</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample1.cs)]

## <a name="adding-a-controller"></a><span data-ttu-id="216e9-145">新增控制器</span><span class="sxs-lookup"><span data-stu-id="216e9-145">Adding a Controller</span></span>

<span data-ttu-id="216e9-146">在 Web API 中，*控制器*是處理 HTTP 要求的物件。</span><span class="sxs-lookup"><span data-stu-id="216e9-146">In Web API, a *controller* is an object that handles HTTP requests.</span></span> <span data-ttu-id="216e9-147">我們將新增可以傳回一份產品或單一產品識別碼所指定的控制站</span><span class="sxs-lookup"><span data-stu-id="216e9-147">We'll add a controller that can return either a list of products or a single product specified by ID.</span></span>

> [!NOTE]
> <span data-ttu-id="216e9-148">如果您已使用 ASP.NET MVC，您已熟悉控制站。</span><span class="sxs-lookup"><span data-stu-id="216e9-148">If you have used ASP.NET MVC, you are already familiar with controllers.</span></span> <span data-ttu-id="216e9-149">Web API 控制器 MVC 控制器類似，但繼承**ApiController**而不是類別**控制站**類別。</span><span class="sxs-lookup"><span data-stu-id="216e9-149">Web API controllers are similar to MVC controllers, but inherit the **ApiController** class instead of the **Controller** class.</span></span>

<span data-ttu-id="216e9-150">在**方案總管 中**，以滑鼠右鍵按一下 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="216e9-150">In **Solution Explorer**, right-click the Controllers folder.</span></span> <span data-ttu-id="216e9-151">選取 **新增**，然後選取**控制站**。</span><span class="sxs-lookup"><span data-stu-id="216e9-151">Select **Add** and then select **Controller**.</span></span>

![](tutorial-your-first-web-api/_static/image5.png)

<span data-ttu-id="216e9-152">在 **新增 Scaffold**對話方塊中，選取**Web API 控制器-空白**。</span><span class="sxs-lookup"><span data-stu-id="216e9-152">In the **Add Scaffold** dialog, select **Web API Controller - Empty**.</span></span> <span data-ttu-id="216e9-153">按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="216e9-153">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image6.png)

<span data-ttu-id="216e9-154">在 [**新增控制器**] 對話方塊中，將控制器命名&quot;ProductsController&quot;。</span><span class="sxs-lookup"><span data-stu-id="216e9-154">In the **Add Controller** dialog, name the controller &quot;ProductsController&quot;.</span></span> <span data-ttu-id="216e9-155">按一下 [加入] 。</span><span class="sxs-lookup"><span data-stu-id="216e9-155">Click **Add**.</span></span>

![](tutorial-your-first-web-api/_static/image7.png)

<span data-ttu-id="216e9-156">Scaffolding 會建立名為 ProductsController.cs 在 Controllers 資料夾中的檔案。</span><span class="sxs-lookup"><span data-stu-id="216e9-156">The scaffolding creates a file named ProductsController.cs in the Controllers folder.</span></span>

![](tutorial-your-first-web-api/_static/image8.png)

> [!NOTE]
> <span data-ttu-id="216e9-157">您不需要將您的控制站放入名為控制器的資料夾。</span><span class="sxs-lookup"><span data-stu-id="216e9-157">You don't need to put your controllers into a folder named Controllers.</span></span> <span data-ttu-id="216e9-158">資料夾名稱只是便利方式來組織您的原始程式檔。</span><span class="sxs-lookup"><span data-stu-id="216e9-158">The folder name is just a convenient way to organize your source files.</span></span>

<span data-ttu-id="216e9-159">如果此檔案尚未開啟，按兩下檔案以開啟它。</span><span class="sxs-lookup"><span data-stu-id="216e9-159">If this file is not open already, double-click the file to open it.</span></span> <span data-ttu-id="216e9-160">您可以將此檔案中的程式碼取代為下列：</span><span class="sxs-lookup"><span data-stu-id="216e9-160">Replace the code in this file with the following:</span></span>

[!code-csharp[Main](tutorial-your-first-web-api/samples/sample2.cs)]

<span data-ttu-id="216e9-161">為了簡化範例中，產品會儲存在控制器類別內的固定陣列。</span><span class="sxs-lookup"><span data-stu-id="216e9-161">To keep the example simple, products are stored in a fixed array inside the controller class.</span></span> <span data-ttu-id="216e9-162">當然，實際的應用程式中，您會查詢資料庫，或使用其他外部資料來源。</span><span class="sxs-lookup"><span data-stu-id="216e9-162">Of course, in a real application, you would query a database or use some other external data source.</span></span>

<span data-ttu-id="216e9-163">控制器會定義傳回產品的兩個方法：</span><span class="sxs-lookup"><span data-stu-id="216e9-163">The controller defines two methods that return products:</span></span>

- <span data-ttu-id="216e9-164">`GetAllProducts`方法會傳回整個清單的產品**IEnumerable&lt;產品&gt;** 型別。</span><span class="sxs-lookup"><span data-stu-id="216e9-164">The `GetAllProducts` method returns the entire list of products as an **IEnumerable&lt;Product&gt;** type.</span></span>
- <span data-ttu-id="216e9-165">`GetProduct`方法查閱單一產品依其識別碼。</span><span class="sxs-lookup"><span data-stu-id="216e9-165">The `GetProduct` method looks up a single product by its ID.</span></span>

<span data-ttu-id="216e9-166">就這麼容易！</span><span class="sxs-lookup"><span data-stu-id="216e9-166">That's it!</span></span> <span data-ttu-id="216e9-167">您必須使用 web API。</span><span class="sxs-lookup"><span data-stu-id="216e9-167">You have a working web API.</span></span> <span data-ttu-id="216e9-168">每個控制站上的方法對應至一或多個 Uri:</span><span class="sxs-lookup"><span data-stu-id="216e9-168">Each method on the controller corresponds to one or more URIs:</span></span>

| <span data-ttu-id="216e9-169">控制器方法</span><span class="sxs-lookup"><span data-stu-id="216e9-169">Controller Method</span></span> | <span data-ttu-id="216e9-170">URI</span><span class="sxs-lookup"><span data-stu-id="216e9-170">URI</span></span> |
| --- | --- |
| <span data-ttu-id="216e9-171">GetAllProducts</span><span class="sxs-lookup"><span data-stu-id="216e9-171">GetAllProducts</span></span> | <span data-ttu-id="216e9-172">/api/products</span><span class="sxs-lookup"><span data-stu-id="216e9-172">/api/products</span></span> |
| <span data-ttu-id="216e9-173">GetProduct</span><span class="sxs-lookup"><span data-stu-id="216e9-173">GetProduct</span></span> | <span data-ttu-id="216e9-174">/api/products/*id*</span><span class="sxs-lookup"><span data-stu-id="216e9-174">/api/products/*id*</span></span> |

<span data-ttu-id="216e9-175">針對`GetProduct`方法中，*識別碼*URI 中是預留位置。</span><span class="sxs-lookup"><span data-stu-id="216e9-175">For the `GetProduct` method, the *id* in the URI is a placeholder.</span></span> <span data-ttu-id="216e9-176">例如，若要取得識別碼 5 的產品，URI 是`api/products/5`。</span><span class="sxs-lookup"><span data-stu-id="216e9-176">For example, to get the product with ID of 5, the URI is `api/products/5`.</span></span>

<span data-ttu-id="216e9-177">如需有關如何 Web API 會將 HTTP 要求路由至控制器方法的詳細資訊，請參閱[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="216e9-177">For more information about how Web API routes HTTP requests to controller methods, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="calling-the-web-api-with-javascript-and-jquery"></a><span data-ttu-id="216e9-178">呼叫 Web API 以 Javascript 和 jQuery</span><span class="sxs-lookup"><span data-stu-id="216e9-178">Calling the Web API with Javascript and jQuery</span></span>

<span data-ttu-id="216e9-179">在本節中，我們將新增使用 AJAX 呼叫 web API 的 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="216e9-179">In this section, we'll add an HTML page that uses AJAX to call the web API.</span></span> <span data-ttu-id="216e9-180">我們將 jQuery 進行 AJAX 呼叫並以結果更新頁面。</span><span class="sxs-lookup"><span data-stu-id="216e9-180">We'll use jQuery to make the AJAX calls and also to update the page with the results.</span></span>

<span data-ttu-id="216e9-181">在 [方案總管] 中，以滑鼠右鍵按一下專案，然後選取**新增**，然後選取**新項目**。</span><span class="sxs-lookup"><span data-stu-id="216e9-181">In Solution Explorer, right-click the project and select **Add**, then select **New Item**.</span></span>

![](tutorial-your-first-web-api/_static/image9.png)

<span data-ttu-id="216e9-182">在 **加入新項目**對話方塊中，選取**Web**節點下的**Visual C#**，然後選取**HTML 網頁**項目。</span><span class="sxs-lookup"><span data-stu-id="216e9-182">In the **Add New Item** dialog, select the **Web** node under **Visual C#**, and then select the **HTML Page** item.</span></span> <span data-ttu-id="216e9-183">將頁面命名&quot;index.html&quot;。</span><span class="sxs-lookup"><span data-stu-id="216e9-183">Name the page &quot;index.html&quot;.</span></span>

![](tutorial-your-first-web-api/_static/image10.png)

<span data-ttu-id="216e9-184">您可以將此檔案中的所有項目取代為下列：</span><span class="sxs-lookup"><span data-stu-id="216e9-184">Replace everything in this file with the following:</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample3.html)]

<span data-ttu-id="216e9-185">您可以使用幾種方式來取得 jQuery。</span><span class="sxs-lookup"><span data-stu-id="216e9-185">There are several ways to get jQuery.</span></span> <span data-ttu-id="216e9-186">在此範例中，我使用了[Microsoft Ajax CDN](../../../ajax/cdn/overview.md)。</span><span class="sxs-lookup"><span data-stu-id="216e9-186">In this example, I used the [Microsoft Ajax CDN](../../../ajax/cdn/overview.md).</span></span> <span data-ttu-id="216e9-187">您也可以下載從[http://jquery.com/](http://jquery.com/)，和 ASP.NET"Web API 專案範本包含 jQuery 以及。</span><span class="sxs-lookup"><span data-stu-id="216e9-187">You can also download it from [http://jquery.com/](http://jquery.com/), and the ASP.NET "Web API" project template includes jQuery as well.</span></span>

### <a name="getting-a-list-of-products"></a><span data-ttu-id="216e9-188">取得產品清單</span><span class="sxs-lookup"><span data-stu-id="216e9-188">Getting a List of Products</span></span>

<span data-ttu-id="216e9-189">若要取得的產品清單，將傳送至 HTTP GET 要求給&quot;/api/產品&quot;。</span><span class="sxs-lookup"><span data-stu-id="216e9-189">To get a list of products, send an HTTP GET request to &quot;/api/products&quot;.</span></span>

<span data-ttu-id="216e9-190">JQuery [getJSON](http://api.jquery.com/jQuery.getJSON/)函式會將 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="216e9-190">The jQuery [getJSON](http://api.jquery.com/jQuery.getJSON/) function sends an AJAX request.</span></span> <span data-ttu-id="216e9-191">回應包含 JSON 物件的陣列。</span><span class="sxs-lookup"><span data-stu-id="216e9-191">For response contains array of JSON objects.</span></span> <span data-ttu-id="216e9-192">`done`函式會指定如果要求成功呼叫的回呼。</span><span class="sxs-lookup"><span data-stu-id="216e9-192">The `done` function specifies a callback that is called if the request succeeds.</span></span> <span data-ttu-id="216e9-193">在回呼中，我們可以更新 DOM 的產品資訊。</span><span class="sxs-lookup"><span data-stu-id="216e9-193">In the callback, we update the DOM with the product information.</span></span>

[!code-html[Main](tutorial-your-first-web-api/samples/sample4.html)]

### <a name="getting-a-product-by-id"></a><span data-ttu-id="216e9-194">取得產品識別碼</span><span class="sxs-lookup"><span data-stu-id="216e9-194">Getting a Product By ID</span></span>

<span data-ttu-id="216e9-195">若要取得的產品識別碼，將傳送至 HTTP GET 要求給&quot;/api/產品/*識別碼*&quot;，其中*識別碼*是產品識別碼。</span><span class="sxs-lookup"><span data-stu-id="216e9-195">To get a product by ID, send an HTTP GET request to &quot;/api/products/*id*&quot;, where *id* is the product ID.</span></span>

[!code-javascript[Main](tutorial-your-first-web-api/samples/sample5.js)]

<span data-ttu-id="216e9-196">我們仍然呼叫`getJSON`傳送 AJAX 要求，但這次我們 ID 放在要求 URI 中。</span><span class="sxs-lookup"><span data-stu-id="216e9-196">We still call `getJSON` to send the AJAX request, but this time we put the ID in the request URI.</span></span> <span data-ttu-id="216e9-197">此要求的回應是單一產品的 JSON 表示法。</span><span class="sxs-lookup"><span data-stu-id="216e9-197">The response from this request is a JSON representation of a single product.</span></span>

## <a name="running-the-application"></a><span data-ttu-id="216e9-198">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="216e9-198">Running the Application</span></span>

<span data-ttu-id="216e9-199">按 f5 鍵開始偵錯應用程式。</span><span class="sxs-lookup"><span data-stu-id="216e9-199">Press F5 to start debugging the application.</span></span> <span data-ttu-id="216e9-200">網頁看起來應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="216e9-200">The web page should look like the following:</span></span>

![](tutorial-your-first-web-api/_static/image11.png)

<span data-ttu-id="216e9-201">若要取得的產品識別碼，請輸入識別碼，再按一下 [搜尋]:</span><span class="sxs-lookup"><span data-stu-id="216e9-201">To get a product by ID, enter the ID and click Search:</span></span>

![](tutorial-your-first-web-api/_static/image12.png)

<span data-ttu-id="216e9-202">如果您輸入無效的識別碼時，伺服器就會傳回 HTTP 錯誤：</span><span class="sxs-lookup"><span data-stu-id="216e9-202">If you enter an invalid ID, the server returns an HTTP error:</span></span>

![](tutorial-your-first-web-api/_static/image13.png)

## <a name="using-f12-to-view-the-http-request-and-response"></a><span data-ttu-id="216e9-203">若要檢視的 HTTP 要求和回應中使用 F12</span><span class="sxs-lookup"><span data-stu-id="216e9-203">Using F12 to View the HTTP Request and Response</span></span>

<span data-ttu-id="216e9-204">當您使用的 HTTP 服務時，它可以是很適合用來查看 HTTP 要求，並要求訊息。</span><span class="sxs-lookup"><span data-stu-id="216e9-204">When you are working with an HTTP service, it can be very useful to see the HTTP request and request messages.</span></span> <span data-ttu-id="216e9-205">您可以使用 Internet Explorer 9 中的 F12 開發人員工具來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="216e9-205">You can do this by using the F12 developer tools in Internet Explorer 9.</span></span> <span data-ttu-id="216e9-206">從 Internet Explorer 9 中，按下**F12**來開啟 [工具]。</span><span class="sxs-lookup"><span data-stu-id="216e9-206">From Internet Explorer 9, press **F12** to open the tools.</span></span> <span data-ttu-id="216e9-207">按一下**網路** 索引標籤，然後按**開始擷取**。</span><span class="sxs-lookup"><span data-stu-id="216e9-207">Click the **Network** tab and press **Start Capturing**.</span></span> <span data-ttu-id="216e9-208">現在請返回 web 頁面，然後按**F5**重新載入網頁。</span><span class="sxs-lookup"><span data-stu-id="216e9-208">Now go back to the web page and press **F5** to reload the web page.</span></span> <span data-ttu-id="216e9-209">Internet Explorer 會擷取瀏覽器與 web 伺服器之間的 HTTP 流量。</span><span class="sxs-lookup"><span data-stu-id="216e9-209">Internet Explorer will capture the HTTP traffic between the browser and the web server.</span></span> <span data-ttu-id="216e9-210">[摘要] 檢視會顯示頁面的所有網路流量：</span><span class="sxs-lookup"><span data-stu-id="216e9-210">The summary view shows all the network traffic for a page:</span></span>

![](tutorial-your-first-web-api/_static/image14.png)

<span data-ttu-id="216e9-211">找出項目相對的 uri"api/產品 /"。</span><span class="sxs-lookup"><span data-stu-id="216e9-211">Locate the entry for the relative URI "api/products/".</span></span> <span data-ttu-id="216e9-212">選取此項目，然後按一下**前往 詳細檢視**。</span><span class="sxs-lookup"><span data-stu-id="216e9-212">Select this entry and click **Go to detailed view**.</span></span> <span data-ttu-id="216e9-213">在詳細資料 檢視中，有一些索引標籤來檢視要求和回應標頭和本文。</span><span class="sxs-lookup"><span data-stu-id="216e9-213">In the detail view, there are tabs to view the request and response headers and bodies.</span></span> <span data-ttu-id="216e9-214">例如，如果您按一下**要求標頭**索引標籤上，您可以看到用戶端已要求&quot;application/json&quot; Accept 標頭中。</span><span class="sxs-lookup"><span data-stu-id="216e9-214">For example, if you click the **Request headers** tab, you can see that the client requested &quot;application/json&quot; in the Accept header.</span></span>

![](tutorial-your-first-web-api/_static/image15.png)

<span data-ttu-id="216e9-215">如果您按一下 [回應內文] 索引標籤，您可以看到如何將產品清單已序列化為 JSON。</span><span class="sxs-lookup"><span data-stu-id="216e9-215">If you click the Response body tab, you can see how the product list was serialized to JSON.</span></span> <span data-ttu-id="216e9-216">其他瀏覽器具有類似的功能。</span><span class="sxs-lookup"><span data-stu-id="216e9-216">Other browsers have similar functionality.</span></span> <span data-ttu-id="216e9-217">另一個有用的工具是[Fiddler](http://www.fiddler2.com/fiddler2/)、 web 偵錯 proxy。</span><span class="sxs-lookup"><span data-stu-id="216e9-217">Another useful tool is [Fiddler](http://www.fiddler2.com/fiddler2/), a web debugging proxy.</span></span> <span data-ttu-id="216e9-218">您可以使用 Fiddler 來檢視您的 HTTP 流量，以及撰寫 HTTP 要求，這可讓您在要求中的 HTTP 標頭的完整控制。</span><span class="sxs-lookup"><span data-stu-id="216e9-218">You can use Fiddler to view your HTTP traffic, and also to compose HTTP requests, which gives you full control over the HTTP headers in the request.</span></span>

## <a name="see-this-app-running-on-azure"></a><span data-ttu-id="216e9-219">請參閱在 Azure 上執行此應用程式</span><span class="sxs-lookup"><span data-stu-id="216e9-219">See this App Running on Azure</span></span>

<span data-ttu-id="216e9-220">若要查看為即時 web 應用程式正在執行的完成的網站嗎？</span><span class="sxs-lookup"><span data-stu-id="216e9-220">Would you like to see the finished site running as a live web app?</span></span> <span data-ttu-id="216e9-221">您可以部署您的 Azure 帳戶的應用程式的完整版本，只要按一下下面的按鈕。</span><span class="sxs-lookup"><span data-stu-id="216e9-221">You can deploy a complete version of the app to your Azure account by simply clicking the following button.</span></span>

[![](https://azuredeploy.net/deploybutton.png)](https://deploy.azure.com/?WT.mc_id=deploy_azure_aspnet&repository=https://github.com/tfitzmac/WebAPI-ProductsApp#/form/setup)

<span data-ttu-id="216e9-222">您需要有 Azure 帳戶才能將此解決方案部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="216e9-222">You need an Azure account to deploy this solution to Azure.</span></span> <span data-ttu-id="216e9-223">如果您還沒有帳戶，您會有下列選項：</span><span class="sxs-lookup"><span data-stu-id="216e9-223">If you do not already have an account, you have the following options:</span></span>

- <span data-ttu-id="216e9-224">[免費申請 Azure 帳戶](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604)-取得信用額度來試用 Azure 付費服務，您可以使用和甚至用後最多，您可保留帳戶，並使用免費的 Azure 服務。</span><span class="sxs-lookup"><span data-stu-id="216e9-224">[Open an Azure account for free](https://azure.microsoft.com/pricing/free-trial/?WT.mc_id=A443DD604) - You get credits you can use to try out paid Azure services, and even after they're used up you can keep the account and use free Azure services.</span></span>
- <span data-ttu-id="216e9-225">[啟用 MSDN 訂戶權益](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604)-您的 MSDN 訂用帳戶信用額度每月都會提供您 Azure 付費服務，您可以使用。</span><span class="sxs-lookup"><span data-stu-id="216e9-225">[Activate MSDN subscriber benefits](https://azure.microsoft.com/pricing/member-offers/msdn-benefits-details/?WT.mc_id=A443DD604) - Your MSDN subscription gives you credits every month that you can use for paid Azure services.</span></span>

## <a name="next-steps"></a><span data-ttu-id="216e9-226">後續步驟</span><span class="sxs-lookup"><span data-stu-id="216e9-226">Next Steps</span></span>

- <span data-ttu-id="216e9-227">支援 POST、 PUT 和 DELETE 動作，並將寫入到資料庫的 HTTP 服務的更完整範例，請參閱 <<c0> [ 與 Entity Framework 6 中使用 Web API 2](../data/using-web-api-with-entity-framework/part-1.md)。</span><span class="sxs-lookup"><span data-stu-id="216e9-227">For a more complete example of an HTTP service that supports POST, PUT, and DELETE actions and writes to a database, see [Using Web API 2 with Entity Framework 6](../data/using-web-api-with-entity-framework/part-1.md).</span></span>
- <span data-ttu-id="216e9-228">如需有關建立 HTTP 服務之上的流暢並反應快速的 web 應用程式的詳細資訊，請參閱[ASP.NET 單一頁面應用程式](../../../single-page-application/index.md)。</span><span class="sxs-lookup"><span data-stu-id="216e9-228">For more about creating fluid and responsive web applications on top of an HTTP service, see [ASP.NET Single Page Application](../../../single-page-application/index.md).</span></span>
- <span data-ttu-id="216e9-229">如需如何將 Visual Studio web 專案部署至 Azure App Service 的資訊，請參閱[Azure App Service 中建立 ASP.NET web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/)。</span><span class="sxs-lookup"><span data-stu-id="216e9-229">For information about how to deploy a Visual Studio web project to Azure App Service, see [Create an ASP.NET web app in Azure App Service](https://azure.microsoft.com/documentation/articles/web-sites-dotnet-get-started/).</span></span>
