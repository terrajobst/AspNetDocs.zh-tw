---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
title: 使用 Visual Studio ASP.NET Web 部署：部署程式碼更新 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: c76dbc35-a914-4ee3-919c-4f4d1fa05104
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update
msc.type: authoredcontent
ms.openlocfilehash: 3881833bfe2a50a38a357614f92f434a04a8ab08
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78567400"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-a-code-update"></a><span data-ttu-id="64bad-103">使用 Visual Studio ASP.NET Web 部署：部署程式碼更新</span><span class="sxs-lookup"><span data-stu-id="64bad-103">ASP.NET Web Deployment using Visual Studio: Deploying a Code Update</span></span>

<span data-ttu-id="64bad-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="64bad-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="64bad-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="64bad-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="64bad-106">本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。</span><span class="sxs-lookup"><span data-stu-id="64bad-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="64bad-107">如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。</span><span class="sxs-lookup"><span data-stu-id="64bad-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="64bad-108">概觀</span><span class="sxs-lookup"><span data-stu-id="64bad-108">Overview</span></span>

<span data-ttu-id="64bad-109">在初始部署之後，您維護和開發網站的工作會繼續進行，而且在很久之前，您會想要部署更新。</span><span class="sxs-lookup"><span data-stu-id="64bad-109">After the initial deployment, your work of maintaining and developing your web site continues, and before long you will want to deploy an update.</span></span> <span data-ttu-id="64bad-110">本教學課程會引導您完成將更新部署至應用程式程式碼的流程。</span><span class="sxs-lookup"><span data-stu-id="64bad-110">This tutorial takes you through the process of deploying an update to your application code.</span></span> <span data-ttu-id="64bad-111">您在本教學課程中執行及部署的更新不會牽涉到資料庫變更;在下一個教學課程中，您會看到部署資料庫變更的不同之處。</span><span class="sxs-lookup"><span data-stu-id="64bad-111">The update that you implement and deploy in this tutorial does not involve a database change; you'll see what's different about deploying a database change in the next tutorial.</span></span>

<span data-ttu-id="64bad-112">提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。</span><span class="sxs-lookup"><span data-stu-id="64bad-112">Reminder: If you get an error message or something doesn't work as you go through the tutorial, be sure to check the [troubleshooting page](troubleshooting.md).</span></span>

## <a name="make-a-code-change"></a><span data-ttu-id="64bad-113">進行程式碼變更</span><span class="sxs-lookup"><span data-stu-id="64bad-113">Make a code change</span></span>

<span data-ttu-id="64bad-114">做為應用程式更新的簡單範例，您會將所選講師所教授的課程清單新增到**講師**頁面。</span><span class="sxs-lookup"><span data-stu-id="64bad-114">As a simple example of an update to your application, you'll add to the **Instructors** page a list of courses taught by the selected instructor.</span></span>

<span data-ttu-id="64bad-115">如果您執行 [**講師**] 頁面，您會發現方格中有 [**選取**] 連結，但它們不會執行任何動作，而是讓資料列背景變成灰色。</span><span class="sxs-lookup"><span data-stu-id="64bad-115">If you run the **Instructors** page, you'll notice that there are **Select** links in the grid, but they don't do anything other than make the row background turn gray.</span></span>

![具有選取專案的講師頁面](deploying-a-code-update/_static/image1.png)

<span data-ttu-id="64bad-117">現在您將新增在按一下 [**選取**] 連結時執行的程式碼，並顯示所選講師所教授的課程清單。</span><span class="sxs-lookup"><span data-stu-id="64bad-117">Now you'll add code that runs when the **Select** link is clicked and displays a list of courses taught by the selected instructor .</span></span>

1. <span data-ttu-id="64bad-118">在 [ **ErrorMessageLabel** ] `Label` 控制項之後，于 [ *.aspx*] 中立即新增下列標記：</span><span class="sxs-lookup"><span data-stu-id="64bad-118">In *Instructors.aspx*, add the following markup immediately after the **ErrorMessageLabel** `Label` control:</span></span>

    [!code-aspx[Main](deploying-a-code-update/samples/sample1.aspx)]
2. <span data-ttu-id="64bad-119">執行頁面，然後選取講師。</span><span class="sxs-lookup"><span data-stu-id="64bad-119">Run the page and select an instructor.</span></span> <span data-ttu-id="64bad-120">您會看到該講師所教授的課程清單。</span><span class="sxs-lookup"><span data-stu-id="64bad-120">You see a list of courses taught by that instructor.</span></span>

    ![講師頁面包含教授的課程](deploying-a-code-update/_static/image2.png)
