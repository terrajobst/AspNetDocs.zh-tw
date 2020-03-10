---
uid: web-pages/overview/testing-and-debugging/introduction-to-debugging
title: 調試 ASP.NET Web Pages （Razor）網站簡介 |Microsoft Docs
author: Rick-Anderson
description: 「偵錯工具」是在您的字碼頁中尋找和修正錯誤的過程。 本章將說明一些您可以用來進行 debug 和分析的工具和技巧 。
ms.author: riande
ms.date: 02/20/2014
ms.assetid: 68de4326-7611-4b9b-b5f6-79b7adc3069f
msc.legacyurl: /web-pages/overview/testing-and-debugging/introduction-to-debugging
msc.type: authoredcontent
ms.openlocfilehash: ae7d871e56326610c043dc20fe6e0919e1b4ac89
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78624366"
---
# <a name="introduction-to-debugging-aspnet-web-pages-razor-sites"></a><span data-ttu-id="eeedb-104">調試 ASP.NET Web Pages （Razor）網站簡介</span><span class="sxs-lookup"><span data-stu-id="eeedb-104">Introduction to Debugging ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="eeedb-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="eeedb-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="eeedb-106">本文說明在 ASP.NET Web Pages （Razor）網站中，用來進行頁面偵錯工具的各種方式。</span><span class="sxs-lookup"><span data-stu-id="eeedb-106">This article explains various ways to debug pages in an ASP.NET Web Pages (Razor) website.</span></span> <span data-ttu-id="eeedb-107">「偵錯工具」是在您的字碼頁中尋找和修正錯誤的過程。</span><span class="sxs-lookup"><span data-stu-id="eeedb-107">Debugging is the process of finding and fixing errors in your code pages.</span></span>
>
> <span data-ttu-id="eeedb-108">**您將瞭解的內容：**</span><span class="sxs-lookup"><span data-stu-id="eeedb-108">**What you'll learn:**</span></span>
>
> - <span data-ttu-id="eeedb-109">如何顯示有助於分析和偵錯工具頁面的資訊。</span><span class="sxs-lookup"><span data-stu-id="eeedb-109">How to display information that helps analyze and debug pages.</span></span>
> - <span data-ttu-id="eeedb-110">如何在 Visual Studio 中使用調試工具。</span><span class="sxs-lookup"><span data-stu-id="eeedb-110">How to use debugging tools in Visual Studio.</span></span>
>
>
> <span data-ttu-id="eeedb-111">以下是文章中引進的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="eeedb-111">These are the ASP.NET features introduced in the article:</span></span>
>
> - <span data-ttu-id="eeedb-112">`ServerInfo` helper。</span><span class="sxs-lookup"><span data-stu-id="eeedb-112">The `ServerInfo` helper.</span></span>
> - <span data-ttu-id="eeedb-113">`ObjectInfo` helper。</span><span class="sxs-lookup"><span data-stu-id="eeedb-113">`ObjectInfo` helper.</span></span>
>
>
> ## <a name="software-versions"></a><span data-ttu-id="eeedb-114">軟體版本</span><span class="sxs-lookup"><span data-stu-id="eeedb-114">Software versions</span></span>
>
>
> - <span data-ttu-id="eeedb-115">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="eeedb-115">ASP.NET Web Pages (Razor) 3</span></span>
> - <span data-ttu-id="eeedb-116">Visual Studio 2013</span><span class="sxs-lookup"><span data-stu-id="eeedb-116">Visual Studio 2013</span></span>
>
>
> <span data-ttu-id="eeedb-117">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="eeedb-117">This tutorial also works with ASP.NET Web Pages 2.</span></span> <span data-ttu-id="eeedb-118">您可以使用 WebMatrix 3，但不支援整合式偵錯工具。</span><span class="sxs-lookup"><span data-stu-id="eeedb-118">You can use WebMatrix 3 but the integrated debugger is not supported.</span></span>

