---
uid: web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
title: 為具類型資料集的 Tableadapter 建立新的預存程式（VB） |Microsoft Docs
author: rick-anderson
description: 在先前的教學課程中，我們已在程式碼中建立 SQL 語句，並將語句傳遞至要執行的資料庫。 另一種方法是使用 。
ms.author: riande
ms.date: 07/18/2007
ms.assetid: a5a4a9ba-d18d-489a-a6b0-a3c26d6b0274
msc.legacyurl: /web-forms/overview/data-access/advanced-data-access-scenarios/creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb
msc.type: authoredcontent
ms.openlocfilehash: a7cc890038e5bb4eb61c7c3b808154c196ab2423
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78533646"
---
# <a name="creating-new-stored-procedures-for-the-typed-datasets-tableadapters-vb"></a>為具類型資料集的 Tableadapter 建立新的預存程序 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_67_VB.zip)或[下載 PDF](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/datatutorial67vb1.pdf)

> 在先前的教學課程中，我們已在程式碼中建立 SQL 語句，並將語句傳遞至要執行的資料庫。 另一個方法是使用預存程式，其中 SQL 語句是在資料庫中預先定義的。 在本教學課程中，我們將學習如何讓 TableAdapter Wizard 為我們產生新的預存程式。

## <a name="introduction"></a>簡介

這些教學課程的資料存取層（DAL）會使用具類型的資料集。 如[建立資料存取層](../introduction/creating-a-data-access-layer-vb.md)教學課程中所述，具類型的資料集是由強型別的 Datatable 和 tableadapter 所組成。 Datatable 代表系統中的邏輯實體，而 Tableadapter 介面與基礎資料庫來執行資料存取工作。 這包括以資料填入 Datatable、執行傳回純量資料的查詢，以及插入、更新和刪除資料庫中的記錄。

Tableadapter 所執行的 SQL 命令可以是臨機操作 SQL 語句，例如 `SELECT columnList FROM TableName`或預存程式。 我們架構中的 Tableadapter 會使用臨機操作 SQL 語句。 不過，許多開發人員和資料庫管理員都偏好使用預存程式，而不是特定 SQL 語句的安全性、可維護性和可更新的原因。 其他則 ardently 偏好特定 SQL 語句以提供彈性。 在我自己的工作中，我偏好在臨機操作 SQL 語句上進行預存程式，但選擇使用特定 SQL 語句來簡化先前的教學課程。

定義 TableAdapter 或加入新的方法時，TableAdapter 的 wizard 可讓您輕鬆地建立新的預存程式，或使用現有的預存程式，就像使用臨機操作 SQL 語句一樣。 在本教學課程中，我們將檢查如何讓 TableAdapter s wizard 自動產生預存程式。 在下一個教學課程中，我們將探討如何設定 TableAdapter s 方法，以使用現有或手動建立的預存程式。

