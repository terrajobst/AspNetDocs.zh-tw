---
uid: web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
title: 第7部分：建立主頁面 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 07/04/2012
ms.assetid: eb32a17b-626c-4373-9a7d-3387992f3c04
msc.legacyurl: /web-api/overview/older-versions/using-web-api-1-with-entity-framework-5/using-web-api-with-entity-framework-part-7
msc.type: authoredcontent
ms.openlocfilehash: fe4074c701159a137be3644d65ca844f160c2399
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74599980"
---
# <a name="part-7-creating-the-main-page"></a><span data-ttu-id="89a28-102">第7部分：建立主頁面</span><span class="sxs-lookup"><span data-stu-id="89a28-102">Part 7: Creating the Main Page</span></span>

<span data-ttu-id="89a28-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="89a28-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="89a28-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="89a28-104">Download Completed Project</span></span>](https://code.msdn.microsoft.com/ASP-NET-Web-API-with-afa30545)

## <a name="creating-the-main-page"></a><span data-ttu-id="89a28-105">建立主要頁面</span><span class="sxs-lookup"><span data-stu-id="89a28-105">Creating the Main Page</span></span>

<span data-ttu-id="89a28-106">在本節中，您將建立主應用程式頁面。</span><span class="sxs-lookup"><span data-stu-id="89a28-106">In this section, you will create the main application page.</span></span> <span data-ttu-id="89a28-107">此頁面比管理頁面更為複雜，因此我們將在幾個步驟中進行處理。</span><span class="sxs-lookup"><span data-stu-id="89a28-107">This page will be more complex than the Admin page, so we'll approach it in several steps.</span></span> <span data-ttu-id="89a28-108">在此過程中，您將會看到一些更先進的「挖加」的方法。</span><span class="sxs-lookup"><span data-stu-id="89a28-108">Along the way, you'll see some more advanced Knockout.js techniques.</span></span> <span data-ttu-id="89a28-109">以下是頁面的基本版面配置：</span><span class="sxs-lookup"><span data-stu-id="89a28-109">Here is the basic layout of the page:</span></span>

![](using-web-api-with-entity-framework-part-7/_static/image1.png)

- <span data-ttu-id="89a28-110">「產品」包含產品的陣列。</span><span class="sxs-lookup"><span data-stu-id="89a28-110">"Products" holds an array of products.</span></span>
- <span data-ttu-id="89a28-111">「購物車」包含具有數量的產品陣列。</span><span class="sxs-lookup"><span data-stu-id="89a28-111">"Cart" holds an array of products with quantities.</span></span> <span data-ttu-id="89a28-112">按一下 [新增至購物車] 會更新購物車。</span><span class="sxs-lookup"><span data-stu-id="89a28-112">Clicking "Add to Cart" updates the cart.</span></span>
- <span data-ttu-id="89a28-113">「訂單」包含訂單識別碼的陣列。</span><span class="sxs-lookup"><span data-stu-id="89a28-113">"Orders" holds an array of order IDs.</span></span>
- <span data-ttu-id="89a28-114">「詳細資料」包含訂單詳細資料，也就是專案的陣列（具有數量的產品）</span><span class="sxs-lookup"><span data-stu-id="89a28-114">"Details" holds an order detail, which is an array of items (products with quantities)</span></span>

<span data-ttu-id="89a28-115">我們一開始會在 HTML 中定義一些基本版面配置，而不會有任何資料系結或腳本。</span><span class="sxs-lookup"><span data-stu-id="89a28-115">We'll start by defining some basic layout in HTML, with no data binding or script.</span></span> <span data-ttu-id="89a28-116">開啟檔案 Views/Home/Index. cshtml，並將所有內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="89a28-116">Open the file Views/Home/Index.cshtml and replace all of the contents with the following:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample1.html)]

<span data-ttu-id="89a28-117">接下來，新增腳本區段並建立空白的視圖模型：</span><span class="sxs-lookup"><span data-stu-id="89a28-117">Next, add a Scripts section and create an empty view-model:</span></span>

[!code-cshtml[Main](using-web-api-with-entity-framework-part-7/samples/sample2.cshtml)]

