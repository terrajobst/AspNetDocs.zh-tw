---
uid: mvc/overview/older-versions-1/nerddinner/create-a-database
title: 建立資料庫 | Microsoft 文件
author: microsoft
description: 步驟2顯示的步驟可讓您建立資料庫，以保存 NerdDinner 應用程式的所有晚餐和 RSVP 資料。
ms.author: riande
ms.date: 07/27/2010
ms.assetid: 983f3ffa-08b8-4868-b8c9-aa34593fc683
msc.legacyurl: /mvc/overview/older-versions-1/nerddinner/create-a-database
msc.type: authoredcontent
ms.openlocfilehash: b0aa7c8cdf741f44e09ed18e2b2f73fe6bf786ae
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581001"
---
# <a name="create-a-database"></a><span data-ttu-id="917b9-103">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="917b9-103">Create a Database</span></span>

<span data-ttu-id="917b9-104">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="917b9-104">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="917b9-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="917b9-105">Download PDF</span></span>](http://aspnetmvcbook.s3.amazonaws.com/aspnetmvc-nerdinner_v1.pdf)

> <span data-ttu-id="917b9-106">這是免費「 [NerdDinner」應用程式教學](introducing-the-nerddinner-tutorial.md)課程的步驟2，逐步解說如何使用 ASP.NET MVC 1 建立一個小型但完整的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="917b9-106">This is step 2 of a free ["NerdDinner" application tutorial](introducing-the-nerddinner-tutorial.md) that walks-through how to build a small, but complete, web application using ASP.NET MVC 1.</span></span>
> 
> <span data-ttu-id="917b9-107">步驟2顯示的步驟可讓您建立資料庫，以保存 NerdDinner 應用程式的所有晚餐和 RSVP 資料。</span><span class="sxs-lookup"><span data-stu-id="917b9-107">Step 2 shows the steps to create the database holding all of the dinner and RSVP data for our NerdDinner application.</span></span>
> 
> <span data-ttu-id="917b9-108">如果您使用 ASP.NET MVC 3，建議您遵循[使用 mvc 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md)或[mvc 音樂存放](../../older-versions/mvc-music-store/mvc-music-store-part-1.md)教學課程的消費者入門。</span><span class="sxs-lookup"><span data-stu-id="917b9-108">If you are using ASP.NET MVC 3, we recommend you follow the [Getting Started With MVC 3](../../older-versions/getting-started-with-aspnet-mvc3/cs/intro-to-aspnet-mvc-3.md) or [MVC Music Store](../../older-versions/mvc-music-store/mvc-music-store-part-1.md) tutorials.</span></span>

## <a name="nerddinner-step-2-creating-the-database"></a><span data-ttu-id="917b9-109">NerdDinner 步驟2：建立資料庫</span><span class="sxs-lookup"><span data-stu-id="917b9-109">NerdDinner Step 2: Creating the Database</span></span>

<span data-ttu-id="917b9-110">我們將使用資料庫來儲存 NerdDinner 應用程式的所有晚餐和 RSVP 資料。</span><span class="sxs-lookup"><span data-stu-id="917b9-110">We'll be using a database to store all of the Dinner and RSVP data for our NerdDinner application.</span></span>

<span data-ttu-id="917b9-111">下列步驟顯示如何使用免費的 SQL Server Express edition 來建立資料庫（您可以使用[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)的第2版輕鬆地安裝）。</span><span class="sxs-lookup"><span data-stu-id="917b9-111">The steps below show creating the database using the free SQL Server Express edition (which you can easily install using V2 of the [Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)).</span></span> <span data-ttu-id="917b9-112">我們撰寫的所有程式碼都適用于 SQL Server Express 和完整 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="917b9-112">All of the code we'll write works with both SQL Server Express and the full SQL Server.</span></span>

### <a name="creating-a-new-sql-server-express-database"></a><span data-ttu-id="917b9-113">建立新的 SQL Server Express 資料庫</span><span class="sxs-lookup"><span data-stu-id="917b9-113">Creating a new SQL Server Express database</span></span>

