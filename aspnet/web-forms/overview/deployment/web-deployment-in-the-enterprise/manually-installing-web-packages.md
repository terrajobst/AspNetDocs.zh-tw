---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
title: 手動安裝 Web 套件 |Microsoft Docs
author: jrjlee
description: 本主題描述如何以手動方式將 web 部署套件匯入 Internet Information Services （IIS）中。 建立和封裝 Web Applicati 主題 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f11d22a7-5d32-4ad0-8a9b-276460a61c06
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/manually-installing-web-packages
msc.type: authoredcontent
ms.openlocfilehash: f778549d3e26989a2e71ef21171adec521842729
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634201"
---
# <a name="manually-installing-web-packages"></a><span data-ttu-id="43a95-104">手動安裝 Web 套件</span><span class="sxs-lookup"><span data-stu-id="43a95-104">Manually Installing Web Packages</span></span>

<span data-ttu-id="43a95-105">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="43a95-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="43a95-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="43a95-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="43a95-107">本主題描述如何以手動方式將 web 部署套件匯入 Internet Information Services （IIS）中。</span><span class="sxs-lookup"><span data-stu-id="43a95-107">This topic describes how to manually import a web deployment package into Internet Information Services (IIS).</span></span>
> 
> <span data-ttu-id="43a95-108">[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)主題說明了 IIS Web Deployment Tool （Web Deploy）與 Microsoft Build Engine （MSBuild）和 Web 發行管線（WPP）如何搭配使用，讓您將 web 應用程式專案封裝成單一的 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="43a95-108">The topic [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md) described how the IIS Web Deployment Tool (Web Deploy), in conjunction with the Microsoft Build Engine (MSBuild) and the Web Publishing Pipeline (WPP), lets you package your web application projects into a single zip file.</span></span> <span data-ttu-id="43a95-109">此檔案通常稱為 web 部署套件（或只是部署套件），其中包含 IIS 在 web 伺服器上重新建立 web 應用程式所需的所有內容和設定資訊。</span><span class="sxs-lookup"><span data-stu-id="43a95-109">This file, commonly known as a web deployment package (or simply a deployment package), contains all the content and configuration information that IIS needs in order to re-create your web application on a web server.</span></span>
> 
> <span data-ttu-id="43a95-110">建立 web 部署套件之後，您可以透過各種方式將它發佈至 IIS 伺服器。</span><span class="sxs-lookup"><span data-stu-id="43a95-110">Once you've created a web deployment package, you can publish it to an IIS server in various ways.</span></span> <span data-ttu-id="43a95-111">在許多情況下，您會想要利用 MSBuild、WPP 和 Web Deploy 之間的整合點，在自動或單一步驟的組建和部署程式中，從遠端建立和安裝 Web 套件。</span><span class="sxs-lookup"><span data-stu-id="43a95-111">In a lot of scenarios, you'll want to take advantage of the integration points between MSBuild, the WPP, and Web Deploy to create and install web packages remotely as part of an automated or single-step build and deployment process.</span></span> <span data-ttu-id="43a95-112">[部署 Web 套件](deploying-web-packages.md)中會說明此程式。</span><span class="sxs-lookup"><span data-stu-id="43a95-112">This process is described in [Deploying Web Packages](deploying-web-packages.md).</span></span> <span data-ttu-id="43a95-113">不過，這不一定可行。</span><span class="sxs-lookup"><span data-stu-id="43a95-113">However, this isn't always possible.</span></span> <span data-ttu-id="43a95-114">假設您想要將 web 應用程式部署到網際網路面向的生產環境。</span><span class="sxs-lookup"><span data-stu-id="43a95-114">Suppose you want to deploy a web application to an Internet-facing production environment.</span></span> <span data-ttu-id="43a95-115">基於安全性理由，這類生產環境最不可能位於與組建伺服器不同的子網上的防火牆後方，位於周邊網路（也稱為 DMZ、非軍事區域和遮蔽式子網路）。</span><span class="sxs-lookup"><span data-stu-id="43a95-115">For security reasons, such a production environment is at the very least likely to be behind a firewall on a subnet that is separate from the build server, in a perimeter network (also known as DMZ, demilitarized zone, and screened subnet).</span></span> <span data-ttu-id="43a95-116">在許多情況下，生產環境會位於不同的網域或實體隔離的網路上。</span><span class="sxs-lookup"><span data-stu-id="43a95-116">In lots of cases, the production environment will be on a separate domain or on a physically isolated network.</span></span>
> 
> <span data-ttu-id="43a95-117">在這些情況下，您的唯一選項可能是將 web 套件移植到目的地伺服器，並手動將它匯入到 IIS 中。</span><span class="sxs-lookup"><span data-stu-id="43a95-117">In these scenarios, your only option may be to port the web package onto the destination server and manually import it into IIS.</span></span> <span data-ttu-id="43a95-118">雖然這種方法會排除自動化部署，但它仍然是發佈 web 應用程式&#x2014;的高效率技巧，只要將單一 zip 檔案複製到您的 web 伺服器，然後使用 wizard 引導您完成匯入程式。</span><span class="sxs-lookup"><span data-stu-id="43a95-118">Although this approach precludes automated deployment, it's still a highly effective technique for publishing a web application&#x2014;you simply copy a single zip file to your web server and use a wizard to guide you through the import process.</span></span>

