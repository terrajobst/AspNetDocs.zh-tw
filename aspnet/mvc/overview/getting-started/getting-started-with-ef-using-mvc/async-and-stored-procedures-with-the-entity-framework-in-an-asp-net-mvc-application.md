---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中搭配使用非同步和預存程式與 EF
description: 在本教學課程中，您會瞭解如何執行非同步程式設計模型，並瞭解如何使用預存程式。
author: tdykstra
ms.author: riande
ms.date: 01/18/2019
ms.topic: tutorial
ms.assetid: 27d110fc-d1b7-4628-a763-26f1e6087549
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 5612f2f25d06feb904a205505ed8f048d2263266
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583437"
---
# <a name="tutorial-use-async-and-stored-procedures-with-ef-in-an-aspnet-mvc-app"></a><span data-ttu-id="bb145-103">教學課程：在 ASP.NET MVC 應用程式中搭配使用非同步和預存程式與 EF</span><span class="sxs-lookup"><span data-stu-id="bb145-103">Tutorial: Use async and stored procedures with EF in an ASP.NET MVC App</span></span>

<span data-ttu-id="bb145-104">在先前的教學課程中，您已瞭解如何使用同步程式設計模型來讀取和更新資料。</span><span class="sxs-lookup"><span data-stu-id="bb145-104">In earlier tutorials you learned how to read and update data using the synchronous programming model.</span></span> <span data-ttu-id="bb145-105">在本教學課程中，您會瞭解如何執行非同步程式設計模型。</span><span class="sxs-lookup"><span data-stu-id="bb145-105">In this tutorial you see how to implement the asynchronous programming model.</span></span> <span data-ttu-id="bb145-106">非同步程式碼可以協助應用程式的執行效果更好，因為它會更有效地使用伺服器資源。</span><span class="sxs-lookup"><span data-stu-id="bb145-106">Asynchronous code can help an application perform better because it makes better use of server resources.</span></span>

<span data-ttu-id="bb145-107">在本教學課程中，您也會瞭解如何在實體上使用預存程式進行插入、更新和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="bb145-107">In this tutorial you also see how to use stored procedures for insert, update, and delete operations on an entity.</span></span>

<span data-ttu-id="bb145-108">最後，您會將應用程式重新部署至 Azure，以及您在第一次部署之後所執行的所有資料庫變更。</span><span class="sxs-lookup"><span data-stu-id="bb145-108">Finally, you redeploy the application to Azure, along with all of the database changes that you've implemented since the first time you deployed.</span></span>

<span data-ttu-id="bb145-109">下列圖例顯示了您將操作的一些頁面。</span><span class="sxs-lookup"><span data-stu-id="bb145-109">The following illustrations show some of the pages that you'll work with.</span></span>

![部門頁面](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image1.png)

![建立部門](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image2.png)

<span data-ttu-id="bb145-112">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="bb145-112">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb145-113">瞭解非同步程式碼</span><span class="sxs-lookup"><span data-stu-id="bb145-113">Learn about asynchronous code</span></span>
> * <span data-ttu-id="bb145-114">建立部門控制器</span><span class="sxs-lookup"><span data-stu-id="bb145-114">Create a Department controller</span></span>
> * <span data-ttu-id="bb145-115">使用預存程式</span><span class="sxs-lookup"><span data-stu-id="bb145-115">Use stored procedures</span></span>
> * <span data-ttu-id="bb145-116">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="bb145-116">Deploy to Azure</span></span>

## <a name="prerequisites"></a><span data-ttu-id="bb145-117">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="bb145-117">Prerequisites</span></span>

