---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
title: ASP.NET MVC 4 協助程式、表單和驗證 |Microsoft Docs
author: rick-anderson
description: 在 ASP.NET MVC 4 模型和資料存取實際操作實驗室中，您已從資料庫載入及顯示資料。 在此實際操作實驗室中，您將會新增至 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 187ee9cd-bc70-479b-bfed-f568b8da96eb
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-helpers-forms-and-validation
msc.type: authoredcontent
ms.openlocfilehash: 0e2605a4188eaf814f6ab0ebfeaabed4457bcfa3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78539575"
---
# <a name="aspnet-mvc-4-helpers-forms-and-validation"></a><span data-ttu-id="6f055-104">ASP.NET MVC 4 協助程式、表單和驗證</span><span class="sxs-lookup"><span data-stu-id="6f055-104">ASP.NET MVC 4 Helpers, Forms and Validation</span></span>

<span data-ttu-id="6f055-105">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="6f055-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="6f055-106">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="6f055-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="6f055-107">在**ASP.NET MVC 4 模型和資料存取**實際操作實驗室中，您已從資料庫載入及顯示資料。</span><span class="sxs-lookup"><span data-stu-id="6f055-107">In **ASP.NET MVC 4 Models and Data Access** Hands-on Lab, you have been loading and displaying data from the database.</span></span> <span data-ttu-id="6f055-108">在這個實際操作的實驗室中，您會將編輯該資料的能力新增至「**音樂存放區**」應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-108">In this Hands-on Lab, you will add to the **Music Store** application the ability to edit that data.</span></span>

<span data-ttu-id="6f055-109">記住該目標之後，您將會先建立控制器，以支援專輯的建立、讀取、更新和刪除（CRUD）動作。</span><span class="sxs-lookup"><span data-stu-id="6f055-109">With that goal in mind, you will first create the controller that will support the Create, Read, Update and Delete (CRUD) actions of albums.</span></span> <span data-ttu-id="6f055-110">您將會產生一個索引視圖範本，利用 ASP.NET MVC 的「樣板」功能，在 HTML 資料表中顯示專輯的屬性。</span><span class="sxs-lookup"><span data-stu-id="6f055-110">You will generate an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span> <span data-ttu-id="6f055-111">若要增強該視圖，您將加入自訂 HTML helper，將會截斷完整的描述。</span><span class="sxs-lookup"><span data-stu-id="6f055-111">To enhance that view, you will add a custom HTML helper that will truncate long descriptions.</span></span>

<span data-ttu-id="6f055-112">之後，您將會新增 [編輯] 和 [建立] 視圖，讓您可以改變資料庫中的專輯，並提供像是下拉式清單等表單元素的協助。</span><span class="sxs-lookup"><span data-stu-id="6f055-112">Afterwards, you will add the Edit and Create Views that will let you alter the albums in the database, with the help of form elements like dropdowns.</span></span>

<span data-ttu-id="6f055-113">最後，您會讓使用者刪除專輯，同時您也可以藉由驗證其輸入，防止他們輸入錯誤的資料。</span><span class="sxs-lookup"><span data-stu-id="6f055-113">Lastly, you will let users delete an album and also you will prevent them from entering wrong data by validating their input.</span></span>

<span data-ttu-id="6f055-114">這個實際操作實驗室假設您有**ASP.NET MVC**的基本知識。</span><span class="sxs-lookup"><span data-stu-id="6f055-114">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="6f055-115">如果您之前未使用過**ASP.NET mvc** ，建議您移至**ASP.NET mvc 基礎**實際操作實驗室。</span><span class="sxs-lookup"><span data-stu-id="6f055-115">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="6f055-116">本實驗室將針對源資料夾中提供的範例 Web 應用程式套用次要變更，引導您完成先前所述的增強功能和新功能。</span><span class="sxs-lookup"><span data-stu-id="6f055-116">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="6f055-117">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="6f055-117">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="6f055-118">此實驗室的特定專案可在[ASP.NET MVC 4 helper、表單和驗證中](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation)取得。</span><span class="sxs-lookup"><span data-stu-id="6f055-118">The project specific to this lab is available at [ASP.NET MVC 4 Helpers, Forms and Validation](https://github.com/Microsoft-Web/HOL-MVC4HelpersFormsAndValidation).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="6f055-119">目標</span><span class="sxs-lookup"><span data-stu-id="6f055-119">Objectives</span></span>

<span data-ttu-id="6f055-120">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="6f055-120">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="6f055-121">建立控制器以支援 CRUD 作業</span><span class="sxs-lookup"><span data-stu-id="6f055-121">Create a controller to support CRUD operations</span></span>
- <span data-ttu-id="6f055-122">產生索引視圖以顯示 HTML 資料表中的實體屬性</span><span class="sxs-lookup"><span data-stu-id="6f055-122">Generate an Index View to display entity properties in an HTML table</span></span>
- <span data-ttu-id="6f055-123">新增自訂 HTML helper</span><span class="sxs-lookup"><span data-stu-id="6f055-123">Add a custom HTML helper</span></span>
- <span data-ttu-id="6f055-124">建立和自訂編輯檢視</span><span class="sxs-lookup"><span data-stu-id="6f055-124">Create and customize an Edit View</span></span>
- <span data-ttu-id="6f055-125">區分回應 HTTP GET 或 HTTP POST 呼叫的動作方法</span><span class="sxs-lookup"><span data-stu-id="6f055-125">Differentiate between action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="6f055-126">新增和自訂建立視圖</span><span class="sxs-lookup"><span data-stu-id="6f055-126">Add and customize a Create View</span></span>
- <span data-ttu-id="6f055-127">處理實體的刪除</span><span class="sxs-lookup"><span data-stu-id="6f055-127">Handle the deletion of an entity</span></span>
- <span data-ttu-id="6f055-128">驗證使用者輸入</span><span class="sxs-lookup"><span data-stu-id="6f055-128">Validate user input</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="6f055-129">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6f055-129">Prerequisites</span></span>

<span data-ttu-id="6f055-130">您必須具有下列專案，才能完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="6f055-130">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="6f055-131">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。</span><span class="sxs-lookup"><span data-stu-id="6f055-131">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="6f055-132">安裝程式</span><span class="sxs-lookup"><span data-stu-id="6f055-132">Setup</span></span>

<span data-ttu-id="6f055-133">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="6f055-133">**Installing Code Snippets**</span></span>

<span data-ttu-id="6f055-134">為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。</span><span class="sxs-lookup"><span data-stu-id="6f055-134">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="6f055-135">若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="6f055-135">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="6f055-136">如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 B：使用程式碼片段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="6f055-136">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="6f055-137">練習</span><span class="sxs-lookup"><span data-stu-id="6f055-137">Exercises</span></span>

<span data-ttu-id="6f055-138">下列練習會組成這個實際操作實驗室：</span><span class="sxs-lookup"><span data-stu-id="6f055-138">The following exercises make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="6f055-139">建立存放管理員控制器及其索引視圖</span><span class="sxs-lookup"><span data-stu-id="6f055-139">Creating the Store Manager controller and its Index view</span></span>](#Exercise1)
2. [<span data-ttu-id="6f055-140">新增 HTML Helper</span><span class="sxs-lookup"><span data-stu-id="6f055-140">Adding an HTML Helper</span></span>](#Exercise2)
3. [<span data-ttu-id="6f055-141">建立編輯檢視</span><span class="sxs-lookup"><span data-stu-id="6f055-141">Creating the Edit View</span></span>](#Exercise3)
4. [<span data-ttu-id="6f055-142">新增建立視圖</span><span class="sxs-lookup"><span data-stu-id="6f055-142">Adding a Create View</span></span>](#Exercise4)
5. [<span data-ttu-id="6f055-143">處理刪除</span><span class="sxs-lookup"><span data-stu-id="6f055-143">Handling Deletion</span></span>](#Exercise5)
6. [<span data-ttu-id="6f055-144">新增驗證</span><span class="sxs-lookup"><span data-stu-id="6f055-144">Adding Validation</span></span>](#Exercise6)
7. [<span data-ttu-id="6f055-145">在用戶端使用不顯眼的 jQuery</span><span class="sxs-lookup"><span data-stu-id="6f055-145">Using Unobtrusive jQuery at Client Side</span></span>](#Exercise7)

> [!NOTE]
> <span data-ttu-id="6f055-146">每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-146">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="6f055-147">如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。</span><span class="sxs-lookup"><span data-stu-id="6f055-147">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="6f055-148">完成此實驗室的預估時間： **60 分鐘**</span><span class="sxs-lookup"><span data-stu-id="6f055-148">Estimated time to complete this lab: **60 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Creating_the_Store_Manager_controller_and_its_Index_view"></a>
### <a name="exercise-1-creating-the-store-manager-controller-and-its-index-view"></a><span data-ttu-id="6f055-149">練習1：建立存放管理員控制器及其索引視圖</span><span class="sxs-lookup"><span data-stu-id="6f055-149">Exercise 1: Creating the Store Manager controller and its Index view</span></span>

<span data-ttu-id="6f055-150">在此練習中，您將瞭解如何建立新的控制器以支援 CRUD 作業、自訂其索引動作方法，以從資料庫傳回專輯清單，最後再產生利用 ASP.NET MVC 的樣板的索引檢視器範本在 HTML 表格中顯示專輯屬性的功能。</span><span class="sxs-lookup"><span data-stu-id="6f055-150">In this exercise, you will learn how to create a new controller to support CRUD operations, customize its Index action method to return a list of albums from the database and finally generating an Index View template taking advantage of ASP.NET MVC's scaffolding feature to display the albums' properties in an HTML table.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Creating_the_StoreManagerController"></a>
#### <a name="task-1---creating-the-storemanagercontroller"></a><span data-ttu-id="6f055-151">工作 1-建立 StoreManagerController</span><span class="sxs-lookup"><span data-stu-id="6f055-151">Task 1 - Creating the StoreManagerController</span></span>

<span data-ttu-id="6f055-152">在這項工作中，您將建立名為**StoreManagerController**的新控制器，以支援 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="6f055-152">In this task, you will create a new controller called **StoreManagerController** to support CRUD operations.</span></span>

1. <span data-ttu-id="6f055-153">開啟位於**來源/Ex1-CreatingTheStoreManagerController/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-153">Open the **Begin** solution located at **Source/Ex1-CreatingTheStoreManagerController/Begin/** folder.</span></span>

   1. <span data-ttu-id="6f055-154">在繼續之前，您必須先下載一些遺漏的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="6f055-154">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="6f055-155">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-155">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="6f055-156">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="6f055-156">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="6f055-157">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-157">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6f055-158">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="6f055-158">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="6f055-159">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f055-159">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="6f055-160">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6f055-160">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="6f055-161">新增控制器。</span><span class="sxs-lookup"><span data-stu-id="6f055-161">Add a new controller.</span></span> <span data-ttu-id="6f055-162">若要這麼做，請在方案總管內的 [**控制器**] 資料夾上按一下滑鼠右鍵，然後依序選取 [**新增**] 和 [**控制器**] 命令。</span><span class="sxs-lookup"><span data-stu-id="6f055-162">To do this, right-click the **Controllers** folder within the Solution Explorer, select **Add** and then the **Controller** command.</span></span> <span data-ttu-id="6f055-163">將**控制器** **名稱**變更為**StoreManagerController** ，並確認已選取 [**具有空白讀取/寫入動作的 MVC 控制器**] 選項。</span><span class="sxs-lookup"><span data-stu-id="6f055-163">Change the **Controller** **Name** to **StoreManagerController** and make sure the option **MVC controller with empty read/write actions** is selected.</span></span> <span data-ttu-id="6f055-164">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="6f055-164">Click **Add**.</span></span>

    <span data-ttu-id="6f055-165">![[新增控制器] 對話方塊](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "[加入控制器] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="6f055-165">![Add controller dialog](aspnet-mvc-4-helpers-forms-and-validation/_static/image1.png "Add controller dialog")</span></span>

    <span data-ttu-id="6f055-166">*[新增控制器] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="6f055-166">*Add Controller Dialog*</span></span>

    <span data-ttu-id="6f055-167">會產生新的控制器類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-167">A new Controller class is generated.</span></span> <span data-ttu-id="6f055-168">由於您指定要為讀取/寫入新增動作，因此會使用已填入的 TODO 批註來建立常見的 CRUD 動作，並提示包含應用程式特定的邏輯。</span><span class="sxs-lookup"><span data-stu-id="6f055-168">Since you indicated to add actions for read/write, stub methods for those, common CRUD actions are created with TODO comments filled in, prompting to include the application specific logic.</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Customizing_the_StoreManager_Index"></a>
#### <a name="task-2---customizing-the-storemanager-index"></a><span data-ttu-id="6f055-169">工作 2-自訂 StoreManager 索引</span><span class="sxs-lookup"><span data-stu-id="6f055-169">Task 2 - Customizing the StoreManager Index</span></span>

<span data-ttu-id="6f055-170">在這項工作中，您將自訂 StoreManager 索引動作方法，以傳回具有資料庫專輯清單的視圖。</span><span class="sxs-lookup"><span data-stu-id="6f055-170">In this task, you will customize the StoreManager Index action method to return a View with the list of albums from the database.</span></span>

1. <span data-ttu-id="6f055-171">在 StoreManagerController 類別中，新增下列*using*指示詞。</span><span class="sxs-lookup"><span data-stu-id="6f055-171">In the StoreManagerController class, add the following *using* directives.</span></span>

    <span data-ttu-id="6f055-172">（程式碼片段-*使用 MvcMusicStore ASP.NET MVC 4 協助程式和表單和驗證-Ex1*）</span><span class="sxs-lookup"><span data-stu-id="6f055-172">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 using MvcMusicStore*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample1.cs)]
2. <span data-ttu-id="6f055-173">將欄位加入至**StoreManagerController** ，以保存 MusicStoreEntities 的實例 **。**</span><span class="sxs-lookup"><span data-stu-id="6f055-173">Add a field to the **StoreManagerController** to hold an instance of **MusicStoreEntities.**</span></span>

    <span data-ttu-id="6f055-174">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex1 MusicStoreEntities*）</span><span class="sxs-lookup"><span data-stu-id="6f055-174">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample2.cs)]
3. <span data-ttu-id="6f055-175">執行 StoreManagerController 索引動作，以使用專輯清單傳回視圖。</span><span class="sxs-lookup"><span data-stu-id="6f055-175">Implement the StoreManagerController Index action to return a View with the list of albums.</span></span>

    <span data-ttu-id="6f055-176">控制器動作邏輯與先前撰寫的 StoreController 索引動作非常類似。</span><span class="sxs-lookup"><span data-stu-id="6f055-176">The Controller action logic will be very similar to the StoreController's Index action written earlier.</span></span> <span data-ttu-id="6f055-177">使用 LINQ 取出所有專輯，包括顯示的內容類型和演出者資訊。</span><span class="sxs-lookup"><span data-stu-id="6f055-177">Use LINQ to retrieve all albums, including Genre and Artist information for display.</span></span>

    <span data-ttu-id="6f055-178">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex1 StoreManagerController 索引*）</span><span class="sxs-lookup"><span data-stu-id="6f055-178">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex1 StoreManagerController Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample3.cs)]

<a id="Ex1Task3"></a>

<a id="strongTask_3_-_Creating_the_Index_Viewstrong"></a>
#### <a name="task-3---creating-the-index-view"></a><span data-ttu-id="6f055-179">工作 3-建立索引視圖</span><span class="sxs-lookup"><span data-stu-id="6f055-179">Task 3 - Creating the Index View</span></span>

<span data-ttu-id="6f055-180">在這項工作中，您將建立索引視圖範本，以顯示**StoreManager**控制器所傳回的專輯清單。</span><span class="sxs-lookup"><span data-stu-id="6f055-180">In this task, you will create the Index View template to display the list of albums returned by the **StoreManager** Controller.</span></span>

1. <span data-ttu-id="6f055-181">在建立新的視圖範本之前，您應該先建立專案，讓 [**加入視圖] 對話方塊**知道要使用的**專輯**類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-181">Before creating the new View template, you should build the project so that the **Add View Dialog** knows about the **Album** class to use.</span></span> <span data-ttu-id="6f055-182">選取**組建 |組建 MvcMusicStore**以建立專案。</span><span class="sxs-lookup"><span data-stu-id="6f055-182">Select **Build | Build MvcMusicStore** to build the project.</span></span>
2. <span data-ttu-id="6f055-183">在**索引**動作方法內按一下滑鼠右鍵，然後選取 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-183">Right-click inside the **Index** action method and select **Add View**.</span></span> <span data-ttu-id="6f055-184">這會顯示 [**加入視圖**] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6f055-184">This will bring up the **Add View** dialog.</span></span>

    <span data-ttu-id="6f055-185">![加入視圖](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "加入視圖")</span><span class="sxs-lookup"><span data-stu-id="6f055-185">![Add view](aspnet-mvc-4-helpers-forms-and-validation/_static/image2.png "Add view")</span></span>

    <span data-ttu-id="6f055-186">*從 Index 方法內加入視圖*</span><span class="sxs-lookup"><span data-stu-id="6f055-186">*Adding a View from within the Index method*</span></span>
3. <span data-ttu-id="6f055-187">在 [加入視圖] 對話方塊中，確認視圖名稱為 [**索引**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-187">In the Add View dialog, verify that the View Name is **Index**.</span></span> <span data-ttu-id="6f055-188">選取 [**建立強型別視圖**] 選項，然後從 [**模型類別**] 下拉式選單選取 [**專輯] （MvcMusicStore）** 。</span><span class="sxs-lookup"><span data-stu-id="6f055-188">Select the **Create a strongly-typed view** option, and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="6f055-189">從 [ **Scaffold 範本**] 下拉式清單中選取 [**清單**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-189">Select **List** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="6f055-190">將 [ **View engine** ] 保留為**Razor** ，其他欄位則設為預設值，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-190">Leave the **View engine** to **Razor** and the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="6f055-191">![加入索引視圖](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "加入索引視圖")</span><span class="sxs-lookup"><span data-stu-id="6f055-191">![Adding an index view](aspnet-mvc-4-helpers-forms-and-validation/_static/image3.png "Adding an index view")</span></span>

    <span data-ttu-id="6f055-192">*加入索引視圖*</span><span class="sxs-lookup"><span data-stu-id="6f055-192">*Adding an Index View*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Customizing_the_scaffold_of_the_Index_View"></a>
#### <a name="task-4---customizing-the-scaffold-of-the-index-view"></a><span data-ttu-id="6f055-193">工作 4-自訂索引視圖的 scaffold</span><span class="sxs-lookup"><span data-stu-id="6f055-193">Task 4 - Customizing the scaffold of the Index View</span></span>

<span data-ttu-id="6f055-194">在這項工作中，您將調整以 ASP.NET MVC 樣板功能建立的簡單視圖範本，讓它顯示您想要的欄位。</span><span class="sxs-lookup"><span data-stu-id="6f055-194">In this task, you will adjust the simple View template created with ASP.NET MVC scaffolding feature to have it display the fields you want.</span></span>

> [!NOTE]
> <span data-ttu-id="6f055-195">ASP.NET MVC 中的樣板支援會產生一個簡單的視圖範本，其中會列出專輯模型**中的所有**欄位。</span><span class="sxs-lookup"><span data-stu-id="6f055-195">The **scaffolding** support within ASP.NET MVC generates a simple View template which lists all fields in the Album model.</span></span> <span data-ttu-id="6f055-196">[樣板 **] 提供快速**開始使用強型別視圖的方式：您可以快速地產生預設範本，然後修改產生的程式碼，而不需要手動撰寫視圖範本。</span><span class="sxs-lookup"><span data-stu-id="6f055-196">**Scaffolding** provides a quick way to get started on a strongly typed view: rather than having to write the View template manually, scaffolding quickly generates a default template and then you can modify the generated code.</span></span>

1. <span data-ttu-id="6f055-197">檢查所建立的程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f055-197">Review the code created.</span></span> <span data-ttu-id="6f055-198">產生的欄位清單將會是下列 HTML**資料表的一部分，而**該架構會用來顯示表格式資料。</span><span class="sxs-lookup"><span data-stu-id="6f055-198">The generated list of fields will be part of the following HTML table that **Scaffolding** is using for displaying tabular data.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample4.cshtml)]
2. <span data-ttu-id="6f055-199">以下列程式碼取代 **&lt;資料表&gt;** 程式**代碼，以顯示 [內容**類型]、[**演出者**]、[**專輯標題**] 和 [**價格**] 欄位。</span><span class="sxs-lookup"><span data-stu-id="6f055-199">Replace the **&lt;table&gt;** code with the following code to display only the **Genre**, **Artist**, **Album Title**, and **Price** fields.</span></span> <span data-ttu-id="6f055-200">這會刪除 [ **AlbumId** ] 和 [**專輯封面 URL** ] 資料行。</span><span class="sxs-lookup"><span data-stu-id="6f055-200">This deletes the **AlbumId** and **Album Art URL** columns.</span></span> <span data-ttu-id="6f055-201">此外，它也會變更 GenreId 和 ArtistId 資料行，以顯示其**Artist.Name**和**Genre.Name**的連結類別屬性，並移除 [**詳細資料**] 連結。</span><span class="sxs-lookup"><span data-stu-id="6f055-201">Also, it changes GenreId and ArtistId columns to display their linked class properties of **Artist.Name** and **Genre.Name**, and removes the **Details** link.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample5.cshtml)]
3. <span data-ttu-id="6f055-202">變更下列說明。</span><span class="sxs-lookup"><span data-stu-id="6f055-202">Change the following descriptions.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample6.cshtml)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="6f055-203">工作 5-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-203">Task 5 - Running the Application</span></span>