<span data-ttu-id="917b9-114">首先，在 Web 專案上按一下滑鼠右鍵，然後選取 [**新增-&gt;新專案**] 功能表命令：</span><span class="sxs-lookup"><span data-stu-id="917b9-114">We'll begin by right-clicking on our web project, and then select the **Add-&gt;New Item** menu command:</span></span>

![](create-a-database/_static/image1.png)

<span data-ttu-id="917b9-115">這會顯示 Visual Studio 的 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="917b9-115">This will bring up Visual Studio's "Add New Item" dialog.</span></span> <span data-ttu-id="917b9-116">我們會依 [資料] 類別篩選，並選取 [SQL Server 資料庫] 專案範本：</span><span class="sxs-lookup"><span data-stu-id="917b9-116">We'll filter by the "Data" category and select the "SQL Server Database" item template:</span></span>

![](create-a-database/_static/image2.png)

<span data-ttu-id="917b9-117">我們會將您要建立的 SQL Server Express 資料庫命名為 "NerdDinner"，然後按 [確定]。</span><span class="sxs-lookup"><span data-stu-id="917b9-117">We'll name the SQL Server Express database we want to create "NerdDinner.mdf" and hit ok.</span></span> <span data-ttu-id="917b9-118">Visual Studio 接著會詢問我們是否要將此檔案新增至我們的 \App\_Data 目錄（這是已設定為讀取和寫入安全性 Acl 的目錄）：</span><span class="sxs-lookup"><span data-stu-id="917b9-118">Visual Studio will then ask us if we want to add this file to our \App\_Data directory (which is a directory already setup with both read and write security ACLs):</span></span>

![](create-a-database/_static/image3.png)

<span data-ttu-id="917b9-119">我們將按一下 [是]，我們將會建立新的資料庫，並將其新增至我們的方案總管：</span><span class="sxs-lookup"><span data-stu-id="917b9-119">We'll click "Yes" and our new database will be created and added to our Solution Explorer:</span></span>

![](create-a-database/_static/image4.png)

### <a name="creating-tables-within-our-database"></a><span data-ttu-id="917b9-120">在我們的資料庫中建立資料表</span><span class="sxs-lookup"><span data-stu-id="917b9-120">Creating Tables within our Database</span></span>

<span data-ttu-id="917b9-121">我們現在有一個新的空白資料庫。</span><span class="sxs-lookup"><span data-stu-id="917b9-121">We now have a new empty database.</span></span> <span data-ttu-id="917b9-122">讓我們在其中新增一些資料表。</span><span class="sxs-lookup"><span data-stu-id="917b9-122">Let's add some tables to it.</span></span>

<span data-ttu-id="917b9-123">若要這麼做，我們將流覽至 Visual Studio 內的 [伺服器總管] 索引標籤視窗，讓我們管理資料庫和伺服器。</span><span class="sxs-lookup"><span data-stu-id="917b9-123">To do this we'll navigate to the "Server Explorer" tab window within Visual Studio, which enables us to manage databases and servers.</span></span> <span data-ttu-id="917b9-124">儲存在應用程式之 \App\_Data 資料夾中的 SQL Server Express 資料庫，會自動顯示在伺服器總管內。</span><span class="sxs-lookup"><span data-stu-id="917b9-124">SQL Server Express databases stored in the \App\_Data folder of our application will automatically show up within the Server Explorer.</span></span> <span data-ttu-id="917b9-125">我們可以選擇性地使用 [伺服器總管] 視窗頂端的 [連接到資料庫] 圖示，同時將額外的 SQL Server 資料庫（本機和遠端）新增至清單：</span><span class="sxs-lookup"><span data-stu-id="917b9-125">We can optionally use the "Connect to Database" icon on the top of the "Server Explorer" window to add additional SQL Server databases (both local and remote) to the list as well:</span></span>

![](create-a-database/_static/image5.png)

<span data-ttu-id="917b9-126">我們會將兩個數據表新增至我們的 NerdDinner 資料庫–一個用來儲存我們的 Dinners，另一個用來追蹤對他們的 RSVP 接受。</span><span class="sxs-lookup"><span data-stu-id="917b9-126">We will add two tables to our NerdDinner database – one to store our Dinners, and the other to track RSVP acceptances to them.</span></span> <span data-ttu-id="917b9-127">若要建立新的資料表，請以滑鼠右鍵按一下資料庫內的 [資料表] 資料夾，然後選擇 [加入新的資料表] 功能表命令：</span><span class="sxs-lookup"><span data-stu-id="917b9-127">We can create new tables by right-clicking on the "Tables" folder within our database and choosing the "Add New Table" menu command:</span></span>

