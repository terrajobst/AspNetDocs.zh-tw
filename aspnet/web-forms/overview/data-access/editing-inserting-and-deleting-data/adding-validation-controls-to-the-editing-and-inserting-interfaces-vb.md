---
uid: web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
title: 將驗證控制項新增至編輯和插入介面（VB） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將瞭解如何輕鬆地將驗證控制項新增至資料 Web 控制項的 EditItemTemplate 和 InsertItemTemplate，以提供更多 。
ms.author: riande
ms.date: 07/17/2006
ms.assetid: e3d7028a-7a22-4a4f-babe-d53afc41c0e2
msc.legacyurl: /web-forms/overview/data-access/editing-inserting-and-deleting-data/adding-validation-controls-to-the-editing-and-inserting-interfaces-vb
msc.type: authoredcontent
ms.openlocfilehash: 5c5ad110ee0836f0a464b02a2b29254e2e06381e
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74571066"
---
# <a name="adding-validation-controls-to-the-editing-and-inserting-interfaces-vb"></a>將驗證控制項新增至編輯和插入介面 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_19_VB.exe)或[下載 PDF](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/datatutorial19vb1.pdf)

> 在本教學課程中，我們將瞭解如何輕鬆地將驗證控制項新增至資料 Web 控制項的 EditItemTemplate 和 InsertItemTemplate，以提供更可靠的使用者介面。

## <a name="introduction"></a>簡介

在過去三個教學課程中，我們所探討的範例中的 GridView 和 DetailsView 控制項全都是由 BoundFields 和 CheckBoxFields 所組成（在將 GridView 或 DetailsView 系結至資料來源時，Visual Studio 自動新增的欄位類型透過智慧標籤進行控制。 編輯 GridView 或 DetailsView 中的資料列時，那些非唯讀的 BoundFields 會轉換成 textbox，使用者可以從該文字方塊修改現有的資料。 同樣地，將新記錄插入 DetailsView 控制項時，`InsertVisible` 屬性設為 `True` （預設值）的 BoundFields 會轉譯為空白文字方塊，使用者可以在其中提供新記錄的域值。 同樣地，在「標準」、「唯讀」介面中停用的 CheckBoxFields 會在編輯和插入介面中轉換成已啟用的核取方塊。

雖然 BoundField 和 CheckBoxField 的預設編輯和插入介面可能很有説明，但介面缺少任何類型的驗證。 如果使用者輸入錯誤（例如省略 `ProductName` 欄位，或為 `UnitsInStock` 輸入不正確值（例如-50），則會從應用程式架構的深度中引發例外狀況。 雖然可以適當地處理這個例外狀況（如[前一個教學](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)課程中所示），但在理想的情況下，編輯或插入使用者介面會包含驗證控制項，以防止使用者一開始就輸入這類不正確資料。

為了提供自訂的編輯或插入介面，我們必須將 BoundField 或 CheckBoxField 取代為 TemplateField。 TemplateFields，這是在 GridView 控制項中[使用 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)和在 DetailsView 控制項教學課程中[使用 TemplateFields](../custom-formatting/using-templatefields-in-the-detailsview-control-vb.md)所討論的主題，可以包含多個範本，為不同的資料列狀態定義不同的介面。 TemplateField 的 `ItemTemplate` 用於轉譯 DetailsView 或 GridView 控制項中的唯讀欄位或資料列時，而 `EditItemTemplate` 和 `InsertItemTemplate` 會分別指出用於編輯和插入模式的介面。

在本教學課程中，我們將瞭解如何輕鬆地將驗證控制項新增至 TemplateField 的 `EditItemTemplate`，並 `InsertItemTemplate` 以提供更可靠的使用者介面。 具體來說，本教學課程會採用在[檢查與插入、更新和刪除教學課程相關聯的事件](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)中所建立的範例，並增強編輯和插入介面以包含適當的驗證。

## <a name="step-1-replicating-the-example-fromexamining-the-events-associated-with-inserting-updating-and-deletingexamining-the-events-associated-with-inserting-updating-and-deleting-vbmd"></a>步驟1：複寫範例，[以檢查與插入、更新和刪除相關聯的事件](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)

