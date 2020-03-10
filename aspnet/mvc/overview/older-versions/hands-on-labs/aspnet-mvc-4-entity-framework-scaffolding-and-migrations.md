---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
title: ASP.NET MVC 4 Entity Framework 的架構和遷移 |Microsoft Docs
author: rick-anderson
description: 如果您熟悉 ASP.NET MVC 4 控制器方法，或已完成 &quot;協助程式、表單和驗證&quot; 實際操作實驗室，您應該注意 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 093c1362-f10b-407c-a708-be370f4b62b0
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-entity-framework-scaffolding-and-migrations
msc.type: authoredcontent
ms.openlocfilehash: 2b26224390af70e19ca0593abe93a6867140f8ab
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78598900"
---
# <a name="aspnet-mvc-4-entity-framework-scaffolding-and-migrations"></a><span data-ttu-id="b27b9-103">ASP.NET MVC 4 Entity Framework Scaffold 和移轉</span><span class="sxs-lookup"><span data-stu-id="b27b9-103">ASP.NET MVC 4 Entity Framework Scaffolding and Migrations</span></span>

<span data-ttu-id="b27b9-104">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="b27b9-104">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="b27b9-105">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="b27b9-105">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="b27b9-106">如果您熟悉 ASP.NET MVC 4 控制器方法，或已完成 &quot;協助程式、表單和驗證&quot; 實際操作實驗室，您應該注意到，有許多邏輯可以用來建立、更新、列出和移除任何資料實體，這會在應用程式之間重複。</span><span class="sxs-lookup"><span data-stu-id="b27b9-106">If you are familiar with ASP.NET MVC 4 controller methods, or have completed the &quot;Helpers, Forms and Validation&quot; Hands-On lab, you should be aware that many of the logic to create, update, list and remove any data entity it is repeated among the application.</span></span> <span data-ttu-id="b27b9-107">不提說，如果您的模型有數個要操作的類別，您可能會花費相當長的時間來撰寫每個實體作業的 POST 和 GET 動作方法，以及每個視圖。</span><span class="sxs-lookup"><span data-stu-id="b27b9-107">Not to mention that, if your model has several classes to manipulate, you will be likely to spend a considerable time writing the POST and GET action methods for each entity operation, as well as each of the views.</span></span>

<span data-ttu-id="b27b9-108">在此實驗室中，您將瞭解如何使用 ASP.NET MVC 4 架構，自動產生應用程式 CRUD （建立、讀取、更新和刪除）的基準。</span><span class="sxs-lookup"><span data-stu-id="b27b9-108">In this lab you will learn how to use the ASP.NET MVC 4 scaffolding to automatically generate the baseline of your application's CRUD (Create, Read, Update and Delete).</span></span> <span data-ttu-id="b27b9-109">從簡單的模型類別開始，而不需撰寫任何一行程式碼，您將建立一個控制器，其中包含所有 CRUD 作業，以及所有必要的視圖。</span><span class="sxs-lookup"><span data-stu-id="b27b9-109">Starting from a simple model class, and, without writing a single line of code, you will create a controller that will contain all the CRUD operations, as well as the all the necessary views.</span></span> <span data-ttu-id="b27b9-110">建立並執行簡單的方案之後，您將會產生應用程式資料庫，以及用於資料操作的 MVC 邏輯和 views。</span><span class="sxs-lookup"><span data-stu-id="b27b9-110">After building and running the simple solution, you will have the application database generated, together with the MVC logic and views for data manipulation.</span></span>

<span data-ttu-id="b27b9-111">此外，您將瞭解在整個應用程式中使用 Entity Framework 遷移來執行模型更新有多麼容易。</span><span class="sxs-lookup"><span data-stu-id="b27b9-111">In addition, you will learn how easy it is to use Entity Framework Migrations to perform model updates throughout your entire application.</span></span> <span data-ttu-id="b27b9-112">Entity Framework 遷移可讓您在使用簡單步驟變更模型之後，修改資料庫。</span><span class="sxs-lookup"><span data-stu-id="b27b9-112">Entity Framework Migrations will let you modify your database after the model has changed with simple steps.</span></span> <span data-ttu-id="b27b9-113">有了這些概念，您就能夠更有效率地建立及維護 web 應用程式，利用 ASP.NET MVC 4 的最新功能。</span><span class="sxs-lookup"><span data-stu-id="b27b9-113">With all these in mind, you will be able to build and maintain web applications more efficiently, taking advantage of the latest features of ASP.NET MVC 4.</span></span>

