---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
title: 新增 Create 方法和 Create View |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: a3a90963-0286-4fa0-9b3d-c230cc18b0a3
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part6
msc.type: authoredcontent
ms.openlocfilehash: 05a281720f76b107fe8d902ef60d5d2e72af3ef5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543656"
---
# <a name="adding-a-create-method-and-create-view"></a><span data-ttu-id="991d1-104">新增 Create 方法和 Create 檢視</span><span class="sxs-lookup"><span data-stu-id="991d1-104">Adding a Create Method and Create View</span></span>

<span data-ttu-id="991d1-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="991d1-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="991d1-106">這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="991d1-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="991d1-107">您將建立可從資料庫讀取和寫入的簡單 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="991d1-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="991d1-108">請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="991d1-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="991d1-109">在本節中，我們將會執行必要的支援，讓使用者能夠在資料庫中建立新電影。</span><span class="sxs-lookup"><span data-stu-id="991d1-109">In this section we are going to implement the support necessary to enable users to create new movies in our database.</span></span> <span data-ttu-id="991d1-110">我們會藉由執行/Movies/Create URL 動作來完成這項工作。</span><span class="sxs-lookup"><span data-stu-id="991d1-110">We'll do this by implementing the /Movies/Create URL action.</span></span>

<span data-ttu-id="991d1-111">/Movies/Create URL 的執行過程分為兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="991d1-111">Implementing the /Movies/Create URL is a two step process.</span></span> <span data-ttu-id="991d1-112">當使用者第一次造訪/Movies/Create URL 時，我們想要顯示 HTML 表單，他們可以填寫以輸入新電影。</span><span class="sxs-lookup"><span data-stu-id="991d1-112">When a user first visits the /Movies/Create URL we want to show them an HTML form that they can fill out to enter a new movie.</span></span> <span data-ttu-id="991d1-113">然後，當使用者提交表單並將資料張貼回伺服器時，我們會想要抓取張貼的內容，並將它儲存到資料庫中。</span><span class="sxs-lookup"><span data-stu-id="991d1-113">Then, when the user submits the form and posts the data back to the server, we want to retrieve the posted contents and save it into our database.</span></span>

<span data-ttu-id="991d1-114">我們會在 Moviescontroller.cs 類別內的兩個 Create （）方法內，執行這兩個步驟。</span><span class="sxs-lookup"><span data-stu-id="991d1-114">We'll implement these two steps within two Create() methods within our MoviesController class.</span></span> <span data-ttu-id="991d1-115">其中一種方法會顯示 &lt;表單&gt;，使用者應在此填寫以建立新的電影。</span><span class="sxs-lookup"><span data-stu-id="991d1-115">One method will show the &lt;form&gt; that the user should fill out to create a new movie.</span></span> <span data-ttu-id="991d1-116">第二種方法會在使用者將 &lt;表單&gt; 回伺服器時，處理張貼的資料處理，並在資料庫中儲存新的電影。</span><span class="sxs-lookup"><span data-stu-id="991d1-116">The second method will handle processing the posted data when the user submits the &lt;form&gt; back to the server, and save a new Movie within our database.</span></span>

<span data-ttu-id="991d1-117">以下是我們要新增至 Moviescontroller.cs 類別的程式碼，以執行此動作：</span><span class="sxs-lookup"><span data-stu-id="991d1-117">Below is the code we'll add to our MoviesController class to implement this:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample1.cs)]

<span data-ttu-id="991d1-118">上述程式碼包含我們在控制器內所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="991d1-118">The above code contains all of the code that we'll need within our Controller.</span></span>

<span data-ttu-id="991d1-119">現在，讓我們來執行建立視圖範本，用來向使用者顯示表單。</span><span class="sxs-lookup"><span data-stu-id="991d1-119">Let's now implement the Create View template that we'll use to display a form to the user.</span></span> <span data-ttu-id="991d1-120">我們要在第一個 Create 方法中按一下滑鼠右鍵，然後選取 [新增視圖] 來建立電影表單的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="991d1-120">We'll right click in the first Create method and select "Add View" to create the view template for our Movie form.</span></span>

<span data-ttu-id="991d1-121">我們會選擇將「電影」做為 view 資料類別來傳遞，並指出我們想要「scaffold」「建立」範本。</span><span class="sxs-lookup"><span data-stu-id="991d1-121">We'll select that we are going to pass the view template a "Movie" as its view data class, and indicate that we want to "scaffold" a "Create" template.</span></span>

<span data-ttu-id="991d1-122">[![加入視圖](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="991d1-122">[![Add View](getting-started-with-mvc-part6/_static/image2.png)](getting-started-with-mvc-part6/_static/image1.png)</span></span>

<span data-ttu-id="991d1-123">按一下 [新增] 按鈕之後，就會為您建立 \Movies\Create.aspx View 範本。</span><span class="sxs-lookup"><span data-stu-id="991d1-123">After you click the Add button, \Movies\Create.aspx View template will be created for you.</span></span> <span data-ttu-id="991d1-124">因為我們已從 [查看內容] 下拉式清單中選取 [建立]，所以 [加入視圖] 對話方塊會自動為我們「scaffold」一些預設內容。</span><span class="sxs-lookup"><span data-stu-id="991d1-124">Because we selected "Create" from the "view content" dropdown, the Add View dialog automatically "scaffolded" some default content for us.</span></span> <span data-ttu-id="991d1-125">此樣板建立了一個 HTML &lt;表單&gt;、一個位置用於驗證錯誤訊息，而且由於架構會知道電影，因此它會為類別的每個屬性建立標籤和欄位。</span><span class="sxs-lookup"><span data-stu-id="991d1-125">The scaffolding created an HTML &lt;form&gt;, a place for validation error messages to go, and since scaffolding knows about Movies, it created Label and Fields for each property of our class.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part6/samples/sample2.aspx)]

