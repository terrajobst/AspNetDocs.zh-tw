---
uid: web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
title: 設定目標環境的部署屬性 |Microsoft Docs
author: jrjlee
description: 本主題描述如何設定環境特定的屬性，以便將範例 Contact Manager 解決方案部署到特定目標環境 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: b5b86e03-b8ed-46e6-90fa-e1da88ef34e9
msc.legacyurl: /web-forms/overview/deployment/configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment
msc.type: authoredcontent
ms.openlocfilehash: 9742be7d718384c1b108d5f2c0c43e8e8d4fe8a9
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636441"
---
# <a name="configuring-deployment-properties-for-a-target-environment"></a>設定目標環境的部署屬性

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何設定環境特定的屬性，以便將範例 Contact Manager 解決方案部署至特定的目標環境。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)解決方案&#x2014;的範例解決方案，來代表具有實際複雜度層級的 WEB 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案檔所控制&#x2014;，其中一個包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="process-overview"></a>程序概觀

您將用來建立及部署 Contact Manager 解決方案的專案檔會分割成兩個實體檔案：

- 其中一個包含萬用群組建設定和指示（ *Publish*檔案）。
- 其中一個包含環境特定的組建設定（*env-Dev*、 *env-Stage*等等）。

在組建期間，適當的環境特定專案檔會合並到通用的*Publish*檔案中，以形成一組完整的組建指示。 您可以使用描述您自己的部署案例的設定，來建立或自訂環境特定的專案檔，以設定特定目的地環境的部署。

其中有許多值取決於您的目的地環境的設定&#x2014;方式，無論您的目標網頁伺服器是設定為使用 Web Deployment Agent 服務（遠端代理程式）還是 Web Deploy 處理常式。 如需這些方法的詳細資訊，以及有關為您自己的環境選擇正確方法的指引，請參閱[選擇正確的 Web 部署方法](choosing-the-right-approach-to-web-deployment.md)。

[Contact Manager 案例](../deploying-web-applications-in-enterprise-scenarios/enterprise-web-deployment-scenario-overview.md)需要兩個環境特定的專案檔：

- 部署至開發人員測試環境（*Env-Dev*）。 開發人員測試環境已設定為接受使用遠端代理程式的遠端部署，如[案例：設定 Web 部署的測試環境](scenario-configuring-a-test-environment-for-web-deployment.md)中所述。 此檔案必須提供遠端代理程式端點位址，以及特定位置的設定，例如連接字串和服務端點。
- 部署至預備環境（*Env-Stage*）。 預備環境已設定為接受使用 Web Deploy 處理常式的遠端部署，如[案例：設定 Web 部署的預備環境](scenario-configuring-a-staging-environment-for-web-deployment.md)中所述。 此檔案必須提供 Web Deploy 處理常式端點位址，以及特定位置的設定，例如連接字串和服務端點。

請務必注意，您在環境特定的專案檔中設定的設定不會影響 web 套件本身&#x2014;的內容，而是會控制封裝的部署方式，以及解壓縮封裝時所提供的參數值。 您正以手動方式將 web 套件匯入到生產環境，如[案例：設定 Web 部署的生產環境](scenario-configuring-a-production-environment-for-web-deployment.md)和[手動安裝 web 套件](../web-deployment-in-the-enterprise/manually-installing-web-packages.md)中所述，因此當您在產生封裝時，在環境特定的專案檔中使用了哪些設定並不重要。 當您匯入封裝時，Internet Information Services （IIS）管理員會提示您輸入任何參數化的值，例如連接字串和服務端點。

若要將 Contact Manager 解決方案部署至您自己的目標環境，您可以自訂此檔案，或使用它做為範本，並建立您自己的檔案。

**設定 Contact Manager 解決方案的環境特定部署設定**

1. 在 Visual Studio 2010 中開啟 ContactManager-WCF 方案。
2. 在 [**方案總管**] 視窗中，依序展開 [**發行**] 資料夾、[ **EnvConfig** ] 資料夾，然後按兩下 [ **Env-Dev. proj**]。

    ![](configuring-deployment-properties-for-a-target-environment/_static/image1.png)
3. 將*Env Dev*檔案中的屬性值取代為您自己的測試環境的正確值。

    > [!NOTE]
    > 遵循此程式的表格會提供每個屬性的詳細資訊。
4. 儲存您的工作，然後關閉*Env Dev proj*檔案。

## <a name="choosing-the-right-deployment-properties"></a>選擇正確的部署屬性

下表描述範例環境特定專案檔（ *Env Dev*）中每個屬性的用途，並針對您應該提供的值提供一些指引。

