---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
title: 建立路由條件約束（C#） |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 將示範如何使用正則運算式來建立路由條件約束，以控制瀏覽器要求如何符合路由。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 0bfd06b1-12d3-4fbb-9779-a82e5eb7fe7d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-route-constraint-cs
msc.type: authoredcontent
ms.openlocfilehash: 51ef859287b3424faf85f4a3606a220ab48a9466
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582009"
---
# <a name="creating-a-route-constraint-c"></a><span data-ttu-id="df0e3-103">建立路由條件約束 (C#)</span><span class="sxs-lookup"><span data-stu-id="df0e3-103">Creating a Route Constraint (C#)</span></span>

<span data-ttu-id="df0e3-104">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="df0e3-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="df0e3-105">在本教學課程中，Stephen Walther 將示範如何使用正則運算式來建立路由條件約束，以控制瀏覽器要求如何符合路由。</span><span class="sxs-lookup"><span data-stu-id="df0e3-105">In this tutorial, Stephen Walther demonstrates how you can control how browser requests match routes by creating route constraints with regular expressions.</span></span>

<span data-ttu-id="df0e3-106">您可以使用路由條件約束來限制符合特定路由的瀏覽器要求。</span><span class="sxs-lookup"><span data-stu-id="df0e3-106">You use route constraints to restrict the browser requests that match a particular route.</span></span> <span data-ttu-id="df0e3-107">您可以使用正則運算式來指定路由條件約束。</span><span class="sxs-lookup"><span data-stu-id="df0e3-107">You can use a regular expression to specify a route constraint.</span></span>

<span data-ttu-id="df0e3-108">例如，假設您已在 global.asax 檔案的 [清單 1] 中定義路由。</span><span class="sxs-lookup"><span data-stu-id="df0e3-108">For example, imagine that you have defined the route in Listing 1 in your Global.asax file.</span></span>

<span data-ttu-id="df0e3-109">**清單 1-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="df0e3-109">**Listing 1 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample1.cs)]

<span data-ttu-id="df0e3-110">[清單 1] 包含名為 Product 的路由。</span><span class="sxs-lookup"><span data-stu-id="df0e3-110">Listing 1 contains a route named Product.</span></span> <span data-ttu-id="df0e3-111">您可以使用產品路線，將瀏覽器要求對應至 [清單 2] 中所包含的 ProductController。</span><span class="sxs-lookup"><span data-stu-id="df0e3-111">You can use the Product route to map browser requests to the ProductController contained in Listing 2.</span></span>

<span data-ttu-id="df0e3-112">**清單 2-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="df0e3-112">**Listing 2 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample2.cs)]

<span data-ttu-id="df0e3-113">請注意，產品控制器所公開的詳細資料（）動作會接受名為 productId 的單一參數。</span><span class="sxs-lookup"><span data-stu-id="df0e3-113">Notice that the Details() action exposed by the Product controller accepts a single parameter named productId.</span></span> <span data-ttu-id="df0e3-114">這個參數是整數參數。</span><span class="sxs-lookup"><span data-stu-id="df0e3-114">This parameter is an integer parameter.</span></span>

<span data-ttu-id="df0e3-115">清單1中定義的路由會符合下列任何 Url：</span><span class="sxs-lookup"><span data-stu-id="df0e3-115">The route defined in Listing 1 will match any of the following URLs:</span></span>

- <span data-ttu-id="df0e3-116">/Product/23</span><span class="sxs-lookup"><span data-stu-id="df0e3-116">/Product/23</span></span>
- <span data-ttu-id="df0e3-117">/Product/7</span><span class="sxs-lookup"><span data-stu-id="df0e3-117">/Product/7</span></span>

<span data-ttu-id="df0e3-118">可惜的是，路由也會符合下列 Url：</span><span class="sxs-lookup"><span data-stu-id="df0e3-118">Unfortunately, the route will also match the following URLs:</span></span>

- <span data-ttu-id="df0e3-119">/Product/blah</span><span class="sxs-lookup"><span data-stu-id="df0e3-119">/Product/blah</span></span>
- <span data-ttu-id="df0e3-120">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="df0e3-120">/Product/apple</span></span>

