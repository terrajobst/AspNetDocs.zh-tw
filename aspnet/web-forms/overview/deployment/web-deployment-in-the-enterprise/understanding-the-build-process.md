---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
title: 瞭解組建流程 |Microsoft Docs
author: jrjlee
description: 本主題提供企業規模組建和部署程式的逐步解說。 本主題中所述的方法會使用自訂的 Microsoft Build Engin 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 5b982451-547b-4a2f-a5dc-79bc64d84d40
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/understanding-the-build-process
msc.type: authoredcontent
ms.openlocfilehash: 802d93f7ca987d018967275bae68b8c56d883a25
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78641138"
---
# <a name="understanding-the-build-process"></a>了解建置程序

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題提供企業規模組建和部署程式的逐步解說。 本主題中所述的方法會使用自訂的 Microsoft Build Engine （MSBuild）專案檔，對程式的每個層面提供更細微的控制。 在專案檔中，自訂 MSBuild 目標是用來執行部署公用程式，例如 Internet Information Services （IIS） Web 部署工具（Msdeploy.exe）和資料庫部署公用程式 VSDBCMD。
> 
> > [!NOTE]
> > 上一個主題：[瞭解專案](understanding-the-project-file.md)檔，其中描述 MSBuild 專案檔的主要元件，並引進分割專案檔的概念，以支援部署至多個目標環境。 如果您還不熟悉這些概念，您應該先參閱[瞭解專案](understanding-the-project-file.md)檔，然後再進行本主題。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="build-and-deployment-overview"></a>組建和部署總覽

在[Contact Manager 解決方案](the-contact-manager-solution.md)中，有三個檔案控制組建和部署程式：

- *通用專案*檔（*Publish. proj*）。 這包含不會在目的地環境之間變更的組建和部署指示。
- *環境特定的專案*檔（*Env-Dev. proj*）。 這包含特定目的地環境特有的組建和部署設定。 例如，您可以使用*Env Dev*檔案來提供開發人員或測試環境的設定，並建立名為*Env-Stage*的替代檔案，以提供預備環境的設定。
- *命令*檔（*Publish-Dev .cmd*）。 這包含一個 Msbuild.exe 命令，它會指定您要執行的專案檔。 您可以為每個目的地環境建立命令檔，其中每個檔案都包含指定不同環境特定專案檔案的 Msbuild.exe 命令。 這可讓開發人員藉由執行適當的命令檔，部署至不同的環境。

在範例解決方案中，您可以在 [發行方案] 資料夾中找到這三個檔案。

![](understanding-the-build-process/_static/image1.png)

在您仔細查看這些檔案之前，讓我們先看一下當您使用這種方法時，整體組建程式的運作方式。 概括而言，組建和部署程式看起來像這樣：

![](understanding-the-build-process/_static/image2.png)

第一件事是，這兩個專案檔案&#x2014;包含萬用群組建和部署指示，另一個則包含環境特定的設定&#x2014;，會合並成單一專案檔案。 MSBuild 接著會透過專案檔中的指示運作。 它會使用每個專案的專案檔，建立方案中的每個專案。 接著，它會呼叫其他工具，例如 Web Deploy （Msdeploy.exe）和 VSDBCMD 公用程式，將您的 Web 內容和資料庫部署至目標環境。

從開始到完成，組建和部署程式會執行下列工作：

1. 它會刪除輸出目錄的內容，以準備全新的組建。
2. 它會在解決方案中建立每個專案：

    1. 針對 Web 專案&#x2014;，在此案例中為 ASP.NET MVC web 應用程式和 WCF web&#x2014;服務，組建程式會為每個專案建立 web 部署套件。
    2. 針對資料庫專案，組建程式會為每個專案建立部署資訊清單（. deploymanifest 檔案）。
3. 它會使用 VSDBCMD 公用程式來部署方案中的每個資料庫專案，並使用專案&#x2014;檔中的各種屬性與 deploymanifest 檔案搭配的目標連接&#x2014;字串和資料庫名稱。
4. 它會使用 Msdeploy.exe 公用程式來部署方案中的每個 Web 專案，並使用專案檔中的各種屬性來控制部署流程。

您可以使用範例解決方案，更詳細地追蹤此進程。

