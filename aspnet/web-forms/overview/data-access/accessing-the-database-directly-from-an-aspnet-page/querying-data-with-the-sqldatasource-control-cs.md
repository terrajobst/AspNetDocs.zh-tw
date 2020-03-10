---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
title: 使用 SqlDataSource 控制項查詢資料（C#） |Microsoft Docs
author: rick-anderson
description: 在先前的教學課程中，我們使用了 ObjectDataSource 控制項，將展示層與資料存取層完全分開。 從這個輔導開始 。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: 60512d6a-b572-4b7a-beb3-3e44b4d2020c
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/querying-data-with-the-sqldatasource-control-cs
msc.type: authoredcontent
ms.openlocfilehash: 5bda42965f7d1db71b207c0b76e251b8fff64e31
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78626424"
---
# <a name="querying-data-with-the-sqldatasource-control-c"></a>使用 SqlDataSource 控制項查詢資料 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_47_CS.exe)或[下載 PDF](querying-data-with-the-sqldatasource-control-cs/_static/datatutorial47cs1.pdf)

> 在先前的教學課程中，我們使用了 ObjectDataSource 控制項，將展示層與資料存取層完全分開。 從本教學課程開始，我們將瞭解如何將 SqlDataSource 控制項用於不需要嚴格區分簡報和資料存取的簡單應用程式。

## <a name="introduction"></a>簡介