<span data-ttu-id="eeedb-119">在您的程式碼中疑難排解錯誤和問題的重要層面，就是在一開始就予以避免。</span><span class="sxs-lookup"><span data-stu-id="eeedb-119">An important aspect of troubleshooting errors and problems in your code is to avoid them in the first place.</span></span> <span data-ttu-id="eeedb-120">若要這麼做，您可以將可能導致錯誤的程式碼區段放入 `try/catch` 區塊中。</span><span class="sxs-lookup"><span data-stu-id="eeedb-120">You can do that by putting sections of your code that are likely to cause errors into `try/catch` blocks.</span></span> <span data-ttu-id="eeedb-121">如需詳細資訊，請參閱[使用 Razor 語法進行 ASP.NET Web 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=202890)中的處理錯誤一節。</span><span class="sxs-lookup"><span data-stu-id="eeedb-121">For more information, see the section on handling errors in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890).</span></span>

<span data-ttu-id="eeedb-122">`ServerInfo` 協助程式是一種診斷工具，可讓您大致瞭解裝載網頁的 web 伺服器環境的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="eeedb-122">The `ServerInfo` helper is a diagnostic tool that gives you an overview of information about the web server environment that hosts your page.</span></span> <span data-ttu-id="eeedb-123">它也會顯示當瀏覽器要求頁面時所傳送的 HTTP 要求資訊。</span><span class="sxs-lookup"><span data-stu-id="eeedb-123">It also shows you HTTP request information that's sent when a browser requests the page.</span></span> <span data-ttu-id="eeedb-124">[`ServerInfo` helper] 會顯示目前的使用者身分識別、提出要求的瀏覽器類型等等。</span><span class="sxs-lookup"><span data-stu-id="eeedb-124">The `ServerInfo` helper displays the current user identity, the type of browser that made the request, and so on.</span></span> <span data-ttu-id="eeedb-125">這類資訊可協助您針對常見的問題進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="eeedb-125">This kind of information can help you troubleshoot common issues.</span></span>

1. <span data-ttu-id="eeedb-126">建立名為*ServerInfo*的新網頁。</span><span class="sxs-lookup"><span data-stu-id="eeedb-126">Create a new web page named *ServerInfo.cshtml*.</span></span>
2. <span data-ttu-id="eeedb-127">在頁面結尾處，在結束 `</body>` 標記之前，新增 `@ServerInfo.GetHtml()`：</span><span class="sxs-lookup"><span data-stu-id="eeedb-127">At the end of the page, just before the closing `</body>` tag, add `@ServerInfo.GetHtml()`:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample1.cshtml)]

    <span data-ttu-id="eeedb-128">您可以在頁面中的任何位置加入 `ServerInfo` 程式碼。</span><span class="sxs-lookup"><span data-stu-id="eeedb-128">You can add the `ServerInfo` code anywhere in the page.</span></span> <span data-ttu-id="eeedb-129">但在結尾新增它，會將其輸出與其他頁面內容分開，讓您更容易閱讀。</span><span class="sxs-lookup"><span data-stu-id="eeedb-129">But adding it at the end will keep its output separate from your other page content, which makes it easier to read.</span></span>

    > [!NOTE]
    >
    > <span data-ttu-id="eeedb-130">**重要事項**將網頁移至實際伺服器之前，您應該先從網頁移除任何診斷程式代碼。</span><span class="sxs-lookup"><span data-stu-id="eeedb-130">**Important** You should remove any diagnostic code from your web pages before you move web pages to a production server.</span></span> <span data-ttu-id="eeedb-131">這適用于 `ServerInfo` 協助程式，以及本文中牽涉到將程式碼加入至頁面的其他診斷技術。</span><span class="sxs-lookup"><span data-stu-id="eeedb-131">This applies to the `ServerInfo` helper as well as the other diagnostic techniques in this article that involve adding code to a page.</span></span> <span data-ttu-id="eeedb-132">您不想讓網站訪客查看伺服器名稱、使用者名稱、伺服器上的路徑，以及類似的詳細資料等資訊，因為這類資訊可能適用于具有惡意意圖的人。</span><span class="sxs-lookup"><span data-stu-id="eeedb-132">You don't want your website visitors to see information about your server name, user names, paths on your server, and similar details, because this type of information might be useful to people with malicious intent.</span></span>