> [!NOTE]
> 請參閱 Howard 的 blog 專案[Don t 使用預存程式嗎？](http://grokable.com/2003/11/dont-use-stored-procedures-yet-must-be-suffering-from-nihs-not-invented-here-syndrome/)和[Frans Bouma](https://weblogs.asp.net/fbouma/) s 的 Blog 專案[預存程式都不正確，M Kay？，可](https://weblogs.asp.net/fbouma/archive/2003/11/18/38178.aspx)讓生動爭論預存程式和臨機操作 SQL 的優缺點。

## <a name="stored-procedure-basics"></a>預存程序基本概念

函數是所有程式設計語言通用的結構。 函式是在呼叫函數時執行的語句集合。 函數可以接受輸入參數，而且可以選擇性地傳回值。 *[預存程式](http://en.wikipedia.org/wiki/Stored_procedure)* 是資料庫結構，與程式設計語言中的函式共用許多相似之處。 預存程式是由呼叫預存程式時所執行的一組 T-sql 語句所組成。 預存程式可能接受零到多個輸入參數，而且可以從 `SELECT` 查詢中傳回純量值、輸出參數，或最常傳回的結果集。

> [!NOTE]
> 預存程式通常稱為 sprocs 或 SPs。

預存程式是使用[`CREATE PROCEDURE`](https://msdn.microsoft.com/library/aa258259(SQL.80).aspx) t-sql 語句來建立的。 例如，下列 T-sql 腳本會建立名為 `GetProductsByCategoryID` 的預存程式，它會採用名為 `@CategoryID` 的單一參數，並傳回 `UnitPrice`資料表中具有相符 `Discontinued` 值之資料行的 `ProductID`、`ProductName`、`Products` 和 `CategoryID` 欄位：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample1.sql)]

建立這個預存程式之後，就可以使用下列語法來呼叫它：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample2.sql)]

> [!NOTE]
> 在下一個教學課程中，我們將檢查如何透過 Visual Studio IDE 來建立預存程式。 不過，在本教學課程中，我們要讓 TableAdapter wizard 為我們自動產生預存程式。

除了只傳回資料，預存程式通常用來在單一交易的範圍內執行多個資料庫命令。 例如，名為 `DeleteCategory`的預存程式可能會採用 `@CategoryID` 參數，並執行兩個 `DELETE` 的語句： first，一個用來刪除相關的產品，另一個則刪除指定的分類。 預存程式內的多個語句*不*會自動包裝在交易內。 需要發出其他 T-sql 命令，以確保預存程式的多個命令會被視為不可部分完成的作業。 在後續的教學課程中，我們將瞭解如何將預存程式的命令包裝在交易範圍內。

在架構中使用預存程式時，資料存取層的方法會叫用特定的預存程式，而不是發出臨機操作的 SQL 語句。 這會集中執行 SQL 語句的位置（在資料庫上），而不是在應用程式的架構內定義。 這種集中的方式可讓您更輕鬆地尋找、分析及微調查詢，並提供更清楚的圖片，讓您瞭解資料庫的使用位置和方式。

如需預存程式基本概念的詳細資訊，請參閱本教學課程結尾的進一步閱讀一節中的資源。

## <a name="step-1-creating-the-advanced-data-access-layer-scenarios-web-pages"></a>步驟1：建立先進的資料存取層案例網頁

在我們開始討論使用預存程式建立 DAL 之前，讓我們先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在此和接下來的幾個教學課程中所需。 從新增名為 `AdvancedDAL`的資料夾開始。 接下來，將下列 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `NewSprocs.aspx`
- `ExistingSprocs.aspx`
- `JOINs.aspx`
- `AddingColumns.aspx`
- `ComputedColumns.aspx`
- `EncryptingConfigSections.aspx`
- `ManagedFunctionsAndSprocs.aspx`

![新增高級資料存取層案例教學課程的 ASP.NET 網頁](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image1.png)

**圖 1**：新增先進資料存取層案例教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`AdvancedDAL`] 資料夾中的 `Default.aspx` 會在其區段中列出教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 因此，請將這個使用者控制項加入至 `Default.aspx`，方法是將它從方案總管拖曳至頁面 s 設計檢視。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image3.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image2.png)

**圖 2**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image4.png)）

最後，將這些頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，請在使用批次資料 `<siteMapNode>`之後，加入下列標記：

