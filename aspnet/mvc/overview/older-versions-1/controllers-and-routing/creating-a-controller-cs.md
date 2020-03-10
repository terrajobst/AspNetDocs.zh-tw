---
uid: mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
title: 建立控制器（C#） |Microsoft Docs
author: StephenWalther
description: 在本教學課程中，Stephen Walther 會示範如何將控制器新增至 ASP.NET MVC 應用程式。
ms.author: riande
ms.date: 03/02/2009
ms.assetid: 719d50d4-2305-454c-98b4-bae64937c48f
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/creating-a-controller-cs
msc.type: authoredcontent
ms.openlocfilehash: 6e3d0bae7f07410637c2b06c500d94a02c821f5c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544076"
---
# <a name="creating-a-controller-c"></a><span data-ttu-id="14f69-103">建立控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="14f69-103">Creating a Controller (C#)</span></span>

<span data-ttu-id="14f69-104">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="14f69-104">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

> <span data-ttu-id="14f69-105">在本教學課程中，Stephen Walther 會示範如何將控制器新增至 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="14f69-105">In this tutorial, Stephen Walther demonstrates how you can add a controller to an ASP.NET MVC application.</span></span>

<span data-ttu-id="14f69-106">本教學課程的目的是要說明如何建立新的 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="14f69-106">The goal of this tutorial is to explain how you can create new ASP.NET MVC controllers.</span></span> <span data-ttu-id="14f69-107">您將瞭解如何使用 Visual Studio 的 [新增控制器] 功能表選項，以及手動建立類別檔案來建立控制器。</span><span class="sxs-lookup"><span data-stu-id="14f69-107">You learn how to create controllers both by using the Visual Studio Add Controller menu option and by creating a class file by hand.</span></span>

### <a name="using-the-add-controller-menu-option"></a><span data-ttu-id="14f69-108">使用 [新增控制器] 功能表選項</span><span class="sxs-lookup"><span data-stu-id="14f69-108">Using the Add Controller Menu Option</span></span>

<span data-ttu-id="14f69-109">建立新控制器的最簡單方式是以滑鼠右鍵按一下 [Visual Studio 方案總管] 視窗中的 [控制器] 資料夾，然後選取 [**新增]、[控制器**] 功能表選項（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="14f69-109">The easiest way to create a new controller is to right-click the Controllers folder in the Visual Studio Solution Explorer window and select the **Add, Controller** menu option (see Figure 1).</span></span> <span data-ttu-id="14f69-110">選取此功能表選項會開啟 [**新增控制器**] 對話方塊（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="14f69-110">Selecting this menu option opens the **Add Controller** dialog (see Figure 2).</span></span>

