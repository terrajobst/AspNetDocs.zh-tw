---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
title: 部署資料庫專案 |Microsoft Docs
author: jrjlee
description: 注意：在許多企業部署案例中，您都需要能夠將累加式更新發佈到已部署的資料庫。 替代方案是重新建立 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: 832f226a-1aa3-4093-8c29-ce4196793259
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-database-projects
msc.type: authoredcontent
ms.openlocfilehash: 221808758492aedb8e8329364e511df28fd11105
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634264"
---
# <a name="deploying-database-projects"></a>部署資料庫專案

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> [!NOTE]
> 在許多企業部署案例中，您都需要能夠將累加式更新發佈到已部署的資料庫。 替代方案是在每個部署上重新建立資料庫，這表示您會遺失現有資料庫中的任何資料。 當您使用 Visual Studio 2010 時，使用 VSDBCMD 是累加式資料庫發佈的建議方法。 不過，下一版的 Visual Studio 和 Web 發行管線（WPP）將包含可直接支援累加式發行的工具。

如果您在 Visual Studio 2010 中開啟 Contact Manager 範例方案，您會看到資料庫專案包含包含四個檔案的 [Properties] 資料夾。

![](deploying-database-projects/_static/image1.png)

與專案檔（在此案例中為*ContactManager* ），這些檔案會控制組建和部署程式的各個層面：

- *Sqlcmdvars*檔案會提供部署專案時使用之任何 SQLCMD 變數的值。 每個解決方案設定（例如，debug 和 release）都可以指定不同的 sqlcmdvars 檔案。
- *Sqldeployment*檔案提供部署專屬的設定，例如是否要使用專案中所定義的定序或目的地伺服器的定序、是否每次重新建立目的地資料庫，或只是修改現有的資料庫使其成為最新狀態等等。 每個解決方案設定都可以指定不同的 sqldeployment 檔案。
- *.Sqlpermissions*檔案是一個 XML 檔，您可以用它來定義您想要加入至目標資料庫的任何許可權。 所有解決方案設定都會共用相同的 .sqlpermissions 檔案。
- *Sqlsettings*檔案會指定要在建立資料庫時使用的資料庫層級屬性，例如要使用的定序、比較運算子的行為等等。 所有解決方案設定都會共用相同的 sqlsettings 檔案。

值得一提的是，在 Visual Studio 中開啟這些檔案，並讓自己熟悉內容。

當您建立資料庫專案時，組建進程會建立兩個檔案：

- *資料庫架構*（.dbschema 檔案）。 這會描述您想要以 XML 格式建立之資料庫的架構。
- *部署資訊清單*（deploymanifest 檔案）。 其中包含建立及部署資料庫所需的所有資訊。 它會參考 .dbschema 檔案以及其他資源，例如部署指示（sqldeployment 檔案），以及任何預先部署或部署後的 SQL 腳本。

這會顯示這些資源之間的關聯性：

![](deploying-database-projects/_static/image2.png)

如您所見，sqlsettings 檔案和 .sqlpermissions 檔案是組建進程的輸入。 除了資料庫專案檔，這些檔案也會用來建立資料庫架構檔案。 Sqldeployment 檔案和 sqlcmdvars 檔案會原封不動地通過組建進程。 部署資訊清單會指出資料庫架構的位置、sqldeployment 檔案、sqlcmdvars 檔案，以及任何預先部署或部署後 SQL 腳本。

## <a name="why-use-vsdbcmd-to-deploy-a-database-project"></a>為何要使用 VSDBCMD 來部署資料庫專案？

有各種不同的方法可以部署資料庫專案。 不過，並非全部都適用于在企業環境中將資料庫專案部署至遠端伺服器。 從資料庫專案部署考慮您想要的結果。 在企業部署案例中，您可能會想要：

- 從遠端位置部署資料庫專案的能力。
- 對現有資料庫進行累加式更新的功能。
- 包含預先部署腳本或部署後腳本的功能。
- 將部署量身打造到多個目的地環境的能力。
- 能夠將資料庫專案部署為較大型、通常已編寫腳本的單一步驟解決方案部署的一部分。

您可以使用三種主要方法來部署資料庫專案：

