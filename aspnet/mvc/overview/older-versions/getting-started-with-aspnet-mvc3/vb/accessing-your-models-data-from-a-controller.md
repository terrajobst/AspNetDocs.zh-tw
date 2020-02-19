---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
title: 從控制器存取模型資料（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: cad00de1-3c68-4ff4-a436-54236d449459
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/accessing-your-models-data-from-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 37f45d8f12e3ab5c485718bcf2c59934ad272118
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457931"
---
# <a name="accessing-your-models-data-from-a-controller-vb"></a><span data-ttu-id="e4e66-103">從控制器存取模型資料 (VB)</span><span class="sxs-lookup"><span data-stu-id="e4e66-103">Accessing your Model's Data from a Controller (VB)</span></span>

<span data-ttu-id="e4e66-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="e4e66-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="e4e66-105">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="e4e66-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="e4e66-106">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="e4e66-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="e4e66-107">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="e4e66-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="e4e66-108">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="e4e66-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="e4e66-109">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="e4e66-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="e4e66-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="e4e66-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="e4e66-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="e4e66-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="e4e66-112">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="e4e66-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="e4e66-113">本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="e4e66-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="e4e66-114">[下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="e4e66-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="e4e66-115">如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/accessing-your-models-data-from-a-controller.md)。</span><span class="sxs-lookup"><span data-stu-id="e4e66-115">If you prefer C#, switch to the [C# version](../cs/accessing-your-models-data-from-a-controller.md) of this tutorial.</span></span>

<span data-ttu-id="e4e66-116">在本節中，您將建立新的 `MoviesController` 類別，並撰寫可抓取電影資料的程式碼，並使用 view 範本在瀏覽器中顯示它。</span><span class="sxs-lookup"><span data-stu-id="e4e66-116">In this section, you'll create a new `MoviesController` class and write code that retrieves the movie data and displays it in the browser using a view template.</span></span> <span data-ttu-id="e4e66-117">請務必先建立您的應用程式，再繼續進行。</span><span class="sxs-lookup"><span data-stu-id="e4e66-117">Be sure to build your application before proceeding.</span></span>

<span data-ttu-id="e4e66-118">以滑鼠右鍵按一下 [*控制器*] 資料夾，然後建立新的 `MoviesController` 控制器。</span><span class="sxs-lookup"><span data-stu-id="e4e66-118">Right-click the *Controllers* folder and create a new `MoviesController` controller.</span></span> <span data-ttu-id="e4e66-119">選取下列選項：</span><span class="sxs-lookup"><span data-stu-id="e4e66-119">Select the following options:</span></span>