> [!NOTE]
> 如需如何為您自己的伺服器環境自訂環境特定專案檔案的指引，請參閱設定[目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

## <a name="invoking-the-build-and-deployment-process"></a>叫用組建和部署進程

若要將「連絡人管理員」方案部署至開發人員測試環境，開發人員可以執行*Publish-Dev*命令檔。 這會叫用 Msbuild.exe，將*Publish*指定為要執行的專案檔，並將*Env Dev*當做參數值。

[!code-console[Main](understanding-the-build-process/samples/sample1.cmd)]

> [!NOTE]
> **/Fl**參數（ **/fileLogger**的 short）會將組建輸出記錄到目前目錄中名為*msbuild.exe*的檔案。 如需詳細資訊，請參閱[MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311.aspx)。

此時，MSBuild 會開始執行、載入*Publish*檔案，然後開始處理其中的指令。 第一個指令會告知 MSBuild 匯入**TargetEnvPropsFile**參數所指定的專案檔。

[!code-xml[Main](understanding-the-build-process/samples/sample2.xml)]

**TargetEnvPropsFile**參數會指定*env dev*檔案，因此 MSBuild 會將*env dev*檔案的內容合併到*Publish*檔案中。

MSBuild 在合併的專案檔中遇到的下一個元素是屬性群組。 屬性會依其出現在檔案中的順序進行處理。 MSBuild 會為每個屬性建立機碼值組，以提供符合的任何指定條件。 稍後在檔案中定義的屬性會覆寫檔案中稍早定義的任何屬性。 例如，請考慮**OutputRoot**屬性。

[!code-xml[Main](understanding-the-build-process/samples/sample3.xml)]

當 MSBuild 處理第一個**OutputRoot**專案時，若未提供類似名稱的參數，則會將**OutputRoot**屬性的值設定為 **。\Publish\Out**。當它遇到第二個**OutputRoot**元素時，如果條件評估為**true**，則會使用**OutDir**參數的值來覆寫**OutputRoot**屬性的值。

MSBuild 遇到的下一個元素是單一專案群組，其中包含名為**ProjectsToBuild**的專案。

[!code-xml[Main](understanding-the-build-process/samples/sample4.xml)]

MSBuild 會藉由建立名為**ProjectsToBuild**的專案清單來處理此指令。 在此情況下，專案清單會包含單一值&#x2014;，其為方案檔的路徑和檔案名。

此時，其餘元素為目標。 目標的處理方式與屬性和專案&#x2014;截然不同，除非是由使用者明確指定，或由專案檔中的另一個結構所叫用，否則不會處理目標。 回想一下，開啟**專案**標記包含**DefaultTargets**屬性。

[!code-xml[Main](understanding-the-build-process/samples/sample5.xml)]

當叫用 Msbuild.exe 時，如果未指定目標，則會指示 MSBuild 叫用**FullPublish**目標。 **FullPublish**目標未包含任何工作;相反地，它只會指定相依性的清單。

[!code-xml[Main](understanding-the-build-process/samples/sample6.xml)]

此相依性會告訴 MSBuild，若要執行**FullPublish**目標，它必須依照提供的順序叫用此目標清單：

1. 它必須叫用**清理**目標。
2. 它必須叫用**BuildProjects**目標。
3. 它必須叫用**GatherPackagesForPublishing**目標。
4. 它必須叫用**PublishDbPackages**目標。
5. 它必須叫用**PublishWebPackages**目標。

### <a name="the-clean-target"></a>清除目標

**清除**目標基本上會刪除輸出目錄及其所有內容，以準備全新的組建。

[!code-xml[Main](understanding-the-build-process/samples/sample7.xml)]

請注意，目標包含**ItemGroup**元素。 當您在**目標**元素內定義屬性或專案時，您正在建立*動態*屬性和專案。 換句話說，在執行目標之前，不會處理屬性或專案。 在建立程式開始之前，輸出目錄可能不存在或包含任何檔案，因此您無法建立 **\_FilesToDelete**清單做為靜態專案;您必須等到執行進行中。 因此，您會將清單建立為目標中的動態專案。

> [!NOTE]
> 在此情況下，由於**清理**目標是要執行的第一個，因此不需要實際使用動態專案群組。 不過，在這種情況下使用動態屬性和專案是很好的作法，因為您可能會想要在某個時間點以不同的循序執行目標。  
> 您也應該將目標設為避免宣告永遠不會使用的專案。 如果您有僅供特定目標使用的專案，請考慮將它們放在目標中，以移除組建程式上任何不必要的額外負荷。

除了動態專案外，**清理**目標也相當簡單，並利用內建的**訊息**、**刪除**和**RemoveDir**工作來執行下列作業：

1. 將訊息傳送至記錄器。
2. 建立要刪除的檔案清單。
3. 刪除檔案。
4. 移除輸出目錄。

### <a name="the-buildprojects-target"></a>BuildProjects 目標

**BuildProjects**目標基本上會建立範例方案中的所有專案。

[!code-xml[Main](understanding-the-build-process/samples/sample8.xml)]

在上一個主題中，您將瞭解此目標的一些詳細資料，也就是[瞭解專案](understanding-the-project-file.md)檔，以說明工作和目標如何參考屬性和專案。 此時，您主要對**MSBuild**工作感興趣。 您可以使用此工作來建立多個專案。 此工作不會建立 Msbuild.exe 的新實例。它會使用目前正在執行的實例來建立每個專案。 此範例中的重點是部署屬性：

- 當每個專案的組建完成時， **DeployOnBuild**屬性會指示 MSBuild 在專案設定中執行任何部署指示。
- **DeployTarget**屬性會識別您想要在建立專案之後叫用的目標。 在此情況下，**封裝**目標會將專案輸出建立成可部署的 web 封裝。

> [!NOTE]
> **封裝**目標會叫用 Web 發佈管線（WPP），以提供 MSBuild 和 Web Deploy 之間的整合。 如果您想要查看 WPP 提供的內建目標，請查看% PROGRAMFILES （x86）% \ MSBuild\Microsoft\VisualStudio\v10.0\Web 資料夾中的*web.config*檔案。

### <a name="the-gatherpackagesforpublishing-target"></a>GatherPackagesForPublishing 目標

如果您研究**GatherPackagesForPublishing**目標，您會發現它實際上不會包含任何工作。 相反地，它包含定義三個動態專案的單一專案群組。

[!code-xml[Main](understanding-the-build-process/samples/sample9.xml)]

這些專案會參考執行**BuildProjects**目標時所建立的部署套件。 您無法在專案檔中以靜態方式定義這些專案，因為在執行**BuildProjects**目標之前，專案所參考的檔案不存在。 而是必須在目標中動態定義專案，直到執行**BuildProjects**目標之後才會叫用。

專案不會在此目標&#x2014;中使用。此目標只會建立專案，以及與每個專案值相關聯的中繼資料。 一旦處理這些元素之後， **PublishPackages**專案將會包含兩個值： *ContactManager*的路徑，以及*ContactManager*檔案的路徑，而這個檔案則是部署 .cmd 檔案。 Web Deploy 會將這些檔案建立為每個專案之 web 封裝的一部分，而且這些檔案必須在目的地伺服器上叫用，才能部署封裝。 如果您開啟其中一個檔案，基本上會看到包含各種組建特定參數值的 Msdeploy.exe 命令。

**DbPublishPackages**專案會包含單一值，也就是*deploymanifest*檔案的路徑。

> [!NOTE]
> 當您建立資料庫專案時，會產生 deploymanifest 檔案，而且它會使用與 MSBuild 專案檔相同的架構。 其中包含部署資料庫所需的所有資訊，包括資料庫架構（.dbschema）的位置，以及任何預先部署和部署後腳本的詳細資料。 如需詳細資訊，請參閱[資料庫組建和部署的總覽](https://msdn.microsoft.com/library/aa833165.aspx)。

您將進一步瞭解如何建立部署封裝和資料庫部署資訊清單，以及如何在[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)和[部署資料庫專案](deploying-database-projects.md)時使用。

### <a name="the-publishdbpackages-target"></a>PublishDbPackages 目標

簡單地說， **PublishDbPackages**目標會叫用 VSDBCMD 公用程式，將**ContactManager**資料庫部署到目標環境。 設定資料庫部署牽涉到許多決策和細微之處，而您將在[部署資料庫專案](deploying-database-projects.md)和[自訂多個環境的資料庫部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)中深入瞭解這方面的資訊。 在本主題中，我們將著重于此目標實際運作的方式。

首先，請注意開頭標記包含**輸出**屬性。

[!code-xml[Main](understanding-the-build-process/samples/sample10.xml)]

這是*目標批次處理*的範例。 在 MSBuild 專案檔中，批次處理是一種反覆運算集合的技巧。 **輸出**屬性（ **"% （DbPublishPackages. Identity）"）** 的值是指**DbPublishPackages**專案清單的**識別**中繼資料屬性。 此標記法 * output *=% * * * （ItemList. ItemMetadataName）* 會轉譯為：

- 將**DbPublishPackages**中的專案分割成包含相同身分**識別**中繼資料值的專案批次。
- 針對每個批次執行一次目標。

> [!NOTE]
> 身分**識別**是在建立時指派給每個專案的其中一個[內建中繼資料值](https://msdn.microsoft.com/library/ms164313.aspx)。 它會參考**item**元素&#x2014;中的**Include**屬性值，也就是專案的路徑和檔案名。

在此情況下，因為絕對不能有一個以上的專案具有相同的路徑和檔案名，所以我們基本上是使用一個批次大小。 目標會針對每個資料庫封裝執行一次。

您可以在 **\_Cmd**屬性中看到類似的標記法，它會使用適當的參數建立 VSDBCMD 命令。

[!code-xml[Main](understanding-the-build-process/samples/sample11.xml)]

在此情況下， **% （DbPublishPackages. DatabaseConnectionString）** 、 **% （DbPublishPackages. TargetDatabase）** 和 **% （DbPublishPackages. FullPath）** 都會參考**DbPublishPackages**專案集合的中繼資料值。 **Exec**工作會使用 **\_Cmd**屬性，它會叫用命令。

[!code-xml[Main](understanding-the-build-process/samples/sample12.xml)]

由於此標記法的結果， **Exec**工作會根據**DatabaseConnectionString**、 **TargetDatabase**和**FullPath**中繼資料值的唯一組合來建立批次，而工作會針對每個批次執行一次。 這是工作*批次處理*的範例。 不過，由於目標層級批次處理已經將專案集合分割成單一專案批次，因此**Exec**工作將會執行一次，而且只會針對目標的每個反覆運算執行一次。 換句話說，此工作會針對方案中的每個資料庫封裝，叫用一次 VSDBCMD 公用程式。

> [!NOTE]
> 如需有關目標和工作批次處理的詳細資訊，請參閱 MSBuild[批次處理](https://msdn.microsoft.com/library/ms171473.aspx)、[目標批次處理中的專案中繼資料](https://msdn.microsoft.com/library/ms228229.aspx)，以及工作[批次處理中的專案中繼資料](https://msdn.microsoft.com/library/ms171474.aspx)。

### <a name="the-publishwebpackages-target"></a>PublishWebPackages 目標

此時，您已叫用**BuildProjects**目標，它會針對範例方案中的每個專案產生 web 部署套件。 隨附的每個套件都是一個*部署 .cmd*檔案，其中包含將封裝部署至目標環境所需的 msdeploy.exe 命令，以及一個*SetParameters*檔案，它會指定目標環境的必要詳細資料。 您也已叫用**GatherPackagesForPublishing**目標，它會產生包含您感興趣之*部署 .cmd*檔案的專案集合。 基本上， **PublishWebPackages**目標會執行下列功能：

- 它會操作每個封裝的*SetParameters* ，以包含目標環境的正確詳細資料（使用**XmlPoke**工作）。
- 它會使用適當的參數，叫用每個封裝的*deploy .cmd*檔案。

就像**PublishDbPackages**目標一樣， **PublishWebPackages**目標會使用目標批次處理，確保目標會針對每個 web 封裝執行一次。

[!code-xml[Main](understanding-the-build-process/samples/sample13.xml)]

在目標中， **Exec**工作是用來執行每個 web 封裝的*deploy .cmd*檔案。

[!code-xml[Main](understanding-the-build-process/samples/sample14.xml)]

如需設定 web 封裝部署的詳細資訊，請參閱[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)。

## <a name="conclusion"></a>結論

本主題提供了逐步解說，說明如何使用分割專案檔來控制從開始到完成的 Contact Manager 範例解決方案的組建和部署流程。 使用這種方法可讓您在單一、可重複執行的步驟中執行複雜的企業規模部署，只要執行環境特定的命令檔即可。

## <a name="further-reading"></a>進一步閱讀

如需更深入的專案檔和 WPP 簡介，請參閱[Microsoft Build Engine 內：使用 MSBuild 和 Team Foundation Build](http://amzn.com/0735645248) By Sayed Ibrahim Hashimi 和 William BARTHOLOMEW，ISBN：978-0-7356-4524-0。

> [!div class="step-by-step"]
> [上一頁](understanding-the-project-file.md)
> [下一頁](building-and-packaging-web-application-projects.md)
