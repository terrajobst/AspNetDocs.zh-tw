---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb
title: 執行開放式平行存取（VB） |Microsoft Docs
author: rick-anderson
description: 對於允許多位使用者編輯資料的 web 應用程式，有兩位使用者可能同時編輯相同資料的風險。 在此 tutori 中 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 2646968c-2826-4418-b1d0-62610ed177e3
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/implementing-optimistic-concurrency-vb
msc.type: authoredcontent
ms.openlocfilehash: 28c39fe2a290cc3a5b093fdd09de341630606137
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78607909"
---
# <a name="implementing-optimistic-concurrency-vb"></a>實作開放式同步存取 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_21_VB.exe)或[下載 PDF](implementing-optimistic-concurrency-vb/_static/datatutorial21vb1.pdf)

> 對於允許多位使用者編輯資料的 web 應用程式，有兩位使用者可能同時編輯相同資料的風險。 在本教學課程中，我們將會實行開放式並行存取控制來處理這項風險。

## <a name="introduction"></a>簡介

對於只允許使用者查看資料的 web 應用程式，或僅包含可修改資料之單一使用者的 web 應用程式，不會有兩個並行使用者意外覆寫另一個變更的威脅。 不過，對於允許多個使用者更新或刪除資料的 web 應用程式，可能會有一位使用者修改與另一位並行使用者的衝突。 如果沒有任何並行原則，當兩個使用者同時編輯單一記錄時，認可其變更的使用者將會覆寫第一個所做的變更。

例如，假設有兩個使用者（Jisun 和 Sam）同時造訪應用程式中的網頁，讓訪客能夠透過 GridView 控制項更新和刪除產品。 同時按一下 GridView 前後的 [編輯] 按鈕。 Jisun 會將產品名稱變更為「Chai 茶」，並按一下 [更新] 按鈕。 最終結果是傳送到資料庫的 `UPDATE` 語句，它會設定*所有*產品的可更新欄位（即使 Jisun 只更新一個欄位，`ProductName`）。 在此時間點，資料庫的值為「Chai 茶」、「飲料」、「供應商外來液體等等，這是此特定產品。 不過，Sam 的螢幕上的 GridView 仍然會在可編輯的 GridView 資料列中，將產品名稱顯示為 "Chai"。 認可 Jisun 變更後的幾秒後，Sam 會將類別更新為 Condiments，然後按一下 [更新]。 這會導致 `UPDATE` 語句傳送到資料庫，將產品名稱設定為 "Chai"，`CategoryID` 對應的飲料分類識別碼等等。 已覆寫 Jisun 對產品名稱所做的變更。 [圖 1] 以圖形方式描繪這一系列的事件。

[![當兩個使用者同時更新記錄時，有一位使用者的變更可能會覆寫其他人的](implementing-optimistic-concurrency-vb/_static/image2.png)](implementing-optimistic-concurrency-vb/_static/image1.png)

**圖 1**：當兩個使用者同時更新記錄時，有一位使用者的變更可能會覆寫其他人（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image3.png)）

同樣地，當兩位使用者流覽頁面時，如果有其他使用者刪除記錄，則可能會有一位使用者在進行更新。 或者，當使用者載入頁面，而當他們按一下 [刪除] 按鈕時，另一位使用者可能已修改該記錄的內容。

