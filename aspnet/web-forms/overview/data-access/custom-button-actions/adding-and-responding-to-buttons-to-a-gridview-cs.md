---
uid: web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
title: 新增和回應 GridView 的按鈕（C#） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何將自訂按鈕新增至範本以及 GridView 或 DetailsView 控制項的欄位。 特別是，我們將建置 。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 128fdb5f-4c5e-42b5-b485-f3aee90a8e38
msc.legacyurl: /web-forms/overview/data-access/custom-button-actions/adding-and-responding-to-buttons-to-a-gridview-cs
msc.type: authoredcontent
ms.openlocfilehash: 5c87386e4fe2c53b39162071689f2522dcc6c7ac
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78549641"
---
# <a name="adding-and-responding-to-buttons-to-a-gridview-c"></a>新增與回應 GridView 的按鈕 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_28_CS.exe)或[下載 PDF](adding-and-responding-to-buttons-to-a-gridview-cs/_static/datatutorial28cs1.pdf)

> 在本教學課程中，我們將探討如何將自訂按鈕新增至範本以及 GridView 或 DetailsView 控制項的欄位。 特別是，我們將建立一個具有 FormView 的介面，讓使用者可以逐頁流覽供應商。

## <a name="introduction"></a>簡介

雖然許多報表案例都包含報表資料的唯讀存取權，但報表並不是很罕見的，因為它會根據所顯示的資料來包含執行動作的能力。 通常這牽涉到在報表中顯示的每筆記錄加上一個按鈕、LinkButton 或 ImageButton Web 控制項，按一下時，會導致回傳並叫用一些伺服器端程式碼。 逐記錄編輯和刪除資料是最常見的範例。 事實上，如同從[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教學課程的總覽開始介紹，編輯和刪除是很常見的，GridView、DetailsView 和 FormView 控制項都可以支援這類功能，而不需要撰寫任何一行程式碼。

除了 [編輯] 和 [刪除] 按鈕之外，GridView、DetailsView 和 FormView 控制項也可以包含按鈕、LinkButtons 或 ImageButtons，當按下時，就會執行一些自訂的伺服器端邏輯。 在本教學課程中，我們將探討如何將自訂按鈕新增至範本以及 GridView 或 DetailsView 控制項的欄位。 特別是，我們將建立一個具有 FormView 的介面，讓使用者可以逐頁流覽供應商。 針對指定的供應商，FormView 會顯示供應商的相關資訊，以及一個按鈕 Web 控制項，如果按一下，就會將其所有相關聯的產品標示為已中止。 此外，GridView 會列出所選供應商所提供的產品，其中每個資料列都包含 [增加價格和折扣價] 按鈕，如果按下，則會提高或降低產品的 `UnitPrice` 10% （請參閱 [圖 1]）。

[![FormView 和 GridView 包含執行自訂動作的按鈕](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image2.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image1.png)

**圖 1**： FormView 和 GridView 都包含執行自訂動作的按鈕（[按一下以觀看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image3.png)）

## <a name="step-1-adding-the-button-tutorial-web-pages"></a>步驟1：新增按鈕教學課程網頁

在查看如何新增自訂按鈕之前，讓我們先花點時間在我們的網站專案中建立 ASP.NET 網頁，我們將在本教學課程中使用。 從新增名為 `CustomButtons`的資料夾開始。 接下來，將下列兩個 ASP.NET 網頁新增至該資料夾，並確定每個頁面都與 `Site.master` 主版頁面相關聯：

- `Default.aspx`
- `CustomButtons.aspx`

![新增自訂按鈕相關教學課程的 ASP.NET 網頁](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image4.png)

**圖 2**：新增自訂按鈕相關教學課程的 ASP.NET 網頁

如同在其他資料夾中，[`CustomButtons`] 資料夾中的 `Default.aspx` 會在其區段中列出教學課程。 回想一下，`SectionLevelTutorialListing.ascx` 的使用者控制項會提供這種功能。 因此，請將此使用者控制項從方案總管拖曳至頁面的設計檢視，以將其新增至 `Default.aspx`。

[![將 SectionLevelTutorialListing 的 .ascx 使用者控制項新增至 default.aspx](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image6.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image5.png)

**圖 3**：將 `SectionLevelTutorialListing.ascx` 使用者控制項加入 `Default.aspx` （[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image7.png)）

最後，將頁面新增為 `Web.sitemap` 檔案的專案。 具體而言，在分頁和排序 `<siteMapNode>`之後加入下列標記：

[!code-xml[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample1.xml)]

更新 `Web.sitemap`之後，請花一點時間透過瀏覽器來觀看教學課程網站。 左側功能表現在包含用於編輯、插入及刪除教學課程的專案。

![網站地圖現在包含自訂按鈕教學課程的專案](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image8.png)

[**圖 4**]：網站地圖現在包含自訂按鈕教學課程的專案

## <a name="step-2-adding-a-formview-that-lists-the-suppliers"></a>步驟2：加入可列出供應商的 FormView

讓我們藉由新增可列出供應商的 FormView 來開始使用本教學課程。 如簡介中所述，此 FormView 可讓使用者逐頁流覽供應商，並在 GridView 中顯示供應商所提供的產品。 此外，此 FormView 會包含一個按鈕，當您按一下時，會將供應商的所有產品標示為已中止。 在我們考慮如何將自訂按鈕加入至 FormView 之前，讓我們先建立 FormView，使其顯示供應商資訊。

從開啟 [`CustomButtons`] 資料夾中的 [`CustomButtons.aspx`] 頁面開始。 將 FormView 從 [工具箱] 拖曳至設計工具，並將其 [`ID`] 屬性設為 [`Suppliers`]，將它加入頁面中。 從 FormView 的智慧標籤中，選擇建立名為 `SuppliersDataSource`的新 ObjectDataSource。

[![建立名為 SuppliersDataSource 的新 ObjectDataSource](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image10.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image9.png)

**圖 5**：建立名為 `SuppliersDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image11.png)）

設定這個新的 ObjectDataSource，讓它從 `SuppliersBLL` 類別的 `GetSuppliers()` 方法進行查詢（請參閱 [圖 6]）。 由於此 FormView 並未提供更新供應商資訊的介面，因此請從 [更新] 索引標籤的下拉式清單中選取 [（無）] 選項。

[![將資料來源設定為使用 SuppliersBLL 類別 s GetSuppliers （）方法](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image13.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image12.png)

**圖 6**：將資料來源設定為使用 `SuppliersBLL` 類別的 `GetSuppliers()` 方法（[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image14.png)）

設定 ObjectDataSource 之後，Visual Studio 將會產生 FormView 的 `InsertItemTemplate`、`EditItemTemplate`和 `ItemTemplate`。 移除 `InsertItemTemplate` 並 `EditItemTemplate` 並修改 `ItemTemplate`，使其只顯示供應商的公司名稱和電話號碼。 最後，藉由勾選智慧標籤的 [啟用分頁] 核取方塊（或將其 [`AllowPaging`] 屬性設定為 [`True`]）來開啟 FormView 的分頁支援。 這些變更之後，您頁面的宣告式標記看起來應該如下所示：

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample2.aspx)]

[圖 7] 顯示透過瀏覽器觀看時的 CustomButtons 頁面。

[![FormView 會列出目前所選供應商的 [公司名稱] 和 [電話] 欄位](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image16.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image15.png)

**圖 7**： FormView 會列出目前所選供應商的 `CompanyName` 和 `Phone` 欄位（[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image17.png)）

## <a name="step-3-adding-a-gridview-that-lists-the-selected-suppliers-products"></a>步驟3：加入一個 GridView，其中列出所選供應商的產品

在我們將 [停止所有產品] 按鈕新增至 FormView 的範本之前，讓我們先在 FormView 底下新增 GridView，其中會列出所選供應商所提供的產品。 若要完成此動作，請在頁面中新增 GridView、將其 `ID` 屬性設為 `SuppliersProducts`，然後新增名為 `SuppliersProductsDataSource`的新 ObjectDataSource。

[![建立名為 SuppliersProductsDataSource 的新 ObjectDataSource](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image19.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image18.png)

**圖 8**：建立名為 `SuppliersProductsDataSource` 的新 ObjectDataSource （[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image20.png)）

將此 ObjectDataSource 設定為使用 ProductsBLL 類別的 `GetProductsBySupplierID(supplierID)` 方法（請參閱 [圖 9]）。 雖然此 GridView 會允許產品的價格調整，但它不會使用 GridView 的內建編輯或刪除功能。 因此，我們可以針對 ObjectDataSource 的 [更新]、[插入] 和 [刪除] 索引標籤，將下拉式清單設定為 [（無）]。

[![將資料來源設定為使用 ProductsBLL 類別 s GetProductsBySupplierID （已加入供應商）方法](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image22.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image21.png)

**圖 9**：將資料來源設定為使用 `ProductsBLL` 類別的 `GetProductsBySupplierID(supplierID)` 方法（[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image23.png)）

由於 `GetProductsBySupplierID(supplierID)` 方法會接受輸入參數，因此 ObjectDataSource wizard 會提示我們提供此參數值的來源。 若要傳入 FormView 的 `SupplierID` 值，請將 參數來源 下拉式清單設定為 控制，並將 ControlID 下拉式清單設為 `Suppliers` （在步驟2中建立之 FormView 的識別碼）。

[![指出 [供應商] 參數應來自 [供應商 FormView] 控制項](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image25.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image24.png)

**圖 10**：指出 *`supplierID`* 參數應該來自 `Suppliers` 的 FormView 控制項（[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image26.png)）

完成 ObjectDataSource wizard 之後，GridView 會針對每個產品的資料欄位包含 BoundField 或 CheckBoxField。 讓我們修剪一下，只顯示 `ProductName` 和 `UnitPrice` BoundFields，以及 `Discontinued` 的 CheckBoxField;此外，讓我們將 `UnitPrice` BoundField 格式化，使其文字格式化為貨幣。 您的 GridView 和 `SuppliersProductsDataSource` ObjectDataSource 的宣告式標記看起來應該類似下列標記：

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample3.aspx)]

此時，我們的教學課程會顯示主版/詳細資料包告，讓使用者可以從最上方的 FormView 挑選供應商，並透過底部的 GridView 查看該供應商提供的產品。 [圖 11] 顯示從 FormView 選取東京貿易供應商時，此頁面的螢幕擷取畫面。

[![選取的供應商產品會顯示在 GridView 中](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image28.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image27.png)

**圖 11**：選取的供應商產品會顯示在 GridView 中（[按一下以觀看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image29.png)）

## <a name="step-4-creating-dal-and-bll-methods-to-discontinue-all-products-for-a-supplier"></a>步驟4：建立 DAL 和 BLL 方法，以停止供應商的所有產品

在我們可以將按鈕加入至 FormView 之後，當您按一下時，會停止所有供應商的產品，我們必須先將方法新增至執行此動作的 DAL 和 BLL。 特別的是，這個方法會命名為 `DiscontinueAllProductsForSupplier(supplierID)`。 按一下 FormView 的按鈕時，我們會在商務邏輯層叫用此方法，並傳入所選供應商的 `SupplierID`;然後，BLL 會向下呼叫對應的資料存取層方法，這將會發出 `UPDATE` 語句給資料庫，使其無法中止指定的供應商產品。

如同我們在先前的教學課程中所做的，我們將使用最新的方法，一開始先建立 DAL 方法，然後是 BLL 方法，最後在 [ASP.NET] 頁面中執行功能。 在 [`App_Code/DAL`] 資料夾中開啟 `Northwind.xsd` 類型資料集，並將新的方法加入 `ProductsTableAdapter` （以滑鼠右鍵按一下 `ProductsTableAdapter`，然後選擇 [加入查詢]）。 這麼做會顯示 [TableAdapter 查詢設定] wizard，讓我們逐步完成新增方法的程式。 一開始請先指出我們的 DAL 方法將使用臨機操作 SQL 語句。

[![使用特定 SQL 語句建立 DAL 方法](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image31.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image30.png)

**圖 12**：使用臨機操作 SQL 語句建立 DAL 方法（[按一下以觀看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image32.png)）

接下來，嚮導會提示我們輸入要建立的查詢類型。 由於 `DiscontinueAllProductsForSupplier(supplierID)` 方法將需要更新 `Products` 資料庫資料表，針對指定 *`supplierID`* 所提供的所有產品，將 `Discontinued` 欄位設定為1，因此我們必須建立可更新資料的查詢。

[![選擇更新查詢類型](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image34.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image33.png)

**圖 13**：選擇更新查詢類型（[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image35.png)）

下一個 wizard 畫面會提供 TableAdapter 的現有 `UPDATE` 語句，以更新 `Products` DataTable 中定義的每個欄位。 將此查詢文字取代為下列語句：

[!code-sql[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample4.sql)]

輸入此查詢並按 [下一步] 之後，最後一個 wizard 畫面會要求使用 `DiscontinueAllProductsForSupplier`的新方法名稱。 按一下 [完成] 按鈕以完成嚮導。 返回 DataSet 設計工具時，您應該會在名為 `DiscontinueAllProductsForSupplier(@SupplierID)`的 `ProductsTableAdapter` 中看到新的方法。

[![命名新的 DAL 方法 DiscontinueAllProductsForSupplier](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image37.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image36.png)

**圖 14**：將新的 DAL 方法命名 `DiscontinueAllProductsForSupplier` （[按一下以查看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image38.png)）

在資料存取層中建立 `DiscontinueAllProductsForSupplier(supplierID)` 方法之後，下一項工作是在商務邏輯層中建立 `DiscontinueAllProductsForSupplier(supplierID)` 方法。 若要完成此動作，請開啟 `ProductsBLL` 類別檔案，並新增下列內容：

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample5.cs)]

這個方法只會向下呼叫 DAL 中的 `DiscontinueAllProductsForSupplier(supplierID)` 方法，並沿著提供的 *`supplierID`* 參數值傳遞。 如果有任何商務規則只允許供應商的產品在某些情況下停止，這些規則應該在此實作為 BLL。

> [!NOTE]
> 不同于 `ProductsBLL` 類別中的 `UpdateProduct` 多載，`DiscontinueAllProductsForSupplier(supplierID)` 方法簽章不包含 `DataObjectMethodAttribute` 屬性（`<System.ComponentModel.DataObjectMethodAttribute(System.ComponentModel.DataObjectMethodType.Update, Boolean)>`）。 這會在 [更新] 索引標籤中，從 ObjectDataSource 的 [設定資料來源] wizard 下拉式清單中排除 `DiscontinueAllProductsForSupplier(supplierID)` 方法。我省略了這個屬性，因為我們會直接從 ASP.NET 網頁中的事件處理常式呼叫 `DiscontinueAllProductsForSupplier(supplierID)` 方法。

## <a name="step-5-adding-a-discontinue-all-products-button-to-the-formview"></a>步驟5：將 [停止所有產品] 按鈕新增至 FormView

當 BLL 和 DAL 中的 `DiscontinueAllProductsForSupplier(supplierID)` 方法完成時，新增可中斷所選供應商所有產品之能力的最後一個步驟，就是將按鈕 Web 控制項新增至 FormView 的 `ItemTemplate`。 讓我們在供應商的電話號碼底下加上按鈕文字、[停止所有產品] 和 [`ID`] 屬性值為 [`DiscontinueAllProductsForSupplier`]。 您可以透過設計工具加入此按鈕 Web 控制項，方法是按一下 FormView 的智慧標籤中的 [編輯範本] 連結（請參閱 [圖 15]），或直接透過宣告式語法。

[![將 [停止所有產品] 按鈕 Web 控制項新增至 FormView s ItemTemplate](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image40.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image39.png)

**圖 15**：將 [停止所有產品] 按鈕 Web 控制項新增至 FormView 的 `ItemTemplate` （[按一下以觀看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image41.png)）

當流覽頁面的使用者按一下按鈕時，就會引發回傳接踵而來和 FormView 的[`ItemCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.itemcommand.aspx)。 若要執行自訂程式碼來回應按一下這個按鈕，我們可以建立這個事件的事件處理常式。 不過，請瞭解，每當在 FormView 內按一下*任何*按鈕、LinkButton 或 ImageButton Web 控制項時，就會引發 `ItemCommand` 事件。 這表示當使用者在 FormView 中從一頁移到另一個頁面時，就會引發 `ItemCommand` 事件;當使用者在支援插入、更新或刪除的 FormView 中按一下 [新增]、[編輯] 或 [刪除] 時，也是一樣。

由於 `ItemCommand` 不論按一下哪個按鈕而引發，因此，在事件處理常式中，我們需要一種方法來判斷是否已按下 [停止所有產品] 按鈕，或者是否為其他按鈕。 為了達成此目的，我們可以將按鈕 Web 控制項的 `CommandName` 屬性設定為一些識別值。 按一下按鈕時，這個 `CommandName` 值會傳遞至 `ItemCommand` 事件處理常式，讓我們判斷是否已按下 [停止所有產品] 按鈕。 將 [中止所有產品] 按鈕的 `CommandName` 屬性設定為 DiscontinueProducts。

最後，讓我們使用 [用戶端確認] 對話方塊，確保使用者真的想要停止所選供應商的產品。 如在刪除教學課程[時新增用戶端確認](../editing-inserting-and-deleting-data/adding-client-side-confirmation-when-deleting-cs.md)中所見，您可以使用一些 JavaScript 來完成這項作業。 特別的是，將按鈕 Web 控制項的 OnClientClick 屬性設定為 `return confirm('This will mark _all_ of this supplier\'s products as discontinued. Are you certain you want to do this?');`

進行這些變更之後，FormView 的宣告式語法看起來應該如下所示：

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample6.aspx)]

接下來，建立 FormView 的 `ItemCommand` 事件的事件處理常式。 在此事件處理常式中，我們必須先判斷是否已按下 [停止所有產品] 按鈕。 若是如此，我們想要建立 `ProductsBLL` 類別的實例，並叫用它的 `DiscontinueAllProductsForSupplier(supplierID)` 方法，並傳入所選 FormView 的 `SupplierID`：

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample7.cs)]

