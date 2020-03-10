---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
title: 建立自訂路由條件約束（VB） |Microsoft Docs
author: StephenWalther
description: Stephen Walther 會示範如何建立自訂路由條件約束。 我們會實一個簡單的自訂條件約束，以防止路由符合
ms.author: riande
ms.date: 02/16/2009
ms.assetid: 892edb27-1cc2-4eaf-8314-dbc2efc6228a
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-custom-route-constraint-vb
msc.type: authoredcontent
ms.openlocfilehash: 2330708cf4a28180ce8a05f4696bf7a7a32092d6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601406"
---
# <a name="creating-a-custom-route-constraint-vb"></a><span data-ttu-id="b36f1-104">建立自訂的路由條件約束 (VB)</span><span class="sxs-lookup"><span data-stu-id="b36f1-104">Creating a Custom Route Constraint (VB)</span></span>

<span data-ttu-id="b36f1-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="b36f1-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="b36f1-106">Stephen Walther 會示範如何建立自訂路由條件約束。</span><span class="sxs-lookup"><span data-stu-id="b36f1-106">Stephen Walther demonstrates how you can create a custom route constraint.</span></span> <span data-ttu-id="b36f1-107">我們會執行簡單的自訂條件約束，以防止在來自遠端電腦的瀏覽器要求時比對路由。</span><span class="sxs-lookup"><span data-stu-id="b36f1-107">We implement a simple custom constraint that prevents a route from being matched when a browser request is made from a remote computer.</span></span>

<span data-ttu-id="b36f1-108">本教學課程的目的是要示範如何建立自訂路由條件約束。</span><span class="sxs-lookup"><span data-stu-id="b36f1-108">The goal of this tutorial is to demonstrate how you can create a custom route constraint.</span></span> <span data-ttu-id="b36f1-109">自訂路由條件約束可讓您避免比對路由，除非符合某些自訂條件。</span><span class="sxs-lookup"><span data-stu-id="b36f1-109">A custom route constraint enables you to prevent a route from being matched unless some custom condition is matched.</span></span>

<span data-ttu-id="b36f1-110">在本教學課程中，我們會建立 Localhost 路由條件約束。</span><span class="sxs-lookup"><span data-stu-id="b36f1-110">In this tutorial, we create a Localhost route constraint.</span></span> <span data-ttu-id="b36f1-111">Localhost 路由條件約束只符合從本機電腦提出的要求。</span><span class="sxs-lookup"><span data-stu-id="b36f1-111">The Localhost route constraint only matches requests made from the local computer.</span></span> <span data-ttu-id="b36f1-112">跨網際網路的遠端要求不相符。</span><span class="sxs-lookup"><span data-stu-id="b36f1-112">Remote requests from across the Internet are not matched.</span></span>

<span data-ttu-id="b36f1-113">您可以藉由執行 IRouteConstraint 介面來執行自訂路由條件約束。</span><span class="sxs-lookup"><span data-stu-id="b36f1-113">You implement a custom route constraint by implementing the IRouteConstraint interface.</span></span> <span data-ttu-id="b36f1-114">這是一個非常簡單的介面，可描述單一方法：</span><span class="sxs-lookup"><span data-stu-id="b36f1-114">This is an extremely simple interface which describes a single method:</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample1.vb)]

<span data-ttu-id="b36f1-115">方法會傳回布林值。</span><span class="sxs-lookup"><span data-stu-id="b36f1-115">The method returns a Boolean value.</span></span> <span data-ttu-id="b36f1-116">如果您傳回 False，與條件約束相關聯的路由就不會符合瀏覽器要求。</span><span class="sxs-lookup"><span data-stu-id="b36f1-116">If you return False, the route associated with the constraint won't match the browser request.</span></span>

<span data-ttu-id="b36f1-117">[清單 1] 中包含 Localhost 條件約束。</span><span class="sxs-lookup"><span data-stu-id="b36f1-117">The Localhost constraint is contained in Listing 1.</span></span>

<span data-ttu-id="b36f1-118">**清單 1-LocalhostConstraint .vb**</span><span class="sxs-lookup"><span data-stu-id="b36f1-118">**Listing 1 - LocalhostConstraint.vb**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample2.vb)]

