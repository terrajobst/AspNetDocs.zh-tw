---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
title: 使用 Visual Studio ASP.NET Web 部署：部署資料庫更新 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 9cad0833-486a-4474-a7f3-7715542ec4ce
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-database-update
msc.type: authoredcontent
ms.openlocfilehash: 805eb84c24764cf921291f89054435601dbac48e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74636823"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-database-update"></a><span data-ttu-id="44b7f-103">使用 Visual Studio ASP.NET Web 部署：部署資料庫更新</span><span class="sxs-lookup"><span data-stu-id="44b7f-103">ASP.NET Web Deployment using Visual Studio: Deploying a Database Update</span></span>

<span data-ttu-id="44b7f-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="44b7f-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="44b7f-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="44b7f-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="44b7f-106">本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。</span><span class="sxs-lookup"><span data-stu-id="44b7f-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="44b7f-107">如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。</span><span class="sxs-lookup"><span data-stu-id="44b7f-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="44b7f-108">概觀</span><span class="sxs-lookup"><span data-stu-id="44b7f-108">Overview</span></span>

<span data-ttu-id="44b7f-109">在本教學課程中，您會進行資料庫變更和相關的程式碼變更、在 Visual Studio 中測試變更，然後將更新部署到測試、預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="44b7f-109">In this tutorial, you make a database change and related code changes, test the changes in Visual Studio, then deploy the update to the test, staging, and production environments.</span></span>

<span data-ttu-id="44b7f-110">本教學課程會先示範如何更新 Code First 移轉所管理的資料庫，然後再說明如何使用 dbDacFx 提供者更新資料庫。</span><span class="sxs-lookup"><span data-stu-id="44b7f-110">The tutorial first shows how to update a database that is managed by Code First Migrations, and then later it shows how to update a database by using the dbDacFx provider.</span></span>

<span data-ttu-id="44b7f-111">提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="44b7f-111">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="deploy-a-database-update-by-using-code-first-migrations"></a><span data-ttu-id="44b7f-112">使用 Code First 移轉部署資料庫更新</span><span class="sxs-lookup"><span data-stu-id="44b7f-112">Deploy a database update by using Code First Migrations</span></span>

<span data-ttu-id="44b7f-113">在本節中，您會將「出生日期」資料行加入 `Student` 和 `Instructor` 實體的 `Person` 基類。</span><span class="sxs-lookup"><span data-stu-id="44b7f-113">In this section, you add a birth date column to the `Person` base class for the `Student` and `Instructor` entities.</span></span> <span data-ttu-id="44b7f-114">接著，您會更新顯示講師資料的頁面，使其顯示新的資料行。</span><span class="sxs-lookup"><span data-stu-id="44b7f-114">Then you update the page that displays instructor data so that it displays the new column.</span></span> <span data-ttu-id="44b7f-115">最後，您會將變更部署到測試、預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="44b7f-115">Finally, you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-application-database"></a><span data-ttu-id="44b7f-116">將資料行新增至應用程式資料庫中的資料表</span><span class="sxs-lookup"><span data-stu-id="44b7f-116">Add a column to a table in the application database</span></span>

1. <span data-ttu-id="44b7f-117">在*ContosoUniversity*專案中，開啟*Person.cs* ，並在 `Person` 類別的結尾處新增下列屬性（後面應該有兩個右大括弧）：</span><span class="sxs-lookup"><span data-stu-id="44b7f-117">In the *ContosoUniversity.DAL* project, open *Person.cs* and add the following property at the end of the `Person` class (there should be two closing curly braces following it):</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample1.cs)]

    <span data-ttu-id="44b7f-118">接下來，更新 `Seed` 方法，讓它提供新資料行的值。</span><span class="sxs-lookup"><span data-stu-id="44b7f-118">Next, update the `Seed` method so that it provides a value for the new column.</span></span> <span data-ttu-id="44b7f-119">開啟*Migrations\Configuration.cs* ，並將開始 `var instructors = new List<Instructor>` 的程式碼區塊取代為下列包含出生日期資訊的程式碼區塊：</span><span class="sxs-lookup"><span data-stu-id="44b7f-119">Open *Migrations\Configuration.cs* and replace the code block that begins `var instructors = new List<Instructor>` with the following code block which includes birth date information:</span></span>

    [!code-csharp[Main](deploying-a-database-update/samples/sample2.cs)]