|                                                        屬性名稱                                                         |                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                        詳細資料                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                                         |
|------------------------------------------------------------------------------------------------------------------------------|------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------------|
|              <strong>MSDeployComputerName</strong>目的地 web 伺服器或服務端點的名稱。               |                                                                                                                                                                                                                                              如果您要部署到目的地 web 伺服器上的遠端代理程式服務，可以指定目標電腦名稱稱（例如， <strong>TESTWEB1</strong>或<strong>TESTWEB1.fabrikam.net</strong>），也可以指定遠端代理程式端點（例如 `http://TESTWEB1/MSDEPLOYAGENTSERVICE`）。 在每個案例中，部署的運作方式都相同。 如果您要部署到目的地 Web 服務器上的 Web Deploy 處理常式，則應該指定服務端點，並將 IIS 網站的名稱包含為查詢字串參數（例如，`https://STAGEWEB1:8172/MSDeploy.axd?site=DemoSite`）。                                                                                                                                                                                                                                              |
|         <strong>MSDeployAuth</strong>Web Deploy 應該用來驗證遠端電腦的方法。          |                                                                                                                                                                                                                          這應該設定為 [ <strong>NTLM</strong> ] 或 [<strong>基本</strong>]。 一般而言，如果您要部署至遠端代理程式服務，則會使用<strong>NTLM</strong> ，而如果您要部署到 Web Deploy 處理常式，則會使用<strong>基本</strong>。 如果您使用基本驗證，您也必須指定 IIS Web Deployment Tool （Web Deploy）應模擬的使用者名稱和密碼，才能執行部署。 在此範例中，這些值是透過<strong>MSDeployUsername</strong>和<strong>MSDeployPassword</strong>屬性來提供。 如果您使用 NTLM 驗證，則可以省略這些屬性，或將它們保留空白。                                                                                                                                                                                                                          |
| <strong>MSDeployUsername</strong>如果您使用基本驗證，Web Deploy 將會在遠端電腦上使用此帳戶。  |                                                                                                                                                                                                                                                                                                                                                                                                                       這應該會採用表單<em>網域</em>\*使用者名稱 * （例如<strong>FABRIKAM\matt</strong>）。 只有在您指定 [基本驗證] 時，才會使用此值。 如果您使用 NTLM 驗證，則可以省略屬性。 如果提供值，則會忽略它。                                                                                                                                                                                                                                                                                                                                                                                                                        |
| <strong>MSDeployPassword</strong>如果您使用基本驗證，Web Deploy 將會在遠端電腦上使用此密碼。 |                                                                                                                                                                                                                                                                                                                                                                                                                    這是您在<strong>MSDeployUsername</strong>屬性中指定之使用者帳戶的密碼。 只有在您指定 [基本驗證] 時，才會使用此值。 如果您使用 NTLM 驗證，則可以省略屬性。 如果提供值，則會忽略它。                                                                                                                                                                                                                                                                                                                                                                                                                    |
|     <strong>ContactManagerIisPath</strong>您想要在其上部署 Contact Manager MVC 應用程式的 IIS 路徑。     |                                                                                                                                                                                                                                                                                                                                                                        這應該是出現在 IIS 管理員中的路徑，格式為 [<em>iis 網站名稱</em>]/[<em>web</em><em>應用程式名稱</em>]。 請記住，在部署應用程式之前，IIS 網站必須存在。 例如，如果您已建立名為 DemoSite 的 IIS 網站，則可以將 MVC 應用程式的 IIS 路徑指定為 DemoSite/ContactManager。                                                                                                                                                                                                                                                                                                                                                                        |
|   <strong>ContactManagerServiceIisPath</strong>您想要在其上部署 Contact Manager WCF 服務的 IIS 路徑。    |                                                                                                                                                                                                                                                                                                                                                                                                                                                                          例如，如果您已建立名為 DemoSite 的 IIS 網站，則可以將 WCF 服務的 IIS 路徑指定為<strong>DemoSite/ContactManagerService</strong>。                                                                                                                                                                                                                                                                                                                                                                                                                                                                          |
|                  <strong>ContactManagerTargetUrl</strong>可在其上到達 WCF 服務的 URL。                   |                                                                                                                                                     這會採用下列格式： [<em>IIS 網站根 URL</em>]/[<em>服務應用程式名稱</em>]/[<em>服務端點</em>]。 例如，如果您已在埠85上建立 IIS 網站，則 URL 的格式會是 `http://localhost:85/ContactManagerService/ContactService.svc`。 請記住，MVC 應用程式和 WCF 服務會部署到相同的伺服器。 因此，此 URL 只會從其安裝所在的電腦存取。 因此，最好是在 URL 中使用 localhost 或 IP 位址，而不是電腦名稱稱或主機標頭。 如果您使用電腦名稱稱或主機標頭，IIS 中的[回送檢查](https://go.microsoft.com/?linkid=9805131)安全性功能可能會封鎖 URL，並傳回<strong>HTTP 401.1-未經授權</strong>的錯誤。                                                                                                                                                     |
|                  <strong>CmDatabaseConnectionString</strong>資料庫伺服器的連接字串。                  | 連接字串會決定 VSDBCMD 將用來與資料庫伺服器連線的認證，並建立資料庫和網頁伺服器應用程式集區將用來連線資料庫伺服器並與資料庫互動的認證。 基本上，您有兩個選擇。 您可以指定<strong>整合式安全性 = true</strong>，在此情況下會使用整合式 Windows 驗證： <strong>DATA Source = TESTDB1; 整合式安全性 = true</strong>在此情況下，將會使用執行 VSDBCMD 可執行檔之使用者的認證來建立資料庫，而應用程式會使用 web 伺服器電腦帳戶的身分識別來存取資料庫。 或者，您也可以指定 SQL Server 帳戶的使用者名稱和密碼。 在此情況下，VSDBCMD 會使用 SQL Server 認證來建立資料庫，而由應用程式集區用來與資料庫互動： <strong>Data Source = TESTDB1;使用者識別碼 = ASqlUser;Password = Pa $ $w 0rd</strong>本主題中的逐步解說假設您將使用整合式 Windows 驗證。 |
|        <strong>CmTargetDatabase</strong>您想要授與資料庫伺服器上所建立之資料庫的名稱。        |                                                                                                                                                                                                                                                                                                                                                                                                                                                     您在此處提供的值會新增至 VSDBCMD 命令做為參數。 它也可用來建立完整的連接字串，讓 web 伺服器上的應用程式集區可以用來與資料庫互動。                                                                                                                                                                                                                                                                                                                                                                                                                                                     |

這些範例會示範如何針對特定的部署案例設定這些屬性。

### <a name="example-1x2014deployment-to-the-remote-agent-service"></a>部署至&#x2014;遠端代理程式服務的範例1

在這個範例中：

- 您要部署到 TESTWEB1 上的遠端代理程式服務。
- 您正指示 Web Deploy 使用 NTLM 驗證。 Web Deploy 將使用您用來叫用 Microsoft Build Engine （MSBuild）的認證來執行。
- 您使用整合式驗證將**ContactManager**資料庫部署至 TESTDB1。 將使用您用來叫用 MSBuild 的認證來部署資料庫。

[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample1.xml)]

