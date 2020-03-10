---
uid: web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
title: 新增 GridView 的核取方塊欄（VB） |Microsoft Docs
author: rick-anderson
description: 本教學課程探討如何將核取方塊的資料行新增至 GridView 控制項，以提供使用者直覺的方式來選取 [G ...] 的多個資料列。
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 39253d05-75c0-41c7-b9d4-a6c58ecf69ce
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/adding-a-gridview-column-of-checkboxes-vb
msc.type: authoredcontent
ms.openlocfilehash: c620b2eac5844d4030c1309b45e7d6a72d1f386a
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78607349"
---
# <a name="adding-a-gridview-column-of-checkboxes-vb"></a>新增 GridView 的核取方塊欄 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_52_VB.exe)或[下載 PDF](adding-a-gridview-column-of-checkboxes-vb/_static/datatutorial52vb1.pdf)

> 本教學課程探討如何將核取方塊的資料行新增至 GridView 控制項，以提供使用者直覺的方式來選取 GridView 的多個資料列。

## <a name="introduction"></a>簡介

在先前的教學課程中，我們已檢查如何將選項按鈕的資料行加入至 GridView，以供選取特定記錄。 當使用者限制從方格中最多隻選擇一個專案時，選項按鈕的資料行就是適當的使用者介面。 不過有時候，我們可能會想要允許使用者從方格中選取任意數目的專案。 例如，以網頁為基礎的電子郵件客戶程式通常會顯示包含一欄核取方塊的訊息清單。 使用者可以選取任意數目的訊息，然後執行一些動作，例如將電子郵件移到另一個資料夾或刪除它們。

在本教學課程中，我們將瞭解如何加入核取方塊的資料行，以及如何判斷在回傳時已檢查哪些核取方塊。 特別是，我們將建立一個範例，以仔細模擬以 web 為基礎的電子郵件客戶程式使用者介面。 我們的範例會包含一個分頁 GridView，其中列出 `Products` 資料庫資料表中的產品，並在每個資料列中包含一個核取方塊（請參閱 [圖 1]）。 按一下 [刪除選取的產品] 按鈕時，將會刪除選取的產品。

[![每個產品資料列都包含一個核取方塊](adding-a-gridview-column-of-checkboxes-vb/_static/image1.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image1.png)

**圖 1**：每個產品資料列都包含一個核取方塊（[按一下以查看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image2.png)）

## <a name="step-1-adding-a-paged-gridview-that-lists-product-information"></a>步驟1：加入列出產品資訊的分頁 GridView

在我們擔心加入核取方塊的資料行之前，讓我們先專注于在 GridView 中列出支援分頁的產品。 一開始先開啟 [`EnhancedGridView`] 資料夾中的 [`CheckBoxField.aspx`] 頁面，然後從 [工具箱] 將 [GridView] 拖曳至設計工具，將其 `ID` 設定為 [`Products`]。 接下來，選擇將 GridView 系結至名為 `ProductsDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以使用 `ProductsBLL` 類別，並呼叫 `GetProducts()` 方法來傳回資料。 由於此 GridView 會是唯讀的，因此，請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![建立名為 ProductsDataSource 的新 ObjectDataSource](adding-a-gridview-column-of-checkboxes-vb/_static/image2.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image3.png)

**圖 2**：建立名為 `ProductsDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image4.png)）

[![使用 GetProducts （）方法設定 ObjectDataSource 來取得資料](adding-a-gridview-column-of-checkboxes-vb/_static/image3.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image5.png)

**圖 3**：使用 `GetProducts()` 方法設定 ObjectDataSource 來抓取資料（[按一下以查看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image6.png)）

[![將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](adding-a-gridview-column-of-checkboxes-vb/_static/image4.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image7.png)

**圖 4**：將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image8.png)）

完成 [設定資料來源] wizard 之後，Visual Studio 會自動為產品相關的資料欄位建立 BoundColumns 和 CheckBoxColumn。 如同我們在上一個教學課程中所做的一樣，移除所有 `ProductName`、`CategoryName`和 `UnitPrice` BoundFields，並將 `HeaderText` 屬性變更為 [產品]、[類別] 和 [價格]。 設定 `UnitPrice` BoundField，使其值格式化為貨幣。 此外，您也可以從智慧標籤選取 [啟用分頁] 核取方塊，將 GridView 設定為支援分頁。

讓同時新增使用者介面，以刪除選取的產品。 在 GridView 底下新增按鈕 Web 控制項，將其 `ID` 設定為 `DeleteSelectedProducts`，並將其 `Text` 屬性設為刪除選取的產品。 在此範例中，我們只會顯示一則訊息，指出已刪除的產品，而不是實際刪除資料庫中的產品。 為了配合此，請在按鈕下方新增標籤 Web 控制項。 將其識別碼設定為 `DeleteResults`，清除其 `Text` 屬性，並將其 `Visible` 和 `EnableViewState` 屬性設定為 [`False`]。

進行這些變更之後，GridView、ObjectDataSource、Button 和 Label s 宣告式標記應該如下所示：

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample1.aspx)]

