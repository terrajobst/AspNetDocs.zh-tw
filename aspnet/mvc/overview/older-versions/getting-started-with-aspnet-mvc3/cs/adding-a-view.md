---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
title: 加入 View （C#） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: abc7c78d-cb09-4a4c-a887-61bc401d40e3
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: b4a1316feb8d9b7f3ef5ca4755bf1cc5b23e6ef9
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77458186"
---
# <a name="adding-a-view-c"></a><span data-ttu-id="9d89a-103">新增檢視 (C#)</span><span class="sxs-lookup"><span data-stu-id="9d89a-103">Adding a View (C#)</span></span>

<span data-ttu-id="9d89a-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="9d89a-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="9d89a-105">本教學課程的更新版本可在[這裡](../../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="9d89a-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="9d89a-106">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="9d89a-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="9d89a-107">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="9d89a-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="9d89a-108">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="9d89a-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="9d89a-109">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="9d89a-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="9d89a-110">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="9d89a-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="9d89a-111">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="9d89a-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="9d89a-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="9d89a-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="9d89a-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="9d89a-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="9d89a-114">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="9d89a-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="9d89a-115">本主題提供具有C#原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="9d89a-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="9d89a-116">[下載C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="9d89a-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="9d89a-117">如果您偏好 Visual Basic，請切換到本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="9d89a-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="9d89a-118">在本節中，您將修改 `HelloWorldController` 類別，以使用視圖範本檔案，將產生 HTML 回應的程式完全封裝至用戶端。</span><span class="sxs-lookup"><span data-stu-id="9d89a-118">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="9d89a-119">您將使用 ASP.NET MVC 3 引進的新[Razor view 引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)來建立一個視圖範本檔案。</span><span class="sxs-lookup"><span data-stu-id="9d89a-119">You'll create a view template file using the new [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="9d89a-120">以 Razor 為基礎的視圖範本具有 *. cshtml*副檔名，並提供簡潔的方式來使用C#建立 HTML 輸出。</span><span class="sxs-lookup"><span data-stu-id="9d89a-120">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="9d89a-121">Razor 會將撰寫視圖範本時所需的字元和按鍵數目降至最低，並可提供快速、流暢的編碼工作流程。</span><span class="sxs-lookup"><span data-stu-id="9d89a-121">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="9d89a-122">首先，在 `HelloWorldController` 類別中使用具有 `Index` 方法的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="9d89a-122">Start by using a view template with the `Index` method in the `HelloWorldController` class.</span></span> <span data-ttu-id="9d89a-123">目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。</span><span class="sxs-lookup"><span data-stu-id="9d89a-123">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="9d89a-124">變更 `Index` 方法，以傳回 `View` 物件，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d89a-124">Change the `Index` method to return a `View` object, as shown in the following:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="9d89a-125">這段程式碼會使用視圖範本來產生瀏覽器的 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="9d89a-125">This code uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="9d89a-126">在專案中，加入您可以搭配 `Index` 方法使用的 [視圖] 範本。</span><span class="sxs-lookup"><span data-stu-id="9d89a-126">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="9d89a-127">若要這麼做，請以滑鼠右鍵按一下 `Index` 方法，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="9d89a-127">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="9d89a-128">[**加入視圖**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="9d89a-128">The **Add View** dialog box appears.</span></span> <span data-ttu-id="9d89a-129">保留預設值，然後按一下 [**新增**] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="9d89a-129">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="9d89a-130">系統會建立*MvcMovie\Views\HelloWorld*資料夾和*MvcMovie\Views\HelloWorld\Index.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="9d89a-130">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="9d89a-131">您可以在**方案總管**中看到這些專案：</span><span class="sxs-lookup"><span data-stu-id="9d89a-131">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="9d89a-132">以下顯示已建立的*Index. cshtml*檔案：</span><span class="sxs-lookup"><span data-stu-id="9d89a-132">The following shows the *Index.cshtml* file that was created:</span></span>

<span data-ttu-id="9d89a-133">[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="9d89a-133">[![HelloWorldIndex](adding-a-view/_static/image5.png)](adding-a-view/_static/image4.png)</span></span>

<span data-ttu-id="9d89a-134">在 `<h2>` 標記底下新增一些 HTML。</span><span class="sxs-lookup"><span data-stu-id="9d89a-134">Add some HTML under the `<h2>` tag.</span></span> <span data-ttu-id="9d89a-135">修改過的*MvcMovie\Views\HelloWorld\Index.cshtml*檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="9d89a-135">The modified *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample2.cshtml)]

