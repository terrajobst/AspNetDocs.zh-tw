---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
title: 教學課程：瞭解 MVC 5 Web 應用程式的 advanced EF 案例
description: 本教學課程包含幾個實用的主題，當您超越開發使用 Entity Framework Code First 之 ASP.NET web 應用程式的基本概念時，會很有説明。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: f35a9b0c-49ef-4cde-b06d-19d1543feb0b
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/advanced-entity-framework-scenarios-for-an-mvc-web-application
msc.type: authoredcontent
ms.openlocfilehash: d7cc83a5b78a60f575f5c3065079679189296a0c
ms.sourcegitcommit: fe5c7512383a9b0a05d321ff10d3cca1611556f0
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 09/11/2019
ms.locfileid: "58425271"
---
# <a name="tutorial-learn-about-advanced-ef-scenarios-for-an-mvc-5-web-app"></a><span data-ttu-id="51579-103">教學課程：瞭解 MVC 5 Web 應用程式的 advanced EF 案例</span><span class="sxs-lookup"><span data-stu-id="51579-103">Tutorial: Learn about advanced EF Scenarios for an MVC 5 Web app</span></span>

<span data-ttu-id="51579-104">在上一個教學課程中，您已實作為每個階層的資料表繼承。</span><span class="sxs-lookup"><span data-stu-id="51579-104">In the previous tutorial you implemented table-per-hierarchy inheritance.</span></span> <span data-ttu-id="51579-105">本教學課程包含幾個實用的主題，當您超越開發使用 Entity Framework Code First 之 ASP.NET web 應用程式的基本概念時，會很有説明。</span><span class="sxs-lookup"><span data-stu-id="51579-105">This tutorial includes introduces several topics that are useful to be aware of when you go beyond the basics of developing ASP.NET web applications that use Entity Framework Code First.</span></span> <span data-ttu-id="51579-106">前幾節提供逐步指示，引導您逐步執行程式碼，並使用 Visual Studio 來完成工作。接下來的章節會引進數個主題，其中包含簡短的簡介，以及資源的連結以取得詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="51579-106">The first few sections have step-by-step instructions that walk you through the code and using Visual Studio to complete tasks The sections that follow introduce several topics with brief introductions followed by links to resources for more information.</span></span>

<span data-ttu-id="51579-107">在這些主題中，您將會使用您已建立的頁面。</span><span class="sxs-lookup"><span data-stu-id="51579-107">For most of these topics, you'll work with pages that you already created.</span></span> <span data-ttu-id="51579-108">若要使用原始 SQL 進行大量更新，您將會建立新的頁面，以更新資料庫中所有課程的信用額度數：</span><span class="sxs-lookup"><span data-stu-id="51579-108">To use raw SQL to do bulk updates you'll create a new page that updates the number of credits of all courses in the database:</span></span>

