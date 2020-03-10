---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署僅限程式碼的更新-8/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: ddf6252f-9413-4c0c-a360-2cef8d231717
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12
msc.type: authoredcontent
ms.openlocfilehash: e4d094ef84a747c36ce05ddb0e3d1ce0391d5605
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78564404"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-a-code-only-update---8-of-12"></a><span data-ttu-id="96dc2-103">使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署僅限程式碼的更新-8/12</span><span class="sxs-lookup"><span data-stu-id="96dc2-103">Deploying an ASP.NET Web Application with SQL Server Compact using Visual Studio or Visual Web Developer: Deploying a Code-Only Update - 8 of 12</span></span>

<span data-ttu-id="96dc2-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="96dc2-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="96dc2-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="96dc2-105">Download Starter Project</span></span>](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> <span data-ttu-id="96dc2-106">這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。</span><span class="sxs-lookup"><span data-stu-id="96dc2-106">This series of tutorials shows you how to deploy (publish) an ASP.NET web application project that includes a SQL Server Compact database by using Visual Studio 2012 RC or Visual Studio Express 2012 RC for Web.</span></span> <span data-ttu-id="96dc2-107">如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。</span><span class="sxs-lookup"><span data-stu-id="96dc2-107">You can also use Visual Studio 2010 if you install the Web Publish Update.</span></span> <span data-ttu-id="96dc2-108">如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。</span><span class="sxs-lookup"><span data-stu-id="96dc2-108">For an introduction to the series, see [the first tutorial in the series](deployment-to-a-hosting-provider-introduction-1-of-12.md).</span></span>
> 
> <span data-ttu-id="96dc2-109">如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。</span><span class="sxs-lookup"><span data-stu-id="96dc2-109">For a tutorial that shows deployment features introduced after the RC release of Visual Studio 2012, shows how to deploy SQL Server editions other than SQL Server Compact, and shows how to deploy to Azure App Service Web Apps, see [ASP.NET Web Deployment using Visual Studio](../../deployment/visual-studio-web-deployment/introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="96dc2-110">概觀</span><span class="sxs-lookup"><span data-stu-id="96dc2-110">Overview</span></span>

<span data-ttu-id="96dc2-111">在初始部署之後，您維護和開發網站的工作會繼續進行，而且在很久之前，您會想要部署更新。</span><span class="sxs-lookup"><span data-stu-id="96dc2-111">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="96dc2-112">本教學課程會引導您完成將更新部署至應用程式程式碼的流程。</span><span class="sxs-lookup"><span data-stu-id="96dc2-112">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="96dc2-113">此更新不需要變更資料庫;在下一個教學課程中，您會看到部署資料庫變更的不同之處。</span><span class="sxs-lookup"><span data-stu-id="96dc2-113">This update does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="96dc2-114">提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。</span><span class="sxs-lookup"><span data-stu-id="96dc2-114">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md).</span></span>

## <a name="making-a-code-change"></a><span data-ttu-id="96dc2-115">進行程式碼變更</span><span class="sxs-lookup"><span data-stu-id="96dc2-115">Making a Code Change</span></span>

<span data-ttu-id="96dc2-116">做為應用程式更新的簡單範例，您會將所選講師所教授的課程清單新增到**講師**頁面。</span><span class="sxs-lookup"><span data-stu-id="96dc2-116">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="96dc2-117">如果您執行 [**講師**] 頁面，您會發現方格中有 [**選取**] 連結，但它們不會執行任何動作，而是讓資料列背景變成灰色。</span><span class="sxs-lookup"><span data-stu-id="96dc2-117">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

<span data-ttu-id="96dc2-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="96dc2-118">[![Instructors_page](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image1.png)</span></span>

<span data-ttu-id="96dc2-119">現在您將新增在按一下 [**選取**] 連結時執行的程式碼，並顯示所選講師所教授的課程清單。</span><span class="sxs-lookup"><span data-stu-id="96dc2-119">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

<span data-ttu-id="96dc2-120">在 [ **ErrorMessageLabel** ] `Label` 控制項之後，于 [ *.aspx*] 中立即新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="96dc2-120">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

[!code-aspx[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample1.aspx)]

<span data-ttu-id="96dc2-121">執行頁面，然後選取講師。</span><span class="sxs-lookup"><span data-stu-id="96dc2-121">Run the page and select an instructor.</span></span> <span data-ttu-id="96dc2-122">您會看到該講師所教授的課程清單。</span><span class="sxs-lookup"><span data-stu-id="96dc2-122">You see a list of courses taught by that instructor.</span></span>

<span data-ttu-id="96dc2-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span><span class="sxs-lookup"><span data-stu-id="96dc2-123">[![Instructors_page_with_courses](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image3.png)</span></span>

