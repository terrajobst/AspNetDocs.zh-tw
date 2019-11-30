---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署資料庫更新-9/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a8d776af-4735-4612-87f6-9f326587f2d3
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12
msc.type: authoredcontent
ms.openlocfilehash: 3385e1019d9e7a9263fd9513c39b25eb85febbb5
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74581990"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-database-update---9-of-12"></a><span data-ttu-id="4c15f-103">使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署資料庫更新-9/12</span><span class="sxs-lookup"><span data-stu-id="4c15f-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Database Update - 9 of 12</span></span>

<span data-ttu-id="4c15f-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="4c15f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="4c15f-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="4c15f-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="4c15f-106">這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="4c15f-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="4c15f-107">如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="4c15f-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="4c15f-108">如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。</span><span class="sxs-lookup"><span data-stu-id="4c15f-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="4c15f-109">如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="4c15f-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="4c15f-110">概觀</span><span class="sxs-lookup"><span data-stu-id="4c15f-110">Overview</span></span>

<span data-ttu-id="4c15f-111">在本教學課程中，您會進行資料庫變更和相關的程式碼變更、在 Visual Studio 中測試變更，然後將更新部署到測試和生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c15f-111">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to both the test and production environments.</span></span>

<span data-ttu-id="4c15f-112">提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="4c15f-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="adding-a-new-column-to-a-table"></a><span data-ttu-id="4c15f-113">將新的資料行加入至資料表</span><span class="sxs-lookup"><span data-stu-id="4c15f-113">Adding a New Column to a Table</span></span>

<span data-ttu-id="4c15f-114">在本節中，您會將「出生日期」資料行加入 `Student` 和 `Instructor` 實體的 `Person` 基類。</span><span class="sxs-lookup"><span data-stu-id="4c15f-114">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="4c15f-115">接著，您會更新顯示講師資料的頁面，使其顯示新的資料行。</span><span class="sxs-lookup"><span data-stu-id="4c15f-115">Then you update the page that displays instructor data so that it displays the new column.</span></span>

<span data-ttu-id="4c15f-116">在*ContosoUniversity*專案中，開啟*Person.cs* ，並在 `Person` 類別的結尾處新增下列屬性（後面應該有兩個右大括弧）：</span><span class="sxs-lookup"><span data-stu-id="4c15f-116">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample1.cs)]

<span data-ttu-id="4c15f-117">接下來，請更新種子方法，讓它提供新資料行的值。</span><span class="sxs-lookup"><span data-stu-id="4c15f-117">Next, update the Seed method so that it provides a value for the new column.</span></span> <span data-ttu-id="4c15f-118">開啟*Migrations\Configuration.cs* ，並將開始 `var instructors = new List<Instructor>` 的程式碼區塊取代為下列包含出生日期資訊的程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="4c15f-118">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample2.cs)]

<span data-ttu-id="4c15f-119">在 ContosoUniversity 專案中，開啟 [ *default.aspx* ]，然後新增 [範本] 欄位以顯示出生日期。</span><span class="sxs-lookup"><span data-stu-id="4c15f-119">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="4c15f-120">將其新增至 [雇用日期] 和 [辦公室指派]：</span><span class="sxs-lookup"><span data-stu-id="4c15f-120">Add it between the ones for hire date and office assignment:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample3.aspx)]

<span data-ttu-id="4c15f-121">（如果程式碼縮排無法同步處理，您可以按下 CTRL-K，然後按 CTRL-D 自動重新格式化檔案）。</span><span class="sxs-lookup"><span data-stu-id="4c15f-121">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>

<span data-ttu-id="4c15f-122">建立解決方案，然後開啟 [**套件管理員主控台**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="4c15f-122">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="4c15f-123">請確定 [ContosoUniversity] 仍然選取為 [**預設專案**]。</span><span class="sxs-lookup"><span data-stu-id="4c15f-123">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>

<span data-ttu-id="4c15f-124">在 [**套件管理員主控台**] 視窗中，選取 [ **ContosoUniversity** ] 做為**預設專案**，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="4c15f-124">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample4.ps1)]

