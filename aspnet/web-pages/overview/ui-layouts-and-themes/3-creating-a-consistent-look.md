---
uid: web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
title: 在 ASP.NET Web Pages （Razor）網站中建立一致的版面配置 |Microsoft Docs
author: Rick-Anderson
description: 為了讓您更有效率地建立網站的網頁，您可以為網站建立可重複使用的內容區塊（例如頁首和頁尾），而您的 c 。
ms.author: riande
ms.date: 03/10/2014
ms.assetid: d7bd001b-6db2-4422-9b78-f3d08b743b00
msc.legacyurl: /web-pages/overview/ui-layouts-and-themes/3-creating-a-consistent-look
msc.type: authoredcontent
ms.openlocfilehash: 3f63ce68ae4c13970ac0df196167ace0b22b592c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78627446"
---
# <a name="creating-a-consistent-layout-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="8496e-103">在 ASP.NET Web Pages （Razor）網站中建立一致的版面配置</span><span class="sxs-lookup"><span data-stu-id="8496e-103">Creating a Consistent Layout in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="8496e-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="8496e-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="8496e-105">本文說明如何使用 ASP.NET Web Pages （Razor）網站中的版面配置頁來建立可重複使用的內容區塊（例如頁首和頁尾），並建立一致的外觀來尋找網站中的所有頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-105">This article explains how you can use layout pages in an ASP.NET Web Pages (Razor) website to create reusable blocks of content (like headers and footers) and to create a consistent look for all the pages in the site.</span></span>
> 
> <span data-ttu-id="8496e-106">**您將瞭解的內容：**</span><span class="sxs-lookup"><span data-stu-id="8496e-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="8496e-107">如何建立可重複使用的內容區塊，例如頁首和頁尾。</span><span class="sxs-lookup"><span data-stu-id="8496e-107">How to create reusable blocks of content like headers and footers.</span></span>
> - <span data-ttu-id="8496e-108">如何使用版面配置建立網站中所有頁面的一致外觀。</span><span class="sxs-lookup"><span data-stu-id="8496e-108">How to create a consistent look for all the pages in your site using a layout.</span></span>
> - <span data-ttu-id="8496e-109">如何在執行時間將資料傳遞至版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-109">How to pass data at run time to a layout page.</span></span>
> 
> <span data-ttu-id="8496e-110">以下是文章中引進的 ASP.NET 功能：</span><span class="sxs-lookup"><span data-stu-id="8496e-110">These are the ASP.NET features introduced in the article:</span></span>
> 
> - <span data-ttu-id="8496e-111">內容區塊，其為包含要插入多頁之 HTML 格式內容的檔案。</span><span class="sxs-lookup"><span data-stu-id="8496e-111">Content blocks, which are files that contain HTML-formatted content to be inserted in multiple pages.</span></span>
> - <span data-ttu-id="8496e-112">版面配置頁，也就是包含 HTML 格式內容的頁面，可由網站上的網頁共用。</span><span class="sxs-lookup"><span data-stu-id="8496e-112">Layout pages, which are pages that contain HTML-formatted content that can be shared by pages on the website.</span></span>
> - <span data-ttu-id="8496e-113">`RenderPage`、`RenderBody`和 `RenderSection` 方法，告訴 ASP.NET 要在何處插入頁面元素。</span><span class="sxs-lookup"><span data-stu-id="8496e-113">The `RenderPage`, `RenderBody`, and `RenderSection` methods, which tell ASP.NET where to insert page elements.</span></span>
> - <span data-ttu-id="8496e-114">`PageData` 字典，可讓您在內容區塊和版面配置頁之間共用資料。</span><span class="sxs-lookup"><span data-stu-id="8496e-114">The `PageData` dictionary that lets you share data between content blocks and layout pages.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="8496e-115">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="8496e-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="8496e-116">ASP.NET Web Pages （Razor）3</span><span class="sxs-lookup"><span data-stu-id="8496e-116">ASP.NET Web Pages (Razor) 3</span></span>
>   
> 
> <span data-ttu-id="8496e-117">本教學課程也適用于 ASP.NET Web Pages 2。</span><span class="sxs-lookup"><span data-stu-id="8496e-117">This tutorial also works with ASP.NET Web Pages 2.</span></span>

## <a name="about-layout-pages"></a><span data-ttu-id="8496e-118">關於版面配置頁</span><span class="sxs-lookup"><span data-stu-id="8496e-118">About Layout Pages</span></span>

