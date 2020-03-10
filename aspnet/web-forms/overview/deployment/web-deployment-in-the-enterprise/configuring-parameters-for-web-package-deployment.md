---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
title: 設定 Web 套件部署的參數 |Microsoft Docs
author: jrjlee
description: 本主題描述如何設定參數值，例如 Internet Information Services （IIS） web 應用程式名稱、連接字串和服務端點,。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 37947d79-ab1e-4ba9-9017-52e7a2757414
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/configuring-parameters-for-web-package-deployment
msc.type: authoredcontent
ms.openlocfilehash: f04ace98d81a33053b10cab7e40dbd75a6c0992c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78544951"
---
# <a name="configuring-parameters-for-web-package-deployment"></a>設定 Web 套件部署的參數

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述當您將 web 封裝部署到遠端 IIS web 伺服器時，如何設定參數值，例如 Internet Information Services （IIS） web 應用程式名稱、連接字串和服務端點。

當您建立 web 應用程式專案時，組建和封裝進程會產生三個主要檔案：

- *[專案名稱] .zip*檔案。 這是 web 應用程式專案的 web 部署套件。 此套件包含在遠端 IIS 網頁伺服器上重新建立 web 應用程式所需的所有元件、檔案、資料庫腳本和資源。
- *[專案名稱]. 部署 .cmd*檔案。 這包含一組參數化 Web Deploy （Msdeploy.exe）命令，可將您的 Web 部署套件發佈至遠端 IIS Web 服務器。
- *[專案名稱]。SetParameters .xml*檔案。 這會提供一組參數值給 Msdeploy.exe 命令。 當您部署 Web 套件時，可以更新此檔案中的值，並將它傳遞給 Web Deploy 做為命令列參數。

> [!NOTE]
> 如需組建和封裝程式的詳細資訊，請參閱[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)。

*SetParameters*是從您的 web 應用程式專案檔案和專案內的任何設定檔動態產生的。 當您建立並封裝您的專案時，Web 發佈管線（WPP）會自動偵測許多可能在部署環境（例如目的地 IIS Web 應用程式和任何資料庫連接字串）之間變更的變數。 這些值會自動在 web 部署套件中進行參數化，並加入至*SetParameters*檔案。 例如，如果您將連接字串加入*至 web 應用*程式專案中的 web.config 檔案，則組建進程會偵測到這項變更，並據此將專案新增至*SetParameters。*

在許多情況下，此自動參數化就已足夠。 不過，如果您的使用者需要變更部署環境（例如應用程式設定或服務端點 Url）之間的其他設定，您必須告訴 WPP 將部署套件中的這些值參數化，並將對應的專案加入至*SetParameters。* 接下來的各節將說明如何執行此動作。

### <a name="automatic-parameterization"></a>自動參數化

當您建立並封裝 web 應用程式時，WPP 會自動將這些專案參數化：

- 目的地 IIS web 應用程式路徑和名稱。
- *Web.config 檔案*中的任何連接字串。
- 您加入至專案屬性頁中 [**封裝/發行 SQL** ] 索引標籤之任何資料庫的連接字串。

例如，如果您要建立並封裝[Contact Manager](the-contact-manager-solution.md)範例解決方案，而不需要以任何方式觸及參數化程式，則 WPP 會產生這個*ContactManager SetParameters .xml*檔案：

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample1.xml)]

在此情況下：

- **Iis Web 應用程式名稱**參數是您想要部署 Web 應用程式的 iis 路徑。 預設值取自 [專案] 屬性頁中的 [**封裝/發行**] 網頁。
- **Microsoft.visualbasic.applicationservices.cantstartsingleinstanceexception-Web.config 連接字串**參數是從*web.config*檔案中的**connectionStrings/add**元素所產生。 它代表應用程式應該用來與成員資格資料庫聯繫的連接字串。 您在此處提供的值將會被取代為已部署的*web.config*檔案。 預設值取自預先部署的*web.config*檔案。

WPP 也會在它所產生的部署套件中參數化這些屬性。 當您安裝部署套件時，可以提供這些屬性的值。 如果您透過 IIS 管理員以手動方式安裝套件（如[手動安裝網頁套件](manually-installing-web-packages.md)中所述），安裝精靈會提示您提供任何參數的值。 如果您使用*deploy .cmd*檔案從遠端安裝封裝（如[部署 Web 套件](deploying-web-packages.md)中所述），Web Deploy 將會查看這個*SetParameters*檔以提供參數值。 您可以手動編輯*SetParameters*中的值，也可以自訂檔案做為自動化組建和部署程式的一部分。 本主題稍後將更詳細地說明此程式。

### <a name="custom-parameterization"></a>自訂參數化

在更複雜的部署案例中，您通常會想要在部署專案之前，先參數化其他屬性。 一般來說，您應該將任何會因目的地環境而異的屬性和設定參數化。 這些可能包括：

- *Web.config 檔案中的服務*端點。
- *Web.config 檔案中的應用*程式設定。
- 您想要提示使用者指定的任何其他宣告式屬性。

將這些屬性參數化的最簡單方式，就是將*參數 .xml*檔案加入至 web 應用程式專案的根資料夾。 例如，在 Contact Manager 解決方案中，ContactManager 專案會在根資料夾中包含*parameters .xml*檔案。

![](configuring-parameters-for-web-package-deployment/_static/image1.png)

