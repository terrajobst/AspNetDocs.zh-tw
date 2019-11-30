---
uid: web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
title: 將資料庫修改包裝在交易中C#（） |Microsoft Docs
author: rick-anderson
description: 本教學課程是四個中的第一個，它會查看更新、刪除和插入批次的資料。 在本教學課程中，我們將瞭解資料庫交易如何允許 。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: b45fede3-c53a-4ea1-824b-20200808dbae
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/wrapping-database-modifications-within-a-transaction-cs
msc.type: authoredcontent
ms.openlocfilehash: da69e466a5b506b869dc8fc0624f3e6a479199a8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74624771"
---
# <a name="wrapping-database-modifications-within-a-transaction-c"></a>將資料庫修改包裝在交易中 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_63_CS.zip)或[下載 PDF](wrapping-database-modifications-within-a-transaction-cs/_static/datatutorial63cs1.pdf)

> 本教學課程是四個中的第一個，它會查看更新、刪除和插入批次的資料。 在本教學課程中，我們將瞭解資料庫交易如何讓批次修改當做不可部分完成的作業來執行，以確保所有步驟都成功，或所有步驟都失敗。

## <a name="introduction"></a>簡介

如我們所見，從[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教學課程的總覽開始，GridView 提供了資料列層級編輯和刪除的內建支援。 只要按幾下滑鼠，就可以建立豐富的資料修改介面，而不需要撰寫一行程式碼，因為您是以每個資料列為基礎的編輯和刪除內容。 不過，在某些情況下，這是不夠的，因此我們需要讓使用者能夠編輯或刪除一批記錄。

例如，大部分的網頁型電子郵件客戶程式都會使用方格來列出每個訊息，其中每個資料列都包含一個核取方塊，以及電子郵件的資訊（主旨、寄件者等等）。 此介面可讓使用者藉由檢查多個訊息，然後按一下 [刪除選取的訊息] 按鈕來刪除它。 批次編輯介面適用于使用者通常會編輯許多不同記錄的情況。 除了強制使用者按一下 [編輯]、進行變更，然後針對每個需要修改的記錄按一下 [更新] 時，批次編輯介面會使用其編輯介面來呈現每個資料列。 使用者可以快速修改需要變更的資料列集，然後按一下 [全部更新] 按鈕來儲存這些變更。 在這一組教學課程中，我們將探討如何建立介面來插入、編輯和刪除批次的資料。

執行批次作業時，請務必確定批次中某些作業的可能是否可成功，而其他則失敗。 考慮使用批次刪除介面-如果成功刪除第一個選取的記錄，則會發生什麼情況，但第二個則失敗，例如外鍵條件約束違規？ 第一筆記錄是否應復原，或第一筆記錄是否可接受刪除？

如果您想要將批次操作視為不可部分完成的[作業，其中](http://en.wikipedia.org/wiki/Atomic_operation)一個步驟成功或所有步驟都失敗，則必須增強資料存取層，以包含[資料庫交易](http://en.wikipedia.org/wiki/Database_transaction)的支援。 資料庫交易保證在交易中執行的一組 `INSERT`、`UPDATE`和 `DELETE` 語句的不可部分完成性，而且是大多數新式資料庫系統都支援的功能。

在本教學課程中，我們將探討如何擴充 DAL 以使用資料庫交易。 後續的教學課程會檢查如何執行批次插入、更新和刪除介面的網頁。 讓我們開始吧！

> [!NOTE]
> 修改批次交易中的資料時，不一定需要不可部分完成性。 在某些情況下，可能可以接受某些資料修改成功，而其他在相同批次中的失敗，例如從 web 電子郵件用戶端刪除一組電子郵件時。 如果在刪除程式中途發生資料庫錯誤，可能就可以接受那些記錄處理完畢，而不會有錯誤地被刪除。 在這種情況下，DAL 不需要修改以支援資料庫交易。 不過，還有其他批次作業案例，其中不可部分完成性十分重要。 當客戶將其資金從一個銀行帳戶移至另一個時，必須執行兩項作業：必須從第一個帳戶扣除資金，然後再新增至第二個帳戶。 雖然銀行可能不會擔心第一個步驟成功，但是第二個步驟會失敗，但其客戶可能會更。 我建議您逐步執行本教學課程，並將 DAL 的增強功能實作為支援資料庫交易的方式，即使您不打算在批次插入、更新和刪除介面中使用它們，我們將在下列三個教學課程中建立。

## <a name="an-overview-of-transactions"></a>交易總覽

大部分的資料庫都包含對*交易*的支援，這可讓多個資料庫命令組成單一工作邏輯單位。 組成交易的資料庫命令保證是不可部分完成的，這表示所有的命令都會失敗，否則全部都會成功。

一般來說，會使用下列模式，透過 SQL 語句來執行交易：

1. 指出交易的開始。
2. 執行組成交易的 SQL 語句。
3. 如果步驟2中的其中一個語句發生錯誤，則回復交易。
4. 如果步驟2中的所有語句都完成但沒有發生錯誤，請認可交易。

在撰寫 SQL 腳本或建立預存程式時，或透過程式設計方式，使用 ADO.NET 或[`System.Transactions` 命名空間](https://msdn.microsoft.com/library/system.transactions.aspx)中的類別，可以手動輸入用來建立、認可和回復交易的 SQL 語句。 在本教學課程中，我們只會檢查使用 ADO.NET 來管理交易。 在未來的教學課程中，我們將探討如何在資料存取層中使用預存程式，而在這段期間，我們將探索用來建立、回復和認可交易的 SQL 語句。 在此同時，請參閱[管理 SQL Server 預存程式中的交易](http://www.4guysfromrolla.com/webtech/080305-1.shtml)，以取得詳細資訊。

> [!NOTE]
> `System.Transactions` 命名空間中的[`TransactionScope` 類別](https://msdn.microsoft.com/library/system.transactions.transactionscope.aspx)，可讓開發人員以程式設計方式將一系列的語句包裝在交易範圍內，並包含涉及多個來源的複雜交易支援，例如兩個不同的資料庫，或甚至是資料存放區的異類類型，例如 Microsoft SQL Server 資料庫、Oracle 資料庫和 Web 服務。 我決定在本教學課程中使用 ADO.NET 交易，而不是 `TransactionScope` 類別，因為 ADO.NET 對於資料庫交易而言較特定，而且在許多情況下，資源密集程度較低。 此外，在某些情況下，`TransactionScope` 類別會使用 Microsoft 分散式交易協調器（MSDTC）。 關於 MSDTC 的設定、執行和效能問題，使其成為特製化和先進的主題，並超越這些教學課程的範圍。

在 ADO.NET 中使用 SqlClient 提供者時，會透過呼叫[`SqlConnection` 類別](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.aspx)s [`BeginTransaction` 方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqlconnection.begintransaction.aspx)來起始交易，這會傳回[`SqlTransaction` 物件](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.aspx)。 構成交易的資料修改語句會放在 `try...catch` 區塊內。 如果 `try` 區塊的語句中發生錯誤，執行會傳送至 `catch` 區塊，其中可以透過 `SqlTransaction` 物件 s [`Rollback` 方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.rollback.aspx)來回複交易。 如果所有語句都順利完成，在 `try` 區塊結尾的 `SqlTransaction` 物件 s [`Commit` 方法](https://msdn.microsoft.com/library/system.data.sqlclient.sqltransaction.commit.aspx)的呼叫會認可交易。 下列程式碼片段說明此模式。 如需其他語法和使用交易搭配 ADO.NET 的範例，請參閱[維護交易的資料庫一致性](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)。

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample1.cs)]

根據預設，具類型資料集中的 Tableadapter 不會使用交易。 為了提供交易支援，我們需要擴充 TableAdapter 類別，以包含其他使用上述模式的方法，在交易範圍內執行一系列的資料修改語句。 在步驟2中，我們將瞭解如何使用部分類別來新增這些方法。

## <a name="step-1-creating-the-working-with-batched-data-web-pages"></a>步驟1：建立使用批次資料網頁

在我們開始探索如何增強 DAL 以支援資料庫交易之前，讓我們先花點時間建立本教學課程所需的 ASP.NET 網頁，以及接下來的三個頁面。 首先，新增名為 `BatchData` 的新資料夾，然後新增下列 ASP.NET 網頁，並將每個頁面與 `Site.master` 主版頁面建立關聯。

- `Default.aspx`
- `Transactions.aspx`
- `BatchUpdate.aspx`
- `BatchDelete.aspx`
- `BatchInsert.aspx`

![新增 SqlDataSource 相關教學課程的 ASP.NET 網頁](wrapping-database-modifications-within-a-transaction-cs/_static/image1.gif)

**圖 1**：新增 SqlDataSource 相關教學課程的 ASP.NET 網頁

如同其他資料夾，`Default.aspx` 將會使用 `SectionLevelTutorialListing.ascx` 使用者控制項來列出其區段內的教學課程。 因此，請將這個使用者控制項加入至 `Default.aspx`，方法是將它從方案總管拖曳至頁面 s 設計檢視。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](wrapping-database-modifications-within-a-transaction-cs/_static/image2.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image1.png)

**圖 2**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](wrapping-database-modifications-within-a-transaction-cs/_static/image2.png)）

最後，將這四個頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，請在自訂網站地圖 `<siteMapNode>`之後，新增下列標記：

[!code-xml[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample2.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含使用批次資料教學課程的專案。

![網站地圖現在包含使用批次資料教學課程的專案](wrapping-database-modifications-within-a-transaction-cs/_static/image3.gif)

**圖 3**：網站地圖現在包含使用批次資料教學課程的專案

## <a name="step-2-updating-the-data-access-layer-to-support-database-transactions"></a>步驟2：更新資料存取層以支援資料庫交易

如我們在第一個教學課程中所討論，[建立資料存取層](../introduction/creating-a-data-access-layer-cs.md)，DAL 中的具類型資料集是由 Datatable 和 tableadapter 所組成。 Datatable 會保存資料，而 Tableadapter 提供將資料庫中的資料讀取至 Datatable 的功能、使用對 Datatable 進行的變更來更新資料庫等等。 回想一下，Tableadapter 提供兩種模式來更新資料，我稱之為批次更新和資料庫直接存取。 使用批次更新模式時，會將資料集、DataTable 或 Datarow 的集合傳遞至 TableAdapter。 會針對每個已插入、已修改或已刪除的資料列，以及執行 `InsertCommand`、`UpdateCommand`或 `DeleteCommand`，來列舉此資料。 使用 DB Direct 模式時，會改為將插入、更新或刪除單一記錄所需的資料行值傳遞給 TableAdapter。 然後，DB 直接模式方法會使用這些傳入的值來執行適當的 `InsertCommand`、`UpdateCommand`或 `DeleteCommand` 語句。

不論使用何種更新模式，Tableadapter 自動產生的方法都不會使用交易。 根據預設，會將 TableAdapter 所執行的每個插入、更新或刪除視為單一的離散運算。 例如，假設在 BLL 中的某些程式碼會使用 DB 直接模式，將10個記錄插入資料庫中。 此程式碼會呼叫 TableAdapter s `Insert` 方法十次。 如果前五個插入成功，而第六個則導致例外狀況，則前五個插入的記錄會保留在資料庫中。 同樣地，如果使用批次更新模式來執行 DataTable 中已插入、已修改和已刪除之資料列的插入、更新和刪除，則如果前幾個修改成功，但後來發生錯誤，則這些先前的修改completed 會保留在資料庫中。

在某些情況下，我們想要確保一系列修改的不可部分完成性。 若要完成這項操作，我們必須在交易的下加入執行 `InsertCommand`、`UpdateCommand`和 `DeleteCommand` 的新方法，以手動擴充 TableAdapter。 在[建立資料存取層](../introduction/creating-a-data-access-layer-cs.md)中，我們探討了如何使用[部分類別](http://en.wikipedia.org/wiki/Partial_type)來擴充具類型資料集內的 datatable 功能。 這項技術也可以與 Tableadapter 搭配使用。

具類型的資料集 `Northwind.xsd` 位於 `App_Code` 資料夾 s `DAL` 子資料夾中。 在名為 `TransactionSupport` 的 `DAL` 資料夾中建立子資料夾，然後新增名為 `ProductsTableAdapter.TransactionSupport.cs` 的新類別檔案（請參閱 [圖 4]）。 這個檔案會保存 `ProductsTableAdapter` 的部分執行，其中包含使用交易來執行資料修改的方法。

![新增名為 TransactionSupport 的資料夾和名為 ProductsTableAdapter.TransactionSupport.cs 的類別檔案](wrapping-database-modifications-within-a-transaction-cs/_static/image4.gif)

**圖 4**：新增名為 `TransactionSupport` 的資料夾和名為的類別檔案 `ProductsTableAdapter.TransactionSupport.cs`

在 `ProductsTableAdapter.TransactionSupport.cs` 檔案中輸入下列程式碼：

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample3.cs)]

此處的類別宣告中的 `partial` 關鍵字，會向編譯器指示在中加入的成員將會加入至 `NorthwindTableAdapters` 命名空間中的 `ProductsTableAdapter` 類別。 請注意檔案頂端的 `using System.Data.SqlClient` 語句。 由於 TableAdapter 已設定為使用 SqlClient 提供者，因此它會在內部使用[`SqlDataAdapter`](https://msdn.microsoft.com/library/system.data.sqlclient.sqldataadapter.aspx)物件，對資料庫發出其命令。 因此，我們必須使用 `SqlTransaction` 類別來開始交易，然後認可它或將其回復。 如果您使用 Microsoft SQL Server 以外的資料存放區，則必須使用適當的提供者。

這些方法提供啟動、復原和認可交易所需的建立區塊。 它們會標示為 `public`，讓它們可以從 `ProductsTableAdapter`、DAL 中的另一個類別，或架構中的另一層（例如 BLL）中使用。 `BeginTransaction` 會開啟 TableAdapter 的內部 `SqlConnection` （如有需要）、開始交易並將它指派給 `Transaction` 屬性，然後將交易附加至內部 `SqlDataAdapter` s `SqlCommand` 物件。 `CommitTransaction` 和 `RollbackTransaction` 在關閉內部 `Rollback` 物件之前，分別呼叫 `Transaction` 物件 s `Commit` 和 `Connection` 方法。

## <a name="step-3-adding-methods-to-update-and-delete-data-under-the-umbrella-of-a-transaction"></a>步驟3：加入方法以更新和刪除交易中的資料

完成這些方法之後，我們就可以開始將方法新增至 `ProductsDataTable` 或 BLL，以在交易的傘下執行一系列的命令。 下列方法會使用批次更新模式來更新使用交易的 `ProductsDataTable` 實例。 它會藉由呼叫 `BeginTransaction` 方法來啟動交易，然後使用 `try...catch` 區塊來發出資料修改語句。 如果對 `Adapter` 物件 `Update` 方法的呼叫導致例外狀況，執行將會傳送至 `catch` 區塊，其中將會回復交易，並重新擲回例外狀況。 回想一下，`Update` 方法會列舉所提供 `ProductsDataTable` 的資料列，並執行必要的 `InsertCommand`、`UpdateCommand`和 `DeleteCommand`，藉此實作為批次更新模式。 如果其中任何一個命令導致錯誤，則會回復交易，並復原先前在交易 s 存留期間所做的修改。 如果 `Update` 語句在沒有錯誤的情況下完成，則會完整認可交易。

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample4.cs)]

透過 `ProductsTableAdapter.TransactionSupport.cs`中的部分類別，將 `UpdateWithTransaction` 方法新增至 `ProductsTableAdapter` 類別。 或者，您也可以將這個方法加入至商務邏輯層 `ProductsBLL` 類別，其中有一些次要的語法變更。 也就是，`this.BeginTransaction()`、`this.CommitTransaction()`和 `this.RollbackTransaction()` 的關鍵字必須以 `Adapter` 取代（請記住，`Adapter` 是類型 `ProductsBLL` 中的屬性名稱 `ProductsTableAdapter`）。

`UpdateWithTransaction` 方法會使用批次更新模式，但是一系列的 DB 直接呼叫也可以在交易的範圍內使用，如下列方法所示。 `DeleteProductsWithTransaction` 方法會接受 `int`類型之 `List<T>` 的輸入，這是要刪除的 `ProductID`。 方法會透過呼叫 `BeginTransaction` 起始交易，然後在 `try` 區塊中，逐一查看針對每個 `ProductID` 值呼叫 DB-Direct 模式 `Delete` 方法的提供清單。 如果任何對 `Delete` 的呼叫失敗，控制權就會傳送至 `catch` 區塊，其中會回復交易並重新擲回例外狀況。 如果 `Delete` 的所有呼叫都成功，則會認可交易。 將此方法新增至 `ProductsBLL` 類別。

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample5.cs)]