[!code-xml[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample3.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含 advanced DAL 案例教學課程的專案。

![網站地圖現在包含 Advanced DAL 案例教學課程的專案](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image5.png)

**圖 3**：網站地圖現在包含 Advanced DAL 案例教學課程的專案

## <a name="step-2-configuring-a-tableadapter-to-create-new-stored-procedures"></a>步驟2：設定 TableAdapter 以建立新的預存程式

為了示範如何建立使用預存程式（而不是臨機操作 SQL 語句）的資料存取層，讓 s 在名為 `NorthwindWithSprocs.xsd`的 `~/App_Code/DAL` 資料夾中建立新的具類型資料集。 因為我們已在先前的教學課程中詳細說明此程式，所以我們將會快速完成這裡的步驟。 如果您停滯或需要進一步的逐步指示來建立和設定具類型的資料集，請回頭參閱[建立資料存取層](../introduction/creating-a-data-access-layer-vb.md)教學課程。

以滑鼠右鍵按一下 [`DAL`] 資料夾，選擇 [加入新專案]，然後選取資料集範本（如 [圖 4] 所示），將新的資料集加入至專案。

[![將新的具類型資料集加入至名為 NorthwindWithSprocs 的專案](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image7.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image6.png)

**圖 4**：將新的具型別資料集加入至名為 `NorthwindWithSprocs.xsd` 的專案（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image8.png)）

這會建立新的具型別資料集、開啟其設計工具、建立新的 TableAdapter，然後啟動 [TableAdapter 設定向導]。 TableAdapter Configuration Wizard 的第一個步驟會要求我們選取要使用的資料庫。 Northwind 資料庫的連接字串應該會列在下拉式清單中。 選取此，然後按 [下一步]。

在下一個畫面中，我們可以選擇 TableAdapter 應該如何存取資料庫。 在先前的教學課程中，我們選取了 [使用 SQL 語句] 的第一個選項。 在此教學課程中，選取第二個選項 [建立新的預存程式]，然後按 [下一步]

[![指示 TableAdapter 建立新的預存程式](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image10.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image9.png)

**圖 5**：指示 TableAdapter 建立新的預存程式（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image11.png)）

就像使用臨機操作 SQL 語句一樣，在下列步驟中，我們會要求您提供 TableAdapter s 主要查詢的 `SELECT` 語句。 但是，TableAdapter s wizard 會建立包含這個 `SELECT` 查詢的預存程式，而不是使用這裡輸入的 `SELECT` 語句直接執行臨機操作查詢。

針對此 TableAdapter 使用下列 `SELECT` 查詢：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample4.sql)]

[![輸入選取查詢](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image13.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image12.png)

**圖 6**：輸入 `SELECT` 查詢（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image14.png)）

> [!NOTE]
> 上述查詢與 `Northwind` 具類型資料集中 `ProductsTableAdapter` 的主要查詢稍有不同。 回想一下，`Northwind` 具類型的資料集中的 `ProductsTableAdapter` 包含兩個相互關聯的子查詢，以傳回每個產品的類別目錄和供應商的類別名稱和公司名稱。 在即將[更新 TableAdapter 以使用](updating-the-tableadapter-to-use-joins-vb.md)聯結教學課程中，我們將探討如何將此相關資料新增至此 TableAdapter。

請花點時間按一下 [Advanced Options] 按鈕。 在這裡，我們可以指定 wizard 是否也應該產生 TableAdapter 的 insert、update 和 delete 語句、是否使用開放式平行存取，以及是否應該在插入和更新之後重新整理資料表。 預設會核取 [產生 Insert、Update 和 Delete 語句] 選項。 保持核取狀態。 在此教學課程中，請保持未核取 [使用開放式平行存取選項]。

當 TableAdapter wizard 自動建立預存程式時，會顯示 [重新整理資料表] 選項已忽略。 不論是否核取此核取方塊，所產生的 insert 和 update 預存程式都會抓取剛插入或剛更新的記錄，如我們在步驟3中所見。

![保持核取 [產生插入、更新和刪除語句] 選項](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image15.png)

**圖 7**：保持核取 [產生插入、更新和刪除語句] 選項

> [!NOTE]
> 如果已核取 [使用開放式平行存取] 選項，則當其他欄位有變更時，嚮導會將其他條件新增至 `WHERE` 子句，以防止更新資料。 如需使用 TableAdapter 內建開放式並行存取控制功能的詳細資訊，請參閱[執行開放式並行](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb.md)存取教學課程。