有三個可用的[並行控制](http://en.wikipedia.org/wiki/Concurrency_control)策略：

- **不執行任何動作**-如果並行使用者正在修改相同的記錄，請讓最後一個認可獲勝（預設行為）
- [**開放式並行**](http://en.wikipedia.org/wiki/Optimistic_concurrency_control)存取-假設在每次可能會發生並行衝突，而大部分的時間都不會發生。因此，如果發生衝突，只要通知使用者他們的變更無法儲存，因為另一個使用者已修改相同的資料
- 封閉式**並行**存取-假設並行衝突很常見，而且使用者不會被告知他們的變更因其他使用者的並行活動而未儲存;因此，當某位使用者開始更新記錄時，請將它鎖定，藉此防止任何其他使用者編輯或刪除該記錄，直到使用者認可其修改為止

到目前為止，我們所有的教學課程都已使用預設的並行解析策略，也就是我們讓最後的寫入獲勝。 在本教學課程中，我們將探討如何執行開放式並行存取控制。

> [!NOTE]
> 我們不會在本教學課程系列中探討封閉式並行範例。 不常使用封閉式平行存取，因為這類鎖定（如果未正確釋放）可能會防止其他使用者更新資料。 例如，如果使用者鎖定記錄進行編輯，然後在解除鎖定前保留一天，則在原始使用者傳回並完成其更新之前，其他使用者都無法更新該記錄。 因此，在使用封閉式平行存取的情況下，通常會有一個超時時間，如果達到，則會取消鎖定。 「票證銷售網站」會在使用者完成訂單程式時，鎖定特定的座位位置，這是封閉式並行存取控制的範例。

## <a name="step-1-looking-at-how-optimistic-concurrency-is-implemented"></a>步驟1：查看開放式平行存取的執行方式

開放式並行存取控制的運作方式是確保更新或刪除的記錄具有與更新或刪除進程啟動時相同的值。 例如，按一下可編輯之 GridView 中的 [編輯] 按鈕時，會從資料庫讀取記錄的值，並顯示在文字方塊和其他 Web 控制項中。 這些原始值是由 GridView 儲存。 之後，在使用者進行變更並按一下 [更新] 按鈕之後，原始值加上新的值就會傳送到商務邏輯層，然後再向下到資料存取層。 資料存取層必須發出 SQL 語句，只有在使用者開始編輯的原始值與仍在資料庫中的值相同時，才會更新記錄。 [圖 2] 描繪了這一系列的事件。

[若要成功更新或刪除 ![，原始值必須等於目前的資料庫值](implementing-optimistic-concurrency-vb/_static/image5.png)](implementing-optimistic-concurrency-vb/_static/image4.png)

**圖 2**：若要讓 Update 或 Delete 成功，原始值必須等於目前的資料庫值（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image6.png)）

有各種方法可以執行開放式平行存取（請參閱[Peter A. Bromberg](http://peterbromberg.net/)的[開放式平行存取邏輯](http://www.eggheadcafe.com/articles/20050719.asp)，以瞭解一些選項）。 ADO.NET 具類型資料集提供一個可以只以核取方塊的滴答來設定的實作為。 針對具類型資料集中的 TableAdapter 啟用開放式平行存取，會增強 TableAdapter 的 `UPDATE` 和 `DELETE` 語句，以包含 `WHERE` 子句中所有原始值的比較。 例如，如果目前的資料庫值等於在 GridView 中更新記錄時原先抓取的值，則下列 `UPDATE` 語句會更新產品的名稱和價格。 `@ProductName` 和 `@UnitPrice` 參數包含使用者輸入的新值，而 `@original_ProductName` 和 `@original_UnitPrice` 包含在按下 [編輯] 按鈕時，原先載入至 GridView 的值：

[!code-sql[Main](implementing-optimistic-concurrency-vb/samples/sample1.sql)]

> [!NOTE]
> 為了方便閱讀，已簡化此 `UPDATE` 語句。 實際上，`WHERE` 子句中的 `UnitPrice` 檢查會比較複雜，因為 `UnitPrice` 可以包含 `NULL` s，並檢查 `NULL = NULL` 是否一律傳回 False （相反地，您必須使用 `IS NULL`）。

除了使用不同的基礎 `UPDATE` 語句外，將 TableAdapter 設定為使用開放式平行存取也會修改其 DB 直接方法的簽章。 回想一下我們的第一個教學課程：[*建立資料存取層*](../introduction/creating-a-data-access-layer-cs.md)，該 DB 直接方法就是接受純量值清單做為輸入參數（而不是強型別 DataRow 或 DataTable 實例）的方式。 使用開放式平行存取時，DB direct `Update()` 和 `Delete()` 方法也會包含原始值的輸入參數。 此外，使用批次更新模式的 BLL 中的程式碼（`Update()` 接受 Datarow 和 Datatable 的方法多載，而不是純量值）也必須變更。

我們會改為建立一個名為 `NorthwindOptimisticConcurrency`的新型別資料集，並在其中新增使用開放式平行存取的 `Products` TableAdapter，而不是擴充現有 DAL 的 Tableadapter 來使用開放式平行存取（這會需要變更 BLL 以配合）。 之後，我們將建立一個 `ProductsOptimisticConcurrencyBLL` 的商務邏輯層級類別，其中具有適當的修改可支援開放式平行存取 DAL。 一旦這是基礎，我們就準備好建立 ASP.NET 網頁。

## <a name="step-2-creating-a-data-access-layer-that-supports-optimistic-concurrency"></a>步驟2：建立支援開放式平行存取的資料存取層

若要建立新的具類型資料集，請以滑鼠右鍵按一下 [`App_Code`] 資料夾內的 [`DAL`] 資料夾，然後加入名為 `NorthwindOptimisticConcurrency`的新資料集。 如我們在第一個教學課程中所見，這麼做會將新的 TableAdapter 新增至具類型的資料集，並自動啟動 TableAdapter 設定 Wizard。 在第一個畫面中，系統會提示您指定要連接的資料庫-使用 `Web.config`的 [`NORTHWNDConnectionString`] 設定連接到相同的 Northwind 資料庫。

[![連接到相同的 Northwind 資料庫](implementing-optimistic-concurrency-vb/_static/image8.png)](implementing-optimistic-concurrency-vb/_static/image7.png)

**圖 3**：連接到相同的 Northwind 資料庫（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image9.png)）

接下來，系統會提示您如何查詢資料：透過特定 SQL 語句、新的預存程式或現有的預存程式。 因為我們在原始 DAL 中使用臨機操作 SQL 查詢，所以也請在這裡使用此選項。

[![使用臨機操作 SQL 語句來指定要取出的資料](implementing-optimistic-concurrency-vb/_static/image11.png)](implementing-optimistic-concurrency-vb/_static/image10.png)

**圖 4**：使用臨機操作 SQL 語句指定要抓取的資料（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image12.png)）

在下列畫面上，輸入要用來取出產品資訊的 SQL 查詢。 讓我們使用與原始 DAL 中的 `Products` TableAdapter 完全相同的 SQL 查詢，這會傳回所有 `Product` 資料行以及產品的供應商和類別目錄名稱：

[!code-sql[Main](implementing-optimistic-concurrency-vb/samples/sample2.sql)]

[![從原始 DAL 中的產品 TableAdapter 使用相同的 SQL 查詢](implementing-optimistic-concurrency-vb/_static/image14.png)](implementing-optimistic-concurrency-vb/_static/image13.png)

**圖 5**：從原始 DAL 中的 `Products` TableAdapter 使用相同的 SQL 查詢（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image15.png)）

在移至下一個畫面之前，請按一下 [Advanced Options] 按鈕。 若要讓此 TableAdapter 採用開放式並行存取控制，只要勾選 [使用開放式平行存取] 核取方塊即可。

[藉由檢查 &quot;使用開放式平行存取&quot; 核取方塊，![啟用開放式並行存取控制](implementing-optimistic-concurrency-vb/_static/image17.png)](implementing-optimistic-concurrency-vb/_static/image16.png)

**圖 6**：藉由勾選 [使用開放式平行存取] 核取方塊來啟用開放式並行存取控制（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image18.png)）

最後，指出 TableAdapter 應該使用同時填滿 DataTable 並傳回 DataTable 的資料存取模式。也表示應該建立 DB 直接方法。 將的方法名稱變更為將 DataTable 模式從，傳回至 GetProducts，以便鏡像我們在原始 DAL 中使用的命名慣例。

[![讓 TableAdapter 利用所有資料存取模式](implementing-optimistic-concurrency-vb/_static/image20.png)](implementing-optimistic-concurrency-vb/_static/image19.png)

**圖 7**：讓 TableAdapter 利用所有資料存取模式（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image21.png)）

完成 wizard 之後，DataSet 設計工具會包含強型別 `Products` DataTable 和 TableAdapter。 請花點時間將 DataTable 從 `Products` 重新命名為 `ProductsOptimisticConcurrency`，您可以在 DataTable 的標題列上按一下滑鼠右鍵，然後從內容功能表中選擇 [重新命名]，來執行此動作。

