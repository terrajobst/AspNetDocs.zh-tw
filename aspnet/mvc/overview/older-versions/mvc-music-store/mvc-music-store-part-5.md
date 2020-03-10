---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
title: 第5部分：編輯表單和範本化 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第5部分涵蓋編輯表單和範本化。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: 6b09413a-6d6a-425a-87c9-629f91b91b28
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-5
msc.type: authoredcontent
ms.openlocfilehash: 20b99cbe57b5dfa623205838a5929733a6c2d70d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559546"
---
# <a name="part-5-edit-forms-and-templating"></a><span data-ttu-id="0331e-104">第5部分：編輯表單和範本化</span><span class="sxs-lookup"><span data-stu-id="0331e-104">Part 5: Edit Forms and Templating</span></span>

<span data-ttu-id="0331e-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="0331e-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="0331e-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="0331e-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="0331e-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="0331e-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="0331e-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="0331e-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="0331e-109">第5部分涵蓋編輯表單和範本化。</span><span class="sxs-lookup"><span data-stu-id="0331e-109">Part 5 covers Edit Forms and Templating.</span></span>

<span data-ttu-id="0331e-110">在過去的章節中，我們會從資料庫載入資料並加以顯示。</span><span class="sxs-lookup"><span data-stu-id="0331e-110">In the past chapter, we were loading data from our database and displaying it.</span></span> <span data-ttu-id="0331e-111">在本章中，我們也會啟用資料的編輯。</span><span class="sxs-lookup"><span data-stu-id="0331e-111">In this chapter, we'll also enable editing the data.</span></span>

## <a name="creating-the-storemanagercontroller"></a><span data-ttu-id="0331e-112">建立 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="0331e-112">Creating the StoreManagerController</span></span>

<span data-ttu-id="0331e-113">首先，我們會建立名為**StoreManagerController**的新控制器。</span><span class="sxs-lookup"><span data-stu-id="0331e-113">We'll begin by creating a new controller called **StoreManagerController**.</span></span> <span data-ttu-id="0331e-114">在此控制器中，我們將會利用 ASP.NET MVC 3 工具更新中提供的基本架構功能。</span><span class="sxs-lookup"><span data-stu-id="0331e-114">For this controller, we will be taking advantage of the Scaffolding features available in the ASP.NET MVC 3 Tools Update.</span></span> <span data-ttu-id="0331e-115">設定 [新增控制器] 對話方塊的選項，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0331e-115">Set the options for the Add Controller dialog as shown below.</span></span>

![](mvc-music-store-part-5/_static/image1.png)

<span data-ttu-id="0331e-116">當您按一下 [新增] 按鈕時，您會看到 ASP.NET MVC 3 [樣板] 機制會為您執行良好的工作量：</span><span class="sxs-lookup"><span data-stu-id="0331e-116">When you click the Add button, you'll see that the ASP.NET MVC 3 scaffolding mechanism does a good amount of work for you:</span></span>

- <span data-ttu-id="0331e-117">它會建立具有本機 Entity Framework 變數的新 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="0331e-117">It creates the new StoreManagerController with a local Entity Framework variable</span></span>
- <span data-ttu-id="0331e-118">它會將 [StoreManager] 資料夾新增至專案的 [Views] 資料夾</span><span class="sxs-lookup"><span data-stu-id="0331e-118">It adds a StoreManager folder to the project's Views folder</span></span>
- <span data-ttu-id="0331e-119">它會加入建立的. cshtml、Delete. cshtml、Details、. cshtml 和 Index. cshtml 視圖，強型別到專輯類別</span><span class="sxs-lookup"><span data-stu-id="0331e-119">It adds Create.cshtml, Delete.cshtml, Details.cshtml, Edit.cshtml, and Index.cshtml view, strongly typed to the Album class</span></span>

![](mvc-music-store-part-5/_static/image2.png)

<span data-ttu-id="0331e-120">新的 StoreManager 控制器類別包含 CRUD （建立、讀取、更新、刪除）控制器動作，其可瞭解如何使用專輯模型類別，並使用我們的 Entity Framework 內容來存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="0331e-120">The new StoreManager controller class includes CRUD (create, read, update, delete) controller actions which know how to work with the Album model class and use our Entity Framework context for database access.</span></span>

## <a name="modifying-a-scaffolded-view"></a><span data-ttu-id="0331e-121">修改 Scaffold 視圖</span><span class="sxs-lookup"><span data-stu-id="0331e-121">Modifying a Scaffolded View</span></span>

<span data-ttu-id="0331e-122">請務必記住，雖然這段程式碼是為我們產生的，但它是標準的 ASP.NET MVC 程式碼，就像我們在本教學課程中所撰寫的一樣。</span><span class="sxs-lookup"><span data-stu-id="0331e-122">It's important to remember that, while this code was generated for us, it's standard ASP.NET MVC code, just like we've been writing throughout this tutorial.</span></span> <span data-ttu-id="0331e-123">它的目的是要讓您省下花在撰寫重複使用的控制器程式碼，以及手動建立強型別視圖的時間，但這不是您前面所見過的程式碼目錄，您可能會在不得變更錯誤碼.</span><span class="sxs-lookup"><span data-stu-id="0331e-123">It's intended to save you the time you'd spend on writing boilerplate controller code and creating the strongly typed views manually, but this isn't the kind of generated code you may have seen prefaced with dire warnings in comments about how you mustn't change the code.</span></span> <span data-ttu-id="0331e-124">這是您的程式碼，您應該要加以變更。</span><span class="sxs-lookup"><span data-stu-id="0331e-124">This is your code, and you're expected to change it.</span></span>

