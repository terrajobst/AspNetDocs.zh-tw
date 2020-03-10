---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-cs
title: 使用計算資料行（C#） |Microsoft Docs
author: rick-anderson
description: 建立資料庫資料表時，Microsoft SQL Server 可讓您定義計算資料行，其值是從通常 referen 的運算式計算而來。
ms.author: riande
ms.date: 08/03/2007
ms.assetid: 57459065-ed7c-4dfe-ac9c-54c093abc261
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/working-with-computed-columns-cs
msc.type: authoredcontent
ms.openlocfilehash: ad6a96f2721510c2478f707c8eed018ae797f27a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78531791"
---
# <a name="working-with-computed-columns-c"></a>使用計算資料行 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_71_CS.zip)或[下載 PDF](working-with-computed-columns-cs/_static/datatutorial71cs1.pdf)

> 建立資料庫資料表時，Microsoft SQL Server 可讓您定義計算資料行，其值是從通常參考相同資料庫記錄中其他值的運算式計算而來。 這類值在資料庫中是唯讀的，這在使用 Tableadapter 時需要特殊的考慮。 在本教學課程中，我們將學習如何滿足計算資料行所帶來的挑戰。

## <a name="introduction"></a>簡介

Microsoft SQL Server 允許 *[計算資料行](https://msdn.microsoft.com/library/ms191250.aspx)* ，這是其值是從運算式計算而來，且通常會從相同資料表中的其他資料行參考值的資料行。 例如，時間追蹤資料模型可能會有一個名為 `ServiceLog` 的資料表，其中包含資料行，包括 `ServicePerformed`、`EmployeeID`、`Rate`和 `Duration`等等。 雖然可以透過網頁或其他程式設計介面來計算每個服務專案的應付金額（速率乘以持續時間），但在報告這項資訊的 `ServiceLog` `AmountDue` 資料表中包含資料行，可能會很方便。 此資料行可以建立為一般資料行，但每當 `Rate` 或 `Duration` 資料行值變更時，都必須更新。 較好的方法是使用運算式 `Rate * Duration`，讓 `AmountDue` 資料行成為計算資料行。 這麼做會導致 SQL Server 在查詢中參考 `AmountDue` 的資料行值時，自動計算該值。

由於計算資料行的值是由運算式決定，因此這類資料行是唯讀的，因此不能在 `INSERT` 或 `UPDATE` 語句中指派值給它們。 不過，當計算資料行屬於使用臨機操作 SQL 語句之 TableAdapter 的主要查詢時，它們會自動包含在自動產生的 `INSERT` 和 `UPDATE` 語句中。 因此，必須更新 TableAdapter s `INSERT` 和 `UPDATE` 查詢和 `InsertCommand` 和 `UpdateCommand` 屬性，才能移除任何計算資料行的參考。

使用計算資料行搭配使用臨機操作 SQL 語句的 TableAdapter 的一項挑戰，就是在完成 TableAdapter 設定向導時，會自動重新產生 TableAdapter s `INSERT` 和 `UPDATE` 查詢。 因此，手動從 `INSERT` 中移除的計算資料行，如果重新執行此嚮導，`UPDATE` 查詢就會再次出現。 雖然使用預存程式的 Tableadapter 不會受到此肯定脆弱度的影響，但它們在步驟3中會有自己的疑慮。

在本教學課程中，我們將在 Northwind 資料庫的 `Suppliers` 資料表中加入一個計算資料行，然後建立對應的 TableAdapter 來處理這個資料表及其計算資料行。 我們會將 TableAdapter 使用預存程式，而不是臨機操作 SQL 語句，因此在使用 TableAdapter 設定向導時，不會遺失我們的自訂專案。

讓我們開始吧！

## <a name="step-1-adding-a-computed-column-to-thesupplierstable"></a>步驟1：將計算資料行加入至`Suppliers`資料表

Northwind 資料庫沒有任何計算資料行，因此我們需要自己加入一個。 在本教學課程中，我們會將計算的資料行新增至稱為 `FullContactName` 的 `Suppliers` 資料表，以傳回連絡人的名稱、標題和其工作的公司，格式如下： `ContactName` （`ContactTitle`，`CompanyName`）。 當顯示供應商的相關資訊時，可能會在報表中使用這個計算資料行。

一開始先開啟 `Suppliers` 資料表定義，方法是以滑鼠右鍵按一下 伺服器總管中的 `Suppliers` 資料表，然後從內容功能表中選擇 開啟資料表定義。 這會顯示資料表及其屬性的資料行，例如其資料類型、是否允許 `NULL` s 等等。 若要加入計算資料行，請先在資料表定義中輸入資料行的名稱。 接下來，在資料行屬性視窗的 [計算資料行規格] 區段下，將其運算式輸入 [（公式）] 文字方塊中（請參閱 [圖 1]）。 將計算資料行命名為 `FullContactName` 並使用下列運算式：

[!code-sql[Main](working-with-computed-columns-cs/samples/sample1.sql)]

請注意，您可以使用 `+` 運算子，在 SQL 中串連字號串。 `CASE` 語句可以如同傳統程式設計語言中的條件來使用。 在上述運算式中，可以將 `CASE` 語句視為：如果 `ContactTitle` 不 `NULL`，則會輸出以逗號串連的 `ContactTitle` 值，否則不發出任何內容。 如需 `CASE` 語句之實用性的詳細資訊，請參閱[SQL `CASE` 語句的強大功能](http://www.4guysfromrolla.com/webtech/102704-1.shtml)。

> [!NOTE]
> 我們不會在這裡使用 `CASE` 語句，而是也可以使用 `ISNULL(ContactTitle, '')`。 [`ISNULL(checkExpression, replacementValue)`](https://msdn.microsoft.com/library/ms184325.aspx)會傳回非 Null 的*checkExpression* ，否則會傳回*replacementValue*。 雖然 `ISNULL` 或 `CASE` 會在此實例中工作，但有更複雜的情況，也就是 `ISNULL`無法比對 `CASE` 語句的彈性。

加入這個計算資料行之後，您的畫面看起來應該像 [圖 1] 中的螢幕擷取畫面。

[![將名為 FullContactName 的計算資料行新增至供應商資料表](working-with-computed-columns-cs/_static/image2.png)](working-with-computed-columns-cs/_static/image1.png)

**圖 1**：將名為 `FullContactName` 的計算資料行加入至 `Suppliers` 資料表（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image3.png)）

在命名計算資料行並輸入其運算式之後，請按一下工具列中的 [儲存] 圖示、按下 Ctrl + S，或前往 [檔案] 功能表，然後選擇 [儲存 `Suppliers`]，將變更儲存至資料表。

儲存資料表應該會重新整理伺服器總管，包括 `Suppliers` 資料表 s 資料行清單中剛加入的資料行。 此外，在 [（公式）] 文字方塊中輸入的運算式會自動調整為對等的運算式，以去除不必要的空白字元、將資料行名稱括在方括弧（`[]`），並包含括弧以更明確地顯示作業順序：

[!code-sql[Main](working-with-computed-columns-cs/samples/sample2.sql)]

如需 Microsoft SQL Server 中計算資料行的詳細資訊，請參閱[技術檔](https://msdn.microsoft.com/library/ms191250.aspx)。 另請參閱[如何：指定計算資料行](https://msdn.microsoft.com/library/ms188300.aspx)，以取得建立計算資料行的逐步解說。

> [!NOTE]
> 根據預設，計算資料行不會實際儲存在資料表中，而是在每次查詢中參考它們時重新計算。 不過，藉由勾選 [已保存] 核取方塊，您可以指示 SQL Server 實際將計算資料行儲存在資料表中。 這麼做可讓您在計算資料行上建立索引，這樣可以改善在其 `WHERE` 子句中使用計算資料行值之查詢的效能。 如需詳細資訊，請參閱[在計算資料行上建立索引](https://msdn.microsoft.com/library/ms189292.aspx)。

## <a name="step-2-viewing-the-computed-column-s-values"></a>步驟2：查看計算資料行的值

開始處理資料存取層之前，讓我們花一分鐘的時間來查看 `FullContactName` 的值。 從 伺服器總管中，以滑鼠右鍵按一下 `Suppliers` 資料表名稱，然後從內容功能表中選擇 新增查詢。 這會顯示一個查詢視窗，提示我們選擇要包含在查詢中的資料表。 新增 `Suppliers` 資料表，然後按一下 [關閉]。 接下來，檢查 [供應商] 資料表中的 `CompanyName`、`ContactName`、`ContactTitle`和 `FullContactName` 資料行。 最後，按一下工具列中的紅色驚嘆號圖示，以執行查詢並查看結果。

如 [圖 2] 所示，結果中會包含 `FullContactName`，其中列出使用「技術」格式的 `CompanyName`、`ContactName`和 `ContactTitle` 資料行。`ContactName` （`ContactTitle`，`CompanyName`）。

[![FullContactName 使用 [連絡人] 格式（ContactTitle，公司名稱）](working-with-computed-columns-cs/_static/image5.png)](working-with-computed-columns-cs/_static/image4.png)

**圖 2**： `FullContactName` 使用格式 `ContactName` （`ContactTitle`，`CompanyName`）（[按一下以觀看完整大小的影像](working-with-computed-columns-cs/_static/image6.png)）

## <a name="step-3-adding-thesupplierstableadapterto-the-data-access-layer"></a>步驟3：將`SuppliersTableAdapter`新增至資料存取層

為了在我們的應用程式中使用供應商資訊，我們必須先在 DAL 中建立 TableAdapter 和 DataTable。 在理想的情況下，您可以使用先前教學課程中所檢查的相同直接步驟來完成這項作業。 不過，使用計算資料行引進了一些 wrinkles，可提供討論。

如果您使用的 TableAdapter 使用臨機操作 SQL 語句，您可以透過 [TableAdapter 設定向導]，直接在 TableAdapter s 查詢中包含計算資料行。 不過，這會自動產生包含計算資料行的 `INSERT` 和 `UPDATE` 語句。 如果您嘗試執行其中一種方法，就無法修改具有訊息的資料行*ColumnName*的 `SqlException`，因為它是計算資料行，或是會擲回 UNION 運算子的結果。 雖然 `INSERT` 和 `UPDATE` 語句可以透過 TableAdapter s `InsertCommand` 和 `UpdateCommand` 屬性來手動調整，但是每當重新執行 TableAdapter 設定向導時，這些自訂都會遺失。

由於使用臨機操作 SQL 語句的 Tableadapter 肯定脆弱度，因此建議在使用計算資料行時使用預存程式。 如果您使用現有的預存程式，只要[針對具類型的資料集 tableadapter 教學課程使用現有的預存程式來](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-cs.md)設定 TableAdapter 即可。 不過，如果您有 TableAdapter wizard 為您建立預存程式，則一開始請先從主查詢中省略任何計算資料行，這是很重要的。 如果您在主要查詢中包含計算資料行，TableAdapter 設定 wizard 會在完成時通知您，它無法建立對應的預存程式。 簡言之，我們必須一開始使用計算資料行免費的主要查詢來設定 TableAdapter，然後手動更新對應的預存程式和 TableAdapter `SelectCommand` 以包含計算資料行。 此方法類似于將[TableAdapter 更新為使用](updating-the-tableadapter-to-use-joins-cs.md)`JOIN`*s*教學課程中所使用的方法。

在本教學課程中，讓我們新增新的 TableAdapter，並讓它自動為我們建立預存程式。 因此，我們必須一開始就從主查詢中省略 `FullContactName` 計算資料行。

從開啟 `~/App_Code/DAL` 資料夾中的 `NorthwindWithSprocs` 資料集開始。 在設計工具中按一下滑鼠右鍵，然後從內容功能表中，加入宣告新的 TableAdapter。 這會啟動 [TableAdapter 設定向導]。 指定要從中查詢資料的資料庫（從 `Web.config``NORTHWNDConnectionString`），然後按 [下一步]。 由於我們尚未建立任何用來查詢或修改 `Suppliers` 資料表的預存程式，因此請選取 [建立新的預存程式] 選項，讓 wizard 為我們建立，然後按 [下一步]。

[![選擇 [建立新的預存程式] 選項](working-with-computed-columns-cs/_static/image8.png)](working-with-computed-columns-cs/_static/image7.png)

**圖 3**：選擇 [建立新的預存程式] 選項（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image9.png)）

後續步驟會提示我們進行主查詢。 輸入下列查詢，以傳回每個供應商的 `SupplierID`、`CompanyName`、`ContactName`和 `ContactTitle` 資料行。 請注意，此查詢特意省略了計算資料行（`FullContactName`）;我們將會更新對應的預存程式，以便在步驟4中包含此資料行。

[!code-sql[Main](working-with-computed-columns-cs/samples/sample3.sql)]

輸入主要查詢並按 [下一步] 之後，嚮導可讓我們命名所要產生的四個預存程式。 將這些預存程式命名 `Suppliers_Select`、`Suppliers_Insert`、`Suppliers_Update`和 `Suppliers_Delete`，如 [圖 4] 所示。

[![自訂自動產生之預存程式的名稱](working-with-computed-columns-cs/_static/image11.png)](working-with-computed-columns-cs/_static/image10.png)

**圖 4**：自訂自動產生的預存程式名稱（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image12.png)）

下一個 [wizard] 步驟可讓我們命名 TableAdapter s 方法，並指定用來存取和更新資料的模式。 將這三個核取方塊保持核取狀態，但將 `GetData` 方法重新命名為 `GetSuppliers`。 按一下 [完成] 完成精靈。

[![將 GetSuppliers 方法重新命名為](working-with-computed-columns-cs/_static/image14.png)](working-with-computed-columns-cs/_static/image13.png)

**圖 5**：將 `GetData` 方法重新命名為 `GetSuppliers` （[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image15.png)）

按一下 [完成] 之後，嚮導會建立四個預存程式，並將 TableAdapter 和對應的 DataTable 加入至具類型的資料集。

## <a name="step-4-including-the-computed-column-in-the-tableadapter-s-main-query"></a>步驟4：在 TableAdapter s 主查詢中包含計算資料行

我們現在需要更新在步驟3中建立的 TableAdapter 和 DataTable，以包含 `FullContactName` 計算資料行。 這包含兩個步驟：

1. 更新 `Suppliers_Select` 預存程式以傳回 `FullContactName` 的計算資料行，以及
2. 更新 DataTable 以包含對應的 `FullContactName` 資料行。

首先，流覽至伺服器總管並向下切入至 [預存程式] 資料夾。 開啟 `Suppliers_Select` 預存程式，並更新 `SELECT` 查詢，以包含 `FullContactName` 計算資料行：

[!code-sql[Main](working-with-computed-columns-cs/samples/sample4.sql)]

按一下工具列中的 [儲存] 圖示、按下 Ctrl + S，或從 [檔案] 功能表選擇 [儲存 `Suppliers_Select`] 選項，將變更儲存至預存程式。

接下來，返回 DataSet 設計工具，以滑鼠右鍵按一下 `SuppliersTableAdapter`，然後從內容功能表中選擇 設定。 請注意，[`Suppliers_Select`] 資料行現在會在其資料行集合中包含 [`FullContactName`] 資料行。

[![執行 TableAdapter s 設定向導來更新 DataTable 的資料行](working-with-computed-columns-cs/_static/image17.png)](working-with-computed-columns-cs/_static/image16.png)

**圖 6**：執行 TableAdapter s 設定向導來更新 DataTable 的資料行（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image18.png)）

按一下 [完成] 完成精靈。 這會自動將對應的資料行新增至 `SuppliersDataTable`。 TableAdapter wizard 非常聰明，可以偵測 `FullContactName` 的資料行是計算資料行，因此是唯讀的。 因此，它會將資料行的 `ReadOnly` 屬性設定為 `true`。 若要確認這一點，請從 `SuppliersDataTable` 中選取資料行，然後移至屬性視窗（請參閱 [圖 7]）。 請注意，`FullContactName` 資料行 `DataType` 和 `MaxLength` 屬性也會據此進行設定。

[![FullContactName 資料行標示為唯讀](working-with-computed-columns-cs/_static/image20.png)](working-with-computed-columns-cs/_static/image19.png)

**圖 7**： `FullContactName` 資料行標示為唯讀（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image21.png)）