<span data-ttu-id="991d1-126">由於我們的資料庫會自動為電影提供識別碼，因此讓我們移除參考模型的欄位。來自我們建立視圖的識別碼。</span><span class="sxs-lookup"><span data-stu-id="991d1-126">Since our database automatically gives a Movie an ID, let's remove those fields that reference model.Id from our Create View.</span></span> <span data-ttu-id="991d1-127">&lt;圖例&gt;欄位之後，請移除7行，&lt;/legend&gt; 顯示我們不想要的 ID 欄位。</span><span class="sxs-lookup"><span data-stu-id="991d1-127">Remove the 7 lines after &lt;legend&gt;Fields&lt;/legend&gt; as they show the ID field that we don't want.</span></span>

<span data-ttu-id="991d1-128">現在讓我們建立新的電影，並將它加入至資料庫。</span><span class="sxs-lookup"><span data-stu-id="991d1-128">Let's now create a new movie and add it to the database.</span></span> <span data-ttu-id="991d1-129">我們將再次執行應用程式並流覽 "/Movies" URL，然後按一下 [建立] 連結以新增電影。</span><span class="sxs-lookup"><span data-stu-id="991d1-129">We'll do this by running the application again and visit the "/Movies" URL and click the "Create" link to add a new Movie.</span></span>

<span data-ttu-id="991d1-130">[![建立-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="991d1-130">[![Create - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image4.png)](getting-started-with-mvc-part6/_static/image3.png)</span></span>

<span data-ttu-id="991d1-131">當我們按一下 [建立] 按鈕時，我們會將此表單上的資料張貼到我們剛才建立的/Movies/Create 方法中（透過 HTTP POST）。</span><span class="sxs-lookup"><span data-stu-id="991d1-131">When we click the Create button, we'll be posting back (via HTTP POST) the data on this form to the /Movies/Create method that we just created.</span></span> <span data-ttu-id="991d1-132">就像系統會自動從 URL 取得 "Numtimes is" 和 "name" 參數，並將它們對應至先前方法上的參數，系統會自動從文章中取出表單欄位，並將其對應至物件。</span><span class="sxs-lookup"><span data-stu-id="991d1-132">Just like when the system automatically took the "numTimes" and "name " parameter out of the URL and mapped them to parameters on a method earlier, the system will automatically take the Form Fields from a POST and map them to an object.</span></span> <span data-ttu-id="991d1-133">在此情況下，HTML 欄位中的值（例如 "ReleaseDate" 和 "Title"）會自動放入電影新實例的正確屬性中。</span><span class="sxs-lookup"><span data-stu-id="991d1-133">In this case, values from fields in HTML like "ReleaseDate" and "Title" will automatically be put into the correct properties of a new instance of a Movie.</span></span>

<span data-ttu-id="991d1-134">讓我們再次查看 Moviescontroller.cs 的第二個 Create 方法。</span><span class="sxs-lookup"><span data-stu-id="991d1-134">Let's look at the second Create method from our MoviesController again.</span></span> <span data-ttu-id="991d1-135">請注意，它會採用「電影」物件做為引數：</span><span class="sxs-lookup"><span data-stu-id="991d1-135">Notice how it takes a "Movie" object as an argument:</span></span>

[!code-csharp[Main](getting-started-with-mvc-part6/samples/sample3.cs)]

<span data-ttu-id="991d1-136">此 Movie 物件接著會傳遞至建立動作方法的 [HttpPost] 版本，並將它儲存在資料庫中，然後將使用者重新導向回到 Index （）動作方法，這會在電影清單中顯示儲存的結果：</span><span class="sxs-lookup"><span data-stu-id="991d1-136">This Movie object was then passed to the [HttpPost] version of our Create action method, and we saved it in the database and then redirected the user back to the Index() action method which will show the saved result in the movie list:</span></span>

<span data-ttu-id="991d1-137">[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="991d1-137">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part6/_static/image6.png)](getting-started-with-mvc-part6/_static/image5.png)</span></span>

<span data-ttu-id="991d1-138">不過，我們不會檢查電影是否正確，而且資料庫不允許我們儲存沒有標題的電影。</span><span class="sxs-lookup"><span data-stu-id="991d1-138">We aren't checking if our movies are correct, though, and the database won't allow us to save a movie with no Title.</span></span> <span data-ttu-id="991d1-139">如果我們可以告訴使用者，在資料庫擲回錯誤之前，會有很大的好處。</span><span class="sxs-lookup"><span data-stu-id="991d1-139">It'd be nice if we could tell the user that before the database threw an error.</span></span> <span data-ttu-id="991d1-140">我們接下來會在應用程式中新增驗證支援。</span><span class="sxs-lookup"><span data-stu-id="991d1-140">We'll do this next by adding validation support to our application.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="991d1-141">[上一頁](getting-started-with-mvc-part5.md)
> [下一頁](getting-started-with-mvc-part7.md)</span><span class="sxs-lookup"><span data-stu-id="991d1-141">[Previous](getting-started-with-mvc-part5.md)
[Next](getting-started-with-mvc-part7.md)</span></span>
