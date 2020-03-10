---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
title: 自訂資料修改介面（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何將標準 TextBox 和 CheckBox 控制項取代為 alternati，以自訂可編輯的 GridView 介面。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: 4830d984-bd2c-4a08-bfe5-2385599f1f7d
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/customizing-the-data-modification-interface-vb
msc.type: authoredcontent
ms.openlocfilehash: 85ec7bdde6b2bffbbda066b0441bbd36b7072197
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78592614"
---
# <a name="customizing-the-data-modification-interface-vb"></a>自訂資料修改介面 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_20_VB.exe)或[下載 PDF](customizing-the-data-modification-interface-vb/_static/datatutorial20vb1.pdf)

> 在本教學課程中，我們將探討如何將標準 TextBox 和 CheckBox 控制項取代為替代輸入 Web 控制項，以自訂可編輯 GridView 的介面。

## <a name="introduction"></a>簡介

GridView 和 DetailsView 控制項所使用的 BoundFields 和 CheckBoxFields，可簡化修改資料的程式，因為它們能夠轉譯唯讀、可編輯和可插入的介面。 這些介面可以轉譯，而不需要加入任何額外的宣告式標記或程式碼。 不過，BoundField 和 CheckBoxField 的介面缺乏實際案例所需的自訂能力。 為了在 GridView 或 DetailsView 中自訂可編輯或可插入的介面，我們必須改為使用 TemplateField。

在[先前的教學](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)課程中，我們已瞭解如何藉由新增驗證 Web 控制項來自訂資料修改介面。 在本教學課程中，我們將探討如何自訂實際的資料收集 Web 控制項，以替代輸入 Web 控制項取代 BoundField 和 CheckBoxField 的標準 TextBox 和 CheckBox 控制項。 特別是，我們將建立可編輯的 GridView，讓產品的名稱、類別、供應商和已停止狀態得以更新。 編輯特定資料列時，[類別目錄] 和 [供應商] 欄位將會轉譯為 Dropdownlist 進行，其中包含可供選擇的一組可用類別和供應商。 此外，我們會將 CheckBoxField 的預設核取方塊取代為提供兩個選項的 RadioButtonList 控制項：「作用中」和「已停止」。

[![GridView 的編輯介面包含 Dropdownlist 進行和選項按鈕](customizing-the-data-modification-interface-vb/_static/image2.png)](customizing-the-data-modification-interface-vb/_static/image1.png)

**圖 1**： GridView 的編輯介面包含 Dropdownlist 進行和選項按鈕（[按一下以觀看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image3.png)）

## <a name="step-1-creating-the-appropriateupdateproductoverload"></a>步驟1：建立適當的`UpdateProduct`多載

在本教學課程中，我們將建立可編輯的 GridView，允許編輯產品的名稱、類別、供應商和已停止的狀態。 因此，我們需要可接受五個輸入參數的 `UpdateProduct` 多載，這四個產品值加上 `ProductID`。 如同在先前的多載中，這一項將會：

1. 針對指定的 `ProductID`，從資料庫中取出產品資訊。
2. 更新 [`ProductName`]、[`CategoryID`]、[`SupplierID`] 和 [`Discontinued`] 欄位，以及
3. 透過 TableAdapter 的 `Update()` 方法，將更新要求傳送至 DAL。

為了簡潔起見，針對這個特定的多載，我省略了商務規則檢查，可確保標示為已中止的產品不是其供應商所提供的唯一產品。 您可以視需要將它新增到中，或者最好是將邏輯重構成另一個方法。

下列程式碼顯示 `ProductsBLL` 類別中的新 `UpdateProduct` 多載：

[!code-vb[Main](customizing-the-data-modification-interface-vb/samples/sample1.vb)]

## <a name="step-2-crafting-the-editable-gridview"></a>步驟2：製作可編輯的 GridView

