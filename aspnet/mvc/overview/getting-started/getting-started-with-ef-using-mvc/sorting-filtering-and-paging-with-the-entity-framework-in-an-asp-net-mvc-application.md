---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：使用 ASP.NET MVC 應用程式中的 Entity Framework 來加入排序、篩選和分頁 |Microsoft Docs
author: tdykstra
description: 在本教學課程中，您會將排序、篩選和分頁功能新增至**學生**的 [索引] 頁面。 您也會建立簡單的群組頁面。
ms.author: riande
ms.date: 01/14/2019
ms.assetid: d5723e46-41fe-4d09-850a-e03b9e285bfa
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.topic: tutorial
ms.openlocfilehash: d9fadc12aa83a8095f364cf39e5376243a7d0670
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616036"
---
# <a name="tutorial-add-sorting-filtering-and-paging-with-the-entity-framework-in-an-aspnet-mvc-application"></a><span data-ttu-id="51f1a-104">教學課程：使用 ASP.NET MVC 應用程式中的 Entity Framework 來加入排序、篩選和分頁</span><span class="sxs-lookup"><span data-stu-id="51f1a-104">Tutorial: Add sorting, filtering, and paging with the Entity Framework in an ASP.NET MVC application</span></span>

<span data-ttu-id="51f1a-105">在[上一個教學](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程中，您已為 `Student` 實體的基本 CRUD 作業實作為一組網頁。</span><span class="sxs-lookup"><span data-stu-id="51f1a-105">In the [previous tutorial](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md), you implemented a set of web pages for basic CRUD operations for `Student` entities.</span></span> <span data-ttu-id="51f1a-106">在本教學課程中，您會將排序、篩選和分頁功能新增至**學生**的 [索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="51f1a-106">In this tutorial you add sorting, filtering, and paging functionality to the **Students** Index page.</span></span> <span data-ttu-id="51f1a-107">您也會建立簡單的群組頁面。</span><span class="sxs-lookup"><span data-stu-id="51f1a-107">You also create a simple grouping page.</span></span>

<span data-ttu-id="51f1a-108">下圖顯示當您完成時，頁面看起來會是什麼樣子。</span><span class="sxs-lookup"><span data-stu-id="51f1a-108">The following image shows what the page will look like when you're done.</span></span> <span data-ttu-id="51f1a-109">資料行標題是使用者可以按一下以依據該資料行排序的連結。</span><span class="sxs-lookup"><span data-stu-id="51f1a-109">The column headings are links that the user can click to sort by that column.</span></span> <span data-ttu-id="51f1a-110">重覆按一下資料行標題，可切換遞增和遞減排序次序。</span><span class="sxs-lookup"><span data-stu-id="51f1a-110">Clicking a column heading repeatedly toggles between ascending and descending sort order.</span></span>

![Students_Index_page_with_paging](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

<span data-ttu-id="51f1a-112">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="51f1a-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51f1a-113">新增資料行排序連結</span><span class="sxs-lookup"><span data-stu-id="51f1a-113">Add column sort links</span></span>
> * <span data-ttu-id="51f1a-114">新增 [搜尋] 方塊</span><span class="sxs-lookup"><span data-stu-id="51f1a-114">Add a Search box</span></span>
> * <span data-ttu-id="51f1a-115">新增分頁</span><span class="sxs-lookup"><span data-stu-id="51f1a-115">Add paging</span></span>
> * <span data-ttu-id="51f1a-116">建立 [關於] 頁面</span><span class="sxs-lookup"><span data-stu-id="51f1a-116">Create an About page</span></span>

## <a name="prerequisites"></a><span data-ttu-id="51f1a-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="51f1a-117">Prerequisites</span></span>

* [<span data-ttu-id="51f1a-118">實作基本的 CRUD 功能</span><span class="sxs-lookup"><span data-stu-id="51f1a-118">Implementing Basic CRUD Functionality</span></span>](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)

## <a name="add-column-sort-links"></a><span data-ttu-id="51f1a-119">新增資料行排序連結</span><span class="sxs-lookup"><span data-stu-id="51f1a-119">Add column sort links</span></span>

<span data-ttu-id="51f1a-120">若要將排序新增至 [學生索引] 頁面，您將變更 `Student` 控制器的 `Index` 方法，並將程式碼新增至 `Student` 索引視圖。</span><span class="sxs-lookup"><span data-stu-id="51f1a-120">To add sorting to the Student Index page, you'll change the `Index` method of the `Student` controller and add code to the `Student` Index view.</span></span>

### <a name="add-sorting-functionality-to-the-index-method"></a><span data-ttu-id="51f1a-121">將排序功能加入至 Index 方法</span><span class="sxs-lookup"><span data-stu-id="51f1a-121">Add sorting functionality to the Index method</span></span>

- <span data-ttu-id="51f1a-122">在*Controllers\StudentController.cs*中，以下列程式碼取代 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="51f1a-122">In *Controllers\StudentController.cs*, replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs)]

<span data-ttu-id="51f1a-123">此程式碼會從 URL 中的查詢字串接收 `sortOrder` 參數。</span><span class="sxs-lookup"><span data-stu-id="51f1a-123">This code receives a `sortOrder` parameter from the query string in the URL.</span></span> <span data-ttu-id="51f1a-124">查詢字串值是由 ASP.NET MVC 當做動作方法的參數來提供。</span><span class="sxs-lookup"><span data-stu-id="51f1a-124">The query string value is provided by ASP.NET MVC as a parameter to the action method.</span></span> <span data-ttu-id="51f1a-125">參數是一個字串，其為 "Name" 或 "Date"，可選擇性地後面接著底線和字串 "desc"，以指定遞減順序。</span><span class="sxs-lookup"><span data-stu-id="51f1a-125">The parameter is a string that's either "Name" or "Date", optionally followed by an underscore and the string "desc" to specify descending order.</span></span> <span data-ttu-id="51f1a-126">預設排序順序為遞增。</span><span class="sxs-lookup"><span data-stu-id="51f1a-126">The default sort order is ascending.</span></span>

<span data-ttu-id="51f1a-127">第一次要求 [索引] 頁面時，沒有任何查詢字串。</span><span class="sxs-lookup"><span data-stu-id="51f1a-127">The first time the Index page is requested, there's no query string.</span></span> <span data-ttu-id="51f1a-128">學生會依 `LastName`以遞增的順序顯示，這是由 `switch` 語句中的逐步執行案例所建立的預設值。</span><span class="sxs-lookup"><span data-stu-id="51f1a-128">The students are displayed in ascending order by `LastName`, which is the default as established by the fall-through case in the `switch` statement.</span></span> <span data-ttu-id="51f1a-129">使用者按一下資料行標題超連結時，適當的 `sortOrder` 值將會在查詢字串值中提供。</span><span class="sxs-lookup"><span data-stu-id="51f1a-129">When the user clicks a column heading hyperlink, the appropriate `sortOrder` value is provided in the query string.</span></span>

<span data-ttu-id="51f1a-130">系統會使用兩個 `ViewBag` 變數，讓此視圖可以使用適當的查詢字串值來設定資料行標題超連結：</span><span class="sxs-lookup"><span data-stu-id="51f1a-130">The two `ViewBag` variables are used so that the view can configure the column heading hyperlinks with the appropriate query string values:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs)]

