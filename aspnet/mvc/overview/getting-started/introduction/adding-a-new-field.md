---
uid: mvc/overview/getting-started/introduction/adding-a-new-field
title: 加入新的欄位 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: 4085de68-d243-4378-8a64-86236ea8d2da
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-new-field
msc.type: authoredcontent
ms.openlocfilehash: d79655bfadff83095bf4cb84445f5efaf44d6a89
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519072"
---
# <a name="adding-a-new-field"></a><span data-ttu-id="31bb3-102">新增欄位</span><span class="sxs-lookup"><span data-stu-id="31bb3-102">Adding a New Field</span></span>

<span data-ttu-id="31bb3-103">依[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="31bb3-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="31bb3-104">在本節中，您將使用 Entity Framework Code First 移轉來遷移模型類別的某些變更，以便將變更套用至資料庫。</span><span class="sxs-lookup"><span data-stu-id="31bb3-104">In this section you'll use Entity Framework Code First Migrations to migrate some changes to the model classes so the change is applied to the database.</span></span>

<span data-ttu-id="31bb3-105">根據預設，當您使用 Entity Framework Code First 自動建立資料庫時（如您稍早在本教學課程中所做的），Code First 會將資料表新增至資料庫，以協助追蹤資料庫的架構是否與其產生的模型類別同步。</span><span class="sxs-lookup"><span data-stu-id="31bb3-105">By default, when you use Entity Framework Code First to automatically create a database, as you did earlier in this tutorial, Code First adds a table to the database to help track whether the schema of the database is in sync with the model classes it was generated from.</span></span> <span data-ttu-id="31bb3-106">如果它們不是同步的，Entity Framework 會擲回錯誤。</span><span class="sxs-lookup"><span data-stu-id="31bb3-106">If they aren't in sync, the Entity Framework throws an error.</span></span> <span data-ttu-id="31bb3-107">這可讓您更輕鬆地在開發期間追蹤問題，而您可能只會在執行時間發現（藉由隱匿錯誤）。</span><span class="sxs-lookup"><span data-stu-id="31bb3-107">This makes it easier to track down issues at development time that you might otherwise only find (by obscure errors) at run time.</span></span>

## <a name="setting-up-code-first-migrations-for-model-changes"></a><span data-ttu-id="31bb3-108">設定模型變更的 Code First 移轉</span><span class="sxs-lookup"><span data-stu-id="31bb3-108">Setting up Code First Migrations for Model Changes</span></span>

<span data-ttu-id="31bb3-109">流覽至方案總管。</span><span class="sxs-lookup"><span data-stu-id="31bb3-109">Navigate to Solution Explorer.</span></span> <span data-ttu-id="31bb3-110">以滑鼠右鍵按一下 [ *.mdf* ] 檔案，然後選取 [**刪除**] 以移除電影資料庫。</span><span class="sxs-lookup"><span data-stu-id="31bb3-110">Right click on the *Movies.mdf* file and select **Delete** to remove the movies database.</span></span> <span data-ttu-id="31bb3-111">如果看不到 [*電影 .mdf* ] 檔案，請按一下紅色外框下方顯示的 [**顯示所有**檔案] 圖示。</span><span class="sxs-lookup"><span data-stu-id="31bb3-111">If you don't see the *Movies.mdf* file, click on the **Show All Files** icon shown below in the red outline.</span></span>

![](adding-a-new-field/_static/image1.png)

<span data-ttu-id="31bb3-112">建置應用程式，確定沒有任何錯誤。</span><span class="sxs-lookup"><span data-stu-id="31bb3-112">Build the application to make sure there are no errors.</span></span>

<span data-ttu-id="31bb3-113">在 [工具] 功能表中按一下 [NuGet 套件管理員]，然後按一下 [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="31bb3-113">From the **Tools** menu, click **NuGet Package Manager** and then **Package Manager Console**.</span></span>

![新增套件手冊](adding-a-new-field/_static/image2.png)

<span data-ttu-id="31bb3-115">在 [**套件管理員主控台**] 視窗中，于 `PM>` 提示字元輸入</span><span class="sxs-lookup"><span data-stu-id="31bb3-115">In the **Package Manager Console** window at the `PM>` prompt enter</span></span>

<span data-ttu-id="31bb3-116">啟用-遷移-CoNtextTypeName MvcMovie。 MovieDBCoNtext</span><span class="sxs-lookup"><span data-stu-id="31bb3-116">Enable-Migrations -ContextTypeName MvcMovie.Models.MovieDBContext</span></span>

![](adding-a-new-field/_static/image3.png)

<span data-ttu-id="31bb3-117">[**啟用-遷移**] 命令（如上所示）會在新的 [*遷移*] 資料夾中建立*Configuration.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="31bb3-117">The **Enable-Migrations** command (shown above) creates a *Configuration.cs* file in a new *Migrations* folder.</span></span>

![](adding-a-new-field/_static/image4.png)

<span data-ttu-id="31bb3-118">Visual Studio 會開啟*Configuration.cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="31bb3-118">Visual Studio opens the *Configuration.cs* file.</span></span> <span data-ttu-id="31bb3-119">使用下列程式碼取代*Configuration.cs*檔案中的 `Seed` 方法：</span><span class="sxs-lookup"><span data-stu-id="31bb3-119">Replace the `Seed` method in the *Configuration.cs* file with the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample1.cs)]

