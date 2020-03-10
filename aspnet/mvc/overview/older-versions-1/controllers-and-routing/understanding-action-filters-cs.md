---
uid: mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
title: 瞭解動作篩選（C#） |Microsoft Docs
author: microsoft
description: 本教學課程的目的是要說明動作篩選準則。 動作篩選準則是可套用至控制器動作或整個控制器的屬性 。
ms.author: riande
ms.date: 10/16/2008
ms.assetid: a94e4e81-40c1-47b7-8613-126a1a6cc93d
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/understanding-action-filters-cs
msc.type: authoredcontent
ms.openlocfilehash: d1c72c2355c6122f851351a8c1e8f04fa63ae04e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581820"
---
# <a name="understanding-action-filters-c"></a><span data-ttu-id="3e56e-104">了解動作篩選 (C#)</span><span class="sxs-lookup"><span data-stu-id="3e56e-104">Understanding Action Filters (C#)</span></span>

<span data-ttu-id="3e56e-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="3e56e-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="3e56e-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="3e56e-106">Download PDF</span></span>](https://download.microsoft.com/download/e/f/3/ef3f2ff6-7424-48f7-bdaa-180ef64c3490/ASPNET_MVC_Tutorial_14_CS.pdf)

> <span data-ttu-id="3e56e-107">本教學課程的目的是要說明動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="3e56e-107">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="3e56e-108">動作篩選準則是一種屬性，可套用至控制器動作或整個控制器--修改動作的執行方式。</span><span class="sxs-lookup"><span data-stu-id="3e56e-108">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span>

## <a name="understanding-action-filters"></a><span data-ttu-id="3e56e-109">瞭解動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="3e56e-109">Understanding Action Filters</span></span>

<span data-ttu-id="3e56e-110">本教學課程的目的是要說明動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="3e56e-110">The goal of this tutorial is to explain action filters.</span></span> <span data-ttu-id="3e56e-111">動作篩選準則是一種屬性，可套用至控制器動作或整個控制器--修改動作的執行方式。</span><span class="sxs-lookup"><span data-stu-id="3e56e-111">An action filter is an attribute that you can apply to a controller action -- or an entire controller -- that modifies the way in which the action is executed.</span></span> <span data-ttu-id="3e56e-112">ASP.NET MVC 架構包含數個動作篩選準則：</span><span class="sxs-lookup"><span data-stu-id="3e56e-112">The ASP.NET MVC framework includes several action filters:</span></span>

- <span data-ttu-id="3e56e-113">OutputCache –此動作篩選準則會在一段指定的時間內快取控制器動作的輸出。</span><span class="sxs-lookup"><span data-stu-id="3e56e-113">OutputCache – This action filter caches the output of a controller action for a specified amount of time.</span></span>
- <span data-ttu-id="3e56e-114">HandleError –此動作篩選準則會處理控制器動作執行時引發的錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e56e-114">HandleError – This action filter handles errors raised when a controller action executes.</span></span>
- <span data-ttu-id="3e56e-115">授權–此動作篩選準則可讓您限制對特定使用者或角色的存取。</span><span class="sxs-lookup"><span data-stu-id="3e56e-115">Authorize – This action filter enables you to restrict access to a particular user or role.</span></span>

<span data-ttu-id="3e56e-116">您也可以建立自己的自訂動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="3e56e-116">You also can create your own custom action filters.</span></span> <span data-ttu-id="3e56e-117">例如，您可能會想要建立自訂動作篩選準則，以便執行自訂驗證系統。</span><span class="sxs-lookup"><span data-stu-id="3e56e-117">For example, you might want to create a custom action filter in order to implement a custom authentication system.</span></span> <span data-ttu-id="3e56e-118">或者，您可能會想要建立動作篩選準則，以修改控制器動作所傳回的視圖資料。</span><span class="sxs-lookup"><span data-stu-id="3e56e-118">Or, you might want to create an action filter that modifies the view data returned by a controller action.</span></span>

