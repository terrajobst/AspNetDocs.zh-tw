---
uid: web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
title: 依據資料自訂格式設定（VB） |Microsoft Docs
author: rick-anderson
description: 根據系結的資料來調整 GridView、DetailsView 或 FormView 的格式，可以透過多種方式來完成。 在本教學課程中，我們將 。
ms.author: riande
ms.date: 03/31/2010
ms.assetid: df5a1525-386f-4632-972c-57b199870bc3
msc.legacyurl: /web-forms/overview/data-access/custom-formatting/custom-formatting-based-upon-data-vb
msc.type: authoredcontent
ms.openlocfilehash: 268dc763ef6954903f721a3015daaf10bf9bccb1
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78596709"
---
# <a name="custom-formatting-based-upon-data-vb"></a>根據資料自訂格式設定 (VB)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/5/7/0/57084608-dfb3-4781-991c-407d086e2adc/ASPNET_Data_Tutorial_11_VB.exe)或[下載 PDF](custom-formatting-based-upon-data-vb/_static/datatutorial11vb1.pdf)

> 根據系結的資料來調整 GridView、DetailsView 或 FormView 的格式，可以透過多種方式來完成。 在本教學課程中，我們將探討如何透過使用資料系結和 RowDataBound 事件處理常式來完成資料系結格式設定。

## <a name="introduction"></a>簡介

GridView、DetailsView 和 FormView 控制項的外觀，可以透過許多與樣式相關的屬性來自訂。 `CssClass`、`Font`、`BorderWidth`、`BorderStyle`、`BorderColor`、`Width`和 `Height`等屬性會指示呈現控制項的一般外觀。 包括 `HeaderStyle`、`RowStyle`、`AlternatingRowStyle`和其他屬性，都允許將這些相同的樣式設定套用到特定區段。 同樣地，您也可以在欄位層級套用這些樣式設定。

不過，在許多情況下，格式化需求取決於所顯示資料的值。 例如，若要將注意力吸引出存貨產品，列出產品資訊的報表可能會將 `UnitsInStock` 和 `UnitsOnOrder` 欄位都等於0的產品的背景色彩設定為黃色。 為了強調較昂貴的產品，我們可能會想要以粗體字型顯示這些產品的價格超過 $75.00 的成本。

根據系結的資料來調整 GridView、DetailsView 或 FormView 的格式，可以透過多種方式來完成。 在本教學課程中，我們將探討如何使用 `DataBound` 和 `RowDataBound` 事件處理常式來完成資料系結格式設定。 在下一個教學課程中，我們將探討另一種方法。

## <a name="using-the-detailsview-controlsdataboundevent-handler"></a>使用 DetailsView 控制項的`DataBound`事件處理常式

當資料系結至 DetailsView 時（從資料來源控制項，或透過程式設計方式將資料指派給控制項的 `DataSource` 屬性並呼叫其 `DataBind()` 方法），會發生下列一系列的步驟：

1. 會引發資料 Web 控制項的 `DataBinding` 事件。
2. 資料會系結至資料 Web 控制項。
3. 會引發資料 Web 控制項的 `DataBound` 事件。

自訂邏輯可以緊接在步驟1和3之後，透過事件處理常式插入。 藉由建立 `DataBound` 事件的事件處理常式，我們可以程式設計方式判斷已系結至資料 Web 控制項的資料，並視需要調整格式。 為了說明這一點，讓我們建立一個 DetailsView，其中會列出產品的一般資訊，但會以***粗體的斜體字型***顯示 `UnitPrice` 值（如果超過 $75.00）。

## <a name="step-1-displaying-the-product-information-in-a-detailsview"></a>步驟1：在 DetailsView 中顯示產品資訊

