---
uid: mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
title: 將資料傳遞給 View 主版頁面（VB） |Microsoft Docs
author: microsoft
description: 本教學課程的目的是要說明如何將資料從控制器傳遞至視圖主版頁面。 我們會檢查兩個將資料傳送到 view m 的策略 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: 37a1ebae-8773-408f-8645-d21da7ff9ae1
msc.legacyurl: /mvc/overview/older-versions-1/views/passing-data-to-view-master-pages-vb
msc.type: authoredcontent
ms.openlocfilehash: 9f768f47557adedc43cebfa2c092014bba5842de
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74593745"
---
# <a name="passing-data-to-view-master-pages-vb"></a><span data-ttu-id="3227b-104">將資料傳遞至檢視主版頁面 (VB)</span><span class="sxs-lookup"><span data-stu-id="3227b-104">Passing Data to View Master Pages (VB)</span></span>

<span data-ttu-id="3227b-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3227b-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3227b-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="3227b-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_13_VB.pdf)

> <span data-ttu-id="3227b-107">本教學課程的目的是要說明如何將資料從控制器傳遞至視圖主版頁面。</span><span class="sxs-lookup"><span data-stu-id="3227b-107">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="3227b-108">我們會檢查兩個將資料傳送至視圖主版頁面的策略。</span><span class="sxs-lookup"><span data-stu-id="3227b-108">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="3227b-109">首先，我們會討論一個簡單的解決方案，會導致應用程式變得很難維護。</span><span class="sxs-lookup"><span data-stu-id="3227b-109">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="3227b-110">接下來，我們會檢查更好的解決方案，需要更多的初始工作，但會產生更容易維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3227b-110">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

## <a name="passing-data-to-view-master-pages"></a><span data-ttu-id="3227b-111">傳遞資料以觀看主版頁面</span><span class="sxs-lookup"><span data-stu-id="3227b-111">Passing Data to View Master Pages</span></span>

<span data-ttu-id="3227b-112">本教學課程的目的是要說明如何將資料從控制器傳遞至視圖主版頁面。</span><span class="sxs-lookup"><span data-stu-id="3227b-112">The goal of this tutorial is to explain how you can pass data from a controller to a view master page.</span></span> <span data-ttu-id="3227b-113">我們會檢查兩個將資料傳送至視圖主版頁面的策略。</span><span class="sxs-lookup"><span data-stu-id="3227b-113">We examine two strategies for passing data to a view master page.</span></span> <span data-ttu-id="3227b-114">首先，我們會討論一個簡單的解決方案，會導致應用程式變得很難維護。</span><span class="sxs-lookup"><span data-stu-id="3227b-114">First, we discuss an easy solution that results in an application that is difficult to maintain.</span></span> <span data-ttu-id="3227b-115">接下來，我們會檢查更好的解決方案，需要更多的初始工作，但會產生更容易維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3227b-115">Next, we examine a much better solution that requires a little more initial work but results in a much more maintainable application.</span></span>

### <a name="the-problem"></a><span data-ttu-id="3227b-116">問題</span><span class="sxs-lookup"><span data-stu-id="3227b-116">The Problem</span></span>

<span data-ttu-id="3227b-117">假設您正在建立電影資料庫應用程式，而且想要在應用程式的每一頁上顯示電影類別清單（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="3227b-117">Imagine that you are building a movie database application and you want to display the list of movie categories on every page in your application (see Figure 1).</span></span> <span data-ttu-id="3227b-118">另外，想像一下電影類別目錄的清單是儲存在資料庫資料表中。</span><span class="sxs-lookup"><span data-stu-id="3227b-118">Imagine, furthermore, that the list of movie categories is stored in a database table.</span></span> <span data-ttu-id="3227b-119">在這種情況下，從資料庫中取出類別目錄，並在視圖主版頁面中轉譯電影類別目錄是有意義的。</span><span class="sxs-lookup"><span data-stu-id="3227b-119">In that case, it would make sense to retrieve the categories from the database and render the list of movie categories within a view master page.</span></span>