新增 `UpdateProduct` 多載之後，我們就可以建立可編輯的 GridView。 開啟 [`EditInsertDelete`] 資料夾中的 [`CustomizedUI.aspx`] 頁面，並將 GridView 控制項新增至設計工具。 接下來，從 GridView 的智慧標籤建立新的 ObjectDataSource。 設定 ObjectDataSource 以透過 `ProductBLL` 類別的 `GetProducts()` 方法來抓取產品資訊，並使用我們剛才建立的 `UpdateProduct` 多載來更新產品資料。 從 [插入] 和 [刪除] 索引標籤中，從下拉式清單中選取 [（無）]。

[![將 ObjectDataSource 設定為使用剛建立的 UpdateProduct 多載](customizing-the-data-modification-interface-vb/_static/image5.png)](customizing-the-data-modification-interface-vb/_static/image4.png)

**圖 2**：設定 ObjectDataSource 使用剛建立的 `UpdateProduct` 多載（[按一下以查看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image6.png)）

如我們在資料修改教學課程中所見，Visual Studio 所建立之 ObjectDataSource 的宣告式語法會將 `OldValuesParameterFormatString` 屬性指派給 `original_{0}`。 這當然不會與我們的商務邏輯層搭配運作，因為我們的方法不會預期傳入原始 `ProductID` 值。 因此，如同我們在先前的教學課程中所做的，請花一點時間從宣告式語法移除此屬性指派，或改為將這個屬性的值設定為 `{0}`。

在這項變更之後，ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample2.aspx)]

請注意，`OldValuesParameterFormatString` 屬性已經移除，而且 `UpdateParameters` 集合中的 `UpdateProduct` 多載所預期的每個輸入參數都有 `Parameter`。

當 ObjectDataSource 設定為只更新產品值的子集時，GridView 目前會顯示*所有*的產品欄位。 請花點時間編輯 GridView，讓：

- 它只包含 `ProductName`、`SupplierName`、`CategoryName` BoundFields 和 `Discontinued` CheckBoxField
- 要出現在 `Discontinued` CheckBoxField 之前的 `CategoryName` 和 `SupplierName` 欄位（位於左邊）
- `CategoryName` 和 `SupplierName` BoundFields ' `HeaderText` 屬性分別設定為 "Category" 和 "供應商"
- 已啟用編輯支援（勾選 GridView 的智慧標籤中的 [啟用編輯] 核取方塊）

在這些變更之後，設計工具看起來會像 [圖 3]，其中包含 GridView 的宣告式語法，如下所示。

[![從 GridView 移除不必要的欄位](customizing-the-data-modification-interface-vb/_static/image8.png)](customizing-the-data-modification-interface-vb/_static/image7.png)

**圖 3**：從 GridView 移除不必要的欄位（[按一下以查看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image9.png)）

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample3.aspx)]

此時，GridView 的唯讀行為已完成。 當您查看資料時，每個產品都會轉譯為 GridView 中的一個資料列，以顯示產品的名稱、類別、供應商和已停止的狀態。

[![GridView 的唯讀介面已完成](customizing-the-data-modification-interface-vb/_static/image11.png)](customizing-the-data-modification-interface-vb/_static/image10.png)

**圖 4**： GridView 的唯讀介面已完成（[按一下以觀看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image12.png)）

