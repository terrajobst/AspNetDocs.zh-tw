---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
title: 教學課程：使用 MVC 5 開始使用 Entity Framework 6 Code First |Microsoft Docs
description: 在這一系列的教學課程中，您將瞭解如何建立 ASP.NET MVC 5 應用程式，以使用 Entity Framework 6 來進行資料存取。
author: tdykstra
ms.author: riande
ms.date: 01/22/2019
ms.topic: tutorial
ms.assetid: 00bc8b51-32ed-4fd3-9745-be4c2a9c1eaf
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/creating-an-entity-framework-data-model-for-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: a00a5a3aa295c2584b90abbf931c258c9e1b58ca
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616127"
---
# <a name="tutorial-get-started-with-entity-framework-6-code-first-using-mvc-5"></a>教學課程：使用 MVC 5 開始使用 Entity Framework 6 Code First

> [!NOTE]
> 針對新的開發，建議[ASP.NET Core Razor Pages](/aspnet/core/razor-pages) ASP.NET MVC 控制器和 views。 如需與使用 Razor Pages 類似的教學課程系列，請參閱[教學課程：開始使用 ASP.NET Core 中的 Razor Pages](/aspnet/core/tutorials/razor-pages/razor-pages-start)。 新的教學課程：
> * 比較容易學習。
> * 提供更多 EF Core 最佳做法。
> * 使用更有效率的查詢。
> * 具有最新的 API。
> * 涵蓋更多功能。
> * 是新應用程式開發的建議方法。

在這一系列的教學課程中，您將瞭解如何建立 ASP.NET MVC 5 應用程式，以使用 Entity Framework 6 來進行資料存取。 本教學課程使用 Code First 工作流程。 如需如何在 Code First、Database First 和 Model First 之間進行選擇的詳細資訊，請參閱[建立模型](/ef/ef6/modeling/)。

本教學課程系列會說明如何建立 Contoso 大學範例應用程式。 範例應用程式是簡單的大學網站。 有了它，您就可以查看和更新學生、課程和講師資訊。 以下是您所建立的兩個畫面：

![Students_Index_page](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image1.png)

![編輯學生](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image2.png)

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立 MVC web 應用程式
> * 設定網站樣式
> * 安裝 Entity Framework 6
> * 建立資料模型
> * 建立資料庫內容
> * 使用測試資料將 DB 初始化
> * 設定 EF 6 使用 LocalDB
> * 建立控制器和檢視
> * 檢視資料庫

## <a name="prerequisites"></a>Prerequisites

* [Visual Studio 2017](https://visualstudio.microsoft.com/downloads/?utm_medium=microsoft&utm_source=docs.microsoft.com&utm_campaign=button+cta&utm_content=download+vs2017)

## <a name="create-an-mvc-web-app"></a>建立 MVC web 應用程式

1. 開啟 Visual Studio，並使用C# **ASP.NET web 應用程式（.NET Framework）** 範本建立 Web 專案。 將專案命名為*ContosoUniversity* ，然後選取 **[確定]** 。

   ![Visual Studio 中的 [新增專案] 對話方塊](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-project-dialog.png)

1. 在 [**新增 ASP.NET Web 應用程式-ContosoUniversity**] 中，選取 [ **MVC**]。

   ![Visual Studio 中的 [新增 web 應用程式] 對話方塊](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/new-web-app-dialog.png)

    > [!NOTE]
    > 根據預設，**驗證**選項會設定為 [**不需要驗證**]。 在本教學課程中，web 應用程式不需要使用者登入。 此外，它也不會根據登入的使用者來限制存取權。

1. 選取 [確定] 建立專案。

## <a name="set-up-the-site-style"></a>設定網站樣式

一些簡單的變更會設定網站的功能表、配置和首頁。

1. 開啟*Views\Shared\\_Layout*，並進行下列變更：

   - 將每個出現的「我的 ASP.NET 應用程式」和「應用程式名稱」變更為「Contoso 大學」。
   - 新增學生、課程、講師和部門的功能表項目，並刪除連絡人項目。

   這些變更會反白顯示在下列程式碼片段中：

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample1.cshtml?highlight=6,19,24-27,38)]

