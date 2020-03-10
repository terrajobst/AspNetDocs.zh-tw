---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
title: 從控制器存取模型的資料 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 004703cd-e0e9-4ba7-9974-1b0475c71222
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part5
msc.type: authoredcontent
ms.openlocfilehash: 207ed880977d794d81efdc1ea458d17a68d501d8
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543747"
---
# <a name="accessing-your-models-data-from-a-controller"></a><span data-ttu-id="21446-104">從控制器存取模型資料</span><span class="sxs-lookup"><span data-stu-id="21446-104">Accessing your Model's Data from a Controller</span></span>

<span data-ttu-id="21446-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="21446-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="21446-106">這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="21446-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="21446-107">您將建立可從資料庫讀取和寫入的簡單 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="21446-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="21446-108">請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="21446-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="21446-109">在本節中，我們將建立一個新的 Moviescontroller.cs 類別，並撰寫一些程式碼來抓取電影資料，並使用視圖範本將其顯示回瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="21446-109">In this section we are going to create a new MoviesController class, and write some code that retrieves our Movie data and displays it back to the browser using a View template.</span></span>

<span data-ttu-id="21446-110">以滑鼠右鍵按一下 [控制器] 資料夾，並建立新的 Moviescontroller.cs。</span><span class="sxs-lookup"><span data-stu-id="21446-110">Right click on the Controllers folder and make a new MoviesController.</span></span>

<span data-ttu-id="21446-111">[![新增控制器](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="21446-111">[![Add Controller](getting-started-with-mvc-part5/_static/image2.png)](getting-started-with-mvc-part5/_static/image1.png)</span></span>

<span data-ttu-id="21446-112">這會在專案內的 \Controllers 資料夾下方建立新的 "MoviesController.cs" 檔案。</span><span class="sxs-lookup"><span data-stu-id="21446-112">This will create a new "MoviesController.cs" file underneath our \Controllers folder within our project.</span></span> <span data-ttu-id="21446-113">讓我們更新 MovieController，以從我們新填入的資料庫中取出電影清單。</span><span class="sxs-lookup"><span data-stu-id="21446-113">Let's update the MovieController to retrieve the list of movies from our newly populated database.</span></span>

[!code-csharp[Main](getting-started-with-mvc-part5/samples/sample1.cs)]

<span data-ttu-id="21446-114">我們正在執行 LINQ 查詢，因此我們只會取出1984年夏季之後所發行的電影。</span><span class="sxs-lookup"><span data-stu-id="21446-114">We are performing a LINQ query so that we only retrieve movies released after the summer of 1984.</span></span> <span data-ttu-id="21446-115">我們需要一個 View 範本來轉譯這份電影清單，因此，請在方法中按一下滑鼠右鍵，然後選取 [新增視圖] 加以建立。</span><span class="sxs-lookup"><span data-stu-id="21446-115">We'll need a View template to render this list of movies back, so right-click in the method and select Add View to create it.</span></span>

<span data-ttu-id="21446-116">在 [新增視圖] 對話方塊中，我們會指出我們將清單&lt;電影&gt; 到我們的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="21446-116">Within the Add View dialog we'll indicate that we are passing a List&lt;Movies.Models.Movie&gt; to our View template.</span></span> <span data-ttu-id="21446-117">與先前使用 [加入視圖] 對話方塊並選擇建立「空白」範本的時間不同，這次我們會指出我們想要 Visual Studio 為我們自動「scaffold」具有一些預設內容的視圖範本。</span><span class="sxs-lookup"><span data-stu-id="21446-117">Unlike the previous times we used the Add View dialog and chose to create an "Empty" template, this time we'll indicate that we want Visual Studio to automatically "scaffold" a view template for us with some default content.</span></span> <span data-ttu-id="21446-118">我們將在 [View content] 下拉式功能表中選取 [清單] 專案來執行此動作。</span><span class="sxs-lookup"><span data-stu-id="21446-118">We'll do this by selecting the "List" item within the "View content dropdown menu.</span></span>

<span data-ttu-id="21446-119">請記住，當您建立新的類別時，您必須編譯應用程式，它才會顯示在 [加入視圖] 對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="21446-119">Remember, when you have a created a new class you'll need to compile your application for it to show up in the Add View Dialog.</span></span>

![加入視圖](getting-started-with-mvc-part5/_static/image3.png)

<span data-ttu-id="21446-121">按一下 [新增]，系統就會自動為我們產生顯示電影清單的視圖程式碼。</span><span class="sxs-lookup"><span data-stu-id="21446-121">Click add and the system will automatically generate the code for a View for us that displays our list of movies.</span></span> <span data-ttu-id="21446-122">這是將 &lt;h2&gt; 標題變更為「我的電影清單」的好時機，如同我們先前使用 Hello World view 所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="21446-122">This is a good time to change the &lt;h2&gt; heading to something like "My Movie List" like we did earlier with the Hello World view.</span></span>

<span data-ttu-id="21446-123">[![電影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="21446-123">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part5/_static/image5.png)](getting-started-with-mvc-part5/_static/image4.png)</span></span>

<span data-ttu-id="21446-124">執行您的應用程式，並流覽網址列中的/Movies。</span><span class="sxs-lookup"><span data-stu-id="21446-124">Run your application and visit /Movies in the address bar.</span></span> <span data-ttu-id="21446-125">現在，我們已使用控制器內的基本查詢從資料庫中取出資料，並將資料傳回給瞭解電影的視圖。</span><span class="sxs-lookup"><span data-stu-id="21446-125">Now we've retrieved data from the database using a basic query inside the Controller and returned the data to a View that knows about Movies.</span></span> <span data-ttu-id="21446-126">該視圖接著會旋轉電影清單，並為我們建立資料的資料表。</span><span class="sxs-lookup"><span data-stu-id="21446-126">That View then spins through the list of Movies and creates a table of data for us.</span></span>

<span data-ttu-id="21446-127">[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="21446-127">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image7.png)](getting-started-with-mvc-part5/_static/image6.png)</span></span>

<span data-ttu-id="21446-128">我們不會使用此應用程式來執行編輯、詳細資料和刪除功能，因此我們不需要 scaffold 範本為我們建立的預設連結。</span><span class="sxs-lookup"><span data-stu-id="21446-128">We won't be implementing Edit, Details and Delete functionality with this application - so we don't need the default links that the scaffold template created for us.</span></span> <span data-ttu-id="21446-129">開啟/Movies/Index.aspx 檔案，並將其移除。</span><span class="sxs-lookup"><span data-stu-id="21446-129">Open up the /Movies/Index.aspx file and remove them.</span></span>

<span data-ttu-id="21446-130">以下是我們進行這些變更之後，更新後的視圖範本應該看起來的原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="21446-130">Here is the source code for what our updated View template should look like once we make these changes:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part5/samples/sample2.aspx)]

