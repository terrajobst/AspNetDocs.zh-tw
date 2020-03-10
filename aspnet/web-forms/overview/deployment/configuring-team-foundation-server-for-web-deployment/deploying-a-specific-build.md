---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
title: 部署特定組建 |Microsoft Docs
author: jrjlee
description: 本主題描述如何將 web 封裝和資料庫腳本從特定的先前組建部署到新的目的地，例如預備或生產 enviro 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c979535f-48a3-4ec4-a633-a77889b86ddb
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build
msc.type: authoredcontent
ms.openlocfilehash: 6bede6b36c24ade928ab052e14daec1e017bd0b2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78639668"
---
# <a name="deploying-a-specific-build"></a><span data-ttu-id="bf099-103">部署特定的組建</span><span class="sxs-lookup"><span data-stu-id="bf099-103">Deploying a Specific Build</span></span>

<span data-ttu-id="bf099-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="bf099-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="bf099-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="bf099-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="bf099-106">本主題描述如何將 web 封裝和資料庫腳本從特定的先前組建部署到新的目的地，例如預備或生產環境。</span><span class="sxs-lookup"><span data-stu-id="bf099-106">This topic describes how to deploy web packages and database scripts from a specific previous build to a new destination, like a staging or production environment.</span></span>

<span data-ttu-id="bf099-107">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="bf099-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="bf099-108">這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建和部署程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="bf099-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="bf099-109">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="bf099-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="bf099-110">工作總覽</span><span class="sxs-lookup"><span data-stu-id="bf099-110">Task Overview</span></span>

<span data-ttu-id="bf099-111">到目前為止，本教學課程中的主題設定著重于如何建立、封裝和部署 web 應用程式和資料庫，做為單一步驟或自動化程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="bf099-111">Until now, the topics in this tutorial set have focused on how to build, package, and deploy web applications and databases as part of a single-step or automated process.</span></span> <span data-ttu-id="bf099-112">不過，在某些常見的案例中，您會想要從 [放置] 資料夾中的組建清單來選取您部署的資源。</span><span class="sxs-lookup"><span data-stu-id="bf099-112">However, in some common scenarios, you'll want to select the resources that you deploy from a list of builds in a drop folder.</span></span> <span data-ttu-id="bf099-113">換句話說，最新的組建可能不是您想要部署的組建。</span><span class="sxs-lookup"><span data-stu-id="bf099-113">In other words, the latest build may not be the build you want to deploy.</span></span>

