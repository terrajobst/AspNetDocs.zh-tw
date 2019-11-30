---
uid: web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
title: 從 GridView 的頁尾插入新記錄（VB） |Microsoft Docs
author: rick-anderson
description: 雖然 GridView 控制項並未提供插入新記錄資料的內建支援，但本教學課程會示範如何擴大 GridView 以包含 。
ms.author: riande
ms.date: 03/06/2007
ms.assetid: 528acc48-f20c-4b4e-aa16-4cc02f068ebb
msc.legacyurl: /web-forms/overview/data-access/enhancing-the-gridview/inserting-a-new-record-from-the-gridview-s-footer-vb
msc.type: authoredcontent
ms.openlocfilehash: 67ef370a90bc843f5c2da80bb43c8ef8de216b51
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74631943"
---
# <a name="inserting-a-new-record-from-the-gridviews-footer-vb"></a>從 GridView 的頁尾插入新記錄 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/4/a/7/4a7a3b18-d80e-4014-8e53-a6a2427f0d93/ASPNET_Data_Tutorial_53_VB.exe)或[下載 PDF](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/datatutorial53vb1.pdf)

> 雖然 GridView 控制項並未提供插入新記錄資料的內建支援，但本教學課程會示範如何擴大 GridView 以包含插入介面。

## <a name="introduction"></a>簡介