<span data-ttu-id="43a95-119">本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="43a95-119">This topic forms part of a series of tutorials based around the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager solution](the-contact-manager-solution.md)&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

## <a name="task-overview"></a><span data-ttu-id="43a95-120">工作總覽</span><span class="sxs-lookup"><span data-stu-id="43a95-120">Task Overview</span></span>

<span data-ttu-id="43a95-121">您必須完成這些高階工作，才能將 web 部署套件匯入 IIS：</span><span class="sxs-lookup"><span data-stu-id="43a95-121">You'll need to complete these high-level tasks to import a web deployment package into IIS:</span></span>

- <span data-ttu-id="43a95-122">使用 MSBuild 命令列、Team Build 或 Visual Studio 2010 建立 web 部署套件。</span><span class="sxs-lookup"><span data-stu-id="43a95-122">Create a web deployment package using the MSBuild command line, Team Build, or Visual Studio 2010.</span></span>
- <span data-ttu-id="43a95-123">將網頁套件複製到目的地 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="43a95-123">Copy the web package to the destination web server.</span></span>
- <span data-ttu-id="43a95-124">使用 IIS 管理員中的 [匯入應用程式封裝]，即可安裝 web 套件並提供變數的值，例如連接字串和服務端點。</span><span class="sxs-lookup"><span data-stu-id="43a95-124">Use the Import Application Package Wizard in IIS Manager to install the web package and provide values for variables like connection strings and service endpoints.</span></span>

<span data-ttu-id="43a95-125">本主題將說明如何執行這些程式。</span><span class="sxs-lookup"><span data-stu-id="43a95-125">This topic will show you how to perform these procedures.</span></span> <span data-ttu-id="43a95-126">本主題中的工作和逐步解說假設您已經熟悉 web 套件、Web Deploy 和 WPP 背後的概念。</span><span class="sxs-lookup"><span data-stu-id="43a95-126">The tasks and walkthroughs in this topic assume that you're already familiar with the concepts behind web packages, Web Deploy, and the WPP.</span></span> <span data-ttu-id="43a95-127">如需詳細資訊，請參閱[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)。</span><span class="sxs-lookup"><span data-stu-id="43a95-127">For more information, see [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

> [!NOTE]
> <span data-ttu-id="43a95-128">本主題最適合用於[[設定用於 Web Deploy 發佈的 Web 服務器（離線部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)]，其中說明如何安裝必要的元件，並準備 IIS 網站以進行套件匯入。</span><span class="sxs-lookup"><span data-stu-id="43a95-128">This topic is best used in conjunction with [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md), which explains how to install the required components and prepare an IIS website for package import.</span></span>

## <a name="create-a-web-deployment-package"></a><span data-ttu-id="43a95-129">建立 Web 部署套件</span><span class="sxs-lookup"><span data-stu-id="43a95-129">Create a Web Deployment Package</span></span>

