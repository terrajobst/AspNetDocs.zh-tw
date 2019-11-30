---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 在 ASP.NET MVC 應用程式中使用 Entity Framework 排序、篩選和分頁（3/10） |Microsoft Docs
author: tdykstra
description: Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio ... 來建立 ASP.NET MVC 4 應用程式。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 8af630e0-fffa-4110-9eca-c96e201b2724
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: b1ddb70805dcb07fb60eea895ff572c054bde5c6
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595228"
---
# <a name="sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application-3-of-10"></a>在 ASP.NET MVC 應用程式中使用 Entity Framework 排序、篩選和分頁（3/10）

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 Code First 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 如需教學課程系列的資訊，請參閱[本系列的第一個教學課程](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。 您可以從一開始就開始本教學課程系列，或[下載本章節的入門專案](building-the-ef5-mvc4-chapter-downloads.md)，並從這裡開始。
> 
> > [!NOTE] 
> > 
> > 如果您遇到無法解決的問題，請[下載完整的章節](building-the-ef5-mvc4-chapter-downloads.md)並嘗試重現您的問題。 您通常可以藉由比較您的程式碼與已完成的程式碼，來找出問題的解決方法。 如需瞭解一些常見錯誤以及如何解決問題，請參閱[錯誤和](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#errors)因應措施。

在上一個教學課程中，您已為 `Student` 實體的基本 CRUD 作業實作為一組網頁。 在本教學課程中，您會將排序、篩選和分頁功能新增至**學生**的 [索引] 頁面。 此外，還要建立將執行簡易群組的頁面。

下圖顯示當您完成時的頁面外觀。 資料行標題是使用者可以按一下以依據該資料行排序的連結。 重覆按一下資料行標題，可切換遞增和遞減排序次序。

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

## <a name="add-column-sort-links-to-the-students-index-page"></a>將資料行排序連結新增至 Students 的 [索引] 頁面

若要將排序新增至 [學生索引] 頁面，您將變更 `Student` 控制器的 `Index` 方法，並將程式碼新增至 `Student` 索引視圖。

### <a name="add-sorting-functionality-to-the-index-method"></a>將排序功能加入至 Index 方法

在*Controllers\StudentController.cs*中，以下列程式碼取代 `Index` 方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

此程式碼會從 URL 中的查詢字串接收 `sortOrder` 參數。 查詢字串值是由 ASP.NET MVC 當做動作方法的參數來提供。 該參數是 "Name" 或 "Date" 的字串，後面可選擇性地接著底線和字串 "desc" 來指定遞減順序。 預設的排序次序為遞增。

第一次要求 [索引] 頁面時，沒有任何查詢字串。 學生會依 `LastName`以遞增的順序顯示，這是由 `switch` 語句中的逐步執行案例所建立的預設值。 使用者按一下資料行標題超連結時，適當的 `sortOrder` 值將會在查詢字串值中提供。

系統會使用兩個 `ViewBag` 變數，讓此視圖可以使用適當的查詢字串值來設定資料行標題超連結：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

這些是三元陳述式。 第一個指定如果 `sortOrder` 參數為 null 或空白，`ViewBag.NameSortParm` 應該設定為 "name\_desc";否則，它應該設定為空字串。 這兩個陳述式會啟動設定資料行標題超連結的檢視，如下所示：

| 目前排序次序 | 姓氏超連結 | 日期超連結 |
| --- | --- | --- |
| 姓氏遞增 | descending | ascending |
| 姓氏遞減 | ascending | ascending |
| 日期遞增 | ascending | descending |
| 日期遞減 | ascending | ascending |

方法會使用[LINQ to Entities](https://msdn.microsoft.com/library/bb386964.aspx)來指定要排序依據的資料行。 此程式碼會在 `switch` 語句之前建立[IQueryable](https://msdn.microsoft.com/library/bb351562.aspx)變數、在 `switch` 語句中修改它，然後在 `switch` 語句之後呼叫 `ToList` 方法。 當您建立和修改 `IQueryable` 變數時，沒有查詢會傳送至資料庫。 在您呼叫方法（例如 `ToList`）將 `IQueryable` 物件轉換成集合之前，不會執行此查詢。 因此，此程式碼會產生一個不會執行的單一查詢，直到 `return View` 語句為止。

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a>將資料行標題超連結新增至學生索引視圖

在*Views\Student\Index.cshtml*中，以反白顯示的程式碼取代標題資料列的 `<tr>` 和 `<th>` 元素：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

這段程式碼會使用 `ViewBag` 屬性中的資訊，以適當的查詢字串值來設定超連結。

執行頁面，然後按一下 [**姓氏**] 和 [**註冊日期] 資料**行標題，確認排序是否有效。

![Students_Index_page_with_sort_hyperlinks](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

當您按一下 [**姓氏**] 標題之後，學生就會以遞減的姓氏順序顯示。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image3.png)

## <a name="add-a-search-box-to-the-students-index-page"></a>將搜尋方塊新增至學生的 [索引] 頁面

若要將篩選新增至 Students 的 [索引] 頁面，您要將文字方塊和提交按鈕新增至檢視，並在 `Index` 方法中進行對應的變更。 文字方塊可讓您輸入要在名字和姓氏欄位中搜尋的字串。

### <a name="add-filtering-functionality-to-the-index-method"></a>將篩選功能新增至 Index 方法

在*Controllers\StudentController.cs*中，以下列程式碼取代 `Index` 方法（變更會反白顯示）：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

您已將 `searchString` 參數新增至 `Index` 方法。 您也已將 `where` 子句新增至 LINQ 語句，其只會選取名字或姓氏包含搜尋字串的學生。 系統會從您要加入至索引視圖的文字方塊中接收搜尋字串值。只有在有要搜尋的值時，才會執行加入[where](https://msdn.microsoft.com/library/bb535040.aspx)子句的語句。

> [!NOTE]
> 在許多情況下，您可以在 Entity Framework 的實體集上呼叫相同的方法，或在記憶體中的集合上，以擴充方法的方式呼叫。 結果通常都相同，但在某些情況下可能會不同。 例如，當您將空字串傳遞給它時，`Contains` 方法的 .NET Framework 執行會傳回所有資料列，但 SQL Server Compact 4.0 的 Entity Framework 提供者會針對空字串傳回零個數據列。 因此，範例中的程式碼（將 `Where` 語句放在 `if` 語句內）可確保您取得所有 SQL Server 版本的相同結果。 此外，`Contains` 方法的 .NET Framework 實預設會執行區分大小寫的比較，但 Entity Framework SQL Server 提供者預設會執行不區分大小寫的比較。 因此，呼叫 `ToUpper` 方法，讓測試明確不區分大小寫，可確保當您稍後變更程式碼以使用存放庫時，不會變更結果，而這會傳回 `IEnumerable` 集合，而不是 `IQueryable` 物件。 (當您在 `IEnumerable` 集合上呼叫 `Contains` 方法時，將取得 .NET Framework 實作；當您在 `IQueryable` 物件上呼叫它時，則會取得資料庫提供者實作。)

### <a name="add-a-search-box-to-the-student-index-view"></a>將 Search Box 新增至 Student [索引] 檢視

在*Views\Student\Index.cshtml*中，將反白顯示的程式碼緊接在開啟的 `table` 標記前面，以便建立標題、文字方塊和**搜尋**按鈕。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=5-10)]

執行頁面，輸入搜尋字串，然後按一下 [**搜尋**] 以確認篩選正在運作。

![Students_Index_page_with_search_box](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image4.png)

請注意，URL 不包含 "a" 搜尋字串，這表示如果您將此頁面加入書簽，則當您使用書簽時，將不會取得篩選過的清單。 稍後在本教學課程中，您將變更 [**搜尋**] 按鈕，以使用篩選準則的查詢字串。

## <a name="add-paging-to-the-students-index-page"></a>將分頁新增至學生的 [索引] 頁面

若要將分頁新增至學生的 [索引] 頁面，您必須先安裝**PagedList** NuGet 套件。 然後您會在 `Index` 方法中進行其他變更，並將分頁連結新增至 [`Index`] 視圖。 **PagedList**是許多適用于 ASP.NET Mvc 的良好分頁和排序套件，其用途僅為範例，而不是其他選項的建議。 下圖顯示分頁連結。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image5.png)

### <a name="install-the-pagedlistmvc-nuget-package"></a>安裝 PagedList NuGet 套件

NuGet **PagedList**會自動將**PagedList**套件安裝為相依性。 **PagedList**套件會針對 `IQueryable` 和 `IEnumerable` 集合安裝 `PagedList` 集合類型和擴充方法。 擴充方法會在 `PagedList` 集合中，從您的 `IQueryable` 或 `IEnumerable`建立單一頁面的資料，而 `PagedList` 集合則提供數個可協助分頁的屬性和方法。 **PagedList**會安裝頁面協助程式，以顯示分頁按鈕。

從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後按一下 [**管理方案的 NuGet 套件**]。

在 [**管理 NuGet 封裝**] 對話方塊中，按一下左側的 [**線上**] 索引標籤，然後在搜尋方塊中輸入「已分頁」。 當您看到**PagedList**封裝時，請按一下 [**安裝**]。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

在 [**選取專案**] 方塊中，按一下 **[確定]** 。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image7.png)

