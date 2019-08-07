---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中使用 Entity Framework 新增排序、篩選和分頁 |Microsoft Docs
author: tdykstra
description: 在本教學課程中, 您會將排序、篩選和分頁功能新增至**學生**的 [索引] 頁面。 您也會建立簡單的群組頁面。
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: f774732a3960fca079438a88a5472c37cf7be08a
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 08/06/2019
ms.locfileid: "68810761"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a>教學課程：在 ASP.NET MVC 應用程式中使用 Entity Framework 新增排序、篩選和分頁

在[上一個教學](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程中, 您已針對`Student`實體的基本 CRUD 作業實作為一組網頁。 在本教學課程中, 您會將排序、篩選和分頁功能新增至**學生**的 [索引] 頁面。 您也會建立簡單的群組頁面。

下圖顯示當您完成時, 頁面看起來會是什麼樣子。 資料行標題是使用者可以按一下以依據該資料行排序的連結。 重覆按一下資料行標題，可切換遞增和遞減排序次序。

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

在本教學課程中，您已：

> [!div class="checklist"]
> * 新增資料行排序連結
> * 新增 [搜尋] 方塊
> * 新增分頁
> * 建立 [關於] 頁面

## <a name="prerequisites"></a>必要條件

* [實作基本的 CRUD 功能](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a>新增資料行排序連結

若要將排序新增至 [學生索引] 頁面, 您`Index`將變更`Student`控制器的方法, `Student`並將程式碼加入至索引視圖。

### <a name="add-sorting-functionality-to-the-index-method"></a>將排序功能加入至 Index 方法

- 在*Controllers\StudentController.cs*中, 將`Index`方法取代為下列程式碼:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

此程式碼會從 URL 中的查詢字串接收 `sortOrder` 參數。 查詢字串值是由 ASP.NET MVC 當做動作方法的參數來提供。 參數是一個字串, 其為 "Name" 或 "Date", 可選擇性地後面接著底線和字串 "desc", 以指定遞減順序。 預設的排序次序為遞增。

第一次要求 [索引] 頁面時，沒有任何查詢字串。 學生會依`LastName`遞增順序顯示, 這是在`switch`語句中由「範圍外」案例所建立的預設值。 使用者按一下資料行標題超連結時，適當的 `sortOrder` 值將會在查詢字串值中提供。

系統會`ViewBag`使用這兩個變數, 讓此視圖可以使用適當的查詢字串值來設定資料行標題超連結:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

這些是三元陳述式。 第一個指定`sortOrder`參數為 null 或空白時, `ViewBag.NameSortParm`應該設定為 "name\_desc"; 否則, 應該將它設定為空字串。 這兩個陳述式讓檢視能夠設定資料行標題超連結，如下所示：

| 目前排序次序 | 姓氏超連結 | 日期超連結 |
| --- | --- | --- |
| 姓氏遞增 | descending | ascending |
| 姓氏遞減 | ascending | ascending |
| 日期遞增 | ascending | descending |
| 日期遞減 | ascending | ascending |

方法會使用[LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)來指定要排序依據的資料行。 此<xref:System.Linq.IQueryable%601>程式碼會在`switch` `switch`語句之前建立變數、在`switch`語句中修改它, 並在`ToList`語句之後呼叫方法。 當您建立和修改 `IQueryable` 變數時，沒有查詢會傳送至資料庫。 直到您藉由呼叫方法 (例如) `IQueryable` `ToList`將物件轉換為集合時, 才會執行查詢。 因此, 此程式碼會產生在`return View`語句之前不會執行的單一查詢。

除了針對每個排序次序撰寫不同 LINQ 語句以外, 您還可以動態建立 LINQ 語句。 如需動態 LINQ 的詳細資訊, 請參閱[動態 linq](https://go.microsoft.com/fwlink/?LinkID=323957)。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>將資料行標題超連結新增至學生索引視圖

1. 在*Views\Student\Index.cshtml*中, 以`<tr>`反`<th>`白顯示的程式碼取代標題資料列的和元素:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   這段程式碼會使用`ViewBag`屬性中的資訊, 以適當的查詢字串值來設定超連結。

2. 執行頁面, 然後按一下 [**姓氏**] 和 [**註冊日期] 資料**行標題, 確認排序是否有效。

   當您按一下 [**姓氏**] 標題之後, 學生就會以遞減的姓氏順序顯示。

## <a name="add-a-search-box"></a>新增 [搜尋] 方塊

若要將篩選加入至學生的 [索引] 頁面, 您要將文字方塊和 [提交] 按鈕新增至視圖, 並在`Index`方法中進行對應的變更。 文字方塊可讓您輸入要在 [名字] 和 [姓氏] 欄位中搜尋的字串。

### <a name="add-filtering-functionality-to-the-index-method"></a>將篩選功能新增至 Index 方法

- 在*Controllers\StudentController.cs*中, 將`Index`方法取代為下列程式碼 (變更會反白顯示):

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

程式碼會將`searchString`參數新增`Index`至方法。 從將新增至 [索引] 檢視的文字方塊中接收搜尋字串值。 它也會將`where`子句新增至 LINQ 語句, 而這只會選取姓氏或名字包含搜尋字串的學生。 只有在有要搜尋<xref:System.Linq.Queryable.Where%2A>的值時, 才會執行加入子句的語句。

> [!NOTE]
> 在許多情況下, 您可以在 Entity Framework 的實體集上呼叫相同的方法, 或在記憶體中的集合上, 以擴充方法的方式呼叫。 結果通常都相同, 但在某些情況下可能會不同。
>
> 例如, 當您將空字串傳遞`Contains`給它時, 方法的 .NET Framework 執行會傳回所有資料列, 但 SQL Server Compact 4.0 的 Entity Framework 提供者會針對空字串傳回零個數據列。 因此, 範例中的程式碼 (將`Where`語句放在`if`語句內) 可確保您取得所有 SQL Server 版本的相同結果。 此外, 根據預設, `Contains`方法的 .NET Framework 實值會執行區分大小寫的比較, 但 Entity Framework SQL Server 提供者預設會執行不區分大小寫的比較。 因此, 呼叫`ToUpper`方法使測試明確不區分大小寫, 可確保當您稍後變更程式`IEnumerable`代碼以使用存放庫時, 不會變更結果, 這會傳回集合, 而不`IQueryable`是物件。 (當您在 `IEnumerable` 集合上呼叫 `Contains` 方法時，將取得 .NET Framework 實作；當您在 `IQueryable` 物件上呼叫它時，則會取得資料庫提供者實作。)
>
> 對於不同的資料庫提供者, 或當您使用`IQueryable` `IEnumerable`集合時, 如果您使用的物件與相同, 則 Null 處理可能也會不同。 例如, 在某些情況下, `Where` `table.Column != 0`之類的條件可能不會傳回具有`null`做為值的資料行。 根據預設, EF 會產生額外的 SQL 運算子, 使 null 值能夠在資料庫中運作, 如同它在記憶體中運作一樣, 但是您可以在 EF6 中設定[UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics)旗標, 或在 EF Core 中呼叫[UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls)方法設定此行為。

### <a name="add-a-search-box-to-the-student-index-view"></a>將搜尋方塊新增至學生的 [索引] 視圖

1. 在*Views\Student\Index.cshtml*中, 將反白顯示的程式碼`table`緊接在開頭標記的前面, 以便建立標題、文字方塊和**搜尋**按鈕。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. 執行頁面, 輸入搜尋字串, 然後按一下 [**搜尋**] 以確認篩選正在運作。

   請注意, URL 不包含 "a" 搜尋字串, 這表示如果您將此頁面加入書簽, 則當您使用書簽時, 將不會取得篩選過的清單。 這也適用于資料行排序連結, 因為它們會排序整個清單。 稍後在本教學課程中, 您將變更 [**搜尋**] 按鈕, 以使用篩選準則的查詢字串。

## <a name="add-paging"></a>新增分頁

若要將分頁新增至學生的 [索引] 頁面, 您必須先安裝**PagedList** NuGet 套件。 然後您會在`Index`方法中進行其他變更, 並將分頁連結新增至此`Index`視圖。 **PagedList**是許多適用于 ASP.NET Mvc 的良好分頁和排序套件, 其用途僅為範例, 而不是其他選項的建議。

### <a name="install-the-pagedlistmvc-nuget-package"></a>安裝 PagedList NuGet 套件

NuGet **PagedList**會自動將**PagedList**套件安裝為相依性。 **PagedList**套件會安裝`PagedList` `IQueryable`和`IEnumerable`集合的集合類型和擴充方法。 `PagedList`擴充方法會在`IQueryable`或`IEnumerable`的集合中建立單一頁面的資料, 而集合則`PagedList`提供數個可協助分頁的屬性和方法。 **PagedList**會安裝頁面協助程式, 以顯示分頁按鈕。

1. 從 [**工具**] 功能表中, 依序選取 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。

2. 在 [**套件管理員主控台**] 視窗中, 確定 [**套件來源**] 是**nuget.org** , 而 [**預設專案**] 是 [ **ContosoUniversity**], 然後輸入下列命令:

   ```text
   Install-Package PagedList.Mvc
   ```

3. 建置專案。

### <a name="add-paging-functionality-to-the-index-method"></a>將分頁功能新增至 Index 方法

1. 在*Controllers\StudentController.cs*中, 為`using` `PagedList`命名空間新增語句:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. 以下列程式碼取代 `Index` 方法：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   此程式碼會`page`將參數、目前的排序次序參數, 以及目前的篩選參數新增至方法簽章:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   第一次顯示頁面, 或使用者未按一下分頁或排序連結時, 所有參數都是 null。 如果按一下分頁連結, `page`變數會包含要顯示的頁碼。

   `ViewBag`屬性會提供具有目前排序次序的視圖, 因為這必須包含在分頁連結中, 以便在分頁時保持相同的排序次序:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   另一個屬性`ViewBag.CurrentFilter`() 會提供具有目前篩選字串的視圖。 此值必須包含在分頁連結中，才能維護分頁期間的篩選設定，而且它必須在頁面重新顯示時還原為文字方塊。 如果搜尋字串在分頁期間變更，頁面必須重設為 1，因為新的篩選可能會導致顯示不同的資料。 當您在文字方塊中輸入值, 並按下 [提交] 按鈕時, 就會變更搜尋字串。 在此情況下, `searchString`參數不是 null。

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   在方法的結尾, 學生`ToPagedList` `IQueryable`物件上的擴充方法會將 student 查詢轉換成支援分頁的集合類型中的一頁學生。 這一頁的學生接著會傳遞至視圖:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   `ToPagedList` 方法會採用頁面數。 這兩個問號代表[null 聯合運算子](/dotnet/csharp/language-reference/operators/null-coalescing-operator)。 Null 聯合運算子將針對可為 Null 的型別定義預設值；`(page ?? 1)` 運算式表示在它含有值時會傳回值 `page`，或在 `page` 為 null 時傳回 1。

### <a name="add-paging-links-to-the-student-index-view"></a>將分頁連結新增至學生索引視圖

1. 在*Views\Student\Index.cshtml*中, 將現有的程式碼取代為下列程式碼。 所做的變更已醒目標示。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   頁面頂端的 `@model` 陳述式指定檢視現在會取得 `PagedList` 物件，而不是 `List` 物件。

   `using` 的`PagedList.Mvc`語句會提供對分頁按鈕之 MVC helper 的存取權。

   程式碼會使用[html.beginform](/previous-versions/aspnet/dd492719(v=vs.108))的多載, 以允許它指定[FormMethod。 Get](/previous-versions/aspnet/dd460179(v=vs.100))。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   預設[html.beginform](/previous-versions/aspnet/dd492719(v=vs.108))會以 POST 提交表單資料, 這表示參數會傳遞至 HTTP 訊息內文, 而不會在 URL 中作為查詢字串。 當您指定 HTTP GET 時，表單資料會以 URL 中作為查詢字串傳遞，這可讓使用者為該 URL 加上書籤。 [使用 HTTP get 的 W3C 指導方針](http://www.w3.org/2001/tag/doc/whenToUseGet.html)建議您在動作不會產生更新時使用 get。

   文字方塊會使用目前的搜尋字串進行初始化, 因此當您按一下新的頁面時, 您可以看到目前的搜尋字串。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   資料行標頭連結會使用查詢字串，將目前的搜尋字串傳遞至控制器，讓使用者可以在篩選結果內排序：

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   會顯示目前的頁面和總頁數。

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   如果沒有可顯示的頁面, 則會顯示「頁面0為0」。 (在此情況下, 頁碼大於頁面計數, 因為`Model.PageNumber`是 1, 而`Model.PageCount`是 0)。

   `PagedListPager` Helper 會顯示分頁按鈕:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   `PagedListPager` Helper 提供一些您可以自訂的選項, 包括 url 和樣式。 如需詳細資訊, 請參閱 GitHub 網站上的[TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 。

2. 執行頁面。

   以不同排序次序按一下分頁連結，以確定分頁運作正常。 然後輸入搜尋字串並再次嘗試分頁，以確認分頁的排序和篩選能正確運作。

## <a name="create-an-about-page"></a>建立 [關於] 頁面

針對 Contoso 大學網站的 [關於] 頁面, 您將會顯示已註冊每個註冊日期的學生人數。 這需要對群組進行分組和簡單計算。 若要完成此工作，您需要執行下列作業：

- 針對您需要傳遞至檢視的資料，建立檢視模型類別。
- 修改`About` 控制器`Home`中的方法。
- `About`修改 view。

### <a name="create-the-view-model"></a>建立視圖模型

在專案資料夾中建立*viewmodel*資料夾。 在該資料夾中, 新增類別檔案*EnrollmentDateGroup.cs* , 並將範本程式碼取代為下列程式碼:

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>修改 Home 控制器

1. 在*HomeController.cs*中, 將下列`using`語句新增至檔案頂端:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. 在類別的左大括弧之後, 立即新增資料庫內容的類別變數:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. 以下列程式碼取代 `About` 方法：

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   LINQ 陳述式會依註冊日期將學生實體組成群組、計算每個群組中的實體數目、將結果儲存在 `EnrollmentDateGroup` 檢視模型物件的集合中。

4. `Dispose`新增方法:

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>修改 About 檢視

1. 將*Views\Home\About.cshtml*檔案中的程式碼取代為下列程式碼:

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. 執行應用程式, 然後按一下 [**關於**] 連結。

   每個註冊日期的學生計數會顯示在表格中。

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 新增資料行排序連結
> * 新增 [搜尋] 方塊
> * 新增分頁
> * 建立 [關於] 頁面

前往下一篇文章, 以瞭解如何使用連線恢復功能和命令攔截。
> [!div class="nextstepaction"]
> [連接恢復功能和命令攔截](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