<span data-ttu-id="3e56e-119">在本教學課程中，您將瞭解如何從頭開始建立動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="3e56e-119">In this tutorial, you learn how to build an action filter from the ground up.</span></span> <span data-ttu-id="3e56e-120">我們會建立記錄動作篩選，將動作處理的不同階段記錄到 Visual Studio 的 [輸出] 視窗。</span><span class="sxs-lookup"><span data-stu-id="3e56e-120">We create a Log action filter that logs different stages of the processing of an action to the Visual Studio Output window.</span></span>

### <a name="using-an-action-filter"></a><span data-ttu-id="3e56e-121">使用動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="3e56e-121">Using an Action Filter</span></span>

<span data-ttu-id="3e56e-122">動作篩選準則是一個屬性。</span><span class="sxs-lookup"><span data-stu-id="3e56e-122">An action filter is an attribute.</span></span> <span data-ttu-id="3e56e-123">您可以將大部分的動作篩選準則套用至個別的控制器動作或整個控制器。</span><span class="sxs-lookup"><span data-stu-id="3e56e-123">You can apply most action filters to either an individual controller action or an entire controller.</span></span>

<span data-ttu-id="3e56e-124">例如，[清單 1] 中的資料控制站會公開名為 `Index()` 的動作，以傳回目前的時間。</span><span class="sxs-lookup"><span data-stu-id="3e56e-124">For example, the Data controller in Listing 1 exposes an action named `Index()` that returns the current time.</span></span> <span data-ttu-id="3e56e-125">此動作會使用 [`OutputCache` 動作] 篩選準則裝飾。</span><span class="sxs-lookup"><span data-stu-id="3e56e-125">This action is decorated with the `OutputCache` action filter.</span></span> <span data-ttu-id="3e56e-126">此篩選會使動作所傳回的值快取10秒。</span><span class="sxs-lookup"><span data-stu-id="3e56e-126">This filter causes the value returned by the action to be cached for 10 seconds.</span></span>

