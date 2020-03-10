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
# <a name="implement-efficient-data-paging"></a>實作有效率的資料分頁

由[Microsoft](https://github.com/microsoft)

[下載 PDF](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> 這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟8，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。
> 
> 步驟8顯示如何將分頁支援新增至我們的/Dinners URL，如此一來，不會一次顯示 Dinners 的數千個，而是一次只顯示10個即將推出的 Dinners，並讓使用者以 SEO 易記的方式，透過整個清單來翻頁或往後轉。
> 
> 如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。

## <a name="nerddinner-step-8-paging-support"></a>NerdDinner 步驟8：分頁支援

如果我們的網站成功，將會有數千個即將推出的 dinners。 我們必須確定我們的 UI 會進行調整以處理所有的 dinners，並允許使用者流覽。 若要啟用這項功能，我們會將分頁支援新增至我們的 */Dinners* URL，如此一來，就不會一次顯示 Dinners 的數千個，而是可讓使用者以 SEO 易懂的方式，在整個清單中翻頁並向前復原。

### <a name="index-action-method-recap"></a>Index （）動作方法的回顧

我們的 DinnersController 類別內的 Index （）動作方法目前如下所示：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample1.cs)]

對 */Dinners* URL 提出要求時，它會抓取所有即將推出的 Dinners 清單，然後再呈現所有的列出內容：

![](implement-efficient-data-paging/_static/image1.png)

### <a name="understanding-iqueryablelttgt"></a>瞭解 IQueryable&lt;T&gt;

*IQueryable&lt;t&gt;* 是以 LINQ 引進的介面，做為 .net 3.5 的一部分。 它提供強大的「延後執行」案例，可讓我們利用來實行分頁支援。

在我們的 DinnerRepository 中，我們會從 FindUpcomingDinners （）方法傳回 IQueryable&lt;晚餐&gt; 序列：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample2.cs)]

FindUpcomingDinners （）方法所傳回的 IQueryable&lt;晚餐&gt; 物件會封裝一個查詢，以使用 LINQ to SQL 從我們的資料庫中取出晚餐物件。 重要的是，它不會對資料庫執行查詢，直到我們嘗試存取/逐一查看查詢中的資料，或直到我們在其上呼叫 ToList （）方法為止。 呼叫我們的 FindUpcomingDinners （）方法的程式碼可選擇性地選擇在執行查詢之前，將額外的「連鎖」作業/篩選器新增至 IQueryable&lt;晚餐&gt; 物件。 LINQ to SQL 之後，就有足夠的智慧，可以在要求資料時，對資料庫執行合併的查詢。

若要執行分頁邏輯，我們可以更新 DinnersController 的 Index （）動作方法，以便在對其呼叫 ToList （）之前，將額外的 "Skip" 和 "Take" 運算子套用至傳回的 IQueryable&lt;晚餐&gt; 序列：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample3.cs)]

上述程式碼會略過資料庫中前10名即將推出的 dinners，然後傳回 20 dinners。 LINQ to SQL 非常聰明，可以用來建立優化的 SQL 查詢，以在 SQL 資料庫中執行此略過邏輯（而不是在 web 伺服器上）。 這表示即使在資料庫中有數百萬個即將推出的 Dinners，只會在此要求中抓取10個我們想要的部分（使其有效率且可調整）。

### <a name="adding-a-page-value-to-the-url"></a>將 "page" 值新增至 URL

我們不會將特定頁面範圍硬式編碼，而是要讓 Url 包含 "page" 參數，以指出使用者要求的晚餐範圍。

#### <a name="using-a-querystring-value"></a>使用 Querystring 值

下列程式碼示範如何更新索引（）動作方法，以支援 querystring 參數並啟用 Url，例如 */Dinners？ page = 2*：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample4.cs)]

上述 Index （）動作方法具有名為 "page" 的參數。 參數會宣告為可為 null 的整數（也就是 int？表示）。 這表示 */Dinners？ page = 2* URL 會導致 "2" 的值當做參數值傳遞。 */Dinners* URL （不含 querystring 值）會導致傳遞 null 值。

我們會將頁面值乘以頁面大小（在此案例中為10個數據列），以判斷要略過多少 dinners。 我們使用[ C# null 「聯合」運算子（？）](https://weblogs.asp.net/scottgu/archive/2007/09/20/the-new-c-null-coalescing-operator-and-using-it-with-linq.aspx) ，這在處理可為 null 的類型時非常有用。 上述程式碼會在頁面參數為 null 時，將值指派為0。

#### <a name="using-embedded-url-values"></a>使用內嵌的 URL 值

使用 querystring 值的替代方法是在實際 URL 本身內內嵌 page 參數。 例如： */Dinners/Page/2*或 */Dinners/2*。 ASP.NET MVC 包含強大的 URL 路由引擎，可讓您輕鬆地支援這類案例。

我們可以註冊自訂路由規則，將任何傳入 URL 或 URL 格式對應至我們想要的任何控制器類別或動作方法。 我們只需要在專案中開啟 global.asax 檔案就可以了：

![](implement-efficient-data-paging/_static/image2.png)

然後使用 Maproute.html （） helper 方法（例如第一次呼叫路由）來註冊新的對應規則。Maproute.html （）如下：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample5.cs)]

在上述情況中，我們會註冊名為 "UpcomingDinners" 的新路由規則。 我們指出它的 URL 格式為 "Dinners/Page/{Page}"，其中 {Page} 是內嵌在 URL 內的參數值。 Maproute.html （）方法的第三個參數指出，我們應該將符合此格式的 Url 對應至 DinnersController 類別上的 Index （）動作方法。

