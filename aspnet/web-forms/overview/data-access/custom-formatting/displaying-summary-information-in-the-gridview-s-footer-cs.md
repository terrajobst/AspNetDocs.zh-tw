---
uid: web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
title: 在 GridView 的頁尾中顯示摘要資訊（C#） |Microsoft Docs
author: rick-anderson
description: 摘要資訊通常會顯示在報表底部的摘要資料列中。 GridView 控制項可以將頁尾資料列包含在我們可以 pr 的資料格上 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: d50edc31-9286-4c6a-8635-be09e72752a4
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/displaying-summary-information-in-the-gridview-s-footer-cs
msc.type: authoredcontent
ms.openlocfilehash: b258a2bdeaea8da4e9c5c5d8043b167d94e1e817
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74616764"
---
# <a name="displaying-summary-information-in-the-gridviews-footer-c"></a>在 GridView 的頁尾顯示摘要資訊 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/6/9/969e5c94-dfb6-4e47-9570-d6d9e704c3c1/ASPNET_Data_Tutorial_15_CS.exe)或[下載 PDF](displaying-summary-information-in-the-gridview-s-footer-cs/_static/datatutorial15cs1.pdf)

> 摘要資訊通常會顯示在報表底部的摘要資料列中。 GridView 控制項可以將頁尾資料列包含在中，我們可以用程式設計的方式插入匯總資料。 在本教學課程中，我們將瞭解如何在此頁尾資料列中顯示匯總資料。

## <a name="introduction"></a>簡介

除了查看每項產品的價格、庫存單位、訂購單位和重新排序層級以外，使用者可能也會想要匯總資訊，例如平均價格、庫存單位總數等等。 這類摘要資訊通常會顯示在報表底部的摘要資料列中。 GridView 控制項可以將頁尾資料列包含在中，我們可以用程式設計的方式插入匯總資料。

這項工作為我們帶來三個挑戰：

1. 設定 GridView 以顯示其頁尾資料列
2. 判斷摘要資料;也就是，我們要如何計算存貨中的平均價格或總單位數？
3. 將摘要資料插入頁尾資料列的適當資料格中

在本教學課程中，我們將瞭解如何克服這些挑戰。 具體而言，我們將建立一個頁面，其中列出在 GridView 中顯示所選類別產品的下拉式清單中的分類。 GridView 會包含頁尾資料列，其中顯示該類別中產品的平均價格和總單位數。

