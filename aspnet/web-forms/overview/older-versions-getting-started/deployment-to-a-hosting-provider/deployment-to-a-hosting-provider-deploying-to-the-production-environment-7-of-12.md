---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署到生產環境-12-7Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: b83ab819-2b05-4776-b7b4-79ef78d457a5
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12
msc.type: authoredcontent
ms.openlocfilehash: db838633accdedd7c0693b126a007e254ca681e4
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74627347"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-the-production-environment---7-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署到生產環境-12 的7

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

在本教學課程中，您會設定具有主控提供者的帳戶，並使用 Visual Studio 單鍵發佈功能，將您的 ASP.NET web 應用程式部署到生產環境。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="selecting-a-hosting-provider"></a>選取主控提供者

針對 Contoso 大學應用程式和本教學課程系列，您需要支援 ASP.NET 4 和 Web Deploy 的提供者。 選擇特定的主控公司，讓教學課程可以說明部署至即時網站的完整體驗。 每個主控公司都提供不同的功能，而部署到其伺服器的經驗則有所不同。 不過，本教學課程中所述的程式對整體程式而言是一般的。 本教學課程所使用的裝載提供者（Cytanium.com）是其中一種可用的，而在本教學課程中使用時，不會構成背書或建議。

當您準備好要選取自己的主控提供者時，您可以比較 Microsoft.com/web 網站上[提供者資源庫](https://www.microsoft.com/web/hosting)中的功能和價格。

## <a name="creating-an-account"></a>建立帳戶

在您選取的提供者上建立帳戶。 如果完整 SQL Server 資料庫的支援是額外增加的，您就不需要在本教學課程中選取它，但在本系列稍後的[遷移至 SQL Server](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12.md)教學課程時，您將需要它。

在這些教學課程中，您不需要註冊新的功能變數名稱。 您可以使用提供者指派給網站的暫時 URL，進行測試以確認部署是否成功。

建立帳戶之後，您通常會收到歡迎電子郵件，其中包含部署和管理您的網站所需的所有資訊。 您的主機服務提供者傳送的資訊將與此處顯示的內容類別似。 傳送給新帳戶擁有者的 Cytanium 歡迎電子郵件包含下列資訊：

- 提供者之控制台網站的 URL，您可以在其中管理網站的設定。 您指定的識別碼和密碼會包含在歡迎電子郵件的這個部分中，方便您參考。 （這兩者都已變更為此圖的示範值）。

    [![Welcome_Email_Control_Panel_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image1.png)
- 預設 .NET Framework 版本以及如何變更它的相關資訊。 許多主控網站預設為2.0，適用于以 .NET Framework 2.0、3.0 或3.5 為目標的 ASP.NET 應用程式。 不過，Contoso 大學是 .NET Framework 4 應用程式，因此您必須變更此設定。 （針對 ASP.NET 4.5 應用程式，您會使用 .NET 4.0 設定）。

    [![Welcome_Email_Framework_Version](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image3.png)
- 您可以用來存取網站的暫時 URL。 建立此帳戶時，會將 "contosouniversity.com" 輸入為現有的功能變數名稱。 因此，會 `http://contosouniversity.com.vserver01.cytanium.com`暫存 URL。

    [![Welcome_Email_Temporary_URL](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image5.png)
- 有關如何設定資料庫的資訊，以及您需要的連接字串，以便存取它們：

    [![Welcome_Email_Database_Info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image7.png)
- 用於部署網站之工具和設定的相關資訊。 （來自 Cytanium 的電子郵件也提及 WebMatrix，此處會省略）。

    [![Welcome_Email_Deploy_info](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image10.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image9.png)

## <a name="setting-the-net-framework-version"></a>設定 .NET Framework 版本

Cytanium 歡迎電子郵件包含如何變更 .NET Framework 版本的指示連結。 這些指示說明這可以透過 [Cytanium] 控制台來完成。 其他提供者的「控制台」網站看起來不同，或可能會指示您以不同的方式執行此動作。

移至 [控制台 URL]。 使用您的使用者名稱和密碼登入之後，您會看到 [控制台]。

[![Cytanium_Control_Panel](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image12.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image11.png)

在 [**主控空間**] 方塊中，將指標放在 Web 圖示上，然後從功能表中選取 [**網站**]。

[![Cytanium_Control_Panel_selecting_Web_Sites](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image14.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image13.png)

在 [**網站**] 方塊中，按一下 [ **contosouniversity.com** ] （您在建立帳戶時所使用的網站名稱）。

[![Cytanium_Control_Panel_selecting_contosouniversity](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image15.png)

在 [**網站屬性**] 方塊中，選取 [**擴充**功能] 索引標籤。

[![Cytanium_Control_Panel_Extensions_tab](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image17.png)

將 ASP.NET 從**2.0 整合管線**變更為**4.0 （整合式管線）** ，然後按一下 [**更新**]。

## <a name="publishing-to-the-hosting-provider"></a>發行至主控提供者

來自主控提供者的歡迎電子郵件包含發行專案所需的所有設定，而且您可以手動將該資訊輸入發行設定檔中。 但是，您將使用較簡單且較不容易出錯的方法，來設定提供者的部署：您將下載 *.publishsettings*檔案，並將它匯入發行設定檔。

在瀏覽器中，移至 [Cytanium] 控制台，然後選取 [ **web** ]，再選取 [**網站]。**

![選取 Web Sites 的控制台](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image19.png)

選取 [ **contosouniversity.com** ] 網站。

![選取 contosouniversity.com 的控制台](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image20.png)

選取 [ **Web 發行**] 索引標籤。

![控制台 Web 發佈索引標籤](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image21.png)

輸入使用者名稱和密碼，以建立用於網頁發佈的認證。 您可以輸入用來登入 [控制台] 的相同認證。 然後按一下 [**啟用**]。

![控制台建立發行認證](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image22.png)

按一下 [**下載此網站的發行設定檔**]。

![控制台下載發行設定檔](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image23.png)

當系統提示您開啟或儲存檔案時，請儲存檔案。

![儲存發行設定檔](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image24.png)

在 Visual Studio 的**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後選取 [**發佈**]。 [**發行 Web** ] 對話方塊會在 [**預覽**] 索引標籤上開啟，其中已選取**測試**設定檔，因為這是您所使用的最後一個設定檔。

選取 [**設定檔**] 索引標籤，然後按一下 [匯**入**]。

![發行 Web wizard 匯入按鈕](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image25.png)

在 [匯**入發行設定**] 對話方塊中，選取您下載的 *.publishsettings*檔案，然後按一下 [**開啟**]。 Wizard 會前進至 [連線] 索引標籤，其中填入所有欄位。

![[發佈 Web wizard 連接] 索引標籤](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image26.png)

.Publishsettings 檔案會將網站規劃的永久 URL 放在 [目的地 URL] 方塊中，但如果您尚未購買該網域，請將此值取代為暫存 URL。 在此範例中，URL 為 *[http://contosouniversity.com.vserver01.cytanium.com](http://contosouniversity.com.vserver01.cytanium.com)。* 此方塊的唯一目的是指定瀏覽器在部署之後成功開啟的 URL。 如果您將它保留空白，則唯一的結果是瀏覽器不會在部署後自動啟動。

按一下 [**驗證連接**]，確認設定正確，而且您可以連接到伺服器。 如您稍早所見，綠色的核取記號會確認連接是否成功。

當您按一下 [驗證連接] 時，可能會看到 [**憑證錯誤**] 對話方塊。 如果您這樣做，請確認伺服器名稱是否符合您的預期。 如果是，請選取 [**儲存此憑證以供 Visual Studio 的未來會話**]，然後按一下 [**接受**]。 （此錯誤表示主機服務提供者已選擇避免針對您要部署的 URL 購買 SSL 憑證的費用。 如果您想要使用有效的憑證來建立安全連線，請聯絡您的主機服務提供者）。

![憑證錯誤](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image27.png)

按 [ **下一步**]。

在 [**設定**] 索引標籤的 [**資料庫**] 區段中，輸入您為測試發行設定檔輸入的相同值。 您會在下拉式清單中找到所需的連接字串。

- 在 SchoolCoNtext 的 連接字串 方塊中 **，** 選取 `Data Source=|DataDirectory|School-Prod.sdf`
- 在 [ **SchoolCoNtext**] 底下，選取 [套用**Code First 移轉**]。
- 在  **DefaultConnection** 的 連接字串 方塊中，選取 `Data Source=|DataDirectory|aspnet-Prod.sdf`
- 在 [ **DefaultConnection**] 下，將 [**更新資料庫**] 保持清除。

![[發行 Web wizard 設定] 索引標籤](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image28.png)

按 [ **下一步**]。

在 [**預覽**] 索引標籤中，按一下 [**開始預覽**] 以查看將複製的檔案清單。 您會看到稍早在本機電腦上部署到 IIS 時所看到的相同清單。

發行之前，請變更設定檔的名稱，以便套用您的 Web.config 轉換檔案。 選取 [**設定檔**] 索引標籤，然後按一下 [**管理設定檔**]。

![發行 Web wizard 管理設定檔](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image29.png)

在 [**編輯 Web 發行設定檔**] 對話方塊中，選取 [生產] 設定檔，按一下 [**重新命名**]，然後將設定檔名稱變更為 [生產]。 然後按一下 [**關閉**]。

![[編輯網頁發行設定檔] 對話方塊](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image30.png)

按一下 [發行]。

應用程式會發佈至主控提供者。 結果會顯示在 [**輸出**] 視窗中。

![部署後的輸出視窗](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image31.png)

瀏覽器會自動開啟至 [**發行 Web** wizard] 的 [**連接**] 索引標籤上，您在 [**目的地 URL** ] 方塊中輸入的 url。 您會看到與您在 Visual Studio 中執行網站時相同的首頁，但目前標題列中沒有 [（測試）] 或 [（Dev）] 環境指標。 這表示環境指示器*web.config*轉換正常運作。

> [!NOTE]
> 如果您仍在標題中看到 [（測試）]，請從 ContosoUniversity 專案中刪除*obj*資料夾，然後重新部署。 在軟體的發行前版本中，先前套用的轉換檔（web.config）可能會再次套用，雖然您使用的是生產設定檔。

[![Home_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image33.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image32.png)

在您執行會導致資料庫存取的頁面之前，請確定 Elmah 能夠記錄任何發生的錯誤。

## <a name="setting-folder-permissions-for-elmah"></a>設定 Elmah 的資料夾許可權

就像您在本系列的上一個教學課程中所做的一樣，您必須確定應用程式具有應用程式中資料夾的寫入權限，其中 Elmah 會儲存錯誤記錄檔。 當您在本機電腦上部署到 IIS 時，您會以手動方式設定這些許可權。 在本節中，您將瞭解如何在 Cytanium 設定許可權。 （有些主控提供者可能無法讓您執行這項操作; 它們可能會提供一或多個具有寫入權限的預先定義資料夾。 在此情況下，您必須修改應用程式，以使用指定的資料夾。）

您可以在 [Cytanium] 控制台中設定資料夾許可權。 移至 [控制台] URL，然後選取 [**檔案管理員**]。

[![Cytanium_Control_Panel_with_File_Manager_selected](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image35.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image34.png)

在 [**檔案管理員**] 方塊中，選取 [ **contosouniversity.com** ]，然後選取 [ **wwwroot** ] 以查看應用程式的根資料夾。 按一下 [ **Elmah**] 旁的掛鎖圖示。

[![Cytanium_Control_Panel_File_Manager_at_root_folder](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image37.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image36.png)

在 [**檔案**/**資料夾許可權**] 視窗中，選取**contosouniversity.com**的 [**讀取**] 和 [**寫入**] 核取方塊，然後按一下 [**設定許可權**]。

[![Cytanium_Control_Panel_File_Folder_Permissions_Elmah](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image39.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image38.png)

請確定 Elmah 具有*elmah*資料夾的寫入權限，方法是造成錯誤，然後顯示 elmah 錯誤報表。 要求不正確 URL，例如*Studentsxxx。* 如先前所示，您會看到*GenericErrorPage .aspx*頁面。 按一下 [**登出**] 連結，然後執行*Elmah. axd*。 您會先取得**登入**頁面，這會驗證*web.config*轉換是否已成功新增 Elmah authorization。 登入之後，您會看到報告，顯示您所造成的錯誤。

[![Elmah. axd_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image41.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image40.png)

## <a name="testing-in-the-production-environment"></a>在生產環境中測試

執行 [**學生**] 頁面。 應用程式會嘗試第一次存取 School 資料庫，這會觸發 Code First 移轉來建立資料庫。 當頁面在延遲一段時間之後顯示時，就會顯示沒有任何學生。

[![Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image43.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image42.png)

執行 [**講師**] 頁面，確認種子資料已成功將講師資料插入資料庫中。

[![Instructors_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image45.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image44.png)

就像您在測試環境中所做的一樣，您想要確認資料庫更新在生產環境中運作，但您通常不想要將測試資料輸入生產資料庫中。 在本教學課程中，您將使用測試中的相同方法。 但是在實際的應用程式中，您可能會想要尋找驗證資料庫更新是否成功的方法，而不會將測試資料引入生產資料庫。 在某些應用程式中，新增一些專案並加以刪除可能會很實用。

新增學生，然後查看您在 [**學生**] 頁面中輸入的資料，以確認您可以更新資料庫中的資料。

[![Add_Students_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image47.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image46.png)

[![Students_page_with_new_student_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image49.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image48.png)

從 [**課程**] 功能表選取 [**更新信用額度**]，以驗證授權規則是否正常運作。 [**登入**] 頁面隨即顯示。 輸入您的系統管理員帳號憑證，按一下 [**登入**]，[**更新信用額度**] 頁面隨即顯示。

[![Log_In_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image51.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image50.png)

如果登入成功，則會顯示 [**更新信用額度**] 頁面。 這表示已成功部署 ASP.NET 成員資格資料庫（具有單一系統管理員帳戶）。

[![Update_Credits_page_Prod](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image53.png)](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/_static/image52.png)

您現在已成功部署及測試您的網站，且可透過網際網路公開取得。

## <a name="creating-a-more-reliable-test-environment"></a>建立更可靠的測試環境

如[部署至測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教學課程中所述，最可靠的測試環境會是主控提供者的第二個帳戶，就像生產帳戶一樣。 因為您必須註冊第二個主控帳戶，所以這會比使用本機 IIS 做為測試環境更耗費資源。 但是，如果它防止生產網站錯誤或中斷，您可能會決定這是值得付出的代價。

建立及部署到測試帳戶的大部分程式，與您部署到生產環境的步驟類似：

- 建立*web.config*轉換檔案。
- 在主控提供者上建立帳戶。
- 建立新的發行設定檔，並部署到測試帳戶。

### <a name="preventing-public-access-to-the-test-site"></a>防止測試網站的公用存取

測試帳戶有一個重要的考慮，那就是它會在網際網路上上線，但您不想讓公用使用它。 若要讓網站保持在私用，您可以使用下列一或多種方法：

- 請洽詢主機服務提供者，以設定防火牆規則，只允許來自您用於測試之 IP 位址的測試網站存取。
- 偽裝 URL，使其與公用網站的 URL 不類似。
- 使用*機器人 .txt*檔案，以確保搜尋引擎不會編目測試網站，並在搜尋結果中報告其連結。

這兩種方法的第一種是最安全的，但這是每個主控提供者特有的程式，將不會在本教學課程中討論。 如果您使用主機服務提供者來安排，只允許您的 IP 位址流覽至測試帳戶 URL，理論上您不需要擔心搜尋引擎將它編目。 但是，即使在這種情況下，在不小心關閉防火牆規則的情況下，部署*機器人 .txt*檔案是個不錯的主意。

*機器人 .txt*檔案會進入您的專案資料夾中，而且應該包含下列文字：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12/samples/sample1.cmd)]

[`User-agent`] 行會告訴搜尋引擎，檔案中的規則會套用至所有的搜尋引擎 web 編目程式（機器人），而 [`Disallow`] 行會指定網站上不應編目任何頁面。

您可能想要讓搜尋引擎針對您的生產網站進行類別目錄，因此您必須將此檔案從生產部署中排除。 若要這麼做，請參閱[ASP.NET Web 應用程式專案部署常見問題](https://msdn.microsoft.com/library/ee942158.aspx#can_i_exclude_specific_files_or_folders_from_deployment)中的「**我可以從部署中排除特定檔案或資料夾嗎？** 」。 請確定您只針對生產發行設定檔指定排除。

建立第二個主控帳戶是使用不需要的測試環境，但可能值得增加的費用的方法。 在下列教學課程中，您將繼續使用 IIS 做為測試環境。

在下一個教學課程中，您將更新應用程式程式碼，並將變更部署到測試和生產環境。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-deploying-a-code-only-update-8-of-12.md)
