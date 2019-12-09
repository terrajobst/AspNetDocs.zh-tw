---
uid: web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
title: 使用 SQL 快取相依性（VB） |Microsoft Docs
author: rick-anderson
description: 最簡單的快取策略是允許快取的資料在指定的一段時間後過期。 但這種簡單的方法表示快取的資料 maintai 。
ms.author: riande
ms.date: 05/30/2007
ms.assetid: bd347d93-4251-4532-801c-a36f2dfa7f96
msc.legacyurl: /web-forms/overview/data-access/caching-data/using-sql-cache-dependencies-vb
msc.type: authoredcontent
ms.openlocfilehash: 7d095538bd92d50675e5fce44f5ca68e8ee6c0e8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74603627"
---
# <a name="using-sql-cache-dependencies-vb"></a>使用 SQL 快取相依性 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_61_VB.zip)或[下載 PDF](using-sql-cache-dependencies-vb/_static/datatutorial61vb1.pdf)

> 最簡單的快取策略是允許快取的資料在指定的一段時間後過期。 但這種簡單的方法表示快取的資料不會與基礎資料來源保持關聯，因而導致過時的資料保留太長，或目前的資料太久過期。 較好的方法是使用 SqlCacheDependency 類別，讓資料保持快取狀態，直到其基礎資料在 SQL 資料庫中修改為止。 本教學課程將為您示範作法。

## <a name="introduction"></a>簡介

在使用架構教學課程中的 ObjectDataSource 和快取[資料](caching-data-in-the-architecture-vb.md)快取[資料](caching-data-with-the-objectdatasource-vb.md)中所檢查的快取技術，使用以時間為基礎的到期，在指定的期間後從快取收回資料。 這種方法是平衡快取的效能提升與資料過期的最簡單方式。 藉由選取*x*秒的時間到期日，頁面開發人員 concedes 以享有僅限*x*秒快取的效能優勢，但可以很容易，她的資料永遠不會超過最大*x*秒的長度。 當然，對於靜態資料， *x*可以延伸至 web 應用程式的存留期，如在[應用程式啟動時](caching-data-at-application-startup-vb.md)快取資料教學課程中所述。

當快取資料庫資料時，通常會選擇以時間為基礎的到期日來方便使用，但通常是不充分的解決方案。 在理想的情況下，資料庫資料會保持快取狀態，直到資料庫中的基礎資料經過修改為止。只有這樣才會收回快取。 這種方法可將快取的效能優勢最大化，並將過時資料的持續時間降到最低。 不過，為了享受這些優點，必須有一些系統準備好知道基礎資料庫資料何時已修改，並從快取中收回對應的專案。 在 ASP.NET 2.0 之前，網頁開發人員負責執行此系統。

