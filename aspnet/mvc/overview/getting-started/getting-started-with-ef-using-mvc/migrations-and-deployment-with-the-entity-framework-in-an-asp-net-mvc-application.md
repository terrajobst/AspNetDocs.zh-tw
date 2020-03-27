---
uid: mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
title: 教學課程：在 ASP.NET MVC 應用程式中使用 EF 遷移並部署至 Azure
author: tdykstra
description: 在本教學課程中，您會啟用 Code First 遷移，並將應用程式部署至 Azure 中的雲端。
ms.author: riande
ms.date: 01/16/2019
ms.topic: tutorial
ms.assetid: d4dfc435-bda6-4621-9762-9ba270f8de4e
msc.legacyurl: /mvc/overview/getting-started/getting-started-with-ef-using-mvc/migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application
msc.type: authoredcontent
ms.openlocfilehash: 989dd0f0e18b338be057b9c5657586eff996d8ea
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78616078"
---
# <a name="tutorial-use-ef-migrations-in-an-aspnet-mvc-app-and-deploy-to-azure"></a>教學課程：在 ASP.NET MVC 應用程式中使用 EF 遷移並部署至 Azure

到目前為止，Contoso 大學範例 web 應用程式都是在您的開發電腦上，于本機執行 IIS Express。 若要讓其他人可以透過網際網路使用實際的應用程式，您必須將它部署到 web 主控提供者。 在本教學課程中，您會啟用 Code First 遷移，並將應用程式部署至 Azure 中的雲端：

- 啟用 Code First 移轉。 「遷移」功能可讓您變更資料模型，並藉由更新資料庫架構來將變更部署至生產環境，而不需要卸載和重新建立資料庫。
- 部署至 Azure。 這是選擇性步驟;您可以繼續進行其餘的教學課程，而不需要部署專案。

建議您使用持續整合程式與原始檔控制進行部署，但本教學課程並未涵蓋這些主題。 如需詳細資訊，請參閱[使用 Azure 建立真實世界的雲端應用程式](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/introduction)的[原始檔控制](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/source-control)和[連續整合](xref:aspnet/overview/developing-apps-with-windows-azure/building-real-world-cloud-apps-with-windows-azure/continuous-integration-and-continuous-delivery)章節。

在本教學課程中，您已：

> [!div class="checklist"]
> * 啟用 Code First 遷移
> * 在 Azure 中部署應用程式（選擇性）

## <a name="prerequisites"></a>Prerequisites

- [連線恢復功能和命令攔截](connection-resiliency-and-command-interception-with-the-entity-framework-in-an-asp-net-mvc-application.md)

## <a name="enable-code-first-migrations"></a>啟用 Code First 遷移

在開發新的應用程式時，您的資料模型會頻繁變更，而每次模型變更時，模型會與資料庫不同步。 您已設定 Entity Framework 在每次變更資料模型時，自動卸載並重新建立資料庫。 當您加入、移除或變更實體類別或變更 `DbContext` 類別時，下次執行應用程式時，它會自動刪除現有的資料庫、建立符合模型的新資料庫，並植入測試資料。

在您將應用程式部署到生產環境之前，都可以使用上述方法讓資料庫與資料模型保持同步。 當應用程式在生產環境中執行時，通常會儲存您想要保留的資料，而您不想在每次進行變更（例如加入新的資料行）時遺失所有專案。 [Code First 移轉](https://msdn.microsoft.com/data/jj591621)功能可解決這個問題，方法是啟用 Code First 更新資料庫架構，而不是卸載並重新建立資料庫。 在本教學課程中，您將部署應用程式，並準備好讓您啟用遷移。

1. 藉由批註化或刪除您新增至應用程式 Web.config 檔案的 `contexts` 專案，停用您稍早設定的初始化運算式。

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample1.xml?highlight=2,6)]
2. 此外，*在應用程式的 web.config 檔案*中，將連接字串中的資料庫名稱變更為 ContosoUniversity2。

    [!code-xml[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample2.xml?highlight=2)]

    這種變更會設定專案，讓第一次遷移建立新的資料庫。 這不是必要的，但您稍後會看到這是很好的主意。
3. 從 [工具] 功能表中，選取 [NuGet 套件管理員] >  [套件管理員主控台]。

