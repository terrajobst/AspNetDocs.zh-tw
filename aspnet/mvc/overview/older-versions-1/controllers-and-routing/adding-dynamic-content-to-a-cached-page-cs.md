---
uid: mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
title: 將動態內容新增至快取的C#頁面（） |Microsoft Docs
author: microsoft
description: 瞭解如何在相同頁面中混合動態和快取的內容。 快取後的替代功能可讓您顯示動態內容，例如橫幅廣告 o 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 2ddd4407-d143-4a94-877c-21771bfb97a6
msc.legacyurl: /mvc/overview/older-versions-1/controllers-and-routing/adding-dynamic-content-to-a-cached-page-cs
msc.type: authoredcontent
ms.openlocfilehash: be43712d3dd5235117558e991d9dd71aa30ec470
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601581"
---
# <a name="adding-dynamic-content-to-a-cached-page-c"></a><span data-ttu-id="10115-104">將動態內容新增至快取的頁面 (C#)</span><span class="sxs-lookup"><span data-stu-id="10115-104">Adding Dynamic Content to a Cached Page (C#)</span></span>

<span data-ttu-id="10115-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="10115-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="10115-106">瞭解如何在相同頁面中混合動態和快取的內容。</span><span class="sxs-lookup"><span data-stu-id="10115-106">Learn how to mix dynamic and cached content in the same page.</span></span> <span data-ttu-id="10115-107">快取後的替代功能可讓您在已快取輸出的頁面中顯示動態內容，例如橫幅廣告或新聞專案。</span><span class="sxs-lookup"><span data-stu-id="10115-107">Post-cache substitution enables you to display dynamic content, such as banner advertisements or news items, within a page that has been output cached.</span></span>

<span data-ttu-id="10115-108">藉由利用輸出快取，您可以大幅提升 ASP.NET MVC 應用程式的效能。</span><span class="sxs-lookup"><span data-stu-id="10115-108">By taking advantage of output caching, you can dramatically improve the performance of an ASP.NET MVC application.</span></span> <span data-ttu-id="10115-109">每次要求頁面時，不需要重新產生頁面，而是會產生一次頁面，並快取到記憶體中供多位使用者使用。</span><span class="sxs-lookup"><span data-stu-id="10115-109">Instead of regenerating a page each and every time the page is requested, the page can be generated once and cached in memory for multiple users.</span></span>

<span data-ttu-id="10115-110">但還是有問題。</span><span class="sxs-lookup"><span data-stu-id="10115-110">But there is a problem.</span></span> <span data-ttu-id="10115-111">如果您需要在頁面中顯示動態內容，該怎麼做？</span><span class="sxs-lookup"><span data-stu-id="10115-111">What if you need to display dynamic content in the page?</span></span> <span data-ttu-id="10115-112">例如，假設您想要在頁面中顯示橫幅廣告。</span><span class="sxs-lookup"><span data-stu-id="10115-112">For example, imagine that you want to display a banner advertisement in the page.</span></span> <span data-ttu-id="10115-113">您不想要快取橫幅廣告，讓每位使用者都看到相同的廣告。</span><span class="sxs-lookup"><span data-stu-id="10115-113">You don't want the banner advertisement to be cached so that every user sees the very same advertisement.</span></span> <span data-ttu-id="10115-114">您不需要任何錢就能完成！</span><span class="sxs-lookup"><span data-stu-id="10115-114">You wouldn't make any money that way!</span></span>

<span data-ttu-id="10115-115">幸運的是，有一個簡單的解決方案。</span><span class="sxs-lookup"><span data-stu-id="10115-115">Fortunately, there is an easy solution.</span></span> <span data-ttu-id="10115-116">您可以利用 ASP.NET 架構的一項功能，稱為*後置*快取替代。</span><span class="sxs-lookup"><span data-stu-id="10115-116">You can take advantage of a feature of the ASP.NET framework called *post-cache substitution*.</span></span> <span data-ttu-id="10115-117">快取後的替代功能可讓您替代已在記憶體中快取的頁面中的動態內容。</span><span class="sxs-lookup"><span data-stu-id="10115-117">Post-cache substitution enables you to substitute dynamic content in a page that has been cached in memory.</span></span>