2. 在*Views\Home\Index.cshtml*中，將檔案的內容取代為下列程式碼，以將 ASP.NET 和 MVC 的文字取代為此應用程式的文字：

   [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample2.cshtml)]

3. 按 Ctrl + F5 執行網站。 您會在首頁上看到主功能表。

## <a name="install-entity-framework-6"></a>安裝 Entity Framework 6

1. 從 [**工具**] 功能表中，選擇 [ **NuGet 套件管理員**]，然後選擇 [**套件管理員主控台**]。

2. 在 [Package Manager Console] 視窗中，輸入下列命令：

   ```text
   Install-Package EntityFramework
   ```

此步驟是本教學課程的幾個步驟中的其中一個，但這可能是由 ASP.NET MVC 樣板功能自動完成的。 您要手動執行這些動作，讓您可以看到使用 Entity Framework （EF）所需的步驟。 您稍後會使用此架構來建立 MVC 控制器和 views。 替代方式是讓 [架構] 自動安裝 EF NuGet 封裝、建立資料庫內容類別，並建立連接字串。 當您準備好這樣做時，您只需要略過這些步驟，並在建立實體類別之後 scaffold 您的 MVC 控制器。

## <a name="create-the-data-model"></a>建立資料模型

接下來您會為 Contoso 大學應用程式建立實體類別。 您將從下列三個實體開始：

**課程** <-> **註冊** <-> **Student**

| 實體 | Relationship |
| -------- | ------------ |
| 註冊課程 | 一對多 |
| 要註冊的學生 | 一對多 |

在 `Student` 和 `Enrollment` 實體之間存在一對多關聯性，`Course` 與 `Enrollment` 實體之間也存在一對多關聯性。 換句話說，一位學生可以註冊並參加任何數目的課程，而一個課程也可以有任何數目的學生註冊。

在下列各節中，您將為每個實體建立一個類別。

> [!NOTE]
> 如果您在完成所有這些實體類別的建立之前嘗試編譯專案，您會收到編譯器錯誤。

### <a name="the-student-entity"></a>Student 實體

- 在 [*模型*] 資料夾中，建立名為*Student.cs*的類別檔案，方法是以滑鼠右鍵按一下**方案總管**中的資料夾，然後選擇 [**加入** > **類別**]。 使用下列程式碼取代範本程式碼：

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample3.cs)]

`ID` 屬性會成為資料庫資料表中的主索引鍵資料行，並對應至這個類別。 根據預設，Entity Framework 會將名為 `ID` 或*classname* `ID` 的屬性解讀為主要索引鍵。

`Enrollments` 屬性為*導覽屬性*。 導覽屬性會保留與此實體相關的其他實體。 在此情況下，`Student` 實體的 `Enrollments` 屬性會保存與該 `Student` 實體相關的所有 `Enrollment` 實體。 換句話說，如果資料庫中給定的 `Student` 資料列有兩個相關的 `Enrollment` 列（在其 `StudentID` 外鍵資料行中包含該學生的主鍵值的資料列），該 `Student` 實體的 `Enrollments` 導覽屬性會包含這兩個 `Enrollment` 的實體。

導覽屬性通常會定義為 `virtual`，讓它們可以利用某些 Entity Framework 的功能，例如消極式*載入*。 （稍後將在本系列稍後的[讀取相關資料](reading-related-data-with-the-entity-framework-in-an-asp-net-mvc-application.md)教學課程中說明消極式載入）。

若導覽屬性可保有多個實體 (例如在多對多或一對多關聯性中的情況)，其類型必須為一個清單，使得實體可以在該清單中新增、刪除或更新，例如 `ICollection`。

### <a name="the-enrollment-entity"></a>Enrollment 實體

- 在 *Models* 資料夾中，建立 *Enrollment.cs*，然後使用下列程式碼取代現有的程式碼：

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample4.cs)]

`EnrollmentID` 屬性將會是主要金鑰;這個實體會使用*classname* `ID` 模式，而不是由您在 `Student` 實體中看到的本身 `ID`。 通常您會選擇一個模式，然後在您整個資料模型中使用此模式。 在這裡，此變化僅作為向您展示使用不同模式之用。 在稍後的教學課程中，您將瞭解如何使用 `ID` 而不 `classname`，讓您更輕鬆地在資料模型中執行繼承。

