---
uid: web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
title: 設定 Web 部署的 Team Foundation Server |Microsoft Docs
author: jrjlee
description: 本教學課程將說明如何設定 Team Foundation Server （TFS）2010來建立解決方案，並將 web 內容部署至各種目標環境。 .。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: ff55233a-e795-4007-a4fc-861fe1bb590b
msc.legacyurl: /web-forms/overview/deployment/configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: 638d696abbc5f05957c0ed2eb7ebb65fce7813ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78528389"
---
# <a name="configuring-team-foundation-server-for-web-deployment"></a>設定 Web 部署的 Team Foundation Server

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教學課程將說明如何設定 Team Foundation Server （TFS）2010來建立解決方案，並將 web 內容部署至各種目標環境。 這包括連續整合（CI）案例，可讓您在每次開發人員進行變更時自動部署內容。 它也可以包含手動觸發案例，在此情況下，系統管理員可能會想要在測試環境中驗證並驗證組建之後，觸發特定組建至預備環境的部署。 本教學課程中的主題將引導您完成整個設定流程，包括：
> 
> - 如何在 TFS 中建立新的 team 專案。
> - 如何將內容新增至原始檔控制。
> - 如何設定組建伺服器以支援 CI 和部署。
> - 如何建立包含部署邏輯的組建定義。
> - 如何設定自動化部署的許可權。
> 
> 如需這些教學課程的義大利文翻譯，請造訪[http://www.lucamorelli.it](http://www.lucamorelli.it)。

本教學課程假設您已安裝 TFS 2010，並已建立 team 專案集合做為初始設定流程的一部分。 [Visual Studio 2010 的 Team Foundation 安裝指南](https://go.microsoft.com/?linkid=9805132)提供有關這些工作的完整指引。

## <a name="context"></a>內容

這會根據名為 Fabrikam，Inc. 的虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解決方案&#x2014;的範例解決方案，來代表具有實際複雜度層級的 WEB 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案檔所控制&#x2014;，其中一個包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="scenario-overview"></a>情節概觀

如需這些教學課程的高階案例，請參閱[企業 Web 部署：案例總覽](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)。 我們建議您先參閱本主題，再開始進行本教學課程。

## <a name="how-to-use-this-tutorial"></a>如何使用本教學課程

如果這是您第一次執行本教學課程中所述的工作，或者您想要遵循使用範例解決方案的範例，您應該依序逐步進行教學課程主題。 或者，您可以使用個別主題作為特定工作的指引。 本教學課程包含下列主題：

- [在 TFS 中建立 Team 專案](creating-a-team-project-in-tfs.md)。 Team 專案是在 TFS 中進行原始檔控制、進程管理和組建的核心單位。 您必須先建立 team 專案，才能將內容新增至原始檔控制或建立組建定義。
- [將內容加入至原始檔控制](adding-content-to-source-control.md)。 建立 team 專案之後，您就可以開始將內容加入至原始檔控制。 您必須先新增您的專案和方案，以及任何外部相依性，才能開始設定組建。
- 設定[Web 部署的 TFS 組建伺服器](configuring-a-tfs-build-server-for-web-deployment.md)。 如果您想要建立 team 專案內容，您必須設定組建伺服器。 在大部分情況下，這應該與 TFS 安裝在不同的電腦上。 若要設定組建伺服器，您必須安裝和設定 TFS 組建服務、安裝 Visual Studio 2010、建立組建控制器和組建代理程式、安裝程式碼所需的任何產品或元件，才能成功建立，並安裝Internet Information Services （IIS） Web 部署工具（Web Deploy）。
- [建立支援部署的組建定義](creating-a-build-definition-that-supports-deployment.md)。 在您可以開始在 TFS 中建立佇列或觸發組建之前，您必須至少為 team 專案建立一個組建定義。 組建定義會定義組建的各個層面，包括要包含在組建中的專案、應該觸發組建的內容，以及 Team Build 應該將組建輸出傳送至何處。 您可以設定組建定義來執行自訂 Microsoft Build Engine （MSBuild）專案檔，讓您在自動化組建中包含部署邏輯。
- [部署特定的組建](deploying-a-specific-build.md)。 在許多情況下，您會想要將特定的組建（而不是最新的組建）部署到目標環境。 在此情況下，您可以設定從特定的放置資料夾部署內容的組建定義。
- [正在設定 Team Build 部署的許可權](configuring-permissions-for-team-build-deployment.md)。 如果組建服務將內容部署為自動化組建程式的一部分，您就必須將各種許可權授與任何目的地 web 伺服器和資料庫伺服器上的組建服務帳戶。

## <a name="key-technologies"></a>重要技術

本教學課程著重于如何使用這些產品和技術來支援自動化組建和 web 部署：

- Visual Studio Team Foundation Server 2010
- Team Build 和 MSBuild
- Web Deploy

本教學課程也會說明 Windows Server 2008 R2、IIS 7.5、SQL Server 2008 R2、ASP.NET 4.0 和 ASP.NET MVC 3 的使用。

## <a name="other-tutorials-in-this-series"></a>本系列的其他教學課程

這會形成一系列五個企業級 web 部署教學課程的一部分。 這些是系列中的其他教學課程：

- [在企業案例中部署 Web 應用程式](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此簡介內容會提供教學課程系列的上下文背景。 其中說明教學課程案例，並說明整個系列中所述的工作和逐步解說如何符合更廣泛的應用程式生命週期管理（ALM）流程。
- [企業中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教學課程提供 MSBuild 專案檔、Web 發佈管線（WPP）、Web Deploy 和其他相關技術的概念介紹。 它會說明如何搭配使用這些工具來管理複雜的部署流程。
- 設定[Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教學課程說明如何設定 Windows 伺服器以支援各種部署案例，包括使用 Web Deployment Agent 服務（遠端代理程式）或 Web Deploy 處理常式和遠端資料庫部署的遠端 web 套件部署。 它提供有關為您自己的環境選擇適當部署方法的指引，並說明如何使用 Web 伺服陣列架構（WFF），在伺服器陣列中的所有 Web 服務器上複寫已部署的 web 應用程式。
- [先進的企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教學課程說明如何完成各種更先進的部署工作，例如自訂多個環境的資料庫部署、從部署中排除檔案和資料夾，以及在部署過程中讓 web 應用程式離線.

> [!div class="step-by-step"]
> [下一個](creating-a-team-project-in-tfs.md)
