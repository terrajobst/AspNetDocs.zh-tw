---
uid: web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
title: 使用 Visual Studio ASP.NET Web 部署：準備進行資料庫部署 |Microsoft Docs
author: tdykstra
description: 本教學課程系列將示範如何透過互動，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商主機服務提供者。
ms.author: riande
ms.date: 02/15/2013
ms.assetid: ae4def81-fa37-4883-a13e-d9896cbf6c36
msc.legacyurl: /web-forms/overview/deployment/visual-studio-web-deployment/preparing-databases
msc.type: authoredcontent
ms.openlocfilehash: cdcb3578725c41e3c801afd54e6d34455bc4b281
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78636994"
---
# <a name="aspnet-web-deployment-using-visual-studio-preparing-for-database-deployment"></a>使用 Visual Studio ASP.NET Web 部署：準備進行資料庫部署

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://go.microsoft.com/fwlink/p/?LinkId=282627)

> 本教學課程系列說明如何使用 Visual Studio 2012 或 Visual Studio 2010，將 ASP.NET web 應用程式部署（發佈）至 Azure App Service Web Apps 或協力廠商裝載提供者。 如需有關數列的詳細資訊，請參閱[本系列的第一個教學](introduction.md)課程。

## <a name="overview"></a>概觀

本教學課程說明如何準備專案以進行資料庫部署。 在應用程式的兩個資料庫中，資料庫結構和部分（而非全部）的資料必須部署到測試、預備和生產環境。

一般而言，當您開發應用程式時，您會將測試資料輸入至您不想要部署到即時網站的資料庫中。 不過，您可能也會有一些您想要部署的生產環境資料。 在本教學課程中，您將設定 Contoso 大學專案並準備 SQL 腳本，以便在部署時包含正確的資料。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](troubleshooting.md)。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

範例應用程式會使用 SQL Server Express LocalDB。 SQL Server Express 是 SQL Server 的免費版本。 它通常是在開發期間使用，因為它是以與完整版本 SQL Server 相同的資料庫引擎為基礎。 您可以使用 SQL Server Express 進行測試，並確保應用程式在生產環境中會有相同的行為，但不同于 SQL Server 版本的功能有一些例外狀況。

LocalDB 是 SQL Server Express 的特殊執行模式，可讓您使用資料庫做為 *.mdf*檔案。 LocalDB 資料庫檔案通常會保留在 Web 專案的*應用程式\_Data*資料夾中。 SQL Server Express 中的使用者實例功能也可讓您使用 *.mdf*檔案，但是使用者實例功能已被取代;因此，建議使用 LocalDB 來處理 *.mdf*檔案。

通常 SQL Server Express 不會用於生產 web 應用程式。 不建議將 LocalDB 用於與 web 應用程式搭配使用的生產環境，因為它不是設計用於 IIS。

在 Visual Studio 2012 中，預設會隨 Visual Studio 安裝 LocalDB。 在 Visual Studio 2010 和舊版中，預設會使用 Visual Studio 安裝 SQL Server Express （不含 LocalDB）;這就是為什麼您將它安裝為[本系列第一個教學](introduction.md)課程中的其中一個必要條件。

