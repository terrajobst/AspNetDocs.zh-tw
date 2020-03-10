---
uid: web-pages/overview/data/5-working-with-data
title: 在 ASP.NET Web Pages （Razor）網站中使用資料庫的簡介 |Microsoft Docs
author: Rick-Anderson
description: 本章說明如何從資料庫存取資料，並使用 ASP.NET Web Pages 加以顯示。
ms.author: riande
ms.date: 02/18/2014
ms.assetid: 673d502f-2c16-4a6f-bb63-dbfd9a77ef47
msc.legacyurl: /web-pages/overview/data/5-working-with-data
msc.type: authoredcontent
ms.openlocfilehash: 45e988d037465e59ad352bb9444af2c69fd3cd70
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78586531"
---
# <a name="introduction-to-working-with-a-database-in-aspnet-web-pages-razor-sites"></a><span data-ttu-id="d8ac2-103">在 ASP.NET Web Pages （Razor）網站中使用資料庫的簡介</span><span class="sxs-lookup"><span data-stu-id="d8ac2-103">Introduction to Working with a Database in ASP.NET Web Pages (Razor) Sites</span></span>

<span data-ttu-id="d8ac2-104">由[Tom FitzMacken](https://github.com/tfitzmac)</span><span class="sxs-lookup"><span data-stu-id="d8ac2-104">by [Tom FitzMacken](https://github.com/tfitzmac)</span></span>

> <span data-ttu-id="d8ac2-105">本文說明如何使用 Microsoft WebMatrix 工具在 ASP.NET Web Pages （Razor）網站中建立資料庫，以及如何建立可讓您顯示、新增、編輯和刪除資料的頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-105">This article describes how to use Microsoft WebMatrix tools to create a database in an ASP.NET Web Pages (Razor) website, and how to create pages that let you display, add, edit, and delete data.</span></span>
> 
> <span data-ttu-id="d8ac2-106">**您將瞭解的內容：**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-106">**What you'll learn:**</span></span> 
> 
> - <span data-ttu-id="d8ac2-107">如何建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-107">How to create a database.</span></span>
> - <span data-ttu-id="d8ac2-108">如何連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-108">How to connect to a database.</span></span>
> - <span data-ttu-id="d8ac2-109">如何在網頁中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-109">How to display data in a web page.</span></span>
> - <span data-ttu-id="d8ac2-110">如何插入、更新和刪除資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-110">How to insert, update, and delete database records.</span></span>
> 
> <span data-ttu-id="d8ac2-111">以下是文章中引進的功能：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-111">These are the features introduced in the article:</span></span>
> 
> - <span data-ttu-id="d8ac2-112">使用 Microsoft SQL Server Compact 版本資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-112">Working with a Microsoft SQL Server Compact Edition database.</span></span>
> - <span data-ttu-id="d8ac2-113">使用 SQL 查詢。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-113">Working with SQL queries.</span></span>
> - <span data-ttu-id="d8ac2-114">`Database` 類別。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-114">The `Database` class.</span></span>
>   
> 
> ## <a name="software-versions-used-in-the-tutorial"></a><span data-ttu-id="d8ac2-115">教學課程中使用的軟體版本</span><span class="sxs-lookup"><span data-stu-id="d8ac2-115">Software versions used in the tutorial</span></span>
> 
> 
> - <span data-ttu-id="d8ac2-116">ASP.NET Web Pages （Razor）2</span><span class="sxs-lookup"><span data-stu-id="d8ac2-116">ASP.NET Web Pages (Razor) 2</span></span>
> - <span data-ttu-id="d8ac2-117">WebMatrix 2</span><span class="sxs-lookup"><span data-stu-id="d8ac2-117">WebMatrix 2</span></span>
>   
> 
> <span data-ttu-id="d8ac2-118">本教學課程也適用于 WebMatrix 3。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-118">This tutorial also works with WebMatrix 3.</span></span> <span data-ttu-id="d8ac2-119">您可以使用 ASP.NET Web Pages 3 和 Visual Studio 2013 （或適用于 Web 的 Visual Studio Express 2013）;不過，使用者介面將會不同。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-119">You can use ASP.NET Web Pages 3 and Visual Studio 2013 (or Visual Studio Express 2013 for Web); however, the user interface will be different.</span></span>

## <a name="introduction-to-databases"></a><span data-ttu-id="d8ac2-120">資料庫簡介</span><span class="sxs-lookup"><span data-stu-id="d8ac2-120">Introduction to Databases</span></span>

<span data-ttu-id="d8ac2-121">想像一下一般通訊錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-121">Imagine a typical address book.</span></span> <span data-ttu-id="d8ac2-122">針對通訊錄中的每個專案（亦即，針對每個人），您會有數個資訊片段，例如名字、姓氏、位址、電子郵件地址和電話號碼。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-122">For each entry in the address book (that is, for each person) you have several pieces of information such as first name, last name, address, email address, and phone number.</span></span>

<span data-ttu-id="d8ac2-123">以這種方式進行資料圖片的一般方法，就像是具有資料列和資料行的資料表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-123">A typical way to picture data like this is as a table with rows and columns.</span></span> <span data-ttu-id="d8ac2-124">在資料庫詞彙中，每個資料列通常稱為「記錄」。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-124">In database terms, each row is often referred to as a record.</span></span> <span data-ttu-id="d8ac2-125">每個資料行（有時稱為「欄位」）都會包含每個資料類型的值：「名字」、「姓氏」等等。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-125">Each column (sometimes referred to as fields) contains a value for each type of data: first name, last name, and so on.</span></span>

| <span data-ttu-id="d8ac2-126">**ID**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-126">**ID**</span></span> | <span data-ttu-id="d8ac2-127">**FirstName**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-127">**FirstName**</span></span> | <span data-ttu-id="d8ac2-128">**姓氏**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-128">**LastName**</span></span> | <span data-ttu-id="d8ac2-129">**位址**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-129">**Address**</span></span> | <span data-ttu-id="d8ac2-130">**電子郵件**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-130">**Email**</span></span> | <span data-ttu-id="d8ac2-131">**電話**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-131">**Phone**</span></span> |
| --- | --- | --- | --- | --- | --- |
| <span data-ttu-id="d8ac2-132">1</span><span class="sxs-lookup"><span data-stu-id="d8ac2-132">1</span></span> | <span data-ttu-id="d8ac2-133">Jim</span><span class="sxs-lookup"><span data-stu-id="d8ac2-133">Jim</span></span> | <span data-ttu-id="d8ac2-134">Abrus</span><span class="sxs-lookup"><span data-stu-id="d8ac2-134">Abrus</span></span> | <span data-ttu-id="d8ac2-135">210第100個 St SE Orcas WA 98031</span><span class="sxs-lookup"><span data-stu-id="d8ac2-135">210 100th St SE Orcas WA 98031</span></span> | jim@contoso.com | <span data-ttu-id="d8ac2-136">555 0100</span><span class="sxs-lookup"><span data-stu-id="d8ac2-136">555 0100</span></span> |
| <span data-ttu-id="d8ac2-137">2</span><span class="sxs-lookup"><span data-stu-id="d8ac2-137">2</span></span> | <span data-ttu-id="d8ac2-138">Terry</span><span class="sxs-lookup"><span data-stu-id="d8ac2-138">Terry</span></span> | <span data-ttu-id="d8ac2-139">Adams</span><span class="sxs-lookup"><span data-stu-id="d8ac2-139">Adams</span></span> | <span data-ttu-id="d8ac2-140">1234主要 St. 西雅圖 WA 99011</span><span class="sxs-lookup"><span data-stu-id="d8ac2-140">1234 Main St. Seattle WA 99011</span></span> | terry@cohowinery.com | <span data-ttu-id="d8ac2-141">555 0101</span><span class="sxs-lookup"><span data-stu-id="d8ac2-141">555 0101</span></span> |

<span data-ttu-id="d8ac2-142">對於大部分的資料庫資料表而言，資料表必須有一個包含唯一識別碼的資料行，例如客戶編碼、帳戶號碼等等。這就是所謂的資料表*主鍵*，您可以用它來識別資料表中的每個資料列。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-142">For most database tables, the table has to have a column that contains a unique identifier, like a customer number, account number, etc. This is known as the table's *primary key*, and you use it to identify each row in the table.</span></span> <span data-ttu-id="d8ac2-143">在此範例中，[識別碼] 資料行是通訊錄的主要金鑰。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-143">In the example, the ID column is the primary key for the address book.</span></span>

<span data-ttu-id="d8ac2-144">有了對資料庫的基本瞭解之後，您就可以開始學習如何建立簡單的資料庫，並執行新增、修改和刪除資料等作業。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-144">With this basic understanding of databases, you're ready to learn how to create a simple database and perform operations such as adding, modifying, and deleting data.</span></span>

> [!TIP] 
> 
> <span data-ttu-id="d8ac2-145">**關聯式資料庫**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-145">**Relational Databases**</span></span>
> 
> <span data-ttu-id="d8ac2-146">您可以用許多方式來儲存資料，包括文字檔和試算表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-146">You can store data in lots of ways, including text files and spreadsheets.</span></span> <span data-ttu-id="d8ac2-147">不過，對於大部分的企業用途而言，資料會儲存在關係資料庫中。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-147">For most business uses, though, data is stored in a relational database.</span></span>
> 
> <span data-ttu-id="d8ac2-148">本文不會深入探討資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-148">This article doesn't go very deeply into databases.</span></span> <span data-ttu-id="d8ac2-149">不過，您可能會發現很難瞭解。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-149">However, you might find it useful to understand a little about them.</span></span> <span data-ttu-id="d8ac2-150">在關係資料庫中，資訊會以邏輯方式分割成不同的資料表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-150">In a relational database, information is logically divided into separate tables.</span></span> <span data-ttu-id="d8ac2-151">例如，學校的資料庫可能包含學生的個別資料表和類別供應專案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-151">For example, a database for a school might contain separate tables for students and for class offerings.</span></span> <span data-ttu-id="d8ac2-152">資料庫軟體（例如 SQL Server）支援強大的命令，可讓您以動態方式建立資料表之間的關聯性。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-152">The database software (such as SQL Server) supports powerful commands that let you dynamically establish relationships between the tables.</span></span> <span data-ttu-id="d8ac2-153">例如，您可以使用關係資料庫來建立學生與類別之間的邏輯關聯性，以便建立排程。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-153">For example, you can use the relational database to establish a logical relationship between students and classes in order to create a schedule.</span></span> <span data-ttu-id="d8ac2-154">將資料儲存在不同的資料表中可減少資料表結構的複雜性，並減少在資料表中保留多餘資料的需求。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-154">Storing data in separate tables reduces the complexity of the table structure and reduces the need to keep redundant data in tables.</span></span>

## <a name="creating-a-database"></a><span data-ttu-id="d8ac2-155">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="d8ac2-155">Creating a Database</span></span>

<span data-ttu-id="d8ac2-156">此程式說明如何使用 WebMatrix 隨附的 SQL Server Compact 資料庫設計工具，建立名為 SmallBakery 的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-156">This procedure shows you how to create a database named SmallBakery by using the SQL Server Compact Database design tool that's included in WebMatrix.</span></span> <span data-ttu-id="d8ac2-157">雖然您可以使用程式碼建立資料庫，但更常見的做法是使用 WebMatrix 之類的設計工具來建立資料庫和資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-157">Although you can create a database using code, it's more typical to create the database and database tables using a design tool like WebMatrix.</span></span>

1. <span data-ttu-id="d8ac2-158">啟動 WebMatrix，然後在 [快速入門] 頁面上，按一下 [**來自範本的網站**]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-158">Start WebMatrix, and on the Quick Start page, click **Site From Template**.</span></span>
2. <span data-ttu-id="d8ac2-159">選取 [**空白網站**]，然後在 [**網站名稱**] 方塊中輸入 "SmallBakery"，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-159">Select **Empty Site**, and in the **Site Name** box enter "SmallBakery" and then click **OK**.</span></span> <span data-ttu-id="d8ac2-160">網站隨即建立，並顯示在 WebMatrix 中。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-160">The site is created and displayed in WebMatrix.</span></span>
3. <span data-ttu-id="d8ac2-161">在左窗格中，按一下 [**資料庫**] 工作區。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-161">In the left pane, click the **Databases** workspace.</span></span>
4. <span data-ttu-id="d8ac2-162">在功能區中，按一下 [**新增資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-162">In the ribbon, click **New Database**.</span></span> <span data-ttu-id="d8ac2-163">系統會使用與您的網站相同的名稱來建立空的資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-163">An empty database is created with the same name as your site.</span></span>
5. <span data-ttu-id="d8ac2-164">在左窗格中，展開 [ **SmallBakery** ] 節點，然後按一下 [**資料表]** 。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-164">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
6. <span data-ttu-id="d8ac2-165">在功能區中，按一下 [**新增資料表**]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-165">In the ribbon, click **New Table**.</span></span> <span data-ttu-id="d8ac2-166">WebMatrix 會開啟 [資料表設計工具]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-166">WebMatrix opens the table designer.</span></span>

    ![[影像]](5-working-with-data/_static/image1.jpg)
7. <span data-ttu-id="d8ac2-168">按一下 [**名稱**] 資料行，然後輸入 &quot;識別碼&quot;。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-168">Click in the **Name** column and enter &quot;Id&quot;.</span></span>
8. <span data-ttu-id="d8ac2-169">在 [**資料類型] 資料**行中，選取 [ **int**]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-169">In the **Data Type** column, select **int**.</span></span>
9. <span data-ttu-id="d8ac2-170">設定 [**是主要金鑰嗎？** ] 和 [**識別**] 選項為 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-170">Set the **Is Primary Key?** and **Is Identify?** options to **Yes**.</span></span>

    <span data-ttu-id="d8ac2-171">如其名稱所示， **Primary key**會告訴資料庫這將是資料表的主鍵。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-171">As the name suggests, **Is Primary Key** tells the database that this will be the table's primary key.</span></span> <span data-ttu-id="d8ac2-172">[身分**識別] 會**告訴資料庫自動建立每個新記錄的識別碼，並將下一個序號指派給它（從1開始）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-172">**Is Identity** tells the database to automatically create an ID number for every new record and to assign it the next sequential number (starting at 1).</span></span>
10. <span data-ttu-id="d8ac2-173">按一下下一個資料列。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-173">Click in the next row.</span></span> <span data-ttu-id="d8ac2-174">編輯器會啟動新的資料行定義。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-174">The editor starts a new column definition.</span></span>
11. <span data-ttu-id="d8ac2-175">在 [名稱] 值中，輸入 &quot;名稱&quot;。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-175">For the Name value, enter &quot;Name&quot;.</span></span>
12. <span data-ttu-id="d8ac2-176">針對 [**資料類型**]，選擇 [&quot;Nvarchar&quot;]，並將 [長度] 設定為50。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-176">For **Data Type**, choose &quot;nvarchar&quot; and set the length to 50.</span></span> <span data-ttu-id="d8ac2-177">`nvarchar` 的*var*部分會告訴資料庫，此資料行的資料會是字串，其大小可能會因記錄而異。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-177">The *var* part of `nvarchar` tells the database that the data for this column will be a string whose size might vary from record to record.</span></span> <span data-ttu-id="d8ac2-178">（ *N*前置詞代表*國家（地區*），表示欄位可以保存代表任何字母或書寫系統&#8212;的字元資料，也就是欄位保留 Unicode 資料）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-178">(The *n* prefix represents *national*, indicating that the field can hold character data that represents any alphabet or writing system &#8212; that is, that the field holds Unicode data.)</span></span>
13. <span data-ttu-id="d8ac2-179">將 [**允許 Null]** 選項設為 [**否**]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-179">Set the **Allow Nulls** option to **No**.</span></span> <span data-ttu-id="d8ac2-180">這會強制 [*名稱*] 資料行不會保留空白。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-180">This will enforce that the *Name* column is not left blank.</span></span>
14. <span data-ttu-id="d8ac2-181">使用此相同進程，建立名為*Description*的資料行。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-181">Using this same process, create a column named *Description*.</span></span> <span data-ttu-id="d8ac2-182">將 [**資料類型**] 設定為 [Nvarchar]，並將 [長度] 設定為50，並將 [**允許 null]** 設為 false</span><span class="sxs-lookup"><span data-stu-id="d8ac2-182">Set **Data Type** to "nvarchar" and 50 for the length, and set **Allow Nulls** to false.</span></span>
15. <span data-ttu-id="d8ac2-183">建立名為*Price*的資料行。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-183">Create a column named *Price*.</span></span> <span data-ttu-id="d8ac2-184">將 **[資料類型] 設定為 [money]** ，並將 [**允許 null]** 設定為 false。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-184">Set **Data Type to "money"** and set **Allow Nulls** to false.</span></span>
16. <span data-ttu-id="d8ac2-185">在頂端的方塊中，將資料表命名為 &quot;產品&quot;。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-185">In the box at the top, name the table &quot;Product&quot;.</span></span>

    <span data-ttu-id="d8ac2-186">當您完成時，定義看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-186">When you're done, the definition will look like this:</span></span>

    ![[影像]](5-working-with-data/_static/image2.png)
17. <span data-ttu-id="d8ac2-188">按 Ctrl + S 以儲存資料表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-188">Press Ctrl+S to save the table.</span></span>

## <a name="adding-data-to-the-database"></a><span data-ttu-id="d8ac2-189">將資料新增至資料庫</span><span class="sxs-lookup"><span data-stu-id="d8ac2-189">Adding Data to the Database</span></span>

<span data-ttu-id="d8ac2-190">現在您可以將一些範例資料新增至您的資料庫，以便稍後在本文中使用。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-190">Now you can add some sample data to your database that you'll work with later in the article.</span></span>

1. <span data-ttu-id="d8ac2-191">在左窗格中，展開 [ **SmallBakery** ] 節點，然後按一下 [**資料表]** 。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-191">In the left pane, expand the **SmallBakery.sdf** node and then click **Tables**.</span></span>
2. <span data-ttu-id="d8ac2-192">以滑鼠右鍵按一下 [Product] 資料表，然後按一下 [**資料**]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-192">Right-click the Product table and then click **Data**.</span></span>
3. <span data-ttu-id="d8ac2-193">在 [編輯] 窗格中，輸入下列記錄：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-193">In the edit pane, enter the following records:</span></span>

    | <span data-ttu-id="d8ac2-194">**名稱**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-194">**Name**</span></span> | <span data-ttu-id="d8ac2-195">**說明**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-195">**Description**</span></span> | <span data-ttu-id="d8ac2-196">**高價**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-196">**Price**</span></span> |
    | --- | --- | --- |
    | <span data-ttu-id="d8ac2-197">麵包</span><span class="sxs-lookup"><span data-stu-id="d8ac2-197">Bread</span></span> | <span data-ttu-id="d8ac2-198">每天內建全新的。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-198">Baked fresh every day.</span></span> | <span data-ttu-id="d8ac2-199">2.99</span><span class="sxs-lookup"><span data-stu-id="d8ac2-199">2.99</span></span> |
    | <span data-ttu-id="d8ac2-200">草莓 Shortcake</span><span class="sxs-lookup"><span data-stu-id="d8ac2-200">Strawberry Shortcake</span></span> | <span data-ttu-id="d8ac2-201">以我們的花園的有機 strawberries 進行。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-201">Made with organic strawberries from our garden.</span></span> | <span data-ttu-id="d8ac2-202">9.99</span><span class="sxs-lookup"><span data-stu-id="d8ac2-202">9.99</span></span> |
    | <span data-ttu-id="d8ac2-203">Apple 圓形圖</span><span class="sxs-lookup"><span data-stu-id="d8ac2-203">Apple Pie</span></span> | <span data-ttu-id="d8ac2-204">第二個僅適用于您的 mom 圓形圖。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-204">Second only to your mom's pie.</span></span> | <span data-ttu-id="d8ac2-205">12.99</span><span class="sxs-lookup"><span data-stu-id="d8ac2-205">12.99</span></span> |
    | <span data-ttu-id="d8ac2-206">Pecan 圓形圖</span><span class="sxs-lookup"><span data-stu-id="d8ac2-206">Pecan Pie</span></span> | <span data-ttu-id="d8ac2-207">如果您喜歡 pecans，這是為您提供的。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-207">If you like pecans, this is for you.</span></span> | <span data-ttu-id="d8ac2-208">10.99</span><span class="sxs-lookup"><span data-stu-id="d8ac2-208">10.99</span></span> |
    | <span data-ttu-id="d8ac2-209">檸檬圓形圖</span><span class="sxs-lookup"><span data-stu-id="d8ac2-209">Lemon Pie</span></span> | <span data-ttu-id="d8ac2-210">以全世界的最佳 lemons 進行。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-210">Made with the best lemons in the world.</span></span> | <span data-ttu-id="d8ac2-211">11.99</span><span class="sxs-lookup"><span data-stu-id="d8ac2-211">11.99</span></span> |
    | <span data-ttu-id="d8ac2-212">杯子蛋糕</span><span class="sxs-lookup"><span data-stu-id="d8ac2-212">Cupcakes</span></span> | <span data-ttu-id="d8ac2-213">您的孩子和小孩將會很愛。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-213">Your kids and the kid in you will love these.</span></span> | <span data-ttu-id="d8ac2-214">7.99</span><span class="sxs-lookup"><span data-stu-id="d8ac2-214">7.99</span></span> |

    <span data-ttu-id="d8ac2-215">請記住，您不需要針對 [*識別碼*] 資料行輸入任何內容。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-215">Remember that you don't have to enter anything for the *Id* column.</span></span> <span data-ttu-id="d8ac2-216">當您建立*Id*資料行時，會將其**Is Identity**屬性設定為 true，這會使其自動填入。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-216">When you created the *Id* column, you set its **Is Identity** property to true, which causes it to automatically be filled in.</span></span>

    <span data-ttu-id="d8ac2-217">當您完成輸入資料時，[資料表設計工具] 看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-217">When you're finished entering the data, the table designer will look like this:</span></span>

    ![[影像]](5-working-with-data/_static/image3.jpg)
4. <span data-ttu-id="d8ac2-219">關閉包含資料庫資料的索引標籤。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-219">Close the tab that contains the database data.</span></span>

## <a name="displaying-data-from-a-database"></a><span data-ttu-id="d8ac2-220">顯示資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="d8ac2-220">Displaying Data from a Database</span></span>

<span data-ttu-id="d8ac2-221">一旦資料庫中有資料之後，您就可以在 ASP.NET 網頁中顯示資料。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-221">Once you've got a database with data in it, you can display the data in an ASP.NET web page.</span></span> <span data-ttu-id="d8ac2-222">若要選取要顯示的資料表資料列，您可以使用 SQL 語句，這是您傳遞給資料庫的命令。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-222">To select the table rows to display, you use a SQL statement, which is a command that you pass to the database.</span></span>

1. <span data-ttu-id="d8ac2-223">在左窗格中，按一下 [檔案]**工作區。**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-223">In the left pane, click the **Files** workspace.</span></span>
2. <span data-ttu-id="d8ac2-224">在網站的根目錄中，建立名為*ListProducts*的新 CSHTML 頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-224">In the root of the website, create a new CSHTML page named *ListProducts.cshtml*.</span></span>
3. <span data-ttu-id="d8ac2-225">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-225">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample1.cshtml)]

    <span data-ttu-id="d8ac2-226">在第一個程式碼區塊中，開啟您稍早建立的*SmallBakery .sdf*檔案（資料庫）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-226">In the first code block, you open the *SmallBakery.sdf* file (database) that you created earlier.</span></span> <span data-ttu-id="d8ac2-227">`Database.Open` 方法假設 *.sdf*檔案位於您網站的*應用程式\_Data*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-227">The `Database.Open` method assumes that the *.sdf* file is in your website's *App\_Data* folder.</span></span> <span data-ttu-id="d8ac2-228">（請注意，您不需要指定 *.sdf*副檔名&#8212; ，事實上，如果您這樣做，`Open` 方法將無法使用）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-228">(Notice that you don't need to specify the *.sdf* extension &#8212; in fact, if you do, the `Open` method won't work.)</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8ac2-229">*應用程式\_Data*資料夾是 ASP.NET 中用來儲存資料檔案的特殊資料夾。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-229">The *App\_Data* folder is a special folder in ASP.NET that's used to store data files.</span></span> <span data-ttu-id="d8ac2-230">如需詳細資訊，請參閱本文稍後的[連接到資料庫](#SB_ConnectingToADatabase)。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-230">For more information, see [Connecting to a Database](#SB_ConnectingToADatabase) later in this article.</span></span>

    <span data-ttu-id="d8ac2-231">接著，您可以使用下列 SQL `Select` 語句，提出查詢資料庫的要求：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-231">You then make a request to query the database using the following SQL `Select` statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample2.sql)]

    <span data-ttu-id="d8ac2-232">在語句中，`Product` 會識別要查詢的資料表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-232">In the statement, `Product` identifies the table to query.</span></span> <span data-ttu-id="d8ac2-233">`*` 字元指定查詢應傳回資料表中的所有資料行。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-233">The `*` character specifies that the query should return all the columns from the table.</span></span> <span data-ttu-id="d8ac2-234">（如果您只想查看部分資料行，您也可以個別列出資料行，並以逗號分隔。）`Order By` 子句會指出在此情況下，應該&#8212;如何以*名稱*資料行來排序資料。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-234">(You could also list columns individually, separated by commas, if you wanted to see only some of the columns.) The `Order By` clause indicates how the data should be sorted &#8212; in this case, by the *Name* column.</span></span> <span data-ttu-id="d8ac2-235">這表示資料會依照每個資料列的*名稱*資料行的值依字母順序排序。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-235">This means that the data is sorted alphabetically based on the value of the *Name* column for each row.</span></span>

    <span data-ttu-id="d8ac2-236">在頁面的主體中，標記會建立用來顯示資料的 HTML 資料表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-236">In the body of the page, the markup creates an HTML table that will be used to display the data.</span></span> <span data-ttu-id="d8ac2-237">在 `<tbody>` 元素內，您可以使用 `foreach` 迴圈，個別取得查詢所傳回的每個資料列。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-237">Inside the `<tbody>` element, you use a `foreach` loop to individually get each data row that's returned by the query.</span></span> <span data-ttu-id="d8ac2-238">針對每個資料列，您會建立一個 HTML 資料表列（`<tr>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-238">For each data row, you create an HTML table row (`<tr>` element).</span></span> <span data-ttu-id="d8ac2-239">接著，您會為每個資料行建立 HTML 資料表單元格（`<td>` 元素）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-239">Then you create HTML table cells (`<td>` elements) for each column.</span></span> <span data-ttu-id="d8ac2-240">每次執行迴圈時，資料庫中下一個可用的資料列會位於 `row` 變數中（您會在 `foreach` 語句中設定此項）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-240">Each time you go through the loop, the next available row from the database is in the `row` variable (you set this up in the `foreach` statement).</span></span> <span data-ttu-id="d8ac2-241">若要從資料列取得個別的資料行，您可以使用 `row.Name` 或 `row.Description` 或任何名稱是您想要的資料行。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-241">To get an individual column from the row, you can use `row.Name` or `row.Description` or whatever the name is of the column you want.</span></span>
4. <span data-ttu-id="d8ac2-242">在瀏覽器中執行頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-242">Run the page in a browser.</span></span> <span data-ttu-id="d8ac2-243">（在執行之前，請確定已在 [檔案 **] 工作區**中選取頁面。）此頁面會顯示如下所示的清單：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-243">(Make sure the page is selected in the **Files** workspace before you run it.) The page displays a list like the following:</span></span>

    ![[影像]](5-working-with-data/_static/image4.jpg)

> [!TIP] 
> 
> <span data-ttu-id="d8ac2-245">**結構化查詢語言 (SQL)**</span><span class="sxs-lookup"><span data-stu-id="d8ac2-245">**Structured Query Language (SQL)**</span></span>
> 
> <span data-ttu-id="d8ac2-246">SQL 是一種語言，用於大部分關係資料庫中，用來管理資料庫中的資料。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-246">SQL is a language that's used in most relational databases for managing data in a database.</span></span> <span data-ttu-id="d8ac2-247">其中包含的命令可讓您抓取資料並加以更新，並可讓您建立、修改和管理資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-247">It includes commands that let you retrieve data and update it, and that let you create, modify, and manage database tables.</span></span> <span data-ttu-id="d8ac2-248">SQL 與程式設計語言（例如您在 WebMatrix 中使用的語言）不同，因為在 SQL 中，其概念是告訴資料庫您所需的內容，以及資料庫的工作，以瞭解如何取得資料或執行工作。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-248">SQL is different than a programming language (like the one you're using in WebMatrix) because with SQL, the idea is that you tell the database what you want, and it's the database's job to figure out how to get the data or perform the task.</span></span> <span data-ttu-id="d8ac2-249">以下是一些 SQL 命令的範例，以及它們的作用：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-249">Here are examples of some SQL commands and what they do:</span></span>
> 
> `SELECT Id, Name, Price FROM Product WHERE Price > 10.00 ORDER BY Name`
> 
> <span data-ttu-id="d8ac2-250">這會從*Product*資料表中的記錄提取*識別碼*、*名稱*和*價格*資料行（如果*Price*的值大於10），並根據*名稱*資料行的值，以字母順序傳回結果。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-250">This fetches the *Id*, *Name*, and *Price* columns from records in the *Product* table if the value of *Price* is more than 10, and returns the results in alphabetical order based on the values of the *Name* column.</span></span> <span data-ttu-id="d8ac2-251">此命令會傳回包含符合準則之記錄的結果集，如果沒有任何記錄符合，則傳回空的集合。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-251">This command will return a result set that contains the records that meet the criteria, or an empty set if no records match.</span></span>
> 
> `INSERT INTO Product (Name, Description, Price) VALUES ("Croissant", "A flaky delight", 1.99)`
> 
> <span data-ttu-id="d8ac2-252">這會在 [ *Product* ] 資料表中插入新的記錄，將 [*名稱*] 資料行設定為 &quot;可頌麵包&quot;、[*描述*] 資料行 &quot;不穩定取悅&quot;，並將 [價格] 設為1.99。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-252">This inserts a new record into the *Product* table, setting the *Name* column to &quot;Croissant&quot;, the *Description* column to &quot;A flaky delight&quot;, and the price to 1.99.</span></span>
> 
> `DELETE FROM Product WHERE ExpirationDate < "01/01/2008"`
> 
> <span data-ttu-id="d8ac2-253">此命令會刪除*產品*資料表中，其到期日資料行早于2008年1月1日的記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-253">This command deletes records in the *Product* table whose expiration date column is earlier than January 1, 2008.</span></span> <span data-ttu-id="d8ac2-254">（這是假設*Product*資料表有這類資料行）。以 MM/DD/YYYY 格式輸入日期，但應以用於地區設定的格式輸入。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-254">(This assumes that the *Product* table has such a column, of course.) The date is entered here in MM/DD/YYYY format, but it should be entered in the format that's used for your locale.</span></span>
> 
> <span data-ttu-id="d8ac2-255">`Insert Into` 和 `Delete` 命令不會傳回結果集。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-255">The `Insert Into` and `Delete` commands don't return result sets.</span></span> <span data-ttu-id="d8ac2-256">相反地，它們會傳回一個數位，告訴您命令有多少記錄受到影響。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-256">Instead, they return a number that tells you how many records were affected by the command.</span></span>
> 
> <span data-ttu-id="d8ac2-257">對於其中某些作業（例如插入和刪除記錄），要求操作的進程必須在資料庫中擁有適當的許可權。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-257">For some of these operations (like inserting and deleting records), the process that's requesting the operation has to have appropriate permissions in the database.</span></span> <span data-ttu-id="d8ac2-258">這就是當您連接到資料庫時，生產資料庫經常需要提供使用者名稱和密碼的原因。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-258">This is why for production databases you often have to supply a username and password when you connect to the database.</span></span>
> 
> <span data-ttu-id="d8ac2-259">有數十個 SQL 命令，但它們都遵循類似的模式。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-259">There are dozens of SQL commands, but they all follow a pattern like this.</span></span> <span data-ttu-id="d8ac2-260">您可以使用 SQL 命令來建立資料庫資料表、計算資料表中的記錄數目、計算價格，以及執行許多其他作業。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-260">You can use SQL commands to create database tables, count the number of records in a table, calculate prices, and perform many more operations.</span></span>

## <a name="inserting-data-in-a-database"></a><span data-ttu-id="d8ac2-261">在資料庫中插入資料</span><span class="sxs-lookup"><span data-stu-id="d8ac2-261">Inserting Data in a Database</span></span>

<span data-ttu-id="d8ac2-262">本節說明如何建立可讓使用者將新產品加入至*產品*資料庫資料表的頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-262">This section shows how to create a page that lets users add a new product to the *Product* database table.</span></span> <span data-ttu-id="d8ac2-263">插入新的產品記錄後，頁面會使用您在上一節中建立的*ListProducts*頁面來顯示更新的資料表。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-263">After a new product record is inserted, the page displays the updated table using the *ListProducts.cshtml* page that you created in the previous section.</span></span>

<span data-ttu-id="d8ac2-264">此頁面包含驗證，以確保使用者輸入的資料對於資料庫而言是有效的。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-264">The page includes validation to make sure that the data that the user enters is valid for the database.</span></span> <span data-ttu-id="d8ac2-265">例如，頁面中的程式碼會確定已針對所有必要的資料行輸入值。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-265">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>

1. <span data-ttu-id="d8ac2-266">在網站中，建立名為*InsertProducts*的新 CSHTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-266">In the website, create a new CSHTML file named *InsertProducts.cshtml*.</span></span>
2. <span data-ttu-id="d8ac2-267">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-267">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample3.cshtml)]

    <span data-ttu-id="d8ac2-268">頁面的本文包含一個 HTML 表單，內含三個文字方塊，可讓使用者輸入名稱、描述和價格。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-268">The body of the page contains an HTML form with three text boxes that let users enter a name, description, and price.</span></span> <span data-ttu-id="d8ac2-269">當使用者按一下 [**插入**] 按鈕時，頁面頂端的程式碼會開啟與*SmallBakery*資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-269">When users click the **Insert** button, the code at the top of the page opens a connection to the *SmallBakery.sdf* database.</span></span> <span data-ttu-id="d8ac2-270">接著，您可以使用 `Request` 物件來取得使用者已提交的值，並將這些值指派給區域變數。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-270">You then get the values that the user has submitted by using the `Request` object and assign those values to local variables.</span></span>

    <span data-ttu-id="d8ac2-271">若要驗證使用者是否為每個必要的資料行輸入值，請註冊您要驗證的每個 `<input>` 元素：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-271">To validate that the user entered a value for each required column, you register each `<input>` element that you want to validate:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample4.cs)]

    <span data-ttu-id="d8ac2-272">`Validation` helper 會檢查您已註冊的每個欄位中是否有一個值。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-272">The `Validation` helper checks that there is a value in each of the fields that you've registered.</span></span> <span data-ttu-id="d8ac2-273">您可以藉由檢查 `Validation.IsValid()`來測試所有欄位是否通過驗證，這通常會在處理您從使用者取得的資訊之前執行：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-273">You can test whether all the fields passed validation by checking `Validation.IsValid()`, which you typically do before you process the information you get from the user:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample5.cs)]

    <span data-ttu-id="d8ac2-274">（`&&` 運算子表示和-這種測試是指*提交表單，而且所有欄位都已通過驗證*）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-274">(The `&&` operator means AND — this test is *If this is a form submission AND all the fields have passed validation*.)</span></span>

    <span data-ttu-id="d8ac2-275">如果所有資料行都已驗證（不是空的），您可以繼續並建立 SQL 語句來插入資料，然後執行它，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-275">If all the columns validated (none were empty), you go ahead and create a SQL statement to insert the data and then execute it as shown next:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample6.cs)]

    <span data-ttu-id="d8ac2-276">針對要插入的值，您會包含參數預留位置（`@0`、`@1`、`@2`）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-276">For the values to insert, you include parameter placeholders (`@0`, `@1`, `@2`).</span></span>

    > [!NOTE]
    > <span data-ttu-id="d8ac2-277">為了安全起見，請一律使用參數將值傳遞至 SQL 語句，如先前範例所示。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-277">As a security precaution, always pass values to a SQL statement using parameters, as you see in the preceding example.</span></span> <span data-ttu-id="d8ac2-278">這讓您有機會驗證使用者的資料，並協助防止嘗試將惡意命令傳送至您的資料庫（有時也稱為 SQL 插入式攻擊）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-278">This gives you a chance to validate the user's data, plus it helps protect against attempts to send malicious commands to your database (sometimes referred to as SQL injection attacks).</span></span>

    <span data-ttu-id="d8ac2-279">若要執行查詢，您可以使用此語句，並將包含值的變數傳遞給它，以替代預留位置：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-279">To execute the query, you use this statement, passing to it the variables that contain the values to substitute for the placeholders:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample7.cs)]

    <span data-ttu-id="d8ac2-280">執行 `Insert Into` 語句之後，您可以使用這一行將使用者傳送至列出產品的頁面：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-280">After the `Insert Into` statement has executed, you send the user to the page that lists the products using this line:</span></span>

    [!code-javascript[Main](5-working-with-data/samples/sample8.js)]

    <span data-ttu-id="d8ac2-281">如果驗證失敗，您會略過插入。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-281">If validation didn't succeed, you skip the insert.</span></span> <span data-ttu-id="d8ac2-282">相反地，您在頁面中有一個協助程式可以顯示累積的錯誤訊息（如果有的話）：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-282">Instead, you have a helper in the page that can display the accumulated error messages (if any):</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample9.cshtml)]

    <span data-ttu-id="d8ac2-283">請注意，標記中的樣式區塊包含名為 `.validation-summary-errors`的 CSS 類別定義。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-283">Notice that the style block in the markup includes a CSS class definition named `.validation-summary-errors`.</span></span> <span data-ttu-id="d8ac2-284">這是預設用於包含任何驗證錯誤之 `<div>` 元素的 CSS 類別名稱。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-284">This is the name of the CSS class that's used by default for the `<div>` element that contains any validation errors.</span></span> <span data-ttu-id="d8ac2-285">在此情況下，CSS 類別指定驗證摘要錯誤會以紅色和粗體顯示，但您可以定義 `.validation-summary-errors` 類別，以顯示您喜歡的任何格式。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-285">In this case, the CSS class specifies that validation summary errors are displayed in red and in bold, but you can define the `.validation-summary-errors` class to display any formatting you like.</span></span>

