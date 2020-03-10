---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
title: 加入視圖（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: d3633f64-5d3c-45c9-ae4b-cb1563e3739f
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: fa200935d83bb26c07b302449a6eba6fd67b5322
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540422"
---
# <a name="adding-a-view-vb"></a><span data-ttu-id="8dad4-103">新增檢視 (VB)</span><span class="sxs-lookup"><span data-stu-id="8dad4-103">Adding a View (VB)</span></span>

<span data-ttu-id="8dad4-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="8dad4-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="8dad4-105">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="8dad4-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="8dad4-106">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="8dad4-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="8dad4-107">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="8dad4-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="8dad4-108">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="8dad4-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="8dad4-109">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="8dad4-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="8dad4-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="8dad4-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="8dad4-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="8dad4-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="8dad4-112">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="8dad4-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="8dad4-113">本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="8dad4-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="8dad4-114">[下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="8dad4-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="8dad4-115">如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/adding-a-view.md)。</span><span class="sxs-lookup"><span data-stu-id="8dad4-115">If you prefer C#, switch to the [C# version](../cs/adding-a-view.md) of this tutorial.</span></span>

<span data-ttu-id="8dad4-116">在本節中，我們將修改 `HelloWorldController` 類別，以使用視圖範本檔案，將產生 HTML 回應的程式完全封裝至用戶端。</span><span class="sxs-lookup"><span data-stu-id="8dad4-116">In this section we're going to modify the `HelloWorldController` class to use a view template file to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="8dad4-117">讓我們從在 `HelloWorldController` 類別中使用具有 `Index` 方法的視圖範本開始著手。</span><span class="sxs-lookup"><span data-stu-id="8dad4-117">Let's start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="8dad4-118">目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。</span><span class="sxs-lookup"><span data-stu-id="8dad4-118">Currently the `Index` method returns a string with a message that is hard-coded within the controller class.</span></span> <span data-ttu-id="8dad4-119">變更 `Index` 方法，以傳回 `View` 物件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8dad4-119">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-vb[Main](adding-a-view/samples/sample1.vb)]

<span data-ttu-id="8dad4-120">現在讓我們將一個 view 範本加入至我們可以使用 `Index` 方法叫用的專案。</span><span class="sxs-lookup"><span data-stu-id="8dad4-120">Let's now add a view template to our project that we can invoke with the `Index` method.</span></span> <span data-ttu-id="8dad4-121">若要這麼做，請以滑鼠右鍵按一下 `Index` 方法，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="8dad4-121">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

<span data-ttu-id="8dad4-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="8dad4-122">[![IndexAddView](adding-a-view/_static/image2.png "IndexAddView")](adding-a-view/_static/image1.png)</span></span>

<span data-ttu-id="8dad4-123">[**加入視圖**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="8dad4-123">The **Add View** dialog box appears.</span></span> <span data-ttu-id="8dad4-124">保留預設專案，然後按一下 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="8dad4-124">Leave the default entries and click the **Add** button.</span></span>

<span data-ttu-id="8dad4-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="8dad4-125">[![3addView](adding-a-view/_static/image4.png "3addView")](adding-a-view/_static/image3.png)</span></span>

<span data-ttu-id="8dad4-126">系統會建立*MvcMovie\Views\HelloWorld*資料夾和*MvcMovie\Views\HelloWorld\Index.vbhtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="8dad4-126">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.vbhtml* file are created.</span></span> <span data-ttu-id="8dad4-127">您可以在**方案總管**中看到這些專案：</span><span class="sxs-lookup"><span data-stu-id="8dad4-127">You can see them in **Solution Explorer**:</span></span>

<span data-ttu-id="8dad4-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="8dad4-128">[![SolnExpHelloWorldIndx](adding-a-view/_static/image6.png "SolnExpHelloWorldIndx")](adding-a-view/_static/image5.png)</span></span>

<span data-ttu-id="8dad4-129">在 `<h2>` 標記底下新增一些 HTML。</span><span class="sxs-lookup"><span data-stu-id="8dad4-129">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="8dad4-130">修改過的*MvcMovie\Views\HelloWorld\Index.vbhtml*檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="8dad4-130">The modified *MvcMovie\Views\HelloWorld\Index.vbhtml* file is shown below.</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample2.vbhtml)]