<span data-ttu-id="3227b-120">[![在視圖主版頁面中顯示電影類別](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3227b-120">[![Displaying movie categories in a view master page](passing-data-to-view-master-pages-vb/_static/image2.png)](passing-data-to-view-master-pages-vb/_static/image1.png)</span></span>

<span data-ttu-id="3227b-121">**圖 01**：在視圖主版頁面中顯示電影類別（[按一下以觀看完整大小的影像](passing-data-to-view-master-pages-vb/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="3227b-121">**Figure 01**: Displaying movie categories in a view master page ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image3.png))</span></span>

<span data-ttu-id="3227b-122">這是問題所在。</span><span class="sxs-lookup"><span data-stu-id="3227b-122">Here's the problem.</span></span> <span data-ttu-id="3227b-123">如何在主版頁面中取出電影類別目錄清單？</span><span class="sxs-lookup"><span data-stu-id="3227b-123">How do you retrieve the list of movie categories in the master page?</span></span> <span data-ttu-id="3227b-124">直接在主版頁面中呼叫模型類別的方法相當吸引人。</span><span class="sxs-lookup"><span data-stu-id="3227b-124">It is tempting to call methods of your model classes in the master page directly.</span></span> <span data-ttu-id="3227b-125">換句話說，在主版頁面中包含用來從資料庫中抓取資料的程式碼很有吸引力。</span><span class="sxs-lookup"><span data-stu-id="3227b-125">In other words, it is tempting to include the code for retrieving the data from the database right in your master page.</span></span> <span data-ttu-id="3227b-126">不過，略過您的 MVC 控制器來存取資料庫，會違反建立 MVC 應用程式的主要優點之一，這是完全分離的問題。</span><span class="sxs-lookup"><span data-stu-id="3227b-126">However, bypassing your MVC controllers to access the database would violate the clean separation of concerns that is one of the primary benefits of building an MVC application.</span></span>

<span data-ttu-id="3227b-127">在 MVC 應用程式中，您想要讓 mvc 視圖和 MVC 模型之間的所有互動都由 MVC 控制器處理。</span><span class="sxs-lookup"><span data-stu-id="3227b-127">In an MVC application, you want all interaction between your MVC views and your MVC model to be handled by your MVC controllers.</span></span> <span data-ttu-id="3227b-128">這項顧慮的分離會導致更容易維護、可調整且可測試的應用程式。</span><span class="sxs-lookup"><span data-stu-id="3227b-128">This separation of concerns results in a more maintainable, adaptable, and testable application.</span></span>

<span data-ttu-id="3227b-129">在 MVC 應用程式中，傳遞至視圖的所有資料（包括視圖主版頁面）都應該透過控制器動作傳遞至視圖。</span><span class="sxs-lookup"><span data-stu-id="3227b-129">In an MVC application, all data passed to a view – including a view master page – should be passed to a view by a controller action.</span></span> <span data-ttu-id="3227b-130">此外，您應該利用視圖資料來傳遞資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-130">Furthermore, the data should be passed by taking advantage of view data.</span></span> <span data-ttu-id="3227b-131">在本教學課程的其餘部分，我將探討兩種將 view 資料傳遞至視圖主版頁面的方法。</span><span class="sxs-lookup"><span data-stu-id="3227b-131">In the remainder of this tutorial, I examine two methods of passing view data to a view master page.</span></span>

### <a name="the-simple-solution"></a><span data-ttu-id="3227b-132">簡單的解決方案</span><span class="sxs-lookup"><span data-stu-id="3227b-132">The Simple Solution</span></span>

<span data-ttu-id="3227b-133">讓我們從一個最簡單的解決方案開始，將視圖資料從控制器傳遞至視圖主版頁面。</span><span class="sxs-lookup"><span data-stu-id="3227b-133">Let's start with the simplest solution to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="3227b-134">最簡單的解決方法是在每個控制器動作中傳遞主版頁面的視圖資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-134">The simplest solution is to pass the view data for the master page in each and every controller action.</span></span>

<span data-ttu-id="3227b-135">請考慮 [清單 1] 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="3227b-135">Consider the controller in Listing 1.</span></span> <span data-ttu-id="3227b-136">它會公開名為 `Index()` 和 `Details()`的兩個動作。</span><span class="sxs-lookup"><span data-stu-id="3227b-136">It exposes two actions named `Index()` and `Details()`.</span></span> <span data-ttu-id="3227b-137">`Index()` 動作方法會傳回電影資料庫資料表中的每一部電影。</span><span class="sxs-lookup"><span data-stu-id="3227b-137">The `Index()` action method returns every movie in the Movies database table.</span></span> <span data-ttu-id="3227b-138">`Details()` 動作方法會傳回特定電影類別中的每一部電影。</span><span class="sxs-lookup"><span data-stu-id="3227b-138">The `Details()` action method returns every movie in a particular movie category.</span></span>

<span data-ttu-id="3227b-139">**清單1– `Controllers\HomeController.vb`**</span><span class="sxs-lookup"><span data-stu-id="3227b-139">**Listing 1 – `Controllers\HomeController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample1.vb)]

<span data-ttu-id="3227b-140">請注意，`Index()` 和 `Details()` 動作都會加入兩個專案來查看資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-140">Notice that both the `Index()` and the `Details()` actions add two items to view data.</span></span> <span data-ttu-id="3227b-141">`Index()` 動作會新增兩個索引鍵：分類和電影。</span><span class="sxs-lookup"><span data-stu-id="3227b-141">The `Index()` action adds two keys: categories and movies.</span></span> <span data-ttu-id="3227b-142">[類別目錄] 索引鍵代表視圖主版頁面所顯示的電影類別目錄清單。</span><span class="sxs-lookup"><span data-stu-id="3227b-142">The categories key represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="3227b-143">電影金鑰代表索引視圖頁面所顯示的電影清單。</span><span class="sxs-lookup"><span data-stu-id="3227b-143">The movies key represents the list of movies displayed by the Index view page.</span></span>

<span data-ttu-id="3227b-144">[`Details()`] 動作也會新增兩個名為 [類別和電影] 的機碼。</span><span class="sxs-lookup"><span data-stu-id="3227b-144">The `Details()` action also adds two keys named categories and movies.</span></span> <span data-ttu-id="3227b-145">[類別目錄] 索引鍵同樣地代表 [視圖主版] 頁面所顯示的電影類別目錄清單。</span><span class="sxs-lookup"><span data-stu-id="3227b-145">The categories key, once again, represents the list of movie categories displayed by the view master page.</span></span> <span data-ttu-id="3227b-146">電影金鑰代表詳細資料檢視頁面所顯示之特定類別中的電影清單（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="3227b-146">The movies key represents the list of movies in a particular category displayed by the Details view page (see Figure 2).</span></span>

<span data-ttu-id="3227b-147">[![詳細資料檢視](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3227b-147">[![The Details view](passing-data-to-view-master-pages-vb/_static/image5.png)](passing-data-to-view-master-pages-vb/_static/image4.png)</span></span>

<span data-ttu-id="3227b-148">**圖 02**：詳細資料檢視（[按一下以查看完整大小的影像](passing-data-to-view-master-pages-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="3227b-148">**Figure 02**: The Details view ([Click to view full-size image](passing-data-to-view-master-pages-vb/_static/image6.png))</span></span>

<span data-ttu-id="3227b-149">索引視圖包含在 [清單 2] 中。</span><span class="sxs-lookup"><span data-stu-id="3227b-149">The Index view is contained in Listing 2.</span></span> <span data-ttu-id="3227b-150">它只會逐一查看 [觀看資料] 中 [電影] 專案所代表的電影清單。</span><span class="sxs-lookup"><span data-stu-id="3227b-150">It simply iterates through the list of movies represented by the movies item in view data.</span></span>

<span data-ttu-id="3227b-151">**清單2– `Views\Home\Index.aspx`**</span><span class="sxs-lookup"><span data-stu-id="3227b-151">**Listing 2 – `Views\Home\Index.aspx`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample2.aspx)]

<span data-ttu-id="3227b-152">[視圖主版] 頁面包含在 [清單 3] 中。</span><span class="sxs-lookup"><span data-stu-id="3227b-152">The view master page is contained in Listing 3.</span></span> <span data-ttu-id="3227b-153">[視圖主版] 頁面會逐一查看並轉譯 [視圖資料] 中類別專案所代表的所有電影類別目錄。</span><span class="sxs-lookup"><span data-stu-id="3227b-153">The view master page iterates and renders all of the movie categories represented by the categories item from view data.</span></span>

<span data-ttu-id="3227b-154">**清單3– `Views\Shared\Site.master`**</span><span class="sxs-lookup"><span data-stu-id="3227b-154">**Listing 3 – `Views\Shared\Site.master`**</span></span>

[!code-aspx[Main](passing-data-to-view-master-pages-vb/samples/sample3.aspx)]

<span data-ttu-id="3227b-155">所有資料都會透過視圖資料傳遞至視圖和視圖主版頁面。</span><span class="sxs-lookup"><span data-stu-id="3227b-155">All data is passed to the view and the view master page through view data.</span></span> <span data-ttu-id="3227b-156">這是將資料傳遞至主版頁面的正確方式。</span><span class="sxs-lookup"><span data-stu-id="3227b-156">That is the correct way to pass data to the master page.</span></span>

<span data-ttu-id="3227b-157">那麼，這個解決方案有什麼問題呢？</span><span class="sxs-lookup"><span data-stu-id="3227b-157">So, what's wrong with this solution?</span></span> <span data-ttu-id="3227b-158">問題在於，此解決方案違反了試（不重複原則）原則。</span><span class="sxs-lookup"><span data-stu-id="3227b-158">The problem is that this solution violates the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="3227b-159">每個控制器動作都必須新增相同的電影類別清單來查看資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-159">Each and every controller action must add the very same list of movie categories to view data.</span></span> <span data-ttu-id="3227b-160">在您的應用程式中擁有重複的程式碼，可讓您的應用程式更難以維護、調整和修改。</span><span class="sxs-lookup"><span data-stu-id="3227b-160">Having duplicate code in your application makes your application much more difficult to maintain, adapt, and modify.</span></span>

### <a name="the-good-solution"></a><span data-ttu-id="3227b-161">良好的解決方案</span><span class="sxs-lookup"><span data-stu-id="3227b-161">The Good Solution</span></span>

<span data-ttu-id="3227b-162">在本節中，我們會探討將資料從控制器動作傳遞至視圖主版頁面的替代方案和更好的解決方案。</span><span class="sxs-lookup"><span data-stu-id="3227b-162">In this section, we examine an alternative, and better, solution to passing data from a controller action to a view master page.</span></span> <span data-ttu-id="3227b-163">我們不會在每個控制器動作中新增主版頁面的電影類別，而是只將電影類別新增至 view 資料一次。</span><span class="sxs-lookup"><span data-stu-id="3227b-163">Instead of adding the movie categories for the master page in each and every controller action, we add the movie categories to the view data only once.</span></span> <span data-ttu-id="3227b-164">視圖主版頁面所使用的所有視圖資料都會加入應用程式控制器中。</span><span class="sxs-lookup"><span data-stu-id="3227b-164">All view data used by the view master page is added in an Application controller.</span></span>

<span data-ttu-id="3227b-165">ApplicationController 類別包含在 [清單 4] 中。</span><span class="sxs-lookup"><span data-stu-id="3227b-165">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="3227b-166">ApplicationController 類別包含在 [清單 4] 中。</span><span class="sxs-lookup"><span data-stu-id="3227b-166">The ApplicationController class is contained in Listing 4.</span></span>

<span data-ttu-id="3227b-167">**清單4– `Controllers\ApplicationController.vb`**</span><span class="sxs-lookup"><span data-stu-id="3227b-167">**Listing 4 – `Controllers\ApplicationController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample4.vb)]

