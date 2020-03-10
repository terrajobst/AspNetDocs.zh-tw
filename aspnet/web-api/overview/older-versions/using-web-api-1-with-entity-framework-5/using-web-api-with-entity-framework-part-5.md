---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
title: 第5部分：使用挖的 .js 建立動態 UI |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: 9d9cb3b0-f4a7-434e-a508-9fc0ad0eb813
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-5
msc.type: authoredcontent
ms.openlocfilehash: bbdeba756de7986cfeb92aa10a57f4f101382f99
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78555990"
---
# <a name="part-5-creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="ccf62-102">第5部分：使用挖的 .js 建立動態 UI</span><span class="sxs-lookup"><span data-stu-id="ccf62-102">Part 5: Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="ccf62-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="ccf62-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="ccf62-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="ccf62-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-a-dynamic-ui-with-knockoutjs"></a><span data-ttu-id="ccf62-105">使用 Knockout.js 建立動態 UI</span><span class="sxs-lookup"><span data-stu-id="ccf62-105">Creating a Dynamic UI with Knockout.js</span></span>

<span data-ttu-id="ccf62-106">在本節中，我們將使用 [挖加] 將功能新增至系統管理員視圖。</span><span class="sxs-lookup"><span data-stu-id="ccf62-106">In this section, we'll use Knockout.js to add functionality to the Admin view.</span></span>

<span data-ttu-id="ccf62-107">[挖式 .js](http://knockoutjs.com/)是 JAVAscript 程式庫，可讓您輕鬆地將 HTML 控制項系結至資料。</span><span class="sxs-lookup"><span data-stu-id="ccf62-107">[Knockout.js](http://knockoutjs.com/) is a Javascript library that makes it easy to bind HTML controls to data.</span></span> <span data-ttu-id="ccf62-108">挖式 .js 會使用 ViewModel （MVVM）模式。</span><span class="sxs-lookup"><span data-stu-id="ccf62-108">Knockout.js uses the Model-View-ViewModel (MVVM) pattern.</span></span>

- <span data-ttu-id="ccf62-109">*模型*是企業網域中資料的伺服器端標記法（在我們的案例中為產品和訂單）。</span><span class="sxs-lookup"><span data-stu-id="ccf62-109">The *model* is the server-side representation of the data in the business domain (in our case, products and orders).</span></span>
- <span data-ttu-id="ccf62-110">此*視圖*為展示層（HTML）。</span><span class="sxs-lookup"><span data-stu-id="ccf62-110">The *view* is the presentation layer (HTML).</span></span>
- <span data-ttu-id="ccf62-111">*視圖模型*是包含模型資料的 JAVAscript 物件。</span><span class="sxs-lookup"><span data-stu-id="ccf62-111">The *view-model* is a Javascript object that holds the model data.</span></span> <span data-ttu-id="ccf62-112">視圖模型是 UI 的程式碼抽象概念。</span><span class="sxs-lookup"><span data-stu-id="ccf62-112">The view-model is a code abstraction of the UI.</span></span> <span data-ttu-id="ccf62-113">它不知道 HTML 標記法。</span><span class="sxs-lookup"><span data-stu-id="ccf62-113">It has no knowledge of the HTML representation.</span></span> <span data-ttu-id="ccf62-114">相反地，它代表視圖的抽象功能，例如「專案清單」。</span><span class="sxs-lookup"><span data-stu-id="ccf62-114">Instead, it represents abstract features of the view, such as "a list of items".</span></span>

<span data-ttu-id="ccf62-115">此視圖會資料系結至視圖模型。</span><span class="sxs-lookup"><span data-stu-id="ccf62-115">The view is data-bound to the view-model.</span></span> <span data-ttu-id="ccf62-116">視圖模型的更新會自動反映在視圖中。</span><span class="sxs-lookup"><span data-stu-id="ccf62-116">Updates to the view-model are automatically reflected in the view.</span></span> <span data-ttu-id="ccf62-117">視圖模型也會從視圖取得事件，例如按鈕按一下，然後在模型上執行作業，例如建立訂單。</span><span class="sxs-lookup"><span data-stu-id="ccf62-117">The view-model also gets events from the view, such as button clicks, and performs operations on the model, such as creating an order.</span></span>

![](using-web-api-with-entity-framework-part-5/_static/image1.png)

<span data-ttu-id="ccf62-118">首先，我們要定義視圖模型。</span><span class="sxs-lookup"><span data-stu-id="ccf62-118">First we'll define the view-model.</span></span> <span data-ttu-id="ccf62-119">之後，我們會將 HTML 標籤系結至視圖模型。</span><span class="sxs-lookup"><span data-stu-id="ccf62-119">After that, we will bind the HTML markup to the view-model.</span></span>

<span data-ttu-id="ccf62-120">將下列 Razor 區段新增至 Admin. cshtml：</span><span class="sxs-lookup"><span data-stu-id="ccf62-120">Add the following Razor section to Admin.cshtml:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample1.cshtml)]