<span data-ttu-id="df0e3-121">由於 Details （）動作需要整數參數，因此，要求若包含整數值以外的專案，將會造成錯誤。</span><span class="sxs-lookup"><span data-stu-id="df0e3-121">Because the Details() action expects an integer parameter, making a request that contains something other than an integer value will cause an error.</span></span> <span data-ttu-id="df0e3-122">例如，如果您在瀏覽器中輸入 URL/Product/apple，則會出現 [圖 1] 中的錯誤頁面。</span><span class="sxs-lookup"><span data-stu-id="df0e3-122">For example, if you type the URL /Product/apple into your browser then you will get the error page in Figure 1.</span></span>

<span data-ttu-id="df0e3-123">[![[新增專案] 對話方塊](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="df0e3-123">[![The New Project dialog box](creating-a-route-constraint-cs/_static/image1.jpg)](creating-a-route-constraint-cs/_static/image1.png)</span></span>

<span data-ttu-id="df0e3-124">**圖 01**：查看頁面分解（[按一下以觀看完整大小的影像](creating-a-route-constraint-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="df0e3-124">**Figure 01**: Seeing a page explode ([Click to view full-size image](creating-a-route-constraint-cs/_static/image2.png))</span></span>

<span data-ttu-id="df0e3-125">您真正想要做的只是符合包含適當整數 productId 的 Url。</span><span class="sxs-lookup"><span data-stu-id="df0e3-125">What you really want to do is only match URLs that contain a proper integer productId.</span></span> <span data-ttu-id="df0e3-126">定義路由以限制符合路由的 Url 時，您可以使用條件約束。</span><span class="sxs-lookup"><span data-stu-id="df0e3-126">You can use a constraint when defining a route to restrict the URLs that match the route.</span></span> <span data-ttu-id="df0e3-127">[清單 3] 中已修改的產品路由包含僅符合整數的正則運算式條件約束。</span><span class="sxs-lookup"><span data-stu-id="df0e3-127">The modified Product route in Listing 3 contains a regular expression constraint that only matches integers.</span></span>

<span data-ttu-id="df0e3-128">**清單 3-Global.asax.cs**</span><span class="sxs-lookup"><span data-stu-id="df0e3-128">**Listing 3 - Global.asax.cs**</span></span>

[!code-csharp[Main](creating-a-route-constraint-cs/samples/sample3.cs)]

<span data-ttu-id="df0e3-129">正則運算式 \d + 符合一或多個整數。</span><span class="sxs-lookup"><span data-stu-id="df0e3-129">The regular expression \d+ matches one or more integers.</span></span> <span data-ttu-id="df0e3-130">此條件約束會使產品路由符合下列 Url：</span><span class="sxs-lookup"><span data-stu-id="df0e3-130">This constraint causes the Product route to match the following URLs:</span></span>

- <span data-ttu-id="df0e3-131">/Product/3</span><span class="sxs-lookup"><span data-stu-id="df0e3-131">/Product/3</span></span>
- <span data-ttu-id="df0e3-132">/Product/8999</span><span class="sxs-lookup"><span data-stu-id="df0e3-132">/Product/8999</span></span>

<span data-ttu-id="df0e3-133">但不是下列 Url：</span><span class="sxs-lookup"><span data-stu-id="df0e3-133">But not the following URLs:</span></span>

- <span data-ttu-id="df0e3-134">/Product/apple</span><span class="sxs-lookup"><span data-stu-id="df0e3-134">/Product/apple</span></span>
- <span data-ttu-id="df0e3-135">/Product</span><span class="sxs-lookup"><span data-stu-id="df0e3-135">/Product</span></span>

- <span data-ttu-id="df0e3-136">這些瀏覽器要求將由另一個路由處理，或者，如果沒有相符的路由，就會傳回「找*不到資源*」錯誤。</span><span class="sxs-lookup"><span data-stu-id="df0e3-136">These browser requests will be handled by another route or, if there are no matching routes, a *The resource could not be found* error will be returned.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="df0e3-137">[上一頁](creating-custom-routes-cs.md)
> [下一頁](creating-a-custom-route-constraint-cs.md)</span><span class="sxs-lookup"><span data-stu-id="df0e3-137">[Previous](creating-custom-routes-cs.md)
[Next](creating-a-custom-route-constraint-cs.md)</span></span>