<span data-ttu-id="3227b-168">在 [清單 4] 中，您應該會看到關於應用程式控制器的三件事。</span><span class="sxs-lookup"><span data-stu-id="3227b-168">There are three things that you should notice about the Application controller in Listing 4.</span></span> <span data-ttu-id="3227b-169">首先，請注意，類別繼承自基底 System.web. Mvc 類別。</span><span class="sxs-lookup"><span data-stu-id="3227b-169">First, notice that the class inherits from the base System.Web.Mvc.Controller class.</span></span> <span data-ttu-id="3227b-170">應用程式控制器是控制器類別。</span><span class="sxs-lookup"><span data-stu-id="3227b-170">The Application controller is a controller class.</span></span>

<span data-ttu-id="3227b-171">第二，請注意，應用程式控制器類別是 MustInherit 類別。</span><span class="sxs-lookup"><span data-stu-id="3227b-171">Second, notice that the Application controller class is a MustInherit class.</span></span> <span data-ttu-id="3227b-172">MustInherit 類別是一個類別，必須由實體類別來執行。</span><span class="sxs-lookup"><span data-stu-id="3227b-172">An MustInherit class is a class that must be implemented by a concrete class.</span></span> <span data-ttu-id="3227b-173">因為應用程式控制器是 MustInherit 類別，所以您無法直接叫用在類別中定義的任何方法。</span><span class="sxs-lookup"><span data-stu-id="3227b-173">Because the Application controller is an MustInherit class, you cannot not invoke any methods defined in the class directly.</span></span> <span data-ttu-id="3227b-174">如果您嘗試直接叫用應用程式類別，則會出現「找不到資源」的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="3227b-174">If you attempt to invoke the Application class directly then you'll get a Resource Cannot Be Found error message.</span></span>