### <a name="testing-the-insert-page"></a><span data-ttu-id="d8ac2-286">測試插入頁面</span><span class="sxs-lookup"><span data-stu-id="d8ac2-286">Testing the Insert Page</span></span>

1. <span data-ttu-id="d8ac2-287">在瀏覽器中查看頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-287">View the page in a browser.</span></span> <span data-ttu-id="d8ac2-288">頁面會顯示類似下圖所示的表單。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-288">The page displays a form that's similar to the one that's shown in the following illustration.</span></span>

    ![[影像]](5-working-with-data/_static/image5.jpg)
2. <span data-ttu-id="d8ac2-290">輸入所有資料行的值，但請確定您將 [*價格*] 欄位保留空白。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-290">Enter values for all the columns, but make sure that you leave the *Price* column blank.</span></span>
3. <span data-ttu-id="d8ac2-291">按一下 [插入]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-291">Click **Insert**.</span></span> <span data-ttu-id="d8ac2-292">此頁面會顯示錯誤訊息，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-292">The page displays an error message, as shown in the following illustration.</span></span> <span data-ttu-id="d8ac2-293">（不會建立新的記錄）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-293">(No new record is created.)</span></span>

    ![[影像]](5-working-with-data/_static/image6.jpg)
4. <span data-ttu-id="d8ac2-295">完整填寫表單，然後按一下 [**插入**]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-295">Fill the form out completely, and then click **Insert**.</span></span> <span data-ttu-id="d8ac2-296">此時會顯示 [ *ListProducts* ] 頁面，並顯示新的記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-296">This time, the *ListProducts.cshtml* page is displayed and shows the new record.</span></span>

