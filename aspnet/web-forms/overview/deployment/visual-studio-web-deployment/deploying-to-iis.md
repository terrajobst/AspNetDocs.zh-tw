---
uid: web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
title: 使用 Visual Studio ASP.NET Web 部署：部署至測試 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 01/16/2019
ms.assetid: 8bf2c4fb-4ee5-4841-bfc2-03462c1f7a7a
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/deploying-to-iis
msc.type: authoredcontent
ms.openlocfilehash: 738318cce442fdc5d58dd1e4c992d4941be2487e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74591247"
---
# <a name="aspnet-web-deployment-using-visual-studio-deploying-to-test"></a>使用 Visual Studio ASP.NET Web 部署：部署到測試環境

由[Tom 作者: dykstra](https://github.com/tdykstra)

本教學課程系列說明如何使用 Visual Studio 2017，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

如需部署至 Azure 的最新版本，請參閱[在 azure 中建立 ASP.NET Core web 應用程式](/azure/app-service/app-service-web-get-started-dotnet)。

## <a name="overview"></a>總覽

在本教學課程中，您會將 ASP.NET web 應用程式部署到本機電腦上的 Internet information Server （IIS）。

一般而言，當您開發應用程式時，您會執行它並在 Visual Studio 中進行測試。 根據預設，Visual Studio 2017 中的 web 應用程式專案會使用 IIS Express 作為開發 web 伺服器。 IIS Express 的行為比 Visual Studio 程式開發伺服器（也稱為 Cassini）更像是完整的 IIS，Visual Studio 2017 預設使用。 但這兩種開發 web 伺服器的運作方式都與 IIS 完全一樣。 因此，應用程式可以在 Visual Studio 中正確執行和測試，但在部署到 IIS 時失敗。

您可以透過兩種方式可靠地測試您的應用程式：

1. 使用您稍後將用來部署至生產環境的相同程式，將您的應用程式部署到開發電腦上的 IIS。

   當您執行 Web 專案時，可以將 Visual Studio 設定為使用 IIS，但這樣做並不會測試您的部署流程。 這個方法會驗證您的部署程式，而且您的應用程式會在 IIS 底下正確執行。

2. 將您的應用程式部署至類似您生產環境的測試環境。 
 
   這些教學課程的生產環境會在 Azure App Service 中 Web Apps。 理想的測試環境是在 Azure 服務中建立的額外 web 應用程式。 雖然它會以與生產 web 應用程式相同的方式來設定，但您只會使用它來進行測試。

選項2是最可靠的測試方式。 如果您使用選項2，則不一定需要使用選項1。 不過，如果您要部署到協力廠商主機服務提供者，選項2可能不可行或成本很高，因此本教學課程系列會顯示這兩種方法。 [部署至生產環境](deploying-to-production.md)教學課程中提供選項2的指引。

如需在 Visual Studio 中使用 web 伺服器的詳細資訊，請參閱[Visual Studio 中 ASP.NET Web 專案的 Web 服務器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。

一下如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。

## <a name="download-the-contoso-university-starter-project"></a>下載 Contoso 大學入門專案

下載並安裝 Contoso 大學 Visual Studio starter 解決方案和專案。 此解決方案包含已完成的教學課程。 

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

## <a name="install-iis"></a>安裝 IIS

若要部署至開發電腦上的 IIS，請確認已安裝 IIS 和 Web Deploy。 根據預設，Visual Studio 會安裝 Web Deploy，但 IIS 並未包含在預設的 Windows 10、Windows 8 或 Windows 7 設定中。 如果您已經安裝 IIS，而且預設應用程式集區已設定為 .NET 4，請跳到[下一節](#sqlexpress)。

1. 建議您使用[Web Platform Installer （download-wpi）](https://www.microsoft.com/web/downloads/platform.aspx)來安裝 IIS 和 Web Deploy。 DOWNLOAD-WPI 會安裝建議的 IIS 設定，其中包含 IIS 並在必要時 Web Deploy 必要條件。

   如果您已安裝 IIS、Web Deploy 或其任何必要的元件，DOWNLOAD-WPI 只會安裝遺失的內容。

   * 使用 Web Platform Installer 來安裝 IIS 和 Web Deploy：
    
     ![使用 DOWNLOAD-WPI 安裝 IIS](deploying-to-iis/_static/image30.png)

     ![使用 DOWNLOAD-WPI 安裝 Web Deploy](deploying-to-iis/_static/image31.png)

     您會看到指出將會安裝 IIS 7 的訊息。 此連結適用于 Windows 8 中的 IIS 8;但是對於 Windows 8 和更新版本，請執行下列步驟，以確定已安裝 ASP.NET 4.7：

   * 開啟 [**控制台**] > **程式** > [**程式和功能**] > **開啟或關閉 Windows 功能**。

   * 展開 [ **Internet Information Services**]、[ **World Wide Web 服務**] 和 [**應用程式開發] 功能**。
   
   * 確認已選取 [ **ASP.NET 4.7** ]。

     ![選取 ASP.NET 4。7](deploying-to-iis/_static/image1a.png)

   * 確認已選取 [ **World Wide Web 服務**] 和 [ **IIS 管理主控台**]。 這會安裝 IIS 和 IIS 管理員。
    
     ![選取 World Wide Web 服務](deploying-to-iis/_static/image24.png)    
  
   * 選取 [確定]。 指出已進行安裝的對話方塊訊息隨即出現。

安裝 IIS 之後，請執行**Iis 管理員**，以確定 .NET Framework 第4版已指派給預設的應用程式集區。

1. 按 WINDOWS + R，以開啟 [**執行**] 對話方塊。

   （在 Windows 8 或更新版本上，在 [**開始**] 頁面上輸入 "run"。 在 Windows 7 中，從 [**開始**] 功能表選取 [**執行**]。 如果 [**執行**] 不在 [**開始**] 功能表中，請以滑鼠右鍵按一下工作列，然後依序選取 [**屬性**]、[**開始] 功能表**索引標籤、[**自訂**] 和 [**執行命令**]。

2. 輸入 "inetmgr"，然後選取 **[確定]** 。

3. 在 [**連線] 窗格**中，展開伺服器節點，然後選取 [**應用程式**集區]。 在 [**應用程式**集區] 窗格中，如果**DefaultAppPool**已指派給 .net framework 第4版（如下圖所示），請跳至下一節。

   ![Inetmgr_showing_4。0_app_pools](deploying-to-iis/_static/image5a.png)

4. 如果您只看到兩個應用程式集區，且兩者都設定為 .NET Framework 2.0，請在 IIS 中安裝 ASP.NET 4。

   針對 Windows 8 或更新版本，請參閱上一節的指示，以確定已安裝 ASP.NET 4.7，或參閱[如何在 windows 8 和 Windows Server 2012 上安裝 ASP.NET 4.5](https://support.microsoft.com/kb/2736284)。 若是 Windows 7，請以滑鼠右鍵按一下 Windows [**開始**] 功能表中的 [**命令提示**字元]，然後選取 [以**系統管理員身分執行**]，開啟命令提示字元視窗 執行[aspnet\_regiis](https://msdn.microsoft.com/library/k6h9cz8h.aspx) ，使用下列命令在 IIS 中安裝 ASP.NET 4。 （在32位系統中，將 "Framework64" 取代為 "Framework"）。

   [!code-console[Main](deploying-to-iis/samples/sample1.cmd)]

   此命令會建立 .NET Framework 4 的新應用程式集區，但預設的應用程式集區仍會設定為2.0。 您要將以 .NET 4 為目標的應用程式部署到該應用程式集區，因此請將應用程式集區變更為 .NET 4。

5. 如果您關閉了 [ **IIS 管理員**]，請再次執行它，展開伺服器節點，然後選取 [**應用程式**集區]。

6. 在 [**應用程式**集區] 窗格中，選取 [ **DefaultAppPool**]。 在 [**動作**] 窗格中，選取 [**基本設定**]。

   ![Inetmgr_selecting_Basic_Settings_for_app_pool](deploying-to-iis/_static/image25.png)

7. 在 [**編輯應用程式集**區] 對話方塊中，將 [ **.net clr 版本**] 變更為 [ **.net clr v 4.0.30319**]。 選取 [確定]。

   ![Selecting_。 NET_4_for_DefaultAppPool](deploying-to-iis/_static/image6a.png)

您現在已準備好將 web 應用程式發佈至 IIS。 不過，首先要建立資料庫來進行測試。

<a id="sqlexpress"></a>

## <a name="install-sql-server-express"></a>安裝 SQL Server Express

LocalDB 並非設計成在 IIS 中工作，因此您的測試環境必須安裝 SQL Server Express。 如果您使用 Visual Studio 2010 SQL Server Express，則預設已安裝。 如果您使用的是 Visual Studio 2012 或更新版本，請安裝 SQL Server Express。

若要安裝 SQL Server Express，請從 [下載中心下載並安裝它：Microsoft SQL Server 2017 Express edition](https://www.microsoft.com/sql-server/sql-server-editions-express)。 

在 SQL Server 安裝中心 的第一頁上，選取 新增  **SQL Server 獨立安裝 或 將功能新增至現有安裝**，並依照指示接受預設選項。 在安裝精靈中，接受預設設定。 如需安裝選項的詳細資訊，請參閱[從安裝精靈安裝 SQL Server （安裝程式）](https://msdn.microsoft.com/library/ms143219.aspx)。

## <a name="create-sql-server-express-databases-for-the-test-environment"></a>建立測試環境的 SQL Server Express 資料庫

Contoso 大學應用程式有兩個資料庫： 

1. 成員資格資料庫 
2. 應用程式資料庫 

您可以將這些資料庫部署到兩個不同的資料庫或單一資料庫。 結合它們可讓它們之間的資料庫聯結變得更容易。 

如果您要部署到協力廠商主機服務提供者，您的主控方案可能也會讓您有理由加以結合。 例如，提供者可能會對多個資料庫收取更多費用，或甚至不允許一個以上的資料庫。

在本教學課程中，您會在測試環境中部署至兩個資料庫，並在預備和生產環境中部署到一個資料庫。

從 Visual Studio 的 [ **View** ] 功能表中，選取 [**伺服器總管**（Visual Web Developer 中的**資料庫總管**）]。 以滑鼠右鍵按一下 [**資料連線**]，然後選取 [**建立新的 SQL Server 資料庫**]。

![Selecting_Create_New_SQL_Server_Database](deploying-to-iis/_static/image8.png)

在 [**建立新的 SQL Server 資料庫**] 對話方塊中，于 [**伺服器名稱**] 方塊中輸入 ".\SQLExpress"，並在 [**新資料庫名稱**] 方塊中輸入 "aspnet-ContosoUniversity"。 選取 [確定]。

![建立 aspnet-ContosoUniversity](deploying-to-iis/_static/image9.png)

遵循相同的程式，建立名為 `ContosoUniversity`的新 SQL Server Express School 資料庫。

**伺服器總管**會顯示兩個新的資料庫。

![伺服器總管中的新資料庫](deploying-to-iis/_static/image10.png)

## <a name="create-a-grant-script-for-the-new-databases"></a>建立新資料庫的授與腳本

當應用程式在開發電腦上的 IIS 中執行時，應用程式會使用預設應用程式集區的認證來存取資料庫。 不過，根據預設，應用程式集區沒有開啟資料庫的許可權。 這表示您需要執行腳本以授與該許可權。 在本節中，您將建立該腳本並于稍後執行，以確保應用程式可以在 IIS 中執行時開啟資料庫。

在文字編輯器中，將下列 SQL 命令複製到新的檔案，並將它儲存為*Grant. SQL*。 

[!code-sql[Main](deploying-to-iis/samples/sample2.sql)]

在 Visual Studio 中，開啟 [Contoso 大學] 解決方案。 以滑鼠右鍵按一下方案（不是其中一個專案），然後選取 [**新增**]。 選取 [**現有專案**]，流覽至 *[授與 .sql*]，然後開啟它。

> [!NOTE]
> 此腳本是設計用來搭配 SQL Server Express 2012 或更新版本，以及在本教學課程中指定的 Windows 10、Windows 8 或 Windows 7 中的 IIS 設定。 如果您使用的是不同版本的 SQL Server 或 Windows，或如果您在電腦上以不同的方式設定 IIS，可能就需要變更此腳本。 如需 SQL Server 腳本的詳細資訊，請參閱[SQL Server 線上叢書](https://go.microsoft.com/fwlink/?LinkId=132511)。

> [!NOTE] 
> **安全性注意事項**此腳本會為在執行時間存取資料庫的使用者提供 `db_owner` 許可權，這就是您在生產環境中擁有的功能。 在某些情況下，您可能會想要指定具有完整資料庫架構更新許可權的使用者，僅供部署之用，並為執行時間指定僅具有讀取和寫入資料許可權的其他使用者。 如需詳細資訊，請參閱本教學課程稍後的 <<c0>檢查自動的 Web.config 變更 Code First 移轉。

<a id="publish"></a>

## <a name="run-the-grant-script-in-the-application-database"></a>在應用程式資料庫中執行 grant 腳本

您可以將發行設定檔設定為在部署期間于成員資格資料庫中執行授與腳本，因為該資料庫部署會使用[dbDacFx](https://docs.microsoft.com/iis/publish/using-web-deploy/dbdacfx-provider-for-incremental-database-publishing)提供者。 您無法在 Code First 移轉部署期間執行腳本，這就是部署應用程式資料庫的方式。 這表示您必須在應用程式資料庫中部署之前，手動執行腳本。

1. 在 Visual Studio 中，開啟您稍早建立的*Grant .sql*檔案。

2. 選取 **[連線]** 。 

    ![[連線] 按鈕](deploying-to-iis/_static/image11.png)

3. 在 [**連接到伺服器**] 對話方塊中，輸入 *.\SQLExpress*做為**伺服器名稱**。 選取 **[連線]** 。

4. 在 [資料庫] 下拉式清單中，選取 [ **ContosoUniversity**]。 選取 [**執行**]。 

   ![](deploying-to-iis/_static/image12.png)

預設應用程式集區身分識別現在在應用程式資料庫中有足夠的許可權，可供 Code First 移轉在應用程式執行時建立資料庫資料表。

## <a name="publish-to-iis"></a>發佈至 IIS

有數種方式可供您使用 Visual Studio 和 Web Deploy 部署到 IIS：

* 使用 Visual Studio 單鍵發行。
* 從命令列發佈。
* 建立部署套件，並使用 IIS 管理員進行安裝。 封裝有一個 .zip 檔案，其中包含在 IIS 中安裝網站所需的所有檔案和中繼資料。
* 建立部署套件，並使用命令列進行安裝。

您在先前的教學課程中完成以設定 Visual Studio 來自動化部署工作的程式，適用于所有這些方法。 在這些教學課程中，您將使用前兩個方法。 如需使用部署套件的詳細資訊，請參閱 Visual Studio 和 ASP.NET 的 Web 部署內容對應中[建立和安裝 web 部署套件，以部署 web 應用程式](https://go.microsoft.com/fwlink/p/?LinkId=282413#package)。

在發佈之前，請確定您是以系統管理員模式執行 Visual Studio。 如果您在標題列中沒有看到 **（系統管理員）** ，請關閉 Visual Studio。 在 Windows 8 （或更新版本）**起始**頁或 windows 7 **開始** 功能表中，以滑鼠右鍵按一下 Visual Studio 圖示，然後選取 以**系統管理員身分執行**。 只有當您要發行到本機電腦上的 IIS 時，才需要系統管理員模式。

### <a name="create-the-publish-profile"></a>建立發行設定檔

1. 在**方案總管**中，以滑鼠右鍵按一下**ContosoUniversity**專案（而非**ContosoUniversity**專案）。 選取 [發行]。 [**發行**] 頁面隨即出現。

2. 選取 [**新增設定檔**]。 [**挑選發行目標**] 對話方塊隨即出現。

3. 選取 [ **IIS]、[FTP] 等等**。選取 [建立設定檔]。 [**發行**嚮導] 隨即出現。

   ![[發行 Web wizard 設定檔] 索引標籤](deploying-to-iis/_static/image26.png)

4. 從 [**發行方法**] 下拉式功能表中，選取 [ **Web Deploy**]。

5. 針對 [**伺服器**]，輸入*localhost*。

6. 在 [**網站名稱**] 中，輸入*Default Web Site/ContosoUniversity*。

7. 在 [**目的地 URL**] 中，輸入 *http://localhost/ContosoUniversity* 。

   不需要 [**目的地 URL** ] 設定。 當 Visual Studio 完成部署應用程式時，它會自動開啟此 URL 的預設瀏覽器。 如果您不想要在部署後自動開啟瀏覽器，請將此方塊保留空白。

8. 選取 [**驗證連接**]，確認設定正確，而且您可以連接到本機電腦上的 IIS。

   綠色核取記號會確認連接是否成功。

   ![[發佈 Web wizard 連接] 索引標籤](deploying-to-iis/_static/image27.png)

9. 選取 **[下一步**] 前進至 [**設定**] 索引標籤。

10. [設定] 下拉式方塊會指定要**部署的組建**設定。 將它設定為預設值 [**發行**]。 在本教學課程中，您將不會部署 Debug build。

11. 展開 [檔案] [**發行選項**]。 選取 **[從應用程式中排除檔案\_資料夾**]。

    在測試環境中，應用程式會存取您在本機 SQL Server Express 實例中建立的資料庫，而不是*應用程式\_Data*資料夾中的 .mdf 檔案。

12. 在 [**發行**及**移除目的地的其他**檔案] 核取方塊中，保留預先編譯的狀態。

    ![[設定] 索引標籤中的檔案發佈選項](deploying-to-iis/_static/image15a.png)

    先行編譯是適用于大型網站的選項。 在網站發佈之後，第一次要求頁面時，它可以減少啟動時間。

    您不需要移除其他檔案，因為這是您的第一個部署，而且目的地資料夾中還沒有任何檔案。

    > [!NOTE] 
    > 如果您選取 [**移除目的地的其他**檔案] 以進行後續部署到相同的網站，請確定您使用的是預覽功能，如此一來，您就會事先看到哪些檔案將在部署之前刪除。 預期的行為是 Web Deploy 會刪除您在專案中已刪除之目的地伺服器上的檔案。 不過，會比較來源和目的地資料夾下的整個資料夾結構。而在某些情況下，Web Deploy 可能會刪除您不想要刪除的檔案。
    > 
    > 例如，如果您在伺服器上的子資料夾中有 web 應用程式，當您將專案部署至根資料夾時，將會刪除子資料夾。 您在 contoso.com 的主要網站可能會有一個專案，而 contoso.com/blog 的另一個專案則適用于 blog。 Blog 應用程式位於子資料夾中。 如果您在部署主要網站時選取 [**移除目的地的其他**檔案]，則會刪除 blog 應用程式。
    > 
    > 若是另一個範例，您的應用程式\_Data 資料夾可能會意外刪除。 某些資料庫（例如 SQL Server Compact 會將資料庫檔案儲存在應用程式\_的 Data 資料夾中。 在初始部署之後，您不想要繼續在後續部署中複製資料庫檔案，因此您可以選取 [封裝/發行 Web] 索引標籤上的 [**排除應用程式\_資料**]。執行此動作之後，如果您已選取 [**移除目的地的其他**檔案]，則下次發行時，將會刪除您的資料庫檔案和應用程式\_Data 資料夾本身。

### <a name="configure-deployment-for-the-membership-database"></a>設定成員資格資料庫的部署

下列步驟適用于對話方塊的 [**資料庫**] 區段中的**DefaultConnection**資料庫。

1. 在 [**遠端連線字串**] 方塊中，輸入指向新 SQL Server Express 成員資格資料庫的下列連接字串。

   [!code-console[Main](deploying-to-iis/samples/sample3.cmd)]

   部署程式會將此連接字串放在已部署的 Web.config 檔案中，因為已選取 [**在執行時間使用此連接字串**]。

    您也可以從**伺服器總管**取得連接字串。 在**伺服器總管**中，展開 [**資料連線**]，然後選取 **&lt;machinename&gt;\sqlexpress.aspnet-ContosoUniversity**資料庫，然後從 [**屬性**] 視窗複製 [**連接字串**] 值。 該連接字串將會有一個您可以刪除的額外設定： `Pooling=False`。

2. 選取 [**更新資料庫**]。

   這會導致在部署期間，于目的地資料庫中建立資料庫架構。 在接下來的步驟中，您會指定需要執行的其他腳本：一個用來授與資料庫存取權給預設的應用程式集區，另一個則用來部署資料。

3. 選取 [**設定資料庫更新**]。
 
4. 在 [**設定資料庫更新**] 對話方塊中，選取 [**加入 SQL 腳本**]。 流覽至您稍早在 [方案] 資料夾中儲存的*Grant. sql*腳本。

5. 重複此程式以新增*aspnet-data-dev*腳本。

   ![設定成員資格資料庫的資料庫更新](deploying-to-iis/_static/image16.png)

6. 選取 [關閉]。

### <a name="configure-deployment-for-the-application-database"></a>設定應用程式資料庫的部署

當 Visual Studio 偵測到 Entity Framework `DbContext` 類別時，它會在 [**資料庫**] 區段中建立具有 [**執行 Code First 移轉**] 核取方塊的專案，而不是 [**更新資料庫**] 核取方塊。 在本教學課程中，您將使用該核取方塊來指定 Code First 移轉部署。

在某些情況下，您可能會使用 `DbContext` 的資料庫，但是您想要使用 dbDacFx 提供者而不是遷移來部署資料庫。 在此情況下，請參閱 MSDN 上的 ASP.NET Web 部署常見問題中的[如何? 部署 Code First 資料庫而不進行遷移？](https://msdn.microsoft.com/library/ee942158.aspx#deploy_code_first_without_migrations) 。

下列步驟適用于對話方塊的 [**資料庫**] 區段中的**SchoolCoNtext**資料庫。

1. 在 [**遠端連線字串**] 方塊中，輸入指向新 SQL Server Express 應用程式資料庫的下列連接字串。

   [!code-console[Main](deploying-to-iis/samples/sample4.cmd)]

   部署程式會將此連接字串放在已部署的 Web.config 檔案中，因為已選取 [**在執行時間使用此連接字串**]。

   您也可以利用取得成員資格資料庫連接字串的相同方式，從**伺服器總管**取得應用程式資料庫連接字串。

2. 選取**執行 Code First 移轉（在應用程式啟動時執行）** 。

   此選項會讓部署程式設定已部署的 Web.config 檔案，以指定 `MigrateDatabaseToLatestVersion` 初始化運算式。 當應用程式在部署後第一次存取資料庫時，這個初始化運算式會自動將資料庫更新為最新版本。

### <a name="configure-publish-profile-transforms"></a>設定發行設定檔轉換

1. 選取 [關閉]。 當系統詢問您是否要儲存變更時，請選取 **[是]** 。

2. 在**方案總管**中，依序展開 [**屬性**] 和 [ **PublishProfiles**]。

3. 以滑鼠右鍵按一下*CustomProfile .pubxml* ，然後將它重新命名為 *.pubxml*。

4. 以滑鼠右鍵按一下 [ *.pubxml*]。 選取 [**新增設定轉換**]。

   ![[新增設定轉換] 功能表](deploying-to-iis/_static/image17.png)

   Visual Studio 建立 web.config*轉換檔案*並開啟它。

5. *在 web.config 轉換檔案*中，將下列程式碼插入緊接在開啟設定標記之後。

   [!code-xml[Main](deploying-to-iis/samples/sample5.xml)]

    當您使用測試發行設定檔時，這種轉換會將環境指標設定為「測試」。 在部署的網站中，您會在 "Contoso 大學" H1 標題之後看到 "（Test）"。

6. 儲存並關閉檔案。

7. 以滑鼠右鍵按一下*web.config*檔案，然後選取 [**預覽轉換**]，以確定您編碼的轉換會產生預期的變更。

    [Web.config**預覽**] 視窗會顯示套用*web.config* *轉換和 web.config 轉換時*所產生的結果。

### <a name="preview-the-deployment-updates"></a>預覽部署更新

1. 再次開啟 [**發行 Web** wizard] （以滑鼠右鍵按一下 ContosoUniversity 專案，然後依序選取 [**發佈**] 和 [**預覽**]）。

2. 在 [**預覽**] 對話方塊中，選取 [**開始預覽**] 以查看將複製的檔案清單。 

   ![發行預覽](deploying-to-iis/_static/image29.png)

   您也可以選取 [**預覽資料庫**] 連結，以查看將在成員資格資料庫中執行的腳本。 （不會針對 Code First 移轉部署執行任何腳本，因此不會為應用程式資料庫預覽任何內容）。

3. 選取 [發行]。

   如果 Visual Studio 不是在系統管理員模式中，您可能會收到許可權錯誤訊息。 在此情況下，請關閉 Visual Studio，在系統管理員模式中開啟它，然後再次嘗試發佈。

   如果 Visual Studio 處於系統管理員模式，[**輸出**] 視窗會報告 [成功的組建] 和 [發行]。

   ![Output_window_publish_Test](deploying-to-iis/_static/image20.png)

   如果您在 [**發行設定檔**連線] 索引標籤的 [**目的地 URL** ] 方塊中輸入 URL，瀏覽器會自動開啟至您電腦上的 IIS 中執行的 Contoso 大學首頁。

## <a name="test-in-the-test-environment"></a>在測試環境中測試

請注意，環境指標會顯示「（測試）」而不是「（Dev）」，這表示環境指標的*web.config 轉換成功*。

執行 [**講師**] 頁面，確認 Code First 以講師資料植入資料庫。 當您選取此頁面時，可能需要幾分鐘的時間才能載入，因為 Code First 會建立資料庫，然後執行 `Seed` 方法。 （因為應用程式尚未嘗試存取資料庫，所以不會在首頁上這麼做。）

選取 [**學生**] 索引標籤，確認已部署的資料庫沒有任何學生。

從 [**學生**] 功能表中選取 [**新增學生**]。 新增學生，然後在 [**學生**] 頁面中查看新學生。 這會驗證您是否可以成功寫入資料庫。

從 [**課程**] 功能表中，選取 [**更新信用額度**]。 [**更新信用額度**] 頁面需要系統管理員許可權，因此會顯示 [**登入**] 頁面。 輸入您稍早建立的系統管理員帳號憑證（"admin" 和 "devpwd"）。 [**更新信用額度**] 頁面隨即顯示。 這會確認您在上一個教學課程中建立的系統管理員帳戶已正確部署到測試環境。

確認*c:\inetpub\wwwroot\ContosoUniversity*資料夾中有一個只有預留位置檔案的*ELMAH*資料夾。

<a id="reviewingmigrations"></a>

## <a name="review-the-automatic-webconfig-changes-for-code-first-migrations"></a>檢查 Code First 移轉的自動 web.config 變更

在*C:\inetpub\wwwroot\ContosoUniversity*的已部署應用程式中開啟*web.config*檔案，您可以看到部署程式設定 Code First 移轉自動將資料庫更新為最新版本。

![](deploying-to-iis/_static/image21.png)

部署程式也會為 Code First 移轉建立新的連接字串，以獨佔用來更新資料庫架構：

![Database_Publish 連接字串](deploying-to-iis/_static/image22.png)

這個額外的連接字串可讓您指定資料庫架構更新的一個使用者帳戶，以及不同的使用者帳戶來存取應用程式資料。 例如，您可以將**db\_擁有**者角色指派給 Code First 移轉和**db\_datareader**與**db\_資料寫入元**角色至應用程式。 這是常見的深度防禦模式，可防止應用程式中可能的惡意程式碼變更資料庫架構。 （例如，這可能會發生在成功的 SQL 插入式攻擊中）。這些教學課程不會使用此模式。 若要在您的案例中執行此模式，請執行下列步驟：

1. 在 [**發行 Web** wizard] 的 [**設定**] 索引標籤下，輸入指定具有完整資料庫架構更新許可權之使用者的連接字串。 清除 [**在執行時間使用此連接字串**] 核取方塊。 在已部署的 Web.config 檔案中，這會變成 `DatabasePublish` 連接字串。

2. 針對您希望應用程式在執行時間使用的連接字串，建立 Web.config 檔案轉換。

## <a name="summary"></a>總結

您現在已將應用程式部署至開發電腦上的 IIS，並在該處進行測試。

![測試中的首頁](deploying-to-iis/_static/image23.png)

這會驗證部署程式是否已將應用程式的內容複寫到正確的位置（不包括您不想要部署的檔案），以及在部署期間，Web Deploy 正確設定 IIS。 在下一個教學課程中，您將執行一項測試，尋找尚未完成的部署工作：在 [*榆樹 ah* ] 資料夾上設定資料夾許可權。

## <a name="more-information"></a>詳細資訊

如需在 Visual Studio 中執行 IIS 或 IIS Express 的詳細資訊，請參閱下列資源：

- [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 網站上的總覽。
- [簡介 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie 的 blog。
- [Visual Studio 中用於 ASP.NET Web 專案的 Web 服務器](https://msdn.microsoft.com/library/58wxa9w5.aspx)。
- [IIS 與 ASP.NET 網站上的 ASP.NET 程式開發伺服器之間的核心差異](../../older-versions-getting-started/deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。

如需在您的應用程式以中度信任執行時可能會發生哪些問題的詳細資訊，請參閱 Rolla 網站的四位專家的[中級信任中的 ASP.NET 應用程式裝載](http://www.4guysfromrolla.com/articles/100307-1.aspx)。

> [!div class="step-by-step"]
> [上一頁](project-properties.md)
> [下一頁](setting-folder-permissions.md)
