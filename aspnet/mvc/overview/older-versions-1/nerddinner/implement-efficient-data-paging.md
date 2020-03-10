---
uid: mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
title: 實行有效率的資料分頁 |Microsoft Docs
author: microsoft
description: 步驟8顯示如何將分頁支援新增至我們的/Dinners URL，如此一來，不會一次顯示 Dinners 的數千個，我們只會顯示10個即將到來的 Dinners 。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: adea836d-dbc2-4005-94ea-53aef09e9e34
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/implement-efficient-data-paging
msc.type: authoredcontent
ms.openlocfilehash: 2d9a0dba381b71755ac626f76d52bc5bcb434447
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78601049"
---
# <a name="implement-efficient-data-paging"></a><span data-ttu-id="e2139-103">實作有效率的資料分頁</span><span class="sxs-lookup"><span data-stu-id="e2139-103">Implement Efficient Data Paging</span></span>

<span data-ttu-id="e2139-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="e2139-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="e2139-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="e2139-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="e2139-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟8，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2139-106">This is step 8 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="e2139-107">步驟8顯示如何將分頁支援新增至我們的/Dinners URL，如此一來，不會一次顯示 Dinners 的數千個，而是一次只顯示10個即將推出的 Dinners，並讓使用者以 SEO 易記的方式，透過整個清單來翻頁或往後轉。</span><span class="sxs-lookup"><span data-stu-id="e2139-107">Step 8 shows how to add paging support to our /Dinners URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>
> 
> <span data-ttu-id="e2139-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="e2139-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-8-paging-support"></a><span data-ttu-id="e2139-109">NerdDinner 步驟8：分頁支援</span><span class="sxs-lookup"><span data-stu-id="e2139-109">NerdDinner Step 8: Paging Support</span></span>

<span data-ttu-id="e2139-110">如果我們的網站成功，將會有數千個即將推出的 dinners。</span><span class="sxs-lookup"><span data-stu-id="e2139-110">If our site is successful, it will have thousands of upcoming dinners.</span></span> <span data-ttu-id="e2139-111">我們必須確定我們的 UI 會進行調整以處理所有的 dinners，並允許使用者流覽。</span><span class="sxs-lookup"><span data-stu-id="e2139-111">We need to make sure that our UI scales to handle all of these dinners, and allows users to browse them.</span></span> <span data-ttu-id="e2139-112">若要啟用這項功能，我們會將分頁支援新增至我們的 */Dinners* URL，如此一來，就不會一次顯示 Dinners 的數千個，而是可讓使用者以 SEO 易懂的方式，在整個清單中翻頁並向前復原。</span><span class="sxs-lookup"><span data-stu-id="e2139-112">To enable this, we'll add paging support to our */Dinners* URL so that instead of displaying 1000s of dinners at once, we'll only display 10 upcoming dinners at a time - and allow end-users to page back and forward through the entire list in an SEO friendly way.</span></span>

### <a name="index-action-method-recap"></a><span data-ttu-id="e2139-113">Index （）動作方法的回顧</span><span class="sxs-lookup"><span data-stu-id="e2139-113">Index() Action Method Recap</span></span>

<span data-ttu-id="e2139-114">我們的 DinnersController 類別內的 Index （）動作方法目前如下所示：</span><span class="sxs-lookup"><span data-stu-id="e2139-114">The Index() action method within our DinnersController class currently looks like below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

<span data-ttu-id="e2139-115">對 */Dinners* URL 提出要求時，它會抓取所有即將推出的 Dinners 清單，然後再呈現所有的列出內容：</span><span class="sxs-lookup"><span data-stu-id="e2139-115">When a request is made to the */Dinners* URL, it retrieves a list of all upcoming dinners and then renders a listing of all of them out:</span></span>

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a><span data-ttu-id="e2139-116">瞭解 IQueryable&lt;T&gt;</span><span class="sxs-lookup"><span data-stu-id="e2139-116">Understanding IQueryable&lt;T&gt;</span></span>