在[檢查與插入、更新和刪除教學課程相關聯的事件中，](examining-the-events-associated-with-inserting-updating-and-deleting-vb.md)我們建立了一個頁面，其中列出了可編輯 GridView 中產品的名稱和價格。 此外，此頁面包含一個 DetailsView，其 `DefaultMode` 屬性設定為 `Insert`，因此一律以插入模式呈現。 在此 DetailsView 中，使用者可以輸入新產品的名稱和價格，按一下 [插入]，並將它新增至系統（請參閱 [圖 1]）。

[![上一個範例可讓使用者新增新的產品，並編輯現有的產品](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image2.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image1.png)

**圖 1**：先前的範例可讓使用者加入新產品並編輯現有的產品（[按一下以觀看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image3.png)）

本教學課程的目標是要加強 DetailsView 和 GridView，以提供驗證控制項。 特別是，我們的驗證邏輯將會：

- 需要在插入或編輯產品時提供名稱
- 必須在插入記錄時提供價格;編輯記錄時，我們仍需要價格，但會使用在 GridView 的 `RowUpdating` 事件處理常式中，在先前的教學課程中已存在的程式設計邏輯。
- 請確定為價格輸入的值是有效的貨幣格式

我們必須先從 `DataModificationEvents.aspx` 頁面將範例複製到本教學課程的頁面，`UIValidation.aspx`，才能查看如何擴充前一個範例以包含驗證。 為了完成這項工作，我們必須同時複製 `DataModificationEvents.aspx` 頁面的宣告式標記和其原始程式碼。 請執行下列步驟，先複製宣告式標記：

1. 在 Visual Studio 中開啟 [`DataModificationEvents.aspx`] 頁面
2. 移至頁面的宣告式標記（按一下頁面底部的 [來源] 按鈕）
3. 複製 `<asp:Content>` 內的文字，並 `</asp:Content>` 標記（第3到44行），如 [圖 2] 所示。

[![複製 &lt;asp： Content&gt; 控制項內的文字](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image5.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image4.png)

**圖 2**：複製 `<asp:Content>` 控制項內的文字（[按一下以查看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image6.png)）

1. 開啟 [`UIValidation.aspx`] 頁面
2. 移至頁面的宣告式標記
3. 貼上 `<asp:Content>` 控制項內的文字。

若要複製原始碼，請開啟 [`DataModificationEvents.aspx.vb`] 頁面，並只複製 `EditInsertDelete_DataModificationEvents` 類別*中*的文字。 複製三個事件處理常式（`Page_Load`、`GridView1_RowUpdating`和 `ObjectDataSource1_Inserting`），但不要**複製類別**宣告。 將複製的文字貼入 `UIValidation.aspx.vb`的 `EditInsertDelete_UIValidation`*類別中。*

將內容和程式碼從 `DataModificationEvents.aspx` 移至 `UIValidation.aspx`之後，請花點時間在瀏覽器中測試您的進度。 您應該會看到相同的輸出，並在這兩個頁面中體驗相同的功能（請參閱 [圖 1]，以取得 `DataModificationEvents.aspx` 動作的螢幕擷取畫面）。

## <a name="step-2-converting-the-boundfields-into-templatefields"></a>步驟2：將 BoundFields 轉換成 TemplateFields

若要將驗證控制項新增至編輯和插入介面，DetailsView 和 GridView 控制項所使用的 BoundFields 必須轉換成 TemplateFields。 若要達成此目的，請分別按一下 GridView 和 DetailsView 的智慧標籤中的 [編輯資料行] 和 [編輯欄位] 連結。 在那裡選取每個 BoundFields，然後按一下 [將此欄位轉換成 TemplateField] 連結。

[![將每個 DetailsView 和 GridView 的 BoundFields 轉換成 TemplateFields](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image8.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image7.png)

**圖 3**：將每個 DetailsView 和 GridView 的 BoundFields 轉換成 TemplateFields （[按一下以觀看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image9.png)）

透過 [欄位] 對話方塊將 BoundField 轉換成 TemplateField 時，會產生 TemplateField，使其呈現與 BoundField 本身相同的唯讀、編輯和插入介面。 下列標記會顯示在 DetailsView 轉換成 TemplateField 後，會將 [`ProductName`] 欄位的宣告式語法：

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample1.aspx)]

請注意，此 TemplateField 會自動建立三個範本 `ItemTemplate`、`EditItemTemplate`和 `InsertItemTemplate`。 `ItemTemplate` 會使用標籤 Web 控制項顯示單一資料欄值（`ProductName`），而 `EditItemTemplate` 和 `InsertItemTemplate` 會在 TextBox Web 控制項中呈現資料欄位值，而該文字方塊會使用雙向資料系結將資料欄位與文字方塊的 `Text` 屬性產生關聯。 因為我們只會在此頁面中使用 DetailsView 進行插入，所以您可以從這兩個 TemplateFields 中移除 `ItemTemplate` 和 `EditItemTemplate`，但不會對其留下傷害。

由於 GridView 不支援 DetailsView 的內建插入功能，因此將 GridView 的 `ProductName` 欄位轉換成 TemplateField 只會產生 `ItemTemplate` 和 `EditItemTemplate`：

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample2.aspx)]

