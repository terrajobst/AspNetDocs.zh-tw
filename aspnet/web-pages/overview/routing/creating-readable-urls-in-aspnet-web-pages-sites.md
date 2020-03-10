---
uid: web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
title: 在 ASP.NET Web Pages （Razor）網站中建立可讀取的 Url |Microsoft Docs
author: Rick-Anderson
description: 本文說明 ASP.NET Web Pages （Razor）網站中的路由，以及如何讓您使用更容易閱讀且更適合 SEO 的 Url。 您將 。
ms.author: riande
ms.date: 02/17/2014
ms.assetid: a8aac1ac-89de-4415-afe0-97a41c6423d2
msc.legacyurl: /web-pages/overview/routing/creating-readable-urls-in-aspnet-web-pages-sites
msc.type: authoredcontent
ms.openlocfilehash: 832db8e144cab730f16c78f67c12feb9b7c92c7c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628391"
---
# <a name="creating-readable-urls-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="60ca4-104">在 ASP.NET Web Pages （Razor）網站中建立可讀取的 Url</span><span class="sxs-lookup"><span data-stu-id="60ca4-104">Creating Readable URLs in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="60ca4-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="60ca4-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="60ca4-106">本文說明 ASP.NET Web Pages （Razor）網站中的路由，以及如何讓您使用更容易閱讀且更適合 SEO 的 Url。</span><span class="sxs-lookup"><span data-stu-id="60ca4-106">This article describes routing in an ASP.NET Web Pages (Razor) website, and how this lets you use URLs that are more readable and better for SEO.</span></span>
> 
> <span data-ttu-id="60ca4-107">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="60ca4-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="60ca4-108">ASP.NET 如何使用路由，讓您使用更容易閱讀和可搜尋的 Url。</span><span class="sxs-lookup"><span data-stu-id="60ca4-108">How ASP.NET uses routing to let you use more readable and searchable URLs.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="60ca4-109">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="60ca4-109">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="60ca4-110">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="60ca4-110">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="60ca4-111">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="60ca4-111">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-routing"></a><span data-ttu-id="60ca4-112">關於路由</span><span class="sxs-lookup"><span data-stu-id="60ca4-112">About Routing</span></span>

<span data-ttu-id="60ca4-113">網站中頁面的 Url 可能會影響網站運作的程度。</span><span class="sxs-lookup"><span data-stu-id="60ca4-113">The URLs for the pages in your site can have an impact on how well the site works.</span></span> <span data-ttu-id="60ca4-114">&quot;易記&quot; 的 URL 可讓使用者更輕鬆地使用網站。</span><span class="sxs-lookup"><span data-stu-id="60ca4-114">A URL that's &quot;friendly&quot; can make it easier for people to use the site.</span></span> <span data-ttu-id="60ca4-115">它也可以協助網站的搜尋引擎優化（SEO）。</span><span class="sxs-lookup"><span data-stu-id="60ca4-115">It can also help with search-engine optimization (SEO) for the site.</span></span> <span data-ttu-id="60ca4-116">ASP.NET 網站包含自動使用易記 Url 的功能。</span><span class="sxs-lookup"><span data-stu-id="60ca4-116">ASP.NET websites include the ability to use friendly URLs automatically.</span></span>

<span data-ttu-id="60ca4-117">ASP.NET 可讓您建立有意義的 Url 來描述使用者動作，而不是只指向伺服器上的檔案。</span><span class="sxs-lookup"><span data-stu-id="60ca4-117">ASP.NET lets you create meaningful URLs that describe user actions instead of just pointing to a file on the server.</span></span> <span data-ttu-id="60ca4-118">針對虛構的 blog，請考慮下列 Url：</span><span class="sxs-lookup"><span data-stu-id="60ca4-118">Consider these URLs for a fictional blog:</span></span>

- `http://www.contoso.com/Blog/blog.cshtml?categories=hardware`
- `http://www.contoso.com//Blog/blog.cshtml?startdate=2009-11-01&enddate=2009-11-30`

<span data-ttu-id="60ca4-119">比較這些 Url 與下列各項：</span><span class="sxs-lookup"><span data-stu-id="60ca4-119">Compare those URLs to the following ones:</span></span>

- `http://www.contoso.com/Blog/categories/hardware/`
- `http://www.contoso.com/Blog/2009/November`

<span data-ttu-id="60ca4-120">在第一組中，使用者必須知道使用 [ *blog* ] 頁面來顯示該 blog，然後必須建立查詢字串，以取得正確的類別或日期範圍。</span><span class="sxs-lookup"><span data-stu-id="60ca4-120">In the first pair, a user would have to know that the blog is displayed using the *blog.cshtml* page, and would then have to construct a query string that gets the right category or date range.</span></span> <span data-ttu-id="60ca4-121">第二組範例較容易理解和建立。</span><span class="sxs-lookup"><span data-stu-id="60ca4-121">The second set of examples is much easier to comprehend and create.</span></span>