## <a name="deploying-the-code-update-to-the-test-environment"></a><span data-ttu-id="96dc2-124">將程式碼更新部署到測試環境</span><span class="sxs-lookup"><span data-stu-id="96dc2-124">Deploying the Code Update to the Test Environment</span></span>

<span data-ttu-id="96dc2-125">部署到測試環境是一種簡單的事，就是再次執行單鍵發行。</span><span class="sxs-lookup"><span data-stu-id="96dc2-125">Deploying to the test environment is a simple matter of running one-click publish again.</span></span> <span data-ttu-id="96dc2-126">若要讓此程式更快速，您可以使用 Web 單鍵 [**發行**] 工具列。</span><span class="sxs-lookup"><span data-stu-id="96dc2-126">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

<span data-ttu-id="96dc2-127">在 [ **View** ] 功能表中，選擇 [**工具列**]，然後選取 [ **Web One**] [發佈]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-127">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

![Selecting_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image5.png)

<span data-ttu-id="96dc2-129">在 **方案總管**中，選取 ContosoUniversity 專案。</span><span class="sxs-lookup"><span data-stu-id="96dc2-129">In **Solution Explorer**, select the ContosoUniversity project.</span></span>

<span data-ttu-id="96dc2-130">Web 單鍵 [**發行**] 工具列，選擇 [**測試**發行設定檔]，然後按一下 [**發佈 Web** ] （箭號向左和向右的圖示）。</span><span class="sxs-lookup"><span data-stu-id="96dc2-130">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

![Web_One_Click_Publish_toolbar](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image6.png)

<span data-ttu-id="96dc2-132">Visual Studio 會部署已更新的應用程式，且瀏覽器會自動開啟至首頁。</span><span class="sxs-lookup"><span data-stu-id="96dc2-132">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span> <span data-ttu-id="96dc2-133">執行 [講師] 頁面，然後選取講師以確認更新已成功部署。</span><span class="sxs-lookup"><span data-stu-id="96dc2-133">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="96dc2-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span><span class="sxs-lookup"><span data-stu-id="96dc2-134">[![Instructors_page_with_courses_Test](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image7.png)</span></span>

<span data-ttu-id="96dc2-135">您通常也會進行迴歸測試（也就是測試網站的其餘部分，以確保新的變更不會中斷任何現有的功能）。</span><span class="sxs-lookup"><span data-stu-id="96dc2-135">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="96dc2-136">但是在本教學課程中，您會略過該步驟，並繼續將更新部署至生產環境。</span><span class="sxs-lookup"><span data-stu-id="96dc2-136">But for this tutorial you'll skip that step and proceed to deploy the update to production.</span></span>

## <a name="preventing-redeployment-of-the-initial-database-state-to-production"></a><span data-ttu-id="96dc2-137">防止將初始資料庫狀態重新部署到生產環境</span><span class="sxs-lookup"><span data-stu-id="96dc2-137">Preventing Redeployment of the Initial Database State to Production</span></span>

<span data-ttu-id="96dc2-138">在實際的應用程式中，使用者會在初始部署之後與您的生產網站互動，並以即時資料填入資料庫。</span><span class="sxs-lookup"><span data-stu-id="96dc2-138">In a real application, users interact with your production site after your initial deployment, and the databases are populated with live data.</span></span> <span data-ttu-id="96dc2-139">因此，您不想要在初始狀態中重新部署成員資格資料庫，這會清除所有的即時資料。</span><span class="sxs-lookup"><span data-stu-id="96dc2-139">Therefore, you don't want to redeploy the membership database in its initial state, which would wipe out all of the live data.</span></span> <span data-ttu-id="96dc2-140">因為 SQL Server Compact 的資料庫是*應用程式\_* 資料夾中的檔案，所以您必須藉由變更部署設定來避免此情況，讓 *\_應用程式*中的檔案不會部署。</span><span class="sxs-lookup"><span data-stu-id="96dc2-140">Since SQL Server Compact databases are files in the *App\_Data* folder, you have to prevent this by changing deployment settings so that files in the *App\_Data* folder aren't deployed.</span></span>

<span data-ttu-id="96dc2-141">開啟 ContosoUniversity 專案的 [**專案屬性**] 視窗，然後選取 [**封裝/發行 Web** ] 索引標籤。請確定 [設定 **] 下拉式方塊已選取 [作用**中 **（發行）** ] 或 [**發行**]，然後選取 **[從應用程式\_資料夾中排除**檔案]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-141">Open the **Project Properties** window for the ContosoUniversity project, and select the **Package/Publish Web** tab. Make sure that the **Configuration** drop-down box has either **Active (Release)** or **Release** selected, select **Exclude files from the App\_Data folder**.</span></span>

![Exclude_files_from_the_App_Data_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image9.png)