<span data-ttu-id="8496e-119">許多網站都有顯示在每個頁面上的內容，例如頁首和頁尾，或可告知使用者已登入的方塊。</span><span class="sxs-lookup"><span data-stu-id="8496e-119">Many websites have content that's displayed on every page, like a header and footer, or a box that tells users that they're logged in.</span></span> <span data-ttu-id="8496e-120">ASP.NET 可讓您建立具有內容區塊的個別檔案，其中包含文字、標記和程式碼，就像一般的網頁一樣。</span><span class="sxs-lookup"><span data-stu-id="8496e-120">ASP.NET lets you create a separate file with a content block that can contain text, markup, and code, just like a regular web page.</span></span> <span data-ttu-id="8496e-121">接著，您可以將內容區塊插入網站上您想要顯示資訊的其他頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-121">You can then insert the content block in other pages on the site where you want the information to appear.</span></span> <span data-ttu-id="8496e-122">如此一來，您就不需要將相同的內容複寫並貼到每個頁面中。</span><span class="sxs-lookup"><span data-stu-id="8496e-122">That way you don't have to copy and paste the same content into every page.</span></span> <span data-ttu-id="8496e-123">建立這類常見的內容也能讓您更輕鬆地更新您的網站。</span><span class="sxs-lookup"><span data-stu-id="8496e-123">Creating common content like this also makes it easier to update your site.</span></span> <span data-ttu-id="8496e-124">如果您需要變更內容，您可以只更新單一檔案，然後變更會反映在插入內容的所有位置。</span><span class="sxs-lookup"><span data-stu-id="8496e-124">If you need to change the content, you can just update a single file, and the changes are then reflected everywhere the content has been inserted.</span></span>

<span data-ttu-id="8496e-125">下圖顯示內容區塊的工作方式。</span><span class="sxs-lookup"><span data-stu-id="8496e-125">The following diagram shows how content blocks work.</span></span> <span data-ttu-id="8496e-126">當瀏覽器向 web 伺服器要求頁面時，ASP.NET 會在主頁面中呼叫 `RenderPage` 方法的位置插入內容區塊。</span><span class="sxs-lookup"><span data-stu-id="8496e-126">When a browser requests a page from the web server, ASP.NET inserts the content blocks at the point where the `RenderPage` method is called in the main page.</span></span> <span data-ttu-id="8496e-127">[完成（已合併）] 頁面接著會傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8496e-127">The finished (merged) page is then sent to the browser.</span></span>

![概念圖顯示 RenderPage 方法如何在目前的頁面中插入參考的頁面。](3-creating-a-consistent-look/_static/image1.jpg)

<span data-ttu-id="8496e-129">在此程式中，您將建立一個頁面，參考位於不同檔案中的兩個內容區塊（頁首和頁尾）。</span><span class="sxs-lookup"><span data-stu-id="8496e-129">In this procedure, you'll create a page that references two content blocks (a header and a footer) that are located in separate files.</span></span> <span data-ttu-id="8496e-130">您可以在網站的任何頁面中使用這些相同的內容區塊。</span><span class="sxs-lookup"><span data-stu-id="8496e-130">You can use these same content blocks in any page in your site.</span></span> <span data-ttu-id="8496e-131">當您完成時，您會看到如下的頁面：</span><span class="sxs-lookup"><span data-stu-id="8496e-131">When you're done, you'll get a page like this:</span></span>

![螢幕擷取畫面：顯示瀏覽器中的頁面，其結果是執行包含 RenderPage 方法呼叫的頁面。](3-creating-a-consistent-look/_static/image2.png)

1. <span data-ttu-id="8496e-133">在網站的根資料夾中，建立名為*Index. cshtml*的檔案。</span><span class="sxs-lookup"><span data-stu-id="8496e-133">In the root folder of your website, create a file named *Index.cshtml*.</span></span>
2. <span data-ttu-id="8496e-134">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="8496e-134">Replace the existing markup with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample1.html)]
3. <span data-ttu-id="8496e-135">在根資料夾中，建立名為*Shared*的資料夾。</span><span class="sxs-lookup"><span data-stu-id="8496e-135">In the root folder, create a folder named *Shared*.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8496e-136">在名為*shared*的資料夾中，儲存網頁之間共用的檔案是常見的作法。</span><span class="sxs-lookup"><span data-stu-id="8496e-136">It's common practice to store files that are shared among web pages in a folder named *Shared*.</span></span>
4. <span data-ttu-id="8496e-137">在*共用*資料夾中，建立名為 *\_標頭 cshtml*的檔案。</span><span class="sxs-lookup"><span data-stu-id="8496e-137">In the *Shared* folder, create a file named *\_Header.cshtml*.</span></span>
5. <span data-ttu-id="8496e-138">將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-138">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample2.html)]

    <span data-ttu-id="8496e-139">請注意，檔案名是 *\_標頭. cshtml*，加底線（\_）做為前置詞。</span><span class="sxs-lookup"><span data-stu-id="8496e-139">Notice that the file name is *\_Header.cshtml*, with an underscore (\_) as a prefix.</span></span> <span data-ttu-id="8496e-140">如果 ASP.NET 的名稱開頭為底線，則不會將頁面傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8496e-140">ASP.NET won't send a page to the browser if its name starts with an underscore.</span></span> <span data-ttu-id="8496e-141">這可防止使用者直接要求（不小心或其他）這些頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-141">This prevents people from requesting (inadvertently or otherwise) these pages directly.</span></span> <span data-ttu-id="8496e-142">使用底線來命名含有內容區塊的頁面，是個不錯的主意，因為您不想讓使用者能夠要求這些頁面&#8212; ，嚴格地插入其他頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-142">It's a good idea to use an underscore to name pages that have content blocks in them, because you don't really want users to be able to request these pages &#8212; they exist strictly to be inserted into other pages.</span></span>
