---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
title: 執行 What If 部署 |Microsoft Docs
author: jrjlee
description: 本主題描述如何使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）和 V ... 來執行「假設」（或模擬）部署
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c711b453-01ac-4e65-a48c-93d99bf22e58
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/performing-a-what-if-deployment
msc.type: authoredcontent
ms.openlocfilehash: 73a0e038cc0d4ebae0ffc8ed3fd2de4c9dad673c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78628888"
---
# <a name="performing-a-what-if-deployment"></a>執行 "What If" 部署

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）和 VSDBCMD 來執行「假設」（或模擬）部署。 這可讓您在實際部署應用程式之前，判斷部署邏輯在特定目標環境上的效果。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建和部署程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="performing-a-what-if-deployment-for-web-packages"></a>執行 Web 套件的「What If」部署

Web Deploy 包含的功能可讓您在「假設」（或試用）模式中執行部署。 當您以「假設」模式部署成品時，Web Deploy 會產生記錄檔，如同您已執行部署，但它實際上不會變更目的地伺服器上的任何專案。 查看記錄檔可協助您瞭解部署在目的地伺服器上的影響，特別是：

- 將新增哪些內容。
- 會更新哪些內容。
- 將刪除的內容。

由於「假設」部署實際上不會變更目的地伺服器上的任何專案，因此不一定會預測部署是否會成功。

如[部署 Web 套件](../web-deployment-in-the-enterprise/deploying-web-packages.md)中所述，您可以透過兩種方式&#x2014;使用 Web Deploy 部署 web 封裝，方法是直接使用 msdeploy.exe 命令列公用程式，或執行組建程式所產生的 *.deploy .cmd*檔案。

如果您直接使用 Msdeploy.exe，可以將 **– whatif**旗標新增至您的命令，以執行「假設」部署。 例如，若要評估在將 ContactManager 部署至預備環境時，會發生什麼情況，請使用 Msdeploy.exe 命令，如下所示：

[!code-console[Main](performing-a-what-if-deployment/samples/sample1.cmd)]

當您滿意「假設」部署的結果時，您可以移除 **– whatif**旗標來執行即時部署。

