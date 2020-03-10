---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
title: 簡介 ASP.NET Web Pages 使用表單輸入資料庫資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程會示範如何建立輸入表單，然後在使用 ASP.NET Web Pages （...）時，將您從表單取得的資料輸入至資料庫資料表。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: d37c93fc-25fd-4e94-8671-0d437beef206
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/entering-data
msc.type: authoredcontent
ms.openlocfilehash: b9354a7b97a7df9020a681f709e16a92650cfcf0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624534"
---
# <a name="introducing-aspnet-web-pages---entering-database-data-by-using-forms"></a><span data-ttu-id="6f1a8-103">簡介 ASP.NET Web Pages 使用表單輸入資料庫資料</span><span class="sxs-lookup"><span data-stu-id="6f1a8-103">Introducing ASP.NET Web Pages - Entering Database Data by Using Forms</span></span>

<span data-ttu-id="6f1a8-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="6f1a8-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="6f1a8-105">本教學課程會示範如何建立輸入表單，然後在使用 ASP.NET Web Pages （Razor）時，將您從表單中取得的資料輸入至資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-105">This tutorial shows you how to create an entry form and then enter the data that you get from the form into a database table when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="6f1a8-106">它假設您已[在 ASP.NET Web Pages 中，透過 HTML 表單的基本概念](https://go.microsoft.com/fwlink/?LinkId=251581)來完成數列。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-106">It assumes you have completed the series through [Basics of HTML Forms in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581).</span></span>
> 
> <span data-ttu-id="6f1a8-107">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-107">What you'll learn:</span></span>
> 
> - <span data-ttu-id="6f1a8-108">深入瞭解如何處理輸入表單。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-108">More about how to process entry forms.</span></span>
> - <span data-ttu-id="6f1a8-109">如何在資料庫中加入（插入）資料。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-109">How to add (insert) data in a database.</span></span>
> - <span data-ttu-id="6f1a8-110">如何確保使用者在表單中輸入了必要的值（如何驗證使用者輸入）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-110">How to make sure that users have entered a required value in a form (how to validate user input).</span></span>
> - <span data-ttu-id="6f1a8-111">如何顯示驗證錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-111">How to display validation errors.</span></span>
> - <span data-ttu-id="6f1a8-112">如何從目前的頁面跳到另一個頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-112">How to jump to another page from the current page.</span></span>
>   
> 
> <span data-ttu-id="6f1a8-113">討論的功能/技術：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-113">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="6f1a8-114">`Database.Execute` 方法</span><span class="sxs-lookup"><span data-stu-id="6f1a8-114">The `Database.Execute` method.</span></span>
> - <span data-ttu-id="6f1a8-115">SQL `Insert Into` 語句</span><span class="sxs-lookup"><span data-stu-id="6f1a8-115">The SQL `Insert Into` statement</span></span>
> - <span data-ttu-id="6f1a8-116">`Validation` helper。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-116">The `Validation` helper.</span></span>
> - <span data-ttu-id="6f1a8-117">`Response.Redirect` 方法</span><span class="sxs-lookup"><span data-stu-id="6f1a8-117">The `Response.Redirect` method.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="6f1a8-118">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="6f1a8-118">What You'll Build</span></span>

<span data-ttu-id="6f1a8-119">在先前示範如何建立資料庫的教學課程中，您可以直接在 WebMatrix 中編輯資料庫來輸入資料庫資料，請在 [**資料庫**] 工作區中工作。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-119">In the tutorial earlier that showed you how to create a database, you entered database data by editing the database directly in WebMatrix, working in the **Database** workspace.</span></span> <span data-ttu-id="6f1a8-120">不過在大部分的應用程式中，這不是將資料放入資料庫的實用方式。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-120">In most apps, that's not a practical way to put data into the database, though.</span></span> <span data-ttu-id="6f1a8-121">因此，在本教學課程中，您將建立 web 型介面，讓您或任何人輸入資料並將其儲存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-121">So in this tutorial, you'll create a web-based interface that lets you or anyone enter data and save it to the database.</span></span>

<span data-ttu-id="6f1a8-122">您將建立可在其中輸入新電影的頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-122">You'll create a page where you can enter new movies.</span></span> <span data-ttu-id="6f1a8-123">此頁面會包含一個輸入表單，其中具有欄位（文字方塊），您可以在其中輸入電影標題、內容類型和年份。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-123">The page will contain an entry form that has fields (text boxes) where you can enter a movie title, genre, and year.</span></span> <span data-ttu-id="6f1a8-124">頁面看起來會像這個頁面：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-124">The page will look like this page:</span></span>

![瀏覽器中的 [新增電影] 頁面](entering-data/_static/image1.png)

<span data-ttu-id="6f1a8-126">文字方塊會是 HTML `<input>` 專案，看起來就像此標記：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-126">The text boxes will be HTML `<input>` elements that will look like this markup:</span></span>

`<input type="text" name="genre" value="" />`

## <a name="creating-the-basic-entry-form"></a><span data-ttu-id="6f1a8-127">建立基本輸入表單</span><span class="sxs-lookup"><span data-stu-id="6f1a8-127">Creating the Basic Entry Form</span></span>

<span data-ttu-id="6f1a8-128">建立名為*AddMovie*的頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-128">Create a page named *AddMovie.cshtml*.</span></span>

<span data-ttu-id="6f1a8-129">以下列標記取代檔案中的內容。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-129">Replace what's in the file with the following markup.</span></span> <span data-ttu-id="6f1a8-130">全部覆寫;您很快就會在頂端新增程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-130">Overwrite everything; you'll add a code block at the top shortly.</span></span>

[!code-cshtml[Main](entering-data/samples/sample1.cshtml)]

