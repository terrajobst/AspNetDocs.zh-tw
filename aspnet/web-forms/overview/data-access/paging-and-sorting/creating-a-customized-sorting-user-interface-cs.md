---
uid: web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-cs
title: 建立自訂的排序使用者介面C#（） |Microsoft Docs
author: rick-anderson
description: 當顯示一長串的已排序資料時，藉由引進分隔符號列來分組相關資料可能會很有説明。 在本教學課程中，我們將瞭解如何認證 。
ms.author: riande
ms.date: 08/15/2006
ms.assetid: 6f81b633-9d01-4e52-ae4a-2ea6bc109475
msc.legacyurl: /web-forms/overview/data-access/paging-and-sorting/creating-a-customized-sorting-user-interface-cs
msc.type: authoredcontent
ms.openlocfilehash: 93ec07a13de80e4c874ff46b5dfa626b60b632c8
ms.sourcegitcommit: 22fbd8863672c4ad6693b8388ad5c8e753fb41a2
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 11/28/2019
ms.locfileid: "74597274"
---
# <a name="creating-a-customized-sorting-user-interface-c"></a>建立自訂的排序使用者介面 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_27_CS.exe)或[下載 PDF](creating-a-customized-sorting-user-interface-cs/_static/datatutorial27cs1.pdf)

> 當顯示一長串的已排序資料時，藉由引進分隔符號列來分組相關資料可能會很有説明。 在本教學課程中，我們將瞭解如何建立這類排序使用者介面。

## <a name="introduction"></a>簡介

顯示已排序資料的一長串清單，其中只有幾個不同的值在已排序的資料行中，終端使用者可能會發現很難辨識差異界限發生的位置。 例如，資料庫中有81產品，但只有九個不同的類別選擇（八個唯一的分類加上 `NULL` 選項）。 請考慮有興趣檢查落在 [海鮮] 類別之下之產品的使用者案例。 在單一 GridView 中列出*所有*產品的頁面中，使用者可能會決定其最佳做法是依類別排序結果，這會將所有的海鮮產品群組在一起。 依類別排序之後，使用者就必須搜尋清單，尋找以海鮮分組的產品開始和結束的位置。 由於結果是依分類名稱以字母順序排序，尋找海鮮產品並不容易，但仍然需要仔細掃描方格中的專案清單。

為了協助強調已排序群組之間的界限，許多網站都採用使用者介面，在這類群組之間加上分隔符號。 像 [圖 1] 所示的分隔符號，可以讓使用者更快速地找到特定群組並識別其界限，以及確定資料中有哪些不同的群組存在。

[![清楚識別每個類別目錄群組](creating-a-customized-sorting-user-interface-cs/_static/image2.png)](creating-a-customized-sorting-user-interface-cs/_static/image1.png)

**圖 1**：清楚地識別每個類別目錄群組（[按一下以查看完整大小的影像](creating-a-customized-sorting-user-interface-cs/_static/image3.png)）

在本教學課程中，我們將瞭解如何建立這類排序使用者介面。

## <a name="step-1-creating-a-standard-sortable-gridview"></a>步驟1：建立標準、可排序的 GridView

在我們探索如何增強 GridView 以提供增強型排序介面之前，先建立一個可排序的標準 GridView 來列出產品。 從開啟 [`PagingAndSorting`] 資料夾中的 [`CustomSortingUI.aspx`] 頁面開始。 將 GridView 新增至頁面，將其 [`ID`] 屬性設為 [`ProductList`]，並將它系結至新的 ObjectDataSource。 設定 ObjectDataSource 使用 `ProductsBLL` 類別的 `GetProducts()` 方法來選取記錄。

接下來，設定 GridView，使其只包含 `ProductName`、`CategoryName`、`SupplierName`和 `UnitPrice` BoundFields 和已停止的 CheckBoxField。 最後，藉由勾選 GridView s 智慧標籤中的 [啟用排序] 核取方塊（或將其 [`AllowSorting`] 屬性設定為 [`true`]），將 GridView 設定為支援排序。 在 `CustomSortingUI.aspx` 頁面上新增這些專案之後，宣告式標記看起來應該像下面這樣：

