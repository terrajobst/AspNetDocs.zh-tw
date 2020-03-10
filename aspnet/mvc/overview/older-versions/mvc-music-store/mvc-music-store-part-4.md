---
uid: mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
title: 第4部分：模型和資料存取 |Microsoft Docs
author: jongalloway
description: 本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。 第4部分涵蓋模型和資料存取。
ms.author: riande
ms.date: 04/21/2011
ms.assetid: ab55ca81-ab9b-44a0-8700-dc6da2599335
msc.legacyurl: /mvc/overview/older-versions/mvc-music-store/mvc-music-store-part-4
msc.type: authoredcontent
ms.openlocfilehash: 402be340f1ea3344675e7b859cea8c5130cfc8ee
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78559672"
---
# <a name="part-4-models-and-data-access"></a><span data-ttu-id="0962d-104">第4部分：模型和資料存取</span><span class="sxs-lookup"><span data-stu-id="0962d-104">Part 4: Models and Data Access</span></span>

<span data-ttu-id="0962d-105">依[Jon Galloway](https://github.com/jongalloway)</span><span class="sxs-lookup"><span data-stu-id="0962d-105">by [Jon Galloway](https://github.com/jongalloway)</span></span>

> <span data-ttu-id="0962d-106">MVC 音樂存放區是教學課程應用程式，其仲介紹如何使用 ASP.NET MVC 和 Visual Studio 進行 web 程式開發的逐步解說。</span><span class="sxs-lookup"><span data-stu-id="0962d-106">The MVC Music Store is a tutorial application that introduces and explains step-by-step how to use ASP.NET MVC and Visual Studio for web development.</span></span>  
>   
> <span data-ttu-id="0962d-107">MVC 音樂存放區是輕量的範例商店執行，可在線上銷售音樂專輯，並實行基本的網站管理、使用者登入和購物車功能。</span><span class="sxs-lookup"><span data-stu-id="0962d-107">The MVC Music Store is a lightweight sample store implementation which sells music albums online, and implements basic site administration, user sign-in, and shopping cart functionality.</span></span>
> 
> <span data-ttu-id="0962d-108">本教學課程系列詳細說明建立 ASP.NET MVC 音樂存放區範例應用程式所採取的所有步驟。</span><span class="sxs-lookup"><span data-stu-id="0962d-108">This tutorial series details all of the steps taken to build the ASP.NET MVC Music Store sample application.</span></span> <span data-ttu-id="0962d-109">第4部分涵蓋模型和資料存取。</span><span class="sxs-lookup"><span data-stu-id="0962d-109">Part 4 covers Models and Data Access.</span></span>

<span data-ttu-id="0962d-110">到目前為止，我們只是從我們的控制器將「虛擬資料」傳遞給我們的「視圖」範本。</span><span class="sxs-lookup"><span data-stu-id="0962d-110">So far, we've just been passing "dummy data" from our Controllers to our View templates.</span></span> <span data-ttu-id="0962d-111">現在我們已經準備好連接實際的資料庫了。</span><span class="sxs-lookup"><span data-stu-id="0962d-111">Now we're ready to hook up a real database.</span></span> <span data-ttu-id="0962d-112">在本教學課程中，我們將討論如何使用 SQL Server Compact Edition （通常稱為 SQL CE）做為資料庫引擎。</span><span class="sxs-lookup"><span data-stu-id="0962d-112">In this tutorial we'll be covering how to use SQL Server Compact Edition (often called SQL CE) as our database engine.</span></span> <span data-ttu-id="0962d-113">SQL CE 是一種免費的內嵌檔案型資料庫，不需要任何安裝或設定，這讓您在本機開發上十分方便。</span><span class="sxs-lookup"><span data-stu-id="0962d-113">SQL CE is a free, embedded, file based database that doesn't require any installation or configuration, which makes it really convenient for local development.</span></span>

## <a name="database-access-with-entity-framework-code-first"></a><span data-ttu-id="0962d-114">Entity Framework 程式碼的資料庫存取權優先</span><span class="sxs-lookup"><span data-stu-id="0962d-114">Database access with Entity Framework Code-First</span></span>

<span data-ttu-id="0962d-115">我們將使用 ASP.NET MVC 3 專案中所包含的 Entity Framework （EF）支援來查詢和更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="0962d-115">We'll use the Entity Framework (EF) support that is included in ASP.NET MVC 3 projects to query and update the database.</span></span> <span data-ttu-id="0962d-116">EF 是彈性的物件關聯式對應（ORM）資料 API，可讓開發人員以物件導向的方式查詢和更新儲存在資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="0962d-116">EF is a flexible object relational mapping (ORM) data API that enables developers to query and update data stored in a database in an object-oriented way.</span></span>

<span data-ttu-id="0962d-117">Entity Framework 第4版支援稱為「程式碼優先」的開發範例。</span><span class="sxs-lookup"><span data-stu-id="0962d-117">Entity Framework version 4 supports a development paradigm called code-first.</span></span> <span data-ttu-id="0962d-118">Code first 可讓您藉由撰寫簡單的類別（也稱為來自「單純的」 CLR 物件的 POCO）來建立模型物件，甚至可以從類別即時建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="0962d-118">Code-first allows you to create model object by writing simple classes (also known as POCO from "plain-old" CLR objects), and can even create the database on the fly from your classes.</span></span>

### <a name="changes-to-our-model-classes"></a><span data-ttu-id="0962d-119">模型類別的變更</span><span class="sxs-lookup"><span data-stu-id="0962d-119">Changes to our Model Classes</span></span>

<span data-ttu-id="0962d-120">在本教學課程中，我們將利用 Entity Framework 中的資料庫建立功能。</span><span class="sxs-lookup"><span data-stu-id="0962d-120">We will be leveraging the database creation feature in Entity Framework in this tutorial.</span></span> <span data-ttu-id="0962d-121">不過在這麼做之前，讓我們先對模型類別進行一些次要變更，以加入稍後將使用的一些專案。</span><span class="sxs-lookup"><span data-stu-id="0962d-121">Before we do that, though, let's make a few minor changes to our model classes to add in some things we'll be using later on.</span></span>

#### <a name="adding-the-artist-model-classes"></a><span data-ttu-id="0962d-122">加入演出者模型類別</span><span class="sxs-lookup"><span data-stu-id="0962d-122">Adding the Artist Model Classes</span></span>

<span data-ttu-id="0962d-123">我們的專輯會與演出者相關聯，因此我們會新增一個簡單的模型類別來描述演出者。</span><span class="sxs-lookup"><span data-stu-id="0962d-123">Our Albums will be associated with Artists, so we'll add a simple model class to describe an Artist.</span></span> <span data-ttu-id="0962d-124">使用如下所示的程式碼，將新類別新增至名為 Artist.cs 的 [模型] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="0962d-124">Add a new class to the Models folder named Artist.cs using the code shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample1.cs)]

#### <a name="updating-our-model-classes"></a><span data-ttu-id="0962d-125">更新我們的模型類別</span><span class="sxs-lookup"><span data-stu-id="0962d-125">Updating our Model Classes</span></span>

<span data-ttu-id="0962d-126">更新專輯類別，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0962d-126">Update the Album class as shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample2.cs)]

<span data-ttu-id="0962d-127">接下來，對內容類型類別進行下列更新。</span><span class="sxs-lookup"><span data-stu-id="0962d-127">Next, make the following updates to the Genre class.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample3.cs)]