<span data-ttu-id="4c15f-125">當此命令完成時，Visual Studio 會開啟定義新 `DbMigration` 類別的類別檔案，而在 `Up` 方法中，您可以看到建立新資料行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="4c15f-125">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span>

![AddBirthDate_migration_code](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image1.png)

<span data-ttu-id="4c15f-127">建立解決方案，然後在 [**套件管理員主控台**] 視窗中輸入下列命令（請確定仍已選取 [ContosoUniversity] 專案）：</span><span class="sxs-lookup"><span data-stu-id="4c15f-127">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

[!code-powershell[Main](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/samples/sample5.ps1)]

<span data-ttu-id="4c15f-128">當命令完成時，請執行應用程式，然後選取 [講師] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4c15f-128">When the command finishes, run the application and select the Instructors page.</span></span> <span data-ttu-id="4c15f-129">當頁面載入時，您會看到它有新的出生日期欄位。</span><span class="sxs-lookup"><span data-stu-id="4c15f-129">When the page loads, you see that it has the new birth date field.</span></span>

<span data-ttu-id="4c15f-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span><span class="sxs-lookup"><span data-stu-id="4c15f-130">[![Instructors_page_with_birth_date](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image3.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image2.png)</span></span>

## <a name="deploying-the-database-update-to-the-test-environment"></a><span data-ttu-id="4c15f-131">將資料庫更新部署到測試環境</span><span class="sxs-lookup"><span data-stu-id="4c15f-131">Deploying the Database Update to the Test Environment</span></span>

<span data-ttu-id="4c15f-132">在**方案總管**選取 [ContosoUniversity] 專案。</span><span class="sxs-lookup"><span data-stu-id="4c15f-132">In **Solution Explorer** select the ContosoUniversity project.</span></span>

<span data-ttu-id="4c15f-133">在 Web 單鍵的 [**發行**] 工具列中，選取 [**測試**發行設定檔]，然後按一下 [**發佈 Web**]。</span><span class="sxs-lookup"><span data-stu-id="4c15f-133">In the **Web One Click Publish** toolbar, select the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="4c15f-134">（如果工具列已停用，請在**方案總管**中選取 ContosoUniversity 專案）。</span><span class="sxs-lookup"><span data-stu-id="4c15f-134">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

<span data-ttu-id="4c15f-135">Visual Studio 會部署已更新的應用程式，且瀏覽器會開啟至首頁。</span><span class="sxs-lookup"><span data-stu-id="4c15f-135">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span> <span data-ttu-id="4c15f-136">執行 [講師] 頁面，確認已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="4c15f-136">Run the Instructors page to verify that the update was successfully deployed.</span></span> <span data-ttu-id="4c15f-137">當應用程式嘗試存取此頁面的資料庫時，Code First 會更新資料庫架構，並執行 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="4c15f-137">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="4c15f-138">當頁面顯示時，您會看到 [預期的**出生日期] 資料**行中有日期。</span><span class="sxs-lookup"><span data-stu-id="4c15f-138">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>

<span data-ttu-id="4c15f-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span><span class="sxs-lookup"><span data-stu-id="4c15f-139">[![Instructors_page_with_birth_date_Test](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image4.png)</span></span>

## <a name="deploying-the-database-update-to-the-production-environment"></a><span data-ttu-id="4c15f-140">將資料庫更新部署至生產環境</span><span class="sxs-lookup"><span data-stu-id="4c15f-140">Deploying the Database Update to the Production Environment</span></span>

<span data-ttu-id="4c15f-141">您現在可以部署到生產環境。</span><span class="sxs-lookup"><span data-stu-id="4c15f-141">You can now deploy to production.</span></span> <span data-ttu-id="4c15f-142">唯一的差別在於，您將使用*應用程式\_離線的 .htm* ，以防止使用者存取網站，並在您部署變更時更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="4c15f-142">The only difference is that you'll use *app\_offline.htm* to prevent users from accessing the site and thus updating the database while you're deploying changes.</span></span> <span data-ttu-id="4c15f-143">針對生產環境部署，請執行下列步驟：</span><span class="sxs-lookup"><span data-stu-id="4c15f-143">For production deployment perform the following steps:</span></span>