3. <span data-ttu-id="eeedb-133">儲存頁面，並在瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="eeedb-133">Save the page and run it in a browser.</span></span>

    ![調試-1](introduction-to-debugging/_static/image1.jpg)

    <span data-ttu-id="eeedb-135">`ServerInfo` helper 會在頁面中顯示四個資訊資料表：</span><span class="sxs-lookup"><span data-stu-id="eeedb-135">The `ServerInfo` helper displays four tables of information in the page:</span></span>

   - <span data-ttu-id="eeedb-136">伺服器設定。</span><span class="sxs-lookup"><span data-stu-id="eeedb-136">Server Configuration.</span></span> <span data-ttu-id="eeedb-137">本節提供主控網頁伺服器的相關資訊，包括電腦名稱稱、您正在執行的 ASP.NET 版本、功能變數名稱和伺服器時間。</span><span class="sxs-lookup"><span data-stu-id="eeedb-137">This section provides information about the hosting web server, including computer name, the version of ASP.NET you're running, the domain name, and server time.</span></span>
   - <span data-ttu-id="eeedb-138">ASP.NET 伺服器變數。</span><span class="sxs-lookup"><span data-stu-id="eeedb-138">ASP.NET Server Variables.</span></span> <span data-ttu-id="eeedb-139">本節提供許多 HTTP 通訊協定詳細資料（稱為 HTTP 變數）的詳細資料，以及每個網頁要求中的值。</span><span class="sxs-lookup"><span data-stu-id="eeedb-139">This section provides details about the many HTTP protocol details (called HTTP variables) and values that are part of each web page request.</span></span>
   - <span data-ttu-id="eeedb-140">HTTP 執行時間資訊。</span><span class="sxs-lookup"><span data-stu-id="eeedb-140">HTTP Runtime Information.</span></span> <span data-ttu-id="eeedb-141">本節提供有關您的網頁執行所在的 Microsoft .NET Framework 版本、路徑、有關快取的詳細資料等等的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="eeedb-141">This section provides details about that the version of the Microsoft .NET Framework that your web page is running under, the path, details about the cache, and so on.</span></span> <span data-ttu-id="eeedb-142">（如您在[使用 Razor 語法 ASP.NET Web 程式設計簡介](https://go.microsoft.com/fwlink/?LinkId=202890)中所學到的內容，使用 Razor 語法的 ASP.NET Web Pages 是以 Microsoft 的 ASP.NET Web 服務器技術為基礎，其本身是建置於廣泛的軟體發展程式庫，稱為 .NET Framework）。</span><span class="sxs-lookup"><span data-stu-id="eeedb-142">(As you learned in [Introduction to ASP.NET Web Programming Using the Razor Syntax](https://go.microsoft.com/fwlink/?LinkId=202890), ASP.NET Web Pages using the Razor syntax are built on Microsoft's ASP.NET web server technology, which is itself built on an extensive software development library called the .NET Framework.)</span></span>
   - <span data-ttu-id="eeedb-143">環境變數。</span><span class="sxs-lookup"><span data-stu-id="eeedb-143">Environment Variables.</span></span> <span data-ttu-id="eeedb-144">本節提供在 web 伺服器上的所有本機環境變數及其值的清單。</span><span class="sxs-lookup"><span data-stu-id="eeedb-144">This section provides a list of all the local environment variables and their values on the web server.</span></span>

     <span data-ttu-id="eeedb-145">所有伺服器和要求資訊的完整說明已超出本文的範圍，但您可以看到 `ServerInfo` helper 會傳回許多診斷資訊。</span><span class="sxs-lookup"><span data-stu-id="eeedb-145">A full description of all the server and request information is beyond the scope of this article, but you can see that the `ServerInfo` helper returns a lot of diagnostic information.</span></span> <span data-ttu-id="eeedb-146">如需 `ServerInfo` 所傳回之值的詳細資訊，請參閱 MSDN 網站上 Microsoft TechNet 網站上的已辨識的[環境變數](https://technet.microsoft.com/library/dd560744(WS.10).aspx)和[IIS 伺服器變數](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)。</span><span class="sxs-lookup"><span data-stu-id="eeedb-146">For more information about the values that `ServerInfo` returns, see [Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) on the Microsoft TechNet website and [IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) on the MSDN website.</span></span>

## <a name="embedding-output-expressions-to-display-page-values"></a><span data-ttu-id="eeedb-147">內嵌輸出運算式以顯示頁面值</span><span class="sxs-lookup"><span data-stu-id="eeedb-147">Embedding Output Expressions to Display Page Values</span></span>

<span data-ttu-id="eeedb-148">另一個查看程式碼發生狀況的方法，就是將輸出運算式內嵌在頁面中。</span><span class="sxs-lookup"><span data-stu-id="eeedb-148">Another way to see what's happening in your code is to embed output expressions in the page.</span></span> <span data-ttu-id="eeedb-149">如您所知，您可以藉由將 `@myVariable` 或 `@(subTotal * 12)` 之類的內容加入頁面中，直接輸出變數的值。</span><span class="sxs-lookup"><span data-stu-id="eeedb-149">As you know, you can directly output the value of a variable by adding something like `@myVariable` or `@(subTotal * 12)` to the page.</span></span> <span data-ttu-id="eeedb-150">若要進行偵錯工具，您可以將這些輸出運算式放在程式碼的策略性點上。</span><span class="sxs-lookup"><span data-stu-id="eeedb-150">For debugging, you can place these output expressions at strategic points in your code.</span></span> <span data-ttu-id="eeedb-151">這可讓您查看索引鍵變數的值，或頁面執行時的計算結果。</span><span class="sxs-lookup"><span data-stu-id="eeedb-151">This enables you to see the value of key variables or the result of calculations when your page runs.</span></span> <span data-ttu-id="eeedb-152">當您完成偵錯工具時，可以移除運算式或將它們批註起來。此程式說明使用內嵌運算式來協助 debug 頁面的一般方式。</span><span class="sxs-lookup"><span data-stu-id="eeedb-152">When you're done debugging, you can remove the expressions or comment them out. This procedure illustrates a typical way to use embedded expressions to help debug a page.</span></span>

1. <span data-ttu-id="eeedb-153">建立名為*OutputExpression*的新 WebMatrix 頁面。</span><span class="sxs-lookup"><span data-stu-id="eeedb-153">Create a new WebMatrix page that's named *OutputExpression.cshtml*.</span></span>
2. <span data-ttu-id="eeedb-154">將頁面內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="eeedb-154">Replace the page content with the following:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample2.html)]

    <span data-ttu-id="eeedb-155">此範例會使用 `switch` 語句來檢查 `weekday` 變數的值，然後根據該星期的哪一天顯示不同的輸出訊息。</span><span class="sxs-lookup"><span data-stu-id="eeedb-155">The example uses a `switch` statement to check the value of the `weekday` variable and then display a different output message depending on which day of the week it is.</span></span> <span data-ttu-id="eeedb-156">在此範例中，第一個程式碼區塊內的 `if` 區塊會將一天新增至目前的工作日值，任意變更一周中的那一天。</span><span class="sxs-lookup"><span data-stu-id="eeedb-156">In the example, the `if` block within the first code block arbitrarily changes the day of the week by adding one day to the current weekday value.</span></span> <span data-ttu-id="eeedb-157">這是為了說明而引進的錯誤。</span><span class="sxs-lookup"><span data-stu-id="eeedb-157">This is an error introduced for illustration purposes.</span></span>