### <a name="adding-the-app_data-folder"></a><span data-ttu-id="0962d-128">將應用程式新增\_Data 資料夾</span><span class="sxs-lookup"><span data-stu-id="0962d-128">Adding the App\_Data folder</span></span>

<span data-ttu-id="0962d-129">我們會將應用程式\_資料目錄新增至專案，以保存我們的 SQL Server Express 資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="0962d-129">We'll add an App\_Data directory to our project to hold our SQL Server Express database files.</span></span> <span data-ttu-id="0962d-130">應用程式\_資料是 ASP.NET 中的特殊目錄，其中已經具有資料庫存取的正確安全性存取權限。</span><span class="sxs-lookup"><span data-stu-id="0962d-130">App\_Data is a special directory in ASP.NET which already has the correct security access permissions for database access.</span></span> <span data-ttu-id="0962d-131">從 [專案] 功能表中，依序選取 [新增 ASP.NET 資料夾] 和 [應用程式\_資料]。</span><span class="sxs-lookup"><span data-stu-id="0962d-131">From the Project menu, select Add ASP.NET Folder, then App\_Data.</span></span>

![](mvc-music-store-part-4/_static/image1.png)

### <a name="creating-a-connection-string-in-the-webconfig-file"></a><span data-ttu-id="0962d-132">在 web.config 檔案中建立連接字串</span><span class="sxs-lookup"><span data-stu-id="0962d-132">Creating a Connection String in the web.config file</span></span>

