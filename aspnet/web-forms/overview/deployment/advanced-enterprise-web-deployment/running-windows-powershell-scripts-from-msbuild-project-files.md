---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
title: 正在從 MSBuild 專案檔執行 Windows PowerShell 腳本 |Microsoft Docs
author: jrjlee
description: 本主題說明如何在組建和部署程式中執行 Windows PowerShell 腳本。 您可以在本機執行腳本（換句話說，在 [b ...]
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 55f1ae45-fcb5-43a9-8415-fa5b935fc9c9
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/running-windows-powershell-scripts-from-msbuild-project-files
msc.type: authoredcontent
ms.openlocfilehash: 7b09c07b8b7c2a61ca534f7a66a929593f3d04ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78548507"
---
# <a name="running-windows-powershell-scripts-from-msbuild-project-files"></a><span data-ttu-id="f3bff-104">從 MSBuild 專案檔執行 Windows PowerShell 指令碼</span><span class="sxs-lookup"><span data-stu-id="f3bff-104">Running Windows PowerShell Scripts from MSBuild Project Files</span></span>

<span data-ttu-id="f3bff-105">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="f3bff-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="f3bff-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="f3bff-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="f3bff-107">本主題說明如何在組建和部署程式中執行 Windows PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-107">This topic describes how to run a Windows PowerShell script as part of a build and deployment process.</span></span> <span data-ttu-id="f3bff-108">您可以在本機執行腳本（換句話說，在組建伺服器上）或從遠端執行（例如，在目的地 web 伺服器或資料庫伺服器上）。</span><span class="sxs-lookup"><span data-stu-id="f3bff-108">You can run a script locally (in other words, on the build server) or remotely, like on a destination web server or database server.</span></span>
> 
> <span data-ttu-id="f3bff-109">有很多原因會讓您想要執行部署後的 Windows PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-109">There are lots of reasons why you might want to run a post-deployment Windows PowerShell script.</span></span> <span data-ttu-id="f3bff-110">例如，您可能要：</span><span class="sxs-lookup"><span data-stu-id="f3bff-110">For example, you might want to:</span></span>
> 
> - <span data-ttu-id="f3bff-111">將自訂事件來源新增至登錄。</span><span class="sxs-lookup"><span data-stu-id="f3bff-111">Add a custom event source to the registry.</span></span>
> - <span data-ttu-id="f3bff-112">產生上傳的檔案系統目錄。</span><span class="sxs-lookup"><span data-stu-id="f3bff-112">Generate a file system directory for uploads.</span></span>
> - <span data-ttu-id="f3bff-113">清除組建目錄。</span><span class="sxs-lookup"><span data-stu-id="f3bff-113">Clean up build directories.</span></span>
> - <span data-ttu-id="f3bff-114">將專案寫入自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f3bff-114">Write entries to a custom log file.</span></span>
> - <span data-ttu-id="f3bff-115">將邀請使用者的電子郵件傳送至新布建的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f3bff-115">Send emails inviting users to a newly provisioned web application.</span></span>
> - <span data-ttu-id="f3bff-116">建立具有適當許可權的使用者帳戶。</span><span class="sxs-lookup"><span data-stu-id="f3bff-116">Create user accounts with the appropriate permissions.</span></span>
> - <span data-ttu-id="f3bff-117">設定 SQL Server 實例間的複寫。</span><span class="sxs-lookup"><span data-stu-id="f3bff-117">Configure replication between SQL Server instances.</span></span>
> 
> <span data-ttu-id="f3bff-118">本主題將說明如何從 Microsoft Build Engine （MSBuild）專案檔中的自訂目標，在本機和遠端執行 Windows PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-118">This topic will show you how to run Windows PowerShell scripts both locally and remotely from a custom target in a Microsoft Build Engine (MSBuild) project file.</span></span>

<span data-ttu-id="f3bff-119">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="f3bff-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="f3bff-120">這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="f3bff-120">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="f3bff-121">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="f3bff-121">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="task-overview"></a><span data-ttu-id="f3bff-122">工作總覽</span><span class="sxs-lookup"><span data-stu-id="f3bff-122">Task Overview</span></span>

<span data-ttu-id="f3bff-123">若要在自動化或單一步驟的部署程式中執行 Windows PowerShell 腳本，您必須完成下列高階工作：</span><span class="sxs-lookup"><span data-stu-id="f3bff-123">To run a Windows PowerShell script as part of an automated or single-step deployment process, you'll need to complete these high-level tasks:</span></span>