<span data-ttu-id="bf099-114">請考慮上一個主題中所述的持續整合（CI）案例，建立[支援部署的組建定義](creating-a-build-definition-that-supports-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="bf099-114">Consider the continuous integration (CI) scenario described in the previous topic, [Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="bf099-115">您已在 Team Foundation Server （TFS）2010中建立組建定義。</span><span class="sxs-lookup"><span data-stu-id="bf099-115">You've created a build definition in Team Foundation Server (TFS) 2010.</span></span> <span data-ttu-id="bf099-116">每當開發人員將程式碼簽入 TFS 時，Team Build 就會建立您的程式碼，將 web 封裝和資料庫腳本當做組建流程的一部分來執行、執行任何單元測試，並將您的資源部署到測試環境。</span><span class="sxs-lookup"><span data-stu-id="bf099-116">Every time a developer checks code into TFS, Team Build will build your code, create web packages and database scripts as part of the build process, run any unit tests, and deploy your resources to a test environment.</span></span> <span data-ttu-id="bf099-117">根據您在建立組建定義時所設定的保留原則，TFS 會保留特定數目的先前組建。</span><span class="sxs-lookup"><span data-stu-id="bf099-117">Depending on the retention policy you configured when you created the build definition, TFS will retain a certain number of previous builds.</span></span>

![](deploying-a-specific-build/_static/image1.png)

<span data-ttu-id="bf099-118">現在，假設您已針對測試環境中的其中一個組建執行驗證和驗證測試，而且您已準備好將應用程式部署至預備環境。</span><span class="sxs-lookup"><span data-stu-id="bf099-118">Now, suppose you've performed verification and validation testing against one of these builds in your test environment, and you're ready to deploy your application to a staging environment.</span></span> <span data-ttu-id="bf099-119">在此同時，開發人員可能已簽入新的程式碼。</span><span class="sxs-lookup"><span data-stu-id="bf099-119">In the meantime, developers may have checked in new code.</span></span> <span data-ttu-id="bf099-120">您不想要重建解決方案並部署至預備環境，而且不想要將最新的組建部署至預備環境。</span><span class="sxs-lookup"><span data-stu-id="bf099-120">You don't want to rebuild the solution and deploy to the staging environment, and you don't want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="bf099-121">相反地，您會想要部署已在測試伺服器上驗證並驗證的特定組建。</span><span class="sxs-lookup"><span data-stu-id="bf099-121">Instead, you want to deploy the specific build that you've verified and validated on the test servers.</span></span>

<span data-ttu-id="bf099-122">若要完成此動作，您必須告訴 Microsoft Build Engine （MSBuild）哪裡可以找到特定組建所產生的 web 套件和資料庫腳本。</span><span class="sxs-lookup"><span data-stu-id="bf099-122">To accomplish this, you need to tell the Microsoft Build Engine (MSBuild) where to find the web packages and database scripts that a specific build generated.</span></span>

## <a name="overriding-the-outputroot-property"></a><span data-ttu-id="bf099-123">覆寫 OutputRoot 屬性</span><span class="sxs-lookup"><span data-stu-id="bf099-123">Overriding the OutputRoot Property</span></span>

<span data-ttu-id="bf099-124">在[範例方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)中， *Publish*檔案會宣告名為**OutputRoot**的屬性。</span><span class="sxs-lookup"><span data-stu-id="bf099-124">In the [sample solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md), the *Publish.proj* file declares a property named **OutputRoot**.</span></span> <span data-ttu-id="bf099-125">如其名所示，這是包含組建程式所產生之所有專案的根資料夾。</span><span class="sxs-lookup"><span data-stu-id="bf099-125">As the name suggests, this is the root folder that contains everything that the build process generates.</span></span> <span data-ttu-id="bf099-126">在*Publish*檔案中，您可以看到**OutputRoot**屬性指的是所有部署資源的根位置。</span><span class="sxs-lookup"><span data-stu-id="bf099-126">In the *Publish.proj* file, you can see that the **OutputRoot** property refers to the root location for all deployment resources.</span></span>

> [!NOTE]
> <span data-ttu-id="bf099-127">**OutputRoot**是常用的屬性名稱。</span><span class="sxs-lookup"><span data-stu-id="bf099-127">**OutputRoot** is a commonly used property name.</span></span> <span data-ttu-id="bf099-128">視覺C#效果和 Visual Basic 專案檔也會宣告此屬性，以儲存所有組建輸出的根位置。</span><span class="sxs-lookup"><span data-stu-id="bf099-128">Visual C# and Visual Basic project files also declare this property to store the root location for all build outputs.</span></span>

[!code-xml[Main](deploying-a-specific-build/samples/sample1.xml)]

<span data-ttu-id="bf099-129">如果您想要讓專案檔從不同的位置&#x2014;部署 web 封裝和資料庫腳本，例如先前 TFS 組建&#x2014;的輸出，您只需要覆寫**OutputRoot**屬性。</span><span class="sxs-lookup"><span data-stu-id="bf099-129">If you want your project file to deploy web packages and database scripts from a different location&#x2014;like the outputs of a previous TFS build&#x2014;you simply need to override the **OutputRoot** property.</span></span> <span data-ttu-id="bf099-130">您應該將屬性值設定為 Team Build server 上的相關組建資料夾。</span><span class="sxs-lookup"><span data-stu-id="bf099-130">You should set the property value to the relevant build folder on the Team Build server.</span></span> <span data-ttu-id="bf099-131">如果您是從命令列執行 MSBuild，您可以將**OutputRoot**的值指定為命令列引數：</span><span class="sxs-lookup"><span data-stu-id="bf099-131">If you were running MSBuild from the command line, you could specify a value for **OutputRoot** as a command-line argument:</span></span>

[!code-console[Main](deploying-a-specific-build/samples/sample2.cmd)]

<span data-ttu-id="bf099-132">不過，在實務上，如果您不打算使用組建輸出，&#x2014;您也會想要略過**組建目標，而不**需要建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="bf099-132">In practice, however, you'd also want to skip the **Build** target&#x2014;there's no point in building your solution if you don't plan to use the build outputs.</span></span> <span data-ttu-id="bf099-133">您可以藉由指定要從命令列執行的目標來執行這項操作：</span><span class="sxs-lookup"><span data-stu-id="bf099-133">You could do this by specifying the targets you want to execute from the command line:</span></span>

[!code-console[Main](deploying-a-specific-build/samples/sample3.cmd)]

<span data-ttu-id="bf099-134">不過，在大部分的情況下，您會想要將部署邏輯建立至 TFS 組建定義中。</span><span class="sxs-lookup"><span data-stu-id="bf099-134">However, in most cases, you'll want to build your deployment logic into a TFS build definition.</span></span> <span data-ttu-id="bf099-135">這可讓具有**佇列組建**許可權的使用者，從任何具有 TFS 伺服器連接的 Visual Studio 安裝觸發部署。</span><span class="sxs-lookup"><span data-stu-id="bf099-135">This enables users with the **Queue builds** permission to trigger the deployment from any Visual Studio installation with a connection to the TFS server.</span></span>

## <a name="creating-a-build-definition-to-deploy-specific-builds"></a><span data-ttu-id="bf099-136">建立組建定義以部署特定組建</span><span class="sxs-lookup"><span data-stu-id="bf099-136">Creating a Build Definition to Deploy Specific Builds</span></span>

<span data-ttu-id="bf099-137">下一個程式描述如何建立組建定義，讓使用者使用單一命令觸發對預備環境的部署。</span><span class="sxs-lookup"><span data-stu-id="bf099-137">The next procedure describes how to create a build definition that enables users to trigger deployments to a staging environment with a single command.</span></span>

<span data-ttu-id="bf099-138">在這種情況下，您不想讓組建定義實際建立&#x2014;您想要它在自訂專案檔中執行部署邏輯的任何作業。</span><span class="sxs-lookup"><span data-stu-id="bf099-138">In this case, you don't want the build definition to actually build anything&#x2014;you just want it to execute the deployment logic in your custom project file.</span></span> <span data-ttu-id="bf099-139">如果檔案是在 Team Build 中執行，則*Publish*檔案包含會略過**組建**目標的條件式邏輯。</span><span class="sxs-lookup"><span data-stu-id="bf099-139">The *Publish.proj* file includes conditional logic that skips the **Build** target if the file is running in Team Build.</span></span> <span data-ttu-id="bf099-140">它會藉由評估內建的**BuildingInTeamBuild**屬性來完成這項工作，如果您在 Team Build 中執行專案檔，它會自動設定為**true** 。</span><span class="sxs-lookup"><span data-stu-id="bf099-140">It does this by evaluating the built-in **BuildingInTeamBuild** property, which is automatically set to **true** if you run your project file in Team Build.</span></span> <span data-ttu-id="bf099-141">因此，您可以略過建立程式，並直接執行專案檔來部署現有的組建。</span><span class="sxs-lookup"><span data-stu-id="bf099-141">As a result, you can skip the build process and simply run the project file to deploy an existing build.</span></span>

<span data-ttu-id="bf099-142">**若要建立組建定義以手動觸發部署**</span><span class="sxs-lookup"><span data-stu-id="bf099-142">**To create a build definition to trigger deployment manually**</span></span>

1. <span data-ttu-id="bf099-143">在 Visual Studio 2010 的 [ **Team Explorer** ] 視窗中，展開您的 Team 專案節點，以滑鼠右鍵按一下 [**組建**]，然後按一下 [**新增組建定義**]。</span><span class="sxs-lookup"><span data-stu-id="bf099-143">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](deploying-a-specific-build/_static/image2.png)
2. <span data-ttu-id="bf099-144">在 [**一般**] 索引標籤上，提供組建定義的名稱（例如， **DeployToStaging**）和選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="bf099-144">On the **General** tab, give the build definition a name (for example, **DeployToStaging**) and an optional description.</span></span>
3. <span data-ttu-id="bf099-145">在 [**觸發**程式] 索引標籤上，選取 [**手動–簽入不會觸發新的組建**]。</span><span class="sxs-lookup"><span data-stu-id="bf099-145">On the **Trigger** tab, select **Manual – Check-ins do not trigger a new build**.</span></span>
4. <span data-ttu-id="bf099-146">在 [**組建預設值**] 索引標籤的 [**將組建輸出複製到下列放置資料夾**] 方塊中，輸入放置資料夾的通用命名慣例（UNC）路徑（例如， **\\TFSBUILD\Drops**）。</span><span class="sxs-lookup"><span data-stu-id="bf099-146">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](deploying-a-specific-build/_static/image3.png)
5. <span data-ttu-id="bf099-147">在 [**流程**] 索引標籤的 [**建立**程式檔案] 下拉式清單中，將 [ **defaulttemplate.xaml** ] 保留為已選取。</span><span class="sxs-lookup"><span data-stu-id="bf099-147">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="bf099-148">這是新增至所有新 team 專案的其中一個預設組建流程範本。</span><span class="sxs-lookup"><span data-stu-id="bf099-148">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="bf099-149">在 [**建立流程參數**] 資料表中，按一下 [**要建立的專案**] 資料列，然後按一下**省略號**按鈕。</span><span class="sxs-lookup"><span data-stu-id="bf099-149">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](deploying-a-specific-build/_static/image4.png)
7. <span data-ttu-id="bf099-150">在 [**要建立的專案**] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="bf099-150">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="bf099-151">在 [**類型的專案**] 下拉式清單中，選取 [ **MSBuild 專案**檔]。</span><span class="sxs-lookup"><span data-stu-id="bf099-151">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
9. <span data-ttu-id="bf099-152">流覽至您用來控制部署程式的自訂專案檔位置，選取該檔案，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="bf099-152">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](deploying-a-specific-build/_static/image5.png)
10. <span data-ttu-id="bf099-153">在 [**要建立的專案**] 對話方塊中，按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="bf099-153">In the **Items to Build** dialog box, click **OK**.</span></span>
11. <span data-ttu-id="bf099-154">在 [**建立流程參數**] 資料表中，展開 [ **Advanced** ] 區段。</span><span class="sxs-lookup"><span data-stu-id="bf099-154">In the **Build process parameters** table, expand the **Advanced** section.</span></span>
12. <span data-ttu-id="bf099-155">在 [ **MSBuild 引數**] 資料列中，指定環境特定專案檔的位置，並為您的組建資料夾位置新增預留位置：</span><span class="sxs-lookup"><span data-stu-id="bf099-155">In the **MSBuild Arguments** row, specify the location of your environment-specific project file and add a placeholder for the location of your build folder:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample4.cmd)]

    ![](deploying-a-specific-build/_static/image6.png)

    > [!NOTE]
    > <span data-ttu-id="bf099-156">每次將組建排入佇列時，您都必須覆寫**OutputRoot**值。</span><span class="sxs-lookup"><span data-stu-id="bf099-156">You'll need to override the **OutputRoot** value every time you queue a build.</span></span> <span data-ttu-id="bf099-157">這會在下一個程式中討論。</span><span class="sxs-lookup"><span data-stu-id="bf099-157">This is covered in the next procedure.</span></span>
