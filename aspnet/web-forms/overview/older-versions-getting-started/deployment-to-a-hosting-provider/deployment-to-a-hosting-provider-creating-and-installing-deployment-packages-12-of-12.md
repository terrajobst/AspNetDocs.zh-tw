---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
title: 使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式：疑難排解（12/12） |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 3fc23eed-921d-4d46-a610-a2d156e4bd03
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12
msc.type: authoredcontent
ms.openlocfilehash: db8f58e3679e6dea865dadb6f64916032dd9f38c
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74639867"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-troubleshooting-12-of-12"></a>使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式：疑難排解（12/12）

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署至 Windows Azure 網站，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

此頁面說明當您使用 Visual Studio 部署 ASP.NET web 應用程式時，可能會發生的一些常見問題。 針對每一個，會提供一或多個可能的原因和對應的解決方案。

## <a name="server-error-in--application---current-custom-error-settings-prevent-details-of-the-error-from-being-viewed-remotely"></a>'/' 應用程式中的伺服器錯誤-目前的自訂錯誤設定導致無法從遠端查看錯誤的詳細資料

### <a name="scenario"></a>情節

將網站部署至遠端主機之後，您會收到錯誤訊息，指出 Web.config 檔案中的 customErrors 設定，但不會指出錯誤的實際原因：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample1.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

根據預設，只有當您的 web 應用程式在本機電腦上執行時，ASP.NET 才會顯示詳細的錯誤資訊。 當您的 web 應用程式可透過網際網路公開取得時，通常不會想要顯示詳細錯誤資訊，因為駭客可能可以使用這項資訊來找出應用程式中的弱點。 不過，當您將網站或更新部署至網站時，有時會發生錯誤，而且您需要取得實際的錯誤訊息。

若要讓應用程式在遠端主機上執行時顯示詳細的錯誤訊息，請編輯 Web.config 檔案以將 `customErrors` 模式設定為關閉、重新部署應用程式，然後再次執行應用程式：

1. 如果應用程式的 web.config 檔案在 `system.web` 元素中具有 `customErrors` 元素，請將 `mode` 屬性變更為 "off"。 否則，請將 `mode` 屬性設為 "off" 的 `system.web` 元素中的 `customErrors` 元素，如下列範例所示：

    [!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample2.xml?highlight=3)]
2. 部署應用程式。
3. 執行應用程式，並重複先前造成錯誤發生的任何動作。 現在您可以看到實際的錯誤訊息。
4. 當您解決錯誤時，請還原原始的 `customErrors` 設定，然後重新部署應用程式。

## <a name="access-is-denied-in-a-web-page-that-uses-sql-server-compact"></a>在使用 SQL Server Compact 的網頁中拒絕存取

### <a name="scenario"></a>情節

當您部署使用 SQL Server Compact 的網站，並在已部署的網站中執行可存取資料庫的頁面時，您會看到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample3.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

伺服器上的網路服務帳戶必須能夠讀取*bin\amd64*或*bin\x86*資料夾中的 SQL 服務 Compact 原生二進位檔，但它並沒有這些資料夾的讀取權限。 在*bin*資料夾上設定 NETWORK SERVICE 的 [讀取] 許可權，並務必將許可權延伸至子資料夾。

## <a name="cannot-read-configuration-file-due-to-insufficient-permissions"></a>無法讀取設定檔案，因為許可權不足

### <a name="scenario"></a>情節

當您按一下 [Visual Studio 發佈] 按鈕，將應用程式部署到本機電腦上的 IIS 時，發佈會失敗，而且 [**輸出**] 視窗會顯示類似下面的錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample4.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

若要在本機電腦上使用單鍵 [發行至 IIS]，您必須以系統管理員許可權執行 Visual Studio。 關閉 Visual Studio，然後以系統管理員許可權重新開機它。

## <a name="could-not-connect-to-the-destination-computer--using-the-specified-process"></a>無法連接到目的地電腦 。使用指定的進程

### <a name="scenario"></a>情節

當您按一下 [Visual Studio 發佈] 按鈕來部署應用程式時，發行會失敗，而且 [**輸出**] 視窗會顯示類似下面的錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample5.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

Proxy 伺服器正中斷與目的地伺服器的通訊。 從 Windows [控制台] 或 Internet Explorer 中，選取 [**網際網路選項** **]，** 然後選取 [連線] 索引標籤。在 [**網際網路**內容] 對話方塊中，按一下 [ **LAN 設定**]。 在 [**區域網路（LAN）設定**] 對話方塊中，清除 [**自動偵測設定**] 核取方塊。 然後再次按一下 [發佈] 按鈕。