- <span data-ttu-id="f3bff-124">將 Windows PowerShell 腳本新增至您的方案和原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="f3bff-124">Add the Windows PowerShell script to your solution and to source control.</span></span>
- <span data-ttu-id="f3bff-125">建立命令來叫用您的 Windows PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-125">Create a command that invokes your Windows PowerShell script.</span></span>
- <span data-ttu-id="f3bff-126">在您的命令中，將任何保留的 XML 字元轉義。</span><span class="sxs-lookup"><span data-stu-id="f3bff-126">Escape any reserved XML characters in your command.</span></span>
- <span data-ttu-id="f3bff-127">在您的自訂 MSBuild 專案檔中建立目標，並使用**Exec**工作來執行命令。</span><span class="sxs-lookup"><span data-stu-id="f3bff-127">Create a target in your custom MSBuild project file and use the **Exec** task to run your command.</span></span>

<span data-ttu-id="f3bff-128">本主題將說明如何執行這些程式。</span><span class="sxs-lookup"><span data-stu-id="f3bff-128">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="f3bff-129">本主題中的工作和逐步解說假設您已熟悉 MSBuild 目標和屬性，並瞭解如何使用自訂 MSBuild 專案檔來驅動組建和部署程式。</span><span class="sxs-lookup"><span data-stu-id="f3bff-129">The tasks and walkthroughs in this topic assume that you're already familiar with MSBuild targets and properties, and that you understand how to use a custom MSBuild project file to drive a build and deployment process.</span></span> <span data-ttu-id="f3bff-130">如需詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。</span><span class="sxs-lookup"><span data-stu-id="f3bff-130">For more information, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

## <a name="creating-and-adding-windows-powershell-scripts"></a><span data-ttu-id="f3bff-131">建立和新增 Windows PowerShell 腳本</span><span class="sxs-lookup"><span data-stu-id="f3bff-131">Creating and Adding Windows PowerShell Scripts</span></span>

<span data-ttu-id="f3bff-132">本主題中的工作會使用名為**LogDeploy**的範例 Windows PowerShell 腳本，說明如何從 MSBuild 執行腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-132">The tasks in this topic use a sample Windows PowerShell script named **LogDeploy.ps1** to illustrate how to run scripts from MSBuild.</span></span> <span data-ttu-id="f3bff-133">**LogDeploy**腳本包含簡單的函式，可將單行專案寫入記錄檔：</span><span class="sxs-lookup"><span data-stu-id="f3bff-133">The **LogDeploy.ps1** script contains a simple function that writes a single-line entry to a log file:</span></span>

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample1.ps1)]

<span data-ttu-id="f3bff-134">**LogDeploy**腳本接受兩個參數。</span><span class="sxs-lookup"><span data-stu-id="f3bff-134">The **LogDeploy.ps1** script accepts two parameters.</span></span> <span data-ttu-id="f3bff-135">第一個參數代表您要加入專案之記錄檔的完整路徑，而第二個參數代表您要在記錄檔中記錄的部署目的地。</span><span class="sxs-lookup"><span data-stu-id="f3bff-135">The first parameter represents the full path to the log file to which you want to add an entry, and the second parameter represents the deployment destination that you want to record in the log file.</span></span> <span data-ttu-id="f3bff-136">當您執行腳本時，它會以下列格式在記錄檔中加入一行：</span><span class="sxs-lookup"><span data-stu-id="f3bff-136">When you run the script, it adds a line to the log file in this format:</span></span>

[!code-html[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample2.html)]

<span data-ttu-id="f3bff-137">若要將**LogDeploy**腳本提供給 MSBuild 使用，您必須：</span><span class="sxs-lookup"><span data-stu-id="f3bff-137">To make the **LogDeploy.ps1** script available to MSBuild, you need to:</span></span>

- <span data-ttu-id="f3bff-138">將腳本加入至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="f3bff-138">Add the script to source control.</span></span>
- <span data-ttu-id="f3bff-139">將腳本新增至您在 Visual Studio 2010 的方案中。</span><span class="sxs-lookup"><span data-stu-id="f3bff-139">Add the script to your solution in Visual Studio 2010.</span></span>

