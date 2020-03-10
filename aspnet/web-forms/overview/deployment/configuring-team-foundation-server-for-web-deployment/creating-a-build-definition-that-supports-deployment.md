---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
title: 建立支援部署的組建定義 |Microsoft Docs
author: jrjlee
description: 如果您想要在 Team Foundation Server （TFS）2010中執行任何種類的組建，您必須在 Team 專案中建立組建定義。 本主題 des 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: fe47a018-f6d0-4979-80e7-5b1fa75a5865
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment
msc.type: authoredcontent
ms.openlocfilehash: e11c91a824446572aaf0b3bc6954b9b8ffb4eaff
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78603996"
---
# <a name="creating-a-build-definition-that-supports-deployment"></a><span data-ttu-id="c4f8e-104">建立支援部署的組建定義</span><span class="sxs-lookup"><span data-stu-id="c4f8e-104">Creating a Build Definition That Supports Deployment</span></span>

<span data-ttu-id="c4f8e-105">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="c4f8e-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="c4f8e-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="c4f8e-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="c4f8e-107">如果您想要在 Team Foundation Server （TFS）2010中執行任何種類的組建，您必須在 Team 專案中建立組建定義。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-107">If you want to perform any kind of build in Team Foundation Server (TFS) 2010, you need to create a build definition within your team project.</span></span> <span data-ttu-id="c4f8e-108">本主題描述如何在 TFS 中建立新的組建定義，以及如何控制 web 部署，做為 Team Build 中的組建流程的一部分。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-108">This topic describes how to create a new build definition in TFS and how to control web deployment as part of the build process in Team Build.</span></span>

<span data-ttu-id="c4f8e-109">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-109">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="c4f8e-110">這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建和部署程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-110">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="c4f8e-111">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-111">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="c4f8e-112">工作總覽</span><span class="sxs-lookup"><span data-stu-id="c4f8e-112">Task Overview</span></span>

<span data-ttu-id="c4f8e-113">組建定義是一種機制，可控制 TFS 中 team 專案的組建發生的方式和時機。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-113">A build definition is the mechanism that controls how and when builds occur for team projects in TFS.</span></span> <span data-ttu-id="c4f8e-114">每個組建定義都會指定：</span><span class="sxs-lookup"><span data-stu-id="c4f8e-114">Each build definition specifies:</span></span>

- <span data-ttu-id="c4f8e-115">您想要建立的專案，例如 Visual Studio 方案檔或自訂 Microsoft Build Engine （MSBuild）專案檔。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-115">The things you want to build, like Visual Studio solution files or custom Microsoft Build Engine (MSBuild) project files.</span></span>
- <span data-ttu-id="c4f8e-116">決定何時應進行組建的準則，例如手動觸發程式、持續整合（CI）或閘道簽入。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-116">The criteria that determine when a build should take place, like manual triggers, continuous integration (CI), or gated check-ins.</span></span>
- <span data-ttu-id="c4f8e-117">Team Build 應傳送組建輸出的位置，包括部署成品（例如 web 封裝和資料庫腳本）。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-117">The location to which Team Build should send build outputs, including deployment artifacts like web packages and database scripts.</span></span>
- <span data-ttu-id="c4f8e-118">每個組建應保留的時間量。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-118">The amount of time that each build should be retained.</span></span>
- <span data-ttu-id="c4f8e-119">組建進程的各種其他參數。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-119">Various other parameters of the build process.</span></span>

