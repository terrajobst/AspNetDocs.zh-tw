---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：遷移至 SQL Server-10/12 |Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: a89d6f32-b71b-4036-8ff7-5f8ac2a6eca8
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12
msc.type: authoredcontent
ms.openlocfilehash: c5281a42596d95e725b32e652c75785abe0fd64e
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78573462"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-migrating-to-sql-server---10-of-12"></a>使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：遷移至 SQL Server-10/12

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

本教學課程說明如何從 SQL Server Compact 遷移至 SQL Server。 其中一個原因是，您可能會想要利用 SQL Server Compact 不支援的 SQL Server 功能，例如預存程式、觸發程式、視圖或複寫。 如需 SQL Server Compact 和 SQL Server 之間差異的詳細資訊，請參閱[部署 SQL Server Compact](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12.md)教學課程。

### <a name="sql-server-express-versus-full-sql-server-for-development"></a>SQL Server Express 與完整 SQL Server 以進行開發

一旦決定升級至 SQL Server 之後，您可能會想要在開發和測試環境中使用 SQL Server 或 SQL Server Express。 除了工具支援和資料庫引擎功能的差異之外，SQL Server Compact 和其他版本的 SQL Server 之間提供者的差異。 這些差異可能會導致相同的程式碼產生不同的結果。 因此，如果您決定將 SQL Server Compact 保留為開發資料庫，您應該在每次部署到生產環境之前，在測試環境中的 SQL Server 或 SQL Server Express 中徹底測試您的網站。

