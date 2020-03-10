---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: 執行 What If 部署 |Microsoft Docs
author: jrjlee
description: 本主題描述如何使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）和 V ... 來執行「假設」（或模擬）部署
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628888"
---
# <a name="performing-a-what-if-deployment"></a><span data-ttu-id="1e9a9-103">執行 "What If" 部署</span><span class="sxs-lookup"><span data-stu-id="1e9a9-103">Performing a "What If" Deployment</span></span>

<span data-ttu-id="1e9a9-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="1e9a9-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="1e9a9-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="1e9a9-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="1e9a9-106">本主題描述如何使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）和 VSDBCMD 來執行「假設」（或模擬）部署。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-106">This topic describes how to perform "what if" (or simulated) deployments using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) and VSDBCMD.</span></span> <span data-ttu-id="1e9a9-107">這可讓您在實際部署應用程式之前，判斷部署邏輯在特定目標環境上的效果。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-107">This lets you determine the effects of your deployment logic on a particular target environment before you actually deploy your application.</span></span>

<span data-ttu-id="1e9a9-108">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-108">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="1e9a9-109">這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建和部署程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-109">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build and deployment process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="1e9a9-110">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-110">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="performing-a-what-if-deployment-for-web-packages"></a><span data-ttu-id="1e9a9-111">執行 Web 套件的「What If」部署</span><span class="sxs-lookup"><span data-stu-id="1e9a9-111">Performing a "What If" Deployment for Web Packages</span></span>

<span data-ttu-id="1e9a9-112">Web Deploy 包含的功能可讓您在「假設」（或試用）模式中執行部署。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-112">Web Deploy includes functionality that lets you perform deployments in "what if" (or trial) mode.</span></span> <span data-ttu-id="1e9a9-113">當您以「假設」模式部署成品時，Web Deploy 會產生記錄檔，如同您已執行部署，但它實際上不會變更目的地伺服器上的任何專案。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-113">When you deploy artifacts in "what if" mode, Web Deploy generates a log file as if you had performed the deployment, but it doesn't actually change anything on the destination server.</span></span> <span data-ttu-id="1e9a9-114">查看記錄檔可協助您瞭解部署在目的地伺服器上的影響，特別是：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-114">Reviewing the log file can help you to understand what impact your deployment will have on the destination server, in particular:</span></span>

- <span data-ttu-id="1e9a9-115">將新增哪些內容。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-115">What will get added.</span></span>
- <span data-ttu-id="1e9a9-116">會更新哪些內容。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-116">What will get updated.</span></span>
- <span data-ttu-id="1e9a9-117">將刪除的內容。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-117">What will get deleted.</span></span>

<span data-ttu-id="1e9a9-118">由於「假設」部署實際上不會變更目的地伺服器上的任何專案，因此不一定會預測部署是否會成功。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-118">Because a "what if" deployment doesn't actually change anything on the destination server, what it can't always do is predict whether a deployment will succeed.</span></span>

<span data-ttu-id="1e9a9-119">如[部署 Web 套件](../web-deployment-in-the-enterprise/deploying-web-packages.md)中所述，您可以透過兩種方式&#x2014;使用 Web Deploy 部署 web 封裝，方法是直接使用 msdeploy.exe 命令列公用程式，或執行組建程式所產生的 *.deploy .cmd*檔案。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-119">As described in [Deploying Web Packages](../web-deployment-in-the-enterprise/deploying-web-packages.md), you can deploy web packages using Web Deploy in two ways&#x2014;by using the MSDeploy.exe command-line utility directly or by running the *.deploy.cmd* file that the build process generates.</span></span>

<span data-ttu-id="1e9a9-120">如果您直接使用 Msdeploy.exe，可以將 **– whatif**旗標新增至您的命令，以執行「假設」部署。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-120">If you're using MSDeploy.exe directly, you can run a "what if" deployment by adding the **–whatif** flag to your command.</span></span> <span data-ttu-id="1e9a9-121">例如，若要評估在將 ContactManager 部署至預備環境時，會發生什麼情況，請使用 Msdeploy.exe 命令，如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-121">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package to a staging environment, the MSDeploy command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

<span data-ttu-id="1e9a9-122">當您滿意「假設」部署的結果時，您可以移除 **– whatif**旗標來執行即時部署。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-122">When you're satisfied with the results of your "what if" deployment, you can remove the **–whatif** flag to run a live deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="1e9a9-123">如需有關 Msdeploy.exe 之命令列選項的詳細資訊，請參閱[Web Deploy 作業設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-123">For more information on command-line options for MSDeploy.exe, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span>