<span data-ttu-id="f3bff-140">無論您是否計畫在組建伺服器或遠端電腦上執行腳本，都不需要使用您的解決方案內容部署腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-140">You don't need to deploy the script with your solution content, regardless of whether you plan to run the script on the build server or on a remote computer.</span></span> <span data-ttu-id="f3bff-141">其中一個選項是將腳本新增至方案資料夾。</span><span class="sxs-lookup"><span data-stu-id="f3bff-141">One option is to add the script to a solution folder.</span></span> <span data-ttu-id="f3bff-142">在「連絡人管理員」範例中，因為您想要在部署程式中使用 Windows PowerShell 腳本，所以將腳本新增至「發佈解決方案」資料夾是合理的做法。</span><span class="sxs-lookup"><span data-stu-id="f3bff-142">In the Contact Manager example, because you want to use the Windows PowerShell script as part of the deployment process, it makes sense to add the script to the Publish solution folder.</span></span>

![](running-windows-powershell-scripts-from-msbuild-project-files/_static/image1.png)

<span data-ttu-id="f3bff-143">解決方案資料夾的內容會複製到組建伺服器做為來源材質。</span><span class="sxs-lookup"><span data-stu-id="f3bff-143">The contents of solution folders are copied to build servers as source material.</span></span> <span data-ttu-id="f3bff-144">不過，它們不會構成任何專案輸出的一部分。</span><span class="sxs-lookup"><span data-stu-id="f3bff-144">However, they form no part of any project output.</span></span>

## <a name="executing-a-windows-powershell-script-on-the-build-server"></a><span data-ttu-id="f3bff-145">在組建伺服器上執行 Windows PowerShell 腳本</span><span class="sxs-lookup"><span data-stu-id="f3bff-145">Executing a Windows PowerShell Script on the Build Server</span></span>

<span data-ttu-id="f3bff-146">在某些情況下，您可能會想要在建立專案的電腦上執行 Windows PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-146">In some scenarios, you may want to run Windows PowerShell scripts on the computer that builds your projects.</span></span> <span data-ttu-id="f3bff-147">例如，您可以使用 Windows PowerShell 腳本來清除組建資料夾，或將專案寫入自訂記錄檔。</span><span class="sxs-lookup"><span data-stu-id="f3bff-147">For example, you might use a Windows PowerShell script to clean up build folders or write entries to a custom log file.</span></span>

<span data-ttu-id="f3bff-148">就語法而言，從 MSBuild 專案檔執行 Windows PowerShell 腳本與從一般命令提示字元執行 Windows PowerShell 腳本的方式相同。</span><span class="sxs-lookup"><span data-stu-id="f3bff-148">In terms of syntax, running a Windows PowerShell script from an MSBuild project file is the same as running a Windows PowerShell script from a regular command prompt.</span></span> <span data-ttu-id="f3bff-149">您必須叫用 powershell .exe 可執行檔，並使用 **– command**參數來提供您想要 Windows powershell 執行的命令。</span><span class="sxs-lookup"><span data-stu-id="f3bff-149">You need to invoke the powershell.exe executable and use the **–command** switch to provide the commands you want Windows PowerShell to run.</span></span> <span data-ttu-id="f3bff-150">（在 Windows PowerShell v2 中，您也可以使用 **– file**參數）。</span><span class="sxs-lookup"><span data-stu-id="f3bff-150">(In Windows PowerShell v2, you can also use the **–file** switch).</span></span> <span data-ttu-id="f3bff-151">命令應採用下列格式：</span><span class="sxs-lookup"><span data-stu-id="f3bff-151">The command should take this format:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample3.cmd)]

<span data-ttu-id="f3bff-152">例如:</span><span class="sxs-lookup"><span data-stu-id="f3bff-152">For example:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample4.cmd)]

<span data-ttu-id="f3bff-153">如果腳本的路徑包含空格，您必須以單引號括住檔案路徑，並在前面加上連字號。</span><span class="sxs-lookup"><span data-stu-id="f3bff-153">If the path to your script includes spaces, you need to enclose the file path in single quotes preceded by an ampersand.</span></span> <span data-ttu-id="f3bff-154">您不能使用雙引號，因為您已經使用它們來括住命令：</span><span class="sxs-lookup"><span data-stu-id="f3bff-154">You can't use double quotes, because you've already used them to enclose the command:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample5.cmd)]