3. <span data-ttu-id="eeedb-158">儲存頁面，並在瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="eeedb-158">Save the page and run it in a browser.</span></span>

    <span data-ttu-id="eeedb-159">此頁面會顯示一周中錯誤日的訊息。</span><span class="sxs-lookup"><span data-stu-id="eeedb-159">The page displays the message for the wrong day of the week.</span></span> <span data-ttu-id="eeedb-160">在一周當中的哪一天，您會在一天后看到訊息。</span><span class="sxs-lookup"><span data-stu-id="eeedb-160">Whatever day of the week it actually is, you'll see the message for one day later.</span></span> <span data-ttu-id="eeedb-161">雖然在此情況下，您知道訊息為何關閉（因為程式碼刻意設定了不正確的日期值），但事實上，通常很難知道程式碼中發生錯誤的位置。</span><span class="sxs-lookup"><span data-stu-id="eeedb-161">Although in this case you know why the message is off (because the code deliberately sets the incorrect day value), in reality it's often hard to know where things are going wrong in the code.</span></span> <span data-ttu-id="eeedb-162">若要進行 debug，您必須找出索引鍵物件和變數的值（例如 `weekday`）發生了什麼事。</span><span class="sxs-lookup"><span data-stu-id="eeedb-162">To debug, you need to find out what's happening to the value of key objects and variables such as `weekday`.</span></span>