<span data-ttu-id="3227b-175">第三，請注意，應用程式控制器包含一個可新增電影類別清單以查看資料的函式。</span><span class="sxs-lookup"><span data-stu-id="3227b-175">Third, notice that the Application controller contains a constructor that adds the list of movie categories to view data.</span></span> <span data-ttu-id="3227b-176">繼承自應用程式控制器的每個控制器類別都會自動呼叫應用程式控制器的函式。</span><span class="sxs-lookup"><span data-stu-id="3227b-176">Every controller class that inherits from the Application controller calls the Application controller's constructor automatically.</span></span> <span data-ttu-id="3227b-177">每當您在任何繼承自應用程式控制器的控制器上呼叫任何動作時，電影類別目錄就會自動包含在視圖資料中。</span><span class="sxs-lookup"><span data-stu-id="3227b-177">Whenever you call any action on any controller that inherits from the Application controller, the movie categories is included in the view data automatically.</span></span>

<span data-ttu-id="3227b-178">[清單 5] 中的 [電影控制器] 繼承自應用程式控制器。</span><span class="sxs-lookup"><span data-stu-id="3227b-178">The Movies controller in Listing 5 inherits from the Application controller.</span></span>

<span data-ttu-id="3227b-179">**清單5– `Controllers\MoviesController.vb`**</span><span class="sxs-lookup"><span data-stu-id="3227b-179">**Listing 5 – `Controllers\MoviesController.vb`**</span></span>