<span data-ttu-id="31bb3-120">將滑鼠停留在 `Movie` 底下的紅色曲線上，然後按一下 `Show Potential Fixes` 然後按一下 **使用** **MvcMovie。**</span><span class="sxs-lookup"><span data-stu-id="31bb3-120">Hover over the red squiggly line under `Movie` and click `Show Potential Fixes` and then click **using** **MvcMovie.Models;**</span></span>

![](adding-a-new-field/_static/image5.png)

<span data-ttu-id="31bb3-121">這麼做會加入下列 using 語句：</span><span class="sxs-lookup"><span data-stu-id="31bb3-121">Doing so adds the following using statement:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample2.cs)]

> [!NOTE]
> 
> <span data-ttu-id="31bb3-122">Code First 移轉會在每次遷移之後呼叫 `Seed` 方法（也就是在套件管理員主控台中呼叫**update-database** ），而這個方法會更新已插入的資料列，如果尚未存在，則會將其插入。</span><span class="sxs-lookup"><span data-stu-id="31bb3-122">Code First Migrations calls the `Seed` method after every migration (that is, calling **update-database** in the Package Manager Console), and this method updates rows that have already been inserted, or inserts them if they don't exist yet.</span></span>
> 
> <span data-ttu-id="31bb3-123">下列程式碼中的[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法會執行「upsert」作業：</span><span class="sxs-lookup"><span data-stu-id="31bb3-123">The [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method in the following code performs an "upsert" operation:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample3.cs)]
> 
> <span data-ttu-id="31bb3-124">因為在每次遷移時都會執行[種子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法，所以您不能只插入資料，因為在第一次建立資料庫的遷移之後，您嘗試加入的資料列已經存在。</span><span class="sxs-lookup"><span data-stu-id="31bb3-124">Because the [Seed](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx) method runs with every migration, you can't just insert data, because the rows you are trying to add will already be there after the first migration that creates the database.</span></span> <span data-ttu-id="31bb3-125">如果您嘗試插入已經存在的資料列，則 "[upsert](http://en.wikipedia.org/wiki/Upsert)" 作業會防止發生錯誤，但它會覆寫您在測試應用程式時所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="31bb3-125">The "[upsert](http://en.wikipedia.org/wiki/Upsert)" operation prevents errors that would happen if you try to insert a row that already exists, but it overrides any changes to data that you may have made while testing the application.</span></span> <span data-ttu-id="31bb3-126">在某些資料表中使用測試資料時，您可能不會想要這樣做：在某些情況下，當您在測試時變更資料，而您想要在資料庫更新之後維持變更。</span><span class="sxs-lookup"><span data-stu-id="31bb3-126">With test data in some tables you might not want that to happen: in some cases when you change data while testing you want your changes to remain after database updates.</span></span> <span data-ttu-id="31bb3-127">在此情況下，您想要執行條件式插入作業：只有在不存在資料列時，才插入它。</span><span class="sxs-lookup"><span data-stu-id="31bb3-127">In that case you want to do a conditional insert operation: insert a row only if it doesn't already exist.</span></span>   
> 
> <span data-ttu-id="31bb3-128">傳遞至[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法的第一個參數會指定要用來檢查資料列是否已經存在的屬性。</span><span class="sxs-lookup"><span data-stu-id="31bb3-128">The first parameter passed to the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method specifies the property to use to check if a row already exists.</span></span> <span data-ttu-id="31bb3-129">對於您所提供的測試電影資料，`Title` 屬性可以用於此用途，因為清單中的每個標題都是唯一的：</span><span class="sxs-lookup"><span data-stu-id="31bb3-129">For the test movie data that you are providing, the `Title` property can be used for this purpose since each title in the list is unique:</span></span>
> 
> [!code-csharp[Main](adding-a-new-field/samples/sample4.cs)]
> 
> <span data-ttu-id="31bb3-130">此程式碼假設標題是唯一的。</span><span class="sxs-lookup"><span data-stu-id="31bb3-130">This code assumes that titles are unique.</span></span> <span data-ttu-id="31bb3-131">如果您手動新增重複的標題，則會在下一次執行遷移時收到下列例外狀況。</span><span class="sxs-lookup"><span data-stu-id="31bb3-131">If you manually add a duplicate title, you'll get the following exception the next time you perform a migration.</span></span>   
> 
> <span data-ttu-id="31bb3-132">*序列包含一個以上的元素*</span><span class="sxs-lookup"><span data-stu-id="31bb3-132">*Sequence contains more than one element*</span></span>  
> 
> <span data-ttu-id="31bb3-133">如需[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法的詳細資訊，請參閱[使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。</span><span class="sxs-lookup"><span data-stu-id="31bb3-133">For more information about the [AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx) method, see [Take care with EF 4.3 AddOrUpdate Method](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)..</span></span>

<span data-ttu-id="31bb3-134">**按下 CTRL-SHIFT-B 以建立專案。** （如果您目前未建立，下列步驟將會失敗）。</span><span class="sxs-lookup"><span data-stu-id="31bb3-134">**Press CTRL-SHIFT-B to build the project.**(The following steps will fail if you don't build at this point.)</span></span>

<span data-ttu-id="31bb3-135">下一個步驟是建立初始遷移的 `DbMigration` 類別。</span><span class="sxs-lookup"><span data-stu-id="31bb3-135">The next step is to create a `DbMigration` class for the initial migration.</span></span> <span data-ttu-id="31bb3-136">這個遷移會建立新的資料庫，這就是您在上一個步驟中刪除*movie .mdf*檔案的原因。</span><span class="sxs-lookup"><span data-stu-id="31bb3-136">This migration creates a new database, that's why you deleted the *movie.mdf* file in a previous step.</span></span>

<span data-ttu-id="31bb3-137">在 [**套件管理員主控台**] 視窗中，輸入命令 `add-migration Initial` 以建立初始遷移。</span><span class="sxs-lookup"><span data-stu-id="31bb3-137">In the **Package Manager Console** window, enter the command `add-migration Initial` to create the initial migration.</span></span> <span data-ttu-id="31bb3-138">「初始」名稱是任意的，用來命名所建立的遷移檔案。</span><span class="sxs-lookup"><span data-stu-id="31bb3-138">The name "Initial" is arbitrary and is used to name the migration file created.</span></span>

![](adding-a-new-field/_static/image6.png)

<span data-ttu-id="31bb3-139">Code First 移轉會在 [*遷移*] 資料夾中建立另一個類別檔案（名稱為 *{DateStamp}\_Initial.cs* ），而此類別包含建立資料庫架構的程式碼。</span><span class="sxs-lookup"><span data-stu-id="31bb3-139">Code First Migrations creates another class file in the *Migrations* folder (with the name *{DateStamp}\_Initial.cs* ), and this class contains code that creates the database schema.</span></span> <span data-ttu-id="31bb3-140">使用時間戳預先修正遷移檔案名，以協助進行排序。</span><span class="sxs-lookup"><span data-stu-id="31bb3-140">The migration filename is pre-fixed with a timestamp to help with ordering.</span></span> <span data-ttu-id="31bb3-141">檢查 *{DateStamp}\_Initial.cs*檔案，其中包含為 Movie DB 建立 `Movies` 資料表的指示。</span><span class="sxs-lookup"><span data-stu-id="31bb3-141">Examine the *{DateStamp}\_Initial.cs* file, it contains the instructions to create the `Movies` table for the Movie DB.</span></span> <span data-ttu-id="31bb3-142">當您更新下列指示中的資料庫時，這個 *{DateStamp}\_Initial.cs*檔案將會執行，並建立資料庫架構。</span><span class="sxs-lookup"><span data-stu-id="31bb3-142">When you update the database in the instructions below, this *{DateStamp}\_Initial.cs* file will run and create the DB schema.</span></span> <span data-ttu-id="31bb3-143">然後，會執行**種子**方法，將測試資料填入資料庫。</span><span class="sxs-lookup"><span data-stu-id="31bb3-143">Then the **Seed** method will run to populate the DB with test data.</span></span>

<span data-ttu-id="31bb3-144">在 [**套件管理員主控台**] 中，輸入 `update-database` 來建立資料庫並執行 `Seed` 方法的命令。</span><span class="sxs-lookup"><span data-stu-id="31bb3-144">In the **Package Manager Console**, enter the command `update-database` to create the database and run the `Seed` method.</span></span>

![](adding-a-new-field/_static/image7.png)

<span data-ttu-id="31bb3-145">如果您收到錯誤訊息，指出資料表已經存在，而且無法建立，可能是因為您在刪除資料庫之後，以及執行 `update-database`之前，已執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="31bb3-145">If you get an error that indicates a table already exists and can't be created, it is probably because you ran the application after you deleted the database and before you executed `update-database`.</span></span> <span data-ttu-id="31bb3-146">在這種情況下，請再次刪除 *.mdf*檔案，然後重試 `update-database` 命令。</span><span class="sxs-lookup"><span data-stu-id="31bb3-146">In that case, delete the *Movies.mdf* file again and retry the `update-database` command.</span></span> <span data-ttu-id="31bb3-147">如果您仍然收到錯誤，請刪除 [遷移] 資料夾和 [內容]，然後從這個頁面頂端的指示開始（也就是刪除 [ *.mdf* ] 檔案，然後繼續進行 [啟用-遷移]）。</span><span class="sxs-lookup"><span data-stu-id="31bb3-147">If you still get an error, delete the migrations folder and contents then start with the instructions at the top of this page (that is delete the *Movies.mdf* file then proceed to Enable-Migrations).</span></span> <span data-ttu-id="31bb3-148">如果您仍然收到錯誤，請開啟 SQL Server 物件總管並從清單中移除資料庫。</span><span class="sxs-lookup"><span data-stu-id="31bb3-148">If you still get an error, open SQL Server Object Explorer and remove the database from the list.</span></span>

<span data-ttu-id="31bb3-149">執行應用程式，並流覽至 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="31bb3-149">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="31bb3-150">會顯示種子資料。</span><span class="sxs-lookup"><span data-stu-id="31bb3-150">The seed data is displayed.</span></span>

![](adding-a-new-field/_static/image8.png)

## <a name="adding-a-rating-property-to-the-movie-model"></a><span data-ttu-id="31bb3-151">將 Rating 屬性新增至電影模型</span><span class="sxs-lookup"><span data-stu-id="31bb3-151">Adding a Rating Property to the Movie Model</span></span>

<span data-ttu-id="31bb3-152">首先，將新的 `Rating` 屬性加入至現有的 `Movie` 類別。</span><span class="sxs-lookup"><span data-stu-id="31bb3-152">Start by adding a new `Rating` property to the existing `Movie` class.</span></span> <span data-ttu-id="31bb3-153">開啟*Models\Movie.cs*檔案，然後加入 `Rating` 屬性，如下所示：</span><span class="sxs-lookup"><span data-stu-id="31bb3-153">Open the *Models\Movie.cs* file and add the `Rating` property like this one:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample5.cs)]

<span data-ttu-id="31bb3-154">完整的 `Movie` 類別現在看起來像下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="31bb3-154">The complete `Movie` class now looks like the following code:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample6.cs?highlight=12)]

<span data-ttu-id="31bb3-155">建立應用程式（Ctrl + Shift + B）。</span><span class="sxs-lookup"><span data-stu-id="31bb3-155">Build the application (Ctrl+Shift+B).</span></span>

<span data-ttu-id="31bb3-156">由於您已將新欄位新增至 `Movie` 類別，因此您也需要更新系結*白名單*，以便包含這個新屬性。</span><span class="sxs-lookup"><span data-stu-id="31bb3-156">Because you've added a new field to the `Movie` class, you also need to update the binding *white list* so this new property will be included.</span></span> <span data-ttu-id="31bb3-157">更新 `Create` 和 `Edit` 動作方法的 `bind` 屬性，以包含 `Rating` 屬性：</span><span class="sxs-lookup"><span data-stu-id="31bb3-157">Update the `bind` attribute for `Create` and `Edit` action methods to include the `Rating` property:</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample7.cs?highlight=1)]

<span data-ttu-id="31bb3-158">您也需要更新檢視範本，以便在瀏覽器檢視中顯示、建立和編輯新的 `Rating` 屬性。</span><span class="sxs-lookup"><span data-stu-id="31bb3-158">You also need to update the view templates in order to display, create and edit the new `Rating` property in the browser view.</span></span>

<span data-ttu-id="31bb3-159">開啟 *\Views\Movies\Index.cshtml*檔案，然後在 [**價格**] 資料行的正後方加入 `<th>Rating</th>` 欄標題。</span><span class="sxs-lookup"><span data-stu-id="31bb3-159">Open the *\Views\Movies\Index.cshtml* file and add a `<th>Rating</th>` column heading just after the **Price** column.</span></span> <span data-ttu-id="31bb3-160">然後在範本結尾附近新增 `<td>` 資料行，以轉譯 `@item.Rating` 值。</span><span class="sxs-lookup"><span data-stu-id="31bb3-160">Then add a `<td>` column near the end of the template to render the `@item.Rating` value.</span></span> <span data-ttu-id="31bb3-161">以下是更新的*Index. cshtml*視圖範本的樣子：</span><span class="sxs-lookup"><span data-stu-id="31bb3-161">Below is what the updated *Index.cshtml* view template looks like:</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample8.cshtml?highlight=31-33,52-54)]

