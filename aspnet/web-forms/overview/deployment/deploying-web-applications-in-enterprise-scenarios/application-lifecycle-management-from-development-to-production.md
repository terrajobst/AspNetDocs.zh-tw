---
uid: web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
title: 應用程式生命週期管理：從開發到生產環境 |Microsoft Docs
author: jrjlee
description: 本主題說明虛構的公司如何透過測試、預備和生產環境，來管理 ASP.NET web 應用程式的部署。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: f97a1145-6470-4bca-8f15-ccfb25fb903c
msc.legacyurl: /web-forms/overview/deployment/deploying-web-applications-in-enterprise-scenarios/application-lifecycle-management-from-development-to-production
msc.type: authoredcontent
ms.openlocfilehash: 230cf4393db0ee19cfc42ed54359d61e7926a49d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78640662"
---
# <a name="application-lifecycle-management-from-development-to-production"></a>應用程式生命週期管理：從開發到生產環境

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明虛構的公司如何透過測試、預備和生產環境來管理 ASP.NET web 應用程式的部署，做為持續開發流程的一部分。 在整個主題中，會提供連結給進一步的資訊，以及如何執行特定工作的逐步解說。
> 
> 本主題旨在提供企業中 web 部署的一[系列教學](deploying-web-applications-in-enterprise-scenarios.md)課程的高階總覽。 如果您不熟悉這裡所述的一些概念，請別擔心&#x2014;，這些教學課程會提供所有這些工作和技術的詳細資訊。
> 
> > [!NOTE]
> > 為了簡單起見，本主題不會討論在部署過程中更新資料庫。 不過，對資料庫功能進行累加式更新是許多企業部署案例的需求，您可以在本教學課程系列稍後找到如何完成這項操作的指引。 如需詳細資訊，請參閱[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)。

## <a name="overview"></a>概觀

此處所說明的部署程式是以「[企業 Web 部署：案例總覽](enterprise-web-deployment-scenario-overview.md)」中所述的 Fabrikam，inc. 部署案例為基礎。 在您研究本主題之前，您應該先閱讀案例總覽。 基本上，此案例會透過一般企業環境中的各種階段，檢查組織如何管理合理複雜 web 應用程式（ [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)）的部署。

在高階的過程中，Contact Manager 解決方案會在開發和部署程式中經歷這些階段：

1. 開發人員會將某些程式碼簽入 Team Foundation Server （TFS）2010。
2. TFS 會建立程式碼，並執行與 team 專案相關聯的任何單元測試。
3. TFS 會將方案部署到測試環境。
4. 開發人員小組在測試環境中驗證和驗證方案。
5. 預備環境系統管理員會對預備環境執行「假設」部署，以建立部署是否會造成任何問題。
6. 預備環境系統管理員會執行即時部署至預備環境。
7. 此解決方案會在預備環境中進行使用者接受度測試。
8. Web 部署套件會手動匯入到生產環境中。

這些階段會形成持續開發週期的一部分。

![](application-lifecycle-management-from-development-to-production/_static/image1.png)

在實務上，此程式稍有不同，因為您會在查看每個階段的詳細資訊時看到。 Fabrikam，Inc. 使用不同的方法來部署每個目標環境。

![](application-lifecycle-management-from-development-to-production/_static/image2.png)

本主題的其餘部分將探討此部署生命週期的這些主要階段：

- **必要條件**：您必須先設定伺服器基礎結構，然後才能放置部署邏輯。
- **初始開發和部署**：第一次部署方案之前所需執行的動作。
- **要測試的部署**：當開發人員簽入新的程式碼時，如何自動封裝內容並將其部署至測試環境。
- **部署至預備**環境：如何將特定組建部署至預備環境，以及如何執行「假設」部署，以確保部署不會造成任何問題。
- **部署至生產**環境：當網路基礎結構防止遠端部署時，如何將 web 套件匯入到生產環境。

## <a name="prerequisites"></a>Prerequisites

任何部署案例中的第一項工作，是要確保您的伺服器基礎結構符合您部署工具和技術的需求。 在此情況下，Fabrikam，Inc. 已設定其伺服器基礎結構，如下所示：

