---
uid: web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
title: 在 DetailsView 控制項中使用 TemplateFields （VB） |Microsoft Docs
author: rick-anderson
description: 與 GridView 搭配使用的相同 TemplateFields 功能也適用于 DetailsView 控制項。 在本教學課程中，我們將顯示一項產品 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: 0b91d5f8-127d-4f6a-b204-f2e2b35ef703
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/using-templatefields-in-the-detailsview-control-vb
msc.type: authoredcontent
ms.openlocfilehash: e96f954c27ae1c8ccc18a9c40fe7e541b487c1cc
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74624819"
---
# <a name="using-templatefields-in-the-detailsview-control-vb"></a>在 DetailsView 控制項中使用 TemplateFields (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_13_VB.exe)或[下載 PDF](using-templatefields-in-the-detailsview-control-vb/_static/datatutorial13vb1.pdf)

> 與 GridView 搭配使用的相同 TemplateFields 功能也適用于 DetailsView 控制項。 在本教學課程中，我們將使用包含 TemplateFields 的 DetailsView，一次顯示一項產品。

## <a name="introduction"></a>簡介

TemplateField 比 BoundField、CheckBoxField、HyperLinkField 和其他資料欄位控制項，提供更高的彈性來呈現資料。 在[上一個教學](using-templatefields-in-the-gridview-control-vb.md)課程中，我們探討了如何使用 GridView 中的 TemplateField 來執行下列動作：

- 在一個資料行中顯示多個資料欄值。 具體而言，`FirstName` 和 `LastName` 欄位都已結合成一個 GridView 資料行。
- 使用替代的 Web 控制項來表示資料欄位值。 我們已瞭解如何使用行事曆控制項顯示 `HiredDate` 值。
- 根據基礎資料顯示狀態資訊。 雖然 `Employees` 資料表未包含傳回員工在工作上的天數的資料行，但我們可以在上一個教學課程中使用 TemplateField 和格式化方法來顯示這類資訊。

與 GridView 搭配使用的相同 TemplateFields 功能也適用于 DetailsView 控制項。 在本教學課程中，我們將使用包含兩個 TemplateFields 的 DetailsView，一次顯示一項產品。 第一個 TemplateField 會將 `UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` 資料欄位結合成一列 DetailsView。 第二個 TemplateField 將會顯示 [`Discontinued`] 欄位的值，但如果 `Discontinued` `True`，則會使用格式化方法來顯示 [是]，否則會使用 [否]。

[![兩個 TemplateFields 用於自訂顯示](using-templatefields-in-the-detailsview-control-vb/_static/image2.png)](using-templatefields-in-the-detailsview-control-vb/_static/image1.png)

**圖 1**：兩個 TemplateFields 用於自訂顯示（[按一下以觀看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image3.png)）

讓我們開始吧！

## <a name="step-1-binding-the-data-to-the-detailsview"></a>步驟1：將資料系結至 DetailsView

如前一個教學課程中所討論，使用 TemplateFields 時，最簡單的方法是先建立 DetailsView 控制項，其中只包含 BoundFields，然後再新增 TemplateFields 或將現有的 BoundFields 轉換成 TemplateFields （視需要）. 因此，請啟動本教學課程，方法是透過設計工具將 DetailsView 新增至頁面，並將它系結至會傳回產品清單的 ObjectDataSource。 這些步驟會針對每個產品的非布林值欄位，以及一個布林值欄位（已停用）的 CheckBoxField，建立具有 BoundFields 的 DetailsView。

開啟 [`DetailsViewTemplateField.aspx`] 頁面，並從 [工具箱] 將 [DetailsView] 拖曳至設計工具。 從 DetailsView 的智慧標籤加入宣告新的 ObjectDataSource 控制項，叫用 `ProductsBLL` 類別的 `GetProducts()` 方法。

[![加入新的 ObjectDataSource 控制項來叫用 GetProducts （）方法](using-templatefields-in-the-detailsview-control-vb/_static/image5.png)](using-templatefields-in-the-detailsview-control-vb/_static/image4.png)

**圖 2**：加入新的 ObjectDataSource 控制項來叫用 `GetProducts()` 方法（[按一下以查看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image6.png)）

