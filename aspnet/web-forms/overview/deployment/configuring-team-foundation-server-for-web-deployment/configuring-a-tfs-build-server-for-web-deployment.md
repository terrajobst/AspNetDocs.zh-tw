---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
title: 設定 Web 部署的 TFS 組建伺服器 |Microsoft Docs
author: jrjlee
description: 本主題描述如何準備 Team Foundation Server （TFS）組建伺服器，以使用 Team Build 和 Internet Informat 來建立及部署您的方案 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f8400241-4f4b-4bbd-9994-54fb64909e6e
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-a-tfs-build-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: b3aaf7234706d149a3c784347528923f662c3511
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78631093"
---
# <a name="configuring-a-tfs-build-server-for-web-deployment"></a>設定 Web 部署的 TFS 組建伺服器

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何準備 Team Foundation Server （TFS）組建伺服器，以使用 Team Build 和 Internet Information Services （IIS） Web Deployment Tool （Web Deploy）來建立及部署您的方案。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="task-overview"></a>工作總覽

若要準備組建伺服器以建立和部署您的解決方案，您必須：

- 安裝和設定 TFS 組建服務。
- 安裝 Visual Studio 2010。
- 安裝建立方案所需的任何產品或元件，例如 .NET Framework 或 ASP.NET MVC 的版本。
- 安裝 Web Deploy 2.0 或更新版本。

本主題將說明如何執行這些程式或指向其所在的其他資源。 本主題中的工作和逐步解說假設：

- 您是從執行 Windows Server 2008 R2 Service Pack 1 的全新伺服器組建開始。
- 伺服器已加入具有靜態 IP 位址的網域。
- 您已將 TFS 應用層安裝在不同的伺服器上，如[企業 Web 部署：案例總覽](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)中所述。

### <a name="who-performs-these-procedures"></a>誰執行這些程式？

在大部分情況下，TFS 系統管理員會負責設定組建伺服器。 在某些情況下，開發人員小組可能會取得特定組建伺服器的擁有權。

## <a name="install-and-configure-the-tfs-build-service"></a>安裝和設定 TFS 組建服務

當您設定組建伺服器時，您的第一項工作是安裝和設定 TFS 組建服務。 在此過程中，您將需要：

- 安裝 TFS 組建服務並設定服務帳戶。 任何組建工作（包括部署）都會使用組建服務帳戶的身分識別來執行。
- 建立*組建控制器*和一或多個*組建代理*程式。 每個組建控制器會管理一組組建代理程式。 當您將組建排入佇列時，組建控制器會將組建工作指派給可用的組建代理程式。 TFS 中的每個 team 專案集合都會對應至單一組建控制器。
- 設定組建輸出的放置資料夾。 這是網路共用。 任何組建輸出（例如 web 部署套件）都會傳送至 drop 資料夾。

