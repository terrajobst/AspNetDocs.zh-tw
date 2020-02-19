---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
title: 從控制器存取模型的資料 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 61e0206d-7f32-4018-992d-0a51b48b37dc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 7c4aa34567ac4fb31d1ed874cf65986c4e779e66
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456162"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="53ee5-104">從控制器存取模型資料</span><span class="sxs-lookup"><span data-stu-id="53ee5-104">Accessing Your Model's Data from a Controller</span></span>

<span data-ttu-id="53ee5-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="53ee5-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="53ee5-106">本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="53ee5-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="53ee5-107">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="53ee5-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="53ee5-108">在本節中，您將建立新的 `MoviesController` 類別，並撰寫可抓取電影資料的程式碼，並使用 view 範本在瀏覽器中顯示它。</span><span class="sxs-lookup"><span data-stu-id="53ee5-108">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span>

<span data-ttu-id="53ee5-109">請先**建立應用程式**，再繼續進行下一個步驟。</span><span class="sxs-lookup"><span data-stu-id="53ee5-109">**Build the application** before going on to the next step.</span></span>

<span data-ttu-id="53ee5-110">以滑鼠右鍵按一下 [*控制器*] 資料夾，然後建立新的 `MoviesController` 控制器。</span><span class="sxs-lookup"><span data-stu-id="53ee5-110">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="53ee5-111">在您建立應用程式之前，將不會顯示下列選項。</span><span class="sxs-lookup"><span data-stu-id="53ee5-111">The options below will not appear until you build your application.</span></span> <span data-ttu-id="53ee5-112">選取下列選項：</span><span class="sxs-lookup"><span data-stu-id="53ee5-112">Select the following options:</span></span>

- <span data-ttu-id="53ee5-113">控制器名稱： **moviescontroller.cs**。</span><span class="sxs-lookup"><span data-stu-id="53ee5-113">Controller name: **MoviesController**.</span></span> <span data-ttu-id="53ee5-114">（這是預設值。</span><span class="sxs-lookup"><span data-stu-id="53ee5-114">(This is the default.</span></span> <span data-ttu-id="53ee5-115">)</span><span class="sxs-lookup"><span data-stu-id="53ee5-115">)</span></span>
- <span data-ttu-id="53ee5-116">範本：**具有讀取/寫入動作和視圖的 MVC 控制器，使用 Entity Framework**。</span><span class="sxs-lookup"><span data-stu-id="53ee5-116">Template: **MVC Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="53ee5-117">模型類別： **Movie （MvcMovie）** 。</span><span class="sxs-lookup"><span data-stu-id="53ee5-117">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="53ee5-118">資料內容類別： **MovieDBCoNtext （MvcMovie）** 。</span><span class="sxs-lookup"><span data-stu-id="53ee5-118">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="53ee5-119">Views： **Razor （CSHTML）** 。</span><span class="sxs-lookup"><span data-stu-id="53ee5-119">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="53ee5-120">（預設值）。</span><span class="sxs-lookup"><span data-stu-id="53ee5-120">(The default.)</span></span>

![AddScaffoldedMovieController](accessing-your-models-data-from-a-controller/_static/image1.png)

<span data-ttu-id="53ee5-122">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="53ee5-122">Click **Add**.</span></span> <span data-ttu-id="53ee5-123">Visual Studio Express 會建立下列檔案和資料夾：</span><span class="sxs-lookup"><span data-stu-id="53ee5-123">Visual Studio Express creates the following files and folders:</span></span>