<span data-ttu-id="0962d-133">我們會在網站的設定檔中新增幾行，讓 Entity Framework 知道如何連接到我們的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0962d-133">We will add a few lines to the website's configuration file so that Entity Framework knows how to connect to our database.</span></span> <span data-ttu-id="0962d-134">按兩下位於專案根目錄中的 web.config 檔案。</span><span class="sxs-lookup"><span data-stu-id="0962d-134">Double-click on the Web.config file located in the root of the project.</span></span>

![](mvc-music-store-part-4/_static/image2.png)

<span data-ttu-id="0962d-135">請前往此檔案的底部，並在最後一行的正上方加入 &lt;connectionStrings&gt; 區段，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0962d-135">Scroll to the bottom of this file and add a &lt;connectionStrings&gt; section directly above the last line, as shown below.</span></span>

[!code-xml[Main](mvc-music-store-part-4/samples/sample4.xml)]

### <a name="adding-a-context-class"></a><span data-ttu-id="0962d-136">加入內容類別</span><span class="sxs-lookup"><span data-stu-id="0962d-136">Adding a Context Class</span></span>

<span data-ttu-id="0962d-137">以滑鼠右鍵按一下 [模型] 資料夾，然後加入名為 MusicStoreEntities.cs 的新類別。</span><span class="sxs-lookup"><span data-stu-id="0962d-137">Right-click the Models folder and add a new class named MusicStoreEntities.cs.</span></span>

![](mvc-music-store-part-4/_static/image3.png)

<span data-ttu-id="0962d-138">這個類別將代表 Entity Framework 資料庫內容，並會為我們處理我們的建立、讀取、更新和刪除作業。</span><span class="sxs-lookup"><span data-stu-id="0962d-138">This class will represent the Entity Framework database context, and will handle our create, read, update, and delete operations for us.</span></span> <span data-ttu-id="0962d-139">此類別的程式碼如下所示。</span><span class="sxs-lookup"><span data-stu-id="0962d-139">The code for this class is shown below.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample5.cs)]

<span data-ttu-id="0962d-140">這就是-沒有其他設定、特殊介面等等。藉由擴充 DbCoNtext 基類，我們的 MusicStoreEntities 類別能夠為我們處理我們的資料庫作業。</span><span class="sxs-lookup"><span data-stu-id="0962d-140">That's it - there's no other configuration, special interfaces, etc. By extending the DbContext base class, our MusicStoreEntities class is able to handle our database operations for us.</span></span> <span data-ttu-id="0962d-141">既然我們已連結，現在讓我們在我們的模型類別中加入幾個屬性，以利用資料庫中的一些額外資訊。</span><span class="sxs-lookup"><span data-stu-id="0962d-141">Now that we've got that hooked up, let's add a few more properties to our model classes to take advantage of some of the additional information in our database.</span></span>

### <a name="adding-our-store-catalog-data"></a><span data-ttu-id="0962d-142">新增我們的商店目錄資料</span><span class="sxs-lookup"><span data-stu-id="0962d-142">Adding our store catalog data</span></span>