<span data-ttu-id="1e9a9-124">如果您使用的是 *.deploy*檔案，您可以在命令中包含 **/t**旗標（試用模式）旗標，而不是 **/y**旗標（[是] 或 [更新模式]）來執行「假設」部署。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-124">If you're using the *.deploy.cmd* file, you can run a "what if" deployment by including the **/t** flag (trial mode) flag instead of the **/y** flag ("yes," or update mode) in your command.</span></span> <span data-ttu-id="1e9a9-125">例如，若要評估當您執行 *.deploy*檔案部署 ContactManager 封裝時，會發生什麼情況，您的命令應該如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-125">For example, to evaluate what would happen if you deployed the ContactManager.Mvc.zip package by running the *.deploy.cmd* file, your command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

<span data-ttu-id="1e9a9-126">當您滿意「試用模式」部署的結果時，您可以使用 **/y**旗標來取代 **/t**旗標，以執行即時部署：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-126">When you're satisfied with the results of your "trial mode" deployment, you can replace the **/t** flag with a **/y** flag to run a live deployment:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> <span data-ttu-id="1e9a9-127">如需有關之命令列*選項的詳細*資訊，請參閱[如何：使用 Deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-127">For more information on command-line options for *.deploy.cmd* files, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="1e9a9-128">如果您執行 *.deploy*檔案，但未指定任何旗標，則命令提示字元會顯示可用的旗標清單。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-128">If you run the *.deploy.cmd* file without specifying any flags, the command prompt will display a list of available flags.</span></span>

## <a name="performing-a-what-if-deployment-for-databases"></a><span data-ttu-id="1e9a9-129">執行資料庫的「What If」部署</span><span class="sxs-lookup"><span data-stu-id="1e9a9-129">Performing a "What If" Deployment for Databases</span></span>

<span data-ttu-id="1e9a9-130">本節假設您使用 VSDBCMD 公用程式來執行以架構為基礎的累加式資料庫部署。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-130">This section assumes that you're using the VSDBCMD utility to perform incremental, schema-based database deployment.</span></span> <span data-ttu-id="1e9a9-131">[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)中會更詳細地說明此方法。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-131">This approach is described in more detail in [Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md).</span></span> <span data-ttu-id="1e9a9-132">我們建議您先熟悉本主題，再套用這裡所述的概念。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-132">We recommend that you familiarize yourself with this topic before you apply the concepts described here.</span></span>

<span data-ttu-id="1e9a9-133">當您在**部署**模式中使用 VSDBCMD 時，您可以使用 **/Dd** （或 **/DeployToDatabase**）旗標來控制 VSDBCMD 是否實際部署資料庫，或只產生部署腳本。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-133">When you use VSDBCMD in **Deploy** mode, you can use the **/dd** (or **/DeployToDatabase**) flag to control whether VSDBCMD actually deploys the database or just generates a deployment script.</span></span> <span data-ttu-id="1e9a9-134">如果您要部署 .dbschema 檔案，此行為如下：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-134">If you're deploying a .dbschema file, this is the behavior:</span></span>

- <span data-ttu-id="1e9a9-135">如果您指定 **/dd +** 或 **/dd**，VSDBCMD 會產生部署腳本並部署資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-135">If you specify **/dd+** or **/dd**, VSDBCMD will generate a deployment script and deploy the database.</span></span>
- <span data-ttu-id="1e9a9-136">如果您指定 **/dd-** 或省略參數，VSDBCMD 只會產生部署腳本。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-136">If you specify **/dd-** or omit the switch, VSDBCMD will generate a deployment script only.</span></span>

> [!NOTE]
> <span data-ttu-id="1e9a9-137">如果您部署的是 deploymanifest 檔案，而不是 .dbschema 檔案， **/dd**參數的行為就會變得更複雜。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-137">If you're deploying a .deploymanifest file rather than a .dbschema file, the behavior of the **/dd** switch is a lot more complicated.</span></span> <span data-ttu-id="1e9a9-138">基本上，如果 deploymanifest 檔案包含值為**True**的**DeployToDatabase**元素，則 VSDBCMD 會忽略 **/dd**參數的值。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-138">Essentially, VSDBCMD will ignore the value of the **/dd** switch if the .deploymanifest file includes a **DeployToDatabase** element with a value of **True**.</span></span> <span data-ttu-id="1e9a9-139">[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)會完整描述此行為。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-139">[Deploying Database Projects](../web-deployment-in-the-enterprise/deploying-database-projects.md) describes this behavior in full.</span></span>

<span data-ttu-id="1e9a9-140">例如，若要產生**ContactManager**資料庫的部署腳本，而不實際部署資料庫，您的 VSDBCMD 命令應如下所示：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-140">For example, to generate a deployment script for the **ContactManager** database without actually deploying the database, your VSDBCMD command should resemble this:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