<span data-ttu-id="3e56e-127">**清單1– `Controllers\DataController.cs`**</span><span class="sxs-lookup"><span data-stu-id="3e56e-127">**Listing 1 – `Controllers\DataController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample1.cs)]

<span data-ttu-id="3e56e-128">如果您藉由在瀏覽器的網址列中輸入 URL/Data/Index，重複叫用 `Index()` 動作，並多次按下 [重新整理] 按鈕，則會看到10秒的相同時間。</span><span class="sxs-lookup"><span data-stu-id="3e56e-128">If you repeatedly invoke the `Index()` action by entering the URL /Data/Index into the address bar of your browser and hitting the Refresh button multiple times, then you will see the same time for 10 seconds.</span></span> <span data-ttu-id="3e56e-129">`Index()` 動作的輸出會快取10秒（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="3e56e-129">The output of the `Index()` action is cached for 10 seconds (see Figure 1).</span></span>

<span data-ttu-id="3e56e-130">[![快取時間](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3e56e-130">[![Cached time](understanding-action-filters-cs/_static/image2.png)](understanding-action-filters-cs/_static/image1.png)</span></span>

<span data-ttu-id="3e56e-131">**圖 01**：快取的時間（[按一下以觀看完整大小的影像](understanding-action-filters-cs/_static/image3.png)）</span><span class="sxs-lookup"><span data-stu-id="3e56e-131">**Figure 01**: Cached time ([Click to view full-size image](understanding-action-filters-cs/_static/image3.png))</span></span>

<span data-ttu-id="3e56e-132">在 [清單 1] 中，單一動作篩選準則– `OutputCache` 動作篩選準則–套用至 `Index()` 方法。</span><span class="sxs-lookup"><span data-stu-id="3e56e-132">In Listing 1, a single action filter – the `OutputCache` action filter – is applied to the `Index()` method.</span></span> <span data-ttu-id="3e56e-133">如有需要，您可以將多個動作篩選準則套用至相同的動作。</span><span class="sxs-lookup"><span data-stu-id="3e56e-133">If you need, you can apply multiple action filters to the same action.</span></span> <span data-ttu-id="3e56e-134">例如，您可能會想要將 `OutputCache` 和 `HandleError` 動作篩選準則套用至相同的動作。</span><span class="sxs-lookup"><span data-stu-id="3e56e-134">For example, you might want to apply both the `OutputCache` and `HandleError` action filters to the same action.</span></span>

<span data-ttu-id="3e56e-135">在 [清單 1] 中，[`OutputCache` 動作] 篩選準則會套用至 [`Index()`] 動作。</span><span class="sxs-lookup"><span data-stu-id="3e56e-135">In Listing 1, the `OutputCache` action filter is applied to the `Index()` action.</span></span> <span data-ttu-id="3e56e-136">您也可以將此屬性套用至 `DataController` 類別本身。</span><span class="sxs-lookup"><span data-stu-id="3e56e-136">You also could apply this attribute to the `DataController` class itself.</span></span> <span data-ttu-id="3e56e-137">在此情況下，控制器所公開的任何動作所傳回的結果會快取10秒。</span><span class="sxs-lookup"><span data-stu-id="3e56e-137">In that case, the result returned by any action exposed by the controller would be cached for 10 seconds.</span></span>

### <a name="the-different-types-of-filters"></a><span data-ttu-id="3e56e-138">不同類型的篩選準則</span><span class="sxs-lookup"><span data-stu-id="3e56e-138">The Different Types of Filters</span></span>

<span data-ttu-id="3e56e-139">ASP.NET MVC 架構支援四種不同類型的篩選準則：</span><span class="sxs-lookup"><span data-stu-id="3e56e-139">The ASP.NET MVC framework supports four different types of filters:</span></span>

1. <span data-ttu-id="3e56e-140">授權篩選–會執行 `IAuthorizationFilter` 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e56e-140">Authorization filters – Implements the `IAuthorizationFilter` attribute.</span></span>
2. <span data-ttu-id="3e56e-141">動作篩選–執行 `IActionFilter` 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e56e-141">Action filters – Implements the `IActionFilter` attribute.</span></span>
3. <span data-ttu-id="3e56e-142">結果篩選–執行 `IResultFilter` 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e56e-142">Result filters – Implements the `IResultFilter` attribute.</span></span>
4. <span data-ttu-id="3e56e-143">例外狀況篩選準則–執行 `IExceptionFilter` 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e56e-143">Exception filters – Implements the `IExceptionFilter` attribute.</span></span>

<span data-ttu-id="3e56e-144">篩選器會依照上列循序執行。</span><span class="sxs-lookup"><span data-stu-id="3e56e-144">Filters are executed in the order listed above.</span></span> <span data-ttu-id="3e56e-145">例如，授權篩選準則一律會在動作篩選準則之前執行，而例外狀況篩選準則一律會在每個其他類型的篩選器之後執行。</span><span class="sxs-lookup"><span data-stu-id="3e56e-145">For example, authorization filters are always executed before action filters and exception filters are always executed after every other type of filter.</span></span>

<span data-ttu-id="3e56e-146">授權篩選器用來執行控制器動作的驗證和授權。</span><span class="sxs-lookup"><span data-stu-id="3e56e-146">Authorization filters are used to implement authentication and authorization for controller actions.</span></span> <span data-ttu-id="3e56e-147">例如，授權篩選準則就是授權篩選準則的範例。</span><span class="sxs-lookup"><span data-stu-id="3e56e-147">For example, the Authorize filter is an example of an Authorization filter.</span></span>

<span data-ttu-id="3e56e-148">動作篩選包含在控制器動作執行前後執行的邏輯。</span><span class="sxs-lookup"><span data-stu-id="3e56e-148">Action filters contain logic that is executed before and after a controller action executes.</span></span> <span data-ttu-id="3e56e-149">例如，您可以使用動作篩選準則來修改控制器動作所傳回的視圖資料。</span><span class="sxs-lookup"><span data-stu-id="3e56e-149">You can use an action filter, for instance, to modify the view data that a controller action returns.</span></span>

<span data-ttu-id="3e56e-150">結果篩選包含在執行視圖結果之前和之後執行的邏輯。</span><span class="sxs-lookup"><span data-stu-id="3e56e-150">Result filters contain logic that is executed before and after a view result is executed.</span></span> <span data-ttu-id="3e56e-151">例如，您可能會想要在將視圖轉譯至瀏覽器之前修改視圖結果。</span><span class="sxs-lookup"><span data-stu-id="3e56e-151">For example, you might want to modify a view result right before the view is rendered to the browser.</span></span>

<span data-ttu-id="3e56e-152">例外狀況篩選是要執行的最後一個篩選準則類型。</span><span class="sxs-lookup"><span data-stu-id="3e56e-152">Exception filters are the last type of filter to run.</span></span> <span data-ttu-id="3e56e-153">您可以使用例外狀況篩選器來處理控制器動作或控制器動作結果所引發的錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e56e-153">You can use an exception filter to handle errors raised by either your controller actions or controller action results.</span></span> <span data-ttu-id="3e56e-154">您也可以使用例外狀況篩選來記錄錯誤。</span><span class="sxs-lookup"><span data-stu-id="3e56e-154">You also can use exception filters to log errors.</span></span>

<span data-ttu-id="3e56e-155">每個不同類型的篩選準則都會以特定循序執行。</span><span class="sxs-lookup"><span data-stu-id="3e56e-155">Each different type of filter is executed in a particular order.</span></span> <span data-ttu-id="3e56e-156">如果您想要控制執行相同類型篩選準則的順序，您可以設定篩選的 Order 屬性。</span><span class="sxs-lookup"><span data-stu-id="3e56e-156">If you want to control the order in which filters of the same type are executed then you can set a filter's Order property.</span></span>

<span data-ttu-id="3e56e-157">所有動作篩選準則的基類都是 `System.Web.Mvc.FilterAttribute` 類別。</span><span class="sxs-lookup"><span data-stu-id="3e56e-157">The base class for all action filters is the `System.Web.Mvc.FilterAttribute` class.</span></span> <span data-ttu-id="3e56e-158">如果您想要實作為特定類型的篩選準則，則需要建立繼承自基底篩選準則類別的類別，並執行一或多個 `IAuthorizationFilter`、`IActionFilter`、`IResultFilter`或 `IExceptionFilter` 介面。</span><span class="sxs-lookup"><span data-stu-id="3e56e-158">If you want to implement a particular type of filter, then you need to create a class that inherits from the base Filter class and implements one or more of the `IAuthorizationFilter`, `IActionFilter`, `IResultFilter`, or `IExceptionFilter` interfaces.</span></span>

### <a name="the-base-actionfilterattribute-class"></a><span data-ttu-id="3e56e-159">基底 Actionfilterattribut 類別</span><span class="sxs-lookup"><span data-stu-id="3e56e-159">The Base ActionFilterAttribute Class</span></span>

<span data-ttu-id="3e56e-160">為了讓您更輕鬆地執行自訂動作篩選準則，ASP.NET MVC 架構包含基底 `ActionFilterAttribute` 類別。</span><span class="sxs-lookup"><span data-stu-id="3e56e-160">In order to make it easier for you to implement a custom action filter, the ASP.NET MVC framework includes a base `ActionFilterAttribute` class.</span></span> <span data-ttu-id="3e56e-161">這個類別會同時執行 `IActionFilter` 和 `IResultFilter` 介面，並繼承自 `Filter` 類別。</span><span class="sxs-lookup"><span data-stu-id="3e56e-161">This class implements both the `IActionFilter` and `IResultFilter` interfaces and inherits from the `Filter` class.</span></span>

<span data-ttu-id="3e56e-162">此處的術語並不完全一致。</span><span class="sxs-lookup"><span data-stu-id="3e56e-162">The terminology here is not entirely consistent.</span></span> <span data-ttu-id="3e56e-163">就技術上而言，繼承自 Actionfilterattribut 類別的類別同時是動作篩選準則和結果篩選準則。</span><span class="sxs-lookup"><span data-stu-id="3e56e-163">Technically, a class that inherits from the ActionFilterAttribute class is both an action filter and a result filter.</span></span> <span data-ttu-id="3e56e-164">不過，在鬆散的意義下，word 動作篩選準則是用來參考 ASP.NET MVC 架構中的任何類型篩選。</span><span class="sxs-lookup"><span data-stu-id="3e56e-164">However, in the loose sense, the word action filter is used to refer to any type of filter in the ASP.NET MVC framework.</span></span>

<span data-ttu-id="3e56e-165">基底 `ActionFilterAttribute` 類別具有下列可覆寫的方法：</span><span class="sxs-lookup"><span data-stu-id="3e56e-165">The base `ActionFilterAttribute` class has the following methods that you can override:</span></span>

- <span data-ttu-id="3e56e-166">OnActionExecuting –在執行控制器動作之前，會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="3e56e-166">OnActionExecuting – This method is called before a controller action is executed.</span></span>
- <span data-ttu-id="3e56e-167">OnActionExecuted –在執行控制器動作之後，會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="3e56e-167">OnActionExecuted – This method is called after a controller action is executed.</span></span>
- <span data-ttu-id="3e56e-168">OnResultExecuting –在執行控制器動作結果之前，會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="3e56e-168">OnResultExecuting – This method is called before a controller action result is executed.</span></span>
- <span data-ttu-id="3e56e-169">OnResultExecuted –在執行控制器動作結果之後，會呼叫這個方法。</span><span class="sxs-lookup"><span data-stu-id="3e56e-169">OnResultExecuted – This method is called after a controller action result is executed.</span></span>

<span data-ttu-id="3e56e-170">在下一節中，我們將瞭解如何執行這兩種不同的方法。</span><span class="sxs-lookup"><span data-stu-id="3e56e-170">In the next section, we'll see how you can implement each of these different methods.</span></span>

### <a name="creating-a-log-action-filter"></a><span data-ttu-id="3e56e-171">建立記錄動作篩選準則</span><span class="sxs-lookup"><span data-stu-id="3e56e-171">Creating a Log Action Filter</span></span>

<span data-ttu-id="3e56e-172">為了說明您可以如何建立自訂動作篩選準則，我們將建立自訂動作篩選準則，將處理控制器動作的階段記錄到 Visual Studio 的輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="3e56e-172">In order to illustrate how you can build a custom action filter, we'll create a custom action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span> <span data-ttu-id="3e56e-173">我們的 `LogActionFilter` 包含在 [清單 2] 中。</span><span class="sxs-lookup"><span data-stu-id="3e56e-173">Our `LogActionFilter` is contained in Listing 2.</span></span>

<span data-ttu-id="3e56e-174">**清單2– `ActionFilters\LogActionFilter.cs`**</span><span class="sxs-lookup"><span data-stu-id="3e56e-174">**Listing 2 – `ActionFilters\LogActionFilter.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample2.cs)]

