---
uid: mvc/overview/getting-started/database-first-development/setting-up-database
title: 教學課程：使用 MVC 5 開始使用 EF Database First
description: 本教學課程示範如何從現有的資料庫開始，並快速建立可讓使用者與資料互動的 web 應用程式。
author: Rick-Anderson
ms.author: riande
ms.date: 01/15/2019
ms.topic: tutorial
ms.assetid: 095abad4-3bfe-4f06-b092-ae6a735b7e49
msc.legacyurl: /mvc/overview/getting-started/database-first-development/setting-up-database
msc.type: authoredcontent
ms.openlocfilehash: a760767839a834a9c7e9fe358a3fd806a833261f
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78583521"
---
# <a name="tutorial-get-started-with-ef-database-first-using-mvc-5"></a><span data-ttu-id="6adb8-103">教學課程：使用 MVC 5 開始使用 EF Database First</span><span class="sxs-lookup"><span data-stu-id="6adb8-103">Tutorial: Get started with EF Database First using MVC 5</span></span>

<span data-ttu-id="6adb8-104">使用 MVC、Entity Framework 和 ASP.NET 的樣板，您可以建立 web 應用程式，以提供介面給現有的資料庫。</span><span class="sxs-lookup"><span data-stu-id="6adb8-104">Using MVC, Entity Framework, and ASP.NET Scaffolding, you can create a web application that provides an interface to an existing database.</span></span> <span data-ttu-id="6adb8-105">本教學課程系列會示範如何自動產生程式碼，讓使用者可以顯示、編輯、建立和刪除位於資料庫資料表中的資料。</span><span class="sxs-lookup"><span data-stu-id="6adb8-105">This tutorial series shows you how to automatically generate code that enables users to display, edit, create, and delete data that resides in a database table.</span></span> <span data-ttu-id="6adb8-106">產生的程式碼會對應至資料庫資料表中的資料行。</span><span class="sxs-lookup"><span data-stu-id="6adb8-106">The generated code corresponds to the columns in the database table.</span></span> <span data-ttu-id="6adb8-107">在此系列的最後一個部分中，您將瞭解如何將資料批註加入至資料模型，以指定驗證需求和顯示格式。</span><span class="sxs-lookup"><span data-stu-id="6adb8-107">In the last part of the series, you learn how add data annotations to the data model to specify validation requirements and display formatting.</span></span> <span data-ttu-id="6adb8-108">當您完成時，您可以前進到 Azure 文章，以瞭解如何將 .NET 應用程式和 SQL database 部署到 Azure App Service。</span><span class="sxs-lookup"><span data-stu-id="6adb8-108">When you're done, you can advance to an Azure article to learn how to deploy a .NET app and SQL database to Azure App Service.</span></span>

<span data-ttu-id="6adb8-109">本教學課程示範如何從現有的資料庫開始，並快速建立可讓使用者與資料互動的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6adb8-109">This tutorial shows how to start with an existing database and quickly create a web application that enables users to interact with the data.</span></span> <span data-ttu-id="6adb8-110">它會使用 Entity Framework 6 和 MVC 5 來建立 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6adb8-110">It uses the Entity Framework 6 and MVC 5 to build the web application.</span></span> <span data-ttu-id="6adb8-111">ASP.NET 的 [樣板] 功能可讓您自動產生程式碼來顯示、更新、建立和刪除資料。</span><span class="sxs-lookup"><span data-stu-id="6adb8-111">The ASP.NET Scaffolding feature enables you to automatically generate code for displaying, updating, creating and deleting data.</span></span> <span data-ttu-id="6adb8-112">您可以使用 Visual Studio 內的發佈工具，輕鬆地將網站和資料庫部署至 Azure。</span><span class="sxs-lookup"><span data-stu-id="6adb8-112">Using the publishing tools within Visual Studio, you can easily deploy the site and database to Azure.</span></span>

<span data-ttu-id="6adb8-113">這部分的系列內容著重于建立資料庫，並將資料填入其中。</span><span class="sxs-lookup"><span data-stu-id="6adb8-113">This part of the series focuses on creating a database and populating it with data.</span></span>

