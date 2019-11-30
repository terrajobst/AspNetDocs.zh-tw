---
uid: web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-cs
title: 使用 SqlDataSource （C#）來執行開放式平行存取 |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討開放式並行存取控制的基本概念，然後探索如何使用 SqlDataSource 控制項來執行它。
ms.author: riande
ms.date: 02/20/2007
ms.assetid: df999966-ac48-460e-b82b-4877a57d6ab9
msc.legacyurl: /web-forms/overview/data-access/accessing-the-database-directly-from-an-aspnet-page/implementing-optimistic-concurrency-with-the-sqldatasource-cs
msc.type: authoredcontent
ms.openlocfilehash: 87fca52e2e8be844411b2fff8382c6002eccbe09
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74598106"
---
# <a name="implementing-optimistic-concurrency-with-the-sqldatasource-c"></a>使用 SqlDataSource 實作開放式同步存取 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_50_CS.exe)或[下載 PDF](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/datatutorial50cs1.pdf)

> 在本教學課程中，我們將探討開放式並行存取控制的基本概念，然後探索如何使用 SqlDataSource 控制項來執行它。

## <a name="introduction"></a>簡介

在先前的教學課程中，我們探討了如何將插入、更新和刪除功能新增至 SqlDataSource 控制項。 簡言之，若要提供這些功能，我們需要在控制項 s `InsertCommand`、`UpdateCommand`或 `DeleteCommand` 屬性中指定對應的 `INSERT`、`UPDATE`或 `DELETE` SQL 語句，以及 `InsertParameters`、`UpdateParameters`和 `DeleteParameters` 集合中的適當參數。 雖然可以手動指定這些屬性和集合，但是 [設定資料來源嚮導] 的 [建立 `INSERT`]、[`UPDATE`] 和 [`DELETE` 語句] 核取方塊會根據 `SELECT` 語句，自動建立這些語句。

除了 [產生 `INSERT`]、[`UPDATE`] 和 [`DELETE` 語句] 核取方塊，[Advanced SQL 產生選項] 對話方塊還包含 [使用開放式平行存取] 選項（請參閱 [圖 1]）。 若有選取時，自動產生的 `UPDATE` 和 `DELETE` 語句中的 `WHERE` 子句會修改成隻在使用者上次將資料載入方格後未修改基礎資料庫資料時，才執行更新或刪除。

![您可以從 [Advanced SQL 產生選項] 對話方塊新增開放式平行存取支援](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image1.gif)

**圖 1**：您可以從 [Advanced SQL 產生選項] 對話方塊加入開放式平行存取支援

回到[執行開放式並行](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md)存取教學課程，我們檢查了開放式並行存取控制的基本概念，以及如何將它加入至 ObjectDataSource。 在本教學課程中，我們將針對開放式並行存取控制的基本概念進行潤色，然後探索如何使用 SqlDataSource 來執行。

## <a name="a-recap-of-optimistic-concurrency"></a>開放式平行存取的回顧

對於允許多個同時使用者編輯或刪除相同資料的 web 應用程式，有可能有一位使用者意外覆寫另一項變更。 在[執行開放式並行](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md)存取教學課程中，我提供了下列範例：

假設有兩位使用者（Jisun 和 Sam）同時造訪應用程式中的網頁，讓訪客能夠透過 GridView 控制項來更新和刪除產品。 同時按一下 [Chai] 的 [編輯] 按鈕，以在同一時間前後進行。 Jisun 會將產品名稱變更為 Chai 茶，並按一下 [更新] 按鈕。 最終結果是傳送至資料庫的 `UPDATE` 語句，它會設定*所有*產品的可更新欄位（即使 Jisun 只更新一個欄位，`ProductName`）。 在此時間點，資料庫的值為 Chai 茶、類別飲料、供應商外來液體等等。 不過，Sam s 畫面上的 GridView 仍然會在可編輯的 GridView 資料列中，將產品名稱顯示為 Chai。 在 Jisun s 變更之後的幾秒後，Sam 會將類別更新為 Condiments，然後按一下 [更新]。 這會導致 `UPDATE` 語句傳送到資料庫，將產品名稱設定為 Chai，`CategoryID` 對應的 Condiments 分類識別碼等等。 已覆寫對產品名稱所做的 Jisun 變更。

[圖 2] 說明這種互動。

