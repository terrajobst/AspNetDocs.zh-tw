---
uid: web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
title: ASP.NET Web Pages 簡介-顯示資料 |Microsoft Docs
author: Rick-Anderson
description: 本教學課程說明如何在 WebMatrix 中建立資料庫，以及當您使用 ASP.NET Web Pages （Razor）時，如何在頁面中顯示資料庫資料。 它假設 y 。
ms.author: riande
ms.date: 05/28/2015
ms.assetid: b3a006a0-3ea2-4d45-b833-e20e3a3c0a1a
msc.legacyurl: /web-pages/overview/getting-started/introducing-aspnet-web-pages-2/displaying-data
msc.type: authoredcontent
ms.openlocfilehash: 9e665ca8dd064c23a8b8bd3593014969d0c3da48
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78525218"
---
# <a name="introducing-aspnet-web-pages---displaying-data"></a><span data-ttu-id="34c04-104">簡介 ASP.NET Web Pages-顯示資料</span><span class="sxs-lookup"><span data-stu-id="34c04-104">Introducing ASP.NET Web Pages - Displaying Data</span></span>

<span data-ttu-id="34c04-105">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="34c04-105">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="34c04-106">本教學課程說明如何在 WebMatrix 中建立資料庫，以及當您使用 ASP.NET Web Pages （Razor）時，如何在頁面中顯示資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-106">This tutorial shows you how to create a database in WebMatrix and how to display database data in a page when you use ASP.NET Web Pages (Razor).</span></span> <span data-ttu-id="34c04-107">它假設您已完成[ASP.NET Web Pages 程式設計簡介](../introducing-razor-syntax-c.md)的系列。</span><span class="sxs-lookup"><span data-stu-id="34c04-107">It assumes you have completed the series through [Introduction to ASP.NET Web Pages Programming](../introducing-razor-syntax-c.md).</span></span>
> 
> <span data-ttu-id="34c04-108">您將學到什麼：</span><span class="sxs-lookup"><span data-stu-id="34c04-108">What you'll learn:</span></span>
> 
> - <span data-ttu-id="34c04-109">如何使用 WebMatrix 工具來建立資料庫和資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="34c04-109">How to use WebMatrix tools to create a database and database tables.</span></span>
> - <span data-ttu-id="34c04-110">如何使用 WebMatrix 工具將資料新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="34c04-110">How to use WebMatrix tools to add data to a database.</span></span>
> - <span data-ttu-id="34c04-111">如何在頁面上顯示資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-111">How to display data from the database on a page.</span></span>
> - <span data-ttu-id="34c04-112">如何在 ASP.NET Web Pages 中執行 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="34c04-112">How to run SQL commands in ASP.NET Web Pages.</span></span>
> - <span data-ttu-id="34c04-113">如何自訂 `WebGrid` helper 來變更資料顯示，以及新增分頁和排序。</span><span class="sxs-lookup"><span data-stu-id="34c04-113">How to customize the `WebGrid` helper to change the data display and to add paging and sorting.</span></span>
>   
> 
> <span data-ttu-id="34c04-114">討論的功能/技術：</span><span class="sxs-lookup"><span data-stu-id="34c04-114">Features/technologies discussed:</span></span>
> 
> - <span data-ttu-id="34c04-115">WebMatrix 資料庫工具。</span><span class="sxs-lookup"><span data-stu-id="34c04-115">WebMatrix database tools.</span></span>
> - <span data-ttu-id="34c04-116">`WebGrid` helper。</span><span class="sxs-lookup"><span data-stu-id="34c04-116">`WebGrid` helper.</span></span>

## <a name="what-youll-build"></a><span data-ttu-id="34c04-117">您要建置的內容</span><span class="sxs-lookup"><span data-stu-id="34c04-117">What You'll Build</span></span>

<span data-ttu-id="34c04-118">在上一個教學課程中，您已介紹 ASP.NET Web Pages （*cshtml*檔案）、Razor 語法的基本概念，以及協助程式。</span><span class="sxs-lookup"><span data-stu-id="34c04-118">In the previous tutorial, you were introduced to ASP.NET Web Pages (*.cshtml* files), to the basics of Razor syntax, and to helpers.</span></span> <span data-ttu-id="34c04-119">在本教學課程中，您將開始建立將用於該系列其餘部分的實際 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="34c04-119">In this tutorial, you'll begin creating the actual web application that you'll use for the rest of the series.</span></span> <span data-ttu-id="34c04-120">應用程式是簡單的電影應用程式，可讓您查看、新增、變更及刪除電影的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="34c04-120">The app is a simple movie application that lets you view, add, change, and delete information about movies.</span></span>

<span data-ttu-id="34c04-121">當您完成本教學課程時，您將能夠看到看起來像此頁面的電影清單：</span><span class="sxs-lookup"><span data-stu-id="34c04-121">When you're done with this tutorial, you'll be able to view a movie listing that looks like this page:</span></span>

![WebGrid 顯示，其中包含設定為 CSS 類別名稱的參數](displaying-data/_static/image1.png)

<span data-ttu-id="34c04-123">但若要開始，您必須建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="34c04-123">But to begin, you have to create a database.</span></span>

## <a name="a-very-brief-introduction-to-databases"></a><span data-ttu-id="34c04-124">資料庫的簡要簡介</span><span class="sxs-lookup"><span data-stu-id="34c04-124">A Very Brief Introduction to Databases</span></span>

<span data-ttu-id="34c04-125">本教學課程只會提供資料庫的 briefest 簡介。</span><span class="sxs-lookup"><span data-stu-id="34c04-125">This tutorial will provide only the briefest introduction to databases.</span></span> <span data-ttu-id="34c04-126">如果您有資料庫經驗，可以略過這個簡短的小節。</span><span class="sxs-lookup"><span data-stu-id="34c04-126">If you have database experience, you can skip this short section.</span></span>

<span data-ttu-id="34c04-127">資料庫包含一個或多個資料表，其中包含 &mdash; 的資訊，例如客戶、訂單和廠商的資料表，或是學生、老師、班級和成績。</span><span class="sxs-lookup"><span data-stu-id="34c04-127">A database contains one or more tables that contain information &mdash; for example, tables for customers, orders, and vendors, or for students, teachers, classes, and grades.</span></span> <span data-ttu-id="34c04-128">就結構而言，資料庫資料表就像是試算表。</span><span class="sxs-lookup"><span data-stu-id="34c04-128">Structurally, a database table is like a spreadsheet.</span></span> <span data-ttu-id="34c04-129">想像一下一般通訊錄。</span><span class="sxs-lookup"><span data-stu-id="34c04-129">Imagine a typical address book.</span></span> <span data-ttu-id="34c04-130">針對通訊錄中的每個專案（亦即，針對每個人），您會有數個資訊片段，例如名字、姓氏、位址、電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="34c04-130">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

![當做簡單方格的範例資料庫資料表](displaying-data/_static/image2.png)

<span data-ttu-id="34c04-132">（資料列有時稱為「*記錄*」，而資料行有時稱為「*欄位*」）。</span><span class="sxs-lookup"><span data-stu-id="34c04-132">(Rows are sometimes referred to as *records*, and columns are sometimes referred to as *fields*.)</span></span>

<span data-ttu-id="34c04-133">對於大部分的資料庫資料表而言，資料表必須有一個包含唯一值的資料行，例如客戶編碼、帳戶號碼等等。</span><span class="sxs-lookup"><span data-stu-id="34c04-133">For most database tables, the table has to have a column that contains a unique value, like a customer number, account number, and so on.</span></span> <span data-ttu-id="34c04-134">這個值稱為資料表的*主鍵*，您可以用它來識別資料表中的每個資料列。</span><span class="sxs-lookup"><span data-stu-id="34c04-134">This value is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="34c04-135">在此範例中，ID 資料行是上一個範例中所顯示通訊錄的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="34c04-135">In the example, the ID column is the primary key for the address book shown in the previous example.</span></span>