- TFS 已設定為包含 team 專案集合、組建控制器和組建代理程式。 如需詳細資訊，請參閱設定[自動化 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md) 。
- 測試環境已設定為接受使用 Web Deployment Agent 服務（「遠端代理程式」）的遠端部署，如[案例：設定 Web 部署的測試環境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-test-environment-for-web-deployment.md)和[針對 Web Deploy 發佈的網頁伺服器（遠端代理程式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)中所述。
- 預備環境已設定為接受使用 Web Deploy 處理常式端點的遠端部署，如[案例：設定 Web 部署的預備環境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-staging-environment-for-web-deployment.md)和[設定用於 Web Deploy 發佈的 Web 服務器（Web Deploy 處理常式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)中所述。
- 生產環境已設定為允許系統管理員以手動方式將 web 部署套件匯入 Internet Information Services （IIS）中，如[案例：設定 Web 部署的生產環境](../configuring-server-environments-for-web-deployment/scenario-configuring-a-production-environment-for-web-deployment.md)和[設定用於 Web Deploy 發佈的 Web 服務器（離線部署）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-offline-deployment.md)中所述。

## <a name="initial-development-and-deployment"></a>初始開發和部署

在 Fabrikam，Inc. 開發小組第一次部署 Contact Manager 解決方案之前，它必須執行下列工作：

- 在 TFS 中建立新的 team 專案。
- 建立包含部署邏輯的 Microsoft Build Engine （MSBuild）專案檔案。
- 建立可觸發部署進程的 TFS 組建定義。

### <a name="create-a-new-team-project"></a>建立新的 Team 專案

- TFS 系統管理員（Walters）會為應用程式建立新的 team 專案，如在[TFS 中建立 Team 專案](../configuring-team-foundation-server-for-web-deployment/creating-a-team-project-in-tfs.md)中所述。 接下來，首席開發人員 Matt Hink 會建立基本架構解決方案。 他會將檔案簽入 TFS 中的新 team 專案，如[將內容新增至原始檔控制](../configuring-team-foundation-server-for-web-deployment/adding-content-to-source-control.md)中所述。

### <a name="create-the-deployment-logic"></a>建立部署邏輯