## <a name="updating-data-in-a-database"></a><span data-ttu-id="d8ac2-297">更新資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="d8ac2-297">Updating Data in a Database</span></span>

<span data-ttu-id="d8ac2-298">在資料表中輸入資料之後，您可能需要加以更新。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-298">After data has been entered into a table, you might need to update it.</span></span> <span data-ttu-id="d8ac2-299">此程式示範如何建立兩個頁面，與您先前為數據插入所建立的分頁類似。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-299">This procedure shows you how to create two pages that are similar to the ones you created for data insertion earlier.</span></span> <span data-ttu-id="d8ac2-300">第一頁會顯示產品，並讓使用者選取其中一項來變更。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-300">The first page displays products and lets users select one to change.</span></span> <span data-ttu-id="d8ac2-301">第二頁可讓使用者實際進行編輯並加以儲存。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-301">The second page lets the users actually make the edits and save them.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d8ac2-302">**重要事項**在生產網站中，您通常會限制可對資料進行變更的人員。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-302">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="d8ac2-303">如需如何設定成員資格，以及如何授權使用者在網站上執行工作的相關資訊，請參閱[新增 ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-303">For information about how to set up membership and about ways to authorize users to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="d8ac2-304">在網站中，建立名為*EditProducts*的新 CSHTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-304">In the website, create a new CSHTML file named *EditProducts.cshtml*.</span></span>
2. <span data-ttu-id="d8ac2-305">將檔案中的現有標記取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-305">Replace the existing markup in the file with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample10.cshtml)]

    <span data-ttu-id="d8ac2-306">此頁面與先前的*ListProducts*頁面之間唯一的差異在於，此頁面中的 HTML 資料表包含一個額外的資料行，可顯示 [**編輯**] 連結。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-306">The only difference between this page and the *ListProducts.cshtml* page from earlier is that the HTML table in this page includes an extra column that displays an **Edit** link.</span></span> <span data-ttu-id="d8ac2-307">當您按一下此連結時，它會帶您前往 [ *UpdateProducts* ] 頁面（您將在下一步建立），您可以在其中編輯選取的記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-307">When you click this link, it takes you to the *UpdateProducts.cshtml* page (which you'll create next) where you can edit the selected record.</span></span>

    <span data-ttu-id="d8ac2-308">查看建立 [**編輯**] 連結的程式碼：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-308">Look at the code that creates the **Edit** link:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample11.cshtml)]

    <span data-ttu-id="d8ac2-309">這會建立一個 HTML `<a>` 專案，其 `href` 屬性是以動態方式設定。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-309">This creates an HTML `<a>` element whose `href` attribute is set dynamically.</span></span> <span data-ttu-id="d8ac2-310">`href` 屬性指定使用者按一下連結時要顯示的頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-310">The `href` attribute specifies the page to display when the user clicks the link.</span></span> <span data-ttu-id="d8ac2-311">它也會將目前資料列的 `Id` 值傳遞至連結。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-311">It also passes the `Id` value of the current row to the link.</span></span> <span data-ttu-id="d8ac2-312">當頁面執行時，頁面來源可能會包含如下的連結：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-312">When the page runs, the page source might contain links like these:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample12.html)]

    <span data-ttu-id="d8ac2-313">請注意，`href` 屬性會設定為 `UpdateProducts/n`，其中*n*是產品編號。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-313">Notice that the `href` attribute is set to `UpdateProducts/n`, where *n* is a product number.</span></span> <span data-ttu-id="d8ac2-314">當使用者按一下其中一個連結時，產生的 URL 看起來會像這樣：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-314">When a user clicks one of these links, the resulting URL will look something like this:</span></span>

    `http://localhost:18816/UpdateProducts/6`

    <span data-ttu-id="d8ac2-315">換句話說，要編輯的產品編號會在 URL 中傳遞。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-315">In other words, the product number to be edited will be passed in the URL.</span></span>
