---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
title: 加入視圖 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: e8f1515c-c277-47ff-a23e-224118f13f02
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part3
msc.type: authoredcontent
ms.openlocfilehash: 462b1210c45da67058899193afcea973f3daf122
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581554"
---
# <a name="adding-a-view"></a><span data-ttu-id="c6084-104">新增檢視</span><span class="sxs-lookup"><span data-stu-id="c6084-104">Adding a View</span></span>

<span data-ttu-id="c6084-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="c6084-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="c6084-106">這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="c6084-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="c6084-107">您將建立可從資料庫讀取和寫入的簡單 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="c6084-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="c6084-108">請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="c6084-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="c6084-109">在本節中，我們將探討如何讓我們的 HelloWorldController 類別使用視圖範本檔案，將產生的 HTML 回應完全封裝回用戶端。</span><span class="sxs-lookup"><span data-stu-id="c6084-109">In this section we are going to look at how we can have our HelloWorldController class use a View template file to cleanly encapsulate generating HTML responses back to a client.</span></span>

<span data-ttu-id="c6084-110">讓我們從使用具有索引方法的視圖範本開始。</span><span class="sxs-lookup"><span data-stu-id="c6084-110">Let's start by using a View template with our Index method.</span></span> <span data-ttu-id="c6084-111">我們的方法稱為 Index，它位於 HelloWorldController 中。</span><span class="sxs-lookup"><span data-stu-id="c6084-111">Our method is called Index and it's in the HelloWorldController.</span></span> <span data-ttu-id="c6084-112">目前，我們的 Index （）方法會傳回字串，內含在控制器類別中硬式編碼的訊息。</span><span class="sxs-lookup"><span data-stu-id="c6084-112">Currently our Index() method returns a string with a message that is hardcoded within the Controller class.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample1.cs)]

<span data-ttu-id="c6084-113">現在讓我們將 Index 方法變更為，如下所示：</span><span class="sxs-lookup"><span data-stu-id="c6084-113">Let's now change the Index method to instead look like this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample2.cs)]

<span data-ttu-id="c6084-114">現在讓我們將一個 View 範本新增至我們的專案，我們可以用來做為 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="c6084-114">Let's now add a View template to our project that we can use for our Index() method.</span></span> <span data-ttu-id="c6084-115">若要這麼做，請以滑鼠右鍵按一下索引方法中間的某個位置，然後按一下 [加入視圖]。</span><span class="sxs-lookup"><span data-stu-id="c6084-115">To do this, right-click with your mouse somewhere in the middle of the Index method and click Add View...</span></span>

![影像](getting-started-with-mvc-part3/_static/image1.png)

<span data-ttu-id="c6084-117">這會顯示 [新增視圖] 對話方塊，提供我們一些選項，讓我們瞭解如何建立可供索引方法使用的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="c6084-117">This will bring up the "Add View" dialog which provides us some options for how we want to create a view template that can be used by our Index method.</span></span> <span data-ttu-id="c6084-118">目前，請不要變更任何專案，只要按一下 [新增] 按鈕即可。</span><span class="sxs-lookup"><span data-stu-id="c6084-118">For now, don't change anything, and just click the Add button.</span></span>

<span data-ttu-id="c6084-119">[![加入視圖 對話方塊](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="c6084-119">[![Add View Dialog](getting-started-with-mvc-part3/_static/image3.png)](getting-started-with-mvc-part3/_static/image2.png)</span></span>

<span data-ttu-id="c6084-120">按一下 [新增] 之後，新的資料夾和新的檔案就會出現在 [方案] 資料夾中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="c6084-120">After you click Add, a new folder and a new file will appear in the Solution Folder, as seen here.</span></span> <span data-ttu-id="c6084-121">我現在在 Views 底下有一個 [HelloWorld] 資料夾，以及該資料夾內的一個 [Index .aspx] 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6084-121">I now have a HelloWorld folder under Views, and an Index.aspx file inside that folder.</span></span>

<span data-ttu-id="c6084-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="c6084-122">[![solutionexplorerwithindex](getting-started-with-mvc-part3/_static/image5.png)](getting-started-with-mvc-part3/_static/image4.png)</span></span>

<span data-ttu-id="c6084-123">新的索引檔案也已經開啟並可供編輯。</span><span class="sxs-lookup"><span data-stu-id="c6084-123">The new Index file is also already opened and ready for editing.</span></span> <span data-ttu-id="c6084-124">在第一個 &lt;h2 下新增一些文字，&gt;索引&lt;/h2&gt;，例如 "Hello World"。</span><span class="sxs-lookup"><span data-stu-id="c6084-124">Add some text under the first &lt;h2&gt;Index&lt;/h2&gt; like "Hello World."</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample3.html)]

