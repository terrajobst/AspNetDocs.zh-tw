---
uid: web-forms/overview/deployment/visual-studio-web-deployment/introduction
title: 使用 Visual Studio ASP.NET Web 部署：簡介 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何使用 V ...，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: 24ad086d-865e-433c-9ac9-05f1a553da16
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/introduction
msc.type: authoredcontent
ms.openlocfilehash: 96dd31d949633e001fc595621bedbf74e98000fc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74640228"
---
# <a name="aspnet-web-deployment-using-visual-studio-introduction"></a>使用 Visual Studio ASP.NET Web 部署：簡介

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何搭配 Azure SDK for .NET 使用 Visual Studio 2012，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。 大部分的程式與 Visual Studio 2013 類似。
> 
> 您可以開發 web 應用程式，以便透過網際網路提供給其他人使用。 但是，web 程式設計教學課程通常會在向您示範如何讓您的開發電腦上運作，而立即停止。 這一系列的教學課程會從其他人離開：您已建立 web 應用程式並加以測試，並已準備好開始使用。 後續步驟 這些教學課程示範如何在本機開發電腦上，先部署到 IIS 進行測試，然後再部署到 Azure 或協力廠商主機服務提供者以進行預備和生產環境。 您將部署的範例應用程式是使用 Entity Framework、SQL Server 和 ASP.NET 成員資格系統的 web 應用程式專案。 範例應用程式會使用 ASP.NET Web Forms，但所顯示的程式也適用于 ASP.NET MVC 和 Web API。
> 
> 這些教學課程假設您知道如何在 Visual Studio 中使用 ASP.NET。 如果您沒有這麼做，最好的起點是[基本的 ASP.NET Web Form 教學](../../older-versions-getting-started/tailspin-spyworks/tailspin-spyworks-part-1.md)課程或[基本的 ASP.NET MVC 教學](../../../../mvc/overview/older-versions/getting-started-with-aspnet-mvc4/intro-to-aspnet-mvc-4.md)課程。
> 
> 如果您有與本教學課程不直接相關的問題，您可以將其張貼至[ASP.NET 部署論壇](https://forums.asp.net/26.aspx/1?Configuration+and+Deployment)或[StackOverflow](http://stackoverflow.com)。
> 
> 本內容也可以在[TechNet 電子書圖庫](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#ASPNETWebDeploymentusingVisualStudio)中取得免費的電子書。

## <a name="overview"></a>概觀

這些教學課程會引導您部署 ASP.NET web 應用程式，其中包含 SQL Server 資料庫。 您會先部署到本機開發電腦上的 IIS 進行測試，然後在 Azure App Service 和 Azure SQL Database 進行預備和生產環境的 Web Apps。 您將瞭解如何使用 Visual Studio 單鍵發佈來部署，而您將瞭解如何使用命令列進行部署。

教學課程的數目可能會讓部署程式看起來很困難。 事實上，基本程式很簡單。 不過，在真實世界的情況下，您通常需要執行額外的部署工作，例如，在目標伺服器上設定資料夾許可權。 我們已經說明了其中一些額外的工作，希望教學課程不會省略可能會讓您無法成功部署實際應用程式的資訊。

教學課程的設計是依序執行，而且每個元件都是在上一個部分建立。 您可以略過與您的情況無關的部分，但您可能需要在稍後的教學課程中調整這些程式。

## <a name="intended-audience"></a>目標物件

這些教學課程的目標是在下列環境中工作的 ASP.NET 開發人員：

- 生產環境 Azure App Service Web Apps 或協力廠商主機服務提供者。
- 部署不限於持續整合程式，但可以直接從 Visual Studio 完成。

這些教學課程中不涵蓋使用[持續傳遞](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)程式從[原始檔控制](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control.md)進行部署，除了一個示範如何從命令列部署的教學課程。 如需持續傳遞的詳細資訊，請參閱下列資源：

- [持續整合與持續傳遞（使用 Windows Azure 建立真實世界的雲端應用程式）](../../../../aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery.md)
- [在 Azure App Service 中部署 web 應用程式](https://azure.microsoft.com/documentation/articles/web-sites-deploy/)
- [在企業案例中部署 Web 應用程式](../deploying-web-applications-in-enterprise-scenarios/deploying-web-applications-in-enterprise-scenarios.md)（針對 Visual Studio 2010 撰寫的一組較舊的教學課程，對於企業環境仍然具有有用的資訊）。

## <a name="using-a-third-party-hosting-provider"></a>使用協力廠商主機服務提供者

本教學課程會引導您完成設定 Azure 帳戶，以及將應用程式部署至預備和生產 Azure App Service 中 Web Apps 的流程。 不過，您可以使用相同的基本程式部署至您選擇的協力廠商主控提供者。 其中，教學課程會透過 Azure 獨有的程式來說明，並建議您在協力廠商主機服務提供者上可預期的差異。

## <a name="deploying-web-app-projects"></a>部署 web 應用程式專案

您為這些教學課程下載並部署的範例應用程式是 Visual Studio web 應用程式專案。 不過，如果您安裝 Visual Studio 的最新 Web 發佈更新，您可以針對 Web 應用程式專案使用相同的部署方法和工具。

## <a name="deploying-aspnet-mvc-projects"></a>部署 ASP.NET MVC 專案

範例應用程式是 ASP.NET Web form 專案，但您瞭解如何執行的每一項動作也適用于 ASP.NET MVC。 Visual Studio MVC 專案只是另一種形式的 web 應用程式專案。 唯一的不同之處在于，如果您要部署至不支援 ASP.NET MVC 或目標版本的主控提供者，您必須確定您已在專案中安裝適當的（[mvc 3](http://nuget.org/packages/AspNetMvc/3.0.20105.0)、 [Mvc 4](http://www.nuget.org/packages/Microsoft.AspNet.Mvc/4.0.30506.0)或[mvc 5](http://www.nuget.org/packages/Microsoft.AspNet.Mvc)） NuGet 套件。

## <a name="programming-language"></a>程式設計語言

範例應用程式會C#使用C#，但教學課程不需要知識，而教學課程所顯示的部署技巧則不是語言特定的。

## <a name="database-deployment-methods"></a>資料庫部署方法

有三種方式可讓您在 Visual Studio 中部署 SQL Server 資料庫以及 web 部署：

- Entity Framework Code First 移轉
- DbDacFx Web Deploy 提供者
- DbFullSql Web Deploy 提供者

在本教學課程中，您將使用這些方法的前兩個。 DbFullSql Web Deploy 提供者是舊版的方法，除了某些特定案例（例如從 SQL Server Compact 遷移至 SQL Server 以外），不再建議使用。

本教學課程中所顯示的方法適用于 SQL Server 資料庫，而不是 SQL Server Compact。 如需有關如何部署 SQL Server Compact 資料庫的詳細資訊，請參閱[使用 SQL Server Compact Visual Studio Web 部署](../../older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-introduction-1-of-12.md)。

本教學課程中所顯示的方法會要求您使用 Web Deploy publish 方法。 如果您偏好使用不同的發佈方法（例如 FTP、檔案系統或 FPSE），請參閱 Visual Studio 和 ASP.NET 的 Web 部署內容對應中的[部署與 web 應用程式部署分開的資料庫](https://go.microsoft.com/fwlink/p/?LinkId=282413#databaseseparate)。

### <a name="entity-framework-code-first-migrations"></a>Entity Framework Code First 移轉

在 Entity Framework 版本4.3 中，Microsoft 引進 Code First 移轉。 Code First 移轉會自動化對資料模型進行累加式變更，並將這些變更傳播至資料庫的程式。 在舊版的 Code First 中，您通常會讓 Entity Framework 在每次變更資料模型時，卸載並重新建立資料庫。 這不是開發的問題，因為可以輕鬆地重新建立測試資料，但在生產環境中，您通常會想要更新資料庫架構，而不需卸載資料庫。 「遷移」功能可讓 Code First 更新資料庫，而不需要卸載再重新建立。 您可以讓 Code First 自動決定如何進行必要的架構變更，或者您可以撰寫程式碼來自訂變更。 如需 Code First 移轉的簡介，請參閱[Code First 移轉](https://msdn.microsoft.com/library/hh770484.aspx)。

當您部署 Web 專案時，Visual Studio 可以自動化部署 Code First 移轉所管理之資料庫的程式。 當您建立發行設定檔時，您會選取標示為 執行 Code First 移轉（在應用程式啟動時執行）的核取方塊。 這項設定會導致部署程式在目的地伺服器上自動設定應用程式的 web.config 檔案，讓 Code First 使用 `MigrateDatabaseToLatestVersion` 初始化運算式類別。

Visual Studio 在部署過程中不會對資料庫執行任何動作。 當部署的應用程式在部署後第一次存取資料庫時，Code First 會自動建立資料庫，或將資料庫架構更新為最新版本。 如果應用程式會執行遷移種子方法，此方法會在建立資料庫或更新架構之後執行。

在本教學課程中，您將使用 Code First 移轉來部署應用程式資料庫。

### <a name="the-dbdacfx-web-deploy-provider"></a>DbDacFx Web Deploy 提供者

針對不是由 Entity Framework Code First 管理的 SQL Server 資料庫，您可以在設定發行設定檔時，選取標示為 [更新資料庫] 的核取方塊。 在初始部署期間，dbDacFx 提供者會在目的地資料庫中建立資料表和其他資料庫物件，以符合源資料庫。 在後續的部署中，提供者會決定來源與目的地資料庫之間的差異，並更新目的地資料庫的架構，使其符合源資料庫。 根據預設，提供者不會進行任何會造成資料遺失的變更，例如當卸載資料表或資料行時。

這個方法不會將資料庫資料表中的資料部署自動化，但是您可以建立腳本來執行這項作業，並設定 Visual Studio 在部署期間執行它們。 在部署期間執行腳本的另一個原因是進行無法自動完成的架構變更，因為它們會造成資料遺失。

在本教學課程中，您將使用 dbDacFx 提供者來部署 ASP.NET 成員資格資料庫。

## <a name="troubleshooting-during-this-tutorial"></a>本教學課程期間的疑難排解

當部署期間發生錯誤，或部署的網站未正確執行時，錯誤訊息不一定會提供明顯的解決方案。 為了協助您處理一些常見的問題，您可以使用[疑難排解參考頁面](troubleshooting.md)。 如果您在進行教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解] 頁面。

## <a name="comments-welcome"></a>歡迎留言

歡迎您提供教學課程的批註，而更新教學課程時，將會針對教學課程批註中提供的改進進行修正或建議。

<a id="prerequisites"></a>

## <a name="prerequisites"></a>必要條件：

本教學課程是針對下列產品所撰寫：

- Windows 8 或 Windows 7。
- Visual Studio 2012 或 Visual Studio 2012 Express for Web 含[最新的更新](https://go.microsoft.com/fwlink/?LinkId=272486)。
- [適用于 Visual Studio 2012 的 Azure SDK](https://go.microsoft.com/fwlink/?LinkId=254364)

您可以使用 Visual Studio 2010 SP1 或 Visual Studio 2013 來遵循本教學課程，但某些螢幕擷取畫面會有所不同，而且有些功能會有所不同。

如果您使用 Visual Studio 2013，請安裝[適用于 Visual Studio 2013 的 AZURE SDK](https://go.microsoft.com/fwlink/?LinkID=324322)。

如果您使用的是 Visual Studio 2010 SP1，請安裝下列軟體：

- [適用于 Visual Studio 2010 的 Azure SDK](https://go.microsoft.com/fwlink/?LinkID=254269)
- [SQL Server Express LocalDB](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=SQLLocalDBOnly_11_0)
- [SQL Server Data Tools](https://msdn.microsoft.com/library/hh500335.aspx)。

根據您的電腦上已有多少 SDK 相依性而定，安裝 Azure SDK 可能需要很長的時間（從數分鐘到半小時以上）。 即使您打算發行至協力廠商主機服務提供者，而不是 Azure，您也需要 Azure SDK，因為 SDK 包含 Visual Studio web 發佈功能的最新更新。

> [!NOTE]
> 本教學課程是使用 Azure SDK 的版本1.8.1 所撰寫。 因為已發行具有額外功能的較新版本。 這些教學課程已更新為提及這些功能，並連結至有詳細資訊的資源。

指示和螢幕擷取畫面是以 Windows 8 為基礎，但教學課程會說明 Windows 7 的差異。

需要其他軟體才能完成本教學課程，但您還不需要安裝。 本教學課程將逐步引導您在需要時進行安裝的步驟。

## <a name="download-the-sample-application"></a>下載範例應用程式

您將部署的應用程式名稱為 Contoso 大學，而且已經為您建立。 這是一個簡化版的大學網站，以鬆散于[ASP.NET 網站上 Entity Framework 教學](https://asp.net/entity-framework/tutorials)課程中所述的 Contoso 大學應用程式為基礎。

當您已安裝必要條件時，請下載[Contoso 大學 web 應用程式](https://go.microsoft.com/fwlink/p/?LinkId=282627)。 *.Zip*檔案包含多個版本的專案。 若要逐步執行教學課程的步驟，請從位於C#資料夾中的專案開始。 若要在教學課程結束時查看專案的外觀，請在 ContosoUniversity-End 資料夾中開啟專案。

若要準備專案以進行教學課程步驟，請執行下列步驟：

1. 在您用來處理 Visual Studio 專案C#的任何資料夾中，將 ContosoUniversity 方案檔案從名為 ContosoUniversity 的資料夾中儲存。

    根據預設，這是 Visual Studio 2012 的下列資料夾：

    `C:\Users\<username>\Documents\Visual Studio 2012\Projects`

    （針對本教學課程中的螢幕擷取畫面，專案資料夾位於 `C`：磁片磁碟機的根目錄中）。
2. 啟動 Visual Studio 並開啟專案。
3. 在**方案總管**中，以滑鼠右鍵按一下方案，然後按一下 [ **EnableNuGet 套件還原**]。
4. 建置方案。
5. 如果您遇到編譯錯誤，請手動還原 NuGet 套件：

    1. 在**方案總管**中，以滑鼠右鍵按一下方案，然後按一下 [**管理方案的 NuGet 套件**]。
    2. 在 [**管理 NuGet 套件**] 對話方塊的頂端，您會看到**此解決方案缺少部分 NuGet 套件。按一下以還原。** 按一下 [**還原**] 按鈕。
    3. 重建方案。
6. 按 CTRL-F5 執行應用程式。

    應用程式會開啟至 Contoso 大學首頁。

    ![首頁開發](introduction/_static/image1.png)

    （在 Visual Studio 啟動 SQL Server Express LocalDB 實例時可能會有等候時間，如果該進程花費太多時間，您可能會收到逾時錯誤。 在這種情況下，只要重新開機專案即可。）

網站頁面可從功能表列存取，並可讓您執行下列功能：

- 顯示學生統計資料（[關於] 頁面）。
- 顯示、編輯、刪除及新增學生。
- 顯示和編輯課程。
- 顯示和編輯講師。
- 顯示和編輯部門。

以下是幾個代表性頁面的螢幕擷取畫面。

![學生頁面開發](introduction/_static/image2.png)

![新增學生頁面 Dev](introduction/_static/image3.png)

## <a name="review-application-features-that-affect-deployment"></a>審查會影響部署的應用程式功能

應用程式的下列功能會影響您部署它的方式，或是您必須如何部署它。 本系列的下列教學課程會更詳細地說明每一項。

- Contoso 大學會使用 SQL Server 資料庫來儲存應用程式資料，例如學生和講師姓名。 資料庫包含測試資料與生產資料的混合，而且當您部署到生產環境時，您需要排除測試資料。
- 應用程式會使用 ASP.NET 成員資格系統，將使用者帳戶資訊儲存在 SQL Server 資料庫中。 應用程式會定義可存取某些受限制資訊的系統管理員使用者。 您需要部署成員資格資料庫，但不含測試帳戶，而是使用系統管理員帳戶。
- 應用程式會使用協力廠商的錯誤記錄和報告公用程式。 這個公用程式是在必須與應用程式一起部署的元件中提供。
- 錯誤記錄公用程式會將 XML 檔案中的錯誤資訊寫入檔案資料夾。 您必須確定 ASP.NET 在部署的網站中執行的帳戶具有此資料夾的寫入權限，而且您必須從部署中排除此資料夾。 （否則，測試環境中的錯誤記錄檔資料可能會部署到生產和/或生產錯誤記錄檔）。
- 應用程式包含一些必須在部署的*web.config*檔案中變更的設定，視目的地環境（測試、預備或生產）而定，以及必須根據組建設定（Debug 或 Release）變更的其他設定而定。
- Visual Studio 解決方案包含類別庫專案。 只應部署此專案所產生的元件，而不是專案本身。

## <a name="summary"></a>總結

在此系列的第一個教學課程中，您已下載 Visual Studio 專案的範例，以及會影響您如何部署應用程式的網站功能。 在下列教學課程中，您會設定要自動處理的某些專案，以準備進行部署。 您手動處理的其他人。

> [!div class="step-by-step"]
> [下一步](preparing-databases.md)