<span data-ttu-id="34c04-136">您在 web 應用程式中所做的大部分工作，都包含從資料庫讀取資訊，並將它顯示在頁面上。</span><span class="sxs-lookup"><span data-stu-id="34c04-136">Much of the work you do in web applications consists of reading information out of the database and displaying it on a page.</span></span> <span data-ttu-id="34c04-137">您也經常會收集使用者的資訊，並將其新增至資料庫，或是修改已在資料庫中的記錄。</span><span class="sxs-lookup"><span data-stu-id="34c04-137">You'll also often gather information from users and add it to a database, or you'll modify records that are already in the database.</span></span> <span data-ttu-id="34c04-138">（我們將在本教學課程設定的過程中涵蓋所有這些作業）。</span><span class="sxs-lookup"><span data-stu-id="34c04-138">(We'll cover all of these operations in the course of this tutorial set.)</span></span>

<span data-ttu-id="34c04-139">資料庫工作的大幅很複雜，而且可能需要專門知識。</span><span class="sxs-lookup"><span data-stu-id="34c04-139">Database work can be enormously complex and can require specialized knowledge.</span></span> <span data-ttu-id="34c04-140">不過，在本教學課程中，您必須只瞭解基本概念，這一切都將在您走時說明。</span><span class="sxs-lookup"><span data-stu-id="34c04-140">For this tutorial set, though, you have to understand only basic concepts, which will all be explained as you go.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="34c04-141">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="34c04-141">Creating a Database</span></span>

<span data-ttu-id="34c04-142">WebMatrix 所包含的工具可讓您輕鬆地建立資料庫，並在資料庫中建立資料表。</span><span class="sxs-lookup"><span data-stu-id="34c04-142">WebMatrix includes tools that make it easy to create a database and to create tables in the database.</span></span> <span data-ttu-id="34c04-143">（資料庫的結構稱為資料庫的*架構*）。在此教學課程中，您將建立一個資料庫，其中只有一個資料表 &mdash; 電影。</span><span class="sxs-lookup"><span data-stu-id="34c04-143">(The structure of a database is referred to as the database's *schema*.) For this tutorial set, you'll create a database that has only one table in it &mdash; Movies.</span></span>

<span data-ttu-id="34c04-144">開啟 WebMatrix （如果您尚未這麼做），並開啟您在上一個教學課程中建立的 WebPagesMovies 網站。</span><span class="sxs-lookup"><span data-stu-id="34c04-144">Open WebMatrix if you haven't already done so, and open the WebPagesMovies site that you created in the previous tutorial.</span></span>

<span data-ttu-id="34c04-145">在左窗格中，按一下 [**資料庫**] 工作區。</span><span class="sxs-lookup"><span data-stu-id="34c04-145">In the left pane, click the **Database** workspace.</span></span>

![WebMatrix 資料庫工作區索引標籤](displaying-data/_static/image3.png)

<span data-ttu-id="34c04-147">功能區會變更以顯示資料庫相關工作。</span><span class="sxs-lookup"><span data-stu-id="34c04-147">The ribbon changes to show database-related tasks.</span></span> <span data-ttu-id="34c04-148">在功能區中，按一下 [**新增資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="34c04-148">In the ribbon, click **New Database**.</span></span>

![WebMatrix 功能區中的 [新增資料庫] 按鈕](displaying-data/_static/image4.png)

<span data-ttu-id="34c04-150">WebMatrix 會建立與您的網站 &mdash; *WebPagesMovies*同名的 SQL Server CE 資料庫（ *.sdf*檔案）。</span><span class="sxs-lookup"><span data-stu-id="34c04-150">WebMatrix creates a SQL Server CE database (an *.sdf* file) that has the same name as your site &mdash; *WebPagesMovies.sdf*.</span></span> <span data-ttu-id="34c04-151">（您不會在這裡執行此動作，但您可以將檔案重新命名為任何您喜歡的專案，只要它的副檔名為 *.sdf*即可）。</span><span class="sxs-lookup"><span data-stu-id="34c04-151">(You won't do this here, but you can rename the file to anything you like, as long as it has an *.sdf* extension.)</span></span>

## <a name="creating-a-table"></a><span data-ttu-id="34c04-152">建立資料表</span><span class="sxs-lookup"><span data-stu-id="34c04-152">Creating a Table</span></span>

<span data-ttu-id="34c04-153">在功能區中，按一下 [**新增資料表**]。</span><span class="sxs-lookup"><span data-stu-id="34c04-153">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="34c04-154">WebMatrix 會在新的索引標籤中開啟 [資料表設計工具] （如果無法使用 [新增資料表] 選項，請確定已在左側樹狀檢視中選取新的資料庫）。</span><span class="sxs-lookup"><span data-stu-id="34c04-154">WebMatrix opens the table designer in a new tab. (If the New Table option isn't available, make sure that the new database is selected in the tree view on the left.)</span></span>

![WebMatrix 功能區中的 [新增資料表] 按鈕](displaying-data/_static/image5.png)

<span data-ttu-id="34c04-156">在頂端的文字方塊中（浮水印會顯示為「輸入資料表名稱」），輸入「電影」。</span><span class="sxs-lookup"><span data-stu-id="34c04-156">In the text box at the top (where the watermark says "Enter table name"), enter "Movies".</span></span>

![在 WebMatrix 資料庫設計工具中輸入資料表名稱](displaying-data/_static/image6.png)

<span data-ttu-id="34c04-158">資料表名稱底下的窗格是您定義個別資料行的位置。</span><span class="sxs-lookup"><span data-stu-id="34c04-158">The pane underneath the table name is where you define individual columns.</span></span> <span data-ttu-id="34c04-159">針對本教學課程中的*電影*資料表，您只會建立幾個資料行： *ID*、 *Title* *、內容*類型和*年份*。</span><span class="sxs-lookup"><span data-stu-id="34c04-159">For the *Movies* table in this tutorial, you'll create only a few columns: *ID*, *Title*, *Genre*, and *Year*.</span></span>

<span data-ttu-id="34c04-160">在 [**名稱**] 方塊中，輸入 "ID"。</span><span class="sxs-lookup"><span data-stu-id="34c04-160">In the **Name** box, enter "ID".</span></span> <span data-ttu-id="34c04-161">在此輸入值會啟用新資料行的所有控制項。</span><span class="sxs-lookup"><span data-stu-id="34c04-161">Entering a value here activates all the controls for the new column.</span></span>

<span data-ttu-id="34c04-162">索引標籤至 [**資料類型**] 清單，然後選擇 [ **int**]。這個值會指定 ID 資料行將包含整數（數位）資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-162">Tab to the **Data Type** list and choose **int**. This value specifies that the ID column will contain integer (number) data.</span></span>

> [!NOTE]
> <span data-ttu-id="34c04-163">我們不會在此呼叫它（很多），但您可以使用標準 Windows 鍵盤手勢在此方格中進行流覽。</span><span class="sxs-lookup"><span data-stu-id="34c04-163">We won't call it out any more here (much), but you can use standard Windows keyboard gestures to navigate in this grid.</span></span> <span data-ttu-id="34c04-164">例如，您可以在欄位之間定位，只要開始輸入，就可以選取清單中的專案，依此類推。</span><span class="sxs-lookup"><span data-stu-id="34c04-164">For example, you can tab between fields, you can just start typing in order to select an item in a list, and so on.</span></span>

<span data-ttu-id="34c04-165">索引標籤超過**預設值**方塊（也就是將它保留空白）。</span><span class="sxs-lookup"><span data-stu-id="34c04-165">Tab past the **Default Value** box (that is, leave it blank).</span></span> <span data-ttu-id="34c04-166">選擇 [**是主要金鑰**] 核取方塊，然後選取它。</span><span class="sxs-lookup"><span data-stu-id="34c04-166">Tab to the **Is Primary Key** check box and select it.</span></span> <span data-ttu-id="34c04-167">此選項會告訴資料庫，[*識別碼*] 資料行會包含可識別個別資料列的資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-167">This option tells the database that the *ID* column will contain the data that identifies individual rows.</span></span> <span data-ttu-id="34c04-168">（也就是說，每個資料列在 [識別碼] 資料行中都有唯一的值，您可以用來尋找該資料列）。</span><span class="sxs-lookup"><span data-stu-id="34c04-168">(That is, each row will have a unique value in the ID column that you can use to find that row.)</span></span>

<span data-ttu-id="34c04-169">選擇 [**是身分識別**] 選項。</span><span class="sxs-lookup"><span data-stu-id="34c04-169">Choose the **Is Identity** option.</span></span> <span data-ttu-id="34c04-170">此選項會告訴資料庫，它應該會自動為每個新的資料列產生下一個連續數位。</span><span class="sxs-lookup"><span data-stu-id="34c04-170">This option tells the database that it should automatically generate the next sequential number for each new row.</span></span> <span data-ttu-id="34c04-171">（[**是身分識別**] 選項只有在您也選取了 [**是主要索引鍵**] 選項時才適用）。</span><span class="sxs-lookup"><span data-stu-id="34c04-171">(The **Is Identity** option works only if you've also selected the **Is Primary Key** option.)</span></span>

<span data-ttu-id="34c04-172">按一下下一個格線列，或按兩次 Tab 鍵，完成目前的資料列。</span><span class="sxs-lookup"><span data-stu-id="34c04-172">Click in the next grid row, or press Tab twice to finish the current row.</span></span> <span data-ttu-id="34c04-173">任一手勢會儲存目前的資料列，並啟動下一個資料列。</span><span class="sxs-lookup"><span data-stu-id="34c04-173">Either gesture saves the current row and starts the next one.</span></span> <span data-ttu-id="34c04-174">請注意，[**預設值**] 資料行現在會顯示**Null**。</span><span class="sxs-lookup"><span data-stu-id="34c04-174">Notice that the **Default Value** column now says **Null**.</span></span> <span data-ttu-id="34c04-175">（Null 是預設值的預設值，因此要說出）。</span><span class="sxs-lookup"><span data-stu-id="34c04-175">(Null is the default value for the default value, so to speak.)</span></span>

<span data-ttu-id="34c04-176">當您完成定義新的**ID**資料行時，設計工具看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="34c04-176">When you've finished defining the new **ID** column, the designer will look like this illustration:</span></span>

![定義電影資料表的 ID 資料行之後的 WebMatrix 資料庫設計工具](displaying-data/_static/image7.png)

<span data-ttu-id="34c04-178">若要建立下一個資料行，請按一下 [**名稱**] 資料行中的方塊。</span><span class="sxs-lookup"><span data-stu-id="34c04-178">To create the next column, click in the box in the **Name** column.</span></span> <span data-ttu-id="34c04-179">輸入資料行的「標題」，然後選取 [ **Nvarchar** ] 做為**資料類型**值。</span><span class="sxs-lookup"><span data-stu-id="34c04-179">Enter "Title" for the column and then select **nvarchar** for the **Data Type** value.</span></span> <span data-ttu-id="34c04-180">**NVarchar**的 "var" 部分會告訴資料庫，此資料行的資料將是字串，其大小可能會因記錄而異。</span><span class="sxs-lookup"><span data-stu-id="34c04-180">The "var" part of **nvarchar** tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="34c04-181">（"N" 前置詞代表「國家」，表示欄位可以保存任何字母或書寫系統的字元資料，也就是欄位保留 Unicode 資料）。</span><span class="sxs-lookup"><span data-stu-id="34c04-181">(The "n" prefix represents "national," which indicates that the field can hold character data for any alphabet or writing system — that is, the field holds Unicode data.)</span></span>

<span data-ttu-id="34c04-182">當您選擇 [ **Nvarchar**] 時，會出現另一個方塊，您可以在其中輸入欄位的最大長度。</span><span class="sxs-lookup"><span data-stu-id="34c04-182">When you choose **nvarchar**, another box appears where you can enter the maximum length for the field.</span></span> <span data-ttu-id="34c04-183">輸入50，假設您在本教學課程中使用的電影標題不會超過50個字元。</span><span class="sxs-lookup"><span data-stu-id="34c04-183">Enter 50, on the assumption that no movie title that you'll work with in this tutorial will be longer than 50 characters.</span></span>

<span data-ttu-id="34c04-184">略過**預設值**，並清除 [**允許 null]** 選項。</span><span class="sxs-lookup"><span data-stu-id="34c04-184">Skip **Default Value** and clear the **Allow Nulls** option.</span></span> <span data-ttu-id="34c04-185">您不希望資料庫允許將任何電影輸入至沒有標題的資料庫中。</span><span class="sxs-lookup"><span data-stu-id="34c04-185">You don't want the database to allow any movies to be entered into the database that don't have a title.</span></span>

<span data-ttu-id="34c04-186">當您完成並移至下一個資料列時，設計工具會如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="34c04-186">When you're done and move to the next row, the designer looks like this illustration:</span></span>

![定義電影資料表的標題資料行之後的 WebMatrix 資料庫設計工具](displaying-data/_static/image8.png)

<span data-ttu-id="34c04-188">重複這些步驟來建立名為「內容類型」的資料行，但長度除外，請將它設定為只30。</span><span class="sxs-lookup"><span data-stu-id="34c04-188">Repeat these steps to create a column named "Genre", except for the length, set it to just 30.</span></span>

<span data-ttu-id="34c04-189">建立另一個名為 "Year" 的資料行。</span><span class="sxs-lookup"><span data-stu-id="34c04-189">Create another column named "Year."</span></span> <span data-ttu-id="34c04-190">針對 [資料類型]，選擇 [ **Nchar** （非**Nvarchar**）]，並將長度設定為4。</span><span class="sxs-lookup"><span data-stu-id="34c04-190">For the data type, choose **nchar** (not **nvarchar**) and set the length to 4.</span></span> <span data-ttu-id="34c04-191">在年份中，您會使用4位數的數位，例如 "1995" 或 "2010"，因此您不需要可變大小的資料行。</span><span class="sxs-lookup"><span data-stu-id="34c04-191">For the year, you're going to use a 4-digit number like "1995" or "2010", so you don't require a variable-sized column.</span></span>

<span data-ttu-id="34c04-192">完成的設計如下所示：</span><span class="sxs-lookup"><span data-stu-id="34c04-192">Here's what the finished design looks like:</span></span>

![針對電影資料表定義所有欄位後的 WebMatrix 資料庫設計工具](displaying-data/_static/image9.png)

<span data-ttu-id="34c04-194">按 Ctrl + S，或按一下快速存取工具列中的 [**儲存**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="34c04-194">Press Ctrl+S or click the **Save** button in the Quick Access toolbar.</span></span> <span data-ttu-id="34c04-195">關閉 [資料庫設計工具]，方法是關閉索引標籤。</span><span class="sxs-lookup"><span data-stu-id="34c04-195">Close the database designer by closing the tab.</span></span>

## <a name="adding-some-example-data"></a><span data-ttu-id="34c04-196">新增一些範例資料</span><span class="sxs-lookup"><span data-stu-id="34c04-196">Adding Some Example Data</span></span>

<span data-ttu-id="34c04-197">稍後在本教學課程系列中，您將建立一個頁面，您可以在表單中輸入新電影。</span><span class="sxs-lookup"><span data-stu-id="34c04-197">Later in this tutorial series you'll create a page where you can enter new movies in a form.</span></span> <span data-ttu-id="34c04-198">不過，現在您可以新增一些範例資料，讓您可以在頁面上顯示。</span><span class="sxs-lookup"><span data-stu-id="34c04-198">For now, however, you can add some example data that you can then display on a page.</span></span>

<span data-ttu-id="34c04-199">在 WebMatrix 的 [**資料庫**] 工作區中，您會看到一個樹狀結構，其中會顯示您稍早建立的 *.sdf*檔案。</span><span class="sxs-lookup"><span data-stu-id="34c04-199">In the **Database** workspace in WebMatrix, notice that there's a tree that shows you the *.sdf* file you created earlier.</span></span> <span data-ttu-id="34c04-200">開啟新的 *.sdf*檔案的節點，然後開啟 [**資料表]** 節點。</span><span class="sxs-lookup"><span data-stu-id="34c04-200">Open the node for your new *.sdf* file, and then open the **Tables** node.</span></span>

![將樹狀結構開啟至電影資料表的 WebMatrix 資料庫工作區](displaying-data/_static/image10.png)

<span data-ttu-id="34c04-202">以滑鼠右鍵按一下 [**電影**] 節點，然後選擇 [**資料**]。</span><span class="sxs-lookup"><span data-stu-id="34c04-202">Right-click the **Movies** node and then choose **Data**.</span></span> <span data-ttu-id="34c04-203">WebMatrix 會開啟一個格線，您可以在其中輸入*電影*資料表的資料：</span><span class="sxs-lookup"><span data-stu-id="34c04-203">WebMatrix opens a grid where you can enter data for the *Movies* table:</span></span>

![WebMatrix 中的資料庫專案方格（空白）](displaying-data/_static/image11.png)

<span data-ttu-id="34c04-205">按一下 [**標題**] 資料行，並輸入 "When Harry 符合 Sally"。</span><span class="sxs-lookup"><span data-stu-id="34c04-205">Click the **Title** column and enter "When Harry Met Sally".</span></span> <span data-ttu-id="34c04-206">移至 [類型]**資料行（** 您可以使用 Tab 鍵），然後輸入 "Romantic 喜劇"。</span><span class="sxs-lookup"><span data-stu-id="34c04-206">Move to the **Genre** column (you can use the Tab key) and enter "Romantic Comedy".</span></span> <span data-ttu-id="34c04-207">移至 [**年**] 資料行，然後輸入 "1989"：</span><span class="sxs-lookup"><span data-stu-id="34c04-207">Move to the **Year** column and enter "1989":</span></span>

![具有一筆記錄的 WebMatrix 中的資料庫輸入方格](displaying-data/_static/image12.png)

<span data-ttu-id="34c04-209">按 Enter 鍵，WebMatrix 會儲存新電影。</span><span class="sxs-lookup"><span data-stu-id="34c04-209">Press Enter, and WebMatrix saves the new movie.</span></span> <span data-ttu-id="34c04-210">請注意，[**識別碼**] 資料行已填入。</span><span class="sxs-lookup"><span data-stu-id="34c04-210">Notice that the **ID** column has been filled in.</span></span>

![WebMatrix 中的資料庫輸入方格，其中包含一筆記錄和自動產生的識別碼](displaying-data/_static/image13.png)

<span data-ttu-id="34c04-212">輸入另一部電影（例如，"戲劇"、"1939"）。</span><span class="sxs-lookup"><span data-stu-id="34c04-212">Enter another movie (for example, "Gone with the Wind", "Drama", "1939").</span></span> <span data-ttu-id="34c04-213">[識別碼] 資料行會再次填入：</span><span class="sxs-lookup"><span data-stu-id="34c04-213">The ID column is filled in again:</span></span>

![WebMatrix 中的資料庫專案方格，其中包含兩個記錄和自動產生的識別碼](displaying-data/_static/image14.png)

<span data-ttu-id="34c04-215">輸入第三個電影（例如，"Ghostbusters"、"喜劇"）。</span><span class="sxs-lookup"><span data-stu-id="34c04-215">Enter a third movie (for example, "Ghostbusters", "Comedy").</span></span> <span data-ttu-id="34c04-216">以實驗的方式，將 [**年份**] 資料行保留空白，然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="34c04-216">As an experiment, leave the **Year** column blank and then press Enter.</span></span> <span data-ttu-id="34c04-217">因為您已取消選取 [**允許 Null]** 選項，所以資料庫會顯示錯誤：</span><span class="sxs-lookup"><span data-stu-id="34c04-217">Because you unselected the **Allow Nulls** option, the database shows an error:</span></span>

![如果必要的資料行值保留空白，則會顯示「不正確資料」錯誤](displaying-data/_static/image15.png)

<span data-ttu-id="34c04-219">按一下 **[確定]** 返回並修正專案（"Ghostbusters" 的年份是1984），然後按 enter。</span><span class="sxs-lookup"><span data-stu-id="34c04-219">Click **OK** to go back and fix the entry (the year for "Ghostbusters" is 1984), and then press Enter.</span></span>

<span data-ttu-id="34c04-220">填入數個電影，直到您有8個以上的影片為止。</span><span class="sxs-lookup"><span data-stu-id="34c04-220">Fill in several movies until you have 8 or so.</span></span> <span data-ttu-id="34c04-221">（輸入8可讓您更輕鬆地在稍後使用分頁。</span><span class="sxs-lookup"><span data-stu-id="34c04-221">(Entering 8 makes it easier to work with paging later.</span></span> <span data-ttu-id="34c04-222">但如果太多，現在只需輸入幾個。）實際的資料並不重要。</span><span class="sxs-lookup"><span data-stu-id="34c04-222">But if that's too many, enter just a few for now.) The actual data doesn't matter.</span></span>

![具有任一筆記錄的 WebMatrix 中的資料庫輸入方格](displaying-data/_static/image16.png)

<span data-ttu-id="34c04-224">如果您輸入所有電影而沒有任何錯誤，則識別碼值為連續。</span><span class="sxs-lookup"><span data-stu-id="34c04-224">If you entered all the movies without any errors, the ID values are sequential.</span></span> <span data-ttu-id="34c04-225">如果您嘗試儲存未完成的電影記錄，識別碼編號可能不是連續的。</span><span class="sxs-lookup"><span data-stu-id="34c04-225">If you tried to save an incomplete movie record, the ID numbers might not be sequential.</span></span> <span data-ttu-id="34c04-226">如果是這樣，沒關係。</span><span class="sxs-lookup"><span data-stu-id="34c04-226">If so, that's okay.</span></span> <span data-ttu-id="34c04-227">這些數位沒有任何固有的意義，而且唯一重要的是，它們在*電影*資料表中是唯一的。</span><span class="sxs-lookup"><span data-stu-id="34c04-227">The numbers don't have any inherent meaning, and the only thing that's important is that they're unique in the *Movies* table.</span></span>

<span data-ttu-id="34c04-228">關閉包含 [資料庫設計工具] 的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="34c04-228">Close the tab that contains the database designer.</span></span>

<span data-ttu-id="34c04-229">現在您可以將此資料顯示在網頁上。</span><span class="sxs-lookup"><span data-stu-id="34c04-229">Now you can turn to displaying this data on a web page.</span></span>

## <a name="displaying-data-in-a-page-by-using-the-webgrid-helper"></a><span data-ttu-id="34c04-230">使用 WebGrid Helper 在頁面中顯示資料</span><span class="sxs-lookup"><span data-stu-id="34c04-230">Displaying Data in a Page by Using the WebGrid Helper</span></span>

<span data-ttu-id="34c04-231">若要在頁面中顯示資料，您將使用 `WebGrid` helper。</span><span class="sxs-lookup"><span data-stu-id="34c04-231">To display data in a page, you're going to use the `WebGrid` helper.</span></span> <span data-ttu-id="34c04-232">此 helper 會在方格或資料表（資料列和資料行）中產生顯示。</span><span class="sxs-lookup"><span data-stu-id="34c04-232">This helper produces a display in a grid or table (rows and columns).</span></span> <span data-ttu-id="34c04-233">如您所見，您可以使用格式設定和其他功能來縮小方格的範圍。</span><span class="sxs-lookup"><span data-stu-id="34c04-233">As you'll see, you'll be able refine the grid with formatting and other features.</span></span>

<span data-ttu-id="34c04-234">若要執行方格，您必須撰寫幾行程式碼。</span><span class="sxs-lookup"><span data-stu-id="34c04-234">To run the grid, you'll have to write a few lines of code.</span></span> <span data-ttu-id="34c04-235">這幾行會做為您在本教學課程中所做的幾乎所有資料存取的一種模式。</span><span class="sxs-lookup"><span data-stu-id="34c04-235">These few lines will serve as a kind of pattern for almost all of the data access that you do in this tutorial.</span></span>

> [!NOTE]
> <span data-ttu-id="34c04-236">您實際上有許多選項可以在頁面上顯示資料;`WebGrid` helper 只是一個。</span><span class="sxs-lookup"><span data-stu-id="34c04-236">You actually have many options for displaying data on a page; the `WebGrid` helper is just one.</span></span> <span data-ttu-id="34c04-237">我們在本教學課程中選擇它，是因為它是顯示資料的最簡單方式，而且是合理的彈性。</span><span class="sxs-lookup"><span data-stu-id="34c04-237">We chose it for this tutorial because it's the easiest way to display data and because it's reasonably flexible.</span></span> <span data-ttu-id="34c04-238">在下一個教學課程中，您將瞭解如何使用更「手動」方式來處理頁面中的資料，讓您更直接控制如何顯示資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-238">In the next tutorial set, you'll see how to use a more "manual" way to work with data in the page, which gives you more direct control over how to display the data.</span></span>

<span data-ttu-id="34c04-239">在 WebMatrix 的左窗格中，按一下 [檔案]**工作區。**</span><span class="sxs-lookup"><span data-stu-id="34c04-239">In the left pane in WebMatrix, click the **Files** workspace.</span></span>

<span data-ttu-id="34c04-240">您所建立的新資料庫會在*應用程式\_Data*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="34c04-240">The new database you created is in the *App\_Data* folder.</span></span> <span data-ttu-id="34c04-241">如果資料夾尚未存在，則 WebMatrix 會為您的新資料庫建立該資料夾。</span><span class="sxs-lookup"><span data-stu-id="34c04-241">If the folder didn't already exist, WebMatrix created it for your new database.</span></span> <span data-ttu-id="34c04-242">（如果您先前已安裝 helper，此資料夾可能已經存在）。</span><span class="sxs-lookup"><span data-stu-id="34c04-242">(The folder might have existed if you'd previously installed helpers.)</span></span>

<span data-ttu-id="34c04-243">在樹狀檢視中，選取網站的根目錄。</span><span class="sxs-lookup"><span data-stu-id="34c04-243">In the tree view, select the root of the website.</span></span> <span data-ttu-id="34c04-244">您必須選取網站的根目錄;否則，新的檔案可能會新增至應用程式\_Data 資料夾中。</span><span class="sxs-lookup"><span data-stu-id="34c04-244">You must select the root of the website; otherwise, the new file might be added to the App\_Data folder.</span></span>

<span data-ttu-id="34c04-245">在功能區中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="34c04-245">In the ribbon, click **New**.</span></span> <span data-ttu-id="34c04-246">在 [**選擇檔案類型**] 方塊中，選擇 [ **CSHTML**]。</span><span class="sxs-lookup"><span data-stu-id="34c04-246">In the **Choose a File Type** box, choose **CSHTML**.</span></span>

<span data-ttu-id="34c04-247">在 [**名稱**] 方塊中，將新頁面命名為「電影. cshtml」：</span><span class="sxs-lookup"><span data-stu-id="34c04-247">In the **Name** box, name the new page "Movies.cshtml":</span></span>

![顯示 [電影] 頁面的 [選擇檔案類型] 對話方塊](displaying-data/_static/image17.png)

<span data-ttu-id="34c04-249">按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="34c04-249">Click the **OK** button.</span></span> <span data-ttu-id="34c04-250">WebMatrix 會開啟新檔案，其中包含一些基本架構元素。</span><span class="sxs-lookup"><span data-stu-id="34c04-250">WebMatrix opens a new file with some skeleton elements in it.</span></span> <span data-ttu-id="34c04-251">首先，您要撰寫一些程式碼，從資料庫取得資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-251">First you'll write some code to go get the data from the database.</span></span> <span data-ttu-id="34c04-252">接著，您會將標記新增至頁面，以實際顯示資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-252">Then you'll add markup to the page to actually display the data.</span></span>

### <a name="writing-the-data-query-code"></a><span data-ttu-id="34c04-253">撰寫資料查詢程式碼</span><span class="sxs-lookup"><span data-stu-id="34c04-253">Writing the Data Query Code</span></span>

<span data-ttu-id="34c04-254">在頁面頂端的 [`@{`] 和 [`}`] 字元之間，輸入下列程式碼。</span><span class="sxs-lookup"><span data-stu-id="34c04-254">At the top of the page, between the `@{` and `}` characters, enter the following code.</span></span> <span data-ttu-id="34c04-255">（請確定您在開頭和右大括弧之間輸入此程式碼）。</span><span class="sxs-lookup"><span data-stu-id="34c04-255">(Make sure that you enter this code between the opening and closing braces.)</span></span>

[!code-csharp[Main](displaying-data/samples/sample1.cs)]

<span data-ttu-id="34c04-256">第一行會開啟您稍早建立的資料庫，這一律是在資料庫中執行某些動作之前的第一個步驟。</span><span class="sxs-lookup"><span data-stu-id="34c04-256">The first line opens the database that you created earlier, which is always the first step before doing something with the database.</span></span> <span data-ttu-id="34c04-257">您會告訴資料庫的 `Database.Open` 方法名稱已開啟。</span><span class="sxs-lookup"><span data-stu-id="34c04-257">You tell the `Database.Open` method name of the database to open.</span></span> <span data-ttu-id="34c04-258">請注意，您不會在名稱中包含 *.sdf。*</span><span class="sxs-lookup"><span data-stu-id="34c04-258">Notice that you don't include *.sdf* in the name.</span></span> <span data-ttu-id="34c04-259">`Open` 方法假設它正在尋找 *.sdf*檔案（也就是*WebPagesMovies .sdf*），而且 *.sdf*檔案位於*應用程式\_Data*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="34c04-259">The `Open` method assumes that it's looking for an *.sdf* file (that is, *WebPagesMovies.sdf*) and that the *.sdf* file is in the *App\_Data* folder.</span></span> <span data-ttu-id="34c04-260">（稍早我們說過，*應用程式\_Data*資料夾是保留的，此案例是 ASP.NET 對該名稱進行假設的其中一個地方）。</span><span class="sxs-lookup"><span data-stu-id="34c04-260">(Earlier we noted that the *App\_Data* folder is reserved; this scenario is one of the places where ASP.NET makes assumptions about that name.)</span></span>

<span data-ttu-id="34c04-261">當資料庫開啟時，它的參考會放入名為 `db`的變數中。</span><span class="sxs-lookup"><span data-stu-id="34c04-261">When the database is opened, a reference to it is put into the variable named `db`.</span></span> <span data-ttu-id="34c04-262">（可以命名為任何專案）。`db` 變數是您最後與資料庫互動的方式。</span><span class="sxs-lookup"><span data-stu-id="34c04-262">(Which could be named anything.) The `db` variable is how you'll end up interacting with the database.</span></span>

<span data-ttu-id="34c04-263">第二行會使用 `Query` 方法，實際提取資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-263">The second line actually fetches the database data by using the `Query` method.</span></span> <span data-ttu-id="34c04-264">請注意此程式碼的運作方式： `db` 變數具有已開啟資料庫的參考，而且您會使用 `db` 變數（`db.Query`）來叫用 `Query` 方法。</span><span class="sxs-lookup"><span data-stu-id="34c04-264">Notice how this code works: the `db` variable has a reference to the opened database, and you invoke the `Query` method by using the `db` variable (`db.Query`).</span></span>

<span data-ttu-id="34c04-265">查詢本身是 SQL `Select` 語句。</span><span class="sxs-lookup"><span data-stu-id="34c04-265">The query itself is a SQL `Select` statement.</span></span> <span data-ttu-id="34c04-266">（如需有關 SQL 的背景資訊，請參閱稍後的說明）。在語句中，`Movies` 會識別要查詢的資料表。</span><span class="sxs-lookup"><span data-stu-id="34c04-266">(For a little background about SQL, see the explanation later.) In the statement, `Movies` identifies the table to query.</span></span> <span data-ttu-id="34c04-267">`*` 字元指定查詢應傳回資料表中的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="34c04-267">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="34c04-268">（您也可以個別列出資料行，並以逗號分隔）。</span><span class="sxs-lookup"><span data-stu-id="34c04-268">(You could also list columns individually, separated by commas.)</span></span>

<span data-ttu-id="34c04-269">傳回查詢的結果（如果有的話），並可在 `selectedData` 變數中取得。</span><span class="sxs-lookup"><span data-stu-id="34c04-269">The results of the query, if any, are returned and made available in the `selectedData` variable.</span></span> <span data-ttu-id="34c04-270">同樣地，變數可以命名為任何專案。</span><span class="sxs-lookup"><span data-stu-id="34c04-270">Again, the variable could be named anything.</span></span>

<span data-ttu-id="34c04-271">最後，第三行會告訴 ASP.NET 您想要使用 `WebGrid` helper 的實例。</span><span class="sxs-lookup"><span data-stu-id="34c04-271">Finally, the third line tells ASP.NET that you want to use an instance of the `WebGrid` helper.</span></span> <span data-ttu-id="34c04-272">您可以使用 `new` 關鍵字來建立（具現*化*） helper 物件，並透過 `selectedData` 變數將查詢結果傳遞給它。</span><span class="sxs-lookup"><span data-stu-id="34c04-272">You create (*instantiate*) the helper object by using the `new` keyword and pass it the query results via the `selectedData` variable.</span></span> <span data-ttu-id="34c04-273">新的 `WebGrid` 物件以及資料庫查詢的結果，可在 `grid` 變數中取得。</span><span class="sxs-lookup"><span data-stu-id="34c04-273">The new `WebGrid` object, along with the results of the database query, are made available in the `grid` variable.</span></span> <span data-ttu-id="34c04-274">您需要這樣的結果，才能實際顯示頁面中的資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-274">You'll need that result in a moment to actually display the data in the page.</span></span>

<span data-ttu-id="34c04-275">在這個階段，資料庫已開啟，您已取得您想要的資料，而且您已準備好該資料的 `WebGrid` helper。</span><span class="sxs-lookup"><span data-stu-id="34c04-275">At this stage, the database has been opened, you've gotten the data you want, and you've prepared the `WebGrid` helper with that data.</span></span> <span data-ttu-id="34c04-276">接下來是在頁面中建立標記。</span><span class="sxs-lookup"><span data-stu-id="34c04-276">Next is to create the markup in the page.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="34c04-277">**結構化查詢語言 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="34c04-277">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="34c04-278">SQL 是一種語言，用於大部分關係資料庫中，用來管理資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-278">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="34c04-279">其中包含的命令可讓您抓取資料並加以更新，並可讓您建立、修改和管理資料庫資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="34c04-279">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage data in database tables.</span></span> <span data-ttu-id="34c04-280">SQL 不同于程式設計語言（例如C#）。</span><span class="sxs-lookup"><span data-stu-id="34c04-280">SQL is different than a programming language (like C#).</span></span> <span data-ttu-id="34c04-281">在 SQL 中，您會告訴資料庫您所需的內容，而這就是資料庫的工作，以找出如何取得資料或執行工作。</span><span class="sxs-lookup"><span data-stu-id="34c04-281">With SQL, you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="34c04-282">以下是一些 SQL 命令的範例，以及它們的作用：</span><span class="sxs-lookup"><span data-stu-id="34c04-282">Here are examples of some SQL commands and what they do:</span></span>
> 
> `Select * From Movies`
> 
> `SELECT ID, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="34c04-283">第一個 `Select` 語句會從*電影*資料表取得所有資料行（由 `*`指定）。</span><span class="sxs-lookup"><span data-stu-id="34c04-283">The first `Select` statement gets all the columns (specified by `*`) from the *Movies* table.</span></span>
> 
> <span data-ttu-id="34c04-284">第二個 `Select` 語句會從*Product*資料表中的記錄，提取 price 資料行值大於10的識別碼、名稱和價格資料行。</span><span class="sxs-lookup"><span data-stu-id="34c04-284">The second `Select` statement fetches the ID, Name, and Price columns from records in the *Product* table whose Price column value is more than 10.</span></span> <span data-ttu-id="34c04-285">此命令會根據名稱資料行的值，以字母順序傳回結果。</span><span class="sxs-lookup"><span data-stu-id="34c04-285">The command returns the results in alphabetical order based on the values of the Name column.</span></span> <span data-ttu-id="34c04-286">如果沒有任何記錄符合價格條件，此命令會傳回空的集合。</span><span class="sxs-lookup"><span data-stu-id="34c04-286">If no records match the price criteria, the command returns an empty set.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ('Croissant', 'A flaky delight', 1.99)`
> 
> <span data-ttu-id="34c04-287">此命令會將新記錄插入*Product*資料表，並將 Name 資料行設定為 "可頌麵包"、Description 資料行設為 "a 不穩定取悅"，並將價格設為1.99。</span><span class="sxs-lookup"><span data-stu-id="34c04-287">This command inserts a new record into the *Product* table, setting the Name column to "Croissant", the Description column to "A flaky delight", and the price to 1.99.</span></span>
> 
> <span data-ttu-id="34c04-288">請注意，當您指定非數值時，此值會以單引號括住（不是雙引號，如所示C#）。</span><span class="sxs-lookup"><span data-stu-id="34c04-288">Notice that when you're specifying a non-numeric value, the value is enclosed in single quotation marks (not double quotation marks, as in C#).</span></span> <span data-ttu-id="34c04-289">您可以在文字或日期值前後加上引號，但不能用在數位的周圍。</span><span class="sxs-lookup"><span data-stu-id="34c04-289">You use these quotation marks around text or date values, but not around numbers.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < '01/01/2008'`
> 
> <span data-ttu-id="34c04-290">此命令會刪除*產品*資料表中，其到期日資料行早于2008年1月1日的記錄。</span><span class="sxs-lookup"><span data-stu-id="34c04-290">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="34c04-291">（此命令假設*產品*資料表具有這類資料行）。以 MM/DD/YYYY 格式輸入日期，但應以用於地區設定的格式輸入。</span><span class="sxs-lookup"><span data-stu-id="34c04-291">(The command assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="34c04-292">`Insert` 和 `Delete` 命令不會傳回結果集。</span><span class="sxs-lookup"><span data-stu-id="34c04-292">The `Insert` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="34c04-293">相反地，它們會傳回一個數位，告訴您命令有多少記錄受到影響。</span><span class="sxs-lookup"><span data-stu-id="34c04-293">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="34c04-294">對於其中某些作業（例如插入和刪除記錄），要求操作的進程必須在資料庫中擁有適當的許可權。</span><span class="sxs-lookup"><span data-stu-id="34c04-294">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="34c04-295">這就是為什麼生產資料庫在您連接到資料庫時，通常必須提供使用者名稱和密碼的原因。</span><span class="sxs-lookup"><span data-stu-id="34c04-295">That's why for production databases you often have to supply a user name and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="34c04-296">有數十個 SQL 命令，但它們都遵循如下所示的模式。</span><span class="sxs-lookup"><span data-stu-id="34c04-296">There are dozens of SQL commands, but they all follow a pattern like the commands you see here.</span></span> <span data-ttu-id="34c04-297">您可以使用 SQL 命令來建立資料庫資料表、計算資料表中的記錄數目、計算價格，以及執行許多其他作業。</span><span class="sxs-lookup"><span data-stu-id="34c04-297">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>

### <a name="adding-markup-to-display-the-data"></a><span data-ttu-id="34c04-298">加入標記以顯示資料</span><span class="sxs-lookup"><span data-stu-id="34c04-298">Adding Markup to Display the Data</span></span>

<span data-ttu-id="34c04-299">在 `<head>` 元素內，將 `<title>` 元素的內容設定為「電影」：</span><span class="sxs-lookup"><span data-stu-id="34c04-299">Inside the `<head>` element, set contents of the `<title>` element to "Movies":</span></span>

[!code-html[Main](displaying-data/samples/sample2.html?highlight=3)]

<span data-ttu-id="34c04-300">在頁面的 `<body>` 元素內，新增下列專案：</span><span class="sxs-lookup"><span data-stu-id="34c04-300">Inside the `<body>` element of the page, add the following:</span></span>

[!code-html[Main](displaying-data/samples/sample3.html)]

<span data-ttu-id="34c04-301">就這麼容易！</span><span class="sxs-lookup"><span data-stu-id="34c04-301">That's it.</span></span> <span data-ttu-id="34c04-302">`grid` 變數是您稍早在程式碼中建立 `WebGrid` 物件時所建立的值。</span><span class="sxs-lookup"><span data-stu-id="34c04-302">The `grid` variable is the value you created when you created the `WebGrid` object in code earlier.</span></span>

<span data-ttu-id="34c04-303">在 WebMatrix 樹狀檢視中，以滑鼠右鍵按一下頁面，然後選取 [**在瀏覽器中啟動**]。</span><span class="sxs-lookup"><span data-stu-id="34c04-303">In the WebMatrix tree view, right-click the page and select **Launch in browser**.</span></span> <span data-ttu-id="34c04-304">您會看到類似此頁面的內容：</span><span class="sxs-lookup"><span data-stu-id="34c04-304">You'll see something like this page:</span></span>

![電影資料表的預設 WebGrid helper 輸出](displaying-data/_static/image18.png)

<span data-ttu-id="34c04-306">按一下資料行標題連結，依該資料行排序。</span><span class="sxs-lookup"><span data-stu-id="34c04-306">Click a column heading link to sort by that column.</span></span> <span data-ttu-id="34c04-307">按一下標題就能夠排序，這是內建在**WebGrid** helper 中的功能。</span><span class="sxs-lookup"><span data-stu-id="34c04-307">Being able to sort by clicking a heading is a feature that's built into the **WebGrid** helper.</span></span>

<span data-ttu-id="34c04-308">`GetHtml` 方法，如其名所示，會產生可顯示資料的標記。</span><span class="sxs-lookup"><span data-stu-id="34c04-308">The `GetHtml` method, as its name suggests, generates markup that displays the data.</span></span> <span data-ttu-id="34c04-309">根據預設，`GetHtml` 方法會產生 HTML `<table>` 元素。</span><span class="sxs-lookup"><span data-stu-id="34c04-309">By default, the `GetHtml` method generates an HTML `<table>` element.</span></span> <span data-ttu-id="34c04-310">（如果您想要的話，可以在瀏覽器中查看頁面的來源來驗證轉譯）。</span><span class="sxs-lookup"><span data-stu-id="34c04-310">(If you want, you can verify the rendering by looking at the source of the page in the browser.)</span></span>

## <a name="modifying-the-look-of-the-grid"></a><span data-ttu-id="34c04-311">修改方格的外觀</span><span class="sxs-lookup"><span data-stu-id="34c04-311">Modifying the Look of the Grid</span></span>

<span data-ttu-id="34c04-312">像您一樣使用 `WebGrid` 協助程式很簡單，但所產生的顯示是純文字。</span><span class="sxs-lookup"><span data-stu-id="34c04-312">Using the `WebGrid` helper like you just did is easy, but the resulting display is plain.</span></span> <span data-ttu-id="34c04-313">[`WebGrid` helper] 具有各種選項，可讓您控制資料的顯示方式。</span><span class="sxs-lookup"><span data-stu-id="34c04-313">The `WebGrid` helper has all sorts of options that let you control how the data is displayed.</span></span> <span data-ttu-id="34c04-314">本教學課程中有太多要探索的內容，但本節將為您介紹其中一些選項。</span><span class="sxs-lookup"><span data-stu-id="34c04-314">There are far too many to explore in this tutorial, but this section will give you an idea of some of those options.</span></span> <span data-ttu-id="34c04-315">本系列稍後的教學課程將涵蓋一些其他選項。</span><span class="sxs-lookup"><span data-stu-id="34c04-315">A few additional options will be covered in later tutorials in this series.</span></span>

### <a name="specifying-individual-columns-to-display"></a><span data-ttu-id="34c04-316">指定要顯示的個別資料行</span><span class="sxs-lookup"><span data-stu-id="34c04-316">Specifying Individual Columns to Display</span></span>

<span data-ttu-id="34c04-317">若要開始，您可以指定只顯示特定資料行。</span><span class="sxs-lookup"><span data-stu-id="34c04-317">To start, you can specify that you want to display only certain columns.</span></span> <span data-ttu-id="34c04-318">根據預設，如您所見，方格會顯示 [*電影*] 資料表中的四個數據行。</span><span class="sxs-lookup"><span data-stu-id="34c04-318">By default, as you've seen, the grid shows all four of the columns from the *Movies* table.</span></span>

<span data-ttu-id="34c04-319">在 [*電影*] 檔案中，將您剛才新增的 `@grid.GetHtml()` 標記取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="34c04-319">In the *Movies.cshtml* file, replace the `@grid.GetHtml()` markup that you just added with the following:</span></span>

[!code-css[Main](displaying-data/samples/sample4.css)]

<span data-ttu-id="34c04-320">若要告知 helper 要顯示哪些資料行，您可以加入 `GetHtml` 方法的 `columns` 參數，並傳入資料行集合。</span><span class="sxs-lookup"><span data-stu-id="34c04-320">To tell the helper which columns to display, you include a `columns` parameter for the `GetHtml` method and pass in a collection of columns.</span></span> <span data-ttu-id="34c04-321">在集合中，您可以指定要包含的每個資料行。</span><span class="sxs-lookup"><span data-stu-id="34c04-321">In the collection, you specify each column to include.</span></span> <span data-ttu-id="34c04-322">您可以藉由包含 `grid.Column` 物件來指定要顯示的個別資料行，並傳入您想要的資料行名稱。</span><span class="sxs-lookup"><span data-stu-id="34c04-322">You specify an individual column to display by including a `grid.Column` object, and pass in the name of the data column you want.</span></span> <span data-ttu-id="34c04-323">（這些資料行必須包含在 SQL 查詢結果中，`WebGrid` helper 無法顯示查詢未傳回的資料行）。</span><span class="sxs-lookup"><span data-stu-id="34c04-323">(These columns must be included in the SQL query results — the `WebGrid` helper cannot display columns that were not returned by the query.)</span></span>

<span data-ttu-id="34c04-324">再次啟動瀏覽器中的 [ *cshtml* ] 頁面，這次您會看到如下所示的畫面（請注意，不會顯示任何 ID 資料行）：</span><span class="sxs-lookup"><span data-stu-id="34c04-324">Launch the *Movies.cshtml* page in the browser again, and this time you get a display like the following one (notice that no ID column is displayed):</span></span>

![WebGrid 顯示只顯示選取的資料行](displaying-data/_static/image19.png)

### <a name="changing-the-look-of-the-grid"></a><span data-ttu-id="34c04-326">變更方格的外觀</span><span class="sxs-lookup"><span data-stu-id="34c04-326">Changing the Look of the Grid</span></span>

<span data-ttu-id="34c04-327">另外還有幾個選項可用來顯示資料行，其中有一些會在本集合稍後的教學課程中探索。</span><span class="sxs-lookup"><span data-stu-id="34c04-327">There are quite a few more options for displaying columns, some of which will be explored in later tutorials in this set.</span></span> <span data-ttu-id="34c04-328">目前，本節將為您介紹可將方格的樣式設為整體的方式。</span><span class="sxs-lookup"><span data-stu-id="34c04-328">For now, this section will introduce you to ways in which you can style the grid as a whole.</span></span>

<span data-ttu-id="34c04-329">在頁面的 `<head>` 區段中，在結尾 `</head>` 標記之前，新增下列 `<style>` 元素：</span><span class="sxs-lookup"><span data-stu-id="34c04-329">Inside the `<head>` section of the page, just before the closing `</head>` tag, add the following `<style>` element:</span></span>

[!code-css[Main](displaying-data/samples/sample5.css)]

<span data-ttu-id="34c04-330">這個 CSS 標記會定義名為 `grid`、`head`等等的類別。</span><span class="sxs-lookup"><span data-stu-id="34c04-330">This CSS markup defines classes named `grid`, `head`, and so on.</span></span> <span data-ttu-id="34c04-331">您也可以將這些樣式定義放在個別的 *.css*檔案中，並將其連結至頁面。</span><span class="sxs-lookup"><span data-stu-id="34c04-331">You could also put these style definitions in a separate *.css* file and link that to the page.</span></span> <span data-ttu-id="34c04-332">（事實上，您稍後會在本教學課程中設定）。但為了方便您進行本教學課程，這些專案會在顯示資料的相同頁面中。</span><span class="sxs-lookup"><span data-stu-id="34c04-332">(In fact, you'll do that later in this tutorial set.) But to make things easy for this tutorial, they're inside the same page that displays the data.</span></span>

<span data-ttu-id="34c04-333">現在您可以取得 `WebGrid` helper 以使用這些樣式類別。</span><span class="sxs-lookup"><span data-stu-id="34c04-333">Now you can get the `WebGrid` helper to use these style classes.</span></span> <span data-ttu-id="34c04-334">Helper 只有這種用途的屬性（例如 `tableStyle`），您可以將 CSS 樣式類別名稱指派給它們，而該類別名稱會轉譯成由協助程式轉譯的標記之一部分。</span><span class="sxs-lookup"><span data-stu-id="34c04-334">The helper has a number of properties (for example, `tableStyle`) for just this purpose — you assign a CSS style class name to them, and that class name is rendered as part of the markup that's rendered by the helper.</span></span>

<span data-ttu-id="34c04-335">變更 `grid.GetHtml` 標記，使其看起來像下面這段程式碼：</span><span class="sxs-lookup"><span data-stu-id="34c04-335">Change the `grid.GetHtml` markup so that it now looks like this code:</span></span>

[!code-css[Main](displaying-data/samples/sample6.css)]

<span data-ttu-id="34c04-336">這裡的新功能是您已將 `tableStyle`、`headerStyle`和 `alternatingRowStyle` 參數新增至 `GetHtml` 方法。</span><span class="sxs-lookup"><span data-stu-id="34c04-336">What's new here is that you've added `tableStyle`, `headerStyle`, and `alternatingRowStyle` parameters to the `GetHtml` method.</span></span> <span data-ttu-id="34c04-337">這些參數已設定為您稍早新增的 CSS 樣式名稱。</span><span class="sxs-lookup"><span data-stu-id="34c04-337">These parameters have been set to the names of the CSS styles that you added a moment ago.</span></span>

<span data-ttu-id="34c04-338">執行頁面，這次您會看到看起來比以前更簡單的方格：</span><span class="sxs-lookup"><span data-stu-id="34c04-338">Run the page, and this time you see a grid that looks much less plain than before:</span></span>

![WebGrid 顯示，其中包含設定為 CSS 類別名稱的參數](displaying-data/_static/image20.png)

<span data-ttu-id="34c04-340">若要查看 `GetHtml` 方法產生的內容，您可以在瀏覽器中查看頁面的來源。</span><span class="sxs-lookup"><span data-stu-id="34c04-340">To see what the `GetHtml` method generated, you can look at the source of the page in the browser.</span></span> <span data-ttu-id="34c04-341">這裡不會詳細說明，但重點是，藉由指定 `tableStyle`之類的參數，您就會使方格產生如下所示的 HTML 標籤：</span><span class="sxs-lookup"><span data-stu-id="34c04-341">We won't go into detail here, but the important point is that by specifying parameters like `tableStyle`, you caused the grid to generate HTML tags like the following:</span></span>

`<table class="grid">`

<span data-ttu-id="34c04-342">`<table>` 標記已加入 `class` 屬性，它會參考您稍早新增的其中一個 CSS 規則。</span><span class="sxs-lookup"><span data-stu-id="34c04-342">The `<table>` tag has had a `class` attribute added to it that references one of the CSS rules that you added earlier.</span></span> <span data-ttu-id="34c04-343">這段程式碼會顯示基本模式 &mdash; `GetHtml` 方法的不同參數，讓您參考該方法接著會連同標記一起產生的 CSS 類別。</span><span class="sxs-lookup"><span data-stu-id="34c04-343">This code shows you the basic pattern &mdash; different parameters for the `GetHtml` method let you reference CSS classes that the method then generates along with the markup.</span></span> <span data-ttu-id="34c04-344">您對 CSS 類別的作用是由您決定。</span><span class="sxs-lookup"><span data-stu-id="34c04-344">What you do with the CSS classes is up to you.</span></span>

## <a name="adding-paging"></a><span data-ttu-id="34c04-345">加入分頁</span><span class="sxs-lookup"><span data-stu-id="34c04-345">Adding Paging</span></span>

<span data-ttu-id="34c04-346">做為本教學課程的最後一項工作，您會將分頁加入至方格。</span><span class="sxs-lookup"><span data-stu-id="34c04-346">As the last task for this tutorial, you'll add paging to the grid.</span></span> <span data-ttu-id="34c04-347">現在就不會發生任何問題，同時顯示所有電影。</span><span class="sxs-lookup"><span data-stu-id="34c04-347">Right now it's no problem to display all your movies at once.</span></span> <span data-ttu-id="34c04-348">但是，如果您新增了數百個電影，頁面顯示會變長。</span><span class="sxs-lookup"><span data-stu-id="34c04-348">But if you added hundreds of movies, the page display would get long.</span></span>

<span data-ttu-id="34c04-349">在頁面程式碼中，將建立 `WebGrid` 物件的那一行變更為下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="34c04-349">In the page code, change the line that creates the `WebGrid` object to the following code:</span></span>

[!code-csharp[Main](displaying-data/samples/sample7.cs)]

<span data-ttu-id="34c04-350">與之前的唯一差異在於，您已加入設定為3的 `rowsPerPage` 參數。</span><span class="sxs-lookup"><span data-stu-id="34c04-350">The only difference from before is that you've added a `rowsPerPage` parameter that's set to 3.</span></span>

<span data-ttu-id="34c04-351">執行頁面。</span><span class="sxs-lookup"><span data-stu-id="34c04-351">Run the page.</span></span> <span data-ttu-id="34c04-352">方格一次會顯示3個數據列，再加上導覽連結，讓您逐頁流覽資料庫中的電影：</span><span class="sxs-lookup"><span data-stu-id="34c04-352">The grid displays 3 rows at a time, plus navigation links that let you page through the movies in your database:</span></span>

![WebGrid 顯示與分頁](displaying-data/_static/image21.png)

## <a name="coming-up-next"></a><span data-ttu-id="34c04-354">下一步</span><span class="sxs-lookup"><span data-stu-id="34c04-354">Coming Up Next</span></span>

<span data-ttu-id="34c04-355">在下一個教學課程中，您將瞭解如何使用 Razor C#和程式碼來取得表單中的使用者輸入。</span><span class="sxs-lookup"><span data-stu-id="34c04-355">In the next tutorial, you'll learn how to use Razor and C# code to get user input in a form.</span></span> <span data-ttu-id="34c04-356">您會在 [電影] 頁面中新增搜尋方塊，讓您可以依標題或內容類型來尋找電影。</span><span class="sxs-lookup"><span data-stu-id="34c04-356">You'll add a search box to the Movies page so that you can find movies by title or genre.</span></span>

## <a name="complete-listing-for-movies-page"></a><span data-ttu-id="34c04-357">電影的完整清單頁面</span><span class="sxs-lookup"><span data-stu-id="34c04-357">Complete Listing for Movies Page</span></span>

[!code-cshtml[Main](displaying-data/samples/sample8.cshtml)]

## <a name="additional-resources"></a><span data-ttu-id="34c04-358">其他資源</span><span class="sxs-lookup"><span data-stu-id="34c04-358">Additional Resources</span></span>

- [<span data-ttu-id="34c04-359">使用 Razor 語法 ASP.NET Web 程式設計的簡介</span><span class="sxs-lookup"><span data-stu-id="34c04-359">Introduction to ASP.NET Web Programming Using the Razor Syntax</span></span>](https://go.microsoft.com/fwlink/?LinkID=202890)

> [!div class="step-by-step"]
> <span data-ttu-id="34c04-360">[上一頁](intro-to-web-pages-programming.md)
> [下一頁](form-basics.md)</span><span class="sxs-lookup"><span data-stu-id="34c04-360">[Previous](intro-to-web-pages-programming.md)
[Next](form-basics.md)</span></span>