3. <span data-ttu-id="64bad-122">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="64bad-122">Close the browser.</span></span>

## <a name="deploy-the-code-update-to-the-test-environment"></a><span data-ttu-id="64bad-123">將程式碼更新部署到測試環境</span><span class="sxs-lookup"><span data-stu-id="64bad-123">Deploy the code update to the test environment</span></span>

<span data-ttu-id="64bad-124">在您可以使用發行設定檔部署到測試、預備和生產環境之前，您需要變更資料庫發行選項。</span><span class="sxs-lookup"><span data-stu-id="64bad-124">Before you can use your publish profiles to deploy to test, staging, and production, you need to change database publishing options.</span></span> <span data-ttu-id="64bad-125">您不再需要執行成員資格資料庫的授與和資料部署腳本。</span><span class="sxs-lookup"><span data-stu-id="64bad-125">You no longer need to run the grant and data deployment scripts for the membership database.</span></span>

1. <span data-ttu-id="64bad-126">以滑鼠右鍵按一下 [ContosoUniversity] 專案，然後按一下 [**發佈**]，以開啟 [**發佈 Web** wizard]。</span><span class="sxs-lookup"><span data-stu-id="64bad-126">Open the **Publish Web** wizard by right-clicking the ContosoUniversity project and clicking **Publish**.</span></span>
2. <span data-ttu-id="64bad-127">按一下 [**配置**檔] 下拉式清單中的**測試**設定檔。</span><span class="sxs-lookup"><span data-stu-id="64bad-127">Click the **Test** profile in the **Profile** drop-down list.</span></span>
3. <span data-ttu-id="64bad-128">按一下 [設定] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="64bad-128">Click the **Settings** tab.</span></span>
4. <span data-ttu-id="64bad-129">在 [**資料庫**] 區段的 [ **DefaultConnection** ] 下，清除 [**更新資料庫**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="64bad-129">Under **DefaultConnection** in the **Databases** section, clear the **Update database** check box.</span></span>
5. <span data-ttu-id="64bad-130">按一下 [**設定檔**] 索引標籤，然後按一下 [**配置**檔] 下拉式清單中的**暫存**設定檔。</span><span class="sxs-lookup"><span data-stu-id="64bad-130">Click the **Profile** tab, and then click the **Staging** profile in the **Profile** drop-down list.</span></span>
6. <span data-ttu-id="64bad-131">當系統詢問您是否要儲存對**測試**設定檔所做的變更時，請按一下 **[是]** 。</span><span class="sxs-lookup"><span data-stu-id="64bad-131">When you are asked if you want to save the changes made to the **Test** profile, click **Yes**.</span></span>
7. <span data-ttu-id="64bad-132">在暫存設定檔中進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="64bad-132">Make the same change in the Staging profile.</span></span>
8. <span data-ttu-id="64bad-133">重複此程式，在生產設定檔中進行相同的變更。</span><span class="sxs-lookup"><span data-stu-id="64bad-133">Repeat the process to make the same change in the Production profile.</span></span>
9. <span data-ttu-id="64bad-134">關閉 [**發行 Web** wizard]。</span><span class="sxs-lookup"><span data-stu-id="64bad-134">Close the **Publish Web** wizard.</span></span>

<span data-ttu-id="64bad-135">部署到測試環境現在很簡單，只要執行一次 [發佈] 即可。</span><span class="sxs-lookup"><span data-stu-id="64bad-135">Deploying to the test environment is now a simple matter of running one-click publish again.</span></span> <span data-ttu-id="64bad-136">若要讓此程式更快速，您可以使用 Web 單鍵 [**發行**] 工具列。</span><span class="sxs-lookup"><span data-stu-id="64bad-136">To make this process quicker, you can use the **Web One Click Publish** toolbar.</span></span>

1. <span data-ttu-id="64bad-137">在 [ **View** ] 功能表中，選擇 [**工具列**]，然後選取 [ **Web One**] [發佈]。</span><span class="sxs-lookup"><span data-stu-id="64bad-137">In the **View** menu, choose **Toolbars** and then select **Web One Click Publish**.</span></span>

    ![Selecting_One_Click_Publish_toolbar](deploying-a-code-update/_static/image3.png)
2. <span data-ttu-id="64bad-139">在 **方案總管**中，選取 ContosoUniversity 專案。</span><span class="sxs-lookup"><span data-stu-id="64bad-139">In **Solution Explorer**, select the ContosoUniversity project.</span></span>
3. <span data-ttu-id="64bad-140">Web 單鍵 [**發行**] 工具列，選擇 [**測試**發行設定檔]，然後按一下 [**發佈 Web** ] （箭號向左和向右的圖示）。</span><span class="sxs-lookup"><span data-stu-id="64bad-140">the **Web One Click Publish** toolbar, choose the **Test** publish profile and then click **Publish Web** (the icon with arrows pointing left and right).</span></span>

    ![Web_One_Click_Publish_toolbar](deploying-a-code-update/_static/image4.png)
4. <span data-ttu-id="64bad-142">Visual Studio 會部署已更新的應用程式，且瀏覽器會自動開啟至首頁。</span><span class="sxs-lookup"><span data-stu-id="64bad-142">Visual Studio deploys the updated application, and the browser automatically opens to the home page.</span></span>
5. <span data-ttu-id="64bad-143">執行 [講師] 頁面，然後選取講師以確認更新已成功部署。</span><span class="sxs-lookup"><span data-stu-id="64bad-143">Run the Instructors page and select an instructor to verify that the update was successfully deployed.</span></span>

<span data-ttu-id="64bad-144">您通常也會進行迴歸測試（也就是測試網站的其餘部分，以確保新的變更不會中斷任何現有的功能）。</span><span class="sxs-lookup"><span data-stu-id="64bad-144">You would normally also do regression testing (that is, test the rest of the site to make sure that the new change didn't break any existing functionality).</span></span> <span data-ttu-id="64bad-145">但是在本教學課程中，您會略過該步驟，並繼續將更新部署至預備和生產環境。</span><span class="sxs-lookup"><span data-stu-id="64bad-145">But for this tutorial you'll skip that step and proceed to deploy the update to staging and production.</span></span>

<span data-ttu-id="64bad-146">當您重新部署時，Web Deploy 會自動判斷哪些檔案已變更，而且只會將已變更的檔案複製到伺服器。</span><span class="sxs-lookup"><span data-stu-id="64bad-146">When you redeploy, Web Deploy automatically determines which files have changed and only copies changed files to the server.</span></span> <span data-ttu-id="64bad-147">根據預設，Web Deploy 會在檔案上使用上次變更的日期，以判斷哪些檔案已變更。</span><span class="sxs-lookup"><span data-stu-id="64bad-147">By default, Web Deploy uses last-changed dates on files to determine which ones have changed.</span></span> <span data-ttu-id="64bad-148">某些原始檔控制系統會變更檔案的日期，即使您未變更檔案內容也一樣。</span><span class="sxs-lookup"><span data-stu-id="64bad-148">Some source control systems change file dates even when you don't change the file contents.</span></span> <span data-ttu-id="64bad-149">在這種情況下，您可能會想要設定 Web Deploy 使用檔案總和檢查碼來判斷哪些檔案已變更。</span><span class="sxs-lookup"><span data-stu-id="64bad-149">In that case, you might want to configure Web Deploy to use file checksums to determine which files have changed.</span></span> <span data-ttu-id="64bad-150">如需詳細資訊，請參閱 ASP.NET 部署常見問題中的[為何所有檔案都已重新部署，但我並未變更它們？](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) 。</span><span class="sxs-lookup"><span data-stu-id="64bad-150">For more information, see [Why do all of my files get redeployed although I didn't change them?](https://msdn.microsoft.com/library/ee942158.aspx#use_checksum) in the ASP.NET Deployment FAQ.</span></span>

## <a name="take-the-application-offline-during-deployment"></a><span data-ttu-id="64bad-151">在部署期間讓應用程式離線</span><span class="sxs-lookup"><span data-stu-id="64bad-151">Take the application offline during deployment</span></span>

<span data-ttu-id="64bad-152">您要部署的變更現在是單一頁面的簡單變更。</span><span class="sxs-lookup"><span data-stu-id="64bad-152">The change you're deploying now is a simple change to a single page.</span></span> <span data-ttu-id="64bad-153">但有時候您會部署較大的變更，或部署程式碼和資料庫變更，而且如果使用者在部署完成之前要求頁面，網站可能會不正確地運作。</span><span class="sxs-lookup"><span data-stu-id="64bad-153">But sometimes you deploy larger changes, or you deploy both code and database changes, and the site might behave incorrectly if a user requests a page before deployment is finished.</span></span> <span data-ttu-id="64bad-154">若要防止使用者在部署進行時存取網站，您可以使用*應用程式\_離線 .htm*檔案。</span><span class="sxs-lookup"><span data-stu-id="64bad-154">To prevent users from accessing the site while deployment is in progress, you can use an *app\_offline.htm* file.</span></span> <span data-ttu-id="64bad-155">當您在應用程式的根資料夾中，將名為 app 的檔案 *\_離線*時，IIS 會自動顯示該檔案，而不是執行您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="64bad-155">When you put a file named *app\_offline.htm* in the root folder of your application, IIS automatically displays that file instead of running your application.</span></span> <span data-ttu-id="64bad-156">因此，若要在部署期間防止存取，您可以將*應用程式\_離線的 .htm* ，執行部署程式，然後在部署成功之後，將*應用程式\_離線。*</span><span class="sxs-lookup"><span data-stu-id="64bad-156">So to prevent access during deployment, you put *app\_offline.htm* in the root folder, run the deployment process, and then remove *app\_offline.htm* after successful deployment.</span></span>

<span data-ttu-id="64bad-157">您可以設定 Web Deploy 自動將預設*應用\_程式*放在伺服器上的離線 .htm 檔案中，然後在完成時將其移除。</span><span class="sxs-lookup"><span data-stu-id="64bad-157">You can configure Web Deploy to automatically put a default *app\_offline.htm* file on the server when it starts deploying and remove it when it finishes.</span></span> <span data-ttu-id="64bad-158">若要這麼做，您只需要將下列 XML 元素新增至您的發行設定檔（. .pubxml）檔案：</span><span class="sxs-lookup"><span data-stu-id="64bad-158">To do that all you have to do is add the following XML element to your publish profile (.pubxml) file:</span></span>

[!code-xml[Main](deploying-a-code-update/samples/sample2.xml)]

<span data-ttu-id="64bad-159">在本教學課程中，您將瞭解如何建立及使用自訂*應用程式\_離線 .htm*檔案。</span><span class="sxs-lookup"><span data-stu-id="64bad-159">For this tutorial you'll see how to create and use a custom *app\_offline.htm* file.</span></span>

<span data-ttu-id="64bad-160">不需要在預備網站中使用*應用程式\_離線*，因為您沒有存取暫存網站的使用者。</span><span class="sxs-lookup"><span data-stu-id="64bad-160">Using *app\_offline.htm* in the staging site isn't required, because you don't have users accessing the staging site.</span></span> <span data-ttu-id="64bad-161">但最好是使用預備環境，以您計畫在生產環境中部署的方式來測試所有專案。</span><span class="sxs-lookup"><span data-stu-id="64bad-161">But it's a good practice to use staging to test everything the way you plan to deploy in production.</span></span>

### <a name="create-app_offlinehtm"></a><span data-ttu-id="64bad-162">建立離線應用程式\_.htm</span><span class="sxs-lookup"><span data-stu-id="64bad-162">Create app\_offline.htm</span></span>

1. <span data-ttu-id="64bad-163">在**方案總管**中，以滑鼠右鍵按一下方案，然後按一下 [**加入**]，再按一下 [**新增專案**]。</span><span class="sxs-lookup"><span data-stu-id="64bad-163">In **Solution Explorer**, right-click the solution and click **Add**, and then click **New Item**.</span></span>
2. <span data-ttu-id="64bad-164">建立名為*應用程式\_離線*的**html 網頁**（在 Visual Studio 預設建立的 *.html*副檔名中刪除最後的 "l"）。</span><span class="sxs-lookup"><span data-stu-id="64bad-164">Create an **HTML Page** named *app\_offline.htm* (delete the final "l" in the *.html* extension that Visual Studio creates by default).</span></span>
3. <span data-ttu-id="64bad-165">將範本標記取代為下列標記：</span><span class="sxs-lookup"><span data-stu-id="64bad-165">Replace the template markup with the following markup:</span></span>

    [!code-html[Main](deploying-a-code-update/samples/sample3.html)]
4. <span data-ttu-id="64bad-166">儲存並關閉檔案。</span><span class="sxs-lookup"><span data-stu-id="64bad-166">Save and close the file.</span></span>

### <a name="copy-app_offlinehtm-to-the-root-folder-of-the-web-site"></a><span data-ttu-id="64bad-167">將應用程式\_離線複製到網站的根資料夾</span><span class="sxs-lookup"><span data-stu-id="64bad-167">Copy app\_offline.htm to the root folder of the web site</span></span>

<span data-ttu-id="64bad-168">您可以使用任何 FTP 工具將檔案複製到網站。</span><span class="sxs-lookup"><span data-stu-id="64bad-168">You can use any FTP tool to copy files to the web site.</span></span> <span data-ttu-id="64bad-169">[FileZilla](http://filezilla-project.org/)是常用的 FTP 工具，會顯示在螢幕擷取畫面中。</span><span class="sxs-lookup"><span data-stu-id="64bad-169">[FileZilla](http://filezilla-project.org/) is a popular FTP tool and is shown in the screen shots.</span></span>

<span data-ttu-id="64bad-170">若要使用 FTP 工具，您需要三個專案： FTP URL、使用者名稱和密碼。</span><span class="sxs-lookup"><span data-stu-id="64bad-170">To use an FTP tool, you need three things: the FTP URL, the user name, and the password.</span></span>

<span data-ttu-id="64bad-171">URL 會顯示在 Azure 管理入口網站中網站的 [儀表板] 頁面上，而 FTP 的 [使用者名稱] 和 [密碼] 可在您稍早下載的 *.publishsettings*檔案中找到。</span><span class="sxs-lookup"><span data-stu-id="64bad-171">The URL is shown on the web site's dashboard page in the Azure Management Portal, and the user name and password for FTP can be found in the *.publishsettings* file that you downloaded earlier.</span></span> <span data-ttu-id="64bad-172">下列步驟顯示如何取得這些值。</span><span class="sxs-lookup"><span data-stu-id="64bad-172">The following steps show how to get these values.</span></span>

1. <span data-ttu-id="64bad-173">在 Azure 管理入口網站中，按一下 [**網站**] 索引標籤，然後按一下暫存網站。</span><span class="sxs-lookup"><span data-stu-id="64bad-173">In the Azure Management Portal, click **Web Sites** tab and then click the staging web site.</span></span>
2. <span data-ttu-id="64bad-174">在 [**儀表板**] 頁面上，向下流覽至 [**快速概覽**] 區段中的 [FTP 主機名稱]。</span><span class="sxs-lookup"><span data-stu-id="64bad-174">On the **Dashboard** page, scroll down to find the FTP host name in the **Quick Glance** section.</span></span>

    ![FTP 主機名稱](deploying-a-code-update/_static/image5.png)
3. <span data-ttu-id="64bad-176">在 [記事本] 或其他文字編輯器中開啟 *.publishsettings*檔案。</span><span class="sxs-lookup"><span data-stu-id="64bad-176">Open the staging *.publishsettings* file in Notepad or another text editor.</span></span>
4. <span data-ttu-id="64bad-177">尋找 FTP 設定檔的 `publishProfile` 元素。</span><span class="sxs-lookup"><span data-stu-id="64bad-177">Find the `publishProfile` element for the FTP profile.</span></span>
5. <span data-ttu-id="64bad-178">複製 `userName` 和 `userPWD` 值。</span><span class="sxs-lookup"><span data-stu-id="64bad-178">Copy the `userName` and `userPWD` values.</span></span>

    ![FTP 認證](deploying-a-code-update/_static/image6.png)
6. <span data-ttu-id="64bad-180">開啟您的 FTP 工具並登入 FTP URL。</span><span class="sxs-lookup"><span data-stu-id="64bad-180">Open your FTP tool and log on to the FTP URL.</span></span>
7. <span data-ttu-id="64bad-181">將*應用程式\_離線*，從 [方案] 資料夾複製到預備網站中的 [ */site/wwwroot* ] 資料夾。</span><span class="sxs-lookup"><span data-stu-id="64bad-181">Copy *app\_offline.htm* from the solution folder to the */site/wwwroot* folder in the staging site.</span></span>

    ![複製 app_offline](deploying-a-code-update/_static/image7.png)
8. <span data-ttu-id="64bad-183">流覽至您的預備網站 URL。</span><span class="sxs-lookup"><span data-stu-id="64bad-183">Browse to your staging site's URL.</span></span> <span data-ttu-id="64bad-184">您會看到*應用程式\_離線 .htm*  頁面，而不是您的首頁。</span><span class="sxs-lookup"><span data-stu-id="64bad-184">You see that the *app\_offline.htm* page is now displayed instead of your home page.</span></span>

    ![瀏覽器視窗中的 app_offline .htm](deploying-a-code-update/_static/image8.png)

<span data-ttu-id="64bad-186">您現在已準備好部署至預備環境。</span><span class="sxs-lookup"><span data-stu-id="64bad-186">You are now ready to deploy to staging.</span></span>

## <a name="deploy-the-code-update-to-staging-and-production"></a><span data-ttu-id="64bad-187">將程式碼更新部署至預備和生產環境</span><span class="sxs-lookup"><span data-stu-id="64bad-187">Deploy the code update to staging and production</span></span>

1. <span data-ttu-id="64bad-188">在 Web 單鍵的 [**發行**] 工具列中，選擇**預備**發行設定檔，然後按一下 [**發佈 Web**]。</span><span class="sxs-lookup"><span data-stu-id="64bad-188">In the **Web One Click Publish** toolbar, choose the **Staging** publish profile and then click **Publish Web**.</span></span>

    <span data-ttu-id="64bad-189">Visual Studio 會部署已更新的應用程式，並將瀏覽器開啟至網站的首頁。</span><span class="sxs-lookup"><span data-stu-id="64bad-189">Visual Studio deploys the updated application and opens the browser to the site's home page.</span></span> <span data-ttu-id="64bad-190">隨即顯示*應用程式\_離線的 .htm*檔案。</span><span class="sxs-lookup"><span data-stu-id="64bad-190">The *app\_offline.htm* file is displayed.</span></span> <span data-ttu-id="64bad-191">您必須先移除*應用程式\_離線 .htm*檔案，才能進行測試以確認部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="64bad-191">Before you can test to verify successful deployment, you must remove the *app\_offline.htm* file.</span></span>
2. <span data-ttu-id="64bad-192">返回您的 FTP 工具，並從預備網站刪除**應用程式\_離線 .htm** 。</span><span class="sxs-lookup"><span data-stu-id="64bad-192">Return to your FTP tool, and delete **app\_offline.htm** from the staging site.</span></span>
3. <span data-ttu-id="64bad-193">在瀏覽器中，開啟預備網站中的 [講師] 頁面，然後選取講師以確認更新已成功部署。</span><span class="sxs-lookup"><span data-stu-id="64bad-193">In the browser, open the Instructors page in the staging site, and select an instructor to verify that the update was successfully deployed.</span></span>
4. <span data-ttu-id="64bad-194">依照您針對預備環境所做的相同程式進行操作。</span><span class="sxs-lookup"><span data-stu-id="64bad-194">Follow the same procedure for production as you did for staging.</span></span>

<a id="specificfiles"></a>

## <a name="reviewing-changes-and-deploying-specific-files"></a><span data-ttu-id="64bad-195">檢查變更和部署特定檔案</span><span class="sxs-lookup"><span data-stu-id="64bad-195">Reviewing Changes and Deploying Specific Files</span></span>

<span data-ttu-id="64bad-196">Visual Studio 2012 也讓您能夠部署個別檔案。</span><span class="sxs-lookup"><span data-stu-id="64bad-196">Visual Studio 2012 also gives you the ability to deploy individual files.</span></span> <span data-ttu-id="64bad-197">針對選取的檔案，您可以查看本機版本與已部署版本之間的差異、將檔案部署到目的地環境，或將檔案從目的地環境複製到本機專案。</span><span class="sxs-lookup"><span data-stu-id="64bad-197">For a selected file you can view differences between the local version and the deployed version, deploy the file to the destination environment, or copy the file from the destination environment to the local project.</span></span> <span data-ttu-id="64bad-198">在本教學課程的這一節中，您會瞭解如何使用這些功能。</span><span class="sxs-lookup"><span data-stu-id="64bad-198">In this section of the tutorial you see how to use these features.</span></span>

### <a name="make-a-change-to-deploy"></a><span data-ttu-id="64bad-199">進行部署的變更</span><span class="sxs-lookup"><span data-stu-id="64bad-199">Make a change to deploy</span></span>

1. <span data-ttu-id="64bad-200">開啟*Content/.css*，然後尋找 `body` 標記的區塊。</span><span class="sxs-lookup"><span data-stu-id="64bad-200">Open *Content/Site.css*, and find the block for the `body` tag.</span></span>
2. <span data-ttu-id="64bad-201">將 `background-color` 的值從 `#fff` 變更為 `darkblue`。</span><span class="sxs-lookup"><span data-stu-id="64bad-201">Change the value for `background-color` from `#fff` to `darkblue`.</span></span>

    [!code-css[Main](deploying-a-code-update/samples/sample4.css?highlight=2)]

### <a name="view-the-change-in-the-publish-preview-window"></a><span data-ttu-id="64bad-202">在 [發行預覽] 視窗中查看變更</span><span class="sxs-lookup"><span data-stu-id="64bad-202">View the change in the Publish Preview window</span></span>

<span data-ttu-id="64bad-203">當您使用 [**發行 Web** wizard] 發行專案時，您可以在 [**預覽**] 視窗中按兩下該檔案，以查看即將發行的變更。</span><span class="sxs-lookup"><span data-stu-id="64bad-203">When you use the **Publish Web** wizard to publish the project, you can see what changes are going to be published by double-clicking the file in the **Preview** window.</span></span>

1. <span data-ttu-id="64bad-204">以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。</span><span class="sxs-lookup"><span data-stu-id="64bad-204">Right-click the ContosoUniversity project and click **Publish**.</span></span>
2. <span data-ttu-id="64bad-205">從 [**設定檔**] 下拉式清單中，選取 [**測試**發行設定檔]。</span><span class="sxs-lookup"><span data-stu-id="64bad-205">From the **Profile** drop-down list, select the **Test** publish profile.</span></span>
3. <span data-ttu-id="64bad-206">按一下 [**預覽**]，然後按一下 [**開始預覽**]。</span><span class="sxs-lookup"><span data-stu-id="64bad-206">Click **Preview**, and then click **Start Preview**.</span></span>
4. <span data-ttu-id="64bad-207">在**預覽**窗格中，按兩下 [ **Site .css**]。</span><span class="sxs-lookup"><span data-stu-id="64bad-207">In the **Preview** pane, double-click **Site.css**.</span></span>

    ![按兩下 [網站 .css]](deploying-a-code-update/_static/image9.png)

    <span data-ttu-id="64bad-209">[**預覽變更**] 對話方塊會顯示即將部署之變更的預覽。</span><span class="sxs-lookup"><span data-stu-id="64bad-209">The **Preview changes** dialog shows a preview of the changes that will be deployed.</span></span>

    ![網站 .css 的預覽變更](deploying-a-code-update/_static/image10.png)

    <span data-ttu-id="64bad-211">如果您*按兩下 web.config 檔案*，[**預覽變更**] 對話方塊會顯示組建設定轉換和發行設定檔轉換的效果。</span><span class="sxs-lookup"><span data-stu-id="64bad-211">If you double-click the *Web.config* file, the **Preview changes** dialog shows the effect of your build configuration transformations and publish profile transformations.</span></span> <span data-ttu-id="64bad-212">此時，您未做任何會導致伺服器上的*web.config*檔案變更的動作，因此您預期不會有任何變更。</span><span class="sxs-lookup"><span data-stu-id="64bad-212">At this point you have not done anything that would cause the *Web.config* file on the server to change, so you expect to see no changes.</span></span> <span data-ttu-id="64bad-213">不過，[**預覽變更**] 視窗會錯誤地顯示兩個變更。</span><span class="sxs-lookup"><span data-stu-id="64bad-213">However, the **Preview changes** window incorrectly shows two changes.</span></span> <span data-ttu-id="64bad-214">這看起來會移除兩個 XML 元素。</span><span class="sxs-lookup"><span data-stu-id="64bad-214">It looks like two XML elements will be removed.</span></span> <span data-ttu-id="64bad-215">當您在 Code First 內容類別的**應用程式啟動上選取 [執行 Code First 移轉**] 時，發佈程式會新增這些元素。</span><span class="sxs-lookup"><span data-stu-id="64bad-215">These elements are added by the publish process when you select **Execute Code First Migrations on application start** for a Code First context class.</span></span> <span data-ttu-id="64bad-216">比較是在發行程式新增這些元素之前完成，因此它似乎已被移除，但不會被移除。</span><span class="sxs-lookup"><span data-stu-id="64bad-216">The comparison is done before the publish process adds those elements, so it looks like they are being removed although they will not be removed.</span></span> <span data-ttu-id="64bad-217">此錯誤將在未來的版本中修正。</span><span class="sxs-lookup"><span data-stu-id="64bad-217">This error will be corrected in a future release.</span></span>
5. <span data-ttu-id="64bad-218">按一下 [ **關閉**]。</span><span class="sxs-lookup"><span data-stu-id="64bad-218">Click **Close**.</span></span>
6. <span data-ttu-id="64bad-219">按一下 [發行]。</span><span class="sxs-lookup"><span data-stu-id="64bad-219">Click **Publish**.</span></span>
7. <span data-ttu-id="64bad-220">當瀏覽器開啟至測試網站的首頁時，請按 CTRL + F5 以進行硬重新整理，以便查看 CSS 變更的效果。</span><span class="sxs-lookup"><span data-stu-id="64bad-220">When the browser opens to the home page of the Test site, press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![CSS 變更的效果](deploying-a-code-update/_static/image11.png)
8. <span data-ttu-id="64bad-222">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="64bad-222">Close the browser.</span></span>

### <a name="publish-specific-files-from-solution-explorer"></a><span data-ttu-id="64bad-223">從方案總管發行特定檔案</span><span class="sxs-lookup"><span data-stu-id="64bad-223">Publish specific files from Solution Explorer</span></span>

<span data-ttu-id="64bad-224">假設您不喜歡藍色背景，而且想要還原成原始的色彩。</span><span class="sxs-lookup"><span data-stu-id="64bad-224">Suppose you don't like the blue background and want to revert to the original color.</span></span> <span data-ttu-id="64bad-225">在本節中，您將直接從**方案總管**發佈特定檔案，以還原原始設定。</span><span class="sxs-lookup"><span data-stu-id="64bad-225">In this section you'll restore the original settings by publishing a specific file directly from **Solution Explorer**.</span></span>

1. <span data-ttu-id="64bad-226">開啟*Content/Site .css* ，然後將 `background-color` 設定還原為 [`#fff`]。</span><span class="sxs-lookup"><span data-stu-id="64bad-226">Open *Content/Site.css* and restore the `background-color` setting to `#fff`.</span></span>
2. <span data-ttu-id="64bad-227">在**方案總管**中，以滑鼠右鍵按一下*內容/網站 .css*檔案。</span><span class="sxs-lookup"><span data-stu-id="64bad-227">In **Solution Explorer**, right-click the *Content/Site.css* file.</span></span>

    <span data-ttu-id="64bad-228">內容功能表會顯示三個 [發行] 選項。</span><span class="sxs-lookup"><span data-stu-id="64bad-228">The context menu shows three publish options.</span></span>

    ![從方案總管發佈選項](deploying-a-code-update/_static/image12.png)
3. <span data-ttu-id="64bad-230">按一下 [**預覽變更] 至 [網站 .css**]。</span><span class="sxs-lookup"><span data-stu-id="64bad-230">Click **Preview changes to Site.css**.</span></span>

    <span data-ttu-id="64bad-231">視窗隨即開啟，以顯示本機檔案與其在目的地環境中的版本之間的差異。</span><span class="sxs-lookup"><span data-stu-id="64bad-231">A window opens to show the differences between the local file and the version of it in the destination environment.</span></span>

    ![Diff-Content/Site .css](deploying-a-code-update/_static/image13.png)
4. <span data-ttu-id="64bad-233">在**方案總管**中，再次以滑鼠右鍵按一下 [**網站 .css** ]，然後按一下 [**發行網站 .css**]。</span><span class="sxs-lookup"><span data-stu-id="64bad-233">In **Solution Explorer**, right-click **Site.css** again and click **Publish Site.css**.</span></span>

    <span data-ttu-id="64bad-234">[ **Web 發行活動**] 視窗會顯示檔案已發行。</span><span class="sxs-lookup"><span data-stu-id="64bad-234">The **Web Publish Activity** window shows that the file has been published.</span></span>

    ![[Web 發行活動] 視窗](deploying-a-code-update/_static/image14.png)
5. <span data-ttu-id="64bad-236">開啟瀏覽器並前往 [`http://localhost/contosouniversity` URL]，然後按 CTRL + F5 以進行硬重新整理，以便查看 CSS 變更的效果。</span><span class="sxs-lookup"><span data-stu-id="64bad-236">Open a browser to the `http://localhost/contosouniversity` URL, and then press CTRL+F5 to cause a hard refresh in order to see the effect of the CSS change.</span></span>

    ![具有一般 CSS 的首頁](deploying-a-code-update/_static/image15.png)
6. <span data-ttu-id="64bad-238">關閉瀏覽器。</span><span class="sxs-lookup"><span data-stu-id="64bad-238">Close the browser.</span></span>

## <a name="summary"></a><span data-ttu-id="64bad-239">總結</span><span class="sxs-lookup"><span data-stu-id="64bad-239">Summary</span></span>

<span data-ttu-id="64bad-240">您現在已瞭解幾種部署應用程式更新的方式，而不需要變更資料庫，而且您已瞭解如何預覽變更，以確認會更新的內容是您的預期。</span><span class="sxs-lookup"><span data-stu-id="64bad-240">You've now seen several ways to deploy an application update that does not involve a database change, and you've seen how to preview the changes to verify that what will be updated is what you expect.</span></span> <span data-ttu-id="64bad-241">[講師] 頁面現在有 [**課程教授**] 區段。</span><span class="sxs-lookup"><span data-stu-id="64bad-241">The Instructors page now has a **Courses Taught** section.</span></span>

![講師頁面包含教授的課程](deploying-a-code-update/_static/image16.png)

<span data-ttu-id="64bad-243">下一個教學課程會示範如何部署資料庫變更：您會將 [出生日期] 欄位加入至資料庫和 [講師] 頁面。</span><span class="sxs-lookup"><span data-stu-id="64bad-243">The next tutorial shows you how to deploy a database change: you'll add a birthdate field to the database and to the Instructors page.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="64bad-244">[上一頁](deploying-to-production.md)
> [下一頁](deploying-a-database-update.md)</span><span class="sxs-lookup"><span data-stu-id="64bad-244">[Previous](deploying-to-production.md)
[Next](deploying-a-database-update.md)</span></span>