<span data-ttu-id="8dad4-131">執行應用程式，並流覽至 &quot;hello world&quot; 控制器（`http://localhost:xxxx/HelloWorld`）。</span><span class="sxs-lookup"><span data-stu-id="8dad4-131">Run the application and browse to the &quot;hello world&quot; controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="8dad4-132">控制器中的 `Index` 方法不會執行太多工做;它只會執行 `return View()`語句，這表示我們想要使用視圖範本檔案來呈現對用戶端的回應。</span><span class="sxs-lookup"><span data-stu-id="8dad4-132">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which indicated that we wanted to use a view template file to render a response to the client.</span></span> <span data-ttu-id="8dad4-133">因為我們並未明確指定要使用的視圖範本檔案的名稱，所以 ASP.NET MVC 會預設為使用 *\Views\HelloWorld*資料夾中的*vbhtml*視圖檔案。</span><span class="sxs-lookup"><span data-stu-id="8dad4-133">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.vbhtml* view file within the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="8dad4-134">下圖顯示在此視圖中硬式編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="8dad4-134">The image below shows the string hard-coded in the view.</span></span>

<span data-ttu-id="8dad4-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="8dad4-135">[![3HelloWorld](adding-a-view/_static/image8.png "3HelloWorld")](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="8dad4-136">看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="8dad4-136">Looks pretty good.</span></span> <span data-ttu-id="8dad4-137">不過，請注意，瀏覽器的標題列會顯示 &quot;索引&quot; 而頁面上的大標題會顯示為 [&quot;我的 MVC 應用程式]。&quot; 讓我們變更這些。</span><span class="sxs-lookup"><span data-stu-id="8dad4-137">However, notice that the browser's title bar says &quot;Index&quot; and the big title on the page says &quot;My MVC Application.&quot; Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="8dad4-138">變更檢視和版面配置頁</span><span class="sxs-lookup"><span data-stu-id="8dad4-138">Changing views and layout pages</span></span>

<span data-ttu-id="8dad4-139">首先，讓我們變更 MVC 應用程式 &quot;的文字。&quot; 該文字會共用並顯示在每個頁面上。</span><span class="sxs-lookup"><span data-stu-id="8dad4-139">First, let's change the text &quot;My MVC Application.&quot; That text is shared and appears on every page.</span></span> <span data-ttu-id="8dad4-140">它實際上只會出現在專案中的一個位置，即使它是在應用程式的每個頁面上也一樣。</span><span class="sxs-lookup"><span data-stu-id="8dad4-140">It actually appears in only one place in our project, even though it's on every page in our application.</span></span> <span data-ttu-id="8dad4-141">移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 *\_配置 vbhtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="8dad4-141">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.vbhtml* file.</span></span> <span data-ttu-id="8dad4-142">這個檔案稱為版面配置頁，它是所有其他頁面都使用的共用 &quot;shell&quot;。</span><span class="sxs-lookup"><span data-stu-id="8dad4-142">This file is called a layout page and it's the shared &quot;shell&quot; that all other pages use.</span></span>

<span data-ttu-id="8dad4-143">請注意靠近檔案底部的 `@RenderBody()` 行程式碼。</span><span class="sxs-lookup"><span data-stu-id="8dad4-143">Note the `@RenderBody()` line of code near the bottom of the file.</span></span> <span data-ttu-id="8dad4-144">`RenderBody` 是一種預留位置，其中會顯示您建立的所有頁面，&quot;包裝在版面配置頁中的&quot;。</span><span class="sxs-lookup"><span data-stu-id="8dad4-144">`RenderBody` is a placeholder where all the pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="8dad4-145">將 [`<h1>`] 標題從 [ **&quot;** 我的 MVC 應用&quot; 程式] 變更為 [&quot;Mvc 電影應用程式&quot;]。</span><span class="sxs-lookup"><span data-stu-id="8dad4-145">Change the `<h1>` heading from **&quot;** My MVC Application&quot; to &quot;MVC Movie App&quot;.</span></span>