ASP.NET 2.0 提供[`SqlCacheDependency` 類別](https://msdn.microsoft.com/library/system.web.caching.sqlcachedependency.aspx)和必要的基礎結構，以判斷資料庫中發生變更時，可以收回對應的快取專案。 有兩種技術可判斷基礎資料何時變更：通知和輪詢。 討論通知和輪詢之間的差異之後，我們將建立支援輪詢所需的基礎結構，然後探索如何在宣告式和以程式設計方式中使用 `SqlCacheDependency` 類別。

## <a name="understanding-notification-and-polling"></a>瞭解通知和輪詢

有兩種技術可以用來判斷資料庫中的資料何時已修改：通知和輪詢。 透過通知，當特定查詢的結果在上次執行查詢之後已經變更時，資料庫就會自動發出警示 ASP.NET 執行時間，此時會收回與查詢相關聯的快取專案。 使用輪詢時，資料庫伺服器會維護特定資料表上次更新時間的相關資訊。 ASP.NET 執行時間會定期輪詢資料庫，以檢查哪些資料表在輸入快取之後已經變更。 已修改資料的資料表會收回其相關聯的快取專案。

通知選項所需的安裝比輪詢少，而且更細微，因為它會追蹤查詢層級的變更，而不是在資料表層級。 可惜的是，通知僅適用于 Microsoft SQL Server 2005 的完整版本（亦即，非 Express 版本）。 不過，您可以使用 [輪詢] 選項，將所有版本的 Microsoft SQL Server 從7.0 到2005。 由於這些教學課程使用 SQL Server 2005 的 Express edition，因此我們將著重于設定和使用 [輪詢] 選項。 如需 SQL Server 2005 s 通知功能的進一步資源，請參閱本教學課程結尾的進一步閱讀章節。

使用輪詢時，資料庫必須設定為包含名為 `AspNet_SqlCacheTablesForChangeNotification` 的資料表，其中包含三個數據行： `tableName`、`notificationCreated`和 `changeId`。 此資料表包含每個資料表的資料列，其中有可能需要在 web 應用程式的 SQL 快取相依性中使用的資料。 [`tableName`] 資料行會指定資料表的名稱，而 `notificationCreated` 則表示資料列加入至資料表的日期和時間。 `changeId` 資料行的類型是 `int`，其初始值為0。 其值會隨著資料表的每次修改而遞增。

除了 `AspNet_SqlCacheTablesForChangeNotification` 資料表以外，資料庫也需要在可能出現在 SQL 快取相依性中的每個資料表上包含觸發程式。 每當插入、更新或刪除資料列，並在 `AspNet_SqlCacheTablesForChangeNotification`中遞增資料表的 `changeId` 值時，就會執行這些觸發程式。

當使用 `SqlCacheDependency` 物件快取資料時，ASP.NET 執行時間會追蹤資料表的目前 `changeId`。 系統會定期檢查資料庫，而且 `changeId` 與資料庫中的值不同的任何 `SqlCacheDependency` 物件都會被收回，因為不同的 `changeId` 值表示自快取資料以來已經變更了資料表。

## <a name="step-1-exploring-theaspnet_regsqlexecommand-line-program"></a>步驟1：探索`aspnet_regsql.exe`命令列程式

使用輪詢方法時，必須將資料庫設定為包含上述的基礎結構：預先定義的資料表（`AspNet_SqlCacheTablesForChangeNotification`）、少數的預存程式，以及可用於 web 應用程式中 SQL 快取相依性的每個資料表上的觸發程式。 您可以透過命令列程式 `aspnet_regsql.exe`建立這些資料表、預存程式和觸發程式，這可在 [`$WINDOWS$\Microsoft.NET\Framework\version`] 資料夾中找到。 若要建立 `AspNet_SqlCacheTablesForChangeNotification` 資料表和相關聯的預存程式，請從命令列執行下列命令：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample1.cmd)]

> [!NOTE]
> 若要執行這些命令，指定的資料庫登入必須位於[`db_securityadmin`](https://msdn.microsoft.com/library/ms188685.aspx)和[`db_ddladmin`](https://msdn.microsoft.com/library/ms190667.aspx)角色中。 若要檢查 `aspnet_regsql.exe` 命令列程式傳送至資料庫的 T-sql，請參閱[此 blog 專案](http://scottonwriting.net/sowblog/posts/10709.aspx)。

例如，若要使用 Windows 驗證將輪詢的基礎結構新增至名為 `ScottsServer` 的資料庫伺服器上名為 `pubs` 的 Microsoft SQL Server 資料庫，請流覽至適當的目錄，並從命令列輸入：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample2.cmd)]

新增資料庫層級基礎結構之後，我們需要將觸發程式新增至將在 SQL 快取相依性中使用的資料表。 再次使用 `aspnet_regsql.exe` 命令列程式，但使用 `-t` 參數指定資料表名稱，而不是使用 `-ed` 參數使用 `-et`，如下所示：

[!code-html[Main](using-sql-cache-dependencies-vb/samples/sample3.html)]

若要將觸發程式新增至 `authors`，並在 `ScottsServer`的 `pubs` 資料庫上 `titles` 資料表，請使用：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample4.cmd)]

在本教學課程中，請將觸發程式新增至 `Products`、`Categories`和 `Suppliers` 資料表。 我們將在步驟3中查看特定的命令列語法。

## <a name="step-2-referencing-a-microsoft-sql-server-2005-express-edition-database-inapp_data"></a>步驟2：參考`App_Data` 中的 Microsoft SQL Server 2005 Express Edition 資料庫