開啟 [`CustomFormatting`] 資料夾中的 [`CustomColors.aspx`] 頁面，將 [DetailsView] 控制項從 [工具箱] 拖曳至設計工具，將其 [`ID`] 屬性值設定為 [`ExpensiveProductsPriceInBoldItalic`]，並將它系結至叫用 `ProductsBLL` 類別之 `GetProducts()` 方法的新 ObjectDataSource 控制項。 為了簡單起見，我們在此省略了完成這項操作的詳細步驟，因為我們會在先前的教學課程中詳細地檢查它們。

將 ObjectDataSource 系結至 DetailsView 之後，請花一點時間修改欄位清單。 我選擇移除 `ProductID`、`SupplierID`、`CategoryID`、`UnitsInStock`、`UnitsOnOrder`、`ReorderLevel`和 `Discontinued` BoundFields，然後重新命名並重新格式化其餘 BoundFields。 我也清除了 `Width` 並 `Height` 設定。 因為 DetailsView 只會顯示一筆記錄，所以我們需要啟用分頁，才能讓終端使用者查看所有產品。 若要這麼做，請勾選 DetailsView 的智慧標籤中的 [啟用分頁] 核取方塊。

[![圖1：核取 DetailsView 的智慧標籤中的 [啟用分頁] 核取方塊](custom-formatting-based-upon-data-vb/_static/image2.png)](custom-formatting-based-upon-data-vb/_static/image1.png)

**圖 1**：圖1：核取 DetailsView 的智慧標籤中的 [啟用分頁] 核取方塊（[按一下以查看完整大小的影像](custom-formatting-based-upon-data-vb/_static/image3.png)）

這些變更之後，DetailsView 標記會是：

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample1.aspx)]

請花點時間在瀏覽器中測試此頁面。

[![DetailsView 控制項一次顯示一項產品](custom-formatting-based-upon-data-vb/_static/image5.png)](custom-formatting-based-upon-data-vb/_static/image4.png)

**圖 2**： DetailsView 控制項一次顯示一項產品（[按一下以觀看完整大小的影像](custom-formatting-based-upon-data-vb/_static/image6.png)）

## <a name="step-2-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>步驟2：在資料系結事件處理常式中以程式設計方式決定資料的值

為了以粗體、斜體字型顯示其 `UnitPrice` 值超過 $75.00 的價格，我們必須先能夠以程式設計方式判斷 `UnitPrice` 值。 針對 DetailsView，可以在 `DataBound` 事件處理常式中完成這項作業。 若要建立事件處理常式，請在設計工具中按一下 [DetailsView]，然後流覽至 [屬性視窗]。 如果看不到，請按 F4，或移至 [View] 功能表，然後選取 [屬性視窗] 功能表選項。 從 屬性視窗中，按一下閃電圖示來列出 DetailsView 的事件。 接下來，按兩下 [`DataBound`] 事件，或輸入您想要建立的事件處理常式名稱。

![建立資料系結事件的事件處理常式](custom-formatting-based-upon-data-vb/_static/image7.png)

**圖 3**：建立 `DataBound` 事件的事件處理常式

> [!NOTE]
> 您也可以從 ASP.NET 網頁的程式碼部分建立事件處理常式。 在這裡，您會在頁面頂端找到兩個下拉式清單。 從左側下拉式清單中選取物件，並從右邊的下拉式清單中選取您想要建立處理常式的事件，Visual Studio 將會自動建立適當的事件處理常式。

這麼做會自動建立事件處理常式，並帶您前往已加入它的程式碼部分。 此時您會看到：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample2.vb)]

系結至 DetailsView 的資料可以透過 `DataItem` 屬性來存取。 回想一下，我們會將控制項系結至強型別 DataTable，這是由強型別 DataRow 實例的集合所組成。 當 DataTable 系結至 DetailsView 時，DataTable 中的第一個 DataRow 會指派給 DetailsView 的 `DataItem` 屬性。 具體而言，`DataItem` 屬性會指派 `DataRowView` 物件。 我們可以使用 `DataRowView`的 `Row` 屬性來取得基礎 DataRow 物件的存取權，這實際上是 `ProductsRow` 實例。 一旦有了這個 `ProductsRow` 實例，我們就可以直接檢查物件的屬性值來做出決定。

