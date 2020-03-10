---
uid: web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb
title: 使用可選取的主要 GridView 搭配詳細資料 Detailview 之（VB）的主要/詳細資訊 |Microsoft Docs
author: rick-anderson
description: 本教學課程將會有一個 GridView，其資料列包含每個產品的名稱和價格，以及 [選取] 按鈕。 按一下 [particu] 的 [選取] 按鈕 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 1d1a7c93-971d-4690-9c5e-dac0e5014a09
msc.legacyurl: /web-forms/overview/data-access/masterdetail/master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb
msc.type: authoredcontent
ms.openlocfilehash: a953c00acc4c37fd563321477b6b21689d6e686c
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78620901"
---
# <a name="masterdetail-using-a-selectable-master-gridview-with-a-details-detailview-vb"></a>使用具有詳細資料 DetailView 之可選取主要 GridView 的主要/詳細資料 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/d/7/5d7571fc-d0b7-4798-ad4a-c976c02363ce/ASPNET_Data_Tutorial_10_VB.exe)或[下載 PDF](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/datatutorial10vb1.pdf)

> 本教學課程將會有一個 GridView，其資料列包含每個產品的名稱和價格，以及 [選取] 按鈕。 按一下特定產品的 [選取] 按鈕，將會在相同頁面上的 DetailsView 控制項中顯示其完整詳細資料。

## <a name="introduction"></a>簡介

在[上一個教學](master-detail-filtering-across-two-pages-vb.md)課程中，我們已瞭解如何使用兩個網頁來建立主要/詳細資料包表：「主要」網頁，我們會在其中顯示供應商清單;和 [詳細資料] 網頁，列出所選供應商所提供的產品。 這兩個頁面的報表格式可以壓縮成一頁。 本教學課程將會有一個 GridView，其資料列包含每個產品的名稱和價格，以及 [選取] 按鈕。 按一下特定產品的 [選取] 按鈕，將會在相同頁面上的 DetailsView 控制項中顯示其完整詳細資料。