`aspnet_regsql.exe` 命令列程式需要資料庫和伺服器名稱，才能新增必要的輪詢基礎結構。 但是，位於 `App_Data` 資料夾中 Microsoft SQL Server 2005 Express 資料庫的資料庫和伺服器名稱是什麼？ 我發現最簡單的方法，就是將資料庫附加到 `localhost\SQLExpress` 資料庫實例，然後使用[SQL Server Management Studio](https://msdn.microsoft.com/library/ms174173.aspx)重新命名資料，而不需要探索資料庫和伺服器名稱。 如果您的電腦上已安裝其中一個完整版本的 SQL Server 2005，則您的電腦上可能已經安裝 SQL Server Management Studio。 如果您只有 Express edition，您可以下載免費的[Microsoft SQL Server Management Studio Express edition](https://www.microsoft.com/downloads/details.aspx?displaylang=en&amp;FamilyID=C243A5AE-4BD1-4E3D-94B8-5A0F62BF7796)。

從關閉 Visual Studio 開始。 接下來，開啟 SQL Server Management Studio，然後選擇使用 Windows 驗證連接到 `localhost\SQLExpress` 伺服器。

![附加至 localhost\SQLExpress 伺服器](using-sql-cache-dependencies-vb/_static/image1.gif)

**圖 1**：附加至 `localhost\SQLExpress` 伺服器

連接到伺服器之後，Management Studio 將會顯示伺服器，並有資料庫、安全性等的子資料夾。 以滑鼠右鍵按一下 [資料庫] 資料夾，然後選擇 [附加] 選項。 這會顯示 [附加資料庫] 對話方塊（請參閱 [圖 2]）。 按一下 [新增] 按鈕，然後選取 web 應用程式 `App_Data` 資料夾中的 [`NORTHWND.MDF` 資料庫] 資料夾。

[![附加 NORTHWND.MDF 檔。App_Data 資料夾中的 .MDF 資料庫](using-sql-cache-dependencies-vb/_static/image2.gif)](using-sql-cache-dependencies-vb/_static/image1.png)

**圖 2**：從 `App_Data` 資料夾附加 `NORTHWND.MDF` 資料庫（[按一下以觀看完整大小的影像](using-sql-cache-dependencies-vb/_static/image2.png)）

這會將資料庫新增至 [資料庫] 資料夾。 資料庫名稱可能是資料庫檔案的完整路徑，或是前面加上[GUID](http://en.wikipedia.org/wiki/Globally_Unique_Identifier)的完整路徑。 若要避免在使用 aspnet\_regsql 命令列工具時輸入這個冗長的資料庫名稱，請以滑鼠右鍵按一下 [剛附加的資料庫]，然後選擇 [重新命名]，將資料庫重新命名為易記名稱。 我已將資料庫重新命名為 DataTutorials。

![將附加的資料庫重新命名為更方便人易記的名稱](using-sql-cache-dependencies-vb/_static/image3.gif)

**圖 3**：將附加的資料庫重新命名為更方便人易記的名稱

## <a name="step-3-adding-the-polling-infrastructure-to-the-northwind-database"></a>步驟3：將輪詢基礎結構新增至 Northwind 資料庫

既然我們已從 `App_Data` 資料夾連接 `NORTHWND.MDF` 資料庫，我們就準備好新增輪詢基礎結構。 假設您已將資料庫重新命名為 DataTutorials，請執行下列四個命令：

[!code-console[Main](using-sql-cache-dependencies-vb/samples/sample5.cmd)]

執行這四個命令之後，以滑鼠右鍵按一下 Management Studio 中的資料庫名稱，移至 [工作] 子功能表，然後選擇 [卸離]。 然後關閉 Management Studio 並重新開啟 Visual Studio。

Visual Studio 重新開啟之後，請透過伺服器總管深入探索資料庫。 請注意，新的資料表（`AspNet_SqlCacheTablesForChangeNotification`）、新的預存程式，以及 `Products`、`Categories`和 `Suppliers` 資料表上的觸發程式。

![資料庫現在包含必要的輪詢基礎結構](using-sql-cache-dependencies-vb/_static/image4.gif)

**圖 4**：資料庫現在包含必要的輪詢基礎結構

## <a name="step-4-configuring-the-polling-service"></a>步驟4：設定輪詢服務

在資料庫中建立所需的資料表、觸發程式和預存程式之後，最後一個步驟是設定輪詢服務，這是藉由指定要使用的資料庫和輪詢頻率（以毫秒為單位），透過 `Web.config` 來完成。 下列標記會每秒輪詢 Northwind 資料庫一次。

[!code-xml[Main](using-sql-cache-dependencies-vb/samples/sample6.xml)]

`<add>` 元素（NorthwindDB）中的 `name` 值會將人類看得懂的名稱與特定資料庫產生關聯。 使用 SQL 快取相依性時，我們必須參考此處定義的資料庫名稱，以及快取資料所依據的資料表。 我們將瞭解如何使用 `SqlCacheDependency` 類別，以程式設計方式將 SQL 快取相依性與步驟6中的快取資料產生關聯。

建立 SQL 快取相依性之後，輪詢系統會每隔 `pollTime` 毫秒，連接到 `<databases>` 元素中定義的資料庫，並執行 `AspNet_SqlCachePollingStoredProcedure` 的預存程式。 這個預存程式-這是使用 `aspnet_regsql.exe` 命令列工具在步驟3中新增的：傳回 `AspNet_SqlCacheTablesForChangeNotification`中每筆記錄的 `tableName` 和 `changeId` 值。 已過期的 SQL 快取相依性會從快取中收回。

`pollTime` 設定會引進效能和資料過期之間的取捨。 小型 `pollTime` 值會增加對資料庫的要求數，但會更快速地從快取中收回過時的資料。 較大的 `pollTime` 值會減少資料庫要求的數目，但會增加後端資料變更與收回相關快取專案之間的延遲。 幸好，資料庫要求是執行簡單的預存程式，它只會從簡單的輕量資料表傳回幾個資料列。 但請使用不同的 `pollTime` 值進行實驗，以找出應用程式的資料庫存取與資料過期之間的理想平衡。 允許的最小 `pollTime` 值為500。

> [!NOTE]
> 上述範例會在 `<sqlCacheDependency>` 元素中提供單一 `pollTime` 值，但您可以選擇性地在 `<add>` 元素中指定 `pollTime` 值。 如果您已指定多個資料庫，而且想要自訂每個資料庫的輪詢頻率，這就很有用。

## <a name="step-5-declaratively-working-with-sql-cache-dependencies"></a>步驟5：以宣告方式使用 SQL 快取相依性

在步驟1到4中，我們探討了如何設定必要的資料庫基礎結構和設定輪詢系統。 有了此基礎結構之後，我們現在可以使用程式設計或宣告式技術，將專案新增至資料快取，並具有相關聯的 SQL 快取相依性。 在此步驟中，我們將探討如何以宣告方式使用 SQL 快取相依性。 在步驟6中，我們將探討程式設計方式。

[使用 objectdatasource](caching-data-with-the-objectdatasource-vb.md)教學課程來快取資料會探索 objectdatasource 的宣告式快取功能。 藉由將 [`EnableCaching`] 屬性設定為 [`True`]，並將 [`CacheDuration`] 屬性設為某個時間間隔，ObjectDataSource 會在指定的間隔內自動快取其基礎物件所傳回的資料。 ObjectDataSource 也可以使用一或多個 SQL 快取相依性。

若要以宣告方式使用 SQL 快取相依性，請開啟 [`Caching`] 資料夾中的 [`SqlCacheDependencies.aspx`] 頁面，並從 [工具箱] 將 GridView 拖曳至設計工具。 將 GridView 的 `ID` 設定為 `ProductsDeclarative` 並從其智慧標籤，選擇將其系結至名為 `ProductsDataSourceDeclarative`的新 ObjectDataSource。

[![建立名為 ProductsDataSourceDeclarative 的新 ObjectDataSource](using-sql-cache-dependencies-vb/_static/image5.gif)](using-sql-cache-dependencies-vb/_static/image3.png)

**圖 5**：建立名為 `ProductsDataSourceDeclarative` 的新 ObjectDataSource （[按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image4.png)）

設定 ObjectDataSource 使用 `ProductsBLL` 類別，並將 [選取] 索引標籤中的下拉式清單設為 `GetProducts()`。 在 [更新] 索引標籤中，選擇具有三個輸入參數的 `UpdateProduct` 多載-`productName`、`unitPrice`和 `productID`。 在 [插入] 和 [刪除] 索引標籤中，將下拉式清單設定為 [（無）]。

[![使用具有三個輸入參數的 UpdateProduct 多載](using-sql-cache-dependencies-vb/_static/image6.gif)](using-sql-cache-dependencies-vb/_static/image5.png)

**圖 6**：使用具有三個輸入參數的 UpdateProduct 多載（[按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image6.png)）

[![將 [插入] 和 [刪除] 索引標籤的下拉式清單設定為 [（無）]](using-sql-cache-dependencies-vb/_static/image7.gif)](using-sql-cache-dependencies-vb/_static/image7.png)

**圖 7**：在 [插入] 和 [刪除] 索引標籤上，將下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image8.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 將會在 GridView 中針對每個資料欄位建立 BoundFields 和 CheckBoxFields。 請移除所有欄位，但 `ProductName`、`CategoryName`和 `UnitPrice`，並視需要將這些欄位格式化。 從 GridView 的智慧標籤，勾選 [啟用分頁]、[啟用排序] 和 [啟用編輯] 核取方塊。 Visual Studio 會將 ObjectDataSource s `OldValuesParameterFormatString` 屬性設定為 `original_{0}`。 為了讓 GridView 的編輯功能能夠正常運作，請從宣告式語法完全移除此屬性，或將它設回預設值 `{0}`。

最後，將 標籤 Web 控制項加入 GridView 上方，並將其 `ID` 屬性設定為 `ODSEvents`，並將其 `EnableViewState` 屬性設為 `False` 進行這些變更之後，您的頁面宣告式標記看起來應該如下所示。 請注意，我對 GridView 欄位做了一些美觀自訂，這些都不是示範 SQL 快取相依性功能的必要專案。

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample7.aspx)]

