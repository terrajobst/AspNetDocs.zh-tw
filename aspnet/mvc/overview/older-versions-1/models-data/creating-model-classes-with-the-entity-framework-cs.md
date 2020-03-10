---
uid: mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
title: 使用 Entity Framework （C#）建立模型類別 |Microsoft Docs
author: microsoft
description: 在本教學課程中，您將瞭解如何搭配 Microsoft Entity Framework 使用 ASP.NET MVC。 您會瞭解如何使用 Entity Wizard 來建立 ADO.NET Entity Da 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: 61644169-e8b1-45dd-bf96-9c2301b69879
msc.legacyurl: /mvc/overview/older-versions-1/models-data/creating-model-classes-with-the-entity-framework-cs
msc.type: authoredcontent
ms.openlocfilehash: 2e0e365c287fc455015d237ea466301335805d14
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78581162"
---
# <a name="creating-model-classes-with-the-entity-framework-c"></a><span data-ttu-id="b903c-104">使用 Entity Framework 建立模型類別 (C#)</span><span class="sxs-lookup"><span data-stu-id="b903c-104">Creating Model Classes with the Entity Framework (C#)</span></span>

<span data-ttu-id="b903c-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="b903c-105">by [Microsoft](https://github.com/microsoft)</span></span>

> <span data-ttu-id="b903c-106">在本教學課程中，您將瞭解如何搭配 Microsoft Entity Framework 使用 ASP.NET MVC。</span><span class="sxs-lookup"><span data-stu-id="b903c-106">In this tutorial, you learn how to use ASP.NET MVC with the Microsoft Entity Framework.</span></span> <span data-ttu-id="b903c-107">您將瞭解如何使用 Entity Wizard 來建立 ADO.NET 實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="b903c-107">You learn how to use the Entity Wizard to create an ADO.NET Entity Data Model.</span></span> <span data-ttu-id="b903c-108">在本教學課程中，我們會建立一個 web 應用程式，說明如何使用 Entity Framework 來選取、插入、更新和刪除資料庫資料。</span><span class="sxs-lookup"><span data-stu-id="b903c-108">Over the course of this tutorial, we build a web application that illustrates how to select, insert, update, and delete database data by using the Entity Framework.</span></span>

<span data-ttu-id="b903c-109">本教學課程的目的是要說明如何在建立 ASP.NET MVC 應用程式時，使用 Microsoft Entity Framework 來建立資料存取類別。</span><span class="sxs-lookup"><span data-stu-id="b903c-109">The goal of this tutorial is to explain how you can create data access classes using the Microsoft Entity Framework when building an ASP.NET MVC application.</span></span> <span data-ttu-id="b903c-110">本教學課程假設您先前不知道 Microsoft Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="b903c-110">This tutorial assumes no previous knowledge of the Microsoft Entity Framework.</span></span> <span data-ttu-id="b903c-111">在本教學課程結束時，您將瞭解如何使用 Entity Framework 來選取、插入、更新和刪除資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-111">By the end of this tutorial, you'll understand how to use the Entity Framework to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="b903c-112">Microsoft Entity Framework 是物件關聯式對應（O/RM）工具，可讓您自動從資料庫產生資料存取層。</span><span class="sxs-lookup"><span data-stu-id="b903c-112">The Microsoft Entity Framework is an Object Relational Mapping (O/RM) tool that enables you to generate a data access layer from a database automatically.</span></span> <span data-ttu-id="b903c-113">此 Entity Framework 可讓您以手動方式建立資料存取類別，以避免乏味的工作。</span><span class="sxs-lookup"><span data-stu-id="b903c-113">The Entity Framework enables you to avoid the tedious work of building your data access classes by hand.</span></span>

<span data-ttu-id="b903c-114">為了說明如何搭配使用 Microsoft Entity Framework 與 ASP.NET MVC，我們將建立一個簡單的範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="b903c-114">In order to illustrate how you can use the Microsoft Entity Framework with ASP.NET MVC, we'll build a simple sample application.</span></span> <span data-ttu-id="b903c-115">我們將建立電影資料庫應用程式，讓您可以顯示和編輯電影資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-115">We'll create a Movie Database application that enables you to display and edit movie database records.</span></span>

<span data-ttu-id="b903c-116">本教學課程假設您有 Visual Studio 2008 或 Visual Web Developer 2008 （含 Service Pack 1）。</span><span class="sxs-lookup"><span data-stu-id="b903c-116">This tutorial assumes that you have Visual Studio 2008 or Visual Web Developer 2008 with Service Pack 1.</span></span> <span data-ttu-id="b903c-117">您需要 Service Pack 1，才能使用 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="b903c-117">You need Service Pack 1 in order to use the Entity Framework.</span></span> <span data-ttu-id="b903c-118">您可以從下列位址下載 Visual Studio 2008 Service Pack 1 或 Visual Web Developer （含 Service Pack 1）：</span><span class="sxs-lookup"><span data-stu-id="b903c-118">You can download Visual Studio 2008 Service Pack 1 or Visual Web Developer with Service Pack 1 from the following address:</span></span>

