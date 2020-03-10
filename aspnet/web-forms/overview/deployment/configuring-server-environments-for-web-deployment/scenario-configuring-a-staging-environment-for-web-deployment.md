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
# <a name="scenario-configuring-a-staging-environment-for-web-deployment"></a>案例：設定 Web 部署的預備環境

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明預備環境的一般 web 部署案例，並說明您需要完成才能設定類似環境的工作。

許多組織會使用預備環境來預覽 web 應用程式或網站的更新。 這讓組織內的人員有機會在網站「上線」之前探索及審查新的功能或內容，換句話說則是部署到生產環境。 預備環境的設計目的是要盡可能地複寫生產環境，以提供實際的預覽。 這種預備環境通常具有下列特性：

- 環境是由多個負載平衡的 web 伺服器和一或多個資料庫伺服器所組成，通常會有容錯移轉叢集和資料庫鏡像。
- 應用程式可以由開發小組手動部署，或由 Team Build server 自動部署。
- 部署應用程式的使用者或進程帳戶不太可能會擁有預備伺服器上的系統管理員許可權。
- 應用程式的變更會經常部署，因此環境必須支援單一步驟或自動化部署。

> [!NOTE]
> 向外擴充多部伺服器上的資料庫部署已超出本教學課程的範圍。 如需有關此區域的詳細資訊，請參閱[SQL Server 線上叢書](https://technet.microsoft.com/library/ms130214.aspx)。

例如，在我們的[教學課程案例](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，TEAM FOUNDATION SERVER （TFS）會管理 Contact Manager 解決方案。 TFS 系統管理員（Walters）已建立組建定義，可讓開發人員視需要觸發對預備環境的部署。

![](scenario-configuring-a-staging-environment-for-web-deployment/_static/image1.png)

請注意，在大部分的情況下，您不一定會想要將最新的組建部署至預備環境。 相反地，您很可能會想要在測試環境中部署已通過驗證和驗證的特定組建。

## <a name="solution-overview"></a>方案概觀

在此案例中，您可以從部署需求的分析中推算這些事實：

- 執行部署的使用者或進程帳戶不會在預備伺服器上擁有系統管理員許可權，因此預備 web 伺服器必須支援非系統管理員部署。 因此，您必須將預備 web 伺服器設定為使用 Web Deploy 處理常式，而不是遠端代理程式。
- 預備環境包含多部 web 伺服器，但它需要支援單鍵或自動化部署，因此您必須使用 Web 伺服陣列架構（WFF）來建立伺服器陣列。 使用這種方法，您可以將應用程式部署到一部 web 伺服器（主伺服器），而 WFF 會在預備環境中的所有其他 web 伺服器上複寫部署。
- 執行部署的使用者或進程帳戶必須擁有建立資料庫的許可權。 因此，除了將資料庫伺服器設定為支援遠端存取和部署之外，您還需要將此帳戶新增至資料庫伺服器上的**dbcreator**伺服器角色。

這些主題提供完成這些工作所需的所有資訊：

- [使用 Web 伺服陣列架構建立伺服器](creating-a-server-farm-with-the-web-farm-framework.md)陣列。 本主題說明如何使用 WFF 建立和設定伺服器陣列，以便在多個負載平衡的 web 伺服器之間複寫 web 平台產品和元件、設定和網站和應用程式。
- [設定用於 Web Deploy 發佈的 Web 服務器（Web Deploy 處理常式）](configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)。 本主題說明如何使用遠端代理程式方法（從全新的 Windows Server 2008 R2 組建開始），建立支援 Web Deploy 發行的網頁伺服器。
- [設定資料庫伺服器以進行 Web Deploy 發行](configuring-a-database-server-for-web-deploy-publishing.md)。 本主題說明如何設定資料庫伺服器，以支援遠端存取和部署，從預設安裝的 SQL Server 2008 R2 開始。

## <a name="further-reading"></a>進一步閱讀

如需設定一般開發人員測試環境的指引，請參閱[案例：設定 Web 部署的測試環境](scenario-configuring-a-test-environment-for-web-deployment.md)。 如需設定一般生產環境的指引，請參閱[案例：設定 Web 部署的生產環境](scenario-configuring-a-production-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一頁](scenario-configuring-a-test-environment-for-web-deployment.md)
> [下一頁](scenario-configuring-a-production-environment-for-web-deployment.md)