> [!NOTE]
> <span data-ttu-id="c4f8e-120">如需組建定義的詳細資訊，請參閱[定義您的組建進程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-120">For more information on build definitions, see [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span>

<span data-ttu-id="c4f8e-121">本主題將說明如何建立使用 CI 的組建定義，以便在開發人員簽入新內容時觸發組建。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-121">This topic will show you how to create a build definition that uses CI, so that a build is triggered when a developer checks in new content.</span></span> <span data-ttu-id="c4f8e-122">如果組建成功，組建服務會執行自訂專案檔，以將方案部署到測試環境。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-122">If the build succeeds, the build service runs a custom project file to deploy the solution to a test environment.</span></span>

<span data-ttu-id="c4f8e-123">當您觸發組建時，必須執行下列動作：</span><span class="sxs-lookup"><span data-stu-id="c4f8e-123">When you trigger a build, these actions need to happen:</span></span>

- <span data-ttu-id="c4f8e-124">首先，Team Build 應該建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-124">First, Team Build should build the solution.</span></span> <span data-ttu-id="c4f8e-125">在此程式中，Team Build 會叫用 Web 發行管線（WPP），為方案中的每個 web 應用程式專案產生 web 部署套件。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-125">As part of this process, Team Build will invoke the Web Publishing Pipeline (WPP) to generate web deployment packages for each of the web application projects in the solution.</span></span> <span data-ttu-id="c4f8e-126">Team Build 也會執行與方案相關聯的任何單元測試。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-126">Team Build will also run any unit tests associated with the solution.</span></span>
- <span data-ttu-id="c4f8e-127">如果解決方案組建失敗，則 Team Build 不應採取進一步的動作。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-127">If the solution build fails, Team Build should take no further action.</span></span> <span data-ttu-id="c4f8e-128">應該將單元測試失敗視為組建失敗。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-128">Unit test failures should be treated as a build failure.</span></span>
- <span data-ttu-id="c4f8e-129">如果解決方案組建成功，Team Build 應該執行自訂專案檔來控制方案的部署。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-129">If the solution build succeeds, Team Build should run the custom project file that controls the deployment of the solution.</span></span> <span data-ttu-id="c4f8e-130">在此程式中，Team Build 會叫用 Internet Information Services （IIS） Web 部署工具（Web Deploy），在目的地 Web 服務器上安裝已封裝的 web 應用程式，而且它將會叫用 VSDBCMD 公用程式來執行資料庫建立目的地資料庫伺服器上的腳本。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-130">As part of this process, Team Build will invoke the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) to install the packaged web applications on the destination web servers, and it will invoke the VSDBCMD.exe utility to run database creation scripts on the destination database servers.</span></span>

<span data-ttu-id="c4f8e-131">這會說明此程式：</span><span class="sxs-lookup"><span data-stu-id="c4f8e-131">This illustrates the process:</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image1.png)

<span data-ttu-id="c4f8e-132">[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)範例解決方案包含自訂 msbuild 專案檔（ *Publish*），您可以從 msbuild 或 Team Build 執行該檔案。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-132">The [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution includes a custom MSBuild project file, *Publish.proj*, that you can run from MSBuild or Team Build.</span></span> <span data-ttu-id="c4f8e-133">如[瞭解建立](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述，這個專案檔會定義將 web 封裝和資料庫部署至目標環境的邏輯。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-133">As described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), this project file defines the logic that deploys your web packages and databases to a target environment.</span></span> <span data-ttu-id="c4f8e-134">此檔案包含的邏輯會省略建立和封裝程式（如果它是在 Team Build 中執行），只留下要執行的部署工作。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-134">The file includes logic that omits the building and packaging process if it's running in Team Build, leaving just the deployment tasks to run.</span></span> <span data-ttu-id="c4f8e-135">這是因為當您以這種方式自動化部署時，通常會想要確保解決方案成功建立，並在部署程式開始之前傳遞任何單元測試。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-135">This is because when you automate deployment in this way, you'll typically want to ensure that the solution builds successfully and passes any unit tests before the deployment process commences.</span></span>

<span data-ttu-id="c4f8e-136">下一節將說明如何藉由建立新的組建定義來執行此程式。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-136">The next section explains how to implement this process by creating a new build definition.</span></span>

> [!NOTE]
> <span data-ttu-id="c4f8e-137">這&#x2014;項程式中，單一自動化進程建立、測試及部署解決方案&#x2014;可能最適合部署到測試環境。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-137">This procedure&#x2014;in which a single automated process builds, tests, and deploys a solution&#x2014;is likely to be most suited to deployment to test environments.</span></span> <span data-ttu-id="c4f8e-138">對於預備和生產環境，您很可能會想要從先前的組建部署內容，而您已經在測試環境中驗證和驗證。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-138">For staging and production environments you're a lot more likely to want to deploy content from a previous build that you've already verified and validated in a test environment.</span></span> <span data-ttu-id="c4f8e-139">這個方法會在下一個主題中說明如何[部署特定的組建](deploying-a-specific-build.md)。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-139">This approach is described in the next topic, [Deploying a Specific Build](deploying-a-specific-build.md).</span></span>

