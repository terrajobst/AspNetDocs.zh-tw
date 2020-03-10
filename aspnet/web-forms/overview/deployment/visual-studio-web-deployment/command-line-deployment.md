---
uid: web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
title: 使用 Visual Studio：命令列部署來 ASP.NET Web 部署 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 82b8dea0-f062-4ee4-8784-3ffa30fbb1ca
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/command-line-deployment
msc.type: authoredcontent
ms.openlocfilehash: 13cfe4492398b59f2c80394689cc113ccb218c60
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78630918"
---
# <a name="aspnet-web-deployment-using-visual-studio-command-line-deployment"></a>使用 Visual Studio：命令列部署來 ASP.NET Web 部署

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>概觀

本教學課程說明如何從命令列叫用 Visual Studio web 發佈管線。 這適用于您想要將部署程式[自動化](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)的案例，而不是在 Visual Studio 中手動執行，通常是使用[原始程式碼版本控制系統](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)。

## <a name="make-a-change-to-deploy"></a>進行部署的變更

目前 [關於] 頁面會顯示範本程式碼。

![包含範本程式碼的關於頁面](command-line-deployment/_static/image1.png)

您會將其取代為顯示學生註冊摘要的程式碼。

開啟*About .aspx*頁面，刪除 `MainContent` `Content` 元素內的所有標記，並在其位置插入下列標記：

[!code-aspx[Main](command-line-deployment/samples/sample1.aspx)]

執行專案，並選取 [**關於**] 頁面。

![About 頁面](command-line-deployment/_static/image2.png)

## <a name="deploy-to-test-by-using-the-command-line"></a>使用命令列部署以進行測試

您不會部署其他資料庫變更，因此請停用 aspnet ContosoUniversity 資料庫的 dbDacFx 資料庫部署。 開啟 [**發行 Web** wizard]，並在三個發行設定檔的每一個中，清除 [**設定**] 索引標籤上的 [**更新資料庫**] 核取方塊。

在 Windows 8 起始頁中，搜尋**VS2012 的開發人員命令提示字元**。

以滑鼠右鍵按一下 VS2012 的**開發人員命令提示字元**圖示，然後按一下 [**以系統管理員身分執行**]。

在命令提示字元中輸入下列命令，以方案檔的路徑取代方案檔的路徑：

[!code-console[Main](command-line-deployment/samples/sample2.cmd)]

MSBuild 會建立方案，並將其部署至測試環境。

![命令列輸出](command-line-deployment/_static/image3.png)

開啟瀏覽器並移至 `http://localhost/ContosoUniversity`，然後按一下 [**關於**] 頁面，確認部署是否成功。

如果您尚未在測試中建立任何學生，您會在 [**學生主體統計資料]** 標題底下看到空白頁面。 前往 [**學生**] 頁面，按一下 [**新增學生**]，再新增一些學生，然後返回 [**關於**] 頁面以查看學生統計資料。

![測試環境中的關於頁面](command-line-deployment/_static/image4.png)

## <a name="key-command-line-options"></a>金鑰命令列選項

您輸入的命令已將解決方案檔案路徑和兩個屬性傳遞至 MSBuild：

[!code-console[Main](command-line-deployment/samples/sample3.cmd)]

### <a name="deploying-the-solution-versus-deploying-individual-projects"></a>部署解決方案與部署個別專案

指定方案檔會導致建立方案中的所有專案。 如果您的方案中有多個 Web 專案，則會套用下列 MSBuild 行為：

