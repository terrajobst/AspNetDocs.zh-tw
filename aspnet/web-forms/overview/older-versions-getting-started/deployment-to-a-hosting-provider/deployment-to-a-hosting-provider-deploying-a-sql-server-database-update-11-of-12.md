---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署 SQL Server 資料庫更新-11/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 5e2bb092-cb22-4511-ad0a-22ae12dd99b3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12
msc.type: authoredcontent
ms.openlocfilehash: 0894c0ac24737e66b6960ef3d48aa17f78c6aa1d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74621059"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-sql-server-database-update---11-of-12"></a><span data-ttu-id="3be26-103">使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式：部署 SQL Server 資料庫更新-11/12</span><span class="sxs-lookup"><span data-stu-id="3be26-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a SQL Server Database Update - 11 of 12</span></span>

<span data-ttu-id="3be26-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="3be26-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="3be26-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="3be26-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="3be26-106">這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="3be26-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="3be26-107">如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="3be26-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="3be26-108">如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。</span><span class="sxs-lookup"><span data-stu-id="3be26-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="3be26-109">如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署至 Windows Azure 網站，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="3be26-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Windows Azure Web Sites, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="3be26-110">概觀</span><span class="sxs-lookup"><span data-stu-id="3be26-110">Overview</span></span>

<span data-ttu-id="3be26-111">本教學課程說明如何將資料庫更新部署至完整的 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3be26-111">This tutorial shows you how to deploy a database update to a full SQL Server database.</span></span> <span data-ttu-id="3be26-112">由於 Code First 移轉會執行更新資料庫的所有工作，因此程式與您在[部署資料庫更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教學課程中所做的 SQL Server Compact 程式幾乎完全相同。</span><span class="sxs-lookup"><span data-stu-id="3be26-112">Because Code First Migrations does all the work of updating the database, the process is almost identical to what you did for SQL Server Compact in the [Deploying a Database Update](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md) tutorial.</span></span>

<span data-ttu-id="3be26-113">提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="3be26-113">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="3be26-114">將新的資料行加入至資料表</span><span class="sxs-lookup"><span data-stu-id="3be26-114">Adding a New Column to a Table</span></span>

<span data-ttu-id="3be26-115">在本教學課程的這一節中，您將會進行資料庫變更和對應的程式碼變更，然後在 Visual Studio 中進行測試，以準備將它們部署至測試和生產環境。</span><span class="sxs-lookup"><span data-stu-id="3be26-115">In this section of the tutorial you'll make a database change and corresponding code changes, then test them in Visual Studio in preparation for deploying them to the test and production environments.</span></span> <span data-ttu-id="3be26-116">變更牽涉到將 `OfficeHours` 資料行加入 `Instructor` 實體，並在**講師**網頁中顯示新資訊。</span><span class="sxs-lookup"><span data-stu-id="3be26-116">The change involves adding an `OfficeHours` column to the `Instructor` entity and displaying the new information in the **Instructors** web page.</span></span>

<span data-ttu-id="3be26-117">在 ContosoUniversity 專案中，開啟*Instructor.cs* ，並在 `HireDate` 和 `Courses` 屬性之間新增下列屬性：</span><span class="sxs-lookup"><span data-stu-id="3be26-117">In the ContosoUniversity.DAL project, open *Instructor.cs* and add the following property between the `HireDate` and `Courses` properties:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample1.cs)]

<span data-ttu-id="3be26-118">更新初始化運算式類別，使其植入具有測試資料的新資料行。</span><span class="sxs-lookup"><span data-stu-id="3be26-118">Update the initializer class so that it seeds the new column with test data.</span></span> <span data-ttu-id="3be26-119">開啟*Migrations\Configuration.cs* ，並將開始 `var instructors = new List<Instructor>` 的程式碼區塊取代為下列包含新資料行的程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="3be26-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes the new column:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample2.cs)]

<span data-ttu-id="3be26-120">在 ContosoUniversity 專案中，開啟 [ *default.aspx* ]，然後在第一個 `GridView` 控制項的 [結束 `</Columns>`] 標籤之前，加入 office 小時的新範本欄位：</span><span class="sxs-lookup"><span data-stu-id="3be26-120">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field for office hours just before the closing `</Columns>` tag in the first `GridView` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample3.aspx)]

