---
uid: web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
title: 在 ASP.NET Web Pages （Razor）網站中快取資料以獲得更佳的效能 |Microsoft Docs
author: Rick-Anderson
description: 您可以藉由讓 it 儲存（也就是快取）來加速您的網站，這通常會花很長的時間來抓取或處理 。
ms.author: riande
ms.date: 02/14/2014
ms.assetid: 961e525b-7700-469e-8a68-d7010b6fb68c
msc.legacyurl: /web-pages/overview/performance-and-traffic/15-caching-to-improve-the-performance-of-your-website
msc.type: authoredcontent
ms.openlocfilehash: 01796d3ca699a6af5d9162b22a926551435c2040
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641516"
---
# <a name="caching-data-in-an-aspnet-web-pages-razor-site-for-better-performance"></a><span data-ttu-id="b18f0-103">在 ASP.NET Web Pages （Razor）網站中快取資料以獲得更好的效能</span><span class="sxs-lookup"><span data-stu-id="b18f0-103">Caching Data in an ASP.NET Web Pages (Razor) Site for Better Performance</span></span>

<span data-ttu-id="b18f0-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="b18f0-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="b18f0-105">本文說明如何使用協助程式快取資訊，以在 ASP.NET Web Pages （Razor）網站中取得更快速的效能。</span><span class="sxs-lookup"><span data-stu-id="b18f0-105">This article explains how to use a helper to cache information for faster performance in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="b18f0-106">您可以藉由讓 it 儲存&#8212; ，來加速您的網站， &#8212;快取資料的結果，通常需要很長的時間來抓取或處理，而且不常變更。</span><span class="sxs-lookup"><span data-stu-id="b18f0-106">You can speed up your website by having it store &#8212; that is, cache &#8212; the results of data that ordinarily would take considerable time to retrieve or process and that does not change often.</span></span>
> 
> <span data-ttu-id="b18f0-107">**您將瞭解的內容：**</span><span class="sxs-lookup"><span data-stu-id="b18f0-107">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="b18f0-108">如何使用快取來改善網站的回應能力。</span><span class="sxs-lookup"><span data-stu-id="b18f0-108">How to use caching to improve the responsiveness of your website.</span></span>
> 
> <span data-ttu-id="b18f0-109">以下是文章中引進的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="b18f0-109">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="b18f0-110">`WebCache` helper。</span><span class="sxs-lookup"><span data-stu-id="b18f0-110">The `WebCache` helper.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="b18f0-111">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="b18f0-111">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="b18f0-112">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="b18f0-112">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="b18f0-113">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="b18f0-113">This tutorial also works with ASP.NET Web Pages 2.</span></span>

<span data-ttu-id="b18f0-114">每次有人向您的網站要求頁面時，網頁伺服器都必須執行一些工作，才能完成要求。</span><span class="sxs-lookup"><span data-stu-id="b18f0-114">Every time someone requests a page from your site, the web server has to do some work in order to fulfill the request.</span></span> <span data-ttu-id="b18f0-115">對於某些頁面，伺服器可能必須執行花費（相對）長時間的工作，例如從資料庫中抓取資料。</span><span class="sxs-lookup"><span data-stu-id="b18f0-115">For some of your pages, the server might have to perform tasks that take a (comparatively) long time, such as retrieving data from a database.</span></span> <span data-ttu-id="b18f0-116">即使這些工作不會花很長的時間，但如果您的網站遇到大量的流量，則導致 web 伺服器執行複雜或緩慢工作的一系列個別要求，可能會增加許多工作。</span><span class="sxs-lookup"><span data-stu-id="b18f0-116">Even if these tasks don't take long in absolute terms, if your site experiences a lot of traffic, a whole series of individual requests that cause the web server to perform the complicated or slow task can add up to a lot of work.</span></span> <span data-ttu-id="b18f0-117">這最後可能會影響網站的效能。</span><span class="sxs-lookup"><span data-stu-id="b18f0-117">This can ultimately affect the performance of the site.</span></span>

