---
uid: web-forms/overview/data-access/working-with-batched-data/batch-inserting-cs
title: 批次插入C#（） |Microsoft Docs
author: rick-anderson
description: 瞭解如何在單一作業中插入多個資料庫記錄。 在使用者介面層中，我們延伸了 GridView，讓使用者可以輸入多個 n 。
ms.author: riande
ms.date: 06/26/2007
ms.assetid: cf025e08-48fc-4385-b176-8610aa7b5565
msc.legacyurl: /web-forms/overview/data-access/working-with-batched-data/batch-inserting-cs
msc.type: authoredcontent
ms.openlocfilehash: 5dc4d0b6ac9bf3aa2baa54fe9f5d4149494e47d2
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78618521"
---
# <a name="batch-inserting-c"></a>批次插入 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載程式代碼](https://download.microsoft.com/download/3/9/f/39f92b37-e92e-4ab3-909e-b4ef23d01aa3/ASPNET_Data_Tutorial_66_CS.zip)或[下載 PDF](batch-inserting-cs/_static/datatutorial66cs1.pdf)

> 瞭解如何在單一作業中插入多個資料庫記錄。 在使用者介面層中，我們延伸了 GridView，讓使用者可以輸入多個新記錄。 在資料存取層中，我們會將多個插入作業包裝在交易中，以確保所有插入都成功，或所有插入都已回復。

## <a name="introduction"></a>簡介

在[批次更新](batch-updating-cs.md)教學課程中，我們探討了自訂 GridView 控制項來呈現可編輯多筆記錄的介面。 流覽頁面的使用者可以進行一系列的變更，然後按一下滑鼠按鍵，執行批次更新。 在使用者經常更新許多筆記錄的情況下，相較于在[插入、更新和刪除資料](../editing-inserting-and-deleting-data/an-overview-of-inserting-updating-and-deleting-data-cs.md)教學課程的總覽中第一次探索的預設個別列編輯功能，這類介面可以節省無數點按和鍵盤到滑鼠的內容切換。

這種概念也可以在加入記錄時套用。 想像一下，在 Northwind 商貿中，我們通常會收到供應商的出貨，其中包含特定類別的多項產品。 例如，我們可能會收到來自東京貿易的六個不同茶和咖啡產品的出貨。 如果使用者透過 DetailsView 控制項一次輸入六個產品，他們就必須再次選擇許多相同的值：他們必須選擇相同的類別（飲料）、相同的供應商（東京貿易）、相同的已中斷值（False）和順序值的相同單位（0）。 這個重複的資料輸入不僅耗時，而且容易發生錯誤。

有了一些工作，我們可以建立一個批次插入介面，讓使用者選擇一次供應商和類別，輸入一系列產品名稱和單位價格，然後按一下按鈕將新產品新增至資料庫（請參閱 [圖 1]）。 隨著每個產品的加入，其 `ProductName` 和 `UnitPrice` 資料欄位都會指派文字方塊中輸入的值，而其 `CategoryID` 和 `SupplierID` 值會從表單頂端的 Dropdownlist 進行中指派值。 `Discontinued` 和 `UnitsOnOrder` 值會分別設定為 `false` 和0的硬式編碼值。

[![批次插入介面](batch-inserting-cs/_static/image2.png)](batch-inserting-cs/_static/image1.png)

**圖 1**：批次插入介面（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image3.png)）

在本教學課程中，我們將建立一個頁面，以執行 [圖 1] 所示的批次插入介面。 如同先前的兩個教學課程，我們會將插入內容包裝在交易範圍內，以確保不可部分完成性。 讓我們開始吧！

## <a name="step-1-creating-the-display-interface"></a>步驟1：建立顯示介面

本教學課程將包含分成兩個區域的單一頁面：顯示區域和插入區域。 我們將在此步驟中建立的顯示介面會顯示 GridView 中的產品，並包含標題為 [處理產品出貨] 的按鈕。 按一下此按鈕時，會以插入介面取代顯示介面，如 [圖 1] 所示。 當您按一下 [從出貨新增產品] 或 [取消] 按鈕之後，顯示介面就會返回。 我們將在步驟2中建立插入介面。

