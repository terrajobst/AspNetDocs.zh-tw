---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
title: 案例：設定 Web 部署的測試環境 |Microsoft Docs
author: jrjlee
description: 本主題描述開發人員或測試環境的一般 web 部署案例，並說明您需要完成才能設定 si 的工作 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 44a22ac7-1fc7-4174-b946-c6129fb6a19b
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: d580e550f2461837f0e8a4e477273348b49cb53e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78637813"
---
# <a name="scenario-configuring-a-test-environment-for-web-deployment"></a>案例：設定 Web 部署的測試環境

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述開發人員或測試環境的一般 web 部署案例，並說明您需要完成才能設定類似環境的工作。

當開發人員在 web 應用程式上工作時，他們通常會被授與伺服器環境的存取權，讓他們可以在實際的設定下用來測試應用程式的變更。 這種開發或測試環境通常具有下列特性：

- 環境是由單一 web 伺服器和單一資料庫伺服器所組成。
- 開發人員通常會在伺服器上擁有系統管理員許可權，讓他們將環境設定為其應用程式的需求。
- 應用程式的變更會經常部署，因此環境必須支援單一步驟或自動化部署。

例如，在我們的[教學課程案例](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中，Matt Hink 是 Fabrikam，inc. Matt 正致力於 Contact Manager 解決方案，並且定期需要將變更部署到測試環境。 Matt 是測試 web 伺服器和測試資料庫伺服器上的系統管理員。 一開始，Matt 必須能夠直接將解決方案部署到測試環境。

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image1.png)

隨著工作進展和更多開發人員加入小組，Contact Manager 解決方案會針對 Team Foundation Server （TFS）中的持續整合（CI）進行設定。 每當開發人員簽入內容時，Team Build 應該會建立方案、執行任何單元測試，並將方案自動部署到測試環境。

![](scenario-configuring-a-test-environment-for-web-deployment/_static/image2.png)

## <a name="solution-overview"></a>方案概觀

測試環境必須支援遠端電腦的單一步驟或自動化部署，因此您可以選擇兩個主要方法。 您可以：

- 設定測試 web 伺服器，以支援使用 Web Deployment Agent 服務（「遠端代理程式」）進行部署。
- 設定測試 web 伺服器，以支援使用 Web Deploy 處理常式進行部署。

> [!NOTE]
> 您也可以[視需要使用 Web Deploy](https://technet.microsoft.com/library/ee517345(WS.10).aspx) （「temp 代理程式」）。 這類似于在需求和條件約束方面的遠端代理程式方法。

在此情況下，開發人員在目的地伺服器上具有系統管理員許可權，而且測試環境不受嚴格的安全性限制，因此邏輯選擇是將測試 web 伺服器設定為支援使用遠端代理程式進行部署。 這比較不復雜，而且需要的初始設定比 Web Deploy 處理常式方法少。 您也需要設定您的資料庫伺服器，以支援遠端存取和部署。

這些主題提供完成這些工作所需的所有資訊：

- [設定用於 Web Deploy 發佈的網頁伺服器（遠端代理程式）](configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)。 本主題說明如何使用遠端代理程式方法（從全新的 Windows Server 2008 R2 組建開始），建立支援 Web Deploy 發行的網頁伺服器。
- [設定資料庫伺服器以進行 Web Deploy 發行](configuring-a-database-server-for-web-deploy-publishing.md)。 本主題說明如何設定資料庫伺服器，以支援遠端存取和部署，從預設安裝的 SQL Server 2008 R2 開始。

## <a name="further-reading"></a>進一步閱讀

如需設定一般預備環境的指引，請參閱[案例：設定 Web 部署的預備環境](scenario-configuring-a-staging-environment-for-web-deployment.md)。 如需設定一般生產環境的指引，請參閱[案例：設定 Web 部署的生產環境](scenario-configuring-a-production-environment-for-web-deployment.md)。

> [!div class="step-by-step"]
> [上一頁](choosing-the-right-approach-to-web-deployment.md)
> [下一頁](scenario-configuring-a-staging-environment-for-web-deployment.md)