- 您可以在 Visual Studio 2010 中，將部署功能與資料庫專案類型搭配使用。 當您在 Visual Studio 2010 中建立及部署資料庫專案時，部署程式會使用部署資訊清單來產生組建設定特有的 SQL 部署檔案。 這會建立資料庫（如果尚未存在），或對資料庫進行任何必要的變更（如果已經存在）。 您可以使用 SQLCMD 在目的地伺服器上執行這個檔案，也可以設定 Visual Studio 來建立和執行檔案。 這種方法的缺點是您只能控制部署設定的限制。 您通常可能也需要修改 SQL 部署檔案，以提供環境特定變數值。 您只能從已安裝 Visual Studio 2010 的電腦使用此方法，而開發人員必須知道並提供所有目的地環境的連接字串和認證。
- 您可以使用 Internet Information Services （IIS） Web 部署工具（Web Deploy），將[資料庫部署為 Web 應用程式專案的一部分](https://msdn.microsoft.com/library/dd465343.aspx)。 不過，如果您想要部署資料庫專案，而不只是在目的地伺服器上複寫現有的本機資料庫，這個方法就會變得更複雜。 您可以設定 Web Deploy 來執行資料庫專案所產生的 SQL 部署腳本，但為了這麼做，您必須為 Web 應用程式專案建立自訂的 WPP 目標檔案。 這會在部署程式中增加相當大的複雜度。 此外，Web Deploy 不會直接支援現有資料庫的累加式更新。 如需這種方法的詳細資訊，請參閱將[Web 發佈管線擴充至封裝資料庫專案部署的 SQL](https://go.microsoft.com/?linkid=9805121)檔案。
- 您可以使用 VSDBCMD 公用程式來部署資料庫，方法是使用資料庫架構或部署資訊清單。 您可以從 MSBuild 目標呼叫 VSDBCMD，這可讓您在較大的腳本式部署程式中發佈資料庫。 您可以從 VSDBCMD 命令覆寫 sqlcmdvars 檔案和許多其他資料庫屬性中的變數，這可讓您針對不同的環境自訂部署，而不需要建立多個組建設定。 VSDBCMD 提供差異化功能，這表示它只會進行必要的變更，使目的地資料庫與您的資料庫架構一致。 VSDBCMD 也提供廣泛的命令列選項，可讓您更精細地控制部署流程。

在此總覽中，您可以看到使用 VSDBCMD 搭配 MSBuild 是最適合一般企業部署案例的方法：

|  | Visual Studio 2010 | Web Deploy 2.0 | VSDBCMD .exe |
| --- | --- | --- | --- |
| 支援遠端部署？ | [是] | [是] | [是] |
| 支援累加式更新？ | [是] | 否 | [是] |
| 支援前置/部署後腳本？ | [是] | [是] | [是] |
| 支援多環境部署嗎？ | 有限 | 有限 | [是] |
| 支援腳本式部署？ | 有限 | [是] | [是] |

本主題的其餘部分將說明如何使用 VSDBCMD 搭配 MSBuild 來部署資料庫專案。

## <a name="understanding-the-deployment-process"></a>瞭解部署程式

VSDBCMD 公用程式可讓您使用資料庫架構（.dbschema 檔案）或部署資訊清單（deploymanifest 檔案）來部署資料庫。 在實務上，您幾乎一律會使用部署資訊清單，因為部署資訊清單可讓您為各種部署屬性提供預設值，並識別您想要執行的任何預先部署或部署後 SQL 腳本。 例如，此 VSDBCMD 命令是用來將**ContactManager**資料庫部署到測試環境中的資料庫伺服器：

[!code-console[Main](deploying-database-projects/samples/sample1.cmd)]

在此情況下：

- **/A** （或 **/Action**）參數會指定您想要 VSDBCMD 執行的動作。 您可以將此設定為 [匯**入**] 或 [**部署**]。 [匯**入**] 選項是用來從現有的資料庫產生 .dbschema 檔案，而 [**部署**] 選項是用來將 .dbschema 檔案部署到目標資料庫。
- **/Manifest** （或 **/ManifestFile**）交換器會識別您想要部署的 deploymanifest 檔案。 如果您想要改為使用 .dbschema 檔案，請使用 **/model** （或 **/ModelFile**）參數。
- **/Cs** （或 **/ConnectionString**）參數會提供目標資料庫伺服器的連接字串。 請注意，這不會包含連接到伺服器&#x2014;以建立資料庫所需的資料庫 VSDBCMD 名稱。它不需要連接至個別的資料庫。 如果您的 deploymanifest 檔案包含連接字串，您可以省略此參數。 如果您仍然使用參數，參數值會覆寫 deploymanifest 值。
- <strong>/P： TargetDatabase</strong>屬性會提供您想要在建立時指派給目標資料庫的名稱。 這會覆寫 deploymanifest 檔案中<strong>TargetDatabase</strong>屬性的值。 您可以使用<strong>/p：</strong> <em>[property name]</em>語法來設定各種不同的部署屬性，並覆寫 sqlcmdvars 檔案中所宣告的任何 SQLCMD 變數。
- **/Dd +** （或 **/DeployToDatabase +** ）參數表示您想要建立部署，並將其部署至目標環境。 如果您指定 **/dd-** ，或省略參數，VSDBCMD 會產生部署腳本，但不會將它部署至目標環境。 此參數通常是混淆的來源，並會在下一節中更詳細地說明。
- **/Script** （或 **/DeploymentScriptFile**）參數會指定您要產生部署腳本的位置。 這個值不會影響部署進程。

如需 VSDBCMD 的詳細資訊，請參閱[VSDBCMD 的命令列參考。EXE （部署和架構匯入）](https://msdn.microsoft.com/library/dd193283.aspx)和[如何：使用 VSDBCMD 從命令提示字元準備要部署的資料庫。EXE](https://msdn.microsoft.com/library/dd193258.aspx)。

如需如何從 MSBuild 專案檔使用 VSDBCMD 的範例，請參閱[瞭解組建處理](understanding-the-build-process.md)。 如需如何為多個環境設定資料庫部署設定的範例，請參閱[自訂多個環境的資料庫](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)部署。

## <a name="understanding-the-deploytodatabase-switch"></a>瞭解 DeployToDatabase 交換器

**/Dd**或 **/DeployToDatabase**參數的行為取決於您是使用 VSDBCMD 搭配 .dbschema 檔案或 deploymanifest 檔案。 如果您使用的是 .dbschema 檔案，其行為相當簡單：

- 如果您指定 **/dd +** 或 **/dd**，VSDBCMD 會產生部署腳本並部署資料庫。
- 如果您指定 **/dd-** 或省略參數，VSDBCMD 只會產生部署腳本。

如果您使用的是 deploymanifest 檔案，則行為會變得複雜許多。 這是因為 deploymanifest 檔案包含屬性名稱**DeployToDatabase** ，這也會決定是否已部署資料庫。

[!code-xml[Main](deploying-database-projects/samples/sample2.xml)]

這個屬性的值是根據資料庫專案的屬性來設定。 如果您將 [**部署] 動作**設定為 [**建立部署腳本（.sql）** ]，此值將會是**False**。 如果您將 [**部署] 動作**設定為**建立部署腳本（.sql），並部署到資料庫**，則值將為**True**。

> [!NOTE]
> 這些設定會與特定的組建設定和平臺相關聯。 例如，如果您設定了 [ **Debug** ] 設定，然後使用 [**發行**] 設定發佈，將不會使用您的設定。

![](deploying-database-projects/_static/image3.png)

> [!NOTE]
> 在此案例中，[**部署] 動作**應一律設定為 [**建立部署腳本（.sql）** ]，因為您不想要 Visual Studio 2010 來部署您的資料庫。 換句話說， **DeployToDatabase**屬性應該一律為**False**。

當指定了**DeployToDatabase**屬性時，如果屬性值為**false**，則 **/dd**參數只會覆寫屬性：

- 如果**DeployToDatabase**屬性為**False**，而且您指定了 **/dd +** 或 **/Dd**，則 VSDBCMD 會覆寫**DeployToDatabase**屬性並部署資料庫。
- 如果**DeployToDatabase**屬性為**False**，而且您指定 **/DD-** 或省略參數，VSDBCMD 就不會部署資料庫。
- 如果**DeployToDatabase**屬性為**True**，則 VSDBCMD 會忽略參數並部署資料庫。
- 無論您是否也要部署資料庫，都是在每個案例中產生部署腳本。

## <a name="conclusion"></a>結論

本主題提供 Visual Studio 2010 中資料庫專案的組建和部署程式總覽。 同時也會說明如何使用 VSDBCMD 搭配 MSBuild 來支援企業級資料庫部署。

如需如何在實務中運作的詳細資訊，請參閱[自訂多個環境的資料庫部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)。

## <a name="further-reading"></a>進一步閱讀

如需如何為每個環境建立個別的部署設定檔，以自訂資料庫部署的詳細資訊，請參閱[自訂多個環境的資料庫部署](../advanced-enterprise-web-deployment/customizing-database-deployments-for-multiple-environments.md)。 如需有關如何藉由執行部署後腳本來設定資料庫角色成員資格的指引，請參閱將[資料庫角色成員資格部署到測試環境](../advanced-enterprise-web-deployment/deploying-database-role-memberships-to-test-environments.md)。 如需管理成員資格資料庫所強加之一些獨特挑戰的指引，請參閱[將成員資格資料庫部署到企業環境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)。

MSDN 上的這些主題會針對 Visual Studio 資料庫專案和資料庫部署程式，提供更廣泛的指引和背景資訊：

- [Visual Studio 2010 SQL Server 資料庫專案](https://msdn.microsoft.com/library/ff678491.aspx)
- [管理資料庫變更](https://msdn.microsoft.com/library/aa833404.aspx)
- [如何：使用 VSDBCMD 從命令提示字元準備要部署的資料庫。CONVERT.EXE](https://msdn.microsoft.com/library/dd193258.aspx)
- [資料庫組建和部署總覽](https://msdn.microsoft.com/library/aa833165.aspx)

> [!div class="step-by-step"]
> [上一頁](deploying-web-packages.md)
> [下一頁](creating-and-running-a-deployment-command-file.md)