<span data-ttu-id="51f1a-131">這些是三元陳述式。</span><span class="sxs-lookup"><span data-stu-id="51f1a-131">These are ternary statements.</span></span> <span data-ttu-id="51f1a-132">第一個指定如果 `sortOrder` 參數為 null 或空白，`ViewBag.NameSortParm` 應該設定為 "name\_desc";否則，它應該設定為空字串。</span><span class="sxs-lookup"><span data-stu-id="51f1a-132">The first one specifies that if the `sortOrder` parameter is null or empty, `ViewBag.NameSortParm` should be set to "name\_desc"; otherwise, it should be set to an empty string.</span></span> <span data-ttu-id="51f1a-133">這兩個陳述式會啟動設定資料行標題超連結的檢視，如下所示：</span><span class="sxs-lookup"><span data-stu-id="51f1a-133">These two statements enable the view to set the column heading hyperlinks as follows:</span></span>

| <span data-ttu-id="51f1a-134">目前排序次序</span><span class="sxs-lookup"><span data-stu-id="51f1a-134">Current sort order</span></span> | <span data-ttu-id="51f1a-135">姓氏超連結</span><span class="sxs-lookup"><span data-stu-id="51f1a-135">Last Name Hyperlink</span></span> | <span data-ttu-id="51f1a-136">日期超連結</span><span class="sxs-lookup"><span data-stu-id="51f1a-136">Date Hyperlink</span></span> |
| --- | --- | --- |
| <span data-ttu-id="51f1a-137">姓氏遞增</span><span class="sxs-lookup"><span data-stu-id="51f1a-137">Last Name ascending</span></span> | <span data-ttu-id="51f1a-138">descending</span><span class="sxs-lookup"><span data-stu-id="51f1a-138">descending</span></span> | <span data-ttu-id="51f1a-139">ascending</span><span class="sxs-lookup"><span data-stu-id="51f1a-139">ascending</span></span> |
| <span data-ttu-id="51f1a-140">姓氏遞減</span><span class="sxs-lookup"><span data-stu-id="51f1a-140">Last Name descending</span></span> | <span data-ttu-id="51f1a-141">ascending</span><span class="sxs-lookup"><span data-stu-id="51f1a-141">ascending</span></span> | <span data-ttu-id="51f1a-142">ascending</span><span class="sxs-lookup"><span data-stu-id="51f1a-142">ascending</span></span> |
| <span data-ttu-id="51f1a-143">日期遞增</span><span class="sxs-lookup"><span data-stu-id="51f1a-143">Date ascending</span></span> | <span data-ttu-id="51f1a-144">ascending</span><span class="sxs-lookup"><span data-stu-id="51f1a-144">ascending</span></span> | <span data-ttu-id="51f1a-145">descending</span><span class="sxs-lookup"><span data-stu-id="51f1a-145">descending</span></span> |
| <span data-ttu-id="51f1a-146">日期遞減</span><span class="sxs-lookup"><span data-stu-id="51f1a-146">Date descending</span></span> | <span data-ttu-id="51f1a-147">ascending</span><span class="sxs-lookup"><span data-stu-id="51f1a-147">ascending</span></span> | <span data-ttu-id="51f1a-148">ascending</span><span class="sxs-lookup"><span data-stu-id="51f1a-148">ascending</span></span> |

<span data-ttu-id="51f1a-149">方法會使用[LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities)來指定要排序依據的資料行。</span><span class="sxs-lookup"><span data-stu-id="51f1a-149">The method uses [LINQ to Entities](/dotnet/framework/data/adonet/ef/language-reference/linq-to-entities) to specify the column to sort by.</span></span> <span data-ttu-id="51f1a-150">此程式碼會在 `switch` 語句之前建立 <xref:System.Linq.IQueryable%601> 變數、在 `switch` 語句中修改它，並在 `switch` 語句之後呼叫 `ToList` 方法。</span><span class="sxs-lookup"><span data-stu-id="51f1a-150">The code creates an <xref:System.Linq.IQueryable%601> variable before the `switch` statement, modifies it in the `switch` statement, and calls the `ToList` method after the `switch` statement.</span></span> <span data-ttu-id="51f1a-151">當您建立和修改 `IQueryable` 變數時，沒有查詢會傳送至資料庫。</span><span class="sxs-lookup"><span data-stu-id="51f1a-151">When you create and modify `IQueryable` variables, no query is sent to the database.</span></span> <span data-ttu-id="51f1a-152">在您呼叫方法（例如 `ToList`）將 `IQueryable` 物件轉換成集合之前，不會執行此查詢。</span><span class="sxs-lookup"><span data-stu-id="51f1a-152">The query is not executed until you convert the `IQueryable` object into a collection by calling a method such as `ToList`.</span></span> <span data-ttu-id="51f1a-153">因此，此程式碼會產生一個不會執行的單一查詢，直到 `return View` 語句為止。</span><span class="sxs-lookup"><span data-stu-id="51f1a-153">Therefore, this code results in a single query that is not executed until the `return View` statement.</span></span>

