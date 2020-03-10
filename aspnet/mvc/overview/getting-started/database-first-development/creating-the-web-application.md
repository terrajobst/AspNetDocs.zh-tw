---
uid: mvc/overview/getting-started/database-first-development/creating-the-web-application
title: 教學課程：使用 ASP.NET MVC 建立 EF Database First 的 Web 應用程式和資料模型
description: 本教學課程著重于建立 web 應用程式，並根據您的資料庫資料表產生資料模型。
author: Rick-Anderson
ms.author: riande
ms.date: 01/28/2019
ms.topic: tutorial
ms.assetid: bc8f2bd5-ff57-4dcd-8418-a5bd517d8953
msc.legacyurl: /mvc/overview/getting-started/database-first-development/creating-the-web-application
msc.type: authoredcontent
ms.openlocfilehash: 30fd42be5677df6fa6ee0630914098c30d21385b
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616267"
---
# <a name="tutorial-create-the-web-application-and-data-models-for-ef-database-first-with-aspnet-mvc"></a><span data-ttu-id="28fb2-103">教學課程：使用 ASP.NET MVC 建立 EF Database First 的 Web 應用程式和資料模型</span><span class="sxs-lookup"><span data-stu-id="28fb2-103">Tutorial: Create the Web Application and Data Models for EF Database First with ASP.NET MVC</span></span>

 <span data-ttu-id="28fb2-104">使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="28fb2-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="28fb2-105">本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="28fb2-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="28fb2-106">產生的程式碼會對應至資料庫資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="28fb2-106">The generated code corresponds to the columns in the database table.</span></span>

<span data-ttu-id="28fb2-107">本教學課程著重于建立 web 應用程式，並根據您的資料庫資料表產生資料模型。</span><span class="sxs-lookup"><span data-stu-id="28fb2-107">This tutorial focuses on creating the web application, and generating the data models based on your database tables.</span></span>

<span data-ttu-id="28fb2-108">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="28fb2-108">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="28fb2-109">建立 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="28fb2-109">Create an ASP.NET web app</span></span>
> * <span data-ttu-id="28fb2-110">產生模型</span><span class="sxs-lookup"><span data-stu-id="28fb2-110">Generate the models</span></span>

## <a name="prerequisites"></a><span data-ttu-id="28fb2-111">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="28fb2-111">Prerequisites</span></span>

* [<span data-ttu-id="28fb2-112">使用 MVC 5 開始使用 Entity Framework 6 Database First</span><span class="sxs-lookup"><span data-stu-id="28fb2-112">Getting started with Entity Framework 6 Database First using MVC 5</span></span>](setting-up-database.md)

## <a name="create-an-aspnet-web-app"></a><span data-ttu-id="28fb2-113">建立 ASP.NET Web 應用程式</span><span class="sxs-lookup"><span data-stu-id="28fb2-113">Create an ASP.NET web app</span></span>

<span data-ttu-id="28fb2-114">在新方案或與資料庫專案相同的方案中，在 Visual Studio 中建立新的專案，然後選取 [ **ASP.NET Web 應用程式**] 範本。</span><span class="sxs-lookup"><span data-stu-id="28fb2-114">In either a new solution or the same solution as the database project, create a new project in Visual Studio and select the **ASP.NET Web Application** template.</span></span> <span data-ttu-id="28fb2-115">將專案命名為**ContosoSite**。</span><span class="sxs-lookup"><span data-stu-id="28fb2-115">Name the project **ContosoSite**.</span></span>

![建立專案](creating-the-web-application/_static/image1.png)

<span data-ttu-id="28fb2-117">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="28fb2-117">Click **OK**.</span></span>

<span data-ttu-id="28fb2-118">在 [新增 ASP.NET 專案] 視窗中，選取 [ **MVC** ] 範本。</span><span class="sxs-lookup"><span data-stu-id="28fb2-118">In the New ASP.NET Project window, select the **MVC** template.</span></span> <span data-ttu-id="28fb2-119">您現在可以清除 **[雲端中的主機**] 選項，因為您稍後會將應用程式部署至雲端。</span><span class="sxs-lookup"><span data-stu-id="28fb2-119">You can clear the **Host in the cloud** option for now because you will deploy the application to the cloud later.</span></span> <span data-ttu-id="28fb2-120">按一下 **[確定]** 以建立應用程式。</span><span class="sxs-lookup"><span data-stu-id="28fb2-120">Click **OK** to create the application.</span></span>

<span data-ttu-id="28fb2-121">專案會使用預設檔案和資料夾來建立。</span><span class="sxs-lookup"><span data-stu-id="28fb2-121">The project is created with the default files and folders.</span></span>