目前為止我們檢查過的所有教學課程都使用了一套分層式架構，其中包含了簡報、商務邏輯和資料存取層。 資料存取層（DAL）是在第一個教學課程（[建立資料存取層](../introduction/creating-a-data-access-layer-cs.md)）和第二個商務邏輯層（[建立商務邏輯層](../introduction/creating-a-business-logic-layer-cs.md)）中製作的。 從使用[ObjectDataSource 顯示資料](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教學課程開始，我們已瞭解如何使用 ASP.NET 2.0 s new ObjectDataSource 控制項，以宣告方式與展示層中的架構進行介面。

雖然到目前為止的所有教學課程都已使用架構來處理資料，但也可以直接從 ASP.NET 網頁存取、插入、更新和刪除資料庫資料，略過架構。 這麼做會將特定的資料庫查詢和商務邏輯直接放置在網頁中。 對於大型或複雜的應用程式，設計、執行和使用階層式架構，對於應用程式的成功、可更新性和可維護性而言極為重要。 不過，在建立非常簡單的一次性應用程式時，可能不需要開發健全的架構。

ASP.NET 2.0 提供五個內建的資料來源控制項[SqlDataSource](https://msdn.microsoft.com/library/dz12d98w%28vs.80%29.aspx)、 [AccessDataSource](https://msdn.microsoft.com/library/8e5545e1.aspx)、 [ObjectDataSource](https://msdn.microsoft.com/library/9a4kyhcx.aspx)、 [XmlDataSource](https://msdn.microsoft.com/library/e8d8587a%28en-US,VS.80%29.aspx)和[SiteMapDataSource](https://msdn.microsoft.com/library/5ex9t96x%28en-US,VS.80%29.aspx)。 SqlDataSource 可以用來直接從關係資料庫存取和修改資料，包括 Microsoft SQL Server、Microsoft Access、Oracle、MySQL 等。 在本教學課程和接下來的三個中，我們將探討如何使用 SqlDataSource 控制項、探索如何查詢和篩選資料庫資料，以及如何使用 SqlDataSource 來插入、更新和刪除資料。

![ASP.NET 2.0 包含五個內建的資料來源控制項](querying-data-with-the-sqldatasource-control-cs/_static/image1.gif)

**圖 1**： ASP.NET 2.0 包含五個內建的資料來源控制項

## <a name="comparing-the-objectdatasource-and-sqldatasource"></a>比較 ObjectDataSource 和 SqlDataSource

就概念而言，ObjectDataSource 和 SqlDataSource 控制項只是資料的 proxy。 如[使用 ObjectDataSource 顯示資料](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教學課程中所述，ObjectDataSource 的屬性會指出提供資料的物件類型，以及要叫用的方法，以便選取、插入、更新及刪除基礎物件類型中的資料。 一旦設定了 ObjectDataSource 的屬性，就可以使用 ObjectDataSource s `Select()`、`Insert()`、`Delete()`和 `Update()` 方法，將資料 Web 控制項（例如 GridView、DetailsView 或 DataList）系結至控制項，以與基礎結構互動。

SqlDataSource 會提供相同的功能，但會對關係資料庫（而非物件程式庫）進行操作。 在 SqlDataSource 中，我們必須指定資料庫連接字串，以及要執行以插入、更新、刪除和抓取資料的臨機操作 SQL 查詢或預存程式。 SqlDataSource s `Select()`、`Insert()`、`Update()`和 `Delete()` 方法在叫用時，會連接到指定的資料庫，併發出適當的 SQL 查詢。 如下圖所示，這些方法會執行連接至資料庫、發出查詢和傳回結果的 grunt 工作。

![SqlDataSource 可做為資料庫的 Proxy](querying-data-with-the-sqldatasource-control-cs/_static/image2.gif)

**圖 2**： SqlDataSource 做為資料庫的 Proxy

> [!NOTE]
> 在本教學課程中，我們將焦點放在從資料庫中抓取資料。 在[使用 SqlDataSource 控制項來插入、更新和刪除資料](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)教學課程中，我們將瞭解如何設定 SqlDataSource 以支援插入、更新和刪除。

## <a name="the-sqldatasource-and-accessdatasource-controls"></a>SqlDataSource 和 AccessDataSource 控制項

除了 SqlDataSource 控制項以外，ASP.NET 2.0 也包含 AccessDataSource 控制項。 這兩個不同的控制項領導許多開發人員 ASP.NET 2.0，懷疑 AccessDataSource 控制項的設計是要專門與 Microsoft Access 搭配使用，其 SqlDataSource 控制項專門用於 Microsoft SQL Server。 雖然 AccessDataSource 是專為使用 Microsoft Access 而設計，但 SqlDataSource 控制項適用于可透過 .NET 存取的*任何*關係資料庫。 這包括任何 OleDb 或 ODBC 相容的資料存放區，例如 Microsoft SQL Server、Microsoft Access、Oracle、Informix、MySQL 及于 postgresql 等等。

AccessDataSource 和 SqlDataSource 控制項的唯一差異在於資料庫連接資訊的指定方式。 AccessDataSource 控制項只需要 Access 資料庫檔案的檔案路徑。 另一方面，SqlDataSource 需要完整的連接字串。

## <a name="step-1-creating-the-sqldatasource-web-pages"></a>步驟1：建立 SqlDataSource 網頁

在我們開始探索如何使用 SqlDataSource 控制項直接處理資料庫資料之前，先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在本教學課程和接下來的三篇中提供。 從新增名為 `SqlDataSource`的資料夾開始。 接下來，將下列 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `Querying.aspx`
- `ParameterizedQueries.aspx`
- `InsertUpdateDelete.aspx`
- `OptimisticConcurrency.aspx`

![新增 SqlDataSource 相關教學課程的 ASP.NET 網頁](querying-data-with-the-sqldatasource-control-cs/_static/image3.gif)

**圖 3**：新增 SqlDataSource 相關教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`SqlDataSource`] 資料夾中的 `Default.aspx` 會在其區段中列出教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 因此，請將這個使用者控制項加入至 `Default.aspx`，方法是將它從方案總管拖曳至頁面 s 設計檢視。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](querying-data-with-the-sqldatasource-control-cs/_static/image5.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image4.gif)

**圖 4**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](querying-data-with-the-sqldatasource-control-cs/_static/image6.gif)）

最後，將這四個頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，在將自訂按鈕新增至 DataList 和中繼器 `<siteMapNode>`之後，新增下列標記：

[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample1.sql)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含用於編輯、插入及刪除教學課程的專案。

![網站地圖現在包含 SqlDataSource 教學課程的專案](querying-data-with-the-sqldatasource-control-cs/_static/image7.gif)