[![按一下 [選取] 按鈕會顯示產品的詳細資料](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image2.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image1.png)

**圖 1**：按一下 [選取] 按鈕會顯示產品的詳細資料（[按一下以查看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image3.png)）

## <a name="step-1-creating-a-selectable-gridview"></a>步驟1：建立可選取的 GridView

回想一下，在兩個分頁的主要/詳細資料包表中，每個主要記錄都包含一個超連結，按下時，就會將使用者傳送至詳細資料頁面，並在查詢字串中傳遞按一下過的資料列 `SupplierID` 值。 這類超連結會使用 HyperLinkField 加入至每個 GridView 資料列。 針對 [單一頁面主要/詳細資料] 報表，每個 GridView 資料列都需要一個按鈕，當按下時，就會顯示詳細資料。 GridView 控制項可以設定為每個導致回傳的資料列都包含 [選取] 按鈕，並將該資料列標示為 GridView 的[SelectedRow](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedrow.aspx)。

首先，將 GridView 控制項新增至 [`Filtering`] 資料夾中的 [`DetailsBySelecting.aspx`] 頁面，將其 `ID` 屬性設定為 [`ProductsGrid`]。 接下來，新增名為 `AllProductsDataSource` 的新 ObjectDataSource，以叫用 `ProductsBLL` 類別的 `GetProducts()` 方法。

[![建立名為 AllProductsDataSource 的 ObjectDataSource](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image5.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image4.png)

**圖 2**：建立名為 `AllProductsDataSource` 的 ObjectDataSource （[按一下以查看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image6.png)）

[![使用 ProductsBLL 類別](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image8.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image7.png)

**圖 3**：使用 `ProductsBLL` 類別（[按一下以觀看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image9.png)）

[![設定 ObjectDataSource 以叫用 GetProducts （）方法](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image11.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image10.png)

**圖 4**：設定 ObjectDataSource 以叫用 `GetProducts()` 方法（[按一下以查看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image12.png)）

編輯 GridView 的欄位移除所有 `ProductName`，但 `UnitPrice` BoundFields。 此外，您也可以視需要隨意自訂這些 BoundFields，例如將 `UnitPrice` BoundField 格式化為貨幣，並變更 BoundFields 的 `HeaderText` 屬性。 您可以從 GridView 的智慧標籤按一下 [編輯資料行] 連結，或手動設定宣告式語法，以圖形方式完成這些步驟。

[![移除所有 [ProductName] 和 [單價] BoundFields](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image14.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image13.png)

**圖 5**：移除所有 `ProductName` 和 `UnitPrice` BoundFields （[按一下以觀看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image15.png)）

GridView 的最終標記為：

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample1.aspx)]

接下來，我們需要將 GridView 標示為可選取，這會在每個資料列中加入一個 [選取] 按鈕。 若要完成這項操作，只要勾選 GridView 智慧標籤中的 [啟用選取範圍] 核取方塊即可。

[![讓 GridView 的資料列可供選取](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image17.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image16.png)

**圖 6**：讓 GridView 的資料列可供選取（[按一下以查看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image18.png)）

勾選 [啟用選取範圍] 選項會將 CommandField 新增至 `ProductsGrid` GridView，並將其 `ShowSelectButton` 屬性設定為 True。 這會導致 GridView 的每個資料列都有 [選取] 按鈕，如 [圖 6] 所示。 根據預設，[選取] 按鈕會轉譯為 LinkButtons，但您可以使用按鈕或 ImageButtons，而不是透過 CommandField 的 `ButtonType` 屬性。

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample2.aspx)]

當 GridView 資料列的 [選取] 按鈕按一下 [回傳接踵而來] 時，會更新 GridView 的 `SelectedRow` 屬性。 除了 `SelectedRow` 屬性以外，GridView 還提供[SelectedIndex](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedindex%28VS.80%29.aspx)、 [SelectedValue](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selectedvalue%28VS.80%29.aspx)和[SelectedDataKey](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.selecteddatakey%28VS.80%29.aspx)屬性。 `SelectedIndex` 屬性會傳回選取之資料列的索引，而 `SelectedValue` 和 `SelectedDataKey` 屬性會根據 GridView 的[DataKeyNames 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.datakeynames%28VS.80%29.aspx)傳回值。

`DataKeyNames` 屬性是用來將一個或多個資料欄值與每個資料列產生關聯，而且通常用來以每個 GridView 資料列來唯一識別基礎資料中的資訊。 `SelectedValue` 屬性會針對選取的資料列傳回第一個 `DataKeyNames` 資料欄位的值，其中，做為 `SelectedDataKey` 屬性會傳回選取的資料列 `DataKey` 物件，其中包含該資料列的指定資料索引鍵欄位的所有值。

當您透過設計工具將資料來源系結至 GridView、DetailsView 或 FormView 時，`DataKeyNames` 屬性會自動設定為唯一識別的資料欄位。 雖然已在先前的教學課程中自動為我們設定此屬性，但在未指定 `DataKeyNames` 屬性的情況下，這些範例仍有作用。 不過，針對本教學課程中可選取的 GridView，以及我們將在其中檢查插入、更新和刪除的後續教學課程，必須正確設定 `DataKeyNames` 屬性。 請花點時間確保 GridView 的 `DataKeyNames` 屬性已設為 `ProductID`。

讓我們透過瀏覽器來觀看我們的進度。 請注意，GridView 會列出所有產品的名稱和價格，以及選取的 LinkButton。 按一下 [選取] 按鈕會導致回傳。 在步驟2中，我們將瞭解如何藉由顯示所選產品的詳細資料，讓 DetailsView 回應此回傳。

[![每個產品資料列都包含 Select LinkButton](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image20.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image19.png)

**圖 7**：每個產品資料列都包含一個 Select LinkButton （[按一下以觀看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image21.png)）

## <a name="highlighting-the-selected-row"></a>反白顯示選取的資料列

`ProductsGrid` GridView 具有 `SelectedRowStyle` 屬性，可以用來為選取的資料列指定視覺化樣式。 使用得當，這可以更清楚地顯示 GridView 目前選取的資料列，以改善使用者的體驗。 在本教學課程中，我們將選取的資料列以黃色背景反白顯示。

如同我們先前的教學課程，讓我們努力將定義為 CSS 類別的美觀相關設定保持在最前面。 因此，請在名為 `SelectedRowStyle`的 `Styles.css` 中建立新的 CSS 類別。

[!code-css[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample3.css)]

若要將此 CSS 類別套用至教學課程系列中*所有*gridview 的 `SelectedRowStyle` 屬性，請編輯 `DataWebControls` 主題中的 `GridView.skin` 面板，以包含 `SelectedRowStyle` 設定，如下所示：

[!code-aspx[Main](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/samples/sample4.aspx)]

透過這種新增，選取的 GridView 資料列現在會以黃色背景色彩反白顯示。

[![使用 GridView 的 SelectedRowStyle 屬性自訂選取的資料列外觀](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image23.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image22.png)

**圖 8**：使用 GridView 的 `SelectedRowStyle` 屬性自訂選取的資料列外觀（[按一下以查看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image24.png)）

## <a name="step-2-displaying-the-selected-products-details-in-a-detailsview"></a>步驟2：在 DetailsView 中顯示所選產品的詳細資料

`ProductsGrid` GridView 完成後，剩下的工作就是新增 DetailsView，以顯示所選特定產品的相關資訊。 在 GridView 上方新增 DetailsView 控制項，並建立名為 `ProductDetailsDataSource`的新 ObjectDataSource。 因為我們想要讓此 DetailsView 顯示所選產品的特定資訊，請將 `ProductDetailsDataSource` 設定為使用 `ProductsBLL` 類別的 `GetProductByProductID(productID)` 方法。

[![叫用 ProductsBLL 類別的 GetProductByProductID （productID）方法](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image26.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image25.png)

**圖 9**：叫用 `ProductsBLL` 類別的 `GetProductByProductID(productID)` 方法（[按一下以查看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image27.png)）

將 *`productID`* 參數的值從 GridView 控制項的 `SelectedValue` 屬性取得。 如先前所述，GridView 的 `SelectedValue` 屬性會傳回所選資料列的第一個資料索引鍵值。 因此，GridView 的 `DataKeyNames` 屬性必須設定為 `ProductID`，如此一來，`SelectedValue`就會傳回選取的資料列 `ProductID` 值。

[![將 productID 參數設定為 GridView 的 SelectedValue 屬性](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image29.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image28.png)

**圖 10**：將 *`productID`* 參數設定為 GridView 的 `SelectedValue` 屬性（[按一下以查看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image30.png)）

一旦 `productDetailsDataSource` ObjectDataSource 已正確設定並系結至 DetailsView，本教學課程就完成了！ 當第一次流覽頁面時，未選取任何資料列，因此 GridView 的 `SelectedValue` 屬性會傳回 `Nothing`。 由於沒有 `NULL` `ProductID` 值的產品，`GetProductByProductID(productID)` 方法不會傳回任何記錄，這表示不會顯示 DetailsView （請參閱 [圖 11]）。 按一下 GridView 資料列的 [選取] 按鈕時，會重新整理回傳接踵而來和 DetailsView。 此時，GridView 的 `SelectedValue` 屬性會傳回所選資料列的 `ProductID`，`GetProductByProductID(productID)` 方法會傳回 `ProductsDataTable`，其中包含該特定產品的相關資訊，而 DetailsView 會顯示這些詳細資料（請參閱 [圖 12]）。

[![第一次造訪時，只會顯示 GridView](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image32.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image31.png)

**圖 11**：第一次造訪時，只會顯示 GridView （[按一下以觀看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image33.png)）

[![選取資料列時，會顯示產品的詳細資料](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image35.png)](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image34.png)

**圖 12**：選取資料列時，會顯示產品的詳細資訊（[按一下以觀看完整大小的影像](master-detail-using-a-selectable-master-gridview-with-a-details-detailview-vb/_static/image36.png)）

## <a name="summary"></a>總結

在此和上述三個教學課程中，我們已看到一些用於顯示主要/詳細資料包表的技術。 在本教學課程中，我們使用可選取的 GridView 來存放主要記錄和 DetailsView，以在相同的頁面上顯示所選主要記錄的詳細資料。 在先前的教學課程中，我們探討了如何使用 Dropdownlist 進行來顯示主版/詳細資料包表，以及在另一個網頁上顯示主要記錄和詳細資料記錄。

本教學課程將結束我們的主要/詳細資料包告檢查。 從下一個教學課程開始，我們將開始探索使用 GridView、DetailsView 和 FormView 的自訂格式。 我們將瞭解如何根據系結的資料自訂這些控制項的外觀、如何摘要 GridView 的頁尾中的資料，以及如何使用範本來取得更大程度的版面配置控制。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Giesenow。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](master-detail-filtering-across-two-pages-vb.md)
