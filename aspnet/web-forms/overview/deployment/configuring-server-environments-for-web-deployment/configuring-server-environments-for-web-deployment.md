---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
title: 設定 Web 部署的伺服器環境 |Microsoft Docs
author: jrjlee
description: 本教學課程將說明如何設定伺服器環境，以在各種不同的 scen 中支援單鍵或自動化的網站部署和發佈 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 0bf0959b-4ca8-45de-bd13-b15347543b5a
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 073161ce4faa3b7ba6749d7dfbaa5309eeca4f74
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634467"
---
# <a name="configuring-server-environments-for-web-deployment"></a><span data-ttu-id="8f12d-103">設定 Web 部署的伺服器環境</span><span class="sxs-lookup"><span data-stu-id="8f12d-103">Configuring Server Environments for Web Deployment</span></span>

<span data-ttu-id="8f12d-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="8f12d-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="8f12d-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="8f12d-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="8f12d-106">本教學課程將說明如何設定伺服器環境，以在各種不同的案例中支援單鍵或自動化的網站部署和發佈。</span><span class="sxs-lookup"><span data-stu-id="8f12d-106">This tutorial will show you how to set up server environments to support one-click, or automated, website deployment and publishing in various different scenarios.</span></span> <span data-ttu-id="8f12d-107">本教學課程包含的主題可引導您完成各種工作，例如設定 web 伺服器以支援部署和設定 Web 伺服陣列架構（WFF）伺服器陣列的特定方法，以及提供較高層級的端對端指引。</span><span class="sxs-lookup"><span data-stu-id="8f12d-107">The tutorial includes topics to walk you through completing various tasks, like configuring a web server to support specific approaches to deployment and setting up a Web Farm Framework (WFF) server farm, together with scenario-based overviews that provide higher-level end-to-end guidance.</span></span>
> 
> <span data-ttu-id="8f12d-108">本教學課程使用「[企業 Web 部署：案例總覽](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)」中所述的 Fabrikam，inc. 部署案例，做為範例和網路基礎結構的參考點。</span><span class="sxs-lookup"><span data-stu-id="8f12d-108">The tutorial uses the Fabrikam, Inc. deployment scenario described in [Enterprise Web Deployment: Scenario Overview](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md) as a reference point for examples and network infrastructure.</span></span>
> 
> <span data-ttu-id="8f12d-109">如需這些教學課程的義大利文翻譯，請造訪[http://www.lucamorelli.it](http://www.lucamorelli.it)。</span><span class="sxs-lookup"><span data-stu-id="8f12d-109">For an Italian translation of these tutorials, visit [http://www.lucamorelli.it](http://www.lucamorelli.it).</span></span>

<span data-ttu-id="8f12d-110">本教學課程包含下列主題：</span><span class="sxs-lookup"><span data-stu-id="8f12d-110">This tutorial includes these topics:</span></span>

- [<span data-ttu-id="8f12d-111">選擇 Web 部署的正確方法</span><span class="sxs-lookup"><span data-stu-id="8f12d-111">Choosing the Right Approach to Web Deployment</span></span>](choosing-the-right-approach-to-web-deployment.md)
- [<span data-ttu-id="8f12d-112">案例：設定 Web 部署的測試環境</span><span class="sxs-lookup"><span data-stu-id="8f12d-112">Scenario: Configuring a Test Environment for Web Deployment</span></span>](scenario-configuring-a-test-environment-for-web-deployment.md)
- [<span data-ttu-id="8f12d-113">案例：設定 Web 部署的預備環境</span><span class="sxs-lookup"><span data-stu-id="8f12d-113">Scenario: Configuring a Staging Environment for Web Deployment</span></span>](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [<span data-ttu-id="8f12d-114">案例：設定 Web 部署的生產環境</span><span class="sxs-lookup"><span data-stu-id="8f12d-114">Scenario: Configuring a Production Environment for Web Deployment</span></span>](scenario-configuring-a-production-environment-for-web-deployment.md)
- [<span data-ttu-id="8f12d-115">設定 Web Deploy 發行的網頁伺服器 (遠端代理程式)</span><span class="sxs-lookup"><span data-stu-id="8f12d-115">Configuring a Web Server for Web Deploy Publishing (Remote Agent)</span></span>](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [<span data-ttu-id="8f12d-116">設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)</span><span class="sxs-lookup"><span data-stu-id="8f12d-116">Configuring a Web Server for Web Deploy Publishing (Web Deploy Handler)</span></span>](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [<span data-ttu-id="8f12d-117">設定 Web Deploy 發行的網頁伺服器 (離線部署)</span><span class="sxs-lookup"><span data-stu-id="8f12d-117">Configuring a Web Server for Web Deploy Publishing (Offline Deployment)</span></span>](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [<span data-ttu-id="8f12d-118">設定 Web Deploy 發行的資料庫伺服器</span><span class="sxs-lookup"><span data-stu-id="8f12d-118">Configuring a Database Server for Web Deploy Publishing</span></span>](configuring-a-database-server-for-web-deploy-publishing.md)
- [<span data-ttu-id="8f12d-119">使用 Web 伺服陣列架構建立伺服器陣列</span><span class="sxs-lookup"><span data-stu-id="8f12d-119">Creating a Server Farm with the Web Farm Framework</span></span>](creating-a-server-farm-with-the-web-farm-framework.md)
- [<span data-ttu-id="8f12d-120">設定目標環境的部署屬性</span><span class="sxs-lookup"><span data-stu-id="8f12d-120">Configuring Deployment Properties for a Target Environment</span></span>](configuring-deployment-properties-for-a-target-environment.md)

<span data-ttu-id="8f12d-121">第一個主題[選擇 Web 部署的正確方法](choosing-the-right-approach-to-web-deployment.md)，說明您可以使用 INTERNET INFORMATION SERVICES （IIS） Web 部署工具（Web Deploy）2.0 來發行 web 應用程式的主要方法。</span><span class="sxs-lookup"><span data-stu-id="8f12d-121">The first topic, [Choosing the Right Approach to Web Deployment](choosing-the-right-approach-to-web-deployment.md), describes the main approaches you can use to publish web applications by using the Internet Information Services (IIS) Web Deployment Tool (Web Deploy) 2.0.</span></span> <span data-ttu-id="8f12d-122">它也會識別對應至每個方法的案例。</span><span class="sxs-lookup"><span data-stu-id="8f12d-122">It also identifies the scenarios that map to each approach.</span></span> <span data-ttu-id="8f12d-123">從這裡開始，每個案例主題都會提供完成所需工作的高階總覽，並識別您需要進行的主題，以協助您完成這些作業。</span><span class="sxs-lookup"><span data-stu-id="8f12d-123">From here, each scenario topic provides a high-level overview of the tasks you need to complete and identifies the topics you'll need to work through to help you complete these tasks.</span></span>

<span data-ttu-id="8f12d-124">如果您使用瞭解建立及部署方案[的組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述的分割專案檔方法，最後一個主題[設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)，說明如何設定環境特定的專案檔，以部署至不同的目的地環境。</span><span class="sxs-lookup"><span data-stu-id="8f12d-124">If you're using the split project file approach described in [Understanding the Build Process](../web-deployment-in-the-enterprise/understanding-the-build-process.md) to build and deploy your solution, the final topic, [Configuring Deployment Properties for a Target Environment](configuring-deployment-properties-for-a-target-environment.md), describes how to configure environment-specific project files for deployment to different destination environments.</span></span>

## <a name="key-technologies"></a><span data-ttu-id="8f12d-125">重要技術</span><span class="sxs-lookup"><span data-stu-id="8f12d-125">Key Technologies</span></span>

<span data-ttu-id="8f12d-126">本教學課程著重于如何使用這些產品和技術來支援 web 部署：</span><span class="sxs-lookup"><span data-stu-id="8f12d-126">This tutorial focuses on how to use these products and technologies to support web deployment:</span></span>

- <span data-ttu-id="8f12d-127">IIS 7。5</span><span class="sxs-lookup"><span data-stu-id="8f12d-127">IIS 7.5</span></span>
- <span data-ttu-id="8f12d-128">Web Deploy 2。x</span><span class="sxs-lookup"><span data-stu-id="8f12d-128">Web Deploy 2.x</span></span>
- <span data-ttu-id="8f12d-129">WFF 2。x</span><span class="sxs-lookup"><span data-stu-id="8f12d-129">WFF 2.x</span></span>
- <span data-ttu-id="8f12d-130">IIS Web 管理服務（WMSvc）</span><span class="sxs-lookup"><span data-stu-id="8f12d-130">IIS Web Management Service (WMSvc)</span></span>

<span data-ttu-id="8f12d-131">本教學課程也會說明 Windows Server 2008 R2、SQL Server 2008 R2、ASP.NET 4.0 和 ASP.NET MVC 3 的使用。</span><span class="sxs-lookup"><span data-stu-id="8f12d-131">The tutorial also touches on the use of Windows Server 2008 R2, SQL Server 2008 R2, ASP.NET 4.0, and ASP.NET MVC 3.</span></span>

## <a name="other-tutorials-in-this-series"></a><span data-ttu-id="8f12d-132">本系列的其他教學課程</span><span class="sxs-lookup"><span data-stu-id="8f12d-132">Other Tutorials in This Series</span></span>

<span data-ttu-id="8f12d-133">這會形成一系列五個企業級 web 部署教學課程的一部分。</span><span class="sxs-lookup"><span data-stu-id="8f12d-133">This forms part of a series of five tutorials on enterprise-scale web deployment.</span></span> <span data-ttu-id="8f12d-134">這些是系列中的其他教學課程：</span><span class="sxs-lookup"><span data-stu-id="8f12d-134">These are the other tutorials in the series:</span></span>

- <span data-ttu-id="8f12d-135">[在企業案例中部署 Web 應用程式](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。</span><span class="sxs-lookup"><span data-stu-id="8f12d-135">[Deploying Web Applications in Enterprise Scenarios](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md).</span></span> <span data-ttu-id="8f12d-136">此簡介內容會提供教學課程系列的上下文背景。</span><span class="sxs-lookup"><span data-stu-id="8f12d-136">This introductory content provides the contextual background for the tutorial series.</span></span> <span data-ttu-id="8f12d-137">其中說明教學課程案例，並說明整個系列中所述的工作和逐步解說如何符合更廣泛的應用程式生命週期管理（ALM）流程。</span><span class="sxs-lookup"><span data-stu-id="8f12d-137">It describes the tutorial scenario, and it illustrates how the tasks and walkthroughs described throughout the series fit into a broader Application Lifecycle Management (ALM) process.</span></span>
- <span data-ttu-id="8f12d-138">[企業中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。</span><span class="sxs-lookup"><span data-stu-id="8f12d-138">[Web Deployment in the Enterprise](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md).</span></span> <span data-ttu-id="8f12d-139">本教學課程提供 Microsoft Build Engine （MSBuild）專案檔、Web 發佈管線、Web Deploy 和其他相關技術的概念介紹。</span><span class="sxs-lookup"><span data-stu-id="8f12d-139">This tutorial provides a conceptual introduction to Microsoft Build Engine (MSBuild) project files, the Web Publishing Pipeline, Web Deploy, and other related technologies.</span></span> <span data-ttu-id="8f12d-140">它會說明如何搭配使用這些工具來管理複雜的部署流程。</span><span class="sxs-lookup"><span data-stu-id="8f12d-140">It explains how you can use these tools together to manage complex deployment processes.</span></span>
- <span data-ttu-id="8f12d-141">[正在設定 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="8f12d-141">[Configuring Team Foundation Server for Web Deployment](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md).</span></span> <span data-ttu-id="8f12d-142">本教學課程說明如何設定 Team Foundation Server （TFS）以支援各種部署案例，包括自動部署作為持續整合（CI）程式的一部分，以及手動觸發特定組建的部署。</span><span class="sxs-lookup"><span data-stu-id="8f12d-142">This tutorial describes how to configure Team Foundation Server (TFS) to support various deployment scenarios, including automated deployment as part of a continuous integration (CI) process and manually triggered deployments of specific builds.</span></span>
- <span data-ttu-id="8f12d-143">[先進的企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="8f12d-143">[Advanced Enterprise Web Deployment](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md).</span></span> <span data-ttu-id="8f12d-144">本教學課程說明如何完成各種更先進的部署工作，例如自訂多個環境的資料庫部署、從部署中排除檔案和資料夾，以及在部署過程中讓 web 應用程式離線.</span><span class="sxs-lookup"><span data-stu-id="8f12d-144">This tutorial describes how to accomplish various more advanced deployment tasks, like customizing database deployments for multiple environments, excluding files and folders from deployment, and taking web applications offline during the deployment process.</span></span>

> [!div class="step-by-step"]
> [<span data-ttu-id="8f12d-145">下一個</span><span class="sxs-lookup"><span data-stu-id="8f12d-145">Next</span></span>](choosing-the-right-approach-to-web-deployment.md)
