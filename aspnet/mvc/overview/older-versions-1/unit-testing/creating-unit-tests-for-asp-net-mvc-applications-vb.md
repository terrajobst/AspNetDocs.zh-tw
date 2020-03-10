---
uid: mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
title: 建立 ASP.NET MVC 應用程式的單元測試（VB） |Microsoft Docs
author: StephenWalther
description: 瞭解如何建立控制器動作的單元測試。 在本教學課程中，Stephen Walther 示範如何測試控制器動作是否會傳回 parti 。
ms.author: riande
ms.date: 08/19/2008
ms.assetid: eb35710d-1d99-44ac-b61f-e50af8cb328a
msc.legacyurl: /mvc/overview/older-versions-1/unit-testing/creating-unit-tests-for-asp-net-mvc-applications-vb
msc.type: authoredcontent
ms.openlocfilehash: 643faddaf6f9cd075131e8e5a9cccb303e355ceb
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78541430"
---
# <a name="creating-unit-tests-for-aspnet-mvc-applications-vb"></a><span data-ttu-id="4ec82-104">建立 ASP.NET MVC 應用程式的單元測試 (VB)</span><span class="sxs-lookup"><span data-stu-id="4ec82-104">Creating Unit Tests for ASP.NET MVC Applications (VB)</span></span>

<span data-ttu-id="4ec82-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="4ec82-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="4ec82-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="4ec82-106">Download PDF</span></span>](https://download.microsoft.com/download/8/4/8/84843d8d-1575-426c-bcb5-9d0c42e51416/ASPNET_MVC_Tutorial_07_VB.pdf)

> <span data-ttu-id="4ec82-107">瞭解如何建立控制器動作的單元測試。</span><span class="sxs-lookup"><span data-stu-id="4ec82-107">Learn how to create unit tests for controller actions.</span></span> <span data-ttu-id="4ec82-108">在本教學課程中，Stephen Walther 示範如何測試控制器動作是否會傳回特定的視圖、傳回一組特定的資料，或傳回不同類型的動作結果。</span><span class="sxs-lookup"><span data-stu-id="4ec82-108">In this tutorial, Stephen Walther demonstrates how to test whether a controller action returns a particular view, returns a particular set of data, or returns a different type of action result.</span></span>

<span data-ttu-id="4ec82-109">本教學課程的目的是要示範如何為 ASP.NET MVC 應用程式中的控制器撰寫單元測試。</span><span class="sxs-lookup"><span data-stu-id="4ec82-109">The goal of this tutorial is to demonstrate how you can write unit tests for the controllers in your ASP.NET MVC applications.</span></span> <span data-ttu-id="4ec82-110">我們會討論如何建立三種不同類型的單元測試。</span><span class="sxs-lookup"><span data-stu-id="4ec82-110">We discuss how to build three different types of unit tests.</span></span> <span data-ttu-id="4ec82-111">您將瞭解如何測試控制器動作所傳回的視圖、如何測試控制器動作所傳回的 View 資料，以及如何測試某個控制器動作是否會將您重新導向至第二個控制器動作。</span><span class="sxs-lookup"><span data-stu-id="4ec82-111">You learn how to test the view returned by a controller action, how to test the View Data returned by a controller action, and how to test whether or not one controller action redirects you to a second controller action.</span></span>

## <a name="creating-the-controller-under-test"></a><span data-ttu-id="4ec82-112">建立受測試的控制器</span><span class="sxs-lookup"><span data-stu-id="4ec82-112">Creating the Controller under Test</span></span>

<span data-ttu-id="4ec82-113">讓我們從建立要測試的控制器開始。</span><span class="sxs-lookup"><span data-stu-id="4ec82-113">Let's start by creating the controller that we intend to test.</span></span> <span data-ttu-id="4ec82-114">名為 `ProductController`的控制器包含在 [清單 1] 中。</span><span class="sxs-lookup"><span data-stu-id="4ec82-114">The controller, named the `ProductController`, is contained in Listing 1.</span></span>