## <a name="applying-transactions-across-multiple-tableadapters"></a>跨多個 Tableadapter 套用交易

本教學課程中所檢查的交易相關程式碼允許將 `ProductsTableAdapter` 的多個語句視為不可部分完成的作業。 但是，如果對不同資料庫資料表的多次修改需要以自動方式執行，該怎麼辦？ 例如，刪除類別時，我們可能會先將其目前的產品重新指派給其他類別。 這兩個步驟會重新指派產品，而刪除類別目錄應執行為不可部分完成的作業。 但是 `ProductsTableAdapter` 只包含修改 `Products` 資料表的方法，而 `CategoriesTableAdapter` 只包含修改 `Categories` 資料表的方法。 那麼，交易如何同時包含這兩個 Tableadapter 呢？

其中一個選項是將方法加入至名為 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 的 `CategoriesTableAdapter`，並讓該方法呼叫一個預存程式，這兩個都是重新指派產品，並刪除預存程式內所定義之交易範圍內的類別目錄。 在未來的教學課程中，我們將探討如何在預存程式中開始、認可和回復交易。

另一個選項是在 DAL 中建立包含 `DeleteCategoryAndReassignProducts(categoryIDtoDelete, reassignToCategoryID)` 方法的 helper 類別。 這個方法會建立 `CategoriesTableAdapter` 和 `ProductsTableAdapter` 的實例，然後將這兩個 Tableadapter `Connection` 屬性設定為相同的 `SqlConnection` 實例。 此時，這兩個 Tableadapter 的其中一個會使用 `BeginTransaction`的呼叫來起始交易。 重新指派產品和刪除類別的 Tableadapter 方法會在 `try...catch` 區塊中叫用，並視需要將交易認可或回復。

