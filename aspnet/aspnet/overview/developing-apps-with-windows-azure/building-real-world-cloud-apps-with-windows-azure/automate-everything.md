---
uid: aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
title: 自動化所有作業（使用 Azure 建立真實世界的雲端應用程式） |Microsoft Docs
author: MikeWasson
description: 使用 Azure 電子書建立真實世界的雲端應用程式，是以 Scott Guthrie 所開發的簡報為基礎。 它會說明13個模式和實務，
ms.author: riande
ms.date: 06/12/2014
ms.assetid: ba6e6baa-9b9f-471f-b39d-b007a3addadc
msc.legacyurl: /aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/automate-everything
msc.type: authoredcontent
ms.openlocfilehash: e741a753a36ebdaefbff8eee0b38911785c716ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78584942"
---
# <a name="automate-everything-building-real-world-cloud-apps-with-azure"></a>自動化所有作業（使用 Azure 建立真實世界的雲端應用程式）

由[Mike Wasson](https://github.com/MikeWasson)， [Rick Anderson](https://twitter.com/RickAndMSFT)， [Tom 作者: dykstra](https://github.com/tdykstra)

[下載 Fix It 專案](https://code.msdn.microsoft.com/Fix-It-app-for-Building-cdd80df4)或[下載電子書](https://blogs.msdn.com/b/microsoft_press/archive/2014/07/23/free-ebook-building-cloud-apps-with-microsoft-azure.aspx)

> **使用 Azure 電子書建立真實世界的雲端應用程式**，是以 Scott Guthrie 所開發的簡報為基礎。 其中說明13種模式和作法，可協助您成功開發雲端 web 應用程式。 如需電子書的簡介，請參閱[第一章](introduction.md)。

我們會查看的前三個模式實際上適用于任何軟體發展專案，但特別是雲端專案。 此模式是關於自動化開發工作。 這是很重要的主題，因為手動進程的速度很慢且容易出錯;盡可能自動化這些功能，有助於設定快速、可靠且敏捷的工作流程。 這對雲端開發而言是唯一重要的，因為您可以輕鬆地自動化許多難以或無法在內部部署環境中自動執行的工作。 例如，您可以設定整個測試環境，包括新的 web 伺服器和後端 Vm、資料庫、blob 儲存體（檔案儲存體）、佇列等。

## <a name="devops-workflow"></a>DevOps 工作流程

越來越多您聽過「DevOps」一詞。 本詞彙的開發目的是要整合開發和操作工作，以便有效率地開發軟體。 您想要啟用的工作流程類型是您可以開發應用程式、加以部署、從生產環境使用方式學習、變更它以回應您所學的內容，以及快速且可靠地重複此週期。

某些成功的雲端開發小組會一天多次部署到即時環境。 每隔2-3 個月就會用來部署主要更新的 Azure 團隊，但現在它會每隔2-3 天發行次要更新，並每隔2-3 周釋放一次主要版本。 進入該步調可説明您回應客戶的意見反應。

若要這麼做，您必須啟用可重複、可靠且可預測的開發和部署週期，並提供低週期時間。

![DevOps 工作流程](automate-everything/_static/image1.png)

換句話說，您對於某項功能的想法，以及客戶使用它和提供意見反應的時間，都必須盡可能縮短。 前三個模式-自動化所有專案、原始檔控制、持續整合和傳遞--都是我們建議的最佳作法，以便啟用這種程式。

## <a name="azure-management-scripts"></a>Azure 管理腳本

在[這篇電子書的簡介](introduction.md)中，您看到了 Azure 管理入口網站的網頁型主控台。 管理入口網站可讓您監視及管理您已在 Azure 上部署的所有資源。 這是建立和刪除服務的簡單方式，例如 web 應用程式和 Vm、設定這些服務、監視服務作業等等。 這是很棒的工具，但使用它是手動程式。 如果您要開發任何規模的實際執行應用程式，尤其是在小組環境中，建議您流覽入口網站 UI，以瞭解並探索 Azure，然後將重複執行的進程自動化。

您幾乎可以在管理入口網站或 Visual Studio 中手動執行的所有作業，也可以藉由呼叫 REST 管理 API 來完成。 您可以使用[Windows PowerShell](https://msdn.microsoft.com/library/windowsazure/jj156055.aspx)撰寫腳本，也可以使用開放原始碼架構，例如[Chef](http://www.opscode.com/chef/)或[Puppet](http://puppetlabs.com/puppet/what-is-puppet)。 您也可以在 Mac 或 Linux 環境中使用 Bash 命令列工具。 Azure 有適用于所有這些不同環境的腳本 Api，如果您想要撰寫程式碼而不是腳本，它會有[.net 管理 api](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx) 。

針對 Fix It 應用程式，我們建立了一些 Windows PowerShell 腳本，將建立測試環境的程式自動化，並將專案部署到該環境，我們將會回顧這些腳本的一些內容。

## <a name="environment-creation-script"></a>環境建立腳本

我們要探討的第一個腳本是名為*New-AzureWebsiteEnv*。 它會建立 Azure 環境，讓您可以將 Fix It 應用程式部署至進行測試。 此腳本執行的主要工作如下：

- 建立 Web 應用程式。
- 建立儲存體帳戶。 （Blob 和佇列的必要項，如您在稍後的章節中所見）。
- 建立 SQL Database 伺服器和兩個資料庫：應用程式資料庫和成員資格資料庫。
- 在 Azure 中儲存應用程式將用來存取儲存體帳戶和資料庫的設定。
- 建立將用於自動化部署的設定檔。

### <a name="run-the-script"></a>執行指令碼

> [!NOTE]
> 本章的這個部分會顯示腳本的範例，以及您輸入以執行它們的命令。 這是示範，並不提供執行腳本所需知道的一切。 如需逐步執行的作法指示，請參閱[附錄：修正 It 範例應用程式](the-fix-it-sample-application.md#deploybase)。

若要執行 PowerShell 腳本來管理 Azure 服務，您必須安裝 Azure PowerShell 主控台，並將其設定為與您的 Azure 訂用帳戶搭配運作。 設定好之後，您可以使用如下的命令來執行修正 It 環境建立腳本：

`.\New-AzureWebsiteEnv.ps1 -Name <websitename> -SqlDatabasePassword <password>`

`Name` 參數會指定建立資料庫和儲存體帳戶時所要使用的名稱，而 `SqlDatabasePassword` 參數會指定將針對 SQL Database 所建立之系統管理員帳戶的密碼。 您可以使用其他參數，我們將在稍後討論。

![PowerShell 視窗](automate-everything/_static/image2.png)

腳本完成之後，您可以在管理入口網站中看到所建立的內容。 您會發現兩個資料庫：

![資料庫](automate-everything/_static/image3.png)

儲存體帳戶：

![儲存體帳戶](automate-everything/_static/image4.png)

和 web 應用程式：

![網站](automate-everything/_static/image5.png)

在 web 應用程式的 [**設定**] 索引標籤上，您可以看到它已為 [修正 it] 應用程式設定 [儲存體帳戶設定] 和 [SQL database 連接字串]。

![appSettings 和 connectionStrings](automate-everything/_static/image6.png)

[*自動化*] 資料夾現在也包含一個 *&lt;websitename&gt;. .pubxml*檔案。 這個檔案會儲存 MSBuild 將用來將應用程式部署至剛建立之 Azure 環境的設定。 例如:

[!code-xml[Main](automate-everything/samples/sample1.xml)]

如您所見，腳本已建立一個完整的測試環境，而整個程式在大約90秒內完成。

如果您小組中的其他人想要建立測試環境，他們只要執行腳本就可以了。 不僅快速，而且也可以確信他們使用的環境與您所使用的環境完全相同。 如果每個人都是使用入口網站 UI 來手動設定專案，您就無法放心。

### <a name="a-look-at-the-scripts"></a>查看腳本

實際上，有三個腳本可執行此工作。 您可以從命令列呼叫一個，它會自動使用其他兩個來執行一些工作：

- *New-AzureWebSiteEnv*是主要的腳本。

    - *New-AzureStorage*會建立儲存體帳戶。
    - *New-AzureSql*會建立資料庫。

### <a name="parameters-in-the-main-script"></a>主要腳本中的參數

主要腳本*New-AzureWebSiteEnv*會定義數個參數：

[!code-powershell[Main](automate-everything/samples/sample2.ps1)]

需要兩個參數：

- 腳本建立的 web 應用程式名稱。 （這也用於 URL： `<name>.azurewebsites.net`）。
- 腳本所建立之資料庫伺服器的新系統管理使用者密碼。

選擇性參數可讓您指定資料中心位置（預設為「美國西部」）、資料庫伺服器管理員名稱（預設為 "dbuser"），以及資料庫伺服器的防火牆規則。

### <a name="create-the-web-app"></a>建立 Web 應用程式

腳本的第一件事是藉由呼叫 `New-AzureWebsite` Cmdlet 來建立 web 應用程式，並將 web 應用程式名稱和位置參數值傳入其中：

[!code-powershell[Main](automate-everything/samples/sample3.ps1?highlight=2)]

### <a name="create-the-storage-account"></a>建立儲存體帳戶

然後，主要腳本會執行*New-AzureStorage*腳本，並針對儲存體帳戶名稱指定 " *&lt;websitename&gt;* storage"，並為 web 應用程式指定相同的資料中心位置。

[!code-powershell[Main](automate-everything/samples/sample4.ps1?highlight=3)]

*New-AzureStorage*會呼叫 `New-AzureStorageAccount` Cmdlet 來建立儲存體帳戶，並傳回帳戶名稱和存取金鑰值。 應用程式將需要這些值，才能存取儲存體帳戶中的 blob 和佇列。

[!code-powershell[Main](automate-everything/samples/sample5.ps1?highlight=2)]

您可能不一定會想要建立新的儲存體帳戶;您可以藉由新增可選擇性地指示其使用現有儲存體帳戶的參數，來增強腳本。

### <a name="create-the-databases"></a>建立資料庫

然後，主要腳本會在設定預設資料庫和防火牆規則名稱之後，執行資料庫建立腳本*New-AzureSql*：

[!code-powershell[Main](automate-everything/samples/sample6.ps1)]

[!code-powershell[Main](automate-everything/samples/sample7.ps1?highlight=2)]

資料庫建立腳本會抓取開發電腦的 IP 位址，並設定防火牆規則，讓開發電腦能夠連接及管理伺服器。 接著，資料庫建立腳本會經歷數個步驟來設定資料庫：

- 使用 `New-AzureSqlDatabaseServer` Cmdlet 建立伺服器。

    [!code-powershell[Main](automate-everything/samples/sample8.ps1?highlight=1)]
- 建立防火牆規則，讓開發電腦能夠管理伺服器，以及讓 web 應用程式連線到它。 

    [!code-powershell[Main](automate-everything/samples/sample9.ps1?highlight=3,5)]
- 使用 `New-AzureSqlDatabaseServerContext` Cmdlet，建立包含伺服器名稱和認證的資料庫內容。

    [!code-powershell[Main](automate-everything/samples/sample10.ps1?highlight=4)]

    `New-PSCredentialFromPlainText` 是腳本中的函式，會呼叫 `ConvertTo-SecureString` Cmdlet 來加密密碼，並傳回 `PSCredential` 物件，這與 `Get-Credential` Cmdlet 所傳回的類型相同。
- 使用 `New-AzureSqlDatabase` Cmdlet，建立應用程式資料庫和成員資格資料庫。

    [!code-powershell[Main](automate-everything/samples/sample11.ps1?highlight=2,5)]
- 呼叫本機定義的函數，以建立每個資料庫的連接字串。 應用程式會使用這些連接字串來存取資料庫。 

    [!code-powershell[Main](automate-everything/samples/sample12.ps1?highlight=1-2)]

    SQLAzureDatabaseConnectionString 是腳本中定義的函式，它會從提供給它的參數值建立連接字串。

    [!code-powershell[Main](automate-everything/samples/sample13.ps1?highlight=1)]
- 傳回具有資料庫伺服器名稱和連接字串的雜湊表。

    [!code-powershell[Main](automate-everything/samples/sample14.ps1)]

修正 It 應用程式會使用不同的成員資格和應用程式資料庫。 您也可以將成員資格和應用程式資料都放在單一資料庫中。

### <a name="store-app-settings-and-connection-strings"></a>儲存應用程式設定和連接字串

Azure 有一項功能，可讓您儲存設定和連接字串，以在嘗試讀取 Web.config 檔案中的 `appSettings` 或 `connectionStrings` 集合時，自動覆寫傳回給應用程式的內容。 當您部署時，這是套用[web.config 轉換](../../../../web-forms/overview/deployment/visual-studio-web-deployment/web-config-transformations.md)的替代方法。 如需詳細資訊，請參閱本電子書後面的[將敏感性資料儲存在 Azure](source-control.md#appsettings)中。

環境建立腳本會將應用程式在 Azure 中執行時所需的所有 `appSettings` 和 `connectionStrings` 值儲存在 Azure 中，以存取儲存體帳戶和資料庫。

[!code-powershell[Main](automate-everything/samples/sample15.ps1)]

[!code-powershell[Main](automate-everything/samples/sample16.ps1)]

[!code-powershell[Main](automate-everything/samples/sample17.ps1?highlight=2)]

[新的 new relic](http://newrelic.com/)是我們在[監視和遙測](monitoring-and-telemetry.md)一章中示範的遙測架構。 環境建立腳本也會重新開機 web 應用程式，以確保它會挑選新的 New relic 設定。

[!code-powershell[Main](automate-everything/samples/sample18.ps1?highlight=2)]

### <a name="preparing-for-deployment"></a>準備部署

在程式結束時，環境建立腳本會呼叫兩個函數來建立部署腳本將使用的檔案。

其中一個函式會建立發行設定檔 *（&lt;websitename&gt;. .pubxml*檔案）。 程式碼會呼叫 Azure REST API 來取得發行設定，並將資訊儲存在 *.publishsettings*檔案中。 然後，它會使用該檔案中的資訊以及範本檔案（ *.pubxml*）來建立包含發行設定檔的 *.pubxml*檔案。 這個兩步驟的程式會模擬您在 Visual Studio 中執行的作業：下載 *.publishsettings*檔案，並匯入以建立發行設定檔。

另一個函式會使用另一個範本檔案（網站-環境範本）來建立*website-environment*檔案，其中包含部署腳本將與 *.pubxml*檔案搭配使用的設定。

### <a name="troubleshooting-and-error-handling"></a>疑難排解和錯誤處理

腳本就像程式一樣：它們可能會失敗，而且當您想要知道失敗的最大程度和造成問題的原因時。 基於這個理由，環境建立腳本會將 `VerbosePreference` 變數的值從 `SilentlyContinue` 變更為 `Continue`，以便顯示所有詳細資訊訊息。 它也會將 `ErrorActionPreference` 變數的值從 `Continue` 變更為 `Stop`，讓腳本即使在遇到非終止錯誤時也會停止：

[!code-powershell[Main](automate-everything/samples/sample19.ps1)]

在執行任何工作之前，腳本會儲存開始時間，讓它能夠計算完成的已耗用時間：

[!code-powershell[Main](automate-everything/samples/sample20.ps1)]

完成工作之後，腳本會顯示經過時間：

[!code-powershell[Main](automate-everything/samples/sample21.ps1)]

針對每個金鑰作業，腳本會寫入詳細資訊訊息，例如：

[!code-powershell[Main](automate-everything/samples/sample22.ps1)]

## <a name="deployment-script"></a>部署指令碼

*New-AzureWebsiteEnv*腳本在建立環境時所執行的工作， *Publish-AzureWebsite*腳本會進行應用程式部署。

部署腳本會從環境建立腳本所建立的*website-environment*中，取得 web 應用程式的名稱。

[!code-powershell[Main](automate-everything/samples/sample23.ps1)]

它會從 *.publishsettings*檔案取得部署使用者密碼：

[!code-powershell[Main](automate-everything/samples/sample24.ps1)]

它會執行[MSBuild](http://msbuildbook.com/)命令來建立及部署專案：

[!code-powershell[Main](automate-everything/samples/sample25.ps1)]

如果您已在命令列上指定 `Launch` 參數，它會呼叫 `Show-AzureWebsite` Cmdlet，將您的預設瀏覽器開啟至網站 URL。

[!code-powershell[Main](automate-everything/samples/sample26.ps1?highlight=3)]

您可以使用如下的命令來執行部署腳本：

`.\Publish-AzureWebsite.ps1 ..\MyFixIt\MyFixIt.csproj -Launch`

完成後，瀏覽器會開啟，並在 `<websitename>.azurewebsites.net` URL 的雲端中執行網站。

![修正部署至 Windows Azure 的 It 應用程式](automate-everything/_static/image7.png)

## <a name="summary"></a>總結

使用這些腳本，您可以確信相同的步驟一律會使用相同的循序執行相同的訂單。 這有助於確保小組中的每位開發人員都不會錯過任何東西，或在自己的電腦上部署自訂專案，而在另一個小組成員的環境或實際執行時，實際上無法以相同的方式運作。

同樣地，您可以使用 REST API、Windows PowerShell 腳本、.NET 語言 API 或可在 Linux 或 Mac 上執行的 Bash 公用程式，將您可以在管理入口網站中執行的大部分 Azure 管理功能自動化。

在[下一章](source-control.md)中，我們將探討原始程式碼，並說明在原始程式碼存放庫中包含腳本是很重要的。

## <a name="resources"></a>資源

- [安裝和設定適用于 Azure 的 Windows PowerShell](https://docs.microsoft.com/powershell/azure/overview?view=azurermps-4.3.1)。 說明如何安裝 Azure PowerShell Cmdlet，以及如何在您的電腦上安裝所需的憑證，以便管理您的 Azure 帳戶。 這是開始使用的絕佳位置，因為它也有可供學習 PowerShell 本身的資源連結。
- [Azure 腳本中心](https://docs.microsoft.com/azure/automation/automation-runbook-gallery)。 WindowsAzure.com 入口網站來開發可管理 Azure 服務的腳本，並提供入門教學課程的連結、Cmdlet 參考檔和原始程式碼，以及範例腳本
- [週末腳本：使用 Azure 和 PowerShell 消費者入門](https://blogs.technet.com/b/heyscriptingguy/archive/2013/06/22/weekend-scripter-getting-started-with-windows-azure-and-powershell.aspx)。 在 Windows PowerShell 專用的 blog 中，這篇文章提供了使用 PowerShell 來進行 Azure 管理功能的絕佳簡介。
- [安裝和設定 Azure 跨平臺命令列介面](https://docs.microsoft.com/cli/azure/install-azure-cli?view=azure-cli-latest)。 適用于 Mac 和 Linux 以及 Windows 系統的 Azure 腳本架構快速入門教學課程。
- [命令列工具區段：下載 Azure sdk 和工具主題](https://azure.microsoft.com/downloads/)。 適用于 Azure 命令列工具相關檔和下載的入口網站頁面。
- [使用 Azure 管理庫和 .NET 將一切自動化](http://www.hanselman.com/blog/PennyPinchingInTheCloudAutomatingEverythingWithTheWindowsAzureManagementLibrariesAndNET.aspx)。 Scott Hanselman 引進了適用于 Azure 的 .NET 管理 API。
- [使用 Windows PowerShell 指令碼來發行至開發和測試環境](https://msdn.microsoft.com/library/azure/dn642480.aspx)。 說明如何使用 Visual Studio 自動為 Web 專案產生之發佈腳本的 MSDN 檔。
- [PowerShell Tools for Visual Studio 2013](https://visualstudiogallery.msdn.microsoft.com/c9eb3ba8-0c59-4944-9a62-6eee37294597)。 Visual Studio 延伸模組，可在 Visual Studio 中新增 Windows PowerShell 的語言支援。

> [!div class="step-by-step"]
> [上一頁](introduction.md)
> [下一頁](source-control.md)