<span data-ttu-id="31bb3-162">接下來，開啟 *\Views\Movies\Create.cshtml*檔案，並新增具有下列反白顯示標記的 [`Rating`] 欄位。</span><span class="sxs-lookup"><span data-stu-id="31bb3-162">Next, open the *\Views\Movies\Create.cshtml* file and add the `Rating` field with the following highlighted markup.</span></span> <span data-ttu-id="31bb3-163">這會轉譯一個文字方塊，讓您可以在建立新電影時指定評等。</span><span class="sxs-lookup"><span data-stu-id="31bb3-163">This renders a text box so that you can specify a rating when a new movie is created.</span></span>

[!code-cshtml[Main](adding-a-new-field/samples/sample9.cshtml?highlight=9-15)]

<span data-ttu-id="31bb3-164">您現已更新應用程式代碼，以支援新的 `Rating` 屬性。</span><span class="sxs-lookup"><span data-stu-id="31bb3-164">You've now updated the application code to support the new `Rating` property.</span></span>

<span data-ttu-id="31bb3-165">執行應用程式，並流覽至 */Movies* URL。</span><span class="sxs-lookup"><span data-stu-id="31bb3-165">Run the application and navigate to the */Movies* URL.</span></span> <span data-ttu-id="31bb3-166">不過，當您這麼做時，您會看到下列其中一個錯誤：</span><span class="sxs-lookup"><span data-stu-id="31bb3-166">When you do this, though, you'll see one of the following errors:</span></span>