<span data-ttu-id="6f055-204">在這項工作中，您將測試**StoreManager** **索引**視圖範本是否根據先前步驟的設計來顯示專輯清單。</span><span class="sxs-lookup"><span data-stu-id="6f055-204">In this task, you will test that the **StoreManager** **Index** View template displays a list of albums according to the design of the previous steps.</span></span>

1. <span data-ttu-id="6f055-205">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-205">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-206">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-206">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-207">將 URL 變更為 [ **/StoreManager** ]，以確認專輯清單已顯示，並顯示其 [**標題**]、[**演出者** **] 和 [** 內容類型]。</span><span class="sxs-lookup"><span data-stu-id="6f055-207">Change the URL to **/StoreManager** to verify that a list of albums is displayed, showing their **Title**, **Artist** and **Genre**.</span></span>

    <span data-ttu-id="6f055-208">![流覽專輯清單](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "流覽專輯清單")</span><span class="sxs-lookup"><span data-stu-id="6f055-208">![Browsing the list of albums](aspnet-mvc-4-helpers-forms-and-validation/_static/image4.png "Browsing the list of albums")</span></span>

    <span data-ttu-id="6f055-209">*流覽專輯清單*</span><span class="sxs-lookup"><span data-stu-id="6f055-209">*Browsing the list of albums*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Adding_an_HTML_Helper"></a>
### <a name="exercise-2-adding-an-html-helper"></a><span data-ttu-id="6f055-210">練習2：新增 HTML Helper</span><span class="sxs-lookup"><span data-stu-id="6f055-210">Exercise 2: Adding an HTML Helper</span></span>

<span data-ttu-id="6f055-211">StoreManager 的 [索引] 頁面有一個可能的問題： [標題] 和 [演出者名稱] 屬性可以夠長的時間，以擲出資料表格式。</span><span class="sxs-lookup"><span data-stu-id="6f055-211">The StoreManager Index page has one potential issue: Title and Artist Name properties can both be long enough to throw off the table formatting.</span></span> <span data-ttu-id="6f055-212">在此練習中，您將學習如何新增自訂 HTML helper 來截斷該文字。</span><span class="sxs-lookup"><span data-stu-id="6f055-212">In this exercise you will learn how to add a custom HTML helper to truncate that text.</span></span>

<span data-ttu-id="6f055-213">在下圖中，您可以看到當您使用小型瀏覽器大小時，如何修改格式。</span><span class="sxs-lookup"><span data-stu-id="6f055-213">In the following figure, you can see how the format is modified because of the length of the text when you use a small browser size.</span></span>

<span data-ttu-id="6f055-214">![流覽未截斷文字的專輯清單](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "流覽未截斷文字的專輯清單")</span><span class="sxs-lookup"><span data-stu-id="6f055-214">![Browsing the list of Albums with not truncated text](aspnet-mvc-4-helpers-forms-and-validation/_static/image5.png "Browsing the list of Albums with not truncated text")</span></span>

<span data-ttu-id="6f055-215">*流覽未截斷文字的專輯清單*</span><span class="sxs-lookup"><span data-stu-id="6f055-215">*Browsing the list of Albums with not truncated text*</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Extending_the_HTML_Helper"></a>
#### <a name="task-1---extending-the-html-helper"></a><span data-ttu-id="6f055-216">工作 1-擴充 HTML Helper</span><span class="sxs-lookup"><span data-stu-id="6f055-216">Task 1 - Extending the HTML Helper</span></span>

<span data-ttu-id="6f055-217">在這項工作中，您會將新方法**截斷**至 ASP.NET MVC Views 內公開的**HTML**物件。</span><span class="sxs-lookup"><span data-stu-id="6f055-217">In this task, you will add a new method **Truncate** to the **HTML** object exposed within ASP.NET MVC Views.</span></span> <span data-ttu-id="6f055-218">若要這麼做，您要將**擴充方法**實作為 ASP.NET Mvc 所提供的內建**system.web. HtmlHelper**類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-218">To do this, you will implement an **extension method** to the built-in **System.Web.Mvc.HtmlHelper** class provided by ASP.NET MVC.</span></span>