下列程式碼說明如何判斷系結至 DetailsView 控制項的 `UnitPrice` 值是否大於 $75.00：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample3.vb)]

> [!NOTE]
> 由於 `UnitPrice` 在資料庫中可以有 `NULL` 值，因此我們會先檢查並確定我們不會處理 `NULL` 值，然後才存取 `ProductsRow`的 `UnitPrice` 屬性。 這項檢查很重要，因為如果我們在具有 `NULL` 值時嘗試存取 `UnitPrice` 屬性，`ProductsRow` 物件將會擲回[system.data.strongtypingexception 例外](https://msdn.microsoft.com/library/system.data.strongtypingexception.aspx)狀況。

## <a name="step-3-formatting-the-unitprice-value-in-the-detailsview"></a>步驟3：格式化 DetailsView 中的單價值

此時，我們可以判斷系結至 DetailsView 的 `UnitPrice` 值是否有超過 $75.00 的值，但我們還不知道如何以程式設計方式調整 DetailsView 的格式。 若要修改 DetailsView 中整個資料列的格式，請使用 `DetailsViewID.Rows(index)`以程式設計方式存取資料列。若要修改特定的資料格，請使用 `DetailsViewID.Rows(index).Cells(index)`的存取權。 一旦有了資料列或資料格的參考之後，就可以藉由設定其樣式相關的屬性來調整其外觀。

以程式設計方式存取資料列時，您必須知道資料列的索引，其開頭為0。 `UnitPrice` 的資料列是 DetailsView 中的第五個數據列，並提供索引4，讓它以程式設計方式使用 `ExpensiveProductsPriceInBoldItalic.Rows(4)`來存取。 此時，我們可以使用下列程式碼，以粗體的斜體字型顯示整個資料列的內容：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample4.vb)]

不過，這會讓標籤（價格）和*值為粗體*和斜體。 如果我們只想要將值設為粗體和斜體，我們必須將此格式套用到資料列中的第二個數據格，這可以使用下列方式來完成：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample5.vb)]

由於我們的教學課程已經使用樣式表單來維護轉譯的標記和樣式相關資訊之間的清楚分隔，而不是設定特定樣式屬性（如上所示），而是改用 CSS 類別。 開啟 `Styles.css` 樣式表單，並使用下列定義加入名為 `ExpensivePriceEmphasis` 的新 CSS 類別：

[!code-css[Main](custom-formatting-based-upon-data-vb/samples/sample6.css)]

然後，在 `DataBound` 事件處理常式中，將儲存格的 `CssClass` 屬性設定為 [`ExpensivePriceEmphasis`]。 下列程式碼會顯示完整的 `DataBound` 事件處理常式：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample7.vb)]

當您觀看 Chai （成本低於 $75.00）時，價格會以一般字型顯示（請參閱 [圖 4]）。 不過，當您在 Mishi Kobe Niku （其價格為 $97.00）時，價格會以粗體的斜體字型顯示（請參閱 [圖 5]）。

[低於 $75.00 的 ![價格會以一般字型顯示](custom-formatting-based-upon-data-vb/_static/image9.png)](custom-formatting-based-upon-data-vb/_static/image8.png)

**圖 4**：小於 $75.00 的價格會以一般字型顯示（[按一下以觀看完整大小的影像](custom-formatting-based-upon-data-vb/_static/image10.png)）

[![昂貴的產品價格會以粗體的斜體字型顯示](custom-formatting-based-upon-data-vb/_static/image12.png)](custom-formatting-based-upon-data-vb/_static/image11.png)

**圖 5**：昂貴的產品價格會以粗體的斜體字型顯示（[按一下以觀看完整大小的影像](custom-formatting-based-upon-data-vb/_static/image13.png)）

