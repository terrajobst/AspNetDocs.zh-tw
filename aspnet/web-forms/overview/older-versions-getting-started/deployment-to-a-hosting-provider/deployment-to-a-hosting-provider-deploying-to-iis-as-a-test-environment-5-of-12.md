---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署至 IIS 作為測試環境-5/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: 493b2a66-816c-485c-8315-952ed1085ccc
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12
msc.type: authoredcontent
ms.openlocfilehash: 5d85232ff2cb229d771d517db7173721c9e277bf
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633394"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-to-iis-as-a-test-environment---5-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署至 IIS 作為測試環境-5/12

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

本教學課程說明如何將 ASP.NET web 應用程式部署到本機電腦上的 IIS。

當您開發應用程式時，通常會在 Visual Studio 中執行測試。 根據預設，這表示您使用的是 Visual Studio 程式開發伺服器（也稱為 Cassini）。 Visual Studio 程式開發伺服器可讓您輕鬆地在 Visual Studio 開發期間進行測試，但它的作用與 IIS 完全一樣。 如此一來，當您在 Visual Studio 中進行測試時，應用程式可能會正確執行，但當它部署至裝載環境中的 IIS 時，會失敗。

您可以透過下列方式，更可靠地測試您的應用程式：

1. 在開發期間，當您在 Visual Studio 中測試時，請使用 IIS Express 或完整的 IIS，而不是 Visual Studio 程式開發伺服器。 這個方法通常會更精確地模擬您的網站在 IIS 下執行的方式。 不過，這個方法不會測試您的部署程式，也不會驗證部署程式的結果是否會正確執行。
2. 使用您稍後將用來部署至生產環境的相同程式，將應用程式部署到開發電腦上的 IIS。 除了驗證您的應用程式會在 IIS 下正確執行之外，這個方法也會驗證您的部署流程。
3. 將應用程式部署到盡可能接近您生產環境的測試環境。 由於這些教學課程的生產環境是協力廠商主控提供者，因此理想的測試環境會是具有主控提供者的第二個帳戶。 您只會使用此第二個帳戶進行測試，但其設定方式與生產帳戶相同。

本教學課程說明選項2的步驟。 選項3的指引是在[部署至生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程的結尾處提供，在本教學課程結束時，會有選項1的資源連結。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="configuring-the-application-to-run-in-medium-trust"></a>將應用程式設定為以中度信任執行

在安裝 IIS 並進行部署之前，您將變更 Web.config 檔案設定，讓網站在一般共用主控環境中執行的方式更類似。

主機服務提供者通常會在中*度信任*執行您的網站，這表示不允許執行某些動作。 例如，應用程式代碼無法存取 Windows 登錄，而且無法讀取或寫入位於應用程式資料夾階層外的檔案。 根據預設，您的應用程式會在您的本機電腦上以*高信任*度執行，這表示應用程式可能會在您將其部署到生產環境時，執行失敗的工作。 因此，為了讓測試環境更精確地反映出生產環境，您會將應用程式設定為以中度信任來執行。

在應用程式的 web.config 檔案中，于**system.web 元素中**加入**trust**元素，如下列範例所示。

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample1.xml?highlight=4)]

應用程式現在會在 IIS 中以中等信任的方式執行，即使在您的本機電腦上也一樣。 此設定可讓您儘早攔截應用程式的任何嘗試作業，以執行會在生產環境中失敗的作業。

> [!NOTE]
> 如果您使用 Entity Framework Code First 移轉，請確定您已安裝5.0 版或更新版本。 在 Entity Framework 版本4.3 中，遷移需要完全信任，才能更新資料庫架構。

## <a name="installing-iis-and-web-deploy"></a>安裝 IIS 和 Web Deploy

若要部署到開發電腦上的 IIS，您必須安裝 IIS 和 Web Deploy。 這些不包含在預設的 Windows 7 設定中。 如果您已經安裝 IIS 和 Web Deploy，請跳到下一節。

