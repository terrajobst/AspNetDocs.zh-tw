---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
title: 將新欄位新增至電影模型和資料表 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 9ef2c4f1-a305-4e0a-9fb8-bfbd9ef331d9
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-new-field-to-the-movie-model-and-table
msc.type: authoredcontent
ms.openlocfilehash: d966b95163f64b20a17d2327a12c5d6c44a4a66b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457696"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table"></a><span data-ttu-id="6bf28-104">將新欄位新增至電影模型和資料表</span><span class="sxs-lookup"><span data-stu-id="6bf28-104">Adding a New Field to the Movie Model and Table</span></span>

<span data-ttu-id="6bf28-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="6bf28-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="6bf28-106">本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="6bf28-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="6bf28-107">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="6bf28-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="6bf28-108">在本節中，您將使用 Entity Framework Code First 移轉來遷移模型類別的某些變更，以便將變更套用至資料庫。</span><span class="sxs-lookup"><span data-stu-id="6bf28-108">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="6bf28-109">根據預設，當您使用 Entity Framework Code First 自動建立資料庫時（如您稍早在本教學課程中所做的），Code First 會將資料表新增至資料庫，以協助追蹤資料庫的架構是否與其產生的模型類別同步。</span><span class="sxs-lookup"><span data-stu-id="6bf28-109">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="6bf28-110">如果它們不是同步的，Entity Framework 會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bf28-110">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="6bf28-111">這可讓您更輕鬆地在開發期間追蹤問題，而您可能只會在執行時間發現（藉由隱匿錯誤）。</span><span class="sxs-lookup"><span data-stu-id="6bf28-111">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="6bf28-112">設定模型變更的 Code First 移轉</span><span class="sxs-lookup"><span data-stu-id="6bf28-112">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="6bf28-113">如果您使用 Visual Studio 2012，請按兩下方案總管中的 [ *.mdf* ] 檔案，開啟 [資料庫] 工具。</span><span class="sxs-lookup"><span data-stu-id="6bf28-113">If you are using Visual Studio 2012, double click the *Movies.mdf* file from Solution Explorer to open the database tool.</span></span> <span data-ttu-id="6bf28-114">Visual Studio Express for Web 會顯示資料庫總管，Visual Studio 2012 會顯示伺服器總管。</span><span class="sxs-lookup"><span data-stu-id="6bf28-114">Visual Studio Express for Web will show Database Explorer, Visual Studio 2012 will show Server Explorer.</span></span> <span data-ttu-id="6bf28-115">如果您使用 Visual Studio 2010，請使用 SQL Server 物件總管。</span><span class="sxs-lookup"><span data-stu-id="6bf28-115">If you are using Visual Studio 2010, use SQL Server Object Explorer.</span></span>

<span data-ttu-id="6bf28-116">在資料庫工具（資料庫總管、伺服器總管或 SQL Server 物件總管）中，以滑鼠右鍵按一下 `MovieDBContext`，然後選取 [**刪除**] 以卸載電影資料庫。</span><span class="sxs-lookup"><span data-stu-id="6bf28-116">In the database tool (Database Explorer, Server Explorer or SQL Server Object Explorer), right click on `MovieDBContext` and select **Delete** to drop the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image1.png)

<span data-ttu-id="6bf28-117">流覽回到方案總管。</span><span class="sxs-lookup"><span data-stu-id="6bf28-117">Navigate back to Solution Explorer.</span></span> <span data-ttu-id="6bf28-118">以滑鼠右鍵按一下 [ *.mdf* ] 檔案，然後選取 [**刪除**] 以移除電影資料庫。</span><span class="sxs-lookup"><span data-stu-id="6bf28-118">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image2.png)

