---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
title: 第3部分： Views 和 Viewmodel |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第3部分涵蓋 Views 和 Viewmodel。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 94297aa0-1f2d-4d72-bbcb-63f64653e0c0
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-3
msc.type: authoredcontent
ms.openlocfilehash: 3fcfc816cde22c697a78bab2c9ea7ace1bf68501
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559805"
---
# <a name="part-3-views-and-viewmodels"></a><span data-ttu-id="9abdd-104">第3部分： Views 和 Viewmodel</span><span class="sxs-lookup"><span data-stu-id="9abdd-104">Part 3: Views and ViewModels</span></span>

<span data-ttu-id="9abdd-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="9abdd-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="9abdd-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="9abdd-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="9abdd-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="9abdd-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>  
>   
> <span data-ttu-id="9abdd-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="9abdd-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="9abdd-109">第3部分涵蓋 Views 和 Viewmodel。</span><span class="sxs-lookup"><span data-stu-id="9abdd-109">Part 3 covers Views and ViewModels.</span></span>

<span data-ttu-id="9abdd-110">到目前為止，我們只是從控制器動作傳回字串。</span><span class="sxs-lookup"><span data-stu-id="9abdd-110">So far we've just been returning strings from controller actions.</span></span> <span data-ttu-id="9abdd-111">這是一種很好的方法，讓您瞭解控制器的工作方式，但不是您想要建立實際 web 應用程式的方式。</span><span class="sxs-lookup"><span data-stu-id="9abdd-111">That's a nice way to get an idea of how controllers work, but it's not how you'd want to build a real web application.</span></span> <span data-ttu-id="9abdd-112">我們想要有更好的方法，讓您將 HTML 傳回到流覽網站的瀏覽器，我們可以使用範本檔案更輕鬆地自訂 HTML 內容送回。</span><span class="sxs-lookup"><span data-stu-id="9abdd-112">We are going to want a better way to generate HTML back to browsers visiting our site – one where we can use template files to more easily customize the HTML content send back.</span></span> <span data-ttu-id="9abdd-113">這正是 Views 的功能。</span><span class="sxs-lookup"><span data-stu-id="9abdd-113">That's exactly what Views do.</span></span>

## <a name="adding-a-view-template"></a><span data-ttu-id="9abdd-114">加入視圖範本</span><span class="sxs-lookup"><span data-stu-id="9abdd-114">Adding a View template</span></span>

<span data-ttu-id="9abdd-115">若要使用視圖範本，我們會將 HomeController Index 方法變更為傳回 ActionResult，並讓它返回 View （），如下所示：</span><span class="sxs-lookup"><span data-stu-id="9abdd-115">To use a view-template, we'll change the HomeController Index method to return an ActionResult, and have it return View(), like below:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample1.cs)]

<span data-ttu-id="9abdd-116">上述變更指出，而不是傳回字串，而是改為使用「View」來產生結果。</span><span class="sxs-lookup"><span data-stu-id="9abdd-116">The above change indicates that instead of returned a string, we instead want to use a "View" to generate a result back.</span></span>

<span data-ttu-id="9abdd-117">我們現在會將適當的視圖範本加入至專案。</span><span class="sxs-lookup"><span data-stu-id="9abdd-117">We'll now add an appropriate View template to our project.</span></span> <span data-ttu-id="9abdd-118">若要這麼做，我們要將文字游標放在索引動作方法內，然後以滑鼠右鍵按一下並選取 [加入視圖]。</span><span class="sxs-lookup"><span data-stu-id="9abdd-118">To do this we'll position the text cursor within the Index action method, then right-click and select "Add View".</span></span> <span data-ttu-id="9abdd-119">這會顯示 [新增視圖] 對話方塊：</span><span class="sxs-lookup"><span data-stu-id="9abdd-119">This will bring up the Add View dialog:</span></span>

<span data-ttu-id="9abdd-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="9abdd-120">![](mvc-music-store-part-3/_static/image1.jpg) ![](mvc-music-store-part-3/_static/image1.png)</span></span>

<span data-ttu-id="9abdd-121">[加入視圖] 對話方塊可讓我們快速且輕鬆地產生視圖範本檔案。</span><span class="sxs-lookup"><span data-stu-id="9abdd-121">The "Add View" dialog allows us to quickly and easily generate View template files.</span></span> <span data-ttu-id="9abdd-122">根據預設，[加入視圖] 對話方塊會預先填入要建立之視圖範本的名稱，使其符合將使用它的動作方法。</span><span class="sxs-lookup"><span data-stu-id="9abdd-122">By default the "Add View" dialog pre-populates the name of the View template to create so that it matches the action method that will use it.</span></span> <span data-ttu-id="9abdd-123">因為我們在 HomeController 的 Index （）動作方法中使用 [新增視圖] 操作功能表，所以上面的 [加入視圖] 對話方塊會有「索引」做為預設預先填入的視圖名稱。</span><span class="sxs-lookup"><span data-stu-id="9abdd-123">Because we used the "Add View" context menu within the Index() action method of our HomeController, the "Add View" dialog above has "Index" as the view name pre-populated by default.</span></span> <span data-ttu-id="9abdd-124">我們不需要變更此對話方塊上的任何選項，因此，請按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9abdd-124">We don't need to change any of the options on this dialog, so click the Add button.</span></span>

