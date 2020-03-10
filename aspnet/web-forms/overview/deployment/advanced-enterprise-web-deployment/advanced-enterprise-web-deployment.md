---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
title: Advanced Enterprise Web Deployment |Microsoft Docs
author: jrjlee
description: 本教學課程將示範如何在許多企業部署案例中執行所需或需要的各種工作。 如需義大利 translati 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 7dcaba80-f2ec-4db3-ad98-daadc3afdb49
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/advanced-enterprise-web-deployment
msc.type: authoredcontent
ms.openlocfilehash: bf4c7d021763017592483df35cb717295c4924aa
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78587602"
---
# <a name="advanced-enterprise-web-deployment"></a>進階的企業 Web 部署

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本教學課程將示範如何在許多企業部署案例中執行所需或需要的各種工作。
> 
> 如需這些教學課程的義大利文翻譯，請造訪[http://www.lucamorelli.it](http://www.lucamorelli.it)。

這會根據名為 Fabrikam，Inc. 的虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解決方案&#x2014;的範例解決方案，來代表具有實際複雜度層級的 WEB 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案檔所控制&#x2014;，其中一個包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="scenario-overview"></a>情節概觀

如需這些教學課程的高階案例，請參閱[企業 Web 部署：案例總覽](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)。 我們建議您先參閱本主題，再開始進行本教學課程。

## <a name="how-to-use-this-tutorial"></a>如何使用本教學課程

- 本教學課程中的每個主題都是獨立的，並可解決企業部署案例中所發生的特定挑戰或問題。 您不需要以任何特定順序來處理這些主題。 不過，本教學課程涵蓋一些先進的工作。 因此，您應該熟悉企業教學課程中[Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)所涵蓋的概念和技術，以充分發揮此內容的效益。
- 本教學課程包含下列主題：
- [執行「What If」部署](performing-a-what-if-deployment.md)。 在許多情況下，您會想要在實際進行任何變更之前，先判斷建議部署對目標環境或任何現有內容的影響。 本主題描述如何執行「假設」部署，以產生記錄檔和資料庫更新腳本，如同您已將內容部署至目標環境一樣，而不需要實際進行任何變更。 分析這些資源可協助您在即時部署之前找出任何潛在的問題。
- [自訂多個環境的資料庫部署](customizing-database-deployments-for-multiple-environments.md)。 當您將資料庫專案部署至多個目的地時，您通常會想要自訂每個目標環境的部署屬性。 例如，在測試環境中，您通常會在每個部署上重新建立資料庫，而在預備或生產環境中，您很可能會進行累加式更新以保留您的資料。 本主題說明如何藉由建立每個目標環境的環境特定部署設定（. sqldeployment）檔案，將這些屬性變更併入您的部署邏輯。
- 將資料庫角色成員資格部署到測試環境。 當您在每個部署&#x2014;上重新建立資料庫時（例如，作為持續整合（CI）組建的一部分），並部署&#x2014;到測試環境時，您通常需要每次都設定資料庫角色成員資格。 例如，您通常需要將許可權授與與 web 應用程式相關聯的應用程式集區身分識別。 本主題說明如何藉由將部署後 SQL 腳本新增至部署邏輯，來自動化此程式。
- [將成員資格資料庫部署到企業環境](deploying-membership-databases-to-enterprise-environments.md)。 ASP.NET 成員資格資料庫具有各種特性，而使部署程式變得複雜。 例如，僅限架構的部署會讓資料庫處於無法運作的狀態。 在大部分的情況下，最好是直接在每個目的地環境中建立成員資格資料庫。 不過，如果您必須部署成員資格資料庫，本主題會說明一些您可以用來滿足固有挑戰的方法。
- [從部署中排除檔案和資料夾](excluding-files-and-folders-from-deployment.md)。 在某些情況下，您會想要將 web 套件的內容量身打造到特定的目的地環境。 例如，當您部署到測試環境時，您可能會想要包含 JavaScript 程式庫的完整版本，以支援用戶端的偵錯工具，但在部署至預備或生產環境時，請使用縮減版本的程式庫。 本主題說明如何從封裝建立程式中排除特定的檔案和資料夾。
- [使用 Web Deploy 讓 Web 應用程式離線](taking-web-applications-offline-with-web-deploy.md)。 當您將解決方案部署至預備或生產環境時，您通常會想要讓 web 應用程式在部署過程中離線。 本主題說明如何在部署程式開始時，將 *\_離線 .htm*檔案的應用程式新增至您的 web 應用程式，並在結束時將它移除。 當*應用程式\_離線 .htm*檔案時，流覽至該 web 應用程式的任何使用者都會自動重新導向至應用程式 *\_的離線 .htm*檔案。
- [正在從 MSBuild 執行 Windows PowerShell 腳本](running-windows-powershell-scripts-from-msbuild-project-files.md)。 許多部署案例都需要更複雜的部署後動作，例如在登錄中新增自訂事件來源，或在 SQL Server 實例之間設定複寫。 這些動作通常是透過 Windows PowerShell 腳本來完成。 本主題說明如何從 Microsoft Build Engine （MSBuild）專案檔執行 Windows PowerShell 腳本，做為組建和部署程式的一部分。
- 針對[封裝程式進行疑難排解](troubleshooting-the-packaging-process.md)。 Web 發行管線（WPP）定義一個名為**EnablePackageProcessLoggingAndAssert**的 MSBuild 屬性，您可以用它來產生有關 Web 應用程式專案的封裝程式的深入資訊。 本主題說明屬性的用途和使用方式。

## <a name="key-technologies"></a>重要技術

本教學課程著重于如何使用這些產品和技術來支援自動化組建和 web 部署：

- Visual Studio 2010 和 Team Foundation Server （TFS）2010
- MSBuild 和 TFS Team Build
- Internet Information Services （IIS）7。5
- IIS Web Deployment Tool （Web Deploy）2。1
- VSDBCMD .exe 資料庫部署公用程式

## <a name="other-tutorials-in-this-series"></a>本系列的其他教學課程

這會形成一系列五個企業級 web 部署教學課程的一部分。 這些是系列中的其他教學課程：

- [在企業案例中部署 Web 應用程式](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)。 此簡介內容會提供教學課程系列的上下文背景。 其中說明教學課程案例，並說明整個系列中所述的工作和逐步解說如何符合更廣泛的應用程式生命週期管理（ALM）流程。
- [企業中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教學課程提供 MSBuild 專案檔、WPP、Web Deploy 和其他相關技術的概念介紹。 它會說明如何搭配使用這些工具來管理複雜的部署流程。
- 設定[Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教學課程說明如何設定 Windows 伺服器以支援各種部署案例，包括使用 Web Deployment Agent 服務（遠端代理程式）或 Web Deploy 處理常式和遠端資料庫部署的遠端 web 套件部署。 它提供有關為您自己的環境選擇適當部署方法的指引，並說明如何使用 Web 伺服陣列架構（WFF），在伺服器陣列中的所有 Web 服務器上複寫已部署的 web 應用程式。
- [正在設定 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教學課程說明如何設定 TFS 以支援各種部署案例，包括做為 CI 程式的一部分進行自動化部署，以及手動觸發特定組建的部署。

> [!div class="step-by-step"]
> [下一個](performing-a-what-if-deployment.md)