![](adding-a-new-field/_static/image9.png)  
  
<span data-ttu-id="31bb3-167">在建立資料庫之後，支援 ' MovieDBCoNtext ' 內容的模型已經變更。</span><span class="sxs-lookup"><span data-stu-id="31bb3-167">The model backing the 'MovieDBContext' context has changed since the database was created.</span></span> <span data-ttu-id="31bb3-168">請考慮使用 Code First 移轉來更新資料庫（ https://go.microsoft.com/fwlink/?LinkId=238269) 。</span><span class="sxs-lookup"><span data-stu-id="31bb3-168">Consider using Code First Migrations to update the database (https://go.microsoft.com/fwlink/?LinkId=238269).</span></span>

![](adding-a-new-field/_static/image10.png)

<span data-ttu-id="31bb3-169">您看到這個錯誤是因為應用程式中更新的 `Movie` 模型類別，現在與現有資料庫 `Movie` 資料表的架構不同。</span><span class="sxs-lookup"><span data-stu-id="31bb3-169">You're seeing this error because the updated `Movie` model class in the application is now different than the schema of the `Movie` table of the existing database.</span></span> <span data-ttu-id="31bb3-170">(資料庫資料表中沒有任何 `Rating` 資料行)。</span><span class="sxs-lookup"><span data-stu-id="31bb3-170">(There's no `Rating` column in the database table.)</span></span>

