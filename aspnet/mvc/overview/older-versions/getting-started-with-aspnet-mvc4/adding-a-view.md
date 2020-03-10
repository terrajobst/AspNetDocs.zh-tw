---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
title: 加入視圖 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: dde851d7-882e-4d99-9b96-cf96daed81cc
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-view
msc.type: authoredcontent
ms.openlocfilehash: 81c2e1f46b08cbc9b5aa5d6c1b36d9d8dc2ba581
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78599747"
---
# <a name="adding-a-view"></a><span data-ttu-id="1a698-104">新增檢視</span><span class="sxs-lookup"><span data-stu-id="1a698-104">Adding a View</span></span>

<span data-ttu-id="1a698-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1a698-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="1a698-106">本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="1a698-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="1a698-107">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="1a698-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="1a698-108">在本節中，您將修改 `HelloWorldController` 類別，以使用視圖範本檔案，將產生 HTML 回應的程式完全封裝至用戶端。</span><span class="sxs-lookup"><span data-stu-id="1a698-108">In this section you're going to modify the `HelloWorldController` class to use view template files to cleanly encapsulate the process of generating HTML responses to a client.</span></span>

<span data-ttu-id="1a698-109">您將使用 ASP.NET MVC 3 引進的[Razor view 引擎](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx)來建立一個視圖範本檔案。</span><span class="sxs-lookup"><span data-stu-id="1a698-109">You'll create a view template file using the [Razor view engine](https://weblogs.asp.net/scottgu/archive/2010/07/02/introducing-razor.aspx) introduced with ASP.NET MVC 3.</span></span> <span data-ttu-id="1a698-110">以 Razor 為基礎的視圖範本具有 *. cshtml*副檔名，並提供簡潔的方式來使用C#建立 HTML 輸出。</span><span class="sxs-lookup"><span data-stu-id="1a698-110">Razor-based view templates have a *.cshtml* file extension, and provide an elegant way to create HTML output using C#.</span></span> <span data-ttu-id="1a698-111">Razor 會將撰寫視圖範本時所需的字元和按鍵數目降至最低，並可提供快速、流暢的編碼工作流程。</span><span class="sxs-lookup"><span data-stu-id="1a698-111">Razor minimizes the number of characters and keystrokes required when writing a view template, and enables a fast, fluid coding workflow.</span></span>

<span data-ttu-id="1a698-112">目前，`Index` 方法會傳回字串，內含在控制器類別中硬式編碼的訊息。</span><span class="sxs-lookup"><span data-stu-id="1a698-112">Currently the `Index` method returns a string with a message that is hard-coded in the controller class.</span></span> <span data-ttu-id="1a698-113">變更 `Index` 方法以傳回 `View` 物件，如下列程式碼所示：</span><span class="sxs-lookup"><span data-stu-id="1a698-113">Change the `Index` method to return a `View` object, as shown in the following code:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample1.cs)]