- <span data-ttu-id="53ee5-124">專案的 [*控制器*] 資料夾中的*MoviesController.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="53ee5-124">*A MoviesController.cs* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="53ee5-125">專案 [ *Views* ] 資料夾中的 [*電影*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="53ee5-125">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="53ee5-126">在新的*Views\Movies*資料夾中，*建立. cshtml、Delete.* cshtml、Details、cshtml 和*Index.* cshtml。</span><span class="sxs-lookup"><span data-stu-id="53ee5-126">*Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml*, and *Index.cshtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="53ee5-127">ASP.NET MVC 4 會為您自動建立 CRUD （建立、讀取、更新和刪除）動作方法和視圖（自動建立 CRUD 動作方法和 views）稱為「樣板」（樣板））。</span><span class="sxs-lookup"><span data-stu-id="53ee5-127">ASP.NET MVC 4 automatically created the CRUD (create, read, update, and delete) action methods and views for you (the automatic creation of CRUD action methods and views is known as scaffolding).</span></span> <span data-ttu-id="53ee5-128">您現在有一個功能完整的 web 應用程式，可讓您建立、列出、編輯和刪除電影專案。</span><span class="sxs-lookup"><span data-stu-id="53ee5-128">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="53ee5-129">執行應用程式，並藉由將 */Movies*附加至瀏覽器網址列中的 URL，流覽至 `Movies` 控制器。</span><span class="sxs-lookup"><span data-stu-id="53ee5-129">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="53ee5-130">因為應用程式會依賴預設路由（定義于*global.asax*檔案中），所以瀏覽器要求 `http://localhost:xxxxx/Movies` 會路由傳送至 `Movies` 控制器的預設 `Index` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="53ee5-130">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="53ee5-131">換句話說，瀏覽器要求 `http://localhost:xxxxx/Movies` 與瀏覽器要求 `http://localhost:xxxxx/Movies/Index`有效。</span><span class="sxs-lookup"><span data-stu-id="53ee5-131">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="53ee5-132">結果是空的電影清單，因為您還沒有加入。</span><span class="sxs-lookup"><span data-stu-id="53ee5-132">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image2.png)

### <a name="creating-a-movie"></a><span data-ttu-id="53ee5-133">建立電影</span><span class="sxs-lookup"><span data-stu-id="53ee5-133">Creating a Movie</span></span>

<span data-ttu-id="53ee5-134">選取 **Create New** 連結。</span><span class="sxs-lookup"><span data-stu-id="53ee5-134">Select the **Create New** link.</span></span> <span data-ttu-id="53ee5-135">輸入電影的一些詳細資料，然後按一下 [**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="53ee5-135">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image3.png)

<span data-ttu-id="53ee5-136">按一下 [**建立**] 按鈕會導致表單張貼至伺服器，其中電影資訊會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="53ee5-136">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="53ee5-137">接著，您會被重新導向至 [ */Movies* URL]，您可以在清單中看到新建立的電影。</span><span class="sxs-lookup"><span data-stu-id="53ee5-137">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="53ee5-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span><span class="sxs-lookup"><span data-stu-id="53ee5-138">![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image4.png "IndexWhenHarryMet")</span></span>

<span data-ttu-id="53ee5-139">建立幾個電影項目。</span><span class="sxs-lookup"><span data-stu-id="53ee5-139">Create a couple more movie entries.</span></span> <span data-ttu-id="53ee5-140">嘗試 **Edit**、**Details** 和 **Delete** 連結，這些連結都可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="53ee5-140">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="53ee5-141">檢查產生的程式碼</span><span class="sxs-lookup"><span data-stu-id="53ee5-141">Examining the Generated Code</span></span>

<span data-ttu-id="53ee5-142">開啟*Controllers\MoviesController.cs*檔案，並檢查產生的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="53ee5-142">Open the *Controllers\MoviesController.cs* file and examine the generated `Index` method.</span></span> <span data-ttu-id="53ee5-143">具有 `Index` 方法的電影控制器部分如下所示。</span><span class="sxs-lookup"><span data-stu-id="53ee5-143">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample1.cs)]

<span data-ttu-id="53ee5-144">如先前所述，來自 `MoviesController` 類別的下一行會具現化電影資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="53ee5-144">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="53ee5-145">您可以使用電影資料庫內容來查詢、編輯和刪除電影。</span><span class="sxs-lookup"><span data-stu-id="53ee5-145">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample2.cs)]