<span data-ttu-id="1e9a9-141">VSDBCMD 是差異資料庫部署工具，因此部署腳本會以動態方式產生，以包含將目前資料庫（如果有的話）更新為指定的架構所需的所有 SQL 命令。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-141">VSDBCMD is a differential database deployment tool, and as such the deployment script is dynamically generated to contain all the SQL commands necessary to update the current database, if one exists, to the specified schema.</span></span> <span data-ttu-id="1e9a9-142">檢查部署腳本是一種實用的方法，可判斷您的部署對目前資料庫及其包含的資料有何影響。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-142">Reviewing the deployment script is a useful way to determine what impact your deployment will have on the current database and the data it contains.</span></span> <span data-ttu-id="1e9a9-143">例如，您可能會想要判斷：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-143">For example, you might want to determine:</span></span>

- <span data-ttu-id="1e9a9-144">是否將移除任何現有的資料表，以及是否會導致資料遺失。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-144">Whether any existing tables will be removed, and whether that will result in data loss.</span></span>
- <span data-ttu-id="1e9a9-145">作業的順序是否會造成資料遺失的風險，例如，如果您正在分割或合併資料表。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-145">Whether the order of operations carries a risk of data loss, for example, if you're splitting or merging tables.</span></span>

<span data-ttu-id="1e9a9-146">如果您對部署腳本感到滿意，可以使用 **/dd +** 旗標重複 VSDBCMD 以進行變更。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-146">If you're happy with the deployment script, you can repeat the VSDBCMD with a **/dd+** flag to make the changes.</span></span> <span data-ttu-id="1e9a9-147">或者，您可以編輯部署腳本以符合您的需求，然後在資料庫伺服器上手動執行。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-147">Alternatively, you can edit the deployment script to meet your requirements and then execute it manually on the database server.</span></span>

## <a name="integrating-what-if-functionality-into-custom-project-files"></a><span data-ttu-id="1e9a9-148">將「What If」功能整合到自訂專案檔案</span><span class="sxs-lookup"><span data-stu-id="1e9a9-148">Integrating "What If" Functionality into Custom Project Files</span></span>

<span data-ttu-id="1e9a9-149">在更複雜的部署案例中，您會想要使用自訂的 Microsoft Build Engine （MSBuild）專案檔來封裝您的組建和部署邏輯，如[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-149">In more complex deployment scenarios, you'll want to use a custom Microsoft Build Engine (MSBuild) project file to encapsulate your build and deployment logic, as described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md).</span></span> <span data-ttu-id="1e9a9-150">例如，在[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)範例解決方案中， *Publish*檔案：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-150">For example, in the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) sample solution, the *Publish.proj* file:</span></span>

- <span data-ttu-id="1e9a9-151">建立解決方案。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-151">Builds the solution.</span></span>
- <span data-ttu-id="1e9a9-152">會使用 Web Deploy 來封裝和部署 ContactManager 的 Mvc 應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-152">Uses Web Deploy to package and deploy the ContactManager.Mvc application.</span></span>
- <span data-ttu-id="1e9a9-153">會使用 Web Deploy 來封裝和部署 ContactManager 服務應用程式。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-153">Uses Web Deploy to package and deploy the ContactManager.Service application.</span></span>
- <span data-ttu-id="1e9a9-154">部署**ContactManager**資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-154">Deploys the **ContactManager** database.</span></span>

<span data-ttu-id="1e9a9-155">當您以這種方式將多個 web 封裝和/或資料庫的部署整合到單一步驟的程式時，您可能也會想要在「假設」模式下執行整個部署的選項。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-155">When you integrate the deployment of multiple web packages and/or databases into a single-step process in this way, you may also want the option of performing the entire deployment in a "what if" mode.</span></span>

<span data-ttu-id="1e9a9-156">*Publish*檔案會示範如何執行此動作。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-156">The *Publish.proj* file demonstrates how you can do this.</span></span> <span data-ttu-id="1e9a9-157">首先，您必須建立屬性來儲存 "what if" 值：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-157">First, you need to create a property to store the "what if" value:</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

<span data-ttu-id="1e9a9-158">在此情況下，您已建立名為**WhatIf**的屬性，其預設值為**false**。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-158">In this case, you've created a property named **WhatIf** with a default value of **false**.</span></span> <span data-ttu-id="1e9a9-159">使用者可以覆寫此值，方法是在命令列參數中將屬性設為**true** ，您很快就會看到。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-159">Users can override this value by setting the property to **true** in a command-line parameter, as you'll see shortly.</span></span>

