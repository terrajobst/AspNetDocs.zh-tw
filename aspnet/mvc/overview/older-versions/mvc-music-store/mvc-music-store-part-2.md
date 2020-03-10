---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
title: 第2部分：控制器 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第2部分涵蓋控制器。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 998ce4e1-9d72-435b-8f1c-399a10ae4360
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-2
msc.type: authoredcontent
ms.openlocfilehash: 9dc2226f4951d4bed122df37d35bbb94730a00ad
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559875"
---
# <a name="part-2-controllers"></a><span data-ttu-id="f28c3-104">第2部分：控制器</span><span class="sxs-lookup"><span data-stu-id="f28c3-104">Part 2: Controllers</span></span>

<span data-ttu-id="f28c3-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="f28c3-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="f28c3-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="f28c3-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="f28c3-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="f28c3-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="f28c3-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="f28c3-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="f28c3-109">第2部分涵蓋控制器。</span><span class="sxs-lookup"><span data-stu-id="f28c3-109">Part 2 covers Controllers.</span></span>

<span data-ttu-id="f28c3-110">使用傳統的 web 架構時，連入的 Url 通常會對應到磁片上的檔案。</span><span class="sxs-lookup"><span data-stu-id="f28c3-110">With traditional web frameworks, incoming URLs are typically mapped to files on disk.</span></span> <span data-ttu-id="f28c3-111">例如： "/Products.aspx" 或 "/Products.php" 等 URL 的要求可能會由 "Products" 或 "Products. php" 檔案處理。</span><span class="sxs-lookup"><span data-stu-id="f28c3-111">For example: a request for a URL like "/Products.aspx" or "/Products.php" might be processed by a "Products.aspx" or "Products.php" file.</span></span>

<span data-ttu-id="f28c3-112">以 Web 為基礎的 MVC 架構會以稍有不同的方式將 Url 對應至伺服器程式碼。</span><span class="sxs-lookup"><span data-stu-id="f28c3-112">Web-based MVC frameworks map URLs to server code in a slightly different way.</span></span> <span data-ttu-id="f28c3-113">與其將傳入 Url 對應至檔案，它們會改為將 Url 對應至類別上的方法。</span><span class="sxs-lookup"><span data-stu-id="f28c3-113">Instead of mapping incoming URLs to files, they instead map URLs to methods on classes.</span></span> <span data-ttu-id="f28c3-114">這些類別稱為「控制器」，負責處理傳入 HTTP 要求、處理使用者輸入、抓取和儲存資料，以及判斷要傳回給用戶端的回應（顯示 HTML、下載檔案、重新導向至不同的URL 等）。</span><span class="sxs-lookup"><span data-stu-id="f28c3-114">These classes are called "Controllers" and they are responsible for processing incoming HTTP requests, handling user input, retrieving and saving data, and determining the response to send back to the client (display HTML, download a file, redirect to a different URL, etc.).</span></span>

## <a name="adding-a-homecontroller"></a><span data-ttu-id="f28c3-115">新增 HomeController</span><span class="sxs-lookup"><span data-stu-id="f28c3-115">Adding a HomeController</span></span>

<span data-ttu-id="f28c3-116">我們將會藉由新增控制器類別來處理我們網站首頁的 Url，以開始使用 MVC 音樂存放區應用程式。</span><span class="sxs-lookup"><span data-stu-id="f28c3-116">We'll begin our MVC Music Store application by adding a Controller class that will handle URLs to the Home page of our site.</span></span> <span data-ttu-id="f28c3-117">我們將遵循 ASP.NET MVC 的預設命名慣例，並將其稱為 HomeController。</span><span class="sxs-lookup"><span data-stu-id="f28c3-117">We'll follow the default naming conventions of ASP.NET MVC and call it HomeController.</span></span>