[![摘要資訊會顯示在 GridView 的頁尾資料列中](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image2.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image1.png)

**圖 1**：摘要資訊會顯示在 GridView 的頁尾資料列中（[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image3.png)）

本教學課程及其類別對產品的主要/詳細資料介面，建基於先前的[主要/詳細資料篩選 DropDownList](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)教學課程中所涵蓋的概念。 如果您尚未進行過先前的教學課程，請先執行這項操作，再繼續進行此操作。

## <a name="step-1-adding-the-categories-dropdownlist-and-products-gridview"></a>步驟1：新增類別 DropDownList 和 Products GridView

在將摘要資訊新增至 GridView 的頁尾之前，讓我們先建立主要/詳細資料包表。 完成第一個步驟之後，我們將探討如何包含摘要資料。

從開啟 [`CustomFormatting`] 資料夾中的 [`SummaryDataInFooter.aspx`] 頁面開始。 新增 DropDownList 控制項，並將其 `ID` 設定為 `Categories`。 接下來，按一下 DropDownList 的智慧標籤中的 [選擇資料來源] 連結，並加入宣告名為 `CategoriesDataSource` 的新 ObjectDataSource，以叫用 `CategoriesBLL` 類別的 `GetCategories()` 方法。

[![新增名為 CategoriesDataSource 的新 ObjectDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image5.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image4.png)

**圖 2**：新增名為 `CategoriesDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image6.png)）

[![讓 ObjectDataSource 叫用 CategoriesBLL 類別的 GetCategories （）方法](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image8.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image7.png)

**圖 3**：讓 ObjectDataSource 叫用 `CategoriesBLL` 類別的 `GetCategories()` 方法（[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image9.png)）

設定 ObjectDataSource 之後，嚮導會將我們傳回到 DropDownList 的資料來源設定 wizard，我們必須在其中指定要顯示的資料欄值，以及哪一個應該對應至 DropDownList 的 `ListItem` 的值。 顯示 [`CategoryName`] 欄位，並使用 `CategoryID` 做為值。

[![分別使用 [類別] 和 [類別名稱] 欄位做為 ListItems 的文字和值](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image11.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image10.png)

**圖 4**：分別使用 [`CategoryName`] 和 [`CategoryID`] 欄位作為 `ListItem` 的 `Text` 和 `Value` （[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image12.png)）

此時，我們有一個 DropDownList （`Categories`），其中列出系統中的類別。 我們現在需要加入 GridView，其中列出屬於所選類別目錄的產品。 不過，在這麼做之前，請花點時間檢查 DropDownList 的智慧標籤中的 [啟用 AutoPostBack] 核取方塊。 如使用 DropDownList 教學課程的*主要/詳細資料篩選*中所述，將 DropDownList 的 `AutoPostBack` 屬性設定為，`true` 每當 DropDownList 值變更時，頁面就會回傳。 這會導致 GridView 重新整理，並顯示新選取之類別目錄的產品。 如果 `AutoPostBack` 屬性設為 `false` （預設值），則變更分類不會導致回傳，因此不會更新列出的產品。

[![核取 DropDownList 的智慧標籤中的 [啟用 AutoPostBack] 核取方塊](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image14.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image13.png)

[**圖 5**]：核取 DropDownList 的智慧標籤中的 [啟用 AutoPostBack] 核取方塊（[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image15.png)）

將 GridView 控制項新增至頁面，以顯示所選類別目錄的產品。 將 GridView 的 `ID` 設定為 `ProductsInCategory`，並將它系結至名為 `ProductsInCategoryDataSource`的新 ObjectDataSource。

[![新增名為 ProductsInCategoryDataSource 的新 ObjectDataSource](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image17.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image16.png)

**圖 6**：新增名為 `ProductsInCategoryDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image18.png)）

設定 ObjectDataSource，使其叫用 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法。

[![讓 ObjectDataSource 叫用 GetProductsByCategoryID （類別 Id）方法](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image20.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image19.png)

**圖 7**：讓 ObjectDataSource 叫用 `GetProductsByCategoryID(categoryID)` 方法（[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image21.png)）

由於 `GetProductsByCategoryID(categoryID)` 方法會採用輸入參數，因此我們可以在 wizard 的最後一個步驟中指定參數值的來源。 若要顯示所選類別中的這些產品，請將參數從 `Categories` DropDownList 中提取。

[![從選取的 [類別] DropDownList 取得 [類別目錄] 參數值](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image23.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image22.png)

**圖 8**：從選取的類別 DropDownList 取得 *`categoryID`* 參數值（[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image24.png)）

完成 wizard 之後，GridView 會有每個產品屬性的 BoundField。 讓我們清除這些 BoundFields，以便只顯示 `ProductName`、`UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` BoundFields。 您可以隨意將任何欄位層級設定加入至其餘的 BoundFields （例如，將 `UnitPrice` 格式化為貨幣）。 進行這些變更之後，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample1.aspx)]

此時，我們有一個功能完整的主要/詳細資料包表，其中顯示屬於所選類別之產品的名稱、單位價格、庫存單位和單位順序。

[![從選取的 [類別] DropDownList 取得 [類別目錄] 參數值](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image26.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image25.png)

**圖 9**：從選取的類別 DropDownList 取得 *`categoryID`* 參數值（[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image27.png)）

## <a name="step-2-displaying-a-footer-in-the-gridview"></a>步驟2：在 GridView 中顯示頁尾

GridView 控制項可以同時顯示頁首和頁尾資料列。 這些資料列會分別根據 [`ShowHeader`] 和 [`ShowFooter`] 屬性的值來顯示，`ShowHeader` 預設為 [`true`]，`ShowFooter` 為 [`false`]。 若要在 GridView 中包含頁尾，只要將其 `ShowFooter` 屬性設為 `true`即可。

[![將 GridView 的 ShowFooter 屬性設定為 true](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image29.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image28.png)

**圖 10**：將 GridView 的 `ShowFooter` 屬性設定為 `true` （[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image30.png)）

頁尾資料列具有 GridView 中所定義之每個欄位的資料格;不過，這些資料格預設是空的。 花點時間在瀏覽器中觀看進度。 當 `ShowFooter` 屬性現在設定為 [`true`] 時，GridView 會包含空的頁尾資料列。

[![GridView 現在包含頁尾資料列](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image32.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image31.png)

**圖 11**： GridView 現在包含頁尾資料列（[按一下以查看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image33.png)）

[圖 11] 中的頁尾資料列並不會有白色的背景。 讓我們在指定深紅色背景的 `Styles.css` 中建立一個 `FooterStyle` 的 CSS 類別，然後在 `DataWebControls` 主題中設定 `GridView.skin` 的外觀檔，將此 CSS 類別指派給 GridView 的 `FooterStyle`的 `CssClass` 屬性。 如果您需要在面板和主題上進行筆刷，請回頭參閱[使用 ObjectDataSource 顯示資料](../basic-reporting/displaying-data-with-the-objectdatasource-cs.md)教學課程。

首先，將下列 CSS 類別新增至 `Styles.css`：

[!code-css[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample2.css)]

`FooterStyle` CSS 類別與 `HeaderStyle` 類別的樣式相似，雖然 `HeaderStyle`的背景色彩奧妙較暗，而且其文字會以粗體字型顯示。 此外，頁尾中的文字會靠右對齊，而標頭的文字則會置中。

接下來，若要將此 CSS 類別與每個 GridView 的頁尾產生關聯，請開啟 `DataWebControls` 主題中的 `GridView.skin` 檔案，並設定 `FooterStyle`的 `CssClass` 屬性。 在此加法之後，檔案的標記應該如下所示：

[!code-aspx[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample3.aspx)]

如下面的螢幕擷取畫面所示，這種變更使頁尾更清楚。

[![GridView 的頁尾資料列現在有 Reddish 的背景色彩](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image35.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image34.png)

**圖 12**： GridView 的頁尾資料列現在有 Reddish 的背景色彩（[按一下以觀看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image36.png)）

## <a name="step-3-computing-the-summary-data"></a>步驟3：計算摘要資料

顯示 GridView 的頁尾後，下一個挑戰就是如何計算摘要資料。 有兩種方式可計算此匯總資訊：

1. 透過 SQL 查詢，我們可以對資料庫發出額外的查詢，以計算特定類別的摘要資料。 SQL 包含許多彙總函式以及 `GROUP BY` 子句，以指定資料應該摘要的資料。 下列 SQL 查詢會取回所需的資訊：  

    [!code-sql[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample4.sql)]

    當然，您不想直接從 `SummaryDataInFooter.aspx` 頁面發出此查詢，而是在 `ProductsTableAdapter` 和 `ProductsBLL`中建立方法。
2. 如[根據資料進行自訂格式](custom-formatting-based-upon-data-cs.md)教學課程中所述，將這項資訊新增至 gridview 時，將其計算，而 gridview 的 `RowDataBound` 事件處理常式會針對每個在其資料系結之後加入至 Gridview 的資料列，引發一次。 藉由建立此事件的事件處理常式，我們可以保留要匯總之值的總計。 在最後一個資料列已系結至 GridView 之後，我們擁有計算平均值所需的總計和資訊。

我通常會採用第二種方法，因為它會儲存資料庫的旅程，以及在資料存取層和商務邏輯層中執行摘要功能所需的工作，但這兩種方法都已足夠。 在本教學課程中，我們將使用第二個選項，並使用 `RowDataBound` 事件處理常式追蹤執行總計。

建立 GridView 的 `RowDataBound` 事件處理常式，方法是在設計工具中選取 GridView，按一下屬性視窗中的閃電圖示，然後按兩下 [`RowDataBound`] 事件。 這會在 `SummaryDataInFooter.aspx` 頁面的程式碼後置類別中，建立名為 `ProductsInCategory_RowDataBound` 的新事件處理常式。

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample5.cs)]

為了維持總計的執行，我們需要在事件處理常式的範圍之外定義變數。 建立下列四個頁面層級的變數：

- `_totalUnitPrice`，屬於類型 `decimal`
- `_totalNonNullUnitPriceCount`，屬於類型 `int`
- `_totalUnitsInStock`，屬於類型 `int`
- `_totalUnitsOnOrder`，屬於類型 `int`

接下來，撰寫程式碼，為 `RowDataBound` 事件處理常式中遇到的每個資料列遞增這三個變數。

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample6.cs)]

`RowDataBound` 事件處理常式一開始會先確保我們處理的是 DataRow。 一旦建立之後，只系結至 `e.Row` 中 `GridViewRow` 物件的 `Northwind.ProductsRow` 實例會儲存在 `product`變數中。 接下來，執行總計變數會以目前產品的對應值遞增（假設它們不包含資料庫 `NULL` 值）。 我們會追蹤執行中的 `UnitPrice` 總計和非`NULL` 的 `UnitPrice` 記錄數目，因為平均價格是這兩個數字的商。

## <a name="step-4-displaying-the-summary-data-in-the-footer"></a>步驟4：在頁尾中顯示摘要資料

匯總摘要資料之後，最後一個步驟是將它顯示在 GridView 的頁尾資料列中。 您也可以透過 `RowDataBound` 事件處理常式，以程式設計方式完成這項工作。 回想一下，針對系結至 GridView 的*每個*資料列（包括頁尾資料列），會引發 `RowDataBound` 事件處理常式。 因此，我們可以使用下列程式碼來擴充事件處理常式，以顯示頁尾資料列中的資料：

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample7.cs)]