<span data-ttu-id="89a28-118">根據稍早所繪的設計，我們的視圖模型需要產品、購物車、訂單和詳細資料的可預見值。</span><span class="sxs-lookup"><span data-stu-id="89a28-118">Based on the design sketched earlier, our view model needs observables for products, cart, orders, and details.</span></span> <span data-ttu-id="89a28-119">將下列變數新增至 `AppViewModel` 物件：</span><span class="sxs-lookup"><span data-stu-id="89a28-119">Add the following variables to the `AppViewModel` object:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample3.js)]

<span data-ttu-id="89a28-120">使用者可以將產品清單中的專案新增至購物車，並移除購物車中的專案。</span><span class="sxs-lookup"><span data-stu-id="89a28-120">Users can add items from the products list into the cart, and remove items from the cart.</span></span> <span data-ttu-id="89a28-121">為了封裝這些函式，我們將建立另一個代表產品的視圖模型類別。</span><span class="sxs-lookup"><span data-stu-id="89a28-121">To encapsulate these functions, we'll create another view-model class that represents a product.</span></span> <span data-ttu-id="89a28-122">將下列程式碼新增至 `AppViewModel`：</span><span class="sxs-lookup"><span data-stu-id="89a28-122">Add the following code to `AppViewModel`:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample4.js?highlight=4)]

<span data-ttu-id="89a28-123">`ProductViewModel` 類別包含兩個函式，可用來將產品移至購物車或從中移動： `addItemToCart` 會將產品的一個單位新增至購物車，而 `removeAllFromCart` 則會移除產品的所有數量。</span><span class="sxs-lookup"><span data-stu-id="89a28-123">The `ProductViewModel` class contains two functions that are used to move the product to and from the cart: `addItemToCart` adds one unit of the product to the cart, and `removeAllFromCart` removes all quantities of the product.</span></span>

<span data-ttu-id="89a28-124">使用者可以選取現有的訂單，並取得訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="89a28-124">Users can select an existing order and get the order details.</span></span> <span data-ttu-id="89a28-125">我們會將此功能封裝到另一個視圖模型中：</span><span class="sxs-lookup"><span data-stu-id="89a28-125">We'll encapsulate this functionality into another view-model:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample5.js?highlight=4)]

<span data-ttu-id="89a28-126">`OrderDetailsViewModel` 會以訂單進行初始化，並藉由將 AJAX 要求傳送至伺服器來提取訂單詳細資料。</span><span class="sxs-lookup"><span data-stu-id="89a28-126">The `OrderDetailsViewModel` is initialized with an order, and it fetches the order details by sending an AJAX request to the server.</span></span>

<span data-ttu-id="89a28-127">此外，請注意 `OrderDetailsViewModel`上的 `total` 屬性。</span><span class="sxs-lookup"><span data-stu-id="89a28-127">Also, notice the `total` property on the `OrderDetailsViewModel`.</span></span> <span data-ttu-id="89a28-128">此屬性是一種特殊類型的可觀察，稱為計算的可[觀察](http://knockoutjs.com/documentation/computedObservables.html)。</span><span class="sxs-lookup"><span data-stu-id="89a28-128">This property is a special kind of observable called a [computed observable](http://knockoutjs.com/documentation/computedObservables.html).</span></span> <span data-ttu-id="89a28-129">顧名思義，「計算的可觀察」可讓您將資料系結至&#8212;計算的值，在此案例中為訂單的總成本。</span><span class="sxs-lookup"><span data-stu-id="89a28-129">As the name implies, a computed observable lets you data bind to a computed value&#8212;in this case, the total cost of the order.</span></span>

<span data-ttu-id="89a28-130">接下來，將下列函式新增至 `AppViewModel`：</span><span class="sxs-lookup"><span data-stu-id="89a28-130">Next, add these functions to `AppViewModel`:</span></span>

- <span data-ttu-id="89a28-131">`resetCart` 會移除購物車中的所有專案。</span><span class="sxs-lookup"><span data-stu-id="89a28-131">`resetCart` removes all items from the cart.</span></span>
- <span data-ttu-id="89a28-132">`getDetails` 取得訂單的詳細資料（藉由將新的 `OrderDetailsViewModel` 推送至 `details` 清單）。</span><span class="sxs-lookup"><span data-stu-id="89a28-132">`getDetails` gets the details for an order (by pushing a new `OrderDetailsViewModel` onto the `details` list).</span></span>
- <span data-ttu-id="89a28-133">`createOrder` 會建立新的訂單，並清空購物車。</span><span class="sxs-lookup"><span data-stu-id="89a28-133">`createOrder` creates a new order and empties the cart.</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample6.js?highlight=4)]