<span data-ttu-id="9abdd-125">當我們按一下 [加入] 按鈕時，Visual Web Developer 會在 \Views\Home 目錄中為我們建立新的 [索引] 視圖範本，如果尚未存在，則建立資料夾。</span><span class="sxs-lookup"><span data-stu-id="9abdd-125">When we click the Add button, Visual Web Developer will create a new Index.cshtml view template for us in the \Views\Home directory, creating the folder if doesn't already exist.</span></span>

![](mvc-music-store-part-3/_static/image2.png)

<span data-ttu-id="9abdd-126">"Index. #" 檔案的名稱和資料夾位置很重要，並遵循預設的 ASP.NET MVC 命名慣例。</span><span class="sxs-lookup"><span data-stu-id="9abdd-126">The name and folder location of the "Index.cshtml" file is important, and follows the default ASP.NET MVC naming conventions.</span></span> <span data-ttu-id="9abdd-127">目錄名稱 \Views\Home 會符合名為 HomeController 的控制器。</span><span class="sxs-lookup"><span data-stu-id="9abdd-127">The directory name, \Views\Home, matches the controller - which is named HomeController.</span></span> <span data-ttu-id="9abdd-128">[視圖] 範本名稱 [索引] 符合將顯示此視圖的控制器動作方法。</span><span class="sxs-lookup"><span data-stu-id="9abdd-128">The view template name, Index, matches the controller action method which will be displaying the view.</span></span>

<span data-ttu-id="9abdd-129">當我們使用此命名慣例來傳回視圖時，ASP.NET MVC 可讓我們避免必須明確指定視圖範本的名稱或位置。</span><span class="sxs-lookup"><span data-stu-id="9abdd-129">ASP.NET MVC allows us to avoid having to explicitly specify the name or location of a view template when we use this naming convention to return a view.</span></span> <span data-ttu-id="9abdd-130">當我們在 HomeController 中撰寫如下所示的程式碼時，它會預設呈現 \Views\Home\Index.cshtml view 範本：</span><span class="sxs-lookup"><span data-stu-id="9abdd-130">It will by default render the \Views\Home\Index.cshtml view template when we write code like below within our HomeController:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample2.cs)]

<span data-ttu-id="9abdd-131">在我們按一下 [加入視圖] 對話方塊中的 [新增] 按鈕之後，Visual Web Developer 已建立並開啟 "Index. cshtml" 視圖範本。</span><span class="sxs-lookup"><span data-stu-id="9abdd-131">Visual Web Developer created and opened the "Index.cshtml" view template after we clicked the "Add" button within the "Add View" dialog.</span></span> <span data-ttu-id="9abdd-132">如下列所示，會顯示索引. cshtml 的內容。</span><span class="sxs-lookup"><span data-stu-id="9abdd-132">The contents of Index.cshtml are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample3.cshtml)]

<span data-ttu-id="9abdd-133">此視圖會使用 Razor 語法，這比 ASP.NET Web form 和舊版 ASP.NET MVC 中使用的 Web form view engine 更簡潔。</span><span class="sxs-lookup"><span data-stu-id="9abdd-133">This view is using the Razor syntax, which is more concise than the Web Forms view engine used in ASP.NET Web Forms and previous versions of ASP.NET MVC.</span></span> <span data-ttu-id="9abdd-134">Web form view 引擎仍然可以在 ASP.NET MVC 3 中使用，但許多開發人員發現 Razor view 引擎很適合 ASP.NET MVC 開發。</span><span class="sxs-lookup"><span data-stu-id="9abdd-134">The Web Forms view engine is still available in ASP.NET MVC 3, but many developers find that the Razor view engine fits ASP.NET MVC development really well.</span></span>

<span data-ttu-id="9abdd-135">前三行使用 ViewBag 來設定頁面標題。</span><span class="sxs-lookup"><span data-stu-id="9abdd-135">The first three lines set the page title using ViewBag.Title.</span></span> <span data-ttu-id="9abdd-136">我們很快就會介紹這項功能的運作方式，但首先讓我們更新文字標題文字並查看頁面。</span><span class="sxs-lookup"><span data-stu-id="9abdd-136">We'll look at how this works in more detail soon, but first let's update the text heading text and view the page.</span></span> <span data-ttu-id="9abdd-137">將 &lt;h2&gt; 標記更新為 [這是首頁]，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9abdd-137">Update the &lt;h2&gt; tag to say "This is the Home Page" as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample4.cshtml)]

<span data-ttu-id="9abdd-138">執行應用程式時，會顯示在首頁上可以看到我們的新文字。</span><span class="sxs-lookup"><span data-stu-id="9abdd-138">Running the application shows that our new text is visible on the home page.</span></span>

![](mvc-music-store-part-3/_static/image3.png)

## <a name="using-a-layout-for-common-site-elements"></a><span data-ttu-id="9abdd-139">使用通用網站元素的版面配置</span><span class="sxs-lookup"><span data-stu-id="9abdd-139">Using a Layout for common site elements</span></span>

<span data-ttu-id="9abdd-140">大部分網站都有許多頁面之間共用的內容：導覽、頁尾、標誌影像、樣式表單參考等等。Razor view 引擎可讓您輕鬆地使用稱為 \_Layout 的頁面來進行管理，並在/Views/Shared 資料夾內自動為我們建立。</span><span class="sxs-lookup"><span data-stu-id="9abdd-140">Most websites have content which is shared between many pages: navigation, footers, logo images, stylesheet references, etc. The Razor view engine makes this easy to manage using a page called \_Layout.cshtml which has automatically been created for us inside the /Views/Shared folder.</span></span>

