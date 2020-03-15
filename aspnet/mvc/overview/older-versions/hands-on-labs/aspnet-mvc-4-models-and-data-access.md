---
uid: mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
title: ASP.NET MVC 4 模型和資料存取 |Microsoft Docs
author: rick-anderson
description: 注意：此實際操作實驗室假設您有 ASP.NET MVC 的基本知識。 如果您之前未使用過 ASP.NET MVC，建議您移至 ASP.NET MVC 4 。
ms.author: riande
ms.date: 02/18/2013
ms.assetid: 634ea84b-f904-4afe-b71b-49cccef4d9cc
msc.legacyurl: /mvc/overview/older-versions/hands-on-labs/aspnet-mvc-4-models-and-data-access
msc.type: authoredcontent
ms.openlocfilehash: 90635b617930d0a9c126795f4c8790d542e33dc9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78560197"
---
# <a name="aspnet-mvc-4-models-and-data-access"></a><span data-ttu-id="330f0-104">ASP.NET MVC 4 模型和資料存取</span><span class="sxs-lookup"><span data-stu-id="330f0-104">ASP.NET MVC 4 Models and Data Access</span></span>

<span data-ttu-id="330f0-105">依[Web Camp 團隊](https://twitter.com/webcamps)</span><span class="sxs-lookup"><span data-stu-id="330f0-105">By [Web Camps Team](https://twitter.com/webcamps)</span></span>

[<span data-ttu-id="330f0-106">下載 Web Camp 訓練套件</span><span class="sxs-lookup"><span data-stu-id="330f0-106">Download Web Camps Training Kit</span></span>](https://aka.ms/webcamps-training-kit)

<span data-ttu-id="330f0-107">這個實際操作實驗室假設您有**ASP.NET MVC**的基本知識。</span><span class="sxs-lookup"><span data-stu-id="330f0-107">This Hands-on Lab assumes you have basic knowledge of **ASP.NET MVC**.</span></span> <span data-ttu-id="330f0-108">如果您之前未使用過**ASP.NET mvc** ，建議您移至**ASP.NET mvc 4 基礎**實際操作實驗室。</span><span class="sxs-lookup"><span data-stu-id="330f0-108">If you have not used **ASP.NET MVC** before, we recommend you to go over **ASP.NET MVC 4 Fundamentals** Hands-on Lab.</span></span>

<span data-ttu-id="330f0-109">本實驗室將針對源資料夾中提供的範例 Web 應用程式套用次要變更，引導您完成先前所述的增強功能和新功能。</span><span class="sxs-lookup"><span data-stu-id="330f0-109">This lab walks you through the enhancements and new features previously described by applying minor changes to a sample Web application provided in the Source folder.</span></span>

> [!NOTE]
> <span data-ttu-id="330f0-110">所有範例程式碼和程式碼片段都包含在 Web Camp 訓練套件中，可在[Microsoft web/WebCampTrainingKit 版本](https://aka.ms/webcamps-training-kit)取得。</span><span class="sxs-lookup"><span data-stu-id="330f0-110">All sample code and snippets are included in the Web Camps Training Kit, available at [Microsoft-Web/WebCampTrainingKit Releases](https://aka.ms/webcamps-training-kit).</span></span> <span data-ttu-id="330f0-111">此實驗室的特定專案可在[ASP.NET MVC 4 模型和資料存取](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess)中取得。</span><span class="sxs-lookup"><span data-stu-id="330f0-111">The project specific to this lab is available at [ASP.NET MVC 4 Models and Data Access](https://github.com/Microsoft-Web/HOL-MVC4ModelsAndDataAccess).</span></span>

<span data-ttu-id="330f0-112">在**ASP.NET MVC 基礎**實際操作實驗室中，您已將硬式編碼的資料從控制器傳遞至 View 範本。</span><span class="sxs-lookup"><span data-stu-id="330f0-112">In **ASP.NET MVC Fundamentals** Hands-on Lab, you have been passing hard-coded data from the Controllers to the View templates.</span></span> <span data-ttu-id="330f0-113">但是，為了建立真實的 Web 應用程式，您可能會想要使用實際的資料庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-113">But, in order to build a real Web application, you might want to use a real database.</span></span>

<span data-ttu-id="330f0-114">這個實際操作實驗室將示範如何使用資料庫引擎，以儲存和抓取音樂存放區應用程式所需的資料。</span><span class="sxs-lookup"><span data-stu-id="330f0-114">This Hands-on Lab will show you how to use a database engine in order to store and retrieve the data needed for the Music Store application.</span></span> <span data-ttu-id="330f0-115">為達到此目的，您將從現有的資料庫開始，並從中建立實體資料模型。</span><span class="sxs-lookup"><span data-stu-id="330f0-115">To accomplish that, you will start with an existing database and create the Entity Data Model from it.</span></span> <span data-ttu-id="330f0-116">在此實驗室中，您將符合**Database First**的方法，以及**Code First**的方法。</span><span class="sxs-lookup"><span data-stu-id="330f0-116">Throughout this lab, you will meet the **Database First** approach as well as the **Code First** approach.</span></span>

<span data-ttu-id="330f0-117">不過，您也可以使用**Model First**方法，使用工具建立相同的模型，然後從它產生資料庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-117">However, you can also use the **Model First** approach, create the same model using the tools, and then generate the database from it.</span></span>

<span data-ttu-id="330f0-118">![Database First 與 Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First 與 Model First")</span><span class="sxs-lookup"><span data-stu-id="330f0-118">![Database First vs. Model First](aspnet-mvc-4-models-and-data-access/_static/image1.png "Database First vs. Model First")</span></span>

<span data-ttu-id="330f0-119">*Database First 與 Model First*</span><span class="sxs-lookup"><span data-stu-id="330f0-119">*Database First vs. Model First*</span></span>

<span data-ttu-id="330f0-120">產生模型之後，您將在 StoreController 中進行適當的調整，以提供存放區視圖與從資料庫取得的資料，而不是使用硬式編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="330f0-120">After generating the Model, you will make the proper adjustments in the StoreController to provide the Store Views with the data taken from the database, instead of using hard-coded data.</span></span> <span data-ttu-id="330f0-121">您不需要對視圖範本進行任何變更，因為此 StoreController 將會傳回相同的 Viewmodel 給視圖範本，不過這次資料會來自資料庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-121">You will not need to make any change to the View templates because the StoreController will be returning the same ViewModels to the View templates, although this time the data will come from the database.</span></span>

<span data-ttu-id="330f0-122">**Code First 方法**</span><span class="sxs-lookup"><span data-stu-id="330f0-122">**The Code First Approach**</span></span>

<span data-ttu-id="330f0-123">Code First 的方法可讓我們從程式碼定義模型，而不會產生通常與架構結合的類別。</span><span class="sxs-lookup"><span data-stu-id="330f0-123">The Code First approach allows us to define the model from the code without generating classes that are generally coupled with the framework.</span></span>

<span data-ttu-id="330f0-124">在 code first 中，模型物件是使用 Poco 來定義，&quot;純舊 CLR 物件&quot;。</span><span class="sxs-lookup"><span data-stu-id="330f0-124">In code first, model objects are defined with POCOs, &quot;Plain Old CLR Objects&quot;.</span></span> <span data-ttu-id="330f0-125">Poco 是簡單的純類別，沒有繼承且不會執行介面。</span><span class="sxs-lookup"><span data-stu-id="330f0-125">POCOs are simple plain classes that have no inheritance and do not implement interfaces.</span></span> <span data-ttu-id="330f0-126">我們可以自動產生資料庫，也可以使用現有的資料庫，並從程式碼產生類別對應。</span><span class="sxs-lookup"><span data-stu-id="330f0-126">We can automatically generate the database from them, or we can use an existing database and generate the class mapping from the code.</span></span>

<span data-ttu-id="330f0-127">使用這種方法的優點是，模型與持續性架構（在此案例中為 Entity Framework）保持獨立，因為 Poco 類別不會與對應架構結合。</span><span class="sxs-lookup"><span data-stu-id="330f0-127">The benefits of using this approach is that the Model remains independent from the persistence framework (in this case, Entity Framework), as the POCOs classes are not coupled with the mapping framework.</span></span>

> [!NOTE]
> <span data-ttu-id="330f0-128">這個實驗室是以 ASP.NET MVC 4 和自訂和最小化的音樂存放範例應用程式版本為基礎，只符合此實際操作實驗室中顯示的功能。</span><span class="sxs-lookup"><span data-stu-id="330f0-128">This Lab is based on ASP.NET MVC 4 and a version of the Music Store sample application customized and minimized to fit only the features shown in this Hands-On Lab.</span></span>
> 
> <span data-ttu-id="330f0-129">如果您想要流覽整個**音樂存放**教學課程應用程式，您可以在[MVC-音樂存放區](https://github.com/evilDave/MVC-Music-Store)中找到它。</span><span class="sxs-lookup"><span data-stu-id="330f0-129">If you wish to explore the whole **Music Store** tutorial application you can find it in [MVC-Music-Store](https://github.com/evilDave/MVC-Music-Store).</span></span>

<a id="Prerequisites"></a>

<a id="Prerequisites"></a>
### <a name="prerequisites"></a><span data-ttu-id="330f0-130">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="330f0-130">Prerequisites</span></span>

<span data-ttu-id="330f0-131">您必須具有下列專案，才能完成此實驗室：</span><span class="sxs-lookup"><span data-stu-id="330f0-131">You must have the following items to complete this lab:</span></span>

- <span data-ttu-id="330f0-132">適用于 Web 或上層的[Microsoft Visual Studio Express 2012](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) （如需有關如何安裝的指示，請參閱[附錄 A](#AppendixA) ）。</span><span class="sxs-lookup"><span data-stu-id="330f0-132">[Microsoft Visual Studio Express 2012 for Web](https://www.microsoft.com/visualstudio/eng/products/visual-studio-express-for-web) or superior (read [Appendix A](#AppendixA) for instructions on how to install it).</span></span>

<a id="Setup"></a>

<a id="Setup"></a>
### <a name="setup"></a><span data-ttu-id="330f0-133">安裝程式</span><span class="sxs-lookup"><span data-stu-id="330f0-133">Setup</span></span>

<span data-ttu-id="330f0-134">**安裝程式碼片段**</span><span class="sxs-lookup"><span data-stu-id="330f0-134">**Installing Code Snippets**</span></span>

<span data-ttu-id="330f0-135">為了方便起見，您將在此實驗室中管理的大部分程式碼都是以 Visual Studio 程式碼片段的形式提供。</span><span class="sxs-lookup"><span data-stu-id="330f0-135">For convenience, much of the code you will be managing along this lab is available as Visual Studio code snippets.</span></span> <span data-ttu-id="330f0-136">若要安裝程式碼片段，請執行 **.\Source\Setup\CodeSnippets.vsi**檔案。</span><span class="sxs-lookup"><span data-stu-id="330f0-136">To install the code snippets run **.\Source\Setup\CodeSnippets.vsi** file.</span></span>

<span data-ttu-id="330f0-137">如果您不熟悉 Visual Studio Code 程式碼片段，而且想要瞭解如何使用，您可以參閱本檔中的附錄 &quot;[附錄 C：使用程式碼片段](#AppendixC)&quot;。</span><span class="sxs-lookup"><span data-stu-id="330f0-137">If you are not familiar with the Visual Studio Code Snippets, and want to learn how to use them, you can refer to the appendix from this document &quot;[Appendix C: Using Code Snippets](#AppendixC)&quot;.</span></span>

---

<a id="Exercises"></a>

<a id="Exercises"></a>
## <a name="exercises"></a><span data-ttu-id="330f0-138">練習</span><span class="sxs-lookup"><span data-stu-id="330f0-138">Exercises</span></span>

<span data-ttu-id="330f0-139">這個實際操作實驗室是由下列練習所組成：</span><span class="sxs-lookup"><span data-stu-id="330f0-139">This Hands-on Lab is comprised by the following exercises:</span></span>

1. [<span data-ttu-id="330f0-140">練習1：加入資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-140">Exercise 1: Adding a Database</span></span>](#Exercise1)
2. [<span data-ttu-id="330f0-141">練習2：使用 Code First 建立資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-141">Exercise 2: Creating a Database using Code First</span></span>](#Exercise2)
3. [<span data-ttu-id="330f0-142">練習3：使用參數查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-142">Exercise 3: Querying the Database with Parameters</span></span>](#Exercise3)

> [!NOTE]
> <span data-ttu-id="330f0-143">每個練習都會伴隨一個**結束**資料夾，其中包含您在完成練習之後應該取得的結果解決方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-143">Each exercise is accompanied by an **End** folder containing the resulting solution you should obtain after completing the exercises.</span></span> <span data-ttu-id="330f0-144">如果您需要額外的協助來進行練習，您可以使用此解決方案做為指南。</span><span class="sxs-lookup"><span data-stu-id="330f0-144">You can use this solution as a guide if you need additional help working through the exercises.</span></span>

<span data-ttu-id="330f0-145">完成此實驗室的預估時間： **35 分鐘**。</span><span class="sxs-lookup"><span data-stu-id="330f0-145">Estimated time to complete this lab: **35 minutes**.</span></span>

<a id="Exercise1"></a>

<a id="Exercise_1_Adding_a_Database"></a>
### <a name="exercise-1-adding-a-database"></a><span data-ttu-id="330f0-146">練習1：加入資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-146">Exercise 1: Adding a Database</span></span>

<span data-ttu-id="330f0-147">在此練習中，您將瞭解如何將具有 MusicStore 應用程式資料表的資料庫新增至方案，以便取用其資料。</span><span class="sxs-lookup"><span data-stu-id="330f0-147">In this exercise, you will learn how to add a database with the tables of the MusicStore application to the solution in order to consume its data.</span></span> <span data-ttu-id="330f0-148">一旦使用模型產生資料庫，並將其加入至方案，您就會修改 StoreController 類別，以提供具有從資料庫取得之資料的視圖範本，而不是使用硬式編碼的值。</span><span class="sxs-lookup"><span data-stu-id="330f0-148">Once the database is generated with the model, and added to the solution, you will modify the StoreController class to provide the View template with the data taken from the database, instead of using hard-coded values.</span></span>

<a id="Ex1Task1"></a>

<a id="Task_1_-_Adding_a_Database"></a>
#### <a name="task-1---adding-a-database"></a><span data-ttu-id="330f0-149">工作 1-加入資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-149">Task 1 - Adding a Database</span></span>

<span data-ttu-id="330f0-150">在這項工作中，您會將已建立的資料庫（其中包含 MusicStore 應用程式的主資料表）新增至方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-150">In this task, you will add an already created database with the main tables of the MusicStore application to the solution.</span></span>

1. <span data-ttu-id="330f0-151">開啟位於**來源/Ex1-AddingADatabaseDBFirst/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-151">Open the **Begin** solution located at **Source/Ex1-AddingADatabaseDBFirst/Begin/** folder.</span></span>

   1. <span data-ttu-id="330f0-152">在繼續之前，您必須先下載一些遺漏的 NuGet 套件。</span><span class="sxs-lookup"><span data-stu-id="330f0-152">You will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="330f0-153">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-153">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="330f0-154">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="330f0-154">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="330f0-155">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-155">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="330f0-156">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="330f0-156">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="330f0-157">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-157">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="330f0-158">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="330f0-158">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="330f0-159">新增**MvcMusicStore**資料庫檔案。</span><span class="sxs-lookup"><span data-stu-id="330f0-159">Add **MvcMusicStore** database file.</span></span> <span data-ttu-id="330f0-160">在這個實際操作的實驗室中，您將使用已建立的資料庫，稱為**MvcMusicStore**。</span><span class="sxs-lookup"><span data-stu-id="330f0-160">In this Hands-on Lab, you will use an already created database called **MvcMusicStore.mdf**.</span></span> <span data-ttu-id="330f0-161">若要這麼做，請以滑鼠右鍵按一下 [**應用程式\_資料**資料夾]，指向 [**加入**]，然後按一下 [**現有專案**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-161">To do that, right-click **App\_Data** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="330f0-162">流覽至 **\Source\Assets** ，然後選取 [ **MvcMusicStore** ] 檔案。</span><span class="sxs-lookup"><span data-stu-id="330f0-162">Browse to **\Source\Assets** and select the **MvcMusicStore.mdf** file.</span></span>

    <span data-ttu-id="330f0-163">![加入現有的專案](aspnet-mvc-4-models-and-data-access/_static/image2.png "加入現有的專案")</span><span class="sxs-lookup"><span data-stu-id="330f0-163">![Adding an Existing Item](aspnet-mvc-4-models-and-data-access/_static/image2.png "Adding an Existing Item")</span></span>

    <span data-ttu-id="330f0-164">*加入現有的專案*</span><span class="sxs-lookup"><span data-stu-id="330f0-164">*Adding an Existing Item*</span></span>

    <span data-ttu-id="330f0-165">![MvcMusicStore .mdf 資料庫檔案](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore .mdf 資料庫檔案")</span><span class="sxs-lookup"><span data-stu-id="330f0-165">![MvcMusicStore.mdf database file](aspnet-mvc-4-models-and-data-access/_static/image3.png "MvcMusicStore.mdf database file")</span></span>

    <span data-ttu-id="330f0-166">*MvcMusicStore .mdf 資料庫檔案*</span><span class="sxs-lookup"><span data-stu-id="330f0-166">*MvcMusicStore.mdf database file*</span></span>

    <span data-ttu-id="330f0-167">資料庫已加入至專案。</span><span class="sxs-lookup"><span data-stu-id="330f0-167">The database has been added to the project.</span></span> <span data-ttu-id="330f0-168">即使資料庫位於方案內部，您仍可以查詢並更新它裝載于不同的資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="330f0-168">Even when the database is located inside the solution, you can query and update it as it was hosted in a different database server.</span></span>

    <span data-ttu-id="330f0-169">![方案總管中的 MvcMusicStore 資料庫](aspnet-mvc-4-models-and-data-access/_static/image4.png "方案總管中的 MvcMusicStore 資料庫")</span><span class="sxs-lookup"><span data-stu-id="330f0-169">![MvcMusicStore database in Solution Explorer](aspnet-mvc-4-models-and-data-access/_static/image4.png "MvcMusicStore database in Solution Explorer")</span></span>

    <span data-ttu-id="330f0-170">*方案總管中的 MvcMusicStore 資料庫*</span><span class="sxs-lookup"><span data-stu-id="330f0-170">*MvcMusicStore database in Solution Explorer*</span></span>
3. <span data-ttu-id="330f0-171">驗證與資料庫的連接。</span><span class="sxs-lookup"><span data-stu-id="330f0-171">Verify the connection to the database.</span></span> <span data-ttu-id="330f0-172">若要這麼做，請按兩下 [ **MvcMusicStore** ] 以建立連接。</span><span class="sxs-lookup"><span data-stu-id="330f0-172">To do this, double-click **MvcMusicStore.mdf** to establish a connection.</span></span>

    <span data-ttu-id="330f0-173">![連接到 MvcMusicStore .mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "連接到 MvcMusicStore .mdf")</span><span class="sxs-lookup"><span data-stu-id="330f0-173">![Connecting to MvcMusicStore.mdf](aspnet-mvc-4-models-and-data-access/_static/image5.png "Connecting to MvcMusicStore.mdf")</span></span>

    <span data-ttu-id="330f0-174">*連接到 MvcMusicStore .mdf*</span><span class="sxs-lookup"><span data-stu-id="330f0-174">*Connecting to MvcMusicStore.mdf*</span></span>

<a id="Ex1Task2"></a>

<a id="Task_2_-_Creating_a_Data_Model"></a>
#### <a name="task-2---creating-a-data-model"></a><span data-ttu-id="330f0-175">工作 2-建立資料模型</span><span class="sxs-lookup"><span data-stu-id="330f0-175">Task 2 - Creating a Data Model</span></span>

<span data-ttu-id="330f0-176">在這項工作中，您將建立資料模型，以與上一個工作中新增的資料庫互動。</span><span class="sxs-lookup"><span data-stu-id="330f0-176">In this task, you will create a data model to interact with the database added in the previous task.</span></span>

1. <span data-ttu-id="330f0-177">建立將代表資料庫的資料模型。</span><span class="sxs-lookup"><span data-stu-id="330f0-177">Create a data model that will represent the database.</span></span> <span data-ttu-id="330f0-178">若要這麼做，請在方案總管以滑鼠右鍵按一下 [**模型**] 資料夾，指向 [**加入**]，然後按一下 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-178">To do this, in Solution Explorer right-click the **Models** folder, point to **Add** and then click **New Item**.</span></span> <span data-ttu-id="330f0-179">在 **加入新專案** 對話方塊中，選取 **資料** 範本，然後**ADO.NET 實體資料模型**專案。</span><span class="sxs-lookup"><span data-stu-id="330f0-179">In the **Add New Item** dialog, select the **Data** template and then the **ADO.NET Entity Data Model** item.</span></span> <span data-ttu-id="330f0-180">將資料模型名稱變更為**StoreDB** ，然後按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-180">Change the data model name to **StoreDB.edmx** and click **Add**.</span></span>

    <span data-ttu-id="330f0-181">![新增 StoreDB ADO.NET 實體資料模型](aspnet-mvc-4-models-and-data-access/_static/image6.png "新增 StoreDB ADO.NET 實體資料模型")</span><span class="sxs-lookup"><span data-stu-id="330f0-181">![Adding the StoreDB ADO.NET Entity Data Model](aspnet-mvc-4-models-and-data-access/_static/image6.png "Adding the StoreDB ADO.NET Entity Data Model")</span></span>

    <span data-ttu-id="330f0-182">*新增 StoreDB ADO.NET 實體資料模型*</span><span class="sxs-lookup"><span data-stu-id="330f0-182">*Adding the StoreDB ADO.NET Entity Data Model*</span></span>
2. <span data-ttu-id="330f0-183">[**實體資料模型 Wizard]** 隨即出現。</span><span class="sxs-lookup"><span data-stu-id="330f0-183">The **Entity Data Model Wizard** will appear.</span></span> <span data-ttu-id="330f0-184">此 wizard 會引導您建立模型層。</span><span class="sxs-lookup"><span data-stu-id="330f0-184">This wizard will guide you through the creation of the model layer.</span></span> <span data-ttu-id="330f0-185">因為模型應該根據最近新增的現有資料庫來建立，所以請選取 [**從資料庫產生**]，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-185">Since the model should be created based on the existing database recently added, select **Generate from database** and click **Next**.</span></span>

    <span data-ttu-id="330f0-186">![選擇模型內容](aspnet-mvc-4-models-and-data-access/_static/image7.png "選擇模型內容")</span><span class="sxs-lookup"><span data-stu-id="330f0-186">![Choosing the model content](aspnet-mvc-4-models-and-data-access/_static/image7.png "Choosing the model content")</span></span>

    <span data-ttu-id="330f0-187">*選擇模型內容*</span><span class="sxs-lookup"><span data-stu-id="330f0-187">*Choosing the model content*</span></span>
3. <span data-ttu-id="330f0-188">由於您是從資料庫產生模型，因此您必須指定要使用的連接。</span><span class="sxs-lookup"><span data-stu-id="330f0-188">Since you are generating a model from a database, you will need to specify the connection to use.</span></span> <span data-ttu-id="330f0-189">按一下 [**新增連接**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-189">Click **New Connection**.</span></span>
4. <span data-ttu-id="330f0-190">選取 [ **Microsoft SQL Server 資料庫**檔案]，然後按一下 [**繼續**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-190">Select **Microsoft SQL Server Database File** and click **Continue**.</span></span>

    <span data-ttu-id="330f0-191">![選擇資料來源](aspnet-mvc-4-models-and-data-access/_static/image8.png "選擇資料來源")</span><span class="sxs-lookup"><span data-stu-id="330f0-191">![Choose data source](aspnet-mvc-4-models-and-data-access/_static/image8.png "Choose data source")</span></span>

    <span data-ttu-id="330f0-192">*[選擇資料來源] 對話方塊*</span><span class="sxs-lookup"><span data-stu-id="330f0-192">*Choose data source dialog*</span></span>
5. <span data-ttu-id="330f0-193">按一下 **[流覽]** 並選取位於**應用程式\_Data**資料夾中的資料庫**MvcMusicStore** ，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-193">Click **Browse** and select the database **MvcMusicStore.mdf** you located in the **App\_Data** folder and click **OK**.</span></span>

    <span data-ttu-id="330f0-194">![連接屬性](aspnet-mvc-4-models-and-data-access/_static/image9.png "連線內容")</span><span class="sxs-lookup"><span data-stu-id="330f0-194">![Connection properties](aspnet-mvc-4-models-and-data-access/_static/image9.png "Connection properties")</span></span>

    <span data-ttu-id="330f0-195">*連接屬性*</span><span class="sxs-lookup"><span data-stu-id="330f0-195">*Connection properties*</span></span>
6. <span data-ttu-id="330f0-196">產生的類別應該與實體連接字串具有相同的名稱，因此請將其名稱變更為**MusicStoreEntities** ，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-196">The generated class should have the same name as the entity connection string, so change its name to **MusicStoreEntities** and click **Next**.</span></span>

    <span data-ttu-id="330f0-197">![選擇資料連線](aspnet-mvc-4-models-and-data-access/_static/image10.png "選擇資料連線")</span><span class="sxs-lookup"><span data-stu-id="330f0-197">![Choosing the data connection](aspnet-mvc-4-models-and-data-access/_static/image10.png "Choosing the data connection")</span></span>

    <span data-ttu-id="330f0-198">*選擇資料連線*</span><span class="sxs-lookup"><span data-stu-id="330f0-198">*Choosing the data connection*</span></span>
7. <span data-ttu-id="330f0-199">選擇要使用的資料庫物件。</span><span class="sxs-lookup"><span data-stu-id="330f0-199">Choose the database objects to use.</span></span> <span data-ttu-id="330f0-200">當實體模型只會使用資料庫的資料表時，請選取 [**資料表]** 選項，並確定也已選取 [在**模型中包含外鍵資料行**] 和 [將複數化] 或 [單數化] [**產生的物件名稱**] 選項。</span><span class="sxs-lookup"><span data-stu-id="330f0-200">As the Entity Model will use just the database's tables, select the **Tables** option, and make sure that the **Include foreign key columns in the model** and **Pluralize or singularize generated object names** options are also selected.</span></span> <span data-ttu-id="330f0-201">將 [模型命名空間] 變更為**MvcMusicStore** ，然後按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-201">Change the Model Namespace to **MvcMusicStore.Model** and click **Finish**.</span></span>

    <span data-ttu-id="330f0-202">![選擇資料庫物件](aspnet-mvc-4-models-and-data-access/_static/image11.png "選擇資料庫物件")</span><span class="sxs-lookup"><span data-stu-id="330f0-202">![Choosing the database objects](aspnet-mvc-4-models-and-data-access/_static/image11.png "Choosing the database objects")</span></span>

    <span data-ttu-id="330f0-203">*選擇資料庫物件*</span><span class="sxs-lookup"><span data-stu-id="330f0-203">*Choosing the database objects*</span></span>

    > [!NOTE]
    > <span data-ttu-id="330f0-204">如果顯示 [安全性警告] 對話方塊，請按一下 **[確定]** 以執行範本，並產生模型實體的類別。</span><span class="sxs-lookup"><span data-stu-id="330f0-204">If a Security Warning dialog is shown, click **OK** to run the template and generate the classes for the model entities.</span></span>
8. <span data-ttu-id="330f0-205">資料庫的實體圖表將會出現，而會建立對應每個資料表到資料庫的個別類別。</span><span class="sxs-lookup"><span data-stu-id="330f0-205">An entity diagram for the database will appear, while a separate class that maps each table to the database will be created.</span></span> <span data-ttu-id="330f0-206">例如，**專輯**資料表會以**專輯**類別表示，而資料表中的每個資料行都會對應至類別屬性。</span><span class="sxs-lookup"><span data-stu-id="330f0-206">For example, the **Albums** table will be represented by an **Album** class, where each column in the table will map to a class property.</span></span> <span data-ttu-id="330f0-207">這可讓您查詢和使用代表資料庫中資料列的物件。</span><span class="sxs-lookup"><span data-stu-id="330f0-207">This will allow you to query and work with objects that represent rows in the database.</span></span>

    <span data-ttu-id="330f0-208">![實體圖表](aspnet-mvc-4-models-and-data-access/_static/image12.png "實體圖表")</span><span class="sxs-lookup"><span data-stu-id="330f0-208">![Entity diagram](aspnet-mvc-4-models-and-data-access/_static/image12.png "Entity diagram")</span></span>

    <span data-ttu-id="330f0-209">*實體圖表*</span><span class="sxs-lookup"><span data-stu-id="330f0-209">*Entity diagram*</span></span>

    > [!NOTE]
    > <span data-ttu-id="330f0-210">T4 範本（tt）會執行程式碼來產生實體類別，並會覆寫具有相同名稱的現有類別。</span><span class="sxs-lookup"><span data-stu-id="330f0-210">The T4 templates (.tt) run code to generate the entities classes and will overwrite the existing classes with the same name.</span></span> <span data-ttu-id="330f0-211">在此範例中，&quot;專輯&quot;的類別、&quot;內容類型&quot; 和 &quot;演出者&quot; 會被產生的程式碼覆寫。</span><span class="sxs-lookup"><span data-stu-id="330f0-211">In this example, the classes &quot;Album&quot;, &quot;Genre&quot; and &quot;Artist&quot; were overwritten with the generated code.</span></span>

<a id="Ex1Task3"></a>

<a id="Task_3_-_Building_the_Application"></a>
#### <a name="task-3---building-the-application"></a><span data-ttu-id="330f0-212">工作 3-建立應用程式</span><span class="sxs-lookup"><span data-stu-id="330f0-212">Task 3 - Building the Application</span></span>

<span data-ttu-id="330f0-213">在這項工作中，您將會檢查，雖然模型產生已移除**專輯**、內容**類型和** **演出者**模型類別，但已使用新的資料模型類別成功建立專案。</span><span class="sxs-lookup"><span data-stu-id="330f0-213">In this task, you will check that, although the model generation have removed the **Album**, **Genre** and **Artist** model classes, the project builds successfully by using the new data model classes.</span></span>

1. <span data-ttu-id="330f0-214">建立專案，方法是選取 [**建立**] 功能表項目，然後選取 [**建立 MvcMusicStore**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-214">Build the project by selecting the **Build** menu item and then **Build MvcMusicStore**.</span></span>

    <span data-ttu-id="330f0-215">![建立專案](aspnet-mvc-4-models-and-data-access/_static/image13.png "建立專案")</span><span class="sxs-lookup"><span data-stu-id="330f0-215">![Building the project](aspnet-mvc-4-models-and-data-access/_static/image13.png "Building the project")</span></span>

    <span data-ttu-id="330f0-216">*建立專案*</span><span class="sxs-lookup"><span data-stu-id="330f0-216">*Building the project*</span></span>
2. <span data-ttu-id="330f0-217">已成功建立專案。</span><span class="sxs-lookup"><span data-stu-id="330f0-217">The project builds successfully.</span></span> <span data-ttu-id="330f0-218">為什麼它仍然有效？</span><span class="sxs-lookup"><span data-stu-id="330f0-218">Why does it still work?</span></span> <span data-ttu-id="330f0-219">其運作方式是因為資料庫資料表具有欄位，其中包含您在已移除的類別**專輯** **和內容**類型中使用的屬性。</span><span class="sxs-lookup"><span data-stu-id="330f0-219">It works because the database tables have fields that include the properties that you were using in the removed classes **Album** and **Genre**.</span></span>

    <span data-ttu-id="330f0-220">![組建成功](aspnet-mvc-4-models-and-data-access/_static/image14.png "組建成功")</span><span class="sxs-lookup"><span data-stu-id="330f0-220">![Builds succeeded](aspnet-mvc-4-models-and-data-access/_static/image14.png "Builds succeeded")</span></span>

    <span data-ttu-id="330f0-221">*組建成功*</span><span class="sxs-lookup"><span data-stu-id="330f0-221">*Builds succeeded*</span></span>
3. <span data-ttu-id="330f0-222">雖然設計工具會以圖表格式顯示實體，但它們實際上C#是類別。</span><span class="sxs-lookup"><span data-stu-id="330f0-222">While the designer displays the entities in a diagram format, they are really C# classes.</span></span> <span data-ttu-id="330f0-223">在方案總管中展開 [ **StoreDB** ] 節點，然後在**StoreDB.tt**中，您會看到新產生的實體。</span><span class="sxs-lookup"><span data-stu-id="330f0-223">Expand the **StoreDB.edmx** node in the Solution Explorer and then **StoreDB.tt**, you will see the new generated entities.</span></span>

    <span data-ttu-id="330f0-224">![產生的檔案](aspnet-mvc-4-models-and-data-access/_static/image15.png "產生的檔案")</span><span class="sxs-lookup"><span data-stu-id="330f0-224">![Generated files](aspnet-mvc-4-models-and-data-access/_static/image15.png "Generated files")</span></span>

    <span data-ttu-id="330f0-225">*產生的檔案*</span><span class="sxs-lookup"><span data-stu-id="330f0-225">*Generated files*</span></span>

<a id="Ex1Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="330f0-226">工作 4-查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-226">Task 4 - Querying the Database</span></span>

<span data-ttu-id="330f0-227">在這項工作中，您將更新 StoreController 類別，如此一來，它就會查詢資料庫以取得資訊，而不是使用硬式編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="330f0-227">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will query the database to retrieve the information.</span></span>

1. <span data-ttu-id="330f0-228">開啟**Controllers\StoreController.cs** ，並將下欄欄位新增至類別，以保存**MusicStoreEntities**類別的實例，名為**storeDB**：</span><span class="sxs-lookup"><span data-stu-id="330f0-228">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="330f0-229">（程式碼片段-*模型和資料存取-Ex1 storeDB*）</span><span class="sxs-lookup"><span data-stu-id="330f0-229">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample1.cs)]
2. <span data-ttu-id="330f0-230">**MusicStoreEntities**類別會針對資料庫中的每個資料表公開集合屬性。</span><span class="sxs-lookup"><span data-stu-id="330f0-230">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="330f0-231">更新**流覽**動作方法，以取得所有**專輯**的內容類型。</span><span class="sxs-lookup"><span data-stu-id="330f0-231">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="330f0-232">（程式碼片段-*模型和資料存取-Ex1 存放區流覽*）</span><span class="sxs-lookup"><span data-stu-id="330f0-232">(Code Snippet - *Models And Data Access - Ex1 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample2.cs)]

    > [!NOTE]
    > <span data-ttu-id="330f0-233">您會使用稱為**LINQ** （語言整合式查詢）的 .net 功能，針對這些集合撰寫強型別查詢運算式-這將會針對資料庫執行程式碼，並傳回您可以對其進行程式設計的物件。</span><span class="sxs-lookup"><span data-stu-id="330f0-233">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="330f0-234">如需 LINQ 的詳細資訊，請造訪[msdn 網站](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="330f0-234">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926&amp;#040;v=vs.110&amp;#041;.aspx).</span></span>
3. <span data-ttu-id="330f0-235">更新**索引**動作方法，以取得所有內容內容。</span><span class="sxs-lookup"><span data-stu-id="330f0-235">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="330f0-236">（程式碼片段-*模型和資料存取-Ex1 存放區索引*）</span><span class="sxs-lookup"><span data-stu-id="330f0-236">(Code Snippet - *Models And Data Access - Ex1 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample3.cs)]
4. <span data-ttu-id="330f0-237">更新**索引**動作方法以抓取所有內容，並將集合轉換為清單。</span><span class="sxs-lookup"><span data-stu-id="330f0-237">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="330f0-238">（程式碼片段-*模型和資料存取-Ex1 Store GenreMenu*）</span><span class="sxs-lookup"><span data-stu-id="330f0-238">(Code Snippet - *Models And Data Access - Ex1 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample4.cs)]

<a id="Ex1Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="330f0-239">工作 5-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="330f0-239">Task 5 - Running the Application</span></span>

<span data-ttu-id="330f0-240">在這項工作中，您將檢查 [存放區索引] 頁面現在會顯示儲存在資料庫中的內容，而不是硬式編碼的內容。</span><span class="sxs-lookup"><span data-stu-id="330f0-240">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="330f0-241">不需要變更 View 範本，因為**StoreController**會傳回與之前相同的實體，不過這次資料會來自資料庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-241">There is no need to change the View template because the **StoreController** is returning the same entities as before, although this time the data will come from the database.</span></span>

1. <span data-ttu-id="330f0-242">重建方案，然後按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="330f0-242">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="330f0-243">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="330f0-243">The project starts in the Home page.</span></span> <span data-ttu-id="330f0-244">確認 [內容類型] 功能表**不再是 [** 硬式編碼] 清單，而且資料是從資料庫中直接抓取。</span><span class="sxs-lookup"><span data-stu-id="330f0-244">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image16.png)

    <span data-ttu-id="330f0-246">*從資料庫流覽內容內容*</span><span class="sxs-lookup"><span data-stu-id="330f0-246">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="330f0-247">現在，流覽至任何內容類型，並確認專輯已從資料庫中填入。</span><span class="sxs-lookup"><span data-stu-id="330f0-247">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="330f0-248">![從資料庫流覽專輯](aspnet-mvc-4-models-and-data-access/_static/image17.png "從資料庫流覽專輯")</span><span class="sxs-lookup"><span data-stu-id="330f0-248">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image17.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="330f0-249">*從資料庫流覽專輯*</span><span class="sxs-lookup"><span data-stu-id="330f0-249">*Browsing Albums from the database*</span></span>

<a id="Exercise2"></a>

<a id="Exercise_2_Creating_a_Database_Using_Code_First"></a>
### <a name="exercise-2-creating-a-database-using-code-first"></a><span data-ttu-id="330f0-250">練習2：使用 Code First 建立資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-250">Exercise 2: Creating a Database Using Code First</span></span>

<span data-ttu-id="330f0-251">在此練習中，您將瞭解如何使用 Code First 的方法，以 MusicStore 應用程式的資料表來建立資料庫，以及如何存取其資料。</span><span class="sxs-lookup"><span data-stu-id="330f0-251">In this exercise, you will learn how to use the Code First approach to create a database with the tables of the MusicStore application, and how to access its data.</span></span>

<span data-ttu-id="330f0-252">產生模型之後，您將修改 StoreController，以提供具有從資料庫取得之資料的視圖範本，而不是使用硬式編碼的值。</span><span class="sxs-lookup"><span data-stu-id="330f0-252">Once the model is generated, you will modify the StoreController to provide the View template with the data taken from the database, instead of using hardcoded values.</span></span>

> [!NOTE]
> <span data-ttu-id="330f0-253">如果您已完成練習1，而且已經使用 Database First 的方法，您現在將瞭解如何使用不同的程式來取得相同的結果。</span><span class="sxs-lookup"><span data-stu-id="330f0-253">If you have completed Exercise 1 and have already worked with the Database First approach, you will now learn how to get the same results with a different process.</span></span> <span data-ttu-id="330f0-254">在練習1中共通的工作已標示為可讓您更輕鬆閱讀。</span><span class="sxs-lookup"><span data-stu-id="330f0-254">The tasks that are in common with Exercise 1 have been marked to make your reading easier.</span></span> <span data-ttu-id="330f0-255">如果您尚未完成練習1，但想要學習 Code First 的方法，您可以從這個練習著手，取得主題的完整涵蓋範圍。</span><span class="sxs-lookup"><span data-stu-id="330f0-255">If you have not completed Exercise 1 but would like to learn the Code First approach, you can start from this exercise and get a full coverage of the topic.</span></span>

<a id="Ex2Task1"></a>

<a id="Task_1_-_Populating_Sample_Data"></a>
#### <a name="task-1---populating-sample-data"></a><span data-ttu-id="330f0-256">工作 1-填入範例資料</span><span class="sxs-lookup"><span data-stu-id="330f0-256">Task 1 - Populating Sample Data</span></span>

<span data-ttu-id="330f0-257">在這項工作中，您會在資料庫最初使用程式碼優先建立時，將範例資料填入其中。</span><span class="sxs-lookup"><span data-stu-id="330f0-257">In this task, you will populate the database with sample data when it is initially created using Code-First.</span></span>

1. <span data-ttu-id="330f0-258">開啟位於**來源/Ex2-CreatingADatabaseCodeFirst/開始/** 資料夾的 [**開始**] 解決方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-258">Open the **Begin** solution located at **Source/Ex2-CreatingADatabaseCodeFirst/Begin/** folder.</span></span> <span data-ttu-id="330f0-259">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-259">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="330f0-260">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="330f0-260">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="330f0-261">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-261">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="330f0-262">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="330f0-262">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="330f0-263">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-263">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="330f0-264">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="330f0-264">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="330f0-265">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-265">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="330f0-266">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="330f0-266">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="330f0-267">將**SampleData.cs**檔案新增至 [**模型**] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="330f0-267">Add the **SampleData.cs** file to the **Models** folder.</span></span> <span data-ttu-id="330f0-268">若要這麼做，請以滑鼠右鍵按一下 [**模型**] 資料夾，指向 [**加入**]，然後按一下 [**現有專案**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-268">To do that, right-click **Models** folder, point to **Add** and then click **Existing Item**.</span></span> <span data-ttu-id="330f0-269">流覽至 **\Source\Assets** ，然後選取**SampleData.cs**檔案。</span><span class="sxs-lookup"><span data-stu-id="330f0-269">Browse to **\Source\Assets** and select the **SampleData.cs** file.</span></span>

    <span data-ttu-id="330f0-270">![範例資料填入程式碼](aspnet-mvc-4-models-and-data-access/_static/image18.png "範例資料填入程式碼")</span><span class="sxs-lookup"><span data-stu-id="330f0-270">![Sample data populate code](aspnet-mvc-4-models-and-data-access/_static/image18.png "Sample data populate code")</span></span>

    <span data-ttu-id="330f0-271">*範例資料填入程式碼*</span><span class="sxs-lookup"><span data-stu-id="330f0-271">*Sample data populate code*</span></span>
3. <span data-ttu-id="330f0-272">開啟**Global.asax.cs**檔案，並新增下列*using*語句。</span><span class="sxs-lookup"><span data-stu-id="330f0-272">Open the **Global.asax.cs** file and add the following *using* statements.</span></span>

    <span data-ttu-id="330f0-273">（程式碼片段-*模型和資料存取-Ex2 Global Global.asax using*）</span><span class="sxs-lookup"><span data-stu-id="330f0-273">(Code Snippet - *Models And Data Access - Ex2 Global Asax Usings*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample5.cs)]
4. <span data-ttu-id="330f0-274">在**應用程式\_Start （）** 方法中，加入下列這一行來設定資料庫初始化運算式。</span><span class="sxs-lookup"><span data-stu-id="330f0-274">In the **Application\_Start()** method add the following line to set the database initializer.</span></span>

    <span data-ttu-id="330f0-275">（程式碼片段-*模型和資料存取-Ex2 Global Global.asax SetInitializer*）</span><span class="sxs-lookup"><span data-stu-id="330f0-275">(Code Snippet - *Models And Data Access - Ex2 Global Asax SetInitializer*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample6.cs)]

<a id="Ex2Task2"></a>

<a id="Task_2_-_Configuring_the_connection_to_the_Database"></a>
#### <a name="task-2---configuring-the-connection-to-the-database"></a><span data-ttu-id="330f0-276">工作 2-設定與資料庫的連接</span><span class="sxs-lookup"><span data-stu-id="330f0-276">Task 2 - Configuring the connection to the Database</span></span>

<span data-ttu-id="330f0-277">既然您已經將資料庫加入至專案，您就會**在 web.config 檔案**中寫入連接字串。</span><span class="sxs-lookup"><span data-stu-id="330f0-277">Now that you have already added a database to our project, you will write in the **Web.config** file the connection string.</span></span>

1. <span data-ttu-id="330f0-278">在 web.config 新增連接字串 **。** 若要這麼做，請在專案根目錄開啟**web.config** ，並在 **&lt;connectionStrings&gt;** 區段中，將名為 DefaultConnection 的連接字串取代為這一行：</span><span class="sxs-lookup"><span data-stu-id="330f0-278">Add a connection string at **Web.config**. To do that, open **Web.config** at project root and replace the connection string named DefaultConnection with this line in the **&lt;connectionStrings&gt;** section:</span></span>

    <span data-ttu-id="330f0-279">![Web.config 檔案位置](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config 檔案位置")</span><span class="sxs-lookup"><span data-stu-id="330f0-279">![Web.config file location](aspnet-mvc-4-models-and-data-access/_static/image19.png "Web.config file location")</span></span>

    <span data-ttu-id="330f0-280">*Web.config 檔案位置*</span><span class="sxs-lookup"><span data-stu-id="330f0-280">*Web.config file location*</span></span>

    [!code-xml[Main](aspnet-mvc-4-models-and-data-access/samples/sample7.xml)]

<a id="Ex2Task3"></a>

<a id="Task_3_-_Working_with_the_Model"></a>
#### <a name="task-3---working-with-the-model"></a><span data-ttu-id="330f0-281">工作 3-使用模型</span><span class="sxs-lookup"><span data-stu-id="330f0-281">Task 3 - Working with the Model</span></span>

<span data-ttu-id="330f0-282">既然您已經設定資料庫的連接，就會將此模型與資料庫資料表連結。</span><span class="sxs-lookup"><span data-stu-id="330f0-282">Now that you have already configured the connection to the database, you will link the model with the database tables.</span></span> <span data-ttu-id="330f0-283">在這項工作中，您將建立一個類別，它會使用 Code First 連結到資料庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-283">In this task, you will create a class that will be linked to the database with Code First.</span></span> <span data-ttu-id="330f0-284">請記住，有一個應該修改的 POCO 模型類別存在。</span><span class="sxs-lookup"><span data-stu-id="330f0-284">Remember that there is an existent POCO model class that should be modified.</span></span>

> [!NOTE]
> <span data-ttu-id="330f0-285">如果您已完成練習1，您會注意到這個步驟是由嚮導執行。</span><span class="sxs-lookup"><span data-stu-id="330f0-285">If you completed Exercise 1, you will note that this step was performed by a wizard.</span></span> <span data-ttu-id="330f0-286">藉由執行 Code First，您將以手動方式建立將連結至資料實體的類別。</span><span class="sxs-lookup"><span data-stu-id="330f0-286">By doing Code First, you will manually create classes that will be linked to data entities.</span></span>

1. <span data-ttu-id="330f0-287">從**模型**專案資料夾開啟 POCO 模型類別內容類型，並包含識別碼。</span><span class="sxs-lookup"><span data-stu-id="330f0-287">Open the POCO model class **Genre** from **Models** project folder and include an ID.</span></span> <span data-ttu-id="330f0-288">使用名稱為**GenreId**的 int 屬性。</span><span class="sxs-lookup"><span data-stu-id="330f0-288">Use an int property with the name **GenreId**.</span></span>

    <span data-ttu-id="330f0-289">（程式碼片段-*模型和資料存取-Ex2 Code First*內容類型）</span><span class="sxs-lookup"><span data-stu-id="330f0-289">(Code Snippet - *Models And Data Access - Ex2 Code First Genre*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample8.cs)]

    > [!NOTE]
    > <span data-ttu-id="330f0-290">若要使用 Code First 慣例，類別內容類型必須具有將會自動偵測的 primary key 屬性。</span><span class="sxs-lookup"><span data-stu-id="330f0-290">To work with Code First conventions, the class Genre must have a primary key property that will be automatically detected.</span></span>
    > 
    > <span data-ttu-id="330f0-291">您可以在這[篇 msdn 文章](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx)中閱讀更多有關 Code First 慣例的資訊。</span><span class="sxs-lookup"><span data-stu-id="330f0-291">You can read more about Code First Conventions in this [msdn article](https://msdn.microsoft.com/library/hh161541&amp;#040;v=vs.103&amp;#041;.aspx).</span></span>
2. <span data-ttu-id="330f0-292">現在，從 [**模型**] 專案資料夾開啟 POCO 模型類別**專輯**，並包含外鍵，並建立名稱為**GenreId**和**ArtistId**的屬性。</span><span class="sxs-lookup"><span data-stu-id="330f0-292">Now, open the POCO model class **Album** from **Models** project folder and include the foreign keys, create properties with the names **GenreId** and **ArtistId**.</span></span> <span data-ttu-id="330f0-293">此類別已有主要金鑰的**GenreId** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-293">This class already have the **GenreId** for the primary key.</span></span>

    <span data-ttu-id="330f0-294">（程式碼片段-*模型和資料存取-Ex2 Code First 專輯*）</span><span class="sxs-lookup"><span data-stu-id="330f0-294">(Code Snippet - *Models And Data Access - Ex2 Code First Album*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample9.cs)]
3. <span data-ttu-id="330f0-295">開啟 POCO 模型類別**演出者**，並包含**ArtistId**屬性。</span><span class="sxs-lookup"><span data-stu-id="330f0-295">Open the POCO model class **Artist** and include the **ArtistId** property.</span></span>

    <span data-ttu-id="330f0-296">（程式碼片段-*模型和資料存取-Ex2 Code First 演出者*）</span><span class="sxs-lookup"><span data-stu-id="330f0-296">(Code Snippet - *Models And Data Access - Ex2 Code First Artist*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample10.cs)]
4. <span data-ttu-id="330f0-297">以滑鼠右鍵按一下**模型**專案資料夾，然後選取 [**新增] |類別**。</span><span class="sxs-lookup"><span data-stu-id="330f0-297">Right-click the **Models** project folder and select **Add | Class**.</span></span> <span data-ttu-id="330f0-298">將檔案命名為**MusicStoreEntities.cs**。</span><span class="sxs-lookup"><span data-stu-id="330f0-298">Name the file **MusicStoreEntities.cs**.</span></span> <span data-ttu-id="330f0-299">然後，按一下 [**新增]。**</span><span class="sxs-lookup"><span data-stu-id="330f0-299">Then, click **Add.**</span></span>

    <span data-ttu-id="330f0-300">![新增類別](aspnet-mvc-4-models-and-data-access/_static/image20.png "新增類別")</span><span class="sxs-lookup"><span data-stu-id="330f0-300">![Adding a class](aspnet-mvc-4-models-and-data-access/_static/image20.png "Adding a class")</span></span>

    <span data-ttu-id="330f0-301">*加入新專案*</span><span class="sxs-lookup"><span data-stu-id="330f0-301">*Adding a new item*</span></span>

    <span data-ttu-id="330f0-302">![新增 class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "新增 class2")</span><span class="sxs-lookup"><span data-stu-id="330f0-302">![Adding a class2](aspnet-mvc-4-models-and-data-access/_static/image21.png "Adding a class2")</span></span>

    <span data-ttu-id="330f0-303">*新增類別*</span><span class="sxs-lookup"><span data-stu-id="330f0-303">*Adding a class*</span></span>
5. <span data-ttu-id="330f0-304">開啟您剛才建立的類別（ **MusicStoreEntities.cs**），並包含命名空間**system.object**和**entity。**</span><span class="sxs-lookup"><span data-stu-id="330f0-304">Open the class you have just created, **MusicStoreEntities.cs**, and include the namespaces **System.Data.Entity** and **System.Data.Entity.Infrastructure**.</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample11.cs)]
6. <span data-ttu-id="330f0-305">取代類別宣告以擴充**DbCoNtext**類別：宣告公用**DBSet**和覆寫**OnModelCreating**方法。</span><span class="sxs-lookup"><span data-stu-id="330f0-305">Replace the class declaration to extend the **DbContext** class: declare a public **DBSet** and override **OnModelCreating** method.</span></span> <span data-ttu-id="330f0-306">在此步驟之後，您會取得網域類別，將您的模型與 Entity Framework 連結。</span><span class="sxs-lookup"><span data-stu-id="330f0-306">After this step you will get a domain class that will link your model with the Entity Framework.</span></span> <span data-ttu-id="330f0-307">若要這麼做，請將類別程式碼取代為下列內容：</span><span class="sxs-lookup"><span data-stu-id="330f0-307">In order to do that, replace the class code with the following:</span></span>

    <span data-ttu-id="330f0-308">（程式碼片段-*模型和資料存取-Ex2 Code First MusicStoreEntities*）</span><span class="sxs-lookup"><span data-stu-id="330f0-308">(Code Snippet - *Models And Data Access - Ex2 Code First MusicStoreEntities*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample12.cs)]

> [!NOTE]
> <span data-ttu-id="330f0-309">有了 Entity Framework **DbCoNtext**和**DBSet** ，您就能夠查詢 POCO 類別的內容類型。</span><span class="sxs-lookup"><span data-stu-id="330f0-309">With Entity Framework **DbContext** and **DBSet** you will be able to query the POCO class Genre.</span></span> <span data-ttu-id="330f0-310">藉由擴充**OnModelCreating**方法，您就可以在程式**代碼**中指定內容類型如何對應至資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="330f0-310">By extending **OnModelCreating** method, you are specifying in the **code** how Genre will be mapped to a database table.</span></span> <span data-ttu-id="330f0-311">您可以在這篇 msdn 文章中找到有關 DBCoNtext 和 DBSet 的詳細資訊：[連結](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span><span class="sxs-lookup"><span data-stu-id="330f0-311">You can find more information about DBContext and DBSet in this msdn article: [link](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.103).aspx)</span></span>

<a id="Ex2Task4"></a>

<a id="Task_4_-_Querying_the_Database"></a>
#### <a name="task-4---querying-the-database"></a><span data-ttu-id="330f0-312">工作 4-查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-312">Task 4 - Querying the Database</span></span>

<span data-ttu-id="330f0-313">在這項工作中，您將更新 StoreController 類別，如此一來，它就會從資料庫中取出資料，而不是使用硬式編碼的資料。</span><span class="sxs-lookup"><span data-stu-id="330f0-313">In this task, you will update the StoreController class so that, instead of using hardcoded data, it will retrieve it from the database.</span></span>

> [!NOTE]
> <span data-ttu-id="330f0-314">這項工作在練習1中很常見。</span><span class="sxs-lookup"><span data-stu-id="330f0-314">This task is in common with Exercise 1.</span></span>
> 
> <span data-ttu-id="330f0-315">如果您已完成練習1，您會注意到這兩種方法中的步驟都相同（Database first 或 Code first）。</span><span class="sxs-lookup"><span data-stu-id="330f0-315">If you completed Exercise 1 you will note these steps are the same in both approaches (Database first or Code first).</span></span> <span data-ttu-id="330f0-316">資料與模型的連結方式不同，但對資料實體的存取也不會受到控制器的透明度。</span><span class="sxs-lookup"><span data-stu-id="330f0-316">They are different in how the data is linked with the model, but the access to data entities is yet transparent from the controller.</span></span>

1. <span data-ttu-id="330f0-317">開啟**Controllers\StoreController.cs** ，並將下欄欄位新增至類別，以保存**MusicStoreEntities**類別的實例，名為**storeDB**：</span><span class="sxs-lookup"><span data-stu-id="330f0-317">Open **Controllers\StoreController.cs** and add the following field to the class to hold an instance of the **MusicStoreEntities** class, named **storeDB**:</span></span>

    <span data-ttu-id="330f0-318">（程式碼片段-*模型和資料存取-Ex1 storeDB*）</span><span class="sxs-lookup"><span data-stu-id="330f0-318">(Code Snippet - *Models And Data Access - Ex1 storeDB*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample13.cs)]
2. <span data-ttu-id="330f0-319">**MusicStoreEntities**類別會針對資料庫中的每個資料表公開集合屬性。</span><span class="sxs-lookup"><span data-stu-id="330f0-319">The **MusicStoreEntities** class exposes a collection property for each table in the database.</span></span> <span data-ttu-id="330f0-320">更新**流覽**動作方法，以取得所有**專輯**的內容類型。</span><span class="sxs-lookup"><span data-stu-id="330f0-320">Update **Browse** action method to retrieve a Genre with all of the **Albums**.</span></span>

    <span data-ttu-id="330f0-321">（程式碼片段-*模型和資料存取-Ex2 存放區流覽*）</span><span class="sxs-lookup"><span data-stu-id="330f0-321">(Code Snippet - *Models And Data Access - Ex2 Store Browse*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample14.cs)]

    > [!NOTE]
    > <span data-ttu-id="330f0-322">您會使用稱為**LINQ** （語言整合式查詢）的 .net 功能，針對這些集合撰寫強型別查詢運算式-這將會針對資料庫執行程式碼，並傳回您可以對其進行程式設計的物件。</span><span class="sxs-lookup"><span data-stu-id="330f0-322">You are using a capability of .NET called **LINQ** (language-integrated query) to write strongly-typed query expressions against these collections - which will execute code against the database and return objects that you can program against.</span></span>
    > 
    > <span data-ttu-id="330f0-323">如需 LINQ 的詳細資訊，請造訪[msdn 網站](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="330f0-323">For more information about LINQ, please visit the [msdn site](https://msdn.microsoft.com/library/bb397926(v=vs.110).aspx).</span></span>
3. <span data-ttu-id="330f0-324">更新**索引**動作方法，以取得所有內容內容。</span><span class="sxs-lookup"><span data-stu-id="330f0-324">Update **Index** action method to retrieve all the genres.</span></span>

    <span data-ttu-id="330f0-325">（程式碼片段-*模型和資料存取-Ex2 存放區索引*）</span><span class="sxs-lookup"><span data-stu-id="330f0-325">(Code Snippet - *Models And Data Access - Ex2 Store Index*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample15.cs)]
4. <span data-ttu-id="330f0-326">更新**索引**動作方法以抓取所有內容，並將集合轉換為清單。</span><span class="sxs-lookup"><span data-stu-id="330f0-326">Update **Index** action method to retrieve all the genres and transform the collection to a list.</span></span>

    <span data-ttu-id="330f0-327">（程式碼片段-*模型和資料存取-Ex2 Store GenreMenu*）</span><span class="sxs-lookup"><span data-stu-id="330f0-327">(Code Snippet - *Models And Data Access - Ex2 Store GenreMenu*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample16.cs)]

<a id="Ex2Task5"></a>

<a id="Task_5_-_Running_the_Application"></a>
#### <a name="task-5---running-the-application"></a><span data-ttu-id="330f0-328">工作 5-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="330f0-328">Task 5 - Running the Application</span></span>

<span data-ttu-id="330f0-329">在這項工作中，您將檢查 [存放區索引] 頁面現在會顯示儲存在資料庫中的內容，而不是硬式編碼的內容。</span><span class="sxs-lookup"><span data-stu-id="330f0-329">In this task, you will check that the Store Index page will now display the Genres stored in the database instead of the hardcoded ones.</span></span> <span data-ttu-id="330f0-330">不需要變更視圖範本，因為**StoreController**會傳回與之前相同的**StoreIndexViewModel** ，但是這次資料會來自資料庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-330">There is no need to change the View template because the **StoreController** is returning the same **StoreIndexViewModel** as before, but this time the data will come from the database.</span></span>

1. <span data-ttu-id="330f0-331">重建方案，然後按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="330f0-331">Rebuild the solution and press **F5** to run the Application.</span></span>
2. <span data-ttu-id="330f0-332">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="330f0-332">The project starts in the Home page.</span></span> <span data-ttu-id="330f0-333">確認 [內容類型] 功能表**不再是 [** 硬式編碼] 清單，而且資料是從資料庫中直接抓取。</span><span class="sxs-lookup"><span data-stu-id="330f0-333">Verify that the menu of **Genres** is no longer a hardcoded list, and the data is directly retrieved from the database.</span></span>

    ![BrowsingGenresFromDataBase](aspnet-mvc-4-models-and-data-access/_static/image22.png)

    <span data-ttu-id="330f0-335">*從資料庫流覽內容內容*</span><span class="sxs-lookup"><span data-stu-id="330f0-335">*Browsing Genres from the database*</span></span>
3. <span data-ttu-id="330f0-336">現在，流覽至任何內容類型，並確認專輯已從資料庫中填入。</span><span class="sxs-lookup"><span data-stu-id="330f0-336">Now browse to any genre and verify the albums are populated from database.</span></span>

    <span data-ttu-id="330f0-337">![從資料庫流覽專輯](aspnet-mvc-4-models-and-data-access/_static/image23.png "從資料庫流覽專輯")</span><span class="sxs-lookup"><span data-stu-id="330f0-337">![Browsing Albums from the database](aspnet-mvc-4-models-and-data-access/_static/image23.png "Browsing Albums from the database")</span></span>

    <span data-ttu-id="330f0-338">*從資料庫流覽專輯*</span><span class="sxs-lookup"><span data-stu-id="330f0-338">*Browsing Albums from the database*</span></span>

<a id="Exercise3"></a>

<a id="Exercise_3_Querying_the_Database_with_Parameters"></a>
### <a name="exercise-3-querying-the-database-with-parameters"></a><span data-ttu-id="330f0-339">練習3：使用參數查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-339">Exercise 3: Querying the Database with Parameters</span></span>

<span data-ttu-id="330f0-340">在此練習中，您將學習如何使用參數來查詢資料庫，以及如何使用查詢結果成形，這項功能可減少資料庫存取以更有效率的方式抓取資料的次數。</span><span class="sxs-lookup"><span data-stu-id="330f0-340">In this exercise, you will learn how to query the database using parameters, and how to use Query Result Shaping, a feature that reduces the number database accesses retrieving data in a more efficient way.</span></span>

> [!NOTE]
> <span data-ttu-id="330f0-341">如需查詢結果成形的進一步資訊，請造訪下列[msdn 文章](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx)。</span><span class="sxs-lookup"><span data-stu-id="330f0-341">For further information on Query Result Shaping, visit the following [msdn article](https://msdn.microsoft.com/library/bb896272&amp;#040;v=vs.100&amp;#041;.aspx).</span></span>

<a id="Ex3Task1"></a>

<a id="Task_1_-_Modifying_StoreController_to_Retrieve_Albums_from_Database"></a>
#### <a name="task-1---modifying-storecontroller-to-retrieve-albums-from-database"></a><span data-ttu-id="330f0-342">工作 1-修改 StoreController 以從資料庫中取出專輯</span><span class="sxs-lookup"><span data-stu-id="330f0-342">Task 1 - Modifying StoreController to Retrieve Albums from Database</span></span>

<span data-ttu-id="330f0-343">在這項工作中，您將變更**StoreController**類別來存取資料庫，以從特定的內容類型中取出專輯。</span><span class="sxs-lookup"><span data-stu-id="330f0-343">In this task, you will change the **StoreController** class to access the database to retrieve albums from a specific genre.</span></span>

1. <span data-ttu-id="330f0-344">如果您想要使用「資料庫優先」方法 **，請開啟**位於**Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin**資料夾的「**開始**」方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-344">Open the **Begin** solution located at the **Source\Ex3-QueryingTheDatabaseWithParametersCodeFirst\Begin** folder if you want to use Code-First approach or **Source\Ex3-QueryingTheDatabaseWithParametersDBFirst\Begin** folder if you want to use Database-First approach.</span></span> <span data-ttu-id="330f0-345">否則，您可能會繼續使用藉由完成前一個練習所取得的**結束**解決方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-345">Otherwise, you might continue using the **End** solution obtained by completing the previous exercise.</span></span>

   1. <span data-ttu-id="330f0-346">如果您開啟了提供的**開始**解決方案，您將需要先下載一些遺漏的 NuGet 套件，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="330f0-346">If you opened the provided **Begin** solution, you will need to download some missing NuGet packages before continue.</span></span> <span data-ttu-id="330f0-347">若要這麼做，請按一下 [**專案**] 功能表，然後選取 [**管理 NuGet 套件**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-347">To do this, click the **Project** menu and select **Manage NuGet Packages**.</span></span>
   2. <span data-ttu-id="330f0-348">在 [**管理 NuGet 封裝**] 對話方塊中，按一下 [**還原**] 以下載遺漏的套件。</span><span class="sxs-lookup"><span data-stu-id="330f0-348">In the **Manage NuGet Packages** dialog, click **Restore** in order to download missing packages.</span></span>
   3. <span data-ttu-id="330f0-349">最後，按一下 [**組建**] | [**組建方案**] 來建立方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-349">Finally, build the solution by clicking **Build** | **Build Solution**.</span></span>

      > [!NOTE]
      > <span data-ttu-id="330f0-350">使用 NuGet 的其中一個優點是您不需要在專案中寄送所有程式庫，以減少專案大小。</span><span class="sxs-lookup"><span data-stu-id="330f0-350">One of the advantages of using NuGet is that you don't have to ship all the libraries in your project, reducing the project size.</span></span> <span data-ttu-id="330f0-351">使用 NuGet Power Tools，藉由指定 package 檔案中的封裝版本，您就能夠在第一次執行專案時下載所有必要的程式庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-351">With NuGet Power Tools, by specifying the package versions in the Packages.config file, you will be able to download all the required libraries the first time you run the project.</span></span> <span data-ttu-id="330f0-352">這就是為什麼您必須在從這個實驗室中開啟現有的解決方案之後，才需要執行這些步驟。</span><span class="sxs-lookup"><span data-stu-id="330f0-352">This is why you will have to run these steps after you open an existing solution from this lab.</span></span>
2. <span data-ttu-id="330f0-353">開啟**StoreController**類別以變更**流覽**動作方法。</span><span class="sxs-lookup"><span data-stu-id="330f0-353">Open the **StoreController** class to change the **Browse** action method.</span></span> <span data-ttu-id="330f0-354">若要這麼做，請在 **方案總管**中展開 **控制器** 資料夾，然後按兩下  **StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="330f0-354">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
3. <span data-ttu-id="330f0-355">變更 [**流覽動作]** 方法，以取得特定內容類型的專輯。</span><span class="sxs-lookup"><span data-stu-id="330f0-355">Change the **Browse** action method to retrieve albums for a specific genre.</span></span> <span data-ttu-id="330f0-356">若要這麼做，請取代下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="330f0-356">To do this, replace the following code:</span></span>

    <span data-ttu-id="330f0-357">（程式碼片段-*模型和資料存取-Ex3 StoreController BrowseMethod*）</span><span class="sxs-lookup"><span data-stu-id="330f0-357">(Code Snippet - *Models And Data Access - Ex3 StoreController BrowseMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample17.cs)]

> [!NOTE]
> <span data-ttu-id="330f0-358">若要填入實體的集合，您必須使用**Include**方法來指定您也想要取得專輯。</span><span class="sxs-lookup"><span data-stu-id="330f0-358">To populate a collection of the entity, you need to use the **Include** method to specify you want to retrieve the albums too.</span></span> <span data-ttu-id="330f0-359">您可以使用。LINQ 中的**單一（）** 延伸模組，因為在此情況下，專輯僅應有一個內容類型。</span><span class="sxs-lookup"><span data-stu-id="330f0-359">You can use the .**Single()** extension in LINQ because in this case only one genre is expected for an album.</span></span> <span data-ttu-id="330f0-360">**Single （）** 方法會採用 Lambda 運算式做為參數，在此情況下，它會指定單一類型物件，使其名稱符合所定義的值。</span><span class="sxs-lookup"><span data-stu-id="330f0-360">The **Single()** method takes a Lambda expression as a parameter, which in this case specifies a single Genre object such that its name matches the value defined.</span></span>
> 
> <span data-ttu-id="330f0-361">您將會利用一項功能，讓您在抓取內容類型物件時，指出您想要載入的其他相關實體。</span><span class="sxs-lookup"><span data-stu-id="330f0-361">You will take advantage of a feature that allows you to indicate other related entities you want loaded as well when the Genre object is retrieved.</span></span> <span data-ttu-id="330f0-362">這項功能稱為「**查詢結果塑造**」，可讓您減少存取資料庫以取得資訊所需的次數。</span><span class="sxs-lookup"><span data-stu-id="330f0-362">This feature is called **Query Result Shaping**, and enables you to reduce the number of times needed to access the database to retrieve information.</span></span> <span data-ttu-id="330f0-363">在此案例中，您會想要為您所取得的內容類型預先提取專輯。</span><span class="sxs-lookup"><span data-stu-id="330f0-363">In this scenario, you will want to pre-fetch the Albums for the Genre you retrieve.</span></span>
> 
> <span data-ttu-id="330f0-364">此查詢包含內容類型 **。包含（&quot;專輯&quot;）** ，表示您也想要相關的專輯。</span><span class="sxs-lookup"><span data-stu-id="330f0-364">The query includes **Genres.Include(&quot;Albums&quot;)** to indicate that you want related albums as well.</span></span> <span data-ttu-id="330f0-365">這會導致更有效率的應用程式，因為它會在單一資料庫要求中同時取得內容類型和專輯資料。</span><span class="sxs-lookup"><span data-stu-id="330f0-365">This will result in a more efficient application, since it will retrieve both Genre and Album data in a single database request.</span></span>

<a id="Ex3Task2"></a>

<a id="Task_2_-_Running_the_Application"></a>
#### <a name="task-2---running-the-application"></a><span data-ttu-id="330f0-366">工作 2-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="330f0-366">Task 2 - Running the Application</span></span>

<span data-ttu-id="330f0-367">在這項工作中，您將執行應用程式，並從資料庫中取出特定類型的專輯。</span><span class="sxs-lookup"><span data-stu-id="330f0-367">In this task, you will run the application and retrieve albums of a specific genre from the database.</span></span>

1. <span data-ttu-id="330f0-368">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="330f0-368">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="330f0-369">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="330f0-369">The project starts in the Home page.</span></span> <span data-ttu-id="330f0-370">將 URL 變更為 **/Store/Browse？內容類型 = Pop** ，以確認結果是從資料庫中取得。</span><span class="sxs-lookup"><span data-stu-id="330f0-370">Change the URL to **/Store/Browse?genre=Pop** to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="330f0-371">![依內容類型流覽](aspnet-mvc-4-models-and-data-access/_static/image24.png "依內容類型流覽")</span><span class="sxs-lookup"><span data-stu-id="330f0-371">![Browsing by genre](aspnet-mvc-4-models-and-data-access/_static/image24.png "Browsing by genre")</span></span>

    <span data-ttu-id="330f0-372">*流覽/Store/Browse？內容類型 = Pop*</span><span class="sxs-lookup"><span data-stu-id="330f0-372">*Browsing /Store/Browse?genre=Pop*</span></span>

<a id="Ex3Task3"></a>

<a id="Task_3_-_Accessing_Albums_by_Id"></a>
#### <a name="task-3---accessing-albums-by-id"></a><span data-ttu-id="330f0-373">工作 3-依識別碼存取專輯</span><span class="sxs-lookup"><span data-stu-id="330f0-373">Task 3 - Accessing Albums by Id</span></span>

<span data-ttu-id="330f0-374">在這項工作中，您將重複先前的程式，依其識別碼取得專輯。</span><span class="sxs-lookup"><span data-stu-id="330f0-374">In this task, you will repeat the previous procedure to get albums by their Id.</span></span>

1. <span data-ttu-id="330f0-375">如有需要，請關閉瀏覽器，以返回 Visual Studio。</span><span class="sxs-lookup"><span data-stu-id="330f0-375">Close the browser if needed, to return to Visual Studio.</span></span> <span data-ttu-id="330f0-376">開啟**StoreController**類別來變更**Details**動作方法。</span><span class="sxs-lookup"><span data-stu-id="330f0-376">Open the **StoreController** class to change the **Details** action method.</span></span> <span data-ttu-id="330f0-377">若要這麼做，請在 **方案總管**中展開 **控制器** 資料夾，然後按兩下  **StoreController.cs**。</span><span class="sxs-lookup"><span data-stu-id="330f0-377">To do this, in the **Solution Explorer**, expand the **Controllers** folder and double-click **StoreController.cs**.</span></span>
2. <span data-ttu-id="330f0-378">變更 [**詳細資料**動作] 方法，以根據其**識別碼**抓取專輯詳細資料。若要這麼做，請取代下列程式碼：</span><span class="sxs-lookup"><span data-stu-id="330f0-378">Change the **Details** action method to retrieve albums details based on their **Id**. To do this, replace the following code:</span></span>

    <span data-ttu-id="330f0-379">（程式碼片段-*模型和資料存取-Ex3 StoreController DetailsMethod*）</span><span class="sxs-lookup"><span data-stu-id="330f0-379">(Code Snippet - *Models And Data Access - Ex3 StoreController DetailsMethod*)</span></span>

    [!code-csharp[Main](aspnet-mvc-4-models-and-data-access/samples/sample18.cs)]

<a id="Ex3Task4"></a>

<a id="Task_4_-_Running_the_Application"></a>
#### <a name="task-4---running-the-application"></a><span data-ttu-id="330f0-380">工作 4-正在執行應用程式</span><span class="sxs-lookup"><span data-stu-id="330f0-380">Task 4 - Running the Application</span></span>

<span data-ttu-id="330f0-381">在這項工作中，您將會在網頁瀏覽器中執行應用程式，並依其識別碼取得專輯詳細資料。</span><span class="sxs-lookup"><span data-stu-id="330f0-381">In this task, you will run the Application in a web browser and obtain album details by their Id.</span></span>

1. <span data-ttu-id="330f0-382">按**F5**執行應用程式。</span><span class="sxs-lookup"><span data-stu-id="330f0-382">Press **F5** to run the Application.</span></span>
2. <span data-ttu-id="330f0-383">專案會在首頁中啟動。</span><span class="sxs-lookup"><span data-stu-id="330f0-383">The project starts in the Home page.</span></span> <span data-ttu-id="330f0-384">將 URL 變更為 **/Store/Details/51**或流覽內容類型，然後選取專輯以確認結果是從資料庫中取得。</span><span class="sxs-lookup"><span data-stu-id="330f0-384">Change the URL to **/Store/Details/51** or browse the genres and select an album to verify that the results are being retrieved from the database.</span></span>

    <span data-ttu-id="330f0-385">![流覽詳細資料](aspnet-mvc-4-models-and-data-access/_static/image25.png "流覽詳細資料")</span><span class="sxs-lookup"><span data-stu-id="330f0-385">![Browsing Details](aspnet-mvc-4-models-and-data-access/_static/image25.png "Browsing Details")</span></span>

    <span data-ttu-id="330f0-386">*流覽/Store/Details/51*</span><span class="sxs-lookup"><span data-stu-id="330f0-386">*Browsing /Store/Details/51*</span></span>

> [!NOTE]
> <span data-ttu-id="330f0-387">此外，您可以遵循[附錄 B：使用 Web Deploy 發佈 ASP.NET MVC 4 應用程式](#AppendixB)，將此應用程式部署到 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="330f0-387">Additionally, you can deploy this application to Windows Azure Web Sites following [Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy](#AppendixB).</span></span>

---

<a id="Summary"></a>

<a id="Summary"></a>
## <a name="summary"></a><span data-ttu-id="330f0-388">總結</span><span class="sxs-lookup"><span data-stu-id="330f0-388">Summary</span></span>

<span data-ttu-id="330f0-389">藉由完成此實際操作實驗室，您已瞭解 ASP.NET MVC 模型和資料存取的基本概念，並使用**Database First**方法以及**Code First**方法：</span><span class="sxs-lookup"><span data-stu-id="330f0-389">By completing this Hands-on Lab you have learned the fundamentals of ASP.NET MVC Models and Data Access, using the **Database First** approach as well as the **Code First** Approach:</span></span>

- <span data-ttu-id="330f0-390">如何將資料庫新增至方案，以便取用其資料</span><span class="sxs-lookup"><span data-stu-id="330f0-390">How to add a database to the solution in order to consume its data</span></span>
- <span data-ttu-id="330f0-391">如何更新控制器以提供視圖範本，其中包含從資料庫取得的資料，而不是硬式編碼</span><span class="sxs-lookup"><span data-stu-id="330f0-391">How to update Controllers to provide View templates with the data taken from the database instead of hard-coded one</span></span>
- <span data-ttu-id="330f0-392">如何使用參數查詢資料庫</span><span class="sxs-lookup"><span data-stu-id="330f0-392">How to query the database using parameters</span></span>
- <span data-ttu-id="330f0-393">如何使用查詢結果成形，這項功能可減少資料庫存取次數，以更有效率的方式來抓取資料</span><span class="sxs-lookup"><span data-stu-id="330f0-393">How to use the Query Result Shaping, a feature that reduces the number of database accesses, retrieving data in a more efficient way</span></span>
- <span data-ttu-id="330f0-394">如何使用 Microsoft Entity Framework 中的 Database First 和 Code First 方法，將資料庫與模型連結</span><span class="sxs-lookup"><span data-stu-id="330f0-394">How to use both Database First and Code First approaches in Microsoft Entity Framework to link the database with the model</span></span>

<a id="AppendixA"></a>

<a id="Appendix_A_Installing_Visual_Studio_Express_2012_for_Web"></a>
## <a name="appendix-a-installing-visual-studio-express-2012-for-web"></a><span data-ttu-id="330f0-395">附錄 A：安裝 Web 的 Visual Studio Express 2012</span><span class="sxs-lookup"><span data-stu-id="330f0-395">Appendix A: Installing Visual Studio Express 2012 for Web</span></span>

<span data-ttu-id="330f0-396">您可以使用 **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)** 安裝 Web 或另一個 &quot;Express&quot; 版本**的 Microsoft Visual Studio Express 2012** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-396">You can install **Microsoft Visual Studio Express 2012 for Web** or another &quot;Express&quot; version using the **[Microsoft Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)**.</span></span> <span data-ttu-id="330f0-397">下列指示會引導您完成使用*Microsoft Web Platform Installer*安裝*Visual studio Express 2012 for Web*所需的步驟。</span><span class="sxs-lookup"><span data-stu-id="330f0-397">The following instructions guide you through the steps required to install *Visual studio Express 2012 for Web* using *Microsoft Web Platform Installer*.</span></span>

1. <span data-ttu-id="330f0-398">移至[[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169)。</span><span class="sxs-lookup"><span data-stu-id="330f0-398">Go to [[https://go.microsoft.com/?linkid=9810169](https://go.microsoft.com/?linkid=9810169)](https://go.microsoft.com/?linkid=9810169).</span></span> <span data-ttu-id="330f0-399">或者，如果您已經安裝 Web Platform Installer，您可以開啟它，然後使用 Windows Azure SDK&quot;來搜尋產品 &quot;<em>Visual Studio Express 2012 For Web</em> 。</span><span class="sxs-lookup"><span data-stu-id="330f0-399">Alternatively, if you already have installed Web Platform Installer, you can open it and search for the product &quot;<em>Visual Studio Express 2012 for Web with Windows Azure SDK</em>&quot;.</span></span>
2. <span data-ttu-id="330f0-400">按一下 [**立即安裝**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-400">Click on **Install Now**.</span></span> <span data-ttu-id="330f0-401">如果您沒有**Web Platform Installer**系統會將您重新導向，先下載並安裝。</span><span class="sxs-lookup"><span data-stu-id="330f0-401">If you do not have **Web Platform Installer** you will be redirected to download and install it first.</span></span>
3. <span data-ttu-id="330f0-402">開啟**Web Platform Installer**之後，請按一下 [**安裝**] 以啟動安裝程式。</span><span class="sxs-lookup"><span data-stu-id="330f0-402">Once **Web Platform Installer** is open, click **Install** to start the setup.</span></span>

    <span data-ttu-id="330f0-403">![安裝 Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "安裝 Visual Studio Express")</span><span class="sxs-lookup"><span data-stu-id="330f0-403">![Install Visual Studio Express](aspnet-mvc-4-models-and-data-access/_static/image26.png "Install Visual Studio Express")</span></span>

    <span data-ttu-id="330f0-404">*安裝 Visual Studio Express*</span><span class="sxs-lookup"><span data-stu-id="330f0-404">*Install Visual Studio Express*</span></span>
4. <span data-ttu-id="330f0-405">閱讀所有產品的授權和條款，然後按一下 [**我接受**] 繼續。</span><span class="sxs-lookup"><span data-stu-id="330f0-405">Read all the products' licenses and terms and click **I Accept** to continue.</span></span>

    ![接受授權條款](aspnet-mvc-4-models-and-data-access/_static/image27.png)

    <span data-ttu-id="330f0-407">*接受授權條款*</span><span class="sxs-lookup"><span data-stu-id="330f0-407">*Accepting the license terms*</span></span>
5. <span data-ttu-id="330f0-408">等到下載和安裝程式完成為止。</span><span class="sxs-lookup"><span data-stu-id="330f0-408">Wait until the downloading and installation process completes.</span></span>

    ![安裝進度](aspnet-mvc-4-models-and-data-access/_static/image28.png)

    <span data-ttu-id="330f0-410">*安裝進度*</span><span class="sxs-lookup"><span data-stu-id="330f0-410">*Installation progress*</span></span>
6. <span data-ttu-id="330f0-411">當安裝完成時，按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-411">When the installation completes, click **Finish**.</span></span>

    ![安裝已完成](aspnet-mvc-4-models-and-data-access/_static/image29.png)

    <span data-ttu-id="330f0-413">*安裝已完成*</span><span class="sxs-lookup"><span data-stu-id="330f0-413">*Installation completed*</span></span>
7. <span data-ttu-id="330f0-414">按一下 **[** 結束] 以關閉 Web Platform Installer。</span><span class="sxs-lookup"><span data-stu-id="330f0-414">Click **Exit** to close Web Platform Installer.</span></span>
8. <span data-ttu-id="330f0-415">若要開啟 Web Visual Studio Express，請移至 [**開始**] 畫面，然後開始撰寫 &quot;**VS Express**&quot;，然後按一下 [ **VS Express for Web** ] 磚。</span><span class="sxs-lookup"><span data-stu-id="330f0-415">To open Visual Studio Express for Web, go to the **Start** screen and start writing &quot;**VS Express**&quot;, then click on the **VS Express for Web** tile.</span></span>

    ![VS Express for Web 磚](aspnet-mvc-4-models-and-data-access/_static/image30.png)

    <span data-ttu-id="330f0-417">*VS Express for Web 磚*</span><span class="sxs-lookup"><span data-stu-id="330f0-417">*VS Express for Web tile*</span></span>

<a id="AppendixB"></a>

<a id="Appendix_B_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
## <a name="appendix-b-publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="330f0-418">附錄 B：使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="330f0-418">Appendix B: Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

<span data-ttu-id="330f0-419">本附錄將告訴您如何從 Windows Azure 管理入口網站建立新的網站，以及如何發佈您在實驗室之後取得的應用程式，利用 Windows Azure 提供的 Web Deploy 發行功能。</span><span class="sxs-lookup"><span data-stu-id="330f0-419">This appendix will show you how to create a new web site from the Windows Azure Management Portal and publish the application you obtained by following the lab, taking advantage of the Web Deploy publishing feature provided by Windows Azure.</span></span>

<a id="ApxBTask1"></a>

<a id="Task_1_-_Creating_a_New_Web_Site_from_the_Windows_Azure_Portal"></a>
#### <a name="task-1---creating-a-new-web-site-from-the-windows-azure-portal"></a><span data-ttu-id="330f0-420">工作 1-從 Windows Azure 入口網站建立新的網站</span><span class="sxs-lookup"><span data-stu-id="330f0-420">Task 1 - Creating a New Web Site from the Windows Azure Portal</span></span>

1. <span data-ttu-id="330f0-421">移至[Windows Azure 管理入口網站](https://manage.windowsazure.com/)並使用與您的訂用帳戶相關聯的 Microsoft 認證登入。</span><span class="sxs-lookup"><span data-stu-id="330f0-421">Go to the [Windows Azure Management Portal](https://manage.windowsazure.com/) and sign in using the Microsoft credentials associated with your subscription.</span></span>

    > [!NOTE]
    > <span data-ttu-id="330f0-422">有了 Windows Azure，您可以免費裝載10個 ASP.NET 網站，然後隨著流量的成長而調整。</span><span class="sxs-lookup"><span data-stu-id="330f0-422">With Windows Azure you can host 10 ASP.NET Web Sites for free and then scale as your traffic grows.</span></span> <span data-ttu-id="330f0-423">您可以在[這裡](https://aka.ms/aspnet-hol-azure)註冊。</span><span class="sxs-lookup"><span data-stu-id="330f0-423">You can sign up [here](https://aka.ms/aspnet-hol-azure).</span></span>

    <span data-ttu-id="330f0-424">![登入 Windows Azure 入口網站](aspnet-mvc-4-models-and-data-access/_static/image31.png "登入 Windows Azure 入口網站")</span><span class="sxs-lookup"><span data-stu-id="330f0-424">![Log on to Windows Azure portal](aspnet-mvc-4-models-and-data-access/_static/image31.png "Log on to Windows Azure portal")</span></span>

    <span data-ttu-id="330f0-425">*登入 Windows Azure 管理入口網站*</span><span class="sxs-lookup"><span data-stu-id="330f0-425">*Log on to Windows Azure Management Portal*</span></span>
2. <span data-ttu-id="330f0-426">按一下命令列上的 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-426">Click **New** on the command bar.</span></span>

    <span data-ttu-id="330f0-427">![建立新網站](aspnet-mvc-4-models-and-data-access/_static/image32.png "建立新網站")</span><span class="sxs-lookup"><span data-stu-id="330f0-427">![Creating a new Web Site](aspnet-mvc-4-models-and-data-access/_static/image32.png "Creating a new Web Site")</span></span>

    <span data-ttu-id="330f0-428">*建立新網站*</span><span class="sxs-lookup"><span data-stu-id="330f0-428">*Creating a new Web Site*</span></span>
3. <span data-ttu-id="330f0-429">按一下 [**計算** | 的**網站**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-429">Click **Compute** | **Web Site**.</span></span> <span data-ttu-id="330f0-430">然後選取 [**快速建立**] 選項。</span><span class="sxs-lookup"><span data-stu-id="330f0-430">Then select **Quick Create** option.</span></span> <span data-ttu-id="330f0-431">提供新網站的可用 URL，然後按一下 [**建立網站**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-431">Provide an available URL for the new web site and click **Create Web Site**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="330f0-432">Windows Azure 網站是在雲端中執行之 Web 應用程式的主機，您可以控制和管理。</span><span class="sxs-lookup"><span data-stu-id="330f0-432">A Windows Azure Web Site is the host for a web application running in the cloud that you can control and manage.</span></span> <span data-ttu-id="330f0-433">[快速建立] 選項可讓您從入口網站外部，將已完成的 web 應用程式部署至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="330f0-433">The Quick Create option allows you to deploy a completed web application to the Windows Azure Web Site from outside the portal.</span></span> <span data-ttu-id="330f0-434">它不包含設定資料庫的步驟。</span><span class="sxs-lookup"><span data-stu-id="330f0-434">It does not include steps for setting up a database.</span></span>

    <span data-ttu-id="330f0-435">![使用 [快速建立] 建立新的網站](aspnet-mvc-4-models-and-data-access/_static/image33.png "使用 [快速建立] 建立新的網站")</span><span class="sxs-lookup"><span data-stu-id="330f0-435">![Creating a new Web Site using Quick Create](aspnet-mvc-4-models-and-data-access/_static/image33.png "Creating a new Web Site using Quick Create")</span></span>

    <span data-ttu-id="330f0-436">*使用 [快速建立] 建立新的網站*</span><span class="sxs-lookup"><span data-stu-id="330f0-436">*Creating a new Web Site using Quick Create*</span></span>
4. <span data-ttu-id="330f0-437">等到新**網站**建立完畢。</span><span class="sxs-lookup"><span data-stu-id="330f0-437">Wait until the new **Web Site** is created.</span></span>
5. <span data-ttu-id="330f0-438">建立網站之後，請按一下 [ **URL** ] 資料行下方的連結。</span><span class="sxs-lookup"><span data-stu-id="330f0-438">Once the Web Site is created click the link under the **URL** column.</span></span> <span data-ttu-id="330f0-439">檢查新網站是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="330f0-439">Check that the new Web Site is working.</span></span>

    <span data-ttu-id="330f0-440">![流覽至新網站](aspnet-mvc-4-models-and-data-access/_static/image34.png "流覽至新網站")</span><span class="sxs-lookup"><span data-stu-id="330f0-440">![Browsing to the new web site](aspnet-mvc-4-models-and-data-access/_static/image34.png "Browsing to the new web site")</span></span>

    <span data-ttu-id="330f0-441">*流覽至新網站*</span><span class="sxs-lookup"><span data-stu-id="330f0-441">*Browsing to the new web site*</span></span>

    <span data-ttu-id="330f0-442">![網站正在執行](aspnet-mvc-4-models-and-data-access/_static/image35.png "網站正在執行")</span><span class="sxs-lookup"><span data-stu-id="330f0-442">![Web site running](aspnet-mvc-4-models-and-data-access/_static/image35.png "Web site running")</span></span>

    <span data-ttu-id="330f0-443">*網站正在執行*</span><span class="sxs-lookup"><span data-stu-id="330f0-443">*Web site running*</span></span>
6. <span data-ttu-id="330f0-444">返回入口網站，然後按一下 [**名稱**] 欄底下的網站名稱，以顯示管理頁面。</span><span class="sxs-lookup"><span data-stu-id="330f0-444">Go back to the portal and click the name of the web site under the **Name** column to display the management pages.</span></span>

    <span data-ttu-id="330f0-445">![開啟網站管理頁面](aspnet-mvc-4-models-and-data-access/_static/image36.png "開啟網站管理頁面")</span><span class="sxs-lookup"><span data-stu-id="330f0-445">![Opening the web site management pages](aspnet-mvc-4-models-and-data-access/_static/image36.png "Opening the web site management pages")</span></span>

    <span data-ttu-id="330f0-446">*開啟網站管理頁面*</span><span class="sxs-lookup"><span data-stu-id="330f0-446">*Opening the Web Site management pages*</span></span>
7. <span data-ttu-id="330f0-447">在 [**儀表板**] 頁面的 [**快速概覽**] 區段下，按一下 [**下載發行設定檔**] 連結。</span><span class="sxs-lookup"><span data-stu-id="330f0-447">In the **Dashboard** page, under the **quick glance** section, click the **Download publish profile** link.</span></span>

    > [!NOTE]
    > <span data-ttu-id="330f0-448">*發行設定檔*包含將 web 應用程式發佈至 Windows Azure 網站所需的所有資訊，以供每個已啟用的發行方法使用。</span><span class="sxs-lookup"><span data-stu-id="330f0-448">The *publish profile* contains all of the information required to publish a web application to a Windows Azure website for each enabled publication method.</span></span> <span data-ttu-id="330f0-449">發行設定檔包含 URL、使用者認證和資料庫字串，這些都是用來連接到已啟用發行方法的每個端點並進行驗證的必要資訊。</span><span class="sxs-lookup"><span data-stu-id="330f0-449">The publish profile contains the URLs, user credentials and database strings required to connect to and authenticate against each of the endpoints for which a publication method is enabled.</span></span> <span data-ttu-id="330f0-450">**Microsoft WebMatrix 2**、 **Microsoft Visual Studio Express for Web**和**Microsoft Visual Studio 2012**支援讀取發行設定檔，以將這些程式的設定自動化，以將 Web 應用程式發佈至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="330f0-450">**Microsoft WebMatrix 2**, **Microsoft Visual Studio Express for Web** and **Microsoft Visual Studio 2012** support reading publish profiles to automate configuration of these programs for publishing web applications to Windows Azure websites.</span></span>

    <span data-ttu-id="330f0-451">![正在下載網站發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image37.png "正在下載網站發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="330f0-451">![Downloading the web site publish profile](aspnet-mvc-4-models-and-data-access/_static/image37.png "Downloading the web site publish profile")</span></span>

    <span data-ttu-id="330f0-452">*正在下載網站發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="330f0-452">*Downloading the Web Site publish profile*</span></span>
8. <span data-ttu-id="330f0-453">將發行設定檔下載到已知的位置。</span><span class="sxs-lookup"><span data-stu-id="330f0-453">Download the publish profile file to a known location.</span></span> <span data-ttu-id="330f0-454">在此練習中，您將瞭解如何使用此檔案，將 web 應用程式從 Visual Studio 發行至 Windows Azure 網站。</span><span class="sxs-lookup"><span data-stu-id="330f0-454">Further in this exercise you will see how to use this file to publish a web application to a Windows Azure Web Sites from Visual Studio.</span></span>

    <span data-ttu-id="330f0-455">![儲存發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image38.png "正在儲存發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="330f0-455">![Saving the publish profile file](aspnet-mvc-4-models-and-data-access/_static/image38.png "Saving the publish profile")</span></span>

    <span data-ttu-id="330f0-456">*儲存發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="330f0-456">*Saving the publish profile file*</span></span>

<a id="ApxBTask2"></a>

<a id="Task_2_-_Configuring_the_Database_Server"></a>
#### <a name="task-2---configuring-the-database-server"></a><span data-ttu-id="330f0-457">工作 2-設定資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="330f0-457">Task 2 - Configuring the Database Server</span></span>

<span data-ttu-id="330f0-458">如果您的應用程式會使用 SQL Server 資料庫，您必須建立 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="330f0-458">If your application makes use of SQL Server databases you will need to create a SQL Database server.</span></span> <span data-ttu-id="330f0-459">如果您想要部署不使用 SQL Server 的簡單應用程式，您可能會略過這項工作。</span><span class="sxs-lookup"><span data-stu-id="330f0-459">If you want to deploy a simple application that does not use SQL Server you might skip this task.</span></span>

1. <span data-ttu-id="330f0-460">您將需要 SQL Database 伺服器來儲存應用程式資料庫。</span><span class="sxs-lookup"><span data-stu-id="330f0-460">You will need a SQL Database server for storing the application database.</span></span> <span data-ttu-id="330f0-461">您可以在 Windows Azure 管理入口網站的  **SQL 資料庫** | **伺服器** | **伺服器的儀表板**上，從您的訂用帳戶中查看 SQL Database 伺服器。</span><span class="sxs-lookup"><span data-stu-id="330f0-461">You can view the SQL Database servers from your subscription in the Windows Azure Management portal at **Sql Databases** | **Servers** | **Server's Dashboard**.</span></span> <span data-ttu-id="330f0-462">如果您沒有建立伺服器，可以使用命令列上的 [**新增**] 按鈕建立一個。</span><span class="sxs-lookup"><span data-stu-id="330f0-462">If you do not have a server created, you can create one using the **Add** button on the command bar.</span></span> <span data-ttu-id="330f0-463">記下 [**伺服器名稱] 和 [URL]、[系統管理員登入名稱] 和 [密碼**]，因為您將在後續工作中使用它們。</span><span class="sxs-lookup"><span data-stu-id="330f0-463">Take note of the **server name and URL, administrator login name and password**, as you will use them in the next tasks.</span></span> <span data-ttu-id="330f0-464">請不要建立資料庫，因為它會在稍後的階段中建立。</span><span class="sxs-lookup"><span data-stu-id="330f0-464">Do not create the database yet, as it will be created in a later stage.</span></span>

    <span data-ttu-id="330f0-465">![SQL Database Server 儀表板](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server 儀表板")</span><span class="sxs-lookup"><span data-stu-id="330f0-465">![SQL Database Server Dashboard](aspnet-mvc-4-models-and-data-access/_static/image39.png "SQL Database Server Dashboard")</span></span>

    <span data-ttu-id="330f0-466">*SQL Database Server 儀表板*</span><span class="sxs-lookup"><span data-stu-id="330f0-466">*SQL Database Server Dashboard*</span></span>
2. <span data-ttu-id="330f0-467">在下一項工作中，您將會從 Visual Studio 測試資料庫連線，因此您必須在伺服器的**允許 IP 位址**清單中包含本機 IP 位址。</span><span class="sxs-lookup"><span data-stu-id="330f0-467">In the next task you will test the database connection from Visual Studio, for that reason you need to include your local IP address in the server's list of **Allowed IP Addresses**.</span></span> <span data-ttu-id="330f0-468">若要這麼做，請按一下 **設定**，從**目前的用戶端 IP 位址**中選取 IP 位址，並將它貼入 [**起始 Ip 位址**] 和 [**結束 ip 位址**] 文字方塊，然後按一下 ![新增-用戶端-IP-位址-確定 按鈕](aspnet-mvc-4-models-and-data-access/_static/image40.png) 按鈕。</span><span class="sxs-lookup"><span data-stu-id="330f0-468">To do that, click **Configure**, select the IP address from **Current Client IP Address** and paste it on the **Start IP Address** and **End IP Address** text boxes and click the ![add-client-ip-address-ok-button](aspnet-mvc-4-models-and-data-access/_static/image40.png) button.</span></span>

    ![正在新增用戶端 IP 位址](aspnet-mvc-4-models-and-data-access/_static/image41.png)

    <span data-ttu-id="330f0-470">*正在新增用戶端 IP 位址*</span><span class="sxs-lookup"><span data-stu-id="330f0-470">*Adding Client IP Address*</span></span>
3. <span data-ttu-id="330f0-471">將**用戶端 Ip 位址**新增至 [允許的 ip 位址] 清單之後，按一下 [**儲存**] 以確認變更。</span><span class="sxs-lookup"><span data-stu-id="330f0-471">Once the **Client IP Address** is added to the allowed IP addresses list, click on **Save** to confirm the changes.</span></span>

    ![確認變更](aspnet-mvc-4-models-and-data-access/_static/image42.png)

    <span data-ttu-id="330f0-473">*確認變更*</span><span class="sxs-lookup"><span data-stu-id="330f0-473">*Confirm Changes*</span></span>

<a id="ApxBTask3"></a>

<a id="Task_3_-_Publishing_an_ASPNET_MVC_4_Application_using_Web_Deploy"></a>
#### <a name="task-3---publishing-an-aspnet-mvc-4-application-using-web-deploy"></a><span data-ttu-id="330f0-474">工作 3-使用 Web Deploy 發行 ASP.NET MVC 4 應用程式</span><span class="sxs-lookup"><span data-stu-id="330f0-474">Task 3 - Publishing an ASP.NET MVC 4 Application using Web Deploy</span></span>

1. <span data-ttu-id="330f0-475">返回 ASP.NET MVC 4 解決方案。</span><span class="sxs-lookup"><span data-stu-id="330f0-475">Go back to the ASP.NET MVC 4 solution.</span></span> <span data-ttu-id="330f0-476">在 **方案總管**中，以滑鼠右鍵按一下 網站 專案，然後選取 **發佈**。</span><span class="sxs-lookup"><span data-stu-id="330f0-476">In the **Solution Explorer**, right-click the web site project and select **Publish**.</span></span>

    <span data-ttu-id="330f0-477">![發行應用程式](aspnet-mvc-4-models-and-data-access/_static/image43.png "發行應用程式")</span><span class="sxs-lookup"><span data-stu-id="330f0-477">![Publishing the Application](aspnet-mvc-4-models-and-data-access/_static/image43.png "Publishing the Application")</span></span>

    <span data-ttu-id="330f0-478">*發行網站*</span><span class="sxs-lookup"><span data-stu-id="330f0-478">*Publishing the web site*</span></span>
2. <span data-ttu-id="330f0-479">匯入您在第一個工作中儲存的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="330f0-479">Import the publish profile you saved in the first task.</span></span>

    <span data-ttu-id="330f0-480">![匯入發行設定檔](aspnet-mvc-4-models-and-data-access/_static/image44.png "匯入發行設定檔")</span><span class="sxs-lookup"><span data-stu-id="330f0-480">![Importing the publish profile](aspnet-mvc-4-models-and-data-access/_static/image44.png "Importing the publish profile")</span></span>

    <span data-ttu-id="330f0-481">*正在匯入發行設定檔*</span><span class="sxs-lookup"><span data-stu-id="330f0-481">*Importing publish profile*</span></span>
3. <span data-ttu-id="330f0-482">按一下 [**驗證連接**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-482">Click **Validate Connection**.</span></span> <span data-ttu-id="330f0-483">驗證完成後，按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-483">Once Validation is complete click **Next**.</span></span>

    > [!NOTE]
    > <span data-ttu-id="330f0-484">當您看到 [驗證連線] 按鈕旁出現綠色核取記號時，驗證就會完成。</span><span class="sxs-lookup"><span data-stu-id="330f0-484">Validation is complete once you see a green checkmark appear next to the Validate Connection button.</span></span>

    <span data-ttu-id="330f0-485">![正在驗證連接](aspnet-mvc-4-models-and-data-access/_static/image45.png "正在驗證連接")</span><span class="sxs-lookup"><span data-stu-id="330f0-485">![Validating connection](aspnet-mvc-4-models-and-data-access/_static/image45.png "Validating connection")</span></span>

    <span data-ttu-id="330f0-486">*正在驗證連接*</span><span class="sxs-lookup"><span data-stu-id="330f0-486">*Validating connection*</span></span>
4. <span data-ttu-id="330f0-487">在 [**設定**] 頁面的 [**資料庫**] 區段底下，按一下資料庫連接的文字方塊旁邊的按鈕（也就是**DefaultConnection**）。</span><span class="sxs-lookup"><span data-stu-id="330f0-487">In the **Settings** page, under the **Databases** section, click the button next to your database connection's textbox (i.e. **DefaultConnection**).</span></span>

    <span data-ttu-id="330f0-488">![Web deploy 設定](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy 設定")</span><span class="sxs-lookup"><span data-stu-id="330f0-488">![Web deploy configuration](aspnet-mvc-4-models-and-data-access/_static/image46.png "Web deploy configuration")</span></span>

    <span data-ttu-id="330f0-489">*Web deploy 設定*</span><span class="sxs-lookup"><span data-stu-id="330f0-489">*Web deploy configuration*</span></span>
5. <span data-ttu-id="330f0-490">設定資料庫連接，如下所示：</span><span class="sxs-lookup"><span data-stu-id="330f0-490">Configure the database connection as follows:</span></span>

   - <span data-ttu-id="330f0-491">在 [**伺服器名稱**] 中，使用*tcp：* prefix 輸入您的 SQL Database 伺服器 URL。</span><span class="sxs-lookup"><span data-stu-id="330f0-491">In the **Server name** type your SQL Database server URL using the *tcp:* prefix.</span></span>
   - <span data-ttu-id="330f0-492">在 [**使用者名稱**] 中，輸入您的伺服器管理員登入名稱。</span><span class="sxs-lookup"><span data-stu-id="330f0-492">In **User name** type your server administrator login name.</span></span>
   - <span data-ttu-id="330f0-493">在 [**密碼**] 中輸入您的伺服器管理員登入密碼。</span><span class="sxs-lookup"><span data-stu-id="330f0-493">In **Password** type your server administrator login password.</span></span>
   - <span data-ttu-id="330f0-494">輸入新的資料庫名稱。</span><span class="sxs-lookup"><span data-stu-id="330f0-494">Type a new database name.</span></span>

     <span data-ttu-id="330f0-495">![正在設定目的地連接字串](aspnet-mvc-4-models-and-data-access/_static/image47.png "正在設定目的地連接字串")</span><span class="sxs-lookup"><span data-stu-id="330f0-495">![Configuring destination connection string](aspnet-mvc-4-models-and-data-access/_static/image47.png "Configuring destination connection string")</span></span>

     <span data-ttu-id="330f0-496">*正在設定目的地連接字串*</span><span class="sxs-lookup"><span data-stu-id="330f0-496">*Configuring destination connection string*</span></span>
6. <span data-ttu-id="330f0-497">然後按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="330f0-497">Then click **OK**.</span></span> <span data-ttu-id="330f0-498">當系統提示您建立資料庫時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="330f0-498">When prompted to create the database click **Yes**.</span></span>

    <span data-ttu-id="330f0-499">![建立資料庫](aspnet-mvc-4-models-and-data-access/_static/image48.png "建立資料庫字串")</span><span class="sxs-lookup"><span data-stu-id="330f0-499">![Creating the database](aspnet-mvc-4-models-and-data-access/_static/image48.png "Creating the database string")</span></span>

    <span data-ttu-id="330f0-500">*建立資料庫*</span><span class="sxs-lookup"><span data-stu-id="330f0-500">*Creating the database*</span></span>
7. <span data-ttu-id="330f0-501">您將用來連接到 Windows Azure 中 SQL Database 的連接字串會顯示在 [預設連接] 文字方塊中。</span><span class="sxs-lookup"><span data-stu-id="330f0-501">The connection string you will use to connect to SQL Database in Windows Azure is shown within Default Connection textbox.</span></span> <span data-ttu-id="330f0-502">然後按一下 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="330f0-502">Then click **Next**.</span></span>

    <span data-ttu-id="330f0-503">![指向 SQL Database 的連接字串](aspnet-mvc-4-models-and-data-access/_static/image49.png "指向 SQL Database 的連接字串")</span><span class="sxs-lookup"><span data-stu-id="330f0-503">![Connection string pointing to SQL Database](aspnet-mvc-4-models-and-data-access/_static/image49.png "Connection string pointing to SQL Database")</span></span>

    <span data-ttu-id="330f0-504">*指向 SQL Database 的連接字串*</span><span class="sxs-lookup"><span data-stu-id="330f0-504">*Connection string pointing to SQL Database*</span></span>
8. <span data-ttu-id="330f0-505">在 [**預覽**] 頁面中，按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-505">In the **Preview** page, click **Publish**.</span></span>

    <span data-ttu-id="330f0-506">![發行 web 應用程式](aspnet-mvc-4-models-and-data-access/_static/image50.png "發行 web 應用程式")</span><span class="sxs-lookup"><span data-stu-id="330f0-506">![Publishing the web application](aspnet-mvc-4-models-and-data-access/_static/image50.png "Publishing the web application")</span></span>

    <span data-ttu-id="330f0-507">*發行 web 應用程式*</span><span class="sxs-lookup"><span data-stu-id="330f0-507">*Publishing the web application*</span></span>
9. <span data-ttu-id="330f0-508">發佈程式完成後，您的預設瀏覽器會開啟已發行的網站。</span><span class="sxs-lookup"><span data-stu-id="330f0-508">Once the publishing process finishes, your default browser will open the published web site.</span></span>

<a id="AppendixC"></a>

<a id="Appendix_C_Using_Code_Snippets"></a>
## <a name="appendix-c-using-code-snippets"></a><span data-ttu-id="330f0-509">附錄 C：使用程式碼片段</span><span class="sxs-lookup"><span data-stu-id="330f0-509">Appendix C: Using Code Snippets</span></span>

<span data-ttu-id="330f0-510">有了程式碼片段，您就可以輕鬆地擁有所需的所有程式碼。</span><span class="sxs-lookup"><span data-stu-id="330f0-510">With code snippets, you have all the code you need at your fingertips.</span></span> <span data-ttu-id="330f0-511">實驗室檔會告訴您可以使用它們的確切時機，如下圖所示。</span><span class="sxs-lookup"><span data-stu-id="330f0-511">The lab document will tell you exactly when you can use them, as shown in the following figure.</span></span>

<span data-ttu-id="330f0-512">![使用 Visual Studio 程式碼片段將程式碼插入您的專案](aspnet-mvc-4-models-and-data-access/_static/image51.png "使用 Visual Studio 程式碼片段將程式碼插入您的專案")</span><span class="sxs-lookup"><span data-stu-id="330f0-512">![Using Visual Studio code snippets to insert code into your project](aspnet-mvc-4-models-and-data-access/_static/image51.png "Using Visual Studio code snippets to insert code into your project")</span></span>

<span data-ttu-id="330f0-513">*使用 Visual Studio 程式碼片段將程式碼插入您的專案*</span><span class="sxs-lookup"><span data-stu-id="330f0-513">*Using Visual Studio code snippets to insert code into your project*</span></span>

<span data-ttu-id="330f0-514">***若要使用鍵盤新增程式碼片段（C#僅限）***</span><span class="sxs-lookup"><span data-stu-id="330f0-514">***To add a code snippet using the keyboard (C# only)***</span></span>

1. <span data-ttu-id="330f0-515">將游標放在您想要插入程式碼的位置。</span><span class="sxs-lookup"><span data-stu-id="330f0-515">Place the cursor where you would like to insert the code.</span></span>
2. <span data-ttu-id="330f0-516">開始鍵入程式碼片段名稱（不含空格或連字號）。</span><span class="sxs-lookup"><span data-stu-id="330f0-516">Start typing the snippet name (without spaces or hyphens).</span></span>
3. <span data-ttu-id="330f0-517">監看 IntelliSense 會顯示相符的程式碼片段名稱。</span><span class="sxs-lookup"><span data-stu-id="330f0-517">Watch as IntelliSense displays matching snippets' names.</span></span>
4. <span data-ttu-id="330f0-518">選取正確的程式碼片段（或繼續輸入，直到選取整個程式碼片段的名稱為止）。</span><span class="sxs-lookup"><span data-stu-id="330f0-518">Select the correct snippet (or keep typing until the entire snippet's name is selected).</span></span>
5. <span data-ttu-id="330f0-519">按兩次 Tab 鍵，在游標位置插入程式碼片段。</span><span class="sxs-lookup"><span data-stu-id="330f0-519">Press the Tab key twice to insert the snippet at the cursor location.</span></span>

<span data-ttu-id="330f0-520">![開始鍵入程式碼片段名稱](aspnet-mvc-4-models-and-data-access/_static/image52.png "開始鍵入程式碼片段名稱")</span><span class="sxs-lookup"><span data-stu-id="330f0-520">![Start typing the snippet name](aspnet-mvc-4-models-and-data-access/_static/image52.png "Start typing the snippet name")</span></span>

<span data-ttu-id="330f0-521">*開始鍵入程式碼片段名稱*</span><span class="sxs-lookup"><span data-stu-id="330f0-521">*Start typing the snippet name*</span></span>

<span data-ttu-id="330f0-522">![按 Tab 鍵以選取反白顯示的程式碼片段](aspnet-mvc-4-models-and-data-access/_static/image53.png "按 Tab 鍵以選取反白顯示的程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="330f0-522">![Press Tab to select the highlighted snippet](aspnet-mvc-4-models-and-data-access/_static/image53.png "Press Tab to select the highlighted snippet")</span></span>

<span data-ttu-id="330f0-523">*按 Tab 鍵以選取反白顯示的程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="330f0-523">*Press Tab to select the highlighted snippet*</span></span>

<span data-ttu-id="330f0-524">![再按一次 Tab 鍵，將會展開程式碼片段](aspnet-mvc-4-models-and-data-access/_static/image54.png "再按一次 Tab 鍵，將會展開程式碼片段")</span><span class="sxs-lookup"><span data-stu-id="330f0-524">![Press Tab again and the snippet will expand](aspnet-mvc-4-models-and-data-access/_static/image54.png "Press Tab again and the snippet will expand")</span></span>

<span data-ttu-id="330f0-525">*再按一次 Tab 鍵，將會展開程式碼片段*</span><span class="sxs-lookup"><span data-stu-id="330f0-525">*Press Tab again and the snippet will expand*</span></span>

<span data-ttu-id="330f0-526">***若要使用滑鼠C#（、Visual Basic 和 XML）加入程式碼片段***sha-1.</span><span class="sxs-lookup"><span data-stu-id="330f0-526">***To add a code snippet using the mouse (C#, Visual Basic and XML)*** 1.</span></span> <span data-ttu-id="330f0-527">以滑鼠右鍵按一下您要插入程式碼片段的位置。</span><span class="sxs-lookup"><span data-stu-id="330f0-527">Right-click where you want to insert the code snippet.</span></span>

1. <span data-ttu-id="330f0-528">選取 [**插入程式碼片段**]，後面接著 [ **My Code 程式碼片段**]。</span><span class="sxs-lookup"><span data-stu-id="330f0-528">Select **Insert Snippet** followed by **My Code Snippets**.</span></span>
2. <span data-ttu-id="330f0-529">按一下清單中的相關程式碼片段，即可加以選取。</span><span class="sxs-lookup"><span data-stu-id="330f0-529">Pick the relevant snippet from the list, by clicking on it.</span></span>

<span data-ttu-id="330f0-530">![以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]](aspnet-mvc-4-models-and-data-access/_static/image55.png "以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]")</span><span class="sxs-lookup"><span data-stu-id="330f0-530">![Right-click where you want to insert the code snippet and select Insert Snippet](aspnet-mvc-4-models-and-data-access/_static/image55.png "Right-click where you want to insert the code snippet and select Insert Snippet")</span></span>

<span data-ttu-id="330f0-531">*以滑鼠右鍵按一下您要插入程式碼片段的位置，然後選取 [插入片段]*</span><span class="sxs-lookup"><span data-stu-id="330f0-531">*Right-click where you want to insert the code snippet and select Insert Snippet*</span></span>

<span data-ttu-id="330f0-532">![按一下清單中的相關程式碼片段，即可加以選取](aspnet-mvc-4-models-and-data-access/_static/image56.png "按一下清單中的相關程式碼片段，即可加以選取")</span><span class="sxs-lookup"><span data-stu-id="330f0-532">![Pick the relevant snippet from the list, by clicking on it](aspnet-mvc-4-models-and-data-access/_static/image56.png "Pick the relevant snippet from the list, by clicking on it")</span></span>

<span data-ttu-id="330f0-533">*按一下清單中的相關程式碼片段，即可加以選取*</span><span class="sxs-lookup"><span data-stu-id="330f0-533">*Pick the relevant snippet from the list, by clicking on it*</span></span>
