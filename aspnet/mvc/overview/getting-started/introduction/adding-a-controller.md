---
uid: mvc/overview/getting-started/introduction/adding-a-controller
title: 新增控制器 |Microsoft Docs
author: Rick-Anderson
description: ''
ms.author: riande
ms.date: 10/17/2013
ms.assetid: cc764f3b-6921-486a-8f44-c6ccd1249acd
msc.legacyurl: /mvc/overview/getting-started/introduction/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 80000b366203eff4b9524b7a5995832753b9eed3
ms.sourcegitcommit: 88fc80e3f65aebdf61ec9414810ddbc31c543f04
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 01/22/2020
ms.locfileid: "76519046"
---
# <a name="adding-a-controller"></a><span data-ttu-id="38e87-102">加入控制器</span><span class="sxs-lookup"><span data-stu-id="38e87-102">Adding a Controller</span></span>

<span data-ttu-id="38e87-103">依[Rick Anderson]((https://twitter.com/RickAndMSFT))</span><span class="sxs-lookup"><span data-stu-id="38e87-103">by [Rick Anderson]((https://twitter.com/RickAndMSFT))</span></span>

[!INCLUDE [Tutorial Note](index.md)]

<span data-ttu-id="38e87-104">MVC 代表*模型視圖控制器*。</span><span class="sxs-lookup"><span data-stu-id="38e87-104">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="38e87-105">MVC 是一種模式，可供開發良好架構、可測試且易於維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="38e87-105">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="38e87-106">以 MVC 為基礎的應用程式包含：</span><span class="sxs-lookup"><span data-stu-id="38e87-106">MVC-based applications contain:</span></span>

- <span data-ttu-id="38e87-107">**M**模型 ()：代表應用程式資料的類別，並使用驗證邏輯來強制執行該資料的商務規則。</span><span class="sxs-lookup"><span data-stu-id="38e87-107">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="38e87-108">**V**檢視 ()：您的應用程式用來動態產生 HTML 回應的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="38e87-108">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="38e87-109">**C**控制器 ()：處理傳入瀏覽器要求、抓取模型資料，然後指定會傳回瀏覽器回應的視圖範本的類別。</span><span class="sxs-lookup"><span data-stu-id="38e87-109">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="38e87-110">我們將在此教學課程系列中涵蓋所有這些概念，並示範如何使用它們來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="38e87-110">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="38e87-111">讓我們從建立控制器類別開始。</span><span class="sxs-lookup"><span data-stu-id="38e87-111">Let's begin by creating a controller class.</span></span> <span data-ttu-id="38e87-112">在**方案總管**中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後依序按一下 [**新增**]、[**控制器**]。</span><span class="sxs-lookup"><span data-stu-id="38e87-112">In **Solution Explorer**, right-click the *Controllers* folder and then click **Add**, then **Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="38e87-113">在 [**新增 Scaffold** ] 對話方塊中，按一下 [ **MVC 5 控制器-空白**]，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="38e87-113">In the **Add Scaffold** dialog box, click **MVC 5 Controller - Empty**, and then click **Add**.</span></span>

![](adding-a-controller/_static/image2.png)  

<span data-ttu-id="38e87-114">將新的控制器命名為 "HelloWorldController"，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="38e87-114">Name your new controller "HelloWorldController" and click **Add**.</span></span>

![新增控制器](adding-a-controller/_static/image3.png)

<span data-ttu-id="38e87-116">請注意，在**方案總管**中，已建立名為*HelloWorldController.cs*的新檔案和新的資料夾*Views\HelloWorld*。</span><span class="sxs-lookup"><span data-stu-id="38e87-116">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs* and a new folder *Views\HelloWorld*.</span></span> <span data-ttu-id="38e87-117">控制器已在 IDE 中開啟。</span><span class="sxs-lookup"><span data-stu-id="38e87-117">The controller is open in the IDE.</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="38e87-118">以下列程式碼取代檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="38e87-118">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="38e87-119">控制器方法會傳回 HTML 字串做為範例。</span><span class="sxs-lookup"><span data-stu-id="38e87-119">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="38e87-120">控制器的名稱為 `HelloWorldController`，而第一個方法的名稱為 `Index`。</span><span class="sxs-lookup"><span data-stu-id="38e87-120">The controller is named `HelloWorldController` and the first method is named `Index`.</span></span> <span data-ttu-id="38e87-121">讓我們從瀏覽器叫用它。</span><span class="sxs-lookup"><span data-stu-id="38e87-121">Let's invoke it from a browser.</span></span> <span data-ttu-id="38e87-122">執行應用程式（按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="38e87-122">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="38e87-123">在瀏覽器中，將 &quot;HelloWorld&quot; 附加至網址列中的路徑。</span><span class="sxs-lookup"><span data-stu-id="38e87-123">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="38e87-124">（例如，在下圖中，它是 `http://localhost:1234/HelloWorld.`）瀏覽器中的頁面看起來會如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="38e87-124">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="38e87-125">在上述方法中，程式碼會直接傳回字串。</span><span class="sxs-lookup"><span data-stu-id="38e87-125">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="38e87-126">您已告訴系統只傳回一些 HTML，而且的確有！</span><span class="sxs-lookup"><span data-stu-id="38e87-126">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="38e87-127">ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。</span><span class="sxs-lookup"><span data-stu-id="38e87-127">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="38e87-128">ASP.NET MVC 使用的預設 URL 路由邏輯會使用類似如下的格式來判斷要叫用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="38e87-128">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="38e87-129">您可以在應用程式中設定路由的格式， *\_啟動/RouteConfig .cs*檔案。</span><span class="sxs-lookup"><span data-stu-id="38e87-129">You set the format for routing in the *App\_Start/RouteConfig.cs* file.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs?highlight=7-8)]

<span data-ttu-id="38e87-130">當您執行應用程式但未提供任何 URL 區段時，它會預設為上述程式碼的 [預設值] 區段中所指定的 "Home" 控制器和 "Index" 動作方法。</span><span class="sxs-lookup"><span data-stu-id="38e87-130">When you run the application and don't supply any URL segments, it defaults to the "Home" controller and the "Index" action method specified in the defaults section of the code above.</span></span>

<span data-ttu-id="38e87-131">URL 的第一個部分會決定要執行的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="38e87-131">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="38e87-132">因此， */HelloWorld*會對應至 `HelloWorldController` 類別。</span><span class="sxs-lookup"><span data-stu-id="38e87-132">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="38e87-133">URL 的第二個部分會決定要執行的類別上的動作方法。</span><span class="sxs-lookup"><span data-stu-id="38e87-133">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="38e87-134">因此， */HelloWorld/Index*會導致 `HelloWorldController` 類別的 `Index` 方法執行。</span><span class="sxs-lookup"><span data-stu-id="38e87-134">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="38e87-135">請注意，我們只需要流覽至 */HelloWorld* ，預設會使用 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="38e87-135">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="38e87-136">這是因為名為 `Index` 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。</span><span class="sxs-lookup"><span data-stu-id="38e87-136">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span> <span data-ttu-id="38e87-137">URL 區段的第三個部分 (`Parameters`) 是路由資料。</span><span class="sxs-lookup"><span data-stu-id="38e87-137">The third part of the URL segment ( `Parameters`) is for route data.</span></span> <span data-ttu-id="38e87-138">我們稍後會在本教學課程中看到路由資料。</span><span class="sxs-lookup"><span data-stu-id="38e87-138">We'll see route data later on in this tutorial.</span></span>

<span data-ttu-id="38e87-139">瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="38e87-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="38e87-140">`Welcome` 方法會執行並傳回字串 &quot;這是歡迎動作方法 ...&quot;。</span><span class="sxs-lookup"><span data-stu-id="38e87-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="38e87-141">預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="38e87-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="38e87-142">在此 URL 中，控制器是 `HelloWorld`，而 `Welcome` 是動作方法。</span><span class="sxs-lookup"><span data-stu-id="38e87-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="38e87-143">您尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="38e87-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="38e87-144">讓我們稍微修改範例，讓您可以將 URL 中的某些參數資訊傳遞至控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4*）。</span><span class="sxs-lookup"><span data-stu-id="38e87-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="38e87-145">變更您的 `Welcome` 方法，使其包含兩個參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="38e87-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="38e87-146">請注意，程式碼會C#使用選擇性參數功能，表示如果未針對該參數傳遞任何值，則 `numTimes` 參數應預設為1。</span><span class="sxs-lookup"><span data-stu-id="38e87-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample3.cs)]