建立具有兩個介面的頁面時，一次只會顯示其中一個，而每個介面通常會放在[面板 Web 控制項](http://www.w3schools.com/aspnet/control_panel.asp)內，做為其他控制項的容器。 因此，我們的頁面會針對每個介面控制一個面板。

一開始先開啟 [`BatchData`] 資料夾中的 [`BatchInsert.aspx`] 頁面，並將面板從 [工具箱] 拖曳至設計工具（請參閱 [圖 2]）。 將面板的 `ID` 屬性設定為 [`DisplayInterface`]。 將面板新增至設計工具時，其 [`Height`] 和 [`Width`] 屬性會分別設定為50px 和125px。 清除屬性視窗中的這些屬性值。

[![將面板從 [工具箱] 拖曳至設計工具](batch-inserting-cs/_static/image5.png)](batch-inserting-cs/_static/image4.png)

**圖 2**：將面板從 [工具箱] 拖曳至設計工具（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image6.png)）

接下來，將 [按鈕] 和 [GridView] 控制項拖曳至面板。 將 [按鈕 `ID`] 屬性設定為 [`ProcessShipment`] 和其 [`Text`] 屬性，以處理產品出貨。 將 GridView 的 `ID` 屬性設定為 `ProductsGrid`，並將其從智慧標籤系結至名為 `ProductsDataSource`的新 ObjectDataSource。 設定 ObjectDataSource 以從 `ProductsBLL` 類別的 `GetProducts` 方法提取其資料。 由於此 GridView 僅用於顯示資料，因此請將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。 按一下 [完成] 完成 [設定資料來源嚮導]。

[![顯示從 ProductsBLL 類別 s GetProducts 方法傳回的資料](batch-inserting-cs/_static/image8.png)](batch-inserting-cs/_static/image7.png)

**圖 3**：顯示從 `ProductsBLL` 類別的 `GetProducts` 方法傳回的資料（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image9.png)）

[![將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]](batch-inserting-cs/_static/image11.png)](batch-inserting-cs/_static/image10.png)

**圖 4**：將 [更新]、[插入] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）] （[按一下以查看完整大小的影像](batch-inserting-cs/_static/image12.png)）

完成 ObjectDataSource wizard 之後，Visual Studio 會為產品資料欄位新增 BoundFields 和 CheckBoxField。 移除除了 [`ProductName`]、[`CategoryName`]、[`SupplierName`]、[`UnitPrice`] 和 [`Discontinued`] 欄位以外的所有 您可以隨意進行任何美觀自訂。 我決定將 `UnitPrice` 欄位格式化為貨幣值、重新排序欄位，並將數個欄位重新命名 `HeaderText` 值。 此外，請檢查 GridView s 智慧標籤中的 [啟用分頁] 和 [啟用排序] 核取方塊，以將 GridView 設定為包含分頁和排序支援。

加入面板、按鈕、GridView 和 ObjectDataSource 控制項並自訂 GridView 欄位之後，您的頁面宣告式標記看起來應該如下所示：

[!code-aspx[Main](batch-inserting-cs/samples/sample1.aspx)]

請注意，按鈕和 GridView 的標記會出現在開頭和結尾 `<asp:Panel>` 標記內。 由於這些控制項位於 `DisplayInterface` 面板中，因此只要將面板的 `Visible` 屬性設定為 [`false`]，就可以隱藏它們。 步驟3查看以程式設計方式變更面板的 `Visible` 屬性，以回應按鈕按一下以顯示一個介面，同時隱藏另一個介面。

請花點時間透過瀏覽器來查看進度。 如 [圖 5] 所示，您應該會在 GridView 上方看到一個 [處理產品出貨] 按鈕，其中列出一次的產品十個。

[![GridView 列出產品並提供排序和分頁功能](batch-inserting-cs/_static/image14.png)](batch-inserting-cs/_static/image13.png)

**圖 5**： GridView 會列出產品並提供排序和分頁功能（[按一下以觀看完整大小的影像](batch-inserting-cs/_static/image15.png)）

## <a name="step-2-creating-the-inserting-interface"></a>步驟2：建立插入介面

顯示介面完成後，我們就可以開始建立插入介面。 在本教學課程中，我們將建立一個插入介面，它會提示您輸入單一供應商和類別目錄值，然後允許使用者輸入最多五個產品名稱和單位價格值。 在此介面中，使用者可以新增一到五個新產品，全都共用相同的類別和供應商，但擁有唯一的產品名稱和價格。