<span data-ttu-id="f28c3-118">以滑鼠右鍵按一下方案總管中的 [控制器] 資料夾，然後依序選取 [新增] 和 [控制器 ...]命令</span><span class="sxs-lookup"><span data-stu-id="f28c3-118">Right-click the "Controllers" folder within the Solution Explorer and select "Add", and then the "Controller…" command:</span></span>

![](mvc-music-store-part-2/_static/image1.jpg)

<span data-ttu-id="f28c3-119">這會顯示 [新增控制器] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="f28c3-119">This will bring up the "Add Controller" dialog.</span></span> <span data-ttu-id="f28c3-120">將控制器命名為 "HomeController"，然後按 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="f28c3-120">Name the controller "HomeController" and press the Add button.</span></span>

![](mvc-music-store-part-2/_static/image1.png)

<span data-ttu-id="f28c3-121">這會使用下列程式碼建立新的檔案 HomeController.cs：</span><span class="sxs-lookup"><span data-stu-id="f28c3-121">This will create a new file, HomeController.cs, with the following code:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample1.cs)]

<span data-ttu-id="f28c3-122">為了盡可能地開始，讓我們將 Index 方法取代為只傳回字串的簡單方法。</span><span class="sxs-lookup"><span data-stu-id="f28c3-122">To start as simply as possible, let's replace the Index method with a simple method that just returns a string.</span></span> <span data-ttu-id="f28c3-123">我們會進行兩個變更：</span><span class="sxs-lookup"><span data-stu-id="f28c3-123">We'll make two changes:</span></span>

- <span data-ttu-id="f28c3-124">變更方法以傳回字串，而不是 ActionResult</span><span class="sxs-lookup"><span data-stu-id="f28c3-124">Change the method to return a string instead of an ActionResult</span></span>
- <span data-ttu-id="f28c3-125">變更 return 語句以傳回 "Hello from Home"</span><span class="sxs-lookup"><span data-stu-id="f28c3-125">Change the return statement to return "Hello from Home"</span></span>

<span data-ttu-id="f28c3-126">方法現在看起來應該像這樣：</span><span class="sxs-lookup"><span data-stu-id="f28c3-126">The method should now look like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample2.cs)]

## <a name="running-the-application"></a><span data-ttu-id="f28c3-127">執行應用程式</span><span class="sxs-lookup"><span data-stu-id="f28c3-127">Running the Application</span></span>

<span data-ttu-id="f28c3-128">現在讓我們來執行網站。</span><span class="sxs-lookup"><span data-stu-id="f28c3-128">Now let's run the site.</span></span> <span data-ttu-id="f28c3-129">我們可以啟動我們的 web 伺服器，並使用下列任何一項來試用網站：</span><span class="sxs-lookup"><span data-stu-id="f28c3-129">We can start our web-server and try out the site using any of the following::</span></span>

- <span data-ttu-id="f28c3-130">選擇 [Debug ⇨] [開始調試] 功能表項目</span><span class="sxs-lookup"><span data-stu-id="f28c3-130">Choose the Debug ⇨ Start Debugging menu item</span></span>
- <span data-ttu-id="f28c3-131">按一下工具列中的綠色箭號按鈕 ![](mvc-music-store-part-2/_static/image2.jpg)</span><span class="sxs-lookup"><span data-stu-id="f28c3-131">Click the Green arrow button in the toolbar ![](mvc-music-store-part-2/_static/image2.jpg)</span></span>
- <span data-ttu-id="f28c3-132">使用鍵盤快速鍵 F5。</span><span class="sxs-lookup"><span data-stu-id="f28c3-132">Use the keyboard shortcut, F5.</span></span>

