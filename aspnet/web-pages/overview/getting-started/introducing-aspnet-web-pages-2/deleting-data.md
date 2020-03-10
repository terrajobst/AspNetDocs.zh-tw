---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
title: ASP.NET Web Pages 簡介-刪除資料庫資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程會示範如何刪除個別的資料庫專案。 它假設您已透過更新 ASP.NET Web Pa 中的資料庫資料來完成數列 。
ms.author: riande
ms.date: 01/02/2018
ms.assetid: 75b5c1cf-84bd-434f-8a86-85c568eb5b09
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/deleting-data
msc.type: authoredcontent
ms.openlocfilehash: c8620fc1abc61d514bdc039c66f7a84e67e89abe
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78629035"
---
# <a name="introducing-aspnet-web-pages---deleting-database-data"></a><span data-ttu-id="9ac2d-104">ASP.NET Web Pages 簡介-刪除資料庫資料</span><span class="sxs-lookup"><span data-stu-id="9ac2d-104">Introducing ASP.NET Web Pages - Deleting Database Data</span></span>

<span data-ttu-id="9ac2d-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="9ac2d-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="9ac2d-106">本教學課程會示範如何刪除個別的資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-106">This tutorial shows you how to delete an individual database entry.</span></span> <span data-ttu-id="9ac2d-107">它假設您已透過[更新 ASP.NET Web Pages 中的資料庫資料](updating-data.md)來完成數列。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-107">It assumes you have completed the series through [Updating Database Data in ASP.NET Web Pages](updating-data.md).</span></span>
> 
> <span data-ttu-id="9ac2d-108">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="9ac2d-109">如何從記錄清單中選取個別記錄。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-109">How to select an individual record from a listing of records.</span></span>
> - <span data-ttu-id="9ac2d-110">如何從資料庫中刪除單一記錄。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-110">How to delete a single record from a database.</span></span>
> - <span data-ttu-id="9ac2d-111">如何檢查表單中是否已按一下特定按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-111">How to check that a specific button was clicked in a form.</span></span>
>   
> 
> <span data-ttu-id="9ac2d-112">討論的功能/技術：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-112">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="9ac2d-113">`WebGrid` helper。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-113">The `WebGrid` helper.</span></span>
> - <span data-ttu-id="9ac2d-114">SQL `Delete` 命令。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-114">The SQL `Delete` command.</span></span>
> - <span data-ttu-id="9ac2d-115">執行 SQL `Delete` 命令的 `Database.Execute` 方法。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-115">The `Database.Execute` method to run a SQL `Delete` command.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="9ac2d-116">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="9ac2d-116">What You'll Build</span></span>

<span data-ttu-id="9ac2d-117">在上一個教學課程中，您已瞭解如何更新現有的資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-117">In the previous tutorial, you learned how to update an existing database record.</span></span> <span data-ttu-id="9ac2d-118">本教學課程很類似，不同之處在于您會將它刪除，而不是更新記錄。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-118">This tutorial is similar, except that instead of updating the record, you'll delete it.</span></span> <span data-ttu-id="9ac2d-119">這些程式都是一樣的，不同之處在于刪除作業較簡單，因此本教學課程將會簡短。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-119">The processes are much the same, except that deleting is simpler, so this tutorial will be short.</span></span>

<span data-ttu-id="9ac2d-120">在 [*電影*] 頁面中，您將更新 `WebGrid` 協助程式，讓它顯示每個電影旁的 [**刪除**] 連結，以伴隨您稍早新增的**編輯**連結。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-120">In the *Movies* page, you'll update the `WebGrid` helper so that it displays a **Delete** link next to each movie to accompany the **Edit** link you added earlier.</span></span>

![顯示每個電影之刪除連結的電影頁面](deleting-data/_static/image1.png)

<span data-ttu-id="9ac2d-122">如同編輯，當您按一下 [**刪除**] 連結時，它會將您帶到不同的頁面，其中電影資訊已經在表單中：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-122">As with editing, when you click the **Delete** link, it takes you to a different page, where the movie information is already in a form:</span></span>

![刪除顯示電影的電影頁面](deleting-data/_static/image2.png)

<span data-ttu-id="9ac2d-124">然後，您可以按一下按鈕來永久刪除記錄。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-124">You can then click the button to delete the record permanently.</span></span>

