---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
title: 簡介 ASP.NET Web Pages-更新資料庫資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程說明當您使用 ASP.NET Web Pages （Razor）時，如何更新（變更）現有的資料庫專案。 它假設您已完成第一系列 。
ms.author: riande
ms.date: 01/02/2018
ms.assetid: ac86ec9c-6b69-485b-b9e0-8b9127b13e6b
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/updating-data
msc.type: authoredcontent
ms.openlocfilehash: 8f8bcfb7d9d2416a2699776cadbdaae8e12415ba
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574225"
---
# <a name="introducing-aspnet-web-pages---updating-database-data"></a><span data-ttu-id="42527-104">簡介 ASP.NET Web Pages-更新資料庫資料</span><span class="sxs-lookup"><span data-stu-id="42527-104">Introducing ASP.NET Web Pages - Updating Database Data</span></span>

<span data-ttu-id="42527-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="42527-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="42527-106">本教學課程說明當您使用 ASP.NET Web Pages （Razor）時，如何更新（變更）現有的資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="42527-106">This tutorial shows you how to update (change) an existing database entry when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="42527-107">它假設您已使用[ASP.NET Web Pages 的表單，透過輸入資料來](entering-data.md)完成數列。</span><span class="sxs-lookup"><span data-stu-id="42527-107">It assumes you have completed the series through [Entering Data by Using Forms Using ASP.NET Web Pages](entering-data.md).</span></span>
> 
> <span data-ttu-id="42527-108">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="42527-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="42527-109">如何在 `WebGrid` helper 中選取個別記錄。</span><span class="sxs-lookup"><span data-stu-id="42527-109">How to select an individual record in the `WebGrid` helper.</span></span>
> - <span data-ttu-id="42527-110">如何從資料庫讀取單一記錄。</span><span class="sxs-lookup"><span data-stu-id="42527-110">How to read a single record from a database.</span></span>
> - <span data-ttu-id="42527-111">如何使用資料庫記錄中的值預先載入表單。</span><span class="sxs-lookup"><span data-stu-id="42527-111">How to preload a form with values from the database record.</span></span>
> - <span data-ttu-id="42527-112">如何更新資料庫中的現有記錄。</span><span class="sxs-lookup"><span data-stu-id="42527-112">How to update an existing record in a database.</span></span>
> - <span data-ttu-id="42527-113">如何將資訊儲存在頁面中，而不顯示它。</span><span class="sxs-lookup"><span data-stu-id="42527-113">How to store information in the page without displaying it.</span></span>
> - <span data-ttu-id="42527-114">如何使用隱藏欄位來儲存資訊。</span><span class="sxs-lookup"><span data-stu-id="42527-114">How to use a hidden field to store information.</span></span>
>   
> 
> <span data-ttu-id="42527-115">討論的功能/技術：</span><span class="sxs-lookup"><span data-stu-id="42527-115">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="42527-116">`WebGrid` helper。</span><span class="sxs-lookup"><span data-stu-id="42527-116">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="42527-117">SQL `Update` 命令。</span><span class="sxs-lookup"><span data-stu-id="42527-117">The SQL `Update` command.</span></span>
> - <span data-ttu-id="42527-118">`Database.Execute` 方法</span><span class="sxs-lookup"><span data-stu-id="42527-118">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="42527-119">隱藏欄位（`<input type="hidden">`）。</span><span class="sxs-lookup"><span data-stu-id="42527-119">Hidden fields (`<input type="hidden">`).</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="42527-120">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="42527-120">What You'll Build</span></span>

<span data-ttu-id="42527-121">在上一個教學課程中，您已瞭解如何將記錄新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="42527-121">In the previous tutorial, you learned how to add a record to a database.</span></span> <span data-ttu-id="42527-122">在此，您將瞭解如何顯示要編輯的記錄。</span><span class="sxs-lookup"><span data-stu-id="42527-122">Here, you'll learn how to display a record for editing.</span></span> <span data-ttu-id="42527-123">在 [*電影*] 頁面中，您將更新 `WebGrid` 協助程式，使其顯示每個電影旁的 [**編輯**] 連結：</span><span class="sxs-lookup"><span data-stu-id="42527-123">In the *Movies* page, you'll update the `WebGrid` helper so that it displays an **Edit** link next to each movie:</span></span>

![WebGrid 顯示包含每個電影的 [編輯] 連結](updating-data/_static/image1.png)

<span data-ttu-id="42527-125">當您按一下 [**編輯**] 連結時，它會帶您前往不同的頁面，其中電影資訊已經是表單：</span><span class="sxs-lookup"><span data-stu-id="42527-125">When you click the **Edit** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![編輯電影頁面，顯示要編輯的電影](updating-data/_static/image2.png)

<span data-ttu-id="42527-127">您可以變更任何值。</span><span class="sxs-lookup"><span data-stu-id="42527-127">You can change any of the values.</span></span> <span data-ttu-id="42527-128">當您提交變更時，頁面中的程式碼會更新資料庫，並帶您回到電影清單。</span><span class="sxs-lookup"><span data-stu-id="42527-128">When you submit the changes, the code in the page updates the database and takes you back to the movie listing.</span></span>

<span data-ttu-id="42527-129">此程式的運作方式幾乎與您在上一個教學課程中建立的*AddMovie*相同，因此本教學課程中大部分的功能都很熟悉。</span><span class="sxs-lookup"><span data-stu-id="42527-129">This part of the process works almost exactly like the *AddMovie.cshtml* page you created in the previous tutorial, so much of this tutorial will be familiar.</span></span>

<span data-ttu-id="42527-130">有數種方式可讓您執行編輯個別電影的方式。</span><span class="sxs-lookup"><span data-stu-id="42527-130">There are several ways you could implement a way to edit an individual movie.</span></span> <span data-ttu-id="42527-131">已選擇所顯示的方法，因為它很容易執行且易於瞭解。</span><span class="sxs-lookup"><span data-stu-id="42527-131">The approach shown was chosen because it's easy to implement and easy to understand.</span></span>

## <a name="adding-an-edit-link-to-the-movie-listing"></a><span data-ttu-id="42527-132">新增電影清單的編輯連結</span><span class="sxs-lookup"><span data-stu-id="42527-132">Adding an Edit Link to the Movie Listing</span></span>

<span data-ttu-id="42527-133">首先，您將更新 [*電影*] 頁面，讓每個電影清單也包含一個 [**編輯**] 連結。</span><span class="sxs-lookup"><span data-stu-id="42527-133">To begin, you'll update the *Movies* page so that each movie listing also contains an **Edit** link.</span></span>

<span data-ttu-id="42527-134">開啟 [*電影*] 檔案。</span><span class="sxs-lookup"><span data-stu-id="42527-134">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="42527-135">在頁面主體中，藉由新增資料行來變更 `WebGrid` 標記。</span><span class="sxs-lookup"><span data-stu-id="42527-135">In the body of the page, change the `WebGrid` markup by adding a column.</span></span> <span data-ttu-id="42527-136">以下是修改過的標記：</span><span class="sxs-lookup"><span data-stu-id="42527-136">Here's the modified markup:</span></span>

[!code-html[Main](updating-data/samples/sample1.html?highlight=6)]

<span data-ttu-id="42527-137">新的資料行是這一項：</span><span class="sxs-lookup"><span data-stu-id="42527-137">The new column is this one:</span></span>

[!code-html[Main](updating-data/samples/sample2.html)]