<span data-ttu-id="43a95-130">第一個工作是為您想要部署的 web 應用程式專案建立 web 部署套件。</span><span class="sxs-lookup"><span data-stu-id="43a95-130">The first task is to create a web deployment package for the web application project you want to deploy.</span></span> <span data-ttu-id="43a95-131">您可以用各種方式建立網頁封裝。</span><span class="sxs-lookup"><span data-stu-id="43a95-131">You can create web packages in a variety of ways.</span></span>

<span data-ttu-id="43a95-132">**方法1：使用 Visual Studio 在組建程式中建立封裝**</span><span class="sxs-lookup"><span data-stu-id="43a95-132">**Approach 1: Create a package as part of the build process with Visual Studio**</span></span>

<span data-ttu-id="43a95-133">您可以設定 web 應用程式專案，透過專案屬性頁上的 [**封裝/發行 web** ] 索引標籤，在每個組建之後建立 web 部署封裝。</span><span class="sxs-lookup"><span data-stu-id="43a95-133">You can configure your web application project to create a web deployment package after every build through the **Package/Publish Web** tab on the project property pages.</span></span> <span data-ttu-id="43a95-134">[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)中會說明這個程式。</span><span class="sxs-lookup"><span data-stu-id="43a95-134">This process is described in [Building and Packaging Web Application Projects](building-and-packaging-web-application-projects.md).</span></span>

<span data-ttu-id="43a95-135">**方法2：使用 MSBuild 建立封裝作為組建程式的一部分**</span><span class="sxs-lookup"><span data-stu-id="43a95-135">**Approach 2: Create a package as part of the build process with MSBuild**</span></span>

<span data-ttu-id="43a95-136">如果您直接使用 MSBuild 建立 web 應用程式專案（不論是透過自訂 MSBuild 專案檔或從命令列），您可以在命令中包含**DeployOnBuild = true**和**DeployTarget = package**屬性，以建立 web 部署封裝做為建立程式的一部分。</span><span class="sxs-lookup"><span data-stu-id="43a95-136">If you build your web application project by using MSBuild directly, either through a custom MSBuild project file or from the command line, you can create a web deployment package as part of the build process by including the **DeployOnBuild=true** and **DeployTarget=Package** properties in your command.</span></span> <span data-ttu-id="43a95-137">瞭解此程式的說明請參閱[瞭解組建流程](understanding-the-build-process.md)。</span><span class="sxs-lookup"><span data-stu-id="43a95-137">This process is described in [Understanding the Build Process](understanding-the-build-process.md).</span></span>

<span data-ttu-id="43a95-138">**方法3：依需求在 Visual Studio 中建立套件**</span><span class="sxs-lookup"><span data-stu-id="43a95-138">**Approach 3: Create a package on demand in Visual Studio**</span></span>

<span data-ttu-id="43a95-139">您可以在 Visual Studio 2010 中隨時建立 web 應用程式專案的 web 部署套件。</span><span class="sxs-lookup"><span data-stu-id="43a95-139">You can create a web deployment package for a web application project at any time in Visual Studio 2010.</span></span> <span data-ttu-id="43a95-140">若要這麼做，請在 [**方案總管**] 視窗中，以滑鼠右鍵按一下您的 web 應用程式專案，然後按一下 [**建立部署封裝**]。</span><span class="sxs-lookup"><span data-stu-id="43a95-140">To do this, in the **Solution Explorer** window, right-click your web application project, and then click **Build Deployment Package**.</span></span>

![](manually-installing-web-packages/_static/image1.png)

<span data-ttu-id="43a95-141">**方法4：依需求從命令列建立套件**</span><span class="sxs-lookup"><span data-stu-id="43a95-141">**Approach 4: Create a package on demand from the command line**</span></span>

<span data-ttu-id="43a95-142">您可以使用 MSBuild 在 web 應用程式專案上叫用**封裝**目標，以從命令列建立 web 部署封裝。</span><span class="sxs-lookup"><span data-stu-id="43a95-142">You can create a web deployment package from the command line by invoking the **Package** target on your web application project using MSBuild.</span></span> <span data-ttu-id="43a95-143">命令應如下所示：</span><span class="sxs-lookup"><span data-stu-id="43a95-143">The command should resemble this:</span></span>