<span data-ttu-id="e2139-117">*IQueryable&lt;t&gt;* 是以 LINQ 引進的介面，做為 .net 3.5 的一部分。</span><span class="sxs-lookup"><span data-stu-id="e2139-117">*IQueryable&lt;T&gt;* is an interface that was introduced with LINQ as part of .NET 3.5.</span></span> <span data-ttu-id="e2139-118">它提供強大的「延後執行」案例，可讓我們利用來實行分頁支援。</span><span class="sxs-lookup"><span data-stu-id="e2139-118">It enables powerful "deferred execution" scenarios that we can take advantage of to implement paging support.</span></span>

<span data-ttu-id="e2139-119">在我們的 DinnerRepository 中，我們會從 FindUpcomingDinners （）方法傳回 IQueryable&lt;晚餐&gt; 序列：</span><span class="sxs-lookup"><span data-stu-id="e2139-119">In our DinnerRepository we are returning an IQueryable&lt;Dinner&gt; sequence from our FindUpcomingDinners() method:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

<span data-ttu-id="e2139-120">FindUpcomingDinners （）方法所傳回的 IQueryable&lt;晚餐&gt; 物件會封裝一個查詢，以使用 LINQ to SQL 從我們的資料庫中取出晚餐物件。</span><span class="sxs-lookup"><span data-stu-id="e2139-120">The IQueryable&lt;Dinner&gt; object returned by our FindUpcomingDinners() method encapsulates a query to retrieve Dinner objects from our database using LINQ to SQL.</span></span> <span data-ttu-id="e2139-121">重要的是，它不會對資料庫執行查詢，直到我們嘗試存取/逐一查看查詢中的資料，或直到我們在其上呼叫 ToList （）方法為止。</span><span class="sxs-lookup"><span data-stu-id="e2139-121">Importantly, it won't execute the query against the database until we attempt to access/iterate over the data in the query, or until we call the ToList() method on it.</span></span> <span data-ttu-id="e2139-122">呼叫我們的 FindUpcomingDinners （）方法的程式碼可選擇性地選擇在執行查詢之前，將額外的「連鎖」作業/篩選器新增至 IQueryable&lt;晚餐&gt; 物件。</span><span class="sxs-lookup"><span data-stu-id="e2139-122">The code calling our FindUpcomingDinners() method can optionally choose to add additional "chained" operations/filters to the IQueryable&lt;Dinner&gt; object before executing the query.</span></span> <span data-ttu-id="e2139-123">LINQ to SQL 之後，就有足夠的智慧，可以在要求資料時，對資料庫執行合併的查詢。</span><span class="sxs-lookup"><span data-stu-id="e2139-123">LINQ to SQL is then smart enough to execute the combined query against the database when the data is requested.</span></span>

<span data-ttu-id="e2139-124">若要執行分頁邏輯，我們可以更新 DinnersController 的 Index （）動作方法，以便在對其呼叫 ToList （）之前，將額外的 "Skip" 和 "Take" 運算子套用至傳回的 IQueryable&lt;晚餐&gt; 序列：</span><span class="sxs-lookup"><span data-stu-id="e2139-124">To implement paging logic we can update our DinnersController's Index() action method so that it applies additional "Skip" and "Take" operators to the returned IQueryable&lt;Dinner&gt; sequence before calling ToList() on it:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

<span data-ttu-id="e2139-125">上述程式碼會略過資料庫中前10名即將推出的 dinners，然後傳回 20 dinners。</span><span class="sxs-lookup"><span data-stu-id="e2139-125">The above code skips over the first 10 upcoming dinners in the database, and then returns back 20 dinners.</span></span> <span data-ttu-id="e2139-126">LINQ to SQL 非常聰明，可以用來建立優化的 SQL 查詢，以在 SQL 資料庫中執行此略過邏輯（而不是在 web 伺服器上）。</span><span class="sxs-lookup"><span data-stu-id="e2139-126">LINQ to SQL is smart enough to construct an optimized SQL query that performs this skipping logic in the SQL database – and not in the web-server.</span></span> <span data-ttu-id="e2139-127">這表示即使在資料庫中有數百萬個即將推出的 Dinners，只會在此要求中抓取10個我們想要的部分（使其有效率且可調整）。</span><span class="sxs-lookup"><span data-stu-id="e2139-127">This means that even if we have millions of upcoming Dinners in the database, only the 10 we want will be retrieved as part of this request (making it efficient and scalable).</span></span>