> [!NOTE]
> <span data-ttu-id="b27b9-114">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可從[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="b27b9-114">All sample code and snippets are included in the Web Camps Training Kit, available from at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="b27b9-115">此實驗室的特定專案可在[ASP.NET MVC 4 Entity Framework 的樣板和遷移](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations)中取得。</span><span class="sxs-lookup"><span data-stu-id="b27b9-115">The project specific to this lab is available at [ASP.NET MVC 4 Entity Framework Scaffolding and Migrations](https://github.com/Microsoft-Web/HOL-EntityFrameworkScaffoldingAndMigrations).</span></span>

<a id="Objectives"></a>
### <a name="objectives"></a><span data-ttu-id="b27b9-116">目標</span><span class="sxs-lookup"><span data-stu-id="b27b9-116">Objectives</span></span>

<span data-ttu-id="b27b9-117">在此實際操作實驗室中，您將瞭解如何：</span><span class="sxs-lookup"><span data-stu-id="b27b9-117">In this Hands-On Lab, you will learn how to:</span></span>

- <span data-ttu-id="b27b9-118">在控制器中使用 CRUD 作業的 ASP.NET 架構。</span><span class="sxs-lookup"><span data-stu-id="b27b9-118">Use ASP.NET scaffolding for CRUD operations in controllers.</span></span>
- <span data-ttu-id="b27b9-119">使用 Entity Framework 遷移來變更資料庫模型。</span><span class="sxs-lookup"><span data-stu-id="b27b9-119">Change the database model using Entity Framework Migrations.</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="b27b9-120">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="b27b9-120">Prerequisites</span></span>

<span data-ttu-id="b27b9-121">您必須具有下列專案，才能完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="b27b9-121">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="b27b9-122">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。</span><span class="sxs-lookup"><span data-stu-id="b27b9-122">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="b27b9-123">安裝程式</span><span class="sxs-lookup"><span data-stu-id="b27b9-123">Setup</span></span>

<span data-ttu-id="b27b9-124">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="b27b9-124">**Installing Code Snippets**</span></span>

<span data-ttu-id="b27b9-125">為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。</span><span class="sxs-lookup"><span data-stu-id="b27b9-125">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="b27b9-126">若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="b27b9-126">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="b27b9-127">如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 B：使用程式碼片段](#AppendixB)&quot;。</span><span class="sxs-lookup"><span data-stu-id="b27b9-127">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix B: Using Code Snippets](#AppendixB)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="b27b9-128">練習</span><span class="sxs-lookup"><span data-stu-id="b27b9-128">Exercises</span></span>

<span data-ttu-id="b27b9-129">下列練習會組成這個實際操作實驗室：</span><span class="sxs-lookup"><span data-stu-id="b27b9-129">The following exercise make up this Hands-On Lab:</span></span>

1. [<span data-ttu-id="b27b9-130">搭配 Entity Framework 遷移使用 ASP.NET MVC 4 樣板</span><span class="sxs-lookup"><span data-stu-id="b27b9-130">Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>](#Exercise1)

> [!NOTE]
> <span data-ttu-id="b27b9-131">此練習會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。</span><span class="sxs-lookup"><span data-stu-id="b27b9-131">This exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercise.</span></span> <span data-ttu-id="b27b9-132">如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。</span><span class="sxs-lookup"><span data-stu-id="b27b9-132">You can use this solution as a guide if you need additional help working through the exercise.</span></span>

<span data-ttu-id="b27b9-133">完成此實驗室的預估時間： **30 分鐘**</span><span class="sxs-lookup"><span data-stu-id="b27b9-133">Estimated time to complete this lab: **30 minutes**</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Using_ASPNET_MVC_4_Scaffolding_with_Entity_Framework_Migrations"></a>
### <a name="exercise-1-using-aspnet-mvc-4-scaffolding-with-entity-framework-migrations"></a><span data-ttu-id="b27b9-134">練習1：搭配 Entity Framework 遷移使用 ASP.NET MVC 4 樣板</span><span class="sxs-lookup"><span data-stu-id="b27b9-134">Exercise 1: Using ASP.NET MVC 4 Scaffolding with Entity Framework Migrations</span></span>

<span data-ttu-id="b27b9-135">ASP.NET MVC 樣板提供快速的方式，以標準化的方式產生 CRUD 作業，建立必要的邏輯，讓您的應用程式與資料庫層互動。</span><span class="sxs-lookup"><span data-stu-id="b27b9-135">ASP.NET MVC scaffolding provides a quick way to generate the CRUD operations in a standardized way, creating the necessary logic that lets your application interact with the database layer.</span></span>

<span data-ttu-id="b27b9-136">在此練習中，您將瞭解如何搭配使用 ASP.NET MVC 4 樣板與 code first 來建立 CRUD 方法。</span><span class="sxs-lookup"><span data-stu-id="b27b9-136">In this exercise, you will learn how to use ASP.NET MVC 4 scaffolding with code first to create the CRUD methods.</span></span> <span data-ttu-id="b27b9-137">然後，您將瞭解如何使用 Entity Framework 遷移來更新您的模型，套用資料庫中的變更。</span><span class="sxs-lookup"><span data-stu-id="b27b9-137">Then, you will learn how to update your model applying the changes in the database by using Entity Framework Migrations.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1-_Creating_a_new_ASPNET_MVC_4_project_using_Scaffolding"></a>
#### <a name="task-1--creating-a-new-aspnet-mvc-4-project-using-scaffolding"></a><span data-ttu-id="b27b9-138">工作 1-使用樣板建立新的 ASP.NET MVC 4 專案</span><span class="sxs-lookup"><span data-stu-id="b27b9-138">Task 1- Creating a new ASP.NET MVC 4 project using Scaffolding</span></span>

1. <span data-ttu-id="b27b9-139">如果尚未開啟，請啟動**Visual Studio 2012**。</span><span class="sxs-lookup"><span data-stu-id="b27b9-139">If not already open, start **Visual Studio 2012**.</span></span>
2. <span data-ttu-id="b27b9-140">選取檔案 **|新增專案**。</span><span class="sxs-lookup"><span data-stu-id="b27b9-140">Select **File | New Project**.</span></span> <span data-ttu-id="b27b9-141">在 [新增專案] 對話方塊中的 **[ C#視覺效果] |Web**區段中，選取 [ **ASP.NET MVC 4 Web 應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-141">In the New Project dialog, under the **Visual C# | Web** section, select **ASP.NET MVC 4 Web Application**.</span></span> <span data-ttu-id="b27b9-142">將專案命名為**MVC4andEFMigrations** ，並將此實驗室的 [位置] 設定為 [ **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="b27b9-142">Name the project to **MVC4andEFMigrations** and set the location to **Source\Ex1-UsingMVC4ScaffoldingEFMigrations** folder of this lab.</span></span> <span data-ttu-id="b27b9-143">將 [**方案名稱**] 設定為 [**開始**]，並確定已核取 [**為方案建立目錄**]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-143">Set the **Solution name** to **Begin** and ensure **Create directory for solution** is checked.</span></span> <span data-ttu-id="b27b9-144">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-144">Click **OK**.</span></span>

    <span data-ttu-id="b27b9-145">![[新增 ASP.NET MVC 4 專案] 對話方塊](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "[新增 ASP.NET MVC 4 專案] 對話方塊")</span><span class="sxs-lookup"><span data-stu-id="b27b9-145">![New ASP.NET MVC 4 Project Dialog Box](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image1.png "New ASP.NET MVC 4 Project Dialog Box")</span></span>

    <span data-ttu-id="b27b9-146">*[新增 ASP.NET MVC 4 專案] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="b27b9-146">*New ASP.NET MVC 4 Project Dialog Box*</span></span>
3. <span data-ttu-id="b27b9-147">在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 範本，並確定 [ **Razor** ] 是選取的**視圖引擎**。</span><span class="sxs-lookup"><span data-stu-id="b27b9-147">In the **New ASP.NET MVC 4 Project** dialog box select the **Internet Application** template, and make sure that **Razor** is the selected **View engine**.</span></span> <span data-ttu-id="b27b9-148">按一下 [確定] 建立專案。</span><span class="sxs-lookup"><span data-stu-id="b27b9-148">Click **OK** to create the project.</span></span>

    <span data-ttu-id="b27b9-149">![新增 ASP.NET MVC 4 網際網路應用程式](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "新增 ASP.NET MVC 4 網際網路應用程式")</span><span class="sxs-lookup"><span data-stu-id="b27b9-149">![New ASP.NET MVC 4 Internet Application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image2.png "New ASP.NET MVC 4 Internet Application")</span></span>

    <span data-ttu-id="b27b9-150">*新增 ASP.NET MVC 4 網際網路應用程式*</span><span class="sxs-lookup"><span data-stu-id="b27b9-150">*New ASP.NET MVC 4 Internet Application*</span></span>
4. <span data-ttu-id="b27b9-151">在方案總管中，以滑鼠右鍵按一下 [**模型**]，然後選取 [**新增] |** 建立簡單類別 person （POCO）的類別。</span><span class="sxs-lookup"><span data-stu-id="b27b9-151">In the Solution Explorer, right-click **Models** and select **Add | Class** to create a simple class person (POCO).</span></span> <span data-ttu-id="b27b9-152">為 it**人員**命名，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="b27b9-152">Name it **Person** and click **OK**.</span></span>
5. <span data-ttu-id="b27b9-153">開啟 Person 類別並插入下列屬性。</span><span class="sxs-lookup"><span data-stu-id="b27b9-153">Open the Person class and insert the following properties.</span></span>

    <span data-ttu-id="b27b9-154">（程式碼片段- *ASP.NET MVC 4 和 Entity Framework 遷移-Ex1 Person 屬性*）</span><span class="sxs-lookup"><span data-stu-id="b27b9-154">(Code Snippet - *ASP.NET MVC 4 and Entity Framework Migrations - Ex1 Person Properties*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample1.cs)]
6. <span data-ttu-id="b27b9-155">按一下 [**組建] |建立方案**以儲存變更並建立專案。</span><span class="sxs-lookup"><span data-stu-id="b27b9-155">Click **Build | Build Solution** to save the changes and build the project.</span></span>

    <span data-ttu-id="b27b9-156">![建置應用程式](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "建置應用程式")</span><span class="sxs-lookup"><span data-stu-id="b27b9-156">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image3.png "Building the application")</span></span>

    <span data-ttu-id="b27b9-157">*建置應用程式*</span><span class="sxs-lookup"><span data-stu-id="b27b9-157">*Building the Application*</span></span>
7. <span data-ttu-id="b27b9-158">在 方案總管中，以滑鼠右鍵按一下 控制器 資料夾，然後選取 **新增 |控制器**。</span><span class="sxs-lookup"><span data-stu-id="b27b9-158">In the Solution Explorer, right-click the controllers folder and select **Add | Controller**.</span></span>
8. <span data-ttu-id="b27b9-159">將控制器命名為*PersonController* ，並使用下列值完成 [樣板]**選項**。</span><span class="sxs-lookup"><span data-stu-id="b27b9-159">Name the controller *PersonController* and complete the **Scaffolding options** with the following values.</span></span>

   1. <span data-ttu-id="b27b9-160">在 [**範本**] 下拉式清單中，使用 [Entity Framework] 選項，選取**具有讀取/寫入動作和 views 的 MVC 控制器**。</span><span class="sxs-lookup"><span data-stu-id="b27b9-160">In the **Template** drop-down list, select the **MVC controller with read/write actions and views, using Entity Framework** option.</span></span>
   2. <span data-ttu-id="b27b9-161">在 [**模型類別**] 下拉式清單中，選取 [ **Person** ] 類別。</span><span class="sxs-lookup"><span data-stu-id="b27b9-161">In the **Model class** drop-down list, select the **Person** class.</span></span>
   3. <span data-ttu-id="b27b9-162">在 [**資料內容類別**] 清單中，選取 [ **&lt;新的資料內容 ...]&gt;** 。</span><span class="sxs-lookup"><span data-stu-id="b27b9-162">In the **Data Context class** list, select **&lt;New data context...&gt;**.</span></span> <span data-ttu-id="b27b9-163">選擇任何名稱，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="b27b9-163">Choose any name and click **OK**.</span></span>
   4. <span data-ttu-id="b27b9-164">在 [ **Views** ] 下拉式清單中，確認已選取 [ **Razor** ]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-164">In the **Views** drop-down list, make sure that **Razor** is selected.</span></span>

      <span data-ttu-id="b27b9-165">![使用樣板新增人員控制器](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "使用樣板新增人員控制器")</span><span class="sxs-lookup"><span data-stu-id="b27b9-165">![Adding the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image4.png "Adding the Person controller with scaffolding")</span></span>

      <span data-ttu-id="b27b9-166">*使用樣板新增人員控制器*</span><span class="sxs-lookup"><span data-stu-id="b27b9-166">*Adding the Person controller with scaffolding*</span></span>
9. <span data-ttu-id="b27b9-167">按一下 [**新增**]，為具有樣板的人員建立新的控制器。</span><span class="sxs-lookup"><span data-stu-id="b27b9-167">Click **Add** to create the new controller for Person with scaffolding.</span></span> <span data-ttu-id="b27b9-168">您現在已產生控制器動作和 views。</span><span class="sxs-lookup"><span data-stu-id="b27b9-168">You have now generated the controller actions as well as the views.</span></span>

    <span data-ttu-id="b27b9-169">![建立具有樣板的人員控制器之後](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "建立具有樣板的人員控制器之後")</span><span class="sxs-lookup"><span data-stu-id="b27b9-169">![After creating the Person controller with scaffolding](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image5.png "After creating the Person controller with scaffolding")</span></span>

    <span data-ttu-id="b27b9-170">*建立具有樣板的人員控制器之後*</span><span class="sxs-lookup"><span data-stu-id="b27b9-170">*After creating the Person controller with scaffolding*</span></span>
10. <span data-ttu-id="b27b9-171">開啟**PersonController**類別。</span><span class="sxs-lookup"><span data-stu-id="b27b9-171">Open **PersonController** class.</span></span> <span data-ttu-id="b27b9-172">請注意，已自動產生完整的 CRUD 動作方法。</span><span class="sxs-lookup"><span data-stu-id="b27b9-172">Notice that the full CRUD action methods have been generated automatically.</span></span>

   <span data-ttu-id="b27b9-173">![在人員控制器內](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "在人員控制器內")</span><span class="sxs-lookup"><span data-stu-id="b27b9-173">![Inside the Person controller](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image6.png "Inside the Person controller")</span></span>

   <span data-ttu-id="b27b9-174">*在人員控制器內*</span><span class="sxs-lookup"><span data-stu-id="b27b9-174">*Inside the Person controller*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2-_Running_the_application"></a>
#### <a name="task-2--running-the-application"></a><span data-ttu-id="b27b9-175">工作 2-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="b27b9-175">Task 2- Running the application</span></span>

<span data-ttu-id="b27b9-176">此時，尚未建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="b27b9-176">At this point, the database is not yet created.</span></span> <span data-ttu-id="b27b9-177">在這項工作中，您會第一次執行應用程式，並測試 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="b27b9-177">In this task, you will run the application for the first time and test the CRUD operations.</span></span> <span data-ttu-id="b27b9-178">系統會使用 Code First 即時建立資料庫。</span><span class="sxs-lookup"><span data-stu-id="b27b9-178">The database will be created on the fly with Code First.</span></span>

1. <span data-ttu-id="b27b9-179">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b27b9-179">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="b27b9-180">在瀏覽器中，將 **/Person**新增至 URL，以開啟 [人員] 頁面。</span><span class="sxs-lookup"><span data-stu-id="b27b9-180">In the browser, add **/Person** to the URL to open the Person page.</span></span>

    <span data-ttu-id="b27b9-181">![應用程式首次執行](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "應用程式首次執行")</span><span class="sxs-lookup"><span data-stu-id="b27b9-181">![Application first run](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image7.png "Application first run")</span></span>

    <span data-ttu-id="b27b9-182">*應用程式：第一次執行*</span><span class="sxs-lookup"><span data-stu-id="b27b9-182">*Application: first run*</span></span>
3. <span data-ttu-id="b27b9-183">您現在將探索 Person 頁面並測試 CRUD 作業。</span><span class="sxs-lookup"><span data-stu-id="b27b9-183">You will now explore the Person pages and test the CRUD operations.</span></span>

    1. <span data-ttu-id="b27b9-184">按一下 [**建立新**的] 以加入新人員。</span><span class="sxs-lookup"><span data-stu-id="b27b9-184">Click **Create New** to add a new person.</span></span> <span data-ttu-id="b27b9-185">輸入 [名字] 和 [姓氏]，然後按一下 [**建立**]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-185">Enter a first name and a last name and click **Create**.</span></span>

        <span data-ttu-id="b27b9-186">![加入新人員](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "加入新人員")</span><span class="sxs-lookup"><span data-stu-id="b27b9-186">![Adding a new person](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image8.png "Adding a new person")</span></span>

        <span data-ttu-id="b27b9-187">*加入新人員*</span><span class="sxs-lookup"><span data-stu-id="b27b9-187">*Adding a new person*</span></span>
    2. <span data-ttu-id="b27b9-188">在人員清單中，您可以刪除、編輯或加入專案。</span><span class="sxs-lookup"><span data-stu-id="b27b9-188">In the person's list, you can delete, edit or add items.</span></span>

        <span data-ttu-id="b27b9-189">![人員清單](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "人員清單")</span><span class="sxs-lookup"><span data-stu-id="b27b9-189">![person list](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image9.png "person list")</span></span>

        <span data-ttu-id="b27b9-190">*人員清單*</span><span class="sxs-lookup"><span data-stu-id="b27b9-190">*Person list*</span></span>
    3. <span data-ttu-id="b27b9-191">按一下 [**詳細資料**] 以開啟該人員的詳細資料。</span><span class="sxs-lookup"><span data-stu-id="b27b9-191">Click **Details** to open the person's details.</span></span>

        <span data-ttu-id="b27b9-192">![人員的詳細資料](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "人員的詳細資料")</span><span class="sxs-lookup"><span data-stu-id="b27b9-192">![Person's details](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image10.png "Person's details")</span></span>

        <span data-ttu-id="b27b9-193">*人員的詳細資料*</span><span class="sxs-lookup"><span data-stu-id="b27b9-193">*Person's details*</span></span>
4. <span data-ttu-id="b27b9-194">關閉瀏覽器並返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="b27b9-194">Close the browser and return to Visual Studio.</span></span> <span data-ttu-id="b27b9-195">請注意，您已在整個應用程式中建立 person 實體的整個 CRUD-從模型到 views，而不需要撰寫任何一行程式碼！</span><span class="sxs-lookup"><span data-stu-id="b27b9-195">Notice that you have created the whole CRUD for the person entity throughout your application -from the model to the views- without having to write a single line of code!</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3-_Updating_the_database_using_Entity_Framework_Migrations"></a>
#### <a name="task-3--updating-the-database-using-entity-framework-migrations"></a><span data-ttu-id="b27b9-196">工作 3-使用 Entity Framework 遷移來更新資料庫</span><span class="sxs-lookup"><span data-stu-id="b27b9-196">Task 3- Updating the database using Entity Framework Migrations</span></span>

<span data-ttu-id="b27b9-197">在這項工作中，您將使用 Entity Framework 遷移來更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="b27b9-197">In this task you will update the database using Entity Framework Migrations.</span></span> <span data-ttu-id="b27b9-198">您將會發現，使用 Entity Framework 遷移功能來變更模型並反映資料庫中的變更有多簡單。</span><span class="sxs-lookup"><span data-stu-id="b27b9-198">You will discover how easy it is to change the model and reflect the changes in your databases by using the Entity Framework Migrations feature.</span></span>

1. <span data-ttu-id="b27b9-199">開啟 [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-199">Open the Package Manager Console.</span></span> <span data-ttu-id="b27b9-200">選取 [工具] > [NuGet 套件管理員] > [套件管理員主控台]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-200">Select **Tools** > **NuGet Package Manager** > **Package Manager Console**.</span></span>
2. <span data-ttu-id="b27b9-201">在 [套件管理器主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="b27b9-201">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="b27b9-202">PMC</span><span class="sxs-lookup"><span data-stu-id="b27b9-202">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample2.ps1)]

    <span data-ttu-id="b27b9-203">![啟用遷移](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "啟用移轉")</span><span class="sxs-lookup"><span data-stu-id="b27b9-203">![Enabling Migrations](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image11.png "Enabling Migrations")</span></span>

    <span data-ttu-id="b27b9-204">*啟用遷移*</span><span class="sxs-lookup"><span data-stu-id="b27b9-204">*Enabling migrations*</span></span>

    <span data-ttu-id="b27b9-205">[啟用-遷移] 命令會建立 [**遷移**] 資料夾，其中包含用來初始化資料庫的腳本。</span><span class="sxs-lookup"><span data-stu-id="b27b9-205">The Enable-Migration command creates the **Migrations** folder, which contains a script to initialize the database.</span></span>

    <span data-ttu-id="b27b9-206">![[遷移] 資料夾](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "[遷移] 資料夾")</span><span class="sxs-lookup"><span data-stu-id="b27b9-206">![Migrations folder](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image12.png "Migrations folder")</span></span>

    <span data-ttu-id="b27b9-207">*[遷移] 資料夾*</span><span class="sxs-lookup"><span data-stu-id="b27b9-207">*Migrations folder*</span></span>
3. <span data-ttu-id="b27b9-208">在 [遷移] 資料夾中開啟**Configuration.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="b27b9-208">Open the **Configuration.cs** file in the Migrations folder.</span></span> <span data-ttu-id="b27b9-209">找出類別的函式，並將**AutomaticMigrationsEnabled**值變更為*true*。</span><span class="sxs-lookup"><span data-stu-id="b27b9-209">Locate the class constructor and change the **AutomaticMigrationsEnabled** value to *true*.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample3.cs)]
4. <span data-ttu-id="b27b9-210">開啟 Person 類別，並為人員的中間名加入屬性。</span><span class="sxs-lookup"><span data-stu-id="b27b9-210">Open the Person class and add an attribute for the person's middle name.</span></span> <span data-ttu-id="b27b9-211">使用這個新屬性時，您會變更模型。</span><span class="sxs-lookup"><span data-stu-id="b27b9-211">With this new attribute, you are changing the model.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample4.cs)]
5. <span data-ttu-id="b27b9-212">選取**組建 |建立**應用程式的功能表上的 [組建方案]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-212">Select **Build | Build Solution** on the menu to build the application.</span></span>

    <span data-ttu-id="b27b9-213">![建置應用程式](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "建置應用程式")</span><span class="sxs-lookup"><span data-stu-id="b27b9-213">![Building the application](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image13.png "Building the application")</span></span>

    <span data-ttu-id="b27b9-214">*建置應用程式*</span><span class="sxs-lookup"><span data-stu-id="b27b9-214">*Building the application*</span></span>
6. <span data-ttu-id="b27b9-215">在 [套件管理器主控台] 中，輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="b27b9-215">In the Package Manager Console, enter the following command:</span></span>

    <span data-ttu-id="b27b9-216">PMC</span><span class="sxs-lookup"><span data-stu-id="b27b9-216">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample5.ps1)]

    <span data-ttu-id="b27b9-217">此命令會尋找資料物件中的變更，然後再加入必要的命令，以便據以修改資料庫。</span><span class="sxs-lookup"><span data-stu-id="b27b9-217">This command will look for changes in the data objects, and then, it will add the necessary commands to modify the database accordingly.</span></span>

    <span data-ttu-id="b27b9-218">![加入中間名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "加入中間名")</span><span class="sxs-lookup"><span data-stu-id="b27b9-218">![Adding a middle name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image14.png "Adding a middle name")</span></span>

    <span data-ttu-id="b27b9-219">*加入中間名*</span><span class="sxs-lookup"><span data-stu-id="b27b9-219">*Adding a middle name*</span></span>