2. <span data-ttu-id="44b7f-120">建立解決方案，然後開啟 [**套件管理員主控台**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="44b7f-120">Build the solution, and then open the **Package Manager Console** window.</span></span> <span data-ttu-id="44b7f-121">請確定 [ContosoUniversity] 仍然選取為 [**預設專案**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-121">Make sure that ContosoUniversity.DAL is still selected as the **Default project**.</span></span>
3. <span data-ttu-id="44b7f-122">在 [**套件管理員主控台**] 視窗中，選取 [ **ContosoUniversity** ] 做為**預設專案**，然後輸入下列命令：</span><span class="sxs-lookup"><span data-stu-id="44b7f-122">In the **Package Manager Console** window, select **ContosoUniversity.DAL** as the **Default project**, and then enter the following command:</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample3.ps1)]

    <span data-ttu-id="44b7f-123">當此命令完成時，Visual Studio 會開啟定義新 `DbMigration` 類別的類別檔案，而在 `Up` 方法中，您可以看到建立新資料行的程式碼。</span><span class="sxs-lookup"><span data-stu-id="44b7f-123">When this command finishes, Visual Studio opens the class file that defines the new `DbMigration` class, and in the `Up` method you can see the code that creates the new column.</span></span> <span data-ttu-id="44b7f-124">當您執行變更時，`Up` 方法會建立資料行，而 `Down` 方法則會在您回復變更時刪除資料行。</span><span class="sxs-lookup"><span data-stu-id="44b7f-124">The `Up` method creates the column when you are implementing the change, and the `Down` method deletes the column when you are rolling back the change.</span></span>

    ![AddBirthDate_migration_code](deploying-a-database-update/_static/image1.png)
4. <span data-ttu-id="44b7f-126">建立解決方案，然後在 [**套件管理員主控台**] 視窗中輸入下列命令（請確定仍已選取 [ContosoUniversity] 專案）：</span><span class="sxs-lookup"><span data-stu-id="44b7f-126">Build the solution, and then enter the following command in the **Package Manager Console** window (make sure the ContosoUniversity.DAL project is still selected):</span></span>

    [!code-powershell[Main](deploying-a-database-update/samples/sample4.ps1)]

    <span data-ttu-id="44b7f-127">Entity Framework 會執行 `Up` 方法，然後執行 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="44b7f-127">The Entity Framework runs the `Up` method and then runs the `Seed` method.</span></span>

### <a name="display-the-new-column-in-the-instructors-page"></a><span data-ttu-id="44b7f-128">在 [講師] 頁面中顯示新的資料行</span><span class="sxs-lookup"><span data-stu-id="44b7f-128">Display the new column in the Instructors page</span></span>

1. <span data-ttu-id="44b7f-129">在 ContosoUniversity 專案中，開啟 [ *default.aspx* ]，然後新增 [範本] 欄位以顯示出生日期。</span><span class="sxs-lookup"><span data-stu-id="44b7f-129">In the ContosoUniversity project, open *Instructors.aspx* and add a new template field to display the birth date.</span></span> <span data-ttu-id="44b7f-130">將其新增至 [雇用日期] 和 [辦公室指派]：</span><span class="sxs-lookup"><span data-stu-id="44b7f-130">Add it between the ones for hire date and office assignment:</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample5.aspx?highlight=9-17)]

    <span data-ttu-id="44b7f-131">（如果程式碼縮排無法同步處理，您可以按下 CTRL-K，然後按 CTRL-D 自動重新格式化檔案）。</span><span class="sxs-lookup"><span data-stu-id="44b7f-131">(If code indentation gets out of sync, you can press CTRL-K and then CTRL-D to automatically reformat the file.)</span></span>