> [!NOTE]
> <span data-ttu-id="38e87-147">安全性注意事項：上述程式碼會使用[HTTPutility.htmlencode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx)來保護應用程式免于惡意的輸入（亦即 JavaScript）。</span><span class="sxs-lookup"><span data-stu-id="38e87-147">Security Note: The code above uses [HttpUtility.HtmlEncode](https://msdn.microsoft.com/library/ee360286(v=vs.110).aspx) to protect the application from malicious input (namely JavaScript).</span></span> <span data-ttu-id="38e87-148">如需詳細資訊，請參閱[如何：在 Web 應用程式中防止腳本惡意探索，方法是將 HTML 編碼套用至字串](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx)。</span><span class="sxs-lookup"><span data-stu-id="38e87-148">For more information see [How to: Protect Against Script Exploits in a Web Application by Applying HTML Encoding to Strings](https://msdn.microsoft.com/library/a2a4yykt(v=vs.100).aspx).</span></span>

 <span data-ttu-id="38e87-149">執行您的應用程式，並流覽至範例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`）。</span><span class="sxs-lookup"><span data-stu-id="38e87-149">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`).</span></span> <span data-ttu-id="38e87-150">您可以在 URL 中針對 `name` 和 `numtimes` 嘗試不同的值。</span><span class="sxs-lookup"><span data-stu-id="38e87-150">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="38e87-151">[ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將來自網址列中的查詢字串的已具名引數對應至方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="38e87-151">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="38e87-152">在上述範例中，不會使用 URL 區段（`Parameters`），`name` 和 `numTimes` 參數會當做[查詢字串](http://en.wikipedia.org/wiki/Query_string)傳遞。</span><span class="sxs-lookup"><span data-stu-id="38e87-152">In the sample above, the URL segment ( `Parameters`) is not used, the `name` and `numTimes` parameters are passed as [query strings](http://en.wikipedia.org/wiki/Query_string).</span></span> <span data-ttu-id="38e87-153">?</span><span class="sxs-lookup"><span data-stu-id="38e87-153">The ?</span></span> <span data-ttu-id="38e87-154">上述 URL 中的（問號）是分隔符號，而且查詢字串會跟著。</span><span class="sxs-lookup"><span data-stu-id="38e87-154">(question mark) in the above URL is a separator, and the query strings follow.</span></span> <span data-ttu-id="38e87-155">&amp; 字元可分隔查詢字串。</span><span class="sxs-lookup"><span data-stu-id="38e87-155">The &amp; character separates query strings.</span></span>

<span data-ttu-id="38e87-156">使用下列程式碼取代歡迎方法：</span><span class="sxs-lookup"><span data-stu-id="38e87-156">Replace the Welcome method with the following code:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample4.cs)]

