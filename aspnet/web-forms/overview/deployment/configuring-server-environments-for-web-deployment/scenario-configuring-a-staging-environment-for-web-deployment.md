---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
title: 案例：設定 Web 部署的預備環境 |Microsoft Docs
author: jrjlee
description: 本主題說明預備環境的一般 web 部署案例，並說明您需要完成才能設定類似 env 的工作 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5a8e49b7-5317-4125-b107-7e2466b47bb3
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: eaa61ca850817f8dd98955b59e94be93389bf256
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637841"
---
# <a name="scenario-configuring-a-staging-environment-for-web-deployment"></a><span data-ttu-id="ffc1a-103">案例：設定 Web 部署的預備環境</span><span class="sxs-lookup"><span data-stu-id="ffc1a-103">Scenario: Configuring a Staging Environment for Web Deployment</span></span>

<span data-ttu-id="ffc1a-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="ffc1a-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="ffc1a-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="ffc1a-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="ffc1a-106">本主題說明預備環境的一般 web 部署案例，並說明您需要完成才能設定類似環境的工作。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-106">This topic describes a typical web deployment scenario for a staging environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>

<span data-ttu-id="ffc1a-107">許多組織會使用預備環境來預覽 web 應用程式或網站的更新。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-107">Lots of organizations use staging environments to preview updates to web applications or websites.</span></span> <span data-ttu-id="ffc1a-108">這讓組織內的人員有機會在網站「上線」之前探索及審查新的功能或內容，換句話說則是部署到生產環境。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-108">This gives people within the organization a chance to explore and review new functionality or content before the site "goes live," or in other words is deployed to a production environment.</span></span> <span data-ttu-id="ffc1a-109">預備環境的設計目的是要盡可能地複寫生產環境，以提供實際的預覽。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-109">The staging environment is designed to replicate the production environment as closely as possible, in order to provide a realistic preview.</span></span> <span data-ttu-id="ffc1a-110">這種預備環境通常具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="ffc1a-110">This kind of staging environment typically has these characteristics:</span></span>

- <span data-ttu-id="ffc1a-111">環境是由多個負載平衡的 web 伺服器和一或多個資料庫伺服器所組成，通常會有容錯移轉叢集和資料庫鏡像。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="ffc1a-112">應用程式可以由開發小組手動部署，或由 Team Build server 自動部署。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-112">Applications may be deployed manually by a development team or automatically by a Team Build server.</span></span>
- <span data-ttu-id="ffc1a-113">部署應用程式的使用者或進程帳戶不太可能會擁有預備伺服器上的系統管理員許可權。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-113">The users or process accounts that deploy applications are unlikely to have administrator privileges on the staging servers.</span></span>
- <span data-ttu-id="ffc1a-114">應用程式的變更會經常部署，因此環境必須支援單一步驟或自動化部署。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-114">Changes to applications are deployed on a frequent basis, so the environment needs to support single-step or automated deployment.</span></span>

> [!NOTE]
> <span data-ttu-id="ffc1a-115">向外擴充多部伺服器上的資料庫部署已超出本教學課程的範圍。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-115">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="ffc1a-116">如需有關此區域的詳細資訊，請參閱[SQL Server 線上叢書](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-116">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>