從 [工具箱] 將面板拖曳到設計工具上，然後將它放在現有的 `DisplayInterface` 面板底下。 將這個新加入之面板的 `ID` 屬性設定為 [`InsertingInterface`]，並將其 [`Visible`] 屬性設定為 [`false`]。 我們會新增程式碼，將 `InsertingInterface` 面板的 `Visible` 屬性設定為步驟3中的 `true`。 也請清除面板的 `Height`，並 `Width` 屬性值。

接下來，我們需要建立如 [圖 1] 所示的插入介面。 這個介面可以透過各種 HTML 技術來建立，但我們會使用一個相當簡單的方法：四個數據行、七個數據列的資料表。

> [!NOTE]
> 輸入 HTML `<table>` 元素的標記時，我偏好使用來源視圖。 雖然 Visual Studio 的確有工具可透過設計工具加入 `<table>` 元素，但設計工具似乎都不願意將 `style` 設定的 unasked 插入標記中。 建立 `<table>` 標記之後，我通常會回到設計工具來加入 Web 控制項並設定其屬性。 建立具有預先決定之資料行和資料列的資料表時，我偏好使用靜態 HTML，而不是[資料表 web 控制項](https://msdn.microsoft.com/library/system.web.ui.webcontrols.table.aspx)，因為放置在資料表 web 控制項內的任何 Web 控制項只能使用 `FindControl("controlID")` 模式來存取。 不過，我會針對動態大小的資料表（其資料列或資料行是以某些資料庫或使用者指定的準則為基礎）使用資料表 Web 控制項，因為可以用程式設計的方式來構造資料表 Web 控制項。

在 `InsertingInterface` 面板的 `<asp:Panel>` 標籤內輸入下列標記：

[!code-html[Main](batch-inserting-cs/samples/sample2.html)]

此 `<table>` 標記尚未包含任何 Web 控制項，我們會暫時新增這些控制項。 請注意，每個 `<tr>` 元素都包含特定的 CSS 類別設定： `BatchInsertHeaderRow`，供供應商和類別 Dropdownlist 進行的標頭資料列使用;針對頁尾資料列 `BatchInsertFooterRow`，其中 [從出貨] 和 [取消] 按鈕的 [加入產品] 將會執行;以及將包含 [產品] 和 [單價] 文字方塊控制項之資料列的替代 `BatchInsertRow` 和 `BatchInsertAlternatingRow` 值。 我在 `Styles.css` 檔案中建立了對應的 CSS 類別，讓插入介面的外觀類似于我們在這些教學課程中使用的 GridView 和 DetailsView 控制項。 這些 CSS 類別如下所示。

[!code-css[Main](batch-inserting-cs/samples/sample3.css)]

輸入此標記之後，請返回設計檢視。 此 `<table>` 應該會在設計工具中顯示為四個數據行、七個數據列的資料表，如 [圖 6] 所示。

[插入介面 ![包含四個數據行、七個數據列的資料表](batch-inserting-cs/_static/image17.png)](batch-inserting-cs/_static/image16.png)

**圖 6**：插入介面包含四個數據行、七個數據列的資料表（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image18.png)）

我們現在已準備好將 Web 控制項新增至插入介面。 將兩個 Dropdownlist 進行從 [工具箱] 拖曳到資料表中適用于供應商的適當資料格，而另一個用於類別目錄。

將供應商 DropDownList 的 `ID` 屬性設定為 `Suppliers`，並將它系結至名為 `SuppliersDataSource`的新 ObjectDataSource。 設定新的 ObjectDataSource 以從 `SuppliersBLL` 類別的 `GetSuppliers` 方法取出其資料，並將 [更新] 索引標籤 s 下拉式清單設為 [（無）]。 按一下 [完成] 完成精靈。

[![將 ObjectDataSource 設定為使用 SuppliersBLL 類別的 GetSuppliers 方法](batch-inserting-cs/_static/image20.png)](batch-inserting-cs/_static/image19.png)

**圖 7**：設定 ObjectDataSource 使用 `SuppliersBLL` 類別的 `GetSuppliers` 方法（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image21.png)）

讓 `Suppliers` DropDownList 顯示 [`CompanyName` 資料] 欄位，並使用 [`SupplierID` 資料] 欄位作為其 `ListItem` s 值。

[![顯示 [公司名稱] 欄位，並使用 [供應商] 作為值](batch-inserting-cs/_static/image23.png)](batch-inserting-cs/_static/image22.png)

