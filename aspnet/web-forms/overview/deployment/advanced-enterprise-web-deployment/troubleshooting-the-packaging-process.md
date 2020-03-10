---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
title: 封裝程式的疑難排解 |Microsoft Docs
author: jrjlee
description: 本主題描述如何使用 M ... 中的 EnablePackageProcessLoggingAndAssert 屬性，來收集有關封裝程式的詳細資訊。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 794bd819-00fc-47e2-876d-fc5d15e0de1c
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/troubleshooting-the-packaging-process
msc.type: authoredcontent
ms.openlocfilehash: 8ad649dfff085a8774cc13c11d8a3e3d48277d66
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628209"
---
# <a name="troubleshooting-the-packaging-process"></a><span data-ttu-id="798e7-103">針對封裝程序進行疑難排解</span><span class="sxs-lookup"><span data-stu-id="798e7-103">Troubleshooting the Packaging Process</span></span>

<span data-ttu-id="798e7-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="798e7-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="798e7-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="798e7-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="798e7-106">本主題描述如何使用 Microsoft Build Engine （MSBuild）中的**EnablePackageProcessLoggingAndAssert**屬性，來收集有關封裝程式的詳細資訊。</span><span class="sxs-lookup"><span data-stu-id="798e7-106">This topic describes how you can collect detailed information about the packaging process by using the **EnablePackageProcessLoggingAndAssert** property in the Microsoft Build Engine (MSBuild).</span></span>
> 
> <span data-ttu-id="798e7-107">當您將**EnablePackageProcessLoggingAndAssert**屬性設定為**true**時，MSBuild 將會：</span><span class="sxs-lookup"><span data-stu-id="798e7-107">When you set the **EnablePackageProcessLoggingAndAssert** property to **true**, MSBuild will:</span></span>
> 
> - <span data-ttu-id="798e7-108">將有關封裝程式的其他資訊新增至組建記錄檔。</span><span class="sxs-lookup"><span data-stu-id="798e7-108">Add additional information about the packaging process to the build logs.</span></span>
> - <span data-ttu-id="798e7-109">在某些情況下記錄錯誤，例如，如果在封裝清單中找到重複的檔案。</span><span class="sxs-lookup"><span data-stu-id="798e7-109">Log errors under certain conditions, for example, if duplicate files are found in the packaging list.</span></span>
> - <span data-ttu-id="798e7-110">在*專案名稱*\_封裝資料夾中建立記錄檔目錄，並使用它來記錄您要封裝之檔案的相關資訊。</span><span class="sxs-lookup"><span data-stu-id="798e7-110">Create a Log directory in the *ProjectName*\_Package folder and use it to record information about the files you're packaging.</span></span>
> 
> <span data-ttu-id="798e7-111">如果封裝程式失敗，或是您的 web 部署套件未包含您預期的檔案，您可以使用這項資訊來疑難排解程式，並找出發生問題的位置。</span><span class="sxs-lookup"><span data-stu-id="798e7-111">If the packaging process is failing, or your web deployment packages don't contain the files that you expect, you can use this information to troubleshoot the process and pinpoint where things are going wrong.</span></span>
> 
> > [!NOTE]
> > <span data-ttu-id="798e7-112">只有當您使用**Debug**設定來建立專案時， **EnablePackageProcessLoggingAndAssert**屬性才有效。</span><span class="sxs-lookup"><span data-stu-id="798e7-112">The **EnablePackageProcessLoggingAndAssert** property only works if you build your project using the **Debug** configuration.</span></span> <span data-ttu-id="798e7-113">在其他設定中會忽略屬性。</span><span class="sxs-lookup"><span data-stu-id="798e7-113">The property is ignored in other configurations.</span></span>

<span data-ttu-id="798e7-114">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="798e7-114">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="798e7-115">這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。</span><span class="sxs-lookup"><span data-stu-id="798e7-115">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="798e7-116">在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="798e7-116">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="understanding-the-enablepackageprocessloggingandassert-property"></a><span data-ttu-id="798e7-117">瞭解 EnablePackageProcessLoggingAndAssert 屬性</span><span class="sxs-lookup"><span data-stu-id="798e7-117">Understanding the EnablePackageProcessLoggingAndAssert Property</span></span>