> [https://www.asp.net/downloads/](https://www.asp.net/downloads)

> [!NOTE] 
> 
> <span data-ttu-id="b903c-119">ASP.NET MVC 與 Microsoft Entity Framework 之間沒有任何必要的連接。</span><span class="sxs-lookup"><span data-stu-id="b903c-119">There is no essential connection between ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="b903c-120">您可以搭配 ASP.NET MVC 使用的 Entity Framework 有數個替代方案。</span><span class="sxs-lookup"><span data-stu-id="b903c-120">There are several alternatives to the Entity Framework that you can use with ASP.NET MVC.</span></span> <span data-ttu-id="b903c-121">例如，您可以使用其他 O/RM 工具（例如 Microsoft LINQ to SQL、NHibernate 或 SubSonic）來建立 MVC 模型類別。</span><span class="sxs-lookup"><span data-stu-id="b903c-121">For example, you can build your MVC Model classes using other O/RM tools such as Microsoft LINQ to SQL, NHibernate, or SubSonic.</span></span>

## <a name="creating-the-movie-sample-database"></a><span data-ttu-id="b903c-122">建立電影範例資料庫</span><span class="sxs-lookup"><span data-stu-id="b903c-122">Creating the Movie Sample Database</span></span>

<span data-ttu-id="b903c-123">電影資料庫應用程式會使用名為電影的資料庫資料表，其中包含下列資料行：</span><span class="sxs-lookup"><span data-stu-id="b903c-123">The Movie Database application uses a database table named Movies that contains the following columns:</span></span>

| <span data-ttu-id="b903c-124">資料行名稱</span><span class="sxs-lookup"><span data-stu-id="b903c-124">Column Name</span></span> | <span data-ttu-id="b903c-125">資料類型</span><span class="sxs-lookup"><span data-stu-id="b903c-125">Data Type</span></span> | <span data-ttu-id="b903c-126">允許 Null 嗎？</span><span class="sxs-lookup"><span data-stu-id="b903c-126">Allow Nulls?</span></span> | <span data-ttu-id="b903c-127">是否為主要金鑰？</span><span class="sxs-lookup"><span data-stu-id="b903c-127">Is Primary Key?</span></span> |
| --- | --- | --- | --- |
| <span data-ttu-id="b903c-128">ID</span><span class="sxs-lookup"><span data-stu-id="b903c-128">Id</span></span> | <span data-ttu-id="b903c-129">int</span><span class="sxs-lookup"><span data-stu-id="b903c-129">int</span></span> | <span data-ttu-id="b903c-130">False</span><span class="sxs-lookup"><span data-stu-id="b903c-130">False</span></span> | <span data-ttu-id="b903c-131">True</span><span class="sxs-lookup"><span data-stu-id="b903c-131">True</span></span> |
| <span data-ttu-id="b903c-132">標題</span><span class="sxs-lookup"><span data-stu-id="b903c-132">Title</span></span> | <span data-ttu-id="b903c-133">NVarchar （100）</span><span class="sxs-lookup"><span data-stu-id="b903c-133">nvarchar(100)</span></span> | <span data-ttu-id="b903c-134">False</span><span class="sxs-lookup"><span data-stu-id="b903c-134">False</span></span> | <span data-ttu-id="b903c-135">False</span><span class="sxs-lookup"><span data-stu-id="b903c-135">False</span></span> |
| <span data-ttu-id="b903c-136">導演</span><span class="sxs-lookup"><span data-stu-id="b903c-136">Director</span></span> | <span data-ttu-id="b903c-137">NVarchar （100）</span><span class="sxs-lookup"><span data-stu-id="b903c-137">nvarchar(100)</span></span> | <span data-ttu-id="b903c-138">False</span><span class="sxs-lookup"><span data-stu-id="b903c-138">False</span></span> | <span data-ttu-id="b903c-139">False</span><span class="sxs-lookup"><span data-stu-id="b903c-139">False</span></span> |

<span data-ttu-id="b903c-140">您可以遵循下列步驟，將此資料表新增至 ASP.NET MVC 專案：</span><span class="sxs-lookup"><span data-stu-id="b903c-140">You can add this table to an ASP.NET MVC project by following these steps:</span></span>

1. <span data-ttu-id="b903c-141">在 [方案總管] 視窗中，以滑鼠右鍵按一下應用程式\_[Data] 資料夾，然後選取 [**新增]、[新增專案**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="b903c-141">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item.**</span></span>
2. <span data-ttu-id="b903c-142">從 [**加入新專案**] 對話方塊中，選取 [ **SQL Server 資料庫**]，將資料庫命名為 MoviesDB，然後按一下 [**加入**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b903c-142">From the **Add New Item** dialog box, select **SQL Server Database**, give the database the name MoviesDB.mdf, and click the **Add** button.</span></span>
3. <span data-ttu-id="b903c-143">按兩下 [MoviesDB] 檔案以開啟 [伺服器總管/資料庫總管] 視窗。</span><span class="sxs-lookup"><span data-stu-id="b903c-143">Double-click the MoviesDB.mdf file to open the Server Explorer/Database Explorer window.</span></span>
4. <span data-ttu-id="b903c-144">展開 [MoviesDB] 資料庫連接，以滑鼠右鍵按一下 [資料表] 資料夾，然後選取 [**加入新的資料表**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="b903c-144">Expand the MoviesDB.mdf database connection, right-click the Tables folder, and select the menu option **Add New Table**.</span></span>
5. <span data-ttu-id="b903c-145">在 資料表設計工具中，新增 識別碼、標題 和 導演 資料行。</span><span class="sxs-lookup"><span data-stu-id="b903c-145">In the Table Designer, add the Id, Title, and Director columns.</span></span>
6. <span data-ttu-id="b903c-146">按一下 [**儲存**] 按鈕（其具有軟碟圖示）以儲存新的資料表，並將其名稱設為電影。</span><span class="sxs-lookup"><span data-stu-id="b903c-146">Click the **Save** button (it has the icon of the floppy) to save the new table with the name Movies.</span></span>

<span data-ttu-id="b903c-147">建立電影資料庫資料表之後，您應該在資料表中加入一些範例資料。</span><span class="sxs-lookup"><span data-stu-id="b903c-147">After you create the Movies database table, you should add some sample data to the table.</span></span> <span data-ttu-id="b903c-148">以滑鼠右鍵按一下 [電影] 資料表，然後選取 [**顯示資料表資料**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="b903c-148">Right-click the Movies table and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="b903c-149">您可以在出現的方格中輸入假電影資料。</span><span class="sxs-lookup"><span data-stu-id="b903c-149">You can enter fake movie data into the grid that appears.</span></span>

## <a name="creating-the-adonet-entity-data-model"></a><span data-ttu-id="b903c-150">建立 ADO.NET 實體資料模型</span><span class="sxs-lookup"><span data-stu-id="b903c-150">Creating the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="b903c-151">若要使用 Entity Framework，您需要建立實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="b903c-151">In order to use the Entity Framework, you need to create an Entity Data Model.</span></span> <span data-ttu-id="b903c-152">您可以利用 Visual Studio*實體資料模型 Wizard* ，自動從資料庫產生實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="b903c-152">You can take advantage of the Visual Studio *Entity Data Model Wizard* to generate an Entity Data Model from a database automatically.</span></span>

<span data-ttu-id="b903c-153">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="b903c-153">Follow these steps:</span></span>

1. <span data-ttu-id="b903c-154">以滑鼠右鍵按一下 [方案總管] 視窗中的 [模型] 資料夾，然後選取 [**加入]、[新增專案**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="b903c-154">Right-click the Models folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="b903c-155">在 [**加入新專案**] 對話方塊中，選取 [資料] 類別（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="b903c-155">In the **Add New Item** dialog, select the Data category (see Figure 1).</span></span>
3. <span data-ttu-id="b903c-156">選取 [ **ADO.NET 實體資料模型**] 範本，將實體資料模型名稱指定為 MoviesDBModel，然後按一下 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="b903c-156">Select the **ADO.NET Entity Data Model** template, give the Entity Data Model the name MoviesDBModel.edmx, and click the **Add** button.</span></span> <span data-ttu-id="b903c-157">按一下 [**新增**] 按鈕即可啟動 [資料模型嚮導]。</span><span class="sxs-lookup"><span data-stu-id="b903c-157">Clicking the **Add** button launches the Data Model Wizard.</span></span>
4. <span data-ttu-id="b903c-158">在 [**選擇模型內容**] 步驟中，選擇 [**從資料庫產生**] 選項，然後按 [**下一步]** 按鈕（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="b903c-158">In the **Choose Model Contents** step, choose the **Generate from a database** option and click the **Next** button (see Figure 2).</span></span>
5. <span data-ttu-id="b903c-159">在 [**選擇您的資料連線**] 步驟中，選取 [MoviesDB] 資料庫連接，並輸入實體連接設定名稱 MoviesDBEntities，然後按 [**下一步]** 按鈕（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="b903c-159">In the **Choose Your Data Connection** step, select the MoviesDB.mdf database connection, enter the entities connection settings name MoviesDBEntities, and click the **Next** button (see Figure 3).</span></span>
6. <span data-ttu-id="b903c-160">在 [**選擇您的資料庫物件**] 步驟中，選取 [電影資料庫] 資料表，然後按一下 [**完成]** 按鈕（請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="b903c-160">In the **Choose Your Database Objects** step, select the Movie database table and click the **Finish** button (see Figure 4).</span></span>

<span data-ttu-id="b903c-161">完成這些步驟之後，就會開啟 [ADO.NET 實體資料模型設計工具（Entity Designer）]。</span><span class="sxs-lookup"><span data-stu-id="b903c-161">After you complete these steps, the ADO.NET Entity Data Model Designer (Entity Designer) opens.</span></span>

<span data-ttu-id="b903c-162">**圖1–建立新的實體資料模型**</span><span class="sxs-lookup"><span data-stu-id="b903c-162">**Figure 1 – Creating a new Entity Data Model**</span></span>

![clip_image002](creating-model-classes-with-the-entity-framework-cs/_static/image1.jpg)

<span data-ttu-id="b903c-164">**圖2–選擇模型內容步驟**</span><span class="sxs-lookup"><span data-stu-id="b903c-164">**Figure 2 – Choose Model Contents Step**</span></span>

![clip_image004](creating-model-classes-with-the-entity-framework-cs/_static/image2.jpg)

<span data-ttu-id="b903c-166">**圖3–選擇您的資料連線**</span><span class="sxs-lookup"><span data-stu-id="b903c-166">**Figure 3 – Choose Your Data Connection**</span></span>

![clip_image006](creating-model-classes-with-the-entity-framework-cs/_static/image3.jpg)

<span data-ttu-id="b903c-168">**圖4–選擇您的資料庫物件**</span><span class="sxs-lookup"><span data-stu-id="b903c-168">**Figure 4 – Choose Your Database Objects**</span></span>

![clip_image008](creating-model-classes-with-the-entity-framework-cs/_static/image4.jpg)

#### <a name="modifying-the-adonet-entity-data-model"></a><span data-ttu-id="b903c-170">修改 ADO.NET 實體資料模型</span><span class="sxs-lookup"><span data-stu-id="b903c-170">Modifying the ADO.NET Entity Data Model</span></span>

<span data-ttu-id="b903c-171">建立實體資料模型之後，您可以利用 Entity Designer 來修改模型（請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="b903c-171">After you create an Entity Data Model, you can modify the model by taking advantage of the Entity Designer (see Figure 5).</span></span> <span data-ttu-id="b903c-172">您可以在 [方案總管] 視窗內的 [模型] 資料夾中，按兩下包含的 MoviesDBModel，隨時開啟 Entity Designer。</span><span class="sxs-lookup"><span data-stu-id="b903c-172">You can open the Entity Designer at any time by double-clicking the MoviesDBModel.edmx file contained in the Models folder within the Solution Explorer window.</span></span>

<span data-ttu-id="b903c-173">**[圖 5] – ADO.NET 實體資料模型設計工具**</span><span class="sxs-lookup"><span data-stu-id="b903c-173">**Figure 5 – The ADO.NET Entity Data Model Designer**</span></span>

![clip_image010](creating-model-classes-with-the-entity-framework-cs/_static/image5.jpg)

<span data-ttu-id="b903c-175">例如，您可以使用 Entity Designer 來變更「實體模型資料嚮導」所產生的類別名稱。</span><span class="sxs-lookup"><span data-stu-id="b903c-175">For example, you can use the Entity Designer to change the names of the classes that the Entity Model Data Wizard generates.</span></span> <span data-ttu-id="b903c-176">嚮導會建立名為 [電影] 的新資料存取類別。</span><span class="sxs-lookup"><span data-stu-id="b903c-176">The Wizard created a new data access class named Movies.</span></span> <span data-ttu-id="b903c-177">換句話說，此 Wizard 提供的類別與資料庫資料表的名稱相同。</span><span class="sxs-lookup"><span data-stu-id="b903c-177">In other words, the Wizard gave the class the very same name as the database table.</span></span> <span data-ttu-id="b903c-178">因為我們將使用此類別來代表特定電影實例，所以我們應該將類別從電影重新命名為 Movie。</span><span class="sxs-lookup"><span data-stu-id="b903c-178">Because we will use this class to represent a particular Movie instance, we should rename the class from Movies to Movie.</span></span>

<span data-ttu-id="b903c-179">如果您想要重新命名實體類別，可以按兩下 Entity Designer 中的類別名稱，然後輸入新的名稱（請參閱 [圖 6]）。</span><span class="sxs-lookup"><span data-stu-id="b903c-179">If you want to rename an entity class, you can double-click on the class name in the Entity Designer and enter a new name (see Figure 6).</span></span> <span data-ttu-id="b903c-180">或者，您可以在選取 Entity Designer 中的實體之後，變更屬性視窗中的機構名稱。</span><span class="sxs-lookup"><span data-stu-id="b903c-180">Alternatively, you can change the name of an entity in the Properties window after selecting an entity in the Entity Designer.</span></span>

<span data-ttu-id="b903c-181">**圖6–變更機構名稱**</span><span class="sxs-lookup"><span data-stu-id="b903c-181">**Figure 6 – Changing an entity name**</span></span>

![clip_image012](creating-model-classes-with-the-entity-framework-cs/_static/image6.jpg)

<span data-ttu-id="b903c-183">按一下 [儲存] 按鈕（磁片圖示）以進行修改之後，請記得儲存您的實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="b903c-183">Remember to save your Entity Data Model after making a modification by clicking the Save button (the icon of the floppy disk).</span></span> <span data-ttu-id="b903c-184">在幕後，Entity Designer 會產生一組C#類別。</span><span class="sxs-lookup"><span data-stu-id="b903c-184">Behind the scenes, the Entity Designer generates a set of C# classes.</span></span> <span data-ttu-id="b903c-185">您可以從 [方案總管] 視窗開啟 MoviesDBModel.Designer.cs 檔案，以查看這些類別。</span><span class="sxs-lookup"><span data-stu-id="b903c-185">You can view these classes by opening the MoviesDBModel.Designer.cs file from the Solution Explorer window.</span></span>

<span data-ttu-id="b903c-186">請勿修改 Designer.cs 檔案中的程式碼，因為下次使用 Entity Designer 時，將會覆寫變更。</span><span class="sxs-lookup"><span data-stu-id="b903c-186">Don't modify the code in the Designer.cs file since your changes will be overwritten the next time you use the Entity Designer.</span></span> <span data-ttu-id="b903c-187">如果您想要擴充 Designer.cs 檔案中定義之實體類別的功能，您可以在不同的檔案中建立*部分類別*。</span><span class="sxs-lookup"><span data-stu-id="b903c-187">If you want to extend the functionality of the entity classes defined in the Designer.cs file then you can create *partial classes* in separate files.</span></span>

#### <a name="selecting-database-records-with-the-entity-framework"></a><span data-ttu-id="b903c-188">使用 Entity Framework 選取資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="b903c-188">Selecting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b903c-189">讓我們開始建立電影資料庫應用程式，方法是建立顯示電影記錄清單的頁面。</span><span class="sxs-lookup"><span data-stu-id="b903c-189">Let's start building our Movie Database application by creating a page that displays a list of movie records.</span></span> <span data-ttu-id="b903c-190">[清單 1] 中的 Home 控制器會公開名為 Index （）的動作。</span><span class="sxs-lookup"><span data-stu-id="b903c-190">The Home controller in Listing 1 exposes an action named Index().</span></span> <span data-ttu-id="b903c-191">Index （）動作會利用 Entity Framework，從 Movie 資料庫資料表傳回所有電影記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-191">The Index() action returns all of the movie records from the Movie database table by taking advantage of the Entity Framework.</span></span>

<span data-ttu-id="b903c-192">**清單1– Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="b903c-192">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample1.cs)]

<span data-ttu-id="b903c-193">請注意，[清單 1] 中的控制器包含一個「函式」。</span><span class="sxs-lookup"><span data-stu-id="b903c-193">Notice that the controller in Listing 1 includes a constructor.</span></span> <span data-ttu-id="b903c-194">此函式會初始化名為 \_db 的類別層級欄位。</span><span class="sxs-lookup"><span data-stu-id="b903c-194">The constructor initializes a class-level field named \_db.</span></span> <span data-ttu-id="b903c-195">[\_db] 欄位代表 Microsoft Entity Framework 所產生的資料庫實體。</span><span class="sxs-lookup"><span data-stu-id="b903c-195">The \_db field represents the database entities generated by the Microsoft Entity Framework.</span></span> <span data-ttu-id="b903c-196">[\_db] 欄位是由 Entity Designer 產生之 MoviesDBEntities 類別的實例。</span><span class="sxs-lookup"><span data-stu-id="b903c-196">The \_db field is an instance of the MoviesDBEntities class that was generated by the Entity Designer.</span></span>

<span data-ttu-id="b903c-197">若要在 Home 控制器中使用 theMoviesDBEntities 類別，您必須匯入 MovieEntityApp 命名空間（*MVCProjectName*。模型）。</span><span class="sxs-lookup"><span data-stu-id="b903c-197">In order to use theMoviesDBEntities class in the Home controller, you must import the MovieEntityApp.Models namespace (*MVCProjectName*.Models).</span></span>

<span data-ttu-id="b903c-198">[\_db] 欄位會在 Index （）動作內使用，以從電影資料庫資料表中取出記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-198">The \_db field is used within the Index() action to retrieve the records from the Movies database table.</span></span> <span data-ttu-id="b903c-199">運算式 \_db。MovieSet 代表來自電影資料庫資料表的所有記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-199">The expression \_db.MovieSet represents all of the records from the Movies database table.</span></span> <span data-ttu-id="b903c-200">ToList （）方法可用來將電影組轉換成電影物件的一般集合（清單&lt;電影&gt;）。</span><span class="sxs-lookup"><span data-stu-id="b903c-200">The ToList() method is used to convert the set of movies into a generic collection of Movie objects (List&lt;Movie&gt;).</span></span>

<span data-ttu-id="b903c-201">電影記錄是透過 LINQ to Entities 的協助抓取。</span><span class="sxs-lookup"><span data-stu-id="b903c-201">The movie records are retrieved with the help of LINQ to Entities.</span></span> <span data-ttu-id="b903c-202">[清單 1] 中的 Index （）動作會使用 LINQ*方法語法*來抓取一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-202">The Index() action in Listing 1 uses LINQ *method syntax* to retrieve the set of database records.</span></span> <span data-ttu-id="b903c-203">如果您想要的話，可以改用 LINQ*查詢語法*。</span><span class="sxs-lookup"><span data-stu-id="b903c-203">If you prefer, you can use LINQ *query syntax* instead.</span></span> <span data-ttu-id="b903c-204">下列兩個語句會執行相同的動作：</span><span class="sxs-lookup"><span data-stu-id="b903c-204">The following two statements do the very same thing:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample2.cs)]

<span data-ttu-id="b903c-205">使用任何 LINQ 語法（方法語法或查詢語法），這是最直覺的方式。</span><span class="sxs-lookup"><span data-stu-id="b903c-205">Use whichever LINQ syntax – method syntax or query syntax – that you find most intuitive.</span></span> <span data-ttu-id="b903c-206">這兩種方法之間的效能不會有任何差異–唯一的差別在於樣式。</span><span class="sxs-lookup"><span data-stu-id="b903c-206">There is no difference in performance between the two approaches – the only difference is style.</span></span>

<span data-ttu-id="b903c-207">[清單 2] 中的視圖會用來顯示電影記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-207">The view in Listing 2 is used to display the movie records.</span></span>

<span data-ttu-id="b903c-208">**清單2– Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="b903c-208">**Listing 2 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample3.aspx)]

<span data-ttu-id="b903c-209">[清單 2] 中的視圖包含一個**foreach**迴圈，可逐一查看每個電影記錄，並顯示電影記錄的標題和主管屬性的值。</span><span class="sxs-lookup"><span data-stu-id="b903c-209">The view in Listing 2 contains a **foreach** loop that iterates through each movie record and displays the values of the movie record's Title and Director properties.</span></span> <span data-ttu-id="b903c-210">請注意，每個記錄旁都會顯示 [編輯] 和 [刪除] 連結。</span><span class="sxs-lookup"><span data-stu-id="b903c-210">Notice that an Edit and Delete link is displayed next to each record.</span></span> <span data-ttu-id="b903c-211">此外，[新增電影] 連結會出現在視圖底部（請參閱 [圖 7]）。</span><span class="sxs-lookup"><span data-stu-id="b903c-211">Furthermore, an Add Movie link appears at the bottom of the view (see Figure 7).</span></span>

<span data-ttu-id="b903c-212">**圖7–索引視圖**</span><span class="sxs-lookup"><span data-stu-id="b903c-212">**Figure 7 – The Index view**</span></span>

![clip_image014](creating-model-classes-with-the-entity-framework-cs/_static/image7.jpg)

<span data-ttu-id="b903c-214">索引視圖是具*類型的視圖*。</span><span class="sxs-lookup"><span data-stu-id="b903c-214">The Index view is a *typed view*.</span></span> <span data-ttu-id="b903c-215">索引視圖包含 &lt;% @ Page%&gt; 指示詞與*Inherits*屬性，可將模型屬性轉換成電影物件的強型別一般清單集合（清單&lt;movie）。</span><span class="sxs-lookup"><span data-stu-id="b903c-215">The Index view includes a &lt;%@ Page %&gt; directive with an *Inherits* attribute that casts the Model property to a strongly typed generic List collection of Movie objects (List&lt;Movie).</span></span>

## <a name="inserting-database-records-with-the-entity-framework"></a><span data-ttu-id="b903c-216">使用 Entity Framework 插入資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="b903c-216">Inserting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b903c-217">您可以使用 Entity Framework，讓您輕鬆地將新的記錄插入資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="b903c-217">You can use the Entity Framework to make it easy to insert new records into a database table.</span></span> <span data-ttu-id="b903c-218">[清單 3] 包含兩個新的動作，可供您用來將新記錄插入 Movie 資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="b903c-218">Listing 3 contains two new actions added to the Home controller class that you can use to insert new records into the Movie database table.</span></span>

<span data-ttu-id="b903c-219">**清單3– Controllers\HomeController.cs （新增方法）**</span><span class="sxs-lookup"><span data-stu-id="b903c-219">**Listing 3 – Controllers\HomeController.cs (Add methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample4.cs)]

<span data-ttu-id="b903c-220">第一個 Add （）動作只會傳回一個視圖。</span><span class="sxs-lookup"><span data-stu-id="b903c-220">The first Add() action simply returns a view.</span></span> <span data-ttu-id="b903c-221">此視圖包含一個表單，可用於新增電影資料庫記錄（請參閱 [圖 8]）。</span><span class="sxs-lookup"><span data-stu-id="b903c-221">The view contains a form for adding a new movie database record (see Figure 8).</span></span> <span data-ttu-id="b903c-222">當您提交表單時，會叫用第二個 Add （）動作。</span><span class="sxs-lookup"><span data-stu-id="b903c-222">When you submit the form, the second Add() action is invoked.</span></span>

<span data-ttu-id="b903c-223">請注意，第二個 Add （）動作會以 AcceptVerbs 屬性裝飾。</span><span class="sxs-lookup"><span data-stu-id="b903c-223">Notice that the second Add() action is decorated with the AcceptVerbs attribute.</span></span> <span data-ttu-id="b903c-224">只有在執行 HTTP POST 作業時，才可以叫用此動作。</span><span class="sxs-lookup"><span data-stu-id="b903c-224">This action can be invoked only when performing an HTTP POST operation.</span></span> <span data-ttu-id="b903c-225">換句話說，只有在張貼 HTML 表單時，才可以叫用此動作。</span><span class="sxs-lookup"><span data-stu-id="b903c-225">In other words, this action can only be invoked when posting an HTML form.</span></span>

<span data-ttu-id="b903c-226">第二個 Add （）動作會使用 ASP.NET MVC TryUpdateModel （）方法的協助，建立 Entity Framework Movie 類別的新實例。</span><span class="sxs-lookup"><span data-stu-id="b903c-226">The second Add() action creates a new instance of the Entity Framework Movie class with the help of the ASP.NET MVC TryUpdateModel() method.</span></span> <span data-ttu-id="b903c-227">TryUpdateModel （）方法會接受傳遞至 Add （）方法之 FormCollection 中的欄位，並將這些 HTML 表單欄位的值指派給 Movie 類別。</span><span class="sxs-lookup"><span data-stu-id="b903c-227">The TryUpdateModel() method takes the fields in the FormCollection passed to the Add() method and assigns the values of these HTML form fields to the Movie class.</span></span>

<span data-ttu-id="b903c-228">使用 Entity Framework 時，您必須在使用 TryUpdateModel 或 UpdateModel 方法來更新實體類別的屬性時，提供屬性的「白名單」。</span><span class="sxs-lookup"><span data-stu-id="b903c-228">When using the Entity Framework, you must supply a "white list" of properties when using the TryUpdateModel or UpdateModel methods to update the properties of an entity class.</span></span>

<span data-ttu-id="b903c-229">接下來，Add （）動作會執行一些簡單的表單驗證。</span><span class="sxs-lookup"><span data-stu-id="b903c-229">Next, the Add() action performs some simple form validation.</span></span> <span data-ttu-id="b903c-230">動作會確認 Title 和 Director 屬性都有值。</span><span class="sxs-lookup"><span data-stu-id="b903c-230">The action verifies that both the Title and Director properties have values.</span></span> <span data-ttu-id="b903c-231">如果發生驗證錯誤，則會將驗證錯誤訊息新增至 ModelState。</span><span class="sxs-lookup"><span data-stu-id="b903c-231">If there is a validation error, then a validation error message is added to ModelState.</span></span>

<span data-ttu-id="b903c-232">如果沒有任何驗證錯誤，則會在 [電影資料庫] 資料表中加入新的電影記錄，並提供 Entity Framework 的協助。</span><span class="sxs-lookup"><span data-stu-id="b903c-232">If there are no validation errors then a new movie record is added to the Movies database table with the help of the Entity Framework.</span></span> <span data-ttu-id="b903c-233">新記錄會使用下列兩行程式碼新增至資料庫：</span><span class="sxs-lookup"><span data-stu-id="b903c-233">The new record is added to the database with the following two lines of code:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample5.cs)]