`Grade` 屬性是[列舉](/ef/ef6/modeling/code-first/data-types/enums)。 `Grade` 型別宣告後方的問號表示 `Grade` 屬性[可為 Null](/dotnet/csharp/programming-guide/nullable-types/using-nullable-types)。 Null 的等級與零的等級不同-null 表示不知道等級或尚未指派。

`StudentID` 屬性是外部索引鍵，對應的導覽屬性是 `Student`。 `Enrollment` 實體與一個 `Student` 實體關聯，因此屬性僅能保有單一 `Student` 實體 (不像您先前看到的 `Student.Enrollments` 導覽屬性可保有多個 `Enrollment` 實體)。

`CourseID` 屬性是外部索引鍵，對應的導覽屬性是 `Course`。 一個 `Enrollment` 實體與一個 `Course` 實體建立關聯。

Entity Framework 將屬性（property）&lt;導覽屬性名稱命名為「外鍵屬性」， *&gt;&lt;主鍵屬性名稱&gt;* （例如 `StudentID` `Student` 實體的主要索引鍵 `Student` 後，`ID`導覽屬性的）。 外鍵屬性也可以命名為相同 *&lt;主鍵屬性名稱&gt;* （例如 `CourseID`，因為 `Course` 實體的主要索引鍵是 `CourseID`）。

### <a name="the-course-entity"></a>Course 實體

- 在 [*模型*] 資料夾中，建立*Course.cs*，將範本程式碼取代為下列程式碼：

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample5.cs)]

`Enrollments` 屬性為導覽屬性。 `Course` 實體可以與任何數量的 `Enrollment` 實體相關。

我們將在本系列稍後的教學課程中，進一步瞭解 <xref:System.ComponentModel.DataAnnotations.Schema.DatabaseGeneratedAttribute> 屬性。 基本上，此屬性可讓您為課程輸入主索引鍵，而非讓資料庫產生它。

## <a name="create-the-database-context"></a>建立資料庫內容

協調給定資料模型 Entity Framework 功能的主要類別是*資料庫內容*類。 您可以藉由衍生自[DbCoNtext](https://msdn.microsoft.com/library/system.data.entity.dbcontext(v=vs.113).aspx)類別來建立此類別。 在您的程式碼中，您可以指定要包含在資料模型中的實體。 您也可以自訂某些 Entity Framework 行為。 在此專案中，類別命名為 `SchoolContext`。

- 若要在 ContosoUniversity 專案中建立資料夾，請以滑鼠右鍵按一下**方案總管**中的專案，然後按一下 [**加入**]，再按一下 [**新增資料夾**]。 將新資料夾命名為*DAL* （適用于資料存取層）。 在該資料夾中，建立名為*SchoolCoNtext.cs*的新類別檔案，並以下列程式碼取代範本程式碼：

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample6.cs)]

### <a name="specify-entity-sets"></a>指定實體集

此程式碼會為每個實體集建立[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.113).aspx)屬性。 在 Entity Framework 術語中，*實體集*通常會對應至資料庫資料表，而*實體*會對應到資料表中的資料列。

> [!NOTE]
>
> 您可以省略 `DbSet<Enrollment>` 和 `DbSet<Course>` 語句，它的作用相同。 Entity Framework 會隱含地包含這些專案，因為 `Student` 實體會參考 `Enrollment` 實體，而 `Enrollment` 實體會參考 `Course` 實體。

### <a name="specify-the-connection-string"></a>指定連接字串

連接字串的名稱（您稍後將會加入 web.config 檔案中）會傳遞至該函式。

[!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample7.cs?highlight=1)]

您也可以傳入連接字串本身，而不是儲存在 web.config 檔案中的名稱。 如需指定要使用的資料庫之選項的詳細資訊，請參閱[連接字串和模型](/ef/ef6/fundamentals/configuring/connection-strings)。

如果您未明確指定連接字串或名稱，Entity Framework 會假設連接字串名稱與類別名稱相同。 此範例中的預設連接字串名稱會 `SchoolContext`，與您明確指定的相同。

### <a name="specify-singular-table-names"></a>指定單數資料表名稱