<span data-ttu-id="6f1a8-131">這個範例會顯示建立表單的一般 HTML。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-131">This example shows typical HTML for creating a form.</span></span> <span data-ttu-id="6f1a8-132">它會針對文字方塊和 [提交] 按鈕使用 `<input>` 元素。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-132">It uses `<input>` elements for the text boxes and for the submit button.</span></span> <span data-ttu-id="6f1a8-133">文字方塊的標題是使用標準 `<label>` 元素所建立。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-133">The captions for the text boxes are created by using standard `<label>` elements.</span></span> <span data-ttu-id="6f1a8-134">`<fieldset>` 和 `<legend>` 元素會在表單周圍放置一個不錯的方塊。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-134">The `<fieldset>` and `<legend>` elements put a nice box around the form.</span></span>

<span data-ttu-id="6f1a8-135">請注意，在此頁面中，`<form>` 元素會使用 `post` 做為 `method` 屬性的值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-135">Notice that in this page, the `<form>` element uses `post` as the value for the `method` attribute.</span></span> <span data-ttu-id="6f1a8-136">在上一個教學課程中，您已建立一個使用 `get` 方法的表單。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-136">In the previous tutorial, you created a form that used the `get` method.</span></span> <span data-ttu-id="6f1a8-137">這是正確的，因為雖然表單已提交值給伺服器，但要求並未進行任何變更。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-137">That was correct, because although the form submitted values to the server, the request did not make any changes.</span></span> <span data-ttu-id="6f1a8-138">這一切都是以不同的方式提取資料。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-138">All it did was fetch data in different ways.</span></span> <span data-ttu-id="6f1a8-139">不過，在此頁面中，您*將會*進行變更，也就是加入新的資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-139">However, in this page you *will* make changes—you're going to add new database records.</span></span> <span data-ttu-id="6f1a8-140">因此，此表單應該使用 `post` 方法。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-140">Therefore, this form should use the `post` method.</span></span> <span data-ttu-id="6f1a8-141">（如需 `GET` 和 `POST` 作業之間差異的詳細資訊，請參閱上一個教學課程中的[GET、POST 和 HTTP Verb 安全](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety)提要欄位）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-141">(For more about the difference between `GET` and `POST` operations, see the[GET, POST, and HTTP Verb Safety](https://go.microsoft.com/fwlink/?LinkId=251581#GET,_POST,_and_HTTP_Verb_Safety) sidebar in the previous tutorial.)</span></span>

<span data-ttu-id="6f1a8-142">請注意，每個文字方塊都有一個 `name` 元素（`title`、`genre``year`）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-142">Note that each text box has a `name` element (`title`, `genre`, `year`).</span></span> <span data-ttu-id="6f1a8-143">如您在上一個教學課程中所見，這些名稱很重要，因為您必須擁有這些名稱，才能在稍後取得使用者的輸入。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-143">As you saw in the previous tutorial, these names are important because you must have those names so you can get the user's input later.</span></span> <span data-ttu-id="6f1a8-144">您可以使用任何名稱。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-144">You can use any names.</span></span> <span data-ttu-id="6f1a8-145">使用有意義的名稱有助於記住您所使用的資料，是很有説明的。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-145">It's helpful to use meaningful names that help you remember what data you're working with.</span></span>

<span data-ttu-id="6f1a8-146">每個 `<input>` 元素的 `value` 屬性包含一些 Razor 程式碼（例如，`Request.Form["title"]`）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-146">The `value` attribute of each `<input>` element contains a bit of Razor code (for example, `Request.Form["title"]`).</span></span> <span data-ttu-id="6f1a8-147">您已在上一個教學課程中瞭解此技巧的某個版本，以在提交表單後保留在文字方塊中輸入的值（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-147">You learned a version of this trick in the previous tutorial to preserve the value entered into the text box (if any) after the form has been submitted.</span></span>

## <a name="getting-the-form-values"></a><span data-ttu-id="6f1a8-148">取得表單值</span><span class="sxs-lookup"><span data-stu-id="6f1a8-148">Getting the Form Values</span></span>

<span data-ttu-id="6f1a8-149">接下來，您可以加入處理表單的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-149">Next, you add code that processes the form.</span></span> <span data-ttu-id="6f1a8-150">在大綱中，您會執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-150">In outline, you'll do the following:</span></span>

1. <span data-ttu-id="6f1a8-151">檢查頁面是否正在張貼（已提交）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-151">Check whether the page is being posted (was submitted).</span></span> <span data-ttu-id="6f1a8-152">您只想要讓程式碼在使用者按下按鈕時執行，而不是在頁面第一次執行時執行。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-152">You want to your code to run only when users have clicked the button, not when the page first runs.</span></span>
2. <span data-ttu-id="6f1a8-153">取得使用者在文字方塊中輸入的值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-153">Get the values that the user entered into the text boxes.</span></span> <span data-ttu-id="6f1a8-154">在此情況下，因為表單使用 `POST` 動詞，所以您會從 `Request.Form` 集合取得表單值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-154">In this case, because the form is using the `POST` verb, you get the form values from the `Request.Form` collection.</span></span>
3. <span data-ttu-id="6f1a8-155">將這些值插入*電影*資料庫資料表中的新記錄。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-155">Insert the values as a new record in the *Movies* database table.</span></span>

<span data-ttu-id="6f1a8-156">在檔案的頂端，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-156">At the top of the file, add the following code:</span></span>

[!code-cshtml[Main](entering-data/samples/sample2.cshtml)]

<span data-ttu-id="6f1a8-157">前幾行會建立變數（`title`、`genre`和 `year`），以保存文字方塊中的值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-157">The first few lines create variables (`title`, `genre`, and `year`) to hold the values from the text boxes.</span></span> <span data-ttu-id="6f1a8-158">這一行 `if(IsPost)` 確保只有在使用者按一下 [**新增電影**] 按鈕時，也就是在張貼表單時，*才*會設定變數。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-158">The line `if(IsPost)` makes sure that the variables are set *only* when users click the **Add Movie** button — that is, when the form has been posted.</span></span>