> [!NOTE]
> 如如何[插入、更新和刪除資料教學](an-overview-of-inserting-updating-and-deleting-data-cs.md)課程中所述，請務必啟用 GridView s 檢視狀態（預設行為）。 如果您將 GridView 的 `EnableViewState` 屬性設定為 `false`，就會面臨並行使用者不小心刪除或編輯記錄的風險。 如需詳細資訊，請參閱[警告： ASP.NET 2.0 gridview/DetailsView/FormViews 的並行問題，其支援編輯及/或刪除，且已停用檢視狀態](http://scottonwriting.net/sowblog/posts/10054.aspx)。

## <a name="step-3-using-a-dropdownlist-for-the-category-and-supplier-editing-interfaces"></a>步驟3：針對類別目錄和供應商編輯介面使用 DropDownList

回想一下，`ProductsRow` 物件包含 `CategoryID`、`CategoryName`、`SupplierID`和 `SupplierName` 屬性，這會在 `Products` 資料庫資料表中提供實際的外鍵識別碼值，以及 `Name` 和 `Categories` 資料表中對應的 `Suppliers` 值。 `ProductRow`的 `CategoryID` 和 `SupplierID` 都可以讀取和寫入，而 `CategoryName` 和 `SupplierName` 屬性會標示為唯讀。

由於 `CategoryName` 和 `SupplierName` 屬性的唯讀狀態，對應的 BoundFields 已將其 `ReadOnly` 屬性設定為 `True`，防止在編輯資料列時修改這些值。 雖然我們可以將 [`ReadOnly`] 屬性設定為 [`False`]，在編輯期間將 `CategoryName` 和 `SupplierName` BoundFields 轉譯為文字方塊，這種方法會在使用者嘗試更新產品時造成例外狀況，因為 `UpdateProduct` 和 `CategoryName` 輸入中沒有 `SupplierName` 多載。 事實上，基於兩個原因，我們不想建立這種多載：

- `Products` 資料表沒有 `SupplierName` 或 `CategoryName` 欄位，但是 `SupplierID` 和 `CategoryID`。 因此，我們想要將這些特定的識別碼值（而非其查閱資料表的值）傳遞給我們的方法。
- 要求使用者輸入供應商或類別目錄的名稱不是理想的，因為它需要使用者知道可用的類別和供應商及其正確的拼寫。

[供應商] 和 [類別目錄] 欄位應該會在 [唯讀] 模式（如同現在一樣）中顯示類別目錄和供應商名稱，並在編輯時顯示適用選項的下拉式清單。 使用者可以使用下拉式清單快速查看哪些分類和供應商可供選擇，而且可以更輕鬆地進行選取。

為了提供此行為，我們必須將 `SupplierName` 和 `CategoryName` BoundFields 轉換成 TemplateFields，其 `ItemTemplate` 會發出 `SupplierName` 和 `CategoryName` 值，而其 `EditItemTemplate` 會使用 DropDownList 控制項列出可用的分類和供應商。

## <a name="adding-thecategoriesandsuppliersdropdownlists"></a>新增`Categories`和`Suppliers`Dropdownlist 進行

首先，將 `SupplierName` 和 `CategoryName` BoundFields 轉換成 TemplateFields by：按一下 GridView 智慧標籤中的 [編輯資料行] 連結;從左下方的清單中選取 BoundField;然後按一下 [將此欄位轉換成 TemplateField] 連結。 轉換程式會建立具有 `ItemTemplate` 和 `EditItemTemplate`的 TemplateField，如以下的宣告式語法所示：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample4.aspx)]

由於 BoundField 已標示為唯讀，`ItemTemplate` 和 `EditItemTemplate` 都包含一個標籤 Web 控制項，其 `Text` 屬性會系結至適用的資料欄位（在上述語法中為`CategoryName`）。 我們需要修改 `EditItemTemplate`，以 DropDownList 控制項取代標籤 Web 控制項。

如我們在先前的教學課程中所見，您可以透過設計工具或直接從宣告式語法來編輯範本。 若要透過設計工具進行編輯，請按一下 GridView 智慧標籤中的 [編輯範本] 連結，然後選擇使用 [類別目錄] 欄位的 `EditItemTemplate`。 移除標籤 Web 控制項，並以 DropDownList 控制項取代它，並將 DropDownList 的 ID 屬性設定為 `Categories`。

[![移除文字方塊，並將 DropDownList 新增至 EditItemTemplate](customizing-the-data-modification-interface-vb/_static/image14.png)](customizing-the-data-modification-interface-vb/_static/image13.png)