### <a name="add-paging-functionality-to-the-index-method"></a>將分頁功能新增至 Index 方法

在*Controllers\StudentController.cs*中，為 `PagedList` 命名空間新增 `using` 語句：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

以下列程式碼取代 `Index` 方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

這段程式碼會將 `page` 參數、目前的排序次序參數和目前的篩選參數新增至方法簽章，如下所示：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

第一次顯示頁面，或是使用者尚未按一下分頁或排序連結時，所有參數都會是 null。 如果按一下分頁連結，`page` 變數會包含要顯示的頁碼。

`A ViewBag` 屬性會提供具有目前排序次序的視圖，因為這必須包含在分頁連結中，以便在分頁時保持相同的排序次序：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

另一個屬性（`ViewBag.CurrentFilter`）會提供具有目前篩選字串的視圖。 此值必須包含在分頁連結中，才能維護分頁期間的篩選設定，而且它必須在頁面重新顯示時還原為文字方塊。 如果搜尋字串在分頁期間變更，頁面必須重設為 1，因為新的篩選可能會導致顯示不同的資料。 當您在文字方塊中輸入值，並按下 [提交] 按鈕時，就會變更搜尋字串。 在此情況下，`searchString` 參數不是 null。

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

在方法的結尾，學生 `IQueryable` 物件上的 `ToPagedList` 擴充方法會將 student 查詢轉換成支援分頁的集合類型中的一頁學生。 這一頁的學生接著會傳遞至視圖：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