<span data-ttu-id="42527-138">此資料行的重點是要顯示其文字顯示為「編輯」的連結（`<a>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="42527-138">The point of this column is to show a link (`<a>` element) whose text says "Edit".</span></span> <span data-ttu-id="42527-139">接下來我們要建立一個在頁面執行時看起來像下面的連結，每個電影的 `id` 值都不同：</span><span class="sxs-lookup"><span data-stu-id="42527-139">What we're after is to create a link that looks like the following when the page runs, with the `id` value different for each movie:</span></span>

[!code-css[Main](updating-data/samples/sample3.css)]

<span data-ttu-id="42527-140">此連結將會叫用名為*EditMovie*的頁面，並將查詢字串傳遞 `?id=7` 至該頁面。</span><span class="sxs-lookup"><span data-stu-id="42527-140">This link will invoke a page named *EditMovie*, and it will pass the query string `?id=7` to that page.</span></span>

<span data-ttu-id="42527-141">新資料行的語法看起來可能有點複雜，但這只是因為它會將數個元素放在一起。</span><span class="sxs-lookup"><span data-stu-id="42527-141">The syntax for the new column might look a bit complex, but that's only because it puts together several elements.</span></span> <span data-ttu-id="42527-142">每個個別元素都很簡單。</span><span class="sxs-lookup"><span data-stu-id="42527-142">Each individual element is straightforward.</span></span> <span data-ttu-id="42527-143">如果您只專注于 `<a>` 專案，您會看到此標記：</span><span class="sxs-lookup"><span data-stu-id="42527-143">If you concentrate on just the `<a>` element, you see this markup:</span></span>

[!code-html[Main](updating-data/samples/sample4.html)]

<span data-ttu-id="42527-144">格線運作方式的一些背景：格線會顯示資料列（每個資料庫記錄一個），並顯示資料庫記錄中每個欄位的資料行。</span><span class="sxs-lookup"><span data-stu-id="42527-144">Some background about how the grid works: the grid displays rows, one for each database record, and it displays columns for each field in the database record.</span></span> <span data-ttu-id="42527-145">當每個方格資料列都在進行結構化時，`item` 物件會包含該資料列的資料庫記錄（item）。</span><span class="sxs-lookup"><span data-stu-id="42527-145">While each grid row is being constructed, the `item` object contains the database record (item) for that row.</span></span> <span data-ttu-id="42527-146">這種相片順序可讓您在程式碼中取得該資料列的資料。</span><span class="sxs-lookup"><span data-stu-id="42527-146">This arrangement gives you a way in code to get at the data for that row.</span></span> <span data-ttu-id="42527-147">這就是您在這裡看到的內容：運算式 `item.ID` 取得目前資料庫專案的識別碼值。</span><span class="sxs-lookup"><span data-stu-id="42527-147">That's what you see here: the expression `item.ID` is getting the ID value of the current database item.</span></span> <span data-ttu-id="42527-148">您可以使用 `item.Title`、`item.Genre`或 `item.Year`，以相同的方式取得任何資料庫值（[標題]、[內容類型] 或 [年份]）。</span><span class="sxs-lookup"><span data-stu-id="42527-148">You could get any of the database values (title, genre, or year) the same way by using `item.Title`, `item.Genre`, or `item.Year`.</span></span>

<span data-ttu-id="42527-149">運算式 `"~/EditMovie?id=@item.ID` 結合了目標 URL 的硬式編碼部分（`~/EditMovie?id=`）與這個動態衍生的識別碼。</span><span class="sxs-lookup"><span data-stu-id="42527-149">The expression `"~/EditMovie?id=@item.ID` combines the hard-coded part of the target URL (`~/EditMovie?id=`) with this dynamically derived ID.</span></span> <span data-ttu-id="42527-150">（您在上一個教學課程中看到了 `~` 運算子，它是代表目前網站根目錄的 ASP.NET 運算子）。</span><span class="sxs-lookup"><span data-stu-id="42527-150">(You saw the `~` operator in the previous tutorial; it's an ASP.NET operator that represents the current website root.)</span></span>

<span data-ttu-id="42527-151">結果是，資料行中標記的這個部分只會在執行時間產生類似下列的標記：</span><span class="sxs-lookup"><span data-stu-id="42527-151">The result is that this part of the markup in the column simply produces something like the following markup at run time:</span></span>

[!code-xml[Main](updating-data/samples/sample5.xml)]

<span data-ttu-id="42527-152">當然，每個資料列的實際 `id` 值都是不同的。</span><span class="sxs-lookup"><span data-stu-id="42527-152">Naturally, the actual value of `id` will be different for each row.</span></span>

## <a name="creating-a-custom-display-for-a-grid-column"></a><span data-ttu-id="42527-153">建立格線資料行的自訂顯示</span><span class="sxs-lookup"><span data-stu-id="42527-153">Creating a Custom Display for a Grid Column</span></span>

<span data-ttu-id="42527-154">現在回到方格資料行。</span><span class="sxs-lookup"><span data-stu-id="42527-154">Now back to the grid column.</span></span> <span data-ttu-id="42527-155">您原先在方格中擁有的三個數據行只會顯示資料值（[標題]、[內容類型] 和 [年份]）。</span><span class="sxs-lookup"><span data-stu-id="42527-155">The three columns you originally had in the grid displayed only data values (title, genre, and year).</span></span> <span data-ttu-id="42527-156">您藉由傳遞資料庫資料行的名稱來指定此顯示 &mdash; 例如，`grid.Column("Title")`。</span><span class="sxs-lookup"><span data-stu-id="42527-156">You specified this display by passing the name of the database column &mdash; for example, `grid.Column("Title")`.</span></span>

<span data-ttu-id="42527-157">這個新的 [**編輯**連結] 資料行不同。</span><span class="sxs-lookup"><span data-stu-id="42527-157">This new **Edit** link column is different.</span></span> <span data-ttu-id="42527-158">您不需要指定資料行名稱，而是傳遞 `format` 參數。</span><span class="sxs-lookup"><span data-stu-id="42527-158">Instead of specifying a column name, you're passing a `format` parameter.</span></span> <span data-ttu-id="42527-159">這個參數可讓您定義 `WebGrid` helper 將轉譯的標記，以及 `item` 值，以粗體或綠色或您想要的任何格式來顯示資料行資料。</span><span class="sxs-lookup"><span data-stu-id="42527-159">This parameter lets you define markup that the `WebGrid` helper will render along with the `item` value to display the column data as bold or green or in whatever format that you want.</span></span> <span data-ttu-id="42527-160">例如，如果您希望標題以粗體顯示，您可以建立如下列範例所示的資料行：</span><span class="sxs-lookup"><span data-stu-id="42527-160">For example, if you wanted the title to appear bold, you could create a column like this example:</span></span>

[!code-html[Main](updating-data/samples/sample6.html)]

<span data-ttu-id="42527-161">（您在 `format` 屬性中看到的各種 `@` 字元會標示標記和程式碼值之間的轉換）。</span><span class="sxs-lookup"><span data-stu-id="42527-161">(The various `@` characters you see in the `format` property mark the transition between markup and a code value.)</span></span>

<span data-ttu-id="42527-162">一旦知道 `format` 屬性之後，就能更輕鬆地瞭解新的 [**編輯**連結] 資料行如何放在一起：</span><span class="sxs-lookup"><span data-stu-id="42527-162">Once you know about the `format` property, it's easier to understand how the new **Edit** link column is put together:</span></span>

[!code-html[Main](updating-data/samples/sample7.html)]

<span data-ttu-id="42527-163">此資料行*只*包含轉譯連結的標記，加上從資料列的資料庫記錄中解壓縮的部分資訊（識別碼）。</span><span class="sxs-lookup"><span data-stu-id="42527-163">The column consists *only* of the markup that renders the link, plus some information (the ID) that's extracted from the database record for the row.</span></span>

> [!TIP]
> 
> <span data-ttu-id="42527-164">**方法的具名引數和位置參數**</span><span class="sxs-lookup"><span data-stu-id="42527-164">**Named Parameters and Positional Parameters for a Method**</span></span>
> 
> <span data-ttu-id="42527-165">許多時候，當您呼叫方法並將參數傳遞給它時，就只會列出以逗號分隔的參數值。</span><span class="sxs-lookup"><span data-stu-id="42527-165">Many times when you've called a method and passed parameters to it, you've simply listed the parameter values separated by commas.</span></span> <span data-ttu-id="42527-166">以下提供幾個範例：</span><span class="sxs-lookup"><span data-stu-id="42527-166">Here are a couple of examples:</span></span>
> 
> `db.Execute(insertCommand, title, genre, year)`
> 
> `Validation.RequireField("title", "You must enter a title")`
> 
> <span data-ttu-id="42527-167">當您第一次看到此程式碼時，我們並未提過這個問題，但在每個案例中，您會以特定順序將參數傳遞給方法 &mdash; 也就是在該方法中定義參數的順序。</span><span class="sxs-lookup"><span data-stu-id="42527-167">We didn't mention the issue when you first saw this code, but in each case, you're passing parameters to the methods in a specific order &mdash; namely, the order in which the parameters are defined in that method.</span></span> <span data-ttu-id="42527-168">針對 `db.Execute` 和 `Validation.RequireFields`，如果您要將傳遞值的順序混合，則會在頁面執行時收到錯誤訊息，或至少有一些奇怪的結果。</span><span class="sxs-lookup"><span data-stu-id="42527-168">For `db.Execute` and `Validation.RequireFields`, if you mixed up the order of the values you pass, you'd get an error message when the page runs, or at least some strange results.</span></span> <span data-ttu-id="42527-169">很明顯地，您必須知道要在中傳遞參數的順序。</span><span class="sxs-lookup"><span data-stu-id="42527-169">Clearly, you have to know the order to pass the parameters in.</span></span> <span data-ttu-id="42527-170">（在 WebMatrix 中，IntelliSense 可協助您瞭解參數的名稱、類型和順序）。</span><span class="sxs-lookup"><span data-stu-id="42527-170">(In WebMatrix, IntelliSense can help you learn figure out the name, type, and order of the parameters.)</span></span>
> 
> <span data-ttu-id="42527-171">除了依序傳遞值以外，您還可以使用*具名引數*。</span><span class="sxs-lookup"><span data-stu-id="42527-171">As an alternative to passing values in order, you can use *named parameters*.</span></span> <span data-ttu-id="42527-172">（傳遞參數的順序稱為「使用*位置參數*」）。針對具名引數，您會在傳遞值時明確包含參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="42527-172">(Passing parameters in order is known as using *positional parameters*.) For named parameters, you explicitly include the name of the parameter when passing its value.</span></span> <span data-ttu-id="42527-173">在這些教學課程中，您已使用具名引數已經有數次。</span><span class="sxs-lookup"><span data-stu-id="42527-173">You've used named parameters already a number of times in these tutorials.</span></span> <span data-ttu-id="42527-174">例如:</span><span class="sxs-lookup"><span data-stu-id="42527-174">For example:</span></span>
> 
> [!code-csharp[Main](updating-data/samples/sample8.cs)]
> 
> <span data-ttu-id="42527-175">和</span><span class="sxs-lookup"><span data-stu-id="42527-175">and</span></span>
> 
> [!code-css[Main](updating-data/samples/sample9.css)]
> 
> <span data-ttu-id="42527-176">在幾種情況下，具名引數很方便，尤其是當方法接受許多參數時。</span><span class="sxs-lookup"><span data-stu-id="42527-176">Named parameters are handy for a couple of situations, especially when a method takes many parameters.</span></span> <span data-ttu-id="42527-177">其中一個是當您只想要傳遞一或兩個參數，但您要傳遞的值不在參數清單中的第一個位置時。</span><span class="sxs-lookup"><span data-stu-id="42527-177">One is when you want to pass only one or two parameters, but the values you want to pass are not among the first positions in the parameter list.</span></span> <span data-ttu-id="42527-178">另一種情況是，您想要以對您而言最有意義的順序傳遞參數，讓程式碼更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="42527-178">Another situation is when you want to make your code more readable by passing the parameters in the order that makes the most sense to you.</span></span>
> 
> <span data-ttu-id="42527-179">很明顯地，若要使用具名引數，您必須知道參數的名稱。</span><span class="sxs-lookup"><span data-stu-id="42527-179">Obviously, to use named parameters, you have to know the names of the parameters.</span></span> <span data-ttu-id="42527-180">WebMatrix IntelliSense 可以*顯示*名稱，但目前無法為您填入。</span><span class="sxs-lookup"><span data-stu-id="42527-180">WebMatrix IntelliSense can *show* you the names, but it cannot currently fill them in for you.</span></span>

## <a name="creating-the-edit-page"></a><span data-ttu-id="42527-181">建立 [編輯] 頁面</span><span class="sxs-lookup"><span data-stu-id="42527-181">Creating the Edit Page</span></span>

<span data-ttu-id="42527-182">現在您可以建立 [ *EditMovie* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="42527-182">Now you can create the *EditMovie* page.</span></span> <span data-ttu-id="42527-183">當使用者按一下 [**編輯**] 連結時，將會在此頁面上結束。</span><span class="sxs-lookup"><span data-stu-id="42527-183">When users click the **Edit** link, they'll end up on this page.</span></span>

<span data-ttu-id="42527-184">建立名為*EditMovie*的頁面，並以下列標記取代檔案中的內容：</span><span class="sxs-lookup"><span data-stu-id="42527-184">Create a page named *EditMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](updating-data/samples/sample10.cshtml)]

<span data-ttu-id="42527-185">此標記和程式碼類似于您在 [ *AddMovie* ] 頁面中的內容。</span><span class="sxs-lookup"><span data-stu-id="42527-185">This markup and code is similar to what you have in the *AddMovie* page.</span></span> <span data-ttu-id="42527-186">[提交] 按鈕的文字有些微差異。</span><span class="sxs-lookup"><span data-stu-id="42527-186">There's a small difference in the text for the submit button.</span></span> <span data-ttu-id="42527-187">如同*AddMovie*頁面，有一個 `Html.ValidationSummary` 呼叫會顯示驗證錯誤（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="42527-187">As with the *AddMovie* page, there's an `Html.ValidationSummary` call that will display validation errors if there are any.</span></span> <span data-ttu-id="42527-188">這次我們會離開 `Validation.Message`的呼叫，因為驗證摘要中會顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="42527-188">This time we're leaving out calls to `Validation.Message`, since errors will be displayed in the validation summary.</span></span> <span data-ttu-id="42527-189">如先前的教學課程所述，您可以使用各種組合中的驗證摘要和個別錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="42527-189">As noted in the previous tutorial, you can use the validation summary and the individual error messages in various combinations.</span></span>

<span data-ttu-id="42527-190">請注意，`<form>` 元素的 `method` 屬性設定為 `post`。</span><span class="sxs-lookup"><span data-stu-id="42527-190">Notice again that the `method` attribute of the `<form>` element is set to `post`.</span></span> <span data-ttu-id="42527-191">就像*AddMovie*的頁面一樣，此頁面會對資料庫進行變更。</span><span class="sxs-lookup"><span data-stu-id="42527-191">As with the *AddMovie.cshtml* page, this page makes changes to the database.</span></span> <span data-ttu-id="42527-192">因此，此表單應執行 `POST` 作業。</span><span class="sxs-lookup"><span data-stu-id="42527-192">Therefore, this form should perform a `POST` operation.</span></span> <span data-ttu-id="42527-193">（如需 `GET` 和 `POST` 作業之間差異的詳細資訊，請參閱 HTML 表單教學課程中的[GET、POST 和 HTTP Verb 安全](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety)提要欄位）。</span><span class="sxs-lookup"><span data-stu-id="42527-193">(For more about the difference between `GET` and `POST` operations, see the [GET, POST, and HTTP Verb Safety](form-basics.md#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the tutorial on HTML forms.)</span></span>

<span data-ttu-id="42527-194">如您在先前的教學課程中所見，文字方塊的 `value` 屬性會使用 Razor 程式碼進行設定，以便預先載入。</span><span class="sxs-lookup"><span data-stu-id="42527-194">As you saw in an earlier tutorial, the `value` attributes of the text boxes are being set with Razor code in order to preload them.</span></span> <span data-ttu-id="42527-195">不過，這次您使用的是該工作的 `title` 和 `genre` 之類的變數，而不是 `Request.Form["title"]`：</span><span class="sxs-lookup"><span data-stu-id="42527-195">This time, though, you're using variables like `title` and `genre` for that task instead of `Request.Form["title"]`:</span></span>

`<input type="text" name="title" value="@title" />`

<span data-ttu-id="42527-196">就像之前一樣，此標記會預先載入具有電影值的文字方塊值。</span><span class="sxs-lookup"><span data-stu-id="42527-196">As before, this markup will preload the text box values with the movie values.</span></span> <span data-ttu-id="42527-197">您很快就會看到使用變數的時機，而不是使用 `Request` 物件。</span><span class="sxs-lookup"><span data-stu-id="42527-197">You'll see in a moment why it's handy to use variables this time instead of using the `Request` object.</span></span>

<span data-ttu-id="42527-198">此頁面上也有一個 `<input type="hidden">` 元素。</span><span class="sxs-lookup"><span data-stu-id="42527-198">There's also a `<input type="hidden">` element on this page.</span></span> <span data-ttu-id="42527-199">此元素會儲存電影識別碼，而不會顯示在頁面上。</span><span class="sxs-lookup"><span data-stu-id="42527-199">This element stores the movie ID without making it visible on the page.</span></span> <span data-ttu-id="42527-200">識別碼一開始會使用查詢字串值（`?id=7` 或類似于 URL）傳遞至頁面。</span><span class="sxs-lookup"><span data-stu-id="42527-200">The ID is initially passed to the page by using a query string value (`?id=7` or similar in the URL).</span></span> <span data-ttu-id="42527-201">藉由將識別碼值放入隱藏的欄位中，您可以在提交表單時確保其可供使用，即使您已無法再存取此頁面所叫用的原始 URL 也一樣。</span><span class="sxs-lookup"><span data-stu-id="42527-201">By putting the ID value into a hidden field, you can make sure that it's available when the form is submitted, even if you no longer have access to the original URL that the page was invoked with.</span></span>

<span data-ttu-id="42527-202">不同于*AddMovie*頁面， *EditMovie*頁面的程式碼有兩個不同的功能。</span><span class="sxs-lookup"><span data-stu-id="42527-202">Unlike the *AddMovie* page, the code for the *EditMovie* page has two distinct functions.</span></span> <span data-ttu-id="42527-203">第一個函式是當第一次顯示頁面時（*只有*then），程式碼會從查詢字串取得電影識別碼。</span><span class="sxs-lookup"><span data-stu-id="42527-203">The first function is that when the page is displayed for the first time (and *only* then), the code gets the movie ID from the query string.</span></span> <span data-ttu-id="42527-204">然後，程式碼會使用識別碼來讀取資料庫中的對應電影，並在文字方塊中顯示（預先載入）它。</span><span class="sxs-lookup"><span data-stu-id="42527-204">The code then uses the ID to read the corresponding movie out of the database and display (preload) it in the text boxes.</span></span>

<span data-ttu-id="42527-205">第二個函式是當使用者按一下 [**提交變更**] 按鈕時，程式碼必須讀取文字方塊的值並加以驗證。</span><span class="sxs-lookup"><span data-stu-id="42527-205">The second function is that when the user clicks the **Submit Changes** button, the code has to read the values of the text boxes and validate them.</span></span> <span data-ttu-id="42527-206">程式碼也必須使用新的值來更新資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="42527-206">The code also has to update the database item with the new values.</span></span> <span data-ttu-id="42527-207">這項技術類似于新增記錄，如您在*AddMovie*中所見。</span><span class="sxs-lookup"><span data-stu-id="42527-207">This technique is similar to adding a record, as you saw in *AddMovie*.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="42527-208">新增程式碼以讀取單一電影</span><span class="sxs-lookup"><span data-stu-id="42527-208">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="42527-209">若要執行第一個函式，請將下列程式碼新增至頁面頂端：</span><span class="sxs-lookup"><span data-stu-id="42527-209">To perform the first function, add this code to the top of the page:</span></span>

[!code-cshtml[Main](updating-data/samples/sample11.cshtml)]

<span data-ttu-id="42527-210">大部分的程式碼都位於啟動 `if(!IsPost)`的區塊中。</span><span class="sxs-lookup"><span data-stu-id="42527-210">Most of this code is inside a block that starts `if(!IsPost)`.</span></span> <span data-ttu-id="42527-211">`!` 運算子表示「不」，因此運算式表示*此要求不是 post 提交*，這是一種間接的方式，指出此*要求是否為第一次執行此頁面*。</span><span class="sxs-lookup"><span data-stu-id="42527-211">The `!` operator means "not," so the expression means *if this request is not a post submission*, which is an indirect way of saying *if this request is the first time that this page has been run*.</span></span> <span data-ttu-id="42527-212">如先前所述，此程式碼應該*只*會在頁面第一次執行時執行。</span><span class="sxs-lookup"><span data-stu-id="42527-212">As noted earlier, this code should run *only* the first time the page runs.</span></span> <span data-ttu-id="42527-213">如果您未將程式碼括在 `if(!IsPost)`中，它會在每次叫用頁面時執行，不論是第一次還是回應按鈕的按一下。</span><span class="sxs-lookup"><span data-stu-id="42527-213">If you didn't enclose the code in `if(!IsPost)`, it would run every time the page is invoked, whether the first time or in response to a button click.</span></span>

<span data-ttu-id="42527-214">請注意，此程式碼包含這次的 `else` 區塊。</span><span class="sxs-lookup"><span data-stu-id="42527-214">Notice that the code includes an `else` block this time.</span></span> <span data-ttu-id="42527-215">就像我們在介紹 `if` 區塊時所說的，有時候您會想要在測試的條件不成立時執行替代程式碼。</span><span class="sxs-lookup"><span data-stu-id="42527-215">As we said when we introduced `if` blocks, sometimes you want to run alternative code if the condition you're testing isn't true.</span></span> <span data-ttu-id="42527-216">這就是這種情況。</span><span class="sxs-lookup"><span data-stu-id="42527-216">That's the case here.</span></span> <span data-ttu-id="42527-217">如果條件通過（亦即，如果傳遞至頁面的識別碼是 ok），您就會從資料庫讀取資料列。</span><span class="sxs-lookup"><span data-stu-id="42527-217">If the condition passes (that is, if the ID passed to the page is ok), you read a row from the database.</span></span> <span data-ttu-id="42527-218">不過，如果條件未通過，則會執行 `else` 區塊，而程式碼會設定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="42527-218">However, if the condition doesn't pass, the `else` block runs and the code sets an error message.</span></span>

## <a name="validating-a-value-passed-to-the-page"></a><span data-ttu-id="42527-219">驗證傳遞至頁面的值</span><span class="sxs-lookup"><span data-stu-id="42527-219">Validating a Value Passed to the Page</span></span>

<span data-ttu-id="42527-220">程式碼會使用 `Request.QueryString["id"]` 來取得傳遞至頁面的識別碼。</span><span class="sxs-lookup"><span data-stu-id="42527-220">The code uses `Request.QueryString["id"]` to get the ID that's passed to the page.</span></span> <span data-ttu-id="42527-221">此程式碼可確保已實際傳遞識別碼的值。</span><span class="sxs-lookup"><span data-stu-id="42527-221">The code makes sure that a value was actually passed for the ID.</span></span> <span data-ttu-id="42527-222">如果未傳遞任何值，則程式碼會設定驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="42527-222">If no value was passed, the code sets a validation error.</span></span>

<span data-ttu-id="42527-223">此程式碼會顯示驗證資訊的不同方式。</span><span class="sxs-lookup"><span data-stu-id="42527-223">This code shows a different way to validate information.</span></span> <span data-ttu-id="42527-224">在上一個教學課程中，您已與 `Validation` 協助程式合作。</span><span class="sxs-lookup"><span data-stu-id="42527-224">In the previous tutorial, you worked with the `Validation` helper.</span></span> <span data-ttu-id="42527-225">您已註冊要驗證的欄位，而 ASP.NET 會使用 `Html.ValidationMessage` 和 `Html.ValidationSummary`，自動執行驗證和顯示錯誤。</span><span class="sxs-lookup"><span data-stu-id="42527-225">You registered fields to validate, and ASP.NET automatically did the validation and displayed errors by using `Html.ValidationMessage` and `Html.ValidationSummary`.</span></span> <span data-ttu-id="42527-226">不過，在此情況下，您實際上不是驗證使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="42527-226">In this case, however, you're not really validating user input.</span></span> <span data-ttu-id="42527-227">相反地，您要驗證從別處傳遞至頁面的值。</span><span class="sxs-lookup"><span data-stu-id="42527-227">Instead, you're validating a value that was passed to the page from elsewhere.</span></span> <span data-ttu-id="42527-228">`Validation` helper 不會為您執行此動作。</span><span class="sxs-lookup"><span data-stu-id="42527-228">The `Validation` helper doesn't do that for you.</span></span>

<span data-ttu-id="42527-229">因此，您可以自行檢查值，方法是使用 `if(!Request.QueryString["ID"].IsEmpty()`進行測試）。</span><span class="sxs-lookup"><span data-stu-id="42527-229">Therefore, you check the value yourself, by testing it with `if(!Request.QueryString["ID"].IsEmpty()`).</span></span> <span data-ttu-id="42527-230">如果發生問題，您可以使用 `Html.ValidationSummary`來顯示錯誤，如同您在 `Validation` 協助程式中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="42527-230">If there's a problem, you can display the error by using `Html.ValidationSummary`, as you did with the `Validation` helper.</span></span> <span data-ttu-id="42527-231">若要這麼做，請呼叫 `Validation.AddFormError`，並將要顯示的訊息傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="42527-231">To do that, you call `Validation.AddFormError` and pass it a message to display.</span></span> <span data-ttu-id="42527-232">`Validation.AddFormError` 是內建的方法，可讓您定義與您已熟悉的驗證系統結合的自訂訊息。</span><span class="sxs-lookup"><span data-stu-id="42527-232">`Validation.AddFormError` is a built-in method that lets you define custom messages that tie in with the validation system you're already familiar with.</span></span> <span data-ttu-id="42527-233">（稍後在本教學課程中，我們將討論如何讓此驗證程式更健全）。</span><span class="sxs-lookup"><span data-stu-id="42527-233">(Later in this tutorial we'll talk about how to make this validation process a little more robust.)</span></span>

<span data-ttu-id="42527-234">確定影片的識別碼之後，程式碼會讀取資料庫，只尋找單一資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="42527-234">After making sure that there's an ID for the movie, the code reads the database, looking for only a single database item.</span></span> <span data-ttu-id="42527-235">（您可能已注意到資料庫作業的一般模式：開啟資料庫、定義 SQL 語句，然後執行語句）。這次，SQL `Select` 語句包括 `WHERE ID = @0`。</span><span class="sxs-lookup"><span data-stu-id="42527-235">(You probably have noticed the general pattern for database operations: open the database, define a SQL statement, and run the statement.) This time, the SQL `Select` statement includes `WHERE ID = @0`.</span></span> <span data-ttu-id="42527-236">因為識別碼是唯一的，所以只會傳回一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="42527-236">Because the ID is unique, only one record can be returned.</span></span>

<span data-ttu-id="42527-237">查詢是使用 `db.QuerySingle` （不是 `db.Query`，如同您用於電影清單的）來執行，而程式碼則會將結果放入 `row` 變數中。</span><span class="sxs-lookup"><span data-stu-id="42527-237">The query is performed by using `db.QuerySingle` (not `db.Query`, as you used for the movie listing), and the code puts the result into the `row` variable.</span></span> <span data-ttu-id="42527-238">`row` 的名稱是任意的;您可以將變數命名為任何您喜歡的名稱。</span><span class="sxs-lookup"><span data-stu-id="42527-238">The name `row` is arbitrary; you can name the variables anything you like.</span></span> <span data-ttu-id="42527-239">然後，在頂端初始化的變數會填入電影詳細資料，讓這些值可以顯示在文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="42527-239">The variables initialized at the top are then filled with the movie details so that these values can be displayed in the text boxes.</span></span>

## <a name="testing-the-edit-page-so-far"></a><span data-ttu-id="42527-240">測試編輯頁面（到目前為止）</span><span class="sxs-lookup"><span data-stu-id="42527-240">Testing the Edit Page (So Far)</span></span>

<span data-ttu-id="42527-241">如果您想要測試您的頁面，請立即執行 [*電影*] 頁面，然後按一下任何電影旁的 [**編輯**] 連結。</span><span class="sxs-lookup"><span data-stu-id="42527-241">If you'd like to test your page, run the *Movies* page now and click an **Edit** link next to any movie.</span></span> <span data-ttu-id="42527-242">您會看到 [ *EditMovie* ] 頁面中已填入您所選電影的詳細資料：</span><span class="sxs-lookup"><span data-stu-id="42527-242">You'll see the *EditMovie* page with the details filled in for the movie you selected:</span></span>

![編輯電影頁面，顯示要編輯的電影](updating-data/_static/image3.png)

<span data-ttu-id="42527-244">請注意，頁面的 URL 包含類似 `?id=10` （或其他數位）的內容。</span><span class="sxs-lookup"><span data-stu-id="42527-244">Notice that the URL of the page includes something like `?id=10` (or some other number).</span></span> <span data-ttu-id="42527-245">到目前為止，您已測試*電影*頁面中的**編輯**連結是否正常運作、您的頁面正在從查詢字串讀取識別碼，以及取得單一電影記錄的資料庫查詢正在運作。</span><span class="sxs-lookup"><span data-stu-id="42527-245">So far you've tested that **Edit** links in the *Movie* page work, that your page is reading the ID from the query string, and that the database query to get a single movie record is working.</span></span>

<span data-ttu-id="42527-246">您可以變更電影資訊，但當您按一下 [**提交變更**] 時，不會發生任何事。</span><span class="sxs-lookup"><span data-stu-id="42527-246">You can change the movie information, but nothing happens when you click **Submit Changes**.</span></span>

## <a name="adding-code-to-update-the-movie-with-the-users-changes"></a><span data-ttu-id="42527-247">新增程式碼以使用使用者的變更來更新電影</span><span class="sxs-lookup"><span data-stu-id="42527-247">Adding Code to Update the Movie with the User's Changes</span></span>

<span data-ttu-id="42527-248">在*EditMovie*檔中，若要執行第二個函式（儲存變更），請將下列程式碼新增至 `@` 區塊的右大括弧內。</span><span class="sxs-lookup"><span data-stu-id="42527-248">In the *EditMovie.cshtml* file, to implement the second function (saving changes), add the following code just inside the closing brace of the `@` block.</span></span> <span data-ttu-id="42527-249">（如果您不確定程式碼的確切位置，可以查看本教學課程結尾處[的 [編輯電影] 頁面的完整程式代碼清單](#Complete_Page_Listing_for_EditMovie)。）</span><span class="sxs-lookup"><span data-stu-id="42527-249">(If you're not sure exactly where to put the code, you can look at the [complete code listing for the Edit Movie page](#Complete_Page_Listing_for_EditMovie) that appears at the end of this tutorial.)</span></span>

[!code-csharp[Main](updating-data/samples/sample12.cs)]

<span data-ttu-id="42527-250">同樣地，此標記和程式碼與*AddMovie*中的程式碼類似。</span><span class="sxs-lookup"><span data-stu-id="42527-250">Again, this markup and code is similar to the code in *AddMovie*.</span></span> <span data-ttu-id="42527-251">這段程式碼是在 `if(IsPost)` 區塊中，因為只有在使用者按一下 [**提交變更**] 按鈕時，才會執行此程式碼 &mdash; 也就是在張貼表單時。</span><span class="sxs-lookup"><span data-stu-id="42527-251">The code is in an `if(IsPost)` block, because this code runs only when the user clicks the **Submit Changes** button &mdash; that is, when (and only when) the form has been posted.</span></span> <span data-ttu-id="42527-252">在此情況下，您不會使用類似 `if(IsPost && Validation.IsValid())`的測試，也就是說，您不會使用和來結合這兩個測試。</span><span class="sxs-lookup"><span data-stu-id="42527-252">In this case, you're not using a test like `if(IsPost && Validation.IsValid())`— that is, you're not combining both tests by using AND.</span></span> <span data-ttu-id="42527-253">在此頁面中，您會先判斷是否有提交表單（`if(IsPost)`），然後才註冊欄位進行驗證。</span><span class="sxs-lookup"><span data-stu-id="42527-253">In this page, you first determine whether there's a form submission (`if(IsPost)`), and only then register the fields for validation.</span></span> <span data-ttu-id="42527-254">然後，您可以測試驗證結果（`if(Validation.IsValid()`）。</span><span class="sxs-lookup"><span data-stu-id="42527-254">Then you can test the validation results (`if(Validation.IsValid()`).</span></span> <span data-ttu-id="42527-255">流程與 [ *AddMovie* ] 頁面中稍有不同，但效果相同。</span><span class="sxs-lookup"><span data-stu-id="42527-255">The flow is slightly different than in the *AddMovie.cshtml* page, but the effect is the same.</span></span>

<span data-ttu-id="42527-256">您可以使用其他 `<input>` 元素的 `Request.Form["title"]` 和類似的程式碼，來取得文字方塊的值。</span><span class="sxs-lookup"><span data-stu-id="42527-256">You get the values of the text boxes by using `Request.Form["title"]` and similar code for the other `<input>` elements.</span></span> <span data-ttu-id="42527-257">請注意，這次程式碼會從隱藏欄位（`<input type="hidden">`）取得電影識別碼。</span><span class="sxs-lookup"><span data-stu-id="42527-257">Notice that this time, the code gets the movie ID out of the hidden field (`<input type="hidden">`).</span></span> <span data-ttu-id="42527-258">當頁面第一次執行時，程式碼會從查詢字串中獲得識別碼。</span><span class="sxs-lookup"><span data-stu-id="42527-258">When the page ran the first time, the code got the ID out of the query string.</span></span> <span data-ttu-id="42527-259">您會從隱藏欄位取得值，以確定您取得原先顯示的電影識別碼，以防查詢字串在那之後發生某種程度的改變。</span><span class="sxs-lookup"><span data-stu-id="42527-259">You get the value from the hidden field to make sure that you're getting the ID of the movie that was originally displayed, in case the query string was somehow altered since then.</span></span>

<span data-ttu-id="42527-260">*AddMovie*程式碼與此程式碼之間的重要差異在於，在此程式碼中，您會使用 SQL `Update` 語句，而不是 `Insert Into` 語句。</span><span class="sxs-lookup"><span data-stu-id="42527-260">The really important difference between the *AddMovie* code and this code is that in this code you use the SQL `Update` statement instead of the `Insert Into` statement.</span></span> <span data-ttu-id="42527-261">下列範例顯示 SQL `Update` 語句的語法：</span><span class="sxs-lookup"><span data-stu-id="42527-261">The following example shows the syntax of the SQL `Update` statement:</span></span>

`UPDATE table SET col1="value", col2="value", col3="value" ... WHERE ID = value`

<span data-ttu-id="42527-262">您可以依任何順序指定任何資料行，而不一定要在 `Update` 作業期間更新每個資料行。</span><span class="sxs-lookup"><span data-stu-id="42527-262">You can specify any columns in any order, and you don't necessarily have to update every column during an `Update` operation.</span></span> <span data-ttu-id="42527-263">（您無法更新識別碼本身，因為這會生效地將記錄儲存為新記錄，而且不允許 `Update` 作業）。</span><span class="sxs-lookup"><span data-stu-id="42527-263">(You cannot update the ID itself, because that would in effect save the record as a new record, and that's not allowed for an `Update` operation.)</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="42527-264">**重要事項**具有識別碼的 `Where` 子句非常重要，因為這就是資料庫知道您要更新的資料庫記錄的方式。</span><span class="sxs-lookup"><span data-stu-id="42527-264">**Important** The `Where` clause with the ID is very important, because that's how the database knows which database record you want to update.</span></span> <span data-ttu-id="42527-265">如果您離開 `Where` 子句，資料庫將會更新資料庫中的*每一*筆記錄。</span><span class="sxs-lookup"><span data-stu-id="42527-265">If you left off the `Where` clause, the database would update *every* record in the database.</span></span> <span data-ttu-id="42527-266">在大部分情況下，這會造成嚴重損壞。</span><span class="sxs-lookup"><span data-stu-id="42527-266">In most cases, that would be a disaster.</span></span>

<span data-ttu-id="42527-267">在程式碼中，要更新的值會使用預留位置傳遞至 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="42527-267">In the code, the values to update are passed to the SQL statement by using placeholders.</span></span> <span data-ttu-id="42527-268">若要重複前面說過的內容：基於安全性考慮，請*只*使用預留位置將值傳遞給 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="42527-268">To repeat what we've said before: for security reasons, *only* use placeholders to pass values to a SQL statement.</span></span>

<span data-ttu-id="42527-269">在程式碼使用 `db.Execute` 執行 `Update` 語句之後，它會重新導向回 [清單] 頁面，您可以在其中查看變更。</span><span class="sxs-lookup"><span data-stu-id="42527-269">After the code uses `db.Execute` to run the `Update` statement, it redirects back to the listing page, where you can see the changes.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="42527-270">**不同的 SQL 語句，不同的方法**</span><span class="sxs-lookup"><span data-stu-id="42527-270">**Different SQL Statements, Different Methods**</span></span>
> 
> <span data-ttu-id="42527-271">您可能已經注意到，您會使用稍微不同的方法來執行不同的 SQL 語句。</span><span class="sxs-lookup"><span data-stu-id="42527-271">You might have noticed that you use slightly different methods to run different SQL statements.</span></span> <span data-ttu-id="42527-272">若要執行可能會傳回多筆記錄的 `Select` 查詢，您可以使用 `Query` 方法。</span><span class="sxs-lookup"><span data-stu-id="42527-272">To run a `Select` query that potentially returns multiple records, you use the `Query` method.</span></span> <span data-ttu-id="42527-273">若要執行您知道只會傳回一個資料庫專案的 `Select` 查詢，請使用 `QuerySingle` 方法。</span><span class="sxs-lookup"><span data-stu-id="42527-273">To run a `Select` query that you know will return only one database item, you use the `QuerySingle` method.</span></span> <span data-ttu-id="42527-274">若要執行進行變更但不會傳回資料庫專案的命令，您可以使用 `Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="42527-274">To run commands that make changes but that don't return database items, you use the `Execute` method.</span></span>
> 
> <span data-ttu-id="42527-275">您必須有不同的方法，因為它們會傳回不同的結果，如同您已在 `Query` 和 `QuerySingle`之間的差異中所見。</span><span class="sxs-lookup"><span data-stu-id="42527-275">You have to have different methods because each of them returns different results, as you saw already in the difference between `Query` and `QuerySingle`.</span></span> <span data-ttu-id="42527-276">（`Execute` 方法實際上會傳回值，&mdash; 也就是受 &mdash; 命令影響的資料庫資料列數目，但是您目前已忽略這種情況）。</span><span class="sxs-lookup"><span data-stu-id="42527-276">(The `Execute` method actually returns a value also &mdash; namely, the number of database rows that were affected by the command &mdash; but you've been ignoring that so far.)</span></span>
> 
> <span data-ttu-id="42527-277">當然，`Query` 方法可能只會傳回一個資料庫資料列。</span><span class="sxs-lookup"><span data-stu-id="42527-277">Of course, the `Query` method might return only one database row.</span></span> <span data-ttu-id="42527-278">不過，ASP.NET 一律會將 `Query` 方法的結果視為集合。</span><span class="sxs-lookup"><span data-stu-id="42527-278">However, ASP.NET always treats the results of the `Query` method as a collection.</span></span> <span data-ttu-id="42527-279">即使此方法只會傳回一個資料列，您還是必須從集合中將該單一資料列解壓縮。</span><span class="sxs-lookup"><span data-stu-id="42527-279">Even if the method returns just one row, you have to extract that single row from the collection.</span></span> <span data-ttu-id="42527-280">因此，在您*知道*您只會得到一個資料列的情況下，使用 `QuerySingle`會比較方便。</span><span class="sxs-lookup"><span data-stu-id="42527-280">Therefore, in situations where you *know* you'll get back only one row, it's a bit more convenient to use `QuerySingle`.</span></span>
> 
> <span data-ttu-id="42527-281">還有一些其他方法可執行特定類型的資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="42527-281">There are a few other methods that perform specific types of database operations.</span></span> <span data-ttu-id="42527-282">您可以在[ASP.NET WEB PAGES API 快速參考](../../api-reference/asp-net-web-pages-api-reference.md#Data)中找到資料庫方法的清單。</span><span class="sxs-lookup"><span data-stu-id="42527-282">You can find a listing of database methods in the [ASP.NET Web Pages API Quick Reference](../../api-reference/asp-net-web-pages-api-reference.md#Data).</span></span>

## <a name="making-validation-for-the-id-more-robust"></a><span data-ttu-id="42527-283">讓識別碼的驗證更健全</span><span class="sxs-lookup"><span data-stu-id="42527-283">Making Validation for the ID More Robust</span></span>

<span data-ttu-id="42527-284">第一次執行頁面時，您會從查詢字串取得電影識別碼，以便從資料庫取得該電影。</span><span class="sxs-lookup"><span data-stu-id="42527-284">The first time that the page runs, you get the movie ID from the query string so that you can go get that movie from the database.</span></span> <span data-ttu-id="42527-285">您確定確實有一個要尋找的值，也就是使用下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="42527-285">You made sure that there actually was a value to go look for, which you did by using this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample13.cs)]

<span data-ttu-id="42527-286">您已使用此程式碼來確定如果使用者到達*EditMovies*頁面，而未先在*電影*頁面中選取電影，則頁面會顯示使用者易記的錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="42527-286">You used this code to make sure that if a user gets to the *EditMovies* page without first selecting a movie in the *Movies* page, the page would display a user-friendly error message.</span></span> <span data-ttu-id="42527-287">（否則，使用者會看到一項錯誤，可能只會讓他們感到困惑）。</span><span class="sxs-lookup"><span data-stu-id="42527-287">(Otherwise, users would see an error that would probably just confuse them.)</span></span>

<span data-ttu-id="42527-288">不過，這種驗證並不穩定。</span><span class="sxs-lookup"><span data-stu-id="42527-288">However, this validation isn't very robust.</span></span> <span data-ttu-id="42527-289">此頁面可能也會因下列錯誤而叫用：</span><span class="sxs-lookup"><span data-stu-id="42527-289">The page might also be invoked with these errors:</span></span>

- <span data-ttu-id="42527-290">識別碼不是數位。</span><span class="sxs-lookup"><span data-stu-id="42527-290">The ID isn't a number.</span></span> <span data-ttu-id="42527-291">例如，您可以使用 `http://localhost:nnnnn/EditMovie?id=abc`之類的 URL 叫用此頁面。</span><span class="sxs-lookup"><span data-stu-id="42527-291">For example, the page could be invoked with a URL like `http://localhost:nnnnn/EditMovie?id=abc`.</span></span>
- <span data-ttu-id="42527-292">識別碼是數位，但它會參考不存在的電影（例如 `http://localhost:nnnnn/EditMovie?id=100934`）。</span><span class="sxs-lookup"><span data-stu-id="42527-292">The ID is a number, but it references a movie that doesn't exist (for example, `http://localhost:nnnnn/EditMovie?id=100934`).</span></span>

<span data-ttu-id="42527-293">如果您想要查看這些 Url 所產生的錯誤，請執行 [*電影*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="42527-293">If you're curious to see the errors that result from these URLs, run the *Movies* page.</span></span> <span data-ttu-id="42527-294">選取要編輯的電影，然後將 [ *EditMovie* ] 頁面的 url 變更為包含字母識別碼的 url，或不存在電影的識別碼。</span><span class="sxs-lookup"><span data-stu-id="42527-294">Select a movie to edit, and then change the URL of the *EditMovie* page to a URL that contains an alphabetic ID or the ID of a non-existent movie.</span></span>

<span data-ttu-id="42527-295">那麼，您該怎麼做呢？</span><span class="sxs-lookup"><span data-stu-id="42527-295">So what should you do?</span></span> <span data-ttu-id="42527-296">第一次修正是要確保不只是傳遞至頁面的識別碼，而是識別碼是整數。</span><span class="sxs-lookup"><span data-stu-id="42527-296">The first fix is to make sure that not only is an ID passed to the page, but that the ID is an integer.</span></span> <span data-ttu-id="42527-297">變更 `!IsPost` 測試的程式碼，使其看起來如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="42527-297">Change the code for the `!IsPost` test to look like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample14.cs)]

<span data-ttu-id="42527-298">您已將第二個條件新增至 `IsEmpty` 測試，並連結 `&&` （邏輯 AND）：</span><span class="sxs-lookup"><span data-stu-id="42527-298">You've added a second condition to the `IsEmpty` test, linked with `&&` (logical AND):</span></span>

[!code-csharp[Main](updating-data/samples/sample15.cs)]

<span data-ttu-id="42527-299">您可能會記得[ASP.NET Web Pages 程式設計](../introducing-razor-syntax-c.md)教學課程的簡介，這類方法 `AsBool` `AsInt` 將字元字串轉換成其他資料類型。</span><span class="sxs-lookup"><span data-stu-id="42527-299">You might remember from the [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md) tutorial that methods like `AsBool` an `AsInt` convert a character string to some other data type.</span></span> <span data-ttu-id="42527-300">`IsInt` 方法（和其他，如 `IsBool` 和 `IsDateTime`）類似。</span><span class="sxs-lookup"><span data-stu-id="42527-300">The `IsInt` method (and others, like `IsBool` and `IsDateTime`) are similar.</span></span> <span data-ttu-id="42527-301">不過，它們只會測試您是否*可以*轉換字串，而不會實際執行轉換。</span><span class="sxs-lookup"><span data-stu-id="42527-301">However, they test only whether you *can* convert the string, without actually performing the conversion.</span></span> <span data-ttu-id="42527-302">在這裡，您基本上會說*查詢字串值是否可以轉換成整數 ...* 。</span><span class="sxs-lookup"><span data-stu-id="42527-302">So here you're essentially saying *If the query string value can be converted to an integer ...*.</span></span>

<span data-ttu-id="42527-303">另一個可能的問題是尋找不存在的電影。</span><span class="sxs-lookup"><span data-stu-id="42527-303">The other potential problem is looking for a movie that doesn't exist.</span></span> <span data-ttu-id="42527-304">取得電影的程式碼看起來像下面這段程式碼：</span><span class="sxs-lookup"><span data-stu-id="42527-304">The code to get a movie looks like this code:</span></span>

[!code-csharp[Main](updating-data/samples/sample16.cs)]

<span data-ttu-id="42527-305">如果您將 `movieId` 值傳遞給未對應至實際電影的 `QuerySingle` 方法，則不會傳回任何內容，且後面的語句（例如，`title=row.Title`）會導致錯誤。</span><span class="sxs-lookup"><span data-stu-id="42527-305">If you pass a `movieId` value to the `QuerySingle` method that doesn't correspond to an actual movie, nothing is returned and the statements that follow (for example, `title=row.Title`) result in errors.</span></span>

<span data-ttu-id="42527-306">同樣地，有一個簡單的修正方法。</span><span class="sxs-lookup"><span data-stu-id="42527-306">Again there's an easy fix.</span></span> <span data-ttu-id="42527-307">如果 `db.QuerySingle` 方法未傳回任何結果，則 `row` 變數會是 null。</span><span class="sxs-lookup"><span data-stu-id="42527-307">If the `db.QuerySingle` method returns no results, the `row` variable will be null.</span></span> <span data-ttu-id="42527-308">因此，您可以先檢查 `row` 變數是否為 null，然後再嘗試從中取得值。</span><span class="sxs-lookup"><span data-stu-id="42527-308">So you can check whether the `row` variable is null before you try to get values from it.</span></span> <span data-ttu-id="42527-309">下列程式碼會在從 `row` 物件取得值的語句周圍加入 `if` 區塊：</span><span class="sxs-lookup"><span data-stu-id="42527-309">The following code adds an `if` block around the statements that get the values out of the `row` object:</span></span>

[!code-csharp[Main](updating-data/samples/sample17.cs)]

<span data-ttu-id="42527-310">使用這兩個額外的驗證測試，頁面會變得更具專案符號。</span><span class="sxs-lookup"><span data-stu-id="42527-310">With these two additional validation tests, the page becomes more bullet-proof.</span></span> <span data-ttu-id="42527-311">`!IsPost` 分支的完整程式碼現在看起來如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="42527-311">The complete code for the `!IsPost` branch now looks like this example:</span></span>

[!code-csharp[Main](updating-data/samples/sample18.cs)]

<span data-ttu-id="42527-312">我們會特別注意，這項工作是 `else` 組塊的好用。</span><span class="sxs-lookup"><span data-stu-id="42527-312">We'll note once more that this task is a good use for an `else` block.</span></span> <span data-ttu-id="42527-313">如果測試未通過，`else` 會封鎖設定錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="42527-313">If the tests don't pass, the `else` blocks set error messages.</span></span>

## <a name="adding-a-link-to-return-to-the-movies-page"></a><span data-ttu-id="42527-314">新增連結以返回電影頁面</span><span class="sxs-lookup"><span data-stu-id="42527-314">Adding a Link to Return to the Movies Page</span></span>

<span data-ttu-id="42527-315">最後還有一個有用的詳細資料，就是將連結新增回 [*電影*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="42527-315">A final and helpful detail is to add a link back to the *Movies* page.</span></span> <span data-ttu-id="42527-316">在一般事件流程中，使用者會從 [*電影*] 頁面開始，然後按一下 [**編輯**] 連結。</span><span class="sxs-lookup"><span data-stu-id="42527-316">In the ordinary flow of events, users will start at the *Movies* page and click an **Edit** link.</span></span> <span data-ttu-id="42527-317">這會將它們帶入*EditMovie*頁面，他們可以在其中編輯電影，然後按一下按鈕。</span><span class="sxs-lookup"><span data-stu-id="42527-317">That brings them to the *EditMovie* page, where they can edit the movie and click the button.</span></span> <span data-ttu-id="42527-318">在程式碼處理變更之後，它會重新導向回 [*電影*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="42527-318">After the code processes the change, it redirects back to the *Movies* page.</span></span>

<span data-ttu-id="42527-319">但是：</span><span class="sxs-lookup"><span data-stu-id="42527-319">However:</span></span>

- <span data-ttu-id="42527-320">使用者可能會決定不變更任何專案。</span><span class="sxs-lookup"><span data-stu-id="42527-320">The user might decide not to change anything.</span></span>
- <span data-ttu-id="42527-321">使用者可能已取得此頁面，而不需要先按一下 [*電影*] 頁面中的 [**編輯**] 連結。</span><span class="sxs-lookup"><span data-stu-id="42527-321">The user might have gotten to this page without first clicking an **Edit** link in the *Movies* page.</span></span>

<span data-ttu-id="42527-322">不論是哪一種方式，您都想要讓它們能夠輕鬆地回到主要清單。</span><span class="sxs-lookup"><span data-stu-id="42527-322">Either way, you want to make it easy for them to return to the main listing.</span></span> <span data-ttu-id="42527-323">這是一個簡單的修正 &mdash; 在標記中的結尾 `</form>` 標記之後加入下列標記：</span><span class="sxs-lookup"><span data-stu-id="42527-323">It's an easy fix &mdash; add the following markup just after the closing `</form>` tag in the markup:</span></span>

[!code-html[Main](updating-data/samples/sample19.html)]

<span data-ttu-id="42527-324">此標記會針對您在別處看到的 `<a>` 元素使用相同的語法。</span><span class="sxs-lookup"><span data-stu-id="42527-324">This markup uses the same syntax for an `<a>` element that you've seen elsewhere.</span></span> <span data-ttu-id="42527-325">URL 包含 `~` 表示「網站的根目錄」。</span><span class="sxs-lookup"><span data-stu-id="42527-325">The URL includes `~` to mean "root of the website."</span></span>

## <a name="testing-the-movie-update-process"></a><span data-ttu-id="42527-326">測試電影更新程式</span><span class="sxs-lookup"><span data-stu-id="42527-326">Testing the Movie Update Process</span></span>

<span data-ttu-id="42527-327">現在您可以測試。</span><span class="sxs-lookup"><span data-stu-id="42527-327">Now you can test.</span></span> <span data-ttu-id="42527-328">執行 [*電影*] 頁面，然後按一下電影旁的 [**編輯**]。</span><span class="sxs-lookup"><span data-stu-id="42527-328">Run the *Movies* page, and click **Edit** next to a movie.</span></span> <span data-ttu-id="42527-329">當 [ *EditMovie* ] 頁面出現時，對電影進行變更，然後按一下 [**提交變更**]。</span><span class="sxs-lookup"><span data-stu-id="42527-329">When the *EditMovie* page appears, make changes to the movie and click **Submit Changes**.</span></span> <span data-ttu-id="42527-330">當電影清單出現時，請確定您的變更已顯示。</span><span class="sxs-lookup"><span data-stu-id="42527-330">When the movie listing appears, make sure that your changes are shown.</span></span>

<span data-ttu-id="42527-331">若要確認驗證是否正常運作，請針對另一個電影按一下 [**編輯**]。</span><span class="sxs-lookup"><span data-stu-id="42527-331">To make sure that validation is working, click **Edit** for another movie.</span></span> <span data-ttu-id="42527-332">當您進入 [ *EditMovie* ] 頁面時，請清除 [內容類型] 欄位（或 [**年份** **] 欄位，** 或兩者），然後嘗試提交您的變更。</span><span class="sxs-lookup"><span data-stu-id="42527-332">When you get to the *EditMovie* page, clear the **Genre** field (or **Year** field, or both) and try to submit your changes.</span></span> <span data-ttu-id="42527-333">您會看到一則錯誤，如您所預期：</span><span class="sxs-lookup"><span data-stu-id="42527-333">You'll see an error, as you'd expect:</span></span>

![編輯顯示驗證錯誤的電影頁面](updating-data/_static/image4.png)

<span data-ttu-id="42527-335">按一下 [**返回電影清單**] 連結，放棄您所做的變更並返回 [*電影*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="42527-335">Click the **Return to movie listing** link to abandon your changes and return to the *Movies* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="42527-336">下一步</span><span class="sxs-lookup"><span data-stu-id="42527-336">Coming Up Next</span></span>

<span data-ttu-id="42527-337">在下一個教學課程中，您將瞭解如何刪除電影記錄。</span><span class="sxs-lookup"><span data-stu-id="42527-337">In the next tutorial, you'll see how to delete a movie record.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-edit-links"></a><span data-ttu-id="42527-338">電影頁面的完整清單（以編輯連結更新）</span><span class="sxs-lookup"><span data-stu-id="42527-338">Complete Listing for Movie Page (Updated with Edit Links)</span></span>

[!code-cshtml[Main](updating-data/samples/sample20.cshtml)]

<a id="Complete_Page_Listing_for_EditMovie"></a>
## <a name="complete-page-listing-for-edit-movie-page"></a><span data-ttu-id="42527-339">[編輯電影] 頁面的完成頁面清單</span><span class="sxs-lookup"><span data-stu-id="42527-339">Complete Page Listing for Edit Movie Page</span></span>

[!code-cshtml[Main](updating-data/samples/sample21.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="42527-340">其他資源</span><span class="sxs-lookup"><span data-stu-id="42527-340">Additional Resources</span></span>

- [<span data-ttu-id="42527-341">使用 Razor 語法 ASP.NET Web 程式設計的簡介</span><span class="sxs-lookup"><span data-stu-id="42527-341">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../../getting-started/introducing-razor-syntax-c.md)
- <span data-ttu-id="42527-342">W3Schools 網站上的[SQL UPDATE 語句](http://www.w3schools.com/sql/sql_update.asp)</span><span class="sxs-lookup"><span data-stu-id="42527-342">[SQL UPDATE Statement](http://www.w3schools.com/sql/sql_update.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="42527-343">[上一頁](entering-data.md)
> [下一頁](deleting-data.md)</span><span class="sxs-lookup"><span data-stu-id="42527-343">[Previous](entering-data.md)
[Next](deleting-data.md)</span></span>