![Update_Course_Credits_initial_page](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="51579-110">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="51579-110">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51579-111">執行原始 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="51579-111">Perform raw SQL queries</span></span>
> * <span data-ttu-id="51579-112">執行沒有追蹤的查詢</span><span class="sxs-lookup"><span data-stu-id="51579-112">Perform no-tracking queries</span></span>
> * <span data-ttu-id="51579-113">檢查傳送至資料庫的 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="51579-113">Examine SQL queries sent to database</span></span>

<span data-ttu-id="51579-114">您也會瞭解：</span><span class="sxs-lookup"><span data-stu-id="51579-114">You also learn about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51579-115">建立抽象層</span><span class="sxs-lookup"><span data-stu-id="51579-115">Creating an abstraction layer</span></span>
> * <span data-ttu-id="51579-116">Proxy 類別</span><span class="sxs-lookup"><span data-stu-id="51579-116">Proxy classes</span></span>
> * <span data-ttu-id="51579-117">自動變更偵測</span><span class="sxs-lookup"><span data-stu-id="51579-117">Automatic change detection</span></span>
> * <span data-ttu-id="51579-118">自動驗證</span><span class="sxs-lookup"><span data-stu-id="51579-118">Automatic validation</span></span>
> * <span data-ttu-id="51579-119">Entity Framework 電源工具</span><span class="sxs-lookup"><span data-stu-id="51579-119">Entity Framework Power Tools</span></span>
> * <span data-ttu-id="51579-120">Entity Framework 原始碼</span><span class="sxs-lookup"><span data-stu-id="51579-120">Entity Framework source code</span></span>

## <a name="prerequisite"></a><span data-ttu-id="51579-121">必要條件</span><span class="sxs-lookup"><span data-stu-id="51579-121">Prerequisite</span></span>

* [<span data-ttu-id="51579-122">實作繼承</span><span class="sxs-lookup"><span data-stu-id="51579-122">Implementing Inheritance</span></span>](implementing-inheritance-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="perform-raw-sql-queries"></a><span data-ttu-id="51579-123">執行原始 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="51579-123">Perform raw SQL queries</span></span>

<span data-ttu-id="51579-124">Entity Framework Code First API 包括可讓您直接將 SQL 命令傳遞至資料庫的方法。</span><span class="sxs-lookup"><span data-stu-id="51579-124">The Entity Framework Code First API includes methods that enable you to pass SQL commands directly to the database.</span></span> <span data-ttu-id="51579-125">下列選項可供您選擇：</span><span class="sxs-lookup"><span data-stu-id="51579-125">You have the following options:</span></span>

- <span data-ttu-id="51579-126">針對傳回實體類型的查詢，請使用[DbSet. SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="51579-126">Use the [DbSet.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.dbset.sqlquery.aspx) method for queries that return entity types.</span></span> <span data-ttu-id="51579-127">傳回的物件必須是`DbSet`物件所預期的類型，而且資料庫內容會自動追蹤它們，除非您關閉追蹤。</span><span class="sxs-lookup"><span data-stu-id="51579-127">The returned objects must be of the type expected by the `DbSet` object, and they are automatically tracked by the database context unless you turn tracking off.</span></span> <span data-ttu-id="51579-128">（請參閱下一節中有關[AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx)方法的資訊）。</span><span class="sxs-lookup"><span data-stu-id="51579-128">(See the following section about the [AsNoTracking](https://msdn.microsoft.com/library/system.data.entity.dbextensions.asnotracking.aspx) method.)</span></span>
- <span data-ttu-id="51579-129">針對傳回不是實體之類型的查詢，請使用[SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="51579-129">Use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery.aspx) method for queries that return types that aren't entities.</span></span> <span data-ttu-id="51579-130">即使您使用這個方法來擷取實體類型，資料庫內容也不會追蹤傳回的資料。</span><span class="sxs-lookup"><span data-stu-id="51579-130">The returned data isn't tracked by the database context, even if you use this method to retrieve entity types.</span></span>
- <span data-ttu-id="51579-131">針對非查詢命令使用[ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="51579-131">Use the [Database.ExecuteSqlCommand](https://msdn.microsoft.com/library/gg679456.aspx) for non-query commands.</span></span>

<span data-ttu-id="51579-132">使用 Entity Framework 的優點之一，是它可避免將程式碼繫結至太接近儲存資料之特定方法的位置。</span><span class="sxs-lookup"><span data-stu-id="51579-132">One of the advantages of using the Entity Framework is that it avoids tying your code too closely to a particular method of storing data.</span></span> <span data-ttu-id="51579-133">它可透過產生 SQL 查詢和命令來達成此目的，同時這也可讓您不必自行撰寫。</span><span class="sxs-lookup"><span data-stu-id="51579-133">It does this by generating SQL queries and commands for you, which also frees you from having to write them yourself.</span></span> <span data-ttu-id="51579-134">但在某些情況下，您需要執行手動建立的特定 SQL 查詢，而且這些方法可以讓您處理這類例外狀況。</span><span class="sxs-lookup"><span data-stu-id="51579-134">But there are exceptional scenarios when you need to run specific SQL queries that you have manually created, and these methods make it possible for you to handle such exceptions.</span></span>

<span data-ttu-id="51579-135">如同在 Web 應用程式中執行 SQL 命令一樣，您必須採取一些預防措施，以保護您的網站免於遭受 SQL 插入式攻擊。</span><span class="sxs-lookup"><span data-stu-id="51579-135">As is always true when you execute SQL commands in a web application, you must take precautions to protect your site against SQL injection attacks.</span></span> <span data-ttu-id="51579-136">執行這項操作的方法之一是使用參數化查詢，以確定網頁所提交的字串無法解譯為 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="51579-136">One way to do that is to use parameterized queries to make sure that strings submitted by a web page can't be interpreted as SQL commands.</span></span> <span data-ttu-id="51579-137">在本教學課程中，您會在將使用者輸入整合到查詢時，使用參數化查詢。</span><span class="sxs-lookup"><span data-stu-id="51579-137">In this tutorial you'll use parameterized queries when integrating user input into a query.</span></span>

### <a name="calling-a-query-that-returns-entities"></a><span data-ttu-id="51579-138">呼叫傳回實體的查詢</span><span class="sxs-lookup"><span data-stu-id="51579-138">Calling a Query that Returns Entities</span></span>

<span data-ttu-id="51579-139">`TEntity` [ DbSet&lt; TEntity&gt; ](https://msdn.microsoft.com/library/gg696460.aspx)類別所提供的方法，可讓您用來執行傳回類型實體的查詢。</span><span class="sxs-lookup"><span data-stu-id="51579-139">The [DbSet&lt;TEntity&gt;](https://msdn.microsoft.com/library/gg696460.aspx) class provides a method that you can use to execute a query that returns an entity of type `TEntity`.</span></span> <span data-ttu-id="51579-140">若要查看其`Details` `Department`運作方式，您將變更控制器的方法中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="51579-140">To see how this works you'll change the code in the `Details` method of the `Department` controller.</span></span>

<span data-ttu-id="51579-141">在*DepartmentController.cs*的`Details` `db.Departments.SqlQuery`方法中，以方法呼叫取代方法呼叫，如下列反白顯示的程式碼所示：`db.Departments.FindAsync`</span><span class="sxs-lookup"><span data-stu-id="51579-141">In *DepartmentController.cs*, in the `Details` method, replace the `db.Departments.FindAsync` method call with a `db.Departments.SqlQuery` method call, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample1.cs?highlight=8-14)]

<span data-ttu-id="51579-142">若要確認新的程式碼運作正常，請選取 [部門] 索引標籤，然後針對其中一個部門選取 [詳細資料]。</span><span class="sxs-lookup"><span data-stu-id="51579-142">To verify that the new code works correctly, select the **Departments** tab and then **Details** for one of the departments.</span></span> <span data-ttu-id="51579-143">請確定所有資料都如預期般顯示。</span><span class="sxs-lookup"><span data-stu-id="51579-143">Make sure all of the data displays as expected.</span></span>

### <a name="calling-a-query-that-returns-other-types-of-objects"></a><span data-ttu-id="51579-144">呼叫傳回其他類型之物件的查詢</span><span class="sxs-lookup"><span data-stu-id="51579-144">Calling a Query that Returns Other Types of Objects</span></span>

<span data-ttu-id="51579-145">先前您已針對顯示每個註冊日期之學生數目的 About 頁面，建立學生統計資料方格。</span><span class="sxs-lookup"><span data-stu-id="51579-145">Earlier you created a student statistics grid for the About page that showed the number of students for each enrollment date.</span></span> <span data-ttu-id="51579-146">在*HomeController.cs*中執行此動作的程式碼會使用 LINQ：</span><span class="sxs-lookup"><span data-stu-id="51579-146">The code that does this in *HomeController.cs* uses LINQ:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample2.cs)]

<span data-ttu-id="51579-147">假設您想要撰寫程式碼，直接在 SQL 中抓取這項資料，而不是使用 LINQ。</span><span class="sxs-lookup"><span data-stu-id="51579-147">Suppose you want to write the code that retrieves this data directly in SQL rather than using LINQ.</span></span> <span data-ttu-id="51579-148">若要這麼做，您必須執行查詢來傳回實體物件以外的專案，這表示您需要使用[SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx)方法。</span><span class="sxs-lookup"><span data-stu-id="51579-148">To do that you need to run a query that returns something other than entity objects, which means you need to use the [Database.SqlQuery](https://msdn.microsoft.com/library/system.data.entity.database.sqlquery(v=VS.103).aspx) method.</span></span>

<span data-ttu-id="51579-149">在*HomeController.cs*中，以 SQL 語句取代`About`方法中的 LINQ 語句，如下列反白顯示的程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="51579-149">In *HomeController.cs*, replace the LINQ statement in the `About` method with a SQL statement, as shown in the following highlighted code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample3.cs?highlight=3-18)]

<span data-ttu-id="51579-150">執行 [關於] 頁面。</span><span class="sxs-lookup"><span data-stu-id="51579-150">Run the About page.</span></span> <span data-ttu-id="51579-151">確認它所顯示的資料與之前相同。</span><span class="sxs-lookup"><span data-stu-id="51579-151">Verify that it displays the same data it did before.</span></span>

### <a name="calling-an-update-query"></a><span data-ttu-id="51579-152">呼叫更新查詢</span><span class="sxs-lookup"><span data-stu-id="51579-152">Calling an Update Query</span></span>

<span data-ttu-id="51579-153">假設 Contoso 大學系統管理員想要能夠在資料庫中執行大量變更，例如變更每個課程的信用額度數。</span><span class="sxs-lookup"><span data-stu-id="51579-153">Suppose Contoso University administrators want to be able to perform bulk changes in the database, such as changing the number of credits for every course.</span></span> <span data-ttu-id="51579-154">如果該大學有大量的課程，擷取全部課程作為實體並個別進行變更的效率不佳。</span><span class="sxs-lookup"><span data-stu-id="51579-154">If the university has a large number of courses, it would be inefficient to retrieve them all as entities and change them individually.</span></span> <span data-ttu-id="51579-155">在本節中，您將會執行一個網頁，讓使用者指定一個因素來變更所有課程的信用額度數目，而您會藉由執行 SQL `UPDATE`語句來進行變更。</span><span class="sxs-lookup"><span data-stu-id="51579-155">In this section you'll implement a web page that enables the user to specify a factor by which to change the number of credits for all courses, and you'll make the change by executing a SQL `UPDATE` statement.</span></span> 

<span data-ttu-id="51579-156">在*CourseController.cs*中， `UpdateCourseCredits`新增和`HttpGet` `HttpPost`的方法：</span><span class="sxs-lookup"><span data-stu-id="51579-156">In *CourseController.cs*, add `UpdateCourseCredits` methods for `HttpGet` and `HttpPost`:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample4.cs)]

<span data-ttu-id="51579-157">當控制器處理`HttpGet`要求時， `ViewBag.RowsAffected`變數中不會傳回任何內容，而且此視圖會顯示空白的文字方塊和 [提交] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="51579-157">When the controller processes an `HttpGet` request, nothing is returned in the `ViewBag.RowsAffected` variable, and the view displays an empty text box and a submit button.</span></span>

<span data-ttu-id="51579-158">`multiplier` 按一下`HttpPost` [更新] 按鈕時，會呼叫方法，並在文字方塊中輸入值。</span><span class="sxs-lookup"><span data-stu-id="51579-158">When the **Update** button is clicked, the `HttpPost` method is called, and `multiplier` has the value entered in the text box.</span></span> <span data-ttu-id="51579-159">然後，程式碼會執行更新課程的 SQL，並將受影響的資料列數目傳回給`ViewBag.RowsAffected`變數中的 view。</span><span class="sxs-lookup"><span data-stu-id="51579-159">The code then executes the SQL that updates courses and returns the number of affected rows to the view in the `ViewBag.RowsAffected` variable.</span></span> <span data-ttu-id="51579-160">當 view 取得該變數中的值時，它會顯示已更新的資料列數目，而不是文字方塊和提交按鈕。</span><span class="sxs-lookup"><span data-stu-id="51579-160">When the view gets a value in that variable, it displays the number of rows updated instead of the text box and submit button.</span></span>

<span data-ttu-id="51579-161">在 [ *CourseController.cs*] 中，以滑鼠右鍵`UpdateCourseCredits`按一下其中一個方法，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="51579-161">In *CourseController.cs*, right-click one of the `UpdateCourseCredits` methods, and then click **Add View**.</span></span> <span data-ttu-id="51579-162">[**加入視圖**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="51579-162">The **Add View** dialog appears.</span></span> <span data-ttu-id="51579-163">保留預設值，然後選取 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="51579-163">Leave the defaults and select **Add**.</span></span>

<span data-ttu-id="51579-164">在*Views\Course\UpdateCourseCredits.cshtml*中，將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="51579-164">In *Views\Course\UpdateCourseCredits.cshtml*, replace the template code with the following code:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample5.cshtml)]