<span data-ttu-id="53ee5-146">`Movies` 控制器的要求會傳回 movie 資料庫之 `Movies` 資料表中的所有專案，然後將結果傳遞至 `Index` view。</span><span class="sxs-lookup"><span data-stu-id="53ee5-146">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="53ee5-147">強型別模型和 @model 關鍵字</span><span class="sxs-lookup"><span data-stu-id="53ee5-147">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="53ee5-148">稍早在本教學課程中，您已看到控制器如何使用 `ViewBag` 物件，將資料或物件傳遞至視圖範本。</span><span class="sxs-lookup"><span data-stu-id="53ee5-148">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="53ee5-149">`ViewBag` 是動態物件，可提供方便的晚期繫結方式，將資訊傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="53ee5-149">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="53ee5-150">ASP.NET MVC 也提供將強型別資料或物件傳遞至視圖範本的能力。</span><span class="sxs-lookup"><span data-stu-id="53ee5-150">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="53ee5-151">這個強型別方法可讓您在 Visual Studio 編輯器中，對程式碼和更豐富的 IntelliSense 進行編譯階段檢查。</span><span class="sxs-lookup"><span data-stu-id="53ee5-151">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Studio editor.</span></span> <span data-ttu-id="53ee5-152">Visual Studio 中的「架構」機制在建立方法和 views 時，會使用此方法搭配 `MoviesController` 類別和「視圖」範本。</span><span class="sxs-lookup"><span data-stu-id="53ee5-152">The scaffolding mechanism in Visual Studio used this approach with the `MoviesController` class and view templates when it created the methods and views.</span></span>

<span data-ttu-id="53ee5-153">在*Controllers\MoviesController.cs*檔案中，檢查產生的 `Details` 方法。</span><span class="sxs-lookup"><span data-stu-id="53ee5-153">In the *Controllers\MoviesController.cs* file examine the generated `Details` method.</span></span> <span data-ttu-id="53ee5-154">具有 `Details` 方法的電影控制器部分如下所示。</span><span class="sxs-lookup"><span data-stu-id="53ee5-154">A portion of the movie controller with the `Details` method is shown below.</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample3.cs?highlight=3,8)]

<span data-ttu-id="53ee5-155">如果找到 `Movie`，就會將 `Movie` 模型的實例傳遞至詳細資料檢視。</span><span class="sxs-lookup"><span data-stu-id="53ee5-155">If a `Movie` is found, an instance of the `Movie` model is passed to the Details view.</span></span> <span data-ttu-id="53ee5-156">檢查*Views\Movies\Details.cshtml*檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="53ee5-156">Examine the contents of the *Views\Movies\Details.cshtml* file.</span></span>

<span data-ttu-id="53ee5-157">藉由在視圖範本檔案的頂端包含 `@model` 語句，您可以指定此視圖所預期的物件類型。</span><span class="sxs-lookup"><span data-stu-id="53ee5-157">By including a `@model` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="53ee5-158">當您建立電影控制器時，Visual Studio 會在 `@model`Details.cshtml*檔案的最上方自動包含下列* 陳述式：</span><span class="sxs-lookup"><span data-stu-id="53ee5-158">When you created the movie controller, Visual Studio automatically included the following `@model` statement at the top of the *Details.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.cshtml)]

<span data-ttu-id="53ee5-159">這個 `@model` 指示詞可讓您使用強型別的 `Model` 物件，存取控制器傳遞至檢視的電影。</span><span class="sxs-lookup"><span data-stu-id="53ee5-159">This `@model` directive allows you to access the movie that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="53ee5-160">例如，在*詳細資料的 cshtml*範本中，程式碼會將每個電影欄位傳遞給 `DisplayNameFor`，並使用強型別 `Model` 物件[DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML 協助程式。</span><span class="sxs-lookup"><span data-stu-id="53ee5-160">For example, in the *Details.cshtml* template, the code passes each movie field to the `DisplayNameFor` and [DisplayFor](https://msdn.microsoft.com/library/system.web.mvc.html.displayextensions.displayfor(VS.98).aspx) HTML Helpers with the strongly typed `Model` object.</span></span> <span data-ttu-id="53ee5-161">建立和編輯方法和視圖範本也會通過電影模型物件。</span><span class="sxs-lookup"><span data-stu-id="53ee5-161">The Create and Edit methods and view templates also pass a movie model object.</span></span>

<span data-ttu-id="53ee5-162">檢查*MoviesController.cs*檔案中的 [ *Index. cshtml* ] （.）視圖範本和 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="53ee5-162">Examine the *Index.cshtml* view template and the `Index` method in the *MoviesController.cs* file.</span></span> <span data-ttu-id="53ee5-163">請注意，當程式碼在 `Index` 動作方法中呼叫 `View` helper 方法時，如何建立[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)物件。</span><span class="sxs-lookup"><span data-stu-id="53ee5-163">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="53ee5-164">然後，此程式碼會將此 `Movies` 清單從控制器傳遞至視圖：</span><span class="sxs-lookup"><span data-stu-id="53ee5-164">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-csharp[Main](accessing-your-models-data-from-a-controller/samples/sample5.cs?highlight=3)]

<span data-ttu-id="53ee5-165">當您建立電影控制器時，Visual Studio Express 會自動將下列 `@model` 語句包含在*索引 cshtml*檔案的頂端：</span><span class="sxs-lookup"><span data-stu-id="53ee5-165">When you created the movie controller, Visual Studio Express automatically included the following `@model` statement at the top of the *Index.cshtml* file:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample6.cshtml)]