6. <span data-ttu-id="8496e-143">在*共用*資料夾中，建立名為 *\_頁尾. cshtml*的檔案，並將內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-143">In the *Shared* folder, create a file named *\_Footer.cshtml* and replace the content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample3.html)]
7. <span data-ttu-id="8496e-144">在 [ *Index. cshtml* ] 頁面中，新增兩個對 `RenderPage` 方法的呼叫，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8496e-144">In the *Index.cshtml* page, add two calls to the `RenderPage` method, as shown here:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample4.html)]

    <span data-ttu-id="8496e-145">這會顯示如何將內容區塊插入網頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-145">This shows how to insert a content block into a web page.</span></span> <span data-ttu-id="8496e-146">您可以呼叫 `RenderPage` 方法，並將您想要在該點插入其內容的檔案名傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="8496e-146">You call the `RenderPage` method and pass it the name of the file whose contents you want to insert at that point.</span></span> <span data-ttu-id="8496e-147">在這裡，您要將 *\_標頭. cshtml*和\_頁尾 *. cshtml*檔案的內容插入到*Index.* cshtml 檔案中。</span><span class="sxs-lookup"><span data-stu-id="8496e-147">Here, you're inserting the contents of the *\_Header.cshtml* and *\_Footer.cshtml* files into the *Index.cshtml* file.</span></span>
8. <span data-ttu-id="8496e-148">在瀏覽器中執行 [ *Index. cshtml* ] 頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-148">Run the *Index.cshtml* page in a browser.</span></span> <span data-ttu-id="8496e-149">（在 WebMatrix 的 [檔案 **] 工作區**中，以滑鼠右鍵按一下檔案，然後選取 [**在瀏覽器中啟動**]。）</span><span class="sxs-lookup"><span data-stu-id="8496e-149">(In WebMatrix, in the **Files** workspace, right-click the file and then select **Launch in browser**.)</span></span>
9. <span data-ttu-id="8496e-150">在瀏覽器中，查看頁面來源。</span><span class="sxs-lookup"><span data-stu-id="8496e-150">In the browser, view the page source.</span></span> <span data-ttu-id="8496e-151">（例如，在 Internet Explorer 中，以滑鼠右鍵按一下頁面，然後按一下 [ **View Source**]）。</span><span class="sxs-lookup"><span data-stu-id="8496e-151">(For example, in Internet Explorer, right-click the page and then click **View Source**.)</span></span>

    <span data-ttu-id="8496e-152">這可讓您查看傳送至瀏覽器的網頁標記，其結合了索引頁標記與內容區塊。</span><span class="sxs-lookup"><span data-stu-id="8496e-152">This lets you see the web page markup that's sent to the browser, which combines the index page markup with the content blocks.</span></span> <span data-ttu-id="8496e-153">下列範例會顯示針對*Index*所呈現的頁面來源。</span><span class="sxs-lookup"><span data-stu-id="8496e-153">The following example shows the page source that's rendered for *Index.cshtml*.</span></span> <span data-ttu-id="8496e-154">您插入到*Index*中的 `RenderPage` 呼叫已被標頭和頁尾檔案的實際內容所取代。</span><span class="sxs-lookup"><span data-stu-id="8496e-154">The calls to `RenderPage` that you inserted into *Index.cshtml* have been replaced with the actual contents of the header and footer files.</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample5.html)]

## <a name="creating-a-consistent-look-using-layout-pages"></a><span data-ttu-id="8496e-155">使用版面配置頁建立一致的外觀</span><span class="sxs-lookup"><span data-stu-id="8496e-155">Creating a Consistent Look Using Layout Pages</span></span>

