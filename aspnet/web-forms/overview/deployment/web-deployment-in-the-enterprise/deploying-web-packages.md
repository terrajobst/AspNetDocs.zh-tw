---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
title: 部署 Web 套件 |Microsoft Docs
author: jrjlee
description: 本主題描述如何使用 [Internet Information Services （IIS） Web 部署工具（Web ...]，將 web 部署封裝發佈到遠端伺服器。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: a5c5eed2-8683-40a5-a2e1-35c9f8d17c29
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/deploying-web-packages
msc.type: authoredcontent
ms.openlocfilehash: 91b99e6e250342851aea6860164b6f6af54818d1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78575947"
---
# <a name="deploying-web-packages"></a>部署 Web 套件

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題說明如何使用 Internet Information Services （IIS） Web 部署工具（Web Deploy）2.0，將 web 部署套件發行至遠端伺服器。
> 
> 有兩種主要方式可將 web 封裝部署到遠端伺服器：
> 
> - 您可以直接使用 Msdeploy.exe 命令列公用程式。
> - 您可以執行組建程式所產生的 *[專案名稱]. deploy .cmd*檔案。
> 
> 不論您使用哪種方法，最終結果都相同。 基本上，所有的 *.deploy .cmd*檔案都是以一些預先決定的值執行 msdeploy.exe，因此您不需要提供太多資訊，就能部署封裝。 這可簡化部署程式。 另一方面，使用 Msdeploy.exe 直接提供您更大的彈性，而不是確切部署套件的方式。
> 
> 您所使用的方法將取決於各種因素，包括您在部署程式上需要多少控制，以及您的目標是 Web Deploy 遠端代理程式服務還是 Web Deploy 處理常式。 本主題說明如何使用每種方法，並識別每個方法的適當時機。
> 
> 本主題中的工作和逐步解說假設：
> 
> - 您已建立並封裝您的 web 應用程式，如[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)中所述。
> - 您已修改*SetParameters* ，為您的目標環境提供正確的參數值，如設定[Web 封裝部署的參數](configuring-parameters-for-web-package-deployment.md)中所述。

執行 [*專案名稱*] *。部署 .cmd*檔案是部署 web 封裝最簡單的方式。 特別是，使用 *.deploy*檔案比直接使用 msdeploy.exe 提供下列優點：

- 您不需要指定 web 部署套件&#x2014;的位置 *。 .cmd*檔案已知道其所在位置。
- 您不需要指定*SetParameters* &#x2014;的位置。 *.cmd*檔案已知道其所在位置。
- 您不需要指定來源和目的地 Msdeploy.exe 提供者&#x2014; *。部署 .cmd*檔案已經知道要使用的值。
- 您不需要指定 Msdeploy.exe 作業設定&#x2014; *。部署 .cmd*檔案會自動將常用的值新增至 msdeploy.exe 命令。

在使用 *.deploy*檔案來部署 web 封裝之前，您應該確定：

- *Deploy .cmd*檔案，也就是 [*project name*]。*SetParameters .xml*檔案和 web 封裝（[*專案名稱*]。*zip*）位於相同的資料夾中。
- Web Deploy （Msdeploy.exe）安裝在執行 *. Deploy .cmd*檔案的電腦上。

*Deploy .cmd*檔案支援各種命令列選項。 當您從命令提示字元執行檔案時，這是基本語法：

[!code-console[Main](deploying-web-packages/samples/sample1.cmd)]

您必須指定 **/t**旗標或 **/y**旗標，以指出您想要分別執行試用或即時部署（請勿在相同的命令中使用這兩個旗標）。 下表說明每個旗標的用途。