3. <span data-ttu-id="d8ac2-316">在瀏覽器中查看頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-316">View the page in a browser.</span></span> <span data-ttu-id="d8ac2-317">頁面會顯示如下格式的資料：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-317">The page displays the data in a format like this:</span></span>

    ![[影像]](5-working-with-data/_static/image7.jpg)

    <span data-ttu-id="d8ac2-319">接下來，您將建立可讓使用者實際更新資料的頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-319">Next, you'll create the page that lets users actually update the data.</span></span> <span data-ttu-id="d8ac2-320">[更新] 頁面包含驗證，以驗證使用者輸入的資料。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-320">The update page includes validation to validate the data that the user enters.</span></span> <span data-ttu-id="d8ac2-321">例如，頁面中的程式碼會確定已針對所有必要的資料行輸入值。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-321">For example, code in the page makes sure that a value has been entered for all required columns.</span></span>
4. <span data-ttu-id="d8ac2-322">在網站中，建立名為*UpdateProducts*的新 CSHTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-322">In the website, create a new CSHTML file named *UpdateProducts.cshtml*.</span></span>
5. <span data-ttu-id="d8ac2-323">將檔案中的現有標記取代為下列檔案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-323">Replace the existing markup in the file with the following.</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample13.cshtml)]

    <span data-ttu-id="d8ac2-324">頁面的本文包含一個 HTML 表單，其中會顯示產品以及使用者可以編輯的位置。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-324">The body of the page contains an HTML form where a product is displayed and where users can edit it.</span></span> <span data-ttu-id="d8ac2-325">若要讓產品顯示，請使用下列 SQL 語句：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-325">To get the product to display, you use this SQL statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample14.sql)]

    <span data-ttu-id="d8ac2-326">這會選取識別碼符合在 `@0` 參數中傳遞之值的產品。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-326">This will select the product whose ID matches the value that's passed in the `@0` parameter.</span></span> <span data-ttu-id="d8ac2-327">（因為*Id*是主要金鑰，因此必須是唯一的，因此只能以這種方式選取一筆產品記錄）。若要取得要傳遞給這個 `Select` 語句的識別碼值，您可以使用下列語法來讀取傳遞至頁面的值做為 URL 的一部分：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-327">(Because *Id* is the primary key and therefore must be unique, only one product record can ever be selected this way.) To get the ID value to pass to this `Select` statement, you can read the value that's passed to the page as part of the URL, using the following syntax:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample15.cs)]

    <span data-ttu-id="d8ac2-328">若要實際提取產品記錄，您可以使用 `QuerySingle` 方法，這只會傳回一筆記錄：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-328">To actually fetch the product record, you use the `QuerySingle` method, which will return just one record:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample16.cs)]

    <span data-ttu-id="d8ac2-329">單一資料列會傳回 `row` 變數中。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-329">The single row is returned into the `row` variable.</span></span> <span data-ttu-id="d8ac2-330">您可以從每個資料行取得資料，並將它指派給本機變數，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-330">You can get data out of each column and assign it to local variables like this:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample17.cs)]

    <span data-ttu-id="d8ac2-331">在表單的標記中，這些值會在個別的文字方塊中使用內嵌程式碼自動顯示，如下所示：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-331">In the markup for the form, these values are displayed automatically in individual text boxes by using embedded code like the following:</span></span>

    [!code-html[Main](5-working-with-data/samples/sample18.html)]

    <span data-ttu-id="d8ac2-332">該部分的程式碼會顯示要更新的產品記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-332">That part of the code displays the product record to be updated.</span></span> <span data-ttu-id="d8ac2-333">一旦顯示記錄，使用者就可以編輯個別的資料行。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-333">Once the record has been displayed, the user can edit individual columns.</span></span>

    <span data-ttu-id="d8ac2-334">當使用者按一下 [**更新**] 按鈕來提交表單時，`if(IsPost)` 區塊中的程式碼就會執行。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-334">When the user submits the form by clicking the **Update** button, the code in the `if(IsPost)` block runs.</span></span> <span data-ttu-id="d8ac2-335">這會從 `Request` 物件取得使用者的值、將值儲存在變數中，以及驗證每個資料行都已填入。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-335">This gets the user's values from the `Request` object, stores the values in variables, and validates that each column has been filled in.</span></span> <span data-ttu-id="d8ac2-336">如果通過驗證，程式碼會建立下列 SQL Update 語句：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-336">If validation passes, the code creates the following SQL Update statement:</span></span>

    [!code-sql[Main](5-working-with-data/samples/sample19.sql)]

    <span data-ttu-id="d8ac2-337">在 SQL `Update` 語句中，您可以指定要更新的每個資料行，以及要將其設定為的值。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-337">In a SQL `Update` statement, you specify each column to update and the value to set it to.</span></span> <span data-ttu-id="d8ac2-338">在此程式碼中，會使用參數預留位置來指定值 `@0`、`@1`、`@2`等等。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-338">In this code, the values are specified using the parameter placeholders `@0`, `@1`, `@2`, and so on.</span></span> <span data-ttu-id="d8ac2-339">（如先前所述，為了安全性，您應該一律使用參數將值傳遞至 SQL 語句）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-339">(As noted earlier, for security, you should always pass values to a SQL statement by using parameters.)</span></span>

    <span data-ttu-id="d8ac2-340">當您呼叫 `db.Execute` 方法時，您會以對應至 SQL 語句中參數的順序，傳遞包含值的變數：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-340">When you call the `db.Execute` method, you pass the variables that contain the values in the order that corresponds to the parameters in the SQL statement:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample20.cs)]

    <span data-ttu-id="d8ac2-341">執行 `Update` 語句之後，您可以呼叫下列方法，以將使用者重新導向回 [編輯] 頁面：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-341">After the `Update` statement has been executed, you call the following method in order to redirect the user back to the edit page:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample21.cshtml)]

    <span data-ttu-id="d8ac2-342">其效果是使用者會看到資料庫中資料的更新清單，而且可以編輯另一個產品。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-342">The effect is that the user sees an updated listing of the data in the database and can edit another product.</span></span>
