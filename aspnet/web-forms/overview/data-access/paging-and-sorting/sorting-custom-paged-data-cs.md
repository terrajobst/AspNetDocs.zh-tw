---
uid: web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-cs
title: 排序自訂的分頁C#資料（） |Microsoft Docs
author: rick-anderson
description: 在上一個教學課程中，我們已瞭解如何在 web 網頁上呈現資料時，執行自訂分頁。 在本教學課程中，我們會瞭解如何擴充前述的 。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 778baa4e-4af8-4665-947e-7a01d1a4dff2
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/sorting-custom-paged-data-cs
msc.type: authoredcontent
ms.openlocfilehash: e55ed9b92814753e95bdfdf26c2f051df6f2630d
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74642369"
---
# <a name="sorting-custom-paged-data-c"></a>排序自訂的分頁資料 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_26_CS.exe)或[下載 PDF](sorting-custom-paged-data-cs/_static/datatutorial26cs1.pdf)

> 在上一個教學課程中，我們已瞭解如何在 web 網頁上呈現資料時，執行自訂分頁。 在本教學課程中，我們會瞭解如何擴充上述範例，以包含排序自訂分頁的支援。

## <a name="introduction"></a>簡介

相較于預設分頁，自訂分頁可以改善依數個量級排序資料分頁的效能，讓自訂分頁在分頁處理大量資料時，成為一種相當於事實上的分頁執行選擇。 不過，執行自訂分頁比實作為預設分頁更為複雜，特別是在將排序加入至混合時。 在本教學課程中，我們將擴充前一個範例中的範例，以包含排序*和*自訂分頁的支援。

> [!NOTE]
> 由於本教學課程是以先前的版本為基礎，因此在開始之前，請先從上一個教學課程的網頁（`EfficientPaging.aspx`）複製 `<asp:Content>` 元素內的宣告式語法，然後在 [`SortParameter.aspx`] 頁面的 [`<asp:Content>`] 元素之間貼上。 請回頭參閱將[驗證控制項新增至編輯和插入介面](../editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-cs.md)教學課程的步驟1，以深入瞭解如何將一個 ASP.NET 網頁的功能複寫至另一頁。

## <a name="step-1-reexamining-the-custom-paging-technique"></a>步驟1： Reexamining 自訂分頁技術

若要讓自訂分頁正常運作，我們必須執行一些技術，讓它能夠有效率地抓取特定的記錄子集（給定起始資料列索引和最大資料列參數）。 有一些技巧可以用來達成此目標。 在先前的教學課程中，我們探討了如何使用 Microsoft SQL Server 2005 s new `ROW_NUMBER()` 排名函式來完成這項工作。 簡單地說，`ROW_NUMBER()` 次序函數會將資料列編號指派給依指定排序次序排序之查詢所傳回的每個資料列。 然後藉由傳回編號結果的特定區段來取得適當的記錄子集。 下列查詢說明如何使用這項技術，在依 `ProductName`的字母順序排序結果時，傳回編號為11到20的產品：

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample1.sql)]

這項技術適用于使用特定排序次序進行分頁（在此案例中`ProductName` 依字母順序排序），但必須修改查詢，以顯示依不同排序運算式排序的結果。 在理想的情況下，可以將上述查詢改寫成在 `OVER` 子句中使用參數，如下所示：

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample2.sql)]

可惜的是，不允許參數化 `ORDER BY` 子句。 相反地，我們必須建立可接受 `@sortExpression` 輸入參數的預存程式，但會使用下列其中一種因應措施：