![](create-a-database/_static/image6.png)

<span data-ttu-id="917b9-128">這會開啟資料表設計工具，讓我們設定資料表的架構。</span><span class="sxs-lookup"><span data-stu-id="917b9-128">This will open up a table designer that allows us to configure the schema of our table.</span></span> <span data-ttu-id="917b9-129">針對我們的「Dinners」資料表，我們將新增10個數據行：</span><span class="sxs-lookup"><span data-stu-id="917b9-129">For our "Dinners" table we will add 10 columns of data:</span></span>

![](create-a-database/_static/image7.png)

<span data-ttu-id="917b9-130">我們希望 "DinnerID" 資料行是資料表的唯一主鍵。</span><span class="sxs-lookup"><span data-stu-id="917b9-130">We want the "DinnerID" column to be a unique primary key for the table.</span></span> <span data-ttu-id="917b9-131">我們可以用滑鼠右鍵按一下 [DinnerID] 資料行，然後選擇 [設定主要金鑰] 功能表項目來進行設定：</span><span class="sxs-lookup"><span data-stu-id="917b9-131">We can configure this by right-clicking on the "DinnerID" column and choosing the "Set Primary Key" menu item:</span></span>

![](create-a-database/_static/image8.png)

<span data-ttu-id="917b9-132">除了讓 DinnerID 成為主鍵之外，我們也想要將它設定為「身分識別」資料行，其值會隨著新增至資料表的新資料列而自動遞增（這表示第一個插入的晚餐資料列將 DinnerID 為1，第二個插入的資料列的 DinnerID 為2，依此類推）。</span><span class="sxs-lookup"><span data-stu-id="917b9-132">In addition to making DinnerID a primary key, we also want configure it as an "identity" column whose value is automatically incremented as new rows of data are added to the table (meaning the first inserted Dinner row will have a DinnerID of 1, the second inserted row will have a DinnerID of 2, etc).</span></span>

<span data-ttu-id="917b9-133">我們可以選取 [DinnerID] 資料行來執行這項操作，然後使用 [資料行屬性] 編輯器，將資料行上的 [（是識別）] 屬性設定為 [是]。</span><span class="sxs-lookup"><span data-stu-id="917b9-133">We can do this by selecting the "DinnerID" column and then use the "Column Properties" editor to set the "(Is Identity)" property on the column to "Yes".</span></span> <span data-ttu-id="917b9-134">我們將使用標準身分識別預設值（從1開始，並在每個新的晚餐資料列遞增1）：</span><span class="sxs-lookup"><span data-stu-id="917b9-134">We will use the standard identity defaults (start at 1 and increment 1 on each new Dinner row):</span></span>

![](create-a-database/_static/image9.png)

<span data-ttu-id="917b9-135">接著，我們會輸入 Ctrl-S 或使用檔案&gt;的 [**儲存**] 功能表命令來儲存資料表。</span><span class="sxs-lookup"><span data-stu-id="917b9-135">We'll then save our table by typing Ctrl-S or by using the **File-&gt;Save** menu command.</span></span> <span data-ttu-id="917b9-136">這會提示我們將資料表命名為。</span><span class="sxs-lookup"><span data-stu-id="917b9-136">This will prompt us to name the table.</span></span> <span data-ttu-id="917b9-137">我們會將它命名為 "Dinners"：</span><span class="sxs-lookup"><span data-stu-id="917b9-137">We'll name it "Dinners":</span></span>

![](create-a-database/_static/image10.png)

<span data-ttu-id="917b9-138">我們的新 Dinners 資料表就會顯示在伺服器 explorer 的資料庫中。</span><span class="sxs-lookup"><span data-stu-id="917b9-138">Our new Dinners table will then show up within our database in the server explorer.</span></span>