7. <span data-ttu-id="b27b9-220">選擇性您可以執行下列命令，以差異更新產生 SQL 腳本。</span><span class="sxs-lookup"><span data-stu-id="b27b9-220">(Optional) You can run the following command to generate a SQL script with the differential update.</span></span> <span data-ttu-id="b27b9-221">這可讓您以手動方式更新資料庫（在此情況下不需要），或套用其他資料庫中的變更：</span><span class="sxs-lookup"><span data-stu-id="b27b9-221">This will let you update the database manually (In this case it's not necessary), or apply the changes in other databases:</span></span>

    <span data-ttu-id="b27b9-222">PMC</span><span class="sxs-lookup"><span data-stu-id="b27b9-222">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample6.ps1)]

    <span data-ttu-id="b27b9-223">![產生 SQL 腳本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "產生 SQL 指令碼")</span><span class="sxs-lookup"><span data-stu-id="b27b9-223">![Generating a SQL script](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image15.png "Generating a SQL script")</span></span>

    <span data-ttu-id="b27b9-224">*產生 SQL 腳本*</span><span class="sxs-lookup"><span data-stu-id="b27b9-224">*Generating a SQL script*</span></span>

    <span data-ttu-id="b27b9-225">![SQL 腳本更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL 腳本更新")</span><span class="sxs-lookup"><span data-stu-id="b27b9-225">![SQL Script update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image16.png "SQL Script update")</span></span>

    <span data-ttu-id="b27b9-226">*SQL 腳本更新*</span><span class="sxs-lookup"><span data-stu-id="b27b9-226">*SQL Script update*</span></span>
8. <span data-ttu-id="b27b9-227">在 [套件管理員主控台] 中，輸入下列命令以更新資料庫：</span><span class="sxs-lookup"><span data-stu-id="b27b9-227">In the Package Manager Console, enter the following command to update the database:</span></span>

    <span data-ttu-id="b27b9-228">PMC</span><span class="sxs-lookup"><span data-stu-id="b27b9-228">PMC</span></span>

    [!code-powershell[Main](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/samples/sample7.ps1)]

    <span data-ttu-id="b27b9-229">![正在更新資料庫](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "更新資料庫")</span><span class="sxs-lookup"><span data-stu-id="b27b9-229">![Updating the Database](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image17.png "Updating the Database")</span></span>

    <span data-ttu-id="b27b9-230">*正在更新資料庫*</span><span class="sxs-lookup"><span data-stu-id="b27b9-230">*Updating the Database*</span></span>

    <span data-ttu-id="b27b9-231">這會在 [**人員**] 資料表中加入**MiddleName**資料行，以符合**Person**類別的目前定義。</span><span class="sxs-lookup"><span data-stu-id="b27b9-231">This will add the **MiddleName** column in the **People** table to match the current definition of the **Person** class.</span></span>
9. <span data-ttu-id="b27b9-232">更新資料庫之後，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**新增] |** 要再次新增人員控制器的控制器（以相同的值完成）。</span><span class="sxs-lookup"><span data-stu-id="b27b9-232">Once the database is updated, right-click the Controller folder and select **Add | Controller** to add the Person controller again (Complete with the same values).</span></span> <span data-ttu-id="b27b9-233">這會更新現有的方法，並加入新的屬性。</span><span class="sxs-lookup"><span data-stu-id="b27b9-233">This will update the existing methods and views adding the new attribute.</span></span>

    <span data-ttu-id="b27b9-234">![新增控制器更新](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "新增控制器更新")</span><span class="sxs-lookup"><span data-stu-id="b27b9-234">![Adding a controller update](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image18.png "Adding a controller update")</span></span>

    <span data-ttu-id="b27b9-235">*正在更新控制器*</span><span class="sxs-lookup"><span data-stu-id="b27b9-235">*Updating the controller*</span></span>