<span data-ttu-id="b36f1-119">[清單 1] 中的條件約束會利用 HttpRequest 類別所公開的 IsLocal 屬性。</span><span class="sxs-lookup"><span data-stu-id="b36f1-119">The constraint in Listing 1 takes advantage of the IsLocal property exposed by the HttpRequest class.</span></span> <span data-ttu-id="b36f1-120">當要求的 IP 位址是127.0.0.1，或要求的 IP 與伺服器的 IP 位址相同時，此屬性會傳回 true。</span><span class="sxs-lookup"><span data-stu-id="b36f1-120">This property returns true when the IP address of the request is either 127.0.0.1 or when the IP of the request is the same as the server's IP address.</span></span>

<span data-ttu-id="b36f1-121">在 global.asax 檔案中定義的路由內，您可以使用自訂條件約束。</span><span class="sxs-lookup"><span data-stu-id="b36f1-121">You use a custom constraint within a route defined in the Global.asax file.</span></span> <span data-ttu-id="b36f1-122">[清單 2] 中的 global.asax 檔案使用 Localhost 條件約束，以防止任何人要求系統管理頁面，除非他們從本機伺服器提出要求。</span><span class="sxs-lookup"><span data-stu-id="b36f1-122">The Global.asax file in Listing 2 uses the Localhost constraint to prevent anyone from requesting an Admin page unless they make the request from the local server.</span></span> <span data-ttu-id="b36f1-123">例如，從遠端伺服器進行/Admin/DeleteAll 的要求將會失敗。</span><span class="sxs-lookup"><span data-stu-id="b36f1-123">For example, a request for /Admin/DeleteAll will fail when made from a remote server.</span></span>

<span data-ttu-id="b36f1-124">**清單 2-global.asax**</span><span class="sxs-lookup"><span data-stu-id="b36f1-124">**Listing 2 - Global.asax**</span></span>

[!code-vb[Main](creating-a-custom-route-constraint-vb/samples/sample3.vb)]

<span data-ttu-id="b36f1-125">Localhost 條件約束會用於管理路由的定義中。</span><span class="sxs-lookup"><span data-stu-id="b36f1-125">The Localhost constraint is used in the definition of the Admin route.</span></span> <span data-ttu-id="b36f1-126">此路由不會與遠端瀏覽器要求相符。</span><span class="sxs-lookup"><span data-stu-id="b36f1-126">This route won't be matched by a remote browser request.</span></span> <span data-ttu-id="b36f1-127">不過，請注意，global.asax 中定義的其他路由可能符合相同的要求。</span><span class="sxs-lookup"><span data-stu-id="b36f1-127">Realize, however, that other routes defined in Global.asax might match the same request.</span></span> <span data-ttu-id="b36f1-128">請務必瞭解，條件約束會防止特定路由符合要求，而不是在 global.asax 檔案中定義的所有路由。</span><span class="sxs-lookup"><span data-stu-id="b36f1-128">It is important to understand that a constraint prevents a particular route from matching a request and not all routes defined in the Global.asax file.</span></span>

<span data-ttu-id="b36f1-129">請注意，預設路由已從 [清單 2] 中的 global.asax 檔案加上批註。</span><span class="sxs-lookup"><span data-stu-id="b36f1-129">Notice that the Default route has been commented out from the Global.asax file in Listing 2.</span></span> <span data-ttu-id="b36f1-130">如果您包含預設路由，則預設路由會符合管理控制器的要求。</span><span class="sxs-lookup"><span data-stu-id="b36f1-130">If you include the Default route, then the Default route would match requests for the Admin controller.</span></span> <span data-ttu-id="b36f1-131">在此情況下，即使遠端使用者的要求不符合管理路由，仍然可以叫用管理控制器的動作。</span><span class="sxs-lookup"><span data-stu-id="b36f1-131">In that case, remote users could still invoke actions of the Admin controller even though their requests wouldn't match the Admin route.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b36f1-132">上一篇</span><span class="sxs-lookup"><span data-stu-id="b36f1-132">Previous</span></span>](creating-a-route-constraint-vb.md)