<span data-ttu-id="f3bff-155">當您從 MSBuild 叫用此命令時，還有一些額外的考慮。</span><span class="sxs-lookup"><span data-stu-id="f3bff-155">There are a few additional considerations when you invoke this command from MSBuild.</span></span> <span data-ttu-id="f3bff-156">首先，您應該包含 **–非互動式**旗標，以確保腳本會以安靜的模式執行。</span><span class="sxs-lookup"><span data-stu-id="f3bff-156">First, you should include the **–NonInteractive** flag to ensure that the script executes quietly.</span></span> <span data-ttu-id="f3bff-157">接下來，您應該包含 **– ExecutionPolicy**旗標與適當的引數值。</span><span class="sxs-lookup"><span data-stu-id="f3bff-157">Next, you should include the **–ExecutionPolicy** flag with an appropriate argument value.</span></span> <span data-ttu-id="f3bff-158">這會指定 Windows PowerShell 套用至腳本的執行原則，並可讓您覆寫預設的執行原則，這可能會導致腳本無法執行。</span><span class="sxs-lookup"><span data-stu-id="f3bff-158">This specifies the execution policy that Windows PowerShell will apply to your script and allows you to override the default execution policy, which may prevent execution of your script.</span></span> <span data-ttu-id="f3bff-159">您可以從下列引數值中選擇：</span><span class="sxs-lookup"><span data-stu-id="f3bff-159">You can choose from these argument values:</span></span>

- <span data-ttu-id="f3bff-160">不**受限制**的值可讓 Windows PowerShell 執行您的腳本，不論腳本是否已簽署。</span><span class="sxs-lookup"><span data-stu-id="f3bff-160">A value of **Unrestricted** will allow Windows PowerShell to execute your script, regardless of whether the script is signed.</span></span>
- <span data-ttu-id="f3bff-161">**RemoteSigned**的值可讓 Windows PowerShell 執行在本機電腦上建立的未簽署腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-161">A value of **RemoteSigned** will allow Windows PowerShell to execute unsigned scripts that were created on the local machine.</span></span> <span data-ttu-id="f3bff-162">不過，在其他地方建立的腳本必須經過簽署。</span><span class="sxs-lookup"><span data-stu-id="f3bff-162">However, scripts that were created elsewhere must be signed.</span></span> <span data-ttu-id="f3bff-163">（實際上，在組建伺服器上，您不太可能在本機建立 Windows PowerShell 腳本）。</span><span class="sxs-lookup"><span data-stu-id="f3bff-163">(In practice, you're very unlikely to have created a Windows PowerShell script locally on a build server).</span></span>
- <span data-ttu-id="f3bff-164">**AllSigned**的值可讓 Windows PowerShell 只執行已簽署的腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-164">A value of **AllSigned** will allow Windows PowerShell to execute signed scripts only.</span></span>

<span data-ttu-id="f3bff-165">預設執行原則是**受限制**的，這可防止 Windows PowerShell 執行任何腳本檔案。</span><span class="sxs-lookup"><span data-stu-id="f3bff-165">The default execution policy is **Restricted**, which prevents Windows PowerShell from running any script files.</span></span>

<span data-ttu-id="f3bff-166">最後，您必須將任何在 Windows PowerShell 命令中發生的保留 XML 字元加以轉義：</span><span class="sxs-lookup"><span data-stu-id="f3bff-166">Finally, you need to escape any reserved XML characters that occur in your Windows PowerShell command:</span></span>

- <span data-ttu-id="f3bff-167">將單引號取代**為&amp;** 的</span><span class="sxs-lookup"><span data-stu-id="f3bff-167">Replace single quotes with **&amp;apos;**</span></span>
- <span data-ttu-id="f3bff-168">將雙引號取代為 **&amp;**</span><span class="sxs-lookup"><span data-stu-id="f3bff-168">Replace double quotes with **&amp;quot;**</span></span>
- <span data-ttu-id="f3bff-169">將符號取代為 **&amp;amp;**</span><span class="sxs-lookup"><span data-stu-id="f3bff-169">Replace ampersands with **&amp;amp;**</span></span>

- <span data-ttu-id="f3bff-170">當您進行這些變更時，您的命令會如下所示：</span><span class="sxs-lookup"><span data-stu-id="f3bff-170">When you make these changes, your command will resemble this:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample6.cmd)]

<span data-ttu-id="f3bff-171">在您的自訂 MSBuild 專案檔中，您可以建立新的目標，並使用**Exec**工作來執行此命令：</span><span class="sxs-lookup"><span data-stu-id="f3bff-171">Within your custom MSBuild project file, you can create a new target and use the **Exec** task to run this command:</span></span>

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample7.xml)]

