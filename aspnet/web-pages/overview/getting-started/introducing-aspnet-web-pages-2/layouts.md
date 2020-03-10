---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
title: ASP.NET Web Pages 簡介-建立一致的版面配置 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程示範如何使用版面配置，在使用 ASP.NET Web Pages 的網站上建立頁面的一致外觀。 它假設您已完成 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: c85ec591-f8d7-4882-b763-de6ab9f3df7a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/layouts
msc.type: authoredcontent
ms.openlocfilehash: 678eb7089e95e3d221d6b2d82034a62aefa75757
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78526688"
---
# <a name="introducing-aspnet-web-pages---creating-a-consistent-layout"></a><span data-ttu-id="56885-104">ASP.NET Web Pages 簡介-建立一致的版面配置</span><span class="sxs-lookup"><span data-stu-id="56885-104">Introducing ASP.NET Web Pages - Creating a Consistent Layout</span></span>

<span data-ttu-id="56885-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="56885-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="56885-106">本教學課程示範如何使用*版面*配置，在使用 ASP.NET Web Pages 的網站上建立頁面的一致外觀。</span><span class="sxs-lookup"><span data-stu-id="56885-106">This tutorial shows you how to use *layouts* to create a consistent look for the pages on a site that uses ASP.NET Web Pages.</span></span> <span data-ttu-id="56885-107">它假設您已透過[刪除 ASP.NET Web Pages 中的資料庫資料](https://go.microsoft.com/fwlink/?LinkId=251584)來完成數列。</span><span class="sxs-lookup"><span data-stu-id="56885-107">It assumes you have completed the series through [Deleting Database Data in ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251584).</span></span>
> 
> <span data-ttu-id="56885-108">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="56885-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="56885-109">什麼是版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="56885-109">What a layout page is.</span></span>
> - <span data-ttu-id="56885-110">如何結合版面配置頁與動態內容。</span><span class="sxs-lookup"><span data-stu-id="56885-110">How to combine layout pages with dynamic content.</span></span>
> - <span data-ttu-id="56885-111">如何將值傳遞至版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="56885-111">How to pass values to a layout page.</span></span>

## <a name="about-layouts"></a><span data-ttu-id="56885-112">關於版面配置</span><span class="sxs-lookup"><span data-stu-id="56885-112">About Layouts</span></span>

<span data-ttu-id="56885-113">您目前所建立的頁面已全部完成，也就是獨立頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-113">The pages you've created so far have all been complete, standalone pages.</span></span> <span data-ttu-id="56885-114">它們全都屬於相同的網站，但沒有任何通用元素或標準外觀。</span><span class="sxs-lookup"><span data-stu-id="56885-114">They all belong to the same site, but they don't have any common elements or a standard look.</span></span>

<span data-ttu-id="56885-115">大部分的網站都具有一致的外觀和版面配置。</span><span class="sxs-lookup"><span data-stu-id="56885-115">Most sites do have a consistent look and layout.</span></span> <span data-ttu-id="56885-116">例如，如果您移至[Microsoft.com/web](https://www.microsoft.com/web/)網站並尋找，您會看到所有頁面都遵守整體版面配置和視覺主題：</span><span class="sxs-lookup"><span data-stu-id="56885-116">For example, if you go to the [Microsoft.com/web](https://www.microsoft.com/web/) site and look around, you see that the pages all adhere to an overall layout and to a visual theme:</span></span>

![顯示標題、導覽區域、內容區域和頁尾版面配置的 Microsoft.com/web 網站頁面](layouts/_static/image1.png)

<span data-ttu-id="56885-118">建立這種版面配置的*效率*不佳，就是在每個頁面上分別定義頁首、導覽列和頁尾。</span><span class="sxs-lookup"><span data-stu-id="56885-118">An *inefficient* way to create this layout would be to define a header, navigation bar, and footer separately on each of your pages.</span></span> <span data-ttu-id="56885-119">您每次都會複製相同的標記。</span><span class="sxs-lookup"><span data-stu-id="56885-119">You'd be duplicating the same markup each time.</span></span> <span data-ttu-id="56885-120">如果您想要變更某個專案（例如，更新頁尾），您必須分別變更每個頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-120">If you wanted to change something (for example, update the footer), you'd have to change each page separately.</span></span>

<span data-ttu-id="56885-121">這就是*版面配置頁面*的所在位置。</span><span class="sxs-lookup"><span data-stu-id="56885-121">That's where *layout pages* come in.</span></span> <span data-ttu-id="56885-122">在 ASP.NET Web Pages 中，您可以定義在網站上提供頁面整體容器的版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="56885-122">In ASP.NET Web Pages, you can define a layout page that provides an overall container for pages on your site.</span></span> <span data-ttu-id="56885-123">例如，版面配置頁可以包含頁首、導覽區域和頁尾。</span><span class="sxs-lookup"><span data-stu-id="56885-123">For example, the layout page can contain the header, navigation area, and footer.</span></span> <span data-ttu-id="56885-124">版面配置頁包含主要內容的預留位置。</span><span class="sxs-lookup"><span data-stu-id="56885-124">The layout page includes a placeholder where the main content goes.</span></span>

<span data-ttu-id="56885-125">接著，您可以定義個別的內容頁面，其中只包含該頁面的標記和程式碼。</span><span class="sxs-lookup"><span data-stu-id="56885-125">You can then define individual content pages that contain the markup and the code for only that page.</span></span> <span data-ttu-id="56885-126">內容頁不需要是完整的 HTML 網頁;他們甚至不需要有 `<body>` 元素。</span><span class="sxs-lookup"><span data-stu-id="56885-126">Content pages don't have to be complete HTML pages; they don't even have to have a `<body>` element.</span></span> <span data-ttu-id="56885-127">它們也有一行程式碼，告訴 ASP.NET 您要顯示內容的版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="56885-127">They also have a line of code that tells ASP.NET what layout page you want to display the content in.</span></span> <span data-ttu-id="56885-128">以下是大致說明此關聯性運作方式的圖片：</span><span class="sxs-lookup"><span data-stu-id="56885-128">Here's a picture that shows roughly how this relationship works:</span></span>

![顯示兩個內容頁和版面配置頁的概念圖表](layouts/_static/image2.png)

<span data-ttu-id="56885-130">當您看到此互動運作時，可以輕鬆地瞭解。</span><span class="sxs-lookup"><span data-stu-id="56885-130">This interaction is easy to understand when you see it in action.</span></span> <span data-ttu-id="56885-131">在本教學課程中，您會將電影頁面變更為使用版面配置。</span><span class="sxs-lookup"><span data-stu-id="56885-131">In this tutorial, you'll change your movies pages to use a layout.</span></span>

## <a name="adding-a-layout-page"></a><span data-ttu-id="56885-132">新增版面配置頁</span><span class="sxs-lookup"><span data-stu-id="56885-132">Adding a Layout Page</span></span>

<span data-ttu-id="56885-133">首先，您要建立一個版面配置頁面，其中定義了標題為頁尾的一般頁面配置，以及主要內容的區域。</span><span class="sxs-lookup"><span data-stu-id="56885-133">You'll start by creating a layout page that defines a typical page layout with a header, footer, and an area for the main content.</span></span> <span data-ttu-id="56885-134">在 WebPagesMovies 網站中，新增名為 *\_Layout*的 CSHTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-134">In the WebPagesMovies site, add a CSHTML page named *\_Layout.cshtml*.</span></span>

<span data-ttu-id="56885-135">前置底線（`_`）字元很重要。</span><span class="sxs-lookup"><span data-stu-id="56885-135">The leading underscore ( `_` ) character is significant.</span></span> <span data-ttu-id="56885-136">如果頁面名稱的開頭是底線，ASP.NET 就不會直接將該頁面傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="56885-136">If a page's name starts with an underscore, ASP.NET won't directly send that page to the browser.</span></span> <span data-ttu-id="56885-137">此慣例可讓您定義網站所需的頁面，但使用者應該不能直接要求。</span><span class="sxs-lookup"><span data-stu-id="56885-137">This convention lets you define pages that are required for your site but that users shouldn't be able to request directly.</span></span>

<span data-ttu-id="56885-138">將頁面中的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="56885-138">Replace the content in the page with the following:</span></span>

[!code-html[Main](layouts/samples/sample1.html)]

<span data-ttu-id="56885-139">如您所見，此標記只是 HTML，它會使用 `<div>` 元素來定義頁面中的三個區段，再加上一個 `<div>` 元素來保存這三個區段。</span><span class="sxs-lookup"><span data-stu-id="56885-139">As you can see, this markup is just HTML that uses `<div>` elements to define three sections in the page plus one more `<div>` element to hold the three sections.</span></span> <span data-ttu-id="56885-140">頁尾包含一些 Razor 程式碼： `@DateTime.Now.Year`，這會在頁面中的該位置呈現目前的年份。</span><span class="sxs-lookup"><span data-stu-id="56885-140">The footer contains a bit of Razor code: `@DateTime.Now.Year`, which will render the current year at that location in the page.</span></span>

<span data-ttu-id="56885-141">請注意，有一個名為 [*電影 .css*] 的樣式表單連結。</span><span class="sxs-lookup"><span data-stu-id="56885-141">Notice that there's a link to a style sheet named *Movies.css*.</span></span> <span data-ttu-id="56885-142">樣式表單是要定義元素實體配置詳細資料的位置。</span><span class="sxs-lookup"><span data-stu-id="56885-142">The style sheet is where the details of the physical layout of the elements will be defined.</span></span> <span data-ttu-id="56885-143">您很快就會建立這項功能。</span><span class="sxs-lookup"><span data-stu-id="56885-143">You'll create that in a moment.</span></span>

<span data-ttu-id="56885-144">此 *\_Layout*  頁面中唯一不尋常的功能是 `@Render.Body()` 行。</span><span class="sxs-lookup"><span data-stu-id="56885-144">The only unusual feature in this *\_Layout.cshtml* page is the `@Render.Body()` line.</span></span> <span data-ttu-id="56885-145">這就是當此配置與另一個頁面合併時，內容將會前往的預留位置。</span><span class="sxs-lookup"><span data-stu-id="56885-145">That's the placeholder where the content will go when this layout is merged with another page.</span></span>

## <a name="adding-a-css-file"></a><span data-ttu-id="56885-146">新增 .css 檔案</span><span class="sxs-lookup"><span data-stu-id="56885-146">Adding a .css File</span></span>

<span data-ttu-id="56885-147">若要定義頁面上元素的實際相片順序（也就是外觀），慣用的方法是使用級聯樣式表（CSS）規則。</span><span class="sxs-lookup"><span data-stu-id="56885-147">The preferred way to define the actual arrangement (that is, appearance) of elements on the page is to use cascading style sheet (CSS) rules.</span></span> <span data-ttu-id="56885-148">因此，您將建立一個 *.css*檔案，其中包含您新版面配置的規則。</span><span class="sxs-lookup"><span data-stu-id="56885-148">So you'll create a *.css* file that has the rules for your new layout.</span></span>

<span data-ttu-id="56885-149">在 WebMatrix 中，選取您網站的根目錄。</span><span class="sxs-lookup"><span data-stu-id="56885-149">In WebMatrix, select the root of your site.</span></span> <span data-ttu-id="56885-150">然後在功能區的 [檔案] 索引標籤中，按一下 [**新增**] 按鈕**底下的箭**號，然後按一下 [**新增資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="56885-150">Then in the **Files** tab of the ribbon, click the arrow under the **New** button and then click **New Folder**.</span></span>

![功能區中 [新增] 底下的 [新增資料夾] 選項。](layouts/_static/image3.png)

<span data-ttu-id="56885-152">將新的資料夾命名為*樣式*。</span><span class="sxs-lookup"><span data-stu-id="56885-152">Name the new folder *Styles*.</span></span>

![將新資料夾命名為「樣式」](layouts/_static/image4.png)

<span data-ttu-id="56885-154">在 [新*樣式*] 資料夾內，建立名為 [*電影 .css*] 的檔案。</span><span class="sxs-lookup"><span data-stu-id="56885-154">Inside the new *Styles* folder, create a file named *Movies.css*.</span></span>

![建立新的電影 .css 檔案](layouts/_static/image5.png)

<span data-ttu-id="56885-156">將新 *.css*檔案的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="56885-156">Replace the contents of the new *.css* file with the following:</span></span>

[!code-css[Main](layouts/samples/sample2.css)]

<span data-ttu-id="56885-157">除了注意兩件事以外，我們不會對這些 CSS 規則有太大的看法。</span><span class="sxs-lookup"><span data-stu-id="56885-157">We won't say much about these CSS rules, except to note two things.</span></span> <span data-ttu-id="56885-158">其中一種是除了設定字型和大小之外，規則也會使用絕對位置來建立頁首、頁尾和主要內容區域的位置。</span><span class="sxs-lookup"><span data-stu-id="56885-158">One is that in addition to setting fonts and sizes, the rules use absolute positioning to establish the location of the header, footer, and main content area.</span></span> <span data-ttu-id="56885-159">如果您不熟悉 CSS 中的定位，可以閱讀 W3Schools 網站上的[Css 定位](http://www.w3schools.com/css/css_positioning.asp)教學課程。</span><span class="sxs-lookup"><span data-stu-id="56885-159">If you're new to positioning in CSS, you can read the [CSS Positioning](http://www.w3schools.com/css/css_positioning.asp) tutorial at the W3Schools site.</span></span>

<span data-ttu-id="56885-160">另一個要注意的是，我們在底部複製了原本在*電影. cshtml*檔案中個別定義的樣式規則。</span><span class="sxs-lookup"><span data-stu-id="56885-160">The other thing to note is that at the bottom, we've copied the style rules that were originally defined individually in the *Movies.cshtml* file.</span></span> <span data-ttu-id="56885-161">這些規則是在使用 ASP.NET Web Pages 教學課程來[顯示資料的簡介](https://go.microsoft.com/fwlink/?LinkId=251580)中使用，以便讓 `WebGrid` 協助程式轉譯標記將條紋新增至資料表。</span><span class="sxs-lookup"><span data-stu-id="56885-161">These rules were used in the [Introduction to Displaying Data by Using ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=251580) tutorial to make the `WebGrid` helper render markup that added stripes to the table.</span></span> <span data-ttu-id="56885-162">（如果您要使用樣式定義的 *.css*檔案，可能也會將整個網站的樣式規則放在其中）。</span><span class="sxs-lookup"><span data-stu-id="56885-162">(If you're going to use a *.css* file for style definitions, you might as well put the style rules for the whole site in it.)</span></span>

## <a name="updating-the-movies-file-to-use-the-layout"></a><span data-ttu-id="56885-163">更新電影檔案以使用版面配置</span><span class="sxs-lookup"><span data-stu-id="56885-163">Updating the Movies File to Use the Layout</span></span>

<span data-ttu-id="56885-164">現在您可以更新網站中的現有檔案，以使用新的版面配置。</span><span class="sxs-lookup"><span data-stu-id="56885-164">Now you can update the existing files in your site to use the new layout.</span></span> <span data-ttu-id="56885-165">開啟 [*電影*] 檔案。</span><span class="sxs-lookup"><span data-stu-id="56885-165">Open the *Movies.cshtml* file.</span></span> <span data-ttu-id="56885-166">在頂端，作為第一行程式碼，新增下列內容：</span><span class="sxs-lookup"><span data-stu-id="56885-166">At the top, as the first line of code, add the following:</span></span>

[!code-csharp[Main](layouts/samples/sample3.cs)]

<span data-ttu-id="56885-167">網頁現在以這種方式啟動：</span><span class="sxs-lookup"><span data-stu-id="56885-167">The page now starts out this way:</span></span>

[!code-cshtml[Main](layouts/samples/sample4.cshtml?highlight=2)]

<span data-ttu-id="56885-168">這一行程式碼會告訴 ASP.NET，當 [*電影*] 頁面執行時，應該與\_的配置*cshtml*檔案合併。</span><span class="sxs-lookup"><span data-stu-id="56885-168">This one line of code tells ASP.NET that when the *Movies* page runs, it should be merged with the *\_Layout.cshtml* file.</span></span>

<span data-ttu-id="56885-169">由於*電影的 cshtml*檔案現在使用版面配置頁面，因此您可以從 *\_配置 cshtml*檔案所處理的 [ *cshtml* ] 頁面中移除標記。</span><span class="sxs-lookup"><span data-stu-id="56885-169">Since the *Movies.cshtml* file now uses a layout page, you can remove the markup from the *Movies.cshtml* page that's taken care of by the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="56885-170">取出 `<!DOCTYPE>`、`<html>`，並 `<body>` 開頭和結束記號。</span><span class="sxs-lookup"><span data-stu-id="56885-170">Take out the `<!DOCTYPE>`, `<html>`, and `<body>` opening and closing tags.</span></span> <span data-ttu-id="56885-171">取出整個 `<head>` 專案及其內容，其中包括方格的樣式規則，因為您現在已經在 *.css*檔案中取得這些規則。</span><span class="sxs-lookup"><span data-stu-id="56885-171">Take out the entire `<head>` element and its contents, which includes the style rules for the grid, since you've now got those rules in a *.css* file.</span></span> <span data-ttu-id="56885-172">當您在此時，請將現有的 `<h1>` 專案變更為 `<h2>` 元素;您在版面配置頁中已經有 `<h1>` 元素。</span><span class="sxs-lookup"><span data-stu-id="56885-172">While you're at it, change the existing `<h1>` element to an `<h2>` element; you have an `<h1>` element in the layout page already.</span></span> <span data-ttu-id="56885-173">將 `<h2>` 文字變更為「列出電影」。</span><span class="sxs-lookup"><span data-stu-id="56885-173">Change the `<h2>` text to "List Movies".</span></span>

<span data-ttu-id="56885-174">通常您不需要在 [內容] 頁面中進行這類變更。</span><span class="sxs-lookup"><span data-stu-id="56885-174">Normally you wouldn't have to make these sorts of changes in a content page.</span></span> <span data-ttu-id="56885-175">當您使用版面配置頁面來啟動網站時，您會建立內容頁面，而不需要所有這些元素。</span><span class="sxs-lookup"><span data-stu-id="56885-175">When you start your site out with a layout page, you create content pages without all these elements to begin with.</span></span> <span data-ttu-id="56885-176">不過，在此情況下，您要將獨立頁面轉換成使用版面配置的網頁，所以有一些清除。</span><span class="sxs-lookup"><span data-stu-id="56885-176">In this case, though, you're converting a standalone page to one that uses a layout, so there's a bit of cleanup.</span></span>

<span data-ttu-id="56885-177">當您完成時，[*影片*] 的 [cshtml] 頁面看起來會像下面這樣：</span><span class="sxs-lookup"><span data-stu-id="56885-177">When you're finished, the *Movies.cshtml* page will look like the following:</span></span>

[!code-cshtml[Main](layouts/samples/sample5.cshtml)]

### <a name="testing-the-layout"></a><span data-ttu-id="56885-178">測試版面配置</span><span class="sxs-lookup"><span data-stu-id="56885-178">Testing the Layout</span></span>

<span data-ttu-id="56885-179">現在您可以看到版面配置的外觀。</span><span class="sxs-lookup"><span data-stu-id="56885-179">Now you can see what the layout looks like.</span></span> <span data-ttu-id="56885-180">在 WebMatrix 中，以滑鼠右鍵按一下 [*影片. cshtml* ] 頁面，然後選取 [**在瀏覽器中啟動**]。</span><span class="sxs-lookup"><span data-stu-id="56885-180">In WebMatrix, right-click the *Movies.cshtml* page and select **Launch in browser**.</span></span> <span data-ttu-id="56885-181">當瀏覽器顯示頁面時，它看起來會像這個頁面：</span><span class="sxs-lookup"><span data-stu-id="56885-181">When the browser displays the page, it looks like this page:</span></span>

![使用版面配置呈現的電影頁面](layouts/_static/image6.png)

<span data-ttu-id="56885-183">ASP.NET 已將 電影 頁面的內容合併到 `RenderBody` 方法所在的 *\_Layout*  頁面中。</span><span class="sxs-lookup"><span data-stu-id="56885-183">ASP.NET has merged the content of the Movies.cshtml page into the *\_Layout.cshtml* page right where the `RenderBody` method is.</span></span> <span data-ttu-id="56885-184">當然， *\_Layout*  頁面會參考定義頁面外觀的 *.css*檔案。</span><span class="sxs-lookup"><span data-stu-id="56885-184">And of course the *\_Layout.cshtml* page references a *.css* file that defines the look of the page.</span></span>

## <a name="updating-the-addmovie-page-to-use-the-layout"></a><span data-ttu-id="56885-185">更新 AddMovie 頁面以使用版面配置</span><span class="sxs-lookup"><span data-stu-id="56885-185">Updating the AddMovie Page to Use the Layout</span></span>

<span data-ttu-id="56885-186">版面配置的實際優點是您可以將其用於網站中的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-186">The real benefit of layouts is that you can use them for all the pages in your site.</span></span> <span data-ttu-id="56885-187">開啟 [ *AddMovie* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-187">Open the *AddMovie.cshtml* page.</span></span>

<span data-ttu-id="56885-188">您可能會忘了， *AddMovie*一頁原本有一些 CSS 規則，可以定義驗證錯誤訊息的外觀。</span><span class="sxs-lookup"><span data-stu-id="56885-188">You might remember that the *AddMovie.cshtml* page originally had some CSS rules in it to define the look of validation error messages.</span></span> <span data-ttu-id="56885-189">因為您現在有網站的 *.css*檔案，所以您可以將這些規則移到 *.css*檔案。</span><span class="sxs-lookup"><span data-stu-id="56885-189">Since you have a *.css* file for your site now, you can move those rules to the *.css* file.</span></span> <span data-ttu-id="56885-190">將它們從*AddMovie*檔案中移除，並將它們新增至*電影 .css*檔案的底部。</span><span class="sxs-lookup"><span data-stu-id="56885-190">Remove them from the *AddMovie.cshtml* file and add them to the bottom of the *Movies.css* file.</span></span> <span data-ttu-id="56885-191">您要移動下列規則：</span><span class="sxs-lookup"><span data-stu-id="56885-191">You are moving the following rules:</span></span>

[!code-css[Main](layouts/samples/sample6.css)]

<span data-ttu-id="56885-192">現在在*AddMovie*中，對您的電影進行相同的變更。 *cshtml* —新增 `Layout="~/_Layout.cshtml;`，並移除現在無關的 HTML 標籤。</span><span class="sxs-lookup"><span data-stu-id="56885-192">Now make the same sorts of changes in *AddMovie.cshtml* that you did for *Movies.cshtml* — add `Layout="~/_Layout.cshtml;` and remove the HTML markup that's now extraneous.</span></span> <span data-ttu-id="56885-193">將 `<h1>` 元素變更為 `<h2>`。</span><span class="sxs-lookup"><span data-stu-id="56885-193">Change the `<h1>` element to `<h2>`.</span></span> <span data-ttu-id="56885-194">當您完成時，頁面看起來會像下列範例：</span><span class="sxs-lookup"><span data-stu-id="56885-194">When you're done, the page will look like this example:</span></span>

[!code-cshtml[Main](layouts/samples/sample7.cshtml)]

<span data-ttu-id="56885-195">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-195">Run the page.</span></span> <span data-ttu-id="56885-196">現在看起來如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="56885-196">Now it looks like this illustration:</span></span>

![使用版面配置呈現的 [新增電影] 頁面](layouts/_static/image7.png)

<span data-ttu-id="56885-198">您想要對網站中的頁面進行類似的變更，也就是*EditMovie*和*DeleteMovie*。</span><span class="sxs-lookup"><span data-stu-id="56885-198">You want to make similar changes to the pages in the site — *EditMovie.cshtml* and *DeleteMovie.cshtml*.</span></span> <span data-ttu-id="56885-199">不過，在這麼做之前，您可以對配置進行另一個變更，讓它更具彈性。</span><span class="sxs-lookup"><span data-stu-id="56885-199">However, before you do, you can make another change to the layout that makes it a little more flexible.</span></span>

## <a name="passing-title-information-to-the-layout-page"></a><span data-ttu-id="56885-200">將標題資訊傳遞至版面配置頁</span><span class="sxs-lookup"><span data-stu-id="56885-200">Passing Title Information to the Layout Page</span></span>

<span data-ttu-id="56885-201">您所建立的 *\_配置. cshtml*  頁面具有設定為「我的電影網站」的 `<title>` 元素。</span><span class="sxs-lookup"><span data-stu-id="56885-201">The *\_Layout.cshtml* page that you created has a `<title>` element that's set to "My Movie Site".</span></span> <span data-ttu-id="56885-202">大部分的瀏覽器都會將此元素的內容顯示為索引標籤上的文字：</span><span class="sxs-lookup"><span data-stu-id="56885-202">Most browsers display the content of this element as the text on a tab:</span></span>

![在瀏覽器索引標籤中顯示的頁面 &lt;標題&gt; 元素](layouts/_static/image8.png)

<span data-ttu-id="56885-204">此標題資訊是泛型的。</span><span class="sxs-lookup"><span data-stu-id="56885-204">This title information is generic.</span></span> <span data-ttu-id="56885-205">假設您希望標題文字更特定于目前頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-205">Suppose that you want the title text to be more specific to the current page.</span></span> <span data-ttu-id="56885-206">（搜尋引擎也會使用標題文字來判斷您的頁面為何）。您可以將內容頁面中的資訊（例如，像是*電影*或*AddMovie* ）傳遞至版面配置頁，然後使用該資訊來自訂版面配置頁的呈現方式。</span><span class="sxs-lookup"><span data-stu-id="56885-206">(The title text is also used by search engines to determine what your page is about.) You can pass information from a content page like *Movies.cshtml* or *AddMovie.cshtml* to the layout page, and then use that information to customize what the layout page renders.</span></span>

<span data-ttu-id="56885-207">再次開啟 [*電影. cshtml* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-207">Open the *Movies.cshtml* page again.</span></span> <span data-ttu-id="56885-208">在頂端的程式碼中，新增下面這一行：</span><span class="sxs-lookup"><span data-stu-id="56885-208">In the code at the top, add the following line:</span></span>

[!code-csharp[Main](layouts/samples/sample8.cs)]

<span data-ttu-id="56885-209">`Page` 物件可在所有的*cshtml*頁面上使用，基於此目的，也就是在頁面與其配置之間共用資訊。</span><span class="sxs-lookup"><span data-stu-id="56885-209">The `Page` object is available on all *.cshtml* pages and is for this purpose, namely to share information between a page and its layout.</span></span>

<span data-ttu-id="56885-210">開啟 *\_Layout*  頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-210">Open the *\_Layout.cshtml* page.</span></span> <span data-ttu-id="56885-211">變更 `<title>` 元素，使其看起來像此標記：</span><span class="sxs-lookup"><span data-stu-id="56885-211">Change the `<title>` element so that it looks like this markup:</span></span>

[!code-html[Main](layouts/samples/sample9.html)]

<span data-ttu-id="56885-212">此程式碼會在頁面中的該位置直接呈現在 [`Page.Title`] 屬性中的任何內容。</span><span class="sxs-lookup"><span data-stu-id="56885-212">This code renders whatever is in the `Page.Title` property right at that location in the page.</span></span>

<span data-ttu-id="56885-213">執行 [*電影. cshtml* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-213">Run the *Movies.cshtml* page.</span></span> <span data-ttu-id="56885-214">此時，[瀏覽器] 索引標籤會顯示您傳遞做為 `Page.Title`值的內容：</span><span class="sxs-lookup"><span data-stu-id="56885-214">This time the browser tab shows what you passed as the value of `Page.Title`:</span></span>

![顯示動態建立之標題的瀏覽器索引標籤](layouts/_static/image9.png)

<span data-ttu-id="56885-216">如果您想要的話，請在瀏覽器中查看頁面來源。</span><span class="sxs-lookup"><span data-stu-id="56885-216">If you want, view the page source in the browser.</span></span> <span data-ttu-id="56885-217">您可以看到 `<title>` 元素會轉譯為 `<title>List Movies</title>`。</span><span class="sxs-lookup"><span data-stu-id="56885-217">You can see that the `<title>` element is rendered as `<title>List Movies</title>`.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="56885-218">**Page 物件**</span><span class="sxs-lookup"><span data-stu-id="56885-218">**The Page Object**</span></span>
> 
> <span data-ttu-id="56885-219">`Page` 的一個有用功能是動態物件，`Title` 屬性不是固定或保留名稱。</span><span class="sxs-lookup"><span data-stu-id="56885-219">A useful feature of `Page` is that it's a dynamic object — the `Title` property is not a fixed or reserved name.</span></span> <span data-ttu-id="56885-220">您可以使用*任何*名稱作為 `Page` 物件的值。</span><span class="sxs-lookup"><span data-stu-id="56885-220">You can use *any* name for a value of the `Page` object.</span></span> <span data-ttu-id="56885-221">例如，您可以使用名為 `Page.CurrentName` 或 `Page.MyPage`的屬性，輕鬆地傳遞標題。</span><span class="sxs-lookup"><span data-stu-id="56885-221">For example, you could as easily have passed the title by using a property named `Page.CurrentName` or `Page.MyPage`.</span></span> <span data-ttu-id="56885-222">唯一的限制是名稱必須遵循一般規則，才能命名哪些屬性。</span><span class="sxs-lookup"><span data-stu-id="56885-222">The only restriction is that the name has to follow the normal rules for what properties can be named.</span></span> <span data-ttu-id="56885-223">（例如，名稱不能包含空格）。</span><span class="sxs-lookup"><span data-stu-id="56885-223">(For example, the name can't contain a space.)</span></span>
> 
> <span data-ttu-id="56885-224">您可以使用 `Page` 物件來傳遞任意數目的值。</span><span class="sxs-lookup"><span data-stu-id="56885-224">You can pass any number of values by using the `Page` object.</span></span> <span data-ttu-id="56885-225">如果您想要將電影資訊傳遞至版面配置頁面，您可以使用類似 `Page.MovieTitle` 和 `Page.Genre` 和 `Page.MovieYear`來傳遞值。</span><span class="sxs-lookup"><span data-stu-id="56885-225">If you wanted to pass movie information to the layout page, you could pass values by using something like `Page.MovieTitle` and `Page.Genre` and `Page.MovieYear`.</span></span> <span data-ttu-id="56885-226">（或您為了儲存資訊所需的任何其他名稱）。唯一的要求（可能是顯而易見的）是您必須在 [內容] 頁面和 [版面配置] 頁面中使用相同的名稱。</span><span class="sxs-lookup"><span data-stu-id="56885-226">(Or any other names that you invented to store the information.) The only requirement — which is probably obvious — is that you have to use the same names in the content page and the layout page.</span></span>
> 
> <span data-ttu-id="56885-227">您使用 `Page` 物件傳遞的資訊，並不限於只在版面配置頁上顯示的文字。</span><span class="sxs-lookup"><span data-stu-id="56885-227">The information you pass by using the `Page` object isn't limited to just text to display on the layout page.</span></span> <span data-ttu-id="56885-228">您可以將值傳遞至版面配置頁，然後在版面配置頁中的程式碼可以使用值來決定要顯示頁面的區段、要使用的 *.css*檔案等等。</span><span class="sxs-lookup"><span data-stu-id="56885-228">You can pass a value to the layout page, and then code in the layout page can use the value to decide whether to display a section of the page, what *.css* file to use, and so on.</span></span> <span data-ttu-id="56885-229">您在 `Page` 物件中傳遞的值，就像您在程式碼中使用的任何其他值。</span><span class="sxs-lookup"><span data-stu-id="56885-229">The values you pass in the `Page` object are like any other values that you use in code.</span></span> <span data-ttu-id="56885-230">這只是值源自于 [內容] 頁面，而且會傳遞至版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="56885-230">It's just that the values originate in the content page and are passed to the layout page.</span></span>

<span data-ttu-id="56885-231">開啟 [ *AddMovie* ] 頁面，並在程式碼頂端新增一行，以提供 [ *AddMovie* ] 頁面的標題：</span><span class="sxs-lookup"><span data-stu-id="56885-231">Open the *AddMovie.cshtml* page and add a line to the top of the code that provides a title for the *AddMovie.cshtml* page:</span></span>

[!code-csharp[Main](layouts/samples/sample10.cs)]

<span data-ttu-id="56885-232">執行 [ *AddMovie* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="56885-232">Run the *AddMovie.cshtml* page.</span></span> <span data-ttu-id="56885-233">您會在該處看到新的標題：</span><span class="sxs-lookup"><span data-stu-id="56885-233">You see the new title there:</span></span>

![顯示動態建立的 [新增電影] 標題的瀏覽器索引標籤](layouts/_static/image10.png)

## <a name="updating-the-remaining-pages-to-use-the-layout"></a><span data-ttu-id="56885-235">更新其餘頁面以使用版面配置</span><span class="sxs-lookup"><span data-stu-id="56885-235">Updating the Remaining Pages to Use the Layout</span></span>

<span data-ttu-id="56885-236">現在您可以完成網站中的其餘頁面，使其使用新的版面配置。</span><span class="sxs-lookup"><span data-stu-id="56885-236">Now you can finish the remaining pages in your site so that they use the new layout.</span></span> <span data-ttu-id="56885-237">依次開啟*EditMovie*和*DeleteMovie* ，並在每個中進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="56885-237">Open *EditMovie.cshtml* and *DeleteMovie.cshtml* in turn and make the same changes in each.</span></span>

<span data-ttu-id="56885-238">加入連結至版面配置頁的程式程式碼：</span><span class="sxs-lookup"><span data-stu-id="56885-238">Add the line of code that links to the layout page:</span></span>

[!code-csharp[Main](layouts/samples/sample11.cs)]

<span data-ttu-id="56885-239">新增行以設定頁面的標題：</span><span class="sxs-lookup"><span data-stu-id="56885-239">Add a line to set the title of the page:</span></span>

[!code-csharp[Main](layouts/samples/sample12.cs)]

<span data-ttu-id="56885-240">或：</span><span class="sxs-lookup"><span data-stu-id="56885-240">or:</span></span>

[!code-csharp[Main](layouts/samples/sample13.cs)]

<span data-ttu-id="56885-241">移除所有無關的 HTML 標籤-基本上，只保留 `<body>` 專案內的位（再加上頂端的程式碼區塊）。</span><span class="sxs-lookup"><span data-stu-id="56885-241">Remove all the extraneous HTML markup — basically, leave only the bits that are inside the `<body>` element (plus the code block at the top).</span></span>

<span data-ttu-id="56885-242">將 `<h1>` 元素變更為 `<h2>` 元素。</span><span class="sxs-lookup"><span data-stu-id="56885-242">Change the `<h1>` element to be an `<h2>` element.</span></span>

<span data-ttu-id="56885-243">當您進行這些變更時，請進行測試，並確定其顯示正確且標題正確。</span><span class="sxs-lookup"><span data-stu-id="56885-243">When you've made these changes, test each and make sure that it's displaying properly and that the title is correct.</span></span>

## <a name="parting-thoughts-about-layout-pages"></a><span data-ttu-id="56885-244">關於版面配置頁的資訊</span><span class="sxs-lookup"><span data-stu-id="56885-244">Parting Thoughts About Layout Pages</span></span>

<span data-ttu-id="56885-245">在本教學課程中，您建立了 *\_Layout*  頁面，並使用 `RenderBody` 方法來合併另一頁的內容。</span><span class="sxs-lookup"><span data-stu-id="56885-245">In this tutorial you created a *\_Layout.cshtml* page and used the `RenderBody` method to merge content from another page.</span></span> <span data-ttu-id="56885-246">這是在網頁中使用版面配置的基本模式。</span><span class="sxs-lookup"><span data-stu-id="56885-246">That's the basic pattern for using layouts in Web Pages.</span></span>

<span data-ttu-id="56885-247">版面配置頁有其他不在此討論的功能。</span><span class="sxs-lookup"><span data-stu-id="56885-247">Layout pages have additional features that we didn't cover here.</span></span> <span data-ttu-id="56885-248">例如，您可以嵌套版面配置頁，一個版面配置頁可以輪流參考另一個。</span><span class="sxs-lookup"><span data-stu-id="56885-248">For example, you can nest layout pages — one layout page can in turn reference another.</span></span> <span data-ttu-id="56885-249">如果您要使用需要不同版面配置的網站子區段，則可以使用嵌套的版面配置。</span><span class="sxs-lookup"><span data-stu-id="56885-249">Nested layouts can be useful if you're working with subsections of a site that require different layouts.</span></span> <span data-ttu-id="56885-250">您也可以使用其他方法（例如 `RenderSection`），在版面配置頁面中設定已命名的區段。</span><span class="sxs-lookup"><span data-stu-id="56885-250">You can also use additional methods (for example, `RenderSection`) to set up named sections in the layout page.</span></span>

<span data-ttu-id="56885-251">版面配置頁和 *.css*檔案的組合功能強大。</span><span class="sxs-lookup"><span data-stu-id="56885-251">The combination of layout pages and *.css* files is powerful.</span></span> <span data-ttu-id="56885-252">如您在下一個教學課程系列中所見，您可以在 WebMatrix 中建立以*範本*為基礎的網站，這會提供您在其中預先建立功能的網站。</span><span class="sxs-lookup"><span data-stu-id="56885-252">As you'll see in the next tutorial series, in WebMatrix you can create a site based on a *template*, which gives you a site that has prebuilt functionality in it.</span></span> <span data-ttu-id="56885-253">這些範本可充分利用版面配置頁和 CSS，建立外觀良好且具有功能表等功能的網站。</span><span class="sxs-lookup"><span data-stu-id="56885-253">The templates make good use of layout pages and CSS to create sites that look great and that have features like menus.</span></span> <span data-ttu-id="56885-254">以下是以範本為基礎之網站首頁的螢幕擷取畫面，其中顯示使用版面配置頁和 CSS 的功能：</span><span class="sxs-lookup"><span data-stu-id="56885-254">Here's a screenshot of the home page from a site based on a template, showing features that use layout pages and CSS:</span></span>

![由 WebMatrix 網站範本所建立的版面配置，顯示標頭、流覽區域、內容區域、選擇性區段和登入連結](layouts/_static/image11.png)

## <a name="complete-listing-for-movie-page-updated-to-use-a-layout-page"></a><span data-ttu-id="56885-256">電影頁面的完整清單（更新為使用版面配置頁面）</span><span class="sxs-lookup"><span data-stu-id="56885-256">Complete Listing for Movie Page (Updated to Use a Layout Page)</span></span>

[!code-cshtml[Main](layouts/samples/sample14.cshtml)]

## <a name="complete-page-listing-for-add-movie-page-updated-for-layout"></a><span data-ttu-id="56885-257">[新增電影] 頁面的完成頁面清單（針對版面配置更新）</span><span class="sxs-lookup"><span data-stu-id="56885-257">Complete Page Listing for Add Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample15.cshtml)]

## <a name="complete-page-listing-for-delete-movie-page-updated-for-layout"></a><span data-ttu-id="56885-258">[刪除電影] 頁面的完成頁面清單（已針對版面配置更新）</span><span class="sxs-lookup"><span data-stu-id="56885-258">Complete Page Listing for Delete Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample16.cshtml)]

## <a name="complete-page-listing-for-edit-movie-page-updated-for-layout"></a><span data-ttu-id="56885-259">編輯電影頁面的完成頁面清單（已針對版面配置更新）</span><span class="sxs-lookup"><span data-stu-id="56885-259">Complete Page Listing for Edit Movie Page (Updated for Layout)</span></span>

[!code-cshtml[Main](layouts/samples/sample17.cshtml)]

## <a name="coming-up-next"></a><span data-ttu-id="56885-260">下一步</span><span class="sxs-lookup"><span data-stu-id="56885-260">Coming Up Next</span></span>

<span data-ttu-id="56885-261">在下一個教學課程中，您將瞭解如何將您的網站發佈至網際網路，讓每個人都能看到它。</span><span class="sxs-lookup"><span data-stu-id="56885-261">In the next tutorial, you'll learn how to publish your site to the Internet so everyone can see it.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="56885-262">其他資源</span><span class="sxs-lookup"><span data-stu-id="56885-262">Additional Resources</span></span>

- <span data-ttu-id="56885-263">[建立一致的外觀](https://go.microsoft.com/fwlink/?LinkID=202891)：一篇文章，提供更多有關使用版面配置的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="56885-263">[Creating a Consistent Look](https://go.microsoft.com/fwlink/?LinkID=202891) — An article that provides some more detail on working with layouts.</span></span> <span data-ttu-id="56885-264">它也會說明如何將值傳遞至版面配置頁，以顯示或隱藏部分內容。</span><span class="sxs-lookup"><span data-stu-id="56885-264">It also describes how to pass a value to a layout page that shows or hides some of the content.</span></span>
- <span data-ttu-id="56885-265">[含有 Razor 的嵌套版面配置頁](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor)— Mike Brind 的 blog，是如何將版面配置頁的範例。</span><span class="sxs-lookup"><span data-stu-id="56885-265">[Nested Layout Pages with Razor](http://www.mikesdotnetting.com/Article/164/Nested-Layout-Pages-with-Razor) — Mike Brind blogs an example of how to nest layout pages.</span></span> <span data-ttu-id="56885-266">（包含頁面的下載）。</span><span class="sxs-lookup"><span data-stu-id="56885-266">(Includes a download of the pages.)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="56885-267">[上一頁](deleting-data.md)
> [下一頁](publishing.md)</span><span class="sxs-lookup"><span data-stu-id="56885-267">[Previous](deleting-data.md)
[Next](publishing.md)</span></span>