如果您開啟這個檔案，您會看到它包含單一**參數**專案。 此專案使用 XML 路徑語言（XPath）查詢，在*web.config*檔案中找出並參數化 ContactService WINDOWS COMMUNICATION FOUNDATION （WCF）服務的端點 URL。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample2.xml)]

除了將部署套件中的端點 URL 參數化，WPP 也會將對應的專案加入至與部署套件一起產生的*SetParameters。*

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample3.xml)]

如果您手動安裝部署套件，IIS 管理員會提示您提供服務端點位址與自動參數化的屬性。 如果您藉由執行 *.deploy*檔案來安裝部署套件，您可以編輯*SetParameters* ，以提供服務端點位址的值，以及自動參數化之屬性的值。

如需如何建立*參數 .xml*檔案的完整詳細資訊，請參閱[如何：在安裝套件時使用參數來設定部署設定](https://msdn.microsoft.com/library/ff398068.aspx)。 名為的程式會使用 web.config 檔案**設定的部署參數來**提供逐步指示。

## <a name="modifying-the-setparametersxml-file"></a>修改 SetParameters .xml 檔案

如果您打算&#x2014;以手動方式部署 web 應用程式封裝，請執行 *. deploy .cmd*檔案，或從命令列&#x2014;執行 msdeploy.exe，這不會讓您在部署之前手動編輯*SetParameters。* 不過，如果您正在處理企業規模的解決方案，您可能需要部署 web 應用程式封裝，做為較大、自動化的組建和部署流程的一部分。 在此案例中，您需要 Microsoft Build Engine （MSBuild）為您修改*SetParameters。* 您可以使用 MSBuild **XmlPoke**工作來執行這項作業。

[Contact Manager 範例解決方案](the-contact-manager-solution.md)會說明此程式。 接下來的程式碼範例已編輯，只會顯示與此範例相關的詳細資料。

> [!NOTE]
> 如需範例方案中的專案檔模型，以及一般自訂專案檔案的簡介，請參閱[瞭解專案](understanding-the-project-file.md)檔和[瞭解組建](understanding-the-build-process.md)程式。

首先，會將感興趣的參數值定義為環境特定專案檔中的屬性（例如， *Env-Dev*）。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample4.xml)]

> [!NOTE]
> 如需如何為您自己的伺服器環境自訂環境特定專案檔案的指引，請參閱設定[目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

接下來， *Publish*檔案會匯入這些屬性。 因為每個*SetParameters*檔案都與一個 *.deploy*檔案相關聯，而我們最終希望專案檔叫用每個 *.deploy*檔案，所以專案檔會*為每個 .deploy 檔案*建立一個 MSBuild*專案*，並將相關的屬性定義為*專案中繼資料*。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample5.xml)]

在此情況下：

- **ParametersXml**中繼資料值表示*SetParameters*的位置。
- **IisWebAppName**值是您要部署 web 應用程式的 IIS 路徑。
- **MembershipDBConnectionString**值是成員資格資料庫的連接字串，而**MembershipDBConnectionName**值是*SetParameters .xml*檔案中對應參數的**名稱**屬性。
- **ServiceEndpointValue**值是目的地伺服器上 WCF 服務的端點位址，而**ServiceEndpointParamName**值是*SetParameters .xml*檔案中對應參數的名稱屬性。

最後，在*Publish*檔案中， **PublishWebPackages**目標會使用**XmlPoke**工作來修改*SetParameters*檔案中的這些值。

[!code-xml[Main](configuring-parameters-for-web-package-deployment/samples/sample6.xml)]

您會注意到每個**XmlPoke**工作都指定四個屬性值：

- **XmlInputPath**屬性會告知工作要在何處尋找您要修改的檔案。
- **查詢**屬性是用來識別您要變更之 XML 節點的 XPath 查詢。
- **Value**屬性是您想要插入至所選取 XML 節點的新值。
- **Condition**屬性是工作應該執行或不執行的準則。 在這些情況下，條件可確保您不會嘗試在*SetParameters*中插入 null 或空白值。

## <a name="conclusion"></a>結論

本主題描述*SetParameters*的角色，並說明當您建立 web 應用程式專案時，其產生方式。 文中說明如何藉由將*參數 .xml*檔案加入至專案中，來參數化其他設定。 文中也說明了如何使用專案檔中的**XmlPoke**工作，以較大的自動化組建程式來修改*SetParameters。*

下一個主題 [[部署 Web 套件](deploying-web-packages.md)] 描述如何藉由執行 *.deploy*檔案或直接使用 msdeploy.exe 命令來部署 web 封裝。 在這兩種情況下，您都可以將*SetParameters*指定為部署參數。

## <a name="further-reading"></a>進一步閱讀

如需如何建立 web 封裝的相關資訊，請參閱[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)。 如需如何實際部署 web 套件的指引，請參閱[部署 Web 套件](deploying-web-packages.md)。 如需如何建立*參數 .xml*檔案的逐步解說，請參閱[如何：在安裝套件時使用參數來設定部署設定](https://msdn.microsoft.com/library/ff398068.aspx)。

如需 Web Deploy 中參數化的一般資訊，請參閱[Web Deploy 參數化動作](https://go.microsoft.com/?linkid=9805119)（blog 文章）。

> [!div class="step-by-step"]
> [上一頁](building-and-packaging-web-application-projects.md)
> [下一頁](deploying-web-packages.md)