[!code-vb[Main](passing-data-to-view-master-pages-vb/samples/sample5.vb)]

<span data-ttu-id="3227b-180">電影控制器就像上一節所討論的主控制器一樣，會公開名為 `Index()` 和 `Details()`的兩個動作方法。</span><span class="sxs-lookup"><span data-stu-id="3227b-180">The Movies controller, just like the Home controller discussed in the previous section, exposes two action methods named `Index()` and `Details()`.</span></span> <span data-ttu-id="3227b-181">請注意，視圖主版頁面所顯示的電影類別目錄清單並不會加入至 `Index()` 或 `Details()` 方法中的資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-181">Notice that the list of movie categories displayed by the view master page is not added to view data in either the `Index()` or `Details()` method.</span></span> <span data-ttu-id="3227b-182">由於電影控制器會繼承自應用程式控制器，因此會自動新增電影類別清單來查看資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-182">Because the Movies controller inherits from the Application controller, the list of movie categories is added to view data automatically.</span></span>

<span data-ttu-id="3227b-183">請注意，此方案會加入視圖主版頁面的視圖資料，並不會違反試（不重複原則）準則。</span><span class="sxs-lookup"><span data-stu-id="3227b-183">Notice that this solution to adding view data for a view master page does not violate the DRY (Don't Repeat Yourself) principle.</span></span> <span data-ttu-id="3227b-184">用來將電影類別目錄清單新增至視圖資料的程式碼只包含在一個位置：應用程式控制器的函式。</span><span class="sxs-lookup"><span data-stu-id="3227b-184">The code for adding the list of movie categories to view data is contained in only one location: the constructor for the Application controller.</span></span>

### <a name="summary"></a><span data-ttu-id="3227b-185">總結</span><span class="sxs-lookup"><span data-stu-id="3227b-185">Summary</span></span>

<span data-ttu-id="3227b-186">在本教學課程中，我們討論了兩種將視圖資料從控制器傳遞至視圖主版頁面的方法。</span><span class="sxs-lookup"><span data-stu-id="3227b-186">In this tutorial, we discussed two approaches to passing view data from a controller to a view master page.</span></span> <span data-ttu-id="3227b-187">首先，我們檢查了簡單但很難維護的方法。</span><span class="sxs-lookup"><span data-stu-id="3227b-187">First, we examined a simple, but difficult to maintain approach.</span></span> <span data-ttu-id="3227b-188">在第一節中，我們討論了如何在應用程式的每個控制器動作中，加入視圖主版頁面的視圖資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-188">In the first section, we discussed how you can add view data for a view master page in each every controller action in your application.</span></span> <span data-ttu-id="3227b-189">我們結論是，這是不好的方法，因為它違反了試（不重複原則）原則。</span><span class="sxs-lookup"><span data-stu-id="3227b-189">We concluded that this was a bad approach because it violates the DRY (Don't Repeat Yourself) principle.</span></span>

<span data-ttu-id="3227b-190">接下來，我們檢查了更好的策略來加入視圖主版頁面所需的資料，以查看資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-190">Next, we examined a much better strategy for adding data required by a view master page to view data.</span></span> <span data-ttu-id="3227b-191">我們不會在每個控制器動作中新增 view 資料，而是只在應用程式控制器內新增一次 view 資料。</span><span class="sxs-lookup"><span data-stu-id="3227b-191">Instead of adding the view data in each and every controller action, we added the view data only once within an Application controller.</span></span> <span data-ttu-id="3227b-192">如此一來，您可以在 ASP.NET MVC 應用程式中將資料傳遞至視圖主版頁面時，避免重複的程式碼。</span><span class="sxs-lookup"><span data-stu-id="3227b-192">That way, you can avoid duplicate code when passing data to a view master page in an ASP.NET MVC application.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="3227b-193">上一篇</span><span class="sxs-lookup"><span data-stu-id="3227b-193">Previous</span></span>](creating-page-layouts-with-view-master-pages-vb.md)