<span data-ttu-id="1a698-114">上述 `Index` 方法會使用視圖範本來產生瀏覽器的 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="1a698-114">The `Index` method above uses a view template to generate an HTML response to the browser.</span></span> <span data-ttu-id="1a698-115">控制器方法（也稱為[動作方法](http://rachelappel.com/asp.net-mvc-actionresults-explained)）（例如上述的 `Index` 方法）通常會傳回[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) （或衍生自[ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)的類別），而不是像字串這樣的基本類型。</span><span class="sxs-lookup"><span data-stu-id="1a698-115">Controller methods (also known as [action methods](http://rachelappel.com/asp.net-mvc-actionresults-explained)), such as the `Index` method above, generally return an [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx) (or a class derived from [ActionResult](https://msdn.microsoft.com/library/system.web.mvc.actionresult.aspx)), not primitive types like string.</span></span>

<span data-ttu-id="1a698-116">在專案中，加入您可以搭配 `Index` 方法使用的 [視圖] 範本。</span><span class="sxs-lookup"><span data-stu-id="1a698-116">In the project, add a view template that you can use with the `Index` method.</span></span> <span data-ttu-id="1a698-117">若要這麼做，請以滑鼠右鍵按一下 `Index` 方法，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="1a698-117">To do this, right-click inside the `Index` method and click **Add View**.</span></span>

![](adding-a-view/_static/image1.png)

<span data-ttu-id="1a698-118">[**加入視圖**] 對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="1a698-118">The **Add View** dialog box appears.</span></span> <span data-ttu-id="1a698-119">保留預設值，然後按一下 [**新增**] 按鈕：</span><span class="sxs-lookup"><span data-stu-id="1a698-119">Leave the defaults the way they are and click the **Add** button:</span></span>

![](adding-a-view/_static/image2.png)

<span data-ttu-id="1a698-120">系統會建立*MvcMovie\Views\HelloWorld*資料夾和*MvcMovie\Views\HelloWorld\Index.cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="1a698-120">The *MvcMovie\Views\HelloWorld* folder and the *MvcMovie\Views\HelloWorld\Index.cshtml* file are created.</span></span> <span data-ttu-id="1a698-121">您可以在**方案總管**中看到這些專案：</span><span class="sxs-lookup"><span data-stu-id="1a698-121">You can see them in **Solution Explorer**:</span></span>

![](adding-a-view/_static/image3.png)

<span data-ttu-id="1a698-122">以下顯示已建立的*Index. cshtml*檔案：</span><span class="sxs-lookup"><span data-stu-id="1a698-122">The following shows the *Index.cshtml* file that was created:</span></span>

![HelloWorldIndex](adding-a-view/_static/image4.png)

<span data-ttu-id="1a698-124">在 `<h2>` 標記底下新增下列 HTML。</span><span class="sxs-lookup"><span data-stu-id="1a698-124">Add the following HTML under the `<h2>` tag.</span></span>

[!code-html[Main](adding-a-view/samples/sample2.html)]

<span data-ttu-id="1a698-125">完整的*MvcMovie\Views\HelloWorld\Index.cshtml*檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="1a698-125">The complete *MvcMovie\Views\HelloWorld\Index.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample3.cshtml?highlight=7-8)]

<span data-ttu-id="1a698-126">如果您使用 Visual Studio 2012，請在 [方案管理器] 中，以滑鼠右鍵按一下 [ *Index. cshtml* ] 檔案，然後選取 [ **Page Inspector 中的 View**]。</span><span class="sxs-lookup"><span data-stu-id="1a698-126">If you are using Visual Studio 2012, in solution explorer, right click the *Index.cshtml* file and select **View in Page Inspector**.</span></span>

![PI](adding-a-view/_static/image5.png)

<span data-ttu-id="1a698-128">[Page Inspector 教學](../../views/using-page-inspector-in-aspnet-mvc.md)課程包含此新工具的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="1a698-128">The [Page Inspector tutorial](../../views/using-page-inspector-in-aspnet-mvc.md) has more information about this new tool.</span></span>

<span data-ttu-id="1a698-129">或者，執行應用程式並流覽至 `HelloWorld` 控制器（`http://localhost:xxxx/HelloWorld`）。</span><span class="sxs-lookup"><span data-stu-id="1a698-129">Alternatively, run the application and browse to the `HelloWorld` controller (`http://localhost:xxxx/HelloWorld`).</span></span> <span data-ttu-id="1a698-130">控制器中的 `Index` 方法不會執行太多工做;它只會執行語句 `return View()`，這會指定方法應該使用視圖範本檔案來呈現瀏覽器的回應。</span><span class="sxs-lookup"><span data-stu-id="1a698-130">The `Index` method in your controller didn't do much work; it simply ran the statement `return View()`, which specified that the method should use a view template file to render a response to the browser.</span></span> <span data-ttu-id="1a698-131">由於您未明確指定所要使用之視圖範本檔案的名稱，因此 ASP.NET MVC 會預設為使用 *\Views\HelloWorld*資料夾中的*Index. cshtml* view file。</span><span class="sxs-lookup"><span data-stu-id="1a698-131">Because you didn't explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the *Index.cshtml* view file in the *\Views\HelloWorld* folder.</span></span> <span data-ttu-id="1a698-132">下圖顯示我們的 View 範本中的字串 &quot;Hello！&quot; 在視圖中硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="1a698-132">The image below shows the string &quot;Hello from our View Template!&quot; hard-coded in the view.</span></span>

![](adding-a-view/_static/image6.png)