<span data-ttu-id="1e9a9-160">下一個階段是將任何 Web Deploy 和 VSDBCMD 命令參數化，讓旗標反映**WhatIf**屬性值。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-160">The next stage is to parameterize any Web Deploy and VSDBCMD commands so that the flags reflect the **WhatIf** property value.</span></span> <span data-ttu-id="1e9a9-161">例如，下一個目標（取自*Publish*檔案並簡化）會執行 *.deploy .cmd*檔案以部署 web 封裝。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-161">For example, the next target (taken from the *Publish.proj* file and simplified) runs the *.deploy.cmd* file to deploy a web package.</span></span> <span data-ttu-id="1e9a9-162">根據預設，此命令會包含 **/y**參數（[是] 或 [更新模式]）。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-162">By default, the command includes a **/Y** switch ("yes," or update mode).</span></span> <span data-ttu-id="1e9a9-163">如果**WhatIf**設定為**true**，則會以 **/t**參數（試用或「假設」模式）來取代。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-163">If **WhatIf** is set to **true**, this is replaced by a **/T** switch (trial, or "what if" mode).</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

<span data-ttu-id="1e9a9-164">同樣地，下一個目標會使用 VSDBCMD 公用程式來部署資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-164">Similarly, the next target uses the VSDBCMD utility to deploy a database.</span></span> <span data-ttu-id="1e9a9-165">根據預設，不包含 **/dd**參數。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-165">By default, a **/dd** switch is not included.</span></span> <span data-ttu-id="1e9a9-166">這表示 VSDBCMD 會產生部署腳本，但不會部署資料庫&#x2014;，換句話說，就是「假設」案例。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-166">This means that VSDBCMD will generate a deployment script but will not deploy the database&#x2014;in other words, a "what if" scenario.</span></span> <span data-ttu-id="1e9a9-167">如果**WhatIf**屬性未設定為**true**，則會新增 **/dd**參數，且 VSDBCMD 會部署資料庫。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-167">If the **WhatIf** property is not set to **true**, a **/dd** switch is added and VSDBCMD will deploy the database.</span></span>

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

<span data-ttu-id="1e9a9-168">您可以使用相同的方法，將專案檔中所有相關的命令參數化。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-168">You can use the same approach to parameterize all the relevant commands in your project file.</span></span> <span data-ttu-id="1e9a9-169">當您想要執行「假設」部署時，您可以直接從命令列提供**WhatIf**屬性值：</span><span class="sxs-lookup"><span data-stu-id="1e9a9-169">When you want to run a "what if" deployment, you can then simply provide a **WhatIf** property value from the command line:</span></span>

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

<span data-ttu-id="1e9a9-170">如此一來，您就可以在單一步驟中針對所有專案元件執行「假設」部署。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-170">In this way, you can run a "what if" deployment for all your project components in a single step.</span></span>

## <a name="conclusion"></a><span data-ttu-id="1e9a9-171">結論</span><span class="sxs-lookup"><span data-stu-id="1e9a9-171">Conclusion</span></span>

<span data-ttu-id="1e9a9-172">本主題說明如何使用 Web Deploy、VSDBCMD 和 MSBuild 來執行「假設」部署。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-172">This topic described how to run "what if" deployments using Web Deploy, VSDBCMD, and MSBuild.</span></span> <span data-ttu-id="1e9a9-173">「假設」部署可讓您在實際對目的地環境進行任何變更之前，評估建議部署的影響。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-173">A "what if" deployment lets you evaluate the impact of a proposed deployment before you actually make any changes to the destination environment.</span></span>

## <a name="further-reading"></a><span data-ttu-id="1e9a9-174">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="1e9a9-174">Further Reading</span></span>

<span data-ttu-id="1e9a9-175">如需 Web Deploy 命令列語法的詳細資訊，請參閱[Web Deploy 作業設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-175">For more information on Web Deploy command-line syntax, see [Web Deploy Operation Settings](https://technet.microsoft.com/library/dd569089(WS.10).aspx).</span></span> <span data-ttu-id="1e9a9-176">如需使用 *.deploy*檔案時命令列選項的指引，請參閱[如何：使用 Deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-176">For guidance on command-line options when you use the *.deploy.cmd* file, see [How to: Install a Deployment Package Using the deploy.cmd File](https://msdn.microsoft.com/library/ff356104.aspx).</span></span> <span data-ttu-id="1e9a9-177">如需 VSDBCMD 命令列語法的指引，請參閱[VSDBCMD 的命令列參考。EXE （部署和架構匯入）](https://msdn.microsoft.com/library/dd193283.aspx)。</span><span class="sxs-lookup"><span data-stu-id="1e9a9-177">For guidance on VSDBCMD command-line syntax, see [Command-Line Reference for VSDBCMD.EXE (Deployment and Schema Import)](https://msdn.microsoft.com/library/dd193283.aspx).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="1e9a9-178">[上一頁](advanced-enterprise-web-deployment.md)
> [下一頁](customizing-database-deployments-for-multiple-environments.md)</span><span class="sxs-lookup"><span data-stu-id="1e9a9-178">[Previous](advanced-enterprise-web-deployment.md)
[Next](customizing-database-deployments-for-multiple-environments.md)</span></span>