**圖 8**：顯示 `CompanyName` 資料欄位，並使用 `SupplierID` 作為值（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image24.png)）

將第二個 DropDownList 命名為 `Categories`，並將它系結至名為 `CategoriesDataSource`的新 ObjectDataSource。 將 `CategoriesDataSource` ObjectDataSource 設定為使用 `CategoriesBLL` 類別 s `GetCategories` 方法;將 [更新] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]，然後按一下 [完成] 以完成嚮導。 最後，讓 DropDownList 顯示 `CategoryName` 資料欄位，並使用 `CategoryID` 做為值。

新增這兩個 Dropdownlist 進行並系結至適當設定的 ObjectDataSources 之後，您的畫面看起來應該像 [圖 9]。

[![標頭資料列現在包含 [供應商和類別] Dropdownlist 進行](batch-inserting-cs/_static/image26.png)](batch-inserting-cs/_static/image25.png)

**圖 9**：標頭資料列現在包含 `Suppliers` 和 `Categories` Dropdownlist 進行（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image27.png)）

我們現在需要建立文字方塊，以收集每個新產品的名稱和價格。 將 TextBox 控制項從 [工具箱] 拖曳至設計工具中，每個產品名稱和價格資料列各有一個。 將文字方塊的 [`ID` 屬性] 設定為 [`ProductName1`]、[`UnitPrice1`]、[`ProductName2`]、[`UnitPrice2`]、[`ProductName3`] 等等。`UnitPrice3`

在每個 [單價] 文字方塊之後加入 CompareValidator，將 [`ControlToValidate`] 屬性設定為適當的 `ID`。 同時將 `Operator` 屬性設定為 `GreaterThanEqual`、`ValueToCompare` 為 0 和 `Type` 至 `Currency`。 這些設定會指示 CompareValidator 確保輸入的價格是大於或等於零的有效貨幣值。 將 [`Text`] 屬性設定為 [\*]，`ErrorMessage` [價格] 必須大於或等於零。 此外，請省略任何貨幣符號。

> [!NOTE]
> 插入介面不會包含任何 RequiredFieldValidator 控制項，即使 `Products` 資料庫資料表中的 `ProductName` 欄位不允許 `NULL` 值也一樣。 這是因為我們想要讓使用者輸入最多五個產品。 例如，如果使用者要提供前三個數據列的產品名稱和單價，將最後兩個數據列保留空白，我們只會將三個新產品新增至系統。 不過，由於 `ProductName` 是必要的，因此我們需要以程式設計方式檢查，以確保在輸入單位價格時，是否已提供對應的產品名稱值。 我們會在步驟4中解決這項檢查。

驗證使用者的輸入時，如果值包含貨幣符號，CompareValidator 會報告不正確資料。 將每個單價文字方塊前面的 $ 新增為視覺提示，以指示使用者在輸入價格時省略貨幣符號。

最後，在 [`InsertingInterface`] 面板中新增 ValidationSummary 控制項，並將其 `ShowMessageBox` 屬性設定為 `true`，並將其 `ShowSummary` 屬性設為 [`false`]。 使用這些設定時，如果使用者輸入不正確單位價格值，則會在有問題的 TextBox 控制項旁出現星號，而 ValidationSummary 會顯示用戶端 messagebox，其中顯示我們先前指定的錯誤訊息。

此時，您的畫面看起來應該像 [圖 10]。

[![插入介面現在包含產品名稱和價格的文字方塊](batch-inserting-cs/_static/image29.png)](batch-inserting-cs/_static/image28.png)

**圖 10**：插入介面現在包含產品名稱和價格的文字方塊（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image30.png)）

接下來，我們需要將 [從出貨新增產品] 和 [取消] 按鈕加入頁尾資料列。 將兩個按鈕控制項從 [工具箱] 拖曳至插入介面的頁尾，將 [按鈕] `ID` 屬性設定為 [`AddProducts`] 和 [`CancelButton`] 和 [`Text` 屬性]，分別從 [出貨] 和 [取消] 新增產品。 此外，將 [`CancelButton` 控制項] `CausesValidation` 屬性設定為 [`false`]。