## <a name="adding-a-delete-link-to-the-movie-listing"></a><span data-ttu-id="9ac2d-125">新增電影清單的刪除連結</span><span class="sxs-lookup"><span data-stu-id="9ac2d-125">Adding a Delete Link to the Movie Listing</span></span>

<span data-ttu-id="9ac2d-126">您將從新增 `WebGrid` helper 的**刪除**連結開始。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-126">You'll start by adding a **Delete** link to the `WebGrid` helper.</span></span> <span data-ttu-id="9ac2d-127">此連結類似于您在上一個教學課程中新增的 [**編輯**] 連結。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-127">This link is similar to the **Edit** link you added in a previous tutorial.</span></span>

<span data-ttu-id="9ac2d-128">開啟 [*電影*] 檔案。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-128">Open the *Movies.cshtml* file.</span></span>

<span data-ttu-id="9ac2d-129">藉由新增資料行來變更頁面主體中的 `WebGrid` 標記。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-129">Change the `WebGrid` markup in the body of the page by adding a column.</span></span> <span data-ttu-id="9ac2d-130">以下是修改過的標記：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-130">Here's the modified markup:</span></span>

[!code-html[Main](deleting-data/samples/sample1.html?highlight=9-10)]

<span data-ttu-id="9ac2d-131">新的資料行是這一項：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-131">The new column is this one:</span></span>

[!code-html[Main](deleting-data/samples/sample2.html)]

<span data-ttu-id="9ac2d-132">方格的設定方式，[**編輯**] 資料行會在方格中最左邊，而 [**刪除**] 資料行則最右邊。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-132">The way the grid is configured, the **Edit** column is leftmost in the grid and the **Delete** column is rightmost.</span></span> <span data-ttu-id="9ac2d-133">（現在在 [`Year`] 資料行後面有一個逗號，以免您發現）。這些連結資料行的位置並沒有什麼特殊之處，您可以輕鬆地將它們放在彼此旁。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-133">(There's a comma after the `Year` column now, in case you didn't notice that.) There's nothing special about where these link columns go, and you could as easily put them next to each other.</span></span> <span data-ttu-id="9ac2d-134">在此情況下，它們是分開的，使它們更難以進行混合。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-134">In this case, they're separate to make them harder to get mixed up.</span></span>

![已標記 [編輯] 和 [詳細資料] 連結的電影頁面，顯示它們不在彼此旁邊](deleting-data/_static/image3.png)