針對此報表，請移除 `ProductID`、`SupplierID`、`CategoryID`和 `ReorderLevel` BoundFields。 接下來，重新排序 BoundFields，讓 [`CategoryName`] 和 [`SupplierName` BoundFields] 立即出現在 `ProductName` BoundField 之後。 您可以視需要調整 BoundFields 的 `HeaderText` 屬性和格式屬性。 就像 GridView 一樣，這些 BoundField 層級的編輯都可以透過 [欄位] 對話方塊來執行（按一下 DetailsView 的智慧標籤中的 [編輯欄位] 連結即可存取），或透過宣告式語法。 最後，清除 DetailsView 的 `Height` 並 `Width` 屬性值，以允許 DetailsView 控制項根據顯示的資料進行擴充，並勾選智慧標籤中的 [啟用分頁] 核取方塊。

進行這些變更之後，您的 DetailsView 控制項的宣告式標記看起來應該如下所示：

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample1.aspx)]

請花點時間透過瀏覽器觀看頁面。 此時，您應該會看到列出的單一產品（Chai），其中的資料列會顯示產品的名稱、類別、供應商、價格、庫存單位、依訂單的單位，以及已停止的狀態。

[![使用一系列的 BoundFields 來顯示產品的詳細資料](using-templatefields-in-the-detailsview-control-vb/_static/image8.png)](using-templatefields-in-the-detailsview-control-vb/_static/image7.png)

**圖 3**：產品的詳細資料會以一系列的 BoundFields 顯示（[按一下以觀看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image9.png)）

## <a name="step-2-combining-the-price-units-in-stock-and-units-on-order-into-one-row"></a>步驟2：將價格、庫存單位和單位按序結合成一個資料列

DetailsView 有一個資料列，用於 `UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` 欄位。 我們可以藉由加入新的 TemplateField，或將其中一個現有的 `UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` BoundFields 轉換成 TemplateField，將這些資料欄位結合成一個包含 TemplateField 的資料列。 雖然我個人偏好轉換現有的 BoundFields，我們還是要藉由加入新的 TemplateField 來練習。

首先，按一下 DetailsView 智慧標籤中的 [編輯欄位] 連結，以顯示 [欄位] 對話方塊。 接下來，新增 TemplateField，並將其 [`HeaderText`] 屬性設為 [價格和庫存]，然後移動新的 TemplateField，使其位於 [`UnitPrice`] BoundField 上方。

[![將新的 TemplateField 新增至 DetailsView 控制項](using-templatefields-in-the-detailsview-control-vb/_static/image11.png)](using-templatefields-in-the-detailsview-control-vb/_static/image10.png)

**圖 4**：將新的 TemplateField 新增至 DetailsView 控制項（[按一下以查看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image12.png)）

由於這個新的 TemplateField 將包含目前顯示在 `UnitPrice`、`UnitsInStock`和 `UnitsOnOrder` BoundFields 中的值，讓我們將它們移除。

此步驟的最後一項工作是定義價格和庫存 TemplateField 的 `ItemTemplate` 標記，這可以透過設計工具中的 DetailsView 範本編輯介面，或透過控制項的宣告式語法來完成。 如同 GridView，您可以按一下智慧標籤中的 [編輯範本] 連結來存取 DetailsView 的範本編輯介面。 從這裡，您可以從下拉式清單中選取要編輯的範本，然後從 [工具箱] 加入任何 Web 控制項。

在本教學課程中，請從將標籤控制項新增至價格和清查 TemplateField 的 `ItemTemplate`開始。 接下來，按一下標籤 Web 控制項的智慧標籤中的 [編輯系結] 連結，並將 [`Text`] 屬性系結至 [`UnitPrice`] 欄位。

[![將標籤的 Text 屬性系結至 [單價] 資料欄位](using-templatefields-in-the-detailsview-control-vb/_static/image14.png)](using-templatefields-in-the-detailsview-control-vb/_static/image13.png)

**圖 5**：將標籤的 [`Text`] 屬性系結至 [`UnitPrice` 資料] 欄位（[按一下以查看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image15.png)）

## <a name="formatting-the-price-as-a-currency"></a>將價格格式化為貨幣

透過這種新增，[Web 控制項價格] 和 [清查 TemplateField] 標籤現在只會顯示所選產品的價格。 [圖 6] 顯示透過瀏覽器觀看時，到目前為止的進度螢幕擷取畫面。

[![[價格與清查] TemplateField 顯示價格](using-templatefields-in-the-detailsview-control-vb/_static/image17.png)](using-templatefields-in-the-detailsview-control-vb/_static/image16.png)