## <a name="using-the-formview-controlsdataboundevent-handler"></a>使用 FormView 控制項的`DataBound`事件處理常式

判斷系結至 FormView 之基礎資料的步驟，與 DetailsView 建立 `DataBound` 事件處理常式、將 `DataItem` 屬性轉換成系結至控制項的適當物件類型，以及決定如何繼續。 不過，FormView 和 DetailsView 在其使用者介面外觀的更新方式上有所不同。

FormView 不包含任何 BoundFields，因此缺少 `Rows` 集合。 取而代之的是，FormView 是由樣板組成，這些範本可以混合使用靜態 HTML、Web 控制項和資料系結語法。 調整 FormView 的樣式通常牽涉到調整 FormView 範本內一個或多個 Web 控制項的樣式。

為了說明這一點，讓我們使用 FormView 來列出上述範例中的產品，但這次讓我們只顯示產品名稱和庫存單位，其中包含以紅色字型顯示的單位（如果小於或等於10）。

## <a name="step-4-displaying-the-product-information-in-a-formview"></a>步驟4：在 FormView 中顯示產品資訊

將 FormView 加入至 DetailsView 底下的 [`CustomColors.aspx`] 頁面，並將其 [`ID`] 屬性設定為 [`LowStockedProductsInRed`]。 將 FormView 系結至上一個步驟所建立的 ObjectDataSource 控制項。 這會建立 FormView 的 `ItemTemplate`、`EditItemTemplate`和 `InsertItemTemplate`。 移除 `EditItemTemplate` 並 `InsertItemTemplate` 並簡化 `ItemTemplate`，使其僅包含 `ProductName` 和 `UnitsInStock` 值，每個都在各自適當命名的標籤控制項中。 如同先前範例中的 DetailsView，另請核取 FormView 的智慧標籤中的 [啟用分頁] 核取方塊。

在這些編輯之後，您的 FormView 標記看起來應該如下所示：

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample8.aspx)]

請注意，`ItemTemplate` 包含：

- **靜態 HTML** ：「產品：」和「庫存中的單位」文字，以及 `<br />` 和 `<b>` 元素。
- **Web 控制**兩個標籤控制項，`ProductNameLabel` 和 `UnitsInStockLabel`。
- **資料**系結語法： `<%# Bind("ProductName") %>` 和 `<%# Bind("UnitsInStock") %>` 語法，會將這些欄位中的值指派給 Label 控制項的 `Text` 屬性。

## <a name="step-5-programmatically-determining-the-value-of-the-data-in-the-databound-event-handler"></a>步驟5：在資料系結事件處理常式中以程式設計方式決定資料的值

完成 FormView 的標記後，下一個步驟是以程式設計方式判斷 `UnitsInStock` 值是否小於或等於10。 這是以 FormView 的相同方式來完成，如同使用 DetailsView 一樣。 首先，建立 FormView 的 `DataBound` 事件的事件處理常式。

![建立資料系結事件處理常式](custom-formatting-based-upon-data-vb/_static/image14.png)

**圖 6**：建立 `DataBound` 事件處理常式

在事件處理常式中，將 FormView 的 `DataItem` 屬性轉換成 `ProductsRow` 實例，並判斷 `UnitsInPrice` 值是否需要以紅色字型顯示。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample9.vb)]

## <a name="step-6-formatting-the-unitsinstocklabel-label-control-in-the-formviews-itemtemplate"></a>步驟6：格式化 FormView 的 ItemTemplate 中的 UnitsInStockLabel Label 控制項

最後一個步驟是將顯示的 `UnitsInStock` 值格式化為紅色字型（如果值小於或等於10）。 若要完成這項操作，我們需要以程式設計方式存取 `ItemTemplate` 中的 `UnitsInStockLabel` 控制項，並設定其樣式屬性，使其文字以紅色顯示。 若要存取範本中的 Web 控制項，請使用 `FindControl("controlID")` 方法，如下所示：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample10.vb)]