> [!NOTE]
> <span data-ttu-id="6f055-219">如需**擴充方法**的詳細資訊，請造訪這篇 msdn 文章。</span><span class="sxs-lookup"><span data-stu-id="6f055-219">To read more about **Extension Methods**, please visit this msdn article.</span></span> <span data-ttu-id="6f055-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span><span class="sxs-lookup"><span data-stu-id="6f055-220">[https://msdn.microsoft.com/library/bb383977.aspx](https://msdn.microsoft.com/library/bb383977.aspx).</span></span>

1. <span data-ttu-id="6f055-221">開啟位於**來源/Ex2-AddingAnHTMLHelper/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-221">Open the **Begin** solution located at **Source/Ex2-AddingAnHTMLHelper/Begin/** folder.</span></span> <span data-ttu-id="6f055-222">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-222">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="6f055-223">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="6f055-223">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="6f055-224">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-224">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="6f055-225">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="6f055-225">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="6f055-226">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-226">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6f055-227">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="6f055-227">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="6f055-228">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f055-228">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="6f055-229">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6f055-229">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="6f055-230">開啟 StoreManager 的索引視圖。</span><span class="sxs-lookup"><span data-stu-id="6f055-230">Open StoreManager's Index View.</span></span> <span data-ttu-id="6f055-231">若要這麼做，請在 方案總管展開  **Views**  資料夾，然後**StoreManager**並開啟  **Index. cshtml**  檔案。</span><span class="sxs-lookup"><span data-stu-id="6f055-231">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
3. <span data-ttu-id="6f055-232">在<strong>@model</strong>指示詞底下新增下列程式碼，以定義<strong>截斷</strong>helper 方法。</span><span class="sxs-lookup"><span data-stu-id="6f055-232">Add the following code below the <strong>@model</strong> directive to define the <strong>Truncate</strong> helper method.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample7.cshtml)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Truncating_Text_in_the_Page"></a>
#### <a name="task-2---truncating-text-in-the-page"></a><span data-ttu-id="6f055-233">工作 2-截斷頁面中的文字</span><span class="sxs-lookup"><span data-stu-id="6f055-233">Task 2 - Truncating Text in the Page</span></span>

<span data-ttu-id="6f055-234">在這項工作中，您將使用**截斷**方法來截斷 View 範本中的文字。</span><span class="sxs-lookup"><span data-stu-id="6f055-234">In this task, you will use the **Truncate** method to truncate the text in the View template.</span></span>

1. <span data-ttu-id="6f055-235">開啟 StoreManager 的索引視圖。</span><span class="sxs-lookup"><span data-stu-id="6f055-235">Open StoreManager's Index View.</span></span> <span data-ttu-id="6f055-236">若要這麼做，請在 方案總管展開  **Views**  資料夾，然後**StoreManager**並開啟  **Index. cshtml**  檔案。</span><span class="sxs-lookup"><span data-stu-id="6f055-236">To do this, in the Solution Explorer expand the **Views** folder, then the **StoreManager** and open the **Index.cshtml** file.</span></span>
2. <span data-ttu-id="6f055-237">取代顯示**演出者名稱**和專輯**標題**的行。</span><span class="sxs-lookup"><span data-stu-id="6f055-237">Replace the lines that show the **Artist Name** and Album's **Title**.</span></span> <span data-ttu-id="6f055-238">若要這麼做，請取代下列幾行。</span><span class="sxs-lookup"><span data-stu-id="6f055-238">To do this, replace the following lines.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample8.cshtml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="6f055-239">工作 3-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-239">Task 3 - Running the Application</span></span>

<span data-ttu-id="6f055-240">在這項工作中，您將測試**StoreManager** **索引**視圖範本是否會截斷專輯的標題和演出者名稱。</span><span class="sxs-lookup"><span data-stu-id="6f055-240">In this task, you will test that the **StoreManager** **Index** View template truncates the Album's Title and Artist Name.</span></span>

1. <span data-ttu-id="6f055-241">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-241">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-242">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-242">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-243">將 URL 變更為 **/StoreManager** ，以確認 [**標題**] 和 [**演出者**] 資料行中的長文字已截斷。</span><span class="sxs-lookup"><span data-stu-id="6f055-243">Change the URL to **/StoreManager** to verify that long texts in the **Title** and **Artist** column are truncated.</span></span>

    <span data-ttu-id="6f055-244">![截斷的標題和演出者名稱](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "截斷的標題和演出者名稱")</span><span class="sxs-lookup"><span data-stu-id="6f055-244">![Truncated titles and artists names](aspnet-mvc-4-helpers-forms-and-validation/_static/image6.png "Truncated titles and artists names")</span></span>

    <span data-ttu-id="6f055-245">*截斷的標題和演出者名稱*</span><span class="sxs-lookup"><span data-stu-id="6f055-245">*Truncated Titles and Artist Names*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Creating_the_Edit_View"></a>
### <a name="exercise-3-creating-the-edit-view"></a><span data-ttu-id="6f055-246">練習3：建立編輯檢視</span><span class="sxs-lookup"><span data-stu-id="6f055-246">Exercise 3: Creating the Edit View</span></span>

<span data-ttu-id="6f055-247">在此練習中，您將瞭解如何建立表單，以允許商店經理編輯專輯。</span><span class="sxs-lookup"><span data-stu-id="6f055-247">In this exercise, you will learn how to create a form to allow store managers to edit an Album.</span></span> <span data-ttu-id="6f055-248">他們會流覽 **/StoreManager/Edit/id** URL （**id**是要編輯之專輯的唯一識別碼），因此會對伺服器進行 HTTP GET 呼叫。</span><span class="sxs-lookup"><span data-stu-id="6f055-248">They will browse the **/StoreManager/Edit/id** URL (**id** being the unique id of the album to edit), thus making an HTTP-GET call to the server.</span></span>

<span data-ttu-id="6f055-249">控制器的 [編輯] 動作方法會從資料庫抓取適當的專輯、建立**StoreManagerViewModel**物件加以封裝（連同演出者和內容的清單），然後將它傳遞至 View 範本，以將 HTML 網頁轉譯回使用者。</span><span class="sxs-lookup"><span data-stu-id="6f055-249">The Controller Edit action method will retrieve the appropriate Album from the database, create a **StoreManagerViewModel** object to encapsulate it (along with a list of Artists and Genres), and then pass it off to a View template to render the HTML page back to the user.</span></span> <span data-ttu-id="6f055-250">此頁面將包含 **&lt;表單&gt;** 元素，以及用來編輯專輯屬性的文字方塊和下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="6f055-250">This page will contain a **&lt;form&gt;** element with textboxes and dropdowns for editing the Album properties.</span></span>

<span data-ttu-id="6f055-251">一旦使用者更新專輯表單值，然後按一下 [**儲存**] 按鈕，就會透過 HTTP POST 呼叫將變更提交回 **/StoreManager/Edit/id**。雖然 URL 與最後一個呼叫中的保持相同，但 ASP.NET MVC 會識別這次是 HTTP POST，因此會執行不同的編輯動作方法（一個以 **[HttpPost]** 裝飾的）。</span><span class="sxs-lookup"><span data-stu-id="6f055-251">Once the user updates the Album form values and clicks the **Save** button, the changes are submitted via an HTTP-POST call back to **/StoreManager/Edit/id**. Although the URL remains the same as in the last call, ASP.NET MVC identifies that this time it is an HTTP-POST and therefore executes a different Edit action method (one decorated with **[HttpPost]**).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Edit_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-edit-action-method"></a><span data-ttu-id="6f055-252">工作 1-執行 HTTP-取得編輯動作方法</span><span class="sxs-lookup"><span data-stu-id="6f055-252">Task 1 - Implementing the HTTP-GET Edit Action Method</span></span>

<span data-ttu-id="6f055-253">在這項工作中，您將會執行編輯動作方法的 HTTP GET 版本，以從資料庫中取出適當的專輯，以及所有的內容組和演出者清單。</span><span class="sxs-lookup"><span data-stu-id="6f055-253">In this task, you will implement the HTTP-GET version of the Edit action method to retrieve the appropriate Album from the database, as well as a list of all Genres and Artists.</span></span> <span data-ttu-id="6f055-254">它會將此資料封裝到最後一個步驟中所定義的**StoreManagerViewModel**物件，然後將其傳遞至視圖範本，以使用呈現回應。</span><span class="sxs-lookup"><span data-stu-id="6f055-254">It will package this data up into the **StoreManagerViewModel** object defined in the last step, which will then be passed to a View template to render the response with.</span></span>

1. <span data-ttu-id="6f055-255">開啟位於**來源/Ex3-CreatingTheEditView/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-255">Open the **Begin** solution located at **Source/Ex3-CreatingTheEditView/Begin/** folder.</span></span> <span data-ttu-id="6f055-256">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-256">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="6f055-257">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="6f055-257">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="6f055-258">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-258">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="6f055-259">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="6f055-259">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="6f055-260">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-260">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6f055-261">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="6f055-261">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="6f055-262">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f055-262">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="6f055-263">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6f055-263">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="6f055-264">開啟**StoreManagerController**類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-264">Open the **StoreManagerController** class.</span></span> <span data-ttu-id="6f055-265">若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-265">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="6f055-266">以下列程式碼取代**HTTP-GET 編輯**動作方法，以取出適當的**專輯**以及**內容和** **演出者**清單。</span><span class="sxs-lookup"><span data-stu-id="6f055-266">Replace the **HTTP-GET Edit** action method with the following code to retrieve the appropriate **Album** as well as the **Genres** and **Artists** lists.</span></span>

    <span data-ttu-id="6f055-267">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex3 STOREMANAGERCONTROLLER HTTP-取得編輯動作*）</span><span class="sxs-lookup"><span data-stu-id="6f055-267">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-GET Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample9.cs)]

    > [!NOTE]
    > <span data-ttu-id="6f055-268">您使用的是演出者和內容的**System.web** **SelectList** ，而不是**system.object**清單。</span><span class="sxs-lookup"><span data-stu-id="6f055-268">You are using **System.Web.Mvc** **SelectList** for Artists and Genres instead of the **System.Collections.Generic** List.</span></span>
    > 
    > <span data-ttu-id="6f055-269">**SelectList**是可讓您更清楚的方式來填入 HTML 下拉式清單，以及管理目前選取專案等專案。</span><span class="sxs-lookup"><span data-stu-id="6f055-269">**SelectList** is a cleaner way to populate HTML dropdowns and manage things like current selection.</span></span> <span data-ttu-id="6f055-270">在控制器動作中具現化並設定這些 ViewModel 物件，將會使編輯表單案例更整潔。</span><span class="sxs-lookup"><span data-stu-id="6f055-270">Instantiating and later setting up these ViewModel objects in the controller action will make the Edit form scenario cleaner.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Creating_the_Edit_View"></a>
#### <a name="task-2---creating-the-edit-view"></a><span data-ttu-id="6f055-271">工作 2-建立編輯檢視</span><span class="sxs-lookup"><span data-stu-id="6f055-271">Task 2 - Creating the Edit View</span></span>

<span data-ttu-id="6f055-272">在這項工作中，您將建立編輯檢視範本，稍後會顯示專輯屬性。</span><span class="sxs-lookup"><span data-stu-id="6f055-272">In this task, you will create an Edit View template that will later display the album properties.</span></span>

