---
uid: web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
title: 自訂多個環境的資料庫部署 |Microsoft Docs
author: jrjlee
description: 本主題描述如何在部署過程中，將資料庫的屬性量身打造為特定的目標環境。 注意：本主題假設 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a172979a-1318-4318-a9c6-4f9560d26267
msc.legacyurl: /web-forms/overview/deployment/advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments
msc.type: authoredcontent
ms.openlocfilehash: 8ae8cb1a322afb95c5d2e8d5e73c7825c7b2fe5a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78604024"
---
# <a name="customizing-database-deployments-for-multiple-environments"></a>自訂多個環境的資料庫部署

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何在部署過程中，將資料庫的屬性量身打造為特定的目標環境。
> 
> > [!NOTE]
> > 本主題假設您正在使用 Msbuild.exe 和 VSDBCMD 部署 Visual Studio 2010 資料庫專案。 如需如何選擇這種方法的詳細資訊，請參閱[企業中的 Web 部署](../web-deployment-in-the-enterprise/web-deployment-in-the-enterprise.md)和[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)。
> 
> 
> 當您將資料庫專案部署至多個目的地時，您通常會想要自訂每個目標環境的資料庫部署屬性。 例如，在測試環境中，您通常會在每個部署上重新建立資料庫，而在預備或生產環境中，您很可能會進行累加式更新以保留您的資料。
> 
> 在 Visual Studio 2010 資料庫專案中，部署設定會包含在部署設定（. sqldeployment）檔案中。 本主題將說明如何建立環境專屬的部署設定檔，並指定您想要做為 VSDBCMD 參數使用的檔案。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager 解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)&#x2014;的範例解決方案，來代表具有實際複雜度層級的 web 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案&#x2014;檔所控制，其中包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="task-overview"></a>工作總覽

本主題假設：