<span data-ttu-id="b18f0-118">在這種情況下，若要改善網站效能，其中一種方法就是快取資料。</span><span class="sxs-lookup"><span data-stu-id="b18f0-118">One way to improve the performance of your website in circumstances like this is to cache data.</span></span> <span data-ttu-id="b18f0-119">如果您的網站取得相同資訊的重複要求，而且不需要針對每個人修改該資訊，而且也不會進行時間區分，而是只會提取資料一次，然後儲存結果。</span><span class="sxs-lookup"><span data-stu-id="b18f0-119">If your site gets repeated requests for the same information, and the information does not need to be modified for each person, and it's not time sensitive, instead of re-fetching or recalculating it, you can fetch the data once and then store the results.</span></span> <span data-ttu-id="b18f0-120">下一次收到該資訊的要求時，您就可以將它從快取中取出。</span><span class="sxs-lookup"><span data-stu-id="b18f0-120">The next time a request comes in for that information, you just get it out of the cache.</span></span>

<span data-ttu-id="b18f0-121">一般來說，您會快取不常變更的資訊。</span><span class="sxs-lookup"><span data-stu-id="b18f0-121">In general, you cache information that doesn't change frequently.</span></span> <span data-ttu-id="b18f0-122">當您將資訊放在快取中時，它會儲存在 web 伺服器的記憶體中。</span><span class="sxs-lookup"><span data-stu-id="b18f0-122">When you put information in the cache, it's stored in memory on the web server.</span></span> <span data-ttu-id="b18f0-123">您可以指定應快取的時間長度，從秒到天。</span><span class="sxs-lookup"><span data-stu-id="b18f0-123">You can specify how long it should be cached, from seconds to days.</span></span> <span data-ttu-id="b18f0-124">當快取期間到期時，就會自動從快取中移除資訊。</span><span class="sxs-lookup"><span data-stu-id="b18f0-124">When the caching period expires, the information is automatically removed from the cache.</span></span>

> [!NOTE]
> <span data-ttu-id="b18f0-125">可能會移除快取中的專案，原因是其已過期。</span><span class="sxs-lookup"><span data-stu-id="b18f0-125">Entries in the cache might be removed for reasons other than that they've expired.</span></span> <span data-ttu-id="b18f0-126">例如，網頁伺服器可能會暫時耗盡記憶體，而它可以回收記憶體的方法之一，就是從快取中擲回專案。</span><span class="sxs-lookup"><span data-stu-id="b18f0-126">For example, the web server might temporarily run low on memory, and one way it can reclaim memory is by throwing entries out of the cache.</span></span> <span data-ttu-id="b18f0-127">如您所見，即使您已將資訊放入快取中，還是必須檢查以確定它在您需要的時候仍然存在。</span><span class="sxs-lookup"><span data-stu-id="b18f0-127">As you'll see, even if you've put information into the cache, you have to check to be sure it's still there when you need it.</span></span>

<span data-ttu-id="b18f0-128">假設您的網站有一個頁面，其中顯示目前的溫度和氣象預報。</span><span class="sxs-lookup"><span data-stu-id="b18f0-128">Imagine your website has a page that displays the current temperature and weather forecast.</span></span> <span data-ttu-id="b18f0-129">若要取得這種類型的資訊，您可以將要求傳送至外部服務。</span><span class="sxs-lookup"><span data-stu-id="b18f0-129">To get this type of information, you might send a request to an external service.</span></span> <span data-ttu-id="b18f0-130">由於這項資訊不會變更（例如在兩小時的期間內），而且因為外部呼叫需要時間和頻寬，所以這是快取的理想候選。</span><span class="sxs-lookup"><span data-stu-id="b18f0-130">Since this information doesn't change much (within a two-hour time period, for example) and since external calls require time and bandwidth, it's a good candidate for caching.</span></span>

## <a name="adding-caching-to-a-page"></a><span data-ttu-id="b18f0-131">將快取新增至頁面</span><span class="sxs-lookup"><span data-stu-id="b18f0-131">Adding Caching to a Page</span></span>