<span data-ttu-id="6f1a8-159">如您在先前的教學課程中所見，您可以使用運算式（例如 `Request.Form["name"]`）來取得文字方塊的值，其中*name*是 `<input>` 元素的名稱。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-159">As you saw in an earlier tutorial, you get the value of a text box by using an expression like `Request.Form["name"]`, where *name* is the name of the `<input>` element.</span></span>

<span data-ttu-id="6f1a8-160">變數的名稱（`title`、`genre`和 `year`）是任意的。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-160">The names of the variables (`title`, `genre`, and `year`) are arbitrary.</span></span> <span data-ttu-id="6f1a8-161">就像您指派給 `<input>` 元素的名稱一樣，您可以隨意呼叫它們。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-161">Like the names that you assign to `<input>` elements, you can call them anything you like.</span></span> <span data-ttu-id="6f1a8-162">（變數的名稱不一定要與表單上 `<input>` 元素的名稱屬性相符）。但是如同 `<input>` 的元素，使用變數名稱來反映它們所包含的資料，是個不錯的主意。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-162">(The names of the variables don't have to match the name attributes of `<input>` elements on the form.) But as with the `<input>` elements, it's a good idea to use variable names that reflect the data that they contain.</span></span> <span data-ttu-id="6f1a8-163">當您撰寫程式碼時，一致的名稱可讓您更輕鬆地記住您所使用的資料。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-163">When you write code, consistent names make it easier for you to remember what data you're working with.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="6f1a8-164">將資料新增至資料庫</span><span class="sxs-lookup"><span data-stu-id="6f1a8-164">Adding Data to the Database</span></span>

<span data-ttu-id="6f1a8-165">在您剛才加入的程式碼區塊中，只在 `if` 區塊的右大括弧（`}`）*內*（而不是在程式碼區塊內），新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-165">In the code block you just added, just *inside* the closing brace ( `}` ) of the `if` block (not just inside the code block), add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample3.cs)]

<span data-ttu-id="6f1a8-166">這個範例類似于您在上一個教學課程中用來提取和顯示資料的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-166">This example is similar to the code you used in a previous tutorial to fetch and display data.</span></span> <span data-ttu-id="6f1a8-167">以 `db =` 開頭的那一行會開啟資料庫（如先前的程式碼），而下一行會定義 SQL 語句，如同您之前所看到的一樣。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-167">The line that starts with `db =` opens the database, like before, and the next line defines a SQL statement, again as you saw before.</span></span> <span data-ttu-id="6f1a8-168">不過，這次它會定義 SQL `Insert Into` 語句。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-168">However, this time it defines a SQL `Insert Into` statement.</span></span> <span data-ttu-id="6f1a8-169">下列範例顯示 `Insert Into` 語句的一般語法：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-169">The following example shows the general syntax of the `Insert Into` statement:</span></span>

`INSERT INTO table (column1, column2, column3, ...) VALUES (value1, value2, value3, ...)`

<span data-ttu-id="6f1a8-170">換句話說，您可以指定要插入的資料表，然後列出要插入的資料行，再列出要插入的值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-170">In other words, you specify the table to insert into, then list the columns to insert into, and then list the values to insert.</span></span> <span data-ttu-id="6f1a8-171">（如前所述，SQL 並不區分大小寫，但有些人會將關鍵字變成大寫，讓您更輕鬆地讀取命令）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-171">(As noted before, SQL is not case sensitive but some people capitalize the keywords to make it easier to read the command.)</span></span>

<span data-ttu-id="6f1a8-172">您要插入的資料行已列在命令中，`(Title, Genre, Year)`。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-172">The columns that you're inserting into are already listed in the command — `(Title, Genre, Year)`.</span></span> <span data-ttu-id="6f1a8-173">有趣的部分是如何從文字方塊中取得值到命令的 `VALUES` 部分。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-173">The interesting part is how you get the values from the text boxes into the `VALUES` part of the command.</span></span> <span data-ttu-id="6f1a8-174">您看不到實際的值，而是看到 `@0`、`@1`和 `@2`，這是課程預留位置。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-174">Instead of actual values, you see `@0`, `@1`, and `@2`, which are of course placeholders.</span></span> <span data-ttu-id="6f1a8-175">當您執行命令時（在 `db.Execute` 行），會傳遞您從文字方塊中所獲得的值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-175">When you run the command (on the `db.Execute` line), you pass the values that you got from the text boxes.</span></span>

<span data-ttu-id="6f1a8-176">**重要！**</span><span class="sxs-lookup"><span data-stu-id="6f1a8-176">**Important!**</span></span> <span data-ttu-id="6f1a8-177">請記住，您應該在 SQL 語句中包含使用者在線上輸入的資料的唯一方式，就是使用預留位置，如這裡所見（`VALUES(@0, @1, @2)`）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-177">Remember that the only way you should ever include data entered online by a user in a SQL statement is to use placeholders, as you see here (`VALUES(@0, @1, @2)`).</span></span> <span data-ttu-id="6f1a8-178">如果您將使用者輸入串連到 SQL 語句中，您會將自己開啟至 SQL 插入式攻擊，如[ASP.NET Web Pages 的表單基本概念](https://go.microsoft.com/fwlink/?LinkId=251581)（上一個教學課程）中所述。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-178">If you concatenate user input into a SQL statement, you open yourself to a SQL injection attack, as explained in [Form Basics in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251581) (the previous tutorial).</span></span>

<span data-ttu-id="6f1a8-179">仍然在 `if` 區塊內，在 `db.Execute` 行後面新增下列程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-179">Still inside the `if` block, add the following line after the `db.Execute` line:</span></span>

[!code-css[Main](entering-data/samples/sample4.css)]