<span data-ttu-id="8496e-156">到目前為止，您已經看過在多個頁面上包含相同的內容是很容易的。</span><span class="sxs-lookup"><span data-stu-id="8496e-156">So far you've seen that it's easy to include the same content on multiple pages.</span></span> <span data-ttu-id="8496e-157">建立一致的網站外觀的更結構化方法，就是使用版面配置頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-157">A more structured approach to creating a consistent look for a site is to use layout pages.</span></span> <span data-ttu-id="8496e-158">版面配置頁會定義網頁的結構，但不包含任何實際內容。</span><span class="sxs-lookup"><span data-stu-id="8496e-158">A layout page defines the structure of a web page, but doesn't contain any actual content.</span></span> <span data-ttu-id="8496e-159">建立版面配置頁之後，您可以建立包含內容的網頁，然後將其連結至版面配置頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-159">After you've created a layout page, you can create web pages that contain the content and then link them to the layout page.</span></span> <span data-ttu-id="8496e-160">顯示這些頁面時，將會根據版面配置頁面將其格式化。</span><span class="sxs-lookup"><span data-stu-id="8496e-160">When these pages are displayed, they'll be formatted according to the layout page.</span></span> <span data-ttu-id="8496e-161">（在這種情況下，版面配置頁面會作為在其他頁面中定義之內容的範本類型）。</span><span class="sxs-lookup"><span data-stu-id="8496e-161">(In this sense, a layout page acts as a kind of template for content that's defined in other pages.)</span></span>

<span data-ttu-id="8496e-162">版面配置頁與任何 HTML 網頁一樣，不同之處在于它包含對 `RenderBody` 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="8496e-162">The layout page is just like any HTML page, except that it contains a call to the `RenderBody` method.</span></span> <span data-ttu-id="8496e-163">[版面配置] 頁面中 `RenderBody` 方法的位置，會決定要包含內容頁面中之資訊的位置。</span><span class="sxs-lookup"><span data-stu-id="8496e-163">The position of the `RenderBody` method in the layout page determines where the information from the content page will be included.</span></span>

<span data-ttu-id="8496e-164">下圖顯示如何在執行時間結合內容頁和版面配置頁，以產生完成的網頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-164">The following diagram shows how content pages and layout pages are combined at run time to produce the finished web page.</span></span> <span data-ttu-id="8496e-165">瀏覽器要求內容頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-165">The browser requests a content page.</span></span> <span data-ttu-id="8496e-166">[內容] 頁面中有程式碼，可指定要用於頁面結構的版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-166">The content page has code in it that specifies the layout page to use for the page's structure.</span></span> <span data-ttu-id="8496e-167">在 [版面配置] 頁面中，會將內容插入呼叫 `RenderBody` 方法的位置。</span><span class="sxs-lookup"><span data-stu-id="8496e-167">In the layout page, the content is inserted at the point where the `RenderBody` method is called.</span></span> <span data-ttu-id="8496e-168">內容區塊也可以藉由呼叫 `RenderPage` 方法（以您在上一節中執行的方式），插入至版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-168">Content blocks can also be inserted into the layout page by calling the `RenderPage` method, the way you did in the previous section.</span></span> <span data-ttu-id="8496e-169">網頁完成時，會傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8496e-169">When the web page is complete, it's sent to the browser.</span></span>

![螢幕擷取畫面：顯示瀏覽器中的頁面，其結果是執行包含 RenderBody 方法呼叫的頁面。](3-creating-a-consistent-look/_static/image3.jpg)

<span data-ttu-id="8496e-171">下列程式示範如何建立版面配置頁，並將內容頁面連結至該頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-171">The following procedure shows how to create a layout page and link content pages to it.</span></span>

1. <span data-ttu-id="8496e-172">在您網站的*共用*資料夾中，建立名為 *\_layout1.xml*的檔案。</span><span class="sxs-lookup"><span data-stu-id="8496e-172">In the *Shared* folder of your website, create a file named *\_Layout1.cshtml*.</span></span>
2. <span data-ttu-id="8496e-173">將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-173">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample6.html)]

    <span data-ttu-id="8496e-174">您可以使用版面配置頁中的 `RenderPage` 方法來插入內容區塊。</span><span class="sxs-lookup"><span data-stu-id="8496e-174">You use the `RenderPage` method in a layout page to insert content blocks.</span></span> <span data-ttu-id="8496e-175">版面配置頁只能包含一個 `RenderBody` 方法的呼叫。</span><span class="sxs-lookup"><span data-stu-id="8496e-175">A layout page can contain only one call to the `RenderBody` method.</span></span>
3. <span data-ttu-id="8496e-176">在*共用*資料夾中，建立名為 *\_h 2*的檔案，並將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-176">In the *Shared* folder, create a file named *\_Header2.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample7.html)]
4. <span data-ttu-id="8496e-177">在根資料夾中，建立新的資料夾，並將其命名為*樣式*。</span><span class="sxs-lookup"><span data-stu-id="8496e-177">In the root folder, create a new folder and name it *Styles*.</span></span>
5. <span data-ttu-id="8496e-178">在 [*樣式*] 資料夾中，建立名為*Site .css*的檔案，並新增下列樣式定義：</span><span class="sxs-lookup"><span data-stu-id="8496e-178">In the *Styles* folder, create a file named *Site.css* and add the following style definitions:</span></span>

    [!code-css[Main](3-creating-a-consistent-look/samples/sample8.css)]

    <span data-ttu-id="8496e-179">這些樣式定義僅供示範如何搭配版面配置頁使用樣式表單。</span><span class="sxs-lookup"><span data-stu-id="8496e-179">These style definitions are here only to show how style sheets can be used with layout pages.</span></span> <span data-ttu-id="8496e-180">如有需要，您可以為這些元素定義自己的樣式。</span><span class="sxs-lookup"><span data-stu-id="8496e-180">If you want, you can define your own styles for these elements.</span></span>
6. <span data-ttu-id="8496e-181">在根資料夾中，建立名為*Content1*的檔案，並將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-181">In the root folder, create a file named *Content1.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample9.cshtml)]

    <span data-ttu-id="8496e-182">這是將使用版面配置頁的頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-182">This is a page that will use a layout page.</span></span> <span data-ttu-id="8496e-183">頁面頂端的程式碼區塊會指出要用來格式化此內容的版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-183">The code block at the top of the page indicates which layout page to use to format this content.</span></span>
7. <span data-ttu-id="8496e-184">在瀏覽器中執行*Content1。*</span><span class="sxs-lookup"><span data-stu-id="8496e-184">Run *Content1.cshtml* in a browser.</span></span> <span data-ttu-id="8496e-185">呈現的頁面會使用 *\_layout1.xml*中定義的格式和樣式表單，以及*Content1*中定義的文字（content）。</span><span class="sxs-lookup"><span data-stu-id="8496e-185">The rendered page uses the format and style sheet defined in *\_Layout1.cshtml* and the text (content) defined in *Content1.cshtml*.</span></span>

    ![[影像]](3-creating-a-consistent-look/_static/image4.png)

    <span data-ttu-id="8496e-187">您可以重複步驟6，建立可共用相同版面配置頁的其他內容頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-187">You can repeat step 6 to create additional content pages that can then share the same layout page.</span></span>

    > [!NOTE]
    > <span data-ttu-id="8496e-188">您可以設定您的網站，讓您可以針對資料夾中的所有內容頁面自動使用相同的版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-188">You can set up your site so that you can automatically use the same layout page for all the content pages in a folder.</span></span> <span data-ttu-id="8496e-189">如需詳細資訊，請參閱[針對 ASP.NET Web Pages 自訂全網站行為](https://go.microsoft.com/fwlink/?LinkId=202906)。</span><span class="sxs-lookup"><span data-stu-id="8496e-189">For details, see [Customizing Site-Wide Behavior for ASP.NET Web Pages](https://go.microsoft.com/fwlink/?LinkId=202906).</span></span>

## <a name="designing-layout-pages-that-have-multiple-content-sections"></a><span data-ttu-id="8496e-190">設計具有多個內容區段的版面配置頁</span><span class="sxs-lookup"><span data-stu-id="8496e-190">Designing Layout Pages That Have Multiple Content Sections</span></span>

<span data-ttu-id="8496e-191">內容頁面可以有多個區段，如果您想要使用具有可替換內容的多個區域的版面配置，這會很有用。</span><span class="sxs-lookup"><span data-stu-id="8496e-191">A content page can have multiple sections, which is useful if you want to use layouts that have multiple areas with replaceable content.</span></span> <span data-ttu-id="8496e-192">在 [內容] 頁面中，您可以為每個區段提供唯一的名稱。</span><span class="sxs-lookup"><span data-stu-id="8496e-192">In the content page, you give each section a unique name.</span></span> <span data-ttu-id="8496e-193">（預設區段會保留為未命名）。在 [版面配置] 頁面中，您可以新增 `RenderBody` 方法，以指定應出現未命名（預設）區段的位置。</span><span class="sxs-lookup"><span data-stu-id="8496e-193">(The default section is left unnamed.) In the layout page, you add a `RenderBody` method to specify where the unnamed (default) section should appear.</span></span> <span data-ttu-id="8496e-194">接著，您會新增個別的 `RenderSection` 方法，以便個別轉譯命名的區段。</span><span class="sxs-lookup"><span data-stu-id="8496e-194">You then add separate `RenderSection` methods in order to render named sections individually.</span></span>

<span data-ttu-id="8496e-195">下圖顯示 ASP.NET 如何處理劃分成多個區段的內容。</span><span class="sxs-lookup"><span data-stu-id="8496e-195">The following diagram shows how ASP.NET handles content that's divided into multiple sections.</span></span> <span data-ttu-id="8496e-196">每個命名的區段都包含在 [內容] 頁面的區段區塊中。</span><span class="sxs-lookup"><span data-stu-id="8496e-196">Each named section is contained in a section block in the content page.</span></span> <span data-ttu-id="8496e-197">（它們的名稱是 `Header`，在範例中 `List`）。架構會在呼叫 `RenderSection` 方法的位置，將內容區段插入至版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-197">(They're named `Header` and `List` in the example.) The framework inserts content section into the layout page at the point where the `RenderSection` method is called.</span></span> <span data-ttu-id="8496e-198">未命名的（預設）區段會插入呼叫 `RenderBody` 方法的位置，如先前所見。</span><span class="sxs-lookup"><span data-stu-id="8496e-198">The unnamed (default) section is inserted at the point where the `RenderBody` method is called, as you saw earlier.</span></span>