4. <span data-ttu-id="eeedb-163">藉由插入 `@weekday` （如程式碼中的批註所指示的兩個位置所示）來新增輸出運算式。</span><span class="sxs-lookup"><span data-stu-id="eeedb-163">Add output expressions by inserting `@weekday` as shown in the two places indicated by comments in the code.</span></span> <span data-ttu-id="eeedb-164">這些輸出運算式會在程式碼執行中顯示該時間點的變數值。</span><span class="sxs-lookup"><span data-stu-id="eeedb-164">These output expressions will display the values of the variable at that point in the code execution.</span></span>

    [!code-csharp[Main](introduction-to-debugging/samples/sample3.cs?highlight=2-3,15-16)]
5. <span data-ttu-id="eeedb-165">在瀏覽器中儲存並執行頁面。</span><span class="sxs-lookup"><span data-stu-id="eeedb-165">Save and run the page in a browser.</span></span>

    <span data-ttu-id="eeedb-166">此頁面會先顯示一周中的一天，再加上一天的更新日期，然後從 `switch` 語句產生的訊息。</span><span class="sxs-lookup"><span data-stu-id="eeedb-166">The page displays the real day of the week first, then the updated day of the week that results from adding one day, and then the resulting message from the `switch` statement.</span></span> <span data-ttu-id="eeedb-167">這兩個變數運算式（`@weekday`）的輸出在天數之間沒有空格，因為您未將任何 HTML `<p>` 標記加入至輸出;運算式僅供測試之用。</span><span class="sxs-lookup"><span data-stu-id="eeedb-167">The output from the two variable expressions (`@weekday`) has no spaces between the days because you didn't add any HTML `<p>` tags to the output; the expressions are just for testing.</span></span>

    ![調試-2](introduction-to-debugging/_static/image2.jpg)

    <span data-ttu-id="eeedb-169">現在您可以看到錯誤所在的位置。</span><span class="sxs-lookup"><span data-stu-id="eeedb-169">Now you can see where the error is.</span></span> <span data-ttu-id="eeedb-170">當您第一次在程式碼中顯示 `weekday` 變數時，它會顯示正確的日期。</span><span class="sxs-lookup"><span data-stu-id="eeedb-170">When you first display the `weekday` variable in the code, it shows the correct day.</span></span> <span data-ttu-id="eeedb-171">當您第二次顯示時，在程式碼中 `if` 區塊之後，一天就會關閉。</span><span class="sxs-lookup"><span data-stu-id="eeedb-171">When you display it the second time, after the `if` block in the code, the day is off by one.</span></span> <span data-ttu-id="eeedb-172">所以您知道 weekday 變數的第一個和第二個外觀之間發生了什麼事。</span><span class="sxs-lookup"><span data-stu-id="eeedb-172">So you know that something has happened between the first and second appearance of the weekday variable.</span></span> <span data-ttu-id="eeedb-173">如果這是真正的錯誤，這種方法可協助您縮小造成問題之程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="eeedb-173">If this were a real bug, this kind of approach would help you narrow down the location of the code that's causing the problem.</span></span>