[!code-aspx[Main](creating-a-customized-sorting-user-interface-cs/samples/sample1.aspx)]

在瀏覽器中，花點時間觀看我們的進度。 [圖 2] 顯示可排序的 GridView，其資料依類別目錄依字母順序排序。

[![可排序的 GridView s 資料依類別排序](creating-a-customized-sorting-user-interface-cs/_static/image5.png)](creating-a-customized-sorting-user-interface-cs/_static/image4.png)

**圖 2**：可排序的 GridView s 資料依類別排序（[按一下以觀看完整大小的影像](creating-a-customized-sorting-user-interface-cs/_static/image6.png)）

## <a name="step-2-exploring-techniques-for-adding-the-separator-rows"></a>步驟2：探索加入分隔符號資料列的技巧

使用一般的可排序 GridView 完成後，剩下的工作就是能夠在 GridView 中的每個唯一排序群組之前加入分隔符號資料列。 但這類資料列如何插入 GridView？ 基本上，我們需要逐一查看 GridView 的資料列、判斷已排序資料行中的值之間有何差異，然後再加入適當的分隔欄。 在思考這個問題時，此解決方案似乎是在 GridView 的 `RowDataBound` 事件處理常式中的某處。 如我們在[根據資料的自訂格式](../custom-formatting/custom-formatting-based-upon-data-cs.md)教學課程中所討論，此事件處理常式通常會在根據資料列資料套用資料列層級的格式時使用。 不過，`RowDataBound` 事件處理常式不是這裡的解決方案，因為無法以程式設計方式從這個事件處理常式將資料列加入至 GridView。 事實上，GridView 的 `Rows` 集合是唯讀的。

若要在 GridView 中加入其他資料列，我們有三個選擇：

- 將這些中繼資料分隔資料列新增至系結至 GridView 的實際資料
- 將 GridView 系結至資料之後，將其他 `TableRow` 實例新增至 GridView 的控制項集合
- 建立擴充 GridView 控制項的自訂伺服器控制項，並覆寫負責建立 GridView 結構的方法

如果在許多網頁上或跨多個網站需要這項功能，建立自訂伺服器控制項就是最好的方法。 不過，它需要相當多的程式碼，並徹底探索 GridView 內部工作的深度。 因此，在本教學課程中，我們不會考慮此選項。

其他兩個選項會將分隔符號資料列加入至要系結至 GridView 的實際資料，並在其系結之後操作 GridView 的控制項集合，並以不同的方式攻擊問題並提出討論。

## <a name="adding-rows-to-the-data-bound-to-the-gridview"></a>將資料列加入至系結至 GridView 的資料

當 GridView 系結至資料來源時，它會針對資料來源所傳回的每個記錄建立一個 `GridViewRow`。 因此，我們可以藉由在資料來源中加入分隔記錄，然後將它系結至 GridView，藉以插入所需的分隔資料列。 [圖 3] 說明此概念。

![其中一項技術包括將分隔資料列加入至資料來源](creating-a-customized-sorting-user-interface-cs/_static/image7.png)

**圖 3**：其中一項技術牽涉到將分隔資料列加入至資料來源

我使用引號中的「分隔符號」（separator）記錄，因為沒有任何特殊的分隔符號記錄。相反地，我們必須以某種方式來旗標資料來源中的特定記錄做為分隔符號，而不是一般資料列。 在我們的範例中，我們會將 `ProductsDataTable` 實例重新系結至 GridView，這是由 `ProductRows`所組成。 我們可能會藉由將記錄的 `CategoryID` 屬性設定為 `-1` （因為這樣的值無法正常存在），將記錄標示為分隔資料列。

若要利用這項技術，我們必須執行下列步驟：

