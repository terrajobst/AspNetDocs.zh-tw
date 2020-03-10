---
uid: web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
title: 跨兩個頁面的主要/詳細C#資料篩選（） |Microsoft Docs
author: rick-anderson
description: 在本教學課程中，我們將探討如何跨兩個頁面分隔主要/詳細資料包表。 在 [主要] 頁面中，我們使用重複項控制項來呈現 categ 的清單 。
ms.author: riande
ms.date: 10/30/2010
ms.assetid: 68b8c023-92fa-4df6-9563-1764e16e4b04
msc.legacyurl: /web-forms/overview/data-access/filtering-scenarios-with-the-datalist-and-repeater/master-detail-filtering-acess-two-pages-datalist-cs
msc.type: authoredcontent
ms.openlocfilehash: 545b24a66476c55aff88ac62d3a6528105fea6c0
ms.sourcegitcommit: e7e91932a6e91a63e2e46417626f39d6b244a3ab
ms.translationtype: MT
ms.contentlocale: zh-TW
ms.lasthandoff: 03/06/2020
ms.locfileid: "78607076"
---
# <a name="masterdetail-filtering-across-two-pages-c"></a>跨兩個頁面進行主要/詳細資料篩選 (C#)

由[Scott Mitchell](https://twitter.com/ScottOnWriting)

[下載範例應用程式](https://download.microsoft.com/download/9/c/1/9c1d03ee-29ba-4d58-aa1a-f201dcc822ea/ASPNET_Data_Tutorial_34_CS.exe)或[下載 PDF](master-detail-filtering-acess-two-pages-datalist-cs/_static/datatutorial34cs1.pdf)

> 在本教學課程中，我們將探討如何跨兩個頁面分隔主要/詳細資料包表。 在 [主要] 頁面中，我們使用「中繼器」控制項來轉譯類別目錄清單，當按下時，會將使用者帶到「詳細資料」頁面，其中的兩個數據行 DataList 會顯示屬於所選類別目錄的產品。

## <a name="introduction"></a>簡介

在[先前的教學](master-detail-filtering-with-a-dropdownlist-datalist-cs.md)課程中，我們已瞭解如何在單一網頁中顯示主要/詳細資料包表，使用 dropdownlist 進行來顯示「主要」記錄和 DataList 來顯示「詳細資料」。 主要/詳細資料包表使用的另一個常見模式是在一個網頁上擁有主要記錄，並在另一個頁面上提供詳細資料。 在先前[跨兩頁的主要/詳細資料篩選](../masterdetail/master-detail-filtering-across-two-pages-cs.md)教學課程中，我們使用 GridView 來檢查此模式，以顯示系統中的所有供應商。 這個 GridView 包含一個 HyperLinkField，它會轉譯為第二頁的連結，並沿著 querystring 中的 `SupplierID` 傳遞。 第二個頁面會使用 GridView 列出所選供應商所提供的產品。

這類的兩頁主要/詳細資料包表也可以使用 DataList 和重複項控制項來完成。 唯一的差別在於，DataList 和中繼器都不會提供 HyperLinkField 控制項的支援。 相反地，我們必須在控制項的 `ItemTemplate`內加入超連結 Web 控制項或錨點 HTML 元素（`<a>`）。 超連結的 `NavigateUrl` 屬性或錨點的 `href` 屬性可以使用宣告式或程式設計方式進行自訂。

在本教學課程中，我們將探討一個範例，其中會使用重複項控制項來列出一頁上項目符號清單中的分類。 每個清單專案都會包含分類的名稱和描述，而類別目錄名稱會顯示為第二頁的連結。 按一下此連結會將使用者 whisk 到第二個頁面，其中 DataList 會顯示屬於所選類別目錄的產品。

## <a name="step-1-displaying-the-categories-in-a-bulleted-list"></a>步驟1：在項目符號清單中顯示類別

建立任何主要/詳細資料包表的第一個步驟，是從顯示「主要」記錄開始。 因此，我們的第一項工作是在 [主要] 頁面中顯示類別目錄。 開啟 [`DataListRepeaterFiltering`] 資料夾中的 [`CategoryListMaster.aspx`] 頁面，新增 [中繼器] 控制項，然後從智慧標籤加入宣告新的 ObjectDataSource。 設定新的 ObjectDataSource，使其從 `CategoriesBLL` 類別的 `GetCategories` 方法存取其資料（請參閱 [圖 1]）。

[![將 ObjectDataSource 設定為使用 CategoriesBLL 類別的 GetCategories 方法](master-detail-filtering-acess-two-pages-datalist-cs/_static/image2.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image1.png)

**圖 1**：設定 ObjectDataSource 使用 `CategoriesBLL` 類別的 `GetCategories` 方法（[按一下以查看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image3.png)）

接下來，定義中繼器的範本，讓它將每個類別目錄名稱和描述顯示為項目符號清單中的專案。 讓我們不用擔心每個類別都會連結到詳細資料頁面。 以下顯示中繼器和 ObjectDataSource 的宣告式標記：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample1.aspx)]

完成此標記之後，請花一點時間透過瀏覽器來查看進度。 如 [圖 2] 所示，中繼器會轉譯為項目符號清單，其中會顯示每個類別的名稱和描述。

[![每個類別都會顯示為項目符號清單專案](master-detail-filtering-acess-two-pages-datalist-cs/_static/image5.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image4.png)

**圖 2**：每個類別都會顯示為項目符號清單專案（[按一下以查看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image6.png)）

## <a name="step-2-turning-the-category-name-into-a-link-to-the-details-page"></a>步驟2：將類別目錄名稱轉換成詳細資料頁面的連結

若要允許使用者顯示指定分類的「詳細資料」資訊，我們需要新增每個項目符號清單專案的連結，按一下之後，就會將使用者帶到第二頁（`ProductsForCategoryDetails.aspx`）。 第二頁接著會使用 DataList 來顯示所選類別的產品。 為了判斷已按下連結的類別，我們需要透過某種機制，將按下的分類 `CategoryID` 傳遞至第二頁。 將純量資料從一頁傳輸到另一個頁面的最簡單且最直接的方式，是透過 querystring，這是我們將在本教學課程中使用的選項。 特別的是，`ProductsForCategoryDetails.aspx` 頁面會預期選取的 *`categoryID`* 值會透過名為 `CategoryID`的 querystring 欄位傳遞。 例如，若要查看飲料分類的產品，其 `CategoryID` 為1，使用者會造訪 `ProductsForCategoryDetails.aspx?CategoryID=1`。

若要為中繼器中的每個項目符號清單專案建立超連結，我們需要將超連結 Web 控制項或 HTML 錨點專案（`<a>`）新增至 `ItemTemplate`。 在每個資料列的超連結顯示相同的情況下，這兩種方法都是足夠的。 針對中繼器，我偏好使用錨定元素。 若要使用錨點元素，請將中繼器的 ItemTemplate 更新為：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample2.aspx)]

