---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
title: 企業中的 Web 部署 |Microsoft Docs
author: jrjlee
description: 本教學課程說明如何在您管理企業級 web 應用程式部署至對內時遇到的許多挑戰：
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b8283698-7b82-42a8-8d83-3aeb18ca7fcc
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/web-deployment-in-the-enterprise
msc.type: authoredcontent
ms.openlocfilehash: bc7bb676a71af4ec3451aa3adf3c03ce3b5200d5
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628167"
---
# <a name="web-deployment-in-the-enterprise"></a>企業中的 Web 部署

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教學課程說明當您管理企業級 web 應用程式部署至開發、測試、預備和生產環境時，如何滿足您會遇到的許多挑戰。 本教學課程包含一個參考解決方案，並結合了概念和工作導向的內容，以引導您完成各種常見的工作和程式。
> 
> 如需這些教學課程的義大利文翻譯，請造訪[http://www.lucamorelli.it](http://www.lucamorelli.it)。

## <a name="enterprise-deployment-challenges"></a>企業部署挑戰

當組織想要管理複雜、企業規模解決方案的部署時，通常會遇到這些挑戰：

- 您必須能夠將專案部署到多個環境，例如開發人員或測試環境、預備平臺，以及實際執行伺服器。 您必須使用每個環境的不同設定來部署解決方案。
- 您需要同時部署多個相依專案，以做為單一步驟或自動化組建和部署程式的一部分。
- 您必須能夠從自動化程式中推動部署。 例如，您想要在新的程式碼簽入時，使用持續整合（CI）流程將 web 應用程式部署至測試環境。
- 您必須能夠控制部署程式，並從外部 Visual Studio 設定部署變數，因為開發人員不太可能具有每個目標環境的正確設定或必要認證。
- 您需要部署以架構為基礎的資料庫專案，並在後續的部署中保留現有的資料。
- 您需要在不部署使用者帳戶資料的情況下，以特定方式部署成員資格資料庫。 您可能也需要更新已部署的成員資格資料庫的架構，而不會遺失現有的使用者帳戶資料。
- 當您將內容部署至各種目標環境時，您需要排除特定的檔案或資料夾。

## <a name="overview-of-approach"></a>方法總覽

本教學課程連同此系列中的其他教學課程，會使用這個高階方法來符合上述的挑戰。

- **使用自訂 Microsoft Build Engine （MSBuild）專案檔來控制整體組建和部署程式。**
- 這可讓您在單一、可編寫腳本的作業中，建立及部署方案中的每個專案。
- 環境特有的設定是使用簡單的環境特定專案檔來設定。 相較于以 Visual Studio 為中心的方法，使用解決方案設定和發行設定檔來為不同的環境設定部署，這種方法可讓您設定和管理從外部 Visual Studio 的部署流程。 這表示開發人員不需要事先瞭解目的地環境的連接字串、服務端點、伺服器認證和其他部署變數。
- Team Build 可以在 Team Foundation Server （TFS）工作流程中叫用自訂專案檔案。 這可讓您為 CI 案例設定自動化部署。

**使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）來封裝和部署 Web 應用程式專案。**

- Web Deploy 提供的架構可讓您將 web 應用程式內容封裝和部署到目的地 IIS 網頁伺服器，以及相依性、設定、安全性設定，以及任何其他需求。
- 您可以從您的自訂 MSBuild 專案檔內控制整個封裝和部署流程。 您也可以操控 web 部署套件隨附的設定，例如連接字串、服務端點和 IIS 目的地詳細資料。
- Web Deploy 與 Web 發佈管線一起提供許多擴充點，可讓您自訂部署。 例如，您可以輕鬆地從 web 部署套件中排除不需要的檔案和資料夾。

**使用 VSDBCMD 公用程式來部署和更新資料庫架構。**

- VSDBCMD 可讓您從資料庫架構檔案（.dbschema）部署資料庫，當您建立 Visual Studio 資料庫專案時，就會產生這個檔案。 相反地，Web Deploy 所包含的資料庫部署功能更適合從本機 SQL Server 實例部署現有的資料庫。
- 不同于 Visual Studio 的部署資料庫專案功能，VSDBCMD 可讓您將差異更新部署至現有的目標資料庫。 這可讓您在升級資料庫架構時保留任何現有的資料。
- 您可以從自訂 MSBuild 專案檔內執行 VSDBCMD 命令。

## <a name="content-map"></a>內容對應

本教學課程包含分成四個主要區域的主題。

這些主題會介紹 Contact Manager&#x2014;解決方案&#x2014;的參考解決方案，並說明如何在您的本機電腦上下載並設定它：

- [連絡管理員解決方案](the-contact-manager-solution.md)
- [設定連絡管理員解決方案](setting-up-the-contact-manager-solution.md)

這些主題會介紹 MSBuild 專案檔、描述如何建立和使用自訂專案檔，以及逐步完成 Contact Manager 解決方案的部署程式：

- [了解專案檔](understanding-the-project-file.md)
- [了解建置流程](understanding-the-build-process.md)

這些主題說明 web 應用程式部署，包括組建和封裝程式的運作方式、組建程式如何與 Web 發佈管線整合、如何修改部署參數，以及如何將 web 套件部署到目的地環境

- [建置和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)
- [設定網頁套件部署的參數](configuring-parameters-for-web-package-deployment.md)
- [部署網頁套件](deploying-web-packages.md)

- [部署資料庫專案](deploying-database-projects.md)說明您可以用來部署 Visual Studio 資料庫專案的不同技巧，以及每種方法的優點和缺點。 [建立和執行部署命令](creating-and-running-a-deployment-command-file.md)檔說明如何建立簡單的命令檔來封裝您的部署邏輯，並可讓您將複雜的解決方案部署為單一步驟的進程。
- 最後，藉由顯示將 web 套件匯入 IIS 的方式，[手動安裝 Web 套件](manually-installing-web-packages.md)結束教學課程。

## <a name="key-technologies"></a>重要技術

本教學課程中的主題主要會使用這些技術來管理組建和部署：

- Visual Studio 2010
- MSBuild
- IIS 7。5
- Web Deploy 2.0
- VSDBCMD .exe 資料庫部署公用程式

## <a name="other-tutorials-in-this-series"></a>本系列的其他教學課程

這會形成一系列五個企業級 web 部署教學課程的一部分。 這些是系列中的其他教學課程：

- [在企業案例中部署 Web 應用程式](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此簡介內容會提供教學課程系列的上下文背景。 其中說明教學課程案例，並說明整個系列中所述的工作和逐步解說如何符合更廣泛的應用程式生命週期管理（ALM）流程。
- 設定[Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教學課程說明如何設定 Windows 伺服器以支援各種部署案例，包括使用 Web Deployment Agent 服務（遠端代理程式）或 Web Deploy 處理常式和遠端資料庫部署的遠端 web 套件部署。 它提供有關為您自己的環境選擇適當部署方法的指引，並說明如何使用 Web 伺服陣列架構（WFF），在伺服器陣列中的所有 Web 服務器上複寫已部署的 web 應用程式。
- [正在設定 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教學課程說明如何設定 TFS 以支援各種部署案例，包括做為 CI 程式的一部分進行自動化部署，以及手動觸發特定組建的部署。
- [先進的企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教學課程說明如何完成各種更先進的部署工作，例如自訂多個環境的資料庫部署、從部署中排除檔案和資料夾，以及在部署過程中讓 web 應用程式離線.

> [!div class="step-by-step"]
> [下一個](the-contact-manager-solution.md)