<span data-ttu-id="0331e-125">因此，讓我們從快速編輯 StoreManager 索引視圖（/Views/StoreManager/Index.cshtml）開始。</span><span class="sxs-lookup"><span data-stu-id="0331e-125">So, let's start with a quick edit to the StoreManager Index view (/Views/StoreManager/Index.cshtml).</span></span> <span data-ttu-id="0331e-126">此視圖會顯示一個表格，其中列出存放區中的專輯，其中包含編輯/詳細資料/刪除連結，並包含專輯的公用屬性。</span><span class="sxs-lookup"><span data-stu-id="0331e-126">This view will display a table which lists the Albums in our store with Edit / Details / Delete links, and includes the Album's public properties.</span></span> <span data-ttu-id="0331e-127">我們將移除 [AlbumArtUrl] 欄位，因為它在此顯示中並沒有太大説明。</span><span class="sxs-lookup"><span data-stu-id="0331e-127">We'll remove the AlbumArtUrl field, as it's not very useful in this display.</span></span> <span data-ttu-id="0331e-128">在 view 程式碼 &lt;table&gt; 區段中，移除 &lt;的&gt;，並 &lt;括住 AlbumArtUrl 參考的 td&gt; 元素，如下列反白顯示的幾行所示：</span><span class="sxs-lookup"><span data-stu-id="0331e-128">In &lt;table&gt; section of the view code, remove the &lt;th&gt; and &lt;td&gt; elements surrounding AlbumArtUrl references, as indicated by the highlighted lines below:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample1.cshtml)]

<span data-ttu-id="0331e-129">修改過的視圖程式碼將會如下所示：</span><span class="sxs-lookup"><span data-stu-id="0331e-129">The modified view code will appear as follows:</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample2.cshtml)]

## <a name="a-first-look-at-the-store-manager"></a><span data-ttu-id="0331e-130">第一次查看商店經理</span><span class="sxs-lookup"><span data-stu-id="0331e-130">A first look at the Store Manager</span></span>

<span data-ttu-id="0331e-131">現在執行應用程式，並流覽至/StoreManager/。</span><span class="sxs-lookup"><span data-stu-id="0331e-131">Now run the application and browse to /StoreManager/.</span></span> <span data-ttu-id="0331e-132">這會顯示剛才修改的存放區經理索引，並顯示商店中的專輯清單，其中包含編輯、詳細資料和刪除的連結。</span><span class="sxs-lookup"><span data-stu-id="0331e-132">This displays the Store Manager Index we just modified, showing a list of the albums in the store with links to Edit, Details, and Delete.</span></span>

![](mvc-music-store-part-5/_static/image3.png)

<span data-ttu-id="0331e-133">按一下 [編輯] 連結會顯示含有專輯欄位的編輯表單，包括內容類型和演出者的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="0331e-133">Clicking the Edit link displays an edit form with fields for the Album, including dropdowns for Genre and Artist.</span></span>

![](mvc-music-store-part-5/_static/image4.png)

<span data-ttu-id="0331e-134">按一下底部的 [返回清單] 連結，然後按一下專輯的 [詳細資料] 連結。</span><span class="sxs-lookup"><span data-stu-id="0331e-134">Click the "Back to List" link at the bottom, then click on the Details link for an Album.</span></span> <span data-ttu-id="0331e-135">這會顯示個別專輯的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="0331e-135">This displays the detail information for an individual Album.</span></span>

![](mvc-music-store-part-5/_static/image5.png)

<span data-ttu-id="0331e-136">再次按一下 [回到清單] 連結，然後按一下 [刪除] 連結。</span><span class="sxs-lookup"><span data-stu-id="0331e-136">Again, click the Back to List link, then click on a Delete link.</span></span> <span data-ttu-id="0331e-137">這會顯示確認對話方塊，其中會顯示專輯詳細資料，並詢問我們是否確定要將它刪除。</span><span class="sxs-lookup"><span data-stu-id="0331e-137">This displays a confirmation dialog, showing the album details and asking if we're sure we want to delete it.</span></span>

![](mvc-music-store-part-5/_static/image6.png)

<span data-ttu-id="0331e-138">按一下底部的 [刪除] 按鈕將會刪除專輯，並返回 [索引] 頁面，其中會顯示已刪除的專輯。</span><span class="sxs-lookup"><span data-stu-id="0331e-138">Clicking the Delete button at the bottom will delete the album and return you to the Index page, which shows the album deleted.</span></span>

<span data-ttu-id="0331e-139">我們不是使用 Store Manager 完成，但我們有工作控制器和程式碼可供 CRUD 作業開始。</span><span class="sxs-lookup"><span data-stu-id="0331e-139">We're not done with the Store Manager, but we have working controller and view code for the CRUD operations to start from.</span></span>

## <a name="looking-at-the-store-manager-controller-code"></a><span data-ttu-id="0331e-140">查看 Store Manager 控制器程式碼</span><span class="sxs-lookup"><span data-stu-id="0331e-140">Looking at the Store Manager Controller code</span></span>

<span data-ttu-id="0331e-141">存放區管理員控制器包含適當的程式碼數量。</span><span class="sxs-lookup"><span data-stu-id="0331e-141">The Store Manager Controller contains a good amount of code.</span></span> <span data-ttu-id="0331e-142">讓我們從上到下逐一查看。</span><span class="sxs-lookup"><span data-stu-id="0331e-142">Let's go through this from top to bottom.</span></span> <span data-ttu-id="0331e-143">控制器包含一些 MVC 控制器的標準命名空間，以及我們的模型命名空間的參考。</span><span class="sxs-lookup"><span data-stu-id="0331e-143">The controller includes some standard namespaces for an MVC controller, as well as a reference to our Models namespace.</span></span> <span data-ttu-id="0331e-144">控制器具有 MusicStoreEntities 的私用實例，用於每個控制器動作以進行資料存取。</span><span class="sxs-lookup"><span data-stu-id="0331e-144">The controller has a private instance of MusicStoreEntities, used by each of the controller actions for data access.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample3.cs)]

### <a name="store-manager-index-and-details-actions"></a><span data-ttu-id="0331e-145">存放管理員索引和詳細資料動作</span><span class="sxs-lookup"><span data-stu-id="0331e-145">Store Manager Index and Details actions</span></span>