如果問題持續發生，請洽詢您的系統管理員，以判斷可以使用 proxy 或防火牆設定來完成的動作。 發生此問題的原因是 Web Deploy 針對 Web 管理服務部署使用非標準埠（8172）;針對其他連接，Web Deploy 使用埠80。 當您要部署到協力廠商裝載提供者時，通常是使用 Web 管理服務。

## <a name="default-net-40-application-pool-does-not-exist"></a>預設 .NET 4.0 應用程式集區不存在

### <a name="scenario"></a>情節

當您部署需要 .NET Framework 4 的應用程式時，您會看到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample6.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

IIS 中未安裝 ASP.NET 4。 如果您要部署的伺服器是您的開發電腦，且安裝了 Visual Studio 2010，則 ASP.NET 4 會安裝在電腦上，但可能不會安裝在 IIS 中。 在您要部署的伺服器上，開啟提升許可權的命令提示字元，並執行下列命令，在 IIS 中安裝 ASP.NET 4：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample7.cmd)]

您可能也需要手動設定預設應用程式集區的 .NET Framework 版本。 如需詳細資訊，請參閱[部署至 IIS 作為測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教學課程。

## <a name="format-of-the-initialization-string-does-not-conform-to-specification-starting-at-index-0"></a>初始化字串的格式不符合從索引0開始的規格。

### <a name="scenario"></a>情節

當您使用單鍵發行來部署應用程式之後，當您執行存取資料庫的頁面時，會收到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample8.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

開啟已*部署網站中的 web.config*檔案，並檢查連接字串值是否以 `$(ReplaceableToken_`開頭，如下列範例所示：

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample9.xml)]

如果連接字串看起來像這個範例，請編輯專案檔，並將下列屬性新增至所有組建設定的 `PropertyGroup` 元素：

[!code-xml[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample10.xml)]

然後重新部署應用程式。

## <a name="http-500-internal-server-error"></a>HTTP 500 內部伺服器錯誤

### <a name="scenario"></a>情節

當您執行部署的網站時，您會看到下列錯誤訊息，其中沒有指出錯誤原因的特定資訊：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample11.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

500錯誤有許多原因，但如果您遵循這些教學課程，其中一個可能的原因是，您將 XML 元素放在其中一個 XML 轉換檔案中的錯誤位置。 例如，如果您將轉換插入 `<system.web>` 之下的 `<location>` 專案，而不是直接在 `<configuration>`下，就會收到這個錯誤。 在這種情況下，解決方法是更正 XML 轉換檔並重新部署。

## <a name="http-50021-internal-server-error"></a>HTTP 500.21 內部伺服器錯誤

### <a name="scenario"></a>情節

當您執行已部署的網站時，您會看到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample12.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

您已部署的網站是以 ASP.NET 4 為目標，但 ASP.NET 4 並未在伺服器上的 IIS 中註冊。 在伺服器上，開啟提升許可權的命令提示字元，並執行下列命令來註冊 ASP.NET 4：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample13.cmd)]

您可能也需要手動設定預設應用程式集區的 .NET Framework 版本。 如需詳細資訊，請參閱[部署至 IIS 作為測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教學課程。

## <a name="login-failed-opening-sql-server-express-database-in-app_data"></a>登入無法在應用程式\_資料中開啟 SQL Server Express 資料庫

### <a name="scenario"></a>情節

您已將*web.config*檔案連接字串更新為指向 SQL Server Express 資料庫，以作為*應用程式\_Data*資料夾中的 *.mdf*檔案，而且第一次執行應用程式時，您會看到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample14.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

*.Mdf*檔案的名稱不能與電腦上曾經存在的任何 SQL Server Express 資料庫名稱相符，即使您刪除了先前現有資料庫的 *.mdf*檔案也一樣。 將 *.mdf*檔案的名稱變更為從未用來做為資料庫名稱的名稱，並將*web.config*檔案變更為使用新的名稱。 或者，您可以使用[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)來刪除先前現有 SQL Server Express 資料庫。

## <a name="model-compatibility-cannot-be-checked"></a>無法檢查模型相容性

### <a name="scenario"></a>情節

您已將*web.config*檔案連接字串更新為指向新的 SQL Server Express 資料庫，而且第一次執行應用程式時，您會看到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample15.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

如果您放入 Web.config 檔案中的資料庫名稱在您的電腦之前曾經使用過，則資料庫中可能已經有一些資料表存在。 選取先前尚未在電腦上使用的新名稱，並將*web.config*檔案變更為指向 [使用這個新的資料庫名稱]。 或者，您可以使用[SQL Server Express 公用程式](https://www.microsoft.com/download/details.aspx?DisplayLang=en&amp;id=3990)或[SQL Server Management Studio Express](https://www.microsoft.com/download/details.aspx?displaylang=en&amp;id=7593)來刪除現有的資料庫。

## <a name="sql-error-when-a-script-attempts-to-create-users-or-roles"></a>腳本嘗試建立使用者或角色時發生 SQL 錯誤

### <a name="scenario"></a>情節

您正在使用 [**封裝/發行 SQL** ] 索引標籤上所設定的資料庫部署，在部署期間執行的 SQL 腳本包括 [建立使用者] 或 [建立角色] 命令，而執行這些命令時，腳本執行會失敗。 您可能會看到更詳細的訊息，如下所示：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample16.cmd)]