<span data-ttu-id="51f1a-154">除了針對每個排序次序撰寫不同 LINQ 語句以外，您還可以動態建立 LINQ 語句。</span><span class="sxs-lookup"><span data-stu-id="51f1a-154">As an alternative to writing different LINQ statements for each sort order, you can dynamically create a LINQ statement.</span></span> <span data-ttu-id="51f1a-155">如需動態 LINQ 的詳細資訊，請參閱[動態 linq](https://go.microsoft.com/fwlink/?LinkID=323957)。</span><span class="sxs-lookup"><span data-stu-id="51f1a-155">For information about dynamic LINQ, see [Dynamic LINQ](https://go.microsoft.com/fwlink/?LinkID=323957).</span></span>

### <a name="add-column-heading-hyperlinks-to-the-student-index-view"></a><span data-ttu-id="51f1a-156">將資料行標題超連結新增至學生索引視圖</span><span class="sxs-lookup"><span data-stu-id="51f1a-156">Add column heading hyperlinks to the Student index view</span></span>

1. <span data-ttu-id="51f1a-157">在*Views\Student\Index.cshtml*中，以反白顯示的程式碼取代標題資料列的 `<tr>` 和 `<th>` 元素：</span><span class="sxs-lookup"><span data-stu-id="51f1a-157">In *Views\Student\Index.cshtml*, replace the `<tr>` and `<th>` elements for the heading row with the highlighted code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cshtml?highlight=5-15)]

   <span data-ttu-id="51f1a-158">這段程式碼會使用 `ViewBag` 屬性中的資訊，以適當的查詢字串值來設定超連結。</span><span class="sxs-lookup"><span data-stu-id="51f1a-158">This code uses the information in the `ViewBag` properties to set up hyperlinks with the appropriate query string values.</span></span>

2. <span data-ttu-id="51f1a-159">執行頁面，然後按一下 [**姓氏**] 和 [**註冊日期] 資料**行標題，確認排序是否有效。</span><span class="sxs-lookup"><span data-stu-id="51f1a-159">Run the page and click the **Last Name** and **Enrollment Date** column headings to verify that sorting works.</span></span>

   <span data-ttu-id="51f1a-160">當您按一下 [**姓氏**] 標題之後，學生就會以遞減的姓氏順序顯示。</span><span class="sxs-lookup"><span data-stu-id="51f1a-160">After you click the **Last Name** heading, students are displayed in descending last name order.</span></span>

## <a name="add-a-search-box"></a><span data-ttu-id="51f1a-161">新增 [搜尋] 方塊</span><span class="sxs-lookup"><span data-stu-id="51f1a-161">Add a Search box</span></span>

<span data-ttu-id="51f1a-162">若要將篩選加入至學生的 [索引] 頁面，您要將文字方塊和 [提交] 按鈕新增至視圖，並在 `Index` 方法中進行對應的變更。</span><span class="sxs-lookup"><span data-stu-id="51f1a-162">To add filtering to the Students index page, you'll add a text box and a submit button to the view and make corresponding changes in the `Index` method.</span></span> <span data-ttu-id="51f1a-163">文字方塊可讓您輸入要在 [名字] 和 [姓氏] 欄位中搜尋的字串。</span><span class="sxs-lookup"><span data-stu-id="51f1a-163">The text box lets you enter a string to search for in the first name and last name fields.</span></span>

### <a name="add-filtering-functionality-to-the-index-method"></a><span data-ttu-id="51f1a-164">將篩選功能新增至 Index 方法</span><span class="sxs-lookup"><span data-stu-id="51f1a-164">Add filtering functionality to the Index method</span></span>

- <span data-ttu-id="51f1a-165">在*Controllers\StudentController.cs*中，以下列程式碼取代 `Index` 方法（變更會反白顯示）：</span><span class="sxs-lookup"><span data-stu-id="51f1a-165">In *Controllers\StudentController.cs*, replace the `Index` method with the following code (the changes are highlighted):</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs?highlight=1,7-11)]

<span data-ttu-id="51f1a-166">程式碼會將 `searchString` 參數新增至 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="51f1a-166">The code adds a `searchString` parameter to the `Index` method.</span></span> <span data-ttu-id="51f1a-167">從將新增至 [索引] 檢視的文字方塊中接收搜尋字串值。</span><span class="sxs-lookup"><span data-stu-id="51f1a-167">The search string value is received from a text box that you'll add to the Index view.</span></span> <span data-ttu-id="51f1a-168">它也會將 `where` 子句新增至 LINQ 語句，而這只會選取其名字或姓氏包含搜尋字串的學生。</span><span class="sxs-lookup"><span data-stu-id="51f1a-168">It also adds a `where` clause to the LINQ statement that selects only students whose first name or last name contains the search string.</span></span> <span data-ttu-id="51f1a-169">只有在有要搜尋的值時，才會執行加入 <xref:System.Linq.Queryable.Where%2A> 子句的語句。</span><span class="sxs-lookup"><span data-stu-id="51f1a-169">The statement that adds the <xref:System.Linq.Queryable.Where%2A> clause executes only if there's a value to search for.</span></span>