* [<span data-ttu-id="bb145-118">更新相關資料</span><span class="sxs-lookup"><span data-stu-id="bb145-118">Updating Related Data</span></span>](updating-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="why-use-asynchronous-code"></a><span data-ttu-id="bb145-119">為何要使用非同步程式碼</span><span class="sxs-lookup"><span data-stu-id="bb145-119">Why use asynchronous code</span></span>

<span data-ttu-id="bb145-120">網頁伺服器的可用執行緒數量有限，而且在高負載情況下，可能會使用所有可用的執行緒。</span><span class="sxs-lookup"><span data-stu-id="bb145-120">A web server has a limited number of threads available, and in high load situations all of the available threads might be in use.</span></span> <span data-ttu-id="bb145-121">發生此情況時，伺服器將無法處理新的要求，直到執行緒空出來。</span><span class="sxs-lookup"><span data-stu-id="bb145-121">When that happens, the server can't process new requests until the threads are freed up.</span></span> <span data-ttu-id="bb145-122">使用同步程式碼，許多執行緒可能在實際上並未執行任何工作時受到占用，原因是在等候 I/O 完成。</span><span class="sxs-lookup"><span data-stu-id="bb145-122">With synchronous code, many threads may be tied up while they aren't actually doing any work because they're waiting for I/O to complete.</span></span> <span data-ttu-id="bb145-123">使用非同步程式碼，處理程序在等候 I/O 完成時，其執行緒將會空出來以讓伺服器處理其他要求。</span><span class="sxs-lookup"><span data-stu-id="bb145-123">With asynchronous code, when a process is waiting for I/O to complete, its thread is freed up for the server to use for processing other requests.</span></span> <span data-ttu-id="bb145-124">因此，非同步程式碼可讓伺服器資源更有效率地使用，而伺服器則可以在不延遲的情況下處理更多的流量。</span><span class="sxs-lookup"><span data-stu-id="bb145-124">As a result, asynchronous code enables server resources to be use more efficiently, and the server is enabled to handle more traffic without delays.</span></span>

<span data-ttu-id="bb145-125">在舊版的 .NET 中，撰寫和測試非同步程式碼既複雜又容易出錯，而且很難進行偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="bb145-125">In earlier versions of .NET, writing and testing asynchronous code was complex, error prone, and hard to debug.</span></span> <span data-ttu-id="bb145-126">在 .NET 4.5 中，撰寫、測試和偵錯工具的非同步程式碼會更容易，除非您有不這麼做的原因。</span><span class="sxs-lookup"><span data-stu-id="bb145-126">In .NET 4.5, writing, testing, and debugging asynchronous code is so much easier that you should generally write asynchronous code unless you have a reason not to.</span></span> <span data-ttu-id="bb145-127">非同步程式碼會產生少量的額外負荷，但對於低流量的情況，效能的衝擊是可忽略的，而在高流量的情況下，可能會大幅改善效能。</span><span class="sxs-lookup"><span data-stu-id="bb145-127">Asynchronous code does introduce a small amount of overhead, but for low traffic situations the performance hit is negligible, while for high traffic situations, the potential performance improvement is substantial.</span></span>

<span data-ttu-id="bb145-128">如需非同步程式設計的詳細資訊，請參閱[使用 .net 4.5 的非同步支援來避免封鎖呼叫](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async)。</span><span class="sxs-lookup"><span data-stu-id="bb145-128">For more information about asynchronous programming, see [Use .NET 4.5's async support to avoid blocking calls](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/web-development-best-practices.md#async).</span></span>

## <a name="create-department-controller"></a><span data-ttu-id="bb145-129">建立部門控制器</span><span class="sxs-lookup"><span data-stu-id="bb145-129">Create Department controller</span></span>

<span data-ttu-id="bb145-130">建立部門控制器的方式與先前的控制器相同，但這次請選取 [**使用非同步控制器動作**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="bb145-130">Create a Department controller the same way you did the earlier controllers, except this time select the **Use async controller actions** check box.</span></span>

<span data-ttu-id="bb145-131">下列重點說明如何將 `Index` 方法的同步程式碼加入，使其成為非同步：</span><span class="sxs-lookup"><span data-stu-id="bb145-131">The following highlights show what was added to the synchronous code for the `Index` method to make it asynchronous:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.cs?highlight=1,4)]

<span data-ttu-id="bb145-132">已套用四個變更，讓 Entity Framework 資料庫查詢能夠以非同步方式執行：</span><span class="sxs-lookup"><span data-stu-id="bb145-132">Four changes were applied to enable the Entity Framework database query to execute asynchronously:</span></span>

- <span data-ttu-id="bb145-133">方法會以 `async` 關鍵字標示，這會指示編譯器為方法主體的部分產生回呼，並自動建立傳回的 `Task<ActionResult>` 物件。</span><span class="sxs-lookup"><span data-stu-id="bb145-133">The method is marked with the `async` keyword, which tells the compiler to generate callbacks for parts of the method body and to automatically create the `Task<ActionResult>` object that is returned.</span></span>
- <span data-ttu-id="bb145-134">傳回類型已從 `ActionResult` 變更為 `Task<ActionResult>`。</span><span class="sxs-lookup"><span data-stu-id="bb145-134">The return type was changed from `ActionResult` to `Task<ActionResult>`.</span></span> <span data-ttu-id="bb145-135">`Task<T>` 類型代表進行中的工作，其類型為 `T`的結果。</span><span class="sxs-lookup"><span data-stu-id="bb145-135">The `Task<T>` type represents ongoing work with a result of type `T`.</span></span>
- <span data-ttu-id="bb145-136">`await` 關鍵字已套用至 web 服務呼叫。</span><span class="sxs-lookup"><span data-stu-id="bb145-136">The `await` keyword was applied to the web service call.</span></span> <span data-ttu-id="bb145-137">當編譯器看到此關鍵字時，它會在幕後將方法分割成兩個部分。</span><span class="sxs-lookup"><span data-stu-id="bb145-137">When the compiler sees this keyword, behind the scenes it splits the method into two parts.</span></span> <span data-ttu-id="bb145-138">第一個部分會以非同步方式啟動的作業結尾。</span><span class="sxs-lookup"><span data-stu-id="bb145-138">The first part ends with the operation that is started asynchronously.</span></span> <span data-ttu-id="bb145-139">第二個部分會放在作業完成時呼叫的回呼方法中。</span><span class="sxs-lookup"><span data-stu-id="bb145-139">The second part is put into a callback method that is called when the operation completes.</span></span>
- <span data-ttu-id="bb145-140">已呼叫 `ToList` 擴充方法的非同步版本。</span><span class="sxs-lookup"><span data-stu-id="bb145-140">The asynchronous version of the `ToList` extension method was called.</span></span>

<span data-ttu-id="bb145-141">為什麼 `departments.ToList` 語句已修改，但不是 `departments = db.Departments` 的語句？</span><span class="sxs-lookup"><span data-stu-id="bb145-141">Why is the `departments.ToList` statement modified but not the `departments = db.Departments` statement?</span></span> <span data-ttu-id="bb145-142">原因是，只有導致查詢或命令傳送至資料庫的語句會以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="bb145-142">The reason is that only statements that cause queries or commands to be sent to the database are executed asynchronously.</span></span> <span data-ttu-id="bb145-143">`departments = db.Departments` 語句會設定查詢，但在呼叫 `ToList` 方法之前，不會執行查詢。</span><span class="sxs-lookup"><span data-stu-id="bb145-143">The `departments = db.Departments` statement sets up a query but the query is not executed until the `ToList` method is called.</span></span> <span data-ttu-id="bb145-144">因此，只會以非同步方式執行 `ToList` 方法。</span><span class="sxs-lookup"><span data-stu-id="bb145-144">Therefore, only the `ToList` method is executed asynchronously.</span></span>

<span data-ttu-id="bb145-145">在 `Details` 方法和 `HttpGet` `Edit` 和 `Delete` 方法中，`Find` 方法是讓查詢傳送至資料庫的方法，因此這是非同步執行的方法：</span><span class="sxs-lookup"><span data-stu-id="bb145-145">In the `Details` method and the `HttpGet` `Edit` and `Delete` methods, the `Find` method is the one that causes a query to be sent to the database, so that's the method that gets executed asynchronously:</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.cs?highlight=7)]

<span data-ttu-id="bb145-146">在 `Create`、`HttpPost Edit`和 `DeleteConfirmed` 方法中，這是會導致執行命令的 `SaveChanges` 方法呼叫，而不是只會在記憶體中修改實體的語句（例如 `db.Departments.Add(department)`）。</span><span class="sxs-lookup"><span data-stu-id="bb145-146">In the `Create`, `HttpPost Edit`, and `DeleteConfirmed` methods, it is the `SaveChanges` method call that causes a command to be executed, not statements such as `db.Departments.Add(department)` which only cause entities in memory to be modified.</span></span>

[!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs?highlight=6)]