<span data-ttu-id="0962d-143">我們將利用 Entity Framework 中的功能，將「種子」資料新增至新建立的資料庫。</span><span class="sxs-lookup"><span data-stu-id="0962d-143">We will take advantage of a feature in Entity Framework which adds "seed" data to a newly created database.</span></span> <span data-ttu-id="0962d-144">這會預先填入我們的商店目錄，其中包含內容清單、演出者和專輯。</span><span class="sxs-lookup"><span data-stu-id="0962d-144">This will pre-populate our store catalog with a list of Genres, Artists, and Albums.</span></span> <span data-ttu-id="0962d-145">MvcMusicStore-Assets .zip 下載-其中包含我們稍早在本教學課程中使用的網站設計檔案-具有具有此種子資料的類別檔案，該檔案位於名為 Code 的資料夾中。</span><span class="sxs-lookup"><span data-stu-id="0962d-145">The MvcMusicStore-Assets.zip download - which included our site design files used earlier in this tutorial - has a class file with this seed data, located in a folder named Code.</span></span>

<span data-ttu-id="0962d-146">在 [程式碼/模型] 資料夾內，找出 SampleData.cs 檔案，並將它放入專案的 [模型] 資料夾中，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0962d-146">Within the Code / Models folder, locate the SampleData.cs file and drop it into the Models folder in our project, as shown below.</span></span>

![](mvc-music-store-part-4/_static/image4.png)

<span data-ttu-id="0962d-147">現在，我們需要新增一行程式碼，告訴 Entity Framework 該 SampleData 類別的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="0962d-147">Now we need to add one line of code to tell Entity Framework about that SampleData class.</span></span> <span data-ttu-id="0962d-148">按兩下專案根目錄中的 global.asax 檔案加以開啟，然後將下列一行新增至應用程式\_Start 方法的頂端。</span><span class="sxs-lookup"><span data-stu-id="0962d-148">Double-click on the Global.asax file in the root of the project to open it and add the following line to the top the Application\_Start method.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample6.cs)]

<span data-ttu-id="0962d-149">到目前為止，我們已完成為專案設定 Entity Framework 所需的工作。</span><span class="sxs-lookup"><span data-stu-id="0962d-149">At this point, we've completed the work necessary to configure Entity Framework for our project.</span></span>

## <a name="querying-the-database"></a><span data-ttu-id="0962d-150">查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="0962d-150">Querying the Database</span></span>

<span data-ttu-id="0962d-151">現在讓我們更新我們的 StoreController，如此一來，您就可以改為使用「虛擬資料」來呼叫我們的資料庫，以查詢其所有資訊。</span><span class="sxs-lookup"><span data-stu-id="0962d-151">Now let's update our StoreController so that instead of using "dummy data" it instead calls into our database to query all of its information.</span></span> <span data-ttu-id="0962d-152">首先，我們會在**StoreController**上宣告一個欄位，以保存 MusicStoreEntities 類別的實例，名為 storeDB：</span><span class="sxs-lookup"><span data-stu-id="0962d-152">We'll start by declaring a field on the **StoreController** to hold an instance of the MusicStoreEntities class, named storeDB:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample7.cs)]

### <a name="updating-the-store-index-to-query-the-database"></a><span data-ttu-id="0962d-153">更新存放區索引以查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="0962d-153">Updating the Store Index to query the database</span></span>

<span data-ttu-id="0962d-154">MusicStoreEntities 類別是由 Entity Framework 維護，並公開資料庫中每個資料表的集合屬性。</span><span class="sxs-lookup"><span data-stu-id="0962d-154">The MusicStoreEntities class is maintained by the Entity Framework and exposes a collection property for each table in our database.</span></span> <span data-ttu-id="0962d-155">讓我們更新我們的 StoreController 索引動作，以取得資料庫中的所有內容。</span><span class="sxs-lookup"><span data-stu-id="0962d-155">Let's update our StoreController's Index action to retrieve all Genres in our database.</span></span> <span data-ttu-id="0962d-156">我們先前是以硬式編碼字串資料的方式來執行這項操作。</span><span class="sxs-lookup"><span data-stu-id="0962d-156">Previously we did this by hard-coding string data.</span></span> <span data-ttu-id="0962d-157">現在，我們可以改為使用 Entity Framework 內容 Generes 集合：</span><span class="sxs-lookup"><span data-stu-id="0962d-157">Now we can instead just use the Entity Framework context Generes collection:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample8.cs)]

