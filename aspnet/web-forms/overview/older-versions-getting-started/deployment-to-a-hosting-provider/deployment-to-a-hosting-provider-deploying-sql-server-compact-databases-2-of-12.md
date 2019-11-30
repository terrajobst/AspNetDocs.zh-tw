---
uid: web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
title: 使用 Visual Studio 或 Visual Web Developer SQL Server Compact 部署 ASP.NET Web 應用程式：部署 SQL Server Compact 資料庫-12Microsoft Docs
author: tdykstra
description: 這一系列的教學課程會示範如何使用 Visual Stu 部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案 。
ms.author: riande
ms.date: 11/17/2011
ms.assetid: c3c76516-4c48-4153-bd03-d70e3a3edbb0
msc.legacyurl: /web-forms/overview/older-versions-getting-started/deployment-to-a-hosting-provider/deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12
msc.type: authoredcontent
ms.openlocfilehash: 56ceabc79947967846d342354fd033510be5f05a
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74625573"
---
# <a name="deploying-an-aspnet-web-application-with-sql-server-compact-using-visual-studio-or-visual-web-developer-deploying-sql-server-compact-databases---2-of-12"></a>使用 Visual Studio 或 Visual Web Developer 的 SQL Server Compact 部署 ASP.NET Web 應用程式：部署 SQL Server Compact 資料庫-12 之2

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載入門專案](https://code.msdn.microsoft.com/Deploying-an-ASPNET-Web-4e31366b)

> 這一系列的教學課程會示範如何使用 Visual Studio 2012 RC 或 Visual Studio Express 2012 RC for Web，來部署（發行）包含 SQL Server Compact 資料庫的 ASP.NET web 應用程式專案。 如果您安裝 Web 發佈更新，也可以使用 Visual Studio 2010。 如需此系列的簡介，請參閱[本系列的第一個教學](deployment-to-a-hosting-provider-introduction-1-of-12.md)課程。
> 
> 如需示範在 Visual Studio 2012 的 RC 版本後引進部署功能的教學課程，說明如何部署 SQL Server Compact 以外的 SQL Server 版本，並示範如何部署到 Azure App Service Web Apps，請參閱[使用 Visual Studio ASP.NET Web 部署](../../deployment/visual-studio-web-deployment/introduction.md)。

## <a name="overview"></a>概觀

本教學課程示範如何設定兩個 SQL Server Compact 資料庫和用於部署的資料庫引擎。

針對資料庫存取，Contoso 大學應用程式需要必須與應用程式一起部署的下列軟體，因為它不包含在 .NET Framework 中：

- [SQL Server Compact](https://www.microsoft.com/sqlserver/en/us/editions/compact.aspx) （資料庫引擎）。
- [ASP.NET Universal Providers](http://www.hanselman.com/blog/IntroducingSystemWebProvidersASPNETUniversalProvidersForSessionMembershipRolesAndUserProfileOnSQLCompactAndSQLAzure.aspx) （可讓 ASP.NET 成員資格系統使用 SQL Server Compact）
- [Entity Framework 5.0](https://msdn.microsoft.com/library/gg696172(d=lightweight,v=vs.103).aspx)（包含遷移的 Code First）。

您也必須部署應用程式的兩個資料庫中的資料庫結構和部分（而非全部）資料。 一般而言，當您開發應用程式時，您會將測試資料輸入至您不想要部署到即時網站的資料庫中。 不過，您也可以輸入您想要部署的一些生產資料。 在本教學課程中，您將設定 Contoso 大學專案，以便在部署時包含所需的軟體和正確的資料。

提醒：如果您在進行本教學課程時收到錯誤訊息或無法解決問題，請務必查看 [疑難排解][頁面](deployment-to-a-hosting-provider-creating-and-installing-deployment-packages-12-of-12.md)。

## <a name="sql-server-compact-versus-sql-server-express"></a>SQL Server Compact 與 SQL Server Express

範例應用程式會使用 SQL Server Compact 4.0。 這個資料庫引擎是網站的一個相對新選項;舊版的 SQL Server Compact 無法在 web 主控環境中使用。 相較于使用 SQL Server Express 進行開發的更常見案例，SQL Server Compact 提供幾項優點，並部署至完整 SQL Server。 視您選擇的主控提供者而定，SQL Server Compact 的部署成本可能較低，因為有些提供者會額外收費，以支援完整的 SQL Server 資料庫。 SQL Server Compact 不收取額外費用，因為您可以將 database engine 本身部署為 web 應用程式的一部分。

不過，您也應該留意其限制。 SQL Server Compact 不支援預存程式、觸發程式、views 或 replication。 （如需 SQL Server Compact 不支援之 SQL Server 功能的完整清單，請參閱[SQL Server Compact 和 SQL Server 之間的差異](https://msdn.microsoft.com/library/bb896140.aspx)）。此外，您可以使用哪些工具來操作 SQL Server Express 和 SQL Server 資料庫中的架構和資料，無法用於 SQL Server Compact。 例如，您無法在 SQL Server Compact 資料庫的 Visual Studio 中使用 SQL Server Management Studio 或 SQL Server Data Tools。 您有其他選項可用來處理 SQL Server Compact 資料庫：

- 您可以使用 Visual Studio 中的伺服器總管，為 SQL Server Compact 提供有限的資料庫操作功能。
- 您可以使用[WebMatrix](https://www.microsoft.com/web/webmatrix/)的資料庫操作功能，其功能高於伺服器總管。
- 您可以使用功能相當完整的協力廠商或開放原始碼工具，例如 [ [SQL Server Compact 工具箱](https://github.com/ErikEJ/SqlCeToolbox)] 和 [ [SQL Compact 資料] 和 [架構腳本公用程式](https://github.com/ErikEJ/SqlCeToolbox)]。
- 您可以撰寫並執行自己的 DDL （資料定義語言）腳本，以運算元據庫架構。

您可以從 SQL Server Compact 開始，然後在您的需求演進後升級。 本系列稍後的教學課程會示範如何從 SQL Server Compact 遷移至 SQL Server Express，以及 SQL Server。 不過，如果您要建立新的應用程式，並預期在不久的將來需要 SQL Server，最好是從 SQL Server 或 SQL Server Express 開始。

## <a name="configuring-the-sql-server-compact-database-engine-for-deployment"></a>設定部署的 SQL Server Compact 資料庫引擎

在 Contoso 大學應用程式中進行資料存取所需的軟體是藉由安裝下列 NuGet 套件來新增：

- [Entityframework.sqlservercompact](http://nuget.org/List/Packages/SqlServerCompact)
- [System.web. provider](http://nuget.org/List/Packages/System.Web.Providers) （ASP.NET 通用提供者）
- [EntityFramework](http://nuget.org/List/Packages/EntityFramework)
- [EntityFramework. Entityframework.sqlservercompact](http://nuget.org/List/Packages/EntityFramework.sqlservercompact)

這些連結會指向這些套件的目前版本，這可能比您在本教學課程中下載的入門專案中所安裝的版本還新。 若要部署至主機服務提供者，請確定您使用 Entity Framework 5.0 或更新版本。 舊版的 Code First 移轉需要完全信任，而在許多主控提供者上，您的應用程式將會以中度信任來執行。 如需有關中度信任的詳細資訊，請參閱[部署至 IIS 作為測試環境](deployment-to-a-hosting-provider-deploying-to-iis-as-a-test-environment-5-of-12.md)教學課程。

NuGet 套件安裝通常會負責將此軟體部署到應用程式時所需的一切。 在某些情況下，這牽涉到一些工作，例如變更 Web.config 檔案，以及新增在您建立方案時執行的 PowerShell 腳本。 **如果您想要新增這些功能的支援（例如 SQL Server Compact 和 Entity Framework）而不使用 NuGet，請確定您知道安裝了哪些 NuGet 套件，才能手動執行相同的工作。**

有一個例外狀況，NuGet 不會處理您必須執行的所有工作，以確保部署成功。 Entityframework.sqlservercompact NuGet 套件會將組建後腳本新增至您的專案，以將原生元件複製到專案*bin*資料夾底下的*x86*和*amd64*子資料夾，但此腳本不會在專案中包含這些資料夾。 因此，除非您在專案中手動包含這些網站，否則 Web Deploy 不會將它們複製到目的地網站。 （這是預設部署設定的行為，而您在這些教學課程中不會用到的另一個選項，是變更控制此行為的設定。 您可以變更的設定只是在 [**專案屬性**] 視窗的 [**封裝/發行 Web** ] 索引標籤上，執行 [**要部署的專案**] 底下**的應用程式所需**的檔案。 通常不建議變更這項設定，因為它可能會導致在生產環境中部署更多的檔案，而不需要這麼做。 如需替代方案的詳細資訊，請參閱設定[專案屬性](deployment-to-a-hosting-provider-configuring-project-properties-4-of-12.md)教學課程。）

建立專案，然後在**方案總管**按一下 [**顯示所有**檔案] （如果您尚未這麼做）。 您也可能**需要按一下 [** 重新整理]。

![Solution_Explorer_Show_All_Files](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image1.png)

展開 [ **bin** ] 資料夾以查看 [ **amd64** ] 和 [ **x86** ] 資料夾，然後選取這些資料夾，以滑鼠右鍵按一下，然後選取 [**包含在專案中**]。

![amd64_and_x86_in_Solution_Explorer .png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image2.png)

資料夾圖示會變更，以顯示資料夾已包含在專案中。

![Solution_Explorer_amd64_included .png](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image3.png)

## <a name="configuring-code-first-migrations-for-application-database-deployment"></a>設定應用程式資料庫部署的 Code First 移轉

當您部署應用程式資料庫時，通常不會只是將您的開發資料庫與其所有資料一起部署到生產環境，因為其中有許多資料可能僅供測試之用。 例如，測試資料庫中的學生名稱是虛構的。 另一方面，您通常無法只部署資料庫結構，完全沒有資料。 測試資料庫中的某些資料可能是實際的資料，當使用者開始使用應用程式時，就必須存在。 例如，您的資料庫可能會有一個資料表，其中包含有效的等級值或實際部門名稱。

若要模擬這個常見的案例，您將設定 Code First 移轉種子方法，只將您想要在生產環境中的資料插入資料庫中。 這個種子方法不會插入測試資料，因為它會在 Code First 于生產環境中建立資料庫之後，于生產環境中執行。

在之前的 Code First 版本中，在發行之前，通常會使用植入測試資料的方法，因為在開發期間每個模型都有變更，因此資料庫必須完全刪除並從頭重新建立。 使用 Code First 移轉，在資料庫變更之後會保留測試資料，因此不需要在種子方法中包含測試資料。 您下載的專案會使用的預先遷移方法，將所有資料包含在初始化運算式類別的種子方法中。 在本教學課程中，您將停用初始化運算式類別並啟用遷移。 接著，您將更新「遷移」設定類別中的種子方法，使其只插入您想要在生產環境中插入的資料。

下圖說明應用程式資料庫的架構：

[![School_database_diagram](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image5.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image4.png)

在這些教學課程中，您會假設在第一次部署網站時，`Student` 和 `Enrollment` 資料表應該是空的。 其他資料表包含應用程式上線時必須預先載入的資料。

由於您將使用 Code First 移轉，因此您不再需要使用**DropCreateDatabaseIfModelChanges** Code First 初始化運算式。 這個初始化運算式的程式碼位於 ContosoUniversity 專案的 SchoolInitializer.cs 檔案中。 當應用程式第一次嘗試存取資料庫時，web.config 檔案之**appSettings**元素中的設定會使此初始化運算式執行：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample1.xml?highlight=3)]

開啟應用程式的 web.config 檔案，並從 appSettings 專案中移除指定 Code First 初始化運算式類別的元素。 AppSettings 元素現在看起來像這樣：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample2.xml)]

> [!NOTE]
> 另一種指定初始化運算式類別的方法，就是在*global.asax*檔案的 `Application_Start` 方法中呼叫 `Database.SetInitializer`。 如果您要在使用該方法來指定初始化運算式的專案中啟用遷移，請移除該程式程式碼。

接下來，啟用 Code First 移轉。

第一個步驟是確保 ContosoUniversity 專案設定為啟始專案。 在**方案總管**中，以滑鼠右鍵按一下 ContosoUniversity 專案，然後選取 [**設定為啟始專案**]。 Code First 移轉會在啟始專案中尋找資料庫連接字串。

從 [**工具**] 功能表中，依序按一下 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。

![Selecting_Package_Manager_Console](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image6.png)

在 [**套件管理員主控台**] 視窗的頂端，選取 [ContosoUniversity] 做為預設專案，然後在 `PM>` 提示字元輸入「啟用-遷移」。

![啟用-migrations_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image7.png)

此命令會在 ContosoUniversity 專案的新 [*遷移*] 資料夾中建立*Configuration.cs*檔案。

![Migrations_folder_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image8.png)

您已選取 DAL 專案，因為必須在包含 Code First 內容類別的專案中執行「啟用-遷移」命令。 當該類別在類別庫專案中時，Code First 移轉會在方案的啟始專案中尋找資料庫連接字串。 在 ContosoUniversity 方案中，Web 專案已設定為啟始專案。 （如果您不想要將具有連接字串的專案指定為 Visual Studio 中的啟始專案，您可以在 PowerShell 命令中指定啟始專案。 若要查看啟用-遷移命令的命令語法，您可以輸入命令「get-help 啟用-遷移」。）

開啟 Configuration.cs 檔案，並將 `Seed` 方法中的批註取代為下列程式碼：

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample3.cs)]

`List` 的參考在其底下有紅色曲線，因為您還沒有其命名空間的 `using` 語句。 以滑鼠右鍵按一下其中一個 `List` 實例，然後按一下 [**解析**]，再按一下 [**使用 system.object**]。

![使用 using 語句來解析](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image9.png)

此功能表選取專案會將下列程式碼加入至靠近檔案頂端的 `using` 語句。

[!code-csharp[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample4.cs)]

> [!NOTE]
> 將程式碼加入至 `Seed` 方法是您可以將固定資料插入資料庫的許多方式之一。 替代方法是將程式碼新增至每個遷移類別的 `Up` 和 `Down` 方法。 `Up` 和 `Down` 方法包含可執行資料庫變更的程式碼。 您會在[部署資料庫更新](deployment-to-a-hosting-provider-deploying-a-database-update-9-of-12.md)教學課程中看到它們的範例。
> 
> 您也可以使用 `Sql` 方法，撰寫執行 SQL 語句的程式碼。 例如，如果您已將預算資料行新增至部門資料表，而且想要在遷移過程中將所有部門預算初始化為 $1000.00，您可以將下列程式程式碼新增至該遷移的 `Up` 方法：
> 
> `Sql("UPDATE Department SET Budget = 1000");`
> 
> 本教學課程所示的這個範例會使用 Code First 移轉 `Configuration` 類別的 `Seed` 方法中的 `AddOrUpdate` 方法。 Code First 移轉會在每次遷移後呼叫 `Seed` 方法，而這個方法會更新已插入的資料列，如果尚未存在，則會將其插入。 `AddOrUpdate` 的方法可能不是您案例的最佳選擇。 如需詳細資訊，請參閱 Julie Lerman 的 blog 上的[處理 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

按下 CTRL-SHIFT-B 以建立專案。

下一個步驟是建立初始遷移的 `DbMigration` 類別。 您想要讓這種遷移建立新的資料庫，因此您必須刪除已經存在的資料庫。 *應用程式\_Data*資料夾中的 SQL Server Compact 資料庫會包含在 *.sdf*檔案中。 在**方案總管**中，展開 ContosoUniversity 專案中的 [*應用程式\_資料*]，以查看兩個 SQL Server Compact 資料庫（以 *.sdf*檔案表示）。

以滑鼠右鍵按一下*School .sdf*檔案，然後按一下 [**刪除**]。

![sdf_files_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image10.png)

在 [**套件管理員主控台**] 視窗中，輸入「新增-遷移初始」命令以建立初始遷移，並將其命名為「初始」。

![新增-migration_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image11.png)

Code First 移轉會在 [*遷移*] 資料夾中建立另一個類別檔案，而此類別包含建立資料庫架構的程式碼。

在 [**套件管理員主控台**] 中，輸入「更新-資料庫」命令來建立資料庫，並執行**種子**方法。

![更新-database_command](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image12.png)

（如果您收到錯誤，指出資料表已經存在，而且無法建立，可能是因為您在刪除資料庫之後，以及執行 `update-database`之前，已執行應用程式。 在此情況下，請再次刪除*School .sdf*檔案，然後重試 `update-database` 命令）。

執行應用程式。 現在 [學生] 頁面是空的，但講師頁面包含講師。 這是您在部署應用程式之後，將會在生產環境中取得的內容。

![Empty_Students_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image13.png)

![Instructors_page_after_initial_migration](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image14.png)

專案現在已準備好部署*School*資料庫。

## <a name="creating-a-membership-database-for-deployment"></a>建立部署的成員資格資料庫

Contoso 大學應用程式會使用 ASP.NET 成員資格系統和表單驗證來驗證和授權使用者。 其中一個頁面只能供系統管理員存取。 若要查看此頁面，請執行應用程式，然後從 [**課程**] 底下的飛出視窗中選取 [**更新點數**]。 應用程式會顯示 [**登入**] 頁面，因為只有系統管理員才有權使用 [**更新信用額度**] 頁面。

[![Log_in_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image16.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image15.png)

使用密碼 "Pas $ w0rd" 以 "admin" 的身分登入（請注意，數位零取代 "w0rd" 中的字母 "o"）。 登入之後，就會顯示 [**更新信用額度**] 頁面。

[![Update_Credits_page](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image18.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image17.png)

當您第一次部署網站時，通常會排除您為測試所建立的大部分或所有使用者帳戶。 在此情況下，您將部署系統管理員帳戶，而不是使用者帳戶。 您不需要手動刪除測試帳戶，而是會建立新的成員資格資料庫，其中只有您在生產環境中所需的一個系統管理員使用者帳戶。

> [!NOTE]
> 成員資格資料庫會儲存帳戶密碼的雜湊。 若要將帳戶從一部機器部署到另一台電腦，您必須確定雜湊常式不會在目的地伺服器上產生與來源電腦上不同的雜湊。 當您使用 ASP.NET Universal Providers 時，它們會產生相同的雜湊，前提是您不會變更預設演算法。 預設演算法為 HMACSHA256，而且是在 web.config 檔案中 **[machineKey](https://msdn.microsoft.com/library/w8h3skw9.aspx)** 元素的**驗證**屬性中指定。

成員資格資料庫不會由 Code First 移轉維護，而且不會有自動初始化運算式來植入具有測試帳戶的資料庫（就像 School 資料庫一樣）。 因此，若要讓測試資料保持可用，您可以在建立新的測試資料庫之前，先建立一個複本。

在**方案總管**中，將*應用程式\_Data*資料夾中的*aspnet .Sdf*檔案重新命名為*aspnet-Dev .sdf*。 （不要製作複本，只要將它重新命名，您就會在一段時間內建立新的資料庫）。

在**方案總管**中，請確定已選取 Web 專案（ContosoUniversity，而非 ContosoUniversity）。 然後在 [**專案**] 功能表中，選取 [ **ASP.NET**設定] 來執行**網站管理工具**（WAT）。

選取 [安全性] 索引標籤。

[![WAT_Security_tab](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image20.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image19.png)

按一下 [**建立或管理角色**] 並新增**系統管理員**角色。

[![WAT_Create_New_Role](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image22.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image21.png)

流覽回 [**安全性**] 索引標籤，按一下 [**建立使用者**]，然後以系統管理員身分新增使用者 "admin"。 在您按一下 [**建立使用者**] 頁面上的 [**建立使用者**] 按鈕之前，請確定您已選取 [**系統管理員**] 核取方塊。 本教學課程中使用的密碼為 "Pas $ w0rd"，您可以輸入任何電子郵件地址。

[![WAT_Create_User](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image24.png)](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image23.png)

關閉瀏覽器。 在**方案總管**中，按一下 [重新整理] 按鈕，以查看新的*aspnet .sdf*檔案。

![New_aspnet。 sdf_in_Solution_Explorer](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image25.png)

以滑鼠右鍵按一下 [ **aspnet .sdf** ]，然後選取 [**包含在專案中**]。

## <a name="distinguishing-development-from-production-databases"></a>區別生產資料庫的開發

在本節中，您將重新命名資料庫，讓開發版本為 School-Dev .sdf 和 aspnet-Dev，而實際執行版本為 School-Prod .sdf 和 aspnet-Prod. .sdf。 這並不是必要的，但這麼做可協助您防止資料庫的測試和實際執行版本混淆。

在**方案總管**中，**按一下 [** 重新整理] 並展開應用程式\_資料夾，以查看您稍早建立的 School 資料庫;以滑鼠右鍵按一下它，然後選取 [**包含在專案中**]。

![Including_School。 sdf_in_project](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/_static/image26.png)

將*aspnet .sdf*重新命名為*aspnet-Prod .sdf*。

將*School .sdf*重新命名為*School-Dev .sdf*。

當您在 Visual Studio 中執行應用程式時，您不會想要使用 *-生產*版本的資料庫檔案，而是要使用 *-Dev*版本。 因此，您必須變更 Web.config 檔案中的連接字串，使其指向資料庫的*Dev*版本。 （您還沒有建立 School-Prod .sdf 檔案，但這沒關係，因為 Code First 會在您第一次執行應用程式時，于生產環境中建立該資料庫）。

開啟應用程式的 web.config 檔案，並找出連接字串：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample5.xml)]

將 "aspnet .sdf" 變更為 "aspnet-Dev"，並將 "School .sdf" 變更為 "School-Dev"：

[!code-xml[Main](deployment-to-a-hosting-provider-deploying-sql-server-compact-databases-2-of-12/samples/sample6.xml?highlight=4-5)]

SQL Server Compact 資料庫引擎和這兩個資料庫現在已可供部署。 在下列教學課程中，您會針對在開發、測試和生產環境中必須不同的設定，設定自動的*web.config*檔案轉換。 （必須變更的設定是連接字串，但您稍後會在建立發行設定檔時設定這些變更）。

## <a name="more-information"></a>更多資訊

如需 NuGet 的詳細資訊，請參閱[使用 nuget 和 Nuget 管理專案程式庫](https://msdn.microsoft.com/magazine/hh547106.aspx)[檔](http://docs.nuget.org/docs/start-here/overview)。 如果您不想要使用 NuGet，您必須瞭解如何分析 NuGet 套件，以判斷它在安裝時的功能。 （例如，它可能會設定*web.config 轉換、設定 PowerShell*腳本在組建階段執行等等）。若要深入瞭解 NuGet 的運作方式，請參閱特別[建立和發行封裝](http://docs.nuget.org/docs/creating-packages/creating-and-publishing-a-package)和[設定檔案和原始程式碼轉換](http://docs.nuget.org/docs/creating-packages/configuration-file-and-source-code-transformations)。

> [!div class="step-by-step"]
> [上一頁](deployment-to-a-hosting-provider-introduction-1-of-12.md)
> [下一頁](deployment-to-a-hosting-provider-web-config-file-transformations-3-of-12.md)