## <a name="step-5-adding-agetsupplierbysupplieridmethod-to-the-tableadapter"></a>步驟5：將`GetSupplierBySupplierID`方法加入至 TableAdapter

在本教學課程中，我們將建立 ASP.NET 網頁，以在可更新的方格中顯示供應商。 在過去的教學課程中，我們已更新來自商務邏輯層的一筆記錄，方法是從 DAL 將該特定記錄抓取為強型別 DataTable，更新其屬性，然後將更新的 DataTable 傳送回 DAL 以將變更傳播至資料庫。 若要完成第一個步驟-從 DAL 中抓取要更新的記錄，我們必須先將 `GetSupplierBySupplierID(supplierID)` 方法新增至 DAL。

以滑鼠右鍵按一下資料集設計中的 `SuppliersTableAdapter`，然後從內容功能表中選擇 加入查詢 選項。 如同我們在步驟3中所做的，請選取 [建立新的預存程式] 選項，讓 wizard 為我們產生新的預存程式（請參閱 [圖 3]，以取得此 wizard 步驟的螢幕擷取畫面）。 由於這個方法會傳回具有多個資料行的記錄，因此，請指出我們想要使用 SQL 查詢，這是傳回資料列的 SELECT，然後按 [下一步]。

[![選擇要傳回資料列的 SELECT 選項](working-with-computed-columns-cs/_static/image23.png)](working-with-computed-columns-cs/_static/image22.png)