<span data-ttu-id="10115-118">一般來說，當您使用 [OutputCache] 屬性來輸出快取頁面時，會在伺服器和用戶端（網頁瀏覽器）上快取頁面。</span><span class="sxs-lookup"><span data-stu-id="10115-118">Normally, when you output cache a page by using the [OutputCache] attribute, the page is cached on both the server and the client (the web browser).</span></span> <span data-ttu-id="10115-119">當您使用快取後的替換時，只會在伺服器上快取頁面。</span><span class="sxs-lookup"><span data-stu-id="10115-119">When you use post-cache substitution, a page is cached only on the server.</span></span>

#### <a name="using-post-cache-substitution"></a><span data-ttu-id="10115-120">使用快取後的替代</span><span class="sxs-lookup"><span data-stu-id="10115-120">Using Post-Cache Substitution</span></span>

<span data-ttu-id="10115-121">使用快取後的替代需要兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="10115-121">Using post-cache substitution requires two steps.</span></span> <span data-ttu-id="10115-122">首先，您必須定義方法來傳回字串，表示您想要在快取頁面中顯示的動態內容。</span><span class="sxs-lookup"><span data-stu-id="10115-122">First, you need to define a method that returns a string that represents the dynamic content that you want to display in the cached page.</span></span> <span data-ttu-id="10115-123">接下來，您會呼叫 HttpResponse. WriteSubstitution （）方法，將動態內容插入頁面中。</span><span class="sxs-lookup"><span data-stu-id="10115-123">Next, you call the HttpResponse.WriteSubstitution() method to inject the dynamic content into the page.</span></span>

<span data-ttu-id="10115-124">例如，假設您想要在快取的頁面中隨機顯示不同的新聞專案。</span><span class="sxs-lookup"><span data-stu-id="10115-124">Imagine, for example, that you want to randomly display different news items in a cached page.</span></span> <span data-ttu-id="10115-125">[清單 1] 中的類別會公開名為 RenderNews （）的單一方法，它會從三個新聞專案的清單隨機傳回一個新聞專案。</span><span class="sxs-lookup"><span data-stu-id="10115-125">The class in Listing 1 exposes a single method, named RenderNews(), that randomly returns one news item from a list of three news items.</span></span>

<span data-ttu-id="10115-126">**清單1– Models\News.cs**</span><span class="sxs-lookup"><span data-stu-id="10115-126">**Listing 1 – Models\News.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample1.cs)]

<span data-ttu-id="10115-127">若要利用快取後的替代，請呼叫 HttpResponse. WriteSubstitution （）方法。</span><span class="sxs-lookup"><span data-stu-id="10115-127">To take advantage of post-cache substitution, you call the HttpResponse.WriteSubstitution() method.</span></span> <span data-ttu-id="10115-128">WriteSubstitution （）方法會設定程式碼，以動態內容取代快取頁面的區域。</span><span class="sxs-lookup"><span data-stu-id="10115-128">The WriteSubstitution() method sets up the code to replace a region of the cached page with dynamic content.</span></span> <span data-ttu-id="10115-129">WriteSubstitution （）方法是用來在 [清單 2] 的視圖中顯示隨機新聞專案。</span><span class="sxs-lookup"><span data-stu-id="10115-129">The WriteSubstitution() method is used to display the random news item in the view in Listing 2.</span></span>

<span data-ttu-id="10115-130">**清單2– Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="10115-130">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample2.aspx)]

<span data-ttu-id="10115-131">RenderNews 方法會傳遞至 WriteSubstitution （）方法。</span><span class="sxs-lookup"><span data-stu-id="10115-131">The RenderNews method is passed to the WriteSubstitution() method.</span></span> <span data-ttu-id="10115-132">請注意，不會呼叫 RenderNews 方法（沒有括弧）。</span><span class="sxs-lookup"><span data-stu-id="10115-132">Notice that the RenderNews method is not called (there are no parentheses).</span></span> <span data-ttu-id="10115-133">相反地，會將方法的參考傳遞給 WriteSubstitution （）。</span><span class="sxs-lookup"><span data-stu-id="10115-133">Instead a reference to the method is passed to WriteSubstitution().</span></span>

<span data-ttu-id="10115-134">索引視圖會被快取。</span><span class="sxs-lookup"><span data-stu-id="10115-134">The Index view is cached.</span></span> <span data-ttu-id="10115-135">[清單 3] 中的控制器會傳回此視圖。</span><span class="sxs-lookup"><span data-stu-id="10115-135">The view is returned by the controller in Listing 3.</span></span> <span data-ttu-id="10115-136">請注意，Index （）動作是以 [OutputCache] 屬性裝飾，這會導致索引視圖快取60秒。</span><span class="sxs-lookup"><span data-stu-id="10115-136">Notice that the Index() action is decorated with an [OutputCache] attribute that causes the Index view to be cached for 60 seconds.</span></span>

