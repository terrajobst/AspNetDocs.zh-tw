---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 建立和執行部署命令檔 |Microsoft Docs
author: jrjlee
description: 本主題描述如何建立命令檔，讓您使用 Microsoft Build Engine （MSBuild）專案檔以單一步驟執行部署，然後重新 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634306"
---
# <a name="creating-and-running-a-deployment-command-file"></a><span data-ttu-id="4e1e6-103">建立及執行部署命令檔</span><span class="sxs-lookup"><span data-stu-id="4e1e6-103">Creating and Running a Deployment Command File</span></span>

<span data-ttu-id="4e1e6-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="4e1e6-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="4e1e6-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="4e1e6-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="4e1e6-106">本主題描述如何建立命令檔，讓您使用 Microsoft Build Engine （MSBuild）專案檔，以單一步驟、可重複的程式執行部署。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-106">This topic describes how to build a command file that will let you run a deployment using Microsoft Build Engine (MSBuild) project files as a single-step, repeatable process.</span></span>

<span data-ttu-id="4e1e6-107">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager](the-contact-manager-solution.md)解決方案&#x2014;的範例解決方案，來代表具有實際複雜度層級的 WEB 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-107">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="4e1e6-108">這些教學課程中的部署方法是以[瞭解組建](understanding-the-build-process.md)程式中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案檔所控制&#x2014;，其中一個包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-108">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="4e1e6-109">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-109">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="process-overview"></a><span data-ttu-id="4e1e6-110">程序概觀</span><span class="sxs-lookup"><span data-stu-id="4e1e6-110">Process Overview</span></span>

<span data-ttu-id="4e1e6-111">在本主題中，您將瞭解如何建立及執行命令檔，以使用這些專案檔對目標環境執行可重複的部署。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-111">In this topic, you'll learn how to create and run a command file that uses these project files to perform a repeatable deployment to your target environment.</span></span> <span data-ttu-id="4e1e6-112">基本上，命令檔只需要包含 MSBuild 命令，它會：</span><span class="sxs-lookup"><span data-stu-id="4e1e6-112">Essentially, the command file simply needs to contain an MSBuild command that:</span></span>

- <span data-ttu-id="4e1e6-113">告訴 MSBuild 執行與環境無關的*Publish*檔案。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-113">Tells MSBuild to execute the environment-agnostic *Publish.proj* file.</span></span>
- <span data-ttu-id="4e1e6-114">告訴*Publish*檔案，其中包含環境特定的專案設定以及要在哪裡尋找。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-114">Tells the *Publish.proj* file which file contains the environment-specific project settings and where to find it.</span></span>

## <a name="create-an-msbuild-command"></a><span data-ttu-id="4e1e6-115">建立 MSBuild 命令</span><span class="sxs-lookup"><span data-stu-id="4e1e6-115">Create an MSBuild Command</span></span>

<span data-ttu-id="4e1e6-116">如[瞭解組建](understanding-the-build-process.md)程式中所述，環境特定的專案&#x2014;檔（例如， *Env-Dev*&#x2014;）是設計成要在組建時匯入到與環境無關的*Publish*檔案中。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-116">As described in [Understanding the Build Process](understanding-the-build-process.md), the environment-specific project file&#x2014;for example, *Env-Dev.proj*&#x2014;is designed to be imported into the environment-agnostic *Publish.proj* file at build time.</span></span> <span data-ttu-id="4e1e6-117">這兩個檔案一起提供一組完整的指示，告訴 MSBuild 如何建立和部署您的解決方案。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-117">Together, these two files provide a complete set of instructions that tell MSBuild how to build and deploy your solution.</span></span>

<span data-ttu-id="4e1e6-118">*Publish*檔案會使用**import**元素來匯入環境特定的專案檔。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-118">The *Publish.proj* file uses an **Import** element to import the environment-specific project file.</span></span>

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

<span data-ttu-id="4e1e6-119">因此，當您使用 Msbuild.exe 來建立及部署 Contact Manager 解決方案時，您必須：</span><span class="sxs-lookup"><span data-stu-id="4e1e6-119">As such, when you use MSBuild.exe to build and deploy the Contact Manager solution, you need to:</span></span>

- <span data-ttu-id="4e1e6-120">在*Publish*檔案上執行 msbuild.exe。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-120">Run MSBuild.exe on the *Publish.proj* file.</span></span>
- <span data-ttu-id="4e1e6-121">藉由提供名為**TargetEnvPropsFile**的命令列參數，指定環境特定專案檔的位置。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-121">Specify the location of the environment-specific project file by supplying a command-line parameter named **TargetEnvPropsFile**.</span></span>