<span data-ttu-id="0331e-146">[索引] 視圖會抓取專輯清單，包括每個專輯參考的內容類型和演出者資訊，如同我們在使用 Store Browse 方法時所看到的一樣。</span><span class="sxs-lookup"><span data-stu-id="0331e-146">The index view retrieves a list of Albums, including each album's referenced Genre and Artist information, as we previously saw when working on the Store Browse method.</span></span> <span data-ttu-id="0331e-147">索引視圖會遵循連結化物件的參考，讓它可以顯示每個專輯的內容類型名稱和演出者名稱，讓控制器有效率地在原始要求中查詢這項資訊。</span><span class="sxs-lookup"><span data-stu-id="0331e-147">The Index view is following the references to the linked objects so that it can display each album's Genre name and Artist name, so the controller is being efficient and querying for this information in the original request.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample4.cs)]

<span data-ttu-id="0331e-148">StoreManager 控制器的詳細資料控制器動作的運作方式與我們先前撰寫的 Store Controller Details 動作完全相同-它會使用 Find （）方法來依識別碼查詢專輯，然後將它傳回給視圖。</span><span class="sxs-lookup"><span data-stu-id="0331e-148">The StoreManager Controller's Details controller action works exactly the same as the Store Controller Details action we wrote previously - it queries for the Album by ID using the Find() method, then returns it to the view.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample5.cs)]

### <a name="the-create-action-methods"></a><span data-ttu-id="0331e-149">建立動作方法</span><span class="sxs-lookup"><span data-stu-id="0331e-149">The Create Action Methods</span></span>

<span data-ttu-id="0331e-150">建立動作方法與我們目前看到的不同，因為它們會處理表單輸入。</span><span class="sxs-lookup"><span data-stu-id="0331e-150">The Create action methods are a little different from ones we've seen so far, because they handle form input.</span></span> <span data-ttu-id="0331e-151">使用者第一次造訪/StoreManager/Create/時，將會顯示空白表單。</span><span class="sxs-lookup"><span data-stu-id="0331e-151">When a user first visits /StoreManager/Create/ they will be shown an empty form.</span></span> <span data-ttu-id="0331e-152">這個 HTML 網頁會包含一個 &lt;表單&gt; 元素，其中包含下拉式清單和 textbox input 元素，可在其中輸入專輯的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0331e-152">This HTML page will contain a &lt;form&gt; element that contains dropdown and textbox input elements where they can enter the album's details.</span></span>

<span data-ttu-id="0331e-153">使用者填滿專輯表單值後，可以按 [儲存] 按鈕，將這些變更提交回我們的應用程式，以儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="0331e-153">After the user fills in the Album form values, they can press the "Save" button to submit these changes back to our application to save within the database.</span></span> <span data-ttu-id="0331e-154">當使用者按下 [儲存] 按鈕時，&lt;表單&gt; 會對/StoreManager/Create/URL 執行 HTTP POST，並提交 &lt;表單&gt; 值做為 HTTP POST 的一部分。</span><span class="sxs-lookup"><span data-stu-id="0331e-154">When the user presses the "save" button the &lt;form&gt; will perform an HTTP-POST back to the /StoreManager/Create/ URL and submit the &lt;form&gt; values as part of the HTTP-POST.</span></span>

<span data-ttu-id="0331e-155">ASP.NET MVC 可讓我們輕鬆地分割這兩個 URL 調用案例的邏輯，方法是讓我們在我們的 StoreManagerController 類別內執行兩個不同的「建立」動作方法–一個用來處理初始 HTTP-GET 流覽至/StoreManager/Create/URL，另一個用來處理已提交變更的 HTTP POST。</span><span class="sxs-lookup"><span data-stu-id="0331e-155">ASP.NET MVC allows us to easily split up the logic of these two URL invocation scenarios by enabling us to implement two separate "Create" action methods within our StoreManagerController class – one to handle the initial HTTP-GET browse to the /StoreManager/Create/ URL, and the other to handle the HTTP-POST of the submitted changes.</span></span>

### <a name="passing-information-to-a-view-using-viewbag"></a><span data-ttu-id="0331e-156">使用 ViewBag 將資訊傳遞至視圖</span><span class="sxs-lookup"><span data-stu-id="0331e-156">Passing information to a View using ViewBag</span></span>

<span data-ttu-id="0331e-157">我們稍早在本教學課程中使用過此 ViewBag，但尚未討論過。</span><span class="sxs-lookup"><span data-stu-id="0331e-157">We've used the ViewBag earlier in this tutorial, but haven't talked much about it.</span></span> <span data-ttu-id="0331e-158">ViewBag 可讓我們在不使用強型別模型物件的情況下，將資訊傳遞給視圖。</span><span class="sxs-lookup"><span data-stu-id="0331e-158">The ViewBag allows us to pass information to the view without using a strongly typed model object.</span></span> <span data-ttu-id="0331e-159">在此情況下，我們的編輯 HTTP-取得控制器動作必須將內容類型和演出者清單傳遞至表單以填入下拉式清單，而最簡單的方法是將它們當做 ViewBag 專案傳回。</span><span class="sxs-lookup"><span data-stu-id="0331e-159">In this case, our Edit HTTP-GET controller action needs to pass both a list of Genres and Artists to the form to populate the dropdowns, and the simplest way to do that is to return them as ViewBag items.</span></span>

<span data-ttu-id="0331e-160">ViewBag 是動態物件，這表示您可以輸入 ViewBag 或 ViewBag，而不需要撰寫程式碼來定義這些屬性。</span><span class="sxs-lookup"><span data-stu-id="0331e-160">The ViewBag is a dynamic object, meaning that you can type ViewBag.Foo or ViewBag.YourNameHere without writing code to define those properties.</span></span> <span data-ttu-id="0331e-161">在此情況下，控制器程式碼會使用 ViewBag. GenreId 和 ViewBag ArtistId，讓以表單提交的下拉式值將會是 GenreId 和 ArtistId，也就是他們將設定的專輯屬性。</span><span class="sxs-lookup"><span data-stu-id="0331e-161">In this case, the controller code uses ViewBag.GenreId and ViewBag.ArtistId so that the dropdown values submitted with the form will be GenreId and ArtistId, which are the Album properties they will be setting.</span></span>