[![DataTable 和 TableAdapter 已加入至具類型的資料集](implementing-optimistic-concurrency-vb/_static/image23.png)](implementing-optimistic-concurrency-vb/_static/image22.png)

**圖 8**： DataTable 和 TableAdapter 已加入至具類型的資料集（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image24.png)）

若要查看 `ProductsOptimisticConcurrency` TableAdapter （使用開放式平行存取）和產品 TableAdapter （不是）之間的 `UPDATE` 和 `DELETE` 查詢之間的差異，請按一下 [TableAdapter]，然後移至 [屬性視窗]。 在 [`DeleteCommand`] 和 [`UpdateCommand` 屬性] 的 [`CommandText` 子屬性] 中，您可以看到在叫用 DAL 的更新或刪除相關方法時，傳送至資料庫的實際 SQL 語法。 針對 `ProductsOptimisticConcurrency` TableAdapter，使用的 `DELETE` 語句是：

[!code-sql[Main](implementing-optimistic-concurrency-vb/samples/sample3.sql)]

而在原始 DAL 中，產品 TableAdapter 的 `DELETE` 語句是更簡單的：

[!code-sql[Main](implementing-optimistic-concurrency-vb/samples/sample4.sql)]

如您所見，使用開放式平行存取之 TableAdapter 的 `DELETE` 語句中的 `WHERE` 子句，包括每個 `Product` 資料表的現有資料行值與上一次填入 GridView （或 DetailsView 或 FormView）時的原始值之間的比較。 由於 `ProductID`、`ProductName`和 `Discontinued` 以外的所有欄位都可以有 `NULL` 值，因此會包含額外的參數和檢查，以正確比較 `NULL` 子句中 `WHERE` 的值。

在本教學課程中，我們不會將任何額外的 Datatable 新增至開放式啟用平行存取的資料集，因為我們的 ASP.NET 網頁只會提供更新和刪除產品資訊。 不過，我們仍然需要將 `GetProductByProductID(productID)` 方法新增至 `ProductsOptimisticConcurrency` TableAdapter。

若要完成此動作，請以滑鼠右鍵按一下 TableAdapter 的標題列（`Fill` 上方的區域並 `GetProducts` 方法名稱），然後從內容功能表選擇 [加入查詢]。 這會啟動 [TableAdapter 查詢設定] Wizard。 如同我們的 TableAdapter 初始設定，您可以選擇使用臨機操作 SQL 語句來建立 `GetProductByProductID(productID)` 方法（請參閱 [圖 4]）。 因為 `GetProductByProductID(productID)` 方法會傳回特定產品的相關資訊，表示此查詢是傳回資料列的 `SELECT` 查詢類型。

[![將查詢類型標記為 &quot;SELECT，這會傳回資料列&quot;](implementing-optimistic-concurrency-vb/_static/image26.png)](implementing-optimistic-concurrency-vb/_static/image25.png)

**圖 9**：將查詢類型標記為「`SELECT` 傳回資料列」（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image27.png)）

在下一個畫面中，我們會提示您提供要使用的 SQL 查詢，並預先載入 TableAdapter 的預設查詢。 擴大現有的查詢，以包含子句 `WHERE ProductID = @ProductID`，如 [圖 10] 所示。

[![將 WHERE 子句加入預先載入的查詢，以傳回特定的產品記錄](implementing-optimistic-concurrency-vb/_static/image29.png)](implementing-optimistic-concurrency-vb/_static/image28.png)

**圖 10**：將 `WHERE` 子句新增至預先載入的查詢，以傳回特定的產品記錄（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image30.png)）

最後，將產生的方法名稱變更為 `FillByProductID` 並 `GetProductByProductID`。

[![將方法重新命名為 FillByProductID 和 GetProductByProductID](implementing-optimistic-concurrency-vb/_static/image32.png)](implementing-optimistic-concurrency-vb/_static/image31.png)

**圖 11**：將方法重新命名為 `FillByProductID` 和 `GetProductByProductID` （[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image33.png)）

完成此嚮導之後，TableAdapter 現在會包含兩個用來抓取資料的方法： `GetProducts()`，它會傳回*所有*產品;和 `GetProductByProductID(productID)`，它會傳回指定的產品。

## <a name="step-3-creating-a-business-logic-layer-for-the-optimistic-concurrency-enabled-dal"></a>步驟3：為開放式平行存取啟用的 DAL 建立商務邏輯層

我們現有的 `ProductsBLL` 類別具有同時使用批次更新和 DB 直接模式的範例。 `AddProduct` 方法和 `UpdateProduct` 多載都會使用批次更新模式，並將 `ProductRow` 實例傳入 TableAdapter 的 Update 方法。 另一方面，`DeleteProduct` 方法會使用資料庫直接模式，呼叫 TableAdapter 的 `Delete(productID)` 方法。

有了新的 `ProductsOptimisticConcurrency` TableAdapter，DB 直接方法現在也需要傳入原始值。 例如，`Delete` 方法現在需要10個輸入參數：原始 `ProductID`、`ProductName`、`SupplierID`、`CategoryID`、`QuantityPerUnit`、`UnitPrice`、`UnitsInStock`、`UnitsOnOrder`、`ReorderLevel`和 `Discontinued`。 它會在傳送至資料庫之 `DELETE` 語句的 `WHERE` 子句中使用這些額外的輸入參數值，只有在資料庫目前的值對應到原始的值時，才會刪除指定的記錄。

雖然用於批次更新模式之 TableAdapter `Update` 方法的方法簽章未變更，但記錄原始和新值所需的程式碼具有。 因此，讓我們建立新的商務邏輯層級，以使用新的 DAL，而不是嘗試將開放式平行存取的 DAL 用於現有的 `ProductsBLL` 類別。

將名為 `ProductsOptimisticConcurrencyBLL` 的類別新增至 [`App_Code`] 資料夾內的 [`BLL`] 資料夾。

![將 ProductsOptimisticConcurrencyBLL 類別新增至 BLL 資料夾](implementing-optimistic-concurrency-vb/_static/image34.png)