<span data-ttu-id="b903c-234">第一行程式碼會將新的 Movie 實體新增至 Entity Framework 追蹤的電影集合。</span><span class="sxs-lookup"><span data-stu-id="b903c-234">The first line of code adds the new Movie entity to the set of movies being tracked by the Entity Framework.</span></span> <span data-ttu-id="b903c-235">第二行程式碼會儲存對重新追蹤至基礎資料庫的電影所做的任何變更。</span><span class="sxs-lookup"><span data-stu-id="b903c-235">The second line of code saves whatever changes have been made to the Movies being tracked back to the underlying database.</span></span>

<span data-ttu-id="b903c-236">**圖8–新增視圖**</span><span class="sxs-lookup"><span data-stu-id="b903c-236">**Figure 8 – The Add view**</span></span>

![clip_image016](creating-model-classes-with-the-entity-framework-cs/_static/image8.jpg)

#### <a name="updating-database-records-with-the-entity-framework"></a><span data-ttu-id="b903c-238">使用 Entity Framework 更新資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="b903c-238">Updating Database Records with the Entity Framework</span></span>

<span data-ttu-id="b903c-239">您可以遵循幾乎相同的方式，使用 Entity Framework 來編輯資料庫記錄，做為我們剛遵循以插入新資料庫記錄的方法。</span><span class="sxs-lookup"><span data-stu-id="b903c-239">You can follow almost the same approach to edit a database record with the Entity Framework as the approach that we just followed to insert a new database record.</span></span> <span data-ttu-id="b903c-240">[清單 4] 包含兩個名為 Edit （）的新控制器動作。</span><span class="sxs-lookup"><span data-stu-id="b903c-240">Listing 4 contains two new controller actions named Edit().</span></span> <span data-ttu-id="b903c-241">第一個 Edit （）動作會傳回用於編輯電影記錄的 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="b903c-241">The first Edit() action returns an HTML form for editing a movie record.</span></span> <span data-ttu-id="b903c-242">第二個 Edit （）動作會嘗試更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="b903c-242">The second Edit() action attempts to update the database.</span></span>