**圖 8**：選擇 [選擇傳回資料列] 選項（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image24.png)）

後續步驟會提示我們輸入此方法所使用的查詢。 輸入下列程式，這會傳回與主要查詢相同的資料欄位，但針對特定供應商。

[!code-sql[Main](working-with-computed-columns-cs/samples/sample5.sql)]

下一個畫面會要求我們將自動產生的預存程式命名為。 將此預存程式命名為 `Suppliers_SelectBySupplierID` 然後按 [下一步]。

[![為預存程式命名 Suppliers_SelectBySupplierID](working-with-computed-columns-cs/_static/image26.png)](working-with-computed-columns-cs/_static/image25.png)

**圖 9**：將預存程式命名 `Suppliers_SelectBySupplierID` （[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image27.png)）

最後，嚮導會提示我們輸入要用於 TableAdapter 的資料存取模式和方法名稱。 勾選這兩個核取方塊，但將 `FillBy` 和 `GetDataBy` 方法分別重新命名為 `FillBySupplierID` 和 `GetSupplierBySupplierID`。

[![命名 TableAdapter 方法 FillBySupplierID 和 GetSupplierBySupplierID](working-with-computed-columns-cs/_static/image29.png)](working-with-computed-columns-cs/_static/image28.png)

**圖 10**：將 TableAdapter 方法命名 `FillBySupplierID` 並 `GetSupplierBySupplierID` （[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image30.png)）