藉由按一下 [將此欄位轉換成 TemplateField]，Visual Studio 已建立 TemplateField，其範本會模擬已轉換之 BoundField 的使用者介面。 您可以透過瀏覽器造訪此頁面來確認這一點。 您會發現 TemplateFields 的外觀和行為與改用 BoundFields 時的體驗相同。

> [!NOTE]
> 您可以視需要自訂範本中的編輯介面。 例如，我們可能會想要將 [`UnitPrice`] TemplateFields 中的文字方塊轉譯成小於 [`ProductName`] 文字方塊的文字方塊。 若要完成此動作，您可以將 TextBox 的 `Columns` 屬性設定為適當的值，或透過 `Width` 屬性提供絕對寬度。 在下一個教學課程中，我們將瞭解如何藉由使用替代資料項目 Web 控制項來取代 TextBox，以完全自訂編輯介面。

## <a name="step-3-adding-the-validation-controls-to-the-gridviewsedititemtemplate-s"></a>步驟3：將驗證控制項新增至 GridView 的`EditItemTemplate` s

在建立資料輸入表單時，使用者必須輸入任何必要的欄位，而且所有提供的輸入都是合法且格式正確的值。 為了協助確保使用者的輸入有效，ASP.NET 提供五個內建的驗證控制項，設計用來驗證單一輸入控制項的值：