<span data-ttu-id="38e87-157">執行應用程式，並輸入下列 URL： `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span><span class="sxs-lookup"><span data-stu-id="38e87-157">Run the application and enter the following URL: `http://localhost:xxx/HelloWorld/Welcome/1?name=Scott`</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="38e87-158">這次第三個 URL 區段符合路由參數 `ID.` `Welcome` 動作方法包含符合 `RegisterRoutes` 方法中 URL 規格的參數（`ID`）。</span><span class="sxs-lookup"><span data-stu-id="38e87-158">This time the third URL segment matched the route parameter `ID.` The `Welcome` action method contains a parameter (`ID`) that matched the URL specification in the `RegisterRoutes` method.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample5.cs?highlight=7)]

<span data-ttu-id="38e87-159">在 ASP.NET MVC 應用程式中，較常見的方式是將參數當做路由資料傳遞（像是上述的識別碼），而不是將它們當做查詢字串傳遞。</span><span class="sxs-lookup"><span data-stu-id="38e87-159">In ASP.NET MVC applications, it's more typical to pass in parameters as route data (like we did with ID above) than passing them as query strings.</span></span> <span data-ttu-id="38e87-160">您也可以新增路由，以將參數中的 `name` 和 `numtimes` 傳遞至 URL 中的路由資料。</span><span class="sxs-lookup"><span data-stu-id="38e87-160">You could also add a route to pass both the `name` and `numtimes` in parameters as route data in the URL.</span></span> <span data-ttu-id="38e87-161">在*應用程式\_Start\RouteConfig.cs*檔案中，新增 "Hello" 路由：</span><span class="sxs-lookup"><span data-stu-id="38e87-161">In the *App\_Start\RouteConfig.cs* file, add the "Hello" route:</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample6.cs?highlight=13-16)]

<span data-ttu-id="38e87-162">執行應用程式，並流覽至 `/localhost:XXX/HelloWorld/Welcome/Scott/3`。</span><span class="sxs-lookup"><span data-stu-id="38e87-162">Run the application and browse to `/localhost:XXX/HelloWorld/Welcome/Scott/3`.</span></span>

![](adding-a-controller/_static/image9.png)

<span data-ttu-id="38e87-163">對於許多 MVC 應用程式而言，預設路由運作正常。</span><span class="sxs-lookup"><span data-stu-id="38e87-163">For many MVC applications, the default route works fine.</span></span> <span data-ttu-id="38e87-164">您稍後會在本教學課程中瞭解如何使用模型系結器來傳遞資料，而且您不需要修改該的預設路由。</span><span class="sxs-lookup"><span data-stu-id="38e87-164">You'll learn later in this tutorial to pass data using the model binder, and you won't have to modify the default route for that.</span></span>

<span data-ttu-id="38e87-165">在這些範例中，控制器已執行 MVC 的 &quot;VC&quot; 部分，也就是視圖和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="38e87-165">In these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="38e87-166">控制器會直接傳回 HTML。</span><span class="sxs-lookup"><span data-stu-id="38e87-166">The controller is returning HTML directly.</span></span> <span data-ttu-id="38e87-167">一般來說，您不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。</span><span class="sxs-lookup"><span data-stu-id="38e87-167">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="38e87-168">相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="38e87-168">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="38e87-169">我們來看一下如何執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="38e87-169">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="38e87-170">[上一頁](getting-started.md)
> [下一頁](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="38e87-170">[Previous](getting-started.md)
[Next](adding-a-view.md)</span></span>