<span data-ttu-id="0962d-158">我們不需要對我們的 View 範本進行任何變更，因為我們仍然會傳回我們先前傳回的相同 StoreIndexViewModel-我們現在只會從資料庫傳回即時資料。</span><span class="sxs-lookup"><span data-stu-id="0962d-158">No changes need to happen to our View template since we're still returning the same StoreIndexViewModel we returned before - we're just returning live data from our database now.</span></span>

<span data-ttu-id="0962d-159">當我們再次執行專案並流覽 "/Store" URL 時，我們現在會在資料庫中看到所有內容清單：</span><span class="sxs-lookup"><span data-stu-id="0962d-159">When we run the project again and visit the "/Store" URL, we'll now see a list of all Genres in our database:</span></span>

![](mvc-music-store-part-4/_static/image1.jpg)

### <a name="updating-store-browse-and-details-to-use-live-data"></a><span data-ttu-id="0962d-160">更新存放區流覽和詳細資料以使用即時資料</span><span class="sxs-lookup"><span data-stu-id="0962d-160">Updating Store Browse and Details to use live data</span></span>

<span data-ttu-id="0962d-161">我們使用/Store/Browse？內容類型 = *[部分類型]* 動作方法，依名稱搜尋內容類型。</span><span class="sxs-lookup"><span data-stu-id="0962d-161">With the /Store/Browse?genre=*[some-genre]* action method, we're searching for a Genre by name.</span></span> <span data-ttu-id="0962d-162">我們只會預期一個結果，因為在相同的內容類型名稱中不應該有兩個專案，因此我們可以使用。LINQ 中的單一（）延伸模組，可查詢適當的類型物件，如下所示（尚不輸入此項）：</span><span class="sxs-lookup"><span data-stu-id="0962d-162">We only expect one result, since we shouldn't ever have two entries for the same Genre name, and so we can use the .Single() extension in LINQ to query for the appropriate Genre object like this (don't type this yet):</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample9.cs)]

<span data-ttu-id="0962d-163">單一方法會採用 Lambda 運算式做為參數，這會指定我們想要單一內容類型物件，使其名稱符合我們定義的值。</span><span class="sxs-lookup"><span data-stu-id="0962d-163">The Single method takes a Lambda expression as a parameter, which specifies that we want a single Genre object such that its name matches the value we've defined.</span></span> <span data-ttu-id="0962d-164">在上述案例中，我們會載入單一類型物件，其名稱值符合 Disco。</span><span class="sxs-lookup"><span data-stu-id="0962d-164">In the case above, we are loading a single Genre object with a Name value matching Disco.</span></span>

<span data-ttu-id="0962d-165">我們將利用 Entity Framework 功能，讓我們在取得內容類型物件時，指出我們想要載入的其他相關實體。</span><span class="sxs-lookup"><span data-stu-id="0962d-165">We'll take advantage of an Entity Framework feature that allows us to indicate other related entities we want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="0962d-166">這項功能稱為「查詢結果塑造」，可讓我們減少存取資料庫所需的次數，以取得我們所需的所有資訊。</span><span class="sxs-lookup"><span data-stu-id="0962d-166">This feature is called Query Result Shaping, and enables us to reduce the number of times we need to access the database to retrieve all of the information we need.</span></span> <span data-ttu-id="0962d-167">我們想要預先提取專輯以取得我們所取得的內容類型，因此我們將更新查詢以包含在內容類型中。包含（「專輯」）表示我們也想要相關的專輯。</span><span class="sxs-lookup"><span data-stu-id="0962d-167">We want to pre-fetch the Albums for Genre we retrieve, so we'll update our query to include from Genres.Include("Albums") to indicate that we want related albums as well.</span></span> <span data-ttu-id="0962d-168">這會更有效率，因為它會在單一資料庫要求中同時取得內容類型和專輯資料。</span><span class="sxs-lookup"><span data-stu-id="0962d-168">This is more efficient, since it will retrieve both our Genre and Album data in a single database request.</span></span>

<span data-ttu-id="0962d-169">有了這方面的說明，以下是我們更新的「流覽控制器」動作的樣子：</span><span class="sxs-lookup"><span data-stu-id="0962d-169">With the explanations out of the way, here's how our updated Browse controller action looks:</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample10.cs)]

<span data-ttu-id="0962d-170">我們現在可以更新 [Store] 流覽視圖，以顯示每個內容類型中可用的專輯。</span><span class="sxs-lookup"><span data-stu-id="0962d-170">We can now update the Store Browse View to display the albums which are available in each Genre.</span></span> <span data-ttu-id="0962d-171">開啟 [view] 範本（可在/Views/Store/Browse.cshtml 中找到），然後新增項目符號清單，如下所示。</span><span class="sxs-lookup"><span data-stu-id="0962d-171">Open the view template (found in /Views/Store/Browse.cshtml) and add a bulleted list of Albums as shown below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample11.cshtml)]

