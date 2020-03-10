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
# <a name="configuring-server-environments-for-web-deployment"></a>設定 Web 部署的伺服器環境

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教學課程將說明如何設定伺服器環境，以在各種不同的案例中支援單鍵或自動化的網站部署和發佈。 本教學課程包含的主題可引導您完成各種工作，例如設定 web 伺服器以支援部署和設定 Web 伺服陣列架構（WFF）伺服器陣列的特定方法，以及提供較高層級的端對端指引。
> 
> 本教學課程使用「[企業 Web 部署：案例總覽](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)」中所述的 Fabrikam，inc. 部署案例，做為範例和網路基礎結構的參考點。
> 
> 如需這些教學課程的義大利文翻譯，請造訪[http://www.lucamorelli.it](http://www.lucamorelli.it)。

本教學課程包含下列主題：

- [選擇 Web 部署的正確方法](choosing-the-right-approach-to-web-deployment.md)
- [案例：設定 Web 部署的測試環境](scenario-configuring-a-test-environment-for-web-deployment.md)
- [案例：設定 Web 部署的預備環境](scenario-configuring-a-staging-environment-for-web-deployment.md)
- [案例：設定 Web 部署的生產環境](scenario-configuring-a-production-environment-for-web-deployment.md)
- [設定 Web Deploy 發行的網頁伺服器 (遠端代理程式)](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
- [設定 Web Deploy 發行的網頁伺服器 (Web Deploy 處理常式)](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)
- [設定 Web Deploy 發行的網頁伺服器 (離線部署)](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)
- [設定 Web Deploy 發行的資料庫伺服器](configuring-a-database-server-for-web-deploy-publishing.md)
- [使用 Web 伺服陣列架構建立伺服器陣列](creating-a-server-farm-with-the-web-farm-framework.md)
- [設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)

第一個主題[選擇 Web 部署的正確方法](choosing-the-right-approach-to-web-deployment.md)，說明您可以使用 INTERNET INFORMATION SERVICES （IIS） Web 部署工具（Web Deploy）2.0 來發行 web 應用程式的主要方法。 它也會識別對應至每個方法的案例。 從這裡開始，每個案例主題都會提供完成所需工作的高階總覽，並識別您需要進行的主題，以協助您完成這些作業。

如果您使用瞭解建立及部署方案[的組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述的分割專案檔方法，最後一個主題[設定目標環境的部署屬性](configuring-deployment-properties-for-a-target-environment.md)，說明如何設定環境特定的專案檔，以部署至不同的目的地環境。

## <a name="key-technologies"></a>重要技術

本教學課程著重于如何使用這些產品和技術來支援 web 部署：

- IIS 7。5
- Web Deploy 2。x
- WFF 2。x
- IIS Web 管理服務（WMSvc）

本教學課程也會說明 Windows Server 2008 R2、SQL Server 2008 R2、ASP.NET 4.0 和 ASP.NET MVC 3 的使用。

## <a name="other-tutorials-in-this-series"></a>本系列的其他教學課程

這會形成一系列五個企業級 web 部署教學課程的一部分。 這些是系列中的其他教學課程：

- [在企業案例中部署 Web 應用程式](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此簡介內容會提供教學課程系列的上下文背景。 其中說明教學課程案例，並說明整個系列中所述的工作和逐步解說如何符合更廣泛的應用程式生命週期管理（ALM）流程。
- [企業中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教學課程提供 Microsoft Build Engine （MSBuild）專案檔、Web 發佈管線、Web Deploy 和其他相關技術的概念介紹。 它會說明如何搭配使用這些工具來管理複雜的部署流程。
- [正在設定 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教學課程說明如何設定 Team Foundation Server （TFS）以支援各種部署案例，包括自動部署作為持續整合（CI）程式的一部分，以及手動觸發特定組建的部署。
- [先進的企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教學課程說明如何完成各種更先進的部署工作，例如自訂多個環境的資料庫部署、從部署中排除檔案和資料夾，以及在部署過程中讓 web 應用程式離線.

> [!div class="step-by-step"]
> [下一個](choosing-the-right-approach-to-web-deployment.md)
