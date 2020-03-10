---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: 簡介 ASP.NET Web Pages-更新資料庫資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程說明當您使用 ASP.NET Web Pages （Razor）時，如何更新（變更）現有的資料庫專案。 它假設您已完成第一系列 。
ms.author: riande
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 8f8bcfb7d9d2416a2699776cadbdaae8e12415ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574225"
---
# <a name="introducing-aspnet-web-pages---updating-database-data"></a>簡介 ASP.NET Web Pages-更新資料庫資料

由[Tom FitzMacken](https://github.com/tfitzmac)

> 本教學課程說明當您使用 ASP.NET Web Pages （Razor）時，如何更新（變更）現有的資料庫專案。 它假設您已使用[ASP.NET Web Pages 的表單，透過輸入資料來](entering-data.md)完成數列。
> 
> 您將學到什麼：
> 
> - 如何在 `WebGrid` helper 中選取個別記錄。
> - 如何從資料庫讀取單一記錄。
> - 如何使用資料庫記錄中的值預先載入表單。
> - 如何更新資料庫中的現有記錄。
> - 如何將資訊儲存在頁面中，而不顯示它。
> - 如何使用隱藏欄位來儲存資訊。
>   
> 
> 討論的功能/技術：
> 
> - `WebGrid` helper。
> - SQL `Update` 命令。
> - `Database.Execute` 方法
> - 隱藏欄位（`<input type="hidden">`）。

## <a name="what-youll-build"></a>您要建置的內容

在上一個教學課程中，您已瞭解如何將記錄新增至資料庫。 在此，您將瞭解如何顯示要編輯的記錄。 在 [*電影*] 頁面中，您將更新 `WebGrid` 協助程式，使其顯示每個電影旁的 [**編輯**] 連結：

![WebGrid 顯示包含每個電影的 [編輯] 連結](updating-data/_static/image1.png)

當您按一下 [**編輯**] 連結時，它會帶您前往不同的頁面，其中電影資訊已經是表單：

![編輯電影頁面，顯示要編輯的電影](updating-data/_static/image2.png)

您可以變更任何值。 當您提交變更時，頁面中的程式碼會更新資料庫，並帶您回到電影清單。

此程式的運作方式幾乎與您在上一個教學課程中建立的*AddMovie*相同，因此本教學課程中大部分的功能都很熟悉。

有數種方式可讓您執行編輯個別電影的方式。 已選擇所顯示的方法，因為它很容易執行且易於瞭解。

## <a name="adding-an-edit-link-to-the-movie-listing"></a>新增電影清單的編輯連結

首先，您將更新 [*電影*] 頁面，讓每個電影清單也包含一個 [**編輯**] 連結。

開啟 [*電影*] 檔案。

在頁面主體中，藉由新增資料行來變更 `WebGrid` 標記。 以下是修改過的標記：

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

新的資料行是這一項：

[!code-html[Main](updating-data/samples/sample2.html)]

此資料行的重點是要顯示其文字顯示為「編輯」的連結（`<a>` 元素）。 接下來我們要建立一個在頁面執行時看起來像下面的連結，每個電影的 `id` 值都不同：

[!code-css[Main](updating-data/samples/sample3.css)]

此連結將會叫用名為*EditMovie*的頁面，並將查詢字串傳遞 `?id=7` 至該頁面。

新資料行的語法看起來可能有點複雜，但這只是因為它會將數個元素放在一起。 每個個別元素都很簡單。 如果您只專注于 `<a>` 專案，您會看到此標記：

[!code-html[Main](updating-data/samples/sample4.html)]

格線運作方式的一些背景：格線會顯示資料列（每個資料庫記錄一個），並顯示資料庫記錄中每個欄位的資料行。 當每個方格資料列都在進行結構化時，`item` 物件會包含該資料列的資料庫記錄（item）。 這種相片順序可讓您在程式碼中取得該資料列的資料。 這就是您在這裡看到的內容：運算式 `item.ID` 取得目前資料庫專案的識別碼值。 您可以使用 `item.Title`、`item.Genre`或 `item.Year`，以相同的方式取得任何資料庫值（[標題]、[內容類型] 或 [年份]）。

運算式 `"~/EditMovie?id=@item.ID` 結合了目標 URL 的硬式編碼部分（`~/EditMovie?id=`）與這個動態衍生的識別碼。 （您在上一個教學課程中看到了 `~` 運算子，它是代表目前網站根目錄的 ASP.NET 運算子）。

結果是，資料行中標記的這個部分只會在執行時間產生類似下列的標記：

[!code-xml[Main](updating-data/samples/sample5.xml)]

當然，每個資料列的實際 `id` 值都是不同的。

## <a name="creating-a-custom-display-for-a-grid-column"></a>建立格線資料行的自訂顯示

現在回到方格資料行。 您原先在方格中擁有的三個數據行只會顯示資料值（[標題]、[內容類型] 和 [年份]）。 您藉由傳遞資料庫資料行的名稱來指定此顯示 &mdash; 例如，`grid.Column("Title")`。

這個新的 [**編輯**連結] 資料行不同。 您不需要指定資料行名稱，而是傳遞 `format` 參數。 這個參數可讓您定義 `WebGrid` helper 將轉譯的標記，以及 `item` 值，以粗體或綠色或您想要的任何格式來顯示資料行資料。 例如，如果您希望標題以粗體顯示，您可以建立如下列範例所示的資料行：

[!code-html[Main](updating-data/samples/sample6.html)]

（您在 `format` 屬性中看到的各種 `@` 字元會標示標記和程式碼值之間的轉換）。

一旦知道 `format` 屬性之後，就能更輕鬆地瞭解新的 [**編輯**連結] 資料行如何放在一起：

[!code-html[Main](updating-data/samples/sample7.html)]

此資料行*只*包含轉譯連結的標記，加上從資料列的資料庫記錄中解壓縮的部分資訊（識別碼）。

> [!TIP]
> 
> **方法的具名引數和位置參數**
> 
> 許多時候，當您呼叫方法並將參數傳遞給它時，就只會列出以逗號分隔的參數值。 以下提供幾個範例：
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> 當您第一次看到此程式碼時，我們並未提過這個問題，但在每個案例中，您會以特定順序將參數傳遞給方法 &mdash; 也就是在該方法中定義參數的順序。 針對 `db.Execute` 和 `Validation.RequireFields`，如果您要將傳遞值的順序混合，則會在頁面執行時收到錯誤訊息，或至少有一些奇怪的結果。 很明顯地，您必須知道要在中傳遞參數的順序。 （在 WebMatrix 中，IntelliSense 可協助您瞭解參數的名稱、類型和順序）。
> 
> 除了依序傳遞值以外，您還可以使用*具名引數*。 （傳遞參數的順序稱為「使用*位置參數*」）。針對具名引數，您會在傳遞值時明確包含參數的名稱。 在這些教學課程中，您已使用具名引數已經有數次。 例如:
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> 和
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> 在幾種情況下，具名引數很方便，尤其是當方法接受許多參數時。 其中一個是當您只想要傳遞一或兩個參數，但您要傳遞的值不在參數清單中的第一個位置時。 另一種情況是，您想要以對您而言最有意義的順序傳遞參數，讓程式碼更容易閱讀。
> 
> 很明顯地，若要使用具名引數，您必須知道參數的名稱。 WebMatrix IntelliSense 可以*顯示*名稱，但目前無法為您填入。

## <a name="creating-the-edit-page"></a>建立 [編輯] 頁面

現在您可以建立 [ *EditMovie* ] 頁面。 當使用者按一下 [**編輯**] 連結時，將會在此頁面上結束。

建立名為*EditMovie*的頁面，並以下列標記取代檔案中的內容：

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

此標記和程式碼類似于您在 [ *AddMovie* ] 頁面中的內容。 [提交] 按鈕的文字有些微差異。 如同*AddMovie*頁面，有一個 `Html.ValidationSummary` 呼叫會顯示驗證錯誤（如果有的話）。 這次我們會離開 `Validation.Message`的呼叫，因為驗證摘要中會顯示錯誤。 如先前的教學課程所述，您可以使用各種組合中的驗證摘要和個別錯誤訊息。

請注意，`<form>` 元素的 `method` 屬性設定為 `post`。 就像*AddMovie*的頁面一樣，此頁面會對資料庫進行變更。 因此，此表單應執行 `POST` 作業。 （如需 `GET` 和 `POST` 作業之間差異的詳細資訊，請參閱 HTML 表單教學課程中的[GET、POST 和 HTTP Verb 安全](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety)提要欄位）。

如您在先前的教學課程中所見，文字方塊的 `value` 屬性會使用 Razor 程式碼進行設定，以便預先載入。 不過，這次您使用的是該工作的 `title` 和 `genre` 之類的變數，而不是 `Request.Form["title"]`：

`<input type="text" name="title" value="@title" />`

就像之前一樣，此標記會預先載入具有電影值的文字方塊值。 您很快就會看到使用變數的時機，而不是使用 `Request` 物件。

此頁面上也有一個 `<input type="hidden">` 元素。 此元素會儲存電影識別碼，而不會顯示在頁面上。 識別碼一開始會使用查詢字串值（`?id=7` 或類似于 URL）傳遞至頁面。 藉由將識別碼值放入隱藏的欄位中，您可以在提交表單時確保其可供使用，即使您已無法再存取此頁面所叫用的原始 URL 也一樣。

不同于*AddMovie*頁面， *EditMovie*頁面的程式碼有兩個不同的功能。 第一個函式是當第一次顯示頁面時（*只有*then），程式碼會從查詢字串取得電影識別碼。 然後，程式碼會使用識別碼來讀取資料庫中的對應電影，並在文字方塊中顯示（預先載入）它。

第二個函式是當使用者按一下 [**提交變更**] 按鈕時，程式碼必須讀取文字方塊的值並加以驗證。 程式碼也必須使用新的值來更新資料庫專案。 這項技術類似于新增記錄，如您在*AddMovie*中所見。

## <a name="adding-code-to-read-a-single-movie"></a>新增程式碼以讀取單一電影

若要執行第一個函式，請將下列程式碼新增至頁面頂端：

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

大部分的程式碼都位於啟動 `if(!IsPost)`的區塊中。 `!` 運算子表示「不」，因此運算式表示*此要求不是 post 提交*，這是一種間接的方式，指出此*要求是否為第一次執行此頁面*。 如先前所述，此程式碼應該*只*會在頁面第一次執行時執行。 如果您未將程式碼括在 `if(!IsPost)`中，它會在每次叫用頁面時執行，不論是第一次還是回應按鈕的按一下。

請注意，此程式碼包含這次的 `else` 區塊。 就像我們在介紹 `if` 區塊時所說的，有時候您會想要在測試的條件不成立時執行替代程式碼。 這就是這種情況。 如果條件通過（亦即，如果傳遞至頁面的識別碼是 ok），您就會從資料庫讀取資料列。 不過，如果條件未通過，則會執行 `else` 區塊，而程式碼會設定錯誤訊息。

## <a name="validating-a-value-passed-to-the-page"></a>驗證傳遞至頁面的值

程式碼會使用 `Request.QueryString["id"]` 來取得傳遞至頁面的識別碼。 此程式碼可確保已實際傳遞識別碼的值。 如果未傳遞任何值，則程式碼會設定驗證錯誤。

此程式碼會顯示驗證資訊的不同方式。 在上一個教學課程中，您已與 `Validation` 協助程式合作。 您已註冊要驗證的欄位，而 ASP.NET 會使用 `Html.ValidationMessage` 和 `Html.ValidationSummary`，自動執行驗證和顯示錯誤。 不過，在此情況下，您實際上不是驗證使用者輸入。 相反地，您要驗證從別處傳遞至頁面的值。 `Validation` helper 不會為您執行此動作。

因此，您可以自行檢查值，方法是使用 `if(!Request.QueryString["ID"].IsEmpty()`進行測試）。 如果發生問題，您可以使用 `Html.ValidationSummary`來顯示錯誤，如同您在 `Validation` 協助程式中所做的一樣。 若要這麼做，請呼叫 `Validation.AddFormError`，並將要顯示的訊息傳遞給它。 `Validation.AddFormError` 是內建的方法，可讓您定義與您已熟悉的驗證系統結合的自訂訊息。 （稍後在本教學課程中，我們將討論如何讓此驗證程式更健全）。

確定影片的識別碼之後，程式碼會讀取資料庫，只尋找單一資料庫專案。 （您可能已注意到資料庫作業的一般模式：開啟資料庫、定義 SQL 語句，然後執行語句）。這次，SQL `Select` 語句包括 `WHERE ID = @0`。 因為識別碼是唯一的，所以只會傳回一筆記錄。

查詢是使用 `db.QuerySingle` （不是 `db.Query`，如同您用於電影清單的）來執行，而程式碼則會將結果放入 `row` 變數中。 `row` 的名稱是任意的;您可以將變數命名為任何您喜歡的名稱。 然後，在頂端初始化的變數會填入電影詳細資料，讓這些值可以顯示在文字方塊中。

## <a name="testing-the-edit-page-so-far"></a>測試編輯頁面（到目前為止）

如果您想要測試您的頁面，請立即執行 [*電影*] 頁面，然後按一下任何電影旁的 [**編輯**] 連結。 您會看到 [ *EditMovie* ] 頁面中已填入您所選電影的詳細資料：

![編輯電影頁面，顯示要編輯的電影](updating-data/_static/image3.png)

請注意，頁面的 URL 包含類似 `?id=10` （或其他數位）的內容。 到目前為止，您已測試*電影*頁面中的**編輯**連結是否正常運作、您的頁面正在從查詢字串讀取識別碼，以及取得單一電影記錄的資料庫查詢正在運作。

您可以變更電影資訊，但當您按一下 [**提交變更**] 時，不會發生任何事。

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a>新增程式碼以使用使用者的變更來更新電影

在*EditMovie*檔中，若要執行第二個函式（儲存變更），請將下列程式碼新增至 `@` 區塊的右大括弧內。 （如果您不確定程式碼的確切位置，可以查看本教學課程結尾處[的 [編輯電影] 頁面的完整程式代碼清單](#Complete_Page_Listing_for_EditMovie)。）

[!code-csharp[Main](updating-data/samples/sample12.cs)]

同樣地，此標記和程式碼與*AddMovie*中的程式碼類似。 這段程式碼是在 `if(IsPost)` 區塊中，因為只有在使用者按一下 [**提交變更**] 按鈕時，才會執行此程式碼 &mdash; 也就是在張貼表單時。 在此情況下，您不會使用類似 `if(IsPost && Validation.IsValid())`的測試，也就是說，您不會使用和來結合這兩個測試。 在此頁面中，您會先判斷是否有提交表單（`if(IsPost)`），然後才註冊欄位進行驗證。 然後，您可以測試驗證結果（`if(Validation.IsValid()`）。 流程與 [ *AddMovie* ] 頁面中稍有不同，但效果相同。

您可以使用其他 `<input>` 元素的 `Request.Form["title"]` 和類似的程式碼，來取得文字方塊的值。 請注意，這次程式碼會從隱藏欄位（`<input type="hidden">`）取得電影識別碼。 當頁面第一次執行時，程式碼會從查詢字串中獲得識別碼。 您會從隱藏欄位取得值，以確定您取得原先顯示的電影識別碼，以防查詢字串在那之後發生某種程度的改變。

*AddMovie*程式碼與此程式碼之間的重要差異在於，在此程式碼中，您會使用 SQL `Update` 語句，而不是 `Insert Into` 語句。 下列範例顯示 SQL `Update` 語句的語法：

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

您可以依任何順序指定任何資料行，而不一定要在 `Update` 作業期間更新每個資料行。 （您無法更新識別碼本身，因為這會生效地將記錄儲存為新記錄，而且不允許 `Update` 作業）。

> [!NOTE] 
> 
> **重要事項**具有識別碼的 `Where` 子句非常重要，因為這就是資料庫知道您要更新的資料庫記錄的方式。 如果您離開 `Where` 子句，資料庫將會更新資料庫中的*每一*筆記錄。 在大部分情況下，這會造成嚴重損壞。

在程式碼中，要更新的值會使用預留位置傳遞至 SQL 語句。 若要重複前面說過的內容：基於安全性考慮，請*只*使用預留位置將值傳遞給 SQL 語句。

在程式碼使用 `db.Execute` 執行 `Update` 語句之後，它會重新導向回 [清單] 頁面，您可以在其中查看變更。

> [!TIP] 
> 
> **不同的 SQL 語句，不同的方法**
> 
> 您可能已經注意到，您會使用稍微不同的方法來執行不同的 SQL 語句。 若要執行可能會傳回多筆記錄的 `Select` 查詢，您可以使用 `Query` 方法。 若要執行您知道只會傳回一個資料庫專案的 `Select` 查詢，請使用 `QuerySingle` 方法。 若要執行進行變更但不會傳回資料庫專案的命令，您可以使用 `Execute` 方法。
> 
> 您必須有不同的方法，因為它們會傳回不同的結果，如同您已在 `Query` 和 `QuerySingle`之間的差異中所見。 （`Execute` 方法實際上會傳回值，&mdash; 也就是受 &mdash; 命令影響的資料庫資料列數目，但是您目前已忽略這種情況）。
> 
> 當然，`Query` 方法可能只會傳回一個資料庫資料列。 不過，ASP.NET 一律會將 `Query` 方法的結果視為集合。 即使此方法只會傳回一個資料列，您還是必須從集合中將該單一資料列解壓縮。 因此，在您*知道*您只會得到一個資料列的情況下，使用 `QuerySingle`會比較方便。
> 
> 還有一些其他方法可執行特定類型的資料庫作業。 您可以在[ASP.NET WEB PAGES API 快速參考](../../api-reference/asp-net-web-pages-api-reference.md#Data)中找到資料庫方法的清單。

## <a name="making-validation-for-the-id-more-robust"></a>讓識別碼的驗證更健全

第一次執行頁面時，您會從查詢字串取得電影識別碼，以便從資料庫取得該電影。 您確定確實有一個要尋找的值，也就是使用下列程式碼：

[!code-csharp[Main](updating-data/samples/sample13.cs)]

您已使用此程式碼來確定如果使用者到達*EditMovies*頁面，而未先在*電影*頁面中選取電影，則頁面會顯示使用者易記的錯誤訊息。 （否則，使用者會看到一項錯誤，可能只會讓他們感到困惑）。

不過，這種驗證並不穩定。 此頁面可能也會因下列錯誤而叫用：

- 識別碼不是數位。 例如，您可以使用 `http://localhost:nnnnn/EditMovie?id=abc`之類的 URL 叫用此頁面。
- 識別碼是數位，但它會參考不存在的電影（例如 `http://localhost:nnnnn/EditMovie?id=100934`）。

如果您想要查看這些 Url 所產生的錯誤，請執行 [*電影*] 頁面。 選取要編輯的電影，然後將 [ *EditMovie* ] 頁面的 url 變更為包含字母識別碼的 url，或不存在電影的識別碼。

那麼，您該怎麼做呢？ 第一次修正是要確保不只是傳遞至頁面的識別碼，而是識別碼是整數。 變更 `!IsPost` 測試的程式碼，使其看起來如下列範例所示：

[!code-csharp[Main](updating-data/samples/sample14.cs)]

您已將第二個條件新增至 `IsEmpty` 測試，並連結 `&&` （邏輯 AND）：

[!code-csharp[Main](updating-data/samples/sample15.cs)]

您可能會記得[ASP.NET Web Pages 程式設計](../introducing-razor-syntax-c.md)教學課程的簡介，這類方法 `AsBool` `AsInt` 將字元字串轉換成其他資料類型。 `IsInt` 方法（和其他，如 `IsBool` 和 `IsDateTime`）類似。 不過，它們只會測試您是否*可以*轉換字串，而不會實際執行轉換。 在這裡，您基本上會說*查詢字串值是否可以轉換成整數 ...* 。

另一個可能的問題是尋找不存在的電影。 取得電影的程式碼看起來像下面這段程式碼：

[!code-csharp[Main](updating-data/samples/sample16.cs)]

如果您將 `movieId` 值傳遞給未對應至實際電影的 `QuerySingle` 方法，則不會傳回任何內容，且後面的語句（例如，`title=row.Title`）會導致錯誤。

同樣地，有一個簡單的修正方法。 如果 `db.QuerySingle` 方法未傳回任何結果，則 `row` 變數會是 null。 因此，您可以先檢查 `row` 變數是否為 null，然後再嘗試從中取得值。 下列程式碼會在從 `row` 物件取得值的語句周圍加入 `if` 區塊：

[!code-csharp[Main](updating-data/samples/sample17.cs)]

使用這兩個額外的驗證測試，頁面會變得更具專案符號。 `!IsPost` 分支的完整程式碼現在看起來如下列範例所示：

[!code-csharp[Main](updating-data/samples/sample18.cs)]

我們會特別注意，這項工作是 `else` 組塊的好用。 如果測試未通過，`else` 會封鎖設定錯誤訊息。

## <a name="adding-a-link-to-return-to-the-movies-page"></a>新增連結以返回電影頁面

最後還有一個有用的詳細資料，就是將連結新增回 [*電影*] 頁面。 在一般事件流程中，使用者會從 [*電影*] 頁面開始，然後按一下 [**編輯**] 連結。 這會將它們帶入*EditMovie*頁面，他們可以在其中編輯電影，然後按一下按鈕。 在程式碼處理變更之後，它會重新導向回 [*電影*] 頁面。

但是：

- 使用者可能會決定不變更任何專案。
- 使用者可能已取得此頁面，而不需要先按一下 [*電影*] 頁面中的 [**編輯**] 連結。

不論是哪一種方式，您都想要讓它們能夠輕鬆地回到主要清單。 這是一個簡單的修正 &mdash; 在標記中的結尾 `</form>` 標記之後加入下列標記：

[!code-html[Main](updating-data/samples/sample19.html)]

此標記會針對您在別處看到的 `<a>` 元素使用相同的語法。 URL 包含 `~` 表示「網站的根目錄」。

## <a name="testing-the-movie-update-process"></a>測試電影更新程式

現在您可以測試。 執行 [*電影*] 頁面，然後按一下電影旁的 [**編輯**]。 當 [ *EditMovie* ] 頁面出現時，對電影進行變更，然後按一下 [**提交變更**]。 當電影清單出現時，請確定您的變更已顯示。

若要確認驗證是否正常運作，請針對另一個電影按一下 [**編輯**]。 當您進入 [ *EditMovie* ] 頁面時，請清除 [內容類型] 欄位（或 [**年份** **] 欄位，** 或兩者），然後嘗試提交您的變更。 您會看到一則錯誤，如您所預期：

![編輯顯示驗證錯誤的電影頁面](updating-data/_static/image4.png)

按一下 [**返回電影清單**] 連結，放棄您所做的變更並返回 [*電影*] 頁面。

## <a name="coming-up-next"></a>下一步

在下一個教學課程中，您將瞭解如何刪除電影記錄。

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a>電影頁面的完整清單（以編輯連結更新）

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a>[編輯電影] 頁面的完成頁面清單

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a>其他資源

- [使用 Razor 語法 ASP.NET Web 程式設計的簡介](../../getting-started/introducing-razor-syntax-c.md)
- W3Schools 網站上的[SQL UPDATE 語句](http://www.w3schools.com/sql/sql_update.asp)

> [!div class="step-by-step"]
> [上一頁](entering-data.md)
> [下一頁](deleting-data.md)