<span data-ttu-id="21446-131">它會建立我們不需要的連結，因此我們會在此範例中將其刪除。</span><span class="sxs-lookup"><span data-stu-id="21446-131">It's creating links that we won't need, so we'll delete them for this example.</span></span> <span data-ttu-id="21446-132">我們會保留 [建立新的] 連結，如下所示！</span><span class="sxs-lookup"><span data-stu-id="21446-132">We will keep our Create New link though, as that's next!</span></span> <span data-ttu-id="21446-133">以下是我們的應用程式在移除該資料行時的外觀。</span><span class="sxs-lookup"><span data-stu-id="21446-133">Here's what our app looks like with that column removed.</span></span>

<span data-ttu-id="21446-134">[![電影清單-Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="21446-134">[![Movie List - Windows Internet Explorer](getting-started-with-mvc-part5/_static/image9.png)](getting-started-with-mvc-part5/_static/image8.png)</span></span>

<span data-ttu-id="21446-135">我們現在有簡單的電影資料清單。</span><span class="sxs-lookup"><span data-stu-id="21446-135">We now have a simple listing of our movie data.</span></span> <span data-ttu-id="21446-136">不過，如果我們按一下 [建立新的] 連結，就會收到錯誤，因為它並未連接！</span><span class="sxs-lookup"><span data-stu-id="21446-136">However, if we click the "Create New" link, we'll get an error as it's not hooked up!</span></span> <span data-ttu-id="21446-137">讓我們來執行建立動作方法，並讓使用者在資料庫中輸入新電影。</span><span class="sxs-lookup"><span data-stu-id="21446-137">Let's implement a Create Action method and enable a user to enter new movies in our database.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="21446-138">[上一頁](getting-started-with-mvc-part4.md)
> [下一頁](getting-started-with-mvc-part6.md)</span><span class="sxs-lookup"><span data-stu-id="21446-138">[Previous](getting-started-with-mvc-part4.md)
[Next](getting-started-with-mvc-part6.md)</span></span>