[**圖 5**]：網站地圖現在包含 SqlDataSource 教學課程的專案

## <a name="step-2-adding-and-configuring-the-sqldatasource-control"></a>步驟2：新增和設定 SqlDataSource 控制項

一開始先開啟 [`SqlDataSource`] 資料夾中的 [`Querying.aspx`] 頁面，然後切換至 [設計檢視]。 將 [SqlDataSource] 控制項從 [工具箱] 拖曳至設計工具，並將其 `ID` 設定為 [`ProductsDataSource`]。 就像 ObjectDataSource 一樣，SqlDataSource 不會產生任何轉譯的輸出，因此在設計介面上會顯示為灰色方塊。 若要設定 SqlDataSource，請按一下 SqlDataSource s 智慧標籤中的 [設定資料來源] 連結。

![按一下 SqlDataSource s 智慧標籤中的 [設定資料來源] 連結](querying-data-with-the-sqldatasource-control-cs/_static/image8.gif)

**圖 6**：按一下 SqlDataSource s 智慧標籤的 [設定資料來源] 連結

這會顯示 [SqlDataSource 控制項] [設定資料來源]。 雖然 wizard 的步驟與 ObjectDataSource 控制項不同，但最終目標與提供如何透過資料來源抓取、插入、更新及刪除資料的詳細資訊相同。 針對 SqlDataSource，這牽涉到指定要使用的基礎資料庫，並提供臨機操作 SQL 語句或預存程式。

第一個 wizard 步驟會提示我們輸入資料庫。 下拉式清單中會包含在 web 應用程式 `App_Data` 資料夾中找到的資料庫，以及已加入伺服器總管中 [資料連線] 節點的資料庫。 因為我們已經將 `App_Data` 資料夾中 `NORTHWIND.MDF` 資料庫的連接字串加入到專案的 `Web.config` 檔案中，所以下拉式清單會包含該連接字串的參考，`NORTHWINDConnectionString`。 從下拉式清單中選擇此專案，然後按 [下一步]。

![從下拉式清單中選擇 [NORTHWINDConnectionString]](querying-data-with-the-sqldatasource-control-cs/_static/image9.gif)

**圖 7**：從下拉式清單中選擇 [`NORTHWINDConnectionString`]

選擇資料庫之後，嚮導會要求查詢傳回資料。 我們可以指定要傳回之資料表或視圖的資料行，也可以輸入自訂 SQL 語句或指定預存程式。 您可以透過 [指定自訂 SQL 語句或預存程式]，並從 [資料表] 或 [視圖] 選項按鈕指定資料行，在此選項之間切換。

> [!NOTE]
> 在第一個範例中，讓我們使用 [從資料表或視圖指定資料行] 選項。 我們稍後會在本教學課程中返回嚮導，並探索 [指定自訂 SQL 語句或預存程式] 選項。

[圖 8] 顯示選取了 [從資料表或視圖指定資料行] 選項按鈕時的 [設定 Select 語句] 畫面。 下拉式清單包含 Northwind 資料庫中的一組資料表和 views，並在下面的核取方塊清單中顯示選取的資料表或 view s 資料行。 在此範例中，讓 s 從 `Products` 資料表傳回 `ProductID`、`ProductName`和 `UnitPrice` 資料行。 如 [圖 8] 所示，在進行這些選擇之後，嚮導會顯示所產生的 SQL 語句 `SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`。

![從 Products 資料表傳回資料](querying-data-with-the-sqldatasource-control-cs/_static/image10.gif)

**圖 8**：從 `Products` 資料表傳回資料

當您設定 wizard 從 `Products` 資料表傳回 `ProductID`、`ProductName`和 `UnitPrice` 資料行之後，請按 [下一步] 按鈕。 最後一個畫面可讓您檢查上一個步驟所設定之查詢的結果。 按一下 [測試查詢] 按鈕會執行已設定的 `SELECT` 語句，並在方格中顯示結果。

![按一下 [測試查詢] 按鈕，以檢查您的 SELECT 查詢](querying-data-with-the-sqldatasource-control-cs/_static/image11.gif)