**圖 5**：移除文字方塊，並將 DropDownList 新增至 `EditItemTemplate` （[按一下以觀看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image15.png)）

接下來，我們需要在 DropDownList 中填入可用的類別。 按一下 DropDownList 的智慧標籤中的 [選擇資料來源] 連結，並選擇建立名為 `CategoriesDataSource`的新 ObjectDataSource。

[![建立名為 CategoriesDataSource 的新 ObjectDataSource 控制項](customizing-the-data-modification-interface-vb/_static/image17.png)](customizing-the-data-modification-interface-vb/_static/image16.png)

**圖 6**：建立名為 `CategoriesDataSource` 的新 ObjectDataSource 控制項（[按一下以查看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image18.png)）

若要讓這個 ObjectDataSource 傳回所有類別，請將它系結至 `CategoriesBLL` 類別的 `GetCategories()` 方法。

[![將 ObjectDataSource 系結至 CategoriesBLL 的 GetCategories （）方法](customizing-the-data-modification-interface-vb/_static/image20.png)](customizing-the-data-modification-interface-vb/_static/image19.png)

**圖 7**：將 ObjectDataSource 系結至 `CategoriesBLL`的 `GetCategories()` 方法（[按一下以查看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image21.png)）

最後，設定 DropDownList 的設定，讓 [`CategoryName`] 欄位顯示在每個 DropDownList `ListItem` 中，並使用 `CategoryID` 欄位做為值。

[![顯示 [類別名稱] 欄位，並使用 [類別] 做為值](customizing-the-data-modification-interface-vb/_static/image23.png)](customizing-the-data-modification-interface-vb/_static/image22.png)

**圖 8**：顯示 [`CategoryName`] 欄位，並使用 `CategoryID` 做為值（[按一下以查看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image24.png)）

進行這些變更之後，`CategoryName` TemplateField 中的 `EditItemTemplate` 宣告式標記會同時包含 DropDownList 和 ObjectDataSource：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample5.aspx)]

> [!NOTE]
> `EditItemTemplate` 中的 DropDownList 必須啟用其檢視狀態。 我們很快就會將資料系結語法新增至 DropDownList 的宣告式語法，並將資料系結命令（例如 `Eval()`，`Bind()` 只能出現在已啟用檢視狀態的控制項中。

重複這些步驟，將名為 `Suppliers` 的 DropDownList 新增至 `SupplierName` TemplateField 的 `EditItemTemplate`。 這牽涉到將 DropDownList 新增至 `EditItemTemplate` 並建立另一個 ObjectDataSource。 不過，`Suppliers` DropDownList 的 ObjectDataSource 應該設定為叫用 `SuppliersBLL` 類別的 `GetSuppliers()` 方法。 此外，將 `Suppliers` DropDownList 設定為顯示 [`CompanyName`] 欄位，並使用 [`SupplierID`] 欄位作為其 `ListItem` 的值。

將 Dropdownlist 進行新增至兩個 `EditItemTemplate` s 之後，請在瀏覽器中載入頁面，然後按一下 Chef Anton 的 Cajun Seasoning 產品的 [編輯] 按鈕。 如 [圖 9] 所示，產品的 [類別] 和 [供應商] 資料行會呈現為下拉式清單，其中包含可供選擇的可用類別和供應商。 不過，請注意，預設會選取這兩個下拉式清單中的*第一個*專案（類別的飲料，而外來液體為供應商），即使 Chef Anton 的 Cajun Seasoning 是新的奧爾良 Condiment Cajun 所提供的樂趣。

[![預設會選取下拉式清單中的第一個專案](customizing-the-data-modification-interface-vb/_static/image26.png)](customizing-the-data-modification-interface-vb/_static/image25.png)

**圖 9**：預設會選取下拉式清單中的第一個專案（[按一下以查看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image27.png)）