![概念圖顯示 RenderSection 方法如何將參考區段插入目前的頁面。](3-creating-a-consistent-look/_static/image5.jpg)

<span data-ttu-id="8496e-200">此程式說明如何建立具有多個內容區段的內容頁面，以及如何使用支援多個內容區段的版面配置頁來呈現它。</span><span class="sxs-lookup"><span data-stu-id="8496e-200">This procedure shows how to create a content page that has multiple content sections and how to render it using a layout page that supports multiple content sections.</span></span>

1. <span data-ttu-id="8496e-201">在*共用*資料夾中，建立名為 *\_Layout2*的檔案。</span><span class="sxs-lookup"><span data-stu-id="8496e-201">In the *Shared* folder, create a file named *\_Layout2.cshtml*.</span></span>
2. <span data-ttu-id="8496e-202">將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-202">Replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample10.html)]

    <span data-ttu-id="8496e-203">您可以使用 `RenderSection` 方法來呈現標頭和清單區段。</span><span class="sxs-lookup"><span data-stu-id="8496e-203">You use the `RenderSection` method to render both the header and list sections.</span></span>
3. <span data-ttu-id="8496e-204">在根資料夾中，建立名為*Content2*的檔案，並將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-204">In the root folder, create a file named *Content2.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample11.cshtml)]

    <span data-ttu-id="8496e-205">此內容頁面會在頁面頂端包含程式碼區塊。</span><span class="sxs-lookup"><span data-stu-id="8496e-205">This content page contains a code block at the top of the page.</span></span> <span data-ttu-id="8496e-206">每個命名的區段都包含在區段區塊中。</span><span class="sxs-lookup"><span data-stu-id="8496e-206">Each named section is contained in a section block.</span></span> <span data-ttu-id="8496e-207">頁面的其餘部分包含預設（未命名）內容區段。</span><span class="sxs-lookup"><span data-stu-id="8496e-207">The rest of the page contains the default (unnamed) content section.</span></span>