<span data-ttu-id="0962d-172">執行我們的應用程式，並流覽至/Store/Browse？內容類型 = 爵士樂會顯示我們現在已從資料庫提取結果，並顯示所選類型中的所有專輯。</span><span class="sxs-lookup"><span data-stu-id="0962d-172">Running our application and browsing to /Store/Browse?genre=Jazz shows that our results are now being pulled from the database, displaying all albums in our selected Genre.</span></span>

![](mvc-music-store-part-4/_static/image2.jpg)

<span data-ttu-id="0962d-173">我們會對/Store/Details/[id] URL 進行相同的變更，並將我們的虛擬資料取代成一個資料庫查詢，其會載入識別碼符合參數值的專輯。</span><span class="sxs-lookup"><span data-stu-id="0962d-173">We'll make the same change to our /Store/Details/[id] URL, and replace our dummy data with a database query which loads an Album whose ID matches the parameter value.</span></span>

[!code-csharp[Main](mvc-music-store-part-4/samples/sample12.cs)]

<span data-ttu-id="0962d-174">執行我們的應用程式並流覽至/Store/Details/1，會顯示我們的結果現在已從資料庫提取。</span><span class="sxs-lookup"><span data-stu-id="0962d-174">Running our application and browsing to /Store/Details/1 shows that our results are now being pulled from the database.</span></span>

![](mvc-music-store-part-4/_static/image5.png)

<span data-ttu-id="0962d-175">現在，我們的商店詳細資料頁面已設定為依專輯識別碼顯示專輯，讓我們更新 [**流覽]** 視圖以連結至詳細資料檢視。</span><span class="sxs-lookup"><span data-stu-id="0962d-175">Now that our Store Details page is set up to display an album by the Album ID, let's update the **Browse** view to link to the Details view.</span></span> <span data-ttu-id="0962d-176">我們會使用 Html.actionlink，與我們在上一節結尾處的「存放區索引」連結和「儲存」流覽方式完全相同。</span><span class="sxs-lookup"><span data-stu-id="0962d-176">We will use Html.ActionLink, exactly as we did to link from Store Index to Store Browse at the end of the previous section.</span></span> <span data-ttu-id="0962d-177">流覽視圖的完整來源如下所示。</span><span class="sxs-lookup"><span data-stu-id="0962d-177">The complete source for the Browse view appears below.</span></span>

[!code-cshtml[Main](mvc-music-store-part-4/samples/sample13.cshtml)]

<span data-ttu-id="0962d-178">我們現在可以從我們的 [商店] 頁面流覽至 [內容類型] 頁面，其中會列出可用的專輯，而按一下專輯後，我們就可以查看該專輯的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="0962d-178">We're now able to browse from our Store page to a Genre page, which lists the available albums, and by clicking on an album we can view details for that album.</span></span>

![](mvc-music-store-part-4/_static/image6.png)

> [!div class="step-by-step"]
> <span data-ttu-id="0962d-179">[上一頁](mvc-music-store-part-3.md)
> [下一頁](mvc-music-store-part-5.md)</span><span class="sxs-lookup"><span data-stu-id="0962d-179">[Previous](mvc-music-store-part-3.md)
[Next](mvc-music-store-part-5.md)</span></span>
