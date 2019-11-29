---
uid: mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
title: 顯示資料庫資料的資料表（VB） |Microsoft Docs
author: microsoft
description: 在本教學課程中，我將示範兩種顯示一組資料庫記錄的方法。 我在 HTML ta 中示範了兩種格式化一組資料庫記錄的方法 。
ms.author: riande
ms.date: 10/07/2008
ms.assetid: 5bb4587f-5bcd-44f5-b368-3c1709162b35
msc.legacyurl: /mvc/overview/older-versions-1/models-data/displaying-a-table-of-database-data-vb
msc.type: authoredcontent
ms.openlocfilehash: f2e2489ac8455913f55c746dbe05b9fe8272285b
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74590803"
---
# <a name="displaying-a-table-of-database-data-vb"></a><span data-ttu-id="cc6a4-104">顯示資料庫資料的資料表 (VB)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-104">Displaying a Table of Database Data (VB)</span></span>

<span data-ttu-id="cc6a4-105">由[Microsoft](https://github.com/microsoft)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-105">by [Microsoft](https://github.com/microsoft)</span></span>

[<span data-ttu-id="cc6a4-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="cc6a4-106">Download PDF</span></span>](https://download.microsoft.com/download/1/1/f/11f721aa-d749-4ed7-bb89-a681b68894e6/ASPNET_MVC_Tutorial_11_VB.pdf)

> <span data-ttu-id="cc6a4-107">在本教學課程中，我將示範兩種顯示一組資料庫記錄的方法。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-107">In this tutorial, I demonstrate two methods of displaying a set of database records.</span></span> <span data-ttu-id="cc6a4-108">我在 HTML 資料表中示範了兩種將一組資料庫記錄格式化的方法。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-108">I show two methods of formatting a set of database records in an HTML table.</span></span> <span data-ttu-id="cc6a4-109">首先，我會示範如何直接在視圖內格式化資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-109">First, I show how you can format the database records directly within a view.</span></span> <span data-ttu-id="cc6a4-110">接下來，我將示範在格式化資料庫記錄時，您可以如何利用部分。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-110">Next, I demonstrate how you can take advantage of partials when formatting database records.</span></span>

<span data-ttu-id="cc6a4-111">本教學課程的目的是要說明如何在 ASP.NET MVC 應用程式中顯示資料庫資料的 HTML 表格。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-111">The goal of this tutorial is to explain how you can display an HTML table of database data in an ASP.NET MVC application.</span></span> <span data-ttu-id="cc6a4-112">首先，您會瞭解如何使用 Visual Studio 所包含的樣板工具來產生可自動顯示一組記錄的視圖。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-112">First, you learn how to use the scaffolding tools included in Visual Studio to generate a view that displays a set of records automatically.</span></span> <span data-ttu-id="cc6a4-113">接下來，您將瞭解在格式化資料庫記錄時，如何使用部分做為範本。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-113">Next, you learn how to use a partial as a template when formatting database records.</span></span>

## <a name="create-the-model-classes"></a><span data-ttu-id="cc6a4-114">建立模型類別</span><span class="sxs-lookup"><span data-stu-id="cc6a4-114">Create the Model Classes</span></span>

<span data-ttu-id="cc6a4-115">我們即將顯示電影資料庫資料表中的一組記錄。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-115">We are going to display the set of records from the Movies database table.</span></span> <span data-ttu-id="cc6a4-116">電影資料庫資料表包含下列資料行：</span><span class="sxs-lookup"><span data-stu-id="cc6a4-116">The Movies database table contains the following columns:</span></span>

<a id="0.4_table01"></a>

| <span data-ttu-id="cc6a4-117">**資料行名稱**</span><span class="sxs-lookup"><span data-stu-id="cc6a4-117">**Column Name**</span></span> | <span data-ttu-id="cc6a4-118">**資料類型**</span><span class="sxs-lookup"><span data-stu-id="cc6a4-118">**Data Type**</span></span> | <span data-ttu-id="cc6a4-119">**允許 Null**</span><span class="sxs-lookup"><span data-stu-id="cc6a4-119">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="cc6a4-120">ID</span><span class="sxs-lookup"><span data-stu-id="cc6a4-120">Id</span></span> | <span data-ttu-id="cc6a4-121">Int</span><span class="sxs-lookup"><span data-stu-id="cc6a4-121">Int</span></span> | <span data-ttu-id="cc6a4-122">False</span><span class="sxs-lookup"><span data-stu-id="cc6a4-122">False</span></span> |
| <span data-ttu-id="cc6a4-123">標題</span><span class="sxs-lookup"><span data-stu-id="cc6a4-123">Title</span></span> | <span data-ttu-id="cc6a4-124">NVarchar （200）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-124">Nvarchar(200)</span></span> | <span data-ttu-id="cc6a4-125">False</span><span class="sxs-lookup"><span data-stu-id="cc6a4-125">False</span></span> |
| <span data-ttu-id="cc6a4-126">Director</span><span class="sxs-lookup"><span data-stu-id="cc6a4-126">Director</span></span> | <span data-ttu-id="cc6a4-127">NVarchar （50）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-127">NVarchar(50)</span></span> | <span data-ttu-id="cc6a4-128">False</span><span class="sxs-lookup"><span data-stu-id="cc6a4-128">False</span></span> |
| <span data-ttu-id="cc6a4-129">DateReleased</span><span class="sxs-lookup"><span data-stu-id="cc6a4-129">DateReleased</span></span> | <span data-ttu-id="cc6a4-130">DateTime</span><span class="sxs-lookup"><span data-stu-id="cc6a4-130">DateTime</span></span> | <span data-ttu-id="cc6a4-131">False</span><span class="sxs-lookup"><span data-stu-id="cc6a4-131">False</span></span> |

<span data-ttu-id="cc6a4-132">為了在 ASP.NET MVC 應用程式中呈現電影資料表，我們需要建立模型類別。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-132">In order to represent the Movies table in our ASP.NET MVC application, we need to create a model class.</span></span> <span data-ttu-id="cc6a4-133">在本教學課程中，我們會使用 Microsoft Entity Framework 來建立我們的模型類別。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-133">In this tutorial, we use the Microsoft Entity Framework to create our model classes.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="cc6a4-134">在本教學課程中，我們會使用 Microsoft Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-134">In this tutorial, we use the Microsoft Entity Framework.</span></span> <span data-ttu-id="cc6a4-135">不過，請務必瞭解，您可以使用各種不同的技術，從 ASP.NET MVC 應用程式與資料庫互動，包括 LINQ to SQL、NHibernate 或 ADO.NET。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-135">However, it is important to understand that you can use a variety of different technologies to interact with a database from an ASP.NET MVC application including LINQ to SQL, NHibernate, or ADO.NET.</span></span>

<span data-ttu-id="cc6a4-136">請遵循下列步驟來啟動實體資料模型 Wizard：</span><span class="sxs-lookup"><span data-stu-id="cc6a4-136">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="cc6a4-137">以滑鼠右鍵按一下 [方案總管] 視窗中的 [模型] 資料夾，然後選取 [**加入]、[新增專案**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-137">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="cc6a4-138">選取 [**資料**] 類別，然後選取 [ **ADO.NET 實體資料模型**] 範本。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-138">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="cc6a4-139">提供您的資料模型名稱*MoviesDBModel* ，然後按一下 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-139">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="cc6a4-140">按一下 [新增] 按鈕之後，[實體資料模型 Wizard] 隨即出現（請參閱 [圖 1]）。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-140">After you click the Add button, the Entity Data Model Wizard appears (see Figure 1).</span></span> <span data-ttu-id="cc6a4-141">請遵循下列步驟來完成嚮導：</span><span class="sxs-lookup"><span data-stu-id="cc6a4-141">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="cc6a4-142">在 [**選擇模型內容**] 步驟中，選取 [**從資料庫產生**] 選項。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-142">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="cc6a4-143">在 [**選擇您的資料**連線] 步驟中，使用 [ *MoviesDB* ] 資料連線和 [連線設定] 的名稱*MoviesDBEntities* 。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-143">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="cc6a4-144">按 [**下一步]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-144">Click the **Next** button.</span></span>
3. <span data-ttu-id="cc6a4-145">在 [**選擇您的資料庫物件**] 步驟中，展開 [資料表] 節點，選取 [電影] 資料表。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-145">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="cc6a4-146">輸入命名空間*模型*，然後按一下 [**完成]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-146">Enter the namespace *Models* and click the **Finish** button.</span></span>

<span data-ttu-id="cc6a4-147">[建立 LINQ to SQL 類別的 ![](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-147">[![Creating LINQ to SQL classes](displaying-a-table-of-database-data-vb/_static/image1.jpg)](displaying-a-table-of-database-data-vb/_static/image1.png)</span></span>

<span data-ttu-id="cc6a4-148">**圖 01**：建立 LINQ to SQL 類別（[按一下以觀看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-148">**Figure 01**: Creating LINQ to SQL classes ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image2.png))</span></span>

<span data-ttu-id="cc6a4-149">當您完成實體資料模型 Wizard 之後，實體資料模型設計工具隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-149">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="cc6a4-150">設計工具應該會顯示 [電影] 實體（請參閱 [圖 2]）。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-150">The Designer should display the Movies entity (see Figure 2).</span></span>

<span data-ttu-id="cc6a4-151">[![實體資料模型設計工具](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-151">[![The Entity Data Model Designer](displaying-a-table-of-database-data-vb/_static/image2.jpg)](displaying-a-table-of-database-data-vb/_static/image3.png)</span></span>

<span data-ttu-id="cc6a4-152">**圖 02**：實體資料模型設計工具（[按一下以查看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-152">**Figure 02**: The Entity Data Model Designer ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image4.png))</span></span>

<span data-ttu-id="cc6a4-153">我們需要先進行一項變更，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-153">We need to make one change before we continue.</span></span> <span data-ttu-id="cc6a4-154">「實體資料」 Wizard 會產生名為「*電影*」的模型類別，代表電影資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-154">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="cc6a4-155">因為我們將使用 Movie 類別來代表特定電影，所以我們需要將類別的名稱修改成*電影*，而不是*電影*（單數而非複數）。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-155">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="cc6a4-156">按兩下設計工具介面上的類別名稱，並將類別的名稱從電影變更為 Movie。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-156">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="cc6a4-157">進行這項變更之後，請按一下 [**儲存**] 按鈕（磁片磁碟機的圖示）以產生 Movie 類別。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-157">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="create-the-movies-controller"></a><span data-ttu-id="cc6a4-158">建立電影控制器</span><span class="sxs-lookup"><span data-stu-id="cc6a4-158">Create the Movies Controller</span></span>

<span data-ttu-id="cc6a4-159">既然我們已經有方法可以表示資料庫記錄，我們可以建立一個會傳回電影集合的控制器。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-159">Now that we have a way to represent our database records, we can create a controller that returns the collection of movies.</span></span> <span data-ttu-id="cc6a4-160">在 [Visual Studio 方案總管] 視窗中，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**新增]、[控制器**] 功能表選項（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-160">Within the Visual Studio Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller** (see Figure 3).</span></span>

<span data-ttu-id="cc6a4-161">[![[新增控制器] 功能表](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-161">[![The Add Controller Menu](displaying-a-table-of-database-data-vb/_static/image3.jpg)](displaying-a-table-of-database-data-vb/_static/image5.png)</span></span>

<span data-ttu-id="cc6a4-162">**圖 03**： [新增控制器] 功能表（[按一下以查看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-162">**Figure 03**: The Add Controller Menu ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image6.png))</span></span>

<span data-ttu-id="cc6a4-163">當 [**新增控制器**] 對話方塊出現時，請輸入控制器名稱 MovieController （請參閱 [圖 4]）。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-163">When the **Add Controller** dialog appears, enter the controller name MovieController (see Figure 4).</span></span> <span data-ttu-id="cc6a4-164">按一下 [**新增**] 按鈕以新增新的控制器。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-164">Click the **Add** button to add the new controller.</span></span>

<span data-ttu-id="cc6a4-165">[![[新增控制器] 對話方塊](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-165">[![The Add Controller dialog](displaying-a-table-of-database-data-vb/_static/image4.jpg)](displaying-a-table-of-database-data-vb/_static/image7.png)</span></span>

<span data-ttu-id="cc6a4-166">**圖 04**： [新增控制器] 對話方塊（[按一下以查看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-166">**Figure 04**: The Add Controller dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image8.png))</span></span>

<span data-ttu-id="cc6a4-167">我們需要修改 Movie controller 所公開的 Index （）動作，讓它傳回一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-167">We need to modify the Index() action exposed by the Movie controller so that it returns the set of database records.</span></span> <span data-ttu-id="cc6a4-168">修改控制器，使其看起來像 [清單 1] 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-168">Modify the controller so that it looks like the controller in Listing 1.</span></span>

<span data-ttu-id="cc6a4-169">**清單1– Controllers\MovieController.vb**</span><span class="sxs-lookup"><span data-stu-id="cc6a4-169">**Listing 1 – Controllers\MovieController.vb**</span></span>

[!code-vb[Main](displaying-a-table-of-database-data-vb/samples/sample1.vb)]

<span data-ttu-id="cc6a4-170">在 [清單 1] 中，MoviesDBEntities 類別是用來代表 MoviesDB 資料庫。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-170">In Listing 1, the MoviesDBEntities class is used to represent the MoviesDB database.</span></span> <span data-ttu-id="cc6a4-171">運算式*實體。MovieSet. ToList （）* 會傳回來自電影資料庫資料表的所有電影集合。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-171">The expression *entities.MovieSet.ToList()* returns the set of all movies from the Movies database table.</span></span>

## <a name="create-the-view"></a><span data-ttu-id="cc6a4-172">建立視圖</span><span class="sxs-lookup"><span data-stu-id="cc6a4-172">Create the View</span></span>

<span data-ttu-id="cc6a4-173">在 HTML 資料表中顯示一組資料庫記錄最簡單的方式，就是利用 Visual Studio 所提供的樣板。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-173">The easiest way to display a set of database records in an HTML table is to take advantage of the scaffolding provided by Visual Studio.</span></span>

<span data-ttu-id="cc6a4-174">選取 [**組建]、** [組建方案] 功能表選項來建立您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-174">Build your application by selecting the menu option **Build, Build Solution**.</span></span> <span data-ttu-id="cc6a4-175">您必須先建立應用程式，才能開啟 [**加入視圖**] 對話方塊，否則您的資料類別不會出現在對話方塊中。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-175">You must build your application before opening the **Add View** dialog or your data classes won't appear in the dialog.</span></span>

<span data-ttu-id="cc6a4-176">以滑鼠右鍵按一下 [索引] （）動作，然後選取 [**新增視圖**] 功能表選項（請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-176">Right-click the Index() action and select the menu option **Add View** (see Figure 5).</span></span>

<span data-ttu-id="cc6a4-177">[![新增視圖](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-177">[![Adding a view](displaying-a-table-of-database-data-vb/_static/image5.jpg)](displaying-a-table-of-database-data-vb/_static/image9.png)</span></span>

<span data-ttu-id="cc6a4-178">**圖 05**：加入視圖（[按一下以觀看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-178">**Figure 05**: Adding a view ([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image10.png))</span></span>

<span data-ttu-id="cc6a4-179">在 [**加入視圖**] 對話方塊中，核取標示為 [**建立強型別的視圖**] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-179">In the **Add View** dialog, check the checkbox labeled **Create a strongly-typed view**.</span></span> <span data-ttu-id="cc6a4-180">選取 Movie 類別做為**view 資料類別**。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-180">Select the Movie class as the **view data class**.</span></span> <span data-ttu-id="cc6a4-181">選取 [*清單*] 做為**視圖內容**（請參閱 [圖 6]）。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-181">Select *List* as the **view content** (see Figure 6).</span></span> <span data-ttu-id="cc6a4-182">選取這些選項會產生強型別視圖，以顯示電影清單。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-182">Selecting these options will generate a strongly-typed view that displays a list of movies.</span></span>

<span data-ttu-id="cc6a4-183">[![[加入視圖] 對話方塊](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-183">[![The Add View dialog](displaying-a-table-of-database-data-vb/_static/image6.jpg)](displaying-a-table-of-database-data-vb/_static/image11.png)</span></span>

<span data-ttu-id="cc6a4-184">**圖 06**： [加入視圖] 對話方塊（[按一下以查看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-184">**Figure 06**: The Add View dialog([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image12.png))</span></span>

<span data-ttu-id="cc6a4-185">按一下 [**新增**] 按鈕後，會自動產生 [清單 2] 中的視圖。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-185">After you click the **Add** button, the view in Listing 2 is generated automatically.</span></span> <span data-ttu-id="cc6a4-186">此視圖包含逐一查看電影集合，並顯示電影的每個內容所需的程式碼。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-186">This view contains the code required to iterate through the collection of movies and display each of the properties of a movie.</span></span>

<span data-ttu-id="cc6a4-187">**清單2– Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="cc6a4-187">**Listing 2 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample2.aspx)]

<span data-ttu-id="cc6a4-188">您可以選取功能表選項 [Debug]、[**開始調試**] （或按 F5 鍵）來執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-188">You can run the application by selecting the menu option **Debug, Start Debugging** (or hitting the F5 key).</span></span> <span data-ttu-id="cc6a4-189">執行應用程式會啟動 Internet Explorer。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-189">Running the application launches Internet Explorer.</span></span> <span data-ttu-id="cc6a4-190">如果您流覽至/Movie URL，則會看到 [圖 7] 中的頁面。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-190">If you navigate to the /Movie URL then you'll see the page in Figure 7.</span></span>

<span data-ttu-id="cc6a4-191">[![電影的資料表](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-191">[![A table of movies](displaying-a-table-of-database-data-vb/_static/image7.jpg)](displaying-a-table-of-database-data-vb/_static/image13.png)</span></span>

<span data-ttu-id="cc6a4-192">**圖 07**：電影的資料表（[按一下以觀看完整大小的影像](displaying-a-table-of-database-data-vb/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="cc6a4-192">**Figure 07**: A table of movies([Click to view full-size image](displaying-a-table-of-database-data-vb/_static/image14.png))</span></span>

<span data-ttu-id="cc6a4-193">如果您不喜歡 [圖 7] 中資料庫記錄方格外觀的任何內容，就可以直接修改索引視圖。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-193">If you don't like anything about the appearance of the grid of database records in Figure 7 then you can simply modify the Index view.</span></span> <span data-ttu-id="cc6a4-194">例如，您可以藉由修改索引視圖，將*DateReleased*標頭變更為 [*發行日期*]。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-194">For example, you can change the *DateReleased* header to *Date Released* by modifying the Index view.</span></span>

## <a name="create-a-template-with-a-partial"></a><span data-ttu-id="cc6a4-195">建立具有部分的範本</span><span class="sxs-lookup"><span data-stu-id="cc6a4-195">Create a Template with a Partial</span></span>

<span data-ttu-id="cc6a4-196">當 view 變得太複雜時，最好先將此觀點分解成部分。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-196">When a view gets too complicated, it is a good idea to start breaking the view into partials.</span></span> <span data-ttu-id="cc6a4-197">使用部分可讓您的觀點更容易瞭解和維護。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-197">Using partials makes your views easier to understand and maintain.</span></span> <span data-ttu-id="cc6a4-198">我們會建立一個部分，讓我們用來做為範本來設定每個電影資料庫記錄的格式。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-198">We'll create a partial that we can use as a template to format each of the movie database records.</span></span>

<span data-ttu-id="cc6a4-199">請遵循下列步驟來建立部分：</span><span class="sxs-lookup"><span data-stu-id="cc6a4-199">Follow these steps to create the partial:</span></span>

1. <span data-ttu-id="cc6a4-200">以滑鼠右鍵按一下 [Views\Movie] 資料夾，然後選取 [**新增視圖**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-200">Right-click the Views\Movie folder and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="cc6a4-201">選取標示為 *[建立部分視圖（.ascx）* ] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-201">Check the checkbox labeled *Create a partial view (.ascx)*.</span></span>
3. <span data-ttu-id="cc6a4-202">將部分*MovieTemplate*命名為。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-202">Name the partial *MovieTemplate*.</span></span>
4. <span data-ttu-id="cc6a4-203">核取標示為 [**建立強型別的視圖**] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-203">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
5. <span data-ttu-id="cc6a4-204">選取 [電影] 做為*view 資料類別*。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-204">Select Movie as the *view data class*.</span></span>
6. <span data-ttu-id="cc6a4-205">選取 [空白] 做為 [*視圖內容*]。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-205">Select Empty as the *view content*.</span></span>
7. <span data-ttu-id="cc6a4-206">按一下 [**新增**] 按鈕，將部分新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-206">Click the **Add** button to add the partial to your project.</span></span>

<span data-ttu-id="cc6a4-207">完成這些步驟之後，請修改 MovieTemplate 部分，看起來像 [清單 3]。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-207">After you complete these steps, modify the MovieTemplate partial to look like Listing 3.</span></span>

<span data-ttu-id="cc6a4-208">**清單3– Views\Movie\MovieTemplate.ascx**</span><span class="sxs-lookup"><span data-stu-id="cc6a4-208">**Listing 3 – Views\Movie\MovieTemplate.ascx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample3.aspx)]

<span data-ttu-id="cc6a4-209">[清單 3] 中的部分包含單一記錄資料列的範本。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-209">The partial in Listing 3 contains a template for a single row of records.</span></span>

<span data-ttu-id="cc6a4-210">[清單 4] 中修改過的索引視圖會使用 MovieTemplate 部分。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-210">The modified Index view in Listing 4 uses the MovieTemplate partial.</span></span>

<span data-ttu-id="cc6a4-211">**清單4– Views\Movie\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="cc6a4-211">**Listing 4 – Views\Movie\Index.aspx**</span></span>

[!code-aspx[Main](displaying-a-table-of-database-data-vb/samples/sample4.aspx)]

<span data-ttu-id="cc6a4-212">[清單 4] 中的視圖包含一個 For Each 迴圈，可逐一查看所有電影。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-212">The view in Listing 4 contains a For Each loop that iterates through all of the movies.</span></span> <span data-ttu-id="cc6a4-213">針對每個電影，MovieTemplate 部分是用來格式化電影。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-213">For each movie, the MovieTemplate partial is used to format the movie.</span></span> <span data-ttu-id="cc6a4-214">MovieTemplate 是藉由呼叫 RenderPartial （） helper 方法來呈現。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-214">The MovieTemplate is rendered by calling the RenderPartial() helper method.</span></span>

<span data-ttu-id="cc6a4-215">修改過的索引表會呈現資料庫記錄的相同 HTML 資料表。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-215">The modified Index view renders the very same HTML table of database records.</span></span> <span data-ttu-id="cc6a4-216">不過，此視圖已經大幅簡化。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-216">However, the view has been greatly simplified.</span></span>

<span data-ttu-id="cc6a4-217">RenderPartial （）方法與大多數其他 helper 方法不同，因為它不會傳回字串。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-217">The RenderPartial() method is different than most of the other helper methods because it does not return a string.</span></span> <span data-ttu-id="cc6a4-218">因此，您必須使用 &lt;% RenderPartial （）%&gt;，而不是 &lt;% = RenderPartial （）%&gt;來呼叫 RenderPartial （）方法。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-218">Therefore, you must call the RenderPartial() method using &lt;% Html.RenderPartial() %&gt; instead of &lt;%= Html.RenderPartial() %&gt;.</span></span>

## <a name="summary"></a><span data-ttu-id="cc6a4-219">總結</span><span class="sxs-lookup"><span data-stu-id="cc6a4-219">Summary</span></span>

<span data-ttu-id="cc6a4-220">本教學課程的目的是要說明如何在 HTML 資料表中顯示一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-220">The goal of this tutorial was to explain how you can display a set of database records in an HTML table.</span></span> <span data-ttu-id="cc6a4-221">首先，您已瞭解如何利用 Microsoft Entity Framework，從控制器動作傳回一組資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-221">First, you learned how to return a set of database records from a controller action by taking advantage of the Microsoft Entity Framework.</span></span> <span data-ttu-id="cc6a4-222">接下來，您已瞭解如何使用 Visual Studio 的架構來產生可自動顯示專案集合的視圖。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-222">Next, you learned how to use Visual Studio scaffolding to generate a view that displays a collection of items automatically.</span></span> <span data-ttu-id="cc6a4-223">最後，您已瞭解如何利用部分來簡化視圖。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-223">Finally, you learned how to simplify the view by taking advantage of a partial.</span></span> <span data-ttu-id="cc6a4-224">您已瞭解如何使用部分做為範本，讓您可以格式化每個資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="cc6a4-224">You learned how to use a partial as a template so that you can format each database record.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="cc6a4-225">[上一頁](creating-model-classes-with-linq-to-sql-vb.md)
> [下一頁](performing-simple-validation-vb.md)</span><span class="sxs-lookup"><span data-stu-id="cc6a4-225">[Previous](creating-model-classes-with-linq-to-sql-vb.md)
[Next](performing-simple-validation-vb.md)</span></span>