<span data-ttu-id="1a698-133">看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="1a698-133">Looks pretty good.</span></span> <span data-ttu-id="1a698-134">不過，請注意，瀏覽器的標題列會顯示 &quot;Index My ASP.NET A&quot;，而頁面頂端的大連結則顯示在這裡 &quot;您的標誌。&quot; 在此處 &quot;您的標誌。&quot; 連結是註冊和登入連結，下方連結至 Home、About 和 Contact 頁面。</span><span class="sxs-lookup"><span data-stu-id="1a698-134">However, notice that the browser's title bar shows &quot;Index My ASP.NET A&quot; and the big link on the top of the page says &quot;your logo here.&quot; Below the &quot;your logo here.&quot; link are registration and log in links, and below that links to Home, About and Contact pages.</span></span> <span data-ttu-id="1a698-135">讓我們變更其中一些部分。</span><span class="sxs-lookup"><span data-stu-id="1a698-135">Let's change some of these.</span></span>

## <a name="changing-views-and-layout-pages"></a><span data-ttu-id="1a698-136">變更視圖和版面配置頁</span><span class="sxs-lookup"><span data-stu-id="1a698-136">Changing Views and Layout Pages</span></span>

<span data-ttu-id="1a698-137">首先，您想要在這裡變更您的標誌 &quot;。在頁面頂端&quot; [標題]。</span><span class="sxs-lookup"><span data-stu-id="1a698-137">First, you want to change the &quot;your logo here.&quot; title at the top of the page.</span></span> <span data-ttu-id="1a698-138">這是每一頁通用的文字。</span><span class="sxs-lookup"><span data-stu-id="1a698-138">That text is common to every page.</span></span> <span data-ttu-id="1a698-139">它實際上只會在專案的一個位置中實作為，即使它出現在應用程式的每個頁面上也一樣。</span><span class="sxs-lookup"><span data-stu-id="1a698-139">It's actually implemented in only one place in the project, even though it appears on every page in the application.</span></span> <span data-ttu-id="1a698-140">移至**方案總管**中的 [ */Views/Shared* ] 資料夾，然後開啟 *\_版面配置. cshtml*檔案。</span><span class="sxs-lookup"><span data-stu-id="1a698-140">Go to the */Views/Shared* folder in **Solution Explorer** and open the *\_Layout.cshtml* file.</span></span> <span data-ttu-id="1a698-141">這個檔案稱為版面配置*頁*，它是所有其他頁面都使用的共用 &quot;shell&quot;。</span><span class="sxs-lookup"><span data-stu-id="1a698-141">This file is called a *layout page* and it's the shared &quot;shell&quot; that all other pages use.</span></span>

![_LayoutCshtml](adding-a-view/_static/image7.png)

<span data-ttu-id="1a698-143">版面配置範本可讓您在一處指定網站的 HTML 容器版面配置，然後將它套用到您網站中的多個頁面。</span><span class="sxs-lookup"><span data-stu-id="1a698-143">Layout templates allow you to specify the HTML container layout of your site in one place and then apply it across multiple pages in your site.</span></span> <span data-ttu-id="1a698-144">找到 `@RenderBody()` 這行。</span><span class="sxs-lookup"><span data-stu-id="1a698-144">Find the `@RenderBody()` line.</span></span> <span data-ttu-id="1a698-145">`RenderBody` 是顯示您建立之所有檢視特定頁面的預留位置，「包裝」&quot;&quot;在版面配置頁中。</span><span class="sxs-lookup"><span data-stu-id="1a698-145">`RenderBody` is a placeholder where all the view-specific pages you create show up, &quot;wrapped&quot; in the layout page.</span></span> <span data-ttu-id="1a698-146">例如，如果您選取 [關於] 連結，則會在 `RenderBody` 方法中轉譯*Views\Home\About.cshtml*視圖。</span><span class="sxs-lookup"><span data-stu-id="1a698-146">For example, if you select the About link, the *Views\Home\About.cshtml* view is rendered inside the `RenderBody` method.</span></span>

<span data-ttu-id="1a698-147">變更版面配置範本中的網站標題標題，從此處 &quot;您的標誌&quot; 至 &quot;MVC 電影&quot;。</span><span class="sxs-lookup"><span data-stu-id="1a698-147">Change the site-title heading in the layout template from &quot;your logo here&quot; to &quot;MVC Movie&quot;.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample4.cshtml)]