<span data-ttu-id="798e7-118">[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)說明 Web 發佈管線（WPP）如何提供一組 msbuild 目標，以擴充 msbuild 的功能，並讓它與 INTERNET INFORMATION SERVICES （IIS） Web 部署工具（Web Deploy）整合。</span><span class="sxs-lookup"><span data-stu-id="798e7-118">[Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md) described how the Web Publishing Pipeline (WPP) provides a set of MSBuild targets that extend the functionality of MSBuild and enable it to integrate with the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span> <span data-ttu-id="798e7-119">當您封裝 web 應用程式專案時，就是叫用 WPP 目標。</span><span class="sxs-lookup"><span data-stu-id="798e7-119">When you package a web application project, you're invoking WPP targets.</span></span>

<span data-ttu-id="798e7-120">其中許多的 WPP 目標包括當**EnablePackageProcessLoggingAndAssert**屬性設定為**true**時，會記錄其他資訊的條件式邏輯。</span><span class="sxs-lookup"><span data-stu-id="798e7-120">Lots of these WPP targets include conditional logic that logs additional information when the **EnablePackageProcessLoggingAndAssert** property is set to **true**.</span></span> <span data-ttu-id="798e7-121">例如，如果您檢查**封裝**目標，您可以看到它會建立額外的記錄檔目錄，並在**EnablePackageProcessLoggingAndAssert**等於**true**時，將檔案清單寫入文字檔。</span><span class="sxs-lookup"><span data-stu-id="798e7-121">For example, if you review the **Package** target, you can see that it creates an additional log directory and writes a list of files to a text file if **EnablePackageProcessLoggingAndAssert** is equal to **true**.</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample1.xml)]

> [!NOTE]
> <span data-ttu-id="798e7-122">WPP 目標是在% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 資料夾中的*web.config*檔案中定義。</span><span class="sxs-lookup"><span data-stu-id="798e7-122">The WPP targets are defined in the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span> <span data-ttu-id="798e7-123">您可以開啟此檔案，並在 Visual Studio 2010 或任何 XML 編輯器中檢查目標。</span><span class="sxs-lookup"><span data-stu-id="798e7-123">You can open this file and review the targets in Visual Studio 2010 or any XML editor.</span></span> <span data-ttu-id="798e7-124">請小心不要修改檔案的內容。</span><span class="sxs-lookup"><span data-stu-id="798e7-124">Take care not to modify the contents of the file.</span></span>

## <a name="enabling-the-additional-logging"></a><span data-ttu-id="798e7-125">啟用其他記錄</span><span class="sxs-lookup"><span data-stu-id="798e7-125">Enabling the Additional Logging</span></span>

<span data-ttu-id="798e7-126">您可以透過各種方式提供**EnablePackageProcessLoggingAndAssert**屬性的值，視您建立專案的方式而定。</span><span class="sxs-lookup"><span data-stu-id="798e7-126">You can supply a value for the **EnablePackageProcessLoggingAndAssert** property in various ways, depending on how you build your project.</span></span>

<span data-ttu-id="798e7-127">如果您從命令列建立專案，您可以提供**EnablePackageProcessLoggingAndAssert**屬性的值做為命令列引數：</span><span class="sxs-lookup"><span data-stu-id="798e7-127">If you build your project from the command line, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property as a command-line argument:</span></span>

[!code-console[Main](troubleshooting-the-packaging-process/samples/sample2.cmd)]

<span data-ttu-id="798e7-128">如果您要使用自訂專案檔來建立專案，您可以在**MSBuild**工作的**Properties**屬性中包含**EnablePackageProcessLoggingAndAssert**值：</span><span class="sxs-lookup"><span data-stu-id="798e7-128">If you're using a custom project file to build your projects, you can include the **EnablePackageProcessLoggingAndAssert** value in the **Properties** attribute of the **MSBuild** task:</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample3.xml)]

<span data-ttu-id="798e7-129">如果您要使用 Team Foundation Server （TFS）組建定義來建立專案，您可以在 [ **MSBuild 引數**] 資料列中提供**EnablePackageProcessLoggingAndAssert**屬性的值：![](troubleshooting-the-packaging-process/_static/image1.png)</span><span class="sxs-lookup"><span data-stu-id="798e7-129">If you're using a Team Foundation Server (TFS) build definition to build your projects, you can supply a value for the **EnablePackageProcessLoggingAndAssert** property in the **MSBuild Arguments** row:![](troubleshooting-the-packaging-process/_static/image1.png)</span></span>