<span data-ttu-id="f28c3-133">使用上述任何步驟，將會編譯我們的專案，然後讓 Visual Web Developer 內建的 ASP.NET 程式開發伺服器開始。</span><span class="sxs-lookup"><span data-stu-id="f28c3-133">Using any of the above steps will compile our project, and then cause the ASP.NET Development Server that is built-into Visual Web Developer to start.</span></span> <span data-ttu-id="f28c3-134">畫面的右下角會顯示通知，指出 ASP.NET 程式開發伺服器已啟動，並會顯示其執行所在的埠號碼。</span><span class="sxs-lookup"><span data-stu-id="f28c3-134">A notification will appear in the bottom corner of the screen to indicate that the ASP.NET Development Server has started up, and will show the port number that it is running under.</span></span>

![](mvc-music-store-part-2/_static/image2.png)

<span data-ttu-id="f28c3-135">Visual Web Developer 接著會自動開啟瀏覽器視窗，其 URL 指向我們的 Web 服務器。</span><span class="sxs-lookup"><span data-stu-id="f28c3-135">Visual Web Developer will then automatically open a browser window whose URL points to our web-server.</span></span> <span data-ttu-id="f28c3-136">這可讓我們快速試用我們的 web 應用程式：</span><span class="sxs-lookup"><span data-stu-id="f28c3-136">This will allow us to quickly try out our web application:</span></span>

![](mvc-music-store-part-2/_static/image3.png)

<span data-ttu-id="f28c3-137">好啦，我們建立了新的網站，新增了三行功能，而且在瀏覽器中有文字。</span><span class="sxs-lookup"><span data-stu-id="f28c3-137">Okay, that was pretty quick – we created a new website, added a three line function, and we've got text in a browser.</span></span> <span data-ttu-id="f28c3-138">不是 rocket 科學，而是一開始。</span><span class="sxs-lookup"><span data-stu-id="f28c3-138">Not rocket science, but it's a start.</span></span>

<span data-ttu-id="f28c3-139">*注意： Visual Web Developer 包含 ASP.NET 程式開發伺服器，會以隨機免費的「埠」號碼執行您的網站。在上方的螢幕擷取畫面中，網站會在 `http://localhost:26641/`執行，因此它會使用埠26641。您的埠號碼會不同。當我們在本教學課程中討論 URL 的類似/Store/Browse 時，將會在埠號碼之後。假設埠號碼為26641，流覽至/Store/Browse 就表示流覽 `http://localhost:26641/Store/Browse`。*</span><span class="sxs-lookup"><span data-stu-id="f28c3-139">*Note: Visual Web Developer includes the ASP.NET Development Server, which will run your website on a random free "port" number. In the screenshot above, the site is running at `http://localhost:26641/`, so it's using port 26641. Your port number will be different. When we talk about URL's like /Store/Browse in this tutorial, that will go after the port number. Assuming a port number of 26641, browsing to /Store/Browse will mean browsing to `http://localhost:26641/Store/Browse`.*</span></span>

## <a name="adding-a-storecontroller"></a><span data-ttu-id="f28c3-140">新增 StoreController</span><span class="sxs-lookup"><span data-stu-id="f28c3-140">Adding a StoreController</span></span>

<span data-ttu-id="f28c3-141">我們新增了一個簡單的 HomeController，可實現網站的首頁。</span><span class="sxs-lookup"><span data-stu-id="f28c3-141">We added a simple HomeController that implements the Home Page of our site.</span></span> <span data-ttu-id="f28c3-142">現在讓我們新增另一個控制器，我們將用它來執行音樂存放區的流覽功能。</span><span class="sxs-lookup"><span data-stu-id="f28c3-142">Let's now add another controller that we'll use to implement the browsing functionality of our music store.</span></span> <span data-ttu-id="f28c3-143">我們的存放區控制器將支援三種案例：</span><span class="sxs-lookup"><span data-stu-id="f28c3-143">Our store controller will support three scenarios:</span></span>