Matt Hink 會使用[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法，來建立各種自訂 MSBuild 專案檔。 Matt 會建立：

- 名為*Publish*的專案檔，其會執行部署進程。 此檔案包含可在方案中建立專案、建立 web 封裝，以及將封裝部署到目的地伺服器環境的 MSBuild 目標。
- 名為*Env-Dev*和*env-Stage*的環境特定專案檔。 其中包含分別適用于測試環境和預備環境的設定，例如連接字串、服務端點，以及將接收 web 封裝之遠端服務的詳細資料。 如需針對特定目的地環境選擇正確設定的指引，請參閱設定[目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

若要執行部署，使用者可以使用 MSBuild 或 Team Build 執行*Publish*檔案，並將相關環境特定專案檔（*env-Dev*或*env-Stage*）的位置指定為命令列引數。 然後， *Publish*檔案會匯入環境特定的專案檔，為每個目標環境建立一組完整的發行指示。

> [!NOTE]
> 這些自訂專案檔案的工作方式與您用來叫用 MSBuild 的機制無關。 例如，您可以直接使用 MSBuild 命令列，如[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述。 您可以從命令檔執行專案檔案，如[建立及執行部署命令](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)檔中所述。 或者，您也可以從 TFS 中的組建定義執行專案檔，如[建立支援部署的組建定義](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)中所述。  
> 在每個案例中，最後的結果&#x2014;都是相同的 MSBuild 會執行合併的專案檔，並將您的方案部署至目標環境。 這可讓您在觸發發佈程式的方式上有很大的彈性。

一旦建立自訂專案檔之後，Matt 會將其加入至方案資料夾，並將它們簽入原始檔控制中。

### <a name="create-build-definitions"></a>建立組建定義

做為最後的準備工作，Matt 和解決方式會共同為新的 team 專案建立三個組建定義：

- **DeployToTest**。 這會建立 Contact Manager 解決方案，並在每次發生簽入時將其部署至測試環境。
- **DeployToStaging**。 這會在開發人員將組建排入佇列時，將資源從指定的先前組建部署至預備環境。
- **DeployToStaging-WhatIf**。 當開發人員將組建排入佇列時，這會執行「假設」部署至預備環境。

下列各節提供每個組建定義的更多詳細資料。

## <a name="deployment-to-test"></a>要測試的部署

Fabrikam，Inc. 的開發小組會維護測試環境，以進行各種軟體測試活動，例如驗證和驗證、可用性測試、相容性測試，以及特定或探索式測試。

開發小組已在 TFS 中建立名為**DeployToTest**的組建定義。 此組建定義使用連續整合觸發程式，這表示每次 Fabrikam，Inc. 開發小組的成員執行簽入時，就會執行組建程式。 觸發組建時，組建定義將會：

- 建立 ContactManager 的方案。 這接著會建立方案中的每個專案。
- 在方案資料夾結構中執行任何單元測試（如果成功建立方案）。
- 執行控制部署程式的自訂專案檔（如果解決方案成功建立並通過任何單元測試）。

最後的結果是，如果解決方案成功建立並通過單元測試，則 web 封裝和任何其他部署資源都會部署到測試環境。

![](application-lifecycle-management-from-development-to-production/_static/image3.png)

### <a name="how-does-the-deployment-process-work"></a>部署程式如何運作？

**DeployToTest**組建定義會將這些引數提供給 MSBuild：

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample1.cmd)]

當 Team Build 在方案中建立專案時，會使用**DeployOnBuild = true**和**DeployTarget = package**屬性。 當專案是 web 應用程式專案時，這些屬性會指示 MSBuild 為專案建立 web 部署封裝。 **TargetEnvPropsFile**屬性會告訴*Publish*檔案，在何處尋找要匯入的環境特定專案檔案。

> [!NOTE]
> 如需如何建立像這樣的組建定義的詳細逐步解說，請參閱[建立支援部署的組建定義](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。

*Publish*檔案包含在方案中建立每個專案的目標。 不過，如果您正在 Team Build 中執行檔案，它也會包含略過這些組建目標的條件式邏輯。 這可讓您利用 Team Build 所提供的額外組建功能，例如執行單元測試的能力。 如果解決方案組建或單元測試失敗，將不會執行*Publish*檔案，且不會部署應用程式。

條件式邏輯是藉由評估**BuildingInTeamBuild**屬性來完成。 這是 MSBuild 屬性，當您使用 Team Build 來建立專案時，它會自動設定為**true** 。

## <a name="deployment-to-staging"></a>部署至預備環境

當組建符合測試環境中開發人員小組的所有需求時，小組可能會想要將相同的組建部署至預備環境。 預備環境通常會設定為盡可能符合生產或「即時」環境的特性，例如伺服器規格、作業系統和軟體，以及網路設定。 預備環境通常用於負載測試、使用者接受度測試和更廣泛的內部評論。 組建會直接從組建伺服器部署至預備環境。

![](application-lifecycle-management-from-development-to-production/_static/image4.png)

用來將解決方案部署至預備環境（ **DeployToStaging-WhatIf**和**DeployToStaging**）的組建定義會共用下列特性：

- 它們實際上不會建立任何專案。 當您將解決方案部署至預備環境時，他想要部署已在測試環境中驗證並驗證的特定現有組建。 組建定義只需要執行控制部署進程的自訂專案檔。
- 當 [使用] 觸發組建時，他會使用組建參數來指定哪個組建包含想要從組建伺服器部署的資源。
- 組建定義不會自動觸發。 當您想要將解決方案部署至預備環境時，會以手動方式將組建排入佇列。

這是部署至預備環境的高階程式：

1. 預備環境系統管理員（Walters）會使用**DeployToStaging-WhatIf**組建定義將組建排入佇列。 使用「建立定義」參數來指定想要部署的組建。
2. **DeployToStaging-WhatIf**組建定義會在 "what if" 模式下執行自訂專案檔案。 這會產生記錄檔，就好像在執行即時部署時一樣，但它實際上不會對目的地環境進行任何變更。
3. [的資訊] 會檢查記錄檔，以確定部署在預備環境中的效果。 特別是，您應該先檢查要新增的內容、將更新的內容，以及將刪除的內容。
4. 如果您認為部署不會對現有的資源或資料進行任何不必要的變更，他會使用**DeployToStaging**組建定義將組建排入佇列。
5. **DeployToStaging**組建定義會執行自訂專案檔案。 這些會將部署資源發佈至預備環境中的主要 web 伺服器。
6. Web 伺服陣列架構（WFF）控制器會同步處理預備環境中的 web 伺服器。 這可讓應用程式在伺服器陣列中的所有 web 伺服器上使用。

### <a name="how-does-the-deployment-process-work"></a>部署程式如何運作？

**DeployToStaging**組建定義會將這些引數提供給 MSBuild：

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample2.cmd)]

**TargetEnvPropsFile**屬性會告訴*Publish*檔案，在何處尋找要匯入的環境特定專案檔案。 **OutputRoot**屬性會覆寫內建值，並指出包含您要部署之資源的組建資料夾位置。 當您將組建排入佇列時，他會使用 [**參數**] 索引標籤來提供**OutputRoot**屬性的更新值。