<span data-ttu-id="28fb2-122">在本教學課程中，您將使用 Entity Framework 6。</span><span class="sxs-lookup"><span data-stu-id="28fb2-122">In this tutorial, you will use Entity Framework 6.</span></span> <span data-ttu-id="28fb2-123">您可以透過 [管理 NuGet 封裝] 視窗，再次檢查項目中的 Entity Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="28fb2-123">You can double-check the version of Entity Framework in your project through the Manage NuGet Packages window.</span></span> <span data-ttu-id="28fb2-124">如有必要，請更新您的 Entity Framework 版本。</span><span class="sxs-lookup"><span data-stu-id="28fb2-124">If necessary, update your version of Entity Framework.</span></span>

![顯示版本](creating-the-web-application/_static/image3.png)

## <a name="generate-the-models"></a><span data-ttu-id="28fb2-126">產生模型</span><span class="sxs-lookup"><span data-stu-id="28fb2-126">Generate the models</span></span>

<span data-ttu-id="28fb2-127">您現在將從資料庫資料表建立 Entity Framework 模型。</span><span class="sxs-lookup"><span data-stu-id="28fb2-127">You will now create Entity Framework models from the database tables.</span></span> <span data-ttu-id="28fb2-128">這些模型是您將用來處理資料的類別。</span><span class="sxs-lookup"><span data-stu-id="28fb2-128">These models are classes that you will use to work with the data.</span></span> <span data-ttu-id="28fb2-129">每個模型都會鏡像資料庫中的資料表，並包含對應至資料表中資料行的屬性。</span><span class="sxs-lookup"><span data-stu-id="28fb2-129">Each model mirrors a table in the database and contains properties that correspond to the columns in the table.</span></span>

<span data-ttu-id="28fb2-130">以滑鼠右鍵按一下 [**模型**] 資料夾，然後選取 [**加入**] 和 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="28fb2-130">Right-click the **Models** folder, and select **Add** and **New Item**.</span></span>

<span data-ttu-id="28fb2-131">在 加入新專案 視窗中，選取左窗格中的 **資料**，然後從中間窗格的選項**ADO.NET 實體資料模型**。</span><span class="sxs-lookup"><span data-stu-id="28fb2-131">In the Add New Item window, select **Data** in the left pane and **ADO.NET Entity Data Model** from the options in the center pane.</span></span> <span data-ttu-id="28fb2-132">將新的模型檔案命名為**ContosoModel**。</span><span class="sxs-lookup"><span data-stu-id="28fb2-132">Name the new model file **ContosoModel**.</span></span>

<span data-ttu-id="28fb2-133">按一下 [新增]。</span><span class="sxs-lookup"><span data-stu-id="28fb2-133">Click **Add**.</span></span>

<span data-ttu-id="28fb2-134">在實體資料模型 Wizard 中，從 [資料庫] 選取 [ **EF Designer**]。</span><span class="sxs-lookup"><span data-stu-id="28fb2-134">In the Entity Data Model Wizard, select **EF Designer from database**.</span></span>

<span data-ttu-id="28fb2-135">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="28fb2-135">Click **Next**.</span></span>

<span data-ttu-id="28fb2-136">如果您的開發環境內已定義資料庫連接，您可能會看到其中一個預先選取的連接。</span><span class="sxs-lookup"><span data-stu-id="28fb2-136">If you have database connections defined within your development environment, you may see one of these connections pre-selected.</span></span> <span data-ttu-id="28fb2-137">不過，您想要建立與您在本教學課程的第一個部分中所建立之資料庫的新連接。</span><span class="sxs-lookup"><span data-stu-id="28fb2-137">However, you want to create a new connection to the database you created in the first part of this tutorial.</span></span> <span data-ttu-id="28fb2-138">按一下 [**新增連接**] 按鈕。</span><span class="sxs-lookup"><span data-stu-id="28fb2-138">Click the **New Connection** button.</span></span>

<span data-ttu-id="28fb2-139">在 連線屬性視窗中，提供您的資料庫建立所在之本機伺服器的名稱（在此案例中為 **（localdb） \ProjectsV13**）。</span><span class="sxs-lookup"><span data-stu-id="28fb2-139">In the Connection Properties window, provide the name of the local server where your database was created (in this case **(localdb)\ProjectsV13**).</span></span> <span data-ttu-id="28fb2-140">提供伺服器名稱之後，請從可用的資料庫中選取 ContosoUniversityData。</span><span class="sxs-lookup"><span data-stu-id="28fb2-140">After providing the server name, select the ContosoUniversityData from the available databases.</span></span>

![設定連接屬性](creating-the-web-application/_static/image8.png)

<span data-ttu-id="28fb2-142">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="28fb2-142">Click **OK**.</span></span>