<span data-ttu-id="6bf28-119">建置應用程式，確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="6bf28-119">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="6bf28-120">在 [工具] 功能表中按一下 [NuGet 套件管理員]，然後按一下 [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="6bf28-120">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![新增套件手冊](adding-a-new-field-to-the-movie-model-and-table/_static/image3.png)

<span data-ttu-id="6bf28-122">在 [**套件管理員主控台**] 視窗的 `PM>` 提示字元中，輸入 "MvcMovie" （MovieDBCoNtext）。</span><span class="sxs-lookup"><span data-stu-id="6bf28-122">In the **Package Manager Console** window at the `PM>` prompt enter "Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext".</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image4.png)

<span data-ttu-id="6bf28-123">[**啟用-遷移**] 命令（如上所示）會在新的 [*遷移*] 資料夾中建立*Configuration.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="6bf28-123">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image5.png)

<span data-ttu-id="6bf28-124">Visual Studio 會開啟*Configuration.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="6bf28-124">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="6bf28-125">使用下列程式碼取代*Configuration.cs*檔案中的 `Seed` 方法：</span><span class="sxs-lookup"><span data-stu-id="6bf28-125">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample1.cs)]

<span data-ttu-id="6bf28-126">以滑鼠右鍵按一下 `Movie` 底下的紅色曲線，然後選取 [**解析**]，然後**使用** **MvcMovie。**</span><span class="sxs-lookup"><span data-stu-id="6bf28-126">Right click on the red squiggly line under `Movie` and select **Resolve** then **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image6.png)

<span data-ttu-id="6bf28-127">這麼做會加入下列 using 語句：</span><span class="sxs-lookup"><span data-stu-id="6bf28-127">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample2.cs)]

> [!NOTE] 
> 
> <span data-ttu-id="6bf28-128">Code First 移轉會在每次遷移之後呼叫 `Seed` 方法（也就是在套件管理員主控台中呼叫**update-database** ），而這個方法會更新已插入的資料列，如果尚未存在，則會將其插入。</span><span class="sxs-lookup"><span data-stu-id="6bf28-128">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>

<span data-ttu-id="6bf28-129">**按下 CTRL-SHIFT-B 以建立專案。** （如果您目前未建立，下列步驟將會失敗）。</span><span class="sxs-lookup"><span data-stu-id="6bf28-129">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if your don't build at this point.)</span></span>

<span data-ttu-id="6bf28-130">下一個步驟是建立初始遷移的 `DbMigration` 類別。</span><span class="sxs-lookup"><span data-stu-id="6bf28-130">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="6bf28-131">這個遷移會建立新的資料庫，這就是您在上一個步驟中刪除*movie .mdf*檔案的原因。</span><span class="sxs-lookup"><span data-stu-id="6bf28-131">This migration to creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="6bf28-132">在 [**套件管理員主控台**] 視窗中，輸入「新增-遷移初始」命令以建立初始遷移。</span><span class="sxs-lookup"><span data-stu-id="6bf28-132">In the **Package Manager Console** window, enter the command "add-migration Initial" to create the initial migration.</span></span> <span data-ttu-id="6bf28-133">「初始」名稱是任意的，用來命名所建立的遷移檔案。</span><span class="sxs-lookup"><span data-stu-id="6bf28-133">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image7.png)

<span data-ttu-id="6bf28-134">Code First 移轉會在 [*遷移*] 資料夾中建立另一個類別檔案（名稱為 *{DateStamp}\_Initial.cs* ），而此類別包含建立資料庫架構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bf28-134">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="6bf28-135">使用時間戳預先修正遷移檔案名，以協助進行排序。</span><span class="sxs-lookup"><span data-stu-id="6bf28-135">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="6bf28-136">檢查 *{DateStamp}\_Initial.cs*檔案，其中包含為 Movie DB 建立電影資料表的指示。</span><span class="sxs-lookup"><span data-stu-id="6bf28-136">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the Movies table for the Movie DB.</span></span> <span data-ttu-id="6bf28-137">當您更新下列指示中的資料庫時，這個 *{DateStamp}\_Initial.cs*檔案將會執行，並建立資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="6bf28-137">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="6bf28-138">然後，會執行**種子**方法，將測試資料填入資料庫。</span><span class="sxs-lookup"><span data-stu-id="6bf28-138">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="6bf28-139">在 [**套件管理員主控台**] 中，輸入「更新-資料庫」命令來建立資料庫，並執行**種子**方法。</span><span class="sxs-lookup"><span data-stu-id="6bf28-139">In the **Package Manager Console**, enter the command "update-database" to create the database and run the **Seed** method.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image8.png)