按一下 [完成] 完成精靈。

## <a name="step-6-creating-the-business-logic-layer"></a>步驟6：建立商務邏輯層

在我們建立使用步驟1中所建立之計算資料行的 ASP.NET 網頁之前，我們必須先在 BLL 中新增對應的方法。 我們將在步驟7中建立的 ASP.NET 網頁，可讓使用者查看和編輯供應商。 因此，我們需要 BLL 至少提供一種方法來取得所有供應商，以及另一種方式來更新特定供應商。

在 `~/App_Code/BLL` 資料夾中建立名為 `SuppliersBLLWithSprocs` 的新類別檔案，並新增下列程式碼：

[!code-csharp[Main](working-with-computed-columns-cs/samples/sample6.cs)]

就像其他 BLL 類別一樣，`SuppliersBLLWithSprocs` 具有 `protected` `Adapter` 屬性，它會傳回 `SuppliersTableAdapter` 類別的實例，以及兩個 `public` 方法： `GetSuppliers` 和 `UpdateSupplier`。 `GetSuppliers` 方法會呼叫並傳回資料存取層中對應 `GetSupplier` 方法所傳回的 `SuppliersDataTable`。 `UpdateSupplier` 方法會透過呼叫 DAL 的 `GetSupplierBySupplierID(supplierID)` 方法，來抓取要更新之特定供應商的相關資訊。 然後，它會更新 `CategoryName`、`ContactName`和 `ContactTitle` 屬性，並藉由呼叫資料存取層的 `Update` 方法（傳入已修改的 `SuppliersRow` 物件）來認可資料庫的這些變更。