[OnModelCreating](https://msdn.microsoft.com/library/system.data.entity.dbcontext.onmodelcreating(v=vs.103).aspx)方法中的 `modelBuilder.Conventions.Remove` 語句會防止複數化資料表名稱。 如果您未這麼做，則資料庫中產生的資料表會命名為 `Students`、`Courses`和 `Enrollments`。 相反地，資料表名稱會是 `Student`、`Course`和 `Enrollment`。 針對是否要複數化資料表名稱，開發人員並沒有共識。 本教學課程使用單數形式，但重點在於，您可以藉由包含或省略這行程式碼來選取您偏好的任何格式。

## <a name="initialize-db-with-test-data"></a>使用測試資料將 DB 初始化

Entity Framework 可以在應用程式執行時，自動為您建立（或卸載並重新建立）資料庫。 您可以指定每次執行應用程式時，或只有在模型與現有資料庫不同步時，才會執行此作業。 您也可以撰寫 `Seed` 方法，Entity Framework 在建立資料庫之後自動呼叫，以便將測試資料填入其中。

預設行為是只在資料庫不存在時才建立它（如果模型已變更且資料庫已經存在，則會擲回例外狀況）。 在本節中，您將指定每當模型變更時，應該卸載並重新建立資料庫。 卸載資料庫會導致所有資料遺失。 這在開發期間通常是正常的，因為當重新建立資料庫時，會執行 `Seed` 方法，並重新建立您的測試資料。 但是在生產環境中，您通常不會想要在每次需要變更資料庫架構時遺失所有資料。 稍後您會看到如何使用 Code First 移轉變更資料庫架構，而不是卸載並重新建立資料庫，以處理模型變更。

1. 在 DAL 資料夾中，建立名為*SchoolInitializer.cs*的新類別檔案，並將範本程式碼取代為下列程式碼，這會在需要時建立資料庫，並將測試資料載入至新的資料庫。

   [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample8.cs)]

   `Seed` 方法會將資料庫內容物件當做輸入參數，而方法中的程式碼會使用該物件將新的實體加入至資料庫。 針對每個實體類型，程式碼會建立新實體的集合，並將其加入適當的 `DbSet` 屬性，然後將變更儲存至資料庫。 在每個實體群組之後，都不需要呼叫 `SaveChanges` 方法，但在這裡完成這項作業，但如果程式碼寫入資料庫時發生例外狀況，就會協助您找出問題的來源。

2. 若要告知 Entity Framework 使用您的初始化運算式類別，請將專案新增至應用程式*web.config*檔案中的 `entityFramework` 元素（根專案資料夾中的），如下列範例所示：

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample9.xml?highlight=2-6)]

   `context type` 會指定完整的內容類別名稱及其所在的元件，而 `databaseinitializer type` 會指定初始化運算式類別及其所在元件的完整名稱。 （當您不想讓 EF 使用初始化運算式時，可以在 `context` 元素上設定屬性： `disableDatabaseInitialization="true"`）。如需詳細資訊，請參閱[設定檔案設定](/ef/ef6/fundamentals/configuring/config-file)。

   在*web.config*檔案中設定初始化運算式的替代方法是，藉由將 `Database.SetInitializer` 語句加入至*Global.asax.cs*檔案中的 `Application_Start` 方法，在程式碼中執行此動作。 如需詳細資訊，請參閱[瞭解 Entity Framework Code First 中的資料庫初始化運算式](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)。

應用程式現在已設定，因此當您第一次在指定的應用程式執行中存取資料庫時，Entity Framework 會將資料庫與模型（您的 `SchoolContext` 和實體類別）做比較。 如果有差異，應用程式會卸載並重新建立資料庫。

> [!NOTE]
> 當您將應用程式部署到生產 web 伺服器時，您必須移除或停用卸載並重新建立資料庫的程式碼。 您將在本系列稍後的教學課程中執行此動作。

## <a name="set-up-ef-6-to-use-localdb"></a>設定 EF 6 使用 LocalDB