1. 以程式設計方式取出資料以系結至 GridView （`ProductsDataTable` 實例）
2. 根據 GridView 的 `SortExpression` 和 `SortDirection` 屬性來排序資料
3. 逐一查看 `ProductsDataTable`中的 `ProductsRows`，尋找已排序資料行中差異的位置
4. 在每個群組界限中，將分隔符號記錄 `ProductsRow` 實例插入 DataTable 中，其 `CategoryID` 設定為 `-1` （或決定將記錄標示為分隔符號記錄的任何指定）
5. 插入分隔符號列之後，以程式設計方式將資料系結至 GridView

除了這五個步驟以外，我們也需要為 GridView 的 `RowDataBound` 事件提供事件處理常式。 在這裡，我們會檢查每個 `DataRow` 並判斷它是否為分隔符號資料列，其 `CategoryID` 設定已 `-1`。 若是如此，我們可能會想要調整其格式或顯示在資料格中的文字。

使用這項技術來插入排序群組界限需要比上述更多的工作，因為您也需要為 GridView 的 `Sorting` 事件提供事件處理常式，並追蹤 `SortExpression` 和 `SortDirection` 值。

## <a name="manipulating-the-gridview-s-control-collection-after-it-s-been-databound"></a>在資料系結之後操作 GridView 的控制項集合

我們可以在將資料系結至 gridview*之後*加入分隔符號資料列，而不是在系結至 gridview 之前，先將資料傳送給它。 資料系結的程式會建立 GridView 的控制階層，事實上，這只是由一系列資料列組成的 `Table` 實例，其中每一個都是由一組資料格所組成。 具體而言，GridView 的控制項集合包含其根目錄的 `Table` 物件、系結至 GridView 之 `DataSource` 中每筆記錄的 `GridViewRow` （衍生自 `TableRow` 類別），以及 `TableCell` 中每個資料欄位的每個 `GridViewRow` 實例中的 `DataSource`物件。

若要在每個排序群組之間加入分隔資料列，我們可以在建立此控制項階層之後直接操作。 我們可以放心，GridView 的控制項階層是在頁面轉譯的最後一次建立的。 因此，此方法會覆寫 `Page` 類別的 `Render` 方法，此時 GridView 的最終控制項階層會更新為包含所需的分隔資料列。 [圖 4] 說明此程式。

[![用於操作 GridView s 控制項階層的替代技術](creating-a-customized-sorting-user-interface-cs/_static/image9.png)](creating-a-customized-sorting-user-interface-cs/_static/image8.png)

**圖 4**：操作 GridView s 控制階層的替代方法（[按一下以觀看完整大小的影像](creating-a-customized-sorting-user-interface-cs/_static/image10.png)）

在本教學課程中，我們將使用這第二個方法來自訂排序使用者體驗。

> [!NOTE]
> 本教學課程中所示範的程式碼是以[Teemu Keiski](http://aspadvice.com/blogs/joteke/default.aspx) s blog 專案中提供的範例為基礎，[並使用 GridView 排序群組來播放一些](http://aspadvice.com/blogs/joteke/archive/2006/02/11/15130.aspx)。

## <a name="step-3-adding-the-separator-rows-to-the-gridview-s-control-hierarchy"></a>步驟3：將分隔符號資料列加入至 GridView 的控制項階層架構

因為我們只想要在控制項階層已建立並在該頁面上最後一次建立時，將分隔資料列加入至 GridView 的控制項階層，所以我們想要在頁面生命週期結束時，但在實際 GridView c 之前執行這項新增控制階層已轉譯為 HTML。 我們可以完成這項工作的最新可能點是 `Page` 類別的 `Render` 事件，我們可以使用下列方法簽章，在程式碼後置類別中覆寫：

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample2.cs)]

叫用 `Page` 類別的原始 `Render` 方法時 `base.Render(writer)` 會轉譯頁面中的每個控制項，並根據控制項階層來產生標記。 因此，我們必須呼叫 `base.Render(writer)`，以便呈現頁面，而且我們會在呼叫 `base.Render(writer)`之前操作 GridView s 控制項階層，以便在轉譯之前將分隔符號資料列新增至 GridView s 控制項階層。

若要插入排序群組標頭，我們必須先確認使用者已要求排序資料。 根據預設，GridView 的內容不會排序，因此不需要輸入任何群組排序標頭。