<span data-ttu-id="10115-137">**清單3– Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="10115-137">**Listing 3 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample3.cs)]

<span data-ttu-id="10115-138">即使快取索引視圖，當您要求 [索引] 頁面時，也會顯示不同的隨機新聞專案。</span><span class="sxs-lookup"><span data-stu-id="10115-138">Even though the Index view is cached, different random news items are displayed when you request the Index page.</span></span> <span data-ttu-id="10115-139">當您要求 [索引] 頁面時，頁面所顯示的時間不會變更60秒（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="10115-139">When you request the Index page, the time displayed by the page does not change for 60 seconds (see Figure 1).</span></span> <span data-ttu-id="10115-140">但時間不會改變，而是會證明頁面已快取。</span><span class="sxs-lookup"><span data-stu-id="10115-140">The fact that the time does not change proves that the page is cached.</span></span> <span data-ttu-id="10115-141">不過，WriteSubstitution （）方法插入的內容（隨機新聞專案），會隨著每個要求而變更。</span><span class="sxs-lookup"><span data-stu-id="10115-141">However, the content injected by the WriteSubstitution() method – the random news item – changes with each request .</span></span>

<span data-ttu-id="10115-142">**圖1–在快取的頁面中插入動態新聞專案**</span><span class="sxs-lookup"><span data-stu-id="10115-142">**Figure 1 – Injecting dynamic news items in a cached page**</span></span>

![clip_image002](adding-dynamic-content-to-a-cached-page-cs/_static/image1.jpg)

#### <a name="using-post-cache-substitution-in-helper-methods"></a><span data-ttu-id="10115-144">在 Helper 方法中使用後置快取替代</span><span class="sxs-lookup"><span data-stu-id="10115-144">Using Post-Cache Substitution in Helper Methods</span></span>

<span data-ttu-id="10115-145">更簡單的方法是利用快取後的替代方式，在自訂 helper 方法內封裝對 WriteSubstitution （）方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="10115-145">An easier way to take advantage of post-cache substitution is to encapsulate the call to the WriteSubstitution() method within a custom helper method.</span></span> <span data-ttu-id="10115-146">這種方法是由 [清單 4] 中的 helper 方法來說明。</span><span class="sxs-lookup"><span data-stu-id="10115-146">This approach is illustrated by the helper method in Listing 4.</span></span>

<span data-ttu-id="10115-147">**清單4– AdHelper.cs**</span><span class="sxs-lookup"><span data-stu-id="10115-147">**Listing 4 – AdHelper.cs**</span></span>

[!code-csharp[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample4.cs)]

<span data-ttu-id="10115-148">[清單 4] 包含一個會公開兩個方法的靜態類別： RenderBanner （）和 RenderBannerInternal （）。</span><span class="sxs-lookup"><span data-stu-id="10115-148">Listing 4 contains a static class that exposes two methods: RenderBanner() and RenderBannerInternal().</span></span> <span data-ttu-id="10115-149">RenderBanner （）方法代表實際的 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="10115-149">The RenderBanner() method represents the actual helper method.</span></span> <span data-ttu-id="10115-150">這個方法會擴充標準的 ASP.NET MVC HtmlHelper 類別，讓您可以在視圖中呼叫 RenderBanner （），就像任何其他 helper 方法一樣。</span><span class="sxs-lookup"><span data-stu-id="10115-150">This method extends the standard ASP.NET MVC HtmlHelper class so that you can call Html.RenderBanner() in a view just like any other helper method.</span></span>

<span data-ttu-id="10115-151">RenderBanner （）方法會呼叫 HttpResponse. WriteSubstitution （）方法，並將 RenderBannerInternal （）方法傳遞至 WriteSubstitution （）方法。</span><span class="sxs-lookup"><span data-stu-id="10115-151">The RenderBanner() method calls the HttpResponse.WriteSubstitution() method passing the RenderBannerInternal() method to the WriteSubstitution() method.</span></span>

<span data-ttu-id="10115-152">RenderBannerInternal （）方法是私用方法。</span><span class="sxs-lookup"><span data-stu-id="10115-152">The RenderBannerInternal() method is a private method.</span></span> <span data-ttu-id="10115-153">這個方法不會公開為 helper 方法。</span><span class="sxs-lookup"><span data-stu-id="10115-153">This method won't be exposed as a helper method.</span></span> <span data-ttu-id="10115-154">RenderBannerInternal （）方法會從三個橫幅廣告影像的清單中隨機傳回一個橫幅廣告影像。</span><span class="sxs-lookup"><span data-stu-id="10115-154">The RenderBannerInternal() method randomly returns one banner advertisement image from a list of three banner advertisement images.</span></span>