1. <span data-ttu-id="6f055-273">建立編輯檢視。</span><span class="sxs-lookup"><span data-stu-id="6f055-273">Create the Edit View.</span></span> <span data-ttu-id="6f055-274">若要這樣做，請以滑鼠右鍵按一下 [**編輯**動作] 方法內部，然後選取 [**新增視圖**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-274">To do this, right-click inside the **Edit** action method and select **Add View**.</span></span>
2. <span data-ttu-id="6f055-275">在 [加入視圖] 對話方塊中，確認視圖名稱為 [**編輯**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-275">In the Add View dialog, verify that the View Name is **Edit**.</span></span> <span data-ttu-id="6f055-276">核取 [**建立強型別視圖**] 核取方塊，然後從 [**視圖] 資料類別**下拉式方塊中選取 [**專輯（MvcMusicStore）** ]。</span><span class="sxs-lookup"><span data-stu-id="6f055-276">Check the **Create a strongly-typed view** checkbox and select **Album (MvcMusicStore.Models)** from the **View data class** drop-down.</span></span> <span data-ttu-id="6f055-277">從 [ **Scaffold 範本**] 下拉式選單選取 [**編輯**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-277">Select **Edit** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="6f055-278">將其他欄位保留為預設值，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-278">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="6f055-279">![新增編輯檢視](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "新增編輯檢視")</span><span class="sxs-lookup"><span data-stu-id="6f055-279">![Adding an Edit view](aspnet-mvc-4-helpers-forms-and-validation/_static/image7.png "Adding an Edit view")</span></span>

    <span data-ttu-id="6f055-280">*新增編輯檢視*</span><span class="sxs-lookup"><span data-stu-id="6f055-280">*Adding an Edit view*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="6f055-281">工作 3-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-281">Task 3 - Running the Application</span></span>

<span data-ttu-id="6f055-282">在這項工作中，您會測試 [ **StoreManager** **編輯**視圖] 頁面是否會針對當做參數傳遞的專輯顯示內容的值。</span><span class="sxs-lookup"><span data-stu-id="6f055-282">In this task, you will test that the **StoreManager** **Edit** View page displays the properties' values for the album passed as parameter.</span></span>

1. <span data-ttu-id="6f055-283">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-283">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-284">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-284">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-285">將 URL 變更為 [ **/StoreManager/Edit/1** ]，確認已顯示所傳遞專輯的屬性值。</span><span class="sxs-lookup"><span data-stu-id="6f055-285">Change the URL to **/StoreManager/Edit/1** to verify that the properties' values for the album passed are displayed.</span></span>

    <span data-ttu-id="6f055-286">![流覽專輯的編輯檢視](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "流覽專輯的編輯檢視")</span><span class="sxs-lookup"><span data-stu-id="6f055-286">![Browsing Album's Edit View](aspnet-mvc-4-helpers-forms-and-validation/_static/image8.png "Browsing Album's Edit View")</span></span>

    <span data-ttu-id="6f055-287">*流覽專輯的編輯檢視*</span><span class="sxs-lookup"><span data-stu-id="6f055-287">*Browsing Album's Edit view*</span></span>

<a id="Ex3Task4"></a>

<a id="Task_4_-_Implementing_drop-downs_on_the_Album_Editor_Template"></a>
#### <a name="task-4---implementing-drop-downs-on-the-album-editor-template"></a><span data-ttu-id="6f055-288">工作 4-在專輯編輯器範本上執行下拉式清單</span><span class="sxs-lookup"><span data-stu-id="6f055-288">Task 4 - Implementing drop-downs on the Album Editor Template</span></span>

<span data-ttu-id="6f055-289">在這項工作中，您會將下拉式清單新增至在上一個工作中建立的 View 範本，讓使用者可以從一份演出者和內容類型的清單中進行選取。</span><span class="sxs-lookup"><span data-stu-id="6f055-289">In this task, you will add drop-downs to the View template created in the last task, so that the user can select from a list of Artists and Genres.</span></span>

1. <span data-ttu-id="6f055-290">以下列內容取代所有**專輯**欄位集程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f055-290">Replace all the **Album** fieldset code with the following:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample10.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="6f055-291">已新增**DropDownList** helper 來呈現選擇演出者和內容內容的下拉式清單。</span><span class="sxs-lookup"><span data-stu-id="6f055-291">An **Html.DropDownList** helper has been added to render drop-downs for choosing Artists and Genres.</span></span> <span data-ttu-id="6f055-292">傳遞至**DropDownList**的參數為：</span><span class="sxs-lookup"><span data-stu-id="6f055-292">The parameters passed to **Html.DropDownList** are:</span></span>
    > 
    > 1. <span data-ttu-id="6f055-293">表單欄位名稱（ **&quot;ArtistId&quot;** ）。</span><span class="sxs-lookup"><span data-stu-id="6f055-293">The name of the form field (**&quot;ArtistId&quot;**).</span></span>
    > 2. <span data-ttu-id="6f055-294">下拉式的值**SelectList** 。</span><span class="sxs-lookup"><span data-stu-id="6f055-294">The **SelectList** of values for the drop-down.</span></span>

<a id="Ex3Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="6f055-295">工作 5-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-295">Task 5 - Running the Application</span></span>

<span data-ttu-id="6f055-296">在這項工作中，您會測試 [ **StoreManager** **編輯**視圖] 頁面是否顯示下拉式清單，而不是 [演出者] 和 [內容類型識別碼] 文字欄位。</span><span class="sxs-lookup"><span data-stu-id="6f055-296">In this task, you will test that the **StoreManager** **Edit** View page displays drop-downs instead of Artist and Genre ID text fields.</span></span>

1. <span data-ttu-id="6f055-297">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-297">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-298">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-298">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-299">將 URL 變更為 **/StoreManager/Edit/1** ，以確認它會顯示下拉式清單，而不是 [演出者] 和 [內容類型識別碼] 文字欄位。</span><span class="sxs-lookup"><span data-stu-id="6f055-299">Change the URL to **/StoreManager/Edit/1** to verify that it displays drop-downs instead of Artist and Genre ID text fields.</span></span>

    <span data-ttu-id="6f055-300">![使用下拉式清單流覽專輯的編輯檢視](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "使用下拉式清單流覽專輯的編輯檢視")</span><span class="sxs-lookup"><span data-stu-id="6f055-300">![Browsing Album's Edit View with drop downs](aspnet-mvc-4-helpers-forms-and-validation/_static/image9.png "Browsing Album's Edit View with drop downs")</span></span>

    <span data-ttu-id="6f055-301">*流覽專輯的編輯檢視，這次使用下拉式清單*</span><span class="sxs-lookup"><span data-stu-id="6f055-301">*Browsing Album's Edit view, this time with dropdowns*</span></span>

<a id="Ex3Task6"></a>

<a id="Task_6_-_Implementing_the_HTTP-POST_Edit_action_method"></a>
#### <a name="task-6---implementing-the-http-post-edit-action-method"></a><span data-ttu-id="6f055-302">工作 6-執行 HTTP POST 編輯動作方法</span><span class="sxs-lookup"><span data-stu-id="6f055-302">Task 6 - Implementing the HTTP-POST Edit action method</span></span>

<span data-ttu-id="6f055-303">現在，編輯檢視會如預期般顯示，您必須執行 HTTP POST 編輯動作方法，以儲存對專輯所做的變更。</span><span class="sxs-lookup"><span data-stu-id="6f055-303">Now that the Edit View displays as expected, you need to implement the HTTP-POST Edit Action method to save the changes made to the Album.</span></span>

1. <span data-ttu-id="6f055-304">如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6f055-304">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="6f055-305">從 [**控制器**] 資料夾開啟**StoreManagerController** 。</span><span class="sxs-lookup"><span data-stu-id="6f055-305">Open **StoreManagerController** from the **Controllers** folder.</span></span>
2. <span data-ttu-id="6f055-306">將**HTTP POST 編輯**動作方法程式碼取代為下列內容（請注意，必須取代的方法是接收兩個參數的多載版本）：</span><span class="sxs-lookup"><span data-stu-id="6f055-306">Replace **HTTP-POST Edit** action method code with the following (note that the method that must be replaced is overloaded version that receives two parameters):</span></span>

    <span data-ttu-id="6f055-307">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex3 STOREMANAGERCONTROLLER HTTP-POST 編輯動作*）</span><span class="sxs-lookup"><span data-stu-id="6f055-307">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex3 StoreManagerController HTTP-POST Edit action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample11.cs)]

    > [!NOTE]
    > <span data-ttu-id="6f055-308">當使用者按一下視圖的 [**儲存**] 按鈕，並對伺服器執行表單值的 HTTP POST，將其保存在資料庫中時，就會執行此方法。</span><span class="sxs-lookup"><span data-stu-id="6f055-308">This method will be executed when the user clicks the **Save** button of the View and performs an HTTP-POST of the form values back to the server to persist them in the database.</span></span> <span data-ttu-id="6f055-309">裝飾專案 **[HttpPost]** 表示此方法應該用於這些 HTTP POST 案例。</span><span class="sxs-lookup"><span data-stu-id="6f055-309">The decorator **[HttpPost]** indicates that the method should be used for those HTTP-POST scenarios.</span></span> <span data-ttu-id="6f055-310">方法會採用**專輯**物件。</span><span class="sxs-lookup"><span data-stu-id="6f055-310">The method takes an **Album** object.</span></span> <span data-ttu-id="6f055-311">ASP.NET MVC 會從張貼的 &lt;表單&gt; 值，自動建立專輯物件。</span><span class="sxs-lookup"><span data-stu-id="6f055-311">ASP.NET MVC will automatically create the Album object from the posted &lt;form&gt; values.</span></span>
    > 
    > <span data-ttu-id="6f055-312">方法會執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="6f055-312">The method will perform these steps:</span></span>
    > 
    > 1. <span data-ttu-id="6f055-313">如果模型有效：</span><span class="sxs-lookup"><span data-stu-id="6f055-313">If model is valid:</span></span>
    > 
    >     1. <span data-ttu-id="6f055-314">更新內容中的專輯專案，將其標示為已修改的物件。</span><span class="sxs-lookup"><span data-stu-id="6f055-314">Update the album entry in the context to mark it as a modified object.</span></span>
    >     2. <span data-ttu-id="6f055-315">儲存變更並重新導向至索引視圖。</span><span class="sxs-lookup"><span data-stu-id="6f055-315">Save the changes and redirect to the index view.</span></span>
    > 2. <span data-ttu-id="6f055-316">如果模型無效，它會在 ViewBag 中填入**GenreId**和**ArtistId**，然後它會傳回具有所接收專輯物件的視圖，以允許使用者執行任何必要的更新。</span><span class="sxs-lookup"><span data-stu-id="6f055-316">If the model is not valid, it will populate the ViewBag with the **GenreId** and **ArtistId**, then it will return the view with the received Album object to allow the user perform any required update.</span></span>

<a id="Ex3Task7"></a>

<a id="Task_7_-_Running_the_Application"></a>
#### <a name="task-7---running-the-application"></a><span data-ttu-id="6f055-317">工作 7-執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-317">Task 7 - Running the Application</span></span>

<span data-ttu-id="6f055-318">在這項工作中，您會測試 [ **StoreManager 編輯**視圖] 頁面是否會實際將更新的專輯資料儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="6f055-318">In this task, you will test that the **StoreManager Edit** View page actually saves the updated Album data in the database.</span></span>

1. <span data-ttu-id="6f055-319">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-319">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-320">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-320">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-321">將 URL 變更為 **/StoreManager/Edit/1**。</span><span class="sxs-lookup"><span data-stu-id="6f055-321">Change the URL to **/StoreManager/Edit/1**.</span></span> <span data-ttu-id="6f055-322">將 [專輯] 標題變更為 [已**載入**]，然後按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-322">Change the Album title to **Load** and click on **Save**.</span></span> <span data-ttu-id="6f055-323">確認專輯清單中的專輯標題確實已變更。</span><span class="sxs-lookup"><span data-stu-id="6f055-323">Verify that album's title actually changed in the list of albums.</span></span>

    <span data-ttu-id="6f055-324">![更新專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "更新專輯")</span><span class="sxs-lookup"><span data-stu-id="6f055-324">![Updating an album](aspnet-mvc-4-helpers-forms-and-validation/_static/image10.png "Updating an album")</span></span>

    <span data-ttu-id="6f055-325">*更新專輯*</span><span class="sxs-lookup"><span data-stu-id="6f055-325">*Updating an Album*</span></span>

<a id="Exercise4"></a>

<a id="Exercise_4_Adding_a_Create_View"></a>
### <a name="exercise-4-adding-a-create-view"></a><span data-ttu-id="6f055-326">練習4：新增建立視圖</span><span class="sxs-lookup"><span data-stu-id="6f055-326">Exercise 4: Adding a Create View</span></span>

<span data-ttu-id="6f055-327">既然**StoreManagerController**支援**編輯**功能，在這個練習中，您將學習如何新增建立視圖範本，讓商店經理將新專輯加入應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-327">Now that the **StoreManagerController** supports the **Edit** ability, in this exercise you will learn how to add a Create View template to let store managers add new Albums to the application.</span></span>

<span data-ttu-id="6f055-328">就像您對編輯功能所做的一樣，您將使用**StoreManagerController**類別內的兩個不同方法來執行建立案例：</span><span class="sxs-lookup"><span data-stu-id="6f055-328">Like you did with the Edit functionality, you will implement the Create scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="6f055-329">當商店經理第一次造訪 **/StoreManager/Create** URL 時，其中一個動作方法會顯示空白表單。</span><span class="sxs-lookup"><span data-stu-id="6f055-329">One action method will display an empty form when store managers first visit the **/StoreManager/Create** URL.</span></span>
2. <span data-ttu-id="6f055-330">第二個動作方法會處理案例，其中 store manager 會在表單中按一下 [**儲存**] 按鈕，並將值以 HTTP POST 形式提交回 **/StoreManager/Create** URL。</span><span class="sxs-lookup"><span data-stu-id="6f055-330">A second action method will handle the scenario where the store manager clicks the **Save** button within the form and submits the values back to the **/StoreManager/Create** URL as an HTTP-POST.</span></span>

<a id="Ex4Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Create_action_method"></a>
#### <a name="task-1---implementing-the-http-get-create-action-method"></a><span data-ttu-id="6f055-331">工作 1-執行 HTTP-GET 建立動作方法</span><span class="sxs-lookup"><span data-stu-id="6f055-331">Task 1 - Implementing the HTTP-GET Create action method</span></span>

<span data-ttu-id="6f055-332">在這項工作中，您將會執行 Create action 方法的 HTTP GET 版本來抓取所有內容清單和演出者的清單、將此資料封裝到**StoreManagerViewModel**物件中，然後再傳遞至視圖範本。</span><span class="sxs-lookup"><span data-stu-id="6f055-332">In this task, you will implement the HTTP-GET version of the Create action method to retrieve a list of all Genres and Artists, package this data up into a **StoreManagerViewModel** object, which will then be passed to a View template.</span></span>

1. <span data-ttu-id="6f055-333">開啟位於**來源/Ex4-AddingACreateView/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-333">Open the **Begin** solution located at **Source/Ex4-AddingACreateView/Begin/** folder.</span></span> <span data-ttu-id="6f055-334">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-334">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="6f055-335">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="6f055-335">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="6f055-336">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-336">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="6f055-337">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="6f055-337">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="6f055-338">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-338">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6f055-339">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="6f055-339">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="6f055-340">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f055-340">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="6f055-341">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6f055-341">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="6f055-342">開啟**StoreManagerController**類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-342">Open **StoreManagerController** class.</span></span> <span data-ttu-id="6f055-343">若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-343">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="6f055-344">將**Create** action 方法程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="6f055-344">Replace the **Create** action method code with the following:</span></span>

    <span data-ttu-id="6f055-345">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex4 STOREMANAGERCONTROLLER HTTP-取得建立動作*）</span><span class="sxs-lookup"><span data-stu-id="6f055-345">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP-GET Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample12.cs)]