> [!NOTE]
> <span data-ttu-id="51f1a-170">在許多情況下，您可以在 Entity Framework 的實體集上呼叫相同的方法，或在記憶體中的集合上，以擴充方法的方式呼叫。</span><span class="sxs-lookup"><span data-stu-id="51f1a-170">In many cases you can call the same method either on an Entity Framework entity set or as an extension method on an in-memory collection.</span></span> <span data-ttu-id="51f1a-171">結果通常都相同，但在某些情況下可能會不同。</span><span class="sxs-lookup"><span data-stu-id="51f1a-171">The results are normally the same but in some cases may be different.</span></span>
>
> <span data-ttu-id="51f1a-172">例如，當您將空字串傳遞給它時，`Contains` 方法的 .NET Framework 執行會傳回所有資料列，但 SQL Server Compact 4.0 的 Entity Framework 提供者會針對空字串傳回零個數據列。</span><span class="sxs-lookup"><span data-stu-id="51f1a-172">For example, the .NET Framework implementation of the `Contains` method returns all rows when you pass an empty string to it, but the Entity Framework provider for SQL Server Compact 4.0 returns zero rows for empty strings.</span></span> <span data-ttu-id="51f1a-173">因此，範例中的程式碼（將 `Where` 語句放在 `if` 語句內）可確保您取得所有 SQL Server 版本的相同結果。</span><span class="sxs-lookup"><span data-stu-id="51f1a-173">Therefore the code in the example (putting the `Where` statement inside an `if` statement) makes sure that you get the same results for all versions of SQL Server.</span></span> <span data-ttu-id="51f1a-174">此外，`Contains` 方法的 .NET Framework 實預設會執行區分大小寫的比較，但 Entity Framework SQL Server 提供者預設會執行不區分大小寫的比較。</span><span class="sxs-lookup"><span data-stu-id="51f1a-174">Also, the .NET Framework implementation of the `Contains` method performs a case-sensitive comparison by default, but Entity Framework SQL Server providers perform case-insensitive comparisons by default.</span></span> <span data-ttu-id="51f1a-175">因此，呼叫 `ToUpper` 方法，讓測試明確不區分大小寫，可確保當您稍後變更程式碼以使用存放庫時，不會變更結果，而這會傳回 `IEnumerable` 集合，而不是 `IQueryable` 物件。</span><span class="sxs-lookup"><span data-stu-id="51f1a-175">Therefore, calling the `ToUpper` method to make the test explicitly case-insensitive ensures that results do not change when you change the code later to use a repository, which will return an `IEnumerable` collection instead of an `IQueryable` object.</span></span> <span data-ttu-id="51f1a-176">(當您在 `Contains` 集合上呼叫 `IEnumerable` 方法時，將取得 .NET Framework 實作；當您在 `IQueryable` 物件上呼叫它時，則會取得資料庫提供者實作。)</span><span class="sxs-lookup"><span data-stu-id="51f1a-176">(When you call the `Contains` method on an `IEnumerable` collection, you get the .NET Framework implementation; when you call it on an `IQueryable` object, you get the database provider implementation.)</span></span>
>
> <span data-ttu-id="51f1a-177">不同資料庫提供者的 Null 處理也可能不同，或當您使用 `IEnumerable` 集合時，與使用 `IQueryable` 物件時相同。</span><span class="sxs-lookup"><span data-stu-id="51f1a-177">Null handling may also be different for different database providers or when you use an `IQueryable` object compared to when you use an `IEnumerable` collection.</span></span> <span data-ttu-id="51f1a-178">例如，在某些情況下，`Where` 條件（例如 `table.Column != 0`）可能不會傳回具有 `null` 值的資料行。</span><span class="sxs-lookup"><span data-stu-id="51f1a-178">For example, in some scenarios a `Where` condition such as `table.Column != 0` may not return columns that have `null` as the value.</span></span> <span data-ttu-id="51f1a-179">根據預設，EF 會產生額外的 SQL 運算子，使 null 值能夠在資料庫中運作，就像它在記憶體中運作一樣，但是您可以在 EF6 中設定[UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics)旗標，或在 EF Core 中呼叫[UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls)方法來設定此行為。</span><span class="sxs-lookup"><span data-stu-id="51f1a-179">By default, EF generates additional SQL operators to make equality between null values work in the database like it works in memory, but you can set the [UseDatabaseNullSemantics](https://docs.microsoft.com/dotnet/api/system.data.entity.infrastructure.dbcontextconfiguration.usedatabasenullsemantics) flag in EF6 or call the [UseRelationalNulls](https://docs.microsoft.com/dotnet/api/microsoft.entityframeworkcore.infrastructure.relationaldbcontextoptionsbuilder-2.userelationalnulls) method in EF Core to configure this behavior.</span></span>

### <a name="add-a-search-box-to-the-student-index-view"></a><span data-ttu-id="51f1a-180">將搜尋方塊新增至學生的 [索引] 視圖</span><span class="sxs-lookup"><span data-stu-id="51f1a-180">Add a search box to the Student index view</span></span>

1. <span data-ttu-id="51f1a-181">在*Views\Student\Index.cshtml*中，將反白顯示的程式碼緊接在開啟的 `table` 標記前面，以便建立標題、文字方塊和**搜尋**按鈕。</span><span class="sxs-lookup"><span data-stu-id="51f1a-181">In *Views\Student\Index.cshtml*, add the highlighted code immediately before the opening `table` tag in order to create a caption, a text box, and a **Search** button.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml?highlight=4-11)]