在輸入 `SELECT` 查詢並確認已核取 [產生 Insert、Update 和 Delete 語句] 選項之後，請按 [下一步]。 [圖 8] 所示的下一個畫面會提示您輸入 wizard 所建立之預存程式的名稱，以便選取、插入、更新和刪除資料。 將這些預存程式名稱變更為 `Products_Select`、`Products_Insert`、`Products_Update`和 `Products_Delete`。

[![重新命名預存程式](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image17.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image16.png)

**圖 8**：重新命名預存程式（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image18.png)）

若要查看 TableAdapter wizard 將用來建立四個預存程式的 T-sql，請按一下 [預覽 SQL 腳本] 按鈕。 在 [預覽 SQL 腳本] 對話方塊中，您可以將腳本儲存至檔案，或將它複製到剪貼簿。

![預覽用來產生預存程式的 SQL 腳本](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image19.png)

**圖 9**：預覽用來產生預存程式的 SQL 腳本

命名預存程式之後，請按 [下一步]，將 TableAdapter 的對應方法命名為。 就像使用臨機操作 SQL 語句一樣，我們可以建立方法來填滿現有的 DataTable，或傳回一個新的。 我們也可以指定 TableAdapter 是否應包含用於插入、更新和刪除記錄的資料庫直接模式。 將這三個核取方塊保持為已核取，但重新命名會將 DataTable 方法傳回給 `GetProducts` （如 [圖 10] 所示）。

[![命名方法填滿和 GetProducts](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image21.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image20.png)

**圖 10**：將方法命名 `Fill` 並 `GetProducts` （[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image22.png)）

按 [下一步] 以查看嚮導將執行之步驟的摘要。 按一下 [完成] 按鈕以完成嚮導。 一旦 wizard 完成，您就會回到資料集的設計工具，現在應該會包含 `ProductsDataTable`。

[![資料集的設計工具會顯示新加入的 ProductsDataTable](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image24.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image23.png)

**圖 11**：資料集的設計工具會顯示新加入的 `ProductsDataTable` （[按一下以觀看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image25.png)）

## <a name="step-3-examining-the-newly-created-stored-procedures"></a>步驟3：檢查新建立的預存程式

在步驟2中使用的 TableAdapter wizard，會自動建立用來選取、插入、更新和刪除資料的預存程式。 您可以藉由前往伺服器總管並向下切入資料庫的 [預存程式] 資料夾，透過 Visual Studio 來查看或修改這些預存程式。 如 [圖 12] 所示，Northwind 資料庫包含四個新的預存程式： `Products_Delete`、`Products_Insert`、`Products_Select`和 `Products_Update`。

![在步驟2中建立的四個預存程式，可以在資料庫的 [預存程式] 資料夾中找到](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image26.png)

**圖 12**：在步驟2中建立的四個預存程式，可以在資料庫的 [預存程式] 資料夾中找到

> [!NOTE]
> 如果看不到 [伺服器總管]，請移至 [View] 功能表，然後選擇 [伺服器總管] 選項。 如果您看不到從步驟2新增的產品相關預存程式，請嘗試以滑鼠右鍵按一下 [預存程式] 資料夾，然後選擇 [重新整理]。

若要查看或修改預存程式，請在伺服器總管中按兩下其名稱，或者以滑鼠右鍵按一下預存程式，然後選擇 [開啟]。 [圖 13] 顯示開啟時的 `Products_Delete` 預存程式。

[![預存程式可以在中開啟和修改 Visual Studio](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image28.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image27.png)

**圖 13**：預存程式可以從 Visual Studio 中開啟和修改（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image29.png)）

`Products_Delete` 和 `Products_Select` 預存程式的內容相當簡單。 另一方面，`Products_Insert` 和 `Products_Update` 預存程式在 `INSERT` 和 `UPDATE` 語句之後執行 `SELECT` 語句時，會有進一步的檢查。 例如，下列 SQL 會組成 `Products_Insert` 預存程式：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample5.sql)]