<span data-ttu-id="9ac2d-136">新的資料行會顯示其文字顯示為 "Delete" 的連結（`<a>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-136">The new column shows a link (`<a>` element) whose text says "Delete".</span></span> <span data-ttu-id="9ac2d-137">連結的目標（其 `href` 屬性）是最後解析成類似此 URL 的程式碼，每個電影的 `id` 值都不同：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-137">The target of the link (its `href` attribute) is code that ultimately resolves to something like this URL, with the `id` value different for each movie:</span></span>

[!code-css[Main](deleting-data/samples/sample3.css)]

<span data-ttu-id="9ac2d-138">此連結將會叫用名為*DeleteMovie*的頁面，並將您所選電影的識別碼傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-138">This link will invoke a page named *DeleteMovie* and pass it the ID of the movie you've selected.</span></span>

<span data-ttu-id="9ac2d-139">本教學課程將不會詳細說明如何建立此連結，因為它與上一個教學課程中的 [**編輯**] 連結（[更新 ASP.NET Web Pages 中的資料庫資料](updating-data.md)）幾乎相同。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-139">This tutorial won't go into detail about how this link is constructed, because it's almost identical to the **Edit** link from the previous tutorial ([Updating Database Data in ASP.NET Web Pages](updating-data.md)).</span></span>

## <a name="creating-the-delete-page"></a><span data-ttu-id="9ac2d-140">建立 [刪除] 頁面</span><span class="sxs-lookup"><span data-stu-id="9ac2d-140">Creating the Delete Page</span></span>

<span data-ttu-id="9ac2d-141">現在您可以建立將做為方格中 [**刪除**] 連結目標的頁面。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-141">Now you can create the page that will be the target for the **Delete** link in the grid.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="9ac2d-142">**重要事項**第一次選取要刪除的記錄，然後使用個別的頁面和按鈕來確認程式對於安全性非常重要的技巧。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-142">**Important** The technique of first selecting a record to delete and then using a separate page and button to confirm the process is extremely important for security.</span></span> <span data-ttu-id="9ac2d-143">如同您在先前的教學課程中所閱讀，對您的網站進行*任何*變更時，應該*一律*使用表單 &mdash; 也就是使用 HTTP POST 作業來完成。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-143">As you've read in previous tutorials, making *any* sort of change to your website should *always* be done using a form &mdash; that is, using an HTTP POST operation.</span></span> <span data-ttu-id="9ac2d-144">如果您只要按一下連結（也就是使用「取得」作業）來變更網站，人們就可以對您的網站提出簡單的要求，並刪除您的資料。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-144">If you made it possible to change the site just by clicking a link (that is, using a GET operation), people could make simple requests to your site and delete your data.</span></span> <span data-ttu-id="9ac2d-145">即使是索引網站的搜尋引擎編目程式，也可能會因為下列連結而不小心刪除資料。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-145">Even a search-engine crawler that's indexing your site could inadvertently delete data just by following links.</span></span>
> 
> <span data-ttu-id="9ac2d-146">當您的應用程式可讓使用者變更記錄時，您必須將記錄呈現給使用者，才能進行編輯。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-146">When your app lets people change a record, you have to present the record to the user for editing anyway.</span></span> <span data-ttu-id="9ac2d-147">但您可能會想要略過此步驟來刪除記錄。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-147">But you might be tempted to skip this step for deleting a record.</span></span> <span data-ttu-id="9ac2d-148">不過，請勿略過該步驟。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-148">Don't skip that step, though.</span></span> <span data-ttu-id="9ac2d-149">（這也有助於使用者查看記錄，並確認他們正在刪除其所需的記錄）。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-149">(It's also helpful for users to see the record and confirm that they're deleting the record that they intended.)</span></span>
> 
> <span data-ttu-id="9ac2d-150">在後續的教學課程設定中，您將瞭解如何新增登入功能，讓使用者在刪除記錄之前必須先登入。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-150">In a subsequent tutorial set, you'll see how to add login functionality so a user would have to log in before deleting a record.</span></span>

<span data-ttu-id="9ac2d-151">建立名為*DeleteMovie*的頁面，並以下列標記取代檔案中的內容：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-151">Create a page named *DeleteMovie.cshtml* and replace what's in the file with the following markup:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample4.cshtml)]

<span data-ttu-id="9ac2d-152">此標記類似于*EditMovie*頁面，不同之處在于，標記包含 `<span>` 元素，而不是使用文字方塊（`<input type="text">`）。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-152">This markup is like the *EditMovie* pages, except that instead of using text boxes (`<input type="text">`), the markup includes `<span>` elements.</span></span> <span data-ttu-id="9ac2d-153">這裡沒有任何要編輯的東西。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-153">There's nothing here to edit.</span></span> <span data-ttu-id="9ac2d-154">您只需要顯示電影詳細資料，讓使用者可以確定他們刪除的是正確的電影。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-154">All you have to do is display the movie details so that users can make sure that they're deleting the right movie.</span></span>

<span data-ttu-id="9ac2d-155">標記已經包含一個連結，可讓使用者回到電影清單頁面。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-155">The markup already contains a link that lets the user return to the movie listing page.</span></span>

<span data-ttu-id="9ac2d-156">如同在 [ *EditMovie* ] 頁面中，所選電影的識別碼會儲存在隱藏欄位中。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-156">As in the *EditMovie* page, the ID of the selected movie is stored in a hidden field.</span></span> <span data-ttu-id="9ac2d-157">（它會在第一個位置以查詢字串值的形式傳遞至頁面。）有一個 `Html.ValidationSummary` 呼叫會顯示驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-157">(It's passed into the page in the first place as a query string value.) There's an `Html.ValidationSummary` call that will display validation errors.</span></span> <span data-ttu-id="9ac2d-158">在此情況下，錯誤可能是未將電影識別碼傳遞至頁面，或電影識別碼無效。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-158">In this case, the error might be that no movie ID was passed to the page or that the movie ID is invalid.</span></span> <span data-ttu-id="9ac2d-159">如果有人執行此頁面，而未先在 [*電影*] 頁面中選取電影，就會發生這種情況。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-159">This situation could occur if someone ran this page without first selecting a movie in the *Movies* page.</span></span>

<span data-ttu-id="9ac2d-160">按鈕標題為 [**刪除電影**]，而其 [名稱] 屬性設定為 [`buttonDelete`]。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-160">The button caption is **Delete Movie**, and its name attribute is set to `buttonDelete`.</span></span> <span data-ttu-id="9ac2d-161">`name` 屬性將用於程式碼中，以識別提交表單的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-161">The `name` attribute will be used in the code to identify the button that submitted the form.</span></span>

<span data-ttu-id="9ac2d-162">當第一次顯示網頁時，您必須將程式碼寫入1）讀取電影詳細資料，而2）則會在使用者按一下按鈕時實際刪除電影。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-162">You'll have to write code to 1) read the movie details when the page is first displayed and 2) actually delete the movie when the user clicks the button.</span></span>

## <a name="adding-code-to-read-a-single-movie"></a><span data-ttu-id="9ac2d-163">新增程式碼以讀取單一電影</span><span class="sxs-lookup"><span data-stu-id="9ac2d-163">Adding Code to Read a Single Movie</span></span>

<span data-ttu-id="9ac2d-164">在 [ *DeleteMovie* ] 頁面的頂端，新增下列程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-164">At the top of the *DeleteMovie.cshtml* page, add the following code block:</span></span>

[!code-cshtml[Main](deleting-data/samples/sample5.cshtml)]

<span data-ttu-id="9ac2d-165">此標記與 [ *EditMovie* ] 頁面中的對應程式碼相同。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-165">This markup is the same as the corresponding code in the *EditMovie* page.</span></span> <span data-ttu-id="9ac2d-166">它會從查詢字串中取得影片識別碼，並使用識別碼從資料庫讀取記錄。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-166">It gets the movie ID out of the query string and uses the ID to read a record from the database.</span></span> <span data-ttu-id="9ac2d-167">程式碼包含驗證測試（`IsInt()` 和 `row != null`），以確定傳遞至頁面的電影識別碼是有效的。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-167">The code includes the validation test (`IsInt()` and `row != null`) to make sure that the movie ID being passed to the page is valid.</span></span>

<span data-ttu-id="9ac2d-168">請記住，此程式碼應該只在頁面第一次執行時執行。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-168">Remember that this code should only run the first time the page runs.</span></span> <span data-ttu-id="9ac2d-169">當使用者按一下 [**刪除電影**] 按鈕時，您不會想要從資料庫重新讀取電影記錄。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-169">You don't want to re-read the movie record from the database when the user clicks the **Delete Movie** button.</span></span> <span data-ttu-id="9ac2d-170">因此，*如果要求不是 post 作業（表單提交）* ，則會在測試中顯示用來讀取電影的程式碼，`if(!IsPost)` &mdash;。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-170">Therefore, code to read the movie is inside a test that says `if(!IsPost)` &mdash; that is, *if the request is not a post operation (form submission)*.</span></span>

## <a name="adding-code-to-delete-the-selected-movie"></a><span data-ttu-id="9ac2d-171">新增程式碼以刪除選取的電影</span><span class="sxs-lookup"><span data-stu-id="9ac2d-171">Adding Code to Delete the Selected Movie</span></span>

<span data-ttu-id="9ac2d-172">若要在使用者按一下按鈕時刪除電影，請在 `@` 區塊的右大括弧內新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-172">To delete the movie when the user clicks the button, add the following code just inside the closing brace of the `@` block:</span></span>

[!code-csharp[Main](deleting-data/samples/sample6.cs)]

<span data-ttu-id="9ac2d-173">此程式碼類似于更新現有記錄的程式碼，但較簡單。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-173">This code is similar to the code for updating an existing record, but simpler.</span></span> <span data-ttu-id="9ac2d-174">此程式碼基本上會執行 SQL `Delete` 語句。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-174">The code basically runs a SQL `Delete` statement.</span></span>

 <span data-ttu-id="9ac2d-175">如同在 [ *EditMovie* ] 頁面中，程式碼位於 `if(IsPost)` 區塊中。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-175">As in the *EditMovie* page, the code is in an `if(IsPost)` block.</span></span> <span data-ttu-id="9ac2d-176">這一次，`if()` 條件有點複雜：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-176">This time, the `if()` condition is a little more complicated:</span></span> 

[!code-csharp[Main](deleting-data/samples/sample7.cs)]

<span data-ttu-id="9ac2d-177">這裡有兩個條件。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-177">There are two conditions here.</span></span> <span data-ttu-id="9ac2d-178">第一種方式是提交頁面，就像您在 &mdash; `if(IsPost)`之前所看到的一樣。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-178">The first is that the page is being submitted, as you've seen before &mdash; `if(IsPost)`.</span></span>

<span data-ttu-id="9ac2d-179">第二個條件是 `!Request["buttonDelete"].IsEmpty()`，表示要求具有名為 `buttonDelete`的物件。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-179">The second condition is `!Request["buttonDelete"].IsEmpty()`, meaning that the request has an object named `buttonDelete`.</span></span> <span data-ttu-id="9ac2d-180">無可否認的，這是測試提交表單之按鈕的間接方式。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-180">Admittedly, it's an indirect way of testing which button submitted the form.</span></span> <span data-ttu-id="9ac2d-181">如果表單包含多個 [提交] 按鈕，則只會在要求中出現所按下的按鈕名稱。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-181">If a form contains multiple submit buttons, only the name of the button that was clicked appears in the request.</span></span> <span data-ttu-id="9ac2d-182">因此，在邏輯上，如果特定按鈕的名稱出現在要求 &mdash; 中，或如程式碼中所述，如果該按鈕不是空的 &mdash; 這就是提交表單的按鈕。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-182">Therefore, logically, if the name of a particular button appears in the request &mdash; or as stated in the code, if that button isn't empty &mdash; that's the button that submitted the form.</span></span>

<span data-ttu-id="9ac2d-183">`&&` 運算子表示 "and" （邏輯 AND）。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-183">The `&&` operator means "and" (logical AND).</span></span> <span data-ttu-id="9ac2d-184">因此，整個 `if` 條件為 。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-184">Therefore the entire `if` condition is ...</span></span>

<span data-ttu-id="9ac2d-185">*此要求是 post （不是第一次要求）*</span><span class="sxs-lookup"><span data-stu-id="9ac2d-185">*This request is a post (not a first-time request)*</span></span>  
  
 <span data-ttu-id="9ac2d-186">AND</span><span class="sxs-lookup"><span data-stu-id="9ac2d-186">AND</span></span>  
  
<span data-ttu-id="9ac2d-187">*[* `buttonDelete`]*按鈕是提交表單的按鈕。*</span><span class="sxs-lookup"><span data-stu-id="9ac2d-187">*The* `buttonDelete`*button was the button that submitted the form.*</span></span>

<span data-ttu-id="9ac2d-188">這個表單（事實上，此頁面）只包含一個按鈕，因此技術上不需要 `buttonDelete` 的額外測試。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-188">This form (in fact, this page) contains only one button, so the additional test for `buttonDelete` is technically not required.</span></span> <span data-ttu-id="9ac2d-189">但是，您即將執行會永久移除資料的作業。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-189">Still, you're about to perform an operation that will permanently remove data.</span></span> <span data-ttu-id="9ac2d-190">因此，您想要盡可能確保只有在使用者明確要求作業時才執行作業。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-190">So you want to be as sure as possible that you're performing the operation only when the user has explicitly requested it.</span></span> <span data-ttu-id="9ac2d-191">例如，假設您稍後展開此頁面，並將其他按鈕加入其中。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-191">For example, suppose that you expanded this page later and added other buttons to it.</span></span> <span data-ttu-id="9ac2d-192">就算如此，刪除影片的程式碼只會在按一下 [`buttonDelete`] 按鈕時執行。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-192">Even then, the code that deletes the movie will run only if the `buttonDelete` button was clicked.</span></span>

<span data-ttu-id="9ac2d-193">如同在 [ *EditMovie* ] 頁面中，您會從隱藏的欄位取得識別碼，然後執行 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-193">As in the *EditMovie* page, you get the ID from the hidden field and then run the SQL command.</span></span> <span data-ttu-id="9ac2d-194">`Delete` 語句的語法為：</span><span class="sxs-lookup"><span data-stu-id="9ac2d-194">The syntax for the `Delete` statement is:</span></span>

`DELETE FROM table WHERE ID = value`

<span data-ttu-id="9ac2d-195">請務必包含 `WHERE` 子句和識別碼。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-195">It's vital to include the `WHERE` clause and the ID.</span></span> <span data-ttu-id="9ac2d-196">如果您省略 WHERE 子句，將會*刪除資料表中的所有記錄*。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-196">If you leave out the WHERE clause, *all the records in the table will be deleted*.</span></span> <span data-ttu-id="9ac2d-197">如您所見，您可以使用預留位置，將識別碼值傳遞至 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-197">As you have seen, you pass the ID value to the SQL command by using a placeholder.</span></span>

## <a name="testing-the-movie-delete-process"></a><span data-ttu-id="9ac2d-198">測試電影刪除流程</span><span class="sxs-lookup"><span data-stu-id="9ac2d-198">Testing the Movie Delete Process</span></span>

<span data-ttu-id="9ac2d-199">現在您可以測試。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-199">Now you can test.</span></span> <span data-ttu-id="9ac2d-200">執行 [*電影*] 頁面，然後按一下電影旁的 [**刪除**]。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-200">Run the *Movies* page, and click **Delete** next to a movie.</span></span> <span data-ttu-id="9ac2d-201">當 [ *DeleteMovie* ] 頁面出現時，按一下 [**刪除電影**]。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-201">When the *DeleteMovie* page appears, click **Delete Movie**.</span></span>

![已反白顯示 [刪除電影] 按鈕的 [刪除電影] 頁面](deleting-data/_static/image4.png)

<span data-ttu-id="9ac2d-203">當您按一下按鈕時，程式碼會刪除電影，並返回電影清單。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-203">When you click the button, the code deletes the movies and returns to the movie listing.</span></span> <span data-ttu-id="9ac2d-204">您可以在這裡搜尋已刪除的電影，並確認它已被刪除。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-204">There you can search for the deleted movie and confirm that it's been deleted.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="9ac2d-205">下一步</span><span class="sxs-lookup"><span data-stu-id="9ac2d-205">Coming Up Next</span></span>

<span data-ttu-id="9ac2d-206">下一個教學課程會示範如何為網站上的所有頁面提供常見的外觀和版面配置。</span><span class="sxs-lookup"><span data-stu-id="9ac2d-206">The next tutorial shows you how to give all the pages on your site a common look and layout.</span></span>

## <a name="complete-listing-for-movie-page-updated-with-delete-links"></a><span data-ttu-id="9ac2d-207">電影頁面的完整清單（以刪除連結更新）</span><span class="sxs-lookup"><span data-stu-id="9ac2d-207">Complete Listing for Movie Page (Updated with Delete Links)</span></span>

[!code-cshtml[Main](deleting-data/samples/sample8.cshtml)]

## <a name="complete-listing-for-deletemovie-page"></a><span data-ttu-id="9ac2d-208">DeleteMovie 頁面的完整清單</span><span class="sxs-lookup"><span data-stu-id="9ac2d-208">Complete Listing for DeleteMovie Page</span></span>

[!code-cshtml[Main](deleting-data/samples/sample9.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="9ac2d-209">其他資源</span><span class="sxs-lookup"><span data-stu-id="9ac2d-209">Additional Resources</span></span>

- [<span data-ttu-id="9ac2d-210">使用 Razor 語法 ASP.NET Web 程式設計的簡介</span><span class="sxs-lookup"><span data-stu-id="9ac2d-210">Introduction to ASP.NET Web Programming by Using the Razor Syntax</span></span>](../introducing-razor-syntax-c.md)
- <span data-ttu-id="9ac2d-211">W3Schools 網站上的[SQL DELETE 子句](http://www.w3schools.com/sql/sql_delete.asp)</span><span class="sxs-lookup"><span data-stu-id="9ac2d-211">[SQL DELETE Statement](http://www.w3schools.com/sql/sql_delete.asp) on the W3Schools site</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9ac2d-212">[上一頁](updating-data.md)
> [下一頁](layouts.md)</span><span class="sxs-lookup"><span data-stu-id="9ac2d-212">[Previous](updating-data.md)
[Next](layouts.md)</span></span>