2. <span data-ttu-id="51f1a-182">執行頁面，輸入搜尋字串，然後按一下 [**搜尋**] 以確認篩選正在運作。</span><span class="sxs-lookup"><span data-stu-id="51f1a-182">Run the page, enter a search string, and click **Search** to verify that filtering is working.</span></span>

   <span data-ttu-id="51f1a-183">請注意，URL 不包含 "a" 搜尋字串，這表示如果您將此頁面加入書簽，則當您使用書簽時，將不會取得篩選過的清單。</span><span class="sxs-lookup"><span data-stu-id="51f1a-183">Notice the URL doesn't contain the "an" search string, which means that if you bookmark this page, you won't get the filtered list when you use the bookmark.</span></span> <span data-ttu-id="51f1a-184">這也適用于資料行排序連結，因為它們會排序整個清單。</span><span class="sxs-lookup"><span data-stu-id="51f1a-184">This applies also to the column sort links, as they will sort the whole list.</span></span> <span data-ttu-id="51f1a-185">稍後在本教學課程中，您將變更 [**搜尋**] 按鈕，以使用篩選準則的查詢字串。</span><span class="sxs-lookup"><span data-stu-id="51f1a-185">You'll change the **Search** button to use query strings for filter criteria later in the tutorial.</span></span>

## <a name="add-paging"></a><span data-ttu-id="51f1a-186">新增分頁</span><span class="sxs-lookup"><span data-stu-id="51f1a-186">Add paging</span></span>

<span data-ttu-id="51f1a-187">若要將分頁新增至學生的 [索引] 頁面，您必須先安裝**PagedList** NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="51f1a-187">To add paging to the Students index page, you'll start by installing the **PagedList.Mvc** NuGet package.</span></span> <span data-ttu-id="51f1a-188">然後您會在 `Index` 方法中進行其他變更，並將分頁連結新增至 [`Index`] 視圖。</span><span class="sxs-lookup"><span data-stu-id="51f1a-188">Then you'll make additional changes in the `Index` method and add paging links to the `Index` view.</span></span> <span data-ttu-id="51f1a-189">**PagedList**是許多適用于 ASP.NET Mvc 的良好分頁和排序套件，其用途僅為範例，而不是其他選項的建議。</span><span class="sxs-lookup"><span data-stu-id="51f1a-189">**PagedList.Mvc** is one of many good paging and sorting packages for ASP.NET MVC, and its use here is intended only as an example, not as a recommendation for it over other options.</span></span>

### <a name="install-the-pagedlistmvc-nuget-package"></a><span data-ttu-id="51f1a-190">安裝 PagedList NuGet 套件</span><span class="sxs-lookup"><span data-stu-id="51f1a-190">Install the PagedList.MVC NuGet package</span></span>

<span data-ttu-id="51f1a-191">NuGet **PagedList**會自動將**PagedList**套件安裝為相依性。</span><span class="sxs-lookup"><span data-stu-id="51f1a-191">The NuGet **PagedList.Mvc** package automatically installs the **PagedList** package as a dependency.</span></span> <span data-ttu-id="51f1a-192">**PagedList**套件會針對 `IQueryable` 和 `IEnumerable` 集合安裝 `PagedList` 集合類型和擴充方法。</span><span class="sxs-lookup"><span data-stu-id="51f1a-192">The **PagedList** package installs a `PagedList` collection type and extension methods for `IQueryable` and `IEnumerable` collections.</span></span> <span data-ttu-id="51f1a-193">擴充方法會在 `PagedList` 集合中，從您的 `IQueryable` 或 `IEnumerable`建立單一頁面的資料，而 `PagedList` 集合則提供數個可協助分頁的屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="51f1a-193">The extension methods create a single page of data in a `PagedList` collection out of your `IQueryable` or `IEnumerable`, and the `PagedList` collection provides several properties and methods that facilitate paging.</span></span> <span data-ttu-id="51f1a-194">**PagedList**會安裝頁面協助程式，以顯示分頁按鈕。</span><span class="sxs-lookup"><span data-stu-id="51f1a-194">The **PagedList.Mvc** package installs a paging helper that displays the paging buttons.</span></span>

1. <span data-ttu-id="51f1a-195">從 [**工具**] 功能表中，依序選取 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="51f1a-195">From the **Tools** menu, select **NuGet Package Manager** and then **Package Manager Console**.</span></span>

2. <span data-ttu-id="51f1a-196">在 [**套件管理員主控台**] 視窗中，確定 [**套件來源**] 是**nuget.org** ，而 [**預設專案**] 是 [ **ContosoUniversity**]，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="51f1a-196">In the **Package Manager Console** window, make sure the **Package source** is **nuget.org** and the **Default project** is **ContosoUniversity**, and then enter the following command:</span></span>

   ```text
   Install-Package PagedList.Mvc
   ```

3. <span data-ttu-id="51f1a-197">建置專案。</span><span class="sxs-lookup"><span data-stu-id="51f1a-197">Build the project.</span></span>

### <a name="add-paging-functionality-to-the-index-method"></a><span data-ttu-id="51f1a-198">將分頁功能新增至 Index 方法</span><span class="sxs-lookup"><span data-stu-id="51f1a-198">Add paging functionality to the Index method</span></span>

1. <span data-ttu-id="51f1a-199">在*Controllers\StudentController.cs*中，為 `PagedList` 命名空間新增 `using` 語句：</span><span class="sxs-lookup"><span data-stu-id="51f1a-199">In *Controllers\StudentController.cs*, add a `using` statement for the `PagedList` namespace:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs)]