如果您在 [**發行 Web** ] 嚮導中設定資料庫部署，而不是 [**封裝/發行 SQL** ] 索引標籤，則會發生此錯誤，請在 [設定[及部署](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)] 論壇中建立執行緒，此解決方案將會新增至此 [疑難排解] 頁面。

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

您用來執行部署的使用者帳戶沒有建立使用者或角色的許可權。 例如，主控公司可能會將 `db_datareader`、`db_datawriter`和 `db_ddladmin` 角色指派給它為您設定的使用者帳戶。 這些就足以建立大部分的資料庫物件，而不是建立使用者或角色。 避免錯誤的其中一種方法是從資料庫部署中排除使用者和角色。 若要這麼做，您可以編輯資料庫自動產生之腳本的 `PreSource` 元素，使其包含下列屬性：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample17.cmd)]

如需如何在專案檔中編輯 `PreSource` 元素的詳細資訊，請參閱[如何：編輯專案檔中的部署設定](https://msdn.microsoft.com/library/ff398069(v=vs.100).aspx)。 如果您的開發資料庫中的使用者或角色必須位於目的地資料庫中，請洽詢您的主機服務提供者以取得協助。

## <a name="sql-server-timeout-error-when-running-custom-scripts-during-deployment"></a>在部署期間執行自訂腳本時發生 SQL Server 逾時錯誤

### <a name="scenario"></a>情節

您已指定要在部署期間執行的自訂 SQL 腳本，而當 Web Deploy 執行時，它們會超時。

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

執行多個具有不同交易模式的腳本可能會導致逾時錯誤。 根據預設，自動產生的腳本會在交易中執行，但是自訂腳本則不會。 如果您在 [**封裝/發行 SQL** ] 索引標籤上選取 [**從現有資料庫提取資料及/或架構**] 選項，而且加入自訂 SQL 腳本，則必須變更某些腳本的交易設定，讓所有腳本都使用相同的交易設定。 如需詳細資訊，請參閱[如何：使用 Web 應用程式專案部署資料庫](https://msdn.microsoft.com/library/dd465343.aspx)。

如果您已設定交易設定，讓全部都相同，但仍然收到此錯誤，則可能的因應措施是分別執行腳本。 在 [**封裝/發行**SQL] 索引標籤的 [**資料庫腳本**] 方格中，清除導致逾時錯誤之腳本的 [**包含**] 核取方塊，然後發佈專案。 然後回到 [**資料庫腳本**] 方格中，選取該腳本的 [**包含**] 核取方塊，並清除其他腳本的 [**包含**] 核取方塊。 然後再次發行專案。 這次當您發佈時，只有選取的自訂腳本會執行。

## <a name="stream-data-of-site-manifest-is-not-yet-available"></a>尚未提供網站資訊清單的串流資料

### <a name="scenario"></a>情節

當您使用*部署 .cmd*檔案搭配 `t` （測試）選項來安裝套件時，您會看到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample18.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

錯誤訊息表示命令無法產生測試報告。 不過，如果您使用 [`y` （實際安裝）] 選項，此命令可能會執行。 訊息只會指出在測試模式中執行命令時發生問題。

## <a name="this-application-requires-managedruntimeversion-v40"></a>此應用程式需要 ManagedRuntimeVersion v4。0

### <a name="scenario"></a>情節

當您嘗試部署時，您會看到下列錯誤訊息：

 錯誤： ' sitemanifest/dbFullSql [@path= ' C:\TEMP\AdventureWorksGrant.sql ']/sqlScript ' 的資料流程資料尚無法使用。 您嘗試使用的應用程式集區，' managedRuntimeVersion ' 屬性設定為 ' v2.0 '。 此應用程式需要 ' v4.0 '。 

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

IIS 中未安裝 ASP.NET 4。 如果您要部署的伺服器是您的開發電腦，且安裝了 Visual Studio 2010，則 ASP.NET 4 會安裝在電腦上，但可能不會安裝在 IIS 中。 在您要部署的伺服器上，開啟提升許可權的命令提示字元，並執行下列命令，在 IIS 中安裝 ASP.NET 4：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample19.cmd)]