如需 SQL Server 版本的詳細資訊，包括 LocalDB，請參閱下列[使用 SQL Server 資料庫](../../../../whitepapers/aspnet-data-access-content-map.md#sqlserver)的資源。

## <a name="entity-framework-and-universal-providers"></a>Entity Framework 和 Universal Providers

針對資料庫存取，Contoso 大學應用程式需要必須與應用程式一起部署的下列軟體，因為它不包含在 .NET Framework 中：

- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) （可讓 ASP.NET 成員資格系統使用 Azure SQL Database）
- [Entity Framework](https://msdn.microsoft.com/library/gg696172.aspx)

因為此套裝軟體含在 NuGet 套件中，所以已設定專案，以便將必要的元件與專案一起部署。 （連結會指向這些套件的目前版本，這可能比您在本教學課程中下載的入門專案中所安裝的版本還新）。

如果您要部署到協力廠商主機服務提供者，而不是 Azure，請確定您使用 Entity Framework 5.0 或更新版本。 舊版的 Code First 移轉需要完全信任，而且大部分的主控提供者都會以中等信任執行您的應用程式。 如需有關中度信任的詳細資訊，請參閱[部署至 IIS 作為測試環境](deploying-to-iis.md)教學課程。

## <a name="configure-code-first-migrations-for-application-database-deployment"></a>設定應用程式資料庫部署的 Code First 移轉

Contoso 大學應用程式資料庫是由 Code First 管理，您將使用 Code First 移轉加以部署。 如需使用 Code First 移轉進行資料庫部署的總覽，請參閱[本系列的第一個教學](introduction.md)課程。

當您部署應用程式資料庫時，通常不會只是將您的開發資料庫與其所有資料一起部署到生產環境，因為其中有許多資料可能僅供測試之用。 例如，測試資料庫中的學生名稱是虛構的。 另一方面，您通常無法只部署資料庫結構，完全沒有資料。 測試資料庫中的某些資料可能是實際的資料，當使用者開始使用應用程式時，就必須存在。 例如，您的資料庫可能會有一個資料表，其中包含有效的等級值或實際部門名稱。

若要模擬這個常見的案例，您將設定 Code First 移轉 `Seed` 方法，只將您想要在生產環境中的資料插入資料庫中。 這個 `Seed` 方法不應該插入測試資料，因為它會在生產環境中 Code First 建立資料庫之後，于生產環境中執行。

在之前的 Code First 版本中，在發行之前，`Seed` 方法也經常插入測試資料，因為在開發期間，資料庫必須完全刪除並從頭重新建立。 使用 Code First 移轉，在資料庫變更之後會保留測試資料，因此不需要在 `Seed` 方法中包含測試資料。 您下載的專案會使用的方法，將所有資料包含在初始化運算式類別的 `Seed` 方法中。 在本教學課程中，您將停用該初始化運算式類別並啟用遷移。 接著，您將更新「遷移」設定類別中的 `Seed` 方法，使其只插入您想要在生產環境中插入的資料。

下圖說明應用程式資料庫的架構：

[![School_database_diagram](preparing-databases/_static/image2.png)](preparing-databases/_static/image1.png)

在這些教學課程中，您會假設在第一次部署網站時，`Student` 和 `Enrollment` 資料表應該是空的。 其他資料表包含應用程式上線時必須預先載入的資料。

### <a name="disable-the-initializer"></a>停用初始化運算式

由於您將使用 Code First 移轉，因此不需要使用 `DropCreateDatabaseIfModelChanges` Code First 初始化運算式。 這個初始化運算式的程式碼位於 ContosoUniversity 專案的*SchoolInitializer.cs*檔案中。 當應用程式第一次嘗試存取資料庫時 *，web.config 檔案*的 `appSettings` 元素中的設定會使此初始化運算式執行：

[!code-xml[Main](preparing-databases/samples/sample1.xml?highlight=3)]

開啟*應用程式的 web.config 檔案*，並移除或批註指定 Code First 初始化運算式類別的 `add` 元素。 `appSettings` 元素現在看起來像這樣：

[!code-xml[Main](preparing-databases/samples/sample2.xml)]

> [!NOTE]
> 另一種指定初始化運算式類別的方法，就是在*global.asax*檔案的 `Application_Start` 方法中呼叫 `Database.SetInitializer`。 如果您要在使用該方法來指定初始化運算式的專案中啟用遷移，請移除該程式程式碼。

> [!NOTE]
> 如果您使用 Visual Studio 2013，請在 PMC 中的步驟2和3：（a）之間新增下列步驟，並輸入 "update-package entityframework-版本 6.1.1" 以取得 EF 的目前版本。 然後（b）建立專案以取得組建錯誤的清單，並加以修正。 刪除已不存在之命名空間的 using 語句，以滑鼠右鍵按一下並按一下 [解析]，以加入所需的 using 語句，並將 EntityState 的出現變更為 EntityState。

### <a name="enable-code-first-migrations"></a>啟用 Code First 移轉

1. 請確定 ContosoUniversity 專案（而非 ContosoUniversity）已設定為啟始專案。 在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後選取 [**設定為啟始專案**]。 Code First 移轉會在啟始專案中尋找資料庫連接字串。
2. 從 [**工具**] 功能表中，選擇 [ **NuGet 套件管理員**] > [**套件管理員主控台**]。

    ![Selecting_Package_Manager_Console](preparing-databases/_static/image3.png)
3. 在 [**套件管理員主控台**] 視窗的頂端，選取 [ContosoUniversity] 做為預設專案，然後在 `PM>` 提示字元輸入「啟用-遷移」。

    ![啟用-遷移命令](preparing-databases/_static/image4.png)

    （如果您收到錯誤，指出無法辨識 [*啟用-遷移*] 命令，請輸入命令*更新-封裝 EntityFramework-重新安裝*，然後再試一次）。

    此命令會在 ContosoUniversity 專案中建立一個 [*遷移*] 資料夾，並在該資料夾中放入兩個檔案：您可以用來設定遷移的*Configuration.cs*檔案，以及用於建立資料庫之第一個遷移的*InitialCreate.cs*檔案。

    ![[遷移] 資料夾](preparing-databases/_static/image5.png)

    您已在 [**套件管理員主控台**] 的 [**預設專案**] 下拉式清單中選取 DAL 專案，因為 `enable-migrations` 命令必須在包含 Code First 內容類別的專案中執行。 當該類別在類別庫專案中時，Code First 移轉會在方案的啟始專案中尋找資料庫連接字串。 在 ContosoUniversity 方案中，Web 專案已設定為啟始專案。 如果您不想要將具有連接字串的專案指定為 Visual Studio 中的啟始專案，您可以在 PowerShell 命令中指定啟始專案。 若要查看命令語法，請輸入命令 `get-help enable-migrations`。

    `enable-migrations` 命令會自動建立第一次遷移，因為資料庫已經存在。 另一個替代方式是讓遷移建立資料庫。 若要這麼做，請在啟用遷移之前，使用**伺服器總管**或**SQL Server 物件總管**來刪除 ContosoUniversity 資料庫。 啟用遷移之後，請輸入「新增-遷移 InitialCreate」命令，手動建立第一次遷移。 然後，您可以輸入「更新-資料庫」命令來建立資料庫。

### <a name="set-up-the-seed-method"></a>設定種子方法

在本教學課程中，您將藉由將程式碼加入至 Code First 移轉 `Configuration` 類別的 `Seed` 方法來新增固定資料。 Code First 移轉會在每次遷移後呼叫 `Seed` 方法。

由於 `Seed` 方法會在每次遷移之後執行，因此，在第一次遷移之後，資料表中已經有資料。 若要處理這種情況，您將使用 `AddOrUpdate` 方法來更新已經插入的資料列，或插入它們（如果尚未存在的話）。 `AddOrUpdate` 的方法可能不是您案例的最佳選擇。 如需詳細資訊，請參閱 Julie Lerman 的 blog 上的[處理 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

1. 開啟*Configuration.cs*檔案，並將 `Seed` 方法中的批註取代為下列程式碼：

    [!code-csharp[Main](preparing-databases/samples/sample3.cs)]
2. `List` 的參考在其底下有紅色曲線，因為您還沒有其命名空間的 `using` 語句。 以滑鼠右鍵按一下其中一個 `List` 實例，然後按一下 [**解析**]，再按一下 [**使用 system.object**]。

    ![使用 using 語句來解析](preparing-databases/_static/image6.png)

    此功能表選取專案會將下列程式碼加入至靠近檔案頂端的 `using` 語句。

    [!code-csharp[Main](preparing-databases/samples/sample4.cs)]
3. 按下 CTRL-SHIFT-B 以建立專案。

專案現在已準備好部署*ContosoUniversity*資料庫。 當您部署應用程式之後，第一次執行它並流覽至存取資料庫的頁面時，Code First 會建立資料庫，並執行這個 `Seed` 方法。

> [!NOTE]
> 將程式碼加入至 `Seed` 方法是您可以將固定資料插入資料庫的許多方式之一。 替代方法是將程式碼新增至每個遷移類別的 `Up` 和 `Down` 方法。 `Up` 和 `Down` 方法包含可執行資料庫變更的程式碼。 您會在[部署資料庫更新](deploying-a-database-update.md)教學課程中看到它們的範例。
> 
> 您也可以使用 `Sql` 方法，撰寫執行 SQL 語句的程式碼。 例如，如果您已將預算資料行新增至部門資料表，而且想要在遷移過程中將所有部門預算初始化為 $1000.00，您可以將下列程式程式碼新增至該遷移的 `Up` 方法：
> 
> `Sql("UPDATE Department SET Budget = 1000");`

## <a name="create-scripts-for-membership-database-deployment"></a>建立成員資格資料庫部署的腳本

Contoso 大學應用程式會使用 ASP.NET 成員資格系統和表單驗證來驗證和授權使用者。 只有在系統管理員角色中的使用者，才能存取 [**更新信用額度**] 頁面。

執行應用程式並按一下 [**課程**]，然後按一下 [**更新信用額度**]。

![按一下 [更新信用額度]](preparing-databases/_static/image7.png)

[**登入**] 頁面會出現，因為 [**更新信用額度**] 頁面需要系統管理許可權。

輸入*admin*作為 [使用者名稱] 並*devpwd*為 [密碼]，然後按一下 [**登入**]。

![登入頁面](preparing-databases/_static/image8.png)

[**更新信用額度**] 頁面隨即出現。

![更新信用額度頁面](preparing-databases/_static/image9.png)

使用者和角色資訊位於*ContosoUniversity*資料庫中，由*web.config*檔案中的**DefaultConnection**連接字串所指定。

此資料庫不是由 Entity Framework Code First 管理，因此您無法使用遷移來進行部署。 您將使用 dbDacFx 提供者來部署資料庫架構，而您將設定發行設定檔，以執行將初始資料插入資料庫資料表的腳本。

> [!NOTE]
> Visual Studio 2013 引進了新的 ASP.NET 成員資格系統（現在名為 ASP.NET Identity）。 新系統可讓您將應用程式和成員資格資料表保留在相同的資料庫中，而且您可以使用 Code First 移轉部署兩者。 範例應用程式會使用先前的 ASP.NET 成員資格系統，而無法使用 Code First 移轉進行部署。 部署這個成員資格資料庫的程式也適用于您的應用程式需要部署不是由 Entity Framework Code First 所建立之 SQL Server 資料庫的任何其他案例。

此外，您通常不會想要在開發環境中使用相同的資料。 當您第一次部署網站時，通常會排除您為測試所建立的大部分或所有使用者帳戶。 因此，下載的專案有兩個成員資格資料庫： *aspnet-ContosoUniversity*與開發使用者和*aspnet-ContosoUniversity-Prod*搭配生產使用者。 在本教學課程中，兩個資料庫中的使用者名稱都相同： *admin*和*nonadmin*。 這兩個使用者在開發資料庫中都有*devpwd*的密碼，而在生產資料庫中則是*prodpwd* 。

您會將開發使用者部署到測試環境，並將實際執行使用者部署至預備和生產環境。 若要這麼做，您將在本教學課程中建立兩個 SQL 腳本，一個用於開發，另一個用於生產環境，在稍後的教學課程中，您將設定發佈程式來執行它們。

> [!NOTE]
> 成員資格資料庫會儲存帳戶密碼的雜湊。 若要將帳戶從一部機器部署到另一台電腦，您必須確定雜湊常式不會在目的地伺服器上產生與來源電腦上不同的雜湊。 當您使用 ASP.NET Universal Providers 時，它們會產生相同的雜湊，前提是您不會變更預設演算法。 預設演算法為 HMACSHA256，而且是在 web.config 檔案中 **[machineKey](https://msdn.microsoft.com/library/system.web.configuration.machinekeysection.aspx)** 元素的**驗證**屬性中指定。

您可以手動建立資料部署腳本，方法是使用 SQL Server Management Studio （SSMS），或使用協力廠商工具。 本教學課程的其餘部分將示範如何在 SSMS 中執行此作業，但如果您不想要安裝和使用 SSMS，您可以從專案的已完成版本取得腳本，並跳至您將它們儲存在方案資料夾中的區段。

若要安裝 SSMS，請從[下載中心安裝它： Microsoft SQL Server 2012 Express](https://www.microsoft.com/download/details.aspx?id=29062) ，請按一下[ENU\x64\SQLManagementStudio\_x64\_繁體中文](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x64/SQLManagementStudio_x64_ENU.exe)或[ENU\x86\SQLManagementStudio\_x86\_繁體中文](https://download.microsoft.com/download/8/D/D/8DD7BDBA-CEF7-4D8E-8C16-D9F69527F909/ENU/x86/SQLManagementStudio_x86_ENU.exe)。 如果您為系統選擇錯誤的帳戶，將無法安裝，而且您可以嘗試另一個。

（請注意，這是 600 mb 的下載。 可能需要很長的時間才能安裝，而且需要重新開機電腦。）

在 SQL Server 安裝中心 的第一頁上，按一下 **新增 SQL Server 獨立安裝或將功能加入至現有安裝**，然後依照指示接受預設選項。

### <a name="create-the-development-database-script"></a>建立開發資料庫腳本

1. 執行 SSMS。
2. 在 [**連接到伺服器**] 對話方塊中，輸入 *（localdb） \V11.0*做**為伺服器名稱**，將 [**驗證**] 設定為 [ **Windows 驗證**]，然後按一下 **[連接]** 。

    ![SSMS 連接到伺服器](preparing-databases/_static/image10.png)
3. 在 [**物件總管**] 視窗中，展開 [**資料庫**]，以滑鼠**按右鍵 [** **aspnet-ContosoUniversity**]，按一下 [工作]，然後按一下 [**產生腳本**]。

    ![SSMS 產生腳本](preparing-databases/_static/image11.png)
4. 在 [**產生和發佈腳本**] 對話方塊中，按一下 [**設定腳本編寫選項**]。

    您可以略過 [**選擇物件**] 步驟，因為預設值是 [**編寫整個資料庫的腳本] 和 [所有資料庫物件**]，以及您想要的內容。
5. 按一下 **[進階]** 。

    ![SSMS 腳本選項](preparing-databases/_static/image12.png)
6. 在 [ **Advanced 腳本選項**] 對話方塊中，向下流覽至 [**要編寫腳本的資料類型**]，然後按一下下拉式清單中的 [**僅限資料**] 選項。
7. 將 [**腳本使用資料庫**] 變更為**False**。 USE 語句對 Azure SQL Database 而言無效，而且不需要在測試環境中 SQL Server Express 部署。

    ![僅 SSMS 腳本資料，沒有 USE 語句](preparing-databases/_static/image13.png)
8. 按一下 [確定]。
9. 在 [**產生和發佈腳本**] 對話方塊中，[**檔案名**] 方塊指定將建立腳本的位置。 將您方案資料夾的路徑（具有 ContosoUniversity .sln 檔案的資料夾）和檔案名變更為*aspnet-data-dev。*
10. 按 **[下一步**] 移至 [**摘要**] 索引標籤，然後再按 **[下一步]** 以建立腳本。

    ![已建立 SSMS 腳本](preparing-databases/_static/image14.png)
11. 按一下 [完成] **Walkthrough: Calling Code in an VSTO Add-in from VBA**。

### <a name="create-the-production-database-script"></a>建立生產環境資料庫腳本

由於您尚未以生產資料庫執行專案，因此它還不會附加到 LocalDB 實例。 因此，您必須先附加資料庫。

1. 在 SSMS**物件總管**中，以滑鼠右鍵按一下 [**資料庫**]，然後按一下 [**附加**]。

    ![SSMS 附加](preparing-databases/_static/image15.png)
2. 在 [**附加資料庫**] 對話方塊中，按一下 [**新增**]，然後流覽至*應用程式\_Data*資料夾中的*aspnet-ContosoUniversity-Prod .mdf*檔案。

     ![SSMS 新增要附加的 .mdf 檔案](preparing-databases/_static/image16.png)
3. 按一下 [確定]。
4. 遵循您稍早用來為生產環境檔案建立腳本的相同程式。 將腳本檔案命名為*aspnet-data-prod*。

## <a name="summary"></a>總結

這兩個資料庫現在已準備好部署，而且您的方案資料夾中有兩個數據部署腳本。

![資料部署腳本](preparing-databases/_static/image17.png)

在下列教學課程中，您會設定會影響部署的專案設定，而且您會針對在部署的應用程式中必須不同的設定，設定自動的*web.config*檔案轉換。

## <a name="more-information"></a>詳細資訊

如需 NuGet 的詳細資訊，請參閱[使用 nuget 和 Nuget 管理專案程式庫](https://msdn.microsoft.com/magazine/hh547106.aspx)[檔](http://docs.nuget.org/docs/start-here/overview)。 如果您不想要使用 NuGet，您必須瞭解如何分析 NuGet 套件，以判斷它在安裝時的功能。 （例如，它可能會設定*web.config 轉換、設定 PowerShell*腳本在組建階段執行等等）。若要深入瞭解 NuGet 的運作方式，請參閱[建立和發行封裝](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package)和[設定檔案和原始程式碼轉換](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)。

> [!div class="step-by-step"]
> [上一頁](introduction.md)
> [下一頁](web-config-transformations.md)