2. <span data-ttu-id="51f1a-200">以下列程式碼取代 `Index` 方法：</span><span class="sxs-lookup"><span data-stu-id="51f1a-200">Replace the `Index` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=1,3,7-16,41-43)]

   <span data-ttu-id="51f1a-201">此程式碼會將 `page` 參數、目前的排序次序參數，以及目前的篩選參數新增至方法簽章：</span><span class="sxs-lookup"><span data-stu-id="51f1a-201">This code adds a `page` parameter, a current sort order parameter, and a current filter parameter to the method signature:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

   <span data-ttu-id="51f1a-202">第一次顯示頁面，或使用者未按一下分頁或排序連結時，所有參數都是 null。</span><span class="sxs-lookup"><span data-stu-id="51f1a-202">The first time the page is displayed, or if the user hasn't clicked a paging or sorting link, all the parameters are null.</span></span> <span data-ttu-id="51f1a-203">如果按一下分頁連結，`page` 變數會包含要顯示的頁碼。</span><span class="sxs-lookup"><span data-stu-id="51f1a-203">If a paging link is clicked, the `page` variable contains the page number to display.</span></span>

   <span data-ttu-id="51f1a-204">`ViewBag` 屬性會提供具有目前排序次序的視圖，因為這必須包含在分頁連結中，以便在分頁時保持相同的排序次序：</span><span class="sxs-lookup"><span data-stu-id="51f1a-204">A `ViewBag` property provides the view with the current sort order, because this must be included in the paging links in order to keep the sort order the same while paging:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample9.cs)]

   <span data-ttu-id="51f1a-205">另一個屬性（`ViewBag.CurrentFilter`）會提供具有目前篩選字串的視圖。</span><span class="sxs-lookup"><span data-stu-id="51f1a-205">Another property, `ViewBag.CurrentFilter`, provides the view with the current filter string.</span></span> <span data-ttu-id="51f1a-206">此值必須包含在分頁連結中，才能維護分頁期間的篩選設定，而且它必須在頁面重新顯示時還原為文字方塊。</span><span class="sxs-lookup"><span data-stu-id="51f1a-206">This value must be included in the paging links in order to maintain the filter settings during paging, and it must be restored to the text box when the page is redisplayed.</span></span> <span data-ttu-id="51f1a-207">如果搜尋字串在分頁期間變更，頁面必須重設為 1，因為新的篩選可能會導致顯示不同的資料。</span><span class="sxs-lookup"><span data-stu-id="51f1a-207">If the search string is changed during paging, the page has to be reset to 1, because the new filter can result in different data to display.</span></span> <span data-ttu-id="51f1a-208">當您在文字方塊中輸入值，並按下 [提交] 按鈕時，就會變更搜尋字串。</span><span class="sxs-lookup"><span data-stu-id="51f1a-208">The search string is changed when a value is entered in the text box and the submit button is pressed.</span></span> <span data-ttu-id="51f1a-209">在此情況下，`searchString` 參數不是 null。</span><span class="sxs-lookup"><span data-stu-id="51f1a-209">In that case, the `searchString` parameter is not null.</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample10.cs)]

   <span data-ttu-id="51f1a-210">在方法的結尾，學生 `IQueryable` 物件上的 `ToPagedList` 擴充方法會將 student 查詢轉換成支援分頁的集合類型中的一頁學生。</span><span class="sxs-lookup"><span data-stu-id="51f1a-210">At the end of the method, the `ToPagedList` extension method on the students `IQueryable` object converts the student query to a single page of students in a collection type that supports paging.</span></span> <span data-ttu-id="51f1a-211">這一頁的學生接著會傳遞至視圖：</span><span class="sxs-lookup"><span data-stu-id="51f1a-211">That single page of students is then passed to the view:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample11.cs)]

   <span data-ttu-id="51f1a-212">`ToPagedList` 方法會採用頁面數。</span><span class="sxs-lookup"><span data-stu-id="51f1a-212">The `ToPagedList` method takes a page number.</span></span> <span data-ttu-id="51f1a-213">這兩個問號代表[null 聯合運算子](/dotnet/csharp/language-reference/operators/null-coalescing-operator)。</span><span class="sxs-lookup"><span data-stu-id="51f1a-213">The two question marks represent the [null-coalescing operator](/dotnet/csharp/language-reference/operators/null-coalescing-operator).</span></span> <span data-ttu-id="51f1a-214">Null 聯合運算子將針對可為 Null 的型別定義預設值；`(page ?? 1)` 運算式表示在它含有值時會傳回值 `page`，或在 `page` 為 null 時傳回 1。</span><span class="sxs-lookup"><span data-stu-id="51f1a-214">The null-coalescing operator defines a default value for a nullable type; the expression `(page ?? 1)` means return the value of `page` if it has a value, or return 1 if `page` is null.</span></span>

### <a name="add-paging-links-to-the-student-index-view"></a><span data-ttu-id="51f1a-215">將分頁連結新增至學生索引視圖</span><span class="sxs-lookup"><span data-stu-id="51f1a-215">Add paging links to the Student index view</span></span>

