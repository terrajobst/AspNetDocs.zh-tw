---
uid: mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
title: 使用 ASP.NET MVC （C#）在15分鐘內建立電影資料庫應用程式 |Microsoft Docs
author: StephenWalther
description: Stephen Walther 會從一開始到完成，建立整個資料庫驅動的 ASP.NET MVC 應用程式。 本教學課程是新使用者的最佳簡介 。
ms.author: riande
ms.date: 01/27/2009
ms.assetid: dd1be137-91c5-47a8-8137-fecf0789c7f5
msc.legacyurl: /mvc/overview/older-versions-1/movie-database/create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs
msc.type: authoredcontent
ms.openlocfilehash: 1be5d135a44feb27626dd26a544b64cfb57b18a9
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74596359"
---
# <a name="create-a-movie-database-application-in-15-minutes-with-aspnet-mvc-c"></a><span data-ttu-id="22e9d-104">使用 ASP.NET MVC 在 15 分鐘內建立影片資料庫應用程式 (C#)</span><span class="sxs-lookup"><span data-stu-id="22e9d-104">Create a Movie Database Application in 15 Minutes with ASP.NET MVC (C#)</span></span>

<span data-ttu-id="22e9d-105">依[Stephen Walther](https://github.com/StephenWalther)</span><span class="sxs-lookup"><span data-stu-id="22e9d-105">by [Stephen Walther](https://github.com/StephenWalther)</span></span>

[<span data-ttu-id="22e9d-106">下載程式代碼</span><span class="sxs-lookup"><span data-stu-id="22e9d-106">Download Code</span></span>](https://download.microsoft.com/download/7/2/8/728F8794-E59A-4D18-9A56-7AD2DB05BD9D/MovieApp_CS.zip)

> <span data-ttu-id="22e9d-107">Stephen Walther 會從一開始到完成，建立整個資料庫驅動的 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-107">Stephen Walther builds an entire database-driven ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="22e9d-108">本教學課程是 ASP.NET MVC 架構的新手，以及想要瞭解如何建立 ASP.NET MVC 應用程式之人員的絕佳簡介。</span><span class="sxs-lookup"><span data-stu-id="22e9d-108">This tutorial is a great introduction for people who are new to the ASP.NET MVC Framework and who want to get a sense of the process of building an ASP.NET MVC application.</span></span>

<span data-ttu-id="22e9d-109">本教學課程的目的是要讓您瞭解「這是什麼」來建立 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-109">The purpose of this tutorial is to give you a sense of "what it is like" to build an ASP.NET MVC application.</span></span> <span data-ttu-id="22e9d-110">在本教學課程中，我會從一開始到完成建立整個 ASP.NET 的 MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-110">In this tutorial, I blast through building an entire ASP.NET MVC application from start to finish.</span></span> <span data-ttu-id="22e9d-111">我會向您示範如何建立一個簡單的資料庫導向應用程式，以說明如何列出、建立和編輯資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-111">I show you how to build a simple database-driven application that illustrates how you can list, create, and edit database records.</span></span>

<span data-ttu-id="22e9d-112">為了簡化應用程式的建立過程，我們將利用 Visual Studio 2008 的「樣板」功能。</span><span class="sxs-lookup"><span data-stu-id="22e9d-112">To simplify the process of building our application, we'll take advantage of the scaffolding features of Visual Studio 2008.</span></span> <span data-ttu-id="22e9d-113">我們會讓 Visual Studio 產生我們的控制器、模型和視圖的初始程式碼和內容。</span><span class="sxs-lookup"><span data-stu-id="22e9d-113">We'll let Visual Studio generate the initial code and content for our controllers, models, and views.</span></span>

<span data-ttu-id="22e9d-114">如果您已經使用過 Active Server Pages 或 ASP.NET，則應該會發現 ASP.NET MVC 非常熟悉。</span><span class="sxs-lookup"><span data-stu-id="22e9d-114">If you have worked with Active Server Pages or ASP.NET, then you should find ASP.NET MVC very familiar.</span></span> <span data-ttu-id="22e9d-115">ASP.NET MVC views 非常類似 Active Server Pages 應用程式中的頁面。</span><span class="sxs-lookup"><span data-stu-id="22e9d-115">ASP.NET MVC views are very much like the pages in an Active Server Pages application.</span></span> <span data-ttu-id="22e9d-116">而且，如同傳統的 ASP.NET Web form 應用程式，ASP.NET MVC 可讓您完整存取 .NET framework 所提供的一組豐富的語言和類別。</span><span class="sxs-lookup"><span data-stu-id="22e9d-116">And, just like a traditional ASP.NET Web Forms application, ASP.NET MVC provides you with full access to the rich set of languages and classes provided by the .NET framework.</span></span>

<span data-ttu-id="22e9d-117">我希望這個教學課程可讓您瞭解建立 ASP.NET MVC 應用程式的體驗，與建立 Active Server Pages 或 ASP.NET Web Forms 應用程式的體驗有何不同。</span><span class="sxs-lookup"><span data-stu-id="22e9d-117">My hope is that this tutorial will give you a sense of how the experience of building an ASP.NET MVC application is both similar and different than the experience of building an Active Server Pages or ASP.NET Web Forms application.</span></span>

## <a name="overview-of-the-movie-database-application"></a><span data-ttu-id="22e9d-118">電影資料庫應用程式的總覽</span><span class="sxs-lookup"><span data-stu-id="22e9d-118">Overview of the Movie Database Application</span></span>

<span data-ttu-id="22e9d-119">因為我們的目標是要簡化事情，所以我們將建立一個非常簡單的電影資料庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-119">Because our goal is to keep things simple, we'll build a very simple Movie Database application.</span></span> <span data-ttu-id="22e9d-120">我們的簡單電影資料庫應用程式可讓我們執行三項工作：</span><span class="sxs-lookup"><span data-stu-id="22e9d-120">Our simple Movie Database application will allow us to do three things:</span></span>

1. <span data-ttu-id="22e9d-121">列出一組電影資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="22e9d-121">List a set of movie database records</span></span>
2. <span data-ttu-id="22e9d-122">建立新的電影資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="22e9d-122">Create a new movie database record</span></span>
3. <span data-ttu-id="22e9d-123">編輯現有的電影資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="22e9d-123">Edit an existing movie database record</span></span>

<span data-ttu-id="22e9d-124">同樣地，因為我們想要簡單起見，所以我們將利用建立應用程式所需之 ASP.NET MVC 架構的最小功能。</span><span class="sxs-lookup"><span data-stu-id="22e9d-124">Again, because we want to keep things simple, we'll take advantage of the minimum number of features of the ASP.NET MVC framework needed to build our application.</span></span> <span data-ttu-id="22e9d-125">例如，我們不會利用以測試為導向的開發。</span><span class="sxs-lookup"><span data-stu-id="22e9d-125">For example, we won't be taking advantage of Test-Driven Development.</span></span>

<span data-ttu-id="22e9d-126">為了建立我們的應用程式，我們需要完成下列每個步驟：</span><span class="sxs-lookup"><span data-stu-id="22e9d-126">In order to create our application, we need to complete each of the following steps:</span></span>

1. <span data-ttu-id="22e9d-127">建立 ASP.NET MVC Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="22e9d-127">Create the ASP.NET MVC Web Application Project</span></span>
2. <span data-ttu-id="22e9d-128">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="22e9d-128">Create the database</span></span>
3. <span data-ttu-id="22e9d-129">建立資料庫模型</span><span class="sxs-lookup"><span data-stu-id="22e9d-129">Create the database model</span></span>
4. <span data-ttu-id="22e9d-130">建立 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="22e9d-130">Create the ASP.NET MVC controller</span></span>
5. <span data-ttu-id="22e9d-131">建立 ASP.NET MVC views</span><span class="sxs-lookup"><span data-stu-id="22e9d-131">Create the ASP.NET MVC views</span></span>

## <a name="preliminaries"></a><span data-ttu-id="22e9d-132">準備工作</span><span class="sxs-lookup"><span data-stu-id="22e9d-132">Preliminaries</span></span>

<span data-ttu-id="22e9d-133">您需要 Visual Studio 2008 或 Visual Web Developer 2008 Express，才能建立 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-133">You'll need either Visual Studio 2008 or Visual Web Developer 2008 Express to build an ASP.NET MVC application.</span></span> <span data-ttu-id="22e9d-134">您也需要下載 ASP.NET MVC 架構。</span><span class="sxs-lookup"><span data-stu-id="22e9d-134">You also need to download the ASP.NET MVC framework.</span></span>

<span data-ttu-id="22e9d-135">如果您未擁有 Visual Studio 2008，則可以從這個網站下載 Visual Studio 2008 的90天試用版：</span><span class="sxs-lookup"><span data-stu-id="22e9d-135">If you don't own Visual Studio 2008, then you can download a 90 day trial version of Visual Studio 2008 from this website:</span></span>

[https://msdn.microsoft.com/vs2008/products/cc268305.aspx](https://msdn.microsoft.com/vs2008/products/cc268305.aspx)

<span data-ttu-id="22e9d-136">或者，您也可以使用 Visual Web Developer Express 2008 建立 ASP.NET MVC 應用程式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-136">Alternatively, you can create ASP.NET MVC applications with Visual Web Developer Express 2008.</span></span> <span data-ttu-id="22e9d-137">如果您決定使用 Visual Web Developer Express，則必須安裝 Service Pack 1。</span><span class="sxs-lookup"><span data-stu-id="22e9d-137">If you decide to use Visual Web Developer Express then you must have Service Pack 1 installed.</span></span> <span data-ttu-id="22e9d-138">您可以從這個網站下載 Visual Web Developer 2008 Express （含 Service Pack 1）：</span><span class="sxs-lookup"><span data-stu-id="22e9d-138">You can download Visual Web Developer 2008 Express with Service Pack 1 from this website:</span></span>

[<span data-ttu-id="22e9d-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;d isplaylang = en</span><span class="sxs-lookup"><span data-stu-id="22e9d-139">https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en</span></span>](https://www.microsoft.com/downloads/details.aspx?FamilyId=BDB6391C-05CA-4036-9154-6DF4F6DEBD14&amp;displaylang=en)

<span data-ttu-id="22e9d-140">安裝 Visual Studio 2008 或 Visual Web Developer 2008 之後，您必須安裝 ASP.NET MVC 架構。</span><span class="sxs-lookup"><span data-stu-id="22e9d-140">After you install either Visual Studio 2008 or Visual Web Developer 2008, you need to install the ASP.NET MVC framework.</span></span> <span data-ttu-id="22e9d-141">您可以從下列網站下載 ASP.NET MVC 架構：</span><span class="sxs-lookup"><span data-stu-id="22e9d-141">You can download the ASP.NET MVC framework from the following website:</span></span>

[https://www.asp.net/mvc/](../../../index.md)

> [!NOTE] 
> 
> <span data-ttu-id="22e9d-142">您可以利用 Web Platform Installer，而不是個別下載 ASP.NET framework 和 ASP.NET MVC 架構。</span><span class="sxs-lookup"><span data-stu-id="22e9d-142">Instead of downloading the ASP.NET framework and the ASP.NET MVC framework individually, you can take advantage of the Web Platform Installer.</span></span> <span data-ttu-id="22e9d-143">Web Platform Installer 是一種應用程式，可讓您輕鬆地管理已安裝的應用程式是您的電腦：</span><span class="sxs-lookup"><span data-stu-id="22e9d-143">The Web Platform Installer is an application that enables you to easily manage the installed applications are your computer:</span></span>
> 
> [https://www.microsoft.com/web/gallery/Install.aspx](https://www.microsoft.com/web/gallery/Install.aspx)

## <a name="creating-an-aspnet-mvc-web-application-project"></a><span data-ttu-id="22e9d-144">建立 ASP.NET MVC Web 應用程式專案</span><span class="sxs-lookup"><span data-stu-id="22e9d-144">Creating an ASP.NET MVC Web Application Project</span></span>

<span data-ttu-id="22e9d-145">讓我們從在 Visual Studio 2008 中建立新的 ASP.NET MVC Web 應用程式專案開始。</span><span class="sxs-lookup"><span data-stu-id="22e9d-145">Let's start by creating a new ASP.NET MVC Web Application project in Visual Studio 2008.</span></span> <span data-ttu-id="22e9d-146">選取功能表選項 [檔案] **、[新增專案**]，您會看到 [圖 1] 中的 [新增專案] 對話方塊。</span><span class="sxs-lookup"><span data-stu-id="22e9d-146">Select the menu option **File, New Project** and you will see the New Project dialog box in Figure 1.</span></span> <span data-ttu-id="22e9d-147">選取C# [作為程式設計語言]，然後選取 [ASP.NET MVC Web 應用程式] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="22e9d-147">Select C# as the programming language and select the ASP.NET MVC Web Application project template.</span></span> <span data-ttu-id="22e9d-148">提供專案名稱 MovieApp，然後按一下 [確定] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22e9d-148">Give your project the name MovieApp and click the OK button.</span></span>

<span data-ttu-id="22e9d-149">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-149">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image1.png)</span></span>

<span data-ttu-id="22e9d-150">**圖 01**： [新增專案] 對話方塊（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-150">**Figure 01**: The New Project dialog box ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.png))</span></span>

<span data-ttu-id="22e9d-151">請確定您從 [新增專案] 對話方塊頂端的下拉式清單中選取 [.NET Framework 3.5]，否則不會出現 [ASP.NET MVC Web 應用程式] 專案範本。</span><span class="sxs-lookup"><span data-stu-id="22e9d-151">Make sure that you select .NET Framework 3.5 from the dropdown list at the top of the New Project dialog or the ASP.NET MVC Web Application project template won't appear.</span></span>

<span data-ttu-id="22e9d-152">每當您建立新的 MVC Web 應用程式專案時，Visual Studio 會提示您建立個別的單元測試專案。</span><span class="sxs-lookup"><span data-stu-id="22e9d-152">Whenever you create a new MVC Web Application project, Visual Studio prompts you to create a separate unit test project.</span></span> <span data-ttu-id="22e9d-153">[圖 2] 中的對話方塊隨即出現。</span><span class="sxs-lookup"><span data-stu-id="22e9d-153">The dialog in Figure 2 appears.</span></span> <span data-ttu-id="22e9d-154">由於時間限制，我們不會在本教學課程中建立測試（沒錯，我們應該會覺得有點犯）選取 [**否**] 選項，然後按一下 [**確定]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22e9d-154">Because we won't be creating tests in this tutorial because of time constraints (and, yes, we should feel a little guilty about this) select the **No** option and click the **OK** button.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="22e9d-155">Visual Web Developer 不支援測試專案。</span><span class="sxs-lookup"><span data-stu-id="22e9d-155">Visual Web Developer does not support test projects.</span></span>

<span data-ttu-id="22e9d-156">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-156">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image2.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.png)</span></span>

<span data-ttu-id="22e9d-157">**圖 02**： [建立單元測試專案] 對話方塊（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-157">**Figure 02**: The Create Unit Test Project dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.png))</span></span>

<span data-ttu-id="22e9d-158">ASP.NET MVC 應用程式具有一組標準的資料夾： [模型]、[Views] 和 [控制器] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="22e9d-158">An ASP.NET MVC application has a standard set of folders: a Models, Views, and Controllers folder.</span></span> <span data-ttu-id="22e9d-159">您可以在 [方案總管] 視窗中看到這組標準資料夾。</span><span class="sxs-lookup"><span data-stu-id="22e9d-159">You can see this standard set of folders in the Solution Explorer window.</span></span> <span data-ttu-id="22e9d-160">我們必須將檔案新增至每個 [模型]、[Views] 和 [控制器] 資料夾，才能建立電影資料庫應用程式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-160">We'll need to add files to each of the Models, Views, and Controllers folders in order to build our Movie Database application.</span></span>

<span data-ttu-id="22e9d-161">當您使用 Visual Studio 建立新的 MVC 應用程式時，您會取得範例應用程式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-161">When you create a new MVC application with Visual Studio, you get a sample application.</span></span> <span data-ttu-id="22e9d-162">因為我們想要從頭開始，所以我們需要刪除此範例應用程式的內容。</span><span class="sxs-lookup"><span data-stu-id="22e9d-162">Because we want to start from scratch, we need to delete the content for this sample application.</span></span> <span data-ttu-id="22e9d-163">您必須刪除下列檔案和下列資料夾：</span><span class="sxs-lookup"><span data-stu-id="22e9d-163">You need to delete the following file and the following folder:</span></span>

- <span data-ttu-id="22e9d-164">Controllers\HomeController.cs</span><span class="sxs-lookup"><span data-stu-id="22e9d-164">Controllers\HomeController.cs</span></span>
- <span data-ttu-id="22e9d-165">Views\Home</span><span class="sxs-lookup"><span data-stu-id="22e9d-165">Views\Home</span></span>

## <a name="creating-the-database"></a><span data-ttu-id="22e9d-166">建立資料庫</span><span class="sxs-lookup"><span data-stu-id="22e9d-166">Creating the Database</span></span>

<span data-ttu-id="22e9d-167">我們需要建立一個資料庫來保存電影資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-167">We need to create a database to hold our movie database records.</span></span> <span data-ttu-id="22e9d-168">幸運的是，Visual Studio 包含一個名為 SQL Server Express 的免費資料庫。</span><span class="sxs-lookup"><span data-stu-id="22e9d-168">Luckily, Visual Studio includes a free database named SQL Server Express.</span></span> <span data-ttu-id="22e9d-169">請遵循下列步驟來建立資料庫：</span><span class="sxs-lookup"><span data-stu-id="22e9d-169">Follow these steps to create the database:</span></span>

1. <span data-ttu-id="22e9d-170">在 [方案總管] 視窗中，以滑鼠右鍵按一下應用程式\_[Data] 資料夾，然後選取 [**新增]、[新增專案**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22e9d-170">Right-click the App\_Data folder in the Solution Explorer window and select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="22e9d-171">選取 [**資料**] 類別，然後選取 [ **SQL Server 資料庫**] 範本（請參閱 [圖 3]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-171">Select the **Data** category and select the **SQL Server Database** template (see Figure 3).</span></span>
3. <span data-ttu-id="22e9d-172">將新的資料庫命名為*MoviesDB* ，然後按一下 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22e9d-172">Name your new database *MoviesDB.mdf* and click the **Add** button.</span></span>

<span data-ttu-id="22e9d-173">建立資料庫之後，您可以按兩下位於應用程式\_Data 資料夾中的 MoviesDB .mdf 檔案來連接到資料庫。</span><span class="sxs-lookup"><span data-stu-id="22e9d-173">After you create your database, you can connect to the database by double-clicking the MoviesDB.mdf file located in the App\_Data folder.</span></span> <span data-ttu-id="22e9d-174">按兩下 [MoviesDB] 檔案，即可開啟 [伺服器總管] 視窗。</span><span class="sxs-lookup"><span data-stu-id="22e9d-174">Double-clicking the MoviesDB.mdf file opens the Server Explorer window.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="22e9d-175">在 Visual Web Developer 的案例中，[伺服器總管] 視窗會命名為 [資料庫總管] 視窗。</span><span class="sxs-lookup"><span data-stu-id="22e9d-175">The Server Explorer window is named the Database Explorer window in the case of Visual Web Developer.</span></span>

<span data-ttu-id="22e9d-176">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-176">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image3.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.png)</span></span>

<span data-ttu-id="22e9d-177">**圖 03**：建立 Microsoft SQL Server 資料庫（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-177">**Figure 03**: Creating a Microsoft SQL Server Database ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.png))</span></span>

<span data-ttu-id="22e9d-178">接下來，我們需要建立新的資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="22e9d-178">Next, we need to create a new database table.</span></span> <span data-ttu-id="22e9d-179">在 [伺服器 Explorer] 視窗中，以滑鼠右鍵按一下 [資料表] 資料夾，然後選取 [**加入新的資料表**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22e9d-179">From within the Sever Explorer window, right-click the Tables folder and select the menu option **Add New Table**.</span></span> <span data-ttu-id="22e9d-180">選取此功能表選項會開啟 [資料庫資料表設計工具]。</span><span class="sxs-lookup"><span data-stu-id="22e9d-180">Selecting this menu option opens the database table designer.</span></span> <span data-ttu-id="22e9d-181">建立下列資料庫資料行：</span><span class="sxs-lookup"><span data-stu-id="22e9d-181">Create the following database columns:</span></span>

<a id="0.1_table01"></a>

| <span data-ttu-id="22e9d-182">**資料行名稱**</span><span class="sxs-lookup"><span data-stu-id="22e9d-182">**Column Name**</span></span> | <span data-ttu-id="22e9d-183">**資料類型**</span><span class="sxs-lookup"><span data-stu-id="22e9d-183">**Data Type**</span></span> | <span data-ttu-id="22e9d-184">**允許 Null**</span><span class="sxs-lookup"><span data-stu-id="22e9d-184">**Allow Nulls**</span></span> |
| --- | --- | --- |
| <span data-ttu-id="22e9d-185">ID</span><span class="sxs-lookup"><span data-stu-id="22e9d-185">Id</span></span> | <span data-ttu-id="22e9d-186">Int</span><span class="sxs-lookup"><span data-stu-id="22e9d-186">Int</span></span> | <span data-ttu-id="22e9d-187">False</span><span class="sxs-lookup"><span data-stu-id="22e9d-187">False</span></span> |
| <span data-ttu-id="22e9d-188">標題</span><span class="sxs-lookup"><span data-stu-id="22e9d-188">Title</span></span> | <span data-ttu-id="22e9d-189">NVarchar （100）</span><span class="sxs-lookup"><span data-stu-id="22e9d-189">Nvarchar(100)</span></span> | <span data-ttu-id="22e9d-190">False</span><span class="sxs-lookup"><span data-stu-id="22e9d-190">False</span></span> |
| <span data-ttu-id="22e9d-191">Director</span><span class="sxs-lookup"><span data-stu-id="22e9d-191">Director</span></span> | <span data-ttu-id="22e9d-192">NVarchar （100）</span><span class="sxs-lookup"><span data-stu-id="22e9d-192">Nvarchar(100)</span></span> | <span data-ttu-id="22e9d-193">False</span><span class="sxs-lookup"><span data-stu-id="22e9d-193">False</span></span> |
| <span data-ttu-id="22e9d-194">DateReleased</span><span class="sxs-lookup"><span data-stu-id="22e9d-194">DateReleased</span></span> | <span data-ttu-id="22e9d-195">DateTime</span><span class="sxs-lookup"><span data-stu-id="22e9d-195">DateTime</span></span> | <span data-ttu-id="22e9d-196">False</span><span class="sxs-lookup"><span data-stu-id="22e9d-196">False</span></span> |

<span data-ttu-id="22e9d-197">第一個資料行（Id 資料行）有兩個特殊的屬性。</span><span class="sxs-lookup"><span data-stu-id="22e9d-197">The first column, the Id column, has two special properties.</span></span> <span data-ttu-id="22e9d-198">首先，您必須將識別碼資料行標記為主鍵資料行。</span><span class="sxs-lookup"><span data-stu-id="22e9d-198">First, you need to mark the Id column as the primary key column.</span></span> <span data-ttu-id="22e9d-199">選取 [Id] 資料行之後，請按一下 [**設定主要金鑰**] 按鈕（它是看起來像是索引鍵的圖示）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-199">After selecting the Id column, click the **Set Primary Key** button (it is the icon that looks like a key).</span></span> <span data-ttu-id="22e9d-200">第二，您必須將 Id 資料行標示為識別欄位。</span><span class="sxs-lookup"><span data-stu-id="22e9d-200">Second, you need to mark the Id column as an Identity column.</span></span> <span data-ttu-id="22e9d-201">在屬性視窗的資料行中，向下流覽至 [識別規格] 區段，並將它展開。</span><span class="sxs-lookup"><span data-stu-id="22e9d-201">In the Column Properties window, scroll down to the Identity Specification section and expand it.</span></span> <span data-ttu-id="22e9d-202">將 [ **Is Identity** ] 屬性變更為 [**是]** 值。</span><span class="sxs-lookup"><span data-stu-id="22e9d-202">Change the **Is Identity** property to the value **Yes**.</span></span> <span data-ttu-id="22e9d-203">當您完成時，資料表看起來應該如 [圖 4] 所示。</span><span class="sxs-lookup"><span data-stu-id="22e9d-203">When you are finished, the table should look like Figure 4.</span></span>

<span data-ttu-id="22e9d-204">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-204">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image4.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.png)</span></span>

<span data-ttu-id="22e9d-205">**圖 04**：電影資料庫資料表（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-205">**Figure 04**: The Movies database table ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.png))</span></span>

<span data-ttu-id="22e9d-206">最後一個步驟是儲存新的資料表。</span><span class="sxs-lookup"><span data-stu-id="22e9d-206">The final step is to save the new table.</span></span> <span data-ttu-id="22e9d-207">按一下 [儲存] 按鈕（軟碟的圖示），並為新的資料表命名 [電影]。</span><span class="sxs-lookup"><span data-stu-id="22e9d-207">Click the Save button (the icon of the floppy) and give the new table the name Movies.</span></span>

<span data-ttu-id="22e9d-208">建立完資料表之後，請將一些電影記錄新增至資料表。</span><span class="sxs-lookup"><span data-stu-id="22e9d-208">After you finish creating the table, add some movie records to the table.</span></span> <span data-ttu-id="22e9d-209">以滑鼠右鍵按一下 [伺服器總管] 視窗中的 [電影] 資料表，然後選取 [**顯示資料表資料**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22e9d-209">Right-click the Movies table in the Server Explorer window and select the menu option **Show Table Data**.</span></span> <span data-ttu-id="22e9d-210">輸入您最愛的電影清單（請參閱 [圖 5]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-210">Enter a list of your favorite movies (see Figure 5).</span></span>

<span data-ttu-id="22e9d-211">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-211">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image5.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.png)</span></span>

<span data-ttu-id="22e9d-212">**圖 05**：輸入電影記錄（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-212">**Figure 05**: Entering movie records ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.png))</span></span>

## <a name="creating-the-model"></a><span data-ttu-id="22e9d-213">建立模型</span><span class="sxs-lookup"><span data-stu-id="22e9d-213">Creating the Model</span></span>

<span data-ttu-id="22e9d-214">接下來，我們需要建立一組類別來代表我們的資料庫。</span><span class="sxs-lookup"><span data-stu-id="22e9d-214">We next need to create a set of classes to represent our database.</span></span> <span data-ttu-id="22e9d-215">我們需要建立資料庫模型。</span><span class="sxs-lookup"><span data-stu-id="22e9d-215">We need to create a database model.</span></span> <span data-ttu-id="22e9d-216">我們將利用 Microsoft Entity Framework，自動為資料庫模型產生類別。</span><span class="sxs-lookup"><span data-stu-id="22e9d-216">We'll take advantage of the Microsoft Entity Framework to generate the classes for our database model automatically.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="22e9d-217">ASP.NET MVC 架構並未系結至 Microsoft Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="22e9d-217">The ASP.NET MVC framework is not tied to the Microsoft Entity Framework.</span></span> <span data-ttu-id="22e9d-218">您可以利用各種物件關聯式對應（或/M）工具（包括 LINQ to SQL、Subsonic 和 NHibernate）來建立資料庫模型類別。</span><span class="sxs-lookup"><span data-stu-id="22e9d-218">You can create your database model classes by taking advantage of a variety of Object Relational Mapping (OR/M) tools including LINQ to SQL, Subsonic, and NHibernate.</span></span>

<span data-ttu-id="22e9d-219">請遵循下列步驟來啟動實體資料模型 Wizard：</span><span class="sxs-lookup"><span data-stu-id="22e9d-219">Follow these steps to launch the Entity Data Model Wizard:</span></span>

1. <span data-ttu-id="22e9d-220">以滑鼠右鍵按一下 [方案總管] 視窗中的 [模型] 資料夾，然後選取 [**加入]、[新增專案**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22e9d-220">Right-click the Models folder in the Solution Explorer window and the select the menu option **Add, New Item**.</span></span>
2. <span data-ttu-id="22e9d-221">選取 [**資料**] 類別，然後選取 [ **ADO.NET 實體資料模型**] 範本。</span><span class="sxs-lookup"><span data-stu-id="22e9d-221">Select the **Data** category and select the **ADO.NET Entity Data Model** template.</span></span>
3. <span data-ttu-id="22e9d-222">提供您的資料模型名稱*MoviesDBModel* ，然後按一下 [**新增**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22e9d-222">Give your data model the name *MoviesDBModel.edmx* and click the **Add** button.</span></span>

<span data-ttu-id="22e9d-223">按一下 [新增] 按鈕之後，[實體資料模型 Wizard] 隨即出現（請參閱 [圖 6]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-223">After you click the Add button, the Entity Data Model Wizard appears (see Figure 6).</span></span> <span data-ttu-id="22e9d-224">請遵循下列步驟來完成嚮導：</span><span class="sxs-lookup"><span data-stu-id="22e9d-224">Follow these steps to complete the wizard:</span></span>

1. <span data-ttu-id="22e9d-225">在 [**選擇模型內容**] 步驟中，選取 [**從資料庫產生**] 選項。</span><span class="sxs-lookup"><span data-stu-id="22e9d-225">In the **Choose Model Contents** step, select the **Generate from database** option.</span></span>
2. <span data-ttu-id="22e9d-226">在 [**選擇您的資料**連線] 步驟中，使用 [ *MoviesDB* ] 資料連線和 [連線設定] 的名稱*MoviesDBEntities* 。</span><span class="sxs-lookup"><span data-stu-id="22e9d-226">In the **Choose Your Data Connection** step, use the *MoviesDB.mdf* data connection and the name *MoviesDBEntities* for the connection settings.</span></span> <span data-ttu-id="22e9d-227">按 [**下一步]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22e9d-227">Click the **Next** button.</span></span>
3. <span data-ttu-id="22e9d-228">在 [**選擇您的資料庫物件**] 步驟中，展開 [資料表] 節點，選取 [電影] 資料表。</span><span class="sxs-lookup"><span data-stu-id="22e9d-228">In the **Choose Your Database Objects** step, expand the Tables node, select the Movies table.</span></span> <span data-ttu-id="22e9d-229">輸入命名空間*MovieApp* ，然後按一下 [**完成]** 按鈕。</span><span class="sxs-lookup"><span data-stu-id="22e9d-229">Enter the namespace *MovieApp.Models* and click the **Finish** button.</span></span>

<span data-ttu-id="22e9d-230">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-230">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image6.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.png)</span></span>

<span data-ttu-id="22e9d-231">**圖 06**：使用實體資料模型 Wizard 產生資料庫模型（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-231">**Figure 06**: Generating a database model with the Entity Data Model Wizard ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.png))</span></span>

<span data-ttu-id="22e9d-232">當您完成實體資料模型 Wizard 之後，實體資料模型設計工具隨即開啟。</span><span class="sxs-lookup"><span data-stu-id="22e9d-232">After you complete the Entity Data Model Wizard, the Entity Data Model Designer opens.</span></span> <span data-ttu-id="22e9d-233">設計工具應該會顯示電影資料庫資料表（請參閱 [圖 7]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-233">The Designer should display the Movies database table (see Figure 7).</span></span>

<span data-ttu-id="22e9d-234">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-234">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image7.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.png)</span></span>

<span data-ttu-id="22e9d-235">**圖 07**：實體資料模型設計工具（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-235">**Figure 07**: The Entity Data Model Designer ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.png))</span></span>

<span data-ttu-id="22e9d-236">我們需要先進行一項變更，才能繼續進行。</span><span class="sxs-lookup"><span data-stu-id="22e9d-236">We need to make one change before we continue.</span></span> <span data-ttu-id="22e9d-237">「實體資料」 Wizard 會產生名為「*電影*」的模型類別，代表電影資料庫資料表。</span><span class="sxs-lookup"><span data-stu-id="22e9d-237">The Entity Data Wizard generates a model class named *Movies* that represents the Movies database table.</span></span> <span data-ttu-id="22e9d-238">因為我們將使用 Movie 類別來代表特定電影，所以我們需要將類別的名稱修改成*電影*，而不是*電影*（單數而非複數）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-238">Because we'll use the Movies class to represent a particular movie, we need to modify the name of the class to be *Movie* instead of *Movies* (singular rather than plural).</span></span>

<span data-ttu-id="22e9d-239">按兩下設計工具介面上的類別名稱，並將類別的名稱從電影變更為 Movie。</span><span class="sxs-lookup"><span data-stu-id="22e9d-239">Double-click the name of the class on the designer surface and change the name of the class from Movies to Movie.</span></span> <span data-ttu-id="22e9d-240">進行這項變更之後，請按一下 [**儲存**] 按鈕（磁片磁碟機的圖示）以產生 Movie 類別。</span><span class="sxs-lookup"><span data-stu-id="22e9d-240">After making this change, click the **Save** button (the icon of the floppy disk) to generate the Movie class.</span></span>

## <a name="creating-the-aspnet-mvc-controller"></a><span data-ttu-id="22e9d-241">建立 ASP.NET MVC 控制器</span><span class="sxs-lookup"><span data-stu-id="22e9d-241">Creating the ASP.NET MVC Controller</span></span>

<span data-ttu-id="22e9d-242">下一個步驟是建立 ASP.NET MVC 控制器。</span><span class="sxs-lookup"><span data-stu-id="22e9d-242">The next step is to create the ASP.NET MVC controller.</span></span> <span data-ttu-id="22e9d-243">控制器負責控制使用者與 ASP.NET MVC 應用程式互動的方式。</span><span class="sxs-lookup"><span data-stu-id="22e9d-243">A controller is responsible for controlling how a user interacts with an ASP.NET MVC application.</span></span>

<span data-ttu-id="22e9d-244">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="22e9d-244">Follow these steps:</span></span>

1. <span data-ttu-id="22e9d-245">在 [方案總管] 視窗中，以滑鼠右鍵按一下 [控制器] 資料夾，然後選取 [**新增]、[控制器**] 功能表選項。</span><span class="sxs-lookup"><span data-stu-id="22e9d-245">In the Solution Explorer window, right-click the Controllers folder and select the menu option **Add, Controller**.</span></span>
2. <span data-ttu-id="22e9d-246">在 [新增控制器] 對話方塊中，輸入名稱*HomeController* ，並核取標示**為 [新增]、[更新] 和 [詳細資料案例] 的動作方法**（請參閱 [圖 8]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-246">In the Add Controller dialog, enter the name *HomeController* and check the checkbox labeled **Add action methods for Create, Update, and Details scenarios** (see Figure 8).</span></span>
3. <span data-ttu-id="22e9d-247">按一下 [**新增**] 按鈕，將新的控制器新增至您的專案。</span><span class="sxs-lookup"><span data-stu-id="22e9d-247">Click the **Add** button to add the new controller to your project.</span></span>

<span data-ttu-id="22e9d-248">完成這些步驟之後，即會建立 [清單 1] 中的控制器。</span><span class="sxs-lookup"><span data-stu-id="22e9d-248">After you complete these steps, the controller in Listing 1 is created.</span></span> <span data-ttu-id="22e9d-249">請注意，它包含名為 Index、Details、Create 和 Edit 的方法。</span><span class="sxs-lookup"><span data-stu-id="22e9d-249">Notice that it contains methods named Index, Details, Create, and Edit.</span></span> <span data-ttu-id="22e9d-250">在下列各節中，我們將新增必要的程式碼，以讓這些方法正常執行。</span><span class="sxs-lookup"><span data-stu-id="22e9d-250">In the following sections, we'll add the necessary code to get these methods to work.</span></span>

<span data-ttu-id="22e9d-251">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-251">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image8.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image15.png)</span></span>

<span data-ttu-id="22e9d-252">**圖 08**：加入新的 ASP.NET MVC 控制器（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-252">**Figure 08**: Adding a new ASP.NET MVC Controller ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image16.png))</span></span>

<span data-ttu-id="22e9d-253">**清單1– Controllers\HomeController.cs**</span><span class="sxs-lookup"><span data-stu-id="22e9d-253">**Listing 1 – Controllers\HomeController.cs**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample1.cs)]

## <a name="listing-database-records"></a><span data-ttu-id="22e9d-254">列出資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="22e9d-254">Listing Database Records</span></span>

<span data-ttu-id="22e9d-255">Home 控制器的 Index （）方法是 ASP.NET MVC 應用程式的預設方法。</span><span class="sxs-lookup"><span data-stu-id="22e9d-255">The Index() method of the Home controller is the default method for an ASP.NET MVC application.</span></span> <span data-ttu-id="22e9d-256">當您執行 ASP.NET MVC 應用程式時，Index （）方法是第一個呼叫的控制器方法。</span><span class="sxs-lookup"><span data-stu-id="22e9d-256">When you run an ASP.NET MVC application, the Index() method is the first controller method that is called.</span></span>

<span data-ttu-id="22e9d-257">我們將使用 Index （）方法來顯示電影資料庫資料表中的記錄清單。</span><span class="sxs-lookup"><span data-stu-id="22e9d-257">We'll use the Index() method to display the list of records from the Movies database table.</span></span> <span data-ttu-id="22e9d-258">我們將利用稍早建立的資料庫模型類別，以使用 Index （）方法來抓取電影資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-258">We'll take advantage of the database model classes that we created earlier to retrieve the movie database records with the Index() method.</span></span>

<span data-ttu-id="22e9d-259">我已修改 [清單 2] 中的 HomeController 類別，使其包含名為 \_db 的新私用欄位。</span><span class="sxs-lookup"><span data-stu-id="22e9d-259">I've modified the HomeController class in Listing 2 so that it contains a new private field named \_db.</span></span> <span data-ttu-id="22e9d-260">MoviesDBEntities 類別代表我們的資料庫模型，我們將使用此類別來與我們的資料庫通訊。</span><span class="sxs-lookup"><span data-stu-id="22e9d-260">The MoviesDBEntities class represents our database model and we'll use this class to communicate with our database.</span></span>

<span data-ttu-id="22e9d-261">我也修改了 [清單 2] 中的 Index （）方法。</span><span class="sxs-lookup"><span data-stu-id="22e9d-261">I've also modified the Index() method in Listing 2.</span></span> <span data-ttu-id="22e9d-262">Index （）方法會使用 MoviesDBEntities 類別來抓取電影資料庫資料表中的所有電影記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-262">The Index() method uses the MoviesDBEntities class to retrieve all of the movie records from the Movies database table.</span></span> <span data-ttu-id="22e9d-263">運算式 *\_db。MovieSet. ToList （）* 會傳回電影資料庫資料表中所有電影記錄的清單。</span><span class="sxs-lookup"><span data-stu-id="22e9d-263">The expression *\_db.MovieSet.ToList()* returns a list of all of the movie records from the Movies database table.</span></span>

<span data-ttu-id="22e9d-264">電影清單會傳遞至 view。</span><span class="sxs-lookup"><span data-stu-id="22e9d-264">The list of movies is passed to the view.</span></span> <span data-ttu-id="22e9d-265">傳遞至 view （）方法的任何專案都會以視圖資料的形式傳遞至 view。</span><span class="sxs-lookup"><span data-stu-id="22e9d-265">Anything that gets passed to the View() method gets passed to the view as view data.</span></span>

<span data-ttu-id="22e9d-266">**[清單 2] –控制器/HomeController .cs （已修改的索引方法）**</span><span class="sxs-lookup"><span data-stu-id="22e9d-266">**Listing 2 – Controllers/HomeController.cs (modified Index method)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample2.cs)]

<span data-ttu-id="22e9d-267">Index （）方法會傳回名為 Index 的 view。</span><span class="sxs-lookup"><span data-stu-id="22e9d-267">The Index() method returns a view named Index.</span></span> <span data-ttu-id="22e9d-268">我們必須建立此視圖，以顯示電影資料庫記錄的清單。</span><span class="sxs-lookup"><span data-stu-id="22e9d-268">We need to create this view to display the list of movie database records.</span></span> <span data-ttu-id="22e9d-269">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="22e9d-269">Follow these steps:</span></span>

<span data-ttu-id="22e9d-270">在開啟 [**加入視圖**] 對話方塊之前，您應該建立專案（選取 [**組建]、[組建方案**] 功能表選項），否則 [**視圖資料類別**] 下拉式清單中不會顯示任何類別。</span><span class="sxs-lookup"><span data-stu-id="22e9d-270">You should build your project (select the menu option **Build, Build Solution**) before opening the **Add View** dialog or no classes will appear in the **View data class** dropdown list.</span></span>

1. <span data-ttu-id="22e9d-271">以滑鼠右鍵按一下程式碼編輯器中的 Index （）方法，然後選取 [**新增視圖**] 功能表選項（請參閱 [圖 9]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-271">Right-click the Index() method in the code editor and select the menu option **Add View** (see Figure 9).</span></span>
2. <span data-ttu-id="22e9d-272">在 [加入視圖] 對話方塊中，確認已核取標示為 [**建立強型別視圖**] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="22e9d-272">In the Add View dialog, verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="22e9d-273">從 [**視圖內容**] 下拉式清單中，選取 [值]*清單*。</span><span class="sxs-lookup"><span data-stu-id="22e9d-273">From the **View content** dropdown list, select the value *List*.</span></span>
4. <span data-ttu-id="22e9d-274">從 [ **View data class** ] 下拉式清單中，選取 [ *MovieApp*] 值。</span><span class="sxs-lookup"><span data-stu-id="22e9d-274">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="22e9d-275">按一下 [新增] 按鈕以建立新的視圖（請參閱 [圖 10]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-275">Click the Add button to create the new view (see Figure 10).</span></span>

<span data-ttu-id="22e9d-276">完成這些步驟之後，名為 Views\Home 的新視圖會新增至 [] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="22e9d-276">After you complete these steps, a new view named Index.aspx is added to the Views\Home folder.</span></span> <span data-ttu-id="22e9d-277">索引視圖的內容包含在 [清單 3] 中。</span><span class="sxs-lookup"><span data-stu-id="22e9d-277">The contents of the Index view are included in Listing 3.</span></span>

<span data-ttu-id="22e9d-278">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-278">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image9.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image17.png)</span></span>

<span data-ttu-id="22e9d-279">**圖 09**：從控制器動作加入視圖（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-279">**Figure 09**: Adding a view from a controller action ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image18.png))</span></span>

<span data-ttu-id="22e9d-280">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-280">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image10.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image19.png)</span></span>

<span data-ttu-id="22e9d-281">**圖 10**：使用 [加入視圖] 對話方塊來建立新的視圖（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-281">**Figure 10**: Creating a new view with the Add View dialog ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image20.png))</span></span>

<span data-ttu-id="22e9d-282">**清單3– Views\Home\Index.aspx**</span><span class="sxs-lookup"><span data-stu-id="22e9d-282">**Listing 3 – Views\Home\Index.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample3.aspx)]

<span data-ttu-id="22e9d-283">[索引] 視圖會顯示 HTML 資料表中電影資料庫資料表的所有電影記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-283">The Index view displays all of the movie records from the Movies database table within an HTML table.</span></span> <span data-ttu-id="22e9d-284">此視圖包含一個 foreach 迴圈，可逐一查看 ViewData 屬性所代表的每個電影。</span><span class="sxs-lookup"><span data-stu-id="22e9d-284">The view contains a foreach loop that iterates through each movie represented by the ViewData.Model property.</span></span> <span data-ttu-id="22e9d-285">如果您按 F5 鍵來執行應用程式，則會看到 [圖 11] 中的網頁。</span><span class="sxs-lookup"><span data-stu-id="22e9d-285">If you run your application by hitting the F5 key, then you'll see the web page in Figure 11.</span></span>

<span data-ttu-id="22e9d-286">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-286">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image11.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image21.png)</span></span>

<span data-ttu-id="22e9d-287">**圖 11**：索引視圖（[按一下以查看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-287">**Figure 11**: The Index view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image22.png))</span></span>

## <a name="creating-new-database-records"></a><span data-ttu-id="22e9d-288">建立新的資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="22e9d-288">Creating New Database Records</span></span>

<span data-ttu-id="22e9d-289">我們在上一節中建立的索引視圖包含用來建立新資料庫記錄的連結。</span><span class="sxs-lookup"><span data-stu-id="22e9d-289">The Index view that we created in the previous section includes a link for creating new database records.</span></span> <span data-ttu-id="22e9d-290">讓我們繼續執行邏輯，並建立建立新電影資料庫記錄所需的視圖。</span><span class="sxs-lookup"><span data-stu-id="22e9d-290">Let's go ahead and implement the logic and create the view necessary for creating new movie database records.</span></span>

<span data-ttu-id="22e9d-291">Home 控制器包含兩個名為 Create （）的方法。</span><span class="sxs-lookup"><span data-stu-id="22e9d-291">The Home controller contains two methods named Create().</span></span> <span data-ttu-id="22e9d-292">第一個 Create （）方法沒有參數。</span><span class="sxs-lookup"><span data-stu-id="22e9d-292">The first Create() method has no parameters.</span></span> <span data-ttu-id="22e9d-293">Create （）方法的這個多載會用來顯示用來建立新電影資料庫記錄的 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="22e9d-293">This overload of the Create() method is used to display the HTML form for creating a new movie database record.</span></span>

<span data-ttu-id="22e9d-294">第二個 Create （）方法具有 FormCollection 參數。</span><span class="sxs-lookup"><span data-stu-id="22e9d-294">The second Create() method has a FormCollection parameter.</span></span> <span data-ttu-id="22e9d-295">當建立新電影的 HTML 表單張貼至伺服器時，會呼叫 Create （）方法的這個多載。</span><span class="sxs-lookup"><span data-stu-id="22e9d-295">This overload of the Create() method is called when the HTML form for creating a new movie is posted to the server.</span></span> <span data-ttu-id="22e9d-296">請注意，第二個 Create （）方法有一個 AcceptVerbs 屬性，可防止呼叫方法，除非執行 HTTP POST 作業。</span><span class="sxs-lookup"><span data-stu-id="22e9d-296">Notice that this second Create() method has an AcceptVerbs attribute that prevents the method from being called unless an HTTP POST operation is performed.</span></span>

<span data-ttu-id="22e9d-297">第二個 Create （）方法已在清單4中已更新的 HomeController 類別中修改。</span><span class="sxs-lookup"><span data-stu-id="22e9d-297">This second Create() method has been modified in the updated HomeController class in Listing 4.</span></span> <span data-ttu-id="22e9d-298">新版本的 Create （）方法會接受 Movie 參數，並包含將新電影插入電影資料庫資料表的邏輯。</span><span class="sxs-lookup"><span data-stu-id="22e9d-298">The new version of the Create() method accepts a Movie parameter and contains the logic for inserting a new movie into the Movies database table.</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="22e9d-299">請注意 Bind 屬性。</span><span class="sxs-lookup"><span data-stu-id="22e9d-299">Notice the Bind attribute.</span></span> <span data-ttu-id="22e9d-300">因為我們不想要從 HTML 表單更新 Movie Id 屬性，所以我們需要明確排除這個屬性。</span><span class="sxs-lookup"><span data-stu-id="22e9d-300">Because we don't want to update the Movie Id property from HTML form, we need to explicitly exclude this property.</span></span>

<span data-ttu-id="22e9d-301">**清單4– Controllers\HomeController.cs （已修改的 Create 方法）**</span><span class="sxs-lookup"><span data-stu-id="22e9d-301">**Listing 4 – Controllers\HomeController.cs (modified Create method)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample4.cs)]

<span data-ttu-id="22e9d-302">Visual Studio 可讓您輕鬆建立建立新電影資料庫記錄的表單（請參閱 [圖 12]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-302">Visual Studio makes it easy to create the form for creating a new movie database record (see Figure 12).</span></span> <span data-ttu-id="22e9d-303">請依照下列步驟：</span><span class="sxs-lookup"><span data-stu-id="22e9d-303">Follow these steps:</span></span>

1. <span data-ttu-id="22e9d-304">以滑鼠右鍵按一下程式碼編輯器中的 Create （）方法，然後選取功能表選項 [**加入視圖**]。</span><span class="sxs-lookup"><span data-stu-id="22e9d-304">Right-click the Create() method in the code editor and select the menu option **Add View**.</span></span>
2. <span data-ttu-id="22e9d-305">確認已核取標示為 [**建立強型別視圖**] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="22e9d-305">Verify that the checkbox labeled **Create a strongly-typed view** is checked.</span></span>
3. <span data-ttu-id="22e9d-306">從 [**視圖內容**] 下拉式清單中，選取 [*建立*] 值。</span><span class="sxs-lookup"><span data-stu-id="22e9d-306">From the **View content** dropdown list, select the value *Create*.</span></span>
4. <span data-ttu-id="22e9d-307">從 [ **View data class** ] 下拉式清單中，選取 [ *MovieApp*] 值。</span><span class="sxs-lookup"><span data-stu-id="22e9d-307">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="22e9d-308">按一下 [**新增**] 按鈕以建立新的視圖。</span><span class="sxs-lookup"><span data-stu-id="22e9d-308">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="22e9d-309">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-309">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image12.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image23.png)</span></span>

<span data-ttu-id="22e9d-310">**圖 12**：新增 Create View （[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-310">**Figure 12**: Adding the Create view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image24.png))</span></span>

<span data-ttu-id="22e9d-311">Visual Studio 會自動產生清單5中的視圖。</span><span class="sxs-lookup"><span data-stu-id="22e9d-311">Visual Studio generates the view in Listing 5 automatically.</span></span> <span data-ttu-id="22e9d-312">此視圖包含 HTML 表單，其中包含的欄位會對應至 Movie 類別的每個屬性。</span><span class="sxs-lookup"><span data-stu-id="22e9d-312">This view contains an HTML form that includes fields that correspond to each of the properties of the Movie class.</span></span>

<span data-ttu-id="22e9d-313">**清單5– Views\Home\Create.aspx**</span><span class="sxs-lookup"><span data-stu-id="22e9d-313">**Listing 5 – Views\Home\Create.aspx**</span></span>

[!code-aspx[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample5.aspx)]

> [!NOTE] 
> 
> <span data-ttu-id="22e9d-314">[加入視圖] 對話方塊所產生的 HTML 表單會產生識別碼表單欄位。</span><span class="sxs-lookup"><span data-stu-id="22e9d-314">The HTML form generated by the Add View dialog generates an Id form field.</span></span> <span data-ttu-id="22e9d-315">因為 Id 資料行是識別欄位，所以我們不需要此表單欄位，因此您可以放心地將它移除。</span><span class="sxs-lookup"><span data-stu-id="22e9d-315">Because the Id column is an Identity column, we don't need this form field and you can safely remove it.</span></span>

<span data-ttu-id="22e9d-316">新增 [建立] 視圖之後，您可以將新的電影記錄新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="22e9d-316">After you add the Create view, you can add new Movie records to the database.</span></span> <span data-ttu-id="22e9d-317">按 F5 鍵執行您的應用程式，然後按一下 [建立新的] 連結以查看 [圖 13] 中的表單。</span><span class="sxs-lookup"><span data-stu-id="22e9d-317">Run your application by pressing the F5 key and click the Create New link to see the form in Figure 13.</span></span> <span data-ttu-id="22e9d-318">如果您完成並提交表單，則會建立新的電影資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-318">If you complete and submit the form, a new movie database record is created.</span></span>

<span data-ttu-id="22e9d-319">請注意，您會自動取得表單驗證。</span><span class="sxs-lookup"><span data-stu-id="22e9d-319">Notice that you get form validation automatically.</span></span> <span data-ttu-id="22e9d-320">如果您不想輸入電影的發行日期，或輸入了不正確發行日期，則會重新顯示表單，並醒目提示 [發行日期] 欄位。</span><span class="sxs-lookup"><span data-stu-id="22e9d-320">If you neglect to enter a release date for a movie, or you enter an invalid release date, then the form is redisplayed and the release date field is highlighted.</span></span>

<span data-ttu-id="22e9d-321">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-321">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image13.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image25.png)</span></span>

<span data-ttu-id="22e9d-322">**圖 13**：建立新的電影資料庫記錄（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-322">**Figure 13**: Creating a new movie database record ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image26.png))</span></span>

## <a name="editing-existing-database-records"></a><span data-ttu-id="22e9d-323">編輯現有的資料庫記錄</span><span class="sxs-lookup"><span data-stu-id="22e9d-323">Editing Existing Database Records</span></span>

<span data-ttu-id="22e9d-324">在先前的章節中，我們討論了如何列出和建立新的資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-324">In the previous sections, we discussed how you can list and create new database records.</span></span> <span data-ttu-id="22e9d-325">在最後一節中，我們會討論如何編輯現有的資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-325">In this final section, we discuss how you can edit existing database records.</span></span>

<span data-ttu-id="22e9d-326">首先，我們需要產生編輯表單。</span><span class="sxs-lookup"><span data-stu-id="22e9d-326">First, we need to generate the Edit form.</span></span> <span data-ttu-id="22e9d-327">這個步驟很簡單，因為 Visual Studio 會自動為我們產生編輯表單。</span><span class="sxs-lookup"><span data-stu-id="22e9d-327">This step is easy since Visual Studio will generate the Edit form for us automatically.</span></span> <span data-ttu-id="22e9d-328">在 Visual Studio 程式碼編輯器中開啟 HomeController.cs 類別，並遵循下列步驟：</span><span class="sxs-lookup"><span data-stu-id="22e9d-328">Open the HomeController.cs class in the Visual Studio code editor and follow these steps:</span></span>

1. <span data-ttu-id="22e9d-329">以滑鼠右鍵按一下程式碼編輯器中的 Edit （）方法，然後選取 [**新增視圖**] 功能表選項（請參閱 [圖 14]）。</span><span class="sxs-lookup"><span data-stu-id="22e9d-329">Right-click the Edit() method in the code editor and select the menu option **Add View** (see Figure 14).</span></span>
2. <span data-ttu-id="22e9d-330">核取標示為 [**建立強型別的視圖**] 的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="22e9d-330">Check the checkbox labeled **Create a strongly-typed view**.</span></span>
3. <span data-ttu-id="22e9d-331">從 [**視圖內容**] 下拉式清單中，選取 [*編輯*] 值。</span><span class="sxs-lookup"><span data-stu-id="22e9d-331">From the **View content** dropdown list, select the value *Edit*.</span></span>
4. <span data-ttu-id="22e9d-332">從 [ **View data class** ] 下拉式清單中，選取 [ *MovieApp*] 值。</span><span class="sxs-lookup"><span data-stu-id="22e9d-332">From the **View data class** dropdown list, select the value *MovieApp.Models.Movie*.</span></span>
5. <span data-ttu-id="22e9d-333">按一下 [**新增**] 按鈕以建立新的視圖。</span><span class="sxs-lookup"><span data-stu-id="22e9d-333">Click the **Add** button to create the new view.</span></span>

<span data-ttu-id="22e9d-334">完成這些步驟之後，會將名為 Edit 的新視圖加入至 Views\Home 資料夾。</span><span class="sxs-lookup"><span data-stu-id="22e9d-334">Completing these steps adds a new view named Edit.aspx to the Views\Home folder.</span></span> <span data-ttu-id="22e9d-335">此視圖包含用於編輯電影記錄的 HTML 表單。</span><span class="sxs-lookup"><span data-stu-id="22e9d-335">This view contains an HTML form for editing a movie record.</span></span>

<span data-ttu-id="22e9d-336">[![[新增專案] 對話方塊](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)</span><span class="sxs-lookup"><span data-stu-id="22e9d-336">[![The New Project dialog box](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image14.jpg)](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image27.png)</span></span>

<span data-ttu-id="22e9d-337">**圖 14**：新增編輯檢視（[按一下以觀看完整大小的影像](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png)）</span><span class="sxs-lookup"><span data-stu-id="22e9d-337">**Figure 14**: Adding the Edit view ([Click to view full-size image](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/_static/image28.png))</span></span>

> [!NOTE] 
> 
> <span data-ttu-id="22e9d-338">編輯檢視包含一個對應于 Movie Id 屬性的 HTML 表單欄位。</span><span class="sxs-lookup"><span data-stu-id="22e9d-338">The Edit view contains an HTML form field that corresponds to the Movie Id property.</span></span> <span data-ttu-id="22e9d-339">因為您不想讓人員編輯 Id 屬性的值，所以您應該移除此表單欄位。</span><span class="sxs-lookup"><span data-stu-id="22e9d-339">Because you don't want people editing the value of the Id property, you should remove this form field.</span></span>

<span data-ttu-id="22e9d-340">最後，我們需要修改「主控制器」，讓它支援編輯資料庫記錄。</span><span class="sxs-lookup"><span data-stu-id="22e9d-340">Finally, we need to modify the Home controller so that it supports editing a database record.</span></span> <span data-ttu-id="22e9d-341">已更新的 HomeController 類別包含在 [清單 6] 中。</span><span class="sxs-lookup"><span data-stu-id="22e9d-341">The updated HomeController class is contained in Listing 6.</span></span>

<span data-ttu-id="22e9d-342">**清單6– Controllers\HomeController.cs （編輯方法）**</span><span class="sxs-lookup"><span data-stu-id="22e9d-342">**Listing 6 – Controllers\HomeController.cs (Edit methods)**</span></span>

[!code-csharp[Main](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-cs/samples/sample6.cs)]

<span data-ttu-id="22e9d-343">在 [清單 6] 中，我已將其他邏輯新增至 Edit （）方法的兩個多載。</span><span class="sxs-lookup"><span data-stu-id="22e9d-343">In Listing 6, I've added additional logic to both overloads of the Edit() method.</span></span> <span data-ttu-id="22e9d-344">第一個 Edit （）方法會傳回電影資料庫記錄，其對應至傳遞給方法的 Id 參數。</span><span class="sxs-lookup"><span data-stu-id="22e9d-344">The first Edit() method returns the movie database record that corresponds to the Id parameter passed to the method.</span></span> <span data-ttu-id="22e9d-345">第二個多載會執行資料庫中電影記錄的更新。</span><span class="sxs-lookup"><span data-stu-id="22e9d-345">The second overload performs the updates to a movie record in the database.</span></span>

<span data-ttu-id="22e9d-346">請注意，您必須取出原始電影，然後呼叫 ApplyPropertyChanges （），以更新資料庫中的現有電影。</span><span class="sxs-lookup"><span data-stu-id="22e9d-346">Notice that you must retrieve the original movie, and then call ApplyPropertyChanges(), to update the existing movie in the database.</span></span>

## <a name="summary"></a><span data-ttu-id="22e9d-347">總結</span><span class="sxs-lookup"><span data-stu-id="22e9d-347">Summary</span></span>

<span data-ttu-id="22e9d-348">本教學課程的目的是要讓您瞭解建立 ASP.NET MVC 應用程式的體驗。</span><span class="sxs-lookup"><span data-stu-id="22e9d-348">The purpose of this tutorial was to give you a sense of the experience of building an ASP.NET MVC application.</span></span> <span data-ttu-id="22e9d-349">我希望您發現建立 ASP.NET MVC web 應用程式非常類似于建立 Active Server Pages 或 ASP.NET 應用程式的體驗。</span><span class="sxs-lookup"><span data-stu-id="22e9d-349">I hope that you discovered that building an ASP.NET MVC web application is very similar to the experience of building an Active Server Pages or ASP.NET application.</span></span>

<span data-ttu-id="22e9d-350">在本教學課程中，我們只會檢查 ASP.NET MVC 架構的最基本功能。</span><span class="sxs-lookup"><span data-stu-id="22e9d-350">In this tutorial, we examined only the most basic features of the ASP.NET MVC framework.</span></span> <span data-ttu-id="22e9d-351">在未來的教學課程中，我們將深入探討控制器、控制器動作、視圖、視圖資料和 HTML 協助程式等主題。</span><span class="sxs-lookup"><span data-stu-id="22e9d-351">In future tutorials, we dive deeper into topics such as controllers, controller actions, views, view data, and HTML helpers.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="22e9d-352">下一步</span><span class="sxs-lookup"><span data-stu-id="22e9d-352">Next</span></span>](create-a-movie-database-application-in-15-minutes-with-asp-net-mvc-vb.md)