- 針對每個可能使用的排序運算式撰寫硬式編碼的查詢;然後，使用 `IF/ELSE` T-sql 語句來判斷要執行的查詢。
- 使用 `CASE` 語句，根據 `@sortExpressio` n 輸入參數提供動態 `ORDER BY` 運算式;如需詳細資訊，請參閱[SQL `CASE` 語句的功能](http://www.4guysfromrolla.com/webtech/102704-1.shtml)中用來動態排序查詢結果一節的。
- 將適當的查詢製作為預存程式中的字串，然後使用[`sp_executesql` 系統預存](https://msdn.microsoft.com/library/ms188001.aspx)程式來執行動態查詢。

這些因應措施都有一些缺點。 第一個選項並不像其他兩個一樣可維護，因為您需要為每個可能的排序運算式建立查詢。 因此，如果您稍後決定要將新的可排序欄位加入至 GridView，您也必須返回並更新預存程式。 第二種方法有一些微妙差異，會在依非字串資料庫資料行排序時引進效能考慮，而且也會與第一個的可維護性問題有所影響。 第三個選擇（使用動態 SQL）會造成 SQL 插入式攻擊的風險，如果攻擊者能夠執行預存程式來傳入其選擇的輸入參數值。

雖然這些方法都不是完美的，但我認為第三個選項是這三個最佳選擇。 隨著動態 SQL 的使用，它提供了其他兩個的彈性層級。 此外，如果攻擊者能夠執行預存程式來傳入他所選的輸入參數，就只能利用 SQL 插入式攻擊。 由於 DAL 使用參數化查詢，因此 ADO.NET 會保護透過架構傳送至資料庫的參數，這表示只有在攻擊者可以直接執行預存程式時，SQL 插入式攻擊弱點才會存在。

若要執行這項功能，請在 Northwind 資料庫中建立名為 `GetProductsPagedAndSorted`的新預存程式。 這個預存程式應接受三個輸入參數： `@sortExpression`、`nvarchar(100`類型的輸入參數），指定應該如何排序結果，並直接插入 `OVER` 子句中的 `ORDER BY` 文字後面。和 `@startRowIndex` 和 `@maximumRows`，從上一個教學課程中所檢查的 `GetProductsPaged` 預存程式中，相同的兩個整數輸入參數。 使用下列腳本建立 `GetProductsPagedAndSorted` 預存程式：

[!code-sql[Main](sorting-custom-paged-data-cs/samples/sample3.sql)]

預存程式一開始會先確保已指定 `@sortExpression` 參數的值。 如果遺失，則會依 `ProductID`將結果排序。 接下來，會將動態 SQL 查詢結構化。 請注意，這裡的動態 SQL 查詢與先前用來從 Products 資料表中取出所有資料列的查詢稍有不同。 在先前的範例中，我們使用子查詢取得每個產品的相關聯類別和供應商名稱。 這項決定是在[建立資料存取層](../introduction/creating-a-data-access-layer-cs.md)教學課程中執行，而不是使用 `JOIN` s，因為 TableAdapter 無法自動為這類查詢建立相關聯的插入、更新和刪除方法。 不過，`GetProductsPagedAndSorted` 預存程式必須使用 `JOIN` s，才會依據分類或供應商名稱來排序結果。

這個動態查詢是藉由串連靜態查詢部分和 `@sortExpression`、`@startRowIndex`和 `@maximumRows` 參數來建立的。 因為 `@startRowIndex` 和 `@maximumRows` 是整數參數，所以必須將它們轉換成 Nvarchars，才能正確串連。 一旦建立此動態 SQL 查詢，它就會透過 `sp_executesql`來執行。

請花點時間為 `@sortExpression`、`@startRowIndex`和 `@maximumRows` 參數的不同值測試此預存程式。 在 伺服器總管中，以滑鼠右鍵按一下預存程式名稱，然後選擇 執行。 這會顯示 [執行預存程式] 對話方塊，您可以在其中輸入輸入參數（請參閱 [圖 1]）。 若要依類別目錄名稱排序結果，請針對 `@sortExpression` 參數值使用 [類別目錄]。若要依供應商的公司名稱排序，請使用 [公司名稱]。 提供參數值之後，按一下 [確定]。 結果會顯示在 [輸出] 視窗中。 [圖 2] 顯示當以遞減順序依 `UnitPrice` 排序時，傳回11到20的產品時所得到的結果。

![針對預存程式的三個輸入參數，嘗試不同的值](sorting-custom-paged-data-cs/_static/image1.png)

**圖 1**：針對預存程式的三個輸入參數，嘗試不同的值

[![預存程式的結果會顯示在輸出視窗](sorting-custom-paged-data-cs/_static/image3.png)](sorting-custom-paged-data-cs/_static/image2.png)

**圖 2**：預存程式的結果會顯示在輸出視窗中（[按一下以查看完整大小的影像](sorting-custom-paged-data-cs/_static/image4.png)）

> [!NOTE]
> 當根據 `OVER` 子句中指定的 `ORDER BY` 資料行來排列結果的等級時，SQL Server 必須排序結果。 如果在資料行上有叢集索引，則會將結果排序依據，或如果有涵蓋索引，則這是快速作業，否則會更耗費成本。 若要改善夠大的查詢效能，請考慮為結果排序依據的資料行加入非叢集索引。 如需詳細資訊，請參閱[SQL Server 2005 中的次序函數和效能](http://www.sql-server-performance.com/ak_ranking_functions.asp)。

## <a name="step-2-augmenting-the-data-access-and-business-logic-layers"></a>步驟2：擴充資料存取和商務邏輯層

建立 `GetProductsPagedAndSorted` 預存程式之後，下一步就是提供方法，透過我們的應用程式架構來執行該預存程式。 這需要將適當的方法加入 DAL 和 BLL。 首先，將方法新增至 DAL。 開啟 `Northwind.xsd` 類型資料集，以滑鼠右鍵按一下 `ProductsTableAdapter`，然後從內容功能表中選擇 [加入查詢] 選項。 如同我們在先前的教學課程中所做的一樣，我們想要設定這個新的 DAL 方法，以使用現有的預存程式，在此情況下為 `GetProductsPagedAndSorted`。 一開始，表示您想要新的 TableAdapter 方法使用現有的預存程式。

![選擇使用現有的預存程式](sorting-custom-paged-data-cs/_static/image5.png)

**圖 3**：選擇使用現有的預存程式

若要指定要使用的預存程式，請從下一個畫面的下拉式清單中選取 [`GetProductsPagedAndSorted` 預存程式]。

![使用 GetProductsPagedAndSorted 預存程式](sorting-custom-paged-data-cs/_static/image6.png)

**圖 4**：使用 GetProductsPagedAndSorted 預存程式

這個預存程式會傳回一組記錄做為其結果，因此，在下一個畫面中，表示它會傳回表格式資料。

![表示預存程式會傳回表格式資料](sorting-custom-paged-data-cs/_static/image7.png)

**圖 5**：表示預存程式會傳回表格式資料

最後，建立使用 [填滿 DataTable] 和 [傳回 DataTable 模式] 的 DAL 方法，分別命名 `FillPagedAndSorted` 和 `GetProductsPagedAndSorted`的方法。

![選擇方法名稱](sorting-custom-paged-data-cs/_static/image8.png)

**圖 6**：選擇方法名稱

既然我們已經擴充 DAL，我們就準備好轉換成 BLL 了。 開啟 `ProductsBLL` 類別檔案，並加入新的方法，`GetProductsPagedAndSorted`。 這個方法必須接受三個輸入參數 `sortExpression`、`startRowIndex`和 `maximumRows`，而且應該只向下呼叫 DAL s `GetProductsPagedAndSorted` 方法，如下所示：

[!code-csharp[Main](sorting-custom-paged-data-cs/samples/sample4.cs)]

## <a name="step-3-configuring-the-objectdatasource-to-pass-in-the-sortexpression-parameter"></a>步驟3：設定要傳入 SortExpression 參數的 ObjectDataSource

增強 DAL 和 BLL 以包含利用 `GetProductsPagedAndSorted` 預存程式的方法，剩下的工作就是在 `SortParameter.aspx` 頁面中設定 ObjectDataSource，以使用新的 BLL 方法，並根據使用者已要求用來排序結果的資料行來傳入 `SortExpression` 參數。

首先，將 ObjectDataSource s `SelectMethod` 從 `GetProductsPaged` 變更為 `GetProductsPagedAndSorted`。 這可以透過 [設定資料來源]、[屬性視窗] 或直接透過宣告式語法來完成。 接下來，我們需要提供 ObjectDataSource s [`SortParameterName` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.objectdatasource.sortparametername.aspx)的值。 如果設定了這個屬性，ObjectDataSource 就會嘗試將 GridView 的 `SortExpression` 屬性傳入 `SelectMethod`。 特別是，ObjectDataSource 會尋找其名稱等於 `SortParameterName` 屬性值的輸入參數。 由於 BLL 的 `GetProductsPagedAndSorted` 方法具有名為 `sortExpression`的排序運算式輸入參數，因此請將 ObjectDataSource s `SortExpression` 屬性設定為 sortExpression。

進行這兩項變更之後，ObjectDataSource 的宣告式語法看起來應該如下所示：

[!code-aspx[Main](sorting-custom-paged-data-cs/samples/sample5.aspx)]

> [!NOTE]
> 如同先前的教學課程，請確定 ObjectDataSource 不會在其 SelectParameters 集合*中包含 sortExpression* 、StartRowIndex 或 maximumRows 輸入參數。

若要在 GridView 中啟用排序，只要勾選 GridView s 智慧標籤中的 [啟用排序] 核取方塊，將 GridView 的 `AllowSorting` 屬性設定為 `true`，並使每個資料行的標頭文字呈現為 LinkButton。 當終端使用者按一下其中一個標頭 LinkButtons 時，就會發生回傳接踵而來和下列步驟：

1. GridView 會將其[`SortExpression` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.sortexpression.aspx)更新為按一下標題連結之欄位的 `SortExpression` 值
2. ObjectDataSource 會叫用 BLL 的 `GetProductsPagedAndSorted` 方法，並傳入 GridView 的 `SortExpression` 屬性，做為方法 s `sortExpression` 輸入參數的值（以及適當的 `startRowIndex` 和 `maximumRows` 輸入參數值）
3. BLL 會叫用 DAL s `GetProductsPagedAndSorted` 方法
4. DAL 會執行 `GetProductsPagedAndSorted` 預存程式，傳入 `@sortExpression` 參數（連同 `@startRowIndex` 和 `@maximumRows` 輸入參數值）
5. 預存程式會將適當的資料子集傳回給 BLL，並將其傳回至 ObjectDataSource;然後，此資料會系結至 GridView、轉譯為 HTML，然後傳送給終端使用者

[圖 7] 顯示依 `UnitPrice` 以遞增順序排序時的第一頁結果。

[![結果會依單價排序](sorting-custom-paged-data-cs/_static/image10.png)](sorting-custom-paged-data-cs/_static/image9.png)

**圖 7**：結果依單價排序（[按一下以觀看完整大小的影像](sorting-custom-paged-data-cs/_static/image11.png)）

雖然目前的執行可以依產品名稱、類別目錄名稱、每個單位的數量和單價來正確排序結果，但嘗試依供應商名稱訂購結果會導致執行時間例外狀況（請參閱 [圖 8]）。

![嘗試依供應商排序結果會導致下列執行時間例外狀況](sorting-custom-paged-data-cs/_static/image12.png)

**圖 8**：嘗試依供應商排序結果會導致下列執行時間例外狀況

發生這個例外狀況的原因是 GridView `SupplierName` BoundField 的 `SortExpression` 設定為 `SupplierName`。 不過，實際上會呼叫 `Suppliers` 資料表中的供應商名稱，`CompanyName` 我們已將此資料行名稱的別名設為 `SupplierName`。 不過，`ROW_NUMBER()` 函數所使用的 `OVER` 子句不能使用別名，而且必須使用實際的資料行名稱。 因此，請將 `SupplierName` BoundField s `SortExpression` 從「商」變更為「公司名稱」（請參閱 [圖 9]）。 如 [圖 10] 所示，在這項變更之後，供應商可以排序結果。

![將 [BoundField] SortExpression 變更為 [公司名稱]](sorting-custom-paged-data-cs/_static/image13.png)

**圖 9**：將 [BoundField] SortExpression 變更為 [公司名稱]

[![現在可以依供應商排序結果](sorting-custom-paged-data-cs/_static/image15.png)](sorting-custom-paged-data-cs/_static/image14.png)

**圖 10**：現在可以依供應商排序結果（[按一下以觀看完整大小的影像](sorting-custom-paged-data-cs/_static/image16.png)）

## <a name="summary"></a>總結

我們在前一個教學課程中檢查的自訂分頁執行，需要在設計階段指定結果排序所依據的順序。 簡單地說，這表示我們所實行的自訂分頁執行無法同時提供排序功能。 在本教學課程中，我們會克服了這項限制，方法是從第一個延伸預存程式，以包含可供排序結果的 `@sortExpression` 輸入參數。

建立這個預存程式並在 DAL 和 BLL 中建立新的方法之後，我們就能夠藉由設定 ObjectDataSource，將 GridView 的 current `SortExpression` 屬性傳入 BLL `SelectMethod`，來實作為排序和自訂分頁的 GridView。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Carlos Santos。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](efficiently-paging-through-large-amounts-of-data-cs.md)
> [下一頁](creating-a-customized-sorting-user-interface-cs.md)