<span data-ttu-id="b903c-243">**清單4– Controllers\HomeController.cs （編輯方法）**</span><span class="sxs-lookup"><span data-stu-id="b903c-243">**Listing 4 – Controllers\HomeController.cs (Edit methods)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample6.cs)]

<span data-ttu-id="b903c-244">第二個 Edit （）動作一開始會從符合所編輯電影識別碼的資料庫中抓取電影記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-244">The second Edit() action starts by retrieving the Movie record from the database that matches the Id of the movie being edited.</span></span> <span data-ttu-id="b903c-245">下列 LINQ to Entities 語句會抓取符合特定識別碼的第一個資料庫記錄：</span><span class="sxs-lookup"><span data-stu-id="b903c-245">The following LINQ to Entities statement grabs the first database record that matches a particular Id:</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample7.cs)]

<span data-ttu-id="b903c-246">接下來，TryUpdateModel （）方法是用來將 HTML 表單欄位的值指派給 movie 實體的屬性。</span><span class="sxs-lookup"><span data-stu-id="b903c-246">Next, the TryUpdateModel() method is used to assign the values of the HTML form fields to the properties of the movie entity.</span></span> <span data-ttu-id="b903c-247">請注意，提供的白名單是用來指定要更新的確切屬性。</span><span class="sxs-lookup"><span data-stu-id="b903c-247">Notice that a white list is supplied to specify the exact properties to update.</span></span>