請注意，`CategoryID` 可以直接插入錨點元素的 `href` 屬性中;不過，若要這麼做，請務必將 `href` 屬性的值與單引號（和附注引號）分隔，因為 `href` 屬性內的 `Eval` 方法會以引號分隔其字串（`"CategoryID"`）。 或者，您也可以改用超連結 Web 控制項：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample3.aspx)]

請注意，在使用字串串連的資料系結語法中，如何直接將 URL 的靜態部分（`ProductsForCategoryDetails.aspx?CategoryID`）附加至 `Eval("CategoryID")` 的結果。

使用超連結控制項的其中一個優點是，它可以在必要時，以程式設計方式從中繼器的 `ItemDataBound` 事件處理常式中存取。 例如，您可能會想要將類別名稱顯示為文字，而不是與沒有相關聯產品的類別連結。 這類檢查可以透過程式設計方式在 `ItemDataBound` 事件處理常式中執行;針對沒有相關聯產品的類別目錄，可以將超連結的 `NavigateUrl` 屬性設定為空白字串，因而導致該特定分類名稱轉譯為純文字（而不是連結）。 如需有關根據程式設計 `ItemDataBound` 邏輯來格式化 DataList 和中繼器內容的詳細資訊，請參閱根據資料來格式化 datalist[和中繼器](../displaying-data-with-the-datalist-and-repeater/formatting-the-datalist-and-repeater-based-upon-data-cs.md)教學課程。

如果您遵循，請隨意在頁面中使用錨定元素或超連結控制項方法。 不論何種方法，在瀏覽器中查看時，每個類別目錄名稱都應該轉譯為 `ProductsForCategoryDetails.aspx`的連結，並傳入適用的 `CategoryID` 值（請參閱 [圖 3]）。

