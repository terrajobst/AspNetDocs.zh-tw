---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
title: 將資料行加入至模型 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 7ae696b9-348f-4993-8ebb-a838acbe0c28
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part8
msc.type: authoredcontent
ms.openlocfilehash: 1cf092c3db3959d6f47006f1be2ba82833c5dc06
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78543579"
---
# <a name="adding-a-column-to-the-model"></a><span data-ttu-id="73959-104">將資料行新增至模型</span><span class="sxs-lookup"><span data-stu-id="73959-104">Adding a Column to the Model</span></span>

<span data-ttu-id="73959-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="73959-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="73959-106">這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="73959-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="73959-107">您將建立可從資料庫讀取和寫入的簡單 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="73959-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="73959-108">請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="73959-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="73959-109">在本節中，我們將逐步解說如何對資料庫架構進行變更，並處理應用程式內的變更。</span><span class="sxs-lookup"><span data-stu-id="73959-109">In this section we are going to walk through how we can make changes to the schema of our database, and handle the changes within our application.</span></span>

<span data-ttu-id="73959-110">讓我們在電影資料表中新增「評等」資料行。</span><span class="sxs-lookup"><span data-stu-id="73959-110">Let's add a "Rating" Column to the Movie table.</span></span> <span data-ttu-id="73959-111">回到 IDE，然後按一下 [資料庫總管]。</span><span class="sxs-lookup"><span data-stu-id="73959-111">Go back to the IDE and click the Database Explorer.</span></span> <span data-ttu-id="73959-112">以滑鼠右鍵按一下電影資料表，然後選取 [開啟資料表定義]。</span><span class="sxs-lookup"><span data-stu-id="73959-112">Right click the Movie table and select Open Table Definition.</span></span>

<span data-ttu-id="73959-113">新增「評等」資料行，如下所示。</span><span class="sxs-lookup"><span data-stu-id="73959-113">Add a "Rating" column as seen below.</span></span> <span data-ttu-id="73959-114">因為我們目前沒有任何評等，所以資料行可以允許 null。</span><span class="sxs-lookup"><span data-stu-id="73959-114">Since we don't have any Ratings now, the column can allow nulls.</span></span> <span data-ttu-id="73959-115">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="73959-115">Click Save.</span></span>

