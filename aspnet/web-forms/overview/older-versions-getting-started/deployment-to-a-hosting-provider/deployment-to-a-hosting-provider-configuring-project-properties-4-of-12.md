---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
title: 部署 ASP.NET Web 應用程式與 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer:設定專案屬性-4，12 個 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何部署 （發行） 的 ASP.NET web 應用程式專案，其中包含 SQL Server Compact 資料庫，使用 Visual Stu...
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 8b013630-842c-4d44-a6fc-c6be43e7210f
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-configuring-project-properties-4-of-12
msc.type: authoredcontent
ms.openlocfilehash: ecd169f70eee162a647f6ea827ba5649b6c22ffd
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57054515"
---
<a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-configuring-project-properties---4-of-12"></a><span data-ttu-id="555bc-103">部署 ASP.NET Web 應用程式與 SQL Server Compact 使用 Visual Studio 或 Visual Web Developer:設定專案屬性-4，12 個</span><span class="sxs-lookup"><span data-stu-id="555bc-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Configuring Project Properties - 4 of 12</span></span>
====================
<span data-ttu-id="555bc-104">藉由[Tom Dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="555bc-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="555bc-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="555bc-105">Download Starter Project</span></span>](http://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="555bc-106">這一系列的教學課程會示範如何部署 （發行） 的 ASP.NET web 應用程式專案使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web 包含 SQL Server Compact 資料庫。</span><span class="sxs-lookup"><span data-stu-id="555bc-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="555bc-107">如果您安裝 Web Publish Update，您也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="555bc-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="555bc-108">在數列的簡介，請參閱[系列的第一個教學課程](deployment-to-a-hosting-provider-introduction-1-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="555bc-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="555bc-109">顯示 Visual Studio 2012 RC 版本之後引入的部署功能，示範如何部署 SQL Server Compact，以外的 SQL Server 版本，並示範如何部署至 Azure App Service Web Apps 的教學課程，請參閱[ASP.NET Web 部署使用 Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="555bc-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>


## <a name="overview"></a><span data-ttu-id="555bc-110">總覽</span><span class="sxs-lookup"><span data-stu-id="555bc-110">Overview</span></span>

<span data-ttu-id="555bc-111">儲存專案檔中的專案內容中所設定的某些部署選項 ( *.csproj*或是 *.vbproj*檔案)。</span><span class="sxs-lookup"><span data-stu-id="555bc-111">Some deployment options are configured in project properties that are stored in the project file (the *.csproj* or *.vbproj* file).</span></span> <span data-ttu-id="555bc-112">在大部分情況下，這些設定的預設值是什麼您想要的但您可以使用**專案屬性**UI 內建於 Visual Studio 搭配使用這些設定，如果您需要變更它們。</span><span class="sxs-lookup"><span data-stu-id="555bc-112">In most cases, the default values of these settings are what you want, but you can use the **Project Properties** UI built into Visual Studio to work with these settings if you have to change them.</span></span> <span data-ttu-id="555bc-113">在本教學課程中，您檢閱中的部署設定**專案屬性**。</span><span class="sxs-lookup"><span data-stu-id="555bc-113">In this tutorial you review the deployment settings in **Project Properties**.</span></span> <span data-ttu-id="555bc-114">您也會建立預留位置檔案會造成要部署的空資料夾。</span><span class="sxs-lookup"><span data-stu-id="555bc-114">You also create a placeholder file that causes an empty folder to be deployed.</span></span>

## <a name="configuring-deployment-settings-in-the-project-properties-window"></a><span data-ttu-id="555bc-115">在 [專案屬性] 視窗中設定部署設定</span><span class="sxs-lookup"><span data-stu-id="555bc-115">Configuring Deployment Settings in the Project Properties Window</span></span>

<span data-ttu-id="555bc-116">如您所見下列的教學課程中，大部分的設定會影響部署期間進行的作業會納入發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="555bc-116">Most settings that affect what happens during deployment are included in the publish profile, as you'll see in the following tutorials.</span></span> <span data-ttu-id="555bc-117">您應該要注意的幾個設定都位於**封裝/發行**索引標籤**專案屬性**視窗。</span><span class="sxs-lookup"><span data-stu-id="555bc-117">A few settings that you should be aware of are located in the **Package/Publish** tabs of the **Project Properties** window.</span></span> <span data-ttu-id="555bc-118">這些設定會指定每個組建組態 — 也就是有不同的設定，在發行組建，比您的偵錯組建。</span><span class="sxs-lookup"><span data-stu-id="555bc-118">These settings are specified for each build configuration — that is, you can have different settings for a Release build than you have for a Debug build.</span></span>

<span data-ttu-id="555bc-119">在 **方案總管 中**，以滑鼠右鍵按一下**ContosoUniversity**專案，然後選取**屬性**，然後選取**封裝/發行 Web** 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="555bc-119">In **Solution Explorer**, right-click the **ContosoUniversity** project, select **Properties**, and then select the **Package/Publish Web** tab.</span></span>

![Package_Publish_Web_tab](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image1.png)

<span data-ttu-id="555bc-121">視窗顯示時，則預設為顯示設定任何的建置組態目前作用中的解決方案。</span><span class="sxs-lookup"><span data-stu-id="555bc-121">When the window is displayed, it defaults to showing settings for whichever build configuration is currently active for the solution.</span></span> <span data-ttu-id="555bc-122">如果**組態** 方塊中不會指出**作用 （發行）**，選取**版本**才能顯示 發行 組建組態設定。</span><span class="sxs-lookup"><span data-stu-id="555bc-122">If the **Configuration** box does not indicate **Active (Release)**, select **Release** in order to display settings for the Release build configuration.</span></span> <span data-ttu-id="555bc-123">您會將發行組建部署到您的測試和生產環境。</span><span class="sxs-lookup"><span data-stu-id="555bc-123">You'll deploy Release builds to both your test and production environments.</span></span>

![Package_Publish_Web_tab_selecting_Release](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image2.png)

<span data-ttu-id="555bc-125">與**作用 （發行）** 或是**版本**選取，您看到當您部署使用 [發行] 組建組態時有效的值：</span><span class="sxs-lookup"><span data-stu-id="555bc-125">With **Active (Release)** or **Release** selected, you see the values that are effective when you deploy using the Release build configuration:</span></span>

- <span data-ttu-id="555bc-126">在 [**要部署的項目**] 方塊中，**只執行應用程式所需的檔案**已選取。</span><span class="sxs-lookup"><span data-stu-id="555bc-126">In the **Items to deploy** box, **Only files needed to run the application** is selected.</span></span> <span data-ttu-id="555bc-127">其他選項包括**此專案中的所有檔案**或是**此專案資料夾中的所有檔案**。</span><span class="sxs-lookup"><span data-stu-id="555bc-127">Other options are **All files in this project** or **All files in this project folder**.</span></span> <span data-ttu-id="555bc-128">藉由保留預設選取項目不會變更您避免部署原始程式碼檔案，例如。</span><span class="sxs-lookup"><span data-stu-id="555bc-128">By leaving the default selection unchanged you avoid deploying source code files, for example.</span></span> <span data-ttu-id="555bc-129">這項設定是包含 SQL Server Compact 的二進位檔案的資料夾必須包含在專案中的原因的原因。</span><span class="sxs-lookup"><span data-stu-id="555bc-129">This setting is the reason why the folders that contain the SQL Server Compact binary files had to be included in the project.</span></span> <span data-ttu-id="555bc-130">如需有關這項設定的詳細資訊，請參閱 <<c0>  **為什麼不在我的專案資料夾中檔案的所有部署？** 中[ASP.NET Web 應用程式專案部署常見問題集](https://msdn.microsoft.com/library/ee942158.aspx)。</span><span class="sxs-lookup"><span data-stu-id="555bc-130">For more information about this setting, see **Why don't all of the files in my project folder get deployed?** in [ASP.NET Web Application Project Deployment FAQ](https://msdn.microsoft.com/library/ee942158.aspx).</span></span>
- <span data-ttu-id="555bc-131">**排除產生偵錯符號**已選取。</span><span class="sxs-lookup"><span data-stu-id="555bc-131">**Exclude generated debug symbols** is selected.</span></span> <span data-ttu-id="555bc-132">當您使用這個組建組態時，您將不會偵錯。</span><span class="sxs-lookup"><span data-stu-id="555bc-132">You won't be debugging when you use this build configuration.</span></span>
- <span data-ttu-id="555bc-133">**從應用程式中排除檔案\_Data 資料夾**未選取。</span><span class="sxs-lookup"><span data-stu-id="555bc-133">**Exclude files from the App\_Data folder** is not selected.</span></span> <span data-ttu-id="555bc-134">您的成員資格資料庫的 SQL Server Compact 檔案是在該資料夾中，您必須將它部署。</span><span class="sxs-lookup"><span data-stu-id="555bc-134">Your SQL Server Compact file for the membership database is in that folder and you have to deploy it.</span></span> <span data-ttu-id="555bc-135">當您部署不包含資料庫變更的更新時，您會選取此核取方塊。</span><span class="sxs-lookup"><span data-stu-id="555bc-135">When you deploy updates that do not include database changes, you'll select this checkbox.</span></span>
- <span data-ttu-id="555bc-136">**先行編譯此應用程式發行前的**未選取。</span><span class="sxs-lookup"><span data-stu-id="555bc-136">**Precompile this application before publishing** is not selected.</span></span> <span data-ttu-id="555bc-137">在大部分情況下，沒有需要先行編譯 web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="555bc-137">In most scenarios, there's no need to precompile web application projects.</span></span> <span data-ttu-id="555bc-138">如需有關這個選項的詳細資訊，請參閱 <<c0> [ 封裝/發行 Web 索引標籤中，專案屬性](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx)並[進階先行編譯設定對話方塊](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx)。</span><span class="sxs-lookup"><span data-stu-id="555bc-138">For more information about this option, see [Package/Publish Web Tab, Project Properties](https://msdn.microsoft.com/library/dd410108(v=vs.110).aspx) and [Advanced Precompile Settings Dialog](https://msdn.microsoft.com/library/hh475319(v=vs.110).aspx).</span></span>
- <span data-ttu-id="555bc-139">**包含在封裝/發行 SQL 索引標籤中設定的所有資料庫**已選取此選項沒有任何作用現在因為您未設定，但**封裝/發行 SQL**  索引標籤。該索引標籤是用來是唯一的選項，部署 SQL Server 資料庫的舊版資料庫部署方法。</span><span class="sxs-lookup"><span data-stu-id="555bc-139">**Include all databases configured in Package/Publish SQL tab** is selected, but this option has no effect now because you aren't configuring the **Package/Publish SQL** tab. That tab is for a legacy database deployment method that used to be the only option for deploying SQL Server databases.</span></span> <span data-ttu-id="555bc-140">您將使用**封裝/發行 SQL**索引標籤中[移轉至 SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)教學課程。</span><span class="sxs-lookup"><span data-stu-id="555bc-140">You'll use the **Package/Publish SQL** tab in the [Migrating to SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md) tutorial.</span></span>
- <span data-ttu-id="555bc-141">**Web Deployment 封裝設定**區段不適用，因為您使用單鍵發行在這些教學課程。</span><span class="sxs-lookup"><span data-stu-id="555bc-141">The **Web Deployment Package Settings** section does not apply because you're using one-click publish in these tutorials.</span></span>

<span data-ttu-id="555bc-142">變更**組態**下拉式清單方塊，以偵錯以查看針對偵錯組建的預設設定。</span><span class="sxs-lookup"><span data-stu-id="555bc-142">Change the **Configuration** drop-down box to Debug to see the default settings for Debug builds.</span></span> <span data-ttu-id="555bc-143">這些值都相同，除了**排除產生偵錯符號**已清除，以便您可以偵錯，當您部署的偵錯組建。</span><span class="sxs-lookup"><span data-stu-id="555bc-143">The values are the same, except **Exclude generated debug symbols** is cleared so that you can debug when you deploy a Debug build.</span></span>

## <a name="making-sure-that-the-elmah-folder-gets-deployed"></a><span data-ttu-id="555bc-144">讓確定 Elmah 資料夾取得部署</span><span class="sxs-lookup"><span data-stu-id="555bc-144">Making Sure that the Elmah Folder gets Deployed</span></span>

<span data-ttu-id="555bc-145">如您在先前的教學課程中所見[Elmah NuGet 套件](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx)提供的錯誤記錄和報告功能。</span><span class="sxs-lookup"><span data-stu-id="555bc-145">As you saw in the previous tutorial, the [Elmah NuGet package](http://www.hanselman.com/blog/NuGetPackageOfTheWeek7ELMAHErrorLoggingModulesAndHandlersWithSQLServerCompact.aspx) provides functionality for error logging and reporting.</span></span> <span data-ttu-id="555bc-146">Contoso 大學應用程式中 Elmah 已設定為將錯誤詳細資料儲存在名為的資料夾*Elmah*:</span><span class="sxs-lookup"><span data-stu-id="555bc-146">In the Contoso University application Elmah has been configured to store error details in a folder named *Elmah*:</span></span>

![Elmah 資料夾](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12/_static/image3.png)

<span data-ttu-id="555bc-148">從部署中排除特定檔案或資料夾是常見的需求;另一個範例就是使用者可以上傳檔案的資料夾。</span><span class="sxs-lookup"><span data-stu-id="555bc-148">Excluding specific files or folders from deployment is a common requirement; another example would be a folder that users can upload files to.</span></span> <span data-ttu-id="555bc-149">您不想記錄檔，或上傳您的開發環境，可供部署到生產環境中所建立的檔案。</span><span class="sxs-lookup"><span data-stu-id="555bc-149">You don't want log files or uploaded files that were created in your development environment to be deployed to production.</span></span> <span data-ttu-id="555bc-150">如果您要將更新部署到生產環境，您不想要刪除在生產環境中存在的檔案，部署程序。</span><span class="sxs-lookup"><span data-stu-id="555bc-150">And if you are deploying an update to production you don't want the deployment process to delete files that exist in production.</span></span> <span data-ttu-id="555bc-151">（根據如何設定部署選項，如果檔案存在於目的地站台但未在來源站台部署時，Web Deploy 刪除它從目的地。）</span><span class="sxs-lookup"><span data-stu-id="555bc-151">(Depending on how you set a deployment option, if a file exists in the destination site but not the source site when you deploy, Web Deploy deletes it from the destination.)</span></span>

<span data-ttu-id="555bc-152">如稍早在本教學課程中，您所見**部署的項目**選項**封裝/發行 Web**索引標籤設定為**只需要執行此應用程式檔案**。</span><span class="sxs-lookup"><span data-stu-id="555bc-152">As you saw earlier in this tutorial, the **Items to deploy** option in the **Package/Publish Web** tab is set to **Only Files Needed to run this application**.</span></span> <span data-ttu-id="555bc-153">如此一來，在開發過程中建立的 Elmah 記錄檔將不會部署，這是您想要發生。</span><span class="sxs-lookup"><span data-stu-id="555bc-153">As a result, log files that are created by Elmah in development will not be deployed, which is what you want to happen.</span></span> <span data-ttu-id="555bc-154">(若要部署，它們必須包含在專案及其**建置動作**屬性必須設為**內容**。</span><span class="sxs-lookup"><span data-stu-id="555bc-154">(To be deployed, they would have to be included in the project and their **Build Action** property would have to be set to **Content**.</span></span> <span data-ttu-id="555bc-155">如需詳細資訊，請參閱 <<c0>  **為什麼不在我的專案資料夾中檔案的所有部署？** 中[ASP.NET Web 應用程式專案部署常見問題集](https://msdn.microsoft.com/library/ee942158.aspx))。</span><span class="sxs-lookup"><span data-stu-id="555bc-155">For more information, see **Why don't all of the files in my project folder get deployed?** in [ASP.NET Web Application Project Deployment FAQ](https://msdn.microsoft.com/library/ee942158.aspx)).</span></span> <span data-ttu-id="555bc-156">不過，Web Deploy 不會建立一個資料夾目的地站台中除非至少一個檔案複製到它。</span><span class="sxs-lookup"><span data-stu-id="555bc-156">However, Web Deploy will not create a folder in the destination site unless there's at least one file to copy to it.</span></span> <span data-ttu-id="555bc-157">因此，您會新增 *.txt*檔案到資料夾，以做為預留位置，以便將複製的資料夾。</span><span class="sxs-lookup"><span data-stu-id="555bc-157">Therefore, you'll add a *.txt* file to the folder to act as a placeholder so that the folder will be copied.</span></span>

<span data-ttu-id="555bc-158">在 [**方案總管] 中**，以滑鼠右鍵按一下*Elmah*資料夾中，選取**加入新項目**，並建立名為的檔案*Placeholder.txt*。</span><span class="sxs-lookup"><span data-stu-id="555bc-158">In **Solution Explorer**, right-click the *Elmah* folder, select **Add New Item**, and create a file named *Placeholder.txt*.</span></span> <span data-ttu-id="555bc-159">將下列文字放入它："This is 預留位置檔案，以確保取得部署資料夾"。</span><span class="sxs-lookup"><span data-stu-id="555bc-159">Put the following text in it: "This is a placeholder file to ensure that the folder gets deployed."</span></span> <span data-ttu-id="555bc-160">然後儲存檔案。</span><span class="sxs-lookup"><span data-stu-id="555bc-160">and save the file.</span></span> <span data-ttu-id="555bc-161">這就是您必須執行才能確定，Visual Studio 會部署這個檔案和資料夾，因為**建置動作**屬性 *.txt*檔案設定為**內容**預設。</span><span class="sxs-lookup"><span data-stu-id="555bc-161">That's all you have to do in order to make sure that Visual Studio deploys this file and the folder it's in, because the **Build Action** property of *.txt* files is set to **Content** by default.</span></span>

<span data-ttu-id="555bc-162">您現在已完成所有的部署設定工作。</span><span class="sxs-lookup"><span data-stu-id="555bc-162">You have now completed all of the deployment set-up tasks.</span></span> <span data-ttu-id="555bc-163">在下一個教學課程中，將 Contoso 大學網站部署到測試環境，並測試其存在。</span><span class="sxs-lookup"><span data-stu-id="555bc-163">In the next tutorial, you'll deploy the Contoso University site to the test environment and test it there.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="555bc-164">[上一頁](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="555bc-164">[Previous](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)</span></span>