> [!NOTE]
> 如需有關 Msdeploy.exe 之命令列選項的詳細資訊，請參閱[Web Deploy 作業設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。

如果您使用的是 *.deploy*檔案，您可以在命令中包含 **/t**旗標（試用模式）旗標，而不是 **/y**旗標（[是] 或 [更新模式]）來執行「假設」部署。 例如，若要評估當您執行 *.deploy*檔案部署 ContactManager 封裝時，會發生什麼情況，您的命令應該如下所示：

[!code-console[Main](performing-a-what-if-deployment/samples/sample2.cmd)]

當您滿意「試用模式」部署的結果時，您可以使用 **/y**旗標來取代 **/t**旗標，以執行即時部署：

[!code-console[Main](performing-a-what-if-deployment/samples/sample3.cmd)]

> [!NOTE]
> 如需有關之命令列*選項的詳細*資訊，請參閱[如何：使用 Deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。 如果您執行 *.deploy*檔案，但未指定任何旗標，則命令提示字元會顯示可用的旗標清單。

## <a name="performing-a-what-if-deployment-for-databases"></a>執行資料庫的「What If」部署

本節假設您使用 VSDBCMD 公用程式來執行以架構為基礎的累加式資料庫部署。 [部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)中會更詳細地說明此方法。 我們建議您先熟悉本主題，再套用這裡所述的概念。

當您在**部署**模式中使用 VSDBCMD 時，您可以使用 **/Dd** （或 **/DeployToDatabase**）旗標來控制 VSDBCMD 是否實際部署資料庫，或只產生部署腳本。 如果您要部署 .dbschema 檔案，此行為如下：

- 如果您指定 **/dd +** 或 **/dd**，VSDBCMD 會產生部署腳本並部署資料庫。
- 如果您指定 **/dd-** 或省略參數，VSDBCMD 只會產生部署腳本。

> [!NOTE]
> 如果您部署的是 deploymanifest 檔案，而不是 .dbschema 檔案， **/dd**參數的行為就會變得更複雜。 基本上，如果 deploymanifest 檔案包含值為**True**的**DeployToDatabase**元素，則 VSDBCMD 會忽略 **/dd**參數的值。 [部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)會完整描述此行為。

例如，若要產生**ContactManager**資料庫的部署腳本，而不實際部署資料庫，您的 VSDBCMD 命令應如下所示：

[!code-console[Main](performing-a-what-if-deployment/samples/sample4.cmd)]

VSDBCMD 是差異資料庫部署工具，因此部署腳本會以動態方式產生，以包含將目前資料庫（如果有的話）更新為指定的架構所需的所有 SQL 命令。 檢查部署腳本是一種實用的方法，可判斷您的部署對目前資料庫及其包含的資料有何影響。 例如，您可能會想要判斷：

- 是否將移除任何現有的資料表，以及是否會導致資料遺失。
- 作業的順序是否會造成資料遺失的風險，例如，如果您正在分割或合併資料表。

如果您對部署腳本感到滿意，可以使用 **/dd +** 旗標重複 VSDBCMD 以進行變更。 或者，您可以編輯部署腳本以符合您的需求，然後在資料庫伺服器上手動執行。

## <a name="integrating-what-if-functionality-into-custom-project-files"></a>將「What If」功能整合到自訂專案檔案

在更複雜的部署案例中，您會想要使用自訂的 Microsoft Build Engine （MSBuild）專案檔來封裝您的組建和部署邏輯，如[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述。 例如，在[Contact Manager](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)範例解決方案中， *Publish*檔案：

- 建立解決方案。
- 會使用 Web Deploy 來封裝和部署 ContactManager 的 Mvc 應用程式。
- 會使用 Web Deploy 來封裝和部署 ContactManager 服務應用程式。
- 部署**ContactManager**資料庫。

當您以這種方式將多個 web 封裝和/或資料庫的部署整合到單一步驟的程式時，您可能也會想要在「假設」模式下執行整個部署的選項。

*Publish*檔案會示範如何執行此動作。 首先，您必須建立屬性來儲存 "what if" 值：

[!code-xml[Main](performing-a-what-if-deployment/samples/sample5.xml)]

在此情況下，您已建立名為**WhatIf**的屬性，其預設值為**false**。 使用者可以覆寫此值，方法是在命令列參數中將屬性設為**true** ，您很快就會看到。

下一個階段是將任何 Web Deploy 和 VSDBCMD 命令參數化，讓旗標反映**WhatIf**屬性值。 例如，下一個目標（取自*Publish*檔案並簡化）會執行 *.deploy .cmd*檔案以部署 web 封裝。 根據預設，此命令會包含 **/y**參數（[是] 或 [更新模式]）。 如果**WhatIf**設定為**true**，則會以 **/t**參數（試用或「假設」模式）來取代。

[!code-xml[Main](performing-a-what-if-deployment/samples/sample6.xml)]

同樣地，下一個目標會使用 VSDBCMD 公用程式來部署資料庫。 根據預設，不包含 **/dd**參數。 這表示 VSDBCMD 會產生部署腳本，但不會部署資料庫&#x2014;，換句話說，就是「假設」案例。 如果**WhatIf**屬性未設定為**true**，則會新增 **/dd**參數，且 VSDBCMD 會部署資料庫。

[!code-xml[Main](performing-a-what-if-deployment/samples/sample7.xml)]

您可以使用相同的方法，將專案檔中所有相關的命令參數化。 當您想要執行「假設」部署時，您可以直接從命令列提供**WhatIf**屬性值：

[!code-console[Main](performing-a-what-if-deployment/samples/sample8.cmd)]

如此一來，您就可以在單一步驟中針對所有專案元件執行「假設」部署。

## <a name="conclusion"></a>結論

本主題說明如何使用 Web Deploy、VSDBCMD 和 MSBuild 來執行「假設」部署。 「假設」部署可讓您在實際對目的地環境進行任何變更之前，評估建議部署的影響。

## <a name="further-reading"></a>進一步閱讀

如需 Web Deploy 命令列語法的詳細資訊，請參閱[Web Deploy 作業設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。 如需使用 *.deploy*檔案時命令列選項的指引，請參閱[如何：使用 Deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。 如需 VSDBCMD 命令列語法的指引，請參閱[VSDBCMD 的命令列參考。EXE （部署和架構匯入）](https://msdn.microsoft.com/library/dd193283.aspx)。

> [!div class="step-by-step"]
> [上一頁](advanced-enterprise-web-deployment.md)
> [下一頁](customizing-database-deployments-for-multiple-environments.md)