<span data-ttu-id="b18f0-132">ASP.NET 包含 `WebCache` 協助程式，可讓您輕鬆地將快取新增至您的網站，並將資料新增至快取。</span><span class="sxs-lookup"><span data-stu-id="b18f0-132">ASP.NET includes a `WebCache` helper that makes it easy to add caching to your site and add data to the cache.</span></span> <span data-ttu-id="b18f0-133">在這個程式中，您將建立快取目前時間的頁面。</span><span class="sxs-lookup"><span data-stu-id="b18f0-133">In this procedure, you'll create a page that caches the current time.</span></span> <span data-ttu-id="b18f0-134">這不是真實世界的範例，因為目前的時間是經常變更的專案，而且這一點也不太複雜而無法計算。</span><span class="sxs-lookup"><span data-stu-id="b18f0-134">This isn't a real-world example, since the current time is something that does change often, and that moreover isn't complex to calculate.</span></span> <span data-ttu-id="b18f0-135">不過，這是說明快取實際運作的好方法。</span><span class="sxs-lookup"><span data-stu-id="b18f0-135">However, it's a good way to illustrate caching in action.</span></span>

1. <span data-ttu-id="b18f0-136">將名為*WebCache*的新頁面新增至網站。</span><span class="sxs-lookup"><span data-stu-id="b18f0-136">Add a new page named *WebCache.cshtml* to the website.</span></span>
2. <span data-ttu-id="b18f0-137">將下列程式碼和標記新增至頁面：</span><span class="sxs-lookup"><span data-stu-id="b18f0-137">Add the following code and markup to the page:</span></span>

    [!code-cshtml[Main](15-caching-to-improve-the-performance-of-your-website/samples/sample1.cshtml)]

    <span data-ttu-id="b18f0-138">當您快取資料時，您可以使用名稱，將它放入快取中，這在整個網站中都是唯一的。</span><span class="sxs-lookup"><span data-stu-id="b18f0-138">When you cache data, you put it into the cache using a name this is unique across the website.</span></span> <span data-ttu-id="b18f0-139">在此情況下，您將使用名為 `CachedTime`的快取專案。</span><span class="sxs-lookup"><span data-stu-id="b18f0-139">In this case, you'll use a cache entry named `CachedTime`.</span></span> <span data-ttu-id="b18f0-140">這是程式碼範例中所顯示的 `cacheItemKey`。</span><span class="sxs-lookup"><span data-stu-id="b18f0-140">This is the `cacheItemKey` shown in the code example.</span></span>

    <span data-ttu-id="b18f0-141">程式碼會先讀取 `CachedTime` 快取專案。</span><span class="sxs-lookup"><span data-stu-id="b18f0-141">The code first reads the `CachedTime` cache entry.</span></span> <span data-ttu-id="b18f0-142">如果傳回值（亦即，如果快取專案不是 null），則程式碼只會將時間變數的值設定為快取資料。</span><span class="sxs-lookup"><span data-stu-id="b18f0-142">If a value is returned (that is, if the cache entry isn't null), the code just sets the value of the time variable to the cache data.</span></span>

    <span data-ttu-id="b18f0-143">不過，如果快取專案不存在（亦即，它是 null），則程式碼會設定時間值、將它新增至快取，並將到期值設定為一分鐘。</span><span class="sxs-lookup"><span data-stu-id="b18f0-143">However, if the cache entry doesn't exist (that is, it's null), the code sets the time value, adds it to the cache, and sets an expiration value to one minute.</span></span> <span data-ttu-id="b18f0-144">一分鐘後，就會捨棄快取專案。</span><span class="sxs-lookup"><span data-stu-id="b18f0-144">After one minute, the cache entry is discarded.</span></span> <span data-ttu-id="b18f0-145">（快取中專案的預設到期值為20分鐘）。命令 `WebCache.Set(cacheItemKey, time, 1, false)` 顯示如何將目前時間值新增至快取，並將其到期日設定為1分鐘。</span><span class="sxs-lookup"><span data-stu-id="b18f0-145">(The default expiration value for an item in the cache is 20 minutes.) The command `WebCache.Set(cacheItemKey, time, 1, false)` shows how to add the current time value to the cache and set its expiration to 1 minute.</span></span> <span data-ttu-id="b18f0-146">將*slidingExpiration*參數設定為 `false` 表示每次要求時，不會更新到期時間。</span><span class="sxs-lookup"><span data-stu-id="b18f0-146">Setting the *slidingExpiration* parameter to `false` means the expiration time is not renewed each time it is requested.</span></span> <span data-ttu-id="b18f0-147">它在最初新增至快取之後，將會剛好在1分鐘後到期。</span><span class="sxs-lookup"><span data-stu-id="b18f0-147">It will expire exactly 1 minute after it was originally added to the cache.</span></span> <span data-ttu-id="b18f0-148">如果您將此值設定為 `true` 則每次從快取要求值時，就會重設1分鐘的到期時間。</span><span class="sxs-lookup"><span data-stu-id="b18f0-148">If you set this value to `true` the 1 minute expiration time is reset each time the value is requested from the cache.</span></span>

    <span data-ttu-id="b18f0-149">此程式碼說明當您快取資料時，應該一律使用的模式。</span><span class="sxs-lookup"><span data-stu-id="b18f0-149">This code illustrates the pattern you should always use when you cache data.</span></span> <span data-ttu-id="b18f0-150">在您取得快取的內容之前，請一律先檢查 `WebCache.Get` 方法是否傳回 null。</span><span class="sxs-lookup"><span data-stu-id="b18f0-150">Before you get something out of the cache, always check first whether the `WebCache.Get` method has returned null.</span></span> <span data-ttu-id="b18f0-151">請記住，快取專案可能已過期，或因為某些其他原因已移除，因此任何指定的專案永遠都不保證會在快取中。</span><span class="sxs-lookup"><span data-stu-id="b18f0-151">Remember that the cache entry might have expired or might have been removed for some other reason, so any given entry is never guaranteed to be in the cache.</span></span>