<span data-ttu-id="4e1e6-122">若要這麼做，您的 MSBuild 命令應如下所示：</span><span class="sxs-lookup"><span data-stu-id="4e1e6-122">To do this, your MSBuild command should resemble this:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

<span data-ttu-id="4e1e6-123">從這裡開始，是移至可重複的單一步驟部署的簡單步驟。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-123">From here, it's a simple step to move to a repeatable, single-step deployment.</span></span> <span data-ttu-id="4e1e6-124">您只需要將 MSBuild 命令新增至 .cmd 檔案就可以了。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-124">All you need to do is to add your MSBuild command to a .cmd file.</span></span> <span data-ttu-id="4e1e6-125">在 Contact Manager 解決方案中，Publish 資料夾包含名為*Publish-Dev*的檔案，它會確實執行此工作。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-125">In the Contact Manager solution, the Publish folder includes a file named *Publish-Dev.cmd* that does exactly this.</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="4e1e6-126">**/Fl**參數會指示 msbuild 在用來叫用 msbuild.exe 的工作目錄中，建立名為*msbuild.exe*的記錄檔。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-126">The **/fl** switch instructs MSBuild to create a log file named *msbuild.log* in the working directory in which MSBuild.exe was invoked.</span></span>

<span data-ttu-id="4e1e6-127">若要部署或重新部署 Contact Manager 解決方案，您只需要執行*Publish-Dev .cmd*檔案。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-127">To deploy or redeploy the Contact Manager solution, all you need to do is run the *Publish-Dev.cmd* file.</span></span> <span data-ttu-id="4e1e6-128">當您執行檔案時，MSBuild 將會：</span><span class="sxs-lookup"><span data-stu-id="4e1e6-128">When you run the file, MSBuild will:</span></span>

- <span data-ttu-id="4e1e6-129">建立方案中的所有專案。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-129">Build all the projects in the solution.</span></span>
- <span data-ttu-id="4e1e6-130">為 web 應用程式專案產生可部署的 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-130">Generate deployable web packages for the web application projects.</span></span>
- <span data-ttu-id="4e1e6-131">為資料庫專案產生 .dbschema 和. deploymanifest 檔案。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-131">Generate .dbschema and .deploymanifest files for the database projects.</span></span>
- <span data-ttu-id="4e1e6-132">將 web 套件部署到 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-132">Deploy the web packages to the web server.</span></span>
- <span data-ttu-id="4e1e6-133">將資料庫部署到資料庫伺服器。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-133">Deploy the database to the database server.</span></span>

## <a name="run-the-deployment"></a><span data-ttu-id="4e1e6-134">執行部署</span><span class="sxs-lookup"><span data-stu-id="4e1e6-134">Run the Deployment</span></span>

<span data-ttu-id="4e1e6-135">當您已建立目標環境的命令檔時，您應該只要執行檔案就可以完成整個部署。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-135">When you've created a command file for your target environment, you should be able to complete the entire deployment by simply running the file.</span></span>

<span data-ttu-id="4e1e6-136">**將 Contact Manager 解決方案部署至您的測試環境**</span><span class="sxs-lookup"><span data-stu-id="4e1e6-136">**To deploy the Contact Manager solution to your test environment**</span></span>