- <span data-ttu-id="e4e66-120">控制器名稱： **moviescontroller.cs**。</span><span class="sxs-lookup"><span data-stu-id="e4e66-120">Controller name: **MoviesController**.</span></span> <span data-ttu-id="e4e66-121">(這是預設值。)</span><span class="sxs-lookup"><span data-stu-id="e4e66-121">(This is the default.)</span></span>
- <span data-ttu-id="e4e66-122">範本：**具有讀取/寫入動作和視圖的控制器，使用 Entity Framework**。</span><span class="sxs-lookup"><span data-stu-id="e4e66-122">Template: **Controller with read/write actions and views, using Entity Framework**.</span></span>
- <span data-ttu-id="e4e66-123">模型類別： **Movie （MvcMovie）** 。</span><span class="sxs-lookup"><span data-stu-id="e4e66-123">Model class: **Movie (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="e4e66-124">資料內容類別： **MovieDBCoNtext （MvcMovie）** 。</span><span class="sxs-lookup"><span data-stu-id="e4e66-124">Data context class: **MovieDBContext (MvcMovie.Models)**.</span></span>
- <span data-ttu-id="e4e66-125">Views： **Razor （CSHTML）** 。</span><span class="sxs-lookup"><span data-stu-id="e4e66-125">Views: **Razor (CSHTML)**.</span></span> <span data-ttu-id="e4e66-126">（預設值）。</span><span class="sxs-lookup"><span data-stu-id="e4e66-126">(The default.)</span></span>

<span data-ttu-id="e4e66-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-127">[![5addMovieController](accessing-your-models-data-from-a-controller/_static/image2.png)](accessing-your-models-data-from-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="e4e66-128">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="e4e66-128">Click **Add**.</span></span> <span data-ttu-id="e4e66-129">Visual Web Developer 會建立下列檔案和資料夾：</span><span class="sxs-lookup"><span data-stu-id="e4e66-129">Visual Web Developer creates the following files and folders:</span></span>

- <span data-ttu-id="e4e66-130">專案的 [*控制器*] 資料夾中的*moviescontroller.cs .vb*檔案。</span><span class="sxs-lookup"><span data-stu-id="e4e66-130">*A MoviesController.vb* file in the project's *Controllers* folder.</span></span>
- <span data-ttu-id="e4e66-131">專案 [ *Views* ] 資料夾中的 [*電影*] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="e4e66-131">A *Movies* folder in the project's *Views* folder.</span></span>
- <span data-ttu-id="e4e66-132">在新的*Views\Movies*資料夾中*建立 vbhtml、Delete.* vbhtml、Details、vbhtml、. vbhtml 和*Index。*</span><span class="sxs-lookup"><span data-stu-id="e4e66-132">*Create.vbhtml, Delete.vbhtml, Details.vbhtml, Edit.vbhtml*, and *Index.vbhtml* in the new *Views\Movies* folder.</span></span>

<span data-ttu-id="e4e66-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-133">[![5_ScaffoldMovie](accessing-your-models-data-from-a-controller/_static/image4.png)](accessing-your-models-data-from-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="e4e66-134">ASP.NET MVC 3 架構機制會自動為您建立 CRUD （建立、讀取、更新和刪除）動作方法和視圖。</span><span class="sxs-lookup"><span data-stu-id="e4e66-134">The ASP.NET MVC 3 scaffolding mechanism automatically created the CRUD (create, read, update, and delete) action methods and views for you.</span></span> <span data-ttu-id="e4e66-135">您現在有一個功能完整的 web 應用程式，可讓您建立、列出、編輯和刪除電影專案。</span><span class="sxs-lookup"><span data-stu-id="e4e66-135">You now have a fully functional web application that lets you create, list, edit, and delete movie entries.</span></span>

<span data-ttu-id="e4e66-136">執行應用程式，並藉由將 */Movies*附加至瀏覽器網址列中的 URL，流覽至 `Movies` 控制器。</span><span class="sxs-lookup"><span data-stu-id="e4e66-136">Run the application and browse to the `Movies` controller by appending */Movies* to the URL in the address bar of your browser.</span></span> <span data-ttu-id="e4e66-137">因為應用程式會依賴預設路由（定義于*global.asax*檔案中），所以瀏覽器要求 `http://localhost:xxxxx/Movies` 會路由傳送至 `Movies` 控制器的預設 `Index` 動作方法。</span><span class="sxs-lookup"><span data-stu-id="e4e66-137">Because the application is relying on the default routing (defined in the *Global.asax* file), the browser request `http://localhost:xxxxx/Movies` is routed to the default `Index` action method of the `Movies` controller.</span></span> <span data-ttu-id="e4e66-138">換句話說，瀏覽器要求 `http://localhost:xxxxx/Movies` 與瀏覽器要求 `http://localhost:xxxxx/Movies/Index`有效。</span><span class="sxs-lookup"><span data-stu-id="e4e66-138">In other words, the browser request `http://localhost:xxxxx/Movies` is effectively the same as the browser request `http://localhost:xxxxx/Movies/Index`.</span></span> <span data-ttu-id="e4e66-139">結果是空的電影清單，因為您還沒有加入。</span><span class="sxs-lookup"><span data-stu-id="e4e66-139">The result is an empty list of movies, because you haven't added any yet.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image5.png)

## <a name="creating-a-movie"></a><span data-ttu-id="e4e66-140">建立電影</span><span class="sxs-lookup"><span data-stu-id="e4e66-140">Creating a Movie</span></span>

<span data-ttu-id="e4e66-141">選取 **Create New** 連結。</span><span class="sxs-lookup"><span data-stu-id="e4e66-141">Select the **Create New** link.</span></span> <span data-ttu-id="e4e66-142">輸入電影的一些詳細資料，然後按一下 [**建立**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="e4e66-142">Enter some details about a movie and then click the **Create** button.</span></span>

![](accessing-your-models-data-from-a-controller/_static/image6.png)

<span data-ttu-id="e4e66-143">按一下 [**建立**] 按鈕會導致表單張貼至伺服器，其中電影資訊會儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="e4e66-143">Clicking the **Create** button causes the form to be posted to the server, where the movie information is saved in the database.</span></span> <span data-ttu-id="e4e66-144">接著，您會被重新導向至 [ */Movies* URL]，您可以在清單中看到新建立的電影。</span><span class="sxs-lookup"><span data-stu-id="e4e66-144">You're then redirected to the */Movies* URL, where you can see the newly created movie in the listing.</span></span>

<span data-ttu-id="e4e66-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-145">[![IndexWhenHarryMet](accessing-your-models-data-from-a-controller/_static/image8.png)](accessing-your-models-data-from-a-controller/_static/image7.png)</span></span>

<span data-ttu-id="e4e66-146">建立幾個電影項目。</span><span class="sxs-lookup"><span data-stu-id="e4e66-146">Create a couple more movie entries.</span></span> <span data-ttu-id="e4e66-147">嘗試 **Edit**、**Details** 和 **Delete** 連結，這些連結都可以正常運作。</span><span class="sxs-lookup"><span data-stu-id="e4e66-147">Try the **Edit**, **Details**, and **Delete** links, which are all functional.</span></span>

## <a name="examining-the-generated-code"></a><span data-ttu-id="e4e66-148">檢查產生的程式碼</span><span class="sxs-lookup"><span data-stu-id="e4e66-148">Examining the Generated Code</span></span>

<span data-ttu-id="e4e66-149">開啟*Controllers\MoviesController.vb*檔案，並檢查產生的 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="e4e66-149">Open the *Controllers\MoviesController.vb* file and examine the generated `Index` method.</span></span> <span data-ttu-id="e4e66-150">具有 `Index` 方法的電影控制器部分如下所示。</span><span class="sxs-lookup"><span data-stu-id="e4e66-150">A portion of the movie controller with the `Index` method is shown below.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample1.vb)]

<span data-ttu-id="e4e66-151">如先前所述，來自 `MoviesController` 類別的下一行會具現化電影資料庫內容。</span><span class="sxs-lookup"><span data-stu-id="e4e66-151">The following line from the `MoviesController` class instantiates a movie database context, as described previously.</span></span> <span data-ttu-id="e4e66-152">您可以使用電影資料庫內容來查詢、編輯和刪除電影。</span><span class="sxs-lookup"><span data-stu-id="e4e66-152">You can use the movie database context to query, edit, and delete movies.</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample2.vb)]