<span data-ttu-id="6adb8-114">此系列是以 Tom 作者: dykstra 和 Rick Anderson 的貢獻來撰寫。</span><span class="sxs-lookup"><span data-stu-id="6adb8-114">This series was written with contributions from Tom Dykstra and Rick Anderson.</span></span> <span data-ttu-id="6adb8-115">已根據意見區段中的使用者意見反應來改進。</span><span class="sxs-lookup"><span data-stu-id="6adb8-115">It was improved based on feedback from users in the comments section.</span></span>

<span data-ttu-id="6adb8-116">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="6adb8-116">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6adb8-117">設定資料庫</span><span class="sxs-lookup"><span data-stu-id="6adb8-117">Set up the database</span></span>

## <a name="prerequisites"></a><span data-ttu-id="6adb8-118">Prerequisites</span><span class="sxs-lookup"><span data-stu-id="6adb8-118">Prerequisites</span></span>

[<span data-ttu-id="6adb8-119">Visual Studio 2017</span><span class="sxs-lookup"><span data-stu-id="6adb8-119">Visual Studio 2017</span></span>](https://visualstudio.microsoft.com/downloads/)

## <a name="set-up-the-database"></a><span data-ttu-id="6adb8-120">設定資料庫</span><span class="sxs-lookup"><span data-stu-id="6adb8-120">Set up the database</span></span>

<span data-ttu-id="6adb8-121">若要模擬擁有現有資料庫的環境，您必須先使用一些預先填入的資料來建立資料庫，然後建立連接到資料庫的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="6adb8-121">To mimic the environment of having an existing database, you will first create a database with some pre-filled data, and then create your web application that connects to the database.</span></span>

<span data-ttu-id="6adb8-122">本教學課程是使用 LocalDB 與 Visual Studio 2017 開發的。</span><span class="sxs-lookup"><span data-stu-id="6adb8-122">This tutorial was developed using LocalDB with Visual Studio 2017.</span></span> <span data-ttu-id="6adb8-123">您可以使用現有的資料庫伺服器，而不是 LocalDB，但根據您的 Visual Studio 版本和您的資料庫類型而定，可能不支援 Visual Studio 中的所有資料工具。</span><span class="sxs-lookup"><span data-stu-id="6adb8-123">You can use an existing database server instead of LocalDB, but depending on your version of Visual Studio and your type of database, all of the data tools in Visual Studio might not be supported.</span></span> <span data-ttu-id="6adb8-124">如果您的資料庫無法使用這些工具，您可能需要在資料庫的管理元件內執行一些資料庫特定步驟。</span><span class="sxs-lookup"><span data-stu-id="6adb8-124">If the tools are not available for your database, you may need to perform some of the database-specific steps within the management suite for your database.</span></span>

<span data-ttu-id="6adb8-125">如果您的 Visual Studio 版本中的資料庫工具發生問題，請確定您已安裝最新版本的資料庫工具。</span><span class="sxs-lookup"><span data-stu-id="6adb8-125">If you have a problem with the database tools in your version of Visual Studio, make sure you have installed the latest version of the database tools.</span></span> <span data-ttu-id="6adb8-126">如需有關更新或安裝資料庫工具的詳細資訊，請參閱[Microsoft SQL Server Data tools](https://msdn.microsoft.com/data/hh297027)。</span><span class="sxs-lookup"><span data-stu-id="6adb8-126">For information about updating or installing the database tools, see [Microsoft SQL Server Data Tools](https://msdn.microsoft.com/data/hh297027).</span></span>

<span data-ttu-id="6adb8-127">啟動 Visual Studio 並建立**SQL Server 資料庫專案**。</span><span class="sxs-lookup"><span data-stu-id="6adb8-127">Launch Visual Studio and create a **SQL Server Database Project**.</span></span> <span data-ttu-id="6adb8-128">將專案命名為**ContosoUniversityData**。</span><span class="sxs-lookup"><span data-stu-id="6adb8-128">Name the project **ContosoUniversityData**.</span></span>

![建立資料庫專案](setting-up-database/_static/image1.png)

<span data-ttu-id="6adb8-130">您現在有一個空的資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="6adb8-130">You now have an empty database project.</span></span> <span data-ttu-id="6adb8-131">為確保您可以將此資料庫部署至 Azure，您會將 Azure SQL Database 設定為專案的目標平臺。</span><span class="sxs-lookup"><span data-stu-id="6adb8-131">To make sure that you can deploy this database to Azure, you'll set Azure SQL Database as the target platform for the project.</span></span> <span data-ttu-id="6adb8-132">設定目標平臺並不會實際部署資料庫;這只表示資料庫專案會驗證資料庫設計是否與目標平臺相容。</span><span class="sxs-lookup"><span data-stu-id="6adb8-132">Setting the target platform does not actually deploy the database; it only means that the database project will verify that the database design is compatible with the target platform.</span></span> <span data-ttu-id="6adb8-133">若要設定目標平臺，請開啟專案的**屬性**，然後針對目標平臺選取 [ **Microsoft Azure SQL Database** ]。</span><span class="sxs-lookup"><span data-stu-id="6adb8-133">To set the target platform, open the **Properties** for the project and select **Microsoft Azure SQL Database** for the target platform.</span></span>

<span data-ttu-id="6adb8-134">您可以藉由加入定義資料表的 SQL 腳本來建立本教學課程所需的資料表。</span><span class="sxs-lookup"><span data-stu-id="6adb8-134">You can create the tables needed for this tutorial by adding SQL scripts that define the tables.</span></span> <span data-ttu-id="6adb8-135">以滑鼠右鍵按一下您的專案，並加入新的專案。</span><span class="sxs-lookup"><span data-stu-id="6adb8-135">Right-click your project and add a new item.</span></span> <span data-ttu-id="6adb8-136">選取**資料表和 Views** > **資料表**，並將它命名為*Student*。</span><span class="sxs-lookup"><span data-stu-id="6adb8-136">Select **Tables and Views** > **Table** and name it *Student*.</span></span>

<span data-ttu-id="6adb8-137">在資料表檔案中，以下列程式碼取代 T-sql 命令以建立資料表。</span><span class="sxs-lookup"><span data-stu-id="6adb8-137">In the table file, replace the T-SQL command with the following code to create the table.</span></span>

[!code-sql[Main](setting-up-database/samples/sample1.sql)]

<span data-ttu-id="6adb8-138">請注意，[設計] 視窗會自動與程式碼同步處理。</span><span class="sxs-lookup"><span data-stu-id="6adb8-138">Notice that the design window automatically synchronizes with the code.</span></span> <span data-ttu-id="6adb8-139">您可以使用程式碼或設計工具。</span><span class="sxs-lookup"><span data-stu-id="6adb8-139">You can work with either the code or designer.</span></span>

![顯示程式碼和設計](setting-up-database/_static/image5.png)

<span data-ttu-id="6adb8-141">新增另一個資料表。</span><span class="sxs-lookup"><span data-stu-id="6adb8-141">Add another table.</span></span> <span data-ttu-id="6adb8-142">這次請將它命名為「課程」，並使用下列 T-sql 命令。</span><span class="sxs-lookup"><span data-stu-id="6adb8-142">This time name it Course and use the following T-SQL command.</span></span>

[!code-sql[Main](setting-up-database/samples/sample2.sql)]

<span data-ttu-id="6adb8-143">再重複一次，以建立名為註冊的資料表。</span><span class="sxs-lookup"><span data-stu-id="6adb8-143">And, repeat one more time to create a table named Enrollment.</span></span>

[!code-sql[Main](setting-up-database/samples/sample3.sql)]

<span data-ttu-id="6adb8-144">您可以透過在部署資料庫之後執行的腳本，將資料填入資料庫。</span><span class="sxs-lookup"><span data-stu-id="6adb8-144">You can populate your database with data through a script that is run after the database is deployed.</span></span> <span data-ttu-id="6adb8-145">將部署後腳本新增至專案。</span><span class="sxs-lookup"><span data-stu-id="6adb8-145">Add a Post-Deployment Script to the project.</span></span> <span data-ttu-id="6adb8-146">以滑鼠右鍵按一下您的專案，並加入新的專案。</span><span class="sxs-lookup"><span data-stu-id="6adb8-146">Right-click your project and add a new item.</span></span> <span data-ttu-id="6adb8-147">選取 [**使用者腳本**] > **部署後腳本**。</span><span class="sxs-lookup"><span data-stu-id="6adb8-147">Select **User Scripts** > **Post-Deployment Script**.</span></span> <span data-ttu-id="6adb8-148">您可以使用預設名稱。</span><span class="sxs-lookup"><span data-stu-id="6adb8-148">You can use the default name.</span></span>

<span data-ttu-id="6adb8-149">將下列 T-sql 程式碼新增至部署後腳本。</span><span class="sxs-lookup"><span data-stu-id="6adb8-149">Add the following T-SQL code to the post-deployment script.</span></span> <span data-ttu-id="6adb8-150">當找不到相符的記錄時，此腳本只會將資料新增至資料庫。</span><span class="sxs-lookup"><span data-stu-id="6adb8-150">This script simply adds data to the database when no matching record is found.</span></span> <span data-ttu-id="6adb8-151">它不會覆寫或刪除您可能已在資料庫中輸入的任何資料。</span><span class="sxs-lookup"><span data-stu-id="6adb8-151">It does not overwrite or delete any data you may have entered into the database.</span></span>

[!code-sql[Main](setting-up-database/samples/sample4.sql)]

<span data-ttu-id="6adb8-152">請務必注意，部署後腳本會在您每次部署資料庫專案時執行。</span><span class="sxs-lookup"><span data-stu-id="6adb8-152">It is important to note that the post-deployment script is run every time you deploy your database project.</span></span> <span data-ttu-id="6adb8-153">因此，撰寫此腳本時，您必須仔細考慮您的需求。</span><span class="sxs-lookup"><span data-stu-id="6adb8-153">Therefore, you need to carefully consider your requirements when writing this script.</span></span> <span data-ttu-id="6adb8-154">在某些情況下，您可能會想要在每次部署專案時，從一組已知的資料開始。</span><span class="sxs-lookup"><span data-stu-id="6adb8-154">In some cases, you may wish to start over from a known set of data every time the project is deployed.</span></span> <span data-ttu-id="6adb8-155">在其他情況下，您可能不想要以任何方式改變現有的資料。</span><span class="sxs-lookup"><span data-stu-id="6adb8-155">In other cases, you may not want to alter the existing data in any way.</span></span> <span data-ttu-id="6adb8-156">根據您的需求，您可以決定是否需要部署後腳本，或是您需要在腳本中包含的內容。</span><span class="sxs-lookup"><span data-stu-id="6adb8-156">Based on your requirements, you can decide whether you need a post-deployment script or what you need to include in the script.</span></span> <span data-ttu-id="6adb8-157">如需使用部署後腳本填入資料庫的詳細資訊，請參閱[在 SQL Server 資料庫專案中包含資料](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx)。</span><span class="sxs-lookup"><span data-stu-id="6adb8-157">For more information about populating your database with a post-deployment script, see [Including Data in a SQL Server Database Project](https://blogs.msdn.com/b/ssdt/archive/2012/02/02/including-data-in-an-sql-server-database-project.aspx).</span></span>

<span data-ttu-id="6adb8-158">現在您有4個 SQL 腳本檔案，但沒有實際的資料表。</span><span class="sxs-lookup"><span data-stu-id="6adb8-158">You now have 4 SQL script files but no actual tables.</span></span> <span data-ttu-id="6adb8-159">您已準備好將資料庫專案部署至 localdb。</span><span class="sxs-lookup"><span data-stu-id="6adb8-159">You are ready to deploy your database project to localdb.</span></span> <span data-ttu-id="6adb8-160">在 Visual Studio 中，按一下 [開始] 按鈕（或 F5）來建立及部署您的資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="6adb8-160">In Visual Studio, click the Start button (or F5) to build and deploy your database project.</span></span> <span data-ttu-id="6adb8-161">檢查 [**輸出**] 索引標籤，確認組建和部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="6adb8-161">Check the **Output** tab to verify that the build and deployment succeeded.</span></span>

<span data-ttu-id="6adb8-162">若要查看是否已建立新的資料庫，請開啟**SQL Server 物件總管**，並在正確的本機資料庫伺服器中尋找專案的名稱（在此案例中為 **（localdb） \ProjectsV13**）。</span><span class="sxs-lookup"><span data-stu-id="6adb8-162">To see that the new database has been created, open **SQL Server Object Explorer** and look for the name of the project in the correct local database server (in this case **(localdb)\ProjectsV13**).</span></span>

<span data-ttu-id="6adb8-163">若要查看資料表是否已填入資料，請以滑鼠右鍵按一下資料表，然後選取 [**查看資料**]。</span><span class="sxs-lookup"><span data-stu-id="6adb8-163">To see that the tables are populated with data, right-click a table, and select **View Data**.</span></span>

![顯示資料表資料](setting-up-database/_static/image9.png)

<span data-ttu-id="6adb8-165">資料表資料的可編輯檢視隨即顯示。</span><span class="sxs-lookup"><span data-stu-id="6adb8-165">An editable view of the table data is displayed.</span></span> <span data-ttu-id="6adb8-166">例如，如果您選取 **資料表** > **dbo. 課程** > **視圖資料**，您會看到包含三個數據行的資料表（**課程**、**標題**和**點數**）和四個數據列。</span><span class="sxs-lookup"><span data-stu-id="6adb8-166">For example, if you select **Tables** > **dbo.course** > **View Data**, you see a table with three columns (**Course**, **Title**, and **Credits**) and four rows.</span></span>

## <a name="additional-resources"></a><span data-ttu-id="6adb8-167">其他資源</span><span class="sxs-lookup"><span data-stu-id="6adb8-167">Additional resources</span></span>

<span data-ttu-id="6adb8-168">如需 Code First 開發的簡介範例，請參閱[使用 ASP.NET MVC 5 消費者入門](../introduction/getting-started.md)。</span><span class="sxs-lookup"><span data-stu-id="6adb8-168">For an introductory example of Code First development, see [Getting Started with ASP.NET MVC 5](../introduction/getting-started.md).</span></span> <span data-ttu-id="6adb8-169">如需更先進的範例，請參閱[建立 ASP.NET MVC 4 應用程式的 Entity Framework 資料模型](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)。</span><span class="sxs-lookup"><span data-stu-id="6adb8-169">For a more advanced example, see [Creating an Entity Framework Data Model for an ASP.NET MVC 4 App](../getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md).</span></span>

<span data-ttu-id="6adb8-170">如需有關選取要使用哪一個 Entity Framework 方法的指引，請參閱[Entity Framework 開發方法](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。</span><span class="sxs-lookup"><span data-stu-id="6adb8-170">For guidance on selecting which Entity Framework approach to use, see [Entity Framework Development Approaches](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf).</span></span>

## <a name="next-steps"></a><span data-ttu-id="6adb8-171">後續步驟</span><span class="sxs-lookup"><span data-stu-id="6adb8-171">Next steps</span></span>

<span data-ttu-id="6adb8-172">在本教學課程中，您已：</span><span class="sxs-lookup"><span data-stu-id="6adb8-172">In this tutorial, you:</span></span>

> [!div class="checklist"]
> * <span data-ttu-id="6adb8-173">設定資料庫</span><span class="sxs-lookup"><span data-stu-id="6adb8-173">Set up the database</span></span>

<span data-ttu-id="6adb8-174">請前進到下一個教學課程，以瞭解如何建立 web 應用程式和資料模型。</span><span class="sxs-lookup"><span data-stu-id="6adb8-174">Advance to the next tutorial to learn how to create the web application and data models.</span></span>
> [!div class="nextstepaction"]
> [<span data-ttu-id="6adb8-175">建立 web 應用程式和資料模型</span><span class="sxs-lookup"><span data-stu-id="6adb8-175">Create the web application and data models</span></span>](creating-the-web-application.md)
