---
uid: web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
title: 建立和執行部署命令檔 |Microsoft Docs
author: jrjlee
description: 本主題描述如何建立命令檔，讓您使用 Microsoft Build Engine （MSBuild）專案檔以單一步驟執行部署，然後重新 。
ms.author: riande
ms.date: 05/04/2012
ms.assetid: c61560e9-9f6c-4985-834a-08a3eabf9c3c
msc.legacyurl: /web-forms/overview/deployment/web-deployment-in-the-enterprise/creating-and-running-a-deployment-command-file
msc.type: authoredcontent
ms.openlocfilehash: f1477ff423e4898385066a35b42503f3c70dcc68
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78634306"
---
# <a name="creating-and-running-a-deployment-command-file"></a>建立及執行部署命令檔

[Jason 先生](https://github.com/jrjlee)

[下載 PDF](https://msdnshared.blob.core.windows.net/media/MSDNBlogsFS/prod.evol.blogs.msdn.com/CommunityServer.Blogs.Components.WeblogFiles/00/00/00/63/56/8130.DeployingWebAppsInEnterpriseScenarios.pdf)

> 本主題描述如何建立命令檔，讓您使用 Microsoft Build Engine （MSBuild）專案檔，以單一步驟、可重複的程式執行部署。

本主題會根據名為 Fabrikam，Inc. 之虛構公司的企業部署需求，形成一系列教學課程的一部分。本教學課程系列使用&#x2014; [Contact Manager](the-contact-manager-solution.md)解決方案&#x2014;的範例解決方案，來代表具有實際複雜度層級的 WEB 應用程式，包括 ASP.NET MVC 3 應用程式、Windows Communication Foundation （WCF）服務和資料庫專案。

這些教學課程中的部署方法是以[瞭解組建](understanding-the-build-process.md)程式中所述的分割專案檔案方法為基礎，其中的組建程式是由兩個專案檔所控制&#x2014;，其中一個包含適用于每個目的地環境的組建指示，另一個包含環境特定的組建和部署設定。 在組建期間，環境特定的專案檔會合並到環境無關的專案檔中，以形成一組完整的組建指示。

## <a name="process-overview"></a>程序概觀

在本主題中，您將瞭解如何建立及執行命令檔，以使用這些專案檔對目標環境執行可重複的部署。 基本上，命令檔只需要包含 MSBuild 命令，它會：

- 告訴 MSBuild 執行與環境無關的*Publish*檔案。
- 告訴*Publish*檔案，其中包含環境特定的專案設定以及要在哪裡尋找。

## <a name="create-an-msbuild-command"></a>建立 MSBuild 命令

如[瞭解組建](understanding-the-build-process.md)程式中所述，環境特定的專案&#x2014;檔（例如， *Env-Dev*&#x2014;）是設計成要在組建時匯入到與環境無關的*Publish*檔案中。 這兩個檔案一起提供一組完整的指示，告訴 MSBuild 如何建立和部署您的解決方案。

*Publish*檔案會使用**import**元素來匯入環境特定的專案檔。

[!code-xml[Main](creating-and-running-a-deployment-command-file/samples/sample1.xml)]

因此，當您使用 Msbuild.exe 來建立及部署 Contact Manager 解決方案時，您必須：

- 在*Publish*檔案上執行 msbuild.exe。
- 藉由提供名為**TargetEnvPropsFile**的命令列參數，指定環境特定專案檔的位置。

若要這麼做，您的 MSBuild 命令應如下所示：

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample2.cmd)]

從這裡開始，是移至可重複的單一步驟部署的簡單步驟。 您只需要將 MSBuild 命令新增至 .cmd 檔案就可以了。 在 Contact Manager 解決方案中，Publish 資料夾包含名為*Publish-Dev*的檔案，它會確實執行此工作。

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample3.cmd)]

> [!NOTE]
> **/Fl**參數會指示 msbuild 在用來叫用 msbuild.exe 的工作目錄中，建立名為*msbuild.exe*的記錄檔。

若要部署或重新部署 Contact Manager 解決方案，您只需要執行*Publish-Dev .cmd*檔案。 當您執行檔案時，MSBuild 將會：

- 建立方案中的所有專案。
- 為 web 應用程式專案產生可部署的 web 封裝。
- 為資料庫專案產生 .dbschema 和. deploymanifest 檔案。
- 將 web 套件部署到 web 伺服器。
- 將資料庫部署到資料庫伺服器。

## <a name="run-the-deployment"></a>執行部署

當您已建立目標環境的命令檔時，您應該只要執行檔案就可以完成整個部署。

**將 Contact Manager 解決方案部署至您的測試環境**

1. 在開發人員工作站上，開啟 Windows Explorer，然後流覽至*Publish-Dev*檔案的位置。
2. 按兩下檔案加以執行。
3. 如果出現 [**開啟檔案-安全性警告**] 對話方塊，請按一下 [**執行**]。
4. 如果您的設定和測試伺服器設定正確，當 MSBuild 完成處理專案檔時，[命令提示字元] 視窗會顯示**組建成功**訊息。

    ![](creating-and-running-a-deployment-command-file/_static/image1.png)
5. 如果這是您第一次將解決方案部署到此環境，您將需要將測試 web 伺服器電腦帳戶新增至**ContactManager**資料庫上的**db\_資料寫入元**和**db\_datareader**角色。 [設定用於 Web Deploy 發佈的資料庫伺服器](../configuring-server-environments-for-web-deployment/configuring-a-database-server-for-web-deploy-publishing.md)中會描述此程式。

    > [!NOTE]
    > 當您建立資料庫時，您只需要指派這些許可權。 根據預設，組建程式不會在每個部署&#x2014;上重新建立資料庫，而是會將現有的資料庫與最新的架構進行比較，並只進行所需的變更。 因此，您應該只在第一次部署解決方案時，才需要對應這些資料庫角色。
6. 開啟 Internet Explorer 並流覽至 Contact Manager 應用程式的 URL （例如，`http://testweb1:85/ContactManager/`）。
7. 確認應用程式如預期般運作，而且您能夠新增連絡人。

    ![](creating-and-running-a-deployment-command-file/_static/image2.png)

## <a name="conclusion"></a>結論

建立包含 MSBuild 指示的命令檔，可讓您快速且輕鬆地建立多專案方案，並將其部署到特定的目的地環境。 如果您需要將解決方案重複部署至多個目的地環境，可以建立多個命令檔。 在每個命令檔中，MSBuild 命令會建立相同的通用專案檔，但它會指定不同的環境特定專案檔案。 例如，要發行至開發人員或測試環境的命令檔可能包含此 MSBuild 命令：

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample4.cmd)]

發行至預備環境的命令檔可能包含此 MSBuild 命令：

[!code-console[Main](creating-and-running-a-deployment-command-file/samples/sample5.cmd)]

> [!NOTE]
> 如需如何為您自己的伺服器環境自訂環境特定專案檔案的指引，請參閱設定[目標環境的部署屬性](../configuring-server-environments-for-web-deployment/configuring-deployment-properties-for-a-target-environment.md)。

您也可以在 MSBuild 命令中覆寫屬性或設定各種其他參數，以自訂每個環境的組建程式。 如需詳細資訊，請參閱[MSBuild 命令列參考](https://msdn.microsoft.com/library/ms164311.aspx)。

> [!div class="step-by-step"]
> [上一頁](deploying-database-projects.md)
> [下一頁](manually-installing-web-packages.md)