<span data-ttu-id="b903c-248">接下來，會執行一些簡單的驗證，以確認電影標題和主管屬性都有值。</span><span class="sxs-lookup"><span data-stu-id="b903c-248">Next, some simple validation is performed to verify that both the Movie Title and Director properties have values.</span></span> <span data-ttu-id="b903c-249">如果其中一個屬性遺漏值，則會將驗證錯誤訊息新增至 ModelState，而 ModelState 會傳回 false 值。</span><span class="sxs-lookup"><span data-stu-id="b903c-249">If either property is missing a value, then a validation error message is added to ModelState and ModelState.IsValid returns the value false.</span></span>

<span data-ttu-id="b903c-250">最後，如果沒有任何驗證錯誤，則會藉由呼叫 SaveChanges （）方法，將基礎電影資料庫資料表更新為任何變更。</span><span class="sxs-lookup"><span data-stu-id="b903c-250">Finally, if there are no validation errors, then the underlying Movies database table is updated with any changes by calling the SaveChanges() method.</span></span>

<span data-ttu-id="b903c-251">編輯資料庫記錄時，您必須將正在編輯的記錄識別碼傳遞至執行資料庫更新的控制器動作。</span><span class="sxs-lookup"><span data-stu-id="b903c-251">When editing database records, you need to pass the Id of the record being edited to the controller action that performs the database update.</span></span> <span data-ttu-id="b903c-252">否則，控制器動作將不會知道要在基礎資料庫中更新哪一筆記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-252">Otherwise, the controller action will not know which record to update in the underlying database.</span></span> <span data-ttu-id="b903c-253">[清單 5] 中包含的編輯檢視包含隱藏的表單欄位，代表正在編輯之資料庫記錄的識別碼。</span><span class="sxs-lookup"><span data-stu-id="b903c-253">The Edit view, contained in Listing 5, includes a hidden form field that represents the Id of the database record being edited.</span></span>