<span data-ttu-id="bb145-147">開啟*Views\Department\Index.cshtml*，並將範本程式碼取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="bb145-147">Open *Views\Department\Index.cshtml*, and replace the template code with the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cshtml?highlight=3,5,20-22,36-38)]

<span data-ttu-id="bb145-148">此程式碼會將標題從 [索引] 變更為 [部門]，將系統管理員名稱移至右側，並提供系統管理員的完整名稱。</span><span class="sxs-lookup"><span data-stu-id="bb145-148">This code changes the title from Index to Departments, moves the Administrator name to the right, and provides the full name of the administrator.</span></span>

<span data-ttu-id="bb145-149">在 [建立]、[刪除]、[詳細資料] 和 [編輯] 視圖中，將 [`InstructorID`] 欄位的標題變更為 [系統管理員]，如同您在課程視圖中將 [部門名稱] 欄位變更為 [部門] 的相同方式。</span><span class="sxs-lookup"><span data-stu-id="bb145-149">In the Create, Delete, Details, and Edit views, change the caption for the `InstructorID` field to "Administrator" the same way you changed the department name field to "Department" in the Course views.</span></span>

<span data-ttu-id="bb145-150">在 [建立] 和 [編輯] 視圖中，使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="bb145-150">In the Create and Edit views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cshtml)]