<span data-ttu-id="4ec82-115">**清單1– `ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="4ec82-115">**Listing 1 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample1.vb)]

<span data-ttu-id="4ec82-116">`ProductController` 包含兩個名為 `Index()` 和 `Details()`的動作方法。</span><span class="sxs-lookup"><span data-stu-id="4ec82-116">The `ProductController` contains two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="4ec82-117">這兩個動作方法都會傳回一個視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-117">Both action methods return a view.</span></span> <span data-ttu-id="4ec82-118">請注意，[`Details()`] 動作會接受名為 [識別碼] 的參數。</span><span class="sxs-lookup"><span data-stu-id="4ec82-118">Notice that the `Details()` action accepts a parameter named Id.</span></span>

## <a name="testing-the-view-returned-by-a-controller"></a><span data-ttu-id="4ec82-119">測試控制器所傳回的視圖</span><span class="sxs-lookup"><span data-stu-id="4ec82-119">Testing the View returned by a Controller</span></span>

<span data-ttu-id="4ec82-120">假設我們想要測試 `ProductController` 是否會傳回正確的視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-120">Imagine that we want to test whether or not the `ProductController` returns the right view.</span></span> <span data-ttu-id="4ec82-121">我們想要確保叫用 `ProductController.Details()` 動作時，會傳回詳細資料檢視。</span><span class="sxs-lookup"><span data-stu-id="4ec82-121">We want to make sure that when the `ProductController.Details()` action is invoked, the Details view is returned.</span></span> <span data-ttu-id="4ec82-122">[清單 2] 中的測試類別包含測試 `ProductController.Details()` 動作所傳回之視圖的單元測試。</span><span class="sxs-lookup"><span data-stu-id="4ec82-122">The test class in Listing 2 contains a unit test for testing the view returned by the `ProductController.Details()` action.</span></span>

<span data-ttu-id="4ec82-123">**清單2– `ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="4ec82-123">**Listing 2 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample2.vb)]

<span data-ttu-id="4ec82-124">[清單 2] 中的類別包含名為 `TestDetailsView()`的測試方法。</span><span class="sxs-lookup"><span data-stu-id="4ec82-124">The class in Listing 2 includes a test method named `TestDetailsView()`.</span></span> <span data-ttu-id="4ec82-125">這個方法包含三行程式碼。</span><span class="sxs-lookup"><span data-stu-id="4ec82-125">This method contains three lines of code.</span></span> <span data-ttu-id="4ec82-126">第一行程式碼會建立 `ProductController` 類別的新實例。</span><span class="sxs-lookup"><span data-stu-id="4ec82-126">The first line of code creates a new instance of the `ProductController` class.</span></span> <span data-ttu-id="4ec82-127">第二行程式碼會叫用控制器的 `Details()` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="4ec82-127">The second line of code invokes the controller's `Details()` action method.</span></span> <span data-ttu-id="4ec82-128">最後，程式碼的最後一行會檢查 `Details()` 動作所傳回的視圖是否為詳細資料檢視。</span><span class="sxs-lookup"><span data-stu-id="4ec82-128">Finally, the last line of code checks whether or not the view returned by the `Details()` action is the Details view.</span></span>

<span data-ttu-id="4ec82-129">`ViewResult.ViewName` 屬性代表控制器傳回的視圖名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec82-129">The `ViewResult.ViewName` property represents the name of the view returned by a controller.</span></span> <span data-ttu-id="4ec82-130">關於測試這個屬性的一個重大警告。</span><span class="sxs-lookup"><span data-stu-id="4ec82-130">One big warning about testing this property.</span></span> <span data-ttu-id="4ec82-131">有兩種方式可讓控制器傳回一個視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-131">There are two ways that a controller can return a view.</span></span> <span data-ttu-id="4ec82-132">控制器可以明確地傳回如下所示的視圖：</span><span class="sxs-lookup"><span data-stu-id="4ec82-132">A controller can explicitly return a view like this:</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample3.vb)]

<span data-ttu-id="4ec82-133">或者，您也可以從控制器動作的名稱推斷視圖名稱，如下所示：</span><span class="sxs-lookup"><span data-stu-id="4ec82-133">Alternatively, the name of the view can be inferred from the name of the controller action like this:</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample4.vb)]