<a id="Ex4Task2"></a>

<a id="Task_2_-_Adding_the_Create_View"></a>
#### <a name="task-2---adding-the-create-view"></a><span data-ttu-id="6f055-346">工作 2-新增建立視圖</span><span class="sxs-lookup"><span data-stu-id="6f055-346">Task 2 - Adding the Create View</span></span>

<span data-ttu-id="6f055-347">在這項工作中，您將新增建立視圖範本，以顯示新的（空白）專輯表單。</span><span class="sxs-lookup"><span data-stu-id="6f055-347">In this task, you will add the Create View template that will display a new (empty) Album form.</span></span>

1. <span data-ttu-id="6f055-348">以滑鼠右鍵按一下 [**建立**動作] 方法內部，然後選取 [**新增視圖**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-348">Right-click inside the **Create** action method and select **Add View**.</span></span> <span data-ttu-id="6f055-349">這會顯示 [加入視圖] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6f055-349">This will bring up the Add View dialog.</span></span>
2. <span data-ttu-id="6f055-350">在 [加入視圖] 對話方塊中，確認視圖名稱為 [**建立**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-350">In the Add View dialog, verify that the View Name is **Create**.</span></span> <span data-ttu-id="6f055-351">選取 [**建立強型別視圖**] 選項，然後從 [**模型類別**] 下拉式選單中選取 [**專輯（MvcMusicStore）** ]，然後從 [ **Scaffold 範本**] 下拉式視窗中**建立**。</span><span class="sxs-lookup"><span data-stu-id="6f055-351">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down and **Create** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="6f055-352">將其他欄位保留為預設值，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-352">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="6f055-353">![新增建立視圖](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view .png")</span><span class="sxs-lookup"><span data-stu-id="6f055-353">![Adding a create view](aspnet-mvc-4-helpers-forms-and-validation/_static/image11.png "adding-a-create-view.png")</span></span>

    <span data-ttu-id="6f055-354">*新增 Create View*</span><span class="sxs-lookup"><span data-stu-id="6f055-354">*Adding the Create View*</span></span>
3. <span data-ttu-id="6f055-355">將 [ **GenreId** ] 和 [ **ArtistId** ] 欄位更新為使用下拉式清單，如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f055-355">Update the **GenreId** and **ArtistId** fields to use a drop-down list as shown below:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample13.cshtml)]

<a id="Ex4Task3"></a>

<a id="Task_3_-_Running_the_Application"></a>
#### <a name="task-3---running-the-application"></a><span data-ttu-id="6f055-356">工作 3-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-356">Task 3 - Running the Application</span></span>

<span data-ttu-id="6f055-357">在這項工作中，您會測試 [ **StoreManager** **建立**視圖] 頁面是否顯示空的專輯表單。</span><span class="sxs-lookup"><span data-stu-id="6f055-357">In this task, you will test that the **StoreManager** **Create** View page displays an empty Album form.</span></span>

1. <span data-ttu-id="6f055-358">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-358">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-359">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-359">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-360">將 URL 變更為 **/StoreManager/Create**。</span><span class="sxs-lookup"><span data-stu-id="6f055-360">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="6f055-361">確認顯示空白表單以填滿新的專輯屬性。</span><span class="sxs-lookup"><span data-stu-id="6f055-361">Verify that an empty form is displayed for filling the new Album properties.</span></span>

    <span data-ttu-id="6f055-362">![建立具有空白表單的 View](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "建立具有空白表單的 View")</span><span class="sxs-lookup"><span data-stu-id="6f055-362">![Create View with an empty form](aspnet-mvc-4-helpers-forms-and-validation/_static/image12.png "Create View with an empty form")</span></span>

    <span data-ttu-id="6f055-363">*建立具有空白表單的 View*</span><span class="sxs-lookup"><span data-stu-id="6f055-363">*Create View with an empty form*</span></span>

<a id="Ex4Task4"></a>

<a id="Task_4_-_Implementing_the_HTTP-POST_Create_Action_Method"></a>
#### <a name="task-4---implementing-the-http-post-create-action-method"></a><span data-ttu-id="6f055-364">工作 4-執行 HTTP POST 建立動作方法</span><span class="sxs-lookup"><span data-stu-id="6f055-364">Task 4 - Implementing the HTTP-POST Create Action Method</span></span>

<span data-ttu-id="6f055-365">在這項工作中，您將會執行建立動作方法的 HTTP POST 版本，當使用者按一下 [**儲存**] 按鈕時將會叫用。</span><span class="sxs-lookup"><span data-stu-id="6f055-365">In this task, you will implement the HTTP-POST version of the Create action method that will be invoked when a user clicks the **Save** button.</span></span> <span data-ttu-id="6f055-366">方法應該將新的專輯儲存在資料庫中。</span><span class="sxs-lookup"><span data-stu-id="6f055-366">The method should save the new album in the database.</span></span>

1. <span data-ttu-id="6f055-367">如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6f055-367">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="6f055-368">開啟**StoreManagerController**類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-368">Open **StoreManagerController** class.</span></span> <span data-ttu-id="6f055-369">若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-369">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="6f055-370">將**HTTP POST 建立**動作方法程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="6f055-370">Replace **HTTP-POST Create** action method code with the following:</span></span>

    <span data-ttu-id="6f055-371">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex4 STOREMANAGERCONTROLLER HTTP-POST 建立動作*）</span><span class="sxs-lookup"><span data-stu-id="6f055-371">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex4 StoreManagerController HTTP- POST Create action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="6f055-372">[建立] 動作與先前的 [編輯動作] 方法非常類似，但它不會將物件設定為已修改，而是加入至內容。</span><span class="sxs-lookup"><span data-stu-id="6f055-372">The Create action is pretty similar to the previous Edit action method but instead of setting the object as modified, it is being added to the context.</span></span>

<a id="Ex4Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="6f055-373">工作 5-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-373">Task 5 - Running the Application</span></span>

<span data-ttu-id="6f055-374">在這項工作中，您將測試**StoreManager**的 [建立視圖] 頁面可讓您建立新的專輯，然後重新導向至 StoreManager 索引視圖。</span><span class="sxs-lookup"><span data-stu-id="6f055-374">In this task, you will test that the **StoreManager Create** View page lets you create a new Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="6f055-375">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-375">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-376">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-376">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-377">將 URL 變更為 **/StoreManager/Create**。</span><span class="sxs-lookup"><span data-stu-id="6f055-377">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="6f055-378">以新專輯的資料填滿所有表單欄位，如下圖所示：</span><span class="sxs-lookup"><span data-stu-id="6f055-378">Fill all the form fields with data for a new Album, like the one in the following figure:</span></span>

    <span data-ttu-id="6f055-379">![建立專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "建立專輯")</span><span class="sxs-lookup"><span data-stu-id="6f055-379">![Creating an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image13.png "Creating an Album")</span></span>

    <span data-ttu-id="6f055-380">*建立專輯*</span><span class="sxs-lookup"><span data-stu-id="6f055-380">*Creating an Album*</span></span>
3. <span data-ttu-id="6f055-381">確認您已重新導向至 StoreManager 索引視圖，其中包含剛建立的新專輯。</span><span class="sxs-lookup"><span data-stu-id="6f055-381">Verify that you get redirected to the StoreManager Index View that includes the new Album just created.</span></span>

    <span data-ttu-id="6f055-382">![已建立新的專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "已建立新的專輯")</span><span class="sxs-lookup"><span data-stu-id="6f055-382">![New Album Created](aspnet-mvc-4-helpers-forms-and-validation/_static/image14.png "New Album Created")</span></span>

    <span data-ttu-id="6f055-383">*已建立新的專輯*</span><span class="sxs-lookup"><span data-stu-id="6f055-383">*New Album Created*</span></span>

<a id="Exercise5"></a>

<a id="Exercise_5_Handling_Deletion"></a>
### <a name="exercise-5-handling-deletion"></a><span data-ttu-id="6f055-384">練習5：處理刪除</span><span class="sxs-lookup"><span data-stu-id="6f055-384">Exercise 5: Handling Deletion</span></span>

<span data-ttu-id="6f055-385">尚未實行刪除專輯的功能。</span><span class="sxs-lookup"><span data-stu-id="6f055-385">The ability to delete albums is not yet implemented.</span></span> <span data-ttu-id="6f055-386">這就是本練習的相關內容。</span><span class="sxs-lookup"><span data-stu-id="6f055-386">This is what this exercise will be about.</span></span> <span data-ttu-id="6f055-387">就像之前一樣，您將使用**StoreManagerController**類別內的兩個不同方法來執行刪除案例：</span><span class="sxs-lookup"><span data-stu-id="6f055-387">Like before, you will implement the Delete scenario using two separate methods within the **StoreManagerController** class:</span></span>

1. <span data-ttu-id="6f055-388">一個動作方法會顯示確認表單</span><span class="sxs-lookup"><span data-stu-id="6f055-388">One action method will display a confirmation form</span></span>
2. <span data-ttu-id="6f055-389">第二個動作方法會處理表單提交</span><span class="sxs-lookup"><span data-stu-id="6f055-389">A second action method will handle the form submission</span></span>

<a id="Ex5Task1"></a>

<a id="Task_1_-_Implementing_the_HTTP-GET_Delete_Action_Method"></a>
#### <a name="task-1---implementing-the-http-get-delete-action-method"></a><span data-ttu-id="6f055-390">工作 1-執行 HTTP-GET Delete 動作方法</span><span class="sxs-lookup"><span data-stu-id="6f055-390">Task 1 - Implementing the HTTP-GET Delete Action Method</span></span>

<span data-ttu-id="6f055-391">在這項工作中，您將會執行 Delete 動作方法的 HTTP GET 版本來抓取專輯的資訊。</span><span class="sxs-lookup"><span data-stu-id="6f055-391">In this task, you will implement the HTTP-GET version of the Delete action method to retrieve the album's information.</span></span>

1. <span data-ttu-id="6f055-392">開啟位於**來源/Ex5-HandlingDeletion/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-392">Open the **Begin** solution located at **Source/Ex5-HandlingDeletion/Begin/** folder.</span></span> <span data-ttu-id="6f055-393">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-393">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="6f055-394">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="6f055-394">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="6f055-395">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-395">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="6f055-396">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="6f055-396">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="6f055-397">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-397">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6f055-398">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="6f055-398">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="6f055-399">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f055-399">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="6f055-400">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6f055-400">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="6f055-401">開啟**StoreManagerController**類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-401">Open **StoreManagerController** class.</span></span> <span data-ttu-id="6f055-402">若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-402">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
3. <span data-ttu-id="6f055-403">「刪除控制器」動作與先前的「存放區詳細資料控制器」動作完全相同：它會使用 URL 中提供的**識別碼**從資料庫查詢**專輯**物件，並傳回適當的**視圖**。</span><span class="sxs-lookup"><span data-stu-id="6f055-403">The Delete controller action is exactly the same as the previous Store Details controller action: it queries the **album** object from the database using the **id** provided in the URL and returns the appropriate **View**.</span></span> <span data-ttu-id="6f055-404">若要這麼做，請將 HTTP-GET **Delete**動作方法程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="6f055-404">To do this, replace the HTTP-GET **Delete** action method code with the following:</span></span>

    <span data-ttu-id="6f055-405">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證 Ex5 處理刪除 HTTP-取得刪除動作*）</span><span class="sxs-lookup"><span data-stu-id="6f055-405">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-GET Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample15.cs)]
4. <span data-ttu-id="6f055-406">在**Delete**動作方法內按一下滑鼠右鍵，然後選取 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-406">Right-click inside the **Delete** action method and select **Add View**.</span></span> <span data-ttu-id="6f055-407">這會顯示 [加入視圖] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="6f055-407">This will bring up the Add View dialog.</span></span>
5. <span data-ttu-id="6f055-408">在 [加入視圖] 對話方塊中，確認視圖名稱為 [**刪除**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-408">In the Add View dialog, verify that the View name is **Delete**.</span></span> <span data-ttu-id="6f055-409">選取 [**建立強型別視圖**] 選項，然後從 [**模型類別**] 下拉式選單選取 [**專輯] （MvcMusicStore）** 。</span><span class="sxs-lookup"><span data-stu-id="6f055-409">Select the **Create a strongly-typed view** option and select **Album (MvcMusicStore.Models)** from the **Model class** drop-down.</span></span> <span data-ttu-id="6f055-410">從 [ **Scaffold 範本**] 下拉式選單中選取 [**刪除**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-410">Select **Delete** from the **Scaffold template** drop-down.</span></span> <span data-ttu-id="6f055-411">將其他欄位保留為預設值，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-411">Leave the other fields with their default value and then click **Add**.</span></span>

    <span data-ttu-id="6f055-412">![加入刪除視圖](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "加入刪除視圖")</span><span class="sxs-lookup"><span data-stu-id="6f055-412">![Adding a Delete View](aspnet-mvc-4-helpers-forms-and-validation/_static/image15.png "Adding a Delete View")</span></span>

    <span data-ttu-id="6f055-413">*加入刪除視圖*</span><span class="sxs-lookup"><span data-stu-id="6f055-413">*Adding a Delete View*</span></span>
6. <span data-ttu-id="6f055-414">[刪除] 範本會顯示模型中的所有欄位。</span><span class="sxs-lookup"><span data-stu-id="6f055-414">The Delete template shows all the fields from the model.</span></span> <span data-ttu-id="6f055-415">您只會顯示專輯的標題。</span><span class="sxs-lookup"><span data-stu-id="6f055-415">You will show only the album's title.</span></span> <span data-ttu-id="6f055-416">若要這麼做，請使用下列程式碼取代此視圖的內容：</span><span class="sxs-lookup"><span data-stu-id="6f055-416">To do this, replace the content of the view with the following code:</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample16.cshtml)]

<a id="Ex05Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="6f055-417">工作 2-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-417">Task 2 - Running the Application</span></span>

<span data-ttu-id="6f055-418">在這項工作中，您將測試**StoreManager** **刪除**視圖頁面是否顯示確認刪除表單。</span><span class="sxs-lookup"><span data-stu-id="6f055-418">In this task, you will test that the **StoreManager** **Delete** View page displays a confirmation deletion form.</span></span>

1. <span data-ttu-id="6f055-419">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-419">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-420">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-420">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-421">將 URL 變更為 **/StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="6f055-421">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="6f055-422">按一下 [**刪除**]，然後確認已上傳新的視圖，以選取要刪除的一個專輯。</span><span class="sxs-lookup"><span data-stu-id="6f055-422">Select one album to delete by clicking **Delete** and verify that the new view is uploaded.</span></span>

    <span data-ttu-id="6f055-423">![刪除專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "刪除專輯")</span><span class="sxs-lookup"><span data-stu-id="6f055-423">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image16.png "Deleting an Album")</span></span>

    <span data-ttu-id="6f055-424">*刪除專輯*</span><span class="sxs-lookup"><span data-stu-id="6f055-424">*Deleting an Album*</span></span>

<a id="Ex05Task3"></a>

<a id="Task_3-_Implementing_the_HTTP-POST_Delete_Action_Method"></a>
#### <a name="task-3--implementing-the-http-post-delete-action-method"></a><span data-ttu-id="6f055-425">工作 3-執行 HTTP POST 刪除動作方法</span><span class="sxs-lookup"><span data-stu-id="6f055-425">Task 3- Implementing the HTTP-POST Delete Action Method</span></span>

<span data-ttu-id="6f055-426">在這項工作中，您將會執行刪除動作方法的 HTTP POST 版本，當使用者按一下 [**刪除**] 按鈕時將會叫用。</span><span class="sxs-lookup"><span data-stu-id="6f055-426">In this task, you will implement the HTTP-POST version of the Delete action method that will be invoked when a user clicks the **Delete** button.</span></span> <span data-ttu-id="6f055-427">方法應該刪除資料庫中的專輯。</span><span class="sxs-lookup"><span data-stu-id="6f055-427">The method should delete the album in the database.</span></span>

1. <span data-ttu-id="6f055-428">如有需要，請關閉瀏覽器，以返回 [Visual Studio] 視窗。</span><span class="sxs-lookup"><span data-stu-id="6f055-428">Close the browser if needed, to return to the Visual Studio window.</span></span> <span data-ttu-id="6f055-429">開啟**StoreManagerController**類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-429">Open **StoreManagerController** class.</span></span> <span data-ttu-id="6f055-430">若要這麼做，請展開 [**控制器**] 資料夾，然後按兩下 [ **StoreManagerController.cs**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-430">To do this, expand the **Controllers** folder and double-click **StoreManagerController.cs**.</span></span>
2. <span data-ttu-id="6f055-431">將**HTTP POST 刪除**動作方法程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="6f055-431">Replace **HTTP-POST Delete** action method code with the following:</span></span>

    <span data-ttu-id="6f055-432">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證 Ex5 處理刪除 HTTP-POST 刪除動作*）</span><span class="sxs-lookup"><span data-stu-id="6f055-432">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex5 Handling Deletion HTTP-POST Delete action*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample17.cs)]