如如何[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教學課程中所述，GridView、DetailsView 和 FormView Web 控制項各包含內建的資料修改功能。 搭配宣告式資料來源控制項使用時，可以快速且輕鬆地設定這三個 Web 控制項，以修改資料和案例，而不需要撰寫任何一行程式碼。 可惜的是，只有 DetailsView 和 FormView 控制項提供內建的插入、編輯和刪除功能。 GridView 僅提供編輯和刪除支援。 不過，有一個小的肘矽脂，我們可以擴大 GridView 以包含插入介面。

在加入 GridView 的插入功能時，我們會負責決定新記錄的新增方式、建立插入介面，以及撰寫程式碼來插入新的記錄。 在本教學課程中，我們將探討如何將插入介面新增至 GridView s 頁尾資料列（請參閱 [圖 1]）。 每個資料行的頁尾儲存格都包含適當的資料集合用戶介面元素（產品名稱的 TextBox、供應商的 DropDownList 等等）。 我們也需要一個 [加入] 按鈕的資料行，當按下時，將會導致回傳，並使用頁尾資料列中提供的值，將新記錄插入 `Products` 資料表。

[![頁尾資料列提供用於加入新產品的介面](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image1.png)

**圖 1**：頁尾資料列提供用於加入新產品的介面（[按一下以觀看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.png)）

## <a name="step-1-displaying-product-information-in-a-gridview"></a>步驟1：在 GridView 中顯示產品資訊

在我們考慮如何在 GridView 的頁尾中建立插入介面之前，讓我們先專注于將 GridView 加入至列出資料庫中產品的頁面。 一開始先開啟 [`EnhancedGridView`] 資料夾中的 [`InsertThroughFooter.aspx`] 頁面，然後從 [工具箱] 將 [GridView] 拖曳至設計工具，將 [GridView] `ID` 屬性設定為 [`Products`]。 接下來，使用 GridView 的智慧標籤，將它系結至名為 `ProductsDataSource`的新 ObjectDataSource。

[![建立名為 ProductsDataSource 的新 ObjectDataSource](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image2.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.png)

**圖 2**：建立名為 `ProductsDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.png)）

設定 ObjectDataSource 使用 `ProductsBLL` 類別的 `GetProducts()` 方法來取出產品資訊。 在本教學課程中，讓我們完全專注于新增插入功能，而不需要擔心編輯和刪除。 因此，請確定 [插入] 索引標籤中的下拉式清單已設定為 [`AddProduct()`]，而且 [更新] 和 [刪除] 索引標籤中的下拉式清單已設定為 [（無）]。

[![將 AddProduct 方法對應至 ObjectDataSource s Insert （）方法](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image3.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.png)

**圖 3**：將 `AddProduct` 方法對應至 ObjectDataSource s `Insert()` 方法（[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.png)）

[![將 [更新] 和 [刪除] 索引標籤下拉式清單設定為 [（無）]](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image4.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.png)

**圖 4**：將 [更新] 和 [刪除] 索引標籤下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.png)）

完成 ObjectDataSource s 設定資料來源 wizard 之後，Visual Studio 會自動為每個對應的資料欄位，將欄位加入至 GridView。 現在，請保留 Visual Studio 新增的所有欄位。 稍後在本教學課程中，我們將傳回並移除在加入新記錄時，不需要指定其值的部分欄位。

由於資料庫中的產品已接近80，因此使用者必須在網頁底部向下滾動，才能加入新的記錄。 因此，讓我們啟用分頁，讓插入介面更為可見且可供存取。 若要開啟分頁，只要勾選 GridView 的智慧標籤中的 [啟用分頁] 核取方塊即可。

此時，GridView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample1.aspx)]

[![所有產品資料欄位都會顯示在分頁 GridView 中](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image5.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.png)

**圖 5**：所有產品資料欄位都會顯示在分頁 GridView 中（[按一下以觀看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.png)）

## <a name="step-2-adding-a-footer-row"></a>步驟2：加入頁尾資料列

除了其標頭和資料列之外，GridView 還包含頁尾資料列。 [頁首] 和 [頁尾] 資料列會根據 GridView 的[`ShowHeader`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showheader.aspx)和[`ShowFooter`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.showfooter.aspx)屬性的值來顯示。 若要顯示頁尾資料列，只要將 [`ShowFooter`] 屬性設為 [`True`] 即可。 如 [圖 6] 所示，將 `ShowFooter` 屬性設為 `True` 會在方格中加入頁尾資料列。

[![若要顯示頁尾資料列，請將 ShowFooter 設定為 True。](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image6.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.png)

**圖 6**：若要顯示頁尾資料列，請將 `ShowFooter` 設定為 `True` （[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.png)）

請注意，頁尾資料列具有深紅色的背景色彩。 這是因為我們所建立的 DataWebControls 主題，並套用至使用 ObjectDataSource 教學課程[顯示資料](../basic-reporting/displaying-data-with-the-objectdatasource-vb.md)中的所有頁面。 具體而言，`GridView.skin` 檔案會設定 `FooterStyle` 屬性，這會使用 `FooterStyle` 的 CSS 類別。 `FooterStyle` 類別定義于 `Styles.css` 中，如下所示：

[!code-css[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample2.css)]

> [!NOTE]
> 我們曾在先前的教學課程中使用 GridView 的頁尾資料列。 如有需要，請回到在[GridView 的頁尾教學課程中顯示摘要資訊](../custom-formatting/displaying-summary-information-in-the-gridview-s-footer-vb.md)，以取得重新整理程式。

將 [`ShowFooter`] 屬性設定為 [`True`] 之後，請花一點時間在瀏覽器中查看輸出。 頁尾資料列目前不會包含任何文字或 Web 控制項。 在步驟3中，我們將修改每個 GridView 欄位的頁尾，使其包含適當的插入介面。

[![空白頁尾資料列顯示在分頁介面控制項上方](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image7.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image13.png)

**圖 7**：空白頁尾資料列會顯示在分頁介面控制項上方（[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image14.png)）

## <a name="step-3-customizing-the-footer-row"></a>步驟3：自訂頁尾資料列

回到 GridView 控制項教學課程中的[使用 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-vb.md) ，我們已瞭解如何使用 TemplateFields （相對於 BoundFields 或 CheckBoxFields），大幅自訂特定 GridView 資料行的顯示;在[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)中，我們探討了如何使用 TemplateFields 自訂 GridView 中的編輯介面。 回想一下，TemplateField 是由許多樣板組成，這些範本定義了用於特定資料列類型的標記、Web 控制項和資料系結語法混合。 例如，`ItemTemplate`會指定用於唯讀資料列的範本，而 `EditItemTemplate` 則會定義可編輯資料列的範本。

除了 `ItemTemplate` 和 `EditItemTemplate`之外，TemplateField 也包含指定頁尾資料列內容的 `FooterTemplate`。 因此，我們可以將每個欄位插入介面所需的 Web 控制項新增至 `FooterTemplate`。 若要開始，請將 GridView 中的所有欄位轉換成 TemplateFields。 若要這麼做，您可以按一下 GridView 的智慧標籤中的 [編輯資料行] 連結，選取左下角的每個欄位，然後按一下 [將此欄位轉換成 TemplateField] 連結。

![將每個欄位轉換成 TemplateField](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image8.gif)

**圖 8**：將每個欄位轉換成 TemplateField

按一下 [將此欄位轉換成 TemplateField]，會將目前的欄位類型變成相等的 TemplateField。 例如，會將每個 BoundField 取代為具有 `ItemTemplate` 的 TemplateField，其中包含的標籤會顯示對應的資料欄位，以及顯示文字方塊中資料欄位的 `EditItemTemplate`。 `ProductName` BoundField 已轉換成下列 TemplateField 標記：

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample3.aspx)]

同樣地，`Discontinued` CheckBoxField 已轉換成 TemplateField，其 `ItemTemplate` 和 `EditItemTemplate` 包含核取方塊 Web 控制項（已停用 [`ItemTemplate` s] 核取方塊）。 唯讀 `ProductID` BoundField 已轉換成 TemplateField，並在 `ItemTemplate` 和 `EditItemTemplate`中具有標籤控制項。 簡言之，將現有的 GridView 欄位轉換成 TemplateField，可以快速又輕鬆地切換到可自訂的 TemplateField，而不會遺失任何現有的欄位功能。

由於我們重新使用的 GridView 不支援編輯，因此您可以自由地從每個 TemplateField 移除 `EditItemTemplate`，只留下 `ItemTemplate`。 這麼做之後，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample4.aspx)]

既然已將每個 GridView 欄位轉換成 TemplateField，就可以在每個欄位中輸入適當的插入介面 `FooterTemplate`。 某些欄位將不會有插入介面（例如`ProductID`）;有些則會因用來收集新產品資訊的 Web 控制項而有所不同。

若要建立編輯介面，請從 GridView 的智慧標籤選擇 [編輯範本] 連結。 然後從下拉式清單中選取適當的欄位 `FooterTemplate`，並將適當的控制項從 [工具箱] 拖曳至設計工具。

[![將適當的插入介面新增至每個欄位 FooterTemplate](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image9.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image15.png)

**圖 9**：將適當的插入介面新增至每個欄位 `FooterTemplate` （[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image16.png)）

下列項目符號清單會列舉 GridView 欄位，並指定要加入的插入介面：

- `ProductID` 無。
- `ProductName` 新增文字方塊，並將其 `ID` 設定為 [`NewProductName`]。 也請新增 RequiredFieldValidator 控制項，以確保使用者輸入新產品名稱的值。
- `SupplierID` 無。
- `CategoryID` 無。
- `QuantityPerUnit` 新增文字方塊，並將其 `ID` 設定為 [`NewQuantityPerUnit`]。
- `UnitPrice` 新增名為 `NewUnitPrice` 的 TextBox 和 CompareValidator，以確保輸入的值是大於或等於零的貨幣值。
- `UnitsInStock` 使用其 `ID` 設定為 `NewUnitsInStock`的文字方塊。 包含 CompareValidator，可確保輸入的值是大於或等於零的整數值。
- `UnitsOnOrder` 使用其 `ID` 設定為 `NewUnitsOnOrder`的文字方塊。 包含 CompareValidator，可確保輸入的值是大於或等於零的整數值。
- `ReorderLevel` 使用其 `ID` 設定為 `NewReorderLevel`的文字方塊。 包含 CompareValidator，可確保輸入的值是大於或等於零的整數值。
- `Discontinued` 新增核取方塊，將其 `ID` 設定為 [`NewDiscontinued`]。
- `CategoryName` 新增 DropDownList，並將其 `ID` 設定為 [`NewCategoryID`]。 將它系結至名為 `CategoriesDataSource` 的新 ObjectDataSource，並將其設定為使用 `CategoriesBLL` 類別 s `GetCategories()` 方法。 讓 DropDownList 的 `ListItem` s 顯示 `CategoryName` 資料欄位，並使用 `CategoryID` 資料欄位作為其值。
- `SupplierName` 新增 DropDownList，並將其 `ID` 設定為 [`NewSupplierID`]。 將它系結至名為 `SuppliersDataSource` 的新 ObjectDataSource，並將其設定為使用 `SuppliersBLL` 類別 s `GetSuppliers()` 方法。 讓 DropDownList 的 `ListItem` s 顯示 `CompanyName` 資料欄位，並使用 `SupplierID` 資料欄位作為其值。

針對每個驗證控制項，清除 [`ForeColor`] 屬性，如此就會使用 `FooterStyle` CSS 類別的白色前景色彩來取代預設的紅色。 此外，也請使用 `ErrorMessage` 屬性來取得詳細描述，但將 `Text` 屬性設定為星號。 若要防止驗證控制項的文字導致插入介面換行兩行，請針對每個使用驗證控制項的 `FooterTemplate`，將 `FooterStyle` s `Wrap` 屬性設為 false。 最後，在 GridView 底下新增 ValidationSummary 控制項，並將其 [`ShowMessageBox`] 屬性設為 [`True`]，並將其 `ShowSummary` 屬性設定為 [`False`]。

加入新產品時，我們必須提供 `CategoryID` 和 `SupplierID`。 這項資訊是透過 [`CategoryName`] 和 [`SupplierName`] 欄位之頁尾資料格中的 Dropdownlist 進行來捕捉。 我選擇使用這些欄位，而不是 `CategoryID` 和 `SupplierID` TemplateFields，因為在方格的資料列中，使用者可能會更有興趣看到類別目錄和供應商名稱，而不是其識別碼值。 因為 `CategoryID` 和 `SupplierID` 值現在會在 `CategoryName` 中捕捉，而 `SupplierName` 欄位 s 插入介面，所以我們可以從 GridView 移除 `CategoryID` 和 `SupplierID` TemplateFields。

同樣地，當加入新產品時，不會使用 `ProductID`，因此也可以移除 `ProductID` TemplateField。 不過，讓 s 離開方格中的 [`ProductID`] 欄位。 除了組成插入介面的 [textbox]、[Dropdownlist 進行]、[核取方塊] 和 [驗證] 控制項外，我們也需要 [新增] 按鈕，當您按下時，會執行邏輯以將新產品加入至資料庫。 在步驟4中，我們會在 `ProductID` TemplateField s `FooterTemplate`的插入介面中包含 [新增] 按鈕。

歡迎您改善各種 GridView 欄位的外觀。 例如，您可能想要將 `UnitPrice` 值格式化為貨幣、將 `UnitsInStock`、`UnitsOnOrder`和 `ReorderLevel` 欄位靠右對齊，並更新 TemplateFields 的 `HeaderText` 值。

建立在 `FooterTemplate` s 中插入介面、移除 `SupplierID`和 `CategoryID` TemplateFields，以及透過格式化和對齊 TemplateFields 來改善方格美學的許多之後，GridView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample5.aspx)]

透過瀏覽器觀看時，GridView 的頁尾資料列現在包含已完成的插入介面（請參閱 [圖 10]）。 此時，插入介面不會包含使用者指示她輸入新產品的資料，而且想要在資料庫中插入新記錄的方法。 此外，我們還不會處理輸入頁尾的資料如何轉譯成 `Products` 資料庫中的新記錄。 在步驟4中，我們將探討如何在插入介面中包含 [新增] 按鈕，以及如何在按下時執行回傳程式碼。 步驟5顯示如何使用頁尾中的資料插入新記錄。

[![GridView 頁尾提供用於新增記錄的介面](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image10.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image17.png)

**圖 10**： GridView 頁尾提供用於新增記錄的介面（[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image18.png)）

## <a name="step-4-including-an-add-button-in-the-inserting-interface"></a>步驟4：在插入介面中包含 [新增] 按鈕

我們必須在插入介面的某處包含 [加入] 按鈕，因為頁尾資料列的插入介面目前缺少使用者表示已完成輸入新產品資訊的方式。 這可能會放在其中一個現有的 `FooterTemplate` 中，或者我們可以將新的資料行加入到方格中，以供此用途使用。 在本教學課程中，讓我們將 [新增] 按鈕放在 `ProductID` TemplateField s `FooterTemplate`中。

從設計工具中，按一下 GridView s 智慧標籤中的 [編輯範本] 連結，然後從下拉式清單中選擇 [`ProductID`] 欄位 `FooterTemplate`。 將按鈕 Web 控制項（或您偏好的 LinkButton 或 ImageButton）新增至範本，將其識別碼設定為 `AddProduct`、要插入的 `CommandName`，以及要新增的 `Text` 屬性，如 [圖 11] 所示。

[![將 [新增] 按鈕放在 ProductID TemplateField s FooterTemplate](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image11.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image19.png)

**圖 11**：將 [新增] 按鈕放在 `ProductID` TemplateField s `FooterTemplate` （[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image20.png)）

一旦您包含 [新增] 按鈕，請在瀏覽器中測試頁面。 請注意，當您在插入介面中按一下含有無效資料的 [加入] 按鈕時，回傳會是 short 縮短，而 ValidationSummary 控制項會指出不正確資料（請參閱 [圖 12]）。 輸入適當的資料後，按一下 [新增] 按鈕會導致回傳。 但不會將任何記錄新增至資料庫。 我們需要撰寫一些程式碼，才能實際執行插入。

[![如果插入介面中有不正確資料，[新增] 按鈕的回傳是 Short 縮短](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image12.gif)](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image21.png)

**圖 12**：如果插入介面中有不正確資料，[新增] 按鈕的回傳是 Short 縮短（[按一下以查看完整大小的影像](inserting-a-new-record-from-the-gridview-s-footer-vb/_static/image22.png)）

> [!NOTE]
> 插入介面中的驗證控制項未指派給驗證群組。 只要插入介面是頁面上唯一一組驗證控制項，這項功能就能正常運作。 不過，如果頁面上有其他驗證控制項（例如格線編輯介面中的驗證控制項），則插入介面中的驗證控制項和 [加入] 按鈕 `ValidationGroup` 屬性應指派相同的值，以便將這些控制項與特定的驗證群組產生關聯。 如需將頁面上的驗證控制項和按鈕分割成驗證群組的詳細資訊，請參閱[剖析 ASP.NET 2.0 中的驗證控制項](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)。

## <a name="step-5-inserting-a-new-record-into-theproductstable"></a>步驟5：將新記錄插入`Products`資料表

利用 GridView 的內建編輯功能時，GridView 會自動處理執行更新所需的所有工作。 特別的是，按一下 [更新] 按鈕時，它會將輸入自編輯介面的值複製到 ObjectDataSource s `UpdateParameters` 集合中的參數，並藉由叫用 ObjectDataSource 的 `Update()` 方法來啟動更新。 由於 GridView 不會提供這類內建功能來插入，因此我們必須執行程式碼來呼叫 ObjectDataSource s `Insert()` 方法，並將插入介面中的值複製到 ObjectDataSource s `InsertParameters` 集合。

按一下 [新增] 按鈕之後，就應該執行此插入邏輯。 如在 GridView 中[新增和回應按鈕](../custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-vb.md)教學課程中所述，只要按一下 gridview 中的按鈕、LinkButton 或 ImageButton，gridview 的 `RowCommand` 事件就會在回傳時引發。 如果已明確加入 Button、LinkButton 或 ImageButton （例如頁尾資料列中的 [加入] 按鈕），或是 GridView 已自動加入，則會引發此事件（例如，選取 [啟用排序] 時，每個資料行頂端的 LinkButtons，或是選取 [啟用分頁] 時，在分頁介面中 LinkButtons。

因此，若要回應使用者按一下 [加入] 按鈕，我們必須為 GridView 的 `RowCommand` 事件建立事件處理常式。 每當按下 GridView 中的*任何*按鈕、LinkButton 或 ImageButton 時，就會引發此事件，因此，如果傳遞至事件處理常式的 `CommandName` 屬性對應至 [加入] 按鈕（插入）的 `CommandName` 值，我們就一定要繼續進行插入邏輯。 此外，如果驗證控制項報告有效的資料，我們也應該只繼續進行。 為了配合此，請使用下列程式碼建立 `RowCommand` 事件的事件處理常式：

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample6.vb)]

> [!NOTE]
> 您可能想知道事件處理常式 bothers 檢查 `Page.IsValid` 屬性的原因。 畢竟，如果插入介面中提供了不正確資料，就不會抑制回傳嗎？ 只要使用者尚未停用 JavaScript，或已採取步驟來規避用戶端驗證邏輯，這個假設就是正確的。 簡言之，絕對不要完全依賴用戶端驗證;在處理資料之前，一定要先執行伺服器端的有效性檢查。

在步驟1中，我們建立了 `ProductsDataSource` ObjectDataSource，使其 `Insert()` 方法對應到 `ProductsBLL` 類別的 `AddProduct` 方法。 若要將新記錄插入 `Products` 資料表中，我們可以直接叫用 ObjectDataSource s `Insert()` 方法：

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample7.vb)]

現在已叫用 `Insert()` 方法，剩下的工作就是將插入介面的值複製到傳遞給 `ProductsBLL` class s `AddProduct` 方法的參數。 如我們在[檢查與插入、更新和刪除教學課程相關聯的事件](../editing-inserting-and-deleting-data/examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)中所見，您可以透過 ObjectDataSource s `Inserting` 事件來完成這項作業。 在 `Inserting` 事件中，我們需要以程式設計方式參考來自 `Products` GridView s 頁尾資料列的控制項，並將其值指派給 `e.InputParameters` 集合。 如果使用者省略一個值，例如將 [`ReorderLevel`] 文字方塊保留空白，我們必須指定要 `NULL`插入資料庫的值。 由於 `AddProducts` 方法會針對可為 null 的資料庫欄位接受可為 null 的類型，因此只要使用可為 null 的類型，並將其值設定為在省略使用者輸入的情況下 `Nothing`。

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample8.vb)]

當 `Inserting` 事件處理常式完成時，可以透過 GridView 的頁尾資料列，將新記錄加入至 `Products` 資料庫資料表。 請繼續嘗試新增數個新產品。

## <a name="enhancing-and-customizing-the-add-operation"></a>增強和自訂加入作業

目前，按一下 [加入] 按鈕會將新記錄加入至資料庫資料表，但不會提供任何視覺效果意見反應，記錄已成功加入。 在理想的情況下，[標籤 Web 控制項] 或 [用戶端警示] 方塊會通知使用者他們的插入已順利完成。 我將此做為讀者的練習。

本教學課程中使用的 GridView 並不會將任何排序次序套用至列出的產品，也不允許使用者排序資料。 因此，記錄會依照其主要索引鍵欄位在資料庫中排序。 由於每個新記錄的 `ProductID` 值都大於最後一個，因此每次加入新產品時，就會附加到方格的結尾。 因此，在加入新的記錄之後，您可能會想要自動將使用者傳送至 GridView 的最後一頁。 在 `RowCommand` 事件處理常式中的 `ProductsDataSource.Insert()` 呼叫之後加入下列程式程式碼，以指出在將資料系結至 GridView 之後，使用者需要傳送至最後一頁，即可完成這項作業：

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample9.vb)]

`SendUserToLastPage` 是一種頁面層級的布林變數，一開始會指派 `False`的值。 在 GridView 的 `DataBound` 事件處理常式中，如果 `SendUserToLastPage` 為 false，則 `PageIndex` 屬性會更新，以將使用者傳送至最後一頁。

[!code-vb[Main](inserting-a-new-record-from-the-gridview-s-footer-vb/samples/sample10.vb)]

在 `DataBound` 事件處理常式中設定 `PageIndex` 屬性的原因（相對於 `RowCommand` 事件處理常式）是因為當 `RowCommand` 事件處理常式引發時，我們尚未將新記錄加入至 `Products` 資料庫資料表。 因此，在 `RowCommand` 事件處理常式中，最後一頁索引（`PageCount - 1`）表示在加入新產品*之前*的最後一頁索引。 對於大部分新增的產品而言，加入新的產品之後，最後一頁的索引會是相同的。 但當新增的產品產生新的最後一頁索引時，如果我們不正確地更新 `RowCommand` 事件處理常式中的 `PageIndex`，就會進入倒數第二頁（加入新產品之前的最後一頁索引），而不是新的最後一頁索引。 由於 `DataBound` 事件處理常式會在加入新產品並將資料重新系結到方格後引發 `PageIndex`，因此我們知道我們會取得正確的最後一頁索引。

最後，在本教學課程中使用的 GridView 非常寬，因為必須針對加入新產品而收集的欄位數目。 由於此寬度的緣故，可能會偏好 DetailsView s 垂直版面配置。 藉由收集較少的輸入，可以減少 GridView 的整體寬度。 我們可能不需要在加入新產品時收集 `UnitsOnOrder`、`UnitsInStock`和 `ReorderLevel` 欄位，在此情況下，可以從 GridView 移除這些欄位。

若要調整所收集的資料，我們可以使用兩種方法的其中一種：

- 繼續使用預期 `UnitsOnOrder`、`UnitsInStock`和 `ReorderLevel` 欄位值的 `AddProduct` 方法。 在 `Inserting` 事件處理常式中，提供硬式編碼的預設值，以用於已從插入介面移除的這些輸入。
- 在不接受 `UnitsOnOrder`、`UnitsInStock`和 `ReorderLevel` 欄位輸入的 `ProductsBLL` 類別中，建立 `AddProduct` 方法的新多載。 然後，在 [ASP.NET] 頁面中，將 ObjectDataSource 設定為使用這個新的多載。

任一選項也會同樣地運作。 在過去的教學課程中，我們使用了第二個選項，為 `ProductsBLL` 類別 s `UpdateProduct` 方法建立多個多載。

## <a name="summary"></a>總結

GridView 缺少 DetailsView 和 FormView 中的內建插入功能，但在頁尾資料列中加入插入介面的工作也不多。 若要在 GridView 中顯示頁尾資料列，只要將其 `ShowFooter` 屬性設為 `True`即可。 您可以針對每個欄位自訂頁尾資料列內容，方法是將欄位轉換為 TemplateField，並將插入介面新增至 `FooterTemplate`。 如我們在本教學課程中所見，`FooterTemplate` 可以包含按鈕、文字方塊、Dropdownlist 進行、核取方塊、用來填入資料驅動 Web 控制項（例如 Dropdownlist 進行）和驗證控制項的資料來源控制項。 除了用來收集使用者輸入的控制項之外，還需要加入按鈕、LinkButton 或 ImageButton。

按一下 [新增] 按鈕時，會叫用 ObjectDataSource s `Insert()` 方法來啟動插入工作流程。 然後，ObjectDataSource 會呼叫所設定的 insert 方法（在本教學課程中，`ProductsBLL` 類別 s `AddProduct` 方法）。 我們必須先將 GridView s 插入介面的值複製到 ObjectDataSource s `InsertParameters` 集合，然後再叫用 insert 方法。 藉由以程式設計方式參考 ObjectDataSource s `Inserting` 事件處理常式中的插入介面 Web 控制項，即可完成這項作業。

本教學課程會完成我們的探討，以增強 GridView 的外觀。 下一組教學課程將探討如何使用二進位資料，例如影像、Pdf、Word 檔等，以及資料 Web 控制項。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Bernadette Leigh。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一篇](adding-a-gridview-column-of-checkboxes-vb.md)