### <a name="who-performs-this-procedure"></a><span data-ttu-id="c4f8e-140">誰執行此程式？</span><span class="sxs-lookup"><span data-stu-id="c4f8e-140">Who Performs This Procedure?</span></span>

<span data-ttu-id="c4f8e-141">一般而言，TFS 系統管理員會執行此程式。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-141">Typically, a TFS administrator performs this procedure.</span></span> <span data-ttu-id="c4f8e-142">在某些情況下，開發人員小組領導人可能會負責 TFS 中的 team 專案集合。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-142">In some cases, a developer team leader may take responsibility for the team project collection in TFS.</span></span> <span data-ttu-id="c4f8e-143">若要建立新的組建定義，您必須是包含方案之 team 專案集合的 [**專案集合組建系統管理員**] 群組成員。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-143">In order to create a new build definition, you need to be a member of the **Project Collection Build Administrators** group for the team project collection that contains your solution.</span></span>

## <a name="create-a-build-definition-for-ci-and-deployment"></a><span data-ttu-id="c4f8e-144">建立 CI 和部署的組建定義</span><span class="sxs-lookup"><span data-stu-id="c4f8e-144">Create a Build Definition for CI and Deployment</span></span>

<span data-ttu-id="c4f8e-145">下一個程式描述如何建立 CI 觸發程式的組建定義。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-145">The next procedure describes how to create a build definition that CI triggers.</span></span> <span data-ttu-id="c4f8e-146">如果組建成功，則會使用自訂 MSBuild 專案檔中的邏輯來部署方案。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-146">If the build succeeds, the solution is deployed using the logic in a custom MSBuild project file.</span></span>

<span data-ttu-id="c4f8e-147">**建立 CI 和部署的組建定義**</span><span class="sxs-lookup"><span data-stu-id="c4f8e-147">**To create a build definition for CI and deployment**</span></span>

1. <span data-ttu-id="c4f8e-148">在 Visual Studio 2010 的 [ **Team Explorer** ] 視窗中，展開您的 Team 專案節點，以滑鼠右鍵按一下 [**組建**]，然後按一下 [**新增組建定義**]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-148">In Visual Studio 2010, in the **Team Explorer** window, expand your team project node, right-click **Builds**, and then click **New Build Definition**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image2.png)
2. <span data-ttu-id="c4f8e-149">在 [**一般**] 索引標籤上，提供組建定義的名稱（例如， **DeployToTest**）和選擇性描述。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-149">On the **General** tab, give the build definition a name (for example, **DeployToTest**) and an optional description.</span></span>
3. <span data-ttu-id="c4f8e-150">在 [**觸發**程式] 索引標籤上，選取您想要觸發新組建的準則。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-150">On the **Trigger** tab, select the criteria on which you want to trigger a new build.</span></span> <span data-ttu-id="c4f8e-151">例如，如果您想要建立方案，並在每次開發人員簽入新程式碼時部署至測試環境，請選取 [**持續整合**]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-151">For example, if you want to build the solution and deploy to the test environment every time a developer checks in new code, select **Continuous Integration**.</span></span>
4. <span data-ttu-id="c4f8e-152">在 [**組建預設值**] 索引標籤的 [**將組建輸出複製到下列放置資料夾**] 方塊中，輸入放置資料夾的通用命名慣例（UNC）路徑（例如， **\\TFSBUILD\Drops**）。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-152">On the **Build Defaults** tab, in the **Copy build output to the following drop folder** box, type the Universal Naming Convention (UNC) path of your drop folder (for example, **\\TFSBUILD\Drops**).</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image3.png)

    > [!NOTE]
    > <span data-ttu-id="c4f8e-153">這個放置位置會儲存數個組建，視您設定的保留原則而定。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-153">This drop location stores several builds, depending on the retention policy you configure.</span></span> <span data-ttu-id="c4f8e-154">當您想要從特定組建將部署成品發佈至預備或生產環境時，您可以在這裡找到這些專案。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-154">When you want to publish deployment artifacts from a specific build to a staging or production environment, this is where you'll find them.</span></span>