![](mvc-music-store-part-3/_static/image4.png)

<span data-ttu-id="9abdd-141">按兩下此資料夾以查看內容，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9abdd-141">Double-click on this folder to view the contents, which are shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample5.cshtml)]

<span data-ttu-id="9abdd-142">來自個別視圖的內容將會由 @RenderBody（）命令顯示，而我們想要出現在外的任何一般內容，都可以加入 \_Layout 標記中。</span><span class="sxs-lookup"><span data-stu-id="9abdd-142">The content from our individual views will be displayed by the @RenderBody() command, and any common content that we want to appear outside of that can be added to the \_Layout.cshtml markup.</span></span> <span data-ttu-id="9abdd-143">我們會想要讓 MVC 音樂存放區有一個通用標題，其中包含首頁的連結，以及網站中所有頁面的存放區，因此我們會將其新增至範本中的 @RenderBody（）語句正上方。</span><span class="sxs-lookup"><span data-stu-id="9abdd-143">We'll want our MVC Music Store to have a common header with links to our Home page and Store area on all pages in the site, so we'll add that to the template directly above that @RenderBody() statement.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample6.cshtml)]

## <a name="updating-the-stylesheet"></a><span data-ttu-id="9abdd-144">更新樣式表單</span><span class="sxs-lookup"><span data-stu-id="9abdd-144">Updating the StyleSheet</span></span>

<span data-ttu-id="9abdd-145">空白專案範本包含非常簡單的 CSS 檔案，其中只包含用來顯示驗證訊息的樣式。</span><span class="sxs-lookup"><span data-stu-id="9abdd-145">The empty project template includes a very streamlined CSS file which just includes styles used to display validation messages.</span></span> <span data-ttu-id="9abdd-146">我們的設計工具提供了一些額外的 CSS 和影像，可定義網站的外觀與風格，因此我們將在現在新增這些功能。</span><span class="sxs-lookup"><span data-stu-id="9abdd-146">Our designer has provided some additional CSS and images to define the look and feel for our site, so we'll add those in now.</span></span>

<span data-ttu-id="9abdd-147">已更新的 CSS 檔案和影像會包含在 MvcMusicStore-Assets 的內容目錄中，可在 [ [MVC-音樂] 存放區](https://github.com/evilDave/MVC-Music-Store)取得。</span><span class="sxs-lookup"><span data-stu-id="9abdd-147">The updated CSS file and Images are included in the Content directory of MvcMusicStore-Assets.zip which is available at [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span> <span data-ttu-id="9abdd-148">我們會在 Windows Explorer 中選取這兩個專案，並將其放入 Visual Web Developer 中解決方案的 Content 資料夾，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9abdd-148">We'll select both of them in Windows Explorer and drop them into our Solution's Content folder in Visual Web Developer, as shown below:</span></span>

![](mvc-music-store-part-3/_static/image5.png)

<span data-ttu-id="9abdd-149">系統會要求您確認是否要覆寫現有的網站 .css 檔案。</span><span class="sxs-lookup"><span data-stu-id="9abdd-149">You'll be asked to confirm if you want to overwrite the existing Site.css file.</span></span> <span data-ttu-id="9abdd-150">按一下 [是]。</span><span class="sxs-lookup"><span data-stu-id="9abdd-150">Click Yes.</span></span>

![](mvc-music-store-part-3/_static/image6.png)

<span data-ttu-id="9abdd-151">應用程式的 Content 資料夾現在會如下所示：</span><span class="sxs-lookup"><span data-stu-id="9abdd-151">The Content folder of your application will now appear as follows:</span></span>

![](mvc-music-store-part-3/_static/image7.png)

<span data-ttu-id="9abdd-152">現在讓我們來執行應用程式，並在首頁上查看變更的外觀。</span><span class="sxs-lookup"><span data-stu-id="9abdd-152">Now let's run the application and see how our changes look on the Home page.</span></span>

![](mvc-music-store-part-3/_static/image8.png)

- <span data-ttu-id="9abdd-153">讓我們來複習一下變更的內容： HomeController 的索引動作方法已找到並顯示 \Views\Home\Index.cshtmlView 範本，雖然我們的程式碼稱為 "return View （）"，因為我們的視圖範本遵循標準命名慣例。</span><span class="sxs-lookup"><span data-stu-id="9abdd-153">Let's review what's changed: The HomeController's Index action method found and displayed the \Views\Home\Index.cshtmlView template, even though our code called "return View()", because our View template followed the standard naming convention.</span></span>
- <span data-ttu-id="9abdd-154">首頁會顯示在 \Views\Home\Index.cshtml view 範本內定義的簡單歡迎訊息。</span><span class="sxs-lookup"><span data-stu-id="9abdd-154">The Home Page is displaying a simple welcome message that is defined within the \Views\Home\Index.cshtml view template.</span></span>
- <span data-ttu-id="9abdd-155">首頁是使用我們的 \_Layout 範本，因此歡迎訊息包含在標準網站 HTML 版面配置中。</span><span class="sxs-lookup"><span data-stu-id="9abdd-155">The Home Page is using our \_Layout.cshtml template, and so the welcome message is contained within the standard site HTML layout.</span></span>

## <a name="using-a-model-to-pass-information-to-our-view"></a><span data-ttu-id="9abdd-156">使用模型將資訊傳遞至我們的視圖</span><span class="sxs-lookup"><span data-stu-id="9abdd-156">Using a Model to pass information to our View</span></span>

<span data-ttu-id="9abdd-157">只顯示硬式編碼 HTML 的視圖範本不會產生非常有趣的網站。</span><span class="sxs-lookup"><span data-stu-id="9abdd-157">A View template that just displays hardcoded HTML isn't going to make a very interesting web site.</span></span> <span data-ttu-id="9abdd-158">為了建立動態網站，我們會改為將控制器動作的資訊傳遞至我們的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="9abdd-158">To create a dynamic web site, we'll instead want to pass information from our controller actions to our view templates.</span></span>

<span data-ttu-id="9abdd-159">在模型視圖控制器模式中，「模型」一詞指的是代表應用程式中資料的物件。</span><span class="sxs-lookup"><span data-stu-id="9abdd-159">In the Model-View-Controller pattern, the term Model refers to objects which represent the data in the application.</span></span> <span data-ttu-id="9abdd-160">通常，模型物件會對應至資料庫中的資料表，但不一定要這麼做。</span><span class="sxs-lookup"><span data-stu-id="9abdd-160">Often, model objects correspond to tables in your database, but they don't have to.</span></span>

<span data-ttu-id="9abdd-161">傳回 ActionResult 的控制器動作方法可以將模型物件傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="9abdd-161">Controller action methods which return an ActionResult can pass a model object to the view.</span></span> <span data-ttu-id="9abdd-162">這可讓控制器完全封裝產生回應所需的所有資訊，然後將此資訊傳送到 View 範本，用來產生適當的 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="9abdd-162">This allows a Controller to cleanly package up all the information needed to generate a response, and then pass this information off to a View template to use to generate the appropriate HTML response.</span></span> <span data-ttu-id="9abdd-163">藉由查看其運作方式最容易瞭解，讓我們開始吧。</span><span class="sxs-lookup"><span data-stu-id="9abdd-163">This is easiest to understand by seeing it in action, so let's get started.</span></span>

<span data-ttu-id="9abdd-164">首先，我們將建立一些模型類別，以代表我們存放區內的內容類型和專輯。</span><span class="sxs-lookup"><span data-stu-id="9abdd-164">First we'll create some Model classes to represent Genres and Albums within our store.</span></span> <span data-ttu-id="9abdd-165">讓我們從建立內容類型類別開始。</span><span class="sxs-lookup"><span data-stu-id="9abdd-165">Let's start by creating a Genre class.</span></span> <span data-ttu-id="9abdd-166">以滑鼠右鍵按一下專案中的 [模型] 資料夾，選擇 [新增類別] 選項，並將檔案命名為 "Genre.cs"。</span><span class="sxs-lookup"><span data-stu-id="9abdd-166">Right-click the "Models" folder within your project, choose the "Add Class" option, and name the file "Genre.cs".</span></span>

![](mvc-music-store-part-3/_static/image2.jpg)

![](mvc-music-store-part-3/_static/image9.png)

<span data-ttu-id="9abdd-167">然後將 [公用字串名稱] 屬性加入至已建立的類別：</span><span class="sxs-lookup"><span data-stu-id="9abdd-167">Then add a public string Name property to the class that was created:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample7.cs)]