| 旗標 | 說明 |
| --- | --- |
| **一起** | 使用 **– whatif**旗標呼叫 msdeploy.exe，這表示試用版執行。 它不會部署封裝，而是會建立一份報告，說明部署套件時所發生的情況。 |
| **/Y** | 呼叫 Msdeploy.exe，但不含 **– whatif**旗標。 這會將封裝部署到本機電腦或指定的目的地伺服器。 |
| **/M** | 指定目的地伺服器名稱或服務 URL。 如需您可以在這裡提供之值的詳細資訊，請參閱本主題中的**端點考慮**一節。 如果您省略 **/m**旗標，封裝將會部署到本機電腦。 |
| **/A** | 指定 Msdeploy.exe 應用來執行部署的驗證類型。 可能的值為 [ **NTLM** ] 和 [**基本**]。 如果您省略 **/a**旗標，驗證類型會預設為**NTLM**以部署到 Web Deploy 遠端代理程式服務，以及部署至 Web Deploy 處理常式的**基本**。 |
| **/U** | 指定使用者名稱。 只有當您使用基本驗證時，才適用這種情況。 |
| **/P** | 指定密碼。 只有當您使用基本驗證時，才適用這種情況。 |
| **/L** | 指出應該將封裝部署到本機 IIS Express 實例。 |
| **/G** | 指定使用[tempAgent 提供者設定](https://technet.microsoft.com/library/ee517345(WS.10).aspx)來部署封裝。 如果您省略 **/g**旗標，此值會預設為**false**。 |

> [!NOTE]
> 每次組建程式建立 web 套件時，它也會建立名為 *[project name]. deploy-readme*的檔案，說明這些部署選項。

除了這些旗標之外，您還可以將 Web Deploy 作業設定指定為額外的 *。部署 .cmd*參數。 您指定的任何其他設定都只會傳遞至基礎的 Msdeploy.exe 命令。 如需這些設定的詳細資訊，請參閱[Web Deploy 作業設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。

假設您想要執行*deploy .cmd*檔案，將 ContactManager 部署至測試環境。 您的測試環境已設定為使用 Web Deploy 遠端代理程式服務，如[設定 Web Deploy 發佈的網頁伺服器（遠端代理程式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-remote-agent.md)中所述。 若要部署 web 應用程式，您需要完成接下來的步驟。

**若要使用 deploy .cmd 檔案部署 web 應用程式**

1. 建立和封裝 web 應用程式專案，如[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)中所述。
2. 修改*ContactManager* ，使其包含測試環境的正確參數值，如設定[Web 封裝部署的參數](configuring-parameters-for-web-package-deployment.md)中所述。
3. 開啟 [命令提示字元] 視窗，並流覽至*ContactManager*的位置。
4. 輸入此命令，然後按 Enter 鍵：

    [!code-console[Main](deploying-web-packages/samples/sample2.cmd)]

在這個範例中：

- **/Y**旗標表示您想要實際部署封裝，而不是執行試用版。
- **/M**旗標表示您想要將封裝部署到名為 TESTWEB1 的伺服器。 在這個值中，Msdeploy.exe 會嘗試將封裝部署到位於 http://TESTWEB1/MSDeployAgentService的 Web Deploy 遠端代理程式服務。
- **/A**旗標表示您想要使用 NTLM 驗證。 因此，您不需要指定使用者名稱和密碼。

若要說明如何使用 *.deploy*檔案簡化部署程式，請參閱當您執行*ContactManager*時所產生和執行的 msdeploy.exe 命令，方法是使用上面顯示的選項。

[!code-console[Main](deploying-web-packages/samples/sample3.cmd)]

如需使用*deploy .cmd*檔案來部署 web 封裝的詳細資訊，請參閱[如何：使用 Deploy 檔案安裝部署套件](https://msdn.microsoft.com/library/ff356104.aspx)。

## <a name="using-msdeployexe"></a>使用 Msdeploy.exe

雖然使用*deploy .cmd*檔案通常會簡化部署程式，但在某些情況下，最好直接使用 msdeploy.exe。 例如:

- 如果您想要以非系統管理員使用者的身分部署至 Web Deploy 處理常式，則無法使用*deploy .cmd*檔案。 這是因為 Web Deploy 2.0 中的錯誤，如**端點考慮**中所述。
- 如果您想要在不同位置的不同*SetParameters*之間手動切換，您可能會想要直接使用 msdeploy.exe。
- 如果您想要覆寫數個 Msdeploy.exe 命令列引數，您可能會想要直接使用 Msdeploy.exe。

當您使用 Msdeploy.exe 時，您必須提供三個重要的資訊片段：

- **– Source**參數，表示資料的來源位置。
- **-Dest**參數，指出資料的目的地。
- **–動詞**參數，[表示您想要執行](https://technet.microsoft.com/library/dd568989(WS.10).aspx)的作業。

Msdeploy.exe 依賴[Web Deploy 提供者](https://technet.microsoft.com/library/dd569040(WS.10).aspx)來處理來源和目的地資料。 Web Deploy 包含很多提供者，代表它可以&#x2014;使用的應用程式和資料來源範圍，例如，SQL Server 資料庫、IIS web 伺服器、憑證、全域組件快取（GAC）元件、各種不同的設定檔，以及許多其他類型的資料的提供者。 **– Source**參數和 **– dest**參數都必須指定提供者，格式為 **– source**： [*providerName*] = [*location*]。 當您將 web 套件部署到 IIS 網站時，應該使用下列值：

- **–來源**提供者一律是[package](https://technet.microsoft.com/library/dd569019(WS.10).aspx)。 例如:

    [!code-console[Main](deploying-web-packages/samples/sample4.cmd)]
- **– Dest**提供者一律是[自動](https://technet.microsoft.com/library/dd569016(WS.10).aspx)的。例如：

    [!code-console[Main](deploying-web-packages/samples/sample5.cmd)]
- **–動詞**一律會**同步**。

    [!code-console[Main](deploying-web-packages/samples/sample6.cmd)]

此外，您還需要指定各種其他[提供者特定的設定](https://technet.microsoft.com/library/dd569001(WS.10).aspx)和一般作業[設定](https://technet.microsoft.com/library/dd569089(WS.10).aspx)。 例如，假設您想要將 ContactManager 的 Mvc web 應用程式部署到預備環境。 部署會將目標設為 Web Deploy 處理常式，而且必須使用基本驗證。 若要部署 web 應用程式，您需要完成接下來的步驟。

**使用 Msdeploy.exe 部署 web 應用程式**

1. 建立和封裝 web 應用程式專案，如[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)中所述。
2. 修改*ContactManager*以包含預備環境的正確參數值，如設定[Web 封裝部署的參數](configuring-parameters-for-web-package-deployment.md)中所述。
3. 開啟 [命令提示字元] 視窗，並流覽至 Msdeploy.exe 的位置。 這通常位於%PROGRAMFILES%\IIS\Microsoft Web Deploy V2\msdeploy.exe。
4. 輸入此命令，然後按 Enter （忽略分行符號）：

    [!code-console[Main](deploying-web-packages/samples/sample7.cmd)]

在這個範例中：

- **– Source**參數會指定**封裝**提供者，並指出 web 封裝的位置。
- **– Dest**參數會指定**auto**提供者。 **ComputerName**設定會在目的地伺服器上提供 Web Deploy 處理常式的服務 URL。 **Authtype**設定指出您想要使用基本驗證，因此您必須提供使用者**名稱**和**密碼**。 最後， **includeAcls = "False"** 設定表示您不想要將來源 web 應用程式中檔案的存取控制清單（acl）複製到目的地伺服器。
- **– Verb： sync**引數指出您想要在目的地伺服器上複寫來源內容。
- **– DisableLink**引數表示您不想要在目的地伺服器上複寫應用程式集區、虛擬目錄設定或安全通訊端層（SSL）憑證。 如需詳細資訊，請參閱[Web Deploy 連結延伸](https://technet.microsoft.com/library/dd569028(WS.10).aspx)模組。
- **– SetParamFile**參數提供*SetParameters*的位置。
- **– AllowUntrusted**參數指出 Web Deploy 應該接受不是由受信任的憑證授權單位單位所發行的 SSL 憑證。 如果您要部署到 Web Deploy 處理常式，而且您已使用自我簽署憑證來保護服務 URL，您必須包含此參數。

## <a name="automating-web-package-deployment"></a>自動化 Web 套件部署

在許多企業案例中，您會想要將 web 套件部署為較大的單一步驟或自動化部署的一部分。 無論您是否選擇直接執行 *.deploy*檔案或使用 msdeploy.exe 來部署 web 套件，您都可以參數化命令，並從 Microsoft Build Engine （MSBuild）專案檔中的目標呼叫它們。

在 Contact Manager 範例解決方案中，查看*Publish*檔案中的**PublishWebPackages**目標。 這個目標會針對每個執行一次。部署名為**PublishPackages**的專案清單所識別的 *.cmd*檔案。 目標會使用屬性和專案中繼資料，為每個 *. 部署 .cmd*檔案建立一組完整的引數值，然後使用**Exec**工作來執行命令。

[!code-xml[Main](deploying-web-packages/samples/sample8.xml)]

> [!NOTE]
> 如需範例方案中的專案檔模型，以及一般自訂專案檔案的簡介，請參閱[瞭解專案](understanding-the-project-file.md)檔和[瞭解組建](understanding-the-build-process.md)程式。

## <a name="endpoint-considerations"></a>端點考慮

不論您是藉由執行 *.deploy*檔案或直接使用 msdeploy.exe 來部署 web 封裝，都必須為您的部署指定電腦名稱稱或服務端點。

如果目的地 web 伺服器已設定為使用 Web Deploy 遠端代理程式服務進行部署，您可以指定目標服務 URL 作為目的地。

[!code-console[Main](deploying-web-packages/samples/sample9.cmd)]

或者，您可以單獨指定伺服器名稱作為目的地，Web Deploy 將會推斷遠端代理程式服務 URL。

[!code-console[Main](deploying-web-packages/samples/sample10.cmd)]

如果目的地 web 伺服器已設定為使用 Web Deploy 處理常式進行部署，您必須指定 IIS Web 管理服務（WMSvc）的端點位址作為目的地。 根據預設，這會採用下列格式：

[!code-console[Main](deploying-web-packages/samples/sample11.cmd)]

您可以使用 *. deploy .cmd*檔案或 msdeploy.exe 直接將目標設為這些端點的任何一個。 不過，如果您想要以非系統管理員使用者的身分部署至 Web Deploy 處理常式（如[設定 Web Deploy 發佈的 Web 服務器（Web Deploy 處理常式）](../configuring-server-environments-for-web-deployment/configuring-a-web-server-for-web-deploy-publishing-web-deploy-handler.md)中所述，您需要將查詢字串新增至服務端點位址。

[!code-console[Main](deploying-web-packages/samples/sample12.cmd)]

這是因為非系統管理員的使用者沒有 IIS 的伺服器層級存取權;他或她只能存取特定的 IIS 網站。 在撰寫本文時，由於 Web 發行管線（WPP）中的錯誤，您無法使用包含查詢字串的端點位址來執行 *.deploy*檔案。 在此案例中，您需要直接使用 Msdeploy.exe 來部署您的 web 封裝。

> [!NOTE]
> 如需有關 Web Deploy 遠端代理程式服務和 Web Deploy 處理常式的詳細資訊，請參閱[選擇正確的 Web 部署方法](../configuring-server-environments-for-web-deployment/choosing-the-right-approach-to-web-deployment.md)。 如需如何設定環境特定專案檔以部署至這些端點的指引，請參閱設定[目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

## <a name="authentication-considerations"></a>驗證考量

無論您是藉由執行 *.deploy*檔案或直接使用 msdeploy.exe 來部署 web 封裝，都必須指定驗證類型。 Web Deploy 接受兩個可能的值： **NTLM**或**Basic**。 如果指定基本驗證，您也必須提供使用者名稱和密碼。 當您選取驗證類型時，需要留意的各種因素如下：

- 如果您要部署到 Web Deploy 遠端代理程式服務，則必須使用 NTLM 驗證。 遠端代理程式服務不接受基本驗證認證。
- 如果您要部署到 Web Deploy 處理常式，可以使用 NTLM 或基本驗證。 預設設定為 [基本驗證]。 雖然基本驗證依賴以純文字傳送的使用者名稱和密碼，但您的認證會受到保護，因為 Web Deploy 處理常式一律使用 SSL 加密。
- 如果您的網頁封裝包含資料庫，而 web 伺服器和資料庫伺服器是不同的電腦，由於[ntlm 「雙躍點](https://go.microsoft.com/?linkid=9805120)」的限制，您將無法使用 ntlm 驗證來部署資料庫。 您需要在部署連接字串中使用 SQL Server 認證，或提供基本驗證認證來 Web Deploy。 將[成員資格資料庫部署到企業環境](../advanced-enterprise-web-deployment/deploying-membership-databases-to-enterprise-environments.md)中有更詳細的說明此問題。

## <a name="conclusion"></a>結論

本主題說明如何藉由執行 *.deploy*檔案或直接使用 msdeploy.exe 來部署 web 封裝。 文中說明了每種方法的適當時機，並說明如何在較大的單一步驟或自動化的組建程式中，將部署命令參數化和執行。

## <a name="further-reading"></a>進一步閱讀

如需如何建立和參數化 web 部署套件的指引，請參閱[建立和封裝 Web 應用程式專案](building-and-packaging-web-application-projects.md)和設定[web 套件部署的參數](configuring-parameters-for-web-package-deployment.md)。 如需如何從 Team Foundation Server （TFS）實例建立及部署 web 封裝的指引，請參閱設定[自動化 Web 部署的 Team Foundation Server](../configuring-team-foundation-server-for-web-deployment/configuring-team-foundation-server-for-web-deployment.md)。 如需如何自訂和疑難排解部署程式的相關資訊，請參閱[從部署中排除檔案和資料夾](../advanced-enterprise-web-deployment/excluding-files-and-folders-from-deployment.md)。

> [!div class="step-by-step"]
> [上一頁](configuring-parameters-for-web-package-deployment.md)
> [下一頁](deploying-database-projects.md)