- <span data-ttu-id="f28c3-144">音樂存放區中音樂內容的清單頁面</span><span class="sxs-lookup"><span data-stu-id="f28c3-144">A listing page of the music genres in our music store</span></span>
- <span data-ttu-id="f28c3-145">列出特定內容類型中所有音樂專輯的流覽頁面</span><span class="sxs-lookup"><span data-stu-id="f28c3-145">A browse page that lists all of the music albums in a particular genre</span></span>
- <span data-ttu-id="f28c3-146">顯示特定音樂專輯相關資訊的詳細資料頁面</span><span class="sxs-lookup"><span data-stu-id="f28c3-146">A details page that shows information about a specific music album</span></span>

<span data-ttu-id="f28c3-147">首先，我們要加入新的 StoreController 類別。</span><span class="sxs-lookup"><span data-stu-id="f28c3-147">We'll start by adding a new StoreController class..</span></span> <span data-ttu-id="f28c3-148">如果您還沒有這麼做，請關閉瀏覽器或選取 [Debug ⇨停止偵錯工具] 功能表項目，以停止執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="f28c3-148">If you haven't already, stop running the application either by closing the browser or selecting the Debug ⇨ Stop Debugging menu item.</span></span>

<span data-ttu-id="f28c3-149">現在加入新的 StoreController。</span><span class="sxs-lookup"><span data-stu-id="f28c3-149">Now add a new StoreController.</span></span> <span data-ttu-id="f28c3-150">就像我們在 HomeController 中所做的一樣，只要以滑鼠右鍵按一下方案總管中的 [控制器] 資料夾，然後選擇 [加入&gt;控制器] 功能表項目，就可以做到這一點。</span><span class="sxs-lookup"><span data-stu-id="f28c3-150">Just like we did with HomeController, we'll do this by right-clicking on the "Controllers" folder within the Solution Explorer and choosing the Add-&gt;Controller menu item</span></span>

![](mvc-music-store-part-2/_static/image4.png)

<span data-ttu-id="f28c3-151">我們的新 StoreController 已經有 "Index" 方法。</span><span class="sxs-lookup"><span data-stu-id="f28c3-151">Our new StoreController already has an "Index" method.</span></span> <span data-ttu-id="f28c3-152">我們將使用此「索引」方法來執行清單頁面，其中列出我們的音樂存放區中的所有內容類型。</span><span class="sxs-lookup"><span data-stu-id="f28c3-152">We'll use this "Index" method to implement our listing page that lists all genres in our music store.</span></span> <span data-ttu-id="f28c3-153">我們也會新增兩個其他方法，以執行我們想要讓 StoreController 處理的其他兩個案例：流覽和詳細資料。</span><span class="sxs-lookup"><span data-stu-id="f28c3-153">We'll also add two additional methods to implement the two other scenarios we want our StoreController to handle: Browse and Details.</span></span>

<span data-ttu-id="f28c3-154">在控制器內的這些方法（索引、流覽和詳細資料）稱為「控制器動作」，而且您已經看到 HomeController （）動作方法，其工作是回應 URL 要求，而（通常是說）決定哪些內容應該傳送回叫用 URL 的瀏覽器或使用者。</span><span class="sxs-lookup"><span data-stu-id="f28c3-154">These methods (Index, Browse and Details) within our Controller are called "Controller Actions", and as you've already seen with the HomeController.Index()action method, their job is to respond to URL requests and (generally speaking) determine what content should be sent back to the browser or user that invoked the URL.</span></span>

<span data-ttu-id="f28c3-155">我們將藉由變更 theIndex （）方法來啟動我們的 StoreController 執行，以傳回字串 "Hello from Store. Index （）"，我們將為 Browse （）和 Details （）新增類似的方法：</span><span class="sxs-lookup"><span data-stu-id="f28c3-155">We'll start our StoreController implementation by changing theIndex() method to return the string "Hello from Store.Index()" and we'll add similar methods for Browse() and Details():</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample3.cs)]

<span data-ttu-id="f28c3-156">再次執行專案，並流覽下列 Url：</span><span class="sxs-lookup"><span data-stu-id="f28c3-156">Run the project again and browse the following URLs:</span></span>