**圖 9**：按一下 [測試查詢] 按鈕，以檢查您的 `SELECT` 查詢

若要完成精靈，請按一下 [完成]。

和 ObjectDataSource 一樣，SqlDataSource s wizard 只會將值指派給控制項的屬性，亦即[`ConnectionString`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.connectionstring.aspx)和[`SelectCommand`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.selectcommand.aspx)屬性。 完成 wizard 之後，您的 SqlDataSource 控制項的宣告式標記看起來應該如下所示：

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample2.aspx)]

`ConnectionString` 屬性提供如何連接到資料庫的相關資訊。 這個屬性可以指派為完整的硬式編碼連接字串值，或可指向 `Web.config`中的連接字串。 若要參考 Web.config 中的連接字串值，請使用 `<%$ expressionPrefix:expressionValue %>`的語法。 一般來說， *expressionPrefix*是 ConnectionStrings，而*expressionValue*是 `Web.config` [`<connectionStrings>` 區段](https://msdn.microsoft.com/library/bf7sd233.aspx)中的連接字串名稱。 不過，語法可以用來參考資源檔中 `<appSettings>` 元素或內容。 如需此語法的詳細資訊，請參閱[ASP.NET 運算式總覽](https://msdn.microsoft.com/library/d5bd1tad.aspx)。

`SelectCommand` 屬性會指定要執行的臨機操作 SQL 語句或預存程式，以傳回資料。

## <a name="step-3-adding-a-data-web-control-and-binding-it-to-the-sqldatasource"></a>步驟3：加入資料 Web 控制項並將它系結至 SqlDataSource

一旦設定 SqlDataSource 之後，就可以系結至資料 Web 控制項，例如 GridView 或 DetailsView。 在本教學課程中，我們會在 GridView 中顯示資料。 從 [工具箱] 將 GridView 拖曳至頁面上，然後從 [GridView] 智慧標籤的下拉式清單中選擇資料來源，將它系結至 [`ProductsDataSource` SqlDataSource]。

[![加入 GridView 並將它系結至 SqlDataSource 控制項](querying-data-with-the-sqldatasource-control-cs/_static/image13.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image12.gif)

**圖 10**：加入 GridView 並將它系結至 SqlDataSource 控制項（[按一下以查看完整大小的影像](querying-data-with-the-sqldatasource-control-cs/_static/image14.gif)）

當您從 GridView 的智慧標籤的下拉式清單中選取 SqlDataSource 控制項之後，Visual Studio 將會針對資料來源控制項所傳回的每個資料行，自動加入 GridView 的 BoundField 或 CheckBoxField。 由於 SqlDataSource 會傳回三個資料庫資料行 `ProductID`、`ProductName`和 `UnitPrice` GridView 中有三個欄位。

請花點時間設定 GridView 的三 BoundFields。 將 [`ProductName`] 欄位 `HeaderText` 屬性變更為 [產品名稱]，並將 [`UnitPrice`] 欄位變更為 [價格]。 同時將 `UnitPrice` 欄位格式化為貨幣。 進行這些修改之後，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample3.aspx)]

透過瀏覽器造訪此頁面。 如 [圖 11] 所示，GridView 會列出每個產品的 `ProductID`、`ProductName`和 `UnitPrice` 值。