1. 在 `PM>` 提示字元中，輸入下列命令：

    ```text
    enable-migrations
    add-migration InitialCreate
    ```

    `enable-migrations` 命令會在 ContosoUniversity 專案中建立一個 [*遷移*] 資料夾，它會將*Configuration.cs*檔案放在該資料夾中，供您編輯以設定遷移。

    （如果您錯過上述步驟，引導您變更資料庫名稱，則遷移會尋找現有的資料庫，並自動執行 `add-migration` 命令。 這沒什麼問題，只是表示您不會在部署資料庫之前執行遷移程式碼的測試。 稍後當您執行 `update-database` 命令時，不會發生任何事，因為資料庫已經存在）。

    開啟*ContosoUniversity\Migrations\Configuration.cs*檔案。 如同您稍早所見的初始化運算式類別，`Configuration` 類別包含 `Seed` 的方法。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample3.cs)]

    [種子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法的目的是要讓您在 Code First 建立或更新資料庫之後，插入或更新測試資料。 當資料庫建立時，以及每次在資料模型變更之後更新資料庫架構時，就會呼叫方法。

### <a name="set-up-the-seed-method"></a>設定種子方法

當您卸載並重新建立每個資料模型變更的資料庫時，會使用初始化運算式類別的 `Seed` 方法來插入測試資料，因為在每個模型變更之後，就會卸載資料庫，而且所有測試資料都會遺失。 使用 Code First 移轉，在資料庫變更之後會保留測試資料，因此通常不需要在[種子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法中包含測試資料。 事實上，如果您要使用遷移將資料庫部署到生產環境，您不希望 `Seed` 方法插入測試資料，因為 `Seed` 方法將會在生產環境中執行。 在這種情況下，您想要 `Seed` 方法只將生產環境中所需的資料插入資料庫中。 例如，當應用程式在生產環境中可供使用時，您可能會想要讓資料庫在 `Department` 資料表中包含實際的部門名稱。

在本教學課程中，您將使用遷移來進行部署，但您的 `Seed` 方法仍會插入測試資料，讓您更輕鬆地查看應用程式功能的運作方式，而不需要手動插入大量資料。

1. 將*Configuration.cs*檔案的內容取代為下列程式碼，以將測試資料載入至新的資料庫。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample4.cs)]

    [種子](https://msdn.microsoft.com/library/hh829453(v=vs.103).aspx)方法會將資料庫內容物件當做輸入參數，而方法中的程式碼會使用該物件將新的實體加入至資料庫。 針對每個實體類型，程式碼會建立新實體的集合，並將其加入至適當的[DbSet](https://msdn.microsoft.com/library/system.data.entity.dbset(v=vs.103).aspx)屬性，然後將變更儲存至資料庫。 您不需要在每個實體群組之後呼叫[SaveChanges](https://msdn.microsoft.com/library/system.data.entity.dbcontext.savechanges(v=VS.103).aspx)方法，這是在這裡完成，但如果在程式碼寫入資料庫時發生例外狀況，這樣做可協助您找出問題的來源。

    某些插入資料的語句會使用[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法來執行「upsert」作業。 由於 `Seed` 方法會在您每次執行 `update-database` 命令時執行（通常是在每個遷移之後），因此您不能只插入資料，因為在第一次建立資料庫的遷移之後，您嘗試加入的資料列已經存在。 如果您嘗試插入已經存在的資料列，則 "upsert" 作業會防止發生錯誤，但它會***覆寫***您在測試應用程式時所做的任何變更。 在某些資料表中使用測試資料時，您可能不會想要這樣做：在某些情況下，當您在測試時變更資料，而您想要在資料庫更新之後維持變更。 在此情況下，您想要執行條件式插入作業：只有在不存在資料列時，才插入它。 種子方法會使用這兩個方法。

    傳遞至[AddOrUpdate](https://msdn.microsoft.com/library/system.data.entity.migrations.idbsetextensions.addorupdate(v=vs.103).aspx)方法的第一個參數會指定要用來檢查資料列是否已經存在的屬性。 對於您所提供的測試學生資料，`LastName` 屬性可以用於此用途，因為清單中的每個姓氏都是唯一的：

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample5.cs)]

    此程式碼假設姓氏是唯一的。 如果您以手動方式新增姓氏重複的學生，則會在下一次執行遷移時收到下列例外狀況：

    **序列包含一個以上的元素**

    如需如何處理重復資料（例如名為 "Alexander Carson" 的兩名學生）的相關資訊，請參閱 Rick Anderson 的 blog 上的[植入和偵錯工具 Entity Framework （EF） db](https://blogs.msdn.com/b/rickandy/archive/2013/02/12/seeding-and-debugging-entity-framework-ef-dbs.aspx) 。 如需有關 `AddOrUpdate` 方法的詳細資訊，請參閱 Julie Lerman 的 blog 上的[使用 EF 4.3 AddOrUpdate 方法](http://thedatafarm.com/blog/data-access/take-care-with-ef-4-3-addorupdate-method/)。

    建立 `Enrollment` 實體的程式碼會假設您在 `students` 集合的實體中有 `ID` 值，雖然您並未在建立集合的程式碼中設定該屬性。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample6.cs?highlight=2)]

    您可以使用這裡的 `ID` 屬性，因為當您呼叫 `students` 集合的 `SaveChanges` 時，會設定 `ID` 值。 EF 會在將實體插入資料庫時，自動取得主要金鑰值，而且會在記憶體中更新實體的 `ID` 屬性。

    將每個 `Enrollment` 實體加入 `Enrollments` 實體集的程式碼，不會使用 `AddOrUpdate` 方法。 它會檢查實體是否已存在，並插入實體（如果不存在）。 這個方法會保留您使用應用程式 UI 對註冊等級所做的變更。 程式碼會對 `Enrollment`[清單](https://msdn.microsoft.com/library/6sh2ey19.aspx)的每個成員執行迴圈，如果在資料庫中找不到註冊，就會將註冊加入至資料庫。 當您第一次更新資料庫時，資料庫將會是空的，因此它會新增每個註冊。

    [!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample7.cs)]