- 您在命令列上指定的屬性會傳遞至每個專案。 因此，每個 Web 專案都必須有您指定之名稱的發行設定檔。 如果您指定 `/p:PublishProfile=Test`，每個 Web 專案都必須有一個名為*Test*的發行設定檔。
- 當另一個專案不是建立時，您可能會成功發行一個。 如需詳細資訊，請參閱 stackoverflow 執行緒[MSBuild 失敗並有兩個封裝](http://stackoverflow.com/questions/14226451/msbuild-fails-with-two-packages)。

如果您指定個別的專案，而不是方案，則必須加入指定 Visual Studio 版本的參數。 如果您使用 Visual Studio 2012，命令列會類似于下列範例：

[!code-console[Main](command-line-deployment/samples/sample4.cmd?highlight=1)]

Visual Studio 2010 的版本號碼為10.0。 如需詳細資訊，請參閱 Sayed Hashimi 的 blog 中的[Visual Studio 專案相容性和 VisualStudioVersion](http://sedodream.com/2012/08/19/VisualStudioProjectCompatabilityAndVisualStudioVersion.aspx) 。

### <a name="specifying-the-publish-profile"></a>指定發行設定檔

您可以依名稱或 *.pubxml*檔案的完整路徑來指定發行設定檔，如下列範例所示：

[!code-console[Main](command-line-deployment/samples/sample5.cmd?highlight=1)]

### <a name="web-publish-methods-supported-for-command-line-publishing"></a>支援命令列發行的 Web 發行方法

命令列發行支援三種發行方法：

- `MSDeploy`-使用 Web Deploy 發佈。
- `Package`-藉由建立 Web Deploy 套件來發行。 您必須從建立套件的 MSBuild 命令分開安裝。
- `FileSystem`-將檔案複製到指定的資料夾以進行發佈。

### <a name="specifying-the-build-configuration-and-platform"></a>指定組建設定和平臺

組建設定和平臺必須在 Visual Studio 中或在命令列上設定。 發行設定檔包含名為 `LastUsedBuildConfiguration` 和 `LastUsedPlatform`的屬性，但您無法設定這些屬性，以決定專案的建立方式。 如需詳細資訊，請參閱[MSBuild：如何設定](http://sedodream.com/2012/10/27/MSBuildHowToSetTheConfigurationProperty.aspx)Sayed Hashimi 的 blog 的 configuration 屬性。

## <a name="deploy-to-staging"></a>部署至預備環境

若要部署至 Azure，您必須將密碼新增至命令列。 如果您已將密碼儲存在 Visual Studio 的發行設定檔中，它會以加密格式儲存在您的 *.pubxml 使用者*檔案中。 當您執行命令列部署時，MSBuild 不會存取該檔案，因此您必須在命令列參數中傳入密碼。

1. 從您稍早針對預備網站所下載的 *.publishsettings*檔案複製所需的密碼。 Password 是 Web Deploy `publishProfile` 元素的 `userPWD` 屬性值。

    ![Web Deploy 密碼](command-line-deployment/_static/image5.png)
2. 在 Windows 8 起始頁中，搜尋**VS2012 的開發人員命令提示字元**，然後按一下圖示以開啟命令提示字元。 （這次您不需要將它開啟為系統管理員，因為您不是部署到本機電腦上的 IIS）。
3. 在命令提示字元中輸入下列命令，將方案檔的路徑取代為您方案檔的路徑，並將密碼替換成您的密碼：

    [!code-console[Main](command-line-deployment/samples/sample6.cmd)]

    請注意，此命令列會包含額外的參數： `/p:AllowUntrustedCertificate=true`。 隨著本教學課程的撰寫，當您從命令列發佈至 Azure 時，必須設定 `AllowUntrustedCertificate` 屬性。 當此 bug 的修正程式發行時，您就不需要該參數。
4. 開啟瀏覽器並移至預備網站的 URL，然後按一下 [**關於**] 頁面，確認部署是否成功。

    如您稍早在測試環境中所見，您可能必須建立一些學生，才能在 [**關於**] 頁面上查看統計資料。

## <a name="deploy-to-production"></a>部署至生產環境

部署至生產環境的程式與預備的進程類似。

1. 從您稍早針對生產網站所下載的 *.publishsettings*檔案複製所需的密碼。
2. 開啟**VS2012 的開發人員命令提示字元**。
3. 在命令提示字元中輸入下列命令，將方案檔的路徑取代為您方案檔的路徑，並將密碼替換成您的密碼：

    [!code-console[Main](command-line-deployment/samples/sample7.cmd)]

    對於實際的生產網站，如果也有資料庫變更，您通常會在部署之前將*應用程式\_離線 .htm*檔案複製到網站，並在部署成功之後將其刪除。
4. 開啟瀏覽器並移至預備網站的 URL，然後按一下 [**關於**] 頁面，確認部署是否成功。

## <a name="summary"></a>總結

您現在已使用命令列部署應用程式更新。

![測試環境中的關於頁面](command-line-deployment/_static/image6.png)

在下一個教學課程中，您會看到如何擴充 web 發佈管線的範例。 此範例將示範如何部署專案中未包含的檔案。

> [!div class="step-by-step"]
> [上一頁](deploying-a-database-update.md)
> [下一頁](deploying-extra-files.md)
