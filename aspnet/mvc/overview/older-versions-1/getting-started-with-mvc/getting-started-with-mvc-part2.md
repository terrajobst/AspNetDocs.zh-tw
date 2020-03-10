---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
title: 新增控制器 |Microsoft Docs
author: shanselman
description: 如果本教學課程可在此使用 Visual Studio 2013，則為更新版本。 新的教學課程使用 ASP.NET MVC 5，它提供了許多透過 t 的改良功能 。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: ff03dcc0-da97-458d-838f-0823e7482642
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part2
msc.type: authoredcontent
ms.openlocfilehash: e2a298584473f57c2b14edf507f0f6886d906ea3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543978"
---
# <a name="adding-a-controller"></a><span data-ttu-id="58639-104">新增控制器</span><span class="sxs-lookup"><span data-stu-id="58639-104">Adding a Controller</span></span>

<span data-ttu-id="58639-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="58639-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> > [!NOTE]
> > <span data-ttu-id="58639-106">如果本教學[課程](../../getting-started/introduction/getting-started.md)可在此使用[Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013)，則為更新版本。</span><span class="sxs-lookup"><span data-stu-id="58639-106">An updated version if this tutorial is available [here](../../getting-started/introduction/getting-started.md) using [Visual Studio 2013](https://my.visualstudio.com/Downloads?q=visual%20studio%202013).</span></span> <span data-ttu-id="58639-107">新的教學課程會使用 ASP.NET MVC 5，這在此教學課程中提供了許多改進功能。</span><span class="sxs-lookup"><span data-stu-id="58639-107">The new tutorial uses ASP.NET MVC 5, which provides many improvements over this tutorial.</span></span>
>
>
> <span data-ttu-id="58639-108">這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="58639-108">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="58639-109">您將建立可從資料庫讀取和寫入的簡單 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="58639-109">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="58639-110">請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="58639-110">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="58639-111">MVC 代表 Model、View、Controller。</span><span class="sxs-lookup"><span data-stu-id="58639-111">MVC stands for Model, View, Controller.</span></span> <span data-ttu-id="58639-112">MVC 是用來開發應用程式的模式，因此每個部分的責任與另一個元件不同。</span><span class="sxs-lookup"><span data-stu-id="58639-112">MVC is a pattern for developing applications such that each part has a responsibility that is different from another.</span></span>

- <span data-ttu-id="58639-113">模型：應用程式的資料</span><span class="sxs-lookup"><span data-stu-id="58639-113">Model: The data of your application</span></span>
- <span data-ttu-id="58639-114">Views：應用程式將用來動態產生 HTML 回應的範本檔案。</span><span class="sxs-lookup"><span data-stu-id="58639-114">Views: The template files your application will use to dynamically generate HTML responses.</span></span>
- <span data-ttu-id="58639-115">控制器：處理應用程式傳入 URL 要求、捕獲模型資料，然後指定將回應轉譯回用戶端的類別</span><span class="sxs-lookup"><span data-stu-id="58639-115">Controllers: Classes that handle incoming URL requests to the application, retrieve model data, and then specify view templates that render a response back to the client</span></span>

<span data-ttu-id="58639-116">本教學課程將涵蓋所有這些概念，並示範如何使用它們來建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="58639-116">We'll be covering all these concepts in this tutorial and show you how to use them to build an application.</span></span>

<span data-ttu-id="58639-117">讓我們建立新的控制器，方法是以滑鼠右鍵按一下 [方案瀏覽器] 中的 [控制器] 資料夾，然後選取 [新增控制器]。</span><span class="sxs-lookup"><span data-stu-id="58639-117">Let's create a new controller by right-clicking the controllers folder in the solution Explorer and selecting Add Controller.</span></span>

<span data-ttu-id="58639-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="58639-118">[![AddControllerRightClick](getting-started-with-mvc-part2/_static/image2.png)](getting-started-with-mvc-part2/_static/image1.png)</span></span>

<span data-ttu-id="58639-119">將新的控制器命名為 "HelloWorldController"，然後按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="58639-119">Name your new controller "HelloWorldController" and click Add.</span></span>

<span data-ttu-id="58639-120">[![新增控制器 對話方塊](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="58639-120">[![Add Controller Dialog](getting-started-with-mvc-part2/_static/image4.png)](getting-started-with-mvc-part2/_static/image3.png)</span></span>

<span data-ttu-id="58639-121">請注意，在右邊的方案總管中，已為您建立了名為 HelloWorldController.cs 的新檔案，而該檔案現在已在**IDE**中開啟。</span><span class="sxs-lookup"><span data-stu-id="58639-121">Notice in the Solution Explorer on the right that a new file has been created for you called HelloWorldController.cs and that file is now opened in the **IDE**.</span></span>

<span data-ttu-id="58639-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="58639-122">[![HelloWorldControllerCode](getting-started-with-mvc-part2/_static/image6.png)](getting-started-with-mvc-part2/_static/image5.png)</span></span>

<span data-ttu-id="58639-123">建立兩個新的方法，在新的公用類別 HelloWorldController 中看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="58639-123">Create two new methods that look like this inside of your new public class HelloWorldController.</span></span> <span data-ttu-id="58639-124">我們會直接從我們的控制器傳回 HTML 字串，做為範例。</span><span class="sxs-lookup"><span data-stu-id="58639-124">We'll return a string of HTML directly from our controller as an example.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample1.cs)]

<span data-ttu-id="58639-125">您的控制器命名為 HelloWorldController，而您的新方法稱為 Index。</span><span class="sxs-lookup"><span data-stu-id="58639-125">Your Controller is named HelloWorldController and your new Method is called Index.</span></span> <span data-ttu-id="58639-126">再次執行您的應用程式，就像之前一樣（按一下 [播放] 按鈕，或按 F5 鍵來執行此動作）。</span><span class="sxs-lookup"><span data-stu-id="58639-126">Run your application again, just as before (click the play button or press F5 to do this).</span></span> <span data-ttu-id="58639-127">當您的瀏覽器啟動之後，請將網址列中的路徑變更為 `http://localhost:xx/HelloWorld`，其中 xx 是您的電腦所選擇的任何數位。</span><span class="sxs-lookup"><span data-stu-id="58639-127">Once your browser has started up, change the path in the address bar to `http://localhost:xx/HelloWorld` where xx is whatever number your computer has chosen.</span></span> <span data-ttu-id="58639-128">現在，您的瀏覽器看起來應該像下面的螢幕擷取畫面。</span><span class="sxs-lookup"><span data-stu-id="58639-128">Now your browser should look like the screenshot below.</span></span> <span data-ttu-id="58639-129">在上述方法中，我們傳回傳遞至稱為「內容」之方法的字串。</span><span class="sxs-lookup"><span data-stu-id="58639-129">In our method above we returned a string passed into a method called "Content."</span></span> <span data-ttu-id="58639-130">我們告訴系統只傳回一些 HTML，而且的確會傳回！</span><span class="sxs-lookup"><span data-stu-id="58639-130">We told the system just returns some HTML, and it did!</span></span>

<span data-ttu-id="58639-131">ASP.NET MVC 會根據傳入的 URL，叫用不同的控制器類別（以及其中的不同動作方法）。</span><span class="sxs-lookup"><span data-stu-id="58639-131">ASP.NET MVC invokes different Controller classes (and different Action methods within them) depending on the incoming URL.</span></span> <span data-ttu-id="58639-132">ASP.NET MVC 使用的預設對應邏輯會使用如下的格式來控制要執行的程式碼：</span><span class="sxs-lookup"><span data-stu-id="58639-132">The default mapping logic used by ASP.NET MVC uses a format like this to control what code is run:</span></span>

<span data-ttu-id="58639-133">/[控制器]/[ActionName]/[Parameters]</span><span class="sxs-lookup"><span data-stu-id="58639-133">/[Controller]/[ActionName]/[Parameters]</span></span>

<span data-ttu-id="58639-134">URL 的第一個部分會決定要執行的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="58639-134">The first part of the URL determines the Controller class to execute.</span></span> <span data-ttu-id="58639-135">因此，/HelloWorld 會對應至 HelloWorldController 類別。</span><span class="sxs-lookup"><span data-stu-id="58639-135">So /HelloWorld maps to the HelloWorldController class.</span></span> <span data-ttu-id="58639-136">URL 的第二個部分會決定要執行的類別上的動作方法。</span><span class="sxs-lookup"><span data-stu-id="58639-136">The second part of the URL determines the Action method on the class to execute.</span></span> <span data-ttu-id="58639-137">因此，/HelloWorld/Index 會導致 HelloWorldController 類別的 Index （）方法執行。</span><span class="sxs-lookup"><span data-stu-id="58639-137">So /HelloWorld/Index would cause the Index() method of the HelloWorldController class to execute.</span></span> <span data-ttu-id="58639-138">請注意，我們只需要造訪上面的/HelloWorld，並隱含方法索引。</span><span class="sxs-lookup"><span data-stu-id="58639-138">Notice that we only had to visit /HelloWorld above and the method Index was implied.</span></span> <span data-ttu-id="58639-139">這是因為名為 "Index" 的方法是在控制器上呼叫的預設方法（如果未明確指定的話）。</span><span class="sxs-lookup"><span data-stu-id="58639-139">This is because a method named "Index" is the default method that will be called on a controller if one is not explicitly specified.</span></span>

<span data-ttu-id="58639-140">[![這是我的預設動作](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="58639-140">[![This is my default action](getting-started-with-mvc-part2/_static/image8.png)](getting-started-with-mvc-part2/_static/image7.png)</span></span>

<span data-ttu-id="58639-141">現在，讓我們流覽 `http://localhost:xx/HelloWorld/Welcome.` 我們的歡迎方法現在已執行，並傳回其 HTML 字串。</span><span class="sxs-lookup"><span data-stu-id="58639-141">Now, let's visit `http://localhost:xx/HelloWorld/Welcome.` Now our Welcome Method has executed and returned its HTML string.</span></span>

<span data-ttu-id="58639-142">同樣地，/[控制器]/[ActionName]/[Parameters]，讓控制器 HelloWorld，而歡迎是在此情況下的方法。</span><span class="sxs-lookup"><span data-stu-id="58639-142">Again, /[Controller]/[ActionName]/[Parameters] so Controller is HelloWorld and Welcome is the Method in this case.</span></span> <span data-ttu-id="58639-143">尚未完成參數。</span><span class="sxs-lookup"><span data-stu-id="58639-143">We haven't done Parameters yet.</span></span>

<span data-ttu-id="58639-144">[![這是歡迎動作方法](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="58639-144">[![This is the Welcome action method](getting-started-with-mvc-part2/_static/image10.png)](getting-started-with-mvc-part2/_static/image9.png)</span></span>

<span data-ttu-id="58639-145">讓我們稍微修改我們的範例，讓我們可以從 URL 將中的某些資訊傳遞至控制器，例如：/HelloWorld/Welcome？ name = Scott&amp;numtimes is = 4。</span><span class="sxs-lookup"><span data-stu-id="58639-145">Let's modify our sample slightly so that we can pass some information in from the URL to our controller, for example like this: /HelloWorld/Welcome?name=Scott&amp;numtimes=4.</span></span> <span data-ttu-id="58639-146">變更您的 [歡迎使用] 方法以包含兩個參數，並如下所示更新它。</span><span class="sxs-lookup"><span data-stu-id="58639-146">Change your Welcome method to include two parameters and update it like below.</span></span> <span data-ttu-id="58639-147">請注意，我們使用了C#選擇性參數功能，表示如果未傳入參數 numtimes is，它應該預設為1。</span><span class="sxs-lookup"><span data-stu-id="58639-147">Note that we've used the C# optional parameter feature to indicate that the parameter numTimes should default to 1 if it's not passed in.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part2/samples/sample2.cs)]

<span data-ttu-id="58639-148">執行您的應用程式，並視需要流覽 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` 變更 name 和 numtimes is 的值。</span><span class="sxs-lookup"><span data-stu-id="58639-148">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` changing the value of name and numtimes as you like.</span></span> <span data-ttu-id="58639-149">系統會自動將您的查詢字串中的已具名引數對應至方法中的參數。</span><span class="sxs-lookup"><span data-stu-id="58639-149">The system automatically mapped the named parameters from your query string in the address bar to parameters in your method.</span></span>

<span data-ttu-id="58639-150">在這兩個範例中，控制器都已執行所有工作，並已直接傳回 HTML。</span><span class="sxs-lookup"><span data-stu-id="58639-150">In both these examples the controller has been doing all the work, and has been returning HTML directly.</span></span> <span data-ttu-id="58639-151">一般來說，我們不希望控制器直接傳回 HTML，因為這會使程式碼變得非常繁瑣。</span><span class="sxs-lookup"><span data-stu-id="58639-151">Ordinarily we don't want our Controllers returning HTML directly - since that ends up being very cumbersome to code.</span></span> <span data-ttu-id="58639-152">相反地，我們通常會使用個別的視圖範本檔案來協助產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="58639-152">Instead we'll typically use a separate View template file to help generate the HTML response.</span></span> <span data-ttu-id="58639-153">我們來看一下如何做到這一點。</span><span class="sxs-lookup"><span data-stu-id="58639-153">Let's look at how we can do this.</span></span> <span data-ttu-id="58639-154">關閉瀏覽器並返回 IDE。</span><span class="sxs-lookup"><span data-stu-id="58639-154">Close your browser and return to the IDE.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="58639-155">[上一頁](getting-started-with-mvc-part1.md)
> [下一頁](getting-started-with-mvc-part3.md)</span><span class="sxs-lookup"><span data-stu-id="58639-155">[Previous](getting-started-with-mvc-part1.md)
[Next](getting-started-with-mvc-part3.md)</span></span>