在我們的範例中，我們想要存取 `ID` 值 `UnitsInStockLabel`的標籤控制項，因此我們將使用：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample11.vb)]

一旦有了 Web 控制項的程式設計參考，我們就可以視需要修改其樣式相關的屬性。 如同先前的範例，我已在名為 `LowUnitsInStockEmphasis`的 `Styles.css` 中建立 CSS 類別。 若要將此樣式套用至標籤 Web 控制項，請據以設定其 `CssClass` 屬性。

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample12.vb)]

> [!NOTE]
> 在 DetailsView 或 GridView 控制項中使用[TemplateFields](https://msdn.microsoft.com/library/system.web.ui.webcontrols.templatefield(VS.80).aspx)時，也可以使用以程式設計方式來格式化範本，並使用 `FindControl("controlID")` 然後設定其樣式相關屬性的語法。 我們會在下一個教學課程中檢查 TemplateFields。

[圖 7] 顯示 FormView 在觀看產品時，其 `UnitsInStock` 值大於10，而 [圖 8] 中的產品值小於10。

[![在庫存中具有夠大單位的產品，則不會套用任何自訂格式](custom-formatting-based-upon-data-vb/_static/image16.png)](custom-formatting-based-upon-data-vb/_static/image15.png)

**圖 7**：對於具有足夠大單位庫存的產品，不會套用任何自訂格式（[按一下以觀看完整大小的影像](custom-formatting-based-upon-data-vb/_static/image17.png)）

[![值為10（含）以下的產品的庫存號碼單位會以紅色顯示](custom-formatting-based-upon-data-vb/_static/image19.png)](custom-formatting-based-upon-data-vb/_static/image18.png)

**圖 8**：庫存號碼中的單位會以紅色顯示，這些產品的值為10或更小（[按一下以觀看完整大小的影像](custom-formatting-based-upon-data-vb/_static/image20.png)）

## <a name="formatting-with-the-gridviewsrowdataboundevent"></a>使用 GridView 的`RowDataBound`事件進行格式設定

我們稍早在資料系結期間檢查了 DetailsView 和 FormView 控制進度的步驟順序。 讓我們再次檢查一下這些步驟，做為重新整理程式。

1. 會引發資料 Web 控制項的 `DataBinding` 事件。
2. 資料會系結至資料 Web 控制項。
3. 會引發資料 Web 控制項的 `DataBound` 事件。

這三個簡單的步驟就足以進行 DetailsView 和 FormView，因為它們只會顯示一筆記錄。 針對 GridView，會顯示系結至它的*所有*記錄（而不只是第一個），步驟2則比較複雜。

在步驟2中，GridView 會列舉資料來源，而針對每一筆記錄，會建立一個 `GridViewRow` 實例，並將目前的記錄系結至它。 針對加入至 GridView 的每個 `GridViewRow`，會引發兩個事件：

- 建立 `GridViewRow` 之後， **`RowCreated`** 引發
- **`RowDataBound`** 在目前的記錄已系結至 `GridViewRow`之後引發。

就 GridView 而言，資料系結會更準確地由下列一系列的步驟來描述：

1. GridView 的 `DataBinding` 事件會引發。
2. 資料會系結至 GridView。   
  
   針對資料來源中的每筆記錄 

    1. 建立 `GridViewRow` 物件
    2. 引發 `RowCreated` 事件
    3. 將記錄系結至 `GridViewRow`
    4. 引發 `RowDataBound` 事件
    5. 將 `GridViewRow` 新增至 `Rows` 集合
3. GridView 的 `DataBound` 事件會引發。

若要自訂 GridView 個別記錄的格式，我們必須建立 `RowDataBound` 事件的事件處理常式。 為了說明這一點，讓我們將 GridView 新增至 [`CustomColors.aspx`] 頁面，其中列出每個產品的名稱、類別和價格，並以黃色的背景色彩反白顯示價格小於 $10.00 的產品。

## <a name="step-7-displaying-product-information-in-a-gridview"></a>步驟7：在 GridView 中顯示產品資訊

在先前範例中的 FormView 底下新增 GridView，並將其 `ID` 屬性設為 `HighlightCheapProducts`。 因為我們已經有一個會傳回頁面上所有產品的 ObjectDataSource，所以請將 GridView 系結至該頁面。 最後，編輯 GridView 的 BoundFields，只包含產品的名稱、類別和價格。 在這些編輯之後，GridView 的標記看起來應該像這樣：

[!code-aspx[Main](custom-formatting-based-upon-data-vb/samples/sample13.aspx)]

[圖 9] 顯示透過瀏覽器觀看此點的進度。

[![GridView 會列出每個產品的名稱、類別和價格](custom-formatting-based-upon-data-vb/_static/image22.png)](custom-formatting-based-upon-data-vb/_static/image21.png)

**圖 9**： GridView 會列出每個產品的名稱、類別和價格（[按一下以查看完整大小的影像](custom-formatting-based-upon-data-vb/_static/image23.png)）

## <a name="step-8-programmatically-determining-the-value-of-the-data-in-the-rowdatabound-event-handler"></a>步驟8：以程式設計方式判斷 RowDataBound 事件處理常式中的資料值

當 `ProductsDataTable` 系結至 GridView 時，會列舉其 `ProductsRow` 實例，並針對每個 `ProductsRow` 建立 `GridViewRow`。 `GridViewRow`的 `DataItem` 屬性會指派給特定的 `ProductRow`，在此之後，會引發 GridView 的 `RowDataBound` 事件處理常式。 若要判斷系結至 GridView 之每個產品的 `UnitPrice` 值，則需要為 GridView 的 `RowDataBound` 事件建立事件處理常式。 在這個事件處理常式中，我們可以檢查目前 `GridViewRow` 的 `UnitPrice` 值，並針對該資料列進行格式設定決策。

您可以使用與 FormView 和 DetailsView 相同的一系列步驟來建立這個事件處理常式。

![建立 GridView RowDataBound 事件的事件處理常式](custom-formatting-based-upon-data-vb/_static/image24.png)

**圖 10**：為 GridView 的 `RowDataBound` 事件建立事件處理常式

以這種方式建立事件處理常式，會將下列程式碼自動新增至 ASP.NET 網頁的程式碼部分：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample14.vb)]