**圖 6**： [價格] 和 [清查] TemplateField 會顯示價格（[按一下以查看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image18.png)）

請注意，產品的價格不會格式化為貨幣。 透過 BoundField，您可以將 `HtmlEncode` 屬性設為 `False`，並將 `DataFormatString` 屬性設定為 `{0:formatSpecifier}`來進行格式化。 不過，針對 TemplateField，必須在資料系結語法中指定任何格式設定指示，或使用在應用程式代碼中某處定義的格式化方法（例如在 ASP.NET 網頁的程式碼後置類別中）。

若要指定標籤 Web 控制項中所使用之資料系結語法的格式，請從標籤的智慧標籤按一下 [編輯資料系結] 連結，以返回 [資料系結] 對話方塊。 您可以直接在 [格式] 下拉式清單中輸入格式指示，或選取其中一個已定義的格式字串。 就像 BoundField 的 `DataFormatString` 屬性一樣，會使用 `{0:formatSpecifier}`來指定格式。

針對 [`UnitPrice`] 欄位，請選取適當的下拉式清單值，或手動輸入 `{0:C}`，以使用指定的貨幣格式。

[![將價格格式化為貨幣](using-templatefields-in-the-detailsview-control-vb/_static/image20.png)](using-templatefields-in-the-detailsview-control-vb/_static/image19.png)

**圖 7**：將價格格式化為貨幣（[按一下以觀看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image21.png)）

以宣告的方式，格式設定規格會表示為 `Bind` 或 `Eval` 方法中的第二個參數。 剛才透過設計工具所做的設定會導致宣告式標記中的下列資料系結運算式：

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample2.aspx)]

## <a name="adding-the-remaining-data-fields-to-the-templatefield"></a>將剩餘的資料欄位加入至 TemplateField

此時，我們已在 [價格與庫存] TemplateField 中顯示並格式化 `UnitPrice` 資料欄位，但仍然需要顯示 [`UnitsInStock`] 和 [`UnitsOnOrder`] 欄位。 讓我們在價格和括弧下方的一行顯示這些資訊。 從設計工具中的範本編輯介面，可以藉由將游標放在範本內，並直接在要顯示的文字中輸入，來加入這類標記。 或者，您也可以直接在宣告式語法中輸入這個標記。

新增靜態標記、標記 Web 控制項和資料系結語法，讓價格和清查 TemplateField 顯示價格和清查資訊，如下所示：

*UnitPrice*  
（依**庫存/訂單：**  / *UnitsOnOrder*的*庫存*量）

執行此工作之後，DetailsView 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample3.aspx)]

隨著這些變更，我們已將價格和清查資訊合併成單一 DetailsView 資料列。

[![價格和清查資訊會顯示在單一資料列中](using-templatefields-in-the-detailsview-control-vb/_static/image23.png)](using-templatefields-in-the-detailsview-control-vb/_static/image22.png)

**圖 8**：價格和清查資訊會顯示在單一資料列中（[按一下以查看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image24.png)）

## <a name="step-3-customizing-the-discontinued-field-information"></a>步驟3：自訂已停止的欄位資訊

`Products` 資料表的 `Discontinued` 資料行是表示產品是否已中止的位值。 將 DetailsView （或 GridView）系結至資料來源控制項時，布林值欄位（例如 `Discontinued`）會實作為 CheckBoxFields，而非布林值欄位（例如 `ProductID`、`ProductName`等等）會實作為 BoundFields。 如果資料欄位的值為 True 且未核取，則 CheckBoxField 會轉譯為停用的核取方塊。

而不是顯示 CheckBoxField，我們可能會想要改為顯示文字，指出產品是否已停止。 若要完成此作業，我們可以從 DetailsView 中移除 CheckBoxField，然後新增其 `DataField` 屬性設為 `Discontinued`的 BoundField。 請花點時間執行此動作。 在此變更之後，DetailsView 會針對已停止的產品顯示 "True" 文字，並針對仍在使用中的產品顯示 "False"。

[![字串 True 和 False 用來顯示已停止狀態](using-templatefields-in-the-detailsview-control-vb/_static/image26.png)](using-templatefields-in-the-detailsview-control-vb/_static/image25.png)

**圖 9**：用來顯示已停止狀態的字串 True 和 False （[按一下以觀看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image27.png)）