1. <span data-ttu-id="51f1a-216">在*Views\Student\Index.cshtml*中，將現有的程式碼取代為下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="51f1a-216">In *Views\Student\Index.cshtml*, replace the existing code with the following code.</span></span> <span data-ttu-id="51f1a-217">所做的變更已醒目標示。</span><span class="sxs-lookup"><span data-stu-id="51f1a-217">The changes are highlighted.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample12.cshtml?highlight=1-3,6,9,14,17,24,30,55-56,58-59)]

   <span data-ttu-id="51f1a-218">頁面頂端的 `@model` 陳述式指定檢視現在會取得 `PagedList` 物件，而不是 `List` 物件。</span><span class="sxs-lookup"><span data-stu-id="51f1a-218">The `@model` statement at the top of the page specifies that the view now gets a `PagedList` object instead of a `List` object.</span></span>

   <span data-ttu-id="51f1a-219">`PagedList.Mvc` 的 `using` 語句會提供對分頁按鈕之 MVC helper 的存取權。</span><span class="sxs-lookup"><span data-stu-id="51f1a-219">The `using` statement for `PagedList.Mvc` gives access to the MVC helper for the paging buttons.</span></span>

   <span data-ttu-id="51f1a-220">程式碼會使用[html.beginform](/previous-versions/aspnet/dd492719(v=vs.108))的多載，以允許它指定[FormMethod。 Get](/previous-versions/aspnet/dd460179(v=vs.100))。</span><span class="sxs-lookup"><span data-stu-id="51f1a-220">The code uses an overload of [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) that allows it to specify [FormMethod.Get](/previous-versions/aspnet/dd460179(v=vs.100)).</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample13.cshtml?highlight=1)]

   <span data-ttu-id="51f1a-221">預設[html.beginform](/previous-versions/aspnet/dd492719(v=vs.108))會以 POST 提交表單資料，這表示參數會傳遞至 HTTP 訊息內文，而不會在 URL 中作為查詢字串。</span><span class="sxs-lookup"><span data-stu-id="51f1a-221">The default [BeginForm](/previous-versions/aspnet/dd492719(v=vs.108)) submits form data with a POST, which means that parameters are passed in the HTTP message body and not in the URL as query strings.</span></span> <span data-ttu-id="51f1a-222">當您指定 HTTP GET 時，表單資料會以 URL 中作為查詢字串傳遞，這可讓使用者為該 URL 加上書籤。</span><span class="sxs-lookup"><span data-stu-id="51f1a-222">When you specify HTTP GET, the form data is passed in the URL as query strings, which enables users to bookmark the URL.</span></span> <span data-ttu-id="51f1a-223">[使用 HTTP get 的 W3C 指導方針](http://www.w3.org/2001/tag/doc/whenToUseGet.html)建議您在動作不會產生更新時使用 get。</span><span class="sxs-lookup"><span data-stu-id="51f1a-223">The [W3C guidelines for the use of HTTP GET](http://www.w3.org/2001/tag/doc/whenToUseGet.html) recommend that you should use GET when the action does not result in an update.</span></span>

   <span data-ttu-id="51f1a-224">文字方塊會使用目前的搜尋字串進行初始化，因此當您按一下新的頁面時，您可以看到目前的搜尋字串。</span><span class="sxs-lookup"><span data-stu-id="51f1a-224">The text box is initialized with the current search string so when you click a new page you can see the current search string.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample14.cshtml?highlight=1)]

   <span data-ttu-id="51f1a-225">資料行標頭連結會使用查詢字串，將目前的搜尋字串傳遞至控制器，讓使用者可以在篩選結果內排序：</span><span class="sxs-lookup"><span data-stu-id="51f1a-225">The column header links use the query string to pass the current search string to the controller so that the user can sort within filter results:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample15.cshtml?highlight=1)]

   <span data-ttu-id="51f1a-226">會顯示目前的頁面和總頁數。</span><span class="sxs-lookup"><span data-stu-id="51f1a-226">The current page and total number of pages are displayed.</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample16.cshtml)]

   <span data-ttu-id="51f1a-227">如果沒有可顯示的頁面，則會顯示「頁面0為0」。</span><span class="sxs-lookup"><span data-stu-id="51f1a-227">If there are no pages to display, "Page 0 of 0" is shown.</span></span> <span data-ttu-id="51f1a-228">（在此情況下，頁碼大於頁面計數，因為 `Model.PageNumber` 是1，而 `Model.PageCount` 是0）。</span><span class="sxs-lookup"><span data-stu-id="51f1a-228">(In that case the page number is greater than the page count because `Model.PageNumber` is 1, and `Model.PageCount` is 0.)</span></span>

   <span data-ttu-id="51f1a-229">`PagedListPager` helper 會顯示分頁按鈕：</span><span class="sxs-lookup"><span data-stu-id="51f1a-229">The paging buttons are displayed by the `PagedListPager` helper:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample17.cshtml)]

   <span data-ttu-id="51f1a-230">[`PagedListPager` 協助程式] 提供一些您可以自訂的選項，包括 Url 和樣式。</span><span class="sxs-lookup"><span data-stu-id="51f1a-230">The `PagedListPager` helper provides a number of options that you can customize, including URLs and styling.</span></span> <span data-ttu-id="51f1a-231">如需詳細資訊，請參閱 GitHub 網站上的[TroyGoode/PagedList](https://github.com/TroyGoode/PagedList) 。</span><span class="sxs-lookup"><span data-stu-id="51f1a-231">For more information, see [TroyGoode / PagedList](https://github.com/TroyGoode/PagedList) on the GitHub site.</span></span>

2. <span data-ttu-id="51f1a-232">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="51f1a-232">Run the page.</span></span>

   <span data-ttu-id="51f1a-233">以不同排序次序按一下分頁連結，以確定分頁運作正常。</span><span class="sxs-lookup"><span data-stu-id="51f1a-233">Click the paging links in different sort orders to make sure paging works.</span></span> <span data-ttu-id="51f1a-234">然後輸入搜尋字串並再次嘗試分頁，以確認分頁的排序和篩選能正確運作。</span><span class="sxs-lookup"><span data-stu-id="51f1a-234">Then enter a search string and try paging again to verify that paging also works correctly with sorting and filtering.</span></span>

## <a name="create-an-about-page"></a><span data-ttu-id="51f1a-235">建立 [關於] 頁面</span><span class="sxs-lookup"><span data-stu-id="51f1a-235">Create an About page</span></span>

<span data-ttu-id="51f1a-236">針對 Contoso 大學網站的 [關於] 頁面，您將會顯示已註冊每個註冊日期的學生人數。</span><span class="sxs-lookup"><span data-stu-id="51f1a-236">For the Contoso University website's About page, you'll display how many students have enrolled for each enrollment date.</span></span> <span data-ttu-id="51f1a-237">這需要對群組進行分組和簡單計算。</span><span class="sxs-lookup"><span data-stu-id="51f1a-237">This requires grouping and simple calculations on the groups.</span></span> <span data-ttu-id="51f1a-238">若要完成此工作，您需要執行下列作業：</span><span class="sxs-lookup"><span data-stu-id="51f1a-238">To accomplish this, you'll do the following:</span></span>

- <span data-ttu-id="51f1a-239">針對您需要傳遞至檢視的資料，建立檢視模型類別。</span><span class="sxs-lookup"><span data-stu-id="51f1a-239">Create a view model class for the data that you need to pass to the view.</span></span>
- <span data-ttu-id="51f1a-240">修改 `Home` 控制器中的 `About` 方法。</span><span class="sxs-lookup"><span data-stu-id="51f1a-240">Modify the `About` method in the `Home` controller.</span></span>
- <span data-ttu-id="51f1a-241">修改 `About` 視圖。</span><span class="sxs-lookup"><span data-stu-id="51f1a-241">Modify the `About` view.</span></span>

### <a name="create-the-view-model"></a><span data-ttu-id="51f1a-242">建立視圖模型</span><span class="sxs-lookup"><span data-stu-id="51f1a-242">Create the View Model</span></span>

<span data-ttu-id="51f1a-243">在專案資料夾中建立*viewmodel*資料夾。</span><span class="sxs-lookup"><span data-stu-id="51f1a-243">Create a *ViewModels* folder in the project folder.</span></span> <span data-ttu-id="51f1a-244">在該資料夾中，新增類別檔案*EnrollmentDateGroup.cs* ，並將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="51f1a-244">In that folder, add a class file *EnrollmentDateGroup.cs* and replace the template code with the following code:</span></span>

[!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample18.cs)]