<span data-ttu-id="0331e-162">這些下拉式值會使用 SelectList 物件（專為該目的而建立）傳回給表單。</span><span class="sxs-lookup"><span data-stu-id="0331e-162">These dropdown values are returned to the form using the SelectList object, which is built just for that purpose.</span></span> <span data-ttu-id="0331e-163">這會使用類似如下的程式碼來完成：</span><span class="sxs-lookup"><span data-stu-id="0331e-163">This is done using code like this:</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample6.cs)]

<span data-ttu-id="0331e-164">如您在動作方法程式碼中所見，有三個參數是用來建立這個物件：</span><span class="sxs-lookup"><span data-stu-id="0331e-164">As you can see from the action method code, three parameters are being used to create this object:</span></span>

- <span data-ttu-id="0331e-165">下拉式清單將顯示的專案清單。</span><span class="sxs-lookup"><span data-stu-id="0331e-165">The list of items the dropdown will be displaying.</span></span> <span data-ttu-id="0331e-166">請注意，這不只是字串，而是要傳遞內容清單。</span><span class="sxs-lookup"><span data-stu-id="0331e-166">Note that this isn't just a string - we're passing a list of Genres.</span></span>
- <span data-ttu-id="0331e-167">要傳遞至 SelectList 的下一個參數是選取的值。</span><span class="sxs-lookup"><span data-stu-id="0331e-167">The next parameter being passed to the SelectList is the Selected Value.</span></span> <span data-ttu-id="0331e-168">SelectList 如何知道如何預先選取清單中的專案。</span><span class="sxs-lookup"><span data-stu-id="0331e-168">This how the SelectList knows how to pre-select an item in the list.</span></span> <span data-ttu-id="0331e-169">當我們查看 [編輯] 表單時，這會比較容易瞭解，這非常類似。</span><span class="sxs-lookup"><span data-stu-id="0331e-169">This will be easier to understand when we look at the Edit form, which is pretty similar.</span></span>
- <span data-ttu-id="0331e-170">最後一個參數是要顯示的屬性。</span><span class="sxs-lookup"><span data-stu-id="0331e-170">The final parameter is the property to be displayed.</span></span> <span data-ttu-id="0331e-171">在此情況下，這表示 Genre.Name 屬性就是將向使用者顯示的內容。</span><span class="sxs-lookup"><span data-stu-id="0331e-171">In this case, this is indicating that the Genre.Name property is what will be shown to the user.</span></span>

<span data-ttu-id="0331e-172">記住這一點之後，HTTP GET Create 動作非常簡單-這兩個 SelectLists 會加入至 ViewBag，而且不會有任何模型物件傳遞至表單（因為尚未建立）。</span><span class="sxs-lookup"><span data-stu-id="0331e-172">With that in mind, then, the HTTP-GET Create action is pretty simple - two SelectLists are added to the ViewBag, and no model object is passed to the form (since it hasn't been created yet).</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample7.cs)]

### <a name="html-helpers-to-display-the-drop-downs-in-the-create-view"></a><span data-ttu-id="0331e-173">HTML 協助程式，以顯示 [建立] 視圖中的下拉式清單</span><span class="sxs-lookup"><span data-stu-id="0331e-173">HTML Helpers to display the Drop Downs in the Create View</span></span>

<span data-ttu-id="0331e-174">既然我們已經討論過如何將下拉式值傳遞至視圖，讓我們快速查看一下視圖，以查看這些值的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="0331e-174">Since we've talked about how the drop down values are passed to the view, let's take a quick look at the view to see how those values are displayed.</span></span> <span data-ttu-id="0331e-175">在 view code （/Views/StoreManager/Create.cshtml）中，您會看到下列呼叫來顯示 [內容類型] 下拉式按鈕。</span><span class="sxs-lookup"><span data-stu-id="0331e-175">In the view code (/Views/StoreManager/Create.cshtml), you'll see the following call is made to display the Genre drop down.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample8.cshtml)]

<span data-ttu-id="0331e-176">這就是所謂的 HTML Helper，這是一個可執行一般 view 工作的公用程式方法。</span><span class="sxs-lookup"><span data-stu-id="0331e-176">This is known as an HTML Helper - a utility method which performs a common view task.</span></span> <span data-ttu-id="0331e-177">HTML helper 非常適合讓我們的視圖程式碼變得簡潔易懂。</span><span class="sxs-lookup"><span data-stu-id="0331e-177">HTML Helpers are very useful in keeping our view code concise and readable.</span></span> <span data-ttu-id="0331e-178">DropDownList helper 是由 ASP.NET MVC 提供，但我們稍後會看到，我們可以建立自己的協助程式，以在我們的應用程式中重複使用。</span><span class="sxs-lookup"><span data-stu-id="0331e-178">The Html.DropDownList helper is provided by ASP.NET MVC, but as we'll see later it's possible to create our own helpers for view code we'll reuse in our application.</span></span>

<span data-ttu-id="0331e-179">DropDownList 呼叫只需要告訴兩件事，就可以在何處取得要顯示的清單，以及應該預先選取的值（如果有的話）。</span><span class="sxs-lookup"><span data-stu-id="0331e-179">The Html.DropDownList call just needs to be told two things - where to get the list to display, and what value (if any) should be pre-selected.</span></span> <span data-ttu-id="0331e-180">第一個參數 GenreId 會告知 DropDownList 在模型或 ViewBag 中尋找名為 GenreId 的值。</span><span class="sxs-lookup"><span data-stu-id="0331e-180">The first parameter, GenreId, tells the DropDownList to look for a value named GenreId in either the model or ViewBag.</span></span> <span data-ttu-id="0331e-181">第二個參數是用來指出要顯示為下拉式清單中一開始所選取的值。</span><span class="sxs-lookup"><span data-stu-id="0331e-181">The second parameter is used to indicate the value to show as initially selected in the drop down list.</span></span> <span data-ttu-id="0331e-182">因為此表單是建立表單，所以沒有預先選取的值和 String。會傳遞空的。</span><span class="sxs-lookup"><span data-stu-id="0331e-182">Since this form is a Create form, there's no value to be preselected and String.Empty is passed.</span></span>

### <a name="handling-the-posted-form-values"></a><span data-ttu-id="0331e-183">處理已張貼的表單值</span><span class="sxs-lookup"><span data-stu-id="0331e-183">Handling the Posted Form values</span></span>

<span data-ttu-id="0331e-184">如先前所討論，每個表單有兩個相關聯的動作方法。</span><span class="sxs-lookup"><span data-stu-id="0331e-184">As we discussed before, there are two action methods associated with each form.</span></span> <span data-ttu-id="0331e-185">第一個會處理 HTTP GET 要求，並顯示表單。</span><span class="sxs-lookup"><span data-stu-id="0331e-185">The first handles the HTTP-GET request and displays the form.</span></span> <span data-ttu-id="0331e-186">第二個處理 HTTP POST 要求，其中包含已提交的表單值。</span><span class="sxs-lookup"><span data-stu-id="0331e-186">The second handles the HTTP-POST request, which contains the submitted form values.</span></span> <span data-ttu-id="0331e-187">請注意，控制器動作有一個 [HttpPost] 屬性，它會告知 ASP.NET MVC 它應該只回應 HTTP POST 要求。</span><span class="sxs-lookup"><span data-stu-id="0331e-187">Notice that controller action has an [HttpPost] attribute, which tells ASP.NET MVC that it should only respond to HTTP-POST requests.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample9.cs)]

