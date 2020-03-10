---
uid: web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
title: 使用 Web API 搭配 ASP.NET Web Forms-ASP.NET 4。x
author: MikeWasson
description: 使用程式碼逐步解說將 Web API 新增至 ASP.NET 4.x 的 ASP.NET Forms 應用程式的教學課程
ms.author: riande
ms.date: 04/03/2012
ms.custom: seoapril2019
ms.assetid: 25da8c3f-4e90-4946-9765-4f160985e1e4
msc.legacyurl: /web-api/overview/getting-started-with-aspnet-web-api/using-web-api-with-aspnet-web-forms
msc.type: authoredcontent
ms.openlocfilehash: ae553b62998fefd128e12711cbde958ea42d8c63
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78556774"
---
# <a name="using-web-api-with-aspnet-web-forms"></a><span data-ttu-id="be113-103">使用具有 ASP.NET Web Forms 的 Web API</span><span class="sxs-lookup"><span data-stu-id="be113-103">Using Web API with ASP.NET Web Forms</span></span>

<span data-ttu-id="be113-104">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="be113-104">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

<span data-ttu-id="be113-105">本教學課程將逐步引導您完成將 Web API 新增至 ASP.NET 4.x 中傳統 ASP.NET Web Forms 應用程式的步驟。</span><span class="sxs-lookup"><span data-stu-id="be113-105">This tutorial walks you through the steps to add Web API to a traditional ASP.NET Web Forms application in ASP.NET 4.x.</span></span> 

## <a name="overview"></a><span data-ttu-id="be113-106">概觀</span><span class="sxs-lookup"><span data-stu-id="be113-106">Overview</span></span>

<span data-ttu-id="be113-107">雖然 ASP.NET Web API 是以 ASP.NET MVC 封裝，但將 Web API 新增至傳統的 ASP.NET Web Forms 應用程式很容易。</span><span class="sxs-lookup"><span data-stu-id="be113-107">Although ASP.NET Web API is packaged with ASP.NET MVC, it is easy to add Web API to a traditional ASP.NET Web Forms application.</span></span>

<span data-ttu-id="be113-108">若要在 Web Forms 應用程式中使用 Web API，有兩個主要步驟：</span><span class="sxs-lookup"><span data-stu-id="be113-108">To use Web API in a Web Forms application, there are two main steps:</span></span>

- <span data-ttu-id="be113-109">新增衍生自**ApiController**類別的 Web API 控制器。</span><span class="sxs-lookup"><span data-stu-id="be113-109">Add a Web API controller that derives from the **ApiController** class.</span></span>
- <span data-ttu-id="be113-110">將路由表新增至**應用程式\_Start**方法。</span><span class="sxs-lookup"><span data-stu-id="be113-110">Add a route table to the **Application\_Start** method.</span></span>

## <a name="create-a-web-forms-project"></a><span data-ttu-id="be113-111">建立 Web Forms 專案</span><span class="sxs-lookup"><span data-stu-id="be113-111">Create a Web Forms Project</span></span>

<span data-ttu-id="be113-112">啟動 Visual Studio，然後從 [**開始**] 頁面選取 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="be113-112">Start Visual Studio and select **New Project** from the **Start** page.</span></span> <span data-ttu-id="be113-113">或者，**從 [檔案**] 功能表選取 [**新增**]，然後選取 [**專案**]。</span><span class="sxs-lookup"><span data-stu-id="be113-113">Or, from the **File** menu, select **New** and then **Project**.</span></span>

<span data-ttu-id="be113-114">在 [**範本**] 窗格中，選取 [**已安裝的範本**]，然後展開 **C#視覺效果**節點。</span><span class="sxs-lookup"><span data-stu-id="be113-114">In the **Templates** pane, select **Installed Templates** and expand the **Visual C#** node.</span></span> <span data-ttu-id="be113-115">在 **[ C#視覺效果**] 底下，選取 [ **Web**]。</span><span class="sxs-lookup"><span data-stu-id="be113-115">Under **Visual C#**, select **Web**.</span></span> <span data-ttu-id="be113-116">在專案範本清單中，選取 [ **ASP.NET Web Forms 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="be113-116">In the list of project templates, select **ASP.NET Web Forms Application**.</span></span> <span data-ttu-id="be113-117">輸入專案的名稱，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="be113-117">Enter a name for the project and click **OK**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image1.png)