<span data-ttu-id="917b9-139">接著，我們會重複上述步驟，並建立「RSVP」資料表。</span><span class="sxs-lookup"><span data-stu-id="917b9-139">We'll then repeat the above steps and create a "RSVP" table.</span></span> <span data-ttu-id="917b9-140">具有3個數據行的這個資料表。</span><span class="sxs-lookup"><span data-stu-id="917b9-140">This table with have 3 columns.</span></span> <span data-ttu-id="917b9-141">我們會將 RsvpID 資料行設定為主要金鑰，並將它設為識別欄位：</span><span class="sxs-lookup"><span data-stu-id="917b9-141">We will setup the RsvpID column as the primary key, and also make it an identity column:</span></span>

![](create-a-database/_static/image11.png)

<span data-ttu-id="917b9-142">我們會儲存它，並將它命名為「RSVP」。</span><span class="sxs-lookup"><span data-stu-id="917b9-142">We'll save it and give it the name "RSVP".</span></span>

### <a name="setting-up-a-foreign-key-relationship-between-tables"></a><span data-ttu-id="917b9-143">設定資料表之間的外鍵關聯性</span><span class="sxs-lookup"><span data-stu-id="917b9-143">Setting up a Foreign Key Relationship between Tables</span></span>

<span data-ttu-id="917b9-144">我們的資料庫中現在有兩個數據表。</span><span class="sxs-lookup"><span data-stu-id="917b9-144">We now have two tables within our database.</span></span> <span data-ttu-id="917b9-145">我們的最後一個架構設計步驟是在這兩個數據表之間設定「一對多」關聯性，讓我們可以將每個晚餐資料列與套用至該資料的零或多個 RSVP 資料列產生關聯。</span><span class="sxs-lookup"><span data-stu-id="917b9-145">Our last schema design step will be to setup a "one-to-many" relationship between these two tables – so that we can associate each Dinner row with zero or more RSVP rows that apply to it.</span></span> <span data-ttu-id="917b9-146">我們會將 RSVP 資料表的「DinnerID」資料行設定為與「Dinners」資料表中的「DinnerID」資料行具有外鍵關聯性，以達到此目的。</span><span class="sxs-lookup"><span data-stu-id="917b9-146">We will do this by configuring the RSVP table's "DinnerID" column to have a foreign-key relationship to the "DinnerID" column in the "Dinners" table.</span></span>

<span data-ttu-id="917b9-147">若要這麼做，我們要在 [資料表設計工具] 中按兩下 [RSVP] 資料表，方法是在 [伺服器瀏覽器] 中按兩下它。</span><span class="sxs-lookup"><span data-stu-id="917b9-147">To do this we'll open up the RSVP table within the table designer by double-clicking it in the server explorer.</span></span> <span data-ttu-id="917b9-148">然後選取其中的 "DinnerID" 資料行，按一下滑鼠右鍵，然後選擇 [關聯性 ...]內容功能表命令：</span><span class="sxs-lookup"><span data-stu-id="917b9-148">We'll then select the "DinnerID" column within it, right-click, and choose the "Relationships…" context menu command:</span></span>

![](create-a-database/_static/image12.png)

<span data-ttu-id="917b9-149">這會出現一個對話方塊，可讓我們用來設定資料表之間的關聯性：</span><span class="sxs-lookup"><span data-stu-id="917b9-149">This will bring up a dialog that we can use to setup relationships between tables:</span></span>

![](create-a-database/_static/image13.png)

<span data-ttu-id="917b9-150">我們將按一下 [新增] 按鈕，將新的關聯性新增至對話方塊。</span><span class="sxs-lookup"><span data-stu-id="917b9-150">We'll click the "Add" button to add a new relationship to the dialog.</span></span> <span data-ttu-id="917b9-151">加入關聯性之後，我們會在對話方塊右邊的屬性方格中展開 [資料表和資料行規格] 樹狀檢視節點，然後按一下 [...]按鈕的右邊：</span><span class="sxs-lookup"><span data-stu-id="917b9-151">Once a relationship has been added, we'll expand the "Tables and Column Specification" tree-view node within the property grid to the right of the dialog, and then click the "…" button to the right of it:</span></span>

![](create-a-database/_static/image14.png)