<span data-ttu-id="51579-165">藉由選取 [課程] 索引標籤，然後將 "/UpdateCourseCredits" 新增至瀏覽器位址列中的 URL 結尾 (例如：`http://localhost:50205/Course/UpdateCourseCredits`)，以執行 `UpdateCourseCredits` 方法。</span><span class="sxs-lookup"><span data-stu-id="51579-165">Run the `UpdateCourseCredits` method by selecting the **Courses** tab, then adding "/UpdateCourseCredits" to the end of the URL in the browser's address bar (for example: `http://localhost:50205/Course/UpdateCourseCredits`).</span></span> <span data-ttu-id="51579-166">在文字方塊中輸入數目：</span><span class="sxs-lookup"><span data-stu-id="51579-166">Enter a number in the text box:</span></span>

![Update_Course_Credits_initial_page_with_2_entered](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image1.png)

<span data-ttu-id="51579-168">按一下 [更新]。</span><span class="sxs-lookup"><span data-stu-id="51579-168">Click **Update**.</span></span> <span data-ttu-id="51579-169">您會看到受影響的資料列數目。</span><span class="sxs-lookup"><span data-stu-id="51579-169">You see the number of rows affected.</span></span>

<span data-ttu-id="51579-170">按一下 [回到清單]，以查看課程與已修訂學分數的清單。</span><span class="sxs-lookup"><span data-stu-id="51579-170">Click **Back to List** to see the list of courses with the revised number of credits.</span></span>

<span data-ttu-id="51579-171">如需原始 SQL 查詢的詳細資訊，請參閱 MSDN 上的[原始 Sql 查詢](https://msdn.microsoft.com/data/jj592907)。</span><span class="sxs-lookup"><span data-stu-id="51579-171">For more information about raw SQL queries, see [Raw SQL Queries](https://msdn.microsoft.com/data/jj592907) on MSDN.</span></span>

## <a name="no-tracking-queries"></a><span data-ttu-id="51579-172">無追蹤查詢</span><span class="sxs-lookup"><span data-stu-id="51579-172">No-tracking queries</span></span>

<span data-ttu-id="51579-173">當資料庫內容擷取資料表資料列並建立代表他們的實體物件時，根據預設，它會追蹤在記憶體中的實體是否與資料庫中的內容保持同步。</span><span class="sxs-lookup"><span data-stu-id="51579-173">When a database context retrieves table rows and creates entity objects that represent them, by default it keeps track of whether the entities in memory are in sync with what's in the database.</span></span> <span data-ttu-id="51579-174">記憶體中的資料所扮演的角色是一個快取，並會在您更新實體時使用。</span><span class="sxs-lookup"><span data-stu-id="51579-174">The data in memory acts as a cache and is used when you update an entity.</span></span> <span data-ttu-id="51579-175">這個快取通常在 Web 應用程式當中是不需要的，因為內容執行個體通常壽命都很短 (每次要求都會建立一個新的並進行處置)，並且通常讀取實體的內容都會在實體重新獲得利用前遭到處置。</span><span class="sxs-lookup"><span data-stu-id="51579-175">This caching is often unnecessary in a web application because context instances are typically short-lived (a new one is created and disposed for each request) and the context that reads an entity is typically disposed before that entity is used again.</span></span>

<span data-ttu-id="51579-176">您可以使用[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)方法，在記憶體中停用實體物件的追蹤。</span><span class="sxs-lookup"><span data-stu-id="51579-176">You can disable tracking of entity objects in memory by using the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method.</span></span> <span data-ttu-id="51579-177">您會想要進行這項操作的常見案例包括下列情況：</span><span class="sxs-lookup"><span data-stu-id="51579-177">Typical scenarios in which you might want to do that include the following:</span></span>

- <span data-ttu-id="51579-178">查詢會抓取關閉追蹤的大量資料，可能會明顯地提升效能。</span><span class="sxs-lookup"><span data-stu-id="51579-178">A query retrieves such a large volume of data that turning off tracking might noticeably enhance performance.</span></span>
- <span data-ttu-id="51579-179">您想要附加實體以進行更新，但您先前已針對不同目的抓取相同的實體。</span><span class="sxs-lookup"><span data-stu-id="51579-179">You want to attach an entity in order to update it, but you earlier retrieved the same entity for a different purpose.</span></span> <span data-ttu-id="51579-180">由於實體已由資料庫內容進行追蹤，您無法連結到您想要變更的實體。</span><span class="sxs-lookup"><span data-stu-id="51579-180">Because the entity is already being tracked by the database context, you can't attach the entity that you want to change.</span></span> <span data-ttu-id="51579-181">處理這種情況的其中一種方式是`AsNoTracking`使用選項搭配先前的查詢。</span><span class="sxs-lookup"><span data-stu-id="51579-181">One way to handle this situation is to use the `AsNoTracking` option with the earlier query.</span></span>

<span data-ttu-id="51579-182">如需示範如何使用[AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx)方法的範例，請參閱[本教學課程的先前版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md)。</span><span class="sxs-lookup"><span data-stu-id="51579-182">For an example that demonstrates how to use the [AsNoTracking](https://msdn.microsoft.com/library/gg679352(v=vs.103).aspx) method, see [the earlier version of this tutorial](../../older-versions/getting-started-with-ef-5-using-mvc-4/advanced-entity-framework-scenarios-for-an-mvc-web-application.md).</span></span> <span data-ttu-id="51579-183">這個版本的教學課程不會在 Edit 方法中的模型系結器建立的實體上設定修改過的旗標， `AsNoTracking`因此不需要。</span><span class="sxs-lookup"><span data-stu-id="51579-183">This version of the tutorial doesn't set the Modified flag on a model-binder-created entity in the Edit method, so it doesn't need `AsNoTracking`.</span></span>

## <a name="examine-sql-sent-to-database"></a><span data-ttu-id="51579-184">檢查傳送至資料庫的 SQL</span><span class="sxs-lookup"><span data-stu-id="51579-184">Examine SQL sent to database</span></span>

<span data-ttu-id="51579-185">有時能夠看到傳送至資料庫的實際 SQL 查詢很有幫助。</span><span class="sxs-lookup"><span data-stu-id="51579-185">Sometimes it's helpful to be able to see the actual SQL queries that are sent to the database.</span></span> <span data-ttu-id="51579-186">在先前的教學課程中，您已瞭解如何在攔截器程式碼中執行此動作;現在您會看到一些方法，而不需要撰寫攔截器程式碼。</span><span class="sxs-lookup"><span data-stu-id="51579-186">In an earlier tutorial you saw how to do that in interceptor code; now you'll see some ways to do it without writing interceptor code.</span></span> <span data-ttu-id="51579-187">若要試試看，您將會看到一個簡單的查詢，然後查看當您加入積極式載入、篩選和排序等選項時，會發生什麼事。</span><span class="sxs-lookup"><span data-stu-id="51579-187">To try this out, you'll look at a simple query and then look at what happens to it as you add options such eager loading, filtering, and sorting.</span></span>

<span data-ttu-id="51579-188">在 [*控制器/CourseController*] 中`Index` ，以下列程式碼取代方法，以暫時停止積極式載入：</span><span class="sxs-lookup"><span data-stu-id="51579-188">In *Controllers/CourseController*, replace the `Index` method with the following code, in order to temporarily stop eager loading:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample6.cs)]