### <a name="adding-a-page-value-to-the-url"></a><span data-ttu-id="e2139-128">將 "page" 值新增至 URL</span><span class="sxs-lookup"><span data-stu-id="e2139-128">Adding a "page" value to the URL</span></span>

<span data-ttu-id="e2139-129">我們不會將特定頁面範圍硬式編碼，而是要讓 Url 包含 "page" 參數，以指出使用者要求的晚餐範圍。</span><span class="sxs-lookup"><span data-stu-id="e2139-129">Instead of hard-coding a specific page range, we'll want our URLs to include a "page" parameter that indicates which Dinner range a user is requesting.</span></span>

#### <a name="using-a-querystring-value"></a><span data-ttu-id="e2139-130">使用 Querystring 值</span><span class="sxs-lookup"><span data-stu-id="e2139-130">Using a Querystring value</span></span>

<span data-ttu-id="e2139-131">下列程式碼示範如何更新索引（）動作方法，以支援 querystring 參數並啟用 Url，例如 */Dinners？ page = 2*：</span><span class="sxs-lookup"><span data-stu-id="e2139-131">The code below demonstrates how we can update our Index() action method to support a querystring parameter and enable URLs like */Dinners?page=2*:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

<span data-ttu-id="e2139-132">上述 Index （）動作方法具有名為 "page" 的參數。</span><span class="sxs-lookup"><span data-stu-id="e2139-132">The Index() action method above has a parameter named "page".</span></span> <span data-ttu-id="e2139-133">參數會宣告為可為 null 的整數（也就是 int？表示）。</span><span class="sxs-lookup"><span data-stu-id="e2139-133">The parameter is declared as a nullable integer (that is what int? indicates).</span></span> <span data-ttu-id="e2139-134">這表示 */Dinners？ page = 2* URL 會導致 "2" 的值當做參數值傳遞。</span><span class="sxs-lookup"><span data-stu-id="e2139-134">This means that the */Dinners?page=2* URL will cause a value of "2" to be passed as the parameter value.</span></span> <span data-ttu-id="e2139-135">*/Dinners* URL （不含 querystring 值）會導致傳遞 null 值。</span><span class="sxs-lookup"><span data-stu-id="e2139-135">The */Dinners* URL (without a querystring value) will cause a null value to be passed.</span></span>