<span data-ttu-id="0331e-188">此動作有四個責任：</span><span class="sxs-lookup"><span data-stu-id="0331e-188">This action has four responsibilities:</span></span>

- 1. <span data-ttu-id="0331e-189">讀取表單值</span><span class="sxs-lookup"><span data-stu-id="0331e-189">Read the form values</span></span>
- 2. <span data-ttu-id="0331e-190">檢查表單值是否通過任何驗證規則</span><span class="sxs-lookup"><span data-stu-id="0331e-190">Check if the form values pass any validation rules</span></span>
- 3. <span data-ttu-id="0331e-191">如果表單提交有效，請儲存資料並顯示更新的清單</span><span class="sxs-lookup"><span data-stu-id="0331e-191">If the form submission is valid, save the data and display the updated list</span></span>
- 4. <span data-ttu-id="0331e-192">如果表單提交無效，請重新顯示含有驗證錯誤的表單</span><span class="sxs-lookup"><span data-stu-id="0331e-192">If the form submission is not valid, redisplay the form with validation errors</span></span>

#### <a name="reading-form-values-with-model-binding"></a><span data-ttu-id="0331e-193">使用模型系結讀取表單值</span><span class="sxs-lookup"><span data-stu-id="0331e-193">Reading Form Values with Model Binding</span></span>

<span data-ttu-id="0331e-194">控制器動作會處理表單提交，其中包含 GenreId 和 ArtistId （從下拉式清單）的值，以及 Title、Price 和 AlbumArtUrl 的 textbox 值。</span><span class="sxs-lookup"><span data-stu-id="0331e-194">The controller action is processing a form submission that includes values for GenreId and ArtistId (from the drop down list) and textbox values for Title, Price, and AlbumArtUrl.</span></span> <span data-ttu-id="0331e-195">雖然可以直接存取表單值，但更好的方法是使用內建于 ASP.NET MVC 中的模型系結功能。</span><span class="sxs-lookup"><span data-stu-id="0331e-195">While it's possible to directly access form values, a better approach is to use the Model Binding capabilities built into ASP.NET MVC.</span></span> <span data-ttu-id="0331e-196">當控制器動作接受模型類型做為參數時，ASP.NET MVC 會使用表單輸入（以及路由和 querystring 值）嘗試填入該類型的物件。</span><span class="sxs-lookup"><span data-stu-id="0331e-196">When a controller action takes a model type as a parameter, ASP.NET MVC will attempt to populate an object of that type using form inputs (as well as route and querystring values).</span></span> <span data-ttu-id="0331e-197">其執行方式是尋找名稱符合模型物件屬性的值，例如，設定新專輯物件的 GenreId 值時，它會尋找名稱為 GenreId 的輸入。</span><span class="sxs-lookup"><span data-stu-id="0331e-197">It does this by looking for values whose names match properties of the model object, e.g. when setting the new Album object's GenreId value, it looks for an input with the name GenreId.</span></span> <span data-ttu-id="0331e-198">當您使用 ASP.NET MVC 中的標準方法來建立視圖時，表單一律會使用屬性名稱做為輸入功能變數名稱來呈現，因此此功能變數名稱將會完全相符。</span><span class="sxs-lookup"><span data-stu-id="0331e-198">When you create views using the standard methods in ASP.NET MVC, the forms will always be rendered using property names as input field names, so this the field names will just match up.</span></span>

#### <a name="validating-the-model"></a><span data-ttu-id="0331e-199">驗證模型</span><span class="sxs-lookup"><span data-stu-id="0331e-199">Validating the Model</span></span>