5. <span data-ttu-id="c4f8e-155">在 [**流程**] 索引標籤的 [**建立**程式檔案] 下拉式清單中，將 [ **defaulttemplate.xaml** ] 保留為已選取。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-155">On the **Process** tab, in the **Build process file** dropdown list, leave **DefaultTemplate.xaml** selected.</span></span> <span data-ttu-id="c4f8e-156">這是新增至所有新 team 專案的其中一個預設組建流程範本。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-156">This is one of the default build process templates that get added to all new team projects.</span></span>
6. <span data-ttu-id="c4f8e-157">在 [**建立流程參數**] 資料表中，按一下 [**要建立的專案**] 資料列，然後按一下**省略號**按鈕。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-157">In the **Build process parameters** table, click in the **Items to Build** row, and then click the **ellipsis** button.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image4.png)
7. <span data-ttu-id="c4f8e-158">在 [**要建立的專案**] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-158">In the **Items to Build** dialog box, click **Add**.</span></span>
8. <span data-ttu-id="c4f8e-159">流覽至方案檔的位置，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-159">Browse to the location of your solution file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image5.png)
9. <span data-ttu-id="c4f8e-160">在 [**要建立的專案**] 對話方塊中，按一下 [**新增**]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-160">In the **Items to Build** dialog box, click **Add**.</span></span>
10. <span data-ttu-id="c4f8e-161">在 [**類型的專案**] 下拉式清單中，選取 [ **MSBuild 專案**檔]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-161">In the **Items of type** dropdown list, select **MSBuild Project files**.</span></span>
11. <span data-ttu-id="c4f8e-162">流覽至您用來控制部署程式的自訂專案檔位置，選取該檔案，然後按一下 **[確定]** 。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-162">Browse to the location of the custom project file with which you control the deployment process, select the file, and then click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image6.png)
12. <span data-ttu-id="c4f8e-163">[**要建立的專案**] 對話方塊現在應該會顯示兩個專案。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-163">The **Items to Build** dialog box should now show two items.</span></span> <span data-ttu-id="c4f8e-164">按一下 [確定]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-164">Click **OK**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image7.png)
13. <span data-ttu-id="c4f8e-165">在 [**流程**] 索引標籤的 [**建立流程參數**] 資料表中，展開 [ **Advanced** ] 區段。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-165">On the **Process** tab, in the **Build process parameters** table, expand the **Advanced** section.</span></span>
14. <span data-ttu-id="c4f8e-166">在 [ **MSBuild 引數**] 資料列中，加入任何*一個*要建立之專案所需的 MSBuild 命令列引數。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-166">In the **MSBuild Arguments** row, add any MSBuild command-line arguments that *either* of your items to build requires.</span></span> <span data-ttu-id="c4f8e-167">在 Contact Manager 解決方案案例中，這些引數是必要的：</span><span class="sxs-lookup"><span data-stu-id="c4f8e-167">In the Contact Manager solution scenario, these arguments are required:</span></span>

    [!code-console[Main](creating-a-build-definition-that-supports-deployment/samples/sample1.cmd)]

    ![](creating-a-build-definition-that-supports-deployment/_static/image8.png)
