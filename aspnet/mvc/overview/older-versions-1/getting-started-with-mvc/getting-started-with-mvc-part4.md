---
uid: mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
title: 建立資料庫 |Microsoft Docs
author: shanselman
description: 這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。 建立可從資料庫讀取和寫入的簡單 web 應用程式。
ms.author: riande
ms.date: 08/14/2010
ms.assetid: 742df67f-484d-4ef3-af6b-8c791e556b43
msc.legacyurl: /mvc/overview/older-versions-1/getting-started-with-mvc/getting-started-with-mvc-part4
msc.type: authoredcontent
ms.openlocfilehash: 995db714ce6365415d06dc458aee84a31c7c8fd6
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581435"
---
# <a name="creating-a-database"></a><span data-ttu-id="22a5b-104">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="22a5b-104">Creating a Database</span></span>

<span data-ttu-id="22a5b-105">由[Scott Hanselman](https://github.com/shanselman)</span><span class="sxs-lookup"><span data-stu-id="22a5b-105">by [Scott Hanselman](https://github.com/shanselman)</span></span>

> <span data-ttu-id="22a5b-106">這是初學者教學課程，介紹 ASP.NET MVC 的基本概念。</span><span class="sxs-lookup"><span data-stu-id="22a5b-106">This is a beginner tutorial that introduces the basics of ASP.NET MVC.</span></span> <span data-ttu-id="22a5b-107">您將建立可從資料庫讀取和寫入的簡單 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22a5b-107">You'll create a simple web application that reads and writes from a database.</span></span> <span data-ttu-id="22a5b-108">請造訪[ASP.NET mvc 學習中心](../../../index.md)，以尋找其他 ASP.NET mvc 教學課程和範例。</span><span class="sxs-lookup"><span data-stu-id="22a5b-108">Visit the [ASP.NET MVC learning center](../../../index.md) to find other ASP.NET MVC tutorials and samples.</span></span>

<span data-ttu-id="22a5b-109">在本節中，我們將建立新的 SQL Express 資料庫，我們將用它來儲存和抓取電影資料。</span><span class="sxs-lookup"><span data-stu-id="22a5b-109">In this section we are going to create a new SQL Express database that we'll use to store and retrieve our movie data.</span></span> <span data-ttu-id="22a5b-110">從 Visual Web Developer IDE 中，選取 [View] |伺服器總管。</span><span class="sxs-lookup"><span data-stu-id="22a5b-110">From within the Visual Web Developer IDE, select View | Server Explorer.</span></span> <span data-ttu-id="22a5b-111">以滑鼠右鍵按一下 [資料連線]，然後按一下 [新增連接 ...]</span><span class="sxs-lookup"><span data-stu-id="22a5b-111">Right click on Data Connections and click Add Connection...</span></span>

![AddConnection](getting-started-with-mvc-part4/_static/image1.png)

<span data-ttu-id="22a5b-113">在 [選擇資料來源] 對話方塊中，選取 Microsoft SQL Server，然後選取 [繼續]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-113">In the Choose Data Source dialog, select Microsoft SQL Server and select Continue.</span></span>

![](getting-started-with-mvc-part4/_static/image2.png)

<span data-ttu-id="22a5b-114">在 [新增連線] 對話方塊中，為您的伺服器名稱輸入 ".\SQLEXPRESS"，並輸入「電影」作為新資料庫的名稱。</span><span class="sxs-lookup"><span data-stu-id="22a5b-114">In the Add Connection dialog, enter ".\SQLEXPRESS" for your Server Name, and enter "Movies" as the name for your new database.</span></span>

<span data-ttu-id="22a5b-115">[![新增連接 對話方塊](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-115">[![Add Connection dialog](getting-started-with-mvc-part4/_static/image4.png)](getting-started-with-mvc-part4/_static/image3.png)</span></span>

<span data-ttu-id="22a5b-116">按一下 [確定]，系統會詢問您是否要建立該資料庫。</span><span class="sxs-lookup"><span data-stu-id="22a5b-116">Click OK and you'll be asked if you want to create that database.</span></span> <span data-ttu-id="22a5b-117">選取 [是]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-117">Select yes.</span></span>

<span data-ttu-id="22a5b-118">[![建立電影嗎？](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-118">[![Create Movies?](getting-started-with-mvc-part4/_static/image6.png)](getting-started-with-mvc-part4/_static/image5.png)</span></span>

<span data-ttu-id="22a5b-119">現在您已在伺服器總管中找到空的資料庫。</span><span class="sxs-lookup"><span data-stu-id="22a5b-119">Now you've got an empty database in Server Explorer.</span></span>

![加入新的資料表](getting-started-with-mvc-part4/_static/image7.png)

<span data-ttu-id="22a5b-121">以滑鼠右鍵按一下 [資料表]，然後按一下 [加入資料表]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-121">Right click on Tables and click Add Table.</span></span> <span data-ttu-id="22a5b-122">資料表設計工具將會出現。</span><span class="sxs-lookup"><span data-stu-id="22a5b-122">The Table Designer will appear.</span></span> <span data-ttu-id="22a5b-123">新增 Id、Title、ReleaseDate、內容類型和價格的資料行。</span><span class="sxs-lookup"><span data-stu-id="22a5b-123">Add columns for Id, Title, ReleaseDate, Genre, and Price.</span></span> <span data-ttu-id="22a5b-124">以滑鼠右鍵按一下 [ID] 資料行，然後按一下 [設定主要金鑰]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-124">Right click on the ID column and click set Primary Key.</span></span> <span data-ttu-id="22a5b-125">我的設計區域看起來像這樣。</span><span class="sxs-lookup"><span data-stu-id="22a5b-125">Here's what my design areas looks like.</span></span>

<span data-ttu-id="22a5b-126">[![資料庫資料表編輯器](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-126">[![Database Table Editor](getting-started-with-mvc-part4/_static/image9.png)](getting-started-with-mvc-part4/_static/image8.png)</span></span>

<span data-ttu-id="22a5b-127">此外，請選取 [識別碼] 資料行，然後在 [資料行屬性] 下方，將 [識別規格] 變更為 [是]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-127">Also, select the Id column and under Column Properties below change "Identity Specification" to "Yes."</span></span>

<span data-ttu-id="22a5b-128">[![IsIdentity-資料行屬性](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-128">[![IsIdentity - Column Properties](getting-started-with-mvc-part4/_static/image11.png)](getting-started-with-mvc-part4/_static/image10.png)</span></span>

<span data-ttu-id="22a5b-129">當您完成時，請按一下工具列中的 [儲存] 圖示，或選取 [檔案] |從功能表中儲存，並將您的資料表命名為「**電影**」（單數）。</span><span class="sxs-lookup"><span data-stu-id="22a5b-129">When you've got it done, click the Save icon in the toolbar or select File | Save from the menu, and name your table "**Movie**" (singular).</span></span> <span data-ttu-id="22a5b-130">我們擁有資料庫和資料表！</span><span class="sxs-lookup"><span data-stu-id="22a5b-130">We've got a database and a table!</span></span>

<span data-ttu-id="22a5b-131">[![選擇名稱](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-131">[![Choose Name](getting-started-with-mvc-part4/_static/image13.png)](getting-started-with-mvc-part4/_static/image12.png)</span></span>

<span data-ttu-id="22a5b-132">返回伺服器總管，以滑鼠右鍵按一下 [電影] 資料表，然後選取 [顯示資料表資料]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-132">Go back to Server Explorer and right click the Movie table, then select "Show Table Data."</span></span> <span data-ttu-id="22a5b-133">輸入一些電影，讓我們的資料庫有一些資料。</span><span class="sxs-lookup"><span data-stu-id="22a5b-133">Enter a few movies so our database has some data.</span></span>

<span data-ttu-id="22a5b-134">[![資料庫資料表編輯](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-134">[![Database Table Editing](getting-started-with-mvc-part4/_static/image15.png)](getting-started-with-mvc-part4/_static/image14.png)</span></span>

## <a name="creating-a-model"></a><span data-ttu-id="22a5b-135">建立模型</span><span class="sxs-lookup"><span data-stu-id="22a5b-135">Creating a Model</span></span>

<span data-ttu-id="22a5b-136">現在，切換回 IDE 右側的 [方案總管]，並以滑鼠右鍵按一下 [模型] 資料夾，然後選取 [新增] |新專案。</span><span class="sxs-lookup"><span data-stu-id="22a5b-136">Now, switch back to the Solution Explorer on the right hand side of the IDE and right-click on the Models folder and select Add | New Item.</span></span>

<span data-ttu-id="22a5b-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-137">[![addnewmodelitem](getting-started-with-mvc-part4/_static/image17.png)](getting-started-with-mvc-part4/_static/image16.png)</span></span>

<span data-ttu-id="22a5b-138">我們即將從新的資料庫建立實體模型。</span><span class="sxs-lookup"><span data-stu-id="22a5b-138">We're going to create an Entity Model from our new database.</span></span> <span data-ttu-id="22a5b-139">這會在專案中加入一組類別，讓我們能夠輕鬆地查詢和運算元據庫內的資料。</span><span class="sxs-lookup"><span data-stu-id="22a5b-139">This will add a set of classes to our project that makes it easy for us to query and manipulate the data within our database.</span></span> <span data-ttu-id="22a5b-140">選取對話方塊左側的 [資料] 節點，然後選取 [ADO.NET 實體資料模型專案] 範本。</span><span class="sxs-lookup"><span data-stu-id="22a5b-140">Select the Data node on the left-hand side of the dialog, and then select the ADO.NET Entity Data Model item template.</span></span> <span data-ttu-id="22a5b-141">將它命名為 [電影 .edmx]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-141">Name it Movies.edmx.</span></span>

<span data-ttu-id="22a5b-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-142">[![AddNewDataModel](getting-started-with-mvc-part4/_static/image19.png)](getting-started-with-mvc-part4/_static/image18.png)</span></span>

<span data-ttu-id="22a5b-143">按一下 [新增] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22a5b-143">Click the "Add" button.</span></span> <span data-ttu-id="22a5b-144">這會啟動「實體資料模型 Wizard」。</span><span class="sxs-lookup"><span data-stu-id="22a5b-144">This will then launch the "Entity Data Model Wizard".</span></span>

<span data-ttu-id="22a5b-145">在彈出的新對話方塊中，選取 [從資料庫產生]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-145">In the new dialog that pops up, select Generate from Database.</span></span> <span data-ttu-id="22a5b-146">因為我們剛剛建立了資料庫，所以只需要告訴 Entity Framework 新資料庫及其資料表的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="22a5b-146">Since we've just made a database, we'll only need to tell the Entity Framework about our new database and its table.</span></span> <span data-ttu-id="22a5b-147">按 [下一步]，在 web 應用程式的設定中儲存我們的資料庫連接。</span><span class="sxs-lookup"><span data-stu-id="22a5b-147">Click Next to save our database connection in our web application's configuration.</span></span> <span data-ttu-id="22a5b-148">現在，勾選 [資料表和電影] 核取方塊，然後按一下 [完成]。</span><span class="sxs-lookup"><span data-stu-id="22a5b-148">Now, check the Tables and Movie checkbox and click Finish.</span></span>

<span data-ttu-id="22a5b-149">[![實體資料模型 Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-149">[![Entity Data Model Wizard](getting-started-with-mvc-part4/_static/image21.png)](getting-started-with-mvc-part4/_static/image20.png)</span></span>

<span data-ttu-id="22a5b-150">現在，我們可以在 Entity Framework Designer 中看到新的電影資料表，並從程式碼進行存取。</span><span class="sxs-lookup"><span data-stu-id="22a5b-150">Now we can see our new Movie table in the Entity Framework Designer and access it from code.</span></span>

<span data-ttu-id="22a5b-151">[![電影-Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span><span class="sxs-lookup"><span data-stu-id="22a5b-151">[![Movies - Microsoft Visual Web Developer 2010 Express](getting-started-with-mvc-part4/_static/image23.png)](getting-started-with-mvc-part4/_static/image22.png)</span></span>

<span data-ttu-id="22a5b-152">在設計介面上，您可以看到「電影」類別。</span><span class="sxs-lookup"><span data-stu-id="22a5b-152">On the design surface you can see a "Movie" class.</span></span> <span data-ttu-id="22a5b-153">這個類別會對應至資料庫中的「電影」資料表，而其中的每個屬性會對應至具有資料表的資料行。</span><span class="sxs-lookup"><span data-stu-id="22a5b-153">This class maps to the "Movie" table in our database, and each property within it maps to a column with the table.</span></span> <span data-ttu-id="22a5b-154">「電影」類別的每個實例都會對應到「電影」資料表中的一個資料列。</span><span class="sxs-lookup"><span data-stu-id="22a5b-154">Each instance of a "Movie" class will correspond to a row within the "Movie" table.</span></span>

<span data-ttu-id="22a5b-155">如果您不喜歡 Entity Framework 所使用的預設命名和對應慣例，可以使用 Entity Framework 設計工具來變更或自訂它們。</span><span class="sxs-lookup"><span data-stu-id="22a5b-155">If you don't like the default naming and mapping conventions used by the Entity Framework, you can use the Entity Framework designer to change or customize them.</span></span> <span data-ttu-id="22a5b-156">在此應用程式中，我們將使用預設值，並直接依自己的方式儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="22a5b-156">For this application we'll use the defaults and just save the file as-is.</span></span>

<span data-ttu-id="22a5b-157">現在，讓我們來處理一些實際資料！</span><span class="sxs-lookup"><span data-stu-id="22a5b-157">Now, let's work with some real data!</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="22a5b-158">[上一頁](getting-started-with-mvc-part3.md)
> [下一頁](getting-started-with-mvc-part5.md)</span><span class="sxs-lookup"><span data-stu-id="22a5b-158">[Previous](getting-started-with-mvc-part3.md)
[Next](getting-started-with-mvc-part5.md)</span></span>