<span data-ttu-id="917b9-152">按一下 [...]按鈕會顯示另一個對話方塊，讓我們指定關聯性中涉及的資料表和資料行，以及讓我們命名關聯性。</span><span class="sxs-lookup"><span data-stu-id="917b9-152">Clicking the "…" button will bring up another dialog that allows us to specify which tables and columns are involved in the relationship, as well as allow us to name the relationship.</span></span>

<span data-ttu-id="917b9-153">我們會將主鍵資料表變更為 "Dinners"，並選取 Dinners 資料表內的 "DinnerID" 資料行作為主鍵。</span><span class="sxs-lookup"><span data-stu-id="917b9-153">We will change the Primary Key Table to be "Dinners", and select the "DinnerID" column within the Dinners table as the primary key.</span></span> <span data-ttu-id="917b9-154">我們的「RSVP」資料表會是外鍵資料表和「RSVP」。DinnerID 資料行會與外鍵建立關聯：</span><span class="sxs-lookup"><span data-stu-id="917b9-154">Our RSVP table will be the foreign-key table, and the RSVP.DinnerID column will be associated as the foreign-key:</span></span>

![](create-a-database/_static/image15.png)

<span data-ttu-id="917b9-155">此時，RSVP 資料表中的每個資料列都會與晚餐表中的資料列相關聯。</span><span class="sxs-lookup"><span data-stu-id="917b9-155">Now each row in the RSVP table will be associated with a row in the Dinner table.</span></span> <span data-ttu-id="917b9-156">SQL Server 會為我們維護參考完整性-如果未指向有效的晚餐資料列，則會防止我們新增新的 RSVP 資料列。</span><span class="sxs-lookup"><span data-stu-id="917b9-156">SQL Server will maintain referential integrity for us – and prevent us from adding a new RSVP row if it does not point to a valid Dinner row.</span></span> <span data-ttu-id="917b9-157">如果仍有 RSVP 資料列參考資料列，也會導致我們無法刪除晚餐資料列。</span><span class="sxs-lookup"><span data-stu-id="917b9-157">It will also prevent us from deleting a Dinner row if there are still RSVP rows referring to it.</span></span>

### <a name="adding-data-to-our-tables"></a><span data-ttu-id="917b9-158">將資料加入我們的資料表</span><span class="sxs-lookup"><span data-stu-id="917b9-158">Adding Data to our Tables</span></span>

<span data-ttu-id="917b9-159">讓我們透過將一些範例資料新增至我們的 Dinners 資料表來完成。</span><span class="sxs-lookup"><span data-stu-id="917b9-159">Let's finish by adding some sample data to our Dinners table.</span></span> <span data-ttu-id="917b9-160">我們可以在 [伺服器總管] 中以滑鼠右鍵按一下資料表，然後選擇 [顯示資料表資料] 命令，將資料新增至資料表：</span><span class="sxs-lookup"><span data-stu-id="917b9-160">We can add data to a table by right-clicking on it within the Server Explorer and choosing the "Show Table Data" command:</span></span>

![](create-a-database/_static/image16.png)

<span data-ttu-id="917b9-161">我們會新增幾個資料列，供我們稍後開始執行應用程式時使用：</span><span class="sxs-lookup"><span data-stu-id="917b9-161">We'll add a few rows of Dinner data that we can use later as we start implementing the application:</span></span>

![](create-a-database/_static/image17.png)

### <a name="next-step"></a><span data-ttu-id="917b9-162">後續步驟</span><span class="sxs-lookup"><span data-stu-id="917b9-162">Next Step</span></span>

<span data-ttu-id="917b9-163">我們已完成資料庫的建立。</span><span class="sxs-lookup"><span data-stu-id="917b9-163">We've finished creating our database.</span></span> <span data-ttu-id="917b9-164">現在讓我們建立可用來查詢和更新的模型類別。</span><span class="sxs-lookup"><span data-stu-id="917b9-164">Let's now create model classes that we can use to query and update it.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="917b9-165">[上一頁](create-a-new-aspnet-mvc-project.md)
> [下一頁](build-a-model-with-business-rule-validations.md)</span><span class="sxs-lookup"><span data-stu-id="917b9-165">[Previous](create-a-new-aspnet-mvc-project.md)
[Next](build-a-model-with-business-rule-validations.md)</span></span>