最後，我們需要新增標籤 Web 控制項，以顯示兩個介面的狀態訊息。 例如，當使用者成功新增產品的新出貨時，我們想要回到顯示介面，並顯示確認訊息。 不過，如果使用者提供新產品的價格，但保留產品名稱，則需要顯示警告訊息，因為 [`ProductName`] 欄位是必要的。 因為我們需要此訊息來顯示這兩個介面，所以請將它放在面板外的頁面頂端。

將 [標籤] Web 控制項從 [工具箱] 拖曳至設計工具中頁面的頂端。 將 [`ID`] 屬性設定為 [`StatusLabel`]，清除 [`Text`] 屬性，然後將 [`Visible`] 和 [`EnableViewState`] 屬性設定為 [`false`]。 如同在先前的教學課程中所見，將 `EnableViewState` 屬性設定為 `false` 可讓我們以程式設計方式變更標籤的屬性值，並讓它們在後續回傳時，自動回復為預設值。 這會簡化顯示狀態訊息的程式碼，以回應後續回傳時消失的某些使用者動作。 最後，將 [`StatusLabel` 控制項] `CssClass` 屬性設定為 [警告]，這是在 `Styles.css` 中定義的 CSS 類別名稱，會以大、斜體、粗體、紅色字型顯示文字。

[圖 11] 顯示新增和設定標籤之後的 Visual Studio 設計工具。

[![將 StatusLabel 控制項放在兩個面板控制項的上方](batch-inserting-cs/_static/image32.png)](batch-inserting-cs/_static/image31.png)

**圖 11**：將 `StatusLabel` 控制項放在兩個面板控制項上方（[按一下以觀看完整大小的影像](batch-inserting-cs/_static/image33.png)）

## <a name="step-3-switching-between-the-display-and-inserting-interfaces"></a>步驟3：在顯示和插入介面之間切換

此時，我們已完成顯示和插入介面的標記，但仍保留兩個工作：

- 在顯示和插入介面之間切換
- 將出貨中的產品加入至資料庫

目前顯示介面可見，但插入介面已隱藏。 這是因為 `DisplayInterface` 面板 `Visible` 屬性會設定為 `true` （預設值），而 `InsertingInterface` 面板 s `Visible` 屬性會設定為 `false`。 若要在兩個介面之間切換，我們只需要切換每個控制項 `Visible` 屬性值。

當按一下 [處理產品出貨] 按鈕時，我們想要從顯示介面移至插入介面。 因此，請為這個按鈕的 `Click` 事件建立事件處理常式，其中包含下列程式碼：

[!code-csharp[Main](batch-inserting-cs/samples/sample4.cs)]

這段程式碼只會隱藏 [`DisplayInterface`] 面板，並顯示 [`InsertingInterface`] 面板。

接下來，在插入介面中，為 [從出貨新增產品] 和 [取消] 按鈕控制項建立事件處理常式。 當按一下其中一個按鈕時，我們必須還原回顯示介面。 建立這兩個按鈕控制項的 `Click` 事件處理常式，讓他們呼叫 `ReturnToDisplayInterface`，這是我們將會馬上新增的方法。 除了隱藏 [`InsertingInterface`] 面板和顯示 [`DisplayInterface`] 面板之外，`ReturnToDisplayInterface` 方法還必須將 Web 控制項傳回至其預先編輯狀態。 這牽涉到將 Dropdownlist 進行 `SelectedIndex` 屬性設定為0，並清除 TextBox 控制項的 `Text` 屬性。

> [!NOTE]
> 如果我們未在回到顯示介面之前將控制項傳回至其預先編輯狀態，請考慮可能會發生的情況。 使用者可以按一下 [處理產品出貨] 按鈕，輸入出貨中的產品，然後按一下 [從出貨新增產品]。 這會新增產品，並將使用者傳回到顯示介面。 此時，使用者可能會想要新增另一個出貨。 按一下 [處理產品出貨] 按鈕時，他們會回到插入介面，但 DropDownList 選擇和文字方塊值仍會以先前的值填入。

[!code-csharp[Main](batch-inserting-cs/samples/sample5.cs)]