**圖 12**：將 `ProductsOptimisticConcurrencyBLL` 類別新增到 BLL 資料夾

接下來，將下列程式碼新增至 `ProductsOptimisticConcurrencyBLL` 類別：

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample5.vb)]

請注意，在類別宣告的開頭使用 `NorthwindOptimisticConcurrencyTableAdapters` 語句。 `NorthwindOptimisticConcurrencyTableAdapters` 命名空間包含 `ProductsOptimisticConcurrencyTableAdapter` 類別，它會提供 DAL 的方法。 此外，在類別宣告之前，您會發現 `System.ComponentModel.DataObject` 屬性，它會指示 Visual Studio 在 ObjectDataSource wizard 的下拉式清單中包含此類別。

`ProductsOptimisticConcurrencyBLL`的 `Adapter` 屬性可讓您快速存取 `ProductsOptimisticConcurrencyTableAdapter` 類別的實例，並遵循原始 BLL 類別（`ProductsBLL`、`CategoriesBLL`等等）中使用的模式。 最後，`GetProducts()` 方法只會向下呼叫 DAL 的 `GetProducts()` 方法，並傳回針對資料庫中的每個產品記錄，填入 `ProductsOptimisticConcurrencyRow` 實例的 `ProductsOptimisticConcurrencyDataTable` 物件。

## <a name="deleting-a-product-using-the-db-direct-pattern-with-optimistic-concurrency"></a>使用資料庫直接模式與開放式平行存取來刪除產品

針對使用開放式平行存取的 DAL 使用 DB direct 模式時，必須將新的和原始值傳遞給這些方法。 若要刪除，則不會有任何新的值，因此只需要傳入原始值。 在 BLL 中，我們必須接受所有原始參數做為輸入參數。 讓我們在 `ProductsOptimisticConcurrencyBLL` 類別中的 `DeleteProduct` 方法使用 DB 直接方法。 這表示此方法需要將所有十個產品資料欄位當做輸入參數，並將其傳遞給 DAL，如下列程式碼所示：

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample6.vb)]

如果原始值-最後載入 GridView （或 DetailsView 或 FormView）中的值，當使用者按一下 [刪除] 按鈕時，就會與資料庫中的值不同，`WHERE` 子句不會與任何資料庫記錄相符，而且不會影響任何記錄。 因此，TableAdapter 的 `Delete` 方法會傳回 `0`，而 BLL 的 `DeleteProduct` 方法將會傳回 `false`。

## <a name="updating-a-product-using-the-batch-update-pattern-with-optimistic-concurrency"></a>使用批次更新模式與開放式平行存取來更新產品

如先前所述，不論是否採用開放式平行存取，適用于批次更新模式的 TableAdapter `Update` 方法都會有相同的方法簽章。 也就是說，`Update` 方法需要 DataRow、Datarow 陣列、DataTable 或具類型資料集。 沒有其他輸入參數可用於指定原始值。 這是可能的，因為 DataTable 會追蹤其 DataRow 的原始和修改值。 當 DAL 發出其 `UPDATE` 語句時，`@original_ColumnName` 參數會填入 DataRow 的原始值，而 `@ColumnName` 參數則會填入 DataRow 的修改值。

在 `ProductsBLL` 類別（使用我們的原始非開放式平行存取 DAL）中，當使用批次更新模式來更新產品資訊時，我們的程式碼會執行下列一連串的事件：

1. 使用 TableAdapter 的 `GetProductByProductID(productID)` 方法，將目前的資料庫產品資訊讀入 `ProductRow` 實例
2. 將新值指派給步驟1中的 `ProductRow` 實例
3. 呼叫 TableAdapter 的 `Update` 方法，傳入 `ProductRow` 實例

不過，這一系列的步驟將不會正確支援開放式平行存取，因為在步驟1中填入的 `ProductRow` 會直接從資料庫填入，這表示 DataRow 所使用的原始值是目前存在於資料庫中，而不是在編輯程式開始時系結至 GridView 的資料。 相反地，在使用開放式平行存取的 DAL 時，我們需要改變 `UpdateProduct` 方法多載，以使用下列步驟：

1. 使用 TableAdapter 的 `GetProductByProductID(productID)` 方法，將目前的資料庫產品資訊讀入 `ProductsOptimisticConcurrencyRow` 實例
2. 將*原始*值指派給步驟1中的 `ProductsOptimisticConcurrencyRow` 實例
3. 呼叫 `ProductsOptimisticConcurrencyRow` 實例的 `AcceptChanges()` 方法，指示 DataRow 其目前的值為「原始」
4. 將*新*值指派給 `ProductsOptimisticConcurrencyRow` 實例
5. 呼叫 TableAdapter 的 `Update` 方法，傳入 `ProductsOptimisticConcurrencyRow` 實例

步驟1會針對指定的產品記錄，讀取所有目前的資料庫值。 這個步驟在 `UpdateProduct` 多載中是多餘的，會更新*所有*的產品資料行（因為在步驟2中會覆寫這些值），但對於那些只將資料行值子集當做輸入參數傳入的多載而言，是不可或缺的。 將原始值指派給 `ProductsOptimisticConcurrencyRow` 實例之後，就會呼叫 `AcceptChanges()` 方法，這會將目前的 DataRow 值標示為要在 `UPDATE` 語句的 `@original_ColumnName` 參數中使用的原始值。 接下來，新的參數值會指派給 `ProductsOptimisticConcurrencyRow`，最後，會叫用 `Update` 方法，並傳入 DataRow。

下列程式碼顯示接受所有產品資料欄位做為輸入參數的 `UpdateProduct` 多載。 雖然此處未顯示，但本教學課程的下載中所包含的 `ProductsOptimisticConcurrencyBLL` 類別也包含 `UpdateProduct` 多載，只接受產品的名稱和價格做為輸入參數。

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample7.vb)]

## <a name="step-4-passing-the-original-and-new-values-from-the-aspnet-page-to-the-bll-methods"></a>步驟4：將 ASP.NET 網頁中的原始和新值傳遞給 BLL 方法