> [!NOTE]
> 當第一次載入頁面時，如果您想要依特定資料行來排序 GridView，請在第一頁上呼叫 GridView s `Sort` 方法（但不在後續回傳時）。 若要完成這項操作，請在 `if (!Page.IsPostBack)` 條件的 `Page_Load` 事件處理常式中新增此呼叫。 如需 `Sort` 方法的詳細資訊，請回頭參閱[分頁和排序報表資料](paging-and-sorting-report-data-cs.md)教學課程資訊。

假設資料已經過排序，下一項工作是要判斷資料的排序依據，然後掃描資料列以尋找該資料行的值之間的差異。 下列程式碼可確保資料已排序，並尋找資料已排序所依據的資料行：

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample3.cs)]

如果 GridView 尚未排序，則不會設定 GridView 的 `SortExpression` 屬性。 因此，如果這個屬性有一些值，我們只想要加入分隔符號資料列。 如果有的話，我們接下來必須決定資料的排序依據的索引。 這是藉由在 GridView 的 `Columns` 集合中進行迴圈，搜尋其 `SortExpression` 屬性等於 GridView s `SortExpression` 屬性的資料行來完成。 除了資料行的索引之外，我們也會抓取 [`HeaderText`] 屬性，這會在顯示分隔符號資料列時使用。

藉由排序資料的資料行索引，最後一個步驟是列舉 GridView 的列。 針對每個資料列，我們必須判斷排序的資料行的值是否與上一個資料列的排序資料行 s 值不同。 若是如此，我們必須將新的 `GridViewRow` 實例插入控制項階層中。 使用下列程式碼即可完成這項作業：

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample4.cs)]

此程式碼一開始會以程式設計方式參考在 GridView 控制項階層的根目錄中找到的 `Table` 物件，並建立名為 `lastValue`的字串變數。 `lastValue` 可用來比較目前資料列的已排序資料行值與前一個資料列的值。 接下來，會列舉 GridView 的 `Rows` 集合，並針對每個資料列，已排序資料行的值會儲存在 `currentValue` 變數中。

> [!NOTE]
> 若要判斷特定資料列排序資料行的值，我使用 cell `Text` 屬性。 這適用于 BoundFields，但不會如預期般用於 TemplateFields、CheckBoxFields 等等。 我們將在稍後討論如何為替代的 GridView 欄位提供考慮。

然後會比較 `currentValue` 和 `lastValue` 變數。 如果兩者不同，我們需要在控制項階層中加入一個新的分隔資料列。 這是藉由判斷 `Table` 物件 s `Rows` 集合中 `GridViewRow` 的索引、建立新的 `GridViewRow` 和 `TableCell` 實例，然後將 `TableCell` 和 `GridViewRow` 加入至控制項階層來完成。

請注意，分隔符號資料列獨立 `TableCell` 的格式會使其橫跨 GridView 的整個寬度、使用 `SortHeaderRowStyle` CSS 類別進行格式化，並具有其 `Text` 屬性，使其同時顯示排序組名（例如 Category）和 group s 值（例如飲料）。 最後，`lastValue` 會更新為 `currentValue`的值。

用來格式化排序群組標頭資料列 `SortHeaderRowStyle` 的 CSS 類別必須在 `Styles.css` 檔案中指定。 您可以隨意使用任何想要的樣式設定;我使用了下列內容：

[!code-css[Main](creating-a-customized-sorting-user-interface-cs/samples/sample5.css)]

使用目前的程式碼，排序介面會在依任何 BoundField 排序時加入排序群組標頭（請參閱 [圖 5]，這會顯示依供應商排序時的螢幕擷取畫面）。 不過，依任何其他欄位類型（例如 CheckBoxField 或 TemplateField）排序時，不會找到排序群組標頭（請參閱 [圖 6]）。

[![排序介面在依 BoundFields 排序時包含排序群組標頭](creating-a-customized-sorting-user-interface-cs/_static/image12.png)](creating-a-customized-sorting-user-interface-cs/_static/image11.png)