<span data-ttu-id="4ec82-134">此控制器動作也會傳回名為 `Details`的視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-134">This controller action also returns a view named `Details`.</span></span> <span data-ttu-id="4ec82-135">不過，此視圖的名稱是從動作名稱推斷而來。</span><span class="sxs-lookup"><span data-stu-id="4ec82-135">However, the name of the view is inferred from the action name.</span></span> <span data-ttu-id="4ec82-136">如果您想要測試檢視名稱，則必須明確地從控制器動作傳回視圖名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec82-136">If you want to test the view name, then you must explicitly return the view name from the controller action.</span></span>

<span data-ttu-id="4ec82-137">您可以透過輸入鍵盤組合**Ctrl-R、** 或按一下 [**在方案中執行所有測試**] 按鈕（請參閱 [圖 1]）來執行 [清單 2] 中的單元測試。</span><span class="sxs-lookup"><span data-stu-id="4ec82-137">You can run the unit test in Listing 2 by either entering the keyboard combination **Ctrl-R, A** or by clicking the **Run All Tests in Solution** button (see Figure 1).</span></span> <span data-ttu-id="4ec82-138">如果測試成功，您會看到 [圖 2] 中的 [測試結果] 視窗。</span><span class="sxs-lookup"><span data-stu-id="4ec82-138">If the test passes, you'll see the Test Results window in Figure 2.</span></span>

