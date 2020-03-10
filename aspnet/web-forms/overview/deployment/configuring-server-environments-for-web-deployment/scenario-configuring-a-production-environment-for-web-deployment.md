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
# <a name="scenario-configuring-a-production-environment-for-web-deployment"></a>案例：設定 Web 部署的生產環境

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明生產環境的一般 web 部署案例，並說明您需要完成才能設定類似環境的工作。

生產環境是 web 應用程式或網站的最終目的地。 此時，您的應用程式已通過測試，已部署至預備環境，並已準備好「上線」。 生產環境的特性可能會根據 web 內容的本質和用途、您的組織規模、目標物件和許多其他因素而有很大的差異。 在企業規模的案例中，生產環境可能具有下列特性：

- 環境是由多個負載平衡的 web 伺服器和一或多個資料庫伺服器所組成，通常會有容錯移轉叢集和資料庫鏡像。
- 如果環境是網際網路對向，則可能會與您的內部網路隔離。 它可能位於周邊網路中的不同子網，它可能位於不同的網域，而且可能位於完全不同的網路基礎結構上。
- 開發人員和組建伺服器進程帳戶在實際執行伺服器上的系統管理員許可權非常不太可能。
- 應用程式的變更會以較不頻繁的方式部署，而不是測試或預備部署。

> [!NOTE]
> 向外擴充多部伺服器上的資料庫部署已超出本教學課程的範圍。 如需有關此區域的詳細資訊，請參閱[SQL Server 線上叢書](https://technet.microsoft.com/library/ms130214.aspx)。

例如，在我們的[教學課程案例](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，Team Build server 包含組建定義，可讓使用者在單一步驟中建立 Contact Manager 解決方案，並將其部署至預備環境。 當應用程式準備好要部署到生產環境時，由於安全性需求和網路基礎結構的條件約束，生產環境管理員必須手動將 web 套件複製到生產 web 伺服器並匯入它透過 Internet Information Services （IIS）管理員。

![](scenario-configuring-a-production-environment-for-web-deployment/_static/image1.png)

## <a name="solution-overview"></a>方案概觀

在此案例中，您可以從部署需求的分析中推算這些事實：

- 由於安全性限制和網路設定，您無法將生產環境設定為支援單鍵或自動化部署。 在此案例中，離線部署是唯一可行的方法。
- 生產環境包含多部 web 伺服器，因此您可以使用 Web 伺服陣列架構（WFF）來建立伺服器陣列。 使用這種方法時，系統管理員只需要將應用程式匯入到一部 web 伺服器（主伺服器），WFF 就會將部署複寫到生產環境中的所有其他 web 伺服器上。

這些主題提供完成這些工作所需的所有資訊：

- [使用 Web 伺服陣列架構建立伺服器](configuring-a-database-server-for-web-deploy-publishing.md)陣列。 本主題說明如何使用 WFF 建立和設定伺服器陣列，以便在多個負載平衡的 web 伺服器之間複寫 web 平台產品和元件、設定和網站和應用程式。
- [設定用於 Web Deploy 發佈的 Web 服務器（離線部署）](configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)。 本主題說明如何建立 web 伺服器，讓系統管理員以手動方式匯入和部署 web 套件，從全新的 Windows Server 2008 R2 組建開始。
- [設定資料庫伺服器以進行 Web Deploy 發行](configuring-a-database-server-for-web-deploy-publishing.md)。 本主題說明如何設定資料庫伺服器，以支援遠端存取和部署，從預設安裝的 SQL Server 2008 R2 開始。

## <a name="further-reading"></a>進一步閱讀

如需設定一般開發人員測試環境的指引，請參閱[案例：設定 Web 部署的測試環境](scenario-configuring-a-test-environment-for-web-deployment.md)。 如需設定一般預備環境的指引，請參閱[案例：設定 Web 部署的預備環境](scenario-configuring-a-staging-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一頁](scenario-configuring-a-staging-environment-for-web-deployment.md)
> [下一頁](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)