不同于 SQL Server Compact，SQL Server Express 基本上是相同的資料庫引擎，並使用與完整 SQL Server 相同的 .NET 提供者。 當您使用 SQL Server Express 進行測試時，您可以放心取得與 SQL Server 相同的結果。 您可以使用與 SQL Server Express 搭配使用的大部分相同資料庫工具，SQL Server （ [SQL Server Profiler](https://msdn.microsoft.com/library/ms181091.aspx)的值得注意的例外狀況），並支援其他 SQL Server 的功能，例如預存程式、視圖、觸發程式和複寫。 （不過，您通常必須在生產網站中使用完整的 SQL Server。 SQL Server Express 可以在共用的主控環境中執行，但它不是專為它所設計，而且許多主機提供者都不支援）。

如果您使用 Visual Studio 2012，通常會為您的開發環境選擇 SQL Server Express LocalDB，因為這是預設會隨 Visual Studio 安裝的內容。 不過，LocalDB 無法在 IIS 中運作，因此針對您的測試環境，您必須使用 SQL Server 或 SQL Server Express。

### <a name="combining-databases-versus-keeping-them-separate"></a>結合資料庫與保持獨立

Contoso 大學應用程式有兩個 SQL Server Compact 資料庫：成員資格資料庫（*aspnet .sdf*）和應用程式資料庫（*School .sdf*）。 當您遷移時，可以將這些資料庫移轉至兩個不同的資料庫或單一資料庫。 您可能想要結合這些專案，以便在應用程式資料庫與成員資格資料庫之間進行資料庫聯結。 您的主控方案也可能提供組合的原因。 例如，主機服務提供者可能會對多個資料庫收取更多費用，或甚至不允許一個以上的資料庫。 這就是在本教學課程中使用的 Cytanium Lite 主控帳戶的情況，只允許單一 SQL Server 資料庫。

在本教學課程中，您將以這種方式遷移兩個資料庫：

- 遷移至開發環境中的兩個 LocalDB 資料庫。
- 遷移至測試環境中的兩個 SQL Server Express 資料庫。
- 遷移至生產環境中的一個合併完整 SQL Server 資料庫。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="installing-sql-server-express"></a>安裝 SQL Server Express

SQL Server Express 預設會隨 Visual Studio 2010 自動安裝，但根據預設，它不會隨 Visual Studio 2012 一起安裝。 若要安裝 SQL Server 2012 Express，請按一下下列連結

- [SQL Server Express 2012](https://www.microsoft.com/download/details.aspx?id=29062)

選擇*繁體中文/x64/SQLEXPR\_x64\_繁體中文*或*繁體中文/x86/SQLEXPR\_x86\_繁體中文 .exe*，然後在安裝精靈中接受預設設定。 如需安裝選項的詳細資訊，請參閱[從安裝精靈安裝 SQL Server 2012 （安裝程式）](https://msdn.microsoft.com/library/ms143219.aspx)。

## <a name="creating-sql-server-express-databases-for-the-test-environment"></a>建立測試環境的 SQL Server Express 資料庫

下一步是建立 ASP.NET 成員資格和學校資料庫。

從  **View**  功能表選取 **伺服器總管**（Visual Web Developer 中的**資料庫總管**），然後以滑鼠右鍵按一下 **資料連線**，然後選取 **建立新的 SQL Server 資料庫**。

![Selecting_Create_New_SQL_Server_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image1.png)

在 [**建立新的 SQL Server 資料庫**] 對話方塊中，于 [**伺服器名稱**] 方塊中輸入 ".\SQLExpress"，並在 [**新資料庫名稱**] 方塊中輸入 "aspnet-Test"，然後按一下 **[確定]** 。

![Create_New_SQL_Server_Database_aspnet](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image2.png)

遵循相同的程式，建立名為「學校測試」的新 SQL Server Express School 資料庫。

（您會將「測試」附加至這些資料庫名稱，因為稍後您會針對開發環境建立每個資料庫的額外實例，而且您必須能夠區分這兩組資料庫）。

**伺服器總管**現在會顯示兩個新的資料庫。

![New_databases_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image3.png)

## <a name="creating-a-grant-script-for-the-new-databases"></a>建立新資料庫的授與腳本

當應用程式在開發電腦上的 IIS 中執行時，應用程式會使用預設應用程式集區的認證來存取資料庫。 不過，根據預設，應用程式集區識別沒有開啟資料庫的許可權。 因此，您必須執行腳本以授與該許可權。 在本節中，您會建立稍後將執行的腳本，以確保應用程式在 IIS 中執行時可以開啟資料庫。

在您于[部署到生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中建立的解決方案*SolutionFiles*資料夾中，建立名為*Grant .sql*的新 sql 檔案。 將下列 SQL 命令複製到檔案中，然後儲存並關閉檔案：

[!code-sql[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample1.sql)]

> [!NOTE]
> 此腳本是設計來搭配使用 SQL Server 2008 和 Windows 7 中的 IIS 設定，如同在本教學課程中所指定。 如果您使用不同版本的 SQL Server 或 Windows，或如果您在電腦上以不同的方式設定 IIS，則可能需要變更此腳本。 如需 SQL Server 腳本的詳細資訊，請參閱[SQL Server 線上叢書](https://go.microsoft.com/fwlink/?LinkId=132511)。

> [!NOTE] 
> 
> **安全性注意事項**此腳本會將資料庫\_擁有者許可權授與在執行時間存取資料庫的使用者，這就是您在生產環境中擁有的功能。 在某些情況下，您可能會想要指定具有完整資料庫架構更新許可權的使用者，只供部署之用，並為執行時間指定僅具有讀取和寫入資料許可權的其他使用者。 如需詳細資訊，請參閱在[部署至 IIS 作為測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)中，**檢查 Code First 移轉的自動 web.config 變更**。

## <a name="configuring-database-deployment-for-the-test-environment"></a>設定測試環境的資料庫部署

接下來，您將設定 Visual Studio，讓它針對每個資料庫執行下列工作：

- 產生 SQL 腳本，以在目的地資料庫中建立源資料庫的結構（資料表、資料行、條件約束等）。
- 產生 SQL 腳本，將源資料庫的資料插入目的地資料庫中的資料表。
- 在目的地資料庫中執行產生的腳本，以及您所建立的授與腳本。

開啟 [**專案屬性**] 視窗，然後選取 [**封裝/發行 SQL** ] 索引標籤。

請確定已**在 [設定**] 下拉式清單中選取 [使用中 **（發行）** ] 或 [**發行**]。

按一下 [**啟用此頁面**]。

![Package_Publish_SQL_tab_Enable_This_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image4.png)

[**封裝/發行 SQL** ] 索引標籤通常是停用的，因為它會指定舊版部署方法。 在大部分的情況下，您應該在 [**發行 Web** wizard] 中設定資料庫部署。 從 SQL Server Compact 遷移至 SQL Server 或 SQL Server Express 是一個特別的案例，此方法是不錯的選擇。

按一下 [從 web.config 匯**入**]。

![Selecting_Import_from_Web .config](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image5.png)

Visual Studio 會*在 web.config 檔案*中尋找連接字串，尋找一個用於成員資格資料庫，另一個用於 School 資料庫，並在**資料庫專案**資料表中加入一個對應于每個連接字串的資料列。 它所找到的連接字串適用于現有的 SQL Server Compact 資料庫，而下一個步驟則是設定這些資料庫的部署方式和位置。

您會在 [資料庫專案**詳細資料**] 區段中的 [**資料庫專案**] 資料表底下，輸入資料庫部署設定。 [**資料庫專案詳細資料**] 區段中顯示的設定，會與 [**資料庫專案**] 資料表中的任何資料列相關，如下圖所示。

![Database_Entry_Details_section_of_Package_Publish_SQL_tab](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image6.png)

### <a name="configuring-deployment-settings-for-the-membership-database"></a>設定成員資格資料庫的部署設定

選取 [**資料庫專案**] 資料表中的 [ **DefaultConnection-部署**] 資料列，以進行設定以套用至成員資格資料庫。

在 [**目的地資料庫的連接字串**] 中，輸入指向新 SQL Server Express 成員資格資料庫的連接字串。 您可以從**伺服器總管**取得所需的連接字串。 在**伺服器總管**中，展開 [**資料**連線] 並選取 [ **aspnetTest** ] 資料庫，然後從 [**屬性**] 視窗複製 [**連接字串**] 值。

![aspnet_connection_string_in_Server_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image7.png)

相同的連接字串會在此重現：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample2.cmd)]

在 [**封裝/發行 SQL** ] 索引標籤中，將此連接字串複製並貼到**目的地資料庫的連接字串**中。

請確定已選取 [**從現有資料庫提取資料及/或架構**]。 這會導致在目的地資料庫中自動產生並執行 SQL 腳本。

**源資料庫值的連接字串**會從*web.config*檔案中解壓縮，並指向開發 SQL Server Compact 資料庫。 這是將用來產生稍後將在目的地資料庫中執行之腳本的源資料庫。 由於您想要部署資料庫的實際執行版本，因此請將 "aspnet-Dev" 變更為 "aspnet-Prod"。

因為您想要複製資料（使用者帳戶和角色）以及資料庫結構，所以請將**資料庫腳本選項**從**架構**變更為**架構和資料**。

若要將部署設定為執行您稍早建立的授與腳本，您必須將它們新增至 [**資料庫腳本**] 區段。 按一下 [**新增腳本**]，然後在 [**加入 SQL 腳本**] 對話方塊中，流覽至您儲存授與腳本的資料夾（這是包含您的方案檔的資料夾）。 選取名為*Grant .sql*的檔案，然後按一下 [**開啟**]。

[![Select_File_dialog_box_grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image9.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image8.png)

[**資料庫專案**] 中 [ **DefaultConnection] 部署**資料列的設定現在看起來如下圖所示：

![Database_Entry_Details_for_DefaultConnection_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image10.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>配置 School 資料庫的部署設定

接下來，選取 [**資料庫專案**] 資料表中的 [ **SchoolCoNtext-部署**] 資料列，以便設定 School 資料庫的部署設定。

您可以使用先前所用的相同方法來取得新 SQL Server Express 資料庫的連接字串。 在 [**封裝/發行 SQL** ] 索引標籤中，將此連接字串複製到**目的地資料庫的連接字串**。

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample3.cmd)]

請確定已選取 [**從現有資料庫提取資料及/或架構**]。

**源資料庫值的連接字串**會從*web.config*檔案中解壓縮，並指向開發 SQL Server Compact 資料庫。 將 "School-Dev" 變更為 "School-Prod"，以部署資料庫的實際執行版本。 （您從未在\_Data 資料夾的應用程式中建立了 School-Prod .sdf 檔案，因此您稍後會從測試環境將該檔案複製到 ContosoUniversity 專案資料夾中的應用程式\_Data 資料夾）。

將**資料庫腳本選項**變更為**架構和資料**。

您也會想要執行腳本，將此資料庫的讀取和寫入權限授與應用程式集區身分識別，因此，請依照您為成員資格資料庫所做的方式新增*grant .sql*腳本檔。

當您完成時，**資料庫專案**中**SchoolCoNtext 部署**資料列的設定看起來會像下圖：

![Database_Entry_Details_for_SchoolCoNtext_Test](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image11.png)

將變更儲存至 [**封裝/發行 SQL** ] 索引標籤。

從*c:\inetpub\wwwroot\ContosoUniversity\App\_data*資料夾將*School-Prod .sdf*檔案複製到 ContosoUniversity 專案中的*應用程式\_data*資料夾。

### <a name="specifying-transacted-mode-for-the-grant-script"></a>指定授與腳本的交易模式

部署程式會產生可部署資料庫架構和資料的腳本。 根據預設，這些腳本會在交易中執行。 不過，自訂腳本（例如授與腳本）預設不會在交易中執行。 如果部署程式混合了交易模式，當腳本在部署期間執行時，您可能會收到逾時錯誤。 在本節中，您會編輯專案檔，以便將自訂腳本設定為在交易中執行。

在**方案總管**中，以滑鼠右鍵按一下**ContosoUniversity**專案，然後選取 **[卸載專案**]。

![Unload_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image12.png)

然後再次以滑鼠右鍵按一下專案，然後選取 [**編輯 ContosoUniversity**]。

![Edit_Project_in_Solution_Explorer](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image13.png)

[Visual Studio 編輯器] 會顯示專案檔的 XML 內容。 請注意，有數個 `PropertyGroup` 元素。 （在影像中，已省略 `PropertyGroup` 元素的內容）。

![專案檔案編輯器視窗](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image15.png)

第一個沒有 `Condition` 屬性的，就是適用于不論組建設定為何的設定。 一個 `PropertyGroup` 元素僅適用于 Debug 組建設定（請注意 `Condition` 屬性），一個僅適用于發行組建設定，另一個僅適用于測試組建設定。 在發行組建設定的 `PropertyGroup` 元素中，您會看到 `PublishDatabaseSettings` 元素，其中包含您在 [**封裝/發行 SQL** ] 索引標籤上輸入的設定。有一個 `Object` 元素對應到您指定的每個授與腳本（請注意兩個 "Grant. sql" 實例）。 根據預設，每個授與腳本的 `Source` 元素的 `Transacted` 屬性都會 `False`。

![Transacted_false](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image16.png)

將 `Source` 元素的 `Transacted` 屬性值變更為 [`True`]。

![Transacted_true](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image17.png)

儲存並關閉專案檔，然後以滑鼠右鍵按一下**方案總管**中的專案，然後選取 [**重載專案**]。

![Reload_project](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image18.png)

## <a name="setting-up-webconfig-transformations-for-the-connection-strings"></a>設定連接字串的 web.config 轉換

您在 [**封裝/發行 SQL** ] 索引標籤上輸入之新 SQL Express 資料庫的連接字串，僅供 Web Deploy 在部署期間用來更新目的地資料庫。 您仍然必須設定*web.config*轉換，*讓部署的 web.config 檔案*中的連接字串指向新的 SQL Server Express 資料庫。 （當您使用 [**封裝/發行 SQL** ] 索引標籤時，您無法在發行設定檔中設定連接字串）。

開啟*web.config* ，並將 `connectionStrings` 元素取代為下列範例中的 `connectionStrings` 元素。 （請確定您只複製 connectionStrings 元素，而不是此處顯示的周圍程式碼來提供內容）。

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample4.xml?highlight=2-11)]

此程式碼會在部署的*web.config*檔案中，取代每個 `add` 元素的 `connectionString` 和 `providerName` 屬性。 這些連接字串與您在 [**封裝/發行 SQL** ] 索引標籤中輸入的不同。已新增 "MultipleActiveResultSets = True" 設定，因為它是 Entity Framework 和 Universal Providers 的必要專案。

## <a name="installing-sql-server-compact"></a>安裝 SQL Server Compact

Entityframework.sqlservercompact NuGet 套件提供 Contoso 大學應用程式的 SQL Server Compact database engine 元件。 但是現在不是應用程式，但是 Web Deploy 必須能夠讀取 SQL Server Compact 資料庫，才能建立腳本以在 SQL Server 資料庫中執行。 若要讓 Web Deploy 讀取 SQL Server Compact 資料庫，請使用下列連結在開發電腦上安裝 SQL Server Compact： [Microsoft SQL Server Compact 4.0](https://www.microsoft.com/downloads/details.aspx?FamilyID=15F7C9B3-A150-4AD2-823E-E4E0DCF85DF6)。

## <a name="deploying-to-the-test-environment"></a>部署到測試環境

若要發行至測試環境，您必須建立發行設定檔，並將其設定為使用 [**封裝/發行 SQL** ] 索引標籤來發行資料庫，而不是發行設定檔資料庫設定。

首先，刪除現有的測試組態檔。

在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。

選取 [**設定檔**] 索引標籤。

按一下 [管理設定檔]。

選取 [**測試**]，按一下 [**移除**]，然後按一下 [**關閉**]。

關閉 [**發行 Web** wizard] 以儲存此變更。

接下來，建立新的測試組態檔，並使用它來發行專案。

在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。

選取 [**設定檔**] 索引標籤。

從下拉式清單中選取 **&lt;新增 ...&gt;** ，然後輸入 "Test" 作為設定檔名稱。

在 [**服務 URL** ] 方塊中，輸入*localhost*。

在 [**網站/應用程式**] 方塊中，輸入*Default Web Site/ContosoUniversity*。

在 [**目的地 URL** ] 方塊中，輸入 `http://localhost/ContosoUniversity/`。

按 [下一步]。

[**設定**] 索引標籤會警告您已設定 [**封裝/發行 SQL** ] 索引標籤，並可讓您按一下 [啟用新的資料庫發行增強功能] 來覆寫這些索引標籤。 在此部署中，您不想要覆寫 [**封裝/發行 SQL** ] 索引標籤設定，因此只要按 **[下一步**]。

![Publish_Web_wizard_Settings_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image19.png)

[**預覽**] 索引標籤上的訊息指出**未選取要發行的任何資料庫**，但這只表示發行設定檔中未設定資料庫發行。

按一下 [發行]。

![Publish_Web_wizard_Preview_tab_Migrate](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image20.png)

Visual Studio 部署應用程式，並在測試環境中將瀏覽器開啟至網站的首頁。 執行 [講師] 頁面，以查看它是否顯示您稍早看到的相同資料。 執行 [**新增學生**] 頁面，新增學生，然後在 [**學生**] 頁面中查看新學生。 這會確認您可以更新資料庫。 選取 [**更新信用額度**] 頁面（您必須登入）以確認成員資格資料庫已部署，而且您有其存取權。

## <a name="creating-a-sql-server-database-for-the-production-environment"></a>建立生產環境的 SQL Server 資料庫

現在您已部署到測試環境，您已準備好設定部署到生產環境。 您可以藉由建立要部署的資料庫來開始進行測試環境。 當您從總覽中回想過，Cytanium Lite 主控方案只允許單一 SQL Server 資料庫，因此您只會設定一個資料庫，而不是兩個。 成員資格和學校 SQL Server Compact 資料庫中的所有資料表和資料，都會部署到生產環境中的一個 SQL Server 資料庫。

移至[http://panel.cytanium.com](http://panel.cytanium.com)的 [Cytanium] 控制台。 按住滑鼠停留在**資料庫**上，然後按一下 [ **SQL Server 2008**]。

[![Selecting_Databases_in_Control_Panel](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image22.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image21.png)

在 [ **SQL Server 2008** ] 頁面中，按一下 [**建立資料庫**]。

[![Selecting_Create_Database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image24.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image23.png)

將資料庫命名為 "School"，然後按一下 [**儲存**]。 （此頁面會自動新增前置詞 "contosou"，因此有效的名稱會是 "contosouSchool"）。

[![Naming_the_database](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image26.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image25.png)

在相同的頁面上，按一下 [**建立使用者**]。 在 Cytanium 的伺服器上，而不是使用整合式 Windows 安全性，並讓應用程式集區身分識別開啟您的資料庫，您將建立有權開啟資料庫的使用者。 您會將使用者的認證加入至生產*web.config*檔案中的連接字串。 在此步驟中，您會建立這些認證。

[![Creating_a_database_user](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image28.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image27.png)

在 [ **SQL 使用者屬性**] 頁面中填入必要的欄位：

- 輸入 "ContosoUniversityUser" 作為名稱。
- 輸入密碼。
- 選取 [ **contosouSchool** ] 做為預設資料庫。
- 選取 [ **contosouSchool** ] 核取方塊。

[![SQL_User_Properties_page](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image30.png)](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image29.png)

## <a name="configuring-database-deployment-for-the-production-environment"></a>設定生產環境的資料庫部署

現在您已準備好在 [**封裝/發行 SQL** ] 索引標籤中設定資料庫部署設定，如同您先前在測試環境中所做的一樣。

開啟 [**專案屬性**] 視窗，選取 [**封裝/發行 SQL** ] 索引標籤，並確定已選取 [設定] 下拉式清單中**的 [使用**中 **（發行）** ] 或 [**發行**]。

當您設定每個資料庫的部署設定時，您在生產和測試環境中所做的主要差異在於如何設定連接字串。 針對測試環境，您輸入了不同的目的地資料庫連接字串，但在生產環境中，這兩個資料庫的目的地連接字串都相同。 這是因為您要將這兩個資料庫部署到生產環境中的一個資料庫。

### <a name="configuring-deployment-settings-for-the-membership-database"></a>設定成員資格資料庫的部署設定

若要設定套用至成員資格資料庫的設定，請選取 [**資料庫專案**] 資料表中的 [ **DefaultConnection-部署**] 資料列。

在 [**目的地資料庫的連接字串**] 中，輸入指向您剛才建立之新生產 SQL Server 資料庫的連接字串。 您可以從歡迎電子郵件取得連接字串。 電子郵件的相關部分包含下列範例連接字串：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample5.cmd)]

取代三個變數之後，您所需的連接字串看起來就像下面這個範例：

[!code-console[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample6.cmd)]

在 [**封裝/發行 SQL** ] 索引標籤中，將此連接字串複製並貼到**目的地資料庫的連接字串**中。

請確定仍然選取**現有資料庫中的提取資料和/或架構**，而且**資料庫腳本選項**仍然是**架構和資料**。

在 [**資料庫腳本**] 方塊中，清除 [Grant. sql 腳本] 旁的核取方塊。

![Disable_Grant_script](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/_static/image31.png)

### <a name="configuring-deployment-settings-for-the-school-database"></a>配置 School 資料庫的部署設定

接下來，選取 [**資料庫專案**] 資料表中的 [ **SchoolCoNtext-部署**] 資料列，以便設定 School 資料庫設定。

將相同的連接字串複製到您為成員資格資料庫複製到該欄位之**目的地資料庫的連接字串**中。

請確定仍然選取**現有資料庫中的提取資料和/或架構**，而且**資料庫腳本選項**仍然是**架構和資料**。

在 [**資料庫腳本**] 方塊中，清除 [Grant. sql 腳本] 旁的核取方塊。

將變更儲存至 [**封裝/發行 SQL** ] 索引標籤。

## <a name="setting-up-webconfig-transforms-for-the-connection-strings-to-production-databases"></a>將連接字串的 web.config 轉換設定為生產資料庫

接下來，您將設定*web.config*轉換，*讓部署的 web.config 檔案*中的連接字串指向新的實際執行資料庫。 您在 [**封裝/發行 SQL** ] 索引標籤上輸入以供 Web Deploy 使用的連接字串，與應用程式所需使用的連接字串相同，但新增 [`MultipleResultSets`] 選項除外。

開啟*web.config* ，並將 `connectionStrings` 元素取代為如下列範例所示的 `connectionStrings` 元素。 （只複製 `connectionStrings` 專案，而不是提供用來顯示內容的周圍標記）。

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample7.xml?highlight=2-11)]

您有時會看到通知，告訴您一律加密*web.config*檔案中的連接字串。 如果您要部署到自己公司網路上的伺服器，這可能是適當的。 不過，當您要部署至共用的裝載環境時，您會信任主控提供者的安全性作法，而不需要或實際加密連接字串。

## <a name="deploying-to-the-production-environment"></a>部署到生產環境

現在您已經準備好部署到生產環境。 Web Deploy 會讀取您專案之*應用程式*中的 SQL Server Compact 資料庫\_[Data] 資料夾，然後在生產 SQL Server 資料庫中重新建立其所有資料表和資料。 若要使用 [**封裝/發行 Web** ] 索引標籤設定進行發佈，您必須為生產環境建立新的發行設定檔。

首先，刪除現有的生產設定檔，如同您稍早在測試組態檔中所做的一樣。

在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。

選取 [**設定檔**] 索引標籤。

按一下 [管理設定檔]。

選取 [**生產**]，按一下 [**移除**]，然後按一下 [**關閉**]。

關閉 [**發行 Web** wizard] 以儲存此變更。

接下來，建立新的生產設定檔，並使用它來發行專案。

在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後按一下 [**發佈**]。

選取 [**設定檔**] 索引標籤。

按一下 [匯**入**]，然後選取您稍早下載的 .publishsettings 檔案。

在 [**連接**] 索引標籤上，將 [**目的地 URL** ] 變更為正確的暫存 url，在此範例中為 http://contosouniversity.com.vserver01.cytanium.com。

將設定檔重新命名為生產環境。 （選取 [**設定檔**] 索引標籤，然後按一下 [**管理設定檔**] 來這麼做）。

關閉 [**發行 Web** wizard] 以儲存變更。

在實際的應用程式中，如果是在生產環境中更新資料庫，您現在可以在發行之前執行兩個額外步驟：

1. 如[部署到生產環境](deployment-to-a-hosting-provider-deploying-to-the-production-environment-7-of-12.md)教學課程中所示，上傳*應用程式\_離線 .htm*。
2. 使用 [Cytanium] 控制台的 [**檔案管理員**] 功能，將*aspnet-Prod*和*School-Prod .sdf*檔案從生產網站複製到 ContosoUniversity 專案的*應用程式\_Data*資料夾。 這可確保您要部署到新 SQL Server 資料庫的資料包含生產網站所進行的最新更新。

在 Web 單鍵的 [**發佈**] 工具列中，確定已選取 [**生產**設定檔]，然後按一下 [**發佈**]。

如果您在發佈之前將<em>應用程式\_離線</em>，您必須使用 [Cytanium 控制台] 中的 [<strong>檔案管理員</strong>] 公用程式來刪除<em>離線應用程式\_。</em>在測試之前的 .htm。 同時，您也可以將應用程式中的<em>.sdf</em>檔案從<em>\_Data</em>資料夾中刪除。

您現在可以開啟瀏覽器，並移至公用網站的 URL 來測試應用程式，方法與部署至測試環境的方式相同。

## <a name="switching-to-sql-server-express-localdb-in-development"></a>切換至開發中的 SQL Server Express LocalDB

如總覽中所述，通常最好是在開發中使用您在測試和生產環境中使用的相同資料庫引擎。 （請記住，在開發中使用 SQL Server Express 的優點是，資料庫在開發、測試和生產環境中的運作方式都相同）。在本節中，您將設定當您從 Visual Studio 執行應用程式時，要使用 SQL Server Express LocalDB 的 ContosoUniversity 專案。

執行此遷移的最簡單方式是讓 Code First 和成員資格系統為您建立新的開發資料庫。 使用此方法進行遷移需要三個步驟：

1. 變更連接字串以指定新的 SQL Express LocalDB 資料庫。
2. 執行網站管理工具來建立系統管理員使用者。 這會建立成員資格資料庫。
3. 使用 Code First 移轉的 [更新資料庫] 命令來建立和植入應用程式資料庫。

### <a name="updating-connection-strings-in-the-webconfig-file"></a>更新 Web.config 檔案中的連接字串

開啟*web.config*檔案，並以下列程式碼取代 `connectionStrings` 元素：

[!code-xml[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample8.xml)]

### <a name="creating-the-membership-database"></a>建立成員資格資料庫

在**方案總管**中，選取 [ContosoUniversity] 專案，然後按一下 [**專案**] 功能表中的 [ **ASP.NET**設定]。

選取 [安全性] 索引標籤。

按一下 [**建立或管理角色**]，然後建立**系統管理員**角色。

返回 [安全性] 索引標籤。

按一下 [**建立使用者**]，然後選取 [**系統管理員**] 核取方塊，並建立名為 admin 的使用者。

關閉 [網站**管理工具**]。

### <a name="creating-the-school-database"></a>建立 School 資料庫

開啟 [套件管理員主控台] 視窗。

在 [**預設專案**] 下拉式清單中，選取 [ContosoUniversity] 專案。

輸入下列命令：

[!code-powershell[Main](deployment-to-a-hosting-provider-migrating-to-sql-server-10-of-12/samples/sample9.ps1)]

Code First 移轉會套用建立資料庫的初始遷移，然後套用 AddBirthDate 遷移，然後執行種子方法。

按下 Ctrl F5 來執行網站。 如同您在測試和生產環境中所做的一樣，執行 [**新增學生**] 頁面，新增學生，然後在 [**學生**] 頁面中查看新的學生。 這會驗證 School 資料庫是否已建立並初始化，以及您是否擁有它的讀取和寫入存取權。

選取 [**更新信用額度**] 頁面並登入，以確認成員資格資料庫已部署，而且您有其存取權。 如果您未遷移您的使用者帳戶，請建立系統管理員帳戶，然後選取 [**更新信用額度**] 頁面，以驗證其是否正常運作。

## <a name="cleaning-up-sql-server-compact-files"></a>清理 SQL Server Compact 檔案

您不再需要包含的檔案和 NuGet 套件來支援 SQL Server Compact。 如果您想要（不需要此步驟），您可以清除不必要的檔案和參考。

在**方案總管**中，將來自*應用程式*的 *.sdf*檔案從 [ *Bin* ] 資料夾中刪除\_[Data] 資料夾和 [ *amd64* ] 和 [ *x86* ] 資料夾。

在**方案總管**中，以滑鼠右鍵按一下方案（不是其中一個專案），然後按一下 [**管理方案的 NuGet 套件**]。

在 [**管理 NuGet 封裝**] 對話方塊的左窗格中，選取 [**已安裝的封裝**]。

選取 [ **EntityFramework entityframework.sqlservercompact** ] 套件，然後按一下 [**管理**]。

在 [**選取專案**] 對話方塊中，會選取這兩個專案。 若要卸載這兩個專案中的封裝，請清除這兩個核取方塊，然後按一下 **[確定]** 。

在詢問您是否也要卸載相依套件的對話方塊中，按一下 [否]。 其中一個是您必須保留的 Entity Framework 套件。

遵循相同的程式來卸載**entityframework.sqlservercompact**套件。 （必須依照此順序卸載封裝，因為**EntityFramework. entityframework.sqlservercompact**套件相依于**entityframework.sqlservercompact**套件）。

您現在已成功遷移至 SQL Server Express 和完整 SQL Server。 在下一個教學課程中，您將會進行另一個資料庫變更，而您將瞭解如何在測試和實際執行資料庫使用 SQL Server Express 和完整 SQL Server 時，部署資料庫變更。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-deploying-a-sql-server-database-update-11-of-12.md)