<span data-ttu-id="9abdd-168">*注意：如果您想要的話，{get; set;} 標記法會使用C#的自動執行屬性功能。這讓我們有屬性的優點，而不需要我們宣告支援欄位。*</span><span class="sxs-lookup"><span data-stu-id="9abdd-168">*Note: In case you're wondering, the { get; set; } notation is making use of C#'s auto-implemented properties feature. This gives us the benefits of a property without requiring us to declare a backing field.*</span></span>

<span data-ttu-id="9abdd-169">接下來，請遵循相同的步驟來建立具有 [標題] 和 [內容類型] 屬性的專輯類別（名為 Album.cs）：</span><span class="sxs-lookup"><span data-stu-id="9abdd-169">Next, follow the same steps to create an Album class (named Album.cs) that has a Title and a Genre property:</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample8.cs)]

<span data-ttu-id="9abdd-170">現在我們可以修改 StoreController，以使用可顯示模型中動態資訊的 Views。</span><span class="sxs-lookup"><span data-stu-id="9abdd-170">Now we can modify the StoreController to use Views which display dynamic information from our Model.</span></span> <span data-ttu-id="9abdd-171">如果現在是-基於示範目的，我們根據要求識別碼來命名專輯，我們可以如下圖所示顯示該資訊。</span><span class="sxs-lookup"><span data-stu-id="9abdd-171">If - for demonstration purposes right now - we named our Albums based on the request ID, we could display that information as in the view below.</span></span>

![](mvc-music-store-part-3/_static/image10.png)

<span data-ttu-id="9abdd-172">我們會先變更 [Store Details] 動作，讓它顯示單一專輯的資訊。</span><span class="sxs-lookup"><span data-stu-id="9abdd-172">We'll start by changing the Store Details action so it shows the information for a single album.</span></span> <span data-ttu-id="9abdd-173">在**StoreControllers**類別的頂端新增 "using" 語句以包含 MvcMusicStore 命名空間，因此我們不需要在每次想要使用專輯類別時輸入 MvcMusicStore。</span><span class="sxs-lookup"><span data-stu-id="9abdd-173">Add a "using" statement to the top of the **StoreControllers** class to include the MvcMusicStore.Models namespace, so we don't need to type MvcMusicStore.Models.Album every time we want to use the album class.</span></span> <span data-ttu-id="9abdd-174">該類別的 "using" 區段現在應該會顯示如下。</span><span class="sxs-lookup"><span data-stu-id="9abdd-174">The "usings" section of that class should now appear as below.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample9.cs)]