<span data-ttu-id="6f1a8-180">將新電影插入資料庫之後，這行程式碼會將您（重新導向）至*電影*頁面，讓您可以看到剛才輸入的電影。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-180">After the new movie has been inserted into the database, this line jumps you (redirects) to the *Movies* page so you can see the movie you just entered.</span></span> <span data-ttu-id="6f1a8-181">`~` 運算子表示「網站的根目錄」。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-181">The `~` operator means "root of the website."</span></span> <span data-ttu-id="6f1a8-182">（`~` 運算子僅適用于 ASP.NET 網頁，而非 HTML 一般）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-182">(The `~` operator works only in ASP.NET pages, not in HTML generally.)</span></span>

<span data-ttu-id="6f1a8-183">完整的程式碼區塊如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-183">The complete code block looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample5.cshtml)]

## <a name="testing-the-insert-command-so-far"></a><span data-ttu-id="6f1a8-184">測試插入命令（到目前為止）</span><span class="sxs-lookup"><span data-stu-id="6f1a8-184">Testing the Insert Command (So Far)</span></span>

<span data-ttu-id="6f1a8-185">您還沒這麼做，但現在是測試的好時機。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-185">You're not done yet, but now is a good time to test.</span></span>

<span data-ttu-id="6f1a8-186">在 WebMatrix 中檔案的樹狀檢視中，以滑鼠右鍵按一下 [ *AddMovie* ] 頁面，然後按一下 [**在瀏覽器中啟動**]。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-186">In the tree view of files in WebMatrix, right-click the *AddMovie.cshtml* page and then click **Launch in browser**.</span></span>

![瀏覽器中的 [新增電影] 頁面](entering-data/_static/image2.png)

<span data-ttu-id="6f1a8-188">（如果您最終會在瀏覽器中使用不同的頁面，請確定 URL 是 `http://localhost:nnnnn/AddMovie`），其中*nnnnn*是您所使用的埠號碼）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-188">(If you end up with a different page in the browser, make sure that the URL is `http://localhost:nnnnn/AddMovie`), where *nnnnn* is the port number that you're using.)</span></span>

<span data-ttu-id="6f1a8-189">您是否收到錯誤頁面？</span><span class="sxs-lookup"><span data-stu-id="6f1a8-189">Did you get an error page?</span></span> <span data-ttu-id="6f1a8-190">若是如此，請仔細閱讀，並確定程式碼看起來完全符合先前所列的內容。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-190">If so, read it carefully and make sure that the code looks exactly what was listed earlier.</span></span>

<span data-ttu-id="6f1a8-191">以 &mdash; 的形式輸入電影，例如，使用 "公民 Kane"、"戲劇" 和 "1941"。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-191">Enter a movie in the form &mdash; for example, use "Citizen Kane", "Drama", and "1941".</span></span> <span data-ttu-id="6f1a8-192">（或任何）。然後按一下 [**新增電影**]。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-192">(Or whatever.) Then click **Add Movie**.</span></span>