### <a name="example-2x2014deployment-to-the-web-deploy-handler-endpoint"></a>範例 2&#x2014;部署至 Web Deploy 處理常式端點

在這個範例中：

- 您要部署到 STAGEWEB1 上的 Web Deploy 處理常式服務端點。
- 您正指示 Web Deploy 使用基本驗證。
- 您要指定 Web Deploy 應該模擬遠端電腦上的 FABRIKAM\stagingdeployer 帳戶。
- 您正在使用 SQL Server authentication 將**ContactManager**資料庫部署至 STAGEDB1。

[!code-xml[Main](configuring-deployment-properties-for-a-target-environment/samples/sample2.xml)]

## <a name="conclusion"></a>結論

此時，您的專案檔已完全設定為可建立 Contact Manager 解決方案，並將其部署到一或多個目的地環境。

若要使用這些專案檔做為單一步驟、可重複部署程式的一部分，您需要使用 MSBuild 執行*Publish*檔案，並傳入環境特定專案檔的位置做為參數。 您可以透過各種方式來執行這項操作：

- 如需 MSBuild 和自訂專案檔簡介的總覽，請參閱[瞭解專案檔案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)。
- 如需如何制訂執行自訂專案檔之 MSBuild 命令的相關資訊，請參閱[部署 Web 套件](../web-deployment-in-the-enterprise/deploying-web-packages.md)。
- 如需如何將 MSBuild 命令併入命令檔中進行單一步驟、可重複部署的相關資訊，請參閱[建立和執行部署命令](../web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file.md)檔。
- 如需如何從 Team Build 執行自訂專案檔的詳細資訊，請參閱[建立支援部署的組建定義](../configuring-team-foundation-server-for-web-deployment/creating-a-build-definition-that-supports-deployment.md)。

> [!div class="step-by-step"]
> [上一篇](creating-a-server-farm-with-the-web-farm-framework.md)