花點時間在瀏覽器中觀看頁面（請參閱 [圖 5]）。 此時，您應該會看到前十個產品的名稱、類別和價格。

[![列出前十個產品的名稱、類別和價格](adding-a-gridview-column-of-checkboxes-vb/_static/image5.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image9.png)

**圖 5**：列出前十個產品的名稱、類別和價格（[按一下以觀看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image10.png)）

## <a name="step-2-adding-a-column-of-checkboxes"></a>步驟2：加入核取方塊的資料行

由於 ASP.NET 2.0 包含 CheckBoxField，因此可能會認為它可以用來將核取方塊的資料行新增至 GridView。 可惜的是，這種情況不是如此，因為 CheckBoxField 是設計來搭配布林資料欄位使用。 也就是說，若要使用 CheckBoxField，我們必須指定其值所參考的基礎資料欄位，以判斷是否已核取轉譯的核取方塊。 我們無法使用 CheckBoxField 只包含未核取核取方塊的資料行。

相反地，我們必須新增 TemplateField，並將 CheckBox Web 控制項新增至其 `ItemTemplate`。 請繼續並將 TemplateField 新增至 `Products` GridView，並將它設為第一個（最左邊的）欄位。 從 GridView 的智慧標籤中，按一下 [編輯範本] 連結，然後從 [工具箱] 將 [CheckBox Web 控制項] 拖曳至 [`ItemTemplate`]。 將此核取方塊 `ID` 屬性設定為 [`ProductSelector`]。

[![將名為 ProductSelector 的 CheckBox Web 控制項新增至 TemplateField s ItemTemplate](adding-a-gridview-column-of-checkboxes-vb/_static/image6.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image11.png)

**圖 6**：將名為 `ProductSelector` 的 CheckBox Web 控制項新增至 TemplateField s `ItemTemplate` （[按一下以查看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image12.png)）

新增 [TemplateField] 和 [CheckBox] Web 控制項之後，每個資料列現在都會包含一個核取方塊。 [圖 7] 顯示在新增 TemplateField 和 CheckBox 之後，透過瀏覽器觀看此頁面。

[![每個產品資料列現在都包含一個核取方塊](adding-a-gridview-column-of-checkboxes-vb/_static/image7.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image13.png)

**圖 7**：每個產品資料列現在都包含一個核取方塊（[按一下以觀看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image14.png)）

## <a name="step-3-determining-what-checkboxes-were-checked-on-postback"></a>步驟3：判斷哪些核取方塊已在回傳時檢查

此時，我們有一個核取方塊，但無法判斷哪些核取方塊已在回傳時檢查。 當按一下 [刪除選取的產品] 按鈕時，我們需要知道已檢查哪些核取方塊，才能刪除這些產品。

GridView 的[`Rows` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows.aspx)可讓您存取 GridView 中的資料列。 我們可以逐一查看這些資料列，以程式設計方式存取 CheckBox 控制項，然後查閱其 `Checked` 屬性，以判斷是否已選取此核取方塊。

建立 `DeleteSelectedProducts` 按鈕 Web 控制項 `Click` 事件的事件處理常式，並新增下列程式碼：

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample2.vb)]

`Rows` 屬性會傳回構成 GridView 資料列 `GridViewRow` 實例的集合。 此處的 `For Each` 迴圈會列舉此集合。 針對每個 `GridViewRow` 物件，會使用 `row.FindControl("controlID")`以程式設計方式存取資料列的核取方塊。 如果勾選此核取方塊，則會從 `DataKeys` 集合中抓取對應 `ProductID` 值的資料列。 在此練習中，我們只會在 [`DeleteResults`] 標籤中顯示一則資訊性訊息，不過，在工作的應用程式中，我們會改為呼叫 `ProductsBLL` 類別 s `DeleteProduct(productID)` 方法。

加入此事件處理常式後，按一下 [刪除選取的產品] 按鈕，現在會顯示所選產品的 `ProductID`。

[![按一下 [刪除選取的產品] 按鈕時，會列出選取的產品 ProductIDs](adding-a-gridview-column-of-checkboxes-vb/_static/image8.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image15.png)

**圖 8**：當按一下 [刪除選取的產品] 按鈕時，會列出選取的產品 `ProductID` （[按一下以查看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image16.png)）

## <a name="step-4-adding-check-all-and-uncheck-all-buttons"></a>步驟4：新增全部核取和取消選取所有按鈕

如果使用者想要刪除目前頁面上的所有產品，他們必須檢查十個核取方塊。 我們可以藉由新增 [全選] 按鈕來協助加速此程式，只要按下，就會選取方格中的所有核取方塊。 [取消核取] 按鈕會同樣有用。

將兩個按鈕 Web 控制項新增至頁面，並將其放在 GridView 上方。 將第一個 `ID` 設定為 `CheckAll`，並將其 `Text` 屬性設為 [全部檢查];將第二個 `ID` 設定為 `UncheckAll`，並將其 `Text` 屬性設為 [全部取消選取]。

[!code-aspx[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample3.aspx)]

接下來，在程式碼後置類別中建立名為 `ToggleCheckState(checkState)` 的方法，叫用時，會列舉 `Products` GridView s `Rows` 集合，並將每個核取方塊的 `Checked` 屬性設定為傳入的*checkState*參數值。

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample4.vb)]