15. <span data-ttu-id="c4f8e-168">在這個範例中：</span><span class="sxs-lookup"><span data-stu-id="c4f8e-168">In this example:</span></span>

    1. <span data-ttu-id="c4f8e-169">當您建立 Contact Manager 方案時，需要**DeployOnBuild = true**和**DeployTarget = package**引數。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-169">The **DeployOnBuild=true** and **DeployTarget=package** arguments are required when you build the Contact Manager solution.</span></span> <span data-ttu-id="c4f8e-170">這會指示 MSBuild 在建立每個 web 應用程式專案之後建立 web 部署封裝，如[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)中所述。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-170">This instructs MSBuild to create web deployment packages after building each web application project, as described in [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span>
    2. <span data-ttu-id="c4f8e-171">當您建立*Publish*檔案時，需要**TargetEnvPropsFile**引數。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-171">The **TargetEnvPropsFile** argument is required when you build the *Publish.proj* file.</span></span> <span data-ttu-id="c4f8e-172">此屬性工作表示環境特定設定檔案的位置，如[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-172">This property indicates the location of the environment-specific configuration file, as described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>
16. <span data-ttu-id="c4f8e-173">在 [**保留原則**] 索引標籤上，設定您想要保留多少個類型的組建，視需要而定。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-173">On the **Retention Policy** tab, configure how many builds of each type you want to retain as required.</span></span>
17. <span data-ttu-id="c4f8e-174">按一下 [儲存]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-174">Click **Save**.</span></span>

## <a name="queue-a-build"></a><span data-ttu-id="c4f8e-175">將組建排入佇列</span><span class="sxs-lookup"><span data-stu-id="c4f8e-175">Queue a Build</span></span>

<span data-ttu-id="c4f8e-176">此時，您已建立至少一個新的組建定義。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-176">At this point, you have created at least one new build definition.</span></span> <span data-ttu-id="c4f8e-177">您定義的組建進程現在會根據您在組建定義中指定的觸發程式來執行。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-177">The build process you defined will now run according to the triggers you specified in the build definition.</span></span>

<span data-ttu-id="c4f8e-178">如果您已將組建定義設定為使用 CI，您可以透過兩種方式來測試組建定義：</span><span class="sxs-lookup"><span data-stu-id="c4f8e-178">If you've configured your build definition to use CI, you can test your build definition in two ways:</span></span>

- <span data-ttu-id="c4f8e-179">將某些內容簽入 team 專案，以觸發自動組建。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-179">Check in some content to the team project to trigger an automatic build.</span></span>
- <span data-ttu-id="c4f8e-180">手動將組建排到佇列。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-180">Queue a build manually.</span></span>

<span data-ttu-id="c4f8e-181">**手動將組建排入佇列**</span><span class="sxs-lookup"><span data-stu-id="c4f8e-181">**To queue a build manually**</span></span>

1. <span data-ttu-id="c4f8e-182">在 [ **Team Explorer** ] 視窗中，以滑鼠右鍵按一下組建定義，然後按一下 [將**新組建**排入佇列]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-182">In the **Team Explorer** window, right-click the build definition, and then click **Queue New Build**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image9.png)
2. <span data-ttu-id="c4f8e-183">在 [**佇列組建**] 對話方塊中，檢查組建屬性，然後按一下 [**佇列**]。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-183">In the **Queue Build** dialog box, review the build properties, and then click **Queue**.</span></span>

    ![](creating-a-build-definition-that-supports-deployment/_static/image10.png)

<span data-ttu-id="c4f8e-184">若要檢查組建&#x2014;的進度和結果，不論其是否已手動觸發，或在 [&#x2014; **Team Explorer** ] 視窗中自動按兩下組建定義。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-184">To review the progress and the outcome of a build&#x2014;regardless of whether it was triggered manually or automatically&#x2014;double-click the build definition in the **Team Explorer** window.</span></span> <span data-ttu-id="c4f8e-185">這會開啟 [**組建瀏覽器**] 索引標籤。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-185">This will open a **Build Explorer** tab.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image11.png)

<span data-ttu-id="c4f8e-186">從這裡，您可以針對失敗的組建進行疑難排解。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-186">From here, you can troubleshoot failed builds.</span></span> <span data-ttu-id="c4f8e-187">如果您按兩下個別的組建，您可以查看摘要資訊，並按一下以列出詳細的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-187">If you double-click an individual build, you can view summary information and click through to detailed log files.</span></span>

![](creating-a-build-definition-that-supports-deployment/_static/image12.png)

<span data-ttu-id="c4f8e-188">您可以使用這份資訊來疑難排解失敗的組建，並解決任何問題，再嘗試另一個組建。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-188">You can use this information to troubleshoot failed builds and address any problems before you attempt another build.</span></span>

> [!NOTE]
> <span data-ttu-id="c4f8e-189">除非您已將目的地環境中所需的任何許可權授與組建伺服器，否則執行部署邏輯的組建可能會失敗。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-189">Builds that execute deployment logic are likely to fail until you have granted the build server any permissions required in the destination environment.</span></span> <span data-ttu-id="c4f8e-190">如需詳細資訊，請參閱設定[Team Build 部署的許可權](configuring-permissions-for-team-build-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-190">For more information, see [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span>

## <a name="monitor-the-build-process"></a><span data-ttu-id="c4f8e-191">監視組建進程</span><span class="sxs-lookup"><span data-stu-id="c4f8e-191">Monitor the Build Process</span></span>

<span data-ttu-id="c4f8e-192">TFS 提供各種功能，可協助您監視組建程式。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-192">TFS provides a broad range of functionality to help you monitor the build process.</span></span> <span data-ttu-id="c4f8e-193">例如，TFS 可以在組建完成時，傳送電子郵件給您，或在工作列通知區域中顯示警示。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-193">For example, TFS can send you an email or display alerts in your taskbar notification area when a build has completed.</span></span> <span data-ttu-id="c4f8e-194">如需詳細資訊，請參閱[執行和監視組建](https://msdn.microsoft.com/library/ms181721.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-194">For more information, see [Run and Monitor Builds](https://msdn.microsoft.com/library/ms181721.aspx).</span></span>

## <a name="conclusion"></a><span data-ttu-id="c4f8e-195">結論</span><span class="sxs-lookup"><span data-stu-id="c4f8e-195">Conclusion</span></span>

<span data-ttu-id="c4f8e-196">本主題說明如何在 TFS 中建立組建定義。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-196">This topic described how to create a build definition in TFS.</span></span> <span data-ttu-id="c4f8e-197">組建定義是針對 CI 設定的，因此每當開發人員將內容簽入 team 專案時，就會執行組建程式。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-197">The build definition is configured for CI, so the build process runs whenever a developer checks in content to the team project.</span></span> <span data-ttu-id="c4f8e-198">組建定義會執行自訂的 MSBuild 專案檔，將 web 封裝和資料庫腳本部署到目標伺服器環境。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-198">The build definition executes a custom MSBuild project file to deploy web packages and database scripts to a target server environment.</span></span>

<span data-ttu-id="c4f8e-199">為了讓自動化部署成功成為組建程式的一部分，您必須在目標 web 伺服器和目標資料庫伺服器上，將適當的許可權授與組建服務帳戶。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-199">In order for an automated deployment to succeed as part of a build process, you'll need to grant appropriate permissions to the build service account on the target web servers and the target database server.</span></span> <span data-ttu-id="c4f8e-200">本教學課程中的最後一個主題是設定[Team Build 部署的許可權](configuring-permissions-for-team-build-deployment.md)，描述如何識別並設定從 Team build 伺服器進行自動化部署所需的許可權。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-200">The final topic in this tutorial, [Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md), describes how to identify and configure the permissions required for automated deployment from a Team Build server.</span></span>

## <a name="further-reading"></a><span data-ttu-id="c4f8e-201">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="c4f8e-201">Further Reading</span></span>

<span data-ttu-id="c4f8e-202">如需建立組建定義的詳細資訊，請參閱[建立基本組建定義](https://msdn.microsoft.com/library/ms181716.aspx)和[定義您的組建進程](https://msdn.microsoft.com/library/ms181715.aspx)。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-202">For more information on creating build definitions, see [Create a Basic Build Definition](https://msdn.microsoft.com/library/ms181716.aspx) and [Define Your Build Process](https://msdn.microsoft.com/library/ms181715.aspx).</span></span> <span data-ttu-id="c4f8e-203">如需佇列組建的詳細指引，請參閱[將組建](https://msdn.microsoft.com/library/ms181722.aspx)排入佇列。</span><span class="sxs-lookup"><span data-stu-id="c4f8e-203">For more guidance on queuing builds, see [Queue a Build](https://msdn.microsoft.com/library/ms181722.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="c4f8e-204">[上一頁](configuring-a-tfs-build-server-for-web-deployment.md)
> [下一頁](deploying-a-specific-build.md)</span><span class="sxs-lookup"><span data-stu-id="c4f8e-204">[Previous](configuring-a-tfs-build-server-for-web-deployment.md)
[Next](deploying-a-specific-build.md)</span></span>
