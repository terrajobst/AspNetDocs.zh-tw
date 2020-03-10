---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
title: 案例：設定 Web 部署的生產環境 |Microsoft Docs
author: jrjlee
description: 本主題說明生產環境的一般 web 部署案例，並說明您需要完成的工作，才能設定類似的 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 2e861511-450e-4752-a61e-4a01933f9b6e
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 2d76e715cdbf6ec484fa0ff98b3b3d1d8dfd3961
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78635419"
---
# <a name="scenario-configuring-a-production-environment-for-web-deployment"></a><span data-ttu-id="0742c-103">案例：設定 Web 部署的生產環境</span><span class="sxs-lookup"><span data-stu-id="0742c-103">Scenario: Configuring a Production Environment for Web Deployment</span></span>

<span data-ttu-id="0742c-104">[Jason 先生](https://github.com/jrjlee)</span><span class="sxs-lookup"><span data-stu-id="0742c-104">by [Jason Lee](https://github.com/jrjlee)</span></span>

[<span data-ttu-id="0742c-105">下載 PDF</span><span class="sxs-lookup"><span data-stu-id="0742c-105">Download PDF</span></span>](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> <span data-ttu-id="0742c-106">本主題說明生產環境的一般 web 部署案例，並說明您需要完成才能設定類似環境的工作。</span><span class="sxs-lookup"><span data-stu-id="0742c-106">This topic describes a typical web deployment scenario for a production environment and explains the tasks you need to complete in order to set up a similar environment.</span></span>

<span data-ttu-id="0742c-107">生產環境是 web 應用程式或網站的最終目的地。</span><span class="sxs-lookup"><span data-stu-id="0742c-107">The production environment is the final destination for a web application or a website.</span></span> <span data-ttu-id="0742c-108">此時，您的應用程式已通過測試，已部署至預備環境，並已準備好「上線」。</span><span class="sxs-lookup"><span data-stu-id="0742c-108">By this point, your application has been through testing, has been deployed to a staging environment, and is ready to "go live."</span></span> <span data-ttu-id="0742c-109">生產環境的特性可能會根據 web 內容的本質和用途、您的組織規模、目標物件和許多其他因素而有很大的差異。</span><span class="sxs-lookup"><span data-stu-id="0742c-109">The characteristics of a production environment can vary widely according to the nature and purpose of your web content, the size of your organization, your target audience, and lots of other factors.</span></span> <span data-ttu-id="0742c-110">在企業規模的案例中，生產環境可能具有下列特性：</span><span class="sxs-lookup"><span data-stu-id="0742c-110">In an enterprise-scale scenario, the production environment may have these characteristics:</span></span>

- <span data-ttu-id="0742c-111">環境是由多個負載平衡的 web 伺服器和一或多個資料庫伺服器所組成，通常會有容錯移轉叢集和資料庫鏡像。</span><span class="sxs-lookup"><span data-stu-id="0742c-111">The environment consists of multiple load-balanced web servers and one or more database servers, often with failover clustering and database mirroring.</span></span>
- <span data-ttu-id="0742c-112">如果環境是網際網路對向，則可能會與您的內部網路隔離。</span><span class="sxs-lookup"><span data-stu-id="0742c-112">If the environment is Internet-facing, it's likely to be segregated from your internal network.</span></span> <span data-ttu-id="0742c-113">它可能位於周邊網路中的不同子網，它可能位於不同的網域，而且可能位於完全不同的網路基礎結構上。</span><span class="sxs-lookup"><span data-stu-id="0742c-113">It may be on a different subnet in a perimeter network, it may be on a different domain, and it may be on an entirely different network infrastructure.</span></span>
- <span data-ttu-id="0742c-114">開發人員和組建伺服器進程帳戶在實際執行伺服器上的系統管理員許可權非常不太可能。</span><span class="sxs-lookup"><span data-stu-id="0742c-114">Developers and build server process accounts are highly unlikely to have administrator privileges on the production servers.</span></span>
- <span data-ttu-id="0742c-115">應用程式的變更會以較不頻繁的方式部署，而不是測試或預備部署。</span><span class="sxs-lookup"><span data-stu-id="0742c-115">Changes to applications are deployed on a less frequent basis than test or staging deployments.</span></span>

> [!NOTE]
> <span data-ttu-id="0742c-116">向外擴充多部伺服器上的資料庫部署已超出本教學課程的範圍。</span><span class="sxs-lookup"><span data-stu-id="0742c-116">Scaling out a database deployment across multiple servers is beyond the scope of this tutorial.</span></span> <span data-ttu-id="0742c-117">如需有關此區域的詳細資訊，請參閱[SQL Server 線上叢書](https://technet.microsoft.com/library/ms130214.aspx)。</span><span class="sxs-lookup"><span data-stu-id="0742c-117">For more information on this area, please consult [SQL Server Books Online](https://technet.microsoft.com/library/ms130214.aspx).</span></span>

<span data-ttu-id="0742c-118">例如，在我們的[教學課程案例](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，Team Build server 包含組建定義，可讓使用者在單一步驟中建立 Contact Manager 解決方案，並將其部署至預備環境。</span><span class="sxs-lookup"><span data-stu-id="0742c-118">For example, in our [tutorial scenario](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md), a Team Build server includes build definitions that let users build the Contact Manager solution and deploy it to a staging environment in a single step.</span></span> <span data-ttu-id="0742c-119">當應用程式準備好要部署到生產環境時，由於安全性需求和網路基礎結構的條件約束，生產環境管理員必須手動將 web 套件複製到生產 web 伺服器並匯入它透過 Internet Information Services （IIS）管理員。</span><span class="sxs-lookup"><span data-stu-id="0742c-119">When the application is ready to be deployed to production, due to the constraints imposed by security requirements and the network infrastructure, the production environment administrator must manually copy the web package onto a production web server and import it through Internet Information Services (IIS) Manager.</span></span>

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a><span data-ttu-id="0742c-120">方案概觀</span><span class="sxs-lookup"><span data-stu-id="0742c-120">Solution Overview</span></span>

<span data-ttu-id="0742c-121">在此案例中，您可以從部署需求的分析中推算這些事實：</span><span class="sxs-lookup"><span data-stu-id="0742c-121">In this scenario, you can deduce these facts from an analysis of the deployment requirements:</span></span>

- <span data-ttu-id="0742c-122">由於安全性限制和網路設定，您無法將生產環境設定為支援單鍵或自動化部署。</span><span class="sxs-lookup"><span data-stu-id="0742c-122">Due to security restrictions and the network configuration, you can't configure the production environment to support one-click or automated deployment.</span></span> <span data-ttu-id="0742c-123">在此案例中，離線部署是唯一可行的方法。</span><span class="sxs-lookup"><span data-stu-id="0742c-123">Offline deployment is the only viable approach in this scenario.</span></span>
- <span data-ttu-id="0742c-124">生產環境包含多部 web 伺服器，因此您可以使用 Web 伺服陣列架構（WFF）來建立伺服器陣列。</span><span class="sxs-lookup"><span data-stu-id="0742c-124">The production environment includes multiple web servers, so you can use the Web Farm Framework (WFF) to create a server farm.</span></span> <span data-ttu-id="0742c-125">使用這種方法時，系統管理員只需要將應用程式匯入到一部 web 伺服器（主伺服器），WFF 就會將部署複寫到生產環境中的所有其他 web 伺服器上。</span><span class="sxs-lookup"><span data-stu-id="0742c-125">Using this approach, the administrator only needs to import the application onto one web server (the primary server), and WFF will replicate the deployment on all the other web servers in the production environment.</span></span>

<span data-ttu-id="0742c-126">這些主題提供完成這些工作所需的所有資訊：</span><span class="sxs-lookup"><span data-stu-id="0742c-126">These topics provide all the information you need in order to complete these tasks:</span></span>

- <span data-ttu-id="0742c-127">[使用 Web 伺服陣列架構建立伺服器](configuring-a-database-server-for-web-deploy-publishing.md)陣列。</span><span class="sxs-lookup"><span data-stu-id="0742c-127">[Create a Server Farm with the Web Farm Framework](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="0742c-128">本主題說明如何使用 WFF 建立和設定伺服器陣列，以便在多個負載平衡的 web 伺服器之間複寫 web 平台產品和元件、設定和網站和應用程式。</span><span class="sxs-lookup"><span data-stu-id="0742c-128">This topic describes how to create and configure a server farm using WFF, so that web platform products and components, configuration settings, and websites and applications are replicated across multiple load-balanced web servers.</span></span>
- <span data-ttu-id="0742c-129">[設定用於 Web Deploy 發佈的 Web 服務器（離線部署）](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="0742c-129">[Configure a Web Server for Web Deploy Publishing (Offline Deployment)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md).</span></span> <span data-ttu-id="0742c-130">本主題說明如何建立 web 伺服器，讓系統管理員以手動方式匯入和部署 web 套件，從全新的 Windows Server 2008 R2 組建開始。</span><span class="sxs-lookup"><span data-stu-id="0742c-130">This topic describes how to build a web server that lets administrators import and deploy web packages manually, starting from a clean Windows Server 2008 R2 build.</span></span>
- <span data-ttu-id="0742c-131">[設定資料庫伺服器以進行 Web Deploy 發行](configuring-a-database-server-for-web-deploy-publishing.md)。</span><span class="sxs-lookup"><span data-stu-id="0742c-131">[Configure a Database Server for Web Deploy Publishing](configuring-a-database-server-for-web-deploy-publishing.md).</span></span> <span data-ttu-id="0742c-132">本主題說明如何設定資料庫伺服器，以支援遠端存取和部署，從預設安裝的 SQL Server 2008 R2 開始。</span><span class="sxs-lookup"><span data-stu-id="0742c-132">This topic describes how to configure a database server to support remote access and deployment, starting from a default installation of SQL Server 2008 R2.</span></span>

## <a name="further-reading"></a><span data-ttu-id="0742c-133">進一步閱讀</span><span class="sxs-lookup"><span data-stu-id="0742c-133">Further Reading</span></span>

<span data-ttu-id="0742c-134">如需設定一般開發人員測試環境的指引，請參閱[案例：設定 Web 部署的測試環境](scenario-configuring-a-test-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="0742c-134">For guidance on configuring a typical developer test environment, see [Scenario: Configuring a Test Environment for Web Deployment](scenario-configuring-a-test-environment-for-web-deployment.md).</span></span> <span data-ttu-id="0742c-135">如需設定一般預備環境的指引，請參閱[案例：設定 Web 部署的預備環境](scenario-configuring-a-staging-environment-for-web-deployment.md)。</span><span class="sxs-lookup"><span data-stu-id="0742c-135">For guidance on configuring a typical staging environment, see [Scenario: Configuring a Staging Environment for Web Deployment](scenario-configuring-a-staging-environment-for-web-deployment.md).</span></span>

> [!div class="step-by-step"]
> <span data-ttu-id="0742c-136">[上一頁](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [下一頁](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span><span class="sxs-lookup"><span data-stu-id="0742c-136">[Previous](scenario-configuring-a-staging-environment-for-web-deployment.md)
[Next](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)</span></span>