4. <span data-ttu-id="8496e-208">在瀏覽器中執行*Content2。*</span><span class="sxs-lookup"><span data-stu-id="8496e-208">Run *Content2.cshtml* in a browser.</span></span>

    ![螢幕擷取畫面：顯示瀏覽器中的頁面，其結果是執行包含 RenderSection 方法呼叫的頁面。](3-creating-a-consistent-look/_static/image6.png)

## <a name="making-content-sections-optional"></a><span data-ttu-id="8496e-210">將內容區段設為選擇性</span><span class="sxs-lookup"><span data-stu-id="8496e-210">Making Content Sections Optional</span></span>

<span data-ttu-id="8496e-211">一般來說，您在內容頁面中建立的區段必須符合版面配置頁面中所定義的區段。</span><span class="sxs-lookup"><span data-stu-id="8496e-211">Normally, the sections that you create in a content page have to match sections that are defined in the layout page.</span></span> <span data-ttu-id="8496e-212">如果發生下列任何一種情況，您可能會收到錯誤：</span><span class="sxs-lookup"><span data-stu-id="8496e-212">You can get errors if any of the following occur:</span></span>

- <span data-ttu-id="8496e-213">[內容] 頁面包含 [版面配置] 頁面中沒有對應區段的區段。</span><span class="sxs-lookup"><span data-stu-id="8496e-213">The content page contains a section that has no corresponding section in the layout page.</span></span>
- <span data-ttu-id="8496e-214">版面配置頁包含沒有內容的區段。</span><span class="sxs-lookup"><span data-stu-id="8496e-214">The layout page contains a section for which there's no content.</span></span>
- <span data-ttu-id="8496e-215">版面配置頁包含嘗試多次轉譯相同區段的方法呼叫。</span><span class="sxs-lookup"><span data-stu-id="8496e-215">The layout page includes method calls that try to render the same section more than once.</span></span>

<span data-ttu-id="8496e-216">不過，您可以藉由在版面配置頁中宣告區段為選擇性，來覆寫已命名區段的這個行為。</span><span class="sxs-lookup"><span data-stu-id="8496e-216">However, you can override this behavior for a named section by declaring the section to be optional in the layout page.</span></span> <span data-ttu-id="8496e-217">這可讓您定義多個可以共用版面配置頁的內容頁，但可能會有或沒有特定區段的內容。</span><span class="sxs-lookup"><span data-stu-id="8496e-217">This lets you define multiple content pages that can share a layout page but that might or might not have content for a specific section.</span></span>

1. <span data-ttu-id="8496e-218">開啟*Content2* ，並移除下列區段：</span><span class="sxs-lookup"><span data-stu-id="8496e-218">Open *Content2.cshtml* and remove the following section:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample12.cshtml)]
2. <span data-ttu-id="8496e-219">儲存頁面，然後在瀏覽器中執行。</span><span class="sxs-lookup"><span data-stu-id="8496e-219">Save the page and then run it in a browser.</span></span> <span data-ttu-id="8496e-220">會顯示錯誤訊息，因為 [內容] 頁面不會提供版面配置頁中所定義之區段的內容，也就是標頭區段。</span><span class="sxs-lookup"><span data-stu-id="8496e-220">An error message is displayed, because the content page doesn't provide content for a section defined in the layout page, namely the header section.</span></span>

    ![螢幕擷取畫面：顯示當您執行呼叫 RenderSection 方法但未提供對應區段的頁面時，所發生的錯誤。](3-creating-a-consistent-look/_static/image7.png)
3. <span data-ttu-id="8496e-222">在*共用*資料夾中，開啟 [ *\_Layout2* ] 頁面，並取代這一行：</span><span class="sxs-lookup"><span data-stu-id="8496e-222">In the *Shared* folder, open the *\_Layout2.cshtml* page and replace this line:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample13.js)]

    <span data-ttu-id="8496e-223">取代為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="8496e-223">with the following code:</span></span>

    [!code-javascript[Main](3-creating-a-consistent-look/samples/sample14.js)]

    <span data-ttu-id="8496e-224">或者，您可以使用下列程式碼區塊來取代前一行程式碼，這樣會產生相同的結果：</span><span class="sxs-lookup"><span data-stu-id="8496e-224">As an alternative, you could replace the previous line of code with the following code block, which produces the same results:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample15.cshtml)]