<span data-ttu-id="14f69-111">[![[新增專案] 對話方塊](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="14f69-111">[![The New Project dialog box](creating-a-controller-cs/_static/image1.jpg)](creating-a-controller-cs/_static/image1.png)</span></span>

<span data-ttu-id="14f69-112">**圖 01**：新增控制器（[按一下以觀看完整大小的影像](creating-a-controller-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="14f69-112">**Figure 01**: Adding a new controller([Click to view full-size image](creating-a-controller-cs/_static/image2.png))</span></span>

<span data-ttu-id="14f69-113">[![[新增專案] 對話方塊](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="14f69-113">[![The New Project dialog box](creating-a-controller-cs/_static/image2.jpg)](creating-a-controller-cs/_static/image3.png)</span></span>

<span data-ttu-id="14f69-114">**圖 02**： [新增控制器] 對話方塊（[按一下以查看完整大小的影像](creating-a-controller-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="14f69-114">**Figure 02**: The Add Controller dialog ([Click to view full-size image](creating-a-controller-cs/_static/image4.png))</span></span>

<span data-ttu-id="14f69-115">請注意，控制器名稱的第一個部分會反白顯示在 [**新增控制器**] 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="14f69-115">Notice that the first part of the controller name is highlighted in the **Add Controller** dialog.</span></span> <span data-ttu-id="14f69-116">每個控制器名稱的結尾都必須是尾碼*控制器*。</span><span class="sxs-lookup"><span data-stu-id="14f69-116">Every controller name must end with the suffix *Controller*.</span></span> <span data-ttu-id="14f69-117">例如，您可以建立名為*ProductController*的控制器，而不是名為*Product*的控制器。</span><span class="sxs-lookup"><span data-stu-id="14f69-117">For example, you can create a controller named *ProductController* but not a controller named *Product*.</span></span>

<span data-ttu-id="14f69-118">如果您建立的控制器缺少*控制器*尾碼，則您將無法叫用控制器。</span><span class="sxs-lookup"><span data-stu-id="14f69-118">If you create a controller that is missing the *Controller* suffix then you won't be able to invoke the controller.</span></span> <span data-ttu-id="14f69-119">不要這麼做--我在犯此錯誤之後，浪費了無數小時的時間。</span><span class="sxs-lookup"><span data-stu-id="14f69-119">Don't do this -- I've wasted countless hours of my life after making this mistake.</span></span>

<span data-ttu-id="14f69-120">**清單 1-Controllers\ProductController.cs**</span><span class="sxs-lookup"><span data-stu-id="14f69-120">**Listing 1 - Controllers\ProductController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample1.cs)]

<span data-ttu-id="14f69-121">您應該一律在 [控制器] 資料夾中建立控制器。</span><span class="sxs-lookup"><span data-stu-id="14f69-121">You should always create controllers in the Controllers folder.</span></span> <span data-ttu-id="14f69-122">否則，您將違反 ASP.NET MVC 的慣例，而其他開發人員將會更容易瞭解您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="14f69-122">Otherwise, you'll be violating the conventions of ASP.NET MVC and other developers will have a more difficult time understanding your application.</span></span>

### <a name="scaffolding-action-methods"></a><span data-ttu-id="14f69-123">樣板動作方法</span><span class="sxs-lookup"><span data-stu-id="14f69-123">Scaffolding Action Methods</span></span>

<span data-ttu-id="14f69-124">當您建立控制器時，可以選擇自動產生 [建立]、[更新] 和 [詳細資料] 動作方法（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="14f69-124">When you create a controller, you have the option to generate Create, Update, and Details action methods automatically (see Figure 3).</span></span> <span data-ttu-id="14f69-125">如果您選取此選項，則會產生 [清單 2] 中的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="14f69-125">If you select this option then the controller class in Listing 2 is generated.</span></span>

<span data-ttu-id="14f69-126">[![自動建立動作方法](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="14f69-126">[![Creating action methods automatically](creating-a-controller-cs/_static/image3.jpg)](creating-a-controller-cs/_static/image5.png)</span></span>

<span data-ttu-id="14f69-127">**圖 03**：自動建立動作方法（[按一下以觀看完整大小的影像](creating-a-controller-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="14f69-127">**Figure 03**: Creating action methods automatically ([Click to view full-size image](creating-a-controller-cs/_static/image6.png))</span></span>

<span data-ttu-id="14f69-128">**清單 2-Controllers\CustomerController.cs**</span><span class="sxs-lookup"><span data-stu-id="14f69-128">**Listing 2 - Controllers\CustomerController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample2.cs)]

<span data-ttu-id="14f69-129">這些產生的方法都是存根方法。</span><span class="sxs-lookup"><span data-stu-id="14f69-129">These generated methods are stub methods.</span></span> <span data-ttu-id="14f69-130">您必須自行加入用來建立、更新和顯示客戶詳細資料的實際邏輯。</span><span class="sxs-lookup"><span data-stu-id="14f69-130">You must add the actual logic for creating, updating, and showing details for a customer yourself.</span></span> <span data-ttu-id="14f69-131">但是，存根方法提供了一個不錯的起點。</span><span class="sxs-lookup"><span data-stu-id="14f69-131">But, the stub methods provide you with a nice starting point.</span></span>

### <a name="creating-a-controller-class"></a><span data-ttu-id="14f69-132">建立控制器類別</span><span class="sxs-lookup"><span data-stu-id="14f69-132">Creating a Controller Class</span></span>

<span data-ttu-id="14f69-133">ASP.NET MVC 控制器只是一個類別。</span><span class="sxs-lookup"><span data-stu-id="14f69-133">The ASP.NET MVC controller is just a class.</span></span> <span data-ttu-id="14f69-134">如果您想要的話，可以忽略方便的 Visual Studio 控制器樣板，並手動建立控制器類別。</span><span class="sxs-lookup"><span data-stu-id="14f69-134">If you prefer, you can ignore the convenient Visual Studio controller scaffolding and create a controller class by hand.</span></span> <span data-ttu-id="14f69-135">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="14f69-135">Follow these steps:</span></span>

1. <span data-ttu-id="14f69-136">以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [新增] **、[新專案**] 功能表選項，然後選取 [**類別**] 範本（請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="14f69-136">Right-click the Controllers folder and select the menu option **Add, New Item** and select the **Class** template (see Figure 4).</span></span>
2. <span data-ttu-id="14f69-137">將新類別命名為 PersonController.cs，然後按一下 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="14f69-137">Name the new class PersonController.cs and click the **Add** button.</span></span>
3. <span data-ttu-id="14f69-138">修改產生的類別檔案，讓類別繼承自基底 System.web. Controller 類別（請參閱 [清單 3]）。</span><span class="sxs-lookup"><span data-stu-id="14f69-138">Modify the resulting class file so that the class inherits from the base System.Web.Mvc.Controller class (see Listing 3).</span></span>

<span data-ttu-id="14f69-139">[建立新類別 ![](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="14f69-139">[![Creating a new class](creating-a-controller-cs/_static/image4.jpg)](creating-a-controller-cs/_static/image7.png)</span></span>

<span data-ttu-id="14f69-140">**圖 04**：建立新的類別（[按一下以查看完整大小的影像](creating-a-controller-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="14f69-140">**Figure 04**: Creating a new class([Click to view full-size image](creating-a-controller-cs/_static/image8.png))</span></span>

<span data-ttu-id="14f69-141">**清單 3-Controllers\PersonController.cs**</span><span class="sxs-lookup"><span data-stu-id="14f69-141">**Listing 3 - Controllers\PersonController.cs**</span></span>

[!code-csharp[Main](creating-a-controller-cs/samples/sample3.cs)]

<span data-ttu-id="14f69-142">[清單 3] 中的控制器會公開一個名為 Index （）的動作，以傳回字串 "Hello World！"。</span><span class="sxs-lookup"><span data-stu-id="14f69-142">The controller in Listing 3 exposes one action named Index() that returns the string "Hello World!".</span></span> <span data-ttu-id="14f69-143">您可以藉由執行應用程式並要求如下所示的 URL 來叫用此控制器動作：</span><span class="sxs-lookup"><span data-stu-id="14f69-143">You can invoke this controller action by running your application and requesting a URL like the following:</span></span>

`http://localhost:40071/Person`

> [!NOTE]
> 
> <span data-ttu-id="14f69-144">ASP.NET 程式開發伺服器使用隨機埠號碼（例如，40071）。</span><span class="sxs-lookup"><span data-stu-id="14f69-144">The ASP.NET Development Server uses a random port number (for example, 40071).</span></span> <span data-ttu-id="14f69-145">輸入 URL 以叫用控制器時，您必須提供正確的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="14f69-145">When entering a URL to invoke a controller, you'll need to supply the right port number.</span></span> <span data-ttu-id="14f69-146">您可以將滑鼠游標移至 Windows 通知區域（畫面右下方）中的 ASP.NET 程式開發伺服器圖示上，藉以判斷埠號碼。</span><span class="sxs-lookup"><span data-stu-id="14f69-146">You can determine the port number by hovering your mouse over the icon for the ASP.NET Development Server in the Windows Notification Area (bottom-right of your screen).</span></span>
> 
> [!div class="step-by-step"]
> <span data-ttu-id="14f69-147">[上一頁](adding-dynamic-content-to-a-cached-page-cs.md)
> [下一頁](creating-an-action-cs.md)</span><span class="sxs-lookup"><span data-stu-id="14f69-147">[Previous](adding-dynamic-content-to-a-cached-page-cs.md)
[Next](creating-an-action-cs.md)</span></span>