<span data-ttu-id="ccf62-121">您可以將此區段新增至檔案中的任何位置。</span><span class="sxs-lookup"><span data-stu-id="ccf62-121">You can add this section anywhere in the file.</span></span> <span data-ttu-id="ccf62-122">當此視圖呈現時，區段會顯示在 HTML 頁面的底部，在結尾 &lt;/body&gt; 標記之前。</span><span class="sxs-lookup"><span data-stu-id="ccf62-122">When the view is rendered, the section appears at the bottom of the HTML page, right before the closing &lt;/body&gt; tag.</span></span>

<span data-ttu-id="ccf62-123">此頁面的所有腳本都會放在批註所指示的腳本標記內：</span><span class="sxs-lookup"><span data-stu-id="ccf62-123">All of the script for this page will go inside the script tag indicated by the comment:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample2.html)]

<span data-ttu-id="ccf62-124">首先，定義視圖模型類別：</span><span class="sxs-lookup"><span data-stu-id="ccf62-124">First, define a view-model class:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample3.js)]

<span data-ttu-id="ccf62-125">**observableArray**是一種特殊類型的物件，稱為可*觀察*的。</span><span class="sxs-lookup"><span data-stu-id="ccf62-125">**ko.observableArray** is a special kind of object in Knockout, called an *observable*.</span></span> <span data-ttu-id="ccf62-126">從「[挖的 .js」檔](http://knockoutjs.com/documentation/observables.html)：可觀察的是可以通知訂閱者有關變更的「JavaScript 物件」。</span><span class="sxs-lookup"><span data-stu-id="ccf62-126">From the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html): An observable is a "JavaScript object that can notify subscribers about changes."</span></span> <span data-ttu-id="ccf62-127">當可觀察的變更內容時，會自動更新此視圖以符合。</span><span class="sxs-lookup"><span data-stu-id="ccf62-127">When the contents of an observable change, the view is automatically updated to match.</span></span>

<span data-ttu-id="ccf62-128">若要填入 `products` 陣列，請向 Web API 發出 AJAX 要求。</span><span class="sxs-lookup"><span data-stu-id="ccf62-128">To populate the `products` array, make an AJAX request to the web API.</span></span> <span data-ttu-id="ccf62-129">回想一下，我們已將 API 的基底 URI 儲存在視圖包中（請參閱本教學課程的[第4部分](using-web-api-with-entity-framework-part-4.md)）。</span><span class="sxs-lookup"><span data-stu-id="ccf62-129">Recall that we stored the base URI for the API in the view bag (see [Part 4](using-web-api-with-entity-framework-part-4.md) of the tutorial).</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample4.js?highlight=5)]

<span data-ttu-id="ccf62-130">接下來，將函數新增至視圖模型，以建立、更新和刪除產品。</span><span class="sxs-lookup"><span data-stu-id="ccf62-130">Next, add functions to the view-model to create, update, and delete products.</span></span> <span data-ttu-id="ccf62-131">這些函式會將 AJAX 呼叫提交至 Web API，並使用結果來更新視圖模型。</span><span class="sxs-lookup"><span data-stu-id="ccf62-131">These functions submit AJAX calls to the web API and use the results to update the view-model.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample5.js?highlight=7)]