- [RequiredFieldValidator](https://msdn.microsoft.com/library/5hbw267h(VS.80).aspx)可確保已提供值
- [CompareValidator](https://msdn.microsoft.com/library/db330ayw(VS.80).aspx)會根據另一個 Web 控制值或常數值來驗證值，或確保值的格式對於指定的資料類型是合法的
- [RangeValidator](https://msdn.microsoft.com/library/f70d09xt.aspx)可確保值在值的範圍內
- [RegularExpressionValidator](https://msdn.microsoft.com/library/eahwtc9e.aspx)會根據[正則運算式](http://en.wikipedia.org/wiki/Regular_expression)來驗證值
- [CustomValidator](https://msdn.microsoft.com/library/9eee01cx(VS.80).aspx)會根據自訂的使用者定義方法來驗證值

如需這五個控制項的詳細資訊，請參閱[ASP.NET 快速入門教學](https://asp.net/QuickStart/aspnet/)課程的[驗證控制項一節](https://quickstarts.asp.net/quickstartv20/aspnet/doc/ctrlref/validation/default.aspx)。

在本教學課程中，我們將需要在 DetailsView 和 GridView 的 `ProductName` TemplateFields 中使用 RequiredFieldValidator，並在 DetailsView 的 `UnitPrice` TemplateField 中使用 RequiredFieldValidator。 此外，我們還需要將 CompareValidator 新增至兩個控制項的 `UnitPrice` TemplateFields，以確保輸入的價格具有大於或等於0的值，且會以有效的貨幣格式呈現。

> [!NOTE]
> 雖然 ASP.NET 1.x 具有這五個相同的驗證控制項，但 ASP.NET 2.0 已新增一些改良功能，主要兩個則是針對 Internet Explorer 以外的瀏覽器提供用戶端腳本支援，而且能夠將頁面上的驗證控制項分割成驗證群組。 如需2.0 中新驗證控制功能的詳細資訊，請參閱[剖析 the ASP.NET 2.0 中的驗證控制項](http://aspnet.4guysfromrolla.com/articles/112305-1.aspx)。

讓我們從將必要的驗證控制項新增至 GridView TemplateFields 中的 `EditItemTemplate` 開始。 若要完成此動作，請按一下 GridView 智慧標籤中的 [編輯範本] 連結，以顯示範本編輯介面。 從這裡，您可以從下拉式清單中選取要編輯的範本。 因為我們想要增強編輯介面，所以我們需要將驗證控制項新增至 `ProductName` 和 `UnitPrice`的 `EditItemTemplate`。

[![我們需要擴充 ProductName 和單價的 EditItemTemplates](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image11.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image10.png)

**圖 4**：我們需要擴充 `ProductName` 和 `UnitPrice`的 `EditItemTemplate` （[按一下以觀看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image12.png)）

在 [`ProductName`] `EditItemTemplate`中，將 RequiredFieldValidator 從 [工具箱] 拖曳至範本編輯介面，並放在文字方塊後面，以新增一個。

[![將 RequiredFieldValidator 新增至 ProductName EditItemTemplate](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image14.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image13.png)

**圖 5**：將 RequiredFieldValidator 新增至 `ProductName` `EditItemTemplate` （[按一下以查看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image15.png)）

所有驗證控制項都可以藉由驗證單一 ASP.NET Web 控制項的輸入來執行。 因此，我們必須指出剛才新增的 RequiredFieldValidator 應該針對 `EditItemTemplate`中的 TextBox 進行驗證;將驗證控制項的[ControlToValidate 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.controltovalidate(VS.80).aspx)設定為適當 Web 控制項的 `ID`，即可完成這項作業。 文字方塊目前有 `TextBox1`的 nondescript `ID`，但讓我們將其變更為更適當的專案。 按一下範本中的文字方塊，然後從 屬性視窗中，將 `ID` 從 `TextBox1` 變更為 `EditProductName`。

[![將文字方塊的識別碼變更為 EditProductName](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image17.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image16.png)

**圖 6**：將文字方塊的 `ID` 變更為 `EditProductName` （[按一下以查看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image18.png)）

接下來，將 RequiredFieldValidator 的 `ControlToValidate` 屬性設定為 `EditProductName`。 最後，將 [ [ErrorMessage] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.errormessage(VS.80).aspx)設為 [您必須提供產品的名稱] 和 [ [Text] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basevalidator.text(VS.80).aspx)設定為 [\*]。 如果有提供 `Text` 屬性值，就是驗證控制項在驗證失敗時所顯示的文字。 ValidationSummary 控制項會使用所需的 `ErrorMessage` 屬性值;如果省略 `Text` 屬性值，則 `ErrorMessage` 屬性值也會是驗證控制項在無效輸入時顯示的文字。

設定 RequiredFieldValidator 的這三個屬性之後，您的畫面看起來應該像 [圖 7]。

[![設定 RequiredFieldValidator 的 ControlToValidate、ErrorMessage 和 Text 屬性](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image20.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image19.png)

**圖 7**：設定 RequiredFieldValidator 的 `ControlToValidate`、`ErrorMessage`和 `Text` 屬性（[按一下以查看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image21.png)）

將 RequiredFieldValidator 新增至 `ProductName` `EditItemTemplate`後，剩下的工作就是將必要的驗證新增至 `UnitPrice` `EditItemTemplate`。 因為我們已決定在編輯記錄時，`UnitPrice` 是選擇性的，所以我們不需要新增 RequiredFieldValidator。 不過，我們需要新增 CompareValidator，以確保 `UnitPrice`（如有提供）會正確地格式化為貨幣且大於或等於0。

將 CompareValidator 新增至 `UnitPrice` `EditItemTemplate`之前，讓我們先將 TextBox Web 控制項的識別碼從 `TextBox2` 變更為 `EditUnitPrice`。 進行這種變更之後，請新增 CompareValidator，將其 `ControlToValidate` 屬性設為 `EditUnitPrice`，其 `ErrorMessage` 屬性設為「價格必須大於或等於零，而且不能包含貨幣符號」和其 `Text` 屬性設為 "\*"。

若要指出 `UnitPrice` 值必須大於或等於0，請將 CompareValidator 的[Operator 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.operator(VS.80).aspx)設為 `GreaterThanEqual`、其[ValueToCompare 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.comparevalidator.valuetocompare(VS.80).aspx)設定為 "0"，並將其[Type 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.basecomparevalidator.type.aspx)設定為 `Currency`。 下列宣告式語法會顯示在進行這些變更之後，`UnitPrice` TemplateField 的 `EditItemTemplate`：

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample3.aspx)]

進行這些變更之後，請在瀏覽器中開啟頁面。 如果您嘗試在編輯產品時省略名稱或輸入不正確價格值，則文字方塊旁會出現星號。 如 [圖 8] 所示，包含貨幣符號（例如 $19.95）的價格值會被視為無效。 CompareValidator 的 `Currency` `Type` 允許數位分隔符號（例如逗號或句號，視文化特性設定而定）和前置加號或負號，但*不允許貨幣*符號。 這種行為可能會 perplex 使用者，因為編輯介面目前使用貨幣格式呈現 `UnitPrice`。

> [!NOTE]
> 回想一下，在*與插入、更新和刪除教學課程相關聯的事件*中，我們將 BoundField 的 `DataFormatString` 屬性設定為 `{0:c}`，以便將它格式化為貨幣。 此外，我們會將 [`ApplyFormatInEditMode`] 屬性設為 [true]，使 GridView 的編輯介面將 `UnitPrice` 格式化為貨幣。 將 BoundField 轉換成 TemplateField 時，Visual Studio 記下這些設定，並使用資料系結語法 `<%# Bind("UnitPrice", "{0:c}") %>`，將 TextBox 的 `Text` 屬性格式化為貨幣。

[![星號會出現在具有無效輸入的文字方塊旁邊](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image23.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image22.png)

**圖 8**：具有無效輸入的文字方塊旁邊會出現星號（[按一下以觀看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image24.png)）

雖然驗證的運作方式不盡相同，但在編輯記錄時，使用者必須手動移除貨幣符號，這是無法接受的。 若要解決此問題，我們有三個選項：

1. 設定 `EditItemTemplate`，讓 `UnitPrice` 值不會格式化為貨幣。
2. 允許使用者藉由移除 CompareValidator，並將其取代為正確檢查正確格式貨幣值的 RegularExpressionValidator，來輸入貨幣符號。 這裡的問題在於，驗證貨幣值的正則運算式並不是很棒，如果我們想要納入文化特性設定，則需要撰寫程式碼。
3. 完全移除驗證控制項，並依賴 GridView 的 `RowUpdating` 事件處理常式中的伺服器端驗證邏輯。

讓我們在此練習中使用選項 #1。 由於 `EditItemTemplate`： `<%# Bind("UnitPrice", "{0:c}") %>`中 TextBox 的資料系結運算式，因此目前 `UnitPrice` 會格式化為貨幣。 將 Bind 語句變更為 `Bind("UnitPrice", "{0:n2}")`，將結果格式化為具有兩位數精確度的數位。 這可以直接透過宣告式語法來完成，或從 `UnitPrice` TemplateField 的 `EditItemTemplate` 中的 [`EditUnitPrice`] 文字方塊中按一下 [編輯資料系結] 連結（請參閱 [圖 9] 和 [10]）。

[![按一下文字方塊的 [編輯系結] 連結](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image26.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image25.png)

**圖 9**：按一下文字方塊的 [編輯系結] 連結（[按一下以查看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image27.png)）

[![在 Bind 語句中指定格式規範](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image29.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image28.png)

**圖 10**：在 `Bind` 語句中指定格式規範（[按一下以查看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image30.png)）

透過這項變更，編輯介面中的格式化價格包括逗號做為群組分隔符號，並將句點當做小數分隔符號，但會保留貨幣符號。

> [!NOTE]
> `UnitPrice` `EditItemTemplate` 不包含 RequiredFieldValidator，允許回傳至控制發生和更新邏輯開始。 不過，從*檢查與插入、更新和刪除*教學課程關聯的事件中複製的 `RowUpdating` 事件處理常式，包含可確保已提供 `UnitPrice` 的程式設計檢查。 請隨意移除此邏輯，將其保持原狀，或將 RequiredFieldValidator 新增至 `UnitPrice` `EditItemTemplate`。

## <a name="step-4-summarizing-data-entry-problems"></a>步驟4：摘要資料輸入問題

除了五個驗證控制項以外，ASP.NET 還包含[ValidationSummary 控制項](https://msdn.microsoft.com/library/f9h59855(VS.80).aspx)，它會顯示偵測到無效資料之驗證控制項的 `ErrorMessage`。 此摘要資料可顯示為網頁上的文字，或透過強制回應的用戶端 messagebox。 讓我們增強此教學課程，以包含用戶端 messagebox，其中摘要說明任何驗證問題。

若要完成此動作，請將 ValidationSummary 控制項從 [工具箱] 拖曳至設計工具。 驗證控制項的位置並不重要，因為我們要將它設定為只將摘要顯示為 messagebox。 加入控制項之後，將其[ShowSummary 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showsummary(VS.80).aspx)設為 `False`，並將其[ShowMessageBox 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.validationsummary.showmessagebox(VS.80).aspx)設定為 `True`。 透過這項新增功能，任何驗證錯誤都會在用戶端 messagebox 中匯總。

[在用戶端 Messagebox 中，會摘要說明驗證錯誤 ![](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image32.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image31.png)

**圖 11**：驗證錯誤會在用戶端 Messagebox 中匯總（[按一下以觀看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image33.png)）

## <a name="step-5-adding-the-validation-controls-to-the-detailsviewsinsertitemtemplate"></a>步驟5：將驗證控制項新增至 DetailsView 的`InsertItemTemplate`

本教學課程剩下的工作，就是將驗證控制項新增至 DetailsView 的插入介面。 將驗證控制項新增至 DetailsView 範本的程式，與步驟3中所檢查的程式相同。因此，我們將在此步驟中輕鬆完成這項工作。 如同我們對 GridView 的 `EditItemTemplate`，建議您將 nondescript `TextBox1` 的文字方塊 `ID` 重新命名，並 `TextBox2` `InsertProductName` 和 `InsertUnitPrice`。

將 RequiredFieldValidator 新增至 `ProductName` `InsertItemTemplate`。 將 [`ControlToValidate`] 設定為範本中文字方塊的 `ID`，其 `Text` 屬性設為 "\*"，而其 `ErrorMessage` 屬性設為 [您必須提供產品的名稱]。

由於新增記錄時，此頁面需要 `UnitPrice`，因此，請將 RequiredFieldValidator 新增至 `UnitPrice` `InsertItemTemplate`，適當地設定其 `ControlToValidate`、`Text`和 `ErrorMessage` 屬性。 最後，將 CompareValidator 新增至 `UnitPrice` `InsertItemTemplate`，並設定其 `ControlToValidate`、`Text`、`ErrorMessage`、`Type`、`Operator`和 `ValueToCompare` 屬性，就像我們在 GridView `UnitPrice`中 `EditItemTemplate`的 CompareValidator 一樣。

加入這些驗證控制項之後，如果未提供新產品的名稱，或其價格為負數或格式不合法，則無法將其新增至系統。

[已將 ![驗證邏輯新增至 DetailsView 的插入介面](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image35.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image34.png)

**圖 12**：驗證邏輯已新增至 DetailsView 的插入介面（[按一下以觀看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image36.png)）

## <a name="step-6-partitioning-the-validation-controls-into-validation-groups"></a>步驟6：將驗證控制項分割成驗證群組

我們的頁面是由兩個邏輯上不同的驗證控制項集所組成：對應至 GridView 的編輯介面，以及對應至 DetailsView 插入介面的設定。 根據預設，當回傳時，會檢查頁面上的*所有*驗證控制項。 不過，在編輯記錄時，我們不希望 DetailsView 的插入介面驗證控制項進行驗證。 [圖 13] 說明當使用者使用完全合法的值來編輯產品時，我們目前的難題，按一下 [更新] 會導致驗證錯誤，因為插入介面中的名稱和價格值是空白的。

[更新產品 ![會導致插入介面的驗證控制項引發](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image38.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image37.png)

**圖 13**：更新產品會引發插入介面的驗證控制項（[按一下以查看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image39.png)）

ASP.NET 2.0 中的驗證控制項可以透過其 `ValidationGroup` 屬性分割成驗證群組。 若要關聯群組中的一組驗證控制項，只要將其 `ValidationGroup` 屬性設為相同的值即可。 在本教學課程中，將 GridView TemplateFields 中驗證控制項的 `ValidationGroup` 屬性設為 `EditValidationControls`，並將 DetailsView TemplateFields 的 `ValidationGroup` 屬性設定為 `InsertValidationControls`。 當您使用設計工具的編輯範本介面時，可以直接在宣告式標記中或透過屬性視窗來完成這些變更。

除了驗證控制項以外，ASP.NET 2.0 中的按鈕和按鈕相關控制項也包含 `ValidationGroup` 屬性。 只有當回傳是由具有相同 `ValidationGroup` 屬性設定的按鈕所引發時，才會檢查驗證群組的驗證程式是否有效。 例如，為了讓 DetailsView 的 [插入] 按鈕觸發 `InsertValidationControls` 驗證群組，我們必須將 CommandField 的 `ValidationGroup` 屬性設定為 [`InsertValidationControls`] （請參閱 [圖 14]）。 此外，將 GridView 的 [CommandField's `ValidationGroup`] 屬性設定為 [`EditValidationControls`]。

[![將 DetailsView 的 CommandField's ValidationGroup 屬性設定為 InsertValidationControls](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image41.png)](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image40.png)

**圖 14**：將 DetailsView 的 CommandField's `ValidationGroup` 屬性設定為 `InsertValidationControls` （[按一下以查看完整大小的影像](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/_static/image42.png)）

這些變更之後，DetailsView 和 GridView 的 TemplateFields 和 CommandFields 看起來應該如下所示：

DetailsView 的 TemplateFields 和 CommandField

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample4.aspx)]

GridView 的 CommandField 和 TemplateFields

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample5.aspx)]

此時，只有在按下 GridView 的 [插入] 按鈕時才會引發編輯特定的驗證控制項，而插入特定的驗證控制項則只會在按一下 DetailsView 的 [插入] 按鈕時引發，以解決 [圖 13] 中反白顯示的問題。 不過，在此變更中，當輸入不正確資料時，不會再顯示 ValidationSummary 控制項。 ValidationSummary 控制項也包含 `ValidationGroup` 屬性，而且只會在其驗證群組中顯示這些驗證控制項的摘要資訊。 因此，我們在此頁面中必須有兩個驗證控制項，一個用於 `InsertValidationControls` 驗證群組，另一個用於 `EditValidationControls`。

[!code-aspx[Main](adding-validation-controls-to-the-editing-and-inserting-interfaces-vb/samples/sample6.aspx)]

完成此新增教學課程後，

## <a name="summary"></a>總結

雖然 BoundFields 可以同時提供插入和編輯介面，但介面無法自訂。 通常，我們會想要將驗證控制項新增至編輯和插入介面，以確保使用者以合法格式輸入必要的輸入。 若要完成此動作，我們必須將 BoundFields 轉換成 TemplateFields，並將驗證控制項新增至適當的範本。 在本教學課程中，我們將從*檢查與插入、更新和刪除教學課程相關聯的事件*中擴充範例，並將驗證控制項新增至 DetailsView 的插入介面和 GridView 的編輯介面。 此外，我們也看到了如何使用 ValidationSummary 控制項顯示摘要驗證資訊，以及如何將頁面上的驗證控制項分割成不同的驗證群組。

如我們在本教學課程中所見，TemplateFields 允許增強編輯和插入介面，以包含驗證控制項。 TemplateFields 也可以擴充以包含額外的輸入 Web 控制項，讓文字方塊能夠由更適合的 Web 控制項取代。 在下一個教學課程中，我們將瞭解如何使用資料系結 DropDownList 控制項來取代 TextBox 控制項，這在編輯外鍵（例如 `Products` 資料表中的 `CategoryID` 或 `SupplierID`）時是理想的選擇。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的潛在客戶審核者為 Liz Shulok 和 Zack。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](handling-bll-and-dal-level-exceptions-in-an-asp-net-page-vb.md)
> [下一頁](customizing-the-data-modification-interface-vb.md)