<span data-ttu-id="f3bff-172">在此範例中，請注意：</span><span class="sxs-lookup"><span data-stu-id="f3bff-172">In this example, note that:</span></span>

- <span data-ttu-id="f3bff-173">任何變數（例如參數值和 Windows PowerShell 可執行檔的位置）都會宣告為 MSBuild 屬性。</span><span class="sxs-lookup"><span data-stu-id="f3bff-173">Any variables, like parameter values and the location of the Windows PowerShell executable, are declared as MSBuild properties.</span></span>
- <span data-ttu-id="f3bff-174">包含的條件可讓使用者從命令列覆寫這些值。</span><span class="sxs-lookup"><span data-stu-id="f3bff-174">Conditions are included to enable users to override these values from the command line.</span></span>
- <span data-ttu-id="f3bff-175">**MSDeployComputerName**屬性會在專案檔中的其他位置宣告。</span><span class="sxs-lookup"><span data-stu-id="f3bff-175">The **MSDeployComputerName** property is declared elsewhere in the project file.</span></span>

<span data-ttu-id="f3bff-176">當您執行此目標做為組建程式的一部分時，Windows PowerShell 將會執行您的命令，並將記錄專案寫入您指定的檔案。</span><span class="sxs-lookup"><span data-stu-id="f3bff-176">When you execute this target as part of your build process, Windows PowerShell will run your command and write a log entry to the file you specified.</span></span>

## <a name="executing-a-windows-powershell-script-on-a-remote-computer"></a><span data-ttu-id="f3bff-177">在遠端電腦上執行 Windows PowerShell 腳本</span><span class="sxs-lookup"><span data-stu-id="f3bff-177">Executing a Windows PowerShell Script on a Remote Computer</span></span>

<span data-ttu-id="f3bff-178">Windows PowerShell 能夠透過[Windows 遠端管理](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx)（WinRM）在遠端電腦上執行腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-178">Windows PowerShell is capable of running scripts on remote computers through [Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384426.aspx) (WinRM).</span></span> <span data-ttu-id="f3bff-179">若要這樣做，您需要使用[Invoke 命令](https://technet.microsoft.com/library/dd347578.aspx)Cmdlet。</span><span class="sxs-lookup"><span data-stu-id="f3bff-179">To do this, you need to use the [Invoke-Command](https://technet.microsoft.com/library/dd347578.aspx) cmdlet.</span></span> <span data-ttu-id="f3bff-180">這可讓您針對一或多部遠端電腦執行腳本，而不需要將腳本複製到遠端電腦。</span><span class="sxs-lookup"><span data-stu-id="f3bff-180">This lets you execute your script against one or more remote computers without copying the script to the remote computers.</span></span> <span data-ttu-id="f3bff-181">任何結果都會傳回您執行腳本的本機電腦。</span><span class="sxs-lookup"><span data-stu-id="f3bff-181">Any results are returned to the local computer from which you ran the script.</span></span>

> [!NOTE]
> <span data-ttu-id="f3bff-182">使用**Invoke 命令**Cmdlet 在遠端電腦上執行 Windows PowerShell 腳本之前，您必須先設定 WinRM 接聽程式以接受遠端訊息。</span><span class="sxs-lookup"><span data-stu-id="f3bff-182">Before you use the **Invoke-Command** cmdlet to execute Windows PowerShell scripts on a remote computer, you need to configure a WinRM listener to accept remote messages.</span></span> <span data-ttu-id="f3bff-183">若要這麼做，您可以在遠端電腦上執行**winrm quickconfig**命令。</span><span class="sxs-lookup"><span data-stu-id="f3bff-183">You can do this by running the command **winrm quickconfig** on the remote computer.</span></span> <span data-ttu-id="f3bff-184">如需詳細資訊，請參閱[Windows 遠端管理的安裝和](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx)設定。</span><span class="sxs-lookup"><span data-stu-id="f3bff-184">For more information, see [Installation and Configuration for Windows Remote Management](https://msdn.microsoft.com/library/windows/desktop/aa384372(v=vs.85).aspx).</span></span>

<span data-ttu-id="f3bff-185">在 Windows PowerShell 視窗中，您可以使用此語法在遠端電腦上執行**LogDeploy**腳本：</span><span class="sxs-lookup"><span data-stu-id="f3bff-185">From a Windows PowerShell window, you'd use this syntax to run the **LogDeploy.ps1** script on a remote computer:</span></span>

[!code-powershell[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample8.ps1)]

> [!NOTE]
> <span data-ttu-id="f3bff-186">有各種其他方法可以使用**Invoke 命令**來執行腳本檔案，但當您需要提供參數值和管理具有空格的路徑時，這個方法是最直接的方式。</span><span class="sxs-lookup"><span data-stu-id="f3bff-186">There are various other ways of using **Invoke-Command** to run a script file, but this approach is the most straightforward when you need to provide parameter values and manage paths with spaces.</span></span>

<span data-ttu-id="f3bff-187">當您從命令提示字元執行此動作時，您必須叫用 Windows PowerShell 可執行檔，並使用 **– command**參數來提供您的指示：</span><span class="sxs-lookup"><span data-stu-id="f3bff-187">When you run this from a command prompt, you need to invoke the Windows PowerShell executable and use the **–command** parameter to provide your instructions:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample9.cmd)]