`ToPagedList` 方法會採用頁面數。 這兩個問號代表[null 聯合運算子](https://msdn.microsoft.com/library/ms173224.aspx)。 Null 聯合運算子將針對可為 Null 的型別定義預設值；`(page ?? 1)` 運算式表示在它含有值時會傳回值 `page`，或在 `page` 為 null 時傳回 1。

### <a name="add-paging-links-to-the-student-index-view"></a>將分頁連結新增至學生索引視圖

在*Views\Student\Index.cshtml*中，將現有的程式碼取代為下列程式碼：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=6,9,14-20,56-58)]

頁面頂端的 `@model` 陳述式指定檢視現在會取得 `PagedList` 物件，而不是 `List` 物件。

`PagedList.Mvc` 的 `using` 語句會提供對分頁按鈕之 MVC helper 的存取權。

程式碼會使用[html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)的多載，以允許它指定[FormMethod。 Get](https://msdn.microsoft.com/library/system.web.mvc.formmethod(v=vs.100).aspx/css)。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

預設[html.beginform](https://msdn.microsoft.com/library/system.web.mvc.html.formextensions.beginform(v=vs.108).aspx)會以 POST 提交表單資料，這表示參數會傳遞至 HTTP 訊息內文，而不會在 URL 中作為查詢字串。 當您指定 HTTP GET 時，表單資料會以 URL 中作為查詢字串傳遞，這可讓使用者為該 URL 加上書籤。 [使用 HTTP GET 的 W3C 指導方針](http://www.w3.org/2001/tag/doc/whenToUseGet.html)指定當動作不會產生更新時，您應該使用 GET。

文字方塊會使用目前的搜尋字串進行初始化，因此當您按一下新的頁面時，您可以看到目前的搜尋字串。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

資料行標頭連結會使用查詢字串，將目前的搜尋字串傳遞至控制器，讓使用者可以在篩選結果內排序：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

會顯示目前的頁面和總頁數。

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

如果沒有可顯示的頁面，則會顯示「頁面0為0」。 （在此情況下，頁碼大於頁面計數，因為 `Model.PageNumber` 是1，而 `Model.PageCount` 是0）。

`PagedListPager` helper 會顯示分頁按鈕：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

[`PagedListPager` 協助程式] 提供一些您可以自訂的選項，包括 Url 和樣式。 如需詳細資訊，請參閱 GitHub 網站上的[TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 。

執行頁面。

![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image8.png)

以不同排序次序按一下分頁連結，以確定分頁運作正常。 然後輸入搜尋字串並再次嘗試分頁，以確認分頁的排序和篩選能正確運作。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="create-an-about-page-that-shows-student-statistics"></a>建立顯示學生統計資料的 About 頁面

針對 Contoso 大學網站的 [關於] 頁面，您將會顯示已註冊每個註冊日期的學生人數。 這需要對群組進行分組和簡單計算。 若要完成此工作，您需要執行下列作業：

- 針對您需要傳遞至檢視的資料，建立檢視模型類別。
- 修改 `Home` 控制器中的 `About` 方法。
- 修改 `About` 視圖。

### <a name="create-the-view-model"></a>建立視圖模型

建立*viewmodel*資料夾。 在該資料夾中，新增類別檔案*EnrollmentDateGroup.cs* ，並將現有的程式碼取代為下列程式碼：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a>修改 Home 控制器

在*HomeController.cs*中，將下列 `using` 語句加入檔案的頂端：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

在類別的左大括弧之後，立即新增資料庫內容的類別變數：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

以下列程式碼取代 `About` 方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

LINQ 陳述式會以註冊日期將學生實體組成群組、計算每個群組中的實體數目、將結果儲存在 `EnrollmentDateGroup` 檢視模型物件中的集合。

新增 `Dispose` 方法：

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a>修改 About 檢視

將*Views\Home\About.cshtml*檔案中的程式碼取代為下列程式碼：

[!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

執行應用程式，然後按一下 [**關於**] 連結。 每個註冊日期的學生人數將會顯示在資料表中。

![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image10.png)

## <a name="optional-deploy-the-app-to-windows-azure"></a>選擇性：將應用程式部署至 Windows Azure

到目前為止，您的應用程式已在您的開發電腦上，于本機執行 IIS Express。 若要讓其他人可以透過網際網路使用它，您必須將它部署到 web 主控提供者。 在本教學課程的這個選擇性區段中，您會將它部署到 Windows Azure 網站。

### <a name="using-code-first-migrations-to-deploy-the-database"></a>使用 Code First 移轉部署資料庫

若要部署資料庫，您將使用 Code First 移轉。 當您建立用來設定從 Visual Studio 部署之設定的發行設定檔時，您會選取標示為 **[執行 Code First 移轉（在應用程式啟動時執行）** ] 的核取方塊。 這項設定會導致部署程式在目的地伺服器上自動設定應用程式*的 web.config 檔案*，讓 Code First 使用 `MigrateDatabaseToLatestVersion` 初始化運算式類別。

Visual Studio 在部署過程中不會對資料庫執行任何動作。 當部署的應用程式在部署後第一次存取資料庫時，Code First 會自動建立資料庫，或將資料庫架構更新為最新版本。 如果應用程式 `Seed` 方法來執行遷移，則在建立資料庫或更新架構之後，就會執行此方法。

您的遷移 `Seed` 方法會插入測試資料。 如果您要部署到生產環境，您必須變更 `Seed` 方法，使其只插入您想要插入至實際執行資料庫的資料。 例如，在您目前的資料模型中，您可能想要在開發資料庫中擁有真實的課程，但虛構的學生。 您可以撰寫一個 `Seed` 方法，在開發期間載入，然後在部署到生產環境之前，先將虛構的學生加上批註。 或者，您也可以撰寫 `Seed` 的方法，只載入課程，並使用應用程式的 UI，以手動方式在測試資料庫中輸入虛構的學生。

### <a name="get-a-windows-azure-account"></a>取得 Windows Azure 帳戶

您將需要一個 Windows Azure 帳戶。 如果您還沒有帳戶，只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資訊，請參閱[Windows Azure 免費試用](https://azure.microsoft.com/free/?WT.mc_id=A443DD604)。

### <a name="create-a-web-site-and-a-sql-database-in-windows-azure"></a>在 Windows Azure 中建立網站和 SQL 資料庫

您的 Windows Azure 網站將在共用主控環境中執行，這表示它會在與其他 Windows Azure 用戶端共用的虛擬機器（Vm）上執行。 共用的裝載環境是在雲端中開始使用的低成本方式。 之後，如果您的 web 流量增加，應用程式可以透過在專用 Vm 上執行來調整規模以符合需求。 如果您需要更複雜的架構，您可以遷移至 Windows Azure 雲端服務。 雲端服務會在專用 Vm 上執行，您可以根據自己的需求進行設定。

Windows Azure SQL Database 是以 SQL Server 技術為基礎的雲端式關係資料庫服務。 搭配使用 SQL Server 的工具和應用程式也可以與 SQL Database 搭配使用。

1. 在[Windows Azure 管理入口網站](https://manage.windowsazure.com/)中，按一下左側索引標籤中的 [**網站**]，然後按一下 [**新增**]。

    ![管理入口網站中的 [新增] 按鈕](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image11.png)
2. 按一下 [**自訂建立**]。

    ![在管理入口網站中使用資料庫連結建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image12.png)

   **新的網站-自訂建立**嚮導隨即開啟。
3. 在嚮導的 [**新網站**] 步驟中，于 [ **URL** ] 方塊中輸入字串，以作為應用程式的唯一 URL。 完整的 URL 將包含您在此處輸入的內容，加上您在文字方塊旁看到的尾碼。 此圖顯示「ConU」，但可能會取得該 URL，因此您必須選擇不同的 URL。

    ![在管理入口網站中使用資料庫連結建立](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image13.png)
4. 在 [**區域**] 下拉式清單中，選擇接近您的區域。 此設定會指定您的網站將在哪一個資料中心執行。
5. 在 [**資料庫**] 下拉式清單中，選擇 [**建立免費的 20 MB SQL Database**]。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image14.png)
6. 在 [ **DB 連接字串名稱**] 中，輸入*SchoolCoNtext*。

    ![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image15.png)
7. 按一下方塊底部右側的箭號。 嚮導會前進至 [**資料庫設定**] 步驟。
8. 在 [**名稱**] 方塊中，輸入*ContosoUniversityDB*。
9. 在 [**伺服器**] 方塊中，選取 [**新增 SQL Database 伺服器**]。 或者，如果您先前已建立伺服器，您可以從下拉式清單中選取該伺服器。
10. 輸入系統管理員**登入名稱**和**密碼**。 如果您選取 [**新增 SQL Database 伺服器**]，則不會在此輸入現有的名稱和密碼，而是輸入您目前定義的新名稱和密碼，以便稍後在存取資料庫時使用。 如果您選取先前建立的伺服器，則會輸入該伺服器的認證。 在此教學課程中，您不會選取 [ ***Advanced*** ] 核取方塊。 [ ***Advanced*** ] 選項可讓您設定資料庫定[序](https://msdn.microsoft.com/library/aa174903(v=SQL.80).aspx)。
11. 選擇網站所選擇的相同**區域**。
12. 按一下方塊右下方的核取記號，表示您已經完成。   
  
    ![新網站的資料庫設定步驟-使用資料庫建立嚮導](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image16.png)  

    下圖顯示使用現有的 SQL Server 和登入。   
  
    ![新網站的資料庫設定步驟-使用資料庫建立嚮導](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image17.png)  
  
    管理入口網站會回到 [網站] 頁面，[**狀態**] 欄會顯示正在建立的網站。 經過一段時間（通常不到一分鐘）之後，[**狀態**] 欄會顯示已成功建立網站。 在左側的導覽列中，您帳戶中的網站數目會顯示在 [**網站**] 圖示旁，而且資料庫的數目會顯示在 [ **SQL 資料庫**] 圖示旁。

## <a name="deploy-the-application-to-windows-azure"></a>將應用程式部署至 Windows Azure

1. 在 Visual Studio 中，以滑鼠右鍵按一下**方案總管**中的專案，然後從內容功能表中選取 [**發佈**]。  
  
    ![在專案內容功能表中發佈](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image18.png)
2. 在**發行 Web** wizard 的 [**設定檔**] 索引標籤中，按一下 [匯**入**]。  
  
    ![匯入發行設定](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image19.png)
3. 如果您先前未在 Visual Studio 中新增您的 Windows Azure 訂用帳戶，請執行下列步驟。 在這些步驟中，您會新增訂閱，讓 [**從 Windows Azure**網站匯入] 下的下拉式清單包含您的網站。

    a. 在 [匯**入發行設定檔**] 對話方塊中，按一下 [**從 Windows Azure 網站匯入**]，然後按一下 [**加入 windows azure 訂**用帳戶]。

    ![新增 Windows Azure 訂用帳戶](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image20.png)

    b. 在 [匯**入 Windows Azure 訂閱**] 對話方塊中，按一下 [**下載訂閱**檔案]。

    ![下載訂用帳戶檔案](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image21.png)

    c. 在您的瀏覽器視窗中，儲存 *.publishsettings*檔案。

    ![下載 .publishsettings 檔案](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image22.png)

    > [!WARNING]
    > 安全性- *.publishsettings*檔案包含用來管理 Windows Azure 訂閱和服務的認證（未編碼）。 這個檔案的安全性最佳作法是暫時儲存在來原始目錄之外（例如在*Libraries\Documents*資料夾中），然後在匯入完成後刪除它。 取得 `.publishsettings` 檔案存取權的惡意使用者可以編輯、建立和刪除您的 Windows Azure 服務。

    d. 在 [匯**入 Windows Azure 訂閱**] 對話方塊中，按一下 **[流覽]** 並流覽至 *.publishsettings*檔案。

    ![下載 sub](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image23.png)

    e. 按一下 [匯入]。

    ![匯入](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image24.png)
4. 在 [匯**入發行設定檔**] 對話方塊中，選取 [**從 Windows Azure 網站匯入**]，從下拉式清單中選取您的網站，然後按一下 **[確定]** 。  
  
    ![匯入發行設定檔](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image25.png)
5. 在 [**連接**] 索引標籤中，按一下 [**驗證**連線] 以確定設定正確。  
  
    ![驗證連接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)
6. 當連接經過驗證之後，[**驗證**連線] 按鈕旁會顯示綠色核取記號。 按 [ **下一步**]。  
  
    ![已成功驗證連接](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image27.png)
7. 開啟 [ **SchoolCoNtext** ] 底下的 [**遠端連線字串**] 下拉式清單，然後選取您所建立之資料庫的連接字串。
8. 選取**執行 Code First 移轉（在應用程式啟動時執行）** 。
9. 取消核取 [**在執行時間使用此連接字串**進行**UserCoNtext （DefaultConnection）** ]，因為此應用程式未使用成員資格資料庫。   
  
    ![[設定] 索引標籤](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image28.png)
10. 按 [ **下一步**]。
11. 在 [**預覽**] 索引標籤中，按一下 [**開始預覽**]。  
  
    ![[預覽] 索引標籤中的 [StartPreview] 按鈕](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image29.png)  
  
    [] 索引標籤會顯示將複製到伺服器的檔案清單。 不需要顯示預覽即可發行應用程式，但這是很有用的功能。 在此情況下，您不需要使用顯示的檔案清單來執行任何動作。 下一次部署此應用程式時，只有已變更的檔案才會出現在這份清單中。  
  
    ![StartPreview 檔案輸出](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image30.png)
12. 按一下 [發行]。  
    Visual Studio 開始將檔案複製到 Windows Azure 伺服器的程式。
13. [**輸出**] 視窗會顯示已採取的部署動作，並報告部署已成功完成。  
  
    ![報告部署成功的輸出視窗](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image31.png)
14. 部署成功時，預設瀏覽器會自動開啟至已部署網站的 URL。  
    您所建立的應用程式現在正在雲端中執行。 按一下 [學生] 索引標籤。  
  
    ![Students_index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image32.png)

此時，您的*SchoolCoNtext*資料庫已建立在 Windows Azure SQL Database 中，因為您選取了 **[執行 Code First 移轉] （在應用程式啟動時執行）** 。 已部署網站*中的 web.config*檔案已變更，因此[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始化運算式會在程式碼第一次讀取或寫入資料庫中的資料時執行（在您選取 [**學生**] 索引標籤時，會發生此情況）：

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image33.png)

部署程式也會建立新的連接字串 *（SchoolCoNtext\_DatabasePublish*），以供 Code First 移轉用來更新資料庫架構和植入資料庫。

![Database_Publish 連接字串](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image34.png)

*DefaultConnection*連接字串適用于成員資格資料庫（我們在本教學課程中不會使用）。 *SchoolCoNtext*連接字串適用于 ContosoUniversity 資料庫。

您可以在*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*中的電腦上，找到已部署的 web.config 檔案版本。您可以使用 FTP 來存取已部署的*web.config*檔案本身。 如需指示，請參閱[使用 Visual Studio ASP.NET Web 部署：部署程式碼更新](../../../../web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update.md)。 依照開頭為「使用 FTP 工具」的指示進行，您需要三個專案： FTP URL、使用者名稱和密碼。

> [!NOTE]
> Web 應用程式不會執行安全性，因此任何尋找 URL 的人都可以變更資料。 如需如何保護網站的指示，請參閱將[具有成員資格、OAuth 和 SQL Database 的安全 ASP.NET MVC 應用程式部署到 Windows Azure](https://docs.microsoft.com/aspnet/core/security/authorization/secure-data)網站。 您可以使用 Windows Azure 管理入口網站或 Visual Studio 中的**伺服器總管**，防止其他人使用此網站來停止網站。

![](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image35.png)

## <a name="code-first-initializers"></a>Code First 初始化運算式

在 [部署] 區段中，您會看到正在使用的[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始化運算式。 Code First 也會提供您可以使用的其他初始化運算式，包括[CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) （預設值）、 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx)和[DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)。 `DropCreateAlways` 初始化運算式有助於設定單元測試的條件。 您也可以撰寫自己的初始化運算式，如果您不想等到應用程式讀取或寫入資料庫，可以明確地呼叫初始化運算式。 如需初始化運算式的完整說明，請參閱

## <a name="summary"></a>總結

在本教學課程中，您已瞭解如何建立資料模型，以及如何執行基本的 CRUD、排序、篩選、分頁和群組功能。 在下一個教學課程中，您將藉由展開資料模型來開始查看更多的主題。

您可以在[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [上一頁](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
> [下一頁](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