- 如[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述，您可以使用分割專案檔案方法來部署解決方案。
- 您可以從專案檔呼叫 VSDBCMD 來部署資料庫專案，如[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式中所述。

若要建立支援在目標環境之間改變資料庫部署屬性的部署系統，您必須：

- 為每個目標環境建立部署設定（. sqldeployment）檔案。
- 建立 VSDBCMD 命令，將部署設定檔指定為命令列參數。
- 參數化 Microsoft Build Engine （MSBuild）專案檔中的 VSDBCMD 命令，讓 VSDBCMD 選項適用于目標環境。

本主題將說明如何執行上述每個程式。

## <a name="creating-environment-specific-deployment-configuration-files"></a>建立環境特定的部署設定檔

根據預設，資料庫專案會包含名為*sqldeployment*的單一部署設定檔。 如果您在 Visual Studio 2010 中開啟此檔案，您會看到可供您使用的不同部署選項：

- **部署比較定序**。 這可讓您選擇是否要使用專案的資料庫定序（*來源*定序）或目的地伺服器的資料庫定序（*目標*定序）。 在大部分情況下，當您部署到開發或測試環境時，您會想要使用來源定序。 當您部署至預備或生產環境時，您通常會想要將目標定序保持不變，以避免發生任何互通性問題。
- **部署資料庫屬性**。 這可讓您選擇是否要套用資料庫屬性，如*sqlsettings*檔案中所定義。 當您第一次部署資料庫時，您應該部署資料庫屬性。 如果您要更新現有的資料庫，屬性應該已準備就緒，您應該不需要再次部署它們。
- **一律重新建立資料庫**。 這可讓您選擇是否要在每次部署時重新建立目標資料庫，或進行累加式變更，使目標資料庫與您的架構保持在最新狀態。 如果您重新建立資料庫，將會遺失現有資料庫中的任何資料。 因此，您通常應該將此設定為**false** ，以部署至預備或生產環境。
- **如果可能發生資料遺失，則封鎖累加式部署**。 這可讓您選擇如果資料庫架構的變更會造成資料遺失，是否應該停止部署。 您通常會將此**值**設定為 true，以部署到生產環境，讓您有機會介入和保護任何重要資料。 如果您已將 [**永遠重新建立資料庫**] 設定為 [ **false**]，則此設定不會有任何作用。
- **以單一使用者模式執行部署**。 在開發或測試環境中，這通常不是問題。 不過，您通常應該將此設定為**true** ，以部署至預備或生產環境。 這可防止使用者在部署進行時對資料庫進行變更。
- **部署前備份資料庫**。 當您部署到生產環境時，通常會將此設定為**true** ，以預防資料遺失。 當您部署至預備環境時，如果您的臨時資料庫包含大量資料，您可能也會想要將它設定為**true** 。
- **針對目標資料庫中但不在資料庫專案中的物件產生 DROP 語句**。 在大部分情況下，這是對資料庫進行累加式變更時不可或缺的一部分。 如果您已將 [**永遠重新建立資料庫**] 設定為 [ **false**]，則此設定不會有任何作用。
- **請勿使用 ALTER ASSEMBLY 語句來更新 CLR 類型**。 此設定會決定 SQL Server 如何將 common language runtime （CLR）類型更新為較新的元件版本。 在大部分的情況下，這應該設定為**false** 。

下表顯示不同目的地環境的一般部署設定。 不過，視您的確切需求而定，您的設定可能會有所不同。

|  | 開發人員/測試 | 預備/整合 | 生產環境 |
| --- | --- | --- | --- |
| **部署比較定序** | 原始程式檔 | Target | Target |
| **部署資料庫屬性** | True | 第一次只有 | 第一次只有 |
| **一律重新建立資料庫** | True | False | False |
| **如果可能發生資料遺失，則封鎖增量部署** | False | 可能 | True |
| **以單一使用者模式執行部署腳本** | False | True | True |
| **部署前備份資料庫** | False | 可能 | True |
| **針對目標資料庫中但不在資料庫專案中的物件產生 DROP 語句** | False | True | True |
| **請勿使用 ALTER ASSEMBLY 語句來更新 CLR 類型** | False | False | False |

> [!NOTE]
> 如需有關資料庫部署屬性和環境考慮的詳細資訊，請參閱[資料庫專案設定總覽](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)、[如何：設定部署詳細資料的屬性](https://msdn.microsoft.com/library/dd172125.aspx)、[建立資料庫並部署至隔離開發環境](https://msdn.microsoft.com/library/dd193409.aspx)，以及[建立資料庫並將其部署至預備或生產環境](https://msdn.microsoft.com/library/dd193413.aspx)。

若要支援將資料庫專案部署至多個目的地，您應該為每個目標環境建立部署設定檔。

**建立環境特定的設定檔**

1. 在 Visual Studio 2010 的 [**方案總管**] 視窗中，以滑鼠右鍵按一下您的資料庫專案，然後按一下 [**屬性**]。
2. 在 [資料庫專案屬性] 頁面的 [**部署**] 索引標籤上，按一下 [**部署設定檔**] 資料列中的 [**新增**]。

    ![](customizing-database-deployments-for-multiple-environments/_static/image1.png)
3. 在 [**新增部署設定檔**] 對話方塊中，為檔案提供有意義的名稱（例如， **TestEnvironment. sqldeployment**），然後按一下 [**儲存**]。
4. 在 *[Filename] * * * sqldeployment** 頁面上，設定部署內容以符合目的地環境的需求，然後儲存檔案。

    ![](customizing-database-deployments-for-multiple-environments/_static/image2.png)
5. 請注意，新的檔案會加入至您資料庫專案的 [屬性] 資料夾中。

    ![](customizing-database-deployments-for-multiple-environments/_static/image3.png)

## <a name="specifying-the-deployment-configuration-file-in-vsdbcmd"></a>在 VSDBCMD 中指定部署設定檔

當您使用 Visual Studio 2010 內的解決方案設定（例如 Debug 和 Release）時，您可以將部署設定檔與每個設定產生關聯。 當您建立特定設定時，組建程式會產生特定設定的部署資訊清單檔案，該檔案會指向設定特定的部署設定檔。 不過，這些教學課程中所述部署方法的其中一個主要目標是讓使用者能夠控制部署流程，而不需要使用 Visual Studio 2010 和解決方案設定。 在此方法中，不論目標部署環境為何，解決方案設定都相同。 若要將您的資料庫部署量身打造到特定的目的地環境，您可以使用 VSDBCMD 命令列選項來指定您的部署設定檔。

若要在 VSDBCMD 中指定部署設定檔，請使用**p：/DeploymentConfigurationFile**參數，並提供檔案的完整路徑。 這會覆寫部署資訊清單所識別的部署設定檔。 例如，您可以使用這個 VSDBCMD 命令，將**ContactManager**資料庫部署到測試環境：

[!code-console[Main](customizing-database-deployments-for-multiple-environments/samples/sample1.cmd)]

> [!NOTE]
> 請注意，建立程式會在將檔案複製到輸出目錄時，重新命名您的 sqldeployment 檔案。

如果您在預先部署或部署後的 SQL 腳本中使用 SQL 命令變數，您可以使用類似的方法，將環境特定的 sqlcmdvars 檔案與您的部署產生關聯。 在此情況下，您會使用**p：/SqlCommandVariablesFile**參數來識別您的 sqlcmdvars 檔案。

## <a name="running-the-vsdbcmd-command-from-an-msbuild-project-file"></a>從 MSBuild 專案檔執行 VSDBCMD 命令

您可以使用 MSBuild 目標中的**Exec**工作，從 msbuild 專案檔叫用 VSDBCMD 命令。 最簡單的形式如下所示：

[!code-xml[Main](customizing-database-deployments-for-multiple-environments/samples/sample2.xml)]

- 實際上，若要讓您的專案檔易於閱讀和重複使用，您會想要建立屬性來儲存各種命令列參數。 這可讓使用者更輕鬆地在環境特定的專案檔中提供屬性值，或從 MSBuild 命令列覆寫預設值。 如果您使用[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔中所述的分割專案檔方法，您應該據以將組建指示和屬性分成兩個檔案：
- 環境特定的設定（例如部署設定檔案名、資料庫連接字串和目標資料庫名稱）應該會在環境特定的專案檔中。
- 執行 VSDBCMD 命令的 MSBuild 目標，以及任何通用屬性（例如 VSDBCMD 可執行檔的位置），都應該放在通用專案檔中。

您也應該先確定您已建立資料庫專案，再叫用 VSDBCMD，以便建立 deploymanifest 檔案並備妥可供使用。 您可以在[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式主題中看到這種方法的完整範例，該程式會逐步引導您完成[Contact Manager 範例解決方案](../web-deployment-in-the-enterprise/the-contact-manager-solution.md)中的專案檔案。

## <a name="conclusion"></a>結論

本主題說明當您使用 MSBuild 和 VSDBCMD 部署資料庫專案時，如何將資料庫屬性量身打造至不同的目的地環境。 當您需要將資料庫專案部署為較大型企業級解決方案的一部分時，這個方法很有用。 這些解決方案通常會部署到多個目的地，例如沙箱開發或測試環境、預備或整合平臺，以及生產或即時環境。 這些目標環境中的每個通常都需要一組唯一的資料庫部署屬性。

## <a name="further-reading"></a>進一步閱讀

如需使用 VSDBCMD 部署資料庫專案的詳細資訊，請參閱[部署資料庫專案](../web-deployment-in-the-enterprise/deploying-database-projects.md)。 如需使用自訂 MSBuild 專案檔控制部署程式的詳細資訊，請參閱[瞭解專案](../web-deployment-in-the-enterprise/understanding-the-project-file.md)檔和[瞭解組建](../web-deployment-in-the-enterprise/understanding-the-build-process.md)程式。

MSDN 上的這些文章提供有關資料庫部署的一般指引：

- [資料庫專案設定總覽](https://msdn.microsoft.com/library/aa833291(v=VS.100).aspx)
- [如何：設定部署詳細資料的屬性](https://msdn.microsoft.com/library/dd172125.aspx)
- [建立資料庫並將其部署至隔離開發環境](https://msdn.microsoft.com/library/dd193409.aspx)
- [建立資料庫並將其部署至預備或生產環境](https://msdn.microsoft.com/library/dd193413.aspx)

> [!div class="step-by-step"]
> [上一頁](performing-a-what-if-deployment.md)
> [下一頁](deploying-database-role-memberships-to-test-environments.md)