13. <span data-ttu-id="bf099-158">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="bf099-158">Click **Save**.</span></span>

<span data-ttu-id="bf099-159">當您觸發組建時，您必須更新**OutputRoot**屬性以指向您想要部署的組建。</span><span class="sxs-lookup"><span data-stu-id="bf099-159">When you trigger a build, you need to update the **OutputRoot** property to point to the build you want to deploy.</span></span>

<span data-ttu-id="bf099-160">**若要從組建定義部署特定的組建**</span><span class="sxs-lookup"><span data-stu-id="bf099-160">**To deploy a specific build from a build definition**</span></span>

1. <span data-ttu-id="bf099-161">在 [ **Team Explorer** ] 視窗中，以滑鼠右鍵按一下組建定義，然後按一下 [將**新組建**排入佇列]。</span><span class="sxs-lookup"><span data-stu-id="bf099-161">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](deploying-a-specific-build/_static/image7.png)
2. <span data-ttu-id="bf099-162">在 [**佇列組建**] 對話方塊的 [**參數**] 索引標籤上，展開 [ **Advanced** ] 區段。</span><span class="sxs-lookup"><span data-stu-id="bf099-162">In the **Queue Build** dialog box, on the **Parameters** tab, expand the **Advanced** section.</span></span>
3. <span data-ttu-id="bf099-163">在 [ **MSBuild 引數**] 資料列中，將**OutputRoot**屬性的值取代為組建資料夾的位置。</span><span class="sxs-lookup"><span data-stu-id="bf099-163">In the **MSBuild Arguments** row, replace the value of the **OutputRoot** property with the location of your build folder.</span></span> <span data-ttu-id="bf099-164">例如:</span><span class="sxs-lookup"><span data-stu-id="bf099-164">For example:</span></span>

    [!code-console[Main](deploying-a-specific-build/samples/sample5.cmd)]

    ![](deploying-a-specific-build/_static/image8.png)

    > [!NOTE]
    > <span data-ttu-id="bf099-165">請務必在組建資料夾路徑結尾包含尾端斜線。</span><span class="sxs-lookup"><span data-stu-id="bf099-165">Be sure to include a trailing slash at the end of the path to your build folder.</span></span>
