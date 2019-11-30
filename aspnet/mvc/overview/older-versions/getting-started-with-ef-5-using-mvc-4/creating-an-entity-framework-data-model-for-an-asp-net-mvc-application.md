---
uid: mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 建立 ASP.NET MVC 應用程式的 Entity Framework 資料模型（1/10） |Microsoft Docs
author: tdykstra
description: 此教學課程系列的較新版本適用于 Visual Studio 2013、Entity Framework 6 和 MVC 5。 Contoso 大學範例 web 應用程式已取消 。
ms.author: riande
ms.date: 07/30/2013
ms.assetid: 4ba029b6-ee7c-4e45-a0e7-b703c37e5d9a
msc.legacyurl: /mvc/overview/older-versions/getting-started-with-ef-5-using-mvc-4/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 8ee5aa22b6b2329b01d41437f30508e28a2288b2
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74595963"
---
# <a name="creating-an-entity-framework-data-model-for-an-aspnet-mvc-application-1-of-10"></a>建立 ASP.NET MVC 應用程式的 Entity Framework 資料模型（1/10）

由[Tom 作者: dykstra](https://github.com/tdykstra)

[下載已完成的專案](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)

> > [!NOTE] 
> > 
> > [此教學課程系列的較新版本](../../getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application.md)適用于 Visual Studio 2013、Entity Framework 6 和 MVC 5。
> 
> 
> Contoso 大學範例 web 應用程式示範如何使用 Entity Framework 5 和 Visual Studio 2012 來建立 ASP.NET MVC 4 應用程式。 這個範例應用程式是虛構的 Contoso 大學網站。 其中包括的功能有學生入學許可、課程建立、教師指派。 本教學課程系列會說明如何建立 Contoso 大學範例應用程式。 您可以[下載已完成的應用程式](https://code.msdn.microsoft.com/Getting-Started-with-dd0e2ed8)。
> 
> ## <a name="code-first"></a>Code First
> 
> 有三種方式可以使用 Entity Framework 中的資料： *Database First*、 *Model First*和*Code First*。 本教學課程適用于 Code First。 如需這些工作流程之間的差異，以及如何為您的案例選擇最適合的指引的詳細資訊，請參閱[Entity Framework 開發工作流程](https://msdn.microsoft.com/library/ms178359.aspx#dbfmfcf)。
> 
> ## <a name="mvc"></a>MVC
> 
> 範例應用程式是以[ASP.NET MVC](../../../index.md)為基礎。 如果您想要使用 ASP.NET Web form 模型，請參閱模型系結[和 Web forms](../../../../web-forms/overview/presenting-and-managing-data/model-binding/retrieving-data.md)教學課程系列和[ASP.NET 資料存取內容地圖](../../../../whitepapers/aspnet-data-access-content-map.md)。
> 
> ## <a name="software-versions"></a>軟體版本
> 
> | **教學課程中所示** | **也適用于** |
> | --- | --- |
> | Windows 8 | Windows 7 |
> | Visual Studio 2012 | 適用于 Web 的 Visual Studio 2012 Express。 如果您還沒有 VS 2012 或 VS 2012 Express for Web，Windows Azure SDK 就會自動安裝此程式。 Visual Studio 2013 應該可以使用，但本教學課程尚未經過測試，而且有些功能表選項和對話方塊不同。 需要 windows azure [SDK 的 VS 2013 版本](https://go.microsoft.com/fwlink/p/?linkid=323510)，才能進行 windows azure 部署。 |
> | .NET 4.5 | 所顯示的大部分功能都可以在 .NET 4 中使用，但有些不會。 例如，EF 中的列舉支援需要 .NET 4.5。 |
> | Entity Framework 5 |  |
> | [Windows Azure SDK 2。1](https://go.microsoft.com/fwlink/p/?linkid=323511) | 如果您略過 Windows Azure 部署步驟，則不需要 SDK。 發行新版本的 SDK 時，此連結將會安裝較新的版本。 在此情況下，您可能必須針對新的 UI 和功能調整一些指示。 |
> 
> ## <a name="questions"></a>問題
> 
> 如果您有與本教學課程不直接相關的問題，您可以將其張貼到[ASP.NET Entity Framework 論壇](https://forums.asp.net/1227.aspx)、 [Entity Framework 和 LINQ to Entities 論壇](https://social.msdn.microsoft.com/forums/adodotnetentityframework/threads/)，或[StackOverflow.com](http://stackoverflow.com/)。
> 
> ## <a name="acknowledgments"></a>致謝
> 
> 請參閱系列中的最後一個教學課程，以取得[通知和 VB 的相關注意事項](advanced-entity-framework-scenarios-for-an-mvc-web-application.md#acknowledgments)。
> 
> ## <a name="original-version-of-the-tutorial"></a>教學課程的原始版本
> 
> 本教學課程的原始版本可在[EF 4.1/MVC 3 電子書](https://social.technet.microsoft.com/wiki/contents/articles/11608.e-book-gallery-for-microsoft-technologies.aspx#GettingStartedwiththeEntityFramework4.1usingASP.NETMVC)中取得。

## <a name="the-contoso-university-web-application"></a>Contoso 大學 Web 應用程式

您在這些教學課程中會建置的應用程式為一個簡單的大學網站。

使用者可以檢視和更新學生、課程和教師資訊。 以下是您會建立的幾個畫面。

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

此網站的 UI 樣式與內建範本產生的相當類似，以使此教學課程能聚焦於如何使用 Entity Framework。

## <a name="prerequisites"></a>必要條件：

本教學課程中的指示和螢幕擷取畫面假設您使用的是[Visual Studio 2012](https://www.microsoft.com/visualstudio/eng/downloads)或[Visual Studio 2012 Express for Web](https://go.microsoft.com/fwlink/?LinkID=275131)，其中安裝了最新的 update 和 Azure SDK For .Net （從7月的2013起）。 您可以使用下列連結來取得所有此項：

[Azure SDK for .NET （Visual Studio 2012）](https://go.microsoft.com/fwlink/?LinkId=254364)

如果您已安裝 Visual Studio，上面的連結將會安裝任何遺失的元件。 如果您沒有 Visual Studio，此連結將會安裝 Visual Studio 2012 Express for Web。 您可以使用 Visual Studio 2013，但某些必要的程式和畫面會有所不同。

## <a name="create-an-mvc-web-application"></a>建立 MVC Web 應用程式

開啟 Visual Studio，然後使用C# **ASP.NET MVC 4 Web 應用程式**範本建立名為 "ContosoUniversity" 的新專案。 請確定您的目標是 **.NET Framework 4.5** （您將使用[`enum` 屬性](https://msdn.microsoft.com/data/hh859576.aspx)，而這需要 .net 4.5）。

![New_project_dialog_box](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image3.png)

在 [**新增 ASP.NET MVC 4 專案**] 對話方塊中，選取 [**網際網路應用程式**] 範本。

將 [ **Razor** view 引擎] 保持選取狀態，並將 [**建立單元測試專案**] 核取方塊保留為已清除。

按一下 [確定]。

![Project_template_options](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image4.png)

## <a name="set-up-the-site-style"></a>設定網站樣式

一些簡單的變更會設定網站的功能表、配置和首頁。

開啟*Views\Shared\\_Layout.* # #，並以下列程式碼取代檔案的內容。 所做的變更已醒目標示。

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=5,15,25-28,43)]

此程式碼會進行下列變更：

- 以「Contoso 大學」取代「我的 ASP.NET MVC 應用程式」和「您的標誌」的範本實例。
- 加入數個將在本教學課程中使用的動作連結。

在*Views\Home\Index.cshtml*中，以下列程式碼取代檔案的內容，以消除 ASP.NET 和 MVC 的範本段落：

[!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

在*Controllers\HomeController.cs*中，將 `Index` 動作方法中 `ViewBag.Message` 的值變更為「歡迎使用 Contoso 大學！」，如下列範例所示：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs?highlight=3)]

按 CTRL + F5 執行網站。 您會在首頁上看到主功能表。

![Contoso_University_home_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image5.png)

## <a name="create-the-data-model"></a>建立資料模型

接下來您會為 Contoso 大學應用程式建立實體類別。 您將從下列三個實體開始：

![Class_diagram](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image6.png)

在 `Student` 和 `Enrollment` 實體之間存在一對多關聯性，`Course` 與 `Enrollment` 實體之間也存在一對多關聯性。 換句話說，一位學生可以註冊並參加任何數目的課程，而一個課程也可以有任何數目的學生註冊。

在下節中，您會為這些實體建立各自的類別。

> [!NOTE]
> 如果您在完成所有這些實體類別的建立之前嘗試編譯專案，您會收到編譯器錯誤。

### <a name="the-student-entity"></a>Student 實體

![Student_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image7.png)

在 [*模型*] 資料夾中，建立*Student.cs* ，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`StudentID` 屬性會成為資料庫資料表中的主索引鍵資料行，並對應至這個類別。 根據預設，Entity Framework 會將名為 `ID` 或*classname* `ID` 的屬性解讀為主要索引鍵。

`Enrollments` 屬性為*導覽屬性*。 導覽屬性會保留與此實體相關的其他實體。 在此情況下，`Student` 實體的 `Enrollments` 屬性會保存與該 `Student` 實體相關的所有 `Enrollment` 實體。 換句話說，如果資料庫中給定的 `Student` 資料列有兩個相關的 `Enrollment` 列（在其 `StudentID` 外鍵資料行中包含該學生的主鍵值的資料列），該 `Student` 實體的 `Enrollments` 導覽屬性會包含這兩個 `Enrollment` 的實體。

導覽屬性通常會定義為 `virtual`，讓它們可以利用某些 Entity Framework 的功能，例如消極式*載入*。 （稍後將在本系列稍後的[讀取相關資料](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)教學課程中說明延遲載入。

若導覽屬性可保有多個實體 (例如在多對多或一對多關聯性中的情況)，其類型必須為一個清單，使得實體可以在該清單中新增、刪除或更新，例如 `ICollection`。

### <a name="the-enrollment-entity"></a>註冊實體

![Enrollment_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image8.png)

在 *Models* 資料夾中，建立 *Enrollment.cs*，然後使用下列程式碼取代現有的程式碼：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

年級屬性是一個[列舉](https://msdn.microsoft.com/data/hh859576.aspx)。 `Grade` 型別宣告後方的問號表示 `Grade` 屬性[可為 Null](https://msdn.microsoft.com/library/2cf62fcy.aspx)。 Null 的等級與零的等級不同-null 表示不知道等級或尚未指派。

`StudentID` 屬性是外部索引鍵，對應的導覽屬性是 `Student`。 `Enrollment` 實體與一個 `Student` 實體關聯，因此屬性僅能保有單一 `Student` 實體 (不像您先前看到的 `Student.Enrollments` 導覽屬性可保有多個 `Enrollment` 實體)。

`CourseID` 屬性是外部索引鍵，對應的導覽屬性是 `Course`。 一個 `Enrollment` 實體與一個 `Course` 實體建立關聯。

### <a name="the-course-entity"></a>Course 實體

![Course_entity](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image9.png)

在 [*模型*] 資料夾中，建立*Course.cs*，以下列程式碼取代現有的程式碼：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

`Enrollments` 屬性為導覽屬性。 `Course` 實體可以與任何數量的 `Enrollment` 實體相關。

我們會更深入瞭解 [[DatabaseGenerated](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedattribute(v=vs.110).aspx)（[DatabaseGeneratedOption](https://msdn.microsoft.com/library/system.componentmodel.dataannotations.schema.databasegeneratedoption(v=vs.95).aspx)。None）] 屬性（在下一個教學課程中）。 基本上，此屬性可讓您為課程輸入主索引鍵，而非讓資料庫產生它。

## <a name="create-the-database-context"></a>建立資料庫內容

協調給定資料模型 Entity Framework 功能的主要類別是*資料庫內容*類。 您可以藉由衍生自[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=VS.103).aspx)類別來建立此類別。 在您的程式碼中，您會指定資料模型中包含哪些實體。 您也可以自訂某些 Entity Framework 行為。 在此專案中，類別命名為 `SchoolContext`。

建立名為*DAL* （適用于資料存取層）的資料夾。 在該資料夾中，建立名為*SchoolCoNtext.cs*的新類別檔案，並以下列程式碼取代現有的程式碼：

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs)]

此程式碼會為每個實體集建立[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=VS.103).aspx)屬性。 在 Entity Framework 術語中，*實體集*通常會對應至資料庫資料表，而*實體*會對應到資料表中的資料列。

[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的 `modelBuilder.Conventions.Remove` 語句會防止複數化資料表名稱。 如果您未這麼做，則產生的資料表會命名為 `Students`、`Courses`和 `Enrollments`。 相反地，資料表名稱會是 `Student`、`Course`和 `Enrollment`。 針對是否要複數化資料表名稱，開發人員並沒有共識。 本教學課程使用單數形式，但重點在於，您可以藉由包含或省略這行程式碼來選取您偏好的任何格式。

## <a name="sql-server-express-localdb"></a>SQL Server Express LocalDB

[LocalDB](https://blogs.msdn.com/b/sqlexpress/archive/2011/07/12/introducing-localdb-a-better-sql-express.aspx)是輕量版的 SQL Server Express 資料庫引擎，會視需要啟動並在使用者模式中執行。 LocalDB 會在 SQL Server Express 的特殊執行模式下執行，可讓您使用資料庫做為 *.mdf*檔案。 LocalDB 資料庫檔案通常會保留在 Web 專案的*應用程式\_Data*資料夾中。 SQL Server Express 中的使用者實例功能也可讓您使用 *.mdf*檔案，但是使用者實例功能已被取代;因此，建議使用 LocalDB 來處理 *.mdf*檔案。

通常 SQL Server Express 不會用於生產 web 應用程式。 不建議將 LocalDB 用於與 web 應用程式搭配使用的生產環境，因為它不是設計用於 IIS。

在 Visual Studio 2012 和更新版本中，預設會隨 Visual Studio 安裝 LocalDB。 在 Visual Studio 2010 和舊版中，預設會使用 Visual Studio 安裝 SQL Server Express （不含 LocalDB）;如果您使用的是 Visual Studio 2010，就必須手動安裝它。

在本教學課程中，您將使用 LocalDB，以便將資料庫儲存在*應用程式中\_Data*資料夾做為 *.mdf*檔案。 開啟根*web.config*檔案，然後將新的連接字串新增至 `connectionStrings` 集合，如下列範例所示。 （請務必更新根專案資料夾*中的 web.config 檔案。* 此外，您不需要更新的*Views*子資料夾中也會有*web.config*檔案）。

[!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.xml)]

根據預設，Entity Framework 會尋找名為的連接字串，與 `DbContext` 類別（此專案的`SchoolContext`）相同。 您已新增的連接字串會指定位於*應用程式\_Data*資料夾中名為*ContosoUniversity*的 LocalDB 資料庫。 如需詳細資訊，請參閱[SQL Server ASP.NET Web 應用程式的連接字串](https://msdn.microsoft.com/library/jj653752.aspx)。

您實際上不需要指定連接字串。 如果您未提供連接字串，Entity Framework 會為您建立一個。不過，資料庫可能不在應用程式的*應用程式\_data*資料夾中。 如需有關建立資料庫之位置的詳細資訊，請參閱[Code First 至新的資料庫](https://msdn.microsoft.com/data/jj193542)。

`connectionStrings` 集合也有一個名為 `DefaultConnection` 的連接字串，用於成員資格資料庫。 在本教學課程中，您將不會使用成員資格資料庫。 這兩個連接字串的唯一差異在於資料庫名稱和 name 屬性值。

## <a name="set-up-and-execute-a-code-first-migration"></a>設定和執行 Code First 遷移

當您第一次開始開發應用程式時，您的資料模型會經常變更，而且每次模型變更時，它就不會與資料庫同步。 您可以設定 Entity Framework 在每次變更資料模型時，自動卸載並重新建立資料庫。 這在開發初期並不成問題，因為可以輕鬆地重新建立測試資料，但在部署到生產環境之後，您通常會想要更新資料庫架構，而不需卸載資料庫。 「遷移」功能可讓 Code First 更新資料庫，而不需要卸載再重新建立。 在新專案的開發週期初期，您可能會想要在每次模型變更時，使用[DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=vs.103).aspx)卸載、重新建立並重新植入資料庫。 您已準備好部署應用程式，您可以轉換成遷移方法。 在本教學課程中，您只會使用遷移。 如需詳細資訊，請參閱[Code First 移轉](https://msdn.microsoft.com/data/jj591621)和[遷移螢幕錄製影片系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。

### <a name="enable-code-first-migrations"></a>啟用 Code First 移轉

1. 從 [**工具**] 功能表中，依序按一下 [ **NuGet 套件管理員**] 和 [**套件管理員主控台**]。

    ![Selecting_Package_Manager_Console](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image10.png)
2. 在 `PM>` 提示字元中，輸入下列命令：

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.ps1)]

    ![啟用-遷移命令](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image11.png)

    此命令會在 ContosoUniversity 專案中建立一個 [*遷移*] 資料夾，並在該資料夾中放入*Configuration.cs*檔案，供您編輯以設定遷移。

    ![[遷移] 資料夾](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image12.png)

    `Configuration` 類別包含一個 `Seed` 的方法，此方法會在建立資料庫時呼叫，而且每次在資料模型變更之後更新。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.cs)]

    這個 `Seed` 方法的目的是要讓您在 Code First 建立測試資料或加以更新之後，將其插入至資料庫。

### <a name="set-up-the-seed-method"></a>設定種子方法

當 Code First 移轉建立資料庫時，以及每次將資料庫更新為最新的遷移時，就會執行[種子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法。 種子方法的目的是要讓您在應用程式第一次存取資料庫之前，將資料插入資料表。

在舊版的 Code First 中，在發行之前，`Seed` 方法通常是插入測試資料，因為在開發期間每個模型都有變更時，資料庫必須完全刪除並從頭重新建立。 使用 Code First 移轉，在資料庫變更之後會保留測試資料，因此通常不需要在[種子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法中包含測試資料。 事實上，如果您要使用遷移將資料庫部署到生產環境，您不希望 `Seed` 方法插入測試資料，因為 `Seed` 方法將會在生產環境中執行。 在此情況下，您想要 `Seed` 方法只將您想要在生產環境中插入的資料插入資料庫中。 例如，當應用程式在生產環境中可供使用時，您可能會想要讓資料庫在 `Department` 資料表中包含實際的部門名稱。

在本教學課程中，您將使用遷移來進行部署，但您的 `Seed` 方法仍會插入測試資料，讓您更輕鬆地查看應用程式功能的運作方式，而不需要手動插入大量資料。

1. 將*Configuration.cs*檔案的內容取代為下列程式碼，這會將測試資料載入至新的資料庫。 

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

    [種子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法會將資料庫內容物件當做輸入參數，而方法中的程式碼會使用該物件將新的實體加入至資料庫。 針對每個實體類型，程式碼會建立新實體的集合，並將其加入至適當的[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)屬性，然後將變更儲存至資料庫。 您不需要在每個實體群組之後呼叫[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法，這是在這裡完成，但如果在程式碼寫入資料庫時發生例外狀況，這樣做可協助您找出問題的來源。

    某些插入資料的語句會使用[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法來執行「upsert」作業。 因為 `Seed` 方法會隨著每次遷移而執行，所以您不能只插入資料，因為在第一次建立資料庫的遷移之後，您嘗試加入的資料列已經存在。 如果您嘗試插入已經存在的資料列，則 "upsert" 作業會防止發生錯誤，但它會***覆寫***您在測試應用程式時所做的任何變更。 在某些資料表中使用測試資料時，您可能不會想要這樣做：在某些情況下，當您在測試時變更資料，而您想要在資料庫更新之後維持變更。 在此情況下，您想要執行條件式插入作業：只有在不存在資料列時，才插入它。 種子方法會使用這兩個方法。

    傳遞至[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法的第一個參數會指定要用來檢查資料列是否已經存在的屬性。 對於您所提供的測試學生資料，`LastName` 屬性可以用於此用途，因為清單中的每個姓氏都是唯一的：

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

    此程式碼假設姓氏是唯一的。 如果您以手動方式新增姓氏重複的學生，則會在下一次執行遷移時收到下列例外狀況。

    序列包含一個以上的元素

    如需有關 `AddOrUpdate` 方法的詳細資訊，請參閱 Julie Lerman 的 blog 上的[使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

    新增 `Enrollment` 實體的程式碼不會使用 `AddOrUpdate` 方法。 它會檢查實體是否已存在，並插入實體（如果不存在）。 這個方法會保留您在執行遷移時對註冊等級所進行的變更。 程式碼會對 `Enrollment`[清單](https://msdn.microsoft.com/library/6sh2ey19.aspx)的每個成員執行迴圈，如果在資料庫中找不到註冊，就會將註冊加入至資料庫。 當您第一次更新資料庫時，資料庫將會是空的，因此它會新增每個註冊。

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cs)]

    如需有關如何調試 `Seed` 方法，以及如何處理重復資料（例如名為 "Alexander Carson" 的兩名學生）的詳細資訊，請參閱 Rick Anderson 的 blog 上的[植入和偵測 Entity Framework （EF） db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 。
2. 建置專案。

### <a name="create-and-execute-the-first-migration"></a>建立並執行第一次遷移

1. 在 [套件管理員主控台] 視窗中，輸入下列命令： 

    [!code-powershell[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample14.ps1)]

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image13.png)

    `add-migration` 命令會將包含建立資料庫之程式碼的 *[DateStamp]\_InitialCreate.cs*檔案新增至 [遷移] 資料夾。 第一個參數（`InitialCreate)` 用於檔案名，而且可以是任何您想要的名稱; 您通常會選擇一個字組或片語，以摘要說明在遷移中完成的作業。 例如，您可以將稍後的遷移命名 &quot;AddDepartmentTable&quot;。

    ![具有初始遷移的遷移資料夾](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

    `InitialCreate` 類別的 `Up` 方法會建立對應至資料模型實體集的資料庫資料表，而 `Down` 方法會將它們刪除。 移轉會呼叫 `Up` 方法，以實作資料模型變更來進行移轉。 當您輸入命令以復原更新時，Migrations 會呼叫 `Down` 方法。 下列程式碼顯示 `InitialCreate` 檔案的內容：

    [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample15.cs)]

    `update-database` 命令會執行 `Up` 方法來建立資料庫，然後執行 `Seed` 方法來填入資料庫。

現在已為您的資料模型建立 SQL Server 資料庫。 資料庫的名稱是*ContosoUniversity*，而且 *.mdf*檔案位於專案的*應用程式\_Data*資料夾，因為這是您在連接字串中指定的內容。

您可以使用**伺服器總管**或**SQL Server 物件總管**（SSOX），在 Visual Studio 中查看資料庫。 在本教學課程中，您將使用**伺服器總管**。 在 Visual Studio Express 2012 for Web 中，**伺服器總管**稱為**資料庫總管**。

1. 從 [ **View** ] 功能表中，按一下 [**伺服器總管**]。
2. 按一下 [**新增連接**] 圖示。

    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image15.png)
3. 如果出現 **選擇資料來源** 對話方塊的提示，請按一下  **Microsoft SQL Server**，然後按一下 **繼續**。  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image16.png)
4. 在 [**加入連接**] 對話方塊中，輸入 **（localdb） \V11.0**做為**伺服器名稱**。 在 [**選取或輸入資料庫名稱**] 底下，選取 [ **ContosoUniversity]。**  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image17.png)
5. 按一下 [確定]
6. 展開 [ **SchoolCoNtext** ]，然後展開 [**資料表]** 。  
  
    ![](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image18.png)
7. 以滑鼠右鍵按一下 [ **Student** ] 資料表，然後按一下 [**顯示資料表資料**]，以查看已建立的資料行以及已插入資料表中的資料列。

    ![Student 資料表](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image19.png)

## <a name="creating-a-student-controller-and-views"></a>建立學生控制器和 Views

下一個步驟是在您的應用程式中建立 ASP.NET 的 MVC 控制器和可使用其中一個資料表的視圖。

1. 若要建立 `Student` 控制器，請在**方案總管**中的 [**控制器**] 資料夾上按一下滑鼠右鍵，選取 [**新增**]，然後按一下 [**控制器**]。 在 [**新增控制器**] 對話方塊中，進行下列選擇，然後按一下 [**新增**]： 

   - 控制器名稱： **StudentController**。
   - 範本：**具有讀取/寫入動作和視圖的 MVC 控制器，使用 Entity Framework**。
   - 模型類別： **Student （ContosoUniversity）** 。 （如果您在下拉式清單中看不到這個選項，請建立專案，然後再試一次）。
   - 資料內容類別： **SchoolCoNtext （ContosoUniversity）** 。
   - Views： **Razor （CSHTML）** 。 （預設值）。

     ![Add_Controller_dialog_box_for_Student_controller](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image20.png)
2. Visual Studio 會開啟*Controllers\StudentController.cs*檔案。 您會看到已建立的類別變數，可具現化資料庫內容物件：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample16.cs)]

     `Index` 動作方法會藉由讀取資料庫內容實例的 `Students` 屬性，從*學生*實體集取得學生的清單：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample17.cs)]

     *Student\Index.cshtml* view 會在資料表中顯示此清單：

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample18.cshtml)]
3. 按 CTRL+F5 執行專案。

     按一下 [**學生**] 索引標籤，查看 `Seed` 方法所插入的測試資料。

     ![[學生索引] 頁面](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image21.png)

## <a name="conventions"></a>慣例

為了讓 Entity Framework 能夠為您建立完整資料庫，您必須撰寫的程式碼數量最少，因為使用*慣例*或 Entity Framework 所做的假設。 其中一些已注明：

- 實體類別名稱的複數化形式會當做資料表名稱使用。
- 實體屬性名稱會用於資料行名稱。
- 名為 `ID` 或*classname* `ID` 的實體屬性會被辨識為主鍵屬性。

您已瞭解可以覆寫慣例（例如，您指定不應複數化資料表名稱），而您將在本系列稍後的[建立更複雜的資料模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)教學課程中，深入瞭解慣例和如何覆寫它們。 如需詳細資訊，請參閱[Code First 慣例](https://msdn.microsoft.com/data/jj679962)。

## <a name="summary"></a>總結

您現在已建立簡單的應用程式，它會使用 Entity Framework 和 SQL Server Express 來儲存和顯示資料。 在下列教學課程中，您將瞭解如何執行基本的 CRUD （建立、讀取、更新、刪除）作業。 您可以在此頁面底部留下意見反應。 請讓我們知道您喜歡本教學課程部分的方式，以及我們如何改善。

您可以在[ASP.NET 資料存取內容對應](../../../../whitepapers/aspnet-data-access-content-map.md)中找到其他 Entity Framework 資源的連結。

> [!div class="step-by-step"]
> [下一步](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)