<span data-ttu-id="0331e-200">此模型會使用 ModelState 的簡單呼叫來進行驗證。</span><span class="sxs-lookup"><span data-stu-id="0331e-200">The model is validated with a simple call to ModelState.IsValid.</span></span> <span data-ttu-id="0331e-201">我們尚未將任何驗證規則新增至我們的專輯類別-我們將在稍後執行此動作，但現在這項檢查並不會有太多的功能。</span><span class="sxs-lookup"><span data-stu-id="0331e-201">We haven't added any validation rules to our Album class yet - we'll do that in a bit - so right now this check doesn't have much to do.</span></span> <span data-ttu-id="0331e-202">重要的是，此 ModelStat 檢查會根據我們放在模型上的驗證規則來調整，因此未來對驗證規則所做的變更不需要對控制器動作程式碼進行任何更新。</span><span class="sxs-lookup"><span data-stu-id="0331e-202">What's important is that this ModelStat.IsValid check will adapt to the validation rules we put on our model, so future changes to validation rules won't require any updates to the controller action code.</span></span>

#### <a name="saving-the-submitted-values"></a><span data-ttu-id="0331e-203">儲存已提交的值</span><span class="sxs-lookup"><span data-stu-id="0331e-203">Saving the submitted values</span></span>

<span data-ttu-id="0331e-204">如果表單提交通過驗證，就可以將值儲存至資料庫。</span><span class="sxs-lookup"><span data-stu-id="0331e-204">If the form submission passes validation, it's time to save the values to the database.</span></span> <span data-ttu-id="0331e-205">使用 Entity Framework，只需要將模型加入專輯集合，然後呼叫 SaveChanges。</span><span class="sxs-lookup"><span data-stu-id="0331e-205">With Entity Framework, that just requires adding the model to the Albums collection and calling SaveChanges.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample10.cs)]

<span data-ttu-id="0331e-206">Entity Framework 會產生適當的 SQL 命令來保存值。</span><span class="sxs-lookup"><span data-stu-id="0331e-206">Entity Framework generates the appropriate SQL commands to persist the value.</span></span> <span data-ttu-id="0331e-207">儲存資料之後，我們會重新導向回到專輯清單，讓我們可以看到我們的更新。</span><span class="sxs-lookup"><span data-stu-id="0331e-207">After saving the data, we redirect back to the list of Albums so we can see our update.</span></span> <span data-ttu-id="0331e-208">這是藉由傳回 RedirectToAction，並以我們想要顯示的控制器動作名稱來完成。</span><span class="sxs-lookup"><span data-stu-id="0331e-208">This is done by returning RedirectToAction with the name of the controller action we want displayed.</span></span> <span data-ttu-id="0331e-209">在此情況下，這是索引方法。</span><span class="sxs-lookup"><span data-stu-id="0331e-209">In this case, that's the Index method.</span></span>

#### <a name="displaying-invalid-form-submissions-with-validation-errors"></a><span data-ttu-id="0331e-210">顯示驗證錯誤的無效表單提交</span><span class="sxs-lookup"><span data-stu-id="0331e-210">Displaying invalid form submissions with Validation Errors</span></span>

<span data-ttu-id="0331e-211">在不正確表單輸入案例中，下拉式清單值會加入至 ViewBag （如同在 HTTP GET 案例中），而系結的模型值則會傳回給 view 以供顯示。</span><span class="sxs-lookup"><span data-stu-id="0331e-211">In the case of invalid form input, the dropdown values are added to the ViewBag (as in the HTTP-GET case) and the bound model values are passed back to the view for display.</span></span> <span data-ttu-id="0331e-212">驗證錯誤會使用 @Html.ValidationMessageFor HTML Helper 自動顯示。</span><span class="sxs-lookup"><span data-stu-id="0331e-212">Validation errors are automatically displayed using the @Html.ValidationMessageFor HTML Helper.</span></span>

#### <a name="testing-the-create-form"></a><span data-ttu-id="0331e-213">測試建立表單</span><span class="sxs-lookup"><span data-stu-id="0331e-213">Testing the Create Form</span></span>

<span data-ttu-id="0331e-214">若要測試這項作業，請執行應用程式並流覽至/StoreManager/Create/-這會顯示 StoreController Create HTTP GET 方法所傳回的空白表單。</span><span class="sxs-lookup"><span data-stu-id="0331e-214">To test this out, run the application and browse to /StoreManager/Create/ - this will show you the blank form which was returned by the StoreController Create HTTP-GET method.</span></span>

<span data-ttu-id="0331e-215">填入一些值，然後按一下 [建立] 按鈕以提交表單。</span><span class="sxs-lookup"><span data-stu-id="0331e-215">Fill in some values and click the Create button to submit the form.</span></span>

![](mvc-music-store-part-5/_static/image7.png)

![](mvc-music-store-part-5/_static/image8.png)

### <a name="handling-edits"></a><span data-ttu-id="0331e-216">處理編輯</span><span class="sxs-lookup"><span data-stu-id="0331e-216">Handling Edits</span></span>

<span data-ttu-id="0331e-217">[編輯動作組] （HTTP-GET 和 HTTP POST）與我們剛才查看的建立動作方法非常類似。</span><span class="sxs-lookup"><span data-stu-id="0331e-217">The Edit action pair (HTTP-GET and HTTP-POST) are very similar to the Create action methods we just looked at.</span></span> <span data-ttu-id="0331e-218">因為編輯案例牽涉到使用現有的專輯，所以 Edit HTTP GET 方法會根據「識別碼」參數載入專輯，並透過路由傳入。</span><span class="sxs-lookup"><span data-stu-id="0331e-218">Since the edit scenario involves working with an existing album, the Edit HTTP-GET method loads the Album based on the "id" parameter, passed in via the route.</span></span> <span data-ttu-id="0331e-219">這段程式碼可供 AlbumId 用來抓取專輯，如同我們先前在詳細資料控制器動作中所探討的一樣。</span><span class="sxs-lookup"><span data-stu-id="0331e-219">This code for retrieving an album by AlbumId is the same as we've previously looked at in the Details controller action.</span></span> <span data-ttu-id="0331e-220">如同 Create/HTTP-GET 方法，下拉式值會透過 ViewBag 傳回。</span><span class="sxs-lookup"><span data-stu-id="0331e-220">As with the Create / HTTP-GET method, the drop down values are returned via the ViewBag.</span></span> <span data-ttu-id="0331e-221">這可讓我們將專輯當做我們的模型物件傳回給視圖（這是對專輯類別的強型別），同時透過 ViewBag 傳遞其他資料（例如內容類型的清單）。</span><span class="sxs-lookup"><span data-stu-id="0331e-221">This allows us to return an Album as our model object to the view (which is strongly typed to the Album class) while passing additional data (e.g. a list of Genres) via the ViewBag.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample11.cs)]