- <span data-ttu-id="f28c3-157">/Store</span><span class="sxs-lookup"><span data-stu-id="f28c3-157">/Store</span></span>
- <span data-ttu-id="f28c3-158">/Store/Browse</span><span class="sxs-lookup"><span data-stu-id="f28c3-158">/Store/Browse</span></span>
- <span data-ttu-id="f28c3-159">/Store/Details</span><span class="sxs-lookup"><span data-stu-id="f28c3-159">/Store/Details</span></span>

<span data-ttu-id="f28c3-160">存取這些 Url 將會叫用控制器中的動作方法，並傳回字串回應：</span><span class="sxs-lookup"><span data-stu-id="f28c3-160">Accessing these URLs will invoke the action methods within our Controller and return string responses:</span></span>

![](mvc-music-store-part-2/_static/image5.png)

<span data-ttu-id="f28c3-161">這很棒，但這些只是常數位串。</span><span class="sxs-lookup"><span data-stu-id="f28c3-161">That's great, but these are just constant strings.</span></span> <span data-ttu-id="f28c3-162">讓我們將其設為動態，讓他們從 URL 中取出資訊，並將它顯示在頁面輸出中。</span><span class="sxs-lookup"><span data-stu-id="f28c3-162">Let's make them dynamic, so they take information from the URL and display it in the page output.</span></span>

<span data-ttu-id="f28c3-163">首先，我們將變更 [流覽動作] 方法，以從 URL 抓取 querystring 值。</span><span class="sxs-lookup"><span data-stu-id="f28c3-163">First we'll change the Browse action method to retrieve a querystring value from the URL.</span></span> <span data-ttu-id="f28c3-164">我們可以藉由將「內容類型」參數新增至動作方法來達到此目的。</span><span class="sxs-lookup"><span data-stu-id="f28c3-164">We can do this by adding a "genre" parameter to our action method.</span></span> <span data-ttu-id="f28c3-165">當我們執行此 ASP.NET 時，MVC 會在叫用時，自動將名為 "內容類型的任何 querystring 或表單 post 參數傳遞至動作方法。</span><span class="sxs-lookup"><span data-stu-id="f28c3-165">When we do this ASP.NET MVC will automatically pass any querystring or form post parameters named "genre" to our action method when it is invoked.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample4.cs)]

<span data-ttu-id="f28c3-166">*注意：我們會使用 Httputility.htmlencode. HtmlEncode 公用程式方法來淨化使用者輸入。這可防止使用者使用/Store/Browse 之類的連結將 JAVAscript 插入我們的視圖中？內容類型 =&lt;腳本&gt;視窗。位置 = 'http://hackersite.com'&lt;/script&gt;。*</span><span class="sxs-lookup"><span data-stu-id="f28c3-166">*Note: We're using the HttpUtility.HtmlEncode utility method to sanitize the user input. This prevents users from injecting Javascript into our View with a link like /Store/Browse?Genre=&lt;script&gt;window.location='http://hackersite.com'&lt;/script&gt;.*</span></span>

<span data-ttu-id="f28c3-167">現在讓我們流覽至/Store/Browse 嗎？內容類型 = Disco</span><span class="sxs-lookup"><span data-stu-id="f28c3-167">Now let's browse to /Store/Browse?Genre=Disco</span></span>

![](mvc-music-store-part-2/_static/image6.png)