4. <span data-ttu-id="8496e-225">再次執行瀏覽器中的*Content2*頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-225">Run the *Content2.cshtml* page in a browser again.</span></span> <span data-ttu-id="8496e-226">（如果您仍然在瀏覽器中開啟此頁面，您可以直接重新整理它。）這次會顯示頁面，而不會發生錯誤，即使沒有標頭也一樣。</span><span class="sxs-lookup"><span data-stu-id="8496e-226">(If you still have this page open in the browser, you can just refresh it.) This time the page is displayed with no error, even though it has no header.</span></span>

## <a name="passing-data-to-layout-pages"></a><span data-ttu-id="8496e-227">將資料傳遞至版面配置頁</span><span class="sxs-lookup"><span data-stu-id="8496e-227">Passing Data to Layout Pages</span></span>

<span data-ttu-id="8496e-228">您可能會在 [內容] 頁面中定義您需要在版面配置頁面中參考的資料。</span><span class="sxs-lookup"><span data-stu-id="8496e-228">You might have data defined in the content page that you need to refer to in a layout page.</span></span> <span data-ttu-id="8496e-229">若是如此，您必須將資料從 [內容] 頁面傳遞至 [版面配置] 頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-229">If so, you need to pass the data from the content page to the layout page.</span></span> <span data-ttu-id="8496e-230">例如，您可能想要顯示使用者的登入狀態，或者您可能想要根據使用者輸入來顯示或隱藏內容區域。</span><span class="sxs-lookup"><span data-stu-id="8496e-230">For example, you might want to display the login status of a user, or you might want to show or hide content areas based on user input.</span></span>

<span data-ttu-id="8496e-231">若要將資料從內容頁面傳遞至版面配置頁，您可以將值放入 [內容] 頁面的 [`PageData`] 屬性中。</span><span class="sxs-lookup"><span data-stu-id="8496e-231">To pass data from a content page to a layout page, you can put values into the `PageData` property of the content page.</span></span> <span data-ttu-id="8496e-232">`PageData` 屬性是名稱/值組的集合，其中包含您要在頁面之間傳遞的資料。</span><span class="sxs-lookup"><span data-stu-id="8496e-232">The `PageData` property is a collection of name/value pairs that hold the data that you want to pass between pages.</span></span> <span data-ttu-id="8496e-233">在 [版面配置] 頁面中，您可以從 [`PageData`] 屬性讀取值。</span><span class="sxs-lookup"><span data-stu-id="8496e-233">In the layout page, you can then read values out of the `PageData` property.</span></span>

<span data-ttu-id="8496e-234">以下是另一個圖表。</span><span class="sxs-lookup"><span data-stu-id="8496e-234">Here's another diagram.</span></span> <span data-ttu-id="8496e-235">這個範例會示範 ASP.NET 如何使用 `PageData` 屬性，將值從內容頁傳遞至版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-235">This one shows how ASP.NET can use the `PageData` property to pass values from a content page to the layout page.</span></span> <span data-ttu-id="8496e-236">當 ASP.NET 開始建立網頁時，它會建立 `PageData` 集合。</span><span class="sxs-lookup"><span data-stu-id="8496e-236">When ASP.NET begins building the web page, it creates the `PageData` collection.</span></span> <span data-ttu-id="8496e-237">在 [內容] 頁面中，您可以撰寫程式碼，將資料放入 `PageData` 集合中。</span><span class="sxs-lookup"><span data-stu-id="8496e-237">In the content page, you write code to put data in the `PageData` collection.</span></span> <span data-ttu-id="8496e-238">`PageData` 集合中的值也可以由內容頁面中的其他區段或其他內容區塊來存取。</span><span class="sxs-lookup"><span data-stu-id="8496e-238">Values in the `PageData` collection can also be accessed by other sections in the content page or by additional content blocks.</span></span>

![概念圖，顯示內容頁面如何填入 PageData 字典，並將該資訊傳遞至版面配置頁。](3-creating-a-consistent-look/_static/image8.jpg)