<span data-ttu-id="9abdd-175">接下來，我們會更新詳細資料控制器動作，讓它傳回 ActionResult，而不是字串，就像我們使用 HomeController 的 Index 方法所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="9abdd-175">Next, we'll update the Details controller action so that it returns an ActionResult rather than a string, as we did with the HomeController's Index method.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample10.cs)]

<span data-ttu-id="9abdd-176">現在我們可以修改邏輯，將專輯物件傳回給視圖。</span><span class="sxs-lookup"><span data-stu-id="9abdd-176">Now we can modify the logic to return an Album object to the view.</span></span> <span data-ttu-id="9abdd-177">稍後在本教學課程中，我們將從資料庫中抓取資料，但現在我們會使用「虛擬資料」來開始。</span><span class="sxs-lookup"><span data-stu-id="9abdd-177">Later in this tutorial we will be retrieving the data from a database – but for right now we will use "dummy data" to get started.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample11.cs)]

<span data-ttu-id="9abdd-178">*注意：如果您不熟悉C#，您可能會假設使用 var 表示我們的專輯變數是晚期繫結。這不正確， C#編譯器會根據我們指派給變數的內容來使用型別推斷，以判斷專輯是專輯類型，並將本機專輯變數編譯為專輯類型，因此我們會取得編譯時期檢查，並 Visual Studio 程式碼編輯器支援。*</span><span class="sxs-lookup"><span data-stu-id="9abdd-178">*Note: If you're unfamiliar with C#, you may assume that using var means that our album variable is late-bound. That's not correct – the C# compiler is using type-inference based on what we're assigning to the variable to determine that album is of type Album and compiling the local album variable as an Album type, so we get compile-time checking and Visual Studio code-editor support.*</span></span>

<span data-ttu-id="9abdd-179">現在讓我們建立一個使用專輯的視圖範本來產生 HTML 回應。</span><span class="sxs-lookup"><span data-stu-id="9abdd-179">Let's now create a View template that uses our Album to generate an HTML response.</span></span> <span data-ttu-id="9abdd-180">在這麼做之前，我們必須先建立專案，讓 [加入視圖] 對話方塊知道我們新建立的專輯類別。</span><span class="sxs-lookup"><span data-stu-id="9abdd-180">Before we do that we need to build the project so that the Add View dialog knows about our newly created Album class.</span></span> <span data-ttu-id="9abdd-181">您可以藉由選取 [Debug ⇨ Build MvcMusicStore] 功能表項目來建立專案（如需額外的點數，您可以使用 Ctrl + Shift-B 快捷方式來建立專案）。</span><span class="sxs-lookup"><span data-stu-id="9abdd-181">You can build the project by selecting the Debug⇨Build MvcMusicStore menu item (for extra credit, you can use the Ctrl-Shift-B shortcut to build the project).</span></span>

![](mvc-music-store-part-3/_static/image11.png)

<span data-ttu-id="9abdd-182">既然我們已設定支援的類別，我們就可以開始建立我們的 View 範本。</span><span class="sxs-lookup"><span data-stu-id="9abdd-182">Now that we've set up our supporting classes, we're ready to build our View template.</span></span> <span data-ttu-id="9abdd-183">以滑鼠右鍵按一下詳細資料方法，然後選取 [加入視圖 ...]從內容功能表。</span><span class="sxs-lookup"><span data-stu-id="9abdd-183">Right-click within the Details method and select "Add View…" from the context menu.</span></span>

![](mvc-music-store-part-3/_static/image12.png)

<span data-ttu-id="9abdd-184">我們會建立新的視圖範本，就像我們之前使用 HomeController 一樣。</span><span class="sxs-lookup"><span data-stu-id="9abdd-184">We are going to create a new View template like we did before with the HomeController.</span></span> <span data-ttu-id="9abdd-185">因為我們是從 StoreController 建立它，所以預設會在 \Views\Store\Index.cshtml 檔案中產生。</span><span class="sxs-lookup"><span data-stu-id="9abdd-185">Because we are creating it from the StoreController it will by default be generated in a \Views\Store\Index.cshtml file.</span></span>

<span data-ttu-id="9abdd-186">與之前不同的是，我們要核取 [建立強型別] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="9abdd-186">Unlike before, we are going to check the "Create a strongly-typed" view checkbox.</span></span> <span data-ttu-id="9abdd-187">接著，我們要在「View data class」（downlist）中選取「專輯」類別。</span><span class="sxs-lookup"><span data-stu-id="9abdd-187">We are then going to select our "Album" class within the "View data-class" drop-downlist.</span></span> <span data-ttu-id="9abdd-188">這會導致 [加入視圖] 對話方塊建立一個需要將專輯物件傳遞給它使用的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="9abdd-188">This will cause the "Add View" dialog to create a View template that expects that an Album object will be passed to it to use.</span></span>

![](mvc-music-store-part-3/_static/image13.png)

<span data-ttu-id="9abdd-189">當我們按一下 [新增] 按鈕時，將會建立 \Views\Store\Details.cshtml View 範本，其中包含下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="9abdd-189">When we click the "Add" button our \Views\Store\Details.cshtml View template will be created, containing the following code.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample12.cshtml)]