<span data-ttu-id="31bb3-171">有幾個方法可以解決這個錯誤：</span><span class="sxs-lookup"><span data-stu-id="31bb3-171">There are a few approaches to resolving the error:</span></span>

1. <span data-ttu-id="31bb3-172">讓 Entity Framework 自動卸除資料庫，並重新依據新的模型類別結構描述來建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="31bb3-172">Have the Entity Framework automatically drop and re-create the database based on the new model class schema.</span></span> <span data-ttu-id="31bb3-173">在開發週期早期，當您在測試資料庫上進行開發時，這個方法會很方便；其可讓您一併調整模型和資料庫結構描述，更加快速。</span><span class="sxs-lookup"><span data-stu-id="31bb3-173">This approach is very convenient early in the development cycle when you are doing active development on a test database; it allows you to quickly evolve the model and database schema together.</span></span> <span data-ttu-id="31bb3-174">不過，缺點是您會遺失資料庫中的現有資料，因此您*不*會想要在生產資料庫上使用此方法！</span><span class="sxs-lookup"><span data-stu-id="31bb3-174">The downside, though, is that you lose existing data in the database — so you *don't* want to use this approach on a production database!</span></span> <span data-ttu-id="31bb3-175">使用初始設定式將測試資料自動植入資料庫，通常是開發應用程式的有效方式。</span><span class="sxs-lookup"><span data-stu-id="31bb3-175">Using an initializer to automatically seed a database with test data is often a productive way to develop an application.</span></span> <span data-ttu-id="31bb3-176">如需 Entity Framework 資料庫初始化運算式的詳細資訊，請參閱[ASP.NET MVC/Entity Framework 教學](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程。</span><span class="sxs-lookup"><span data-stu-id="31bb3-176">For more information on Entity Framework database initializers, see [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>
2. <span data-ttu-id="31bb3-177">您可明確修改現有資料庫的結構描述，使其符合模型類別。</span><span class="sxs-lookup"><span data-stu-id="31bb3-177">Explicitly modify the schema of the existing database so that it matches the model classes.</span></span> <span data-ttu-id="31bb3-178">這種方法的優點是可以保留您的資料。</span><span class="sxs-lookup"><span data-stu-id="31bb3-178">The advantage of this approach is that you keep your data.</span></span> <span data-ttu-id="31bb3-179">您可以手動方式或藉由建立資料庫變更指令碼來進行這項變更。</span><span class="sxs-lookup"><span data-stu-id="31bb3-179">You can make this change either manually or by creating a database change script.</span></span>
3. <span data-ttu-id="31bb3-180">使用 Code First 移轉來更新資料庫結構描述。</span><span class="sxs-lookup"><span data-stu-id="31bb3-180">Use Code First Migrations to update the database schema.</span></span>