`Click` 事件處理常式都只會呼叫 `ReturnToDisplayInterface` 方法，不過我們會回到步驟4中的 [從出貨新增產品] `Click` 事件處理常式，然後加入程式碼以儲存產品。 `ReturnToDisplayInterface` 一開始會將 `Suppliers` 和 `Categories` Dropdownlist 進行傳回至其第一個選項。 兩個常數 `firstControlID` 和 `lastControlID` 會標記插入介面中用來命名 [產品名稱] 和 [單價] 文字方塊的開始和結束控制項索引值，並用於 `for` 迴圈的界限，將 TextBox 控制項的 `Text` 屬性設回空字串。 最後，面板 `Visible` 屬性會重設，以便隱藏插入介面並顯示顯示介面。

請花點時間在瀏覽器中測試此頁面。 第一次造訪頁面時，您應該會看到顯示介面，如 [圖 5] 所示。 按一下 [處理產品出貨] 按鈕。 頁面將回傳，您現在應該會看到插入介面，如 [圖 12] 所示。 按一下 [從出貨新增產品] 或 [取消] 按鈕，即可將您返回顯示介面。

> [!NOTE]
> 在觀看插入介面時，請花點時間測試 [單價] 文字方塊上的 CompareValidators。 當您按一下 [從出貨新增產品] 按鈕時，您應該會看到用戶端 messagebox 警告，其貨幣值或價格值小於零。

[按一下 [處理產品出貨] 按鈕之後，會顯示插入介面 ![](batch-inserting-cs/_static/image35.png)](batch-inserting-cs/_static/image34.png)

**圖 12**：按一下 [處理產品出貨] 按鈕之後，即會顯示插入介面（[按一下以查看完整大小的影像](batch-inserting-cs/_static/image36.png)）

## <a name="step-4-adding-the-products"></a>步驟4：新增產品

本教學課程剩下的工作，就是將產品儲存到資料庫的 [從出貨新增產品] 按鈕 `Click` 事件處理常式。 建立 `ProductsDataTable` 並為每個提供的產品名稱加入 `ProductsRow` 實例，即可完成這項作業。 加入這些 `ProductsRow` 之後，我們就會呼叫傳入 `ProductsDataTable`的 `ProductsBLL` 類別 s `UpdateWithTransaction` 方法。 回想一下，在交易教學課程的[包裝資料庫修改](wrapping-database-modifications-within-a-transaction-cs.md)中所建立的 `UpdateWithTransaction` 方法，會將 `ProductsDataTable` 傳遞至 `ProductsTableAdapter` 的 `UpdateWithTransaction` 方法。 從該處開始，會啟動 ADO.NET 交易，而 TableAdapter 會針對 DataTable 中的每個加入的 `ProductsRow`，將 `INSERT` 語句發出到資料庫。 假設所有產品都已新增而不發生錯誤，則會認可交易，否則會回復。

[從出貨新增產品] 按鈕 `Click` 事件處理常式的程式碼，也必須執行一些錯誤檢查。 由於插入介面中沒有使用 RequiredFieldValidators，因此使用者可以在省略其名稱時輸入產品的價格。 由於產品的名稱是必要的，因此，如果這類條件色彩，我們需要提醒使用者，而不要繼續進行插入。 完整的 `Click` 事件處理常式程式碼如下所示：

[!code-csharp[Main](batch-inserting-cs/samples/sample6.cs)]

事件處理常式一開始會先確保 `Page.IsValid` 屬性會傳回 `true`的值。 如果它傳回 `false`，則表示有一或多個 CompareValidators 報告了不正確資料;在這種情況下，我們不想要嘗試插入輸入的產品，或是在嘗試將使用者輸入的單位價格值指派給 `ProductsRow` 的 `UnitPrice` 屬性時，最後會發生例外狀況。

接下來，會建立新的 `ProductsDataTable` 實例（`products`）。 `for` 迴圈是用來逐一查看 [產品名稱] 和 [單價] 文字方塊，而 `Text` 屬性會讀入本機變數 `productName` 和 `unitPrice`。 如果使用者已輸入單價的值，而不是對應的產品名稱，則 `StatusLabel` 會在您提供單價時顯示訊息，而您也必須包含產品的名稱，而且事件處理常式會結束。

如果已提供產品名稱，則會使用 `ProductsDataTable` s `NewProductsRow` 方法來建立新的 `ProductsRow` 實例。 這個新的 `ProductsRow` 實例 `ProductName` 屬性會設定為 [目前的產品名稱] 文字方塊，而 `SupplierID` 和 `CategoryID` 屬性則會指派給插入介面 s 標頭中 Dropdownlist 進行的 `SelectedValue` 屬性。 如果使用者輸入產品價格的值，則會將其指派給 `ProductsRow` 實例 `UnitPrice` 屬性;否則，屬性會保留為未指派，這會導致資料庫中 `UnitPrice` 的 `NULL` 值。 最後，`Discontinued` 和 `UnitsOnOrder` 屬性會分別指派給硬式編碼的值 `false` 和0。