當 `RowDataBound` 事件引發時，事件處理常式會當做第二個參數類型的物件傳遞 `GridViewRowEventArgs`，其具有名為 `Row`的屬性。 這個屬性會傳回只是資料系結之 `GridViewRow` 的參考。 若要存取系結至 `GridViewRow` 的 `ProductsRow` 實例，我們使用 `DataItem` 屬性，如下所示：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample15.vb)]

使用 `RowDataBound` 事件處理常式時，請務必記住 GridView 是由不同類型的資料列所組成，而且會針對*所有*資料列類型引發此事件。 `GridViewRow`的型別可以透過其 `RowType` 屬性來決定，而且可以有其中一個可能的值：

- `DataRow` 從 GridView 的 `DataSource` 系結至記錄的資料列
- `EmptyDataRow` GridView 的 `DataSource` 為空白時所顯示的資料列
- `Footer` 頁尾資料列;當 GridView 的 `ShowFooter` 屬性設定為時顯示 `True`
- `Header` 標頭資料列;如果 GridView 的 ShowHeader 屬性設定為 `True` （預設值），則會顯示
- 適用于執行分頁之 GridView 的 `Pager`，顯示分頁介面的資料列
- `Separator` 不是用於 GridView，而是由 DataList 和重複項控制項的 `RowType` 屬性使用，我們將在未來的教學課程中討論兩個數據 Web 控制項