[![當兩個使用者同時更新記錄時，有一位使用者變更可能會覆寫其他的](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image2.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image1.png)

**圖 2**：當兩個使用者同時更新記錄時，有一位使用者變更的可能性可能會覆寫其他的（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image2.png)）

若要防止展開此案例，必須實作為[並行存取控制](http://en.wikipedia.org/wiki/Concurrency_control)的形式。 [開放式並行](http://en.wikipedia.org/wiki/Optimistic_concurrency_control)存取：本教學課程的重點在於假設，雖然每個階段可能會發生並行衝突，但大部分的情況下都不會發生這類衝突。 因此，如果發生衝突，開放式並行存取控制只會通知使用者其變更無法儲存，因為另一個使用者已修改相同的資料。

> [!NOTE]
> 對於假設會有許多並行衝突或無法容忍這類衝突的應用程式，則可以改用封閉式並行存取控制。 請回頭[執行開放式並行](../editing-inserting-and-deleting-data/implementing-optimistic-concurrency-cs.md)存取教學課程，以深入瞭解封閉式並行存取控制。

開放式並行存取控制的運作方式是確保更新或刪除的記錄具有與更新或刪除進程啟動時相同的值。 例如，當您在可編輯的 GridView 中按一下 [編輯] 按鈕時，會從資料庫讀取記錄的值，並顯示在文字方塊和其他 Web 控制項中。 這些原始值是由 GridView 儲存。 之後，當使用者進行變更並按一下 [更新] 按鈕之後，所使用的 `UPDATE` 語句就必須考慮原始值加上新的值，而且只有在使用者開始編輯的原始值與資料庫中仍有的值相同時，才更新基礎資料庫記錄。 [圖 3] 描繪了這一系列的事件。

[若要成功更新或刪除 ![，原始值必須等於目前的資料庫值](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image3.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image3.png)

**圖 3**：若要讓 Update 或 Delete 成功，原始值必須等於目前的資料庫值（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image4.png)）

有各種方法可以執行開放式平行存取（請參閱[Peter A. Bromberg](http://www.eggheadcafe.com/articles/pbrombergresume.asp)的[開放式平行存取邏輯](http://www.eggheadcafe.com/articles/20050719.asp)，以瞭解一些選項）。 SqlDataSource 所使用的技術（以及資料存取層中所使用的 ADO.NET 具類型資料集）會增強 `WHERE` 子句，以包含所有原始值的比較。 例如，如果目前的資料庫值等於在 GridView 中更新記錄時原先抓取的值，則下列 `UPDATE` 語句會更新產品的名稱和價格。 `@ProductName` 和 `@UnitPrice` 參數包含使用者輸入的新值，而 `@original_ProductName` 和 `@original_UnitPrice` 包含在按下 [編輯] 按鈕時，原先載入至 GridView 的值：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample1.sql)]

如我們在本教學課程中所見，使用 SqlDataSource 來啟用開放式並行存取控制，就像勾選核取方塊一樣簡單。

## <a name="step-1-creating-a-sqldatasource-that-supports-optimistic-concurrency"></a>步驟1：建立支援開放式平行存取的 SqlDataSource

從 [`SqlDataSource`] 資料夾開啟 [`OptimisticConcurrency.aspx`] 頁面開始。 從 [工具箱] 將 [SqlDataSource] 控制項拖曳至設計工具，將其 `ID` 屬性設定為 [`ProductsDataSourceWithOptimisticConcurrency`]。 接下來，按一下控制項 s 智慧標籤中的 [設定資料來源] 連結。 從嚮導的第一個畫面中，選擇使用 `NORTHWINDConnectionString`，然後按 [下一步]。

[![選擇使用 NORTHWINDConnectionString](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image4.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image5.png)

**圖 4**：選擇使用 `NORTHWINDConnectionString` （[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image6.png)）

在此範例中，我們將新增 GridView，讓使用者編輯 `Products` 資料表。 因此，從 [設定 Select 語句] 畫面中，選擇下拉式清單中的 [`Products`] 資料表，然後選取 [`ProductID`]、[`ProductName`]、[`UnitPrice`] 和 [`Discontinued`] 資料行，如 [圖 5] 所示。

[從 Products 資料表 ![，傳回 ProductID、ProductName、單價和已停止的資料行](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image5.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image7.png)

**圖 5**：從 [`Products`] 資料表中，傳回 [`ProductID`]、[`ProductName`]、[`UnitPrice`] 和 [`Discontinued`] 資料行（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image8.png)）

挑選資料行之後，請按一下 [Advanced] 按鈕以顯示 [Advanced SQL 產生選項] 對話方塊。 核取 [產生 `INSERT`]、[`UPDATE`] 和 [`DELETE` 語句，並使用開放式平行存取] 核取方塊，然後按一下 [確定] （如需螢幕擷取畫面，請參閱 [圖 1] 按 [下一步]，然後按一下 [完成]，以完成嚮導。

完成 [設定資料來源] 嚮導之後，請花點時間檢查產生的 `DeleteCommand` 並 `UpdateCommand` 屬性和 `DeleteParameters` 和 `UpdateParameters` 集合。 若要這麼做，最簡單的方法是按一下左下角的 [來源] 索引標籤，以查看頁面的宣告式語法。 您會在這裡找到 `UpdateCommand` 值：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample2.sql)]

`UpdateParameters` 集合中有七個參數：

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample3.aspx)]