<span data-ttu-id="c6084-125">執行您的應用程式，並在瀏覽器中再次造訪[`http://localhost:xx/HelloWorld`](http://localhostxx) 。</span><span class="sxs-lookup"><span data-stu-id="c6084-125">Run your application and visit [`http://localhost:xx/HelloWorld`](http://localhostxx) again in your browser.</span></span> <span data-ttu-id="c6084-126">在此範例中，控制器的索引方法不會執行任何工作，但會呼叫「傳回 View （）」，表示我們想要使用視圖範本檔案將回應轉譯回用戶端。</span><span class="sxs-lookup"><span data-stu-id="c6084-126">The Index method in our controller in this example didn't do any work, but did call "return View()" which indicated that we wanted to use a view template file to render a response back to the client.</span></span> <span data-ttu-id="c6084-127">因為我們並未明確指定要使用的視圖範本檔案的名稱，所以 ASP.NET MVC 會預設為使用 \Views\HelloWorld 資料夾中的 default.aspx view 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6084-127">Because we did not explicitly specify the name of the view template file to use, ASP.NET MVC defaulted to using the Index.aspx view file within the \Views\HelloWorld folder.</span></span> <span data-ttu-id="c6084-128">現在我們會在我們的視圖中看到硬式編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="c6084-128">Now we see the string we hard-coded in our View.</span></span>

<span data-ttu-id="c6084-129">[![索引-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="c6084-129">[![Index - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image7.png)](getting-started-with-mvc-part3/_static/image6.png)</span></span>

<span data-ttu-id="c6084-130">看起來不錯。</span><span class="sxs-lookup"><span data-stu-id="c6084-130">Looks pretty good.</span></span> <span data-ttu-id="c6084-131">不過，請注意，瀏覽器的標題會顯示「索引」，而頁面上的大標題會顯示「我的 MVC 應用程式」。</span><span class="sxs-lookup"><span data-stu-id="c6084-131">However, notice that the Browser's title says "Index" and the big title on the page says "My MVC Application."</span></span> <span data-ttu-id="c6084-132">讓我們變更這些。</span><span class="sxs-lookup"><span data-stu-id="c6084-132">Let's change those.</span></span>

### <a name="changing-views-and-master-pages"></a><span data-ttu-id="c6084-133">變更視圖和主版頁面</span><span class="sxs-lookup"><span data-stu-id="c6084-133">Changing Views and Master Pages</span></span>

<span data-ttu-id="c6084-134">首先，讓我們變更「我的 MVC 應用程式」文字。</span><span class="sxs-lookup"><span data-stu-id="c6084-134">First, let's change the text "My MVC Application."</span></span> <span data-ttu-id="c6084-135">該文字會共用並顯示在每個頁面上。</span><span class="sxs-lookup"><span data-stu-id="c6084-135">That text is shared and appears on every page.</span></span> <span data-ttu-id="c6084-136">它實際上只會出現在我們的程式碼中的一個位置，即使它是在應用程式的每個頁面上也一樣。</span><span class="sxs-lookup"><span data-stu-id="c6084-136">It actually appears in only one place in our code, even though it's on every page in our app.</span></span> <span data-ttu-id="c6084-137">移至方案總管中的 [/Views/Shared] 資料夾，然後開啟 [網站] 檔案。</span><span class="sxs-lookup"><span data-stu-id="c6084-137">Go to the /Views/Shared folder in the Solution Explorer and open the Site.Master file.</span></span> <span data-ttu-id="c6084-138">此檔案稱為「主版頁面」，它是所有其他頁面都使用的共用「shell」。</span><span class="sxs-lookup"><span data-stu-id="c6084-138">This file is called a Master Page and it's the shared "shell" that all our other pages use.</span></span>

<span data-ttu-id="c6084-139">請注意，在此檔案中顯示 ContentPlaceholder "MainContent" 的一些文字。</span><span class="sxs-lookup"><span data-stu-id="c6084-139">Notice some text that says ContentPlaceholder "MainContent" in this file.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample4.aspx)]

<span data-ttu-id="c6084-140">該預留位置就是您所建立的所有頁面都會顯示在主版頁面中「包裝」的位置。</span><span class="sxs-lookup"><span data-stu-id="c6084-140">That placeholder is where all the pages you create will show up, "wrapped" in the master page.</span></span> <span data-ttu-id="c6084-141">請嘗試變更標題，然後執行您的應用程式並流覽多個頁面。</span><span class="sxs-lookup"><span data-stu-id="c6084-141">Try changing the title, then run your app and visit multiple pages.</span></span> <span data-ttu-id="c6084-142">您會發現，您的一項變更會出現在多個頁面上。</span><span class="sxs-lookup"><span data-stu-id="c6084-142">You'll notice that your one change appears on multiple pages.</span></span>

[!code-html[Main](getting-started-with-mvc-part3/samples/sample5.html)]

<span data-ttu-id="c6084-143">現在每個頁面都會有主要標題，也就是「我的 MVC 電影應用程式」的 H1。</span><span class="sxs-lookup"><span data-stu-id="c6084-143">Now every page will have the Primary Heading - that's H1 - of "My MVC Movie Application."</span></span> <span data-ttu-id="c6084-144">這會處理頂端的白色文字，並在所有頁面上共用。</span><span class="sxs-lookup"><span data-stu-id="c6084-144">That handles the white text at the top there that's shared across all the pages.</span></span>

<span data-ttu-id="c6084-145">以下是完整的網站，其中包含已變更的標題：</span><span class="sxs-lookup"><span data-stu-id="c6084-145">Here is the Site.Master in its entirety with our changed title:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample6.aspx)]