<span data-ttu-id="31bb3-181">在本教學課程中，我們將使用 Code First 移轉。</span><span class="sxs-lookup"><span data-stu-id="31bb3-181">For this tutorial, we'll use Code First Migrations.</span></span>

<span data-ttu-id="31bb3-182">更新種子方法，讓它提供新資料行的值。</span><span class="sxs-lookup"><span data-stu-id="31bb3-182">Update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="31bb3-183">開啟 [Migrations\Configuration.cs 檔案]，並將 [評等] 欄位新增至每個 Movie 物件。</span><span class="sxs-lookup"><span data-stu-id="31bb3-183">Open Migrations\Configuration.cs file and add a Rating field to each Movie object.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample10.cs?highlight=6)]

<span data-ttu-id="31bb3-184">建立解決方案，然後開啟 [**套件管理員主控台**] 視窗並輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="31bb3-184">Build the solution, and then open the **Package Manager Console** window and enter the following command:</span></span>

`add-migration Rating`

<span data-ttu-id="31bb3-185">`add-migration` 命令會告訴遷移架構使用目前的 movie DB 架構來檢查目前的電影模型，並建立必要的程式碼來將資料庫移轉至新的模型。</span><span class="sxs-lookup"><span data-stu-id="31bb3-185">The `add-migration` command tells the migration framework to examine the current movie model with the current movie DB schema and create the necessary code to migrate the DB to the new model.</span></span> <span data-ttu-id="31bb3-186">名稱*分級*是任意的，用來命名遷移檔案。</span><span class="sxs-lookup"><span data-stu-id="31bb3-186">The name *Rating* is arbitrary and is used to name the migration file.</span></span> <span data-ttu-id="31bb3-187">使用有意義的名稱來進行遷移步驟會很有説明。</span><span class="sxs-lookup"><span data-stu-id="31bb3-187">It's helpful to use a meaningful name for the migration step.</span></span>