<span data-ttu-id="9abdd-190">請注意第一行，這表示此視圖已針對我們的專輯類別進行強型別。</span><span class="sxs-lookup"><span data-stu-id="9abdd-190">Notice the first line, which indicates that this view is strongly-typed to our Album class.</span></span> <span data-ttu-id="9abdd-191">Razor view 引擎瞭解它已通過專輯物件，因此我們可以輕鬆地存取模型屬性，甚至能夠在 Visual Web Developer editor 中取得 IntelliSense 的優點。</span><span class="sxs-lookup"><span data-stu-id="9abdd-191">The Razor view engine understands that it has been passed an Album object, so we can easily access model properties and even have the benefit of IntelliSense in the Visual Web Developer editor.</span></span>

<span data-ttu-id="9abdd-192">更新 &lt;h2&gt; 標記，讓它藉由修改該行以顯示專輯的 Title 屬性，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9abdd-192">Update the &lt;h2&gt; tag so it displays the Album's Title property by modifying that line to appear as follows.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample13.cshtml)]

<span data-ttu-id="9abdd-193">請注意，當您在 @Model 關鍵字之後輸入句點時，會觸發 IntelliSense，其中顯示專輯類別支援的屬性和方法。</span><span class="sxs-lookup"><span data-stu-id="9abdd-193">Notice that IntelliSense is triggered when you enter the period after the @Model keyword, showing the properties and methods that the Album class supports.</span></span>

<span data-ttu-id="9abdd-194">現在讓我們重新執行專案，並造訪/Store/Details/5 URL。</span><span class="sxs-lookup"><span data-stu-id="9abdd-194">Let's now re-run our project and visit the /Store/Details/5 URL.</span></span> <span data-ttu-id="9abdd-195">我們會看到專輯的詳細資料，如下所示。</span><span class="sxs-lookup"><span data-stu-id="9abdd-195">We'll see details of an Album like below.</span></span>

![](mvc-music-store-part-3/_static/image14.png)

<span data-ttu-id="9abdd-196">現在，我們將針對 Store 流覽動作方法進行類似的更新。</span><span class="sxs-lookup"><span data-stu-id="9abdd-196">Now we'll make a similar update for the Store Browse action method.</span></span> <span data-ttu-id="9abdd-197">更新方法，使其傳回 ActionResult，並修改方法邏輯，讓它建立新的類型物件，並將它傳回給視圖。</span><span class="sxs-lookup"><span data-stu-id="9abdd-197">Update the method so it returns an ActionResult, and modify the method logic so it creates a new Genre object and returns it to the View.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample14.cs)]

<span data-ttu-id="9abdd-198">在流覽方法上按一下滑鼠右鍵，然後選取 [新增 View ...]從操作功能表中，新增強型別的視圖，將強型別加入至內容類型類別。</span><span class="sxs-lookup"><span data-stu-id="9abdd-198">Right-click in the Browse method and select "Add View…" from the context menu, then add a View that is strongly-typed add a strongly typed to the Genre class.</span></span>

![](mvc-music-store-part-3/_static/image15.png)

<span data-ttu-id="9abdd-199">更新 view 程式碼中的 &lt;h2&gt; 元素（在/Views/Store/Browse.cshtml 中），以顯示內容類型資訊。</span><span class="sxs-lookup"><span data-stu-id="9abdd-199">Update the &lt;h2&gt; element in the view code (in /Views/Store/Browse.cshtml) to display the Genre information.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample15.cshtml)]

<span data-ttu-id="9abdd-200">現在讓我們重新執行專案，並流覽至/Store/Browse？內容類型 = Disco URL。</span><span class="sxs-lookup"><span data-stu-id="9abdd-200">Now let's re-run our project and browse to the /Store/Browse?Genre=Disco URL.</span></span> <span data-ttu-id="9abdd-201">我們會看到如下所示的流覽頁面。</span><span class="sxs-lookup"><span data-stu-id="9abdd-201">We'll see the Browse page displayed like below.</span></span>

![](mvc-music-store-part-3/_static/image16.png)

<span data-ttu-id="9abdd-202">最後，讓我們對**存放區索引**動作方法和 view 進行稍微比較複雜的更新，以顯示我們存放區中所有內容的清單。</span><span class="sxs-lookup"><span data-stu-id="9abdd-202">Finally, let's make a slightly more complex update to the **Store Index** action method and view to display a list of all the Genres in our store.</span></span> <span data-ttu-id="9abdd-203">我們會使用內容清單做為模型物件，而不只是單一內容類型來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="9abdd-203">We'll do that by using a List of Genres as our model object, rather than just a single Genre.</span></span>

[!code-csharp[Main](mvc-music-store-part-3/samples/sample16.cs)]

<span data-ttu-id="9abdd-204">以滑鼠右鍵按一下 [存放區索引動作] 方法，然後依序選取 [加入視圖]，選取 [內容類型] 做為模型類別，然後按 [加入] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="9abdd-204">Right-click in the Store Index action method and select Add View as before, select Genre as the Model class, and press the Add button.</span></span>

![](mvc-music-store-part-3/_static/image17.png)

<span data-ttu-id="9abdd-205">首先，我們將變更 @model 宣告，以指出此視圖會預期有數個內容類型物件，而不是只有一個。</span><span class="sxs-lookup"><span data-stu-id="9abdd-205">First we'll change the @model declaration to indicate that the view will be expecting several Genre objects rather than just one.</span></span> <span data-ttu-id="9abdd-206">將/Store/Index.cshtml 的第一行變更為 [讀取]，如下所示：</span><span class="sxs-lookup"><span data-stu-id="9abdd-206">Change the first line of /Store/Index.cshtml to read as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample17.cshtml)]