4. <span data-ttu-id="bf099-166">按一下 [**佇列**]。</span><span class="sxs-lookup"><span data-stu-id="bf099-166">Click **Queue**.</span></span>

<span data-ttu-id="bf099-167">當您將組建排入佇列時，專案檔會從您在**OutputRoot**屬性中指定的組建放置資料夾，部署資料庫腳本和 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="bf099-167">When you queue the build, the project file will deploy the database scripts and web packages from the build drop folder you specified in the **OutputRoot** property.</span></span>

## <a name="conclusion"></a><span data-ttu-id="bf099-168">結論</span><span class="sxs-lookup"><span data-stu-id="bf099-168">Conclusion</span></span>

<span data-ttu-id="bf099-169">本主題描述如何使用「分割專案檔」部署模型，從特定的先前組建發行部署資源，例如 web 套件和資料庫腳本。</span><span class="sxs-lookup"><span data-stu-id="bf099-169">This topic described how to publish deployment resources, like web packages and database scripts, from a specific previous build using the split project file deployment model.</span></span> <span data-ttu-id="bf099-170">文中說明了如何覆寫**OutputRoot**屬性，以及如何將部署邏輯併入 TFS 組建定義中。</span><span class="sxs-lookup"><span data-stu-id="bf099-170">It explained how to override the **OutputRoot** property and how to incorporate the deployment logic into a TFS build definition.</span></span>

## <a name="further-reading"></a><span data-ttu-id="bf099-171">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="bf099-171">Further Reading</span></span>

<span data-ttu-id="bf099-172">如需建立組建定義的詳細資訊，請參閱[建立基本組建定義](https://msdn.microsoft.com/library/ms181716.aspx)和[定義您的組建進程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="bf099-172">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="bf099-173">如需佇列組建的詳細指引，請參閱[將組建](https://msdn.microsoft.com/library/ms181722.aspx)排入佇列。</span><span class="sxs-lookup"><span data-stu-id="bf099-173">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="bf099-174">[上一頁](creating-a-build-definition-that-supports-deployment.md)
> [下一頁](configuring-permissions-for-team-build-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="bf099-174">[Previous](creating-a-build-definition-that-supports-deployment.md)
[Next](configuring-permissions-for-team-build-deployment.md)</span></span>