<span data-ttu-id="51579-189">現在在`return`語句上設定中斷點（F9 的游標在該行上）。</span><span class="sxs-lookup"><span data-stu-id="51579-189">Now set a breakpoint on the `return` statement (F9 with the cursor on that line).</span></span> <span data-ttu-id="51579-190">按**F5**以在 [調試] 模式中執行專案，然後選取 [課程索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="51579-190">Press **F5** to run the project in debug mode, and select the Course Index page.</span></span> <span data-ttu-id="51579-191">當程式碼到達中斷點時，請檢查`sql`變數。</span><span class="sxs-lookup"><span data-stu-id="51579-191">When the code reaches the breakpoint, examine the `sql` variable.</span></span> <span data-ttu-id="51579-192">您會看到傳送至 SQL Server 的查詢。</span><span class="sxs-lookup"><span data-stu-id="51579-192">You see the query that's sent to SQL Server.</span></span> <span data-ttu-id="51579-193">這是一個簡單`Select`的語句。</span><span class="sxs-lookup"><span data-stu-id="51579-193">It's a simple `Select` statement.</span></span>

[!code-json[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample7.json)]

<span data-ttu-id="51579-194">按一下放大鏡以在**文字視覺化**中查看查詢。</span><span class="sxs-lookup"><span data-stu-id="51579-194">Click the magnifying glass to see the query in the **Text Visualizer**.</span></span>

![](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image10.png)

<span data-ttu-id="51579-195">現在您會將下拉式清單新增至 [課程] 索引頁面，讓使用者可以篩選特定部門。</span><span class="sxs-lookup"><span data-stu-id="51579-195">Now you'll add a drop-down list to the Courses Index page so that users can filter for a particular department.</span></span> <span data-ttu-id="51579-196">您將依標題排序課程，並針對`Department`導覽屬性指定積極式載入。</span><span class="sxs-lookup"><span data-stu-id="51579-196">You'll sort the courses by title, and you'll specify eager loading for the `Department` navigation property.</span></span>

<span data-ttu-id="51579-197">在*CourseController.cs*中，將`Index`方法取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="51579-197">In *CourseController.cs*, replace the `Index` method with the following code:</span></span>

[!code-csharp[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample8.cs)]

<span data-ttu-id="51579-198">還原`return`語句上的中斷點。</span><span class="sxs-lookup"><span data-stu-id="51579-198">Restore the breakpoint on the `return` statement.</span></span>

<span data-ttu-id="51579-199">方法會在`SelectedDepartment`參數中接收所選下拉式清單的值。</span><span class="sxs-lookup"><span data-stu-id="51579-199">The method receives the selected value of the drop-down list in the `SelectedDepartment` parameter.</span></span> <span data-ttu-id="51579-200">如果未選取任何內容，此參數將會是 null。</span><span class="sxs-lookup"><span data-stu-id="51579-200">If nothing is selected, this parameter will be null.</span></span>

<span data-ttu-id="51579-201">包含所有部門的集合會傳遞至下拉式清單的視圖。`SelectList`</span><span class="sxs-lookup"><span data-stu-id="51579-201">A `SelectList` collection containing all departments is passed to the view for the drop-down list.</span></span> <span data-ttu-id="51579-202">傳遞至此`SelectList`函式的參數會指定值功能變數名稱、文字功能變數名稱和選取的專案。</span><span class="sxs-lookup"><span data-stu-id="51579-202">The parameters passed to the `SelectList` constructor specify the value field name, the text field name, and the selected item.</span></span>

<span data-ttu-id="51579-203">針對存放`Get` `Course`庫的方法，程式碼會針對`Department`導覽屬性指定篩選條件運算式、排序次序和積極式載入。</span><span class="sxs-lookup"><span data-stu-id="51579-203">For the `Get` method of the `Course` repository, the code specifies a filter expression, a sort order, and eager loading for the `Department` navigation property.</span></span> <span data-ttu-id="51579-204">`true`如果下拉式清單中未選取任何內容（ `SelectedDepartment`亦即為 null），則篩選運算式一律會傳回。</span><span class="sxs-lookup"><span data-stu-id="51579-204">The filter expression always returns `true` if nothing is selected in the drop-down list (that is, `SelectedDepartment` is null).</span></span>

<span data-ttu-id="51579-205">在*Views\Course\Index.cshtml*中，于開頭`table`標記的正後方新增下列程式碼，以建立下拉式清單和提交按鈕：</span><span class="sxs-lookup"><span data-stu-id="51579-205">In *Views\Course\Index.cshtml*, immediately before the opening `table` tag, add the following code to create the drop-down list and a submit button:</span></span>

[!code-cshtml[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample9.cshtml)]

<span data-ttu-id="51579-206">在仍然設定中斷點的情況下，執行 [課程索引] 頁面。</span><span class="sxs-lookup"><span data-stu-id="51579-206">With the breakpoint still set, run the Course Index page.</span></span> <span data-ttu-id="51579-207">繼續執行程式碼第一次叫用中斷點時，讓頁面顯示在瀏覽器中。</span><span class="sxs-lookup"><span data-stu-id="51579-207">Continue through the first times that the code hits a breakpoint, so that the page is displayed in the browser.</span></span> <span data-ttu-id="51579-208">從下拉式清單中選取部門，然後按一下 [**篩選**]。</span><span class="sxs-lookup"><span data-stu-id="51579-208">Select a department from the drop-down list and click **Filter**.</span></span>

<span data-ttu-id="51579-209">這次，第一個中斷點將會是 [部門] 查詢的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="51579-209">This time the first breakpoint will be for the departments query for the drop-down list.</span></span> <span data-ttu-id="51579-210">在下一次程式`query`代碼到達中斷點時略過，並查看變數，以查看查詢的`Course`樣子。</span><span class="sxs-lookup"><span data-stu-id="51579-210">Skip that and view the `query` variable the next time the code reaches the breakpoint in order to see what the `Course` query now looks like.</span></span> <span data-ttu-id="51579-211">您會看到如下所示的內容：</span><span class="sxs-lookup"><span data-stu-id="51579-211">You'll see something like the following:</span></span>

[!code-sql[Main](advanced-entity-framework-scenarios-for-an-mvc-web-application/samples/sample10.sql)]

<span data-ttu-id="51579-212">您可以看到`JOIN`查詢現在是一種會載入`Department`資料`Course`以及資料的查詢，而且它包含`WHERE`子句。</span><span class="sxs-lookup"><span data-stu-id="51579-212">You can see that the query is now a `JOIN` query that loads `Department` data along with the `Course` data, and that it includes a `WHERE` clause.</span></span>

<span data-ttu-id="51579-213">移除這`var sql = courses.ToString()`一行。</span><span class="sxs-lookup"><span data-stu-id="51579-213">Remove the `var sql = courses.ToString()` line.</span></span>

## <a name="create-an-abstraction-layer"></a><span data-ttu-id="51579-214">建立抽象層</span><span class="sxs-lookup"><span data-stu-id="51579-214">Create an abstraction layer</span></span>

<span data-ttu-id="51579-215">許多開發人員撰寫程式碼以實作存放庫和工作單元模式，作為使用 Entity Framework 之程式碼周圍的包裝函式。</span><span class="sxs-lookup"><span data-stu-id="51579-215">Many developers write code to implement the repository and unit of work patterns as a wrapper around code that works with the Entity Framework.</span></span> <span data-ttu-id="51579-216">這些模式主要用來建立資料存取層和應用程式的商務邏輯層之間的抽象層。</span><span class="sxs-lookup"><span data-stu-id="51579-216">These patterns are intended to create an abstraction layer between the data access layer and the business logic layer of an application.</span></span> <span data-ttu-id="51579-217">實作這些模式可協助隔離您的應用程式與資料存放區中的變更，並可促進自動化單元測試或測試驅動開發 (TDD)。</span><span class="sxs-lookup"><span data-stu-id="51579-217">Implementing these patterns can help insulate your application from changes in the data store and can facilitate automated unit testing or test-driven development (TDD).</span></span> <span data-ttu-id="51579-218">不過，撰寫額外的程式碼來執行這些模式並不一定是使用 EF 之應用程式的最佳選擇，原因如下：</span><span class="sxs-lookup"><span data-stu-id="51579-218">However, writing additional code to implement these patterns is not always the best choice for applications that use EF, for several reasons:</span></span>

- <span data-ttu-id="51579-219">EF 內容類別本身會隔離您的程式碼與資料存放區特有的程式碼。</span><span class="sxs-lookup"><span data-stu-id="51579-219">The EF context class itself insulates your code from data-store-specific code.</span></span>
- <span data-ttu-id="51579-220">EF 內容類別可作為您使用 EF 進行之資料庫更新的工作單元類別。</span><span class="sxs-lookup"><span data-stu-id="51579-220">The EF context class can act as a unit-of-work class for database updates that you do using EF.</span></span>
- <span data-ttu-id="51579-221">Entity Framework 6 中引進的功能，可讓您更輕鬆地執行 TDD，而不需要撰寫存放庫程式碼。</span><span class="sxs-lookup"><span data-stu-id="51579-221">Features introduced in Entity Framework 6 make it easier to implement TDD without writing repository code.</span></span>

<span data-ttu-id="51579-222">如需如何執行儲存機制和工作單位模式的詳細資訊，請參閱[本教學課程系列的 Entity Framework 5 版本](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="51579-222">For more information about how to implement the repository and unit of work patterns, see [the Entity Framework 5 version of this tutorial series](../../older-versions/getting-started-with-ef-5-using-mvc-4/implementing-the-repository-and-unit-of-work-patterns-in-an-asp-net-mvc-application.md).</span></span> <span data-ttu-id="51579-223">如需在 Entity Framework 6 中執行 TDD 之方式的詳細資訊，請參閱下列資源：</span><span class="sxs-lookup"><span data-stu-id="51579-223">For information about ways to implement TDD in Entity Framework 6, see the following resources:</span></span>

- [<span data-ttu-id="51579-224">EF6 如何更輕鬆地啟用模擬 DbSets</span><span class="sxs-lookup"><span data-stu-id="51579-224">How EF6 Enables Mocking DbSets more easily</span></span>](http://thedatafarm.com/data-access/how-ef6-enables-mocking-dbsets-more-easily/)
- [<span data-ttu-id="51579-225">使用模擬架構進行測試</span><span class="sxs-lookup"><span data-stu-id="51579-225">Testing with a mocking framework</span></span>](https://msdn.microsoft.com/data/dn314429)
- [<span data-ttu-id="51579-226">使用您自己的測試進行測試雙精度浮點數</span><span class="sxs-lookup"><span data-stu-id="51579-226">Testing with your own test doubles</span></span>](https://msdn.microsoft.com/data/dn314431)

<a id="proxies"></a>

## <a name="proxy-classes"></a><span data-ttu-id="51579-227">Proxy 類別</span><span class="sxs-lookup"><span data-stu-id="51579-227">Proxy classes</span></span>

<span data-ttu-id="51579-228">當 Entity Framework 建立實體實例時（例如，當您執行查詢時），通常會將其建立為動態產生之衍生型別的實例，作為實體的 proxy。</span><span class="sxs-lookup"><span data-stu-id="51579-228">When the Entity Framework creates entity instances (for example, when you execute a query), it often creates them as instances of a dynamically generated derived type that acts as a proxy for the entity.</span></span> <span data-ttu-id="51579-229">例如，請參閱下列兩個偵錯工具映射。</span><span class="sxs-lookup"><span data-stu-id="51579-229">For example, see the following two debugger images.</span></span> <span data-ttu-id="51579-230">在第一個影像中，您會在`student`具現化實體`Student`後立即看到變數是預期的類型。</span><span class="sxs-lookup"><span data-stu-id="51579-230">In the first image, you see that the `student` variable is the expected `Student` type immediately after you instantiate the entity.</span></span> <span data-ttu-id="51579-231">在第二個影像中，使用 EF 從資料庫讀取 student 實體之後，您會看到 proxy 類別。</span><span class="sxs-lookup"><span data-stu-id="51579-231">In the second image, after EF has been used to read a student entity from the database, you see the proxy class.</span></span>

![在 proxy 類別之前](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image12.png)

![Proxy 類別之後](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image13.png)

<span data-ttu-id="51579-234">此 proxy 類別會覆寫實體的某些虛擬屬性，以插入在存取屬性時自動執行動作的勾點。</span><span class="sxs-lookup"><span data-stu-id="51579-234">This proxy class overrides some virtual properties of the entity to insert hooks for performing actions automatically when the property is accessed.</span></span> <span data-ttu-id="51579-235">此機制用於的一個函式是消極式載入。</span><span class="sxs-lookup"><span data-stu-id="51579-235">One function this mechanism is used for is lazy loading.</span></span>

<span data-ttu-id="51579-236">在大部分的情況下，您不需要知道此 proxy 的使用方式，但有一些例外狀況：</span><span class="sxs-lookup"><span data-stu-id="51579-236">Most of the time you don't need to be aware of this use of proxies, but there are exceptions:</span></span>

- <span data-ttu-id="51579-237">在某些情況下，您可能會想要防止 Entity Framework 建立 proxy 實例。</span><span class="sxs-lookup"><span data-stu-id="51579-237">In some scenarios you might want to prevent the Entity Framework from creating proxy instances.</span></span> <span data-ttu-id="51579-238">例如，當您將實體序列化時，您通常會想要有 POCO 類別，而不是 proxy 類別。</span><span class="sxs-lookup"><span data-stu-id="51579-238">For example, when you're serializing entities you generally want the POCO classes, not the proxy classes.</span></span> <span data-ttu-id="51579-239">避免序列化問題的其中一種方法是序列化資料傳輸物件（Dto），而不是實體物件，如[使用 WEB API 與 Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md)教學課程中所示。</span><span class="sxs-lookup"><span data-stu-id="51579-239">One way to avoid serialization problems is to serialize data transfer objects (DTOs) instead of entity objects, as shown in the [Using Web API with Entity Framework](../../../../web-api/overview/data/using-web-api-with-entity-framework/part-1.md) tutorial.</span></span> <span data-ttu-id="51579-240">另一種方式是[停用 proxy 建立](https://msdn.microsoft.com/data/jj592886.aspx)。</span><span class="sxs-lookup"><span data-stu-id="51579-240">Another way is to [disable proxy creation](https://msdn.microsoft.com/data/jj592886.aspx).</span></span>
- <span data-ttu-id="51579-241">當您使用`new`運算子來具現化實體類別時，您不會取得 proxy 實例。</span><span class="sxs-lookup"><span data-stu-id="51579-241">When you instantiate an entity class using the `new` operator, you don't get a proxy instance.</span></span> <span data-ttu-id="51579-242">這表示您不會取得延遲載入和自動變更追蹤之類的功能。</span><span class="sxs-lookup"><span data-stu-id="51579-242">This means you don't get functionality such as lazy loading and automatic change tracking.</span></span> <span data-ttu-id="51579-243">這通常沒什麼問題;您通常不需要消極式載入，因為您正在建立不在資料庫中的新實體，而且如果您將實體明確標示為`Added`，則通常不需要變更追蹤。</span><span class="sxs-lookup"><span data-stu-id="51579-243">This is typically okay; you generally don't need lazy loading, because you're creating a new entity that isn't in the database, and you generally don't need change tracking if you're explicitly marking the entity as `Added`.</span></span> <span data-ttu-id="51579-244">不過，如果您需要消極式載入，而且需要變更追蹤，您可以使用`DbSet`類別的[create](https://msdn.microsoft.com/library/gg679504.aspx)方法來建立具有 proxy 的新實體實例。</span><span class="sxs-lookup"><span data-stu-id="51579-244">However, if you do need lazy loading and you need change tracking, you can create new entity instances with proxies using the [Create](https://msdn.microsoft.com/library/gg679504.aspx) method of the `DbSet` class.</span></span>
- <span data-ttu-id="51579-245">您可能想要從 proxy 類型取得實際的實體類型。</span><span class="sxs-lookup"><span data-stu-id="51579-245">You might want to get an actual entity type from a proxy type.</span></span> <span data-ttu-id="51579-246">您可以使用`ObjectContext`類別的[GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx)方法來取得 proxy 類型實例的實際實體類型。</span><span class="sxs-lookup"><span data-stu-id="51579-246">You can use the [GetObjectType](https://msdn.microsoft.com/library/system.data.objects.objectcontext.getobjecttype.aspx) method of the `ObjectContext` class to get the actual entity type of a proxy type instance.</span></span>

<span data-ttu-id="51579-247">如需詳細資訊，請參閱 MSDN 上[的](https://msdn.microsoft.com/data/JJ592886.aspx)使用 proxy。</span><span class="sxs-lookup"><span data-stu-id="51579-247">For more information, see [Working with Proxies](https://msdn.microsoft.com/data/JJ592886.aspx) on MSDN.</span></span>

## <a name="automatic-change-detection"></a><span data-ttu-id="51579-248">自動變更偵測</span><span class="sxs-lookup"><span data-stu-id="51579-248">Automatic change detection</span></span>

<span data-ttu-id="51579-249">Entity Framework 藉由比較實體的目前值與原始值，判斷實體如何變更 (以及因此需要將哪些更新傳送至資料庫)。</span><span class="sxs-lookup"><span data-stu-id="51579-249">The Entity Framework determines how an entity has changed (and therefore which updates need to be sent to the database) by comparing the current values of an entity with the original values.</span></span> <span data-ttu-id="51579-250">查詢或附加實體時，會儲存原始值。</span><span class="sxs-lookup"><span data-stu-id="51579-250">The original values are stored when the entity is queried or attached.</span></span> <span data-ttu-id="51579-251">會導致自動變更偵測的一些方法如下：</span><span class="sxs-lookup"><span data-stu-id="51579-251">Some of the methods that cause automatic change detection are the following:</span></span>

- `DbSet.Find`
- `DbSet.Local`
- `DbSet.Remove`
- `DbSet.Add`
- `DbSet.Attach`
- `DbContext.SaveChanges`
- `DbContext.GetValidationErrors`
- `DbContext.Entry`
- `DbChangeTracker.Entries`

<span data-ttu-id="51579-252">如果您要追蹤大量實體，並在迴圈中多次呼叫其中一種方法，您可以使用[AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx)屬性暫時關閉自動變更偵測，以獲得顯著的效能改進。</span><span class="sxs-lookup"><span data-stu-id="51579-252">If you're tracking a large number of entities and you call one of these methods many times in a loop, you might get significant performance improvements by temporarily turning off automatic change detection using the [AutoDetectChangesEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.autodetectchangesenabled.aspx) property.</span></span> <span data-ttu-id="51579-253">如需詳細資訊，請參閱 MSDN 上的[自動偵測變更](https://msdn.microsoft.com/data/jj556205)。</span><span class="sxs-lookup"><span data-stu-id="51579-253">For more information, see [Automatically Detecting Changes](https://msdn.microsoft.com/data/jj556205) on MSDN.</span></span>

## <a name="automatic-validation"></a><span data-ttu-id="51579-254">自動驗證</span><span class="sxs-lookup"><span data-stu-id="51579-254">Automatic validation</span></span>

<span data-ttu-id="51579-255">當您呼叫`SaveChanges`方法時，根據預設，Entity Framework 會在更新資料庫之前，先驗證所有已變更實體的所有屬性中的資料。</span><span class="sxs-lookup"><span data-stu-id="51579-255">When you call the `SaveChanges` method, by default the Entity Framework validates the data in all properties of all changed entities before updating the database.</span></span> <span data-ttu-id="51579-256">如果您已更新大量實體，而且您已經驗證過資料，這是不必要的工作，而且您可以暫時關閉驗證，讓儲存變更的程式更少時間。</span><span class="sxs-lookup"><span data-stu-id="51579-256">If you've updated a large number of entities and you've already validated the data, this work is unnecessary and you could make the process of saving the changes take less time by temporarily turning off validation.</span></span> <span data-ttu-id="51579-257">您可以使用[ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx)屬性來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="51579-257">You can do that using the [ValidateOnSaveEnabled](https://msdn.microsoft.com/library/system.data.entity.infrastructure.dbcontextconfiguration.validateonsaveenabled.aspx) property.</span></span> <span data-ttu-id="51579-258">如需詳細資訊，請參閱 MSDN 上的[驗證](https://msdn.microsoft.com/data/gg193959)。</span><span class="sxs-lookup"><span data-stu-id="51579-258">For more information, see [Validation](https://msdn.microsoft.com/data/gg193959) on MSDN.</span></span>

## <a name="entity-framework-power-tools"></a><span data-ttu-id="51579-259">Entity Framework 電源工具</span><span class="sxs-lookup"><span data-stu-id="51579-259">Entity Framework Power Tools</span></span>

<span data-ttu-id="51579-260">[Entity Framework Power](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) tool 是用來建立這些教學課程中所顯示之資料模型圖表的 Visual Studio 增益集。</span><span class="sxs-lookup"><span data-stu-id="51579-260">[Entity Framework Power Tools](https://marketplace.visualstudio.com/items?itemName=ErikEJ.EntityFramework6PowerToolsCommunityEdition) is a Visual Studio add-in that was used to create the data model diagrams shown in these tutorials.</span></span> <span data-ttu-id="51579-261">這些工具也可以執行其他功能，例如根據現有資料庫中的資料表產生實體類別，讓您可以將資料庫與 Code First 搭配使用。</span><span class="sxs-lookup"><span data-stu-id="51579-261">The tools can also do other function such as generate entity classes based on the tables in an existing database so that you can use the database with Code First.</span></span> <span data-ttu-id="51579-262">安裝工具之後，內容功能表中會出現一些額外的選項。</span><span class="sxs-lookup"><span data-stu-id="51579-262">After you install the tools, some additional options appear in context menus.</span></span> <span data-ttu-id="51579-263">例如，當您以滑鼠右鍵按一下**方案總管**中的內容類別時，就會看到並**Entity Framework**選項。</span><span class="sxs-lookup"><span data-stu-id="51579-263">For example, when you right-click your context class in **Solution Explorer**, you see and **Entity Framework** option.</span></span> <span data-ttu-id="51579-264">這讓您能夠產生圖表。</span><span class="sxs-lookup"><span data-stu-id="51579-264">This gives you the ability to generate a diagram.</span></span> <span data-ttu-id="51579-265">當您使用 Code First 無法變更圖表中的資料模型，但您可以四處移動，讓它更容易瞭解。</span><span class="sxs-lookup"><span data-stu-id="51579-265">When you're using Code First you can't change the data model in the diagram, but you can move things around to make it easier to understand.</span></span>

![EF 圖表](advanced-entity-framework-scenarios-for-an-mvc-web-application/_static/image15.png)

## <a name="entity-framework-source-code"></a><span data-ttu-id="51579-267">Entity Framework 原始碼</span><span class="sxs-lookup"><span data-stu-id="51579-267">Entity Framework source code</span></span>

<span data-ttu-id="51579-268">Entity Framework 6 的原始程式碼可從[GitHub](https://github.com/aspnet/EntityFramework6)取得。</span><span class="sxs-lookup"><span data-stu-id="51579-268">The source code for Entity Framework 6 is available at [GitHub](https://github.com/aspnet/EntityFramework6).</span></span> <span data-ttu-id="51579-269">您可以提出 bug，而您可以為 EF 原始程式碼貢獻自己的增強功能。</span><span class="sxs-lookup"><span data-stu-id="51579-269">You can file bugs, and you can contribute your own enhancements to the EF source code.</span></span>

<span data-ttu-id="51579-270">雖然原始程式碼已開放，但 Entity Framework 完全支援做為 Microsoft 產品。</span><span class="sxs-lookup"><span data-stu-id="51579-270">Although the source code is open, Entity Framework is fully supported as a Microsoft product.</span></span> <span data-ttu-id="51579-271">Microsoft Entity Framework 小組將控制接受哪些貢獻，並測試所有的程式碼變更以確保每次發行的品質。</span><span class="sxs-lookup"><span data-stu-id="51579-271">The Microsoft Entity Framework team keeps control over which contributions are accepted and tests all code changes to ensure the quality of each release.</span></span>

## <a name="acknowledgments"></a><span data-ttu-id="51579-272">感謝</span><span class="sxs-lookup"><span data-stu-id="51579-272">Acknowledgments</span></span>

- <span data-ttu-id="51579-273">Tom 作者: dykstra 寫了本教學課程的原始版本，共同撰寫了 EF 5 更新，並撰寫了 EF 6 更新。</span><span class="sxs-lookup"><span data-stu-id="51579-273">Tom Dykstra wrote the original version of this tutorial, co-authored the EF 5 update, and wrote the EF 6 update.</span></span> <span data-ttu-id="51579-274">Tom 是 Microsoft Web Platform 和 Tools 內容小組的資深程式設計作者。</span><span class="sxs-lookup"><span data-stu-id="51579-274">Tom is a senior programming writer on the Microsoft Web Platform and Tools Content Team.</span></span>
- <span data-ttu-id="51579-275">[Rick Anderson](https://blogs.msdn.com/b/rickandy/)（twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)）大部分的工作都是更新 ef 5 和 MVC 4 的教學課程，並共同撰寫 ef 6 更新。</span><span class="sxs-lookup"><span data-stu-id="51579-275">[Rick Anderson](https://blogs.msdn.com/b/rickandy/) (twitter [@RickAndMSFT](http://twitter.com/RickAndMSFT)) did most of the work updating the tutorial for EF 5 and MVC 4 and co-authored the EF 6 update.</span></span> <span data-ttu-id="51579-276">Rick 是 Microsoft 的資深程式設計作者，著重于 Azure 和 MVC。</span><span class="sxs-lookup"><span data-stu-id="51579-276">Rick is a senior programming writer for Microsoft focusing on Azure and MVC.</span></span>
- <span data-ttu-id="51579-277">[Rowan 莎莎](http://www.romiller.com)和 Entity Framework 小組的其他成員可協助進行程式碼審核，並説明您在更新 ef 5 和 ef 6 教學課程時所出現的許多遷移問題。</span><span class="sxs-lookup"><span data-stu-id="51579-277">[Rowan Miller](http://www.romiller.com) and other members of the Entity Framework team assisted with code reviews and helped debug many issues with migrations that arose while we were updating the tutorial for EF 5 and EF 6.</span></span>

## <a name="troubleshoot-common-errors"></a><span data-ttu-id="51579-278">針對常見錯誤進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="51579-278">Troubleshoot common errors</span></span>

### <a name="cannot-createshadow-copy"></a><span data-ttu-id="51579-279">無法建立/陰影複製</span><span class="sxs-lookup"><span data-stu-id="51579-279">Cannot create/shadow copy</span></span>

<span data-ttu-id="51579-280">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="51579-280">Error Message:</span></span>

> <span data-ttu-id="51579-281">當檔案已存在時，&lt;無法&gt;建立/陰影複製 ' filename '。</span><span class="sxs-lookup"><span data-stu-id="51579-281">Cannot create/shadow copy '&lt;filename&gt;' when that file already exists.</span></span>

<span data-ttu-id="51579-282">方案</span><span class="sxs-lookup"><span data-stu-id="51579-282">Solution</span></span>

<span data-ttu-id="51579-283">等候幾秒鐘，然後重新整理頁面。</span><span class="sxs-lookup"><span data-stu-id="51579-283">Wait a few seconds and refresh the page.</span></span>

### <a name="update-database-not-recognized"></a><span data-ttu-id="51579-284">更新-無法辨識資料庫</span><span class="sxs-lookup"><span data-stu-id="51579-284">Update-Database not recognized</span></span>

<span data-ttu-id="51579-285">錯誤訊息（來自 PMC `Update-Database`中的命令）：</span><span class="sxs-lookup"><span data-stu-id="51579-285">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="51579-286">「更新-資料庫」一詞無法辨識為 Cmdlet、函式、指令檔或可運作程式的名稱。</span><span class="sxs-lookup"><span data-stu-id="51579-286">The term 'Update-Database' is not recognized as the name of a cmdlet, function, script file, or operable program.</span></span> <span data-ttu-id="51579-287">請檢查名稱的拼寫，或如果已包含路徑，請確認路徑正確，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="51579-287">Check the spelling of the name, or if a path was included, verify that the path is correct and try again.</span></span>

<span data-ttu-id="51579-288">方案</span><span class="sxs-lookup"><span data-stu-id="51579-288">Solution</span></span>

<span data-ttu-id="51579-289">結束 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="51579-289">Exit Visual Studio.</span></span> <span data-ttu-id="51579-290">重新開啟專案，然後再試一次。</span><span class="sxs-lookup"><span data-stu-id="51579-290">Reopen project and try again.</span></span>

### <a name="validation-failed"></a><span data-ttu-id="51579-291">驗證失敗</span><span class="sxs-lookup"><span data-stu-id="51579-291">Validation failed</span></span>

<span data-ttu-id="51579-292">錯誤訊息（來自 PMC `Update-Database`中的命令）：</span><span class="sxs-lookup"><span data-stu-id="51579-292">Error Message (from the `Update-Database` command in the PMC):</span></span>

> <span data-ttu-id="51579-293">一或多個實體的驗證失敗。</span><span class="sxs-lookup"><span data-stu-id="51579-293">Validation failed for one or more entities.</span></span> <span data-ttu-id="51579-294">如需詳細資訊，請參閱 ' EntityValidationErrors ' 屬性。</span><span class="sxs-lookup"><span data-stu-id="51579-294">See 'EntityValidationErrors' property for more details.</span></span>

<span data-ttu-id="51579-295">方案</span><span class="sxs-lookup"><span data-stu-id="51579-295">Solution</span></span>

<span data-ttu-id="51579-296">此問題的其中一個原因是`Seed`方法執行時的驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="51579-296">One cause of this problem is validation errors when the `Seed` method runs.</span></span> <span data-ttu-id="51579-297">如需有關偵測`Seed`方法的秘訣，請參閱植入[和偵錯工具 Entity Framework （EF） db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="51579-297">See [Seeding and Debugging Entity Framework (EF) DBs](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) for tips on debugging the `Seed` method.</span></span>

### <a name="http-50019-error"></a><span data-ttu-id="51579-298">HTTP 500.19 錯誤</span><span class="sxs-lookup"><span data-stu-id="51579-298">HTTP 500.19 error</span></span>

<span data-ttu-id="51579-299">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="51579-299">Error Message:</span></span>

> <span data-ttu-id="51579-300">HTTP 錯誤 500.19-內部伺服器錯誤：無法存取要求的網頁，因為該頁面的相關設定資料無效。</span><span class="sxs-lookup"><span data-stu-id="51579-300">HTTP Error 500.19 - Internal Server Error The requested page cannot be accessed because the related configuration data for the page is invalid.</span></span>

<span data-ttu-id="51579-301">方案</span><span class="sxs-lookup"><span data-stu-id="51579-301">Solution</span></span>

<span data-ttu-id="51579-302">您可以取得此錯誤的其中一種方式是，使用相同的埠號碼，讓解決方案有多個複本。</span><span class="sxs-lookup"><span data-stu-id="51579-302">One way you can get this error is from having multiple copies of the solution, each of them using the same port number.</span></span> <span data-ttu-id="51579-303">您通常可以藉由結束 Visual Studio 的所有實例，然後重新開機您正在處理的專案，來解決此問題。</span><span class="sxs-lookup"><span data-stu-id="51579-303">You can usually solve this problem by exiting all instances of Visual Studio, then restarting the project you're working on.</span></span> <span data-ttu-id="51579-304">如果無法解決問題，請嘗試變更埠號碼。</span><span class="sxs-lookup"><span data-stu-id="51579-304">If that doesn't work, try changing the port number.</span></span> <span data-ttu-id="51579-305">以滑鼠右鍵按一下專案檔，然後按一下 [屬性]。</span><span class="sxs-lookup"><span data-stu-id="51579-305">Right click on the project file and then click properties.</span></span> <span data-ttu-id="51579-306">選取 [ **Web** ] 索引標籤，然後在 [**專案 Url** ] 文字方塊中變更埠號碼。</span><span class="sxs-lookup"><span data-stu-id="51579-306">Select the **Web** tab and then change the port number in the **Project Url** text box.</span></span>

### <a name="error-locating-sql-server-instance"></a><span data-ttu-id="51579-307">搜尋 SQL Server 執行個體時發生錯誤</span><span class="sxs-lookup"><span data-stu-id="51579-307">Error locating SQL Server instance</span></span>

<span data-ttu-id="51579-308">錯誤訊息：</span><span class="sxs-lookup"><span data-stu-id="51579-308">Error Message:</span></span>

> <span data-ttu-id="51579-309">建立與 SQL Server　的連線時，發生與網路相關的錯誤或是執行個體特有的錯誤。</span><span class="sxs-lookup"><span data-stu-id="51579-309">A network-related or instance-specific error occurred while establishing a connection to SQL Server.</span></span> <span data-ttu-id="51579-310">找不到或無法存取伺服器。</span><span class="sxs-lookup"><span data-stu-id="51579-310">The server was not found or was not accessible.</span></span> <span data-ttu-id="51579-311">確認執行個名稱是否正確，以及 SQL Server 是否設定為允許遠端連線</span><span class="sxs-lookup"><span data-stu-id="51579-311">Verify that the instance name is correct and that SQL Server is configured to allow remote connections.</span></span> <span data-ttu-id="51579-312">(提供者：SQL 網路介面，錯誤：26 - 尋找指定的伺服器/執行個體時發生錯誤)</span><span class="sxs-lookup"><span data-stu-id="51579-312">(provider: SQL Network Interfaces, error: 26 - Error Locating Server/Instance Specified)</span></span>

<span data-ttu-id="51579-313">方案</span><span class="sxs-lookup"><span data-stu-id="51579-313">Solution</span></span>

<span data-ttu-id="51579-314">檢查連接字串。</span><span class="sxs-lookup"><span data-stu-id="51579-314">Check the connection string.</span></span> <span data-ttu-id="51579-315">如果您已手動刪除資料庫，請在結構字串中變更資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="51579-315">If you have manually deleted the database, change the name of the database in the construction string.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="51579-316">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="51579-316">Get the code</span></span>

[<span data-ttu-id="51579-317">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="51579-317">Download Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="51579-318">其他資源</span><span class="sxs-lookup"><span data-stu-id="51579-318">Additional resources</span></span>

 <span data-ttu-id="51579-319">如需如何使用 Entity Framework 來處理資料的詳細資訊，請參閱[MSDN 上的 EF 檔頁面](https://msdn.microsoft.com/data/ee712907)和[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="51579-319">For more information about how to work with data using the Entity Framework, see the [EF documentation page on MSDN](https://msdn.microsoft.com/data/ee712907) and [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

<span data-ttu-id="51579-320">如需有關如何在建立 web 應用程式之後部署它的詳細資訊，請參閱 MSDN Library 中的[ASP.NET Web 部署-建議的資源](../../../../whitepapers/aspnet-web-deployment-content-map.md)。</span><span class="sxs-lookup"><span data-stu-id="51579-320">For more information about how to deploy your web application after you've built it, see [ASP.NET Web Deployment - Recommended Resources](../../../../whitepapers/aspnet-web-deployment-content-map.md) in the MSDN Library.</span></span>

<span data-ttu-id="51579-321">如需與 MVC 相關之其他主題（例如驗證和授權）的詳細資訊，請參閱[ASP.NET Mvc 建議的資源](../recommended-resources-for-mvc.md)。</span><span class="sxs-lookup"><span data-stu-id="51579-321">For information about other topics related to MVC, such as authentication and authorization, see the [ASP.NET MVC - Recommended Resources](../recommended-resources-for-mvc.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="51579-322">後續步驟</span><span class="sxs-lookup"><span data-stu-id="51579-322">Next steps</span></span>

<span data-ttu-id="51579-323">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="51579-323">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51579-324">執行原始 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="51579-324">Performed raw SQL queries</span></span>
> * <span data-ttu-id="51579-325">未執行任何追蹤查詢</span><span class="sxs-lookup"><span data-stu-id="51579-325">Performed no-tracking queries</span></span>
> * <span data-ttu-id="51579-326">已檢查傳送至資料庫的 SQL 查詢</span><span class="sxs-lookup"><span data-stu-id="51579-326">Examined SQL queries sent to the database</span></span>

<span data-ttu-id="51579-327">您也瞭解到：</span><span class="sxs-lookup"><span data-stu-id="51579-327">You also learned about:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="51579-328">建立抽象層</span><span class="sxs-lookup"><span data-stu-id="51579-328">Creating an abstraction layer</span></span>
> * <span data-ttu-id="51579-329">Proxy 類別</span><span class="sxs-lookup"><span data-stu-id="51579-329">Proxy classes</span></span>
> * <span data-ttu-id="51579-330">自動變更偵測</span><span class="sxs-lookup"><span data-stu-id="51579-330">Automatic change detection</span></span>
> * <span data-ttu-id="51579-331">自動驗證</span><span class="sxs-lookup"><span data-stu-id="51579-331">Automatic validation</span></span>
> * <span data-ttu-id="51579-332">Entity Framework 電源工具</span><span class="sxs-lookup"><span data-stu-id="51579-332">Entity Framework Power Tools</span></span>
> * <span data-ttu-id="51579-333">Entity Framework 原始碼</span><span class="sxs-lookup"><span data-stu-id="51579-333">Entity Framework source code</span></span>

<span data-ttu-id="51579-334">這會完成這一系列的教學課程，以在 ASP.NET MVC 應用程式中使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="51579-334">This completes this series of tutorials on using the Entity Framework in an ASP.NET MVC application.</span></span> <span data-ttu-id="51579-335">如果您想要瞭解 EF Database First，請參閱資料庫第一個教學課程系列。</span><span class="sxs-lookup"><span data-stu-id="51579-335">If you want to learn about EF Database First, see the DB First tutorial series.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="51579-336">Entity Framework Database First</span><span class="sxs-lookup"><span data-stu-id="51579-336">Entity Framework Database First</span></span>](../database-first-development/setting-up-database.md)