<span data-ttu-id="9d89a-136">執行應用程式，並流覽至 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。</span><span class="sxs-lookup"><span data-stu-id="9d89a-136">Run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="9d89a-137">控制器中的 `Index` 方法不會執行太多工做;它只會執行語句 `return View()`，這會指定方法應該使用視圖範本檔案來呈現瀏覽器的回應。</span><span class="sxs-lookup"><span data-stu-id="9d89a-137">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="9d89a-138">由於您未明確指定所要使用之視圖範本檔案的名稱，因此 ASP.NET MVC 會預設為使用 *\Views\HelloWorld*資料夾中的*Index. cshtml* view file。</span><span class="sxs-lookup"><span data-stu-id="9d89a-138">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="9d89a-139">下圖顯示在此視圖中硬式編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="9d89a-139">The image below shows the string hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="9d89a-140">看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="9d89a-140">Looks pretty good.</span></span> <span data-ttu-id="9d89a-141">不過，請注意，瀏覽器的標題列會顯示「索引」，而頁面上的大標題會顯示「我的 MVC 應用程式」。</span><span class="sxs-lookup"><span data-stu-id="9d89a-141">However, notice that the browser's title bar says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="9d89a-142">讓我們變更這些。</span><span class="sxs-lookup"><span data-stu-id="9d89a-142">Let's change those.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="9d89a-143">變更視圖和版面配置頁</span><span class="sxs-lookup"><span data-stu-id="9d89a-143">Changing Views and Layout Pages</span></span>

<span data-ttu-id="9d89a-144">首先，您要變更頁面頂端的「我的 MVC 應用程式」標題。</span><span class="sxs-lookup"><span data-stu-id="9d89a-144">First, you want to change the "My MVC Application" title at the top of the page.</span></span> <span data-ttu-id="9d89a-145">這是每一頁通用的文字。</span><span class="sxs-lookup"><span data-stu-id="9d89a-145">That text is common to every page.</span></span> <span data-ttu-id="9d89a-146">它實際上只會在專案的一個位置中實作為，即使它出現在應用程式的每個頁面上也一樣。</span><span class="sxs-lookup"><span data-stu-id="9d89a-146">It actually is implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="9d89a-147">移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 *\_版面配置. cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="9d89a-147">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="9d89a-148">這個檔案稱為版面配置*頁*，它是所有其他頁面都使用的共用「shell」。</span><span class="sxs-lookup"><span data-stu-id="9d89a-148">This file is called a *layout page* and it's the shared "shell" that all other pages use.</span></span>

<span data-ttu-id="9d89a-149">[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="9d89a-149">[![_LayoutCshtml](adding-a-view/_static/image8.png)](adding-a-view/_static/image7.png)</span></span>

<span data-ttu-id="9d89a-150">版面配置範本可讓您在一處指定網站的 HTML 容器版面配置，然後將它套用到您網站中的多個頁面。</span><span class="sxs-lookup"><span data-stu-id="9d89a-150">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="9d89a-151">請注意靠近檔案底部的 `@RenderBody()` 行。</span><span class="sxs-lookup"><span data-stu-id="9d89a-151">Note the `@RenderBody()` line near the bottom of the file.</span></span> <span data-ttu-id="9d89a-152">`RenderBody` 是一種預留位置，其中您所建立的所有視圖特定頁面都會顯示在版面配置頁中「包裝」。</span><span class="sxs-lookup"><span data-stu-id="9d89a-152">`RenderBody` is a placeholder where all the view-specific pages you create show up, "wrapped" in the layout page.</span></span> <span data-ttu-id="9d89a-153">將版面配置範本中的標題標題從「我的 MVC 應用程式」變更為「MVC 電影應用程式」。</span><span class="sxs-lookup"><span data-stu-id="9d89a-153">Change the title heading in the layout template from "My MVC Application" to "MVC Movie App".</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml)]

<span data-ttu-id="9d89a-154">執行應用程式，並注意它現在會顯示「MVC 電影應用程式」。</span><span class="sxs-lookup"><span data-stu-id="9d89a-154">Run the application and notice that it now says "MVC Movie App".</span></span> <span data-ttu-id="9d89a-155">按一下 [**關於**] 連結，您也會看到該頁面如何顯示「MVC 電影應用程式」。</span><span class="sxs-lookup"><span data-stu-id="9d89a-155">Click the **About** link, and you see how that page shows "MVC Movie App", too.</span></span> <span data-ttu-id="9d89a-156">我們能夠在版面配置範本中進行變更一次，並讓網站上的所有頁面反映新的標題。</span><span class="sxs-lookup"><span data-stu-id="9d89a-156">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="9d89a-157">完整的 *\_配置 cshtml*檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d89a-157">The complete *\_Layout.cshtml* file is shown below:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="9d89a-158">現在，讓我們變更索引頁面的標題（view）。</span><span class="sxs-lookup"><span data-stu-id="9d89a-158">Now, let's change the title of the Index page (view).</span></span>