<span data-ttu-id="53ee5-166">此 `@model` 指示詞可讓您使用強型別的 `Model` 物件，來存取控制器傳遞至視圖的電影清單。</span><span class="sxs-lookup"><span data-stu-id="53ee5-166">This `@model` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="53ee5-167">例如，在*Index. cshtml*範本中，程式碼會對強型別 `Model` 物件執行 `foreach` 語句，藉以迴圈執行電影：</span><span class="sxs-lookup"><span data-stu-id="53ee5-167">For example, in the *Index.cshtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-cshtml[Main](accessing-your-models-data-from-a-controller/samples/sample7.cshtml?highlight=1,4,7,10,13,16,19-21)]

<span data-ttu-id="53ee5-168">因為 `Model` 物件是強型別（做為 `IEnumerable<Movie>` 物件），所以迴圈中的每個 `item` 物件都會輸入為 `Movie`。</span><span class="sxs-lookup"><span data-stu-id="53ee5-168">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="53ee5-169">除了其他優點外，這也表示您可以在程式碼編輯器中，取得程式碼的編譯時期檢查和完整的 IntelliSense 支援：</span><span class="sxs-lookup"><span data-stu-id="53ee5-169">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

![ModelIntelliSense](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="working-with-sql-server-localdb"></a><span data-ttu-id="53ee5-171">使用 SQL Server LocalDB</span><span class="sxs-lookup"><span data-stu-id="53ee5-171">Working with SQL Server LocalDB</span></span>

<span data-ttu-id="53ee5-172">Entity Framework Code First 偵測到所提供的資料庫連接字串指向尚未存在的 `Movies` 資料庫，因此 Code First 自動建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="53ee5-172">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="53ee5-173">您可以藉由查看*應用程式\_Data*資料夾來確認它是否已建立。</span><span class="sxs-lookup"><span data-stu-id="53ee5-173">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="53ee5-174">如果您看不到 [*電影 .mdf* ] 檔案，請按一下 [**方案總管**] 工具列中的 [**顯示所有**檔案] 按鈕，按一下 [重新整理 **] 按鈕，** 然後展開*應用程式\_[Data* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="53ee5-174">If you don't see the *Movies.mdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="53ee5-175">按兩下 [ *.Mdf* ] 以開啟 [**資料庫瀏覽器**]，然後展開 [**資料表]** 資料夾，以查看電影資料表。</span><span class="sxs-lookup"><span data-stu-id="53ee5-175">Double-click *Movies.mdf* to open **DATABASE EXPLORER**, then expand the **Tables** folder to see the Movies table.</span></span>

<span data-ttu-id="53ee5-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span><span class="sxs-lookup"><span data-stu-id="53ee5-176">![DB_explorer](accessing-your-models-data-from-a-controller/_static/image7.png "DB_explorer")</span></span>

> [!NOTE]
> <span data-ttu-id="53ee5-177">如果未出現 [資料庫 explorer]，請從 [**工具**] 功能表中選取 **[連接到資料庫]** ，然後取消 [**選擇資料來源**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="53ee5-177">If the database explorer doesn't appear, from the **TOOLS** menu, select **Connect to Database**, then cancel the **Choose Data Source** dialog.</span></span> <span data-ttu-id="53ee5-178">這會強制開啟 [資料庫 explorer]。</span><span class="sxs-lookup"><span data-stu-id="53ee5-178">This will force open the database explorer.</span></span>

> [!NOTE]
> <span data-ttu-id="53ee5-179">如果您使用 VWD 或 Visual Studio 2010，並取得類似下列任一項的錯誤：</span><span class="sxs-lookup"><span data-stu-id="53ee5-179">If you are using VWD or Visual Studio 2010 and get an error similar to any of the following following:</span></span>
> 
> - <span data-ttu-id="53ee5-180">資料庫 ' C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES。無法開啟 .MDF '，因為它是706版。</span><span class="sxs-lookup"><span data-stu-id="53ee5-180">The database 'C:\Webs\MVC4\MVCMOVIE\MVCMOVIE\APP\_DATA\MOVIES.MDF' cannot be opened because it is version 706.</span></span> <span data-ttu-id="53ee5-181">此伺服器支援655版和更早版本。</span><span class="sxs-lookup"><span data-stu-id="53ee5-181">This server supports version 655 and earlier.</span></span> <span data-ttu-id="53ee5-182">不支援降級路徑。</span><span class="sxs-lookup"><span data-stu-id="53ee5-182">A downgrade path is not supported.</span></span>
> - <span data-ttu-id="53ee5-183">&quot;的 InvalidOperation 例外狀況已由使用者程式碼處理，&quot; 提供的 SqlConnection 未指定初始目錄。</span><span class="sxs-lookup"><span data-stu-id="53ee5-183">&quot;InvalidOperation Exception was unhandled by user code&quot; The supplied SqlConnection does not specify an initial catalog.</span></span>
> 
> <span data-ttu-id="53ee5-184">您必須安裝[SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx)和[LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0)。</span><span class="sxs-lookup"><span data-stu-id="53ee5-184">You need to install the [SQL Server Data Tools](https://blogs.msdn.com/b/rickandy/archive/2012/08/02/installing-and-using-sql-server-data-tools-ssdt-on-visual-studio-2010-and-vwd.aspx) and [LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLLocalDBOnly_11_0).</span></span> <span data-ttu-id="53ee5-185">請確認前一頁指定的 `MovieDBContext` 連接字串。</span><span class="sxs-lookup"><span data-stu-id="53ee5-185">Verify the `MovieDBContext` connection string specified on the previous page.</span></span>

<span data-ttu-id="53ee5-186">以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**顯示資料表資料**] 以查看您所建立的資料。</span><span class="sxs-lookup"><span data-stu-id="53ee5-186">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image8.png)

<span data-ttu-id="53ee5-187">以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**開啟資料表定義**]，查看 Entity Framework Code First 為您建立的資料表結構。</span><span class="sxs-lookup"><span data-stu-id="53ee5-187">Right-click the `Movies` table and select **Open Table Definition** to see the table structure that Entity Framework Code First created for you.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image9.png "MoviesTable")