[LocalDB](/sql/database-engine/configure-windows/sql-server-2016-express-localdb?view=sql-server-2017)是輕量版的 SQL Server Express 資料庫引擎。 安裝和設定、視需要啟動，以及在使用者模式中執行，都很容易。 LocalDB 會在 SQL Server Express 的特殊執行模式下執行，可讓您使用資料庫做為 *.mdf*檔案。 如果您想要能夠使用專案來複製資料庫，您可以將 LocalDB 資料庫檔案放在 Web 專案的*應用程式\_Data*資料夾中。 SQL Server Express 中的使用者實例功能也可讓您使用 *.mdf*檔案，但是使用者實例功能已被取代;因此，建議使用 LocalDB 來處理 *.mdf*檔案。 LocalDB 預設會隨 Visual Studio 安裝。

通常，SQL Server Express 不會用於生產 web 應用程式。 不建議將 LocalDB 用於與 web 應用程式搭配使用的生產環境，因為它不是設計用於 IIS。

- 在本教學課程中，您將使用 LocalDB。 開啟*應用程式的 web.config 檔案*，然後在 `appSettings` 元素前面加入 `connectionStrings` 元素，如下列範例所示。 （請務必更新根專案資料夾*中的 web.config 檔案。* *Views*子資料夾中也*有一個 web.config*檔案，您不需要更新此檔案）。

   [!code-xml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample10.xml?highlight=1-3)]

您已新增的連接字串會指定 Entity Framework 將使用名為*ContosoUniversity1*的 LocalDB 資料庫。 （資料庫尚不存在，但 EF 會加以建立）。如果您想要在*應用程式\_Data*資料夾中建立資料庫，您可以將 `AttachDBFilename=|DataDirectory|\ContosoUniversity1.mdf` 新增至連接字串。 如需連接字串的詳細資訊，請參閱[SQL Server ASP.NET Web 應用程式的連接字串](/previous-versions/aspnet/jj653752(v=vs.110))。

您實際上不需要*在 web.config 檔案*中使用連接字串。 如果您未提供連接字串，Entity Framework 會根據您的內容類別來使用預設連接字串。 如需詳細資訊，請參閱[Code First 至新的資料庫](/ef/ef6/modeling/code-first/workflows/new-database)。

## <a name="create-controller-and-views"></a>建立控制器和檢視

現在您將建立網頁來顯示資料。 要求資料的程式會自動觸發資料庫的建立。 首先您要建立新的控制器。 但是在執行此動作之前，請先建立專案，讓模型和內容類別別可用於 MVC 控制器的架構。

1. 以滑鼠右鍵按一下**方案總管**中的 [**控制器**] 資料夾，選取 [**加入**]，然後按一下 [**新增 scaffold 專案**]。
2. 在 [**新增 Scaffold** ] 對話方塊中，使用 [Entity Framework] 選取 [**具有視圖的 MVC 5 控制器**]，然後選擇 [**新增**]。

     ![Visual Studio 中的 [新增 Scaffold] 對話方塊](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/add-scaffold.png)

3. 在 [**新增控制器**] 對話方塊中，進行下列選擇，然後選擇 [**新增**]：

   - 模型類別： **Student （ContosoUniversity）** 。 （如果您在下拉式清單中看不到這個選項，請建立專案，然後再試一次）。
   - 資料內容類別： **SchoolCoNtext （ContosoUniversity）** 。
   - 控制器名稱： **StudentController** （不是 studentscontroller.cs）。
   - 保留其他欄位的預設值。

     當您按一下 [**新增**] 時，scaffolder 會建立一個*StudentController.cs*檔，以及一組可與控制器搭配使用的視圖（ *. cshtml*檔案）。 在未來建立使用 Entity Framework 的專案時，您也可以利用 scaffolder 的一些額外功能：建立您的第一個模型類別、不要建立連接字串，然後在 [**新增控制器**] 方塊中選取 [**資料內容類別**] 旁邊的 [ **+** ] 按鈕，以指定**新的資料內容**。 Scaffolder 會建立您的 `DbContext` 類別和您的連接字串，以及控制器和 views。
4. Visual Studio 會開啟*Controllers\StudentController.cs*檔案。 您會看到已建立可具現化資料庫內容物件的類別變數：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample11.cs)]

     `Index` 動作方法會藉由讀取資料庫內容實例的 `Students` 屬性，從*學生*實體集取得學生的清單：

     [!code-csharp[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample12.cs)]

     *Student\Index.cshtml* view 會在資料表中顯示此清單：

     [!code-cshtml[Main](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/samples/sample13.cshtml)]