<span data-ttu-id="6f1a8-193">如果一切順利，您會被重新導向至 [*電影*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-193">If all goes well, you're redirected to the *Movies* page.</span></span> <span data-ttu-id="6f1a8-194">請確定您的新電影已列出。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-194">Make sure that your new movie is listed.</span></span>

![顯示新增電影的電影頁面](entering-data/_static/image3.png)

## <a name="validating-user-input"></a><span data-ttu-id="6f1a8-196">驗證使用者輸入</span><span class="sxs-lookup"><span data-stu-id="6f1a8-196">Validating User Input</span></span>

<span data-ttu-id="6f1a8-197">返回 [ *AddMovie* ] 頁面，或重新執行。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-197">Go back to the *AddMovie* page, or run it again.</span></span> <span data-ttu-id="6f1a8-198">輸入另一個電影，但這次請輸入 &mdash; 的標題，例如，輸入 "Singin' in the Rain"。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-198">Enter another movie, but this time, enter only the title &mdash; for example, enter "Singin' in the Rain".</span></span> <span data-ttu-id="6f1a8-199">然後按一下 [**新增電影**]。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-199">Then click **Add Movie**.</span></span>

<span data-ttu-id="6f1a8-200">您會重新導向至 [*電影*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-200">You're redirected to the *Movies* page again.</span></span> <span data-ttu-id="6f1a8-201">您可以找到新電影，但它不完整。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-201">You can find the new movie, but it's incomplete.</span></span>

![顯示遺漏一些值的新電影的電影頁面](entering-data/_static/image4.png)

<span data-ttu-id="6f1a8-203">當您建立*電影*資料表時，您會明確指出沒有任何欄位可以是 null。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-203">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="6f1a8-204">在這裡，您會有新電影的輸入表單，而您要將欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-204">Here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="6f1a8-205">這就是錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-205">That's an error.</span></span>

<span data-ttu-id="6f1a8-206">在此情況下，資料庫實際上不會引發（或*擲*回）錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-206">In this case, the database didn't actually raise (or *throw*) an error.</span></span> <span data-ttu-id="6f1a8-207">您未提供內容類型或年份，因此*AddMovie*頁面中的程式碼會將這些值視為所謂的*空字串*。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-207">You didn't supply a genre or year, so the code in the *AddMovie* page treated those values as so-called *empty strings*.</span></span> <span data-ttu-id="6f1a8-208">當 SQL `Insert Into` 命令執行時，[內容類型] 和 [年份] 欄位在其中沒有有用的資料，但它們不是 null。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-208">When the SQL `Insert Into` command ran, the genre and year fields didn't have useful data in them, but they weren't null.</span></span>

<span data-ttu-id="6f1a8-209">很明顯地，您不想讓使用者在資料庫中輸入半空白的電影資訊。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-209">Obviously, you don't want to let users enter half-empty movie information into the database.</span></span> <span data-ttu-id="6f1a8-210">解決方案是驗證使用者的輸入。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-210">The solution is to validate the user's input.</span></span> <span data-ttu-id="6f1a8-211">一開始，驗證只會確保使用者已輸入所有欄位的值（亦即，它們都不會包含空字串）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-211">Initially, the validation will simply make sure that the user has entered a value for all of the fields (that is, that none of them contains an empty string).</span></span>

> [!TIP]
> 
> <span data-ttu-id="6f1a8-212">**Null 和空字串**</span><span class="sxs-lookup"><span data-stu-id="6f1a8-212">**Null and Empty Strings**</span></span>
> 
> <span data-ttu-id="6f1a8-213">在程式設計中，「沒有值」的不同概念會有所區別。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-213">In programming, there's a distinction between different notions of "no value."</span></span> <span data-ttu-id="6f1a8-214">一般來說，如果從未以任何方式設定或初始化值，就會是*null* 。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-214">In general, a value is *null* if it has never been set or initialized in any way.</span></span> <span data-ttu-id="6f1a8-215">相反地，預期字元資料（字串）的變數可以設定為*空字串*。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-215">In contrast, a variable that expects character data (strings) can be set to an *empty string*.</span></span> <span data-ttu-id="6f1a8-216">在此情況下，此值不是 null;它只會明確設定為長度為零的字元字串。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-216">In that case, the value is not null; it's just been explicitly set to a string of characters whose length is zero.</span></span> <span data-ttu-id="6f1a8-217">這兩個語句會顯示差異：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-217">These two statements show the difference:</span></span>
> 
> [!code-csharp[Main](entering-data/samples/sample6.cs)]
> 
> <span data-ttu-id="6f1a8-218">這有點複雜，但重點在於，`null` 代表一種不確定的狀態。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-218">It's a little more complicated than that, but the important point is that `null` represents a sort of undetermined state.</span></span>
> 
> <span data-ttu-id="6f1a8-219">接下來，請務必瞭解值為 null 的確切時間，以及它是否只是空字串。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-219">Now and then it's important to understand exactly when a value is null and when it's just an empty string.</span></span> <span data-ttu-id="6f1a8-220">在 [ *AddMovie* ] 頁面的程式碼中，您可以使用 `Request.Form["title"]` 等來取得文字方塊的值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-220">In the code for the *AddMovie* page, you get the values of the text boxes by using `Request.Form["title"]` and so on.</span></span> <span data-ttu-id="6f1a8-221">當頁面第一次執行時（在您按一下按鈕之前），`Request.Form["title"]` 的值為 null。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-221">When the page first runs (before you click the button), the value of `Request.Form["title"]` is null.</span></span> <span data-ttu-id="6f1a8-222">但是當您提交表單時，`Request.Form["title"]` 會取得 `title` 文字方塊的值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-222">But when you submit the form, `Request.Form["title"]` gets the value of the `title` text box.</span></span> <span data-ttu-id="6f1a8-223">這並不明顯，但空白的文字方塊不是 null;其中只有一個空字串。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-223">It's not obvious, but an empty text box is not null; it just has an empty string in it.</span></span> <span data-ttu-id="6f1a8-224">因此，當程式碼執行以回應按下按鈕時，`Request.Form["title"]` 中會有一個空字串。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-224">So when the code runs in response to the button click, `Request.Form["title"]` has an empty string in it.</span></span>
> 
> <span data-ttu-id="6f1a8-225">這項區別為何重要？</span><span class="sxs-lookup"><span data-stu-id="6f1a8-225">Why is this distinction important?</span></span> <span data-ttu-id="6f1a8-226">當您建立*電影*資料表時，您會明確指出沒有任何欄位可以是 null。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-226">When you created the *Movies* table, you explicitly said that none of the fields could be null.</span></span> <span data-ttu-id="6f1a8-227">但在這裡，您會有新電影的輸入表單，而您會將欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-227">But here you have an entry form for new movies, and you're leaving fields blank.</span></span> <span data-ttu-id="6f1a8-228">當您嘗試儲存沒有內容類型或年份值的新電影時，您會合理地預期資料庫抱怨。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-228">You would reasonably expect the database to complain when you tried to save new movies that didn't have values for genre or year.</span></span> <span data-ttu-id="6f1a8-229">這就是 &mdash; 的重點，即使您將這些文字方塊保留空白，值也不會是 null;它們是空字串。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-229">But that's the point &mdash; even if you leave those text boxes blank, the values aren't null; they're empty strings.</span></span> <span data-ttu-id="6f1a8-230">因此，您可以將新電影儲存到資料庫中，這些資料行都是空的 &mdash; 而不是 null！</span><span class="sxs-lookup"><span data-stu-id="6f1a8-230">As a result, you're able to save new movies to the database with these columns empty &mdash; but not null!</span></span> <span data-ttu-id="6f1a8-231">&mdash; 值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-231">&mdash; values.</span></span> <span data-ttu-id="6f1a8-232">因此，您必須確定使用者不會提交空字串，您可以藉由驗證使用者的輸入來進行。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-232">Therefore, you have to make sure that users don't submit an empty string, which you can do by validating the user's input.</span></span>

### <a name="the-validation-helper"></a><span data-ttu-id="6f1a8-233">驗證協助程式</span><span class="sxs-lookup"><span data-stu-id="6f1a8-233">The Validation Helper</span></span>

<span data-ttu-id="6f1a8-234">ASP.NET Web Pages 包括協助程式 &mdash; `Validation` helper &mdash;，您可以用來確保使用者輸入符合您需求的資料。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-234">ASP.NET Web Pages includes a helper &mdash; the `Validation` helper &mdash; that you can use to make sure that users enter data that meets your requirements.</span></span> <span data-ttu-id="6f1a8-235">`Validation` helper 是內建 ASP.NET Web Pages 的協助程式之一，因此您不需要使用 NuGet 將它安裝為套件，這是您在先前的教學課程中安裝 Gravatar helper 的方式。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-235">The `Validation` helper is one of the helpers that's built in to ASP.NET Web Pages, so you don't have to install it as a package by using NuGet, the way you installed the Gravatar helper in an earlier tutorial.</span></span>

<span data-ttu-id="6f1a8-236">若要驗證使用者的輸入，您將執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-236">To validate the user's input, you'll do the following:</span></span>

- <span data-ttu-id="6f1a8-237">使用 [程式碼]，指定您想要在頁面上的文字方塊中要求值。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-237">Use code to specify that you want to require values in the text boxes on the page.</span></span>
- <span data-ttu-id="6f1a8-238">將測試放入程式碼中，只有當所有專案都正確驗證時，才會將電影資訊新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-238">Put a test into the code so that the movie information is added to the database only if everything validates properly.</span></span>
- <span data-ttu-id="6f1a8-239">將程式碼新增至標記，以顯示錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-239">Add code into the markup to display error messages.</span></span>

<span data-ttu-id="6f1a8-240">在 [ *AddMovie* ] 頁面的程式碼區塊中，于變數宣告前面的頂端，新增下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-240">In the code block in the *AddMovie* page, right up at the top before the variable declarations, add the following code:</span></span>

[!code-csharp[Main](entering-data/samples/sample7.cs)]

<span data-ttu-id="6f1a8-241">您會針對您想要要求輸入的每個欄位（`<input>` 元素）呼叫 `Validation.RequireField` 一次。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-241">You call `Validation.RequireField` once for each field (`<input>` element) where you want to require an entry.</span></span> <span data-ttu-id="6f1a8-242">您也可以為每個呼叫新增自訂的錯誤訊息，就像您在這裡看到的一樣。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-242">You can also add a custom error message for each call, like you see here.</span></span> <span data-ttu-id="6f1a8-243">（我們只會改變訊息，告訴您可以把任何東西放在那裡）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-243">(We varied the messages just to show that you can put anything you like there.)</span></span>

<span data-ttu-id="6f1a8-244">如果發生問題，您會想要防止新電影資訊插入資料庫中。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-244">If there's a problem, you want to prevent the new movie information from being inserted into the database.</span></span> <span data-ttu-id="6f1a8-245">在 `if(IsPost)` 區塊中，使用 `&&` （邏輯 AND）來新增另一個測試 `Validation.IsValid()`的條件。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-245">In the `if(IsPost)` block, use `&&` (logical AND) to add another condition that tests `Validation.IsValid()`.</span></span> <span data-ttu-id="6f1a8-246">當您完成時，整個 `if(IsPost)` 區塊看起來就像下面這段程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-246">When you're done, the whole `if(IsPost)` block looks like this code:</span></span>

[!code-csharp[Main](entering-data/samples/sample8.cs)]

<span data-ttu-id="6f1a8-247">如果您使用 `Validation` helper 註冊的任何欄位發生驗證錯誤，則 `Validation.IsValid` 方法會傳回 false。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-247">If there's a validation error with any of the fields that you registered by using the `Validation` helper, the `Validation.IsValid` method returns false.</span></span> <span data-ttu-id="6f1a8-248">在此情況下，將不會執行該區塊中的任何程式碼，因此不會將不正確電影專案插入資料庫中。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-248">And in that case, none of the code in that block will run, so no invalid movie entries will be inserted into the database.</span></span> <span data-ttu-id="6f1a8-249">當然，您也不會被重新導向到*電影*頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-249">And of course you're not redirected to the *Movies* page.</span></span>

<span data-ttu-id="6f1a8-250">完整的程式碼區塊，包括驗證程式代碼，現在看起來像這個範例：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-250">The complete code block, including the validation code, now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample9.cshtml?highlight=10)]

## <a name="displaying-validation-errors"></a><span data-ttu-id="6f1a8-251">顯示驗證錯誤</span><span class="sxs-lookup"><span data-stu-id="6f1a8-251">Displaying Validation Errors</span></span>

<span data-ttu-id="6f1a8-252">最後一個步驟是顯示任何錯誤訊息。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-252">The last step is to display any error messages.</span></span> <span data-ttu-id="6f1a8-253">您可以針對每個驗證錯誤顯示個別的訊息，也可以顯示摘要或兩者。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-253">You can display individual messages for each validation error, or you can display a summary, or both.</span></span> <span data-ttu-id="6f1a8-254">在本教學課程中，您將會執行這兩項作業，讓您可以查看其運作方式。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-254">For this tutorial, you'll do both so that you can see how it works.</span></span>

<span data-ttu-id="6f1a8-255">在您要驗證的每個 `<input>` 元素旁，呼叫 `Html.ValidationMessage` 方法，並將您要驗證的 `<input>` 元素名稱傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-255">Next to each `<input>` element that you're validating, call the `Html.ValidationMessage` method and pass it the name of the `<input>` element you're validating.</span></span> <span data-ttu-id="6f1a8-256">您可以將 `Html.ValidationMessage` 方法放在您想要出現錯誤訊息的位置。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-256">You put the `Html.ValidationMessage` method right where you want the error message to appear.</span></span> <span data-ttu-id="6f1a8-257">當頁面執行時，`Html.ValidationMessage` 方法會呈現驗證錯誤所在的 `<span>` 元素。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-257">When the page runs, the `Html.ValidationMessage` method renders a `<span>` element where the validation error will go.</span></span> <span data-ttu-id="6f1a8-258">（如果沒有錯誤，則會轉譯 `<span>` 專案，但其中沒有任何文字）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-258">(If there's no error, the `<span>` element is rendered, but there's no text in it.)</span></span>

<span data-ttu-id="6f1a8-259">變更頁面中的標記，使其在頁面上包含三個 `<input>` 元素的 `Html.ValidationMessage` 方法，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-259">Change the markup in the page so that it includes an `Html.ValidationMessage` method for each of the three `<input>` elements on the page, like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample10.cshtml?highlight=3,8,13)]

<span data-ttu-id="6f1a8-260">若要查看摘要的運作方式，也請在頁面上的 `<h1>Add a Movie</h1>` 元素後面，加入下列標記和程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-260">To see how the summary works, also add the following markup and code right after the `<h1>Add a Movie</h1>` element on the page:</span></span>

[!code-cshtml[Main](entering-data/samples/sample11.cshtml)]

<span data-ttu-id="6f1a8-261">根據預設，`Html.ValidationSummary` 方法會顯示清單中的所有驗證訊息（位於 `<div>` 元素內的 `<ul>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-261">By default, the `Html.ValidationSummary` method displays all the validation messages in a list (a `<ul>` element that's inside a `<div>` element).</span></span> <span data-ttu-id="6f1a8-262">如同 `Html.ValidationMessage` 方法，一律會轉譯驗證摘要的標記;如果沒有任何錯誤，則不會轉譯任何清單專案。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-262">As with the `Html.ValidationMessage` method, the markup for the validation summary is always rendered; if there are no errors, no list items are rendered.</span></span>

<span data-ttu-id="6f1a8-263">摘要可以是顯示驗證訊息的替代方式，而不是使用 `Html.ValidationMessage` 方法來顯示每個欄位特定的錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-263">The summary can be an alternative way to display validation messages instead of by using the `Html.ValidationMessage` method to display each field-specific error.</span></span> <span data-ttu-id="6f1a8-264">或者，您可以同時使用摘要和詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-264">Or you can use both a summary and the details.</span></span> <span data-ttu-id="6f1a8-265">或者，您可以使用 `Html.ValidationSummary` 方法來顯示一般錯誤，然後使用個別的 `Html.ValidationMessage` 呼叫來顯示詳細資料。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-265">Or you can use the `Html.ValidationSummary` method to display a generic error and then use individual `Html.ValidationMessage` calls to display details.</span></span>

<span data-ttu-id="6f1a8-266">[完成] 頁面現在會如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-266">The complete page now looks like this example:</span></span>

[!code-cshtml[Main](entering-data/samples/sample12.cshtml)]

<span data-ttu-id="6f1a8-267">就這麼容易！</span><span class="sxs-lookup"><span data-stu-id="6f1a8-267">That's it.</span></span> <span data-ttu-id="6f1a8-268">您現在可以藉由新增電影來測試頁面，但保留一或多個欄位。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-268">You can now test the page by adding a movie but leaving out one or more of the fields.</span></span> <span data-ttu-id="6f1a8-269">當您這樣做時，您會看到下列錯誤顯示：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-269">When you do, you see the following error display:</span></span>

![新增顯示驗證錯誤訊息的電影頁面](entering-data/_static/image5.png)

## <a name="styling-the-validation-error-messages"></a><span data-ttu-id="6f1a8-271">設定驗證錯誤訊息的樣式</span><span class="sxs-lookup"><span data-stu-id="6f1a8-271">Styling the Validation Error Messages</span></span>

<span data-ttu-id="6f1a8-272">您可以看到有錯誤訊息，但它們並沒有太大的差異。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-272">You can see that there are error messages, but they don't really stand out very well.</span></span> <span data-ttu-id="6f1a8-273">不過，有一種簡單的方式可將錯誤訊息樣式。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-273">There's an easy way to style the error messages, though.</span></span>

<span data-ttu-id="6f1a8-274">若要將 `Html.ValidationMessage`顯示的個別錯誤訊息樣式，請建立名為 `field-validation-error`的 CSS 樣式類別。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-274">To style the individual error messages that are displayed by `Html.ValidationMessage`, create a CSS style class named `field-validation-error`.</span></span> <span data-ttu-id="6f1a8-275">若要定義驗證摘要的尋找，請建立名為 `validation-summary-errors`的 CSS 樣式類別。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-275">To define the look for the validation summary, create a CSS style class named `validation-summary-errors`.</span></span>

<span data-ttu-id="6f1a8-276">若要查看這項技術的運作方式，請在頁面的 [`<head>`] 區段內加入 `<style>` 元素。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-276">To see how this technique works, add a `<style>` element inside the `<head>` section of the page.</span></span> <span data-ttu-id="6f1a8-277">然後定義名為 `field-validation-error` 的樣式類別，以及包含下列規則的 `validation-summary-errors`：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-277">Then define style classes named `field-validation-error` and `validation-summary-errors` that contain the following rules:</span></span>

[!code-cshtml[Main](entering-data/samples/sample13.cshtml?highlight=4-17)]

<span data-ttu-id="6f1a8-278">一般來說，您可能會將樣式資訊放在個別的 *.css*檔案中，但為了簡單起見，您可以將它們放在頁面中，以供您立即使用。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-278">Normally you'd probably put style information into a separate *.css* file, but for simplicity you can put them in the page for now.</span></span> <span data-ttu-id="6f1a8-279">（稍後在本教學課程中，您會將 CSS 規則移至不同的 *.css*檔案）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-279">(Later in this tutorial set, you'll move the CSS rules to a separate *.css* file.)</span></span>

<span data-ttu-id="6f1a8-280">如果發生驗證錯誤，`Html.ValidationMessage` 方法會呈現包含 `class="field-validation-error"`的 `<span>` 元素。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-280">If there's a validation error, the `Html.ValidationMessage` method renders a `<span>` element that includes `class="field-validation-error"`.</span></span> <span data-ttu-id="6f1a8-281">藉由加入該類別的樣式定義，您可以設定訊息的外觀。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-281">By adding a style definition for that class, you can configure what the message looks like.</span></span> <span data-ttu-id="6f1a8-282">如果發生錯誤，`ValidationSummary` 方法同樣會以動態方式呈現屬性 `class="validation-summary-errors"`。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-282">If there are errors, the `ValidationSummary` method likewise dynamically renders the attribute `class="validation-summary-errors"`.</span></span>

<span data-ttu-id="6f1a8-283">再次執行頁面，並故意省略幾個欄位。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-283">Run the page again and deliberately leave out a couple of the fields.</span></span> <span data-ttu-id="6f1a8-284">這些錯誤現在更明顯。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-284">The errors are now more noticeable.</span></span> <span data-ttu-id="6f1a8-285">（事實上，它們是過渡濫用的，但這只是為了說明您可以執行的動作）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-285">(In fact, they're overdone, but that's just to show what you can do.)</span></span>

![[新增電影] 頁面，其中顯示已樣式的驗證錯誤](entering-data/_static/image6.png)

## <a name="adding-a-link-to-the-movies-page"></a><span data-ttu-id="6f1a8-287">新增電影頁面的連結</span><span class="sxs-lookup"><span data-stu-id="6f1a8-287">Adding a Link to the Movies Page</span></span>

<span data-ttu-id="6f1a8-288">最後一個步驟是讓從原始電影清單中取得*AddMovie*頁面變得更方便。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-288">One final step is to make it convenient to get to the *AddMovie* page from the original movie listing.</span></span>

<span data-ttu-id="6f1a8-289">再次開啟 [*電影*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-289">Open the *Movies* page again.</span></span> <span data-ttu-id="6f1a8-290">在 `WebGrid` helper 後面的關閉 `</div>` 標記之後，新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-290">After the closing `</div>` tag that follows the `WebGrid` helper, add the following markup:</span></span>

[!code-cshtml[Main](entering-data/samples/sample14.cshtml)]

<span data-ttu-id="6f1a8-291">如先前所見，ASP.NET 會將 `~` 運算子解讀為網站的根目錄。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-291">As you saw before, ASP.NET interprets the `~` operator as the root of the website.</span></span> <span data-ttu-id="6f1a8-292">您不需要使用 `~` 運算子;您可以使用標記 `<a href="./AddMovie">Add a movie</a>` 或其他方式來定義 HTML 瞭解的路徑。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-292">You don't have to use the `~` operator; you could use the markup `<a href="./AddMovie">Add a movie</a>` or some other way to define the path that HTML understands.</span></span> <span data-ttu-id="6f1a8-293">但是，當您建立 Razor 頁面的連結時，`~` 運算子是不錯的一般方法，因為它可讓網站更具彈性，如果您將目前頁面移至子資料夾，此連結仍然會前往 [ *AddMovie* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-293">But the `~` operator is a good general approach when you create links for Razor pages, because it makes the site more flexible — if you move the current page to a subfolder, the link will still go to the *AddMovie* page.</span></span> <span data-ttu-id="6f1a8-294">（請記住，`~` 運算子僅適用于*cshtml*頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-294">(Remember that the `~` operator only works in *.cshtml* pages.</span></span> <span data-ttu-id="6f1a8-295">ASP.NET 瞭解它，但它並不是標準的 HTML）。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-295">ASP.NET understands it, but it's not standard HTML.)</span></span>

<span data-ttu-id="6f1a8-296">當您完成時，請執行 [*電影*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-296">When you're done, run the *Movies* page.</span></span> <span data-ttu-id="6f1a8-297">看起來會像這個頁面：</span><span class="sxs-lookup"><span data-stu-id="6f1a8-297">It will look like this page:</span></span>

![包含連結至 [新增電影] 頁面的電影頁面](entering-data/_static/image7.png)

<span data-ttu-id="6f1a8-299">按一下 [**新增電影**] 連結，以確定它會移至 [ *AddMovie* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-299">Click the **Add a movie** link to make sure that it goes to the *AddMovie* page.</span></span>

## <a name="coming-up-next"></a><span data-ttu-id="6f1a8-300">下一步</span><span class="sxs-lookup"><span data-stu-id="6f1a8-300">Coming Up Next</span></span>

<span data-ttu-id="6f1a8-301">在下一個教學課程中，您將學習如何讓使用者編輯已在資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-301">In the next tutorial, you'll learn how to let users edit data that's already in the database.</span></span>

## <a name="complete-listing-for-addmovie-page"></a><span data-ttu-id="6f1a8-302">AddMovie 頁面的完整清單</span><span class="sxs-lookup"><span data-stu-id="6f1a8-302">Complete Listing for AddMovie Page</span></span>

[!code-cshtml[Main](entering-data/samples/sample15.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="6f1a8-303">其他資源</span><span class="sxs-lookup"><span data-stu-id="6f1a8-303">Additional Resources</span></span>

- [<span data-ttu-id="6f1a8-304">使用 Razor 語法 ASP.NET Web 程式設計的簡介</span><span class="sxs-lookup"><span data-stu-id="6f1a8-304">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)
- <span data-ttu-id="6f1a8-305">W3Schools 網站上的[SQL INSERT INTO 語句](http://www.w3schools.com/sql/sql_insert.asp)</span><span class="sxs-lookup"><span data-stu-id="6f1a8-305">[SQL INSERT INTO Statement](http://www.w3schools.com/sql/sql_insert.asp) on the W3Schools site</span></span>
- <span data-ttu-id="6f1a8-306">[驗證 ASP.NET Web Pages 網站中的使用者輸入](https://go.microsoft.com/fwlink/?LinkId=253002)。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-306">[Validating User Input in ASP.NET Web Pages Sites](https://go.microsoft.com/fwlink/?LinkId=253002).</span></span> <span data-ttu-id="6f1a8-307">有關使用 `Validation` helper 的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="6f1a8-307">More information about working with the `Validation` helper.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="6f1a8-308">[上一頁](form-basics.md)
> [下一頁](updating-data.md)</span><span class="sxs-lookup"><span data-stu-id="6f1a8-308">[Previous](form-basics.md)
[Next](updating-data.md)</span></span>
