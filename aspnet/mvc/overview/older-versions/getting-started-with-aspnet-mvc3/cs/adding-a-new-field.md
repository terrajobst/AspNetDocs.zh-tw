---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
title: 將新欄位新增至電影模型和資料表（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: b4e76c1a-f66e-43a0-aa72-f39df79c07c1
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: 40b02a2f608f07091ce6b5339688a1e6290e2e37
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540800"
---
# <a name="adding-a-new-field-to-the-movie-model-and-table-c"></a><span data-ttu-id="a6818-103">將新欄位新增至電影模型和資料表 (C#)</span><span class="sxs-lookup"><span data-stu-id="a6818-103">Adding a New Field to the Movie Model and Table (C#)</span></span>

<span data-ttu-id="a6818-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="a6818-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="a6818-105">本教學課程的更新版本可在[這裡](../../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="a6818-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="a6818-106">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="a6818-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="a6818-107">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="a6818-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="a6818-108">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="a6818-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="a6818-109">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="a6818-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="a6818-110">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="a6818-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="a6818-111">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="a6818-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="a6818-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="a6818-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="a6818-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="a6818-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="a6818-114">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="a6818-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="a6818-115">本主題提供具有C#原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="a6818-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="a6818-116">[下載C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="a6818-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="a6818-117">如果您偏好 Visual Basic，請切換到本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="a6818-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="a6818-118">在本節中，您將對模型類別進行一些變更，並瞭解如何更新資料庫架構，以符合模型的變更。</span><span class="sxs-lookup"><span data-stu-id="a6818-118">In this section you'll make some changes to the model classes and learn how you can update the database schema to match the model changes.</span></span>

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="a6818-119">將 Rating 屬性新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="a6818-119">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="a6818-120">首先，將新的 `Rating` 屬性加入至現有的 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="a6818-120">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="a6818-121">開啟*Movie.cs*檔案，然後加入 `Rating` 屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6818-121">Open the *Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="a6818-122">完整的 `Movie` 類別現在看起來像下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="a6818-122">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

<span data-ttu-id="a6818-123">使用 [ **Debug** &gt;**組建電影**] 功能表命令來重新編譯應用程式。</span><span class="sxs-lookup"><span data-stu-id="a6818-123">Recompile the application using the **Debug** &gt;**Build Movie** menu command.</span></span>

<span data-ttu-id="a6818-124">既然您已更新 `Model` 類別，您也必須更新 *\Views\Movies\Index.cshtml*和 *\Views\Movies\Create.cshtml* view 範本，才能支援新的 `Rating` 屬性。</span><span class="sxs-lookup"><span data-stu-id="a6818-124">Now that you've updated the `Model` class, you also need to update the *\Views\Movies\Index.cshtml* and *\Views\Movies\Create.cshtml* view templates in order to support the new `Rating` property.</span></span>

<span data-ttu-id="a6818-125">開啟 *\Views\Movies\Index.cshtml*檔案，然後在 [**價格**] 資料行的正後方加入 `<th>Rating</th>` 欄標題。</span><span class="sxs-lookup"><span data-stu-id="a6818-125">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="a6818-126">然後在範本結尾附近新增 `<td>` 資料行，以轉譯 `@item.Rating` 值。</span><span class="sxs-lookup"><span data-stu-id="a6818-126">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="a6818-127">以下是更新的*Index. cshtml*視圖範本的樣子：</span><span class="sxs-lookup"><span data-stu-id="a6818-127">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample3.cshtml)]

<span data-ttu-id="a6818-128">接下來，開啟 *\Views\Movies\Create.cshtml*檔案，並在接近表單結尾處新增下列標記。</span><span class="sxs-lookup"><span data-stu-id="a6818-128">Next, open the *\Views\Movies\Create.cshtml* file and add the following markup near the end of the form.</span></span> <span data-ttu-id="a6818-129">這會轉譯一個文字方塊，讓您可以在建立新電影時指定評等。</span><span class="sxs-lookup"><span data-stu-id="a6818-129">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample4.cshtml)]