5. 按 Ctrl+F5 執行專案。 （如果您收到「無法建立陰影複製」錯誤，請關閉瀏覽器，然後再試一次）。

     按一下 [**學生**] 索引標籤，查看 `Seed` 方法所插入的測試資料。 視瀏覽器視窗的範圍而定，您會在頂端的網址列中看到 [Student] 索引標籤連結，或者您必須按一下右上角才能看到連結。

     ![功能表按鈕](creating-an-entity-framework-data-model-for-an-asp-net-mvc-application/_static/image14.png)

## <a name="view-the-database"></a>檢視資料庫

當您執行 [學生] 頁面，而應用程式嘗試存取資料庫時，EF 發現沒有資料庫，而且已建立一個。 EF 接著會執行種子方法，將資料填入資料庫。

您可以使用**伺服器總管**或**SQL Server 物件總管**（SSOX），在 Visual Studio 中查看資料庫。 在本教學課程中，您將使用**伺服器總管**。

1. 關閉瀏覽器。
2. 在**伺服器總管**中，展開 [**資料連線**] （您可能需要先選取 [重新整理] 按鈕）、展開 [ **School CoNtext （ContosoUniversity）** ]，然後展開 [**資料表]** ，以查看新資料庫中的資料表。

3. 以滑鼠右鍵按一下 [ **Student** ] 資料表，然後按一下 [**顯示資料表資料**]，以查看已建立的資料行以及已插入資料表中的資料列。

4. 關閉**伺服器總管**連接。

*ContosoUniversity1*是 *% USERPROFILE%* 資料夾中*的資料庫檔案。*

因為您使用的是 `DropCreateDatabaseIfModelChanges` 初始化運算式，所以您現在可以變更 `Student` 類別、再次執行應用程式，而且會自動重新建立資料庫以符合您的變更。 例如，如果您將 `EmailAddress` 屬性加入 `Student` 類別，請再次執行 [學生] 頁面，然後再次查看資料表，您會看到新的 `EmailAddress` 資料行。

## <a name="conventions"></a>慣例

為了讓 Entity Framework 能夠為您建立完整資料庫，您必須撰寫的程式碼數量最少，因為*慣例*或 Entity Framework 所做的假設。 其中有些是已記下或已使用，而不需要您知道它們：

- 實體類別名稱的複數化形式會當做資料表名稱使用。
- 實體屬性名稱會用於資料行名稱。
- 名為 `ID` 或*classname* `ID` 的實體屬性會被辨識為主鍵屬性。
- 如果將屬性命名為 *&lt;導覽屬性名稱&gt;&lt;主鍵屬性名稱&gt;* （例如 `StudentID` `Student` 實體的主要索引鍵 `Student`），則會將其視為外鍵屬性。`ID` 外鍵屬性也可以命名為相同 &lt;主鍵屬性名稱&gt; （例如 `EnrollmentID`，因為 `Enrollment` 實體的主要索引鍵是 `EnrollmentID`）。

您已瞭解可以覆寫慣例。 例如，您指定不應複數化資料表名稱，稍後您會看到如何將屬性明確地標示為外鍵屬性。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

如需 EF 6 的詳細資訊，請參閱下列文章：

* [ASP.NET 資料存取 - 建議資源](../../../../whitepapers/aspnet-data-access-content-map.md)

* [Code First 慣例](/ef/ef6/modeling/code-first/conventions/built-in)

* [建立更複雜的資料模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 建立 MVC web 應用程式
> * 設定網站樣式
> * 已安裝 Entity Framework 6
> * 建立資料模型
> * 建立資料庫內容
> * 使用測試資料將 DB 初始化
> * 設定 EF 6 使用 LocalDB
> * 建立控制器和檢視
> * 檢視資料庫

前往下一篇文章，以瞭解如何在您的控制器和 views 中檢查和自訂建立、讀取、更新、刪除（CRUD）程式碼。
> [!div class="nextstepaction"]
> [實作基本的 CRUD 功能](implementing-basic-crud-functionality-with-the-entity-framework-in-asp-net-mvc-application.md)