當 DAL 和 BLL 完成後，剩下的工作就是建立一個 ASP.NET 網頁，它可以利用內建在系統中的開放式平行存取邏輯。 具體而言，資料 Web 控制項（GridView、DetailsView 或 FormView）必須記住其原始值，而 ObjectDataSource 必須將這兩組值傳遞給商務邏輯層。 此外，ASP.NET 網頁必須設定為適當地處理並行違規。

一開始先開啟 [`EditInsertDelete`] 資料夾中的 [`OptimisticConcurrency.aspx`] 頁面，並將 GridView 新增至設計工具，將其 `ID` 屬性設定為 [`ProductsGrid`]。 從 GridView 的智慧標籤中，選擇建立名為 `ProductsOptimisticConcurrencyDataSource`的新 ObjectDataSource。 因為我們想要讓此 ObjectDataSource 使用支援開放式平行存取的 DAL，請將它設定為使用 `ProductsOptimisticConcurrencyBLL` 物件。

[![讓 ObjectDataSource 使用 ProductsOptimisticConcurrencyBLL 物件](implementing-optimistic-concurrency-vb/_static/image36.png)](implementing-optimistic-concurrency-vb/_static/image35.png)

**圖 13**：讓 ObjectDataSource 使用 `ProductsOptimisticConcurrencyBLL` 物件（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image37.png)）

從 wizard 的下拉式清單中選擇 [`GetProducts`]、[`UpdateProduct`] 和 [`DeleteProduct`] 方法。 針對 UpdateProduct 方法，使用接受所有產品資料欄位的多載。

## <a name="configuring-the-objectdatasource-controls-properties"></a>設定 ObjectDataSource 控制項的屬性

完成 wizard 之後，ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample8.aspx)]

如您所見，`DeleteParameters` 集合在 `ProductsOptimisticConcurrencyBLL` 類別的 `DeleteProduct` 方法中，包含10個輸入參數的 `Parameter` 實例。 同樣地，`UpdateParameters` 集合會針對 `UpdateProduct`中的每個輸入參數包含 `Parameter` 實例。

對於牽涉到資料修改的前述教學課程，我們會在此時移除 ObjectDataSource 的 `OldValuesParameterFormatString` 屬性，因為此屬性指出 BLL 方法預期會傳入舊的（或原始）值，以及新的值。 此外，此屬性值也會指出原始值的輸入參數名稱。 因為我們會將原始值傳入 BLL，*請勿移除此*屬性。

> [!NOTE]
> `OldValuesParameterFormatString` 屬性的值必須對應到需要原始值之 BLL 中的輸入參數名稱。 因為我們將這些參數命名 `original_productName`、`original_supplierID`等等，所以您可以將 `OldValuesParameterFormatString` 屬性值保留為 `original_{0}`。 不過，如果 BLL 方法的輸入參數具有如 `old_productName`、`old_supplierID`等等的名稱，您就必須將 `OldValuesParameterFormatString` 屬性更新為 `old_{0}`。

有一個最後的屬性設定需要進行，才能讓 ObjectDataSource 正確地將原始值傳遞給 BLL 方法。 ObjectDataSource 具有[ConflictDetection 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.conflictdetection.aspx)，可指派給[兩個值的其中一個](https://msdn.microsoft.com/library/system.web.ui.conflictoptions.aspx)：

- `OverwriteChanges`-預設值;不會將原始值傳送給 BLL 方法的原始輸入參數
- `CompareAllValues`-會將原始值傳送給 BLL 方法;使用開放式平行存取時，請選擇此選項

請花點時間將 `ConflictDetection` 屬性設為 `CompareAllValues`。

## <a name="configuring-the-gridviews-properties-and-fields"></a>設定 GridView 的屬性和欄位

已正確設定 ObjectDataSource 的屬性後，讓我們將注意力轉變成設定 GridView。 首先，因為我們想要 GridView 支援編輯和刪除，請按一下 [啟用編輯]，然後從 GridView 的智慧標籤中啟用 [刪除] 核取方塊。 這會加入 CommandField，其 `ShowEditButton` 和 `ShowDeleteButton` 皆設定為 `true`。

當系結至 `ProductsOptimisticConcurrencyDataSource` ObjectDataSource 時，GridView 會針對每個產品的資料欄位包含一個欄位。 雖然這種 GridView 可以進行編輯，但使用者體驗卻是可接受的。 `CategoryID` 和 `SupplierID` BoundFields 會轉譯成文字方塊，要求使用者輸入適當的類別和供應商做為識別碼編號。 數值欄位不會有任何格式，而且沒有驗證控制項可確保已提供產品的名稱，而且單價、庫存單位、依訂單的單位和重新排序層級值都是正確的數值，而且大於或等於為零。

如我們在將*驗證控制項新增至編輯和插入介面*和*自訂資料修改介面*教學課程中所述，您可以使用 TemplateFields 取代 BoundFields 來自訂使用者介面。 我已經用下列方式修改了這個 GridView 和其編輯介面：

- 已移除 `ProductID`、`SupplierName`和 `CategoryName` BoundFields
- 將 `ProductName` BoundField 轉換成 TemplateField，並新增 RequiredFieldValidation 控制項。
- 將 `CategoryID` 和 `SupplierID` BoundFields 轉換為 TemplateFields，並將編輯介面調整為使用 Dropdownlist 進行，而不是文字方塊。 在這些 TemplateFields 的 `ItemTemplates`中，會顯示 `CategoryName` 和 `SupplierName` 資料欄位。
- 已將 `UnitPrice`、`UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` BoundFields 轉換成 TemplateFields，並新增 CompareValidator 控制項。

由於我們已在先前的教學課程中檢查如何完成這些工作，因此我只會在此列出最終的宣告式語法，並將實作為實務。

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample9.aspx)]

我們非常接近完整的範例。 不過，有幾個微妙差異將會蔓延，並造成我們的問題。 此外，我們還需要一些介面，在發生並行違規時警示使用者。

> [!NOTE]
> 為了讓資料 Web 控制項正確地將原始值傳遞給 ObjectDataSource （然後傳遞給 BLL），請務必將 GridView 的 `EnableViewState` 屬性設定為 `true` （預設值）。 如果您停用 view 狀態，則在回傳時，原始值會遺失。