請注意，您可以使用 FormView 的[`SelectedValue` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.formview.selectedvalue.aspx)來存取 formview 中目前選取之供應商的 `SupplierID`。 `SelectedValue` 屬性會傳回要在 FormView 中顯示之記錄的第一個資料索引鍵值。 FormView 的[`DataKeyNames` 屬性](https://msdn.microsoft.com/system.web.ui.webcontrols.formview.datakeynames.aspx)（表示從中提取資料索引鍵值的資料欄位），會在將 ObjectDataSource 系結至步驟2中的 FormView 時，自動設定為 `SupplierID` Visual Studio。

建立 `ItemCommand` 事件處理常式之後，請花點時間測試頁面。 流覽至 Cooperativa de Quesos ' 內華達 Cabras ' 供應商（這是 FormView for me 中的第五個供應商）。 此供應商提供兩個產品： Queso Cabrales 和 Queso Manchego La Pastora，這兩者都*不*會中止。

假設 Cooperativa de Quesos ' 內華達 Cabras ' 已用盡企業，因此其產品即將淘汰。 按一下 [停止所有產品] 按鈕。 這會顯示 [用戶端確認] 對話方塊（請參閱 [圖 16]）。

[![Cooperativa de Quesos 內華達 Cabras 提供兩個有效的產品](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image43.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image42.png)

**圖 16**： Cooperativa De Quesos 內華達 Cabras 提供兩個使用[中的產品（按一下以觀看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image44.png)）

如果您在 [用戶端確認] 對話方塊中按一下 [確定]，就會繼續提交表單，而導致會引發 FormView 的 `ItemCommand` 事件的回傳。 然後，我們建立的事件處理常式會執行，叫用 `DiscontinueAllProductsForSupplier(supplierID)` 方法，並同時停 Queso Cabrales 和 Queso Manchego La Pastora 產品。

如果您已停用 GridView 的 view 狀態，GridView 會在每次回傳時重新系結至基礎資料存放區，因此會立即更新以反映這兩項產品現在已停止（請參閱 [圖 17]）。 不過，如果您在 GridView 中未停用 view 狀態，則在進行這項變更之後，您必須手動將資料重新系結至 GridView。 若要完成此動作，只需在叫用 `DiscontinueAllProductsForSupplier(supplierID)` 方法之後，立即呼叫 GridView 的 `DataBind()` 方法。

[![按一下 [中止所有產品] 按鈕之後，供應商的產品會據以更新](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image46.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image45.png)

**圖 17**：按一下 [停止所有產品] 按鈕之後，供應商的產品會隨之更新（[按一下以觀看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image47.png)）

## <a name="step-6-creating-an-updateproduct-overload-in-the-business-logic-layer-for-adjusting-a-products-price"></a>步驟6：在商務邏輯層中建立 UpdateProduct 多載以調整產品的價格

與 FormView 中的 [停止所有產品] 按鈕相同，為了增加和減少 GridView 中產品的價格，我們必須先新增適當的資料存取層和商務邏輯層方法。 因為我們已經有更新 DAL 中單一產品資料列的方法，所以我們可以藉由為 BLL 中的 `UpdateProduct` 方法建立新的多載，提供這類功能。

過去的 `UpdateProduct` 多載已將產品欄位的某種組合納入純量輸入值，然後只針對指定的產品更新這些欄位。 針對此多載，我們將會與此標準略有不同，並改為傳入產品的 `ProductID` 以及調整 `UnitPrice` 的百分比（而不是傳入新的、已調整的 `UnitPrice` 本身）。 這種方法可以簡化我們需要在 ASP.NET 網頁程式碼後置類別中撰寫的程式碼，因為我們不需要擔心如何判斷目前產品的 `UnitPrice`。

本教學課程的 `UpdateProduct` 多載如下所示：

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample8.cs)]

這個多載會透過 DAL 的 `GetProductByProductID(productID)` 方法，抓取所指定產品的相關資訊。 然後，它會檢查是否已為產品的 `UnitPrice` 指派 `NULL` 值的資料庫。 如果是，價格會原封不動地保留。 不過，如果有非`NULL` 的 `UnitPrice` 值，方法就會依照指定的百分比（`unitPriceAdjustmentPercent`）來更新產品的 `UnitPrice`。

## <a name="step-7-adding-the-increase-and-decrease-buttons-to-the-gridview"></a>步驟7：將 [增加] 和 [減少] 按鈕新增至 GridView

GridView （和 DetailsView）都是由欄位集合所組成。 除了 BoundFields、CheckBoxFields 和 TemplateFields，ASP.NET 還包含 ButtonField，其名稱暗示，會轉譯為每個資料列具有按鈕、LinkButton 或 ImageButton 的資料行。 類似于 FormView，按一下 GridView 分頁按鈕、[編輯] 或 [刪除] 按鈕、[排序按鈕] 等專案中的*任何*按鈕，都會導致回傳並引發 GridView 的[`RowCommand` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.gridview.rowcommand.aspx)。

ButtonField 具有 `CommandName` 屬性，可將指定的值指派給其每個按鈕 `CommandName` 屬性。 就像 FormView 一樣，`RowCommand` 事件處理常式會使用 `CommandName` 值來判斷所按的按鈕。

讓我們將兩個新的 ButtonFields 新增至 GridView，一個具有按鈕文字價格 + 10%，另一個具有文字價格-10%。 若要加入這些 ButtonFields，請按一下 GridView 智慧標籤中的 [編輯資料行] 連結，從左上方的清單中選取 [ButtonField] 欄位類型，然後按一下 [新增] 按鈕。

![將兩個 ButtonFields 新增至 GridView](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image48.png)

**圖 18**：將兩個 ButtonFields 新增至 GridView

移動兩個 ButtonFields，使其顯示為前兩個 GridView 欄位。 接下來，將這兩個 ButtonFields 的 [`Text` 屬性] 設定為 [價格 + 10%] 和 [價格-10%]，並將 `CommandName` 屬性分別設為 IncreasePrice 和 DecreasePrice。 根據預設，ButtonField 會將其按鈕的資料行呈現為 LinkButtons。 不過，這可以透過 ButtonField 的[`ButtonType` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.buttonfieldbase.buttontype.aspx)來變更。 讓我們將這兩個 ButtonFields 轉譯為一般的 push 按鈕;因此，請將 `ButtonType` 屬性設為 `Button`。 [圖 19] 顯示在進行這些變更之後的 [欄位] 對話方塊;之後是 GridView 的宣告式標記。

![設定 ButtonFields Text、CommandName 和 ButtonType 屬性](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image49.png)

**圖 19**：設定 ButtonFields `Text`、`CommandName`和 `ButtonType` 屬性

[!code-aspx[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample9.aspx)]

建立這些 ButtonFields 之後，最後一個步驟是建立 GridView `RowCommand` 事件的事件處理常式。 這個事件處理常式（如果因為已按下 [價格 + 10%] 或 [價格-10%] 按鈕而引發）需要判斷已按一下按鈕之資料列的 `ProductID`，然後叫用 `ProductsBLL` 類別的 `UpdateProduct` 方法，連同 `ProductID`傳遞適當的 `UnitPrice` 百分比調整。 下列程式碼會執行這些工作：

[!code-csharp[Main](adding-and-responding-to-buttons-to-a-gridview-cs/samples/sample10.cs)]

為了判斷已按下 [價格 + 10%] 或 [Price-10%] 按鈕的資料列 `ProductID`，我們需要查閱 GridView 的 `DataKeys` 集合。 這個集合會保存每個 GridView 資料列的 `DataKeyNames` 屬性中所指定的欄位值。 由於 GridView 的 `DataKeyNames` 屬性是在將 ObjectDataSource 系結至 GridView 時 Visual Studio 設定為 ProductID，因此 `DataKeys(rowIndex).Value` 會為指定的*rowIndex*提供 `ProductID`。

ButtonField 會自動傳入資料列的*rowIndex* ，其按鈕已透過 `e.CommandArgument` 參數按一下。 因此，若要判斷已按下價格 + 10% 或 Price-10% 按鈕的資料列 `ProductID`，我們使用： `Convert.ToInt32(SuppliersProducts.DataKeys(Convert.ToInt32(e.CommandArgument)).Value)`。

如同 [中斷所有產品] 按鈕，如果您已停用 GridView 的檢視狀態，GridView 就會在每次回傳時重新系結至基礎資料存放區，因此會立即更新以反映按一下時發生的價格變更其中一個按鈕。 不過，如果您在 GridView 中未停用 view 狀態，則在進行這項變更之後，您必須手動將資料重新系結至 GridView。 若要完成此動作，只需在叫用 `UpdateProduct` 方法之後，立即呼叫 GridView 的 `DataBind()` 方法。

[圖 20] 顯示起來啦阿嬤凱利的 Homestead 所提供的產品時的頁面。 [圖 21] 顯示在起來啦阿嬤的 Boysenberry 散佈後按兩次 [價格 + 10%] 按鈕時的結果，以及 Northwoods Cranberry Sauce 的 [價格-10%] 按鈕。

[![GridView 包含價格 + 10% 和價格-10% 按鈕](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image51.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image50.png)

**圖 20**： GridView 包含價格 + 10% 和 price-10% 按鈕（[按一下以觀看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image52.png)）

[![第一個和第三個產品的價格已透過價格 + 10% 和價格-10% 按鈕更新](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image54.png)](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image53.png)

**圖 21**：第一個和第三個產品的價格已透過價格 + 10% 和價格-10% 按鈕更新（[按一下以觀看完整大小的影像](adding-and-responding-to-buttons-to-a-gridview-cs/_static/image55.png)）

> [!NOTE]
> GridView （和 DetailsView）也可以將按鈕、LinkButtons 或 ImageButtons 新增至其 TemplateFields。 如同 BoundField，當您按下這些按鈕時，將會引發回傳，並引發 GridView 的 `RowCommand` 事件。 不過，在 TemplateField 中加入按鈕時，按鈕的 `CommandArgument` 不會自動設定為數據列的索引，如同使用 ButtonFields 時一樣。 如果您需要決定在 `RowCommand` 事件處理常式中按下按鈕的資料列索引，您將需要使用類似下列的程式碼，以手動方式在 TemplateField 內的宣告式語法中設定按鈕的 `CommandArgument` 屬性：  
> `<asp:Button runat="server" ... CommandArgument='<%# ((GridViewRow) Container).RowIndex %>'`

## <a name="summary"></a>總結

GridView、DetailsView 和 FormView 控制項全都可以包含按鈕、LinkButtons 或 ImageButtons。 按一下這類按鈕時，會導致回傳，並引發 [FormView] 和 [DetailsView] 控制項中的 `ItemCommand` 事件和 GridView 中的 [`RowCommand`] 事件。 這些資料 Web 控制項具有內建功能，可處理常見的命令相關動作，例如刪除或編輯記錄。 不過，我們也可以使用按下的按鈕，以回應執行我們自己的自訂程式碼。

若要完成此動作，我們必須建立 `ItemCommand` 或 `RowCommand` 事件的事件處理常式。 在此事件處理常式中，我們會先檢查傳入的 `CommandName` 值，以判斷已按下的按鈕，然後採取適當的自訂動作。 在本教學課程中，我們已瞭解如何使用按鈕和 ButtonFields 來終止指定供應商的所有產品，或將特定產品的價格增加或減少10%。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [下一個](adding-and-responding-to-buttons-to-a-gridview-vb.md)