由於在加入所有資料列之後，會將頁尾資料列加入 GridView 中，因此我們可以放心地，我們已經準備好要在頁尾中顯示摘要資料，而執行中的總計算將已完成。 最後一個步驟是在頁尾的儲存格中設定這些值。

若要顯示特定頁尾資料格中的文字，請使用 `e.Row.Cells[index].Text = value`，其中 `Cells` 索引從0開始。 下列程式碼會計算平均價格（除以產品數目的總價格），並將其顯示在 GridView 適當頁尾資料格中的庫存單位總數和單位數。

[!code-csharp[Main](displaying-summary-information-in-the-gridview-s-footer-cs/samples/sample8.cs)]

[圖 13] 顯示此程式碼加入後的報表。 請注意，`ToString("c")` 如何使平均價格摘要資訊的格式與貨幣類似。

[![GridView 的頁尾資料列現在有 Reddish 的背景色彩](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image38.png)](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image37.png)

**圖 13**： GridView 的頁尾資料列現在有 Reddish 的背景色彩（[按一下以觀看完整大小的影像](displaying-summary-information-in-the-gridview-s-footer-cs/_static/image39.png)）

## <a name="summary"></a>總結

顯示摘要資料是常見的報表需求，而 GridView 控制項可讓您輕鬆地在其頁尾資料列中加入這類資訊。 當 GridView 的 `ShowFooter` 屬性設定為 `true`，而且可以透過 `RowDataBound` 事件處理常式以程式設計方式設定其資料格內的文字時，就會顯示頁尾資料列。 您可以重新查詢資料庫，或使用 ASP.NET 網頁程式碼後置類別中的程式碼，以程式設計方式計算摘要資料，來計算摘要資料。

本教學課程將說明如何使用 GridView、DetailsView 和 FormView 控制項來檢查自訂格式。 我們的下一個教學課程會開始探索如何使用這些相同的控制項來插入、更新和刪除資料。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](using-the-formview-s-templates-cs.md)
> [下一頁](custom-formatting-based-upon-data-vb.md)