<span data-ttu-id="bb145-151">在 [刪除] 和 [詳細資料] 視圖中，使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="bb145-151">In the Delete and Details views use the following code:</span></span>

[!code-cshtml[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cshtml)]

<span data-ttu-id="bb145-152">執行應用程式，然後按一下 [**部門**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="bb145-152">Run the application, and click the **Departments** tab.</span></span>

<span data-ttu-id="bb145-153">所有專案的運作方式與其他控制器相同，但在此控制器中，所有 SQL 查詢都會以非同步方式執行。</span><span class="sxs-lookup"><span data-stu-id="bb145-153">Everything works the same as in the other controllers, but in this controller all of the SQL queries are executing asynchronously.</span></span>

<span data-ttu-id="bb145-154">當您使用 Entity Framework 的非同步程式設計時，要注意的一些事項：</span><span class="sxs-lookup"><span data-stu-id="bb145-154">Some things to be aware of when you are using asynchronous programming with the Entity Framework:</span></span>

- <span data-ttu-id="bb145-155">非同步程式碼不是安全線程。</span><span class="sxs-lookup"><span data-stu-id="bb145-155">The async code is not thread safe.</span></span> <span data-ttu-id="bb145-156">換句話說，不要嘗試使用相同的內容實例平行執行多個作業。</span><span class="sxs-lookup"><span data-stu-id="bb145-156">In other words, in other words, don't try to do multiple operations in parallel using the same context instance.</span></span>
- <span data-ttu-id="bb145-157">若您想要充分利用非同步程式碼帶來的效能優點，請確保任何您正在使用的程式庫 (例如分頁) 也使用了非同步 (若它們有呼叫任何可能會傳送查詢到資料庫的 Entity Framework 方法的話)。</span><span class="sxs-lookup"><span data-stu-id="bb145-157">If you want to take advantage of the performance benefits of async code, make sure that any library packages that you're using (such as for paging), also use async if they call any Entity Framework methods that cause queries to be sent to the database.</span></span>

## <a name="use-stored-procedures"></a><span data-ttu-id="bb145-158">使用預存程式</span><span class="sxs-lookup"><span data-stu-id="bb145-158">Use stored procedures</span></span>

<span data-ttu-id="bb145-159">有些開發人員和 Dba 偏好使用預存程式來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="bb145-159">Some developers and DBAs prefer to use stored procedures for database access.</span></span> <span data-ttu-id="bb145-160">在舊版的 Entity Framework 您可以藉由[執行原始 SQL 查詢](advanced-entity-framework-scenarios-for-an-mvc-web-application.md)，使用預存程式來抓取資料，但無法指示 EF 使用預存程式進行更新作業。</span><span class="sxs-lookup"><span data-stu-id="bb145-160">In earlier versions of Entity Framework you can retrieve data using a stored procedure by [executing a raw SQL query](advanced-entity-framework-scenarios-for-an-mvc-web-application.md), but you can't instruct EF to use stored procedures for update operations.</span></span> <span data-ttu-id="bb145-161">在 EF 6 中，您可以輕鬆地將 Code First 設定為使用預存程式。</span><span class="sxs-lookup"><span data-stu-id="bb145-161">In EF 6 it's easy to configure Code First to use stored procedures.</span></span>

1. <span data-ttu-id="bb145-162">在*DAL\SchoolCoNtext.cs*中，將反白顯示的程式碼新增至 `OnModelCreating` 方法。</span><span class="sxs-lookup"><span data-stu-id="bb145-162">In *DAL\SchoolContext.cs*, add the highlighted code to the `OnModelCreating` method.</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs?highlight=9)]

    <span data-ttu-id="bb145-163">此程式碼會指示 Entity Framework 在 `Department` 實體上使用預存程式進行插入、更新和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="bb145-163">This code instructs Entity Framework to use stored procedures for insert, update, and delete operations on the `Department` entity.</span></span>
