---
uid: web-api/overview/data/using-web-api-with-entity-framework/part-3
title: 使用 Code First 移轉來植入資料庫 |Microsoft Docs
author: MikeWasson
description: ''
ms.author: riande
ms.date: 06/16/2014
ms.assetid: 76e2013a-65b7-488c-834d-9448ecea378e
msc.legacyurl: /web-api/overview/data/using-web-api-with-entity-framework/part-3
msc.type: authoredcontent
ms.openlocfilehash: 257bd06848adb949330856cc71eeb3d685e9d036
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78557453"
---
# <a name="use-code-first-migrations-to-seed-the-database"></a><span data-ttu-id="b9cf6-102">使用 Code First 移轉來植入資料庫</span><span class="sxs-lookup"><span data-stu-id="b9cf6-102">Use Code First Migrations to Seed the Database</span></span>

<span data-ttu-id="b9cf6-103">由[Mike Wasson](https://github.com/MikeWasson)</span><span class="sxs-lookup"><span data-stu-id="b9cf6-103">by [Mike Wasson](https://github.com/MikeWasson)</span></span>

[<span data-ttu-id="b9cf6-104">下載已完成的專案</span><span class="sxs-lookup"><span data-stu-id="b9cf6-104">Download Completed Project</span></span>](https://github.com/MikeWasson/BookService)

<span data-ttu-id="b9cf6-105">在本節中，您將使用 EF 中的[Code First 移轉](https://msdn.microsoft.com/data/jj591621)，將測試資料植入資料庫。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-105">In this section, you will use [Code First Migrations](https://msdn.microsoft.com/data/jj591621) in EF to seed the database with test data.</span></span>

<span data-ttu-id="b9cf6-106">從 [**工具**] 功能表中，選取 [ **NuGet 套件管理員**]，然後選取 [**套件管理員主控台**]。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-106">From the **Tools** menu, select **NuGet Package Manager**, then select **Package Manager Console**.</span></span> <span data-ttu-id="b9cf6-107">在 [Package Manager Console] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="b9cf6-107">In the Package Manager Console window, enter the following command:</span></span>

[!code-console[Main](part-3/samples/sample1.cmd)]

<span data-ttu-id="b9cf6-108">此命令會將名為「遷移」的資料夾新增至專案，再加上 [遷移] 資料夾中名為 Configuration.cs 的程式碼檔案。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-108">This command adds a folder named Migrations to your project, plus a code file named Configuration.cs in the Migrations folder.</span></span>

![](part-3/_static/image1.png)

<span data-ttu-id="b9cf6-109">開啟 Configuration.cs 檔案。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-109">Open the Configuration.cs file.</span></span> <span data-ttu-id="b9cf6-110">新增下列**using**語句。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-110">Add the following **using** statement.</span></span>

[!code-csharp[Main](part-3/samples/sample2.cs)]

<span data-ttu-id="b9cf6-111">然後將下列程式碼新增至**設定 Seed**方法：</span><span class="sxs-lookup"><span data-stu-id="b9cf6-111">Then add the following code to the **Configuration.Seed** method:</span></span>

[!code-csharp[Main](part-3/samples/sample3.cs)]

<span data-ttu-id="b9cf6-112">在 [套件管理員主控台] 視窗中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="b9cf6-112">In the Package Manager Console window, type the following commands:</span></span>

[!code-console[Main](part-3/samples/sample4.cmd)]

<span data-ttu-id="b9cf6-113">第一個命令會產生用來建立資料庫的程式碼，而第二個命令會執行該程式碼。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-113">The first command generates code that creates the database, and the second command executes that code.</span></span> <span data-ttu-id="b9cf6-114">資料庫會使用[LocalDB](https://msdn.microsoft.com/library/hh510202.aspx)在本機建立。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-114">The database is created locally, using [LocalDB](https://msdn.microsoft.com/library/hh510202.aspx).</span></span>

![](part-3/_static/image2.png)

## <a name="explore-the-api-optional"></a><span data-ttu-id="b9cf6-115">探索 API （選擇性）</span><span class="sxs-lookup"><span data-stu-id="b9cf6-115">Explore the API (Optional)</span></span>

<span data-ttu-id="b9cf6-116">按 F5 以在偵錯模式中執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-116">Press F5 to run the application in debug mode.</span></span> <span data-ttu-id="b9cf6-117">Visual Studio 會開始 IIS Express 並執行您的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-117">Visual Studio starts IIS Express and runs your web app.</span></span> <span data-ttu-id="b9cf6-118">Visual Studio 接著會啟動瀏覽器，並開啟應用程式的首頁。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-118">Visual Studio then launches a browser and opens the app's home page.</span></span>

<span data-ttu-id="b9cf6-119">當 Visual Studio 執行 Web 專案時，它會指派通訊埠編號。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-119">When Visual Studio runs a web project, it assigns a port number.</span></span> <span data-ttu-id="b9cf6-120">在下圖中，埠號碼為50524。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-120">In the image below, the port number is 50524.</span></span> <span data-ttu-id="b9cf6-121">當您執行應用程式時，您會看到不同的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-121">When you run the application, you'll see a different port number.</span></span>

![](part-3/_static/image3.png)

<span data-ttu-id="b9cf6-122">首頁會使用 ASP.NET MVC 來執行。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-122">The home page is implemented using ASP.NET MVC.</span></span> <span data-ttu-id="b9cf6-123">頁面頂端有一個顯示「API」的連結。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-123">At the top of the page, there is a link that says "API".</span></span> <span data-ttu-id="b9cf6-124">此連結會將您帶入 Web API 的自動產生說明頁面。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-124">This link brings you to an auto-generated help page for the web API.</span></span> <span data-ttu-id="b9cf6-125">（若要瞭解如何產生此說明頁面，以及如何將您自己的檔新增至頁面，請參閱[建立 ASP.NET Web API 的說明頁面](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md)。）您可以按一下 [說明] 頁面連結，以查看有關 API 的詳細資料，包括要求和回應格式。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-125">(To learn how this help page is generated, and how you can add your own documentation to the page, see [Creating Help Pages for ASP.NET Web API](../../getting-started-with-aspnet-web-api/creating-api-help-pages.md).) You can click on the help page links to see details about the API, including the request and response format.</span></span>

![](part-3/_static/image4.png)

<span data-ttu-id="b9cf6-126">此 API 會啟用資料庫上的 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-126">The API enables CRUD operations on the database.</span></span> <span data-ttu-id="b9cf6-127">以下摘要說明 API。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-127">The following summarizes the API.</span></span>

| <span data-ttu-id="b9cf6-128">作者</span><span class="sxs-lookup"><span data-stu-id="b9cf6-128">Authors</span></span> |  |
| --- | -- |
| <span data-ttu-id="b9cf6-129">取得 api/作者</span><span class="sxs-lookup"><span data-stu-id="b9cf6-129">GET api/authors</span></span> | <span data-ttu-id="b9cf6-130">取得所有作者。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-130">Get all authors.</span></span> |
| <span data-ttu-id="b9cf6-131">取得 api/作者/{id}</span><span class="sxs-lookup"><span data-stu-id="b9cf6-131">GET api/authors/{id}</span></span> | <span data-ttu-id="b9cf6-132">依識別碼取得作者。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-132">Get an author by ID.</span></span> |
| <span data-ttu-id="b9cf6-133">張貼/api/authors</span><span class="sxs-lookup"><span data-stu-id="b9cf6-133">POST /api/authors</span></span> | <span data-ttu-id="b9cf6-134">建立新的作者。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-134">Create a new author.</span></span> |
| <span data-ttu-id="b9cf6-135">PUT/api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="b9cf6-135">PUT /api/authors/{id}</span></span> | <span data-ttu-id="b9cf6-136">更新現有的作者。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-136">Update an existing author.</span></span> |
| <span data-ttu-id="b9cf6-137">刪除/api/authors/{id}</span><span class="sxs-lookup"><span data-stu-id="b9cf6-137">DELETE /api/authors/{id}</span></span> | <span data-ttu-id="b9cf6-138">刪除作者。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-138">Delete an author.</span></span> |

| <span data-ttu-id="b9cf6-139">書籍</span><span class="sxs-lookup"><span data-stu-id="b9cf6-139">Books</span></span> |  |
| --- | -- |
| <span data-ttu-id="b9cf6-140">取得/api/books</span><span class="sxs-lookup"><span data-stu-id="b9cf6-140">GET /api/books</span></span> | <span data-ttu-id="b9cf6-141">取得所有書籍。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-141">Get all books.</span></span> |
| <span data-ttu-id="b9cf6-142">取得/api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="b9cf6-142">GET /api/books/{id}</span></span> | <span data-ttu-id="b9cf6-143">依識別碼取得書籍。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-143">Get a book by ID.</span></span> |
| <span data-ttu-id="b9cf6-144">張貼/api/books</span><span class="sxs-lookup"><span data-stu-id="b9cf6-144">POST /api/books</span></span> | <span data-ttu-id="b9cf6-145">建立新書籍。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-145">Create a new book.</span></span> |
| <span data-ttu-id="b9cf6-146">PUT/api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="b9cf6-146">PUT /api/books/{id}</span></span> | <span data-ttu-id="b9cf6-147">更新現有的書籍。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-147">Update an existing book.</span></span> |
| <span data-ttu-id="b9cf6-148">刪除/api/books/{id}</span><span class="sxs-lookup"><span data-stu-id="b9cf6-148">DELETE /api/books/{id}</span></span> | <span data-ttu-id="b9cf6-149">刪除書籍。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-149">Delete a book.</span></span> |

## <a name="view-the-database-optional"></a><span data-ttu-id="b9cf6-150">查看資料庫（選擇性）</span><span class="sxs-lookup"><span data-stu-id="b9cf6-150">View the Database (Optional)</span></span>

<span data-ttu-id="b9cf6-151">當您執行 [更新-資料庫] 命令時，EF 會建立資料庫並呼叫 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-151">When you ran the Update-Database command, EF created the database and called the `Seed` method.</span></span> <span data-ttu-id="b9cf6-152">當您在本機執行應用程式時，EF 會使用[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-152">When you run the application locally, EF uses [LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx).</span></span> <span data-ttu-id="b9cf6-153">您可以在 Visual Studio 中查看資料庫。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-153">You can view the database in Visual Studio.</span></span> <span data-ttu-id="b9cf6-154">從 [檢視] 功能表選取 [SQL Server 物件總管]。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-154">From the **View** menu, select **SQL Server Object Explorer**.</span></span>

![](part-3/_static/image5.png)

<span data-ttu-id="b9cf6-155">在 [**連接到伺服器**] 對話方塊的 [**伺服器名稱**] 編輯方塊中，輸入 "（localdb） \v11.0"。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-155">In the **Connect to Server** dialog, in the **Server Name** edit box, type "(localdb)\v11.0".</span></span> <span data-ttu-id="b9cf6-156">將 [**驗證**] 選項保留為 [Windows 驗證]。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-156">Leave the **Authentication** option as "Windows Authentication".</span></span> <span data-ttu-id="b9cf6-157">按一下 **[Connect]** (連線)。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-157">Click **Connect**.</span></span>

![](part-3/_static/image6.png)

<span data-ttu-id="b9cf6-158">Visual Studio 會連接到 LocalDB，並在 [SQL Server 物件總管] 視窗中顯示現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-158">Visual Studio connects to LocalDB and shows your existing databases in the SQL Server Object Explorer window.</span></span> <span data-ttu-id="b9cf6-159">您可以展開節點，以查看 EF 所建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-159">You can expand the nodes to see the tables that EF created.</span></span>

![](part-3/_static/image7.png)

<span data-ttu-id="b9cf6-160">若要查看資料，請以滑鼠右鍵按一下資料表，然後選取 [**查看資料**]。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-160">To view the data, right-click a table and select **View Data**.</span></span>

![](part-3/_static/image8.png)

<span data-ttu-id="b9cf6-161">下列螢幕擷取畫面顯示 [書籍] 資料表的結果。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-161">The following screenshot shows the results for the Books table.</span></span> <span data-ttu-id="b9cf6-162">請注意，EF 已填入具有種子資料的資料庫，且資料表包含作者資料表的外鍵。</span><span class="sxs-lookup"><span data-stu-id="b9cf6-162">Notice that EF populated the database with the seed data, and the table contains the foreign key to the Authors table.</span></span>

![](part-3/_static/image9.png)

> [!div class="step-by-step"]
> <span data-ttu-id="b9cf6-163">[上一頁](part-2.md)
> [下一頁](part-4.md)</span><span class="sxs-lookup"><span data-stu-id="b9cf6-163">[Previous](part-2.md)
[Next](part-4.md)</span></span>