[!code-html[Main](adding-a-view/samples/sample3.html)]

<span data-ttu-id="8dad4-146">執行應用程式，並注意它現在會顯示 &quot;MVC 電影應用程式&quot;。</span><span class="sxs-lookup"><span data-stu-id="8dad4-146">Run the application and note it now says &quot;MVC Movie App&quot;.</span></span> <span data-ttu-id="8dad4-147">按一下 [**關於**] 連結，該頁面也會顯示 &quot;MVC 電影應用程式&quot;。</span><span class="sxs-lookup"><span data-stu-id="8dad4-147">Click the **About** link, and that page shows &quot;MVC Movie App&quot;, too.</span></span>

<span data-ttu-id="8dad4-148">完整的 *\_配置的 vbhtml*檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="8dad4-148">The complete *\_Layout.vbhtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="8dad4-149">現在，讓我們變更索引頁面的標題（view）。</span><span class="sxs-lookup"><span data-stu-id="8dad4-149">Now, let's change the title of the Index page (view).</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample5.vbhtml)]

<span data-ttu-id="8dad4-150">開啟*MvcMovie\Views\HelloWorld\Index.vbhtml*。</span><span class="sxs-lookup"><span data-stu-id="8dad4-150">Open *MvcMovie\Views\HelloWorld\Index.vbhtml*.</span></span> <span data-ttu-id="8dad4-151">有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後是次要標頭（`<h2>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="8dad4-151">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="8dad4-152">我們會讓它們略有不同，讓您可以看到哪一段程式碼變更了哪個部分的應用程式。</span><span class="sxs-lookup"><span data-stu-id="8dad4-152">We'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

<span data-ttu-id="8dad4-153">執行應用程式，並流覽至`http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="8dad4-153">Run the application and browse to`http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="8dad4-154">請注意，瀏覽器標題、主要標題和次要標題已變更</span><span class="sxs-lookup"><span data-stu-id="8dad4-154">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="8dad4-155">您可以輕鬆地在應用程式中進行大幅變更，而對視圖進行小幅變更。</span><span class="sxs-lookup"><span data-stu-id="8dad4-155">It's easy to make big changes in your application with small changes to a view.</span></span> <span data-ttu-id="8dad4-156">(如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。</span><span class="sxs-lookup"><span data-stu-id="8dad4-156">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="8dad4-157">請在瀏覽器中按 Ctrl + F5 以強制載入來自伺服器的回應)。</span><span class="sxs-lookup"><span data-stu-id="8dad4-157">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="8dad4-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="8dad4-158">[![3_MyMovieList](adding-a-view/_static/image10.png "3_MyMovieList")](adding-a-view/_static/image9.png)</span></span>

<span data-ttu-id="8dad4-159">不過，我們有點 &quot;的資料&quot; （在此案例中，&quot;Hello World！&quot; 訊息）是硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="8dad4-159">Our little bit of &quot;data&quot; (in this case the &quot;Hello World!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="8dad4-160">我們的 MVC 應用程式有 V （views），而我們已經有 C （控制器），但沒有 M （模型）。</span><span class="sxs-lookup"><span data-stu-id="8dad4-160">Our MVC application has V (views) and we've got C (controllers), but no M (model) yet.</span></span> <span data-ttu-id="8dad4-161">很快地，我們將逐步解說如何建立資料庫，並從中抓取模型資料。</span><span class="sxs-lookup"><span data-stu-id="8dad4-161">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="8dad4-162">將資料從控制器傳遞至檢視</span><span class="sxs-lookup"><span data-stu-id="8dad4-162">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="8dad4-163">不過，在我們進入資料庫並討論模型之前，讓我們先討論如何將控制器的資訊傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="8dad4-163">Before we go to a database and talk about models, though, let's first talk about passing information from the Controller to a View.</span></span> <span data-ttu-id="8dad4-164">我們想要傳遞「視圖」範本所需的內容，以便向用戶端轉譯 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="8dad4-164">We want to pass what a view template requires in order to render an HTML response to a client.</span></span> <span data-ttu-id="8dad4-165">這些物件通常是由控制器類別所建立並傳遞給視圖範本，而且它們應該只包含此視圖範本所需的資料，而且不再需要。</span><span class="sxs-lookup"><span data-stu-id="8dad4-165">These objects are typically created and passed by a controller class to a view template, and they should contain only the data that the view template requires — and no more.</span></span>

<span data-ttu-id="8dad4-166">先前使用 `HelloWorldController` 類別，`Welcome` 動作方法會採用 `name` 和 `numTimes` 參數，然後將參數值輸出至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="8dad4-166">Previously with the `HelloWorldController` class, the `Welcome` action method took a `name` and a `numTimes` parameter and then output the parameter values to the browser.</span></span> <span data-ttu-id="8dad4-167">而不是讓控制器直接轉譯此回應，讓我們改為將該資料放在此視圖的包中。</span><span class="sxs-lookup"><span data-stu-id="8dad4-167">Rather than have the controller continue to render this response directly, let's instead we'll put that data in a bag for the View.</span></span> <span data-ttu-id="8dad4-168">控制器和 Views 可以使用 `ViewBag` 物件來保存該資料。</span><span class="sxs-lookup"><span data-stu-id="8dad4-168">Controllers and Views can use a `ViewBag` object to hold that data.</span></span> <span data-ttu-id="8dad4-169">這會自動傳遞至視圖範本，並用來呈現 HTML 回應，使用包的內容做為資料。</span><span class="sxs-lookup"><span data-stu-id="8dad4-169">That will be passed over to a view template automatically, and used to render the HTML response using the contents of the bag as data.</span></span> <span data-ttu-id="8dad4-170">如此一來，控制器就會關心一件事，並使用另一個視圖範本，讓我們能夠在應用程式中維護 &quot;的顧慮分離&quot;。</span><span class="sxs-lookup"><span data-stu-id="8dad4-170">That way the controller is concerned with one thing and the view template with another — enabling us to maintain clean &quot;separation of concerns&quot; within the application.</span></span>

<span data-ttu-id="8dad4-171">或者，我們可以定義自訂類別，然後自行建立該物件的實例，並在其中填入資料並將其傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="8dad4-171">Alternatively, we could define a custom class, then create an instance of that object on our own, fill it with data and pass it to the View.</span></span> <span data-ttu-id="8dad4-172">這通常稱為 ViewModel，因為它是 View 的自訂模型。</span><span class="sxs-lookup"><span data-stu-id="8dad4-172">That is often called a ViewModel, because it's a custom Model for the View.</span></span> <span data-ttu-id="8dad4-173">不過，對於少量的資料，ViewBag 的效果很好。</span><span class="sxs-lookup"><span data-stu-id="8dad4-173">For small amounts of data, however, the ViewBag works great.</span></span>

<span data-ttu-id="8dad4-174">返回*HelloWorldController* ，將控制器內的 `Welcome` 方法變更為將訊息和 numtimes is 放入 ViewBag 中。</span><span class="sxs-lookup"><span data-stu-id="8dad4-174">Return to the *HelloWorldController.vb* file change the `Welcome` method inside the controller to put the Message and NumTimes into the ViewBag.</span></span> <span data-ttu-id="8dad4-175">ViewBag 是動態物件。</span><span class="sxs-lookup"><span data-stu-id="8dad4-175">The ViewBag is a dynamic object.</span></span> <span data-ttu-id="8dad4-176">這表示您可以將任何想要的內容放在其中。</span><span class="sxs-lookup"><span data-stu-id="8dad4-176">That means you can put whatever you want in to it.</span></span> <span data-ttu-id="8dad4-177">ViewBag 沒有已定義的屬性，除非您在其中放置內容。</span><span class="sxs-lookup"><span data-stu-id="8dad4-177">The ViewBag has no defined properties until you put something inside it.</span></span>

<span data-ttu-id="8dad4-178">在相同檔案中，具有新類別的完整 `HelloWorldController.vb`。</span><span class="sxs-lookup"><span data-stu-id="8dad4-178">The complete `HelloWorldController.vb` with the new class in the same file.</span></span>

[!code-vb[Main](adding-a-view/samples/sample6.vb)]

<span data-ttu-id="8dad4-179">現在，我們的 ViewBag 包含將會自動傳遞到 View 的資料。</span><span class="sxs-lookup"><span data-stu-id="8dad4-179">Now our ViewBag contains data that will be passed over to the View automatically.</span></span> <span data-ttu-id="8dad4-180">同樣地，如果我們喜歡，也可以傳入我們自己的物件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="8dad4-180">Again, alternatively we could have passed in our own object like this if we liked:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="8dad4-181">現在我們需要一個 `WelcomeView` 範本！</span><span class="sxs-lookup"><span data-stu-id="8dad4-181">Now we need a `WelcomeView` template!</span></span> <span data-ttu-id="8dad4-182">執行應用程式，以編譯新的程式碼。</span><span class="sxs-lookup"><span data-stu-id="8dad4-182">Run the application so the new code is compiled.</span></span> <span data-ttu-id="8dad4-183">關閉瀏覽器，在 `Welcome` 方法內按一下滑鼠右鍵，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="8dad4-183">Close the browser, right-click inside the `Welcome` method, and then click **Add View**.</span></span>

<span data-ttu-id="8dad4-184">[**加入視圖**] 對話方塊的外觀如下所示。</span><span class="sxs-lookup"><span data-stu-id="8dad4-184">Here's what your **Add View** dialog box looks like.</span></span>

<span data-ttu-id="8dad4-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="8dad4-185">[![3AddWelcomeView](adding-a-view/_static/image12.png "3AddWelcomeView")](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="8dad4-186">將下列程式碼加入至新的歡迎畫面中的 `<h2>` 元素底下<em>。</em>vbhtml 檔案。</span><span class="sxs-lookup"><span data-stu-id="8dad4-186">Add the following code under the `<h2>` element in the new <em>Welcome.</em>vbhtml file.</span></span> <span data-ttu-id="8dad4-187">我們會建立迴圈，並說 &quot;Hello&quot; 的次數，如同使用者所說的一樣！</span><span class="sxs-lookup"><span data-stu-id="8dad4-187">We'll make a loop and say &quot;Hello&quot; as many times as the user says we should!</span></span>

[!code-vbhtml[Main](adding-a-view/samples/sample8.vbhtml)]

<span data-ttu-id="8dad4-188">執行應用程式，並流覽至 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span><span class="sxs-lookup"><span data-stu-id="8dad4-188">Run the application and browse to `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`</span></span>

<span data-ttu-id="8dad4-189">現在會從 URL 取得資料，並自動傳遞至控制器。</span><span class="sxs-lookup"><span data-stu-id="8dad4-189">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="8dad4-190">控制器會將資料封裝成 `Model` 物件，並將該物件傳遞至 view。</span><span class="sxs-lookup"><span data-stu-id="8dad4-190">The controller packages up the data into a `Model` object and passes that object to the view.</span></span> <span data-ttu-id="8dad4-191">視圖會將資料以 HTML 形式顯示給使用者。</span><span class="sxs-lookup"><span data-stu-id="8dad4-191">The view than displays the data as HTML to the user.</span></span>

<span data-ttu-id="8dad4-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="8dad4-192">[![3Hello_Scott_4](adding-a-view/_static/image14.png "3Hello_Scott_4")](adding-a-view/_static/image13.png)</span></span>

<span data-ttu-id="8dad4-193">這是一種適用于模型的 &quot;M&quot;，但不是資料庫種類。</span><span class="sxs-lookup"><span data-stu-id="8dad4-193">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="8dad4-194">讓我們運用所學的內容，建立電影的資料庫。</span><span class="sxs-lookup"><span data-stu-id="8dad4-194">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="8dad4-195">[上一頁](adding-a-controller.md)
> [下一頁](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="8dad4-195">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