10. <span data-ttu-id="b27b9-236">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-236">Click **Add**.</span></span> <span data-ttu-id="b27b9-237">然後，選取 [**覆寫 PersonController.cs** ] 和 [**覆寫關聯的視圖**] 的值，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="b27b9-237">Then, select the values **Overwrite PersonController.cs** and the **Overwrite associated views** and click **OK**.</span></span>

   ![新增控制器覆寫](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image19.png)

   <span data-ttu-id="b27b9-239">*正在更新控制器*</span><span class="sxs-lookup"><span data-stu-id="b27b9-239">*Updating the controller*</span></span>

<a id="Ex1Task4"></a>

<a id="Task4-_Running_the_application"></a>
#### <a name="task4--running-the-application"></a><span data-ttu-id="b27b9-240">Task4-執行應用程式</span><span class="sxs-lookup"><span data-stu-id="b27b9-240">Task4- Running the application</span></span>

1. <span data-ttu-id="b27b9-241">按 **F5** 執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="b27b9-241">Press **F5** to run the application.</span></span>
2. <span data-ttu-id="b27b9-242">開啟 **/Person**。</span><span class="sxs-lookup"><span data-stu-id="b27b9-242">Open **/Person**.</span></span> <span data-ttu-id="b27b9-243">請注意，資料已保留，但已加入「中間名」資料行。</span><span class="sxs-lookup"><span data-stu-id="b27b9-243">Notice that the data was preserved, while the middle name column was added.</span></span>

    <span data-ttu-id="b27b9-244">![已新增中間名](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "已新增中間名")</span><span class="sxs-lookup"><span data-stu-id="b27b9-244">![Middle Name added](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image20.png "Middle Name added")</span></span>

    <span data-ttu-id="b27b9-245">*已新增中間名*</span><span class="sxs-lookup"><span data-stu-id="b27b9-245">*Middle Name added*</span></span>