<span data-ttu-id="e4e66-153">`Movies` 控制器的要求會傳回 movie 資料庫之 `Movies` 資料表中的所有專案，然後將結果傳遞至 `Index` view。</span><span class="sxs-lookup"><span data-stu-id="e4e66-153">A request to the `Movies` controller returns all the entries in the `Movies` table of the movie database and then passes the results to the `Index` view.</span></span>

## <a name="strongly-typed-models-and-the-model-keyword"></a><span data-ttu-id="e4e66-154">強型別模型和 @model 關鍵字</span><span class="sxs-lookup"><span data-stu-id="e4e66-154">Strongly Typed Models and the @model Keyword</span></span>

<span data-ttu-id="e4e66-155">稍早在本教學課程中，您已看到控制器如何使用 `ViewBag` 物件，將資料或物件傳遞至視圖範本。</span><span class="sxs-lookup"><span data-stu-id="e4e66-155">Earlier in this tutorial, you saw how a controller can pass data or objects to a view template using the `ViewBag` object.</span></span> <span data-ttu-id="e4e66-156">`ViewBag` 是動態物件，可提供方便的晚期繫結方式，將資訊傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="e4e66-156">The `ViewBag` is a dynamic object that provides a convenient late-bound way to pass information to a view.</span></span>

<span data-ttu-id="e4e66-157">ASP.NET MVC 也提供將強型別資料或物件傳遞至視圖範本的能力。</span><span class="sxs-lookup"><span data-stu-id="e4e66-157">ASP.NET MVC also provides the ability to pass strongly typed data or objects to a view template.</span></span> <span data-ttu-id="e4e66-158">這個強型別方法可讓您更妥善地編譯器代碼，以及在 Visual Web Developer editor 中更豐富的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="e4e66-158">This strongly typed approach enables better compile-time checking of your code and richer IntelliSense in the Visual Web Developer editor.</span></span> <span data-ttu-id="e4e66-159">我們會將此方法與 `MoviesController` 類別和*Index. vbhtml*視圖範本搭配使用。</span><span class="sxs-lookup"><span data-stu-id="e4e66-159">We're using this approach with the `MoviesController` class and *Index.vbhtml* view template.</span></span>

