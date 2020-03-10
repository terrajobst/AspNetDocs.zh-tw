---
uid: web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
title: 批次更新（VB） |Microsoft Docs
author: rick-anderson
description: 瞭解如何在單一作業中更新多個資料庫記錄。 在使用者介面層中，我們會建立一個 GridView，其中每個資料列都是可編輯的。 在 [資料 ...]
ms.author: riande
ms.date: 06/26/2007
ms.assetid: d191a204-d7ea-458d-b81c-0b9049ecb55f
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-updating-vb
msc.type: authoredcontent
ms.openlocfilehash: f0bb83b17585876dd6d28a5893a223cce15da31d
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78618360"
---
# <a name="batch-updating-vb"></a>批次更新 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_64_VB.zip)或[下載 PDF](batch-updating-vb/_static/datatutorial64vb1.pdf)

> 瞭解如何在單一作業中更新多個資料庫記錄。 在使用者介面層中，我們會建立一個 GridView，其中每個資料列都是可編輯的。 在資料存取層中，我們會將多個更新作業包裝在交易中，以確保所有更新都會成功，或所有更新都會復原。

## <a name="introduction"></a>簡介

在[先前的教學](wrapping-database-modifications-within-a-transaction-vb.md)課程中，我們已瞭解如何擴充資料存取層，以加入資料庫交易的支援。 資料庫交易保證會將一系列的資料修改語句視為一個不可部分完成的作業，這可確保所有修改都會失敗，否則全部都會成功。 使用此低層級 DAL 功能時，我們已準備好將注意力轉換成建立批次資料修改介面。

在本教學課程中，我們將建立一個 GridView，其中每個資料列都可編輯（請參閱 [圖 1]） 因為每個資料列都是在其編輯介面中轉譯，所以不需要編輯、更新和取消按鈕的資料行。 相反地，頁面上有兩個 [更新產品] 按鈕，當您按一下時，會列舉 GridView 資料列並更新資料庫。

[GridView 中的每個資料列 ![都是可編輯的](batch-updating-vb/_static/image1.gif)](batch-updating-vb/_static/image1.png)

**圖 1**： GridView 中的每個資料列都是可編輯的（[按一下以查看完整大小的影像](batch-updating-vb/_static/image2.png)）

讓我們開始吧！

> [!NOTE]
> 在[執行批次更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md)教學課程中，我們使用 DataList 控制項來建立批次編輯介面。 本教學課程與中的上一個版本不同，後者是使用 GridView，而批次更新則是在交易的範圍內執行。 完成本教學課程之後，建議您回到先前的教學課程，並將其更新為使用上一個教學課程中新增的資料庫交易相關功能。

## <a name="examining-the-steps-for-making-all-gridview-rows-editable"></a>檢查將所有 GridView 資料列設為可編輯的步驟

如如何[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-vb.md)教學課程中所述，GridView 提供了內建支援，可讓您以每一資料列為基礎來編輯其基礎資料。 就內部而言，GridView 會透過其[`EditIndex` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.editindex(VS.80).aspx)來說明哪些資料列可供編輯。 當 GridView 系結到它的資料來源時，它會檢查每個資料列，以查看資料列的索引是否等於 `EditIndex`的值。 若是如此，則會使用其編輯介面來呈現資料列的欄位。 針對 BoundFields，編輯介面是一個文字方塊，其 `Text` 屬性會被指派 BoundField s `DataField` 屬性所指定之資料欄位的值。 若為 TemplateFields，則會使用 `EditItemTemplate` 來取代 `ItemTemplate`。

回想一下，編輯工作流程會在使用者按一下資料列的 [編輯] 按鈕時開始。 這會導致回傳，將 GridView 的 `EditIndex` 屬性設定為已按下的資料列 s 索引，然後將資料重新系結至方格。 按一下 [資料列] 的 [取消] 按鈕時，在回傳時，`EditIndex` 會設定為 `-1` 的值，然後再將資料重新系結至方格。 由於 GridView 的資料列會以零開始編制索引，將 `EditIndex` 設定為 `-1` 會影響以唯讀模式顯示 GridView。