## <a name="step-4-adding-theupdatewithtransactionmethod-to-the-business-logic-layer"></a>步驟4：將`UpdateWithTransaction`方法加入至商務邏輯層

在步驟3中，我們已將 `UpdateWithTransaction` 方法新增至 DAL 中的 `ProductsTableAdapter`。 我們應該為 BLL 新增對應的方法。 雖然展示層可以直接向下呼叫 DAL 以叫用 `UpdateWithTransaction` 方法，但這些教學課程已嘗試，可定義多層式架構，以將 DAL 與展示層隔離。 因此，它對我們來繼續這種方法。

開啟 `ProductsBLL` 類別檔案，並加入名為 `UpdateWithTransaction` 的方法，只要向下呼叫對應的 DAL 方法即可。 `ProductsBLL`中現在應該有兩個新的方法： `UpdateWithTransaction`（您剛新增的），以及在步驟3中新增的 `DeleteProductsWithTransaction`。

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample6.cs)]

> [!NOTE]
> 這些方法不包含指派給 `ProductsBLL` 類別中大部分其他方法的 `DataObjectMethodAttribute` 屬性，因為我們會直接從 ASP.NET 網頁的程式碼後置類別叫用這些方法。 回想一下，`DataObjectMethodAttribute` 是用來旗標要在 ObjectDataSource 的 [設定資料來源] 中和在哪個索引標籤（SELECT、UPDATE、INSERT 或 DELETE）上出現的方法。 由於 GridView 缺少任何內建的批次編輯或刪除支援，因此我們必須以程式設計方式叫用這些方法，而不是使用無程式碼的宣告式方法。