想像一下，我們不想要使用字串 "True" 或 "False"，而是改為 "YES" 和 "NO"。 這類自訂可以透過 TemplateField 和格式化方法的協助來執行。 格式化方法可以接受任意數目的輸入參數，但必須傳回要插入範本的 HTML （以字串表示）。

將格式化方法新增至名為 `DisplayDiscontinuedAsYESorNO` 的 `DetailsViewTemplateField.aspx` 頁面程式碼後置類別，接受 `Northwind.ProductsRow` 物件做為輸入參數，並傳回字串。 如前一個教學課程中所討論，這個方法*必須*標示為 `Protected` 或 `Public`，才能從範本存取。

[!code-vb[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample4.vb)]

這個方法會檢查輸入參數（`discontinued`），如果 `True`則傳回 "YES"，否則傳回 "NO"。

> [!NOTE]
> 在上一個教學課程中所檢查的格式化方法中，您應該記得我們傳入的資料欄位可能包含 `NULL` s，因此必須先檢查員工的 `HiredDate` 屬性值是否有資料庫 `NULL` 值，再存取 `EmployeesRow`的 `HiredDate` 屬性。 這裡不需要這樣的檢查，因為 `Discontinued` 資料行永遠不會指派資料庫 `NULL` 值。 此外，這也是為什麼方法可以接受布林值輸入參數，而不是必須接受 `ProductsRow` 實例或 `Object`型別參數的原因。

完成這個格式化方法之後，剩下的就是從 TemplateField 的 `ItemTemplate`呼叫它。 若要建立 TemplateField，請移除 `Discontinued` BoundField 並加入新的 TemplateField，或將 `Discontinued` BoundField 轉換成 TemplateField。 然後，從宣告式標記視圖中編輯 TemplateField，使其只包含會叫用 `DisplayDiscontinuedAsYESorNO` 方法的 ItemTemplate，傳入目前 `ProductRow` 實例 `Discontinued` 屬性的值。 這可以透過 `Eval` 方法來存取。 具體來說，TemplateField 的標記看起來應該像這樣：

[!code-aspx[Main](using-templatefields-in-the-detailsview-control-vb/samples/sample5.aspx)]

這會導致在轉譯 DetailsView 時叫用 `DisplayDiscontinuedAsYESorNO` 方法，傳入 `ProductRow` 實例的 `Discontinued` 值。 由於 `Eval` 方法會傳回 `Object`類型的值，但 `DisplayDiscontinuedAsYESorNO` 方法需要 `Boolean`類型的輸入參數，因此我們會將 `Eval` 方法的傳回值轉換成 `Boolean`。 根據所接收的值，`DisplayDiscontinuedAsYESorNO` 方法會傳回「是」或「否」。 傳回的值就是在此 DetailsView 資料列中顯示的內容（請參閱 [圖 10]）。

[![是，或目前沒有任何值顯示在已停止的資料列中](using-templatefields-in-the-detailsview-control-vb/_static/image29.png)](using-templatefields-in-the-detailsview-control-vb/_static/image28.png)

**圖 10**： [是] 或目前沒有任何值顯示在已停止的資料列中（[按一下以查看完整大小的影像](using-templatefields-in-the-detailsview-control-vb/_static/image30.png)）

## <a name="summary"></a>總結

DetailsView 控制項中的 TemplateField 允許比其他欄位控制項提供更高的彈性來顯示資料，而且適用于下列情況：

- 多個資料欄位必須顯示在一個 GridView 資料行中
- 資料最適合使用 Web 控制項而非純文字來表示
- 輸出取決於基礎資料，例如顯示中繼資料或重新格式化資料

雖然 TemplateFields 允許在轉譯 DetailsView 的基礎資料時有更大的彈性，但 DetailsView 輸出仍然會覺得有點 boxy，因為每個欄位都會轉譯為 HTML `<table>`中的資料列。

FormView 控制項在設定轉譯的輸出時，提供更大的彈性。 FormView 不會包含欄位，而是只有一系列的範本（`ItemTemplate`、`EditItemTemplate`、`HeaderTemplate`等等）。 我們將在下一個教學課程中瞭解如何使用 FormView 來達到轉譯版面配置的更大控制權。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Dan Jagers。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](using-templatefields-in-the-gridview-control-vb.md)
> [下一頁](using-the-formview-s-templates-vb.md)