<span data-ttu-id="e4e66-160">請注意，當程式碼在 `Index` 動作方法中呼叫 `View` helper 方法時，如何建立[`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx)物件。</span><span class="sxs-lookup"><span data-stu-id="e4e66-160">Notice how the code creates a [`List`](https://msdn.microsoft.com/library/6sh2ey19.aspx) object when it calls the `View` helper method in the `Index` action method.</span></span> <span data-ttu-id="e4e66-161">然後，此程式碼會將此 `Movies` 清單從控制器傳遞至視圖：</span><span class="sxs-lookup"><span data-stu-id="e4e66-161">The code then passes this `Movies` list from the controller to the view:</span></span>

[!code-vb[Main](accessing-your-models-data-from-a-controller/samples/sample3.vb)]

<span data-ttu-id="e4e66-162">藉由在視圖範本檔案的頂端包含 `@ModelType` 語句，您可以指定此視圖所預期的物件類型。</span><span class="sxs-lookup"><span data-stu-id="e4e66-162">By including a `@ModelType` statement at the top of the view template file, you can specify the type of object that the view expects.</span></span> <span data-ttu-id="e4e66-163">當您建立電影控制器時，Visual Web Developer 會自動將下列 `@model` 語句加入至位於*Index. vbhtml*檔案的頂端：</span><span class="sxs-lookup"><span data-stu-id="e4e66-163">When you created the movie controller, Visual Web Developer automatically included the following `@model` statement at the top of the *Index.vbhtml* file:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample4.vbhtml)]

<span data-ttu-id="e4e66-164">此 `@ModelType` 指示詞可讓您使用強型別的 `Model` 物件，來存取控制器傳遞至視圖的電影清單。</span><span class="sxs-lookup"><span data-stu-id="e4e66-164">This `@ModelType` directive allows you to access the list of movies that the controller passed to the view by using a `Model` object that's strongly typed.</span></span> <span data-ttu-id="e4e66-165">例如，在*Index. vbhtml*範本中，程式碼會對強型別 `Model` 物件執行 `foreach` 語句，藉以迴圈播放電影：</span><span class="sxs-lookup"><span data-stu-id="e4e66-165">For example, in the *Index.vbhtml* template, the code loops through the movies by doing a `foreach` statement over the strongly typed `Model` object:</span></span>

[!code-vbhtml[Main](accessing-your-models-data-from-a-controller/samples/sample5.vbhtml)]

<span data-ttu-id="e4e66-166">因為 `Model` 物件是強型別（做為 `IEnumerable<Movie>` 物件），所以迴圈中的每個 `item` 物件都會輸入為 `Movie`。</span><span class="sxs-lookup"><span data-stu-id="e4e66-166">Because the `Model` object is strongly typed (as an `IEnumerable<Movie>` object), each `item` object in the loop is typed as `Movie`.</span></span> <span data-ttu-id="e4e66-167">除了其他優點外，這也表示您可以在程式碼編輯器中，取得程式碼的編譯時期檢查和完整的 IntelliSense 支援：</span><span class="sxs-lookup"><span data-stu-id="e4e66-167">Among other benefits, this means that you get compile-time checking of the code and full IntelliSense support in the code editor:</span></span>

<span data-ttu-id="e4e66-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-168">[![5_Intellisense](accessing-your-models-data-from-a-controller/_static/image10.png)](accessing-your-models-data-from-a-controller/_static/image9.png)</span></span>

## <a name="working-with-sql-server-compact"></a><span data-ttu-id="e4e66-169">使用 SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="e4e66-169">Working with SQL Server Compact</span></span>

<span data-ttu-id="e4e66-170">Entity Framework Code First 偵測到所提供的資料庫連接字串指向尚未存在的 `Movies` 資料庫，因此 Code First 自動建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="e4e66-170">Entity Framework Code First detected that the database connection string that was provided pointed to a `Movies` database that didn't exist yet, so Code First created the database automatically.</span></span> <span data-ttu-id="e4e66-171">您可以藉由查看*應用程式\_Data*資料夾來確認它是否已建立。</span><span class="sxs-lookup"><span data-stu-id="e4e66-171">You can verify that it's been created by looking in the *App\_Data* folder.</span></span> <span data-ttu-id="e4e66-172">如果您看不到 [*電影 .sdf* ] 檔案，請按一下 [**方案總管**] 工具列中的 [**顯示所有**檔案] 按鈕，按一下 [重新整理 **] 按鈕，** 然後展開 [*應用程式\_* 資料夾]。</span><span class="sxs-lookup"><span data-stu-id="e4e66-172">If you don't see the *Movies.sdf* file, click the **Show All Files** button in the **Solution Explorer** toolbar, click the **Refresh** button, and then expand the *App\_Data* folder.</span></span>

<span data-ttu-id="e4e66-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-173">[![SDF_in_SolnExp](accessing-your-models-data-from-a-controller/_static/image12.png)](accessing-your-models-data-from-a-controller/_static/image11.png)</span></span>

<span data-ttu-id="e4e66-174">按兩下 [ *.sdf* ] 以開啟**伺服器總管**。</span><span class="sxs-lookup"><span data-stu-id="e4e66-174">Double-click *Movies.sdf* to open **Server Explorer**.</span></span> <span data-ttu-id="e4e66-175">然後展開 [**資料表]** 資料夾，以查看已在資料庫中建立的資料表。</span><span class="sxs-lookup"><span data-stu-id="e4e66-175">Then expand the **Tables** folder to see the tables that have been created in the database.</span></span>

> [!NOTE]
> <span data-ttu-id="e4e66-176">如果您按兩下 [ *.sdf*] 時出現錯誤，請確定您已安裝**適用于 SQL Server Compact 4.0 的 Visual Studio 2010 SP1 工具**。</span><span class="sxs-lookup"><span data-stu-id="e4e66-176">If you get an error when you double-click *Movies.sdf*, make sure you've installed **Visual Studio 2010 SP1 Tools for SQL Server Compact 4.0**.</span></span> <span data-ttu-id="e4e66-177">（如需軟體的連結，請參閱本教學課程系列的第1部分中的必要條件清單）。如果您現在安裝發行，就必須關閉並重新開啟 Visual Web Developer。</span><span class="sxs-lookup"><span data-stu-id="e4e66-177">(For links to the software, see the list of prerequisites in part 1 of this tutorial series.) If you install the release now, you'll have to close and re-open Visual Web Developer.</span></span>

<span data-ttu-id="e4e66-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-178">[![DB_explorer](accessing-your-models-data-from-a-controller/_static/image14.png)](accessing-your-models-data-from-a-controller/_static/image13.png)</span></span>

<span data-ttu-id="e4e66-179">有兩個數據表，一個用於 `Movie` 實體集，然後是 `EdmMetadata` 資料表。</span><span class="sxs-lookup"><span data-stu-id="e4e66-179">There are two tables, one for the `Movie` entity set and then the `EdmMetadata` table.</span></span> <span data-ttu-id="e4e66-180">Entity Framework 會使用 `EdmMetadata` 資料表來判斷模型和資料庫何時未同步。</span><span class="sxs-lookup"><span data-stu-id="e4e66-180">The `EdmMetadata` table is used by the Entity Framework to determine when the model and the database are out of sync.</span></span>

<span data-ttu-id="e4e66-181">以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**顯示資料表資料**] 以查看您所建立的資料。</span><span class="sxs-lookup"><span data-stu-id="e4e66-181">Right-click the `Movies` table and select **Show Table Data** to see the data you created.</span></span>

<span data-ttu-id="e4e66-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-182">[![MoviesTable](accessing-your-models-data-from-a-controller/_static/image16.png)](accessing-your-models-data-from-a-controller/_static/image15.png)</span></span>

<span data-ttu-id="e4e66-183">以滑鼠右鍵按一下 [`Movies`] 資料表，然後選取 [**編輯資料表架構**]。</span><span class="sxs-lookup"><span data-stu-id="e4e66-183">Right-click the `Movies` table and select **Edit Table Schema**.</span></span>

<span data-ttu-id="e4e66-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-184">[![EditTableSchema](accessing-your-models-data-from-a-controller/_static/image18.png)](accessing-your-models-data-from-a-controller/_static/image17.png)</span></span>

![TableSchemaSM](accessing-your-models-data-from-a-controller/_static/image19.png)

<span data-ttu-id="e4e66-186">請注意 `Movies` 資料表的架構如何對應至您稍早建立的 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="e4e66-186">Notice how the schema of the `Movies` table maps to the `Movie` class you created earlier.</span></span> <span data-ttu-id="e4e66-187">Entity Framework Code First 會根據您的 `Movie` 類別，自動為您建立此架構。</span><span class="sxs-lookup"><span data-stu-id="e4e66-187">Entity Framework Code First automatically created this schema for you based on your `Movie` class.</span></span>

<span data-ttu-id="e4e66-188">當您完成時，請關閉連線。</span><span class="sxs-lookup"><span data-stu-id="e4e66-188">When you're finished, close the connection.</span></span> <span data-ttu-id="e4e66-189">（如果您不關閉連線，下次執行專案時可能會出現錯誤）。</span><span class="sxs-lookup"><span data-stu-id="e4e66-189">(If you don't close the connection, you might get an error the next time you run the project).</span></span>

<span data-ttu-id="e4e66-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="e4e66-190">[![CloseConnection](accessing-your-models-data-from-a-controller/_static/image21.png)](accessing-your-models-data-from-a-controller/_static/image20.png)</span></span>

<span data-ttu-id="e4e66-191">您現在已擁有資料庫和簡單的清單頁面，可顯示其內容。</span><span class="sxs-lookup"><span data-stu-id="e4e66-191">You now have the database and a simple listing page to display content from it.</span></span> <span data-ttu-id="e4e66-192">在下一個教學課程中，我們將檢查 scaffold 程式碼的其餘部分，並新增 `SearchIndex` 方法和 `SearchIndex` 視圖，讓您在此資料庫中搜尋電影。</span><span class="sxs-lookup"><span data-stu-id="e4e66-192">In the next tutorial, we'll examine the rest of the scaffolded code and add a `SearchIndex` method and a `SearchIndex` view that lets you search for movies in this database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="e4e66-193">[上一頁](adding-a-model.md)
> [下一頁](examining-the-edit-methods-and-edit-view.md)</span><span class="sxs-lookup"><span data-stu-id="e4e66-193">[Previous](adding-a-model.md)
[Next](examining-the-edit-methods-and-edit-view.md)</span></span>