[![GridView 會顯示每個產品的 ProductID、ProductName 和單價值](querying-data-with-the-sqldatasource-control-cs/_static/image16.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image15.gif)

**圖 11**： GridView 會顯示每個產品的 `ProductID`、`ProductName`和 `UnitPrice` 值（[按一下以查看完整大小的影像](querying-data-with-the-sqldatasource-control-cs/_static/image17.gif)）

流覽頁面時，GridView 會叫用它的資料來源控制項 `Select()` 方法。 當我們使用 ObjectDataSource 控制項時，這稱為 `ProductsBLL` 類別 s `GetProducts()` 方法。 不過，使用 SqlDataSource 時，`Select()` 方法會建立與指定之資料庫的連接，併發出 `SelectCommand` （在此範例中為`SELECT [ProductID], [ProductName], [UnitPrice] FROM [Products]`）。 此 SqlDataSource 會傳回它的結果，接著 GridView 會列舉，並在 GridView 中針對每個傳回的資料庫記錄建立一個資料列。

## <a name="the-built-in-data-web-control-features-and-the-sqldatasource-control"></a>內建的資料 Web 控制項功能和 SqlDataSource 控制項

一般而言，資料 Web 控制項分頁、排序、編輯、刪除、插入等功能，都是資料 Web 控制項特有的，而且不會相依于所使用的資料來源控制項。 也就是說，GridView 可以利用內建的分頁、排序、編輯和刪除它是否系結至 ObjectDataSource 或 SqlDataSource。 不過，某些資料 Web 控制項功能對所使用的資料來源控制項或資料來源控制設定而言是敏感的。

例如，在[有效率地逐一查看大量資料的](../paging-and-sorting/efficiently-paging-through-large-amounts-of-data-cs.md)教學課程中，我們討論了資料 Web 控制項輕鬆自在管理的分頁邏輯如何傳回基礎資料來源中的*所有*記錄，然後根據目前的頁面索引和每頁要顯示的記錄數目，只顯示適當的記錄子集。 當分頁通過夠大的結果集時，此模型的效率非常低。 幸好，可以將 ObjectDataSource 設定為支援自訂分頁，這只會傳回要顯示的精確記錄子集。 不過，SqlDataSource 控制項缺少用來執行自訂分頁的屬性。

具有分頁和排序的另一個奧妙會出現在 SqlDataSource 中。 根據預設，從 SqlDataSource 傳回的資料可以透過 GridView 分頁或進行排序。 若要示範這一點，請檢查 `Querying.aspx` 中 GridView s 智慧標籤的 [啟用分頁] 和 [啟用排序] 選項，並確認此功能如預期般運作。

排序和分頁會運作，因為 SqlDataSource 會將資料庫資料捕獲到鬆散類型的資料集。 查詢所傳回的記錄總數是執行分頁的重要層面，可以從資料集確認。 此外，資料集的結果可以透過 DataView 排序。 當 GridView 要求分頁或已排序的資料時，SqlDataSource 會自動使用這些功能。

SqlDataSource 可以設定為傳回 DataReader，而不是資料集，方法是將其[`DataSourceMode` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.datasourcemode.aspx)從 `DataSet` （預設值）變更為 `DataReader`。 將 SqlDataSource 的結果傳遞至預期 DataReader 的現有程式碼時，可能會偏好使用 DataReader。 此外，由於 Datareader 是比資料集更簡單的物件，因此它們會提供較佳的效能。 不過，如果您進行這項變更，資料 Web 控制項就不能進行排序或分頁，因為 SqlDataSource 無法確定查詢傳回多少筆記錄，而且 DataReader 是否提供任何方法來排序傳回的資料。

## <a name="step-4-using-a-custom-sql-statement-or-stored-procedure"></a>步驟4：使用自訂 SQL 語句或預存程式

設定 SqlDataSource 控制項時，用來傳回資料的查詢可以用兩種方法之一來指定，做為自訂 SQL 語句或預存程式，或當做現有資料表或視圖的資料行。 在步驟2中，我們已檢查從 `Products` 資料表中選取資料行。 讓我們看看如何使用自訂的 SQL 語句。

將另一個 GridView 控制項加入至 [`Querying.aspx`] 頁面，然後從智慧標籤的下拉式清單中選擇建立新的資料來源。 接下來，指出將從資料庫提取資料，這將會建立新的 SqlDataSource 控制項。 將控制項命名為 `ProductsWithCategoryInfoDataSource`。

![建立名為 ProductsWithCategoryInfoDataSource 的新 SqlDataSource 控制項](querying-data-with-the-sqldatasource-control-cs/_static/image18.gif)

**圖 12**：建立名為 `ProductsWithCategoryInfoDataSource` 的新 SqlDataSource 控制項

下一個畫面會要求我們指定資料庫。 如 [圖 7] 所示，從下拉式清單中選取 [`NORTHWINDConnectionString`]，然後按 [下一步]。 在 [設定 Select 語句] 畫面中，選擇 [指定自訂 SQL 語句或預存程式] 選項按鈕，然後按 [下一步]。 這會顯示 [定義自訂語句] 或 [預存程式] 畫面，其中提供標示為 SELECT、UPDATE、INSERT 和 DELETE 的索引標籤。 在每個索引標籤中，您可以在文字方塊中輸入自訂的 SQL 語句，或從下拉式清單中選擇一個預存程式。 在本教學課程中，我們將探討如何輸入自訂的 SQL 語句;下一個教學課程包含使用預存程式的範例。

![輸入自訂 SQL 語句或挑選預存程式](querying-data-with-the-sqldatasource-control-cs/_static/image19.gif)

**圖 13**：輸入自訂 SQL 語句或挑選預存程式

您可以將自訂 SQL 語句手動輸入文字方塊中，或按一下 [查詢產生器] 按鈕以圖形方式來建立。 從 [查詢產生器] 或 [] 文字方塊中，使用下列查詢來傳回來自 `Products` 資料表的 `ProductID` 和 `ProductName` 欄位，方法是使用 `JOIN` 從 `CategoryName` 資料表中取出 product s `Categories`：

[!code-sql[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample4.sql)]

![您可以使用查詢產生器，以圖形方式建立查詢](querying-data-with-the-sqldatasource-control-cs/_static/image20.gif)

**圖 14**：您可以使用查詢產生器以圖形方式建立查詢

指定查詢之後，請按 [下一步] 繼續前往 [測試查詢] 畫面。 按一下 [完成] 以完成 SqlDataSource wizard。

完成 wizard 之後，GridView 會加入三個 BoundFields，其中顯示查詢所傳回的 `ProductID`、`ProductName`和 `CategoryName` 資料行，並產生下列宣告式標記：

[!code-aspx[Main](querying-data-with-the-sqldatasource-control-cs/samples/sample5.aspx)]

[![GridView 會顯示每個產品的識別碼、名稱和相關聯的類別名稱](querying-data-with-the-sqldatasource-control-cs/_static/image22.gif)](querying-data-with-the-sqldatasource-control-cs/_static/image21.gif)

**圖 15**： GridView 會顯示每個產品的識別碼、名稱和相關聯的類別名稱（[按一下以查看完整大小的影像](querying-data-with-the-sqldatasource-control-cs/_static/image23.gif)）

## <a name="summary"></a>總結

在本教學課程中，我們已瞭解如何使用 SqlDataSource 控制項來查詢和顯示資料。 就像 ObjectDataSource 一樣，SqlDataSource 會當做 proxy，提供存取資料的宣告式方法。 其屬性會指定要連接的資料庫，以及要執行的 SQL `SELECT` 查詢;您可以透過屬性視窗或使用 [設定資料來源] wizard 來指定它們。

我們在本教學課程中檢查的 `SELECT` 查詢範例會從指定的查詢傳回所有記錄。 不過，SqlDataSource 控制項可以包含具有參數的 `WHERE` 子句，其值是以程式設計方式指派，或從指定的來源自動提取。 在下一個教學課程中，我們將探討如何建立及使用參數化查詢！

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [存取關係資料庫資料](http://aspnet.4guysfromrolla.com/articles/022206-1.aspx)
- [SqlDataSource 控制項總覽](https://msdn.microsoft.com/library/dz12d98w.aspx)
- [ASP.NET 快速入門教學課程： SqlDataSource 控制項](https://quickstarts.asp.net/QuickStartv20/aspnet/doc/ctrlref/data/sqldatasource.aspx)
- [Web.config `<connectionStrings>` 元素](https://msdn.microsoft.com/library/bf7sd233.aspx)
- [資料庫連接字串參考](http://www.connectionstrings.com/)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Susan Connery、Bernadette Leigh 和 David Suru。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一個](using-parameterized-queries-with-the-sqldatasource-cs.md)