2. 建置專案。

### <a name="execute-the-first-migration"></a>執行第一次遷移

當您執行 `add-migration` 命令時，遷移所產生的程式碼會從頭開始建立資料庫。 此程式碼也位於 [*遷移*] 資料夾中，名稱為 *&lt;timestamp&gt;\_InitialCreate.cs*的檔案中。 `InitialCreate` 類別的 `Up` 方法會建立對應至資料模型實體集的資料庫資料表，而 `Down` 方法會將它們刪除。

[!code-csharp[Main](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/samples/sample8.cs)]

移轉會呼叫 `Up` 方法，以實作資料模型變更來進行移轉。 當您輸入命令以復原更新時，Migrations 會呼叫 `Down` 方法。

這是您在輸入 `add-migration InitialCreate` 命令時所建立的初始遷移。 參數（在範例中`InitialCreate`）會用於檔案名，而且可以是任何您想要的名稱;您通常會選擇一個字組或片語，以摘要說明在遷移中完成的作業。 例如，您可以將稍後的遷移命名 &quot;AddDepartmentTable&quot;。

如果在您建立初始移轉時資料庫已經存在，系統會產生資料庫建立程式碼，但不需要執行，因為資料庫已經符合資料模型。 當您將應用程式部署到資料庫尚未存在的其他環境中時，即會執行這個程式碼以建立您的資料庫；建議您先進行測試。 這就是為什麼您在先前的連接字串中變更資料庫名稱&mdash;，讓遷移可以從頭開始建立新的。

1. 在 [Package Manager Console] 視窗中，輸入下列命令：

    `update-database`

    `update-database` 命令會執行 `Up` 方法來建立資料庫，然後執行 `Seed` 方法來填入資料庫。 當您部署應用程式之後，相同的進程會在生產環境中自動執行，如下一節所示。
2. 使用**伺服器總管**來檢查資料庫，如同您在第一個教學課程中所做的一樣，然後執行應用程式來確認所有專案的運作方式都與之前相同。

## <a name="deploy-to-azure"></a>部署到 Azure

到目前為止，應用程式已在您的開發電腦上，于本機執行 IIS Express。 若要讓其他人可以透過網際網路使用它，您必須將它部署到 web 主控提供者。 在本教學課程的這一節中，您會將它部署至 Azure。 這是選擇性區段;您可以略過此動作並繼續進行下列教學課程，或者您可以針對您選擇的不同主控提供者，調整本節中的指示。

### <a name="use-code-first-migrations-to-deploy-the-database"></a>使用 Code First 遷移來部署資料庫

若要部署資料庫，您將使用 Code First 移轉。 當您建立用來設定從 Visual Studio 部署之設定的發行設定檔時，您會選取標示為 [**更新資料庫**] 的核取方塊。 這項設定會導致部署程式在目的地伺服器上自動設定應用程式*的 web.config 檔案*，讓 Code First 使用 `MigrateDatabaseToLatestVersion` 初始化運算式類別。