同樣地，`DeleteCommand` 屬性和 `DeleteParameters` 集合看起來應該如下所示：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample4.sql)]

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample5.aspx)]

除了擴充 `UpdateCommand` 的 `WHERE` 子句和 `DeleteCommand` 屬性（以及將額外的參數新增至個別的參數集合）之外，選取 [使用開放式平行存取] 選項也會調整其他兩個屬性：

- 將[`ConflictDetection` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.conflictdetection.aspx)從 `OverwriteChanges` （預設值）變更為 `CompareAllValues`
- 將[`OldValuesParameterFormatString` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.sqldatasource.oldvaluesparameterformatstring.aspx)從 {0} （預設值）變更為原始\_{0}。

當資料 Web 控制項叫用 SqlDataSource s `Update()` 或 `Delete()` 方法時，它會傳入原始值。 如果 [SqlDataSource s `ConflictDetection`] 屬性設為 [`CompareAllValues`]，則會將這些原始值新增至命令。 `OldValuesParameterFormatString` 屬性提供用於這些原始值參數的命名模式。 [設定資料來源] 嚮導會使用原始\_{0} 並在 `DeleteCommand` `UpdateCommand` 中命名每個原始參數，並據以 `UpdateParameters` 和 `DeleteParameters` 集合。

> [!NOTE]
> 由於我們不會使用 SqlDataSource 控制項的插入功能，因此請隨意移除 `InsertCommand` 屬性及其 `InsertParameters` 集合。

## <a name="correctly-handlingnullvalues"></a>正確處理`NULL`值

可惜的是，使用開放式平行存取時，[設定資料來源] wizard 自動產生的增強型 `UPDATE` 和 `DELETE` 語句*不會*使用包含 `NULL` 值的記錄。 若要瞭解原因，請考慮我們的 SqlDataSource `UpdateCommand`：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample6.sql)]

`Products` 資料表中的 `UnitPrice` 資料行可以有 `NULL` 值。 如果特定記錄具有 `UnitPrice`的 `NULL` 值，則 `WHERE` 子句部分 `[UnitPrice] = @original_UnitPrice`*一律*會評估為 false，因為 `NULL = NULL` 一律會傳回 false。 因此，包含 `NULL` 值的記錄無法編輯或刪除，因為 `UPDATE` 和 `DELETE` 語句 `WHERE` 子句不會傳回任何要更新或刪除的資料列。

> [!NOTE]
> 此錯誤在2004年6月首次向 Microsoft 回報， [SqlDataSource 會產生不正確的 SQL 語句](https://connect.microsoft.com/VisualStudio/feedback/ViewFeedback.aspx?FeedbackID=93937)，而且據傳排定在下一版的 ASP.NET 中修正。

若要修正此問題，我們必須針對可以有 `NULL` 值的**所有**資料行，以手動方式更新 `UpdateCommand` 和 `DeleteCommand` 屬性中的 `WHERE` 子句。 在 [一般] 中，將 `[ColumnName] = @original_ColumnName` 變更為：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample7.sql)]