![](accessing-your-models-data-from-a-controller/_static/image10.png)

<span data-ttu-id="53ee5-188">請注意 `Movies` 資料表的架構如何對應至您稍早建立的 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="53ee5-188">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="53ee5-189">Entity Framework Code First 會根據您的 `Movie` 類別，自動為您建立此架構。</span><span class="sxs-lookup"><span data-stu-id="53ee5-189">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="53ee5-190">當您完成時，請以滑鼠右鍵按一下 [ *MovieDBCoNtext* ]，然後選取 [**關閉連接**] 來關閉連線。</span><span class="sxs-lookup"><span data-stu-id="53ee5-190">When you're finished, close the connection by right clicking *MovieDBContext* and selecting **Close Connection**.</span></span> <span data-ttu-id="53ee5-191">（如果您不關閉連線，下次執行專案時可能會出現錯誤）。</span><span class="sxs-lookup"><span data-stu-id="53ee5-191">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

![](accessing-your-models-data-from-a-controller/_static/image11.png "CloseConnection")

<span data-ttu-id="53ee5-192">您現在已擁有資料庫和簡單的清單頁面，可顯示其內容。</span><span class="sxs-lookup"><span data-stu-id="53ee5-192">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="53ee5-193">在下一個教學課程中，我們將檢查 scaffold 程式碼的其餘部分，並新增 `SearchIndex` 方法和 `SearchIndex` 視圖，讓您在此資料庫中搜尋電影。</span><span class="sxs-lookup"><span data-stu-id="53ee5-193">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="53ee5-194">[上一頁](adding-a-model.md)
> [下一頁](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="53ee5-194">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