6. <span data-ttu-id="eeedb-174">藉由移除您新增的兩個輸出運算式，並移除變更星期幾的程式碼，修正頁面中的程式碼。</span><span class="sxs-lookup"><span data-stu-id="eeedb-174">Fix the code in the page by removing the two output expressions you added, and removing the code that changes the day of the week.</span></span> <span data-ttu-id="eeedb-175">其餘的完整程式碼區塊如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="eeedb-175">The remaining, complete block of code looks like the following example:</span></span>

    [!code-cshtml[Main](introduction-to-debugging/samples/sample4.cshtml)]
7. <span data-ttu-id="eeedb-176">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="eeedb-176">Run the page in a browser.</span></span> <span data-ttu-id="eeedb-177">此時，您會看到針對一周中的實際日期顯示正確的訊息。</span><span class="sxs-lookup"><span data-stu-id="eeedb-177">This time you see the correct message displayed for the actual day of the week.</span></span>

## <a name="using-the-objectinfo-helper-to-display-object-values"></a><span data-ttu-id="eeedb-178">使用 ObjectInfo Helper 顯示物件值</span><span class="sxs-lookup"><span data-stu-id="eeedb-178">Using the ObjectInfo Helper to Display Object Values</span></span>

<span data-ttu-id="eeedb-179">`ObjectInfo` helper 會顯示您傳遞給它的每個物件的類型和值。</span><span class="sxs-lookup"><span data-stu-id="eeedb-179">The `ObjectInfo` helper displays the type and the value of each object you pass to it.</span></span> <span data-ttu-id="eeedb-180">您可以使用它來查看程式碼中變數和物件的值（如同您在上一個範例中使用的輸出運算式），而且您可以查看物件的資料類型資訊。</span><span class="sxs-lookup"><span data-stu-id="eeedb-180">You can use it to view the value of variables and objects in your code (like you did with output expressions in the previous example), plus you can see data type information about the object.</span></span>

1. <span data-ttu-id="eeedb-181">開啟您稍早建立的名為*OutputExpression*的檔案。</span><span class="sxs-lookup"><span data-stu-id="eeedb-181">Open the file named *OutputExpression.cshtml* that you created earlier.</span></span>
2. <span data-ttu-id="eeedb-182">將頁面中的所有程式碼取代為下列程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="eeedb-182">Replace all code in the page with the following block of code:</span></span>

    [!code-html[Main](introduction-to-debugging/samples/sample5.html)]
3. <span data-ttu-id="eeedb-183">在瀏覽器中儲存並執行頁面。</span><span class="sxs-lookup"><span data-stu-id="eeedb-183">Save and run the page in a browser.</span></span>

    ![調試-4](introduction-to-debugging/_static/image3.jpg)

    <span data-ttu-id="eeedb-185">在此範例中，`ObjectInfo` helper 會顯示兩個專案：</span><span class="sxs-lookup"><span data-stu-id="eeedb-185">In this example, the `ObjectInfo` helper displays two items:</span></span>

   - <span data-ttu-id="eeedb-186">類型。</span><span class="sxs-lookup"><span data-stu-id="eeedb-186">The type.</span></span> <span data-ttu-id="eeedb-187">針對第一個變數，類型為 `DayOfWeek`。</span><span class="sxs-lookup"><span data-stu-id="eeedb-187">For the first variable, the type is `DayOfWeek`.</span></span> <span data-ttu-id="eeedb-188">針對第二個變數，類型為 `String`。</span><span class="sxs-lookup"><span data-stu-id="eeedb-188">For the second variable, the type is `String`.</span></span>
   - <span data-ttu-id="eeedb-189">值。</span><span class="sxs-lookup"><span data-stu-id="eeedb-189">The value.</span></span> <span data-ttu-id="eeedb-190">在此情況下，因為您已經在頁面中顯示問候語變數的值，所以當您將變數傳遞給 `ObjectInfo`時，值會再次顯示。</span><span class="sxs-lookup"><span data-stu-id="eeedb-190">In this case, because you already display the value of the greeting variable in the page, the value is displayed again when you pass the variable to `ObjectInfo`.</span></span>

     <span data-ttu-id="eeedb-191">對於更複雜的物件，`ObjectInfo` helper 可以顯示更多&#8212;的資訊，基本上，它可以顯示物件所有屬性的類型和值。</span><span class="sxs-lookup"><span data-stu-id="eeedb-191">For more complex objects, the `ObjectInfo` helper can display more information &#8212; basically, it can display the types and values of all of an object's properties.</span></span>