<span data-ttu-id="28fb2-143">現在會顯示正確的連接屬性。</span><span class="sxs-lookup"><span data-stu-id="28fb2-143">The correct connection properties are now displayed.</span></span> <span data-ttu-id="28fb2-144">在 web.config 檔案中，您可以使用預設名稱來連接。</span><span class="sxs-lookup"><span data-stu-id="28fb2-144">You can use the default name for connection in the Web.Config file.</span></span>

<span data-ttu-id="28fb2-145">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="28fb2-145">Click **Next**.</span></span>

<span data-ttu-id="28fb2-146">選取最新版本的 Entity Framework。</span><span class="sxs-lookup"><span data-stu-id="28fb2-146">Select the latest version of Entity Framework.</span></span>

<span data-ttu-id="28fb2-147">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="28fb2-147">Click **Next**.</span></span>

<span data-ttu-id="28fb2-148">選取 [**資料表]** ，為所有三個數據表產生模型。</span><span class="sxs-lookup"><span data-stu-id="28fb2-148">Select **Tables** to generate models for all three tables.</span></span>

<span data-ttu-id="28fb2-149">按一下 [完成] **Walkthrough: Calling Code in an VSTO Add-in from VBA**。</span><span class="sxs-lookup"><span data-stu-id="28fb2-149">Click **Finish**.</span></span>

<span data-ttu-id="28fb2-150">如果您收到安全性警告，請選取 **[確定]** 繼續執行範本。</span><span class="sxs-lookup"><span data-stu-id="28fb2-150">If you receive a security warning, select **OK** to continue running the template.</span></span>

<span data-ttu-id="28fb2-151">系統會從資料庫資料表產生模型，並顯示一個圖表，其中顯示資料表之間的屬性和關聯性。</span><span class="sxs-lookup"><span data-stu-id="28fb2-151">The models are generated from the database tables, and a diagram is displayed that shows the properties and relationships between the tables.</span></span>

![模型的圖表](creating-the-web-application/_static/image11.png)

<span data-ttu-id="28fb2-153">[模型] 資料夾現在包含許多與從資料庫產生之模型相關的新檔案。</span><span class="sxs-lookup"><span data-stu-id="28fb2-153">The Models folder now includes many new files related to the models that were generated from the database.</span></span>

<span data-ttu-id="28fb2-154">**ContosoModel.CoNtext.cs**檔案包含衍生自**DbCoNtext**類別的類別，並針對對應至資料庫資料表的每個模型類別提供屬性。</span><span class="sxs-lookup"><span data-stu-id="28fb2-154">The **ContosoModel.Context.cs** file contains a class that derives from the **DbContext** class, and provides a property for each model class that corresponds to a database table.</span></span> <span data-ttu-id="28fb2-155">**Course.cs**、 **Enrollment.cs**和**Student.cs**檔案包含代表資料庫資料表的模型類別。</span><span class="sxs-lookup"><span data-stu-id="28fb2-155">The **Course.cs**, **Enrollment.cs**, and **Student.cs** files contain the model classes that represent the databases tables.</span></span> <span data-ttu-id="28fb2-156">使用樣板時，您將會同時使用內容類別和模型類別。</span><span class="sxs-lookup"><span data-stu-id="28fb2-156">You will use both the context class and the model classes when working with scaffolding.</span></span>

<span data-ttu-id="28fb2-157">繼續進行本教學課程之前，請先建立專案。</span><span class="sxs-lookup"><span data-stu-id="28fb2-157">Before proceeding with this tutorial, build the project.</span></span> <span data-ttu-id="28fb2-158">在下一節中，您將會根據資料模型產生程式碼，但如果尚未建立專案，該區段將無法使用。</span><span class="sxs-lookup"><span data-stu-id="28fb2-158">In the next section, you will generate code based on the data models, but that section will not work if the project has not been built.</span></span>

## <a name="next-steps"></a><span data-ttu-id="28fb2-159">後續步驟</span><span class="sxs-lookup"><span data-stu-id="28fb2-159">Next steps</span></span>

<span data-ttu-id="28fb2-160">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="28fb2-160">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="28fb2-161">建立 ASP.NET web 應用程式</span><span class="sxs-lookup"><span data-stu-id="28fb2-161">Created an ASP.NET web app</span></span>
> * <span data-ttu-id="28fb2-162">產生模型</span><span class="sxs-lookup"><span data-stu-id="28fb2-162">Generated the models</span></span>

<span data-ttu-id="28fb2-163">前進到下一個教學課程，以瞭解如何建立以資料模型為基礎的產生程式碼。</span><span class="sxs-lookup"><span data-stu-id="28fb2-163">Advance to the next tutorial to learn how to create generate code based on the data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="28fb2-164">產生視圖</span><span class="sxs-lookup"><span data-stu-id="28fb2-164">Generating views</span></span>](generating-views.md)