<span data-ttu-id="89a28-134">最後，藉由對產品和訂單提出 AJAX 要求來初始化視圖模型：</span><span class="sxs-lookup"><span data-stu-id="89a28-134">Finally, initialize the view model by making AJAX requests for the products and orders:</span></span>

[!code-javascript[Main](using-web-api-with-entity-framework-part-7/samples/sample7.js)]

<span data-ttu-id="89a28-135">好的，這是很多程式碼，但是我們會逐步建立它，因此希望設計清楚明瞭。</span><span class="sxs-lookup"><span data-stu-id="89a28-135">OK, that's a lot of code, but we built it up step-by-step, so hopefully the design is clear.</span></span> <span data-ttu-id="89a28-136">現在我們可以將一些挖的 .js 系結新增至 HTML。</span><span class="sxs-lookup"><span data-stu-id="89a28-136">Now we can add some Knockout.js bindings to the HTML.</span></span>

<span data-ttu-id="89a28-137">**Products**</span><span class="sxs-lookup"><span data-stu-id="89a28-137">**Products**</span></span>

<span data-ttu-id="89a28-138">以下是產品清單的系結：</span><span class="sxs-lookup"><span data-stu-id="89a28-138">Here are the bindings for the product list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample8.html)]

<span data-ttu-id="89a28-139">這會逐一查看 products 陣列，並顯示名稱和價格。</span><span class="sxs-lookup"><span data-stu-id="89a28-139">This iterates over the products array and displays the name and price.</span></span> <span data-ttu-id="89a28-140">只有在使用者登入時，才可以看到 [加入順序] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="89a28-140">The "Add to Order" button is visible only when the user is logged in.</span></span>

<span data-ttu-id="89a28-141">[加入至訂單] 按鈕會在產品的 `ProductViewModel` 實例上呼叫 `addItemToCart`。</span><span class="sxs-lookup"><span data-stu-id="89a28-141">The "Add to Order" button calls `addItemToCart` on the `ProductViewModel` instance for the product.</span></span> <span data-ttu-id="89a28-142">這會示範挖式 .js 的絕佳功能：當視圖模型包含其他視圖模型時，您可以將系結套用至內部模型。</span><span class="sxs-lookup"><span data-stu-id="89a28-142">This demonstrates a nice feature of Knockout.js: When a view-model contains other view-models, you can apply the bindings to the inner model.</span></span> <span data-ttu-id="89a28-143">在此範例中，`foreach` 內的系結會套用至每個 `ProductViewModel` 實例。</span><span class="sxs-lookup"><span data-stu-id="89a28-143">In this example, the bindings within the `foreach` are applied to each of the `ProductViewModel` instances.</span></span> <span data-ttu-id="89a28-144">這種方法比將所有功能放入單一視圖模型中更為簡潔。</span><span class="sxs-lookup"><span data-stu-id="89a28-144">This approach is much cleaner than putting all of the functionality into a single view-model.</span></span>

<span data-ttu-id="89a28-145">**放**</span><span class="sxs-lookup"><span data-stu-id="89a28-145">**Cart**</span></span>

<span data-ttu-id="89a28-146">以下是購物車的系結：</span><span class="sxs-lookup"><span data-stu-id="89a28-146">Here are the bindings for the cart:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample9.html)]

