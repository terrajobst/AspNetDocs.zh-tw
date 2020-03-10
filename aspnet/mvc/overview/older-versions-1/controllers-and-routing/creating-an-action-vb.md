---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
title: 建立動作（VB） |Microsoft Docs
author: microsoft
description: 瞭解如何將新動作新增至 ASP.NET MVC 控制器。 瞭解方法的需求是動作。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: c8d93e11-ef78-4a30-afbc-f30419000a60
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-an-action-vb
msc.type: authoredcontent
ms.openlocfilehash: b1b53bea899deecef203551b23c087944e3990ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78582002"
---
# <a name="creating-an-action-vb"></a><span data-ttu-id="17b4e-104">建立動作 (VB)</span><span class="sxs-lookup"><span data-stu-id="17b4e-104">Creating an Action (VB)</span></span>

<span data-ttu-id="17b4e-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="17b4e-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="17b4e-106">瞭解如何將新動作新增至 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="17b4e-106">Learn how to add a new action to an ASP.NET MVC controller.</span></span> <span data-ttu-id="17b4e-107">瞭解方法的需求是動作。</span><span class="sxs-lookup"><span data-stu-id="17b4e-107">Learn about the requirements for a method to be an action.</span></span>

<span data-ttu-id="17b4e-108">本教學課程的目的是要說明如何建立新的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="17b4e-108">The goal of this tutorial is to explain how you can create a new controller action.</span></span> <span data-ttu-id="17b4e-109">您會瞭解動作方法的需求。</span><span class="sxs-lookup"><span data-stu-id="17b4e-109">You learn about the requirements of an action method.</span></span> <span data-ttu-id="17b4e-110">您也將瞭解如何防止方法公開為動作。</span><span class="sxs-lookup"><span data-stu-id="17b4e-110">You also learn how to prevent a method from being exposed as an action.</span></span>

## <a name="adding-an-action-to-a-controller"></a><span data-ttu-id="17b4e-111">將動作新增至控制器</span><span class="sxs-lookup"><span data-stu-id="17b4e-111">Adding an Action to a Controller</span></span>

<span data-ttu-id="17b4e-112">您可以藉由將新的方法加入至控制器，將新的動作新增至控制器。</span><span class="sxs-lookup"><span data-stu-id="17b4e-112">You add a new action to a controller by adding a new method to the controller.</span></span> <span data-ttu-id="17b4e-113">例如，[清單 1] 中的控制器包含名為 Index （）的動作，以及名為 SayHello （）的動作。</span><span class="sxs-lookup"><span data-stu-id="17b4e-113">For example, the controller in Listing 1 contains an action named Index() and an action named SayHello().</span></span> <span data-ttu-id="17b4e-114">這兩種方法都會公開為動作。</span><span class="sxs-lookup"><span data-stu-id="17b4e-114">Both methods are exposed as actions.</span></span>

<span data-ttu-id="17b4e-115">**清單 1-Controllers\HomeController.vb**</span><span class="sxs-lookup"><span data-stu-id="17b4e-115">**Listing 1 - Controllers\HomeController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample1.vb)]

<span data-ttu-id="17b4e-116">若要以動作的形式公開至 universe，方法必須符合特定需求：</span><span class="sxs-lookup"><span data-stu-id="17b4e-116">In order to be exposed to the universe as an action, a method must meet certain requirements:</span></span>

- <span data-ttu-id="17b4e-117">此方法必須是公用的。</span><span class="sxs-lookup"><span data-stu-id="17b4e-117">The method must be public.</span></span>
- <span data-ttu-id="17b4e-118">方法不可以是靜態方法。</span><span class="sxs-lookup"><span data-stu-id="17b4e-118">The method cannot be a static method.</span></span>
- <span data-ttu-id="17b4e-119">方法不可以是擴充方法。</span><span class="sxs-lookup"><span data-stu-id="17b4e-119">The method cannot be an extension method.</span></span>
- <span data-ttu-id="17b4e-120">方法不可以是函數、getter 或 setter。</span><span class="sxs-lookup"><span data-stu-id="17b4e-120">The method cannot be a constructor, getter, or setter.</span></span>
- <span data-ttu-id="17b4e-121">方法不能有開放式泛型型別。</span><span class="sxs-lookup"><span data-stu-id="17b4e-121">The method cannot have open generic types.</span></span>
- <span data-ttu-id="17b4e-122">方法不是控制器基類的方法。</span><span class="sxs-lookup"><span data-stu-id="17b4e-122">The method is not a method of the controller base class.</span></span>
- <span data-ttu-id="17b4e-123">方法不能包含**ref**或**out**參數。</span><span class="sxs-lookup"><span data-stu-id="17b4e-123">The method cannot contain **ref** or **out** parameters.</span></span>