2. <span data-ttu-id="bb145-164">在 [套件管理主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="bb145-164">In Package Manage Console, enter the following command:</span></span>

    `add-migration DepartmentSP`

    <span data-ttu-id="bb145-165">開啟 *[遷移]\\&lt;時間戳記&gt;\_DepartmentSP.cs* ，以在建立 Insert、Update 和 Delete 預存程式的 `Up` 方法中查看程式碼：</span><span class="sxs-lookup"><span data-stu-id="bb145-165">Open *Migrations\\&lt;timestamp&gt;\_DepartmentSP.cs* to see the code in the `Up` method that creates Insert, Update, and Delete stored procedures:</span></span>

    [!code-csharp[Main](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs?highlight=3-4,26-27,42-43)]
3. <span data-ttu-id="bb145-166">在 [套件管理主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="bb145-166">In Package Manage Console, enter the following command:</span></span>

     `update-database`
4. <span data-ttu-id="bb145-167">在 [debug] 模式中執行應用程式，按一下 [**部門**] 索引標籤，然後按一下 **[新建]。**</span><span class="sxs-lookup"><span data-stu-id="bb145-167">Run the application in debug mode, click the **Departments** tab, and then click **Create New**.</span></span>
5. <span data-ttu-id="bb145-168">輸入新部門的資料，然後按一下 [**建立**]。</span><span class="sxs-lookup"><span data-stu-id="bb145-168">Enter data for a new department, and then click **Create**.</span></span>

6. <span data-ttu-id="bb145-169">在 Visual Studio 中，查看 [**輸出**] 視窗中的記錄，以查看是否已使用預存程式來插入新的部門資料列。</span><span class="sxs-lookup"><span data-stu-id="bb145-169">In Visual Studio, look at the logs in the **Output** window to see that a stored procedure was used to insert the new Department row.</span></span>

     ![部門插入 SP](async-and-stored-procedures-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image6.png)

<span data-ttu-id="bb145-171">Code First 會建立預設的預存程式名稱。</span><span class="sxs-lookup"><span data-stu-id="bb145-171">Code First creates default stored procedure names.</span></span> <span data-ttu-id="bb145-172">如果您使用現有的資料庫，您可能需要自訂預存程式名稱，才能使用已經在資料庫中定義的預存程式。</span><span class="sxs-lookup"><span data-stu-id="bb145-172">If you are using an existing database, you might need to customize the stored procedure names in order to use stored procedures already defined in the database.</span></span> <span data-ttu-id="bb145-173">如需如何執行此動作的詳細資訊，請參閱[Entity Framework Code First 插入/更新/刪除預存程式](https://msdn.microsoft.com/data/dn468673)。</span><span class="sxs-lookup"><span data-stu-id="bb145-173">For information about how to do that, see [Entity Framework Code First Insert/Update/Delete Stored Procedures](https://msdn.microsoft.com/data/dn468673).</span></span>

<span data-ttu-id="bb145-174">如果您想要自訂產生的預存程式，您可以編輯 scaffold 程式碼來進行遷移 `Up` 方法，以建立預存程式。</span><span class="sxs-lookup"><span data-stu-id="bb145-174">If you want to customize what generated stored procedures do, you can edit the scaffolded code for the migrations `Up` method that creates the stored procedure.</span></span> <span data-ttu-id="bb145-175">如此一來，每當執行遷移時，您的變更就會反映出來，並在部署後於生產環境中自動執行時，套用到您的生產環境資料庫。</span><span class="sxs-lookup"><span data-stu-id="bb145-175">That way your changes are reflected whenever that migration is run and will be applied to your production database when migrations runs automatically in production after deployment.</span></span>

<span data-ttu-id="bb145-176">如果您想要變更在先前的遷移中建立的現有預存程式，您可以使用 [新增-遷移] 命令來產生空白的遷移，然後手動撰寫呼叫[AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx)方法的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bb145-176">If you want to change an existing stored procedure that was created in a previous migration, you can use the Add-Migration command to generate a blank migration, and then manually write code that calls the [AlterStoredProcedure](https://msdn.microsoft.com/library/system.data.entity.migrations.dbmigration.alterstoredprocedure.aspx) method.</span></span>

## <a name="deploy-to-azure"></a><span data-ttu-id="bb145-177">部署到 Azure</span><span class="sxs-lookup"><span data-stu-id="bb145-177">Deploy to Azure</span></span>

<span data-ttu-id="bb145-178">本節要求您已完成此系列的[遷移與部署](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md)教學課程中的選擇性將**應用程式部署至 Azure**一節。</span><span class="sxs-lookup"><span data-stu-id="bb145-178">This section requires you to have completed the optional **Deploying the app to Azure** section in the [Migrations and Deployment](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application.md) tutorial of this series.</span></span> <span data-ttu-id="bb145-179">如果您已藉由刪除本機專案中的資料庫來解決了遷移錯誤，請略過本節。</span><span class="sxs-lookup"><span data-stu-id="bb145-179">If you had migrations errors that you resolved by deleting the database in your local project, skip this section.</span></span>

1. <span data-ttu-id="bb145-180">在 Visual Studio 的 [方案總管] 中以滑鼠右鍵按一下專案，再選取內容功能表中的 [發佈]。</span><span class="sxs-lookup"><span data-stu-id="bb145-180">In Visual Studio, right-click the project in **Solution Explorer** and select **Publish** from the context menu.</span></span>
2. <span data-ttu-id="bb145-181">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="bb145-181">Click **Publish**.</span></span>

    <span data-ttu-id="bb145-182">Visual Studio 會將應用程式部署至 Azure，並在您的預設瀏覽器中開啟應用程式，並在 Azure 中執行。</span><span class="sxs-lookup"><span data-stu-id="bb145-182">Visual Studio deploys the application to Azure, and the application opens in your default browser, running in Azure.</span></span>
3. <span data-ttu-id="bb145-183">測試應用程式以確認其運作正常。</span><span class="sxs-lookup"><span data-stu-id="bb145-183">Test the application to verify it's working.</span></span>

    <span data-ttu-id="bb145-184">當您第一次執行存取資料庫的頁面時，Entity Framework 會執行所有需要的遷移 `Up` 方法，使資料庫與目前的資料模型保持在最新狀態。</span><span class="sxs-lookup"><span data-stu-id="bb145-184">The first time you run a page that accesses the database, the Entity Framework runs all of the migrations `Up` methods required to bring the database up to date with the current data model.</span></span> <span data-ttu-id="bb145-185">您現在可以使用您在上一次部署之後新增的所有網頁，包括您在本教學課程中新增的部門頁面。</span><span class="sxs-lookup"><span data-stu-id="bb145-185">You can now use all of the web pages that you added since the last time you deployed, including the Department pages that you added in this tutorial.</span></span>

## <a name="get-the-code"></a><span data-ttu-id="bb145-186">取得程式碼</span><span class="sxs-lookup"><span data-stu-id="bb145-186">Get the code</span></span>

[<span data-ttu-id="bb145-187">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="bb145-187">Download the Completed Project</span></span>](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a><span data-ttu-id="bb145-188">其他資源</span><span class="sxs-lookup"><span data-stu-id="bb145-188">Additional resources</span></span>

<span data-ttu-id="bb145-189">您可以在[ASP.NET 資料存取-建議的資源](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。</span><span class="sxs-lookup"><span data-stu-id="bb145-189">Links to other Entity Framework resources can be found in the [ASP.NET Data Access - Recommended Resources](../../../../whitepapers/aspnet-data-access-content-map.md).</span></span>

## <a name="next-steps"></a><span data-ttu-id="bb145-190">後續步驟</span><span class="sxs-lookup"><span data-stu-id="bb145-190">Next steps</span></span>

<span data-ttu-id="bb145-191">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="bb145-191">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="bb145-192">瞭解非同步程式碼</span><span class="sxs-lookup"><span data-stu-id="bb145-192">Learned about asynchronous code</span></span>
> * <span data-ttu-id="bb145-193">建立部門控制器</span><span class="sxs-lookup"><span data-stu-id="bb145-193">Created a Department controller</span></span>
> * <span data-ttu-id="bb145-194">已使用預存程式</span><span class="sxs-lookup"><span data-stu-id="bb145-194">Used stored procedures</span></span>
> * <span data-ttu-id="bb145-195">已部署至 Azure</span><span class="sxs-lookup"><span data-stu-id="bb145-195">Deployed to Azure</span></span>

<span data-ttu-id="bb145-196">前往下一篇文章，以瞭解如何在多位使用者同時更新相同實體時處理衝突。</span><span class="sxs-lookup"><span data-stu-id="bb145-196">Advance to the next article to learn how to handle conflicts when multiple users update the same entity at the same time.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="bb145-197">處理並行</span><span class="sxs-lookup"><span data-stu-id="bb145-197">Handling concurrency</span></span>](handling-concurrency-with-the-entity-framework-in-an-asp-net-mvc-application.md)