接下來，建立 ObjectDataSource s `Selecting` 事件的事件處理常式，並在其中新增下列程式碼：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample8.vb)]

回想一下，ObjectDataSource s `Selecting` 事件只有在從其基礎物件中抓取資料時才會引發。 如果 ObjectDataSource 從本身的快取存取資料，則不會引發此事件。

現在，請透過瀏覽器造訪此頁面。 由於我們尚未執行任何快取，因此每次您分頁、排序或編輯方格時，頁面應該會顯示文字，並選取 [引發的事件]，如 [圖 8] 所示。

[![ObjectDataSource s 選取事件會在 GridView 每次進行分頁、編輯或排序時引發](using-sql-cache-dependencies-vb/_static/image8.gif)](using-sql-cache-dependencies-vb/_static/image9.png)

**圖 8**：每次 GridView 進行分頁、編輯或排序（[按一下以觀看完整大小的影像](using-sql-cache-dependencies-vb/_static/image10.png)）時，會引發 ObjectDataSource s `Selecting` 事件

如在[使用 ObjectDataSource](caching-data-with-the-objectdatasource-vb.md)快取資料教學課程中所見，將 `EnableCaching` 屬性設為 `True` 會導致 ObjectDataSource 快取其 `CacheDuration` 屬性所指定之持續時間的資料。 ObjectDataSource 也具有[`SqlCacheDependency` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sqlcachedependency.aspx)，它會使用模式，將一或多個 SQL 快取相依性新增至快取的資料：