1. <span data-ttu-id="4e1e6-137">在開發人員工作站上，開啟 Windows Explorer，然後流覽至*Publish-Dev*檔案的位置。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-137">On your developer workstation, open Windows Explorer, and then browse to the location of the *Publish-Dev.cmd* file.</span></span>
2. <span data-ttu-id="4e1e6-138">按兩下檔案加以執行。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-138">Double-click the file to run it.</span></span>
3. <span data-ttu-id="4e1e6-139">如果出現 [**開啟檔案-安全性警告**] 對話方塊，請按一下 [**執行**]。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-139">If an **Open File – Security Warning** dialog box appears, click **Run**.</span></span>
4. <span data-ttu-id="4e1e6-140">如果您的設定和測試伺服器設定正確，當 MSBuild 完成處理專案檔時，[命令提示字元] 視窗會顯示**組建成功**訊息。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-140">If your configuration settings and test servers are set up correctly, the Command Prompt window will show a **Build succeeded** message when MSBuild has finished processing the project files.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. <span data-ttu-id="4e1e6-141">如果這是您第一次將解決方案部署到此環境，您將需要將測試 web 伺服器電腦帳戶新增至**ContactManager**資料庫上的**db\_資料寫入元**和**db\_datareader**角色。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-141">If this is the first time you've deployed the solution to this environment, you'll need to add the test web server machine account to the **db\_datawriter** and **db\_datareader** roles on the **ContactManager** database.</span></span> <span data-ttu-id="4e1e6-142">[設定用於 Web Deploy 發佈的資料庫伺服器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)中會描述此程式。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-142">This procedure is described in [Configure a Database Server for Web Deploy Publishing](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md).</span></span>

    > [!NOTE]
    > <span data-ttu-id="4e1e6-143">當您建立資料庫時，您只需要指派這些許可權。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-143">You only need to assign these permissions when you create the database.</span></span> <span data-ttu-id="4e1e6-144">根據預設，組建程式不會在每個部署&#x2014;上重新建立資料庫，而是會將現有的資料庫與最新的架構進行比較，並只進行所需的變更。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-144">By default, the build process will not recreate the database on every deployment&#x2014;instead, it will compare the existing database to the latest schema and make only the changes required.</span></span> <span data-ttu-id="4e1e6-145">因此，您應該只在第一次部署解決方案時，才需要對應這些資料庫角色。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-145">As a result, you should only need to map these database roles the first time you deploy the solution.</span></span>
6. <span data-ttu-id="4e1e6-146">開啟 Internet Explorer 並流覽至 Contact Manager 應用程式的 URL （例如，`http://testweb1:85/ContactManager/`）。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-146">Open Internet Explorer and browse to the URL of the Contact Manager application (for example, `http://testweb1:85/ContactManager/`).</span></span>
7. <span data-ttu-id="4e1e6-147">確認應用程式如預期般運作，而且您能夠新增連絡人。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-147">Verify that the application works as expected and you're able to add contacts.</span></span>

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a><span data-ttu-id="4e1e6-148">結論</span><span class="sxs-lookup"><span data-stu-id="4e1e6-148">Conclusion</span></span>

<span data-ttu-id="4e1e6-149">建立包含 MSBuild 指示的命令檔，可讓您快速且輕鬆地建立多專案方案，並將其部署到特定的目的地環境。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-149">Creating a command file containing your MSBuild instructions provides you with a quick and easy way of building and deploying a multi-project solution to a specific destination environment.</span></span> <span data-ttu-id="4e1e6-150">如果您需要將解決方案重複部署至多個目的地環境，可以建立多個命令檔。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-150">If you need to repeatedly deploy your solution to multiple destination environments, you can create multiple command files.</span></span> <span data-ttu-id="4e1e6-151">在每個命令檔中，MSBuild 命令會建立相同的通用專案檔，但它會指定不同的環境特定專案檔案。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-151">In each command file, the MSBuild command will build the same universal project file, but it will specify a different environment-specific project file.</span></span> <span data-ttu-id="4e1e6-152">例如，要發行至開發人員或測試環境的命令檔可能包含此 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="4e1e6-152">For example, a command file to publish to a developer or test environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

<span data-ttu-id="4e1e6-153">發行至預備環境的命令檔可能包含此 MSBuild 命令：</span><span class="sxs-lookup"><span data-stu-id="4e1e6-153">A command file to publish to a staging environment might contain this MSBuild command:</span></span>

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> <span data-ttu-id="4e1e6-154">如需如何為您自己的伺服器環境自訂環境特定專案檔案的指引，請參閱設定[目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-154">For guidance on how to customize the environment-specific project files for your own server environments, see [Configure Deployment Properties for a Target Environment](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md).</span></span>

<span data-ttu-id="4e1e6-155">您也可以在 MSBuild 命令中覆寫屬性或設定各種其他參數，以自訂每個環境的組建程式。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-155">You can also customize the build process for each environment by overriding properties or setting various other switches in your MSBuild command.</span></span> <span data-ttu-id="4e1e6-156">如需詳細資訊，請參閱[MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311.aspx)。</span><span class="sxs-lookup"><span data-stu-id="4e1e6-156">For more information, see [MSBuild Command Line Reference](https://msdn.microsoft.com/library/ms164311.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="4e1e6-157">[上一頁](deploying-database-projects.md)
> [下一頁](manually-installing-web-packages.md)</span><span class="sxs-lookup"><span data-stu-id="4e1e6-157">[Previous](deploying-database-projects.md)
[Next](manually-installing-web-packages.md)</span></span>