Visual Studio 在將您的專案複製到目的地伺服器時，不會在部署程式期間對資料庫執行任何動作。 當您執行已部署的應用程式，並在部署後第一次存取資料庫時，Code First 會檢查資料庫是否符合資料模型。 如果有不相符的情況，Code First 會自動建立資料庫（如果尚不存在），或將資料庫架構更新為最新版本（如果資料庫存在但不符合模型）。 如果應用程式 `Seed` 方法來執行遷移，則在建立資料庫或更新架構之後，就會執行此方法。

您的遷移 `Seed` 方法會插入測試資料。 如果您要部署到生產環境，您必須變更 `Seed` 方法，使其只插入您想要插入至實際執行資料庫的資料。 例如，在您目前的資料模型中，您可能想要在開發資料庫中擁有真實的課程，但虛構的學生。 您可以撰寫一個 `Seed` 方法，在開發期間載入，然後在部署到生產環境之前，先將虛構的學生加上批註。 或者，您也可以撰寫 `Seed` 的方法，只載入課程，並使用應用程式的 UI，以手動方式在測試資料庫中輸入虛構的學生。

### <a name="get-an-azure-account"></a>取得 Azure 帳戶

您將需要 Azure 帳戶。 如果您還沒有訂用帳戶，但您有 Visual Studio 訂用帳戶，您可以[啟用您的訂](https://azure.microsoft.com/pricing/member-offers/credit-for-visual-studio-subscribers/
)用帳戶權益。 否則，您只需要幾分鐘的時間就可以建立免費試用帳戶。 如需詳細資料，請參閱 [Azure 免費試用](https://azure.microsoft.com/free/)。

### <a name="create-a-web-site-and-a-sql-database-in-azure"></a>在 Azure 中建立網站和 SQL 資料庫

您在 Azure 中的 web 應用程式將會在共用主控環境中執行，這表示它會在與其他 Azure 用戶端共用的虛擬機器（Vm）上執行。 共用主控環境是一種在雲端中開始營運的低成本方法。 因為應用程式是在專用 VM 上執行，所以如果日後您的 Web 流量增加，可依需求對應用程式進行延展。 若要深入瞭解 Azure App Service 的定價選項，請參閱[App Service 定價](https://azure.microsoft.com/pricing/details/app-service/)。

您會將資料庫部署至 Azure SQL database。 SQL database 是以 SQL Server 技術為基礎的雲端式關係資料庫服務。 搭配使用 SQL Server 的工具和應用程式也可以使用 SQL database。

1. 在[Azure 管理入口網站](https://portal.azure.com)中，選擇左側索引標籤中的 [**建立資源**]，然後選擇**新**窗格 *（或分頁*）上的 [**查看全部**]，以查看所有可用的資源。 在 [**所有專案**] 分頁的 [ **web** ] 區段中，選擇 [ **web 應用程式 + SQL** ]。 最後，選擇 [**建立**]。

    ![在 Azure 入口網站中建立資源](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/create-azure-resource.png)

   [建立新的**Web 應用程式 + SQL**資源] 表單隨即開啟。

2. 在 [**應用程式名稱**] 方塊中輸入字串，以做為應用程式的唯一 URL。 完整的 URL 將包含您在此處輸入的內容，加上 Azure App 服務（. azurewebsites.net）的預設網域。 如果已採用**應用程式名稱**，則會以紅色通知您*應用程式名稱 [無法使用*] 訊息。 如果**應用程式名稱**可用，您會看到綠色核取記號。

3. 在 [**訂**用帳戶] 方塊中，選擇您想要**App Service**所在的 Azure 訂用帳戶。

4. 在 [**資源群組**] 文字方塊中，選擇資源群組或建立一個新的。 此設定會指定您的網站將在哪一個資料中心執行。 如需資源群組的詳細資訊，請參閱[資源群組](/azure/azure-resource-manager/resource-group-overview#resource-groups)。

5. 按一下 [ *App Service] 區段*、[**建立新**的] 和 [填入**App Service 方案**（可以與 App Service 相同的名稱）]、[**位置**] 和 [**定價層**] （有一個免費選項）來建立新的**App Service 計畫**。

6. 按一下 [ **SQL Database**]，然後選擇 [**建立新的資料庫**] 或選取現有的資料庫。

7. 在 [**名稱**] 方塊中，輸入您的資料庫名稱。
8. 按一下 [**目標伺服器**] 方塊，然後選取 [**建立新的伺服器**]。 或者，如果您先前已建立伺服器，您可以從可用伺服器清單中選取該伺服器。
9. 選擇 [**定價層**] 區段，選擇 [*免費*]。 如果需要額外的資源，可以隨時調整資料庫。 若要深入瞭解 Azure SQL 定價，請參閱[Azure SQL Database 定價](https://azure.microsoft.com/pricing/details/sql-database/managed/)。
10. 視需要修改定[序](/sql/relational-databases/collations/collation-and-unicode-support)。
11. 輸入系統管理員**Sql 管理員使用者名稱**和**sql 管理員密碼**。

    - 如果您選取 [**新增 SQL Database 伺服器**]，請定義新的名稱和密碼，以便稍後在存取資料庫時使用。
    - 如果您選取先前建立的伺服器，請輸入該伺服器的認證。

12. 您可以使用 Application Insights 來啟用 App Service 的遙測集合。 透過少量設定，Application Insights 會收集重要的事件、例外狀況、相依性、要求和追蹤資訊。 若要深入瞭解 Application Insights，請參閱[Azure 監視器](https://azure.microsoft.com/services/monitor/)。
13. 按一下底部的 [**建立**]，表示您已經完成。

    管理入口網站會回到 [儀表板] 頁面，而頁面頂端的 [**通知**] 區域會顯示正在建立的網站。 一段時間後（通常不到一分鐘），就會有部署成功的通知。 在左側的導覽列中，新的 App Service 會出現在 [**應用程式服務**] 區段中，而新的 sql 資料庫會出現在 [ **sql 資料庫**] 區段中。

### <a name="deploy-the-app-to-azure"></a>將應用程式部署至 Azure

1. 在 Visual Studio 的 [方案總管] 中以滑鼠右鍵按一下專案，再選取內容功能表中的 [發佈]。

2. 在 [**挑選發行目標**] 頁面上，選擇 [ **App Service** ]，然後**選取 [現有**]，然後選擇 [**發佈**]。

    ![挑選發行目標頁面](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/publish-select-existing-azure-app-service.png)

3. 如果您先前尚未在 Visual Studio 中新增您的 Azure 訂用帳戶，請在畫面上執行步驟。 這些步驟可讓 Visual Studio 連接到您的 Azure 訂用帳戶，讓**應用程式服務**清單包含您的網站。

4. 在 [ **App Service** ] 頁面上，選取您已新增 App Service 的**訂**用帳戶。 在 [ **View**] 底下，選取 [**資源群組**]。 展開您已新增 App Service 的資源群組，然後選取 [App Service]。 選擇 **[確定]** 以發佈應用程式。

5. [輸出] 視窗會顯示已採取的部署動作，並報告部署作業已順利完成。

6. 部署成功時，預設瀏覽器會自動開啟至已部署網站的 URL。

    ![Students_index_page_with_paging](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/cloud-app-browser.png)

    您的應用程式現在正在雲端中執行。

此時，已在 Azure SQL 資料庫中建立*SchoolCoNtext*資料庫，因為您選取了 **[執行 Code First 移轉] （在應用程式啟動時執行）** 。 已部署網站*中的 web.config*檔案已經變更，因此[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始化運算式會在程式碼第一次讀取或寫入資料庫中的資料時執行（在您選取 [**學生**] 索引標籤時，會發生這種情況）：

![Web.config 檔案摘錄](https://asp.net/media/4367421/mig.png)

部署程式也會建立新的連接字串 *（SchoolCoNtext\_DatabasePublish*），以供 Code First 移轉用來更新資料庫架構和植入資料庫。

![Web.config 檔案中的連接字串](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/image26.png)

您可以在*ContosoUniversity\obj\Release\Package\PackageTmp\Web.config*中的電腦上，找到已部署的 web.config 檔案版本。您可以使用 FTP 來存取已部署的*web.config*檔案本身。 如需指示，請參閱[使用 Visual Studio ASP.NET Web 部署：部署程式碼更新](xref:web-forms/overview/deployment/visual-studio-web-deployment/deploying-a-code-update)。 依照開頭為「使用 FTP 工具」的指示進行，您需要三個專案： FTP URL、使用者名稱和密碼。

> [!NOTE]
> Web 應用程式不會執行安全性，因此任何尋找 URL 的人都可以變更資料。 如需如何保護網站的指示，請參閱[將具有成員資格、OAuth 和 SQL database 的安全 ASP.NET MVC 應用程式部署至 Azure](/aspnet/core/security/authorization/secure-data)。 您可以使用 Azure 管理入口網站或 Visual Studio 中的**伺服器總管**停止服務，以防止其他人使用該網站。

![停止 app service 功能表項目](migrations-and-deployment-with-the-entity-framework-in-an-asp-net-mvc-application/_static/server-explorer-stop-app-service.png)

## <a name="advanced-migrations-scenarios"></a>先進的遷移案例

如果您依照本教學課程中的指示自動執行遷移來部署資料庫，而且您要部署到在多部伺服器上執行的網站，您可以讓多部伺服器同時嘗試執行遷移。 遷移是不可部分完成的，因此如果兩部伺服器嘗試執行相同的遷移，其中一個會成功，另一個則失敗（假設作業無法完成兩次）。 在該案例中，如果您想要避免這些問題，您可以手動呼叫遷移，並設定您自己的程式碼，使其只會發生一次。 如需詳細資訊，請參閱從 Rowan 中的程式[代碼執行和腳本遷移](http://romiller.com/2012/02/09/running-scripting-migrations-from-code/)的 Blog 和[遷移 .exe](/ef/ef6/modeling/code-first/migrations/migrate-exe) （從命令列執行遷移）。

如需其他遷移案例的詳細資訊，請參閱[遷移螢幕錄製影片系列](https://blogs.msdn.com/b/adonet/archive/2014/03/12/migrations-screencast-series.aspx)。

## <a name="update-specific-migration"></a>更新特定的遷移

`update-database -target MigrationName`

`update-database -target MigrationName` 命令會執行目標遷移。

## <a name="ignore-migration-changes-to-database"></a>忽略資料庫的遷移變更

`Add-migration MigrationName -ignoreChanges`

`ignoreChanges` 使用目前的模型做為快照集來建立空的遷移。

## <a name="code-first-initializers"></a>Code First 初始化運算式

在 [部署] 區段中，您會看到使用的[MigrateDatabaseToLatestVersion](https://msdn.microsoft.com/library/hh829476(v=vs.103).aspx)初始化運算式。 Code First 也會提供其他初始化運算式，包括[CreateDatabaseIfNotExists](https://msdn.microsoft.com/library/gg679221(v=vs.103).aspx) （預設值）、 [DropCreateDatabaseIfModelChanges](https://msdn.microsoft.com/library/gg679604(v=VS.103).aspx) （您先前使用的）和[DropCreateDatabaseAlways](https://msdn.microsoft.com/library/gg679506(v=VS.103).aspx)。 `DropCreateAlways` 初始化運算式有助於設定單元測試的條件。 您也可以撰寫自己的初始化運算式，如果您不想等到應用程式讀取或寫入資料庫，可以明確地呼叫初始化運算式。

如需初始化運算式的詳細資訊，請參閱 <>[瞭解 Entity Framework 中的資料庫初始化運算式 Code First](http://www.codeguru.com/csharp/article.php/c19999/Understanding-Database-Initializers-in-Entity-Framework-Code-First.htm)和 < 程式設計的第6章[Entity Framework：](http://shop.oreilly.com/product/0636920022220.do) Julie Lerman 和 Rowan 莎莎的 Code First。

## <a name="get-the-code"></a>取得程式碼

[下載已完成的專案](https://webpifeed.blob.core.windows.net/webpifeed/Partners/ASP.NET%20MVC%20Application%20Using%20Entity%20Framework%20Code%20First.zip)

## <a name="additional-resources"></a>其他資源

您可以在[ASP.NET 資料存取-建議的資源](xref:whitepapers/aspnet-data-access-content-map)中找到其他 Entity Framework 資源的連結。

## <a name="next-steps"></a>後續步驟

在本教學課程中，您已：

> [!div class="checklist"]
> * 已啟用 Code First 遷移
> * 已在 Azure 中部署應用程式（選擇性）

前進到下一篇文章，以瞭解如何為 ASP.NET MVC 應用程式建立更複雜的資料模型。
> [!div class="nextstepaction"]
> [建立更複雜的資料模型](creating-a-more-complex-data-model-for-an-asp-net-mvc-application.md)