<span data-ttu-id="6bf28-140">如果您收到錯誤訊息，指出資料表已經存在，而且無法建立，可能是因為您在刪除資料庫之後，以及執行 `update-database`之前，已執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6bf28-140">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="6bf28-141">在這種情況下，請再次刪除 *.mdf*檔案，然後重試 `update-database` 命令。</span><span class="sxs-lookup"><span data-stu-id="6bf28-141">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="6bf28-142">如果您仍然收到錯誤，請刪除 [遷移] 資料夾和 [內容]，然後從這個頁面頂端的指示開始（也就是刪除 [ *.mdf* ] 檔案，然後繼續進行 [啟用-遷移]）。</span><span class="sxs-lookup"><span data-stu-id="6bf28-142">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span>

<span data-ttu-id="6bf28-143">執行應用程式，並流覽至 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="6bf28-143">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="6bf28-144">會顯示種子資料。</span><span class="sxs-lookup"><span data-stu-id="6bf28-144">The seed data is displayed.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image9.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="6bf28-145">將 Rating 屬性新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="6bf28-145">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="6bf28-146">首先，將新的 `Rating` 屬性加入至現有的 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="6bf28-146">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="6bf28-147">開啟*Models\Movie.cs*檔案，然後加入 `Rating` 屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6bf28-147">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample3.cs)]

<span data-ttu-id="6bf28-148">完整的 `Movie` 類別現在看起來像下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6bf28-148">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample4.cs?highlight=8)]

<span data-ttu-id="6bf28-149">使用 [組建] &gt;[**建立電影**] 功能表命令，或按 CTRL SHIFT B**來建立應用**程式。</span><span class="sxs-lookup"><span data-stu-id="6bf28-149">Build the application using the **Build** &gt;**Build Movie** menu command or by pressing CTRL-SHIFT-B.</span></span>

<span data-ttu-id="6bf28-150">既然您已更新 `Model` 類別，您也必須更新 *\Views\Movies\Index.cshtml*和 *\Views\Movies\Create.cshtml* view 範本，才能在瀏覽器視圖中顯示新的 `Rating` 屬性。</span><span class="sxs-lookup"><span data-stu-id="6bf28-150">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to display the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="6bf28-151">開啟<em>\Views\Movies\Index.cshtml</em>檔案，然後在 [<strong>價格</strong>] 資料行的正後方加入 `<th>Rating</th>` 欄標題。</span><span class="sxs-lookup"><span data-stu-id="6bf28-151">Open the<em>\Views\Movies\Index.cshtml</em> file and add a `<th>Rating</th>` column heading just after the <strong>Price</strong> column.</span></span> <span data-ttu-id="6bf28-152">然後在範本結尾附近新增 `<td>` 資料行，以轉譯 `@item.Rating` 值。</span><span class="sxs-lookup"><span data-stu-id="6bf28-152">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="6bf28-153">以下是更新的<em>Index. cshtml</em>視圖範本的樣子：</span><span class="sxs-lookup"><span data-stu-id="6bf28-153">Below is what the updated <em>Index.cshtml</em> view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample5.cshtml?highlight=26-28,46-48)]

<span data-ttu-id="6bf28-154">接下來，開啟 *\Views\Movies\Create.cshtml*檔案，並在接近表單結尾處新增下列標記。</span><span class="sxs-lookup"><span data-stu-id="6bf28-154">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="6bf28-155">這會轉譯一個文字方塊，讓您可以在建立新電影時指定評等。</span><span class="sxs-lookup"><span data-stu-id="6bf28-155">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample6.cshtml)]