## <a name="managing-model-and-database-schema-differences"></a><span data-ttu-id="a6818-130">管理模型和資料庫架構的差異</span><span class="sxs-lookup"><span data-stu-id="a6818-130">Managing Model and Database Schema Differences</span></span>

<span data-ttu-id="a6818-131">您現已更新應用程式代碼，以支援新的 `Rating` 屬性。</span><span class="sxs-lookup"><span data-stu-id="a6818-131">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="a6818-132">現在執行應用程式，並流覽至 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="a6818-132">Now run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="a6818-133">不過，當您這麼做時，您會看到下列錯誤：</span><span class="sxs-lookup"><span data-stu-id="a6818-133">When you do this, though, you'll see the following error:</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="a6818-134">您看到這個錯誤是因為應用程式中更新的 `Movie` 模型類別，現在與現有資料庫 `Movie` 資料表的架構不同。</span><span class="sxs-lookup"><span data-stu-id="a6818-134">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="a6818-135">(資料庫資料表中沒有任何 `Rating` 資料行)。</span><span class="sxs-lookup"><span data-stu-id="a6818-135">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="a6818-136">根據預設，當您使用 Entity Framework Code First 自動建立資料庫時（如您稍早在本教學課程中所做的），Code First 會將資料表新增至資料庫，以協助追蹤資料庫的架構是否與其產生的模型類別同步。</span><span class="sxs-lookup"><span data-stu-id="a6818-136">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="a6818-137">如果它們不是同步的，Entity Framework 會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="a6818-137">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="a6818-138">這可讓您更輕鬆地在開發期間追蹤問題，而您可能只會在執行時間發現（藉由隱匿錯誤）。</span><span class="sxs-lookup"><span data-stu-id="a6818-138">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span> <span data-ttu-id="a6818-139">同步檢查功能會造成您剛才看到的錯誤訊息顯示出來。</span><span class="sxs-lookup"><span data-stu-id="a6818-139">The sync-checking feature is what causes the error message to be displayed that you just saw.</span></span>

<span data-ttu-id="a6818-140">有兩種方法可以解決此錯誤：</span><span class="sxs-lookup"><span data-stu-id="a6818-140">There are two approaches to resolving the error:</span></span>

1. <span data-ttu-id="a6818-141">讓 Entity Framework 自動卸除資料庫，並重新依據新的模型類別結構描述來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="a6818-141">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="a6818-142">在測試資料庫上進行開發時，這個方法非常方便，因為它可讓您快速地將模型和資料庫架構進化在一起。</span><span class="sxs-lookup"><span data-stu-id="a6818-142">This approach is very convenient when doing active development on a test database, because it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="a6818-143">不過，缺點是您會遺失資料庫中的現有資料，因此您*不*會想要在生產資料庫上使用此方法！</span><span class="sxs-lookup"><span data-stu-id="a6818-143">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span>
2. <span data-ttu-id="a6818-144">您可明確修改現有資料庫的結構描述，使其符合模型類別。</span><span class="sxs-lookup"><span data-stu-id="a6818-144">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="a6818-145">這種方法的優點是可以保留您的資料。</span><span class="sxs-lookup"><span data-stu-id="a6818-145">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="a6818-146">您可以手動方式或藉由建立資料庫變更指令碼來進行這項變更。</span><span class="sxs-lookup"><span data-stu-id="a6818-146">You can make this change either manually or by creating a database change script.</span></span>

<span data-ttu-id="a6818-147">在本教學課程中，我們將使用第一種方法，您會在模型變更時，讓 Entity Framework Code First 自動重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="a6818-147">For this tutorial, we'll use the first approach — you'll have the Entity Framework Code First automatically re-create the database anytime the model changes.</span></span>

## <a name="automatically-re-creating-the-database-on-model-changes"></a><span data-ttu-id="a6818-148">在模型變更時自動重新建立資料庫</span><span class="sxs-lookup"><span data-stu-id="a6818-148">Automatically Re-Creating the Database on Model Changes</span></span>