<span data-ttu-id="3be26-121">建置方案。</span><span class="sxs-lookup"><span data-stu-id="3be26-121">Build the solution.</span></span>

<span data-ttu-id="3be26-122">開啟 [**套件管理員主控台**] 視窗，然後選取 [ContosoUniversity] 做為**預設專案**。</span><span class="sxs-lookup"><span data-stu-id="3be26-122">Open the **Package Manager Console** window, and select ContosoUniversity.DAL as the **Default project**.</span></span>

<span data-ttu-id="3be26-123">輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="3be26-123">Enter the following commands:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample4.ps1)]

<span data-ttu-id="3be26-124">執行應用程式，然後選取 [**講師**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3be26-124">Run the application and select the **Instructors** page.</span></span> <span data-ttu-id="3be26-125">網頁需要比平常更長的時間才能載入，因為 Entity Framework 會重新建立資料庫，並植入測試資料。</span><span class="sxs-lookup"><span data-stu-id="3be26-125">The page takes a little longer than usual to load, because the Entity Framework re-creates the database and seeds it with test data.</span></span>

<span data-ttu-id="3be26-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="3be26-126">[![Instructors_page_with_office_hours](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image1.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="3be26-127">將資料庫更新部署到測試環境</span><span class="sxs-lookup"><span data-stu-id="3be26-127">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="3be26-128">當您使用 Code First 移轉時，用於將資料庫變更部署至 SQL Server 的方法，與 SQL Server Compact 的方式相同。</span><span class="sxs-lookup"><span data-stu-id="3be26-128">When you use Code First Migrations, the method for deploying a database change to SQL Server is the same as for SQL Server Compact.</span></span> <span data-ttu-id="3be26-129">不過，您必須變更測試發行設定檔，因為它仍然設定為從 SQL Server Compact 遷移至 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="3be26-129">However, you have to change the Test publish profile because it is still set up to migrate from SQL Server Compact to SQL Server.</span></span>

<span data-ttu-id="3be26-130">第一個步驟是移除您在上一個教學課程中建立的連接字串轉換。</span><span class="sxs-lookup"><span data-stu-id="3be26-130">The first step is to remove the connection string transformations that you created in the previous tutorial.</span></span> <span data-ttu-id="3be26-131">因為您會在發行設定檔中指定連接字串轉換，就像您在設定 [**封裝/發行 SQL** ] 索引標籤以進行遷移到 SQL Server 之前所做的一樣，因此不再需要這些設定。</span><span class="sxs-lookup"><span data-stu-id="3be26-131">These are no longer needed because you'll specify connection string transformations in the publish profile, as you did before you configured the **Package/Publish SQL** tab for migration to SQL Server.</span></span>

<span data-ttu-id="3be26-132">開啟*web.config*檔案，並移除 `connectionStrings` 元素。</span><span class="sxs-lookup"><span data-stu-id="3be26-132">Open the *Web.Test.config* file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="3be26-133">*Web.config*檔案中唯一剩餘的轉換，是 `appSettings` 元素中的 `Environment` 值。</span><span class="sxs-lookup"><span data-stu-id="3be26-133">The only remaining transformation in the *Web.Test.config* file is for the `Environment` value in the `appSettings` element.</span></span>

<span data-ttu-id="3be26-134">現在您可以更新發行設定檔，併發布至測試環境。</span><span class="sxs-lookup"><span data-stu-id="3be26-134">Now you can update the publish profile and publish to the test environment.</span></span>

<span data-ttu-id="3be26-135">開啟 [**發行 Web** wizard]，然後切換至 [**設定檔**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3be26-135">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="3be26-136">選取 [**測試**發行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="3be26-136">Select the **Test** publish profile.</span></span>

<span data-ttu-id="3be26-137">選取 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3be26-137">Select the **Settings** tab.</span></span>

<span data-ttu-id="3be26-138">按一下 **[啟用新的資料庫發行增強功能**]。</span><span class="sxs-lookup"><span data-stu-id="3be26-138">Click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="3be26-139">在 [ **SchoolCoNtext**] 的 [連接字串] 方塊中，輸入您在上一個教學課程的*web.config 轉換檔案*中使用的相同值：</span><span class="sxs-lookup"><span data-stu-id="3be26-139">In the connection string box for **SchoolContext**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample5.cmd)]