<span data-ttu-id="c6084-146">現在，讓我們變更 [索引] 頁面的標題。</span><span class="sxs-lookup"><span data-stu-id="c6084-146">Now, let's change the title of the Index page.</span></span>

<span data-ttu-id="c6084-147">開啟/HelloWorld/Index.aspx。</span><span class="sxs-lookup"><span data-stu-id="c6084-147">Open /HelloWorld/Index.aspx.</span></span> <span data-ttu-id="c6084-148">有兩個地方可以變更。</span><span class="sxs-lookup"><span data-stu-id="c6084-148">There's two places to change.</span></span> <span data-ttu-id="c6084-149">首先，出現在瀏覽器標題中的標題，然後是次要標題（也就是 H2）。</span><span class="sxs-lookup"><span data-stu-id="c6084-149">First, the Title that appears in the title of the browser, then the secondary header - that's H2 - as well.</span></span> <span data-ttu-id="c6084-150">我要讓它們彼此略有不同，讓您可以看到哪一段程式碼變更了哪個部分的應用程式。</span><span class="sxs-lookup"><span data-stu-id="c6084-150">I'll make them each slightly different so you can see which bit of code changes which part of the app.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample7.aspx)]

<span data-ttu-id="c6084-151">執行您的應用程式並造訪/Movies。</span><span class="sxs-lookup"><span data-stu-id="c6084-151">Run your app and visit /Movies.</span></span> <span data-ttu-id="c6084-152">請注意，瀏覽器標題、主要標題和次要標題已變更。</span><span class="sxs-lookup"><span data-stu-id="c6084-152">Notice that the browser title, the primary heading and the secondary headings have changed.</span></span> <span data-ttu-id="c6084-153">您可以輕鬆地在您的應用程式中進行大幅變更，而對您的視圖進行小幅變更。</span><span class="sxs-lookup"><span data-stu-id="c6084-153">It's easy to make big changes in your app with small changes to your view.</span></span>

<span data-ttu-id="c6084-154">[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="c6084-154">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image9.png)](getting-started-with-mvc-part3/_static/image8.png)</span></span>

<span data-ttu-id="c6084-155">有點「資料」（在此案例中為「Hello World！」</span><span class="sxs-lookup"><span data-stu-id="c6084-155">Our little bit of "data" (in this case the "Hello World!"</span></span> <span data-ttu-id="c6084-156">訊息）已硬式編碼。</span><span class="sxs-lookup"><span data-stu-id="c6084-156">message) was hard coded though.</span></span> <span data-ttu-id="c6084-157">我們有 V （Views），而我們已經有 C （控制器），但沒有 M （模型）。</span><span class="sxs-lookup"><span data-stu-id="c6084-157">We've got V (Views) and we've got C (Controllers), but no M (Model) yet.</span></span> <span data-ttu-id="c6084-158">我們很快就會逐步解說如何建立資料庫，並從中抓取模型資料。</span><span class="sxs-lookup"><span data-stu-id="c6084-158">We'll shortly walk through how create a database and retrieve model data from it.</span></span>

