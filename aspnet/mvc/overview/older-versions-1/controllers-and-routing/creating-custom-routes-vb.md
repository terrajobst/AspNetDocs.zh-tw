---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
title: 建立自訂路由（VB） |Microsoft Docs
author: microsoft
description: 瞭解如何將自訂路由新增至 ASP.NET MVC 應用程式。 在本教學課程中，您將瞭解如何修改 global.asax 檔案中的預設路由表。
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 6ac5758b-6199-42af-adcb-21954b864951
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-custom-routes-vb
msc.type: authoredcontent
ms.openlocfilehash: 22b44e9e575c9d404881a23ee735bb0c8b7109e1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601294"
---
# <a name="creating-custom-routes-vb"></a><span data-ttu-id="5246b-104">建立自訂路由 (VB)</span><span class="sxs-lookup"><span data-stu-id="5246b-104">Creating Custom Routes (VB)</span></span>

<span data-ttu-id="5246b-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="5246b-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="5246b-106">瞭解如何將自訂路由新增至 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5246b-106">Learn how to add custom routes to an ASP.NET MVC application.</span></span> <span data-ttu-id="5246b-107">在本教學課程中，您將瞭解如何修改 global.asax 檔案中的預設路由表。</span><span class="sxs-lookup"><span data-stu-id="5246b-107">In this tutorial, you learn how to modify the default route table in the Global.asax file.</span></span>

<span data-ttu-id="5246b-108">在本教學課程中，您將瞭解如何將自訂路由新增至 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5246b-108">In this tutorial, you learn how to add a custom route to an ASP.NET MVC application.</span></span> <span data-ttu-id="5246b-109">您將瞭解如何使用自訂路由來修改 global.asax 檔案中的預設路由表。</span><span class="sxs-lookup"><span data-stu-id="5246b-109">You learn how to modify the default route table in the Global.asax file with a custom route.</span></span>

<span data-ttu-id="5246b-110">在 ASP.NET MVC 應用程式中，預設路由表會正常執行。</span><span class="sxs-lookup"><span data-stu-id="5246b-110">In ASP.NET MVC applications, the default route table will work just fine.</span></span> <span data-ttu-id="5246b-111">不過，您可能會發現您有特殊的路由需求。</span><span class="sxs-lookup"><span data-stu-id="5246b-111">However, you might discover that you have specialized routing needs.</span></span> <span data-ttu-id="5246b-112">在此情況下，您可以建立自訂路由。</span><span class="sxs-lookup"><span data-stu-id="5246b-112">In that case, you can create a custom route.</span></span>

<span data-ttu-id="5246b-113">例如，假設您要建立一個 blog 應用程式。</span><span class="sxs-lookup"><span data-stu-id="5246b-113">Imagine, for example, that you are building a blog application.</span></span> <span data-ttu-id="5246b-114">您可能會想要處理傳入的要求，如下所示：</span><span class="sxs-lookup"><span data-stu-id="5246b-114">You might want to handle incoming requests that look like this:</span></span>

<span data-ttu-id="5246b-115">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="5246b-115">/Archive/12-25-2009</span></span>

<span data-ttu-id="5246b-116">當使用者輸入此要求時，您會想要傳回對應于日期12/25/2009 的 blog 專案。</span><span class="sxs-lookup"><span data-stu-id="5246b-116">When a user enters this request, you want to return the blog entry that corresponds to the date 12/25/2009.</span></span> <span data-ttu-id="5246b-117">若要處理這種類型的要求，您必須建立自訂路由。</span><span class="sxs-lookup"><span data-stu-id="5246b-117">In order to handle this type of request, you need to create a custom route.</span></span>