## <a name="passing-the-correct-original-values-to-the-objectdatasource"></a>將正確的原始值傳遞至 ObjectDataSource

設定 GridView 的方式有幾個問題。 如果 ObjectDataSource 的 `ConflictDetection` 屬性設定為 `CompareAllValues` （如我們所示），則由 GridView （或 DetailsView 或 FormView）叫用 ObjectDataSource 的 `Update()` 或 `Delete()` 方法時，ObjectDataSource 會嘗試將 GridView 的原始值複製到其適當的 `Parameter` 實例。 如需此程式的圖形表示，請回頭參閱 [圖 2]。

具體而言，在每次資料系結至 GridView 時，GridView 的原始值都會指派給雙向資料系結語句中的值。 因此，所有必要的原始值都必須透過雙向資料系結來捕捉，而且是以可轉換的格式提供。

若要查看這是很重要的原因，請花一點時間造訪瀏覽器中的頁面。 如預期，GridView 會在最左邊的資料行中，使用 [編輯] 和 [刪除] 按鈕來列出每個產品。

[![在 GridView 中列出產品](implementing-optimistic-concurrency-vb/_static/image39.png)](implementing-optimistic-concurrency-vb/_static/image38.png)

**圖 14**：產品會列在 GridView 中（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image40.png)）

如果您按一下任何產品的 [刪除] 按鈕，則會擲回 `FormatException`。

[![嘗試刪除 FormatException 中的任何產品結果](implementing-optimistic-concurrency-vb/_static/image42.png)](implementing-optimistic-concurrency-vb/_static/image41.png)

**圖 15**：嘗試刪除 `FormatException` 中的任何產品結果（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image43.png)）

當 ObjectDataSource 嘗試讀取原始 `UnitPrice` 值時，就會引發 `FormatException`。 由於 `ItemTemplate` 的 `UnitPrice` 會格式化為貨幣（`<%# Bind("UnitPrice", "{0:C}") %>`），因此它會包含貨幣符號，例如 $19.95。 當 ObjectDataSource 嘗試將這個字串轉換成 `decimal`時，就會發生 `FormatException`。 為了避免這個問題，我們有幾個選項：

- 從 `ItemTemplate`中移除貨幣格式。 也就是說，而不是使用 `<%# Bind("UnitPrice", "{0:C}") %>`，而是只使用 `<%# Bind("UnitPrice") %>`。 其缺點在於價格已不再格式化。
- 在 `ItemTemplate`中顯示格式化為貨幣的 `UnitPrice`，但使用 `Eval` 關鍵字來完成這項操作。 回想一下，`Eval` 會執行單向資料系結。 我們仍然需要提供原始值的 `UnitPrice` 值，因此在 `ItemTemplate`中仍然需要雙向資料系結語句，但這可以放在 `Visible` 屬性設定為 `false`的標籤 Web 控制項中。 我們可以在 ItemTemplate 中使用下列標記：

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample10.aspx)]

- 使用 `<%# Bind("UnitPrice") %>`從 `ItemTemplate`移除貨幣格式。 在 GridView 的 `RowDataBound` 事件處理常式中，以程式設計方式存取顯示 `UnitPrice` 值的標籤 Web 控制項，並將其 `Text` 屬性設定為格式化版本。
- 將 `UnitPrice` 保留為貨幣格式。 在 GridView 的 `RowDeleting` 事件處理常式中，使用 `Decimal.Parse`，將現有的原始 `UnitPrice` 值（$19.95）取代為實際的十進位值。 我們已瞭解如何在 ASP.NET 網頁教學課程中[*處理 BLL 和 DAL 層級的例外*](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-cs.md)狀況，以在 `RowUpdating` 事件處理常式中完成類似的作業。

在我的範例中，我選擇使用第二個方法，加入隱藏的標籤 Web 控制項，其 `Text` 屬性是系結至未格式化 `UnitPrice` 值的雙向資料。

解決此問題之後，請再次嘗試按一下任何產品的 [刪除] 按鈕。 這次當 ObjectDataSource 嘗試叫用 BLL 的 `UpdateProduct` 方法時，您會收到 `InvalidOperationException`。

[![ObjectDataSource 找不到具有所要傳送之輸入參數的方法](implementing-optimistic-concurrency-vb/_static/image45.png)](implementing-optimistic-concurrency-vb/_static/image44.png)

**圖 16**： ObjectDataSource 找不到具有所要傳送之輸入參數的方法（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image46.png)）

查看例外狀況的訊息，可以清楚的是，ObjectDataSource 想要叫用具有 `original_CategoryName` 和 `original_SupplierName` 輸入參數的 BLL `DeleteProduct` 方法。 這是因為 `CategoryID` 和 `SupplierID` TemplateFields 的 `ItemTemplate` 目前包含具有 `CategoryName` 和 `SupplierName` 資料欄位的雙向 Bind 語句。 相反地，我們需要在 `CategoryID` 和 `SupplierID` 資料欄位中包含 `Bind` 語句。 若要完成此動作，請使用 `Eval` 語句來取代現有的 Bind 語句，然後加入隱藏的標籤控制項，其 `Text` 屬性會使用雙向資料系結系結至 `CategoryID` 和 `SupplierID` 資料欄位，如下所示：

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample11.aspx)]

有了這些變更，我們現在可以成功刪除和編輯產品資訊！ 在步驟5中，我們將探討如何確認偵測到並行違規。 但現在，請花幾分鐘的時間來嘗試更新和刪除一些記錄，以確保單一使用者的更新和刪除作業如預期般運作。

## <a name="step-5-testing-the-optimistic-concurrency-support"></a>步驟5：測試開放式平行存取支援

為了確認偵測到並行違規（而不是造成資料被盲目覆寫），我們需要在此頁面開啟兩個瀏覽器視窗。 在這兩個瀏覽器實例中，按一下 [Chai] 的 [編輯] 按鈕。 然後，只在其中一個瀏覽器中，將名稱變更為 "Chai 茶"，然後按一下 [更新]。 更新應會成功，並將 GridView 還原為其預先編輯狀態，並以 "Chai 茶" 作為新的產品名稱。