> [!NOTE]
> 除了 `SupplierID` 和 `CompanyName`以外，[供應商] 資料表中的所有資料行都允許 `NULL` 值。 因此，如果傳入的 `contactName` 或 `contactTitle` 參數 `null` 我們必須分別使用 `ContactTitle` 和 `NULL` 方法，將對應的 `ContactName` 和 `SetContactNameNull` 屬性設定為 `SetContactTitleNull` 資料庫值。

## <a name="step-7-working-with-the-computed-column-from-the-presentation-layer"></a>步驟7：使用展示層中的計算資料行

將計算資料行新增至 `Suppliers` 資料表，並據以更新 DAL 和 BLL 之後，我們就可以建立可與 `FullContactName` 計算資料行搭配使用的 ASP.NET 網頁。 一開始先開啟 [`AdvancedDAL`] 資料夾中的 [`ComputedColumns.aspx`] 頁面，然後從 [工具箱] 將 [GridView] 拖曳至設計工具。 將 GridView 的 `ID` 屬性設定為 `Suppliers`，並將其從智慧標籤系結至名為 `SuppliersDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 使用我們在步驟6中新增的 `SuppliersBLLWithSprocs` 類別，然後按 [下一步]。

[![將 ObjectDataSource 設定為使用 SuppliersBLLWithSprocs 類別](working-with-computed-columns-cs/_static/image32.png)](working-with-computed-columns-cs/_static/image31.png)

**圖 11**：設定 ObjectDataSource 使用 `SuppliersBLLWithSprocs` 類別（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image33.png)）

`SuppliersBLLWithSprocs` 類別中只定義了兩個方法： `GetSuppliers` 和 `UpdateSupplier`。 請確定在 [選取和更新] 索引標籤中分別指定這兩個方法，然後按一下 [完成] 以完成 ObjectDataSource 的設定。

完成資料來源設定 wizard 後，Visual Studio 將會針對每個傳回的資料欄位加入 BoundField。 移除 `SupplierID` BoundField，並分別將 `CompanyName`、`ContactName`、`ContactTitle`和 `FullContactName` BoundFields 的 `HeaderText` 屬性變更為 [公司]、[連絡人姓名]、[標題] 和 [完整連絡人姓名]。 從智慧標籤中，勾選 [啟用編輯] 核取方塊，以開啟 GridView 的內建編輯功能。

除了將 BoundFields 加入 GridView 之外，資料來源 Wizard 的完成也會導致 Visual Studio 將 ObjectDataSource s `OldValuesParameterFormatString` 屬性設定為原始\_{0}。 將此設定還原回其預設值 {0}。

對 GridView 和 ObjectDataSource 進行這些編輯之後，其宣告式標記看起來應該如下所示：

[!code-aspx[Main](working-with-computed-columns-cs/samples/sample7.aspx)]

接下來，透過瀏覽器造訪此頁面。 如 [圖 12] 所示，每個供應商都會列在包含 [`FullContactName`] 資料行的方格中，其值只是將其他三個數據行的串連設定為 `ContactName` （`ContactTitle`，`CompanyName`）。

[![方格中列出每個供應商](working-with-computed-columns-cs/_static/image35.png)](working-with-computed-columns-cs/_static/image34.png)

**圖 12**：每個供應商都會列在方格中（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image36.png)）

按一下特定供應商的 [編輯] 按鈕會導致回傳，而且該資料列會呈現在其編輯介面中（請參閱 [圖 13]）。 前三個數據行在其預設的編輯介面中轉譯-TextBox 控制項，其 `Text` 屬性設定為資料欄位的值。 不過，`FullContactName` 資料行仍會保留為文字。 當 BoundFields 在資料來源設定 wizard 完成時加入至 GridView 時，`FullContactName` BoundField s `ReadOnly` 屬性會設定為 `true`，因為 `SuppliersDataTable` 中對應的 `FullContactName` 資料行將其 `ReadOnly` 屬性設定為 `true`。 如步驟4所述，`FullContactName` s `ReadOnly` 屬性已設定為 `true`，因為 TableAdapter 偵測到資料行是計算資料行。

[![無法編輯 FullContactName 資料行](working-with-computed-columns-cs/_static/image38.png)](working-with-computed-columns-cs/_static/image37.png)

**圖 13**：無法編輯 `FullContactName` 資料行（[按一下以查看完整大小的影像](working-with-computed-columns-cs/_static/image39.png)）

請繼續並更新一個或多個可編輯資料行的值，然後按一下 [更新]。 請注意，`FullContactName` s 值會自動更新以反映變更。

> [!NOTE]
> GridView 目前針對可編輯的欄位使用 BoundFields，因此會產生預設的編輯介面。 因為 [`CompanyName`] 欄位是必要的，所以應該轉換成包含 RequiredFieldValidator 的 TemplateField。 我將這個練習留給感興趣的讀者。 如需將 BoundField 轉換為 TemplateField 和加入驗證控制項的逐步指示，請參閱將[驗證控制項新增至編輯和插入介面](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)教學課程。

## <a name="summary"></a>總結

定義資料表的架構時，Microsoft SQL Server 允許包含計算資料行。 這些資料行的值是從通常參考相同記錄中其他資料行值的運算式計算而來。 由於計算資料行的值是以運算式為基礎，因此它們是唯讀的，而且無法在 `INSERT` 或 `UPDATE` 語句中指派值。 在 TableAdapter 的主查詢中使用計算資料行時，如果嘗試自動產生對應的 `INSERT`、`UPDATE`和 `DELETE` 語句，這就會造成挑戰。

在本教學課程中，我們已討論規避計算資料行所造成之挑戰的技術。 特別是，我們使用 TableAdapter 中的預存程式，來克服使用臨機操作 SQL 語句之 Tableadapter 中的肯定脆弱度。 當 [TableAdapter wizard] 建立新的預存程式時，請務必讓主查詢一開始省略任何計算資料行，因為它們的存在會防止產生資料修改預存程式。 一開始設定 TableAdapter 之後，可以改良其 `SelectCommand` 預存程式來包含任何計算資料行。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Geisenow 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](adding-additional-datatable-columns-cs.md)
> [下一頁](configuring-the-data-access-layer-s-connection-and-command-level-settings-cs.md)