<span data-ttu-id="9abdd-207">這會告訴 Razor view 引擎，它將使用可以保存數個內容類型物件的模型物件。</span><span class="sxs-lookup"><span data-stu-id="9abdd-207">This tells the Razor view engine that it will be working with a model object that can hold several Genre objects.</span></span> <span data-ttu-id="9abdd-208">我們使用 IEnumerable&lt;內容類型&gt;，而不是清單&gt;&lt;類型類型，因為它較通用，可讓我們將模型類型稍後變更為支援 IEnumerable 介面的任何物件類型。</span><span class="sxs-lookup"><span data-stu-id="9abdd-208">We're using an IEnumerable&lt;Genre&gt; rather than a List&lt;Genre&gt; since it's more generic, allowing us to change our model type later to any object type that supports the IEnumerable interface.</span></span>

<span data-ttu-id="9abdd-209">接下來，我們會迴圈處理模型中的內容類型物件，如下列已完成的視圖程式碼所示。</span><span class="sxs-lookup"><span data-stu-id="9abdd-209">Next, we'll loop through the Genre objects in the model as shown in the completed view code below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample18.cshtml)]

<span data-ttu-id="9abdd-210">請注意，當我們輸入這段程式碼時，我們有完整的 IntelliSense 支援，因此當我們鍵入「@Model」時。</span><span class="sxs-lookup"><span data-stu-id="9abdd-210">Notice that we have full IntelliSense support as we enter this code, so that when we type "@Model."</span></span> <span data-ttu-id="9abdd-211">我們會看到型別類型的 IEnumerable 所支援的所有方法和屬性。</span><span class="sxs-lookup"><span data-stu-id="9abdd-211">we see all methods and properties supported by an IEnumerable of type Genre.</span></span>

![](mvc-music-store-part-3/_static/image18.png)

<span data-ttu-id="9abdd-212">在我們的 "foreach" 迴圈內，Visual Web Developer 知道每個專案都屬於類型類型，因此我們會看到每個類型的 IntelliSense。</span><span class="sxs-lookup"><span data-stu-id="9abdd-212">Within our "foreach" loop, Visual Web Developer knows that each item is of type Genre, so we see IntelliSense for each the Genre type.</span></span>

![](mvc-music-store-part-3/_static/image19.png)

<span data-ttu-id="9abdd-213">接下來，[樣板] 功能會檢查內容類型物件，並判斷每個都有一個 Name 屬性，因此它會迴圈執行並將其寫出。它也會產生每個個別專案的編輯、詳細資料和刪除連結。</span><span class="sxs-lookup"><span data-stu-id="9abdd-213">Next, the scaffolding feature examined the Genre object and determined that each will have a Name property, so it loops through and writes them out. It also generates Edit, Details, and Delete links to each individual item.</span></span> <span data-ttu-id="9abdd-214">我們稍後將在我們的存放區管理員中利用這項功能，但現在我們想要改為使用簡單的清單。</span><span class="sxs-lookup"><span data-stu-id="9abdd-214">We'll take advantage of that later in our store manager, but for now we'd like to have a simple list instead.</span></span>

<span data-ttu-id="9abdd-215">當我們執行應用程式並流覽至/Store 時，我們會看到顯示的是 [計數] 和 [清單]。</span><span class="sxs-lookup"><span data-stu-id="9abdd-215">When we run the application and browse to /Store, we see that both the count and list of Genres is displayed.</span></span>

![](mvc-music-store-part-3/_static/image20.png)

## <a name="adding-links-between-pages"></a><span data-ttu-id="9abdd-216">在頁面之間新增連結</span><span class="sxs-lookup"><span data-stu-id="9abdd-216">Adding Links between pages</span></span>

<span data-ttu-id="9abdd-217">列出內容類型的/Store URL 目前只會將內容類型名稱列出為純文字。</span><span class="sxs-lookup"><span data-stu-id="9abdd-217">Our /Store URL that lists Genres currently lists the Genre names simply as plain text.</span></span> <span data-ttu-id="9abdd-218">讓我們變更此專案，讓我們改為將內容類型名稱連結至適當的/Store/Browse URL，讓按一下音樂類型（如「Disco」）會流覽至/Store/Browse？內容類型 = Disco URL。</span><span class="sxs-lookup"><span data-stu-id="9abdd-218">Let's change this so that instead of plain text we instead have the Genre names link to the appropriate /Store/Browse URL, so that clicking on a music genre like "Disco" will navigate to the /Store/Browse?genre=Disco URL.</span></span> <span data-ttu-id="9abdd-219">我們可以使用如下的程式碼來更新 \Views\Store\Index.cshtml View 範本，以輸出這些連結 **（不要在此輸入-我們將在此進行改善）** ：</span><span class="sxs-lookup"><span data-stu-id="9abdd-219">We could update our \Views\Store\Index.cshtml View template to output these links using code like below **(don't type this in - we're going to improve on it)**:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample19.html)]

<span data-ttu-id="9abdd-220">這是可行的，但之後可能會導致問題，因為它依賴硬式編碼的字串。</span><span class="sxs-lookup"><span data-stu-id="9abdd-220">That works, but it could lead to trouble later since it relies on a hardcoded string.</span></span> <span data-ttu-id="9abdd-221">比方說，如果我們想要重新命名控制器，我們需要搜尋程式碼，尋找需要更新的連結。</span><span class="sxs-lookup"><span data-stu-id="9abdd-221">For instance, if we wanted to rename the Controller, we'd need to search through our code looking for links that need to be updated.</span></span>