<span data-ttu-id="9d89a-159">開啟*MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="9d89a-159">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="9d89a-160">有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後是次要標頭（`<h2>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="9d89a-160">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="9d89a-161">您會使這些變更略有不同，因此可看出哪一段程式碼變更了應用程式的哪個部分。</span><span class="sxs-lookup"><span data-stu-id="9d89a-161">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="9d89a-162">若要指示要顯示的 HTML 標題，上述程式碼會設定 `ViewBag` 物件的 `Title` 屬性（位於*Index. cshtml* view template 中）。</span><span class="sxs-lookup"><span data-stu-id="9d89a-162">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="9d89a-163">如果您回顧版面配置範本的原始程式碼，您會注意到範本會在 `<title>` 元素中使用這個值，做為 HTML `<head>` 區段的一部分。</span><span class="sxs-lookup"><span data-stu-id="9d89a-163">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML.</span></span> <span data-ttu-id="9d89a-164">使用這種方法，您可以輕鬆地在您的視圖範本和配置檔案之間傳遞其他參數。</span><span class="sxs-lookup"><span data-stu-id="9d89a-164">Using this approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="9d89a-165">執行應用程式，並流覽至 `http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="9d89a-165">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="9d89a-166">請注意，瀏覽器標題、主要標題和次要標題已變更</span><span class="sxs-lookup"><span data-stu-id="9d89a-166">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="9d89a-167">(如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。</span><span class="sxs-lookup"><span data-stu-id="9d89a-167">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="9d89a-168">請在瀏覽器中按 Ctrl + F5 以強制載入來自伺服器的回應)。</span><span class="sxs-lookup"><span data-stu-id="9d89a-168">Press Ctrl+F5 in your browser to force the response from the server to be loaded.)</span></span>

<span data-ttu-id="9d89a-169">同時也請注意，已將 [*建立*] 視圖範本中的內容與 [\_配置] [ *cshtml* ] 視圖範本合併，並將單一 HTML 回應傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="9d89a-169">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="9d89a-170">版面配置範本可讓您輕鬆進行會套用到應用程式之所有頁面的變更。</span><span class="sxs-lookup"><span data-stu-id="9d89a-170">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="9d89a-171">然而，我們的這一點點「資料」(在此案例中為 "Hello from our View Template!"</span><span class="sxs-lookup"><span data-stu-id="9d89a-171">Our little bit of "data" (in this case the "Hello from our View Template!"</span></span> <span data-ttu-id="9d89a-172">訊息) 是硬式編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="9d89a-172">message) is hard-coded, though.</span></span> <span data-ttu-id="9d89a-173">MVC 應用程式具有 "V" (檢視)，並已取得 "C" (控制器)，但還沒有 "M" (模型)。</span><span class="sxs-lookup"><span data-stu-id="9d89a-173">The MVC application has a "V" (view) and you've got a "C" (controller), but no "M" (model) yet.</span></span> <span data-ttu-id="9d89a-174">很快地，我們將逐步解說如何建立資料庫，並從中抓取模型資料。</span><span class="sxs-lookup"><span data-stu-id="9d89a-174">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="9d89a-175">將資料從控制器傳遞至檢視</span><span class="sxs-lookup"><span data-stu-id="9d89a-175">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="9d89a-176">不過，在我們進入資料庫並討論模型之前，讓我們先討論如何將控制器的資訊傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="9d89a-176">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="9d89a-177">系統會叫用控制器類別，以回應傳入的 URL 要求。</span><span class="sxs-lookup"><span data-stu-id="9d89a-177">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="9d89a-178">控制器類別是您撰寫程式碼來處理傳入參數、從資料庫抓取資料，最後決定要傳回給瀏覽器的回應類型。</span><span class="sxs-lookup"><span data-stu-id="9d89a-178">A controller class is where you write the code that handles the incoming parameters, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="9d89a-179">然後，您可以從控制器使用視圖範本來產生並格式化瀏覽器的 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="9d89a-179">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="9d89a-180">控制器會負責提供所需的任何資料或物件，以便讓視圖範本呈現對瀏覽器的回應。</span><span class="sxs-lookup"><span data-stu-id="9d89a-180">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="9d89a-181">「視圖」範本應該永遠不會執行商務邏輯，或直接與資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="9d89a-181">A view template should never perform business logic or interact with a database directly.</span></span> <span data-ttu-id="9d89a-182">相反地，它應該只能與由控制器提供給它的資料搭配使用。</span><span class="sxs-lookup"><span data-stu-id="9d89a-182">Instead, it should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="9d89a-183">維護這項「關注點分離」有助於讓您的程式碼保持整潔且更容易維護。</span><span class="sxs-lookup"><span data-stu-id="9d89a-183">Maintaining this "separation of concerns" helps keep your code clean and more maintainable.</span></span>