<span data-ttu-id="b903c-254">**清單5– Views\Home\Edit.aspx**</span><span class="sxs-lookup"><span data-stu-id="b903c-254">**Listing 5 – Views\Home\Edit.aspx**</span></span>

[!code-aspx[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample8.aspx)]

## <a name="deleting-database-records-with-the-entity-framework"></a><span data-ttu-id="b903c-255">使用 Entity Framework 刪除資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="b903c-255">Deleting Database Records with the Entity Framework</span></span>

<span data-ttu-id="b903c-256">我們在本教學課程中需要處理的最終資料庫作業，是刪除資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-256">The final database operation, which we need to tackle in this tutorial, is deleting database records.</span></span> <span data-ttu-id="b903c-257">您可以使用 [清單 6] 中的 [控制器] 動作來刪除特定的資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-257">You can use the controller action in Listing 6 to delete a particular database record.</span></span>

<span data-ttu-id="b903c-258">**清單 6--\Controllers\HomeController.cs （刪除動作）**</span><span class="sxs-lookup"><span data-stu-id="b903c-258">**Listing 6 -- \Controllers\HomeController.cs (Delete action)**</span></span>

[!code-csharp[Main](creating-model-classes-with-the-entity-framework-cs/samples/sample9.cs)]

<span data-ttu-id="b903c-259">Delete （）動作會先抓取符合傳遞給動作之識別碼的 Movie 實體。</span><span class="sxs-lookup"><span data-stu-id="b903c-259">The Delete() action first retrieves the Movie entity that matches the Id passed to the action.</span></span> <span data-ttu-id="b903c-260">接下來，藉由呼叫 DeleteObject （）方法並接著 SaveChanges （）方法，從資料庫刪除電影。</span><span class="sxs-lookup"><span data-stu-id="b903c-260">Next, the movie is deleted from the database by calling the DeleteObject() method followed by the SaveChanges() method.</span></span> <span data-ttu-id="b903c-261">最後，會將使用者重新導向回到索引視圖。</span><span class="sxs-lookup"><span data-stu-id="b903c-261">Finally, the user is redirected back to the Index view.</span></span>