<span data-ttu-id="4ec82-139">[![在方案中執行所有測試](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="4ec82-139">[![Run All Tests in Solution](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image2.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image1.png)</span></span>

<span data-ttu-id="4ec82-140">**圖 01**：在方案中執行所有測試（[按一下以查看完整大小的影像](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="4ec82-140">**Figure 01**: Run All Tests in Solution ([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image3.png))</span></span>

<span data-ttu-id="4ec82-141">[![成功！](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4ec82-141">[![Success!](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image5.png)](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image4.png)</span></span>

<span data-ttu-id="4ec82-142">**圖 02**：成功！</span><span class="sxs-lookup"><span data-stu-id="4ec82-142">**Figure 02**: Success!</span></span> <span data-ttu-id="4ec82-143">（[按一下以查看完整大小的影像](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="4ec82-143">([Click to view full-size image](creating-unit-tests-for-asp-net-mvc-applications-vb/_static/image6.png))</span></span>

## <a name="testing-the-view-data-returned-by-a-controller"></a><span data-ttu-id="4ec82-144">測試控制器所傳回的 View 資料</span><span class="sxs-lookup"><span data-stu-id="4ec82-144">Testing the View Data returned by a Controller</span></span>

<span data-ttu-id="4ec82-145">MVC 控制器會使用稱為 *`View Data`* 的內容，將資料傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-145">An MVC controller passes data to a view by using something called *`View Data`*.</span></span> <span data-ttu-id="4ec82-146">例如，假設您想要在叫用 `ProductController Details()` 動作時，顯示特定產品的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="4ec82-146">For example, imagine that you want to display the details for a particular product when you invoke the `ProductController Details()` action.</span></span> <span data-ttu-id="4ec82-147">在此情況下，您可以建立 `Product` 類別的實例（定義于模型中），並利用 `View Data`來將實例傳遞至 `Details` 視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-147">In that case, you can create an instance of a `Product` class (defined in your model) and pass the instance to the `Details` view by taking advantage of `View Data`.</span></span>

<span data-ttu-id="4ec82-148">[清單 3] 中修改過的 `ProductController` 包含會傳回產品的已更新 `Details()` 動作。</span><span class="sxs-lookup"><span data-stu-id="4ec82-148">The modified `ProductController` in Listing 3 includes an updated `Details()` action that returns a Product.</span></span>

<span data-ttu-id="4ec82-149">**清單3– `ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="4ec82-149">**Listing 3 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample5.vb)]

<span data-ttu-id="4ec82-150">首先，`Details()` 動作會建立代表膝上型電腦的 `Product` 類別的新實例。</span><span class="sxs-lookup"><span data-stu-id="4ec82-150">First, the `Details()` action creates a new instance of the `Product` class that represents a laptop computer.</span></span> <span data-ttu-id="4ec82-151">接下來，`Product` 類別的實例會當做第二個參數傳遞至 `View()` 方法。</span><span class="sxs-lookup"><span data-stu-id="4ec82-151">Next, the instance of the `Product` class is passed as the second parameter to the `View()` method.</span></span>

<span data-ttu-id="4ec82-152">您可以撰寫單元測試來測試預期的資料是否包含在視圖資料中。</span><span class="sxs-lookup"><span data-stu-id="4ec82-152">You can write unit tests to test whether the expected data is contained in view data.</span></span> <span data-ttu-id="4ec82-153">[清單 4] 中的單元測試會在您呼叫 `ProductController Details()` 動作方法時，測試是否會傳回代表膝上型電腦的產品。</span><span class="sxs-lookup"><span data-stu-id="4ec82-153">The unit test in Listing 4 tests whether or not a Product representing a laptop computer is returned when you call the `ProductController Details()` action method.</span></span>

<span data-ttu-id="4ec82-154">**清單4– `ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="4ec82-154">**Listing 4 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample6.vb)]

<span data-ttu-id="4ec82-155">在 [清單 4] 中，`TestDetailsView()` 方法會測試藉由叫用 `Details()` 方法所傳回的 View 資料。</span><span class="sxs-lookup"><span data-stu-id="4ec82-155">In Listing 4, the `TestDetailsView()` method tests the View Data returned by invoking the `Details()` method.</span></span> <span data-ttu-id="4ec82-156">`ViewData` 會在叫用 `Details()` 方法所傳回的 `ViewResult` 上公開為屬性。</span><span class="sxs-lookup"><span data-stu-id="4ec82-156">The `ViewData` is exposed as a property on the `ViewResult` returned by invoking the `Details()` method.</span></span> <span data-ttu-id="4ec82-157">`ViewData.Model` 屬性包含傳遞至視圖的產品。</span><span class="sxs-lookup"><span data-stu-id="4ec82-157">The `ViewData.Model` property contains the product passed to the view.</span></span> <span data-ttu-id="4ec82-158">測試只會驗證封裝含在 View 資料中的產品具有名稱 [膝上型電腦]。</span><span class="sxs-lookup"><span data-stu-id="4ec82-158">The test simply verifies that the product contained in the View Data has the name Laptop.</span></span>

## <a name="testing-the-action-result-returned-by-a-controller"></a><span data-ttu-id="4ec82-159">測試控制器所傳回的動作結果</span><span class="sxs-lookup"><span data-stu-id="4ec82-159">Testing the Action Result returned by a Controller</span></span>

<span data-ttu-id="4ec82-160">較複雜的控制器動作可能會根據傳遞至控制器動作的參數值，傳回不同類型的動作結果。</span><span class="sxs-lookup"><span data-stu-id="4ec82-160">A more complex controller action might return different types of action results depending on the values of the parameters passed to the controller action.</span></span> <span data-ttu-id="4ec82-161">控制器動作可以傳回各種類型的動作結果，包括 `ViewResult`、`RedirectToRouteResult`或 `JsonResult`。</span><span class="sxs-lookup"><span data-stu-id="4ec82-161">A controller action can return a variety of types of action results including a `ViewResult`, `RedirectToRouteResult`, or `JsonResult`.</span></span>

<span data-ttu-id="4ec82-162">例如，當您將有效的產品識別碼傳遞給動作時，[清單 5] 中的 [修改的 `Details()`] 動作會傳回 [`Details`] 視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-162">For example, the modified `Details()` action in Listing 5 returns the `Details` view when you pass a valid product Id to the action.</span></span> <span data-ttu-id="4ec82-163">如果您傳遞不正確產品識別碼--值小於1的識別碼，則會將您重新導向至 `Index()` 動作。</span><span class="sxs-lookup"><span data-stu-id="4ec82-163">If you pass an invalid product Id -- an Id with a value less than 1 -- then you are redirected to the `Index()` action.</span></span>

<span data-ttu-id="4ec82-164">**清單5– `ProductController.vb`**</span><span class="sxs-lookup"><span data-stu-id="4ec82-164">**Listing 5 – `ProductController.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample7.vb)]

<span data-ttu-id="4ec82-165">您可以使用 [清單 6] 中的單元測試來測試 `Details()` 動作的行為。</span><span class="sxs-lookup"><span data-stu-id="4ec82-165">You can test the behavior of the `Details()` action with the unit test in Listing 6.</span></span> <span data-ttu-id="4ec82-166">[清單 6] 中的單元測試會在將值為-1 的識別碼傳遞給 `Details()` 方法時，確認您已重新導向至 `Index` 視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-166">The unit test in Listing 6 verifies that you are redirected to the `Index` view when an Id with the value -1 is passed to the `Details()` method.</span></span>

<span data-ttu-id="4ec82-167">**清單6– `ProductControllerTest.vb`**</span><span class="sxs-lookup"><span data-stu-id="4ec82-167">**Listing 6 – `ProductControllerTest.vb`**</span></span>

[!code-vb[Main](creating-unit-tests-for-asp-net-mvc-applications-vb/samples/sample8.vb)]

<span data-ttu-id="4ec82-168">當您在控制器動作中呼叫 `RedirectToAction()` 方法時，控制器動作會傳回 `RedirectToRouteResult`。</span><span class="sxs-lookup"><span data-stu-id="4ec82-168">When you call the `RedirectToAction()` method in a controller action, the controller action returns a `RedirectToRouteResult`.</span></span> <span data-ttu-id="4ec82-169">測試會檢查 `RedirectToRouteResult` 是否會將使用者重新導向至名為 `Index`的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="4ec82-169">The test checks whether the `RedirectToRouteResult` will redirect the user to a controller action named `Index`.</span></span>

## <a name="summary"></a><span data-ttu-id="4ec82-170">總結</span><span class="sxs-lookup"><span data-stu-id="4ec82-170">Summary</span></span>

<span data-ttu-id="4ec82-171">在本教學課程中，您已瞭解如何建立 MVC 控制器動作的單元測試。</span><span class="sxs-lookup"><span data-stu-id="4ec82-171">In this tutorial, you learned how to build unit tests for MVC controller actions.</span></span> <span data-ttu-id="4ec82-172">首先，您已瞭解如何確認控制器動作是否傳回正確的視圖。</span><span class="sxs-lookup"><span data-stu-id="4ec82-172">First, you learned how to verify whether the right view is returned by a controller action.</span></span> <span data-ttu-id="4ec82-173">您已瞭解如何使用 `ViewResult.ViewName` 屬性來驗證視圖的名稱。</span><span class="sxs-lookup"><span data-stu-id="4ec82-173">You learned how to use the `ViewResult.ViewName` property to verify the name of a view.</span></span>

<span data-ttu-id="4ec82-174">接下來，我們會探討如何測試 `View Data`的內容。</span><span class="sxs-lookup"><span data-stu-id="4ec82-174">Next, we examined how you can test the contents of `View Data`.</span></span> <span data-ttu-id="4ec82-175">您已瞭解如何在呼叫控制器動作之後，檢查 `View Data` 中是否傳回正確的產品。</span><span class="sxs-lookup"><span data-stu-id="4ec82-175">You learned how to check whether the right product was returned in `View Data` after calling a controller action.</span></span>

<span data-ttu-id="4ec82-176">最後，我們會討論如何測試控制器動作是否傳回不同類型的動作結果。</span><span class="sxs-lookup"><span data-stu-id="4ec82-176">Finally, we discussed how you can test whether different types of action results are returned from a controller action.</span></span> <span data-ttu-id="4ec82-177">您已瞭解如何測試控制器是否會傳回 `ViewResult` 或 `RedirectToRouteResult`。</span><span class="sxs-lookup"><span data-stu-id="4ec82-177">You learned how to test whether a controller returns a `ViewResult` or a `RedirectToRouteResult`.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="4ec82-178">上一篇</span><span class="sxs-lookup"><span data-stu-id="4ec82-178">Previous</span></span>](creating-unit-tests-for-asp-net-mvc-applications-cs.md)