<span data-ttu-id="3be26-140">選取**執行 Code First 移轉（在應用程式啟動時執行）** 。</span><span class="sxs-lookup"><span data-stu-id="3be26-140">Select **Execute Code First Migrations (runs on application start)**.</span></span> <span data-ttu-id="3be26-141">（在您的 Visual Studio 版本中，此核取方塊可能標示為 [套用**Code First 移轉**]）。</span><span class="sxs-lookup"><span data-stu-id="3be26-141">(In your version of Visual Studio, the check box might be labeled **Apply Code First Migrations**.)</span></span>

<span data-ttu-id="3be26-142">在 [ **DefaultConnection**] 的 [連接字串] 方塊中，輸入您在上一個教學課程的*web.config 轉換檔案*中使用的相同值：</span><span class="sxs-lookup"><span data-stu-id="3be26-142">In the connection string box for **DefaultConnection**, enter the same value that you used in the *Web.Test.config* transformation file in the previous tutorial:</span></span>

[!code-console[Main](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/samples/sample6.cmd)]

<span data-ttu-id="3be26-143">將**更新資料庫**保留為已清除。</span><span class="sxs-lookup"><span data-stu-id="3be26-143">Leave **Update database** cleared.</span></span>

<span data-ttu-id="3be26-144">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="3be26-144">Click **Publish**.</span></span>

<span data-ttu-id="3be26-145">Visual Studio 會將程式碼變更部署至測試環境，並將瀏覽器開啟至 Contoso 大學首頁。</span><span class="sxs-lookup"><span data-stu-id="3be26-145">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="3be26-146">選取 [講師] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3be26-146">Select the Instructors page.</span></span>

<span data-ttu-id="3be26-147">當應用程式執行此頁面時，它會嘗試存取資料庫。</span><span class="sxs-lookup"><span data-stu-id="3be26-147">When the application runs this page, it tries to access the database.</span></span> <span data-ttu-id="3be26-148">Code First 移轉檢查資料庫是否為最新的，並找出最近尚未套用的遷移。</span><span class="sxs-lookup"><span data-stu-id="3be26-148">Code First Migrations checks if the database is current, and finds that the latest migration has not been applied yet.</span></span> <span data-ttu-id="3be26-149">Code First 移轉會套用最新的遷移、執行 `Seed` 方法，然後網頁會正常執行。</span><span class="sxs-lookup"><span data-stu-id="3be26-149">Code First Migrations applies the latest migration, runs the `Seed` method, and then the page runs normally.</span></span> <span data-ttu-id="3be26-150">您會看到新的 [Office 小時] 資料行與植入的資料。</span><span class="sxs-lookup"><span data-stu-id="3be26-150">You see the new Office Hours column with the seeded data.</span></span>

<span data-ttu-id="3be26-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="3be26-151">[![Instructors_page_with_OfficeHours_Test](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="3be26-152">將資料庫更新部署至生產環境</span><span class="sxs-lookup"><span data-stu-id="3be26-152">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="3be26-153">您也必須變更生產環境的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="3be26-153">You have to change the publish profile for the production environment also.</span></span> <span data-ttu-id="3be26-154">在此情況下，您將移除現有的設定檔，並藉由匯入更新的 .publishsettings 檔案來建立一個新的。</span><span class="sxs-lookup"><span data-stu-id="3be26-154">In this case you'll remove the existing profile and create a new one by importing an updated .publishsettings file.</span></span> <span data-ttu-id="3be26-155">更新的檔案將包含 Cytanium 之 SQL Server 資料庫的連接字串。</span><span class="sxs-lookup"><span data-stu-id="3be26-155">The updated file will include the connection string for the SQL Server database at Cytanium.</span></span>

<span data-ttu-id="3be26-156">如您在部署到測試環境時所看到的，您不再需要在*web.config*轉換檔案中進行連接字串轉換。</span><span class="sxs-lookup"><span data-stu-id="3be26-156">As you saw when you deployed to the test environment, you no longer need connection string transforms in the *Web.Production.config* transformation file.</span></span> <span data-ttu-id="3be26-157">開啟該檔案，並移除 `connectionStrings` 元素。</span><span class="sxs-lookup"><span data-stu-id="3be26-157">Open that file and remove the `connectionStrings` element.</span></span> <span data-ttu-id="3be26-158">其餘的轉換適用于 `appSettings` 元素中的 `Environment` 值，以及限制對 Elmah 錯誤報表存取的 `location` 元素。</span><span class="sxs-lookup"><span data-stu-id="3be26-158">The remaining transformations are for the `Environment` value in the `appSettings` element and the `location` element that restricts access to Elmah error reports.</span></span>