[!code-css[Main](using-sql-cache-dependencies-vb/samples/sample9.css)]

其中*databaseName*是 `Web.config`中 `<add>` 專案的 `name` 屬性中所指定的資料庫名稱，而*tableName*則是資料庫資料表的名稱。 例如，若要建立根據 Northwind `Products` 資料表的 SQL 快取相依性無限快取資料的 ObjectDataSource，請將 ObjectDataSource s `EnableCaching` 屬性設定為 `True`，並將其 `SqlCacheDependency` 屬性設為 NorthwindDB： Products。

> [!NOTE]
> 您可以使用 SQL 快取相依性*和*以時間為基礎的到期，方法是將 `EnableCaching` 設定為 `True`、`CacheDuration` 到時間間隔，並 `SqlCacheDependency` 到資料庫和資料表名稱。 當達到以時間為基礎的到期或輪詢系統注意到基礎資料庫資料已變更（以先發生者為准）時，ObjectDataSource 會收回其資料。

`SqlCacheDependencies.aspx` 中的 GridView 會顯示兩個數據表的資料（`Products` 和 `Categories` （產品 s `CategoryName` 欄位是透過 `JOIN` 上的 `Categories`來抓取）。 因此，我們想要指定兩個 SQL 快取相依性： NorthwindDB： Products;NorthwindDB：類別目錄。

[![使用產品和類別上的 SQL 快取相依性來設定 ObjectDataSource 以支援快取](using-sql-cache-dependencies-vb/_static/image9.gif)](using-sql-cache-dependencies-vb/_static/image11.png)

**圖 9**：使用 `Products` 和 `Categories` 上的 SQL 快取相依性來設定 ObjectDataSource 以支援快取（[按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image12.png)）