3. <span data-ttu-id="b27b9-246">如果您按一下 [**編輯**]，就可以將中間名加入至目前的人員。</span><span class="sxs-lookup"><span data-stu-id="b27b9-246">If you click **Edit**, you will be able to add a middle name to the current person.</span></span>

    <span data-ttu-id="b27b9-247">![中間名版本](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "中間名版本")</span><span class="sxs-lookup"><span data-stu-id="b27b9-247">![Middle Name edition](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image21.png "Middle Name edition")</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="b27b9-248">總結</span><span class="sxs-lookup"><span data-stu-id="b27b9-248">Summary</span></span>

<span data-ttu-id="b27b9-249">在這個實際操作的實驗室中，您已學到使用任何模型類別來建立 CRUD 作業與 ASP.NET MVC 4 架構的簡單步驟。</span><span class="sxs-lookup"><span data-stu-id="b27b9-249">In this Hands-On lab, you have learned simple steps to create CRUD operations with ASP.NET MVC 4 Scaffolding using any model class.</span></span> <span data-ttu-id="b27b9-250">然後，您已瞭解如何在應用程式中執行端對端更新-從資料庫到 views-使用 Entity Framework 遷移。</span><span class="sxs-lookup"><span data-stu-id="b27b9-250">Then, you have learned how to perform an end to end update in your application -from the database to the views- by using Entity Framework Migrations.</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="b27b9-251">附錄 A：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="b27b9-251">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="b27b9-252">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="b27b9-252">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="b27b9-253">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="b27b9-253">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="b27b9-254">移至 [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="b27b9-254">Go to [https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="b27b9-255">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="b27b9-255">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="b27b9-256">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-256">Click on **Install Now**.</span></span> <span data-ttu-id="b27b9-257">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="b27b9-257">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="b27b9-258">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="b27b9-258">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="b27b9-259">![安裝 Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="b27b9-259">![Install Visual Studio Express](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image22.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="b27b9-260">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="b27b9-260">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="b27b9-261">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="b27b9-261">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image23.png)

    <span data-ttu-id="b27b9-263">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="b27b9-263">*Accepting the license terms*</span></span>
5. <span data-ttu-id="b27b9-264">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="b27b9-264">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image24.png)

    <span data-ttu-id="b27b9-266">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="b27b9-266">*Installation progress*</span></span>
6. <span data-ttu-id="b27b9-267">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="b27b9-267">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image25.png)

    <span data-ttu-id="b27b9-269">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="b27b9-269">*Installation completed*</span></span>
