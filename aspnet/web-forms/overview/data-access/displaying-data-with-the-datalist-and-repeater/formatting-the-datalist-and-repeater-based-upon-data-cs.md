---
uid: web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
title: 根據資料格式化 DataList 和中繼器（C#） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將逐步解說範例，說明如何使用格式化函數搭配 ... 來格式化 DataList 和中繼器控制項的外觀。
ms.author: riande
ms.date: 09/13/2006
ms.assetid: 83e3d759-82b8-41e6-8d62-f0f4b3edec41
msc.legacyurl: /web-forms/overview/data-access/displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs
msc.type: authoredcontent
ms.openlocfilehash: 68de3450ed97fc7bd0efb27e089d9db8e3e85fb0
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74633303"
---
# <a name="formatting-the-datalist-and-repeater-based-upon-data-c"></a>根據資料格式化 DataList 和重複項 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_30_CS.exe)或[下載 PDF](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/datatutorial30cs1.pdf)

> 在本教學課程中，我們將逐步解說範例，說明如何使用範本內的格式函數或藉由處理資料系結事件，來格式化 DataList 和中繼器控制項的外觀。

## <a name="introduction"></a>簡介

如我們在先前的教學課程中所見，DataList 提供一些會影響其外觀的樣式相關屬性。 特別是，我們已瞭解如何將預設 CSS 類別指派給 DataList s `HeaderStyle`、`ItemStyle`、`AlternatingItemStyle`和 `SelectedItemStyle` 屬性。 除了這四個屬性以外，DataList 還包含一些其他樣式相關的屬性，例如 `Font`、`ForeColor`、`BackColor`和 `BorderWidth`等等。 中繼器控制項不包含任何與樣式相關的屬性。 任何這類樣式設定都必須直接在「中繼器」範本的標記內進行。

不過，通常資料的格式化方式取決於資料本身。 例如，當列出產品時，我們可能會想要以淺灰色字型色彩來顯示產品資訊（如果已停用），或者，如果是零，我們可能會想要反白顯示 `UnitsInStock` 值。 如我們在先前的教學課程中所見，GridView、DetailsView 和 FormView 提供兩種不同的方式，根據其資料來格式化其外觀：

- **`DataBound` 事件**會為適當的 `DataBound` 事件建立事件處理常式，這會在資料系結至每個專案（針對 GridView 是 `RowDataBound` 事件時引發），而 DataList 和中繼器則是 `ItemDataBound` 事件）。 在該事件處理常式中，可以檢查剛系結的資料，並進行格式設定決策。 我們已在[根據資料的自訂格式](../custom-formatting/custom-formatting-based-upon-data-cs.md)教學課程中檢查這項技術。
- 使用 DetailsView 或 GridView 控制項中的 TemplateFields 或在 FormView 控制項中使用範本時，在**範本中格式化**函式，我們可以將格式化函式新增至 ASP.NET 網頁的程式碼後置類別、商務邏輯層，或可從 web 應用程式存取的任何其他類別庫。 此格式化功能可以接受任意數目的輸入參數，但必須傳回 HTML 以在範本中轉譯。 在 GridView 控制項教學課程中，[使用 TemplateFields](../custom-formatting/using-templatefields-in-the-gridview-control-cs.md)先檢查格式函數。

這兩種格式化技術都可透過 DataList 和中繼器控制項來使用。 在本教學課程中，我們將逐步解說針對這兩個控制項使用這兩種技術的範例。

## <a name="using-theitemdataboundevent-handler"></a>使用`ItemDataBound`事件處理常式