<span data-ttu-id="ccf62-132">現在最重要的部分： fulled 載入 DOM 時，呼叫**applyBindings**函式並傳入 `ProductsViewModel`的新實例：</span><span class="sxs-lookup"><span data-stu-id="ccf62-132">Now the most important part: When the DOM is fulled loaded, call the **ko.applyBindings** function and pass in a new instance of the `ProductsViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-5/samples/sample6.js)]

<span data-ttu-id="ccf62-133">**ApplyBindings**方法會啟動挖式，並將視圖模式向上線到視圖。</span><span class="sxs-lookup"><span data-stu-id="ccf62-133">The **ko.applyBindings** method activates Knockout and wires up the view-model to the view.</span></span>

<span data-ttu-id="ccf62-134">既然我們已經有了視圖模型，我們就可以建立系結。</span><span class="sxs-lookup"><span data-stu-id="ccf62-134">Now that we have a view-model, we can create the bindings.</span></span> <span data-ttu-id="ccf62-135">在挖的 .js 中，您可以藉由將 `data-bind` 屬性加入 HTML 專案來完成此動作。</span><span class="sxs-lookup"><span data-stu-id="ccf62-135">In Knockout.js, you do this by adding `data-bind` attributes to HTML elements.</span></span> <span data-ttu-id="ccf62-136">例如，若要將 HTML 清單系結至陣列，請使用 `foreach` 系結：</span><span class="sxs-lookup"><span data-stu-id="ccf62-136">For example, to bind an HTML list to an array, use the `foreach` binding:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample7.html?highlight=1)]

<span data-ttu-id="ccf62-137">`foreach` 系結會逐一查看陣列，並針對陣列中的每個物件建立子項目。</span><span class="sxs-lookup"><span data-stu-id="ccf62-137">The `foreach` binding iterates through the array and creates child elements for each object in the array.</span></span> <span data-ttu-id="ccf62-138">子項目上的系結可以參考陣列物件上的屬性。</span><span class="sxs-lookup"><span data-stu-id="ccf62-138">Bindings on the child elements can refer to properties on the array objects.</span></span>

<span data-ttu-id="ccf62-139">將下列系結新增至 [更新產品] 清單：</span><span class="sxs-lookup"><span data-stu-id="ccf62-139">Add the following bindings to the "update-products" list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample8.html)]

<span data-ttu-id="ccf62-140">`<li>` 元素會在**foreach**系結的範圍內發生。</span><span class="sxs-lookup"><span data-stu-id="ccf62-140">The `<li>` element occurs within the scope of the **foreach** binding.</span></span> <span data-ttu-id="ccf62-141">也就是說，「挖隔」會針對 `products` 陣列中的每個產品轉譯一次元素。</span><span class="sxs-lookup"><span data-stu-id="ccf62-141">That means Knockout will render the element once for each product in the `products` array.</span></span> <span data-ttu-id="ccf62-142">`<li>` 元素內的所有系結都會參考該產品實例。</span><span class="sxs-lookup"><span data-stu-id="ccf62-142">All of the bindings within the `<li>` element refer to that product instance.</span></span> <span data-ttu-id="ccf62-143">例如，`$data.Name` 指的是產品上的 `Name` 屬性。</span><span class="sxs-lookup"><span data-stu-id="ccf62-143">For example, `$data.Name` refers to the `Name` property on the product.</span></span>

<span data-ttu-id="ccf62-144">若要設定文字輸入的值，請使用 `value` 系結。</span><span class="sxs-lookup"><span data-stu-id="ccf62-144">To set the values of the text inputs, use the `value` binding.</span></span> <span data-ttu-id="ccf62-145">這些按鈕會使用 `click` 系結，系結至模型視圖上的函式。</span><span class="sxs-lookup"><span data-stu-id="ccf62-145">The buttons are bound to functions on the model-view, using the `click` binding.</span></span> <span data-ttu-id="ccf62-146">產品實例會當做參數傳遞至每個函式。</span><span class="sxs-lookup"><span data-stu-id="ccf62-146">The product instance is passed as a parameter to each function.</span></span> <span data-ttu-id="ccf62-147">如需詳細資訊，請[參閱「挖的 .js」檔](http://knockoutjs.com/documentation/observables.html)，以取得各種系結的良好描述。</span><span class="sxs-lookup"><span data-stu-id="ccf62-147">For more information, the [Knockout.js documentation](http://knockoutjs.com/documentation/observables.html) has good descriptions of the various bindings.</span></span>

<span data-ttu-id="ccf62-148">接下來，在 [新增產品] 表單上新增 [**提交**] 事件的系結：</span><span class="sxs-lookup"><span data-stu-id="ccf62-148">Next, add a binding for the **submit** event on the Add Product form:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-5/samples/sample9.html)]

<span data-ttu-id="ccf62-149">這個系結會在視圖模型上呼叫 `create` 函式，以建立新的產品。</span><span class="sxs-lookup"><span data-stu-id="ccf62-149">This binding calls the `create` function on the view-model to create a new product.</span></span>

<span data-ttu-id="ccf62-150">以下是系統管理視圖的完整程式碼：</span><span class="sxs-lookup"><span data-stu-id="ccf62-150">Here is the complete code for the Admin view:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-5/samples/sample10.cshtml)]

<span data-ttu-id="ccf62-151">執行應用程式、使用系統管理員帳戶登入，然後按一下 [管理] 連結。</span><span class="sxs-lookup"><span data-stu-id="ccf62-151">Run the application, log in with the Administrator account, and click the "Admin" link.</span></span> <span data-ttu-id="ccf62-152">您應該會看到產品清單，而且能夠建立、更新或刪除產品。</span><span class="sxs-lookup"><span data-stu-id="ccf62-152">You should see the list of products, and be able to create, update, or delete products.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ccf62-153">[上一頁](using-web-api-with-entity-framework-part-4.md)
> [下一頁](using-web-api-with-entity-framework-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="ccf62-153">[Previous](using-web-api-with-entity-framework-part-4.md)
[Next](using-web-api-with-entity-framework-part-6.md)</span></span>
