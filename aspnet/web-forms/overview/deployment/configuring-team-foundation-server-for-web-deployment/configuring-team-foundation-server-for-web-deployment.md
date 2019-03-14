---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: 設定 Web 部署的 Team Foundation Server |Microsoft Docs
author: jrjlee
description: 本教學課程會示範如何設定 Team Foundation Server (TFS) 2010年建置解決方案，並將 web 內容部署至各種目標環境。 這...
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2b668f2e9bdf73632b8b076416c9ccc5cf34a7ed
ms.sourcegitcommit: 24b1f6decbb17bb22a45166e5fdb0845c65af498
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/01/2019
ms.locfileid: "57058825"
---
<a name="configuring-team-foundation-server-for-web-deployment"></a><span data-ttu-id="f6ca9-104">設定 Web 部署的 Team Foundation Server</span><span class="sxs-lookup"><span data-stu-id="f6ca9-104">Configuring Team Foundation Server for Web Deployment</span></span>
====================
<span data-ttu-id="f6ca9-105">藉由[Jason Lee](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="f6ca9-105">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="f6ca9-106">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="f6ca9-106">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="f6ca9-107">本教學課程會示範如何設定 Team Foundation Server (TFS) 2010年建置解決方案，並將 web 內容部署至各種目標環境。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-107">This tutorial will show you how to configure Team Foundation Server (TFS) 2010 to build solutions and deploy web content to various target environments.</span></span> <span data-ttu-id="f6ca9-108">這包括持續整合 (CI) 案例中，您在其中部署內容會自動每次為開發人員進行變更。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-108">This includes continuous integration (CI) scenarios, where you deploy content automatically every time a developer makes a change.</span></span> <span data-ttu-id="f6ca9-109">它也可以包含手動觸發程序的情況下，系統管理員可能要觸發部署至預備環境之特定組建，一旦確認並驗證測試環境中建置。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-109">It can also include manual trigger scenarios, where an administrator may want to trigger deployment of a specific build to a staging environment once the build has been verified and validated in the test environment.</span></span> <span data-ttu-id="f6ca9-110">在本教學課程的主題將引導您完成整個組態程序，包括：</span><span class="sxs-lookup"><span data-stu-id="f6ca9-110">The topics in this tutorial will guide you through the entire configuration process, including:</span></span>
> 
> - <span data-ttu-id="f6ca9-111">如何在 TFS 中建立新的 team 專案。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-111">How to create a new team project in TFS.</span></span>
> - <span data-ttu-id="f6ca9-112">如何將內容新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-112">How to add content to source control.</span></span>
> - <span data-ttu-id="f6ca9-113">如何設定為支援 CI 及部署組建伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-113">How to configure a build server to support CI and deployment.</span></span>
> - <span data-ttu-id="f6ca9-114">如何建立組建定義，其中包含部署邏輯。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-114">How to create a build definition that includes deployment logic.</span></span>
> - <span data-ttu-id="f6ca9-115">如何設定自動化部署的權限。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-115">How to configure permissions for automated deployment.</span></span>
> 
> <span data-ttu-id="f6ca9-116">這些教學課程義大利文翻譯，請瀏覽[ http://www.lucamorelli.it ](http://www.lucamorelli.it)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-116">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>


<span data-ttu-id="f6ca9-117">本教學課程假設您安裝 TFS 2010，並建立 team 專案集合初始設定程序的一部分。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-117">This tutorial assumes that you have installed TFS 2010 and created a team project collection as part of the initial configuration process.</span></span> <span data-ttu-id="f6ca9-118">[適用於 Visual Studio 2010 Team Foundation 安裝指南](https://go.microsoft.com/?linkid=9805132)提供這些工作的完整指導。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-118">The [Team Foundation Installation Guide for Visual Studio 2010](https://go.microsoft.com/?linkid=9805132) provides comprehensive guidance on these tasks.</span></span>

## <a name="context"></a><span data-ttu-id="f6ca9-119">內容</span><span class="sxs-lookup"><span data-stu-id="f6ca9-119">Context</span></span>

<span data-ttu-id="f6ca9-120">這會形成名為 Fabrikam，Inc.的虛構公司的企業部署需求為基礎的教學課程系列的一部分本系列教學課程使用範例解決方案&#x2014; [Contactmanager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)方案&#x2014;來代表實際的層級的複雜性，包括 ASP.NET MVC 3 應用程式時，Windows Communication 的 web 應用程式Foundation (WCF) 服務與資料庫專案。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-120">This forms part of a series of tutorials based on the enterprise deployment requirements of a fictional company named Fabrikam, Inc. This tutorial series uses a sample solution&#x2014;the [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md) solution&#x2014;to represent a web application with a realistic level of complexity, including an ASP.NET MVC 3 application, a Windows Communication Foundation (WCF) service, and a database project.</span></span>

<span data-ttu-id="f6ca9-121">這些教學課程的核心的部署方法根據分割專案檔案方法中所述[了解建置程序](../web-deployment-in-the-enterprise/understanding-the-build-process.md)，在建置流程控制的兩個專案檔&#x2014;包含建置適用於每個目的地環境中和包含環境特定建置和部署設定的指示。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-121">The deployment method at the heart of these tutorials is based on the split project file approach described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md), in which the build process is controlled by two project files&#x2014;one containing build instructions that apply to every destination environment, and one containing environment-specific build and deployment settings.</span></span> <span data-ttu-id="f6ca9-122">在建置階段的特定環境的專案檔會合併到無從驗證環境的專案檔中，以構成一組完整的組建指示。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-122">At build time, the environment-specific project file is merged into the environment-agnostic project file to form a complete set of build instructions.</span></span>

## <a name="scenario-overview"></a><span data-ttu-id="f6ca9-123">情節概觀</span><span class="sxs-lookup"><span data-stu-id="f6ca9-123">Scenario Overview</span></span>

<span data-ttu-id="f6ca9-124">高階的案例，這些教學課程中所述[企業 Web 部署：案例概觀](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-124">The high-level scenario for these tutorials is described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md).</span></span> <span data-ttu-id="f6ca9-125">我們建議您檢閱本主題，再開始本教學課程。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-125">We recommend that you review this topic before you get started on this tutorial.</span></span>

## <a name="how-to-use-this-tutorial"></a><span data-ttu-id="f6ca9-126">如何使用本教學課程</span><span class="sxs-lookup"><span data-stu-id="f6ca9-126">How to Use This Tutorial</span></span>

<span data-ttu-id="f6ca9-127">如果這是第一次您執行本教學課程中所述的工作，或如果您想要遵循的使用範例方案的範例，您應該逐步教學課程主題中的順序。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-127">If this is the first time you've performed the tasks described in this tutorial, or if you want to follow the examples using the sample solution, you should work through the tutorial topics in order.</span></span> <span data-ttu-id="f6ca9-128">或者，您可以使用做為指導的個別主題，適用於特定工作。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-128">Alternatively, you can use individual topics as guidance for specific tasks.</span></span> <span data-ttu-id="f6ca9-129">本教學課程包含下列主題：</span><span class="sxs-lookup"><span data-stu-id="f6ca9-129">This tutorial includes these topics:</span></span>

- <span data-ttu-id="f6ca9-130">[在 TFS 中建立 Team 專案](creating-a-team-project-in-tfs.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-130">[Creating a Team Project in TFS](creating-a-team-project-in-tfs.md).</span></span> <span data-ttu-id="f6ca9-131">Team 專案是原始檔控制、 程序管理，以及在 TFS 中的組建的核心單位。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-131">A team project is the core unit for source control, process management, and build in TFS.</span></span> <span data-ttu-id="f6ca9-132">您需要建立 team 專案，您可以將內容加入至原始檔控制，或建立組建定義之前。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-132">You need to create a team project before you can add content to source control or create build definitions.</span></span>
- <span data-ttu-id="f6ca9-133">[將內容新增至原始檔控制](adding-content-to-source-control.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-133">[Adding Content to Source Control](adding-content-to-source-control.md).</span></span> <span data-ttu-id="f6ca9-134">一旦您建立 team 專案，您可以開始將內容新增至原始檔控制。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-134">Once you've created a team project, you can start adding content to source control.</span></span> <span data-ttu-id="f6ca9-135">您必須加入您的專案和方案，以及任何外部的相依性，才能開始設定組建。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-135">You'll need to add your projects and solutions, together with any external dependencies, before you can start configuring builds.</span></span>
- <span data-ttu-id="f6ca9-136">[設定 TFS 組建伺服器，Web 部署](configuring-a-tfs-build-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-136">[Configuring a TFS Build Server for Web Deployment](configuring-a-tfs-build-server-for-web-deployment.md).</span></span> <span data-ttu-id="f6ca9-137">如果您想要建置您的 team 專案內容，您必須設定組建伺服器。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-137">If you want to build your team project content, you'll need to configure a build server.</span></span> <span data-ttu-id="f6ca9-138">在大部分情況下，這應該是從您的 TFS 安裝在不同電腦上。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-138">In most cases, this should be on a separate machine from your TFS installation.</span></span> <span data-ttu-id="f6ca9-139">若要設定組建伺服器，您需要安裝及設定 TFS 組建服務，安裝 Visual Studio 2010 中，建立組建控制器和組建代理程式，安裝任何產品或您的程式碼能夠成功建置，並安裝的元件Internet Information Services (IIS) Web Deployment Tool (Web Deploy)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-139">To configure a build server, you need to install and configure the TFS build service, install Visual Studio 2010, create build controllers and build agents, install any products or components that your code needs in order to build successfully, and install the Internet Information Services (IIS) Web Deployment Tool (Web Deploy).</span></span>
- <span data-ttu-id="f6ca9-140">[建立組建定義支援部署](creating-a-build-definition-that-supports-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-140">[Creating a Build Definition That Supports Deployment](creating-a-build-definition-that-supports-deployment.md).</span></span> <span data-ttu-id="f6ca9-141">您可以在佇列或觸發在 TFS 組建啟動之前，您需要建立 team 專案的至少一個組建定義。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-141">Before you can start queuing or triggering builds in TFS, you need to create at least one build definition for your team project.</span></span> <span data-ttu-id="f6ca9-142">組建定義會定義組建，包括哪些項目應該包含在組建中，應該會觸發組建，以及 Team Build 應該其中傳送組建輸出的各個層面。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-142">The build definition defines every aspect of the build, including which things should be included in the build, what should trigger the build, and where Team Build should send the build outputs.</span></span> <span data-ttu-id="f6ca9-143">您可以設定組建定義，執行自訂的 Microsoft Build Engine (MSBuild) 專案檔，可讓您將部署邏輯包含在您的自動化組建。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-143">You can configure a build definition to run custom Microsoft Build Engine (MSBuild) project files, which lets you include deployment logic in your automated builds.</span></span>
- <span data-ttu-id="f6ca9-144">[部署特定的組建](deploying-a-specific-build.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-144">[Deploying a Specific Build](deploying-a-specific-build.md).</span></span> <span data-ttu-id="f6ca9-145">在許多案例中，您會想要將特定的組建，而不是最新的組建部署至目標環境。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-145">In a lot of scenarios, you'll want to deploy a specific build, rather than the latest build, to a target environment.</span></span> <span data-ttu-id="f6ca9-146">在此情況下，您可以設定將從特定的置放資料夾的內容部署的組建定義。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-146">In this case, you can configure a build definition that deploys content from a specific drop folder.</span></span>
- <span data-ttu-id="f6ca9-147">[設定權限的小組組建部署](configuring-permissions-for-team-build-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-147">[Configuring Permissions for Team Build Deployment](configuring-permissions-for-team-build-deployment.md).</span></span> <span data-ttu-id="f6ca9-148">如果組建服務將內容部署自動化的建置程序的一部分，您需要授與至任何目的地 web 伺服器和資料庫伺服器上組建服務帳戶的各種權限。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-148">If the build service is to deploy content as part of an automated build process, you need to grant various permissions to the build service account on any destination web servers and database servers.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="f6ca9-149">主要技術</span><span class="sxs-lookup"><span data-stu-id="f6ca9-149">Key Technologies</span></span>

<span data-ttu-id="f6ca9-150">本教學課程著重於如何使用這些產品和技術來支援自動化的建置和 web 部署：</span><span class="sxs-lookup"><span data-stu-id="f6ca9-150">This tutorial focuses on how to use these products and technologies to support automated build and web deployment:</span></span>

- <span data-ttu-id="f6ca9-151">Visual Studio Team Foundation Server 2010</span><span class="sxs-lookup"><span data-stu-id="f6ca9-151">Visual Studio Team Foundation Server 2010</span></span>
- <span data-ttu-id="f6ca9-152">Team Build 和 MSBuild</span><span class="sxs-lookup"><span data-stu-id="f6ca9-152">Team Build and MSBuild</span></span>
- <span data-ttu-id="f6ca9-153">Web Deploy</span><span class="sxs-lookup"><span data-stu-id="f6ca9-153">Web Deploy</span></span>

<span data-ttu-id="f6ca9-154">本教學課程也會牽涉到使用 Windows Server 2008 R2、 IIS 7.5、 SQL Server 2008 R2、 ASP.NET 4.0 和 ASP.NET MVC 3。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-154">The tutorial also touches on the use of Windows Server 2008 R2, IIS 7.5, SQL Server 2008 R2, ASP.NET 4.0, and ASP.NET MVC 3.</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="f6ca9-155">在這一系列的其他教學課程</span><span class="sxs-lookup"><span data-stu-id="f6ca9-155">Other Tutorials in This Series</span></span>

<span data-ttu-id="f6ca9-156">這會形成企業級 web 部署的一系列五個教學課程的一部分。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-156">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="f6ca9-157">這些是系列中的其他教學課程：</span><span class="sxs-lookup"><span data-stu-id="f6ca9-157">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="f6ca9-158">[部署 Web 應用程式，在企業案例](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-158">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="f6ca9-159">此介紹的內容會提供教學課程系列中的內容相關的背景。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-159">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="f6ca9-160">其中說明教學課程的案例中，並說明了如何工作和逐步解說所述，在整個系列納入更廣泛的應用程式生命週期管理 (ALM) 程序。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-160">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="f6ca9-161">[Web 部署在企業中的](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-161">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="f6ca9-162">本教學課程提供 MSBuild 專案檔的概念性簡介、 Web 發行管線 (WPP)、 Web Deploy 和其他相關的技術。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-162">This tutorial provides a conceptual introduction to MSBuild project files, the Web Publishing Pipeline (WPP), Web Deploy, and other related technologies.</span></span> <span data-ttu-id="f6ca9-163">它說明如何使用這些工具搭配來管理複雜的部署程序。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-163">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="f6ca9-164">[設定 Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-164">[Configuring Server Environments for Web Deployment](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md).</span></span> <span data-ttu-id="f6ca9-165">本教學課程說明如何設定 Windows 伺服器以支援各種部署案例，包括使用 Web Deployment Agent Service （遠端代理程式） 或 Web 部署的處理常式和遠端資料庫部署的遠端 web 套件部署。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-165">This tutorial describes how to configure Windows servers to support various deployment scenarios, including remote web package deployment using the Web Deployment Agent Service (the remote agent) or the Web Deploy Handler and remote database deployment.</span></span> <span data-ttu-id="f6ca9-166">它提供指導方針選擇適當的部署方法，為您自己的環境，並說明如何使用 Web 伺服陣列架構 (WFF) 伺服器陣列中的所有 web 伺服器之間複寫已部署的 web 應用程式。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-166">It provides guidance on choosing the appropriate deployment method for your own environment, and it describes how to use the Web Farm Framework (WFF) to replicate deployed web applications across all the web servers in a server farm.</span></span>
- <span data-ttu-id="f6ca9-167">[進階企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="f6ca9-167">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="f6ca9-168">本教學課程說明如何完成各種進階的部署工作，例如自訂多個環境的資料庫部署、 從部署中排除檔案和資料夾以及部署程序期間取得 web 應用程式離線.</span><span class="sxs-lookup"><span data-stu-id="f6ca9-168">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="f6ca9-169">下一步</span><span class="sxs-lookup"><span data-stu-id="f6ca9-169">Next</span></span>](creating-a-team-project-in-tfs.md)