<span data-ttu-id="5246b-118">[清單 1] 中的 global.asax 檔案包含新的自訂路由，名為 Blog，它會處理類似/Archive/*專案日期*的要求。</span><span class="sxs-lookup"><span data-stu-id="5246b-118">The Global.asax file in Listing 1 contains a new custom route, named Blog, which handles requests that look like /Archive/*entry date*.</span></span>

<span data-ttu-id="5246b-119">**清單 1-global.asax （含自訂路由）**</span><span class="sxs-lookup"><span data-stu-id="5246b-119">**Listing 1 - Global.asax (with custom route)**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample1.vb)]

<span data-ttu-id="5246b-120">您新增至路由表的路由順序很重要。</span><span class="sxs-lookup"><span data-stu-id="5246b-120">The order of the routes that you add to the route table is important.</span></span> <span data-ttu-id="5246b-121">新的自訂 Blog 路由會在現有的預設路由之前新增。</span><span class="sxs-lookup"><span data-stu-id="5246b-121">Our new custom Blog route is added before the existing Default route.</span></span> <span data-ttu-id="5246b-122">如果您反轉順序，則預設路由一律會呼叫，而不是自訂路由。</span><span class="sxs-lookup"><span data-stu-id="5246b-122">If you reversed the order, then the Default route always will get called instead of the custom route.</span></span>

<span data-ttu-id="5246b-123">自訂的 Blog 路由會符合任何以/Archive/. 開頭的要求</span><span class="sxs-lookup"><span data-stu-id="5246b-123">The custom Blog route matches any request that starts with /Archive/.</span></span> <span data-ttu-id="5246b-124">因此，它會符合下列所有 Url：</span><span class="sxs-lookup"><span data-stu-id="5246b-124">So, it matches all of the following URLs:</span></span>

- <span data-ttu-id="5246b-125">/Archive/12-25-2009</span><span class="sxs-lookup"><span data-stu-id="5246b-125">/Archive/12-25-2009</span></span>

- <span data-ttu-id="5246b-126">/Archive/10-6-2004</span><span class="sxs-lookup"><span data-stu-id="5246b-126">/Archive/10-6-2004</span></span>

- <span data-ttu-id="5246b-127">/Archive/apple</span><span class="sxs-lookup"><span data-stu-id="5246b-127">/Archive/apple</span></span>

<span data-ttu-id="5246b-128">自訂路由會將傳入要求對應至名為 Archive 的控制器，並叫用 Entry （）動作。</span><span class="sxs-lookup"><span data-stu-id="5246b-128">The custom route maps the incoming request to a controller named Archive and invokes the Entry() action.</span></span> <span data-ttu-id="5246b-129">呼叫 Entry （）方法時，會將專案日期當做名為 entryDate 的參數傳遞。</span><span class="sxs-lookup"><span data-stu-id="5246b-129">When the Entry() method is called, the entry date is passed as a parameter named entryDate.</span></span>

<span data-ttu-id="5246b-130">您可以在 [清單 2] 中使用與控制器的 Blog 自訂路由。</span><span class="sxs-lookup"><span data-stu-id="5246b-130">You can use the Blog custom route with the controller in Listing 2.</span></span>

<span data-ttu-id="5246b-131">**清單 2-ArchiveController .vb**</span><span class="sxs-lookup"><span data-stu-id="5246b-131">**Listing 2 - ArchiveController.vb**</span></span>

[!code-vb[Main](creating-custom-routes-vb/samples/sample2.vb)]

<span data-ttu-id="5246b-132">請注意，[清單 2] 中的 Entry （）方法會接受 DateTime 類型的參數。</span><span class="sxs-lookup"><span data-stu-id="5246b-132">Notice that the Entry() method in Listing 2 accepts a parameter of type DateTime.</span></span> <span data-ttu-id="5246b-133">MVC 架構很聰明，可以將 URL 中的輸入日期自動轉換成日期時間值。</span><span class="sxs-lookup"><span data-stu-id="5246b-133">The MVC framework is smart enough to convert the entry date from the URL into a DateTime value automatically.</span></span> <span data-ttu-id="5246b-134">如果 URL 中的 entry date 參數無法轉換成 DateTime，則會引發錯誤（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="5246b-134">If the entry date parameter from the URL cannot be converted to a DateTime, an error is raised (see Figure 1).</span></span>

<span data-ttu-id="5246b-135">**圖 1-轉換參數時發生的錯誤**</span><span class="sxs-lookup"><span data-stu-id="5246b-135">**Figure 1 - Error from converting parameter**</span></span>

<span data-ttu-id="5246b-136">[![[新增專案] 對話方塊](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="5246b-136">[![The New Project dialog box](creating-custom-routes-vb/_static/image1.jpg)](creating-custom-routes-vb/_static/image1.png)</span></span>

<span data-ttu-id="5246b-137">**圖 01**：轉換參數時發生錯誤（[按一下以觀看完整大小的影像](creating-custom-routes-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="5246b-137">**Figure 01**: Error from converting parameter ([Click to view full-size image](creating-custom-routes-vb/_static/image2.png))</span></span>

## <a name="summary"></a><span data-ttu-id="5246b-138">總結</span><span class="sxs-lookup"><span data-stu-id="5246b-138">Summary</span></span>

<span data-ttu-id="5246b-139">本教學課程的目的是要示範如何建立自訂路由。</span><span class="sxs-lookup"><span data-stu-id="5246b-139">The goal of this tutorial was to demonstrate how you can create a custom route.</span></span> <span data-ttu-id="5246b-140">您已瞭解如何將自訂路由新增至代表 blog 專案之 global.asax 檔案中的路由表。</span><span class="sxs-lookup"><span data-stu-id="5246b-140">You learned how to add a custom route to the route table in the Global.asax file that represents blog entries.</span></span> <span data-ttu-id="5246b-141">我們已討論如何將 blog 專案的要求對應至名為 ArchiveController 的控制器，以及名為 Entry （）的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="5246b-141">We discussed how to map requests for blog entries to a controller named ArchiveController and a controller action named Entry().</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="5246b-142">[上一頁](asp-net-mvc-controller-overview-vb.md)
> [下一頁](creating-a-route-constraint-vb.md)</span><span class="sxs-lookup"><span data-stu-id="5246b-142">[Previous](asp-net-mvc-controller-overview-vb.md)
[Next](creating-a-route-constraint-vb.md)</span></span>