不過，在另一個瀏覽器視窗實例中，[產品名稱] 文字方塊仍會顯示 "Chai"。 在第二個瀏覽器視窗中，將 `UnitPrice` 更新為 `25.00`。 如果沒有開放式平行存取支援，在第二個瀏覽器實例中按一下 [更新]，會將產品名稱變更回 "Chai"，因而覆寫第一個瀏覽器實例所做的變更。 不過，在採用開放式平行存取的情況下，按一下第二個瀏覽器實例中的 [更新] 按鈕會導致[system.data.dbconcurrencyexception](https://msdn.microsoft.com/library/system.data.dbconcurrencyexception.aspx)。

[![偵測到並行違規時，則會擲回 System.data.dbconcurrencyexception](implementing-optimistic-concurrency-vb/_static/image48.png)](implementing-optimistic-concurrency-vb/_static/image47.png)

**圖 17**：偵測到並行違規時，會擲回 `DBConcurrencyException` （[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image49.png)）

只有在使用 DAL 的批次更新模式時，才會擲回 `DBConcurrencyException`。 DB direct 模式不會引發例外狀況，只表示沒有任何資料列受到影響。 為了說明這一點，請將瀏覽器實例的 GridView 同時傳回至其預先編輯狀態。 接下來，在第一個瀏覽器實例中，按一下 [編輯] 按鈕，並將產品名稱從 "Chai 茶" 變更回 "Chai"，然後按一下 [更新]。 在第二個瀏覽器視窗中，按一下 [Chai] 的 [刪除] 按鈕。

按一下 [刪除] 時，此頁面會回傳，GridView 會叫用 ObjectDataSource 的 `Delete()` 方法，而 ObjectDataSource 會向下呼叫 `ProductsOptimisticConcurrencyBLL` 類別的 `DeleteProduct` 方法，並沿著原始值傳遞。 第二個瀏覽器實例的原始 `ProductName` 值為 "Chai 茶"，這與資料庫中目前的 `ProductName` 值不相符。 因此，對資料庫發出的 `DELETE` 語句會影響零個數據列，因為 `WHERE` 子句所滿足的資料庫中沒有任何記錄。 `DeleteProduct` 方法會傳回 `false`，而 ObjectDataSource 的資料會重新系結至 GridView。

從使用者的觀點來看，在第二個瀏覽器視窗中，按一下 [Chai 茶] 的 [刪除] 按鈕會使螢幕閃爍，而在送回後，產品仍然存在，但現在它會列為 "Chai" （第一個瀏覽器所做的產品名稱變更）實例）。 如果使用者再次按一下 [刪除] 按鈕，刪除將會成功，因為 GridView 的原始 `ProductName` 值（"Chai"）現在符合資料庫中的值。

在這兩種情況下，使用者經驗都不太理想。 當您使用批次更新模式時，我們很清楚不想要向使用者顯示 `DBConcurrencyException` 例外狀況的具體細節。 而使用 DB direct 模式時的行為，會因為使用者命令失敗而造成混淆，但並沒有精確的指示。

若要解決這兩個問題，我們可以在頁面上建立標籤 Web 控制項，以提供更新或刪除失敗原因的說明。 針對批次更新模式，我們可以判斷 GridView 的後置層級事件處理常式中是否發生 `DBConcurrencyException` 例外狀況，並視需要顯示警告標籤。 對於 DB 直接方法，我們可以檢查 BLL 方法的傳回值（如果有一個資料列受到影響，則會 `true`，否則 `false`），並視需要顯示參考用訊息。

## <a name="step-6-adding-informational-messages-and-displaying-them-in-the-face-of-a-concurrency-violation"></a>步驟6：新增參考用訊息，並在面臨並行違規時顯示它們

發生並行違規時，所出現的行為取決於是否使用 DAL 的批次更新或 DB 直接模式。 我們的教學課程會使用這兩種模式，並使用批次更新模式來進行更新，以及用來刪除的資料庫直接模式。 首先，讓我們在頁面中新增兩個標籤 Web 控制項，說明嘗試刪除或更新資料時，發生並行違規。 將標籤控制項的 `Visible` 和 `EnableViewState` 屬性設定為 `false`;這會導致在每個頁面上都隱藏它們，但這些頁面造訪的 `Visible` 屬性是以程式設計方式設定為 `true`。

[!code-aspx[Main](implementing-optimistic-concurrency-vb/samples/sample12.aspx)]

除了設定其 `Visible`、`EnabledViewState`和 `Text` 屬性之外，我也將 `CssClass` 屬性設定為 [`Warning`]，這會使標籤以大、紅色、斜體、粗體字型顯示。 已定義此 CSS `Warning` 類別，並將其加入至樣式. CSS 中*檢查與插入、更新和刪除教學課程相關聯的事件*。

加入這些標籤之後，Visual Studio 中的設計工具看起來應該類似 [圖 18]。

[![兩個標籤控制項已加入至頁面](implementing-optimistic-concurrency-vb/_static/image51.png)](implementing-optimistic-concurrency-vb/_static/image50.png)

**圖 18**：已將兩個標籤控制項新增至頁面（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image52.png)）

有了這些 Web 控制項的標籤之後，我們就可以開始檢查如何判斷發生並行違規的時間，此時可以將適當標籤的 `Visible` 屬性設定為 `true`，顯示參考用訊息。

## <a name="handling-concurrency-violations-when-updating"></a>在更新時處理並行違規

讓我們先看看如何在使用批次更新模式時處理並行違規。 因為與批次更新模式的違規會導致擲回 `DBConcurrencyException` 例外狀況，所以我們需要將程式碼新增至我們的 ASP.NET 網頁，以判斷更新程式期間是否發生 `DBConcurrencyException` 例外狀況。 若是如此，我們應該向使用者顯示一則訊息，說明他們的變更並未儲存，因為另一位使用者在開始編輯記錄和按一下 [更新] 按鈕時，修改了相同的資料。