此外，如果您按一下 [更新]，您會發現產品的 `CategoryID` 和 `SupplierID` 值已設定為 [`NULL`]。 這兩種不想要的行為都是因為 `EditItemTemplate` s 中的 Dropdownlist 進行並未系結至基礎產品資料中的任何資料欄位所造成。

## <a name="binding-the-dropdownlists-to-thecategoryidandsupplieriddata-fields"></a>將 Dropdownlist 進行系結至`CategoryID`並`SupplierID`資料欄位

為了讓已編輯的產品類別目錄和供應商下拉式清單設定為適當的值，並在按一下 Update 時將這些值傳送回 BLL 的 `UpdateProduct` 方法，我們必須使用雙向資料系結，將 Dropdownlist 進行的 `SelectedValue` 屬性系結至 `CategoryID` 和 `SupplierID` 資料欄位。 若要使用 `Categories` DropDownList 來完成此動作，您可以將 `SelectedValue='<%# Bind("CategoryID") %>'` 直接加入至宣告式語法。

或者，您也可以透過設計工具編輯範本，然後按一下 DropDownList 的智慧標籤中的 [編輯系結] 連結，來設定 DropDownList 的系結。 接下來，請使用雙向資料系結（請參閱 [圖 10]），指出 `SelectedValue` 屬性應該系結至 `CategoryID` 欄位。 重複宣告式或設計工具程式，將 `SupplierID` 資料欄位系結至 `Suppliers` DropDownList。

[![使用雙向資料系結將類別系結至 DropDownList 的 SelectedValue 屬性](customizing-the-data-modification-interface-vb/_static/image29.png)](customizing-the-data-modification-interface-vb/_static/image28.png)

**圖 10**：使用雙向資料系結，將 `CategoryID` 系結至 DropDownList 的 `SelectedValue` 屬性（[按一下以查看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image30.png)）

一旦將系結套用至這兩個 Dropdownlist 進行的 `SelectedValue` 屬性，編輯後的產品的類別和供應商資料行就會預設為目前的產品值。 按一下 [更新] 之後，所選下拉式清單專案的 `CategoryID` 和 `SupplierID` 值將會傳遞至 `UpdateProduct` 方法。 [圖 11] 顯示在加入資料系結語句之後的教學課程;請注意，針對 Chef Anton 的 Cajun Seasoning 所選取的下拉式清單專案，如何正確 Condiment 和新的奧爾良 Cajun 樂趣。

[![已編輯的產品目前的類別和供應商的值預設為選取](customizing-the-data-modification-interface-vb/_static/image32.png)](customizing-the-data-modification-interface-vb/_static/image31.png)

**圖 11**：預設會選取已編輯的產品目前的類別和供應商值（[按一下以觀看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image33.png)）

## <a name="handlingnullvalues"></a>處理`NULL`值

`Products` 資料表中的 `CategoryID` 和 `SupplierID` 資料行可以 `NULL`，但 `EditItemTemplate` s 中的 Dropdownlist 進行不會包含清單專案來代表 `NULL` 值。 這有兩個結果：

- 使用者無法使用我們的介面將產品的類別或供應商從非`NULL` 值變更為 `NULL` 一
- 如果產品有 `NULL` `CategoryID` 或 `SupplierID`，按一下 [編輯] 按鈕將會導致例外狀況。 這是因為 `Bind()` 語句中 `CategoryID` （或 `SupplierID`）所傳回的 `NULL` 值並未對應到 DropDownList 中的值（當其 `SelectedValue` 屬性設定為*不*在其清單專案集合中的值時，DropDownList 會擲回例外狀況）。