<span data-ttu-id="89a28-147">這會逐一查看購物車陣列，並顯示名稱、價格和數量。</span><span class="sxs-lookup"><span data-stu-id="89a28-147">This iterates over the cart array and displays the name, price, and quantity.</span></span> <span data-ttu-id="89a28-148">請注意，[移除] 連結和 [建立順序] 按鈕會系結至視圖模型函數。</span><span class="sxs-lookup"><span data-stu-id="89a28-148">Note that the "Remove" link and the "Create Order" button are bound to view-model functions.</span></span>

<span data-ttu-id="89a28-149">**訂單**</span><span class="sxs-lookup"><span data-stu-id="89a28-149">**Orders**</span></span>

<span data-ttu-id="89a28-150">以下是 orders 清單的系結：</span><span class="sxs-lookup"><span data-stu-id="89a28-150">Here are the bindings for the orders list:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample10.html)]

<span data-ttu-id="89a28-151">這會逐一查看訂單，並顯示訂單識別碼。</span><span class="sxs-lookup"><span data-stu-id="89a28-151">This iterates over the orders and shows the order ID.</span></span> <span data-ttu-id="89a28-152">連結上的 click 事件會系結到 `getDetails` 函數。</span><span class="sxs-lookup"><span data-stu-id="89a28-152">The click event on the link is bound to the `getDetails` function.</span></span>

<span data-ttu-id="89a28-153">**訂單詳細資料**</span><span class="sxs-lookup"><span data-stu-id="89a28-153">**Order Details**</span></span>

<span data-ttu-id="89a28-154">以下是訂單詳細資料的系結：</span><span class="sxs-lookup"><span data-stu-id="89a28-154">Here are the bindings for the order details:</span></span>

[!code-html[Main](using-web-api-with-entity-framework-part-7/samples/sample11.html)]

<span data-ttu-id="89a28-155">這會逐一查看訂單中的專案，並顯示產品、價格和數量。</span><span class="sxs-lookup"><span data-stu-id="89a28-155">This iterates over the items in the order and displays the product, price, and quantity.</span></span> <span data-ttu-id="89a28-156">只有當詳細資料陣列包含一個或多個專案時，才會顯示周圍的 div。</span><span class="sxs-lookup"><span data-stu-id="89a28-156">The surrounding div is visible only if the details array contains one or more items.</span></span>

## <a name="conclusion"></a><span data-ttu-id="89a28-157">結論</span><span class="sxs-lookup"><span data-stu-id="89a28-157">Conclusion</span></span>

<span data-ttu-id="89a28-158">在本教學課程中，您已建立使用 Entity Framework 與資料庫通訊的應用程式，並 ASP.NET Web API 在資料層上提供公開介面。</span><span class="sxs-lookup"><span data-stu-id="89a28-158">In this tutorial, you created an application that uses Entity Framework to communicate with the database, and ASP.NET Web API to provide a public-facing interface on top of the data layer.</span></span> <span data-ttu-id="89a28-159">我們會使用 ASP.NET MVC 4 來轉譯 HTML 網頁，並使用挖加 jQuery 來提供動態互動，而不需要頁面重載。</span><span class="sxs-lookup"><span data-stu-id="89a28-159">We use ASP.NET MVC 4 to render the HTML pages, and Knockout.js plus jQuery to provide dynamic interactions without page reloads.</span></span>

<span data-ttu-id="89a28-160">其他資源：</span><span class="sxs-lookup"><span data-stu-id="89a28-160">Additional resources:</span></span>

- [<span data-ttu-id="89a28-161">ASP.NET 資料存取內容地圖</span><span class="sxs-lookup"><span data-stu-id="89a28-161">ASP.NET Data Access Content Map</span></span>](https://msdn.microsoft.com/library/6759sth4.aspx)
- [<span data-ttu-id="89a28-162">Entity Framework 開發人員中心</span><span class="sxs-lookup"><span data-stu-id="89a28-162">Entity Framework Developer Center</span></span>](https://msdn.microsoft.com/data/ef)

> [!div class="step-by-step"]
> [<span data-ttu-id="89a28-163">上一篇</span><span class="sxs-lookup"><span data-stu-id="89a28-163">Previous</span></span>](using-web-api-with-entity-framework-part-6.md)