<span data-ttu-id="9d89a-184">目前，`HelloWorldController` 類別中的 `Welcome` 動作方法會接受 `name` 和 `numTimes` 參數，然後將這些值直接輸出到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="9d89a-184">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="9d89a-185">不是讓控制器將此回應轉譯為字串，讓我們將控制器變更為改用 view 範本。</span><span class="sxs-lookup"><span data-stu-id="9d89a-185">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="9d89a-186">檢視範本會產生動態回應，這表示您需要將適當數量的資料從控制器傳遞至檢視，以便產生回應。</span><span class="sxs-lookup"><span data-stu-id="9d89a-186">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="9d89a-187">若要這麼做，您可以讓控制器將 view template 所需的動態資料放在 view 範本可以存取的 `ViewBag` 物件中。</span><span class="sxs-lookup"><span data-stu-id="9d89a-187">You can do this by having the controller put the dynamic data that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="9d89a-188">返回*HelloWorldController.cs*檔案並變更 `Welcome` 方法，將 `Message` 和 `NumTimes` 值新增至 `ViewBag` 物件。</span><span class="sxs-lookup"><span data-stu-id="9d89a-188">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="9d89a-189">`ViewBag` 是動態物件，這表示您可以將任何想要的內容放在其中：`ViewBag` 物件沒有定義的屬性，直到您將內容放在其中為止。</span><span class="sxs-lookup"><span data-stu-id="9d89a-189">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="9d89a-190">完整的 *HelloWorldController.cs* 檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d89a-190">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample6.cs)]

<span data-ttu-id="9d89a-191">現在，`ViewBag` 物件包含將會自動傳遞至視圖的資料。</span><span class="sxs-lookup"><span data-stu-id="9d89a-191">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="9d89a-192">接下來，您需要一個歡迎視圖範本！</span><span class="sxs-lookup"><span data-stu-id="9d89a-192">Next, you need a Welcome view template!</span></span> <span data-ttu-id="9d89a-193">在 [**調試**] 功能表中，選取 [**建立 MvcMovie** ] 以確定專案已編譯。</span><span class="sxs-lookup"><span data-stu-id="9d89a-193">In the **Debug** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="9d89a-194">[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="9d89a-194">[![BuildHelloWorld](adding-a-view/_static/image12.png)](adding-a-view/_static/image11.png)</span></span>

<span data-ttu-id="9d89a-195">然後以滑鼠右鍵按一下 `Welcome` 方法，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="9d89a-195">Then right-click inside the `Welcome` method and click **Add View**.</span></span> <span data-ttu-id="9d89a-196">[**加入視圖**] 對話方塊如下所示：</span><span class="sxs-lookup"><span data-stu-id="9d89a-196">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image13.png)

<span data-ttu-id="9d89a-197">按一下 **[新增]** ，然後在新的 [*歡迎使用] cshtml*檔案中的 `<h2>` 專案底下新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="9d89a-197">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="9d89a-198">您將建立一個迴圈，顯示「Hello」，就像使用者所說的一樣多次。</span><span class="sxs-lookup"><span data-stu-id="9d89a-198">You'll create a loop that says "Hello" as many times as the user says it should.</span></span> <span data-ttu-id="9d89a-199">完整的*歡迎使用 cshtml*檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="9d89a-199">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample7.cshtml)]

<span data-ttu-id="9d89a-200">執行應用程式，並流覽至下列 URL：</span><span class="sxs-lookup"><span data-stu-id="9d89a-200">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="9d89a-201">現在會從 URL 取得資料，並自動傳遞至控制器。</span><span class="sxs-lookup"><span data-stu-id="9d89a-201">Now data is taken from the URL and passed to the controller automatically.</span></span> <span data-ttu-id="9d89a-202">控制器會將資料封裝到 `ViewBag` 物件中，並將該物件傳遞至 view。</span><span class="sxs-lookup"><span data-stu-id="9d89a-202">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="9d89a-203">然後，此視圖會以 HTML 將資料顯示給使用者。</span><span class="sxs-lookup"><span data-stu-id="9d89a-203">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image14.png)

<span data-ttu-id="9d89a-204">這是一種代表模型的 "M"，但不是資料庫類型。</span><span class="sxs-lookup"><span data-stu-id="9d89a-204">Well, that was a kind of an "M" for model, but not the database kind.</span></span> <span data-ttu-id="9d89a-205">讓我們運用所學的內容，建立電影的資料庫。</span><span class="sxs-lookup"><span data-stu-id="9d89a-205">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="9d89a-206">[上一頁](adding-a-controller.md)
> [下一頁](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="9d89a-206">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