<span data-ttu-id="31bb3-188">當此命令完成時，Visual Studio 會開啟定義新 `DbMigration` 衍生類別的類別檔案，而在 `Up` 方法中，您可以看到建立新資料行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="31bb3-188">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` derived class, and in the `Up` method you can see the code that creates the new column.</span></span>

[!code-csharp[Main](adding-a-new-field/samples/sample11.cs)]

<span data-ttu-id="31bb3-189">建立解決方案，然後在 [**套件管理員主控台**] 視窗中輸入 `update-database` 命令。</span><span class="sxs-lookup"><span data-stu-id="31bb3-189">Build the solution, and then enter the `update-database` command in the **Package Manager Console** window.</span></span>

<span data-ttu-id="31bb3-190">下圖顯示 [**套件管理員主控台**] 視窗中的輸出（前面加上「日期戳記」的*評*等會有所不同）。</span><span class="sxs-lookup"><span data-stu-id="31bb3-190">The following image shows the output in the **Package Manager Console** window (The date stamp prepending *Rating* will be different.)</span></span>

![](adding-a-new-field/_static/image11.png)

<span data-ttu-id="31bb3-191">重新執行應用程式，並流覽至/Movies URL。</span><span class="sxs-lookup"><span data-stu-id="31bb3-191">Re-run the application and navigate to the /Movies URL.</span></span> <span data-ttu-id="31bb3-192">您可以看到新的評等欄位。</span><span class="sxs-lookup"><span data-stu-id="31bb3-192">You can see the new Rating field.</span></span>

![](adding-a-new-field/_static/image12.png)

<span data-ttu-id="31bb3-193">按一下 [**建立新**的] 連結以新增電影。</span><span class="sxs-lookup"><span data-stu-id="31bb3-193">Click the **Create New** link to add a new movie.</span></span> <span data-ttu-id="31bb3-194">請注意，您可以加入評等。</span><span class="sxs-lookup"><span data-stu-id="31bb3-194">Note that you can add a rating.</span></span>

![7_CreateRioII](adding-a-new-field/_static/image13.png)

<span data-ttu-id="31bb3-196">按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="31bb3-196">Click **Create**.</span></span> <span data-ttu-id="31bb3-197">新電影（包括評等）現在會顯示在電影清單中：</span><span class="sxs-lookup"><span data-stu-id="31bb3-197">The new movie, including the rating, now shows up in the movies listing:</span></span>

![7_ourNewMovie_SM](adding-a-new-field/_static/image14.png)

<span data-ttu-id="31bb3-199">現在，專案正在使用遷移，您不需要在加入新欄位或更新架構時卸載資料庫。</span><span class="sxs-lookup"><span data-stu-id="31bb3-199">Now that the project is using migrations, you won't need to drop the database when you add a new field or otherwise update the schema.</span></span> <span data-ttu-id="31bb3-200">在下一節中，我們會進行更多的架構變更，並使用遷移來更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="31bb3-200">In the next section, we'll make more schema changes and use migrations to update the database.</span></span>

<span data-ttu-id="31bb3-201">您也應該將 [`Rating`] 欄位加入至 [編輯]、[詳細資料] 和 [刪除] 視圖範本。</span><span class="sxs-lookup"><span data-stu-id="31bb3-201">You should also add the `Rating` field to the Edit, Details, and Delete view templates.</span></span>

<span data-ttu-id="31bb3-202">您可以再次在 [**套件管理員主控台**] 視窗中輸入「更新資料庫」命令，而不會執行任何遷移程式碼，因為架構符合模型。</span><span class="sxs-lookup"><span data-stu-id="31bb3-202">You could enter the "update-database" command in the **Package Manager Console** window again and no migration code would run, because the schema matches the model.</span></span> <span data-ttu-id="31bb3-203">不過，執行「更新資料庫」將會再次執行 `Seed` 方法，如果您變更了任何種子資料，變更將會遺失，因為 `Seed` 方法會更新插入資料。</span><span class="sxs-lookup"><span data-stu-id="31bb3-203">However, running "update-database" will run the `Seed` method again, and if you changed any of the Seed data, the changes will be lost because the `Seed` method upserts data.</span></span> <span data-ttu-id="31bb3-204">您可以在 Tom 作者: dykstra 的熱門[ASP.NET MVC/Entity Framework 教學](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)課程中閱讀更多有關 `Seed` 方法的資訊。</span><span class="sxs-lookup"><span data-stu-id="31bb3-204">You can read more about the `Seed` method in Tom Dykstra's popular [ASP.NET MVC/Entity Framework tutorial](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="31bb3-205">在本節中，您會看到如何修改模型物件，並讓資料庫與變更保持同步。</span><span class="sxs-lookup"><span data-stu-id="31bb3-205">In this section you saw how you can modify model objects and keep the database in sync with the changes.</span></span> <span data-ttu-id="31bb3-206">您也學到以範例資料填入新建立資料庫的方法，讓您可以試試看案例。</span><span class="sxs-lookup"><span data-stu-id="31bb3-206">You also learned a way to populate a newly created database with sample data so you can try out scenarios.</span></span> <span data-ttu-id="31bb3-207">這只是 Code First 的快速簡介，請參閱[建立適用于 ASP.NET MVC 應用程式的 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)，以取得更完整的主旨教學課程。</span><span class="sxs-lookup"><span data-stu-id="31bb3-207">This was just a quick introduction to Code First, see [Creating an Entity Framework Data Model for an ASP.NET MVC Application](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md) for a more complete tutorial on the subject.</span></span> <span data-ttu-id="31bb3-208">接下來，我們將探討如何將更豐富的驗證邏輯新增至模型類別，並讓某些商務規則得以強制執行。</span><span class="sxs-lookup"><span data-stu-id="31bb3-208">Next, let's look at how you can add richer validation logic to the model classes and enable some business rules to be enforced.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="31bb3-209">[上一頁](adding-search.md)
> [下一頁](adding-validation.md)</span><span class="sxs-lookup"><span data-stu-id="31bb3-209">[Previous](adding-search.md)
[Next](adding-validation.md)</span></span>