預存程式會接受 TableAdapter s wizard 中指定的 `SELECT` 查詢所傳回的 `Products` 資料行做為輸入參數，而這些值會用於 `INSERT` 的語句中。 在 `INSERT` 語句後面，`SELECT` 查詢會用來傳回新加入記錄的 `Products` 資料行值（包括 `ProductID`）。 當使用批次更新模式加入新記錄時，這個重新整理功能就很有用，因為它會自動以資料庫所指派的自動遞增值來更新新增的 `ProductRow` 實例 `ProductID` 屬性。

下列程式碼將說明這項功能。 其中包含針對 `NorthwindWithSprocs` 具類型資料集所建立的 `ProductsTableAdapter` 和 `ProductsDataTable`。 新的產品會藉由建立 `ProductsRow` 實例、提供其值，以及呼叫 TableAdapter 的 `Update` 方法（傳入 `ProductsDataTable`）來新增至資料庫。 就內部而言，TableAdapter 的 `Update` 方法會列舉傳入的 DataTable 中的 `ProductsRow` 實例（在此範例中，我們剛剛新增了一個），並執行適當的 insert、update 或 delete 命令。 在此情況下，會執行 `Products_Insert` 預存程式，這會將新的記錄加入 `Products` 資料表，並傳回新加入之記錄的詳細資料。 然後會更新 `ProductsRow` 實例 `ProductID` 值。 在 `Update` 方法完成之後，我們可以透過 `ProductsRow` 的 `ProductID` 屬性，存取新增的記錄 `ProductID` 值。

[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample6.vb)]

`Products_Update` 預存程式類似地在其 `UPDATE` 語句後面包含 `SELECT` 語句。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample7.sql)]

請注意，這個預存套裝程式含兩個 `ProductID`的輸入參數： `@Original_ProductID` 和 `@ProductID`。 這項功能可用於可能會變更主鍵的案例。 例如，在員工資料庫中，每個員工記錄可能會使用員工的社會安全號碼作為其主要金鑰。 若要變更現有員工的社會安全號碼，必須提供新的社會安全號碼和原始的身分證號碼。 對於 `Products` 資料表而言，這類功能不是必要的，因為 `ProductID` 資料行是 `IDENTITY` 的資料行，而且永遠不會變更。 事實上，`Products_Update` 預存程式中的 `UPDATE` 語句不會在其資料行清單中包含 `ProductID` 資料行。 因此，雖然在 `UPDATE` 語句 s `WHERE` 子句中使用 `@Original_ProductID`，但 `Products` 資料表則是多餘的，而且可由 `@ProductID` 參數取代。 修改預存程式的參數時，必須同時更新使用該預存程式的 TableAdapter 方法。

## <a name="step-4-modifying-a-stored-procedure-s-parameters-and-updating-the-tableadapter"></a>步驟4：修改預存程式的參數並更新 TableAdapter

由於 `@Original_ProductID` 參數是多餘的，因此請將它從 `Products_Update` 預存程式全部移除。 開啟 `Products_Update` 預存程式，刪除 `@Original_ProductID` 參數，然後在 `UPDATE` 語句的 `WHERE` 子句中，將從 `@Original_ProductID` 使用的參數名稱變更為 `@ProductID`。 進行這些變更後，預存程式內的 T-sql 看起來應該如下所示：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample8.sql)]

若要將這些變更儲存到資料庫，請按一下工具列中的 [儲存] 圖示，或按 Ctrl + S。 此時，`Products_Update` 預存程式不會預期 `@Original_ProductID` 輸入參數，但 TableAdapter 已設定為傳遞這類參數。 您可以查看 TableAdapter 將傳送至 `Products_Update` 預存程式的參數，方法是選取 DataSet 設計工具中的 TableAdapter、前往屬性視窗，然後按一下 `UpdateCommand` s `Parameters` 集合中的省略號。 這會顯示 [圖 14] 所示的 [參數集合編輯器] 對話方塊。

![[參數集合編輯器] 會列出傳遞給 Products_Update 預存程式的參數。](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image30.png)