## <a name="unable-to-cast-microsoftwebdeploymentdeploymentprovideroptions"></a>無法轉換 DeploymentProviderOptions。

### <a name="scenario"></a>情節

當您部署套件時，您會看到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample20.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

您正嘗試使用 Web Deploy 1.1 UI，從 IIS 管理員部署到已安裝 Web Deploy 2.0 的伺服器。 如果您要透過匯入封裝來使用 IIS 遠端系統管理工具來進行部署，請在建立連線時，核取 [**可用的新功能**] 對話方塊。 （在第一次建立連接時，這個對話方塊可能只會顯示一次。 若要清除連線並重新開始，請關閉 [IIS 管理員]，然後在命令提示字元中輸入 `inetmgr /reset`，再次啟動它。）如果列出的其中一個功能是**WEB DEPLOY UI**，而且其版本號碼低於8，則您要部署的伺服器可能會安裝1.1 和2.0 版的 Web Deploy。 若要從已安裝2.0 的用戶端部署，伺服器必須只安裝 Web Deploy 2.0。 您必須洽詢您的主機服務提供者，才能解決此問題。

## <a name="unable-to-load-the-native-components-of-sql-server-compact"></a>無法載入 SQL Server Compact 的原生元件

### <a name="scenario"></a>情節

當您執行已部署的網站時，您會看到下列錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample21.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