<a id="Ex5Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="6f055-433">工作 4-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-433">Task 4 - Running the Application</span></span>

<span data-ttu-id="6f055-434">在這項工作中，您將測試**StoreManager 刪除**視圖頁面是否可讓您刪除專輯，然後重新導向至 StoreManager 索引視圖。</span><span class="sxs-lookup"><span data-stu-id="6f055-434">In this task, you will test that the **StoreManager Delete** View page lets you delete an Album and then redirects to the StoreManager Index View.</span></span>

1. <span data-ttu-id="6f055-435">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-435">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-436">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-436">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-437">將 URL 變更為 **/StoreManager**。</span><span class="sxs-lookup"><span data-stu-id="6f055-437">Change the URL to **/StoreManager**.</span></span> <span data-ttu-id="6f055-438">按一下 [刪除] 來選取要刪除的一個專輯 **。**</span><span class="sxs-lookup"><span data-stu-id="6f055-438">Select one album to delete by clicking **Delete.**</span></span> <span data-ttu-id="6f055-439">按一下 [**刪除**] 按鈕以確認刪除：</span><span class="sxs-lookup"><span data-stu-id="6f055-439">Confirm the deletion by clicking **Delete** button:</span></span>

    <span data-ttu-id="6f055-440">![刪除專輯](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "刪除專輯")</span><span class="sxs-lookup"><span data-stu-id="6f055-440">![Deleting an Album](aspnet-mvc-4-helpers-forms-and-validation/_static/image17.png "Deleting an Album")</span></span>

    <span data-ttu-id="6f055-441">*刪除專輯*</span><span class="sxs-lookup"><span data-stu-id="6f055-441">*Deleting an Album*</span></span>
3. <span data-ttu-id="6f055-442">確認專輯已刪除，因為它不會出現在 [**索引**] 頁面中。</span><span class="sxs-lookup"><span data-stu-id="6f055-442">Verify that the album was deleted since it does not appear in the **Index** page.</span></span>

<a id="Exercise6"></a>

<a id="Exercise_6_Adding_Validation"></a>
### <a name="exercise-6-adding-validation"></a><span data-ttu-id="6f055-443">練習6：加入驗證</span><span class="sxs-lookup"><span data-stu-id="6f055-443">Exercise 6: Adding Validation</span></span>

<span data-ttu-id="6f055-444">目前，您現有的建立和編輯表單不會執行任何類型的驗證。</span><span class="sxs-lookup"><span data-stu-id="6f055-444">Currently, the Create and Edit forms you have in place do not perform any kind of validation.</span></span> <span data-ttu-id="6f055-445">如果使用者將 [必要] 欄位保留空白，或在 [價格] 欄位中輸入字母，就會從資料庫中取得第一個錯誤。</span><span class="sxs-lookup"><span data-stu-id="6f055-445">If the user leaves a required field blank or type letters in the price field, the first error you will get will be from the database.</span></span>

<span data-ttu-id="6f055-446">您可以藉由將資料批註加入至模型類別，將驗證新增至應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-446">You can add validation to the application by adding Data Annotations to your model class.</span></span> <span data-ttu-id="6f055-447">資料批註允許描述您要套用至模型屬性的規則，而 ASP.NET MVC 會負責強制執行並向使用者顯示適當的訊息。</span><span class="sxs-lookup"><span data-stu-id="6f055-447">Data Annotations allow describing the rules you want applied to your model properties, and ASP.NET MVC will take care of enforcing and displaying appropriate message to users.</span></span>

<a id="Ex06Task1"></a>

<a id="Task_1_-_Adding_Data_Annotations"></a>
#### <a name="task-1---adding-data-annotations"></a><span data-ttu-id="6f055-448">工作 1-加入資料批註</span><span class="sxs-lookup"><span data-stu-id="6f055-448">Task 1 - Adding Data Annotations</span></span>

<span data-ttu-id="6f055-449">在這項工作中，您會將資料批註加入至專輯模型，讓 [建立和編輯] 頁面在適當時顯示驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="6f055-449">In this task, you will add Data Annotations to the Album Model that will make the Create and Edit page display validation messages when appropriate.</span></span>

<span data-ttu-id="6f055-450">對於簡單的模型類別而言，加入資料批註只是藉由新增**system.workflow.componentmodel.activity**的**using**語句來處理，然後在適當的屬性上放置 **[Required]** 屬性。</span><span class="sxs-lookup"><span data-stu-id="6f055-450">For a simple Model class, adding a Data Annotation is just handled by adding a **using** statement for **System.ComponentModel.DataAnnotation**, then placing a **[Required]** attribute on the appropriate properties.</span></span> <span data-ttu-id="6f055-451">下列範例會將**Name**屬性設為 View 中的必要欄位。</span><span class="sxs-lookup"><span data-stu-id="6f055-451">The following example would make the **Name** property a required field in the View.</span></span>

[!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample18.cs)]

<span data-ttu-id="6f055-452">這在產生實體資料模型的情況下，這種情況就會變得更複雜。</span><span class="sxs-lookup"><span data-stu-id="6f055-452">This is a little more complex in cases like this application where the Entity Data Model is generated.</span></span> <span data-ttu-id="6f055-453">如果您將資料批註直接加入至模型類別，如果您從資料庫更新模型，就會覆寫它們。</span><span class="sxs-lookup"><span data-stu-id="6f055-453">If you added Data Annotations directly to the model classes, they would be overwritten if you update the model from the database.</span></span> <span data-ttu-id="6f055-454">相反地，您可以使用中繼資料部分類別來保存注釋，並使用 **[MetadataType]** 屬性與模型類別產生關聯。</span><span class="sxs-lookup"><span data-stu-id="6f055-454">Instead, you can make use of metadata partial classes which will exist to hold the annotations and are associated with the model classes using the **[MetadataType]** attribute.</span></span>