我們可以在 Querystring 案例中使用與之前相同的索引（）程式碼，但現在我們的 "page" 參數會來自 URL，而不是 Querystring：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample6.cs)]

現在當我們執行應用程式並輸入 */Dinners*時，我們會看到前10個即將推出的 Dinners：

![](implement-efficient-data-paging/_static/image3.png)

當我們輸入 */Dinners/Page/1*時，我們會看到下一個 Dinners 頁面：

![](implement-efficient-data-paging/_static/image4.png)

### <a name="adding-page-navigation-ui"></a>新增頁面導覽 UI

完成分頁案例的最後一個步驟，是在我們的 view 範本內執行「下一步」和「上一頁」導覽 UI，讓使用者可以輕鬆地略過晚餐資料。

若要正確執行此功能，我們必須知道資料庫中的 Dinners 總數，以及此轉譯的資料頁數。 接著，我們需要計算目前要求的 "page" 值是否在資料的開頭或結尾，並據以顯示或隱藏 "previous" 和 "next" UI。 我們可以在 Index （）動作方法內執行此邏輯。 或者，我們可以將協助程式類別新增至我們的專案，以更重複使用的方式封裝此邏輯。

以下是一個簡單的 "PaginatedList" 協助程式類別，衍生自內建 .NET Framework 的清單&lt;T&gt; 集合類別。 它會執行可重複使用的集合類別，可用來將任何 IQueryable 資料的序列分頁。 在我們的 NerdDinner 應用程式中，我們會將它用於 IQueryable&lt;晚餐&gt; 結果，但它可以輕鬆地在其他應用程式案例中，用於 IQueryable&lt;產品&gt; 或 IQueryable&lt;客戶&gt; 結果：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample7.cs)]

請注意它的計算方式，然後公開屬性，例如 "PageIndex"、"PageSize"、"TotalCount" 和 "TotalPages"。 然後，它也會公開兩個 helper 屬性 "HasPreviousPage" 和 "HasNextPage"，指出集合中的資料頁是否位於原始序列的開頭或結尾。 上述程式碼會執行兩個 SQL 查詢，第一個是抓取晚餐物件總數的計數（這不會傳回物件，而是會執行可傳回整數的「選取計數」語句），而第二個則是只取得的資料列我們在資料庫中所需的資料，以取得目前的資料頁面。

然後，我們可以更新 DinnersController （）協助程式方法，從 DinnerRepository FindUpcomingDinners （）結果中建立 PaginatedList&lt;晚餐&gt;，並將它傳遞給我們的 view 範本：

[!code-csharp[Main](implement-efficient-data-paging/samples/sample8.cs)]

然後，我們可以更新 \Views\Dinners\Index.aspx view 範本，使其繼承自 ViewPage&lt;NerdDinner。 PaginatedList&lt;晚餐&gt;&gt;，而不是 ViewPage&lt;IEnumerable&lt;晚餐&gt;&gt;，然後將下列程式碼新增至我們的視圖範本底部，以顯示或隱藏下一個和上一個導覽 UI：

[!code-aspx[Main](implement-efficient-data-paging/samples/sample9.aspx)]

請注意，我們如何使用 RouteLink （） helper 方法來產生我們的超連結。 這個方法與我們先前使用的 .Html （） helper 方法類似。 其差異在於，我們會使用我們在 global.asax 檔案中設定的 "UpcomingDinners" 路由規則來產生 URL。 這可確保我們會產生 Url 給我們的 Index （）動作方法，其格式為： */Dinners/Page/{page}* –其中 {Page} 值是我們根據目前的 PageIndex 提供的變數。

現在當我們再次執行應用程式時，我們會在瀏覽器中一次看到10個 dinners：

![](implement-efficient-data-paging/_static/image5.png)

我們也在頁面底部有 &lt;&lt;&lt; 和 &gt;&gt;&gt; 流覽 UI，可讓我們使用搜尋引擎可存取的 Url 來略過資料的向前和向後：

![](implement-efficient-data-paging/_static/image6.png)

| **側邊主題：瞭解 IQueryable&lt;T&gt; 的含意** |
| --- |
| IQueryable&lt;T&gt; 是一項非常強大的功能，可啟用各種有趣的延後執行案例（例如分頁和以撰寫為基礎的查詢）。 如同所有強大的功能，您會想要小心使用它，並確定它不會被濫用。 請務必辨識，從您的存放庫傳回 IQueryable&lt;T&gt; 結果，可讓呼叫程式碼在連結的運算子方法上附加，並參與終極查詢執行。 如果您不想要提供呼叫程式碼這項功能，則應該傳回反向 IList&lt;T&gt; 或 IEnumerable&lt;T&gt; 結果，其中包含已執行之查詢的結果。 針對分頁案例，這會要求您將實際的資料分頁邏輯推送至所呼叫的存放庫方法。 在此案例中，我們可能會更新 FindUpcomingDinners （） finder 方法，使其具有傳回 PaginatedList 的簽章： PaginatedList&lt; 晚餐&gt; FindUpcomingDinners （int pageIndex，int pageSize） {} 或傳回 IList&lt;晚餐&gt;，並使用 "totalCount" out 參數來傳回 Dinners 的總計數： IList&lt;晚餐&gt; FindUpcomingDinners （int pageIndex，int pageSize，out int totalCount） {} |

### <a name="next-step"></a>後續步驟

現在讓我們看看如何將驗證和授權支援新增至我們的應用程式。

> [!div class="step-by-step"]
> [上一頁](re-use-ui-using-master-pages-and-partials.md)
> [下一頁](secure-applications-using-authentication-and-authorization.md)