<span data-ttu-id="96dc2-143">如果您決定要在未來部署「偵錯工具」組建，建議您對「偵錯工具」組建設定進行相同的變更 **：將設定變更為**「 **debug** 」，然後選取 **[從 App\_資料夾中排除**檔案]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-143">In case you decide to deploy a debug build in the future, it's a good idea to make the same change for the Debug build configuration: change **Configuration** to **Debug** and then select **Exclude files from the App\_Data folder**.</span></span>

<span data-ttu-id="96dc2-144">儲存並關閉 [**封裝/發行 Web** ] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="96dc2-144">Save and close the **Package/Publish Web** tab.</span></span>

> [!NOTE] 
> 
> [!IMPORTANT]
> <span data-ttu-id="96dc2-145">請確定您未在發行設定檔中選取 [**在目的地移除其他**檔案]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-145">Make sure that you don't have **Remove additional files at destination** selected in your publish profiles.</span></span> <span data-ttu-id="96dc2-146">如果您選取該選項，部署程式將會刪除部署的網站中您在 App\_資料中的資料庫，而它將會刪除應用程式\_資料檔案夾本身。</span><span class="sxs-lookup"><span data-stu-id="96dc2-146">If you select that option, the deployment process will delete the databases that you have in App\_Data in the deployed site, and it will delete the App\_Data folder itself.</span></span>

## <a name="preventing-user-access-to-the-production-site-during-update"></a><span data-ttu-id="96dc2-147">在更新期間防止使用者存取生產網站</span><span class="sxs-lookup"><span data-stu-id="96dc2-147">Preventing User Access to the Production Site During Update</span></span>

<span data-ttu-id="96dc2-148">您要部署的變更現在是單一頁面的簡單變更。</span><span class="sxs-lookup"><span data-stu-id="96dc2-148">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="96dc2-149">但有時候您會部署較大的變更，在這種情況下，如果使用者在部署完成之前要求頁面，則網站的行為可能會奇怪。</span><span class="sxs-lookup"><span data-stu-id="96dc2-149">But sometimes you deploy larger changes, and in that case the site can behave strangely if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="96dc2-150">若要避免這種情況，您可以使用*應用程式\_離線 .htm*檔案。</span><span class="sxs-lookup"><span data-stu-id="96dc2-150">To prevent this, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="96dc2-151">當您在應用程式的根資料夾中，將名為 app 的檔案 *\_離線*時，IIS 會自動顯示該檔案，而不是執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="96dc2-151">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="96dc2-152">因此，若要在部署期間防止存取，請將*應用程式\_離線 .htm* ，執行部署程式，然後移除 *\_離線的應用程式*。</span><span class="sxs-lookup"><span data-stu-id="96dc2-152">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm*.</span></span>

<span data-ttu-id="96dc2-153">在**方案總管**中，以滑鼠右鍵按一下方案（不是其中一個專案），然後選取 [**新增方案資料夾**]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-153">In **Solution Explorer**, right-click the solution (not one of the projects) and select **New Solution Folder**.</span></span>

![Creating_a_solution_folder](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image10.png)

<span data-ttu-id="96dc2-155">將資料夾命名為*SolutionFiles*。</span><span class="sxs-lookup"><span data-stu-id="96dc2-155">Name the folder *SolutionFiles*.</span></span>

<span data-ttu-id="96dc2-156">在新資料夾中，建立名為*app\_離線*的 HTML 網頁。</span><span class="sxs-lookup"><span data-stu-id="96dc2-156">In the new folder create an HTML page named *app\_offline.htm*.</span></span> <span data-ttu-id="96dc2-157">以下列標記取代現有的內容：</span><span class="sxs-lookup"><span data-stu-id="96dc2-157">Replace the existing contents with the following markup:</span></span>

[!code-html[Main](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/samples/sample2.html)]

<span data-ttu-id="96dc2-158">您可以在主控提供者的控制台中，使用 FTP 連接或**檔案管理員**公用程式，將*應用程式\_離線 .htm*檔案複製到網站。</span><span class="sxs-lookup"><span data-stu-id="96dc2-158">You can copy the *app\_offline.htm* file to the site by using an FTP connection or the **File Manager** utility in the hosting provider's control panel.</span></span> <span data-ttu-id="96dc2-159">在本教學課程中，您將使用 [**檔案管理員**]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-159">For this tutorial, you'll use the **File Manager**.</span></span>