[!code-console[Main](manually-installing-web-packages/samples/sample1.cmd)]

<span data-ttu-id="43a95-144">無論您使用哪種方法，最後的結果都一樣。</span><span class="sxs-lookup"><span data-stu-id="43a95-144">Whichever approach you use, the end result is the same.</span></span> <span data-ttu-id="43a95-145">WPP 會在您 web 應用程式專案的輸出檔案夾中，建立一個 zip 檔案和各種支援資源的 web 部署套件。</span><span class="sxs-lookup"><span data-stu-id="43a95-145">The WPP creates a web deployment package as a zip file, together with various supporting resources, in the output folder for your web application project.</span></span>

![](manually-installing-web-packages/_static/image2.png)

<span data-ttu-id="43a95-146">當您打算手動匯入 web 套件時，您只需要 zip 檔案。</span><span class="sxs-lookup"><span data-stu-id="43a95-146">When you're planning to import the web package manually, you require only the zip file.</span></span> <span data-ttu-id="43a95-147">將此檔案複製到您的目標 web 伺服器，然後您就可以開始匯入程式。</span><span class="sxs-lookup"><span data-stu-id="43a95-147">Copy this file to your target web server and you can begin the import process.</span></span>

## <a name="import-a-web-package-into-iis"></a><span data-ttu-id="43a95-148">將 Web 封裝匯入 IIS</span><span class="sxs-lookup"><span data-stu-id="43a95-148">Import a Web Package into IIS</span></span>

<span data-ttu-id="43a95-149">您可以使用下一個程式，將 web 部署套件從本機檔案系統匯入到 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="43a95-149">You can use the next procedure to import a web deployment package from the local file system into an IIS website.</span></span> <span data-ttu-id="43a95-150">執行此程式之前，請確定您有：</span><span class="sxs-lookup"><span data-stu-id="43a95-150">Before you perform this procedure, ensure that you have:</span></span>

- <span data-ttu-id="43a95-151">已將 web 部署套件複製到 web 伺服器。</span><span class="sxs-lookup"><span data-stu-id="43a95-151">Copied the web deployment package to the web server.</span></span>
- <span data-ttu-id="43a95-152">設定 IIS web 伺服器來裝載您的應用程式。</span><span class="sxs-lookup"><span data-stu-id="43a95-152">Configured an IIS web server to host your application.</span></span>