## <a name="create-the-model-and-controller"></a><span data-ttu-id="be113-118">建立模型和控制器</span><span class="sxs-lookup"><span data-stu-id="be113-118">Create the Model and Controller</span></span>

<span data-ttu-id="be113-119">本教學課程使用與[消費者入門](tutorial-your-first-web-api.md)教學課程相同的模型和控制器類別。</span><span class="sxs-lookup"><span data-stu-id="be113-119">This tutorial uses the same model and controller classes as the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

<span data-ttu-id="be113-120">首先，新增模型類別。</span><span class="sxs-lookup"><span data-stu-id="be113-120">First, add a model class.</span></span> <span data-ttu-id="be113-121">在**方案總管**中，以滑鼠右鍵按一下專案，然後選取 [**新增類別**]。</span><span class="sxs-lookup"><span data-stu-id="be113-121">In **Solution Explorer**, right-click the project and select **Add Class**.</span></span> <span data-ttu-id="be113-122">將類別命名為 Product，並新增下列實作為：</span><span class="sxs-lookup"><span data-stu-id="be113-122">Name the class Product, and add the following implementation:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample1.cs)]

<span data-ttu-id="be113-123">接下來，將 Web API 控制器新增至專案。*控制器*是處理 Web API 之 HTTP 要求的物件。</span><span class="sxs-lookup"><span data-stu-id="be113-123">Next, add a Web API controller to the project., A *controller* is the object that handles HTTP requests for Web API.</span></span>

<span data-ttu-id="be113-124">在 [方案總管] 中，以滑鼠右鍵按一下專案。</span><span class="sxs-lookup"><span data-stu-id="be113-124">In **Solution Explorer**, right-click the project.</span></span> <span data-ttu-id="be113-125">選取 [**加入新專案**]。</span><span class="sxs-lookup"><span data-stu-id="be113-125">Select **Add New Item**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image2.png)

<span data-ttu-id="be113-126">展開 **已安裝的範本** 底下**的**   **C#視覺效果**，然後選取</span><span class="sxs-lookup"><span data-stu-id="be113-126">Under **Installed Templates**, expand **Visual C#** and select **Web**.</span></span> <span data-ttu-id="be113-127">然後，從範本清單中選取 [ **WEB API 控制器類別**]。</span><span class="sxs-lookup"><span data-stu-id="be113-127">Then, from the list of templates, select **Web API Controller Class**.</span></span> <span data-ttu-id="be113-128">將控制器命名為 "Productscontroller.cs"，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="be113-128">Name the controller "ProductsController" and click **Add**.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image3.png)

<span data-ttu-id="be113-129">[**加入新專案**] wizard 會建立名為 ProductsController.cs 的檔案。</span><span class="sxs-lookup"><span data-stu-id="be113-129">The **Add New Item** wizard will create a file named ProductsController.cs.</span></span> <span data-ttu-id="be113-130">刪除嚮導所包含的方法，並新增下列方法：</span><span class="sxs-lookup"><span data-stu-id="be113-130">Delete the methods that the wizard included and add the following methods:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample2.cs)]

<span data-ttu-id="be113-131">如需此控制器中程式碼的詳細資訊，請參閱[消費者入門](tutorial-your-first-web-api.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="be113-131">For more information about the code in this controller, see the [Getting Started](tutorial-your-first-web-api.md) tutorial.</span></span>

## <a name="add-routing-information"></a><span data-ttu-id="be113-132">新增路由資訊</span><span class="sxs-lookup"><span data-stu-id="be113-132">Add Routing Information</span></span>

<span data-ttu-id="be113-133">接下來，我們將新增 URI 路由，讓 &quot;/api/products/&quot; 表單的 Uri 路由傳送至控制器。</span><span class="sxs-lookup"><span data-stu-id="be113-133">Next, we'll add a URI route so that URIs of the form &quot;/api/products/&quot; are routed to the controller.</span></span>

<span data-ttu-id="be113-134">在**方案總管**中，按兩下 global.asax 以開啟 [程式碼後置檔案 Global.asax.cs]。</span><span class="sxs-lookup"><span data-stu-id="be113-134">In **Solution Explorer**, double-click Global.asax to open the code-behind file Global.asax.cs.</span></span> <span data-ttu-id="be113-135">新增下列**using**語句。</span><span class="sxs-lookup"><span data-stu-id="be113-135">Add the following **using** statement.</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample3.cs)]