## <a name="summary"></a><span data-ttu-id="b903c-262">總結</span><span class="sxs-lookup"><span data-stu-id="b903c-262">Summary</span></span>

<span data-ttu-id="b903c-263">本教學課程的目的是要示範如何利用 ASP.NET MVC 和 Microsoft Entity Framework，來建立資料庫導向的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="b903c-263">The purpose of this tutorial was to demonstrate how you can build database-driven web applications by taking advantage of ASP.NET MVC and the Microsoft Entity Framework.</span></span> <span data-ttu-id="b903c-264">您已瞭解如何建立可讓您選取、插入、更新和刪除資料庫記錄的應用程式。</span><span class="sxs-lookup"><span data-stu-id="b903c-264">You learned how to build an application that enables you to select, insert, update, and delete database records.</span></span>

<span data-ttu-id="b903c-265">首先，我們會討論如何使用實體資料模型 Wizard，從 Visual Studio 內產生實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="b903c-265">First, we discussed how you can use the Entity Data Model Wizard to generate an Entity Data Model from within Visual Studio.</span></span> <span data-ttu-id="b903c-266">接下來，您將瞭解如何使用 LINQ to Entities 從資料庫資料表中取出一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-266">Next, you learn how to use LINQ to Entities to retrieve a set of database records from a database table.</span></span> <span data-ttu-id="b903c-267">最後，我們使用 Entity Framework 來插入、更新和刪除資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="b903c-267">Finally, we used the Entity Framework to insert, update, and delete database records.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="b903c-268">下一個</span><span class="sxs-lookup"><span data-stu-id="b903c-268">Next</span></span>](creating-model-classes-with-linq-to-sql-cs.md)