這項修改可以直接透過宣告式標記、屬性視窗的 UpdateQuery 或 DeleteQuery 選項，或是透過 [設定資料] 中 [指定自訂 SQL 語句或預存程式] 選項的 [更新] 和 [刪除] 索引標籤來進行。來源 wizard。 同樣地，您必須針對 `UpdateCommand` 和 `DeleteCommand` s `WHERE` 子句中可包含 `NULL` 值的*每個*資料行進行這項修改。

將此套用到我們的範例會產生下列已修改的 `UpdateCommand` 和 `DeleteCommand` 值：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample8.sql)]

## <a name="step-2-adding-a-gridview-with-edit-and-delete-options"></a>步驟2：使用 [編輯] 和 [刪除] 選項加入 GridView

當 SqlDataSource 設定為支援開放式平行存取時，剩下的工作就是將資料 Web 控制項加入至利用此並行存取控制的頁面。 在本教學課程中，我們將新增可同時提供編輯和刪除功能的 GridView。 若要完成此動作，請將 GridView 從 [工具箱] 拖曳至設計工具，並將其 `ID` 設定為 [`Products`]。 從 GridView 的智慧標籤，將它系結至步驟1中新增的 `ProductsDataSourceWithOptimisticConcurrency` SqlDataSource 控制項。 最後，請核取 [啟用編輯] 和 [啟用刪除] 選項（從智慧標籤）。

[![將 GridView 系結至 SqlDataSource，並啟用編輯和刪除](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image6.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image9.png)

**圖 6**：將 GridView 系結至 SqlDataSource，並啟用編輯和刪除（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image10.png)）

加入 GridView 之後，請移除 `ProductID` BoundField、將 `ProductName` BoundField s `HeaderText` 屬性變更為 [Product]，然後更新 `UnitPrice` BoundField，使其 [`HeaderText`] 屬性只是價格，以設定其外觀。 在理想的情況下，我們會增強編輯介面，以包含 `ProductName` 值的 RequiredFieldValidator 和 `UnitPrice` 值的 CompareValidator （以確保其格式正確的數值）。 請參閱[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-cs.md)教學課程，以深入瞭解自訂 GridView 的編輯介面。

> [!NOTE]
> 必須啟用 GridView s view 狀態，因為從 GridView 傳遞至 SqlDataSource 的原始值會以檢視狀態儲存。

對 GridView 進行這些修改之後，GridView 和 SqlDataSource 宣告式標記看起來應該如下所示：

[!code-aspx[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample9.aspx)]

若要查看作用中的開放式並行存取控制，請開啟兩個瀏覽器視窗，並在兩者中載入 [`OptimisticConcurrency.aspx`] 頁面。 在兩個瀏覽器中，按一下第一個產品的 [編輯] 按鈕。 在一個瀏覽器中，變更產品名稱，然後按一下 [更新]。 瀏覽器將回傳，而 GridView 會回到其預先編輯模式，顯示剛編輯之記錄的新產品名稱。

在第二個瀏覽器視窗中，變更價格（但保留產品名稱作為其原始值），然後按一下 [更新]。 在回傳時，方格會回到其預先編輯模式，但不會記錄價格的變更。 第二個瀏覽器顯示的值與具有舊價格的新產品名稱的第一個相同。 在第二個瀏覽器視窗中所做的變更已遺失。 此外，由於沒有任何例外狀況或訊息指出發生的平行存取違規，因此變更已遺失，而不是安靜。

[![第二個瀏覽器視窗中的變更不會以無訊息方式遺失](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image7.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image11.png)

**圖 7**：第二個瀏覽器視窗中的變更以無訊息方式遺失（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image12.png)）

未認可第二個瀏覽器變更的原因是因為 `UPDATE` 語句 s `WHERE` 子句已篩選掉所有記錄，因此不會影響任何資料列。 讓我們再看一次 `UPDATE` 語句：

[!code-sql[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample10.sql)]

當第二個瀏覽器視窗更新記錄時，`WHERE` 子句中指定的原始產品名稱不會與現有的產品名稱相符（因為第一個瀏覽器已變更）。 因此，語句 `[ProductName] = @original_ProductName` 會傳回 False，而 `UPDATE` 不會影響任何記錄。