- <span data-ttu-id="4c15f-144">將*應用程式\_離線 .htm*檔案上傳至生產網站。</span><span class="sxs-lookup"><span data-stu-id="4c15f-144">Upload the *app\_offline.htm* file to the production site.</span></span>
- <span data-ttu-id="4c15f-145">在 Visual Studio 中，選擇 Web 單鍵 [**發行**] 工具列中的 [生產設定檔]，然後按一下 [**發佈 Web**]。</span><span class="sxs-lookup"><span data-stu-id="4c15f-145">In Visual Studio, choose the Production profile in the **Web One Click Publish** toolbar and click **Publish Web**.</span></span>
- <span data-ttu-id="4c15f-146">從生產網站刪除*應用程式\_離線 .htm*檔案。</span><span class="sxs-lookup"><span data-stu-id="4c15f-146">Delete the *app\_offline.htm* file from the production site.</span></span>

> [!NOTE]
> <span data-ttu-id="4c15f-147">當您的應用程式在生產環境中使用時，您應該要執行備份計畫。</span><span class="sxs-lookup"><span data-stu-id="4c15f-147">While your application is in use in the production environment you should be implementing a backup plan.</span></span> <span data-ttu-id="4c15f-148">也就是，您應該定期將*School-Prod 的 .sdf*和*aspnet-Prod*檔案從生產網站複製到安全的儲存位置，而且您應該保留數個層代的備份。</span><span class="sxs-lookup"><span data-stu-id="4c15f-148">That is, you should be periodically copying the *School-Prod.sdf* and *aspnet-Prod.sdf* files from the production site to a secure storage location, and you should be keeping several generations of such backups.</span></span> <span data-ttu-id="4c15f-149">當您更新資料庫時，您應該在變更之前立即建立備份複本。</span><span class="sxs-lookup"><span data-stu-id="4c15f-149">When you update the database, you should make a backup copy from immediately before the change.</span></span> <span data-ttu-id="4c15f-150">然後，如果您犯了錯誤，而且在將它部署到生產環境之後卻找不到它，您仍然可以將資料庫復原到損毀之前的狀態。</span><span class="sxs-lookup"><span data-stu-id="4c15f-150">Then, if you make a mistake and don't discover it until after you have deployed it to production, you will still be able to recover the database to the state it was in before it became corrupted.</span></span>

<span data-ttu-id="4c15f-151">當 Visual Studio 在瀏覽器中開啟首頁 URL 時，就會顯示 [ *\_離線的應用程式*] 頁面。</span><span class="sxs-lookup"><span data-stu-id="4c15f-151">When Visual Studio opens the home page URL in the browser, the *app\_offline.htm* page is displayed.</span></span> <span data-ttu-id="4c15f-152">當您刪除*應用程式\_離線的 .htm*檔案之後，您可以再次流覽至您的首頁，以確認更新已成功部署。</span><span class="sxs-lookup"><span data-stu-id="4c15f-152">After you delete the *app\_offline.htm* file, you can browse to your home page again to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="4c15f-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span><span class="sxs-lookup"><span data-stu-id="4c15f-153">[![Instructors_page_with_birth_date_Prod](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image7.png)](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12/_static/image6.png)</span></span>

<span data-ttu-id="4c15f-154">您現在已部署應用程式更新，其中包含對測試和生產環境的資料庫變更。</span><span class="sxs-lookup"><span data-stu-id="4c15f-154">You've now deployed an application update that included a database change to both test and production.</span></span> <span data-ttu-id="4c15f-155">下一個教學課程會示範如何將您的資料庫從 SQL Server Compact 遷移至 SQL Server Express 和 SQL Server。</span><span class="sxs-lookup"><span data-stu-id="4c15f-155">The next tutorial shows you how to migrate your database from SQL Server Compact to SQL Server Express and SQL Server.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4c15f-156">[上一頁](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="4c15f-156">[Previous](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
[Next](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)</span></span>
