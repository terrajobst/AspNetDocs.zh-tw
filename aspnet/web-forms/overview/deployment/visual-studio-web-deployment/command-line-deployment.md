---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 使用 Visual Studio：命令列部署來 ASP.NET Web 部署 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74634196"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a><span data-ttu-id="a1b9d-103">使用 Visual Studio：命令列部署來 ASP.NET Web 部署</span><span class="sxs-lookup"><span data-stu-id="a1b9d-103">ASP.NET Web Deployment using Visual Studio: Command Line Deployment</span></span>

<span data-ttu-id="a1b9d-104">由[Tom 作者: dykstra](https://github.com/tdykstra)</span><span class="sxs-lookup"><span data-stu-id="a1b9d-104">by [Tom Dykstra](https://github.com/tdykstra)</span></span>

[<span data-ttu-id="a1b9d-105">下載入門專案</span><span class="sxs-lookup"><span data-stu-id="a1b9d-105">Download Starter Project</span></span>](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> <span data-ttu-id="a1b9d-106">本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-106">This tutorial series shows you how to deploy (publish) an ASP.NET web application to Azure App Service Web Apps or to a third-party hosting provider, by using Visual Studio 2012 or Visual Studio 2010.</span></span> <span data-ttu-id="a1b9d-107">如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-107">For information about the series, see [the first tutorial in the series](introduction.md).</span></span>

## <a name="overview"></a><span data-ttu-id="a1b9d-108">概觀</span><span class="sxs-lookup"><span data-stu-id="a1b9d-108">Overview</span></span>

<span data-ttu-id="a1b9d-109">本教學課程說明如何從命令列叫用 Visual Studio web 發佈管線。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-109">This tutorial shows you how to invoke the Visual Studio web publish pipeline from the command line.</span></span> <span data-ttu-id="a1b9d-110">這適用于您想要將部署程式[自動化](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)的案例，而不是在 Visual Studio 中手動執行，通常是使用[原始程式碼版本控制系統](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-110">This is useful for scenarios where you want to [automate the deployment process](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md) instead of doing it manually in Visual Studio, typically by using a [source code version control system](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md).</span></span>

## <a name="make-a-change-to-deploy"></a><span data-ttu-id="a1b9d-111">進行部署的變更</span><span class="sxs-lookup"><span data-stu-id="a1b9d-111">Make a change to deploy</span></span>

<span data-ttu-id="a1b9d-112">目前 [關於] 頁面會顯示範本程式碼。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-112">Currently the About page displays the template code.</span></span>

![包含範本程式碼的關於頁面](command-line-deployment/_static/image1.png)

<span data-ttu-id="a1b9d-114">您會將其取代為顯示學生註冊摘要的程式碼。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-114">You'll replace that with code that displays a summary of student enrollment.</span></span>

<span data-ttu-id="a1b9d-115">開啟*About .aspx*頁面，刪除 `MainContent` `Content` 元素內的所有標記，並在其位置插入下列標記：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-115">Open the *About.aspx* page, delete all of the markup inside the `MainContent` `Content` element, and insert the following markup in its place:</span></span>

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

<span data-ttu-id="a1b9d-116">執行專案，並選取 [**關於**] 頁面。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-116">Run the project and select the **About** page.</span></span>

![About 頁面](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a><span data-ttu-id="a1b9d-118">使用命令列部署以進行測試</span><span class="sxs-lookup"><span data-stu-id="a1b9d-118">Deploy to Test by using the command line</span></span>

<span data-ttu-id="a1b9d-119">您不會部署其他資料庫變更，因此請停用 aspnet ContosoUniversity 資料庫的 dbDacFx 資料庫部署。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-119">You won't be deploying another database change, so disable dbDacFx database deployment for the aspnet-ContosoUniversity database.</span></span> <span data-ttu-id="a1b9d-120">開啟 [**發行 Web** wizard]，並在三個發行設定檔的每一個中，清除 [**設定**] 索引標籤上的 [**更新資料庫**] 核取方塊。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-120">Open the **Publish Web** wizard, and in each of the three publish profiles, clear the **Update Database** check box on the **Settings** tab.</span></span>

<span data-ttu-id="a1b9d-121">在 Windows 8 起始頁中，搜尋**VS2012 的開發人員命令提示字元**。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-121">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**.</span></span>

<span data-ttu-id="a1b9d-122">以滑鼠右鍵按一下 VS2012 的**開發人員命令提示字元**圖示，然後按一下 [**以系統管理員身分執行**]。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-122">Right-click the icon for **Developer Command Prompt for VS2012** and click **Run as administrator**.</span></span>

<span data-ttu-id="a1b9d-123">在命令提示字元中輸入下列命令，以方案檔的路徑取代方案檔的路徑：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-123">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file:</span></span>

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

<span data-ttu-id="a1b9d-124">MSBuild 會建立方案，並將其部署至測試環境。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-124">MSBuild builds the solution and deploys it to the test environment.</span></span>

![命令列輸出](command-line-deployment/_static/image3.png)

<span data-ttu-id="a1b9d-126">開啟瀏覽器並移至 `http://localhost/ContosoUniversity`，然後按一下 [**關於**] 頁面，確認部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-126">Open a browser and go to `http://localhost/ContosoUniversity`, then click the **About** page to verify that the deployment was successful.</span></span>

<span data-ttu-id="a1b9d-127">如果您尚未在測試中建立任何學生，您會在 [**學生主體統計資料]** 標題底下看到空白頁面。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-127">If you haven't created any students in test, you'll see an empty page under the **Student Body Statistics** heading.</span></span> <span data-ttu-id="a1b9d-128">前往 [**學生**] 頁面，按一下 [**新增學生**]，再新增一些學生，然後返回 [**關於**] 頁面以查看學生統計資料。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-128">Go to the **Students** page, click **Add Student**, and add some students, and then return to the **About** page to see student statistics.</span></span>

![測試環境中的關於頁面](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a><span data-ttu-id="a1b9d-130">金鑰命令列選項</span><span class="sxs-lookup"><span data-stu-id="a1b9d-130">Key command line options</span></span>

<span data-ttu-id="a1b9d-131">您輸入的命令已將解決方案檔案路徑和兩個屬性傳遞至 MSBuild：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-131">The command that you entered passed the solution file path and two properties to MSBuild:</span></span>

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a><span data-ttu-id="a1b9d-132">部署解決方案與部署個別專案</span><span class="sxs-lookup"><span data-stu-id="a1b9d-132">Deploying the solution versus deploying individual projects</span></span>

<span data-ttu-id="a1b9d-133">指定方案檔會導致建立方案中的所有專案。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-133">Specifying the solution file causes all projects in the solution to be built.</span></span> <span data-ttu-id="a1b9d-134">如果您的方案中有多個 Web 專案，則會套用下列 MSBuild 行為：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-134">If you have multiple web projects in the solution, the following MSBuild behavior applies:</span></span>

- <span data-ttu-id="a1b9d-135">您在命令列上指定的屬性會傳遞至每個專案。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-135">The properties that you specify on the command line are passed to every project.</span></span> <span data-ttu-id="a1b9d-136">因此，每個 Web 專案都必須有您指定之名稱的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-136">Therefore, each web project must have a publish profile with the name that you specify.</span></span> <span data-ttu-id="a1b9d-137">如果您指定 `/p:PublishProfile=Test`，每個 Web 專案都必須有一個名為*Test*的發行設定檔。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-137">If you specify `/p:PublishProfile=Test`, each web project must have a publish profile named *Test*.</span></span>
- <span data-ttu-id="a1b9d-138">當另一個專案不是建立時，您可能會成功發行一個。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-138">You might successfully publish one project when another one doesn't even build.</span></span> <span data-ttu-id="a1b9d-139">如需詳細資訊，請參閱 stackoverflow 執行緒[MSBuild 失敗並有兩個封裝](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-139">For more information, see the stackoverflow thread [MSBuild fails with two packages](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages).</span></span>

<span data-ttu-id="a1b9d-140">如果您指定個別的專案，而不是方案，則必須加入指定 Visual Studio 版本的參數。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-140">If you specify an individual project instead of a solution, you have to add a parameter that specifies the Visual Studio version.</span></span> <span data-ttu-id="a1b9d-141">如果您使用 Visual Studio 2012，命令列會類似于下列範例：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-141">If you are using Visual Studio 2012 the command line would be similar to the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

<span data-ttu-id="a1b9d-142">Visual Studio 2010 的版本號碼為10.0。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-142">The version number for Visual Studio 2010 is 10.0.</span></span> <span data-ttu-id="a1b9d-143">如需詳細資訊，請參閱 Sayed Hashimi 的 blog 中的[Visual Studio 專案相容性和 VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) 。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-143">For more information, see [Visual Studio project compatibility and VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) on Sayed Hashimi's blog.</span></span>

### <a name="specifying-the-publish-profile"></a><span data-ttu-id="a1b9d-144">指定發行設定檔</span><span class="sxs-lookup"><span data-stu-id="a1b9d-144">Specifying the publish profile</span></span>

<span data-ttu-id="a1b9d-145">您可以依名稱或 *.pubxml*檔案的完整路徑來指定發行設定檔，如下列範例所示：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-145">You can specify the publish profile by name or by the full path to the *.pubxml* file, as shown in the following example:</span></span>

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a><span data-ttu-id="a1b9d-146">支援命令列發行的 Web 發行方法</span><span class="sxs-lookup"><span data-stu-id="a1b9d-146">Web publish methods supported for command-line publishing</span></span>

<span data-ttu-id="a1b9d-147">命令列發行支援三種發行方法：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-147">Three publish methods are supported for command line publishing:</span></span>

- <span data-ttu-id="a1b9d-148">`MSDeploy`-使用 Web Deploy 發佈。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-148">`MSDeploy` - Publish by using Web Deploy.</span></span>
- <span data-ttu-id="a1b9d-149">`Package`-藉由建立 Web Deploy 套件來發行。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-149">`Package` - Publish by creating a Web Deploy Package.</span></span> <span data-ttu-id="a1b9d-150">您必須從建立套件的 MSBuild 命令分開安裝。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-150">You have to install the package separately from the MSBuild command that creates it.</span></span>
- <span data-ttu-id="a1b9d-151">`FileSystem`-將檔案複製到指定的資料夾以進行發佈。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-151">`FileSystem` - Publish by copying files to a specified folder.</span></span>

### <a name="specifying-the-build-configuration-and-platform"></a><span data-ttu-id="a1b9d-152">指定組建設定和平臺</span><span class="sxs-lookup"><span data-stu-id="a1b9d-152">Specifying the build configuration and platform</span></span>

<span data-ttu-id="a1b9d-153">組建設定和平臺必須在 Visual Studio 中或在命令列上設定。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-153">The build configuration and platform must be set in Visual Studio or on the command line.</span></span> <span data-ttu-id="a1b9d-154">發行設定檔包含名為 `LastUsedBuildConfiguration` 和 `LastUsedPlatform`的屬性，但您無法設定這些屬性，以決定專案的建立方式。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-154">The publish profiles include properties that are named `LastUsedBuildConfiguration` and `LastUsedPlatform`, but you can't set these properties in order to determine how the project is built.</span></span> <span data-ttu-id="a1b9d-155">如需詳細資訊，請參閱[MSBuild：如何設定](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)Sayed Hashimi 的 blog 的 configuration 屬性。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-155">For more information, see [MSBuild: how to set the configuration property](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx) on Sayed Hashimi's blog.</span></span>

## <a name="deploy-to-staging"></a><span data-ttu-id="a1b9d-156">部署至預備環境</span><span class="sxs-lookup"><span data-stu-id="a1b9d-156">Deploy to staging</span></span>

<span data-ttu-id="a1b9d-157">若要部署至 Azure，您必須將密碼新增至命令列。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-157">To deploy to Azure, you must add the password to the command line.</span></span> <span data-ttu-id="a1b9d-158">如果您已將密碼儲存在 Visual Studio 的發行設定檔中，它會以加密格式儲存在您的 *.pubxml 使用者*檔案中。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-158">If you saved the password in the publish profile in Visual Studio, it was stored in encrypted form in the your *.pubxml.user* file.</span></span> <span data-ttu-id="a1b9d-159">當您執行命令列部署時，MSBuild 不會存取該檔案，因此您必須在命令列參數中傳入密碼。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-159">That file is not accessed by MSBuild when you do a command line deployment, so you have to pass in the password in a command line parameter.</span></span>

1. <span data-ttu-id="a1b9d-160">從您稍早針對預備網站所下載的 *.publishsettings*檔案複製所需的密碼。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-160">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the staging web site.</span></span> <span data-ttu-id="a1b9d-161">Password 是 Web Deploy `publishProfile` 元素的 `userPWD` 屬性值。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-161">The password is the value of the `userPWD` attribute for the Web Deploy `publishProfile` element.</span></span>

    ![Web Deploy 密碼](command-line-deployment/_static/image5.png)
2. <span data-ttu-id="a1b9d-163">在 Windows 8 起始頁中，搜尋**VS2012 的開發人員命令提示字元**，然後按一下圖示以開啟命令提示字元。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-163">In the Windows 8 Start page, search for **Developer Command Prompt for VS2012**, and click the icon to open the command prompt.</span></span> <span data-ttu-id="a1b9d-164">（這次您不需要將它開啟為系統管理員，因為您不是部署到本機電腦上的 IIS）。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-164">(You don't have to open it as administrator this time because you aren't deploying to IIS on the local computer.)</span></span>
3. <span data-ttu-id="a1b9d-165">在命令提示字元中輸入下列命令，將方案檔的路徑取代為您方案檔的路徑，並將密碼替換成您的密碼：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-165">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    <span data-ttu-id="a1b9d-166">請注意，此命令列會包含額外的參數： `/p:AllowUntrustedCertificate=true`。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-166">Notice that this command line includes an extra parameter: `/p:AllowUntrustedCertificate=true`.</span></span> <span data-ttu-id="a1b9d-167">隨著本教學課程的撰寫，當您從命令列發佈至 Azure 時，必須設定 `AllowUntrustedCertificate` 屬性。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-167">As this tutorial is being written, the `AllowUntrustedCertificate` property must be set when you publish to Azure from the command line.</span></span> <span data-ttu-id="a1b9d-168">當此 bug 的修正程式發行時，您就不需要該參數。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-168">When the fix for this bug is released, you won't need that parameter.</span></span>
4. <span data-ttu-id="a1b9d-169">開啟瀏覽器並移至預備網站的 URL，然後按一下 [**關於**] 頁面，確認部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-169">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

    <span data-ttu-id="a1b9d-170">如您稍早在測試環境中所見，您可能必須建立一些學生，才能在 [**關於**] 頁面上查看統計資料。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-170">As you saw earlier for the test environment, you might have to create some students to see statistics on the **About** page.</span></span>

## <a name="deploy-to-production"></a><span data-ttu-id="a1b9d-171">部署到生產環境</span><span class="sxs-lookup"><span data-stu-id="a1b9d-171">Deploy to production</span></span>

<span data-ttu-id="a1b9d-172">部署至生產環境的程式與預備的進程類似。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-172">The process for deploying to production is similar to the process for staging.</span></span>

1. <span data-ttu-id="a1b9d-173">從您稍早針對生產網站所下載的 *.publishsettings*檔案複製所需的密碼。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-173">Copy the password that you need from the *.publishsettings* file that you downloaded earlier for the production web site.</span></span>
2. <span data-ttu-id="a1b9d-174">開啟**VS2012 的開發人員命令提示字元**。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-174">Open **Developer Command Prompt for VS2012**.</span></span>
3. <span data-ttu-id="a1b9d-175">在命令提示字元中輸入下列命令，將方案檔的路徑取代為您方案檔的路徑，並將密碼替換成您的密碼：</span><span class="sxs-lookup"><span data-stu-id="a1b9d-175">Enter the following command at the command prompt, replacing the path to the solution file with the path to your solution file and the password with your password:</span></span>

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    <span data-ttu-id="a1b9d-176">對於實際的生產網站，如果也有資料庫變更，您通常會在部署之前將*應用程式\_離線 .htm*檔案複製到網站，並在部署成功之後將其刪除。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-176">For a real production site, if there was also a database change, you would typically copy the *app\_offline.htm* file to the site before deployment and delete it after successful deployment.</span></span>
4. <span data-ttu-id="a1b9d-177">開啟瀏覽器並移至預備網站的 URL，然後按一下 [**關於**] 頁面，確認部署是否成功。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-177">Open a browser and go to the URL of your staging site, and then click the **About** page to verify that the deployment was successful.</span></span>

## <a name="summary"></a><span data-ttu-id="a1b9d-178">總結</span><span class="sxs-lookup"><span data-stu-id="a1b9d-178">Summary</span></span>

<span data-ttu-id="a1b9d-179">您現在已使用命令列部署應用程式更新。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-179">You have now deployed an application update by using the command line.</span></span>

![測試環境中的關於頁面](command-line-deployment/_static/image6.png)

<span data-ttu-id="a1b9d-181">在下一個教學課程中，您會看到如何擴充 web 發佈管線的範例。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-181">In the next tutorial, you will see an example of how to extend the web publish pipeline.</span></span> <span data-ttu-id="a1b9d-182">此範例將示範如何部署專案中未包含的檔案。</span><span class="sxs-lookup"><span data-stu-id="a1b9d-182">The example will show you how to deploy files that are not included in the project.</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="a1b9d-183">[上一頁](deploying-a-database-update.md)
> [下一頁](deploying-extra-files.md)</span><span class="sxs-lookup"><span data-stu-id="a1b9d-183">[Previous](deploying-a-database-update.md)
[Next](deploying-extra-files.md)</span></span>