<span data-ttu-id="60ca4-122">第一個範例的 Url 也會直接指向特定檔案（*blog. cshtml*）。</span><span class="sxs-lookup"><span data-stu-id="60ca4-122">The URLs for the first example also point directly to a specific file (*blog.cshtml*).</span></span> <span data-ttu-id="60ca4-123">如果基於某些原因而將 blog 移至伺服器上的另一個資料夾，或者如果重新撰寫的是使用不同的頁面，則連結會錯誤。</span><span class="sxs-lookup"><span data-stu-id="60ca4-123">If for some reason the blog were moved to another folder on the server, or if the blog were rewritten to use a different page, the links would be wrong.</span></span> <span data-ttu-id="60ca4-124">第二組 Url 並不會指向特定的頁面，因此即使 blog 的執行或位置變更，Url 仍然有效。</span><span class="sxs-lookup"><span data-stu-id="60ca4-124">The second set of URLs doesn't point to a specific page, so even if the blog implementation or location changes, the URLs would still be valid.</span></span>

<span data-ttu-id="60ca4-125">在 ASP.NET Web Pages 中，您可以建立更易懂的 Url，如同上述範例中的一樣，因為 ASP.NET 會使用*路由*。</span><span class="sxs-lookup"><span data-stu-id="60ca4-125">In ASP.NET Web Pages, you can create friendlier URLs like those in the above examples because ASP.NET uses *routing*.</span></span> <span data-ttu-id="60ca4-126">路由會從可滿足要求的頁面（或頁面）的 URL 建立邏輯對應。</span><span class="sxs-lookup"><span data-stu-id="60ca4-126">Routing creates logical mapping from a URL to a page (or pages) that can fulfill the request.</span></span> <span data-ttu-id="60ca4-127">因為對應是邏輯的（非實體、特定的檔案），所以路由在定義網站 Url 的方式上提供了極大的彈性。</span><span class="sxs-lookup"><span data-stu-id="60ca4-127">Because the mapping is logical (not physical, to a specific file), routing provides great flexibility in how you define the URLs for your site.</span></span>

## <a name="how-routing-works"></a><span data-ttu-id="60ca4-128">路由的運作方式</span><span class="sxs-lookup"><span data-stu-id="60ca4-128">How Routing Works</span></span>

<span data-ttu-id="60ca4-129">當 ASP.NET 處理要求時，它會讀取 URL 以決定如何路由傳送。</span><span class="sxs-lookup"><span data-stu-id="60ca4-129">When ASP.NET processes a request, it reads the URL to determine how to route it.</span></span> <span data-ttu-id="60ca4-130">ASP.NET 會嘗試比對 URL 的個別區段與磁片上的檔案（從左至右）。</span><span class="sxs-lookup"><span data-stu-id="60ca4-130">ASP.NET tries to match individual segments of the URL to files on disk, going from left to right.</span></span> <span data-ttu-id="60ca4-131">如果有相符專案，則 URL 中剩餘的任何內容都會以*路徑資訊*的形式傳遞至頁面。</span><span class="sxs-lookup"><span data-stu-id="60ca4-131">If there's a match, anything remaining in the URL is passed to the page as *path information*.</span></span>

<span data-ttu-id="60ca4-132">假設有人使用此 URL 提出要求：</span><span class="sxs-lookup"><span data-stu-id="60ca4-132">Imagine that someone makes a request using this URL:</span></span>

`http://www.contoso.com/a/b/c`

<span data-ttu-id="60ca4-133">搜尋如下所示：</span><span class="sxs-lookup"><span data-stu-id="60ca4-133">The search goes like this:</span></span>

1. <span data-ttu-id="60ca4-134">是否有檔案的路徑和名稱為 */a/b/c.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="60ca4-134">Is there a file with the path and name of */a/b/c.cshtml*?</span></span> <span data-ttu-id="60ca4-135">若是如此，請執行該頁面，並不傳遞任何資訊。</span><span class="sxs-lookup"><span data-stu-id="60ca4-135">If so, run that page and pass no information to it.</span></span> <span data-ttu-id="60ca4-136">否則...</span><span class="sxs-lookup"><span data-stu-id="60ca4-136">Otherwise ...</span></span>
2. <span data-ttu-id="60ca4-137">是否有檔案的路徑和名稱為 */a/b.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="60ca4-137">Is there a file with the path and name of */a/b.cshtml*?</span></span> <span data-ttu-id="60ca4-138">若是如此，請執行該頁面，並將值 `c` 傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="60ca4-138">If so, run that page and pass the value `c` to it.</span></span> <span data-ttu-id="60ca4-139">否則 。</span><span class="sxs-lookup"><span data-stu-id="60ca4-139">Otherwise …</span></span>
3. <span data-ttu-id="60ca4-140">是否有檔案的路徑和名稱為 */a.cshtml*？</span><span class="sxs-lookup"><span data-stu-id="60ca4-140">Is there a file with the path and name of */a.cshtml*?</span></span> <span data-ttu-id="60ca4-141">若是如此，請執行該頁面，並將值 `b/c` 傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="60ca4-141">If so, run that page and pass the value `b/c` to it.</span></span>