<span data-ttu-id="1a698-148">將 title 元素的內容取代為下列標記：</span><span class="sxs-lookup"><span data-stu-id="1a698-148">Replace the contents of the title element with the following markup:</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample5.cshtml)]

<span data-ttu-id="1a698-149">執行應用程式，並注意它現在會顯示 &quot;MVC Movie &quot;。</span><span class="sxs-lookup"><span data-stu-id="1a698-149">Run the application and notice that it now says &quot;MVC Movie &quot;.</span></span> <span data-ttu-id="1a698-150">按一下 [**關於**] 連結，您會看到該頁面也會顯示 &quot;MVC 電影&quot;的方式。</span><span class="sxs-lookup"><span data-stu-id="1a698-150">Click the **About** link, and you see how that page shows &quot;MVC Movie&quot;, too.</span></span> <span data-ttu-id="1a698-151">我們能夠在版面配置範本中進行變更一次，並讓網站上的所有頁面反映新的標題。</span><span class="sxs-lookup"><span data-stu-id="1a698-151">We were able to make the change once in the layout template and have all pages on the site reflect the new title.</span></span>

![](adding-a-view/_static/image8.png)

<span data-ttu-id="1a698-152">現在，讓我們來變更索引視圖的標題。</span><span class="sxs-lookup"><span data-stu-id="1a698-152">Now, let's change the title of the Index view.</span></span>

<span data-ttu-id="1a698-153">開啟*MvcMovie\Views\HelloWorld\Index.cshtml*。</span><span class="sxs-lookup"><span data-stu-id="1a698-153">Open *MvcMovie\Views\HelloWorld\Index.cshtml*.</span></span> <span data-ttu-id="1a698-154">有兩個地方可以進行變更：首先是出現在瀏覽器標題中的文字，然後是次要標頭（`<h2>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="1a698-154">There are two places to make a change: first, the text that appears in the title of the browser, and then in the secondary header (the `<h2>` element).</span></span> <span data-ttu-id="1a698-155">您會使這些變更略有不同，因此可看出哪一段程式碼變更了應用程式的哪個部分。</span><span class="sxs-lookup"><span data-stu-id="1a698-155">You'll make them slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample6.cshtml)]

<span data-ttu-id="1a698-156">若要指示要顯示的 HTML 標題，上述程式碼會設定 `ViewBag` 物件的 `Title` 屬性（位於*Index. cshtml* view template 中）。</span><span class="sxs-lookup"><span data-stu-id="1a698-156">To indicate the HTML title to display, the code above sets a `Title` property of the `ViewBag` object (which is in the *Index.cshtml* view template).</span></span> <span data-ttu-id="1a698-157">如果您回頭看一下版面配置範本的原始程式碼，就會發現範本會在 `<title>` 元素中使用這個值，做為我們先前修改之 HTML 的 `<head>` 區段的一部分。</span><span class="sxs-lookup"><span data-stu-id="1a698-157">If you look back at the source code of the layout template, you'll notice that the template uses this value in the `<title>` element as part of the `<head>` section of the HTML that we modified previously.</span></span> <span data-ttu-id="1a698-158">使用這種 `ViewBag` 方法，您可以輕鬆地在您的視圖範本和配置檔案之間傳遞其他參數。</span><span class="sxs-lookup"><span data-stu-id="1a698-158">Using this `ViewBag` approach, you can easily pass other parameters between your view template and your layout file.</span></span>

<span data-ttu-id="1a698-159">執行應用程式，並流覽至 `http://localhost:xx/HelloWorld`。</span><span class="sxs-lookup"><span data-stu-id="1a698-159">Run the application and browse to `http://localhost:xx/HelloWorld`.</span></span> <span data-ttu-id="1a698-160">請注意，瀏覽器標題、主要標題和次要標題已變更</span><span class="sxs-lookup"><span data-stu-id="1a698-160">Notice that the browser title, the primary heading, and the secondary headings have changed.</span></span> <span data-ttu-id="1a698-161">(如果您在瀏覽器中沒有看到變更，可能檢視的是快取的內容。</span><span class="sxs-lookup"><span data-stu-id="1a698-161">(If you don't see changes in the browser, you might be viewing cached content.</span></span> <span data-ttu-id="1a698-162">在瀏覽器中按 Ctrl + F5，以強制載入伺服器的回應。）瀏覽器標題會使用*我們在 [&quot;] 視圖範本*中設定的 `ViewBag.Title` 來建立，並在配置檔案中新增額外的 Movie 應用程式&quot;。</span><span class="sxs-lookup"><span data-stu-id="1a698-162">Press Ctrl+F5 in your browser to force the response from the server to be loaded.) The browser title is created with the `ViewBag.Title` we set in the *Index.cshtml* view template and the additional &quot;- Movie App&quot; added in the layout file.</span></span>