由於 `EmptyDataRow`、`Header`、`Footer`和 `Pager` 資料列不會與 `DataSource` 記錄相關聯，因此其 [`Nothing`] 屬性的值一律為 [`DataItem`]。 基於這個理由，在嘗試使用目前 `GridViewRow`的 `DataItem` 屬性之前，我們必須先確定我們正在處理 `DataRow`。 這可以藉由檢查 `GridViewRow`的 `RowType` 屬性來完成，如下所示：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample16.vb)]

## <a name="step-9-highlighting-the-row-yellow-when-the-unitprice-value-is-less-than-1000"></a>步驟9：當單價值小於 $10.00 時，將資料列反白顯示為黃色

最後一個步驟是，如果該資料列的 `UnitPrice` 值小於 $10.00，以程式設計方式反白顯示整個 `GridViewRow`。 存取 GridView 的資料列或資料格的語法與 DetailsView `GridViewID.Rows(index)` 用來存取整個資料列，`GridViewID.Rows(index).Cells(index)` 存取特定的資料格。 不過，當 `RowDataBound` 事件處理常式引發資料系結 `GridViewRow` 尚未加入 GridView 的 `Rows` 集合。 因此，您無法使用 Rows 集合，從 `RowDataBound` 事件處理常式存取目前的 `GridViewRow` 實例。

我們可以使用 `e.Row`來參考 `RowDataBound` 事件處理常式中目前的 `GridViewRow` 實例，而不是 `GridViewID.Rows(index)`。 也就是說，若要從我們要使用的 `RowDataBound` 事件處理常式中反白顯示目前的 `GridViewRow` 實例：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample17.vb)]

我們不會直接設定 `GridViewRow`的 `BackColor` 屬性，而是使用 CSS 類別。 我建立了一個名為 `AffordablePriceEmphasis` 的 CSS 類別，將背景色彩設定為黃色。 完成的 `RowDataBound` 事件處理常式如下：

[!code-vb[Main](custom-formatting-based-upon-data-vb/samples/sample18.vb)]

[![最實惠的產品會以黃色反白顯示](custom-formatting-based-upon-data-vb/_static/image26.png)](custom-formatting-based-upon-data-vb/_static/image25.png)

**圖 11**：最經濟實惠的產品會以黃色反白顯示（[按一下以觀看完整大小的影像](custom-formatting-based-upon-data-vb/_static/image27.png)）

## <a name="summary"></a>總結

在本教學課程中，我們已瞭解如何根據系結至控制項的資料來格式化 GridView、DetailsView 和 FormView。 為了達成此目的，我們建立了 `DataBound` 或 `RowDataBound` 事件的事件處理常式，其中基礎資料會與格式變更一起檢查（如有需要）。 若要存取系結至 DetailsView 或 FormView 的資料，我們會在 `DataBound` 事件處理常式中使用 `DataItem` 屬性;就 GridView 而言，每個 `GridViewRow` 實例的 `DataItem` 屬性都會包含系結至該資料列的資料，而這可在 `RowDataBound` 事件處理常式中使用。

以程式設計方式調整資料 Web 控制項的格式的語法，取決於 Web 控制項以及如何顯示要格式化的資料。 對於 DetailsView 和 GridView 控制項，資料列和資料格可以透過序數索引來存取。 針對使用範本的 FormView，`FindControl("controlID")` 方法通常用來從範本內尋找 Web 控制項。

在下一個教學課程中，我們將探討如何使用具有 GridView 和 DetailsView 的範本。 此外，我們還會看到另一項技術，可讓您根據基礎資料自訂格式。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝

本教學課程系列已由許多有用的審核者所審查。 本教學課程的潛在客戶審核者已 E.R。 Gilmore、Dennis Patterson 和 Dan Jagers。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](displaying-summary-information-in-the-gridview-s-footer-cs.md)
> [下一頁](using-templatefields-in-the-gridview-control-vb.md)