已部署的網站在應用程式的*bin*資料夾底下，沒有具有原生元件的*amd64*和*x86*子資料夾。 在已安裝 SQL Server Compact 的電腦上，原生元件位於*C:\Program Files\Microsoft SQL Server Compact Edition\v4.0\Private*。 在 Visual Studio 專案的正確資料夾中取得正確檔案的最佳方式，是安裝 NuGet Entityframework.sqlservercompact 套件。 套件安裝會加入後置組建腳本，將原生元件複製到*amd64*和*x86*。 不過，為了要部署這些專案，您必須手動將它們包含在專案中。 如需詳細資訊，請參閱[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教學課程。

## <a name="path-is-not-valid-error-after-deploying-an-entity-framework-code-first-application"></a>部署 Entity Framework Code First 應用程式之後發生「路徑無效」錯誤

### <a name="scenario"></a>情節

您部署的應用程式會使用 Entity Framework Code First 移轉和 DBMS （例如 SQL Server Compact），將其資料庫儲存在應用程式\_Data 資料夾的檔案中。 您已設定 Code First 移轉在第一次部署之後建立資料庫。 當您執行應用程式時，您會收到類似下列範例的錯誤訊息：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample22.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

Code First 嘗試建立資料庫，但應用程式\_的資料檔案夾不存在。 當您部署時，*應用\_程式*中沒有任何檔案，或您在 [**專案屬性**] 視窗的 [**封裝/發行 Web** ] 索引標籤上選取了 [**排除應用程式\_資料**]，可能是您沒有任何檔案。 如果資料夾中沒有要複製到伺服器的檔案，部署程式將不會在伺服器上建立資料夾。 如果您已在網站中設定資料庫，則如果您在發行設定檔中選取 [**移除目的地的其他**檔案]，部署程式將會刪除檔案和*應用程式\_資料*資料夾本身。 若要解決此問題，請將預留位置檔案（例如 .txt 檔案）放在*應用程式\_Data*資料夾中，確定您未選取 [**排除應用程式]\_資料**，然後重新部署。 

## <a name="com-object-that-has-been-separated-from-its-underlying-rcw-cannot-be-used"></a>「無法使用與基礎 RCW 分隔的 COM 物件」。

### <a name="scenario"></a>情節

您已成功使用單鍵發行來部署您的應用程式，然後開始收到此錯誤：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample23.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

關閉和重新開機 Visual Studio 通常是解決此錯誤所需的一切。

## <a name="deployment-fails-because-user-credentials-used-for-publishing-dont-have-setacl-authority"></a>部署失敗，因為用於發佈的使用者認證沒有 setACL 授權單位

### <a name="scenario"></a>情節

發行失敗並出現錯誤，指出您沒有設定資料夾許可權的授權單位（您所使用的使用者帳戶沒有 setACL 授權單位）。

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

根據預設，Visual Studio 會設定網站根資料夾的讀取權限，以及應用程式\_Data 資料夾的寫入權限。 如果您知道網站資料夾的預設許可權是正確的，而且不需要設定，您可以藉由將 **&lt;IncludeSetACLProviderOn 目的地&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 新增至發行設定檔檔案（以影響單一設定檔）或對 wpp .targets 檔（影響所有設定檔），停用此行為。 如需如何編輯這些檔案的詳細資訊，請參閱[如何：編輯設定檔（. .pubxml）中的部署設定](https://msdn.microsoft.com/library/ff398069.aspx)。 

## <a name="access-denied-errors-when-the-application-tries-to-write-to-an-application-folder"></a>應用程式嘗試寫入應用程式資料夾時發生拒絕存取的錯誤

### <a name="scenario"></a>情節

您的應用程式在嘗試建立或編輯其中一個應用程式資料夾中的檔案時發生錯誤，因為它沒有該資料夾的寫入權限。

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

根據預設，Visual Studio 會設定網站根資料夾的讀取權限，以及應用程式\_Data 資料夾的寫入權限。 如果您的應用程式需要子資料夾的寫入權限，您可以設定該資料夾的許可權，如[設定資料夾許可權](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)和[部署到生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中所示。 如果您的應用程式需要網站根資料夾的寫入存取權，您必須將 **&lt;IncludeSetACLProviderOn 目的地&gt;False&lt;/IncludeSetACLProviderOnDestination&gt;** 新增至發行設定檔檔案（以影響單一設定檔）或 wpp .targets 檔（以影響所有設定檔），以防止它在根資料夾上設定唯讀存取。 如需如何編輯這些檔案的詳細資訊，請參閱[如何：編輯設定檔（. .pubxml）中的部署設定](https://msdn.microsoft.com/library/ff398069.aspx)。 <a id="aspnet45error"></a>

## <a name="configuration-error---targetframework-attribute-references-a-version-that-is-later-than-the-installed-version-of-the-net-framework"></a>設定錯誤-targetFramework 屬性參考的版本比安裝的版本還要新 .NET Framework

### <a name="scenario"></a>情節

您已成功發行以 ASP.NET 4.5 為目標的 Web 專案，但當您執行應用程式（並在 web.config 檔案中將 `customErrors` 模式設定為 "off"）時，會收到下列錯誤：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample24.cmd)]

錯誤頁面的 [來源錯誤] 方塊會反白顯示 Web.config 中的下列這一行，做為錯誤的原因：

[!code-console[Main](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12/samples/sample25.cmd)]

### <a name="possible-cause-and-solution"></a>可能的原因和解決方案

伺服器不支援 ASP.NET 4.5。 請洽詢主控提供者，以判斷何時及是否可新增 ASP.NET 4.5 的支援。 如果無法選擇升級伺服器，您就必須改為部署以 ASP.NET 4 或更早版本為目標的 Web 專案。如果您將 ASP.NET 4 或舊版 Web 專案部署到相同的目的地，請在 [**發行 web** wizard] 的 [**設定**] 索引標籤上，選取 [**移除目的地的其他**檔案] 核取方塊。 如果您未選取 [**移除目的地的其他**檔案]，將會繼續取得設定錯誤頁面。

[專案**屬性**] 視窗包含 [目標 framework] 下拉式清單，但您無法解決此問題，只需將 **.NET Framework 4.5**變更為 **.NET Framework 4**。 如果您將目標 framework 變更為舊版架構，此專案仍會參考較新的 framework 版本元件，而且不會執行。 您必須手動變更這些參考，或建立以 .NET Framework 4 或更早版本為目標的新專案。 如需詳細資訊，請參閱[Web Sites 的 .NET Framework 目標](https://msdn.microsoft.com/library/bb398791(v=vs.100).aspx)。

> [!div class="step-by-step"]
> [上一篇](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