<span data-ttu-id="ffc1a-117">例如，在我們的[教學課程案例](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，TEAM FOUNDATION SERVER （TFS）會管理 Contact Manager 解決方案。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-117">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), Team Foundation Server (TFS) manages the Contact Manager solution.</span></span> <span data-ttu-id="ffc1a-118">TFS 系統管理員（Walters）已建立組建定義，可讓開發人員視需要觸發對預備環境的部署。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-118">The TFS administrator, Rob Walters, has created a build definition that lets developers trigger a deployment to the staging environment as required.</span></span>

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

<span data-ttu-id="ffc1a-119">請注意，在大部分的情況下，您不一定會想要將最新的組建部署至預備環境。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-119">Note that in most cases, you won't necessarily want to deploy the latest build to the staging environment.</span></span> <span data-ttu-id="ffc1a-120">相反地，您很可能會想要在測試環境中部署已通過驗證和驗證的特定組建。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-120">Instead, you're a lot more likely to want to deploy a specific build that has already undergone validation and verification in the test environment.</span></span>

## <a name="solution-overview"></a><span data-ttu-id="ffc1a-121">方案概觀</span><span class="sxs-lookup"><span data-stu-id="ffc1a-121">Solution Overview</span></span>

<span data-ttu-id="ffc1a-122">在此案例中，您可以從部署需求的分析中推算這些事實：</span><span class="sxs-lookup"><span data-stu-id="ffc1a-122">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="ffc1a-123">執行部署的使用者或進程帳戶不會在預備伺服器上擁有系統管理員許可權，因此預備 web 伺服器必須支援非系統管理員部署。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-123">The user or process account that performs the deployment won't have administrator privileges on the staging servers, so the staging web servers must support non-administrator deployment.</span></span> <span data-ttu-id="ffc1a-124">因此，您必須將預備 web 伺服器設定為使用 Web Deploy 處理常式，而不是遠端代理程式。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-124">As such, you'll need to configure the staging web servers to use the Web Deploy Handler rather than the remote agent.</span></span>
- <span data-ttu-id="ffc1a-125">預備環境包含多部 web 伺服器，但它需要支援單鍵或自動化部署，因此您必須使用 Web 伺服陣列架構（WFF）來建立伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-125">The staging environment includes multiple web servers, but it needs to support one-click or automated deployment, so you'll need to use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="ffc1a-126">使用這種方法，您可以將應用程式部署到一部 web 伺服器（主伺服器），而 WFF 會在預備環境中的所有其他 web 伺服器上複寫部署。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-126">Using this approach, you can deploy an application to one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the staging environment.</span></span>
- <span data-ttu-id="ffc1a-127">執行部署的使用者或進程帳戶必須擁有建立資料庫的許可權。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-127">The user or process account that performs the deployment must have permissions to create databases.</span></span> <span data-ttu-id="ffc1a-128">因此，除了將資料庫伺服器設定為支援遠端存取和部署之外，您還需要將此帳戶新增至資料庫伺服器上的**dbcreator**伺服器角色。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-128">As such, you'll need to add the account to the **dbcreator** server role on the database server, in addition to configuring the database server to support remote access and deployment.</span></span>

<span data-ttu-id="ffc1a-129">這些主題提供完成這些工作所需的所有資訊：</span><span class="sxs-lookup"><span data-stu-id="ffc1a-129">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="ffc1a-130">[使用 Web 伺服陣列架構建立伺服器](creating-a-server-farm-with-the-web-farm-framework.md)陣列。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-130">[Create a Server Farm with the Web Farm Framework](creating-a-server-farm-with-the-web-farm-framework.md).</span></span> <span data-ttu-id="ffc1a-131">本主題說明如何使用 WFF 建立和設定伺服器陣列，以便在多個負載平衡的 web 伺服器之間複寫 web 平台產品和元件、設定和網站和應用程式。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-131">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="ffc1a-132">[設定用於 Web Deploy 發佈的 Web 服務器（Web Deploy 處理常式）](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-132">[Configure a Web Server for Web Deploy Publishing (Web Deploy Handler)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md).</span></span> <span data-ttu-id="ffc1a-133">本主題說明如何使用遠端代理程式方法（從全新的 Windows Server 2008 R2 組建開始），建立支援 Web Deploy 發行的網頁伺服器。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-133">This topic describes how to build a web server that supports Web Deploy publishing, using the remote agent approach, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="ffc1a-134">[設定資料庫伺服器以進行 Web Deploy 發行](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-134">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="ffc1a-135">本主題說明如何設定資料庫伺服器，以支援遠端存取和部署，從預設安裝的 SQL Server 2008 R2 開始。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-135">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="ffc1a-136">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="ffc1a-136">Further Reading</span></span>

<span data-ttu-id="ffc1a-137">如需設定一般開發人員測試環境的指引，請參閱[案例：設定 Web 部署的測試環境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-137">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="ffc1a-138">如需設定一般生產環境的指引，請參閱[案例：設定 Web 部署的生產環境](scenario-configuring-a-production-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="ffc1a-138">For guidance on configuring a typical production environment, see [Scenario: Configuring a Production Environment for Web Deployment](scenario-configuring-a-production-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="ffc1a-139">[上一頁](scenario-configuring-a-test-environment-for-web-deployment.md)
> [下一頁](scenario-configuring-a-production-environment-for-web-deployment.md)</span><span class="sxs-lookup"><span data-stu-id="ffc1a-139">[Previous](scenario-configuring-a-test-environment-for-web-deployment.md)
[Next](scenario-configuring-a-production-environment-for-web-deployment.md)</span></span>