`EditIndex` 屬性適用于每個資料列編輯，但不是針對批次編輯所設計。 為了讓整個 GridView 可供編輯，我們必須使用其編輯介面來呈現每個資料列。 完成這項工作的最簡單方式是建立，其中每個可編輯的欄位會實作為 TemplateField，並在 `ItemTemplate`中定義其編輯介面。

在接下來的幾個步驟中，我們將建立可完全編輯的 GridView。 在步驟1中，我們將從建立 GridView 和其 ObjectDataSource 開始，並將其 BoundFields 和 CheckBoxField 轉換成 TemplateFields。 在步驟2和3中，我們會將編輯介面從 TemplateFields `EditItemTemplate` s 移至其 `ItemTemplate` s。

## <a name="step-1-displaying-product-information"></a>步驟1：顯示產品資訊

在我們擔心建立可編輯資料列的 GridView 之前，讓我們先簡單顯示產品資訊。 開啟 [`BatchData`] 資料夾中的 [`BatchUpdate.aspx`] 頁面，並將 GridView 從 [工具箱] 拖曳至設計工具。 將 GridView 的 `ID` 設定為 `ProductsGrid` 並從其智慧標籤，選擇將其系結至名為 `ProductsDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以從 `ProductsBLL` 類別的 `GetProducts` 方法中取出其資料。

[![將 ObjectDataSource 設定為使用 ProductsBLL 類別](batch-updating-vb/_static/image2.gif)](batch-updating-vb/_static/image3.png)

**圖 2**：設定 ObjectDataSource 使用 `ProductsBLL` 類別（[按一下以查看完整大小的影像](batch-updating-vb/_static/image4.png)）

[![使用 GetProducts 方法取出產品資料](batch-updating-vb/_static/image3.gif)](batch-updating-vb/_static/image5.png)

**圖 3**：使用 `GetProducts` 方法取出產品資料（[按一下以觀看完整大小的影像](batch-updating-vb/_static/image6.png)）

就像 GridView 一樣，ObjectDataSource 的修改功能是設計為以每個資料列為基礎來處理。 若要更新一組記錄，我們必須在 ASP.NET 網頁的程式碼後置類別中撰寫一些程式碼，以批次處理資料並將其傳遞給 BLL。 因此，請將 [ObjectDataSource s 更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。 按一下 [完成] 完成精靈。

[![將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](batch-updating-vb/_static/image4.gif)](batch-updating-vb/_static/image7.png)

**圖 4**：將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](batch-updating-vb/_static/image8.png)）

完成 [設定資料來源] wizard 之後，ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](batch-updating-vb/samples/sample1.aspx)]

完成 [設定資料來源] wizard 也會導致 Visual Studio 為 GridView 中的產品資料欄位建立 BoundFields 和 CheckBoxField。 在本教學課程中，我們只允許使用者查看和編輯產品的名稱、類別、價格和已停止的狀態。 移除所有 [`ProductName`]、[`CategoryName`]、[`UnitPrice`] 和 [`Discontinued`] 欄位，然後將前三個欄位的 `HeaderText` 屬性分別重新命名為 [產品]、[類別] 和 [價格]。 最後，檢查 GridView s 智慧標籤中的 [啟用分頁] 和 [啟用排序] 核取方塊。

此時，GridView 有三個 BoundFields （`ProductName`、`CategoryName`和 `UnitPrice`）和一個 CheckBoxField （`Discontinued`）。 我們需要將這四個欄位轉換成 TemplateFields，然後將編輯介面從 TemplateField s `EditItemTemplate` 移到其 `ItemTemplate`。

> [!NOTE]
> 我們在[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教學課程中探索到建立和自訂 TemplateFields。 我們會逐步解說將 BoundFields 和 CheckBoxField 轉換為 TemplateFields 的步驟，並在其 `ItemTemplate` 中定義其編輯介面，但如果您停滯或需要重新整理器，請不要回頭參考這個稍早的教學課程。

從 GridView 的智慧標籤中，按一下 [編輯資料行] 連結以開啟 [欄位] 對話方塊。 接下來，選取每個欄位，然後按一下 [將此欄位轉換成 TemplateField] 連結。

![將現有的 BoundFields 和 CheckBoxField 轉換為 TemplateFields](batch-updating-vb/_static/image5.gif)

**圖 5**：將現有的 BoundFields 和 CheckBoxField 轉換成 TemplateFields

由於每個欄位都是 TemplateField，因此我們已準備好將編輯介面從 `EditItemTemplate` 移至 `ItemTemplate` s。

## <a name="step-2-creating-theproductnameunitprice-anddiscontinuedediting-interfaces"></a>步驟2：建立`ProductName`、`UnitPrice`和`Discontinued`編輯介面

建立 `ProductName`、`UnitPrice`和 `Discontinued` 編輯介面是此步驟的主題，而且相當簡單，因為每個介面已在 TemplateField s `EditItemTemplate`中定義。 建立 `CategoryName` 的編輯介面比較複雜一點，因為我們需要建立適用類別的 DropDownList。 此 `CategoryName` 編輯介面是在步驟3中破解。

讓我們從 `ProductName` TemplateField 開始。 按一下 GridView 的智慧標籤中的 [編輯範本] 連結，並向下切入至 `ProductName` TemplateField s `EditItemTemplate`。 選取文字方塊，將它複製到剪貼簿，然後貼到 `ProductName` TemplateField s `ItemTemplate`。 將 [TextBox `ID`] 屬性變更為 [`ProductName`]。

接下來，將 RequiredFieldValidator 新增至 `ItemTemplate`，以確保使用者提供每個產品名稱的值。 將 [`ControlToValidate`] 屬性設定為 [ProductName]，您必須提供產品名稱的 [`ErrorMessage`] 屬性。 以及要 \*的 `Text` 屬性。 在 `ItemTemplate`新增這些專案之後，您的畫面看起來應該像 [圖 6]。

[![ProductName TemplateField 現在包含 TextBox 和 RequiredFieldValidator](batch-updating-vb/_static/image6.gif)](batch-updating-vb/_static/image9.png)

**圖 6**： `ProductName` TemplateField 現在包含一個 TextBox 和一個 RequiredFieldValidator （[按一下以觀看完整大小的影像](batch-updating-vb/_static/image10.png)）

針對 `UnitPrice` 編輯介面，從 `EditItemTemplate` 將 TextBox 複製到 `ItemTemplate`開始。 接下來，將 $ 放在文字方塊前面，並將其 [`ID`] 屬性設為 [單價]，並將其 [`Columns`] 屬性設定為8。

此外，也請將 CompareValidator 新增至 `UnitPrice` s `ItemTemplate`，以確保使用者輸入的值是大於或等於 $0.00 的有效貨幣值。 將驗證程式的 `ControlToValidate` 屬性設定為 [單價]，其 `ErrorMessage` 屬性必須輸入有效的貨幣值。 請省略任何貨幣符號。、其 `Text` 屬性來 \*、其 `Type` `Currency`屬性設為 [`Operator`]，而其 [`GreaterThanEqual`] 屬性設為0。`ValueToCompare`

[![新增 CompareValidator，以確保輸入的價格是非負值的貨幣值](batch-updating-vb/_static/image7.gif)](batch-updating-vb/_static/image11.png)

**圖 7**：新增 CompareValidator 以確保輸入的價格是非負值的貨幣值（[按一下以查看完整大小的影像](batch-updating-vb/_static/image12.png)）

針對 `Discontinued` TemplateField，您可以使用已在 `ItemTemplate`中定義的核取方塊。 只要將其 `ID` 設定為 已停止，並將其 `Enabled` 屬性設為 `True`。

## <a name="step-3-creating-thecategorynameediting-interface"></a>步驟3：建立`CategoryName`編輯介面

[`CategoryName` TemplateField] `EditItemTemplate` 中的編輯介面包含一個文字方塊，其中顯示 `CategoryName` 資料欄位的值。 我們需要以列出可能分類的 DropDownList 來取代此程式。

> [!NOTE]
> [自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教學課程包含更全面且完整的討論，可將範本自訂成包含 DropDownList，而不是文字方塊。 雖然這裡的步驟已完成，但會呈現 tersely。 若要深入瞭解如何建立和設定類別 DropDownList，請回頭參閱[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教學課程。

從 [工具箱] 將 [DropDownList] 拖曳至 [`CategoryName`] TemplateField s `ItemTemplate`，將其 `ID` 設定為 [`Categories`]。 此時，我們通常會透過其智慧標籤定義 Dropdownlist 進行的資料來源，並建立新的 ObjectDataSource。 不過，這會在 `ItemTemplate`內加入 ObjectDataSource，這會導致每個 GridView 資料列建立一個 ObjectDataSource 實例。 相反地，讓我們在 GridView 的 TemplateFields 外部建立 ObjectDataSource。 結束範本編輯，並從 [工具箱] 將 [ObjectDataSource] 拖曳至 [`ProductsDataSource` ObjectDataSource] 底下的設計工具。 將新的 ObjectDataSource 命名為 `CategoriesDataSource`，並將它設定為使用 `CategoriesBLL` 類別 s `GetCategories` 方法。

[![將 ObjectDataSource 設定為使用 CategoriesBLL 類別](batch-updating-vb/_static/image8.gif)](batch-updating-vb/_static/image13.png)

**圖 8**：設定 ObjectDataSource 使用 `CategoriesBLL` 類別（[按一下以查看完整大小的影像](batch-updating-vb/_static/image14.png)）

[![使用 GetCategories 方法取出類別目錄資料](batch-updating-vb/_static/image9.gif)](batch-updating-vb/_static/image15.png)

**圖 9**：使用 `GetCategories` 方法抓取分類資料（[按一下以查看完整大小的影像](batch-updating-vb/_static/image16.png)）

由於只會使用此 ObjectDataSource 來抓取資料，因此請將 [更新] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。 按一下 [完成] 完成精靈。

[![將 [更新] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](batch-updating-vb/_static/image10.gif)](batch-updating-vb/_static/image17.png)

**圖 10**：將 [更新] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](batch-updating-vb/_static/image18.png)）

完成 wizard 之後，`CategoriesDataSource` 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](batch-updating-vb/samples/sample2.aspx)]

建立並設定 `CategoriesDataSource` 之後，請回到 `CategoryName` TemplateField s `ItemTemplate`，然後從 DropDownList s 智慧標籤，按一下 [選擇資料來源] 連結。 在 [資料來源設定] 嚮導中，從第一個下拉式清單中選取 [`CategoriesDataSource`] 選項，然後選擇讓 [`CategoryName`] 用來顯示和 `CategoryID` 作為值。

[![將 DropDownList 系結至 CategoriesDataSource](batch-updating-vb/_static/image11.gif)](batch-updating-vb/_static/image19.png)

**圖 11**：將 DropDownList 系結至 `CategoriesDataSource` （[按一下以查看完整大小的影像](batch-updating-vb/_static/image20.png)）

此時，`Categories` DropDownList 會列出所有類別，但它還不會針對系結至 GridView 資料列的產品自動選取適當的類別。 若要完成這件工作，我們必須將 `Categories` DropDownList s `SelectedValue` 設定為 product s `CategoryID` 值。 按一下 DropDownList s 智慧標籤中的 [編輯資料系結] 連結，並將 [`SelectedValue`] 屬性與 [`CategoryID` 資料] 欄位建立關聯，如 [圖 12] 所示。

![將產品的 [類別 1] 值系結至 DropDownList s SelectedValue 屬性](batch-updating-vb/_static/image12.gif)

**圖 12**：將產品的 `CategoryID` 值系結至 DropDownList s `SelectedValue` 屬性

最後一個問題仍然存在：如果產品沒有指定 `CategoryID` 值，則 `SelectedValue` 上的資料系結語句會導致例外狀況。 這是因為 DropDownList 只會包含類別目錄的專案，而且不會提供具有 `CategoryID`之 `NULL` 資料庫值之產品的選項。 若要解決這個問題，請將 DropDownList 的 `AppendDataBoundItems` 屬性設定為 `True`，並將新的專案加入至 DropDownList，並從宣告式語法中省略 `Value` 屬性。 也就是說，請確定 `Categories` DropDownList 的宣告式語法看起來如下：

[!code-aspx[Main](batch-updating-vb/samples/sample3.aspx)]

請注意 `<asp:ListItem Value="">`--選取一個--將其 `Value` 屬性明確設定為空字串。 請回到[自訂資料修改介面](../editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb.md)教學課程，以深入瞭解為何需要這個額外的 DropDownList 專案來處理 `NULL` 案例，以及為什麼將 `Value` 屬性指派給空字串是不可或缺的。

> [!NOTE]
> 這裡有潛在的效能和擴充性問題，值得一提。 由於每個資料列都有一個使用 `CategoriesDataSource` 做為其資料來源的 DropDownList，因此每個頁面的 `CategoriesBLL` 類別 s `GetCategories` 方法將會被呼叫*n*次，其中*n*是 GridView 中的資料列數目。 這些*n*呼叫 `GetCategories` 會導致資料庫的*n*個查詢。 藉由在每個要求快取中快取傳回的分類，或透過使用 SQL 快取相依性的快取層或非常短的以時間為基礎的到期，可以降低對資料庫的影響。 如需有關每個要求快取選項的詳細資訊，請參閱[`HttpContext.Items` 每個要求的快取存放區](http://aspnet.4guysfromrolla.com/articles/060904-1.aspx)。

## <a name="step-4-completing-the-editing-interface"></a>步驟4：完成編輯介面

我們對 GridView 的範本進行了一些變更，而不需要暫停來觀看我們的進度。 請花點時間透過瀏覽器來查看進度。 如 [圖 13] 所示，每個資料列都是使用其 `ItemTemplate`來呈現，其中包含儲存格的編輯介面。

[![每個 GridView 資料列都是可編輯的](batch-updating-vb/_static/image13.gif)](batch-updating-vb/_static/image21.png)

**圖 13**：每個 GridView 資料列都是可編輯的（[按一下以查看完整大小的影像](batch-updating-vb/_static/image22.png)）

這裡有幾個次要的格式問題，我們應該要注意。 首先，請注意，`UnitPrice` 值包含四個小數點。 若要修正此問題，請回到 `UnitPrice` TemplateField s `ItemTemplate`，然後從 TextBox 的智慧標籤，按一下 [編輯系結] 連結。 接下來，指定 `Text` 屬性應格式化為數位。

![將文字屬性格式化為數位](batch-updating-vb/_static/image14.gif)

**圖 14**：將 `Text` 屬性格式化為數位

第二，讓我們將 [`Discontinued`] 欄中的核取方塊置中（而不是靠左對齊）。 在 [GridView] 智慧標籤中按一下 [編輯資料行]，然後從左下角的欄位清單中選取 [`Discontinued` TemplateField]。 向下切入 `ItemStyle`，並將 `HorizontalAlign` 屬性設定為 [中心]，如 [圖 15] 所示。

![停用 [已停止] 核取方塊](batch-updating-vb/_static/image15.gif)

**圖 15**：將 `Discontinued` 核取方塊置中

接下來，將 ValidationSummary 控制項新增至頁面，並將其 `ShowMessageBox` 屬性設為 `True`，並將其 `ShowSummary` 屬性設定為 `False`。 此外，新增按鈕 Web 控制項，按一下之後，將會更新使用者的變更。 具體來說，請新增兩個按鈕 Web 控制項，一個在 GridView 上方，另一個放在其底下，將兩個控制項設定 `Text` 屬性來更新產品。

由於 GridView s 編輯介面是在其 TemplateFields `ItemTemplate` s 中定義，因此 `EditItemTemplate` 是多餘的，而且可能會被刪除。

在上述的格式變更、加入按鈕控制項，以及移除不必要的 `EditItemTemplate` 之後，您的頁面的宣告式語法應如下所示：

[!code-aspx[Main](batch-updating-vb/samples/sample4.aspx)]

[圖 16] 顯示在新增按鈕 Web 控制項及進行格式變更之後，透過瀏覽器觀看此頁面。

[![頁面現在包含兩個 [更新產品] 按鈕](batch-updating-vb/_static/image16.gif)](batch-updating-vb/_static/image23.png)

**圖 16**：此頁面現在包含兩個 [更新產品] 按鈕（[按一下以觀看完整大小的影像](batch-updating-vb/_static/image24.png)）

## <a name="step-5-updating-the-products"></a>步驟5：更新產品

當使用者造訪此頁面時，他們會進行修改，然後按一下兩個 [更新產品] 按鈕的其中一個。 此時，我們必須以某種方式將每個資料列的使用者輸入值儲存到 `ProductsDataTable` 實例中，然後將其傳遞給 BLL 方法，然後將該 `ProductsDataTable` 實例傳遞給 DAL s `UpdateWithTransaction` 方法。 在[先前的教學](wrapping-database-modifications-within-a-transaction-vb.md)課程中建立的 `UpdateWithTransaction` 方法，可確保變更批次會更新為不可部分完成的作業。

在 `BatchUpdate.aspx.vb` 中建立名為 `BatchUpdate` 的方法，並新增下列程式碼：

[!code-vb[Main](batch-updating-vb/samples/sample5.vb)]

這個方法一開始會透過呼叫 BLL 的 `GetProducts` 方法來取得 `ProductsDataTable` 中的所有產品。 然後，它會列舉 `ProductGrid` GridView s [`Rows` 集合](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rows(VS.80).aspx)。 `Rows` 集合包含 GridView 中顯示之每個資料列的[`GridViewRow` 實例](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridviewrow.aspx)。 因為我們在每個頁面上最多顯示10個數據列，所以 GridView 的 `Rows` 集合不會有10個以上的專案。

針對每個資料列，會從 `DataKeys` 集合中抓取 `ProductID`，並從 `ProductsDataTable`選取適當的 `ProductsRow`。 四個 TemplateField 輸入控制項會以程式設計方式參考，並將其值指派給 `ProductsRow` 實例的屬性。 在每個 GridView 資料列的值都已經用來更新 `ProductsDataTable`之後，它就會傳遞給 BLL 的 `UpdateWithTransaction` 方法，如同我們在先前的教學課程中所見，只要向下呼叫 DAL s `UpdateWithTransaction` 方法即可。

本教學課程所使用的批次更新演算法會更新對應至 GridView 中某個資料列之 `ProductsDataTable` 中的每個資料列，而不論產品的資訊是否已變更。 雖然這類盲人更新通常不會造成效能問題，但如果您重新審核資料庫資料表的變更，它們可能會導致多餘的記錄。 回到執行中的[批次更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md)教學課程，我們探索了批次更新介面與 DataList，並新增了只會更新使用者實際修改之記錄的程式碼。 如有需要，您可以隨意使用[執行批次更新](../editing-and-deleting-data-through-the-datalist/performing-batch-updates-vb.md)的技術來更新本教學課程中的程式碼。

> [!NOTE]
> 透過智慧標籤將資料來源系結至 GridView 時，Visual Studio 會自動將資料來源的主要索引鍵值指派給 GridView 的 `DataKeyNames` 屬性。 如果您未透過 GridView 的智慧標籤將 ObjectDataSource 系結至 GridView （如步驟1所述），則您必須手動將 GridView 的 `DataKeyNames` 屬性設定為 ProductID，才能透過 `DataKeys` 集合來存取每個資料列的 `ProductID` 值。

`BatchUpdate` 中使用的程式碼與 BLL `UpdateProduct` 方法中所使用的程式碼相似，主要差異在於，在 `UpdateProduct` 方法中，只有單一 `ProductRow` 實例會從架構中抓取。 指派 `ProductRow` 屬性的程式碼，在 `BatchUpdate`的 `For Each` 迴圈中的 `UpdateProducts` 方法和程式碼之間是一樣的，如同整體模式一樣。

若要完成本教學課程，當您按一下 [更新產品] 按鈕時，我們必須叫用 `BatchUpdate` 方法。 為這兩個按鈕控制項的 `Click` 事件建立事件處理常式，並在事件處理常式中新增下列程式碼：

[!code-vb[Main](batch-updating-vb/samples/sample6.vb)]

首先，對 `BatchUpdate`進行呼叫。 接下來， [`ClientScript` 屬性](https://msdn.microsoft.com/library/system.web.ui.page.clientscript(VS.80).aspx)會用來插入 JavaScript，以顯示會讀取已更新產品的 messagebox。

請花幾分鐘的時間來測試此程式碼。 透過瀏覽器造訪 `BatchUpdate.aspx`，編輯一些資料列，然後按一下其中一個 [更新產品] 按鈕。 假設沒有輸入驗證錯誤，您應該會看到一個讀取已更新產品的 messagebox。 若要驗證更新的不可部分完成性，請考慮新增隨機的 `CHECK` 條件約束，例如不允許1234.56 值 `UnitPrice` 的限制。 然後從 `BatchUpdate.aspx`編輯一些記錄，並確定將其中一個產品的 `UnitPrice` 值設定為禁止的值（1234.56）。 當您按一下 [更新產品] 時，如果將批次作業中的其他變更回復成其原始值，這應該會產生錯誤。

## <a name="an-alternativebatchupdatemethod"></a>替代的`BatchUpdate`方法

我們剛才檢查的 `BatchUpdate` 方法會從 BLL 的 `GetProducts` 方法中抓取*所有*產品，然後只更新出現在 GridView 中的記錄。 如果 GridView 不使用分頁，這種方法就很理想，但如果有的話，可能會有數百、數千或數萬項產品，但 GridView 中只有10個數據列。 在這種情況下，從資料庫取得所有產品只是為了修改其中的10個，並不是理想的選擇。

針對這些類型的情況，請考慮改為使用下列 `BatchUpdateAlternate` 方法：

[!code-vb[Main](batch-updating-vb/samples/sample7.vb)]

`BatchMethodAlternate` 從建立名為 `products`的新空 `ProductsDataTable` 開始。 然後逐步執行 GridView 的 `Rows` 集合，並針對每個資料列使用 BLL 的 `GetProductByProductID(productID)` 方法來取得特定的產品資訊。 抓取的 `ProductsRow` 實例會以 `BatchUpdate`的相同方式更新其屬性，但在更新資料列之後，它會透過 DataTable [`ImportRow(DataRow)` 方法](https://msdn.microsoft.com/library/system.data.datatable.importrow(VS.80).aspx)匯入至 `products` `ProductsDataTable`。

在 `For Each` 迴圈完成之後，`products` 會針對 GridView 中的每個資料列包含一個 `ProductsRow` 實例。 由於每個 `ProductsRow` 實例都已加入至 `products` （而不是更新），因此，如果我們盲目地將它傳遞給 `UpdateWithTransaction` 方法，`ProductsTableAdapter` 會嘗試將每個記錄插入資料庫中。 相反地，我們需要指定每個資料列都已修改（未加入）。

這可以藉由將新的方法加入至名為 `UpdateProductsWithTransaction`的 BLL 來完成。 `UpdateProductsWithTransaction`（如下所示）會將 `ProductsDataTable` 中每個 `ProductsRow` 實例的 `RowState` 設定為 `Modified`，然後將 `ProductsDataTable` 傳遞給 DAL s `UpdateWithTransaction` 方法。

[!code-vb[Main](batch-updating-vb/samples/sample8.vb)]

## <a name="summary"></a>總結

GridView 提供內建的每個資料列編輯功能，但缺少建立完全可編輯介面的支援。 如我們在本教學課程中所見，這類介面是可行的，但需要一些工作。 若要建立 GridView，其中每個資料列都是可編輯的，我們需要將 GridView 的欄位轉換成 TemplateFields，並在 `ItemTemplate` 內定義編輯介面。 此外，您必須將 [更新全部類型] 按鈕 Web 控制項加入至該頁面，並與 GridView 分開。 這些按鈕 `Click` 事件處理常式需要列舉 GridView 的 `Rows` 集合、將變更儲存在 `ProductsDataTable`中，然後將更新的資訊傳遞至適當的 BLL 方法。

在下一個教學課程中，我們將瞭解如何建立用於批次刪除的介面。 特別是，每個 GridView 資料列都會包含一個核取方塊，而不是更新全部類型的按鈕，我們將會刪除選取的資料列按鈕。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Teresa Murphy 和 David Suru。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](wrapping-database-modifications-within-a-transaction-vb.md)
> [下一頁](batch-deleting-vb.md)