7. <span data-ttu-id="b27b9-270">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="b27b9-270">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="b27b9-271">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="b27b9-271">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image26.png)

    <span data-ttu-id="b27b9-273">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="b27b9-273">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Using_Code_Snippets"></a>
## <a name="appendix-b-using-code-snippets"></a><span data-ttu-id="b27b9-274">附錄 B：使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="b27b9-274">Appendix B: Using Code Snippets</span></span>

<span data-ttu-id="b27b9-275">有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="b27b9-275">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="b27b9-276">實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="b27b9-276">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="b27b9-277">![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")</span><span class="sxs-lookup"><span data-stu-id="b27b9-277">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image27.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="b27b9-278">*使用 Visual Studio 程式碼片段將程式碼插入您的專案*</span><span class="sxs-lookup"><span data-stu-id="b27b9-278">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="b27b9-279">***若要使用鍵盤新增程式碼片段（C#僅限）***</span><span class="sxs-lookup"><span data-stu-id="b27b9-279">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="b27b9-280">將游標放在您想要插入程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="b27b9-280">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="b27b9-281">開始鍵入程式碼片段名稱（不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="b27b9-281">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="b27b9-282">監看 IntelliSense 會顯示相符的程式碼片段名稱。</span><span class="sxs-lookup"><span data-stu-id="b27b9-282">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="b27b9-283">選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。</span><span class="sxs-lookup"><span data-stu-id="b27b9-283">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="b27b9-284">按兩次 Tab 鍵，在游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="b27b9-284">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="b27b9-285">![開始鍵入程式碼片段名稱](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "開始鍵入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="b27b9-285">![Start typing the snippet name](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image28.png "Start typing the snippet name")</span></span>

<span data-ttu-id="b27b9-286">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="b27b9-286">*Start typing the snippet name*</span></span>

<span data-ttu-id="b27b9-287">![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="b27b9-287">![Press Tab to select the highlighted snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image29.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="b27b9-288">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="b27b9-288">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="b27b9-289">![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "再按一次 Tab 鍵，將會展開程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="b27b9-289">![Press Tab again and the snippet will expand](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image30.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="b27b9-290">*再按一次 Tab 鍵，將會展開程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="b27b9-290">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="b27b9-291">***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1.</span><span class="sxs-lookup"><span data-stu-id="b27b9-291">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="b27b9-292">以滑鼠右鍵按一下您要插入程式碼片段的位置。</span><span class="sxs-lookup"><span data-stu-id="b27b9-292">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="b27b9-293">選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。</span><span class="sxs-lookup"><span data-stu-id="b27b9-293">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="b27b9-294">按一下清單中的相關程式碼片段，即可加以選取。</span><span class="sxs-lookup"><span data-stu-id="b27b9-294">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="b27b9-295">![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")</span><span class="sxs-lookup"><span data-stu-id="b27b9-295">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image31.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="b27b9-296">*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*</span><span class="sxs-lookup"><span data-stu-id="b27b9-296">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="b27b9-297">![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "按一下清單中的相關程式碼片段，即可加以選取")</span><span class="sxs-lookup"><span data-stu-id="b27b9-297">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-entity-framework-scaffolding-and-migrations/_static/image32.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="b27b9-298">*按一下清單中的相關程式碼片段，即可加以選取*</span><span class="sxs-lookup"><span data-stu-id="b27b9-298">*Pick the relevant snippet from the list, by clicking on it*</span></span>