> [!NOTE]
> Delete 的運作方式相同。 在開啟兩個瀏覽器視窗的情況下，一開始先編輯指定的產品，然後再儲存其變更。 在單一瀏覽器中儲存變更之後，請按一下另一個中相同產品的 [刪除] 按鈕。 因為原始值不會在 `DELETE` 語句 s `WHERE` 子句中相符，所以刪除會以無訊息模式失敗。

從使用者在第二個瀏覽器視窗中的觀點來看，按一下 [更新] 按鈕之後，方格會回到預先編輯模式，但其變更已遺失。 不過，沒有視覺效果的意見反應，他們的變更不會改變。 在理想的情況下，如果使用者的變更會遺失並行違規，我們會通知他們，而且可能會將方格保持在編輯模式。 讓我們看看如何完成此動作。

## <a name="step-3-determining-when-a-concurrency-violation-has-occurred"></a>步驟3：判斷是否發生並行違規

由於並行違規會拒絕所做的變更，因此在發生並行違規時，會很有可能會對使用者發出警示。 若要警示使用者，請將標籤 Web 控制項新增至名為 `ConcurrencyViolationMessage` 的頁面頂端，其 `Text` 屬性會顯示下列訊息：您已嘗試更新或刪除另一位使用者同時更新的記錄。 請檢查其他使用者的變更，然後重做您的更新或刪除。 將 [標籤控制項] `CssClass` 屬性設定為 [警告]，這是在 `Styles.css` 中定義的 CSS 類別，會以紅色、斜體、粗體和大字型顯示文字。 最後，將標籤的 `Visible` 和 `EnableViewState` 屬性設定為 [`false`]。 這會隱藏標籤，但只有那些回傳會明確將其 `Visible` 屬性設為 `true`。

[![將標籤控制項新增至頁面以顯示警告](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image8.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image13.png)

**圖 8**：將標籤控制項新增至頁面以顯示警告（[按一下以查看完整大小的影像](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image14.png)）

執行更新或刪除時，GridView 的 `RowUpdated` 和 `RowDeleted` 事件處理常式會在其資料來源控制執行要求的更新或刪除之後引發。 我們可以從這些事件處理常式判斷作業所影響的資料列數目。 如果零個數據列受到影響，我們想要顯示 [`ConcurrencyViolationMessage`] 標籤。

建立 `RowUpdated` 和 `RowDeleted` 事件的事件處理常式，並新增下列程式碼：

[!code-csharp[Main](implementing-optimistic-concurrency-with-the-sqldatasource-cs/samples/sample11.cs)]

在這兩個事件處理常式中，我們會檢查 `e.AffectedRows` 屬性，如果它等於0，請將 `ConcurrencyViolationMessage` Label s `Visible` 屬性設定為 `true`。 在 `RowUpdated` 事件處理常式中，我們也會藉由將 `KeepInEditMode` 屬性設定為 true，指示 GridView 保持編輯模式。 在這種情況下，我們需要將資料重新系結到方格，讓其他使用者的資料載入編輯介面中。 這是藉由呼叫 GridView s `DataBind()` 方法來完成。

如 [圖 9] 所示，在這兩個事件處理常式中，每當發生並行違規時，就會顯示非常明顯的訊息。

[![訊息會在面臨並行違規時顯示](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image9.gif)](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image15.png)

**圖 9**：發生並行違規時，會顯示訊息（[按一下以觀看完整大小的影像](implementing-optimistic-concurrency-with-the-sqldatasource-cs/_static/image16.png)）

## <a name="summary"></a>總結

建立多個並行使用者可能會編輯相同資料的 web 應用程式時，請務必考慮並行控制選項。 根據預設，ASP.NET 資料 Web 控制項和資料來源控制項不會採用任何並行存取控制。 如我們在本教學課程中所見，使用 SqlDataSource 來執行開放式並行存取控制的速度相當快速且簡單。 SqlDataSource 會處理您將擴充的 `WHERE` 子句加入至自動產生的 `UPDATE` 和 `DELETE` 語句的大部分跑腿活兒，但在處理 `NULL` 值資料行時，有幾個微妙差異，如正確處理 `NULL` 值一節中所述。

本教學課程將結束我們的 SqlDataSource 檢查。 其餘的教學課程將會回到使用 ObjectDataSource 和分層架構來處理資料。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](inserting-updating-and-deleting-data-with-the-sqldatasource-cs.md)
> [下一頁](querying-data-with-the-sqldatasource-control-vb.md)