<span data-ttu-id="96dc2-160">開啟 [控制台]，然後選取 [**檔案管理員**]，如同您在[部署至生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中所做的一樣。</span><span class="sxs-lookup"><span data-stu-id="96dc2-160">Open the control panel and select **File Manager** as you did in the [Deploying to the Production Environment](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md) tutorial.</span></span> <span data-ttu-id="96dc2-161">選取 [ **contosouniversity.com** ]，然後選取 [ **wwwroot** ] 以前往應用程式的根資料夾，然後按一下 **[上傳**]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-161">Select **contosouniversity.com** and then **wwwroot** to get to your application's root folder, and then click **Upload**.</span></span>

<span data-ttu-id="96dc2-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span><span class="sxs-lookup"><span data-stu-id="96dc2-162">[![Upload_button_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image11.png)</span></span>

<span data-ttu-id="96dc2-163">在 [**上傳**檔案] 對話方塊中，選取 *\_離線 .htm 檔案的應用程式*，然後按一下 **[上傳**]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-163">In the **Upload File** dialog box, select the *app\_offline.htm* file and then click **Upload**.</span></span>

<span data-ttu-id="96dc2-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span><span class="sxs-lookup"><span data-stu-id="96dc2-164">[![Upload_dialog_box_in_File_Manager](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image13.png)</span></span>

<span data-ttu-id="96dc2-165">瀏覽至網站的 URL。</span><span class="sxs-lookup"><span data-stu-id="96dc2-165">Browse to your site's URL.</span></span> <span data-ttu-id="96dc2-166">您會看到*應用程式\_離線 .htm*  頁面，而不是您的首頁。</span><span class="sxs-lookup"><span data-stu-id="96dc2-166">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

<span data-ttu-id="96dc2-167">[![App_offline。 htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span><span class="sxs-lookup"><span data-stu-id="96dc2-167">[![App_offline.htm_page_in_production](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image15.png)</span></span>

<span data-ttu-id="96dc2-168">您現在已準備好部署到生產環境。</span><span class="sxs-lookup"><span data-stu-id="96dc2-168">You are now ready to deploy to production.</span></span>

## <a name="deploying-the-code-update-to-the-production-environment"></a><span data-ttu-id="96dc2-169">將程式碼更新部署至生產環境</span><span class="sxs-lookup"><span data-stu-id="96dc2-169">Deploying the Code Update to the Production Environment</span></span>

<span data-ttu-id="96dc2-170">在 Web 單鍵的 [**發行**] 工具列中，選擇 [**生產**] 發行設定檔，然後按一下 [**發佈 Web**]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-170">In the **Web One Click Publish** toolbar, choose the **Production** publish profile and then click **Publish Web**.</span></span>

<span data-ttu-id="96dc2-171">Visual Studio 會部署已更新的應用程式，並將瀏覽器開啟至網站的首頁。</span><span class="sxs-lookup"><span data-stu-id="96dc2-171">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="96dc2-172">隨即顯示*應用程式\_離線的 .htm*檔案。</span><span class="sxs-lookup"><span data-stu-id="96dc2-172">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="96dc2-173">您必須先移除*應用程式\_離線 .htm*檔案，才能進行測試以確認部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="96dc2-173">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>

<span data-ttu-id="96dc2-174">回到 [控制台] 中的 [**檔案管理員**] 應用程式。</span><span class="sxs-lookup"><span data-stu-id="96dc2-174">Return to the **File Manager** application in the control panel.</span></span> <span data-ttu-id="96dc2-175">選取 [ **contosouniversity.com** ] 和 [ **wwwroot**]，選取 [**應用程式\_離線**]，然後按一下 [**刪除**]。</span><span class="sxs-lookup"><span data-stu-id="96dc2-175">Select **contosouniversity.com** and **wwwroot**, select **app\_offline.htm**, and then click **Delete**.</span></span>

<span data-ttu-id="96dc2-176">[![Deleting_app_offline .htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span><span class="sxs-lookup"><span data-stu-id="96dc2-176">[![Deleting_app_offline.htm](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image17.png)</span></span>

<span data-ttu-id="96dc2-177">在瀏覽器中，開啟公用網站中的 [講師] 頁面，然後選取講師以確認更新已成功部署。</span><span class="sxs-lookup"><span data-stu-id="96dc2-177">In the browser, open the Instructors page in the public site, and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="96dc2-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span><span class="sxs-lookup"><span data-stu-id="96dc2-178">[![Instructors_page_with_courses_Prod](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12/_static/image19.png)</span></span>

<span data-ttu-id="96dc2-179">您現在已部署未牽涉到資料庫變更的應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="96dc2-179">You've now deployed an application update that did not involve a database change.</span></span> <span data-ttu-id="96dc2-180">下一個教學課程會說明如何部署資料庫變更。</span><span class="sxs-lookup"><span data-stu-id="96dc2-180">The next tutorial shows you how to deploy a database change.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="96dc2-181">[上一頁](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span><span class="sxs-lookup"><span data-stu-id="96dc2-181">[Previous](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)
[Next](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)</span></span>