<span data-ttu-id="1a698-163">同時也請注意，已將 [*建立*] 視圖範本中的內容與 [\_配置] [ *cshtml* ] 視圖範本合併，並將單一 HTML 回應傳送至瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1a698-163">Also notice how the content in the *Index.cshtml* view template was merged with the *\_Layout.cshtml* view template and a single HTML response was sent to the browser.</span></span> <span data-ttu-id="1a698-164">版面配置範本可讓您輕鬆進行會套用到應用程式之所有頁面的變更。</span><span class="sxs-lookup"><span data-stu-id="1a698-164">Layout templates make it really easy to make changes that apply across all of the pages in your application.</span></span>

![](adding-a-view/_static/image9.png)

<span data-ttu-id="1a698-165">不過，我們有點 &quot;的資料&quot; （在此情況下，我們的 View Template 中的 &quot;Hello！&quot; message）是硬式編碼的。</span><span class="sxs-lookup"><span data-stu-id="1a698-165">Our little bit of &quot;data&quot; (in this case the &quot;Hello from our View Template!&quot; message) is hard-coded, though.</span></span> <span data-ttu-id="1a698-166">MVC 應用程式具有 &quot;V&quot; （view），而且您有 &quot;的 C&quot; （控制器），但尚未 &quot;M&quot; （model）。</span><span class="sxs-lookup"><span data-stu-id="1a698-166">The MVC application has a &quot;V&quot; (view) and you've got a &quot;C&quot; (controller), but no &quot;M&quot; (model) yet.</span></span> <span data-ttu-id="1a698-167">很快地，我們將逐步解說如何建立資料庫，並從中抓取模型資料。</span><span class="sxs-lookup"><span data-stu-id="1a698-167">Shortly, we'll walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-data-from-the-controller-to-the-view"></a><span data-ttu-id="1a698-168">將資料從控制器傳遞至檢視</span><span class="sxs-lookup"><span data-stu-id="1a698-168">Passing Data from the Controller to the View</span></span>

<span data-ttu-id="1a698-169">不過，在我們進入資料庫並討論模型之前，讓我們先討論如何將控制器的資訊傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="1a698-169">Before we go to a database and talk about models, though, let's first talk about passing information from the controller to a view.</span></span> <span data-ttu-id="1a698-170">系統會叫用控制器類別，以回應傳入的 URL 要求。</span><span class="sxs-lookup"><span data-stu-id="1a698-170">Controller classes are invoked in response to an incoming URL request.</span></span> <span data-ttu-id="1a698-171">控制器類別是您撰寫程式碼來處理傳入瀏覽器要求、從資料庫抓取資料，最後決定要傳回給瀏覽器的回應類型。</span><span class="sxs-lookup"><span data-stu-id="1a698-171">A controller class is where you write the code that handles the incoming browser requests, retrieves data from a database, and ultimately decides what type of response to send back to the browser.</span></span> <span data-ttu-id="1a698-172">然後，您可以從控制器使用視圖範本來產生並格式化瀏覽器的 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="1a698-172">View templates can then be used from a controller to generate and format an HTML response to the browser.</span></span>

<span data-ttu-id="1a698-173">控制器會負責提供所需的任何資料或物件，以便讓視圖範本呈現對瀏覽器的回應。</span><span class="sxs-lookup"><span data-stu-id="1a698-173">Controllers are responsible for providing whatever data or objects are required in order for a view template to render a response to the browser.</span></span> <span data-ttu-id="1a698-174">最佳做法：**視圖範本絕對不應執行商務邏輯，或直接與資料庫互動**。</span><span class="sxs-lookup"><span data-stu-id="1a698-174">A best practice: **A view template should never perform business logic or interact with a database directly**.</span></span> <span data-ttu-id="1a698-175">相反地，「視圖」範本只能與由控制器提供給它的資料搭配使用。</span><span class="sxs-lookup"><span data-stu-id="1a698-175">Instead, a view template should work only with the data that's provided to it by the controller.</span></span> <span data-ttu-id="1a698-176">維護這項 &quot;的顧慮&quot; 有助於讓程式碼保持整潔、可測試且更容易維護。</span><span class="sxs-lookup"><span data-stu-id="1a698-176">Maintaining this &quot;separation of concerns&quot; helps keep your code clean, testable and more maintainable.</span></span>