<span data-ttu-id="0331e-222">編輯 HTTP POST 動作與建立 HTTP POST 動作非常類似。</span><span class="sxs-lookup"><span data-stu-id="0331e-222">The Edit HTTP-POST action is very similar to the Create HTTP-POST action.</span></span> <span data-ttu-id="0331e-223">唯一的差別在於，它不會將新的專輯新增至資料庫。專輯集合，我們正在使用 db 尋找專輯的目前實例。專案（專輯），並將其狀態設定為 [已修改]。</span><span class="sxs-lookup"><span data-stu-id="0331e-223">The only difference is that instead of adding a new album to the db.Albums collection, we're finding the current instance of the Album using db.Entry(album) and setting its state to Modified.</span></span> <span data-ttu-id="0331e-224">這會告訴 Entity Framework 我們修改現有的專輯，而不是建立新的專輯。</span><span class="sxs-lookup"><span data-stu-id="0331e-224">This tells Entity Framework that we are modifying an existing album as opposed to creating a new one.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample12.cs)]

<span data-ttu-id="0331e-225">我們可以藉由執行應用程式並流覽至/StoreManger/，然後按一下專輯的 [編輯] 連結，來進行測試。</span><span class="sxs-lookup"><span data-stu-id="0331e-225">We can test this out by running the application and browsing to /StoreManger/, then clicking the Edit link for an album.</span></span>

![](mvc-music-store-part-5/_static/image9.png)

<span data-ttu-id="0331e-226">這會顯示編輯 HTTP GET 方法所顯示的編輯表單。</span><span class="sxs-lookup"><span data-stu-id="0331e-226">This displays the Edit form shown by the Edit HTTP-GET method.</span></span> <span data-ttu-id="0331e-227">填入一些值，然後按一下 [儲存] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="0331e-227">Fill in some values and click the Save button.</span></span>

![](mvc-music-store-part-5/_static/image10.png)

<span data-ttu-id="0331e-228">這會張貼表單、儲存值，並將我們傳給專輯清單，顯示值已更新。</span><span class="sxs-lookup"><span data-stu-id="0331e-228">This posts the form, saves the values, and returns us to the Album list, showing that the values were updated.</span></span>

![](mvc-music-store-part-5/_static/image11.png)

### <a name="handling-deletion"></a><span data-ttu-id="0331e-229">處理刪除</span><span class="sxs-lookup"><span data-stu-id="0331e-229">Handling Deletion</span></span>

<span data-ttu-id="0331e-230">刪除作業會遵循與 [編輯] 和 [建立] 相同的模式，使用一個控制器動作來顯示確認表單，以及另一個控制器動作來處理表單提交。</span><span class="sxs-lookup"><span data-stu-id="0331e-230">Deletion follows the same pattern as Edit and Create, using one controller action to display the confirmation form, and another controller action to handle the form submission.</span></span>

<span data-ttu-id="0331e-231">「HTTP-取得刪除控制器」動作與先前的「存放區管理員詳細資料控制器」動作完全相同。</span><span class="sxs-lookup"><span data-stu-id="0331e-231">The HTTP-GET Delete controller action is exactly the same as our previous Store Manager Details controller action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample13.cs)]

<span data-ttu-id="0331e-232">我們使用 [刪除視圖內容] 範本，顯示強型別為專輯類型的表單。</span><span class="sxs-lookup"><span data-stu-id="0331e-232">We display a form that's strongly typed to an Album type, using the Delete view content template.</span></span>

![](mvc-music-store-part-5/_static/image12.png)

<span data-ttu-id="0331e-233">[刪除] 範本會顯示模型的所有欄位，但我們可以稍微簡化。</span><span class="sxs-lookup"><span data-stu-id="0331e-233">The Delete template shows all the fields for the model, but we can simplify that down quite a bit.</span></span> <span data-ttu-id="0331e-234">將/Views/StoreManager/Delete.cshtml 中的 view 程式碼變更為下列。</span><span class="sxs-lookup"><span data-stu-id="0331e-234">Change the view code in /Views/StoreManager/Delete.cshtml to the following.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample14.cshtml)]

<span data-ttu-id="0331e-235">這會顯示簡化的刪除確認。</span><span class="sxs-lookup"><span data-stu-id="0331e-235">This displays a simplified Delete confirmation.</span></span>

![](mvc-music-store-part-5/_static/image13.png)

<span data-ttu-id="0331e-236">按一下 [刪除] 按鈕會導致表單回傳至伺服器，這會執行 DeleteConfirmed 動作。</span><span class="sxs-lookup"><span data-stu-id="0331e-236">Clicking the Delete button causes the form to be posted back to the server, which executes the DeleteConfirmed action.</span></span>

[!code-csharp[Main](mvc-music-store-part-5/samples/sample15.cs)]

<span data-ttu-id="0331e-237">我們的 HTTP POST 刪除控制器動作會採取下列動作：</span><span class="sxs-lookup"><span data-stu-id="0331e-237">Our HTTP-POST Delete Controller Action takes the following actions:</span></span>

- 1. <span data-ttu-id="0331e-238">依識別碼載入專輯</span><span class="sxs-lookup"><span data-stu-id="0331e-238">Loads the Album by ID</span></span>
- 2. <span data-ttu-id="0331e-239">刪除專輯並儲存變更</span><span class="sxs-lookup"><span data-stu-id="0331e-239">Deletes it the album and save changes</span></span>
- 3. <span data-ttu-id="0331e-240">重新導向至索引，顯示已從清單中移除專輯</span><span class="sxs-lookup"><span data-stu-id="0331e-240">Redirects to the Index, showing that the Album was removed from the list</span></span>

