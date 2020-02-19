---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
title: 新增控制器 |Microsoft Docs
author: Rick-Anderson
description: 注意：本教學課程的更新版本可在這裡使用 ASP.NET MVC 5 和 Visual Studio 2013。 更安全、更容易遵循和示範 。
ms.author: riande
ms.date: 08/28/2012
ms.assetid: 0267d31c-892f-49a1-9e7a-3ae8cc12b2ca
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc4/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: f528c56435976c7f31fce453c834ef9eaebe6244
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77456097"
---
# <a name="adding-a-controller"></a><span data-ttu-id="311e1-104">加入控制器</span><span class="sxs-lookup"><span data-stu-id="311e1-104">Adding a Controller</span></span>

<span data-ttu-id="311e1-105">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="311e1-105">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="311e1-106">本教學課程的更新版本可在[這裡](../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="311e1-106">An updated version of this tutorial is available [here](../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="311e1-107">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="311e1-107">It's more secure, much simpler to follow and demonstrates more features.</span></span>

<span data-ttu-id="311e1-108">MVC 代表*模型視圖控制器*。</span><span class="sxs-lookup"><span data-stu-id="311e1-108">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="311e1-109">MVC 是一種模式，可供開發良好架構、可測試且易於維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="311e1-109">MVC is a pattern for developing applications that are well architected, testable and easy to maintain.</span></span> <span data-ttu-id="311e1-110">以 MVC 為基礎的應用程式包含：</span><span class="sxs-lookup"><span data-stu-id="311e1-110">MVC-based applications contain:</span></span>

- <span data-ttu-id="311e1-111">**M**模型 ()：代表應用程式資料的類別，並使用驗證邏輯來強制執行該資料的商務規則。</span><span class="sxs-lookup"><span data-stu-id="311e1-111">**M** odels: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="311e1-112">**V**檢視 ()：您的應用程式用來動態產生 HTML 回應的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="311e1-112">**V** iews: Template files that your application uses to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="311e1-113">**C**控制器 ()：處理傳入瀏覽器要求、抓取模型資料，然後指定會傳回瀏覽器回應的視圖範本的類別。</span><span class="sxs-lookup"><span data-stu-id="311e1-113">**C** ontrollers: Classes that handle incoming browser requests, retrieve model data, and then specify view templates that return a response to the browser.</span></span>

<span data-ttu-id="311e1-114">我們將在此教學課程系列中涵蓋所有這些概念，並示範如何使用它們來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="311e1-114">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="311e1-115">讓我們從建立控制器類別開始。</span><span class="sxs-lookup"><span data-stu-id="311e1-115">Let's begin by creating a controller class.</span></span> <span data-ttu-id="311e1-116">在**方案總管**中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後選取 [**新增控制器**]。</span><span class="sxs-lookup"><span data-stu-id="311e1-116">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

![](adding-a-controller/_static/image1.png)

<span data-ttu-id="311e1-117">將新的控制器命名為 &quot;HelloWorldController&quot;。</span><span class="sxs-lookup"><span data-stu-id="311e1-117">Name your new controller &quot;HelloWorldController&quot;.</span></span> <span data-ttu-id="311e1-118">將預設範本保留為**空白的 MVC 控制器**，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="311e1-118">Leave the default template as **Empty MVC controller** and click **Add**.</span></span>

![新增控制器](adding-a-controller/_static/image2.png)

<span data-ttu-id="311e1-120">請注意，在**方案總管**中，已建立名為*HelloWorldController.cs*的新檔案。</span><span class="sxs-lookup"><span data-stu-id="311e1-120">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="311e1-121">檔案已在 IDE 中開啟。</span><span class="sxs-lookup"><span data-stu-id="311e1-121">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image3.png)

<span data-ttu-id="311e1-122">以下列程式碼取代檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="311e1-122">Replace the contents of the file with the following code.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="311e1-123">控制器方法會傳回 HTML 字串做為範例。</span><span class="sxs-lookup"><span data-stu-id="311e1-123">The controller methods will return a string of HTML as an example.</span></span> <span data-ttu-id="311e1-124">控制器的名稱為 `HelloWorldController`，而上述第一個方法的名稱為 `Index`。</span><span class="sxs-lookup"><span data-stu-id="311e1-124">The controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="311e1-125">讓我們從瀏覽器叫用它。</span><span class="sxs-lookup"><span data-stu-id="311e1-125">Let's invoke it from a browser.</span></span> <span data-ttu-id="311e1-126">執行應用程式（按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="311e1-126">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="311e1-127">在瀏覽器中，將 &quot;HelloWorld&quot; 附加至網址列中的路徑。</span><span class="sxs-lookup"><span data-stu-id="311e1-127">In the browser, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="311e1-128">（例如，在下圖中，它是 `http://localhost:1234/HelloWorld.`）瀏覽器中的頁面看起來會如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="311e1-128">(For example, in the illustration below, it's `http://localhost:1234/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="311e1-129">在上述方法中，程式碼會直接傳回字串。</span><span class="sxs-lookup"><span data-stu-id="311e1-129">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="311e1-130">您已告訴系統只傳回一些 HTML，而且的確有！</span><span class="sxs-lookup"><span data-stu-id="311e1-130">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image4.png)

<span data-ttu-id="311e1-131">ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。</span><span class="sxs-lookup"><span data-stu-id="311e1-131">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="311e1-132">ASP.NET MVC 使用的預設 URL 路由邏輯會使用類似如下的格式來判斷要叫用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="311e1-132">The default URL routing logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="311e1-133">URL 的第一個部分會決定要執行的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="311e1-133">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="311e1-134">因此， */HelloWorld*會對應至 `HelloWorldController` 類別。</span><span class="sxs-lookup"><span data-stu-id="311e1-134">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="311e1-135">URL 的第二個部分會決定要執行的類別上的動作方法。</span><span class="sxs-lookup"><span data-stu-id="311e1-135">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="311e1-136">因此， */HelloWorld/Index*會導致 `HelloWorldController` 類別的 `Index` 方法執行。</span><span class="sxs-lookup"><span data-stu-id="311e1-136">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="311e1-137">請注意，我們只需要流覽至 */HelloWorld* ，預設會使用 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="311e1-137">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="311e1-138">這是因為名為 `Index` 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。</span><span class="sxs-lookup"><span data-stu-id="311e1-138">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="311e1-139">瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="311e1-139">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="311e1-140">`Welcome` 方法會執行並傳回字串 &quot;這是歡迎動作方法 ...&quot;。</span><span class="sxs-lookup"><span data-stu-id="311e1-140">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="311e1-141">預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="311e1-141">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="311e1-142">在此 URL 中，控制器是 `HelloWorld`，而 `Welcome` 是動作方法。</span><span class="sxs-lookup"><span data-stu-id="311e1-142">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="311e1-143">您尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="311e1-143">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="311e1-144">讓我們稍微修改範例，讓您可以將 URL 中的某些參數資訊傳遞至控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4*）。</span><span class="sxs-lookup"><span data-stu-id="311e1-144">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="311e1-145">變更您的 `Welcome` 方法，使其包含兩個參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="311e1-145">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="311e1-146">請注意，程式碼會C#使用選擇性參數功能，表示如果未針對該參數傳遞任何值，則 `numTimes` 參數應預設為1。</span><span class="sxs-lookup"><span data-stu-id="311e1-146">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="311e1-147">執行您的應用程式，並流覽至範例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。</span><span class="sxs-lookup"><span data-stu-id="311e1-147">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="311e1-148">您可以在 URL 中針對 `name` 和 `numtimes` 嘗試不同的值。</span><span class="sxs-lookup"><span data-stu-id="311e1-148">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="311e1-149">[ASP.NET MVC 模型](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx)系結系統會自動將來自網址列中的查詢字串的已具名引數對應至方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="311e1-149">The [ASP.NET MVC model binding system](http://odetocode.com/Blogs/scott/archive/2009/04/27/6-tips-for-asp-net-mvc-model-binding.aspx) automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="311e1-150">在這兩個範例中，控制器已執行 MVC 的 &quot;VC&quot; 部分，也就是視圖和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="311e1-150">In both these examples the controller has been doing the &quot;VC&quot; portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="311e1-151">控制器會直接傳回 HTML。</span><span class="sxs-lookup"><span data-stu-id="311e1-151">The controller is returning HTML directly.</span></span> <span data-ttu-id="311e1-152">一般來說，您不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。</span><span class="sxs-lookup"><span data-stu-id="311e1-152">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="311e1-153">相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="311e1-153">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="311e1-154">我們來看一下如何執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="311e1-154">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="311e1-155">[上一頁](intro-to-aspnet-mvc-4.md)
> [下一頁](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="311e1-155">[Previous](intro-to-aspnet-mvc-4.md)
[Next](adding-a-view.md)</span></span>