為了支援 `NULL` `CategoryID` 和 `SupplierID` 值，我們需要將另一個 `ListItem` 新增至每個 DropDownList，以代表 `NULL` 值。 在具有 DropDownList 教學課程的[主要/詳細資料篩選](../masterdetail/master-detail-filtering-with-a-dropdownlist-cs.md)中，我們已瞭解如何將額外的 `ListItem` 新增至資料系結 DropDownList，這牽涉到將 DropDownList 的 `AppendDataBoundItems` 屬性設定為 `True` 並手動新增其他 `ListItem`。 不過在先前的教學課程中，我們新增了具有 `Value` `-1`的 `ListItem`。 不過，ASP.NET 中的資料系結邏輯會自動將空白字串轉換成 `NULL` 值，反之亦然。 因此，在本教學課程中，我們希望 `ListItem`的 `Value` 是空字串。

一開始請將 Dropdownlist 進行的 `AppendDataBoundItems` 屬性設定為 `True`。 接下來，將下列 `<asp:ListItem>` 元素新增至每個 DropDownList，以新增 `NULL` `ListItem`，讓宣告式標記看起來像這樣：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample6.aspx)]

我已選擇使用 "（None）" 做為此 `ListItem`的文字值，但如果您想要的話，也可以將它變更為空白字串。

> [!NOTE]
> 如我們在*主要/詳細資料篩選 DropDownList*教學課程中所見，您可以在 屬性視窗中按一下 DropDownList 的 `Items` 屬性（這會顯示 `ListItem` 集合編輯器），透過設計工具將 `ListItem` 新增至 DropDownList。 不過，請務必透過宣告式語法，為本教學課程新增 `NULL` `ListItem`。 如果您使用 [`ListItem` 集合編輯器]，則產生的宣告式語法會在指派空白字串時完全省略 `Value` 設定，並建立如下的宣告式標記： `<asp:ListItem>(None)</asp:ListItem>`。 雖然這看起來可能無害，但遺漏值會導致 DropDownList 在其位置使用 `Text` 屬性值。 這表示如果選取此 `NULL` `ListItem`，則會嘗試將值 "（None）" 指派給 `CategoryID`，這會導致例外狀況。 藉由明確地設定 `Value=""`，當選取 `NULL` `ListItem` 時，`NULL` 值會指派給 `CategoryID`。

針對供應商 DropDownList 重複這些步驟。

透過這項額外的 `ListItem`，編輯介面現在可以將 `NULL` 值指派給產品的 `CategoryID` 和 `SupplierID` 欄位，如 [圖 12] 所示。

[![選擇（無）為產品的類別或供應商指派 Null 值](customizing-the-data-modification-interface-vb/_static/image35.png)](customizing-the-data-modification-interface-vb/_static/image34.png)

**圖 12**：選擇 [（無）] 以指派產品類別或供應商的 `NULL` 值（[按一下以查看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image36.png)）

## <a name="step-4-using-radiobuttons-for-the-discontinued-status"></a>步驟4：針對已停止狀態使用「選項按鈕」

目前，產品的 `Discontinued` 資料欄位是使用 CheckBoxField 表示，這會呈現唯讀資料列的已停用核取方塊，以及所編輯資料列的啟用核取方塊。 雖然此使用者介面通常是合適的，但我們可以在需要時使用 TemplateField 進行自訂。 在本教學課程中，讓我們將 CheckBoxField 變更為 TemplateField，以使用具有兩個選項「作用中」和「已中止」的 RadioButtonList 控制項，使用者可以在其中指定產品的 `Discontinued` 值。

首先，將 `Discontinued` CheckBoxField 轉換成 TemplateField，這將會建立具有 `ItemTemplate` 和 `EditItemTemplate`的 TemplateField。 這兩個範本都包含一個核取方塊，其 `Checked` 屬性系結至 [`Discontinued` 資料] 欄位，兩者之間唯一的差異在於 `ItemTemplate`的核取方塊的 [`Enabled`] 屬性設為 [`False`]。