當資料系結至 DataList 時（從資料來源控制項，或透過程式設計方式將資料指派給控制項 `DataSource` 屬性並呼叫其 `DataBind()` 方法），會引發 DataList s `DataBinding` 事件、列舉的資料來源，而且每個資料記錄都會系結至 DataList。 對於資料來源中的每筆記錄，DataList 會建立一個[`DataListItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.aspx)物件，然後系結至目前的記錄。 在此過程中，DataList 會引發兩個事件：

- 建立 `DataListItem` 之後， **`ItemCreated`** 引發
- 當目前的記錄已系結至 `DataListItem` 之後， **`ItemDataBound`** 引發

下列步驟概述 DataList 控制項的資料系結程式。

1. DataList s [`DataBinding` 事件](https://msdn.microsoft.com/library/system.web.ui.control.databinding.aspx)會引發
2. 資料會系結至 DataList  
  
   針對資料來源中的每筆記錄 

    1. 建立 `DataListItem` 物件
    2. 引發[`ItemCreated` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemcreated.aspx)
    3. 將記錄系結至 `DataListItem`
    4. 引發[`ItemDataBound` 事件](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalist.itemdatabound.aspx)
    5. 將 `DataListItem` 新增至 `Items` 集合

當您將資料系結至中繼器控制項時，它會經歷完全相同的步驟順序。 唯一的差別在於，重複項會使用[`RepeaterItem`](https://msdn.microsoft.com/library/system.web.ui.webcontrols.repeateritem(VS.80).aspx)s，而不是建立 `DataListItem` 實例。

> [!NOTE]
> 精明讀取器可能已注意到當 DataList 和中繼器系結至資料時，與 GridView 系結至資料時，所發生的一系列步驟稍有異常。 在資料系結程式的結尾處，GridView 會引發 `DataBound` 事件;不過，DataList 和中繼器控制項都不會有這類事件。 這是因為在前置和後置層級事件處理常式模式變得很常見之前，會在 ASP.NET 1.x 的時間範圍內重新建立 DataList 和中繼器控制項。

就像 GridView 一樣，根據資料進行格式化的一個選項是建立 `ItemDataBound` 事件的事件處理常式。 這個事件處理常式會檢查剛剛系結至 `DataListItem` 或 `RepeaterItem` 的資料，並視需要影響控制項的格式。

對於 DataList 控制項，可以使用 `DataListItem` 的樣式相關屬性（包括標準 `Font`、`ForeColor`、`BackColor`、`CssClass`等等）來執行整個專案的格式化變更。 為了影響 DataList s 範本內特定 Web 控制項的格式，我們需要以程式設計方式存取和修改這些 Web 控制項的樣式。 我們已瞭解如何在*根據資料的自訂格式*教學課程中完成這項工作。 如同重複項控制項，`RepeaterItem` 類別沒有與樣式相關的屬性;因此，在 `ItemDataBound` 事件處理常式中對 `RepeaterItem` 所做的所有樣式相關變更，都必須藉由以程式設計方式存取及更新範本內的 Web 控制項來完成。

由於 DataList 和中繼器的 `ItemDataBound` 格式化技巧幾乎完全相同，我們的範例將著重在使用 DataList。

## <a name="step-1-displaying-product-information-in-the-datalist"></a>步驟1：在 DataList 中顯示產品資訊

在我們擔心格式化之前，先建立一個使用 DataList 來顯示產品資訊的頁面。 在[上一個教學](displaying-data-with-the-datalist-and-repeater-controls-cs.md)課程中，我們建立了一個 DataList，其 `ItemTemplate` 顯示每個產品的名稱、類別、供應商、每個單位的數量和價格。 讓我們在本教學課程中重複此功能。 若要完成這項操作，您可以從頭開始重新建立 DataList 和其 ObjectDataSource，也可以從上一個教學課程中建立的頁面（`Basics.aspx`）複製這些控制項，然後將它們貼入本教學課程的頁面（`Formatting.aspx`）。

將 DataList 和 ObjectDataSource 功能從 `Basics.aspx` 複寫到 `Formatting.aspx`之後，請花點時間將 DataList s `ID` 屬性從 `DataList1` 變更為更具描述性的 `ItemDataBoundFormattingExample`。 接下來，在瀏覽器中查看 DataList。 如 [圖 1] 所示，每個產品的唯一格式差異在於背景色彩會替代。

[![在 DataList 控制項中列出產品](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image2.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image1.png)

**圖 1**：產品會列在 DataList 控制項中（[按一下以查看完整大小的影像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image3.png)）

在本教學課程中，讓我們格式化 DataList，使價格小於 $20.00 的任何產品都以黃色反白顯示其名稱和單價。

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-itemdatabound-event-handler"></a>步驟2：以程式設計方式判斷 ItemDataBound 事件處理常式中的資料值

因為只有價格低於 $20.00 的產品會套用自訂格式，所以我們必須能夠判斷每個產品的價格。 將資料系結至 DataList 時，DataList 會列舉其資料來源中的記錄，而針對每一筆記錄，會建立一個 `DataListItem` 實例，將資料來源記錄系結至 `DataListItem`。 將特定記錄的資料系結至目前的 `DataListItem` 物件之後，會引發 DataList s `ItemDataBound` 事件。 我們可以為這個事件建立事件處理常式，以檢查目前 `DataListItem` 的資料值，並根據這些值，進行任何必要的格式變更。

建立 DataList 的 `ItemDataBound` 事件，並新增下列程式碼：

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample1.cs)]

雖然 DataList s `ItemDataBound` 事件處理常式背後的概念和語義與 GridView 的 `RowDataBound` 事件處理常式所使用的不同，在*自訂的格式設定根據資料*教學課程中，語法稍有不同。 當 `ItemDataBound` 事件引發時，只系結至資料的 `DataListItem` 會透過 `e.Item` （而不是 `e.Row`，如同 GridView 的 `RowDataBound` 事件處理常式）傳遞至對應的事件處理常式。 DataList s `ItemDataBound` 事件處理常式會針對加入 DataList 中的*每個*資料列而引發，包括標題列、頁尾資料列和分隔資料列。 不過，產品資訊只會系結至資料列。 因此，當您使用 `ItemDataBound` 事件來檢查系結至 DataList 的資料時，我們必須先確定我們已重複處理資料項目目。 這可以藉由檢查 `DataListItem` s [`ItemType` 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.datalistitem.itemtype.aspx)來完成，它可以有[下列八個值](https://msdn.microsoft.com/library/system.web.ui.webcontrols.listitemtype.aspx)的其中一個：

- `AlternatingItem`
- `EditItem`
- `Footer`
- `Header`
- `Item`
- `Pager`
- `SelectedItem`
- `Separator`

`Item` 和 `AlternatingItem``DataListItem` 都構成 DataList 的資料項目。 假設我們重新使用 `Item` 或 `AlternatingItem`，我們會存取系結至目前 `DataListItem`的實際 `ProductsRow` 實例。 `DataListItem` s [`DataItem` 屬性](https://msdn.microsoft.com/system.web.ui.webcontrols.datalistitem.dataitem.aspx)包含 `DataRowView` 物件的參考，其 `Row` 屬性會提供實際 `ProductsRow` 物件的參考。

接下來，我們會檢查 `ProductsRow` 實例的 `UnitPrice` 屬性。 因為 Products 資料表的 `UnitPrice` 欄位允許 `NULL` 值，所以在嘗試存取 `UnitPrice` 屬性之前，應該先使用 `IsUnitPriceNull()` 方法檢查是否有 `NULL` 值。 如果未 `NULL``UnitPrice` 值，我們會接著檢查其是否小於 $20.00。 如果確實低於 $20.00，則需要套用自訂格式。

## <a name="step-3-highlighting-the-product-s-name-and-price"></a>步驟3：反白顯示產品的名稱和價格

一旦我們知道產品的價格小於 $20.00，剩下的就是反白顯示其名稱和價格。 若要完成這項工作，我們必須先以程式設計方式參考 `ItemTemplate` 中顯示產品名稱和價格的標籤控制項。 接下來，我們必須讓它們顯示黃色的背景。 您可以直接修改標籤 `BackColor` 屬性（`LabelID.BackColor = Color.Yellow`）來套用此格式資訊;不過，在理想的情況下，所有顯示相關的事物都應該透過級聯樣式表單來表示。 事實上，我們已經有一個樣式表單，提供在 `Styles.css` - `AffordablePriceEmphasis`中所定義的格式，這是在*根據資料的自訂格式*教學課程中建立和討論的。

若要套用格式，只需將兩個標籤 Web 控制項 `CssClass` 屬性設定為 `AffordablePriceEmphasis`，如下列程式碼所示：

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample2.cs)]

當 `ItemDataBound` 事件處理常式完成時，請在瀏覽器中重新流覽 `Formatting.aspx` 頁面。 如 [圖 2] 所示，價格低於 $20.00 的產品會反白顯示其名稱和價格。

[![小於 $20.00 的產品會反白顯示](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image5.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image4.png)

**圖 2**：小於 $20.00 的產品會反白顯示（[按一下以觀看完整大小的影像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image6.png)）

> [!NOTE]
> 由於 DataList 會轉譯為 HTML `<table>`，因此其 `DataListItem` 實例具有樣式相關的屬性，可設定為將特定樣式套用至整個專案。 例如，如果我們想要在價格小於 $20.00 時將*整個*專案反白顯示，我們可以取代參考標籤的程式碼，並使用下列程式程式碼來設定其 `CssClass` 屬性： `e.Item.CssClass = "AffordablePriceEmphasis"` （請參閱 [圖 3]）。

而組成中繼器控制項的 `RepeaterItem` 則不會提供這類的樣式層級屬性。 因此，將自訂格式套用至中繼器時，需要將樣式屬性應用到 Repeater 範本內的 Web 控制項，就像我們在 [圖 2] 中所做的一樣。

[![$20.00 下的產品會反白顯示整個產品專案](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image8.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image7.png)

**圖 3**：針對 $20.00 底下的產品，將整個產品專案反白顯示（[按一下以觀看完整大小的影像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image9.png)）

## <a name="using-formatting-functions-from-within-the-template"></a>從範本內使用格式化函數

在 [在*Gridview 控制項中使用 TemplateFields* ] 教學課程中，我們已瞭解如何使用 gridview TemplateField 內的格式函數，根據系結至 GridView 的資料列來套用自訂格式。 格式化函式是一種方法，可以從範本叫用，並傳回要在其位置發出的 HTML。 格式化函式可以位於 ASP.NET 網頁的程式碼後置類別中，也可以集中到 `App_Code` 資料夾或個別類別庫專案中的類別檔案。 如果您計畫在多個 ASP.NET 網頁或其他 ASP.NET web 應用程式中使用相同的格式函式，則將格式函式從 ASP.NET 網頁的程式碼後置類別移出是理想的選擇。

若要示範格式化函式，請讓產品資訊包含產品 s 名稱旁邊的 [已停用] 文字（如果已停止）。 此外，如果小於 $20.00，讓的價格反白顯示為黃色（如同我們在 `ItemDataBound` 事件處理常式範例中所做的）;如果價格是 $20.00 或更高，讓不會顯示實際價格，而是改為使用價格報價的文字。 [圖 4] 顯示已套用這些格式規則之產品清單的螢幕擷取畫面。

[![昂貴的產品，價格會以文字取代，請撥打價格報價](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image11.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image10.png)

**圖 4**：對於昂貴的產品，價格會以文字取代，請撥打價格報價（[按一下以查看完整大小的影像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image12.png)）

## <a name="step-1-create-the-formatting-functions"></a>步驟1：建立格式函數

在此範例中，我們需要兩個格式化函式，其中一個會顯示產品名稱，連同文字 [已停止]，如有需要，另一個則顯示反白顯示的價格（如果小於 $20.00）或文字，請在其他情況下呼叫價格報價。 讓我們在 ASP.NET 網頁的程式碼後置類別中建立這些函式，並將它們命名為 `DisplayProductNameAndDiscontinuedStatus` 和 `DisplayPrice`。 這兩種方法都必須傳回 HTML 以轉譯為字串，而且兩者都必須標示 `Protected` （或 `Public`），才能從 ASP.NET 網頁的宣告式語法部分中叫用。 這兩種方法的程式碼如下所示：

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample3.cs)]

請注意，`DisplayProductNameAndDiscontinuedStatus` 方法會接受 `productName` 的值，並將資料欄位 `discontinued` 為純量值，而 `DisplayPrice` 方法會接受 `ProductsRow` 實例（而不是 `unitPrice` 純量值）。 這兩種方法都可行;不過，如果格式化函式使用的純量值可以包含資料庫 `NULL` 值（例如 `UnitPrice`; `ProductName` 或 `Discontinued` 不允許 `NULL` 值），則必須特別小心處理這些純量輸入。

特別的是，輸入參數的類型必須是 `Object`，因為傳入的值可能是 `DBNull` 實例，而不是預期的資料類型。 此外，必須進行檢查，以判斷傳入值是否為資料庫 `NULL` 值。 也就是說，如果我們想要 `DisplayPrice` 方法接受純量值的價格，我們必須使用下列程式碼：

[!code-csharp[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample4.cs)]

請注意，`unitPrice` 輸入參數的類型是 `Object`，而且已修改條件陳述式，以確定 `unitPrice` 是否 `DBNull`。 此外，由於 `unitPrice` 輸入參數是以 `Object`的形式傳入，因此必須轉換成十進位值。

## <a name="step-2-calling-the-formatting-function-from-the-datalist-s-itemtemplate"></a>步驟2：從 DataList s ItemTemplate 呼叫格式化函數

將格式化函式新增至 ASP.NET 網頁的程式碼後置類別後，剩下的工作就是從 DataList s `ItemTemplate`叫用這些格式函數。 若要從範本呼叫格式化函式，請將函式呼叫放在資料系結語法中：

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample5.aspx)]

在 DataList s 中 `ItemTemplate` `ProductNameLabel` Label Web 控制項目前會藉由將 `<%# Eval("ProductName") %>`的結果指派給其 `Text` 屬性，來顯示產品的名稱。 若要讓它顯示名稱加上 [已停止] 文字，請視需要更新宣告式語法，使其改為指派 `Text` 屬性 `DisplayProductNameAndDiscontinuedStatus` 方法的值。 當您這麼做時，必須使用 `Eval("columnName")` 語法來傳入產品的名稱和已停止的值。 `Eval` 會傳回 `Object`類型的值，但 `DisplayProductNameAndDiscontinuedStatus` 方法需要 `String` 和 `Boolean`類型的輸入參數。因此，我們必須將 `Eval` 方法所傳回的值，轉換為預期的輸入參數類型，如下所示：

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample6.aspx)]