## <a name="passing-a-viewmodel"></a><span data-ttu-id="c6084-159">傳遞 ViewModel</span><span class="sxs-lookup"><span data-stu-id="c6084-159">Passing a ViewModel</span></span>

<span data-ttu-id="c6084-160">不過，在我們進入資料庫並討論模型之前，先來談談「Viewmodel」。</span><span class="sxs-lookup"><span data-stu-id="c6084-160">Before we go to a database and talk about Models, though, let's first talk about "ViewModels."</span></span> <span data-ttu-id="c6084-161">這些物件代表將 HTML 回應轉譯回用戶端所需的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="c6084-161">These are objects that represent what a View template requires to render an HTML response back to a client.</span></span> <span data-ttu-id="c6084-162">它們通常是由控制器類別建立並傳遞至視圖範本，而且應該只包含此視圖範本所需的資料，而且不再需要。</span><span class="sxs-lookup"><span data-stu-id="c6084-162">They are typically created and passed by a Controller class to a View template, and should only contain the data that the View template requires - and no more.</span></span>

<span data-ttu-id="c6084-163">先前使用我們的 HelloWorld 範例，我們的歡迎（）動作方法會採用名稱和 Numtimes is 參數，並將它輸出到瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="c6084-163">Previously with our HelloWorld sample, our Welcome() action method took a name and a numTimes parameter and output it to the browser.</span></span> <span data-ttu-id="c6084-164">而不是讓控制器直接轉譯此回應，讓我們改為建立小型類別來保存該資料，然後將它傳遞至 View 範本，以使用它來呈現 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="c6084-164">Rather than have the Controller continue to render this response directly,let's instead make a small class to hold that data and then pass it over to a View template to render back the HTML response using it.</span></span> <span data-ttu-id="c6084-165">如此一來，控制器就會關心一件事，另一個是「視圖」範本，讓我們能夠在應用程式中維持乾淨的「關注點分離」。</span><span class="sxs-lookup"><span data-stu-id="c6084-165">This way the Controller is concerned with one thing and the View template another – enabling us to maintain clean "separation of concerns" within our application.</span></span>

<span data-ttu-id="c6084-166">返回 HelloWorldController.cs 檔案並加入新的 "WelcomeViewModel" 類別，並在控制器內變更歡迎使用的方法。</span><span class="sxs-lookup"><span data-stu-id="c6084-166">Return to the HelloWorldController.cs file and add a new "WelcomeViewModel" class and change the Welcome method inside your controller.</span></span> <span data-ttu-id="c6084-167">以下是在相同檔案中具有新類別的完整 HelloWorldController.cs。</span><span class="sxs-lookup"><span data-stu-id="c6084-167">Here is the complete HelloWorldController.cs with the new class in the same file.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part3/samples/sample8.cs)]

<span data-ttu-id="c6084-168">雖然它是在多行上，但我們的歡迎方法其實只是兩個程式碼語句。</span><span class="sxs-lookup"><span data-stu-id="c6084-168">Even though it's on multiple lines, our Welcome method is really only two code statements.</span></span> <span data-ttu-id="c6084-169">第一個語句會將我們的兩個參數封裝成 ViewModel 物件，而第二個會將產生的物件傳遞到 View。</span><span class="sxs-lookup"><span data-stu-id="c6084-169">The first statement packages up our two parameters into a ViewModel object, and the second passes the resulting object onto the View.</span></span>

<span data-ttu-id="c6084-170">現在我們需要一個歡迎視圖範本！</span><span class="sxs-lookup"><span data-stu-id="c6084-170">Now we need a Welcome View template!</span></span> <span data-ttu-id="c6084-171">以滑鼠右鍵按一下歡迎方法，然後選取 [加入視圖]。</span><span class="sxs-lookup"><span data-stu-id="c6084-171">Right click in the Welcome method and select Add View.</span></span> <span data-ttu-id="c6084-172">此時，我們會核取 [建立強型別視圖]，然後從下拉式清單中選取我們的 WelcomeViewModel 類別。</span><span class="sxs-lookup"><span data-stu-id="c6084-172">This time, we'll check "Create a strongly-typed view" and select our WelcomeViewModel class from the drop down list.</span></span> <span data-ttu-id="c6084-173">這個新的視圖只會知道 WelcomeViewModels 和其他類型的物件。</span><span class="sxs-lookup"><span data-stu-id="c6084-173">This new view will only know about WelcomeViewModels and no other types of objects.</span></span>