<span data-ttu-id="e2139-136">我們會將頁面值乘以頁面大小（在此案例中為10個數據列），以判斷要略過多少 dinners。</span><span class="sxs-lookup"><span data-stu-id="e2139-136">We are multiplying the page value by the page size (in this case 10 rows) to determine how many dinners to skip over.</span></span> <span data-ttu-id="e2139-137">我們使用[ C# null 「聯合」運算子（？）](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) ，這在處理可為 null 的類型時非常有用。</span><span class="sxs-lookup"><span data-stu-id="e2139-137">We are using the [C# null "coalescing" operator (??)](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) which is useful when dealing with nullable types.</span></span> <span data-ttu-id="e2139-138">上述程式碼會在頁面參數為 null 時，將值指派為0。</span><span class="sxs-lookup"><span data-stu-id="e2139-138">The code above assigns page the value of 0 if the page parameter is null.</span></span>

#### <a name="using-embedded-url-values"></a><span data-ttu-id="e2139-139">使用內嵌的 URL 值</span><span class="sxs-lookup"><span data-stu-id="e2139-139">Using Embedded URL values</span></span>

<span data-ttu-id="e2139-140">使用 querystring 值的替代方法是在實際 URL 本身內內嵌 page 參數。</span><span class="sxs-lookup"><span data-stu-id="e2139-140">An alternative to using a querystring value would be to embed the page parameter within the actual URL itself.</span></span> <span data-ttu-id="e2139-141">例如： */Dinners/Page/2*或 */Dinners/2*。</span><span class="sxs-lookup"><span data-stu-id="e2139-141">For example: */Dinners/Page/2* or */Dinners/2*.</span></span> <span data-ttu-id="e2139-142">ASP.NET MVC 包含強大的 URL 路由引擎，可讓您輕鬆地支援這類案例。</span><span class="sxs-lookup"><span data-stu-id="e2139-142">ASP.NET MVC includes a powerful URL routing engine that makes it easy to support scenarios like this.</span></span>

<span data-ttu-id="e2139-143">我們可以註冊自訂路由規則，將任何傳入 URL 或 URL 格式對應至我們想要的任何控制器類別或動作方法。</span><span class="sxs-lookup"><span data-stu-id="e2139-143">We can register custom routing rules that map any incoming URL or URL format to any controller class or action method we want.</span></span> <span data-ttu-id="e2139-144">我們只需要在專案中開啟 global.asax 檔案就可以了：</span><span class="sxs-lookup"><span data-stu-id="e2139-144">All we need to-do is to open the Global.asax file within our project:</span></span>

![](implement-efficient-data-paging/_static/image2.png)

<span data-ttu-id="e2139-145">然後使用 Maproute.html （） helper 方法（例如第一次呼叫路由）來註冊新的對應規則。Maproute.html （）如下：</span><span class="sxs-lookup"><span data-stu-id="e2139-145">And then register a new mapping rule using the MapRoute() helper method like the first call to routes.MapRoute() below:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

<span data-ttu-id="e2139-146">在上述情況中，我們會註冊名為 "UpcomingDinners" 的新路由規則。</span><span class="sxs-lookup"><span data-stu-id="e2139-146">Above we are registering a new routing rule named "UpcomingDinners".</span></span> <span data-ttu-id="e2139-147">我們指出它的 URL 格式為 "Dinners/Page/{Page}"，其中 {Page} 是內嵌在 URL 內的參數值。</span><span class="sxs-lookup"><span data-stu-id="e2139-147">We are indicating it has the URL format "Dinners/Page/{page}" – where {page} is a parameter value embedded within the URL.</span></span> <span data-ttu-id="e2139-148">Maproute.html （）方法的第三個參數指出，我們應該將符合此格式的 Url 對應至 DinnersController 類別上的 Index （）動作方法。</span><span class="sxs-lookup"><span data-stu-id="e2139-148">The third parameter to the MapRoute() method indicates that we should map URLs that match this format to the Index() action method on the DinnersController class.</span></span>

<span data-ttu-id="e2139-149">我們可以在 Querystring 案例中使用與之前相同的索引（）程式碼，但現在我們的 "page" 參數會來自 URL，而不是 Querystring：</span><span class="sxs-lookup"><span data-stu-id="e2139-149">We can use the exact same Index() code we had before with our Querystring scenario – except now our "page" parameter will come from the URL and not the querystring:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

<span data-ttu-id="e2139-150">現在當我們執行應用程式並輸入 */Dinners*時，我們會看到前10個即將推出的 Dinners：</span><span class="sxs-lookup"><span data-stu-id="e2139-150">And now when we run the application and type in */Dinners* we'll see the first 10 upcoming dinners:</span></span>

![](implement-efficient-data-paging/_static/image3.png)

<span data-ttu-id="e2139-151">當我們輸入 */Dinners/Page/1*時，我們會看到下一個 Dinners 頁面：</span><span class="sxs-lookup"><span data-stu-id="e2139-151">And when we type in */Dinners/Page/1* we'll see the next page of dinners:</span></span>

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a><span data-ttu-id="e2139-152">新增頁面導覽 UI</span><span class="sxs-lookup"><span data-stu-id="e2139-152">Adding page navigation UI</span></span>

<span data-ttu-id="e2139-153">完成分頁案例的最後一個步驟，是在我們的 view 範本內執行「下一步」和「上一頁」導覽 UI，讓使用者可以輕鬆地略過晚餐資料。</span><span class="sxs-lookup"><span data-stu-id="e2139-153">The last step to complete our paging scenario will be to implement "next" and "previous" navigation UI within our view template to enable users to easily skip over the Dinner data.</span></span>

<span data-ttu-id="e2139-154">若要正確執行此功能，我們必須知道資料庫中的 Dinners 總數，以及此轉譯的資料頁數。</span><span class="sxs-lookup"><span data-stu-id="e2139-154">To implement this correctly, we'll need to know the total number of Dinners in the database, as well as how many pages of data this translates to.</span></span> <span data-ttu-id="e2139-155">接著，我們需要計算目前要求的 "page" 值是否在資料的開頭或結尾，並據以顯示或隱藏 "previous" 和 "next" UI。</span><span class="sxs-lookup"><span data-stu-id="e2139-155">We'll then need to calculate whether the currently requested "page" value is at the beginning or end of the data, and show or hide the "previous" and "next" UI accordingly.</span></span> <span data-ttu-id="e2139-156">我們可以在 Index （）動作方法內執行此邏輯。</span><span class="sxs-lookup"><span data-stu-id="e2139-156">We could implement this logic within our Index() action method.</span></span> <span data-ttu-id="e2139-157">或者，我們可以將協助程式類別新增至我們的專案，以更重複使用的方式封裝此邏輯。</span><span class="sxs-lookup"><span data-stu-id="e2139-157">Alternatively we can add a helper class to our project that encapsulates this logic in a more re-usable way.</span></span>

<span data-ttu-id="e2139-158">以下是一個簡單的 "PaginatedList" 協助程式類別，衍生自內建 .NET Framework 的清單&lt;T&gt; 集合類別。</span><span class="sxs-lookup"><span data-stu-id="e2139-158">Below is a simple "PaginatedList" helper class that derives from the List&lt;T&gt; collection class built-into the .NET Framework.</span></span> <span data-ttu-id="e2139-159">它會執行可重複使用的集合類別，可用來將任何 IQueryable 資料的序列分頁。</span><span class="sxs-lookup"><span data-stu-id="e2139-159">It implements a re-usable collection class that can be used to paginate any sequence of IQueryable data.</span></span> <span data-ttu-id="e2139-160">在我們的 NerdDinner 應用程式中，我們會將它用於 IQueryable&lt;晚餐&gt; 結果，但它可以輕鬆地在其他應用程式案例中，用於 IQueryable&lt;產品&gt; 或 IQueryable&lt;客戶&gt; 結果：</span><span class="sxs-lookup"><span data-stu-id="e2139-160">In our NerdDinner application we'll have it work over IQueryable&lt;Dinner&gt; results, but it could just as easily be used against IQueryable&lt;Product&gt; or IQueryable&lt;Customer&gt; results in other application scenarios:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

<span data-ttu-id="e2139-161">請注意它的計算方式，然後公開屬性，例如 "PageIndex"、"PageSize"、"TotalCount" 和 "TotalPages"。</span><span class="sxs-lookup"><span data-stu-id="e2139-161">Notice above how it calculates and then exposes properties like "PageIndex", "PageSize", "TotalCount", and "TotalPages".</span></span> <span data-ttu-id="e2139-162">然後，它也會公開兩個 helper 屬性 "HasPreviousPage" 和 "HasNextPage"，指出集合中的資料頁是否位於原始序列的開頭或結尾。</span><span class="sxs-lookup"><span data-stu-id="e2139-162">It also then exposes two helper properties "HasPreviousPage" and "HasNextPage" that indicate whether the page of data in the collection is at the beginning or end of the original sequence.</span></span> <span data-ttu-id="e2139-163">上述程式碼會執行兩個 SQL 查詢，第一個是抓取晚餐物件總數的計數（這不會傳回物件，而是會執行可傳回整數的「選取計數」語句），而第二個則是只取得的資料列我們在資料庫中所需的資料，以取得目前的資料頁面。</span><span class="sxs-lookup"><span data-stu-id="e2139-163">The above code will cause two SQL queries to be run - the first to retrieve the count of the total number of Dinner objects (this doesn't return the objects – rather it performs a "SELECT COUNT" statement that returns an integer), and the second to retrieve just the rows of data we need from our database for the current page of data.</span></span>

<span data-ttu-id="e2139-164">然後，我們可以更新 DinnersController （）協助程式方法，從 DinnerRepository FindUpcomingDinners （）結果中建立 PaginatedList&lt;晚餐&gt;，並將它傳遞給我們的 view 範本：</span><span class="sxs-lookup"><span data-stu-id="e2139-164">We can then update our DinnersController.Index() helper method to create a PaginatedList&lt;Dinner&gt; from our DinnerRepository.FindUpcomingDinners() result, and pass it to our view template:</span></span>

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

<span data-ttu-id="e2139-165">然後，我們可以更新 \Views\Dinners\Index.aspx view 範本，使其繼承自 ViewPage&lt;NerdDinner。 PaginatedList&lt;晚餐&gt;&gt;，而不是 ViewPage&lt;IEnumerable&lt;晚餐&gt;&gt;，然後將下列程式碼新增至我們的視圖範本底部，以顯示或隱藏下一個和上一個導覽 UI：</span><span class="sxs-lookup"><span data-stu-id="e2139-165">We can then update the \Views\Dinners\Index.aspx view template to inherit from ViewPage&lt;NerdDinner.Helpers.PaginatedList&lt;Dinner&gt;&gt; instead of ViewPage&lt;IEnumerable&lt;Dinner&gt;&gt;, and then add the following code to the bottom of our view-template to show or hide next and previous navigation UI:</span></span>

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

<span data-ttu-id="e2139-166">請注意，我們如何使用 RouteLink （） helper 方法來產生我們的超連結。</span><span class="sxs-lookup"><span data-stu-id="e2139-166">Notice above how we are using the Html.RouteLink() helper method to generate our hyperlinks.</span></span> <span data-ttu-id="e2139-167">這個方法與我們先前使用的 .Html （） helper 方法類似。</span><span class="sxs-lookup"><span data-stu-id="e2139-167">This method is similar to the Html.ActionLink() helper method we've used previously.</span></span> <span data-ttu-id="e2139-168">其差異在於，我們會使用我們在 global.asax 檔案中設定的 "UpcomingDinners" 路由規則來產生 URL。</span><span class="sxs-lookup"><span data-stu-id="e2139-168">The difference is that we are generating the URL using the "UpcomingDinners" routing rule we setup within our Global.asax file.</span></span> <span data-ttu-id="e2139-169">這可確保我們會產生 Url 給我們的 Index （）動作方法，其格式為： */Dinners/Page/{page}* –其中 {Page} 值是我們根據目前的 PageIndex 提供的變數。</span><span class="sxs-lookup"><span data-stu-id="e2139-169">This ensures that we'll generate URLs to our Index() action method that have the format: */Dinners/Page/{page}* – where the {page} value is a variable we are providing above based on the current PageIndex.</span></span>

<span data-ttu-id="e2139-170">現在當我們再次執行應用程式時，我們會在瀏覽器中一次看到10個 dinners：</span><span class="sxs-lookup"><span data-stu-id="e2139-170">And now when we run our application again we'll see 10 dinners at a time in our browser:</span></span>

![](implement-efficient-data-paging/_static/image5.png)

<span data-ttu-id="e2139-171">我們也在頁面底部有 &lt;&lt;&lt; 和 &gt;&gt;&gt; 流覽 UI，可讓我們使用搜尋引擎可存取的 Url 來略過資料的向前和向後：</span><span class="sxs-lookup"><span data-stu-id="e2139-171">We also have &lt;&lt;&lt; and &gt;&gt;&gt; navigation UI at the bottom of the page that allows us to skip forwards and backwards over our data using search engine accessible URLs:</span></span>

![](implement-efficient-data-paging/_static/image6.png)

| <span data-ttu-id="e2139-172">**側邊主題：瞭解 IQueryable&lt;T&gt; 的含意**</span><span class="sxs-lookup"><span data-stu-id="e2139-172">**Side Topic: Understanding the implications of IQueryable&lt;T&gt;**</span></span> |
| --- |
| <span data-ttu-id="e2139-173">IQueryable&lt;T&gt; 是一項非常強大的功能，可啟用各種有趣的延後執行案例（例如分頁和以撰寫為基礎的查詢）。</span><span class="sxs-lookup"><span data-stu-id="e2139-173">IQueryable&lt;T&gt; is a very powerful feature that enables a variety of interesting deferred execution scenarios (like paging and composition based queries).</span></span> <span data-ttu-id="e2139-174">如同所有強大的功能，您會想要小心使用它，並確定它不會被濫用。</span><span class="sxs-lookup"><span data-stu-id="e2139-174">As with all powerful features, you want to be careful with how you use it and make sure it is not abused.</span></span> <span data-ttu-id="e2139-175">請務必辨識，從您的存放庫傳回 IQueryable&lt;T&gt; 結果，可讓呼叫程式碼在連結的運算子方法上附加，並參與終極查詢執行。</span><span class="sxs-lookup"><span data-stu-id="e2139-175">It is important to recognize that returning an IQueryable&lt;T&gt; result from your repository enables calling code to append on chained operator methods to it, and so participate in the ultimate query execution.</span></span> <span data-ttu-id="e2139-176">如果您不想要提供呼叫程式碼這項功能，則應該傳回反向 IList&lt;T&gt; 或 IEnumerable&lt;T&gt; 結果，其中包含已執行之查詢的結果。</span><span class="sxs-lookup"><span data-stu-id="e2139-176">If you do not want to provide calling code this ability, then you should return back IList&lt;T&gt; or IEnumerable&lt;T&gt; results - which contain the results of a query that has already executed.</span></span> <span data-ttu-id="e2139-177">針對分頁案例，這會要求您將實際的資料分頁邏輯推送至所呼叫的存放庫方法。</span><span class="sxs-lookup"><span data-stu-id="e2139-177">For pagination scenarios this would require you to push the actual data pagination logic into the repository method being called.</span></span> <span data-ttu-id="e2139-178">在此案例中，我們可能會更新 FindUpcomingDinners （） finder 方法，使其具有傳回 PaginatedList 的簽章： PaginatedList&lt; 晚餐&gt; FindUpcomingDinners （int pageIndex，int pageSize） {} 或傳回 IList&lt;晚餐&gt;，並使用 "totalCount" out 參數來傳回 Dinners 的總計數： IList&lt;晚餐&gt; FindUpcomingDinners （int pageIndex，int pageSize，out int totalCount） {}</span><span class="sxs-lookup"><span data-stu-id="e2139-178">In this scenario we might update our FindUpcomingDinners() finder method to have a signature that either returned a PaginatedList: PaginatedList&lt; Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize) { } Or return back an IList&lt;Dinner&gt;, and use a "totalCount" out param to return the total count of Dinners: IList&lt;Dinner&gt; FindUpcomingDinners(int pageIndex, int pageSize, out int totalCount) { }</span></span> |

### <a name="next-step"></a><span data-ttu-id="e2139-179">後續步驟</span><span class="sxs-lookup"><span data-stu-id="e2139-179">Next Step</span></span>

<span data-ttu-id="e2139-180">現在讓我們看看如何將驗證和授權支援新增至我們的應用程式。</span><span class="sxs-lookup"><span data-stu-id="e2139-180">Let's now look at how we can add authentication and authorization support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e2139-181">[上一頁](re-use-ui-using-master-pages-and-partials.md)
> [下一頁](secure-applications-using-authentication-and-authorization.md)</span><span class="sxs-lookup"><span data-stu-id="e2139-181">[Previous](re-use-ui-using-master-pages-and-partials.md)
[Next](secure-applications-using-authentication-and-authorization.md)</span></span>