<span data-ttu-id="17b4e-124">請注意，控制器動作的傳回型別沒有任何限制。</span><span class="sxs-lookup"><span data-stu-id="17b4e-124">Notice that there are no restrictions on the return type of a controller action.</span></span> <span data-ttu-id="17b4e-125">控制器動作可以傳回字串、DateTime、Random 類別的實例，或 void。</span><span class="sxs-lookup"><span data-stu-id="17b4e-125">A controller action can return a string, a DateTime, an instance of the Random class, or void.</span></span> <span data-ttu-id="17b4e-126">ASP.NET MVC 架構會將不是動作結果的任何傳回型別轉換成字串，並將字串轉譯為瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="17b4e-126">The ASP.NET MVC framework will convert any return type that is not an action result into a string and render the string to the browser.</span></span>

<span data-ttu-id="17b4e-127">當您將任何不違反這些需求的方法新增至控制器時，該方法會公開為控制器動作。</span><span class="sxs-lookup"><span data-stu-id="17b4e-127">When you add any method that does not violate these requirements to a controller, the method is exposed as a controller action.</span></span> <span data-ttu-id="17b4e-128">請注意這裡。</span><span class="sxs-lookup"><span data-stu-id="17b4e-128">Be careful here.</span></span> <span data-ttu-id="17b4e-129">連線到網際網路的任何人都可以叫用控制器動作。</span><span class="sxs-lookup"><span data-stu-id="17b4e-129">A controller action can be invoked by anyone connected to the Internet.</span></span> <span data-ttu-id="17b4e-130">例如，請不要建立 DeleteMyWebsite （）控制器動作。</span><span class="sxs-lookup"><span data-stu-id="17b4e-130">Do not, for example, create a DeleteMyWebsite() controller action.</span></span>

## <a name="preventing-a-public-method-from-being-invoked"></a><span data-ttu-id="17b4e-131">防止叫用公用方法</span><span class="sxs-lookup"><span data-stu-id="17b4e-131">Preventing a Public Method from Being Invoked</span></span>

<span data-ttu-id="17b4e-132">如果您需要在控制器類別中建立公用方法，而且不想要將方法公開為控制器動作，則可以使用 &lt;請以 nonaction&gt; 屬性來避免叫用方法。</span><span class="sxs-lookup"><span data-stu-id="17b4e-132">If you need to create a public method in a controller class and you don't want to expose the method as a controller action then you can prevent the method from being invoked by using the &lt;NonAction&gt; attribute.</span></span> <span data-ttu-id="17b4e-133">例如，[清單 2] 中的控制器包含名為 CompanySecrets （）的公用方法，它會以 &lt;請以 nonaction&gt; 屬性裝飾。</span><span class="sxs-lookup"><span data-stu-id="17b4e-133">For example, the controller in Listing 2 contains a public method named CompanySecrets() that is decorated with the &lt;NonAction&gt; attribute.</span></span>

<span data-ttu-id="17b4e-134">**清單 2-Controllers\WorkController.vb**</span><span class="sxs-lookup"><span data-stu-id="17b4e-134">**Listing 2 - Controllers\WorkController.vb**</span></span>

[!code-vb[Main](creating-an-action-vb/samples/sample2.vb)]

<span data-ttu-id="17b4e-135">如果您嘗試藉由在瀏覽器的網址列中輸入/Work/CompanySecrets 來叫用 CompanySecrets （）控制器動作，則會收到 [圖 1] 中的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="17b4e-135">If you attempt to invoke the CompanySecrets() controller action by typing /Work/CompanySecrets into the address bar of your browser then you'll get the error message in Figure 1.</span></span>

<span data-ttu-id="17b4e-136">[![叫用請以 nonaction 方法](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="17b4e-136">[![Invoking a NonAction method](creating-an-action-vb/_static/image1.jpg)](creating-an-action-vb/_static/image1.png)</span></span>

<span data-ttu-id="17b4e-137">**圖 01**：叫用請以 nonaction 方法（[按一下以查看完整大小的影像](creating-an-action-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="17b4e-137">**Figure 01**: Invoking a NonAction method([Click to view full-size image](creating-an-action-vb/_static/image2.png))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="17b4e-138">[上一頁](creating-a-controller-vb.md)
> [下一頁](aspnet-mvc-controllers-overview-cs.md)</span><span class="sxs-lookup"><span data-stu-id="17b4e-138">[Previous](creating-a-controller-vb.md)
[Next](aspnet-mvc-controllers-overview-cs.md)</span></span>