使用[Web Platform Installer](https://www.microsoft.com/web/downloads/platform.aspx)是安裝 iis 和 Web Deploy 的慣用方式，因為 Web Platform Installer 會安裝 iis 的建議設定，並且會在必要時自動安裝 iis 和 Web Deploy 的必要條件。

若要執行 Web Platform Installer 以安裝 IIS 和 Web Deploy，請使用下列連結。 如果您已經安裝 IIS、Web Deploy 或其任何必要的元件，Web Platform Installer 只會安裝遺失的內容。

- [使用 WebPI 安裝 IIS 和 Web Deploy](https://www.microsoft.com/web/gallery/install.aspx?appsxml=&amp;appid=IIS7;ASPNET;NETFramework4;WDeploy)

## <a name="setting-the-default-application-pool-to-net-4"></a>將預設應用程式集區設定為 .NET 4

安裝 IIS 之後，請執行**Iis 管理員**，以確定 .NET Framework 第4版已指派給預設的應用程式集區。

從 Windows [**開始**] 功能表中，選取 [**執行**]，輸入 "inetmgr"，然後按一下 **[確定]** 。 （如果 [**執行**] 命令不在您的 [**開始**] 功能表中，您可以按下 Windows 鍵和 R 來開啟它。 或以滑鼠**按右鍵工作列，按一下 [** 內容]，選取 [**開始] 功能表**索引標籤，按一下 [**自訂**]，然後選取 [**執行命令**]）。

在 [**連線] 窗格**中，展開伺服器節點，然後選取 [**應用程式**集區]。 在 [**應用程式**集區] 窗格中，如果**DefaultAppPool**已指派給 .net framework 第4版（如下圖所示），請跳至下一節。

[![Inetmgr_showing_4。0_app_pools](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image2.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image1.png)

如果您只看到兩個應用程式集區，而且兩者都設定為 .NET Framework 2.0，則您必須在 IIS 中安裝 ASP.NET 4：

- 以滑鼠右鍵按一下 Windows [**開始**] 功能表中的 [**命令提示**字元]，然後選取 [以**系統管理員身分執行**]，開啟命令提示字元視窗 然後使用下列命令，在 IIS 中執行[aspnet\_regiis](https://msdn.microsoft.com/library/k6h9cz8h.aspx)來安裝 ASP.NET 4。 （在64位系統中，將 "Framework" 取代為 "Framework64"）。

    [!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample2.cmd)]

    [![aspnet_regiis_installing_ASP。 NET_4](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image4.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image3.png)

    此命令會建立 .NET Framework 4 的新應用程式集區，但預設的應用程式集區仍會設定為2.0。 您將會將以 .NET 4 為目標的應用程式部署至該應用程式集區，因此您必須將應用程式集區變更為 .NET 4。

如果您關閉了 [ **IIS 管理員**]，請再次執行它，展開伺服器節點，然後按一下 [**應用程式**集區]，再次顯示 [**應用程式**集區] 窗格。

在 [**應用程式**集區] 窗格中，按一下 [ **DefaultAppPool**]，然後按一下 [**動作**] 窗格中的 [**基本設定**]。

[![Inetmgr_selecting_Basic_Settings_for_app_pool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image6.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image5.png)

在 [**編輯應用程式集**區] 對話方塊中，將 **.NET Framework 版本**變更為 **.NET Framework v 4.0.30319** ，然後按一下 **[確定]** 。

[![Selecting_。 NET_4_for_DefaultAppPool](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image8.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image7.png)

您現在已準備好發佈至 IIS。

## <a name="publishing-to-iis"></a>發行至 IIS

有數種方式可供您使用 Visual Studio 2010 和 Web Deploy 部署：

- 使用 Visual Studio 單鍵發行。
- 建立*部署套件*，並使用 IIS 管理員 UI 進行安裝。 部署套件是由一個 *.zip*檔案所組成，其中包含在 IIS 中安裝網站所需的所有檔案和中繼資料。
- 建立部署套件，並使用命令列進行安裝。

您在先前的教學課程中完成以設定 Visual Studio 來自動化部署工作的程式，適用于這三種方法。 在這些教學課程中，您將使用這些方法的第一個。 如需使用部署套件的相關資訊，請參閱[ASP.NET 部署內容對應](https://msdn.microsoft.com/library/bb386521.aspx)。

在發佈之前，請確定您是以系統管理員模式執行 Visual Studio。 （在 Windows 7 的 [**開始**] 功能表中，以滑鼠右鍵按一下您所使用之 Visual Studio 版本的圖示，然後選取 [以**系統管理員身分執行**]）。只有當您要發行到本機電腦上的 IIS 時，才需要系統管理員模式。

在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案（而非 ContosoUniversity 專案），然後選取 [**發佈**]。

[**發行 Web** wizard] 隨即出現。

![Publish_Web_wizard_Profile_tab](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image9.png)

在下拉式清單中，選取 [ **&lt;新增]&gt;** 。

在 [**新增設定檔**] 對話方塊中，輸入 "Test"，然後按一下 **[確定]** 。

![New_Profile_dialog_box](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image10.png)

這個名稱與您稍早建立的 Web.config 轉換檔案中間節點相同。 這種對應會導致當您使用此設定檔發行時，將會套用 Web.config 轉換。

Wizard 會自動**前進到 [連線] 索引**標籤。

在 [**服務 URL** ] 方塊中，輸入*localhost*。

在 [**網站/應用程式**] 方塊中，輸入*Default Web Site/ContosoUniversity*。

在 [**目的地 URL** ] 方塊中，輸入 `http://localhost/ContosoUniversity`。

不需要 [**目的地 URL** ] 設定。 當 Visual Studio 完成部署應用程式時，它會自動開啟此 URL 的預設瀏覽器。 如果您不想要在部署後自動開啟瀏覽器，請將此方塊保留空白。

![Publish_Web_wizard_Connection_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image11.png)

按一下 [**驗證連接**]，確認設定正確，而且您可以連接到本機電腦上的 IIS。

綠色核取記號會確認連接是否成功。

![Publish_Web_wizard_Connection_tab_validated](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image12.png)

按 **[下一步**] 前進至 [**設定**] 索引標籤。

[設定] 下拉式方塊會指定要**部署的組建**設定。 預設值為 Release，這就是您想要的。

保留清除 [**移除目的地的其他**檔案] 核取方塊。 因為這是您的第一個部署，所以目的地資料夾中還沒有任何檔案。

在 [**資料庫**] 區段的 [連接字串] 方塊中，輸入**SchoolCoNtext**的下列值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample3.cmd)]

部署程式會將此連接字串放在已部署的 Web.config 檔案中，因為已選取 [**在執行時間使用此連接字串**]。

此外，在 [ **SchoolCoNtext**] 底下，選取 [套用**Code First 移轉**]。 此選項會讓部署程式設定已部署的 Web.config 檔案，以指定 `MigrateDatabaseToLatestVersion` 初始化運算式。 當應用程式在部署後第一次存取資料庫時，這個初始化運算式會自動將資料庫更新為最新版本。

在 [ **DefaultConnection**] 的 [連接字串] 方塊中，輸入下列值：

[!code-console[Main](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/samples/sample4.cmd)]

將**更新資料庫**保留為已清除。 成員資格資料庫的部署方式是將應用程式中的 .sdf 檔案複製\_資料，而您不想讓部署流程使用此資料庫執行任何其他動作。

![Publish_Web_wizard_Settings_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image13.png)

按 **[下一步**] 前進至 [**預覽**] 索引標籤。

在 [**預覽**] 索引標籤中，按一下 [**開始預覽**] 以查看將複製的檔案清單。

![Publish_Web_wizard_Preview_tab_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image14.png)

![Publish_Web_wizard_Preview_tab_Test_with_file_list](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image15.png)

按一下 [發行]。

如果 Visual Studio 不是在系統管理員模式中，您可能會收到指出許可權錯誤的錯誤訊息。 在此情況下，請關閉 Visual Studio，在系統管理員模式中開啟它，然後再次嘗試發佈。

如果 Visual Studio 處於系統管理員模式，[**輸出**] 視窗會報告 [成功的組建] 和 [發行]。

![Output_window_publish_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image16.png)

瀏覽器會自動開啟至在本機電腦上的 IIS 中執行的 Contoso 大學首頁。

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image17.png)

## <a name="testing-in-the-test-environment"></a>測試環境中的測試

請注意，環境指標會顯示 "（Test）"，而不是 "（Dev）"，這會顯示環境指標的*web.config 轉換成功*。

[![Home_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image19.png)

執行 [**學生**] 頁面，確認部署的資料庫沒有任何學生。 當您選取此頁面時，可能需要幾分鐘的時間才能載入，因為 Code First 會建立資料庫，然後執行 `Seed` 方法。 （因為應用程式尚未嘗試存取資料庫，所以不會在首頁上這麼做。）

[![Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image21.png)

執行 [**講師**] 頁面，確認 Code First 植入具有講師資料的資料庫：

[![Instructors_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image23.png)

從 [**學生**] 功能表選取 [**新增學生**]、新增學生，然後在 [**學生**] 頁面中查看新學生，以確認您可以成功寫入資料庫：

[![Add_Students_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image26.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image25.png)

[![Students_page_with_new_student_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image28.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image27.png)

從 [**課程**] 功能表中，選取 [**更新信用額度**]。 [**更新信用額度**] 頁面需要系統管理員許可權，因此會顯示 [**登入**] 頁面。 輸入您稍早建立的系統管理員帳號憑證（"admin" 和 "Pas $ w0rd"）。 隨即顯示 [**更新信用額度**] 頁面，確認您在上一個教學課程中建立的系統管理員帳戶已正確部署到測試環境。

[![Log_In_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image30.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image29.png)

[![Update_Credits_page_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image32.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image31.png)

確認只有包含預留位置檔案的*Elmah*資料夾存在。

[![Elmah_folder_Test](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image34.png)](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image33.png)

<a id="efcfmigrations"></a>

## <a name="reviewing-the-automatic-webconfig-changes-for-code-first-migrations"></a>檢查 Code First 移轉的自動 web.config 變更

在*C:\inetpub\wwwroot\ContosoUniversity*的已部署應用程式中開啟*web.config*檔案，您可以看到部署程式設定 Code First 移轉自動將資料庫更新為最新版本。

![](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image35.png)

部署程式也會為 Code First 移轉建立新的連接字串，以獨佔用來更新資料庫架構：

![DatabasePublish_connection_string](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12/_static/image36.png)

這個額外的連接字串可讓您指定資料庫架構更新的一個使用者帳戶，以及不同的使用者帳戶來存取應用程式資料。 例如，您可以將 db\_擁有者角色指派給 Code First 移轉，並將 db\_datareader 和 db\_資料寫入元角色指派給應用程式。 這是常見的深度防禦模式，可防止應用程式中可能的惡意程式碼變更資料庫架構。 （例如，這可能會發生在成功的 SQL 插入式攻擊中）。這些教學課程不會使用此模式。 它並不適用于 SQL Server Compact，而且當您在本系列稍後的教學課程中遷移至 SQL Server 時不適用。 Cytanium 網站只提供一個使用者帳戶來存取您在 Cytanium 建立的 SQL Server 資料庫。 如果您能夠在案例中執行此模式，您可以執行下列步驟來執行它：

1. 在 [**發行 Web** wizard] 的 [**設定**] 索引標籤中，輸入指定具有完整資料庫架構更新許可權之使用者的連接字串，然後清除 [**在執行時間使用此連接字串**] 核取方塊。 在已部署的 Web.config 檔案中，這會變成 `DatabasePublish` 連接字串。
2. 針對您希望應用程式在執行時間使用的連接字串，建立 Web.config 檔案轉換。

您現在已將應用程式部署至開發電腦上的 IIS，並在該處進行測試。 這會驗證部署程式是否已將應用程式的內容複寫到正確的位置（不包括您不想要部署的檔案），也會在部署期間正確地 Web Deploy 設定 IIS。 在下一個教學課程中，您將執行一項測試，尋找尚未完成的部署工作：設定*Elmah*資料夾的資料夾許可權。

## <a name="more-information"></a>更多資訊

如需在 Visual Studio 中執行 IIS 或 IIS Express 的詳細資訊，請參閱下列資源：

- [IIS Express](https://www.iis.net/learn/extensions/introduction-to-iis-express/iis-express-overview) IIS.net 網站上的總覽。
- [簡介 IIS Express](https://weblogs.asp.net/scottgu/archive/2010/06/28/introducing-iis-express.aspx) Scott Guthrie 的 blog。
- [如何：在 Visual Studio 中指定 Web 專案的 Web 服務器](https://msdn.microsoft.com/library/ms178108.aspx)。
- [IIS 與 ASP.NET 網站上的 ASP.NET 程式開發伺服器之間的核心差異](../deploying-web-site-projects/core-differences-between-iis-and-the-asp-net-development-server-cs.md)。
- 在 Rick Anderson 的 blog 的[30 秒內，于 IIS 7 上測試您的 ASP.NET MVC 或 Web Forms 應用程式](https://blogs.msdn.com/b/rickandy/archive/2011/04/22/test-you-asp-net-mvc-or-webforms-application-on-iis-7-in-30-seconds.aspx)。 此專案提供的範例會說明為何使用 Visual Studio 程式開發伺服器（Cassini）進行測試，不如 IIS Express 中的測試一樣可靠，而且在 IIS Express 中進行測試並不像在 IIS 中測試一樣可靠。

如需在您的應用程式以中度信任執行時可能會發生哪些問題的詳細資訊，請參閱 Rolla 網站上4人的[中級信任中的裝載 ASP.NET 應用程式](http://www.4guysfromrolla.com/articles/100307-1.aspx)。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-setting-folder-permissions-6-of-12.md)