<span data-ttu-id="3be26-159">在您為生產環境建立新的發行設定檔之前，請下載更新過的 .publishsettings 檔案，方法與您稍早在[部署至生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中所做的相同。</span><span class="sxs-lookup"><span data-stu-id="3be26-159">Before you create a new publish profile for production, download an updated .publishsettings file the same way you did earlier in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="3be26-160">（在 [Cytanium] 控制台中，按一下 [**網站**]，然後按一下 [ **contosouniversity.com** ] 網站。</span><span class="sxs-lookup"><span data-stu-id="3be26-160">(In the Cytanium control panel, click **Web Sites**, and then click the **contosouniversity.com** website.</span></span> <span data-ttu-id="3be26-161">選取 [ **Web 發行**] 索引標籤，然後按一下 [**下載此網站的發行設定檔**]）。這麼做的原因是要在 .publishsettings 檔案中挑選資料庫連接字串。</span><span class="sxs-lookup"><span data-stu-id="3be26-161">Select the **Web Publishing** tab, and then click **Download Publishing Profile for this web site**.) The reason you are doing this is to pick up the database connection string in the .publishsettings file.</span></span> <span data-ttu-id="3be26-162">第一次下載檔案時無法使用連接字串，因為您仍在使用 SQL Server Compact，而且尚未在 Cytanium 建立 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3be26-162">The connection string wasn't available the first time you downloaded the file, because you were still using SQL Server Compact and hadn't created the SQL Server database at Cytanium yet.</span></span>

<span data-ttu-id="3be26-163">現在您可以更新發行設定檔，併發布到生產環境。</span><span class="sxs-lookup"><span data-stu-id="3be26-163">Now you can update the publish profile and publish to the production environment.</span></span>

<span data-ttu-id="3be26-164">開啟 [**發行 Web** wizard]，然後切換至 [**設定檔**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="3be26-164">Open the **Publish Web** wizard, and then switch to the **Profile** tab.</span></span>

<span data-ttu-id="3be26-165">按一下 [**管理設定檔**]，然後刪除生產設定檔。</span><span class="sxs-lookup"><span data-stu-id="3be26-165">Click **Manage Profiles**, and then delete the Production profile.</span></span>

<span data-ttu-id="3be26-166">關閉 [**發行 Web** wizard] 以儲存此變更。</span><span class="sxs-lookup"><span data-stu-id="3be26-166">Close the **Publish Web** wizard to save this change.</span></span>

<span data-ttu-id="3be26-167">再次開啟 [**發佈 Web**嚮導]，然後按一下 [匯**入**]。</span><span class="sxs-lookup"><span data-stu-id="3be26-167">Open the **Publish Web** wizard again, and then click **Import**.</span></span>

<span data-ttu-id="3be26-168">如果您使用的是暫存 URL，請在 [**連接**] 索引標籤上，將 [**目的地 URL** ] 變更為適當的值。</span><span class="sxs-lookup"><span data-stu-id="3be26-168">On the **Connection** tab, change **Destination URL** to the appropriate value if you are using a temporary URL.</span></span>

<span data-ttu-id="3be26-169">按 [ **下一步**]。</span><span class="sxs-lookup"><span data-stu-id="3be26-169">Click **Next**.</span></span>

<span data-ttu-id="3be26-170">在 [**設定**] 索引標籤上，按一下 [**啟用新的資料庫發行增強功能**]。</span><span class="sxs-lookup"><span data-stu-id="3be26-170">On the **Settings** tab, click **enable the new database publishing improvements**.</span></span>

<span data-ttu-id="3be26-171">在 [ **SchoolCoNtext**] 的 [連接字串] 下拉式清單中，選取 [Cytanium] 連接字串。</span><span class="sxs-lookup"><span data-stu-id="3be26-171">In the connection string drop-down list for **SchoolContext**, select the Cytanium connection string.</span></span>

![Selecting_Cytanium_connection_string](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image5.png)

<span data-ttu-id="3be26-173">選取 **[執行 Code First 遷移（在應用程式啟動時執行）** ]。</span><span class="sxs-lookup"><span data-stu-id="3be26-173">Select **Execute Code First migrations (runs on application start)**.</span></span>

<span data-ttu-id="3be26-174">在 [ **DefaultConnection**] 的 [連接字串] 下拉式清單中，選取 [Cytanium] 連接字串。</span><span class="sxs-lookup"><span data-stu-id="3be26-174">In the connection string drop-down list for **DefaultConnection**, select the Cytanium connection string.</span></span>

<span data-ttu-id="3be26-175">選取 [**設定檔**] 索引標籤，按一下 [**管理設定檔**]，然後將設定檔從 "Web Deploy contosouniversity.com" 重新命名為「生產」。</span><span class="sxs-lookup"><span data-stu-id="3be26-175">Select the **Profile** tab, click **Manage Profiles**, and rename the profile from "contosouniversity.com - Web Deploy" to "Production".</span></span>

<span data-ttu-id="3be26-176">關閉發行設定檔以儲存變更，然後重新開啟。</span><span class="sxs-lookup"><span data-stu-id="3be26-176">Close the publish profile to save the change, then open it again.</span></span>

<span data-ttu-id="3be26-177">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="3be26-177">Click **Publish**.</span></span> <span data-ttu-id="3be26-178">（針對實際生產網站，您會將*應用程式\_離線 .htm*複製到生產環境，並在發行之前將它放在您的專案資料夾中，然後在部署完成時將它移除）。</span><span class="sxs-lookup"><span data-stu-id="3be26-178">(For a real production website, you would copy *app\_offline.htm* to production and put it in your project folder before publishing, then remove it when deployment is complete.)</span></span>

<span data-ttu-id="3be26-179">Visual Studio 會將程式碼變更部署至測試環境，並將瀏覽器開啟至 Contoso 大學首頁。</span><span class="sxs-lookup"><span data-stu-id="3be26-179">Visual Studio deploys the code changes to the test environment and opens the browser to the Contoso University home page.</span></span>

<span data-ttu-id="3be26-180">選取 [講師] 頁面。</span><span class="sxs-lookup"><span data-stu-id="3be26-180">Select the Instructors page.</span></span>

<span data-ttu-id="3be26-181">Code First 移轉以在測試環境中的相同方式更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="3be26-181">Code First Migrations updates the database the same way it did in the Test environment.</span></span> <span data-ttu-id="3be26-182">您會看到新的 [Office 小時] 資料行與植入的資料。</span><span class="sxs-lookup"><span data-stu-id="3be26-182">You see the new Office Hours column with the seeded data.</span></span>

![Instructors_page_with_OfficeHours_Prod](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12/_static/image6.png)

<span data-ttu-id="3be26-184">您現在已成功部署包含資料庫變更的應用程式更新，並使用 SQL Server 資料庫。</span><span class="sxs-lookup"><span data-stu-id="3be26-184">You have now successfully deployed an application update that included a database change, using a SQL Server database.</span></span>

## <a name="more-information"></a><span data-ttu-id="3be26-185">更多資訊</span><span class="sxs-lookup"><span data-stu-id="3be26-185">More Information</span></span>

<span data-ttu-id="3be26-186">這會完成這一系列的教學課程，將 ASP.NET web 應用程式部署到協力廠商裝載提供者。</span><span class="sxs-lookup"><span data-stu-id="3be26-186">This completes this series of tutorials on deploying an ASP.NET web application to a third-party hosting provider.</span></span> <span data-ttu-id="3be26-187">如需這些教學課程中所涵蓋之任何主題的詳細資訊，請參閱 MSDN 網站上的[ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="3be26-187">For more information about any of the topics covered in these tutorials, see the [ASP.NET Deployment Content Map](https://msdn.microsoft.com/library/bb386521(v=vs.110).aspx) on the MSDN web site.</span></span>

## <a name="acknowledgements"></a><span data-ttu-id="3be26-188">致謝</span><span class="sxs-lookup"><span data-stu-id="3be26-188">Acknowledgements</span></span>

<span data-ttu-id="3be26-189">我想感謝下列人對本教學課程系列的內容做出重大貢獻：</span><span class="sxs-lookup"><span data-stu-id="3be26-189">I would like to thank the following people who made significant contributions to the content of this tutorial series:</span></span>

- [<span data-ttu-id="3be26-190">Alberto Poblacion，MVP &amp; MCT，西班牙</span><span class="sxs-lookup"><span data-stu-id="3be26-190">Alberto Poblacion, MVP &amp; MCT, Spain</span></span>](https://mvp.support.microsoft.com/profile/Alberto)
- <span data-ttu-id="3be26-191">Jarod Ferguson，資料平臺開發 MVP，美國</span><span class="sxs-lookup"><span data-stu-id="3be26-191">Jarod Ferguson, Data Platform Development MVP, United States</span></span>
- <span data-ttu-id="3be26-192">Microsoft 的 Mittal</span><span class="sxs-lookup"><span data-stu-id="3be26-192">Harsh Mittal, Microsoft</span></span>
- [<span data-ttu-id="3be26-193">Kristina Olson，Microsoft</span><span class="sxs-lookup"><span data-stu-id="3be26-193">Kristina Olson, Microsoft</span></span>](https://blogs.iis.net/krolson/default.aspx)
- [<span data-ttu-id="3be26-194">Mike Pope，Microsoft</span><span class="sxs-lookup"><span data-stu-id="3be26-194">Mike Pope, Microsoft</span></span>](http://www.mikepope.com/blog/DisplayBlog.aspx)
- <span data-ttu-id="3be26-195">Mohit Srivastava，Microsoft</span><span class="sxs-lookup"><span data-stu-id="3be26-195">Mohit Srivastava, Microsoft</span></span>
- [<span data-ttu-id="3be26-196">Raffaele Rialdi，義大利</span><span class="sxs-lookup"><span data-stu-id="3be26-196">Raffaele Rialdi, Italy</span></span>](http://www.iamraf.net/)
- [<span data-ttu-id="3be26-197">Rick Anderson，Microsoft</span><span class="sxs-lookup"><span data-stu-id="3be26-197">Rick Anderson, Microsoft</span></span>](https://blogs.msdn.com/b/rickandy/)
- <span data-ttu-id="3be26-198">[Sayed Hashimi，Microsoft](http://sedodream.com/default.aspx)（twitter： [@sayedihashimi](http://twitter.com/sayedihashimi)）</span><span class="sxs-lookup"><span data-stu-id="3be26-198">[Sayed Hashimi, Microsoft](http://sedodream.com/default.aspx)(twitter: [@sayedihashimi](http://twitter.com/sayedihashimi))</span></span>
- <span data-ttu-id="3be26-199">[Scott Hanselman](http://www.hanselman.com/blog/) （twitter： [@shanselman](http://twitter.com/shanselman)）</span><span class="sxs-lookup"><span data-stu-id="3be26-199">[Scott Hanselman](http://www.hanselman.com/blog/) (twitter: [@shanselman](http://twitter.com/shanselman))</span></span>
- <span data-ttu-id="3be26-200">[Scott Hunter，Microsoft](https://blogs.msdn.com/b/scothu/) （twitter： [@coolcsh](http://twitter.com/coolcsh)）</span><span class="sxs-lookup"><span data-stu-id="3be26-200">[Scott Hunter, Microsoft](https://blogs.msdn.com/b/scothu/) (twitter: [@coolcsh](http://twitter.com/coolcsh))</span></span>
- [<span data-ttu-id="3be26-201">Srđan Božović，塞爾維亞</span><span class="sxs-lookup"><span data-stu-id="3be26-201">Srđan Božović, Serbia</span></span>](http://msforge.net/blogs/zmajcek/)
- <span data-ttu-id="3be26-202">[Vishal Joshi，Microsoft](http://vishaljoshi.blogspot.com/) （twitter： [@vishalrjoshi](http://twitter.com/vishalrjoshi)）</span><span class="sxs-lookup"><span data-stu-id="3be26-202">[Vishal Joshi, Microsoft](http://vishaljoshi.blogspot.com/) (twitter: [@vishalrjoshi](http://twitter.com/vishalrjoshi))</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="3be26-203">[上一頁](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="3be26-203">[Previous](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)
[Next](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)</span></span>
