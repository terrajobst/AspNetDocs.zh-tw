---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
title: 新增控制器（C#） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 0b8c56b5-fdf3-42dd-a866-98fbe0ab78a0
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/cs/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 959116ff773f4ef466cda6b172e8321590b50e5b
ms.sourcegitcommit: 7709c0a091b8d55b7b33bad8849f7b66b23c3d72
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 02/19/2020
ms.locfileid: "77457819"
---
# <a name="adding-a-controller-c"></a><span data-ttu-id="28bc2-103">新增控制器 (C#)</span><span class="sxs-lookup"><span data-stu-id="28bc2-103">Adding a Controller (C#)</span></span>

<span data-ttu-id="28bc2-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="28bc2-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> > [!NOTE]
> > <span data-ttu-id="28bc2-105">本教學課程的更新版本可在[這裡](../../../getting-started/introduction/getting-started.md)取得，其中使用 ASP.NET MVC 5 和 Visual Studio 2013。</span><span class="sxs-lookup"><span data-stu-id="28bc2-105">An updated version of this tutorial is available [here](../../../getting-started/introduction/getting-started.md) that uses ASP.NET MVC 5 and Visual Studio 2013.</span></span> <span data-ttu-id="28bc2-106">它更安全、更容易遵循，並示範更多功能。</span><span class="sxs-lookup"><span data-stu-id="28bc2-106">It's more secure, much simpler to follow and demonstrates more features.</span></span>
> 
> 
> <span data-ttu-id="28bc2-107">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="28bc2-107">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="28bc2-108">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="28bc2-108">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="28bc2-109">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="28bc2-109">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="28bc2-110">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="28bc2-110">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="28bc2-111">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="28bc2-111">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="28bc2-112">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="28bc2-112">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="28bc2-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="28bc2-113">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="28bc2-114">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="28bc2-114">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="28bc2-115">本主題提供具有C#原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="28bc2-115">A Visual Web Developer project with C# source code is available to accompany this topic.</span></span> <span data-ttu-id="28bc2-116">[下載C#版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="28bc2-116">[Download the C# version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="28bc2-117">如果您偏好 Visual Basic，請切換到本教學課程的[Visual Basic 版本](../vb/intro-to-aspnet-mvc-3.md)。</span><span class="sxs-lookup"><span data-stu-id="28bc2-117">If you prefer Visual Basic, switch to the [Visual Basic version](../vb/intro-to-aspnet-mvc-3.md) of this tutorial.</span></span>

<span data-ttu-id="28bc2-118">MVC 代表*模型視圖控制器*。</span><span class="sxs-lookup"><span data-stu-id="28bc2-118">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="28bc2-119">MVC 是一種模式，可用於開發架構良好且易於維護的應用程式。</span><span class="sxs-lookup"><span data-stu-id="28bc2-119">MVC is a pattern for developing applications that are well architected and easy to maintain.</span></span> <span data-ttu-id="28bc2-120">以 MVC 為基礎的應用程式包含：</span><span class="sxs-lookup"><span data-stu-id="28bc2-120">MVC-based applications contain:</span></span>

- <span data-ttu-id="28bc2-121">控制器：處理應用程式的傳入要求、抓取模型資料，然後指定將回應傳回給用戶端之視圖範本的類別。</span><span class="sxs-lookup"><span data-stu-id="28bc2-121">Controllers: Classes that handle incoming requests to the application, retrieve model data, and then specify view templates that return a response to the client.</span></span>
- <span data-ttu-id="28bc2-122">模型：代表應用程式資料的類別，並使用驗證邏輯來強制執行該資料的商務規則。</span><span class="sxs-lookup"><span data-stu-id="28bc2-122">Models: Classes that represent the data of the application and that use validation logic to enforce business rules for that data.</span></span>
- <span data-ttu-id="28bc2-123">Views：您的應用程式用來動態產生 HTML 回應的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="28bc2-123">Views: Template files that your application uses to dynamically generate HTML responses.</span></span>

<span data-ttu-id="28bc2-124">我們將在此教學課程系列中涵蓋所有這些概念，並示範如何使用它們來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="28bc2-124">We'll be covering all these concepts in this tutorial series and show you how to use them to build an application.</span></span>