<span data-ttu-id="3e56e-175">在 [清單 2] 中，`OnActionExecuting()`、`OnActionExecuted()`、`OnResultExecuting()`和 `OnResultExecuted()` 方法全都會呼叫 `Log()` 方法。</span><span class="sxs-lookup"><span data-stu-id="3e56e-175">In Listing 2, the `OnActionExecuting()`, `OnActionExecuted()`, `OnResultExecuting()`, and `OnResultExecuted()` methods all call the `Log()` method.</span></span> <span data-ttu-id="3e56e-176">方法的名稱和目前的路由資料會傳遞至 `Log()` 方法。</span><span class="sxs-lookup"><span data-stu-id="3e56e-176">The name of the method and the current route data is passed to the `Log()` method.</span></span> <span data-ttu-id="3e56e-177">`Log()` 方法會將訊息寫入 Visual Studio 的 [輸出] 視窗（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="3e56e-177">The `Log()` method writes a message to the Visual Studio Output window (see Figure 2).</span></span>

<span data-ttu-id="3e56e-178">[![寫入 Visual Studio 輸出視窗](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="3e56e-178">[![Writing to the Visual Studio Output window](understanding-action-filters-cs/_static/image5.png)](understanding-action-filters-cs/_static/image4.png)</span></span>

<span data-ttu-id="3e56e-179">**圖 02**：寫入 Visual Studio 的輸出視窗（[按一下以查看完整大小的影像](understanding-action-filters-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="3e56e-179">**Figure 02**: Writing to the Visual Studio Output window ([Click to view full-size image](understanding-action-filters-cs/_static/image6.png))</span></span>

<span data-ttu-id="3e56e-180">[清單 3] 中的 Home 控制器說明如何將記錄動作篩選套用至整個控制器類別。</span><span class="sxs-lookup"><span data-stu-id="3e56e-180">The Home controller in Listing 3 illustrates how you can apply the Log action filter to an entire controller class.</span></span> <span data-ttu-id="3e56e-181">每當叫用 Home 控制器所公開的任何動作時（`Index()` 方法或 `About()` 方法），處理動作的階段就會記錄到 [Visual Studio 輸出] 視窗中。</span><span class="sxs-lookup"><span data-stu-id="3e56e-181">Whenever any of the actions exposed by the Home controller are invoked – either the `Index()` method or the `About()` method – the stages of processing the action are logged to the Visual Studio Output window.</span></span>

<span data-ttu-id="3e56e-182">**清單3– `Controllers\HomeController.cs`**</span><span class="sxs-lookup"><span data-stu-id="3e56e-182">**Listing 3 – `Controllers\HomeController.cs`**</span></span>

[!code-csharp[Main](understanding-action-filters-cs/samples/sample3.cs)]

### <a name="summary"></a><span data-ttu-id="3e56e-183">總結</span><span class="sxs-lookup"><span data-stu-id="3e56e-183">Summary</span></span>

<span data-ttu-id="3e56e-184">在本教學課程中，您已引進 ASP.NET MVC 動作篩選器。</span><span class="sxs-lookup"><span data-stu-id="3e56e-184">In this tutorial, you were introduced to ASP.NET MVC action filters.</span></span> <span data-ttu-id="3e56e-185">您已瞭解四種不同類型的篩選準則：授權篩選準則、動作篩選準則、結果篩選準則和例外狀況篩選器。</span><span class="sxs-lookup"><span data-stu-id="3e56e-185">You learned about the four different types of filters: authorization filters, action filters, result filters, and exception filters.</span></span> <span data-ttu-id="3e56e-186">您也已瞭解基底 `ActionFilterAttribute` 類別的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="3e56e-186">You also learned about the base `ActionFilterAttribute` class.</span></span>

<span data-ttu-id="3e56e-187">最後，您已瞭解如何執行簡單的動作篩選準則。</span><span class="sxs-lookup"><span data-stu-id="3e56e-187">Finally, you learned how to implement a simple action filter.</span></span> <span data-ttu-id="3e56e-188">我們已建立記錄動作篩選器，將處理控制器動作的階段記錄到 Visual Studio 的輸出視窗。</span><span class="sxs-lookup"><span data-stu-id="3e56e-188">We created a Log action filter that logs the stages of processing a controller action to the Visual Studio Output window.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3e56e-189">[上一頁](asp-net-mvc-routing-overview-cs.md)
> [下一頁](improving-performance-with-output-caching-cs.md)</span><span class="sxs-lookup"><span data-stu-id="3e56e-189">[Previous](asp-net-mvc-routing-overview-cs.md)
[Next](improving-performance-with-output-caching-cs.md)</span></span>