### <a name="modify-the-home-controller"></a><span data-ttu-id="51f1a-245">修改 Home 控制器</span><span class="sxs-lookup"><span data-stu-id="51f1a-245">Modify the Home Controller</span></span>

1. <span data-ttu-id="51f1a-246">在*HomeController.cs*中，將下列 `using` 語句加入檔案的頂端：</span><span class="sxs-lookup"><span data-stu-id="51f1a-246">In *HomeController.cs*, add the following `using` statements at the top of the file:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample19.cs)]

2. <span data-ttu-id="51f1a-247">在類別的左大括弧之後，立即新增資料庫內容的類別變數：</span><span class="sxs-lookup"><span data-stu-id="51f1a-247">Add a class variable for the database context immediately after the opening curly brace for the class:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample20.cs?highlight=3)]

3. <span data-ttu-id="51f1a-248">以下列程式碼取代 `About` 方法：</span><span class="sxs-lookup"><span data-stu-id="51f1a-248">Replace the `About` method with the following code:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample21.cs)]

   <span data-ttu-id="51f1a-249">LINQ 陳述式會以註冊日期將學生實體組成群組、計算每個群組中的實體數目、將結果儲存在 `EnrollmentDateGroup` 檢視模型物件中的集合。</span><span class="sxs-lookup"><span data-stu-id="51f1a-249">The LINQ statement groups the student entities by enrollment date, calculates the number of entities in each group, and stores the results in a collection of `EnrollmentDateGroup` view model objects.</span></span>

4. <span data-ttu-id="51f1a-250">新增 `Dispose` 方法：</span><span class="sxs-lookup"><span data-stu-id="51f1a-250">Add a `Dispose` method:</span></span>

   [!code-csharp[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample22.cs)]

### <a name="modify-the-about-view"></a><span data-ttu-id="51f1a-251">修改 About 檢視</span><span class="sxs-lookup"><span data-stu-id="51f1a-251">Modify the About View</span></span>

1. <span data-ttu-id="51f1a-252">將*Views\Home\About.cshtml*檔案中的程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="51f1a-252">Replace the code in the *Views\Home\About.cshtml* file with the following code:</span></span>

   [!code-cshtml[Main](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample23.cshtml)]

2. <span data-ttu-id="51f1a-253">執行應用程式，然後按一下 [**關於**] 連結。</span><span class="sxs-lookup"><span data-stu-id="51f1a-253">Run the app and click the **About** link.</span></span>

   <span data-ttu-id="51f1a-254">每個註冊日期的學生計數會顯示在表格中。</span><span class="sxs-lookup"><span data-stu-id="51f1a-254">The count of students for each enrollment date displays in a table.</span></span>

   ![About_page](sorting-filtering-and-paging-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image9.png)

## <a name="get-the-code"></a><span data-ttu-id="51f1a-256">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="51f1a-256">Get the code</span></span>

[<span data-ttu-id="51f1a-257">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="51f1a-257">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="51f1a-258">其他資源</span><span class="sxs-lookup"><span data-stu-id="51f1a-258">Additional resources</span></span>

<span data-ttu-id="51f1a-259">您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="51f1a-259">Links to other Entity Framework resources can be found in [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51f1a-260">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51f1a-260">Next steps</span></span>

<span data-ttu-id="51f1a-261">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="51f1a-261">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51f1a-262">新增資料行排序連結</span><span class="sxs-lookup"><span data-stu-id="51f1a-262">Add column sort links</span></span>
> * <span data-ttu-id="51f1a-263">新增 [搜尋] 方塊</span><span class="sxs-lookup"><span data-stu-id="51f1a-263">Add a Search box</span></span>
> * <span data-ttu-id="51f1a-264">新增分頁</span><span class="sxs-lookup"><span data-stu-id="51f1a-264">Add paging</span></span>
> * <span data-ttu-id="51f1a-265">建立 [關於] 頁面</span><span class="sxs-lookup"><span data-stu-id="51f1a-265">Create an About page</span></span>

<span data-ttu-id="51f1a-266">前往下一篇文章，以瞭解如何使用連線恢復功能和命令攔截。</span><span class="sxs-lookup"><span data-stu-id="51f1a-266">Advance to the next article to learn how to use connection resiliency and command interception.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="51f1a-267">連接恢復功能和命令攔截</span><span class="sxs-lookup"><span data-stu-id="51f1a-267">Connection resiliency and command interception</span></span>](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)