設定 ObjectDataSource 以支援快取之後，請透過瀏覽器重新查看頁面。 同樣地，所引發的文字選取事件應該會出現在第一頁造訪，但分頁、排序或按一下 [編輯] 或 [取消] 按鈕時應該會消失。 這是因為將資料載入至 ObjectDataSource s 快取之後，它會保留在那裡，直到 `Products` 或 `Categories` 資料表遭到修改，或透過 GridView 更新資料為止。

分頁經過方格並注意缺少選取事件引發的文字之後，請開啟新的瀏覽器視窗，並流覽至 [編輯]、[插入] 和 [刪除] 區段（`~/EditInsertDelete/Basics.aspx`）中的 [基本概念] 教學課程。 更新產品的名稱或價格。 然後，從到第一個瀏覽器視窗，查看不同的資料頁面、排序方格，或按一下列的 [編輯] 按鈕。 此時，所引發的選取事件應該會重新出現，因為基礎資料庫資料已修改（請參閱 [圖 10]）。 如果文字未出現，請稍候片刻，然後再試一次。 請記住，輪詢服務會每隔 `pollTime` 毫秒檢查 `Products` 資料表的變更，因此在更新基礎資料和收回快取資料之間會有延遲。

[修改 Products 資料表的 ![收回快取的產品資料](using-sql-cache-dependencies-vb/_static/image10.gif)](using-sql-cache-dependencies-vb/_static/image13.png)

**圖 10**：修改 Products 資料表收回快取的產品資料（[按一下以觀看完整大小的影像](using-sql-cache-dependencies-vb/_static/image14.png)）

## <a name="step-6-programmatically-working-with-thesqlcachedependencyclass"></a>步驟6：以程式設計方式使用`SqlCacheDependency`類別

架構教學課程中的快取[資料](caching-data-in-the-architecture-vb.md)查看在架構中使用個別快取層的優點，而不是與 ObjectDataSource 緊密結合。 在該教學課程中，我們建立了 `ProductsCL` 類別來示範如何以程式設計方式使用資料快取。 若要利用快取層中的 SQL 快取相依性，請使用 [`SqlCacheDependency`] 類別。

使用輪詢系統時，`SqlCacheDependency` 物件必須與特定資料庫和資料表配對相關聯。 例如，下列程式碼會根據 Northwind 資料庫 `Products` 資料表來建立 `SqlCacheDependency` 物件：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample10.vb)]

`SqlCacheDependency` s 函式的兩個輸入參數分別是資料庫和資料表名稱。 和 ObjectDataSource 的 `SqlCacheDependency` 屬性一樣，所使用的資料庫名稱與 `Web.config`中 `<add>` 元素的 `name` 屬性所指定的值相同。 資料表名稱是資料庫資料表的實際名稱。

若要將 `SqlCacheDependency` 與新增至資料快取的專案產生關聯，請使用其中一個接受相依性的 `Insert` 方法多載。 下列程式碼會將*值*加入無限期的資料快取，但會將其與 `Products` 資料表上的 `SqlCacheDependency` 產生關聯。 簡言之，*值*會保留在快取中，直到因為記憶體限制而收回，或因為輪詢系統偵測到 `Products` 資料表在快取之後已經變更。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample11.vb)]

`ProductsCL` 類別的快取層目前會使用60秒的時間為基礎，從 `Products` 資料表快取資料。 讓 s 更新此類別，使其改用 SQL 快取相依性。 `ProductsCL` 類別 `AddCacheItem` 方法，其負責將資料新增至快取，目前包含下列程式碼：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample12.vb)]

更新此程式碼，以使用 `SqlCacheDependency` 物件，而不是 `MasterCacheKeyArray` 快取相依性：

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample13.vb)]

若要測試這種功能，請將 GridView 新增至現有 `ProductsDeclarative` GridView 底下的頁面。 將這個新的 GridView `ID` 設定為 `ProductsProgrammatic` 並透過其智慧標籤，將它系結至名為 `ProductsDataSourceProgrammatic`的新 ObjectDataSource。 設定 ObjectDataSource 使用 `ProductsCL` 類別，將 [選取和更新] 索引標籤中的下拉式清單分別設為 `GetProducts` 和 `UpdateProduct`。

[![將 ObjectDataSource 設定為使用 ProductsCL 類別](using-sql-cache-dependencies-vb/_static/image11.gif)](using-sql-cache-dependencies-vb/_static/image15.png)