<span data-ttu-id="f3bff-188">如先前所述，當您從 MSBuild 執行命令時，您必須提供一些額外的參數，並將任何保留的 XML 字元換行：</span><span class="sxs-lookup"><span data-stu-id="f3bff-188">As before, you need to provide some additional switches and escape any reserved XML characters when you run the command from MSBuild:</span></span>

[!code-console[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample10.cmd)]

<span data-ttu-id="f3bff-189">最後，您可以像之前一樣，在自訂 MSBuild 目標內使用**Exec**工作來執行命令：</span><span class="sxs-lookup"><span data-stu-id="f3bff-189">Finally, as before, you can use the **Exec** task within a custom MSBuild target to execute your command:</span></span>

[!code-xml[Main](running-windows-powershell-scripts-from-msbuild-project-files/samples/sample11.xml)]

<span data-ttu-id="f3bff-190">當您執行此目標做為組建程式的一部分時，Windows PowerShell 會在您于 **– computername**引數中指定的電腦上執行您的腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-190">When you execute this target as part of your build process, Windows PowerShell will run your script on the computer you specified in the **–computername** argument.</span></span>

## <a name="conclusion"></a><span data-ttu-id="f3bff-191">結論</span><span class="sxs-lookup"><span data-stu-id="f3bff-191">Conclusion</span></span>

<span data-ttu-id="f3bff-192">本主題說明如何從 MSBuild 專案檔執行 Windows PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-192">This topic described how to run a Windows PowerShell script from an MSBuild project file.</span></span> <span data-ttu-id="f3bff-193">您可以使用此方法，在自動或單一步驟的組建和部署程式中，于本機或遠端電腦上執行 Windows PowerShell 腳本。</span><span class="sxs-lookup"><span data-stu-id="f3bff-193">You can use this approach to run a Windows PowerShell script, either locally or on a remote computer, as part of an automated or single-step build and deployment process.</span></span>

## <a name="further-reading"></a><span data-ttu-id="f3bff-194">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="f3bff-194">Further Reading</span></span>

<span data-ttu-id="f3bff-195">如需簽署 Windows PowerShell 腳本和管理執行原則的指引，請參閱執行[Windows Powershell 腳本](https://technet.microsoft.com/library/ee176949.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3bff-195">For guidance on signing Windows PowerShell scripts and managing execution policies, see [Running Windows PowerShell Scripts](https://technet.microsoft.com/library/ee176949.aspx).</span></span> <span data-ttu-id="f3bff-196">如需有關從遠端電腦執行 Windows PowerShell 命令的指引，請參閱執行[遠端命令](https://technet.microsoft.com/library/dd819505.aspx)。</span><span class="sxs-lookup"><span data-stu-id="f3bff-196">For guidance on running Windows PowerShell commands from a remote computer, see [Running Remote Commands](https://technet.microsoft.com/library/dd819505.aspx).</span></span>

<span data-ttu-id="f3bff-197">如需使用自訂 MSBuild 專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。</span><span class="sxs-lookup"><span data-stu-id="f3bff-197">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="f3bff-198">[上一頁](taking-web-applications-offline-with-web-deploy.md)
> [下一頁](troubleshooting-the-packaging-process.md)</span><span class="sxs-lookup"><span data-stu-id="f3bff-198">[Previous](taking-web-applications-offline-with-web-deploy.md)
[Next](troubleshooting-the-packaging-process.md)</span></span>