將屬性指派給 `ProductsRow` 實例之後，就會將其新增至 `ProductsDataTable`。

當 `for` 迴圈完成時，我們會檢查是否已新增任何產品。 畢竟，使用者可以在輸入任何產品名稱或價格之前，先按一下 [從出貨新增產品]。 如果 `ProductsDataTable`中至少有一個產品，則會呼叫 `ProductsBLL` 類別 s `UpdateWithTransaction` 方法。 接下來，資料會重新系結至 `ProductsGrid` GridView，使新加入的產品會出現在顯示介面中。 `StatusLabel` 會更新以顯示確認訊息，並叫用 `ReturnToDisplayInterface`，隱藏插入介面並顯示顯示介面。

如果未輸入任何產品，插入的介面仍會顯示，但不會新增任何產品的訊息。 請在顯示的文字方塊中輸入產品名稱和單位價格。

圖 s 13、14和15顯示插入和顯示介面的作用中。 在 [圖 13] 中，使用者輸入的單位價格值沒有對應的產品名稱。 [圖 14] 顯示成功新增三個新產品後的顯示介面，而 [圖 15] 顯示 GridView 中新增的兩個產品（第三個是在前一頁）。

[輸入單位價格時，需要 ![產品名稱](batch-inserting-cs/_static/image38.png)](batch-inserting-cs/_static/image37.png)

**圖 13**：輸入單位價格時，需要產品名稱（[按一下以觀看完整大小的影像](batch-inserting-cs/_static/image39.png)）

[已為供應商 Mayumi 加入 ![三個新 Veggies](batch-inserting-cs/_static/image41.png)](batch-inserting-cs/_static/image40.png)

**圖 14**：已為供應商 Mayumi 新增三個新的 Veggies （[按一下以觀看完整大小的影像](batch-inserting-cs/_static/image42.png)）

[![新產品可在 GridView 的最後一頁中找到](batch-inserting-cs/_static/image44.png)](batch-inserting-cs/_static/image43.png)

**圖 15**：新產品可在 GridView 的最後一頁中找到（[按一下以觀看完整大小的影像](batch-inserting-cs/_static/image45.png)）

> [!NOTE]
> 本教學課程中使用的批次插入邏輯會在交易範圍內包裝插入。 若要確認這一點，特意會引進資料庫層級錯誤。 例如，不是將新的 `ProductsRow` 實例 s `CategoryID` 屬性指派給 `Categories` DropDownList 中選取的值，而是將它指派給 `i * 5`之類的值。 這裡 `i` 是循環索引器，其值的範圍從1到5。 因此，在批次插入中新增兩個或多個產品時，第一個產品會有有效的 `CategoryID` 值（5），但後續產品的 `CategoryID` 值不符合 `Categories` 資料表中 `CategoryID` 值。 最後的結果是，當第一個 `INSERT` 成功時，後續的工作將會失敗，並出現外鍵條件約束違規。 因為批次插入是不可部分完成的，所以第一個 `INSERT` 將會復原，並在批次插入程式開始之前，將資料庫還原至其狀態。

## <a name="summary"></a>總結

在此和前兩個教學課程中，我們已建立可允許更新、刪除和插入批次資料的介面，這些都是使用我們在交易教學課程的[包裝資料庫修改](wrapping-database-modifications-within-a-transaction-cs.md)中新增至資料存取層的交易支援。 在某些情況下，這類批次處理使用者介面會藉由減少點擊次數、回傳和鍵盤到滑鼠內容切換，同時保有基礎資料的完整性，大幅提升使用者效率。

本教學課程會完成使用批次資料的檢查。 下一組教學課程會探索各種先進的資料存取層案例，包括在 TableAdapter 的方法中使用預存程式、在 DAL 中設定連接和命令層級的設定、加密連接字串等等！

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Hilton Giesenow 和 S ren Jacob Lauritsen。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](batch-deleting-cs.md)
> [下一頁](wrapping-database-modifications-within-a-transaction-vb.md)