<span data-ttu-id="9abdd-222">我們可以使用的替代方法是利用 HTML Helper 方法。</span><span class="sxs-lookup"><span data-stu-id="9abdd-222">An alternative approach we can use is to take advantage of an HTML Helper method.</span></span> <span data-ttu-id="9abdd-223">ASP.NET MVC 包含 HTML Helper 方法，可從我們的 View 範本程式碼取得，以執行像這樣的各種常見工作。</span><span class="sxs-lookup"><span data-stu-id="9abdd-223">ASP.NET MVC includes HTML Helper methods which are available from our View template code to perform a variety of common tasks just like this.</span></span> <span data-ttu-id="9abdd-224">.Html （） helper 方法特別有用，可讓您輕鬆地建立 HTML &lt;&gt; 連結，並處理討厭的詳細資料，例如確定 URL 路徑的 URL 編碼正確。</span><span class="sxs-lookup"><span data-stu-id="9abdd-224">The Html.ActionLink() helper method is a particularly useful one, and makes it easy to build HTML &lt;a&gt; links and takes care of annoying details like making sure URL paths are properly URL encoded.</span></span>

<span data-ttu-id="9abdd-225">.Html （）有數個不同的多載，可讓您盡可能指定連結所需的資訊。</span><span class="sxs-lookup"><span data-stu-id="9abdd-225">Html.ActionLink() has several different overloads to allow specifying as much information as you need for your links.</span></span> <span data-ttu-id="9abdd-226">在最簡單的情況下，只要按一下用戶端上的超連結，您就只會提供連結文字和動作方法來移至。</span><span class="sxs-lookup"><span data-stu-id="9abdd-226">In the simplest case, you'll supply just the link text and the Action method to go to when the hyperlink is clicked on the client.</span></span> <span data-ttu-id="9abdd-227">例如，我們可以使用下列呼叫，連結至存放區詳細資料頁面上的 "/Store/" Index （）方法，並將連結文字「移至存放區索引」：</span><span class="sxs-lookup"><span data-stu-id="9abdd-227">For example, we can link to "/Store/" Index() method on the Store Details page with the link text "Go to the Store Index" using the following call:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample20.cshtml)]

<span data-ttu-id="9abdd-228">*注意：在此情況下，我們不需要指定控制器名稱，因為我們只會連結至呈現目前視圖的相同控制器內的另一個動作。*</span><span class="sxs-lookup"><span data-stu-id="9abdd-228">*Note: In this case, we didn't need to specify the controller name because we're just linking to another action within the same controller that's rendering the current view.*</span></span>

<span data-ttu-id="9abdd-229">我們的流覽頁面連結必須傳遞參數，因此我們將會使用採用三個參數的 .Html 方法的另一個多載：</span><span class="sxs-lookup"><span data-stu-id="9abdd-229">Our links to the Browse page will need to pass a parameter, though, so we'll use another overload of the Html.ActionLink method that takes three parameters:</span></span>

- 1. <span data-ttu-id="9abdd-230">連結文字，會顯示內容類型名稱</span><span class="sxs-lookup"><span data-stu-id="9abdd-230">Link text, which will display the Genre name</span></span>
- 2. <span data-ttu-id="9abdd-231">控制器動作名稱（流覽）</span><span class="sxs-lookup"><span data-stu-id="9abdd-231">Controller action name (Browse)</span></span>
- 3. <span data-ttu-id="9abdd-232">路由參數值，同時指定名稱（內容類型）和值（內容類型名稱）</span><span class="sxs-lookup"><span data-stu-id="9abdd-232">Route parameter values, specifying both the name (Genre) and the value (Genre name)</span></span>

<span data-ttu-id="9abdd-233">總之，以下是我們將這些連結寫到商店索引視圖的方式：</span><span class="sxs-lookup"><span data-stu-id="9abdd-233">Putting that all together, here's how we'll write those links to the Store Index view:</span></span>

[!code-cshtml[Main](mvc-music-store-part-3/samples/sample21.cshtml)]

<span data-ttu-id="9abdd-234">現在當我們再次執行專案並存取/Store/URL 時，我們會看到一份內容清單。</span><span class="sxs-lookup"><span data-stu-id="9abdd-234">Now when we run our project again and access the /Store/ URL we will see a list of genres.</span></span> <span data-ttu-id="9abdd-235">每個內容類型都是超連結–按一下時，會將我們帶到我們的/Store/Browse？內容類型 = [內容類型 *]* URL。</span><span class="sxs-lookup"><span data-stu-id="9abdd-235">Each genre is a hyperlink – when clicked it will take us to our /Store/Browse?genre=*[genre]* URL.</span></span>

![](mvc-music-store-part-3/_static/image3.jpg)

<span data-ttu-id="9abdd-236">內容類型清單的 HTML 看起來像這樣：</span><span class="sxs-lookup"><span data-stu-id="9abdd-236">The HTML for the genre list looks like this:</span></span>

[!code-html[Main](mvc-music-store-part-3/samples/sample22.html)]

> [!div class="step-by-step"]
> <span data-ttu-id="9abdd-237">[上一頁](mvc-music-store-part-2.md)
> [下一頁](mvc-music-store-part-4.md)</span><span class="sxs-lookup"><span data-stu-id="9abdd-237">[Previous](mvc-music-store-part-2.md)
[Next](mvc-music-store-part-4.md)</span></span>