<span data-ttu-id="1a698-177">目前，`HelloWorldController` 類別中的 `Welcome` 動作方法會接受 `name` 和 `numTimes` 參數，然後將這些值直接輸出到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="1a698-177">Currently, the `Welcome` action method in the `HelloWorldController` class takes a `name` and a `numTimes` parameter and then outputs the values directly to the browser.</span></span> <span data-ttu-id="1a698-178">不是讓控制器將此回應轉譯為字串，讓我們將控制器變更為改用 view 範本。</span><span class="sxs-lookup"><span data-stu-id="1a698-178">Rather than have the controller render this response as a string, let's change the controller to use a view template instead.</span></span> <span data-ttu-id="1a698-179">檢視範本會產生動態回應，這表示您需要將適當數量的資料從控制器傳遞至檢視，以便產生回應。</span><span class="sxs-lookup"><span data-stu-id="1a698-179">The view template will generate a dynamic response, which means that you need to pass appropriate bits of data from the controller to the view in order to generate the response.</span></span> <span data-ttu-id="1a698-180">若要這麼做，您可以讓控制器將視圖範本所需的動態資料（參數）放置在 view 範本可以存取的 `ViewBag` 物件中。</span><span class="sxs-lookup"><span data-stu-id="1a698-180">You can do this by having the controller put the dynamic data (parameters) that the view template needs in a `ViewBag` object that the view template can then access.</span></span>