6. <span data-ttu-id="d8ac2-343">儲存網頁。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-343">Save the page.</span></span>
7. <span data-ttu-id="d8ac2-344">執行 [ *EditProducts* ] 頁面（不是 [更新] 頁面），然後按一下 [**編輯**] 以選取要編輯的產品。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-344">Run the *EditProducts.cshtml* page (not the update page) and then click **Edit** to select a product to edit.</span></span> <span data-ttu-id="d8ac2-345">[ *UpdateProducts* ] 頁面隨即顯示，並顯示您所選取的記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-345">The *UpdateProducts.cshtml* page is displayed, showing the record you selected.</span></span>

    ![[影像]](5-working-with-data/_static/image8.jpg)
8. <span data-ttu-id="d8ac2-347">進行變更，然後按一下 [**更新**]。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-347">Make a change and click **Update**.</span></span> <span data-ttu-id="d8ac2-348">[產品] 清單會與更新的資料再次顯示。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-348">The products list is shown again with your updated data.</span></span>

## <a name="deleting-data-in-a-database"></a><span data-ttu-id="d8ac2-349">刪除資料庫中的資料</span><span class="sxs-lookup"><span data-stu-id="d8ac2-349">Deleting Data in a Database</span></span>

<span data-ttu-id="d8ac2-350">本節說明如何讓使用者從*product*資料庫資料表中刪除產品。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-350">This section shows how to let users delete a product from the *Product* database table.</span></span> <span data-ttu-id="d8ac2-351">此範例包含兩個頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-351">The example consists of two pages.</span></span> <span data-ttu-id="d8ac2-352">在第一頁中，使用者選取要刪除的記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-352">In the first page, users select a record to delete.</span></span> <span data-ttu-id="d8ac2-353">接著會在第二頁顯示要刪除的記錄，讓他們確認是否要刪除記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-353">The record to be deleted is then displayed in a second page that lets them confirm that they want to delete the record.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="d8ac2-354">**重要事項**在生產網站中，您通常會限制可對資料進行變更的人員。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-354">**Important** In a production website, you typically restrict who's allowed to make changes to the data.</span></span> <span data-ttu-id="d8ac2-355">如需如何設定成員資格，以及如何授權使用者在網站上執行工作的相關資訊，請參閱[新增 ASP.NET Web Pages 網站的安全性和成員資格](https://go.microsoft.com/fwlink/?LinkId=202904)。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-355">For information about how to set up membership and about ways to authorize user to perform tasks on the site, see [Adding Security and Membership to an ASP.NET Web Pages Site](https://go.microsoft.com/fwlink/?LinkId=202904).</span></span>

1. <span data-ttu-id="d8ac2-356">在網站中，建立名為*ListProductsForDelete*的新 CSHTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-356">In the website, create a new CSHTML file named *ListProductsForDelete.cshtml*.</span></span>
2. <span data-ttu-id="d8ac2-357">以下列內容取代現有的標記：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-357">Replace the existing markup with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample22.cshtml)]

    <span data-ttu-id="d8ac2-358">此頁面與稍早的*EditProducts*頁面類似。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-358">This page is similar to the *EditProducts.cshtml* page from earlier.</span></span> <span data-ttu-id="d8ac2-359">不過，它不會顯示每個產品的 [**編輯**] 連結，而是顯示 [**刪除**] 連結。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-359">However, instead of displaying an **Edit** link for each product, it displays a **Delete** link.</span></span> <span data-ttu-id="d8ac2-360">[**刪除**] 連結是在標記中使用下列內嵌程式碼所建立：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-360">The **Delete** link is created using the following embedded code in the markup:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample23.cshtml)]

    <span data-ttu-id="d8ac2-361">這會在使用者按一下連結時，建立如下所示的 URL：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-361">This creates a URL that looks like this when users click the link:</span></span>

    `http://<server>/DeleteProduct/4`

    <span data-ttu-id="d8ac2-362">URL 會呼叫名為*DeleteProduct*的頁面（您將在下一步建立），並將它的識別碼傳遞給它，以供刪除（此處為4）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-362">The URL calls a page named *DeleteProduct.cshtml* (which you'll create next) and passes it the ID of the product to delete (here, 4).</span></span>
3. <span data-ttu-id="d8ac2-363">儲存檔案，但讓它保持開啟。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-363">Save the file, but leave it open.</span></span>
4. <span data-ttu-id="d8ac2-364">建立另一個名為*DeleteProduct*的 CHTML 檔案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-364">Create another CHTML file named *DeleteProduct.cshtml*.</span></span> <span data-ttu-id="d8ac2-365">以下列內容取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-365">Replace the existing content with the following:</span></span>

    [!code-cshtml[Main](5-working-with-data/samples/sample24.cshtml)]

    <span data-ttu-id="d8ac2-366">此頁面是由*ListProductsForDelete*所呼叫，可讓使用者確認他們想要刪除產品。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-366">This page is called by *ListProductsForDelete.cshtml* and lets users confirm that they want to delete a product.</span></span> <span data-ttu-id="d8ac2-367">若要列出要刪除的產品，您可以使用下列程式碼，取得要從 URL 刪除的產品識別碼：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-367">To list the product to be deleted, you get the ID of the product to delete from the URL using the following code:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample25.cs)]

    <span data-ttu-id="d8ac2-368">該頁面接著會要求使用者按一下按鈕，以實際刪除該記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-368">The page then asks the user to click a button to actually delete the record.</span></span> <span data-ttu-id="d8ac2-369">這是一項重要的安全性措施：當您在網站中執行敏感性作業（例如更新或刪除資料）時，應該一律使用 POST 作業來完成這些作業，而不是取得操作。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-369">This is an important security measure: when you perform sensitive operations in your website like updating or deleting data, these operations should always be done using a POST operation, not a GET operation.</span></span> <span data-ttu-id="d8ac2-370">如果您的網站已設定為可使用「取得」作業來執行「刪除」作業，任何人都可以傳遞類似 `http://<server>/DeleteProduct/4` 的 URL，並從您的資料庫中刪除他們想要的任何專案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-370">If your site is set up so that a delete operation can be performed using a GET operation, anyone can pass a URL like `http://<server>/DeleteProduct/4` and delete anything they want from your database.</span></span> <span data-ttu-id="d8ac2-371">藉由新增確認並撰寫頁面的程式碼，以便只能使用文章來執行刪除作業，您可以將安全性量值新增至您的網站。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-371">By adding the confirmation and coding the page so that the deletion can be performed only by using a POST, you add a measure of security to your site.</span></span>

    <span data-ttu-id="d8ac2-372">實際的刪除作業會使用下列程式碼來執行，這會先確認這是 post 作業，而且識別碼不是空的：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-372">The actual delete operation is performed using the following code, which first confirms that this is a post operation and that the ID isn't empty:</span></span>

    [!code-csharp[Main](5-working-with-data/samples/sample26.cs)]

    <span data-ttu-id="d8ac2-373">程式碼會執行 SQL 語句，以刪除指定的記錄，然後將使用者重新導向回清單頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-373">The code runs a SQL statement that deletes the specified record and then redirects the user back to the listing page.</span></span>