**圖 14**： [參數集合編輯器] 會列出傳遞給 `Products_Update` 預存程式的參數。

只要從成員清單中選取 [`@Original_ProductID`] 參數，然後按一下 [移除] 按鈕，就可以從這裡移除此參數。

或者，您也可以在設計工具中的 TableAdapter 上按一下滑鼠右鍵，然後選擇 [設定]，以重新整理用於所有方法的參數。 這會顯示 [TableAdapter 設定向導]，列出用來選取、插入、更新和刪除的預存程式，以及預存程式預期會接收到的參數。 如果您按一下 [更新] 下拉式清單，您可以看到 `Products_Update` 預存程式預期的輸入參數，現在已不再包含 `@Original_ProductID` （請參閱 [圖 15]）。 只要按一下 [完成]，即可自動更新 TableAdapter 所使用的參數集合。

[![您也可以使用 TableAdapter s 設定 Wizard 來重新整理其方法參數集合](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image32.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image31.png)

**圖 15**：您也可以使用 [TableAdapter] 設定向導來重新整理其方法參數集合（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image33.png)）

## <a name="step-5-adding-additional-tableadapter-methods"></a>步驟5：新增其他 TableAdapter 方法

如步驟2所示，建立新的 TableAdapter 時，可以輕鬆地自動產生對應的預存程式。 將其他方法新增至 TableAdapter 時也是如此。 為了說明這一點，讓我們將 `GetProductByProductID(productID)` 方法新增至在步驟2中建立的 `ProductsTableAdapter`。 這個方法會將 `ProductID` 值做為輸入，並傳回指定之產品的詳細資料。

首先，以滑鼠右鍵按一下 TableAdapter，然後從內容功能表選擇 [加入查詢]。

![將新的查詢加入至 TableAdapter](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image34.png)

**圖 16**：將新的查詢加入至 TableAdapter

這會啟動 [TableAdapter 查詢設定向導]，其中會先提示 TableAdapter 應該如何存取資料庫。 若要建立新的預存程式，請選擇 [建立新的預存程式] 選項，然後按 [下一步]。

[![選擇 [建立新的預存程式] 選項](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image36.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image35.png)

**圖 17**：選擇 [建立新的預存程式] 選項（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image37.png)）

下一個畫面會要求我們識別要執行的查詢類型，是否會傳回一組資料列或單一純量值，或是執行 `UPDATE`、`INSERT`或 `DELETE` 語句。 由於 `GetProductByProductID(productID)` 方法會傳回資料列，請保留選取 [傳回資料列的 SELECT] 選項，然後按 [下一步]。

[![選擇 [選擇傳回資料列] 選項](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image39.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image38.png)

**圖 18**：選擇 [選擇傳回資料列] 選項（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image40.png)）

下一個畫面會顯示 TableAdapter s 主查詢，這只會列出預存程式的名稱（`dbo.Products_Select`）。 將預存程式名稱取代為下列 `SELECT` 語句，這會傳回指定產品的所有產品欄位：

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample9.sql)]