如我們在 ASP.NET 網頁教學課程中*處理 BLL 和 DAL 層級的例外*狀況中所見，您可以在資料 Web 控制項的後置層級事件處理常式中偵測到和隱藏這類例外狀況。 因此，我們需要為 GridView 的 `RowUpdated` 事件建立事件處理常式，以檢查是否已擲回 `DBConcurrencyException` 例外狀況。 這個事件處理常式會傳遞在更新程式期間引發之任何例外狀況的參考，如以下的事件處理常式代碼所示：

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample13.vb)]

在 `DBConcurrencyException` 例外狀況的臉部中，此事件處理常式會顯示 `UpdateConflictMessage` Label 控制項，並指出已處理例外狀況。 當此程式碼準備好時，當更新記錄時發生並行違規時，使用者的變更會遺失，因為他們會同時覆寫其他使用者的修改。 特別是，GridView 會回到其預先編輯狀態，並系結至目前的資料庫資料。 這會使用其他使用者的變更（先前不可見）來更新 GridView 資料列。 此外，`UpdateConflictMessage` Label 控制項也會向使用者說明剛剛發生的情況。 [圖 19] 中詳述了這一系列的事件。

[![使用者的更新在面臨並行違規時遺失](implementing-optimistic-concurrency-vb/_static/image54.png)](implementing-optimistic-concurrency-vb/_static/image53.png)

**圖 19**：遇到並行違規時，使用者的更新會遺失（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image55.png)）

> [!NOTE]
> 或者，您可以將傳入 `GridViewUpdatedEventArgs` 物件的 `KeepInEditMode` 屬性設定為 true，而不是將 GridView 改成進入編輯狀態。 不過，如果您採用這種方法，請務必將資料重新系結至 GridView （藉由叫用其 `DataBind()` 方法），以便將其他使用者的值載入至編輯介面。 在此教學課程中可供下載的程式碼在 `RowUpdated` 事件處理常式中有這兩行程式碼會加上批註;只要取消批註這幾行程式碼，GridView 就會在並行違規之後保持編輯模式。

## <a name="responding-to-concurrency-violations-when-deleting"></a>在刪除時回應並行違規

使用 DB direct 模式時，不會在面臨並行違規的情況下引發例外狀況。 相反地，database 語句只會影響任何記錄，因為 WHERE 子句不會與任何記錄相符。 在 BLL 中建立的所有資料修改方法，都是設計成會傳回布林值，指出它們是否只影響一筆記錄。 因此，若要判斷刪除記錄時是否發生並行違規，我們可以檢查 BLL 的 `DeleteProduct` 方法的傳回值。

您可以透過傳遞至事件處理常式之 `ObjectDataSourceStatusEventArgs` 物件的 `ReturnValue` 屬性，在 ObjectDataSource 的 post 層級事件處理常式中檢查 BLL 方法的傳回值。 因為我們想要從 `DeleteProduct` 方法判斷傳回值，所以我們需要為 ObjectDataSource 的 `Deleted` 事件建立事件處理常式。 `ReturnValue` 屬性的類型是 `object` 而且如果引發例外狀況，而且方法在可能傳回值之前已中斷，則可以 `null`。 因此，我們應該先確定 `ReturnValue` 屬性不 `null`，而且是布林值。 假設這種檢查通過，如果 `ReturnValue` `false`，我們會顯示 `DeleteConflictMessage` 標籤控制項。 您可以使用下列程式碼來完成這項作業：

[!code-vb[Main](implementing-optimistic-concurrency-vb/samples/sample14.vb)]

在遇到並行違規時，會取消使用者的刪除要求。 GridView 會重新整理，顯示該記錄在使用者載入頁面和按一下 [刪除] 按鈕時所發生的變更。 當這類違規過大幅簡化時，會顯示 [`DeleteConflictMessage`] 標籤，說明剛發生的情況（請參閱 [圖 20]）。

[![在面臨並行違規時取消使用者的刪除](implementing-optimistic-concurrency-vb/_static/image57.png)](implementing-optimistic-concurrency-vb/_static/image56.png)

**圖 20**：發生並行違規時，會取消使用者的刪除（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-vb/_static/image58.png)）

## <a name="summary"></a>總結

在允許多個並行使用者更新或刪除資料的每個應用程式中，有並行違規的機會。 如果未考慮這類違規，則當兩個使用者同時更新最後寫入「獲勝」中取得的相同資料時，會覆寫其他使用者的變更。 或者，開發人員可以執行開放式或封閉式並行存取控制。 開放式並行存取控制會假設並行違規不頻繁，而只是不允許會構成並行違規的 update 或 delete 命令。 封閉式並行存取控制項會假設並行違規很頻繁，而只是拒絕一個使用者的 update 或 delete 命令是無法接受的。 使用封閉式並行存取控制時，更新記錄牽涉到鎖定，藉此防止任何其他使用者在鎖定時修改或刪除記錄。

.NET 中的具類型資料集提供支援開放式並行存取控制的功能。 特別的是，發出到資料庫的 `UPDATE` 和 `DELETE` 語句包含所有資料表的資料行，因此，確保只有當記錄的目前資料符合使用者執行其更新或刪除時所擁有的原始資料時，才會發生更新或刪除。 一旦將 DAL 設定為支援開放式平行存取，就需要更新 BLL 方法。 此外，您必須設定向下呼叫 BLL 的 ASP.NET 網頁，讓 ObjectDataSource 從其資料 Web 控制項抓取原始值，並將它們傳遞到 BLL 中。

如我們在本教學課程中所見，在 ASP.NET web 應用程式中執行開放式並行存取控制牽涉到更新 DAL 和 BLL，並在 [ASP.NET] 頁面中新增支援。 此新增的工作是否為您的時間和投入量而定，取決於您的應用程式。 如果您不常有同時更新資料的並行使用者，或它們正在更新的資料與另一個不同，則並行控制不是關鍵問題。 不過，如果您的網站上經常有多個使用者使用相同的資料，並行存取控制可協助防止某個使用者的更新或刪除意外覆寫另一個。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](customizing-the-data-modification-interface-vb.md)
> [下一頁](adding-client-side-confirmation-when-deleting-vb.md)