![](application-lifecycle-management-from-development-to-production/_static/image5.png)

> [!NOTE]
> 如需如何建立像這樣的組建定義的詳細資訊，請參閱[部署特定的組建](../configuring-team-foundation-server-for-web-deployment/deploying-a-specific-build.md)。

**DeployToStaging-WhatIf**組建定義包含與**DeployToStaging**組建定義相同的部署邏輯。 不過，它包含額外的引數**WhatIf = true**：

[!code-console[Main](application-lifecycle-management-from-development-to-production/samples/sample3.cmd)]

在*Publish*檔案中， **WhatIf**屬性會指出所有部署資源都應該以「假設」模式發佈。 換句話說，記錄檔的產生方式就如同部署已向前，但是目的地環境中沒有任何實際變更。 這可讓您評估建議部署&#x2014;的影響，特別是要新增的內容、要更新的內容，以及在您實際進行任何&#x2014;變更之前將會刪除的內容。

> [!NOTE]
> 如需有關如何設定「假設」部署的詳細資訊，請參閱[執行「What If」部署](../advanced-enterprise-web-deployment/performing-a-what-if-deployment.md)。

在預備環境中將應用程式部署至主要 web 伺服器後，WFF 會自動同步處理伺服器陣列中所有伺服器上的應用程式。

> [!NOTE]
> 如需設定 WFF 來同步處理 web 伺服器的詳細資訊，請參閱[使用 web 伺服陣列架構建立伺服器](../configuring-server-environments-for-web-deployment/creating-a-server-farm-with-the-web-farm-framework.md)陣列。

## <a name="deployment-to-production"></a>部署至生產環境

在預備環境中核准組建之後，Fabrikam，Inc. 小組可以將應用程式發行至生產環境。 「生產環境」是指應用程式「上線」，並觸及其目標物件的使用者。

生產環境是在網際網路面向的周邊網路中。 這會與包含組建伺服器的內部網路隔離。 「生產環境管理員」 Lisa Andrews 必須手動從組建伺服器複製 web 部署套件，並將它們匯入到主要生產 web 伺服器上的 IIS 中。

![](application-lifecycle-management-from-development-to-production/_static/image6.png)

這是部署到生產環境的高階程式：

1. 開發人員小組建議在 Lisa 中，有一個組建已準備好部署到生產環境。 小組會建議在組建伺服器上放置資料夾中的 web 部署套件位置。
2. Lisa 會從組建伺服器收集 web 套件，並將它們複製到生產環境中的主要 web 伺服器。
3. Lisa 使用 IIS 管理員來匯入及發佈主要 web 伺服器上的網頁封裝。
4. WFF 控制器會同步處理生產環境中的 web 伺服器。 這可讓應用程式在伺服器陣列中的所有 web 伺服器上使用。

### <a name="how-does-the-deployment-process-work"></a>部署程式如何運作？

IIS 管理員包含 [匯入應用程式套件]，可讓您輕鬆地將網頁封裝發佈至 IIS 網站。 如需如何執行此程式的逐步解說，請參閱[手動安裝網頁封裝](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)。

## <a name="conclusion"></a>結論

本主題提供一般企業規模 web 應用程式的部署生命週期說明。

本主題會形成一系列教學課程的一部分，以提供 web 應用程式部署各個層面的指引。 實際上，在部署程式的每個階段都有許多額外的工作和考慮，而且無法在單一逐步解說中全部涵蓋。 如需詳細資訊，請參閱下列教學課程：

- [企業中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)。 本教學課程提供使用 MSBuild 和 IIS Web 部署工具（Web Deploy）之 web 部署技術的完整簡介。
- 設定[Web 部署的伺服器環境](../configuring-server-environments-for-web-deployment/configuring-server-environments-for-web-deployment.md)。 本教學課程提供如何設定 Windows server 環境以支援各種部署案例的指引。
- 設定[自動 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 本教學課程提供如何將部署邏輯整合到 TFS 組建程式中的指引。
- [先進的企業 Web 部署](../advanced-enterprise-web-deployment/advanced-enterprise-web-deployment.md)。 本教學課程提供有關如何滿足組織所面臨的一些較複雜部署挑戰的指引。

> [!div class="step-by-step"]
> [上一篇](enterprise-web-deployment-scenario-overview.md)