<span data-ttu-id="10115-155">[清單 5] 中修改過的索引視圖會說明如何使用 RenderBanner （） helper 方法。</span><span class="sxs-lookup"><span data-stu-id="10115-155">The modified Index view in Listing 5 illustrates how you can use the RenderBanner() helper method.</span></span> <span data-ttu-id="10115-156">請注意，在此視圖頂端會包含額外的 &lt;% @ Import%&gt; 指示詞，以匯入 MvcApplication1. helper 命名空間。</span><span class="sxs-lookup"><span data-stu-id="10115-156">Notice that an additional &lt;%@ Import %&gt; directive is included at the top of the view to import the MvcApplication1.Helpers namespace.</span></span> <span data-ttu-id="10115-157">如果您不想匯入此命名空間，則 RenderBanner （）方法不會顯示為 Html 屬性上的方法。</span><span class="sxs-lookup"><span data-stu-id="10115-157">If you neglect to import this namespace, then the RenderBanner() method won't appear as a method on the Html property.</span></span>

<span data-ttu-id="10115-158">**清單5– Views\Home\Index.aspx （使用 RenderBanner （）方法）**</span><span class="sxs-lookup"><span data-stu-id="10115-158">**Listing 5 – Views\Home\Index.aspx (with RenderBanner() method)**</span></span>

[!code-aspx[Main](adding-dynamic-content-to-a-cached-page-cs/samples/sample5.aspx)]

<span data-ttu-id="10115-159">當您要求清單5中的視圖所呈現的頁面時，每個要求都會顯示不同的橫幅廣告（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="10115-159">When you request the page rendered by the view in Listing 5, a different banner advertisement is displayed with each request (see Figure 2).</span></span> <span data-ttu-id="10115-160">會快取頁面，但 RenderBanner （） helper 方法會動態插入橫幅廣告。</span><span class="sxs-lookup"><span data-stu-id="10115-160">The page is cached, but the banner advertisement is injected dynamically by the RenderBanner() helper method.</span></span>

<span data-ttu-id="10115-161">**圖2–顯示隨機橫幅廣告的索引視圖**</span><span class="sxs-lookup"><span data-stu-id="10115-161">**Figure 2 – The Index view displaying a random banner advertisement**</span></span>

![clip_image004](adding-dynamic-content-to-a-cached-page-cs/_static/image2.jpg)

#### <a name="summary"></a><span data-ttu-id="10115-163">總結</span><span class="sxs-lookup"><span data-stu-id="10115-163">Summary</span></span>

<span data-ttu-id="10115-164">本教學課程說明如何動態更新快取頁面中的內容。</span><span class="sxs-lookup"><span data-stu-id="10115-164">This tutorial explained how you can dynamically update content in a cached page.</span></span> <span data-ttu-id="10115-165">您已瞭解如何使用 HttpResponse. WriteSubstitution （）方法，讓動態內容插入快取的頁面中。</span><span class="sxs-lookup"><span data-stu-id="10115-165">You learned how to use the HttpResponse.WriteSubstitution() method to enable dynamic content to be injected in a cached page.</span></span> <span data-ttu-id="10115-166">您也已瞭解如何在 HTML helper 方法內封裝對 WriteSubstitution （）方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="10115-166">You also learned how to encapsulate the call to the WriteSubstitution() method within an HTML helper method.</span></span>

<span data-ttu-id="10115-167">盡可能利用快取，這可能會對 web 應用程式的效能產生顯著的影響。</span><span class="sxs-lookup"><span data-stu-id="10115-167">Take advantage of caching whenever possible – it can have a dramatic impact on the performance of your web applications.</span></span> <span data-ttu-id="10115-168">如本教學課程中所述，即使您需要在頁面中顯示動態內容，您也可以利用快取。</span><span class="sxs-lookup"><span data-stu-id="10115-168">As explained in this tutorial, you can take advantage of caching even when you need to display dynamic content in your pages.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="10115-169">[上一頁](improving-performance-with-output-caching-cs.md)
> [下一頁](creating-a-controller-cs.md)</span><span class="sxs-lookup"><span data-stu-id="10115-169">[Previous](improving-performance-with-output-caching-cs.md)
[Next](creating-a-controller-cs.md)</span></span>