<span data-ttu-id="6bf28-156">您現已更新應用程式代碼，以支援新的 `Rating` 屬性。</span><span class="sxs-lookup"><span data-stu-id="6bf28-156">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="6bf28-157">現在執行應用程式，並流覽至 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="6bf28-157">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="6bf28-158">不過，當您這麼做時，您會看到下列其中一個錯誤：</span><span class="sxs-lookup"><span data-stu-id="6bf28-158">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image10.png)

![](adding-a-new-field-to-the-movie-model-and-table/_static/image11.png)

<span data-ttu-id="6bf28-159">您看到這個錯誤是因為應用程式中更新的 `Movie` 模型類別，現在與現有資料庫 `Movie` 資料表的架構不同。</span><span class="sxs-lookup"><span data-stu-id="6bf28-159">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="6bf28-160">(資料庫資料表中沒有任何 `Rating` 資料行)。</span><span class="sxs-lookup"><span data-stu-id="6bf28-160">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="6bf28-161">有幾個方法可以解決這個錯誤：</span><span class="sxs-lookup"><span data-stu-id="6bf28-161">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="6bf28-162">讓 Entity Framework 自動卸除資料庫，並重新依據新的模型類別結構描述來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="6bf28-162">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="6bf28-163">在測試資料庫上進行開發時，這個方法非常方便;它可讓您快速地將模型和資料庫架構進化在一起。</span><span class="sxs-lookup"><span data-stu-id="6bf28-163">This approach is very convenient when doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="6bf28-164">不過，缺點是您會遺失資料庫中的現有資料，因此您*不*會想要在生產資料庫上使用此方法！</span><span class="sxs-lookup"><span data-stu-id="6bf28-164">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="6bf28-165">使用初始化運算式將測試資料自動植入資料庫，通常是開發應用程式的有效方式。</span><span class="sxs-lookup"><span data-stu-id="6bf28-165">Using an initializer to automatically seed a database with test data is often a productive way to develope an application.</span></span> <span data-ttu-id="6bf28-166">如需 Entity Framework 資料庫初始化運算式的詳細資訊，請參閱 Tom 作者: dykstra 的[ASP.NET MVC/Entity Framework 教學](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程。</span><span class="sxs-lookup"><span data-stu-id="6bf28-166">For more information on Entity Framework database initializers, see Tom Dykstra's [ASP.NET MVC/Entity Framework tutorial](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="6bf28-167">您可明確修改現有資料庫的結構描述，使其符合模型類別。</span><span class="sxs-lookup"><span data-stu-id="6bf28-167">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="6bf28-168">這種方法的優點是可以保留您的資料。</span><span class="sxs-lookup"><span data-stu-id="6bf28-168">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="6bf28-169">您可以手動方式或藉由建立資料庫變更指令碼來進行這項變更。</span><span class="sxs-lookup"><span data-stu-id="6bf28-169">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="6bf28-170">使用 Code First 移轉來更新資料庫結構描述。</span><span class="sxs-lookup"><span data-stu-id="6bf28-170">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="6bf28-171">在本教學課程中，我們將使用 Code First 移轉。</span><span class="sxs-lookup"><span data-stu-id="6bf28-171">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="6bf28-172">更新種子方法，讓它提供新資料行的值。</span><span class="sxs-lookup"><span data-stu-id="6bf28-172">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="6bf28-173">開啟 [Migrations\Configuration.cs 檔案]，並將 [評等] 欄位新增至每個 Movie 物件。</span><span class="sxs-lookup"><span data-stu-id="6bf28-173">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample7.cs?highlight=6)]

<span data-ttu-id="6bf28-174">建立解決方案，然後開啟 [**套件管理員主控台**] 視窗並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="6bf28-174">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration AddRatingMig`

<span data-ttu-id="6bf28-175">`add-migration` 命令會告訴遷移架構使用目前的 movie DB 架構來檢查目前的電影模型，並建立必要的程式碼來將資料庫移轉至新的模型。</span><span class="sxs-lookup"><span data-stu-id="6bf28-175">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="6bf28-176">AddRatingMig 是任意的，用來命名遷移檔案。</span><span class="sxs-lookup"><span data-stu-id="6bf28-176">The AddRatingMig is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="6bf28-177">使用有意義的名稱來進行遷移步驟會很有説明。</span><span class="sxs-lookup"><span data-stu-id="6bf28-177">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="6bf28-178">當此命令完成時，Visual Studio 會開啟定義新 `DbMigration` 衍生類別的類別檔案，而在 `Up` 方法中，您可以看到建立新資料行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6bf28-178">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field-to-the-movie-model-and-table/samples/sample8.cs)]

<span data-ttu-id="6bf28-179">建立解決方案，然後在 [**套件管理員主控台**] 視窗中輸入 [更新資料庫] 命令。</span><span class="sxs-lookup"><span data-stu-id="6bf28-179">Build the solution, and then enter the "update-database" command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="6bf28-180">下圖顯示 [**套件管理員主控台**] 視窗中的輸出（前面加上 AddRatingMig 的日期戳記會有所不同）。</span><span class="sxs-lookup"><span data-stu-id="6bf28-180">The following image shows the output in the **Package Manager Console** window (The date stamp prepending AddRatingMig will be different.)</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image12.png)

<span data-ttu-id="6bf28-181">重新執行應用程式，並流覽至/Movies URL。</span><span class="sxs-lookup"><span data-stu-id="6bf28-181">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="6bf28-182">您可以看到新的評等欄位。</span><span class="sxs-lookup"><span data-stu-id="6bf28-182">You can see the new Rating field.</span></span>

![](adding-a-new-field-to-the-movie-model-and-table/_static/image13.png)

<span data-ttu-id="6bf28-183">按一下 [**建立新**的] 連結以新增電影。</span><span class="sxs-lookup"><span data-stu-id="6bf28-183">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="6bf28-184">請注意，您可以加入評等。</span><span class="sxs-lookup"><span data-stu-id="6bf28-184">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field-to-the-movie-model-and-table/_static/image14.png)

<span data-ttu-id="6bf28-186">按一下 **[建立]** 。</span><span class="sxs-lookup"><span data-stu-id="6bf28-186">Click **Create**.</span></span> <span data-ttu-id="6bf28-187">新電影（包括評等）現在會顯示在電影清單中：</span><span class="sxs-lookup"><span data-stu-id="6bf28-187">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field-to-the-movie-model-and-table/_static/image15.png)

<span data-ttu-id="6bf28-189">您也應該將 [`Rating`] 欄位加入至 [編輯]、[詳細資料] 和 [SearchIndex] 視圖範本。</span><span class="sxs-lookup"><span data-stu-id="6bf28-189">You should also add the `Rating` field to the Edit, Details and SearchIndex view templates.</span></span>

<span data-ttu-id="6bf28-190">您可以再次在 [**套件管理員主控台**] 視窗中輸入「更新資料庫」命令，而且不會進行任何變更，因為架構符合模型。</span><span class="sxs-lookup"><span data-stu-id="6bf28-190">You could enter the "update-database" command in the **Package Manager Console** window again and no changes would be made, because the schema matches the model.</span></span>

<span data-ttu-id="6bf28-191">在本節中，您會看到如何修改模型物件，並讓資料庫與變更保持同步。</span><span class="sxs-lookup"><span data-stu-id="6bf28-191">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="6bf28-192">您也學到以範例資料填入新建立資料庫的方法，讓您可以試試看案例。</span><span class="sxs-lookup"><span data-stu-id="6bf28-192">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="6bf28-193">接下來，我們將探討如何將更豐富的驗證邏輯新增至模型類別，並讓某些商務規則得以強制執行。</span><span class="sxs-lookup"><span data-stu-id="6bf28-193">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6bf28-194">[上一頁](examining-the-edit-methods-and-edit-view.md)
> [下一頁](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="6bf28-194">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