**圖 5**：排序介面包含依 BoundFields 排序時的排序群組標頭（[按一下以查看完整大小的影像](creating-a-customized-sorting-user-interface-cs/_static/image13.png)）

[排序 CheckBoxField 時，![排序群組標頭遺失](creating-a-customized-sorting-user-interface-cs/_static/image15.png)](creating-a-customized-sorting-user-interface-cs/_static/image14.png)

**圖 6**：排序 CheckBoxField （[按一下以觀看完整大小的影像](creating-a-customized-sorting-user-interface-cs/_static/image16.png)）時，排序群組標頭遺失

依 CheckBoxField 排序時，排序群組標頭遺漏的原因是因為程式碼目前僅使用 `TableCell` s `Text` 屬性來判斷每個資料列之已排序資料行的值。 若為 CheckBoxFields，`TableCell` s `Text` 屬性為空字串;相反地，此值可透過位於 `TableCell` s `Controls` 集合內的核取方塊 Web 控制項來取得。

若要處理 BoundFields 以外的欄位類型，我們必須擴充指派 `currentValue` 變數的程式碼，以檢查 `TableCell` s `Controls` 集合中是否存在核取方塊。 不使用 `currentValue = gvr.Cells[sortColumnIndex].Text`，而是將此程式碼取代為下列內容：

[!code-csharp[Main](creating-a-customized-sorting-user-interface-cs/samples/sample6.cs)]

此程式碼會檢查目前資料列的已排序資料行 `TableCell`，以判斷 `Controls` 集合中是否有任何控制項。 如果有，而且第一個控制項是核取方塊，則 `currentValue` 變數會設定為 [是] 或 [否]，視 CheckBox 的 `Checked` 屬性而定。 否則，會從 `TableCell` s `Text` 屬性取得值。 這個邏輯可以複寫來處理可能存在於 GridView 中之任何 TemplateFields 的排序。

在上述程式碼新增中，排序群組標頭現在會在依照已停止的 CheckBoxField 排序時出現（請參閱 [圖 7]）。

[![排序群組標頭現在會在排序 CheckBoxField 時出現](creating-a-customized-sorting-user-interface-cs/_static/image18.png)](creating-a-customized-sorting-user-interface-cs/_static/image17.png)

**圖 7**：排序群組標頭現在會在排序 CheckBoxField 時顯示（[按一下以觀看完整大小的影像](creating-a-customized-sorting-user-interface-cs/_static/image19.png)）

> [!NOTE]
> 如果您的產品具有 [`CategoryID`]、[`SupplierID`] 或 [`UnitPrice`] 欄位的 `NULL` 資料庫值，則這些值預設會顯示為 GridView 中的空字串，這表示具有 `NULL` 值之產品的分隔符號資料列文字將會讀取，如下類別：（也就是類別目錄之後沒有名稱：如 Category：飲料）。 如果您想要在這裡顯示的值，您可以將 [BoundFields [`NullDisplayText`] 屬性](https://msdn.microsoft.com/library/system.web.ui.webcontrols.boundfield.nulldisplaytext.aspx)設為您要顯示的文字，或在將 `currentValue` 指派給 [分隔符號] 資料列 `Text` 屬性時，將條件陳述式加入至 Render 方法。

## <a name="summary"></a>總結

GridView 不包含許多自訂排序介面的內建選項。 不過，有了一些低層級的程式碼，就可以調整 GridView 的控制階層，以建立更多自訂的介面。 在本教學課程中，我們已瞭解如何為可排序的 GridView 新增排序群組分隔符號，以便更輕鬆地識別不同的群組和這些群組界限。 如需自訂排序介面的其他範例，請查看[Scott Guthrie](https://weblogs.asp.net/scottgu/) ，其中[有幾個 ASP.NET 2.0 GridView 排序秘訣和訣竅](https://weblogs.asp.net/scottgu/archive/2006/02/11/437995.aspx)blog 專案。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

> [!div class="step-by-step"]
> [上一頁](sorting-custom-paged-data-cs.md)
> [下一頁](paging-and-sorting-report-data-vb.md)