3. <span data-ttu-id="b18f0-152">在瀏覽器中執行*WebCache。*</span><span class="sxs-lookup"><span data-stu-id="b18f0-152">Run *WebCache.cshtml* in a browser.</span></span> <span data-ttu-id="b18f0-153">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）第一次要求頁面時，時間資料不在快取中，而且程式碼必須將時間值新增至快取。</span><span class="sxs-lookup"><span data-stu-id="b18f0-153">(Make sure the page is selected in the **Files** workspace before you run it.) The first time you request the page, the time data isn't in the cache, and the code has to add the time value to the cache.</span></span>

    ![cache-1](15-caching-to-improve-the-performance-of-your-website/_static/image1.jpg)
4. <span data-ttu-id="b18f0-155">在瀏覽器中重新整理*WebCache。*</span><span class="sxs-lookup"><span data-stu-id="b18f0-155">Refresh *WebCache.cshtml* in the browser.</span></span> <span data-ttu-id="b18f0-156">這次，時間資料會在快取中。</span><span class="sxs-lookup"><span data-stu-id="b18f0-156">This time, the time data is in the cache.</span></span> <span data-ttu-id="b18f0-157">請注意，自從上次查看頁面之後，時間尚未變更。</span><span class="sxs-lookup"><span data-stu-id="b18f0-157">Notice that the time hasn't changed since the last time you viewed the page.</span></span>

    ![cache-2](15-caching-to-improve-the-performance-of-your-website/_static/image2.jpg)
5. <span data-ttu-id="b18f0-159">等候一分鐘，讓快取清空，然後重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="b18f0-159">Wait one minute for the cache to be emptied, and then refresh the page.</span></span> <span data-ttu-id="b18f0-160">此頁面會再次指出快取中找不到時間資料，而且更新的時間會新增至快取。</span><span class="sxs-lookup"><span data-stu-id="b18f0-160">The page again indicates that the time data wasn't found in the cache, and the updated time is added to the cache.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="b18f0-161">其他資源</span><span class="sxs-lookup"><span data-stu-id="b18f0-161">Additional Resources</span></span>

- [<span data-ttu-id="b18f0-162">以圖表顯示資料</span><span class="sxs-lookup"><span data-stu-id="b18f0-162">Displaying Data in a Chart</span></span>](https://go.microsoft.com/fwlink/?LinkId=202895)
- <span data-ttu-id="b18f0-163">[WEBCACHE API 參考](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx)（MSDN）</span><span class="sxs-lookup"><span data-stu-id="b18f0-163">[WebCache API reference](https://msdn.microsoft.com/library/system.web.helpers.webcache(v=vs.99).aspx) (MSDN)</span></span>