<span data-ttu-id="be113-136">然後，將下列程式碼新增至**應用程式\_Start**方法：</span><span class="sxs-lookup"><span data-stu-id="be113-136">Then add the following code to the **Application\_Start** method:</span></span>

[!code-csharp[Main](using-web-api-with-aspnet-web-forms/samples/sample4.cs)]

<span data-ttu-id="be113-137">如需路由表的詳細資訊，請參閱[ASP.NET Web API 中的路由](../web-api-routing-and-actions/routing-in-aspnet-web-api.md)。</span><span class="sxs-lookup"><span data-stu-id="be113-137">For more information about routing tables, see [Routing in ASP.NET Web API](../web-api-routing-and-actions/routing-in-aspnet-web-api.md).</span></span>

## <a name="add-client-side-ajax"></a><span data-ttu-id="be113-138">新增用戶端 AJAX</span><span class="sxs-lookup"><span data-stu-id="be113-138">Add Client-Side AJAX</span></span>

<span data-ttu-id="be113-139">您只需要建立用戶端可以存取的 Web API。</span><span class="sxs-lookup"><span data-stu-id="be113-139">That's all you need to create a web API that clients can access.</span></span> <span data-ttu-id="be113-140">現在讓我們加入一個使用 jQuery 呼叫 API 的 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="be113-140">Now let's add an HTML page that uses jQuery to call the API.</span></span>

<span data-ttu-id="be113-141">請確定您的主版頁面（例如，*網站*）包含具有 `ID="HeadContent"`的 `ContentPlaceHolder`：</span><span class="sxs-lookup"><span data-stu-id="be113-141">Make sure your master page (for example, *Site.Master*) includes a `ContentPlaceHolder` with `ID="HeadContent"`:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample8.html)]

<span data-ttu-id="be113-142">開啟檔案 default.aspx。</span><span class="sxs-lookup"><span data-stu-id="be113-142">Open the file Default.aspx.</span></span> <span data-ttu-id="be113-143">取代主要內容區段中的重複顯示文字，如下所示：</span><span class="sxs-lookup"><span data-stu-id="be113-143">Replace the boilerplate text that is in the main content section, as shown:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample5.aspx)]

<span data-ttu-id="be113-144">接下來，在 [`HeaderContent`] 區段中新增 jQuery 來源檔案的參考：</span><span class="sxs-lookup"><span data-stu-id="be113-144">Next, add a reference to the jQuery source file in the `HeaderContent` section:</span></span>

[!code-aspx[Main](using-web-api-with-aspnet-web-forms/samples/sample6.aspx?highlight=2)]

<span data-ttu-id="be113-145">注意：您可以將檔案從**方案總管**拖放到 [程式碼編輯器] 視窗中，輕鬆地加入腳本參考。</span><span class="sxs-lookup"><span data-stu-id="be113-145">Note: You can easily add the script reference by dragging and dropping the file from **Solution Explorer** into the code editor window.</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image4.png)

<span data-ttu-id="be113-146">在 jQuery script 標記底下，新增下列腳本區塊：</span><span class="sxs-lookup"><span data-stu-id="be113-146">Below the jQuery script tag, add the following script block:</span></span>

[!code-html[Main](using-web-api-with-aspnet-web-forms/samples/sample7.html)]

<span data-ttu-id="be113-147">當檔載入時，此腳本會發出 AJAX 要求，以 &quot;api/產品&quot;。</span><span class="sxs-lookup"><span data-stu-id="be113-147">When the document loads, this script makes an AJAX request to &quot;api/products&quot;.</span></span> <span data-ttu-id="be113-148">要求會傳回 JSON 格式的產品清單。</span><span class="sxs-lookup"><span data-stu-id="be113-148">The request returns a list of products in JSON format.</span></span> <span data-ttu-id="be113-149">腳本會將產品資訊新增至 HTML 資料表。</span><span class="sxs-lookup"><span data-stu-id="be113-149">The script adds the product information to the HTML table.</span></span>

<span data-ttu-id="be113-150">當您執行應用程式時，它看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="be113-150">When you run the application, it should look like this:</span></span>

![](using-web-api-with-aspnet-web-forms/_static/image5.png)