<span data-ttu-id="0331e-241">若要進行測試，請執行應用程式，並流覽至/StoreManager。</span><span class="sxs-lookup"><span data-stu-id="0331e-241">To test this, run the application and browse to /StoreManager.</span></span> <span data-ttu-id="0331e-242">從清單中選取專輯，然後按一下 [刪除] 連結。</span><span class="sxs-lookup"><span data-stu-id="0331e-242">Select an album from the list and click the Delete link.</span></span>

![](mvc-music-store-part-5/_static/image14.png)

<span data-ttu-id="0331e-243">這會顯示我們的刪除確認畫面。</span><span class="sxs-lookup"><span data-stu-id="0331e-243">This displays our Delete confirmation screen.</span></span>

![](mvc-music-store-part-5/_static/image15.png)

<span data-ttu-id="0331e-244">按一下 [刪除] 按鈕會移除專輯，並將我們返回 [Store Manager 索引] 頁面，其中顯示已刪除專輯。</span><span class="sxs-lookup"><span data-stu-id="0331e-244">Clicking the Delete button removes the album and returns us to the Store Manager Index page, which shows that the album has been deleted.</span></span>

![](mvc-music-store-part-5/_static/image16.png)

### <a name="using-a-custom-html-helper-to-truncate-text"></a><span data-ttu-id="0331e-245">使用自訂 HTML Helper 來截斷文字</span><span class="sxs-lookup"><span data-stu-id="0331e-245">Using a custom HTML Helper to truncate text</span></span>

<span data-ttu-id="0331e-246">我們的商店經理的 [索引] 頁面有一個可能的問題。</span><span class="sxs-lookup"><span data-stu-id="0331e-246">We've got one potential issue with our Store Manager Index page.</span></span> <span data-ttu-id="0331e-247">我們的專輯 [標題] 和 [演出者名稱] 屬性可以夠長，而可能會擲出我們的資料表格式。</span><span class="sxs-lookup"><span data-stu-id="0331e-247">Our Album Title and Artist Name properties can both be long enough that they could throw off our table formatting.</span></span> <span data-ttu-id="0331e-248">我們將建立自訂的 HTML 協助程式，讓我們能夠輕鬆地截斷我們的視圖中的這些和其他屬性。</span><span class="sxs-lookup"><span data-stu-id="0331e-248">We'll create a custom HTML Helper to allow us to easily truncate these and other properties in our Views.</span></span>

![](mvc-music-store-part-5/_static/image17.png)

<span data-ttu-id="0331e-249">Razor 的 @helper 語法讓您建立自己的 helper 函式，以便在您的視圖中使用是相當容易的。</span><span class="sxs-lookup"><span data-stu-id="0331e-249">Razor's @helper syntax has made it pretty easy to create your own helper functions for use in your views.</span></span> <span data-ttu-id="0331e-250">開啟 [/Views/StoreManager/Index.cshtml] 視圖，並將下列程式碼直接加在 @model 行之後。</span><span class="sxs-lookup"><span data-stu-id="0331e-250">Open the /Views/StoreManager/Index.cshtml view and add the following code directly after the @model line.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample16.cshtml)]

<span data-ttu-id="0331e-251">此 helper 方法會接受字串和最大長度以允許。</span><span class="sxs-lookup"><span data-stu-id="0331e-251">This helper method takes a string and a maximum length to allow.</span></span> <span data-ttu-id="0331e-252">如果提供的文字比指定的長度短，協助專家就會依自己的方式輸出它。</span><span class="sxs-lookup"><span data-stu-id="0331e-252">If the text supplied is shorter than the length specified, the helper outputs it as-is.</span></span> <span data-ttu-id="0331e-253">如果較長，則會截斷文字並呈現 "..."餘數。</span><span class="sxs-lookup"><span data-stu-id="0331e-253">If it is longer, then it truncates the text and renders "…" for the remainder.</span></span>

<span data-ttu-id="0331e-254">現在我們可以使用截斷協助程式，確保專輯標題和演出者名稱屬性都少於25個字元。</span><span class="sxs-lookup"><span data-stu-id="0331e-254">Now we can use our Truncate helper to ensure that both the Album Title and Artist Name properties are less than 25 characters.</span></span> <span data-ttu-id="0331e-255">使用新的截斷協助程式的完整 view 程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="0331e-255">The complete view code using our new Truncate helper appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-5/samples/sample17.cshtml)]

<span data-ttu-id="0331e-256">現在當我們流覽/StoreManager/URL 時，專輯和標題會保留在我們的最大長度之下。</span><span class="sxs-lookup"><span data-stu-id="0331e-256">Now when we browse the /StoreManager/ URL, the albums and titles are kept below our maximum lengths.</span></span>

![](mvc-music-store-part-5/_static/image18.png)

<span data-ttu-id="0331e-257">注意：這會顯示在單一視圖中建立和使用 helper 的簡單案例。</span><span class="sxs-lookup"><span data-stu-id="0331e-257">Note: This shows the simple case of creating and using a helper in one view.</span></span> <span data-ttu-id="0331e-258">若要深入瞭解如何建立可在整個網站中使用的協助程式，請參閱我的 blog 文章： [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span><span class="sxs-lookup"><span data-stu-id="0331e-258">To learn more about creating helpers that you can use throughout your site, see my blog post: [http://bit.ly/mvc3-helper-options](http://bit.ly/mvc3-helper-options)</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0331e-259">[上一頁](mvc-music-store-part-4.md)
> [下一頁](mvc-music-store-part-6.md)</span><span class="sxs-lookup"><span data-stu-id="0331e-259">[Previous](mvc-music-store-part-4.md)
[Next](mvc-music-store-part-6.md)</span></span>