<span data-ttu-id="8496e-240">下列程式顯示如何將資料從內容頁面傳遞至版面配置頁。</span><span class="sxs-lookup"><span data-stu-id="8496e-240">The following procedure shows how to pass data from a content page to a layout page.</span></span> <span data-ttu-id="8496e-241">當頁面執行時，它會顯示一個按鈕，讓使用者隱藏或顯示在版面配置頁中定義的清單。</span><span class="sxs-lookup"><span data-stu-id="8496e-241">When the page runs, it displays a button that lets the user hide or show a list that's defined in the layout page.</span></span> <span data-ttu-id="8496e-242">當使用者按一下按鈕時，它會在 `PageData` 屬性中設定 true/false （布林值）值。</span><span class="sxs-lookup"><span data-stu-id="8496e-242">When users click the button, it sets a true/false (Boolean) value in the `PageData` property.</span></span> <span data-ttu-id="8496e-243">版面配置頁會讀取該值，如果是 false，則會隱藏清單。</span><span class="sxs-lookup"><span data-stu-id="8496e-243">The layout page reads that value, and if it's false, hides the list.</span></span> <span data-ttu-id="8496e-244">此值也會在 [內容] 頁面中用來判斷是否要顯示 [**隱藏清單**] 按鈕或 [**顯示清單**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8496e-244">The value is also used in the content page to determine whether to display the **Hide List** button or the **Show List** button.</span></span>

![[影像]](3-creating-a-consistent-look/_static/image9.jpg)

1. <span data-ttu-id="8496e-246">在根資料夾中，建立名為*Content3*的檔案，並將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-246">In the root folder, create a file named *Content3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample16.cshtml)]

    <span data-ttu-id="8496e-247">此程式碼會在 `PageData` 屬性&#8212;中儲存兩個數據片段，此網頁的標題為 true 或 false，以指定是否要顯示清單。</span><span class="sxs-lookup"><span data-stu-id="8496e-247">The code stores two pieces of data in the `PageData` property &#8212; the title of the web page and true or false to specify whether to display a list.</span></span>

    <span data-ttu-id="8496e-248">請注意，ASP.NET 可讓您使用程式碼區塊，有條件地將 HTML 標籤放入頁面。</span><span class="sxs-lookup"><span data-stu-id="8496e-248">Notice that ASP.NET lets you put HTML markup into the page conditionally using a code block.</span></span> <span data-ttu-id="8496e-249">例如，頁面主體中的 `if/else` 區塊會根據 `PageData["ShowList"]` 是否設定為 true 來決定要顯示的表單。</span><span class="sxs-lookup"><span data-stu-id="8496e-249">For example, the `if/else` block in the body of the page determines which form to display depending on whether `PageData["ShowList"]` is set to true.</span></span>
2. <span data-ttu-id="8496e-250">在*共用*資料夾中，建立名為 *\_Layout3*的檔案，並將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-250">In the *Shared* folder, create a file named *\_Layout3.cshtml* and replace any existing content with the following:</span></span>

    [!code-cshtml[Main](3-creating-a-consistent-look/samples/sample17.cshtml)]

    <span data-ttu-id="8496e-251">版面配置頁在 `<title>` 元素中包含一個運算式，可從 `PageData` 屬性取得標題值。</span><span class="sxs-lookup"><span data-stu-id="8496e-251">The layout page includes an expression in the `<title>` element that gets the title value from the `PageData` property.</span></span> <span data-ttu-id="8496e-252">它也會使用 `PageData` 屬性的 `ShowList` 值，來判斷是否要顯示清單內容區塊。</span><span class="sxs-lookup"><span data-stu-id="8496e-252">It also uses the `ShowList` value of the `PageData` property to determine whether to display the list content block.</span></span>
3. <span data-ttu-id="8496e-253">在*共用*資料夾中，建立名為 *\_清單*的檔案，並將任何現有的內容取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="8496e-253">In the *Shared* folder, create a file named *\_List.cshtml* and replace any existing content with the following:</span></span>

    [!code-html[Main](3-creating-a-consistent-look/samples/sample18.html)]
4. <span data-ttu-id="8496e-254">在瀏覽器中執行*Content3。*</span><span class="sxs-lookup"><span data-stu-id="8496e-254">Run the *Content3.cshtml* page in a browser.</span></span> <span data-ttu-id="8496e-255">頁面會顯示在頁面左側的清單中，並在底部顯示 [**隱藏清單**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8496e-255">The page is displayed with the list visible on the left side of the page and a **Hide List** button at the bottom.</span></span>

    ![螢幕擷取畫面，其中顯示包含清單的頁面和顯示 [隱藏清單] 的按鈕。](3-creating-a-consistent-look/_static/image10.png)
5. <span data-ttu-id="8496e-257">按一下 [**隱藏清單**]。</span><span class="sxs-lookup"><span data-stu-id="8496e-257">Click **Hide List**.</span></span> <span data-ttu-id="8496e-258">清單會消失，且按鈕會變更為 [**顯示清單**]。</span><span class="sxs-lookup"><span data-stu-id="8496e-258">The list disappears and the button changes to **Show List**.</span></span>

    ![螢幕擷取畫面：顯示不包含清單的頁面，以及指出 [顯示清單] 的按鈕。](3-creating-a-consistent-look/_static/image11.png)
6. <span data-ttu-id="8496e-260">按一下 [**顯示清單**] 按鈕，清單就會再次顯示。</span><span class="sxs-lookup"><span data-stu-id="8496e-260">Click the **Show List** button, and the list is displayed again.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="8496e-261">其他資源</span><span class="sxs-lookup"><span data-stu-id="8496e-261">Additional Resources</span></span>

[<span data-ttu-id="8496e-262">針對 ASP.NET Web Pages 自訂全網站行為</span><span class="sxs-lookup"><span data-stu-id="8496e-262">Customizing Site-Wide Behavior for ASP.NET Web Pages</span></span>](https://go.microsoft.com/fwlink/?LinkId=202906)