以 RadioButtonList 控制項取代 `ItemTemplate` 和 `EditItemTemplate` 中的核取方塊，同時將兩個 RadioButtonLists 的 `ID` 屬性都設定為 `DiscontinuedChoice`。 接下來，表示每個 RadioButtonLists 都應該包含兩個選項按鈕，一個標記為 "Active"，值為 "False"，另一個標記為 "已停止"，值為 "True"。 若要完成這項操作，您可以直接透過宣告式語法輸入中的 `<asp:ListItem>` 元素，或使用設計工具中的 [`ListItem` 集合編輯器]。 [圖 13] 顯示指定了兩個選項按鈕選項之後的 [`ListItem` 集合編輯器]。

[![將作用中和已停止的選項新增至 RadioButtonList](customizing-the-data-modification-interface-vb/_static/image38.png)](customizing-the-data-modification-interface-vb/_static/image37.png)

**圖 13**：將作用中和已停止的選項新增至 RadioButtonList （[按一下以觀看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image39.png)）

因為 `ItemTemplate` 中的 RadioButtonList 不應該是可編輯的，請將其 `Enabled` 屬性設定為 [`False`]，讓 `True` 中 RadioButtonList 的 `Enabled` 屬性 `EditItemTemplate`（預設值）。 這會使非編輯的資料列中的選項按鈕變成隻讀，但可讓使用者變更編輯過之資料列的按鈕值。

我們仍然需要指派 RadioButtonList 控制項的 `SelectedValue` 屬性，以便根據產品的 [`Discontinued` 資料] 欄位選取適當的選項按鈕。 如同本教學課程稍早所述的 Dropdownlist 進行，這個資料系結語法可以直接加入宣告式標記中，或透過 RadioButtonLists 的智慧標籤中的 [編輯資料系結] 連結新增。

加入兩個 RadioButtonLists 並加以設定之後，`Discontinued` TemplateField 的宣告式標記看起來應該像這樣：

[!code-aspx[Main](customizing-the-data-modification-interface-vb/samples/sample7.aspx)]

有了這些變更，就會將 [`Discontinued`] 資料行從核取方塊清單轉換為選項按鈕組清單（請參閱 [圖 14]）。 編輯產品時，會選取適當的選項按鈕，然後按一下 [其他] 選項按鈕，再按 [更新]，即可更新產品的已停止狀態。

[![已停止的核取方塊已由選項按鈕組取代](customizing-the-data-modification-interface-vb/_static/image41.png)](customizing-the-data-modification-interface-vb/_static/image40.png)

**圖 14**：已停止的核取方塊已由選項按鈕組取代（[按一下以觀看完整大小的影像](customizing-the-data-modification-interface-vb/_static/image42.png)）

> [!NOTE]
> 因為 `Products` 資料庫中的 `Discontinued` 資料行不能有 `NULL` 的值，所以我們不需要擔心在介面中捕捉 `NULL` 資訊。 不過，如果 `Discontinued` 的資料行可以包含 `NULL` 值，我們會想要將第三個選項按鈕加入至清單，並將其 `Value` 設定為空字串（`Value=""`），就像類別目錄和供應商 Dropdownlist 進行一樣。

## <a name="summary"></a>總結

雖然 BoundField 和 CheckBoxField 會自動呈現唯讀、編輯和插入介面，但它們缺乏自訂的能力。 不過，通常我們需要自訂編輯或插入介面，也許加入驗證控制項（如先前的教學課程中所見），或是自訂資料收集使用者介面（如本教學課程中所見）。 在下列步驟中，您可以使用 TemplateField 自訂介面：

1. 新增 TemplateField，或將現有的 BoundField 或 CheckBoxField 轉換成 TemplateField
2. 視需要擴充介面
3. 使用雙向資料系結將適當的資料欄位系結至新加入的 Web 控制項

除了使用內建的 ASP.NET Web 控制項以外，您也可以使用自訂、編譯的伺服器控制項和使用者控制項來自訂 TemplateField 的範本。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb.md)
> [下一頁](implementing-optimistic-concurrency-vb.md)
