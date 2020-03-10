---
uid: mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
title: 新增控制器（VB） |Microsoft Docs
author: Rick-Anderson
description: 本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，也就是 。
ms.author: riande
ms.date: 01/12/2011
ms.assetid: 741259e1-54ac-4f71-b4e8-2bd5560bb950
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-aspnet-mvc3/vb/adding-a-controller
msc.type: authoredcontent
ms.openlocfilehash: 2e77f62a9796211b0e59a99c71bc532659b7cb92
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78540513"
---
# <a name="adding-a-controller-vb"></a><span data-ttu-id="1fac6-103">新增控制器 (VB)</span><span class="sxs-lookup"><span data-stu-id="1fac6-103">Adding a Controller (VB)</span></span>

<span data-ttu-id="1fac6-104">依[Rick Anderson](https://twitter.com/RickAndMSFT)</span><span class="sxs-lookup"><span data-stu-id="1fac6-104">by [Rick Anderson](https://twitter.com/RickAndMSFT)</span></span>

> <span data-ttu-id="1fac6-105">本教學課程將告訴您使用 Microsoft Visual Web Developer 2010 Express Service Pack 1 建立 ASP.NET MVC Web 應用程式的基本概念，這是 Microsoft Visual Studio 的免費版本。</span><span class="sxs-lookup"><span data-stu-id="1fac6-105">This tutorial will teach you the basics of building an ASP.NET MVC Web application using Microsoft Visual Web Developer 2010 Express Service Pack 1, which is a free version of Microsoft Visual Studio.</span></span> <span data-ttu-id="1fac6-106">開始之前，請先確定您已安裝下列必要條件。</span><span class="sxs-lookup"><span data-stu-id="1fac6-106">Before you start, make sure you've installed the prerequisites listed below.</span></span> <span data-ttu-id="1fac6-107">您可以按一下下列連結來安裝所有這些專案： [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="1fac6-107">You can install all of them by clicking the following link: [Web Platform Installer](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack).</span></span> <span data-ttu-id="1fac6-108">或者，您可以使用下列連結個別安裝必要條件：</span><span class="sxs-lookup"><span data-stu-id="1fac6-108">Alternatively, you can individually install the prerequisites using the following links:</span></span>
> 
> - [<span data-ttu-id="1fac6-109">Visual Studio Web Developer Express SP1 必要條件</span><span class="sxs-lookup"><span data-stu-id="1fac6-109">Visual Studio Web Developer Express SP1 prerequisites</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appid=VWD2010SP1Pack)
> - [<span data-ttu-id="1fac6-110">ASP.NET MVC 3 工具更新</span><span class="sxs-lookup"><span data-stu-id="1fac6-110">ASP.NET MVC 3 Tools Update</span></span>](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=MVC3)
> - <span data-ttu-id="1fac6-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)（執行時間 + 工具支援）</span><span class="sxs-lookup"><span data-stu-id="1fac6-111">[SQL Server Compact 4.0](https://www.microsoft.com/web/gallery/install.aspx?appid=SQLCE;SQLCEVSTools_4_0)(runtime + tools support)</span></span>
> 
> <span data-ttu-id="1fac6-112">如果您使用 Visual Studio 2010，而不是 Visual Web Developer 2010，請按一下下列連結來安裝必要條件： [Visual Studio 2010 必要條件](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack)。</span><span class="sxs-lookup"><span data-stu-id="1fac6-112">If you're using Visual Studio 2010 instead of Visual Web Developer 2010, install the prerequisites by clicking the following link: [Visual Studio 2010 prerequisites](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=VS2010SP1Pack).</span></span>
> 
> <span data-ttu-id="1fac6-113">本主題提供具有 VB.NET 原始程式碼的 Visual Web Developer 專案。</span><span class="sxs-lookup"><span data-stu-id="1fac6-113">A Visual Web Developer project with VB.NET source code is available to accompany this topic.</span></span> <span data-ttu-id="1fac6-114">[下載 VB.NET 版本](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098)。</span><span class="sxs-lookup"><span data-stu-id="1fac6-114">[Download the VB.NET version](https://code.msdn.microsoft.com/Introduction-to-MVC-3-10d1b098).</span></span> <span data-ttu-id="1fac6-115">如果您想C#要的話，請切換到本教學課程的[ C#版本](../cs/adding-a-controller.md)。</span><span class="sxs-lookup"><span data-stu-id="1fac6-115">If you prefer C#, switch to the [C# version](../cs/adding-a-controller.md) of this tutorial.</span></span>

<span data-ttu-id="1fac6-116">MVC 代表*模型視圖控制器*。</span><span class="sxs-lookup"><span data-stu-id="1fac6-116">MVC stands for *model-view-controller*.</span></span> <span data-ttu-id="1fac6-117">MVC 是用來開發應用程式的模式，因此每個元件都有個別的責任：</span><span class="sxs-lookup"><span data-stu-id="1fac6-117">MVC is a pattern for developing applications such that each part has a separate responsibility:</span></span>

- <span data-ttu-id="1fac6-118">模型：應用程式的資料。</span><span class="sxs-lookup"><span data-stu-id="1fac6-118">Model: The data for your application.</span></span>
- <span data-ttu-id="1fac6-119">Views：應用程式將用來動態產生 HTML 回應的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="1fac6-119">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="1fac6-120">控制器：處理應用程式傳入 URL 要求、抓取模型資料，然後指定將回應轉譯至用戶端的類別。</span><span class="sxs-lookup"><span data-stu-id="1fac6-120">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response to the client.</span></span>

<span data-ttu-id="1fac6-121">本教學課程將涵蓋所有這些概念，並示範如何使用它們來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="1fac6-121">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="1fac6-122">以滑鼠右鍵按一下**方案總管**中的 [*控制器*] 資料夾，然後選取 [新增**控制器**]，以建立新的控制器。</span><span class="sxs-lookup"><span data-stu-id="1fac6-122">Create a new controller by right-clicking the *Controllers* folder in **Solution Explorer** and then selecting **Add Controller**.</span></span>

<span data-ttu-id="1fac6-123">[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="1fac6-123">[![AddController](adding-a-controller/_static/image2.png "AddController")](adding-a-controller/_static/image1.png)</span></span>

<span data-ttu-id="1fac6-124">將新的控制器命名為 &quot;HelloWorldController&quot;，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="1fac6-124">Name your new controller &quot;HelloWorldController&quot; and click **Add**.</span></span>

<span data-ttu-id="1fac6-125">[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="1fac6-125">[![2AddEmptyController](adding-a-controller/_static/image4.png "2AddEmptyController")](adding-a-controller/_static/image3.png)</span></span>

<span data-ttu-id="1fac6-126">請注意，在右側**方案總管**中，已為您建立了名為*HelloWorldController.cs*的新檔案，而且該檔案已在 IDE 中開啟。</span><span class="sxs-lookup"><span data-stu-id="1fac6-126">Notice in **Solution Explorer** on the right that a new file has been created for you named *HelloWorldController.cs* and that the file is open in the IDE.</span></span>

<span data-ttu-id="1fac6-127">在新的 `public class HelloWorldController` 區塊內，建立兩個新的方法，看起來像下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="1fac6-127">Inside the new `public class HelloWorldController` block, create two new methods that look like the following code.</span></span> <span data-ttu-id="1fac6-128">我們會直接從控制器傳回 HTML 字串作為範例。</span><span class="sxs-lookup"><span data-stu-id="1fac6-128">We'll return a string of HTML directly from the controller as an example.</span></span>

[!code-vb[Main](adding-a-controller/samples/sample1.vb)]

<span data-ttu-id="1fac6-129">您的控制器命名為 `HelloWorldController`，而新方法的名稱為 `Index`。</span><span class="sxs-lookup"><span data-stu-id="1fac6-129">Your controller is named `HelloWorldController` and your new method is named `Index`.</span></span> <span data-ttu-id="1fac6-130">執行應用程式（按 F5 或 Ctrl + F5）。</span><span class="sxs-lookup"><span data-stu-id="1fac6-130">Run the application (press F5 or Ctrl+F5).</span></span> <span data-ttu-id="1fac6-131">當您的瀏覽器啟動之後，將 &quot;HelloWorld&quot; 附加至網址列中的路徑。</span><span class="sxs-lookup"><span data-stu-id="1fac6-131">Once your browser has started up, append &quot;HelloWorld&quot; to the path in the address bar.</span></span> <span data-ttu-id="1fac6-132">（在我的電腦上，它是 `http://localhost:43246/HelloWorld`）您的瀏覽器看起來會像下面的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="1fac6-132">(On my computer, it's `http://localhost:43246/HelloWorld`) Your browser will look like the screenshot below.</span></span> <span data-ttu-id="1fac6-133">在上述方法中，程式碼會直接傳回字串。</span><span class="sxs-lookup"><span data-stu-id="1fac6-133">In the method above, the code returned a string directly.</span></span> <span data-ttu-id="1fac6-134">我們已告訴系統只傳回一些 HTML，而且的確有！</span><span class="sxs-lookup"><span data-stu-id="1fac6-134">We told the system to just return some HTML, and it did!</span></span>

![](adding-a-controller/_static/image5.png)

<span data-ttu-id="1fac6-135">ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。</span><span class="sxs-lookup"><span data-stu-id="1fac6-135">ASP.NET MVC invokes different controller classes (and different action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="1fac6-136">ASP.NET MVC 使用的預設對應邏輯會使用類似如下的格式來控制要叫用的程式碼：</span><span class="sxs-lookup"><span data-stu-id="1fac6-136">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is invoked:</span></span>

`/[Controller]/[ActionName]/[Parameters]`

<span data-ttu-id="1fac6-137">URL 的第一個部分會決定要執行的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="1fac6-137">The first part of the URL determines the controller class to execute.</span></span> <span data-ttu-id="1fac6-138">因此， */HelloWorld*會對應至 `HelloWorldController` 類別。</span><span class="sxs-lookup"><span data-stu-id="1fac6-138">So */HelloWorld* maps to the `HelloWorldController` class.</span></span> <span data-ttu-id="1fac6-139">URL 的第二個部分會決定要執行的類別上的動作方法。</span><span class="sxs-lookup"><span data-stu-id="1fac6-139">The second part of the URL determines the action method on the class to execute.</span></span> <span data-ttu-id="1fac6-140">因此， */HelloWorld/Index*會導致 `HelloWorldController` 類別的 `Index` 方法執行。</span><span class="sxs-lookup"><span data-stu-id="1fac6-140">So */HelloWorld/Index* would cause the `Index` method of the `HelloWorldController` class to execute.</span></span> <span data-ttu-id="1fac6-141">請注意，我們只需要造訪上述 */HelloWorld* ，預設會使用 `Index` 方法。</span><span class="sxs-lookup"><span data-stu-id="1fac6-141">Notice that we only had to visit */HelloWorld* above and the `Index` method was used by default.</span></span> <span data-ttu-id="1fac6-142">這是因為名為 `Index` 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。</span><span class="sxs-lookup"><span data-stu-id="1fac6-142">This is because a method named `Index` is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="1fac6-143">瀏覽至 `http://localhost:xxxx/HelloWorld/Welcome`。</span><span class="sxs-lookup"><span data-stu-id="1fac6-143">Browse to `http://localhost:xxxx/HelloWorld/Welcome`.</span></span> <span data-ttu-id="1fac6-144">`Welcome` 方法會執行並傳回字串 &quot;這是歡迎動作方法 ...&quot;。</span><span class="sxs-lookup"><span data-stu-id="1fac6-144">The `Welcome` method runs and returns the string &quot;This is the Welcome action method...&quot;.</span></span> <span data-ttu-id="1fac6-145">預設 MVC 對應為 `/[Controller]/[ActionName]/[Parameters]`。</span><span class="sxs-lookup"><span data-stu-id="1fac6-145">The default MVC mapping is `/[Controller]/[ActionName]/[Parameters]`.</span></span> <span data-ttu-id="1fac6-146">針對此 URL，控制器會 `HelloWorld`，`Welcome` 是方法。</span><span class="sxs-lookup"><span data-stu-id="1fac6-146">For this URL, the controller is `HelloWorld` and `Welcome` is the method.</span></span> <span data-ttu-id="1fac6-147">尚未使用 URL 的 `[Parameters]` 部分。</span><span class="sxs-lookup"><span data-stu-id="1fac6-147">We haven't used the `[Parameters]` part of the URL yet.</span></span>

![](adding-a-controller/_static/image6.png)

<span data-ttu-id="1fac6-148">讓我們稍微修改範例，讓我們可以從 URL 將中的一些參數資訊傳遞到控制器（例如， */HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4*）。</span><span class="sxs-lookup"><span data-stu-id="1fac6-148">Let's modify the example slightly so that we can pass some parameter information in from the URL to the controller (for example, */HelloWorld/Welcome?name=Scott&amp;numtimes=4*).</span></span> <span data-ttu-id="1fac6-149">變更您的 `Welcome` 方法，使其包含兩個參數，如下所示。</span><span class="sxs-lookup"><span data-stu-id="1fac6-149">Change your `Welcome` method to include two parameters as shown below.</span></span> <span data-ttu-id="1fac6-150">請注意，我們使用了 VB 選擇性參數功能，表示如果未針對該參數傳遞任何值，則 `numTimes` 參數應預設為1。</span><span class="sxs-lookup"><span data-stu-id="1fac6-150">Note that we've used the VB optional parameter feature to indicate that the `numTimes` parameter should default to 1 if no value is passed for that parameter.</span></span>

[!code-vb[Main](adding-a-controller/samples/sample2.vb)]

<span data-ttu-id="1fac6-151">執行您的應用程式，並流覽至 `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4` **。**</span><span class="sxs-lookup"><span data-stu-id="1fac6-151">Run your application and browse to `http://localhost:xxxx/HelloWorld/Welcome?name=Scott&numtimes=4`**.**</span></span> <span data-ttu-id="1fac6-152">您可以嘗試不同的 `name` 和 `numtimes`值。</span><span class="sxs-lookup"><span data-stu-id="1fac6-152">You can try different values for `name` and `numtimes`.</span></span> <span data-ttu-id="1fac6-153">系統會自動將網址列中查詢字串的已具名引數對應至方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="1fac6-153">The system automatically maps the named parameters from your query string in the address bar to parameters in your method.</span></span>

![](adding-a-controller/_static/image7.png)

<span data-ttu-id="1fac6-154">在這兩個範例中，控制器已執行 MVC 的 VC 部分，也就是「視圖」和「控制器」工作。</span><span class="sxs-lookup"><span data-stu-id="1fac6-154">In both these examples the controller has been doing the VC portion of MVC — that is the view and controller work.</span></span> <span data-ttu-id="1fac6-155">控制器會直接傳回 HTML。</span><span class="sxs-lookup"><span data-stu-id="1fac6-155">The controller is returning HTML directly.</span></span> <span data-ttu-id="1fac6-156">一般來說，我們不希望控制器直接傳回 HTML，因為程式碼會變得很麻煩。</span><span class="sxs-lookup"><span data-stu-id="1fac6-156">Ordinarily we don't want controllers returning HTML directly, since that becomes very cumbersome to code.</span></span> <span data-ttu-id="1fac6-157">相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="1fac6-157">Instead we'll typically use a separate view template file to help generate the HTML response.</span></span> <span data-ttu-id="1fac6-158">我們來看一下如何做到這一點。</span><span class="sxs-lookup"><span data-stu-id="1fac6-158">Let's look at how we can do this.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1fac6-159">[上一頁](intro-to-aspnet-mvc-3.md)
> [下一頁](adding-a-view.md)</span><span class="sxs-lookup"><span data-stu-id="1fac6-159">[Previous](intro-to-aspnet-mvc-3.md)
[Next](adding-a-view.md)</span></span>