MSDN 上的[管理 Team Foundation Build](https://msdn.microsoft.com/library/ms252495.aspx)章節包含執行這些工作所需的所有資源：

- 如需 Team Foundation Build 的概念總覽，包括組建服務、組建控制器和組建代理程式，請參閱[瞭解 Team Foundation Build 系統](https://msdn.microsoft.com/library/dd793166.aspx)。
- 如需安裝和設定組建服務的相關資訊，請參閱[設定組建電腦](https://msdn.microsoft.com/library/ms181712.aspx)。
- 如需建立組建控制器的詳細資訊，請參閱[建立和使用組建控制器](https://msdn.microsoft.com/library/ee330987.aspx)。
- 如需建立組建代理程式的詳細資訊，請參閱建立[和使用組建代理](https://msdn.microsoft.com/library/bb399135.aspx)程式。
- 如需建立和設定 drop 資料夾的相關資訊，請參閱[設定 Drop folders](https://msdn.microsoft.com/library/bb778394.aspx)。

## <a name="install-required-products-and-components"></a>安裝必要的產品和元件

若要讓組建伺服器能夠建立您的方案，您必須安裝方案所需的任何產品、元件或元件。 安裝任何 web 平臺元件之前，您應該先在組建伺服器上安裝 Visual Studio 2010 （任何版本）。 這可確保核心 Microsoft Build Engine （MSBuild）目標檔案和 Web 發行管線（WPP）目標檔案可供組建服務使用。 Visual Studio 安裝程式也應該安裝 Web Deploy，如果您打算將 Web 套件部署為組建程式的一部分，就會需要此元件。

安裝一般 web 平臺元件的最佳方式是使用[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。 這可確保您要安裝每個產品的最新版本，而且它也會自動偵測並安裝每個產品的任何必要條件。 在[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解決方案的情況下，您應該使用 Web Platform Installer 來安裝這些產品和元件：

- **.NET Framework 4.0**。 這是執行此版本 .NET Framework 所建立之應用程式的必要項。
- **Web Deployment Tool 2.1 或更新版本**。 這會在您的伺服器上安裝 Web Deploy （及其基礎可執行檔，Msdeploy.exe）。 在此過程中，它會安裝並啟動 Web Deployment Agent 服務。 此服務可讓您從遠端電腦部署 web 封裝。
- **ASP.NET MVC 3**。 這會安裝執行 ASP.NET MVC 3 應用程式所需的元件。

**若要安裝必要的產品和元件**

1. 安裝 Visual Studio 2010。 當系統提示您選取要安裝的功能時，您應該包含：

    1. 您需要編譯的任何程式設計語言。
    2. Visual Web Developer。 這可確保 WPP 目標會加入至您的組建伺服器。

        ![](configuring-a-tfs-build-server-for-web-deployment/_static/image1.png)
2. 當 Visual Studio 2010 的安裝完成時，請下載並安裝[Visual Studio 2010 Service Pack 1](https://go.microsoft.com/?linkid=9805133) （如果尚未包含在安裝媒體中）。

    > [!NOTE]
    > Visual Studio 2010 Service Pack 1 會解析可防止 MSBuild 尋找 Msdeploy.exe 可執行檔的 bug。
3. 下載並啟動[Web Platform Installer](https://go.microsoft.com/?linkid=9805118)。
4. 在 [ **Web Platform Installer 3.0** ] 視窗頂端，按一下 [**產品**]。
5. 在視窗左側的流覽窗格中 **，按一下 [** 架構]。
6. 在 [ **Microsoft .NET Framework 4** ] 資料列中，如果尚未安裝 .NET Framework，請按一下 [**新增**]。

    > [!NOTE]
    > 您可能已經透過 Windows Update 安裝了 .NET Framework 4.0。 如果已安裝產品或元件，Web Platform Installer 會以**已安裝**的文字取代 [**新增**] 按鈕來指出這一點。

    ![](configuring-a-tfs-build-server-for-web-deployment/_static/image2.png)
7. 在 [ **ASP.NET MVC 3 （Visual Studio 2010）** ] 資料列中，按一下 [**新增**]。
8. 在流覽窗格中，按一下 [**伺服器**]。
9. 在 [ **Web Deployment Tool 2.1** ] 資料列中，按一下 [**新增**]。
10. 按一下 [安裝]。 Web Platform Installer 將會顯示一份產品&#x2014;清單，其中包含&#x2014;要安裝的相關聯相依性，並會提示您接受授權條款。
11. 請參閱授權條款，如果您同意這些條款，請按一下 [**我接受**]。
12. 當安裝完成時，按一下 **[完成]** ，然後關閉 [ **Web Platform Installer 3.0** ] 視窗。

> [!NOTE]
> 如果您的部署套裝程式含使用 VSDBCMD 或 SQLCMD 之類的工具，您必須確保這些元件已安裝在您的組建伺服器上。 VSDBCMD 是一種 Visual Studio 工具，而且通常會在您安裝 Team Foundation Build 時加入伺服器。 SQLCMD 是 SQL Server 工具。 您可以從 [ [Microsoft SQL Server 2008 R2 功能套件](https://go.microsoft.com/?linkid=9805134)] 頁面下載一個獨立版本的 SQLCMD。

## <a name="conclusion"></a>結論

此時，您的組建伺服器已準備好開始建立和部署您的 web 應用程式專案。 下一個主題建立[支援部署的組建定義](creating-a-build-definition-that-supports-deployment.md)，描述如何建立和設定組建定義，以控制專案的建立和部署時間和方式。

## <a name="further-reading"></a>進一步閱讀

如需使用 Team Build 的一般指引，請參閱[管理 Team Foundation build](https://msdn.microsoft.com/library/ms252495.aspx)。

> [!div class="step-by-step"]
> [上一頁](adding-content-to-source-control.md)
> [下一頁](creating-a-build-definition-that-supports-deployment.md)