<span data-ttu-id="60ca4-142">如果搜尋在其指定的資料夾中找不到與*cshtml*檔案完全相符的專案，ASP.NET 會繼續依序尋找這些檔案：</span><span class="sxs-lookup"><span data-stu-id="60ca4-142">If the search found no exact matches for *.cshtml* files in their specified folders, ASP.NET continues looking for these files in turn:</span></span>

1. <span data-ttu-id="60ca4-143">*/a/b/c/default.cshtml* （沒有路徑資訊）。</span><span class="sxs-lookup"><span data-stu-id="60ca4-143">*/a/b/c/default.cshtml* (no path information).</span></span>
2. <span data-ttu-id="60ca4-144">*/a/b/c/index.cshtml* （沒有路徑資訊）。</span><span class="sxs-lookup"><span data-stu-id="60ca4-144">*/a/b/c/index.cshtml* (no path information).</span></span>

> [!NOTE]
> <span data-ttu-id="60ca4-145">更明確地說，特定頁面的要求（也就是包含 .rc 副檔名*的要求*）的運作方式就如同您所預期。</span><span class="sxs-lookup"><span data-stu-id="60ca4-145">To be clear, requests for specific pages (that is, requests that include the *.cshtml* filename extension) work just like you'd expect.</span></span> <span data-ttu-id="60ca4-146">`http://www.contoso.com/a/b.cshtml` 之類的要求將會執行頁面*b. cshtml* 。</span><span class="sxs-lookup"><span data-stu-id="60ca4-146">A request like `http://www.contoso.com/a/b.cshtml` will run the page *b.cshtml* just fine.</span></span>

<span data-ttu-id="60ca4-147">在頁面中，您可以透過頁面的 `UrlData` 屬性（也就是字典）取得路徑資訊。</span><span class="sxs-lookup"><span data-stu-id="60ca4-147">Inside a page, you can get the path information via the page's `UrlData` property, which is a dictionary.</span></span> <span data-ttu-id="60ca4-148">假設您有一個名為*ViewCustomers*的檔案，而您的網站取得此要求：</span><span class="sxs-lookup"><span data-stu-id="60ca4-148">Imagine that you have a file named *ViewCustomers.cshtml* and your site gets this request:</span></span>

`http://mysite.com/myWebSite/ViewCustomers/1000`

<span data-ttu-id="60ca4-149">如上述規則所述，要求將會移至您的頁面。</span><span class="sxs-lookup"><span data-stu-id="60ca4-149">As described in the rules above, the request will go to your page.</span></span> <span data-ttu-id="60ca4-150">在頁面中，您可以使用類似下列的程式碼來取得和顯示路徑資訊（在此案例中，值 &quot;1000&quot;）：</span><span class="sxs-lookup"><span data-stu-id="60ca4-150">Inside the page, you can use code like the following to get and display the path information (in this case, the value &quot;1000&quot;):</span></span>

[!code-html[Main](creating-readable-urls-in-aspnet-web-pages-sites/samples/sample1.html)]

> [!NOTE]
> <span data-ttu-id="60ca4-151">由於路由不會包含完整的檔案名，因此如果您有相同名稱但副檔名不同的頁面（例如， *mypage.aspx*和*mypage.aspx*），則可能會造成混淆。</span><span class="sxs-lookup"><span data-stu-id="60ca4-151">Because routing doesn't involve complete file names, there can be ambiguity if you have pages that have the same name but different file-name extensions (for example, *MyPage.cshtml* and *MyPage.html*).</span></span> <span data-ttu-id="60ca4-152">為了避免路由的問題，最好確保您的網站中沒有其名稱只會與延伸模組不同的頁面。</span><span class="sxs-lookup"><span data-stu-id="60ca4-152">In order to avoid problems with routing, it's best to make sure that you don't have pages in your site whose names differ only in their extension.</span></span>

<a id="Additional_Resources"></a>
## <a name="additional-resources"></a><span data-ttu-id="60ca4-153">其他資源</span><span class="sxs-lookup"><span data-stu-id="60ca4-153">Additional Resources</span></span>

<span data-ttu-id="60ca4-154">[WebMatrix-SEO 的 url、urldata.base 和路由](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO)。</span><span class="sxs-lookup"><span data-stu-id="60ca4-154">[WebMatrix - URLs, UrlData and Routing for SEO](http://www.mikesdotnetting.com/Article/165/WebMatrix-URLs-UrlData-and-Routing-for-SEO).</span></span> <span data-ttu-id="60ca4-155">Mike Brind 的此 blog 專案提供了有關路由在 ASP.NET Web Pages 中的運作方式的其他詳細資料。</span><span class="sxs-lookup"><span data-stu-id="60ca4-155">This blog entry by Mike Brind provides some additional details on how routing works in ASP.NET Web Pages.</span></span>