<span data-ttu-id="a6818-149">讓我們更新應用程式，如此一來，每當您變更應用程式的模型時，Code First 就會自動卸載並重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="a6818-149">Let's update the application so that Code First automatically drops and re-creates the database anytime you change the model for the application.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="a6818-150">**警告**只有當您使用開發或測試資料庫，而*不*是在包含實際資料的生產資料庫上時，才應該啟用這種方法來自動卸載和重新建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="a6818-150">**Warning** You should enable this approach of automatically dropping and re-creating the database only when you're using a development or test database, and *never* on a production database that contains real data.</span></span> <span data-ttu-id="a6818-151">在實際伺服器上使用它可能會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="a6818-151">Using it on a production server can lead to data loss.</span></span>

<span data-ttu-id="a6818-152">在**方案總管**中，以滑鼠右鍵按一下 [*模型*] 資料夾，選取 [**新增**]，然後選取 [**類別**]。</span><span class="sxs-lookup"><span data-stu-id="a6818-152">In **Solution Explorer**, right click the *Models* folder, select **Add**, and then select **Class**.</span></span>

![](adding-a-new-field/_static/image2.png)

<span data-ttu-id="a6818-153">將類別命名為 "MovieInitializer"。</span><span class="sxs-lookup"><span data-stu-id="a6818-153">Name the class "MovieInitializer".</span></span> <span data-ttu-id="a6818-154">更新 `MovieInitializer` 類別，以包含下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="a6818-154">Update the `MovieInitializer` class to contain the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="a6818-155">`MovieInitializer` 類別指定模型所使用的資料庫應該卸載，並在模型類別變更時自動重新建立。</span><span class="sxs-lookup"><span data-stu-id="a6818-155">The `MovieInitializer` class specifies that the database used by the model should be dropped and automatically re-created if the model classes ever change.</span></span> <span data-ttu-id="a6818-156">程式碼包含 `Seed` 方法，可指定在建立（或重新建立）時自動新增至資料庫的一些預設資料。</span><span class="sxs-lookup"><span data-stu-id="a6818-156">The code includes a `Seed` method to specify some default data to automatically add to the database any time it's created (or re-created).</span></span> <span data-ttu-id="a6818-157">這可讓您在資料庫中填入一些範例資料，而不需要您在每次進行模型變更時手動填入。</span><span class="sxs-lookup"><span data-stu-id="a6818-157">This provides a useful way to populate the database with some sample data, without requiring you to manually populate it each time you make a model change.</span></span>

<span data-ttu-id="a6818-158">既然您已定義 `MovieInitializer` 類別，您會想要將它連接，以便每次應用程式執行時，它會檢查模型類別是否與資料庫中的架構不同。</span><span class="sxs-lookup"><span data-stu-id="a6818-158">Now that you've defined the `MovieInitializer` class, you'll want to wire it up so that each time the application runs, it checks whether the model classes are different from the schema in the database.</span></span> <span data-ttu-id="a6818-159">如果是，您可以執行初始化運算式來重新建立資料庫，以符合模型，然後在資料庫中填入範例資料。</span><span class="sxs-lookup"><span data-stu-id="a6818-159">If they are, you can run the initializer to re-create the database to match the model and then populate the database with the sample data.</span></span>

<span data-ttu-id="a6818-160">開啟位於 `MvcMovies` 專案根目錄的*global.asax*檔案：</span><span class="sxs-lookup"><span data-stu-id="a6818-160">Open the *Global.asax* file that's at the root of the `MvcMovies` project:</span></span>

[![](adding-a-new-field/_static/image4.png)](adding-a-new-field/_static/image3.png)

<span data-ttu-id="a6818-161">*Global.asax*檔案包含定義專案之整個應用程式的類別，並且包含在應用程式第一次啟動時執行的 `Application_Start` 事件處理常式。</span><span class="sxs-lookup"><span data-stu-id="a6818-161">The *Global.asax* file contains the class that defines the entire application for the project, and contains an `Application_Start` event handler that runs when the application first starts.</span></span>

<span data-ttu-id="a6818-162">讓我們在檔案頂端新增兩個 using 語句。</span><span class="sxs-lookup"><span data-stu-id="a6818-162">Let's add two using statements to the top of the file.</span></span> <span data-ttu-id="a6818-163">第一個參考 Entity Framework 命名空間，而第二個參考 `MovieInitializer` 類別所在的命名空間：</span><span class="sxs-lookup"><span data-stu-id="a6818-163">The first references the Entity Framework namespace, and the second references the namespace where our `MovieInitializer` class lives:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs)]