1. <span data-ttu-id="6f055-455">開啟位於**來源/Ex6-AddingValidation/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-455">Open the **Begin** solution located at **Source/Ex6-AddingValidation/Begin/** folder.</span></span> <span data-ttu-id="6f055-456">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-456">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="6f055-457">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="6f055-457">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="6f055-458">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-458">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="6f055-459">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="6f055-459">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="6f055-460">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-460">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6f055-461">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="6f055-461">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="6f055-462">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f055-462">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="6f055-463">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6f055-463">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="6f055-464">從 [**模型**] 資料夾開啟**Album.cs** 。</span><span class="sxs-lookup"><span data-stu-id="6f055-464">Open the **Album.cs** from the **Models** folder.</span></span>
3. <span data-ttu-id="6f055-465">以反白顯示的程式碼取代**Album.cs**內容，使其看起來如下所示：</span><span class="sxs-lookup"><span data-stu-id="6f055-465">Replace **Album.cs** content with the highlighted code, so that it looks like the following:</span></span>

    > [!NOTE]
    > <span data-ttu-id="6f055-466">**[DisplayFormat （ConvertEmptyStringToNull = false）]** 這一行表示當資料欄位在資料來源中更新時，模型中的空字串將不會轉換成 null。</span><span class="sxs-lookup"><span data-stu-id="6f055-466">The line **[DisplayFormat(ConvertEmptyStringToNull=false)]** indicates that empty strings from the model won't be converted to null when the data field is updated in the data source.</span></span> <span data-ttu-id="6f055-467">當 Entity Framework 在資料批註驗證欄位之前，將 null 值指派給模型時，這種設定會避免發生例外狀況。</span><span class="sxs-lookup"><span data-stu-id="6f055-467">This setting will avoid an exception when the Entity Framework assigns null values to the model before Data Annotation validates the fields.</span></span>

    <span data-ttu-id="6f055-468">（程式碼片段- *ASP.NET MVC 4 協助程式和表單和驗證-Ex6 專輯中繼資料部分類別*）</span><span class="sxs-lookup"><span data-stu-id="6f055-468">(Code Snippet - *ASP.NET MVC 4 Helpers and Forms and Validation - Ex6 Album metadata partial class*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample19.cs)]

    > [!NOTE]
    > <span data-ttu-id="6f055-469">此**專輯**部分類別具有**MetadataType**屬性，指向資料批註的**AlbumMetaData**類別。</span><span class="sxs-lookup"><span data-stu-id="6f055-469">This **Album** partial class has a **MetadataType** attribute which points to the **AlbumMetaData** class for the Data Annotations.</span></span> <span data-ttu-id="6f055-470">以下是您用來標注專輯模型的一些資料批註屬性：</span><span class="sxs-lookup"><span data-stu-id="6f055-470">These are some of the Data Annotation attributes you are using to annotate the Album model:</span></span>
    > 
    > - <span data-ttu-id="6f055-471">必要-指出屬性是必要欄位</span><span class="sxs-lookup"><span data-stu-id="6f055-471">Required - Indicates that the property is a required field</span></span>
    > - <span data-ttu-id="6f055-472">DisplayName-定義要在表單欄位和驗證訊息上使用的文字</span><span class="sxs-lookup"><span data-stu-id="6f055-472">DisplayName - Defines the text to be used on form fields and validation messages</span></span>
    > - <span data-ttu-id="6f055-473">DisplayFormat-指定顯示和格式化資料欄位的方式。</span><span class="sxs-lookup"><span data-stu-id="6f055-473">DisplayFormat - Specifies how data fields are displayed and formatted.</span></span>
    > - <span data-ttu-id="6f055-474">StringLength-定義字串欄位的最大長度</span><span class="sxs-lookup"><span data-stu-id="6f055-474">StringLength - Defines a maximum length for a string field</span></span>
    > - <span data-ttu-id="6f055-475">範圍-提供數值欄位的最大和最小值</span><span class="sxs-lookup"><span data-stu-id="6f055-475">Range - Gives a maximum and minimum value for a numeric field</span></span>
    > - <span data-ttu-id="6f055-476">ScaffoldColumn-允許隱藏編輯表單中的欄位</span><span class="sxs-lookup"><span data-stu-id="6f055-476">ScaffoldColumn - Allows hiding fields from editor forms</span></span>

<a id="Ex06Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="6f055-477">工作 2-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-477">Task 2 - Running the Application</span></span>

<span data-ttu-id="6f055-478">在這項工作中，您將使用上一個工作中所選擇的顯示名稱，測試 [建立] 和 [編輯] 頁面是否會驗證欄位。</span><span class="sxs-lookup"><span data-stu-id="6f055-478">In this task, you will test that the Create and Edit pages validate fields, using the display names chosen in the last task.</span></span>

1. <span data-ttu-id="6f055-479">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-479">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="6f055-480">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-480">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-481">將 URL 變更為 **/StoreManager/Create**。</span><span class="sxs-lookup"><span data-stu-id="6f055-481">Change the URL to **/StoreManager/Create**.</span></span> <span data-ttu-id="6f055-482">確認顯示名稱符合部分類別中的名稱（例如**專輯封面 URL** ，而不是**AlbumArtUrl**）</span><span class="sxs-lookup"><span data-stu-id="6f055-482">Verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**)</span></span>
3. <span data-ttu-id="6f055-483">按一下 [**建立**]，而不填滿表單。</span><span class="sxs-lookup"><span data-stu-id="6f055-483">Click **Create**, without filling the form.</span></span> <span data-ttu-id="6f055-484">確認您取得對應的驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="6f055-484">Verify that you get the corresponding validation messages.</span></span>

    <span data-ttu-id="6f055-485">![[建立] 頁面中的已驗證欄位](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "[建立] 頁面中的已驗證欄位")</span><span class="sxs-lookup"><span data-stu-id="6f055-485">![Validated fields in the Create page](aspnet-mvc-4-helpers-forms-and-validation/_static/image18.png "Validated fields in the Create page")</span></span>

    <span data-ttu-id="6f055-486">*[建立] 頁面中的已驗證欄位*</span><span class="sxs-lookup"><span data-stu-id="6f055-486">*Validated fields in the Create page*</span></span>
4. <span data-ttu-id="6f055-487">您可以使用 [**編輯**] 頁面確認相同的情況。</span><span class="sxs-lookup"><span data-stu-id="6f055-487">You can verify that the same occurs with the **Edit** page.</span></span> <span data-ttu-id="6f055-488">將 URL 變更為 **/StoreManager/Edit/1** ，並確認顯示名稱符合部分類別（例如**專輯封面 URL** ，而不是**AlbumArtUrl**）中的名稱。</span><span class="sxs-lookup"><span data-stu-id="6f055-488">Change the URL to **/StoreManager/Edit/1** and verify that the display names match the ones in the partial class (like **Album Art URL** instead of **AlbumArtUrl**).</span></span> <span data-ttu-id="6f055-489">清空 [**標題**] 和 [**價格**] 欄位，然後按一下 [**儲存**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-489">Empty the **Title** and **Price** fields and click **Save**.</span></span> <span data-ttu-id="6f055-490">確認您取得對應的驗證訊息。</span><span class="sxs-lookup"><span data-stu-id="6f055-490">Verify that you get the corresponding validation messages.</span></span>

    ![[編輯] 頁面中的已驗證欄位](aspnet-mvc-4-helpers-forms-and-validation/_static/image19.png)

    <span data-ttu-id="6f055-492">*[編輯] 頁面中的已驗證欄位*</span><span class="sxs-lookup"><span data-stu-id="6f055-492">*Validated fields in the Edit page*</span></span>

<a id="Exercise7"></a>

<a id="Exercise_7_Using_Unobtrusive_jQuery_at_Client_Side"></a>
### <a name="exercise-7-using-unobtrusive-jquery-at-client-side"></a><span data-ttu-id="6f055-493">練習7：在用戶端使用不顯眼的 jQuery</span><span class="sxs-lookup"><span data-stu-id="6f055-493">Exercise 7: Using Unobtrusive jQuery at Client Side</span></span>

<span data-ttu-id="6f055-494">在此練習中，您將瞭解如何在用戶端啟用 MVC 4 不顯眼的 jQuery 驗證。</span><span class="sxs-lookup"><span data-stu-id="6f055-494">In this exercise, you will learn how to enable MVC 4 Unobtrusive jQuery validation at client side.</span></span>

> [!NOTE]
> <span data-ttu-id="6f055-495">不顯眼的 jQuery 會使用資料 ajax 前置詞 JavaScript，在伺服器上叫用動作方法，而不是干擾發出內嵌用戶端腳本。</span><span class="sxs-lookup"><span data-stu-id="6f055-495">The Unobtrusive jQuery uses data-ajax prefix JavaScript to invoke action methods on the server rather than intrusively emitting inline client scripts.</span></span>

<a id="Ex7Task1"></a>

<a id="Task_1_-_Running_the_Application_before_Enabling_Unobtrusive_jQuery"></a>
#### <a name="task-1---running-the-application-before-enabling-unobtrusive-jquery"></a><span data-ttu-id="6f055-496">工作 1-在啟用不顯眼的 jQuery 之前執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-496">Task 1 - Running the Application before Enabling Unobtrusive jQuery</span></span>

<span data-ttu-id="6f055-497">在這項工作中，您將在包含 jQuery 之前執行應用程式，以便比較這兩個驗證模型。</span><span class="sxs-lookup"><span data-stu-id="6f055-497">In this task, you will run the application before including jQuery in order to compare both validation models.</span></span>

1. <span data-ttu-id="6f055-498">開啟位於**來源/Ex7-UnobtrusivejQueryValidation/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-498">Open the **Begin** solution located at **Source/Ex7-UnobtrusivejQueryValidation/Begin/** folder.</span></span> <span data-ttu-id="6f055-499">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-499">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="6f055-500">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="6f055-500">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="6f055-501">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-501">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="6f055-502">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="6f055-502">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="6f055-503">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="6f055-503">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="6f055-504">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="6f055-504">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="6f055-505">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f055-505">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="6f055-506">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="6f055-506">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="6f055-507">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-507">Press **F5** to run the application.</span></span>
3. <span data-ttu-id="6f055-508">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-508">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-509">流覽 **/StoreManager/Create** ，然後按一下 [**建立**] 而不填滿表單，以確認您取得驗證訊息：</span><span class="sxs-lookup"><span data-stu-id="6f055-509">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="6f055-510">![已停用用戶端驗證](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "已停用用戶端驗證")</span><span class="sxs-lookup"><span data-stu-id="6f055-510">![Client validation disabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image20.png "Client validation disabled")</span></span>

    <span data-ttu-id="6f055-511">*已停用用戶端驗證*</span><span class="sxs-lookup"><span data-stu-id="6f055-511">*Client validation disabled*</span></span>
4. <span data-ttu-id="6f055-512">在瀏覽器中，開啟 HTML 原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f055-512">In the browser, open the HTML source code:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample20.html)]

<a id="Ex7Task2"></a>

<a id="Task_2_-_Enabling_Unobtrusive_Client_Validation"></a>
#### <a name="task-2---enabling-unobtrusive-client-validation"></a><span data-ttu-id="6f055-513">工作 2-啟用不顯眼的用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="6f055-513">Task 2 - Enabling Unobtrusive Client Validation</span></span>

<span data-ttu-id="6f055-514">在這項工作**中，您將從 web.config**檔案啟用 jQuery 不顯眼的**用戶端驗證**，在所有新的 ASP.NET MVC 4 專案中，預設都會設定為 false。</span><span class="sxs-lookup"><span data-stu-id="6f055-514">In this task, you will enable jQuery **unobtrusive client validation** from **Web.config** file, which is by default set to false in all new ASP.NET MVC 4 projects.</span></span> <span data-ttu-id="6f055-515">此外，您還會加入必要的腳本參考，以進行 jQuery 不顯眼的用戶端驗證工作。</span><span class="sxs-lookup"><span data-stu-id="6f055-515">Additionally, you will add the necessary scripts references to make jQuery Unobtrusive Client Validation work.</span></span>

1. <span data-ttu-id="6f055-516">在專案根目錄開啟**web.config**檔案，並確定 [ **ClientValidationEnabled** ] 和 [ **UnobtrusiveJavaScriptEnabled**索引鍵] 值已設定為 [ **true**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-516">Open **Web.Config** file at project root, and make sure that the **ClientValidationEnabled** and **UnobtrusiveJavaScriptEnabled** keys values are set to **true**.</span></span>

    [!code-xml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample21.xml)]

    > [!NOTE]
    > <span data-ttu-id="6f055-517">您也可以在 Global.asax.cs 的程式碼中啟用用戶端驗證，以取得相同的結果：</span><span class="sxs-lookup"><span data-stu-id="6f055-517">You can also enable client validation by code at Global.asax.cs to get the same results:</span></span>
    > 
    > <span data-ttu-id="6f055-518">**HtmlHelper. ClientValidationEnabled = true;**</span><span class="sxs-lookup"><span data-stu-id="6f055-518">**HtmlHelper.ClientValidationEnabled = true;**</span></span>
    > 
    > <span data-ttu-id="6f055-519">此外，您可以將 ClientValidationEnabled 屬性指派給任何控制器，使其具有自訂行為。</span><span class="sxs-lookup"><span data-stu-id="6f055-519">Additionally, you can assign ClientValidationEnabled attribute into any controller to have a custom behavior.</span></span>
2. <span data-ttu-id="6f055-520">在**Views\StoreManager**開啟**Create. cshtml** 。</span><span class="sxs-lookup"><span data-stu-id="6f055-520">Open **Create.cshtml** at **Views\StoreManager**.</span></span>
3. <span data-ttu-id="6f055-521">請確定已透過 &quot; **~/bundles/jqueryval**&quot; 配套，在 view 中參考下列腳本檔案**jquery.** validate 和**jquery**。</span><span class="sxs-lookup"><span data-stu-id="6f055-521">Make sure the following script files, **jquery.validate** and **jquery.validate.unobtrusive**, are referenced in the view through the &quot;**~/bundles/jqueryval**&quot; bundle.</span></span>

    [!code-cshtml[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample22.cshtml)]

    > [!NOTE]
    > <span data-ttu-id="6f055-522">所有這些 jQuery 程式庫都包含在 MVC 4 新專案中。</span><span class="sxs-lookup"><span data-stu-id="6f055-522">All these jQuery libraries are included in MVC 4 new projects.</span></span> <span data-ttu-id="6f055-523">您可以在專案的 **/Scripts**資料夾中找到更多程式庫。</span><span class="sxs-lookup"><span data-stu-id="6f055-523">You can find more libraries in the **/Scripts** folder of you project.</span></span>
    > 
    > <span data-ttu-id="6f055-524">若要讓此驗證程式庫正常執行，您必須加入 jQuery framework 程式庫的參考。</span><span class="sxs-lookup"><span data-stu-id="6f055-524">In order to make this validation libraries work, you need to add a reference to the jQuery framework library.</span></span> <span data-ttu-id="6f055-525">因為此參考已經加入\_的配置**cshtml**檔案中，所以您不需要將它新增到這個特定的視圖中。</span><span class="sxs-lookup"><span data-stu-id="6f055-525">Since this reference is already added in the **\_Layout.cshtml** file, you do not need to add it in this particular view.</span></span>

<a id="Ex7Task3"></a>

<a id="Task_3_-_Running_the_Application_Using_Unobtrusive_jQuery_Validation"></a>
#### <a name="task-3---running-the-application-using-unobtrusive-jquery-validation"></a><span data-ttu-id="6f055-526">工作 3-使用不顯眼的 jQuery 驗證執行應用程式</span><span class="sxs-lookup"><span data-stu-id="6f055-526">Task 3 - Running the Application Using Unobtrusive jQuery Validation</span></span>

<span data-ttu-id="6f055-527">在這項工作中，您將測試**StoreManager** create view 範本會在使用者建立新的專輯時，使用 jQuery 程式庫來執行用戶端驗證。</span><span class="sxs-lookup"><span data-stu-id="6f055-527">In this task, you will test that the **StoreManager** create view template performs client side validation using jQuery libraries when the user creates a new album.</span></span>

1. <span data-ttu-id="6f055-528">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-528">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="6f055-529">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="6f055-529">The project starts in the Home page.</span></span> <span data-ttu-id="6f055-530">流覽 **/StoreManager/Create** ，然後按一下 [**建立**] 而不填滿表單，以確認您取得驗證訊息：</span><span class="sxs-lookup"><span data-stu-id="6f055-530">Browse **/StoreManager/Create** and click **Create** without filling the form to verify that you get validation messages:</span></span>

    <span data-ttu-id="6f055-531">![已啟用 jQuery 的用戶端驗證](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "已啟用 jQuery 的用戶端驗證")</span><span class="sxs-lookup"><span data-stu-id="6f055-531">![Client validation with jQuery enabled](aspnet-mvc-4-helpers-forms-and-validation/_static/image21.png "Client validation with jQuery enabled")</span></span>

    <span data-ttu-id="6f055-532">*已啟用 jQuery 的用戶端驗證*</span><span class="sxs-lookup"><span data-stu-id="6f055-532">*Client validation with jQuery enabled*</span></span>
3. <span data-ttu-id="6f055-533">在瀏覽器中，開啟 [建立視圖] 的原始程式碼：</span><span class="sxs-lookup"><span data-stu-id="6f055-533">In the browser, open the source code for Create view:</span></span>

    [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample23.html)]

   > [!NOTE]
   > <span data-ttu-id="6f055-534">針對每個用戶端驗證規則，不顯眼的 jQuery 會加入具有資料 val-*rulename*=&quot;*訊息*&quot;的屬性。</span><span class="sxs-lookup"><span data-stu-id="6f055-534">For each client validation rule, Unobtrusive jQuery adds an attribute with data-val-*rulename*=&quot;*message*&quot;.</span></span> <span data-ttu-id="6f055-535">以下是不顯眼的 jQuery 插入 html 輸入欄位來執行用戶端驗證的標記清單：</span><span class="sxs-lookup"><span data-stu-id="6f055-535">Below is a list of tags that Unobtrusive jQuery inserts into the html input field to perform client validation:</span></span>
   > 
   > - <span data-ttu-id="6f055-536">資料-val</span><span class="sxs-lookup"><span data-stu-id="6f055-536">Data-val</span></span>
   > - <span data-ttu-id="6f055-537">資料-val-數位</span><span class="sxs-lookup"><span data-stu-id="6f055-537">Data-val-number</span></span>
   > - <span data-ttu-id="6f055-538">資料-val-範圍</span><span class="sxs-lookup"><span data-stu-id="6f055-538">Data-val-range</span></span>
   > - <span data-ttu-id="6f055-539">資料-val-範圍-分鐘/資料-val-範圍-最大值</span><span class="sxs-lookup"><span data-stu-id="6f055-539">Data-val-range-min / Data-val-range-max</span></span>
   > - <span data-ttu-id="6f055-540">資料-val-必要</span><span class="sxs-lookup"><span data-stu-id="6f055-540">Data-val-required</span></span>
   > - <span data-ttu-id="6f055-541">資料-val-長度</span><span class="sxs-lookup"><span data-stu-id="6f055-541">Data-val-length</span></span>
   > - <span data-ttu-id="6f055-542">資料-val-長度-最大/資料-val-長度-分鐘</span><span class="sxs-lookup"><span data-stu-id="6f055-542">Data-val-length-max / Data-val-length-min</span></span>
   > 
   > <span data-ttu-id="6f055-543">所有資料值都會填入模型**資料注釋**。</span><span class="sxs-lookup"><span data-stu-id="6f055-543">All the data values are filled with model **Data Annotation**.</span></span> <span data-ttu-id="6f055-544">然後，在伺服器端運作的所有邏輯都可以在用戶端執行。</span><span class="sxs-lookup"><span data-stu-id="6f055-544">Then, all the logic that works at server side can be run at client side.</span></span> <span data-ttu-id="6f055-545">例如，Price 屬性在模型中具有下列資料批註：</span><span class="sxs-lookup"><span data-stu-id="6f055-545">For example, Price attribute has the following data annotation in the model:</span></span>
   > 
   > [!code-csharp[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample24.cs)]
   > 
   > <span data-ttu-id="6f055-546">使用不顯眼的 jQuery 之後，產生的程式碼為：</span><span class="sxs-lookup"><span data-stu-id="6f055-546">After using Unobtrusive jQuery, the generated code is:</span></span>
   > 
   > [!code-html[Main](aspnet-mvc-4-helpers-forms-and-validation/samples/sample25.html)]

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="6f055-547">總結</span><span class="sxs-lookup"><span data-stu-id="6f055-547">Summary</span></span>