<span data-ttu-id="43a95-153">如需設定 IIS web 伺服器以支援 web 部署套件的詳細資訊，請參閱[Configure a Web server for Web Deploy 發佈（離線部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="43a95-153">For more information on configuring an IIS web server to support web deployment packages, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span>

<span data-ttu-id="43a95-154">**使用 IIS 管理員匯入 web 部署套件**</span><span class="sxs-lookup"><span data-stu-id="43a95-154">**To import a web deployment package using IIS Manager**</span></span>

1. <span data-ttu-id="43a95-155">在 **[Iis**管理員] 的 [連線] 窗格中，以滑鼠右鍵按一下您的 IIS 網站，指向 [**部署**]，然後按一下 [匯**入應用程式**]。</span><span class="sxs-lookup"><span data-stu-id="43a95-155">In IIS Manager, in the **Connections** pane, right-click your IIS website, point to **Deploy**, and then click **Import Application**.</span></span>

    ![](manually-installing-web-packages/_static/image3.png)
2. <span data-ttu-id="43a95-156">在 [匯入應用程式套件] 中，于 [**選取封裝**] 頁面上，流覽至 web 部署套件的位置，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="43a95-156">In the Import Application Package Wizard, on the **Select the Package** page, browse to the location of your web deployment package, and then click **Next**.</span></span>
3. <span data-ttu-id="43a95-157">在 [**選取封裝的內容**] 頁面上，清除您不需要的任何內容，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="43a95-157">On the **Select the Contents of the Package** page, clear any content that you don't require, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image4.png)

    > [!NOTE]
    > <span data-ttu-id="43a95-158">在許多情況下，您可能不想要匯入 web 部署套件隨附的所有內容。</span><span class="sxs-lookup"><span data-stu-id="43a95-158">In a lot of cases, you may not want to import everything that comes with a web deployment package.</span></span> <span data-ttu-id="43a95-159">例如，您可能不想讓 Web Deploy 取代相關聯的資料庫。</span><span class="sxs-lookup"><span data-stu-id="43a95-159">For example, you may not want to allow Web Deploy to replace the associated database.</span></span>  
    > <span data-ttu-id="43a95-160">**授與許可權**專案會在目的地檔案系統上設定許可權，以確保應用程式集區身分識別可以存取儲存網站內容的實體資料夾。</span><span class="sxs-lookup"><span data-stu-id="43a95-160">The **Grant permissions** entries set permissions on the destination file system to ensure that the application pool identity can access the physical folder that stores the website content.</span></span> <span data-ttu-id="43a95-161">此外，會將資料夾的讀取權限授與匿名驗證使用者，讓應用程式提供多用途網際網路郵件延伸（MIME）類型檔案。</span><span class="sxs-lookup"><span data-stu-id="43a95-161">In addition, the anonymous authentication user is granted read permission to the folder to let the application serve Multipurpose Internet Mail Extensions (MIME) type files.</span></span> <span data-ttu-id="43a95-162">如果您想要的話，也可以移除這些專案，並手動設定許可權。</span><span class="sxs-lookup"><span data-stu-id="43a95-162">If you prefer, you can remove these entries and configure permissions manually.</span></span>
4. <span data-ttu-id="43a95-163">在 [**輸入應用程式封裝資訊**] 頁面上，提供所要求的資訊。</span><span class="sxs-lookup"><span data-stu-id="43a95-163">On the **Enter Application Package Information** page, provide the requested information.</span></span>

    ![](manually-installing-web-packages/_static/image5.png)
5. <span data-ttu-id="43a95-164">當您建立 web 套件時，WPP 會分析應用程式的設定檔案，並偵測任何變數，例如連接字串和服務端點。</span><span class="sxs-lookup"><span data-stu-id="43a95-164">When you create a web package, the WPP analyzes the configuration file for your application and detects any variables, like connection strings and service endpoints.</span></span> <span data-ttu-id="43a95-165">在此情況下：</span><span class="sxs-lookup"><span data-stu-id="43a95-165">In this case:</span></span>

    1. <span data-ttu-id="43a95-166">[**應用程式路徑**] 是您要安裝應用程式的 IIS 路徑。</span><span class="sxs-lookup"><span data-stu-id="43a95-166">**Application Path** is the IIS path where you want to install your application.</span></span> <span data-ttu-id="43a95-167">此設定通用於 WPP 所建立的所有部署套件。</span><span class="sxs-lookup"><span data-stu-id="43a95-167">This setting is common to all deployment packages that the WPP creates.</span></span>
    2. <span data-ttu-id="43a95-168">**ContactService 服務端點位址**是應用程式應該用來與已部署的 WCF 服務進行通訊的位址。</span><span class="sxs-lookup"><span data-stu-id="43a95-168">**ContactService Service Endpoint Address** is the address that the application should use to communicate with the deployed WCF service.</span></span> <span data-ttu-id="43a95-169">此設定會對應*至 web.config 檔案*中的專案。</span><span class="sxs-lookup"><span data-stu-id="43a95-169">This setting corresponds to an entry in the *web.config* file.</span></span>
    3. <span data-ttu-id="43a95-170">第一個**連接字串**設定是 Web Deploy 應該用來部署與應用程式相關聯之資料庫的連接字串（在此案例中為 ASP.NET 成員資格資料庫）。</span><span class="sxs-lookup"><span data-stu-id="43a95-170">The first **Connection String** setting is the connection string that Web Deploy should use to deploy the database associated with the application (in this case an ASP.NET membership database).</span></span> <span data-ttu-id="43a95-171">此設定會對應至 Visual Studio 中 [**封裝/發行 SQL** ] 索引標籤上的設定。</span><span class="sxs-lookup"><span data-stu-id="43a95-171">This setting corresponds to the setting on the **Package/Publish SQL** tab in Visual Studio.</span></span>
    4. <span data-ttu-id="43a95-172">第二個**連接字串**設定是連接字串，當應用程式啟動並執行時，它會實際用來與資料庫進行通訊。</span><span class="sxs-lookup"><span data-stu-id="43a95-172">The second **Connection String** setting is the connection string that your application will actually use to communicate with the database when it's up and running.</span></span> <span data-ttu-id="43a95-173">這會對應*至 web.config 檔案*中的連接字串專案。</span><span class="sxs-lookup"><span data-stu-id="43a95-173">This corresponds to a connection string entry in the *web.config* file.</span></span>

        > [!NOTE]
        > <span data-ttu-id="43a95-174">如需這些參數來自何處的詳細資訊，請參閱設定[Web 封裝部署的參數](configuring-parameters-for-web-package-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="43a95-174">For more information on where these parameters come from, see [Configuring Parameters for Web Package Deployment](configuring-parameters-for-web-package-deployment.md).</span></span>
6. <span data-ttu-id="43a95-175">按 [下一步]。</span><span class="sxs-lookup"><span data-stu-id="43a95-175">Click **Next**.</span></span>
7. <span data-ttu-id="43a95-176">如果這不是您第一次將應用程式部署到此網站，系統會提示您指定是否要在安裝前刪除所有現有的內容。</span><span class="sxs-lookup"><span data-stu-id="43a95-176">If this is not the first time you've deployed the application to this website, you'll be prompted to specify whether you want to delete all existing content prior to installation.</span></span> <span data-ttu-id="43a95-177">選擇適合您需求的選項，然後按 **[下一步]** 。</span><span class="sxs-lookup"><span data-stu-id="43a95-177">Choose the option that's appropriate for your requirements, and then click **Next**.</span></span>

    ![](manually-installing-web-packages/_static/image6.png)
8. <span data-ttu-id="43a95-178">當 IIS 完成安裝套件時，請按一下 **[完成]** 。</span><span class="sxs-lookup"><span data-stu-id="43a95-178">When IIS has finished installing the package, click **Finish**.</span></span>

    ![](manually-installing-web-packages/_static/image7.png)

<span data-ttu-id="43a95-179">此時，您已成功將 web 應用程式發佈至 IIS。</span><span class="sxs-lookup"><span data-stu-id="43a95-179">At this point, you've successfully published your web application to IIS.</span></span>

## <a name="conclusion"></a><span data-ttu-id="43a95-180">結論</span><span class="sxs-lookup"><span data-stu-id="43a95-180">Conclusion</span></span>

<span data-ttu-id="43a95-181">本主題說明如何使用 IIS 管理員將 web 部署套件匯入 IIS 網站。</span><span class="sxs-lookup"><span data-stu-id="43a95-181">This topic described how to import a web deployment package into an IIS website using IIS Manager.</span></span> <span data-ttu-id="43a95-182">當安全性或基礎結構的條件約束不可能或不想要進行遠端部署時，此 web 應用程式發佈的方法會很適合</span><span class="sxs-lookup"><span data-stu-id="43a95-182">This approach to web application publishing is appropriate when security or infrastructure constraints make remote deployment impossible or undesirable.</span></span>

## <a name="further-reading"></a><span data-ttu-id="43a95-183">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="43a95-183">Further Reading</span></span>

<span data-ttu-id="43a95-184">如需如何設定 IIS web 伺服器以支援手動匯入 web 封裝的指引，請參閱[設定用於 Web Deploy 發佈的 Web 服務器（離線部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="43a95-184">For guidance on how to configure an IIS web server to support manually importing a web package, see [Configure a Web Server for Web Deploy Publishing (Offline Deployment)](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="43a95-185">如需部署 web 套件的一般指引，請參閱[逐步解說：使用 Web 部署封裝部署 Web 應用程式專案（第1部，共4部）](https://msdn.microsoft.com/library/dd483479.aspx)。</span><span class="sxs-lookup"><span data-stu-id="43a95-185">For more general guidance on deploying web packages, see [Walkthrough: Deploying a Web Application Project Using a Web Deployment Package (Part 1 of 4)](https://msdn.microsoft.com/library/dd483479.aspx).</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="43a95-186">上一篇</span><span class="sxs-lookup"><span data-stu-id="43a95-186">Previous</span></span>](creating-and-running-a-deployment-command-file.md)