[![以 SELECT 查詢取代預存程式名稱](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image42.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image41.png)

**圖 19**：以 `SELECT` 查詢取代預存程式名稱（[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image43.png)）

接下來的畫面會要求您命名將要建立的預存程式。 輸入 `Products_SelectByProductID` 的名稱，然後按 [下一步]。

[![命名新的預存程式 Products_SelectByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image45.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image44.png)

**圖 20**：為新的預存程式命名 `Products_SelectByProductID` （[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image46.png)）

Wizard 的最後一個步驟可讓我們變更所產生的方法名稱，並指出是否要使用 [填滿 DataTable] 模式、傳回 DataTable 模式或兩者。 針對這個方法，請同時選取這兩個選項，但將方法重新命名為 `FillByProductID` 和 `GetProductByProductID`。 按 [下一步] 以查看嚮導將執行之步驟的摘要，然後按一下 [完成] 以完成嚮導。

[![將 TableAdapter s 方法重新命名為 FillByProductID 和 GetProductByProductID](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image48.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image47.png)

**圖 21**：將 TableAdapter s 方法重新命名為 `FillByProductID` 和 `GetProductByProductID` （[按一下以查看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image49.png)）

完成 wizard 之後，TableAdapter 具有可用的新方法，`GetProductByProductID(productID)` 在叫用時，將會執行剛建立的 `Products_SelectByProductID` 預存程式。 請花點時間切入 [預存程式] 資料夾並開啟 [`Products_SelectByProductID`] （如果看不到，以滑鼠右鍵按一下 [預存程式] 資料夾，然後選擇 [重新整理]），從伺服器總管查看這個新的預存程式。

請注意，`SelectByProductID` 預存程式會採用 `@ProductID` 做為輸入參數，並執行我們在 wizard 中輸入的 `SELECT` 語句。

[!code-sql[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample10.sql)]

## <a name="step-6-creating-a-business-logic-layer-class"></a>步驟6：建立商務邏輯層類別

在整個教學課程系列中，我們都嘗試維護一個分層架構，其中展示層會對商務邏輯層（BLL）進行所有的呼叫。 為了遵守這項設計決策，我們必須先為新的具型別資料集建立 BLL 類別，然後才能從展示層存取產品資料。

在 `~/App_Code/BLL` 資料夾中建立名為 `ProductsBLLWithSprocs.vb` 的新類別檔案，並在其中新增下列程式碼：

[!code-vb[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample11.vb)]

這個類別會模擬先前教學課程中的 `ProductsBLL` 類別語義，但會使用 `NorthwindWithSprocs` 資料集中的 `ProductsTableAdapter` 和 `ProductsDataTable` 物件。 例如，`ProductsBLLWithSprocs` 類別會使用 `Imports NorthwindWithSprocsTableAdapters`，而不是在類別檔案的開頭 `ProductsBLL` 執行 `Imports NorthwindTableAdapters` 語句。 同樣地，在此類別中使用的 `ProductsDataTable` 和 `ProductsRow` 物件會加上 `NorthwindWithSprocs` 命名空間的前置詞。 `ProductsBLLWithSprocs` 類別提供兩種資料存取方法，`GetProducts` 和 `GetProductByProductID`，以及新增、更新和刪除單一產品實例的方法。

## <a name="step-7-working-with-thenorthwindwithsprocsdataset-from-the-presentation-layer"></a>步驟7：使用展示層中的`NorthwindWithSprocs`資料集

此時，我們建立了 DAL，其使用預存程式來存取和修改基礎資料庫資料。 我們也建立了一個基本的 BLL，其中包含用來抓取所有產品或特定產品的方法，以及用來新增、更新和刪除產品的方法。 若要將本教學課程四捨五入，讓 s 建立一個 ASP.NET 網頁，使用 BLL 的 `ProductsBLLWithSprocs` 類別來顯示、更新和刪除記錄。

開啟 [`AdvancedDAL`] 資料夾中的 [`NewSprocs.aspx`] 頁面，然後將 GridView 從 [工具箱] 拖曳至設計工具，將它命名為 `Products`。 從 GridView 的智慧標籤選擇將其系結至名為 `ProductsDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以使用 `ProductsBLLWithSprocs` 類別，如 [圖 22] 所示。

[![將 ObjectDataSource 設定為使用 ProductsBLLWithSprocs 類別](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image51.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image50.png)

**圖 22**：設定 ObjectDataSource 使用 `ProductsBLLWithSprocs` 類別（[按一下以觀看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image52.png)）

[選取] 索引標籤中的下拉式清單有兩個選項： [`GetProducts`] 和 [`GetProductByProductID`]。 因為我們想要顯示 GridView 中的所有產品，請選擇 [`GetProducts`] 方法。 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單，每個都只有一個方法。 請確定每個下拉式清單都已選取適當的方法，然後按一下 [完成]。

ObjectDataSource wizard 完成後，Visual Studio 會將 BoundFields 和 CheckBoxField 新增至 [產品資料] 欄位的 GridView。 藉由勾選智慧標籤中的 [啟用編輯] 和 [啟用刪除] 選項，來開啟 GridView 的內建編輯和刪除功能。

[![頁面包含已啟用編輯和刪除支援的 GridView](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image54.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image53.png)

**圖 23**：此頁面包含已啟用編輯和刪除支援的 GridView （[按一下以觀看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image55.png)）

如先前的教學課程中所討論，在 ObjectDataSource s wizard 完成後，Visual Studio 將 `OldValuesParameterFormatString` 屬性設為原始\_{0}。 這必須還原為預設值 {0}，才能讓資料修改功能適當地使用我們 BLL 中的方法所預期的參數。 因此，請務必將 `OldValuesParameterFormatString` 屬性設定為 {0}，或從宣告式語法中移除屬性。

完成 [設定資料來源] 嚮導之後，開啟 GridView 中的編輯與刪除支援，並將 ObjectDataSource 的 `OldValuesParameterFormatString` 屬性傳回其預設值，您的頁面宣告式標記看起來應該如下所示：

[!code-aspx[Main](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/samples/sample12.aspx)]

到目前為止，我們可以藉由自訂編輯介面以包含驗證來整理 GridView，讓 `CategoryID` 和 `SupplierID` 的資料行呈現為 Dropdownlist 進行，依此類推。 我們也可以將用戶端確認新增至 [刪除] 按鈕，建議您花時間執行這些增強功能。 因為這些主題已在先前的教學課程中討論過，所以我們不會在這裡討論它們。

無論您是否增強 GridView，請在瀏覽器中測試 page s 核心功能。 如 [圖 24] 所示，此頁面會列出 GridView 中提供每個資料列編輯和刪除功能的產品。

[![可以從 GridView 查看、編輯和刪除產品](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image57.png)](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image56.png)

**圖 24**：可以從 GridView 查看、編輯和刪除產品（[按一下以觀看完整大小的影像](creating-new-stored-procedures-for-the-typed-dataset-s-tableadapters-vb/_static/image58.png)）

## <a name="summary"></a>總結

具類型資料集中的 Tableadapter 可以使用臨機操作 SQL 語句或預存程式來存取資料庫中的資料。 使用預存程式時，可以使用現有的預存程式，也可以指示 TableAdapter wizard 根據 `SELECT` 查詢來建立新的預存程式。 在本教學課程中，我們探討了如何為我們自動建立預存程式。

雖然自動產生的預存程式有助於節省時間，但在某些情況下，嚮導所建立的預存程式不會與我們自己建立的不同。 其中一個範例是 `Products_Update` 預存程式，即使 `@Original_ProductID` 參數是多餘的，也應該同時 `@Original_ProductID` 和 `@ProductID` 輸入參數。

在許多情況下，預存程式可能已經建立，或者我們想要手動建立它們，以便更精細地控制預存程式的命令。 不論是哪一種情況，我們都想要指示 TableAdapter 針對其方法使用現有的預存程式。 在下一個教學課程中，我們應該會看到如何完成這項操作。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [建立和維護預存程式](https://msdn.microsoft.com/library/aa214299(SQL.80).aspx)
- [從預存程式中取出純量資料](http://aspnet.4guysfromrolla.com/articles/062905-1.aspx)
- [SQL Server 預存程式基本概念](http://www.awprofessional.com/articles/article.asp?p=25288&amp;rl=1)
- [預存程式：總覽](http://www.sqlteam.com/item.asp?ItemID=563)
- [撰寫預存程式](http://www.4guysfromrolla.com/webtech/111499-1.shtml)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Geisenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](creating-stored-procedures-and-user-defined-functions-with-managed-code-cs.md)
> [下一頁](using-existing-stored-procedures-for-the-typed-dataset-s-tableadapters-vb.md)