**圖 11**：設定 ObjectDataSource 使用 `ProductsCL` 類別（[按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image16.png)）

[![從 [選取索引標籤 s] 下拉式清單中選取 GetProducts 方法](using-sql-cache-dependencies-vb/_static/image12.gif)](using-sql-cache-dependencies-vb/_static/image17.png)

**圖 12**：從 [選取索引標籤] 下拉式清單中選取 [`GetProducts`] 方法（[按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image18.png)）

[![從 [更新] 索引標籤下拉式清單中選擇 UpdateProduct 方法](using-sql-cache-dependencies-vb/_static/image13.gif)](using-sql-cache-dependencies-vb/_static/image19.png)

**圖 13**：從 [更新] 索引標籤下拉式清單中選擇 [UpdateProduct] 方法（[按一下以查看完整大小的影像](using-sql-cache-dependencies-vb/_static/image20.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 將會在 GridView 中針對每個資料欄位建立 BoundFields 和 CheckBoxFields。 就像在此頁面中新增的第一個 GridView 一樣，移除所有欄位，但 `ProductName`、`CategoryName`和 `UnitPrice`，並視需要將這些欄位格式化。 從 GridView 的智慧標籤，勾選 [啟用分頁]、[啟用排序] 和 [啟用編輯] 核取方塊。 如同 `ProductsDataSourceDeclarative` ObjectDataSource，Visual Studio 會將 `ProductsDataSourceProgrammatic` ObjectDataSource s `OldValuesParameterFormatString` 屬性設定為 [`original_{0}`]。 為了讓 GridView 的編輯功能能夠正常運作，請將此屬性設回 `{0}` （或從宣告式語法中移除屬性指派）。

完成這些工作之後，所產生的 GridView 和 ObjectDataSource 宣告式標記看起來應該如下所示：

[!code-aspx[Main](using-sql-cache-dependencies-vb/samples/sample14.aspx)]

若要測試快取層中的 SQL 快取相依性，請在 `ProductCL` 類別 s `AddCacheItem` 方法中設定中斷點，然後開始進行調試。 當您第一次造訪 `SqlCacheDependencies.aspx`時，應該在第一次要求資料並將其放入快取時，叫用中斷點。 接下來，移至 GridView 中的另一個頁面，或排序其中一個資料行。 這會導致 GridView 重新查詢其資料，但是資料應該會在快取中找到，因為 `Products` 資料庫資料表尚未修改。 如果在快取中找不到資料，請確定您的電腦上有足夠的記憶體可供使用，然後再試一次。

逐頁查看 GridView 的幾個頁面之後，請開啟第二個瀏覽器視窗，並流覽至 [編輯]、[插入] 和 [刪除] 區段（`~/EditInsertDelete/Basics.aspx`）中的 [基本概念] 教學課程。 從 Products 資料表更新記錄，然後從第一個瀏覽器視窗中，查看新的頁面，或按一下其中一個排序標頭。

在此案例中，您會看到兩個專案的其中一項：會叫用中斷點，表示快取的資料因為資料庫中的變更而收回;或者，將不會叫用中斷點，這表示 `SqlCacheDependencies.aspx` 現在會顯示過時的資料。 如果未叫用中斷點，很可能是因為資料已變更，所以輪詢服務尚未引發。 請記住，輪詢服務會每隔 `pollTime` 毫秒檢查 `Products` 資料表的變更，因此在更新基礎資料和收回快取資料之間會有延遲。

> [!NOTE]
> 在 `SqlCacheDependencies.aspx`中透過 GridView 編輯其中一項產品時，可能會出現此延遲。 在 [在[架構中](caching-data-in-the-architecture-vb.md)快取資料] 教學課程中，我們新增了 `MasterCacheKeyArray` 快取相依性，以確保透過 `ProductsCL` 類別 s `UpdateProduct` 方法編輯的資料會從快取中收回。 不過，在此步驟稍早修改 `AddCacheItem` 方法時，我們取代了此快取相依性，因此 `ProductsCL` 類別會繼續顯示快取的資料，直到輪詢系統注意到 `Products` 資料表的變更為止。 我們將在步驟7中瞭解如何重新引入 `MasterCacheKeyArray` 快取相依性。

## <a name="step-7-associating-multiple-dependencies-with-a-cached-item"></a>步驟7：建立多個相依性與快取專案的關聯

回想一下，`MasterCacheKeyArray` 快取相依性是用來確保*所有*與產品相關的資料在更新時都已從快取中收回。 例如，`GetProductsByCategoryID(categoryID)` 方法會針對每個唯一的*類別 id*值快取 `ProductsDataTables` 實例。 如果其中一個物件被收回，`MasterCacheKeyArray` 快取相依性可確保也會移除其他物件。 若沒有此快取相依性，當已修改快取的資料時，可能會有其他快取的產品資料已過期。 因此，在使用 SQL 快取相依性時，我們必須維護 `MasterCacheKeyArray` 快取相依性。 不過，資料快取 s `Insert` 方法只允許單一相依性物件。

此外，在使用 SQL 快取相依性時，我們可能需要將多個資料庫資料表關聯為相依性。 例如，`ProductsCL` 類別中快取的 `ProductsDataTable` 包含每個產品的類別目錄和供應商名稱，但 `AddCacheItem` 方法只會使用 `Products`上的相依性。 在此情況下，如果使用者更新類別或供應商的名稱，快取的產品資料將保留在快取中並已過期。 因此，我們只想要讓快取的產品資料相依于 `Products` 的資料表，但同時也會放在 `Categories` 和 `Suppliers` 資料表上。

[`AggregateCacheDependency` 類別](https://msdn.microsoft.com/library/system.web.caching.aggregatecachedependency.aspx)提供一個方法，讓多個相依性與快取專案產生關聯。 一開始請先建立 `AggregateCacheDependency` 實例。 接下來，使用 `AggregateCacheDependency` s `Add` 方法來新增一組相依性。 之後將專案插入資料快取時，傳入 `AggregateCacheDependency` 實例。 當*任何*`AggregateCacheDependency` 實例的相依性變更時，就會收回快取的專案。

以下顯示 `ProductsCL` 類別 `AddCacheItem` 方法的已更新程式碼。 方法會建立 `MasterCacheKeyArray` 快取相依性，以及 `Products`、`Categories`和 `Suppliers` 資料表的 `SqlCacheDependency` 物件。 這些全都結合成一個名為 `aggregateDependencies`的 `AggregateCacheDependency` 物件，然後傳遞至 `Insert` 方法。

[!code-vb[Main](using-sql-cache-dependencies-vb/samples/sample15.vb)]

測試這個新的程式碼。`Products`、`Categories`或 `Suppliers` 資料表的變更現在會使快取的資料被收回。 此外，`ProductsCL` 類別的 `UpdateProduct` 方法（透過 GridView 編輯產品時呼叫）會收回 `MasterCacheKeyArray` 快取相依性，這會導致快取的 `ProductsDataTable` 被收回，並在下一個要求中重新抓取資料。

> [!NOTE]
> SQL 快取相依性也可以與[輸出](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/caching/output.aspx)快取搭配使用。 如需這項功能的示範，請參閱：搭配[SQL Server 使用 ASP.NET 輸出](https://msdn.microsoft.com/library/e3w8402y(VS.80).aspx)快取。

## <a name="summary"></a>總結

快取資料庫資料時，資料最好會保留在快取中，直到在資料庫中修改為止。 有了 ASP.NET 2.0，您就可以在宣告式和程式設計案例中建立和使用 SQL 快取相依性。 這種方法的其中一項挑戰，就是在資料修改時進行探索。 Microsoft SQL Server 2005 的完整版本提供通知功能，可在查詢結果變更時，對應用程式發出警示。 針對 SQL Server 2005 和舊版 SQL Server 的 Express Edition，必須改為使用輪詢系統。 幸好，設定必要的輪詢基礎結構相當簡單。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [使用 Microsoft SQL Server 2005 中的查詢通知](https://msdn.microsoft.com/library/ms175110.aspx)
- [建立查詢通知](https://msdn.microsoft.com/library/ms188669.aspx)
- [在 ASP.NET 中使用 `SqlCacheDependency` 類別進行快取](https://msdn.microsoft.com/library/ms178604(VS.80).aspx)
- [ASP.NET SQL Server 註冊工具（`aspnet_regsql.exe`）](https://msdn.microsoft.com/library/ms229862(vs.80).aspx)
- [`SqlCacheDependency` 總覽](http://www.aspnetresources.com/blog/sql_cache_depedency_overview.aspx)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Marko Rangel、Teresa Murphy 和 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](caching-data-at-application-startup-vb.md)