[![現在類別目錄名稱連結至 ProductsForCategoryDetails .aspx](master-detail-filtering-acess-two-pages-datalist-cs/_static/image8.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image7.png)

**圖 3**：分類名稱現在會連結至 `ProductsForCategoryDetails.aspx` （[按一下以觀看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image9.png)）

## <a name="step-3-listing-the-products-that-belong-to-the-selected-category"></a>步驟3：列出屬於所選類別的產品

在 [`CategoryListMaster.aspx`] 頁面完成後，我們就準備好將注意力轉換成「詳細資料」頁面，`ProductsForCategoryDetails.aspx`。 開啟此頁面，從 [工具箱] 將 [DataList] 拖曳至設計工具，並將其 [`ID`] 屬性設定為 [`ProductsInCategory`]。 接下來，從 DataList 的智慧標籤選擇將新的 ObjectDataSource 加入至頁面，並將它命名為 `ProductsInCategoryDataSource`。 設定它，使其呼叫 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法;將 [插入]、[更新] 和 [刪除] 索引標籤中的下拉式清單設定為 [（無）]。

[![將 ObjectDataSource 設定為使用 ProductsBLL 類別的 GetProductsByCategoryID （類別 Id）方法](master-detail-filtering-acess-two-pages-datalist-cs/_static/image11.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image10.png)

**圖 4**：設定 ObjectDataSource 使用 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法（[按一下以查看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image12.png)）

由於 `GetProductsByCategoryID(categoryID)` 方法會接受輸入參數（ *`categoryID`* ），因此，[選擇資料來源] 會讓我們有機會指定參數的來源。 使用 QueryStringField `CategoryID`，將參數來源設定為 QueryString。

[![使用 Querystring 欄位類別 Id 做為參數的來源](master-detail-filtering-acess-two-pages-datalist-cs/_static/image14.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image13.png)

**圖 5**：使用 Querystring 欄位 `CategoryID` 做為參數的來源（[按一下以查看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image15.png)）

如我們在先前的教學課程中所見，完成 [選擇資料來源] wizard 之後，Visual Studio 會自動建立 DataList 的 `ItemTemplate`，其中列出每個資料欄位名稱和值。 將此範本取代為只會列出產品名稱、供應商和價格的範本。 此外，將 DataList 的 `RepeatColumns` 屬性設定為2。 這些變更之後，您的 DataList 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample4.aspx)]

若要觀看此頁面的作用，請從 [`CategoryListMaster.aspx`] 頁面啟動;接下來，按一下分類項目符號清單中的連結。 這麼做會將您帶到 `ProductsForCategoryDetails.aspx`，並透過 querystring 傳遞 `CategoryID`。 `ProductsForCategoryDetails.aspx` 中的 `ProductsInCategoryDataSource` ObjectDataSource 會接著取得指定分類的那些產品，並將其顯示在 DataList 中，這會呈現每個資料列的兩個產品。 [圖 6] 顯示觀看飲料時 `ProductsForCategoryDetails.aspx` 的螢幕擷取畫面。

[![顯示飲料，每個資料列兩個](master-detail-filtering-acess-two-pages-datalist-cs/_static/image17.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image16.png)

**圖 6**：顯示飲料，每個資料列兩個（[按一下以觀看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image18.png)）

## <a name="step-4-displaying-category-information-on-productsforcategorydetailsaspx"></a>步驟4：在 ProductsForCategoryDetails 上顯示類別資訊

當使用者按一下 `CategoryListMaster.aspx`中的類別時，系統會將他們納入 `ProductsForCategoryDetails.aspx`，並顯示屬於所選類別目錄的產品。 不過，在 `ProductsForCategoryDetails.aspx` 不會有所選類別的視覺提示。 若使用者要按一下 [飲料]，但不小心按一下 [Condiments]，就無法在到達 `ProductsForCategoryDetails.aspx`時發現錯誤。 為了減輕這個潛在問題，我們可以在 `ProductsForCategoryDetails.aspx` 頁面的頂端顯示所選類別的相關資訊（其名稱和描述）。

若要完成這項操作，請在 `ProductsForCategoryDetails.aspx`的 [中繼器] 控制項上方新增 FormView。 接下來，從名為 `CategoryDataSource` 的 FormView 智慧標籤，將新的 ObjectDataSource 加入至頁面，並將它設定為使用 `CategoriesBLL` 類別的 `GetCategoryByCategoryID(categoryID)` 方法。

[透過 CategoriesBLL 類別的 GetCategoryByCategoryID （類別目錄）方法，![存取類別的相關資訊](master-detail-filtering-acess-two-pages-datalist-cs/_static/image20.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image19.png)

**圖 7**：透過 `CategoriesBLL` 類別的 `GetCategoryByCategoryID(categoryID)` 方法存取類別的相關資訊（[按一下以查看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image21.png)）

如同步驟3中新增的 `ProductsInCategoryDataSource` ObjectDataSource，`CategoryDataSource`的 [設定資料來源] wizard 會提示我們輸入 `GetCategoryByCategoryID(categoryID)` 方法之輸入參數的來源。 使用與之前完全相同的設定，將參數來源設定為 QueryString，並將 QueryStringField 值設為 `CategoryID` （請參閱 [圖 5]）。

完成 wizard 之後，Visual Studio 會自動建立 FormView 的 `ItemTemplate`、`EditItemTemplate`和 `InsertItemTemplate`。 因為我們提供了唯讀介面，所以您可以隨意移除 `EditItemTemplate` 和 `InsertItemTemplate`。 此外，您可以隨意自訂 FormView 的 `ItemTemplate`。 移除多餘的範本並自訂 ItemTemplate 之後，您的 FormView 和 ObjectDataSource 的宣告式標記看起來應該如下所示：

[!code-aspx[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample5.aspx)]

[圖 8] 顯示透過瀏覽器來觀看此頁面時的螢幕擷取畫面。

> [!NOTE]
> 除了 FormView 外，我也在 FormView 上方加入了超連結控制項，讓使用者回到分類清單（`CategoryListMaster.aspx`）。 請隨意將此連結放在別處，或完全省略。

[![類別目錄資訊現在會顯示在頁面頂端](master-detail-filtering-acess-two-pages-datalist-cs/_static/image23.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image22.png)

**圖 8**：類別目錄資訊現在會顯示在頁面頂端（[按一下以觀看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image24.png)）

## <a name="step-5-displaying-a-message-if-no-products-belong-to-the-selected-category"></a>步驟5：如果沒有產品屬於選取的類別，則顯示訊息

[`CategoryListMaster.aspx`] 頁面會列出系統中的所有類別，而不論是否有任何相關聯的產品。 如果使用者按一下沒有相關聯產品的類別，將不會轉譯 `ProductsForCategoryDetails.aspx` 中的 DataList，因為它的資料來源不會有任何專案。 如我們在過去的教學課程中所見，GridView 提供了一個 `EmptyDataText` 屬性，可用於指定在資料來源中沒有任何記錄時所要顯示的文字訊息。 可惜的是，DataList 和中繼器都不會有這類屬性。

若要顯示訊息，通知使用者所選類別沒有符合的產品，我們需要將標籤控制項新增至頁面，其 `Text` 屬性會被指派要在沒有相符產品的事件中顯示的訊息。 然後，我們需要根據 DataList 是否包含任何專案，以程式設計方式設定其 `Visible` 屬性。

若要完成這項操作，請從在 DataList 底下新增標籤開始。 將其 [`ID`] 屬性設定為 [`NoProductsMessage`]，並將其 [`Text`] 屬性設為 [沒有任何產品可供選取的類別 ...]接下來，我們需要根據是否有任何資料系結至 `ProductsInCategory` DataList，以程式設計方式設定此標籤的 `Visible` 屬性。 此指派必須在資料已系結至 DataList 後進行。 針對 GridView、DetailsView 和 FormView，我們可以建立控制項的 `DataBound` 事件的事件處理常式，這會在資料系結完成後引發。 不過，DataList 和中繼器都沒有可用的 `DataBound` 事件。

在此特定範例中，我們可以在 `Page_Load` 事件處理常式中指派標籤的 `Visible` 屬性，因為資料會在頁面的 `Load` 事件之前指派給 DataList。 不過，這種方法在一般情況下無法正常執行，因為 ObjectDataSource 的資料可能會在頁面生命週期的稍後系結至 DataList。 例如，如果顯示的資料是以另一個控制項中的值為基礎，例如在使用 DropDownList 來保存「主要」記錄時顯示主要/詳細報表，則資料可能不會重新系結至資料 Web 控制項，直到頁面生命週期中的 `PreRender` 階段為止。

所有情況下都適用的一個解決方案，就是在系結 `Item` 或 `AlternatingItem`的專案類型時，將 `Visible` 屬性指派給 DataList 的 `ItemDataBound` （或 `ItemCreated`）事件處理常式中的 `False`。 在這種情況下，我們知道資料來源中至少有一個資料項目，因此可以隱藏 `NoProductsMessage` 標籤。 除了這個事件處理常式之外，我們也需要 DataList 的 `DataBinding` 事件的事件處理常式，我們會將標籤的 `Visible` 屬性初始化為 `True`。 因為 `DataBinding` 事件會在 `ItemDataBound` 事件之前引發，所以標籤的 `Visible` 屬性一開始會設定為 `True`;但是，如果有任何資料項目，則會設定為 `False`。 下列程式碼會實行此邏輯：

[!code-csharp[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample6.cs)]

Northwind 資料庫中的所有類別都與一或多個產品相關聯。 為了測試這項功能，我手動調整了本教學課程的 Northwind 資料庫，將所有與產生分類（`CategoryID` = 7）相關聯的產品重新指派給 [海鮮] 類別（`CategoryID` = 8）。 這可以透過選擇 [新增查詢] 並使用下列 `UPDATE` 語句，從伺服器總管完成：

[!code-sql[Main](master-detail-filtering-acess-two-pages-datalist-cs/samples/sample7.sql)]

據以更新資料庫之後，請返回 [`CategoryListMaster.aspx`] 頁面，然後按一下 [產生] 連結。 因為已不再有任何產品屬於 [產生] 分類，所以您應該會看到「選取的類別沒有產品 ...」訊息，如 [圖 9] 所示。

[如果沒有任何產品屬於選取的類別，就會顯示 ![訊息](master-detail-filtering-acess-two-pages-datalist-cs/_static/image26.png)](master-detail-filtering-acess-two-pages-datalist-cs/_static/image25.png)

**圖 9**：如果沒有任何產品屬於選取的類別，就會顯示訊息（[按一下以查看完整大小的影像](master-detail-filtering-acess-two-pages-datalist-cs/_static/image27.png)）

## <a name="summary"></a>總結

雖然主要/詳細資料包表可以在單一頁面上顯示主要和詳細資料記錄，但在許多網站中，它們會分成兩個網頁。 在本教學課程中，我們探討了如何使用「主要」網頁中的重複項和 [詳細資料] 頁面中列出的相關聯產品，讓類別目錄列在項目符號清單中，以執行這類主要/詳細資料包告。 主要網頁中的每個清單專案都包含 [詳細資料] 頁面的連結，這些資訊會沿著資料列的 `CategoryID` 值傳遞。

在詳細資料頁面中，您可以透過 `ProductsBLL` 類別的 `GetProductsByCategoryID(categoryID)` 方法，針對指定的供應商來取得這些產品。 *`categoryID`* 參數值是使用 `CategoryID` querystring 值做為參數來源，以宣告方式指定。 我們也探討了如何使用 FormView 在詳細資料頁面中顯示類別目錄詳細資料，以及如果沒有任何產品屬於選取的類別，如何顯示訊息。

快樂的程式設計！

## <a name="about-the-author"></a>關於作者

[Scott Mitchell](http://www.4guysfromrolla.com/ScottMitchell.shtml)，自1998起，有七個 ASP/ASP. NET 書籍和創辦人的[4GuysFromRolla.com](http://www.4guysfromrolla.com)。 Scott 以獨立的顧問、訓練員和作者的身分運作。 他的最新著作是[*在24小時內讓自己的 ASP.NET 2.0*](https://www.amazon.com/exec/obidos/ASIN/0672327384/4guysfromrollaco)。 他可以在mitchell@4GuysFromRolla.com觸達[。](mailto:mitchell@4GuysFromRolla.com) 或者透過他的 blog，可以在[http://ScottOnWriting.NET](http://ScottOnWriting.NET)找到。

## <a name="special-thanks-to"></a>特別感謝 。

本教學課程系列已由許多有用的審核者所審查。 本教學課程的領導審查者為 Zack，Liz Shulok。 有興趣複習我即將發行的 MSDN 文章嗎？ 若是如此，請在mitchell@4GuysFromRolla.com的那一行下拉式[。](mailto:mitchell@4GuysFromRolla.com)

> [!div class="step-by-step"]
> [上一頁](master-detail-filtering-with-a-dropdownlist-datalist-cs.md)
> [下一頁](master-detail-using-a-bulleted-list-of-master-records-with-a-details-datalist-cs.md)