<span data-ttu-id="73959-116">[![編輯電影資料表](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="73959-116">[![Editing Movies Table](getting-started-with-mvc-part8/_static/image2.png)](getting-started-with-mvc-part8/_static/image1.png)</span></span>

<span data-ttu-id="73959-117">接下來，返回方案總管並開啟 [電影 .edmx] 檔案（位於 \Models 資料夾）。</span><span class="sxs-lookup"><span data-stu-id="73959-117">Next, return to the Solution Explorer and open up the Movies.edmx file (which is in the \Models folder).</span></span> <span data-ttu-id="73959-118">以滑鼠右鍵按一下設計介面（白色區域），然後選取 [從資料庫更新模型]。</span><span class="sxs-lookup"><span data-stu-id="73959-118">Right click on the design surface (the white area) and select Update Model from Database.</span></span>

<span data-ttu-id="73959-119">[![電影-Microsoft Visual Web Developer 2010 Express （11）](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="73959-119">[![Movies - Microsoft Visual Web Developer 2010 Express (11)](getting-started-with-mvc-part8/_static/image4.png)](getting-started-with-mvc-part8/_static/image3.png)</span></span>

<span data-ttu-id="73959-120">這會啟動「更新嚮導」。</span><span class="sxs-lookup"><span data-stu-id="73959-120">This will launch the "Update Wizard".</span></span> <span data-ttu-id="73959-121">按一下其中的 [重新整理] 索引標籤，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="73959-121">Click the Refresh tab within it and click Finish.</span></span> <span data-ttu-id="73959-122">我們的電影模型類別會以新的資料行更新。</span><span class="sxs-lookup"><span data-stu-id="73959-122">Our Movie model class will then be updated with the new column.</span></span>

![更新嚮導（2）](getting-started-with-mvc-part8/_static/image5.png)

<span data-ttu-id="73959-124">按一下 [完成] 之後，您就可以看到新的評等資料行已新增至模型中的 Movie 實體。</span><span class="sxs-lookup"><span data-stu-id="73959-124">After clicking Finish, you can see the new Rating Column has been added to the Movie Entity in our model.</span></span>

<span data-ttu-id="73959-125">[![Movie 實體](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="73959-125">[![Movie Entity](getting-started-with-mvc-part8/_static/image7.png)](getting-started-with-mvc-part8/_static/image6.png)</span></span>

<span data-ttu-id="73959-126">我們已在資料庫模型中新增資料行，但 Views 並不知道它的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="73959-126">We've added a column in the database model, but the Views don't know about it.</span></span>

## <a name="update-views-with-model-changes"></a><span data-ttu-id="73959-127">更新具有模型變更的視圖</span><span class="sxs-lookup"><span data-stu-id="73959-127">Update Views with Model Changes</span></span>

<span data-ttu-id="73959-128">有幾種方式可以更新我們的視圖範本，以反映新的評等資料行。</span><span class="sxs-lookup"><span data-stu-id="73959-128">There are a few ways we could update our view templates to reflect the new Rating column.</span></span> <span data-ttu-id="73959-129">因為我們透過 [加入視圖] 對話方塊產生這些視圖，所以我們可以刪除它們，然後重新建立它們。</span><span class="sxs-lookup"><span data-stu-id="73959-129">Since we created these Views by generating them via the Add View dialog, we could delete them and recreate them again.</span></span> <span data-ttu-id="73959-130">不過，使用者通常已經從初始 scaffold 產生修改其 View 範本，而且想要手動新增或刪除欄位，就如同我們在建立時的 [識別碼] 欄位一樣。</span><span class="sxs-lookup"><span data-stu-id="73959-130">However, typically people will have already made modifications to their View templates from the initial scaffolded generation and will want to add or delete fields manually, just as we did with the ID field for Create.</span></span>

<span data-ttu-id="73959-131">開啟 [\Views\Movies\Index.aspx] 範本，然後將 &lt;的&gt;評等&lt;/th&gt; 新增至電影資料表的標題。</span><span class="sxs-lookup"><span data-stu-id="73959-131">Open up the \Views\Movies\Index.aspx template and add a &lt;th&gt;Rating&lt;/th&gt; to the head of the Movie table.</span></span> <span data-ttu-id="73959-132">我在內容類型後面加入了。</span><span class="sxs-lookup"><span data-stu-id="73959-132">I added mine after Genre.</span></span> <span data-ttu-id="73959-133">然後，在相同的資料行位置，但向下縮小，以輸出新的評等。</span><span class="sxs-lookup"><span data-stu-id="73959-133">Then, in the same column position but lower down, add a line to output our new Rating.</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample1.aspx)]

<span data-ttu-id="73959-134">我們最後的 Index .aspx 範本看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="73959-134">Our final Index.aspx template will look like this:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample2.aspx)]

<span data-ttu-id="73959-135">讓我們開啟 \Views\Movies\Create.aspx 範本，並為新的評等屬性新增標籤和文字方塊：</span><span class="sxs-lookup"><span data-stu-id="73959-135">Let's then open up the \Views\Movies\Create.aspx template and add a Label and Textbox for our new Rating property:</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample3.aspx)]

<span data-ttu-id="73959-136">最後的 [建立 .aspx] 範本看起來像這樣，然後讓我們將瀏覽器的標題和次要 &lt;h2&gt; 標題變更為「建立電影」，而不是在這裡！</span><span class="sxs-lookup"><span data-stu-id="73959-136">Our final Create.aspx template will look like this, and let's change our browser's title and secondary &lt;h2&gt; title to something like "Create a Movie" while we're in here!</span></span>

[!code-aspx[Main](getting-started-with-mvc-part8/samples/sample4.aspx)]

<span data-ttu-id="73959-137">執行您的應用程式，現在您已將資料庫中的新欄位新增至 [建立] 頁面。</span><span class="sxs-lookup"><span data-stu-id="73959-137">Run your app and now you've got a new field in the database that's been added to the Create page.</span></span> <span data-ttu-id="73959-138">新增電影-這次有評等，然後按一下 [建立]。</span><span class="sxs-lookup"><span data-stu-id="73959-138">Add a new Movie - this time with a Rating - and click Create.</span></span>

<span data-ttu-id="73959-139">[![建立電影-Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="73959-139">[![Create a Movie - Windows Internet Explorer](getting-started-with-mvc-part8/_static/image9.png)](getting-started-with-mvc-part8/_static/image8.png)</span></span>

<span data-ttu-id="73959-140">按一下 [建立] 之後，系統會將您傳送至 [索引] 頁面，其中會以資料庫中的新 [評等] 欄列出新電影</span><span class="sxs-lookup"><span data-stu-id="73959-140">After you click Create, you're sent to the Index page where you new Movie is listed with the new Rating Column in the database</span></span>

<span data-ttu-id="73959-141">[![電影清單-Windows Internet Explorer （12）](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="73959-141">[![Movie List - Windows Internet Explorer (12)](getting-started-with-mvc-part8/_static/image11.png)](getting-started-with-mvc-part8/_static/image10.png)</span></span>

<span data-ttu-id="73959-142">這個基本教學課程讓您開始建立控制器、將它們與 Views 產生關聯，以及傳遞硬式編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="73959-142">This basic tutorial got you started making Controllers, associating them with Views and passing around hard-coded data.</span></span> <span data-ttu-id="73959-143">然後我們建立並設計資料庫，並在其中放入一些資料。</span><span class="sxs-lookup"><span data-stu-id="73959-143">Then we created and designed a Database and put some data it in.</span></span> <span data-ttu-id="73959-144">我們已從資料庫中取出資料，並將它顯示在 HTML 資料表中。</span><span class="sxs-lookup"><span data-stu-id="73959-144">We retrieved the data from the database and displayed it in an HTML table.</span></span> <span data-ttu-id="73959-145">然後，我們加入了建立表單，讓使用者可以從 Web 應用程式中將資料加入資料庫本身。</span><span class="sxs-lookup"><span data-stu-id="73959-145">Then we added a Create form that let the user add data to the database themselves from within the Web Application.</span></span> <span data-ttu-id="73959-146">我們已新增驗證，然後進行驗證，並在用戶端上使用 JavaScript。</span><span class="sxs-lookup"><span data-stu-id="73959-146">We added validation, then made the validation use JavaScript on the client-side.</span></span> <span data-ttu-id="73959-147">最後，我們將資料庫變更為包含新的資料行，然後更新兩個頁面，以建立及顯示這項新資料。</span><span class="sxs-lookup"><span data-stu-id="73959-147">Finally, we changed the database to include a new column of data, then updated our two pages to create and display this new data.</span></span>

<span data-ttu-id="73959-148">我現在建議您移至我們的中繼層級教學課程「[MVC 音樂存放區](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)」，以及[https://asp.net/mvc](https://asp.net/mvc)的許多影片和資源，以深入瞭解 ASP.NET MVC！</span><span class="sxs-lookup"><span data-stu-id="73959-148">I now encourage you to move on to our intermediate-level tutorial "[MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)" as well as the many videos and resources at [https://asp.net/mvc](https://asp.net/mvc) to learn even more about ASP.NET MVC!</span></span>

<span data-ttu-id="73959-149">敬祝您使用愉快！</span><span class="sxs-lookup"><span data-stu-id="73959-149">Enjoy!</span></span>

- <span data-ttu-id="73959-150">Scott Hanselman-在 Twitter 上[http://hanselman.com](http://hanselman.com)和[@shanselman](http://twitter.com/shanselman) 。</span><span class="sxs-lookup"><span data-stu-id="73959-150">Scott Hanselman - [http://hanselman.com](http://hanselman.com) and [@shanselman](http://twitter.com/shanselman) on Twitter.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="73959-151">上一篇</span><span class="sxs-lookup"><span data-stu-id="73959-151">Previous</span></span>](getting-started-with-mvc-part7.md)
