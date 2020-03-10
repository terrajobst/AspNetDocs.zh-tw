---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
title: 使用 Visual Studio 2010 在企業案例中部署 Web 應用程式 |Microsoft Docs
author: jrjlee
description: 這組教學課程說明您可以用來在各種企業案例中部署 web 應用程式的工具和技術。 其中說明如何充分運用 。
ms.author: riande
ms.date: 05/03/2012
ms.assetid: 48cfe378-d62a-48c6-a4db-6be3cead6898
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios
msc.type: authoredcontent
ms.openlocfilehash: eb7b82d16079d4d086af1919d092fb28db60d8b3
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78574155"
---
# <a name="deploying-web-applications-in-enterprise-scenarios-using-visual-studio-2010"></a>使用 Visual Studio 2010 在企業案例中部署 Web 應用程式

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 這組教學課程說明您可以用來在各種企業案例中部署 web 應用程式的工具和技術。 其中說明如何充分運用像是 Visual Studio 2010、Microsoft Build Engine （MSBuild）、Internet Information Services （IIS）7.5、IIS Web 部署工具（Web Deploy）、Web 伺服陣列架構（WFF），以及 VSDBCMD 等公用程式之類的技術。簡化和管理部署流程。 其中包含概念性總覽和工作導向的指引，可協助您：
> 
> - 檢查並建立企業級 web 應用程式的部署需求。
> - 設定測試、預備和生產 web 伺服器環境，以支援 web 部署。
> - 設定 Team Foundation Server （TFS）持續整合（CI）程式，以支援自動化的 web 部署。
> - 將企業規模的 web 應用程式部署到不同的伺服器環境，並具有不同的需求和限制。
> - 將變更部署到在不同伺服器環境中執行的 web 應用程式。
> 
> > [!NOTE]
> > 雖然這些教學課程會說明如何使用 TFS 做為 CI 伺服器，但您可以輕鬆地調整任何 CI 伺服器的指引。 您不需要 TFS 的詳細知識，就能瞭解和運用教學課程。
> 
> 
> 如需這些教學課程的義大利文翻譯，請造訪[http://www.lucamorelli.it](http://www.lucamorelli.it)。

## <a name="about-the-authors"></a>關於作者

Jason 先生是[內容主機](http://www.contentmaster.com/)的主要技術人員，他曾使用過 Microsoft 產品和技術（特別是 SharePoint 和 ASP.NET）數年。 Jason 保有電腦的博士學位，目前已 MCPD 且 MCTS 認證。 您可以在[www.jrjlee.com](http://www.jrjlee.com/)閱讀 Jason 的技術 blog。

Benjamin Curry 是[內容主機](http://www.contentmaster.com/)的主體技術人員，他在其事業期間撰寫了白皮書、SDK 檔、PowerPoint 簡報和講師指導與線上訓練課程。 他是 ASP.NET 檔團隊的原始成員，他曾用過多年來的 Microsoft web 技術。

## <a name="target-audience"></a>目標對象

這組教學課程適用于 ASP.NET web 應用程式開發人員和解決方案架構設計人員，使用 Visual Studio 2010 建立企業級 web 應用程式。 若要充分發揮內容的價值，您應該使用 Visual Studio 2010，並且對 TFS 有基本的熟悉度，並瞭解 Microsoft web platform 技術（例如 ASP.NET MVC 3、Windows Communication Foundation （WCF）、IIS、SQL）伺服器和 Visual Studio 資料庫專案。 不過，您不必熟悉部署工具和技術，也不需要知道如何設定 CI 系統。

## <a name="requirements"></a>需求

若要遵循逐步解說並執行這些教學課程所述的工作，您必須在開發電腦上安裝此軟體：

- Visual Studio 2010 Premium 或旗艦版（含 Service Pack 1）
- .NET Framework 4.0
- .NET Framework 3.5 （含 Service Pack 1）
- ASP.NET MVC 3.0
- IIS 7.5 Express
- SQL Server Express 2008 R2

若要執行這些逐步解說中所述的部署步驟，您必須具備範例 Web 應用程式部署環境的存取權。 為了獲得最佳結果，這些環境應反映貴組織的企業部署模式。 接著，您可以修改本檔中提供的逐步解說，以反映您自己組織的部署環境和需求。

## <a name="series-contents"></a>數列內容

本簡介章節包含兩個進一步的主題。 其設計是為了提供更廣泛的教學課程內容，如下所示：

- [企業 Web 部署：案例總覽](enterprise-web-deployment-scenario-overview.md)。 本主題描述能支援此系列中每個教學課程的案例。 此案例著重于名為 Fabrikam，Inc. 之虛構公司的應用程式生命週期管理（ALM）需求，因為它會開發企業規模的 web 應用程式。
- [應用程式生命週期管理：從開發到生產環境](application-lifecycle-management-from-development-to-production.md)。 本主題提供部署程式的高階端對端總覽。 其中說明 Fabrikam，Inc. 如何透過測試、預備和生產環境，在持續開發過程中移動企業規模的 ASP.NET web 應用程式。

此系列包含四個教學課程集合。 每個重點著重于 web 部署的不同層面：

- [企業中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教學課程提供 MSBuild 專案檔、Web 發佈管線、Web Deploy 和其他相關技術的概念介紹。 它會說明如何搭配使用這些工具來管理複雜的部署流程。
- 設定[Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教學課程說明如何設定 Windows 伺服器以支援各種部署案例，包括使用 Web Deployment Agent 服務（「遠端代理程式」）或 Web Deploy 處理常式和遠端資料庫部署的遠端 web 套件部署。 它提供有關為您自己的環境選擇適當部署方法的指引，並說明如何使用 WFF，在伺服器陣列中的所有 web 伺服器上複寫已部署的 web 應用程式。
- [正在設定 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教學課程說明如何設定 TFS 以支援各種部署案例，包括做為 CI 程式的一部分進行自動化部署，以及手動觸發特定組建的部署。
- [先進的企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教學課程說明如何完成各種更先進的部署工作，例如自訂多個環境的資料庫部署、從部署中排除檔案和資料夾，以及在部署過程中讓 web 應用程式離線.

## <a name="where-to-start"></a>開始位置

這一組教學課程會使用具有實際複雜性層級的範例解決方案，以及虛構的企業部署案例，來提供參考實作為，並將工作和逐步解說授與一般內容。 下一個主題「[企業 Web 部署：案例總覽](enterprise-web-deployment-scenario-overview.md)」介紹了案例和範例解決方案。 您可以從該處逐步完成最符合您需求的教學課程和主題。

> [!div class="step-by-step"]
> [下一個](enterprise-web-deployment-scenario-overview.md)