接下來，為 [`CheckAll`] 和 [`UncheckAll`] 按鈕建立 `Click` 事件處理常式。 在 `CheckAll` s 事件處理常式中，只要呼叫 `ToggleCheckState(True)`;在 `UncheckAll`中，呼叫 `ToggleCheckState(False)`。

[!code-vb[Main](adding-a-gridview-column-of-checkboxes-vb/samples/sample5.vb)]

使用此程式碼時，按一下 [全選] 按鈕會導致回傳，並檢查 GridView 中的所有核取方塊。 同樣地，按一下 [取消核取所有] 核取方塊。 [圖 9] 顯示勾選 [全部核取] 按鈕之後的畫面。

[![按一下 [全部核取] 按鈕即可選取所有核取方塊](adding-a-gridview-column-of-checkboxes-vb/_static/image9.gif)](adding-a-gridview-column-of-checkboxes-vb/_static/image17.png)

**圖 9**：按一下 [全部核取] 按鈕即可選取所有核取方塊（[按一下以查看完整大小的影像](adding-a-gridview-column-of-checkboxes-vb/_static/image18.png)）

> [!NOTE]
> 顯示覆選框的資料行時，選擇或取消選取所有核取方塊的一種方法是透過標題列中的核取方塊。 此外，目前的勾選全部/取消核取所有執行都需要回傳。 不過，您可以透過用戶端腳本來檢查或取消核取核取方塊，藉此提供更快速得到的使用者體驗。 若要使用 [檢查全部] 和 [取消選取全部] 的標題列核取方塊進行探索，以及使用用戶端技術的討論，請參閱[使用用戶端腳本檢查 GridView 中的所有核取方塊和勾選全部核取方塊](http://aspnet.4guysfromrolla.com/articles/053106-1.aspx)。

## <a name="summary"></a>總結

如果您需要讓使用者從 GridView 選擇任意數目的資料列，再繼續進行，加入核取方塊的資料行是一個選項。 如我們在本教學課程中所見，在 GridView 中包含核取方塊的資料行，需要加入具有 CheckBox Web 控制項的 TemplateField。 藉由使用 Web 控制項（與將標記直接插入範本中，如同我們在先前的教學課程中所做的），ASP.NET 會自動記住哪些核取方塊是，而不是在回傳期間檢查。 我們也可以透過程式設計方式存取程式碼中的核取方塊，以判斷是否已選取指定的核取方塊，或變更已核取的狀態。

本教學課程和最後一個探討如何將資料列選取器資料行加入 GridView。 在下一個教學課程中，我們將探討如何透過一些工作，將插入功能新增至 GridView。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](adding-a-gridview-column-of-radio-buttons-vb.md)
> [下一頁](inserting-a-new-record-from-the-gridview-s-footer-vb.md)