<span data-ttu-id="28bc2-125">讓我們從建立控制器類別開始。</span><span class="sxs-lookup"><span data-stu-id="28bc2-125">Let's begin by creating a controller class.</span></span> <span data-ttu-id="28bc2-126">在**方案總管**中，以滑鼠右鍵按一下 [*控制器*] 資料夾，然後選取 [**新增控制器**]。</span><span class="sxs-lookup"><span data-stu-id="28bc2-126">In **Solution Explorer**, right-click the *Controllers* folder and then select **Add Controller**.</span></span>

[![](adding-a-controller/_static/image2.png)](adding-a-controller/_static/image1.png)

<span data-ttu-id="28bc2-127">將新的控制器命名為 "HelloWorldController"。</span><span class="sxs-lookup"><span data-stu-id="28bc2-127">Name your new controller "HelloWorldController".</span></span> <span data-ttu-id="28bc2-128">將 [預設範本] 保留為**空白控制器**，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="28bc2-128">Leave the default template as **Empty controller** and click **Add**.</span></span>

<span data-ttu-id="28bc2-129">[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="28bc2-129">[![AddHelloWorldController](adding-a-controller/_static/image4.png)](adding-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="28bc2-130">請注意，在**方案總管**中，已建立名為*HelloWorldController.cs*的新檔案。</span><span class="sxs-lookup"><span data-stu-id="28bc2-130">Notice in **Solution Explorer** that a new file has been created named *HelloWorldController.cs*.</span></span> <span data-ttu-id="28bc2-131">檔案已在 IDE 中開啟。</span><span class="sxs-lookup"><span data-stu-id="28bc2-131">The file is open in the IDE.</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="28bc2-132">在 `public class HelloWorldController` 區塊內，建立兩個類似下列程式碼的方法。</span><span class="sxs-lookup"><span data-stu-id="28bc2-132">Inside the `public class HelloWorldController` block, create two methods that look like the following code.</span></span> <span data-ttu-id="28bc2-133">控制器會傳回 HTML 字串做為範例。</span><span class="sxs-lookup"><span data-stu-id="28bc2-133">The controller will return a string of HTML as an example.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample1.cs)]