<span data-ttu-id="6f055-548">藉由完成此實際操作實驗室，您已瞭解如何讓使用者使用下列各項來變更儲存在資料庫中的資料：</span><span class="sxs-lookup"><span data-stu-id="6f055-548">By completing this Hands-On Lab you have learned how to enable users to change the data stored in the database with the use of the following:</span></span>

- <span data-ttu-id="6f055-549">控制器動作，例如索引、建立、編輯、刪除</span><span class="sxs-lookup"><span data-stu-id="6f055-549">Controller actions like Index, Create, Edit, Delete</span></span>
- <span data-ttu-id="6f055-550">ASP.NET MVC 在 HTML 資料表中顯示內容的功能</span><span class="sxs-lookup"><span data-stu-id="6f055-550">ASP.NET MVC's scaffolding feature for displaying properties in an HTML table</span></span>
- <span data-ttu-id="6f055-551">自訂 HTML 協助程式以改善使用者體驗</span><span class="sxs-lookup"><span data-stu-id="6f055-551">Custom HTML helpers to improve user experience</span></span>
- <span data-ttu-id="6f055-552">回應 HTTP GET 或 HTTP POST 呼叫的動作方法</span><span class="sxs-lookup"><span data-stu-id="6f055-552">Action methods that react to either HTTP-GET or HTTP-POST calls</span></span>
- <span data-ttu-id="6f055-553">類似視圖範本的共用編輯器範本，例如建立和編輯</span><span class="sxs-lookup"><span data-stu-id="6f055-553">A shared editor template for similar View templates like Create and Edit</span></span>
- <span data-ttu-id="6f055-554">下拉式清單等表單元素</span><span class="sxs-lookup"><span data-stu-id="6f055-554">Form elements like drop-downs</span></span>
- <span data-ttu-id="6f055-555">模型驗證的資料批註</span><span class="sxs-lookup"><span data-stu-id="6f055-555">Data annotations for Model validation</span></span>
- <span data-ttu-id="6f055-556">使用 jQuery 不顯眼程式庫的用戶端驗證</span><span class="sxs-lookup"><span data-stu-id="6f055-556">Client Side Validation using jQuery Unobtrusive library</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="6f055-557">附錄 A：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="6f055-557">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="6f055-558">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="6f055-558">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="6f055-559">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="6f055-559">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="6f055-560">移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="6f055-560">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="6f055-561">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="6f055-561">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="6f055-562">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-562">Click on **Install Now**.</span></span> <span data-ttu-id="6f055-563">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="6f055-563">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="6f055-564">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="6f055-564">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="6f055-565">![安裝 Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="6f055-565">![Install Visual Studio Express](aspnet-mvc-4-helpers-forms-and-validation/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="6f055-566">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="6f055-566">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="6f055-567">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="6f055-567">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](aspnet-mvc-4-helpers-forms-and-validation/_static/image23.png)

    <span data-ttu-id="6f055-569">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="6f055-569">*Accepting the license terms*</span></span>
5. <span data-ttu-id="6f055-570">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="6f055-570">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](aspnet-mvc-4-helpers-forms-and-validation/_static/image24.png)

    <span data-ttu-id="6f055-572">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="6f055-572">*Installation progress*</span></span>
6. <span data-ttu-id="6f055-573">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="6f055-573">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](aspnet-mvc-4-helpers-forms-and-validation/_static/image25.png)

    <span data-ttu-id="6f055-575">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="6f055-575">*Installation completed*</span></span>
7. <span data-ttu-id="6f055-576">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="6f055-576">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="6f055-577">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="6f055-577">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](aspnet-mvc-4-helpers-forms-and-validation/_static/image26.png)

    <span data-ttu-id="6f055-579">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="6f055-579">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="6f055-580">附錄 B：使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="6f055-580">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="6f055-581">有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="6f055-581">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="6f055-582">實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="6f055-582">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="6f055-583">![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")</span><span class="sxs-lookup"><span data-stu-id="6f055-583">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-helpers-forms-and-validation/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="6f055-584">*使用 Visual Studio 程式碼片段將程式碼插入您的專案*</span><span class="sxs-lookup"><span data-stu-id="6f055-584">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="6f055-585">***若要使用鍵盤新增程式碼片段（C#僅限）***</span><span class="sxs-lookup"><span data-stu-id="6f055-585">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="6f055-586">將游標放在您想要插入程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="6f055-586">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="6f055-587">開始鍵入程式碼片段名稱（不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="6f055-587">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="6f055-588">監看 IntelliSense 會顯示相符的程式碼片段名稱。</span><span class="sxs-lookup"><span data-stu-id="6f055-588">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="6f055-589">選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。</span><span class="sxs-lookup"><span data-stu-id="6f055-589">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="6f055-590">按兩次 Tab 鍵，在游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="6f055-590">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="6f055-591">![開始鍵入程式碼片段名稱](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "開始鍵入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="6f055-591">![Start typing the snippet name](aspnet-mvc-4-helpers-forms-and-validation/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="6f055-592">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="6f055-592">*Start typing the snippet name*</span></span>

<span data-ttu-id="6f055-593">![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="6f055-593">![Press Tab to select the highlighted snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="6f055-594">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="6f055-594">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="6f055-595">![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "再按一次 Tab 鍵，將會展開程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="6f055-595">![Press Tab again and the snippet will expand](aspnet-mvc-4-helpers-forms-and-validation/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="6f055-596">*再按一次 Tab 鍵，將會展開程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="6f055-596">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="6f055-597">***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1.</span><span class="sxs-lookup"><span data-stu-id="6f055-597">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="6f055-598">以滑鼠右鍵按一下您要插入程式碼片段的位置。</span><span class="sxs-lookup"><span data-stu-id="6f055-598">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="6f055-599">選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。</span><span class="sxs-lookup"><span data-stu-id="6f055-599">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="6f055-600">按一下清單中的相關程式碼片段，即可加以選取。</span><span class="sxs-lookup"><span data-stu-id="6f055-600">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="6f055-601">![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")</span><span class="sxs-lookup"><span data-stu-id="6f055-601">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-helpers-forms-and-validation/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="6f055-602">*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*</span><span class="sxs-lookup"><span data-stu-id="6f055-602">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="6f055-603">![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "按一下清單中的相關程式碼片段，即可加以選取")</span><span class="sxs-lookup"><span data-stu-id="6f055-603">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-helpers-forms-and-validation/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="6f055-604">*按一下清單中的相關程式碼片段，即可加以選取*</span><span class="sxs-lookup"><span data-stu-id="6f055-604">*Pick the relevant snippet from the list, by clicking on it*</span></span>