## <a name="using-debugging-tools-in-visual-studio"></a><span data-ttu-id="eeedb-192">在 Visual Studio 中使用調試工具</span><span class="sxs-lookup"><span data-stu-id="eeedb-192">Using Debugging Tools in Visual Studio</span></span>

<span data-ttu-id="eeedb-193">如需更完整的偵錯工具體驗，請使用[Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)。</span><span class="sxs-lookup"><span data-stu-id="eeedb-193">For a more comprehensive debugging experience, use [Visual Studio](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017).</span></span> <span data-ttu-id="eeedb-194">有了 Visual Studio，您就可以在程式碼中，于想要檢查的那一行設定中斷點。</span><span class="sxs-lookup"><span data-stu-id="eeedb-194">With Visual Studio, you can set a breakpoint in your code at the line that you want to inspect.</span></span>

![設定中斷點](introduction-to-debugging/_static/image1.png)

<span data-ttu-id="eeedb-196">當您測試網站時，執行中的程式碼會在中斷點暫停。</span><span class="sxs-lookup"><span data-stu-id="eeedb-196">When you test the web site, the executing code halts at the breakpoint.</span></span>

![到達中斷點](introduction-to-debugging/_static/image2.png)

<span data-ttu-id="eeedb-198">您可以檢查變數目前的值，並逐行執行程式碼。</span><span class="sxs-lookup"><span data-stu-id="eeedb-198">You can examine the current values of the variables, and step through the code line-by-line.</span></span>

![查看值](introduction-to-debugging/_static/image3.png)

<span data-ttu-id="eeedb-200">如需在 Visual Studio 中使用整合式偵錯工具來 debug ASP.NET Razor 頁面的詳細資訊，請參閱[使用 Visual Studio 的程式設計 ASP.NET Web Pages （Razor）](https://go.microsoft.com/fwlink/?LinkId=205854)。</span><span class="sxs-lookup"><span data-stu-id="eeedb-200">For information about using the integrated debugger in Visual Studio to debug ASP.NET Razor pages, see [Programming ASP.NET Web Pages (Razor) Using Visual Studio](https://go.microsoft.com/fwlink/?LinkId=205854).</span></span>

## <a name="additional-resources"></a><span data-ttu-id="eeedb-201">其他資源</span><span class="sxs-lookup"><span data-stu-id="eeedb-201">Additional Resources</span></span>

- [<span data-ttu-id="eeedb-202">使用 Visual Studio 的程式設計 ASP.NET Web Pages （Razor）</span><span class="sxs-lookup"><span data-stu-id="eeedb-202">Programming ASP.NET Web Pages (Razor) Using Visual Studio</span></span>](https://go.microsoft.com/fwlink/?LinkId=205854)
- <span data-ttu-id="eeedb-203">[IIS 伺服器變數](https://msdn.microsoft.com/library/ms524602(VS.90).aspx)（MSDN）</span><span class="sxs-lookup"><span data-stu-id="eeedb-203">[IIS Server Variables](https://msdn.microsoft.com/library/ms524602(VS.90).aspx) (MSDN)</span></span>
- <span data-ttu-id="eeedb-204">辨識的[環境變數](https://technet.microsoft.com/library/dd560744(WS.10).aspx)（TechNet）</span><span class="sxs-lookup"><span data-stu-id="eeedb-204">[Recognized Environment Variables](https://technet.microsoft.com/library/dd560744(WS.10).aspx) (TechNet)</span></span>