> <span data-ttu-id="c6084-174">*注意：在新增的 WelcomeViewModel 之後，您必須編譯一次，才會顯示在下拉式清單中。*</span><span class="sxs-lookup"><span data-stu-id="c6084-174">*NOTE: You'll need to have compiled once after adding your WelcomeViewModel for to show up in the drop down list.*</span></span>

<span data-ttu-id="c6084-175">您的 [加入視圖] 對話方塊看起來應該會像這樣。</span><span class="sxs-lookup"><span data-stu-id="c6084-175">Here's what your Add View dialog should look like.</span></span> <span data-ttu-id="c6084-176">按一下 [加入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="c6084-176">Click the Add button.</span></span> ![新增視圖已圈號](getting-started-with-mvc-part3/_static/image10.png)

<span data-ttu-id="c6084-178">將此程式碼新增至新的 [歡迎使用 .aspx] 中的 [&lt;h2]&gt; 之下。</span><span class="sxs-lookup"><span data-stu-id="c6084-178">Add this code under the &lt;h2&gt; in your new Welcome.aspx.</span></span> <span data-ttu-id="c6084-179">我們會建立迴圈，並在使用者說出「我應該」的時候說「Hello」！</span><span class="sxs-lookup"><span data-stu-id="c6084-179">We'll make a loop and say Hello as many times as the user says we should!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part3/samples/sample9.aspx)]

<span data-ttu-id="c6084-180">另外也請注意，因為我們告訴此 WelcomeViewModel （他們已結婚，請記住？），我們會在每次參考模型物件時取得有用的 Intellisense，如下列螢幕擷取畫面所示：</span><span class="sxs-lookup"><span data-stu-id="c6084-180">Also, notice while you're typing that because we told this View about the WelcomeViewModel (they are married, remember?) that we get helpful Intellisense each time we reference our Model object as seen in the screenshot below:</span></span>

<span data-ttu-id="c6084-181">[![NumTime 原始程式碼](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="c6084-181">[![NumTime Source Code](getting-started-with-mvc-part3/_static/image12.png)](getting-started-with-mvc-part3/_static/image11.png)</span></span>

<span data-ttu-id="c6084-182">執行您的應用程式，並再次流覽 `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4`。</span><span class="sxs-lookup"><span data-stu-id="c6084-182">Run your application and visit `http://localhost:xx/HelloWorld/Welcome?name=Scott&numtimes=4` again.</span></span> <span data-ttu-id="c6084-183">現在我們會從 URL 取得資料，並自動將其傳入控制器，我們的控制器會將資料封裝成 ViewModel，並將該物件傳遞至我們的 View。</span><span class="sxs-lookup"><span data-stu-id="c6084-183">Now we're taking data from the URL, it's passed into our Controller automatically, our Controller packages up the data into a ViewModel and passes that object onto our View.</span></span> <span data-ttu-id="c6084-184">視圖會將資料以 HTML 形式顯示給使用者。</span><span class="sxs-lookup"><span data-stu-id="c6084-184">The View than displays the data as HTML to the user.</span></span>

<span data-ttu-id="c6084-185">[![歡迎使用-Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="c6084-185">[![Welcome - Windows Internet Explorer](getting-started-with-mvc-part3/_static/image14.png)](getting-started-with-mvc-part3/_static/image13.png)</span></span>

<span data-ttu-id="c6084-186">這就是模型的「M」類型，但不是資料庫種類。</span><span class="sxs-lookup"><span data-stu-id="c6084-186">Well, that was a kind of an "M" for Model, but not the database kind.</span></span> <span data-ttu-id="c6084-187">讓我們來看看我們所學到的內容，並建立電影資料庫。</span><span class="sxs-lookup"><span data-stu-id="c6084-187">Let's take what we've learned and create a database of Movies.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c6084-188">[上一頁](getting-started-with-mvc-part2.md)
> [下一頁](getting-started-with-mvc-part4.md)</span><span class="sxs-lookup"><span data-stu-id="c6084-188">[Previous](getting-started-with-mvc-part2.md)
[Next](getting-started-with-mvc-part4.md)</span></span>