<span data-ttu-id="1a698-181">返回*HelloWorldController.cs*檔案並變更 `Welcome` 方法，將 `Message` 和 `NumTimes` 值新增至 `ViewBag` 物件。</span><span class="sxs-lookup"><span data-stu-id="1a698-181">Return to the *HelloWorldController.cs* file and change the `Welcome` method to add a `Message` and `NumTimes` value to the `ViewBag` object.</span></span> <span data-ttu-id="1a698-182">`ViewBag` 是動態物件，這表示您可以將任何想要的內容放在其中：`ViewBag` 物件沒有定義的屬性，直到您將內容放在其中為止。</span><span class="sxs-lookup"><span data-stu-id="1a698-182">`ViewBag` is a dynamic object, which means you can put whatever you want in to it; the `ViewBag` object has no defined properties until you put something inside it.</span></span> <span data-ttu-id="1a698-183">[ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將指定的參數（`name` 和 `numTimes`）從網址列中的查詢字串對應至方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="1a698-183">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters (`name` and `numTimes`) from the query string in the address bar to parameters in your method.</span></span> <span data-ttu-id="1a698-184">完整的 *HelloWorldController.cs* 檔案如下所示：</span><span class="sxs-lookup"><span data-stu-id="1a698-184">The complete *HelloWorldController.cs* file looks like this:</span></span>

[!code-csharp[Main](adding-a-view/samples/sample7.cs)]

<span data-ttu-id="1a698-185">現在，`ViewBag` 物件包含將會自動傳遞至視圖的資料。</span><span class="sxs-lookup"><span data-stu-id="1a698-185">Now the `ViewBag` object contains data that will be passed to the view automatically.</span></span>

<span data-ttu-id="1a698-186">接下來，您需要一個歡迎視圖範本！</span><span class="sxs-lookup"><span data-stu-id="1a698-186">Next, you need a Welcome view template!</span></span> <span data-ttu-id="1a698-187">在 [**建立**] 功能表中，選取 [**建立 MvcMovie** ] 以確定專案已編譯。</span><span class="sxs-lookup"><span data-stu-id="1a698-187">In the **Build** menu, select **Build MvcMovie** to make sure the project is compiled.</span></span>

<span data-ttu-id="1a698-188">然後以滑鼠右鍵按一下 `Welcome` 方法，然後按一下 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="1a698-188">Then right-click inside the `Welcome` method and click **Add View**.</span></span>

![](adding-a-view/_static/image10.png)

<span data-ttu-id="1a698-189">[**加入視圖**] 對話方塊如下所示：</span><span class="sxs-lookup"><span data-stu-id="1a698-189">Here's what the **Add View** dialog box looks like:</span></span>

![](adding-a-view/_static/image11.png)

<span data-ttu-id="1a698-190">按一下 **[新增]** ，然後在新的 [*歡迎使用] cshtml*檔案中的 `<h2>` 專案底下新增下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="1a698-190">Click **Add**, and then add the following code under the `<h2>` element in the new *Welcome.cshtml* file.</span></span> <span data-ttu-id="1a698-191">您將建立一個迴圈，指出 &quot;Hello&quot; 的次數與使用者所說的數目一樣多。</span><span class="sxs-lookup"><span data-stu-id="1a698-191">You'll create a loop that says &quot;Hello&quot; as many times as the user says it should.</span></span> <span data-ttu-id="1a698-192">完整的*歡迎使用 cshtml*檔案如下所示。</span><span class="sxs-lookup"><span data-stu-id="1a698-192">The complete *Welcome.cshtml* file is shown below.</span></span>

[!code-cshtml[Main](adding-a-view/samples/sample8.cshtml)]

<span data-ttu-id="1a698-193">執行應用程式，並流覽至下列 URL：</span><span class="sxs-lookup"><span data-stu-id="1a698-193">Run the application and browse to the following URL:</span></span>

`http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`

<span data-ttu-id="1a698-194">現在會從 URL 取得資料，並使用[模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結器傳遞至控制器。</span><span class="sxs-lookup"><span data-stu-id="1a698-194">Now data is taken from the URL and passed to the controller using the [model binder](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx).</span></span> <span data-ttu-id="1a698-195">控制器會將資料封裝到 `ViewBag` 物件中，並將該物件傳遞至 view。</span><span class="sxs-lookup"><span data-stu-id="1a698-195">The controller packages the data into a `ViewBag` object and passes that object to the view.</span></span> <span data-ttu-id="1a698-196">然後，此視圖會以 HTML 將資料顯示給使用者。</span><span class="sxs-lookup"><span data-stu-id="1a698-196">The view then displays the data as HTML to the user.</span></span>

![](adding-a-view/_static/image12.png)

<span data-ttu-id="1a698-197">在上述範例中，我們使用了 `ViewBag` 物件，將資料從控制器傳遞至 view。</span><span class="sxs-lookup"><span data-stu-id="1a698-197">In the sample above, we used a `ViewBag` object to pass data from the controller to a view.</span></span> <span data-ttu-id="1a698-198">在本教學課程中，我們將使用 view 模型，將資料從控制器傳遞至 view。</span><span class="sxs-lookup"><span data-stu-id="1a698-198">Latter in the tutorial, we will use a view model to pass data from a controller to a view.</span></span> <span data-ttu-id="1a698-199">傳遞資料的「視圖模型」方法通常是透過「視圖包」方法來處理的最佳作法。</span><span class="sxs-lookup"><span data-stu-id="1a698-199">The view model approach to passing data is generally much preferred over the view bag approach.</span></span> <span data-ttu-id="1a698-200">如需詳細資訊，請參閱 blog 專案[Dynamic V 強](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx)型別視圖。</span><span class="sxs-lookup"><span data-stu-id="1a698-200">See the blog entry [Dynamic V Strongly Typed Views](https://blogs.msdn.com/b/rickandy/archive/2011/01/28/dynamic-v-strongly-typed-views.aspx) for more information.</span></span>

<span data-ttu-id="1a698-201">這是一種適用于模型的 &quot;M&quot;，但不是資料庫種類。</span><span class="sxs-lookup"><span data-stu-id="1a698-201">Well, that was a kind of an &quot;M&quot; for model, but not the database kind.</span></span> <span data-ttu-id="1a698-202">讓我們運用所學的內容，建立電影的資料庫。</span><span class="sxs-lookup"><span data-stu-id="1a698-202">Let's take what we've learned and create a database of movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1a698-203">[上一頁](adding-a-controller.md)
> [下一頁](adding-a-model.md)</span><span class="sxs-lookup"><span data-stu-id="1a698-203">[Previous](adding-a-controller.md)
[Next](adding-a-model.md)</span></span>