<span data-ttu-id="f28c3-168">接著，讓我們將 [詳細資料] 動作變更為 [讀取]，並顯示名為 ID 的輸入參數。</span><span class="sxs-lookup"><span data-stu-id="f28c3-168">Let's next change the Details action to read and display an input parameter named ID.</span></span> <span data-ttu-id="f28c3-169">與先前的方法不同的是，我們不會將識別碼值內嵌為 querystring 參數。</span><span class="sxs-lookup"><span data-stu-id="f28c3-169">Unlike our previous method, we won't be embedding the ID value as a querystring parameter.</span></span> <span data-ttu-id="f28c3-170">相反地，我們會直接將它內嵌在 URL 本身內。</span><span class="sxs-lookup"><span data-stu-id="f28c3-170">Instead we'll embed it directly within the URL itself.</span></span> <span data-ttu-id="f28c3-171">例如：/Store/Details/5。</span><span class="sxs-lookup"><span data-stu-id="f28c3-171">For example: /Store/Details/5.</span></span>

<span data-ttu-id="f28c3-172">ASP.NET MVC 可讓我們輕鬆執行此動作，而不需要進行任何設定。</span><span class="sxs-lookup"><span data-stu-id="f28c3-172">ASP.NET MVC lets us easily do this without having to configure anything.</span></span> <span data-ttu-id="f28c3-173">ASP.NET MVC 的預設路由慣例是在動作方法名稱之後，將 URL 的區段視為名為 "ID" 的參數。</span><span class="sxs-lookup"><span data-stu-id="f28c3-173">ASP.NET MVC's default routing convention is to treat the segment of a URL after the action method name as a parameter named "ID".</span></span> <span data-ttu-id="f28c3-174">如果您的動作方法具有名為 ID 的參數，則 ASP.NET MVC 會自動將 URL 區段當做參數傳遞給您。</span><span class="sxs-lookup"><span data-stu-id="f28c3-174">If your action method has a parameter named ID then ASP.NET MVC will automatically pass the URL segment to you as a parameter.</span></span>

[!code-csharp[Main](mvc-music-store-part-2/samples/sample5.cs)]

<span data-ttu-id="f28c3-175">執行應用程式，並流覽至/Store/Details/5：</span><span class="sxs-lookup"><span data-stu-id="f28c3-175">Run the application and browse to /Store/Details/5:</span></span>

![](mvc-music-store-part-2/_static/image7.png)

<span data-ttu-id="f28c3-176">我們來回顧到目前為止所做的事：</span><span class="sxs-lookup"><span data-stu-id="f28c3-176">Let's recap what we've done so far:</span></span>

- <span data-ttu-id="f28c3-177">我們已在 Visual Web Developer 中建立新的 ASP.NET MVC 專案</span><span class="sxs-lookup"><span data-stu-id="f28c3-177">We've created a new ASP.NET MVC project in Visual Web Developer</span></span>
- <span data-ttu-id="f28c3-178">我們已討論過 ASP.NET MVC 應用程式的基本資料夾結構</span><span class="sxs-lookup"><span data-stu-id="f28c3-178">We've discussed the basic folder structure of an ASP.NET MVC application</span></span>
- <span data-ttu-id="f28c3-179">我們已瞭解如何使用 ASP.NET 程式開發伺服器來執行我們的網站</span><span class="sxs-lookup"><span data-stu-id="f28c3-179">We've learned how to run our website using the ASP.NET Development Server</span></span>
- <span data-ttu-id="f28c3-180">我們建立了兩個控制器類別： HomeController 和 StoreController</span><span class="sxs-lookup"><span data-stu-id="f28c3-180">We've created two Controller classes: a HomeController and a StoreController</span></span>
- <span data-ttu-id="f28c3-181">我們已在控制器上新增動作方法，以回應 URL 要求並將文字傳回瀏覽器</span><span class="sxs-lookup"><span data-stu-id="f28c3-181">We've added Action Methods to our controllers which respond to URL requests and return text to the browser</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f28c3-182">[上一頁](mvc-music-store-part-1.md)
> [下一頁](mvc-music-store-part-3.md)</span><span class="sxs-lookup"><span data-stu-id="f28c3-182">[Previous](mvc-music-store-part-1.md)
[Next](mvc-music-store-part-3.md)</span></span>