<span data-ttu-id="a6818-164">然後尋找 `Application_Start` 方法，並在方法的開頭新增對 `Database.SetInitializer` 的呼叫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="a6818-164">Then find the `Application_Start` method and add a call to `Database.SetInitializer` at the beginning of the method, as shown below:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs)]

<span data-ttu-id="a6818-165">您剛才加入的 `Database.SetInitializer` 語句指出，如果架構和資料庫不相符，就應該自動刪除和重新建立 `MovieDBContext` 實例所使用的資料庫。</span><span class="sxs-lookup"><span data-stu-id="a6818-165">The `Database.SetInitializer` statement you just added indicates that the database used by the `MovieDBContext` instance should be automatically deleted and re-created if the schema and the database don't match.</span></span> <span data-ttu-id="a6818-166">如您所見，它也會將 `MovieInitializer` 類別中所指定的範例資料填入資料庫中。</span><span class="sxs-lookup"><span data-stu-id="a6818-166">And as you saw, it will also populate the database with the sample data that's specified in the `MovieInitializer` class.</span></span>

<span data-ttu-id="a6818-167">關閉*global.asax*檔案。</span><span class="sxs-lookup"><span data-stu-id="a6818-167">Close the *Global.asax* file.</span></span>

<span data-ttu-id="a6818-168">重新執行應用程式，並流覽至 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="a6818-168">Re-run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="a6818-169">當應用程式啟動時，它會偵測模型結構不再符合資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="a6818-169">When the application starts, it detects that the model structure no longer matches the database schema.</span></span> <span data-ttu-id="a6818-170">它會自動重新建立資料庫，以符合新的模型結構，並在資料庫中填入範例電影：</span><span class="sxs-lookup"><span data-stu-id="a6818-170">It automatically re-creates the database to match the new model structure and populates the database with the sample movies:</span></span>

![7_MyMovieList_SM](adding-a-new-field/_static/image5.png)

<span data-ttu-id="a6818-172">按一下 [**建立新**的] 連結以新增電影。</span><span class="sxs-lookup"><span data-stu-id="a6818-172">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="a6818-173">請注意，您可以加入評等。</span><span class="sxs-lookup"><span data-stu-id="a6818-173">Note that you can add a rating.</span></span>

<span data-ttu-id="a6818-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="a6818-174">[![7_CreateRioII](adding-a-new-field/_static/image7.png)](adding-a-new-field/_static/image6.png)</span></span>

<span data-ttu-id="a6818-175">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="a6818-175">Click **Create**.</span></span> <span data-ttu-id="a6818-176">新電影（包括評等）現在會顯示在電影清單中：</span><span class="sxs-lookup"><span data-stu-id="a6818-176">The new movie, including the rating, now shows up in the movies listing:</span></span>

<span data-ttu-id="a6818-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="a6818-177">[![7_ourNewMovie_SM](adding-a-new-field/_static/image9.png)](adding-a-new-field/_static/image8.png)</span></span>

<span data-ttu-id="a6818-178">在本節中，您會看到如何修改模型物件，並讓資料庫與變更保持同步。</span><span class="sxs-lookup"><span data-stu-id="a6818-178">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="a6818-179">您也學到以範例資料填入新建立資料庫的方法，讓您可以試試看案例。</span><span class="sxs-lookup"><span data-stu-id="a6818-179">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="a6818-180">接下來，我們將探討如何將更豐富的驗證邏輯新增至模型類別，並讓某些商務規則得以強制執行。</span><span class="sxs-lookup"><span data-stu-id="a6818-180">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a6818-181">[上一頁](examining-the-edit-methods-and-edit-view.md)
> [下一頁](adding-validation-to-the-model.md)</span><span class="sxs-lookup"><span data-stu-id="a6818-181">[Previous](examining-the-edit-methods-and-edit-view.md)
[Next](adding-validation-to-the-model.md)</span></span>