## <a name="step-5-atomically-updating-database-data-from-the-presentation-layer"></a>步驟5：從展示層自動更新資料庫資料

為了說明交易在更新記錄批次時所產生的效果，請建立一個使用者介面來列出 GridView 中的所有產品，並包含按鈕 Web 控制項，當按下時，會將產品重新指派 `CategoryID` 值。 特別的是，類別重新指派將會進行，因此會為前幾個產品指派一個有效的 `CategoryID` 值，而其他專案則被特意指派不存在的 `CategoryID` 值。 如果我們嘗試以 `CategoryID` 不符合現有分類 `CategoryID`的產品更新資料庫，將會發生 foreign key 條件約束違規，並引發例外狀況。 在此範例中，我們會看到，當使用交易時，外鍵條件約束違規引發的例外狀況將會回復先前的有效 `CategoryID` 變更。 不過，當不使用交易時，將會保留對初始分類的修改。

一開始先開啟 [`BatchData`] 資料夾中的 [`Transactions.aspx`] 頁面，然後從 [工具箱] 將 [GridView] 拖曳至設計工具。 將其 `ID` 設定為 `Products`，並將其從智慧標籤系結至名為 `ProductsDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以從 `ProductsBLL` 類別的 `GetProducts` 方法提取其資料。 這會是唯讀 GridView，因此，請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]，然後按一下 [完成]。

[![圖5：將 ObjectDataSource 設定為使用 ProductsBLL 類別的 GetProducts 方法](wrapping-database-modifications-within-a-transaction-cs/_static/image5.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image3.png)

**圖 5**：圖5：設定 ObjectDataSource 使用 `ProductsBLL` 類別的 `GetProducts` 方法（[按一下以查看完整大小的影像](wrapping-database-modifications-within-a-transaction-cs/_static/image4.png)）

[![將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](wrapping-database-modifications-within-a-transaction-cs/_static/image6.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image5.png)

**圖 6**：將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](wrapping-database-modifications-within-a-transaction-cs/_static/image6.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 將會建立 [產品資料] 欄位的 BoundFields 和 CheckBoxField。 除了 [`ProductID`]、[`ProductName`]、[`CategoryID`] 和 [`CategoryName`] 之外，移除所有這些欄位，並分別將 `ProductName` 和 `CategoryName` BoundFields `HeaderText` 屬性重新命名為 [產品] 和 [類別]。 從智慧標籤中，勾選 [啟用分頁] 選項。 進行這些修改之後，GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample7.aspx)]

接下來，在 GridView 上方加入三個按鈕 Web 控制項。 將第一個按鈕的 Text 屬性設定為 [重新整理方格]，第二個則會修改類別目錄（含交易），而第三個則會修改類別目錄（不含交易）。

[!code-aspx[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample8.aspx)]

此時，Visual Studio 中的設計檢視看起來應該像 [圖 7] 所示的螢幕擷取畫面。

[![頁面包含 GridView 和三個按鈕的 Web 控制項](wrapping-database-modifications-within-a-transaction-cs/_static/image7.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image7.png)

**圖 7**：此頁面包含 GridView 和三個按鈕的 Web 控制項（[按一下以觀看完整大小的影像](wrapping-database-modifications-within-a-transaction-cs/_static/image8.png)）

為三個按鈕 `Click` 事件的每一個建立事件處理常式，並使用下列程式碼：

[!code-csharp[Main](wrapping-database-modifications-within-a-transaction-cs/samples/sample9.cs)]

[重新整理] 按鈕 `Click` 事件處理常式會藉由呼叫 `Products` GridView s `DataBind` 方法，直接將資料重新系結至 GridView。

第二個事件處理常式會將產品重新指派 `CategoryID` s，並使用來自 BLL 的新交易方法，在交易的傘之下執行資料庫更新。 請注意，每個產品的 `CategoryID` 會任意設定為與其 `ProductID`相同的值。 這會在前幾個產品中正常執行，因為這些產品具有對應到有效 `CategoryID` 的 `ProductID` 值。 但是一旦 `ProductID` 開始變得太大，此純屬巧合就會重迭 `ProductID` s，而 `CategoryID` s 則不再適用。

第三個 `Click` 事件處理常式會以相同的方式更新中的產品 `CategoryID`，但會使用 `ProductsTableAdapter` 的預設 `Update` 方法，將更新傳送至資料庫。 這個 `Update` 方法不會在交易內包裝一系列的命令，因此，在第一次遇到外鍵條件約束違規錯誤之前，會持續進行這些變更。

若要示範此行為，請透過瀏覽器造訪此頁面。 一開始，您應該會看到資料的第一頁，如 [圖 8] 所示。 接下來，按一下 [修改類別目錄（使用交易）] 按鈕。 這會導致回傳並嘗試更新 `CategoryID` 值的所有產品，但會導致外鍵條件約束違規（請參閱 [圖 9]）。

[![產品會顯示在可分頁的 GridView 中](wrapping-database-modifications-within-a-transaction-cs/_static/image8.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image9.png)

**圖 8**：產品會顯示在可分頁的 GridView 中（[按一下以查看完整大小的影像](wrapping-database-modifications-within-a-transaction-cs/_static/image10.png)）

[![重新指派分類會導致 Foreign Key 條件約束違規](wrapping-database-modifications-within-a-transaction-cs/_static/image9.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image11.png)

**圖 9**：重新指派分類會導致外鍵條件約束違規（[按一下以查看完整大小的影像](wrapping-database-modifications-within-a-transaction-cs/_static/image12.png)）

現在按一下瀏覽器的 [上一頁] 按鈕，然後按一下 [重新整理格線] 按鈕。 重新整理資料時，您應該會看到完全相同的輸出，如 [圖 8] 所示。 也就是說，即使某些產品 `CategoryID` 已變更為合法值，並在資料庫中更新，當外鍵條件約束違規發生時，它們也會回復。

現在，請嘗試按一下 [修改類別目錄（不含交易）] 按鈕。 這會導致相同的外鍵條件約束違規錯誤（請參閱 [圖 9]），但這次 `CategoryID` 值已變更為合法值的產品將不會回復。 按瀏覽器的 [上一頁] 按鈕，然後按 [重新整理格線] 按鈕。 如 [圖 10] 所示，前八個產品的 `CategoryID` 已經重新指派。 例如，在 [圖 8] 中，變更的 `CategoryID` 是1，但在 [圖 10] 中，它已重新指派給2。

[![某些產品的 [類別] 值已更新，但有些則不是](wrapping-database-modifications-within-a-transaction-cs/_static/image10.gif)](wrapping-database-modifications-within-a-transaction-cs/_static/image13.png)

**圖 10**：某些產品 `CategoryID` 值已更新，有些則不是（[按一下以觀看完整大小的影像](wrapping-database-modifications-within-a-transaction-cs/_static/image14.png)）

## <a name="summary"></a>總結

根據預設，TableAdapter s 方法不會在交易範圍內包裝已執行的資料庫語句，但是只要花一些工作，我們就可以加入方法來建立、認可和復原交易。 在本教學課程中，我們已在 `ProductsTableAdapter` 類別中建立三種這類方法： `BeginTransaction`、`CommitTransaction`和 `RollbackTransaction`。 我們已瞭解如何搭配使用這些方法與 `try...catch` 區塊，讓一系列的資料修改語句變成不可部分完成。 特別是，我們已在 `ProductsTableAdapter`中建立 `UpdateWithTransaction` 方法，這會使用批次更新模式來對所提供 `ProductsDataTable`的資料列執行必要的修改。 我們也將 `DeleteProductsWithTransaction` 方法新增到 BLL 中的 `ProductsBLL` 類別，這會接受 `ProductID` 值的 `List` 作為其輸入，並針對每個 `Delete` 呼叫 DB 直接模式方法 `ProductID`。 這兩種方法一開始先建立交易，然後在 `try...catch` 區塊內執行資料修改語句。 如果發生例外狀況，則會回復交易，否則會進行認可。

步驟5說明交易式批次更新的效果，與忽略使用交易的批次更新。 在接下來的三個教學課程中，我們將根據本教學課程中所述的基礎，建立用於執行批次更新、刪除和插入的使用者介面。

快樂的程式設計！

## <a name="further-reading"></a>進一步閱讀

如需本教學課程中所討論之主題的詳細資訊，請參閱下列資源：

- [維護交易的資料庫一致性](http://aspnet.4guysfromrolla.com/articles/072705-1.aspx)
- [管理 SQL Server 預存程式中的交易](http://www.4guysfromrolla.com/webtech/080305-1.shtml)
- [交易變得簡單： `System.Transactions`](https://blogs.msdn.com/florinlazar/archive/2004/07/23/192239.aspx)
- [TransactionScope 和 Dataadapter](http://andyclymer.blogspot.com/2007/01/transactionscope-and-dataadapters.html)
- [在 .NET 中使用 Oracle Database 的交易](http://www.oracle.com/technology/pub/articles/price_dbtrans_dotnet.html)

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Dave Gardner、Hilton Giesenow 和 Teresa Murphy。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [下一步](batch-updating-cs.md)