若要顯示價格，我們可以直接將 `UnitPriceLabel` 標籤 `Text` 屬性設定為 `DisplayPrice` 方法所傳回的值，就像我們用來顯示產品名稱和 [已停用] 的文字一樣。 不過，我們會改為傳入整個 `ProductsRow` 實例，而不是以純量輸入參數的形式傳入 `UnitPrice`：

[!code-aspx[Main](formatting-the-datalist-and-repeater-based-upon-data-cs/samples/sample7.aspx)]

在設定格式函式的呼叫之後，請花一點時間在瀏覽器中查看進度。 您的畫面看起來應該像 [圖 5]，其中已淘汰的產品（包括 [已停止] 文字），而那些產品的價格超過 $20.00，而其價格已取代為「請撥打價格報價」的文字。

[![昂貴的產品，價格會以文字取代，請撥打價格報價](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image14.png)](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image13.png)

**圖 5**：對於昂貴的產品，價格會以文字取代，請撥打價格報價（[按一下以查看完整大小的影像](formatting-the-datalist-and-repeater-based-upon-data-cs/_static/image15.png)）

## <a name="summary"></a>總結

根據資料來格式化 DataList 或重複項控制項的內容時，可以使用兩種方法來完成。 第一種方法是建立 `ItemDataBound` 事件的事件處理常式，當資料來源中的每筆記錄系結至新 `DataListItem` 或 `RepeaterItem`時，就會引發這個事件。 在 `ItemDataBound` 事件處理常式中，可以檢查目前的專案資料，然後將格式設定套用至範本的內容，或在整個專案本身的 `DataListItem` s。

或者，您也可以透過格式化功能來實現自訂格式。 格式化函式是一種方法，可以從 DataList 或 Repeater 的範本叫用，以傳回要在其位置發出的 HTML。 通常，格式化函式所傳回的 HTML 會由系結至目前專案的值決定。 這些值可以傳遞至格式化函式，可能是純量值，或傳入整個物件系結至專案（例如 `ProductsRow` 實例）。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Yaakov Ellis、Randy Schmidt 和 Liz Shulok。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](displaying-data-with-the-datalist-and-repeater-controls-cs.md)
> [下一頁](showing-multiple-records-per-row-with-the-datalist-control-cs.md)