5. <span data-ttu-id="d8ac2-374">在瀏覽器中執行*ListProductsForDelete。*</span><span class="sxs-lookup"><span data-stu-id="d8ac2-374">Run *ListProductsForDelete.cshtml* in a browser.</span></span>

    ![[影像]](5-working-with-data/_static/image9.jpg)
6. <span data-ttu-id="d8ac2-376">按一下其中一項產品的 [**刪除**] 連結。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-376">Click the **Delete** link for one of the products.</span></span> <span data-ttu-id="d8ac2-377">[ *DeleteProduct* ] 頁面隨即顯示，以確認您想要刪除該記錄。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-377">The *DeleteProduct.cshtml* page is displayed to confirm that you want to delete that record.</span></span>
7. <span data-ttu-id="d8ac2-378">按一下 [刪除] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-378">Click the **Delete** button.</span></span> <span data-ttu-id="d8ac2-379">會刪除產品記錄，並使用更新的產品清單來重新整理此頁面。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-379">The product record is deleted and the page is refreshed with an updated product listing.</span></span>

> [!TIP]
> 
> <a id="SB_ConnectingToADatabase"></a>
> ### <a name="connecting-to-a-database"></a><span data-ttu-id="d8ac2-380">連接到資料庫</span><span class="sxs-lookup"><span data-stu-id="d8ac2-380">Connecting to a Database</span></span>
> 
> <span data-ttu-id="d8ac2-381">您可以透過兩種方式連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-381">You can connect to a database in two ways.</span></span> <span data-ttu-id="d8ac2-382">第一種是使用 `Database.Open` 方法，並指定資料庫檔案的名稱（較不是 *.sdf*副檔名）：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-382">The first is to use the `Database.Open` method and to specify the name of the database file (less the *.sdf* extension):</span></span>
> 
> `var db = Database.Open("SmallBakery");`
> 
> <span data-ttu-id="d8ac2-383">`Open` 方法會假設。 *.sdf*檔案位於網站的*應用程式\_Data*資料夾中。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-383">The `Open` method assumes that the .*sdf* file is in the website's *App\_Data* folder.</span></span> <span data-ttu-id="d8ac2-384">此資料夾是特別為保存資料所設計。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-384">This folder is designed specifically for holding data.</span></span> <span data-ttu-id="d8ac2-385">例如，它具有適當的許可權可允許網站讀取及寫入資料，而作為安全性措施，WebMatrix 不允許從這個資料夾存取檔案。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-385">For example, it has appropriate permissions to allow the website to read and write data, and as a security measure, WebMatrix does not allow access to files from this folder.</span></span>
> 
> <span data-ttu-id="d8ac2-386">第二種方式是使用連接字串。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-386">The second way is to use a connection string.</span></span> <span data-ttu-id="d8ac2-387">連線字串包含如何連線到資料庫的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-387">A connection string contains information about how to connect to a database.</span></span> <span data-ttu-id="d8ac2-388">這可以包含檔案路徑，也可以包含本機或遠端伺服器上 SQL Server 資料庫的名稱，以及用來連接到該伺服器的使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-388">This can include a file path, or it can include the name of a SQL Server database on a local or remote server, along with a user name and password to connect to that server.</span></span> <span data-ttu-id="d8ac2-389">（如果您將資料保留在集中管理的 SQL Server 版本中，例如在主控提供者的網站上，則一律使用連接字串來指定資料庫連接資訊）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-389">(If you keep data in a centrally managed version of SQL Server, such as on a hosting provider's site, you always use a connection string to specify the database connection information.)</span></span>
> 
> <span data-ttu-id="d8ac2-390">在 WebMatrix 中，連接字串通常會儲存在名為*web.config*的 XML 檔案中。正如其名，您可以在網站的根目錄中*使用 web.config 檔案*來儲存網站的設定資訊，包括您的網站可能需要的任何連接字串。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-390">In WebMatrix, connection strings are usually stored in an XML file named *Web.config*. As the name implies, you can use a *Web.config* file in the root of your website to store the site's configuration information, including any connection strings that your site might require.</span></span> <span data-ttu-id="d8ac2-391">*Web.config 檔案*中的連接字串範例可能如下所示：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-391">An example of a connection string in a *Web.config* file might look like the following:</span></span>
> 
> [!code-xml[Main](5-working-with-data/samples/sample27.xml)]
> 
> <span data-ttu-id="d8ac2-392">在此範例中，連接字串會指向在伺服器上執行的 SQL Server 實例中的資料庫（相對於本機 *.sdf*檔案）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-392">In the example, the connection string points to a database in an instance of SQL Server that's running on a server somewhere (as opposed to a local *.sdf* file).</span></span> <span data-ttu-id="d8ac2-393">您必須以適當的名稱取代 `myServer` 和 `myDatabase`，並指定 `username` 和 `password`的 SQL Server 登入值。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-393">You would need to substitute the appropriate names for `myServer` and `myDatabase`, and specify SQL Server login values for `username` and `password`.</span></span> <span data-ttu-id="d8ac2-394">（使用者名稱和密碼值不一定與您的 Windows 認證相同，或者是您的主機服務提供者提供給您登入其伺服器的值。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-394">(The username and password values are not necessarily the same as your Windows credentials or as the values that your hosting provider has given you for logging in to their servers.</span></span> <span data-ttu-id="d8ac2-395">請洽詢系統管理員以取得您所需的確切值）。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-395">Check with the administrator for the exact values you need.)</span></span>
> 
> <span data-ttu-id="d8ac2-396">`Database.Open` 方法很有彈性，因為它可讓您傳遞資料庫 *.sdf*檔案的名稱或儲存在*web.config*檔案中的連接字串名稱。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-396">The `Database.Open` method is flexible, because it lets you pass either the name of a database *.sdf* file or the name of a connection string that's stored in the *Web.config* file.</span></span> <span data-ttu-id="d8ac2-397">下列範例顯示如何使用上述範例中所述的連接字串來連接到資料庫：</span><span class="sxs-lookup"><span data-stu-id="d8ac2-397">The following example shows how to connect to the database using the connection string illustrated in the previous example:</span></span>
> 
> [!code-cshtml[Main](5-working-with-data/samples/sample28.cshtml)]
> 
> <span data-ttu-id="d8ac2-398">如前所述，`Database.Open` 方法可讓您傳遞資料庫名稱或連接字串，並找出要使用的資料。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-398">As noted, the `Database.Open` method lets you pass either a database name or a connection string, and it'll figure out which to use.</span></span> <span data-ttu-id="d8ac2-399">當您部署（發佈）您的網站時，這非常有用。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-399">This is very useful when you deploy (publish) your website.</span></span> <span data-ttu-id="d8ac2-400">當您在開發和測試網站時，您可以在應用程式中使用 *.sdf*檔案 *\_Data*資料夾。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-400">You can use an *.sdf* file in the *App\_Data* folder when you're developing and testing your site.</span></span> <span data-ttu-id="d8ac2-401">然後，當您將網站移至實際執行伺服器時，您可以*在 web.config 檔案*中使用與 *.sdf*檔案同名的連接字串，但這會指向主控提供者的資料庫&#8212; ，而不需要變更您的程式碼。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-401">Then when you move your site to a production server, you can use a connection string in the *Web.config* file that has the same name as your *.sdf* file but that points to the hosting provider's database &#8212; all without having to change your code.</span></span>
> 
> <span data-ttu-id="d8ac2-402">最後，如果您想要直接使用連接字串，您可以呼叫 `Database.OpenConnectionString` 方法，並將實際*的*連接字串傳遞給它，而不只是 web.config 檔案中的名稱。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-402">Finally, if you want to work directly with a connection string, you can call the `Database.OpenConnectionString` method and pass it the actual connection string instead of just the name of one in the *Web.config* file.</span></span> <span data-ttu-id="d8ac2-403">這在某些情況下很有用，因為您無法存取連接字串（或其中的值，例如 *.sdf*檔案名），直到頁面執行為止。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-403">This might be useful in situations where for some reason you don't have access to the connection string (or values in it, such as the *.sdf* file name) until the page is running.</span></span> <span data-ttu-id="d8ac2-404">不過，在大部分的情況下，您可以使用本文中所述的 `Database.Open`。</span><span class="sxs-lookup"><span data-stu-id="d8ac2-404">However, for most scenarios, you can use `Database.Open` as described in this article.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="d8ac2-405">其他資源</span><span class="sxs-lookup"><span data-stu-id="d8ac2-405">Additional Resources</span></span>

- [<span data-ttu-id="d8ac2-406">SQL Server Compact</span><span class="sxs-lookup"><span data-stu-id="d8ac2-406">SQL Server Compact</span></span>](https://www.microsoft.com/sqlserver/2008/en/us/compact.aspx)
- [<span data-ttu-id="d8ac2-407">連接到 WebMatrix 中的 SQL Server 或 MySQL 資料庫</span><span class="sxs-lookup"><span data-stu-id="d8ac2-407">Connecting to a SQL Server or MySQL Database in WebMatrix</span></span>](https://go.microsoft.com/fwlink/?LinkId=208661)
- [<span data-ttu-id="d8ac2-408">在 ASP.NET Web Pages 網站中驗證使用者輸入</span><span class="sxs-lookup"><span data-stu-id="d8ac2-408">Validating User Input in ASP.NET Web Pages Sites</span></span>](https://go.microsoft.com/fwlink/?LinkId=253002)