2. <span data-ttu-id="44b7f-132">執行應用程式，然後按一下 [**講師**] 連結。</span><span class="sxs-lookup"><span data-stu-id="44b7f-132">Run the application and click the **Instructors** link.</span></span>

    <span data-ttu-id="44b7f-133">當頁面載入時，您會看到它有新的出生日期欄位。</span><span class="sxs-lookup"><span data-stu-id="44b7f-133">When the page loads, you see that it has the new birth date field.</span></span>

    ![具有生日的講師頁面](deploying-a-database-update/_static/image2.png)
3. <span data-ttu-id="44b7f-135">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="44b7f-135">Close the browser.</span></span>

### <a name="deploy-the-database-update"></a><span data-ttu-id="44b7f-136">部署資料庫更新</span><span class="sxs-lookup"><span data-stu-id="44b7f-136">Deploy the database update</span></span>

1. <span data-ttu-id="44b7f-137">在**方案總管**選取 [ContosoUniversity] 專案。</span><span class="sxs-lookup"><span data-stu-id="44b7f-137">In **Solution Explorer** select the ContosoUniversity project.</span></span>
2. <span data-ttu-id="44b7f-138">在 Web 單鍵的 [**發行**] 工具列中，按一下 [**測試**發行設定檔]，然後按一下 [**發佈 Web**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-138">In the **Web One Click Publish** toolbar, click the **Test** publish profile, and then click **Publish Web**.</span></span> <span data-ttu-id="44b7f-139">（如果工具列已停用，請在**方案總管**中選取 ContosoUniversity 專案）。</span><span class="sxs-lookup"><span data-stu-id="44b7f-139">(If the toolbar is disabled, select the ContosoUniversity project in **Solution Explorer**.)</span></span>

    <span data-ttu-id="44b7f-140">Visual Studio 會部署已更新的應用程式，且瀏覽器會開啟至首頁。</span><span class="sxs-lookup"><span data-stu-id="44b7f-140">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
3. <span data-ttu-id="44b7f-141">執行 [**講師**] 頁面，確認已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="44b7f-141">Run the **Instructors** page to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="44b7f-142">當應用程式嘗試存取此頁面的資料庫時，Code First 會更新資料庫架構，並執行 `Seed` 方法。</span><span class="sxs-lookup"><span data-stu-id="44b7f-142">When the application tries to access the database for this page, Code First updates the database schema and runs the `Seed` method.</span></span> <span data-ttu-id="44b7f-143">當頁面顯示時，您會看到 [預期的**出生日期] 資料**行中有日期。</span><span class="sxs-lookup"><span data-stu-id="44b7f-143">When the page displays, you see the expected **Birth Date** column with dates in it.</span></span>
4. <span data-ttu-id="44b7f-144">在 Web 單鍵的 [**發行**] 工具列中，按一下 [**臨時**發行] 設定檔，然後按一下 [**發佈 Web**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-144">In the **Web One Click Publish** toolbar, click the **Staging** publish profile, and then click **Publish Web**.</span></span>
5. <span data-ttu-id="44b7f-145">在預備環境中執行**講師**頁面，確認已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="44b7f-145">Run the **Instructors** page in staging to verify that the update was successfully deployed.</span></span>
6. <span data-ttu-id="44b7f-146">在 Web 單鍵的 [**發行**] 工具列中，按一下 [**生產**] 發行設定檔，然後按一下 [**發佈 Web**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-146">In the **Web One Click Publish** toolbar, click the **Production** publish profile, and then click **Publish Web**.</span></span>
7. <span data-ttu-id="44b7f-147">在生產環境中執行**講師**頁面，確認已成功部署更新。</span><span class="sxs-lookup"><span data-stu-id="44b7f-147">Run the **Instructors** page in production to verify that the update was successfully deployed.</span></span>

    <span data-ttu-id="44b7f-148">對於包含資料庫變更的實際生產應用程式更新，您通常也會在 *\_* 部署期間讓應用程式離線，如您在上一個教學課程中所見。</span><span class="sxs-lookup"><span data-stu-id="44b7f-148">For a real production application update that includes a database change you would also typically take the application offline during deployment by using *app\_offline.htm*, as you saw in the previous tutorial.</span></span>

## <a name="deploy-a-database-update-by-using-the-dbdacfx-provider"></a><span data-ttu-id="44b7f-149">使用 dbDacFx 提供者來部署資料庫更新</span><span class="sxs-lookup"><span data-stu-id="44b7f-149">Deploy a database update by using the dbDacFx provider</span></span>

<span data-ttu-id="44b7f-150">在本節中，您會將 [*批註*] 資料行新增至成員資格資料庫中的*使用者*資料表，並建立一個頁面，讓您顯示和編輯每個使用者的批註。</span><span class="sxs-lookup"><span data-stu-id="44b7f-150">In this section, you add a *Comments* column to the *User* table in the membership database and create a page that lets you display and edit comments for each user.</span></span> <span data-ttu-id="44b7f-151">然後，將變更部署到測試、預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="44b7f-151">Then you deploy the changes to test, staging, and production.</span></span>

### <a name="add-a-column-to-a-table-in-the-membership-database"></a><span data-ttu-id="44b7f-152">將資料行加入至成員資格資料庫中的資料表</span><span class="sxs-lookup"><span data-stu-id="44b7f-152">Add a column to a table in the membership database</span></span>

1. <span data-ttu-id="44b7f-153">在 Visual Studio 中，開啟**SQL Server 物件總管**。</span><span class="sxs-lookup"><span data-stu-id="44b7f-153">In Visual Studio, open **SQL Server Object Explorer**.</span></span>
2. <span data-ttu-id="44b7f-154">依序展開 **[（localdb）] \v11.0、[** **資料庫**] 和 [ **aspnet-ContosoUniversity** （不是**aspnet-ContosoUniversity-生產**）]，然後展開 [**資料表]** 。</span><span class="sxs-lookup"><span data-stu-id="44b7f-154">Expand **(localdb)\v11.0**, expand **Databases**, expand **aspnet-ContosoUniversity** (not **aspnet-ContosoUniversity-Prod**) and then expand **Tables**.</span></span>

    <span data-ttu-id="44b7f-155">如果您在 [ **SQL Server** ] 節點底下看不到 [ **（localdb）] \v11.0** ，請以滑鼠右鍵按一下 [ **SQL Server** ] 節點，然後按一下 [**新增 SQL Server**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-155">If you don't see **(localdb)\v11.0** under the **SQL Server** node, right-click the **SQL Server** node and click **Add SQL Server**.</span></span> <span data-ttu-id="44b7f-156">在 [**連接到伺服器**] 對話方塊中，輸入 *（localdb） \V11.0*做為**伺服器名稱**，然後按一下 **[連接]** 。</span><span class="sxs-lookup"><span data-stu-id="44b7f-156">In the **Connect to Server** dialog box enter *(localdb)\v11.0* as the **Server name**, and then click **Connect**.</span></span>

    <span data-ttu-id="44b7f-157">如果您看不到 [ **aspnet-ContosoUniversity**]，請執行專案並使用系統*管理員*認證登入（密碼是*devpwd*），然後重新整理 [ **SQL Server 物件總管**] 視窗。</span><span class="sxs-lookup"><span data-stu-id="44b7f-157">If you don't see **aspnet-ContosoUniversity**, run the project and log in using the *admin* credentials (password is *devpwd*), and then refresh the **SQL Server Object Explorer** window.</span></span>
3. <span data-ttu-id="44b7f-158">以滑鼠右鍵按一下 [**使用者**] 資料表，然後按一下 [**視圖設計**工具]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-158">Right-click the **Users** table, and then click **View Designer**.</span></span>

    ![SSOX 視圖設計工具](deploying-a-database-update/_static/image3.png)
4. <span data-ttu-id="44b7f-160">在設計工具中，新增 [*批註*] 資料行，並將它設為*Nvarchar （128）* 且可為 null，然後按一下 [**更新**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-160">In the designer, add a *Comments* column and make it *nvarchar(128)* and nullable, and then click **Update**.</span></span>

    ![加入批註資料行](deploying-a-database-update/_static/image4.png)
5. <span data-ttu-id="44b7f-162">在 [**預覽資料庫更新**] 方塊中，按一下 [**更新資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-162">In the **Preview Database Updates** box, click **Update Database**.</span></span>

    ![預覽資料庫更新](deploying-a-database-update/_static/image5.png)

### <a name="create-a-page-to-display-and-edit-the-new-column"></a><span data-ttu-id="44b7f-164">建立頁面以顯示和編輯新的資料行</span><span class="sxs-lookup"><span data-stu-id="44b7f-164">Create a page to display and edit the new column</span></span>

1. <span data-ttu-id="44b7f-165">在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案中的 [**帳戶**] 資料夾，按一下 [**加入**]，然後按一下 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-165">In **Solution Explorer**, right-click the **Account** folder in the ContosoUniversity project, click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="44b7f-166">**使用主版頁面建立新的 Web 表單**，並將其命名為*使用者名稱 .aspx*。</span><span class="sxs-lookup"><span data-stu-id="44b7f-166">Create a new **Web Form Using Master Page** and name it *UserInfo.aspx*.</span></span> <span data-ttu-id="44b7f-167">接受預設的*網站*檔案作為主版頁面。</span><span class="sxs-lookup"><span data-stu-id="44b7f-167">Accept the default *Site.Master* file as the master page.</span></span>
3. <span data-ttu-id="44b7f-168">將下列標記複製到 `MainContent` `Content` 元素（3個 `Content` 元素的最後一個）：</span><span class="sxs-lookup"><span data-stu-id="44b7f-168">Copy the following markup into the `MainContent` `Content` element (the last of the 3 `Content` elements):</span></span>

    [!code-aspx[Main](deploying-a-database-update/samples/sample6.aspx)]
4. <span data-ttu-id="44b7f-169">以滑鼠右鍵按一下 [*使用者資訊 .aspx* ] 頁面，然後按一下 [**在瀏覽器中查看**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-169">Right-click the *UserInfo.aspx* page and click **View in Browser**.</span></span>
5. <span data-ttu-id="44b7f-170">使用您的系統*管理員*使用者認證登入（密碼為*devpwd*），並為使用者新增一些批註，以確認網頁是否正常運作。</span><span class="sxs-lookup"><span data-stu-id="44b7f-170">Log in with your *admin* user credentials (password is *devpwd*) and add some comments to a user to verify that the page works correctly.</span></span>

    ![使用者資訊頁面](deploying-a-database-update/_static/image6.png)
6. <span data-ttu-id="44b7f-172">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="44b7f-172">Close the browser.</span></span>

## <a name="deploy-the-database-update"></a><span data-ttu-id="44b7f-173">部署資料庫更新</span><span class="sxs-lookup"><span data-stu-id="44b7f-173">Deploy the database update</span></span>

<span data-ttu-id="44b7f-174">若要使用 dbDacFx 提供者進行部署，您只需要選取發行設定檔中的 [**更新資料庫**] 選項。</span><span class="sxs-lookup"><span data-stu-id="44b7f-174">To deploy by using the dbDacFx provider, you just need to select the **Update database** option in the publish profile.</span></span> <span data-ttu-id="44b7f-175">不過，在使用此選項時，您也設定了一些額外的 SQL 腳本來執行：那些仍在設定檔中，因此您必須避免它們再次執行。</span><span class="sxs-lookup"><span data-stu-id="44b7f-175">However, for the initial deployment when you used this option you also configured some additional SQL scripts to run: those are still in the profile and you'll have to prevent them from running again.</span></span>

1. <span data-ttu-id="44b7f-176">以滑鼠右鍵按一下 [ContosoUniversity] 專案，然後按一下 [**發佈**]，以開啟 [**發佈 Web** wizard]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-176">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="44b7f-177">選取**測試**設定檔。</span><span class="sxs-lookup"><span data-stu-id="44b7f-177">Select the **Test** profile.</span></span>
3. <span data-ttu-id="44b7f-178">按一下 [**設定**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="44b7f-178">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="44b7f-179">在 [ **DefaultConnection**] 底下，選取 [**更新資料庫**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-179">Under **DefaultConnection**, select **Update database**.</span></span>
5. <span data-ttu-id="44b7f-180">停用您設定為初始部署執行的其他腳本：</span><span class="sxs-lookup"><span data-stu-id="44b7f-180">Disable the additional scripts that you configured to run for the initial deployment:</span></span>

    1. <span data-ttu-id="44b7f-181">按一下 [**設定資料庫更新**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-181">Click **Configure database updates**.</span></span>
    2. <span data-ttu-id="44b7f-182">在 [**設定資料庫更新**] 對話方塊中，清除 [*授與 .sql* ] 和 [ *aspnet-data-dev*] 旁的核取方塊。</span><span class="sxs-lookup"><span data-stu-id="44b7f-182">In the **Configure Database Updates** dialog box, clear the check boxes next to *Grant.sql* and *aspnet-data-dev.sql*.</span></span>
    3. <span data-ttu-id="44b7f-183">按一下 [ **關閉**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-183">Click **Close**.</span></span>
6. <span data-ttu-id="44b7f-184">按一下 [**預覽**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="44b7f-184">Click the **Preview** tab.</span></span>
7. <span data-ttu-id="44b7f-185">在 [**資料庫**] 底下的 [ **DefaultConnection**] 右邊，按一下 [**預覽資料庫**] 連結。</span><span class="sxs-lookup"><span data-stu-id="44b7f-185">Under **Databases** and to the right of **DefaultConnection**, click the **Preview database** link.</span></span>

    ![資料庫預覽](deploying-a-database-update/_static/image7.png)

    <span data-ttu-id="44b7f-187">[預覽] 視窗會顯示將在目的地資料庫中執行的腳本，讓該資料庫架構符合源資料庫的架構。</span><span class="sxs-lookup"><span data-stu-id="44b7f-187">The preview window shows the script that will be run in the destination database to make that database schema match the schema of the source database.</span></span> <span data-ttu-id="44b7f-188">此腳本包含可加入新資料行的 ALTER TABLE 命令。</span><span class="sxs-lookup"><span data-stu-id="44b7f-188">The script includes an ALTER TABLE command that adds the new column.</span></span>
8. <span data-ttu-id="44b7f-189">關閉 [**資料庫預覽**] 對話方塊，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="44b7f-189">Close the **Database Preview** dialog box, and then click **Publish**.</span></span>

    <span data-ttu-id="44b7f-190">Visual Studio 會部署已更新的應用程式，且瀏覽器會開啟至首頁。</span><span class="sxs-lookup"><span data-stu-id="44b7f-190">Visual Studio deploys the updated application, and the browser opens to the home page.</span></span>
9. <span data-ttu-id="44b7f-191">執行 [使用者資訊] 頁面（將*帳戶/使用者資訊*類型新增至首頁 URL），以確認更新已成功部署。</span><span class="sxs-lookup"><span data-stu-id="44b7f-191">Run the UserInfo page (add *Account/UserInfo.aspx* to the home page URL) to verify that the update was successfully deployed.</span></span> <span data-ttu-id="44b7f-192">您必須輸入*admin*和*devpwd*來登入。</span><span class="sxs-lookup"><span data-stu-id="44b7f-192">You'll have to log in by entering *admin* and *devpwd*.</span></span>

    <span data-ttu-id="44b7f-193">根據預設，資料表中的資料不會部署，而且您不會設定要執行的資料部署腳本，因此您不會發現在開發中新增的批註。</span><span class="sxs-lookup"><span data-stu-id="44b7f-193">Data in tables is not deployed by default, and you didn't configure a data deployment script to run, so you won't find the comment that you added in development.</span></span> <span data-ttu-id="44b7f-194">您現在可以在預備環境中加入新的批註，以確認變更已部署至資料庫，且網頁運作正常。</span><span class="sxs-lookup"><span data-stu-id="44b7f-194">You can add a new comment now in staging to verify that the change was deployed to the database and the page works correctly.</span></span>
10. <span data-ttu-id="44b7f-195">遵循相同的程式部署至預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="44b7f-195">Follow the same procedure to deploy to staging and production.</span></span>

    <span data-ttu-id="44b7f-196">別忘了停用額外的腳本。</span><span class="sxs-lookup"><span data-stu-id="44b7f-196">Don't forget to disable the extra scripts.</span></span> <span data-ttu-id="44b7f-197">與測試組態檔相較之下，唯一的差別在於，您只會在預備和生產設定檔中停用一個腳本，因為它們已設定為僅執行*aspnet-prod-data。*</span><span class="sxs-lookup"><span data-stu-id="44b7f-197">The only difference compared to the Test profile is that you will disable only one script in the Staging and Production profiles because they were configured to run only *aspnet-prod-data.sql*.</span></span>

    <span data-ttu-id="44b7f-198">預備和生產的認證是 admin 和 prodpwd。</span><span class="sxs-lookup"><span data-stu-id="44b7f-198">The credentials for staging and production are admin and prodpwd.</span></span>

    <span data-ttu-id="44b7f-199">對於包含資料庫變更的實際生產應用程式更新，您通常也會在部署期間將應用程式離線，方法是先上傳應用程式 *\_離線*，然後再發佈和刪除它，如同您在[上一個教學](deploying-a-code-update.md)課程中所見。</span><span class="sxs-lookup"><span data-stu-id="44b7f-199">For a real production application update that includes a database change you would also typically take the application offline during deployment by uploading *app\_offline.htm* before publishing and deleting it afterward, as you saw in [the previous tutorial](deploying-a-code-update.md).</span></span>

## <a name="summary"></a><span data-ttu-id="44b7f-200">總結</span><span class="sxs-lookup"><span data-stu-id="44b7f-200">Summary</span></span>

<span data-ttu-id="44b7f-201">您現在已部署應用程式更新，其中包含使用 Code First 移轉和 dbDacFx 提供者的資料庫變更。</span><span class="sxs-lookup"><span data-stu-id="44b7f-201">You've now deployed an application update that included a database change using both Code First Migrations and the dbDacFx provider.</span></span>

![具有生日的講師頁面](deploying-a-database-update/_static/image8.png)

![使用者資訊頁面](deploying-a-database-update/_static/image9.png)

<span data-ttu-id="44b7f-204">下一個教學課程說明如何使用命令列執行部署。</span><span class="sxs-lookup"><span data-stu-id="44b7f-204">The next tutorial shows you how to execute deployments by using the command line.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="44b7f-205">[上一頁](deploying-a-code-update.md)
> [下一頁](command-line-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="44b7f-205">[Previous](deploying-a-code-update.md)
[Next](command-line-deployment.md)</span></span>