<span data-ttu-id="28bc2-134">您的控制器命名為 `HelloWorldController`，而上述第一個方法的名稱為 `Index`。</span><span class="sxs-lookup"><span data-stu-id="28bc2-134">Your controller is named `HelloWorldController` and the first method above is named `Index`.</span></span> <span data-ttu-id="28bc2-135">讓我們從瀏覽器叫用它。</span><span class="sxs-lookup"><span data-stu-id="28bc2-135">Let's invoke it from a browser.</span></span> <span data-ttu-id="28bc2-136">執行應用程式（按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="28bc2-136">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="28bc2-137">在瀏覽器中，將 "HelloWorld" 附加至網址列中的路徑。</span><span class="sxs-lookup"><span data-stu-id="28bc2-137">In the browser, append "HelloWorld" to the path in the address bar.</span></span> <span data-ttu-id="28bc2-138">（例如，在下圖中，它是 `http://localhost:43246/HelloWorld.`）瀏覽器中的頁面看起來會如下列螢幕擷取畫面所示。</span><span class="sxs-lookup"><span data-stu-id="28bc2-138">(For example, in the illustration below, it's `http://localhost:43246/HelloWorld.`) The page in the browser will look like the following screenshot.</span></span> <span data-ttu-id="28bc2-139">在上述方法中，程式碼會直接傳回字串。</span><span class="sxs-lookup"><span data-stu-id="28bc2-139">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="28bc2-140">您已告訴系統只傳回一些 HTML，而且的確有！</span><span class="sxs-lookup"><span data-stu-id="28bc2-140">You told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="28bc2-141">ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。</span><span class="sxs-lookup"><span data-stu-id="28bc2-141">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="28bc2-142">ASP.NET MVC 使用的預設對應邏輯會使用類似如下的格式來判斷要叫用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="28bc2-142">The default mapping logic used by ASP.NET MVC uses a format like this to determine what code to invoke:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="28bc2-143">URL 的第一個部分會決定要執行的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="28bc2-143">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="28bc2-144">因此， */HelloWorld*會對應至 `HelloWorldController` 類別。</span><span class="sxs-lookup"><span data-stu-id="28bc2-144">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="28bc2-145">URL 的第二個部分會決定要執行的類別上的動作方法。</span><span class="sxs-lookup"><span data-stu-id="28bc2-145">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="28bc2-146">因此， */HelloWorld/Index*會導致 `HelloWorldController` 類別的 `Index` 方法執行。</span><span class="sxs-lookup"><span data-stu-id="28bc2-146">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="28bc2-147">請注意，我們只需要流覽至 */HelloWorld* ，預設會使用 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="28bc2-147">Notice that we only had to browse to */HelloWorld* and the `Index` method was used by default.</span></span> <span data-ttu-id="28bc2-148">這是因為名為 `Index` 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。</span><span class="sxs-lookup"><span data-stu-id="28bc2-148">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="28bc2-149">瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="28bc2-149">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="28bc2-150">`Welcome` 方法隨即執行，並傳回字串 "This is the Welcome action method..."。</span><span class="sxs-lookup"><span data-stu-id="28bc2-150">The `Welcome` method runs and returns the string "This is the Welcome action method...".</span></span> <span data-ttu-id="28bc2-151">預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="28bc2-151">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="28bc2-152">在此 URL 中，控制器是 `HelloWorld`，而 `Welcome` 是動作方法。</span><span class="sxs-lookup"><span data-stu-id="28bc2-152">For this URL, the controller is `HelloWorld` and `Welcome` is the action method.</span></span> <span data-ttu-id="28bc2-153">您尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="28bc2-153">You haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="28bc2-154">讓我們稍微修改範例，讓您可以將 URL 中的某些參數資訊傳遞至控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4*）。</span><span class="sxs-lookup"><span data-stu-id="28bc2-154">Let's modify the example slightly so that you can pass some parameter information from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="28bc2-155">變更您的 `Welcome` 方法，使其包含兩個參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="28bc2-155">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="28bc2-156">請注意，程式碼會C#使用選擇性參數功能，表示如果未針對該參數傳遞任何值，則 `numTimes` 參數應預設為1。</span><span class="sxs-lookup"><span data-stu-id="28bc2-156">Note that the code uses the C# optional-parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-csharp[Main](adding-a-controller/samples/sample2.cs)]

<span data-ttu-id="28bc2-157">執行您的應用程式，並流覽至範例 URL （`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`。</span><span class="sxs-lookup"><span data-stu-id="28bc2-157">Run your application and browse to the example URL (`http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4)`.</span></span> <span data-ttu-id="28bc2-158">您可以在 URL 中針對 `name` 和 `numtimes` 嘗試不同的值。</span><span class="sxs-lookup"><span data-stu-id="28bc2-158">You can try different values for `name` and `numtimes` in the URL.</span></span> <span data-ttu-id="28bc2-159">系統會自動將來自網址列中的查詢字串的已具名引數對應至方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="28bc2-159">The system automatically maps the named parameters from the query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image8.png)

<span data-ttu-id="28bc2-160">在這兩個範例中，控制器已執行 MVC 的 "VC" 部分，也就是視圖和控制器工作。</span><span class="sxs-lookup"><span data-stu-id="28bc2-160">In both these examples the controller has been doing the "VC" portion of MVC — that is, the view and controller work.</span></span> <span data-ttu-id="28bc2-161">控制器會直接傳回 HTML。</span><span class="sxs-lookup"><span data-stu-id="28bc2-161">The controller is returning HTML directly.</span></span> <span data-ttu-id="28bc2-162">一般來說，您不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。</span><span class="sxs-lookup"><span data-stu-id="28bc2-162">Ordinarily you don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="28bc2-163">相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="28bc2-163">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="28bc2-164">我們來看一下如何執行這個動作。</span><span class="sxs-lookup"><span data-stu-id="28bc2-164">Let's look next at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="28bc2-165">[上一頁](intro-to-aspnet-mvc-3.md)
> [下一頁](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="28bc2-165">[Previous](intro-to-aspnet-mvc-3.md)
[Next](adding-a-view.md)</span></span>