> [!NOTE]
> <span data-ttu-id="798e7-130">如需建立和設定組建定義的詳細資訊，請參閱建立[支援部署的組建定義](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="798e7-130">For more information on creating and configuring build definitions, see [Creating a Build Definition That Supports Deployment](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md).</span></span>

<span data-ttu-id="798e7-131">或者，如果您想要在每個組建中包含封裝，您可以修改 web 應用程式專案的專案檔，將**EnablePackageProcessLoggingAndAssert**屬性設定為**true**。</span><span class="sxs-lookup"><span data-stu-id="798e7-131">Alternatively, if you want to include the package in every build, you can modify the project file for your web application project to set the **EnablePackageProcessLoggingAndAssert** property to **true**.</span></span> <span data-ttu-id="798e7-132">您應該將屬性新增至 .csproj 或. vbproj 檔案中的第一個**PropertyGroup**元素。</span><span class="sxs-lookup"><span data-stu-id="798e7-132">You should add the property to the first **PropertyGroup** element within your .csproj or .vbproj file.</span></span>

[!code-xml[Main](troubleshooting-the-packaging-process/samples/sample4.xml)]

## <a name="reviewing-the-log-files"></a><span data-ttu-id="798e7-133">查看記錄檔</span><span class="sxs-lookup"><span data-stu-id="798e7-133">Reviewing the Log Files</span></span>

<span data-ttu-id="798e7-134">當您建立並封裝已將**EnablePackageProcessLoggingAndAssert**設定為**true**的 web 應用程式專案時，MSBuild 會在*專案名稱*\_封裝資料夾中，建立名為 Log 的其他資料夾。</span><span class="sxs-lookup"><span data-stu-id="798e7-134">When you build and package a web application project with **EnablePackageProcessLoggingAndAssert** set to **true**, MSBuild creates an additional folder named Log in the *ProjectName*\_Package folder.</span></span> <span data-ttu-id="798e7-135">記錄檔資料夾包含各種檔案：</span><span class="sxs-lookup"><span data-stu-id="798e7-135">The Log folder contains various files:</span></span>

![](troubleshooting-the-packaging-process/_static/image2.png)

<span data-ttu-id="798e7-136">您所看到的檔案清單會根據您的專案和組建程式中的內容而有所不同。</span><span class="sxs-lookup"><span data-stu-id="798e7-136">The list of files that you see will vary according to the things in your project and your build process.</span></span> <span data-ttu-id="798e7-137">不過，這些檔案通常用來記錄在程式的各個階段中，由 WPP 收集來封裝的檔案清單：</span><span class="sxs-lookup"><span data-stu-id="798e7-137">However, these files are typically used to record the list of files that the WPP is collecting for packaging, at various stages of the process:</span></span>

- <span data-ttu-id="798e7-138">*PreExcludePipelineCollectFilesPhaseFileList*檔案會列出 MSBuild 在指定要排除的任何檔案移除之前，所收集的檔案。</span><span class="sxs-lookup"><span data-stu-id="798e7-138">The *PreExcludePipelineCollectFilesPhaseFileList.txt* file lists the files that MSBuild collects for packaging before any files that are specified for exclusion are removed.</span></span>
- <span data-ttu-id="798e7-139">移除指定排除的任何檔案之後， *AfterExcludeFilesFilesList*檔案會包含修改過的檔案清單。</span><span class="sxs-lookup"><span data-stu-id="798e7-139">The *AfterExcludeFilesFilesList.txt* file contains the modified file list after any files that are specified for exclusion are removed.</span></span>

    > [!NOTE]
    > <span data-ttu-id="798e7-140">如需從封裝程式排除檔案和資料夾的詳細資訊，請參閱[從部署中排除檔案和資料夾](excluding-files-and-folders-from-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="798e7-140">For more information on excluding files and folders from the packaging process, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>
- <span data-ttu-id="798e7-141">在*執行任何 web.config*轉換之後， *AfterTransformWebConfig*檔案會列出收集以封裝的檔案。</span><span class="sxs-lookup"><span data-stu-id="798e7-141">The *AfterTransformWebConfig.txt* file lists the files collected for packaging after any *Web.config* transforms have been performed.</span></span> <span data-ttu-id="798e7-142">在這份清單*中，任何*設定*特定的 web.config 轉換*檔案（例如*web.config*和 web.config）都會從要封裝的檔案清單中排除。</span><span class="sxs-lookup"><span data-stu-id="798e7-142">In this list, any configuration-specific *Web.config* transform files, like *Web.Debug.config* and *Web.Release.config*, are excluded from the list of files for packaging.</span></span> <span data-ttu-id="798e7-143">單一轉換的*web.config*會包含在其位置。</span><span class="sxs-lookup"><span data-stu-id="798e7-143">A single transformed *Web.config* is included in their place.</span></span>
- <span data-ttu-id="798e7-144">在*web.config 檔案*中的連接字串已參數化之後， *PostAutoParameterizationWebConfigConnectionStrings*檔案會包含檔案的清單。</span><span class="sxs-lookup"><span data-stu-id="798e7-144">The *PostAutoParameterizationWebConfigConnectionStrings.txt* file contains the list of files after the connection strings in the *Web.config* file have been parameterized.</span></span> <span data-ttu-id="798e7-145">此程式可讓您在部署封裝時，將連接字串取代為目標環境的正確設定。</span><span class="sxs-lookup"><span data-stu-id="798e7-145">This is the process that lets you replace your connection strings with the right settings for your target environment when you deploy the package.</span></span>
- <span data-ttu-id="798e7-146">*Prepackage*包含要包含在封裝中的已完成檔案預先建立清單。</span><span class="sxs-lookup"><span data-stu-id="798e7-146">The *Prepackage.txt* file contains the finalized pre-build list of files to be included in the package.</span></span>

> [!NOTE]
> <span data-ttu-id="798e7-147">其他記錄檔的名稱通常會對應至 WPP 目標。</span><span class="sxs-lookup"><span data-stu-id="798e7-147">The names of the additional log files typically correspond to WPP targets.</span></span> <span data-ttu-id="798e7-148">您可以檢查% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 資料夾中的*Microsoft. web.config*檔案來檢查這些目標。</span><span class="sxs-lookup"><span data-stu-id="798e7-148">You can review these targets by examining the *Microsoft.Web.Publishing.targets* file in the %PROGRAMFILES(x86)%\MSBuild\Microsoft\VisualStudio\v10.0\Web folder.</span></span>

<span data-ttu-id="798e7-149">如果您的網頁封裝內容不是您所預期，則在處理常式發生錯誤時，檢查這些檔案可能是很有用的方式。</span><span class="sxs-lookup"><span data-stu-id="798e7-149">If the contents of your web package aren't what you expected, reviewing these files can be a useful way to identify at what point in the process things went wrong.</span></span>

## <a name="conclusion"></a><span data-ttu-id="798e7-150">結論</span><span class="sxs-lookup"><span data-stu-id="798e7-150">Conclusion</span></span>

<span data-ttu-id="798e7-151">本主題說明如何使用 MSBuild 中的**EnablePackageProcessLoggingAndAssert**屬性來進行封裝程式的疑難排解。</span><span class="sxs-lookup"><span data-stu-id="798e7-151">This topic described how you can use the **EnablePackageProcessLoggingAndAssert** property in MSBuild to troubleshoot the packaging process.</span></span> <span data-ttu-id="798e7-152">它說明了您可以將屬性值提供給組建進程的不同方式，並說明當您將屬性設定為**true**時所記錄的其他資訊。</span><span class="sxs-lookup"><span data-stu-id="798e7-152">It explained the different ways in which you can supply the property value to the build process, and it described the additional information that is recorded when you set the property to **true**.</span></span>

## <a name="further-reading"></a><span data-ttu-id="798e7-153">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="798e7-153">Further Reading</span></span>

<span data-ttu-id="798e7-154">如需使用自訂 MSBuild 專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。</span><span class="sxs-lookup"><span data-stu-id="798e7-154">For more information on using custom MSBuild project files to control the deployment process, see [Understanding the Project File](../web-deployment-in-the-enterprise/understanding-the-project-file.md) and [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md).</span></span> <span data-ttu-id="798e7-155">如需 WPP 以及它如何管理封裝程式的詳細資訊，請參閱[建立和封裝 Web 應用程式專案](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="798e7-155">For more information on the WPP and how it manages the packaging process, see [Building and Packaging Web Application Projects](../web-deployment-in-the-enterprise/building-and-packaging-web-application-projects.md).</span></span> <span data-ttu-id="798e7-156">如需有關如何從 web 部署套件中排除特定檔案和資料夾的指引，請參閱[從部署中排除檔案和資料夾](excluding-files-and-folders-from-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="798e7-156">For guidance on how to exclude specific files and folders from web deployment packages, see [Excluding Files and Folders from Deployment](excluding-files-and-folders-from-deployment.md).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="798e7-157">上一篇</span><span class="sxs-lookup"><span data-stu-id="798e7-157">Previous</span></span>](running-windows-powershell-scripts-from-msbuild-project-files.md)
